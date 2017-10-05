---
title: "파트너를 사용하여 Azure Media Services에 Widevine 라이선스 제공 | Microsoft 문서"
description: "이 문서에서는 Azure 미디어 서비스(AMS)를 사용하여 PlayReady와 Widevine DRM이 모두 있는 AMS에서 동적으로 암호화된 스트림을 전달하는 방법을 설명합니다. PlayReady 라이선스는 미디어 서비스 PlayReady 라이선스 서버에서 제공되며 Widevine 라이선스는 castLabs 라이선스 서버에서 제공됩니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 6867e4f910970121df3858516c6bab3114c3c6f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-partners-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="2cbb4-104">파트너를 사용하여 Azure 미디어 서비스에 Widevine 라이선스 제공</span><span class="sxs-lookup"><span data-stu-id="2cbb4-104">Using partners to deliver Widevine licenses to Azure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="2cbb4-105">개요</span><span class="sxs-lookup"><span data-stu-id="2cbb4-105">Overview</span></span>
<span data-ttu-id="2cbb4-106">Microsoft Azure 미디어 서비스를 사용하면 CENC(Common Encryption) 사양에 따라 암호화되는 Widevine DRM으로 보호된 MPEG DASH를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbb4-106">Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="2cbb4-107">미디어 서비스 .NET SDK 버전 3.5.2부터는 미디어 서비스를 사용하여 Widevine 라이선스 템플릿을 구성하고 Widevine 라이선스를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbb4-107">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="2cbb4-108">또한 다음 AMS 파트너를 사용하여 Widevine 라이선스를 배달할 수 있습니다. [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="2cbb4-108">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="2cbb4-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="2cbb4-109">castLabs</span></span>
<span data-ttu-id="2cbb4-110">[castLabs](http://castlabs.com/company/partners/azure/) 를 사용하여 Widevine 라이선스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbb4-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses.</span></span> <span data-ttu-id="2cbb4-111">자세한 내용은 [castLabs를 사용하여 Azure 미디어 서비스에 DRM 라이선스 제공](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="2cbb4-111">For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="2cbb4-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="2cbb4-112">Axinom</span></span>
<span data-ttu-id="2cbb4-113">[Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) 을 사용하여 Widevine 라이선스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cbb4-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) to deliver Widevine licenses.</span></span> <span data-ttu-id="2cbb4-114">자세한 내용은 [Axinom을 사용하여 Azure 미디어 서비스에 DRM 라이선스 제공](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="2cbb4-114">For more information, see [Using Axinom to deliver DRM licenses to Azure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2cbb4-115">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="2cbb4-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2cbb4-116">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="2cbb4-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2cbb4-117">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2cbb4-117">See also</span></span>
[<span data-ttu-id="2cbb4-118">PlayReady 및/또는 Widevine 동적 일반 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="2cbb4-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="2cbb4-119">Mingfei의 블로그</span><span class="sxs-lookup"><span data-stu-id="2cbb4-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

