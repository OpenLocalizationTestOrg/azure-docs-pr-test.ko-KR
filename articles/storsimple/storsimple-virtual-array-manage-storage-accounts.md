---
title: "StorSimple Virtual Array의 저장소 계정 공유 자격 증명 관리 | Microsoft Docs"
description: "StorSimple 장치 관리자 구성 페이지를 사용하여 StorSimple Virtual Array과 연결된 저장소 계정 자격 증명의 보안 키를 추가, 편집, 삭제 또는 회전하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: a4ce2d329d0e1399cffaf886adf2b95e34b9cd7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-storsimple-device-manager-to-manage-storage-account-credentials-for-storsimple-virtual-array"></a><span data-ttu-id="9380d-103">StorSimple 장치 관리자를 사용하여 StorSimple 가상 배열의 저장소 계정 자격 증명 관리</span><span class="sxs-lookup"><span data-stu-id="9380d-103">Use StorSimple Device Manager to manage storage account credentials for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="9380d-104">개요</span><span class="sxs-lookup"><span data-stu-id="9380d-104">Overview</span></span>
<span data-ttu-id="9380d-105">StorSimple 가상 배열의 StorSimple 장치 관리자 서비스 블레이드 중 **구성** 섹션에서는 StorSimple Manager 서비스에서 만들 수 있는 글로벌 서비스 매개 변수를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-105">The **Configuration** section of the StorSimple Device Manager service blade of your StorSimple Virtual Array presents the global service parameters that can be created in the StorSimple Manager service.</span></span> <span data-ttu-id="9380d-106">이러한 매개 변수는 서비스에 연결된 모든 장치에 적용할 수 있으며 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-106">These parameters can be applied to all the devices connected to the service, and include:</span></span>

