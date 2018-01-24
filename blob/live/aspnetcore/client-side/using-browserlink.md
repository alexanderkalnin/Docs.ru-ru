---
title: "Связь с браузером в ASP.NET Core"
author: ncarandini
description: "Объясняет, как связь с браузером является функцией Visual Studio, которая связывает среду разработки с одного или нескольких веб-браузеров."
ms.author: riande
manager: wpickett
ms.date: 09/22/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: client-side/using-browserlink
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d5db65c268923e96c45b034639437fc3496ccac1
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="browser-link-in-aspnet-core"></a><span data-ttu-id="76e9d-103">Связь с браузером в ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="76e9d-103">Browser Link in ASP.NET Core</span></span> 

<span data-ttu-id="76e9d-104">По [Nicolò Carandini](https://github.com/ncarandini), [Mike Wasson](https://github.com/MikeWasson), и [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="76e9d-104">By [Nicolò Carandini](https://github.com/ncarandini), [Mike Wasson](https://github.com/MikeWasson), and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="76e9d-105">Связь с браузером — это функция в Visual Studio, который создает канал связи между средой разработки и один или несколько веб-браузеры.</span><span class="sxs-lookup"><span data-stu-id="76e9d-105">Browser Link is a feature in Visual Studio that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="76e9d-106">Можно использовать связь с браузером для обновления веб-приложения в нескольких браузерах одновременно, это полезно для тестирования в различных браузерах.</span><span class="sxs-lookup"><span data-stu-id="76e9d-106">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

## <a name="browser-link-setup"></a><span data-ttu-id="76e9d-107">Установка связи обозревателя</span><span class="sxs-lookup"><span data-stu-id="76e9d-107">Browser Link setup</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="76e9d-108">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="76e9d-108">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="76e9d-109">ASP.NET Core 2.x **веб-приложение**, **пустой**, и **веб-API** шаблона проекты, использующие [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) мета пакет, который содержит ссылку на пакет для [Microsoft.VisualStudio.Web.BrowserLink](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.BrowserLink/).</span><span class="sxs-lookup"><span data-stu-id="76e9d-109">The ASP.NET Core 2.x **Web Application**, **Empty**, and **Web API** template projects use the [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) meta-package, which contains a package reference for [Microsoft.VisualStudio.Web.BrowserLink](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.BrowserLink/).</span></span> <span data-ttu-id="76e9d-110">Таким образом, использование `Microsoft.AspNetCore.All` метапакет требует никаких дополнительных действий, чтобы сделать доступными для использования связь с браузером.</span><span class="sxs-lookup"><span data-stu-id="76e9d-110">Therefore, using the `Microsoft.AspNetCore.All` meta-package requires no further action to make Browser Link available for use.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="76e9d-111">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="76e9d-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="76e9d-112">ASP.NET Core 1.x **веб-приложение** шаблон проекта содержит ссылку на пакет для [Microsoft.VisualStudio.Web.BrowserLink](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.BrowserLink/) пакета.</span><span class="sxs-lookup"><span data-stu-id="76e9d-112">The ASP.NET Core 1.x **Web Application** project template has a package reference for the [Microsoft.VisualStudio.Web.BrowserLink](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.BrowserLink/) package.</span></span> <span data-ttu-id="76e9d-113">**Пустой** или **веб-API** шаблона проектов необходимо добавить ссылку на пакет `Microsoft.VisualStudio.Web.BrowserLink`.</span><span class="sxs-lookup"><span data-stu-id="76e9d-113">The **Empty** or **Web API** template projects require you to add a package reference to `Microsoft.VisualStudio.Web.BrowserLink`.</span></span>

<span data-ttu-id="76e9d-114">Так как это функция Visual Studio, самым простым способом для добавления пакета **пустой** или **веб-API** шаблона проекта является открытие **консоль диспетчера пакетов** (**Представление** > **другие окна** > **консоль диспетчера пакетов**) и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="76e9d-114">Since this is a Visual Studio feature, the easiest way to add the package to an **Empty** or **Web API** template project is to open the **Package Manager Console** (**View** > **Other Windows** > **Package Manager Console**) and run the following command:</span></span>

```console
install-package Microsoft.VisualStudio.Web.BrowserLink
```

<span data-ttu-id="76e9d-115">Кроме того, можно использовать **диспетчера пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="76e9d-115">Alternatively, you can use **NuGet Package Manager**.</span></span> <span data-ttu-id="76e9d-116">Щелкните правой кнопкой мыши имя проекта в **обозревателе решений** и выберите **управление пакетами NuGet**:</span><span class="sxs-lookup"><span data-stu-id="76e9d-116">Right-click the project name in **Solution Explorer** and choose **Manage NuGet Packages**:</span></span>

![Диспетчер пакетов Open NuGet](using-browserlink/_static/open-nuget-package-manager.png)

<span data-ttu-id="76e9d-118">Найти и установить пакет:</span><span class="sxs-lookup"><span data-stu-id="76e9d-118">Find and install the package:</span></span>

![Добавление пакета с помощью диспетчера пакетов NuGet](using-browserlink/_static/add-package-with-nuget-package-manager.png)

---

### <a name="configuration"></a><span data-ttu-id="76e9d-120">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="76e9d-120">Configuration</span></span>

<span data-ttu-id="76e9d-121">В `Configure` метод *файла Startup.cs* файла:</span><span class="sxs-lookup"><span data-stu-id="76e9d-121">In the `Configure` method of the *Startup.cs* file:</span></span>

```csharp
app.UseBrowserLink();
```

<span data-ttu-id="76e9d-122">Обычно код находится внутри `if` блок, позволяющий только связь с браузером в среде разработки, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="76e9d-122">Usually the code is inside an `if` block that only enables Browser Link in the Development environment, as shown here:</span></span>

```csharp
if (env.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
    app.UseBrowserLink();
}
```

<span data-ttu-id="76e9d-123">Дополнительные сведения см. в статье [Работа с несколькими средами](xref:fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="76e9d-123">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

## <a name="how-to-use-browser-link"></a><span data-ttu-id="76e9d-124">Как использовать связь с браузером</span><span class="sxs-lookup"><span data-stu-id="76e9d-124">How to use Browser Link</span></span>

<span data-ttu-id="76e9d-125">При наличии в открытом проекте ASP.NET Core, Visual Studio отображает панели инструментов обозревателя ссылку рядом с **целевой объект отладки** управления панели инструментов:</span><span class="sxs-lookup"><span data-stu-id="76e9d-125">When you have an ASP.NET Core project open, Visual Studio shows the Browser Link toolbar control next to the **Debug Target** toolbar control:</span></span>

![Раскрывающееся меню обозревателя ссылки](using-browserlink/_static/browserLink-dropdown-menu.png)

<span data-ttu-id="76e9d-127">На панели инструментов связь с браузером можно:</span><span class="sxs-lookup"><span data-stu-id="76e9d-127">From the Browser Link toolbar control, you can:</span></span>

* <span data-ttu-id="76e9d-128">Обновите веб-приложения в нескольких браузерах за один раз.</span><span class="sxs-lookup"><span data-stu-id="76e9d-128">Refresh the web application in several browsers at once.</span></span>
* <span data-ttu-id="76e9d-129">Откройте **мониторинга связи с браузером**.</span><span class="sxs-lookup"><span data-stu-id="76e9d-129">Open the **Browser Link Dashboard**.</span></span>
* <span data-ttu-id="76e9d-130">Включить или отключить **связь с браузером**.</span><span class="sxs-lookup"><span data-stu-id="76e9d-130">Enable or disable **Browser Link**.</span></span> <span data-ttu-id="76e9d-131">Примечание: По умолчанию в Visual Studio 2017 г. (15,3) отключена связь с браузером.</span><span class="sxs-lookup"><span data-stu-id="76e9d-131">Note: Browser Link is disabled by default in Visual Studio 2017 (15.3).</span></span>
* <span data-ttu-id="76e9d-132">Включить или отключить [Автосинхронизации CSS](#enable-or-disable-css-auto-sync).</span><span class="sxs-lookup"><span data-stu-id="76e9d-132">Enable or disable [CSS Auto-Sync](#enable-or-disable-css-auto-sync).</span></span>

> [!NOTE]
> <span data-ttu-id="76e9d-133">Некоторые Visual Studio подключаемые модули, прежде всего *2015 пакет расширения Web* и *2017 г. пакет расширения веб*, предоставляют расширенные функциональные возможности для связи с браузером, но некоторые дополнительные функции не работают с ASP. Проекты NET Core.</span><span class="sxs-lookup"><span data-stu-id="76e9d-133">Some Visual Studio plug-ins, most notably *Web Extension Pack 2015* and *Web Extension Pack 2017*, offer extended functionality for Browser Link, but some of the additional features don't work with ASP.NET Core projects.</span></span>

## <a name="refresh-the-web-application-in-several-browsers-at-once"></a><span data-ttu-id="76e9d-134">Обновить веб-приложения в нескольких браузерах за один раз</span><span class="sxs-lookup"><span data-stu-id="76e9d-134">Refresh the web application in several browsers at once</span></span>

<span data-ttu-id="76e9d-135">Чтобы выбрать один веб-браузер для запуска при запуске проекта, используйте раскрывающееся меню в **целевой объект отладки** управления панели инструментов:</span><span class="sxs-lookup"><span data-stu-id="76e9d-135">To choose a single web browser to launch when starting the project, use the drop-down menu in the **Debug Target** toolbar control:</span></span>

![Раскрывающееся меню F5](using-browserlink/_static/debug-target-dropdown-menu.png)

<span data-ttu-id="76e9d-137">Чтобы одновременно открыть несколько браузеров, выберите **просмотреть с помощью...**  же раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="76e9d-137">To open multiple browsers at once, choose **Browse with...** from the same drop-down.</span></span> <span data-ttu-id="76e9d-138">Удерживая нажатой клавишу CTRL при выборе в браузерах, требуется и нажмите кнопку **Обзор**:</span><span class="sxs-lookup"><span data-stu-id="76e9d-138">Hold down the CTRL key to select the browsers you want, and then click **Browse**:</span></span>

![Одновременное открытие большинство браузеров](using-browserlink/_static/open-many-browsers-at-once.png)

<span data-ttu-id="76e9d-140">Ниже приведен на снимке экрана показан откройте Visual Studio с помощью индекса представления и два открытые окна браузера.</span><span class="sxs-lookup"><span data-stu-id="76e9d-140">Here's a screenshot showing Visual Studio with the Index view open and two open browsers:</span></span>

![Синхронизация с пример двух браузеров](using-browserlink/_static/sync-with-two-browsers-example.png)

<span data-ttu-id="76e9d-142">Наведите указатель мыши на панели инструментов связь с браузером для просмотра в браузерах, подключенных к проекту:</span><span class="sxs-lookup"><span data-stu-id="76e9d-142">Hover over the Browser Link toolbar control to see the browsers that are connected to the project:</span></span>

![Подсказки при наведении курсора мыши](using-browserlink/_static/hoover-tip.png)

<span data-ttu-id="76e9d-144">Изменить представление индекса и всех подключенных браузерах обновляются при нажатии кнопки "Обновить" в связи с браузером:</span><span class="sxs-lookup"><span data-stu-id="76e9d-144">Change the Index view, and all connected browsers are updated when you click the Browser Link refresh button:</span></span>

![браузеры синхронизации для изменения](using-browserlink/_static/browsers-sync-to-changes.png)

<span data-ttu-id="76e9d-146">Связь с браузером также работает с браузерами, запустите из вне Visual Studio и перейдите к URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="76e9d-146">Browser Link also works with browsers that you launch from outside Visual Studio and navigate to the application URL.</span></span>

### <a name="the-browser-link-dashboard"></a><span data-ttu-id="76e9d-147">Панели мониторинга связи с браузером</span><span class="sxs-lookup"><span data-stu-id="76e9d-147">The Browser Link Dashboard</span></span>

<span data-ttu-id="76e9d-148">В раскрывающемся меню для управления подключением с браузерами открыть связь с браузером, откройте мониторинга связи с браузером:</span><span class="sxs-lookup"><span data-stu-id="76e9d-148">Open the Browser Link Dashboard from the Browser Link drop down menu to manage the connection with open browsers:</span></span>

![Откройте browserslink панели мониторинга.](using-browserlink/_static/open-browserlink-dashboard.png)

<span data-ttu-id="76e9d-150">Если браузер не подключен, можно запустить сеанс режима отладки, выбрав *Просмотр в браузере* ссылку:</span><span class="sxs-lookup"><span data-stu-id="76e9d-150">If no browser is connected, you can start a non-debugging session by selecting the *View in Browser* link:</span></span>

![browserlink-панели мониторинга нет подключений](using-browserlink/_static/browserlink-dashboard-no-connections.png)

<span data-ttu-id="76e9d-152">В противном случае — путь к странице, показывающая всеми браузерами, показаны подключенных браузеры:</span><span class="sxs-lookup"><span data-stu-id="76e9d-152">Otherwise, the connected browsers are shown with the path to the page that each browser is showing:</span></span>

![browserlink панель мониторинга — два подключения](using-browserlink/_static/browserlink-dashboard-two-connections.png)

<span data-ttu-id="76e9d-154">При желании можно щелкнуть имя перечисленных браузера, чтобы обновить этот одного браузера.</span><span class="sxs-lookup"><span data-stu-id="76e9d-154">If you like, you can click on a listed browser name to refresh that single browser.</span></span>

### <a name="enable-or-disable-browser-link"></a><span data-ttu-id="76e9d-155">Включить или отключить связь с браузером</span><span class="sxs-lookup"><span data-stu-id="76e9d-155">Enable or disable Browser Link</span></span>

<span data-ttu-id="76e9d-156">При повторном включении связь с браузером после ее отключения, браузеры для повторного подключения, их необходимо обновить.</span><span class="sxs-lookup"><span data-stu-id="76e9d-156">When you re-enable Browser Link after disabling it, you must refresh the browsers to reconnect them.</span></span>

### <a name="enable-or-disable-css-auto-sync"></a><span data-ttu-id="76e9d-157">Включение и отключение автоматической синхронизации CSS</span><span class="sxs-lookup"><span data-stu-id="76e9d-157">Enable or disable CSS Auto-Sync</span></span>

<span data-ttu-id="76e9d-158">При включенной автоматической синхронизации CSS подключенных браузеров будут автоматически обновляться при внесении изменений в CSS-файлах.</span><span class="sxs-lookup"><span data-stu-id="76e9d-158">When CSS Auto-Sync is enabled, connected browsers are automatically refreshed when you make any change to CSS files.</span></span>

## <a name="how-does-it-work"></a><span data-ttu-id="76e9d-159">Как это работает?</span><span class="sxs-lookup"><span data-stu-id="76e9d-159">How does it work?</span></span>

<span data-ttu-id="76e9d-160">Связь с браузером SignalR использует для создания канала связи между Visual Studio и браузером.</span><span class="sxs-lookup"><span data-stu-id="76e9d-160">Browser Link uses SignalR to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="76e9d-161">Если включена связь с браузером, Visual Studio действует как сервер SignalR, подключенные к нескольким клиентам (браузерах).</span><span class="sxs-lookup"><span data-stu-id="76e9d-161">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="76e9d-162">Связь с браузером также регистрирует компонент по промежуточного слоя в конвейере ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="76e9d-162">Browser Link also registers a middleware component in the ASP.NET request pipeline.</span></span> <span data-ttu-id="76e9d-163">Этот компонент вводит специальные `<script>` references в каждом запросе страницы с сервера.</span><span class="sxs-lookup"><span data-stu-id="76e9d-163">This component injects special `<script>` references into every page request from the server.</span></span> <span data-ttu-id="76e9d-164">При выборе можно просмотреть ссылки на скрипты **Просмотр исходного кода** в браузере и прокрутки к концу `<body>` разметки содержимого:</span><span class="sxs-lookup"><span data-stu-id="76e9d-164">You can see the script references by selecting **View source** in the browser and scrolling to the end of the `<body>` tag content:</span></span>

```javascript
    <!-- Visual Studio Browser Link -->
    <script type="application/json" id="__browserLink_initializationData">
        {"requestId":"a717d5a07c1741949a7cefd6fa2bad08","requestMappingFromServer":false}
    </script>
    <script type="text/javascript" src="http://localhost:54139/b6e36e429d034f578ebccd6a79bf19bf/browserLink" async="async"></script>
    <!-- End Browser Link -->
</body>
```

<span data-ttu-id="76e9d-165">Исходные файлы не изменены.</span><span class="sxs-lookup"><span data-stu-id="76e9d-165">Your source files aren't modified.</span></span> <span data-ttu-id="76e9d-166">Компонент по промежуточного слоя динамически вставляет ссылки на скрипты.</span><span class="sxs-lookup"><span data-stu-id="76e9d-166">The middleware component injects the script references dynamically.</span></span> 

<span data-ttu-id="76e9d-167">Поскольку код браузером все JavaScript, он работает во всех браузерах, поддерживаемых SignalR без необходимости подключаемый модуль обозревателя.</span><span class="sxs-lookup"><span data-stu-id="76e9d-167">Because the browser-side code is all JavaScript, it works on all browsers that SignalR supports without requiring a browser plug-in.</span></span>