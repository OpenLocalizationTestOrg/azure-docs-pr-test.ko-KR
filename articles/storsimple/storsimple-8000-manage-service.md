---
title: "Azure에서 StorSimple 장치 관리자 서비스 배포 | Microsoft Docs"
description: "Azure Portal에서 StorSimple Device Manager 서비스를 만들고 삭제하는 방법 및 서비스 등록 키를 관리하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: 22bb4a32f006d7e49356743c2a87eb622a61d18e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a><span data-ttu-id="da8a8-103">StorSimple 8000 시리즈 장치에 StorSimple 장치 관리자 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="da8a8-103">Deploy the StorSimple Device Manager service for StorSimple 8000 series devices</span></span>

## <a name="overview"></a><span data-ttu-id="da8a8-104">개요</span><span class="sxs-lookup"><span data-stu-id="da8a8-104">Overview</span></span>

<span data-ttu-id="da8a8-105">StorSimple Device Manager 서비스는 Microsoft Azure에서 실행되며 여러 StorSimple 장치에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="da8a8-106">서비스를 만든 후에 단일 중앙 위치에서 StorSimple 장치 관리자 서비스에 연결된 모든 장치를 관리하는 데 사용하여 관리 부담을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-106">After you create the service, you can use it to manage all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="da8a8-107">이 자습서에서는 서비스 만들기, 삭제, 마이그레이션 및 서비스 등록 키 관리에 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-107">This tutorial describes the steps required for the creation, deletion, migration of the service and the management of the service registration key.</span></span> <span data-ttu-id="da8a8-108">이 문서에 포함된 정보는 StorSimple 8000 시리즈 장치에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-108">The information contained in this article is applicable only to StorSimple 8000 series devices.</span></span> <span data-ttu-id="da8a8-109">StorSimple 가상 배열에 대한 자세한 내용은 [StorSimple 가상 배열에 StorSimple 장치 관리자 서비스 배포](storsimple-virtual-array-manage-service.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-109">For more information on StorSimple Virtual Arrays, go to [deploy a StorSimple Device Manager service for your StorSimple Virtual Array](storsimple-virtual-array-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="da8a8-110">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="da8a8-110">Create a service</span></span>
<span data-ttu-id="da8a8-111">StorSimple 장치 관리자 서비스를 만들려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-111">To create a StorSimple Device Manager service, you need to have:</span></span>

* <span data-ttu-id="da8a8-112">엔터프라이즈 계약을 사용하여 구독</span><span class="sxs-lookup"><span data-stu-id="da8a8-112">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="da8a8-113">활성 Microsoft Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="da8a8-113">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="da8a8-114">액세스 관리에 사용되는 청구 정보</span><span class="sxs-lookup"><span data-stu-id="da8a8-114">The billing information that is used for access management</span></span>

<span data-ttu-id="da8a8-115">기업 규약을 포함하는 구독만이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-115">Only the subscriptions with an Enterprise Agreement are allowed.</span></span> <span data-ttu-id="da8a8-116">Azure 클래식 포털에서 허용된 Microsoft 스폰서쉽 구독은 Azure Portal에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-116">Microsoft Sponsorship subscriptions that were allowed in the Azure classic portal are not supported in the Azure portal.</span></span> <span data-ttu-id="da8a8-117">지원되지 않는 구독을 사용하는 경우 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-117">You will see the following message when using an unsupported subscription:</span></span>

![유효하지 않은 구독](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

<span data-ttu-id="da8a8-119">또한 서비스를 만들 때 기본 저장소 계정을 생성하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-119">You can also choose to generate a default storage account when you create the service.</span></span>

<span data-ttu-id="da8a8-120">하나의 서비스로 여러 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-120">A single service can manage multiple devices.</span></span> <span data-ttu-id="da8a8-121">하지만 하나의 장치는 여러 서비스로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-121">However, a device cannot span multiple services.</span></span> <span data-ttu-id="da8a8-122">대규모 엔터프라이즈는 서로 다른 구독, 조직 또는 배포 위치와 동작하는 여러 서비스 인스턴스를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-122">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span> 

> [!NOTE]
> <span data-ttu-id="da8a8-123">StorSimple 8000 시리즈 장치와 StorSimple 가상 배열을 관리하려면 별도의 StorSimple Device Manager 서비스 인스턴스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-123">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>

<span data-ttu-id="da8a8-124">서비스를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-124">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


<span data-ttu-id="da8a8-125">각 StorSimple 장치 관리자 서비스에 대해 다음과 같은 특성이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-125">For each StorSimple Device Manager service, the following attributes exist:</span></span>

* <span data-ttu-id="da8a8-126">**이름** – StorSimple 장치 관리자 서비스를 만들었을 때 할당된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-126">**Name** – The name that was assigned to your StorSimple Device Manager service when it was created.</span></span> <span data-ttu-id="da8a8-127">**서비스 이름은 서비스를 만든 후에 변경할 수 없습니다. Azure Portal에서 이름을 바꿀 수 없는 장치, 볼륨, 볼륨 컨테이너 및 백업 정책 같은 기타 엔터티에도 마찬가지입니다.**</span><span class="sxs-lookup"><span data-stu-id="da8a8-127">**The service name cannot be changed after the service is created. This is also true for other entities such as devices, volumes, volume containers, and backup policies that cannot be renamed in the Azure portal.**</span></span>
* <span data-ttu-id="da8a8-128">**상태** – **활성**, **만들기** 또는 **온라인** 등의 서비스 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-128">**Status** – The status of the service, which can be **Active**, **Creating**, or **Online**.</span></span>
* <span data-ttu-id="da8a8-129">**위치** – StorSimple 장치를 배포할 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-129">**Location** – The geographical location in which the StorSimple device will be deployed.</span></span>
* <span data-ttu-id="da8a8-130">**구독** – 서비스와 연관된 청구 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-130">**Subscription** – The billing subscription that is associated with your service.</span></span>

## <a name="move-a-service-to-azure-portal"></a><span data-ttu-id="da8a8-131">Azure Portal에 서비스 이동</span><span class="sxs-lookup"><span data-stu-id="da8a8-131">Move a service to Azure portal</span></span>
<span data-ttu-id="da8a8-132">이제 Azure Portal에서 StorSimple 8000 시리즈를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-132">StorSimple 8000 series can be now managed in the Azure portal.</span></span> <span data-ttu-id="da8a8-133">기존 서비스로 StorSimple 장치를 관리하는 경우 Azure Portal에 서비스를 이동하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-133">If you have an existing service to manage the StorSimple devices, we recommend that you move your service to the Azure portal.</span></span> <span data-ttu-id="da8a8-134">2017년 9월 30일 이후에 StorSimple Manager 서비스에 Azure 클래식 포털을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-134">The Azure classic portal for the StorSimple Manager service is not available after September 30, 2017.</span></span>

<span data-ttu-id="da8a8-135">Azure Portal로 마이그레이션할 옵션은 단계별로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-135">The option to migrate to the Azure portal is available in phases.</span></span> <span data-ttu-id="da8a8-136">Azure Portal로 마이그레이션할 옵션이 표시되지 않지만 [전환에 대한 고려 사항](#considerations-for-transition)에 설명된 대로 이동하고 마이그레이션의 영향을 검토해야 하는 경우 [요청을 제출](https://aka.ms/ss8000-cx-signup)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-136">If you do not see an option to migrate to Azure portal but you want to move and have reviewed the impact of migration as documented in the [Considerations for transition](#considerations-for-transition), you can [submit a request](https://aka.ms/ss8000-cx-signup).</span></span>

### <a name="considerations-for-transition"></a><span data-ttu-id="da8a8-137">전환에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="da8a8-137">Considerations for transition</span></span>

<span data-ttu-id="da8a8-138">서비스를 이동하기 전에 새 Azure Portal로 마이그레이션하는 작업의 영향을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-138">Review the impact of migrating to the new Azure portal before you move the service.</span></span>

#### <a name="before-you-transition"></a><span data-ttu-id="da8a8-139">전환하기 전에</span><span class="sxs-lookup"><span data-stu-id="da8a8-139">Before you transition</span></span>

* <span data-ttu-id="da8a8-140">장치가 업데이트 3.0 이상을 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-140">Your device is running Update 3.0 or later.</span></span> <span data-ttu-id="da8a8-141">장치에서 이전 버전을 실행 중인 경우 최신 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-141">If your device is running an older version, install the latest updates.</span></span> <span data-ttu-id="da8a8-142">자세한 내용은 [업데이트 4 설치](storsimple-8000-install-update-4.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="da8a8-142">For more information, go to [Install Update 4](storsimple-8000-install-update-4.md).</span></span> <span data-ttu-id="da8a8-143">StorSimple Cloud Appliance(8010/8020)를 사용하는 경우 업데이트 4.0을 사용하여 새로운 클라우드 어플라이언스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-143">If using a StorSimple Cloud Appliance (8010/8020), create a new cloud appliance with Update 4.0.</span></span> 

* <span data-ttu-id="da8a8-144">새 Azure Portal로 전환하면 StorSimple 장치를 관리하는 데 Azure 클래식 포털을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-144">Once you are transitioned to the new Azure portal, you cannot use the Azure classic portal to manage your StorSimple device.</span></span>

* <span data-ttu-id="da8a8-145">전환은 중단되지 않으며 장치에 대한 가동 중지 시간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-145">The transition is non-disruptive and there is no downtime for the device.</span></span>

* <span data-ttu-id="da8a8-146">지정된 구독에서 모든 StorSimple 장치 관리자가 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-146">All the StorSimple Device Managers under the specified subscription are transitioned.</span></span>

#### <a name="during-the-transition"></a><span data-ttu-id="da8a8-147">전환 중</span><span class="sxs-lookup"><span data-stu-id="da8a8-147">During the transition</span></span>

* <span data-ttu-id="da8a8-148">포털에서 장치를 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-148">You cannot manage your device from the portal.</span></span>
* <span data-ttu-id="da8a8-149">계층화 및 예약된 백업 등의 작업이 계속 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-149">Operations such as tiering and scheduled backups continue to occur.</span></span>
* <span data-ttu-id="da8a8-150">전환이 진행 중인 동안 이전 StorSimple 장치 관리자를 삭제하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="da8a8-150">Do not delete the old StorSimple Device Managers while the transition is in progress.</span></span>

#### <a name="after-the-transition"></a><span data-ttu-id="da8a8-151">전환 후</span><span class="sxs-lookup"><span data-stu-id="da8a8-151">After the transition</span></span>

* <span data-ttu-id="da8a8-152">클래식 포털에서 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-152">You can no longer manage your devices from the classic portal.</span></span>

* <span data-ttu-id="da8a8-153">기존 ASM(Azure Service Management) PowerShell cmdlet이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-153">The existing Azure Service Management (ASM) PowerShell cmdlets are not supported.</span></span> <span data-ttu-id="da8a8-154">Azure Resource Manager를 통해 장치를 관리하기 위해 스크립트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-154">Update the scripts to manage your devices through the Azure Resource Manager.</span></span>

* <span data-ttu-id="da8a8-155">서비스 및 장치 구성이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-155">Your service and device configuration are retained.</span></span> <span data-ttu-id="da8a8-156">또한 모든 볼륨과 백업이 Azure Portal로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-156">All your volumes and backups are also transitioned to the Azure portal.</span></span>

### <a name="begin-transition"></a><span data-ttu-id="da8a8-157">전환 시작</span><span class="sxs-lookup"><span data-stu-id="da8a8-157">Begin transition</span></span>

<span data-ttu-id="da8a8-158">Azure Portal로 서비스를 전환하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-158">Perform the following steps to transition your service to the Azure portal.</span></span>

1. <span data-ttu-id="da8a8-159">클래식 포털에서 기존 StorSimple Manager 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-159">Go to your existing StorSimple Manager service in the classic portal.</span></span>

2. <span data-ttu-id="da8a8-160">StorSimple 장치 관리자 서비스를 지금 Azure Portal에서 사용할 수 있는지를 알려 주는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-160">You see a notification that informs you that the StorSimple Device Manager service is now available in the Azure portal.</span></span> <span data-ttu-id="da8a8-161">Azure Portal에서 서비스는 StorSimple 장치 관리자 서비스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-161">Note that in the Azure portal, the service is referred to as StorSimple Device Manager service.</span></span>

    ![마이그레이션 알림](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. <span data-ttu-id="da8a8-163">마이그레이션의 전체 영향을 검토했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-163">Ensure that you have reviewed the full impact of migration.</span></span>
    2. <span data-ttu-id="da8a8-164">클래식 포털에서 이동된 StorSimple 장치 관리자의 목록을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-164">Review the list of StorSimple Device Managers that will be moved from the classic portal.</span></span>

3. <span data-ttu-id="da8a8-165">**마이그레이션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-165">Click **Migrate**.</span></span> <span data-ttu-id="da8a8-166">전환이 시작되고 완료하는 데 몇 분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-166">The transition begins and takes a few minutes to complete.</span></span>

<span data-ttu-id="da8a8-167">전환이 완료되면 Azure Portal에서 StorSimple 장치 관리자 서비스를 통해 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-167">Once the transition is complete, you can manage your devices via the StorSimple Device Manager service in the Azure portal.</span></span>

<span data-ttu-id="da8a8-168">Azure Portal에서는 업데이트 3.0 이상을 실행하는 StorSimple 장치만이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-168">In the Azure portal, only the StorSimple devices running Update 3.0 and higher are supported.</span></span> <span data-ttu-id="da8a8-169">이전 버전을 실행하는 장치에는 제한된 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-169">The devices that are running older versions have limited support.</span></span> <span data-ttu-id="da8a8-170">다음 표에서는 클래식에서 Azure Portal로 마이그레이션하면 업데이트 3.0 이전 버전을 실행하는 장치에 지원되는 작업을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-170">The following table summrizes which operations are supported on the device running versios prior to Update 3.0, once you have migrated from the classic to the Azure portal.</span></span>

| <span data-ttu-id="da8a8-171">작업</span><span class="sxs-lookup"><span data-stu-id="da8a8-171">Operation</span></span>                                                                                                                       | <span data-ttu-id="da8a8-172">지원됨</span><span class="sxs-lookup"><span data-stu-id="da8a8-172">Supported</span></span>      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| <span data-ttu-id="da8a8-173">장치 등록</span><span class="sxs-lookup"><span data-stu-id="da8a8-173">Register a device</span></span>                                                                                                               | <span data-ttu-id="da8a8-174">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-174">Yes</span></span>            |
| <span data-ttu-id="da8a8-175">일반, 네트워크 및 보안과 같은 장치 설정 구성</span><span class="sxs-lookup"><span data-stu-id="da8a8-175">Configure device settings such as general, network, and security</span></span>                                                                | <span data-ttu-id="da8a8-176">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-176">Yes</span></span>            |
| <span data-ttu-id="da8a8-177">업데이트 검사, 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="da8a8-177">Scan, download, and install updates</span></span>                                                                                             | <span data-ttu-id="da8a8-178">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-178">Yes</span></span>            |
| <span data-ttu-id="da8a8-179">장치 비활성화</span><span class="sxs-lookup"><span data-stu-id="da8a8-179">Deactivate device</span></span>                                                                                                               | <span data-ttu-id="da8a8-180">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-180">Yes</span></span>            |
| <span data-ttu-id="da8a8-181">장치 삭제</span><span class="sxs-lookup"><span data-stu-id="da8a8-181">Delete device</span></span>                                                                                                                   | <span data-ttu-id="da8a8-182">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-182">Yes</span></span>            |
| <span data-ttu-id="da8a8-183">볼륨 컨테이너 만들기, 수정 및 삭제</span><span class="sxs-lookup"><span data-stu-id="da8a8-183">Create, modify, and delete a volume container</span></span>                                                                                   | <span data-ttu-id="da8a8-184">아니요</span><span class="sxs-lookup"><span data-stu-id="da8a8-184">No</span></span>             |
| <span data-ttu-id="da8a8-185">볼륨 만들기, 수정 및 삭제</span><span class="sxs-lookup"><span data-stu-id="da8a8-185">Create, modify, and delete a volume</span></span>                                                                                             | <span data-ttu-id="da8a8-186">아니요</span><span class="sxs-lookup"><span data-stu-id="da8a8-186">No</span></span>             |
| <span data-ttu-id="da8a8-187">백업 정책 만들기, 수정 및 삭제</span><span class="sxs-lookup"><span data-stu-id="da8a8-187">Create, modify, and delete a backup policy</span></span>                                                                                      | <span data-ttu-id="da8a8-188">아니요</span><span class="sxs-lookup"><span data-stu-id="da8a8-188">No</span></span>             |
| <span data-ttu-id="da8a8-189">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="da8a8-189">Take a manual backup</span></span>                                                                                                            | <span data-ttu-id="da8a8-190">아니요</span><span class="sxs-lookup"><span data-stu-id="da8a8-190">No</span></span>             |
| <span data-ttu-id="da8a8-191">예약된 백업 수행</span><span class="sxs-lookup"><span data-stu-id="da8a8-191">Take a scheduled backup</span></span>                                                                                                         | <span data-ttu-id="da8a8-192">해당 없음</span><span class="sxs-lookup"><span data-stu-id="da8a8-192">Not applicable</span></span> |
| <span data-ttu-id="da8a8-193">backupset에서 복원</span><span class="sxs-lookup"><span data-stu-id="da8a8-193">Restore from a backupset</span></span>                                                                                                        | <span data-ttu-id="da8a8-194">아니요</span><span class="sxs-lookup"><span data-stu-id="da8a8-194">No</span></span>             |
| <span data-ttu-id="da8a8-195">업데이트 3.0 이상을 실행하는 장치에 복제</span><span class="sxs-lookup"><span data-stu-id="da8a8-195">Clone to a device running Update 3.0 and later</span></span> <br> <span data-ttu-id="da8a8-196">원본 장치는 업데이트 3.0 이전 버전을 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-196">The source device is running version prior to Update 3.0.</span></span>                                | <span data-ttu-id="da8a8-197">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-197">Yes</span></span>            |
| <span data-ttu-id="da8a8-198">업데이트 3.0 이전 버전을 실행하는 장치에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-198">Clone to a device running versions prior to Update 3.0</span></span>                                                                          | <span data-ttu-id="da8a8-199">아니요</span><span class="sxs-lookup"><span data-stu-id="da8a8-199">No</span></span>             |
| <span data-ttu-id="da8a8-200">원본 장치로 장애 조치</span><span class="sxs-lookup"><span data-stu-id="da8a8-200">Failover as source device</span></span> <br> <span data-ttu-id="da8a8-201">(업데이트 3.0 이전 버전을 실행하는 장치에서 업데이트 3.0 이후 버전을 실행하는 장치로)</span><span class="sxs-lookup"><span data-stu-id="da8a8-201">(from a device running version prior to Update 3.0 to a device running Update 3.0 and later)</span></span>                                                               | <span data-ttu-id="da8a8-202">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-202">Yes</span></span>            |
| <span data-ttu-id="da8a8-203">대상 장치로 장애 조치</span><span class="sxs-lookup"><span data-stu-id="da8a8-203">Failover as target device</span></span> <br> <span data-ttu-id="da8a8-204">(업데이트 3.0 이전 소프트웨어 버전을 실행하는 장치로)</span><span class="sxs-lookup"><span data-stu-id="da8a8-204">(to a device running software version prior to Update 3.0)</span></span>                                                                                   | <span data-ttu-id="da8a8-205">아니요</span><span class="sxs-lookup"><span data-stu-id="da8a8-205">No</span></span>             |
| <span data-ttu-id="da8a8-206">경고 지우기</span><span class="sxs-lookup"><span data-stu-id="da8a8-206">Clear an alert</span></span>                                                                                                                  | <span data-ttu-id="da8a8-207">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-207">Yes</span></span>            |
| <span data-ttu-id="da8a8-208">클래식 포털에서 생성된 백업 정책, 백업 카탈로그, 볼륨, 볼륨 컨테이너, 모니터링 차트, 작업 및 경고 보기</span><span class="sxs-lookup"><span data-stu-id="da8a8-208">View backup policies, backup catalog, volumes, volume containers, monitoring charts, jobs, and alerts created in classic portal</span></span> | <span data-ttu-id="da8a8-209">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-209">Yes</span></span>            |
| <span data-ttu-id="da8a8-210">장치 컨트롤러 설정 및 해제</span><span class="sxs-lookup"><span data-stu-id="da8a8-210">Turn on and off device controllers</span></span>                                                                                              | <span data-ttu-id="da8a8-211">예</span><span class="sxs-lookup"><span data-stu-id="da8a8-211">Yes</span></span>            |


## <a name="delete-a-service"></a><span data-ttu-id="da8a8-212">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="da8a8-212">Delete a service</span></span>

<span data-ttu-id="da8a8-213">서비스를 삭제하기 전에 사용 중인 연결 장치가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-213">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="da8a8-214">서비스를 사용 중인 경우 연결된 장치를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-214">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="da8a8-215">비활성화 작업은 장치와 서비스 간의 연결을 제공하지만 클라우드의 장치 데이터는 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-215">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da8a8-216">서비스가 삭제된 후에는 작업을 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-216">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="da8a8-217">서비스를 사용하던 모든 장치는 다른 서비스에 사용하기 전에 공장 기본값으로 다시 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-217">Any device that was using the service needs to be reset to factory defaults before it can be used with another service.</span></span> <span data-ttu-id="da8a8-218">이 시나리오에서는 구성뿐 아니라 장치의 로컬 데이터도 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-218">In this scenario, the local data on the device, as well as the configuration, is lost.</span></span>

<span data-ttu-id="da8a8-219">서비스를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-219">Perform the following steps to delete a service.</span></span>

### <a name="to-delete-a-service"></a><span data-ttu-id="da8a8-220">서비스를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="da8a8-220">To delete a service</span></span>

1. <span data-ttu-id="da8a8-221">삭제하려는 서비스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-221">Search for the service you want to delete.</span></span> <span data-ttu-id="da8a8-222">**리소스** 아이콘을 클릭하고 검색하려는 적절한 용어를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-222">Click **Resources** icon and then input the appropriate terms to search.</span></span> <span data-ttu-id="da8a8-223">검색 결과에서 삭제하려는 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-223">In the search results, click the service you want to delete.</span></span>

    ![삭제할 서비스 검색](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. <span data-ttu-id="da8a8-225">그러면 StorSimple 장치 관리자 서비스 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-225">This takes you to the StorSimple Device Manager service blade.</span></span> <span data-ttu-id="da8a8-226">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-226">Click **Delete**.</span></span>

    ![서비스 삭제](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. <span data-ttu-id="da8a8-228">확인 알림에서 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-228">Click **Yes** in the confirmation notification.</span></span> <span data-ttu-id="da8a8-229">서비스 삭제에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-229">It may take a few minutes for the service to be deleted.</span></span>

    ![삭제 확인](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="da8a8-231">서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="da8a8-231">Get the service registration key</span></span>

<span data-ttu-id="da8a8-232">서비스를 성공적으로 만든 후에 서비스에 StorSimple 장치를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-232">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="da8a8-233">처음으로 StorSimple 장치를 등록하려면 서비스 등록 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-233">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="da8a8-234">기존 StorSimple 서비스에 추가 장치를 등록하려면 등록 키와 서비스 데이터 암호화 키(등록 시 첫 번째 장치에서 생성된 키)가 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-234">To register additional devices with an existing StorSimple service, you need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="da8a8-235">서비스 데이터 암호화 키에 대한 자세한 내용은 [StorSimple 보안](storsimple-8000-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da8a8-235">For more information about the service data encryption key, see [StorSimple security](storsimple-8000-security.md).</span></span> <span data-ttu-id="da8a8-236">StorSimple 장치 관리자 블레이드의 **키**에 액세스하여 등록 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-236">You can get the registration key by accessing **Keys** on your StorSimple Device Manager blade.</span></span>

<span data-ttu-id="da8a8-237">서비스 등록 키를 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-237">Perform the following steps to get the service registration key.</span></span>

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

<span data-ttu-id="da8a8-238">서비스 등록 키를 안전한 장소에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-238">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="da8a8-239">이 키와 서비스 데이터 암호화 키는 이 서비스에 추가 장치를 등록할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-239">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="da8a8-240">서비스 등록 키를 가져온 후 StorSimple용 Windows PowerShell 인터페이스를 통해 장치를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-240">After obtaining the service registration key, you must configure your device through the Windows PowerShell for StorSimple interface.</span></span>

<span data-ttu-id="da8a8-241">이 등록 키 사용 방법에 대한 세부 정보는 [3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da8a8-241">For details on how to use this registration key, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="da8a8-242">서비스 등록 키 생성</span><span class="sxs-lookup"><span data-stu-id="da8a8-242">Regenerate the service registration key</span></span>
<span data-ttu-id="da8a8-243">키 회전을 수행해야 하거나 서비스 관리자 목록이 변경된 경우 서비스 등록 키를 다시 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-243">You need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="da8a8-244">키를 다시 생성하면 후속 장치 등록을 위해서만 새 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-244">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="da8a8-245">이미 등록된 장치는 이 과정에 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-245">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="da8a8-246">서비스 등록 키를 다시 생성하려 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-246">Perform the following steps to regenerate a service registration key.</span></span>

### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="da8a8-247">서비스 등록 키를 다시 생성하려면</span><span class="sxs-lookup"><span data-stu-id="da8a8-247">To regenerate the service registration key</span></span>
1. <span data-ttu-id="da8a8-248">**StorSimple Device Manager** 블레이드에서 **관리 &gt;** **키**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-248">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
    
    ![키 블레이드](./media/storsimple-8000-manage-service/regenregkey2.png)

2. <span data-ttu-id="da8a8-250">**키** 블레이드에서 **다시 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-250">In the **Keys** blade, click **Regenerate**.</span></span>

    ![다시 생성 클릭](./media/storsimple-8000-manage-service/regenregkey3.png)
3. <span data-ttu-id="da8a8-252">**서비스 등록 키 다시 생성** 블레이드에서 키를 다시 생성하는 경우에 필요한 작업을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-252">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="da8a8-253">이 서비스에 등록된 모든 후속 장치는 새 등록 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-253">All the subsequent devices that are registered with this service use the new registration key.</span></span> <span data-ttu-id="da8a8-254">**다시 생성**을 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-254">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="da8a8-255">등록이 완료된 후에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-255">You are notified after the regeneration is complete.</span></span>

    ![다시 생성 확인](./media/storsimple-8000-manage-service/regenregkey4.png)

4. <span data-ttu-id="da8a8-257">새 서비스 등록 키가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-257">A new service registration key will appear.</span></span>

5. <span data-ttu-id="da8a8-258">이 서비스에 새 장치 등록을 위해 이 키를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-258">Copy this key and save it for registering any new devices with this service.</span></span>



## <a name="change-the-service-data-encryption-key"></a><span data-ttu-id="da8a8-259">서비스 데이터 암호화 키 변경</span><span class="sxs-lookup"><span data-stu-id="da8a8-259">Change the service data encryption key</span></span>
<span data-ttu-id="da8a8-260">서비스 데이터 암호화 키는 StorSimple 관리자 서비스에서 StorSimple 장치로 전송된 저장소 계정 자격 증명 등의 기밀 고객 데이터를 암호화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-260">Service data encryption keys are used to encrypt confidential customer data, such as storage account credentials, that are sent from your StorSimple Manager service to the StorSimple device.</span></span> <span data-ttu-id="da8a8-261">IT 조직에 저장 장치에 대한 키 회전 정책이 있는 경우는 이러한 키를 주기적으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-261">You will need to change these keys periodically if your IT organization has a key rotation policy on the storage devices.</span></span> <span data-ttu-id="da8a8-262">키 변경 프로세스는 StorSimple 관리자 서비스에서 관리하는 장치가 단일 장치인지, 여러 장치인지에 따라 약간 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-262">The key change process can be slightly different depending on whether there is a single device or multiple devices managed by the StorSimple Manager service.</span></span> <span data-ttu-id="da8a8-263">자세한 내용은 [StorSimple 보안 및 데이터 보호](storsimple-8000-security.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-263">For more information, go to [StorSimple security and data protection](storsimple-8000-security.md).</span></span>

<span data-ttu-id="da8a8-264">서비스 데이터 암호화 키는 3단계 프로세스에 따라 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-264">Changing the service data encryption key is a 3-step process:</span></span>

1. <span data-ttu-id="da8a8-265">Azure Resource Manager에 Windows PowerShell 스크립트를 사용하여 서비스 데이터 암호화 키를 변경하도록 장치에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-265">Using Windows PowerShell scripts for Azure Resource Manager, authorize a device to change the service data encryption key.</span></span>
2. <span data-ttu-id="da8a8-266">StorSimple용 Windows PowerShell을 사용하여 서비스 데이터 암호화 키 변경을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-266">Using Windows PowerShell for StorSimple, initiate the service data encryption key change.</span></span>
3. <span data-ttu-id="da8a8-267">둘 이상의 StorSimple 장치를 사용하는 경우에는 다른 장치에서 서비스 데이터 암호화 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-267">If you have more than one StorSimple device, update the service data encryption key on the other devices.</span></span>

### <a name="step-1-use-windows-powershell-script-to-authorize-a-device-to-change-the-service-data-encryption-key"></a><span data-ttu-id="da8a8-268">1단계: Windows PowerShell 스크립트를 사용하여 장치에 서비스 데이터 암호화 키를 변경할 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-268">Step 1: Use Windows PowerShell script to Authorize a device to change the service data encryption key</span></span>
<span data-ttu-id="da8a8-269">일반적으로 장치 관리자는 서비스 관리자가 장치에 서비스 데이터 암호화 키를 변경할 수 있는 권한을 부여하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-269">Typically, the device administrator will request that the service administrator authorize a device to change service data encryption keys.</span></span> <span data-ttu-id="da8a8-270">그러면 서비스 관리자는 장치에 키를 변경할 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-270">The service administrator will then authorize the device to change the key.</span></span>

<span data-ttu-id="da8a8-271">Azure Resource Manager 기반 스크립트를 사용하여 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-271">This step is performed using the Azure Resource Manager based script.</span></span> <span data-ttu-id="da8a8-272">서비스 관리자는 권한을 부여할 수 있는 장치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-272">The service administrator can select a device that is eligible to be authorized.</span></span> <span data-ttu-id="da8a8-273">그러면 장치에 서비스 데이터 암호화 키 변경 프로세스를 시작할 수 있는 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-273">The device is then authorized to start the service data encryption key change process.</span></span> 

<span data-ttu-id="da8a8-274">스크립트를 사용하는 방법에 대한 자세한 내용은 [Authorize-ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-274">For more information about using the script, go to [Authorize-ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)</span></span>

#### <a name="which-devices-can-be-authorized-to-change-service-data-encryption-keys"></a><span data-ttu-id="da8a8-275">서비스 데이터 암호화 키를 변경할 권한이 부여될 수 있는 장치</span><span class="sxs-lookup"><span data-stu-id="da8a8-275">Which devices can be authorized to change service data encryption keys?</span></span>
<span data-ttu-id="da8a8-276">서비스 데이터 암호화 키 변경을 시작할 권한을 부여받으려면 장치가 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-276">A device must meet the following criteria before it can be authorized to initiate service data encryption key changes:</span></span>

* <span data-ttu-id="da8a8-277">장치는 온라인 상태여야 서비스 데이터 암호화 키 변경 권한 부여 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-277">The device must be online to be eligible for service data encryption key change authorization.</span></span>
* <span data-ttu-id="da8a8-278">키 변경이 시작되지 않은 경우 30분 후에 동일한 장치에 권한을 다시 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-278">You can authorize the same device again after 30 minutes if the key change has not been initiated.</span></span>
* <span data-ttu-id="da8a8-279">이전에 권한을 부여받은 장치에서 키 변경을 시작하지 않은 경우 다른 장치에 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-279">You can authorize a different device, provided that the key change has not been initiated by the previously authorized device.</span></span> <span data-ttu-id="da8a8-280">새 장치에 권한을 부여하면 이전 장치는 변경을 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-280">After the new device has been authorized, the old device cannot initiate the change.</span></span>
* <span data-ttu-id="da8a8-281">서비스 데이터 암호화 키 롤오버가 진행 중인 동안에는 장치에 권한을 부여할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-281">You cannot authorize a device while the rollover of the service data encryption key is in progress.</span></span>
* <span data-ttu-id="da8a8-282">서비스에 등록된 장치 중 일부만 롤오버한 경우에는 장치에 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-282">You can authorize a device when some of the devices registered with the service have rolled over the encryption while others have not.</span></span> 

### <a name="step-2-use-windows-powershell-for-storsimple-to-initiate-the-service-data-encryption-key-change"></a><span data-ttu-id="da8a8-283">2단계: StorSimple용 Windows PowerShell을 사용하여 서비스 데이터 암호화 키 변경 시작</span><span class="sxs-lookup"><span data-stu-id="da8a8-283">Step 2: Use Windows PowerShell for StorSimple to initiate the service data encryption key change</span></span>
<span data-ttu-id="da8a8-284">이 단계는 권한이 부여된 StorSimple 장치의 StorSimple용 Windows PowerShell 인터페이스에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-284">This step is performed in the Windows PowerShell for StorSimple interface on the authorized StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="da8a8-285">키 롤오버가 완료될 때까지 StorSimple Manager 서비스의 Azure Portal에서 수행할 수 있는 작업은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-285">No operations can be performed in the Azure portal of your StorSimple Manager service until the key rollover is completed.</span></span>
> 
> 

<span data-ttu-id="da8a8-286">장치 직렬 콘솔을 사용하여 Windows PowerShell 인터페이스에 연결하는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-286">If you are using the device serial console to connect to the Windows PowerShell interface, perform the following steps.</span></span>

#### <a name="to-initiate-the-service-data-encryption-key-change"></a><span data-ttu-id="da8a8-287">서비스 데이터 암호화 키 변경을 시작하려면</span><span class="sxs-lookup"><span data-stu-id="da8a8-287">To initiate the service data encryption key change</span></span>
1. <span data-ttu-id="da8a8-288">옵션 1을 선택하여 모든 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-288">Select option 1 to log on with full access.</span></span>
2. <span data-ttu-id="da8a8-289">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-289">At the command prompt, type:</span></span>
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. <span data-ttu-id="da8a8-290">cmdlet이 성공적으로 완료되면 새 서비스 데이터 암호화 키를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-290">After the cmdlet has successfully completed, you will get a new service data encryption key.</span></span> <span data-ttu-id="da8a8-291">이 키를 복사하고 저장해 두었다가 이 프로세스의 3단계에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-291">Copy and save this key for use in step 3 of this process.</span></span> <span data-ttu-id="da8a8-292">이 키는 StorSimple 관리자 서비스에 등록된 나머지 모든 장치를 업데이트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-292">This key will be used to update all the remaining devices registered with the StorSimple Manager service.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da8a8-293">이 프로세스는 StorSimple 장치에 권한을 부여한 후 4시간 이내에 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-293">This process must be initiated within four hours of authorizing a StorSimple device.</span></span>
   > 
   > 
   
   <span data-ttu-id="da8a8-294">이 새 키는 서비스로 전송되어 서비스에 등록된 모든 장치에 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-294">This new key is then sent to the service to be pushed to all the devices that are registered with the service.</span></span> <span data-ttu-id="da8a8-295">서비스 대시보드에 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-295">An alert will then appear on the service dashboard.</span></span> <span data-ttu-id="da8a8-296">서비스는 등록된 장치에서 모든 작업을 사용할 수 없도록 설정합니다. 그러면 장치 관리자는 다른 장치에서 서비스 데이터 암호화 키를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-296">The service will disable all the operations on the registered devices, and the device administrator will then need to update the service data encryption key on the other devices.</span></span> <span data-ttu-id="da8a8-297">그러나 I/O(클라우드로 데이터를 보내는 호스트)는 중단되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-297">However, the I/Os (hosts sending data to the cloud) will not be disrupted.</span></span>
   
   <span data-ttu-id="da8a8-298">단일 장치를 서비스에 등록한 경우 이제 롤오버 프로세스가 완료되었으므로 다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-298">If you have a single device registered to your service, the rollover process is now complete and you can skip the next step.</span></span> <span data-ttu-id="da8a8-299">여러 장치를 서비스에 등록한 경우 3단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-299">If you have multiple devices registered to your service, proceed to step 3.</span></span>

### <a name="step-3-update-the-service-data-encryption-key-on-other-storsimple-devices"></a><span data-ttu-id="da8a8-300">3단계: 다른 StorSimple 장치에서 서비스 데이터 암호화 키 업데이트</span><span class="sxs-lookup"><span data-stu-id="da8a8-300">Step 3: Update the service data encryption key on other StorSimple devices</span></span>
<span data-ttu-id="da8a8-301">여러 장치를 StorSimple 관리자 서비스에 등록한 경우 StorSimple 장치의 Windows PowerShell 인터페이스에서 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-301">These steps must be performed in the Windows PowerShell interface of your StorSimple device if you have multiple devices registered to your StorSimple Manager service.</span></span> <span data-ttu-id="da8a8-302">StorSimple Manager 서비스로 등록된 나머지 StorSimple 장치를 업데이트하는 데 2단계에서 가져온 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-302">The key that you obtained in Step 2 must be used to update all the remaining StorSimple device registered with the StorSimple Manager service.</span></span>

<span data-ttu-id="da8a8-303">다음 단계를 수행하여 장치에서 서비스 데이터 암호화를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-303">Perform the following steps to update the service data encryption on your device.</span></span>

#### <a name="to-update-the-service-data-encryption-key"></a><span data-ttu-id="da8a8-304">서비스 데이터 암호화 키를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="da8a8-304">To update the service data encryption key</span></span>
1. <span data-ttu-id="da8a8-305">StorSimple용 Windows PowerShell을 사용하여 콘솔에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-305">Use Windows PowerShell for StorSimple to connect to the console.</span></span> <span data-ttu-id="da8a8-306">옵션 1을 선택하여 모든 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-306">Select option 1 to log on with full access.</span></span>
2. <span data-ttu-id="da8a8-307">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-307">At the command prompt, type:</span></span>
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. <span data-ttu-id="da8a8-308">[2단계: StorSimple용 Windows PowerShell을 사용하여 서비스 데이터 암호화 키 변경 시작](#to-initiate-the-service-data-encryption-key-change)에서 얻은 서비스 데이터 암호화 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-308">Provide the service data encryption key that you obtained in [Step 2: Use Windows PowerShell for StorSimple to initiate the service data encryption key change](#to-initiate-the-service-data-encryption-key-change).</span></span>


## <a name="next-steps"></a><span data-ttu-id="da8a8-309">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da8a8-309">Next steps</span></span>
* <span data-ttu-id="da8a8-310">[StorSimple 배포 프로세스](storsimple-8000-deployment-walkthrough-u2.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-310">Learn more about the [StorSimple deployment process](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="da8a8-311">[StorSimple 저장소 계정 관리](storsimple-8000-manage-storage-accounts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-311">Learn more about [managing your StorSimple storage account](storsimple-8000-manage-storage-accounts.md).</span></span>
* <span data-ttu-id="da8a8-312">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="da8a8-312">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>
