---
title: "REST API를 사용하여 Azure Mobile Engagement 서비스 API에 액세스"
description: "Mobile Engagement REST API를 사용하여 Azure Mobile Engagement 서비스 API에 액세스하는 방법 설명"
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
ms.openlocfilehash: 4b21bca6fee7012ce1dba96950ae075eded414f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="using-rest-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="f7f38-103">REST를 사용하여 Azure Mobile Engagement 서비스 API에 액세스</span><span class="sxs-lookup"><span data-stu-id="f7f38-103">Using REST to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="f7f38-104">Azure Mobile Engagement는 장치, 도달률/푸시 캠페인 등을 관리할 수 있는 [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-104">Azure Mobile Engagement provides the [Azure Mobile Engagement REST API](https://msdn.microsoft.com/library/azure/mt683754.aspx) for you to manage Devices, Reach/Push campaigns etc.</span></span>

> [!NOTE]
> <span data-ttu-id="f7f38-105">Azure Mobile Engagement 서비스는 2018년 3월에 사용 중지되며 현재 기존 고객에게만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="f7f38-106">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="f7f38-107">REST API를 직접 사용하지 않으려는 분들을 위해, 기본 설정 언어에 대한 SDK를 생성하는 도구와 함께 사용할 수 있는 [Swagger 파일](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json)을 제공해 드립니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-107">If you do not want to use the REST APIs directly, we also provide a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="f7f38-108">Swagger 파일에서 SDK를 생성하는 [AutoRest](https://github.com/Azure/AutoRest) 도구를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-108">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span> <span data-ttu-id="f7f38-109">C# 래퍼를 사용하여 이러한 API와 상호 작용할 수 있는 유사한 방식으로 .NET SDK를 만들었으며 인증 토큰 협상을 수행하거나 새로 고칠 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-109">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span> <span data-ttu-id="f7f38-110">API에 대한 .net SDK를 사용하는 방법을 알아보려면 [서비스 API .NET SDK 샘플](mobile-engagement-dotnet-sdk-service-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-110">See [Service API .NET SDK Sample](mobile-engagement-dotnet-sdk-service-api.md) to learn how to use the .net SDK for API</span></span>
