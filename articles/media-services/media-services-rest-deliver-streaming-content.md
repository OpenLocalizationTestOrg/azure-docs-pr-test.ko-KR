---
title: "REST를 사용 하 여 aaaPublish Azure 미디어 서비스 콘텐츠"
description: "자세한 내용은 어떻게 toocreate는 로케이터를 사용 하는 toobuild 스트리밍 URL입니다. hello 코드 REST API를 사용합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: f849e21b3103b9b33bc652e886b2016ea495b19a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="ec29c-104">REST를 사용하여 Azure Media Services 콘텐츠 게시</span><span class="sxs-lookup"><span data-stu-id="ec29c-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec29c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ec29c-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="ec29c-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="ec29c-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="ec29c-107">포털</span><span class="sxs-lookup"><span data-stu-id="ec29c-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ec29c-108">개요</span><span class="sxs-lookup"><span data-stu-id="ec29c-108">Overview</span></span>
<span data-ttu-id="ec29c-109">적응 비트 전송률 MP4 집합은 주문형 스트리밍 로케이터를 만들고 스트리밍 URL을 작성하여 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="ec29c-110">hello [자산 인코딩](media-services-rest-encode-asset.md) 항목을 적응 비트 전송률 MP4 tooencode 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-110">hello [encoding an asset](media-services-rest-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="ec29c-111">콘텐츠가 암호화되어 있는 경우 [이 항목](media-services-rest-configure-asset-delivery-policy.md) 에서 설명하는 대로 자산 배달 정책을 구성한 후에 로케이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="ec29c-112">또한 스트리밍 로케이터 toobuild Url 점진적으로 다운로드할 수 있는 지점 tooMP4 파일을 하는 요청 시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="ec29c-113">이 항목 방법을 보여 줍니다 toocreate OnDemand 스트리밍 로케이터에 주문 toopublish 자산인 부드러운 스트리밍, MPEG DASH 및 HLS 스트리밍 Url을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-113">This topic shows how toocreate an OnDemand streaming locator in order toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="ec29c-114">핫 toobuild 점진적 다운로드 Url도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-114">It also shows hot toobuild progressive download URLs.</span></span>

<span data-ttu-id="ec29c-115">hello [다음](#types) 섹션에서는 hello 해당 값은 사용 되는 열거형 형식 hello REST 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-115">hello [following](#types) section shows hello enum types whose values are used in hello REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="ec29c-116">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ec29c-117">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec29c-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="ec29c-118">TooMedia 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="ec29c-118">Connect tooMedia Services</span></span>

<span data-ttu-id="ec29c-119">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ec29c-120">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ec29c-121">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="ec29c-122">주문형 스트리밍 로케이터 만들기</span><span class="sxs-lookup"><span data-stu-id="ec29c-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="ec29c-123">toocreate hello OnDemand 스트리밍 로케이터를 살펴보고 toodo hello 다음 필요한 Url:</span><span class="sxs-lookup"><span data-stu-id="ec29c-123">toocreate hello OnDemand streaming locator and get URLs you need toodo hello following:</span></span>

1. <span data-ttu-id="ec29c-124">Hello 콘텐츠 암호화 되어 있으면 액세스 정책을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-124">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="ec29c-125">주문형 스트리밍 로케이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="ec29c-126">Toostream 하려는 경우 스트리밍 매니페스트 파일 (.ism) hello 자산에 hello를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-126">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="ec29c-127">Tooprogressively 다운로드 하려는 경우에 hello 자산에서 MP4 파일의 hello 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-127">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span> 
4. <span data-ttu-id="ec29c-128">Url toohello 매니페스트 파일 또는 MP4 파일을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="ec29c-128">Build URLs toohello manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="ec29c-129">쓰기 또는 삭제 권한을 포함하는 AccessPolicy를 사용하여 스트리밍 로케이터를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="ec29c-130">액세스 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="ec29c-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="ec29c-131">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="ec29c-132">Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="ec29c-132">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="ec29c-133">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec29c-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="ec29c-134">요청:</span><span class="sxs-lookup"><span data-stu-id="ec29c-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="ec29c-135">응답:</span><span class="sxs-lookup"><span data-stu-id="ec29c-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="ec29c-136">주문형 스트리밍 로케이터 만들기</span><span class="sxs-lookup"><span data-stu-id="ec29c-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="ec29c-137">지정 된 자산 hello 및 자산 정책에 대 한 hello 로케이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-137">Create hello locator for hello specified asset and asset policy.</span></span>

<span data-ttu-id="ec29c-138">요청:</span><span class="sxs-lookup"><span data-stu-id="ec29c-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="ec29c-139">응답:</span><span class="sxs-lookup"><span data-stu-id="ec29c-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="ec29c-140">스트리밍 URL 작성</span><span class="sxs-lookup"><span data-stu-id="ec29c-140">Build streaming URLs</span></span>
<span data-ttu-id="ec29c-141">사용 하 여 hello **경로** 부드러운 스트리밍, HLS 및 MPEG DASH Url hello 로케이터 toobuild hello hello 만든 후 반환 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-141">Use hello **Path** value returned after hello creation of hello locator toobuild hello Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="ec29c-142">부드러운 스트리밍: **경로** + 매니페스트 파일 이름 + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="ec29c-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="ec29c-143">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="ec29c-144">HLS: **경로** + 매니페스트 파일 이름 + "/ manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="ec29c-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="ec29c-145">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="ec29c-146">DASH: **경로** + 매니페스트 파일 이름 + "/ manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="ec29c-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="ec29c-147">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="ec29c-148">점진적 다운로드 URL 작성</span><span class="sxs-lookup"><span data-stu-id="ec29c-148">Build progressive download URLs</span></span>
<span data-ttu-id="ec29c-149">사용 하 여 hello **경로** hello hello toobuild hello 점진적 다운로드 URL locator 만든 후 반환 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-149">Use hello **Path** value returned after hello creation of hello locator toobuild hello progressive download URL.</span></span>   

<span data-ttu-id="ec29c-150">URL: **경로** + 자산 파일 mp4 이름</span><span class="sxs-lookup"><span data-stu-id="ec29c-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="ec29c-151">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec29c-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="ec29c-152"><a id="types"></a>열거형 형식</span><span class="sxs-lookup"><span data-stu-id="ec29c-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="ec29c-153">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="ec29c-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ec29c-154">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ec29c-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ec29c-155">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ec29c-155">See also</span></span>
[<span data-ttu-id="ec29c-156">Media Services Operations REST API 개요</span><span class="sxs-lookup"><span data-stu-id="ec29c-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="ec29c-157">자산 배달 정책 구성</span><span class="sxs-lookup"><span data-stu-id="ec29c-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

