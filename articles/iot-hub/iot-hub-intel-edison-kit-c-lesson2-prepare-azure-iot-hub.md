---
title: "Connect Intel Edison (C) tooAzure IoT-2 단원: 장치를 등록 | Microsoft Docs"
description: "리소스 그룹 만들기, Azure IoT hub를 만들 및 hello Azure CLI를 사용 하 여 Edison hello Azure IoT 허브에 등록 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="7ef31-103">IoT Hub 만들기 및 Intel Edison 등록</span><span class="sxs-lookup"><span data-stu-id="7ef31-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="7ef31-104">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="7ef31-104">What you will do</span></span>
* <span data-ttu-id="7ef31-105">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-105">Create a resource group.</span></span>
* <span data-ttu-id="7ef31-106">Hello 리소스 그룹에 Azure IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="7ef31-107">Hello Azure CLI (명령줄 인터페이스 Azure)를 사용 하 여 Intel Edison toohello Azure IoT 허브를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="7ef31-108">Hello Azure CLI tooadd Edison tooyour IoT 허브를 사용 하 여 hello 서비스 Edison tooauthenticate hello 서비스에 대 한 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="7ef31-109">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7ef31-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="7ef31-110">What you will learn</span></span>
<span data-ttu-id="7ef31-111">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-111">In this article, you will learn:</span></span>
* <span data-ttu-id="7ef31-112">어떻게 toouse IoT hub Azure CLI toocreate를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="7ef31-113">어떻게 toocreate Edison에 대 한 IoT hub에서 장치 id입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7ef31-114">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="7ef31-114">What you need</span></span>
* <span data-ttu-id="7ef31-115">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="7ef31-115">An Azure account.</span></span> <span data-ttu-id="7ef31-116">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="7ef31-117">Hello Azure CLI 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="7ef31-118">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="7ef31-118">Create your IoT hub</span></span>
<span data-ttu-id="7ef31-119">Azure IoT Hub를 사용하면 수백만 개의 IoT 자산을 연결, 모니터링 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="7ef31-120">toocreate IoT 허브를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="7ef31-121">Hello 다음 명령을 실행 하 여 Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="7ef31-122">로그인이 완료되면 사용 가능한 구독이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="7ef31-123">Hello 기본 구독 hello 다음 명령을 실행 하 여 toouse 되도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="7ef31-124">`subscription ID or name`hello의 hello 출력에서 찾을 수 `az login` 또는 hello `az account list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="7ef31-125">Hello 다음 명령을 실행 하 여 hello 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="7ef31-126">리소스 공급자는 응용 프로그램에 대한 리소스를 제공하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="7ef31-127">Hello 공급자 제공 hello Azure 리소스를 배포 하기 전에 hello 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="7ef31-128">리소스 그룹 만들기 라는 iot 샘플 hello 미국 서 부 지역에 hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="7ef31-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="7ef31-129">`westus`리소스 그룹을 만들면 hello 위치가입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="7ef31-130">다른 위치 toouse을 원하는 경우 실행할 수 있습니다 `az account list-locations -o table` toosee 모든 hello Azure에서는 지원 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="7ef31-131">Hello 다음 명령을 실행 하 여 hello iot 샘플 리소스 그룹에는 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="7ef31-132">기본적으로 hello 도구 hello 무료 가격 책정 계층에는 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="7ef31-133">자세한 내용은 [Azure IoT Hub 가격 책정](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ef31-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="7ef31-134">IoT hub의 hello 이름 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="7ef31-135">Azure IoT Hub의 F1 버전은 사용자의 Azure 구독에서 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="7ef31-136">IoT Hub에 Edison 등록</span><span class="sxs-lookup"><span data-stu-id="7ef31-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="7ef31-137">메시지 tooyour IoT hub를 보내고 IoT 허브에서 메시지를 수신 하는 각 장치는 고유 ID에 등록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="7ef31-138">다음 명령을 실행하여 IoT Hub에 Edison을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="7ef31-139">요약</span><span class="sxs-lookup"><span data-stu-id="7ef31-139">Summary</span></span>
<span data-ttu-id="7ef31-140">IoT Hub를 만들고 IoT Hub에 장치 ID로 Edison을 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="7ef31-141">Toosend Edison tooyour IoT 허브에서 메시지를 어떻게 준비 toolearn 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ef31-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ef31-142">Next steps</span></span>
<span data-ttu-id="7ef31-143">[Azure 저장소 계정 tooprocess와 저장소 IoT hub 및 Azure 함수 응용 프로그램 메시지를 만들][process-and-store-iot-hub-messages]합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef31-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md