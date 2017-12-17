---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
title: "Создание и управление ролями (VB) | Документы Microsoft"
author: rick-anderson
description: "Этот учебник рассматриваются действия, необходимые для настройки ролей framework. После этого будет создан веб-страницы для создания и удаления ролей."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/24/2008
ms.topic: article
ms.assetid: 83af9f5f-9a00-4f83-8afc-e98bdd49014e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
msc.type: authoredcontent
ms.openlocfilehash: a67065a33bb38388ab941c785b7dcc268645ceca
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="creating-and-managing-roles-vb"></a>Создание и управление ролями (Visual Basic)
====================
по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Загрузить код](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.09.zip) или [скачать PDF](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_vb.pdf)

> Этот учебник рассматриваются действия, необходимые для настройки ролей framework. После этого будет создан веб-страницы для создания и удаления ролей.


## <a name="introduction"></a>Вступление

В <a id="_msoanchor_1"> </a> [ *авторизации на основе пользователя* ](../membership/user-based-authorization-vb.md) учебника мы рассмотрели использование авторизации URL-адреса для ограничения определенных пользователей из нескольких страниц и изучения декларативный и программные способы настройки функциональности страницей ASP.NET, основанной на посетителя. Предоставление разрешения для доступа к странице или функций на основе пользователя по, тем не менее, могут стать кошмар в сценариях при наличии нескольких учетных или при часто изменяются права пользователей. Любое время, пользователь получает или теряет авторизации для выполнения определенной задачи, администратору необходимо обновить соответствующие правила авторизации URL-адрес, декларативная разметка и код.

Обычно помогает классифицировать пользователей по группам или *ролей* и затем применить разрешения для роли, роли отдельно. Например большинство веб-приложений имеют определенный набор страниц или задачи, которые защищены только для пользователей с правами администратора. С помощью методик, рассмотренных в *авторизации на основе пользователя* учебник, мы бы добавили соответствующие правила авторизации URL-адрес, декларативная разметка и код, чтобы разрешить указанные учетные записи пользователей для выполнения административных задач. Но если был добавлен новый администратор или администратор существующих необходимых для ее отменить права администратора, придется вернуться и обновить файлы конфигурации и веб-страниц. С ролями тем не менее, мы могли бы создать роль, называются администраторами и назначить эти доверенных пользователей в роли "Администраторы". Затем мы добавьте соответствующие правила авторизации URL-адрес, декларативная разметка и код, чтобы разрешить роли "Администраторы" для выполнения различных административных задач. С этой инфраструктуры Добавление новых администраторов для узла или удаления существующих сводится добавления или удаления пользователя из роли "Администраторы". Нет конфигурации, декларативная разметка или изменения кода не требуются.

ASP.NET предоставляет платформу ролей для определения ролей и связывании их с учетными записями пользователей. С помощью платформы ролей можно создавать и удалять роли, добавлять или удалять пользователей из роли, определите набор пользователей, которые принадлежат определенной роли и определить, принадлежит ли пользователь к определенной роли. После настройки роли framework мы можно ограничить доступ к страницам на основе роли, роли, используя правила авторизации URL-адрес и Показать или скрыть дополнительные сведения или функциональность страницы на основе ролей выполнившего вход пользователя.

Этот учебник рассматриваются действия, необходимые для настройки ролей framework. После этого будет создан веб-страницы для создания и удаления ролей. В <a id="_msoanchor_2"> </a> [ *назначение ролей пользователям* ](assigning-roles-to-users-vb.md) учебника рассматривается как добавлять и удалять пользователей из ролей. И в <a id="_msoanchor_3"> </a> [ *авторизации на основе ролей* ](role-based-authorization-vb.md) учебнике будет показано, как ограничить доступ к страницам на основе роли, роли том, как настроить в зависимости от функциональности страницы в роли посещение пользователя. Давайте начнем!

## <a name="step-1-adding-new-aspnet-pages"></a>Шаг 1: Добавление новых страниц ASP.NET

