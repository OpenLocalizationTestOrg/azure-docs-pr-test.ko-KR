---
title: "aaaStorSimple 가상 배열 웹 UI 관리 | Microsoft Docs"
description: "Hello StorSimple 가상 배열 웹 UI 통해 tooperform 기본 장치 관리 작업 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="01cbb-103">Hello 웹 UI tooadminister StorSimple 가상 배열 사용</span><span class="sxs-lookup"><span data-stu-id="01cbb-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![설정 프로세스 흐름](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="01cbb-105">개요</span><span class="sxs-lookup"><span data-stu-id="01cbb-105">Overview</span></span>
<span data-ttu-id="01cbb-106">이 문서의 자습서 hello toohello Microsoft Azure StorSimple 가상 배열 (라고도 hello StorSimple 온-프레미스 가상 장치) 실행 중인 2016 년 3 월 GA (일반 공급) 릴리스를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="01cbb-107">이 문서는 hello 복잡 한 워크플로 및 hello StorSimple 가상 배열에서 수행할 수 있는 관리 작업의 일부를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="01cbb-108">관리할 수 있습니다 (참조 tooas hello 포털 UI) UI hello StorSimple Manager 서비스를 사용 하 여 StorSimple 가상 배열 hello 및 hello hello 장치에 대 한 로컬 웹 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="01cbb-109">본이 문서 hello 작업에서는 hello 웹 UI를 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="01cbb-110">이 문서에는 자습서를 따라 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="01cbb-111">Hello 서비스 데이터 암호화 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="01cbb-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="01cbb-112">웹 UI 설정 오류 해결</span><span class="sxs-lookup"><span data-stu-id="01cbb-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="01cbb-113">로그 패키지 생성</span><span class="sxs-lookup"><span data-stu-id="01cbb-113">Generate a log package</span></span>
* <span data-ttu-id="01cbb-114">장치 종료 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="01cbb-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="01cbb-115">Hello 서비스 데이터 암호화 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="01cbb-115">Get hello service data encryption key</span></span>
<span data-ttu-id="01cbb-116">서비스 데이터 암호화 키는 StorSimple Manager 서비스 hello로 첫 번째 장치를 등록할 때 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="01cbb-117">이 키는 다음 hello 서비스 등록 키 tooregister 추가 장치를 StorSimple Manager 서비스 hello에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="01cbb-118">서비스 데이터 암호화 키를 분실 한 경우 및 tooretrieve 필요를 hello 다음이 수행 단계 hello 로컬 웹 UI hello 장치에서에서 서비스로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="01cbb-119">tooget hello 서비스 데이터 암호화 키</span><span class="sxs-lookup"><span data-stu-id="01cbb-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="01cbb-120">Toohello 로컬 웹 UI를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-120">Connect toohello local web UI.</span></span> <span data-ttu-id="01cbb-121">너무 이동**구성** > **클라우드 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="01cbb-122">Hello hello 페이지의 아래쪽에 있는 클릭 **Get 서비스 데이터 암호화 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="01cbb-123">키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-123">A key will appear.</span></span> <span data-ttu-id="01cbb-124">이 키를 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-124">Copy and save this key.</span></span>
   
    ![서비스 데이터 암호화 키 가져오기 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="01cbb-126">웹 UI 설정 오류 해결</span><span class="sxs-lookup"><span data-stu-id="01cbb-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="01cbb-127">경우에 따라 hello 로컬 웹 UI 통해 hello 장치를 구성 오류에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="01cbb-128">toodiagnose 이러한 오류를 해결 하 고, hello 진단 테스트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="01cbb-129">toorun hello 진단 테스트</span><span class="sxs-lookup"><span data-stu-id="01cbb-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="01cbb-130">Hello 로컬 웹 UI에서에서 이동 너무**문제 해결** > **진단 테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![진단 실행 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="01cbb-132">Hello hello 페이지의 아래쪽에 있는 클릭 **진단 테스트 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="01cbb-133">그러면 시작 테스트 toodiagnose 모든 관련 문제를 네트워크, 장치, 웹 프록시, 시간 또는 클라우드 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="01cbb-134">알려 해당 hello 장치에서 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="01cbb-135">Hello 테스트를 완료 한 후 hello 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="01cbb-136">hello 다음 예제에서는 진단 테스트의 hello 결과</span><span class="sxs-lookup"><span data-stu-id="01cbb-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="01cbb-137">Note hello 웹 프록시 설정이이 장치에 대해 구성 되지 않은 하 고 따라서 hello 웹 프록시 테스트 실행 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="01cbb-138">네트워크 설정, DNS 서버에 대 한 다른 테스트 모두 hello 및 시간 설정에 성공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![진단 실행 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="01cbb-140">로그 패키지 생성</span><span class="sxs-lookup"><span data-stu-id="01cbb-140">Generate a log package</span></span>
<span data-ttu-id="01cbb-141">로그 패키지 장치 문제 해결에 Microsoft 기술 지원 서비스를 지원할 수 있는 모든 hello 관련 로그로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="01cbb-142">이 릴리스에서 hello 로컬 웹 UI 통해 로그 패키지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="01cbb-143">toogenerate hello 로그 패키지</span><span class="sxs-lookup"><span data-stu-id="01cbb-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="01cbb-144">Hello 로컬 웹 UI에서에서 이동 너무**문제 해결** > **시스템 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![로그 패키지 생성 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="01cbb-146">Hello hello 페이지의 아래쪽에 있는 클릭 **로그 패키지 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="01cbb-147">Hello 시스템 로그의 패키지 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="01cbb-148">이 작업에 몇 분 정도가 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-148">This will take a couple of minutes.</span></span>
   
    ![로그 패키지 생성 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="01cbb-150">Hello 패키지가 성공적으로 만들어지면 tooindicate hello 시간 및 날짜 hello 패키지를 만들 때 hello 페이지는 업데이트 후 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![로그 패키지 생성 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="01cbb-152">**로그 패키지 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-152">Click **Download log package**.</span></span> <span data-ttu-id="01cbb-153">압축된 패키지가 시스템에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-153">A zipped package will be downloaded on your system.</span></span>
   
    ![로그 패키지 생성 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="01cbb-155">Hello 로그 다운로드 한 패키지를 압축 해제 하 고 hello 시스템 로그 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="01cbb-156">장치 종료 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="01cbb-156">Shut down and restart your device</span></span>
<span data-ttu-id="01cbb-157">종료 하거나 hello 로컬 웹 UI를 사용 하 여 가상 장치를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="01cbb-158">다시 시작 하 고 hello 호스트에서 hello 볼륨 또는 공유가 오프 라인 장치를 다음 hello 전에 하는 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="01cbb-159">이렇게 하면 데이터 손상 가능성이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="01cbb-160">가상 장치 아래로 tooshut</span><span class="sxs-lookup"><span data-stu-id="01cbb-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="01cbb-161">Hello 로컬 웹 UI에서에서 이동 너무**유지 관리** > **전원 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="01cbb-162">Hello hello 페이지의 아래쪽에 있는 클릭 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![장치 종료 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="01cbb-164">Hello 장치 종료는는 작동 중단, 진행 중인 어떤 IO를 중단 한다는 경고 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="01cbb-165">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-165">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="01cbb-167">으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-167">.</span></span>
   
    ![장치 종료 경고](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="01cbb-169">알려 hello을 늘려 종료를 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![장치 종료 시작됨](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="01cbb-171">hello 장치 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-171">hello device will now shut down.</span></span> <span data-ttu-id="01cbb-172">장치 toostart 원하는 통해 Hyper-v 관리자 hello toodo를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="01cbb-173">toorestart 가상 장치</span><span class="sxs-lookup"><span data-stu-id="01cbb-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="01cbb-174">Hello 로컬 웹 UI에서에서 이동 너무**유지 관리** > **전원 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="01cbb-175">Hello hello 페이지의 아래쪽에 있는 클릭 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![장치 다시 시작](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="01cbb-177">재시작 hello 장치는 작동 중단 IOs 진행 중인 경우 중단 되었다는 경고가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="01cbb-178">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-178">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="01cbb-180">으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-180">.</span></span>
   
    ![다시 시작 경고](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="01cbb-182">알려 해당 hello 다시 시작 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![다시 시작 시작됨](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="01cbb-184">Hello를 다시 시작이 진행 중에서 상태인 동안 hello 연결 toohello UI는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="01cbb-185">Hello UI를 주기적으로 새로 고쳐 hello를 다시 시작을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="01cbb-186">또는 hello Hyper-v 관리자를 통해 hello 장치 다시 시작 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01cbb-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="01cbb-187">Next steps</span></span>
<span data-ttu-id="01cbb-188">너무 방법에 대해 알아봅니다[사용 하 여 장치를 StorSimple Manager 서비스 toomanage hello](storsimple-virtual-array-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01cbb-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

