---
title: "Azure Portal에서 배치 계정 만들기 | Microsoft Docs"
description: "클라우드에서 대규모 병렬 작업을 실행하도록 Azure 포털에서 Azure 배치 계정을 만드는 방법에 대해 알아봅니다."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 520d1d42d35b25db1a35d4317e9eb616cf5de565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-batch-account-with-the-azure-portal"></a><span data-ttu-id="30a30-103">Azure Portal에서 Batch 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="30a30-103">Create a Batch account with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="30a30-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="30a30-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="30a30-105">배치 관리 .NET</span><span class="sxs-lookup"><span data-stu-id="30a30-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="30a30-106">[Azure Portal][azure_portal]에 Azure 배치 계정을 만들고 계산 시나리오에 적합한 계정 속성을 선택하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-106">Learn how to create an Azure Batch account in the [Azure portal][azure_portal], and choose the account properties that fit your compute scenario.</span></span> <span data-ttu-id="30a30-107">액세스 키 및 계정 URL과 같은 중요한 계정 속성을 찾는 위치에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-107">Learn where to find important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="30a30-108">배치 계정 및 시나리오에 대한 배경은 [기능 개요](batch-api-basics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-108">For background about Batch accounts and scenarios, see the [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="30a30-109">배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="30a30-109">Create a Batch account</span></span>

<span data-ttu-id="30a30-110">포털을 사용하여 두 개의 *풀 할당 모드*, 즉 **배치 서비스** 모드 또는 더 새로운 **사용자 구독** 모드 중 하나에서 배치 계정을 만들며, 이 경우 더 많은 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-110">Use the portal to create a Batch account in one of the two *pool allocation modes*: **Batch service** mode or the newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="30a30-111">이 두 가지 모드에 대한 내용은 [기능 개요](batch-api-basics.md#account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-111">For information about these two modes, see the [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="30a30-112">사용자 구독 모드의 기능에 대해서는 [블로그 게시물](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-112">For features of the user subscription mode, see also the [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="30a30-113">배치 서비스 모드</span><span class="sxs-lookup"><span data-stu-id="30a30-113">Batch service mode</span></span>



1. <span data-ttu-id="30a30-114">[Azure Portal][azure_portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-114">Sign in to the [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="30a30-115">**새로 만들기** > **계산** > **배치 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Marketplace에서 배치][marketplace_portal]
3. <span data-ttu-id="30a30-117">**새로운 배치 계정** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-117">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="30a30-118">각 블레이드 요소에 대해 아래 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-118">See the descriptions below of each blade element.</span></span>

    ![배치 계정 만들기][account_portal]

    <span data-ttu-id="30a30-120">a.</span><span class="sxs-lookup"><span data-stu-id="30a30-120">a.</span></span> <span data-ttu-id="30a30-121">**계정 이름**: 선택한 배치 계정 이름은 계정을 만든 Azure 지역 내에서 고유해야 합니다(아래 **위치** 참조).</span><span class="sxs-lookup"><span data-stu-id="30a30-121">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="30a30-122">계정 이름은 소문자 또는 숫자만 포함할 수 있으며 길이는 3-24자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-122">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="30a30-123">b.</span><span class="sxs-lookup"><span data-stu-id="30a30-123">b.</span></span> <span data-ttu-id="30a30-124">**구독**: 배치 계정을 만들 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-124">**Subscription**: The subscription in which to create the Batch account.</span></span> <span data-ttu-id="30a30-125">하나의 구독만 보유하는 경우 기본적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="30a30-126">c.</span><span class="sxs-lookup"><span data-stu-id="30a30-126">c.</span></span> <span data-ttu-id="30a30-127">**풀 할당 모드**: **배치 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="30a30-128">c.</span><span class="sxs-lookup"><span data-stu-id="30a30-128">c.</span></span> <span data-ttu-id="30a30-129">**리소스 그룹**: 새 배치 계정에 대한 기존 리소스 그룹을 선택하거나 필요에 따라 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="30a30-130">d.</span><span class="sxs-lookup"><span data-stu-id="30a30-130">d.</span></span> <span data-ttu-id="30a30-131">**위치**: 배치 계정을 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-131">**Location**: The Azure region in which to create the Batch account.</span></span> <span data-ttu-id="30a30-132">구독 및 리소스 그룹에서 지원하는 지역만 옵션으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-132">Only the regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="30a30-133">e.</span><span class="sxs-lookup"><span data-stu-id="30a30-133">e.</span></span> <span data-ttu-id="30a30-134">**저장소 계정**(선택 사항): 배치 계정과 연결하는 범용 Azure Storage 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="30a30-135">대부분의 배치 계정에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="30a30-136">자세한 내용은 이 문서 뒷부분의 [연결된 Azure Storage 계정](#linked-azure-storage-account) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="30a30-137">**만들기** 를 클릭하여 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-137">Click **Create** to create the account.</span></span>

   <span data-ttu-id="30a30-138">포털에서 배포가 진행 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-138">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="30a30-139">완료되면 **알림**에 **배포에 성공했습니다.**라는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="30a30-140">사용자 구독 모드</span><span class="sxs-lookup"><span data-stu-id="30a30-140">User subscription mode</span></span>

### <a name="allow-azure-batch-to-access-the-subscription-one-time-operation"></a><span data-ttu-id="30a30-141">Azure 배치에서 구독에 액세스하도록 허용(일회성 작업)</span><span class="sxs-lookup"><span data-stu-id="30a30-141">Allow Azure Batch to access the subscription (one-time operation)</span></span>
<span data-ttu-id="30a30-142">사용자 구독 모드에서 첫 번째 배치 계정을 만들 때 다음 단계를 수행하여 구독을 배치 계정에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-142">When creating your first Batch account in user subscription mode, perform the following steps to register your subscription with Batch.</span></span> <span data-ttu-id="30a30-143">(이전에 이 작업을 수행한 경우 다음 섹션으로 건너뜁니다.)</span><span class="sxs-lookup"><span data-stu-id="30a30-143">(If you previously did this, skip to the next section.)</span></span>

1. <span data-ttu-id="30a30-144">[Azure Portal][azure_portal]에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-144">Sign in to the [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="30a30-145">**추가 서비스** > **구독**을 차례로 클릭하고, 배치 계정에 사용할 구독을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-145">Click **More Services** > **Subscriptions**, and click the subscription you want to use for the Batch account.</span></span>

3. <span data-ttu-id="30a30-146">**구독** 블레이드에서 **액세스 제어(IAM)** > **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-146">In the **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![구독 액세스 제어][subscription_access]

4. <span data-ttu-id="30a30-148">**권한 추가** 블레이드에서 **참가자** 역할을 선택하고 Batch API를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-148">On the **Add permissions** blade, select the **Contributor** role, search for the Batch API.</span></span> <span data-ttu-id="30a30-149">API를 찾을 때까지 다음 문자열 각각을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-149">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="30a30-150">**MicrosoftAzureBatch**</span><span class="sxs-lookup"><span data-stu-id="30a30-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="30a30-151">**Microsoft Azure Batch** -</span><span class="sxs-lookup"><span data-stu-id="30a30-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="30a30-152">최신 Azure AD 테넌트에서는 이 이름을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="30a30-153">**ddbf3205-c6bd-46ae-8127-60eb93363864**는 Batch API에 대한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 

5. <span data-ttu-id="30a30-154">Batch API를 찾으면 해당 API를 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-154">Once you find the Batch API, select it and click **Save**.</span></span>

    ![배치 권한 추가][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="30a30-156">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="30a30-156">Create a key vault</span></span>
<span data-ttu-id="30a30-157">사용자 구독 모드에서 Azure 키 자격 증명 모음은 만들려는 배치 계정과 동일한 리소스 그룹에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-157">In user subscription mode, an Azure key vault is required that belongs to the same resource group as the Batch account to be created.</span></span> <span data-ttu-id="30a30-158">배치를 [사용할 수 있고](https://azure.microsoft.com/regions/services/) 구독에서 지원하는 지역에 리소스 그룹이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-158">Make sure the resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="30a30-159">[Azure Portal][azure_portal]에서 **새로 만들기** > **보안 + ID** > **Key Vault**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-159">In the [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="30a30-160">**Key Vault 만들기** 블레이드에서 키 자격 증명 모음의 이름을 입력하고, 배치 계정에 사용할 지역에 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-160">In the **Create Key Vault** blade, enter a name for the key vault, and create a resource group in the region you want for your Batch account.</span></span> <span data-ttu-id="30a30-161">나머지 설정은 기본값으로 그대로 두고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-161">Leave the remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="30a30-162">배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="30a30-162">Create a Batch account</span></span>

1. <span data-ttu-id="30a30-163">[Azure Portal][azure_portal]에서 **새로 만들기** > **Compute** > **배치 서비스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-163">In the [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Marketplace에서 배치][marketplace_portal]
3. <span data-ttu-id="30a30-165">**새로운 배치 계정** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-165">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="30a30-166">각 블레이드 요소에 대해 아래 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-166">See the descriptions below of each blade element.</span></span>

    ![배치 계정 만들기][account_portal_byos]

    <span data-ttu-id="30a30-168">a.</span><span class="sxs-lookup"><span data-stu-id="30a30-168">a.</span></span> <span data-ttu-id="30a30-169">**계정 이름**: 선택한 배치 계정 이름은 계정을 만든 Azure 지역 내에서 고유해야 합니다(아래 **위치** 참조).</span><span class="sxs-lookup"><span data-stu-id="30a30-169">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="30a30-170">계정 이름은 소문자 또는 숫자만 포함할 수 있으며 길이는 3-24자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-170">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="30a30-171">b.</span><span class="sxs-lookup"><span data-stu-id="30a30-171">b.</span></span> <span data-ttu-id="30a30-172">**구독**: 둘 이상의 구독이 있는 경우 배치 서비스에 등록한 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-172">**Subscription**: If you have more than one subscription, select the subscription that you registered with the Batch service.</span></span>

    <span data-ttu-id="30a30-173">c.</span><span class="sxs-lookup"><span data-stu-id="30a30-173">c.</span></span> <span data-ttu-id="30a30-174">**풀 할당 모드**: **사용자 구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="30a30-175">d.</span><span class="sxs-lookup"><span data-stu-id="30a30-175">d.</span></span> <span data-ttu-id="30a30-176">**Key Vault**: 이전 섹션에서 배치 계정에 대해 만든 키 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-176">**Key vault**: Select the key vault you created for your Batch account in the previous section.</span></span> <span data-ttu-id="30a30-177">필요에 따라 새 키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="30a30-178">자격 증명 모음을 선택한 후 확인란을 선택하여 해당 키 자격 증명 모음에 Azure 배치 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-178">After selecting the vault, select the checkbox to grant Azure Batch access to the key vault.</span></span>

    <span data-ttu-id="30a30-179">c.</span><span class="sxs-lookup"><span data-stu-id="30a30-179">c.</span></span> <span data-ttu-id="30a30-180">**리소스 그룹**: 키 자격 증명 모음을 만든 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-180">**Resource group**: Select the resource group in which you  created the key vault.</span></span>

    <span data-ttu-id="30a30-181">d.</span><span class="sxs-lookup"><span data-stu-id="30a30-181">d.</span></span> <span data-ttu-id="30a30-182">**위치**: 배치 계정에 대한 키 자격 증명 모음을 만든 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-182">**Location**: The Azure region in which you created the key vault for the Batch account.</span></span>

    <span data-ttu-id="30a30-183">e.</span><span class="sxs-lookup"><span data-stu-id="30a30-183">e.</span></span> <span data-ttu-id="30a30-184">**저장소 계정**(선택 사항): 배치 계정과 연결하는 범용 Azure Storage 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="30a30-185">대부분의 배치 계정에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="30a30-186">자세한 내용은 아래의 [연결된 Azure Storage 계정](#linked-azure-storage-account) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="30a30-187">**만들기** 를 클릭하여 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-187">Click **Create** to create the account.</span></span>

   <span data-ttu-id="30a30-188">포털에서 배포가 진행 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-188">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="30a30-189">완료되면 **알림**에 **배포에 성공했습니다.**라는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="30a30-190">배치 계정 속성 보기</span><span class="sxs-lookup"><span data-stu-id="30a30-190">View Batch account properties</span></span>
<span data-ttu-id="30a30-191">계정이 만들어지면 **배치 계정 블레이드** 를 열어 해당 설정 및 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-191">Once the account has been created, you can open the **Batch account blade** to access its settings and properties.</span></span> <span data-ttu-id="30a30-192">배치 계정 블레이드의 왼쪽 메뉴를 사용하여 모든 계정 설정 및 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-192">You can access all account settings and properties by using the left menu of the Batch account blade.</span></span>

![Azure 포털에서 배치 계정 블레이드][account_blade]

* <span data-ttu-id="30a30-194">**배치 계정 URL**: [배치 API](batch-apis-tools.md#azure-accounts-for-batch-development)로 응용 프로그램을 개발할 때 배치 리소스에 액세스하려면 계정 URL이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-194">**Batch account URL**: When you develop an application with the [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL to access your Batch resources.</span></span> <span data-ttu-id="30a30-195">배치 계정 URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-195">A Batch account URL has the following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![포털에서 배치 계정 URL][account_url]

* <span data-ttu-id="30a30-197">**액세스 키**(배치 서비스 모드): 응용 프로그램에서 배치 계정에 대한 액세스를 인증하려면 계정 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-197">**Access keys** (Batch service mode): To authenticate access to your Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="30a30-198">(Azure Active Directory 인증을 사용하는 사용자 구독 모드에서는 이 설정을 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="30a30-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="30a30-199">배치 계정의 액세스 키를 보거나 다시 생성하려면 배치 계정 블레이드에 있는 왼쪽 메뉴 **검색** 상자에 `keys`를 입력한 다음 **키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-199">To view or regenerate your Batch account's access keys, enter `keys` in the left menu **Search** box on the Batch account blade, then select **Keys**.</span></span>

    ![Azure 포털에서 배치 계정 키][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="30a30-201">연결된 Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="30a30-201">Linked Azure Storage account</span></span>

<span data-ttu-id="30a30-202">필요에 따라 범용 Azure Storage 계정을 배치 계정에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-202">You can optionally link a general-purpose Azure Storage account to your Batch account.</span></span> <span data-ttu-id="30a30-203">배치의 [응용 프로그램 패키지](batch-application-packages.md) 기능은 [배치 파일 규칙 .NET](batch-task-output.md) 라이브러리와 마찬가지로 Azure Blob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-203">The [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does the [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="30a30-204">이러한 선택적 기능은 배치 태스크에서 실행하는 응용 프로그램을 배포하고 생성한 데이터를 유지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-204">These optional features assist you in deploying the applications that your Batch tasks run, and persisting the data they produce.</span></span>

<span data-ttu-id="30a30-205">배치 계정에서 배타적으로 사용할 수 있도록 새로운 저장소 계정을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![범용 저장소 계정 만들기][storage_account]

> [!NOTE]
> <span data-ttu-id="30a30-207">Azure 배치는 현재 범용 저장소 계정 유형만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-207">Azure Batch currently supports only the general-purpose Storage account type.</span></span> <span data-ttu-id="30a30-208">이 계정 유형은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)의 5단계 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="30a30-209">연결된 저장소 계정의 액세스 키를 다시 생성할 때는 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-209">Be careful when regenerating the access keys of a linked Storage account.</span></span> <span data-ttu-id="30a30-210">하나의 저장소 계정 키를 다시 생성하고 연결된 저장소 계정 블레이드에서 **동기화 키** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-210">Regenerate only one Storage account key and click **Sync Keys** on the linked Storage account blade.</span></span> <span data-ttu-id="30a30-211">키를 풀의 계산 노드에 전파한 다음 필요한 경우 다른 키를 다시 생성하고 동기화할 수 있으려면 5분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-211">Wait five minutes to allow the keys to propagate to the compute nodes in your pools, then regenerate and synchronize the other key if necessary.</span></span> <span data-ttu-id="30a30-212">동시에 두 키를 다시 생성하는 경우 계산 노드에서 키를 동기화할 수 없으며 저장소 계정에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-212">If you regenerate both keys at the same time, your compute nodes will not be able to synchronize either key, and they will lose access to the Storage account.</span></span>
>
>

<span data-ttu-id="30a30-213">![ 저장소 계정 키 다시 생성][4]</span><span class="sxs-lookup"><span data-stu-id="30a30-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="30a30-214">배치 서비스 할당량 및 제한</span><span class="sxs-lookup"><span data-stu-id="30a30-214">Batch service quotas and limits</span></span>
<span data-ttu-id="30a30-215">Azure 구독 및 다른 Azure 서비스처럼 특정 [할당량 및 제한](batch-quota-limit.md) 이 배치 계정에 적용되도록 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply to Batch accounts.</span></span> <span data-ttu-id="30a30-216">배치 계정의 현재 할당량이 계정 **속성**의 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-216">Current quotas for a Batch account appear in the portal in the account **Properties**.</span></span>

![Azure 포털에서 배치 계정 할당량][quotas]



<span data-ttu-id="30a30-218">또한 이러한 할당량 대부분은 Azure Portal에 제출된 무료 제품 지원 요청으로 간단히 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in the Azure portal.</span></span> <span data-ttu-id="30a30-219">할당량 증가를 요청하는 방법에 대한 자세한 내용은 [Azure 배치 서비스에 대한 할당량 및 제한](batch-quota-limit.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-219">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="30a30-220">다른 배치 계정 관리 옵션</span><span class="sxs-lookup"><span data-stu-id="30a30-220">Other Batch account management options</span></span>
<span data-ttu-id="30a30-221">Azure 포털을 사용하는 것 외에도 다음 항목으로 배치 계정을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-221">In addition to using the Azure portal, you can also create and manage Batch accounts with the following:</span></span>

* [<span data-ttu-id="30a30-222">배치 PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="30a30-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="30a30-223">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="30a30-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="30a30-224">배치 관리 .NET</span><span class="sxs-lookup"><span data-stu-id="30a30-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="30a30-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30a30-225">Next steps</span></span>
* <span data-ttu-id="30a30-226">배치 서비스의 개념 및 기능에 대한 자세한 내용은 [배치 기능 개요](batch-api-basics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30a30-226">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span></span> <span data-ttu-id="30a30-227">이 문서에서는 풀, 계산 노드, 작업 및 태스크 등의 기본 배치 리소스에 대해 설명하며 대규모 계산 워크로드 실행을 사용할 수 있는 서비스 기능에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-227">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="30a30-228">[배치 .NET 클라이언트 라이브러리](batch-dotnet-get-started.md) 또는 [Python](batch-python-tutorial.md)을 사용하여 배치 지원 응용 프로그램 개발에 대한 기본 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-228">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="30a30-229">이러한 소개 자료에서는 배치 서비스를 사용하여 여러 계산 노드에서 워크로드를 실행하는 작업 응용 프로그램을 단계별로 안내하며, Azure Storage를 사용하여 워크로드 파일을 준비하고 검색하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="30a30-229">These introductory articles guide you through a working application that uses the Batch service to execute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "저장소 계정 키 다시 생성"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
