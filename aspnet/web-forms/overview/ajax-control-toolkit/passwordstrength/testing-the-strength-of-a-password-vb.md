---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: "Тестирование стойкость пароля (VB) | Документы Microsoft"
author: wenz
description: "Пароли являются обязательными практически в любом месте, чтобы отложенной пользователей, как правило, выберите простые пароли, которые легко взломать. Элемент управления PasswordStrength в ASP. N...."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: 7f09a05fd4b5771b7ab532d40476fe45cbd3fe38
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="testing-the-strength-of-a-password-vb"></a>Тестирование стойкость пароля (Visual Basic)
====================
по [Кристиан Wenz](https://github.com/wenz)

[Загрузить код](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) или [скачать PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)

> Пароли являются обязательными практически в любом месте, чтобы отложенной пользователей, как правило, выберите простые пароли, которые легко взломать. PasswordStrength управления в наборе элементов управления ASP.NET AJAX можно проверить, насколько хорошо находится пароль.


## <a name="overview"></a>Обзор

Пароли являются обязательными практически в любом месте, чтобы отложенной пользователей, как правило, выберите простые пароли, которые легко взломать. `PasswordStrength` Элемента управления в наборе элементов управления ASP.NET AJAX можно проверить, насколько хорошо находится пароль.

## <a name="steps"></a>Шаги

`PasswordStrength` Управления расширяет текстовое поле и проверяет, является ли пароль в нем достаточно хорошо. Он предлагает широкий набор функций через атрибуты; Ниже приведены только некоторые из них.

- `MinimumNumericCharacters`Минимальное число цифр в пароле
- `MinimumSymbolCharacters`Минимальное количество специальных символов (не букв и цифр) в пароле
- `PreferredPasswordLength`Минимальная длина пароля
- `RequiresUpperAndLowerCaseCharacters`нужно ли использовать прописные и строчные буквы пароль

`StrengthIndicatorType` Сведения будут отображаться стойкость пароля, как текст (значение `"Text"`) или как тип индикатор хода выполнения (значение `"BarIndicator"`). В `DisplayPosition` атрибут, настройке где отображаются сведения. Ниже приведен полный пример, включая ASP.NET AJAX `ScriptManager` управления `PasswordStrength` управления и, конечно, текстовое поле, где пользователь может ввести пароль. Для примера поле последняя форма является регулярного текстовое поле, а не поле пароля, чтобы во время разработки можно увидеть введя.

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

Запустите страницу и введите отсутствовали: только после ввода строчные буквы, прописные буквы, цифры и символы, считается как неразрывный пароль.


[![Теперь пароль () вполне](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

Теперь пароль () вполне ([Просмотр полноразмерное изображение](testing-the-strength-of-a-password-vb/_static/image3.png))

>[!div class="step-by-step"]
[Назад](testing-the-strength-of-a-password-cs.md)
