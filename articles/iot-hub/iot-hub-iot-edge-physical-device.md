---
title: "Azure IoT 가장자리를 사용 하 여 물리적 장치 aaaUse | Microsoft Docs"
description: "어떻게 toouse 라스베리 Pi 3 장치에서 실행 중인 IoT 지 게이트웨이 통해 텍사스 기기 SensorTag 장치 toosend 데이터 tooan IoT 허브입니다. hello 게이트웨이 Azure IoT 가장자리를 사용 하 여 만들어집니다."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="75181-104">Azure IoT 가장자리 라스베리 Pi tooforward 장치-클라우드 메시지 tooIoT 허브에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="75181-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="75181-105">이 연습에서는 hello의 [Bluetooth 낮은 에너지 샘플] [ lnk-ble-samplecode] 방법을 보여주는 toouse [Azure IoT 가장자리] [ lnk-sdk] 에:</span><span class="sxs-lookup"><span data-stu-id="75181-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="75181-106">실제 장치에서 장치-클라우드 원격 분석 tooIoT 허브를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="75181-107">IoT Hub tooa 물리적 장치에서 명령 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="75181-108">이 연습에서는 다음 내용을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="75181-108">This walkthrough covers:</span></span>

* <span data-ttu-id="75181-109">**아키텍처**: hello Bluetooth 낮은 에너지 샘플에 대 한 중요 한 아키텍처 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="75181-110">**빌드 및 실행**: hello 단계 필요한 toobuild 및 실행된 hello 샘플.</span><span class="sxs-lookup"><span data-stu-id="75181-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="75181-111">아키텍처</span><span class="sxs-lookup"><span data-stu-id="75181-111">Architecture</span></span>

<span data-ttu-id="75181-112">hello 연습 toobuild 및 라스베리 Pi 3에서 IoT 지 게이트웨이 실행 하는 실행 방법을 Raspbian Linux 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75181-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="75181-113">hello 게이트웨이 IoT 가장자리를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="75181-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="75181-114">hello 샘플 텍사스 기기 SensorTag Bluetooth 낮은 에너지 (배포용) 장치 toocollect 온도 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="75181-115">Hello IoT 지 게이트웨이 실행 하는 경우 해당:</span><span class="sxs-lookup"><span data-stu-id="75181-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="75181-116">Hello Bluetooth 낮은 에너지 (배포용) 프로토콜을 사용 하 여 tooa SensorTag 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="75181-117">TooIoT 허브 연결 hello HTTP 프로토콜을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="75181-118">Hello SensorTag 장치 tooIoT 허브에서에서 원격 분석을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="75181-119">IoT Hub toohello SensorTag 장치에서 명령을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="75181-120">hello 게이트웨이 모듈 IoT 가장자리를 따라 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="75181-121">A *배포용 모듈* hello 장치와 송신 명령 toohello 장치에서 배포용 장치 tooreceive 온도 데이터와 교류 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="75181-122">A *배포용 클라우드 toodevice 모듈* hello에 대 한 지침 배포용으로 IoT 허브에서 보낸 JSON 메시지를 변환 하는 *배포용 모듈*합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="75181-123">A *로 거 모듈* 모든 게이트웨이 메시지 tooa 로컬 파일을 기록 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="75181-124">*ID 매핑 모듈* - BLE 장치 MAC 주소 및 Azure IoT Hub 장치 ID 간을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="75181-125">*IoT 허브 모듈* 원격 분석 데이터 tooan IoT 허브를 업로드 하 고 IoT 허브에서 장치 명령을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="75181-126">A *배포용 프린터 모듈* hello 배포용 장치에서 원격 분석을 해석 하 고 형식이 지정 된 데이터 toohello 콘솔 tooenable 문제 해결 및 디버깅 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="75181-127">Hello 게이트웨이 통해 데이터 흐름</span><span class="sxs-lookup"><span data-stu-id="75181-127">How data flows through hello gateway</span></span>

