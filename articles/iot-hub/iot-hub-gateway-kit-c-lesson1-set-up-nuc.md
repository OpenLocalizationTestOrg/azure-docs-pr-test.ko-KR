---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 1: Intel NUC 설정 | Microsoft Docs"
description: "센서와 Azure IoT Hub toocollect 센서 정보 사이의 IoT 게이트웨이로 Intel NUC toowork를 설정 하 고 tooIoT 허브 전송 됩니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 게이트웨이, intel nuc, nuc 컴퓨터, DE3815TYKE"
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="f792a-104">Intel NUC를 IoT 게이트웨이로 설정</span><span class="sxs-lookup"><span data-stu-id="f792a-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="f792a-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="f792a-105">What you will do</span></span>

- <span data-ttu-id="f792a-106">Intel NUC를 IoT 게이트웨이로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="f792a-107">Intel NUC hello에 hello Azure IoT 가장자리 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="f792a-108">Hello Intel NUC tooverify hello 게이트웨이 기능에는 "hello_world" 예제 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="f792a-109">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f792a-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="f792a-110">What you will learn</span></span>

<span data-ttu-id="f792a-111">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f792a-112">어떻게 tooconnect Intel NUC 주변 장치를 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="f792a-113">어떻게 사용 하 여 Intel NUC tooinstall 및 업데이트 hello 필요한 패키지가 hello 스마트 패키지 관리자.</span><span class="sxs-lookup"><span data-stu-id="f792a-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="f792a-114">어떻게 toorun hello_world"hello" 예제 응용 프로그램 tooverify hello 게이트웨이 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f792a-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="f792a-115">What you need</span></span>

