---
title: "Включение создания QR-код для приложения для проверки подлинности в ASP.NET Core"
author: rick-anderson
description: "Включение создания QR-код для приложения для проверки подлинности в ASP.NET Core"
manager: wpickett
ms.author: riande
ms.date: 09/24/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/identity-enable-qrcodes
ms.openlocfilehash: ae2d8eb938c00a26cf7ffb5f2fff0b9e0d22148b
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/30/2018
---
# <a name="enabling-qr-code-generation-for-authenticator-apps-in-aspnet-core"></a>Включение создания QR-код для приложения для проверки подлинности в ASP.NET Core

Примечание: Этот раздел относится к ASP.NET Core 2.x

ASP.NET Core поставляется с поддержки проверки подлинности приложений для отдельных проверки подлинности. Два фактора проверки подлинности (2FA) приложения для проверки подлинности, с помощью синхронизированного одноразовый пароль алгоритм (TOTP), — это рекомендованный подход для 2FA отрасли. 2FA с помощью TOTP предпочтительнее SMS 2FA. Приложение проверки подлинности предоставляет 6 – 8 цифр, какие пользователи должны ввести после подтверждения свое имя пользователя и пароль. Обычно приложение проверки подлинности устанавливается на смартфоне.

Веб-приложения ASP.NET Core шаблонов поддерживает атрибуты проверки подлинности, но не обеспечивают поддержку создания QRCode. Генераторы QRCode простота установки 2FA. В этом документе подробно рассматривается добавление [QR-код](https://wikipedia.org/wiki/QR_code) поколения на страницу настройки 2FA.

## <a name="adding-qr-codes-to-the-2fa-configuration-page"></a>Добавление на страницу настройки 2FA QR-коды

В этих инструкциях используется *qrcode.js* из репозитория https://davidshimjs.github.io/qrcodejs/.

* Загрузить [библиотека javascript qrcode.js](https://davidshimjs.github.io/qrcodejs/) для `wwwroot\lib` в папке проекта.

* В *Pages\Account\Manage\EnableAuthenticator.cshtml* (страниц Razor) или *Views\Manage\EnableAuthenticator.cshtml* (MVC), найдите `Scripts` в конце файла:

```cshtml
@section Scripts {
    @await Html.PartialAsync("_ValidationScriptsPartial")
}
```

* Обновление `Scripts` раздел, чтобы добавить ссылку на `qrcodejs` библиотеки, добавленные и вызова для создания QR-код. Он должен выглядеть следующим образом:

```cshtml
@section Scripts {
    @await Html.PartialAsync("_ValidationScriptsPartial")

    <script type="text/javascript" src="~/lib/qrcode.js"></script>
    <script type="text/javascript">
        new QRCode(document.getElementById("qrCode"),
            {
                text: "@Html.Raw(Model.AuthenticatorUri)",
                width: 150,
                height: 150
            });
    </script>
}
```

* Удаление абзаца, в которой представлены ссылки на эти инструкции.

Запустите приложение и убедитесь, что сканирование QR-кода и проверить код, который подтверждает средством проверки подлинности.

## <a name="change-the-site-name-in-the-qr-code"></a>Изменение имени узла в QR-кода

Имя узла в QR-кода берется из имени проекта, выбранный при первоначальном создании проекта. Его можно изменить путем поиска `GenerateQrCodeUri(string email, string unformattedKey)` метод в *Pages\Account\Manage\EnableAuthenticator.cshtml.cs* (страниц Razor) файла или *Controllers\ManageController.cs* файла (MVC). 

Код по умолчанию на основе шаблона выглядит следующим образом:

```c#
private string GenerateQrCodeUri(string email, string unformattedKey)
{
    return string.Format(
        AuthenicatorUriFormat,
        _urlEncoder.Encode("Razor Pages"),
        _urlEncoder.Encode(email),
        unformattedKey);
}
```

Второй параметр в вызове `string.Format` — это имя узла, взяты из имя вашего решения. Его можно изменить в любое значение, но он всегда должен быть в кодировке URL-адрес.

## <a name="using-a-different-qr-code-library"></a>С помощью другой библиотекой QR-кода

Библиотека QR-кода можно заменить предпочтительные библиотеки. В HTML `qrCode` библиотека предоставляет элемент, в который можно поместить QR-кода с любой механизм.

Правильно отформатированный URL-адрес для QR-код доступен в:

* `AuthenticatorUri`Свойства модели.
* `data-url`свойство в `qrCodeData` элемент. 

Используйте `@Html.Raw` для доступа к свойству модели в представлении (в противном случае двойным шифрованием амперсанды в URL-адресе и будет пропущен параметр метки QR-код).

## <a name="totp-client-and-server-time-skew"></a>Отклонение по времени клиента и сервера TOTP

Проверка подлинности TOTP зависит от сервера и проверки подлинности устройства, необходимости точного времени. Токены только последние 30 секунд. Если имена входа 2FA TOTP не удается, проверьте время сервера точными и предпочтительно синхронизированные точные службе NTP.
