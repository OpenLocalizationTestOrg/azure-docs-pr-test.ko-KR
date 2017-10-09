---
title: "StorSimple 스냅숏 관리자 aaaDeploy | Microsoft Docs"
description: "설치 하 고 toodownload hello StorSimple 스냅숏 관리자는 MMC 스냅인 StorSimple 데이터 보호 및 백업 기능을 관리 하기 위한 방법에 대해 알아봅니다."
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
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a><span data-ttu-id="76073-103">StorSimple 스냅숏 관리자 MMC 스냅인 hello 배포</span><span class="sxs-lookup"><span data-stu-id="76073-103">Deploy hello StorSimple Snapshot Manager MMC snap-in</span></span>

## <a name="overview"></a><span data-ttu-id="76073-104">개요</span><span class="sxs-lookup"><span data-stu-id="76073-104">Overview</span></span>
<span data-ttu-id="76073-105">StorSimple 스냅숏 관리자 hello 데이터 보호 및 Microsoft Azure StorSimple 환경에서 백업 관리를 간소화 하는 Microsoft 관리 콘솔 (MMC) 스냅인입니다.</span><span class="sxs-lookup"><span data-stu-id="76073-105">hello StorSimple Snapshot Manager is a Microsoft Management Console (MMC) snap-in that simplifies data protection and backup management in a Microsoft Azure StorSimple environment.</span></span> <span data-ttu-id="76073-106">StorSimple 스냅숏 관리자를 사용하면 완전히 통합된 저장소 시스템인 것처럼 Microsoft Azure StorSimple 온-프레미스 및 클라우드 저장소를 관리할 수 있으므로 백업 및 복원 프로세스가 간소화되고 비용이 절감됩니다.</span><span class="sxs-lookup"><span data-stu-id="76073-106">With StorSimple Snapshot Manager, you can manage Microsoft Azure StorSimple on-premises and cloud storage as if it were a fully integrated storage system, thus simplifying backup and restore processes and reducing costs.</span></span> 

<span data-ttu-id="76073-107">이 자습서에서는 StorSimple 스냅숏 관리자 설치, 제거 및 업그레이드에 대한 절차와 더불어 구성 요구 사항도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-107">This tutorial describes configuration requirements, as well as procedures for installing, removing, and upgrading StorSimple Snapshot Manager.</span></span>

> [!NOTE]
> * <span data-ttu-id="76073-108">StorSimple 스냅숏 관리자 toomanage Microsoft Azure StorSimple 가상 배열 (라고도 StorSimple 온-프레미스 가상 장치)를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-108">You cannot use StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices).</span></span>
> * <span data-ttu-id="76073-109">StorSimple 장치에서 tooinstall StorSimple 업데이트 2를 계획할 수 있는지 toodownload hello 최신 버전의 StorSimple 스냅숏 관리자를 설치 **StorSimple 업데이트 2를 설치 하기 전에**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-109">If you plan tooinstall StorSimple Update 2 on your StorSimple device, be sure toodownload hello latest version of StorSimple Snapshot Manager and install it **before you install StorSimple Update 2**.</span></span> <span data-ttu-id="76073-110">hello 최신 버전의 StorSimple 스냅숏 관리자가 이전 버전과 호환 하며 모든 릴리스된 버전의 Microsoft Azure StorSimple과 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-110">hello latest version of StorSimple Snapshot Manager is backward compatible and works with all released versions of Microsoft Azure StorSimple.</span></span> <span data-ttu-id="76073-111">Tooupdate 할 hello 이전 버전의 StorSimple 스냅숏 관리자를 사용 하는 경우 it (않아도 toouninstall hello 이전 버전 hello 새 버전을 설치 하기 전에).</span><span class="sxs-lookup"><span data-stu-id="76073-111">If you are using hello previous version of StorSimple Snapshot Manager, you will need tooupdate it (you do not need toouninstall hello previous version before you install hello new version).</span></span>


## <a name="storsimple-snapshot-manager-installation"></a><span data-ttu-id="76073-112">StorSimple 스냅숏 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="76073-112">StorSimple Snapshot Manager installation</span></span>
<span data-ttu-id="76073-113">StorSimple 스냅숏 관리자 hello Windows Server 2008 R2 SP1, Windows Server 2012 또는 Windows Server 2012 R2 운영 체제를 실행 하는 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-113">StorSimple Snapshot Manager can be installed on computers that are running hello Windows Server 2008 R2 SP1, Windows Server 2012, or Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="76073-114">Windows 2008 R2를 실행하는 서버에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-114">On servers running Windows 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0.</span></span>

