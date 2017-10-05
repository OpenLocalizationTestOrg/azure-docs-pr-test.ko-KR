---
title: "REST를 사용하여 미디어 프로세서 인스턴스를 가져오는 방법 | Microsoft Docs"
description: "Azure 미디어 서비스용 미디어 콘텐츠를 인코딩하거나 형식을 변환하거나 암호화하거나 암호 해독하기 위한 미디어 프로세서 구성 요소를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4ad90ad979c5bd74fc55155098c88d5c13cb12e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="426ac-103">미디어 프로세서 인스턴스를 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="426ac-103">How to get a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="426ac-104">.NET</span><span class="sxs-lookup"><span data-stu-id="426ac-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="426ac-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="426ac-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="426ac-106">개요</span><span class="sxs-lookup"><span data-stu-id="426ac-106">Overview</span></span>
<span data-ttu-id="426ac-107">미디어 서비스에서 미디어 프로세서는 미디어 콘텐츠 인코딩, 형식 변환, 암호화 또는 암호 해독과 같은 특정 처리 작업을 다루는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="426ac-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="426ac-108">일반적으로 미디어 콘텐츠 인코드, 암호화 또는 형식 변환 작업을 만들 때 미디어 프로세서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="426ac-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="426ac-109">Azure 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="426ac-109">Azure media processors</span></span> 

<span data-ttu-id="426ac-110">미디어 프로세스 목록은 다음 항목에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="426ac-110">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="426ac-111">인코딩 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="426ac-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="426ac-112">분석 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="426ac-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="426ac-113">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="426ac-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="426ac-114">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="426ac-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="426ac-115">미디어 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="426ac-115">Connect to Media Services</span></span>

<span data-ttu-id="426ac-116">AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="426ac-116">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="426ac-117">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="426ac-117">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="426ac-118">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="426ac-118">You must make subsequent calls to the new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="426ac-119">미디어 프로세서 가져오기</span><span class="sxs-lookup"><span data-stu-id="426ac-119">Get a media processor</span></span>

<span data-ttu-id="426ac-120">다음 REST 호출에서는 이름으로 미디어 프로세서 인스턴스를 가져오는 방법을 보여 줍니다(이 경우 **미디어 인코더 표준**).</span><span class="sxs-lookup"><span data-stu-id="426ac-120">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="426ac-121">요청:</span><span class="sxs-lookup"><span data-stu-id="426ac-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="426ac-122">응답:</span><span class="sxs-lookup"><span data-stu-id="426ac-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="426ac-123">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="426ac-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="426ac-124">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="426ac-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="426ac-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="426ac-125">Next Steps</span></span>
<span data-ttu-id="426ac-126">미디어 프로세서 인스턴스를 가져오는 방법을 알아보았으므로 이제 Media Encoder Standard를 사용하여 자산을 인코딩하는 방법을 보여 주는 [자산을 인코딩하는 방법](media-services-rest-get-started.md) 토픽으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="426ac-126">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