* <span data-ttu-id="9380d-107">저장소 계정 자격 증명</span><span class="sxs-lookup"><span data-stu-id="9380d-107">Storage account credentials</span></span>
* <span data-ttu-id="9380d-108">액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="9380d-108">Access control records</span></span>
  
  ![장치 관리자 서비스 대시보드](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

<span data-ttu-id="9380d-110">이 자습서에서는 StorSimple 가상 배열에 대한 저장소 계정 자격 증명을 추가, 편집 또는 삭제하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-110">This tutorial explains how you can add, edit, or delete storage account credentials for your StorSimple Virtual Array.</span></span> <span data-ttu-id="9380d-111">이 자습서의 정보는 StorSimple 가상 배열에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-111">The information in this tutorial only applies to the StorSimple Virtual Array.</span></span> <span data-ttu-id="9380d-112">8000 시리즈에서 저장소 계정을 관리하는 방법에 대한 자세한 내용은 [StorSimple Manager 서비스를 사용하여 저장소 계정 관리](storsimple-manage-storage-accounts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9380d-112">For information on how to manage storage accounts in 8000 series, see [Use the StorSimple Manager service to manage your storage account](storsimple-manage-storage-accounts.md).</span></span>

<span data-ttu-id="9380d-113">저장소 계정 자격 증명은 클라우드 서비스 공급자와 저장소 계정에 액세스하기 위해 장치가 사용하는 자격 증명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-113">Storage account credentials contain the credentials that the device uses to access your storage account with your cloud service provider.</span></span> <span data-ttu-id="9380d-114">Microsoft Azure 저장소 계정의 경우 계정 이름 및 기본 액세스 키와 같은 자격 증명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-114">For Microsoft Azure storage accounts, these are credentials such as the account name and the primary access key.</span></span>

<span data-ttu-id="9380d-115">**저장소 계정 자격 증명** 블레이드에서 청구 구독에 대해 만들어진 모든 저장소 계정 자격 증명이 다음 정보를 포함하여 테이블 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-115">On the **Storage account credentials** blade, all storage account credentials that are created for the billing subscription are displayed in a tabular format containing the following information:</span></span>

* <span data-ttu-id="9380d-116">**이름** – 만들어졌을 때 계정에 할당된 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-116">**Name** – The unique name assigned to the account when it was created.</span></span>
* <span data-ttu-id="9380d-117">**SSL 사용** – SSL 사용 및 장치와 클라우드 사이의 통신이 보안 채널을 통해 이루어지는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-117">**SSL enabled** – Whether the SSL is enabled and device-to-cloud communication is over the secure channel.</span></span>
  
  ![구성 섹션](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

<span data-ttu-id="9380d-119">**저장소 계정 자격 증명** 블레이드에서 수행할 수 있는 저장소 계정 자격 증명과 관련된 가장 일반적인 태스크는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-119">The most common tasks related to storage account credentials that can be performed on the **Storage account credentials** blade are:</span></span>

* <span data-ttu-id="9380d-120">저장소 계정 자격 증명 추가</span><span class="sxs-lookup"><span data-stu-id="9380d-120">Add a storage account credential</span></span>
* <span data-ttu-id="9380d-121">저장소 계정 자격 증명 편집</span><span class="sxs-lookup"><span data-stu-id="9380d-121">Edit a storage account credential</span></span>
* <span data-ttu-id="9380d-122">저장소 계정 자격 증명 삭제</span><span class="sxs-lookup"><span data-stu-id="9380d-122">Delete a storage account credential</span></span>

## <a name="types-of-storage-account-credentials"></a><span data-ttu-id="9380d-123">저장소 계정 자격 증명 유형</span><span class="sxs-lookup"><span data-stu-id="9380d-123">Types of storage account credentials</span></span>
<span data-ttu-id="9380d-124">StorSimple 장치에서 사용할 수 있는 저장소 계정 자격 증명에는 다음과 같은 세 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-124">There are three types of storage account credentials that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="9380d-125">**자동 생성된 저장소 계정 자격 증명** – 이름 제안 시, 서비스를 처음 만들 때 이 저장소 계정 자격 증명 유형이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-125">**Auto-generated storage account credentials** – As the name suggests, this type of storage account credential is automatically generated when the service is first created.</span></span> <span data-ttu-id="9380d-126">이 저장소 계정 자격 증명을 만드는 방법에 대해 더 알아보려면 [새 서비스 만들기](storsimple-virtual-array-manage-service.md#create-a-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9380d-126">To learn more about how this storage account credential is created, see [Create a new service](storsimple-virtual-array-manage-service.md#create-a-service).</span></span>
* <span data-ttu-id="9380d-127">**서비스 구독의 저장소 계정 자격 증명** – 이러한 계정은 서비스와 동일한 구독과 연결된 Azure Storage 계정 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-127">**storage account credentials in the service subscription** – These are the Azure storage account credentials that are associated with the same subscription as that of the service.</span></span> <span data-ttu-id="9380d-128">이러한 저장소 계정 자격 증명을 만드는 방법에 대해 더 알아보려면 [Azure Storage 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9380d-128">To learn more about how these storage account credentials are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="9380d-129">**서비스 구독 외부의 저장소 계정 자격 증명** - 이러한 계정 자격 증명은 서비스와 연결되지 않았고 서비스가 만들어지기 전에 존재했던 Azure Storage 계정 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-129">**storage account credentials outside of the service subscription** – These are the Azure storage account credentials that are not associated with your service and likely existed before the service was created.</span></span>

## <a name="add-a-storage-account-credential"></a><span data-ttu-id="9380d-130">저장소 계정 자격 증명 추가</span><span class="sxs-lookup"><span data-stu-id="9380d-130">Add a storage account credential</span></span>
<span data-ttu-id="9380d-131">저장소 계정에 연결된 액세스 자격 증명 및 고유 이름을 제공하여 저장소 계정 자격 증명을 StorSimple 장치 관리자 서비스 구성에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-131">You can add a storage account credential to your StorSimple Device Manager service configuration by providing a unique friendly name and access credentials that are linked to the storage account.</span></span> <span data-ttu-id="9380d-132">장치와 클라우드 사이에서 네트워크 통신을 위한 보안 채널을 만들기 위해 SSL(Secure Sockets Layer) 모드를 사용하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-132">You also have the option of enabling the secure sockets layer (SSL) mode to create a secure channel for network communication between your device and the cloud.</span></span>

<span data-ttu-id="9380d-133">특정 클라우드 서비스 공급자에 대해 여러 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="9380d-134">저장소 계정 자격 증명을 저장하는 동안 해당 서비스는 클라우드 서비스 공급자와 통신을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-134">While the storage account credential is being saved, the service attempts to communicate with your cloud service provider.</span></span> <span data-ttu-id="9380d-135">사용자가 지정한 자격 증명 및 액세스 자료가 이 때 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-135">The credentials and the access material that you supplied are authenticated at this time.</span></span> <span data-ttu-id="9380d-136">인증에 성공하는 경우에만 저장소 계정 자격 증명이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-136">A storage account credential is created only if the authentication succeeds.</span></span> <span data-ttu-id="9380d-137">인증에 실패하는 경우 그에 따른 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-137">If the authentication fails, then an appropriate error message is displayed.</span></span>

<span data-ttu-id="9380d-138">Azure Storage 계정 자격 증명을 추가하려면 다음 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-138">Use the following procedures to add Azure storage account credentials:</span></span>

* <span data-ttu-id="9380d-139">장치 관리자 서비스와 동일한 Azure 구독에 있는 저장소 계정 자격 증명을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="9380d-139">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>
* <span data-ttu-id="9380d-140">장치 관리자 서비스 구독 외부에 있는 Azure Storage 계정 자격 증명을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="9380d-140">To add an Azure storage account credential that is outside of the Device Manager service subscription</span></span>

#### <a name="to-add-a-storage-account-credential-that-has-the-same-azure-subscription-as-the-device-manager-service"></a><span data-ttu-id="9380d-141">장치 관리자 서비스와 동일한 Azure 구독에 있는 저장소 계정 자격 증명을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="9380d-141">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>

1. <span data-ttu-id="9380d-142">장치 관리자 서비스를 찾아 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-142">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="9380d-143">그러면 **개요** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-143">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="9380d-144">**구성** 섹션 내의 **저장소 계정 자격 증명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-144">Select **Storage account credentials** within the **Configuration** section.</span></span>
3. <span data-ttu-id="9380d-145">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-145">Click **Add**.</span></span>
4. <span data-ttu-id="9380d-146">**저장소 계정 추가** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-146">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="9380d-147">**구독**에 **현재**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-147">For **Subscription**, select **Current**.</span></span>
    2. <span data-ttu-id="9380d-148">Azure 저장소 계정의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-148">Provide the name of your Azure storage account.</span></span>
    3. <span data-ttu-id="9380d-149">**사용**을 선택하여 StorSimple 장치와 클라우드 간의 네트워크 통신을 위한 보안 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-149">Select **Enable** to create a secure channel for network communication between your StorSimple device and the cloud.</span></span> <span data-ttu-id="9380d-150">사설 클라우드 내에서 작동하는 경우에만 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-150">Select **Disable** only if you are operating within a private cloud.</span></span>
    4. <span data-ttu-id="9380d-151">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-151">Click **Add**.</span></span> <span data-ttu-id="9380d-152">저장소 계정이 성공적으로 만들어진 후 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-152">You are notified after the storage account is successfully created.</span></span><br></br>
   
        ![기존 저장소 계정 자격 증명 추가](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="to-add-an-azure-storage-account-credential-that-is-outside-of-the-device-manager-service-subscription"></a><span data-ttu-id="9380d-154">장치 관리자 서비스 구독 외부에 있는 Azure Storage 계정 자격 증명을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="9380d-154">To add an Azure storage account credential that is outside of the Device Manager service subscription</span></span>

1. <span data-ttu-id="9380d-155">장치 관리자 서비스를 찾아 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-155">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="9380d-156">그러면 **개요** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-156">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="9380d-157">**구성** 섹션 내의 **저장소 계정 자격 증명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-157">Select **Storage account credentials** within the **Configuration** section.</span></span> <span data-ttu-id="9380d-158">그러면 StorSimple 장치 관리자 서비스와 연결된 모든 기존 저장소 계정 자격 증명을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-158">This lists any existing storage account credentials associated with the StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="9380d-159">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-159">Click **Add**.</span></span>
4. <span data-ttu-id="9380d-160">**저장소 계정 추가** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-160">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="9380d-161">**구독**에 **기타**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-161">For **Subscription**, select **Other**.</span></span>
   
    2. <span data-ttu-id="9380d-162">Azure Storage 계정 자격 증명의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-162">Provide the name of your Azure storage account credential.</span></span>
   
    3. <span data-ttu-id="9380d-163">**저장소 계정 선택키** 텍스트 상자에서 Azure Storage 계정 자격 증명의 기본 선택키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-163">In the **Storage account access key** text box, supply the primary Access Key for your Azure storage account credential.</span></span> <span data-ttu-id="9380d-164">이 키를 가져오려면 Azure Storage 서비스로 이동하고 저장소 계정 자격 증명을 선택한 다음 **계정 키 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-164">To get this key, go to the Azure Storage service, select your storage account credential, and click **Manage account keys**.</span></span> <span data-ttu-id="9380d-165">이제 기본 선택키를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-165">You can now copy the primary access key.</span></span>
   
    4. <span data-ttu-id="9380d-166">SSL을 사용하도록 설정하려면 **사용** 단추를 클릭하여 StorSimple 장치 관리자 서비스와 클라우드 간의 네트워크 통신을 위한 보안 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-166">To enable SSL, click the **Enable** button to create a secure channel for network communication between your StorSimple Device Manager service and the cloud.</span></span> <span data-ttu-id="9380d-167">사설 클라우드 내에서 작동하는 경우에만 **사용 안 함** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-167">Click the **Disable** button only if you are operating within a private cloud.</span></span>
   
    5. <span data-ttu-id="9380d-168">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-168">Click **Add**.</span></span> <span data-ttu-id="9380d-169">저장소 계정 자격 증명이 성공적으로 만들어진 후 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-169">You are notified after the storage account credential is successfully created.</span></span>

5. <span data-ttu-id="9380d-170">새로 만든 저장소 계정 자격 증명은 **저장소 계정 자격 증명**의 StorSimple 구성 장치 관리자 서비스 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-170">The newly created storage account credential is displayed on the StorSimple Configure Device Manager service blade under **Storage account credentials**.</span></span>
   
    ![장치 관리자 서비스 구독 외부의 저장소 계정 자격 증명 추가](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a><span data-ttu-id="9380d-172">저장소 계정 자격 증명 편집</span><span class="sxs-lookup"><span data-stu-id="9380d-172">Edit a storage account credential</span></span>
<span data-ttu-id="9380d-173">장치에서 사용하는 저장소 계정 자격 증명을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-173">You can edit a storage account credential used by your device.</span></span> <span data-ttu-id="9380d-174">현재 사용 중인 저장소 계정 자격 증명을 편집할 경우 수정할 수 있는 필드는 저장소 계정 자격 증명에 대한 선택키 및 SSL 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-174">If you edit a storage account credential that is currently in use, the fields available to modify are the access key and the SSL mode for the storage account credential.</span></span> <span data-ttu-id="9380d-175">새 저장소 액세스 키를 제공하거나 **SSL 모드 사용** 선택을 수정하고 업데이트된 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-175">You can supply the new storage access key or modify the **Enable SSL mode** selection and save the updated settings.</span></span>

#### <a name="to-edit-a-storage-account-credential"></a><span data-ttu-id="9380d-176">저장소 계정 자격 증명을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="9380d-176">To edit a storage account credential</span></span>
1. <span data-ttu-id="9380d-177">장치 관리자 서비스를 찾아 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-177">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="9380d-178">그러면 **개요** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-178">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="9380d-179">**구성** 섹션 내의 **저장소 계정 자격 증명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-179">Select **Storage account credentials** within the **Configuration** section.</span></span> <span data-ttu-id="9380d-180">그러면 StorSimple 장치 관리자 서비스와 연결된 모든 기존 저장소 계정 자격 증명을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-180">This lists any existing storage account credentials associated with the StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="9380d-181">저장소 계정 자격 증명의 테이블 형식 목록에서 수정하려는 계정을 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-181">In the tabular list of storage account credentials, select and double-click the account that you want to modify.</span></span>
4. <span data-ttu-id="9380d-182">저장소 계정 자격 증명 **속성** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-182">In the storage account credential **Properties** blade, do the following:</span></span>
   
   1. <span data-ttu-id="9380d-183">필요에 따라 **SSL 사용** 모드 선택을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-183">If necessary, you can modify the **Enable SSL** mode selection.</span></span>
   2. <span data-ttu-id="9380d-184">저장소 계정 자격 증명 선택키를 다시 생성하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-184">You can choose to regenerate your storage account credential access keys.</span></span> <span data-ttu-id="9380d-185">자세한 내용은 [저장소 계정 키 다시 생성](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9380d-185">For more information, see [Regenerate the storage account keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span> <span data-ttu-id="9380d-186">새 저장소 계정 자격 증명 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-186">Supply the new storage account credential key.</span></span> <span data-ttu-id="9380d-187">Azure 저장소 계정의 경우 이 키가 기본 선택키입니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-187">For an Azure storage account, this is the primary access key.</span></span>
   3. <span data-ttu-id="9380d-188">**속성** 블레이드 맨 위에 있는 **저장**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-188">Click **Save** at the top of the **Properties** blade to save the settings.</span></span> <span data-ttu-id="9380d-189">설정은 **저장소 계정 자격 증명** 블레이드에서 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-189">The settings are updated on the **Storage account credentials** blade.</span></span>
      
      ![저장소 계정 자격 증명 편집](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a><span data-ttu-id="9380d-191">저장소 계정 자격 증명 삭제</span><span class="sxs-lookup"><span data-stu-id="9380d-191">Delete a storage account credential</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9380d-192">사용하지 않는 경우에만 저장소 계정 자격 증명을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-192">You can delete a storage account credential only if it is not in use.</span></span> <span data-ttu-id="9380d-193">저장소 계정 자격 증명을 사용하는 중이면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-193">If a storage account credential is in use, you are notified.</span></span>
> 
> 

#### <a name="to-delete-a-storage-account-credential"></a><span data-ttu-id="9380d-194">저장소 계정 자격 증명을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="9380d-194">To delete a storage account credential</span></span>
1. <span data-ttu-id="9380d-195">장치 관리자 서비스를 찾아 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-195">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="9380d-196">그러면 **개요** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-196">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="9380d-197">**구성** 섹션 내의 **저장소 계정 자격 증명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-197">Select **Storage account credentials** within the **Configuration** section.</span></span> <span data-ttu-id="9380d-198">그러면 StorSimple 장치 관리자 서비스와 연결된 모든 기존 저장소 계정 자격 증명을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-198">This lists any existing storage account credentials associated with the StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="9380d-199">저장소 계정 자격 증명의 테이블 형식 목록에서 삭제하려는 계정을 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-199">In the tabular list of storage account credentials, select and double-click the account that you want to delete.</span></span>
4. <span data-ttu-id="9380d-200">저장소 계정 자격 증명 **속성** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-200">In the storage account credential **Properties** blade, do the following:</span></span>
   
   1. <span data-ttu-id="9380d-201">**삭제**를 클릭하여 자격 증명을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-201">Click **Delete** to delete the credentials.</span></span>
   2. <span data-ttu-id="9380d-202">확인 메시지가 나타나면 **예** 를 클릭하여 삭제를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-202">When prompted for confirmation, click **Yes** to continue with the deletion.</span></span> <span data-ttu-id="9380d-203">테이블 형식 목록이 변경을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-203">The tabular listing is updated to reflect the changes.</span></span>
      
      ![저장소 계정 자격 증명 삭제](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a><span data-ttu-id="9380d-205">저장소 계정 자격 증명 키 동기화</span><span class="sxs-lookup"><span data-stu-id="9380d-205">Synchronizing storage account credential keys</span></span>
<span data-ttu-id="9380d-206">보안상의 이유로 키 회전이 데이터 센터에서 요구되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-206">For security reasons, key rotation is often a requirement in data centers.</span></span> <span data-ttu-id="9380d-207">Microsoft Azure 관리자가 Microsoft Azure Storage 서비스를 통해 저장소 계정 자격 증명에 직접 액세스하여 기본 키 또는 보조 키를 다시 생성하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-207">A Microsoft Azure administrator can regenerate or change the primary or secondary key by directly accessing the storage account credential (via the Microsoft Azure Storage service).</span></span> <span data-ttu-id="9380d-208">StorSimple 장치 관리자 서비스는 이 변경 사항을 자동으로 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-208">The StorSimple Device Manager service does not see this change automatically.</span></span>

<span data-ttu-id="9380d-209">StorSimple 장치 관리자 서비스에 변경을 알리려면 StorSimple 장치 관리자 서비스에 액세스하고 저장소 계정 자격 증명에 액세스한 다음 기본 또는 보조 키(변경된 키에 따라 다름)를 동기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-209">To inform the StorSimple Device Manager service of the change, you need to access the StorSimple Device Manager service, access the storage account credential, and then synchronize the primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="9380d-210">그러면 서비스는 최신 키를 가져오고 해당 키를 암호화하여 장치에 암호화된 키를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-210">The service then gets the latest key, encrypts the keys, and sends the encrypted key to the device.</span></span>

#### <a name="to-synchronize-keys-for-storage-account-credentials-in-the-same-subscription-as-the-service-azure-only"></a><span data-ttu-id="9380d-211">서비스와 동일한 구독에서 저장소 계정 자격 증명에 대한 키를 동기화하려면(Azure에만 해당)</span><span class="sxs-lookup"><span data-stu-id="9380d-211">To synchronize keys for storage account credentials in the same subscription as the service (Azure only)</span></span>
1. <span data-ttu-id="9380d-212">서비스 방문 블레이드에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 섹션에서 **저장소 계정 자격 증명**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-212">On the service landing blade, select your service, double-click the service name, and then in the **Configuration** section, click **Storage account credentials**.</span></span>
2. <span data-ttu-id="9380d-213">**저장소 계정 자격 증명** 블레이드의 저장소 계정 자격 증명 목록에서 동기화하려는 키의 저장소 계정 자격 증명을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-213">On the **Storage account credentials** blade, in the list of Storage account credentials, select the storage account credential whose keys that you want to synchronize.</span></span>
3. <span data-ttu-id="9380d-214">선택한 저장소 계정 자격 증명의 **속성** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-214">In the **Properties** blade for the selected storage account credential, do the following:</span></span>
   
    1. <span data-ttu-id="9380d-215">**추가**를 클릭한 다음 **동기화 선택키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-215">Click **More**, and then click **Sync access key**.</span></span>
   
    2. <span data-ttu-id="9380d-216">확인 메시지가 나타나면 **동기화 키**를 클릭하여 동기화를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-216">When prompted for confirmation, click **Sync key** to complete the synchronization.</span></span>
    
4. <span data-ttu-id="9380d-217">StorSimple 장치 관리자 서비스에서 이전에 Microsoft Azure Storage 서비스에서 변경된 키를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-217">In the StorSimple Device Manager service, you need to update the key that was previously changed in the Microsoft Azure Storage service.</span></span> <span data-ttu-id="9380d-218">**동기화 저장소 계정 키** 블레이드에서 기본 선택키가 변경(다시 생성)되는 경우 [기본]을 클릭한 다음 **동기화 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-218">In the **Synchronize storage account key** blade, if the primary access key was changed (regenerated), click Primary, and then click **Sync Key**.</span></span> <span data-ttu-id="9380d-219">보조 키가 변경된 경우 **보조**를 클릭한 다음 **동기화 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-219">If the secondary key was changed, click **Secondary**, and then click **Sync Key**.</span></span>
   
    ![동기화 선택키](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a><span data-ttu-id="9380d-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9380d-221">Next steps</span></span>
* <span data-ttu-id="9380d-222">[StorSimple 가상 배열을 관리](storsimple-ova-web-ui-admin.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9380d-222">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