- <span data-ttu-id="f792a-116">Intel IoT 게이트웨이 소프트웨어 제품군 hello로 Intel NUC 키트 DE3815TYKE (바람 강 Linux * 7.0.0.13) 사전 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="f792a-117">[여기를 클릭 toopurchase 나무숲을 조성 IoT 상용 게이트웨이 키트](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="f792a-118">이더넷 케이블</span><span class="sxs-lookup"><span data-stu-id="f792a-118">An Ethernet cable.</span></span>
- <span data-ttu-id="f792a-119">키보드</span><span class="sxs-lookup"><span data-stu-id="f792a-119">A keyboard.</span></span>
- <span data-ttu-id="f792a-120">HDMI 또는 VGA 케이블</span><span class="sxs-lookup"><span data-stu-id="f792a-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="f792a-121">HDMI 또는 VGA 포트가 있는 모니터</span><span class="sxs-lookup"><span data-stu-id="f792a-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="f792a-122">선택 사항: [Texas Instruments SensorTag(CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="f792a-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![게이트웨이 키트](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="f792a-124">Intel NUC hello 주변 장치를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="f792a-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="f792a-125">아래 hello 이미지는 다양 한 주변 장치에 연결 하는 Intel NUC의 예:</span><span class="sxs-lookup"><span data-stu-id="f792a-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="f792a-126">연결 된 tooa 키보드입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="f792a-127">Tooa 모니터 vga 또는 HDMI 케이블을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="f792a-128">연결 된 tooa 유선 네트워크 이더넷 케이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="f792a-129">연결 된 tooa 전원 공급 장치 전원 케이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-129">Connected tooa power supply with a power cable.</span></span>

![Intel NUC tooperipherals 연결](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="f792a-131">호스트 컴퓨터를 통해 SSH (보안 셸)에서 toohello Intel NUC 시스템에 연결</span><span class="sxs-lookup"><span data-stu-id="f792a-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="f792a-132">키보드 및 Intel NUC 장치의 모니터 tooget hello IP 주소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="f792a-133">Hello IP를 이미 알고 있는 경우 주소를 미리 toostep이이 섹션의 3을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="f792a-134">Hello Intel NUC hello 전원 단추를 눌러 켜고에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="f792a-135">hello 기본 사용자 이름과 암호는 모두 `root`합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="f792a-136">Hello를 실행 하 여 hello Intel NUC의 hello IP 주소를 가져올 `ifconfig` hello Intel NUC 장치에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="f792a-137">Hello 명령 출력의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-137">Here is an example of hello command output.</span></span>

   ![Intel NUC IP를 보여 주는 ifconfig 출력](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="f792a-139">이 예제에서는 값 뒤에 오는 hello `inet addr:` toohello Intel NUC 호스트 컴퓨터에서 연결할 때 필요한 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="f792a-140">Hello 호스트 컴퓨터 tooconnect tooIntel NUC에서에서 SSH 클라이언트를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="f792a-141">Windows용 [PuTTY](http://www.putty.org/)</span><span class="sxs-lookup"><span data-stu-id="f792a-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="f792a-142">hello 기본 제공 SSH 클라이언트 Ubuntu 또는 macOS에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="f792a-143">것이 더 효율적이 고 생산적인 toooperate 호스트 컴퓨터에서는 Intel NUC 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="f792a-144">Intel NUC IP 주소 hello 필요 합니다 SSH 클라이언트를 통해 사용자 이름 및 암호 tooconnect tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="f792a-145">macOS에서 SSH 클라이언트를 사용하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="f792a-146">![MacOS에서 실행되는 SSH 클라이언트](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="f792a-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="f792a-147">Hello Azure IoT 가장자리 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="f792a-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="f792a-148">hello Azure IoT 가장자리 패키지 IoT 가장자리와 해당 종속성의 hello 미리 컴파일된 이진 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="f792a-149">이러한 이진 파일은 Azure IoT 가장자리, Azure IoT SDK hello 및 hello 해당 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="f792a-150">hello 패키지도 포함 되어 "hello_world" 샘플 응용 프로그램은 사용 되는 toovalidate hello 게이트웨이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="f792a-151">IoT 가장자리가 hello 게이트웨이의 hello 핵심 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="f792a-152">이러한 단계 tooinstall hello 패키지를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="f792a-153">Hello 명령을 터미널 창에서 다음을 실행 하 여 hello IoT 클라우드 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="f792a-154">입력 'y' too'Include 물을 때이 채널?'</span><span class="sxs-lookup"><span data-stu-id="f792a-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="f792a-155">표시 되 면는 `import read failed(-1)` 오류를 사용 하 여 hello 명령을 tooresolve hello 문제 다음:</span><span class="sxs-lookup"><span data-stu-id="f792a-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="f792a-156">hello `rpm` imports hello rpm 키 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="f792a-157">hello `smart channel` 명령은 hello rpm 채널 toohello 스마트 패키지 관리자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="f792a-158">Hello를 실행 하기 전에 `smart update` 명령, 나타납니다 다음과 유사한 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![rpm 및 스마트 채널 명령 출력](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="f792a-160">Hello 스마트 update 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="f792a-161">Hello 다음 명령을 실행 하 여 hello Azure IoT 게이트웨이 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="f792a-162">`packagegroup-cloud-azure`hello hello 패키지 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="f792a-163">hello `smart install` 명령에 사용 되는 tooinstall hello 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="f792a-164">이 오류가 나타나는 경우 실행된 hello 다음 명령은: '공개 키 사용할 수 없음'</span><span class="sxs-lookup"><span data-stu-id="f792a-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="f792a-165">이 오류가 나타나는 경우 Intel NUC hello를 다시 부팅: '패키지가 없습니다 util-linux-dev를 제공 하는 데 사용'</span><span class="sxs-lookup"><span data-stu-id="f792a-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="f792a-166">Hello 패키지를 설치한 후 Intel NUC 준비 toofunction 게이트웨이로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="f792a-167">Hello Azure IoT 가장자리 "hello_world" 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f792a-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="f792a-168">샘플 응용 프로그램을 다음 hello에서 한 게이트웨이 만듭니다는 `hello_world.json` 파일을 5 초 마다 hello Azure IoT 가장자리 아키텍처 toolog hello world 메시지 tooa 파일 (log.txt)의 기본 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="f792a-169">Hello 다음 명령을 실행 하 여 hello Hello World 예제를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="f792a-170">몇 분 동안 실행 한 다음 Enter 키 toostop hello 적중 hello Hello World 응용 프로그램을 통해 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="f792a-171">![응용 프로그램 출력](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="f792a-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="f792a-172">Enter 키를 누른 후에 표시되는 '잘못된 인수 핸들(NULL)' 오류는 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="f792a-173">해당 hello 게이트웨이에 hello_world 폴더에 현재 있는 hello log.txt 파일을 열어 성공적으로 실행을 확인할 수 있습니다 ![log.txt 디렉터리 보기](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="f792a-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="f792a-174">Log.txt hello 다음 명령을 사용 하 여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="f792a-175">다음 5 초 마다 hello 게이트웨이 Hello World 모듈에 의해 작성 된 hello 로깅 메시지의 JSON 형식이 출력 될 log.txt의 hello 내용을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="f792a-176">![log.txt 디렉터리 보기](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="f792a-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="f792a-177">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="f792a-178">요약</span><span class="sxs-lookup"><span data-stu-id="f792a-178">Summary</span></span>

<span data-ttu-id="f792a-179">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-179">Congratulations!</span></span> <span data-ttu-id="f792a-180">게이트웨이로 Intel NUC 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="f792a-181">준비가 이제 toomove 호스트 컴퓨터를 다음 단원에서는 tooset toohello에 Azure IoT Hub를 만들고 Azure IoT Hub 논리적 장치를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f792a-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f792a-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f792a-182">Next steps</span></span>
[<span data-ttu-id="f792a-183">IoT 게이트웨이 tooconnect 장치 tooAzure IoT 허브를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f792a-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

