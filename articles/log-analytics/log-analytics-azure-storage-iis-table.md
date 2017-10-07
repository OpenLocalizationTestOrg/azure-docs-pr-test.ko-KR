---
title: "Azure 로그 분석에서 이벤트에 대 한 IIS 및 테이블 저장소에 blob 저장소를 aaaUse | Microsoft Docs"
description: "로그 분석 tooblob 저장소를 작성 하는 IIS 로그 또는 진단 tootable 저장소를 작성 하는 Azure 서비스에 대 한 hello 로그를 읽을 수 있습니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Log Analytics에서 이벤트에 대해 IIS와 Azure Table Storage에 Azure Blob Storage 사용

로그 분석 저장소 또는 IIS 로그 서 면된 tooblob 저장소 tootable 진단 유틸리티를 작성 하는 서비스를 수행 하는 hello에 대 한 hello 로그를 읽을 수 있습니다.

* Service Fabric 클러스터(미리 보기)
* 가상 컴퓨터
* 웹/작업자 역할

Log Analytics에서 이러한 리소스에 대한 데이터를 수집하려면 Azure 진단을 사용하도록 설정되어 있어야 합니다.

진단 성화 hello Azure 포털을 사용할 수 있습니다 또는 PowerShell 로그 분석 toocollect hello 로그를 구성 합니다.

Azure 진단은 Azure에서 실행 중인 가상 컴퓨터, 웹 역할 또는 작업자 역할에서 toocollect 진단 데이터를 수 있는 Azure 확장입니다. hello 데이터는 Azure 저장소 계정에 저장 되 고 로그 분석에 의해 수집할 수 있습니다.

로그 분석 toocollect에 대 한 Azure 진단 로그 hello 로그에에서 있어야 hello 다음 위치:

| 로그 형식 | 리소스 종류 | 위치 |
| --- | --- | --- |
| IIS 로그 |가상 컴퓨터 <br> 웹 역할 <br> 작업자 역할 |wad-iis-logfiles(Blob Storage) |
| syslog |가상 컴퓨터 |LinuxsyslogVer2v0(Table Storage) |
| Service Fabric 작업 이벤트 |Service Fabric 노드 |WADServiceFabricSystemEventTable |
| Service Fabric Reliable Actor 이벤트 |Service Fabric 노드 |WADServiceFabricReliableActorEventTable |
| Service Fabric Reliable Service 이벤트 |Service Fabric 노드 |WADServiceFabricReliableServiceEventTable |
| Windows 이벤트 로그 |Service Fabric 노드 <br> 가상 컴퓨터 <br> 웹 역할 <br> 작업자 역할 |WADWindowsEventLogsTable(Table Storage) |
| Windows ETW 로그 |Service Fabric 노드 <br> 가상 컴퓨터 <br> 웹 역할 <br> 작업자 역할 |WADETWEventTable(Table Storage) |

> [!NOTE]
> Azure 웹사이트에서 IIS 로그는 현재 지원되지 않습니다.
>
>

가상 컴퓨터에 대 한 옵션이 있습니다 hello hello 설치 [로그 분석 에이전트](log-analytics-azure-vm-extension.md) 가상 컴퓨터 tooenable 추가로 insights를 합니다. 또한 toobeing 수 tooanalyze IIS 로그 및 이벤트 로그에 구성 변경 내용 추적, SQL 평가 및 업데이트 평가 포함 한 추가 분석을 수행할 수 있습니다.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>이벤트 로그 및 IIS 로그 컬렉션에 대한 Azure 진단을 가상 컴퓨터에서 사용
이벤트 로그와 IIS 로그 hello Microsoft Azure 포털을 사용 하 여 컬렉션에 대 한 프로시저 tooenable Azure 진단을 가상 컴퓨터에서 다음 사용 하 여 hello 합니다.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>Azure 포털 hello로 가상 컴퓨터에서 Azure 진단 tooenable
1. 가상 컴퓨터를 만들 때 hello VM 에이전트를 설치 합니다. Hello 가상 컴퓨터가 이미 있는 경우 VM 에이전트가 이미 설치 되어 해당 hello를 확인 합니다.

   * 에 Azure 포털 hello, toohello 가상 컴퓨터를 이동, 선택 **옵션 구성**, 다음 **진단** 설정 **상태** 너무**에**.

     완료 되 면 hello VM에 설치 되어 있고 실행 hello Azure 진단 확장을 있습니다. 이 확장은 진단 데이터를 수집합니다.
2. 모니터링을 설정하고 기존 VM에 대한 이벤트 로깅을 구성합니다. Hello VM 수준에서 진단을 설정할 수 있습니다. tooenable 진단 하 고 다음 이벤트 로깅을 구성 단계를 수행 하는 hello를 수행 하십시오.

   1. Hello VM을 선택 합니다.
   2. **모니터링**을 클릭합니다.
   3. **진단**을 클릭합니다.
   4. 집합 hello **상태** 너무**ON**합니다.
   5. Toocollect 하려는 각 진단 로그를 선택 합니다.
   6. **확인**을 클릭합니다.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>IIS 로그 및 이벤트 컬렉션에 대한 웹 역할에서 Azure 진단 사용
너무 참조[어떻게 tooEnable 클라우드 서비스에서 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) 에 대 한 일반 단계 Azure 진단을 사용 하도록 설정 합니다. 아래 hello 지침이이 정보를 사용 하 고 로그 분석에 사용할 사용자 지정 합니다.

