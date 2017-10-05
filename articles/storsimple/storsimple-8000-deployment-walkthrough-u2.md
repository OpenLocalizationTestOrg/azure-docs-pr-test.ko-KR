---
title: "Azure Portal에서 StorSimple 8000 시리즈 장치 배포 | Microsoft Docs"
description: "업데이트 3 이상을 실행하는 StorSimple 8000 시리즈 장치 및 StorSimple 장치 관리자 서비스를 배포하기 위한 단계와 모범 사례를 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3d2023c3e129cfdea27f343a41b3cc373c0c3b8f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-3-and-later"></a><span data-ttu-id="d4547-103">온-프레미스 StorSimple 장치(업데이트 3 이상) 배포</span><span class="sxs-lookup"><span data-stu-id="d4547-103">Deploy your on-premises StorSimple device (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="d4547-104">개요</span><span class="sxs-lookup"><span data-stu-id="d4547-104">Overview</span></span>
<span data-ttu-id="d4547-105">Microsoft Azure StorSimple 장치 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-105">Welcome to Microsoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="d4547-106">이러한 배포 자습서는 StorSimple 8000 시리즈 업데이트 3 이상에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-106">These deployment tutorials apply to StorSimple 8000 Series Update 3 or later.</span></span> <span data-ttu-id="d4547-107">이 자습서 시리즈에서는 StorSimple 장치를 구성하는 방법에 대해 설명하며 구성 검사 목록, 구성 필수 조건 및 자세한 구성 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-107">This series of tutorials includes a configuration checklist, configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="d4547-108">이 자습서의 정보는 안전 주의 사항을 검토했으며, StorSimple 장치의 포장을 풀었고, 랙을 탑재했으며, 케이블에 연결되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-108">The information in these tutorials assumes that you have reviewed the safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="d4547-109">여전히 이러한 작업을 수행해야 하는 경우 [안전 주의 사항](storsimple-8000-safety.md)검토로 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="d4547-109">If you still need to perform those tasks, start with reviewing the [safety precautions](storsimple-8000-safety.md).</span></span> <span data-ttu-id="d4547-110">장치를 개봉, 랙 탑재 및 케이블로 연결하려면 장치별 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-110">Follow the device-specific instructions to unpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="d4547-111">8100 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="d4547-111">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="d4547-112">8600 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="d4547-112">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="d4547-113">설치 및 구성 프로세스를 완료하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-113">You need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="d4547-114">시작하기 전에 구성 검사 목록을 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-114">We recommend that you review the configuration checklist before you begin.</span></span> <span data-ttu-id="d4547-115">배포 및 구성 프로세스는 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-115">The deployment and configuration process can take some time to complete.</span></span>

> [!NOTE]
> <span data-ttu-id="d4547-116">Microsoft Azure 웹 사이트에 게시된 StorSimple 배포 정보는 StorSimple 8000 시리즈 장치에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-116">The StorSimple deployment information published on the Microsoft Azure website applies to StorSimple 8000 series devices only.</span></span> <span data-ttu-id="d4547-117">7000 시리즈 장치에 대한 자세한 내용은 [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-117">For complete information about the 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="d4547-118">7000 시리즈 배포 정보는 [StorSimple 시스템 퀵 스타트 가이드](http://onlinehelp.storsimple.com/111_Appliance/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4547-118">For 7000 series deployment information, see the [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span> 


## <a name="deployment-steps"></a><span data-ttu-id="d4547-119">배포 단계</span><span class="sxs-lookup"><span data-stu-id="d4547-119">Deployment steps</span></span>
<span data-ttu-id="d4547-120">StorSimple 장치를 구성하여 StorSimple 장치 관리자 서비스에 연결하려면 다음과 같은 필수 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-120">Perform these required steps to configure your StorSimple device and connect it to your StorSimple Device Manager service.</span></span> <span data-ttu-id="d4547-121">필수 단계 외에 선택적 단계 및 배포하는 동안 필요할 수도 있는 절차가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-121">In addition to the required steps, there are optional steps and procedures you may need during the deployment.</span></span> <span data-ttu-id="d4547-122">단계별 배포 지침은 각 선택적 단계를 수행해야 하는 시기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-122">The step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="d4547-123">단계</span><span class="sxs-lookup"><span data-stu-id="d4547-123">Step</span></span> | <span data-ttu-id="d4547-124">설명</span><span class="sxs-lookup"><span data-stu-id="d4547-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4547-125">**필수 조건**</span><span class="sxs-lookup"><span data-stu-id="d4547-125">**PREREQUISITES**</span></span> |<span data-ttu-id="d4547-126">향후 배포 준비 과정에서 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-126">These must be completed in preparation for the upcoming deployment.</span></span> |
| [<span data-ttu-id="d4547-127">배포 구성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="d4547-127">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="d4547-128">이 검사 목록을 사용하여 배포 이전 및 배포하는 동안 정보를 수집하고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-128">Use this checklist to gather and record information before and during the deployment.</span></span> |
| [<span data-ttu-id="d4547-129">배포 필수 조건</span><span class="sxs-lookup"><span data-stu-id="d4547-129">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="d4547-130">배포할 준비가 되어 있는 환경인지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-130">These validate the environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="d4547-131">**단계별 배포**</span><span class="sxs-lookup"><span data-stu-id="d4547-131">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="d4547-132">프로덕션 환경에서 StorSimple 장치를 배포하려면 다음 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-132">These steps are required to deploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="d4547-133">1단계: 새 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="d4547-133">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="d4547-134">StorSimple 장치에 대한 클라우드 관리 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-134">Set up cloud management and storage for your StorSimple device.</span></span> <span data-ttu-id="d4547-135">*다른 StorSimple 장치에 대해 기존 서비스가 있는 경우 이 단계를 건너뜁니다*.</span><span class="sxs-lookup"><span data-stu-id="d4547-135">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="d4547-136">2단계: 서비스 등록 키 받기</span><span class="sxs-lookup"><span data-stu-id="d4547-136">Step 2: Get the service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="d4547-137">이 키를 사용하여 StorSimple 장치를 관리 서비스에 등록 및 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-137">Use this key to register & connect your StorSimple device with the management service.</span></span> |
| [<span data-ttu-id="d4547-138">3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록</span><span class="sxs-lookup"><span data-stu-id="d4547-138">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="d4547-139">관리 서비스를 사용하여 설정을 완료하려면 장치를 네트워크에 연결하고 Azure로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-139">To complete the setup using the management service, connect the device to your network and register it with Azure.</span></span> |
| [<span data-ttu-id="d4547-140">4단계: 최소 장치 설정 완료</span><span class="sxs-lookup"><span data-stu-id="d4547-140">Step 4: Complete minimum device setup</span></span>](#step-4-complete-minimum-device-setup)</br>[<span data-ttu-id="d4547-141">선택 사항: StorSimple 장치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-141">Optional: Update your StorSimple device</span></span>](#scan-for-and-apply-updates) |<span data-ttu-id="d4547-142">관리 서비스를 사용하여 장치 설정을 완료하고 저장소를 제공할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-142">Use the management service to complete the device setup and enable it to provide storage.</span></span> |
| [<span data-ttu-id="d4547-143">5단계: 볼륨 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="d4547-143">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="d4547-144">볼륨을 프로비전할 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-144">Create a container to provision volumes.</span></span> <span data-ttu-id="d4547-145">볼륨 컨테이너에는 저장소 계정, 대역폭 및 그 안에 포함된 모든 볼륨에 대한 암호화 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-145">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> |
| [<span data-ttu-id="d4547-146">6단계: 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="d4547-146">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="d4547-147">서버에 대한 StorSimple 장치의 저장소 볼륨을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-147">Provision storage volumes on the StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="d4547-148">7단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="d4547-148">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume)</br>[<span data-ttu-id="d4547-149">선택 사항: MPIO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-149">Optional: Configure MPIO</span></span>](storsimple-8000-configure-mpio-windows-server.md) |<span data-ttu-id="d4547-150">서버를 장치에서 제공하는 iSCSI 저장소에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-150">Connect your servers to the iSCSI storage provided by the device.</span></span> <span data-ttu-id="d4547-151">필요에 따라 MPIO를 구성하여 서버가 링크, 네트워크 및 인터페이스 실패를 허용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-151">Optionally configure MPIO to ensure that your servers can tolerate link, network, and interface failure.</span></span> |
| [<span data-ttu-id="d4547-152">8단계: 백업 수행</span><span class="sxs-lookup"><span data-stu-id="d4547-152">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="d4547-153">백업 정책을 설정하여 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="d4547-153">Set up your backup policy to protect your data</span></span> |
|  | |
| <span data-ttu-id="d4547-154">**기타 절차**</span><span class="sxs-lookup"><span data-stu-id="d4547-154">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="d4547-155">솔루션을 배포하는 경우 이러한 절차를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-155">You may need to refer to these procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="d4547-156">서비스에 대한 새 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="d4547-156">Configure a new storage account for the service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="d4547-157">장치 직렬 콘솔 연결에 PuTTY 사용</span><span class="sxs-lookup"><span data-stu-id="d4547-157">Use PuTTY to connect to the device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="d4547-158">Windows Server 호스트의 IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="d4547-158">Get the IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="d4547-159">수동 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="d4547-159">Create a manual backup</span></span>](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a><span data-ttu-id="d4547-160">배포 구성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="d4547-160">Deployment configuration checklist</span></span>
<span data-ttu-id="d4547-161">장치를 배포하기 전에 정보를 수집하여 StorSimple 장치에 소프트웨어를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-161">Before you deploy your device, you need to collect information to configure the software on your StorSimple device.</span></span> <span data-ttu-id="d4547-162">이 정보를 미리 준비하면 사용자 환경에서 StorSimple 장치를 배포하는 과정을 간소화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-162">Preparing some of this information ahead of time helps streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="d4547-163">또한 이 검사 목록을 다운로드 및 사용하여 장치를 배포하는 동안 구성 세부 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-163">Download and use this checklist to note down the configuration details as you deploy your device.</span></span>

* [<span data-ttu-id="d4547-164">StorSimple 배포 구성 검사 목록 다운로드</span><span class="sxs-lookup"><span data-stu-id="d4547-164">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a><span data-ttu-id="d4547-165">배포 필수 조건</span><span class="sxs-lookup"><span data-stu-id="d4547-165">Deployment prerequisites</span></span>
<span data-ttu-id="d4547-166">다음 섹션에서는 StorSimple 장치 관리자 서비스 및 StorSimple 장치에 대한 필수 조건에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-166">The following sections explain the configuration prerequisites for your StorSimple Device Manager service and your StorSimple device.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="d4547-167">StorSimple 장치 관리자 서비스의 경우</span><span class="sxs-lookup"><span data-stu-id="d4547-167">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="d4547-168">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-168">Before you begin, make sure that:</span></span>

* <span data-ttu-id="d4547-169">액세스 자격 증명이 있는 Microsoft 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-169">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="d4547-170">액세스 자격 증명이 있는 Microsoft Azure 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-170">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="d4547-171">사용자의 Microsoft Azure 구독을 StorSimple 장치 관리자 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-171">Your Microsoft Azure subscription is enabled for the StorSimple Device Manager service.</span></span> <span data-ttu-id="d4547-172">구독은 [기업 계약](https://azure.microsoft.com/pricing/enterprise-agreement/)을 통해 구매해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-172">Your subscription should be purchased through the [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="d4547-173">PuTTY와 같은 터미널 에뮬레이션 소프트웨어에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-173">You have access to terminal emulation software such as PuTTY.</span></span>

### <a name="for-the-device-in-the-datacenter"></a><span data-ttu-id="d4547-174">데이터 센터에서 장치의 경우</span><span class="sxs-lookup"><span data-stu-id="d4547-174">For the device in the datacenter</span></span>
<span data-ttu-id="d4547-175">장치를 구성하기 전에 다음에서 설명한 대로 장치가 완전히 개봉, 랙에 탑재되고 전원, 네트워크 및 직렬 액세스에 완전히 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-175">Before configuring the device, make sure that your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>

* [<span data-ttu-id="d4547-176">8100 장치 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="d4547-176">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="d4547-177">8600 장치 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="d4547-177">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="d4547-178">데이터 센터에서 네트워크의 경우</span><span class="sxs-lookup"><span data-stu-id="d4547-178">For the network in the datacenter</span></span>
<span data-ttu-id="d4547-179">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-179">Before you begin, make sure that:</span></span>

* <span data-ttu-id="d4547-180">[StorSimple 장치에 대한 네트워킹 요구 사항](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device)에서 설명한 대로 데이터 센터 방화벽에서 포트가 열려 있어 iSCSI 및 클라우드 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-180">The ports in your datacenter firewall are opened to allow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="d4547-181">단계별 배포</span><span class="sxs-lookup"><span data-stu-id="d4547-181">Step-by-step deployment</span></span>
<span data-ttu-id="d4547-182">다음 단계별 지침을 사용하여 데이터 센터에서 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-182">Use the following step-by-step instructions to deploy your StorSimple device in the datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="d4547-183">1단계: 새 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="d4547-183">Step 1: Create a new service</span></span>
<span data-ttu-id="d4547-184">StorSimple 장치 관리자 서비스는 여러 StorSimple 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-184">A StorSimple Device Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="d4547-185">StorSimple 장치 관리자 서비스의 인스턴스를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-185">Perform the following steps to create an instance of the StorSimple Device Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="d4547-186">서비스와 함께 저장소 계정을 자동으로 만들도록 설정하지 않은 경우, 서비스를 성공적으로 만든 후 하나 이상의 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-186">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="d4547-187">이 저장소 계정은 볼륨 컨테이너를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-187">This storage account is used when you create a volume container.</span></span>
>
> * <span data-ttu-id="d4547-188">저장소 계정을 자동으로 만들지 않은 경우 자세한 지침은 [서비스에 대한 새 저장소 계정 구성](#configure-a-new-storage-account-for-the-service) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4547-188">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="d4547-189">저장소 계정을 자동으로 생성하도록 설정한 경우, [2단계: 서비스 등록 키 받기](#step-2-get-the-service-registration-key)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-189">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>


## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="d4547-190">2단계: 서비스 등록 키 받기</span><span class="sxs-lookup"><span data-stu-id="d4547-190">Step 2: Get the service registration key</span></span>
<span data-ttu-id="d4547-191">StorSimple 장치 관리자 서비스를 실행한 후에는 서비스 등록 키를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-191">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="d4547-192">이 키는 StorSimple 장치를 서비스에 등록 및 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-192">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="d4547-193">Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-193">Perform the following steps in the Azure portal.</span></span>

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="d4547-194">3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록</span><span class="sxs-lookup"><span data-stu-id="d4547-194">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="d4547-195">다음 절차에서 설명한 대로 StorSimple 장치의 초기 설정을 완료하려면 StorSimple용 Windows PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-195">Use Windows PowerShell for StorSimple to complete the initial setup of your StorSimple device as explained in the following procedure.</span></span> <span data-ttu-id="d4547-196">이 단계를 완료하려면 터미널 에뮬레이션 소프트웨어를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-196">You need to use terminal emulation software to complete this step.</span></span> <span data-ttu-id="d4547-197">자세한 내용은 [장치 직렬 콘솔 연결에 PuTTY 사용](#use-putty-to-connect-to-the-device-serial-console)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4547-197">For more information, see [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-8000-configure-and-register-device-u2](../../includes/storsimple-8000-configure-and-register-device-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="d4547-198">4단계: 최소 장치 설정 완료</span><span class="sxs-lookup"><span data-stu-id="d4547-198">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="d4547-199">StorSimple 장치의 최소 장치 구성에는 다음 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-199">For the minimum device configuration of your StorSimple device, you are required to:</span></span> 

* <span data-ttu-id="d4547-200">장치에 대한 친숙한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-200">Provide a friendly name for your device.</span></span>
* <span data-ttu-id="d4547-201">장치 표준 시간대를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-201">Set the device time zone.</span></span>
* <span data-ttu-id="d4547-202">두 컨트롤러에 고정된 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-202">Assign fixed IP addresses to both the controllers.</span></span>

<span data-ttu-id="d4547-203">최소 장치 설정을 완료하려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-203">Perform the following steps in the Azure portal to complete the minimum device setup.</span></span>

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="d4547-204">5단계: 볼륨 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="d4547-204">Step 5: Create a volume container</span></span>
<span data-ttu-id="d4547-205">볼륨 컨테이너에는 저장소 계정, 대역폭 및 그 안에 포함된 모든 볼륨에 대한 암호화 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-205">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> <span data-ttu-id="d4547-206">StorSimple 장치에서 볼륨 프로비저닝을 시작하려면 볼륨 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-206">You will need to create a volume container before you can start provisioning volumes on your StorSimple device.</span></span>

<span data-ttu-id="d4547-207">볼륨 컨테이너를 만들려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-207">Perform the following steps in the Azure portal to create a volume container.</span></span>

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="d4547-208">6단계: 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="d4547-208">Step 6: Create a volume</span></span>
<span data-ttu-id="d4547-209">볼륨 컨테이너를 만든 후에 서버에 대한 StorSimple 장치에 저장소 볼륨을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-209">After you create a volume container, you can provision a storage volume on the StorSimple device for your servers.</span></span> <span data-ttu-id="d4547-210">볼륨을 만들려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-210">Perform the following steps in the Azure portal to create a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4547-211">StorSimple 장치 관리자는 씬 프로비전된 볼륨과 완전히 프로비전된 볼륨을 둘 다 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-211">StorSimple Device Manager can create both thin and fully provisioned volumes.</span></span> <span data-ttu-id="d4547-212">그러나 부분적으로 프로비전된 볼륨은 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-212">You cannot however create partially provisioned volumes.</span></span>


[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="d4547-213">7단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="d4547-213">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="d4547-214">다음 단계는 Windows Server 호스트에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-214">The following steps are performed on your Windows Server host.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="d4547-215">StorSimple 솔루션의 고가용성을 위해 iSCSI를 구성하기 전에 호스트 서버에 MPIO를 구성하는 것이 좋습니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="d4547-215">For the high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior to configuring iSCSI.</span></span> <span data-ttu-id="d4547-216">호스트 서버에 MPIO를 구성하면 서버가 링크, 네트워크 또는 인터페이스 오류를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-216">MPIO configuration on host servers will ensure that the servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="d4547-217">Windows Server 호스트에서 MPIO 및 iSCSI 설치 및 구성 지침은 [StorSimple 장치에 대한 MPIO 구성](storsimple-8000-configure-mpio-windows-server.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-217">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go to [Configure MPIO for your StorSimple device](storsimple-8000-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="d4547-218">StorSimple 볼륨을 탑재, 초기화 및 포맷하는 단계도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-218">These also include the steps to mount, initialize, and format StorSimple volumes.</span></span>
> * <span data-ttu-id="d4547-219">Linux 호스트에서 MPIO 및 iSCSI 설치 및 구성 지침은 [StorSimple Linux 호스트에 대한 MPIO 구성](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="d4547-219">For MPIO and iSCSI installation and configuration instructions on a Linux host, go to [Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>

<span data-ttu-id="d4547-220">MPIO를 구성하지 않으려는 경우 다음 단계를 수행하여 Windows Server 호스트에서 StorSimple 볼륨을 탑재, 초기화 및 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-220">If you decide not to configure MPIO, perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-8000-mount-initialize-format-volume](../../includes/storsimple-8000-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="d4547-221">8단계: 백업 수행</span><span class="sxs-lookup"><span data-stu-id="d4547-221">Step 8: Take a backup</span></span>
<span data-ttu-id="d4547-222">백업은 볼륨의 지정 시간 보호 기능을 제공하며 복원 시간을 최소화하면서 복구 기능을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-222">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="d4547-223">StorSimple 장치에서 두 유형(로컬 스냅숏 및 클라우드 스냅숏)의 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-223">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="d4547-224">이러한 각 유형의 백업은 **예약됨** 또는 **수동**이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-224">Each of these backup types can be **Scheduled** or **Manual**.</span></span>

<span data-ttu-id="d4547-225">예약된 백업을 만들려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-225">Perform the following steps in the Azure portal to create a scheduled backup.</span></span>

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

<span data-ttu-id="d4547-226">언제든지 수동 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-226">You can take a manual backup at any time.</span></span> <span data-ttu-id="d4547-227">과정은 [수동 백업 만들기](#create-a-manual-backup)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-227">For procedures, go to [Create a manual backup](#create-a-manual-backup).</span></span>

<span data-ttu-id="d4547-228">장치 구성을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-228">You have completed the device configuration.</span></span>

## <a name="configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="d4547-229">서비스에 대한 새 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="d4547-229">Configure a new storage account for the service</span></span>
<span data-ttu-id="d4547-230">서비스와 저장소 계정을 자동으로 생성하도록 설정하지 않은 경우에만 수행해야 하는 선택적 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-230">This is an optional step that you need to perform only if you did not enable the automatic creation of a storage account with your service.</span></span> <span data-ttu-id="d4547-231">StorSimple 볼륨 컨테이너를 만들려면 Microsoft Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-231">A Microsoft Azure storage account is required to create a StorSimple volume container.</span></span>

<span data-ttu-id="d4547-232">다른 지역에 Azure 저장소 계정을 만들어야 하는 경우 단계별 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4547-232">If you need to create an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="d4547-233">**StorSimple 장치 관리자 서비스** 페이지의 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-233">Perform the following steps in the Azure portal, on the **StorSimple Device Manager service** page.</span></span>

[!INCLUDE [storsimple-8000-configure-new-storage-account-u2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a><span data-ttu-id="d4547-234">장치 직렬 콘솔 연결에 PuTTY 사용</span><span class="sxs-lookup"><span data-stu-id="d4547-234">Use PuTTY to connect to the device serial console</span></span>
<span data-ttu-id="d4547-235">StorSimple용 Windows PowerShell에 연결하려면 PuTTY와 같은 터미널 에뮬레이션 소프트웨어를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-235">To connect to Windows PowerShell for StorSimple, you need to use terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="d4547-236">직렬 콘솔을 통해 직접 또는 원격 컴퓨터에서 텔넷 세션을 열어 장치에 액세스할 때 PuTTY를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-236">You can use PuTTY when you access the device directly through the serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="d4547-237">업데이트 검색 및 적용</span><span class="sxs-lookup"><span data-stu-id="d4547-237">Scan for and apply updates</span></span>
<span data-ttu-id="d4547-238">장치 업데이트는 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-238">Updating your device can take several hours.</span></span> <span data-ttu-id="d4547-239">최신 업데이트를 설치하는 방법에 대한 자세한 단계는 [업데이트 4 설치](storsimple-8000-install-update-4.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="d4547-239">For detailed steps on how to install the latest update, go to [Install Update 4](storsimple-8000-install-update-4.md).</span></span>


## <a name="get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="d4547-240">Windows Server 호스트의 IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="d4547-240">Get the IQN of a Windows Server host</span></span>
<span data-ttu-id="d4547-241">Windows Server® 2012를 실행하는 Windows 호스트의 iSCSI 정규화된 이름(IQN)을 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-241">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="d4547-242">수동 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="d4547-242">Create a manual backup</span></span>
<span data-ttu-id="d4547-243">StorSimple 장치에서 단일 볼륨에 대한 주문형 수동 백업을 만들려면 Azure Portal에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d4547-243">Perform the following steps in the Azure portal to create an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="d4547-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4547-244">Next steps</span></span>
* <span data-ttu-id="d4547-245">[StorSimple Cloud Appliance를 구성합니다](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="d4547-245">[Configure a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>
* <span data-ttu-id="d4547-246">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리합니다](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d4547-246">[Use the StorSimple Device Manager service to manage your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