В этом учебнике и двух следующих мы остановимся подробнее различные функции, связанные с ролями и возможности. Нам потребуется несколько страниц ASP.NET для реализации в разделах, проверяются на протяжении этих учебников. Давайте создайте эти страницы и обновление карты сайта.

Начните с создания новой папки в проект с именем `Roles`. Добавьте четыре новых страниц ASP.NET для `Roles` папки, связывание с каждой страницы `Site.master` главной страницы. Имя страницы:

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

На этом этапе проекта в обозревателе решений должен выглядеть примерно на рисунке показано на рис. 1.


[![Были добавлены четыре новых страниц папку «роли»](creating-and-managing-roles-vb/_static/image2.png)](creating-and-managing-roles-vb/_static/image1.png)

**Рис. 1**: четыре новые страницы были добавлены к `Roles` папку ([Просмотр полноразмерное изображение](creating-and-managing-roles-vb/_static/image3.png))


Каждой странице на этом этапе необходимо двух элементов управления содержимым, один для каждого из главной страницы ContentPlaceHolders: `MainContent` и `LoginContent`.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample1.aspx)]

Помните, что `LoginContent` разметки ContentPlaceHolder элемента по умолчанию отображает ссылку на входе и выходе из системы сайта, в зависимости от того, является ли пользователь проверку подлинности. Наличие `Content2` содержимого элемента управления на странице ASP.NET, переопределяет разметки главной страницы по умолчанию. Как уже говорилось в <a id="_msoanchor_4"> </a> [ *Общие сведения для проверки подлинности форм* ](../introduction/an-overview-of-forms-authentication-vb.md) учебник, переопределение разметки по умолчанию полезно на страницах, где мы должны отображаться входа параметры в левом столбце.

Для этих четырех страниц, тем не менее, мы хотим Показать разметки главной страницы по умолчанию для `LoginContent` ContentPlaceHolder. Таким образом, удалить декларативная разметка для `Content2` элемент управления содержимым. После этого, каждый из четырех страницы разметки должен содержать только один элемент управления содержимым.

Наконец, давайте обновление карты узла (`Web.sitemap`) для включения этих новых веб-страниц. Добавьте следующий код XML после `<siteMapNode>` мы добавили учебников членства.

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample2.xml)]

С обновить карты веб-узла на узле с помощью браузера. Как показано на рисунке 2, навигации в левой части теперь включает элементы для роли учебники.


[![Были добавлены четыре новых страниц папку «роли»](creating-and-managing-roles-vb/_static/image5.png)](creating-and-managing-roles-vb/_static/image4.png)

**На рисунке 2**: четыре новые страницы были добавлены к `Roles` папку ([Просмотр полноразмерное изображение](creating-and-managing-roles-vb/_static/image6.png))


## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>Шаг 2: Указание и настройка поставщика ролей Framework

