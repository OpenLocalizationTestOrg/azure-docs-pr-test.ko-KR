---
title: "Azure IoT에 Arduino(C) 연결 - 단원 3: 템플릿 배포 | Microsoft Docs"
description: "Azure 함수 앱은 Azure IoT Hub 이벤트를 수신 대기하고, 들어오는 메시지를 처리하고, 이를 Azure Table Storage에 씁니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "클라우드에 데이터 저장, 클라우드에 저장된 데이터, IoT 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: be6105927645ae2ec56f6885c61dbcb6faf5b11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="a507e-104">Azure 함수 앱 및 Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a507e-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="a507e-105">[Azure Functions](../../articles/azure-functions/functions-overview.md)는 클라우드에서 *함수*(작은 코드)를 손쉽게 실행하기 위한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="a507e-106">Azure 함수 앱은 Azure에서 함수 실행을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="a507e-107">수행할 내용</span><span class="sxs-lookup"><span data-stu-id="a507e-107">What will you do</span></span>
<span data-ttu-id="a507e-108">Azure Resource Manager 템플릿을 사용하여 Azure 함수 앱 및 Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="a507e-109">Azure 함수 앱은 Azure IoT Hub 이벤트를 수신 대기하고, 들어오는 메시지를 처리하고, 이를 Azure Table Storage에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="a507e-110">문제가 발생하면 [Adafruit Feather M0 WiFi Arduino 보드에 대한 문제 해결 페이지](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)에서 솔루션을 찾으세요.</span><span class="sxs-lookup"><span data-stu-id="a507e-110">If you have any problems, look for solutions on the [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="a507e-111">학습할 내용</span><span class="sxs-lookup"><span data-stu-id="a507e-111">What will you learn</span></span>
<span data-ttu-id="a507e-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-112">In this article, you will learn:</span></span>
* <span data-ttu-id="a507e-113">[Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md)를 사용하여 Azure 리소스를 배포하는 방법.</span><span class="sxs-lookup"><span data-stu-id="a507e-113">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="a507e-114">Azure 함수 앱을 사용하여 IoT hub 메시지를 처리하고 이를 Azure Table Storage의 테이블에 쓰는 방법.</span><span class="sxs-lookup"><span data-stu-id="a507e-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="a507e-115">필요한 내용</span><span class="sxs-lookup"><span data-stu-id="a507e-115">What do you need</span></span>
<span data-ttu-id="a507e-116">다음을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-116">You must have successfully completed:</span></span>
- <span data-ttu-id="a507e-117">[Arduino 보드 시작][get-started]</span><span class="sxs-lookup"><span data-stu-id="a507e-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="a507e-118">[Azure IoT Hub 만들기][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="a507e-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="a507e-119">샘플 앱 열기</span><span class="sxs-lookup"><span data-stu-id="a507e-119">Open the sample app</span></span>
<span data-ttu-id="a507e-120">다음 명령을 실행하여 Visual Studio Code에서 샘플 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Repo 구조][repo-structure]

* <span data-ttu-id="a507e-122">`app` 하위 폴더에서 `app.ino` 파일은 키 소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-122">The `app.ino` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="a507e-123">이 소스 파일에는 메시지를 IoT hub로 20번 보내서 각 메시지에 대한 LED를 깜빡이는 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="a507e-124">`config.json`에는 필수 구성 설정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-124">The `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="a507e-125">`arm-template.json` 파일은 Azure 함수 앱 및 Azure Storage 계정을 포함하는 Azure Resource Manager 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="a507e-126">`arm-template-param.json` 파일은 Azure Resource Manager 템플릿에서 사용되는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="a507e-127">`ReceiveDeviceMessages` 하위 폴더에는 Azure 함수에 대한 Node.js 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="a507e-128">Azure Resource Manager 템플릿 구성 및 Azure에서 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="a507e-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="a507e-129">Visual Studio Code에서 `arm-template-param.json` 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager 템플릿 매개 변수][arm-template-params]

* <span data-ttu-id="a507e-131">**[your IoT Hub name]**을 [IoT Hub를 만들고 Arduino 보드를 등록][created-iot-hub-and-registered-arduino-board]할 때 지정한 **{my hub name}**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="a507e-132">**[새 리소스에 대한 문자열 접두사]**를 원하는 접두사로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="a507e-133">접두사는 리소스 이름이 전역적으로 고유하여 충돌을 피할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="a507e-134">접두사에 대시 또는 숫자 이니셜을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a507e-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="a507e-135">`arm-template-param.json` 파일을 업데이트한 후 다음 명령을 실행하여 Azure에 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="a507e-136">이러한 리소스를 만드는 데 약 5분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="a507e-137">리소스 만들기가 진행되는 동안, 다음 문서로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="a507e-138">요약</span><span class="sxs-lookup"><span data-stu-id="a507e-138">Summary</span></span>
<span data-ttu-id="a507e-139">IoT Hub 메시지를 처리하는 Azure 함수 앱과 이러한 메시지를 저장하는 Azure Storage 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="a507e-140">이제 샘플을 배포 및 실행하여 장치-클라우드 메시지를 Arduino 보드에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a507e-140">You can now deploy and run the sample to send device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a507e-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a507e-141">Next steps</span></span>
<span data-ttu-id="a507e-142">[샘플 응용 프로그램을 실행하여 Arduino 보드에 장치-클라우드 메시지를 보냅니다][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="a507e-142">[Run a sample application to send device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md