---
uid: signalr/overview/older-versions/working-with-groups
title: "Работа с группами в SignalR 1.x | Документы Microsoft"
author: pfletcher
description: "Описывается, как сохранить сведения о членстве в группах с помощью API концентратора."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/21/2013
ms.topic: article
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 04da74f23663313e70e54fd4f2f9e5f005791cff
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="working-with-groups-in-signalr-1x"></a>Работа с группами в SignalR 1.x
====================
по [Флетчера Патрик](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

> В этом разделе описывается добавление пользователей в группы и сохраняет сведения о членстве в группе.


## <a name="overview"></a>Обзор

Группы в SignalR предоставляют метод для широковещательной рассылки сообщений для указанного подмножества подключенных клиентов. Группа может иметь любое количество клиентов, и клиент может быть членом любое количество групп. Не нужно явно создавать группы. В результате группа автоматически создается впервые, укажите его имя в вызове Groups.Add и удаляется при удалении последнего соединения через членство в ней. Сведения об использовании групп, в разделе [как управлять членством в группах от концентратора класса](index.md) в API концентраторов — руководство по Server.

Нет никакой интерфейс API для получения список членства в группе или список групп. SignalR отправляет сообщения клиентам и группам на основе модели публикации и подписке, а сервер не поддерживает списки групп или членства в группах. Это позволяет увеличить масштабируемость, так как каждый раз при добавлении узла к веб-ферме, любое состояние, которое поддерживает SignalR для нового узла.

При добавлении пользователя в группу с помощью `Groups.Add` метод, пользователь получает сообщения направляются в эту группу, в течение текущего соединения, но членства пользователя в этой группе не сохраняется вне текущего соединения. Если вы хотите окончательно сохранить сведения о группах и членства в группе, эти данные необходимо хранить в хранилище, например базы данных или хранилище таблиц Azure. Затем при каждом подключении пользователя к приложению, получения из репозитория каким группам принадлежит пользователь и вручную добавьте пользователя к группам.

При повторном подключении после временному перерыву в предоставлении, пользователь автоматически повторно присоединяет групп ранее назначены. Автоматическое повторное присоединение группы применяется только при повторном подключении не при установке нового подключения. Токен цифровой подписью передается от клиента, который содержит список групп ранее назначены. Если вы хотите проверить принадлежность пользователя к запрошенной группы, можно переопределить поведение по умолчанию.

Этот раздел включает следующие подразделы:

- [Добавление и удаление пользователей](#add)
- [Вызов членов группы](#call)
- [Хранение в базе данных членства в группе](#storedatabase)
- [Членство в группе хранения в хранилище таблиц Azure](#storeazuretable)
- [Проверка членства в группе при повторном подключении](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>Добавление и удаление пользователей

Чтобы добавить или удалить пользователей из группы, следует вызвать [добавить](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) или [удалить](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) методы и передайте ему идентификатор соединения пользователя и имя группы в качестве параметров. Необходимо вручную удалить пользователя из группы при завершении соединения.

В следующем примере показан `Groups.Add` и `Groups.Remove` методы, которые используются в методах Hub.

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

`Groups.Add` И `Groups.Remove` методы асинхронного выполнения.

Если вы хотите добавить в группу клиента и немедленно отправить клиенту сообщение с помощью в группу необходимо убедитесь в том, что метод Groups.Add сначала завершается. В следующем примере кода показано, как сделать это с помощью кода, который работает в .NET 4.5, а другой с помощью кода, который работает в .NET 4.

#### <a name="asynchronous-net-45-example"></a>Асинхронные .NET 4.5 пример

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a>Асинхронные .NET Framework 4 пример

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

В общем случае не следует включать `await` при вызове `Groups.Remove` метода, так как идентификатор соединения, который вы пытаетесь удалить становятся доступны. В этом случае `TaskCanceledException` возникает после истечения срока действия запроса. Если приложение необходимо убедиться, что пользователь был удален из группы перед отправкой сообщения в группу, можно добавить `await` до Groups.Remove, а затем catch `TaskCanceledException` исключение, которое может быть создано.

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>Вызов членов группы

Можно отправлять сообщения для всех членов группы или только указанные члены группы, как показано в следующих примерах.

- **Все** подключенных клиентов в указанной группе. 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- Все подключенные клиенты в указанной группе **указанным клиентам, за исключением**, указанный с помощью идентификатор соединения. 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- Все подключенные клиенты в указанной группе **, кроме вызывающего клиента**. 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>Хранение в базе данных членства в группе

В следующих примерах для сохранения данных пользователей и групп в базе данных. Можно использовать любой технологии доступа к данным; Тем не менее в приведенном ниже примере показан способ определения модели с использованием платформы Entity Framework. Эти модели сущностей соответствующие таблицы базы данных и полей. Структуру данных может значительно различаться в зависимости от требований приложения. В этом примере включает класс `ConversationRoom` которого будут уникальны для приложения, которое позволяет пользователям присоединяться к обсуждения различных задач, таких как спортивных или садом. Этот пример также содержит класс для соединения. Класс соединений не являются необходимыми для отслеживания членство в группе, но часто является частью надежное решение для отслеживания пользователей.

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

Затем в концентраторе, можно получить сведения о группе и пользователя из базы данных и вручную добавьте пользователя в соответствующие группы. Пример не включает код для отслеживания пользовательских соединений. В этом примере `await` ключевое слово не применяется перед `Groups.Add` так, как сообщения не отправляются немедленно для членов группы. Если вы хотите отправить сообщение всем членам группы сразу после добавления нового члена, может потребоваться применить `await` ключевое слово, чтобы убедиться, что асинхронная операция завершена.

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Членство в группе хранения в хранилище таблиц Azure

С помощью табличного хранилища Azure для хранения данных пользователей и групп аналогична использованию базы данных. В следующем примере показано сущности таблицы, в которой хранится имя пользователя и имя группы.

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

В концентраторе получить назначенной группы при подключении.

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>Проверка членства в группе при повторном подключении

По умолчанию SignalR автоматически повторно назначает пользователя в соответствующие группы при повторном подключении от временного прерывания, таких как после удалены и повторно установить подключение времени ожидания соединения. Сведения о группе пользователя передается в токене при повторном подключении, и этот маркер проверяется на сервере. Сведения о процессе проверки повторное присоединение пользователей к группам см. в разделе [повторное присоединение групп при повторном подключении](index.md).

В общем случае следует использовать поведение по умолчанию автоматически присоединяется что групп на повторное подключение. SignalR группы не войдут в качестве механизма безопасности для ограничения доступа к конфиденциальным данным. Тем не менее если приложение необходимо тщательно членства пользователя в группе при повторном подключении, можно переопределить поведение по умолчанию. Изменение поведения по умолчанию можно добавить нагрузку для базы данных, так как членство в группе пользователей должны извлекаться для каждого повторное подключение, а не только в том случае, когда пользователь подключается.

Если необходимо проверить членство в группе на повторное подключение, создайте новый модуль конвейер концентратора, возвращающий список назначенных групп, как показано ниже.

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

Затем добавьте этот модуль в конвейер концентратора, как показано ниже.

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]