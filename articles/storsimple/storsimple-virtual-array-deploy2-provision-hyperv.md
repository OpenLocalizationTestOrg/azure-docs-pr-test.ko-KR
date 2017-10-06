---
title: "Hyper-v에서 StorSimple 가상 배열 aaaProvision | Microsoft Docs"
description: "StorSimple 가상 배열 배포에 대한 두 번째 자습서에는 Hyper-V에서 가상 배열을 프로비전하는 내용이 포함됩니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="8c170-103">StorSimple 가상 배열 배포 - Hyper-V에서 프로비전</span><span class="sxs-lookup"><span data-stu-id="8c170-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="8c170-104">개요</span><span class="sxs-lookup"><span data-stu-id="8c170-104">Overview</span></span>
<span data-ttu-id="8c170-105">이 자습서 방법을 tooprovision StorSimple 가상은 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2에서 Hyper-v를 실행 중인 호스트 시스템에서을 배열에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-105">This tutorial describes how tooprovision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="8c170-106">이 문서에는 Azure 포털 및 Microsoft Azure Government 클라우드에서 StorSimple 가상 배열 toohello 배포를 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-106">This article applies toohello deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="8c170-107">관리자 권한 tooprovision 필요 하 고이 정보를 가상 배열을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-107">You need administrator privileges tooprovision and configure a virtual array.</span></span> <span data-ttu-id="8c170-108">hello 프로 비전 하 고 초기 설치에는 약 10 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-108">hello provisioning and initial setup can take around 10 minutes toocomplete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="8c170-109">프로비전 필수 조건</span><span class="sxs-lookup"><span data-stu-id="8c170-109">Provisioning prerequisites</span></span>
<span data-ttu-id="8c170-110">있습니다. 필수 구성 요소 tooprovision hello 가상 배열을 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2에서 Hyper-v를 실행 하는 호스트 시스템에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-110">Here you will find hello prerequisites tooprovision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-hello-storsimple-device-manager-service"></a><span data-ttu-id="8c170-111">Hello StorSimple 장치 관리자 서비스에 대 한</span><span class="sxs-lookup"><span data-stu-id="8c170-111">For hello StorSimple Device Manager service</span></span>
<span data-ttu-id="8c170-112">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="8c170-113">모든 hello 단계를 완료 [StorSimple 가상 배열에 대 한 준비 hello 포털](storsimple-virtual-array-deploy1-portal-prep.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-113">You have completed all hello steps in [Prepare hello portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="8c170-114">Hello Azure 포털에서에서 Hyper-v에 대 한 hello 가상 배열 이미지를 다운로드 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-114">You have downloaded hello virtual array image for Hyper-V from hello Azure portal.</span></span> <span data-ttu-id="8c170-115">자세한 내용은 참조 **3 단계: 다운로드 hello 가상 배열 이미지** 의 [StorSimple 가상 배열 가이드에 대 한 준비 hello 포털](storsimple-virtual-array-deploy1-portal-prep.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-115">For more information, see **Step 3: Download hello virtual array image** of [Prepare hello portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8c170-116">hello StorSimple 가상 배열에서 실행 중인 hello 소프트웨어 hello StorSimple 장치 관리자 서비스와만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-116">hello software running on hello StorSimple Virtual Array may only be used with hello StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a><span data-ttu-id="8c170-117">StorSimple 가상 배열 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="8c170-117">For hello StorSimple Virtual Array</span></span>
<span data-ttu-id="8c170-118">가상 배열을 배포하기 전에 다음 사항을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="8c170-119">액세스 tooa 호스트 시스템을 될 사용된 tooa 프로 비전 할 수는 장치 이상 Windows Server 2008 r 2에서 Hyper-v를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-119">You have access tooa host system running Hyper-V on Windows Server 2008 R2 or later that can be used tooa provision a device.</span></span>
* <span data-ttu-id="8c170-120">hello 호스트 시스템은 수 toodedicate 가상 배열 리소스 tooprovision 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="8c170-120">hello host system is able toodedicate hello following resources tooprovision your virtual array:</span></span>

  * <span data-ttu-id="8c170-121">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="8c170-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="8c170-122">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="8c170-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="8c170-123">파일 서버와 tooconfigure hello 가상 배열 하려는 경우 8GB 2 백만 보다 작은 파일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-123">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="8c170-124">16GB RAM toosupport 2-4 백만 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-124">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
  * <span data-ttu-id="8c170-125">네트워크 인터페이스 하나</span><span class="sxs-lookup"><span data-stu-id="8c170-125">One network interface.</span></span>
  * <span data-ttu-id="8c170-126">데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="8c170-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-hello-network-in-hello-datacenter"></a><span data-ttu-id="8c170-127">Hello 네트워크 hello 데이터 센터에 대 한</span><span class="sxs-lookup"><span data-stu-id="8c170-127">For hello network in hello datacenter</span></span>
<span data-ttu-id="8c170-128">시작 하기 전에 네트워킹 요구 사항 toodeploy StorSimple 가상 배열 hello를 검토 하 고 hello 데이터 센터 네트워크를 적절 하 게 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-128">Before you begin, review hello networking requirements toodeploy a StorSimple Virtual Array and configure hello datacenter network appropriately.</span></span> <span data-ttu-id="8c170-129">자세한 내용은 [StorSimple 가상 배열 네트워킹 요구 사항](storsimple-ova-system-requirements.md#networking-requirements)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c170-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="8c170-130">단계별 프로비전</span><span class="sxs-lookup"><span data-stu-id="8c170-130">Step-by-step provisioning</span></span>
<span data-ttu-id="8c170-131">tooprovision tooa 가상 배열 연결 단계를 수행 하는 tooperform hello 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-131">tooprovision and connect tooa virtual array, you need tooperform hello following steps:</span></span>

1. <span data-ttu-id="8c170-132">Hello 호스트 시스템에 충분 한 리소스 toomeet hello 최소 가상 배열 요구 사항에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-132">Ensure that hello host system has sufficient resources toomeet hello minimum virtual array requirements.</span></span>
2. <span data-ttu-id="8c170-133">하이퍼바이저에서 가상 배열을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="8c170-134">Hello 가상 배열을 시작 하 고 hello IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-134">Start hello virtual array and get hello IP address.</span></span>

<span data-ttu-id="8c170-135">이러한 각 단계는 hello 다음 섹션에에서 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-135">Each of these steps is explained in hello following sections.</span></span>

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="8c170-136">1 단계: hello 호스트 시스템이 최소 가상 배열 요구 사항을 충족 하는지 확인</span><span class="sxs-lookup"><span data-stu-id="8c170-136">Step 1: Ensure that hello host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="8c170-137">가상 배열 toocreate 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-137">toocreate a virtual array, you need:</span></span>

* <span data-ttu-id="8c170-138">hello Hyper-v 역할이 Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 s p 1에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-138">hello Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="8c170-139">Microsoft Windows 클라이언트에서 Microsoft Hyper-v 관리자 toohello 호스트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected toohello host.</span></span>

<span data-ttu-id="8c170-140">기반 하드웨어 (호스트 시스템) hello 가상 배열을 만들면 해당 hello 리소스 tooyour 가상 배열 다음 수 toodedicate hello 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-140">Make sure that hello underlying hardware (host system) on which you are creating hello virtual array is able toodedicate hello following resources tooyour virtual array:</span></span>

* <span data-ttu-id="8c170-141">코어 4개 이상</span><span class="sxs-lookup"><span data-stu-id="8c170-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="8c170-142">RAM 8GB 이상</span><span class="sxs-lookup"><span data-stu-id="8c170-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="8c170-143">파일 서버와 tooconfigure hello 가상 배열 하려는 경우 8GB 2 백만 보다 작은 파일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-143">If you plan tooconfigure hello virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="8c170-144">16GB RAM toosupport 2-4 백만 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-144">You need 16 GB RAM toosupport 2 - 4 million files.</span></span>
* <span data-ttu-id="8c170-145">네트워크 인터페이스 하나</span><span class="sxs-lookup"><span data-stu-id="8c170-145">One network interface.</span></span>
* <span data-ttu-id="8c170-146">시스템 데이터용 가상 디스크 500GB</span><span class="sxs-lookup"><span data-stu-id="8c170-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="8c170-147">2단계: 하이퍼바이저에서 가상 배열 프로비전</span><span class="sxs-lookup"><span data-stu-id="8c170-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="8c170-148">Hello 단계 tooprovision 장치 프로그램 하이퍼바이저에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-148">Perform hello following steps tooprovision a device in your hypervisor.</span></span>

#### <a name="tooprovision-a-virtual-array"></a><span data-ttu-id="8c170-149">tooprovision 가상 배열</span><span class="sxs-lookup"><span data-stu-id="8c170-149">tooprovision a virtual array</span></span>
1. <span data-ttu-id="8c170-150">Windows Server 호스트, hello 가상 배열 이미지 tooa 로컬 드라이브를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-150">On your Windows Server host, copy hello virtual array image tooa local drive.</span></span> <span data-ttu-id="8c170-151">Azure 포털 hello를 통해이 이미지 (VHD 또는 VHDX)를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-151">You downloaded this image (VHD or VHDX) through hello Azure portal.</span></span> <span data-ttu-id="8c170-152">이 이미지를 사용 하 여 hello 절차의 뒷부분에 나오는 hello 이미지를 복사 했던 hello 위치를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-152">Make a note of hello location where you copied hello image as you are using this image later in hello procedure.</span></span>
2. <span data-ttu-id="8c170-153">**서버 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-153">Open **Server Manager**.</span></span> <span data-ttu-id="8c170-154">Hello 오른쪽 위의 모서리에서 클릭 **도구** 선택 **Hyper-v 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-154">In hello top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="8c170-155">Windows Server 2008 r 2를 실행 하는 경우에 hello Hyper-v 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-155">If you are running Windows Server 2008 R2, open hello Hyper-V Manager.</span></span> <span data-ttu-id="8c170-156">서버 관리자에서 **역할 > Hyper-V > Hyper-V 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="8c170-157">**Hyper-v 관리자**hello 범위 창에서 마우스 오른쪽 단추로 클릭 하면 시스템 노드 tooopen hello 상황에 맞는 메뉴를 클릭 한 다음 **새로** > **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-157">In **Hyper-V Manager**, in hello scope pane, right-click your system node tooopen hello context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="8c170-158">Hello에 **시작 하기 전에** hello 새 가상 컴퓨터 마법사의 페이지 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-158">On hello **Before you begin** page of hello New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="8c170-159">Hello에 **이름 및 위치 지정** 페이지를 제공는 **이름** 가상 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-159">On hello **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="8c170-160">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-160">Click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="8c170-161">Hello에 **세대 지정** 페이지 hello 장치 이미지 유형을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-161">On hello **Specify generation** page, choose hello device image type, and then click **Next**.</span></span> <span data-ttu-id="8c170-162">Windows Server 2008 R2를 사용하는 경우에는 이 페이지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="8c170-163">Windows Server 2012 이상에 대한 .vhdx 이미지를 다운로드한 경우 **2세대** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="8c170-164">Windows Server 2008 R2 이상에 대한 .vhd 이미지를 다운로드한 경우 **1세대** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="8c170-165">Hello에 **메모리 할당 하 고** 페이지에서 지정는 **시작 메모리** 의 이상 **8192 MB**, 동적 메모리를 사용 하도록 설정 하 고 클릭 하지 않는 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-165">On hello **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="8c170-166">Hello에 **네트워킹 구성** 페이지 hello 된 가상 스위치에 연결 된 toohello 인터넷을 지정 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-166">On hello **Configure networking** page, specify hello virtual switch that is connected toohello Internet and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="8c170-167">Hello에 **가상 하드 디스크 연결** 페이지에서 선택 **기존 가상 하드 디스크를 사용 하 여**hello 가상 배열 이미지 (.vhdx 또는.vhd)의 hello 위치를 지정 하 고 클릭 **다음**.</span><span class="sxs-lookup"><span data-stu-id="8c170-167">On hello **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify hello location of hello virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="8c170-168">검토 hello **요약** 클릭 하 고 **마침** toocreate hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="8c170-168">Review hello **Summary** and then click **Finish** toocreate hello virtual machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="8c170-169">toomeet hello 최소 요구 사항, 코어 4 개 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-169">toomeet hello minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="8c170-170">hello에 호스트 시스템을 선택 하는 4 tooadd 가상 프로세서 **Hyper-v 관리자** 창.</span><span class="sxs-lookup"><span data-stu-id="8c170-170">tooadd 4 virtual processors, select your host system in hello **Hyper-V Manager** window.</span></span> <span data-ttu-id="8c170-171">Hello 목록은 아래 hello 오른쪽 창에서 **가상 컴퓨터**, 방금 만든 hello 가상 컴퓨터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-171">In hello right-pane under hello list of **Virtual Machines**, locate hello virtual machine you just created.</span></span> <span data-ttu-id="8c170-172">선택 하 고 hello 컴퓨터 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-172">Select and right-click hello machine name and select **Settings**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="8c170-173">Hello에 **설정** 페이지 hello 왼쪽 창에서 클릭 **프로세서**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-173">On hello **Settings** page, in hello left-pane, click **Processor**.</span></span> <span data-ttu-id="8c170-174">Hello 오른쪽 창에서 설정 **가상 프로세서 수가** too4 (이상).</span><span class="sxs-lookup"><span data-stu-id="8c170-174">In hello right-pane, set **number of virtual processors** too4 (or more).</span></span> <span data-ttu-id="8c170-175">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-175">Click **Apply**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="8c170-176">toomeet hello 최소 요구 사항, 있어야 tooadd 500GB 가상 데이터 디스크 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-176">toomeet hello minimum requirements, you also need tooadd a 500 GB virtual data disk.</span></span> <span data-ttu-id="8c170-177">Hello에 **설정을** 페이지:</span><span class="sxs-lookup"><span data-stu-id="8c170-177">In hello **Settings** page:</span></span>

    1. <span data-ttu-id="8c170-178">Hello 왼쪽된 창에서 선택 **SCSI 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-178">In hello left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="8c170-179">Hello 오른쪽 창에서 선택 **하드 드라이브** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-179">In hello right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="8c170-180">Hello에 **하드 드라이브** 페이지, 선택 hello **가상 하드 디스크** 옵션 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-180">On hello **Hard drive** page, select hello **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="8c170-181">hello **새 가상 하드 디스크 마법사** 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-181">hello **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="8c170-182">Hello에 **시작 하기 전에** hello 새 가상 하드 디스크 마법사의 페이지 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-182">On hello **Before you begin** page of hello New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="8c170-183">Hello에 **디스크 형식 선택 페이지**, hello 기본 옵션의 그대로 **VHDX** 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-183">On hello **Choose Disk Format page**, accept hello default option of **VHDX** format.</span></span> <span data-ttu-id="8c170-184">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-184">Click **Next**.</span></span> <span data-ttu-id="8c170-185">Windows Server 2008 R2를 실행하는 경우에는 이 화면이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="8c170-186">Hello에 **디스크 유형 선택 페이지**, 가상 하드 디스크 유형으로 설정 **동적 확장** (권장).</span><span class="sxs-lookup"><span data-stu-id="8c170-186">On hello **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="8c170-187">**고정 크기** 디스크 작동할 것 이지만 오랫동안 toowait를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-187">**Fixed size** disk would work but you may need toowait a long time.</span></span> <span data-ttu-id="8c170-188">Hello를 사용 하지 않는 것이 좋습니다 **차이점 보관용** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-188">We recommend that you do not use hello **Differencing** option.</span></span> <span data-ttu-id="8c170-189">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-189">Click **Next**.</span></span> <span data-ttu-id="8c170-190">Windows Server 2012 R2 및 Windows Server 2012에서 **동적 확장** hello 기본값은 Windows Server 2008 R2 반면 hello 기본 옵션은 **고정 크기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is hello default option whereas in Windows Server 2008 R2, hello default is **Fixed size**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="8c170-191">Hello에 **이름 및 위치 지정** 페이지를 제공는 **이름** 으로 **위치** (tooone 찾아볼 수 있습니다) hello 데이터 디스크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-191">On hello **Specify Name and Location** page, provide a **name** as well as **location** (you can browse tooone) for hello data disk.</span></span> <span data-ttu-id="8c170-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-192">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="8c170-193">Hello에 **디스크 구성** 선택 hello 옵션 페이지 **비어 있는 새 가상 하드 디스크를 만들** 으로 hello 크기를 지정 하 고 **500GB** (이상).</span><span class="sxs-lookup"><span data-stu-id="8c170-193">On hello **Configure Disk** page, select hello option **Create a new blank virtual hard disk** and specify hello size as **500 GB** (or more).</span></span> <span data-ttu-id="8c170-194">500GB hello 최소 요구 사항을 상태인 동안 항상 가장 큰 디스크를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-194">While 500 GB is hello minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="8c170-195">참고 확장 하거나 프로 비전 한 번 hello 디스크를 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-195">Note that you cannot expand or shrink hello disk once provisioned.</span></span> <span data-ttu-id="8c170-196">디스크 tooprovision hello 크기에 자세한 내용은 hello hello 크기 조정 섹션을 검토 [모범 사례 문서](storsimple-ova-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-196">For more information on hello size of disk tooprovision, review hello sizing section in hello [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="8c170-197">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-197">Click **Next**.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="8c170-198">Hello에 **요약** 페이지 가상 데이터 디스크의 hello 세부 정보를 검토 하 고 충족 클릭 **마침** toocreate hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="8c170-198">On hello **Summary** page, review hello details of your virtual data disk and if satisfied, click **Finish** toocreate hello disk.</span></span> <span data-ttu-id="8c170-199">hello 마법사가 닫히고 가상 하드 디스크 tooyour 컴퓨터에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-199">hello wizard closes and a virtual hard disk is added tooyour machine.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="8c170-200">Toohello 반환 **설정을** 페이지.</span><span class="sxs-lookup"><span data-stu-id="8c170-200">Return toohello **Settings** page.</span></span> <span data-ttu-id="8c170-201">클릭 **확인** tooclose hello **설정** 페이지 및 tooHyper V 관리자 창을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-201">Click **OK** tooclose hello **Settings** page and return tooHyper-V Manager window.</span></span>

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a><span data-ttu-id="8c170-202">3 단계: 가상 배열 hello를 시작 하 고 hello IP 가져오기</span><span class="sxs-lookup"><span data-stu-id="8c170-202">Step 3: Start hello virtual array and get hello IP</span></span>
<span data-ttu-id="8c170-203">가상 배열 hello 단계 toostart 다음을 수행 하 고 tooit를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-203">Perform hello following steps toostart your virtual array and connect tooit.</span></span>

#### <a name="toostart-hello-virtual-array"></a><span data-ttu-id="8c170-204">toostart hello 가상 배열</span><span class="sxs-lookup"><span data-stu-id="8c170-204">toostart hello virtual array</span></span>
1. <span data-ttu-id="8c170-205">Hello 가상 배열을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-205">Start hello virtual array.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="8c170-206">Hello 장치가 실행 되 고 후 hello 장치를 선택, 마우스 오른쪽 단추로 클릭 하 고 선택 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-206">After hello device is running, select hello device, right click, and select **Connect**.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="8c170-207">Hello 장치 toobe 준비에 대 한 5-10 분 toowait를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-207">You may have toowait 5-10 minutes for hello device toobe ready.</span></span> <span data-ttu-id="8c170-208">Hello 콘솔 tooindicate hello 진행률에 대 한 상태 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-208">A status message is displayed on hello console tooindicate hello progress.</span></span> <span data-ttu-id="8c170-209">Hello 장치 준비 되 면 너무 이동**동작**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-209">After hello device is ready, go too**Action**.</span></span> <span data-ttu-id="8c170-210">키를 눌러 `Ctrl + Alt + Delete` toolog toohello 가상 배열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-210">Press `Ctrl + Alt + Delete` toolog in toohello virtual array.</span></span> <span data-ttu-id="8c170-211">hello 기본 사용자가 *StorSimpleAdmin* hello 기본 암호는 및 *Password1*합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-211">hello default user is *StorSimpleAdmin* and hello default password is *Password1*.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="8c170-212">보안상의 이유로 hello 처음 로그온 할 때 hello 장치 관리자 암호가 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-212">For security reasons, hello device administrator password expires at hello first logon.</span></span> <span data-ttu-id="8c170-213">입력 정보 요청된 toochange hello 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-213">You are prompted toochange hello password.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="8c170-214">8자 이상을 포함하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="8c170-215">hello 암호 충족 해야 4 요구 사항을 준수 하는 hello 부족 3 이상을: 대문자, 소문자, 숫자 및 특수 문자.</span><span class="sxs-lookup"><span data-stu-id="8c170-215">hello password must satisfy at least 3 out of hello following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="8c170-216">Hello 암호 tooconfirm 다시 입력 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-216">Reenter hello password tooconfirm it.</span></span> <span data-ttu-id="8c170-217">해당 hello 암호가 변경 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-217">You are notified that hello password has changed.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="8c170-218">Hello 암호를 성공적으로 변경 후 hello 가상 배열 다시 시작 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-218">After hello password is successfully changed, hello virtual array may restart.</span></span> <span data-ttu-id="8c170-219">Hello 장치 toostart 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-219">Wait for hello device toostart.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="8c170-220">hello 장치의 Windows PowerShell 콘솔 hello 진행률 표시줄을 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-220">hello Windows PowerShell console of hello device is displayed along with a progress bar.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="8c170-221">6-8단계는 DHCP 환경이 아닌 곳에서 부팅하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="8c170-222">DHCP 환경에 있는 다음 이러한 단계를 생략 하 고 toostep 9를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-222">If you are in a DHCP environment, then skip these steps and go toostep 9.</span></span> <span data-ttu-id="8c170-223">비 DHCP 환경에서 장치를 부팅 하는 경우 다음 화면 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-223">If you booted up your device in non-DHCP environment, you will see hello following screen.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="8c170-224">다음으로 hello 네트워크를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-224">Next, configure hello network.</span></span>
7. <span data-ttu-id="8c170-225">사용 하 여 hello `Get-HcsIpAddress` 명령 toolist hello 네트워크 인터페이스가 가상 배열에서 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-225">Use hello `Get-HcsIpAddress` command toolist hello network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="8c170-226">장치에 사용 하도록 설정 하는 단일 네트워크 인터페이스, hello 기본 이름이 할당 toothis 인터페이스 인지 `Ethernet`합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-226">If your device has a single network interface enabled, hello default name assigned toothis interface is `Ethernet`.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="8c170-227">사용 하 여 hello `Set-HcsIpAddress` cmdlet tooconfigure hello 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-227">Use hello `Set-HcsIpAddress` cmdlet tooconfigure hello network.</span></span> <span data-ttu-id="8c170-228">다음 예제는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8c170-228">See hello following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="8c170-229">Hello 초기 설치가 완료 된 후 hello 장치에 부팅 hello 장치 배너 텍스트를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-229">After hello initial setup is complete and hello device has booted up, you will see hello device banner text.</span></span> <span data-ttu-id="8c170-230">Hello IP 주소와 hello 배너 텍스트 toomanage hello 장치에 표시 된 hello URL의 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-230">Make a note of hello IP address and hello URL displayed in hello banner text toomanage hello device.</span></span> <span data-ttu-id="8c170-231">이 IP 주소 tooconnect toohello 웹 가상 배열 및 hello 전체 로컬 설치 및 등록의 UI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-231">Use this IP address tooconnect toohello web UI of your virtual array and complete hello local setup and registration.</span></span>

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="8c170-232">(선택 사항) 정부 클라우드 hello에 장치를 배포 하는 경우에이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-232">(Optional) Perform this step only if you are deploying your device in hello Government Cloud.</span></span> <span data-ttu-id="8c170-233">장치에서 이제 hello 미국 연방 정보 FIPS (Processing Standard) 모드를 하면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-233">You will now enable hello United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="8c170-234">hello FIPS 140 표준은 hello 중요 한 데이터 보호를 위해 미국 연방 정부 컴퓨터 시스템에서 사용할 수 있도록 승인 하는 암호화 알고리즘을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-234">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span>

    1. <span data-ttu-id="8c170-235">tooenable hello FIPS 모드에서는 hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-235">tooenable hello FIPS mode, run hello following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="8c170-236">암호화 유효성 검사 hello 내용이 적용 되도록 hello FIPS 모드를 활성화 한 후에 장치를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-236">Reboot your device after you have enabled hello FIPS mode so that hello cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="8c170-237">장치에서 FIPS 모드를 사용 또는 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="8c170-238">FIPS 및 비 FIPS 모드 사이 교대로 반복 되 hello 장치가 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-238">Alternating hello device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="8c170-239">장치 hello 최소 구성 요구를 충족 하지 않으면 hello hello 배너 텍스트 (아래 참조)의 오류 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-239">If your device does not meet hello minimum configuration requirements, you see hello following error in hello banner text (shown below).</span></span> <span data-ttu-id="8c170-240">Hello 컴퓨터에 적절 한 리소스 toomeet 최소 요구 사항을 hello hello 장치 구성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-240">Modify hello device configuration so that hello machine has adequate resources toomeet hello minimum requirements.</span></span> <span data-ttu-id="8c170-241">그런 다음 다시 시작 하 고 toohello 장치를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-241">You can then restart and connect toohello device.</span></span> <span data-ttu-id="8c170-242">toohello 최소 구성 요구 사항을 참조 [1 단계: hello 호스트 시스템이 최소 가상 배열 요구 사항을 충족 하는지 확인](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-242">Refer toohello minimum configuration requirements in [Step 1: Ensure that hello host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="8c170-243">Hello 로컬 웹 UI를 사용 하 여 hello 초기 구성 중 다른 오류가 발생 하면 다음 워크플로가 toohello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8c170-243">If you face any other error during hello initial configuration using hello local web UI, refer toohello following workflows:</span></span>

* <span data-ttu-id="8c170-244">진단 테스트를 너무 실행[웹 UI 설정 문제 해결](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c170-244">Run diagnostic tests too[troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="8c170-245">[로그 패키지를 생성하고 로그 파일을 살펴봅니다](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="8c170-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c170-246">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c170-246">Next steps</span></span>
* [<span data-ttu-id="8c170-247">StorSimple 가상 배열을 파일 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="8c170-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="8c170-248">StorSimple 가상 배열을 iSCSI 서버로 설정</span><span class="sxs-lookup"><span data-stu-id="8c170-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)
