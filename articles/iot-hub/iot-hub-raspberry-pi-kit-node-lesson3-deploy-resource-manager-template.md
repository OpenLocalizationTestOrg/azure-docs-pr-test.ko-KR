---
title: "Azure IoT에 Raspberry Pi(노드) 연결 - 단원 3: 템플릿 배포 | Microsoft Docs"
description: "Azure 함수 앱은 Azure IoT Hub 이벤트를 수신 대기하고, 들어오는 메시지를 처리하고, 이를 Azure Table Storage에 씁니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "클라우드에 데이터 저장, 클라우드에 저장된 데이터, IoT 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="a50c0-104">Azure 함수 앱 및 Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a50c0-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="a50c0-105">[Azure Functions](../azure-functions/functions-overview.md)는 클라우드에서 *함수*(작은 코드)를 손쉽게 실행하기 위한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="a50c0-106">Azure 함수 앱은 Azure에서 함수 실행을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a50c0-107">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="a50c0-107">What you will do</span></span>
<span data-ttu-id="a50c0-108">Azure Resource Manager 템플릿을 사용하여 Azure 함수 앱 및 Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="a50c0-109">Azure 함수 앱은 Azure IoT Hub 이벤트를 수신 대기하고, 들어오는 메시지를 처리하고, 이를 Azure Table Storage에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="a50c0-110">문제가 있으면 [문제 해결 페이지](iot-hub-raspberry-pi-kit-node-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="a50c0-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a50c0-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="a50c0-111">What you will learn</span></span>
<span data-ttu-id="a50c0-112">이 문서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-112">In this article, you will learn:</span></span>

* <span data-ttu-id="a50c0-113">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)를 사용하여 Azure 리소스를 배포하는 방법.</span><span class="sxs-lookup"><span data-stu-id="a50c0-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="a50c0-114">Azure 함수 앱을 사용하여 IoT hub 메시지를 처리하고 이를 Azure Table Storage의 테이블에 쓰는 방법.</span><span class="sxs-lookup"><span data-stu-id="a50c0-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a50c0-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="a50c0-115">What you need</span></span>
<span data-ttu-id="a50c0-116">다음을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="a50c0-117">Raspberry Pi 3 시작</span><span class="sxs-lookup"><span data-stu-id="a50c0-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="a50c0-118">Azure IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="a50c0-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a><span data-ttu-id="a50c0-119">샘플 앱 열기</span><span class="sxs-lookup"><span data-stu-id="a50c0-119">Open the sample app</span></span>
<span data-ttu-id="a50c0-120">다음 명령을 실행하여 Visual Studio Code에서 샘플 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Repo 구조](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="a50c0-122">`app` 하위 폴더에서 `app.js` 파일은 키 소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="a50c0-123">이 소스 파일에는 메시지를 IoT hub로 20번 보내서 각 메시지에 대한 LED를 깜빡이는 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="a50c0-124">`arm-template.json` 파일은 Azure 함수 앱 및 Azure Storage 계정을 포함하는 Azure Resource Manager 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="a50c0-125">`arm-template-param.json` 파일은 Azure Resource Manager 템플릿에서 사용되는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="a50c0-126">`ReceiveDeviceMessages` 하위 폴더에는 Azure 함수에 대한 Node.js 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="a50c0-127">Azure Resource Manager 템플릿 구성 및 Azure에서 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="a50c0-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="a50c0-128">Visual Studio Code에서 `arm-template-param.json` 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Azure Resource Manager 템플릿 매개 변수](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="a50c0-130">**[your IoT Hub name]**을 [IoT Hub를 만들고 Raspberry Pi 3을 등록](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)할 때 지정한 **{my hub name}**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="a50c0-131">**[새 리소스에 대한 문자열 접두사]**를 원하는 접두사로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="a50c0-132">접두사는 리소스 이름이 전역적으로 고유하여 충돌을 피할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="a50c0-133">접두사에 대시 또는 숫자 이니셜을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a50c0-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="a50c0-134">`arm-template-param.json` 파일을 업데이트한 후 다음 명령을 실행하여 Azure에 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="a50c0-135">이러한 리소스를 만드는 데 약 5분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="a50c0-136">리소스 만들기가 진행되는 동안, 다음 문서로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="a50c0-137">요약</span><span class="sxs-lookup"><span data-stu-id="a50c0-137">Summary</span></span>
<span data-ttu-id="a50c0-138">IoT Hub 메시지를 처리하는 Azure 함수 앱과 이러한 메시지를 저장하는 Azure Storage 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="a50c0-139">이제 샘플을 배포 및 실행하고 장치-클라우드 메시지를 Pi에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a50c0-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a50c0-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a50c0-140">Next steps</span></span>
[<span data-ttu-id="a50c0-141">샘플 응용 프로그램을 실행하여 Raspberry Pi 3에서 장치-클라우드 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="a50c0-141">Run a sample application to send device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

