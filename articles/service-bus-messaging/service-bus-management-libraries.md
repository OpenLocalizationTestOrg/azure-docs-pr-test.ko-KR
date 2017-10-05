---
title: "Azure Service Bus 관리 라이브러리 | Microsoft Docs"
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
ms.openlocfilehash: 1db00dc1f91e8976b622030450445babbe547ad8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="a9746-103">Service Bus 관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="a9746-103">Service Bus management libraries</span></span>

<span data-ttu-id="a9746-104">Azure Service Bus 관리 라이브러리는 Service Bus 네임스페이스 및 엔터티를 동적으로 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-104">The Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="a9746-105">이를 통해 복잡한 배포 및 메시지 시나리오가 가능하며, 어떤 엔터티를 프로비전할 것인지 프로그래밍 방식으로 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-105">This enables complex deployments and messaging scenarios, and makes it possible to programmatically determine what entities to provision.</span></span> <span data-ttu-id="a9746-106">이러한 라이브러리는 현재 .NET에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="a9746-107">지원되는 기능</span><span class="sxs-lookup"><span data-stu-id="a9746-107">Supported functionality</span></span>

* <span data-ttu-id="a9746-108">네임스페이스 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="a9746-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="a9746-109">큐 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="a9746-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="a9746-110">토픽 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="a9746-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="a9746-111">구독 만들기, 업데이트, 삭제</span><span class="sxs-lookup"><span data-stu-id="a9746-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9746-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a9746-112">Prerequisites</span></span>

<span data-ttu-id="a9746-113">Service Bus 관리 라이브러리 사용을 시작하려면 AAD(Azure Active Directory) 서비스로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-113">To get started using the Service Bus management libraries, you must authenticate with the Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="a9746-114">AAD를 사용하려면 Azure 리소스에 대한 액세스를 제공하는 서비스 주체로 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-114">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="a9746-115">서비스 주체 만들기에 대한 자세한 내용은 다음 문서 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9746-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="a9746-116">Azure Portal을 사용하여 리소스에 액세스할 수 있는 Active Directory 응용 프로그램 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="a9746-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="a9746-117">Azure PowerShell을 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="a9746-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="a9746-118">Azure CLI를 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="a9746-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="a9746-119">이러한 자습서는 관리 라이브러리를 통해 인증에 사용되는 `AppId`(클라이언트 ID), `TenantId` 및 `ClientSecret`(인증 키)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="a9746-120">실행하려는 리소스 그룹에 대한 **소유자** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-120">You must have **Owner** permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="a9746-121">프로그래밍 패턴</span><span class="sxs-lookup"><span data-stu-id="a9746-121">Programming pattern</span></span>

<span data-ttu-id="a9746-122">Service Bus 리소스를 조작하는 패턴은 일반 프로토콜을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="a9746-123">**Microsoft.IdentityModel.Clients.ActiveDirectory** 라이브러리를 사용하여 Azure Active Directory에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="a9746-124">`ServiceBusManagementClient` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-124">Create the `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="a9746-125">`CreateOrUpdate` 매개 변수를 지정된 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="a9746-126">호출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a9746-126">Execute the call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="a9746-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9746-127">Next steps</span></span>
* [<span data-ttu-id="a9746-128">.NET 관리 샘플</span><span class="sxs-lookup"><span data-stu-id="a9746-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="a9746-129">Microsoft.Azure.Management.ServiceBus API 참조</span><span class="sxs-lookup"><span data-stu-id="a9746-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
