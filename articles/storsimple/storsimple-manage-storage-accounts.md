---
title: "StorSimple 저장소 계정 관리 | Microsoft Docs"
description: "StorSimple 관리자 구성 페이지를 사용하여 저장소 계정에 대한 보안 키를 추가, 편집, 삭제 또는 회전하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 68b767c9c93f2daff476a21029b9813f347590b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-storage-account"></a><span data-ttu-id="4979d-103">StorSimple 관리자 서비스를 사용하여 저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="4979d-103">Use the StorSimple Manager service to manage your storage account</span></span>
## <a name="overview"></a><span data-ttu-id="4979d-104">개요</span><span class="sxs-lookup"><span data-stu-id="4979d-104">Overview</span></span>
<span data-ttu-id="4979d-105">**구성** 페이지는 StorSimple 관리자 서비스에서 만들 수 있는 모든 글로벌 서비스 매개 변수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-105">The **Configure** page presents all the global service parameters that can be created in the StorSimple Manager service.</span></span> <span data-ttu-id="4979d-106">이러한 매개 변수는 서비스에 연결된 모든 장치에 적용할 수 있으며 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-106">These parameters can be applied to all the devices connected to the service, and include:</span></span>

* <span data-ttu-id="4979d-107">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="4979d-107">Storage accounts</span></span> 
* <span data-ttu-id="4979d-108">대역폭 템플릿</span><span class="sxs-lookup"><span data-stu-id="4979d-108">Bandwidth templates</span></span> 
* <span data-ttu-id="4979d-109">액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="4979d-109">Access control records</span></span> 

