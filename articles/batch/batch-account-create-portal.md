---
title: "hello Azure 포털에에서 포함 된 일괄 처리 계정 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate Azure 배치 계정에 Azure 포털 toorun hello hello 클라우드에서 대규모 병렬 작업에 알아봅니다"
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
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="946d5-103">Azure 포털 hello로 일괄 처리 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="946d5-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="946d5-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="946d5-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="946d5-105">배치 관리 .NET</span><span class="sxs-lookup"><span data-stu-id="946d5-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="946d5-106">Hello에 toocreate Azure 배치 계정 하는 방법에 대해 알아봅니다 [Azure 포털][azure_portal], 계산 시나리오에 맞는 hello 계정 속성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="946d5-107">액세스 키 및 계정 Url toofind 중요 한 계정 속성의 같은 위치에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="946d5-108">일괄 처리 계정 및 시나리오에 대 한 배경 참조 hello [기능 개요](batch-api-basics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="946d5-109">배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="946d5-109">Create a Batch account</span></span>

<span data-ttu-id="946d5-110">Hello 포털 toocreate 일괄 처리 계정을 사용 하 여 hello 2 중 하나에 *할당 모드 풀*: **서비스 일괄** 모드 또는 최신 hello **사용자 구독** 더 필요한 모드 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="946d5-111">이러한 두 모드에 대 한 정보를 참조 hello [기능 개요](batch-api-basics.md#account)합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="946d5-112">Hello 사용자 구독 모드의 기능에 대 한 참조도 hello [블로그 게시물](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/)합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="946d5-113">배치 서비스 모드</span><span class="sxs-lookup"><span data-stu-id="946d5-113">Batch service mode</span></span>



1. <span data-ttu-id="946d5-114">Toohello 로그인 [Azure 포털][azure_portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="946d5-115">**새로 만들기** > **계산** > **배치 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Hello Marketplace에서에서 일괄 처리][marketplace_portal]
3. <span data-ttu-id="946d5-117">hello **새 일괄 처리 계정** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="946d5-118">각 블레이드 요소의 아래 hello 설명을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="946d5-118">See hello descriptions below of each blade element.</span></span>

    ![배치 계정 만들기][account_portal]

    <span data-ttu-id="946d5-120">a.</span><span class="sxs-lookup"><span data-stu-id="946d5-120">a.</span></span> <span data-ttu-id="946d5-121">**계정 이름**: hello 일괄 처리 계정 이름을 선택 하면 hello hello 계정이 생성 되는 Azure 지역 내에서 고유 해야 합니다. (참조 **위치** 아래).</span><span class="sxs-lookup"><span data-stu-id="946d5-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="946d5-122">hello 계정 이름은 소문자 나 숫자를 포함할 수 있으며 3 ~ 24 자가 하 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="946d5-123">b.</span><span class="sxs-lookup"><span data-stu-id="946d5-123">b.</span></span> <span data-ttu-id="946d5-124">**구독**: hello 어떤 toocreate hello 일괄 처리 계정에서에서 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="946d5-125">하나의 구독만 보유하는 경우 기본적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="946d5-126">c.</span><span class="sxs-lookup"><span data-stu-id="946d5-126">c.</span></span> <span data-ttu-id="946d5-127">**풀 할당 모드**: **배치 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="946d5-128">c.</span><span class="sxs-lookup"><span data-stu-id="946d5-128">c.</span></span> <span data-ttu-id="946d5-129">**리소스 그룹**: 새 배치 계정에 대한 기존 리소스 그룹을 선택하거나 필요에 따라 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="946d5-130">d.</span><span class="sxs-lookup"><span data-stu-id="946d5-130">d.</span></span> <span data-ttu-id="946d5-131">**위치**: hello 어떤 toocreate hello 일괄 처리 계정에에서 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="946d5-132">구독 및 리소스 그룹에서 지 원하는 hello 영역만 옵션으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="946d5-133">e.</span><span class="sxs-lookup"><span data-stu-id="946d5-133">e.</span></span> <span data-ttu-id="946d5-134">**저장소 계정**(선택 사항): 배치 계정과 연결하는 범용 Azure Storage 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="946d5-135">대부분의 배치 계정에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="946d5-136">자세한 내용은 이 문서 뒷부분의 [연결된 Azure Storage 계정](#linked-azure-storage-account) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="946d5-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="946d5-137">클릭 **만들기** toocreate hello 계정.</span><span class="sxs-lookup"><span data-stu-id="946d5-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="946d5-138">hello 포털이 나타냅니다 배포가 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="946d5-139">완료되면 **알림**에 **배포에 성공했습니다.**라는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="946d5-140">사용자 구독 모드</span><span class="sxs-lookup"><span data-stu-id="946d5-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="946d5-141">Azure 배치 tooaccess hello 구독 (일회용 작업) 허용</span><span class="sxs-lookup"><span data-stu-id="946d5-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="946d5-142">사용자 구독 모드에서 첫 번째 일괄 처리 계정을 만든 경우 다음 단계 tooregister hello 일괄 처리와 구독을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="946d5-143">(이전에 동일한 작업을 하는 경우 건너 뛸 toohello 다음.)</span><span class="sxs-lookup"><span data-stu-id="946d5-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="946d5-144">Toohello 로그인 [Azure 포털][azure_portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="946d5-145">클릭 **더 서비스** > **구독**, toouse hello 일괄 처리 계정에 대 한 원하는 hello 구독을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="946d5-146">Hello에 **구독** 블레이드에서 클릭 **액세스 제어 (IAM)** > **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![구독 액세스 제어][subscription_access]

4. <span data-ttu-id="946d5-148">Hello에 **사용 권한을 추가** 블레이드, 선택 hello **참가자** 역할, 일괄 처리 API hello에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="946d5-149">Hello API를 찾을 때까지 이러한 문자열에 대 한 검색:</span><span class="sxs-lookup"><span data-stu-id="946d5-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="946d5-150">**MicrosoftAzureBatch**</span><span class="sxs-lookup"><span data-stu-id="946d5-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="946d5-151">**Microsoft Azure Batch** -</span><span class="sxs-lookup"><span data-stu-id="946d5-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="946d5-152">최신 Azure AD 테넌트에서는 이 이름을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="946d5-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** hello 일괄 처리 API에 대 한 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="946d5-154">일괄 처리 API hello를 찾은 후 선택 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![배치 권한 추가][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="946d5-156">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="946d5-156">Create a key vault</span></span>
<span data-ttu-id="946d5-157">사용자 구독 모드에는 Azure 키 자격 증명 모음 필수가 toothe 속하는 hello 일괄 처리 계정 toobe 만든와 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="946d5-158">Hello 리소스 그룹은 일괄 처리 인 영역에 있는지 확인 [사용 가능한](https://azure.microsoft.com/regions/services/) 및 구독을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="946d5-159">Hello에 [Azure 포털][azure_portal], 클릭 **새로** > **보안 + Id** > **키 자격 증명 모음** .</span><span class="sxs-lookup"><span data-stu-id="946d5-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="946d5-160">Hello에 **키 자격 증명 모음 만들기** 블레이드에서 hello 주요 자격 증명 모음에 대 한 이름을 입력 하 고 일괄 처리 계정에 대해 원하는 hello 지역에서 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="946d5-161">Hello 남은 설정에 기본값을 유지 한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="946d5-162">배치 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="946d5-162">Create a Batch account</span></span>

1. <span data-ttu-id="946d5-163">Hello에 [Azure 포털][azure_portal], 클릭 **새로** > **계산** > **일괄처리서비스**.</span><span class="sxs-lookup"><span data-stu-id="946d5-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Hello Marketplace에서에서 일괄 처리][marketplace_portal]
3. <span data-ttu-id="946d5-165">hello **새 일괄 처리 계정** 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="946d5-166">각 블레이드 요소의 아래 hello 설명을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="946d5-166">See hello descriptions below of each blade element.</span></span>

    ![배치 계정 만들기][account_portal_byos]

    <span data-ttu-id="946d5-168">a.</span><span class="sxs-lookup"><span data-stu-id="946d5-168">a.</span></span> <span data-ttu-id="946d5-169">**계정 이름**: hello 일괄 처리 계정 이름을 선택 하면 hello hello 계정이 생성 되는 Azure 지역 내에서 고유 해야 합니다. (참조 **위치** 아래).</span><span class="sxs-lookup"><span data-stu-id="946d5-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="946d5-170">hello 계정 이름은 소문자 나 숫자를 포함할 수 있으며 3 ~ 24 자가 하 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="946d5-171">b.</span><span class="sxs-lookup"><span data-stu-id="946d5-171">b.</span></span> <span data-ttu-id="946d5-172">**구독**: 둘 이상의 구독이 있는 경우 hello 일괄 처리 서비스에 등록 하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="946d5-173">c.</span><span class="sxs-lookup"><span data-stu-id="946d5-173">c.</span></span> <span data-ttu-id="946d5-174">**풀 할당 모드**: **사용자 구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="946d5-175">d.</span><span class="sxs-lookup"><span data-stu-id="946d5-175">d.</span></span> <span data-ttu-id="946d5-176">**주요 자격 증명 모음**: 선택 hello 주요 자격 증명 모음 hello 이전 섹션에서 일괄 처리 계정에 대해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="946d5-177">필요에 따라 새 키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="946d5-178">Hello 자격 증명 모음을 선택한 후 hello 확인란 toogrant Azure 배치 액세스 toohello 주요 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="946d5-179">c.</span><span class="sxs-lookup"><span data-stu-id="946d5-179">c.</span></span> <span data-ttu-id="946d5-180">**리소스 그룹**: hello 주요 자격 증명 모음을 만든 선택 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="946d5-181">d.</span><span class="sxs-lookup"><span data-stu-id="946d5-181">d.</span></span> <span data-ttu-id="946d5-182">**위치**: hello hello 일괄 처리 계정에 대 한 hello에 키 자격 증명 모음.를 만든 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="946d5-183">e.</span><span class="sxs-lookup"><span data-stu-id="946d5-183">e.</span></span> <span data-ttu-id="946d5-184">**저장소 계정**(선택 사항): 배치 계정과 연결하는 범용 Azure Storage 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="946d5-185">대부분의 배치 계정에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="946d5-186">자세한 내용은 아래의 [연결된 Azure Storage 계정](#linked-azure-storage-account) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="946d5-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="946d5-187">클릭 **만들기** toocreate hello 계정.</span><span class="sxs-lookup"><span data-stu-id="946d5-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="946d5-188">hello 포털이 나타냅니다 배포가 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="946d5-189">완료되면 **알림**에 **배포에 성공했습니다.**라는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="946d5-190">배치 계정 속성 보기</span><span class="sxs-lookup"><span data-stu-id="946d5-190">View Batch account properties</span></span>
<span data-ttu-id="946d5-191">Hello 계정이 생성 된 후 hello를 열 수 있습니다 **일괄 처리 계정 블레이드** tooaccess 설정 및 속성에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="946d5-192">Hello 일괄 처리 계정 블레이드의 hello 왼쪽된 메뉴를 사용 하 여 모든 계정 설정 및 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Azure 포털에서 배치 계정 블레이드][account_blade]

* <span data-ttu-id="946d5-194">**계정 URL을 일괄 처리**: hello로 응용 프로그램을 개발 하는 경우 [일괄 처리 Api](batch-apis-tools.md#azure-accounts-for-batch-development), 계정 URL tooaccess 일괄 처리 리소스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="946d5-195">일괄 처리 계정 URL 형식에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![포털에서 배치 계정 URL][account_url]

* <span data-ttu-id="946d5-197">**액세스 키** (일괄 처리 서비스 모드): tooauthenticate 액세스 tooyour 일괄 처리 계정 응용 프로그램에서 계정 액세스 키 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="946d5-198">(Azure Active Directory 인증을 사용하는 사용자 구독 모드에서는 이 설정을 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="946d5-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="946d5-199">일괄 처리 계정 액세스 키를 입력 tooview 또는 regenerate `keys` hello 왼쪽된 메뉴에 **검색** hello 일괄 처리 계정 블레이드에서 상자 다음 선택 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Azure 포털에서 배치 계정 키][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="946d5-201">연결된 Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="946d5-201">Linked Azure Storage account</span></span>

<span data-ttu-id="946d5-202">필요에 따라 범용 Azure 저장소 계정 tooyour 일괄 처리 계정을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="946d5-203">hello [응용 프로그램 패키지](batch-application-packages.md) 일괄 처리의 기능은 hello와 마찬가지로 Azure Blob 저장소를 사용 하 여 [일괄 처리 파일 규칙.NET](batch-task-output.md) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="946d5-204">이러한 옵션 기능 일괄 처리 작업을 실행 하는 hello 응용 프로그램 배포 및 생성 하는 hello 데이터 유지 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="946d5-205">배치 계정에서 배타적으로 사용할 수 있도록 새로운 저장소 계정을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![범용 저장소 계정 만들기][storage_account]

> [!NOTE]
> <span data-ttu-id="946d5-207">Azure 일괄 처리에는 현재 hello 일반적인 용도의 스토리지 계정 유형만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="946d5-208">이 계정 유형은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)의 5단계 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)에서 설명하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="946d5-209">연결 된 저장소 계정의 hello 선택 키를 다시 생성할 때는 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="946d5-210">하나의 저장소 계정 키를 다시 생성 하 고 클릭 **키 동기화** hello에 저장소 계정 블레이드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="946d5-211">5 분 tooallow hello 키 toopropagate toohello 프로그램 풀의 계산 노드를 다시 생성 하 고 동기화 대기 hello 필요한 경우 다른 키입니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="946d5-212">모두 다시 생성 하는 경우 키 hello에서 동일한 시간, 계산 노드 수 toosynchronize 어느 키 수 없게 되 고 toohello 저장소 계정 액세스를 잃게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="946d5-213">![ 저장소 계정 키 다시 생성][4]</span><span class="sxs-lookup"><span data-stu-id="946d5-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="946d5-214">배치 서비스 할당량 및 제한</span><span class="sxs-lookup"><span data-stu-id="946d5-214">Batch service quotas and limits</span></span>
<span data-ttu-id="946d5-215">있는지와 Azure 구독 및 기타 Azure 서비스 인식, 특정 사항은 [할당량 및 제한](batch-quota-limit.md) tooBatch 계정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="946d5-216">일괄 처리 계정에 대 한 현재 할당량 hello 계정에서 hello 포털에 나타나는 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Azure 포털에서 배치 계정 할당량][quotas]



<span data-ttu-id="946d5-218">또한 이러한 할당량 중 많은 hello Azure 포털에에서 제출 된 무료 제품 지원 요청으로 간단히 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="946d5-219">참조 [할당량과 hello Azure 배치 서비스에 대 한 제한을](batch-quota-limit.md) 할당량 증가 요청에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="946d5-220">다른 배치 계정 관리 옵션</span><span class="sxs-lookup"><span data-stu-id="946d5-220">Other Batch account management options</span></span>
<span data-ttu-id="946d5-221">또한 toousing hello Azure 포털, 만들고 및 hello 다음과 같이 일괄 처리 계정을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="946d5-222">배치 PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="946d5-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="946d5-223">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="946d5-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="946d5-224">배치 관리 .NET</span><span class="sxs-lookup"><span data-stu-id="946d5-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="946d5-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="946d5-225">Next steps</span></span>
* <span data-ttu-id="946d5-226">Hello 참조 [배치 기능 개요](batch-api-basics.md) toolearn 일괄 처리 서비스 개념 및 기능에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="946d5-227">hello 문서 hello 기본 일괄 처리 리소스 풀, 계산 노드, 작업, 작업 등을 설명 하 고 대규모 계산 작업 실행을 사용할 수 있는 서비스의 기능 hello에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="946d5-228">Hello를 사용 하 여 일괄 처리 사용이 가능한 응용 프로그램 개발의 hello 기본 사항 알아보기 [일괄 처리.NET 클라이언트 라이브러리](batch-dotnet-get-started.md) 또는 [Python](batch-python-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="946d5-229">이러한 소개 문서 여러 계산 노드에 hello 일괄 처리 서비스 tooexecute 작업을 사용 하 고 Azure 저장소를 사용 하 여 작업 파일 준비 및 검색을 포함 하는 작업 중인 응용 프로그램을 안내해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="946d5-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

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
