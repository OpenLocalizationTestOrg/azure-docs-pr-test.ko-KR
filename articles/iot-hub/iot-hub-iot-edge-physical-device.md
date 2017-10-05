---
title: "물리적 장치에서 Azure IoT Edge 사용 | Microsoft Docs"
description: "Texas Instruments SensorTag 장치를 사용하여 Raspberry Pi 3에서 실행되는 IoT Edge 게이트웨이를 통해 IoT Hub로 데이터를 전송하는 방법입니다. 이 게이트웨이는 Azure IoT Edge를 사용하여 빌드됩니다."
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
ms.openlocfilehash: 02962a91c739a53dfcf947bcc736e5c293b9384f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-to-forward-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="45ae1-104">Raspberry Pi에 Azure IoT Edge를 사용하여 IoT Hub에 장치-클라우드 메시지 전달</span><span class="sxs-lookup"><span data-stu-id="45ae1-104">Use Azure IoT Edge on a Raspberry Pi to forward device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="45ae1-105">[Bluetooth 저에너지 샘플][lnk-ble-samplecode]의 이 연습에서는 [Azure IoT Edge][lnk-sdk]를 사용하여 다음을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="45ae1-106">물리적 장치에서 IoT Hub로 장치-클라우드 원격 분석을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="45ae1-107">IoT Hub에서 물리적 장치로 명령을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="45ae1-108">이 연습에서는 다음 내용을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-108">This walkthrough covers:</span></span>

* <span data-ttu-id="45ae1-109">**아키텍처**: Bluetooth 저에너지 샘플에 대한 중요한 아키텍처 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="45ae1-110">**빌드 및 실행**: 샘플을 빌드하고 실행하는 데 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="45ae1-111">아키텍처</span><span class="sxs-lookup"><span data-stu-id="45ae1-111">Architecture</span></span>

<span data-ttu-id="45ae1-112">이 연습은 Raspbian Linux를 실행하는 Raspberry Pi 3에서 IoT Edge 게이트웨이를 빌드하고 실행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-112">The walkthrough shows you how to build and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="45ae1-113">게이트웨이는 IoT Edge를 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-113">The gateway is built using IoT Edge.</span></span> <span data-ttu-id="45ae1-114">이 샘플은 Texas Instruments SensorTag BLE(Bluetooth 저에너지) 장치를 사용하여 온도 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="45ae1-115">IoT Edge 게이트웨이를 실행하면 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-115">When you run the IoT Edge gateway it:</span></span>

* <span data-ttu-id="45ae1-116">BLE(Bluetooth 저에너지) 프로토콜을 사용하여 SensorTag 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="45ae1-117">HTTP 프로토콜을 사용하여 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="45ae1-118">SensorTag 장치에서 IoT Hub로 원격 분석을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="45ae1-119">IoT Hub에서 SensorTag 장치로 명령을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="45ae1-120">게이트웨이에는 다음과 같은 IoT Edge 모듈이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-120">The gateway contains the following IoT Edge modules:</span></span>

* <span data-ttu-id="45ae1-121">*BLE 모듈* - BLE 장치와 연결되며, 장치에서 온도 데이터를 수신하고 장치로 명령을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="45ae1-122">*BLE 클라우드-장치 모듈* - *BLE 모듈*에 대한 BLE 지침으로 IoT Hub에서 전송된 JSON 메시지를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-122">A *BLE cloud to device module* that translates JSON messages sent from IoT Hub into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="45ae1-123">*로거 모듈* - 모든 게이트웨이 메시지를 로컬 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="45ae1-124">*ID 매핑 모듈* - BLE 장치 MAC 주소 및 Azure IoT Hub 장치 ID 간을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="45ae1-125">*IoT Hub 모듈* - IoT hub에 원격 분석 데이터를 업로드하고 IoT hub에서 장치 명령을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="45ae1-126">*BLE 프린터 모듈* - BLE 장치의 원격 분석을 해석하고 형식이 지정된 데이터를 콘솔에 출력하여 문제 해결 및 디버깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="45ae1-127">게이트웨이를 통해 데이터가 흐르는 방식</span><span class="sxs-lookup"><span data-stu-id="45ae1-127">How data flows through the gateway</span></span>

