---
title: "가상 컴퓨터에서 Azure 진단 aaaHow toouse | Microsoft Docs"
description: "Azure 가상 컴퓨터에서 Azure 진단 toogather 데이터를 사용 하 여 디버깅, 성능, 모니터링, 트래픽 분석 및 더를 측정 합니다."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a>Azure 가상 컴퓨터에서 진단 사용
Azure 진단의 배경은 [Azure 진단 개요](../monitoring-and-diagnostics/azure-diagnostics.md)를 참조하세요.

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a>어떻게 tooEnable 가상 컴퓨터에서 진단
이 연습을 tooremotely 개발 컴퓨터에서 진단 tooan Azure 가상 컴퓨터에 설치 하는 방법을 설명 합니다. 또한 응용 프로그램을 Azure 가상 컴퓨터에서 실행 되 고 사용 하 여 원격 분석 데이터를 내보내는 tooimplement.NET hello 하는 방법을 알아봅니다 [EventSource 클래스][EventSource Class]합니다. Azure 진단 사용 되는 toocollect hello 원격 분석이 Azure 저장소 계정에 저장 합니다.

### <a name="pre-requisites"></a>필수 조건
이 연습을 Azure 구독 및 Visual Studio 2017 hello Azure SDK를 사용 하는 가정 합니다. Azure 구독이 없는 경우 등록할 수 있습니다 hello에 대 한 [무료 평가판][Free Trial]합니다. 있는지 확인 너무[설치 및 Azure powershell 버전 0.8.7 이상을][Install and configure Azure PowerShell version 0.8.7 or later]합니다.

### <a name="step-1-create-a-virtual-machine"></a>1단계: 가상 컴퓨터 만들기
1. 개발 컴퓨터에서 Visual Studio 2017을 실행합니다.
2. Hello Visual Studio에서에서 **서버 탐색기** 확장 **Azure**를 마우스 오른쪽 단추로 클릭 **가상 컴퓨터** 다음 선택 **가상 컴퓨터 만들기**합니다.
3. Hello에서 Azure 구독 선택 **구독 선택** 대화 상자와 클릭 **다음**합니다.
4. 선택 **Windows Server 2012 R2 Datacenter, 2017 년 6 월** hello에 **가상 컴퓨터 이미지 선택** 대화 상자와 클릭 **다음**합니다.
5. Hello에 **가상 컴퓨터 기본 설정**, 너무 hello 가상 컴퓨터 이름 설정 "wadexample"입니다. 관리자 사용자 이름과 암호를 설정하고 **다음**을 클릭합니다.
6. Hello에 **클라우드 서비스 설정** 대화 "wadexampleVM" 라는 새 클라우드 서비스를 만듭니다. "wadexample"이라는 새 저장소 계정을 만들고 **다음**을 클릭합니다.
7. **만들기**를 클릭합니다.

### <a name="step-2-create-your-application"></a>2단계: 응용 프로그램 만들기
1. 개발 컴퓨터에서 Visual Studio 2017을 실행합니다.
2. .NET Framework 4.5를 대상으로 하는 새 Visual C# 콘솔 응용 프로그램을 만듭니다. "WadExampleVM" hello 프로젝트 이름입니다.

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. Program.cs의 내용을 hello 코드 다음 hello로 대체 합니다. 클래스를 hello **SampleEventSourceWriter** 4 개의 로깅 메서드를 구현: **SendEnums**, **MessageMethod**, **SetOther** 및  **HighFreq**합니다. hello 첫 번째 매개 변수 toohello WriteEvent 메서드 hello 해당 이벤트에 대 한 hello ID를 정의합니다. 각각 hello hello에서 구현 된 로깅 메서드를 호출 하는 무한 루프를 구현 하는 hello Run 메서드가 **SampleEventSourceWriter** 10 초 마다 클래스입니다.

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. Hello 파일을 저장 하 고 선택 **솔루션 빌드** hello에서 **빌드** 메뉴 toobuild 코드입니다.

