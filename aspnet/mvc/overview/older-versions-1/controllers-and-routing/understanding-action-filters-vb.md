---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: "Основные сведения о фильтрах действий (VB) | Документы Microsoft"
author: microsoft
description: "Целью данного учебника является объяснить фильтров действий. Фильтр действий является атрибутом, который можно применить к действия контроллера--или контроллер всего..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 483133ec5db27c2fa1ed4b463e37e17efab12e0f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="understanding-action-filters-vb"></a><span data-ttu-id="280c0-104">Основные сведения о фильтрах действий (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="280c0-104">Understanding Action Filters (VB)</span></span>
====================
<span data-ttu-id="280c0-105">по [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="280c0-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="280c0-106">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="280c0-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> <span data-ttu-id="280c0-107">Целью данного учебника является объяснить фильтров действий.</span><span class="sxs-lookup"><span data-stu-id="280c0-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="280c0-108">Фильтр действий является атрибутом, который можно применять действия контроллера--или всей контроллеру--, изменяет способ, в котором выполняется действие.</span><span class="sxs-lookup"><span data-stu-id="280c0-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>


## <a name="understanding-action-filters"></a><span data-ttu-id="280c0-109">Основные сведения о фильтрах действий</span><span class="sxs-lookup"><span data-stu-id="280c0-109">Understanding Action Filters</span></span>

<span data-ttu-id="280c0-110">Целью данного учебника является объяснить фильтров действий.</span><span class="sxs-lookup"><span data-stu-id="280c0-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="280c0-111">Фильтр действий является атрибутом, который можно применять действия контроллера--или всей контроллеру--, изменяет способ, в котором выполняется действие.</span><span class="sxs-lookup"><span data-stu-id="280c0-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="280c0-112">Платформа ASP.NET MVC включает несколько фильтров действий:</span><span class="sxs-lookup"><span data-stu-id="280c0-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="280c0-113">OutputCache — это фильтр действий кэширует выходные данные действия контроллера для заданного количества времени.</span><span class="sxs-lookup"><span data-stu-id="280c0-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="280c0-114">HandleError — это действие фильтр обрабатывает ошибки, возникшие при выполнении действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="280c0-115">Авторизация — это фильтр действий позволяет ограничить доступ к определенному пользователю или роли.</span><span class="sxs-lookup"><span data-stu-id="280c0-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="280c0-116">Можно также создавать свои собственные настраиваемых фильтров действий.</span><span class="sxs-lookup"><span data-stu-id="280c0-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="280c0-117">Например может потребоваться создание пользовательского фильтра действий, чтобы реализовать пользовательскую систему аутентификации.</span><span class="sxs-lookup"><span data-stu-id="280c0-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="280c0-118">Или может потребоваться создание фильтра действий, изменяющих представление данных, возвращаемых функцией действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="280c0-119">В этом учебнике вы узнаете, как для построения фильтра действий с нуля.</span><span class="sxs-lookup"><span data-stu-id="280c0-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="280c0-120">Мы Создание фильтра действий журнала, который записывает различные этапы обработки действия в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="280c0-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="280c0-121">С помощью фильтра действий</span><span class="sxs-lookup"><span data-stu-id="280c0-121">Using an Action Filter</span></span>

<span data-ttu-id="280c0-122">Фильтр действий является атрибутом.</span><span class="sxs-lookup"><span data-stu-id="280c0-122">An action filter is an attribute.</span></span> <span data-ttu-id="280c0-123">Большинство фильтров действий можно применить действие отдельного контроллера или всей контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="280c0-124">Например, контроллер данных в список 1 предоставляет действие с именем `Index()` , возвращает текущее время.</span><span class="sxs-lookup"><span data-stu-id="280c0-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="280c0-125">Это действие снабжен `OutputCache` фильтра действий.</span><span class="sxs-lookup"><span data-stu-id="280c0-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="280c0-126">Этот фильтр в результате значение, возвращаемое действие на кэширование в течение 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="280c0-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="280c0-127">**Листинг 1.`Controllers\DataController.vb`**</span><span class="sxs-lookup"><span data-stu-id="280c0-127">**Listing 1 – `Controllers\DataController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

<span data-ttu-id="280c0-128">Если несколько раз вызвать `Index()` действие, введя URL-адрес или данных или индекса в адресную строку браузера и попадание обновления кнопку несколько раз, то же время вы увидите на 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="280c0-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="280c0-129">Выходные данные `Index()` действие кэшируется на 10 секунд (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="280c0-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>


<span data-ttu-id="280c0-130">[![Время кэширования](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="280c0-130">[![Cached time](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span></span>

<span data-ttu-id="280c0-131">**На рисунке 01**: время ([Просмотр полноразмерное изображение](understanding-action-filters-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="280c0-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-vb/_static/image3.png))</span></span>


<span data-ttu-id="280c0-132">В список 1 фильтр одно действие — `OutputCache` фильтр действий — применяется к `Index()` метод.</span><span class="sxs-lookup"><span data-stu-id="280c0-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="280c0-133">Если требуется, можно применить несколько фильтров действий для одного действия.</span><span class="sxs-lookup"><span data-stu-id="280c0-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="280c0-134">Например, может потребоваться применить оба `OutputCache` и `HandleError` фильтры действий для одного действия.</span><span class="sxs-lookup"><span data-stu-id="280c0-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="280c0-135">В список 1 `OutputCache` фильтр действий применяется к `Index()` действие.</span><span class="sxs-lookup"><span data-stu-id="280c0-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="280c0-136">Можно также применить этот атрибут к `DataController` сам класс.</span><span class="sxs-lookup"><span data-stu-id="280c0-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="280c0-137">В этом случае результат, возвращаемый какие-либо действия, предоставляемые контроллером будет кэшироваться на 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="280c0-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="280c0-138">Различные типы фильтров</span><span class="sxs-lookup"><span data-stu-id="280c0-138">The Different Types of Filters</span></span>

<span data-ttu-id="280c0-139">Платформа ASP.NET MVC поддерживает четыре типа фильтров:</span><span class="sxs-lookup"><span data-stu-id="280c0-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="280c0-140">Фильтры авторизации — реализует `IAuthorizationFilter` атрибута.</span><span class="sxs-lookup"><span data-stu-id="280c0-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="280c0-141">Фильтры действий — реализует `IActionFilter` атрибута.</span><span class="sxs-lookup"><span data-stu-id="280c0-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="280c0-142">Фильтры — реализует привести `IResultFilter` атрибута.</span><span class="sxs-lookup"><span data-stu-id="280c0-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="280c0-143">Фильтры исключений — реализует `IExceptionFilter` атрибута.</span><span class="sxs-lookup"><span data-stu-id="280c0-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="280c0-144">Фильтры выполняются в указанном выше порядке.</span><span class="sxs-lookup"><span data-stu-id="280c0-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="280c0-145">Например фильтры авторизации всегда выполняются перед фильтрами действий и фильтры исключений, всегда выполняются после каждого типа фильтра.</span><span class="sxs-lookup"><span data-stu-id="280c0-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="280c0-146">Фильтры авторизации используются для реализации проверки подлинности и авторизации для действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="280c0-147">Например фильтр Authorize является примером фильтра авторизации.</span><span class="sxs-lookup"><span data-stu-id="280c0-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="280c0-148">Фильтры действий содержат логику, которая выполняется до и после выполнения действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="280c0-149">Фильтр действий можно использовать для экземпляра, для изменения представления данных, возвращающий действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="280c0-150">Фильтры результатов содержат логику, которая выполняется до и после выполнения результата представления.</span><span class="sxs-lookup"><span data-stu-id="280c0-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="280c0-151">Например, может возникнуть необходимость изменить результат представления правой перед визуализации представления в браузере.</span><span class="sxs-lookup"><span data-stu-id="280c0-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="280c0-152">Фильтры исключений — это последний тип фильтра для выполнения.</span><span class="sxs-lookup"><span data-stu-id="280c0-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="280c0-153">Фильтр исключений можно использовать для обработки ошибок, вызванных результаты действий контроллера или действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="280c0-154">Также можно использовать фильтры исключений ошибок в журнал.</span><span class="sxs-lookup"><span data-stu-id="280c0-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="280c0-155">У каждого типа фильтра выполняется в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="280c0-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="280c0-156">Если вы хотите управлять порядком, в котором выполняются фильтры того же типа можно задать свойство порядок фильтра.</span><span class="sxs-lookup"><span data-stu-id="280c0-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="280c0-157">Базовый класс для всех фильтров действий — `System.Web.Mvc.FilterAttribute` класса.</span><span class="sxs-lookup"><span data-stu-id="280c0-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="280c0-158">Если необходимо реализовать определенный тип фильтра, то необходимо создать класс, наследующий от базового класса фильтра и реализует один или несколько IAuthorizationFilter, IActionFilter, IResultFilter или ExceptionFilter интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="280c0-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the IAuthorizationFilter, IActionFilter, IResultFilter, or ExceptionFilter interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="280c0-159">Базовый класс ActionFilterAttribute</span><span class="sxs-lookup"><span data-stu-id="280c0-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="280c0-160">Для упрощения реализации пользовательского фильтра действий, платформа ASP.NET MVC включает базовый `ActionFilterAttribute` класса.</span><span class="sxs-lookup"><span data-stu-id="280c0-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="280c0-161">Этот класс реализует интерфейс `IActionFilter` и `IResultFilter` интерфейсы и наследует от `Filter` класса.</span><span class="sxs-lookup"><span data-stu-id="280c0-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="280c0-162">Терминология здесь не полностью согласованной.</span><span class="sxs-lookup"><span data-stu-id="280c0-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="280c0-163">С технической точки зрения класс, наследующий от класса ActionFilterAttribute — фильтра действий и фильтра результатов.</span><span class="sxs-lookup"><span data-stu-id="280c0-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="280c0-164">Тем не менее в том смысле, сохранения, фильтр действий word позволяет ссылаться на любой тип фильтра в платформе ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="280c0-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="280c0-165">Базовый класс ActionFilterAttribute имеет следующие методы, которые можно переопределить.</span><span class="sxs-lookup"><span data-stu-id="280c0-165">The base ActionFilterAttribute class has the following methods that you can override:</span></span>

- <span data-ttu-id="280c0-166">OnActionExecuting — этот метод вызывается перед выполнением действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="280c0-167">OnActionExecuted — этот метод вызывается после выполнения действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="280c0-168">OnResultExecuting — этот метод вызывается до выполнения результата действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="280c0-169">OnResultExecuted — этот метод вызывается после выполнения результата действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="280c0-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="280c0-170">В следующем разделе мы рассмотрим, как можно реализовать каждый из этих различных методов.</span><span class="sxs-lookup"><span data-stu-id="280c0-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="280c0-171">Создание фильтра журнала действий</span><span class="sxs-lookup"><span data-stu-id="280c0-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="280c0-172">Чтобы продемонстрировать, как создать настраиваемого фильтра действий, мы создадим пользовательского фильтра действий, записывает в журнал этапы обработки действия контроллера, в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="280c0-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="280c0-173">Наш `LogActionFilter` содержится в списке 2.</span><span class="sxs-lookup"><span data-stu-id="280c0-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="280c0-174">**Листинг 2.`ActionFilters\LogActionFilter.vb`**</span><span class="sxs-lookup"><span data-stu-id="280c0-174">**Listing 2 – `ActionFilters\LogActionFilter.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

<span data-ttu-id="280c0-175">В списке 2 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, и `OnResultExecuted()` все методы вызова `Log()` метод.</span><span class="sxs-lookup"><span data-stu-id="280c0-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="280c0-176">Имя метода и текущие данные маршрута передается `Log()` метод.</span><span class="sxs-lookup"><span data-stu-id="280c0-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="280c0-177">`Log()` Метод записывает сообщение в окне вывода Visual Studio (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="280c0-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>


<span data-ttu-id="280c0-178">[![Запись в окне вывода Visual Studio](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="280c0-178">[![Writing to the Visual Studio Output window](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span></span>

<span data-ttu-id="280c0-179">**На рисунке 02**: запись в окне вывода Visual Studio ([Просмотр полноразмерное изображение](understanding-action-filters-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="280c0-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-vb/_static/image6.png))</span></span>


<span data-ttu-id="280c0-180">Контроллер Home в списке 3 показано, как применять фильтр журнала действий в класс контроллера целиком.</span><span class="sxs-lookup"><span data-stu-id="280c0-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="280c0-181">Каждый раз, когда любой из действия, представляемые контроллера Home вызываются — либо `Index()` метода или `About()` метод — этапы обработки действия регистрируются в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="280c0-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="280c0-182">**Листинг 3.`Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="280c0-182">**Listing 3 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a><span data-ttu-id="280c0-183">Сводка</span><span class="sxs-lookup"><span data-stu-id="280c0-183">Summary</span></span>

<span data-ttu-id="280c0-184">В этом учебнике вы ознакомились с ASP.NET MVC фильтров действий.</span><span class="sxs-lookup"><span data-stu-id="280c0-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="280c0-185">Вы узнали о четыре различных типа фильтров: фильтры авторизации, фильтры действий, фильтры результатов и фильтры исключений.</span><span class="sxs-lookup"><span data-stu-id="280c0-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="280c0-186">Вы также узнали о базе `ActionFilterAttribute` класса.</span><span class="sxs-lookup"><span data-stu-id="280c0-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="280c0-187">Наконец вы узнали, как реализовать простой фильтр действий.</span><span class="sxs-lookup"><span data-stu-id="280c0-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="280c0-188">Мы создали фильтр действий журнала, который записывает в журнал этапы обработки действия контроллера, в окне вывода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="280c0-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="280c0-189">[Назад](asp-net-mvc-routing-overview-vb.md)
[Вперед](improving-performance-with-output-caching-vb.md)</span><span class="sxs-lookup"><span data-stu-id="280c0-189">[Previous](asp-net-mvc-routing-overview-vb.md)
[Next](improving-performance-with-output-caching-vb.md)</span></span>