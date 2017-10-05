---
title: "StorSimple Manager 서비스 배포 | Microsoft Docs"
description: "Azure 클래식 포털에서 StorSimple 관리자 서비스를 만들고 삭제하는 방법 및 서비스 등록 키를 관리하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ba3637a3a8b15b45c16bf5a00c1f4225bcfc5af8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-the-storsimple-manager-service-in-the-azure-classic-portal"></a><span data-ttu-id="b43a2-103">Azure 클래식 포털에서 StorSimple Manager 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="b43a2-103">Deploy the StorSimple Manager service in the Azure classic portal</span></span>

## <a name="overview"></a><span data-ttu-id="b43a2-104">개요</span><span class="sxs-lookup"><span data-stu-id="b43a2-104">Overview</span></span>
<span data-ttu-id="b43a2-105">StorSimple 관리자 서비스는 Microsoft Azure에서 실행되며 여러 StorSimple 장치에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-105">The StorSimple Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="b43a2-106">서비스를 만든 후에 브라우저에서 실행되는 Microsoft Azure 클래식 포털에서 이러한 장치를 관리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-106">After you create the service, you can use it to manage the devices from the Microsoft Azure classic portal running in a browser.</span></span> <span data-ttu-id="b43a2-107">하나의 중앙 위치에서 StorSimple 관리자 서비스에 연결된 모든 장치를 모닝터링하여 관리 부담을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-107">This allows you to monitor all the devices that are connected to the StorSimple Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="b43a2-108">StorSimple 관리자 방문 페이지에는 StorSimple 저장소 장치를 관리하는 데 사용할 수 있는 모든 StorSimple 관리자 서비스가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-108">The StorSimple Manager landing page lists all the StorSimple Manager services that you can use to manage your StorSimple storage devices.</span></span> <span data-ttu-id="b43a2-109">각 StorSimple 관리자 서비스의 경우, 다음 정보가 StorSimple 관리자 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-109">For each StorSimple Manager service, the following information is presented on the StorSimple Manager page:</span></span>

* <span data-ttu-id="b43a2-110">**이름** – 만들었을 때 StorSimple 관리자 서비스에 할당된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-110">**Name** – The name that was assigned to your StorSimple Manager service when it was created.</span></span> <span data-ttu-id="b43a2-111">**서비스 이름은 서비스를 만든 후에 변경할 수 없습니다. Azure 클래식 포털에서 이름을 바꿀 수 없는 장치, 볼륨, 볼륨 컨테이너 및 백업 정책 같은 기타 엔터티에도 마찬가지입니다.**</span><span class="sxs-lookup"><span data-stu-id="b43a2-111">**The service name cannot be changed after the service is created. This is also true for other entities such as devices, volumes, volume containers, and backup policies that cannot be renamed in the Azure classic portal.**</span></span>
* <span data-ttu-id="b43a2-112">**상태** – **활성**, **만들기** 또는 **온라인** 등의 서비스 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-112">**Status** – The status of the service, which can be **Active**, **Creating**, or **Online**.</span></span>
* <span data-ttu-id="b43a2-113">**위치** – StorSimple 장치를 배포할 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-113">**Location** – The geographical location in which the StorSimple device will be deployed.</span></span>
* <span data-ttu-id="b43a2-114">**구독** – 서비스와 연관된 청구 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-114">**Subscription** – The billing subscription that is associated with your service.</span></span>

<span data-ttu-id="b43a2-115">StorSimple 관리자 페이지를 통해 수행할 수 있는 일반적인 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-115">The common tasks that can be performed through the StorSimple Manager page are:</span></span>

* <span data-ttu-id="b43a2-116">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="b43a2-116">Create a service</span></span>
* <span data-ttu-id="b43a2-117">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="b43a2-117">Delete a service</span></span>
* <span data-ttu-id="b43a2-118">서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="b43a2-118">Get the service registration key</span></span>
* <span data-ttu-id="b43a2-119">서비스 등록 키 생성</span><span class="sxs-lookup"><span data-stu-id="b43a2-119">Regenerate the service registration key</span></span>

<span data-ttu-id="b43a2-120">이 자습서에서는 이러한 각 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-120">This tutorial describes how to perform each of these tasks.</span></span>

