---
title: "Используйте шаблон проекта реагирование на них"
author: SteveSandersonMS
description: "Сведения о начале работы с использованием шаблона проекта ASP.NET Core одностраничного приложения (SPA) версии кандидата для реагирование на них и создать реагирование на них приложений."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/06/2017
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/react
ms.openlocfilehash: 5978094083a098a771f5dca103434ea8fcce7777
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="use-the-react-project-template-release-candidate"></a>Используйте шаблон проекта реагировать (версия-кандидат)

> [!NOTE]
> В этой документации не о шаблоне проекта выпущено реагирование на них. **Данная документация является о версии-кандидате шаблона реагирование на них.** Мы надеемся, что для отправки в начале 2018 выпущенной версии.

Обновленный шаблон проекта реагирование на них предоставляет удобную начальную точку для ASP.NET Core приложений с помощью реагирование на них и [создать реагирование на них приложении](https://github.com/facebookincubator/create-react-app) (CRA) соглашения для реализации полнофункционального клиентского пользовательского интерфейса (UI).

Шаблон соответствует Создание проекта ASP.NET Core в качестве внутренних API и в стандартном проекте CRA реагирования для работы в пользовательском Интерфейсе, а с удобством размещение их в проект одного приложения, можно выполнять построение и публикуются как единое целое.

## <a name="create-a-new-app"></a>Создание нового приложения

Чтобы начать, убедитесь, вы уже [установить обновленный шаблон проекта реагирование на них](xref:spa/index#installation). Эти инструкции не относятся к предыдущей шаблон проекта реагирование на них, включенные в .NET Core 2.0.x SDK.

Создание нового проекта из командной строки с помощью команды `dotnet new react` в пустой каталог. Например, следующие команды создают приложения в *Мои новое приложение* каталога и перейти к этому каталогу:

```console
dotnet new react -o my-new-app
cd my-new-app
```

Запустите приложение из Visual Studio или .NET Core CLI:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Откройте созданный *.csproj* файл и запустить приложение в обычном режиме оттуда.

Процесс построения восстанавливает npm зависимостей при первом выполнении может занять несколько минут. Последующие сборки выполняется гораздо быстрее.

# <a name="net-core-clitabnetcore-cli"></a>[Интерфейс командной строки .NET Core](#tab/netcore-cli)

Убедитесь в наличии переменной среды `ASPNETCORE_Environment` со значением `Development`. В Windows (в запросах не PowerShell) запускаются `SET ASPNETCORE_Environment=Development`. В Linux или macOS, запустите `export ASPNETCORE_Environment=Development`.

Запустите `dotnet build` для проверки приложения правильно ли выполняется сборка. Во время первого выполнения процесса построения восстанавливает npm зависимости, что может занять несколько минут. Последующие сборки выполняется гораздо быстрее.

Запустите `dotnet run` для запуска приложения.

---

Шаблон проекта создает приложение ASP.NET Core и реагирование на них приложение. Приложения ASP.NET Core предназначен для использования для доступа к данным, авторизации и других проблем на стороне сервера. Реагирование на них приложения, размещенные в *ClientApp* подкаталог, предназначен для использования все проблемы пользовательского интерфейса.

## <a name="add-pages-images-styles-modules-etc"></a>Добавление страниц, изображений, стили, модули, и т. д.

*ClientApp* каталог представляет собой стандартный приложение CRA реагирования. В разделе официальные [CRA документации](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) для получения дополнительной информации.

Существуют небольшие различия между реагирование на них приложений, созданных с использованием этого шаблона и созданные CRA самостоятельно. Однако в приложении возможности не изменились. Приложение, созданное с помощью шаблона содержит [начальной загрузки](https://getbootstrap.com/)-макета и простой пример маршрутизации на основе.

## <a name="install-npm-packages"></a>Установка пакета npm

Для установки пакета npm сторонних разработчиков, используйте в командной *ClientApp* подкаталог. Пример:

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a>Публикация и развертывание

В разработке приложение запускается в режиме, оптимизированный для удобства разработчиков. Например JavaScript пакеты содержат исходное сопоставление, (что, когда отладка, вы можете просмотреть исходный код). Приложение отслеживает JavaScript, HTML и CSS в файл изменения на диске и автоматически перекомпилирует и перезагружает, когда она видит эти файлы изменения.

В рабочей среде обслуживать версии приложения, оптимизированный для производительности. Это настраивается происходит автоматически. При публикации, конфигурации построения выдает уменьшенный, transpiled построения клиентского кода. В отличие от сборки разработки рабочей сборки не требует Node.js установлен на сервере.

Можно использовать стандартный [методы размещения и развертывания ASP.NET Core](xref:host-and-deploy/index).

## <a name="run-the-cra-server-independently"></a>Запустите сервер CRA независимо друг от друга

Проект настроен для запуска собственного экземпляра сервера разработки CRA в фоновом режиме при запуске приложения ASP.NET Core в режиме разработки. Это удобно, так как это означает, что не нужно вручную запустить отдельный сервер.

Недостаток этой настройки по умолчанию не существует. Каждый раз при изменении кода на C# и ASP.NET основные приложения необходима перезагрузка, CRA сервер перезагрузится. Чтобы запустить резервное копирование необходимы через несколько секунд. Если вы вносите частые изменения кода C# и не хотите ждать CRA к перезагрузке сервера, запустите сервера CRA извне, независимо от процесса ASP.NET Core. Для этого:

1. В командной строке перейдите в *ClientApp* подкаталог и запустить на сервере разработки CRA:

    ```console
    cd ClientApp
    npm start
    ```

2. Измените приложения ASP.NET Core к использованию экземпляра сервера внешней CRA вместо запуска одного свои собственные. В вашей *запуска* класса, замените `spa.UseReactDevelopmentServer` вызова со следующими:

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

При запуске приложения ASP.NET Core, этого не будет запущен сервер CRA. Вместо него используется экземпляр, который можно запустить вручную. Это позволяет запустить и перезапустить быстрее. Реагирование на них приложения для перестроения каждый раз больше не ожидает.
