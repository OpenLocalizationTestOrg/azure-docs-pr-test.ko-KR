---
title: "C를 사용 하 여 Windows에서 장치 aaaConnect | Microsoft Docs"
description: "어떻게 tooconnect 장치 toohello Azure IoT Suite 미리 구성 된 Windows에서 실행 되는 C로 작성 된 응용 프로그램을 사용 하 여 원격 모니터링 솔루션에 설명 합니다."
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
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="265d1-103">사용자 장치 toohello 모니터링 미리 구성 된 솔루션 (Windows) 원격 연결</span><span class="sxs-lookup"><span data-stu-id="265d1-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="265d1-104">Windows에서 C 샘플 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="265d1-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="265d1-105">단계를 수행 하는 hello toocreate hello 원격 모니터링와 통신 하는 클라이언트 응용 프로그램 미리 솔루션을 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="265d1-106">이 응용 프로그램은 C로 작성되었으며 Windows에서 작성 및 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="265d1-107">Visual Studio 2015 또는 Visual Studio 2017에서 시작 프로젝트를 만들고 hello IoT Hub 장치 클라이언트 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="265d1-108">Visual Studio에서 Visual c + + hello를 사용 하 여 C 콘솔 응용 프로그램을 만들 **Win32 콘솔 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="265d1-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="265d1-109">이름 hello 프로젝트 **RMDevice**합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="265d1-110">Hello에 **응용 프로그램 설정** hello에서 페이지 **Win32 응용 프로그램 마법사**, 되도록 **콘솔 응용 프로그램** 을 선택 하 고의 선택을 취소 **미리 컴파일된 헤더** 및 **보안 SDL (Development Lifecycle) 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="265d1-111">**솔루션 탐색기**, hello 파일 stdafx.h, targetver.h, stdafx.cpp을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="265d1-112">**솔루션 탐색기**, hello 파일 RMDevice.cpp tooRMDevice.c 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="265d1-113">**솔루션 탐색기**, hello를 마우스 오른쪽 단추로 클릭 **RMDevice** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="265d1-114">클릭 **찾아보기**, 다음 검색 하 고 hello 다음 NuGet 패키지 설치:</span><span class="sxs-lookup"><span data-stu-id="265d1-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="265d1-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="265d1-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="265d1-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="265d1-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="265d1-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="265d1-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="265d1-118">**솔루션 탐색기**, hello를 마우스 오른쪽 단추로 클릭 **RMDevice** 프로젝트를 마우스 클릭 **속성** tooopen hello 프로젝트 **속성 페이지**대화 상자.</span><span class="sxs-lookup"><span data-stu-id="265d1-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="265d1-119">자세한 내용은 [Visual C++ 프로젝트 속성 설정][lnk-c-project-properties]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="265d1-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="265d1-120">Hello 클릭 **링커** 폴더를 클릭 hello **입력** 속성 페이지.</span><span class="sxs-lookup"><span data-stu-id="265d1-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="265d1-121">추가 **crypt32.lib** toohello **추가 종속성** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="265d1-122">클릭 **확인** 차례로 **확인** 다시 toosave hello 프로젝트 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="265d1-123">Hello Parson JSON 라이브러리 toohello 추가 **RMDevice** 필요한 hello를 더하고 프로젝트 `#include` 문:</span><span class="sxs-lookup"><span data-stu-id="265d1-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="265d1-124">컴퓨터에 적합 한 폴더에서 다음 명령을 hello를 사용 하 여 hello Parson GitHub 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="265d1-125">Hello hello Parson 리포지토리 tooyour의 로컬 복사본에서 hello parson.h 및 parson.c 파일 복사 **RMDevice** 프로젝트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="265d1-126">Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **RMDevice** 프로젝트를 클릭 하 여 **추가**, 클릭 하 고 **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="265d1-127">Hello에 **기존 항목 추가** 대화 상자에서 선택 hello parson.h parson.c에서에서 파일과 hello **RMDevice** 프로젝트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="265d1-128">클릭 **추가** tooadd 이러한 두 파일 tooyour 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="265d1-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="265d1-129">Visual Studio에서 hello RMDevice.c 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="265d1-130">Hello 기존 항목 바꾸기 `#include` 코드 다음 hello로 문:</span><span class="sxs-lookup"><span data-stu-id="265d1-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
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
    > <span data-ttu-id="265d1-131">이제 프로젝트를 빌드하는 방법 설정 hello 올바른 종속성에 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="265d1-132">빌드 및 실행 hello 샘플</span><span class="sxs-lookup"><span data-stu-id="265d1-132">Build and run hello sample</span></span>

<span data-ttu-id="265d1-133">추가 코드 tooinvoke hello **원격\_모니터링\_실행** 함수 로컬 폴더를 빌드하고 hello 장치 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="265d1-134">Hello 대체 **주** 다음 코드 tooinvoke hello로 함수 **원격\_모니터링\_실행** 함수:</span><span class="sxs-lookup"><span data-stu-id="265d1-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="265d1-135">클릭 **빌드** 차례로 **솔루션 빌드** toobuild hello 장치 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="265d1-136">**솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **RMDevice** 프로젝트를 클릭 하 여 **디버그**, 클릭 하 고 **새 인스턴스 시작** toorun hello 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="265d1-137">hello 콘솔 hello 응용 프로그램 보내는 원격 분석 toohello 샘플 솔루션을 미리 구성 된, hello 솔루션 대시보드에서 설정 원하는 속성 값을 받는 및 toomethods hello 솔루션 대시보드에서 호출 응답 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="265d1-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