<span data-ttu-id="45ae1-128">다음 블록 다이어그램에서는 원격 분석 업로드 데이터 흐름 파이프라인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![원격 분석 업로드 게이트웨이 파이프라인](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="45ae1-130">원격 분석 항목이 BLE 장치에서 IoT Hub로 이동하면서 진행되는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="45ae1-131">BLE 장치가 온도 샘플을 생성한 후 Bluetooth를 통해 게이트웨이의 BLE 모듈로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="45ae1-132">BLE 모듈이 샘플을 수신한 후 장치의 MAC 주소와 함께 broker에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="45ae1-133">ID 매핑 모듈이 이 메시지를 선택하고 내부 표를 사용하여 장치의 MAC 주소를 IoT Hub 장치 ID로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="45ae1-134">IoT Hub 장치 ID는 장치 ID와 장치 키로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="45ae1-135">ID 매핑 모듈은 온도 샘플 데이터, 장치의 MAC 주소, 장치 ID 및 장치 키가 포함된 새 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-135">The identity mapping module publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="45ae1-136">IoT Hub 모듈은 새 메시지(ID 매핑 모듈에 의해 생성)를 수신한 후 IoT Hub에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="45ae1-137">로거 모듈이 broker의 모든 메시지를 로컬 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="45ae1-138">다음 블록 다이어그램에서는 장치 명령 데이터 흐름 파이프라인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![장치 명령 게이트웨이 파이프라인](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="45ae1-140">IoT Hub 모듈은 새로운 명령 메시지에 대한 IoT Hub를 주기적으로 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="45ae1-141">IoT Hub 모듈은 새 명령 메시지를 받으면 broke에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="45ae1-142">ID 매핑 모듈은 명령 메시지를 선택하고 내부 표를 사용하여 IoT Hub 장치 ID를 장치 MAC 주소로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="45ae1-143">그런 다음 메시지의 속성 맵에 대상 장치의 MAC 주소가 포함된 새 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="45ae1-144">BLE 클라우드-장치 모듈은 이 메시지를 선택해 BLE 모듈에 적합한 BLE 명령으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="45ae1-145">그런 다음 새 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="45ae1-146">BLE 모듈은 이 메시지를 선택하고 BLE 장치와 통신하여 I/O 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="45ae1-147">로거 모듈이 broker의 모든 메시지를 디스크 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45ae1-148">필수 조건</span><span class="sxs-lookup"><span data-stu-id="45ae1-148">Prerequisites</span></span>

<span data-ttu-id="45ae1-149">이 자습서를 완료하려면 활성 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-149">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="45ae1-150">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="45ae1-151">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45ae1-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="45ae1-152">Raspberry Pi의 명령줄에 원격으로 액세스할 수 있도록 데스크톱 컴퓨터에 SSH 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-152">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="45ae1-153">Windows에서는 SSH 클라이언트를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="45ae1-154">[PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="45ae1-155">대부분의 Linux 배포판 및 Mac OS는 명령줄 SSH 유틸리티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-155">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="45ae1-156">자세한 내용은 [Linux 또는 Mac OS를 사용하는 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45ae1-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="45ae1-157">하드웨어 준비</span><span class="sxs-lookup"><span data-stu-id="45ae1-157">Prepare your hardware</span></span>

<span data-ttu-id="45ae1-158">이 자습서에서는 사용자가 Raspbian을 실행하는 Raspberry Pi 3 에 연결된 [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) 장치를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="45ae1-159">Raspbian 설치</span><span class="sxs-lookup"><span data-stu-id="45ae1-159">Install Raspbian</span></span>

<span data-ttu-id="45ae1-160">다음 옵션 중 하나를 사용하여 Raspbian을 Raspberry Pi 3 장치에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-160">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="45ae1-161">최신 버전의 Raspbian을 설치하려면 [NOOBS][lnk-noobs] 그래픽 사용자 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-161">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="45ae1-162">최신 Raspbian 운영 체제 이미지를 수동으로 [다운로드][lnk-raspbian]하고 SD 카드에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-162">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="45ae1-163">터미널 로그인 및 액세스</span><span class="sxs-lookup"><span data-stu-id="45ae1-163">Sign in and access the terminal</span></span>

<span data-ttu-id="45ae1-164">Raspberry Pi의 터미널 환경에 액세스하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-164">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="45ae1-165">키보드 및 모니터가 Raspberry Pi에 연결된 경우 Raspbian GUI를 사용하여 터미널 창에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-165">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

* <span data-ttu-id="45ae1-166">데스크톱 컴퓨터에서 SSH를 사용하여 Raspberry Pi의 명령줄에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-166">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="45ae1-167">GUI에서 터미널 창 사용</span><span class="sxs-lookup"><span data-stu-id="45ae1-167">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="45ae1-168">Raspbian에 대한 기본 자격 증명은 사용자 이름 **pi** 및 암호 **raspberry**입니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-168">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="45ae1-169">GUI의 작업 표시줄에서 모니터 모양의 아이콘을 사용하여 **터미널** 유틸리티를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-169">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="45ae1-170">SSH를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="45ae1-170">Sign in with SSH</span></span>

<span data-ttu-id="45ae1-171">Raspberry Pi에 명령줄 액세스를 위해 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-171">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="45ae1-172">[SSH(Secure Shell)][lnk-pi-ssh] 문서에서는 Raspberry Pi에서 SSH를 구성하는 방법 및 [Windows][lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]에서 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-172">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="45ae1-173">사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="45ae1-174">BlueZ 5.37 설치</span><span class="sxs-lookup"><span data-stu-id="45ae1-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="45ae1-175">BLE 모듈은 BlueZ 스택을 통해 Bluetooth 하드웨어와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-175">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="45ae1-176">모듈이 제대로 작동하려면 BlueZ 버전 5.37이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-176">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="45ae1-177">다음 지침은 올바른 BlueZ 버전이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-177">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="45ae1-178">현재 Bluetooth 디먼을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-178">Stop the current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="45ae1-179">BlueZ 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-179">Install the BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="45ae1-180">bluez.org에서 BlueZ 소스 코드를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-180">Download the BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="45ae1-181">소스 코드 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-181">Unzip the source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="45ae1-182">디렉터리를 새로 생성된 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-182">Change directories to the newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="45ae1-183">빌드할 BlueZ 코드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-183">Configure the BlueZ code to be built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="45ae1-184">BlueZ를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="45ae1-185">빌드가 완료되면 BlueZ를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="45ae1-186">`/lib/systemd/system/bluetooth.service` 파일에서 새로운 Bluetooth 디먼을 가리키도록 Bluetooth에 대한 systemd 서비스 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-186">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="45ae1-187">'ExecStart' 줄을 다음 텍스트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-187">Replace the 'ExecStart' line with the following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="45ae1-188">Raspberry Pi 3 장치에서 SensorTag 장치로 연결 설정</span><span class="sxs-lookup"><span data-stu-id="45ae1-188">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="45ae1-189">이 샘플을 실행하기 전에 Raspberry Pi 3이 SensorTag 장치에 연결할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-189">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>

1. <span data-ttu-id="45ae1-190">`rfkill` 유틸리티가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-190">Ensure the `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="45ae1-191">Raspberry Pi 3에서 Bluetooth를 차단 해제하고 버전 번호가 **5.37**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-191">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="45ae1-192">대화형 Bluetooth 셸을 시작하려면 Bluetooth 서비스를 시작하고 **bluetoothctl** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-192">To enter the interactive bluetooth shell, start the bluetooth service and execute the **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="45ae1-193">**power on** 명령을 입력하여 bluetooth 컨트롤러에 전원을 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-193">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="45ae1-194">명령은 다음과 비슷한 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-194">The command returns output similar to the following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="45ae1-195">대화형 Bluetooth 셸에서 **scan on** 명령을 입력하여 Bluetooth 장치를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-195">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="45ae1-196">명령은 다음과 비슷한 출력을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-196">The command returns output similar to the following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="45ae1-197">작은 단추(녹색 표시등이 깜박거림)를 눌러 SensorTag 장치를 검색 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-197">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="45ae1-198">Raspberry Pi 3은 SensorTag 장치를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-198">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="45ae1-199">이 예제에서는 SensorTag 장치의 MAC 주소가 **A0:E6:F8:B5:F6:00**이라는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-199">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="45ae1-200">**scan off** 명령을 입력하여 스캔을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-200">Turn off scanning by entering the **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="45ae1-201">**connect \<MAC 주소\>**를 입력하고 MAC 주소를 사용하여 SensorTag 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-201">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="45ae1-202">다음 샘플 출력은 명확히 하기 위해 축약형으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-202">The following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting to connect to A0:E6:F8:B5:F6:00
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

    > <span data-ttu-id="45ae1-203">**list-attributes** 명령을 사용하여 장치의 GATT 특성을 다시 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-203">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="45ae1-204">이제 **disconnect** 명령을 사용하여 장치에서 연결을 끊은 다음 **quit** 명령을 사용하여 Bluetooth 셸을 끝낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-204">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```sh
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="45ae1-205">이제 Raspberry Pi 3에서 BLE IoT Edge 샘플을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-205">You're now ready to run the BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-iot-edge-ble-sample"></a><span data-ttu-id="45ae1-206">IoT Edge BLE 샘플 실행</span><span class="sxs-lookup"><span data-stu-id="45ae1-206">Run the IoT Edge BLE sample</span></span>

<span data-ttu-id="45ae1-207">IoT Edge BLE 샘플을 실행하려면 다음 세 가지 작업을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-207">To run the IoT Edge BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="45ae1-208">IoT Hub에서 두 개의 샘플 장치를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="45ae1-209">Raspberry Pi 3 장치에서 IoT Edge를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="45ae1-210">Raspberry Pi 3 장치에서 BLE 샘플을 구성하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-210">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="45ae1-211">작성할 때 IoT Edge는 Linux에서 실행되는 게이트웨이의 BLE 모듈만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-211">At the time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="45ae1-212">IoT Hub에서 두 개의 샘플 장치 구성</span><span class="sxs-lookup"><span data-stu-id="45ae1-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="45ae1-213">Azure 구독에서 [IoT Hub를 만듭니다][lnk-create-hub]. 이 연습을 완료하려면 허브 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="45ae1-214">계정이 없는 경우 몇 분 내에 [계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="45ae1-215">**SensorTag_01**이라는 장치 하나를 IoT hub에 추가하고 해당 ID와 장치 키를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-215">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="45ae1-216">[장치 Explorer 또는 iothub-explorer][lnk-explorer-tools] 도구를 사용하여 이전 단계에서 만든 IoT Hub에 장치를 추가하고 해당 키를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-216">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="45ae1-217">게이트웨이를 구성할 때 이 장치를 SensorTag 장치에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-217">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="45ae1-218">Raspberry Pi 3에서 Azure IoT Edge 빌드</span><span class="sxs-lookup"><span data-stu-id="45ae1-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="45ae1-219">Azure IoT Edge에 대한 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="45ae1-220">다음 명령을 사용하여 IoT Edge 및 모든 하위 모듈을 홈 디렉터리로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-220">Use the following commands to clone IoT Edge and all its submodules to your home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="45ae1-221">Raspberry Pi 3에 IoT Edge 리포지토리의 전체 복사본이 있는 경우 다음 명령을 사용하여 SDK가 포함된 폴더에서 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-221">When you have a complete copy of the IoT Edge repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="45ae1-222">Raspberry Pi 3에서 BLE 샘플 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="45ae1-222">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="45ae1-223">샘플을 부트스트랩하고 실행하려면 게이트웨이에서 참여하는 각 IoT Edge 모듈을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-223">To bootstrap and run the sample, you must configure each IoT Edge module that participates in the gateway.</span></span> <span data-ttu-id="45ae1-224">이 구성은 JSON 파일에 제공되며 참여하는 5가지 IoT Edge 모듈을 모두 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="45ae1-225">리포지토리에는 구성 파일을 직접 작성하기 위한 시작 지점으로 사용할 수 있는 **gateway\_sample.json**이라는 샘플 JSON 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-225">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="45ae1-226">이 파일은 IoT Edge 리포지토리의 로컬 복사본에 있는 **samples/ble_gateway/src** 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-226">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Edge repository.</span></span>

<span data-ttu-id="45ae1-227">다음 섹션에서는 BLE 샘플에 대해 이 구성 파일을 편집하는 방법을 설명하고 IoT Edge 리포지토리가 Raspberry Pi 3의 **/home/pi/iot-edge/** 폴더에 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-227">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Edge repository is in the **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="45ae1-228">리포지토리가 다른 위치에 있으면 그에 맞게 경로를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-228">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="45ae1-229">로거 구성</span><span class="sxs-lookup"><span data-stu-id="45ae1-229">Logger configuration</span></span>

<span data-ttu-id="45ae1-230">게이트웨이 리포지토리가 **/home/pi/iot-edge/** 폴더에 있다고 가정하고 다음과 같이 로거 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-230">Assuming the gateway repository is located in the **/home/pi/iot-edge/** folder, configure the logger module as follows:</span></span>

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

#### <a name="ble-module-configuration"></a><span data-ttu-id="45ae1-231">BLE 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="45ae1-231">BLE module configuration</span></span>

<span data-ttu-id="45ae1-232">BLE 장치에 대한 샘플 구성에서는 Texas Instruments SensorTag 장치를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-232">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="45ae1-233">GATT 주변 기기로 작동할 수 있는 모든 표준 BLE 장치가 작동되어야 하지만 GATT 특성 ID 및 데이터를 업데이트해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need to update the GATT characteristic IDs and data.</span></span> <span data-ttu-id="45ae1-234">SensorTag 장치의 MAC 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-234">Add the MAC address of your SensorTag device:</span></span>

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

<span data-ttu-id="45ae1-235">SensorTag 장치를 사용하지 않는 경우 BLE 장치에 대한 설명서를 검토하여 GATT 특성 ID 및 데이터 값을 업데이트해야 하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-235">If you are not using a SensorTag device, review the documentation for your BLE device to determine whether you need to update the GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="45ae1-236">IoT Hub 모듈</span><span class="sxs-lookup"><span data-stu-id="45ae1-236">IoT Hub module</span></span>

<span data-ttu-id="45ae1-237">IoT Hub의 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-237">Add the name of your IoT Hub.</span></span> <span data-ttu-id="45ae1-238">일반적으로 접미사 값은 **azure-devices.net**입니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-238">The suffix value is typically **azure-devices.net**:</span></span>

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

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="45ae1-239">ID 매핑 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="45ae1-239">Identity mapping module configuration</span></span>

<span data-ttu-id="45ae1-240">SensorTag 장치의 MAC 주소와 IoT Hub에 추가된 **SensorTag_01** 장치의 장치 ID 및 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-240">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

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

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="45ae1-241">BLE 프린터 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="45ae1-241">BLE Printer module configuration</span></span>

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

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="45ae1-242">BLEC2D 모듈 구성</span><span class="sxs-lookup"><span data-stu-id="45ae1-242">BLEC2D Module Configuration</span></span>

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

#### <a name="routing-configuration"></a><span data-ttu-id="45ae1-243">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="45ae1-243">Routing Configuration</span></span>

<span data-ttu-id="45ae1-244">다음 구성은 IoT Edge 모듈 간에 다음과 같은 라우팅을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-244">The following configuration ensures the following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="45ae1-245">**로거** 모듈은 모든 메시지를 수신하고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-245">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="45ae1-246">**SensorTag** 모듈은 **매핑** 및 **BLE 프린터** 모듈 둘 다에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-246">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="45ae1-247">**매핑** 모듈은 IoT Hub 보내질 메시지를 **IoTHub** 모듈에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-247">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="45ae1-248">**IoTHub** 모듈은 메시지를 **매핑** 모듈로 돌려 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-248">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="45ae1-249">**mapping** 모듈은 메시지를 **BLEC2D** 모듈에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-249">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="45ae1-250">**BLEC2D** 모듈은 메시지를 **Sensor Tag** 모듈로 돌려 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-250">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

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

<span data-ttu-id="45ae1-251">샘플을 실행하려면 JSON 구성 파일에 대한 경로를 매개 변수로 **ble\_gateway** binary에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-251">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="45ae1-252">다음 명령은 **gateway_sample.json** 구성 파일을 사용하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-252">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="45ae1-253">Raspberry Pi의 **iot-edge** 폴더에서 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-253">Execute this command from the **iot-edge** folder on the Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="45ae1-254">샘플을 실행하기 전에 SensorTag 장치에 있는 작은 단추를 눌러 검색을 가능하게 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-254">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="45ae1-255">샘플을 실행할 경우 [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 또는 [iothub-explorer](https://github.com/Azure/iothub-explorer) 도구를 사용하여 SensorTag 장치에서 IoT Edge 게이트웨이가 전달하는 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-255">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the IoT Edge gateway forwards from the SensorTag device.</span></span> <span data-ttu-id="45ae1-256">예를 들어 iothub-explorer를 사용하면 다음 명령으로 장치-클라우드 메시지를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-256">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="45ae1-257">클라우드-장치 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="45ae1-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="45ae1-258">또한 BLE 모듈은 IoT Hub에서 장치로 명령을 보내도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-258">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="45ae1-259">[장치 Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 또는 [iothub-explorer](https://github.com/Azure/iothub-explorer) 도구를 사용하여 BLE 게이트웨이 모듈이 BLE 장치에 전달하는 JSON 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-259">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="45ae1-260">Texas Instruments SensorTag 장치를 사용하는 경우 IoT Hub에서 명령을 보내서 빨간색 LED, 녹색 LED 또는 버저를 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-260">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="45ae1-261">IoT Hub에서 명령을 보내기 전에 먼저 다음 두 JSON 메시지를 순서대로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-261">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="45ae1-262">그런 다음 원하는 명령을 보내서 표시등 또는 버저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-262">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="45ae1-263">모든 LED 및 버저 다시 설정(끄기):</span><span class="sxs-lookup"><span data-stu-id="45ae1-263">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="45ae1-264">I/O를 '원격'으로 구성:</span><span class="sxs-lookup"><span data-stu-id="45ae1-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="45ae1-265">이제 다음 명령을 보내서 SensorTag 장치에서 표시등 또는 버저를 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45ae1-265">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="45ae1-266">빨간색 LED 켜기:</span><span class="sxs-lookup"><span data-stu-id="45ae1-266">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="45ae1-267">녹색 LED 켜기:</span><span class="sxs-lookup"><span data-stu-id="45ae1-267">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="45ae1-268">버저 켜기:</span><span class="sxs-lookup"><span data-stu-id="45ae1-268">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="45ae1-269">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45ae1-269">Next Steps</span></span>

<span data-ttu-id="45ae1-270">IoT Edge와 코드 예제 실험에 대해 더욱 심도 있게 이해하고 싶다면 다음 개발자 자습서 및 리소스를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="45ae1-270">If you want to gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="45ae1-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="45ae1-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="45ae1-272">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45ae1-272">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="45ae1-273">[IoT Hub 개발자 가이드][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="45ae1-273">[IoT Hub developer guide][lnk-devguide]</span></span>

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