Например framework членство в роли framework строится поверх модель поставщика. Как было сказано в <a id="_msoanchor_5"> </a> [ *основы безопасности и поддержкой ASP.NET* ](../introduction/security-basics-and-asp-net-support-vb.md) учебник, .NET Framework имеется три встроенных поставщиков ролей: [ `AuthorizationStoreRoleProvider` ](https://msdn.microsoft.com/en-us/library/system.web.security.authorizationstoreroleprovider.aspx) , [ `WindowsTokenRoleProvider` ](https://msdn.microsoft.com/en-us/library/system.web.security.windowstokenroleprovider.aspx), и [ `SqlRoleProvider` ](https://msdn.microsoft.com/en-us/library/system.web.security.sqlroleprovider.aspx). Этого учебника посвящены `SqlRoleProvider`, где используется базы данных Microsoft SQL Server в качестве хранилища ролей.

В системе framework ролей и `SqlRoleProvider` работают так же, как платформа членства и `SqlMembershipProvider`. Платформа .NET Framework содержит `Roles` класс, который служит в качестве API для платформы ролей. `Roles` Класс общие методы, такие как `CreateRole`, `DeleteRole`, `GetAllRoles`, `AddUserToRole`, `IsUserInRole`, и т. д. При вызове одного из этих методов `Roles` класс делегирует вызов настроенного поставщика. `SqlRoleProvider` Работает с таблицами конкретных ролей (`aspnet_Roles` и `aspnet_UsersInRoles`) в ответе.

Чтобы использовать `SqlRoleProvider` поставщика в приложении, нам нужно указать, что базы данных для использования в качестве хранилища. `SqlRoleProvider` Ожидает, что хранилище указанную роль, имеют определенные таблицы базы данных, представления и хранимые процедуры. Эти объекты необходимые базы данных могут быть добавлены с помощью [ `aspnet_regsql.exe` средство](https://msdn.microsoft.com/en-us/library/ms229862.aspx). На этом этапе мы уже имеется база данных со схемой, необходимые для `SqlRoleProvider`. В <a id="_msoanchor_6"> </a> [ *создания схемы членства в SQL Server* ](../membership/creating-the-membership-schema-in-sql-server-vb.md) учебника мы создали базу данных с именем `SecurityTutorials.mdf` и использовать `aspnet_regsql.exe` Чтобы добавить приложение службы, которые включены требуемые объекты базы данных `SqlRoleProvider`. Поэтому нам просто нужно сообщить платформе ролей для поддержки роли и использовать `SqlRoleProvider` с `SecurityTutorials.mdf` базы данных в качестве хранилища ролей.

Платформа ролей настраивается с помощью `<roleManager>` элемента в приложении `Web.config` файла. По умолчанию поддержка ролей отключена. Чтобы включить его, необходимо задать [ `<roleManager>` ](https://msdn.microsoft.com/en-us/library/ms164660.aspx) элемента `enabled` атрибут `true` следующим образом:

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample3.xml)]

По умолчанию все веб-приложения имеют поставщик ролей, с именем `AspNetSqlRoleProvider` типа `SqlRoleProvider`. Этот поставщик по умолчанию регистрируется в `machine.config` (расположенный в `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`):

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample4.xml)]

Поставщик `connectionStringName` атрибут указывает, используется хранилище роли. `AspNetSqlRoleProvider` Этот атрибут задает поставщик `LocalSqlServer`, которая определена в `machine.config` и точки, по умолчанию для базы данных SQL Server 2005, экспресс-выпуск в `App_Data` папку с именем `aspnet.mdf`.

Следовательно Если мы просто включить платформу роли без указания сведения о поставщиках в нашем приложении `Web.config` файл, приложение использует поставщик ролей по умолчанию зарегистрированные `AspNetSqlRoleProvider`. Если `~/App_Data/aspnet.mdf` базы данных не существует, среда выполнения ASP.NET будет автоматически создать его и добавить схему службы приложения. Тем не менее, мы не хотим использовать `aspnet.mdf` в базе данных; вместо этого мы хотим использовать `SecurityTutorials.mdf` базы данных, мы уже созданы и добавлены схемы служб приложений для. Это изменение можно одним из двух способов:

- **Укажите значение для ***`LocalSqlServer`*** имя строки подключения в ***`Web.config`***.** Путем перезаписи `LocalSqlServer` значение имя строки подключения в `Web.config`, можно использовать поставщик ролей по умолчанию зарегистрированные (`AspNetSqlRoleProvider`) и его правильной работы с `SecurityTutorials.mdf` базы данных. Дополнительные сведения об этом приеме см. в разделе [Скотт Гатри](https://weblogs.asp.net/scottgu/)в записи блога [Настройка ASP.NET 2.0 служб приложений для использования SQL Server 2000 или SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx).
- **Добавить новый зарегистрированный поставщик типа ***`SqlRoleProvider`*** и настройте его ***`connectionStringName`*** параметр, чтобы она указывала на ***`SecurityTutorials.mdf`*** базы данных.** Именно этот подход рекомендуется и использовать в <a id="_msoanchor_7"> </a> [ *создания схемы членства в SQL Server* ](../membership/creating-the-membership-schema-in-sql-server-vb.md) учебника, который подход, который будет использовать в этом учебнике также.

Добавьте следующую разметку конфигурации ролей для `Web.config` файла. Эта разметка регистрирует нового поставщика с именем`SecurityTutorialsSqlRoleProvider.`

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample5.xml)]

