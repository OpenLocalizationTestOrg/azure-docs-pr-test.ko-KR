---
title: "Azure 미디어 서비스 원격 분석 rest aaaConfiguring | Microsoft Docs"
description: "이 문서에서는 toouse REST API를 사용 하 여 Azure 미디어 서비스 원격 분석을 hello 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e1a314fb-cc05-4a82-a41b-d1c9888aab09
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d0b6798c49be756fcebecf2e1e6ea497edd27cf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-azure-media-services-telemetry-with-rest"></a><span data-ttu-id="da4be-103">REST를 사용하여 Azure Media Services 원격 분석 구성</span><span class="sxs-lookup"><span data-stu-id="da4be-103">Configuring Azure Media Services telemetry with REST</span></span>

<span data-ttu-id="da4be-104">이 항목에서는 REST API를 사용 하 여 hello Azure 미디어 서비스 (AMS) 원격 분석을 구성할 때 사용할 수 있는 일반적인 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="da4be-104">This topic describes general steps that you might take when configuring hello Azure Media Services (AMS) telemetry using REST API.</span></span> 

>[!NOTE]
><span data-ttu-id="da4be-105">방식에 대 한 hello 기능에 대해 상세히 AMS 원격 분석 및 tooconsume, hello 참조 [개요](media-services-telemetry-overview.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="da4be-105">For hello detailed explanation of what is AMS telemetry and how tooconsume it, see hello [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="da4be-106">이 항목에서 설명 하는 hello 단계는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da4be-106">hello steps described in this topic are:</span></span>

- <span data-ttu-id="da4be-107">미디어 서비스 계정에 연결 된 hello 저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="da4be-107">Getting hello storage account associated with a Media Services account</span></span>
- <span data-ttu-id="da4be-108">Hello 알림 끝점을 가져오기</span><span class="sxs-lookup"><span data-stu-id="da4be-108">Getting hello Notification Endpoints</span></span>
- <span data-ttu-id="da4be-109">모니터링을 위한 알림 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="da4be-109">Creating a Notification Endpoint for Monitoring.</span></span> 

    <span data-ttu-id="da4be-110">toocreate hello이 나와 tooAzureTable (2) 및 endPontAddress toohello 저장소 테이블 설정 (예를 들어 https://telemetryvalidationstore.table.core.windows.net/) 알림 끝점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da4be-110">toocreate a Notification Endpoint, set hello EndPointType tooAzureTable (2) and endPontAddress set toohello storage table (for example, https://telemetryvalidationstore.table.core.windows.net/).</span></span>
  
- <span data-ttu-id="da4be-111">Hello 모니터링 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="da4be-111">Get hello monitoring configurations</span></span>

    <span data-ttu-id="da4be-112">Hello 서비스에 대 한 모니터링 구성 설정 만들기 toomonitor 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="da4be-112">Create a monitoring configuration settings for hello services you want toomonitor.</span></span> <span data-ttu-id="da4be-113">한 개 이하의 모니터링 구성 설정이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da4be-113">No more than one monitoring configuration settings is allowed.</span></span> 

- <span data-ttu-id="da4be-114">모니터링 구성 추가</span><span class="sxs-lookup"><span data-stu-id="da4be-114">Add a monitoring configuration</span></span>


 
## <a name="get-hello-storage-account-associated-with-a-media-services-account"></a><span data-ttu-id="da4be-115">미디어 서비스 계정에 연결 된 hello 저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="da4be-115">Get hello storage account associated with a Media Services account</span></span>

###<a name="request"></a><span data-ttu-id="da4be-116">요청</span><span class="sxs-lookup"><span data-stu-id="da4be-116">Request</span></span>

    GET https://wamsbnp1clus001rest-hs.cloudapp.net/api/StorageAccounts HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Host: wamsbnp1clus001rest-hs.cloudapp.net
    Response
    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 370
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 8206e222-2a59-482c-a6a9-de6b8bda57fb
    x-ms-request-id: 8206e222-2a59-482c-a6a9-de6b8bda57fb
    X-Content-Type-Options: nosniff
    DataServiceVersion: 2.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:40 GMT
    
    {"d":{"results":[{"__metadata":{"id":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/StorageAccounts('telemetryvalidationstore')","uri":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/StorageAccounts('telemetryvalidationstore')","type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.StorageAccount"},"Name":"telemetryvalidationstore","IsDefault":true,"BytesUsed":null}]}}

## <a name="get-hello-notification-endpoints"></a><span data-ttu-id="da4be-117">Hello 알림 끝점 가져오기</span><span class="sxs-lookup"><span data-stu-id="da4be-117">Get hello Notification Endpoints</span></span>

###<a name="request"></a><span data-ttu-id="da4be-118">요청</span><span class="sxs-lookup"><span data-stu-id="da4be-118">Request</span></span>

    GET https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Host: wamsbnp1clus001rest-hs.cloudapp.net
    
###<a name="response"></a><span data-ttu-id="da4be-119">응답</span><span class="sxs-lookup"><span data-stu-id="da4be-119">Response</span></span>
    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 20
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: c68de2b3-0be1-4823-b622-6ca6f94a96b5
    x-ms-request-id: c68de2b3-0be1-4823-b622-6ca6f94a96b5
    X-Content-Type-Options: nosniff
    DataServiceVersion: 2.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:40 GMT
    
    {  
        "d":{  
            "results":[]
        }
    }
 
## <a name="create-a-notification-endpoint-for-monitoring"></a><span data-ttu-id="da4be-120">모니터링을 위한 알림 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="da4be-120">Create a Notification Endpoint for monitoring</span></span>

###<a name="request"></a><span data-ttu-id="da4be-121">요청</span><span class="sxs-lookup"><span data-stu-id="da4be-121">Request</span></span>

    POST https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Content-Type: application/json; charset=utf-8
    Host: wamsbnp1clus001rest-hs.cloudapp.net
    Content-Length: 115
    
    {  
        "Name":"monitoring",
        "EndPointAddress":"https://telemetryvalidationstore.table.core.windows.net/",
        "EndPointType":2
    }

>[!NOTE]
><span data-ttu-id="da4be-122">Toochange hello "https://telemetryvalidationstore.table.core.windows.net" 값 tooyour 저장소 계정을 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="da4be-122">Don't forget toochange hello "https://telemetryvalidationstore.table.core.windows.net" value tooyour storage account.</span></span>

###<a name="response"></a><span data-ttu-id="da4be-123">응답</span><span class="sxs-lookup"><span data-stu-id="da4be-123">Response</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 578
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A76bb4faf-ea29-4815-840a-9a8e20102fc4')
    Server: Microsoft-IIS/8.5
    request-id: e8fa5a60-7d8b-4b00-a7ee-9b0f162fe0a9
    x-ms-request-id: e8fa5a60-7d8b-4b00-a7ee-9b0f162fe0a9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:42 GMT
    
    {"d":{"__metadata":{"id":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A76bb4faf-ea29-4815-840a-9a8e20102fc4')","uri":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/NotificationEndPoints('nb%3Anepid%3AUUID%3A76bb4faf-ea29-4815-840a-9a8e20102fc4')","type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.NotificationEndPoint"},"Id":"nb:nepid:UUID:76bb4faf-ea29-4815-840a-9a8e20102fc4","Name":"monitoring","Created":"\/Date(1449033042667)\/","EndPointAddress":"https://telemetryvalidationstore.table.core.windows.net/","EndPointType":2}}
 
## <a name="get-hello-monitoring-configurations"></a><span data-ttu-id="da4be-124">Hello 모니터링 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="da4be-124">Get hello monitoring configurations</span></span>

### <a name="request"></a><span data-ttu-id="da4be-125">요청</span><span class="sxs-lookup"><span data-stu-id="da4be-125">Request</span></span>

    GET https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Host: wamsbnp1clus001rest-hs.cloudapp.net

###<a name="response"></a><span data-ttu-id="da4be-126">응답</span><span class="sxs-lookup"><span data-stu-id="da4be-126">Response</span></span>
    
    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 20
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 00a3ee37-bb19-4fca-b5c7-a92b629d4416
    x-ms-request-id: 00a3ee37-bb19-4fca-b5c7-a92b629d4416
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:42 GMT
    
    {"d":{"results":[]}}

## <a name="add-a-monitoring-configuration"></a><span data-ttu-id="da4be-127">모니터링 구성 추가</span><span class="sxs-lookup"><span data-stu-id="da4be-127">Add a monitoring configuration</span></span>

### <a name="request"></a><span data-ttu-id="da4be-128">요청</span><span class="sxs-lookup"><span data-stu-id="da4be-128">Request</span></span>

    POST https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations HTTP/1.1
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Content-Type: application/json; charset=utf-8
    Host: wamsbnp1clus001rest-hs.cloudapp.net
    Content-Length: 133
    
    {  
       "NotificationEndPointId":"nb:nepid:UUID:76bb4faf-ea29-4815-840a-9a8e20102fc4",
       "Settings":[  
          {  
         "Component":"Channel",
         "Level":"Normal"
          }
       ]
    }

### <a name="response"></a><span data-ttu-id="da4be-129">응답</span><span class="sxs-lookup"><span data-stu-id="da4be-129">Response</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 825
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')
    Server: Microsoft-IIS/8.5
    request-id: daede9cb-8684-41b0-a921-a3af66430cbe
    x-ms-request-id: daede9cb-8684-41b0-a921-a3af66430cbe
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    access-control-expose-headers: request-id, x-ms-request-id
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 02 Dec 2015 05:10:43 GMT
    
    {"d":{"__metadata":{"id":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')","uri":"https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')","type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.MonitoringConfiguration"},"Id":"nb:mcid:UUID:1a8931ae-799f-45fd-8aeb-9641740295c2","NotificationEndPointId":"nb:nepid:UUID:76bb4faf-ea29-4815-840a-9a8e20102fc4","Created":"2015-12-02T05:10:43.7680396Z","LastModified":"2015-12-02T05:10:43.7680396Z","Settings":{"__metadata":{"type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.ComponentMonitoringSettings)"},"results":[{"Component":"Channel","Level":"Normal"},{"Component":"StreamingEndpoint","Level":"Disabled"}]}}}

## <a name="stop-telemetry"></a><span data-ttu-id="da4be-130">원격 분석 중지</span><span class="sxs-lookup"><span data-stu-id="da4be-130">Stop telemetry</span></span>

###<a name="request"></a><span data-ttu-id="da4be-131">요청</span><span class="sxs-lookup"><span data-stu-id="da4be-131">Request</span></span>

    DELETE https://wamsbnp1clus001rest-hs.cloudapp.net/api/MonitoringConfigurations('nb%3Amcid%3AUUID%3A1a8931ae-799f-45fd-8aeb-9641740295c2')
    x-ms-version: 2.13
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept: application/json; odata=verbose
    Authorization: (redacted)
    Content-Type: application/json; charset=utf-8
    Host: wamsbnp1clus001rest-hs.cloudapp.net

## <a name="consuming-telemetry-information"></a><span data-ttu-id="da4be-132">이</span><span class="sxs-lookup"><span data-stu-id="da4be-132">Consuming telemetry information</span></span>

<span data-ttu-id="da4be-133">원격 분석 정보 사용에 대한 자세한 내용은 [이](media-services-telemetry-overview.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da4be-133">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da4be-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da4be-134">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="da4be-135">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="da4be-135">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
