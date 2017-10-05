---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 단원 4: 메시지 저장 | Microsoft Docs"
description: "Intel NUC의 메시지를 IoT Hub에 저장하고 Azure Table Storage에 기록한 다음 클라우드에서 읽습니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "클라우드에 데이터 저장, 클라우드에 저장된 데이터, IoT 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7fc47b07acede28ffe790debca7e38521726011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="9658c-104">Azure 함수 앱 및 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="9658c-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="9658c-105">Azure Functions는 클라우드에서 _함수_(작은 코드)를 손쉽게 실행하기 위한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="9658c-106">Azure 함수 앱은 Azure에서 함수 실행을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="9658c-107">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="9658c-107">What you will do</span></span>

- <span data-ttu-id="9658c-108">Azure Resource Manager 템플릿을 사용하여 Azure 함수 앱 및 Azure Storage 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="9658c-109">Azure 함수 앱은 Azure IoT Hub 이벤트를 수신 대기하고, 들어오는 메시지를 처리하고, 이를 Azure Table Storage에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="9658c-110">문제가 있으면 [문제 해결 페이지](iot-hub-gateway-kit-c-sim-troubleshooting.md)에서 솔루션을 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="9658c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="9658c-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="9658c-111">What you will learn</span></span>

<span data-ttu-id="9658c-112">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="9658c-113">Azure Resource Manager를 사용하여 Azure 리소스를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="9658c-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="9658c-114">Azure 함수 앱을 사용하여 IoT Hub 메시지를 처리하고 이를 Azure Table Storage의 테이블에 쓰는 방법</span><span class="sxs-lookup"><span data-stu-id="9658c-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9658c-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="9658c-115">What you need</span></span>

<span data-ttu-id="9658c-116">다음과 같은 이전 단원을 완료했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="9658c-117">1단원: Intel NUC를 IoT Gateway로 설정</span><span class="sxs-lookup"><span data-stu-id="9658c-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="9658c-118">2단원: 호스트 컴퓨터 및 Azure IoT Hub 준비</span><span class="sxs-lookup"><span data-stu-id="9658c-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="9658c-119">3단원: 시뮬레이트된 장치에서 메시지 수신 및 IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="9658c-119">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="9658c-120">샘플 앱 열기</span><span class="sxs-lookup"><span data-stu-id="9658c-120">Open a sample app</span></span>

<span data-ttu-id="9658c-121">`iot-hub-c-intel-nuc-gateway-getting-started` repo 폴더로 이동하여 구성 파일을 초기화한 후 다음 명령을 실행하여 Visual Studio Code에서 샘플 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Repo 구조](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="9658c-123">`arm-template.json` 파일은 Azure 함수 앱 및 Azure Storage 계정을 포함하는 Azure Resource Manager 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="9658c-124">`arm-template-param.json` 파일은 Azure Resource Manager 템플릿에서 사용되는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="9658c-125">`ReceiveDeviceMessages` 하위 폴더에는 Azure 함수에 대한 Node.js 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="9658c-126">Azure Resource Manager 템플릿 구성 및 Azure에서 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="9658c-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="9658c-127">Visual Studio Code에서 `arm-template-param.json` 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![ARM 템플릿 JSON](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="9658c-129">`[your IoT Hub name]`을 단원 2에서 지정했던 `{my hub name}`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="9658c-130">`arm-template-param.json` 파일을 업데이트한 후 다음 명령을 실행하여 Azure에 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="9658c-131">단원 2에서 값을 변경하지 않았다면 `iot-gateway`을 `{resource group name}` 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="9658c-132">요약</span><span class="sxs-lookup"><span data-stu-id="9658c-132">Summary</span></span>

<span data-ttu-id="9658c-133">IoT Hub 메시지를 처리하는 Azure 함수 앱과 이러한 메시지를 저장하는 Azure Storage 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="9658c-134">이제 게이트웨이에서 IoT Hub로 보낸 메시지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9658c-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9658c-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9658c-135">Next steps</span></span>
<span data-ttu-id="9658c-136">[Azure Storage에 유지되는 메시지를 읽습니다](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9658c-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>