### <a name="step-3-deploy-your-application"></a>3단계: 응용 프로그램 배포
1. Hello를 마우스 오른쪽 단추로 클릭 **WadExampleVM** 프로젝트에서 **솔루션 탐색기** 선택 **파일 탐색기에서 폴더 열기**합니다.
2. Toohello 이동 *bin\Debug* 폴더 및 모든 hello 복사 (WadExampleVM.*) 파일
3. **서버 탐색기** hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 선택 **원격 데스크톱을 사용 하 여 연결**합니다.
4. Toohello VM에 연결 되 면 WadExampleVM 라는 폴더를 만들고 hello 폴더에 응용 프로그램 파일을 붙여 넣습니다.
5. Hello WadExampleVM.exe 응용 프로그램을 시작 합니다. 빈 콘솔 창이 표시됩니다.

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a>4 단계: 진단 구성을 만들고 hello 확장 설치
1. Hello 다음 PowerShell 명령을 실행 하 여 hello 공용 구성 파일 스키마 정의 tooyour 개발 컴퓨터를 다운로드 합니다.

     (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
2. Visual Studio에서 새 XML 파일을 엽니다. 이미 열려 있는 프로젝트에서 새로 열거나 열려 있는 프로젝트가 없는 Visual Studio 인스턴스에서 열면 됩니다. Visual Studio에서 **추가** -> **새 항목...**을 선택합니다. -> **Visual C# 항목** -> **데이터** -> **XML 파일**. "WadExample.xml" hello 파일 이름
3. Hello WadConfig.xsd hello 구성 파일에 연결 합니다. Hello WadExample.xml 편집기 창의 hello 활성 창 인지 확인 합니다. 키를 눌러 **F4** tooopen hello **속성** 창. Hello 클릭 **스키마** hello에 대 한 속성 **속성** 창. Hello 클릭 **...** hello에 **스키마** 속성입니다. Hello 클릭 **추가 중...** 단추 한 toohello hello XSD 파일 및 WadConfig.xsd 선택 hello 파일을 저장 한 위치로 이동 합니다. **확인**을 클릭합니다.
4. Hello WadExample.xml 구성 파일의 내용을 hello로 바꾸고 다음과 같은 XML hello hello 파일을 저장 합니다. 이 구성 파일에는 몇 가지 성능 카운터 toocollect 정의: CPU 사용률 및 메모리 사용률에 대 한 하나 있습니다. 그런 다음 hello 구성은 toohello 메서드 hello SampleEventSourceWriter 클래스에 해당 하는 hello 네 개의 이벤트를 정의 합니다.

```
        <?xml version="1.0" encoding="utf-8"?>
        <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
              <WadCfg>
                <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
                  <PerformanceCounters scheduledTransferPeriod="PT1M">
                    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
                    <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
                      </PerformanceCounters>
                      <EtwProviders>
                        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
                              <Event id="1" eventDestination="EnumsTable"/>
                              <Event id="2" eventDestination="MessageTable"/>
                              <Event id="3" eventDestination="SetOtherTable"/>
                              <Event id="4" eventDestination="HighFreqTable"/>
                              <DefaultEvents eventDestination="DefaultTable" />
                        </EtwEventSourceProviderConfiguration>
                      </EtwProviders>
                </DiagnosticMonitorConfiguration>
              </WadCfg>
        </PublicConfig>
```

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a>5단계: Azure 가상 컴퓨터에 원격으로 진단 설치
hello VM의 진단을 관리 하기 위한 PowerShell cmdlet은: 집합 AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension 및 AzureVMDiagnosticsExtension 제거 합니다.

1. 개발자 컴퓨터에서 Azure PowerShell을 엽니다.
2. VM에서 실행 하는 hello 스크립트 tooremotely 설치 진단 (대체 `<user>` 을 사용자 디렉터리 이름입니다. 대체 `<StorageAccountKey>` wadexamplevm 저장소 계정에 대 한 hello 저장소 계정 키를 가진):
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a>6단계: 원격 분석 데이터 확인
Hello Visual Studio에서에서 **서버 탐색기** toohello wadexample 저장소 계정을 탐색 합니다. Hello VM을 실행 하 고 약 5 분 후 hello 테이블 표시 되어야 **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** 및 **WADSetOtherTable**합니다. Hello 테이블 tooview hello 원격 분석 수집 된 중 하나에 두 번 클릭 합니다.

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a>구성 파일 스키마
hello 진단 구성 파일 값 hello 진단 에이전트가 시작 될 때 진단 구성 설정을 사용 하는 tooinitialize을 정의 합니다. Hello 참조 [최신 스키마 참조](https://msdn.microsoft.com/library/azure/mt634524.aspx) 유효한 값 및 예입니다.

## <a name="troubleshooting"></a>문제 해결
자세한 내용은 [Azure 진단 문제 해결](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
[가상 컴퓨터의 목록을 참조 하십시오 관련 Azure 진단 문서](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello 데이터를 수집 하는 문제를 해결 하거나 일반적 진단에 대 한 자세한 합니다.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
