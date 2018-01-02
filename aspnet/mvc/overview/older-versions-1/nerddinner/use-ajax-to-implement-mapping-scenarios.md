---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: "Использование AJAX для реализации сценариев сопоставления | Документы Microsoft"
author: microsoft
description: "Шаг 11 показывает, как интегрировать поддержку сопоставления AJAX в приложении обновление NerdDinner Включение пользователей, создание, изменение или просмотр ужинов, чтобы увидеть l..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: cc55560ce691826b6d52971b16d0515ed73d72a6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="use-ajax-to-implement-mapping-scenarios"></a>Позволяет реализовать сопоставление сценариев AJAX
====================
по [Microsoft](https://github.com/microsoft)

[Скачать PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Это шаг 11 бесплатных [учебника «Обновление NerdDinner» приложения](introducing-the-nerddinner-tutorial.md) , обходов сквозной как построить небольшой, но завершается веб-приложения с помощью ASP.NET MVC 1.
> 
> Шаг 11 показано, как интегрировать поддержку сопоставления AJAX в приложении обновление NerdDinner Включение пользователей создание, изменение или просмотр ужинов графически получить расположение компании dinner.
> 
> При использовании ASP.NET MVC 3, которому рекомендуется следовать [Приступая к работе с MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) или [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) учебники.


## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>Обновление NerdDinner шаг 11: Интеграция карты AJAX

Будет сделан наше приложение немного более визуальной интересных интегрируя поддержку сопоставления AJAX. Это позволит пользователей создание, изменение или просмотр ужинов графически получить расположение компании dinner.

### <a name="creating-a-map-partial-view"></a>Создание частичного представления карты

Мы будем использовать функциональные возможности сопоставления в нескольких местах в приложении. Наш код ПРОБНОГО мы будем инкапсулируют общие функции карты, в рамках одного частичного шаблона, можно повторно использовать в нескольких действий контроллеров и представлений. Мы будем назовите это частичное представление «map.ascx» и создайте его в каталоге \Views\Dinners.

Можно создать map.ascx частичного, щелкнув правой кнопкой мыши каталог \Views\Dinners и выбрав команду Add -&gt;просмотреть команды меню. Мы будем имя представления «Map.ascx», верните его в качестве частичного представления и указывают, что мы собираемся передать его класс модели в строго типизированных «Dinner»:

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

При нажатии кнопки «Добавить» наш частичного шаблона будет создана. Затем мы сообщим Map.ascx файл имеет следующее содержимое:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

Первый &lt;сценарий&gt; ссылок, в библиотеке Microsoft виртуального Земли 6.2 сопоставления. Второй &lt;сценарий&gt; ссылок, в файл map.js, скоро будут созданы, который будет инкапсулироваться нашей общую логику сопоставления Javascript. &lt;Div id = «theMap»&gt; элемент — это контейнер HTML, который будет использовать Virtual Earth для размещения на карте.

Мы получаем встроенный &lt;сценарий&gt; блока, содержащего два функции JavaScript, относящиеся к этому представлению. Первая функция используется jQuery в функцию, которая выполняется, когда страница готова для выполнения сценария на стороне клиента доступ к сети. Вызывает вспомогательную функцию LoadMap(), мы определим в нашем Map.js файла сценария управления картой virtual earth. Вторая функция имеет обработчик события обратного вызова, который добавляет ПИН-кода на карту, определяющий расположение.

Обратите внимание на то, как мы используем серверного &lt;% = %&gt; блок внутри блока клиентского скрипта для внедрения широту и долготу Dinner, требуется сопоставить в JavaScript. Эта методика полезна для вывода динамические значения, которые могут использоваться клиентский сценарий (не требуя отдельный вызов AJAX на сервер для извлечения значений — ускоряющую). &lt;% = %&gt; Блоки будет выполняться при подготовке к просмотру представления на сервере — и поэтому выходные данные HTML так же остановится при достижении значения внутри JavaScript (например: широта var = 47.64312;).

### <a name="creating-a-mapjs-utility-library"></a>Создание библиотеки Map.js программы

Теперь создадим Map.js файл, который можно использовать для инкапсуляции функции JavaScript для нашей карты (и реализуют LoadMap и LoadPin выше). Мы это сделать, щелкнув правой кнопкой мыши каталог \Scripts в данном проекте, а затем выберите «Добавить -&gt;новый элемент» команду меню, выберите элемент JScript и назовите его «Map.js».

Ниже приведен код JavaScript, мы добавим Map.js файл, который будет взаимодействовать с виртуальной землей для отображения нашей карты и добавить его расположения ПИН-коды для наших ужинов:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>Интеграция карты со Создание и изменение формы

Мы будем теперь интегрировать поддержки карт нашей существующих сценариев создания и редактирования. Хорошо то, что это довольно просто дел и не требует мы изменили наш код контроллера. Поскольку наш Создание и изменение представления используют общие частичного представления «DinnerForm» для реализации пользовательского интерфейса формы компании dinner, мы добавления карты в одном месте и иметь оба наших Создание и редактирование сценария использования.

Все, что нам нужно задача — открыть \Views\Dinners\DinnerForm.ascx частичного представления и обновить его, чтобы включить частичные нашей новой карты. Ниже приведен обновленные DinnerForm будет выглядеть после добавления карты (Примечание: из приведенного ниже фрагмента кода для краткости опущены элементы HTML-формы):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

Частичное выше DinnerForm принимает объект типа «DinnerFormViewModel» как тип модели (так как он должен, как объект Dinner, так и SelectList для заполнения dropdownlist стран). Наш частичного карты требуется только объект типа «Dinner» как тип модели, и поэтому когда мы подготовки карты к просмотру частичного мы передаем только Dinner вложенное свойство DinnerFormViewModel к нему:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

Функция JavaScript, которая мы добавили jQuery частичного используется для присоединения событий «Размытие» в текстовом поле «Адрес» HTML. Возможно, вы уже слышали о «фокус» событий, которые срабатывают при нажатии пользователем или вкладок в текстовое поле. Событие «Размытие», которое вызывается, когда пользователь выходит из текстового поля верно обратное. Выше обработчик события очищает текстовое поле значения широты и долготы, когда это происходит, а затем нажмите на новое место адрес в нашей карты. Обработчик события обратного вызова, которое было определено в файле map.js обновляют широты и долготы текстовые поля в форме с помощью значений, возвращаемых виртуальной землей, исходя из адреса, которые мы ей было присвоено.

Затем теперь мы запуска нашего приложения еще раз и перейдите на вкладку «Dinner узла», мы увидим сопоставления по умолчанию, отображается вместе с нашей стандартных элементов формы компании Dinner:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

Когда мы введите адрес и затем вкладку немедленно, карты будет динамически обновляться для отображения расположения и обработчиком событий будет заполнять текстовые поля широты и долготы расположение значениями:

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

Если сохранить новый dinner и затем откройте его для редактирования, мы увидите, что расположения карты отображается при загрузке страницы:

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

Каждый раз при изменении поля адрес обновит схему и координаты широты и долготы.

Теперь, когда на карте отображается Dinner расположение, можно также изменить поля формы широты и долготы перестанут быть видимыми текстовые поля на следующую скрытых элементов (поскольку карты автоматически обновляет их каждый раз, когда вводился адрес). Задача это мы перейдем из использование вспомогательного метода Html.TextBox() HTML с помощью вспомогательного метода Html.Hidden():

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

И теперь немного более понятны нашей формы и избежать отображение необработанных широты и долготы (сохраняя по-прежнему их с каждой компании Dinner в базе данных):

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>Интеграция карты со представление сведений

Итак, давайте интегрирован с нашими сценариями Создание и изменение карты и интегрировать его с нашей сценарием сведения. Все, что нам нужно задача является вызов &lt;% Html.RenderPartial("map"); %&gt; в представлении подробных сведений.

Ниже приведен исходный код для завершения подробного представления (с помощью интеграции карты) выглядит как:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

И теперь при переходе на /Dinners/подробности / [id] URL-адрес сможете увидеть сведения о компании dinner расположение обед на карте (дополненный закрепляющую что при прохождении курсора над отображает название компании dinner и на адрес), а ссылка AJAX на RSVP fo r его:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>Реализация поиска место в базе данных, а также репозитория

Чтобы завершить создание реализацию AJAX, добавим карту на домашнюю страницу приложения, которое позволяет пользователям искать в графическом виде для ужинов рядом с ними.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Для начала рассмотрим путем реализации поддержки в нашей базу данных и данные репозитория слоя, чтобы эффективно выполнять поиск на основе расположения radius ужинов. Можно использовать новый [геопространственных функций SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) реализовать это, или в качестве альтернативы можно использовать подход функции SQL, который Gary Драйден рассматриваемые в статье здесь: [http://www.codeproject.com/KB/cs/ distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) и Conery Роба писал с помощью с помощью LINQ to SQL здесь: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

Чтобы реализовать этот метод, мы будет откройте «Обозреватель сервера» в среде Visual Studio, выберите базу данных, обновление NerdDinner и щелкните правой кнопкой мыши на подузел «функции», в нем и выберите Создание нового «скалярные функции»:

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

Мы будем вставьте следующую функцию DistanceBetween:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

Затем мы создадим табличной функции в SQL Server, который мы назовем «NearestDinners»:

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

Эта функция таблицы «NearestDinners» использует DistanceBetween вспомогательную функцию для возврата всех ужинов 100 километров от широту и долготу мы используем его:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

Для вызова этой функции, мы сначала открою LINQ to SQL конструктор, дважды щелкнув файл в каталог \Models NerdDinner.dbml:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

Мы будем затем перетащите функции NearestDinners и DistanceBetween LINQ SQL конструктор, который приведет к их для добавления в качестве методов на нашем LINQ к классу SQL NerdDinnerDataContext:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

Мы можно отображать метода «FindByLocation» запроса в класс DinnerRepository, использующей функцию NearestDinner для возврата предстоящих ужинов, 100 километров от указанного расположения:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>Реализация метода действия поиска JSON на основе AJAX

Теперь мы будем реализовывать метод действия контроллера, который использует преимущества нового метода репозитория FindByLocation() возвращения список Dinner данных, который может использоваться для заполнения карты. У нас будет данным методом действия возвращения обратно Dinner данных в формате JSON (JavaScript Object Notation), чтобы его можно легко управлять с помощью JavaScript на стороне клиента.

Чтобы реализовать это, мы создадим новый класс «SearchController», щелкнув правой кнопкой мыши каталог \Controllers и выбрав команду Add -&gt;команда меню контроллера. Затем мы будет реализован метод действия «SearchByLocation» в новый класс SearchController как ниже:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

Метод действия SearchByLocation SearchController внутренним образом вызывает метод FindByLocation DinnerRespository, чтобы получить список близлежащих ужинов. Вместо того чтобы возвращать объекты Dinner непосредственно клиенту, однако вместо этого он возвращает JsonDinner объектов. Класс JsonDinner предоставляет подмножество свойств Dinner (например: оно не раскрывает имена пользователей, которые RSVP'd на обед по причинам безопасности). Он также включает свойство RSVPCount на обед — нет, и динамически которого вычисляется путем подсчета количества RSVP объекты, связанные с определенной dinner.

Мы затем используется вспомогательный метод Json() базового класса контроллера для возвращения последовательности ужинов, с помощью формата JSON на основе передачи. JSON — это стандартный текстовый формат для представления простой структуры данных. Ниже приведен пример того, как при возвращаются из наших метод действия выглядит формате JSON список объектов два JsonDinner:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>Вызов метода JSON на основе AJAX с использованием библиотеки jQuery

Теперь готовы обновить домашнюю страницу обновление NerdDinner приложению использовать метод действия SearchByLocation SearchController. Задача, мы откройте шаблон представления /Views/Home/Index.aspx и обновляйте его в текстовое поле, кнопку поиска, то нашей карты и &lt;div&gt; элемента с именем dinnerList:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

Две функции JavaScript можно добавить на страницу:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

Первая функция JavaScript, которая загружает карту при первой загрузке страницы. Второй проводке функции JavaScript копирование JavaScript нажмите кнопку обработчика событий кнопки search. При нажатии кнопки вызывается функция FindDinnersGivenLocation() JavaScript, который мы добавим в наш файл Map.js:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

Эта функция FindDinnersGivenLocation() вызывает карты. Применения Find() для виртуального управления Земли ее в центре введенное местоположение. Когда виртуальной землей карты служба возвращает, карты. Метод применения Find() вызывает метод обратного вызова callbackUpdateMapDinners мы переданных как последний аргумент.

Метод callbackUpdateMapDinners() является, где выполняется реальной работы. В нем jQuery $.post() вспомогательный метод для выполнения вызовов AJAX к методу действия SearchByLocation() наших SearchController — передачи его широту и долготу вновь по центру карты. Он определяет встроенная функция, которая будет вызываться при завершении вспомогательный метод $.post() и формата JSON dinner результаты, возвращенные из SearchByLocation(), метод действия будут передаваться с помощью переменной с именем «ужинов». Он затем делает foreach по каждой возвращаемой компании dinner, а также использует dinner широты и долготы и другие свойства для добавления нового ПИН-кода на карте. Он также добавляет запись компании dinner список HTML ужинов в правой части карты. Он затем проводов вверх события наведения защелки и список HTML, чтобы при наведении на них отображаются сведения о компании dinner:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

Затем теперь мы запустите приложение и посетите домашнюю страницу, мы будет выведен список с картой. Когда мы ввести название города карты для отображения предстоящих ужинов рядом с ней:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

Наведении указателя мыши на обед отобразит подробные сведения о нем.

Щелкните название компании Dinner или пузырек с правой стороны в списке HTML, произойдет переход нам компании dinner — мы можно затем при необходимости RSVP для:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>Следующий шаг

Теперь мы реализовали все функции приложения обновление NerdDinner приложения. Теперь давайте рассмотрим, как мы можно включить автоматическое модульного тестирования его.

>[!div class="step-by-step"]
[Назад](use-ajax-to-deliver-dynamic-updates.md)
[Вперед](enable-automated-unit-testing.md)