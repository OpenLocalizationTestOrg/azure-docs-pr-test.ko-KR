---
title: "Microsoft Azure StorSimple 8000 시리즈 장치에 대 한 StorSimple 저장소 계정 자격 증명 aaaManage | Microsoft Docs"
description: "저장소 계정에 대 한 hello StorSimple 장치 관리자 구성 페이지 tooadd, 편집, 삭제 또는 회전 hello 보안 키를 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a><span data-ttu-id="c9dbc-103">Hello StorSimple 장치 관리자 서비스 toomanage 저장소 계정 자격 증명 사용</span><span class="sxs-lookup"><span data-stu-id="c9dbc-103">Use hello StorSimple Device Manager service toomanage your storage account credentials</span></span>

## <a name="overview"></a><span data-ttu-id="c9dbc-104">개요</span><span class="sxs-lookup"><span data-stu-id="c9dbc-104">Overview</span></span>

<span data-ttu-id="c9dbc-105">hello **구성** hello StorSimple 장치 관리자 서비스 블레이드에서 섹션에서는 hello StorSimple 장치 관리자 서비스에서에서 만들 수 있는 모든 hello 글로벌 서비스 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-105">hello **Configuration** section in hello StorSimple Device Manager service blade presents all hello global service parameters that can be created in hello StorSimple Device Manager service.</span></span> <span data-ttu-id="c9dbc-106">이러한 매개 변수에 적용 된 tooall hello 장치 toohello 서비스를 연결 하 고 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-106">These parameters can be applied tooall hello devices connected toohello service, and include:</span></span>

* <span data-ttu-id="c9dbc-107">저장소 계정 자격 증명</span><span class="sxs-lookup"><span data-stu-id="c9dbc-107">Storage account credentials</span></span>
* <span data-ttu-id="c9dbc-108">대역폭 템플릿</span><span class="sxs-lookup"><span data-stu-id="c9dbc-108">Bandwidth templates</span></span> 
* <span data-ttu-id="c9dbc-109">액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="c9dbc-109">Access control records</span></span> 

