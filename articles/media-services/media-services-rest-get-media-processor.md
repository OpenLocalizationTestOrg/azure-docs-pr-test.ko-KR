---
title: "aaa 방법을 사용 하 여 미디어 프로세서 인스턴스 tooget 놓으면 | Microsoft Docs"
description: "미디어 프로세서 구성 요소 tooencode toocreate를 형식으로 변환, 암호화 또는 Azure 미디어 서비스에 대 한 미디어 콘텐츠를 암호 해독 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="467d5-103">어떻게 tooget 미디어 프로세서 인스턴스</span><span class="sxs-lookup"><span data-stu-id="467d5-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="467d5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="467d5-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="467d5-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="467d5-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="467d5-106">개요</span><span class="sxs-lookup"><span data-stu-id="467d5-106">Overview</span></span>
<span data-ttu-id="467d5-107">미디어 서비스에서 미디어 프로세서는 미디어 콘텐츠 인코딩, 형식 변환, 암호화 또는 암호 해독과 같은 특정 처리 작업을 다루는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="467d5-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="467d5-108">일반적으로 미디어 프로세서 작업 tooencode를 만들 때, encrypt, 만들거나 미디어 콘텐츠 hello 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="467d5-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="467d5-109">Azure 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="467d5-109">Azure media processors</span></span> 

<span data-ttu-id="467d5-110">hello 항목에서는 미디어 프로세서의 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="467d5-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="467d5-111">인코딩 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="467d5-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="467d5-112">분석 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="467d5-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="467d5-113">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="467d5-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="467d5-114">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="467d5-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="467d5-115">TooMedia 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="467d5-115">Connect tooMedia Services</span></span>

<span data-ttu-id="467d5-116">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="467d5-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="467d5-117">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="467d5-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="467d5-118">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="467d5-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="467d5-119">미디어 프로세서 가져오기</span><span class="sxs-lookup"><span data-stu-id="467d5-119">Get a media processor</span></span>

<span data-ttu-id="467d5-120">REST 호출 다음 hello 이름별 tooget 미디어 프로세서 인스턴스 하는 방법을 보여 줍니다 (이 경우 **미디어 인코더 표준**).</span><span class="sxs-lookup"><span data-stu-id="467d5-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="467d5-121">요청:</span><span class="sxs-lookup"><span data-stu-id="467d5-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="467d5-122">응답:</span><span class="sxs-lookup"><span data-stu-id="467d5-122">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="467d5-123">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="467d5-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="467d5-124">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="467d5-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="467d5-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="467d5-125">Next Steps</span></span>
<span data-ttu-id="467d5-126">배웠으므로 tooget 미디어 프로세서 인스턴스를 이동 하는 방법을 toohello [어떻게 tooEncode 자산](media-services-rest-get-started.md) 항목 어떻게 toouse hello 미디어 인코더 표준 tooencode 자산을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="467d5-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