<span data-ttu-id="76073-115">를 설치 하거나 hello StorSimple 스냅숏 관리자 스냅인 콘솔 MMC (Microsoft Management) hello에 대 한 업그레이드 전에 호스트 서버가 제대로 구성 및 해당 hello Microsoft Azure StorSimple 장치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-115">Before you install or upgrade hello StorSimple Snapshot Manager snap-in for hello Microsoft Management Console (MMC), make sure that hello Microsoft Azure StorSimple device and host server are configured correctly.</span></span>

## <a name="configure-prerequisites"></a><span data-ttu-id="76073-116">필수 조건 구성</span><span class="sxs-lookup"><span data-stu-id="76073-116">Configure prerequisites</span></span>
<span data-ttu-id="76073-117">hello 다음 단계를 제공 구성 작업에 대 한 고급 개요 hello StorSimple 스냅숏 관리자를 설치 하기 전에 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-117">hello following steps provide a high-level overview of configuration tasks that you must complete before you install hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="76073-118">시스템 요구 사항 및 단계별 지침을 포함한 전체 Microsoft Azure StorSimple 구성 및 설치 정보는 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76073-118">For complete Microsoft Azure StorSimple configuration and setup information, including system requirements and step-by-step instructions, see [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76073-119">시작 하기 전에 검토 hello [배포 구성 검사 목록](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) 및 및 [배포 필수 구성 요소](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) 에 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-119">Before you begin, review hello [Deployment configuration checklist](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) and and [Deployment prerequisites](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a><span data-ttu-id="76073-120">StorSimple 스냅숏 관리자를 설치하기 전에</span><span class="sxs-lookup"><span data-stu-id="76073-120">Before you install StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="76073-121">압축 풀기 탑재 하 고에 설명 된 대로 hello Microsoft Azure StorSimple 장치를 연결 [StorSimple 8100 장치 설치](storsimple-8100-hardware-installation.md) 또는 [8600 StorSimple 장치 설치](storsimple-8600-hardware-installation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-121">Unpack, mount, and connect hello Microsoft Azure StorSimple device as described in [Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md) or [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
2. <span data-ttu-id="76073-122">호스트 컴퓨터 hello 다음 운영 체제 중 하나를 실행 중인 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-122">Make sure that your host computer is running one of hello following operating systems:</span></span>
   
   * <span data-ttu-id="76073-123">Windows Server 2008 R2(Windows 2008 R2를 실행하는 서버에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="76073-123">Windows Server 2008 R2 (on servers running Windows 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0)</span></span>
   * <span data-ttu-id="76073-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="76073-124">Windows Server 2012</span></span>
   * <span data-ttu-id="76073-125">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="76073-125">Windows Server 2012 R2</span></span>
     
     <span data-ttu-id="76073-126">StorSimple 가상 장치에 대 한 hello 호스트에는 Microsoft Azure 가상 컴퓨터 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-126">For a StorSimple virtual device, hello host must be a Microsoft Azure Virtual Machine.</span></span>
3. <span data-ttu-id="76073-127">모든 hello Microsoft Azure StorSimple 구성 요구 사항을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-127">Make sure that you meet all hello Microsoft Azure StorSimple configuration requirements.</span></span> <span data-ttu-id="76073-128">자세한 내용은 이동 너무[배포 필수 구성 요소](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-128">For details, go too[Deployment prerequisites](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).</span></span>
4. <span data-ttu-id="76073-129">Hello 장치 toohello 호스트를 연결 하 고 hello 초기 구성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-129">Connect hello device toohello host and perform hello initial configuration.</span></span> <span data-ttu-id="76073-130">자세한 내용은 이동 너무[배포 단계](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-130">For details, go too[Deployment steps](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).</span></span>
5. <span data-ttu-id="76073-131">Hello 장치에 볼륨 만들기, toohello 호스트를 할당 하 고 해당 hello 호스트가 탑재 하 고 사용할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-131">Create volumes on hello device, assign them toohello host, and verify that hello host can mount and use them.</span></span> <span data-ttu-id="76073-132">StorSimple 스냅숏 관리자 볼륨 유형만 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-132">StorSimple Snapshot Manager supports hello following types of volumes:</span></span>
   
   * <span data-ttu-id="76073-133">기본 볼륨</span><span class="sxs-lookup"><span data-stu-id="76073-133">Basic volumes</span></span>
   * <span data-ttu-id="76073-134">단순 볼륨</span><span class="sxs-lookup"><span data-stu-id="76073-134">Simple volumes</span></span>
   * <span data-ttu-id="76073-135">동적 볼륨</span><span class="sxs-lookup"><span data-stu-id="76073-135">Dynamic volumes</span></span>
   * <span data-ttu-id="76073-136">미러된 동적 볼륨(RAID 1)</span><span class="sxs-lookup"><span data-stu-id="76073-136">Mirrored dynamic volumes (RAID 1)</span></span>
   * <span data-ttu-id="76073-137">클러스터 공유 볼륨</span><span class="sxs-lookup"><span data-stu-id="76073-137">Cluster-shared volumes</span></span>
     
     <span data-ttu-id="76073-138">너무 hello StorSimple 장치 또는 StorSimple 가상 장치에서 볼륨을 만드는 방법에 대 한 정보를 보려면, 이동[6 단계: 볼륨 만들기](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)에 [온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-138">For information about creating volumes on hello StorSimple device or StorSimple virtual device, go too[Step 6: Create a volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

## <a name="install-a-new-storsimple-snapshot-manager"></a><span data-ttu-id="76073-139">새 StorSimple 스냅숏 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="76073-139">Install a new StorSimple Snapshot Manager</span></span>
<span data-ttu-id="76073-140">StorSimple 스냅숏 관리자를 설치 하기 전에 확인 된 hello StorSimple 장치 또는 StorSimple 가상 장치에 만든 hello 볼륨 탑재, 초기화, 이며에 설명 된 대로 형식이 지정 [필수 구성 요소 구성](#configure-prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-140">Before installing StorSimple Snapshot Manager, make sure that hello volumes you created on hello StorSimple device or StorSimple virtual device are mounted, initialized, and formatted as described in [Configure prerequisites](#configure-prerequisites).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="76073-141">StorSimple 가상 장치에 대 한 hello 호스트에는 Microsoft Azure 가상 컴퓨터 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-141">For a StorSimple virtual device, hello host must be a Microsoft Azure Virtual Machine.</span></span> 
> * <span data-ttu-id="76073-142">Windows 2008 R2, Windows Server 2012 또는 Windows Server 2012 R2 hello 호스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-142">hello host must be running Windows 2008 R2, Windows Server 2012, or Windows Server 2012 R2.</span></span> <span data-ttu-id="76073-143">서버에서 Windows Server 2008 R2를 실행하는 경우에는 Windows Server 2008 SP1 및 Windows Management Framework 3.0도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-143">If your server is running Windows Server 2008 R2, you must also install Windows Server 2008 SP1 and Windows Management Framework 3.0.</span></span>
> * <span data-ttu-id="76073-144">Hello 장치 tooStorSimple 스냅숏 관리자 연결 하기 전에 hello 호스트 toohello StorSimple 장치에서 iSCSI 연결을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-144">You must configure an iSCSI connection from hello host toohello StorSimple device before you can connect hello device tooStorSimple Snapshot Manager.</span></span>

<span data-ttu-id="76073-145">이러한 단계 toocomplete StorSimple 스냅숏 관리자의 새로 설치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-145">Follow these steps toocomplete a fresh installation of StorSimple Snapshot Manager.</span></span> <span data-ttu-id="76073-146">업그레이드를 설치 하는 경우 너무 이동[업그레이드 StorSimple 스냅숏 관리자를 다시 설치 하거나](#upgrade-or-reinstall-storsimple-snapshot-manager)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-146">If you are installing an upgrade, go too[Upgrade or reinstall StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager).</span></span>

* <span data-ttu-id="76073-147">1단계: StorSimple 스냅숏 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="76073-147">Step 1: Install StorSimple Snapshot Manager</span></span> 
* <span data-ttu-id="76073-148">2 단계: tooa StorSimple 스냅숏 관리자 장치 연결</span><span class="sxs-lookup"><span data-stu-id="76073-148">Step 2: Connect StorSimple Snapshot Manager tooa device</span></span> 
* <span data-ttu-id="76073-149">3 단계: hello 연결 toohello 장치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-149">Step 3: Verify hello connection toohello device</span></span> 

### <a name="step-1-install-storsimple-snapshot-manager"></a><span data-ttu-id="76073-150">1단계: StorSimple 스냅숏 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="76073-150">Step 1: Install StorSimple Snapshot Manager</span></span>
<span data-ttu-id="76073-151">다음 단계 tooinstall StorSimple 스냅숏 관리자 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-151">Use hello following steps tooinstall StorSimple Snapshot Manager.</span></span>

#### <a name="tooinstall-storsimple-snapshot-manager"></a><span data-ttu-id="76073-152">StorSimple 스냅숏 관리자 tooinstall</span><span class="sxs-lookup"><span data-stu-id="76073-152">tooinstall StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="76073-153">Hello StorSimple 스냅숏 관리자 소프트웨어 다운로드 (너무 이동[StorSimple 스냅숏 관리자](https://www.microsoft.com/download/details.aspx?id=44220) hello Microsoft 다운로드 센터에서에서) hello 호스트에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-153">Download hello StorSimple Snapshot Manager software (go too[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) in hello Microsoft Download Center) and save it locally on hello host.</span></span>
2. <span data-ttu-id="76073-154">파일 탐색기에서 폴더를 압축된 하는 hello를 마우스 오른쪽 단추로 클릭 하 고 클릭 **압축 풀기**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-154">In File Explorer, right-click hello compressed folder, and then click **Extract all**.</span></span>
3. <span data-ttu-id="76073-155">Hello에 **압축 (Zip) 폴더 풀기** 창의 hello **대상을 선택 하 고 파일 압축 풀기** 입력란에 입력 하거나 찾아보기 toofile toobe 추출 하려는 toohello 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76073-155">In hello **Extract Compressed (Zipped) Folders** window, in hello **Select a destination and extract files** box, type or browse toohello path where you would like toofile toobe extracted.</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="76073-156">StorSimple 스냅숏 관리자 hello c: 드라이브에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-156">You must install StorSimple Snapshot Manager on hello C: drive.</span></span>
    
4. <span data-ttu-id="76073-157">선택 hello **완료 되 면 파일 압축을 푼 표시** 확인란을 선택한 다음 클릭 **추출**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-157">Select hello **Show extracted files when complete** check box, and then click **Extract**.</span></span>
   
    ![파일 추출 대화 상자](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. <span data-ttu-id="76073-159">Hello 추출 완료 되 면 hello 대상 폴더가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="76073-159">When hello extraction is finished, hello destination folder opens.</span></span> <span data-ttu-id="76073-160">Hello hello 대상 폴더에 표시 되는 응용 프로그램 설치 아이콘을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-160">Double-click hello application setup icon that appears in hello destination folder.</span></span>
6. <span data-ttu-id="76073-161">Hello 때 **설치 완료** 메시지가 표시 되 면 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-161">When hello **Setup Successful** message appears, click **Close**.</span></span> <span data-ttu-id="76073-162">StorSimple 스냅숏 관리자 아이콘 hello 바탕 화면에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76073-162">You should see hello StorSimple Snapshot Manager icon on your desktop.</span></span>
   
    ![바탕 화면 아이콘](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a><span data-ttu-id="76073-164">2 단계: tooa StorSimple 스냅숏 관리자 장치 연결</span><span class="sxs-lookup"><span data-stu-id="76073-164">Step 2: Connect StorSimple Snapshot Manager tooa device</span></span>
<span data-ttu-id="76073-165">다음 단계 tooconnect StorSimple 스냅숏 관리자 tooa StorSimple 장치 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-165">Use hello following steps tooconnect StorSimple Snapshot Manager tooa StorSimple device.</span></span>

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a><span data-ttu-id="76073-166">StorSimple 스냅숏 관리자 tooa 장치 tooconnect</span><span class="sxs-lookup"><span data-stu-id="76073-166">tooconnect StorSimple Snapshot Manager tooa device</span></span>
1. <span data-ttu-id="76073-167">바탕 화면에 hello StorSimple 스냅숏 관리자 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-167">Click hello StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="76073-168">hello StorSimple 스냅숏 관리자 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="76073-168">hello StorSimple Snapshot Manager window appears.</span></span> <span data-ttu-id="76073-169">hello 창에는 **범위** 창은 **결과** 창 및 **동작** 창.</span><span class="sxs-lookup"><span data-stu-id="76073-169">hello window contains a **Scope** pane, a **Results** pane, and an **Actions** pane.</span></span> 
   
    ![StorSimple 스냅숏 관리자 사용자 인터페이스](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * <span data-ttu-id="76073-171">hello **범위** 창 (왼쪽된 창의 hello)를 트리 구조로 구성 된 노드 목록이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-171">hello **Scope** pane (hello left pane) contains a list of nodes organized in a tree structure.</span></span> <span data-ttu-id="76073-172">일부 노드 tooselect 뷰 또는 특정 데이터 관련된 toothat 노드를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-172">You can expand some nodes tooselect a view or specific data related toothat node.</span></span> <span data-ttu-id="76073-173">Hello 화살표 아이콘 tooexpand 클릭 하거나 노드를 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-173">Click hello arrow icon tooexpand or collapse a node.</span></span> <span data-ttu-id="76073-174">Hello에 있는 항목을 마우스 오른쪽 단추로 클릭 **범위** 창 toosee 해당 항목에 대 한 사용 가능한 작업 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76073-174">Right-click an item in hello **Scope** pane toosee a list of available actions for that item.</span></span>
   * <span data-ttu-id="76073-175">hello **결과** hello 노드, 뷰 또는 hello에서 선택한 데이터에 대 한 자세한 상태 정보를 포함 하는 창 (가운데 창 hello) **범위** 창.</span><span class="sxs-lookup"><span data-stu-id="76073-175">hello **Results** pane (hello center pane) contains detailed status information about hello node, view, or data that you selected in hello **Scope** pane.</span></span>
   * <span data-ttu-id="76073-176">hello **동작** hello 노드, 뷰 또는 hello에서 선택한 데이터에서 수행할 수 있는 hello 작업을 표시 하는 창 **범위** 창.</span><span class="sxs-lookup"><span data-stu-id="76073-176">hello **Actions** pane lists hello operations that you can perform on hello node, view, or data that you selected in hello **Scope** pane.</span></span>
     
     <span data-ttu-id="76073-177">에 대 한 전체 설명은 hello StorSimple 스냅숏 관리자 사용자 인터페이스를 참조 하세요. [StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-177">For a complete description of hello StorSimple Snapshot Manager user interface, see [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
2. <span data-ttu-id="76073-178">Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 hello **장치** 노드를 차례로 클릭 한 다음 **장치 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-178">In hello **Scope** pane, right-click hello **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="76073-179">hello **장치 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="76073-179">hello **Configure a Device** dialog box appears.</span></span>
   
    ![장치 구성](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. <span data-ttu-id="76073-181">Hello에 **장치** 상자, 선택 hello hello Microsoft Azure StorSimple 장치 또는 가상 장치 IP 주소를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-181">In hello **Device** list box, select hello IP address of hello Microsoft Azure StorSimple device or virtual device.</span></span> <span data-ttu-id="76073-182">Hello에 **암호** 텍스트 상자, hello Azure 포털의에서 hello 장치에 대해 만든 형식 hello StorSimple 스냅숏 관리자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="76073-182">In hello **Password** text box, type hello StorSimple Snapshot Manager password that you created for hello device in hello Azure portal.</span></span> <span data-ttu-id="76073-183">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-183">Click **OK**.</span></span>
4. <span data-ttu-id="76073-184">StorSimple 스냅숏 관리자는 식별 된 hello 장치를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-184">StorSimple Snapshot Manager searches for hello device that you identified.</span></span> <span data-ttu-id="76073-185">Hello 장치 표시 되 면 StorSimple 스냅숏 관리자 연결을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-185">If hello device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="76073-186">할 수 있습니다 [hello 연결 toohello 장치 확인](#to-verify-the-connection) 연결 hello tooconfirm 성공적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-186">You can [verify hello connection toohello device](#to-verify-the-connection) tooconfirm that hello connection was added successfully.</span></span>
   
    <span data-ttu-id="76073-187">어떤 이유로 든 hello 장치를 사용할 수 없으면 StorSimple 스냅숏 관리자 오류 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-187">If hello device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="76073-188">클릭 **확인** tooclose hello 오류 메시지 및 클릭 **취소** tooclose hello **장치 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="76073-188">Click **OK** tooclose hello error message, and then click **Cancel** tooclose hello **Configure a Device** dialog box.</span></span>
5. <span data-ttu-id="76073-189">서버에 연결 tooa 장치 StorSimple 스냅숏 관리자 hello 볼륨 그룹에 연결 된 백업이 있는 해당 장치에 대해 구성 된 각 볼륨 그룹을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="76073-189">When it connects tooa device, StorSimple Snapshot Manager imports each volume group configured for that device, provided that hello volume group has associated backups.</span></span> <span data-ttu-id="76073-190">연결된 백업이 없는 볼륨 그룹은 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-190">Volume groups that do not have associated backups are not imported.</span></span> <span data-ttu-id="76073-191">또한 볼륨 그룹에 대해 만든 백업 정책도 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-191">Additionally, backup policies that were created for a volume group are not imported.</span></span> <span data-ttu-id="76073-192">toosee 가져온된 그룹 hello 마우스 오른쪽 단추로 hello 최상위 **볼륨 그룹** hello에 대 한 노드 **범위** 클릭 **가져온된 그룹을 설정/해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-192">toosee hello imported groups, right-click hello top-most **Volume Groups** node in hello **Scope** pane, and click **Toggle imported groups**.</span></span>

### <a name="step-3-verify-hello-connection-toohello-device"></a><span data-ttu-id="76073-193">3 단계: hello 연결 toohello 장치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-193">Step 3: Verify hello connection toohello device</span></span>
<span data-ttu-id="76073-194">StorSimple 스냅숏 관리자 연결된 toohello StorSimple 장치 인지 단계 tooverify 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-194">Use hello following steps tooverify that StorSimple Snapshot Manager is connected toohello StorSimple device.</span></span>

#### <a name="tooverify-hello-connection"></a><span data-ttu-id="76073-195">tooverify hello 연결</span><span class="sxs-lookup"><span data-stu-id="76073-195">tooverify hello connection</span></span>
1. <span data-ttu-id="76073-196">Hello에 **범위** 창의 hello 클릭 **장치** 노드.</span><span class="sxs-lookup"><span data-stu-id="76073-196">In hello **Scope** pane, click hello **Devices** node.</span></span>
   
    ![StorSimple 스냅숏 관리자 장치 상태](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. <span data-ttu-id="76073-198">Hello 확인 **결과** 창:</span><span class="sxs-lookup"><span data-stu-id="76073-198">Check hello **Results** pane:</span></span> 
   
   * <span data-ttu-id="76073-199">Hello 장치 아이콘에 녹색 표시기가 표시 되 고 **사용 가능** hello에 나타납니다 **상태** 열에서 다음 hello 장치가 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-199">If a green indicator appears on hello device icon and **Available** appears in hello **Status** column, then hello device is connected.</span></span> 
   * <span data-ttu-id="76073-200">Hello 장치 아이콘에 빨간색 표시기를 표시 하 고 hello에 사용할 수 없음 표시 **상태** 열에서 다음 hello 장치에 연결 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-200">If a red indicator appears on hello device icon and Unavailable appears in hello **Status** column, then hello device is not connected.</span></span> 
   * <span data-ttu-id="76073-201">경우 **고치** hello에 표시 **상태** 열에 있으면 StorSimple 스냅숏 관리자를 검색 하 고 볼륨 그룹 및 연결된 된 장치에 대 한 연결 된 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="76073-201">If **Refreshing** appears in hello **Status** column, then StorSimple Snapshot Manager is retrieving volume groups and associated backups for a connected device.</span></span>

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a><span data-ttu-id="76073-202">StorSimple 스냅숏 관리자 업그레이드 또는 다시 설치</span><span class="sxs-lookup"><span data-stu-id="76073-202">Upgrade or reinstall StorSimple Snapshot Manager</span></span>
<span data-ttu-id="76073-203">Hello 소프트웨어를 다시 설치 하거나 업그레이드 하기 전에 StorSimple 스냅숏 관리자를 완전히 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-203">You should uninstall StorSimple Snapshot Manager completely before you upgrade or reinstall hello software.</span></span> 

<span data-ttu-id="76073-204">StorSimple 스냅숏 관리자를 다시 설치 하기 전에 hello hello 호스트 컴퓨터에서 기존 StorSimple 스냅숏 관리자 데이터베이스를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-204">Before reinstalling StorSimple Snapshot Manager, back up hello existing StorSimple Snapshot Manager database on hello host computer.</span></span> <span data-ttu-id="76073-205">이 백업에서이 데이터를 쉽게 복원할 수 있도록 hello 백업 정책 및 구성 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-205">This saves hello backup policies and configuration information so that you can easily restore this data from backup.</span></span>

<span data-ttu-id="76073-206">StorSimple 스냅숏 관리자를 업그레이드하거나 다시 설치하는 경우 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="76073-206">Follow these steps if you are upgrading or reinstalling StorSimple Snapshot Manager:</span></span>

* <span data-ttu-id="76073-207">1단계: StorSimple 스냅숏 관리자 제거</span><span class="sxs-lookup"><span data-stu-id="76073-207">Step 1: Uninstall StorSimple Snapshot Manager</span></span> 
* <span data-ttu-id="76073-208">2 단계: hello StorSimple 스냅숏 관리자 데이터베이스를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-208">Step 2: Back up hello StorSimple Snapshot Manager database</span></span> 
* <span data-ttu-id="76073-209">StorSimple 스냅숏 관리자를 다시 설치 하 고 hello 데이터베이스를 복원 하는 3 단계:</span><span class="sxs-lookup"><span data-stu-id="76073-209">Step 3: Reinstall StorSimple Snapshot Manager and restore hello database</span></span> 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a><span data-ttu-id="76073-210">1단계: StorSimple 스냅숏 관리자 제거</span><span class="sxs-lookup"><span data-stu-id="76073-210">Step 1: Uninstall StorSimple Snapshot Manager</span></span>
<span data-ttu-id="76073-211">다음 단계 toouninstall StorSimple 스냅숏 관리자 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-211">Use hello following steps toouninstall StorSimple Snapshot Manager.</span></span>

#### <a name="toouninstall-storsimple-snapshot-manager"></a><span data-ttu-id="76073-212">StorSimple 스냅숏 관리자 toouninstall</span><span class="sxs-lookup"><span data-stu-id="76073-212">toouninstall StorSimple Snapshot Manager</span></span>
1. <span data-ttu-id="76073-213">Hello 호스트 컴퓨터에서 열고 hello **제어판**, 클릭 **프로그램**, 클릭 하 고 **프로그램 및 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-213">On hello host computer, open hello **Control Panel**, click **Programs**, and then click **Programs and Features**.</span></span>
2. <span data-ttu-id="76073-214">Hello 왼쪽된 창에서 클릭 **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-214">In hello left pane, click **Uninstall or change a program**.</span></span>
3. <span data-ttu-id="76073-215">**StorSimple Snapshot Manager**를 마우스 오른쪽 단추로 클릭하고 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-215">Right-click **StorSimple Snapshot Manager**, and then click **Uninstall**.</span></span>
4. <span data-ttu-id="76073-216">Hello StorSimple 스냅숏 관리자 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-216">This starts hello StorSimple Snapshot Manager Setup program.</span></span> <span data-ttu-id="76073-217">**설치 수정**을 클릭하고 **제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-217">Click **Modify Setup**, and then click **Uninstall**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="76073-218">MMC 프로세스가 hello 백그라운드에서 실행 되는, StorSimple 스냅숏 관리자 또는 디스크 관리와 같은 hello 제거 실패 하 고 메시지 tooclose 받습니다 하기 전에 MMC의 모든 인스턴스 toouninstall hello 프로그램을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-218">If there are any MMC processes running in hello background, such as StorSimple Snapshot Manager or Disk Management, hello uninstall will fail and you will receive a message tooclose all instances of MMC before you attempt toouninstall hello program.</span></span> <span data-ttu-id="76073-219">선택 **자동으로 응용 프로그램을 닫고 설치를 한 후에 완료 toorestart**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-219">Select **Automatically close applications and attempt toorestart them after setup is complete**, and then click **OK**.</span></span>
   > 
   > 
5. <span data-ttu-id="76073-220">Hello 제거 프로세스가 완료 되 면 한 **설치 완료** 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="76073-220">When hello uninstall process is finished, a **Setup Successful** message appears.</span></span> <span data-ttu-id="76073-221">**닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-221">Click **Close**.</span></span>

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a><span data-ttu-id="76073-222">2 단계: hello StorSimple 스냅숏 관리자 데이터베이스를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-222">Step 2: Back up hello StorSimple Snapshot Manager database</span></span>
<span data-ttu-id="76073-223">다음 단계 toocreate hello를 사용 하 고 hello StorSimple 스냅숏 관리자 데이터베이스의 복사본을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-223">Use hello following steps toocreate and save a copy of hello StorSimple Snapshot Manager database.</span></span>

#### <a name="tooback-up-hello-database"></a><span data-ttu-id="76073-224">tooback hello 데이터베이스를</span><span class="sxs-lookup"><span data-stu-id="76073-224">tooback up hello database</span></span>
1. <span data-ttu-id="76073-225">Hello Microsoft StorSimple 관리 서비스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-225">Stop hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="76073-226">서버 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-226">Start Server Manager.</span></span>
   2. <span data-ttu-id="76073-227">Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-227">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="76073-228">Hello에 **서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-228">On hello **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="76073-229">Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-229">In hello right pane, under **Microsoft StorSimple Management Service**, click **Stop hello service**.</span></span>
      
        ![Hello StorSimple 장치 관리자 서비스 중지](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. <span data-ttu-id="76073-231">TooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-231">Browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="76073-232">ProgramData는 숨겨진 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76073-232">ProgramData is a hidden folder.</span></span>
  
3. <span data-ttu-id="76073-233">Hello 클라우드 또는 안전한 장소에 hello 카탈로그 XML 파일, 복사 hello 파일 및 저장소 hello 복사본을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-233">Find hello catalog XML file, copy hello file, and store hello copy in a safe location or in hello cloud.</span></span>
   
    ![StorSimple 백업 카탈로그 파일](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. <span data-ttu-id="76073-235">Hello Microsoft StorSimple 관리 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-235">Restart hello Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="76073-236">Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-236">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="76073-237">Hello에 **서비스** 페이지, 선택 hello **Microsoft StorSimple 관리 알림**e입니다.</span><span class="sxs-lookup"><span data-stu-id="76073-237">On hello **Services** page, select hello **Microsoft StorSimple Management Servic**e.</span></span>
   3. <span data-ttu-id="76073-238">Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스를 다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-238">In hello right pane, under **Microsoft StorSimple Management Service**, click **Restart hello service**.</span></span> 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a><span data-ttu-id="76073-239">StorSimple 스냅숏 관리자를 다시 설치 하 고 hello 데이터베이스를 복원 하는 3 단계:</span><span class="sxs-lookup"><span data-stu-id="76073-239">Step 3: Reinstall StorSimple Snapshot Manager and restore hello database</span></span>
<span data-ttu-id="76073-240">StorSimple 스냅숏 관리자 tooreinstall hello 단계에 따라 [새 StorSimple 스냅숏 관리자 설치](#install-a-new-storsimple-snapshot-manager)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-240">tooreinstall StorSimple Snapshot Manager, follow hello steps in [Install a new StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager).</span></span> <span data-ttu-id="76073-241">그런 다음 프로시저 toorestore hello StorSimple 스냅숏 관리자 데이터베이스에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-241">Then, use hello following procedure toorestore hello StorSimple Snapshot Manager database.</span></span>

#### <a name="toorestore-hello-database"></a><span data-ttu-id="76073-242">toorestore hello 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="76073-242">toorestore hello database</span></span>
1. <span data-ttu-id="76073-243">Hello Microsoft StorSimple 관리 서비스를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-243">Stop hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="76073-244">서버 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-244">Start Server Manager.</span></span>
   2. <span data-ttu-id="76073-245">Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-245">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="76073-246">Hello에 **서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-246">On hello **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="76073-247">Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-247">In hello right pane, under **Microsoft StorSimple Management Service**, click **Stop hello service**.</span></span>
2. <span data-ttu-id="76073-248">TooC:\ProgramData\Microsoft\StorSimple\BACatalog를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="76073-248">Browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="76073-249">ProgramData는 숨겨진 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76073-249">ProgramData is a hidden folder.</span></span>
   > 
   > 
3. <span data-ttu-id="76073-250">Hello 카탈로그 XML 파일을 삭제 하 고 이전에 저장 된 hello 버전으로 바꾸십시오.</span><span class="sxs-lookup"><span data-stu-id="76073-250">Delete hello catalog XML file, and replace it with hello version that you saved earlier.</span></span>
4. <span data-ttu-id="76073-251">Hello Microsoft StorSimple 관리 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-251">Restart hello Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="76073-252">Hello에 서버 관리자 대시보드 hello에 **도구** 메뉴 선택 **서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-252">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="76073-253">Hello에 **서비스** 페이지에서 **Microsoft StorSimple 관리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-253">On hello **Services** page, select **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="76073-254">Hello에서 마우스 오른쪽 단추로 창 아래에서 **Microsoft StorSimple 관리 서비스**, 클릭 **hello 서비스를 다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-254">In hello right pane, under **Microsoft StorSimple Management Service**, click **Restart hello service**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76073-255">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76073-255">Next steps</span></span>
* <span data-ttu-id="76073-256">toolearn 더에 대 한 StorSimple 스냅숏 관리자를 너무 이동[StorSimple 스냅숏 관리자 란?](storsimple-what-is-snapshot-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-256">toolearn more about StorSimple Snapshot Manager, go too[What is StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md).</span></span>
* <span data-ttu-id="76073-257">hello StorSimple 스냅숏 관리자 사용자 인터페이스에 대해 자세히 toolearn 너무 이동[StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-257">toolearn more about hello StorSimple Snapshot Manager user interface, go too[StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
* <span data-ttu-id="76073-258">StorSimple 스냅숏 관리자 사용에 대 한 더 toolearn 너무 이동[StorSimple 스냅숏 관리자를 사용 하 여 tooadminister StorSimple 솔루션](storsimple-snapshot-manager-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76073-258">toolearn more about using StorSimple Snapshot Manager, go too[Use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>

