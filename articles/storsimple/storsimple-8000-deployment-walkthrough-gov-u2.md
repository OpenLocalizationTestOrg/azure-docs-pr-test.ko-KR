---
title: "정부 포털에서 StorSimple 8000 시리즈 장치 배포 | Microsoft Docs"
description: "Azure Government 포털에서 업데이트 3 이상을 실행하는 StorSimple 8000 시리즈 장치 및 서비스를 배포하기 위한 단계와 모범 사례를 설명합니다."
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
ms.workload: NA
ms.date: 06/22/2017
ms.author: alkohli
ms.openlocfilehash: 5a622eb5ae14a6c6b0c2dd4eceb6ffdb9733dcff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-the-government-portal"></a><span data-ttu-id="55621-103">Government 포털에서 온-프레미스 StorSimple 장치 배포</span><span class="sxs-lookup"><span data-stu-id="55621-103">Deploy your on-premises StorSimple device in the Government portal</span></span>

## <a name="overview"></a><span data-ttu-id="55621-104">개요</span><span class="sxs-lookup"><span data-stu-id="55621-104">Overview</span></span>
<span data-ttu-id="55621-105">Microsoft Azure StorSimple 장치 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-105">Welcome to Microsoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="55621-106">이러한 배포 자습서는 Azure Government 포털에서 업데이트 3 소프트웨어 이상을 실행하는 StorSimple 8000 시리즈에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="55621-106">These deployment tutorials apply to the StorSimple 8000 Series running Update 3 software or later in the Azure Government portal.</span></span> <span data-ttu-id="55621-107">이 자습서 시리즈에서는 StorSimple 장치를 구성하는 방법에 대해 설명하며 구성 검사 목록, 구성 필수 조건 목록 및 자세한 구성 단계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-107">This series of tutorials includes a configuration checklist, a list of configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="55621-108">이 자습서의 정보는 안전 주의 사항을 검토했으며, StorSimple 장치의 포장을 풀었고, 랙을 탑재했으며, 케이블에 연결되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-108">The information in these tutorials assumes that you have reviewed the safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="55621-109">여전히 이러한 작업을 수행해야 하는 경우 [안전 주의 사항](storsimple-safety.md)검토로 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="55621-109">If you still need to perform those tasks, start with reviewing the [safety precautions](storsimple-safety.md).</span></span> <span data-ttu-id="55621-110">장치를 개봉, 랙 탑재 및 케이블로 연결하려면 장치별 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="55621-110">Follow the device-specific instructions to unpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="55621-111">8100 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="55621-111">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="55621-112">8600 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="55621-112">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="55621-113">설치 및 구성 프로세스를 완료하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-113">You will need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="55621-114">시작하기 전에 구성 검사 목록을 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-114">We recommend that you review the configuration checklist before you begin.</span></span> <span data-ttu-id="55621-115">배포 및 구성 프로세스는 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-115">The deployment and configuration process can take some time to complete.</span></span>

