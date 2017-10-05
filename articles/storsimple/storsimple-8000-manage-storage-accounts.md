---
title: "Microsoft Azure StorSimple 8000 시리즈 장치에 대한 StorSimple 저장소 계정 자격 증명 관리 | Microsoft Docs"
description: "StorSimple 장치 관리자 구성 페이지를 사용하여 저장소 계정에 대한 보안 키를 추가, 편집, 삭제 또는 회전하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 36058ad69ea670998b50cf9038741c294a5b79ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-your-storage-account-credentials"></a><span data-ttu-id="75b50-103">StorSimple 장치 관리자 서비스를 사용하여 저장소 계정 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="75b50-103">Use the StorSimple Device Manager service to manage your storage account credentials</span></span>

## <a name="overview"></a><span data-ttu-id="75b50-104">개요</span><span class="sxs-lookup"><span data-stu-id="75b50-104">Overview</span></span>

<span data-ttu-id="75b50-105">StorSimple 장치 관리자 서비스 블레이드의 **구성** 섹션에서는 StorSimple 장치 관리자 서비스에서 만들 수 있는 모든 글로벌 서비스 매개 변수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-105">The **Configuration** section in the StorSimple Device Manager service blade presents all the global service parameters that can be created in the StorSimple Device Manager service.</span></span> <span data-ttu-id="75b50-106">이러한 매개 변수는 서비스에 연결된 모든 장치에 적용할 수 있으며 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-106">These parameters can be applied to all the devices connected to the service, and include:</span></span>

* <span data-ttu-id="75b50-107">저장소 계정 자격 증명</span><span class="sxs-lookup"><span data-stu-id="75b50-107">Storage account credentials</span></span>
* <span data-ttu-id="75b50-108">대역폭 템플릿</span><span class="sxs-lookup"><span data-stu-id="75b50-108">Bandwidth templates</span></span> 
* <span data-ttu-id="75b50-109">액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="75b50-109">Access control records</span></span> 