<span data-ttu-id="c9dbc-110">이 자습서에서는 tooadd를 편집 하거나 저장소 계정 자격 증명을 삭제 또는 저장소 계정에 대 한 hello 보안 키를 바꾸는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-110">This tutorial explains how tooadd, edit, or delete storage account credentials, or rotate hello security keys for a storage account.</span></span>

 ![저장소 계정 자격 증명 목록](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

<span data-ttu-id="c9dbc-112">저장소 계정은 hello StorSimple 장치 사용 하 여 tooaccess 저장소 계정과 클라우드 서비스 공급자는 hello 자격 증명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-112">Storage accounts contain hello credentials that hello StorSimple device uses tooaccess your storage account with your cloud service provider.</span></span> <span data-ttu-id="c9dbc-113">Microsoft Azure 저장소 계정에 대 한 hello 계정 이름 및 hello 기본 액세스 키 등의 자격 증명 이들은입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-113">For Microsoft Azure storage accounts, these are credentials such as hello account name and hello primary access key.</span></span> 

<span data-ttu-id="c9dbc-114">Hello에 **저장소 계정 자격 증명** 블레이드, 모든 저장소 계정을 구독 청구 hello에 대해 생성 된 hello 다음 정보를 포함 하는 테이블 형식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-114">On hello **Storage account credentials** blade, all storage accounts that are created for hello billing subscription are displayed in a tabular format containing hello following information:</span></span>

* <span data-ttu-id="c9dbc-115">**이름** – 만들어질 때 할당 된 고유한 이름 toohello 계정 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-115">**Name** – hello unique name assigned toohello account when it was created.</span></span>
* <span data-ttu-id="c9dbc-116">**SSL 사용 가능** – 여부 hello SSL을 사용 및 장치-클라우드 간 통신이 보안 채널 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-116">**SSL enabled** – Whether hello SSL is enabled and device-to-cloud communication is over hello secure channel.</span></span>
* <span data-ttu-id="c9dbc-117">**사용 하는** – hello hello 저장소 계정을 사용 하 여 볼륨의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-117">**Used by** – hello number of volumes using hello storage account.</span></span>

<span data-ttu-id="c9dbc-118">hello 가장 일반적인 작업 관련된 toostorage 계정을 수행할 수 있는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-118">hello most common tasks related toostorage accounts that can be performed are:</span></span>

* <span data-ttu-id="c9dbc-119">저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="c9dbc-119">Add a storage account</span></span> 
* <span data-ttu-id="c9dbc-120">저장소 계정 편집</span><span class="sxs-lookup"><span data-stu-id="c9dbc-120">Edit a storage account</span></span> 
* <span data-ttu-id="c9dbc-121">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="c9dbc-121">Delete a storage account</span></span> 
* <span data-ttu-id="c9dbc-122">저장소 계정의 키 회전</span><span class="sxs-lookup"><span data-stu-id="c9dbc-122">Key rotation of storage accounts</span></span> 

## <a name="types-of-storage-accounts"></a><span data-ttu-id="c9dbc-123">저장소 계정 유형</span><span class="sxs-lookup"><span data-stu-id="c9dbc-123">Types of storage accounts</span></span>

<span data-ttu-id="c9dbc-124">StorSimple 장치에서 사용할 수 있는 저장소 계정에는 다음과 같은 세 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-124">There are three types of storage accounts that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="c9dbc-125">**자동 생성 된 저장소 계정은** – hello 서비스를 처음 만들 때 이러한 유형의 저장소 계정 자동으로 생성 hello 이름에서 알 수 있듯이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-125">**Auto-generated storage accounts** – As hello name suggests, this type of storage account is automatically generated when hello service is first created.</span></span> <span data-ttu-id="c9dbc-126">이 저장소 계정을 만든 방법에 대해 자세히 toolearn 참조 [1 단계: 새 서비스 만들기](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) 에 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-126">toolearn more about how this storage account is created, see [Step 1: Create a new service](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span> 
* <span data-ttu-id="c9dbc-127">**Hello 서비스 구독의 저장소 계정에에서** – hello와 관련 된 hello Azure 저장소 계정 hello 서비스와 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-127">**Storage accounts in hello service subscription** – These are hello Azure storage accounts that are associated with hello same subscription as that of hello service.</span></span> <span data-ttu-id="c9dbc-128">이러한 저장소 계정이 생성 되는 방법에 대해 자세히 toolearn 참조 [Azure 저장소 계정에 대 한](../storage/common/storage-create-storage-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-128">toolearn more about how these storage accounts are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span> 
* <span data-ttu-id="c9dbc-129">**Hello 서비스 구독 외부 저장소 계정** – 서비스와 연결 되지 않은 hello Azure 저장소 계정 및 가능성이 하기 전에 기존된 hello 서비스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-129">**Storage accounts outside of hello service subscription** – These are hello Azure storage accounts that are not associated with your service and likely existed before hello service was created.</span></span>

## <a name="add-a-storage-account"></a><span data-ttu-id="c9dbc-130">저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="c9dbc-130">Add a storage account</span></span>

<span data-ttu-id="c9dbc-131">고유한 제공 하 여 저장소 계정을 추가할 수 있습니다 친숙 한 이름 및 액세스 자격 증명을 toohello 저장소 계정 (hello 지정 된 클라우드 서비스 공급자)에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-131">You can add a storage account by providing a unique friendly name and access credentials that are linked toohello storage account (with hello specified cloud service provider).</span></span> <span data-ttu-id="c9dbc-132">Hello secure sockets layer (SSL) 모드 toocreate 장치와 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널 설정의 hello 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-132">You also have hello option of enabling hello secure sockets layer (SSL) mode toocreate a secure channel for network communication between your device and hello cloud.</span></span>

<span data-ttu-id="c9dbc-133">특정 클라우드 서비스 공급자에 대해 여러 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="c9dbc-134">그러나 주의 저장소 계정이 만들어지면 hello 클라우드 서비스 공급자 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-134">Be aware, however, that after a storage account is created, you cannot change hello cloud service provider.</span></span>

<span data-ttu-id="c9dbc-135">Hello 저장소 계정, 저장 하는 동안 hello 서비스는 클라우드 서비스 공급자와 toocommunicate을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-135">While hello storage account is being saved, hello service attempts toocommunicate with your cloud service provider.</span></span> <span data-ttu-id="c9dbc-136">이 이번에 hello 자격 증명 및 사용자가 제공한 hello 액세스 자료가 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-136">hello credentials and hello access material that you supplied will be authenticated at this time.</span></span> <span data-ttu-id="c9dbc-137">저장소 계정에는 hello 인증에 성공 하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-137">A storage account is created only if hello authentication succeeds.</span></span> <span data-ttu-id="c9dbc-138">Hello 인증에 실패 하면 적절 한 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-138">If hello authentication fails, then an appropriate error message will be displayed.</span></span>

<span data-ttu-id="c9dbc-139">다음 프로시저 tooadd Azure 저장소 계정 자격 증명 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-139">Use hello following procedures tooadd Azure storage account credentials:</span></span>

* <span data-ttu-id="c9dbc-140">저장소 계정 자격 증명 tooadd hello hello 장치 관리자 서비스와 동일한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="c9dbc-140">tooadd a storage account credential that has hello same Azure subscription as hello Device Manager service</span></span>
* <span data-ttu-id="c9dbc-141">tooadd hello 장치 관리자 서비스 구독 외부의 Azure 저장소 계정 자격 증명</span><span class="sxs-lookup"><span data-stu-id="c9dbc-141">tooadd an Azure storage account credential that is outside of hello Device Manager service subscription</span></span>

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a><span data-ttu-id="c9dbc-142">tooadd hello StorSimple 장치 관리자 서비스 구독 외부 Azure 저장소 계정 자격 증명</span><span class="sxs-lookup"><span data-stu-id="c9dbc-142">tooadd an Azure storage account credential outside of hello StorSimple Device Manager service subscription</span></span>

1. <span data-ttu-id="c9dbc-143">Tooyour StorSimple 장치 관리자 서비스를 찾아 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-143">Navigate tooyour StorSimple Device Manager service, select and double-click it.</span></span> <span data-ttu-id="c9dbc-144">Hello 열립니다 **개요** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-144">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="c9dbc-145">선택 **저장소 계정 자격 증명** hello 내 **구성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-145">Select **Storage account credentials** within hello **Configuration** section.</span></span> <span data-ttu-id="c9dbc-146">Hello StorSimple 장치 관리자 서비스와 관련 된 모든 기존 저장소 계정 자격 증명을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-146">This lists any existing storage account credentials associated with hello StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="c9dbc-147">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-147">Click **Add**.</span></span>
4. <span data-ttu-id="c9dbc-148">Hello에 **저장소 계정 자격 증명 추가** 블레이드에서 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="c9dbc-148">In hello **Add a storage account credential** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="c9dbc-149">**구독**에 **기타**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-149">For **Subscription**, select **Other**.</span></span>
   
    2. <span data-ttu-id="c9dbc-150">Azure 저장소 계정 자격 증명의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-150">Provide hello name of your Azure storage account credential.</span></span>
   
    3. <span data-ttu-id="c9dbc-151">Hello에 **저장소 계정 액세스 키** 텍스트 상자 공급 hello Azure 저장소 계정 자격 증명에 대 한 기본 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-151">In hello **Storage account access key** text box, supply hello primary Access Key for your Azure storage account credential.</span></span> <span data-ttu-id="c9dbc-152">이 키 tooget toohello Azure 저장소 서비스를 이동 저장소 계정 자격 증명을 선택 하 고 클릭 **계정 키를 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-152">tooget this key, go toohello Azure Storage service, select your storage account credential, and click **Manage account keys**.</span></span> <span data-ttu-id="c9dbc-153">이제 hello 기본 액세스 키를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-153">You can now copy hello primary access key.</span></span>
   
    4. <span data-ttu-id="c9dbc-154">SSL을 tooenable 클릭 hello **사용** 단추 toocreate StorSimple 장치 관리자 서비스와 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-154">tooenable SSL, click hello **Enable** button toocreate a secure channel for network communication between your StorSimple Device Manager service and hello cloud.</span></span> <span data-ttu-id="c9dbc-155">Hello 클릭 **사용 하지 않도록 설정** 사설 클라우드 내에서 작동 하는 경우에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-155">Click hello **Disable** button only if you are operating within a private cloud.</span></span>
   
    5. <span data-ttu-id="c9dbc-156">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-156">Click **Add**.</span></span> <span data-ttu-id="c9dbc-157">저장소 계정 자격 증명 hello 정상적으로 만들어지면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-157">You are notified after hello storage account credential is successfully created.</span></span>

5. <span data-ttu-id="c9dbc-158">hello 새로 만든 저장소 계정 자격 증명 hello 장치 관리자를 구성 하는 StorSimple 서비스 블레이드 아래에 표시 되는 **저장소 계정 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-158">hello newly created storage account credential is displayed on hello StorSimple Configure Device Manager service blade under **Storage account credentials**.</span></span>
   


## <a name="edit-a-storage-account"></a><span data-ttu-id="c9dbc-159">저장소 계정 편집</span><span class="sxs-lookup"><span data-stu-id="c9dbc-159">Edit a storage account</span></span>

<span data-ttu-id="c9dbc-160">볼륨 컨테이너에서 사용되는 저장소 계정을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-160">You can edit a storage account that is used by a volume container.</span></span> <span data-ttu-id="c9dbc-161">현재 사용 중인 저장소 계정을 편집할 경우 hello 필드 에서만 사용할 수 있는 toomodify는 hello hello 저장소 계정 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-161">If you edit a storage account that is currently in use, hello only field available toomodify is hello access key for hello storage account.</span></span> <span data-ttu-id="c9dbc-162">Hello 새로운 저장소 액세스 키를 제공 하 고 업데이트 hello 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-162">You can supply hello new storage access key and save hello updated settings.</span></span>

#### <a name="tooedit-a-storage-account"></a><span data-ttu-id="c9dbc-163">tooedit 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c9dbc-163">tooedit a storage account</span></span>

1. <span data-ttu-id="c9dbc-164">Tooyour StorSimple 장치 관리자 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-164">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="c9dbc-165">Hello에 **구성** 섹션에서 클릭 **저장소 계정 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-165">In hello **Configuration** section, click **Storage account credentials**.</span></span>

    ![저장소 계정 자격 증명](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. <span data-ttu-id="c9dbc-167">Hello에 **저장소 계정 자격 증명** 블레이드에서 저장소 계정 자격 증명을 선택 hello 목록에서 하 고 hello tooedit 시겠습니까 하나 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-167">In hello **Storage account credentials** blade, from hello list of storage account credentials, select and click hello one you wish tooedit.</span></span> 

3. <span data-ttu-id="c9dbc-168">Hello를 수정할 수 있습니다 **SSL 사용** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-168">You can modify hello **Enable SSL** selection.</span></span> <span data-ttu-id="c9dbc-169">클릭할 수도 있습니다 **더...**  선택한 후 **동기화 액세스 키 toorotate** 저장소 계정 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-169">You can also click **More...** and then select **Sync access key toorotate** your storage account access keys.</span></span> <span data-ttu-id="c9dbc-170">너무 이동[키 저장소 계정의 순환](#key-rotation-of-storage-accounts) tooperform 키 순환 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-170">Go too[Key rotation of storage accounts](#key-rotation-of-storage-accounts) for more information on how tooperform key rotation.</span></span> <span data-ttu-id="c9dbc-171">Hello 설정을 수정한 후 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-171">After you have modified hello settings, click **Save**.</span></span> 

    ![편집된 저장소 계정 자격 증명 저장](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. <span data-ttu-id="c9dbc-173">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-173">When prompted for confirmation, click **Yes**.</span></span> 

    ![수정 확인](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

<span data-ttu-id="c9dbc-175">hello 설정은 업데이트 하 고 저장소 계정에 대 한 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-175">hello settings will be updated and saved for your storage account.</span></span> 

## <a name="delete-a-storage-account"></a><span data-ttu-id="c9dbc-176">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="c9dbc-176">Delete a storage account</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9dbc-177">볼륨 컨테이너에서 사용하지 않는 경우에만 저장소 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-177">You can delete a storage account only if it is not used by a volume container.</span></span> <span data-ttu-id="c9dbc-178">저장소 계정이 볼륨 컨테이너에서 사용 중인 먼저 hello 볼륨 컨테이너를 삭제 한 다음 hello 연결 된 저장소 계정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-178">If a storage account is being used by a volume container, first delete hello volume container and then delete hello associated storage account.</span></span>

#### <a name="toodelete-a-storage-account"></a><span data-ttu-id="c9dbc-179">toodelete 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c9dbc-179">toodelete a storage account</span></span>

1. <span data-ttu-id="c9dbc-180">Tooyour StorSimple 장치 관리자 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-180">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="c9dbc-181">Hello에 **구성** 섹션에서 클릭 **저장소 계정 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-181">In hello **Configuration** section, click **Storage account credentials**.</span></span>

2. <span data-ttu-id="c9dbc-182">저장소 계정의 hello 테이블 형식 목록에서 원하는 toodelete hello 계정 마우스로 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-182">In hello tabular list of storage accounts, hover over hello account that you wish toodelete.</span></span> <span data-ttu-id="c9dbc-183">Tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-183">Right-click tooinvoke hello context menu and click **Delete**.</span></span>

    ![저장소 계정 자격 증명 삭제](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. <span data-ttu-id="c9dbc-185">확인 메시지가 나타나면 클릭 **예** toocontinue hello 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-185">When prompted for confirmation, click **Yes** toocontinue with hello deletion.</span></span> <span data-ttu-id="c9dbc-186">hello 테이블 형식 목록에는 업데이트 된 tooreflect hello 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-186">hello tabular listing will be updated tooreflect hello changes.</span></span>

    ![삭제 확인](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a><span data-ttu-id="c9dbc-188">저장소 계정의 키 회전</span><span class="sxs-lookup"><span data-stu-id="c9dbc-188">Key rotation of storage accounts</span></span>

<span data-ttu-id="c9dbc-189">보안상의 이유로 키 회전이 데이터 센터에서 요구되기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-189">For security reasons, key rotation is often a requirement in data centers.</span></span> <span data-ttu-id="c9dbc-190">각 Microsoft Azure 구독에 하나 이상의 연결된 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-190">Each Microsoft Azure subscription can have one or more associated storage accounts.</span></span> <span data-ttu-id="c9dbc-191">hello 액세스 toothese 계정은 hello 구독 및 각 저장소 계정에 대 한 선택 키에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-191">hello access toothese accounts is controlled by hello subscription and access keys for each storage account.</span></span> 

<span data-ttu-id="c9dbc-192">저장소 계정을 만들 때 Microsoft Azure hello 저장소 계정에 액세스할 때 인증에 사용 되는 두 개의 512 비트 저장소 액세스 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-192">When you create a storage account, Microsoft Azure generates two 512-bit storage access keys that are used for authentication when hello storage account is accessed.</span></span> <span data-ttu-id="c9dbc-193">두 개의 저장소 액세스 키를 갖는 것 중단 tooyour 저장소 서비스와 액세스 toothat 서비스 없는 tooregenerate hello 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-193">Having two storage access keys allows you tooregenerate hello keys with no interruption tooyour storage service or access toothat service.</span></span> <span data-ttu-id="c9dbc-194">hello 현재 사용 중인 키는 hello *기본* 키와 hello 백업 키가 참조 tooas hello *보조* 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-194">hello key that is currently in use is hello *primary* key and hello backup key is referred tooas hello *secondary* key.</span></span> <span data-ttu-id="c9dbc-195">Microsoft Azure StorSimple 장치가 클라우드 저장소 서비스 공급자에 액세스할 때 이러한 두 키 중 하나를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-195">One of these two keys must be supplied when your Microsoft Azure StorSimple device accesses your cloud storage service provider.</span></span>

## <a name="what-is-key-rotation"></a><span data-ttu-id="c9dbc-196">키 회전 정의</span><span class="sxs-lookup"><span data-stu-id="c9dbc-196">What is key rotation?</span></span>

<span data-ttu-id="c9dbc-197">일반적으로 응용 프로그램 중 하나만 사용 hello 키 tooaccess 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-197">Typically, applications use only one of hello keys tooaccess your data.</span></span> <span data-ttu-id="c9dbc-198">특정 시간이 지나면, toousing hello에 대 한 두 번째 키 전환 하는 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-198">After a certain period of time, you can have your applications switch over toousing hello second key.</span></span> <span data-ttu-id="c9dbc-199">응용 프로그램 toohello 보조 키를 전환한 후 hello 첫 번째 키를 사용 중지 하 고 새 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-199">After you have switched your applications toohello secondary key, you can retire hello first key and then generate a new key.</span></span> <span data-ttu-id="c9dbc-200">이러한 방식으로 hello 두 키를 사용 하 여 가동 중지 시간 없이 응용 프로그램 액세스 toohello 데이터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-200">Using hello two keys this way allows your applications access toohello data without incurring any downtime.</span></span>

<span data-ttu-id="c9dbc-201">hello 저장소 계정 키는 항상 암호화 된 형태로 hello 서비스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-201">hello storage account keys are always stored in hello service in an encrypted form.</span></span> <span data-ttu-id="c9dbc-202">그러나 이러한 hello StorSimple 장치 관리자 서비스를 통해 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-202">However, these can be reset via hello StorSimple Device Manager service.</span></span> <span data-ttu-id="c9dbc-203">hello 서비스는 hello 기본 키를 얻을 수 있습니다 및 보조 키 hello 기본 저장소 계정을 hello 저장소 서비스에서 만들어지는 계정과 포함 하 여 동일한 구독을 생성 하는 hello에 있는 저장소 계정의 모든 hello에 대 한 StorSimple 장치 관리자 hello 때 서비스 서비스를 처음 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-203">hello service can get hello primary key and secondary key for all hello storage accounts in hello same subscription, including accounts created in hello Storage service as well as hello default storage accounts generated when hello StorSimple Device Manager service service was first created.</span></span> <span data-ttu-id="c9dbc-204">hello StorSimple 장치 관리자 서비스는 항상 이러한 키 hello Azure 클래식 포털에서에서 가져오고 그런 다음 암호화 된 방식에서 모두를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-204">hello StorSimple Device Manager service will always get these keys from hello Azure classic portal and then store them in an encrypted manner.</span></span>

## <a name="rotation-workflow"></a><span data-ttu-id="c9dbc-205">회전 워크플로</span><span class="sxs-lookup"><span data-stu-id="c9dbc-205">Rotation workflow</span></span>

<span data-ttu-id="c9dbc-206">Microsoft Azure 관리자가 다시 생성 하거나 (Microsoft Azure 저장소 서비스 hello)를 통해 hello 저장소 계정에 직접 액세스 하 여 hello 기본 또는 보조 키를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-206">A Microsoft Azure administrator can regenerate or change hello primary or secondary key by directly accessing hello storage account (via hello Microsoft Azure Storage service).</span></span> <span data-ttu-id="c9dbc-207">hello StorSimple 장치 관리자 서비스는이 변경 내용을 자동으로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-207">hello StorSimple Device Manager service does not see this change automatically.</span></span>

<span data-ttu-id="c9dbc-208">hello 변경의 tooinform hello StorSimple 장치 관리자 서비스를 해야 tooaccess hello StorSimple 장치 관리자 서비스 hello 저장소 계정에 액세스 한 후 (변경 된 어떤 것에 따라) hello 기본 또는 보조 키를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-208">tooinform hello StorSimple Device Manager service of hello change, you will need tooaccess hello StorSimple Device Manager service, access hello storage account, and then synchronize hello primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="c9dbc-209">hello 서비스 다음 hello 최신 키를 가져옵니다, 그리고 hello 키 암호화 및 hello 키 toohello 장치 암호화를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-209">hello service then gets hello latest key, encrypts hello keys, and sends hello encrypted key toohello device.</span></span>

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a><span data-ttu-id="c9dbc-210">저장소 계정에 대 한 키 toosynchronize hello hello 서비스와 같은 구독</span><span class="sxs-lookup"><span data-stu-id="c9dbc-210">toosynchronize keys for storage accounts in hello same subscription as hello service</span></span> 
1. <span data-ttu-id="c9dbc-211">Tooyour StorSimple 장치 관리자 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-211">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="c9dbc-212">Hello에 **구성** 섹션에서 클릭 **저장소 계정 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-212">In hello **Configuration** section, click **Storage account credentials**.</span></span>
2. <span data-ttu-id="c9dbc-213">저장소 계정의 테이블 형식 목록 hello에서 원하는 toomodify hello 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-213">From hello tabular listing of storage accounts, click hello one that you want toomodify.</span></span> 

    ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. <span data-ttu-id="c9dbc-215">클릭 **중... 더 많은** 선택한 후 **동기화 액세스 키 toorotate**합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-215">Click **...More** and then select **Sync access key toorotate**.</span></span>   

    ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. <span data-ttu-id="c9dbc-217">StorSimple 장치 관리자 서비스 hello hello Microsoft Azure 저장소 서비스에서에서 이전에 변경 된 tooupdate hello 키를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-217">In hello StorSimple Device Manager service, you need tooupdate hello key that was previously changed in hello Microsoft Azure Storage service.</span></span> <span data-ttu-id="c9dbc-218">Hello 기본 액세스 키 (다시 생성)가 변경 되었을 경우 선택 **기본** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-218">If hello primary access key was changed (regenerated), select **primary** key.</span></span> <span data-ttu-id="c9dbc-219">Hello 보조 키가 변경 된 경우 선택 **보조** 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-219">If hello secondary key was changed, select **secondary** key.</span></span> <span data-ttu-id="c9dbc-220">**키 동기화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-220">Click **Sync key**.</span></span>
      
      ![키 동기화](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

<span data-ttu-id="c9dbc-222">Hello 키가 성공적으로 sycnhronized 후 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-222">You will be notified after hello key is successfully sycnhronized.</span></span>

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a><span data-ttu-id="c9dbc-223">toosynchronize는 hello 서비스 구독 외부 저장소 계정에 대 한 키</span><span class="sxs-lookup"><span data-stu-id="c9dbc-223">toosynchronize keys for storage accounts outside of hello service subscription</span></span>
1. <span data-ttu-id="c9dbc-224">Hello에 **서비스** 페이지에서 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-224">On hello **Services** page, click hello **Configure** tab.</span></span>
2. <span data-ttu-id="c9dbc-225">**저장소 계정 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-225">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="c9dbc-226">Hello 대화 상자에서 수행 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-226">In hello dialog box, do hello following:</span></span>
   
   1. <span data-ttu-id="c9dbc-227">원하는 tooupdate hello 액세스 키를 가진 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-227">Select hello storage account with hello access key that you want tooupdate.</span></span>
   2. <span data-ttu-id="c9dbc-228">StorSimple 장치 관리자 서비스 hello tooupdate hello 저장소 액세스 키를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-228">You will need tooupdate hello storage access key in hello StorSimple Device Manager service.</span></span> <span data-ttu-id="c9dbc-229">이 경우 hello 저장소 액세스 키를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-229">In this case, you can see hello storage access key.</span></span> <span data-ttu-id="c9dbc-230">Hello에 hello 새 키를 입력 **저장소 계정 액세스 키** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-230">Enter hello new key in hello **Storage Account Access Key** box.</span></span> 
   3. <span data-ttu-id="c9dbc-231">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-231">Save your changes.</span></span> <span data-ttu-id="c9dbc-232">이제 저장소 계정 액세스 키가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-232">Your storage account access key should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9dbc-233">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9dbc-233">Next steps</span></span>
* <span data-ttu-id="c9dbc-234">[StorSimple 보안](storsimple-8000-security.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-234">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="c9dbc-235">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c9dbc-235">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