## <a name="create-a-service"></a><span data-ttu-id="b43a2-121">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="b43a2-121">Create a service</span></span>
<span data-ttu-id="b43a2-122">StorSimple 장치를 배포하려는 경우 **빠른 생성** 옵션을 사용하여 StorSimple 관리자 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-122">Use the **Quick Create** option to create a StorSimple Manager service if you want to deploy your StorSimple device.</span></span> <span data-ttu-id="b43a2-123">서비스를 만들려면:</span><span class="sxs-lookup"><span data-stu-id="b43a2-123">To create a service, you need to have:</span></span>

* <span data-ttu-id="b43a2-124">엔터프라이즈 계약을 사용하여 구독</span><span class="sxs-lookup"><span data-stu-id="b43a2-124">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="b43a2-125">활성 Microsoft Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="b43a2-125">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="b43a2-126">액세스 관리에 사용되는 청구 정보</span><span class="sxs-lookup"><span data-stu-id="b43a2-126">The billing information that is used for access management</span></span>

<span data-ttu-id="b43a2-127">또한 서비스를 만들 때 기본 저장소 계정을 생성하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-127">You can also choose to generate a default storage account when you create the service.</span></span>

<span data-ttu-id="b43a2-128">하나의 서비스로 여러 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-128">A single service can manage multiple devices.</span></span> <span data-ttu-id="b43a2-129">하지만 하나의 장치는 여러 서비스로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-129">However, a device cannot span multiple services.</span></span> <span data-ttu-id="b43a2-130">대규모 엔터프라이즈는 서로 다른 구독, 조직 또는 배포 위치와 동작하는 여러 서비스 인스턴스를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-130">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span> <span data-ttu-id="b43a2-131">StorSimple 8000 시리즈 장치와 StorSimple 가상 배열을 관리하려면 별도의 StorSimple Manager 서비스 인스턴스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-131">Please note that you need separate instances of StorSimple Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b43a2-132">2016년 8월 전에 만든 사용하지 않는 서비스(이 리소스에 대해 수행된 장치 작업이 없음)가 있는 경우, Azure Portal이나 Azure 클래식 포털을 통해 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-132">If you have an unused service created (no device operations were performed on this resource) prior to August 2016, it cannot be managed via Azure portal or Azure classic portal.</span></span> <span data-ttu-id="b43a2-133">Azure Portal에 새 서비스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-133">We recommend that you create a new service in the Azure portal.</span></span>

<span data-ttu-id="b43a2-134">서비스를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-134">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="b43a2-135">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="b43a2-135">Delete a service</span></span>
<span data-ttu-id="b43a2-136">서비스를 삭제하기 전에 사용 중인 연결 장치가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-136">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="b43a2-137">서비스를 사용 중인 경우 연결된 장치를 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-137">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="b43a2-138">비활성화 작업은 장치와 서비스 간의 연결을 제공하지만 클라우드의 장치 데이터는 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-138">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b43a2-139">서비스가 삭제된 후에는 작업을 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-139">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="b43a2-140">서비스를 사용하던 모든 장치는 다른 서비스에 사용하기 전에 공장 기본 설정을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-140">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="b43a2-141">이 시나리오에서는 구성뿐 아니라 장치의 로컬 데이터도 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-141">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>

<span data-ttu-id="b43a2-142">서비스를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-142">Perform the following steps to delete a service.</span></span>

### <a name="to-delete-a-service"></a><span data-ttu-id="b43a2-143">서비스를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="b43a2-143">To delete a service</span></span>
1. <span data-ttu-id="b43a2-144">**StorSimple 관리자 서비스** 페이지에서 삭제하려는 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-144">On the **StorSimple Manager service** page, select the service that you wish to delete.</span></span>
2. <span data-ttu-id="b43a2-145">페이지 맨 아래에서 **삭제** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-145">Click **Delete** at the bottom of the page.</span></span>
3. <span data-ttu-id="b43a2-146">확인 알림에서 **예** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-146">Click **Yes** in the confirmation notification.</span></span> <span data-ttu-id="b43a2-147">서비스 삭제에는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-147">It may take a few minutes for the service to be deleted.</span></span>

