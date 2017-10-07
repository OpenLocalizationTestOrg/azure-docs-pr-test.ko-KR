---
title: "클라우드 서비스와 Azure 진단 (.NET) aaaHow toouse | Microsoft Docs"
description: "Azure 진단 toogather를 사용 하 여 Azure로에서 데이터 클라우드 서비스 디버깅을 위해 성능, 모니터링, 트래픽 분석 및 더를 측정 합니다."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a>Azure Cloud Services에서 Azure 진단 사용
Azure 진단의 배경은 [Azure 진단 개요](../azure-diagnostics.md)를 참조하세요.

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a>어떻게 tooEnable 작업자 역할에서 진단
이 연습 하는 Azure 작업자 역할을 사용 하 여 원격 분석 데이터를 내보내는 tooimplement.NET EventSource 클래스 hello 하는 방법을 설명 합니다. Azure 진단을 사용 하는 toocollect hello 원격 분석 데이터 이며 Azure 저장소 계정에 저장 합니다. 작업자 역할을 만들 때 Visual Studio 진단 1.0 Azure Sdk for.NET 2.4 및 이전 버전의 hello 솔루션의 일부분으로 자동 설정 합니다. hello 다음 지침에서는 설명 hello hello 솔루션에서 진단 1.0을 사용 하지 않도록 설정 하 고 진단 1.2 배포 hello 작업자 역할 또는 1.3 tooyour 작업자 역할을 만드는 프로세스입니다.

### <a name="prerequisites"></a>필수 조건
이 문서에서는 Azure 구독 및 Visual Studio를 사용 하는 hello Azure SDK로 가정 합니다. Azure 구독이 없는 경우 등록할 수 있습니다 hello에 대 한 [무료 평가판][Free Trial]합니다. 있는지 확인 너무[설치 및 Azure powershell 버전 0.8.7 이상을][Install and configure Azure PowerShell version 0.8.7 or later]합니다.

### <a name="step-1-create-a-worker-role"></a>1단계: 작업자 역할 만들기
1. **Visual Studio**를 시작합니다.
2. 만들기는 **Azure 클라우드 서비스** hello에서 프로젝트 **클라우드** .NET Framework 4.5를 대상으로 하는 서식 파일입니다.  "WadExample" hello 프로젝트 이름을 지정 하 고 확인을 클릭 합니다.
3. **작업자 역할**을 선택하고 확인을 클릭합니다. hello 프로젝트 생성 됩니다.
4. **솔루션 탐색기**, hello를 두 번 클릭 **WorkerRole1** 속성 파일입니다.
5. Hello에 **구성** 탭을 선택 취소 **진단 사용** toodisable 진단 1.0 (Azure SDK 2.4 및 이전 버전).
6. 솔루션 tooverify를 빌드 없음 오류가 발생 합니다.

