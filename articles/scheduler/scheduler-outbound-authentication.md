---
title: "스케줄러 아웃바운드 인증"
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
ms.openlocfilehash: e345b2e22daae5b24c23645f7d2636f66df630ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="f88ba-103">스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="f88ba-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="f88ba-104">인증을 요구하는 서비스를 호출하기 위해 스케줄러 작업이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-104">Scheduler jobs may need to call out to services that require authentication.</span></span> <span data-ttu-id="f88ba-105">이를 통해, 호출된 서비스가 스케줄러 작업이 리소스에 액세스 가능한지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-105">This way, a called service can determine if the Scheduler job can access its resources.</span></span> <span data-ttu-id="f88ba-106">이러한 서비스 중 일부에는 다른 Azure 서비스, Salesforce.com, Facebook 및 보안 사용자 지정 웹사이트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="f88ba-107">인증 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="f88ba-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="f88ba-108">스케줄러 작업에 간단하게 인증을 추가할 수 있습니다. 즉 작업을 만들거나 업데이트할 때 JSON 자식 요소 `authentication`을 `request` 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-108">Adding authentication to a Scheduler job is simple – add a JSON child element `authentication` to the `request` element when creating or updating a job.</span></span> <span data-ttu-id="f88ba-109">`authentication` 개체의 일부로 PUT, PATCH 또는 POST 요청에서 스케줄러 서비스에 전달되는 암호는 응답에서 절대 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-109">Secrets passed to the Scheduler service in a PUT, PATCH, or POST request – as part of the `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="f88ba-110">응답에서 암호 정보는 null로 설정되거나, 인증된 엔터티를 나타내는 공용 토큰을 갖을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-110">In responses, secret information is set to null or may have a public token that represents the authenticated entity.</span></span>

<span data-ttu-id="f88ba-111">인증을 제거하려면 작업을 명시적으로 PUT 또는 PATCH하여 `authentication` 개체를 null로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-111">To remove authentication, PUT or PATCH the job explicitly, setting the `authentication` object to null.</span></span> <span data-ttu-id="f88ba-112">응답에는 인증 속성이 하나도 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="f88ba-113">현재 지원되는 인증 유형은 `ClientCertificate`모델(SSL/TLS 클라이언트 인증서를 사용할 경우), `Basic`(기본 인증의 경우), `ActiveDirectoryOAuth`(Active Directory OAuth 인증용)뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-113">Currently, the only supported authentication types are the `ClientCertificate` model (for using the SSL/TLS client certificates), the `Basic` model (for Basic authentication), and the `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="f88ba-114">ClientCertificate 인증에 대한 요청 본문</span><span class="sxs-lookup"><span data-stu-id="f88ba-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="f88ba-115">`ClientCertificate` 모델을 사용하여 인증을 추가할 때는 다음 추가 요소를 요청 본문에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-115">When adding authentication using the `ClientCertificate` model, specify the following additional elements in the request body.</span></span>  

