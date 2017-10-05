---
title: "StorSimple 장치 관리자 서비스 배포 | Microsoft Docs"
description: "Azure Portal에서 StorSimple Device Manager 서비스를 만들고 삭제하는 방법 및 서비스 등록 키를 관리하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="fd671-103">StorSimple 가상 배열에 StorSimple Device Manager 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="fd671-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="fd671-104">개요</span><span class="sxs-lookup"><span data-stu-id="fd671-104">Overview</span></span>

<span data-ttu-id="fd671-105">StorSimple Device Manager 서비스는 Microsoft Azure에서 실행되며 여러 StorSimple 장치에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="fd671-106">서비스를 만든 후에 브라우저에서 실행되는 Microsoft Azure 포털에서 이러한 장치를 관리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="fd671-107">하나의 중앙 위치에서 StorSimple Device Manager 서비스에 연결된 모든 장치를 모닝터링하여 관리 부담을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="fd671-108">StorSimple Device Manager 서비스와 관련된 일반적인 태스크는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="fd671-109">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="fd671-109">Create a service</span></span>
* <span data-ttu-id="fd671-110">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="fd671-110">Delete a service</span></span>
* <span data-ttu-id="fd671-111">서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="fd671-111">Get the service registration key</span></span>
* <span data-ttu-id="fd671-112">서비스 등록 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="fd671-112">Regenerate the service registration key</span></span>