Выше разметка определяет `SecurityTutorialsSqlRoleProvider` как поставщик по умолчанию (через `defaultProvider` атрибута в `<roleManager>` элемент). Также задает `SecurityTutorialsSqlRoleProvider` `applicationName` параметру `SecurityTutorials`, который одинаков `applicationName` параметра, который используется поставщиком членства (`SecurityTutorialsSqlMembershipProvider`). Пока не показано здесь, [ `<add>` элемент](https://msdn.microsoft.com/en-us/library/ms164662.aspx) для `SqlRoleProvider` также может содержать `commandTimeout` атрибут, чтобы указать длительность времени ожидания базы данных, в секундах. Значение по умолчанию — 30.

Эта разметка конфигурации на месте мы готовы начать использовать функции в приложении.

> [!NOTE]
> Демонстрируются выше разметку настройки `<roleManager>` элемента `enabled` и `defaultProvider` атрибуты. Существует несколько других атрибутов, влияющих на как framework ролей связывает сведения о роли на основе пользователя по. Мы рассмотрим эти параметры в <a id="_msoanchor_8"> </a> [ *авторизации на основе ролей* ](role-based-authorization-vb.md) учебника.


## <a name="step-3-examining-the-roles-api"></a>Шаг 3: Проверка роли API-Интерфейс

Framework ролей функциональность предоставляется через [ `Roles` класса](https://msdn.microsoft.com/en-us/library/system.web.security.roles.aspx), который содержит тринадцать общих методов для выполнения операций на основе ролей. Если взглянуть на создание и удаление ролей в шагах 4 и 6, мы будем использовать [ `CreateRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.createrole.aspx) и [ `DeleteRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.deleterole.aspx) методы, которые можно добавить или удалить роль из системы.

Чтобы получить список всех ролей в системе, используйте [ `GetAllRoles` метод](https://msdn.microsoft.com/en-us/library/system.web.security.roles.getallroles.aspx) (см. шаг 5). [ `RoleExists` Метод](https://msdn.microsoft.com/en-us/library/system.web.security.roles.roleexists.aspx) возвращает логическое значение, указывающее, существует ли указанной роли.

В следующем уроке мы рассмотрим, как для связывания пользователей с ролями. `Roles` Класса [ `AddUserToRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.addusertorole.aspx), [ `AddUserToRoles` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.addusertoroles.aspx), [ `AddUsersToRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.adduserstorole.aspx), и [ `AddUsersToRoles` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.adduserstoroles.aspx) методы добавления одного или нескольких пользователей для одной или нескольких ролей. Чтобы удалить пользователей из роли, используйте [ `RemoveUserFromRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.removeuserfromrole.aspx), [ `RemoveUserFromRoles` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.removeuserfromroles.aspx), [ `RemoveUsersFromRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.removeusersfromrole.aspx), или [ `RemoveUsersFromRoles` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.removeusersfromroles.aspx) методы.

В <a id="_msoanchor_9"> </a> [ *авторизации на основе ролей* ](role-based-authorization-vb.md) учебнике мы рассмотрим способы программным путем отображение и скрытие функциональных возможностей, основанных на роли текущего вошедшего пользователя. Для выполнения этой задачи можно использовать класс ролей [ `FindUsersInRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.findusersinrole.aspx), [ `GetRolesForUser` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.getrolesforuser.aspx), [ `GetUsersInRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.getusersinrole.aspx), или [ `IsUserInRole` ](https://msdn.microsoft.com/en-us/library/system.web.security.roles.isuserinrole.aspx) методы.

> [!NOTE]
> Имейте в виду, что любое время эти методы вызывается, `Roles` класс делегирует вызов настроенного поставщика. В нашем случае это означает, что вызов отправляется `SqlRoleProvider`. `SqlRoleProvider` Затем выполняет операцию соответствующей базы данных, в зависимости от вызываемого метода. Например, код `Roles.CreateRole("Administrators")` приводит к `SqlRoleProvider` выполнение `aspnet_Roles_CreateRole` хранимая процедура, которая вставляет новую запись в `aspnet_Roles` таблицу с именем администраторов.


В оставшейся части этого учебника рассматривается использование `Roles` класса `CreateRole`, `GetAllRoles`, и `DeleteRole` методы для управления ролями в системе.

## <a name="step-4-creating-new-roles"></a>Шаг 4: Создание новых ролей

Роли предоставляют способ произвольно группы пользователей, и наиболее часто это группирование используется для более удобным способом для применения правила авторизации. Однако для использования ролей как механизм авторизации, сначала необходимо определить, какие роли существуют в приложении. К сожалению ASP.NET не включает элемент управления CreateRoleWizard. Чтобы добавить новые роли, нам нужно создания подходящего пользовательского интерфейса и вызова API ролей сами. Хорошо то, что это очень легко осуществить.

> [!NOTE]
> Несмотря на отсутствие не CreateRoleWizard веб-элемент управления, имеется [ASP.NET Web Site Administration Tool](https://msdn.microsoft.com/en-us/library/ms228053.aspx), который является локальным приложением ASP.NET, предназначенных для упрощения просмотра и управления конфигурацией веб-приложения. Тем не менее я не большой вентилятор средства администрирования веб-сайта ASP.NET по двум причинам. Во-первых он немного дефектный и взаимодействие с пользователем оставляет много необходимое. Во-вторых ASP.NET Web Site Administration Tool позволяет работать только локально, это означает, что придется создавать свои собственные роли управления веб-страницы, если вам нужно удаленно управлять ролями на действующем сайте. Эти две причины этого учебника, а затем основное внимание уделяется построения необходимые роли средства управления на веб-странице, а не полагаться на ASP.NET Web Site Administration Tool.


Откройте `ManageRoles.aspx` страницы в `Roles` папку и добавьте текстовое поле и кнопку веб-элемент управления на страницу. Задать для элемента управления TextBox `ID` свойства `RoleName` и кнопки `ID` и `Text` свойства `CreateRoleButton` и создать роль, соответственно. На этом этапе декларативная разметка страницы должен выглядеть следующим образом:

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample6.aspx)]

Далее дважды щелкните `CreateRoleButton` кнопки элемента управления в конструктор для создания `Click` обработчик событий и затем добавьте следующий код:

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample7.vb)]

Приведенный выше код запускается, назначив имя усеченную роли, введенное в `RoleName` TextBox для `newRoleName` переменной. Далее, `Roles` класса `RoleExists` вызывается метод, чтобы определить роль `newRoleName` уже существует в системе. Если роль не существует, он создается путем вызова `CreateRole` метод. Если `CreateRole` методу передается имя роли, который уже существует в системе, `ProviderException` исключения. Именно поэтому код сначала проверяет, чтобы убедиться, что роль уже существует в системе перед вызовом `CreateRole`. `Click` Завершении работы обработчика событий при очистке `RoleName` текстового поля `Text` свойство.

> [!NOTE]
> Может возникнуть вопрос что произойдет, если пользователь не вводит любое значение в `RoleName` текстового поля. Если значение, передаваемое в `CreateRole` метод `Nothing` или является пустой строкой, исключение возникает. Аналогично Если имя роли содержит запятую, возникает исключение. Следовательно страница должна содержать проверяющие элементы управления, чтобы убедиться, что пользователь вводит роль и что он не содержит запятые. Я оставьте в качестве упражнения для модуля чтения.


Давайте создадим роль с именем администраторов. Посетите `ManageRoles.aspx` страницы через браузер, введите в текстовое поле Администраторы (см. рис. 3), а затем нажмите кнопку Создать роль.


[![Создание роли администраторов](creating-and-managing-roles-vb/_static/image8.png)](creating-and-managing-roles-vb/_static/image7.png)

**Рис. 3**: Создание роли администраторов ([Просмотр полноразмерное изображение](creating-and-managing-roles-vb/_static/image9.png))


Что происходит? Обратная передача, но есть не визуальная подсказка, которая фактически было роли добавлены к системе. Корпорация Майкрософт будет обновлять эту страницу в шаге 5, чтобы включить визуальную обратную связь. Теперь, тем не менее, можно проверить, последовательно выбрав пункты создана роль `SecurityTutorials.mdf` базы данных и отображения данных из `aspnet_Roles` таблицы. Как показано на рис. 4, `aspnet_Roles` таблица содержит запись для только что добавленные ролей администраторов.


[![Aspnet_Roles таблица содержит строку для администраторов](creating-and-managing-roles-vb/_static/image11.png)](creating-and-managing-roles-vb/_static/image10.png)

**Рис. 4**: `aspnet_Roles` таблица содержит строку для администраторов ([Просмотр полноразмерное изображение](creating-and-managing-roles-vb/_static/image12.png))


## <a name="step-5-displaying-the-roles-in-the-system"></a>Шаг 5: Отображение роли в системе

Давайте дополнять `ManageRoles.aspx` страницу, чтобы включить список текущих ролей в системе. Для этого добавьте элемент управления GridView на страницу и задать его `ID` свойства `RoleList`. Добавьте метод с именем класса с выделенным кодом страницы `DisplayRolesInGrid` используя следующий код:

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample8.vb)]

