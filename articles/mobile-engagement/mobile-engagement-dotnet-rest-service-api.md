---
title: "aaaUsing hello REST API tooaccess Azure Mobile Engagement 서비스 Api"
description: "Toouse Mobile Engagement REST Api tooaccess Azure Mobile Engagement 서비스 Api hello 하는 방법을 설명 합니다."
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: e8df4897-55ee-45df-b41e-ff187e3d9d12
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 315761299a42df6f65e81df20e632f9713844b0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-rest-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="58f17-103">REST tooaccess Azure Mobile Engagement 서비스 Api를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="58f17-103">Using REST tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="58f17-104">Azure Mobile Engagement에서는 hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) 있습니다 toomanage 장치에 대 한 Reach/푸시 캠페인 등입니다.</span><span class="sxs-lookup"><span data-stu-id="58f17-104">Azure Mobile Engagement provides hello [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you toomanage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="58f17-105">hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다.</span><span class="sxs-lookup"><span data-stu-id="58f17-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="58f17-106">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58f17-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="58f17-107">또한 제공 하지 않을 경우 toouse hello REST Api 직접,는 [Swagger 파일](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) 원하는 언어에 대 한 toogenerate Sdk 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58f17-107">If you do not want toouse hello REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="58f17-108">Hello를 사용 하는 것이 좋습니다 [AutoRest](https://github.com/Azure/AutoRest) toogenerate 쿼리하여 Swagger 파일에서 SDK 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="58f17-108">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span> <span data-ttu-id="58f17-109">수 있는 toointeract 이러한 Api와 C# 래퍼를 사용 하 여 비슷한 방식으로.NET SDK 만들어져 및 toodo hello 인증 토큰 협상 하 고 사용자가 직접를 새로 고칠 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58f17-109">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="58f17-110">참조 [서비스 API.NET SDK 샘플](mobile-engagement-dotnet-sdk-service-api.md) toolearn toouse.net SDK API에 대 한 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="58f17-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) toolearn how toouse hello .net SDK for API</span></span>
