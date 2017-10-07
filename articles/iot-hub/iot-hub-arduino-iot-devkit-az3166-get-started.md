---
title: "aaaIoT 하세요 toocloud IoT 하세요 AZ3166 연결 tooAzure IoT 허브 | Microsoft Docs"
description: "자세한 내용은 방법 toosetup이이 자습서에서는 toosend 데이터 toohello Azure 클라우드 플랫폼에 대 한 IoT 하세요 AZ3166 tooAzure IoT 허브를 연결 합니다."
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
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="18148-103">IoT 하세요 AZ3166 tooAzure hello 클라우드에서 IoT 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="18148-104">hello [MXChip IoT 하세요](https://microsoft.github.io/azure-iot-developer-kit/) 수 사용된 toodevelop 및 프로토타입 Microsoft Azure 서비스 활용 하 여 인터넷 IoT (사물) 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="18148-105">풍부한 주변 장치 및 센서가 있는 Arduino 호환 보드, 오픈 소스 보드 패키지 및 증가하는 [프로젝트 카탈로그](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="18148-106">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="18148-106">What you do</span></span>
<span data-ttu-id="18148-107">연결 [하세요](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT 허브를 만들고, 센서의 온도 및 습도 데이터 수집 hello hello 데이터 tooIoT 허브 송신 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="18148-108">DevKit가 아직 없으세요?</span><span class="sxs-lookup"><span data-stu-id="18148-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="18148-109">[여기](https://aka.ms/iot-devkit-purchase)에서 새 DevKit를 받으세요.</span><span class="sxs-lookup"><span data-stu-id="18148-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="18148-110">학습 내용</span><span class="sxs-lookup"><span data-stu-id="18148-110">What you learn</span></span>

* <span data-ttu-id="18148-111">어떻게 tooconnect IoT 하세요 tooWireless 액세스 가리킨 개발 환경을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="18148-112">어떻게 toocreate IoT hub MXChip IoT 하세요에 장치를 등록 하십시오.</span><span class="sxs-lookup"><span data-stu-id="18148-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="18148-113">어떻게 MXChip IoT 하세요에서 샘플 응용 프로그램을 실행 하 여 toocollect 센서 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="18148-114">어떻게 toosend hello 센서 데이터 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="18148-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="18148-115">What you need</span></span>

* <span data-ttu-id="18148-116">마이크로 USB 케이블을 사용하는 MXChip IoT DevKit 보드.</span><span class="sxs-lookup"><span data-stu-id="18148-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="18148-117">지금 사용</span><span class="sxs-lookup"><span data-stu-id="18148-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="18148-118">Windows 10 또는 macOS 10.10+를 실행하는 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="18148-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="18148-119">활성 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="18148-119">An active Azure subscription</span></span>
  * <span data-ttu-id="18148-120">[30일 평가판 Microsoft Azure 계정](https://azureinfo.microsoft.com/us-freetrial.html) 활성화</span><span class="sxs-lookup"><span data-stu-id="18148-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="18148-121">하드웨어 준비</span><span class="sxs-lookup"><span data-stu-id="18148-121">Prepare your hardware</span></span>

<span data-ttu-id="18148-122">Hello 하드웨어 tooyour 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="18148-123">필요한 하드웨어</span><span class="sxs-lookup"><span data-stu-id="18148-123">Hardware you need</span></span>

* <span data-ttu-id="18148-124">DevKit 보드</span><span class="sxs-lookup"><span data-stu-id="18148-124">DevKit board</span></span>
* <span data-ttu-id="18148-125">Micro USB 케이블</span><span class="sxs-lookup"><span data-stu-id="18148-125">Micro USB cable</span></span>

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="18148-127">하세요 tooyour 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="18148-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="18148-128">USB 끝 tooyour PC를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="18148-129">마이크로 USB 끝 toohello 하세요 연결</span><span class="sxs-lookup"><span data-stu-id="18148-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="18148-130">hello 녹색 led가 다음 toopower 연결 확인</span><span class="sxs-lookup"><span data-stu-id="18148-130">hello green LED next toopower confirms connection</span></span>

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="18148-132">WiFi 구성</span><span class="sxs-lookup"><span data-stu-id="18148-132">Configure WiFi</span></span>

<span data-ttu-id="18148-133">IoT 프로젝트는 인터넷 연결에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="18148-134">다음 지침 tooconfigure hello 하세요 tooconnect tooWiFi hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="18148-135">AP 모드로 전환</span><span class="sxs-lookup"><span data-stu-id="18148-135">Enter AP Mode</span></span>

<span data-ttu-id="18148-136">단추 B 키를 누른 채, 푸시 및 릴리스 hello 단추를 선택한 다음 릴리스 단추 2. 그런 다음 다시 설정 프로그램 하세요 WiFi 구성 AP 모드 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="18148-137">hello 구성 포털 IP 주소 뿐만 아니라 hello hello 하세요의 서비스 설정 Identifier(SSID) hello 화면 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="18148-139">TooDevKit AP를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="18148-140">이제 다른 WiFi 사용 장치 (PC 또는 모바일 폰) tooconnect toohello 하세요 SSID (또한 위의 스크린 샷에서 hello에 강조 표시)를 사용 하 여, hello 암호를 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="18148-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="18148-142">DevKit용 WiFi 구성</span><span class="sxs-lookup"><span data-stu-id="18148-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="18148-143">PC 또는 모바일 폰 브라우저에서 hello 하세요 화면에 표시 된 hello open IP 주소, hello 하세요 tooconnect 원하는 hello WiFi 네트워크를 선택한 다음 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="18148-144">클릭 **연결** toocomplete:</span><span class="sxs-lookup"><span data-stu-id="18148-144">Click **Connect** toocomplete:</span></span>

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="18148-146">Hello 연결에 성공 hello 하세요 몇 초 후에 다시 부팅 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="18148-147">성공한 경우 hello 화면에 hello WiFi 이름 및 IP 주소를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="18148-149">hello 사진에 표시 된 hello IP 주소가 hello 실제 IP 할당 및 hello 하세요 화면에 표시 된 일치 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18148-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="18148-150">이 정상으로 WiFi 사용 하 여 DHCP toodynamically Ip를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="18148-151">WiFi을 구성한 후 자격 증명 분리 하는 경우에 해당 연결에 대 한 hello 장치에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="18148-152">예를 들어 집에 hello 하세요 WiFi에 대 한 구성 후 hello 하세요 toohello office 걸린 경우 tooreconfigure AP 모드 해야 합니다 (단계부터 **AP 모드 입력**) tooconnect hello tooyour office WiFi 하세요.</span><span class="sxs-lookup"><span data-stu-id="18148-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="18148-153">DevKit 사용 시작</span><span class="sxs-lookup"><span data-stu-id="18148-153">Start using DevKit</span></span>

<span data-ttu-id="18148-154">하세요에서 실행 되는 hello 기본 앱 hello 최신 펌웨어 버전을 hello 확인 하 고 사용자에 대 한 일부 센서 진단 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="18148-155">Toohello 최신 펌웨어를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="18148-156">필요한 업그레이드 하는 경우 최신 펌웨어 버전을 hello 둘 다 hello 화면에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="18148-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="18148-157">에 따라 [펌웨어를 업그레이드](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) tooupgrade 안내 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="18148-159">이 단일 작업 hello 하세요에서 개발을 시작 하면 되며 앱 업로드, hello 최신 펌웨어 응용 프로그램과 함께 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="18148-160">다양한 센서 테스트</span><span class="sxs-lookup"><span data-stu-id="18148-160">Test various sensors</span></span>

<span data-ttu-id="18148-161">Tootest 센서 단추 B 눌러, 각 센서를 통해 hello B 단추 toocycle를 눌렀다 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="18148-163">개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="18148-163">Prepare development environment</span></span>

<span data-ttu-id="18148-164">Hello 개발 환경을 시간 tooset 이제: 도구와 toobuild 멋진 IoT 응용 프로그램에 대 한 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="18148-165">Windows 또는 macOS 버전 tooyour 운영 체제에 따라 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18148-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="18148-166">Windows</span><span class="sxs-lookup"><span data-stu-id="18148-166">Windows</span></span>

<span data-ttu-id="18148-167">하면 toouse hello 설치 패키지 tooprepare hello 개발 환경을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18148-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="18148-168">문제가 발생 하는 경우 참고할 수 hello [수동 단계](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="18148-169">최신 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="18148-169">Download latest package</span></span>

<span data-ttu-id="18148-170">hello `.zip` 모든 필요한 도구와 패키지 하세요 개발에 필요한 다운로드 한 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="18148-171">다운로드</span><span class="sxs-lookup"><span data-stu-id="18148-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="18148-172">hello `.zip` hello 다음을 포함 하는 파일 도구와 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="18148-173">이미 일부 구성 요소가 설치 되어 있으면 hello 스크립트에서는 검색 하 고을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="18148-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="18148-174">Node.js 및 Yarn: hello 설치 스크립트 및 자동화 된 작업에 대 한 런타임</span><span class="sxs-lookup"><span data-stu-id="18148-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="18148-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -MSI hello Azure 리소스를 관리 하기 위한 플랫폼 간 명령줄 환경을 종속 Python 및 pip를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="18148-176">[Visual Studio Code](https://code.visualstudio.com/): DevKit 개발을 위한 간단한 코드 편집기</span><span class="sxs-lookup"><span data-stu-id="18148-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="18148-177">[Arduino용 Visual Studio Code 확장](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): VS Code에서 Arduino 개발 활성화</span><span class="sxs-lookup"><span data-stu-id="18148-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="18148-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello 확장 Arduino에 대 한이 도구에 사용</span><span class="sxs-lookup"><span data-stu-id="18148-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="18148-179">하세요 보드 패키지: 도구 체인, 라이브러리 및 프로젝트 형식에 hello 하세요</span><span class="sxs-lookup"><span data-stu-id="18148-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="18148-180">ST 링크 유틸리티: 필수 유틸리티 및 드라이버</span><span class="sxs-lookup"><span data-stu-id="18148-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="18148-181">설치 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="18148-181">Run installation script</span></span>

<span data-ttu-id="18148-182">Windows 파일 탐색기에서 찾아 hello `.zip` 압축을 풀고, 찾기 및 `install.cmd`마우스 오른쪽 단추로 클릭 **"관리자 권한으로 실행"** toostart 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="18148-184">설치 하는 동안 각 도구 또는 패키지의 hello 진행률을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-184">During installation, you will see hello progress of each tool or package.</span></span>

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="18148-186">Tooinstall 드라이버를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="18148-187">VS Code Arduino 확장에 대 한 hello hello Arduino IDE에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="18148-188">인 경우 hello hello Arduino IDE를 설치 하는 처음으로 증명된 tooinstall 관련 드라이버 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18148-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="18148-190">인터넷 속도 따라 약 10 분 toofinish 설치를 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="18148-191">Hello 설치가 완료 되 면 Visual Studio Code 및 Arduino IDE 바로 가기를 바탕 화면에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="18148-192">경우에 따라서 VS Code를 시작할 때 Arduino IDE 또는 관련된 보드 패키지를 찾을 수 없다는 오류와 함께 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="18148-193">VS Code 및 toosolve Arduino IDE를 한 번 시작 닫기 VS Code 것을 찾아야 Arduino IDE 경로 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="18148-194">macOS(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="18148-194">macOS (Preview)</span></span>

<span data-ttu-id="18148-195">이러한 단계 tooprepare 개발 환경을 macOS에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="18148-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="18148-196">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="18148-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="18148-197">Hello에 따라 [공식 가이드](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="18148-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="18148-198">`curl` 명령 하나로 Azure CLI 2.0을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="18148-199">하 고 변경 내용 tootake 효과 대 한 명령 셸에서 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="18148-200">Arduino IDE 설치</span><span class="sxs-lookup"><span data-stu-id="18148-200">Install Arduino IDE</span></span>

<span data-ttu-id="18148-201">Visual Studio 코드 Arduino 확장 hello hello Arduino IDE에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="18148-202">다운로드 및 설치 hello [macOS 용 Arduino IDE](https://www.arduino.cc/en/Main/Software)합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="18148-203">Visual Studio Code 설치</span><span class="sxs-lookup"><span data-stu-id="18148-203">Install Visual Studio Code</span></span>

<span data-ttu-id="18148-204">[macOS용 Visual Studio Code](https://code.visualstudio.com/)를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="18148-205">하세요 IoT 응용 프로그램을 구축 하기 위한 기본 개발 도구 hello 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="18148-206">최신 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="18148-206">Download latest package</span></span>

1. <span data-ttu-id="18148-207">Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-207">Install Node.js.</span></span> <span data-ttu-id="18148-208">인기 있는 macOS 패키지 관리자를 사용할 수 있습니다 [Homebrew](https://brew.sh/) 또는 [설치 관리자 미리 만들어진](https://nodejs.org/en/download/) tooinstall 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="18148-209">VS Code에서 DevKit 개발에 필요한 작업 스크립트를 포함하는 `.zip` 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="18148-210">다운로드</span><span class="sxs-lookup"><span data-stu-id="18148-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="18148-211">Hello 찾을 `.zip` 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="18148-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="18148-212">다음 실행 **터미널** 앱과 명령을 tooconfigure 다음 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="18148-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="18148-213">압축 푼된 폴더 tooyour macOS 사용자 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="18148-214">`npm` 패키지 설치:</span><span class="sxs-lookup"><span data-stu-id="18148-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="18148-215">Arduino용 VS Code 확장 설치</span><span class="sxs-lookup"><span data-stu-id="18148-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="18148-216">Visual Studio Code 있습니다 tooinstall 마켓플레이스 확장 hello 도구에 직접, 단순히 hello 왼쪽된 메뉴 창의 hello 확장 아이콘을 클릭 한 다음 검색 `Arduino` tooinstall:</span><span class="sxs-lookup"><span data-stu-id="18148-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="18148-218">DevKit 보드 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="18148-218">Install DevKit board package</span></span>

<span data-ttu-id="18148-219">Tooadd hello 하세요 보드 hello 보드 관리자를 사용 하 여 Visual Studio Code에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="18148-220">사용 하 여 `Cmd+Shift+P` tooinvoke 명령 팔레트과 형식 **Arduino** 다음 찾아 선택 **Arduino: 보드 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="18148-221">클릭 **' Url을 추가로 '** 오른쪽 hello 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18148-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="18148-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="18148-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="18148-223">Hello에 `settings.json` 파일, hello 아래쪽에 선을 추가 `USER SETTINGS` 창 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="18148-225">이제 'az3166' hello 보드 관리자에서에서 검색 하 고 hello 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="18148-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="18148-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="18148-227">이제 모든 hello 필요한 도구 및 macOS에 설치 된 패키지를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="18148-228">프로젝트 폴더 열기</span><span class="sxs-lookup"><span data-stu-id="18148-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="18148-229">VS Code 시작</span><span class="sxs-lookup"><span data-stu-id="18148-229">Launch VS Code</span></span>

<span data-ttu-id="18148-230">DevKit이 연결되어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="18148-231">VS Code를 처음 시작 하 고 hello 하세요 tooyour 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="18148-232">VS Code는 자동으로 찾고 소개 페이지를 팝업합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="18148-234">경우에 따라서 VS Code를 시작할 때 Arduino IDE 또는 관련된 보드 패키지를 찾을 수 없다는 오류와 함께 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="18148-235">toosolve Arduino IDE를 한 번 다시 시작이 닫기 VS Code 및 VS Code을 찾아야 Arduino IDE 경로 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="18148-236">Arduino 예제 폴더 열기</span><span class="sxs-lookup"><span data-stu-id="18148-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="18148-237">너무 전환**' Arduino 예제 '** 탭, 너무 탐색`Examples for MXCHIP AZ3166 > AzureIoT` 을 클릭할 `GetStarted`합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="18148-239">Tooclose hello 창에서 문제가 발생 하는 경우 tooreload 것을 사용 하 여 `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke 명령 팔레트과 형식 **Arduino** toofind 선택 **Arduino: 예제**합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="18148-240">Azure 서비스 프로비전</span><span class="sxs-lookup"><span data-stu-id="18148-240">Provision Azure services</span></span>

<span data-ttu-id="18148-241">Hello 솔루션 창에서 작업을 통해 실행 `Ctrl+P` (macOS: `Cmd+P`) '클라우드를 프로 비전 작업'를 입력 하 여:</span><span class="sxs-lookup"><span data-stu-id="18148-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="18148-242">Hello VS Code 터미널 대화형 명령줄은 과정을 안내 하 프로비저닝 hello Azure 서비스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="18148-244">Arduino 스케치 빌드 및 업로드</span><span class="sxs-lookup"><span data-stu-id="18148-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="18148-245">필요한 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="18148-245">Install required library</span></span>

1. <span data-ttu-id="18148-246">키를 눌러 `F1` 또는 `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke 명령 팔레트과 형식 **Arduino** 다음 찾아 선택 **Arduino: 라이브러리 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="18148-247">`ArduinoJson` 라이브러리를 검색하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="18148-248">빌드 및 hello 장치 코드 업로드</span><span class="sxs-lookup"><span data-stu-id="18148-248">Build and upload hello device code</span></span>

<span data-ttu-id="18148-249">사용 하 여 `Ctrl+P` (macOS: `Cmd+P`) toorun ' 작업 장치 저장소에 자동 업로드 '.</span><span class="sxs-lookup"><span data-stu-id="18148-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="18148-250">hello 터미널 tooenter 구성 모드 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="18148-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="18148-251">toodo A, 단추, 누른 다음 푸시 및 릴리스 hello 단추를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="18148-252">hello 화면에는 '구성' 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="18148-253">' 작업 클라우드 프로 비전 ' 단계에서 검색 하는 tooset hello 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="18148-254">다음을 확인 하 고 hello Arduino 스케치 업로드 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18148-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="18148-256">hello 하세요 재부팅 되며 hello 코드 실행을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="18148-257">테스트 hello 프로젝트</span><span class="sxs-lookup"><span data-stu-id="18148-257">Test hello project</span></span>

<span data-ttu-id="18148-258">VS Code hello 상태 표시줄 tooopen hello 직렬 모니터의 hello 전원 플러그 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="18148-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="18148-259">hello 결과 뒤에 표시 되 면 hello 샘플 응용 프로그램을 성공적으로 실행:</span><span class="sxs-lookup"><span data-stu-id="18148-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="18148-260">hello 직렬 모니터 디스플레이 hello 아래 스크린샷에서 hello의 hello 내용으로 동일한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="18148-261">hello MXChip IoT 하세요 LED가 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![VS Code의 최종 출력](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="18148-263">문제 및 피드백</span><span class="sxs-lookup"><span data-stu-id="18148-263">Problems and feedback</span></span>

<span data-ttu-id="18148-264">찾을 수 있습니다 [Faq](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) 교류할 toous hello 채널 아래에서 문제가 발생 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="18148-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18148-265">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18148-265">Next steps</span></span>

<span data-ttu-id="18148-266">성공적 MXChip IoT 하세요 tooyour IoT 허브를 연결 하 고 보낸된 hello 캡처된 센서 데이터 tooyour IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="18148-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="18148-267">시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="18148-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="18148-268">iothub-explorer를 사용하여 클라우드 장치 메시지 관리</span><span class="sxs-lookup"><span data-stu-id="18148-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="18148-269">데이터 저장소 tooAzure IoT Hub 메시지 저장</span><span class="sxs-lookup"><span data-stu-id="18148-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="18148-270">Azure IoT 허브에서 Power BI toovisualize 실시간 센서 데이터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="18148-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="18148-271">Azure IoT 허브에서 Azure 웹 앱 toovisualize 실시간 센서 데이터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="18148-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="18148-272">IoT 허브에서 hello 센서 데이터를 사용 하 여 Azure 기계 학습에서 일기 예보</span><span class="sxs-lookup"><span data-stu-id="18148-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="18148-273">iothub-explorer를 사용하여 장치 관리</span><span class="sxs-lookup"><span data-stu-id="18148-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="18148-274">Logic Apps를 사용하여 원격 모니터링 및 알림</span><span class="sxs-lookup"><span data-stu-id="18148-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)