<span data-ttu-id="75b50-110">이 자습서에서는 저장소 계정 자격 증명을 추가, 편집 또는 삭제하거나, 저장소 계정에 대한 보안 키를 회전하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-110">This tutorial explains how to add, edit, or delete storage account credentials, or rotate the security keys for a storage account.</span></span>

 ![저장소 계정 자격 증명 목록](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

<span data-ttu-id="75b50-112">저장소 계정에는 StorSimple 장치가 클라우드 서비스 공급자를 통해 저장소 계정에 액세스하는 데 사용하는 자격 증명이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-112">Storage accounts contain the credentials that the StorSimple device uses to access your storage account with your cloud service provider.</span></span> <span data-ttu-id="75b50-113">Microsoft Azure 저장소 계정의 경우 계정 이름 및 기본 액세스 키와 같은 자격 증명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-113">For Microsoft Azure storage accounts, these are credentials such as the account name and the primary access key.</span></span> 

<span data-ttu-id="75b50-114">**저장소 계정 자격 증명** 블레이드에는 청구 구독에 대해 만들어진 모든 저장소 계정이 다음 정보를 포함하여 테이블 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-114">On the **Storage account credentials** blade, all storage accounts that are created for the billing subscription are displayed in a tabular format containing the following information:</span></span>

* <span data-ttu-id="75b50-115">**이름** – 만들어졌을 때 계정에 할당된 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-115">**Name** – The unique name assigned to the account when it was created.</span></span>
* <span data-ttu-id="75b50-116">**SSL 사용** – SSL 사용 및 장치와 클라우드 사이의 통신이 보안 채널을 통해 이루어지는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-116">**SSL enabled** – Whether the SSL is enabled and device-to-cloud communication is over the secure channel.</span></span>
* <span data-ttu-id="75b50-117">**사용 볼륨** – 저장소 계정을 사용하는 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-117">**Used by** – The number of volumes using the storage account.</span></span>

<span data-ttu-id="75b50-118">저장소 계정과 관련하여 수행할 수 있는 가장 일반적인 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-118">The most common tasks related to storage accounts that can be performed are:</span></span>

* <span data-ttu-id="75b50-119">저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="75b50-119">Add a storage account</span></span> 
* <span data-ttu-id="75b50-120">저장소 계정 편집</span><span class="sxs-lookup"><span data-stu-id="75b50-120">Edit a storage account</span></span> 
* <span data-ttu-id="75b50-121">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="75b50-121">Delete a storage account</span></span> 
* <span data-ttu-id="75b50-122">저장소 계정의 키 회전</span><span class="sxs-lookup"><span data-stu-id="75b50-122">Key rotation of storage accounts</span></span> 

## <a name="types-of-storage-accounts"></a><span data-ttu-id="75b50-123">저장소 계정 유형</span><span class="sxs-lookup"><span data-stu-id="75b50-123">Types of storage accounts</span></span>

<span data-ttu-id="75b50-124">StorSimple 장치에서 사용할 수 있는 저장소 계정에는 다음과 같은 세 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-124">There are three types of storage accounts that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="75b50-125">**자동 생성된 저장소 계정** – 이름 제안 시, 서비스를 처음 만들 때 이 저장소 계정 유형이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-125">**Auto-generated storage accounts** – As the name suggests, this type of storage account is automatically generated when the service is first created.</span></span> <span data-ttu-id="75b50-126">이 저장소 계정을 만드는 방법에 대해 자세히 알아보려면 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)에서 [1단계: 새 서비스 만들기](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75b50-126">To learn more about how this storage account is created, see [Step 1: Create a new service](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span> 
* <span data-ttu-id="75b50-127">**서비스 구독의 저장소 계정** – 이러한 계정은 서비스와 동일한 구독과 연결된 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-127">**Storage accounts in the service subscription** – These are the Azure storage accounts that are associated with the same subscription as that of the service.</span></span> <span data-ttu-id="75b50-128">이러한 저장소 계정을 만드는 방법에 대해 더 알아보려면 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75b50-128">To learn more about how these storage accounts are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span> 
* <span data-ttu-id="75b50-129">**서비스 구독 외의 저장소 계정** - 이러한 계정은 서비스와 연결되지 않았고 서비스가 만들어지기 전에 존재했던 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-129">**Storage accounts outside of the service subscription** – These are the Azure storage accounts that are not associated with your service and likely existed before the service was created.</span></span>

## <a name="add-a-storage-account"></a><span data-ttu-id="75b50-130">저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="75b50-130">Add a storage account</span></span>

<span data-ttu-id="75b50-131">저장소 계정(지정된 클라우드 서비스 공급자를 통해)에 연결된 액세스 자격 증명 및 친숙한 고유 이름을 제공하여 저장소 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-131">You can add a storage account by providing a unique friendly name and access credentials that are linked to the storage account (with the specified cloud service provider).</span></span> <span data-ttu-id="75b50-132">장치와 클라우드 사이에서 네트워크 통신을 위한 보안 채널을 만들기 위해 SSL(Secure Sockets Layer) 모드를 사용하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-132">You also have the option of enabling the secure sockets layer (SSL) mode to create a secure channel for network communication between your device and the cloud.</span></span>

<span data-ttu-id="75b50-133">특정 클라우드 서비스 공급자에 대해 여러 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="75b50-134">하지만 저장소 계정을 만든 후에는 클라우드 서비스 공급자를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-134">Be aware, however, that after a storage account is created, you cannot change the cloud service provider.</span></span>

<span data-ttu-id="75b50-135">저장소 계정을 저장하는 동안 해당 서비스는 클라우드 서비스 공급자와 통신을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-135">While the storage account is being saved, the service attempts to communicate with your cloud service provider.</span></span> <span data-ttu-id="75b50-136">사용자가 지정한 자격 증명 및 액세스 자료가 이 때 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-136">The credentials and the access material that you supplied will be authenticated at this time.</span></span> <span data-ttu-id="75b50-137">인증에 성공하는 경우에만 저장소 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-137">A storage account is created only if the authentication succeeds.</span></span> <span data-ttu-id="75b50-138">인증에 실패하는 경우 그에 따른 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-138">If the authentication fails, then an appropriate error message will be displayed.</span></span>

<span data-ttu-id="75b50-139">Azure Storage 계정 자격 증명을 추가하려면 다음 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-139">Use the following procedures to add Azure storage account credentials:</span></span>

* <span data-ttu-id="75b50-140">장치 관리자 서비스와 동일한 Azure 구독에 있는 저장소 계정 자격 증명을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="75b50-140">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>
* <span data-ttu-id="75b50-141">장치 관리자 서비스 구독 외부에 있는 Azure Storage 계정 자격 증명을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="75b50-141">To add an Azure storage account credential that is outside of the Device Manager service subscription</span></span>

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="to-add-an-azure-storage-account-credential-outside-of-the-storsimple-device-manager-service-subscription"></a><span data-ttu-id="75b50-142">StorSimple 장치 관리자 서비스 구독 외부에 있는 Azure Storage 계정 자격 증명을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="75b50-142">To add an Azure storage account credential outside of the StorSimple Device Manager service subscription</span></span>

1. <span data-ttu-id="75b50-143">StorSimple 장치 관리자 서비스를 찾아 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-143">Navigate to your StorSimple Device Manager service, select and double-click it.</span></span> <span data-ttu-id="75b50-144">그러면 **개요** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-144">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="75b50-145">**구성** 섹션 내의 **저장소 계정 자격 증명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-145">Select **Storage account credentials** within the **Configuration** section.</span></span> <span data-ttu-id="75b50-146">그러면 StorSimple 장치 관리자 서비스와 연결된 모든 기존 저장소 계정 자격 증명을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-146">This lists any existing storage account credentials associated with the StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="75b50-147">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-147">Click **Add**.</span></span>
4. <span data-ttu-id="75b50-148">**저장소 계정 자격 증명 추가** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-148">In the **Add a storage account credential** blade, do the following:</span></span>
   
    1. <span data-ttu-id="75b50-149">**구독**에 **기타**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-149">For **Subscription**, select **Other**.</span></span>
   
    2. <span data-ttu-id="75b50-150">Azure Storage 계정 자격 증명의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-150">Provide the name of your Azure storage account credential.</span></span>
   
    3. <span data-ttu-id="75b50-151">**저장소 계정 선택키** 텍스트 상자에서 Azure Storage 계정 자격 증명의 기본 선택키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-151">In the **Storage account access key** text box, supply the primary Access Key for your Azure storage account credential.</span></span> <span data-ttu-id="75b50-152">이 키를 가져오려면 Azure Storage 서비스로 이동하고 저장소 계정 자격 증명을 선택한 다음 **계정 키 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-152">To get this key, go to the Azure Storage service, select your storage account credential, and click **Manage account keys**.</span></span> <span data-ttu-id="75b50-153">이제 기본 선택키를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-153">You can now copy the primary access key.</span></span>
   
    4. <span data-ttu-id="75b50-154">SSL을 사용하도록 설정하려면 **사용** 단추를 클릭하여 StorSimple 장치 관리자 서비스와 클라우드 간의 네트워크 통신을 위한 보안 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-154">To enable SSL, click the **Enable** button to create a secure channel for network communication between your StorSimple Device Manager service and the cloud.</span></span> <span data-ttu-id="75b50-155">사설 클라우드 내에서 작동하는 경우에만 **사용 안 함** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-155">Click the **Disable** button only if you are operating within a private cloud.</span></span>
   
    5. <span data-ttu-id="75b50-156">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-156">Click **Add**.</span></span> <span data-ttu-id="75b50-157">저장소 계정 자격 증명이 성공적으로 만들어진 후 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-157">You are notified after the storage account credential is successfully created.</span></span>

5. <span data-ttu-id="75b50-158">새로 만든 저장소 계정 자격 증명은 **저장소 계정 자격 증명**의 StorSimple 구성 장치 관리자 서비스 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-158">The newly created storage account credential is displayed on the StorSimple Configure Device Manager service blade under **Storage account credentials**.</span></span>
   


## <a name="edit-a-storage-account"></a><span data-ttu-id="75b50-159">저장소 계정 편집</span><span class="sxs-lookup"><span data-stu-id="75b50-159">Edit a storage account</span></span>

<span data-ttu-id="75b50-160">볼륨 컨테이너에서 사용되는 저장소 계정을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-160">You can edit a storage account that is used by a volume container.</span></span> <span data-ttu-id="75b50-161">현재 사용 중인 저장소 계정을 편집할 경우 수정할 수 있는 유일한 필드는 저장소 계정에 대한 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-161">If you edit a storage account that is currently in use, the only field available to modify is the access key for the storage account.</span></span> <span data-ttu-id="75b50-162">새 저장소 액세스 키를 제공할 수 있으며 업데이트된 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-162">You can supply the new storage access key and save the updated settings.</span></span>

#### <a name="to-edit-a-storage-account"></a><span data-ttu-id="75b50-163">저장소 계정을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="75b50-163">To edit a storage account</span></span>

1. <span data-ttu-id="75b50-164">StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-164">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="75b50-165">**구성** 섹션에서 **저장소 계정 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-165">In the **Configuration** section, click **Storage account credentials**.</span></span>

    ![저장소 계정 자격 증명](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. <span data-ttu-id="75b50-167">**저장소 계정 자격 증명** 블레이드의 저장소 계정 자격 증명 목록에서 편집하려는 항목을 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-167">In the **Storage account credentials** blade, from the list of storage account credentials, select and click the one you wish to edit.</span></span> 

3. <span data-ttu-id="75b50-168">**SSL 사용** 섹션을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-168">You can modify the **Enable SSL** selection.</span></span> <span data-ttu-id="75b50-169">**자세히...**를 클릭하여 저장소 계정 액세스 키를 회전하도록 **Sync access key to rotate**(회전할 액세스 키 동기화)를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-169">You can also click **More...** and then select **Sync access key to rotate** your storage account access keys.</span></span> <span data-ttu-id="75b50-170">키 회전을 수행하는 방법에 대한 자세한 내용을 보려면 [저장소 계정의 키 회전](#key-rotation-of-storage-accounts)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-170">Go to [Key rotation of storage accounts](#key-rotation-of-storage-accounts) for more information on how to perform key rotation.</span></span> <span data-ttu-id="75b50-171">설정을 수정한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-171">After you have modified the settings, click **Save**.</span></span> 

    ![편집된 저장소 계정 자격 증명 저장](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. <span data-ttu-id="75b50-173">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-173">When prompted for confirmation, click **Yes**.</span></span> 

    ![수정 확인](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

<span data-ttu-id="75b50-175">저장소 계정에 대한 설정이 업데이트되고 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-175">The settings will be updated and saved for your storage account.</span></span> 

## <a name="delete-a-storage-account"></a><span data-ttu-id="75b50-176">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="75b50-176">Delete a storage account</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75b50-177">볼륨 컨테이너에서 사용하지 않는 경우에만 저장소 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-177">You can delete a storage account only if it is not used by a volume container.</span></span> <span data-ttu-id="75b50-178">저장소 계정을 볼륨 컨테이너에서 사용 중인 경우 먼저 볼륨 컨테이너를 삭제하고 연결된 저장소 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-178">If a storage account is being used by a volume container, first delete the volume container and then delete the associated storage account.</span></span>

#### <a name="to-delete-a-storage-account"></a><span data-ttu-id="75b50-179">저장소 계정을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="75b50-179">To delete a storage account</span></span>

1. <span data-ttu-id="75b50-180">StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-180">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="75b50-181">**구성** 섹션에서 **저장소 계정 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-181">In the **Configuration** section, click **Storage account credentials**.</span></span>

2. <span data-ttu-id="75b50-182">저장소 계정의 테이블 형식 목록에서 삭제하려는 계정을 마우스로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-182">In the tabular list of storage accounts, hover over the account that you wish to delete.</span></span> <span data-ttu-id="75b50-183">마우스 오른쪽 단추를 클릭하여 상황에 맞는 메뉴를 호출하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-183">Right-click to invoke the context menu and click **Delete**.</span></span>

    ![저장소 계정 자격 증명 삭제](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. <span data-ttu-id="75b50-185">확인 메시지가 나타나면 **예** 를 클릭하여 삭제를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-185">When prompted for confirmation, click **Yes** to continue with the deletion.</span></span> <span data-ttu-id="75b50-186">테이블 형식 목록이 변경 내용을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-186">The tabular listing will be updated to reflect the changes.</span></span>

    ![삭제 확인](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a><span data-ttu-id="75b50-188">저장소 계정의 키 회전</span><span class="sxs-lookup"><span data-stu-id="75b50-188">Key rotation of storage accounts</span></span>

<span data-ttu-id="75b50-189">보안상의 이유로 키 회전이 데이터 센터에서 요구되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-189">For security reasons, key rotation is often a requirement in data centers.</span></span> <span data-ttu-id="75b50-190">각 Microsoft Azure 구독에 하나 이상의 연결된 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-190">Each Microsoft Azure subscription can have one or more associated storage accounts.</span></span> <span data-ttu-id="75b50-191">이러한 계정에 대한 액세스는 해당 저장소 계정에 대한 구독 및 액세스 키를 통해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-191">The access to these accounts is controlled by the subscription and access keys for each storage account.</span></span> 

<span data-ttu-id="75b50-192">저장소 계정을 만들면 Microsoft Azure에서 두 개의 512비트 저장소 액세스 키를 생성합니다. 이 키는 저장소 계정에 액세스하는 경우 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-192">When you create a storage account, Microsoft Azure generates two 512-bit storage access keys that are used for authentication when the storage account is accessed.</span></span> <span data-ttu-id="75b50-193">두 개의 저장소 액세스 키가 있으면 저장소 서비스나 해당 서비스에 대한 액세스에 중단 없이 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-193">Having two storage access keys allows you to regenerate the keys with no interruption to your storage service or access to that service.</span></span> <span data-ttu-id="75b50-194">현재 사용 중인 키는 *기본* 키이며 백업 키는 *보조* 키라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-194">The key that is currently in use is the *primary* key and the backup key is referred to as the *secondary* key.</span></span> <span data-ttu-id="75b50-195">Microsoft Azure StorSimple 장치가 클라우드 저장소 서비스 공급자에 액세스할 때 이러한 두 키 중 하나를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-195">One of these two keys must be supplied when your Microsoft Azure StorSimple device accesses your cloud storage service provider.</span></span>

## <a name="what-is-key-rotation"></a><span data-ttu-id="75b50-196">키 회전 정의</span><span class="sxs-lookup"><span data-stu-id="75b50-196">What is key rotation?</span></span>

<span data-ttu-id="75b50-197">일반적으로 응용 프로그램은 데이터 액세스에 키 중 하나만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-197">Typically, applications use only one of the keys to access your data.</span></span> <span data-ttu-id="75b50-198">특정 시간이 지나면 응용 프로그램이 두 번째 키를 사용하도록 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-198">After a certain period of time, you can have your applications switch over to using the second key.</span></span> <span data-ttu-id="75b50-199">두 번째 키로 응용 프로그램을 전환한 후 첫 번째 키를 사용 중지한 다음 새 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-199">After you have switched your applications to the secondary key, you can retire the first key and then generate a new key.</span></span> <span data-ttu-id="75b50-200">이러한 방식으로 두 키를 사용하면 가동 중지 시간 없이 응용 프로그램이 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-200">Using the two keys this way allows your applications access to the data without incurring any downtime.</span></span>

<span data-ttu-id="75b50-201">저장소 계정 키는 항상 암호화된 형태로 서비스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-201">The storage account keys are always stored in the service in an encrypted form.</span></span> <span data-ttu-id="75b50-202">하지만 StorSimple 장치 관리자 서비스를 통해 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-202">However, these can be reset via the StorSimple Device Manager service.</span></span> <span data-ttu-id="75b50-203">서비스는 StorSimple 장치 관리자 서비스를 처음 만들 때 생성한 기본 저장소 계정뿐 아니라 Storage 서비스에서 만든 계정을 비롯하여 동일한 구독의 모든 저장소 계정에 대해 기본 키 및 보조 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-203">The service can get the primary key and secondary key for all the storage accounts in the same subscription, including accounts created in the Storage service as well as the default storage accounts generated when the StorSimple Device Manager service service was first created.</span></span> <span data-ttu-id="75b50-204">StorSimple 장치 관리자 서비스는 Azure 클래식 포털에서 항상 이러한 키를 가져와 암호화된 방법으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-204">The StorSimple Device Manager service will always get these keys from the Azure classic portal and then store them in an encrypted manner.</span></span>

## <a name="rotation-workflow"></a><span data-ttu-id="75b50-205">회전 워크플로</span><span class="sxs-lookup"><span data-stu-id="75b50-205">Rotation workflow</span></span>

<span data-ttu-id="75b50-206">Microsoft Azure 관리자가 저장소 계정에 직접 액세스하여(Microsoft Azure 저장소 서비스를 통해) 기본 키 또는 보조 키를 다시 생성하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-206">A Microsoft Azure administrator can regenerate or change the primary or secondary key by directly accessing the storage account (via the Microsoft Azure Storage service).</span></span> <span data-ttu-id="75b50-207">StorSimple 장치 관리자 서비스는 이 변경 사항을 자동으로 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-207">The StorSimple Device Manager service does not see this change automatically.</span></span>

<span data-ttu-id="75b50-208">StorSimple 장치 관리자 서비스에 변경을 알리려면 StorSimple 장치 관리자 서비스에 액세스하고 저장소 계정에 액세스한 다음 기본 또는 보조 키(변경된 키에 따라 다름)를 동기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-208">To inform the StorSimple Device Manager service of the change, you will need to access the StorSimple Device Manager service, access the storage account, and then synchronize the primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="75b50-209">그러면 서비스는 최신 키를 가져오고 해당 키를 암호화하여 장치에 암호화된 키를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-209">The service then gets the latest key, encrypts the keys, and sends the encrypted key to the device.</span></span>

#### <a name="to-synchronize-keys-for-storage-accounts-in-the-same-subscription-as-the-service"></a><span data-ttu-id="75b50-210">서비스와 동일한 구독에서 저장소 계정에 대한 키를 동기화하려면</span><span class="sxs-lookup"><span data-stu-id="75b50-210">To synchronize keys for storage accounts in the same subscription as the service</span></span> 
1. <span data-ttu-id="75b50-211">StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-211">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="75b50-212">**구성** 섹션에서 **저장소 계정 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-212">In the **Configuration** section, click **Storage account credentials**.</span></span>
2. <span data-ttu-id="75b50-213">저장소 계정의 테이블 형식 목록에서 수정하려는 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-213">From the tabular listing of storage accounts, click the one that you want to modify.</span></span> 

    ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. <span data-ttu-id="75b50-215">**...자세히**를 클릭하고 **Sync access key to rotate**(회전할 액세스 키 동기화)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-215">Click **...More** and then select **Sync access key to rotate**.</span></span>   

    ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. <span data-ttu-id="75b50-217">StorSimple 장치 관리자 서비스에서 이전에 Microsoft Azure Storage 서비스에서 변경된 키를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-217">In the StorSimple Device Manager service, you need to update the key that was previously changed in the Microsoft Azure Storage service.</span></span> <span data-ttu-id="75b50-218">기본 액세스 키가 변경(다시 생성)된 경우 **기본** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-218">If the primary access key was changed (regenerated), select **primary** key.</span></span> <span data-ttu-id="75b50-219">보조 키가 변경된 경우 **보조** 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-219">If the secondary key was changed, select **secondary** key.</span></span> <span data-ttu-id="75b50-220">**키 동기화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-220">Click **Sync key**.</span></span>
      
      ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

<span data-ttu-id="75b50-222">키가 성공적으로 동기화되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-222">You will be notified after the key is successfully sycnhronized.</span></span>

#### <a name="to-synchronize-keys-for-storage-accounts-outside-of-the-service-subscription"></a><span data-ttu-id="75b50-223">서비스 구독 외의 저장소 계정에 대한 키를 동기화하려면</span><span class="sxs-lookup"><span data-stu-id="75b50-223">To synchronize keys for storage accounts outside of the service subscription</span></span>
1. <span data-ttu-id="75b50-224">**서비스** 페이지에서 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-224">On the **Services** page, click the **Configure** tab.</span></span>
2. <span data-ttu-id="75b50-225">**저장소 계정 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-225">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="75b50-226">대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-226">In the dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="75b50-227">업데이트하려는 액세스 키가 있는 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-227">Select the storage account with the access key that you want to update.</span></span>
   2. <span data-ttu-id="75b50-228">StorSimple 장치 관리자 서비스에서 저장소 액세스 키를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-228">You will need to update the storage access key in the StorSimple Device Manager service.</span></span> <span data-ttu-id="75b50-229">이 경우 저장소 액세스 키를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-229">In this case, you can see the storage access key.</span></span> <span data-ttu-id="75b50-230">**저장소 계정 액세스 키** 상자에 새 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-230">Enter the new key in the **Storage Account Access Key** box.</span></span> 
   3. <span data-ttu-id="75b50-231">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-231">Save your changes.</span></span> <span data-ttu-id="75b50-232">이제 저장소 계정 액세스 키가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-232">Your storage account access key should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75b50-233">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75b50-233">Next steps</span></span>
* <span data-ttu-id="75b50-234">[StorSimple 보안](storsimple-8000-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-234">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="75b50-235">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리하는 방법](storsimple-8000-manager-service-administration.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75b50-235">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

