---
title: "Хэширование пароля"
author: rick-anderson
description: "В этом документе объясняется, как для хэширования паролей с помощью интерфейсов API защиты данных ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/password-hashing
ms.openlocfilehash: e97d17b5f6de2e0ddcde6d51618675388b43911a
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="password-hashing"></a><span data-ttu-id="ba120-103">Хэширование пароля</span><span class="sxs-lookup"><span data-stu-id="ba120-103">Password Hashing</span></span>

<span data-ttu-id="ba120-104">База данных защиты кода включает пакет *Microsoft.AspNetCore.Cryptography.KeyDerivation* которого содержит функции шифрования ключа с наследованием.</span><span class="sxs-lookup"><span data-stu-id="ba120-104">The data protection code base includes a package *Microsoft.AspNetCore.Cryptography.KeyDerivation* which contains cryptographic key derivation functions.</span></span> <span data-ttu-id="ba120-105">Данный пакет представляет собой изолированный компонент и не имеет зависимостей от остальной системой защиты данных.</span><span class="sxs-lookup"><span data-stu-id="ba120-105">This package is a standalone component and has no dependencies on the rest of the data protection system.</span></span> <span data-ttu-id="ba120-106">Его можно использовать совершенно независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="ba120-106">It can be used completely independently.</span></span> <span data-ttu-id="ba120-107">Наряду с кодом защиты данных, базовый для удобства существует источник.</span><span class="sxs-lookup"><span data-stu-id="ba120-107">The source exists alongside the data protection code base as a convenience.</span></span>

<span data-ttu-id="ba120-108">Пакет сейчас предоставляет метод `KeyDerivation.Pbkdf2` разрешающее хэширования пароля с помощью [PBKDF2 алгоритм](https://tools.ietf.org/html/rfc2898#section-5.2).</span><span class="sxs-lookup"><span data-stu-id="ba120-108">The package currently offers a method `KeyDerivation.Pbkdf2` which allows hashing a password using the [PBKDF2 algorithm](https://tools.ietf.org/html/rfc2898#section-5.2).</span></span> <span data-ttu-id="ba120-109">Этот API очень похожа на .NET Framework существующие [Rfc2898DeriveBytes тип](https://docs.microsoft.com/dotnet/api/system.security.cryptography.rfc2898derivebytes), но имеются три важные различия:</span><span class="sxs-lookup"><span data-stu-id="ba120-109">This API is very similar to the .NET Framework's existing [Rfc2898DeriveBytes type](https://docs.microsoft.com/dotnet/api/system.security.cryptography.rfc2898derivebytes), but there are three important distinctions:</span></span>

1. <span data-ttu-id="ba120-110">`KeyDerivation.Pbkdf2` Метод поддерживает использование нескольких PRFs (в настоящее время `HMACSHA1`, `HMACSHA256`, и `HMACSHA512`), тогда как `Rfc2898DeriveBytes` поддерживает только тип `HMACSHA1`.</span><span class="sxs-lookup"><span data-stu-id="ba120-110">The `KeyDerivation.Pbkdf2` method supports consuming multiple PRFs (currently `HMACSHA1`, `HMACSHA256`, and `HMACSHA512`), whereas the `Rfc2898DeriveBytes` type only supports `HMACSHA1`.</span></span>

2. <span data-ttu-id="ba120-111">`KeyDerivation.Pbkdf2` Метод обнаруживает текущей операционной системы и пытается выбирать наиболее оптимизированная реализация процедуру, предоставляя гораздо более высокую производительность в определенных случаях.</span><span class="sxs-lookup"><span data-stu-id="ba120-111">The `KeyDerivation.Pbkdf2` method detects the current operating system and attempts to choose the most optimized implementation of the routine, providing much better performance in certain cases.</span></span> <span data-ttu-id="ba120-112">(В Windows 8 предлагает около 10 x пропускную способность `Rfc2898DeriveBytes`.)</span><span class="sxs-lookup"><span data-stu-id="ba120-112">(On Windows 8, it offers around 10x the throughput of `Rfc2898DeriveBytes`.)</span></span>

3. <span data-ttu-id="ba120-113">`KeyDerivation.Pbkdf2` Метод требует указать все параметры (хэшу, PRF и число итераций).</span><span class="sxs-lookup"><span data-stu-id="ba120-113">The `KeyDerivation.Pbkdf2` method requires the caller to specify all parameters (salt, PRF, and iteration count).</span></span> <span data-ttu-id="ba120-114">`Rfc2898DeriveBytes` Тип предоставляет значения по умолчанию для этих.</span><span class="sxs-lookup"><span data-stu-id="ba120-114">The `Rfc2898DeriveBytes` type provides default values for these.</span></span>

[!code-csharp[Main](password-hashing/samples/passwordhasher.cs)]

<span data-ttu-id="ba120-115">См. исходный код для ASP.NET Core удостоверения `PasswordHasher` вариант использования тип для реального мира.</span><span class="sxs-lookup"><span data-stu-id="ba120-115">See the source code for ASP.NET Core Identity's `PasswordHasher` type for a real-world use case.</span></span>