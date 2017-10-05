---
title: "C용 Azure IoT 장치 SDK | Microsoft Docs"
description: "C용 Azure IoT 장치 SDK를 시작하고 IoT Hub로 통신하는 장치 앱을 만드는 방법에 대해 알아봅니다."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="409ae-103">C용 Azure IoT 장치 SDK</span><span class="sxs-lookup"><span data-stu-id="409ae-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="409ae-104">**Azure IoT 장치 SDK**는 **Azure IoT Hub** 서비스와 메시지를 보내고 받는 프로세스를 간소화하도록 설계된 라이브러리 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="409ae-105">각각 특정 플랫폼을 대상으로 하는 다양하게 변형된 SDK가 제공되지만 이 문서에서는 **C용 Azure IoT 장치 SDK**를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="409ae-106">C용 Azure IoT 장치 SDK는 이식성을 최대화하기 위해 ANSI C(C99)로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="409ae-107">이 기능은 다양한 플랫폼과 장치에서 작동하기에 적합한 라이브러리를 만들며, 특히 디스크 및 메모리 사용 공간을 최소화하는 것을 우선적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="409ae-108">이 SDK는 광범위한 플랫폼에서 테스트되었습니다(자세한 내용은 [IoT용 Azure Certified 장치 카탈로그](https://catalog.azureiotsuite.com/) 참조).</span><span class="sxs-lookup"><span data-stu-id="409ae-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="409ae-109">이 문서에는 Windows 플랫폼에서 실행되는 샘플 코드 연습이 포함되어 있지만, 여기서 설명하는 코드는 지원되는 플랫폼 범위 전반에 걸쳐 정확히 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="409ae-110">이 문서에서는 C용 Azure IoT 장치 SDK의 아키텍처를 소개하며, 장치 라이브러리를 초기화하고 IoT Hub와 데이터를 보내고 메시지를 받는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="409ae-111">이 문서의 정보로 SDK 사용을 시작하기에 충분하지만 라이브러리에 대한 추가 정보에 대한 포인터도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="409ae-112">SDK 아키텍처</span><span class="sxs-lookup"><span data-stu-id="409ae-112">SDK architecture</span></span>

