---
title: "C#과 함께 Azure IoT 지 모듈 aaaCreate | Microsoft Docs"
description: "이 자습서는 배포용 데이터 변환기 사용 하 여 모듈 toowrite 최신 Azure IoT 가장자리 NuGet 패키지를 Visual Studio Code 및 C# hello 하는 방법을 보여줍니다."
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: "azure, iot, 자습서, 모듈, nuget, vscode, csharp, edge"
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="702f2-104">C#을 사용하여 Azure IoT Edge 모듈 만들기</span><span class="sxs-lookup"><span data-stu-id="702f2-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="702f2-105">이 자습서에서는 방법에 대 한 모듈 toocreate `Azure IoT Edge` 를 사용 하 여 `Visual Studio Code` 및 `C#`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="702f2-106">이 자습서에서는 연습 환경 설정 방법과 toowrite는 [배포용](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 최신 hello 사용 하 여 데이터 변환기 모듈 `Azure IoT Edge NuGet` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="702f2-107">이 자습서는 hello를 사용 하 여 `.NET Core SDK`, 플랫폼 간 호환성 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="702f2-108">hello 다음 자습서 쓰여집니다 hello를 사용 하 여 `Windows 10` 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="702f2-109">이 자습서에서는 hello 명령 중 일부에 따라 다를 수 있습니다 프로그램 `development environment`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="702f2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="702f2-110">Prerequisites</span></span>

<span data-ttu-id="702f2-111">이 섹션에서는 `Azure IoT Edge` 모듈 개발을 위한 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="702f2-112">Tooboth 적용 **64 비트 Windows** 및 **64 비트 Linux (Debian Ubuntu/8)** 운영 체제.</span><span class="sxs-lookup"><span data-stu-id="702f2-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="702f2-113">hello 소프트웨어 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-113">hello following software is required:</span></span>

