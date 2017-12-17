---
uid: single-page-application/overview/templates/breezeknockout-template
title: "Просто/маскирования шаблона | Документы Microsoft"
author: madskristensen
description: "Шаблон одностраничного приложения просто/маскирования"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/30/2013
ms.topic: article
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 07ec099a0381458fe42c1972a2554f76fd34638c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="breezeknockout-template"></a>Шаблон просто/маскирования
====================
по [Мэдс Kristensen](https://github.com/madskristensen)

> Шаблон MVC просто/маскирования было написано с Ворд колокольчика
> 
> [Загрузите шаблон MVC просто/маскирования](https://go.microsoft.com/fwlink/?LinkId=282649)


Вы уже слышали о «одностраничное приложение» (SPA) может возникнуть вопрос, что это такое. Хотя можно прочитать о нем, а возникнет его самостоятельно. Но у кого есть время, чтобы загрузить пример? Если у вас есть Visual Studio, вы получите пример SPA и запущен в длиной не более 60 секунд с ASP.NET MVC 4 шаблон «Просто/маскирования одностраничного приложения».

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a>Что такое шаблон SPA просто/маскирования

Большинство шаблоны проекта создают основу для приложения. Поместить flesh на этих костей путем добавления кода и обеспечивает рабочее приложение. Шаблон просто/маскирования SPA отличается. Он создает образец приложения, необходимо изучить. Он демонстрирует SPA проектирования приложений и многие из методик по созданию SPA.

Шаблон просто/маскирования похож на [шаблона с использованием KnockoutJS SPA](../introduction/knockoutjs-template.md) включены в ASP.NET и веб-средства 2012.2 обновление. Шаблон SPA просто создает приложение с помощью того же взаимодействие с пользователем, но имеет другую реализацию, с помощью просто для управления данными.

SPA использованием KnockoutJS шаблона делает запросы к службе с необработанные jQuery AJAX, который подходит для простого приложения. Однако более сложные приложения имеют более высокие требования к управлению данными. Например, большинство приложений:

- Запрос и повторного запроса во время сеанса расширенных пользователя.
- Добавьте запрос фильтры, сортировку и разбиение по страницам.
- Общие данные на нескольких экранах.
- Накапливать изменения многих объектов, а затем сохранить их в виде одной транзакции.
- Проверьте изменения на стороне клиента, поэтому пользователя можно исправить ошибки перед фиксацией изменений в базе данных.

Библиотека BreezeJS обрабатывает эти делами, освобождение разработку приложений логики и взаимодействия с пользователем, наиболее важные.

[**Просто** ](http://www.breezejs.com/?utm_source=ms-spa) — это библиотека открытым исходным кодом, для создания сложных данных приложений на языке JavaScript и HTML, типы приложений, которые раньше были доставлены как автономных настольных приложений.

Шаблон просто/маскирования помогут реализовать, первым шагом решающее значение к более надежную инфраструктуру управления данными. Он создает образец приложения Todo, внешне идентичный SPA использованием KnockoutJS шаблон. Внутри он просто заменяет уровень данных AJAX, чтобы можно было сравнить два приближается side-by-side. Конечно он едва соприкасается потенциально просто приложения. Но вы увидите, как просто работает и как немного необходимо, чтобы сделать этот переход.

Итак, начнем.

## <a name="create-a-breezeknockout-template-project"></a>Создание проекта шаблона просто/маскирования

Загрузите и установите шаблон, нажав кнопку «Загрузить» выше. Шаблон упаковывается в виде файла расширения Visual Studio (VSIX). Может потребоваться перезапустить Visual Studio.

В **шаблоны** выберите **установленные шаблоны** и разверните **Visual C#** узла. В разделе **Visual C#**выберите **Web**. В списке шаблонов проектов выберите **веб-приложение ASP.NET MVC 4**. Имя проекта и нажмите кнопку **ОК**.

В **новый проект** мастера выберите **SPA маскирования просто**.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

Нажмите Ctrl + F5, чтобы построить и запустить приложение без отладки, или нажмите клавишу F5 для запуска без отладки.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

При первом запуске приложения оно отображает экран входа. Щелкните ссылку «Регистрация» и glides новую страницу в представлении, где можно ввести имя пользователя и пароль. (Страницы входа и регистрации создаются с помощью ASP.NET MVC.) Для отправки формы регистрации сервера приводит к возникновению ошибки TodoList с двумя элементами для вашей учетной записи. Затем он возвращает их вам желтый заметки.

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

Теперь вы находитесь в Земли SPA. Все, что вы просматриваете и возникают во время обработки Todos к просмотру и управляется на клиенте с помощью Knockout и просто. Исследовать приложения, имени пользователя... но с глаз разработчика. Используйте инструменты разработчика в браузере для записи сетевого трафика. (В Internet Explorer: нажмите клавишу F12, выберите **сети** и нажмите кнопку **начать захват**.) Теперь выполните следующее:

- Добавьте новый элемент Todo.
- Щелкните метку и изменить заголовок элемента Todo
- Установите флажок, чтобы пометить элемент done. Обратите внимание, что текстовое поле отключено, поэтому заголовок больше не является редактируемой.
- Нажмите кнопку «x» справа от метки. Элемент исчезнет и удаляется из базы данных.
- Выберите другой элемент и очистить его название. Вы получите ошибку проверки, что заголовок является обязательным. После небольшой паузы восстанавливается предыдущих заголовка.
- Введите в нелепо длинный заголовок. Вы сможете получить ошибки проверки другой заголовок слишком велика.
- Нажмите кнопку «Добавить Todo List». Новый список появляется слева от приведенного выше списка.
- Воспроизведение с заголовком TodoList, активируя его требуется и проверки длины.
- Щелкните текстовое поле заголовка, чтобы очистить сообщение об ошибке.
- Нажмите кнопку «x» в кружке в правом верхнем углу для удаления TodoList и его todos.

Логика проверки реализуется выполнено клиентского по просто. Атрибуты проверки на классах модели сервера распространяются на клиент и выполняется автоматически, прежде чем клиент подключается к серверу.

Проверьте сетевой трафик. Обратите внимание, что было не обращений к серверу при просто обнаружена ошибка. Каждое допустимое изменение привел к запросу POST на «/ api/Todo/SaveChanges». Просто объединяет изменения и отправляет их вместе в одном запросе контроллера веб-API `SaveChanges` метод. Это отличается от KockoutJS SPA шаблона, который делает PUT, POST и удалять запросы для каждого элемента по отдельности.

## <a name="peek-inside"></a>Показать внутри

У этого приложения стороны клиента и стороне сервера. Стек клиентского состоит из небольшой HTML и сочетание модулей JavaScript приложения (в папке «приложение») плюс сторонних библиотек JavaScript (в папке «Сценарии»).

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

Если изучения SPA использованием KnockoutJS шаблона, это следует очень знакомыми. Обратите внимание на синие прямоугольники. Архитектура пользовательского интерфейса — Model-View-ViewModel (MVVM), в котором мини-приложений HTML представления полностью отделены от поддержки кода представления в модели представления. Система привязки данных (маскирования в данном случае) координирует представление и представление модели, что каждый может выполнять свою работу без глубоких знаний другой.

Модель инкапсулирует данные Todo. Сущности в модели построены просто со свойствами наблюдаемый маскирования, поэтому они могут быть привязаны непосредственно к мини-приложения в представлении. Модель представления запрашивает контекст данных для получения и сохранения модели сущностей. Контекст данных делегируют большую часть работы, чтобы просто.

Серверные стек состоит из некоторых разработчика кода и три библиотеки .NET принцип: веб-API, Entity Framework и Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

Базовая архитектура совпадает с шаблоном KockoutJS SPA. Однако реализация является гораздо проще: DTO были удалены, и большинство данных Entity Framework о делегированных Breeze.NET.

## <a name="next-steps"></a>Дальнейшие действия

Рекомендуется изучить код, по [широко обсуждений](http://www.breezejs.com/spa-template?utm_source=ms-spa) клиента и стеки серверов, просто веб-сайта.

Можно попробовать работа с просто клиентского запроса; Добавление некоторых фильтров и сортировки. Можно добавить дополнительные свойства модели и дополнительные сущности в лучше понять, для разработки SPA начала до конца. Если вы уверены, проектирования, можно разделять работу функций Todo и замените их собственными.

Скоро вы будете готовы к следующему шагу больших: Добавление экранов на стороне клиента и переход между ними. И вы перейдете оставляет этот шаблон SPA включить более полный стек SPA, например [Джон Папа горячей полотенец](https://github.com/johnpapa/HotTowel#readme "горячей полотенец"), который добавляет Durandal просто и маскирования наборе.