## <a name="get-the-service-registration-key"></a><span data-ttu-id="b43a2-148">서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="b43a2-148">Get the service registration key</span></span>
<span data-ttu-id="b43a2-149">서비스를 성공적으로 만든 후에 서비스에 StorSimple 장치를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-149">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="b43a2-150">처음으로 StorSimple 장치를 등록하려면 서비스 등록 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-150">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="b43a2-151">기존 StorSimple 서비스에 추가 장치를 등록하려면 등록 키와 서비스 데이터 암호화 키(등록 시 첫 번째 장치에서 생성된 키)가 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-151">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="b43a2-152">서비스 데이터 암호화 키에 대한 자세한 내용은 [StorSimple 보안](storsimple-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b43a2-152">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="b43a2-153">**등록 키** on the **등록 키** 에 액세스하여 등록 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-153">You can get the registration key by accessing **Registration Key** on the **Services** page.</span></span>

<span data-ttu-id="b43a2-154">서비스 등록 키를 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-154">Perform the following steps to get the service registration key.</span></span>

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

<span data-ttu-id="b43a2-155">서비스 등록 키를 안전한 장소에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-155">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="b43a2-156">이 키와 서비스 데이터 암호화 키는 이 서비스에 추가 장치를 등록할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-156">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="b43a2-157">서비스 등록 키를 가져온 후 StorSimple 인터페이스용 Windows PowerShell을 통해 장치를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-157">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

<span data-ttu-id="b43a2-158">이 등록 키 사용 방법에 대한 세부 정보는 [3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b43a2-158">For details on how to use this registration key, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="b43a2-159">서비스 등록 키 생성</span><span class="sxs-lookup"><span data-stu-id="b43a2-159">Regenerate the service registration key</span></span>
<span data-ttu-id="b43a2-160">키 회전을 수행해야 하거나 서비스 관리자 목록이 변경된 경우 서비스 등록 키를 다시 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-160">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="b43a2-161">키를 다시 생성하면 후속 장치 등록을 위해서만 새 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-161">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="b43a2-162">이미 등록된 장치는 이 과정에 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-162">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="b43a2-163">서비스 등록 키를 다시 생성하려 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-163">Perform the following steps to regenerate a service registration key.</span></span>

### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="b43a2-164">서비스 등록 키를 다시 생성하려면</span><span class="sxs-lookup"><span data-stu-id="b43a2-164">To regenerate the service registration key</span></span>
1. <span data-ttu-id="b43a2-165">**StorSimple Manager 서비스** 페이지에서 **등록 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-165">On the **StorSimple Manager service** page, click **Registration Key**.</span></span>
2. <span data-ttu-id="b43a2-166">**서비스 등록 키** 대화 상자에서 **다시 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-166">In the **Service Registration Key** dialog box, click **Regenerate**.</span></span>
3. <span data-ttu-id="b43a2-167">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-167">You will see a confirmation message.</span></span> <span data-ttu-id="b43a2-168">**확인** 을 클릭하여 등록을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-168">Click **OK** to continue with the regeneration.</span></span>
4. <span data-ttu-id="b43a2-169">새 서비스 등록 키가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-169">A new service registration key will appear.</span></span>
5. <span data-ttu-id="b43a2-170">이 서비스에 새 장치 등록을 위해 이 키를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-170">Copy this key and save it for registering any new devices with this service.</span></span>
6. <span data-ttu-id="b43a2-171">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="b43a2-171">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-manage-service/HCS_CheckIcon.png) <span data-ttu-id="b43a2-173">을 클릭하고 이 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-173">to close this dialog box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b43a2-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b43a2-174">Next steps</span></span>
* <span data-ttu-id="b43a2-175">[StorSimple 배포 프로세스](storsimple-deployment-walkthrough-u2.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-175">Learn more about the [StorSimple deployment process](storsimple-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="b43a2-176">[StorSimple 저장소 계정 관리](storsimple-manage-storage-accounts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-176">Learn more about [managing your StorSimple storage account](storsimple-manage-storage-accounts.md).</span></span>
* <span data-ttu-id="b43a2-177">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b43a2-177">Learn more about how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>
