---
title: "Начало работы с Razor Pages в ASP.NET Core на Mac"
author: rick-anderson
description: "Начало работы с Razor Pages в ASP.NET Core с использованием Visual Studio для Mac"
ms.author: riande
manager: wpickett
ms.date: 07/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-mac/razor-pages-start
ms.openlocfilehash: ca9fca507096f3f09f19fe0a7f1dc023003649d7
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-razor-pages-in-aspnet-core-with-visual-studio-for-mac"></a><span data-ttu-id="7bb9d-103">Начало работы с Razor Pages в ASP.NET Core с использованием Visual Studio для Mac</span><span class="sxs-lookup"><span data-stu-id="7bb9d-103">Getting started with Razor Pages in ASP.NET Core with Visual Studio for Mac</span></span>

<span data-ttu-id="7bb9d-104">Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)</span><span class="sxs-lookup"><span data-stu-id="7bb9d-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="7bb9d-105">В этом учебнике приводятся основные сведения о веб-приложении Razor Pages в ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="7bb9d-106">Перед работой с этим учебником рекомендуем изучить статью [Введение в Razor Pages](xref:mvc/razor-pages/index).</span><span class="sxs-lookup"><span data-stu-id="7bb9d-106">We recommend you complete [Introduction to Razor Pages](xref:mvc/razor-pages/index) before starting this tutorial.</span></span> <span data-ttu-id="7bb9d-107">Razor Pages — это рекомендуемый способ создания пользовательского интерфейса для веб-приложений в ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-107">Razor Pages is the recommended way to build UI for web applications in ASP.NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bb9d-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7bb9d-108">Prerequisites</span></span>

<span data-ttu-id="7bb9d-109">Установите следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="7bb9d-109">Install the following:</span></span>

* <span data-ttu-id="7bb9d-110">[пакет SDK для .NET Core 2.0.0](https://www.microsoft.com/net/core) или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="7bb9d-110">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span></span>
* [<span data-ttu-id="7bb9d-111">Visual Studio для Mac</span><span class="sxs-lookup"><span data-stu-id="7bb9d-111">Visual Studio for Mac</span></span>](https://www.visualstudio.com/vs/visual-studio-mac/)

## <a name="create-a-razor-web-app"></a><span data-ttu-id="7bb9d-112">Создание веб-приложения Razor</span><span class="sxs-lookup"><span data-stu-id="7bb9d-112">Create a Razor web app</span></span>

<span data-ttu-id="7bb9d-113">Из терминала выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-113">From a terminal, run the following commands:</span></span>

```console
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```

<span data-ttu-id="7bb9d-114">Указанные выше команды используют [интерфейс командной строки .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet) для создания и запуска проекта Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-114">The preceding commands use the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet) to create and run a Razor Pages project.</span></span> <span data-ttu-id="7bb9d-115">Откройте в браузере страницу http://localhost:5000 для просмотра приложения.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-115">Open a browser to http://localhost:5000 to view the application.</span></span>

![Домашняя или индексная страница](../razor-pages/razor-pages-start/_static/home.png)

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

## <a name="open-the-project"></a><span data-ttu-id="7bb9d-117">Открытие проекта</span><span class="sxs-lookup"><span data-stu-id="7bb9d-117">Open the project</span></span>

<span data-ttu-id="7bb9d-118">Нажмите клавиши CTRL+C, чтобы завершить работу приложения.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-118">Press Ctrl+C to shut down the application.</span></span>

<span data-ttu-id="7bb9d-119">В Visual Studio откройте меню **Файл > Открыть файл** и выберите файл *RazorPagesMovie.csproj*.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-119">From Visual Studio, select **File > Open**, and then select the *RazorPagesMovie.csproj* file.</span></span>

### <a name="launch-the-app"></a><span data-ttu-id="7bb9d-120">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="7bb9d-120">Launch the app</span></span>

<span data-ttu-id="7bb9d-121">В Visual Studio откройте меню **Выполнить > Запуск без отладки**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-121">In Visual Studio, select **Run > Start Without Debugging** to launch the app.</span></span> <span data-ttu-id="7bb9d-122">Visual Studio запускает [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview), открывает браузер и переходит к `http://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-122">Visual Studio starts [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview), launches a browser, and navigates to `http://localhost:5000`.</span></span>

<span data-ttu-id="7bb9d-123">В следующем учебнике мы добавим в проект модель.</span><span class="sxs-lookup"><span data-stu-id="7bb9d-123">In the next tutorial, we add a model to the project.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="7bb9d-124">Далее: добавление модели</span><span class="sxs-lookup"><span data-stu-id="7bb9d-124">Next: Adding a model</span></span>](xref:tutorials/razor-pages-mac/model)