`Roles` Класса `GetAllRoles` метод возвращает все роли в системе как массив строк. Этот массив строк, затем привязывается к GridView. Чтобы привязать к GridView список ролей, при первой загрузке страницы, необходимо вызвать `DisplayRolesInGrid` метода на странице `Page_Load` обработчика событий. Следующий код вызывает этот метод при первом посещении страницы, но не при последующих обратных передачах.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample9.vb)]

Этот код в месте перейдите на страницу с помощью браузера. Как показано на рисунке 5, вы увидите сетку с одним столбцом с меткой элемента. Сетка включает строку для роли "Администраторы", мы добавили в шаге 4.


[![GridView отображает роли в одном столбце](creating-and-managing-roles-vb/_static/image14.png)](creating-and-managing-roles-vb/_static/image13.png)

**Рис. 5**: GridView отображает роли в одном столбце ([Просмотр полноразмерное изображение](creating-and-managing-roles-vb/_static/image15.png))


GridView отображает одиночному столбец с меткой элемента, так как GridView `AutoGenerateColumns` свойство имеет значение True (по умолчанию), что приведет к тому GridView, чтобы автоматически создавать столбец для каждого свойства в его `DataSource`. Массив имеет одно свойство, представляющее элементов в массиве, поэтому один столбец в GridView.

