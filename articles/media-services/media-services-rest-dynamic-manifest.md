---
title: "Azure Media Services REST API로 필터 생성 | Microsoft Docs"
description: "이 항목에서는 클라이언트가 스트림의 특정 섹션을 스트리밍하는 데 사용할 수 있는 필터를 생성하는 방법을 설명합니다. 이 선택적 스트리밍은 미디어 서비스가 동적 매니페스트를 생성하여 이루어집니다."
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
ms.openlocfilehash: 76d2721138668d9f0a908af3fa42840309b068ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="9faed-104">Azure 미디어 서비스 REST API로 필터 생성</span><span class="sxs-lookup"><span data-stu-id="9faed-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9faed-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9faed-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="9faed-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="9faed-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="9faed-107">미디어 서비스 2.11 버전부터 자산에 대한 필터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="9faed-108">이 필터는 고객이 전체 비디오를 재생하는 대신 비디오의 한 섹션만 재생하거나 자산과 연결된 모든 변환 대신 고객의 장치가 처리할 수 있는 오디오 및 비디오 변환의 하위 집합만 지정하는 등을 선택할 수 있도록 하는 서버 측 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="9faed-109">지정한 필터에 따라 비디오를 스트림하는 고객의 요청에 따라 생성된 **동적 매니페스트**를 통해 자산의 필터링이 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="9faed-110">필터 및 동적 매니페스트에 대한 더 자세한 내용은 [동적 매니페스트 개요](media-services-dynamic-manifest-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9faed-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="9faed-111">이 토픽에서는 REST API를 사용하여 필터를 생성, 업데이트 및 삭제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-111">This topic shows how to use REST APIs to create, update, and delete filters.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="9faed-112">필터 생성에 사용되는 형식</span><span class="sxs-lookup"><span data-stu-id="9faed-112">Types used to create filters</span></span>
<span data-ttu-id="9faed-113">필터를 생성할 때는 다음 형식이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-113">The following types are used when creating filters:</span></span>  

