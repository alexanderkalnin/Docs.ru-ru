---
title: "Добавление поиска"
author: rick-anderson
description: "Инструкции по добавлению поиска в простое приложение ASP.NET Core MVC"
manager: wpickett
ms.author: riande
ms.date: 03/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app/search
ms.openlocfilehash: 3ab9086275ec4c3651383c4c845e40db55f67f4c
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/30/2018
---
[!INCLUDE[adding-model](../../includes/mvc-intro/search1.md)]

Параметр `searchString` можно быстро переименовать в `id` с помощью команды **rename**. Щелкните правой кнопкой мыши элемент `searchString` **> Rename**.

![Контекстное меню](search/_static/rename.png)

Выделены целевые объекты для команды переименования.

![Редактор кода с выделенной переменной в методе Index ActionResult](search/_static/rename2.png)

Измените параметр на `id`, а все вхождения `searchString` — на `id`.

![Редактор кода, в котором переменная изменена на идентификатор](search/_static/rename3.png)

[!INCLUDE[adding-model](../../includes/mvc-intro/search2.md)]

Обратите внимание на то, как IntelliSense автоматически обновляет разметку.

![Контекстное меню IntelliSense с методом, выбранным в списке атрибутов для элемента form](search/_static/int_m.png)

![Контекстное меню IntelliSense с методом get, выбранным в списке значений атрибутов метода](search/_static/int_get.png)

Обратите внимание на другой шрифт тега `<form>`. Такое выделение свидетельствует о том, что тег поддерживается [вспомогательными функциями тегов](../../mvc/views/tag-helpers/intro.md).

![Тег form, выделенный фиолетовым цветом](search/_static/th_font.png)

[!INCLUDE[adding-model](../../includes/mvc-intro/search3.md)]

>[!div class="step-by-step"]
[Назад](controller-methods-views.md)
[Вперед](new-field.md)  