При отображении данных с помощью элемента управления GridView, я хочу явно определить мой столбцы, а не их неявно созданные GridView. Явно определив столбцы, гораздо проще для форматирования данных, изменять порядок столбцов и выполнять другие стандартные задачи. Таким образом давайте обновить декларативная разметка GridView ее столбцы определяются явно.

Начать с настройки в GridView `AutoGenerateColumns` свойству значение False. Затем добавьте TemplateField в сетку, задайте его `HeaderText` свойство ролям и настройте его `ItemTemplate` , чтобы он отображал содержимое массива. Чтобы сделать это, добавьте метки веб-элемент управления с именем `RoleNameLabel` для `ItemTemplate` и привязать его `Text` свойства`Container.DataItem.`

Эти свойства и `ItemTemplate`его содержимое можно задать декларативно или с помощью элемента GridView поля-диалоговое окно и редактирование шаблонов интерфейса. Для достижения поля диалоговое окно, щелкните ссылку Изменить столбцы в смарт-теге элемента GridView. Далее, снимите флажок автоматического создания полей для задания `AutoGenerateColumns` свойству значение False и добавьте TemplateField GridView, установив его `HeaderText` свойство к роли. Для определения `ItemTemplate`в смарт-теге элемента GridView содержимое, выберите параметр редактирование шаблонов. Перетащите элемент управления Label Web `ItemTemplate`, задайте его `ID` свойства `RoleNameLabel`и настроить его параметры привязки данных, чтобы его `Text` привязано свойство `Container.DataItem`.

