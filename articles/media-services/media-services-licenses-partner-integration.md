---
title: "aaaUsing 파트너 toodeliver Widevine 라이선스 tooAzure 미디어 서비스 | Microsoft Docs"
description: "이 문서에서는 Azure 미디어 서비스 (AMS) toodeliver PlayReady와 Widevine DRMs AMS 하 여 동적으로 암호화 된 스트림을 사용 하는 방법을 설명 합니다. 미디어 서비스 PlayReady 라이선스 서버에서 가져온 hello PlayReady 라이선스 및 Widevine 라이선스 castLabs 라이선스 서버에 의해 전달 됩니다."
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
ms.openlocfilehash: 3c18a8a22ced239931dea5385020194bd6d83f28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-partners-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="f7a1e-104">파트너 toodeliver Widevine 라이선스 tooAzure 미디어 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f7a1e-104">Using partners toodeliver Widevine licenses tooAzure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="f7a1e-105">개요</span><span class="sxs-lookup"><span data-stu-id="f7a1e-105">Overview</span></span>
<span data-ttu-id="f7a1e-106">Microsoft Azure 미디어 서비스에서는 toodeliver MPEG DASH hello CENC (Common Encryption) 사양에 따라 암호화 됩니다. Widevine DRM으로 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a1e-106">Microsoft Azure Media Services enables you toodeliver MPEG-DASH protected with Widevine DRM, which is encrypted per hello Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="f7a1e-107">미디어 서비스.NET SDK 버전 3.5.2 hello 부터는 미디어 서비스 있습니다 tooconfigure Widevine 라이선스 템플릿을 통해 하 고 Widevine 라이선스 가져오기.</span><span class="sxs-lookup"><span data-stu-id="f7a1e-107">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="f7a1e-108">Widevine 라이선스를 배달 AMS 파트너 toohelp 다음 hello을 사용할 수 있습니다: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a1e-108">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="f7a1e-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="f7a1e-109">castLabs</span></span>
<span data-ttu-id="f7a1e-110">사용할 수 있습니다 [castLabs](http://castlabs.com/company/partners/azure/) toodeliver Widevine 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a1e-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) toodeliver Widevine licenses.</span></span> <span data-ttu-id="f7a1e-111">자세한 내용은 참조 [castLabs를 사용 하 여 toodeliver DRM tooAzure 미디어 서비스 라이선스](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="f7a1e-111">For more information, see [Using castLabs toodeliver DRM licenses tooAzure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="f7a1e-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="f7a1e-112">Axinom</span></span>
<span data-ttu-id="f7a1e-113">사용할 수 있습니다 [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) toodeliver Widevine 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a1e-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) toodeliver Widevine licenses.</span></span> <span data-ttu-id="f7a1e-114">자세한 내용은 참조 [tooAzure 미디어 서비스 라이선스를 사용 하 여 Axinom toodeliver DRM](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="f7a1e-114">For more information, see [Using Axinom toodeliver DRM licenses tooAzure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f7a1e-115">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="f7a1e-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f7a1e-116">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="f7a1e-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f7a1e-117">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f7a1e-117">See also</span></span>
[<span data-ttu-id="f7a1e-118">PlayReady 및/또는 Widevine 동적 일반 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="f7a1e-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="f7a1e-119">Mingfei의 블로그</span><span class="sxs-lookup"><span data-stu-id="f7a1e-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

