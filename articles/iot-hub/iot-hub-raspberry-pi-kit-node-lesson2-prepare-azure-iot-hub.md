---
featureFlags: usabilla
title: "연결 라스베리 Pi (노드) tooAzure IoT-2 단원: 장치를 등록 | Microsoft Docs"
description: "리소스 그룹의 이름을 만들고 Azure IoT hub를 만들 Azure CLI를 사용 하 여 IoT Hub id 레지스트리에 hello에 Pi를 등록 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Raspberry Pi 클라우드, Pi 클라우드 연결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="6f911-104">IoT Hub 만들기 및 Raspberry Pi 3 등록</span><span class="sxs-lookup"><span data-stu-id="6f911-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="6f911-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="6f911-105">What you will do</span></span>
* <span data-ttu-id="6f911-106">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-106">Create a resource group.</span></span>
* <span data-ttu-id="6f911-107">Hello 리소스 그룹에 Azure IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="6f911-108">Hello Azure CLI (명령줄 인터페이스 Azure)를 사용 하 여 라스베리 Pi 3 toohello Azure IoT 허브를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="6f911-109">Azure CLI tooadd Pi tooyour IoT 허브를 사용 하는 경우 hello 서비스는 hello 서비스와 tooauthenticate Pi에 대 한 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-109">When you use Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="6f911-110">문제가 있는 경우 솔루션 hello에 seek [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6f911-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="6f911-111">What you will learn</span></span>
<span data-ttu-id="6f911-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-112">In this article, you will learn:</span></span>
* <span data-ttu-id="6f911-113">어떻게 toouse Azure CLI toocreate IoT hub</span><span class="sxs-lookup"><span data-stu-id="6f911-113">How toouse Azure CLI toocreate an IoT hub</span></span>
* <span data-ttu-id="6f911-114">어떻게 toocreate Pi에 대 한 IoT hub에서 장치 id</span><span class="sxs-lookup"><span data-stu-id="6f911-114">How toocreate a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6f911-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="6f911-115">What you need</span></span>
* <span data-ttu-id="6f911-116">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="6f911-116">An Azure account</span></span>
* <span data-ttu-id="6f911-117">Mac 또는 hello Azure CLI 설치 된 Windows 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="6f911-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="6f911-118">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="6f911-118">Create your IoT hub</span></span>
<span data-ttu-id="6f911-119">Azure IoT Hub를 사용하면 수백만 개의 IoT 자산을 연결, 모니터링 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="6f911-120">toocreate IoT 허브를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="6f911-121">Hello 다음 명령을 실행 하 여 Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="6f911-122">로그인이 완료되면 사용 가능한 구독이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="6f911-123">Hello 기본 구독 hello 다음 명령을 실행 하 여 toouse 되도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="6f911-124">`subscription ID or name`hello의 hello 출력에서 찾을 수 `az login` 또는 hello `az account list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="6f911-125">Hello 다음 명령을 실행 하 여 hello 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="6f911-126">리소스 공급자는 응용 프로그램에 대한 리소스를 제공하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="6f911-127">Hello 공급자 제공 hello Azure 리소스를 배포 하기 전에 hello 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="6f911-128">리소스 그룹 만들기 라는 iot 샘플 hello 미국 서 부 지역에 hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="6f911-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="6f911-129">`westus`리소스 그룹을 만들면 hello 위치가입니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="6f911-130">다른 위치 toouse을 원하는 경우 실행할 수 있습니다 `az account list-locations -o table` toosee 모든 hello Azure에서는 지원 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="6f911-131">Hello 다음 명령을 실행 하 여 hello iot 샘플 리소스 그룹에는 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="6f911-132">기본적으로 hello 도구 hello 무료 가격 책정 계층에는 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="6f911-133">자세한 내용은 [Azure IoT Hub 가격 책정](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f911-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="6f911-134">IoT hub의 hello 이름 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="6f911-135">Azure IoT Hub의 F1 버전은 사용자의 Azure 구독에서 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="6f911-136">IoT Hub에 Pi 등록</span><span class="sxs-lookup"><span data-stu-id="6f911-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="6f911-137">메시지 tooyour IoT hub를 보내고 IoT 허브에서 메시지를 수신 하는 각 장치는 고유 ID에 등록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="6f911-138">장치 인증에 대 한 자체 서명 된 X.509 인증서를 만들기 및 Azure CLI tooregister 프로그램 Pi를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-138">You will use Azure CLI tooregister your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="6f911-139">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-139">Run hello following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="6f911-140">요약</span><span class="sxs-lookup"><span data-stu-id="6f911-140">Summary</span></span>
<span data-ttu-id="6f911-141">IoT Hub를 만들고 IoT Hub에 장치 ID로 Pi를 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="6f911-142">Toosend Pi tooyour IoT 허브에서 메시지를 어떻게 준비 toolearn 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f911-142">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f911-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f911-143">Next steps</span></span>
[<span data-ttu-id="6f911-144">Azure 저장소 계정 tooprocess 및 Azure 함수 응용 프로그램 작성 및 IoT 허브 메시지 저장</span><span class="sxs-lookup"><span data-stu-id="6f911-144">Create an Azure function app and an Azure storage account tooprocess and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

