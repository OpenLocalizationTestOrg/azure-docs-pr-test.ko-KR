---
title: "Windows에서 C를 사용하여 장치 연결 | Microsoft Docs"
description: "Windows에서 실행되는 C로 작성된 응용 프로그램을 사용하여 미리 구성된 Azure IoT Suite 원격 모니터링 솔루션에 장치를 연결하는 방법을 설명합니다."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: d222bcbd64f288d4091acb0ecd2922b9ceee57e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="2f91b-103">미리 구성된 원격 모니터링 솔루션에 장치 연결(Windows)</span><span class="sxs-lookup"><span data-stu-id="2f91b-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="2f91b-104">Windows에서 C 샘플 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="2f91b-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="2f91b-105">다음 단계에서는 미리 구성된 원격 모니터링 솔루션과 통신하는 클라이언트 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="2f91b-106">이 응용 프로그램은 C로 작성되었으며 Windows에서 작성 및 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="2f91b-107">Visual Studio 2015 또는 Visual Studio 2017에서 시작 프로젝트를 만들고 IoT Hub 장치 클라이언트 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="2f91b-108">Visual Studio에서 Visual C++ **Win32 콘솔 응용 프로그램** 템플릿을 사용하여 C 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="2f91b-109">프로젝트 이름을 **RMDevice**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="2f91b-110">**Win32 응용 프로그램 마법사**의 **응용 프로그램 설정** 페이지에서 **콘솔 응용 프로그램**이 선택되어 있는지 확인하고 **미리 컴파일된 헤더** 및 **SDL(Security Development Lifecycle) 검사**의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="2f91b-111">**솔루션 탐색기**에서 stdafx.h, targetver.h 및 stdafx.cpp 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="2f91b-112">**솔루션 탐색기**에서 RMDevice.cpp 파일의 이름을 RMDevice.c로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="2f91b-113">**솔루션 탐색기**에서 **RMDevice** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="2f91b-114">**찾아보기**를 클릭하고 다음 NuGet 패키지를 검색하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="2f91b-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="2f91b-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="2f91b-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="2f91b-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="2f91b-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="2f91b-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="2f91b-118">**솔루션 탐색기**에서 **RMDevice** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭하여 프로젝트의 **속성 페이지** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="2f91b-119">자세한 내용은 [Visual C++ 프로젝트 속성 설정][lnk-c-project-properties]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f91b-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="2f91b-120">**Linker** 폴더를 클릭한 다음 **입력** 속성 페이지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="2f91b-121">**crypt32.lib**를 **추가 종속성** 속성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="2f91b-122">**확인**을 한 번 클릭한 다음 다시 **확인**을 클릭하여 프로젝트 속성 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="2f91b-123">Parson JSON 라이브러리를 **RMDevice** 프로젝트에 추가하고 필수 `#include` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="2f91b-124">컴퓨터의 적합한 폴더에서 다음 명령을 사용하여 Parson GitHub 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="2f91b-125">Parson 리포지토리의 로컬 복사본에서 parson.h 및 parson.c 파일을 **RMDevice** 프로젝트 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="2f91b-126">Visual Studio에서 **RMDevice** 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **추가**를 클릭하고 **기존 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="2f91b-127">**기존 항목 추가** 대화 상자에서 **RMDevice** 프로젝트 폴더의 parson.h 및 parson.c 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="2f91b-128">그런 다음 **추가**를 클릭하여 프로젝트에 이러한 두 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="2f91b-129">Visual Studio에서 RMDevice.c 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="2f91b-130">기존 `#include` 문을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-130">Replace the existing `#include` statements with the following code:</span></span>
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="2f91b-131">이제 이를 빌드하여 프로젝트에 올바른 종속성 설정이 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="2f91b-132">샘플 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="2f91b-132">Build and run the sample</span></span>

<span data-ttu-id="2f91b-133">코드를 추가하여 **remote\_monitoring\_run** 함수를 호출한 다음 장치 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="2f91b-134">**remote\_monitoring\_run** 함수를 호출하려면 **main** 함수를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="2f91b-135">**빌드**를 클릭한 다음 **솔루션 빌드**를 클릭하여 장치 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="2f91b-136">**솔루션 탐색기**에서 **RMDevice** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **디버그**를 클릭한 다음 **새 인스턴스 시작**을 클릭하여 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="2f91b-137">콘솔은 응용 프로그램이 미리 구성된 솔루션에 샘플 원격 분석을 보내고 솔루션 대시보드에 설정된 desired 속성 값을 수신하고 솔루션 대시보드에서 호출된 메서드에 응답함에 따라 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2f91b-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
