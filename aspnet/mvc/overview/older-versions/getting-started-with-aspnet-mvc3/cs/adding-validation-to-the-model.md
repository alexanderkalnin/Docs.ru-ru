---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: "Добавление проверки для модели (C#) | Документы Microsoft"
author: Rick-Anderson
description: "Создание контроллера"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 6bce4a5d889f548cb1faec15842310703d7077b8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
<a name="adding-validation-to-the-model-c"></a>Добавление проверки для модели (C#)
====================
По [Рик Андерсон](https://github.com/Rick-Anderson)

> > [!NOTE]
> > Доступна обновленная версия этого учебника [здесь](../../../getting-started/introduction/getting-started.md) , с использованием ASP.NET MVC 5 и Visual Studio 2013. Он является более безопасны, выполните гораздо проще и показаны дополнительные возможности.
> 
> 
> Этот учебник поможет узнать основы создания MVC веб-приложения ASP.NET с помощью Microsoft Visual Web Developer 2010 Express пакетом обновления 1, которой — это бесплатная версия Microsoft Visual Studio. Прежде чем начать, убедитесь, что вы установили необходимые компоненты, перечисленные ниже. Все из них можно установить, щелкнув по следующей ссылке: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того можно установить отдельно предварительные требования, используя следующие ссылки:
> 
> - [Необходимые компоненты Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление средств ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(среда выполнения + средства поддержки)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, необходимо установить необходимые компоненты, щелкнув по следующей ссылке: [необходимых компонентов Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Проект Visual Web Developer с исходного кода C# доступна по следующему адресу. [Загрузка версии C#](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Если используется Visual Basic, перейдите в [Visual Basic-версии](../vb/intro-to-aspnet-mvc-3.md) этого учебника.


В этом разделе вы добавите логику проверки в `Movie` модель и необходимо убедиться, что правила проверки применяются каждый раз при попытке создать или изменить фильм, с помощью приложения.

## <a name="keeping-things-dry"></a>Чтобы оставить ТОНЕРА

Одна из основных принципов разработки ASP.NET MVC — ПРОБНОГО («не повторяться»). ASP.NET MVC рекомендует как можно указать только один раз возможности или поведение и включить его everywhere отражаться в приложении. Это уменьшает объем кода, который необходимо написать и делает код, который вы написали гораздо проще для поддержки.

Поддержка проверки в ASP.NET MVC и Entity Framework Code First является отличным примером ТОНЕРА принципа в действии. Правила проверки можно задать декларативно в одном месте (в класс модели), а затем эти правила будут применены везде в приложении.

Давайте взглянем на как можно воспользоваться преимуществами этой поддержки проверки в приложении фильма.

## <a name="adding-validation-rules-to-the-movie-model"></a>Добавление правил проверки модели фильма

Сначала добавить некоторую логику проверки для `Movie` класса.

Откройте файл *Movie.cs*. Добавить `using` инструкции в верхней части файла, который ссылается на [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) пространство имен:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

Пространство имен является частью .NET Framework. Она предоставляет встроенные набор атрибутов проверки, которые декларативно применяются к любому классу или свойству.

Теперь обновите `Movie` класса, чтобы воспользоваться преимуществами встроенной [ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), и [ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) атрибутов проверки . В качестве примера для применения атрибутов, используйте следующий код.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

Атрибуты проверки определяют поведение для свойств модели, к которым они применяются. `Required` Атрибут указывает, что свойство должно иметь значение; в этом образце фильм должен иметь значения для `Title`, `ReleaseDate`, `Genre`, и `Price` свойства, чтобы быть допустимыми. Атрибут `Range` ограничивает диапазон значений. Атрибут `StringLength` позволяет задать максимальную и при необходимости минимальную длину строкового свойства.

Код сначала проверяет, применение правил проверки, заданные на класс модели перед приложение сохраняет изменения в базе данных. Например, в приведенном ниже коде возникает исключение при `SaveChanges` вызывается метод, так как некоторые необходимые `Movie` отсутствуют значения свойств и цена равно нулю (то выходит за пределы допустимого диапазона).

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

С платформой .NET Framework автоматически применяются правила проверки помогает сделать приложение более надежным. Это также гарантирует, что в любом случае будут выполнены все проверки и в базе данных не будут случайно оставлены поврежденные данные.

Ниже приведен полный код для обновленного *Movie.cs* файла:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>Ошибка проверки пользовательского интерфейса в ASP.NET MVC

Повторно запустите приложение и перейдите к */Movies* URL-адрес.

Нажмите кнопку **создания фильма** ссылку, чтобы добавить новый фильма. Заполните форму с некоторые недопустимые значения, а затем нажмите кнопку **создать** кнопки.

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

Обратите внимание на то, как форма автоматически использовал цвет фона для выделите текстовые поля, содержащие недопустимые данные и испускаемого соответствующее сообщение об ошибке проверки рядом с каждого из них. Сообщения об ошибках соответствует строки ошибок указано, при которых указана `Movie` класса. Ошибки применяются (с использованием JavaScript) на стороне клиента и стороне сервера (если у пользователя есть JavaScript отключена).

Реальное преимущество имеет нет необходимости ни одной строки кода в `MoviesController` класса или в *Create.cshtml* представления для включения проверки пользовательского интерфейса. Контроллер и представления, созданные ранее в этом учебнике, автоматически менеджера правил проверки, которые указаны с помощью атрибутов на `Movie` класс модели.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>О том, как проверка происходит в создания, просмотра и создания метода действия

Вам может быть интересно, как пользовательский интерфейс проверки создается без обновления кода контроллера или представлений. Далее показан что `Create` методы в `MovieController` класса, как будет выглядеть. Они отличается от способа их создания ранее в этом учебнике.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

Первый метод действия отображает начальной Создание формы. Вторая обрабатывает формы post. Второй `Create` вызовы метода `ModelState.IsValid` , чтобы проверить, имеет ли фильма ошибок проверки. При вызове этого метода оцениваются все атрибуты проверки, которые были применены к объекту. Если объект имеет ошибки проверки `Create` метод повторно отображает форму. Если ошибок нет, метод сохраняет новый фильм в базе данных.

Ниже приведен *Create.cshtml* представление шаблон, который вы формирования шаблонов ранее в этом учебнике. Он используется в показанных выше методах действия для отображения исходной формы и повторного вывода формы в случае ошибки.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

Обратите внимание на то, как код использует `Html.EditorFor` вспомогательный метод для вывода `<input>` для каждого элемента `Movie` свойство. Рядом с этого вспомогательного объекта представляет собой вызов `Html.ValidationMessageFor` вспомогательный метод. Эти два вспомогательных метода работы с объект модели, который передается по контроллера в представление (в этом случае `Movie` объекта). Они автоматически выполняют поиск проверки атрибутов, указанных в модели отображения сообщения об ошибках и соответствующим образом.

Что очень удобно об этом подходе является, что контроллер ни Просмотр шаблона создать знает ничего о применяются правила проверки или отображаются сообщения об ошибках. Правила проверки и строки ошибок указываются только в классе `Movie`.

Если вы хотите изменить логику проверки позже, это можно сделать только в одном месте. Вам не придется беспокоиться о несогласованности применения правил в различных частях приложения, поскольку вся логика проверки будет определена в одном месте и начнет применяться по всему приложению. Это позволяет максимально оптимизировать код и обеспечить удобство его совершенствования и поддержки. А это означает, что вы будете полностью учитывая ТОНЕРА принцип.

## <a name="adding-formatting-to-the-movie-model"></a>Добавление форматирования к модели фильма

Откройте файл *Movie.cs*. [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) Пространство имен содержит атрибуты форматирования помимо встроенный набор атрибутов проверки. Примените [ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) атрибута и [ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) значение перечисления для даты выпуска и поля цены. В следующем коде показано `ReleaseDate` и `Price` свойства с помощью соответствующих [ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) атрибута.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

Кроме того, можно явно задать [ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx) значение. В следующем коде показано свойство даты выпуска с помощью строки формата даты (а именно, «d»). Это будет использовать для указания, что вы не хотите времени как часть даты выпуска.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

В следующем примере кода форматы `Price` свойство в денежном формате.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

Полный `Movie` класса приведен ниже.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

Запустите приложение и перейдите к `Movies` контроллера.

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

В следующей части этой серии мы рассмотрим приложение и внесем ряд изменений в автоматически создаваемые методы `Details` и `Delete`.

>[!div class="step-by-step"]
[Назад](adding-a-new-field.md)
[Вперед](improving-the-details-and-delete-methods.md)
