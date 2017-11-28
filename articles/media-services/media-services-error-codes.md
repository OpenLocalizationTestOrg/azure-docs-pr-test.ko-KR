---
title: "Azure Media Services 오류 코드 | Microsoft 문서"
description: "이 항목에서는 Azure Media Services 오류 코드에 대한 개요를 제공합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 39886a955124429302609dd9d5a7c20ae7f498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-media-services-error-codes"></a><span data-ttu-id="3c511-103">Azure Media Services 오류 코드</span><span class="sxs-lookup"><span data-stu-id="3c511-103">Azure Media Services error codes</span></span>
<span data-ttu-id="3c511-104">Microsoft Azure Media Services를 사용할 경우 Media Services에서 지원되지 않는 작업에 대한 인증 토큰 만료와 같은 문제에 따라 서비스에서 HTTP 오류 코드를 받을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-104">When using Microsoft Azure Media Services, you may receive HTTP error codes from the service depending on issues such as authentication tokens expiring to actions that are not supported in Media Services.</span></span> <span data-ttu-id="3c511-105">다음은 Media Services에서 반환되는 **HTTP 오류 코드** 및 가능한 원인의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-105">The following is a list of **HTTP error codes** that may be returned by Media Services and the possible causes for them.</span></span>  

## <a name="400-bad-request"></a><span data-ttu-id="3c511-106">400 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="3c511-106">400 Bad Request</span></span>
<span data-ttu-id="3c511-107">요청에 잘못된 정보가 들어 있으며 다음 이유 중 하나 때문에 요청이 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-107">The request contains invalid information and is rejected due to one of the following reasons:</span></span>