| <span data-ttu-id="f88ba-116">요소</span><span class="sxs-lookup"><span data-stu-id="f88ba-116">Element</span></span> | <span data-ttu-id="f88ba-117">설명</span><span class="sxs-lookup"><span data-stu-id="f88ba-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f88ba-118">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="f88ba-118">*authentication (parent element)*</span></span> |<span data-ttu-id="f88ba-119">SSL 클라이언트 인증서를 사용하기 위한 인증 개체 입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="f88ba-120">*type*</span><span class="sxs-lookup"><span data-stu-id="f88ba-120">*type*</span></span> |<span data-ttu-id="f88ba-121">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-121">Required.</span></span> <span data-ttu-id="f88ba-122">인증 유형입니다. SSL 클라이언트 인증서의 경우 이 값은 `ClientCertificate`입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-122">Type of authentication.For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="f88ba-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="f88ba-123">*pfx*</span></span> |<span data-ttu-id="f88ba-124">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-124">Required.</span></span> <span data-ttu-id="f88ba-125">PFX 파일의 Base64 인코딩 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-125">Base64-encoded contents of the PFX file.</span></span> |
| <span data-ttu-id="f88ba-126">*암호*</span><span class="sxs-lookup"><span data-stu-id="f88ba-126">*password*</span></span> |<span data-ttu-id="f88ba-127">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-127">Required.</span></span> <span data-ttu-id="f88ba-128">PFX 파일에 액세스하기 위한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-128">Password to access the PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="f88ba-129">ClientCertificate 인증에 대한 응답 본문</span><span class="sxs-lookup"><span data-stu-id="f88ba-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="f88ba-130">인증 정보와 함께 요청을 보내면 응답에는 다음 인증 관련 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-130">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="f88ba-131">요소</span><span class="sxs-lookup"><span data-stu-id="f88ba-131">Element</span></span> | <span data-ttu-id="f88ba-132">설명</span><span class="sxs-lookup"><span data-stu-id="f88ba-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f88ba-133">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="f88ba-133">*authentication (parent element)*</span></span> |<span data-ttu-id="f88ba-134">SSL 클라이언트 인증서를 사용하기 위한 인증 개체 입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="f88ba-135">*type*</span><span class="sxs-lookup"><span data-stu-id="f88ba-135">*type*</span></span> |<span data-ttu-id="f88ba-136">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-136">Type of authentication.</span></span> <span data-ttu-id="f88ba-137">SSL 클라이언트 인증서의 경우 이 값은 `ClientCertificate`입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-137">For SSL client certificates, the value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="f88ba-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="f88ba-138">*certificateThumbprint*</span></span> |<span data-ttu-id="f88ba-139">인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-139">The thumbprint of the certificate.</span></span> |
| <span data-ttu-id="f88ba-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="f88ba-140">*certificateSubjectName*</span></span> |<span data-ttu-id="f88ba-141">인증서의 주체 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-141">The subject distinguished name of the certificate.</span></span> |
| <span data-ttu-id="f88ba-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="f88ba-142">*certificateExpiration*</span></span> |<span data-ttu-id="f88ba-143">인증서의 만료일입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-143">The expiration date of the certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="f88ba-144">ClientCertificate 인증에 대한 샘플 REST 요청</span><span class="sxs-lookup"><span data-stu-id="f88ba-144">Sample REST Request for ClientCertificate Authentication</span></span>
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="f88ba-145">ClientCertificate 인증에 대한 샘플 REST 응답</span><span class="sxs-lookup"><span data-stu-id="f88ba-145">Sample REST Response for ClientCertificate Authentication</span></span>
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

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="f88ba-146">기본 인증의 요청 본문</span><span class="sxs-lookup"><span data-stu-id="f88ba-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="f88ba-147">`Basic` 모델을 사용하여 인증을 추가할 때는 다음 추가 요소를 요청 본문에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-147">When adding authentication using the `Basic` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="f88ba-148">요소</span><span class="sxs-lookup"><span data-stu-id="f88ba-148">Element</span></span> | <span data-ttu-id="f88ba-149">설명</span><span class="sxs-lookup"><span data-stu-id="f88ba-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f88ba-150">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="f88ba-150">*authentication (parent element)*</span></span> |<span data-ttu-id="f88ba-151">기본 인증을 사용 하기 위한 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="f88ba-152">*type*</span><span class="sxs-lookup"><span data-stu-id="f88ba-152">*type*</span></span> |<span data-ttu-id="f88ba-153">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-153">Required.</span></span> <span data-ttu-id="f88ba-154">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-154">Type of authentication.</span></span> <span data-ttu-id="f88ba-155">기본 인증의 경우 이 값은 `Basic`입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-155">For Basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="f88ba-156">*사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="f88ba-156">*username*</span></span> |<span data-ttu-id="f88ba-157">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-157">Required.</span></span> <span data-ttu-id="f88ba-158">인증하기 위한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-158">Username to authenticate.</span></span> |
| <span data-ttu-id="f88ba-159">*암호*</span><span class="sxs-lookup"><span data-stu-id="f88ba-159">*password*</span></span> |<span data-ttu-id="f88ba-160">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-160">Required.</span></span> <span data-ttu-id="f88ba-161">인증하기 위한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-161">Password to authenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="f88ba-162">기본 인증의 응답 본문</span><span class="sxs-lookup"><span data-stu-id="f88ba-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="f88ba-163">인증 정보와 함께 요청을 보내면 응답에는 다음 인증 관련 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-163">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="f88ba-164">요소</span><span class="sxs-lookup"><span data-stu-id="f88ba-164">Element</span></span> | <span data-ttu-id="f88ba-165">설명</span><span class="sxs-lookup"><span data-stu-id="f88ba-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f88ba-166">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="f88ba-166">*authentication (parent element)*</span></span> |<span data-ttu-id="f88ba-167">기본 인증을 사용 하기 위한 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="f88ba-168">*type*</span><span class="sxs-lookup"><span data-stu-id="f88ba-168">*type*</span></span> |<span data-ttu-id="f88ba-169">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-169">Type of authentication.</span></span> <span data-ttu-id="f88ba-170">기본 인증의 경우 이 값은 `Basic`입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-170">For Basic authentication, the value is `Basic`.</span></span> |
| <span data-ttu-id="f88ba-171">*사용자 이름*</span><span class="sxs-lookup"><span data-stu-id="f88ba-171">*username*</span></span> |<span data-ttu-id="f88ba-172">인증된 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-172">The authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="f88ba-173">기본 인증에 대한 샘플 REST 요청</span><span class="sxs-lookup"><span data-stu-id="f88ba-173">Sample REST Request for Basic Authentication</span></span>
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

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="f88ba-174">기본 인증에 대한 샘플 REST 응답</span><span class="sxs-lookup"><span data-stu-id="f88ba-174">Sample REST Response for Basic Authentication</span></span>
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="f88ba-175">ActiveDirectoryOAuth 인증의 요청 본문</span><span class="sxs-lookup"><span data-stu-id="f88ba-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="f88ba-176">`ActiveDirectoryOAuth` 모델을 사용하여 인증을 추가할 때는 다음 추가 요소를 요청 본문에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-176">When adding authentication using the `ActiveDirectoryOAuth` model, specify the following additional elements in the request body.</span></span>

