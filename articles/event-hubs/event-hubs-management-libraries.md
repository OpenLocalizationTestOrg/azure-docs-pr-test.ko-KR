---
title: "이벤트 허브 관리 라이브러리에 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="c5146-103">Event Hubs 관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="c5146-103">Event Hubs management libraries</span></span>

<span data-ttu-id="c5146-104">이벤트 허브 네임 스페이스 및 엔터티 hello 이벤트 허브 관리 라이브러리에 동적으로 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="c5146-105">이 통해 복잡 한 배포 및 메시징 시나리오 어떤 엔터티 tooprovision를 프로그래밍 방식으로 확인할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="c5146-106">이러한 라이브러리는 현재 .NET에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="c5146-107">지원되는 기능</span><span class="sxs-lookup"><span data-stu-id="c5146-107">Supported functionality</span></span>

* <span data-ttu-id="c5146-108">네임스페이스 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="c5146-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="c5146-109">Event Hubs 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="c5146-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="c5146-110">소비자 그룹 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="c5146-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5146-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c5146-111">Prerequisites</span></span>

<span data-ttu-id="c5146-112">hello 이벤트 허브 관리 라이브러리를 사용 하 여 시작 tooget와 Azure Active Directory (AAD)를 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="c5146-113">AAD는 액세스 tooyour Azure 리소스를 제공 하는 서비스 주체를 인증 해야 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="c5146-114">서비스 주체 만들기에 대한 자세한 내용은 다음 문서 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5146-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="c5146-115">Hello Azure 포털 toocreate Active Directory 응용 프로그램 및 리소스에 액세스할 수 있는 서비스 보안 주체를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c5146-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="c5146-116">Azure PowerShell toocreate 서비스 보안 주체 tooaccess 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="c5146-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="c5146-117">Azure CLI toocreate 서비스 보안 주체 tooaccess 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="c5146-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="c5146-118">이 자습서를 제공는 `AppId` (클라이언트 ID), `TenantId`, 및 `ClientSecret` (인증 키) hello 관리 라이브러리에서 인증에 사용 되는 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="c5146-119">있어야 **소유자** toorun 원하는 hello 리소스 그룹에 대 한 권한.</span><span class="sxs-lookup"><span data-stu-id="c5146-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="c5146-120">프로그래밍 패턴</span><span class="sxs-lookup"><span data-stu-id="c5146-120">Programming pattern</span></span>

<span data-ttu-id="c5146-121">패턴 toomanipulate hello 모든 이벤트 허브 리소스는 일반적으로 프로토콜을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="c5146-122">Hello를 사용 하 여 AAD에서 토큰을 가져올 `Microsoft.IdentityModel.Clients.ActiveDirectory` 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="c5146-123">Hello 만들기 `EventHubManagementClient` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="c5146-124">집합 hello `CreateOrUpdate` tooyour 매개 변수 값을 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="c5146-125">Hello 호출을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5146-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="c5146-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5146-126">Next steps</span></span>
* [<span data-ttu-id="c5146-127">.NET 관리 샘플</span><span class="sxs-lookup"><span data-stu-id="c5146-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="c5146-128">Microsoft.Azure.Management.EventHub 참조</span><span class="sxs-lookup"><span data-stu-id="c5146-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
