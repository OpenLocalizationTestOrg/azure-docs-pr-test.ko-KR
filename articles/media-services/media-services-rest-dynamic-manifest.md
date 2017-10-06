---
title: "Azure 미디어 서비스 REST API를 사용 하 여 aaaCreating 필터 | Microsoft Docs"
description: "이 항목에서는 클라이언트 toostream 스트림의 특정 섹션 사용할 수 있도록 toocreate 필터링 하는 방법을 설명 합니다. 미디어 서비스 스트리밍이 선택적 tooachieve를 동적 매니페스트를 만듭니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="5e15d-104">Azure 미디어 서비스 REST API로 필터 생성</span><span class="sxs-lookup"><span data-stu-id="5e15d-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e15d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5e15d-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="5e15d-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="5e15d-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="5e15d-107">2.11 버전부터 미디어 서비스를 사용 하면 자산에 대 한 toodefine 필터.</span><span class="sxs-lookup"><span data-stu-id="5e15d-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="5e15d-108">이러한 필터는 고객에 게 toochoose toodo 등으로 나눌 수 있는 서버 쪽 규칙: 재생 (재생 하지 않고 hello 전체 비디오), 비디오의 섹션만 고객의 장치 (처리할 수 있도록 하는 오디오 및 비디오 변환의 하위 집합을 지정 하거나 모든 hello 변환 하는 대신 연결 된 hello 자산에).</span><span class="sxs-lookup"><span data-stu-id="5e15d-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="5e15d-109">자산의 필터링이 통해 보관 **동적 매니페스트**비디오 고객의 요청 toostream 시 생성 되는 지정 된 필터에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="5e15d-110">자세한 내용을 보려면 관련된 toofilters 및 동적 매니페스트 참조 [동적 매니페스트 개요](media-services-dynamic-manifest-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="5e15d-111">이 항목에서는 toouse REST Api toocreate이, 업데이트 하 고 필터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="5e15d-112">Toocreate 필터를 사용 하는 형식</span><span class="sxs-lookup"><span data-stu-id="5e15d-112">Types used toocreate filters</span></span>
<span data-ttu-id="5e15d-113">hello 다음 유형은 사용할 필터를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="5e15d-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="5e15d-114">Filter</span><span class="sxs-lookup"><span data-stu-id="5e15d-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="5e15d-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="5e15d-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="5e15d-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="5e15d-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="5e15d-117">FilterTrackSelect 및 FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="5e15d-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="5e15d-118">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="5e15d-119">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e15d-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="5e15d-120">TooMedia 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="5e15d-120">Connect tooMedia Services</span></span>

<span data-ttu-id="5e15d-121">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="5e15d-122">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="5e15d-123">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="5e15d-124">필터 생성</span><span class="sxs-lookup"><span data-stu-id="5e15d-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="5e15d-125">전역 Filter 생성</span><span class="sxs-lookup"><span data-stu-id="5e15d-125">Create global Filters</span></span>
<span data-ttu-id="5e15d-126">필터를 글로벌 필터로 toocreate HTTP 요청을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="5e15d-127">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-127">HTTP Request</span></span>
<span data-ttu-id="5e15d-128">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="5e15d-128">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="5e15d-129">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5e15d-129">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="5e15d-130">HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="5e15d-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="5e15d-131">로컬 AssetFilter 생성</span><span class="sxs-lookup"><span data-stu-id="5e15d-131">Create local AssetFilters</span></span>
<span data-ttu-id="5e15d-132">로컬 AssetFilter toocreate HTTP 요청을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="5e15d-133">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-133">HTTP Request</span></span>
<span data-ttu-id="5e15d-134">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="5e15d-134">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="5e15d-135">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5e15d-135">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="5e15d-136">HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="5e15d-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="5e15d-137">필터 나열</span><span class="sxs-lookup"><span data-stu-id="5e15d-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="5e15d-138">모든 전역 가져오기 **필터**hello AMS 계정에서 s</span><span class="sxs-lookup"><span data-stu-id="5e15d-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="5e15d-139">toolist 필터 HTTP 요청을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="5e15d-140">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="5e15d-141">자산에 연결된 **AssetFilter**가져오기</span><span class="sxs-lookup"><span data-stu-id="5e15d-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="5e15d-142">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="5e15d-143">해당 ID에 따라 **AssetFilter** 가져오기</span><span class="sxs-lookup"><span data-stu-id="5e15d-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="5e15d-144">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="5e15d-145">필터 업데이트</span><span class="sxs-lookup"><span data-stu-id="5e15d-145">Update filters</span></span>
<span data-ttu-id="5e15d-146">사용 하 여 PATCH, PUT 또는 MERGE tooupdate 새 속성 값을 사용 하 여 필터를 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="5e15d-147">이 작업에 대한 자세한 내용은 [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5e15d-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="5e15d-148">필터를 업데이트 하는 경우 스트리밍 끝점 toorefresh hello 규칙에 대 일 분까지 걸릴 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="5e15d-149">Hello 콘텐츠가이 필터를 사용 하 여 제공 된 (그리고 캐시 프록시 및 CDN에 캐시 된) 하는 경우 플레이어에서 오류가 발생할 수 있습니다이 필터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="5e15d-150">되기 tooclear hello 캐시 hello 필터를 업데이트 한 후 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="5e15d-151">이 옵션을 사용할 수 없는 경우에 서로 다른 필터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="5e15d-152">전역 Filter 업데이트</span><span class="sxs-lookup"><span data-stu-id="5e15d-152">Update global Filters</span></span>
<span data-ttu-id="5e15d-153">필터를 글로벌 필터로 tooupdate HTTP 요청을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="5e15d-154">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-154">HTTP Request</span></span>
<span data-ttu-id="5e15d-155">헤더 요청:</span><span class="sxs-lookup"><span data-stu-id="5e15d-155">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="5e15d-156">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="5e15d-156">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="5e15d-157">로컬 AssetFilter 업데이트</span><span class="sxs-lookup"><span data-stu-id="5e15d-157">Update local AssetFilters</span></span>
<span data-ttu-id="5e15d-158">로컬 필터 tooupdate HTTP 요청을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="5e15d-159">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-159">HTTP Request</span></span>
<span data-ttu-id="5e15d-160">헤더 요청:</span><span class="sxs-lookup"><span data-stu-id="5e15d-160">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="5e15d-161">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="5e15d-161">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="5e15d-162">필터 삭제</span><span class="sxs-lookup"><span data-stu-id="5e15d-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="5e15d-163">전역 Filter 삭제</span><span class="sxs-lookup"><span data-stu-id="5e15d-163">Delete global Filters</span></span>
<span data-ttu-id="5e15d-164">필터를 글로벌 필터로 toodelete HTTP 요청을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="5e15d-165">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="5e15d-166">로컬 AssetFilter 삭제</span><span class="sxs-lookup"><span data-stu-id="5e15d-166">Delete local AssetFilters</span></span>
<span data-ttu-id="5e15d-167">로컬 AssetFilter toodelete HTTP 요청을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="5e15d-168">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="5e15d-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="5e15d-169">필터를 사용하는 스트리밍 URL 작성</span><span class="sxs-lookup"><span data-stu-id="5e15d-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="5e15d-170">Toopublish 및 배달 자산을 확인 하려면 어떻게 해야에 대 한 내용은 [콘텐츠 배달 tooCustomers 개요](media-services-deliver-content-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e15d-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="5e15d-171">hello 다음 예제에서는 tooadd tooyour 스트리밍 Url을 필터링 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5e15d-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="5e15d-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="5e15d-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="5e15d-173">**Apple HLS(HTTP 라이브 스트리밍) V4**</span><span class="sxs-lookup"><span data-stu-id="5e15d-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="5e15d-174">**Apple HLS(HTTP 라이브 스트리밍) V3**</span><span class="sxs-lookup"><span data-stu-id="5e15d-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="5e15d-175">**부드러운 스트리밍**</span><span class="sxs-lookup"><span data-stu-id="5e15d-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="5e15d-176">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="5e15d-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5e15d-177">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="5e15d-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="5e15d-178">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5e15d-178">See Also</span></span>
[<span data-ttu-id="5e15d-179">동적 매니페스트 개요</span><span class="sxs-lookup"><span data-stu-id="5e15d-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

