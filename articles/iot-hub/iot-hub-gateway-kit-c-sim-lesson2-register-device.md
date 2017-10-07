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
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="197b5-103">Azure IoT Hub 만들기 및 장치 등록</span><span class="sxs-lookup"><span data-stu-id="197b5-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="197b5-104">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="197b5-104">What you will do</span></span>

- <span data-ttu-id="197b5-105">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="197b5-105">Create a resource group</span></span>
- <span data-ttu-id="197b5-106">첫 번째 IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="197b5-106">Create your first IoT hub</span></span>
- <span data-ttu-id="197b5-107">Hello Azure CLI를 사용 하 여 IoT hub에 장치를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="197b5-108">IoT hub에서 장치를 등록할 때 hello Azure IoT 허브 서비스는 hello 서비스와 장치 toouse tooauthenticate 프로그램에 대 한 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="197b5-109">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="197b5-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="197b5-110">What you will learn</span></span>

<span data-ttu-id="197b5-111">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="197b5-112">어떻게 toouse IoT hub Azure CLI toocreate를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="197b5-113">어떻게 tooregister IoT hub에서 장치.</span><span class="sxs-lookup"><span data-stu-id="197b5-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="197b5-114">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="197b5-114">What you need</span></span>

- <span data-ttu-id="197b5-115">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="197b5-115">An active Azure subscription.</span></span> <span data-ttu-id="197b5-116">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="197b5-117">Hello Azure CLI 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="197b5-118">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="197b5-118">Create an IoT hub</span></span>

<span data-ttu-id="197b5-119">IoT hub toocreate 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="197b5-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="197b5-120">Hello 다음 명령을 실행 하 여 Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="197b5-121">로그인하면 사용 가능한 구독이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="197b5-122">Hello 기본 hello 다음 명령을 실행 하 여 toouse 되도록 Azure 구독을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="197b5-123">`subscription ID or name`hello의 hello 출력에서 찾을 수 `az login` 또는 hello `az account list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="197b5-124">Hello 다음 명령을 실행 하 여 hello 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="197b5-125">리소스 공급자는 응용 프로그램에 대한 리소스를 제공하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="197b5-126">Hello 공급자 제공 hello Azure 리소스를 배포 하기 전에 hello 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="197b5-127">명명 된 리소스 그룹 만들기 `iot-gateway` hello 다음 명령을 실행 하 여 hello 미국 서 부 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="197b5-128">`westus`리소스 그룹을 만들면 hello 위치가입니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="197b5-129">다른 위치 toouse을 원하는 경우 실행할 수 있습니다 `az account list-locations -o table` toosee 모든 hello Azure에서는 지원 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="197b5-130">Hello에서 IoT hub를 만들 `iot-gateway` hello 다음 명령을 실행 하 여 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="197b5-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="197b5-131">기본적으로 hello 도구 hello 무료 가격 책정 계층에는 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="197b5-132">자세한 내용은 [Azure IoT Hub 가격 책정](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="197b5-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="197b5-133">IoT hub의 hello 이름 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="197b5-134">Azure IoT Hub의 F1 버전은 사용자의 Azure 구독에서 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="197b5-135">IoT Hub에 장치 등록</span><span class="sxs-lookup"><span data-stu-id="197b5-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="197b5-136">메시지 tooyour IoT hub를 보내고 IoT 허브에서 메시지를 수신 하는 각 장치는 고유 ID에 등록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="197b5-137">다음 명령을 실행하여 IoT Hub에 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="197b5-138">요약</span><span class="sxs-lookup"><span data-stu-id="197b5-138">Summary</span></span>

<span data-ttu-id="197b5-139">IoT Hub를 만들고 IoT Hub에 장치 ID로 논리적 장치를 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="197b5-140">Tooconfigure 및 물리적 장치 tooyour IoT 허브 hello에서에서 실행 되는 게이트웨이 샘플 응용 프로그램 toosend 데이터의 클라우드 준비 toolearn 것입니다.</span><span class="sxs-lookup"><span data-stu-id="197b5-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="197b5-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="197b5-141">Next steps</span></span>
[<span data-ttu-id="197b5-142">시뮬레이트된 장치 클라우드 업로드 샘플 응용 프로그램 구성 및 실행</span><span class="sxs-lookup"><span data-stu-id="197b5-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)