| <span data-ttu-id="f88ba-177">요소</span><span class="sxs-lookup"><span data-stu-id="f88ba-177">Element</span></span> | <span data-ttu-id="f88ba-178">설명</span><span class="sxs-lookup"><span data-stu-id="f88ba-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f88ba-179">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="f88ba-179">*authentication (parent element)*</span></span> |<span data-ttu-id="f88ba-180">ActiveDirectoryOAuth 인증을 사용하기 위한 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="f88ba-181">*type*</span><span class="sxs-lookup"><span data-stu-id="f88ba-181">*type*</span></span> |<span data-ttu-id="f88ba-182">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-182">Required.</span></span> <span data-ttu-id="f88ba-183">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-183">Type of authentication.</span></span> <span data-ttu-id="f88ba-184">ActiveDirectoryOAuth 인증의 경우 이 값은 `ActiveDirectoryOAuth`입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-184">For ActiveDirectoryOAuth authentication, the value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="f88ba-185">*테넌트*</span><span class="sxs-lookup"><span data-stu-id="f88ba-185">*tenant*</span></span> |<span data-ttu-id="f88ba-186">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-186">Required.</span></span> <span data-ttu-id="f88ba-187">Azure AD 테넌트의 테넌트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-187">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="f88ba-188">*대상*</span><span class="sxs-lookup"><span data-stu-id="f88ba-188">*audience*</span></span> |<span data-ttu-id="f88ba-189">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-189">Required.</span></span> <span data-ttu-id="f88ba-190">이는 https://management.core.windows.net/에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-190">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="f88ba-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="f88ba-191">*clientId*</span></span> |<span data-ttu-id="f88ba-192">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-192">Required.</span></span> <span data-ttu-id="f88ba-193">Azure AD 응용 프로그램의 클라이언트 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-193">Provide the client identifier for the Azure AD application.</span></span> |
| <span data-ttu-id="f88ba-194">*암호*</span><span class="sxs-lookup"><span data-stu-id="f88ba-194">*secret*</span></span> |<span data-ttu-id="f88ba-195">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-195">Required.</span></span> <span data-ttu-id="f88ba-196">토큰을 요청하는 클라이언트의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-196">Secret of the client that is requesting the token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="f88ba-197">테넌트 식별자 확인</span><span class="sxs-lookup"><span data-stu-id="f88ba-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="f88ba-198">Azure PowerShell에서 `Get-AzureAccount` 를 실행하여 Azure AD 테넌트의 테넌트 식별자를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-198">You can find the tenant identifier for the Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="f88ba-199">ActiveDirectoryOAuth 인증의 응답 본문</span><span class="sxs-lookup"><span data-stu-id="f88ba-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="f88ba-200">인증 정보와 함께 요청을 보내면 응답에는 다음 인증 관련 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-200">When a request is sent with authentication info, the response contains the following authentication-related elements.</span></span>

