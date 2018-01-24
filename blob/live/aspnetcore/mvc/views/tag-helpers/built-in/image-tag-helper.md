---
title: "Вспомогательный тег изображения | Документы Microsoft"
author: pkellner
description: "Показано, как работать с тега поддержки изображений"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/image-tag-helper
ms.openlocfilehash: 438c5afb96dce6d8978d26159a3b460614111988
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="imagetaghelper"></a><span data-ttu-id="c6fe9-103">ImageTagHelper</span><span class="sxs-lookup"><span data-stu-id="c6fe9-103">ImageTagHelper</span></span>

<span data-ttu-id="c6fe9-104">Автор: [Питер Кельнер (Peter Kellner)](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="c6fe9-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="c6fe9-105">Тег поддержки изображений улучшает `img` (`<img>`) тега.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-105">The Image Tag Helper enhances the `img` (`<img>`) tag.</span></span> <span data-ttu-id="c6fe9-106">Требуется `src` тег а также `boolean` атрибут `asp-append-version`.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-106">It requires a `src` tag as well as the `boolean` attribute `asp-append-version`.</span></span>

<span data-ttu-id="c6fe9-107">Если источник изображения (`src`) представляет собой статический файл на сервере веб-узла добавляется уникальный кэша busting строку как параметр запроса для источника изображения.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-107">If the image source (`src`) is a static file on the host web server, a unique cache busting string is appended as a query parameter to the image source.</span></span> <span data-ttu-id="c6fe9-108">Это гарантирует, что при изменении файла на сервере веб-узла URL-АДРЕСЕ запроса уникальный создается, содержит параметр обновленный запрос.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-108">This ensures that if the file on the host web server changes, a unique request URL is generated that includes the updated request parameter.</span></span> <span data-ttu-id="c6fe9-109">Кэш busting строка имеет уникальное значение, представляющее хэш файла статическое изображение.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-109">The cache busting string is a unique value representing the hash of the static image file.</span></span>

<span data-ttu-id="c6fe9-110">Если источник изображения (`src`) не является статическим файлом (например удаленный URL-адрес или файл не существует на сервере) `<img>` тега `src` без кэширования, busting строкового параметра запроса создается атрибут.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-110">If the image source (`src`) isn't a static file (for example a remote URL or the file doesn't exist on the server), the `<img>` tag's `src` attribute is generated with no cache busting query string parameter.</span></span>

## <a name="image-tag-helper-attributes"></a><span data-ttu-id="c6fe9-111">Атрибуты вспомогательного тега Image</span><span class="sxs-lookup"><span data-stu-id="c6fe9-111">Image Tag Helper Attributes</span></span>


### <a name="asp-append-version"></a><span data-ttu-id="c6fe9-112">добавить версию ASP</span><span class="sxs-lookup"><span data-stu-id="c6fe9-112">asp-append-version</span></span>

<span data-ttu-id="c6fe9-113">При указании вместе с `src` атрибут вспомогательный тег изображения вызывается.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-113">When specified along with a `src` attribute, the Image Tag Helper is invoked.</span></span>

<span data-ttu-id="c6fe9-114">Примером является допустимым `img` модуль тег:</span><span class="sxs-lookup"><span data-stu-id="c6fe9-114">An example of a valid `img` tag helper is:</span></span>

```cshtml
<img src="~/images/asplogo.png" 
    asp-append-version="true"  />
```

<span data-ttu-id="c6fe9-115">Если статический файл существует в каталоге *... wwwroot/Images/asplogo.PNG* созданного кода html (хэш-код будет отличаться) следующего вида:</span><span class="sxs-lookup"><span data-stu-id="c6fe9-115">If the static file exists in the directory *..wwwroot/images/asplogo.png* the generated html is similar to the following (the hash will be different):</span></span>

```html
<img 
    src="/images/asplogo.png?v=Kl_dqr9NVtnMdsM2MUg4qthUnWZm5T1fCEimBPWDNgM"/>
```

<span data-ttu-id="c6fe9-116">Значение, присваиваемое параметру `v` значение хэша файла на диске.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-116">The value assigned to the parameter `v` is the hash value of the file on disk.</span></span> <span data-ttu-id="c6fe9-117">Если веб-сервер не может получить доступ на чтение к статические ссылки на файл, нет `v` добавляется параметры `src` атрибута.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-117">If the web server is unable to obtain read access to the static file referenced,  no `v` parameters is added to the `src` attribute.</span></span>

- - -

### <a name="src"></a><span data-ttu-id="c6fe9-118">src</span><span class="sxs-lookup"><span data-stu-id="c6fe9-118">src</span></span>

<span data-ttu-id="c6fe9-119">Чтобы активировать вспомогательный тег изображения, атрибут src необходим для `<img>` элемента.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-119">To activate the Image Tag Helper, the src attribute is required on the `<img>` element.</span></span> 

> [!NOTE]
> <span data-ttu-id="c6fe9-120">Использует вспомогательный тег изображения `Cache` поставщика на локальном веб-сервере для хранения вычисляемого `Sha512` для заданного файла.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-120">The Image Tag Helper uses the `Cache` provider on the local web server to store the calculated `Sha512` of a given file.</span></span> <span data-ttu-id="c6fe9-121">Если снова запрошенный файл `Sha512` не требуется повторное вычисление.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-121">If the file is requested again the `Sha512` does not need to be recalculated.</span></span> <span data-ttu-id="c6fe9-122">Кэш становится недействительным, файл наблюдатель, который присоединяется к файлу при его `Sha512` вычисляется.</span><span class="sxs-lookup"><span data-stu-id="c6fe9-122">The Cache is invalidated by a file watcher that is attached to the file when the file's `Sha512` is calculated.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6fe9-123">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c6fe9-123">Additional resources</span></span>

* <xref:performance/caching/memory>