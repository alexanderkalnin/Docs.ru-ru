---
title: "Начало работы с ASP.NET Core 1.1"
author: rick-anderson
description: "Краткий учебник, в котором с помощью ASP.NET Core 1.1 создается и запускается простое приложение Hello World."
ms.author: riande
manager: wpickett
ms.date: 08/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: getting-started-1.1
ms.openlocfilehash: 7f178618508e1a1e9c49d8ace619b9f942998dae
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-aspnet-core-11"></a><span data-ttu-id="a207d-103">Начало работы с ASP.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="a207d-103">Getting Started with ASP.NET Core 1.1</span></span>

> [!NOTE]
> <span data-ttu-id="a207d-104">Эти инструкции предназначены для ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="a207d-104">These instructions are for ASP.NET Core 1.1.</span></span> <span data-ttu-id="a207d-105">Нужны сведения о последней версии?</span><span class="sxs-lookup"><span data-stu-id="a207d-105">Looking for the latest version?</span></span> <span data-ttu-id="a207d-106">См. [текущую версию этого учебника](xref:getting-started).</span><span class="sxs-lookup"><span data-stu-id="a207d-106">See [the current version of this tutorial](xref:getting-started).</span></span>

1. <span data-ttu-id="a207d-107">Запустите **установщик пакета SDK** версии 1.0.4 для .NET Core, который можно получить на [странице скачивания пакета SDK версии 1.0.4 для .NET Core 1.0.5 и 1.1.2](https://github.com/dotnet/core/blob/master/release-notes/download-archives/1.0.5-download.md).</span><span class="sxs-lookup"><span data-stu-id="a207d-107">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core 1.0.5 & 1.1.2 SDK 1.0.4 downloads page](https://github.com/dotnet/core/blob/master/release-notes/download-archives/1.0.5-download.md).</span></span>

2. <span data-ttu-id="a207d-108">Создайте папку для нового проекта .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a207d-108">Create a folder for a new .NET Core project.</span></span>

   <span data-ttu-id="a207d-109">В macOS или Linux откройте окно терминала.</span><span class="sxs-lookup"><span data-stu-id="a207d-109">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="a207d-110">В Windows откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="a207d-110">On Windows, open a command prompt.</span></span>

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

2. <span data-ttu-id="a207d-111">Если на компьютере установлена более поздняя версия пакета SDK, создайте файл *global.json*, чтобы выбрать пакет SDK версии 1.0.4.</span><span class="sxs-lookup"><span data-stu-id="a207d-111">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

2. <span data-ttu-id="a207d-112">Создайте проект .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a207d-112">Create a new .NET Core project.</span></span>

   ```terminal
   dotnet new web
   ```
   
3.  <span data-ttu-id="a207d-113">Восстановите пакеты.</span><span class="sxs-lookup"><span data-stu-id="a207d-113">Restore the packages.</span></span>

    ```terminal
    dotnet restore
    ```

4. <span data-ttu-id="a207d-114">Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="a207d-114">Run the app.</span></span>

   <span data-ttu-id="a207d-115">При необходимости команда `dotnet run` сначала выполняет сборку приложения.</span><span class="sxs-lookup"><span data-stu-id="a207d-115">The `dotnet run` command builds the app first if needed.</span></span>

   ```terminal
   dotnet run
   ```

5. <span data-ttu-id="a207d-116">Перейдите по адресу `http://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="a207d-116">Browse to `http://localhost:5000`</span></span>

<!-- H3 to avoid a single-entry internal TOC -->
### <a name="next-steps"></a><span data-ttu-id="a207d-117">Следующие шаги</span><span class="sxs-lookup"><span data-stu-id="a207d-117">Next steps</span></span>

<span data-ttu-id="a207d-118">Учебники по началу работы см. на странице [Учебники по ASP.NET Core](tutorials/index.md).</span><span class="sxs-lookup"><span data-stu-id="a207d-118">For getting-started tutorials, see [ASP.NET Core Tutorials](tutorials/index.md)</span></span>

<span data-ttu-id="a207d-119">Сведения об основных понятиях и архитектуре ASP.NET Core см. в статьях [Введение в ASP.NET Core](index.md) и [Основы ASP.NET Core](fundamentals/index.md).</span><span class="sxs-lookup"><span data-stu-id="a207d-119">For an introduction to ASP.NET Core concepts and architecture, see [ASP.NET Core Introduction](index.md) and [ASP.NET Core Fundamentals](fundamentals/index.md).</span></span>

<span data-ttu-id="a207d-120">Приложение ASP.NET Core может использовать библиотеку базовых классов и среду выполнения .NET Core или .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a207d-120">An ASP.NET Core app can use the .NET Core or .NET Framework Base Class Library and runtime.</span></span> <span data-ttu-id="a207d-121">Дополнительные сведения см. в статье [Выбор между .NET Core и .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span><span class="sxs-lookup"><span data-stu-id="a207d-121">For more information, see [Choosing between .NET Core and .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>