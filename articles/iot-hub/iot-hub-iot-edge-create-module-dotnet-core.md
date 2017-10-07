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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>C#을 사용하여 Azure IoT Edge 모듈 만들기

이 자습서에서는 방법에 대 한 모듈 toocreate `Azure IoT Edge` 를 사용 하 여 `Visual Studio Code` 및 `C#`합니다.

이 자습서에서는 연습 환경 설정 방법과 toowrite는 [배포용](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) 최신 hello 사용 하 여 데이터 변환기 모듈 `Azure IoT Edge NuGet` 패키지 합니다. 

>[!NOTE]
이 자습서는 hello를 사용 하 여 `.NET Core SDK`, 플랫폼 간 호환성 지원입니다. hello 다음 자습서 쓰여집니다 hello를 사용 하 여 `Windows 10` 운영 체제입니다. 이 자습서에서는 hello 명령 중 일부에 따라 다를 수 있습니다 프로그램 `development environment`합니다. 

## <a name="prerequisites"></a>필수 조건

이 섹션에서는 `Azure IoT Edge` 모듈 개발을 위한 환경을 설정합니다. Tooboth 적용 **64 비트 Windows** 및 **64 비트 Linux (Debian Ubuntu/8)** 운영 체제.

hello 소프트웨어 다음이 필요 합니다.

