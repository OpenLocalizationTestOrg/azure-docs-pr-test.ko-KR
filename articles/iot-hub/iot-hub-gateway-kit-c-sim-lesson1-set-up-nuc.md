---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 1: NUC 설정 | Microsoft Docs"
description: "Intel NUC를 센서와 Azure IoT Hub 사이의 IoT 게이트웨이로 작동하도록 설정하여 센서 정보를 수집하고 IoT Hub에 보냅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: "iot 게이트웨이, intel nuc, nuc 컴퓨터, DE3815TYKE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="389d7-104">Intel NUC를 IoT 게이트웨이로 설정</span><span class="sxs-lookup"><span data-stu-id="389d7-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="389d7-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="389d7-105">What you will do</span></span>

- <span data-ttu-id="389d7-106">Intel NUC를 IoT 게이트웨이로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="389d7-107">Intel NUC에 Azure IoT Edge 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="389d7-108">게이트웨이 기능을 확인하려면 Intel NUC에서 "hello_world" 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="389d7-109">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="389d7-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="389d7-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="389d7-110">What you will learn</span></span>

<span data-ttu-id="389d7-111">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="389d7-112">Intel NUC와 주변 장치를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="389d7-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="389d7-113">스마트 패키지 관리자를 사용하여 Intel NUC에 필요한 패키지를 설치 및 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="389d7-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="389d7-114">게이트웨이 기능을 확인하기 위해 "hello_world" 샘플 응용 프로그램을 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="389d7-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="389d7-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="389d7-115">What you need</span></span>

- <span data-ttu-id="389d7-116">사전 설치된 Intel IoT 게이트웨이 소프트웨어 제품군을 포함하는 Intel NUC 키트 DE3815TYKE(Wind River Linux * 7.0.0.13)</span><span class="sxs-lookup"><span data-stu-id="389d7-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="389d7-117">이더넷 케이블</span><span class="sxs-lookup"><span data-stu-id="389d7-117">An Ethernet cable.</span></span>
- <span data-ttu-id="389d7-118">키보드</span><span class="sxs-lookup"><span data-stu-id="389d7-118">A keyboard.</span></span>
- <span data-ttu-id="389d7-119">HDMI 또는 VGA 케이블</span><span class="sxs-lookup"><span data-stu-id="389d7-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="389d7-120">HDMI 또는 VGA 포트가 있는 모니터</span><span class="sxs-lookup"><span data-stu-id="389d7-120">A monitor with an HDMI or VGA port.</span></span>

