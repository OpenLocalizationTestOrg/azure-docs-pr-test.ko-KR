---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 2: 장치 등록 | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, 사물 인터넷 클라우드, azure iot hub 장치 만들기, ti sensortag, ti ble"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5557989453eb47e4c3a287b26603eff040eb1d96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="c69d3-103">Azure IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="c69d3-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c69d3-104">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="c69d3-104">What you will do</span></span>

- <span data-ttu-id="c69d3-105">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="c69d3-105">Create a resource group</span></span>
- <span data-ttu-id="c69d3-106">첫 번째 IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c69d3-106">Create your first IoT hub</span></span>
- <span data-ttu-id="c69d3-107">Azure CLI를 사용하여 IoT Hub에 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="c69d3-108">IoT Hub에 장치를 등록하면 Azure IoT Hub 서비스가 서비스 인증에 사용할 장치에 대한 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="c69d3-109">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="c69d3-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c69d3-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="c69d3-110">What you will learn</span></span>

<span data-ttu-id="c69d3-111">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="c69d3-112">Azure CLI를 사용하여 IoT Hub를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="c69d3-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="c69d3-113">IoT Hub에 장치를 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="c69d3-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c69d3-114">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="c69d3-114">What you need</span></span>

- <span data-ttu-id="c69d3-115">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="c69d3-115">An active Azure subscription.</span></span> <span data-ttu-id="c69d3-116">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="c69d3-117">Azure CLI이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c69d3-118">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c69d3-118">Create an IoT hub</span></span>

<span data-ttu-id="c69d3-119">IoT Hub를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c69d3-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="c69d3-120">다음 명령을 실행하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="c69d3-121">로그인하면 사용 가능한 구독이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="c69d3-122">사용할 기본 Azure 구독을 다음 명령을 실행하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="c69d3-123">`subscription ID or name`은 `az login` 또는 `az account list` 명령의 출력에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="c69d3-124">다음 명령을 실행하여 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-124">Register the provider by running the following command.</span></span> <span data-ttu-id="c69d3-125">리소스 공급자는 응용 프로그램에 대한 리소스를 제공하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="c69d3-126">공급자를 등록해야만 공급자가 제공하는 Azure 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="c69d3-127">다음 명령을 실행하여 미국 서부 하위 지역에 이름이 `iot-gateway`인 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="c69d3-128">`westus`는 리소스 그룹을 만드는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="c69d3-129">다른 위치를 사용하려는 경우 `az account list-locations -o table`을 실행하면 Azure가 지원하는 모든 위치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="c69d3-130">다음 명령을 실행하여 `iot-gateway` 리소스 그룹에서 IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="c69d3-131">기본적으로 도구는 IoT Hub를 무료 가격 책정 계층에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="c69d3-132">자세한 내용은 [Azure IoT Hub 가격 책정](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c69d3-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="c69d3-133">IoT hub의 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="c69d3-134">Azure IoT Hub의 F1 버전은 사용자의 Azure 구독에서 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="c69d3-135">IoT Hub에 장치 등록</span><span class="sxs-lookup"><span data-stu-id="c69d3-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="c69d3-136">IoT Hub와 메시지를 주고 받는 각 장치는 고유한 ID로 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="c69d3-137">다음 명령을 실행하여 IoT Hub에 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="c69d3-138">요약</span><span class="sxs-lookup"><span data-stu-id="c69d3-138">Summary</span></span>

<span data-ttu-id="c69d3-139">IoT Hub를 만들고 IoT Hub에 장치 ID로 논리적 장치를 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="c69d3-140">이제 물리적 장치에서 클라우드의 IoT Hub로 데이터를 보내도록 게이트웨이 샘플 응용 프로그램을 구성하고 실행하는 방법을 배울 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c69d3-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c69d3-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c69d3-141">Next steps</span></span>
[<span data-ttu-id="c69d3-142">시뮬레이트된 장치 클라우드 업로드 샘플 응용 프로그램 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="c69d3-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)