> [!NOTE]
> <span data-ttu-id="55621-116">Microsoft Azure 웹 사이트에 게시된 StorSimple 배포 정보는 StorSimple 8000 시리즈 장치에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="55621-116">The StorSimple deployment information published on the Microsoft Azure website applies to StorSimple 8000 series devices only.</span></span> <span data-ttu-id="55621-117">7000 시리즈 장치에 대한 자세한 내용은 [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-117">For complete information about the 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com).</span></span> <span data-ttu-id="55621-118">7000 시리즈 배포 정보는 [StorSimple 시스템 퀵 스타트 가이드](http://onlinehelp.storsimple.com/111_Appliance/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55621-118">For 7000 series deployment information, see the [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).</span></span>


## <a name="deployment-steps"></a><span data-ttu-id="55621-119">배포 단계</span><span class="sxs-lookup"><span data-stu-id="55621-119">Deployment steps</span></span>
<span data-ttu-id="55621-120">StorSimple 장치를 구성하여 StorSimple 장치 관리자 서비스에 연결하려면 다음과 같은 필수 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-120">Perform these required steps to configure your StorSimple device and connect it to your StorSimple Device Manager service.</span></span> <span data-ttu-id="55621-121">필수 단계 외에 선택적 단계 및 배포하는 동안 완료해야 할 수도 있는 절차가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-121">In addition to the required steps, there are optional steps and procedures that you may need to complete during the deployment.</span></span> <span data-ttu-id="55621-122">단계별 배포 지침은 각 선택적 단계를 수행해야 하는 시기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="55621-122">The step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="55621-123">단계</span><span class="sxs-lookup"><span data-stu-id="55621-123">Step</span></span> | <span data-ttu-id="55621-124">설명</span><span class="sxs-lookup"><span data-stu-id="55621-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="55621-125">**필수 조건**</span><span class="sxs-lookup"><span data-stu-id="55621-125">**PREREQUISITES**</span></span> |<span data-ttu-id="55621-126">향후 배포 준비 과정에서 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-126">These need to be completed in preparation for the upcoming deployment.</span></span> |
| [<span data-ttu-id="55621-127">배포 구성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="55621-127">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="55621-128">이 검사 목록을 사용하여 배포 이전 및 배포하는 동안 정보를 수집하고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-128">Use this checklist to gather and record information prior to and during the deployment.</span></span> |
| [<span data-ttu-id="55621-129">배포 필수 조건</span><span class="sxs-lookup"><span data-stu-id="55621-129">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="55621-130">배포할 준비가 되어 있는 환경인지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-130">These  validate that the environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="55621-131">**단계별 배포**</span><span class="sxs-lookup"><span data-stu-id="55621-131">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="55621-132">프로덕션 환경에서 StorSimple 장치를 배포하려면 다음 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-132">These steps are required to deploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="55621-133">1단계: 새 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="55621-133">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="55621-134">StorSimple 장치에 대한 클라우드 관리 및 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-134">Set up cloud management and storage for your StorSimple device.</span></span> <span data-ttu-id="55621-135">*다른 StorSimple 장치에 대해 기존 서비스가 있는 경우 이 단계를 건너뜁니다*.</span><span class="sxs-lookup"><span data-stu-id="55621-135">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="55621-136">2단계: 서비스 등록 키 받기</span><span class="sxs-lookup"><span data-stu-id="55621-136">Step 2: Get the service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="55621-137">이 키를 사용하여 StorSimple 장치를 관리 서비스에 등록 및 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-137">Use this key to register and connect your StorSimple device with the management service.</span></span> |
| [<span data-ttu-id="55621-138">3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록</span><span class="sxs-lookup"><span data-stu-id="55621-138">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="55621-139">장치를 네트워크에 연결하고 관리 서비스를 사용하여 Azure로 등록하여 설정을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-139">Connect the device to your network and register it with Azure to complete the setup using the management service.</span></span> |
| [<span data-ttu-id="55621-140">4단계: 최소 장치 설정 완료</span><span class="sxs-lookup"><span data-stu-id="55621-140">Step 4: Complete the minimum device setup</span></span>](#step-4-complete-minimum-device-setup) </br><span data-ttu-id="55621-141">선택 사항: StorSimple 장치를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-141">Optional: Update your StorSimple device.</span></span> |<span data-ttu-id="55621-142">관리 서비스를 사용하여 장치 설정을 완료하고 저장소를 제공할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-142">Use the management service to complete the device setup and enable it to provide storage.</span></span> |
| [<span data-ttu-id="55621-143">5단계: 볼륨 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="55621-143">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="55621-144">볼륨을 프로비전할 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55621-144">Create a container to provision volumes.</span></span> <span data-ttu-id="55621-145">볼륨 컨테이너에는 저장소 계정, 대역폭 및 그 안에 포함된 모든 볼륨에 대한 암호화 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-145">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> |
| [<span data-ttu-id="55621-146">6단계: 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="55621-146">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="55621-147">서버에 대한 StorSimple 장치의 저장소 볼륨을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-147">Provision storage volume(s) on the StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="55621-148">7단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="55621-148">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume) </br><span data-ttu-id="55621-149">선택 사항: MPIO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-149">Optional: Configure MPIO.</span></span> |<span data-ttu-id="55621-150">서버를 장치에서 제공하는 iSCSI 저장소에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-150">Connect your servers to the iSCSI storage provided by the device.</span></span> <span data-ttu-id="55621-151">필요에 따라 MPIO를 구성하여 서버가 링크, 네트워크 및 인터페이스 실패를 허용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-151">Optionally, configure MPIO to ensure that your servers can tolerate link, network, and interface failure.</span></span> |
| [<span data-ttu-id="55621-152">8단계: 백업 수행</span><span class="sxs-lookup"><span data-stu-id="55621-152">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="55621-153">백업 정책을 설정하여 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="55621-153">Set up your backup policy to protect your data</span></span> |
|  | |
| <span data-ttu-id="55621-154">**기타 절차**</span><span class="sxs-lookup"><span data-stu-id="55621-154">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="55621-155">솔루션을 배포하는 경우 이러한 절차를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-155">You may need to refer to these procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="55621-156">서비스에 대한 새 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="55621-156">Configure a new storage account for the service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="55621-157">장치 직렬 콘솔 연결에 PuTTY 사용</span><span class="sxs-lookup"><span data-stu-id="55621-157">Use PuTTY to connect to the device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="55621-158">업데이트 검색 및 적용</span><span class="sxs-lookup"><span data-stu-id="55621-158">Scan for and apply updates</span></span>](#scan-for-and-apply-updates) | |
| [<span data-ttu-id="55621-159">Windows Server 호스트의 IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="55621-159">Get the IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="55621-160">수동 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="55621-160">Create a manual backup</span></span>](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a><span data-ttu-id="55621-161">배포 구성 검사 목록</span><span class="sxs-lookup"><span data-stu-id="55621-161">Deployment configuration checklist</span></span>
<span data-ttu-id="55621-162">StorSimple 장치를 배포하기 전에 정보를 수집하여 장치에 소프트웨어를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-162">Before you deploy your StorSimple device, you will need to collect information to configure the software on your device.</span></span> <span data-ttu-id="55621-163">이 정보의 일부를 미리 준비하면 사용자 환경에서 StorSimple 장치를 배포하는 과정을 간소화하는데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55621-163">Preparing some of this information ahead of time will help streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="55621-164">또한 이 검사 목록을 다운로드 및 사용하여 장치를 배포하는 동안 구성 세부 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-164">Download and use this checklist to note the configuration details as you deploy your device.</span></span>

[<span data-ttu-id="55621-165">StorSimple 배포 구성 검사 목록 다운로드</span><span class="sxs-lookup"><span data-stu-id="55621-165">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a><span data-ttu-id="55621-166">배포 필수 조건</span><span class="sxs-lookup"><span data-stu-id="55621-166">Deployment prerequisites</span></span>
<span data-ttu-id="55621-167">다음 섹션에서는 StorSimple 장치 관리자 서비스 및 StorSimple 장치에 대한 필수 조건에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-167">The following sections explain the configuration prerequisites for your StorSimple Device Manager service and your StorSimple device.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="55621-168">StorSimple 장치 관리자 서비스의 경우</span><span class="sxs-lookup"><span data-stu-id="55621-168">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="55621-169">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-169">Before you begin, make sure that:</span></span>

* <span data-ttu-id="55621-170">액세스 자격 증명이 있는 Microsoft 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-170">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="55621-171">액세스 자격 증명이 있는 Microsoft Azure 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-171">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="55621-172">사용자의 Microsoft Azure 구독을 StorSimple 장치 관리자 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-172">Your Microsoft Azure subscription is enabled for the StorSimple Device Manager service.</span></span> <span data-ttu-id="55621-173">구독은 [기업 계약](https://azure.microsoft.com/pricing/enterprise-agreement/)을 통해 구매해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-173">Your subscription should be purchased through the [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="55621-174">PuTTY와 같은 터미널 에뮬레이션 소프트웨어에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-174">You have access to terminal emulation software such as PuTTY.</span></span>

### <a name="for-the-device-in-the-datacenter"></a><span data-ttu-id="55621-175">데이터 센터에서 장치의 경우</span><span class="sxs-lookup"><span data-stu-id="55621-175">For the device in the datacenter</span></span>
<span data-ttu-id="55621-176">장치를 구성하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-176">Before configuring the device, make sure that:</span></span>

* <span data-ttu-id="55621-177">다음에서 설명한 대로 장치가 완전히 개봉, 랙에 탑재되고 전원, 네트워크 및 직렬 액세스에 완전히 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-177">Your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>
  
  * [<span data-ttu-id="55621-178">8100 장치 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="55621-178">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
  * [<span data-ttu-id="55621-179">8600 장치 개봉, 랙 탑재, 케이블 연결</span><span class="sxs-lookup"><span data-stu-id="55621-179">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="55621-180">데이터 센터에서 네트워크의 경우</span><span class="sxs-lookup"><span data-stu-id="55621-180">For the network in the datacenter</span></span>
<span data-ttu-id="55621-181">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-181">Before you begin, make sure that:</span></span>

* <span data-ttu-id="55621-182">[StorSimple 장치에 대한 네트워킹 요구 사항](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device)에서 설명한 대로 데이터 센터 방화벽에서 포트가 열려 있어 iSCSI 및 클라우드 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-182">The ports in your datacenter firewall are opened to allow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="55621-183">단계별 배포</span><span class="sxs-lookup"><span data-stu-id="55621-183">Step-by-step deployment</span></span>
<span data-ttu-id="55621-184">다음 단계별 지침을 사용하여 데이터 센터에서 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-184">Use the following step-by-step instructions to deploy your StorSimple device in the datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="55621-185">1단계: 새 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="55621-185">Step 1: Create a new service</span></span>
<span data-ttu-id="55621-186">StorSimple 장치 관리자 서비스는 여러 StorSimple 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-186">A StorSimple Device Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="55621-187">StorSimple 장치 관리자 서비스의 새 인스턴스를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-187">Perform the following steps to create a new instance of the StorSimple Device Manager service.</span></span>

[!INCLUDE [storsimple-8000-create-new-service-gov](../../includes/storsimple-8000-create-new-service-gov.md)]

> [!IMPORTANT]
> <span data-ttu-id="55621-188">서비스와 함께 저장소 계정을 자동으로 만들도록 설정하지 않은 경우, 서비스를 성공적으로 만든 후 하나 이상의 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-188">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span> <span data-ttu-id="55621-189">이 저장소 계정은 볼륨 컨테이너를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="55621-189">This storage account will be used when you create a volume container.</span></span>
> 
> * <span data-ttu-id="55621-190">저장소 계정을 자동으로 만들지 않은 경우 자세한 지침은 [서비스에 대한 새 저장소 계정 구성](#configure-a-new-storage-account-for-the-service) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55621-190">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="55621-191">저장소 계정을 자동으로 생성하도록 설정한 경우, [2단계: 서비스 등록 키 받기](#step-2-get-the-service-registration-key)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-191">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>


## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="55621-192">2단계: 서비스 등록 키 받기</span><span class="sxs-lookup"><span data-stu-id="55621-192">Step 2: Get the service registration key</span></span>
<span data-ttu-id="55621-193">StorSimple 장치 관리자 서비스를 실행한 후에는 서비스 등록 키를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-193">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="55621-194">이 키는 StorSimple 장치를 서비스에 등록 및 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="55621-194">This key is used to register and connect your StorSimple device to the service.</span></span>

<span data-ttu-id="55621-195">Government 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-195">Perform the following steps in the Government portal.</span></span>

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="55621-196">3단계: StorSimple용 Windows PowerShell을 통해 장치 구성 및 등록</span><span class="sxs-lookup"><span data-stu-id="55621-196">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="55621-197">다음 절차에서 설명한 대로 StorSimple 장치의 초기 설정을 완료하려면 StorSimple용 Windows PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-197">Use Windows PowerShell for StorSimple to complete the initial setup of your StorSimple device as explained in the following procedure.</span></span> <span data-ttu-id="55621-198">이 단계를 완료하려면 터미널 에뮬레이션 소프트웨어를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-198">You will need to use terminal emulation software to complete this step.</span></span> <span data-ttu-id="55621-199">자세한 내용은 [장치 직렬 콘솔 연결에 PuTTY 사용](#use-putty-to-connect-to-the-device-serial-console)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55621-199">For more information, see [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-8000-configure-and-register-device-gov](../../includes/storsimple-8000-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="55621-200">4단계: 최소 장치 설정 완료</span><span class="sxs-lookup"><span data-stu-id="55621-200">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="55621-201">StorSimple 장치의 최소 장치 구성에는 다음 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-201">For the minimum device configuration of your StorSimple device, you are required to:</span></span>

* <span data-ttu-id="55621-202">장치에 대한 친숙한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-202">Provide a friendly name for your device.</span></span>
* <span data-ttu-id="55621-203">장치 표준 시간대를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-203">Set the device time zone.</span></span>
* <span data-ttu-id="55621-204">두 컨트롤러에 고정된 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-204">Assign fixed IP addresses to both the controllers.</span></span>

<span data-ttu-id="55621-205">Azure Government 포털에서 최소 장치 설정을 완료하려면 Government 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-205">Perform the following steps in the Azure Government portal to complete the minimum device setup.</span></span>

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="55621-206">5단계: 볼륨 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="55621-206">Step 5: Create a volume container</span></span>
<span data-ttu-id="55621-207">볼륨 컨테이너에는 저장소 계정, 대역폭 및 그 안에 포함된 모든 볼륨에 대한 암호화 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-207">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> <span data-ttu-id="55621-208">StorSimple 장치에서 볼륨 프로비저닝을 시작하려면 볼륨 컨테이너를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-208">You will need to create a volume container before you can start provisioning volumes on your StorSimple device.</span></span>

<span data-ttu-id="55621-209">볼륨 컨테이너를 만들려면 Government 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-209">Perform the following steps in the Government portal to create a volume container.</span></span>

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="55621-210">6단계: 볼륨 만들기</span><span class="sxs-lookup"><span data-stu-id="55621-210">Step 6: Create a volume</span></span>
<span data-ttu-id="55621-211">볼륨 컨테이너를 만든 후에 서버에 대한 StorSimple 장치에 저장소 볼륨을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-211">After you create a volume container, you can provision a storage volume on the StorSimple device for your servers.</span></span> <span data-ttu-id="55621-212">볼륨을 만들려면 Government 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-212">Perform the following steps in the Government portal to create a volume.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55621-213">StorSimple 장치 관리자는 씬 프로비저닝된 볼륨만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-213">StorSimple Device Manager can create only thinly provisioned volumes.</span></span>  <span data-ttu-id="55621-214">그러나 부분적으로 프로비전된 볼륨은 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-214">You cannot however create partially provisioned volumes.</span></span>

[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="55621-215">7단계: 볼륨 탑재, 초기화 및 포맷</span><span class="sxs-lookup"><span data-stu-id="55621-215">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="55621-216">Windows Server 호스트에서 이러한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-216">Perform these steps on your Windows Server host.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="55621-217">StorSimple 솔루션의 고가용성을 위해 iSCSI를 구성하기 전에 호스트 서버에 MPIO를 구성하는 것이 좋습니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="55621-217">For the high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior to configuring iSCSI.</span></span> <span data-ttu-id="55621-218">호스트 서버에 MPIO를 구성하면 서버가 링크, 네트워크 또는 인터페이스 오류를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-218">MPIO configuration on host servers will ensure that the servers can tolerate a link, network, or interface failure.</span></span>
> * <span data-ttu-id="55621-219">Windows Server 호스트에서 MPIO 및 iSCSI 설치 및 구성 지침은 [StorSimple 장치에 대한 MPIO 구성](storsimple-configure-mpio-windows-server.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-219">For MPIO and iSCSI installation and configuration instructions on Windows Server host, go to [Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md).</span></span> <span data-ttu-id="55621-220">StorSimple 볼륨을 탑재, 초기화 및 포맷하는 단계도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="55621-220">These will also include the steps to mount, initialize and format StorSimple volumes.</span></span>
> * <span data-ttu-id="55621-221">Linux 호스트에서 MPIO 및 iSCSI 설치 및 구성 지침은 [StorSimple Linux 호스트에 대한 MPIO 구성](storsimple-configure-mpio-on-linux.md)</span><span class="sxs-lookup"><span data-stu-id="55621-221">For MPIO and iSCSI installation and configuration instructions on a Linux host, go to [Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)</span></span>

<span data-ttu-id="55621-222">MPIO를 구성하지 않으려는 경우 다음 단계를 수행하여 Windows Server 호스트에서 StorSimple 볼륨을 탑재, 초기화 및 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-222">If you decide not to configure MPIO, perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="55621-223">8단계: 백업 수행</span><span class="sxs-lookup"><span data-stu-id="55621-223">Step 8: Take a backup</span></span>
<span data-ttu-id="55621-224">백업은 볼륨의 지정 시간 보호 기능을 제공하며 복원 시간을 최소화하면서 복구 기능을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-224">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="55621-225">StorSimple 장치에서 두 유형(로컬 스냅숏 및 클라우드 스냅숏)의 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-225">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="55621-226">이러한 각 유형의 백업은 **예약됨** 또는 **수동**이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-226">Each of these backup types can be **Scheduled** or **Manual**.</span></span>

<span data-ttu-id="55621-227">예약된 백업을 만들려면 Government 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-227">Perform the following steps in the Government portal to create a scheduled backup.</span></span>

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

<span data-ttu-id="55621-228">언제든지 수동 백업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-228">You can take a manual backup at any time.</span></span> <span data-ttu-id="55621-229">과정은 [수동 백업 만들기](#create-a-manual-backup)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-229">For procedures, go to [Create a manual backup](#create-a-manual-backup).</span></span>

## <a name="configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="55621-230">서비스에 대한 새 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="55621-230">Configure a new storage account for the service</span></span>
<span data-ttu-id="55621-231">서비스와 저장소 계정을 자동으로 생성하도록 설정하지 않은 경우에만 수행해야 하는 선택적 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="55621-231">This is an optional step that you need to perform only if you did not enable the automatic creation of a storage account with your service.</span></span> <span data-ttu-id="55621-232">StorSimple 볼륨 컨테이너를 만들려면 Microsoft Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-232">A Microsoft Azure storage account is required to create a StorSimple volume container.</span></span>

<span data-ttu-id="55621-233">다른 지역에 Azure 저장소 계정을 만들어야 하는 경우 단계별 지침은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55621-233">If you need to create an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="55621-234">Government 포털의 **StorSimple 장치 관리자 서비스** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-234">Perform the following steps in the Government portal, on the **StorSimple Device Manager service** page.</span></span>

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a><span data-ttu-id="55621-235">장치 직렬 콘솔 연결에 PuTTY 사용</span><span class="sxs-lookup"><span data-stu-id="55621-235">Use PuTTY to connect to the device serial console</span></span>
<span data-ttu-id="55621-236">StorSimple용 Windows PowerShell에 연결하려면 PuTTY와 같은 터미널 에뮬레이션 소프트웨어를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-236">To connect to Windows PowerShell for StorSimple, you need to use terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="55621-237">직렬 콘솔을 통해 직접 또는 원격 컴퓨터에서 텔넷 세션을 열어 장치에 액세스할 때 PuTTY를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-237">You can use PuTTY when you access the device directly through the serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="55621-238">업데이트 검색 및 적용</span><span class="sxs-lookup"><span data-stu-id="55621-238">Scan for and apply updates</span></span>
<span data-ttu-id="55621-239">장치 업데이트는 몇 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55621-239">Updating your device can take several hours.</span></span> <span data-ttu-id="55621-240">최신 업데이트를 설치하는 방법에 대한 자세한 단계는 [업데이트 4 설치](storsimple-8000-install-update-4.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="55621-240">For detailed steps on how to install the latest update, go to [Install Update 4](storsimple-8000-install-update-4.md).</span></span>

## <a name="get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="55621-241">Windows Server 호스트의 IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="55621-241">Get the IQN of a Windows Server host</span></span>
<span data-ttu-id="55621-242">Windows Server® 2012를 실행하는 Windows 호스트의 iSCSI 정규화된 이름(IQN)을 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-242">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Get IQN of your Windows Server host](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="55621-243">수동 백업 만들기</span><span class="sxs-lookup"><span data-stu-id="55621-243">Create a manual backup</span></span>
<span data-ttu-id="55621-244">StorSimple 장치에서 단일 볼륨에 대한 주문형 수동 백업을 만들려면 Government 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-244">Perform the following steps in the Government portal to create an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="55621-245">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55621-245">Next steps</span></span>
* <span data-ttu-id="55621-246">[가상 장치](storsimple-8000-cloud-appliance-u2.md)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-246">Configure a [virtual device](storsimple-8000-cloud-appliance-u2.md).</span></span>
* <span data-ttu-id="55621-247">[StorSimple 장치 관리자 서비스](storsimple-8000-manager-service-administration.md)를 사용하여 StorSimple 장치를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="55621-247">Use the [StorSimple Device Manager service](storsimple-8000-manager-service-administration.md) to manage your StorSimple device.</span></span>