| <span data-ttu-id="f88ba-201">요소</span><span class="sxs-lookup"><span data-stu-id="f88ba-201">Element</span></span> | <span data-ttu-id="f88ba-202">설명</span><span class="sxs-lookup"><span data-stu-id="f88ba-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f88ba-203">*인증(부모 요소)*</span><span class="sxs-lookup"><span data-stu-id="f88ba-203">*authentication (parent element)*</span></span> |<span data-ttu-id="f88ba-204">ActiveDirectoryOAuth 인증을 사용하기 위한 인증 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="f88ba-205">*type*</span><span class="sxs-lookup"><span data-stu-id="f88ba-205">*type*</span></span> |<span data-ttu-id="f88ba-206">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-206">Type of authentication.</span></span> <span data-ttu-id="f88ba-207">ActiveDirectoryOAuth 인증의 경우 이 값은 `ActiveDirectoryOAuth`입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-207">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="f88ba-208">*테넌트*</span><span class="sxs-lookup"><span data-stu-id="f88ba-208">*tenant*</span></span> |<span data-ttu-id="f88ba-209">Azure AD 테넌트의 테넌트 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-209">The tenant identifier for the Azure AD tenant.</span></span> |
| <span data-ttu-id="f88ba-210">*대상*</span><span class="sxs-lookup"><span data-stu-id="f88ba-210">*audience*</span></span> |<span data-ttu-id="f88ba-211">이는 https://management.core.windows.net/에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-211">This is set to https://management.core.windows.net/.</span></span> |
| <span data-ttu-id="f88ba-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="f88ba-212">*clientId*</span></span> |<span data-ttu-id="f88ba-213">Azure AD 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f88ba-213">The client identifier for the Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="f88ba-214">ActiveDirectoryOAuth 인증에 대한 샘플 REST 요청</span><span class="sxs-lookup"><span data-stu-id="f88ba-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="f88ba-215">ActiveDirectoryOAuth 인증에 대한 샘플 REST 응답</span><span class="sxs-lookup"><span data-stu-id="f88ba-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
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

## <a name="see-also"></a><span data-ttu-id="f88ba-216">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f88ba-216">See Also</span></span>
 [<span data-ttu-id="f88ba-217">스케줄러란?</span><span class="sxs-lookup"><span data-stu-id="f88ba-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="f88ba-218">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="f88ba-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="f88ba-219">Azure 포털에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="f88ba-219">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="f88ba-220">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="f88ba-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="f88ba-221">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="f88ba-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="f88ba-222">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="f88ba-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="f88ba-223">Azure 스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="f88ba-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="f88ba-224">Azure 스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="f88ba-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

