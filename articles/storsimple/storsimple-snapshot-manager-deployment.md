---
title: "StorSimple Snapshot Manager 배포 | Microsoft Docs"
description: "StorSimple 데이터 보호 및 백업 기능을 관리하기 위한 MMC 스냅인인 StorSimple 스냅숏 관리자를 다운로드 및 설치하는 방법을 알아봅니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: cde355381b0d726a1ab340bc4230b2dc8f6e2c56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-snapshot-manager-mmc-snap-in"></a><span data-ttu-id="785f0-103">StorSimple 스냅숏 관리자 MMC 스냅인 배포</span><span class="sxs-lookup"><span data-stu-id="785f0-103">Deploy the StorSimple Snapshot Manager MMC snap-in</span></span>

## <a name="overview"></a><span data-ttu-id="785f0-104">개요</span><span class="sxs-lookup"><span data-stu-id="785f0-104">Overview</span></span>
<span data-ttu-id="785f0-105">StorSimple 스냅숏 관리자는 Microsoft Azure StorSimple 환경에서 데이터 보호 및 백업 관리를 간소화하는 MMC(Microsoft Management Console) 스냅인입니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-105">The StorSimple Snapshot Manager is a Microsoft Management Console (MMC) snap-in that simplifies data protection and backup management in a Microsoft Azure StorSimple environment.</span></span> <span data-ttu-id="785f0-106">StorSimple 스냅숏 관리자를 사용하면 완전히 통합된 저장소 시스템인 것처럼 Microsoft Azure StorSimple 온-프레미스 및 클라우드 저장소를 관리할 수 있으므로 백업 및 복원 프로세스가 간소화되고 비용이 절감됩니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-106">With StorSimple Snapshot Manager, you can manage Microsoft Azure StorSimple on-premises and cloud storage as if it were a fully integrated storage system, thus simplifying backup and restore processes and reducing costs.</span></span> 

<span data-ttu-id="785f0-107">이 자습서에서는 StorSimple 스냅숏 관리자 설치, 제거 및 업그레이드에 대한 절차와 더불어 구성 요구 사항도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-107">This tutorial describes configuration requirements, as well as procedures for installing, removing, and upgrading StorSimple Snapshot Manager.</span></span>

> [!NOTE]
> * <span data-ttu-id="785f0-108">StorSimple 스냅숏 관리자를 사용하여 Microsoft Azure StorSimple 가상 배열 (StorSimple 온-프레미스 가상 장치라고도 함)를 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-108">You cannot use StorSimple Snapshot Manager to manage Microsoft Azure StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices).</span></span>
> * <span data-ttu-id="785f0-109">StorSimple 장치에 StorSimple 업데이트 2를 설치하려는 경우 StorSimple Snapshot Manager의 최신 버전을 다운로드하여 **StorSimple 업데이트 2를 설치하기 전에**설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-109">If you plan to install StorSimple Update 2 on your StorSimple device, be sure to download the latest version of StorSimple Snapshot Manager and install it **before you install StorSimple Update 2**.</span></span> <span data-ttu-id="785f0-110">StorSimple Snapshot Manager의 최신 버전은 이전 버전과 호환되며 릴리스된 모든 버전의 Microsoft Azure StorSimple에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-110">The latest version of StorSimple Snapshot Manager is backward compatible and works with all released versions of Microsoft Azure StorSimple.</span></span> <span data-ttu-id="785f0-111">StorSimple Snapshot Manager의 이전 버전을 사용하고 있다면 업데이트해야 합니다(새 버전을 설치하기 전에 이전 버전을 제거할 필요 없음).</span><span class="sxs-lookup"><span data-stu-id="785f0-111">If you are using the previous version of StorSimple Snapshot Manager, you will need to update it (you do not need to uninstall the previous version before you install the new version).</span></span>


## <a name="storsimple-snapshot-manager-installation"></a><span data-ttu-id="785f0-112">StorSimple 스냅숏 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="785f0-112">StorSimple Snapshot Manager installation</span></span>
<span data-ttu-id="785f0-113">StorSimple Snapshot Manager는 Windows Server 2008 R2 SP1, Windows Server 2012 또는 Windows Server 2012 R2 운영 체제를 실행하는 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-113">StorSimple Snapshot Manager can be installed on computers that are running the Windows Server 2008 R2 SP1, Windows Server 2012, or Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="785f0-114">Windows 2008 R2를 실행하는 서버에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-114">On servers running Windows 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0.</span></span>