Azure 진단을 사용하는 경우:

* IIS 로그는 기본적으로 hello scheduledTransferPeriod 전송 간격에 전송 하는 로그 데이터와 함께 저장 됩니다.
* Windows 이벤트 로그는 기본적으로 전송되지 않습니다.

### <a name="tooenable-diagnostics"></a>tooenable 진단
tooenable Windows 이벤트 로그 또는 toochange scheduledTransferPeriod hello, 같이 hello XML 구성 파일 (diagnostics.wadcfg)을 사용 하 여 Azure 진단 구성 [4 단계: 진단 구성 파일을 만들고 hello를 설치 합니다. 확장](../cloud-services/cloud-services-dotnet-diagnostics.md)

hello 다음 예제에서는 구성 파일에서 수집 IIS 로그 및 모든 hello 응용 프로그램에서에서 발생 한 이벤트와 시스템 로그.

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

ConfigurationSettings hello 다음 예제 처럼 저장소 계정을 지정 하는지 확인 합니다.

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

hello **AccountName** 및 **AccountKey** 값은 hello 저장소 계정 대시보드의 액세스 키 관리 아래에서 Azure 포털 hello에 있습니다. hello 연결 문자열에 대 한 hello 프로토콜 있어야 **https**합니다.

Hello 업데이트 된 진단 구성이 적용 되 고 나면 tooyour 클라우드 서비스 이므로 기록 진단 tooAzure 저장소, 준비 tooconfigure 로그 분석 중인 있습니다.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Azure 저장소에서 Azure 포털 toocollect 로그 hello를 사용 하 여
Azure 서비스를 수행 하는 hello에 대 한 hello Azure 포털 tooconfigure 로그 분석 toocollect hello 로그를 사용할 수 있습니다.

* 서비스 패브릭 클러스터
* 가상 컴퓨터
* 웹/작업자 역할

Hello Azure 포털에서에서 tooyour 로그 분석 작업 영역을 탐색 하 고 작업을 수행 하는 hello를 수행 합니다.

1. *저장소 계정 로그*를 클릭합니다.
2. Hello 클릭 *추가* 작업
3. Hello 진단 로그를 포함 하는 hello 저장소 계정을 선택합니다
   * 이 계정은 클래식 저장소 계정 또는 Azure Resource Manager 저장소 계정일 수 있습니다.
4. Hello에 대 한 toocollect 로그를 원하는 데이터 형식을 선택 합니다.
   * hello 선택 항목은 IIS 로그 이벤트입니다. Syslog (Linux); ETW 로그 서비스 패브릭 이벤트
5. 원본에 대 한 hello 값 자동으로 채워집니다 hello 데이터 입력 하 고 변경할 수 없습니다.
6. 확인 toosave hello 구성을 클릭 합니다.

로그 분석 toocollect 원하는 추가 저장소 계정 및 데이터 형식에 대해 2 ~ 6 단계를 반복 합니다.

약 30 분 수 toosee hello 저장소에서에서 계정의 데이터를 로그 분석 됩니다. 또한 hello 구성이 적용 된 후 toostorage 작성 된 데이터에 대해서만 나타납니다. 로그 분석 hello 저장소 계정에서 hello 기존의 데이터를 읽지 않습니다.

> [!NOTE]
> 새 데이터를 쓰고 또는 hello 포털 원본이 hello 저장소 계정에 해당 hello 유효성을 검사 하지 않습니다.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>PowerShell을 사용하여 이벤트 로그 및 IIS 로그 컬렉션에 대한 Azure 진단을 가상 컴퓨터에서 사용하도록 설정
단계를 사용 하 여 hello [로그 분석 구성 tooindex Azure 진단](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) tootable 저장소 작성 된 Azure 진단의 toouse PowerShell tooread 합니다.

Azure PowerShell을 사용 하 여 hello 기록 된 이벤트를 tooAzure 저장소를 보다 정확 하 게 지정할 수 있습니다.
자세한 내용은 [Azure 가상 컴퓨터에서 진단 사용](../virtual-machines-dotnet-diagnostics.md)을 참조하세요.

사용 하도록 설정 하 고 PowerShell 스크립트 뒤 hello를 사용 하 여 Azure 진단을 업데이트할 수 있습니다.
또한 사용자 지정 로깅 구성을 사용하여 이 스크립트를 사용할 수 있습니다.
Hello 스크립트 tooset hello 저장소 계정, 서비스 이름 및 가상 컴퓨터 이름을 수정 합니다.
hello 스크립트 클래식 가상 컴퓨터에 대 한 cmdlet을 사용합니다.

다음 스크립트 샘플 hello 검토, 복사, 필요에 따라 수정, hello 샘플 PowerShell 스크립트 파일로 저장 고 hello 스크립트를 실행 합니다.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>다음 단계
* 지원되는 Azure 서비스에 대해 [Azure 서비스에 대한 로그 및 메트릭 수집](log-analytics-azure-storage.md)
* [솔루션 사용](log-analytics-add-solutions.md) hello 데이터에 대 한 tooprovide 한 정보입니다.
* [검색 쿼리를 사용 하 여](log-analytics-log-searches.md) tooanalyze hello 데이터입니다.