Независимо от того, какой подход используется GridView полученный должна выглядеть следующим образом после завершения.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample10.aspx)]

> [!NOTE]
> Содержимое массива, отображаются с использованием синтаксиса привязки данных `<%# Container.DataItem %>`. Полное описание того, почему этот синтаксис используется при привязать к GridView, отображающая ее содержимое массива выходит за рамки данного руководства. Дополнительные сведения по данному вопросу посвящены [привязка к веб-элементе управления данных массива скаляр](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx).


В настоящее время `RoleList` GridView привязаны к списку роли только при первом посещении страницы. Нам нужно обновить сетку, каждый раз при добавлении новой роли. Для этого обновления `CreateRoleButton` кнопки `Click` обработчик событий, чтобы он вызывает `DisplayRolesInGrid` метод, если создается новая роль.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample11.vb)]

Теперь в том случае, когда пользователь добавляет новую роль `RoleList` GridView показывает только что добавлена роль при обратной передаче, предоставляя визуальную обратную связь, что роль создана успешно. Чтобы проиллюстрировать это, посетите `ManageRoles.aspx` и добавьте роль с именем руководителями через браузер. После нажатия кнопки Создать роль, произойдет обратная передача и обновлении таблицы будут включать администраторов, а также новая роль, руководителей.


[![Роль руководителями имеет были добавлены](creating-and-managing-roles-vb/_static/image17.png)](creating-and-managing-roles-vb/_static/image16.png)

**Рис. 6**: менеджер роль имеет были добавлены ([Просмотр полноразмерное изображение](creating-and-managing-roles-vb/_static/image18.png))


## <a name="step-6-deleting-roles"></a>Шаг 6: Удаление ролей

На этом этапе пользователь может создать новую роль и просмотрите все существующие роли из `ManageRoles.aspx` страницы. Давайте позволяет также удалять роли. `Roles.DeleteRole` Метод имеет две перегрузки:

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/en-us/library/ek4sywc0.aspx)— Удаляет роль *roleName*. Если роль содержит один или несколько членов исключение.
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/en-us/library/38h6wf59.aspx)— Удаляет роль *roleName*. Если *throwOnPopulateRole* — `True`, возникает исключение, если роль содержит один или несколько членов. Если *throwOnPopulateRole* — `False`, то роль удалена, является ли она содержит элементы, или нет. На внутреннем уровне `DeleteRole(roleName)` вызовы метода `DeleteRole(roleName, True)`.

`DeleteRole` Метод также вызывает исключение, если *roleName* — `Nothing` или является пустой строкой или если *roleName* содержит запятую. Если *roleName* не существует в системе, `DeleteRole` завершает работу, не вызывая исключение.

Давайте дополнять GridView в `ManageRoles.aspx` включать инструкции Delete кнопка, при нажатии удаляет выбранную роль. Начните с добавления кнопку «Удалить» к GridView, перейдите в диалоговое окно поля и добавив кнопку «Удалить», расположенную в CommandField параметр. Сделать удалить кнопку крайний левый столбец и задайте его `DeleteText` свойство для удаления роли.


[![Добавьте кнопку «Удалить» к GridView RoleList](creating-and-managing-roles-vb/_static/image20.png)](creating-and-managing-roles-vb/_static/image19.png)

