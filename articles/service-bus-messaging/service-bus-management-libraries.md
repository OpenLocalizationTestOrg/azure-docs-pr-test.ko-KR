---
title: "서비스 버스 관리 라이브러리 aaaAzure | Microsoft Docs"
description: ".NET에서 Service Bus 네임스페이스 및 메시징 엔터티 관리"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="5b398-103">Service Bus 관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="5b398-103">Service Bus management libraries</span></span>

<span data-ttu-id="5b398-104">서비스 버스 네임 스페이스 및 엔터티 hello Azure 서비스 버스 관리 라이브러리에 동적으로 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="5b398-105">이 복잡 한 배포 및 메시징 시나리오를 활성화 하 고 가능한 tooprogrammatically 어떤 엔터티 tooprovision를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="5b398-106">이러한 라이브러리는 현재 .NET에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="5b398-107">지원되는 기능</span><span class="sxs-lookup"><span data-stu-id="5b398-107">Supported functionality</span></span>

* <span data-ttu-id="5b398-108">네임스페이스 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="5b398-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="5b398-109">큐 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="5b398-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="5b398-110">토픽 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="5b398-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="5b398-111">구독 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="5b398-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b398-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5b398-112">Prerequisites</span></span>

<span data-ttu-id="5b398-113">hello 서비스 버스 관리 라이브러리를 사용 하 여 시작 tooget, Azure Active Directory (AAD) 서비스 hello로 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="5b398-114">AAD는 액세스 tooyour Azure 리소스를 제공 하는 서비스 주체를 인증 해야 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="5b398-115">서비스 주체 만들기에 대한 자세한 내용은 다음 문서 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b398-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="5b398-116">Hello Azure 포털 toocreate Active Directory 응용 프로그램 및 리소스에 액세스할 수 있는 서비스 보안 주체를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5b398-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="5b398-117">Azure PowerShell toocreate 서비스 보안 주체 tooaccess 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="5b398-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="5b398-118">Azure CLI toocreate 서비스 보안 주체 tooaccess 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="5b398-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="5b398-119">이 자습서를 제공는 `AppId` (클라이언트 ID), `TenantId`, 및 `ClientSecret` (인증 키) hello 관리 라이브러리에서 인증에 사용 되는 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="5b398-120">있어야 **소유자** toorun 원하는 hello 리소스 그룹에 대 한 권한.</span><span class="sxs-lookup"><span data-stu-id="5b398-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="5b398-121">프로그래밍 패턴</span><span class="sxs-lookup"><span data-stu-id="5b398-121">Programming pattern</span></span>

<span data-ttu-id="5b398-122">패턴 toomanipulate hello 서비스 버스 리소스는 일반적으로 프로토콜을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="5b398-123">Hello를 사용 하 여 Azure Active Directory에서 토큰을 가져올 **Microsoft.IdentityModel.Clients.ActiveDirectory** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="5b398-124">Hello 만들기 `ServiceBusManagementClient` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="5b398-125">집합 hello `CreateOrUpdate` tooyour 매개 변수 값을 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="5b398-126">Hello 호출을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b398-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="5b398-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b398-127">Next steps</span></span>
* [<span data-ttu-id="5b398-128">.NET 관리 샘플</span><span class="sxs-lookup"><span data-stu-id="5b398-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="5b398-129">Microsoft.Azure.Management.ServiceBus API 참조</span><span class="sxs-lookup"><span data-stu-id="5b398-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
