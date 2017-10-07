---
title: "C 언어용 aaaThe Azure IoT 장치 SDK | Microsoft Docs"
description: "C에 대 한 hello Azure IoT 장치와 SDK 시작 하 고 자세한 방법을 toocreate 장치 앱 통신 하는 IoT 허브를 사용 합니다."
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
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="d9a82-103">C용 Azure IoT 장치 SDK</span><span class="sxs-lookup"><span data-stu-id="d9a82-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="d9a82-104">hello **Azure IoT 장치 SDK** 라이브러리의 집합을 설계 hello에서 메시지 받기를 tooand 메시지를 보내는 toosimplify hello 과정은 **Azure IoT Hub** 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="d9a82-105">Hello에 설명 하지만 hello SDK, 각 특정 플랫폼을 대상으로 이름의 다른 변형이 **C에 대 한 Azure IoT 장치 SDK**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="d9a82-106">ANSI C (C99) toomaximize 이식성 C에 대 한 hello Azure IoT 장치 SDK로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="d9a82-107">이 기능은 hello 라이브러리 잘 맞는 toooperate 여러 플랫폼 및 장치에 디스크를 최소화 하는 경우에 특히 만들고 메모리 사용량은 우선 순위를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="d9a82-108">광범위 한 다양 한 플랫폼 SDK는 hello에서 테스트 되었습니다 (hello 참조 [Azure IoT 장치 카탈로그에 대 한 인증](https://catalog.azureiotsuite.com/) 세부 정보에 대 한).</span><span class="sxs-lookup"><span data-stu-id="d9a82-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="d9a82-109">이 문서 hello Windows 플랫폼에서 실행 되는 샘플 코드의 연습을 포함 하지만 hello 다양 한 지원 되는 플랫폼에서이 문서에서 설명 하는 hello 코드는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="d9a82-110">이 문서 hello Azure IoT 장치 SDK의 toohello 아키텍처의 소개 3. 방법을 tooinitialize hello 장치 라이브러리 데이터 tooIoT 허브에 메시지 보내기 및 받기 여기에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="d9a82-111">이 문서의 정보 hello hello SDK를 사용 하 여 시작 하는 데 충분 한 tooget 수도 있지만 또한 hello 라이브러리에 대 한 포인터 tooadditional 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="d9a82-112">SDK 아키텍처</span><span class="sxs-lookup"><span data-stu-id="d9a82-112">SDK architecture</span></span>