* [<span data-ttu-id="9faed-114">Filter</span><span class="sxs-lookup"><span data-stu-id="9faed-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="9faed-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="9faed-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="9faed-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="9faed-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="9faed-117">FilterTrackSelect 및 FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="9faed-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="9faed-118">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="9faed-119">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9faed-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="9faed-120">미디어 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="9faed-120">Connect to Media Services</span></span>

<span data-ttu-id="9faed-121">AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9faed-121">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="9faed-122">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-122">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="9faed-123">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-123">You must make subsequent calls to the new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="9faed-124">필터 생성</span><span class="sxs-lookup"><span data-stu-id="9faed-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="9faed-125">전역 Filter 생성</span><span class="sxs-lookup"><span data-stu-id="9faed-125">Create global Filters</span></span>
<span data-ttu-id="9faed-126">전역 Filter를 만들려면 다음 HTTP 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-126">To create a global Filter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="9faed-127">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-127">HTTP Request</span></span>
<span data-ttu-id="9faed-128">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="9faed-128">Request Headers</span></span>

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

<span data-ttu-id="9faed-129">요청 본문</span><span class="sxs-lookup"><span data-stu-id="9faed-129">Request body</span></span> 

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




#### <a name="http-response"></a><span data-ttu-id="9faed-130">HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="9faed-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="9faed-131">로컬 AssetFilter 생성</span><span class="sxs-lookup"><span data-stu-id="9faed-131">Create local AssetFilters</span></span>
<span data-ttu-id="9faed-132">로컬 AssetFilter를 만들려면 다음 HTTP 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-132">To create a local AssetFilter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="9faed-133">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-133">HTTP Request</span></span>
<span data-ttu-id="9faed-134">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="9faed-134">Request Headers</span></span>

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

<span data-ttu-id="9faed-135">요청 본문</span><span class="sxs-lookup"><span data-stu-id="9faed-135">Request body</span></span> 

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

#### <a name="http-response"></a><span data-ttu-id="9faed-136">HTTP 응답</span><span class="sxs-lookup"><span data-stu-id="9faed-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="9faed-137">필터 나열</span><span class="sxs-lookup"><span data-stu-id="9faed-137">List filters</span></span>
### <a name="get-all-global-filters-in-the-ams-account"></a><span data-ttu-id="9faed-138">AMS 계정의 모든 전역 **Filter**가져오기</span><span class="sxs-lookup"><span data-stu-id="9faed-138">Get all global **Filter**s in the AMS account</span></span>
<span data-ttu-id="9faed-139">필터를 나열하려면 다음 HTTP 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-139">To list filters, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9faed-140">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="9faed-141">자산에 연결된 **AssetFilter**가져오기</span><span class="sxs-lookup"><span data-stu-id="9faed-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="9faed-142">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="9faed-143">해당 ID에 따라 **AssetFilter** 가져오기</span><span class="sxs-lookup"><span data-stu-id="9faed-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="9faed-144">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="9faed-145">필터 업데이트</span><span class="sxs-lookup"><span data-stu-id="9faed-145">Update filters</span></span>
<span data-ttu-id="9faed-146">PATCH, PUT 또는 MERGE를 사용하여 새 속성 값으로 필터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-146">Use PATCH, PUT or MERGE to update a filter with new property values.</span></span>  <span data-ttu-id="9faed-147">이 작업에 대한 자세한 내용은 [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9faed-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="9faed-148">필터를 업데이트 하는 경우, 규칙을 새로고침하는 스트리밍 끝점에 최대 2분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-148">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="9faed-149">콘텐츠가 이 필터로 처리된 경우(및 프록시와 CDN 캐시에서 캐시된 경우) 이 필터를 업데이트하면 플레이어 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-149">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="9faed-150">필터 업데이트 후에는 캐시를 지우는 것이 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-150">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="9faed-151">이 옵션을 사용할 수 없는 경우에 서로 다른 필터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="9faed-152">전역 Filter 업데이트</span><span class="sxs-lookup"><span data-stu-id="9faed-152">Update global Filters</span></span>
<span data-ttu-id="9faed-153">전역 필터를 업데이트하려면 다음 HTTP 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-153">To update a global filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9faed-154">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-154">HTTP Request</span></span>
<span data-ttu-id="9faed-155">헤더 요청:</span><span class="sxs-lookup"><span data-stu-id="9faed-155">Request headers:</span></span> 

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

<span data-ttu-id="9faed-156">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="9faed-156">Request body:</span></span> 

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

### <a name="update-local-assetfilters"></a><span data-ttu-id="9faed-157">로컬 AssetFilter 업데이트</span><span class="sxs-lookup"><span data-stu-id="9faed-157">Update local AssetFilters</span></span>
<span data-ttu-id="9faed-158">로컬 필터를 업데이트하려면 다음 HTTP 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-158">To update a local filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9faed-159">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-159">HTTP Request</span></span>
<span data-ttu-id="9faed-160">헤더 요청:</span><span class="sxs-lookup"><span data-stu-id="9faed-160">Request headers:</span></span> 

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

<span data-ttu-id="9faed-161">본문 요청:</span><span class="sxs-lookup"><span data-stu-id="9faed-161">Request body:</span></span> 

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


## <a name="delete-filters"></a><span data-ttu-id="9faed-162">필터 삭제</span><span class="sxs-lookup"><span data-stu-id="9faed-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="9faed-163">전역 Filter 삭제</span><span class="sxs-lookup"><span data-stu-id="9faed-163">Delete global Filters</span></span>
<span data-ttu-id="9faed-164">전역 Filter를 삭제하려면 다음 HTTP 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-164">To delete a global Filter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="9faed-165">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="9faed-166">로컬 AssetFilter 삭제</span><span class="sxs-lookup"><span data-stu-id="9faed-166">Delete local AssetFilters</span></span>
<span data-ttu-id="9faed-167">로컬 AssetFilter를 삭제하려면 다음 HTTP 요청을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-167">To delete a local AssetFilter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="9faed-168">HTTP 요청</span><span class="sxs-lookup"><span data-stu-id="9faed-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="9faed-169">필터를 사용하는 스트리밍 URL 작성</span><span class="sxs-lookup"><span data-stu-id="9faed-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="9faed-170">자산을 게시하고 제공하는 방법에 대한 자세한 내용은 [고객에 콘텐츠 배달 개요](media-services-deliver-content-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9faed-170">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="9faed-171">다음 예제에서는 스트리밍 URL에 필터를 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9faed-171">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="9faed-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="9faed-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="9faed-173">**Apple HLS(HTTP 라이브 스트리밍) V4**</span><span class="sxs-lookup"><span data-stu-id="9faed-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="9faed-174">**Apple HLS(HTTP 라이브 스트리밍) V3**</span><span class="sxs-lookup"><span data-stu-id="9faed-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="9faed-175">**부드러운 스트리밍**</span><span class="sxs-lookup"><span data-stu-id="9faed-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="9faed-176">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="9faed-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9faed-177">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="9faed-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9faed-178">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9faed-178">See Also</span></span>
[<span data-ttu-id="9faed-179">동적 매니페스트 개요</span><span class="sxs-lookup"><span data-stu-id="9faed-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