**Рис. 7**: добавить кнопку Удалить `RoleList` GridView ([Просмотр полноразмерное изображение](creating-and-managing-roles-vb/_static/image21.png))


После добавления «удалить», элемента GridView должна выглядеть следующим образом:

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample12.aspx)]

Создайте обработчик событий для элемента GridView `RowDeleting` событий. Это событие, возникающее при обратной передаче, при нажатии кнопки Удалить роль. Добавьте в обработчик событий приведенный ниже код.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample13.vb)]

Код начинается с программного обращения к `RoleNameLabel` веб-элемента управления в строке, удалить роль была нажата. `Roles.DeleteRole` Затем вызывается метод, передавая `Text` из `RoleNameLabel` и `False`, тем самым при удалении роли независимо от того, следует ли есть пользователи, связанные с ролью. Наконец `RoleList` GridView обновляется, чтобы просто удалить роль больше не отображается в сетке.

> [!NOTE]
> Кнопка удаления роли не требует каких-либо подтверждения от пользователя перед удалением роли. Одним из самых простых способов подтверждение действия является через диалоговое окно подтверждения на стороне клиента. Дополнительные сведения об этом приеме см. в разделе [Добавление подтверждения клиентских при удалении](https://asp.net/learn/data-access/tutorial-42-vb.aspx).


## <a name="summary"></a>Сводка

Многие веб-приложения имеют определенные правила авторизации или страницам функциональность, доступная только для определенных классов пользователей. Например может быть набор веб-страниц, которые будут доступны только администраторам. Вместо того чтобы определять эти правила авторизации на основе пользователя по, зачастую полезно более для определения правил на основе роли. То есть вместо того, чтобы явно разрешить пользователям Скотт и Цзисунь для доступа к веб-страниц администрирования, более простого в сопровождении подход заключается в позволяет членам роли "Администраторы" для доступа к этим страницам, а затем для обозначения Скотт и Цзисунь как пользователи, принадлежащие Роли администраторов.

Платформа роли упрощает создание и управление ролями. В этом учебнике мы рассмотрели Настройка framework роли для использования `SqlRoleProvider`, где используется базы данных Microsoft SQL Server в качестве хранилища ролей. Мы также создали веб-страницы, перечислены роли, существующие в системе и позволяет использовать новые роли должен быть создан и существующие для удаления. В последующих руководства вы узнаете, как назначать пользователей ролям и как применять проверку подлинности на основе ролей.

Программирование довольны!

### <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения по темам, рассматриваемые в этом учебнике см. в следующих ресурсах:

- [Изучение ASP.NET 2.0 членства, ролей и профиля](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Практическое руководство: Использование диспетчера ролей в ASP.NET 2.0](https://msdn.microsoft.com/en-us/library/ms998314.aspx)
- [Поставщики ролей](https://msdn.microsoft.com/en-us/library/aa478950.aspx)
- [Последовательное собственные средства администрирования веб-сайта](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [Техническая документация для `<roleManager>` элемента](https://msdn.microsoft.com/en-us/library/ms164660.aspx)
- [С помощью членства и ролей API диспетчера](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>Об авторе

Скотт Митчелл, автор нескольких ASP/ASP.NET и основатель 4GuysFromRolla.com, работает с веб-технологиями Майкрософт с 1998 года. Скотт — независимый консультант, trainer и записи. Его последняя книга —  *[диспетчерами учат самостоятельно ASP.NET 2.0 в течение 24 часов](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Скотт может быть достигнута по [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) или через его блог по [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Благодарности

Этот учебник ряд прошел проверку многие полезные рецензентов. Основными редакторами этого учебника включают Alicja Maziarz, Suchi Банерджи и Мерфи Тереза д. Объясняются моих последующих статей для MSDN? Если Да, напишите мне по[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[Назад](role-based-authorization-cs.md)
[Вперед](assigning-roles-to-users-vb.md)