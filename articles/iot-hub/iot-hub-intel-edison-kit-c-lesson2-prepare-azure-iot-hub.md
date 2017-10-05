---
title: "Azure IoT에 Intel Edison(C) 연결 - 단원 2: 장치 등록 | Microsoft Docs"
description: "리소스 그룹를 만들고 Azure IoT hub를 만들고, Azure CLI를 사용하여 Azure IoT hub에 Edison을 등록합니다."
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
ms.openlocfilehash: 52e3e4734dfd2b89f79b0c66683163e69b8e5f25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="183ef-103">IoT Hub 만들기 및 Intel Edison 등록</span><span class="sxs-lookup"><span data-stu-id="183ef-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="183ef-104">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="183ef-104">What you will do</span></span>
* <span data-ttu-id="183ef-105">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-105">Create a resource group.</span></span>
* <span data-ttu-id="183ef-106">리소스 그룹에 Azure IoT hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="183ef-107">Azure 명령줄 인터페이스(Azure CLI)를 사용하여 Intel Edison을 the Azure IoT Hub에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="183ef-108">Azure CLI를 사용하여 Edison을 IoT hub에 추가하는 경우 서비스는 Edison에 대한 키를 생성하여 서비스로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="183ef-109">문제가 있으면 [문제 해결 페이지][troubleshooting]에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="183ef-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="183ef-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="183ef-110">What you will learn</span></span>
<span data-ttu-id="183ef-111">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-111">In this article, you will learn:</span></span>
* <span data-ttu-id="183ef-112">Azure CLI를 사용하여 IoT Hub를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="183ef-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="183ef-113">IoT Hub에서 Edison에 대한 장치 ID를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="183ef-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="183ef-114">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="183ef-114">What you need</span></span>
* <span data-ttu-id="183ef-115">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="183ef-115">An Azure account.</span></span> <span data-ttu-id="183ef-116">Azure 계정이 없는 경우 몇 분 만에 [무료 Azure 평가판 계정](http://azure.microsoft.com/pricing/free-trial/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="183ef-117">Azure CLI이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="183ef-118">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="183ef-118">Create your IoT hub</span></span>
<span data-ttu-id="183ef-119">Azure IoT Hub를 사용하면 수백만 개의 IoT 자산을 연결, 모니터링 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="183ef-120">IoT Hub를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="183ef-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="183ef-121">다음 명령을 실행하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="183ef-122">로그인이 완료되면 사용 가능한 구독이 모두 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="183ef-123">다음 명령을 실행하여 사용할 기본 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="183ef-124">`subscription ID or name`은 `az login` 또는 `az account list` 명령의 출력에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="183ef-125">다음 명령을 실행하여 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-125">Register the provider by running the following command.</span></span> <span data-ttu-id="183ef-126">리소스 공급자는 응용 프로그램에 대한 리소스를 제공하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="183ef-127">공급자를 등록해야만 공급자가 제공하는 Azure 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="183ef-128">다음 명령을 실행하여 미국 서부 하위 지역에 이름이 iot-sample인 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="183ef-129">`westus`는 리소스 그룹을 만드는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="183ef-130">다른 위치를 사용하려는 경우 `az account list-locations -o table`을 실행하면 Azure가 지원하는 모든 위치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="183ef-131">다음 명령을 실행하여 iot-sample 리소스 그룹에서 IoT hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="183ef-132">기본적으로 도구는 IoT Hub를 무료 가격 책정 계층에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="183ef-133">자세한 내용은 [Azure IoT Hub 가격 책정](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="183ef-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="183ef-134">IoT hub의 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="183ef-135">Azure IoT Hub의 F1 버전은 사용자의 Azure 구독에서 하나만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="183ef-136">IoT Hub에 Edison 등록</span><span class="sxs-lookup"><span data-stu-id="183ef-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="183ef-137">IoT Hub와 메시지를 주고 받는 각 장치는 고유한 ID로 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="183ef-138">다음 명령을 실행하여 IoT Hub에 Edison을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="183ef-139">요약</span><span class="sxs-lookup"><span data-stu-id="183ef-139">Summary</span></span>
<span data-ttu-id="183ef-140">IoT Hub를 만들고 IoT Hub에 장치 ID로 Edison을 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="183ef-141">Edison에서 IoT Hub로 메시지를 보내는 방법을 알아볼 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="183ef-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="183ef-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="183ef-142">Next steps</span></span>
<span data-ttu-id="183ef-143">[IoT Hub 메시지를 처리하고 저장하기 위해 Azure 함수 앱 및 Azure Storage 계정을 만듭니다][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="183ef-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md