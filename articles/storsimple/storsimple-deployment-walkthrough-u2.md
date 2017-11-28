---
title: "aaaDeploy StorSimple 장치 (업데이트 2) | Microsoft Docs"
description: "Hello 단계와 hello StorSimple 업데이트 2 장치 및 서비스를 배포 하기 위한 모범 사례를 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7dff0612-617b-4fc8-a3fe-994c24bc7c51
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: 5906cc3c41f03c426905ef91be37852608ae9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-2"></a><span data-ttu-id="7f018-103">온-프레미스 StorSimple 장치(업데이트 2) 배포</span><span class="sxs-lookup"><span data-stu-id="7f018-103">Deploy your on-premises StorSimple device (Update 2)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f018-104">업데이트 2 이상</span><span class="sxs-lookup"><span data-stu-id="7f018-104">Update 2 & later </span></span>](storsimple-deployment-walkthrough-u2.md)
> * [<span data-ttu-id="7f018-105">업데이트 1</span><span class="sxs-lookup"><span data-stu-id="7f018-105">Update 1</span></span>](storsimple-deployment-walkthrough-u1.md)
> * [<span data-ttu-id="7f018-106">GA 릴리스</span><span class="sxs-lookup"><span data-stu-id="7f018-106">GA Release</span></span>](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7f018-107">개요</span><span class="sxs-lookup"><span data-stu-id="7f018-107">Overview</span></span>
<span data-ttu-id="7f018-108">TooMicrosoft Azure StorSimple 장치 배포를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-108">Welcome tooMicrosoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="7f018-109">이러한 배포 자습서 적용 tooStorSimple 8000 시리즈 업데이트 2입니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-109">These deployment tutorials apply tooStorSimple 8000 Series Update 2.</span></span> <span data-ttu-id="7f018-110">이 자습서 시리즈에서는 StorSimple 장치를 구성하는 방법에 대해 설명하며 구성 검사 목록, 구성 필수 조건 및 자세한 구성 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-110">This series of tutorials includes a configuration checklist, configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="7f018-111">이 자습서에 hello 정보 hello 안전 조치 검토 하 고 압축을 풀, racked, 고 StorSimple 장치를 케이블로 연결를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-111">hello information in these tutorials assumes that you have reviewed hello safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="7f018-112">검토 hello로 시작 하는 작업 tooperform를 여전히 필요 하면 [안전 조치](storsimple-safety.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-112">If you still need tooperform those tasks, start with reviewing hello [safety precautions](storsimple-safety.md).</span></span> <span data-ttu-id="7f018-113">Hello 장치 특정 지침 toounpack, 랙 마운트, 및 장치 케이블 연결을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-113">Follow hello device specific instructions toounpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="7f018-114">8100 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="7f018-114">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="7f018-115">8600 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="7f018-115">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="7f018-116">관리자는 권한이 toocomplete hello 설정 및 구성 프로세스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-116">You will need administrator privileges toocomplete hello setup and configuration process.</span></span> <span data-ttu-id="7f018-117">시작 하기 전에 hello 구성 검사 목록 검토 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-117">We recommend that you review hello configuration checklist before you begin.</span></span> <span data-ttu-id="7f018-118">hello 배포 및 구성 프로세스는 몇 시간 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-118">hello deployment and configuration process can take some time toocomplete.</span></span>

> [!NOTE]
> <span data-ttu-id="7f018-119">hello Microsoft Azure 웹 사이트에 게시 된 StorSimple 배포 정보를 hello tooStorSimple 8000 시리즈 장치에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-119">hello StorSimple deployment information published on hello Microsoft Azure website applies tooStorSimple 8000 series devices only.</span></span> <span data-ttu-id="7f018-120">Hello 7000 시리즈 장치에 대 한 자세한 내용은 이동: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-120">For complete information about hello 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="7f018-121">7000 시리즈 배포 정보에 대 한 참조 hello [StorSimple 시스템 빠른 시작 가이드](http://onlinehelp.storsimple.com/111_Appliance/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-121">For 7000 series deployment information, see hello [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span>
> 
> 

## <a name="deployment-steps"></a><span data-ttu-id="7f018-122">배포 단계</span><span class="sxs-lookup"><span data-stu-id="7f018-122">Deployment steps</span></span>
<span data-ttu-id="7f018-123">이러한 단계가 tooconfigure StorSimple 장치 성능과 tooyour StorSimple Manager 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-123">Perform these required steps tooconfigure your StorSimple device and connect it tooyour StorSimple Manager service.</span></span> <span data-ttu-id="7f018-124">또한 toohello 필요한 단계를 가지는 선택적 단계와 절차가 hello 배포 하는 동안 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-124">In addition toohello required steps, there are optional steps and procedures you may need during hello deployment.</span></span> <span data-ttu-id="7f018-125">hello 단계별 배포 지침은 각 선택적 단계를 수행 해야 하는 시기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-125">hello step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="7f018-126">단계</span><span class="sxs-lookup"><span data-stu-id="7f018-126">Step</span></span> | <span data-ttu-id="7f018-127">설명</span><span class="sxs-lookup"><span data-stu-id="7f018-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f018-128">**필수 조건**</span><span class="sxs-lookup"><span data-stu-id="7f018-128">**PREREQUISITES**</span></span> |<span data-ttu-id="7f018-129">이러한 toobe hello 향후 배포 준비 과정에서 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-129">These need toobe completed in preparation for hello upcoming deployment.</span></span> |
| [<span data-ttu-id="7f018-130">배포 구성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="7f018-130">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="7f018-131">Hello 배포 하는 동안이 검사 목록 toogather 및 기록 정보 이전 tooand를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-131">Use this checklist toogather and record information prior tooand during hello deployment.</span></span> |
| [<span data-ttu-id="7f018-132">배포 필수 조건</span><span class="sxs-lookup"><span data-stu-id="7f018-132">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="7f018-133">Hello의 유효성을 검사 하는 이러한 환경에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-133">These  validate hello environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="7f018-134">**단계별 배포**</span><span class="sxs-lookup"><span data-stu-id="7f018-134">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="7f018-135">이러한 단계는 필요한 toodeploy 프로덕션 환경에서 StorSimple 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-135">These steps are required toodeploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="7f018-136">1단계: 새 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7f018-136">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="7f018-137">StorSimple 장치에 대한 클라우드 관리 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-137">Set up cloud management and storage for your   StorSimple device.</span></span> <span data-ttu-id="7f018-138">*다른 StorSimple 장치에 대해 기존 서비스가 있는 경우 이 단계를 건너뜁니다*.</span><span class="sxs-lookup"><span data-stu-id="7f018-138">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="7f018-139">2 단계: hello 서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f018-139">Step 2: Get hello service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="7f018-140">이 키 tooregister를 사용 하 여 & hello 관리 서비스와 StorSimple 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-140">Use this key tooregister & connect your StorSimple device with hello management service.</span></span> |
| [<span data-ttu-id="7f018-141">3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치 등록</span><span class="sxs-lookup"><span data-stu-id="7f018-141">Step 3: Configure and register hello device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="7f018-142">Hello 장치 tooyour 네트워크를 연결 하 고 Azure toocomplete hello hello 관리 서비스를 사용 하 여 설치 프로그램을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-142">Connect hello device tooyour network and register it with Azure toocomplete hello setup using hello management service.</span></span> |
| [<span data-ttu-id="7f018-143">4단계: 최소 장치 설정 완료</span><span class="sxs-lookup"><span data-stu-id="7f018-143">Step 4: Complete minimum device setup</span></span>](#step-4-complete-minimum-device-setup)</br>[<span data-ttu-id="7f018-144">선택 사항: StorSimple 장치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-144">Optional: Update your StorSimple device</span></span>](#scan-for-and-apply-updates) |<span data-ttu-id="7f018-145">Hello 관리 서비스 toocomplete hello 장치 설치 프로그램을 사용 하 고 tooprovide 저장을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-145">Use hello management service toocomplete hello device setup and enable it tooprovide storage.</span></span> |
| [<span data-ttu-id="7f018-146">5단계: 볼륨 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="7f018-146">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="7f018-147">Tooprovision 볼륨 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-147">Create a container tooprovision volumes.</span></span> <span data-ttu-id="7f018-148">볼륨 컨테이너는 저장소 계정, 대역폭 및 암호화 설정에 포함 된 모든 hello 볼륨에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-148">A volume container has storage   account, bandwidth, and encryption settings for all hello volumes contained in it.</span></span> |
| [<span data-ttu-id="7f018-149">6단계: 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="7f018-149">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="7f018-150">서버에 대 한 hello StorSimple 장치에 대 한 저장소 볼륨을 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-150">Provision storage volume(s) on hello StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="7f018-151">7단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="7f018-151">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume)</br>[<span data-ttu-id="7f018-152">선택 사항: MPIO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-152">Optional: Configure MPIO</span></span>](storsimple-configure-mpio-windows-server.md) |<span data-ttu-id="7f018-153">Hello 장치에서 제공 하 여 서버 toohello iSCSI 저장소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-153">Connect your servers toohello iSCSI storage provided by hello device.</span></span> <span data-ttu-id="7f018-154">필요에 따라 MPIO tooensure 서버 링크, 네트워크 및 인터페이스 발생 한 오류를 허용할 수 있는지를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-154">Optionally configure MPIO tooensure that your servers can tolerate link, network and interface failure.</span></span> |
| [<span data-ttu-id="7f018-155">8단계: 백업 수행</span><span class="sxs-lookup"><span data-stu-id="7f018-155">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="7f018-156">백업 정책 tooprotect 데이터 설정</span><span class="sxs-lookup"><span data-stu-id="7f018-156">Set up your backup policy tooprotect your data</span></span> |
|  | |
| <span data-ttu-id="7f018-157">**기타 절차**</span><span class="sxs-lookup"><span data-stu-id="7f018-157">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="7f018-158">솔루션을 배포 하는 경우 toorefer toothese 프로시저를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-158">You may need toorefer toothese procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="7f018-159">Hello 서비스에 대 한 새 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="7f018-159">Configure a new storage account for hello service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="7f018-160">PuTTY tooconnect toohello 장치 직렬 콘솔을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7f018-160">Use PuTTY tooconnect toohello device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="7f018-161">Hello Windows Server 호스트의 IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f018-161">Get hello IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="7f018-162">수동 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="7f018-162">Create a manual backup</span></span>](#create-a-manual-backup) | |

## <a name="deployment-configuration-checklist"></a><span data-ttu-id="7f018-163">배포 구성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="7f018-163">Deployment configuration checklist</span></span>
<span data-ttu-id="7f018-164">장치를 배포 하기 전에 toocollect 정보 tooconfigure hello 소프트웨어 StorSimple 장치에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-164">Before you deploy your device, you will need toocollect information tooconfigure hello software on your StorSimple device.</span></span> <span data-ttu-id="7f018-165">사전에이 정보 중 일부를 준비 하 고 사용자 환경에서 hello StorSimple 장치 배포의 hello 과정을 간소화 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-165">Preparing some of this information ahead of time will help streamline hello process of deploying hello StorSimple device in your environment.</span></span> <span data-ttu-id="7f018-166">다운로드 하 고 장치를 배포 하는 경우이 검사 목록 toonote hello 구성 세부 정보를 사용 하 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-166">Download and use this checklist toonote down hello configuration details as you deploy your device.</span></span>

* [<span data-ttu-id="7f018-167">StorSimple 배포 구성 검사 목록 다운로드</span><span class="sxs-lookup"><span data-stu-id="7f018-167">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a><span data-ttu-id="7f018-168">배포 필수 조건</span><span class="sxs-lookup"><span data-stu-id="7f018-168">Deployment prerequisites</span></span>
<span data-ttu-id="7f018-169">hello 다음 섹션에서는 StorSimple Manager 서비스 및 StorSimple 장치에 대 한 hello 구성 필수 구성 요소에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-169">hello following sections explain hello configuration prerequisites for your StorSimple Manager service and your StorSimple device.</span></span>

### <a name="for-hello-storsimple-manager-service"></a><span data-ttu-id="7f018-170">Hello StorSimple Manager 서비스에 대 한</span><span class="sxs-lookup"><span data-stu-id="7f018-170">For hello StorSimple Manager service</span></span>
<span data-ttu-id="7f018-171">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-171">Before you begin, make sure that:</span></span>

* <span data-ttu-id="7f018-172">액세스 자격 증명이 있는 Microsoft 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-172">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="7f018-173">액세스 자격 증명이 있는 Microsoft Azure 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-173">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="7f018-174">Microsoft Azure 구독의 hello StorSimple Manager 서비스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-174">Your Microsoft Azure subscription is enabled for hello StorSimple Manager service.</span></span> <span data-ttu-id="7f018-175">Hello를 통해 구독을 구입 해야 [기업 계약](https://azure.microsoft.com/pricing/enterprise-agreement/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-175">Your subscription should be purchased through hello [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="7f018-176">PuTTY와 같은 액세스 tooterminal 에뮬레이션 소프트웨어를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-176">You have access tooterminal emulation software such as PuTTY.</span></span>

### <a name="for-hello-device-in-hello-datacenter"></a><span data-ttu-id="7f018-177">Hello 데이터 센터에서 hello 장치에 대 한</span><span class="sxs-lookup"><span data-stu-id="7f018-177">For hello device in hello datacenter</span></span>
<span data-ttu-id="7f018-178">Hello 장치를 구성 하기 전에 장치 및 되어 있는지 완전히 포장을 푼, 랙 탑재를 전원, 네트워크 및 직렬 액세스에 설명 된 대로 완전 하 게 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-178">Before configuring hello device, make sure that your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>

* [<span data-ttu-id="7f018-179">8100 장치 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="7f018-179">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="7f018-180">8600 장치 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="7f018-180">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a><span data-ttu-id="7f018-181">Hello 네트워크 hello 데이터 센터에 대 한</span><span class="sxs-lookup"><span data-stu-id="7f018-181">For hello network in hello datacenter</span></span>
<span data-ttu-id="7f018-182">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-182">Before you begin, make sure that:</span></span>

* <span data-ttu-id="7f018-183">hello 데이터 센터 방화벽에서 포트는 iSCSI 및 클라우드 트래픽에 대 한 열린된 tooallow에 설명 된 대로 [StorSimple 장치의 네트워킹 요구 사항](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-183">hello ports in your datacenter firewall are opened tooallow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="7f018-184">단계별 배포</span><span class="sxs-lookup"><span data-stu-id="7f018-184">Step-by-step deployment</span></span>
<span data-ttu-id="7f018-185">Hello 데이터 센터에 대 한 단계별 지침 toodeploy 다음 hello StorSimple 장치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-185">Use hello following step-by-step instructions toodeploy your StorSimple device in hello datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="7f018-186">1단계: 새 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="7f018-186">Step 1: Create a new service</span></span>
<span data-ttu-id="7f018-187">StorSimple 관리자 서비스는 여러 StorSimple 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-187">A StorSimple Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="7f018-188">Hello 단계 toocreate hello StorSimple 관리자 서비스의 새 인스턴스를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-188">Perform hello following steps toocreate a new instance of hello StorSimple Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="7f018-189">Toocreate 할 서비스와 저장소 계정의 hello 자동 생성을 설정 하지 않은 경우 저장소 계정을 하나 이상 후 서비스를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-189">If you did not enable hello automatic creation of a storage account with your service, you will need toocreate at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="7f018-190">이 저장소 계정은 볼륨 컨테이너를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-190">This storage account will be used when you create a volume container.</span></span> 
> 
> * <span data-ttu-id="7f018-191">저장소 계정을 자동으로 만들 하지 않은 경우 너무 이동[hello 서비스에 대 한 새 저장소 계정 구성](#configure-a-new-storage-account-for-the-service) 자세한 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-191">If you did not create a storage account automatically, go too[Configure a new storage account for hello service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span> 
> * <span data-ttu-id="7f018-192">저장소 계정의 hello 자동 생성을 사용 하도록 설정한 경우 너무 이동[2 단계: Get hello 서비스 등록 키](#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-192">If you enabled hello automatic creation of a storage account, go too[Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a><span data-ttu-id="7f018-193">2 단계: hello 서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f018-193">Step 2: Get hello service registration key</span></span>
<span data-ttu-id="7f018-194">Hello StorSimple Manager 서비스가 실행 되 고, tooget hello 서비스 등록 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-194">After hello StorSimple Manager service is up and running, you will need tooget hello service registration key.</span></span> <span data-ttu-id="7f018-195">이 키가 사용 되는 tooregister를 hello 서비스와 StorSimple 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-195">This key is used tooregister and connect your StorSimple device with hello service.</span></span>

<span data-ttu-id="7f018-196">Hello hello 관리 포털에서에서 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-196">Perform hello following steps in hello Management Portal.</span></span>

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="7f018-197">3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치 등록</span><span class="sxs-lookup"><span data-stu-id="7f018-197">Step 3: Configure and register hello device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7f018-198">Hello 절차 다음에 설명 된 대로 StorSimple 장치의 StorSimple toocomplete hello 초기 설치에 대 한 Windows PowerShell을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-198">Use Windows PowerShell for StorSimple toocomplete hello initial setup of your StorSimple device as explained in hello following procedure.</span></span> <span data-ttu-id="7f018-199">Toouse 터미널 에뮬레이션 소프트웨어 toocomplete이이 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-199">You will need toouse terminal emulation software toocomplete this step.</span></span> <span data-ttu-id="7f018-200">자세한 내용은 참조 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-200">For more information, see [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="7f018-201">4단계: 최소 장치 설정 완료</span><span class="sxs-lookup"><span data-stu-id="7f018-201">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="7f018-202">StorSimple 장치의 최소 장치 구성을 hello에 대 한 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-202">For hello minimum device configuration of your StorSimple device, you are required to:</span></span> 

* <span data-ttu-id="7f018-203">Hello 보조 DNS 서버를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-203">Set up hello secondary DNS server.</span></span>
* <span data-ttu-id="7f018-204">하나 이상의 네트워크 인터페이스에서 iSCSI를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-204">Enable iSCSI on at least one network interface.</span></span>
* <span data-ttu-id="7f018-205">Tooboth hello 컨트롤러 고정된 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-205">Assign fixed IP addresses tooboth hello controllers.</span></span>

<span data-ttu-id="7f018-206">Hello hello 관리 포털 toocomplete hello 최소 장치 설치에서 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-206">Perform hello following steps in hello Management Portal toocomplete hello minimum device setup.</span></span>

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="7f018-207">5단계: 볼륨 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="7f018-207">Step 5: Create a volume container</span></span>
<span data-ttu-id="7f018-208">볼륨 컨테이너는 저장소 계정, 대역폭 및 암호화 설정에 포함 된 모든 hello 볼륨에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-208">A volume container has storage account, bandwidth, and encryption settings for all hello volumes contained in it.</span></span> <span data-ttu-id="7f018-209">StorSimple 장치에서 볼륨 프로비저닝을 시작 하려면 먼저 볼륨 컨테이너 toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-209">You will need toocreate a volume container before you can start provisioning volumes on your StorSimple device.</span></span> 

<span data-ttu-id="7f018-210">Hello hello 관리 포털 toocreate 볼륨 컨테이너에서에서 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-210">Perform hello following steps in hello Management Portal toocreate a volume container.</span></span>

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="7f018-211">6단계: 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="7f018-211">Step 6: Create a volume</span></span>
<span data-ttu-id="7f018-212">볼륨 컨테이너를 만든 후에 서버에 대 한 hello StorSimple 장치에서 저장소 볼륨을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-212">After you create a volume container, you can provision a storage volume on hello StorSimple device for your servers.</span></span> <span data-ttu-id="7f018-213">Hello hello 관리 포털 toocreate 볼륨의에서 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-213">Perform hello following steps in hello Management Portal toocreate a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f018-214">StorSimple 관리자는 씬 프로비전된 볼륨과 완전히 프로비전된 볼륨을 둘 다 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-214">StorSimple Manager can create both thin and fully provisioned volumes.</span></span> <span data-ttu-id="7f018-215">그러나 부분적으로 프로비전된 볼륨은 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-215">You cannot however create partially provisioned volumes.</span></span> 
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="7f018-216">7단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="7f018-216">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="7f018-217">단계를 수행 하는 hello Windows Server 호스트에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-217">hello following steps are performed on your Windows Server host.</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="7f018-218">StorSimple 솔루션의 고가용성을 hello 위해 호스트 서버 (선택 사항) 이전 tooconfiguring iSCSI에서 MPIO를 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-218">For hello high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior tooconfiguring iSCSI.</span></span> <span data-ttu-id="7f018-219">호스트 서버에 MPIO 구성 링크, 네트워크 또는 인터페이스 오류 hello 서버 허용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-219">MPIO configuration on host servers will ensure that hello servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="7f018-220">에 대 한 iSCSI 및 MPIO 설치 및 구성 지침은 Windows Server 호스트를 이동 너무[StorSimple 장치에 대 한 MPIO 구성](storsimple-configure-mpio-windows-server.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-220">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go too[Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="7f018-221">이러한 hello 단계 toomount 포함, 초기화 및도 StorSimple 볼륨을 포맷 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-221">These will also include hello steps toomount, initialize and format StorSimple volumes.</span></span>
> * <span data-ttu-id="7f018-222">에 대 한 iSCSI 및 MPIO 설치 및 구성 지침은 Linux 호스트를 이동 너무[StorSimple Linux 호스트에 대 한 MPIO 구성](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="7f018-222">For MPIO and iSCSI installation and configuration instructions on a Linux host, go too[Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>
> 
> 

<span data-ttu-id="7f018-223">Hello 단계 toomount 다음을 수행 하지 tooconfigure MPIO를 결정 하는 경우 초기화 및 Windows Server 호스트에 StorSimple 볼륨을 포맷 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-223">If you decide not tooconfigure MPIO, perform hello following steps toomount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="7f018-224">8단계: 백업 수행</span><span class="sxs-lookup"><span data-stu-id="7f018-224">Step 8: Take a backup</span></span>
<span data-ttu-id="7f018-225">백업은 볼륨의 지정 시간 보호 기능을 제공하며 복원 시간을 최소화하면서 복구 기능을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-225">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="7f018-226">StorSimple 장치에서 두 유형(로컬 스냅숏 및 클라우드 스냅숏)의 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-226">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="7f018-227">이러한 각 유형의 백업은 **예약됨** 또는 **수동**이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-227">Each of these backup types can be **Scheduled** or **Manual**.</span></span> 

<span data-ttu-id="7f018-228">Hello hello 관리 포털 toocreate 예약된 된 백업에서에서 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-228">Perform hello following steps in hello Management Portal toocreate a scheduled backup.</span></span>

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

<span data-ttu-id="7f018-229">언제든지 수동 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-229">You can take a manual backup at any time.</span></span> <span data-ttu-id="7f018-230">너무 절차를 보려면[수동 백업 만들기](#create-a-manual-backup)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-230">For procedures, go too[Create a manual backup](#create-a-manual-backup).</span></span> 

## <a name="configure-a-new-storage-account-for-hello-service"></a><span data-ttu-id="7f018-231">Hello 서비스에 대 한 새 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="7f018-231">Configure a new storage account for hello service</span></span>
<span data-ttu-id="7f018-232">이것이 서비스와 저장소 계정의 hello 자동 만들기를 활성화 하지 않은 경우에 tooperform를 필요한 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-232">This is an optional step that you need tooperform only if you did not enable hello automatic creation of a storage account with your service.</span></span> <span data-ttu-id="7f018-233">Microsoft Azure 저장소 계정에 필요한 toocreate StorSimple 볼륨 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-233">A Microsoft Azure storage account is required toocreate a StorSimple volume container.</span></span>

<span data-ttu-id="7f018-234">Toocreate Azure 저장소 계정을 다른 지역에 필요한 경우 참조 [Azure 저장소 계정에 대 한](../storage/common/storage-create-storage-account.md) 단계별 지침.</span><span class="sxs-lookup"><span data-stu-id="7f018-234">If you need toocreate an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="7f018-235">Hello에 hello 관리 포털의에서 단계를 실행 하는 hello 수행 **StorSimple Manager 서비스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7f018-235">Perform hello following steps in hello Management Portal, on hello **StorSimple Manager service** page.</span></span>

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a><span data-ttu-id="7f018-236">PuTTY tooconnect toohello 장치 직렬 콘솔을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7f018-236">Use PuTTY tooconnect toohello device serial console</span></span>
<span data-ttu-id="7f018-237">tooconnect tooWindows StorSimple 용 PowerShell PuTTY와 같은 터미널 에뮬레이션 소프트웨어 toouse 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-237">tooconnect tooWindows PowerShell for StorSimple, you need toouse terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="7f018-238">Hello 직렬 콘솔을 통해 직접 또는 원격 컴퓨터에서 텔넷 세션을 열어 hello 장치에 액세스할 때에 PuTTY를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-238">You can use PuTTY when you access hello device directly through hello serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="7f018-239">업데이트 검색 및 적용</span><span class="sxs-lookup"><span data-stu-id="7f018-239">Scan for and apply updates</span></span>
<span data-ttu-id="7f018-240">장치 업데이트는 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-240">Updating your device can take several hours.</span></span> <span data-ttu-id="7f018-241">Hello에 대 한 단계 tooscan 다음을 수행 하 고 장치에서 업데이트를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-241">Perform hello following steps tooscan for and apply updates on your device.</span></span>
<!--can take 1-4 hours--> 

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a><span data-ttu-id="7f018-242">tooupdate 장치</span><span class="sxs-lookup"><span data-stu-id="7f018-242">tooupdate your device</span></span>
1. <span data-ttu-id="7f018-243">Hello 장치에서 **빠른 시작** 페이지 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-243">On hello device **Quick Start** page, click **Devices**.</span></span> <span data-ttu-id="7f018-244">Hello 물리적 장치를 선택를 클릭 **유지 관리** 클릭 하 고 **업데이트 스캔**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-244">Select hello physical device, click **Maintenance** and then click **Scan Updates**.</span></span>  
2. <span data-ttu-id="7f018-245">사용 가능한 업데이트에 대 한 작업 tooscan 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-245">A job tooscan for available updates is created.</span></span> <span data-ttu-id="7f018-246">사용 가능한 업데이트가 있으면 hello **업데이트 검색** 쪽 변경**업데이트 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-246">If updates are available, hello **Scan Updates** changes too**Install Updates**.</span></span> <span data-ttu-id="7f018-247">**업데이트 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-247">Click **Install Updates**.</span></span> 
3. <span data-ttu-id="7f018-248">업데이트 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-248">An update job will be created.</span></span> <span data-ttu-id="7f018-249">너무 이동 하 여 업데이트의 hello 상태를 모니터링**작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-249">Monitor hello status of your update by navigating too**Jobs**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7f018-250">Hello 업데이트 작업이 시작 되 면 50%로 즉시 hello 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-250">When hello update job starts, it immediately displays hello status as 50 percent.</span></span> <span data-ttu-id="7f018-251">hello 상태 hello 업데이트 작업이 완료 된 후에 too100 비율을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-251">hello status changes too100 percent only after hello update job is complete.</span></span> <span data-ttu-id="7f018-252">Hello 업데이트 프로세스에 대 한 실시간 상태가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-252">There is no real-time status for hello update process.</span></span>
   > 
   > 
4. <span data-ttu-id="7f018-253">Hello 장치를 업데이트 후 이러한 비활성화 된 경우 데이터 2 및 Data 3 네트워크 인터페이스가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-253">After hello device is successfully updated, enable Data 2 and Data 3 network interfaces if these were disabled.</span></span>

<!-- In step 2, you may be requested toodisable Data 2 and Data 3 prior tooinstalling hello updates. You must disable these network interfaces or hello updates may fail.-->

## <a name="get-hello-iqn-of-a-windows-server-host"></a><span data-ttu-id="7f018-254">Hello Windows Server 호스트의 IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="7f018-254">Get hello IQN of a Windows Server host</span></span>
<span data-ttu-id="7f018-255">다음 단계 tooget hello iSCSI hello 수행 정규화 된 이름 (IQN) Windows Server® 2012를 실행 중인 Windows 호스트의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-255">Perform hello following steps tooget hello iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="7f018-256">수동 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="7f018-256">Create a manual backup</span></span>
<span data-ttu-id="7f018-257">StorSimple 장치에서 단일 볼륨에 대 한 hello 관리 포털 toocreate 주문형 수동 백업 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-257">Perform hello following steps in hello Management Portal toocreate an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="7f018-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7f018-258">Next steps</span></span>
* <span data-ttu-id="7f018-259">[가상 장치](storsimple-virtual-device-u2.md)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-259">Configure a [virtual device](storsimple-virtual-device-u2.md).</span></span>
* <span data-ttu-id="7f018-260">사용 하 여 hello [StorSimple Manager 서비스](storsimple-manager-service-administration.md) toomanage StorSimple 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="7f018-260">Use hello [StorSimple Manager service](storsimple-manager-service-administration.md) toomanage your StorSimple device.</span></span>