### <a name="step-2-instrument-your-code"></a>2단계: 코드 계측
WorkerRole.cs의 hello 내용을 코드 다음 hello로 대체 합니다. hello에서 상속 되며, 클래스, SampleEventSourceWriter hello [EventSource 클래스][EventSource Class], 4 개의 로깅 메서드를 구현: **SendEnums**, **MessageMethod** , **SetOther** 및 **HighFreq**합니다. 첫 번째 매개 변수 toohello hello **WriteEvent** 메서드 hello 해당 이벤트에 대 한 hello ID를 정의 합니다. 각각 hello hello에서 구현 된 로깅 메서드를 호출 하는 무한 루프를 구현 하는 hello Run 메서드가 **SampleEventSourceWriter** 10 초 마다 클래스입니다.

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a>3단계: 작업자 역할 배포

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. Visual Studio 내에서 작업자 역할 tooAzure hello를 선택 하 여 배포 **WadExample** 다음 hello 솔루션 탐색기에서에서 프로젝트 **게시** hello에서 **빌드** 메뉴.
2. 구독을 선택합니다.
3. Hello에 **Microsoft Azure 게시 설정** 대화 상자에서 **새로 만들기...** .
4. Hello에 **클라우드 서비스 만들기 및 저장소 계정을** 대화 상자에서 입력 한 **이름** (예: "WadExample") 지역 또는 선호도 그룹을 선택 합니다.
5. 집합 hello **환경** 너무**준비**합니다.
6. 다른 **설정**을 적절히 수정하고 **게시**를 클릭합니다.
7. 배포 완료 되 면 hello 클라우드 서비스에 있는 Azure 포털에서에서 확인 한 **실행** 상태입니다.

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a>4 단계: 진단 구성 파일을 만들고 hello 확장 설치
1. Hello 다음 PowerShell 명령을 실행 하 여 hello 공용 구성 파일 스키마 정의 다운로드 합니다.

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. XML 파일 tooyour 추가 **WorkerRole1** hello를 마우스 오른쪽 단추로 클릭 하 여 프로젝트 **WorkerRole1** 프로젝트를 마우스 선택 **추가** -> **새 항목...** -> **Visual C# 항목** -> **데이터** -> **XML 파일**. "WadExample.xml" hello 파일 이름입니다.

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. Hello WadConfig.xsd hello 구성 파일에 연결 합니다. Hello WadExample.xml 편집기 창의 hello 활성 창 인지 확인 합니다. 키를 눌러 **F4** tooopen hello **속성** 창. Hello 클릭 **스키마** hello에 대 한 속성 **속성** 창. Hello 클릭 **...** hello에 **스키마** 속성입니다. Hello 클릭 **추가 중...** 단추 한 toohello hello XSD 파일 및 WadConfig.xsd 선택 hello 파일을 저장 한 위치로 이동 합니다. **확인**을 클릭합니다.

4. Hello WadExample.xml 구성 파일의 내용을 hello로 바꾸고 다음과 같은 XML hello hello 파일을 저장 합니다. 이 구성 파일에는 몇 가지 성능 카운터 toocollect 정의: CPU 사용률 및 메모리 사용률에 대 한 하나 있습니다. 그런 다음 hello 구성은 toohello 메서드 hello SampleEventSourceWriter 클래스에 해당 하는 hello 네 개의 이벤트를 정의 합니다.

```xml
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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a>5단계: 작업자 역할에 진단 설치
hello 웹 또는 작업자 역할에서 진단을 관리 하기 위한 PowerShell cmdlet은: 집합 AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension 및 AzureServiceDiagnosticsExtension 제거 합니다.

1. Azure PowerShell을 엽니다.
2. 작업자 역할에서 실행 하는 hello 스크립트 tooinstall 진단 (대체 *StorageAccountKey* wadexample 저장소 계정에 대 한 hello 저장소 계정 키를 가진 및 *config_path* hello 경로로 toohello *WadExample.xml* 파일):

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a>6단계: 원격 분석 데이터 확인
Hello Visual Studio에서에서 **서버 탐색기**, toohello wadexample 저장소 계정 이동 합니다. Hello 테이블 hello 클라우드 서비스 실행 약 5 분 후 나타나야 **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** 및 **WADSetOtherTable**합니다. Hello 테이블 tooview hello 원격 분석 수집 된 중 하나를 두 번 클릭 합니다.

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a>구성 파일 스키마
hello 진단 구성 파일 값 hello 진단 에이전트가 시작 될 때 진단 구성 설정을 사용 하는 tooinitialize을 정의 합니다. Hello 참조 [최신 스키마 참조](https://msdn.microsoft.com/library/azure/mt634524.aspx) 유효한 값 및 예입니다.

## <a name="troubleshooting"></a>문제 해결
문제가 있는 경우 일반적인 문제에 대한 도움말인 [Azure 진단 문제 해결](../azure-diagnostics-troubleshooting.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
[관련된 Azure 가상 컴퓨터 진단 문서 목록을 보려면](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello 데이터를 수집 하는 문제를 해결 하거나 일반적 진단에 대 한 자세한 합니다.

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
