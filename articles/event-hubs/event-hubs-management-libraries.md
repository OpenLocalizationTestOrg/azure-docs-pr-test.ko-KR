---
title: "Azure Event Hubs 관리 라이브러리 | Microsoft Docs"
description: ".NET에서 Event Hubs 네임스페이스 및 엔터티 관리"
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 0d659cb860a6c98342b548212820efe046decfcc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="c7734-103">Event Hubs 관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="c7734-103">Event Hubs management libraries</span></span>

<span data-ttu-id="c7734-104">Event Hubs 관리 라이브러리는 Event Hubs 네임스페이스 및 엔터티를 동적으로 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-104">The Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="c7734-105">이를 통해 복잡한 배포 및 메시지 시나리오가 가능하며, 어떤 엔터티를 프로비전할 것인지 프로그래밍 방식으로 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span></span> <span data-ttu-id="c7734-106">이러한 라이브러리는 현재 .NET에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="c7734-107">지원되는 기능</span><span class="sxs-lookup"><span data-stu-id="c7734-107">Supported functionality</span></span>

* <span data-ttu-id="c7734-108">네임스페이스 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="c7734-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="c7734-109">Event Hubs 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="c7734-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="c7734-110">소비자 그룹 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="c7734-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7734-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c7734-111">Prerequisites</span></span>

<span data-ttu-id="c7734-112">Event Hubs 관리 라이브러리 사용을 시작하려면 AAD(Azure Active Directory)로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="c7734-113">AAD를 사용하려면 Azure 리소스에 대한 액세스를 제공하는 서비스 주체로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="c7734-114">서비스 주체 만들기에 대한 자세한 내용은 다음 문서 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7734-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="c7734-115">Azure Portal을 사용하여 리소스에 액세스할 수 있는 Active Directory 응용 프로그램 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="c7734-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="c7734-116">Azure PowerShell을 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="c7734-116">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="c7734-117">Azure CLI를 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="c7734-117">Use Azure CLI to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="c7734-118">이러한 자습서는 관리 라이브러리를 통해 인증에 사용되는 `AppId`(클라이언트 ID), `TenantId` 및 `ClientSecret`(인증 키)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="c7734-119">실행하려는 리소스 그룹에 대한 **소유자** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-119">You must have **Owner** permissions for the resource group on which you want to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="c7734-120">프로그래밍 패턴</span><span class="sxs-lookup"><span data-stu-id="c7734-120">Programming pattern</span></span>

<span data-ttu-id="c7734-121">Event Hubs 리소스를 조작하는 패턴은 일반 프로토콜을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="c7734-122">`Microsoft.IdentityModel.Clients.ActiveDirectory` 라이브러리를 사용하여 AAD에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-122">Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="c7734-123">`EventHubManagementClient` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-123">Create the `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="c7734-124">`CreateOrUpdate` 매개 변수를 지정된 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-124">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="c7734-125">호출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7734-125">Execute the call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="c7734-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7734-126">Next steps</span></span>
* [<span data-ttu-id="c7734-127">.NET 관리 샘플</span><span class="sxs-lookup"><span data-stu-id="c7734-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="c7734-128">Microsoft.Azure.Management.EventHub 참조</span><span class="sxs-lookup"><span data-stu-id="c7734-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
