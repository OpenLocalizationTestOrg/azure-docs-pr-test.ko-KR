---
title: "C mbed에서 사용 하 여 장치 aaaConnect | Microsoft Docs"
description: "어떻게 tooconnect 장치 toohello Azure IoT Suite 미리 구성 된 mbed 장치에서 실행 하는 C로 작성 된 응용 프로그램을 사용 하 여 원격 모니터링 솔루션에 설명 합니다."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="9df0d-103">사용자 장치 toohello 모니터링 미리 구성 된 솔루션 (mbed) 원격 연결</span><span class="sxs-lookup"><span data-stu-id="9df0d-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="9df0d-104">시나리오 개요</span><span class="sxs-lookup"><span data-stu-id="9df0d-104">Scenario overview</span></span>
<span data-ttu-id="9df0d-105">이 시나리오에서는 원격 분석 toohello 원격 모니터링을 수행 하는 hello를 전송 하는 장치를 만들 [솔루션 미리 구성 된][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="9df0d-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="9df0d-106">외부 온도</span><span class="sxs-lookup"><span data-stu-id="9df0d-106">External temperature</span></span>
* <span data-ttu-id="9df0d-107">내부 온도</span><span class="sxs-lookup"><span data-stu-id="9df0d-107">Internal temperature</span></span>
* <span data-ttu-id="9df0d-108">습도</span><span class="sxs-lookup"><span data-stu-id="9df0d-108">Humidity</span></span>

<span data-ttu-id="9df0d-109">간단한 설명을 위해 hello 장치에서 hello 코드 샘플 값을 생성 하지만 실제 센서 tooyour 장치를 연결 하 고 실제 원격 분석 보내기 tooextend hello 샘플 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="9df0d-110">hello 장치 수 toorespond toomethods hello 솔루션 대시보드에서 호출 하 고 원하는 hello 솔루션 대시보드에 설정 된 속성 값 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="9df0d-111">toocomplete이이 자습서에서는 활성 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="9df0d-112">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9df0d-113">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9df0d-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9df0d-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9df0d-114">Before you start</span></span>
<span data-ttu-id="9df0d-115">장치에 대한 코드를 작성하기 전에, 미리 구성된 원격 모니터링 솔루션을 프로비전하고 이 솔루션에 새로운 사용자 지정 장치를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="9df0d-116">미리 구성된 사용자의 원격 모니터링 솔루션 프로비전</span><span class="sxs-lookup"><span data-stu-id="9df0d-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="9df0d-117">hello의 tooan 인스턴스 데이터를 전송 하는이 자습서에서 만드는 hello 장치 [원격 모니터링] [ lnk-remote-monitoring] 솔루션 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="9df0d-118">원격 Azure 계정에서 미리 구성 된 솔루션을 모니터링 하는 hello를 프로 비전 이미 하지 않은 경우 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="9df0d-119">Hello에 <https://www.azureiotsuite.com/> 페이지  **+**  toocreate 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="9df0d-120">클릭 **선택** hello에 **원격 모니터링** toocreate 솔루션 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="9df0d-121">Hello에 **원격 만들 모니터링 솔루션** 페이지에서 입력는 **솔루션 이름** 의 선택한 hello 선택 **지역** , toodeploy 한 hello Azure를 선택 합니다. 구독 toowant toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="9df0d-122">그런 다음 **솔루션 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="9df0d-123">Hello를 프로 비전 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="9df0d-124">미리 구성 하는 hello 솔루션 청구 가능한 Azure 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="9df0d-125">Tooremove 완료 되 면 구독에서 미리 구성 된 솔루션을 hello 반드시 tooavoid 불필요 한 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="9df0d-126">Hello를 방문 하 여 구독에서 미리 구성 된 솔루션을 완전히 제거할 수 <https://www.azureiotsuite.com/> 페이지.</span><span class="sxs-lookup"><span data-stu-id="9df0d-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="9df0d-127">Hello 모니터링 솔루션 원격 hello에 대 한 프로세스를 프로 비전 완료 되 면, 클릭 **시작** 브라우저에서 tooopen hello 솔루션 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![솔루션 대시보드][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="9df0d-129">Hello 원격 모니터링 솔루션에서에서 장치를 프로 비전</span><span class="sxs-lookup"><span data-stu-id="9df0d-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="9df0d-130">솔루션에 장치가 이미 프로비전되어 있으면 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="9df0d-131">Hello 클라이언트 응용 프로그램을 만들 때 tooknow hello에 대 한 장치 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="9df0d-132">장치 tooconnect toohello 미리 구성 된 솔루션을 식별 해야 합니다 자체 tooIoT 허브 유효한 자격 증명을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="9df0d-133">Hello 솔루션 대시보드에서 hello 장치 자격 증명을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="9df0d-134">이 자습서의 뒷부분에 나오는 클라이언트 응용 프로그램에 hello 장치 자격 증명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="9df0d-135">hello 솔루션 대시보드에 전체 hello 다음 단계를 장치 tooyour 원격 모니터링 솔루션 tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="9df0d-136">Hello 왼쪽 아래 모퉁이의 hello 대시보드, 클릭 **장치 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![장치 추가][1]
2. <span data-ttu-id="9df0d-138">Hello에 **사용자 지정 장치** 에서 **새로 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![사용자 지정 장치 추가][2]
3. <span data-ttu-id="9df0d-140">**직접 나만의 장치 ID 정의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="9df0d-141">같은 장치 ID를 입력 **mydevice**, 클릭 **ID 확인** tooverify 해당 이름을 이미와에 없는 사용 클릭 **만들기** tooprovision hello 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![장치 ID 추가][3]
4. <span data-ttu-id="9df0d-143">참고 hello 장치 자격 증명 (장치 ID, IoT 허브 호스트 이름 및 장치 키)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="9df0d-144">클라이언트 응용 프로그램 모니터링 솔루션 원격 이러한 값 tooconnect toohello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="9df0d-145">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-145">Then click **Done**.</span></span>
   
    ![장치 자격 증명 보기][4]
5. <span data-ttu-id="9df0d-147">Hello 솔루션 대시보드에 hello 장치 목록에서 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="9df0d-148">그런 다음, hello **장치 세부 정보** 에서 **장치 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="9df0d-149">현재 장치의 hello 상태는 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="9df0d-150">원격 모니터링 솔루션 hello 수 이제 장치에서 원격 분석을 수신 하 고 hello 장치에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="9df0d-151">빌드 및 hello C 샘플 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="9df0d-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="9df0d-152">hello 다음 지침에서는 설명 hello 연결 하는 단계는 [mbed 사용이 가능한 Freescale FRDM-K64F] [ lnk-mbed-home] 장치 toohello 원격 모니터링 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="9df0d-153">Hello mbed 장치 tooyour 네트워크 및 데스크톱 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="9df0d-154">Hello mbed 장치 tooyour 네트워크 이더넷 케이블을 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="9df0d-155">이 단계는 hello 샘플 응용 프로그램에는 인터넷 액세스가 필요 하기 때문에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="9df0d-156">참조 [mbed 시작] [ lnk-mbed-getstarted] tooconnect mbed 장치 tooyour 데스크톱 PC입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="9df0d-157">데스크톱 컴퓨터에서 Windows를 실행 중인 경우 참조 [PC 구성] [ lnk-mbed-pcconnect] tooconfigure 직렬 포트 액세스 tooyour mbed 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="9df0d-158">Mbed 프로젝트를 만들고 hello 샘플 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="9df0d-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="9df0d-159">이러한 단계 tooadd 일부 샘플 코드 tooan mbed 프로젝트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="9df0d-160">Hello 원격 모니터링 시작 프로젝트를 가져오고 hello 프로젝트 toouse hello MQTT 프로토콜 대신 AMQP 프로토콜 hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="9df0d-161">현재 toouse hello MQTT 프로토콜 toouse hello 장치 관리 기능에 IoT Hub 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="9df0d-162">웹 브라우저에서 toohello mbed.org 이동 [개발자 사이트](https://developer.mbed.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="9df0d-163">아직 등록 하지 않은, 옵션 toocreate (에 무료) 계정 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="9df0d-164">그렇지 않은 경우 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="9df0d-165">클릭 **컴파일러** hello hello 페이지의 상단 오른쪽 모서리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="9df0d-166">이 작업을 통해 toohello 있습니다 *작업 영역* 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="9df0d-167">Hello 하드웨어 플랫폼을 사용 하는 hello hello 창의 상단 오른쪽 모서리에 나타나거나 하드웨어 플랫폼 hello 오른쪽 tooselect hello 아이콘을 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="9df0d-168">클릭 **가져오기** hello 주 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="9df0d-169">클릭 **tooimport URL에서 여기를 클릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![가져오기 toombed 작업 영역을 시작 합니다.][6]

1. <span data-ttu-id="9df0d-171">Hello 팝업 창에서 샘플 코드 https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ hello에 대 한 hello 링크를 입력 한 다음 클릭 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![샘플 코드 toombed 작업 영역 가져오기][7]

1. <span data-ttu-id="9df0d-173">이 프로젝트를 가져오는 다양 한 라이브러리도 가져옵니다 hello mbed 컴파일러 창에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="9df0d-174">일부 제공 되 고 hello Azure IoT 팀에서 유지 관리 ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), 타사 라이브러리 hello mbed 라이브러리 카탈로그에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![mbed 프로젝트 보기][8]

1. <span data-ttu-id="9df0d-176">Hello에 **프로그램 작업 영역**를 마우스 오른쪽 단추로 클릭 hello **iothub\_amqp\_전송** 라이브러리 클릭 **삭제**, 를클릭한다음**확인** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="9df0d-177">Hello에 **프로그램 작업 영역**를 마우스 오른쪽 단추로 클릭 hello **azure\_amqp\_c** 라이브러리 클릭 **삭제**, 클릭 하 고 **확인**  tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="9df0d-178">마우스 오른쪽 단추로 클릭 hello **remote_monitoring** hello에서 프로젝트 **프로그램 작업 영역**선택, **가져오기 라이브러리**을 선택한 후 **From URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![라이브러리 가져오기 toombed 작업 영역을 시작 합니다.][6]

1. <span data-ttu-id="9df0d-180">Hello 팝업 창에 hello 링크 MQTT 전송 라이브러리 https://developer.mbed.org/users/AzureIoTClient/code/iothub hello에 대 한 입력\_mqtt\_전송 / 클릭 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![라이브러리 toombed 작업 영역 가져오기][12]

1. <span data-ttu-id="9df0d-182">반복 hello 이전 단계 tooadd hello MQTT에서에서 라이브러리 https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="9df0d-183">이제 작업 영역 hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-183">Your workspace now looks like hello following:</span></span>

    ![mbed 작업 영역 보기][13]

1. <span data-ttu-id="9df0d-185">원격 열기 hello\_monitoring\remote_monitoring.c 파일과 바꾸기 hello 기존 `#include` 코드 다음 hello로 문:</span><span class="sxs-lookup"><span data-stu-id="9df0d-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="9df0d-186">코드 원격 hello에 남은 모든 hello 삭제\_monitoring\remote\_monitoring.c 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="9df0d-187">빌드 및 실행 hello 샘플</span><span class="sxs-lookup"><span data-stu-id="9df0d-187">Build and run hello sample</span></span>

<span data-ttu-id="9df0d-188">추가 코드 tooinvoke hello **원격\_모니터링\_실행** 함수 로컬 폴더를 빌드하고 hello 장치 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="9df0d-189">추가 **주** 함수 hello 원격의 hello 끝에 다음 코드로\_monitoring.c 파일 tooinvoke hello **원격\_모니터링\_실행** 함수:</span><span class="sxs-lookup"><span data-stu-id="9df0d-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="9df0d-190">클릭 **컴파일** toobuild hello 프로그램.</span><span class="sxs-lookup"><span data-stu-id="9df0d-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="9df0d-191">모든 경고를 무시 하는 hello 빌드 오류를 생성 하는 경우 계속 하기 전에 수정 안전 하 게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="9df0d-192">Hello 빌드에 성공한 경우 hello mbed 컴파일러 웹 사이트는 프로젝트의 hello 이름의.bin 파일을 생성 하 고 tooyour 로컬 컴퓨터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="9df0d-193">Hello.bin 파일 toohello 장치에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="9df0d-194">Hello.bin 파일 toohello 장치 저장 hello 장치 toorestart 시키고 hello.bin 파일에 포함 된 hello 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="9df0d-195">언제 든 지 프로그램 hello를 다시 시작할 hello mbed 장치에 hello 다시 설정 단추를 눌러 수동으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="9df0d-196">Toohello 장치 PuTTY 같은 SSH 클라이언트 응용 프로그램을 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="9df0d-197">Windows 장치 관리자를 선택 하 여 장치를 사용 하는 hello 직렬 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="9df0d-198">PuTTY를 hello 클릭 **직렬** 연결 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="9df0d-199">9600bps에서 일반적으로 연결 하는 hello 장치, hello에 9600를 입력 하므로 **속도** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="9df0d-200">그런 다음 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-200">Then click **Open**.</span></span>

1. <span data-ttu-id="9df0d-201">hello 프로그램 실행을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-201">hello program starts executing.</span></span> <span data-ttu-id="9df0d-202">Hello 프로그램 시작 되지 않으면 자동으로 연결 하는 경우 tooreset hello 보드 (CTRL + Break 또는 키를 눌러 hello 보드의 다시 설정 단추 누름) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df0d-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