<span data-ttu-id="4979d-110">이 자습서에서는 **구성** 페이지를 사용하여 저장소 계정을 추가, 편집 또는 삭제하거나, 저장소 계정에 대한 보안 키를 회전하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-110">This tutorial explains how you can use the **Configure** page to add, edit, or delete storage accounts, or rotate the security keys for a storage account.</span></span>

 ![구성 페이지](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

<span data-ttu-id="4979d-112">저장소 계정은 클라우드 서비스 공급자와 저장소 계정에 액세스하기 위해 장치가 사용하는 자격 증명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-112">Storage accounts contain the credentials that the device uses to access your storage account with your cloud service provider.</span></span> <span data-ttu-id="4979d-113">Microsoft Azure 저장소 계정의 경우 계정 이름 및 기본 액세스 키와 같은 자격 증명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-113">For Microsoft Azure storage accounts, these are credentials such as the account name and the primary access key.</span></span> 

<span data-ttu-id="4979d-114">**구성** 페이지에서 청구 구독에 대해 만들어진 모든 저장소 계정이 다음 정보를 포함하여 테이블 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-114">On the **Configure** page, all storage accounts that are created for the billing subscription are displayed in a tabular format containing the following information:</span></span>

* <span data-ttu-id="4979d-115">**이름** – 만들어졌을 때 계정에 할당된 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-115">**Name** – The unique name assigned to the account when it was created.</span></span>
* <span data-ttu-id="4979d-116">**SSL 사용** – SSL 사용 및 장치와 클라우드 사이의 통신이 보안 채널을 통해 이루어지는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-116">**SSL enabled** – Whether the SSL is enabled and device-to-cloud communication is over the secure channel.</span></span>
* <span data-ttu-id="4979d-117">**사용 볼륨** – 저장소 계정을 사용하는 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-117">**Used by** – The number of volumes using the storage account.</span></span>

<span data-ttu-id="4979d-118">저장소 계정 관련하여 **구성** 페이지에서 수행할 수 있는 가장 일반적인 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-118">The most common tasks related to storage accounts that can be performed on the **Configure** page are:</span></span>

* <span data-ttu-id="4979d-119">저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="4979d-119">Add a storage account</span></span> 
* <span data-ttu-id="4979d-120">저장소 계정 편집</span><span class="sxs-lookup"><span data-stu-id="4979d-120">Edit a storage account</span></span> 
* <span data-ttu-id="4979d-121">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="4979d-121">Delete a storage account</span></span> 
* <span data-ttu-id="4979d-122">저장소 계정의 키 회전</span><span class="sxs-lookup"><span data-stu-id="4979d-122">Key rotation of storage accounts</span></span> 

## <a name="types-of-storage-accounts"></a><span data-ttu-id="4979d-123">저장소 계정 유형</span><span class="sxs-lookup"><span data-stu-id="4979d-123">Types of storage accounts</span></span>
<span data-ttu-id="4979d-124">StorSimple 장치에서 사용할 수 있는 저장소 계정에는 다음과 같은 세 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-124">There are three types of storage accounts that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="4979d-125">**자동 생성된 저장소 계정** – 이름 제안 시, 서비스를 처음 만들 때 이 저장소 계정 유형이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-125">**Auto-generated storage accounts** – As the name suggests, this type of storage account is automatically generated when the service is first created.</span></span> <span data-ttu-id="4979d-126">이 저장소 계정을 만드는 방법에 대해 자세히 알아보려면 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough.md)에서 [1단계: 새 서비스 만들기](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4979d-126">To learn more about how this storage account is created, see [Step 1: Create a new service](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) in [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough.md).</span></span> 
* <span data-ttu-id="4979d-127">**서비스 구독의 저장소 계정** – 이러한 계정은 서비스와 동일한 구독과 연결된 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-127">**Storage accounts in the service subscription** – These are the Azure storage accounts that are associated with the same subscription as that of the service.</span></span> <span data-ttu-id="4979d-128">이러한 저장소 계정을 만드는 방법에 대해 더 알아보려면 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4979d-128">To learn more about how these storage accounts are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span> 
* <span data-ttu-id="4979d-129">**서비스 구독 외의 저장소 계정** - 이러한 계정은 서비스와 연결되지 않았고 서비스가 만들어지기 전에 존재했던 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-129">**Storage accounts outside of the service subscription** – These are the Azure storage accounts that are not associated with your service and likely existed before the service was created.</span></span>

## <a name="add-a-storage-account"></a><span data-ttu-id="4979d-130">저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="4979d-130">Add a storage account</span></span>
<span data-ttu-id="4979d-131">저장소 계정(지정된 클라우드 서비스 공급자를 통해)에 연결된 액세스 자격 증명 및 친숙한 고유 이름을 제공하여 저장소 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-131">You can add a storage account by providing a unique friendly name and access credentials that are linked to the storage account (with the specified cloud service provider).</span></span> <span data-ttu-id="4979d-132">장치와 클라우드 사이에서 네트워크 통신을 위한 보안 채널을 만들기 위해 SSL(Secure Sockets Layer) 모드를 사용하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-132">You also have the option of enabling the secure sockets layer (SSL) mode to create a secure channel for network communication between your device and the cloud.</span></span>

<span data-ttu-id="4979d-133">특정 클라우드 서비스 공급자에 대해 여러 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="4979d-134">하지만 저장소 계정을 만든 후에는 클라우드 서비스 공급자를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-134">Be aware, however, that after a storage account is created, you cannot change the cloud service provider.</span></span>

<span data-ttu-id="4979d-135">저장소 계정을 저장하는 동안 해당 서비스는 클라우드 서비스 공급자와 통신을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-135">While the storage account is being saved, the service attempts to communicate with your cloud service provider.</span></span> <span data-ttu-id="4979d-136">사용자가 지정한 자격 증명 및 액세스 자료가 이 때 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-136">The credentials and the access material that you supplied will be authenticated at this time.</span></span> <span data-ttu-id="4979d-137">인증에 성공하는 경우에만 저장소 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-137">A storage account is created only if the authentication succeeds.</span></span> <span data-ttu-id="4979d-138">인증에 실패하는 경우 그에 따른 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-138">If the authentication fails, then an appropriate error message will be displayed.</span></span>

<span data-ttu-id="4979d-139">Azure 포털에서 만든 Resource Manager 저장소 계정은 StorSimple에서도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-139">Resource Manager storage accounts created in Azure portal are also supported with StorSimple.</span></span> <span data-ttu-id="4979d-140">Resource Manager 저장소 계정은 볼륨 컨테이너를 만들려고 할 때 드롭다운 목록에서 선택할 수 있도록 표시되지 않으며, Azure 클래식 포털에서 만든 저장소 계정만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-140">The Resource Manager storage accounts will not show up in the drop-down list for selection when trying to create a volume container, only the storage accounts created in the Azure classic portal will be displayed.</span></span> <span data-ttu-id="4979d-141">아래에 설명된 저장소 계정 추가 절차에 따라 Resource Manager 저장소 계정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-141">Resource Manager storage accounts will need to be added using the procedure to add a storage account described below.</span></span>

> [!NOTE]
> <span data-ttu-id="4979d-142">저장소 계정을 추가하기 위한 절차는 사용하는 StorSimple 소프트웨어 버전에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-142">The procedure for adding a storage account differs based on the StorSimple software version you are using.</span></span> <span data-ttu-id="4979d-143">StorSimple 버전에 대한 올바른 절차를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-143">Be sure to follow the correct procedure for your StorSimple version.</span></span>
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a><span data-ttu-id="4979d-144">저장소 계정 편집</span><span class="sxs-lookup"><span data-stu-id="4979d-144">Edit a storage account</span></span>
<span data-ttu-id="4979d-145">볼륨 컨테이너에서 사용되는 저장소 계정을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-145">You can edit a storage account that is used by a volume container.</span></span> <span data-ttu-id="4979d-146">현재 사용 중인 저장소 계정을 편집할 경우 수정할 수 있는 유일한 필드는 저장소 계정에 대한 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-146">If you edit a storage account that is currently in use, the only field available to modify is the access key for the storage account.</span></span> <span data-ttu-id="4979d-147">새 저장소 액세스 키를 제공할 수 있으며 업데이트된 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-147">You can supply the new storage access key and save the updated settings.</span></span>

#### <a name="to-edit-a-storage-account"></a><span data-ttu-id="4979d-148">저장소 계정을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="4979d-148">To edit a storage account</span></span>
1. <span data-ttu-id="4979d-149">서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-149">On the service landing page, select your service, double-click the service name, and then click **Configure**.</span></span>
2. <span data-ttu-id="4979d-150">**저장소 계정 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-150">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="4979d-151">**저장소 계정 추가/편집** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="4979d-151">In the **Add/Edit Storage Accounts** dialog box:</span></span>
   
   1. <span data-ttu-id="4979d-152">**저장소 계정**드롭다운 목록에서 수정하려는 기존 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-152">In the drop-down list of **Storage Accounts**, choose an existing account that you would like to modify.</span></span> <span data-ttu-id="4979d-153">서비스를 처음 만들 때 자동으로 생성된 저장소 계정이 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-153">This could also include the storage accounts that were automatically generated when the service was first created.</span></span>
   2. <span data-ttu-id="4979d-154">필요에 따라 **SSL 모드 사용** 선택을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-154">If necessary, you can modify the **Enable SSL Mode** selection.</span></span>
   3. <span data-ttu-id="4979d-155">저장소 계정 액세스 키를 회전하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-155">You can choose to rotate your storage account access keys.</span></span> <span data-ttu-id="4979d-156">키 회전을 수행하는 방법에 대한 자세한 내용은 [저장소 계정의 키 회전](#key-rotation-of-storage-accounts) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4979d-156">See [Key rotation of storage accounts](#key-rotation-of-storage-accounts) for more information about how to perform key rotation.</span></span>
   4. <span data-ttu-id="4979d-157">확인 아이콘 ![확인 아이콘](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) 을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-157">Click the check icon ![check icon](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) to save the settings.</span></span> <span data-ttu-id="4979d-158">설정은 **구성** 페이지에서 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-158">The settings will be updated on the **Configure** page.</span></span> <span data-ttu-id="4979d-159">**저장** 을 클릭하여 새로 업데이트된 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-159">Click **Save** to save the newly updated settings.</span></span>
      
      ![저장소 계정 편집](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a><span data-ttu-id="4979d-161">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="4979d-161">Delete a storage account</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4979d-162">볼륨 컨테이너에서 사용하지 않는 경우에만 저장소 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-162">You can delete a storage account only if it is not used by a volume container.</span></span> <span data-ttu-id="4979d-163">저장소 계정을 볼륨 컨테이너에서 사용 중인 경우 먼저 볼륨 컨테이너를 삭제하고 연결된 저장소 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-163">If a storage account is being used by a volume container, first delete the volume container and then delete the associated storage account.</span></span>
> 
> 

#### <a name="to-delete-a-storage-account"></a><span data-ttu-id="4979d-164">저장소 계정을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="4979d-164">To delete a storage account</span></span>
1. <span data-ttu-id="4979d-165">StorSimple 관리자 서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-165">On the StorSimple Manager service landing page, select your service, double-click the service name, and then click **Configure**.</span></span>
2. <span data-ttu-id="4979d-166">저장소 계정의 테이블 형식 목록에서 삭제하려는 계정을 마우스로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-166">In the tabular list of storage accounts, hover over the account that you wish to delete.</span></span>
3. <span data-ttu-id="4979d-167">삭제 아이콘(**x**)이 해당 저장소 계정의 맨 오른쪽 열에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-167">A delete icon (**x**) will appear in the extreme right column for that storage account.</span></span> <span data-ttu-id="4979d-168">**x** 아이콘을 클릭하여 자격 증명을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-168">Click the **x** icon to delete the credentials.</span></span>
4. <span data-ttu-id="4979d-169">확인 메시지가 나타나면 **예** 를 클릭하여 삭제를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-169">When prompted for confirmation, click **Yes** to continue with the deletion.</span></span> <span data-ttu-id="4979d-170">테이블 형식 목록이 변경 내용을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-170">The tabular listing will be updated to reflect the changes.</span></span>

## <a name="key-rotation-of-storage-accounts"></a><span data-ttu-id="4979d-171">저장소 계정의 키 회전</span><span class="sxs-lookup"><span data-stu-id="4979d-171">Key rotation of storage accounts</span></span>
<span data-ttu-id="4979d-172">보안상의 이유로 키 회전이 데이터 센터에서 요구되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-172">For security reasons, key rotation is often a requirement in data centers.</span></span> 

> [!NOTE]
> <span data-ttu-id="4979d-173">다음의 키 회전 정보 및 회전 절차는 Microsoft Azure 저장소 계정에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-173">The following key rotation information and the rotation procedure apply to Microsoft Azure storage accounts only.</span></span> <span data-ttu-id="4979d-174">다른 클라우드 서비스 공급자를 사용하는 경우에 해당 공급자의 대시보드를 통해 저장소 계정 키를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-174">If you are using another cloud service provider, you can manage storage account keys through that provider's dashboard.</span></span>
> 
> 

<span data-ttu-id="4979d-175">각 Microsoft Azure 구독에 하나 이상의 연결된 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-175">Each Microsoft Azure subscription can have one or more associated storage accounts.</span></span> <span data-ttu-id="4979d-176">이러한 계정에 대한 액세스는 해당 저장소 계정에 대한 구독 및 액세스 키를 통해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-176">The access to these accounts is controlled by the subscription and access keys for each storage account.</span></span> 

<span data-ttu-id="4979d-177">저장소 계정을 만들면 Microsoft Azure에서 두 개의 512비트 저장소 액세스 키를 생성합니다. 이 키는 저장소 계정에 액세스하는 경우 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-177">When you create a storage account, Microsoft Azure generates two 512-bit storage access keys that are used for authentication when the storage account is accessed.</span></span> <span data-ttu-id="4979d-178">두 개의 저장소 액세스 키가 있으면 저장소 서비스나 해당 서비스에 대한 액세스에 중단 없이 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-178">Having two storage access keys allows you to regenerate the keys with no interruption to your storage service or access to that service.</span></span> <span data-ttu-id="4979d-179">현재 사용 중인 키는 *기본* 키이며 백업 키는 *보조* 키라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-179">The key that is currently in use is the *primary* key and the backup key is referred to as the *secondary* key.</span></span> <span data-ttu-id="4979d-180">Microsoft Azure StorSimple 장치가 클라우드 저장소 서비스 공급자에 액세스할 때 이러한 두 키 중 하나를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-180">One of these two keys must be supplied when your Microsoft Azure StorSimple device accesses your cloud storage service provider.</span></span>

## <a name="what-is-key-rotation"></a><span data-ttu-id="4979d-181">키 회전 정의</span><span class="sxs-lookup"><span data-stu-id="4979d-181">What is key rotation?</span></span>
<span data-ttu-id="4979d-182">일반적으로 응용 프로그램은 데이터 액세스에 키 중 하나만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-182">Typically, applications use only one of the keys to access your data.</span></span> <span data-ttu-id="4979d-183">특정 시간이 지나면 응용 프로그램이 두 번째 키를 사용하도록 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-183">After a certain period of time, you can have your applications switch over to using the second key.</span></span> <span data-ttu-id="4979d-184">두 번째 키로 응용 프로그램을 전환한 후 첫 번째 키를 사용 중지한 다음 새 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-184">After you have switched your applications to the secondary key, you can retire the first key and then generate a new key.</span></span> <span data-ttu-id="4979d-185">이러한 방식으로 두 키를 사용하면 가동 중지 시간 없이 응용 프로그램이 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-185">Using the two keys this way allows your applications access to the data without incurring any downtime.</span></span>

<span data-ttu-id="4979d-186">저장소 계정 키는 항상 암호화된 형태로 서비스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-186">The storage account keys are always stored in the service in an encrypted form.</span></span> <span data-ttu-id="4979d-187">하지만 StorSimple 관리자 서비스를 통해 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-187">However, these can be reset via the StorSimple Manager service.</span></span> <span data-ttu-id="4979d-188">서비스는 StorSimple 관리자 서비스를 처음 만들 때 생성한 기본 저장소 계정뿐 아니라 저장소 계정에서 만든 계정을 비롯하여 동일한 구독의 모든 저장소 계정에 대해 기본 키 및 보조 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-188">The service can get the primary key and secondary key for all the storage accounts in the same subscription, including accounts created in the Storage service as well as the default storage accounts generated when the StorSimple Manager service service was first created.</span></span> <span data-ttu-id="4979d-189">StorSimple 관리자 서비스는 Azure 클래식 포털에서 항상 이러한 키를 가져와 암호화된 방법으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-189">The StorSimple Manager service service will always get these keys from the Azure classic portal and then store them in an encrypted manner.</span></span>

## <a name="rotation-workflow"></a><span data-ttu-id="4979d-190">회전 워크플로</span><span class="sxs-lookup"><span data-stu-id="4979d-190">Rotation workflow</span></span>
<span data-ttu-id="4979d-191">Microsoft Azure 관리자가 저장소 계정에 직접 액세스하여(Microsoft Azure 저장소 서비스를 통해) 기본 키 또는 보조 키를 다시 생성하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-191">A Microsoft Azure administrator can regenerate or change the primary or secondary key by directly accessing the storage account (via the Microsoft Azure Storage service).</span></span> <span data-ttu-id="4979d-192">StorSimple 관리자 서비스는이 변경을 자동으로 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-192">The StorSimple Manager service does not see this change automatically.</span></span>

<span data-ttu-id="4979d-193">StorSimple 관리자 서비스에 변경을 알리려면 StorSimple 관리자 서비스에 액세스하고 저장소 계정에 액세스한 다음 기본 또는 보조 키(변경된 키에 따라 다름)를 동기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-193">To inform the StorSimple Manager service of the change, you will need to access the StorSimple Manager service, access the storage account, and then synchronize the primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="4979d-194">그러면 서비스는 최신 키를 가져오고 해당 키를 암호화하여 장치에 암호화된 키를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-194">The service then gets the latest key, encrypts the keys, and sends the encrypted key to the device.</span></span>

#### <a name="to-synchronize-keys-for-storage-accounts-in-the-same-subscription-as-the-service-azure-only"></a><span data-ttu-id="4979d-195">서비스와 동일한 구독에서 저장소 계정에 대한 키를 동기화하려면(Azure에만 해당)</span><span class="sxs-lookup"><span data-stu-id="4979d-195">To synchronize keys for storage accounts in the same subscription as the service (Azure only)</span></span>
1. <span data-ttu-id="4979d-196">**서비스** 페이지에서 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-196">On the **Services** page, click the **Configure** tab.</span></span>
2. <span data-ttu-id="4979d-197">**저장소 계정 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-197">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="4979d-198">대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-198">In the dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="4979d-199">동기화하려는 키가 있는 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-199">Select the storage account with the key that you want to synchronize.</span></span> <span data-ttu-id="4979d-200">표시되면 저장소 계정 키가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-200">The storage account keys are encrypted when they are displayed.</span></span>
   2. <span data-ttu-id="4979d-201">StorSimple 관리자 서비스에서 이전에 Microsoft Azure 저장소 서비스에서 변경된 키를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-201">In the StorSimple Manager service, you need to update the key that was previously changed in the Microsoft Azure Storage service.</span></span> <span data-ttu-id="4979d-202">기본 액세스 키가 변경(다시 생성)된 경우 **기본 키 동기화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-202">If the primary access key was changed (regenerated), click **synchronize primary key**.</span></span> <span data-ttu-id="4979d-203">보조키가 변경된 경우 **보조 키 동기화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-203">If the secondary key was changed, click **synchronize secondary key**.</span></span>
      
      ![키 동기화](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="to-synchronize-keys-for-storage-accounts-outside-of-the-service-subscription"></a><span data-ttu-id="4979d-205">서비스 구독 외의 저장소 계정에 대한 키를 동기화하려면</span><span class="sxs-lookup"><span data-stu-id="4979d-205">To synchronize keys for storage accounts outside of the service subscription</span></span>
1. <span data-ttu-id="4979d-206">**서비스** 페이지에서 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-206">On the **Services** page, click the **Configure** tab.</span></span>
2. <span data-ttu-id="4979d-207">**저장소 계정 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-207">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="4979d-208">대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-208">In the dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="4979d-209">업데이트하려는 액세스 키가 있는 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-209">Select the storage account with the access key that you want to update.</span></span>
   2. <span data-ttu-id="4979d-210">StorSimple 관리자 서비스에서 저장소 액세스 키를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-210">You will need to update the storage access key in the StorSimple Manager service.</span></span> <span data-ttu-id="4979d-211">이 경우 저장소 액세스 키를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-211">In this case, you can see the storage access key.</span></span> <span data-ttu-id="4979d-212">**저장소 계정 액세스 키**상자에 새 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-212">Enter the new key in the **Storage Account Access Key**y box.</span></span> 
   3. <span data-ttu-id="4979d-213">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-213">Save your changes.</span></span> <span data-ttu-id="4979d-214">이제 저장소 계정 액세스 키가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-214">Your storage account access key should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4979d-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4979d-215">Next steps</span></span>
* <span data-ttu-id="4979d-216">[StorSimple 보안](storsimple-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-216">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="4979d-217">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4979d-217">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