<span data-ttu-id="785f0-115">Microsoft Management Console(MMC)용 StorSimple 스냅숏 관리자 스냅인을 설치하거나 업그레이드하기 전에 Microsoft Azure StorSimple 장치 및 호스트 서버가 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-115">Before you install or upgrade the StorSimple Snapshot Manager snap-in for the Microsoft Management Console (MMC), make sure that the Microsoft Azure StorSimple device and host server are configured correctly.</span></span>

## <a name="configure-prerequisites"></a><span data-ttu-id="785f0-116">필수 조건 구성</span><span class="sxs-lookup"><span data-stu-id="785f0-116">Configure prerequisites</span></span>
<span data-ttu-id="785f0-117">다음 단계에서는 StorSimple 스냅숏 관리자를 설치하기 전에 완료해야 하는 구성 작업의 대략적인 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-117">The following steps provide a high-level overview of configuration tasks that you must complete before you install the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="785f0-118">시스템 요구 사항 및 단계별 지침을 포함한 전체 Microsoft Azure StorSimple 구성 및 설치 정보는 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-118">For complete Microsoft Azure StorSimple configuration and setup information, including system requirements and step-by-step instructions, see [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="785f0-119">시작하기 전에 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)에서 [배포 구성 검사 목록](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) 및 [배포 필수 조건](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-119">Before you begin, review the [Deployment configuration checklist](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) and and [Deployment prerequisites](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a><span data-ttu-id="785f0-120">StorSimple 스냅숏 관리자를 설치하기 전에</span><span class="sxs-lookup"><span data-stu-id="785f0-120">Before you install StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="785f0-121">[StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md) 또는 [StorSimple 8600 장치 설치](storsimple-8600-hardware-installation.md)에 설명된 대로 Microsoft Azure StorSimple 장치를 개봉하고 탑재한 후 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-121">Unpack, mount, and connect the Microsoft Azure StorSimple device as described in [Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md) or [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
2. <span data-ttu-id="785f0-122">호스트 컴퓨터에서 다음 운영 체제 중 하나를 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-122">Make sure that your host computer is running one of the following operating systems:</span></span>
   
   * <span data-ttu-id="785f0-123">Windows Server 2008 R2(Windows 2008 R2를 실행하는 서버에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="785f0-123">Windows Server 2008 R2 (on servers running Windows 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0)</span></span>
   * <span data-ttu-id="785f0-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="785f0-124">Windows Server 2012</span></span>
   * <span data-ttu-id="785f0-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="785f0-125">Windows Server 2012 R2</span></span>
     
     <span data-ttu-id="785f0-126">StorSimple 가상 장치의 경우 호스트는 Microsoft Azure 가상 컴퓨터여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-126">For a StorSimple virtual device, the host must be a Microsoft Azure Virtual Machine.</span></span>
3. <span data-ttu-id="785f0-127">Microsoft Azure StorSimple 구성 요구 사항이 모두 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-127">Make sure that you meet all the Microsoft Azure StorSimple configuration requirements.</span></span> <span data-ttu-id="785f0-128">자세한 내용은 [배포 필수 조건](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-128">For details, go to [Deployment prerequisites](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).</span></span>
4. <span data-ttu-id="785f0-129">호스트에 장치를 연결하고 초기 구성을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-129">Connect the device to the host and perform the initial configuration.</span></span> <span data-ttu-id="785f0-130">자세한 내용은 [배포 단계](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-130">For details, go to [Deployment steps](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).</span></span>
5. <span data-ttu-id="785f0-131">장치에서 볼륨을 만들어 호스트에 할당한 후 호스트에 탑재하여 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-131">Create volumes on the device, assign them to the host, and verify that the host can mount and use them.</span></span> <span data-ttu-id="785f0-132">StorSimple 스냅숏 관리자는 다음과 같은 유형의 볼륨을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-132">StorSimple Snapshot Manager supports the following types of volumes:</span></span>
   
   * <span data-ttu-id="785f0-133">기본 볼륨</span><span class="sxs-lookup"><span data-stu-id="785f0-133">Basic volumes</span></span>
   * <span data-ttu-id="785f0-134">단순 볼륨</span><span class="sxs-lookup"><span data-stu-id="785f0-134">Simple volumes</span></span>
   * <span data-ttu-id="785f0-135">동적 볼륨</span><span class="sxs-lookup"><span data-stu-id="785f0-135">Dynamic volumes</span></span>
   * <span data-ttu-id="785f0-136">미러된 동적 볼륨(RAID 1)</span><span class="sxs-lookup"><span data-stu-id="785f0-136">Mirrored dynamic volumes (RAID 1)</span></span>
   * <span data-ttu-id="785f0-137">클러스터 공유 볼륨</span><span class="sxs-lookup"><span data-stu-id="785f0-137">Cluster-shared volumes</span></span>
     
     <span data-ttu-id="785f0-138">StorSimple 장치 또는 StorSimple 가상 장치에서 볼륨을 만드는 방법에 대한 자세한 내용은 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)에서 [6단계: 볼륨 만들기](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-138">For information about creating volumes on the StorSimple device or StorSimple virtual device, go to [Step 6: Create a volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

## <a name="install-a-new-storsimple-snapshot-manager"></a><span data-ttu-id="785f0-139">새 StorSimple 스냅숏 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="785f0-139">Install a new StorSimple Snapshot Manager</span></span>
<span data-ttu-id="785f0-140">StorSimple 스냅숏 관리자를 설치하기 전에 StorSimple 장치 또는 StorSimple 가상 장치에서 만든 볼륨이 [필수 조건 구성](#configure-prerequisites)에서 설명한 대로 탑재, 초기화 및 포맷되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-140">Before installing StorSimple Snapshot Manager, make sure that the volumes you created on the StorSimple device or StorSimple virtual device are mounted, initialized, and formatted as described in [Configure prerequisites](#configure-prerequisites).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="785f0-141">StorSimple 가상 장치의 경우 호스트는 Microsoft Azure 가상 컴퓨터여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-141">For a StorSimple virtual device, the host must be a Microsoft Azure Virtual Machine.</span></span> 
> * <span data-ttu-id="785f0-142">호스트에서 Windows 2008 R2, Windows Server 2012 또는 Windows Server 2012 R2가 실행되고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-142">The host must be running Windows 2008 R2, Windows Server 2012, or Windows Server 2012 R2.</span></span> <span data-ttu-id="785f0-143">서버에서 Windows Server 2008 R2를 실행하는 경우에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-143">If your server is running Windows Server 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0.</span></span>
> * <span data-ttu-id="785f0-144">StorSimple 스냅숏 관리자에 장치를 연결하려면 먼저 호스트에서 StorSimple 장치로 iSCSI 연결을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-144">You must configure an iSCSI connection from the host to the StorSimple device before you can connect the device to StorSimple Snapshot Manager.</span></span>

<span data-ttu-id="785f0-145">StorSimple 스냅숏 관리자의 새로운 설치를 완료하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-145">Follow these steps to complete a fresh installation of StorSimple Snapshot Manager.</span></span> <span data-ttu-id="785f0-146">업그레이드를 설치하는 경우는 [StorSimple 스냅숏 관리자 업그레이드 또는 다시 설치](#upgrade-or-reinstall-storsimple-snapshot-manager)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-146">If you are installing an upgrade, go to [Upgrade or reinstall StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager).</span></span>

* <span data-ttu-id="785f0-147">1단계: StorSimple 스냅숏 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="785f0-147">Step 1: Install StorSimple Snapshot Manager</span></span> 
* <span data-ttu-id="785f0-148">2단계: 장치에 StorSimple 스냅숏 관리자 연결</span><span class="sxs-lookup"><span data-stu-id="785f0-148">Step 2: Connect StorSimple Snapshot Manager to a device</span></span> 
* <span data-ttu-id="785f0-149">3단계: 장치에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="785f0-149">Step 3: Verify the connection to the device</span></span> 

### <a name="step-1-install-storsimple-snapshot-manager"></a><span data-ttu-id="785f0-150">1단계: StorSimple 스냅숏 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="785f0-150">Step 1: Install StorSimple Snapshot Manager</span></span>
<span data-ttu-id="785f0-151">다음 단계를 사용하여 StorSimple 스냅숏 관리자를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-151">Use the following steps to install StorSimple Snapshot Manager.</span></span>

#### <a name="to-install-storsimple-snapshot-manager"></a><span data-ttu-id="785f0-152">StorSimple 스냅숏 관리자를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="785f0-152">To install StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="785f0-153">StorSimple 스냅숏 관리자 소프트웨어를 다운로드(Microsoft 다운로드 센터에서 [StorSimple 스냅숏 관리자](https://www.microsoft.com/download/details.aspx?id=44220) 로 이동)하고 호스트에 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-153">Download the StorSimple Snapshot Manager software (go to [StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) in the Microsoft Download Center) and save it locally on the host.</span></span>
2. <span data-ttu-id="785f0-154">파일 탐색기에서 압축된 폴더를 마우스 오른쪽 단추로 클릭하고 **모두 추출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-154">In File Explorer, right-click the compressed folder, and then click **Extract all**.</span></span>
3. <span data-ttu-id="785f0-155">**압축(Zip) 폴더 풀기** 창의 **대상을 선택하고 압축 파일을 푸십시오.** 상자에서 파일을 추출할 경로를 입력하거나 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-155">In the **Extract Compressed (Zipped) Folders** window, in the **Select a destination and extract files** box, type or browse to the path where you would like to file to be extracted.</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="785f0-156">C: 드라이브에 StorSimple 스냅숏 관리자를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-156">You must install StorSimple Snapshot Manager on the C: drive.</span></span>
    
4. <span data-ttu-id="785f0-157">**완료되면 압축을 푼 파일 표시** 확인란을 선택한 다음 **추출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-157">Select the **Show extracted files when complete** check box, and then click **Extract**.</span></span>
   
    ![파일 추출 대화 상자](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. <span data-ttu-id="785f0-159">추출이 완료되면 대상 폴더가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-159">When the extraction is finished, the destination folder opens.</span></span> <span data-ttu-id="785f0-160">대상 폴더에 표시되는 응용 프로그램 설치 아이콘을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-160">Double-click the application setup icon that appears in the destination folder.</span></span>
6. <span data-ttu-id="785f0-161">**설치 완료** 메시지가 나타나면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-161">When the **Setup Successful** message appears, click **Close**.</span></span> <span data-ttu-id="785f0-162">바탕 화면에 StorSimple 스냅숏 관리자 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-162">You should see the StorSimple Snapshot Manager icon on your desktop.</span></span>
   
    ![바탕 화면 아이콘](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-to-a-device"></a><span data-ttu-id="785f0-164">2단계: 장치에 StorSimple 스냅숏 관리자 연결</span><span class="sxs-lookup"><span data-stu-id="785f0-164">Step 2: Connect StorSimple Snapshot Manager to a device</span></span>
<span data-ttu-id="785f0-165">다음 단계를 사용하여 StorSimple 스냅숏 관리자를 StorSimple 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-165">Use the following steps to connect StorSimple Snapshot Manager to a StorSimple device.</span></span>

#### <a name="to-connect-storsimple-snapshot-manager-to-a-device"></a><span data-ttu-id="785f0-166">장치에 StorSimple 스냅숏 관리자를 연결하려면</span><span class="sxs-lookup"><span data-stu-id="785f0-166">To connect StorSimple Snapshot Manager to a device</span></span>
1. <span data-ttu-id="785f0-167">바탕 화면에서 StorSimple 스냅숏 관리자 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-167">Click the StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="785f0-168">StorSimple 스냅숏 관리자 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-168">The StorSimple Snapshot Manager window appears.</span></span> <span data-ttu-id="785f0-169">창에는 **범위** 창, **결과** 창 및 **작업** 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-169">The window contains a **Scope** pane, a **Results** pane, and an **Actions** pane.</span></span> 
   
    ![StorSimple 스냅숏 관리자 사용자 인터페이스](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * <span data-ttu-id="785f0-171">**범위** 창(왼쪽 창)에는 트리 구조로 정리된 노드 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-171">The **Scope** pane (the left pane) contains a list of nodes organized in a tree structure.</span></span> <span data-ttu-id="785f0-172">일부 노드를 확장하면 해당 노드와 관련된 보기 또는 특정 데이터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-172">You can expand some nodes to select a view or specific data related to that node.</span></span> <span data-ttu-id="785f0-173">노드를 확장하거나 축소하려면 화살표 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-173">Click the arrow icon to expand or collapse a node.</span></span> <span data-ttu-id="785f0-174">**범위** 창에서 항목을 마우스 오른쪽 단추로 클릭하면 해당 항목에 대해 사용할 수 있는 작업 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-174">Right-click an item in the **Scope** pane to see a list of available actions for that item.</span></span>
   * <span data-ttu-id="785f0-175">**결과** 창(가운데 창)에는 **범위** 창에서 선택한 노드, 보기 또는 데이터에 대한 자세한 상태 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-175">The **Results** pane (the center pane) contains detailed status information about the node, view, or data that you selected in the **Scope** pane.</span></span>
   * <span data-ttu-id="785f0-176">**작업** 창에는 **범위** 창에서 선택한 노드, 보기 또는 데이터에서 수행할 수 있는 작업이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-176">The **Actions** pane lists the operations that you can perform on the node, view, or data that you selected in the **Scope** pane.</span></span>
     
     <span data-ttu-id="785f0-177">StorSimple 스냅숏 관리자 사용자 인터페이스에 대한 자세한 설명은 [StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-177">For a complete description of the StorSimple Snapshot Manager user interface, see [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
2. <span data-ttu-id="785f0-178">**범위** 창에서 **장치** 노드를 마우스 오른쪽 단추로 클릭한 다음 **장치 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-178">In the **Scope** pane, right-click the **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="785f0-179">**장치 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-179">The **Configure a Device** dialog box appears.</span></span>
   
    ![장치 구성](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. <span data-ttu-id="785f0-181">**장치** 목록 상자에서 Microsoft Azure StorSimple 장치 또는 가상 장치의 IP 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-181">In the **Device** list box, select the IP address of the Microsoft Azure StorSimple device or virtual device.</span></span> <span data-ttu-id="785f0-182">암호 **텍스트 상자** 에 Azure Portal에서 장치에 대한 StorSimple 스냅숏 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-182">In the **Password** text box, type the StorSimple Snapshot Manager password that you created for the device in the Azure portal.</span></span> <span data-ttu-id="785f0-183">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-183">Click **OK**.</span></span>
4. <span data-ttu-id="785f0-184">StorSimple 스냅숏 관리자에서 사용자가 지정한 장치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-184">StorSimple Snapshot Manager searches for the device that you identified.</span></span> <span data-ttu-id="785f0-185">장치를 사용할 수 있으면 StorSimple 스냅숏 관리자가 연결을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-185">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="785f0-186">[장치에 대한 연결 확인](#to-verify-the-connection) 을 통해 연결이 성공적으로 추가되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-186">You can [verify the connection to the device](#to-verify-the-connection) to confirm that the connection was added successfully.</span></span>
   
    <span data-ttu-id="785f0-187">어떤 이유로든 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자에서 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-187">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="785f0-188">**확인**을 클릭하여 오류 메시지를 닫은 다음 **취소**를 클릭하여 **장치 구성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-188">Click **OK** to close the error message, and then click **Cancel** to close the **Configure a Device** dialog box.</span></span>
5. <span data-ttu-id="785f0-189">장치에 연결할 때 볼륨 그룹에 연결된 백업이 있는 경우 StorSimple 스냅숏 관리자는 해당 장치에 대해 구성된 각 볼륨 그룹을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-189">When it connects to a device, StorSimple Snapshot Manager imports each volume group configured for that device, provided that the volume group has associated backups.</span></span> <span data-ttu-id="785f0-190">연결된 백업이 없는 볼륨 그룹은 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-190">Volume groups that do not have associated backups are not imported.</span></span> <span data-ttu-id="785f0-191">또한 볼륨 그룹에 대해 만든 백업 정책도 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-191">Additionally, backup policies that were created for a volume group are not imported.</span></span> <span data-ttu-id="785f0-192">가져온 그룹을 보려면 **범위** 창의 최상위 **볼륨 그룹** 노드를 마우스 오른쪽 단추로 클릭하고 **가져온 그룹 설정/해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-192">To see the imported groups, right-click the top-most **Volume Groups** node in the **Scope** pane, and click **Toggle imported groups**.</span></span>

### <a name="step-3-verify-the-connection-to-the-device"></a><span data-ttu-id="785f0-193">3단계: 장치에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="785f0-193">Step 3: Verify the connection to the device</span></span>
<span data-ttu-id="785f0-194">다음 단계를 사용하여 StorSimple 스냅숏 관리자가 StorSimple 장치에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-194">Use the following steps to verify that StorSimple Snapshot Manager is connected to the StorSimple device.</span></span>

#### <a name="to-verify-the-connection"></a><span data-ttu-id="785f0-195">연결을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="785f0-195">To verify the connection</span></span>
1. <span data-ttu-id="785f0-196">**범위** 창에서 **장치** 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-196">In the **Scope** pane, click the **Devices** node.</span></span>
   
    ![StorSimple 스냅숏 관리자 장치 상태](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. <span data-ttu-id="785f0-198">**결과** 창에서 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-198">Check the **Results** pane:</span></span> 
   
   * <span data-ttu-id="785f0-199">장치 아이콘에 녹색 표시기가 나타나고 **상태** 열에 **사용 가능**이 나타나면 해당 장치는 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-199">If a green indicator appears on the device icon and **Available** appears in the **Status** column, then the device is connected.</span></span> 
   * <span data-ttu-id="785f0-200">장치 아이콘에 빨간색 표시기가 나타나고 **상태** 열에 사용할 수 없음이 나타나면 해당 장치는 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-200">If a red indicator appears on the device icon and Unavailable appears in the **Status** column, then the device is not connected.</span></span> 
   * <span data-ttu-id="785f0-201">**상태** 열에 **새로 고치는 중**이 표시되면 StorSimple Snapshot Manager가 연결된 장치에 대해 연결된 백업 및 볼륨 그룹을 검색하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-201">If **Refreshing** appears in the **Status** column, then StorSimple Snapshot Manager is retrieving volume groups and associated backups for a connected device.</span></span>

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a><span data-ttu-id="785f0-202">StorSimple 스냅숏 관리자 업그레이드 또는 다시 설치</span><span class="sxs-lookup"><span data-stu-id="785f0-202">Upgrade or reinstall StorSimple Snapshot Manager</span></span>
<span data-ttu-id="785f0-203">StorSimple 스냅숏 관리자를 업그레이드하거나 다시 설치하기 전에 해당 소프트웨어를 완전히 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-203">You should uninstall StorSimple Snapshot Manager completely before you upgrade or reinstall the software.</span></span> 

<span data-ttu-id="785f0-204">StorSimple 스냅숏 관리자를 다시 설치하기 전에 호스트 컴퓨터에 있는 기존 StorSimple 스냅숏 관리자 데이터베이스를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-204">Before reinstalling StorSimple Snapshot Manager, back up the existing StorSimple Snapshot Manager database on the host computer.</span></span> <span data-ttu-id="785f0-205">이렇게 하면 백업 정책 및 구성 정보도 저장되므로 백업에서 이 데이터를 쉽게 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-205">This saves the backup policies and configuration information so that you can easily restore this data from backup.</span></span>

<span data-ttu-id="785f0-206">StorSimple 스냅숏 관리자를 업그레이드하거나 다시 설치하는 경우 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-206">Follow these steps if you are upgrading or reinstalling StorSimple Snapshot Manager:</span></span>

* <span data-ttu-id="785f0-207">1단계: StorSimple 스냅숏 관리자 제거</span><span class="sxs-lookup"><span data-stu-id="785f0-207">Step 1: Uninstall StorSimple Snapshot Manager</span></span> 
* <span data-ttu-id="785f0-208">2단계: StorSimple 스냅숏 관리자 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="785f0-208">Step 2: Back up the StorSimple Snapshot Manager database</span></span> 
* <span data-ttu-id="785f0-209">3단계: StorSimple 스냅숏 관리자 다시 설치 및 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="785f0-209">Step 3: Reinstall StorSimple Snapshot Manager and restore the database</span></span> 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a><span data-ttu-id="785f0-210">1단계: StorSimple 스냅숏 관리자 제거</span><span class="sxs-lookup"><span data-stu-id="785f0-210">Step 1: Uninstall StorSimple Snapshot Manager</span></span>
<span data-ttu-id="785f0-211">다음 단계를 사용하여 StorSimple 스냅숏 관리자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-211">Use the following steps to uninstall StorSimple Snapshot Manager.</span></span>

#### <a name="to-uninstall-storsimple-snapshot-manager"></a><span data-ttu-id="785f0-212">StorSimple 스냅숏 관리자를 제거하려면</span><span class="sxs-lookup"><span data-stu-id="785f0-212">To uninstall StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="785f0-213">호스트 컴퓨터에서 **제어판**을 열고 **프로그램**을 클릭한 다음 **프로그램 및 기능**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-213">On the host computer, open the **Control Panel**, click **Programs**, and then click **Programs and Features**.</span></span>
2. <span data-ttu-id="785f0-214">왼쪽 창에서 **프로그램 제거 또는 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-214">In the left pane, click **Uninstall or change a program**.</span></span>
3. <span data-ttu-id="785f0-215">**StorSimple Snapshot Manager**를 마우스 오른쪽 단추로 클릭하고 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-215">Right-click **StorSimple Snapshot Manager**, and then click **Uninstall**.</span></span>
4. <span data-ttu-id="785f0-216">그러면 StorSimple 스냅숏 관리자 설치 프로그램이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-216">This starts the StorSimple Snapshot Manager Setup program.</span></span> <span data-ttu-id="785f0-217">**설치 수정**을 클릭하고 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-217">Click **Modify Setup**, and then click **Uninstall**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="785f0-218">StorSimple 스냅숏 관리자 또는 디스크 관리 등과 같은 MMC 프로세스가 백그라운드로 실행되고 있으면 제거에 실패하게 되고 프로그램을 제거하려면 먼저 모든 MMC 인스턴스를 닫으라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-218">If there are any MMC processes running in the background, such as StorSimple Snapshot Manager or Disk Management, the uninstall will fail and you will receive a message to close all instances of MMC before you attempt to uninstall the program.</span></span> <span data-ttu-id="785f0-219">**설치가 완료되면 자동으로 응용 프로그램을 닫고 다시 시작합니다**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-219">Select **Automatically close applications and attempt to restart them after setup is complete**, and then click **OK**.</span></span>
   > 
   > 
5. <span data-ttu-id="785f0-220">제거 프로세스가 완료되면 **설치 완료** 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-220">When the uninstall process is finished, a **Setup Successful** message appears.</span></span> <span data-ttu-id="785f0-221">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-221">Click **Close**.</span></span>

### <a name="step-2-back-up-the-storsimple-snapshot-manager-database"></a><span data-ttu-id="785f0-222">2단계: StorSimple 스냅숏 관리자 데이터베이스 백업</span><span class="sxs-lookup"><span data-stu-id="785f0-222">Step 2: Back up the StorSimple Snapshot Manager database</span></span>
<span data-ttu-id="785f0-223">다음 단계를 사용하여 StorSimple 스냅숏 관리자 데이터베이스의 복사본을 만들어 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-223">Use the following steps to create and save a copy of the StorSimple Snapshot Manager database.</span></span>

#### <a name="to-back-up-the-database"></a><span data-ttu-id="785f0-224">데이터베이스를 백업하려면</span><span class="sxs-lookup"><span data-stu-id="785f0-224">To back up the database</span></span>
1. <span data-ttu-id="785f0-225">Microsoft StorSimple 관리 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-225">Stop the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="785f0-226">서버 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-226">Start Server Manager.</span></span>
   2. <span data-ttu-id="785f0-227">서버 관리자 대시보드의 **도구** 메뉴에서 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-227">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="785f0-228">**서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-228">On the **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="785f0-229">오른쪽 창의 **Microsoft StorSimple 관리 서비스** 아래에서 **서비스 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-229">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span></span>
      
        ![StorSimple 장치 관리자 서비스 중지](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. <span data-ttu-id="785f0-231">C:\ProgramData\Microsoft\StorSimple\BACatalog로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-231">Browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="785f0-232">ProgramData는 숨겨진 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-232">ProgramData is a hidden folder.</span></span>
  
3. <span data-ttu-id="785f0-233">카탈로그 XML 파일을 찾아 파일을 복사하고 안전한 위치 또는 클라우드에 복사본을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-233">Find the catalog XML file, copy the file, and store the copy in a safe location or in the cloud.</span></span>
   
    ![StorSimple 백업 카탈로그 파일](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. <span data-ttu-id="785f0-235">Microsoft StorSimple 관리 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-235">Restart the Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="785f0-236">서버 관리자 대시보드의 **도구** 메뉴에서 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-236">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="785f0-237">**서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-237">On the **Services** page, select the **Microsoft StorSimple Management Servic**e.</span></span>
   3. <span data-ttu-id="785f0-238">오른쪽 창의 **Microsoft StorSimple 관리 서비스** 아래에서 **서비스 다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-238">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span></span> 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-the-database"></a><span data-ttu-id="785f0-239">3단계: StorSimple 스냅숏 관리자 다시 설치 및 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="785f0-239">Step 3: Reinstall StorSimple Snapshot Manager and restore the database</span></span>
<span data-ttu-id="785f0-240">StorSimple 스냅숏 관리자를 다시 설치하려면 [새 StorSimple 스냅숏 관리자 설치](#install-a-new-storsimple-snapshot-manager)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-240">To reinstall StorSimple Snapshot Manager, follow the steps in [Install a new StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager).</span></span> <span data-ttu-id="785f0-241">그런 다음 아래의 절차를 사용하여 StorSimple 스냅숏 관리자 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-241">Then, use the following procedure to restore the StorSimple Snapshot Manager database.</span></span>

#### <a name="to-restore-the-database"></a><span data-ttu-id="785f0-242">데이터베이스를 복원하려면</span><span class="sxs-lookup"><span data-stu-id="785f0-242">To restore the database</span></span>
1. <span data-ttu-id="785f0-243">Microsoft StorSimple 관리 서비스를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-243">Stop the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="785f0-244">서버 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-244">Start Server Manager.</span></span>
   2. <span data-ttu-id="785f0-245">서버 관리자 대시보드의 **도구** 메뉴에서 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-245">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="785f0-246">**서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-246">On the **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="785f0-247">오른쪽 창의 **Microsoft StorSimple 관리 서비스** 아래에서 **서비스 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-247">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span></span>
2. <span data-ttu-id="785f0-248">C:\ProgramData\Microsoft\StorSimple\BACatalog로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-248">Browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="785f0-249">ProgramData는 숨겨진 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-249">ProgramData is a hidden folder.</span></span>
   > 
   > 
3. <span data-ttu-id="785f0-250">카탈로그 XML 파일을 삭제하고 이전에 저장한 버전으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-250">Delete the catalog XML file, and replace it with the version that you saved earlier.</span></span>
4. <span data-ttu-id="785f0-251">Microsoft StorSimple 관리 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-251">Restart the Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="785f0-252">서버 관리자 대시보드의 **도구** 메뉴에서 **서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-252">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="785f0-253">**서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-253">On the **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="785f0-254">오른쪽 창의 **Microsoft StorSimple 관리 서비스** 아래에서 **서비스 다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="785f0-254">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="785f0-255">다음 단계</span><span class="sxs-lookup"><span data-stu-id="785f0-255">Next steps</span></span>
* <span data-ttu-id="785f0-256">StorSimple 스냅숏 관리자에 대해 자세히 알아보려면 [StorSimple 스냅숏 관리자란?](storsimple-what-is-snapshot-manager.md)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-256">To learn more about StorSimple Snapshot Manager, go to [What is StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md).</span></span>
* <span data-ttu-id="785f0-257">StorSimple 스냅숏 관리자 사용자 인터페이스에 대해 자세히 알아보려면 [StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-257">To learn more about the StorSimple Snapshot Manager user interface, go to [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
* <span data-ttu-id="785f0-258">StorSimple 스냅숏 관리자를 사용하는 방법에 대해 자세히 알아보려면 [StorSimple 스냅숏 관리자를 사용하여 StorSimple 솔루션 관리](storsimple-snapshot-manager-admin.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="785f0-258">To learn more about using StorSimple Snapshot Manager, go to [Use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>