- [<span data-ttu-id="702f2-114">Git 클라이언트</span><span class="sxs-lookup"><span data-stu-id="702f2-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="702f2-115">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="702f2-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="702f2-116">Contact.java</span><span class="sxs-lookup"><span data-stu-id="702f2-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="702f2-117">그러나 Hello 다음 저장소에에서 있는 hello의 모든 샘플이 자습서에서 설명 하는 코드를이 샘플에 대 한 tooclone hello 리포지토리 않아도:</span><span class="sxs-lookup"><span data-stu-id="702f2-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="702f2-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`</span><span class="sxs-lookup"><span data-stu-id="702f2-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="702f2-119">시작</span><span class="sxs-lookup"><span data-stu-id="702f2-119">Getting started</span></span>

1. <span data-ttu-id="702f2-120">`.NET Core SDK`를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="702f2-121">설치 `Visual Studio Code` 및 hello `C# extension` hello Visual Studio Code 마켓플레이스에에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="702f2-122">이 메시지를 볼 [간략 한 비디오 자습서](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) 를 사용 하 여 tooget을 시작 하는 방법에 대 한 `Visual Studio Code` 및 hello `.NET Core SDK`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="702f2-123">Hello Azure IoT 지 변환기 모듈 만들기</span><span class="sxs-lookup"><span data-stu-id="702f2-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="702f2-124">새 `.NET Core` 클래스 라이브러리 C# 프로젝트를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="702f2-125">명령 프롬프트(`Windows + R` -> `cmd` -> `enter`)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="702f2-126">원하는 사이트로 toocreate hello toohello 폴더 탐색 `C#` 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="702f2-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="702f2-127">**dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="702f2-128">이 명령은 프로젝트 디렉터리에 `Class1.cs`라고 하는 빈 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="702f2-129">여기서 방금 만든 hello 클래스 라이브러리 프로젝트를 입력 하 여 toohello 폴더 탐색 **cd IoTEdgeConverterModule**합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="702f2-130">프로젝트 열기 hello `Visual Studio Code` 입력 하 여 **코드.**합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="702f2-131">Hello 프로젝트에서 열린 `Visual Studio Code`, hello 클릭 **IoTEdgeConverterModule.csproj** hello 다음 이미지와 같이 tooopen hello 파일:</span><span class="sxs-lookup"><span data-stu-id="702f2-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Visual Studio Code 편집 창](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="702f2-133">Hello 삽입 `XML` hello hello 닫는 사이의 코드 조각 뒤에 표시 된 blob `PropertyGroup` 태그 및 닫는 hello `Project` 태그; hello 이미지 앞의 경우 6 개 줄 및 키를 눌러 hello 파일을 저장 `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="702f2-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="702f2-134">Hello를 저장 하면 `.csproj` 파일인 `Visual Studio Code` 에서 메시지를 표시 하는 `unresolved dependencies` hello 다음 이미지와 같이 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="702f2-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Visual Studio Code 복원 종속성 대화 상자](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="702f2-136">a) 클릭 `Restore` hello 프로젝트에서 참조 하는 모든 hello toorestore `.csproj` hello를 포함 하 여 파일 `PackageReferences` 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="702f2-137">b) `Visual Studio Code` hello를 자동으로 만듭니다 `project.assets.json` 프로젝트에서 파일 `obj` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="702f2-138">이 파일을 사용 하면 프로젝트의 종속성 toomake 후속 복원이 단축 하는 방법에 대 한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="702f2-139">`.NET Core Tools`는 MSBuild 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="702f2-140">즉 `.csproj` 프로젝트 파일이 `project.json` 대신 만들어짐을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="702f2-141">`Visual Studio Code`에서 이에 대한 확인 메시지가 표시되지 않으면 수동으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="702f2-142">열기 hello `Visual Studio Code` 키를 눌러 hello에서 터미널 윈도우를 통합된 `Ctrl`  +  `backtick` 키 또는 hello 메뉴를 사용 하 여 `View`  ->  `Integrated Terminal`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="702f2-143">Hello에 `Integrated Terminal` 창 유형을 **dotnet 복원**합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="702f2-144">Hello 이름 바꾸기 `Class1.cs` 파일 너무`BleConverterModule.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="702f2-145">a) toorename hello 파일 먼저 hello 파일을 클릭 한 후 hello를 눌러 `F2` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="702f2-146">b) hello 새 이름 입력 **BleConverterModule**hello 다음 이미지와 같이,:</span><span class="sxs-lookup"><span data-stu-id="702f2-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Visual Studio Code 클래스 이름 바꾸기](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="702f2-148">Hello의 기존 코드 hello `BleConverterModule.cs` 파일 복사 및 붙여넣기 hello 다음 코드 조각에 의해 프로그램 `BleConverterModule.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. <span data-ttu-id="702f2-149">키를 눌러 hello 파일을 저장 `Ctrl`  +  `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="702f2-150">새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` hello 다음 이미지와 같이 키:</span><span class="sxs-lookup"><span data-stu-id="702f2-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Visual Studio Code 새 파일](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="702f2-152">toodeserialize hello `JSON` hello 시뮬레이션에서 수신 하는 개체 `BLE` 장치, hello에 코드를 다음 복사 hello `Untitled-1` 파일 코드 편집기 창입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. <span data-ttu-id="702f2-153">Hello 파일으로 저장 `BleData.cs` 키를 눌러 `Ctrl`  +  `Shift`  +  `S` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="702f2-154">Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `C# (*.cs;*.csx)` hello 다음 이미지와 같이:</span><span class="sxs-lookup"><span data-stu-id="702f2-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Visual Studio Code 다른 이름으로 저장 대화 상자](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="702f2-156">새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="702f2-157">복사 및 붙여넣기 hello에 코드 조각을 다음 hello `Untitled-1` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="702f2-158">이 클래스는는 `Azure IoT Edge` 에서 받은 toooutput hello 데이터를 활용 하는 모듈에 우리의 `BleConverterModule`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. <span data-ttu-id="702f2-159">Hello 파일으로 저장 `DotNetPrinterModule.cs` 키를 눌러 `Ctrl`  +  `Shift`  +  `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="702f2-160">Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `C# (*.cs;*.csx)`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="702f2-161">새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="702f2-162">toodeserialize hello `JSON` hello에서 수신 하는 개체 `BleConverterModule`, 복사 및 붙여넣기 hello 다음 코드 조각을 hello `Untitled-1` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. <span data-ttu-id="702f2-163">Hello 파일으로 저장 `BleConverterData.cs` 키를 눌러 `Ctrl`  +  `Shift`  +  `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="702f2-164">Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `C# (*.cs;*.csx)`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="702f2-165">새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="702f2-166">복사 및 붙여넣기 hello에 코드 조각을 다음 hello `Untitled-1` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. <span data-ttu-id="702f2-167">Hello 파일으로 저장 `gw-config.json` 키를 눌러 `Ctrl`  +  `Shift`  +  `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="702f2-168">Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="702f2-169">디렉터리를 업데이트 hello 출력 tooenable hello 구성 파일 toohello 복사 `IoTEdgeConverterModule.csproj` XML blob을 따라 hello로:</span><span class="sxs-lookup"><span data-stu-id="702f2-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="702f2-170">업데이트 하는 hello `IoTEdgeConverterModule.csproj` hello와 비슷한 모양의 이미지를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Visual Studio Code 업데이트된 .csproj 파일](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="702f2-172">새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="702f2-173">복사 및 붙여넣기 hello에 코드 조각을 다음 hello `Untitled-1` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="702f2-174">Hello 파일으로 저장 `binplace.ps1` 키를 눌러 `Ctrl`  +  `Shift`  +  `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="702f2-175">Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="702f2-176">키를 눌러 hello hello 프로젝트를 빌드할 `Ctrl`  +  `Shift`  +  `B` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="702f2-177">처음으로 hello에 대 한 hello 프로젝트를 빌드할 때 `Visual Studio Code` hello 묻는 `No build task defined.` hello 다음 이미지와 같이 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="702f2-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Visual Studio Code 빌드 작업 대화 상자](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="702f2-179">a) hello 클릭 `Configure Build Task` 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="702f2-180">b)에서 hello `Select a Task Runner` 대화 상자 드롭다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="702f2-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="702f2-181">선택 `.NET Core` hello 다음 이미지와 같이:</span><span class="sxs-lookup"><span data-stu-id="702f2-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Visual Studio Code 작업 선택 대화 상자](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="702f2-183">c) 클릭 하면 hello `.NET Core` 항목이 만드는 hello `tasks.json` 파일을 여 `.vscode` 디렉터리와 열립니다 hello hello에서 파일 `code editor` 창.</span><span class="sxs-lookup"><span data-stu-id="702f2-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="702f2-184">이 파일을 닫기 hello 탭은 필요 toomodify 없습니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="702f2-185">열기 hello `Visual Studio Code` 키를 눌러 hello에서 터미널 윈도우를 통합된 `Ctrl`  +  `backtick` 키 또는 hello 메뉴를 사용 하 여 `View`  ->  `Integrated Terminal` 유형과 **.\binplace.ps1**hello에 `PowerShell` 명령 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="702f2-186">이 명령은 우리의 모든 종속성 toohello 출력 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="702f2-187">Hello에 toohello 프로젝트 출력 디렉터리를 이동 `Integrated Terminal` 입력 하 여 창 **cd.\bin\Debug\netstandard1.3**합니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="702f2-188">입력 하 여 hello 샘플 프로젝트를 실행 **. \gw.exe gw config.json** hello에 `Integrated Terminal` 창의 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="702f2-189">이 자습서에서는 hello 단계 밀접 하 게 수행 했다면, 이제 실행 해야 hello `Azure IoT Edge BLE Data Converter Module` hello 다음 이미지와 같이 예제 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="702f2-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Visual Studio Code에서 실행하는 시뮬레이션된 장치 예제](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="702f2-191">키를 눌러 hello tooterminate hello 응용 프로그램을 사용 하도록 하려는 경우 `<Enter>` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="702f2-192">Toouse 좋습니다 `Ctrl`  +  `C` tooterminate hello `IoT Edge` 응용 프로그램 게이트웨이 (즉, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="702f2-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="702f2-193">이 작업에는 비정상적으로 hello 프로세스 tooterminate 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="702f2-193">As this action may cause hello process tooterminate abnormally.</span></span>