- [Git 클라이언트](https://git-scm.com/downloads)
- [.NET Core SDK](https://www.microsoft.com/net/core#windowscmd)
- [Contact.java](https://code.visualstudio.com/)

그러나 Hello 다음 저장소에에서 있는 hello의 모든 샘플이 자습서에서 설명 하는 코드를이 샘플에 대 한 tooclone hello 리포지토리 않아도:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>시작

1. `.NET Core SDK`를 설치합니다.
2. 설치 `Visual Studio Code` 및 hello `C# extension` hello Visual Studio Code 마켓플레이스에에서 합니다.

이 메시지를 볼 [간략 한 비디오 자습서](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) 를 사용 하 여 tooget을 시작 하는 방법에 대 한 `Visual Studio Code` 및 hello `.NET Core SDK`합니다.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Hello Azure IoT 지 변환기 모듈 만들기

1. 새 `.NET Core` 클래스 라이브러리 C# 프로젝트를 초기화합니다.
    - 명령 프롬프트(`Windows + R` -> `cmd` -> `enter`)를 엽니다.
    - 원하는 사이트로 toocreate hello toohello 폴더 탐색 `C#` 프로젝트.
    - **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**을 입력합니다. 
    - 이 명령은 프로젝트 디렉터리에 `Class1.cs`라고 하는 빈 클래스를 만듭니다.
2. 여기서 방금 만든 hello 클래스 라이브러리 프로젝트를 입력 하 여 toohello 폴더 탐색 **cd IoTEdgeConverterModule**합니다.
3. 프로젝트 열기 hello `Visual Studio Code` 입력 하 여 **코드.**합니다.
4. Hello 프로젝트에서 열린 `Visual Studio Code`, hello 클릭 **IoTEdgeConverterModule.csproj** hello 다음 이미지와 같이 tooopen hello 파일:

    ![Visual Studio Code 편집 창](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Hello 삽입 `XML` hello hello 닫는 사이의 코드 조각 뒤에 표시 된 blob `PropertyGroup` 태그 및 닫는 hello `Project` 태그; hello 이미지 앞의 경우 6 개 줄 및 키를 눌러 hello 파일을 저장 `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. Hello를 저장 하면 `.csproj` 파일인 `Visual Studio Code` 에서 메시지를 표시 하는 `unresolved dependencies` hello 다음 이미지와 같이 대화 상자: 

    ![Visual Studio Code 복원 종속성 대화 상자](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    a) 클릭 `Restore` hello 프로젝트에서 참조 하는 모든 hello toorestore `.csproj` hello를 포함 하 여 파일 `PackageReferences` 추가 했습니다. 

    b) `Visual Studio Code` hello를 자동으로 만듭니다 `project.assets.json` 프로젝트에서 파일 `obj` 폴더입니다. 이 파일을 사용 하면 프로젝트의 종속성 toomake 후속 복원이 단축 하는 방법에 대 한 정보가 있습니다.
 
    >[!NOTE]
    `.NET Core Tools`는 MSBuild 기반입니다. 즉 `.csproj` 프로젝트 파일이 `project.json` 대신 만들어짐을 의미합니다.

    - `Visual Studio Code`에서 이에 대한 확인 메시지가 표시되지 않으면 수동으로 수행할 수 있습니다. 열기 hello `Visual Studio Code` 키를 눌러 hello에서 터미널 윈도우를 통합된 `Ctrl`  +  `backtick` 키 또는 hello 메뉴를 사용 하 여 `View`  ->  `Integrated Terminal`합니다.
    - Hello에 `Integrated Terminal` 창 유형을 **dotnet 복원**합니다.
    
7. Hello 이름 바꾸기 `Class1.cs` 파일 너무`BleConverterModule.cs`합니다. 

    a) toorename hello 파일 먼저 hello 파일을 클릭 한 후 hello를 눌러 `F2` 키입니다.
    
    b) hello 새 이름 입력 **BleConverterModule**hello 다음 이미지와 같이,:

    ![Visual Studio Code 클래스 이름 바꾸기](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Hello의 기존 코드 hello `BleConverterModule.cs` 파일 복사 및 붙여넣기 hello 다음 코드 조각에 의해 프로그램 `BleConverterModule.cs` 파일입니다.

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

9. 키를 눌러 hello 파일을 저장 `Ctrl`  +  `S`합니다.

10. 새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` hello 다음 이미지와 같이 키:

    ![Visual Studio Code 새 파일](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. toodeserialize hello `JSON` hello 시뮬레이션에서 수신 하는 개체 `BLE` 장치, hello에 코드를 다음 복사 hello `Untitled-1` 파일 코드 편집기 창입니다. 

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

12. Hello 파일으로 저장 `BleData.cs` 키를 눌러 `Ctrl`  +  `Shift`  +  `S` 키입니다.
    - Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `C# (*.cs;*.csx)` hello 다음 이미지와 같이:

    ![Visual Studio Code 다른 이름으로 저장 대화 상자](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. 새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` 키입니다.

14. 복사 및 붙여넣기 hello에 코드 조각을 다음 hello `Untitled-1` 파일입니다. 이 클래스는는 `Azure IoT Edge` 에서 받은 toooutput hello 데이터를 활용 하는 모듈에 우리의 `BleConverterModule`합니다.

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

15. Hello 파일으로 저장 `DotNetPrinterModule.cs` 키를 눌러 `Ctrl`  +  `Shift`  +  `S`합니다.
    - Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `C# (*.cs;*.csx)`합니다.

16. 새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` 키입니다.

17. toodeserialize hello `JSON` hello에서 수신 하는 개체 `BleConverterModule`, 복사 및 붙여넣기 hello 다음 코드 조각을 hello `Untitled-1` 파일입니다. 

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

18. Hello 파일으로 저장 `BleConverterData.cs` 키를 눌러 `Ctrl`  +  `Shift`  +  `S`합니다.
    - Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `C# (*.cs;*.csx)`합니다.

19. 새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` 키입니다.

20. 복사 및 붙여넣기 hello에 코드 조각을 다음 hello `Untitled-1` 파일입니다.

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

21. Hello 파일으로 저장 `gw-config.json` 키를 눌러 `Ctrl`  +  `Shift`  +  `S`합니다.
    - Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`합니다.

22. 디렉터리를 업데이트 hello 출력 tooenable hello 구성 파일 toohello 복사 `IoTEdgeConverterModule.csproj` XML blob을 따라 hello로:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - 업데이트 하는 hello `IoTEdgeConverterModule.csproj` hello와 비슷한 모양의 이미지를 수행 해야 합니다.

    ![Visual Studio Code 업데이트된 .csproj 파일](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. 새 파일을 만들 `Untitled-1` 키를 눌러 hello 여 `Ctrl`  +  `N` 키입니다.

24. 복사 및 붙여넣기 hello에 코드 조각을 다음 hello `Untitled-1` 파일입니다.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Hello 파일으로 저장 `binplace.ps1` 키를 눌러 `Ctrl`  +  `Shift`  +  `S`합니다.
    - Hello에 다른 이름으로 저장 대화 상자의 hello `Save as Type` 드롭다운 메뉴에서 선택 `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`합니다.

26. 키를 눌러 hello hello 프로젝트를 빌드할 `Ctrl`  +  `Shift`  +  `B` 키입니다. 처음으로 hello에 대 한 hello 프로젝트를 빌드할 때 `Visual Studio Code` hello 묻는 `No build task defined.` hello 다음 이미지와 같이 대화 상자:

    ![Visual Studio Code 빌드 작업 대화 상자](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    a) hello 클릭 `Configure Build Task` 단추입니다.

    b)에서 hello `Select a Task Runner` 대화 상자 드롭다운 메뉴. 선택 `.NET Core` hello 다음 이미지와 같이: 

    ![Visual Studio Code 작업 선택 대화 상자](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    c) 클릭 하면 hello `.NET Core` 항목이 만드는 hello `tasks.json` 파일을 여 `.vscode` 디렉터리와 열립니다 hello hello에서 파일 `code editor` 창. 이 파일을 닫기 hello 탭은 필요 toomodify 없습니다.

27.  열기 hello `Visual Studio Code` 키를 눌러 hello에서 터미널 윈도우를 통합된 `Ctrl`  +  `backtick` 키 또는 hello 메뉴를 사용 하 여 `View`  ->  `Integrated Terminal` 유형과 **.\binplace.ps1**hello에 `PowerShell` 명령 프롬프트입니다. 이 명령은 우리의 모든 종속성 toohello 출력 디렉터리에 복사합니다.

28. Hello에 toohello 프로젝트 출력 디렉터리를 이동 `Integrated Terminal` 입력 하 여 창 **cd.\bin\Debug\netstandard1.3**합니다.

29. 입력 하 여 hello 샘플 프로젝트를 실행 **. \gw.exe gw config.json** hello에 `Integrated Terminal` 창의 프롬프트입니다. 
    - 이 자습서에서는 hello 단계 밀접 하 게 수행 했다면, 이제 실행 해야 hello `Azure IoT Edge BLE Data Converter Module` hello 다음 이미지와 같이 예제 프로젝트:
    
        ![Visual Studio Code에서 실행하는 시뮬레이션된 장치 예제](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - 키를 눌러 hello tooterminate hello 응용 프로그램을 사용 하도록 하려는 경우 `<Enter>` 키입니다.

>[!IMPORTANT]
Toouse 좋습니다 `Ctrl`  +  `C` tooterminate hello `IoT Edge` 응용 프로그램 게이트웨이 (즉, **gw.exe**). 이 작업에는 비정상적으로 hello 프로세스 tooterminate 발생할 수 있습니다.

