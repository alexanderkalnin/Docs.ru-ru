---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: "Корпоративного веб-развертывания: Общие сведения о сценарии | Документы Microsoft"
author: jrjlee
description: "Этот набор учебников использует образец решения с реалистичных уровень сложности, а также вымышленной корпоративный сценарий развертывания, для обеспечения ref..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/03/2012
ms.topic: article
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: f90db22bf98456661c530e728e854ce109aec6fd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="enterprise-web-deployment-scenario-overview"></a><span data-ttu-id="16b02-103">Корпоративного веб-развертывания: Общие сведения о сценарии</span><span class="sxs-lookup"><span data-stu-id="16b02-103">Enterprise Web Deployment: Scenario Overview</span></span>
====================
<span data-ttu-id="16b02-104">по [Джейсон Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="16b02-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="16b02-105">Скачать PDF</span><span class="sxs-lookup"><span data-stu-id="16b02-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="16b02-106">Этот набор учебников использует образец решения с реалистичных уровень сложности, а также вымышленной корпоративный сценарий развертывания, для реализации ссылки и определяют задачи и пошаговые руководства общий контекст.</span><span class="sxs-lookup"><span data-stu-id="16b02-106">This set of tutorials uses a sample solution with a realistic level of complexity, together with a fictional enterprise deployment scenario, to provide a reference implementation and to give the tasks and walkthroughs a common context.</span></span> <span data-ttu-id="16b02-107">В этом разделе описывается сценарий учебника и вводит образец решения.</span><span class="sxs-lookup"><span data-stu-id="16b02-107">This topic describes the tutorial scenario and introduces the sample solution.</span></span>


## <a name="scenario-description"></a><span data-ttu-id="16b02-108">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="16b02-108">Scenario Description</span></span>

<span data-ttu-id="16b02-109">Fabrikam, Inc., вымышленной компании создается решение, которое позволяет удаленные команды продаж хранения и получения контактной информации из веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="16b02-109">Fabrikam, Inc., a fictitious company, is creating a solution that lets remote sales teams store and retrieve contact information from a web interface.</span></span>

<span data-ttu-id="16b02-110">Процесс управления жизненным циклом приложений (ALM), компании Fabrikam, Inc. требуется решение должно быть развернуто на различных этапах процесса разработки программного обеспечения до трех серверных сред:</span><span class="sxs-lookup"><span data-stu-id="16b02-110">The Application Lifecycle Management (ALM) processes at Fabrikam, Inc. require the solution to be deployed to three server environments at various stages of the software development process:</span></span>

- <span data-ttu-id="16b02-111">Разработчик среде тестирования или «песочницы».</span><span class="sxs-lookup"><span data-stu-id="16b02-111">A developer test or "sandbox" environment.</span></span>
- <span data-ttu-id="16b02-112">Интранет-промежуточной среде.</span><span class="sxs-lookup"><span data-stu-id="16b02-112">An intranet-based staging environment.</span></span>
- <span data-ttu-id="16b02-113">Рабочей среде с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="16b02-113">An Internet-facing production environment.</span></span>

<span data-ttu-id="16b02-114">Каждая из этих сред имеет другой конфигурации и требований к безопасности, а каждый непростой развертывания.</span><span class="sxs-lookup"><span data-stu-id="16b02-114">Each of these environments has different configuration and security requirements, and each poses unique deployment challenges.</span></span>

### <a name="the-fabrikam-inc-server-infrastructure"></a><span data-ttu-id="16b02-115">Fabrikam, Inc. Инфраструктура сервера</span><span class="sxs-lookup"><span data-stu-id="16b02-115">The Fabrikam, Inc. Server Infrastructure</span></span>

<span data-ttu-id="16b02-116">Это высокоуровневое разработку и развертывание инфраструктуры компании Fabrikam, Inc.</span><span class="sxs-lookup"><span data-stu-id="16b02-116">This is the high-level development and deployment infrastructure at Fabrikam, Inc.</span></span>

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

<span data-ttu-id="16b02-117">Компьютеры разработчиков, инфраструктуры управления источника, разработчика тестовой среде и промежуточной среды, в которой находятся в интрасети сети в домене Fabrikam.net.</span><span class="sxs-lookup"><span data-stu-id="16b02-117">The developer workstations, the source control infrastructure, the developer test environment, and the staging environment all reside on the intranet network within the Fabrikam.net domain.</span></span> <span data-ttu-id="16b02-118">В рабочей среде находится в сети периметра (также известный как DMZ, демилитаризованная зона и промежуточной подсетью), который изолирован от этой сети с помощью брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="16b02-118">The production environment resides on a perimeter network (also known as DMZ, demilitarized zone, and screened subnet), which is isolated from the intranet network by a firewall.</span></span> <span data-ttu-id="16b02-119">Это распространенный сценарий развертывания: обычно, чтобы изолировать веб-серверов с выходом в Интернет из внутренней серверной инфраструктуры с помощью брандмауэров или серверов шлюза.</span><span class="sxs-lookup"><span data-stu-id="16b02-119">This is a common deployment scenario: you typically isolate your Internet-facing web servers from your internal server infrastructure through the use of firewalls or gateway servers.</span></span>

<span data-ttu-id="16b02-120">В этом примере:</span><span class="sxs-lookup"><span data-stu-id="16b02-120">In this example:</span></span>

- <span data-ttu-id="16b02-121">Сервер с сервера отдельные сборки Team Foundation Server (TFS) 2010 предоставляет системы управления версиями и функциональные возможности непрерывной интеграции (CI).</span><span class="sxs-lookup"><span data-stu-id="16b02-121">A Team Foundation Server (TFS) 2010 server with a separate build server provides source control and continuous integration (CI) functionality.</span></span>
- <span data-ttu-id="16b02-122">Среды разработки тест включает веб-сервер Internet Information Services (IIS) 7.5 и сервер базы данных SQL Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="16b02-122">The developer test environment includes an Internet Information Services (IIS) 7.5 web server and a SQL Server 2008 R2 database server.</span></span>
- <span data-ttu-id="16b02-123">В рабочей среде включает несколько веб-серверов IIS 7.5, синхронизируются с сервером контроллера веб-фермы (WFF), вместе с сервера базы данных SQL Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="16b02-123">The production environment includes multiple IIS 7.5 web servers synchronized by a Web Farm Framework (WFF) controller server, together with a SQL Server 2008 R2 database server.</span></span> <span data-ttu-id="16b02-124">На практике сервер базы данных может использовать кластеризацию или зеркальное отображение для повышения доступности и масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="16b02-124">In practice, the database server may use clustering or mirroring to improve scalability and availability.</span></span>
- <span data-ttu-id="16b02-125">Промежуточная среда предназначен для репликации конфигурации рабочей среды, как можно точнее.</span><span class="sxs-lookup"><span data-stu-id="16b02-125">The staging environment is designed to replicate the configuration of the production environment as closely as possible.</span></span>
- <span data-ttu-id="16b02-126">Политики изоляции сети и брандмауэра не допускают прямой автоматического развертывания из внутренней сети для сети периметра.</span><span class="sxs-lookup"><span data-stu-id="16b02-126">The firewall and network isolation policies do not permit direct, automated deployment from the intranet to the perimeter network.</span></span>

<span data-ttu-id="16b02-127">Конфигурация каждой из этих сред описывается более подробно второй учебника [настройка сред сервера для развертывания веб-](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="16b02-127">The configuration of each of these environments is described in more detail in the second tutorial, [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

### <a name="team-roles-for-alm"></a><span data-ttu-id="16b02-128">Команды ролей для управления жизненным циклом Приложений</span><span class="sxs-lookup"><span data-stu-id="16b02-128">Team Roles for ALM</span></span>

<span data-ttu-id="16b02-129">Эти пользователи участвуют в создание, управление, создание и публикация решения диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="16b02-129">These users are involved in creating, managing, building, and publishing the Contact Manager solution:</span></span>

- <span data-ttu-id="16b02-130">Мэтт Hink является веб-разработчиком приложения компании Fabrikam, Inc. Он является частью рабочей группы, разработанных с помощью Visual Studio 2010 решение диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="16b02-130">Matt Hink is a web application developer at Fabrikam, Inc. He is part of the team who developed the Contact Manager solution by using Visual Studio 2010.</span></span> <span data-ttu-id="16b02-131">Мэтт имеет права администратора на серверах в среде тестирования developer позволяет ему настроить среду в соответствии с потребностями своей.</span><span class="sxs-lookup"><span data-stu-id="16b02-131">Matt has full administrator rights on the servers in the developer test environment, which lets him configure the environment to meet his needs.</span></span> <span data-ttu-id="16b02-132">Кроме того, у него есть доступ пользователей к экземпляру Visual Studio 2010 TFS, где он хранит исходный код для решения диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="16b02-132">He also has user access to the Visual Studio 2010 TFS instance where he stores the source code for the Contact Manager solution.</span></span>
- <span data-ttu-id="16b02-133">Rob Walters является администратором сервера для команды разработки компания Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="16b02-133">Rob Walters is a server administrator for the Fabrikam, Inc. development team.</span></span> <span data-ttu-id="16b02-134">Вадим имеет права администрирования на сервере TFS, таким образом, он может настраивать все аспекты TFS и Team Build.</span><span class="sxs-lookup"><span data-stu-id="16b02-134">Rob has administrative access on the TFS server so that he can configure all aspects of TFS and Team Build.</span></span> <span data-ttu-id="16b02-135">Вадим также имеет права администрирования теста и промежуточных веб-серверов и действует как администратор базы данных (DBA) для серверов баз данных в тест и промежуточные среды.</span><span class="sxs-lookup"><span data-stu-id="16b02-135">Rob also has administrative access to the test and staging web servers and acts as the database administrator (DBA) for the database servers in the test and staging environments.</span></span> <span data-ttu-id="16b02-136">Вадим настроил Team Build на сервере TFS, для выполнения этих задач:</span><span class="sxs-lookup"><span data-stu-id="16b02-136">Rob has configured Team Build on the TFS server to carry out these tasks:</span></span>

    - <span data-ttu-id="16b02-137">Построение и выполнение модульных тестов для приложения, каждый раз, когда пользователь возвращает файл для TFS.</span><span class="sxs-lookup"><span data-stu-id="16b02-137">Build and run unit tests on the application whenever a user checks in a file to TFS.</span></span> <span data-ttu-id="16b02-138">Это называется элемента конфигурации.</span><span class="sxs-lookup"><span data-stu-id="16b02-138">This is called CI.</span></span>
    - <span data-ttu-id="16b02-139">Автоматически разверните приложение диспетчера контактов в тестовую среду после приложение передает модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="16b02-139">Deploy the Contact Manager application to the test environment automatically once the application passes unit tests.</span></span> <span data-ttu-id="16b02-140">Сюда входят публикации базы данных на тестовых серверах на первоначального развертывания, а также все обновления в базу данных после первоначального развертывания.</span><span class="sxs-lookup"><span data-stu-id="16b02-140">This includes publishing the database to the test servers on initial deployment and any updates to the database after initial deployment.</span></span>
    - <span data-ttu-id="16b02-141">Разверните приложение диспетчера контактов в промежуточной среде, в один шаг процесса.</span><span class="sxs-lookup"><span data-stu-id="16b02-141">Deploy the Contact Manager application to the staging environment in a single-step process.</span></span>
    - <span data-ttu-id="16b02-142">Создание веб-пакета, администратору веб-сервера и администратор базы данных можно использовать для публикации приложения в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="16b02-142">Create a Web package that a Web server administrator and a DBA can use to publish the application to the production environment.</span></span>
- <span data-ttu-id="16b02-143">Лиза Андреева является администратором сервера, ответственный за развертывание приложений на производственных серверах компании Fabrikam, Inc.</span><span class="sxs-lookup"><span data-stu-id="16b02-143">Lisa Andrews is a server administrator responsible for deploying applications to the Fabrikam, Inc. production servers.</span></span> <span data-ttu-id="16b02-144">Она имеет доступ на чтение к общей папке, где TFS Team Build сохраняет пакет веб-развертывания после построения приложения диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="16b02-144">She has read access to the share where the TFS Team Build stores the web deployment package once it builds the Contact Manager application.</span></span> <span data-ttu-id="16b02-145">Она также должна административный доступ к рабочие веб-серверы, что она позволяет развертывать приложения в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="16b02-145">She also has administrative access to the production web servers so that she can deploy the application to production.</span></span> <span data-ttu-id="16b02-146">Кроме того она действует как администратор базы данных, кто развертывает баз данных и обновления базы данных на сервере базы данных в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="16b02-146">Additionally, she acts as the DBA who deploys databases and database updates to the database server in the production environment.</span></span>

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a><span data-ttu-id="16b02-147">Решение диспетчера контактов</span><span class="sxs-lookup"><span data-stu-id="16b02-147">The Contact Manager Solution</span></span>

<span data-ttu-id="16b02-148">Решение диспетчера контактов, предназначенное для зарегистрированного, вошедшего в систему пользователям добавлять и редактировать контактных сведений с помощью веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="16b02-148">The Contact Manager solution is designed to let registered, logged-in users add and edit contact information through a web interface.</span></span> <span data-ttu-id="16b02-149">Диспетчер контактов решение состоит из четырех отдельных проектов:</span><span class="sxs-lookup"><span data-stu-id="16b02-149">The Contact Manager solution consists of four individual projects:</span></span>

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- <span data-ttu-id="16b02-150">**ContactManager.Mvc**.</span><span class="sxs-lookup"><span data-stu-id="16b02-150">**ContactManager.Mvc**.</span></span> <span data-ttu-id="16b02-151">Это проект веб-приложения ASP.NET MVC3, представляющий точку входа для решения.</span><span class="sxs-lookup"><span data-stu-id="16b02-151">This is an ASP.NET MVC3 web application project that represents the entry point for the solution.</span></span> <span data-ttu-id="16b02-152">Он предлагает некоторые основные web функциональные возможности приложений, как предоставить пользователям возможность создавать и просматривать сведения о контакте.</span><span class="sxs-lookup"><span data-stu-id="16b02-152">It offers some basic web application functionality, like providing users with the ability to create and view contact details.</span></span> <span data-ttu-id="16b02-153">Приложение зависит от службы Windows Communication Foundation (WCF) для управления контактами и базу данных служб приложения ASP.NET для управления проверки подлинности и авторизации.</span><span class="sxs-lookup"><span data-stu-id="16b02-153">The application relies on a Windows Communication Foundation (WCF) service to manage contacts and an ASP.NET application services database to manage authentication and authorization.</span></span>
- <span data-ttu-id="16b02-154">**ContactManager.Database**.</span><span class="sxs-lookup"><span data-stu-id="16b02-154">**ContactManager.Database**.</span></span> <span data-ttu-id="16b02-155">Это проект базы данных Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="16b02-155">This is a Visual Studio 2010 database project.</span></span> <span data-ttu-id="16b02-156">Проект определяет схему для базы данных, сведения о контакте хранилищ.</span><span class="sxs-lookup"><span data-stu-id="16b02-156">The project defines the schema for a database that stores contact details.</span></span>
- <span data-ttu-id="16b02-157">**ContactManager.Service**.</span><span class="sxs-lookup"><span data-stu-id="16b02-157">**ContactManager.Service**.</span></span> <span data-ttu-id="16b02-158">Это проект веб-службы WCF.</span><span class="sxs-lookup"><span data-stu-id="16b02-158">This is a WCF web service project.</span></span> <span data-ttu-id="16b02-159">WCF предоставляет, создать конечную точку, которая позволяет вызывающим объектам осуществлять, получения, обновления и удаления (CRUD) с базы данных диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="16b02-159">The WCF exposes an endpoint that allows callers to perform create, retrieve, update, and delete (CRUD) operations on the Contact Manager database.</span></span> <span data-ttu-id="16b02-160">Служба зависит от базы данных диспетчера контактов и ContactManager.Common.dll сборки.</span><span class="sxs-lookup"><span data-stu-id="16b02-160">The service relies on the Contact Manager database and the ContactManager.Common.dll assembly.</span></span>
- <span data-ttu-id="16b02-161">**ContactManager.Common**.</span><span class="sxs-lookup"><span data-stu-id="16b02-161">**ContactManager.Common**.</span></span> <span data-ttu-id="16b02-162">Это проект библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="16b02-162">This is a class library project.</span></span> <span data-ttu-id="16b02-163">Служба WCF использует типы, определенные в этой сборке.</span><span class="sxs-lookup"><span data-stu-id="16b02-163">The WCF service relies on types defined in this assembly.</span></span>

<span data-ttu-id="16b02-164">В первом учебнике этой серии предоставляется полный обзор решения и его требования к развертыванию [веб-развертывания на предприятии](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span><span class="sxs-lookup"><span data-stu-id="16b02-164">A complete review of the solution and its deployment requirements is provided in the first tutorial in this series, [Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span>

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a><span data-ttu-id="16b02-165">Задачи развертывания</span><span class="sxs-lookup"><span data-stu-id="16b02-165">Deployment Tasks</span></span>

<span data-ttu-id="16b02-166">Существует несколько различных задач, связанных с развертыванием приложений для различных сред в крупной организации.</span><span class="sxs-lookup"><span data-stu-id="16b02-166">There are several distinct tasks involved in deploying applications to different environments in a large organization.</span></span> <span data-ttu-id="16b02-167">Существуют следующие основные задачи, которые в учебниках рассматриваются:</span><span class="sxs-lookup"><span data-stu-id="16b02-167">These are the key tasks that the tutorials cover:</span></span>

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

<span data-ttu-id="16b02-168">Ниже приведен список каждого из этапов процесса развертывания с точки зрения пользователей, описанных ранее в этом документе:</span><span class="sxs-lookup"><span data-stu-id="16b02-168">Here is a list of each step in the deployment process from the perspective of the users described earlier in this document:</span></span>

1. <span data-ttu-id="16b02-169">Все члены команды просмотрите решение в Visual Studio 2010, чтобы определить требования к развертыванию ключа и проблемы диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="16b02-169">All members of the team review the Contact Manager solution in Visual Studio 2010 to determine key deployment requirements and issues.</span></span>
2. <span data-ttu-id="16b02-170">Мэтт Hink может развернуть решение диспетчера контактов непосредственно с рабочей станции разработчика в тестовую среду разработчика для первоначального теста логики развертывания.</span><span class="sxs-lookup"><span data-stu-id="16b02-170">Matt Hink may deploy the Contact Manager solution directly from the developer workstation to the developer test environment, to conduct an initial test of the deployment logic.</span></span>
3. <span data-ttu-id="16b02-171">Мэтт Hink добавляет приложение в систему управления версиями в Team Foundation Server.</span><span class="sxs-lookup"><span data-stu-id="16b02-171">Matt Hink adds the application to source control in TFS.</span></span>
4. <span data-ttu-id="16b02-172">Rob Walters создает различные определения сборки для решения диспетчера контактов в Team Build.</span><span class="sxs-lookup"><span data-stu-id="16b02-172">Rob Walters creates various build definitions for the Contact Manager solution in Team Build.</span></span> <span data-ttu-id="16b02-173">Одно определение построения использует элемента конфигурации для развертывания решения в тестовую среду разработчика всякий раз, когда пользователь возвращает новый код.</span><span class="sxs-lookup"><span data-stu-id="16b02-173">One build definition uses CI to deploy the solution to the developer test environment whenever a user checks in new code.</span></span> <span data-ttu-id="16b02-174">Другое определение построения позволяет пользователям триггера развертывания в промежуточной среде, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="16b02-174">Another build definition lets users trigger deployments to the staging environment as required.</span></span>
5. <span data-ttu-id="16b02-175">Каждый раз при возврате нового кода, Team Build автоматически создает компоненты решения, запускает модульные тесты и развертывает решение в тестовой среде разработчика, если построение выполнено успешно и модульные тесты пройдены.</span><span class="sxs-lookup"><span data-stu-id="16b02-175">Every time a user checks in new code, Team Build automatically builds the solution components, runs unit tests, and deploys the solution to the developer test environment if the build was successful and the unit tests pass.</span></span>
6. <span data-ttu-id="16b02-176">Когда пользователь запускает развертывания в промежуточной среде, решение упаковывается и развертывается в процессе один шаг.</span><span class="sxs-lookup"><span data-stu-id="16b02-176">When a user triggers a deployment to the staging environment, the solution is packaged and deployed in a single-step process.</span></span> <span data-ttu-id="16b02-177">Этот процесс также создает пакет ручного развертывания в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="16b02-177">This process also generates a package for manual deployment to the production environment.</span></span>
7. <span data-ttu-id="16b02-178">Лиза Андреева развертывает приложение в рабочей среде вручную, импортируя веб-пакет, созданный на шаге 6.</span><span class="sxs-lookup"><span data-stu-id="16b02-178">Lisa Andrews deploys the application to the production environment by manually importing the web package created in step 6.</span></span>

### <a name="key-deployment-issues"></a><span data-ttu-id="16b02-179">Проблемы с развертыванием ключа</span><span class="sxs-lookup"><span data-stu-id="16b02-179">Key Deployment Issues</span></span>

<span data-ttu-id="16b02-180">Fabrikam, Inc. сценарии и решения диспетчера контактов выделите различных распространенных ошибок и проблем, которые могут возникнуть при развертывании комплексного решения корпоративного уровня.</span><span class="sxs-lookup"><span data-stu-id="16b02-180">The Contact Manager solution and the Fabrikam, Inc. scenario highlight various common issues and challenges that you may encounter when you deploy complex, enterprise-scale solutions.</span></span> <span data-ttu-id="16b02-181">Пример:</span><span class="sxs-lookup"><span data-stu-id="16b02-181">For example:</span></span>

- <span data-ttu-id="16b02-182">Необходимо иметь возможность развернуть проекты для нескольких сред, таких как разработчик или тестовую среду, промежуточные платформы и производственных серверах.</span><span class="sxs-lookup"><span data-stu-id="16b02-182">You need to be able to deploy projects to multiple environments, like developer or test environments, staging platforms, and production servers.</span></span> <span data-ttu-id="16b02-183">Решения должен быть развернут с помощью параметров конфигурации для каждой среды.</span><span class="sxs-lookup"><span data-stu-id="16b02-183">The solution needs to be deployed with different configuration settings for each environment.</span></span>
- <span data-ttu-id="16b02-184">Необходимо развернуть несколько зависимых проектов одновременно как часть один шаг или автоматизированного процесса построения и развертывания.</span><span class="sxs-lookup"><span data-stu-id="16b02-184">You need to deploy multiple dependent projects simultaneously as part of a single-step or automated build and deployment process.</span></span>
- <span data-ttu-id="16b02-185">Необходимо иметь возможность развертывания диска из автоматизированного процесса.</span><span class="sxs-lookup"><span data-stu-id="16b02-185">You need to be able to drive deployment from an automated process.</span></span> <span data-ttu-id="16b02-186">Например вы хотите использовать процесс непрерывной Интеграции для развертывания веб-приложения в промежуточной среде, при возврате нового кода.</span><span class="sxs-lookup"><span data-stu-id="16b02-186">For example, you want to use a CI process to deploy web applications to a staging environment when new code is checked in.</span></span>
- <span data-ttu-id="16b02-187">Необходимо иметь возможность контролировать процесс развертывания и установка переменных развертывания из вне Visual Studio, как разработчики вряд ли будут иметь правильные параметры или учетные данные для каждой целевой среды.</span><span class="sxs-lookup"><span data-stu-id="16b02-187">You need to be able to control the deployment process and set deployment variables from outside Visual Studio, as developers are unlikely to have the correct configuration settings or the necessary credentials for every target environment.</span></span>
- <span data-ttu-id="16b02-188">Необходимо развертывать проекты базы данных на основе схемы и сохранить существующие данные в последующих развертываниях.</span><span class="sxs-lookup"><span data-stu-id="16b02-188">You need to deploy schema-based database projects and preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="16b02-189">Необходимо выполнить развертывание базы данных членства на нерегламентированные без развертывания данных учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="16b02-189">You need to deploy membership databases on an ad hoc basis without deploying user account data.</span></span> <span data-ttu-id="16b02-190">Также может потребоваться обновить схему баз данных развернутой членства без потери существующих данных учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="16b02-190">You may also need to update the schema of deployed membership databases without losing existing user account data.</span></span>
- <span data-ttu-id="16b02-191">Необходимо исключить определенные файлы или папки, при развертывании содержимого на различных целевых средах.</span><span class="sxs-lookup"><span data-stu-id="16b02-191">You need to exclude certain files or folders when you deploy content to various target environments.</span></span>

<span data-ttu-id="16b02-192">Кроме того Управление развертыванием, когда обновления будут часто и добавочные вызывает некоторые дополнительные сложности.</span><span class="sxs-lookup"><span data-stu-id="16b02-192">In addition, managing deployment when updates are frequent and incremental throws up some additional challenges.</span></span> <span data-ttu-id="16b02-193">Пример:</span><span class="sxs-lookup"><span data-stu-id="16b02-193">For example:</span></span>

- <span data-ttu-id="16b02-194">Выполнение модульных тестов, каждый раз, разработчик возвращает в новом коде.</span><span class="sxs-lookup"><span data-stu-id="16b02-194">You run unit tests every time a developer checks in new code.</span></span> <span data-ttu-id="16b02-195">Необходимо развернуть решение, если код проходит модульных тестов.</span><span class="sxs-lookup"><span data-stu-id="16b02-195">You only want to deploy the solution if the code passes the unit tests.</span></span>
- <span data-ttu-id="16b02-196">При развертывании веб-приложения в промежуточной или рабочей среде, необходимо перенаправить пользователя на *приложения\_offline.htm* файла в течение всего процесса развертывания.</span><span class="sxs-lookup"><span data-stu-id="16b02-196">When you deploy a web application to a staging or production environment, you want to redirect users to an *app\_offline.htm* file for the duration of the deployment process.</span></span>
- <span data-ttu-id="16b02-197">Вы хотите войти операции развертывания.</span><span class="sxs-lookup"><span data-stu-id="16b02-197">You want to log deployment activities.</span></span> <span data-ttu-id="16b02-198">Процесс развертывания следует отправить уведомления по электронной почте успешной или неуспешной развертываний выбранным получателям.</span><span class="sxs-lookup"><span data-stu-id="16b02-198">The deployment process should send email notifications of successful or failed deployments to designated recipients.</span></span>
- <span data-ttu-id="16b02-199">При сбое автоматизированного развертывания, процесс развертывания должен повторите текущее развертывание или развертывание вместо предыдущего веб-пакета.</span><span class="sxs-lookup"><span data-stu-id="16b02-199">If an automated deployment fails, the deployment process should retry the current deployment or deploy the previous web package instead.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="16b02-200">[Назад](deploying-web-applications-in-enterprise-scenarios.md)
[Вперед](application-lifecycle-management-from-development-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="16b02-200">[Previous](deploying-web-applications-in-enterprise-scenarios.md)
[Next](application-lifecycle-management-from-development-to-production.md)</span></span>