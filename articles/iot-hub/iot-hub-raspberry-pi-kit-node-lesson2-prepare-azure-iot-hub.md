---
featureFlags: usabilla
title: "Azure IoT에 Raspberry Pi(노드) 연결 - 단원 2: 장치 등록 | Microsoft Docs"
description: "리소스 그룹을 만들고, Azure IoT Hub를 만들고, Azure CLI를 사용하여 IoT Hub ID 레지스트리에 Pi를 등록합니다."
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
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="55d8c-104">IoT Hub 만들기 및 Raspberry Pi 3 등록</span><span class="sxs-lookup"><span data-stu-id="55d8c-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="55d8c-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="55d8c-105">What you will do</span></span>
* <span data-ttu-id="55d8c-106">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-106">Create a resource group.</span></span>
* <span data-ttu-id="55d8c-107">리소스 그룹에 Azure IoT hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="55d8c-108">Azure 명령줄 인터페이스(Azure CLI)를 사용하여 Raspberry Pi 3을 the Azure IoT Hub에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="55d8c-109">Azure CLI를 사용하여 Pi를 IoT Hub에 추가하는 경우 서비스는 Pi에 대한 키를 생성하여 서비스로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="55d8c-110">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="55d8c-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="55d8c-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="55d8c-111">What you will learn</span></span>
<span data-ttu-id="55d8c-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-112">In this article, you will learn:</span></span>
* <span data-ttu-id="55d8c-113">Azure CLI를 사용하여 IoT Hub를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="55d8c-113">How to use Azure CLI to create an IoT hub</span></span>
* <span data-ttu-id="55d8c-114">IoT Hub에서 Pi에 대한 장치 ID를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="55d8c-114">How to create a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="55d8c-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="55d8c-115">What you need</span></span>
* <span data-ttu-id="55d8c-116">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="55d8c-116">An Azure account</span></span>
* <span data-ttu-id="55d8c-117">Azure CLI가 설치된 Mac 또는 Windows 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="55d8c-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="55d8c-118">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="55d8c-118">Create your IoT hub</span></span>
<span data-ttu-id="55d8c-119">Azure IoT Hub를 사용하면 수백만 개의 IoT 자산을 연결, 모니터링 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="55d8c-120">IoT Hub를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="55d8c-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="55d8c-121">다음 명령을 실행하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="55d8c-122">로그인이 완료되면 사용 가능한 구독이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="55d8c-123">다음 명령을 실행하여 사용할 기본 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="55d8c-124">`subscription ID or name`은 `az login` 또는 `az account list` 명령의 출력에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="55d8c-125">다음 명령을 실행하여 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-125">Register the provider by running the following command.</span></span> <span data-ttu-id="55d8c-126">리소스 공급자는 응용 프로그램에 대한 리소스를 제공하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="55d8c-127">공급자를 등록해야만 공급자가 제공하는 Azure 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="55d8c-128">다음 명령을 실행하여 미국 서부 하위 지역에 이름이 iot-sample인 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="55d8c-129">`westus`는 리소스 그룹을 만드는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="55d8c-130">다른 위치를 사용하려는 경우 `az account list-locations -o table`을 실행하면 Azure가 지원하는 모든 위치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="55d8c-131">다음 명령을 실행하여 iot-sample 리소스 그룹에서 IoT hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="55d8c-132">기본적으로 도구는 IoT Hub를 무료 가격 책정 계층에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="55d8c-133">자세한 내용은 [Azure IoT Hub 가격 책정](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55d8c-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="55d8c-134">IoT hub의 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="55d8c-135">Azure IoT Hub의 F1 버전은 사용자의 Azure 구독에서 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="55d8c-136">IoT Hub에 Pi 등록</span><span class="sxs-lookup"><span data-stu-id="55d8c-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="55d8c-137">IoT Hub와 메시지를 주고 받는 각 장치는 고유한 ID로 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="55d8c-138">Azure CLI를 사용하여 Pi를 등록하고 장치 인증을 위해 자체 서명된 X.509 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="55d8c-139">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-139">Run the following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="55d8c-140">요약</span><span class="sxs-lookup"><span data-stu-id="55d8c-140">Summary</span></span>
<span data-ttu-id="55d8c-141">IoT Hub를 만들고 IoT Hub에 장치 ID로 Pi를 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="55d8c-142">Pi에서 IoT Hub로 메시지를 보내는 방법을 알아볼 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55d8c-142">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55d8c-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55d8c-143">Next steps</span></span>
[<span data-ttu-id="55d8c-144">IoT Hub 메시지를 처리하고 저장하기 위해 Azure 함수 앱 및 Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="55d8c-144">Create an Azure function app and an Azure storage account to process and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