<span data-ttu-id="d9a82-113">Hello를 찾을 수 있습니다 [ **C에 대 한 Azure IoT 장치 SDK** ](https://github.com/Azure/azure-iot-sdk-c) hello에 hello API의 GitHub 리포지토리 및 뷰 세부 정보 [C API 참조](https://azure.github.io/azure-iot-sdk-c/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="d9a82-114">hello에 최신 버전의 hello 라이브러리 hello 있습니다 **마스터** hello 리포지토리의 분기:</span><span class="sxs-lookup"><span data-stu-id="d9a82-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="d9a82-115">hello hello SDK의 핵심 구현 중인 hello **iothub\_클라이언트** hello 구현의 hello 가장 낮은 API 계층 hello SDK에에서 포함 된 폴더: hello **IoTHubClient** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="d9a82-116">hello **IoTHubClient** 라이브러리 메시지 tooIoT 허브 송수신 IoT 허브에서 메시지에 대 한 원시 메시징을 구현 하는 Api가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="d9a82-117">이 라이브러리를 사용할 때 메시지 직렬화를 구현해야 하며 IoT Hub와 통신하기 위한 기타 세부 사항도 직접 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="d9a82-118">hello **serializer** 폴더 도우미 함수 및 tooserialize 데이터 tooAzure IoT 허브를 사용 하 여 보내기 전에 클라이언트 라이브러리를 hello 하는 방법을 보여 주는 샘플이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="d9a82-119">hello 사용 하 여 hello serializer의 필수 이며 편의 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="d9a82-120">toouse hello **serializer** hello 데이터 toosend tooIoT 허브 및 hello 메시지에서 tooreceive 예상를 지정 하는 모델을 정의할 라이브러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="d9a82-121">Hello 모델에서 정의 되 면 hello SDK 한를 사용 하면 하는 API 화면으로 tooeasily 작업 장치-클라우드 하 고에 대 한 걱정 없이 클라우드-장치 메시지 hello serialization 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="d9a82-122">hello 라이브러리와 같은 MQTT 및 AMQP 프로토콜을 사용 하 여 전송을 구현 하는 다른 오픈 소스 라이브러리에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="d9a82-123">hello **IoTHubClient** 라이브러리 다른 오픈 소스 라이브러리에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="d9a82-124">hello [Azure C 공유 유틸리티](https://github.com/Azure/azure-c-shared-utility) 몇몇 Azure 관련 C Sdk에 필요한 기본 작업 (예: 문자열, 목록 조작 및 IO)에 대 한 공통 기능을 제공 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="d9a82-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) AMQP 리소스 제한 된 장치에 대해 최적화를 구현 하는 클라이언트 쪽 라이브러리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="d9a82-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) hello MQTT 프로토콜을 구현 하는 일반적인 용도의 라이브러리 및 리소스 제한 된 장치에 대해 최적화 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="d9a82-127">이러한 라이브러리의 용도는 예제 코드를 살펴보면 쉽게 toounderstand입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="d9a82-128">다음 섹션 hello hello SDK에에서 포함 된 hello 예제 응용 프로그램의 여러 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="d9a82-129">이 연습에서는 좋은 회원님 hello에 대 한 SDK hello 및 Api 작동 하는 소개 toohow hello의 hello 아키텍처 계층의 다양 한 기능을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="d9a82-130">Hello 샘플을 실행 하기 전에</span><span class="sxs-lookup"><span data-stu-id="d9a82-130">Before you run hello samples</span></span>

<span data-ttu-id="d9a82-131">C에 대 한 hello Azure IoT 장치 SDK에서에서 hello 샘플을 실행할 수 있습니다, 전에 해야 [hello IoT 허브 서비스의 인스턴스를 만들고](iot-hub-create-through-portal.md) Azure 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="d9a82-132">그런 다음 작업을 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="d9a82-133">개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="d9a82-133">Prepare your development environment</span></span>
* <span data-ttu-id="d9a82-134">장치 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="d9a82-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="d9a82-135">개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="d9a82-135">Prepare your development environment</span></span>

<span data-ttu-id="d9a82-136">패키지는 일반적인 플랫폼 (예: Windows 용 NuGet 또는 apt_get Debian 및 Ubuntu)에 대 한 제공 됩니다 및 hello 샘플 사용 가능한 경우 이러한 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="d9a82-137">일부 경우에 또는 장치에 대 한 toocompile hello SDK 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="d9a82-138">Toocompile hello SDK 필요한 경우 참조 [개발 환경을 준비](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) hello GitHub 리포지토리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="d9a82-139">tooobtain hello 샘플 응용 프로그램 코드를 다운로드 hello GitHub에서 SDK의 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="d9a82-140">Hello에서 hello 소스의 사본을 가져옵니다 **마스터** hello의 분기 [GitHub 리포지토리](https://github.com/Azure/azure-iot-sdk-c)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="d9a82-141">Hello 장치 자격 증명을 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="d9a82-141">Obtain hello device credentials</span></span>

<span data-ttu-id="d9a82-142">Hello 샘플 소스 코드를가지고 hello 다음 일 toodo tooget 장치 자격 증명 집합은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="d9a82-143">장치 toobe 수 tooaccess IoT hub 먼저 hello 장치 toohello IoT Hub id 레지스트리에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="d9a82-144">장치를 추가할 때 필요한 hello 장치 toobe 수 tooconnect toohello IoT 허브에 대 한 장치 자격 증명 집합을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="d9a82-145">hello 다음 섹션에서 설명 하는 hello 샘플 응용 프로그램의 hello 형태로 이러한 자격 증명을 예상는 **장치 연결 문자열**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="d9a82-146">IoT hub를 관리 하는 여러 오픈 소스 도구 toohelp 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="d9a82-147">[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)라는 Windows 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d9a82-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="d9a82-148">[iothub-explorer](https://github.com/azure/iothub-explorer)라는 플랫폼 간 node.js CLI 도구</span><span class="sxs-lookup"><span data-stu-id="d9a82-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="d9a82-149">이 자습서에서는 그래픽 hello *장치 탐색기* 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="d9a82-150">Hello를 사용할 수도 있습니다 *iothub 탐색기* toouse CLI 도구를 선호 하는 경우 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="d9a82-151">hello 장치 탐색기 도구 IoT 허브에 장치를 추가 하는 등에서 hello Azure IoT 서비스 라이브러리 tooperform 다양 한 함수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="d9a82-152">Hello 장치 탐색기 도구 tooadd 장치를 사용 하는 경우 장치에 대 한 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="d9a82-153">이 연결 문자열 toorun hello 예제 응용 프로그램에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="d9a82-154">Hello 장치 탐색기 도구로 잘 모르는 경우에 절차를 수행 하는 hello 설명 어떻게 toouse 것 tooadd 장치 및 장치 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="d9a82-155">tooinstall hello 장치 탐색기 도구 참조 [IoT Hub 장치에 대 한 toouse 장치 탐색기 hello 어떻게](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="d9a82-156">Hello 프로그램을 실행 하면이 인터페이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="d9a82-157">입력 프로그램 **IoT 허브 연결 문자열** hello에 먼저 필드를 클릭 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="d9a82-158">이 단계에서는 IoT Hub와 통신할 수 있도록 hello 도구를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="d9a82-159">Hello IoT 허브 연결 문자열이 구성 된 경우 클릭 hello **관리** 탭:</span><span class="sxs-lookup"><span data-stu-id="d9a82-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="d9a82-160">이 탭은 IoT 허브에 등록 된 hello 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="d9a82-161">Hello를 클릭 하 여 장치를 만들면 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="d9a82-162">미리 채워진 키 집합(기본 및 보조)을 포함한 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="d9a82-163">**장치 ID**를 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="d9a82-164">Hello 장치를 만들면 hello 장치 하나 방금 만든 hello를 포함 하 여 모든 hello 등록 된 장치와 업데이트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="d9a82-165">새 장치를 마우스 오른쪽 단추로 클릭하면 다음 메뉴가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="d9a82-166">선택 하면 **선택한 장치에 대 한 연결 문자열을 복사**, hello 장치 연결 문자열은 복사한 toohello 클립보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="d9a82-167">Hello 장치 연결 문자열의 복사본을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="d9a82-168">경우에 필요한 hello 다음 섹션에에서 설명 된 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="d9a82-169">위의 hello 단계를 완료 하면 일부 코드를 실행 하는 준비 toostart 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="d9a82-170">두 샘플 tooenter 연결 문자열 수 있도록 하는 hello 주 소스 파일의 hello top에 상수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="d9a82-171">예를 들어 hello에서 해당 줄을 hello **iothub\_클라이언트\_샘플\_mqtt** 응용 프로그램에는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="d9a82-172">Hello IoTHubClient 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="d9a82-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="d9a82-173">Hello 내 **iothub\_클라이언트** 폴더 hello에 [azure iot-sdk c](https://github.com/azure/azure-iot-sdk-c) 저장소는는 **샘플** 를호출하는응용프로그램이포함된폴더**iothub\_클라이언트\_샘플\_mqtt**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="d9a82-174">Windows 버전의 hello hello **iothub\_클라이언트\_샘플\_mqtt** 응용 프로그램에 따라 Visual Studio 솔루션 hello:</span><span class="sxs-lookup"><span data-stu-id="d9a82-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="d9a82-175">Visual Studio 2017에서이 프로젝트를 열면 hello 프롬프트 tooretarget hello 프로젝트 toohello 최신 버전을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="d9a82-176">이 솔루션에는 다음의 단일 프로젝트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-176">This solution contains a single project.</span></span> <span data-ttu-id="d9a82-177">이 솔루션에 설치되어 있는 4개의 NuGet 패키지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="d9a82-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="d9a82-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="d9a82-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="d9a82-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="d9a82-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="d9a82-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="d9a82-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="d9a82-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="d9a82-182">Hello 항상 필요한 **Microsoft.Azure.C.SharedUtility** 패키지 hello SDK 사용 하 여 작업할 때.</span><span class="sxs-lookup"><span data-stu-id="d9a82-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="d9a82-183">이 샘플에서는 hello MQTT 프로토콜, 따라서 hello를 포함 해야 **Microsoft.Azure.umqtt** 및 **Microsoft.Azure.IoTHub.MqttTransport** (해당 하는 패키지가 있습니다 AMQP 및 HTTP에 대 한 패키지 ).</span><span class="sxs-lookup"><span data-stu-id="d9a82-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="d9a82-184">Hello 샘플 hello를 사용 하기 때문에 **IoTHubClient** 라이브러리 hello 포함 해야 **Microsoft.Azure.IoTHub.IoTHubClient** 솔루션의 패키지를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="d9a82-185">Hello hello 샘플 응용 프로그램에 대 한 hello 구현을 찾을 수 있습니다 **iothub\_클라이언트\_샘플\_mqtt.c** 소스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="d9a82-186">hello 다음 단계 사용 하 여이 샘플 응용 프로그램 toowalk toouse hello는 데 필요한 작업을 통해 있습니다 **IoTHubClient** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="d9a82-187">Hello 라이브러리를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="d9a82-188">Hello 라이브러리와 함께 작업을 시작 하기 전에 일부 플랫폼 특정 초기화 tooperform를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="d9a82-189">예를 들어 linux toouse AMQP를 사용 하려는 경우 hello OpenSSL 라이브러리를 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="d9a82-190">hello에 대 한 샘플 hello [GitHub 리포지토리](https://github.com/Azure/azure-iot-sdk-c) hello 유틸리티 함수를 호출 **플랫폼\_init** 클라이언트 시작 hello 시점과 hello 호출 **플랫폼\_deinit**  종료 하기 전에 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="d9a82-191">이러한 함수는 hello platform.h 헤더 파일에 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="d9a82-192">Hello에 대상 플랫폼에 대 한 이러한 함수의 hello 정의 검사할 [리포지토리](https://github.com/Azure/azure-iot-sdk-c) toodetermine 해야 하는지 여부 tooinclude 모든 플랫폼 관련 초기화 코드가 클라이언트에서.</span><span class="sxs-lookup"><span data-stu-id="d9a82-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="d9a82-193">먼저 toostart hello 라이브러리 작업 IoT 허브 클라이언트 핸들을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="d9a82-194">Hello 장치 탐색기 도구 toothis 함수에서 얻을 hello 장치 연결 문자열의 복사본을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="d9a82-195">Hello 통신 프로토콜 toouse를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="d9a82-196">이 예제에서는 MQTT를 사용하지만 AMQP와 HTTP도 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="d9a82-197">유효한 설치한 경우 **IOTHUB\_클라이언트\_처리**, hello Api toosend 호출을 시작 하 고 메시지 tooand IoT 허브에서 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="d9a82-198">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="d9a82-198">Send messages</span></span>

<span data-ttu-id="d9a82-199">hello 샘플 응용 프로그램 루프 toosend 메시지 tooyour IoT 허브를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="d9a82-200">다음 코드 조각 hello:</span><span class="sxs-lookup"><span data-stu-id="d9a82-200">hello following snippet:</span></span>

- <span data-ttu-id="d9a82-201">메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-201">Creates a message.</span></span>
- <span data-ttu-id="d9a82-202">속성 toohello 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="d9a82-203">메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-203">Sends a message.</span></span>

<span data-ttu-id="d9a82-204">먼저, 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="d9a82-205">메시지를 보낼 때마다 hello 데이터를 보낼 때 호출 되는 참조 tooa 콜백 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="d9a82-206">이 예제에서는 hello 콜백 함수가 호출 될 **SendConfirmationCallback**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="d9a82-207">다음 코드 조각 hello이 콜백 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-207">hello following snippet shows this callback function:</span></span>

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

<span data-ttu-id="d9a82-208">Hello 호출 toohello 참고 **IoTHubMessage\_Destroy** hello 메시지와 함께 완료 되 면 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="d9a82-209">이 함수는 hello 메시지를 만들 때 할당 된 hello 리소스를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="d9a82-210">메시지 받기</span><span class="sxs-lookup"><span data-stu-id="d9a82-210">Receive messages</span></span>

<span data-ttu-id="d9a82-211">메시지 수신은 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="d9a82-212">첫째, hello 장치 메시지를 받을 때 hello 콜백 tooinvoke를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

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

<span data-ttu-id="d9a82-213">hello 마지막 매개 변수는 void 포인터 toowhatever 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="d9a82-214">Hello 샘플에서은 포인터 tooan 정수 이지만 포인터 tooa 수도 더 복잡 한 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="d9a82-215">이 매개 변수는이 함수의 호출자 hello와 공유 상태에 콜백 함수 toooperate hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="d9a82-216">Hello 장치는 메시지를 받으면 hello 등록 된 콜백 함수가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="d9a82-217">이 콜백 함수에서 검색하는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-217">This callback function retrieves:</span></span>

* <span data-ttu-id="d9a82-218">hello 메시지 id와 hello 메시지에서 상관 관계 id.</span><span class="sxs-lookup"><span data-stu-id="d9a82-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="d9a82-219">hello 메시지 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-219">hello message content.</span></span>
* <span data-ttu-id="d9a82-220">Hello 메시지에서 모든 사용자 지정 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-220">Any custom properties from hello message.</span></span>

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
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
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

<span data-ttu-id="d9a82-221">사용 하 여 hello **IoTHubMessage\_GetByteArray** 함수 tooretrieve hello 메시지를이 예제는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="d9a82-222">Hello 라이브러리를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-222">Uninitialize hello library</span></span>

<span data-ttu-id="d9a82-223">때 이벤트 전송을 완료 되 고 메시지를 받을 hello IoT 라이브러리 초기화 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="d9a82-224">따라서 toodo hello 함수 호출을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="d9a82-225">이 호출은 hello에서 이전에 할당 하는 hello 리소스를 확보 **IoTHubClient\_CreateFromConnectionString** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="d9a82-226">볼 수 있듯이 쉽게 toosend 이며 hello로 메시지를 받을 **IoTHubClient** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="d9a82-227">hello 라이브러리 hello 세부 사항을 처리 어떤 프로토콜 toouse를 포함 하 여 IoT 허브와의 통신 (hello hello 개발자의 관점에서 보면이 간단한 구성 옵션).</span><span class="sxs-lookup"><span data-stu-id="d9a82-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="d9a82-228">hello **IoTHubClient** 라이브러리도 tooserialize hello 데이터 장치에서 보내는 방법을 tooIoT 허브 정밀 하 게 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="d9a82-229">경우에 따라 이러한 제어 수준은 장점이 이지만 있고 다른 toobe에 염려 하지 않도록 하는 구현 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="d9a82-230">경우에 해당 되는 hello 경우 hello를 사용 하 여 고려할 수 있습니다 **serializer** 라이브러리 hello 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="d9a82-231">Hello serializer 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="d9a82-231">Use hello serializer library</span></span>

<span data-ttu-id="d9a82-232">개념적으로 hello **serializer** 라이브러리는 hello 상단 **IoTHubClient** hello SDK에에서는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="d9a82-233">Hello를 사용 하 여 **IoTHubClient** 하지만 IoT Hub와의 통신을 내부 hello에 대 한 라이브러리 hello 개발자에서 메시지 serialization 처리 하는 hello 부담을 제거 하는 모델링 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="d9a82-234">이 라이브러리가 동작하는 방식은 예제를 통해 가장 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="d9a82-235">내부 hello **serializer** hello에서 폴더 [azure iot-sdk c 리포지토리](https://github.com/Azure/azure-iot-sdk-c),이 **샘플** 호출 응용 프로그램이 들어 있는 폴더 **simplesample \_mqtt**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="d9a82-236">이 샘플의 hello Windows 버전 hello 다음 Visual Studio 솔루션에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="d9a82-237">Visual Studio 2017에서이 프로젝트를 열면 hello 프롬프트 tooretarget hello 프로젝트 toohello 최신 버전을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="d9a82-238">Hello 앞의 예제에서와 마찬가지로이 중 하나에 여러 NuGet 패키지가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="d9a82-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="d9a82-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="d9a82-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="d9a82-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="d9a82-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="d9a82-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="d9a82-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="d9a82-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="d9a82-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="d9a82-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="d9a82-244">대부분의 hello 이전 샘플에서 이러한 패키지를 살펴 보았으며 하지만 **Microsoft.Azure.IoTHub.Serializer** 새로운 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="d9a82-245">이 패키지는 hello를 사용 하는 경우 필요한 **serializer** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="d9a82-246">Hello에서 hello 구현의 hello 샘플 응용 프로그램을 찾을 수 있습니다 **simplesample\_mqtt.c** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="d9a82-247">hello 다음 섹션에서는 단계별로 hello이이 샘플의 주요 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="d9a82-248">Hello 라이브러리를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-248">Initialize hello library</span></span>

<span data-ttu-id="d9a82-249">hello로 작업 toostart **serializer** 라이브러리, Api 호출 hello 초기화:</span><span class="sxs-lookup"><span data-stu-id="d9a82-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

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

<span data-ttu-id="d9a82-250">hello 호출 toohello **serializer\_init** 초기화 hello 기본 라이브러리 및 함수는 한 번만 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="d9a82-251">Hello를 호출 하는 다음 **IoTHubClient\_LL\_CreateFromConnectionString** 함수 hello와 같이 동일한 API는 hello를 **IoTHubClient** 샘플.</span><span class="sxs-lookup"><span data-stu-id="d9a82-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="d9a82-252">장치 연결 문자열을 설정 하는이 호출 (hello 프로토콜을 선택 하면이 호출 또한은 toouse 원하는).</span><span class="sxs-lookup"><span data-stu-id="d9a82-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="d9a82-253">이 샘플 MQTT hello 전송으로 사용 하 여 하지만 AMQP 나 HTTP 중 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="d9a82-254">마지막으로 hello 호출 **만들기\_모델\_인스턴스** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="d9a82-255">**WeatherStation** hello 모델의 hello 네임 스페이스 및 **ContosoAnemometer** hello hello 모델 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="d9a82-256">Hello 모델 인스턴스를 만든 후 toostart 메시지 송수신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="d9a82-257">그러나 어떤 모델은 중요 한 toounderstand 되기 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="d9a82-258">Hello 모델 정의</span><span class="sxs-lookup"><span data-stu-id="d9a82-258">Define hello model</span></span>

<span data-ttu-id="d9a82-259">Hello에서 모델 **serializer** 장치 tooIoT 이라는 허브 및 hello 메시지를 보낼 수 있는 hello 메시지를 정의 하는 라이브러리 *동작* hello를 받을 수 있는 언어에서 모델링에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="d9a82-260">Hello와 같이 C 매크로 집합을 사용 하 여 모델을 정의 **simplesample\_mqtt** 샘플 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="d9a82-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="d9a82-261">hello **시작\_네임 스페이스** 및 **끝\_네임 스페이스** 매크로 모두를 인수로 hello 모델의 hello 네임 스페이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="d9a82-262">모델 또는 모델 및 모델 hello를 사용 하는 hello 데이터 구조의 hello 정의 임을 이러한 매크로 사이 아무 것도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="d9a82-263">이 예에서는 **ContosoAnemometer**라는 단일 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="d9a82-264">이 모델은 두 가지 장치 tooIoT 허브를 보낼 수 있음을 데이터 정의: **DeviceId** 및 **WindSpeed**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="d9a82-265">또한 장치에서 수신할 수 있는 세 가지 동작(메시지)으로 **TurnFanOn**, **TurnFanOff** 및 **SetAirResistance**를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="d9a82-266">각 데이터 요소에는 형식이 있고, 각 작업에는 이름(필요에 따라 매개 변수 집합)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="d9a82-267">hello 데이터와 hello 모델에 정의 된 작업 toosend 메시지 tooIoT 허브를 사용할 수 있으며 전송 toomessages toohello 장치 응답 하는 API 화면을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="d9a82-268">이 모델의 사용은 예제를 통해 가장 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="d9a82-269">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="d9a82-269">Send messages</span></span>

<span data-ttu-id="d9a82-270">hello 모델 정의 hello 데이터 tooIoT 허브를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="d9a82-271">이 예제에서는 하는 중 하나를 의미 hello hello를 사용 하 여 정의 하는 두 데이터 항목이 **WITH_DATA** 매크로입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="d9a82-272">여러 단계가 필요한 toosend **DeviceId** 및 **WindSpeed** 값 tooan IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="d9a82-273">hello는 toosend 원하는 tooset hello 데이터를 먼저가:</span><span class="sxs-lookup"><span data-stu-id="d9a82-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="d9a82-274">hello 앞에서 정의한 모델 하면 tooset hello 값의 멤버를 설정 하 여 한 **구조체**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="d9a82-275">다음으로 직렬화 toosend hello 메시지:</span><span class="sxs-lookup"><span data-stu-id="d9a82-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="d9a82-276">이 코드는 hello 장치-클라우드 tooa 버퍼를 serialize (참조 **대상**).</span><span class="sxs-lookup"><span data-stu-id="d9a82-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="d9a82-277">hello 코드에는 다음 hello 호출 **sendMessage** toosend hello 메시지 tooIoT 허브 함수:</span><span class="sxs-lookup"><span data-stu-id="d9a82-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="d9a82-278">두 번째 toolast 매개 hello **IoTHubClient\_LL\_SendEventAsync** 은 hello 데이터 성공적으로 전송 될 때 호출 되는 참조 tooa 콜백 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="d9a82-279">다음은 hello 샘플에서 hello 콜백 함수가입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="d9a82-280">hello 두 번째 매개 변수는 포인터 toouser 컨텍스트입니다. 동일한 포인터가 너무 전달 hello**IoTHubClient\_LL\_SendEventAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="d9a82-281">이 경우 hello 컨텍스트는 단순한 카운터 있지만 원하는 대로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="d9a82-282">그 toosending 장치-클라우드 메시지는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="d9a82-283">hello만 남았습니다 toocover은 어떻게 tooreceive 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="d9a82-284">메시지 받기</span><span class="sxs-lookup"><span data-stu-id="d9a82-284">Receive messages</span></span>

<span data-ttu-id="d9a82-285">메시지를 받는 메시지 hello에서 작동 하는 toohello 방식 유사 하 게 작동 **IoTHubClient** 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="d9a82-286">먼저 메시지 호출 함수를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="d9a82-287">그런 다음 메시지를 받을 때 호출 되는 hello 콜백 함수를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
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

<span data-ttu-id="d9a82-288">이 코드는 상용구--모든 솔루션에 대 한 동일 hello 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="d9a82-289">이 함수 hello 메시지를 수신 및 라우팅하기 hello 호출을 통해 적절 한 함수 toohello 너무 담당**EXECUTE\_명령**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="d9a82-290">이 시점에서 호출 하는 hello 함수 모델의 hello 함수 hello 정의에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="d9a82-291">필요 하면 모델에서 동작을 정의할 때 tooimplement 장치 hello 해당 메시지를 받을 때 호출 되는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="d9a82-292">예를 들어 모델에서 다음 동작을 정의하는 경우:</span><span class="sxs-lookup"><span data-stu-id="d9a82-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="d9a82-293">다음 서명을 사용하는 함수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="d9a82-294">Note hello 함수 hello 이름을 hello 모델의 액션에 hello의 hello 이름 일치 방법을 아니며 hello 함수의 hello 매개 변수 hello 동작에 대 한 지정 된 hello 매개 변수과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="d9a82-295">hello 첫 번째 매개 변수는 항상 있어야 및 모델의 포인터 toohello 인스턴스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="d9a82-296">Hello 장치가이 시그니처와 일치 하는 메시지를 받을 때 hello 해당 함수가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="d9a82-297">tooinclude hello 상용구 코드 외에도 따라서 **IoTHubMessage**, 메시지를 받는 과정은 모델에 정의 된 각 동작에 대 한 간단한 함수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="d9a82-298">Hello 라이브러리를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-298">Uninitialize hello library</span></span>

<span data-ttu-id="d9a82-299">데이터를 전송 하 고 맞아 고 때는 메시지를 받을 hello IoT 라이브러리 초기화 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="d9a82-300">이러한 세 가지 함수는 각각 hello 세 초기화 함수 앞에서 설명한으로 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="d9a82-301">이러한 API를 호출하면 이전에 할당된 리소스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9a82-302">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9a82-302">Next Steps</span></span>

<span data-ttu-id="d9a82-303">이 문서에서는 hello에서 hello 라이브러리를 사용 하 여 hello 기본적인 **C에 대 한 Azure IoT 장치 SDK**합니다. 충분 한 정보 toounderstand hello SDK의 아키텍처 및 tooget 시작 샘플 Windows hello를 사용 하는 방법에 포함 된 항목을 집니까 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="d9a82-304">hello 다음 기사를 설명 하 여 hello SDK에 대 한 hello 설명을 계속 [hello IoTHubClient 라이브러리에 대 한 자세한](iot-hub-device-sdk-c-iothubclient.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="d9a82-305">IoT 허브에 대 한 개발에 대 한 더 toolearn 참조 hello [Azure IoT Sdk][lnk-sdks]합니다.</span><span class="sxs-lookup"><span data-stu-id="d9a82-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="d9a82-306">toofurther는 IoT Hub의 hello 기능을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d9a82-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d9a82-307">[Azure IoT Edge에서 장치 시뮬레이션][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d9a82-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
