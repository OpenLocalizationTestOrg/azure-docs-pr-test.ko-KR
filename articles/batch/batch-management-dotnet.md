---
title: "for.NET-Azure의 hello 클라이언트 라이브러리를 사용 하 여 aaaManage 일괄 처리 계정 리소스 | Microsoft Docs"
description: "만들기, 삭제 및 hello Batch Management.NET 라이브러리를 사용 하 여 Azure 배치 계정 리소스를 수정 합니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="2f57a-103">.NET에 대 한 일괄 처리 계정 및 hello 일괄 처리 관리 클라이언트 라이브러리와 할당량 관리</span><span class="sxs-lookup"><span data-stu-id="2f57a-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f57a-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2f57a-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="2f57a-105">배치 관리 .NET</span><span class="sxs-lookup"><span data-stu-id="2f57a-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="2f57a-106">낮출 수 있습니다 유지 관리 오버 헤드 Azure 일괄 처리 응용 프로그램에서 hello를 사용 하 여 [Batch Management.NET] [ api_mgmt_net] 라이브러리 tooautomate 일괄 처리 계정 만들기, 삭제, 키 관리 및 할당량 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="2f57a-107">**배치 계정을 만들고 삭제** 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="2f57a-108">제공 하는 경우, 독립 소프트웨어 공급 업체 (ISV)로 예를 들어 있는 각 할당 별도 일괄 처리 계정을 요금 청구를 위해 클라이언트에 대 한 서비스, 계정 만들기 및 삭제 기능 tooyour 고객 포털을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="2f57a-109">**계정 키를 검색하고 다시 생성** 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="2f57a-110">이렇게 하면 주기적인 롤오버 또는 계정 키 만료를 적용하는 보안 정책을 준수할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="2f57a-111">다양한 Azure 영역에 여러 배치 계정이 있는 경우 롤오버 프로세스를 자동화하면 솔루션의 효율성이 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="2f57a-112">**계정 할당량 확인** 하 고 있는 일괄 처리 계정을 어떤 제한 사항이 확인을 hello 시도 오류 예측을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="2f57a-113">작업을 시작하기 전에 계정 할당량을 확인하거나 풀을 만들거나 계산 노드를 추가함으로써 이러한 계산 리소스가 만들어지는 위치 또는 시기를 능동적으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="2f57a-114">해당 계정에 추가 리소스를 할당하기 전에 할당량 증가가 필요한 계정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="2f57a-115">**다른 Azure 서비스의 기능을 결합** -Batch Management.NET을 사용 하 여 완전 한 기능의 관리 환경을 제공 하기 위한 [Azure Active Directory][aad_about], 및 hello [Azure 리소스 관리자] [ resman_overview] hello에서 동일한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="2f57a-116">이러한 기능 및 해당 Api를 사용 하 여 개설 인증 방식으로, 기능 toocreate hello 및 리소스 그룹과 hello 기능을 종단 간 관리 솔루션에 대 한 위에 설명 된 삭제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="2f57a-117">이 문서에서는 일괄 처리 계정, 키 및 할당량 hello 프로그래밍 방식으로 관리할, 동안 대부분 수행할 수 있습니다 이러한 활동의 hello를 사용 하 여 [Azure 포털][azure_portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="2f57a-118">자세한 내용은 참조 [hello Azure 포털을 사용 하 여 Azure 배치 계정 만들기](batch-account-create-portal.md) 및 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="2f57a-119">배치 계정을 만들고 삭제</span><span class="sxs-lookup"><span data-stu-id="2f57a-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="2f57a-120">앞서 언급 했 듯이 hello hello 일괄 처리 관리 API의 기본 기능 중 하나 toocreate 이며 Azure 지역에서 일괄 처리 계정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="2f57a-121">toodo를 사용 하 여 [BatchManagementClient.Account.CreateAsync] [ net_create] 및 [DeleteAsync][net_delete], 또는 동기 대응 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="2f57a-122">hello 다음 코드 조각이 계정을 만들고, 계정 hello 일괄 처리 서비스에서에서 새로 만들어진 hello를 가져오고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="2f57a-123">이 코드 조각에서 다른 사람이이 문서에서는 hello 및 `batchManagementClient` 는 완전히 초기화 된 인스턴스가 [BatchManagementClient][net_mgmt_client]합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="2f57a-124">Hello Batch Management.NET 라이브러리와 BatchManagementClient 클래스를 사용 하는 응용 프로그램에 필요 **서비스 관리자** 또는 **coadministrator** hello를 소유 하 고 있는 toohello 구독 액세스 일괄 처리 계정 toobe 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="2f57a-125">자세한 내용은 참조 hello [Azure Active Directory](#azure-active-directory) 섹션과 hello [AccountManagement] [ acct_mgmt_sample] 코드 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="2f57a-126">계정 키를 검색하고 다시 생성</span><span class="sxs-lookup"><span data-stu-id="2f57a-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="2f57a-127">[ListKeysAsync][net_list_keys]를 사용하여 구독 내 배치 계정에서 기본 및 보조 계정 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="2f57a-128">[RegenerateKeyAsync][net_regenerate_keys]를 사용하여 해당 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="2f57a-129">관리 응용 프로그램에 대한 간소화된 연결 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="2f57a-130">첫째,와 toomanage 원하는 hello 일괄 처리 계정에 대 한 계정 키를 가져올 [ListKeysAsync][net_list_keys]합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="2f57a-131">그런 다음이 키를 사용 하 여 hello 일괄 처리.NET 라이브러리를 초기화할 때 [BatchSharedKeyCredentials] [ net_sharedkeycred] 초기화할 때 사용 되는 클래스 [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="2f57a-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="2f57a-132">Azure 구독 및 배치 계정 할당량 확인</span><span class="sxs-lookup"><span data-stu-id="2f57a-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="2f57a-133">Azure 구독 및 hello 개별 Azure 서비스 모두 일괄 처리와 같은 hello 폴더 내의 특정 엔터티 수를 제한 하는 기본 할당량 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="2f57a-134">Azure 구독에 대 한 기본 할당량 hello에 대 한 참조 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="2f57a-135">Hello 일괄 처리 서비스의 기본 할당량 hello에 대 한 참조 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="2f57a-136">Hello Batch Management.NET 라이브러리를 사용 하 여 응용 프로그램에서 이러한 할당량을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="2f57a-137">이렇게 하면 toomake 할당 결정 하기 전에 계정을 추가 하거나 풀 같은 리소스를 계산 하 고 계산 노드.</span><span class="sxs-lookup"><span data-stu-id="2f57a-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="2f57a-138">Azure 구독에서 배치 계정 할당량 확인</span><span class="sxs-lookup"><span data-stu-id="2f57a-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="2f57a-139">일괄 처리 계정 영역의 만들기 전에 Azure 구독 toosee 수 tooadd 해당 지역에 계정이 있는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="2f57a-140">Hello 아래 코드 조각, 먼저을 사용 하 여 [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget 구독 내에 있는 모든 일괄 처리 계정 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="2f57a-141">이 컬렉션을 얻 었 되 면 hello 대상 영역에 있는 계정의 수을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="2f57a-142">사용 하 여 다음 [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain 배치 계정 할당량 hello 및 계정의 수 (있는 경우) 해당 지역에서 생성할 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="2f57a-143">위의 코드 조각는 hello `creds` 의 인스턴스가 [TokenCloudCredentials][azure_tokencreds]합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="2f57a-144">이 개체를 만드는 예가 toosee 참조 hello [AccountManagement] [ acct_mgmt_sample] GitHub에서 코드 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="2f57a-145">배치 계정에서 계산 리소스 할당량 확인</span><span class="sxs-lookup"><span data-stu-id="2f57a-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="2f57a-146">일괄 처리 솔루션의 계산 리소스를 증가 하기 전에 tooallocate hello 계정 할당량을 초과 하지 않습니다 원하는 tooensure hello 리소스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="2f57a-147">Hello 아래 코드 조각, hello 라는 일괄 처리 계정에 대 한 hello 할당량 정보를 인쇄 하기 `mybatchaccount`합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="2f57a-148">응용 프로그램에서 이러한 정보 toodetermine hello 계정 hello 추가 리소스 toobe 생성을 처리할 수 있는지 여부을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="2f57a-149">Azure 구독 및 서비스에 대 한 기본 할당량 상태인 다양 한 이러한 제한은 발생할 수 있습니다 hello에 요청을 실행 하 여 [Azure 포털][azure_portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="2f57a-150">예를 들어 참조 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md) 배치 계정 할당량 증가에 대 한 지침은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="2f57a-151">Batch Management .NET을 통한 Azure AD 사용</span><span class="sxs-lookup"><span data-stu-id="2f57a-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="2f57a-152">hello Batch Management.NET 라이브러리는 Azure 리소스 공급자 클라이언트 이며와 함께 사용 [Azure 리소스 관리자] [ resman_overview] toomanage 프로그래밍 방식으로 리소스를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="2f57a-153">Azure AD는 필요한 tooauthenticate 요청 및 모든 Azure 리소스 공급자를 포함 한 클라이언트 hello Batch Management.NET 라이브러리를 통해 [Azure 리소스 관리자][resman_overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="2f57a-154">Hello Batch Management.NET 라이브러리와 함께 Azure AD를 사용 하는 방법에 대 한 정보를 참조 하십시오. [tooauthenticate 일괄 처리 솔루션을 사용 하 여 Azure Active Directory](batch-aad-auth.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="2f57a-155">GitHub에서 샘플 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2f57a-155">Sample project on GitHub</span></span>

<span data-ttu-id="2f57a-156">toosee Batch Management.NET 작업에서 체크 아웃 hello [AccountManagment] [ acct_mgmt_sample] GitHub에서 샘플 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="2f57a-157">hello AccountManagment 샘플 응용 프로그램 작업을 수행 하는 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="2f57a-158">[ADAL][aad_adal]을 사용하여 Azure AD에서 보안 토큰을 획득합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="2f57a-159">Hello 사용자 서명 되지 않은 경우 Azure 자격 증명에 대 한 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="2f57a-160">Azure AD에서 가져온 hello 보안 토큰을 사용 하 여 만들는 [SubscriptionClient] [ resman_subclient] tooquery Azure의 hello 계정과 연결 된 구독 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="2f57a-161">둘 이상의 구독이 포함 된 경우 hello 사용자 hello 목록에서 구독을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="2f57a-162">Hello 선택한 구독에 연결 된 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="2f57a-163">만들기는 [ResourceManagementClient] [ resman_client] hello 자격 증명을 사용 하 여 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="2f57a-164">사용 하 여 한 [ResourceManagementClient] [ resman_client] toocreate 리소스 그룹 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="2f57a-165">사용 하 여 한 [BatchManagementClient] [ net_mgmt_client] tooperform 여러 일괄 처리 계정 작업 개체:</span><span class="sxs-lookup"><span data-stu-id="2f57a-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="2f57a-166">Hello 새 리소스 그룹에 일괄 처리 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="2f57a-167">계정 hello 일괄 처리 서비스에서에서 새로 만들어진 hello를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="2f57a-168">Hello 새 계정에 대 한 hello 계정 키를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="2f57a-169">Hello 계정에 대 한 새 기본 키를 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="2f57a-170">Hello 계정에 대 한 hello 할당량 정보를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="2f57a-171">Hello 구독에 대 한 hello 할당량 정보를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="2f57a-172">Hello 구독 내에서 모든 계정을 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="2f57a-173">새로 만든 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-173">Delete newly created account.</span></span>
7. <span data-ttu-id="2f57a-174">Hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-174">Delete hello resource group.</span></span>

<span data-ttu-id="2f57a-175">새로 만든 hello 일괄 처리 계정 및 리소스 그룹을 삭제 하기 전에에서 볼 수 있습니다 이러한 hello [Azure 포털][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="2f57a-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="2f57a-176">toorun hello 샘플 응용 프로그램 성공적으로 먼저 등록 해야 Azure AD 테 넌 트 hello Azure 포털 및 grant 권한 toohello Azure 리소스 관리자 API를에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="2f57a-177">제공 하는 hello 단계를 따라 [Active Directory를 사용 하 여 일괄 처리 관리 인증 솔루션](batch-aad-auth-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f57a-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory란?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD의 인증 시나리오"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Azure Active Directory와 응용 프로그램 통합"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
