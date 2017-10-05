---
title: "IoT DevKit에서 클라우드로 - Azure IoT Hub에 IoT DevKit AZ3166 연결 | Microsoft Docs"
description: "이 자습서에서는 Azure 클라우드 플랫폼으로 데이터를 보내기 위해 DevKit AZ3166을 설정하고 해당 Azure IoT Hub에 연결하는 방법을 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: 122fac584ac5b954ef7b33a3121bee2c502ebc63
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-iot-devkit-az3166-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="ae7ed-103">클라우드에서 Azure IoT Hub에 IoT DevKit AZ3166 연결</span><span class="sxs-lookup"><span data-stu-id="ae7ed-103">Connect IoT DevKit AZ3166 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="ae7ed-104">Microsoft Azure 서비스를 활용하는 IoT(사물 인터넷) 솔루션을 개발하고 프로토타입하는 데 [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-104">The [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used to develop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="ae7ed-105">풍부한 주변 장치 및 센서가 있는 Arduino 호환 보드, 오픈 소스 보드 패키지 및 증가하는 [프로젝트 카탈로그](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="ae7ed-106">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="ae7ed-106">What you do</span></span>
<span data-ttu-id="ae7ed-107">사용자가 만드는 Azure IoT Hub에 [DevKit](https://microsoft.github.io/azure-iot-developer-kit/)을 연결하고 센서에서 온도 및 습도 데이터를 수집하고 데이터를 IoT 허브로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) to an Azure IoT hub that you create, collect the temperature and humidity data from sensors and send the data to IoT hub.</span></span>

<span data-ttu-id="ae7ed-108">DevKit가 아직 없으세요?</span><span class="sxs-lookup"><span data-stu-id="ae7ed-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="ae7ed-109">[여기](https://aka.ms/iot-devkit-purchase)에서 새 DevKit를 받으세요.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="ae7ed-110">학습 내용</span><span class="sxs-lookup"><span data-stu-id="ae7ed-110">What you learn</span></span>

* <span data-ttu-id="ae7ed-111">IoT DevKit를 무선 액세스 지점에 연결하고 개발 환경을 준비하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-111">How to connect IoT DevKit to Wireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="ae7ed-112">IoT Hub를 만들고 MXChip IoT DevKit용 장치를 등록하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-112">How to create an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="ae7ed-113">MXChip IoT DevKit에서 샘플 응용 프로그램을 실행하여 센서 데이터를 수집하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-113">How to collect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="ae7ed-114">IoT Hub로 센서 데이터를 보내는 방법</span><span class="sxs-lookup"><span data-stu-id="ae7ed-114">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ae7ed-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="ae7ed-115">What you need</span></span>

* <span data-ttu-id="ae7ed-116">마이크로 USB 케이블을 사용하는 MXChip IoT DevKit 보드.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="ae7ed-117">지금 사용</span><span class="sxs-lookup"><span data-stu-id="ae7ed-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="ae7ed-118">Windows 10 또는 macOS 10.10+를 실행하는 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ae7ed-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="ae7ed-119">활성 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="ae7ed-119">An active Azure subscription</span></span>
  * <span data-ttu-id="ae7ed-120">[30일 평가판 Microsoft Azure 계정](https://azureinfo.microsoft.com/us-freetrial.html) 활성화</span><span class="sxs-lookup"><span data-stu-id="ae7ed-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="ae7ed-121">하드웨어 준비</span><span class="sxs-lookup"><span data-stu-id="ae7ed-121">Prepare your hardware</span></span>

<span data-ttu-id="ae7ed-122">컴퓨터에 하드웨어를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-122">Hook up the hardware to your computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="ae7ed-123">필요한 하드웨어</span><span class="sxs-lookup"><span data-stu-id="ae7ed-123">Hardware you need</span></span>

* <span data-ttu-id="ae7ed-124">DevKit 보드</span><span class="sxs-lookup"><span data-stu-id="ae7ed-124">DevKit board</span></span>
* <span data-ttu-id="ae7ed-125">Micro USB 케이블</span><span class="sxs-lookup"><span data-stu-id="ae7ed-125">Micro USB cable</span></span>

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-to-your-computer"></a><span data-ttu-id="ae7ed-127">DevKit를 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="ae7ed-127">Connect DevKit to your computer</span></span>

1. <span data-ttu-id="ae7ed-128">USB 끝을 PC에 연결</span><span class="sxs-lookup"><span data-stu-id="ae7ed-128">Connect USB end to your PC</span></span>
2. <span data-ttu-id="ae7ed-129">Micro USB 끝을 DevKit에 연결</span><span class="sxs-lookup"><span data-stu-id="ae7ed-129">Connect Micro USB end to the DevKit</span></span>
3. <span data-ttu-id="ae7ed-130">연결을 확인하는 전원 옆에 있는 녹색 LED</span><span class="sxs-lookup"><span data-stu-id="ae7ed-130">The green LED next to power confirms connection</span></span>

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="ae7ed-132">WiFi 구성</span><span class="sxs-lookup"><span data-stu-id="ae7ed-132">Configure WiFi</span></span>

<span data-ttu-id="ae7ed-133">IoT 프로젝트는 인터넷 연결에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="ae7ed-134">다음 지침을 사용하여 DevKit를 WiFi에 연결하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-134">Use the following instructions to configure the DevKit to connect to WiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="ae7ed-135">AP 모드로 전환</span><span class="sxs-lookup"><span data-stu-id="ae7ed-135">Enter AP Mode</span></span>

<span data-ttu-id="ae7ed-136">단추 B를 길게 누른 다음 다시 설정 단추를 눌러서 놓고 단추 B를 놓습니다. DevKit은 WiFi 구성을 위해 AP 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-136">Hold down button B, then push and release the reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="ae7ed-137">화면은 구성 포털 IP 주소와 함께 DevKit의 SSID(서비스 설정 식별자)를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-137">The screen will display the Service Set Identifier(SSID) of the DevKit as well as the configuration portal IP address:</span></span>

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-to-devkit-ap"></a><span data-ttu-id="ae7ed-139">DevKit AP에 연결</span><span class="sxs-lookup"><span data-stu-id="ae7ed-139">Connect to DevKit AP</span></span>

<span data-ttu-id="ae7ed-140">이제 다른 WiFi 사용 장치(PC 또는 휴대폰)를 사용하여 DevKit SSID(위 스크린샷에 강조 표시됨)에 연결합니다. 암호는 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-140">Now, use another WiFi enabled device (PC or mobile phone) to connect to the DevKit SSID (highlighted in the screenshot above), leave the password empty.</span></span>

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="ae7ed-142">DevKit용 WiFi 구성</span><span class="sxs-lookup"><span data-stu-id="ae7ed-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="ae7ed-143">PC 또는 모바일 폰 브라우저에서 DevKit 화면에 표시된 IP 주소를 열고, DevKit에서 연결하려는 WiFi 네트워크를 선택한 다음 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-143">Open the IP address shown on the DevKit screen on your PC or mobile phone browser, select the WiFi network you want the DevKit to connect to, then type the password.</span></span> <span data-ttu-id="ae7ed-144">**연결**을 클릭하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-144">Click **Connect** to complete:</span></span>

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="ae7ed-146">연결에 성공하면 DevKit은 몇 초 후에 다시 부팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-146">Once the connection succeeds, the DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="ae7ed-147">성공한 경우 화면에 WiFi 이름 및 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-147">If succeeded, you will see the WiFi name and IP address on the screen:</span></span>

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="ae7ed-149">사진에 표시된 IP 주소는 DevKit 화면에 할당되고 표시되는 실제 IP와 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-149">The IP address displayed in the photo may not match the actual IP assigned and displayed on the DevKit screen.</span></span> <span data-ttu-id="ae7ed-150">WiFi는 DHCP를 사용하여 동적으로 IP를 할당하므로 이는 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-150">This is normal as WiFi uses DHCP to dynamically assign IPs.</span></span>

<span data-ttu-id="ae7ed-151">WiFi를 구성한 후 자격 증명은 분리되는 경우에도 해당 연결에 대해 장치에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-151">After WiFi is configured, your credentials will be persisted on the device for that connection, even if unplugged.</span></span> <span data-ttu-id="ae7ed-152">예를 들어 집에서 WiFi에 대해 DevKit를 구성한 다음 DevKit를 사무실에 가져간 경우 AP 모드를 다시 구성하여(**AP 모드로 전환** 단계에서 시작) DevKit를 사무실 WiFi에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-152">For example, if you configured the DevKit for WiFi in your home and then took the DevKit to the office, you will need to reconfigure AP mode (starting at step **Enter AP Mode**) to connect the DevKit to your office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="ae7ed-153">DevKit 사용 시작</span><span class="sxs-lookup"><span data-stu-id="ae7ed-153">Start using DevKit</span></span>

<span data-ttu-id="ae7ed-154">DevKit에서 실행 중인 기본 앱은 최신 버전의 펌웨어를 확인하고 일부 센서 진단 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-154">The default app running on DevKit will check the latest version of the firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-to-the-latest-firmware"></a><span data-ttu-id="ae7ed-155">최신 펌웨어로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="ae7ed-155">Upgrade to the latest firmware</span></span>

<span data-ttu-id="ae7ed-156">필요한 업그레이드가 있는 경우 현재 및 최신 펌웨어 버전이 모두 화면에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-156">You will be prompted on the screen both the current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="ae7ed-157">[펌웨어 업그레이드](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) 가이드를 따라 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide to upgrade it.</span></span>

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="ae7ed-159">이는 일회성 작업입니다. DevKit 개발을 시작하고 앱을 업로드하면 앱과 함께 최신 펌웨어가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-159">This is a one-time effort, once you start developing on the DevKit and upload your app, you will have the latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="ae7ed-160">다양한 센서 테스트</span><span class="sxs-lookup"><span data-stu-id="ae7ed-160">Test various sensors</span></span>

<span data-ttu-id="ae7ed-161">단추 B를 눌러 센서를 테스트하고 단추 B를 계속해서 눌렀다 놓아 각 센서를 순환합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-161">Press button B to test sensors, continue pressing and releasing the B button to cycle through each sensor.</span></span>

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="ae7ed-163">개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="ae7ed-163">Prepare development environment</span></span>

<span data-ttu-id="ae7ed-164">이제 IoT 응용 프로그램을 빌드하도록 개발 환경(도구 및 패키지)을 설정할 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-164">Now it's time to set up the development environment: tools and packages for you to build stunning IoT applications.</span></span> <span data-ttu-id="ae7ed-165">운영 체제에 따라 Windows 또는 macOS 버전을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-165">You can choose Windows or macOS version according to your operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="ae7ed-166">Windows</span><span class="sxs-lookup"><span data-stu-id="ae7ed-166">Windows</span></span>

<span data-ttu-id="ae7ed-167">설치 패키지를 사용하여 개발 환경을 준비하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-167">We encourage you to use the installation package to prepare the development environment.</span></span> <span data-ttu-id="ae7ed-168">문제가 발생하는 경우 [수동 단계](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/)를 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-168">If you encounter any issues, you can follow the [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) to get it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="ae7ed-169">최신 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="ae7ed-169">Download latest package</span></span>

<span data-ttu-id="ae7ed-170">다운로드한 `.zip` 파일은 DevKit 개발에 필요한 모든 필요한 도구 및 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-170">The `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="ae7ed-171">다운로드</span><span class="sxs-lookup"><span data-stu-id="ae7ed-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="ae7ed-172">`.zip` 파일은 다음 도구 및 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-172">The `.zip` file contains the following tools and packages.</span></span> <span data-ttu-id="ae7ed-173">이미 일부 구성 요소를 설치한 경우 스크립트에서 이를 검색하고 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-173">If you already have some components installed, the script will detect and skip them.</span></span>
> * <span data-ttu-id="ae7ed-174">Node.js 및 Yarn: 설치 스크립트 및 자동화된 작업에 대한 런타임</span><span class="sxs-lookup"><span data-stu-id="ae7ed-174">Node.js and Yarn: Runtime for the setup script and automated tasks</span></span>
> * <span data-ttu-id="ae7ed-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Azure 리소스를 관리하기 위한 플랫폼 간 명령줄 환경, MSI는 종속 Python 및 pip를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, the MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="ae7ed-176">[Visual Studio Code](https://code.visualstudio.com/): DevKit 개발을 위한 간단한 코드 편집기</span><span class="sxs-lookup"><span data-stu-id="ae7ed-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="ae7ed-177">[Arduino용 Visual Studio Code 확장](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): VS Code에서 Arduino 개발 활성화</span><span class="sxs-lookup"><span data-stu-id="ae7ed-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="ae7ed-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): Arduino에 대한 확장은 이 도구에 의존함</span><span class="sxs-lookup"><span data-stu-id="ae7ed-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): The extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="ae7ed-179">DevKit 보드 패키지: DevKit에 대한 도구 체인, 라이브러리 및 프로젝트</span><span class="sxs-lookup"><span data-stu-id="ae7ed-179">DevKit Board Package: Tool chains, libraries and projects for the DevKit</span></span>
> * <span data-ttu-id="ae7ed-180">ST 링크 유틸리티: 필수 유틸리티 및 드라이버</span><span class="sxs-lookup"><span data-stu-id="ae7ed-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="ae7ed-181">설치 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="ae7ed-181">Run installation script</span></span>

<span data-ttu-id="ae7ed-182">Windows 파일 탐색기에서 `.zip`를 찾고 압축을 풀어 `install.cmd`를 찾고 **"관리자 권한으로 실행"**을 마우스 오른쪽 단추로 클릭하고 선택하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-182">In Windows File Explorer, locate the `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** to start.</span></span>

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="ae7ed-184">설치하는 동안 각 도구 또는 패키지의 진행 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-184">During installation, you will see the progress of each tool or package.</span></span>

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-to-install-drivers"></a><span data-ttu-id="ae7ed-186">드라이버 설치 확인</span><span class="sxs-lookup"><span data-stu-id="ae7ed-186">Confirm to install drivers</span></span>

<span data-ttu-id="ae7ed-187">Arduino 확장에 대한 VS Code는 Arduino IDE에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-187">The VS Code for Arduino extension relies on the Arduino IDE.</span></span> <span data-ttu-id="ae7ed-188">Arduino IDE를 처음 설치하는 경우 관련 드라이버를 설치하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-188">If this is the first time you are installing the Arduino IDE, you will be prompted to install relevant drivers:</span></span>

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="ae7ed-190">인터넷 속도에 따라 설치를 완료하는 데 약 10분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-190">It should take around 10 minutes to finish installation depending on your Internet speed.</span></span> <span data-ttu-id="ae7ed-191">설치가 완료되면 바탕 화면에 Visual Studio Code 및 Arduino IDE 바로 가기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-191">Once the installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="ae7ed-192">경우에 따라서 VS Code를 시작할 때 Arduino IDE 또는 관련된 보드 패키지를 찾을 수 없다는 오류와 함께 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="ae7ed-193">이를 해결하기 위해 VS Code를 닫고 Arduino IDE를 한 번 시작하면 VS Code는 Arduino IDE 경로를 올바르게 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-193">To solve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="ae7ed-194">macOS(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="ae7ed-194">macOS (Preview)</span></span>

<span data-ttu-id="ae7ed-195">이 단계를 따라 macOS에서 개발 환경을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-195">Follow these steps to prepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="ae7ed-196">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="ae7ed-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="ae7ed-197">[공식 가이드](https://docs.microsoft.com//cli/azure/install-azure-cli)를 따라 Azure CLI 2.0을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-197">Follow the [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) to install Azure CLI 2.0:</span></span>

<span data-ttu-id="ae7ed-198">`curl` 명령 하나로 Azure CLI 2.0을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="ae7ed-199">변경 내용을 적용하기 위해 명령 셸을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-199">And restart your command shell for changes to take effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="ae7ed-200">Arduino IDE 설치</span><span class="sxs-lookup"><span data-stu-id="ae7ed-200">Install Arduino IDE</span></span>

<span data-ttu-id="ae7ed-201">Visual Studio Code Arduino 확장은 Arduino IDE에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-201">The Visual Studio Code Arduino extension relies on the Arduino IDE.</span></span> <span data-ttu-id="ae7ed-202">[macOS용 Arduino IDE](https://www.arduino.cc/en/Main/Software)를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-202">Download and install the [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="ae7ed-203">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="ae7ed-203">Install Visual Studio Code</span></span>

<span data-ttu-id="ae7ed-204">[macOS용 Visual Studio Code](https://code.visualstudio.com/)를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="ae7ed-205">이는 DevKit IoT 응용 프로그램을 구축하기 위한 기본 개발 도구가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-205">This will be the primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="ae7ed-206">최신 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="ae7ed-206">Download latest package</span></span>

1. <span data-ttu-id="ae7ed-207">Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-207">Install Node.js.</span></span> <span data-ttu-id="ae7ed-208">인기 있는 macOS 패키지 관리자 [Homebrew](https://brew.sh/) 또는 [미리 빌드된 설치 관리자](https://nodejs.org/en/download/)를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) to install it.</span></span>

2. <span data-ttu-id="ae7ed-209">VS Code에서 DevKit 개발에 필요한 작업 스크립트를 포함하는 `.zip` 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="ae7ed-210">다운로드</span><span class="sxs-lookup"><span data-stu-id="ae7ed-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="ae7ed-211">`.zip`를 찾고 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-211">Locate the `.zip` and extract it.</span></span> <span data-ttu-id="ae7ed-212">그런 다음 **터미널** 앱을 실행하고 다음 명령을 실행하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-212">Then launch **Terminal** app and run the following commands to configure:</span></span>

   <span data-ttu-id="ae7ed-213">압축을 푼 폴더를 macOS 사용자 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-213">Move extracted folder to your macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="ae7ed-214">`npm` 패키지 설치:</span><span class="sxs-lookup"><span data-stu-id="ae7ed-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="ae7ed-215">Arduino용 VS Code 확장 설치</span><span class="sxs-lookup"><span data-stu-id="ae7ed-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="ae7ed-216">Visual Studio Code를 사용하면 도구에서 직접 Marketplace 확장을 설치하고 왼쪽 메뉴 창에서 간단히 확장 아이콘을 클릭한 다음 `Arduino`를 검색하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-216">Visual Studio Code allows you to install Marketplace extensions directly in the tool, simply click the extensions icon in the left menu pane and then search `Arduino` to install:</span></span>

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="ae7ed-218">DevKit 보드 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="ae7ed-218">Install DevKit board package</span></span>

<span data-ttu-id="ae7ed-219">Visual Studio Code에서 보드 관리자를 사용하여 DevKit 보드를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-219">You will need to add the DevKit board using the Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="ae7ed-220">`Cmd+Shift+P`를 사용하여 명령 팔레트를 호출하고 **Arduino**를 입력한 다음 찾아서 **Arduino: 보드 관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-220">Use `Cmd+Shift+P` to invoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="ae7ed-221">오른쪽 아래에서 **'추가 URL'**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-221">Click **'Additional URLs'** at the bottom right.</span></span>
   <span data-ttu-id="ae7ed-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="ae7ed-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="ae7ed-223">`settings.json` 파일에서 `USER SETTINGS` 창의 아래쪽에 줄을 추가하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-223">In the `settings.json` file, add a line at the bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="ae7ed-225">이제 보드 관리자에서 'az3166'을 검색하고 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-225">Now in the Board Manager search for 'az3166' and install the latest version.</span></span>
   <span data-ttu-id="ae7ed-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="ae7ed-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="ae7ed-227">이제 macOS에 대해 필요한 모든 도구 및 패키지를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-227">You now have all the necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="ae7ed-228">프로젝트 폴더 열기</span><span class="sxs-lookup"><span data-stu-id="ae7ed-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="ae7ed-229">VS Code 시작</span><span class="sxs-lookup"><span data-stu-id="ae7ed-229">Launch VS Code</span></span>

<span data-ttu-id="ae7ed-230">DevKit이 연결되어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="ae7ed-231">VS Code를 먼저 시작하고 DevKit를 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-231">Launch VS Code first and connect the DevKit to your computer.</span></span> <span data-ttu-id="ae7ed-232">VS Code는 자동으로 찾고 소개 페이지를 팝업합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="ae7ed-234">경우에 따라서 VS Code를 시작할 때 Arduino IDE 또는 관련된 보드 패키지를 찾을 수 없다는 오류와 함께 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="ae7ed-235">이를 해결하기 위해 VS Code를 닫고 Arduino IDE를 다시 한 번 시작하면 VS Code는 Arduino IDE 경로를 올바르게 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-235">To solve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="ae7ed-236">Arduino 예제 폴더 열기</span><span class="sxs-lookup"><span data-stu-id="ae7ed-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="ae7ed-237">**'Arduino 예제'** 탭으로 전환하고 `Examples for MXCHIP AZ3166 > AzureIoT`로 이동하고 `GetStarted`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-237">Switch to **'Arduino Examples'** tab, navigate to `Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="ae7ed-239">창이 닫힌 경우 다시 로드하려면 `Ctrl+Shift+P`(macOS: `Cmd+Shift+P`)를 사용하여 명령 팔레트를 호출하고 **Arduino**를 입력하여 찾아서 **Arduino: 예제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-239">If you happen to close the pane, to reload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to invoke command palette and type **Arduino** to find and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="ae7ed-240">Azure 서비스 프로비전</span><span class="sxs-lookup"><span data-stu-id="ae7ed-240">Provision Azure services</span></span>

<span data-ttu-id="ae7ed-241">솔루션 창에서 'task cloud-provision'을 입력하여 `Ctrl+P`(macOS: `Cmd+P`)를 통해 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-241">In the solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="ae7ed-242">VS Code 터미널에서 대화형 명령줄은 필요한 Azure 서비스를 프로비전하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-242">In the VS Code terminal, an interactive command line will guide you through provisioning the required Azure services:</span></span>

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="ae7ed-244">Arduino 스케치 빌드 및 업로드</span><span class="sxs-lookup"><span data-stu-id="ae7ed-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="ae7ed-245">필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="ae7ed-245">Install required library</span></span>

1. <span data-ttu-id="ae7ed-246">`F1` 또는 `Ctrl+Shift+P`(macOS: `Cmd+Shift+P`)를 눌러 명령 팔레트를 호출하고 **Arduino**를 입력한 다음 찾아서 **Arduino: 라이브러리 관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to invoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="ae7ed-247">`ArduinoJson` 라이브러리를 검색하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-the-device-code"></a><span data-ttu-id="ae7ed-248">장치 코드 빌드 및 업로드</span><span class="sxs-lookup"><span data-stu-id="ae7ed-248">Build and upload the device code</span></span>

<span data-ttu-id="ae7ed-249">`Ctrl+P`(macOS: `Cmd+P`)를 사용하여 'task device-upload'를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-249">Use `Ctrl+P` (macOS: `Cmd+P`) to run 'task device-upload'.</span></span> <span data-ttu-id="ae7ed-250">터미널에서 구성 모드를 입력하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-250">The terminal will prompt you to enter configuration mode.</span></span> <span data-ttu-id="ae7ed-251">이렇게 하려면 단추 A를 누르고 있다가 다시 설정 단추를 밀어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-251">To do so, hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="ae7ed-252">화면에 '구성'이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-252">The screen will display 'Configuration'.</span></span> <span data-ttu-id="ae7ed-253">이는 'task cloud-provision' 단계에서 검색하는 연결 문자열을 설정하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-253">This is to set the connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="ae7ed-254">그런 다음 Arduino 스케치 확인 및 업로드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-254">Then it will start verifying and uploading the Arduino sketch:</span></span>

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="ae7ed-256">DevKit가 재부팅되고 코드 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-256">The DevKit will reboot and start running the code.</span></span>

## <a name="test-the-project"></a><span data-ttu-id="ae7ed-257">프로젝트 테스트</span><span class="sxs-lookup"><span data-stu-id="ae7ed-257">Test the project</span></span>

<span data-ttu-id="ae7ed-258">VS Code에서 상태 표시줄의 전원 플러그 아이콘을 클릭하여 직렬 모니터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-258">In VS Code, click the power plug icon on the status bar to open the Serial Monitor.</span></span>

<span data-ttu-id="ae7ed-259">다음과 같은 결과가 표시되면 샘플 응용 프로그램은 성공적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-259">The sample application is running successfully when you see the following results:</span></span>

* <span data-ttu-id="ae7ed-260">직렬 모니터는 아래 스크린샷의 내용으로 동일한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-260">The Serial Monitor displays the same information as the content in the screenshot below.</span></span>
* <span data-ttu-id="ae7ed-261">MXChip IoT DevKit의 LED가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-261">The LED on MXChip IoT DevKit is blinking.</span></span>

![VS Code의 최종 출력](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="ae7ed-263">문제 및 피드백</span><span class="sxs-lookup"><span data-stu-id="ae7ed-263">Problems and feedback</span></span>

<span data-ttu-id="ae7ed-264">문제가 발생했거나 아래 채널에서 연락하려는 경우 [FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/)를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out to us from the channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae7ed-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae7ed-265">Next steps</span></span>

<span data-ttu-id="ae7ed-266">IoT Hub에 MXChip IoT DevKit를 성공적으로 연결하고 캡처된 센서 데이터를 IoT Hub에 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-266">You have successfully connected an MXChip IoT DevKit to your IoT Hub, and sent the captured sensor data to your IoT hub.</span></span>

<span data-ttu-id="ae7ed-267">계속해서 IoT Hub을 시작하고 다른 IoT 시나리오를 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-267">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="ae7ed-268">iothub-explorer를 사용하여 클라우드 장치 메시지 관리</span><span class="sxs-lookup"><span data-stu-id="ae7ed-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="ae7ed-269">IoT Hub 메시지를 Azure 데이터 저장소에 저장</span><span class="sxs-lookup"><span data-stu-id="ae7ed-269">Save IoT Hub messages to Azure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="ae7ed-270">Power BI를 사용하여 Azure IoT Hub에서 실시간 센서 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="ae7ed-270">Use Power BI to visualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="ae7ed-271">Azure Web Apps를 사용하여 Azure IoT Hub에서 실시간 센서 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="ae7ed-271">Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="ae7ed-272">Azure Machine Learning에서 IoT Hub의 센서 데이터를 사용한 날씨 예측</span><span class="sxs-lookup"><span data-stu-id="ae7ed-272">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="ae7ed-273">iothub-explorer를 사용하여 장치 관리</span><span class="sxs-lookup"><span data-stu-id="ae7ed-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="ae7ed-274">Logic Apps를 사용하여 원격 모니터링 및 알림</span><span class="sxs-lookup"><span data-stu-id="ae7ed-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)