* <span data-ttu-id="3c511-108">지원되지 않는 API 버전이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-108">An unsupported API version is specified.</span></span> <span data-ttu-id="3c511-109">가장 최신 버전은 [Media Services REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c511-109">For the most current version, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="3c511-110">Media Services의 API 버전이 지정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-110">The API version of Media Services is not specified.</span></span> <span data-ttu-id="3c511-111">API 버전을 지정하는 방법에 대한 정보는 [Media Services Operations REST API 참조](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c511-111">For information on how to specify the API version, see [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3c511-112">.NET 또는 Java SDK를 사용하여 Media Services에 연결하는 경우, Media Services에 대해 작업을 수행하려고 할 때마다 API 버전이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-112">If you are using the .NET or Java SDKs to connect to Media Services, the API version is specified for you whenever you try and perform some action against Media Services.</span></span>
  > 
  > 
* <span data-ttu-id="3c511-113">정의되지 않은 속성이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-113">An undefined property has been specified.</span></span> <span data-ttu-id="3c511-114">속성 이름이 오류 메시지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-114">The property name is in the error message.</span></span> <span data-ttu-id="3c511-115">지정된 엔터티의 구성 요소인 속성 만이 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-115">Only those properties that are members of a given entity can be specified.</span></span> <span data-ttu-id="3c511-116">엔터티 및 해당 속성의 목록은 [Azure Media Services REST API 참조](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c511-116">See [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) for a list of entities and their properties.</span></span>
* <span data-ttu-id="3c511-117">잘못된 속성 값이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-117">An invalid property value has been specified.</span></span> <span data-ttu-id="3c511-118">속성 이름이 오류 메시지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-118">The property name is in the error message.</span></span> <span data-ttu-id="3c511-119">유효한 속성 유형 및 해당 값에 대한 이전 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c511-119">See the previous link for valid property types and their values.</span></span>
* <span data-ttu-id="3c511-120">필수 속성 값이 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-120">A property value is missing and is required.</span></span>
* <span data-ttu-id="3c511-121">지정된 URL 일부에 잘못된 값을 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-121">Part of the URL specified contains a bad value.</span></span>
* <span data-ttu-id="3c511-122">WriteOnce 속성을 업데이트하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-122">An attempt was made to update a WriteOnce property.</span></span>
* <span data-ttu-id="3c511-123">지정되지 않았거나 확인할 수 없는 기본 AssetFile을 사용해 입력 자신이 있는 작업을 만들려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-123">An attempt was made to create a Job that has an input Asset with a primary AssetFile that was not specified or could not be determined.</span></span>
* <span data-ttu-id="3c511-124">SAS Locator를 업데이트하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-124">An attempt was made to update a SAS Locator.</span></span> <span data-ttu-id="3c511-125">SAS Locator는 생성 또는 삭제만 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-125">SAS locators can only be created or deleted.</span></span> <span data-ttu-id="3c511-126">스트리밍 로케이터는 업데이트될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-126">Streaming locators can be updated.</span></span> <span data-ttu-id="3c511-127">자세한 내용은 [Locators](https://docs.microsoft.com/rest/api/media/operations/locator)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c511-127">For more information, see [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>
* <span data-ttu-id="3c511-128">지원되지 않는 작업 또는 쿼리가 제출되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-128">An unsupported operation or query was submitted.</span></span>

## <a name="401-unauthorized"></a><span data-ttu-id="3c511-129">401 권한 없음</span><span class="sxs-lookup"><span data-stu-id="3c511-129">401 Unauthorized</span></span>
<span data-ttu-id="3c511-130">요청이 다음과 같은 이유로 (권한이 부여될 수 있기 전에) 인증될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-130">The request could not be authenticated (before it can be authorized) due to one of the following reasons:</span></span>

* <span data-ttu-id="3c511-131">누락된 인증 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-131">Missing authentication header.</span></span>
* <span data-ttu-id="3c511-132">잘못된 인증 헤더 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-132">Bad authentication header value.</span></span>
  * <span data-ttu-id="3c511-133">토큰이 만료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-133">The token has expired.</span></span> 
  * <span data-ttu-id="3c511-134">토큰에 잘못된 서명이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-134">The token contains an invalid signature.</span></span>

## <a name="403-forbidden"></a><span data-ttu-id="3c511-135">403 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3c511-135">403 Forbidden</span></span>
<span data-ttu-id="3c511-136">요청은 다음과 같은 이유로 허용되지않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-136">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="3c511-137">Media Services 계정을 찾을 수 없거나 삭제되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-137">The Media Services account cannot be found or has been deleted.</span></span>
* <span data-ttu-id="3c511-138">Media Services 계정은 비활성화이고 요청 유형은 HTTP GET이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-138">The Media Services account is disabled and the request type is not HTTP GET.</span></span> <span data-ttu-id="3c511-139">서비스 작업은 또한 403 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-139">Service operations will return a 403 response as well.</span></span>
* <span data-ttu-id="3c511-140">인증 토큰에는 사용자의 자격 증명 정보인 AccountName 및/또는 SubscriptionId가 들어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-140">The authentication token does not contain the user’s credential information: AccountName and/or SubscriptionId.</span></span> <span data-ttu-id="3c511-141">Azure Management Portal의 Media Services 계정에 대한 Media Services UI 확장에서 이 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-141">You can find this information in the Media Services UI extension for your Media Services account in the Azure Management Portal.</span></span>
* <span data-ttu-id="3c511-142">리소스를 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-142">The resource cannot be accessed.</span></span>
  
  * <span data-ttu-id="3c511-143">사용자 Media Services 계정에서는 사용할 수 없는 MediaProcessor를 사용하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-143">An attempt was made to use a MediaProcessor that is not available for your Media Services account.</span></span>
  * <span data-ttu-id="3c511-144">Media Services에서 정의한 JobTemplate을 업데이트하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-144">An attempt was made to update a JobTemplate defined by Media Services.</span></span>
  * <span data-ttu-id="3c511-145">일부 다른 Media Services 계정의 로케이터를 덮어쓰기하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-145">An attempt was made to overwrite some other Media Services account's Locator.</span></span>
  * <span data-ttu-id="3c511-146">일부 다른 Media Services 계정의 ContentKey를 덮어쓰기하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-146">An attempt was made to overwrite some other Media Services account's ContentKey.</span></span>
* <span data-ttu-id="3c511-147">Media Services 계정에 대한 서비스 할당량에 도달했기 때문에 리소스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-147">The resource could not be created due to a service quota that was reached for the Media Services account.</span></span> <span data-ttu-id="3c511-148">서비스 할당량에 관한 자세한 내용은 [할당량 및 제한 사항](media-services-quotas-and-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c511-148">For more information on the service quotas, see [Quotas and Limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="404-not-found"></a><span data-ttu-id="3c511-149">404 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="3c511-149">404 Not Found</span></span>
<span data-ttu-id="3c511-150">리소스에 관한 요청은 다음과 같은 이유로 허용되지않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-150">The request is not allowed on a resource due to one of the following reasons:</span></span>

* <span data-ttu-id="3c511-151">존재하지 않는 엔터티를 업데이트하려고 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-151">An attempt was made to update an entity that does not exist.</span></span>
* <span data-ttu-id="3c511-152">존재하지 않는 엔터티를 삭제하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-152">An attempt was made to delete an entity that does not exist.</span></span>
* <span data-ttu-id="3c511-153">존재하지 않는 엔터티에 연결하는 엔터티를 만들려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-153">An attempt was made to create an entity that links to an entity that does not exist.</span></span>
* <span data-ttu-id="3c511-154">존재하지 않는 엔터티를 GET하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-154">An attempt was made to GET an entity that does not exist.</span></span>
* <span data-ttu-id="3c511-155">Media Services 계정과 연결되지 않은 저장소 계정을 지정하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-155">An attempt was made to specify a storage account that is not associated with the Media Services account.</span></span>  

## <a name="409-conflict"></a><span data-ttu-id="3c511-156">409 충돌</span><span class="sxs-lookup"><span data-stu-id="3c511-156">409 Conflict</span></span>
<span data-ttu-id="3c511-157">요청은 다음과 같은 이유로 허용되지않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-157">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="3c511-158">둘 이상의 AssetFile에 Asset 내에서 지정된 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-158">More than one AssetFile has the specified name within the Asset.</span></span>
* <span data-ttu-id="3c511-159">Asset 내에서 두 번째 보조 AssetFile를 만들려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-159">An attempt was made to create a second primary AssetFile within the Asset.</span></span>
* <span data-ttu-id="3c511-160">이미 사용된 지정 Id를 사용하여 ContentKey를 만들려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-160">An attempt was made to create a ContentKey with the specified Id already used.</span></span>
* <span data-ttu-id="3c511-161">이미 사용된 지정 Id를 사용하여 Locator를 만들려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-161">An attempt was made to create a Locator with the specified Id already used.</span></span>
* <span data-ttu-id="3c511-162">둘 이상의 IngestManifestFile에 IngestManifest 내에서 지정된 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-162">More than one IngestManifestFile has the specified name within the IngestManifest.</span></span>
* <span data-ttu-id="3c511-163">두 번째 저장소 암호화 ContentKey를 저장소 암호화된 Asset에 연결하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-163">An attempt was made to link a second storage encryption ContentKey to the storage-encrypted Asset.</span></span>
* <span data-ttu-id="3c511-164">동일한 ContentKey를 Asset에 연결하려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-164">An attempt was made to link the same ContentKey to the Asset.</span></span>
* <span data-ttu-id="3c511-165">저장소 컨테이너가 누락되었거나 더 이상 해당 Asset과 연결되지 않은 Asset에 로케이터를 만들려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-165">An attempt was made to create a locator to an Asset whose storage container is missing or is no longer associated with the Asset.</span></span>
* <span data-ttu-id="3c511-166">사용 중인 로케이터가 5개 있는 Asset에 로케이터를 만들려는 시도가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-166">An attempt was made to create a locator to an Asset which already has 5 locators in use.</span></span> <span data-ttu-id="3c511-167">(Azure Storage는 한 개의 저장소 컨테이너에 다섯 개의 공유 액세스 정책이란 제한을 적용합니다.)</span><span class="sxs-lookup"><span data-stu-id="3c511-167">(Azure Storage enforces the limit of five shared access policies on one storage container.)</span></span>
* <span data-ttu-id="3c511-168">Asset을 IngestManifestAsset에 연결하는 저장소 계정은 상위 IngestManifest에서 사용되는 저장소 계정과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-168">Linking storage account of an Asset to an IngestManifestAsset is not the same as the storage account used by the parent IngestManifest.</span></span>  

## <a name="500-internal-server-error"></a><span data-ttu-id="3c511-169">500 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="3c511-169">500 Internal Server Error</span></span>
<span data-ttu-id="3c511-170">요청을 처리하는 동안 Media Services가 처리를 계속 실행하는 것을 막는 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-170">During the processing of the request, Media Services encounters some error that prevents the processing from continuing.</span></span> <span data-ttu-id="3c511-171">다음 이유 중 하나 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-171">This could be due to one of the following reasons:</span></span>

* <span data-ttu-id="3c511-172">Media Services 계정의 서비스 할당량 정보를 일시적으로 사용할 수 없기 때문에 Asset 또는 Job을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-172">Creating an Asset or Job fails because the Media Services account's service quota information is temporarily unavailable.</span></span>
* <span data-ttu-id="3c511-173">계정의 저장소 계정 정보를 일시적으로 사용할 수 없기 때문에 Asset 또는 IngestManifest blob 저장소 컨테이너를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-173">Creating an Asset or IngestManifest blob storage container fails because the account's storage account information is temporarily unavailable.</span></span>
* <span data-ttu-id="3c511-174">기타 예기치 않은 오류.</span><span class="sxs-lookup"><span data-stu-id="3c511-174">Other unexpected error.</span></span>

## <a name="503-service-unavailable"></a><span data-ttu-id="3c511-175">503 서비스를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3c511-175">503 Service Unavailable</span></span>
<span data-ttu-id="3c511-176">서버는 현재 요청을 받을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-176">The server is currently unable to receive requests.</span></span> <span data-ttu-id="3c511-177">이 오류는 서비스에 요청을 과도하게 해서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-177">This error may be caused by excessive requests to the service.</span></span> <span data-ttu-id="3c511-178">미디어 서비스 제한 메커니즘은 서비스에 과도한 요청을 보내는 응용 프로그램의 리소스 사용을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-178">Media Services throttling mechanism restricts the resource usage for applications that make excessive request to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="3c511-179">503 오류가 발생하는 이유에 관한 자세한 정보를 얻기 위해 오류 메시지 및 오류 코드 문자열을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-179">Check the error message and error code string to get more detailed information about the reason you got the 503 error.</span></span> <span data-ttu-id="3c511-180">이 오류가 항상 제한을 의미하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-180">This error does not always mean throttling.</span></span>
> 
> 

<span data-ttu-id="3c511-181">가능한 상태 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-181">Possible status descriptions are:</span></span>

* <span data-ttu-id="3c511-182">"서버가 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-182">"Server is busy.</span></span> <span data-ttu-id="3c511-183">이 유형의 요청은 이전에 실행되었을 때 {0}초 이상 걸렸습니다."</span><span class="sxs-lookup"><span data-stu-id="3c511-183">Previous runs of this type of request took more than {0} seconds."</span></span>
* <span data-ttu-id="3c511-184">"서버가 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-184">"Server is busy.</span></span> <span data-ttu-id="3c511-185">초당 요청이 {0} 개보다 많을 경우 제한될 수 있습니다."</span><span class="sxs-lookup"><span data-stu-id="3c511-185">More than {0} requests per second can be throttled."</span></span>
* <span data-ttu-id="3c511-186">"서버가 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-186">"Server is busy.</span></span> <span data-ttu-id="3c511-187">{1}초 내에 {0}요청보다 많을 경우 제한될 수 있습니다."</span><span class="sxs-lookup"><span data-stu-id="3c511-187">More than {0} requests within {1} seconds can be throttled."</span></span>

<span data-ttu-id="3c511-188">이 오류를 처리하려면 지수적 백오프 재시도 논리를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-188">To handle this error, we recommend using exponential back-off retry logic.</span></span> <span data-ttu-id="3c511-189">연속된 오류 응답에 대해 재시도 간에 점진적으로 더 긴 대기 시간을 두는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-189">That means using progressively longer waits between retries for consecutive error responses.</span></span>  <span data-ttu-id="3c511-190">자세한 내용은 [일시적인 오류 처리 응용 프로그램 블록(영문)](https://msdn.microsoft.com/library/hh680905.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c511-190">For more information, see [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3c511-191">[.Net용 Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services/tree/master)를 사용 중인 경우 503 오류에 대한 재시도 논리는 SDK로 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c511-191">If you are using [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), the retry logic for the 503 error has been implemented by the SDK.</span></span>  
> 
> 

## <a name="see-also"></a><span data-ttu-id="3c511-192">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3c511-192">See Also</span></span>
[<span data-ttu-id="3c511-193">Media Services 관리 오류 코드</span><span class="sxs-lookup"><span data-stu-id="3c511-193">Media Services Management Error Codes</span></span>](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a><span data-ttu-id="3c511-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c511-194">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3c511-195">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="3c511-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