<span data-ttu-id="fd671-113">이 자습서에서는 이러한 태스크를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="fd671-114">이 문서에 포함된 정보는 StorSimple 가상 배열에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="fd671-115">StorSimple 8000 시리즈에 대한 자세한 내용은 [StorSimple Manager 서비스 배포](storsimple-manage-service.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd671-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="fd671-116">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="fd671-116">Create a service</span></span>

<span data-ttu-id="fd671-117">서비스를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="fd671-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="fd671-118">엔터프라이즈 계약을 사용하여 구독</span><span class="sxs-lookup"><span data-stu-id="fd671-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="fd671-119">활성 Microsoft Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="fd671-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="fd671-120">액세스 관리에 사용되는 청구 정보</span><span class="sxs-lookup"><span data-stu-id="fd671-120">The billing information that is used for access management</span></span>

<span data-ttu-id="fd671-121">또한 서비스를 만들 때 저장소 계정을 생성하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="fd671-122">하나의 서비스로 여러 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="fd671-123">하지만 하나의 장치는 여러 서비스로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="fd671-124">대규모 엔터프라이즈는 서로 다른 구독, 조직 또는 배포 위치와 동작하는 여러 서비스 인스턴스를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="fd671-125">StorSimple 8000 시리즈 장치와 StorSimple 가상 배열을 관리하려면 별도의 StorSimple Device Manager 서비스 인스턴스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="fd671-126">서비스를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="fd671-127">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="fd671-127">Delete a service</span></span>

<span data-ttu-id="fd671-128">서비스를 삭제하기 전에 사용 중인 연결 장치가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="fd671-129">서비스를 사용 중인 경우 연결된 장치를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="fd671-130">비활성화 작업은 장치와 서비스 간의 연결을 제공하지만 클라우드의 장치 데이터는 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd671-131">서비스가 삭제된 후에는 작업을 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="fd671-132">서비스를 사용하던 모든 장치는 다른 서비스에 사용하기 전에 공장 기본 설정을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="fd671-133">이 시나리오에서는 구성뿐 아니라 장치의 로컬 데이터도 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="fd671-134">서비스를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="fd671-135">서비스를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="fd671-135">To delete a service</span></span>

1. <span data-ttu-id="fd671-136">**모든 리소스**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-136">Go to **All resources**.</span></span> <span data-ttu-id="fd671-137">StorSimple Device Manager 서비스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="fd671-138">삭제하려는 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-138">Select the service that you wish to delete.</span></span>
   
    ![삭제할 서비스 선택](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="fd671-140">서비스 대시보드로 이동하여 서비스에 연결된 장치가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="fd671-141">이 서비스에 등록된 장치가 없는 경우 효과에 대한 배너 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="fd671-142">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-142">Click **Delete**.</span></span>
   
    ![서비스 삭제](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="fd671-144">확인 메시지가 나타나면 확인 알림에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![서비스 삭제 확인](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="fd671-146">서비스 삭제에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="fd671-147">서비스가 성공적으로 삭제된 후에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![성공적인 서비스 삭제](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="fd671-149">서비스 목록이 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-149">The list of services will be refreshed.</span></span>

 ![업데이트된 서비스 목록](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="fd671-151">서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="fd671-151">Get the service registration key</span></span>
<span data-ttu-id="fd671-152">서비스를 성공적으로 만든 후에 서비스에 StorSimple 장치를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="fd671-153">처음으로 StorSimple 장치를 등록하려면 서비스 등록 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="fd671-154">기존 StorSimple 서비스에 추가 장치를 등록하려면 등록 키와 서비스 데이터 암호화 키(등록 시 첫 번째 장치에서 생성된 키)가 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="fd671-155">서비스 데이터 암호화 키에 대한 자세한 내용은 [StorSimple 보안](storsimple-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fd671-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="fd671-156">서비스에 대한 **키** 블레이드에 액세스하여 등록 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="fd671-157">서비스 등록 키를 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="fd671-158">서비스 등록 키를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="fd671-158">To get the service registration key</span></span>
1. <span data-ttu-id="fd671-159">**StorSimple Device Manager** 블레이드에서 **관리 &gt;** **키**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![키 블레이드](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="fd671-161">**키** 블레이드에서 서비스 등록 키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="fd671-162">복사 아이콘을 사용하여 등록 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="fd671-163">서비스 등록 키를 안전한 장소에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="fd671-164">이 키와 서비스 데이터 암호화 키는 이 서비스에 추가 장치를 등록할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="fd671-165">서비스 등록 키를 가져온 후 StorSimple 인터페이스용 Windows PowerShell을 통해 장치를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="fd671-166">서비스 등록 키 생성</span><span class="sxs-lookup"><span data-stu-id="fd671-166">Regenerate the service registration key</span></span>
<span data-ttu-id="fd671-167">키 회전을 수행해야 하거나 서비스 관리자 목록이 변경된 경우 서비스 등록 키를 다시 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="fd671-168">키를 다시 생성하면 후속 장치 등록을 위해서만 새 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="fd671-169">이미 등록된 장치는 이 과정에 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="fd671-170">서비스 등록 키를 다시 생성하려 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="fd671-171">서비스 등록 키를 다시 생성하려면</span><span class="sxs-lookup"><span data-stu-id="fd671-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="fd671-172">**StorSimple Device Manager** 블레이드에서 **관리 &gt;** **키**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![키 블레이드](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="fd671-174">**키** 블레이드에서 **다시 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![다시 생성 클릭](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="fd671-176">**서비스 등록 키 다시 생성** 블레이드에서 키를 다시 생성하는 경우에 필요한 작업을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="fd671-177">이 서비스에 등록된 모든 후속 장치는 새 등록 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="fd671-178">**다시 생성**을 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="fd671-179">등록이 완료된 후에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-179">You will be notified after the registration is complete.</span></span>
   
   ![다시 생성 키 확인](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="fd671-181">새 서비스 등록 키가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-181">A new service registration key will appear.</span></span>
   
    ![다시 생성 키 확인](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="fd671-183">이 서비스에 새 장치 등록을 위해 이 키를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd671-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd671-184">Next steps</span></span>
* <span data-ttu-id="fd671-185">StorSimple 가상 배열 [시작](storsimple-virtual-array-deploy1-portal-prep.md) 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="fd671-186">[StorSimple 장치 관리](storsimple-ova-web-ui-admin.md)방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fd671-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

