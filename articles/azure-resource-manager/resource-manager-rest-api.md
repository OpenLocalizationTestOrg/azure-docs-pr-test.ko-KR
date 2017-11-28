---
title: "관리자 REST Api aaaResource | Microsoft Docs"
description: "리소스 관리자 REST Api 인증 hello 및 사용 예제 개요"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="757c7-103">리소스 관리자 REST API</span><span class="sxs-lookup"><span data-stu-id="757c7-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="757c7-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="757c7-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="757c7-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="757c7-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="757c7-106">포털</span><span class="sxs-lookup"><span data-stu-id="757c7-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="757c7-107">REST API</span><span class="sxs-lookup"><span data-stu-id="757c7-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="757c7-108">뒤에 배포 된 모든 서식 파일에 부속 모든 호출 tooAzure 리소스 관리자 뒤에 있는 모든 구성 된 저장소 계정이 있는 경우 하나 이상의 호출 toohello Azure 리소스 관리자의 RESTful API</span><span class="sxs-lookup"><span data-stu-id="757c7-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="757c7-109">이 항목은 전용된 toothose Api 및 모든 SDK를 전혀 사용 하지 않고 해당를 호출 하는 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="757c7-110">이 방법은 기본 설정된 언어에 대 한 SDK hello을 사용할 수 없거나 필요한 hello 작업을 지원 하지 하는 경우 또는 요청 tooAzure의 완전히 제어 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="757c7-111">이 문서는 Azure에서 노출 하지만 대신 일부 작업을 사용 하 여 toothem를 연결 하는 방법의 예로 모든 API 통과 하지 않으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="757c7-112">Hello를 읽을 수 hello 기본 사항을 이해 하면 [Azure 리소스 관리자 REST API 참조](https://docs.microsoft.com/rest/api/resources/) toofind 대 한 상세 정보가 어떻게 toouse hello 나머지 hello Api입니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="757c7-113">인증</span><span class="sxs-lookup"><span data-stu-id="757c7-113">Authentication</span></span>
<span data-ttu-id="757c7-114">Resource Manager에 대한 인증은 Azure AD(Active Directory)에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="757c7-115">tooconnect tooany API, 먼저 Azure AD tooreceive tooevery 요청에 전달할 수 있는 인증 토큰으로 tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="757c7-116">REST Api toohello 있다고 가정 하는 직접 순수 호출을 기술 하는 것 처럼 사용자 이름 및 암호를 묻는 메시지가 여 tooauthenticate를 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="757c7-117">또한 두 가지 요소 인증 메커니즘을 사용하지 않는다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="757c7-118">따라서 Azure AD 응용 프로그램 및 서비스 보안 주체에 사용 되는 toolog 있는 섞어 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="757c7-119">여러 인증 절차와 모든 Azure AD를 지원 하는지 설명 하지만 사용 되는 tooretrieve 후속 API 요청에 대 한 해당 인증 토큰 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="757c7-120">단계별 지침은 [Azure AD 응용 프로그램 및 서비스 주체 만들기](resource-group-create-service-principal-portal.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="757c7-121">액세스 토큰 생성하기</span><span class="sxs-lookup"><span data-stu-id="757c7-121">Generating an Access Token</span></span>
<span data-ttu-id="757c7-122">Azure AD에 대 한 인증 login.microsoftonline.com에 위치한 tooAzure 광고를를 호출 하 여 수행 됩니다. tooauthenticate, 다음 정보는 toohave hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="757c7-123">Azure AD 테 넌 트 ID (hello toolog에서 사용 하는 Azure AD의 이름, 회사와 동일 하지만 반드시 종종 hello)</span><span class="sxs-lookup"><span data-stu-id="757c7-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="757c7-124">응용 프로그램 ID (hello Azure AD 응용 프로그램 작성 단계 중에 수행)</span><span class="sxs-lookup"><span data-stu-id="757c7-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="757c7-125">암호 (즉 hello Azure AD 응용 프로그램을 만드는 동안 선택한)</span><span class="sxs-lookup"><span data-stu-id="757c7-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="757c7-126">HTTP 요청을 수행 하는 hello, 있는지 tooreplace "Azure AD 테 넌 트 ID", "응용 프로그램 ID" 및 "Password" hello 올바른 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="757c7-127">**일반 HTTP 요청:**</span><span class="sxs-lookup"><span data-stu-id="757c7-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="757c7-128">... (인증 성공) 하는 경우에 다음 응답 응답 비슷한 toohello 발생:</span><span class="sxs-lookup"><span data-stu-id="757c7-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
<span data-ttu-id="757c7-129">(앞에 응답 하는 hello에 hello access_token 된 약식된 tooincrease 가독성)</span><span class="sxs-lookup"><span data-stu-id="757c7-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="757c7-130">**Bash를 사용하여 액세스 토큰 생성하기:**</span><span class="sxs-lookup"><span data-stu-id="757c7-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="757c7-131">**Powershell을 사용하여 액세스 토큰 생성:**</span><span class="sxs-lookup"><span data-stu-id="757c7-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="757c7-132">hello 응답에는 액세스 토큰, 기간 해당 토큰은 유효 하는 방법에 대 한 정보 및 어떤 리소스에 대 한 해당 토큰을 사용할 수 있습니다에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="757c7-133">hello 이전 HTTP 호출에 받은 hello 액세스 토큰에 대 한 모든 요청 toohello 리소스 관리자 API에 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="757c7-134">"인증" hello 값 "전달자 YOUR_ACCESS_TOKEN" 라는 헤더 값으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="757c7-135">Hello 간격 "Bearer" 및 액세스 토큰을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="757c7-136">HTTP 결과 위에서 hello 알 수 있듯이는 캐시 및 동일한 토큰을 다시 사용 해야 하는 시간을 특정 기간에 대 한 hello 토큰은 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="757c7-137">각 API 호출에 대 한 Azure AD에 대해 가능한 tooauthenticate 인 경우에 수 없기 매우 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="757c7-138">Resource Manager REST API 호출</span><span class="sxs-lookup"><span data-stu-id="757c7-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="757c7-139">이 항목에는 몇 가지 Api tooexplain hello의 기본 사용법 hello REST 작업 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="757c7-140">모든 hello 작업에 대 한 정보를 참조 하십시오. [Azure 리소스 관리자 REST Api](https://docs.microsoft.com/rest/api/resources/)합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="757c7-141">모든 구독 나열</span><span class="sxs-lookup"><span data-stu-id="757c7-141">List all subscriptions</span></span>
<span data-ttu-id="757c7-142">할 수 있는 hello 가장 간단한 작업 중 하나에 액세스할 수 있는 toolist hello 사용 가능한 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="757c7-143">요청을 수행 하는 hello, 어떻게 hello 액세스 토큰으로 전달 되어 헤더 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="757c7-144">(실제 액세스 토큰으로 YOUR_ACCESS_TOKEN을 대체합니다.)</span><span class="sxs-lookup"><span data-stu-id="757c7-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="757c7-145">... 결과적으로, 수 있게 구독 목록을이 서비스 사용자 tooaccess 허용 됨</span><span class="sxs-lookup"><span data-stu-id="757c7-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="757c7-146">(구독 ID는 가독성을 위해 줄였습니다)</span><span class="sxs-lookup"><span data-stu-id="757c7-146">(Subscription IDs have been shortened for readability)</span></span>

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="757c7-147">특정 구독의 모든 리소스 그룹 나열</span><span class="sxs-lookup"><span data-stu-id="757c7-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="757c7-148">리소스 관리자 Api hello로 사용할 수 있는 모든 리소스는 리소스 그룹 내부에 중첩 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="757c7-149">HTTP GET 요청을 수행 하는 hello를 사용 하 여 구독에 기존 리소스 그룹에 대 한 리소스 관리자를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="757c7-150">Hello 구독 ID 전달 방법에서 hello URL의 일부로이 시간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="757c7-151">(실제 액세스 토큰 및 구독 ID를 YOUR_ACCESS_TOKEN 및 SUBSCRIPTION_ID로 대체합니다)</span><span class="sxs-lookup"><span data-stu-id="757c7-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="757c7-152">hello 얻게 응답에 따라 달라 집니다 리소스 그룹이 정의 되어 있는지 여부 그리고 있다면 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="757c7-153">(구독 ID는 가독성을 위해 줄였습니다)</span><span class="sxs-lookup"><span data-stu-id="757c7-153">(Subscription IDs have been shortened for readability)</span></span>

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="757c7-154">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="757c7-154">Create a resource group</span></span>
<span data-ttu-id="757c7-155">지금까지 म 했습니다만 된 쿼리 정보에 대 한 리소스 관리자 Api hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="757c7-156">일부 리소스를 만든 하 hello 모두, 리소스 그룹의 가장 간단한부터 살펴보겠습니다 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="757c7-157">hello 다음 HTTP 요청 리소스 그룹의 선택한 지역/위치에 만들고 추가 태그 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="757c7-158">(바꿉니다 YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME 실제 액세스 토큰, 구독 ID로, hello toocreate 리소스 그룹의 이름)</span><span class="sxs-lookup"><span data-stu-id="757c7-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

<span data-ttu-id="757c7-159">성공 하면 응답에 따라 유사한 toohello 하는 응답을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="757c7-159">If successful, you get a response that is similar toohello following response:</span></span>

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="757c7-160">Azure에서 리소스 그룹을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="757c7-161">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="757c7-162">리소스 관리자 템플릿을 사용 하 여 리소스 tooa 리소스 그룹 배포</span><span class="sxs-lookup"><span data-stu-id="757c7-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="757c7-163">Resource Manager를 사용하면 템플릿을 사용하여 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="757c7-164">템플릿은 여러 리소스 및 해당 종속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="757c7-165">이 섹션에 대 한 리소스 관리자 템플릿을 잘 알고 있다면 하만 표시할 toomake hello API toostart 배포를 호출 하는 방법을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="757c7-166">템플릿을 만드는 더 자세한 내용은 [Azure Resource Manager 템플릿 작성하기](resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="757c7-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="757c7-167">서식 파일의 배포는 다른 Api를 호출 하는 많은 toohow를 다 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="757c7-168">중요한 점은 템플릿을 배포하는 데 상당한 시간이 걸린다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="757c7-169">hello API 호출만 반환 하 고이 프로토콜은 tooyou 위쪽으로 아웃 hello 배포 toofind의 상태에 대 한 개발자 tooquery hello 배포 수행 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="757c7-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="757c7-170">자세한 내용은 [Azure 비동기 작업 추적](resource-manager-async-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="757c7-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="757c7-171">이 예제에서는 [GitHub](https://github.com/Azure/azure-quickstart-templates)에서 사용할 수 있는 공개적으로 노출된 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="757c7-172">hello 템플릿을 사용 하 여 Linux VM toohello 미국 서 부 지역을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="757c7-173">이 예에서는 템플릿을 사용할 수 있는 GitHub와 같은 공용 저장소에서를 사용 하는 경우에 hello 요청의 일부로 hello 전체 서식 파일을 대신 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="757c7-174">Hello 내에서 사용 되는 매개 변수 값 hello 요청에서 제공 하는 참고 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="757c7-175">(요청에 대 한 적절 한 SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD 및 DNS_NAME_FOR_PUBLIC_IP toovalues replace)</span><span class="sxs-lookup"><span data-stu-id="757c7-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

<span data-ttu-id="757c7-176">이 요청에 대 한 hello 긴 JSON 응답은이 설명서의 생략 된 tooimprove 가독성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="757c7-177">hello 응답 만든 hello 템플릿 배포에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="757c7-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="757c7-178">Next steps</span></span>

- <span data-ttu-id="757c7-179">비동기 REST 작업을 처리 하는 방법에 대 한 toolearn 참조 [Azure 비동기 작업을 추적](resource-manager-async-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="757c7-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
