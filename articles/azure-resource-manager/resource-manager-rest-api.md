---
title: "리소스 관리자 REST API | Microsoft Docs"
description: "리소스 관리자 REST API 인증 및 사용 예제 개요"
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
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="68f3b-103">리소스 관리자 REST API</span><span class="sxs-lookup"><span data-stu-id="68f3b-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68f3b-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="68f3b-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="68f3b-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="68f3b-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="68f3b-106">포털</span><span class="sxs-lookup"><span data-stu-id="68f3b-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="68f3b-107">REST API</span><span class="sxs-lookup"><span data-stu-id="68f3b-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="68f3b-108">Azure Resource Manager에 대한 모든 호출, 배포된 모든 템플릿, 구성된 모든 저장소 계정에 앞서 Azure Resource Manager의 RESTful API에 대한 하나 또는 하나 이상의 호출이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="68f3b-109">이 항목은 해당 API 및 SDK를 전혀 사용하지 않고 해당 API를 호출하는 방법에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="68f3b-110">이 방법은 Azure에 대한 요청을 완전히 제어하려는 경우 또는 SDK에서 기본 설정 언어를 사용할 수 없거나 필요한 작업을 지원하지 않는 경우에 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="68f3b-111">이 문서에서는 Azure에서 노출된 모든 API를 다루지 않지만 일부 작업을 연결 방법의 예제로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="68f3b-112">기본 사항을 이해한 후에 [Azure Resource Manager REST API 참조](https://docs.microsoft.com/rest/api/resources/)를 읽고 나머지 API를 사용하는 방법에 대한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="68f3b-113">인증</span><span class="sxs-lookup"><span data-stu-id="68f3b-113">Authentication</span></span>
<span data-ttu-id="68f3b-114">Resource Manager에 대한 인증은 Azure AD(Active Directory)에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="68f3b-115">API에 연결하려면 먼저 모든 요청에 전달할 수 있는 인증 토큰을 수신하도록 Azure AD로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="68f3b-116">REST API에 대한 직접 순수 호출을 설명하는 경우 사용자 이름 및 암호를 묻는 메시지를 표시하여 인증하지 않는다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="68f3b-117">또한 두 가지 요소 인증 메커니즘을 사용하지 않는다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="68f3b-118">따라서 로그인에 사용되는 Azure AD 응용 프로그램 및 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="68f3b-119">그러나 Azure AD는 몇 가지 인증 프로시저를 지원하고 이 모두가 후속 API 요청에 필요한 인증 토큰을 검색하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="68f3b-120">단계별 지침은 [Azure AD 응용 프로그램 및 서비스 주체 만들기](resource-group-create-service-principal-portal.md)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="68f3b-121">액세스 토큰 생성하기</span><span class="sxs-lookup"><span data-stu-id="68f3b-121">Generating an Access Token</span></span>
<span data-ttu-id="68f3b-122">Azure AD에 대한 인증은 login.microsoftonline.com에 있는 Azure AD를 호출하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="68f3b-123">인증하려면 다음 정보를 가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="68f3b-124">Azure AD 테넌트 ID(로그인하는 데 사용한 Azure AD의 이름, 종종 회사와 동일하지만 반드시 그렇지는 않음)</span><span class="sxs-lookup"><span data-stu-id="68f3b-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="68f3b-125">응용 프로그램 ID(Azure AD 응용 프로그램 생성 단계 중에 사용됨)</span><span class="sxs-lookup"><span data-stu-id="68f3b-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="68f3b-126">암호(Azure AD 응용 프로그램을 만드는 동안 선택함)</span><span class="sxs-lookup"><span data-stu-id="68f3b-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="68f3b-127">다음 HTTP 요청에서 "Azure AD 테넌트 ID", "응용 프로그램 ID" 및 "암호"를 올바른 값으로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="68f3b-128">**일반 HTTP 요청:**</span><span class="sxs-lookup"><span data-stu-id="68f3b-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="68f3b-129">인증이 성공한 경우 ...은 다음 응답과 유사한 응답이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

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
<span data-ttu-id="68f3b-130">(앞서 응답의 access_token은 가독성을 높이기 위해 줄였습니다)</span><span class="sxs-lookup"><span data-stu-id="68f3b-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="68f3b-131">**Bash를 사용하여 액세스 토큰 생성하기:**</span><span class="sxs-lookup"><span data-stu-id="68f3b-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="68f3b-132">**Powershell을 사용하여 액세스 토큰 생성:**</span><span class="sxs-lookup"><span data-stu-id="68f3b-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="68f3b-133">응답에는 액세스 토큰, 해당 토큰의 유효 기간에 대한 정보 및 해당 토큰을 사용 가능한 리소스에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="68f3b-134">이전 HTTP 호출에서 받은 액세스 토큰은 Resource Manager API에 대한 모든 요청에 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="68f3b-135">"전달자 YOUR_ACCESS_TOKEN" 값을 포함한 "권한 부여"라는 헤더 값으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="68f3b-136">"전달자"와 액세스 토큰 사이의 공간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="68f3b-137">위의 HTTP 결과에서 볼 수 있듯이 토큰은 특정 기간 동안 유효하며 그 동안 동일한 토큰을 캐시하고 다시 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="68f3b-138">각 API 호출에서 Azure AD에 대해 인증하는 작업이 가능하더라도 매우 비효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="68f3b-139">Resource Manager REST API 호출</span><span class="sxs-lookup"><span data-stu-id="68f3b-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="68f3b-140">이 항목에서는 몇 가지 API만을 사용하여 REST 작업의 기본 사용법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="68f3b-141">REST API에 대한 정보는 [Azure Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68f3b-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="68f3b-142">모든 구독 나열</span><span class="sxs-lookup"><span data-stu-id="68f3b-142">List all subscriptions</span></span>
<span data-ttu-id="68f3b-143">가능한 가장 간단한 작업 중 하나는 액세스할 수 있는 사용 가능한 구독을 나열하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="68f3b-144">다음 요청에서 액세스 토큰을 헤더로 전달하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="68f3b-145">(실제 액세스 토큰으로 YOUR_ACCESS_TOKEN을 대체합니다.)</span><span class="sxs-lookup"><span data-stu-id="68f3b-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="68f3b-146">... 결과적으로 이 서비스 주체가 액세스할 수 있는 구독 목록을 가져올 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="68f3b-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="68f3b-147">(구독 ID는 가독성을 위해 줄였습니다)</span><span class="sxs-lookup"><span data-stu-id="68f3b-147">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="68f3b-148">특정 구독의 모든 리소스 그룹 나열</span><span class="sxs-lookup"><span data-stu-id="68f3b-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="68f3b-149">Resource Manager API와 함께 사용할 수 있는 모든 리소스는 리소스 그룹의 내부에 중첩됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="68f3b-150">다음 HTTP GET 요청을 사용하여 구독에 있는 기존 리소스 그룹에 대한 Resource Manager를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="68f3b-151">이번에는 구독 ID를 URL의 일부로 전달하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="68f3b-152">(실제 액세스 토큰 및 구독 ID를 YOUR_ACCESS_TOKEN 및 SUBSCRIPTION_ID로 대체합니다)</span><span class="sxs-lookup"><span data-stu-id="68f3b-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="68f3b-153">정의된 리소스 그룹이 있는지, 있다면 얼마나 많은지에 따라 받는 응답이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="68f3b-154">(구독 ID는 가독성을 위해 줄였습니다)</span><span class="sxs-lookup"><span data-stu-id="68f3b-154">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="68f3b-155">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="68f3b-155">Create a resource group</span></span>
<span data-ttu-id="68f3b-156">지금까지 정보에 대한 Resource Manager API를 쿼리했습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="68f3b-157">이번에는 몇 가지 리소스를 만들고 가장 간단한 리소스 그룹으로 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="68f3b-158">다음 HTTP 요청은 선택한 지역/위치에서 리소스 그룹을 만들고 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="68f3b-159">(실제 액세스 토큰, 구독 ID 및 만들려는 리소스 그룹의 이름을 YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME으로 대체합니다)</span><span class="sxs-lookup"><span data-stu-id="68f3b-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

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

<span data-ttu-id="68f3b-160">성공하면 다음 응답과 유사한 응답을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-160">If successful, you get a response that is similar to the following response:</span></span>

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

<span data-ttu-id="68f3b-161">Azure에서 리소스 그룹을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="68f3b-162">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="68f3b-163">Resource Manager 템플릿을 사용하여 리소스 그룹에 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="68f3b-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="68f3b-164">Resource Manager를 사용하면 템플릿을 사용하여 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="68f3b-165">템플릿은 여러 리소스 및 해당 종속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="68f3b-166">이 섹션에서는 사용자가 Resource Manager 템플릿을 잘 알고 있다고 가정하고 API를 호출하여 배포를 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="68f3b-167">템플릿을 만드는 더 자세한 내용은 [Azure Resource Manager 템플릿 작성하기](resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68f3b-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="68f3b-168">템플릿의 배포는 다른 API를 호출하는 방법과 크게 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="68f3b-169">중요한 점은 템플릿을 배포하는 데 상당한 시간이 걸린다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="68f3b-170">API 호출이 반환되면 사용자는 개발자로서 배포의 상태를 쿼리하여 배포를 수행할 시기를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="68f3b-171">자세한 내용은 [Azure 비동기 작업 추적](resource-manager-async-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68f3b-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="68f3b-172">이 예제에서는 [GitHub](https://github.com/Azure/azure-quickstart-templates)에서 사용할 수 있는 공개적으로 노출된 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="68f3b-173">사용한 템플릿은 미국 서부 지역에 Linux VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="68f3b-174">이 예제에서 GitHub와 같은 공용 저장소에서 사용할 수 있는 템플릿을 사용하더라도 전체 템플릿을 요청의 일부로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="68f3b-175">배포된 템플릿 내에서 사용된 요청에 있는 매개 변수 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="68f3b-176">(SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD 및 DNS_NAME_FOR_PUBLIC_IP를 요청에 대한 적절한 값으로 대체합니다)</span><span class="sxs-lookup"><span data-stu-id="68f3b-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

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

<span data-ttu-id="68f3b-177">이 요청에 대한 긴 JSON 응답은 이 설명서의 가독성을 높이기 위해 생략되었습니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="68f3b-178">응답에는 사용자가 만든 템플릿 기반 배포에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="68f3b-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68f3b-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68f3b-179">Next steps</span></span>

- <span data-ttu-id="68f3b-180">비동기 REST 작업 처리에 대해 알아보려면 [Azure 비동기 작업 추적](resource-manager-async-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="68f3b-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
