---
title: "aaaScheduler 아웃 바운드 인증"
description: "스케줄러 아웃바운드 인증"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="b227f-103">스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="b227f-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="b227f-104">스케줄러 작업 toocall 인증이 필요한 tooservices 아웃 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="b227f-105">이러한 방식으로 호출된 된 서비스 hello 스케줄러 작업 리소스에 액세스할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="b227f-106">이러한 서비스 중 일부에는 다른 Azure 서비스, Salesforce.com, Facebook 및 보안 사용자 지정 웹사이트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="b227f-107">인증 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="b227f-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="b227f-108">추가 인증 tooa 스케줄러 작업은 간단-JSON 자식 요소를 추가 `authentication` toohello `request` 만들거나 작업을 업데이트할 때 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="b227f-109">전달 되는 암호 toohello 스케줄러 서비스 – PUT, PATCH 또는 POST 요청에 hello의 일부로 `authentication` 개체 – 응답에서 반환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="b227f-110">응답에서는 비밀 정보 toonull 설정 되거나 인증 hello 엔터티를 나타내는 공용 토큰을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="b227f-111">tooremove 인증 하거나 hello 작업을 명시적으로 패치 하 여 hello 설정 `authentication` toonull 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="b227f-112">응답에는 인증 속성이 하나도 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="b227f-113">현재 지원만 hello 인증 유형에 hello `ClientCertificate` (사용 하 여 모델 hello SSL/TLS 클라이언트 인증서), hello `Basic` (기본 인증의 경우)에 대 한 모델 및 hello `ActiveDirectoryOAuth` 모델 (Active Directory OAuth 인증용)입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="b227f-114">ClientCertificate 인증에 대한 요청 본문</span><span class="sxs-lookup"><span data-stu-id="b227f-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="b227f-115">Hello를 사용 하 여 인증을 추가할 때 `ClientCertificate` 모델을 hello hello 요청 본문의 추가 요소에 다음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="b227f-116">요소</span><span class="sxs-lookup"><span data-stu-id="b227f-116">Element</span></span> | <span data-ttu-id="b227f-117">설명</span><span class="sxs-lookup"><span data-stu-id="b227f-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b227f-118">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="b227f-118">*authentication (parent element)*</span></span> |<span data-ttu-id="b227f-119">SSL 클라이언트 인증서를 사용하기 위한 인증 개체 입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="b227f-120">*type*</span><span class="sxs-lookup"><span data-stu-id="b227f-120">*type*</span></span> |<span data-ttu-id="b227f-121">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-121">Required.</span></span> <span data-ttu-id="b227f-122">인증 유형입니다. SSL 클라이언트 인증서에 대 한 hello 값 이어야 합니다 `ClientCertificate`합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="b227f-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="b227f-123">*pfx*</span></span> |<span data-ttu-id="b227f-124">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-124">Required.</span></span> <span data-ttu-id="b227f-125">Hello PFX 파일의 Base64 인코딩 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="b227f-126">*암호*</span><span class="sxs-lookup"><span data-stu-id="b227f-126">*password*</span></span> |<span data-ttu-id="b227f-127">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-127">Required.</span></span> <span data-ttu-id="b227f-128">Tooaccess hello PFX 파일 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="b227f-129">ClientCertificate 인증에 대한 응답 본문</span><span class="sxs-lookup"><span data-stu-id="b227f-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="b227f-130">요청 인증 정보와 함께 보내면 hello 응답 hello 다음 인증 관련 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="b227f-131">요소</span><span class="sxs-lookup"><span data-stu-id="b227f-131">Element</span></span> | <span data-ttu-id="b227f-132">설명</span><span class="sxs-lookup"><span data-stu-id="b227f-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b227f-133">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="b227f-133">*authentication (parent element)*</span></span> |<span data-ttu-id="b227f-134">SSL 클라이언트 인증서를 사용하기 위한 인증 개체 입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="b227f-135">*type*</span><span class="sxs-lookup"><span data-stu-id="b227f-135">*type*</span></span> |<span data-ttu-id="b227f-136">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-136">Type of authentication.</span></span> <span data-ttu-id="b227f-137">SSL 클라이언트 인증서 hello 값은 `ClientCertificate`합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="b227f-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="b227f-138">*certificateThumbprint*</span></span> |<span data-ttu-id="b227f-139">hello 인증서의 지문 안녕하세요입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="b227f-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="b227f-140">*certificateSubjectName*</span></span> |<span data-ttu-id="b227f-141">hello 인증서의 hello 주체의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="b227f-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="b227f-142">*certificateExpiration*</span></span> |<span data-ttu-id="b227f-143">hello hello 인증서의 만료 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="b227f-144">ClientCertificate 인증에 대한 샘플 REST 요청</span><span class="sxs-lookup"><span data-stu-id="b227f-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="b227f-145">ClientCertificate 인증에 대한 샘플 REST 응답</span><span class="sxs-lookup"><span data-stu-id="b227f-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="b227f-146">기본 인증의 요청 본문</span><span class="sxs-lookup"><span data-stu-id="b227f-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="b227f-147">Hello를 사용 하 여 인증을 추가할 때 `Basic` 모델을 hello hello 요청 본문의 추가 요소에 다음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="b227f-148">요소</span><span class="sxs-lookup"><span data-stu-id="b227f-148">Element</span></span> | <span data-ttu-id="b227f-149">설명</span><span class="sxs-lookup"><span data-stu-id="b227f-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b227f-150">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="b227f-150">*authentication (parent element)*</span></span> |<span data-ttu-id="b227f-151">기본 인증을 사용 하기 위한 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="b227f-152">*type*</span><span class="sxs-lookup"><span data-stu-id="b227f-152">*type*</span></span> |<span data-ttu-id="b227f-153">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-153">Required.</span></span> <span data-ttu-id="b227f-154">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-154">Type of authentication.</span></span> <span data-ttu-id="b227f-155">기본 인증에 대 한 hello 값 이어야 합니다 `Basic`합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="b227f-156">*사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="b227f-156">*username*</span></span> |<span data-ttu-id="b227f-157">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-157">Required.</span></span> <span data-ttu-id="b227f-158">사용자 이름 tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="b227f-159">*암호*</span><span class="sxs-lookup"><span data-stu-id="b227f-159">*password*</span></span> |<span data-ttu-id="b227f-160">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-160">Required.</span></span> <span data-ttu-id="b227f-161">암호 tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="b227f-162">기본 인증의 응답 본문</span><span class="sxs-lookup"><span data-stu-id="b227f-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="b227f-163">요청 인증 정보와 함께 보내면 hello 응답 hello 다음 인증 관련 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="b227f-164">요소</span><span class="sxs-lookup"><span data-stu-id="b227f-164">Element</span></span> | <span data-ttu-id="b227f-165">설명</span><span class="sxs-lookup"><span data-stu-id="b227f-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b227f-166">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="b227f-166">*authentication (parent element)*</span></span> |<span data-ttu-id="b227f-167">기본 인증을 사용 하기 위한 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="b227f-168">*type*</span><span class="sxs-lookup"><span data-stu-id="b227f-168">*type*</span></span> |<span data-ttu-id="b227f-169">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-169">Type of authentication.</span></span> <span data-ttu-id="b227f-170">기본 인증을 hello 값은 `Basic`합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="b227f-171">*사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="b227f-171">*username*</span></span> |<span data-ttu-id="b227f-172">hello 인증 사용자 이름.</span><span class="sxs-lookup"><span data-stu-id="b227f-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="b227f-173">기본 인증에 대한 샘플 REST 요청</span><span class="sxs-lookup"><span data-stu-id="b227f-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="b227f-174">기본 인증에 대한 샘플 REST 응답</span><span class="sxs-lookup"><span data-stu-id="b227f-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="b227f-175">ActiveDirectoryOAuth 인증의 요청 본문</span><span class="sxs-lookup"><span data-stu-id="b227f-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="b227f-176">Hello를 사용 하 여 인증을 추가할 때 `ActiveDirectoryOAuth` 모델을 hello hello 요청 본문의 추가 요소에 다음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="b227f-177">요소</span><span class="sxs-lookup"><span data-stu-id="b227f-177">Element</span></span> | <span data-ttu-id="b227f-178">설명</span><span class="sxs-lookup"><span data-stu-id="b227f-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b227f-179">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="b227f-179">*authentication (parent element)*</span></span> |<span data-ttu-id="b227f-180">ActiveDirectoryOAuth 인증을 사용하기 위한 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="b227f-181">*type*</span><span class="sxs-lookup"><span data-stu-id="b227f-181">*type*</span></span> |<span data-ttu-id="b227f-182">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-182">Required.</span></span> <span data-ttu-id="b227f-183">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-183">Type of authentication.</span></span> <span data-ttu-id="b227f-184">ActiveDirectoryOAuth 인증에 대 한 hello 값 이어야 합니다 `ActiveDirectoryOAuth`합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="b227f-185">*테넌트*</span><span class="sxs-lookup"><span data-stu-id="b227f-185">*tenant*</span></span> |<span data-ttu-id="b227f-186">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-186">Required.</span></span> <span data-ttu-id="b227f-187">hello hello Azure AD 테 넌 트에 대 한 테 넌 트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="b227f-188">*대상*</span><span class="sxs-lookup"><span data-stu-id="b227f-188">*audience*</span></span> |<span data-ttu-id="b227f-189">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-189">Required.</span></span> <span data-ttu-id="b227f-190">이 toohttps://management.core.windows.net/를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="b227f-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="b227f-191">*clientId*</span></span> |<span data-ttu-id="b227f-192">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-192">Required.</span></span> <span data-ttu-id="b227f-193">Hello Azure AD 응용 프로그램에 대 한 hello 클라이언트 식별자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="b227f-194">*암호*</span><span class="sxs-lookup"><span data-stu-id="b227f-194">*secret*</span></span> |<span data-ttu-id="b227f-195">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-195">Required.</span></span> <span data-ttu-id="b227f-196">Hello 토큰을 요청 하는 hello 클라이언트의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="b227f-197">테넌트 식별자 확인</span><span class="sxs-lookup"><span data-stu-id="b227f-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="b227f-198">실행 하 여 hello Azure AD 테 넌 트에 대 한 hello 테 넌 트 식별자를 찾을 수 있습니다 `Get-AzureAccount` Azure PowerShell에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="b227f-199">ActiveDirectoryOAuth 인증의 응답 본문</span><span class="sxs-lookup"><span data-stu-id="b227f-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="b227f-200">요청 인증 정보와 함께 보내면 hello 응답 hello 다음 인증 관련 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="b227f-201">요소</span><span class="sxs-lookup"><span data-stu-id="b227f-201">Element</span></span> | <span data-ttu-id="b227f-202">설명</span><span class="sxs-lookup"><span data-stu-id="b227f-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b227f-203">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="b227f-203">*authentication (parent element)*</span></span> |<span data-ttu-id="b227f-204">ActiveDirectoryOAuth 인증을 사용하기 위한 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="b227f-205">*type*</span><span class="sxs-lookup"><span data-stu-id="b227f-205">*type*</span></span> |<span data-ttu-id="b227f-206">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-206">Type of authentication.</span></span> <span data-ttu-id="b227f-207">ActiveDirectoryOAuth 인증 hello 값은 `ActiveDirectoryOAuth`합니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="b227f-208">*테넌트*</span><span class="sxs-lookup"><span data-stu-id="b227f-208">*tenant*</span></span> |<span data-ttu-id="b227f-209">hello hello Azure AD 테 넌 트에 대 한 테 넌 트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="b227f-210">*대상*</span><span class="sxs-lookup"><span data-stu-id="b227f-210">*audience*</span></span> |<span data-ttu-id="b227f-211">이 toohttps://management.core.windows.net/를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="b227f-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="b227f-212">*clientId*</span></span> |<span data-ttu-id="b227f-213">hello hello Azure AD 응용 프로그램에 대 한 클라이언트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b227f-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="b227f-214">ActiveDirectoryOAuth 인증에 대한 샘플 REST 요청</span><span class="sxs-lookup"><span data-stu-id="b227f-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="b227f-215">ActiveDirectoryOAuth 인증에 대한 샘플 REST 응답</span><span class="sxs-lookup"><span data-stu-id="b227f-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="b227f-216">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b227f-216">See Also</span></span>
 [<span data-ttu-id="b227f-217">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="b227f-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="b227f-218">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="b227f-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="b227f-219">Hello Azure 포털에서에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="b227f-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="b227f-220">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="b227f-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="b227f-221">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="b227f-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="b227f-222">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="b227f-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="b227f-223">Azure 스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="b227f-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="b227f-224">Azure 스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="b227f-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