<span data-ttu-id="75181-128">블록 다이어그램을 다음 hello hello 원격 분석 업로드 데이터 흐름 파이프라인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75181-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![원격 분석 업로드 게이트웨이 파이프라인](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="75181-130">원격 분석의 항목 사용 배포용 장치 tooIoT에서 이동 하는 hello 단계 허브가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="75181-131">hello 배포용 장치 온도 샘플에서는 오류가 발생 하 고 hello 게이트웨이에 Bluetooth toohello 배포용 모듈을 통해 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="75181-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="75181-132">hello 배포용 모듈 hello 샘플 받아 toohello 브로커 hello 장치의 hello MAC 주소와 함께 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="75181-133">hello 인식 매핑 모듈이이 메시지를 선택 하 고 IoT Hub 장치 id를 내부 테이블 tootranslate hello hello 장치의 MAC 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="75181-134">IoT Hub 장치 ID는 장치 ID와 장치 키로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="75181-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="75181-135">hello 인식 매핑 모듈 hello 온도 예제 데이터, hello 장치, hello 장치 ID 및 hello 장치 키의 hello MAC 주소를 포함 하는 새 메시지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="75181-136">hello IoT 허브 모듈 (hello 인식 매핑 모듈에서 생성)이 새 메시지를 받아 tooIoT 허브 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="75181-137">hello로 거 모듈 hello 브로커 tooa 로컬 파일에서 모든 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="75181-138">블록 다이어그램을 다음 hello hello 장치 명령 데이터 흐름 파이프라인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75181-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![장치 명령 게이트웨이 파이프라인](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="75181-140">IoT Hub 모듈 주기적으로 폴링하여 hello hello 새 명령 메시지에 대 한 IoT hub 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="75181-141">IoT Hub 모듈 hello 새 명령 메시지를 받으면 게시 것 toohello 브로커 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="75181-142">hello 인식 매핑 모듈 hello 명령 메시지를 선택 하 고 내부 테이블 tootranslate hello IoT Hub 장치 ID tooa 장치 MAC 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="75181-143">그런 다음 hello 메시지의 hello 속성 맵에서 hello 대상 장치의 hello MAC 주소를 포함 하는 새 메시지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="75181-144">hello 배포용 클라우드-장치 모듈이이 메시지를 선택 하 고 hello hello 배포용 모듈에 대 한 적절 한 배포용 명령으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="75181-145">그런 다음 새 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="75181-146">hello 배포용 모듈이이 메시지를 선택 하 고 hello 배포용 장치와 통신 하 여 hello I/O 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="75181-147">hello로 거 모듈 hello 브로커 tooa 디스크 파일에서 모든 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75181-148">필수 조건</span><span class="sxs-lookup"><span data-stu-id="75181-148">Prerequisites</span></span>

<span data-ttu-id="75181-149">toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="75181-150">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="75181-151">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75181-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="75181-152">사용자 데스크톱 컴퓨터 tooenable 있습니다 tooremotely 액세스 hello 명령줄로 라스베리 Pi hello에에 SSH 클라이언트를 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="75181-153">Windows에서는 SSH 클라이언트를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="75181-154">[PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="75181-155">대부분의 Linux 배포판 및 Mac OS 명령줄 SSH 유틸리티 hello를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="75181-156">자세한 내용은 [Linux 또는 Mac OS를 사용하는 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75181-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="75181-157">하드웨어 준비</span><span class="sxs-lookup"><span data-stu-id="75181-157">Prepare your hardware</span></span>

<span data-ttu-id="75181-158">이 자습서에서는 사용 하는 가정는 [텍사스 기기 SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) 장치가 연결 tooa 라스베리 Pi 3 Raspbian를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="75181-159">Raspbian 설치</span><span class="sxs-lookup"><span data-stu-id="75181-159">Install Raspbian</span></span>

<span data-ttu-id="75181-160">Hello 옵션 tooinstall Raspbian 라스베리 Pi 3 장치에서 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="75181-161">tooinstall hello 최신 버전의 Raspbian 사용 하 여 hello [NOOBS] [ lnk-noobs] 그래픽 사용자 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="75181-162">수동으로 [다운로드] [ lnk-raspbian] hello Raspbian 운영 체제 tooan SD 카드의 hello 최신 이미지를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="75181-163">로그인 및 액세스 hello 터미널</span><span class="sxs-lookup"><span data-stu-id="75181-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="75181-164">환경을 사용 하는 두 가지 옵션 tooaccess 터미널 라스베리 원주율:</span><span class="sxs-lookup"><span data-stu-id="75181-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="75181-165">키보드 연결된 tooyour 라스베리 Pi를 모니터링 하는 경우에 hello Raspbian GUI tooaccess 터미널 윈도우를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="75181-166">액세스 hello 명령줄 데스크톱 컴퓨터의 SSH를 사용 하 여 라스베리 원주율입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="75181-167">Hello GUI에서에서 터미널 윈도우를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="75181-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="75181-168">Raspbian에 대 한 hello 기본 자격 증명이 username **pi** 및 암호 **라스베리**합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="75181-169">Hello GUI에에서 hello 작업 표시줄에서 hello를 시작할 수 있습니다 **터미널** hello 모양의 아이콘을 모니터를 사용 하 여 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="75181-170">SSH를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="75181-170">Sign in with SSH</span></span>

<span data-ttu-id="75181-171">명령줄 액세스 tooyour 라스베리 Pi에 대 한 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="75181-172">hello 문서 [SSH (보안 셸)] [ lnk-pi-ssh] 설명 방법을 tooconfigure 라스베리 Pi와의 SSH 방법과에서 tooconnect [Windows] [ lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="75181-173">사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="75181-174">BlueZ 5.37 설치</span><span class="sxs-lookup"><span data-stu-id="75181-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="75181-175">hello 배포용 모듈 hello BlueZ 스택을 통해 toohello Bluetooth 하드웨어와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="75181-176">5.37 BlueZ의 버전에 필요한 hello 모듈 toowork 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="75181-177">이러한 지침은 hello BlueZ의 올바른 버전이 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="75181-178">현재 bluetooth 데몬 hello를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="75181-179">Hello BlueZ 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="75181-180">Bluez.org에서 hello BlueZ 소스 코드를 다운로드 하세요.</span><span class="sxs-lookup"><span data-stu-id="75181-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="75181-181">Hello 소스 코드를 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="75181-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="75181-182">디렉터리 toohello 새로 만든 폴더를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="75181-183">Hello BlueZ 코드 toobe 구축을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="75181-184">BlueZ를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="75181-185">빌드가 완료되면 BlueZ를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="75181-186">Bluetooth hello 파일에서 새 bluetooth 데몬이 toohello 하는 것을 나타내는 되므로 systemd 서비스 구성 변경 `/lib/systemd/system/bluetooth.service`합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="75181-187">Hello 'ExecStart' 줄을 텍스트 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="75181-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="75181-188">라스베리 Pi 3 장치에서 연결 toohello SensorTag 장치 사용</span><span class="sxs-lookup"><span data-stu-id="75181-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="75181-189">실행 중인 hello 샘플 하기 전에 tooverify 라스베리 Pi 3 toohello SensorTag 장치를 연결할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="75181-190">Hello 확인 `rfkill` 유틸리티를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="75181-191">Hello 라스베리 Pi 3에서 bluetooth를 차단을 해제 하 고 hello 버전 번호가 인지 확인 **5.37**:</span><span class="sxs-lookup"><span data-stu-id="75181-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="75181-192">tooenter hello 대화형 bluetooth 셸 hello bluetooth 서비스 시작 및 실행 hello **bluetoothctl** 명령:</span><span class="sxs-lookup"><span data-stu-id="75181-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="75181-193">Hello 명령을 입력 **전원 켜기** toopower hello bluetooth 컨트롤러를 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="75181-194">hello 명령은 유사한 toohello 다음을 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="75181-195">Hello 대화형 bluetooth 셸에서 hello 명령을 입력 **검색 시 검색** tooscan bluetooth 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="75181-196">hello 명령은 유사한 toohello 다음을 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="75181-197">Hello 작은 단추 (녹색 led가 깜박입니다 hello)를 눌러 hello SensorTag 장치 검색 가능 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="75181-198">hello 라스베리 Pi 3 hello SensorTag 장치를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="75181-199">이 예제에서는 해당 hello hello 장치가 SensorTag의 MAC 주소를 확인할 수 있습니다 **A0:E6:F8:B5:F6:00**합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="75181-200">Hello를 입력 하 여 검색 기능을 해제 **오프 스캔** 명령:</span><span class="sxs-lookup"><span data-stu-id="75181-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="75181-201">MAC 주소를 사용 하 여 입력 하 여 tooyour SensorTag 장치 연결 **연결 \<MAC 주소\>**합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="75181-202">다음 샘플 출력 hello은 쉽게 구별할 수 있도록 약어:</span><span class="sxs-lookup"><span data-stu-id="75181-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="75181-203">Hello를 사용 하 여 다시 hello 장치의 hello GATT 특성을 나열할 수 있습니다 **특성 목록** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="75181-204">Hello를 사용 하 여 hello 장치에서 연결을 끊을 이제 수 **연결 끊기** 명령을 클릭 한 다음 종료 hello를 사용 하 여 hello bluetooth 셸에서 **종료** 명령:</span><span class="sxs-lookup"><span data-stu-id="75181-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="75181-205">이 든 이제 준비 toorun hello 배포용 IoT 가장자리 샘플 라스베리 Pi 3입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="75181-206">Hello IoT 가장자리 배포용 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="75181-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="75181-207">toorun hello IoT 가장자리 배포용 샘플 toocomplete 세 가지 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="75181-208">IoT Hub에서 두 개의 샘플 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="75181-209">Raspberry Pi 3 장치에서 IoT Edge를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="75181-210">구성 하 고 라스베리 Pi 3 장치에서 hello 배포용 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="75181-211">작성 hello 시 IoT 가장자리 Linux에서 실행 중인 게이트웨이의 배포용 모듈만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="75181-212">IoT Hub에서 두 개의 샘플 장치 구성</span><span class="sxs-lookup"><span data-stu-id="75181-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="75181-213">[IoT 허브를 만듭니다.] [ lnk-create-hub] Azure 구독에 필요한 허브 toocomplete의 hello 이름을이 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="75181-214">계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="75181-215">라는 하나의 장치 추가 **SensorTag_01** tooyour IoT hub id와 장치 키을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="75181-216">Hello를 사용할 수 있습니다 [장치 탐색기 또는 iothub 탐색기] [ lnk-explorer-tools] tooadd 키 tooretrieve hello 이전 단계에서 만든이 장치 toohello IoT 허브 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="75181-217">Hello 게이트웨이 구성 하는 경우이 장치 toohello SensorTag 장치를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="75181-218">Raspberry Pi 3에서 Azure IoT Edge 빌드</span><span class="sxs-lookup"><span data-stu-id="75181-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="75181-219">Azure IoT Edge에 대한 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="75181-220">사용 하 여 hello 다음 tooclone IoT Edge 및 모든 하위 모듈 tooyour 홈 디렉터리 명령:</span><span class="sxs-lookup"><span data-stu-id="75181-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="75181-221">라스베리 Pi 3에 hello IoT 가장자리 저장소의 전체 복사본을 있을 때 hello hello SDK를 포함 하는 hello 폴더에서 다음 명령을 사용 하 여 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="75181-222">구성 하 고 라스베리 Pi 3에서 hello 배포용 샘플을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="75181-223">toobootstrap 및 실행된 hello 샘플 hello 게이트웨이 참여 하는 각 IoT 지 모듈을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="75181-224">이 구성은 JSON 파일에 제공되며 참여하는 5가지 IoT Edge 모듈을 모두 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="75181-225">Hello 저장소 호출 중인 샘플 JSON 파일 **게이트웨이\_sample.json** hello 구성 파일을 직접 작성의 시작 지점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="75181-226">이 파일은 hello에 **샘플/ble_gateway/src** hello IoT 가장자리 저장소의 로컬 복사본에 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="75181-227">hello 다음 섹션에서는 어떻게이 구성은 hello 배포용 샘플에 대 한 파일을 해당 hello IoT 가장자리 리포지토리 가정 tooedit의에서 설명 hello **/home/pi/iot-edge /** 라스베리 Pi 3에는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="75181-228">Hello 리포지토리는 다른 위치를 hello 경로 적절 하 게 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="75181-229">로거 구성</span><span class="sxs-lookup"><span data-stu-id="75181-229">Logger configuration</span></span>

<span data-ttu-id="75181-230">Hello 게이트웨이 저장소 hello에 있는 것으로 가정 **/home/pi/iot-edge /** 폴더를 다음과 같이 hello로 거 모듈을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="75181-231">BLE 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="75181-231">BLE module configuration</span></span>

<span data-ttu-id="75181-232">hello 배포용 장치에 대 한 샘플 구성 hello 텍사스 기기 SensorTag 장치를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="75181-233">주변는 GATT 작동 해야 하지만 tooupdate hello GATT 특성 Id 및 데이터를 할 수 있습니다으로 작동할 수 있는 모든 표준 배포용 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="75181-234">SensorTag 장치의 hello MAC 주소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-234">Add hello MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="75181-235">SensorTag 장치를 사용 하지 않는 경우 tooupdate hello GATT 특성 Id 및 데이터 값을 필요한 지 배포용 장치 toodetermine에 대 한 hello 설명서를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="75181-236">IoT Hub 모듈</span><span class="sxs-lookup"><span data-stu-id="75181-236">IoT Hub module</span></span>

<span data-ttu-id="75181-237">IoT Hub의 hello 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="75181-238">일반적으로 hello 접미사 값은 **azure devices.net**:</span><span class="sxs-lookup"><span data-stu-id="75181-238">hello suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="75181-239">ID 매핑 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="75181-239">Identity mapping module configuration</span></span>

<span data-ttu-id="75181-240">SensorTag 장치 및 hello 장치 ID 및 키의 hello의 hello MAC 주소를 추가 **SensorTag_01** tooyour IoT 허브를 추가 하는 장치:</span><span class="sxs-lookup"><span data-stu-id="75181-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="75181-241">BLE 프린터 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="75181-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="75181-242">BLEC2D 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="75181-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="75181-243">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="75181-243">Routing Configuration</span></span>

<span data-ttu-id="75181-244">hello 다음 구성을 사용 하면 hello 다음 IoT 가장자리 모듈 간의 라우팅:</span><span class="sxs-lookup"><span data-stu-id="75181-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="75181-245">hello **로 거** 모듈 수신 하 고 모든 메시지를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="75181-246">hello **SensorTag** 모듈 tooboth hello 메시지를 보내는 **매핑** 및 **배포용 프린터** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="75181-247">hello **매핑** 모듈 보내는 메시지 toohello **IoTHub** 모듈 toobe tooyour IoT Hub를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="75181-248">hello **IoTHub** 모듈 toohello 회신 메시지를 보내는 **매핑** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="75181-249">hello **매핑** 모듈 보내는 메시지 toohello **BLEC2D** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="75181-250">hello **BLEC2D** 모듈 toohello 회신 메시지를 보내는 **센서 태그** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="75181-251">매개 변수 toohello 패스 hello 경로 toohello JSON 구성 파일 toorun hello 샘플 **배포용\_게이트웨이** 이진입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="75181-252">hello 다음 명령을 사용 하 고 가정 hello **gateway_sample.json** 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="75181-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="75181-253">Hello에서이 명령을 실행 **iot 가장자리** hello 라스베리 Pi의 폴더:</span><span class="sxs-lookup"><span data-stu-id="75181-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="75181-254">Toopress 야 hello 작은 단추 hello SensorTag 장치 toomake 검색 가능한 것 hello 샘플을 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="75181-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="75181-255">Hello 샘플을 실행 하면 hello를 사용할 수 있습니다 [장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 또는 hello [iothub 탐색기](https://github.com/Azure/iothub-explorer) 도구 toomonitor hello 메시지 hello hello SensorTag 장치에서 IoT 지 게이트웨이 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="75181-256">예를 들어 iothub 탐색기를 사용 하 여 다음 명령을 hello를 사용 하 여 장치-클라우드 메시지 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="75181-257">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="75181-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="75181-258">hello 배포용 모듈에는 또한 IoT Hub toohello 장치에서 보내는 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="75181-259">Hello를 사용할 수 있습니다 [장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 또는 hello [iothub 탐색기](https://github.com/Azure/iothub-explorer) 도구 toosend JSON 메시지 해당 hello 배포용 게이트웨이 모듈 toohello 배포용 장치에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="75181-260">Hello 텍사스 기기 SensorTag 장치를 사용 하는 경우 켤 수 있습니다 hello 빨간색 LED, 녹색 LED 또는 버저 IoT 허브에서 명령을 전송 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="75181-261">IoT 허브에서 명령에 보내기 전에 먼저 hello 다음 순서 대로 두 개의 JSON 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="75181-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="75181-262">그런 다음 hello 명령 tooturn hello lights 또는 버저에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="75181-263">(해제) 하는 모든 Led 형식 및 hello 버저 다시 설정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="75181-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="75181-264">I/O를 '원격'으로 구성:</span><span class="sxs-lookup"><span data-stu-id="75181-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="75181-265">이제 hello 나오는 명령 tooturn hello lights 또는 hello SensorTag 장치에서 버저에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75181-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="75181-266">Hello 빨간색 LED를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="75181-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="75181-267">Hello 녹색 LED를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="75181-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="75181-268">Hello 버저를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75181-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="75181-269">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75181-269">Next Steps</span></span>

<span data-ttu-id="75181-270">원하는 toogain IoT 가장자리에 대 한 자세한 하 고 몇 가지 코드 예제를 시험해 방문 hello 다음 개발자 자습서 및 리소스:</span><span class="sxs-lookup"><span data-stu-id="75181-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="75181-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="75181-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="75181-272">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="75181-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="75181-273">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="75181-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
