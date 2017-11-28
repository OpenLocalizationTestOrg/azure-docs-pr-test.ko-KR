---
title: "SensorTag 장치 및 Azure IoT 게이트웨이 - 단원 4: 함수 앱 만들기 | Microsoft Docs"
description: "Intel NUC tooyour IoT 허브에서 메시지를 저장 하 고 tooAzure 테이블 저장소에 쓰는 hello 클라우드에서 읽어 주시기 합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hello 클라우드, 클라우드의 저장 된 데이터에에서 데이터를 저장할 iot 클라우드 서비스"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="64f85-104">Azure 함수 앱 및 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="64f85-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="64f85-105">Azure 기능을 쉽게 실행 하기 위한 솔루션 _함수_ (코드의 작은 조각) hello 클라우드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="64f85-106">Azure 함수 응용 프로그램 호스트 hello Azure에서 함수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="64f85-107">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="64f85-107">What you will do</span></span>

- <span data-ttu-id="64f85-108">Azure 리소스 관리자 템플릿 toocreate를 사용 하 여 Azure 저장소 계정 및 Azure 함수 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="64f85-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="64f85-109">hello Azure 함수 앱 tooAzure IoT 허브 이벤트를 수신 하 고, 들어오는 메시지를 처리, tooAzure 테이블 저장소에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="64f85-110">문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지](iot-hub-gateway-kit-c-troubleshooting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="64f85-111">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="64f85-111">What you will learn</span></span>

<span data-ttu-id="64f85-112">이 단원에서는 다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="64f85-113">어떻게 toouse Azure 리소스 관리자 toodeploy Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="64f85-114">Toouse Azure 응용 프로그램 tooprocess IoT Hub 메시지 작동 방법과 Azure 테이블 저장소에서 tooa 테이블 작성.</span><span class="sxs-lookup"><span data-stu-id="64f85-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="64f85-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="64f85-115">What you need</span></span>

<span data-ttu-id="64f85-116">성공적으로 완료 해야 hello 이전 단원:</span><span class="sxs-lookup"><span data-stu-id="64f85-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="64f85-117">1단원: Intel NUC를 IoT Gateway로 설정</span><span class="sxs-lookup"><span data-stu-id="64f85-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="64f85-118">2단원: 호스트 컴퓨터 및 Azure IoT Hub 준비</span><span class="sxs-lookup"><span data-stu-id="64f85-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="64f85-119">3단원: SensorTag에서 메시지 수신 및 IoT Hub에서 메시지 읽기</span><span class="sxs-lookup"><span data-stu-id="64f85-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="64f85-120">샘플 앱 열기</span><span class="sxs-lookup"><span data-stu-id="64f85-120">Open a sample app</span></span>

<span data-ttu-id="64f85-121">Tooyour 이동 `iot-hub-c-intel-nuc-gateway-getting-started` 리포지토리 폴더, initialize hello 구성 파일 및 hello 다음 명령을 실행 하 여 Visual Studio Code에서 연 다음 hello 샘플 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="64f85-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Repo 구조](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="64f85-123">hello `arm-template.json` 파일은 Azure 저장소 계정 및 Azure 함수 응용 프로그램을 포함 하는 hello Azure 리소스 관리자 템플릿.</span><span class="sxs-lookup"><span data-stu-id="64f85-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="64f85-124">hello `arm-template-param.json` 파일은 hello 구성 파일에서 hello Azure 리소스 관리자 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="64f85-125">hello `ReceiveDeviceMessages` 하위 폴더는 hello Azure 함수에 대 한 hello Node.js 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="64f85-126">Azure Resource Manager 템플릿 구성 및 Azure에서 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="64f85-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="64f85-127">업데이트 hello `arm-template-param.json` Visual Studio 코드 파일.</span><span class="sxs-lookup"><span data-stu-id="64f85-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![ARM 템플릿 JSON](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="64f85-129">`[your IoT Hub name]`을 단원 2에서 지정했던 `{my hub name}`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="64f85-130">Hello를 업데이트 한 후 `arm-template-param.json` 파일, hello 다음 명령을 실행 하 여 hello 리소스 tooAzure 배포:</span><span class="sxs-lookup"><span data-stu-id="64f85-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="64f85-131">사용 하 여 `iot-gateway` 의 hello 값으로 `{resource group name}` hello 값 2 단원에서에서 변경 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="64f85-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="64f85-132">요약</span><span class="sxs-lookup"><span data-stu-id="64f85-132">Summary</span></span>

<span data-ttu-id="64f85-133">Azure 함수 앱 tooprocess IoT 허브 메시지 생성 및 Azure 저장소 계정 toostore 이러한 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="64f85-134">이제 게이트웨이 tooyour IoT 허브에서 보낸 메시지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f85-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64f85-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64f85-135">Next steps</span></span>
<span data-ttu-id="64f85-136">[Azure Storage에 유지되는 메시지를 읽습니다](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="64f85-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
