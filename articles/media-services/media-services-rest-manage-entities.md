---
title: "REST를 사용하여 Media Services 엔터티 관리 | Microsoft Docs"
description: "REST API를 사용하여 미디어 서비스 엔터티를 관리하는 방법을 알아봅니다."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: a336907b605da962f835b8057ac6071f480cd85e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="9f6bf-103">REST를 사용하여 Media Services 엔터티 관리</span><span class="sxs-lookup"><span data-stu-id="9f6bf-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f6bf-104">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="9f6bf-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="9f6bf-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9f6bf-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="9f6bf-106">Microsoft Azure 미디어 서비스는 OData v3에 빌드된 REST 기반 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="9f6bf-107">다른 OData 서비스에서와 거의 같은 방법으로 엔터티를 추가, 쿼리, 업데이트 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-107">You can add, query, update, and delete entities in much the same way as you can on any other OData service.</span></span> <span data-ttu-id="9f6bf-108">예외는 해당하는 경우 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="9f6bf-109">OData에 대한 자세한 내용은 [개방형 데이터 프로토콜 설명서](http://www.odata.org/documentation/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="9f6bf-110">이 항목에서는 REST를 사용하여 Azure Media Services 엔터티를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-110">This topic shows you how to manage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="9f6bf-111">2017년 4월 1일부터 레코드의 총 수가 최고 할당량 미만인 경우에도 사용자 계정에 있는 90일이 지난 작업 레코드는 연결된 태스크 레코드와 함께 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="9f6bf-112">예를 들어, 2017년 4월 1일에는 계정에 있는 2016년 12월 31일 이전의 모든 작업 레코드가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="9f6bf-113">작업/태스크 정보를 보관해야 하는 경우에는 이 항목에 설명된 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-113">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="9f6bf-114">고려 사항</span><span class="sxs-lookup"><span data-stu-id="9f6bf-114">Considerations</span></span>  

<span data-ttu-id="9f6bf-115">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="9f6bf-116">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="9f6bf-117">미디어 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="9f6bf-117">Connect to Media Services</span></span>

<span data-ttu-id="9f6bf-118">AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-118">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="9f6bf-119">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-119">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="9f6bf-120">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-120">You must make subsequent calls to the new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="9f6bf-121">엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="9f6bf-121">Adding entities</span></span>
<span data-ttu-id="9f6bf-122">미디어 서비스의 모든 엔터티는 POST HTTP 요청을 통해 Assets와 같은 엔터티 집합에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-122">Every entity in Media Services is added to an entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="9f6bf-123">다음 예제에서는 AccessPolicy를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-123">The following example shows how to create an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="9f6bf-124">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="9f6bf-124">Querying entities</span></span>
<span data-ttu-id="9f6bf-125">엔터티 쿼리 및 나열은 간단하고 GET HTTP 요청과 선택적 OData 작업만 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="9f6bf-126">다음 예제에서는 모든 MediaProcessor 엔터티 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-126">The following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="9f6bf-127">다음 예제와 같이 특정 엔터티 또는 특정 엔터티와 연결된 모든 엔터티 집합을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in the following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="9f6bf-128">다음 예제에서는 모든 작업의 State 속성만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-128">The following example returns only the State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="9f6bf-129">다음 예제에서는 이름이 "SampleTemplate"인 모든 JobTemplate를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-129">The following example returns all JobTemplates with the name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="9f6bf-130">$expand 작업은 LINQ 고려 사항(WCF 데이터 서비스)에 설명된 지원되지 않는 LINQ 메서드 및 미디어 서비스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-130">The $expand operation is not supported in Media Services as well as the unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="9f6bf-131">대용량 엔터티 컬렉션 열거</span><span class="sxs-lookup"><span data-stu-id="9f6bf-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="9f6bf-132">엔터티를 쿼리할 때 한 번에 반환되는 엔터티 수는 최대 1000개입니다. 공용 REST v2에서는 쿼리 결과를 1000개로 제한하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="9f6bf-133">**skip** 및 **top**을 사용하여 대용량 엔터티 컬렉션을 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-133">Use **skip** and **top** to enumerate through the large collection of entities.</span></span> 

<span data-ttu-id="9f6bf-134">다음 예제에서는 **skip** 및 **top**을 사용하여 처음 2000개의 작업을 건너뛰고 다음 1000개의 작업을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-134">The following example shows how to use **skip** and **top** to skip the first 2000 jobs and get the next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="9f6bf-135">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="9f6bf-135">Updating entities</span></span>
<span data-ttu-id="9f6bf-136">엔터티 형식 및 엔터티 상태에 따라 PATCH, PUT 또는 MERGE HTTP 요청을 통해 해당 엔터티의 속성을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-136">Depending on the entity type and the state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="9f6bf-137">이 작업에 대한 자세한 내용은 [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="9f6bf-138">다음 코드 예제에서는 Asset 엔터티의 Name 속성을 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-138">The following code example shows how to update the Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="9f6bf-139">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="9f6bf-139">Deleting entities</span></span>
<span data-ttu-id="9f6bf-140">DELETE HTTP 요청을 사용하여 미디어 서비스에서 엔터티를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="9f6bf-141">엔터티에 따라 엔터티 삭제 순서가 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-141">Depending on the entity, the order in which you delete entities may be important.</span></span> <span data-ttu-id="9f6bf-142">예를 들어 자산과 같은 엔터티는 자산을 삭제하기 전에 해당 특정 자산을 참조하는 모든 로케이터를 해지(또는 삭제)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting the Asset.</span></span>

<span data-ttu-id="9f6bf-143">다음 예제에서는 파일을 Blob 저장소로 업로드하는 데 사용된 로케이터를 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-143">The following example shows how to delete a Locator that was used to upload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="9f6bf-144">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="9f6bf-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9f6bf-145">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="9f6bf-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