![게이트웨이 키트](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="389d7-122">주변 장치와 연결된 Intel NUC</span><span class="sxs-lookup"><span data-stu-id="389d7-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="389d7-123">아래 이미지는 다양한 주변 장치가 연결된 Intel NUC의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="389d7-124">키보드에 연결됨</span><span class="sxs-lookup"><span data-stu-id="389d7-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="389d7-125">VGA 또는 HDMI 케이블 모니터에 연결됨</span><span class="sxs-lookup"><span data-stu-id="389d7-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="389d7-126">이더넷 케이블을 통해 유선된 네트워크에 연결됨</span><span class="sxs-lookup"><span data-stu-id="389d7-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="389d7-127">전원 케이블로 전원 공급 장치에 연결됨</span><span class="sxs-lookup"><span data-stu-id="389d7-127">Connected to the power supply with a power cable.</span></span>

![주변 장치에 연결된 Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="389d7-129">SSH(보안 셸)를 통해 호스트 컴퓨터에서 Intel NUC 시스템에 연결</span><span class="sxs-lookup"><span data-stu-id="389d7-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="389d7-130">NUC 장치의 IP 주소를 얻기 위해 키보드 및 모니터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="389d7-131">IP 주소를 이미 알고 있는 경우 이 섹션의 3단계로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="389d7-132">전원 단추를 눌러 Intel NUC를 켜고 시스템에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="389d7-133">사용자 이름 및 암호는 모두 `root`입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="389d7-134">`ifconfig` 명령을 실행하여 NUC의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="389d7-135">이 단계는 NUC 장치에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="389d7-136">다음은 명령 출력의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-136">Here is an example of the command output.</span></span>

   ![NUC IP를 보여주는 ifconfig 출력](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="389d7-138">이 예제에서는 `inet addr:` 뒤에 나오는 값은 호스트 컴퓨터에서 Intel NUC로 원격 연결을 하려는 경우에 필요한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="389d7-139">호스트 컴퓨터에서 다음 중 하나의 SSH 클라이언트를 사용하여 Intel NUC에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="389d7-140">Windows용 [PuTTY](http://www.putty.org/)입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="389d7-141">Ubuntu 또는 macOS에 있는 기본 제공 SSH 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="389d7-142">호스트 컴퓨터의 Intel NUC에서 작동하기에 보다 효율적이고 생산적입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="389d7-143">IP 주소, 사용자 이름 및 SSH 클라이언트를 통해 NUC 연결할 때 사용할 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="389d7-144">MacOS에서 SSH 클라이언트를 사용하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="389d7-145">![MacOS에서 실행되는 SSH 클라이언트](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="389d7-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="389d7-146">Azure IoT Edge 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="389d7-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="389d7-147">Azure IoT Edge 패키지에는 SDK 및 해당 종속성이 사전 컴파일된 이진 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="389d7-148">이러한 이진 파일은 Azure IoT Edge, Azure IoT SDK 및 해당하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="389d7-149">또한 이 패키지에는 게이트웨이 기능을 확인하는 데 사용되는 "hello_world" 샘플 응용 프로그램이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="389d7-150">IoT Edge는 게이트웨이의 핵심 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="389d7-151">패키지를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="389d7-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="389d7-152">터미널 창에서 다음 명령을 실행하여 IoT 클라우드 저장소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="389d7-153">`rpm` 명령은 rpm 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="389d7-154">`smart channel` 명령은 rpm 채널을 스마트 패키지 관리자에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="389d7-155">`smart update` 명령을 실행하기 전에 아래와 같은 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![rpm 및 스마트 채널 명령 출력](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="389d7-157">다음 명령을 실행하여 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="389d7-158">`packagegroup-cloud-azure`는 패키지의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="389d7-159">`smart install` 명령은 패키지 설치를 설치하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="389d7-160">패키지를 설치한 후 Intel NUC는 게이트웨이로 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="389d7-161">Azure IoT Edge "hello_world" 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="389d7-162">`azureiotgatewaysdk/samples`로 이동하여 샘플 "hello_world" 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="389d7-163">이 샘플 응용 프로그램은 `hello_world.json` 파일에서 게이트웨이를 만들고 Azure IoT Edge 아키텍처의 기본 구성 요소를 사용하여 5초마다 파일에 hellow world 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="389d7-164">다음 명령을 실행하여 샘플 "hello_world" 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="389d7-165">게이트웨이 기능이 올바르게 작동하는 경우 샘플 응용 프로그램은 다음과 같은 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![응용 프로그램 출력](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="389d7-167">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="389d7-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="389d7-168">요약</span><span class="sxs-lookup"><span data-stu-id="389d7-168">Summary</span></span>

<span data-ttu-id="389d7-169">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-169">Congratulations!</span></span> <span data-ttu-id="389d7-170">게이트웨이로 Intel NUC 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="389d7-171">이제 호스트 컴퓨터를 설정하고 Azure IoT hub를 만들고 Azure IoT hub 논리적 장치를 등록하는 다음 단원으로 이동할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="389d7-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="389d7-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="389d7-172">Next steps</span></span>
[<span data-ttu-id="389d7-173">호스트 컴퓨터 및 Azure IoT Hub 준비</span><span class="sxs-lookup"><span data-stu-id="389d7-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