<span data-ttu-id="409ae-113">GitHub 리포지토리에서 [**C용 Azure IoT 장치 SDK**](https://github.com/Azure/azure-iot-sdk-c)를 찾고 [C API 참조](https://azure.github.io/azure-iot-sdk-c/index.html)에서 API의 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="409ae-114">최신 버전의 라이브러리는 이 리포지토리의 **master** 분기에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="409ae-115">SDK의 핵심 구현은 SDK의 최하위 API 계층인 **IoTHubClient** 라이브러리의 구현을 포함하고 있는 **iothub\_client** 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="409ae-116">**IoTHubClient** 라이브러리에는 IoT Hub와 메시지를 보내고 받기 위한 원시 메시징을 구현하는 API가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="409ae-117">이 라이브러리를 사용할 때 메시지 직렬화를 구현해야 하며 IoT Hub와 통신하기 위한 기타 세부 사항도 직접 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="409ae-118">**serializer** 폴더에는 클라이언트 라이브러리를 사용하여 데이터를 Azure IoT Hub로 보내기 전에 직렬화하는 방법을 보여 주는 도우미 함수와 샘플이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="409ae-119">serializer(직렬 변환기)는 반드시 사용할 필요가 없으며, 편의상 제공되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="409ae-120">**serializer** 라이브러리를 사용하려면 IoT Hub로 보낼 데이터와 IoT Hub에서 받으려는 메시지를 지정하는 모델을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="409ae-121">모델이 정의되면 SDK에서 API 표면을 제공하므로 직렬화 세부 정보에 대해 고민하지 않고도 장치-클라우드 및 클라우드-장치 메시지 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="409ae-122">라이브러리는 프로토콜(예: MQTT, AMQP)을 사용하여 전송을 구현하는 다른 오픈 소스 라이브러리를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="409ae-123">**IoTHubClient** 라이브러리는 다른 오픈 소스 라이브러리에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="409ae-124">[Azure C 공유 유틸리티](https://github.com/Azure/azure-c-shared-utility) 라이브러리 - 여러 Azure 관련 C SDK에서 필요한 기본 작업(예: 문자열, 목록 조작, IO 등)에 공통 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="409ae-125">[Azure uAMQP](https://github.com/Azure/azure-uamqp-c) 라이브러리 - 리소스가 제한된 장치에 맞게 최적화된 AMQP의 클라이언트 쪽 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="409ae-126">[Azure uMQTT](https://github.com/Azure/azure-umqtt-c) 라이브러리 - 리소스가 제한된 장치에 맞게 최적화되고 MQTT 프로토콜을 구현하는 범용 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="409ae-127">예제 코드를 살펴보면 이러한 라이브러리를 더 쉽게 이해하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="409ae-128">다음 섹션에서는 SDK에 포함된 몇 가지 샘플 응용 프로그램을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="409ae-129">이 연습을 통해 SDK 아키텍처 계층의 다양한 기능에 대해 쉽게 설명하고 API 작동 방식을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="409ae-130">샘플을 실행하기 전에</span><span class="sxs-lookup"><span data-stu-id="409ae-130">Before you run the samples</span></span>

<span data-ttu-id="409ae-131">C 용 Azure IoT 장치 SDK에서 샘플을 실행하려면 먼저 Azure 구독에서 [IoT Hub 서비스의 인스턴스를 만들어야](iot-hub-create-through-portal.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="409ae-132">그리고 나서 다음 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="409ae-133">개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="409ae-133">Prepare your development environment</span></span>
* <span data-ttu-id="409ae-134">장치 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="409ae-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="409ae-135">개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="409ae-135">Prepare your development environment</span></span>

<span data-ttu-id="409ae-136">패키지는 일반적인 플랫폼(예: Windows용 NuGet 또는 Debian 및 Ubuntu용 apt_get)을 위해 제공되며, 샘플에서는 사용 가능한 경우 이러한 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="409ae-137">경우에 따라 SDK를 장치용으로 또는 장치에서 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="409ae-138">SDK를 컴파일해야 하는 경우 GitHub 리포지토리에 있는 [개발 환경 준비](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="409ae-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="409ae-139">샘플 응용 프로그램 코드를 얻으려면 GitHub에서 SDK 복사본을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="409ae-140">**GitHub 리포지토리**의 [master](https://github.com/Azure/azure-iot-sdk-c)분기에서 원본의 복사본을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="409ae-141">장치 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="409ae-141">Obtain the device credentials</span></span>

<span data-ttu-id="409ae-142">이제 샘플 원본 코드가 있으므로 다음으로 수행할 작업은 장치 자격 증명 집합을 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="409ae-143">IoT Hub에 액세스할 수 있는 장치의 경우 장치를 IoT Hub ID 레지스트리에 먼저 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="409ae-144">장치를 추가하면 장치를 IoT Hub에 연결하는 데 필요한 장치 자격 증명 집합을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="409ae-145">다음 섹션에서 살펴볼 샘플 응용 프로그램에서는 이러한 자격 증명에 대해 **장치 연결 문자열** 형식을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="409ae-146">IoT Hub를 관리하는 데 도움이 되는 몇 가지 오픈 소스 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="409ae-147">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)라는 Windows 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="409ae-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="409ae-148">[iothub-explorer](https://github.com/azure/iothub-explorer)라는 플랫폼 간 node.js CLI 도구</span><span class="sxs-lookup"><span data-stu-id="409ae-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="409ae-149">이 자습서에서는 그래픽 *장치 탐색기* 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="409ae-150">또한 CLI 도구를 사용하려면 *iothub-explorer* 도구를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="409ae-151">장치 탐색기 도구는 Azure IoT 서비스 라이브러리를 사용하여 IoT Hub에서 장치 추가를 포함하여 다양한 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="409ae-152">장치 탐색기 도구를 사용하여 장치를 추가하면 장치에 대한 연결 문자열을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="409ae-153">이 연결 문자열은 샘플 응용 프로그램을 실행하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="409ae-154">장치 탐색기 도구에 익숙하지 않은 경우 다음 절차에서 이 도구를 사용하여 장치를 추가하고 장치 연결 문자열을 얻는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="409ae-155">장치 탐색기 도구를 설치하려면 [IoT Hub 장치용 장치 탐색기를 사용하는 방법](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="409ae-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="409ae-156">프로그램을 실행하면 다음 인터페이스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="409ae-157">첫 번째 필드에 **IoT Hub 연결 문자열**을 입력하고 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="409ae-158">이 단계에서는 IoT Hub와 통신할 수 있도록 도구를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="409ae-159">IoT Hub 연결 문자열이 구성되었으면 **관리** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="409ae-160">이 탭에서는 IoT Hub에 등록된 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="409ae-161">**만들기** 단추를 클릭하여 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="409ae-162">미리 채워진 키 집합(기본 및 보조)을 포함한 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="409ae-163">**장치 ID**를 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="409ae-164">장치를 만들었으면 방금 만든 장치를 포함하여 등록된 모든 장치로 [장치] 목록이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="409ae-165">새 장치를 마우스 오른쪽 단추로 클릭하면 다음 메뉴가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="409ae-166">**선택한 장치에 대한 연결 문자열 복사**를 선택하면 장치 연결 문자열이 클립보드에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="409ae-167">장치 연결 문자열의 복사본을 보관하세요.</span><span class="sxs-lookup"><span data-stu-id="409ae-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="409ae-168">다음 섹션에서 설명하는 샘플 응용 프로그램을 실행할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="409ae-169">위 단계를 완료하면 일부 코드를 실행할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="409ae-170">두 샘플에는 주요 원본 파일의 맨 위에 연결 문자열을 입력할 수 있는 상수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="409ae-171">예를 들어 **iothub\_client\_sample\_amqp** 응용 프로그램의 해당 줄은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="409ae-172">IoTHubClient 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="409ae-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="409ae-173">[azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) 리포지토리의 **iothub\_client** 폴더 내에는 **iothub\_client\_sample\_mqtt**라는 응용 프로그램이 포함된 **samples** 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="409ae-174">**iothub\_client\_sample\_mqtt** 응용 프로그램의 Windows 버전에는 다음과 같은 Visual Studio 솔루션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="409ae-175">Visual Studio 2017에서 이 프로젝트를 열면 프롬프트를 수락하여 프로젝트를 최신 버전으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="409ae-176">이 솔루션에는 다음의 단일 프로젝트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-176">This solution contains a single project.</span></span> <span data-ttu-id="409ae-177">이 솔루션에 설치되어 있는 4개의 NuGet 패키지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="409ae-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="409ae-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="409ae-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="409ae-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="409ae-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="409ae-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="409ae-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="409ae-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="409ae-182">SDK를 사용하여 작업하는 경우 항상 **Microsoft.Azure.C.SharedUtility** 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="409ae-183">이 샘플은 MQTT 프로토콜을 사용하므로 **Microsoft.Azure.umqtt** 및 **Microsoft.Azure.IoTHub.MqttTransport** 패키지(AMQP 및 HTTP에 해당하는 패키지가 있음)도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="409ae-184">이 샘플에서는 **IoTHubClient** 라이브러리를 사용하므로 솔루션에 **Microsoft.Azure.IoTHub.IoTHubClient** 패키지도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="409ae-185">**iothub\_client\_sample\_amqp.c** 원본 파일에서 샘플 응용 프로그램의 구현을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="409ae-186">다음 단계에서는 이 샘플 응용 프로그램을 사용하여 **IoTHubClient** 라이브러리를 사용하는 데 필요한 내용을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="409ae-187">라이브러리 초기화</span><span class="sxs-lookup"><span data-stu-id="409ae-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="409ae-188">라이브러리 작업을 시작하기 전에 일부 플랫폼별 초기화를 수행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="409ae-189">예를 들어 Linux에서 AMQP를 사용할 계획인 경우 OpenSSL 라이브러리를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="409ae-190">[GitHub 리포지토리](https://github.com/Azure/azure-iot-sdk-c)의 샘플은 클라이언트가 시작될 때 **platform\_init** 유틸리티 함수를 호출하고, 종료하기 전에 **platform\_deinit** 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="409ae-191">이러한 함수는 "platform.h" 헤더 파일에 선언되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="409ae-192">[리포지토리](https://github.com/Azure/azure-iot-sdk-c)에서 대상 플랫폼에 대해 이러한 함수의 정의를 확인하여 클라이언트에 플랫폼별 초기화 코드를 포함해야 하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="409ae-193">라이브러리 작업을 시작하려면 먼저 IoT Hub 클라이언트 핸들을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="409ae-194">장치 탐색기 도구에서 얻은 장치 연결 문자열의 복사본을 이 함수에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="409ae-195">또한 사용할 통신 프로토콜도 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="409ae-196">이 예제에서는 MQTT를 사용하지만 AMQP와 HTTP도 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="409ae-197">유효한 **IOTHUB\_CLIENT\_HANDLE**이 있으면 API 호출을 시작하여 IoT Hub와 메시지를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="409ae-198">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="409ae-198">Send messages</span></span>

<span data-ttu-id="409ae-199">샘플 응용 프로그램은 IoT Hub에 메시지를 보내도록 루프를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="409ae-200">코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-200">The following snippet:</span></span>

- <span data-ttu-id="409ae-201">메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-201">Creates a message.</span></span>
- <span data-ttu-id="409ae-202">메시지에 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-202">Adds a property to the message.</span></span>
- <span data-ttu-id="409ae-203">메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-203">Sends a message.</span></span>

<span data-ttu-id="409ae-204">먼저, 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="409ae-205">메시지를 보낼 때마다 데이터를 보낼 때 호출되는 콜백 함수에 대한 참조를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="409ae-206">이 예제에서 콜백 함수는 **SendConfirmationCallback**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="409ae-207">다음 코드 조각은 이 콜백 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-207">The following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="409ae-208">메시지 작업을 완료했으면 **IoTHubMessage\_Destroy** 함수에 대한 호출에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="409ae-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="409ae-209">이 함수는 메시지를 만들 때 할당된 리소스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="409ae-210">메시지 받기</span><span class="sxs-lookup"><span data-stu-id="409ae-210">Receive messages</span></span>

<span data-ttu-id="409ae-211">메시지 수신은 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="409ae-212">먼저 장치에서 메시지를 받을 때 호출할 콜백을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-212">First, you register the callback to invoke when the device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="409ae-213">마지막 매개 변수는 원하는 항목에 대한 void 포인터입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="409ae-214">이 샘플에서는 정수에 대한 포인터이지만 더 복잡한 데이터 구조에 대한 포인터일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="409ae-215">이 매개 변수는 콜백 함수의 호출자와 공유된 상태에서 해당 콜백 함수가 작동할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="409ae-216">장치에서 메시지를 받으면 등록된 콜백 함수가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="409ae-217">이 콜백 함수에서 검색하는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-217">This callback function retrieves:</span></span>

* <span data-ttu-id="409ae-218">메시지 ID 및 해당 메시지의 상관 관계 ID</span><span class="sxs-lookup"><span data-stu-id="409ae-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="409ae-219">메시지 내용</span><span class="sxs-lookup"><span data-stu-id="409ae-219">The message content.</span></span>
* <span data-ttu-id="409ae-220">메시지의 모든 사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="409ae-220">Any custom properties from the message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="409ae-221">**IoTHubMessage\_GetByteArray** 함수를 사용하여 메시지를 검색합니다. 이 예제에서는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="409ae-222">라이브러리 초기화 취소</span><span class="sxs-lookup"><span data-stu-id="409ae-222">Uninitialize the library</span></span>

<span data-ttu-id="409ae-223">이벤트 보내기 및 메시지 받기를 완료했으면 IoT 라이브러리 초기화를 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="409ae-224">이렇게 하려면 다음 함수 호출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="409ae-225">이 호출은 **IoTHubClient\_CreateFromConnectionString** 함수로 이전에 할당된 리소스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="409ae-226">여기서 볼 수 있듯이 **IoTHubClient** 라이브러리를 사용하여 메시지를 보내고 받는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="409ae-227">라이브러리가 사용할 프로토콜 등 IoT Hub와의 통신에 대한 세부 사항을 처리합니다(개발자 관점에서는 간단한 구성 옵션).</span><span class="sxs-lookup"><span data-stu-id="409ae-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="409ae-228">또한 **IoTHubClient** 라이브러리는 장치에서 IoT Hub로 보내는 데이터를 직렬화하는 방법도 정밀하게 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="409ae-229">어떤 경우에는 이러한 수준의 제어가 장점이지만, 다른 경우에는 사용자가 관계하지 않으려는 구현 세부 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="409ae-230">이 경우 다음 섹션에서 설명하는 **serializer** 라이브러리를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="409ae-231">serializer(직렬 변환기) 사용</span><span class="sxs-lookup"><span data-stu-id="409ae-231">Use the serializer library</span></span>

<span data-ttu-id="409ae-232">개념적으로 **serializer** 라이브러리는 SDK의 **IoTHubClient** 라이브러리 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="409ae-233">IoT Hub와의 기본 통신에 **IoTHubClient** 를 사용하지만 개발자가 메시지 직렬화를 처리하는 부담을 없애주는 모델링 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="409ae-234">이 라이브러리가 동작하는 방식은 예제를 통해 가장 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="409ae-235">[azure-iot-sdk-c 리포지토리](https://github.com/Azure/azure-iot-sdk-c)의 **serializer** 폴더 내에는 **simplesample\_mqtt**라는 응용 프로그램이 포함된 **samples** 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="409ae-236">Windows 버전의 이 샘플은 다음과 같은 Visual Studio 솔루션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="409ae-237">Visual Studio 2017에서 이 프로젝트를 열면 프롬프트를 수락하여 프로젝트를 최신 버전으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="409ae-238">이전 샘플과 마찬가지로 이 하나에는 여러 NuGet 패키지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="409ae-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="409ae-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="409ae-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="409ae-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="409ae-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="409ae-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="409ae-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="409ae-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="409ae-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="409ae-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="409ae-244">이전 샘플에서 대부분의 패키지를 살펴보았지만 **Microsoft.Azure.IoTHub.Serializer**는 새로운 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="409ae-245">이 패키지는 **serializer** 라이브러리를 사용할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="409ae-246">**simplesample\_amqp.c** 파일에서 샘플 응용 프로그램의 구현을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="409ae-247">다음 섹션에서는 이 샘플의 주요 부분을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="409ae-248">라이브러리 초기화</span><span class="sxs-lookup"><span data-stu-id="409ae-248">Initialize the library</span></span>

<span data-ttu-id="409ae-249">**serializer** 라이브러리 작업을 시작하려면 초기화 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="409ae-250">**serializer\_init** 함수에 대한 호출은 일회성 호출이며, 기본 라이브러리를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="409ae-251">그런 다음 **IoTHubClient** 샘플과 동일한 API인 **IoTHubClient\_LL\_CreateFromConnectionString** 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="409ae-252">이 호출은 장치 연결 문자열을 설정하며, 사용하려는 프로토콜을 선택하는 위치이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="409ae-253">이 샘플은 MQTT를 전송으로 사용하지만, AMQP 또는 HTTP를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="409ae-254">마지막으로 **CREATE\_MODEL\_INSTANCE** 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="409ae-255">**WeatherStation**은 모델의 네임스페이스이며, **ContosoAnemometer**는 모델의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="409ae-256">모델 인스턴스가 만들어지면 이를 사용하여 메시지 보내기 및 받기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="409ae-257">하지만 모델을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="409ae-258">모델 정의</span><span class="sxs-lookup"><span data-stu-id="409ae-258">Define the model</span></span>

<span data-ttu-id="409ae-259">**serializer** 라이브러리의 모델은 장치에서 IoT Hub로 보낼 수 있는 이벤트와 모델링 언어로 *작업*(action)이라고 하는 받을 수 있는 메시지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="409ae-260">**simplesample\_amqp** 샘플 응용 프로그램에서와 같이 C 매크로 집합을 사용하여 모델을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="409ae-261">**BEGIN\_NAMESPACE** 및 **END\_NAMESPACE** 매크로 모두 인수로 모델의 네임스페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="409ae-262">이러한 매크로에는 모델의 정의와 모델에서 사용하는 데이터 구조가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="409ae-263">이 예에서는 **ContosoAnemometer**라는 단일 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="409ae-264">이 모델은 장치에서 IoT Hub로 보낼 수 있는 두 가지 데이터, 즉 **DeviceId** 및 **WindSpeed**를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="409ae-265">또한 장치에서 수신할 수 있는 세 가지 동작(메시지)으로 **TurnFanOn**, **TurnFanOff** 및 **SetAirResistance**를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="409ae-266">각 데이터 요소에는 형식이 있고, 각 작업에는 이름(필요에 따라 매개 변수 집합)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="409ae-267">모델에 정의된 이벤트 및 작업은 메시지를 IoT Hub로 보내고 장치로 보낸 메시지에 응답하는 데 사용할 수 있는 API 표면을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="409ae-268">이 모델의 사용은 예제를 통해 가장 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="409ae-269">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="409ae-269">Send messages</span></span>

<span data-ttu-id="409ae-270">모델은 IoT Hub로 보낼 수 있는 데이터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="409ae-271">이 예제에서는 **WITH_DATA** 매크로를 사용하여 정의된 두 데이터 항목 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="409ae-272">**DeviceId** 및 **WindSpeed** 값을 IoT Hub에 보내려면 여러 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="409ae-273">먼저 다음과 같이 보내려는 데이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="409ae-274">앞에서 정의한 모델을 사용하면 **구조체**의 멤버를 설정하여 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="409ae-275">다음으로 보내려는 메시지를 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="409ae-276">다음 코드는 장치-클라우드 메시지를 버퍼에 직렬화합니다( **대상** 기준으로 참조됨).</span><span class="sxs-lookup"><span data-stu-id="409ae-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="409ae-277">그런 다음 코드에서 **sendMessage** 함수를 호출하여 해당 메시지를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="409ae-278">**IoTHubClient\_LL\_SendEventAsync**의 끝에서 두 번째 매개 변수는 데이터를 성공적으로 보낼 때 호출되는 콜백 함수에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="409ae-279">다음은 샘플의 콜백 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="409ae-280">두 번째 매개 변수는 사용자 컨텍스트에 대한 포인터이며, **IoTHubClient\_LL\_SendEventAsync**로 전달된 포인터와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="409ae-281">이 경우 컨텍스트는 간단한 카운터이지만, 사용자가 원하는 모든 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="409ae-282">즉 장치-클라우드 메시지를 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="409ae-283">이제 메시지를 수신하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="409ae-284">메시지 받기</span><span class="sxs-lookup"><span data-stu-id="409ae-284">Receive messages</span></span>

<span data-ttu-id="409ae-285">메시지 수신은 **IoTHubClient** 라이브러리에서 메시지가 작동하는 방식과 유사하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="409ae-286">먼저 메시지 호출 함수를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="409ae-287">그런 다음 메시지를 수신할 때 호출되는 호출 함수를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="409ae-288">다음 코드는 상용구로 모든 솔루션에 대해 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="409ae-289">이 함수는 메시지를 수신하고 **EXECUTE\_COMMAND** 호출을 통해 적절한 함수로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="409ae-290">이 시점에서 호출되는 함수는 모델의 작업 정의에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="409ae-291">모델에서 동작을 정의할 때 장치에서 해당 메시지를 수신할 때 호출되는 함수를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="409ae-292">예를 들어 모델에서 다음 동작을 정의하는 경우:</span><span class="sxs-lookup"><span data-stu-id="409ae-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="409ae-293">다음 서명을 사용하는 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="409ae-294">함수의 이름이 모델의 작업 이름과 일치하고, 함수의 매개 변수가 작업에 대해 지정된 매개 변수와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="409ae-295">첫 번째 매개 변수는 항상 필수이며, 모델 인스턴스에 대한 포인터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="409ae-296">장치에서 이 서명과 일치하는 메시지를 수신하면 해당 함수가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="409ae-297">따라서 **IoTHubMessage**의 상용구 코드를 포함해야 하는 것 외에도 메시지 수신은 모델에 정의된 각 작업에 대한 간단한 함수를 정의하는 정도의 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="409ae-298">라이브러리 초기화 취소</span><span class="sxs-lookup"><span data-stu-id="409ae-298">Uninitialize the library</span></span>

<span data-ttu-id="409ae-299">데이터 보내기 및 메시지 받기를 완료했으면 IoT 라이브러리 초기화를 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="409ae-300">이러한 세 함수 각각은 앞에서 설명한 세 초기화 함수에 맞춰집니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="409ae-301">이러한 API를 호출하면 이전에 할당된 리소스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="409ae-302">다음 단계</span><span class="sxs-lookup"><span data-stu-id="409ae-302">Next Steps</span></span>

<span data-ttu-id="409ae-303">이 문서에서는 **C용 Azure IoT 장치 SDK**에서 라이브러리 사용에 대한 기본 사항을 다룹니다. SDK에 포함된 내용, 아키텍처 및 Windows 샘플 작업을 시작하는 방법을 이해하기에 충분한 정보를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="409ae-304">다음 문서에서는 [IoTHubClient 라이브러리에 대한 자세한 정보](iot-hub-device-sdk-c-iothubclient.md)를 설명하여 SDK를 계속 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="409ae-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="409ae-305">IoT Hub를 개발하는 방법에 대한 자세한 내용은 [Azure IoT SDK][lnk-sdks]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="409ae-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="409ae-306">IoT Hub의 기능을 추가로 탐색하려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="409ae-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="409ae-307">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="409ae-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
