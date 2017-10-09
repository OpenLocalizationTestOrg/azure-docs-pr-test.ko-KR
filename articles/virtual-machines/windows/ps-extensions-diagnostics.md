---
title: "Windows VM에서 Azure PowerShell tooenable 진단 aaaUse | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "자세한 내용은 방법 toouse Windows를 실행 하는 가상 컴퓨터에서 PowerShell tooenable Azure 진단"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Windows를 실행 하는 가상 컴퓨터에서 PowerShell tooenable Azure 진단을 사용합니다
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Azure 진단은 hello 배포 된 응용 프로그램에서 진단 데이터 수집을 사용 하면 Azure 내에서 hello 기능입니다. Hello 진단 확장 toocollect 진단 데이터와 같은 응용 프로그램 로그 나 Windows를 실행 하는 Azure 가상 컴퓨터 (VM)에서 성능 카운터를 사용할 수 있습니다. 이 문서에서는 toouse Windows PowerShell tooenable VM에 대 한 진단 확장을 hello 하는 방법을 설명 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello이이 문서에 필요한 필수 구성 요소에 대 한 합니다.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Hello 리소스 관리자 배포 모델을 사용 하는 경우 hello 진단 확장을 사용 하도록 설정
Hello 확장 구성 toohello 리소스 관리자 템플릿을 추가 하 여 hello Azure 리소스 관리자 배포 모델을 통해 Windows VM을 만드는 동안 hello 진단 확장을 사용할 수 있습니다. 참조 [hello Azure 리소스 관리자 템플릿을 사용 하 여 Windows 가상 컴퓨터를 모니터링 및 진단을 작성](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

hello 리소스 관리자 배포 모델을 통해 생성 된 기존 VM에 tooenable hello 진단 확장을 hello를 사용할 수 있습니다 [집합 AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) 아래 표시 된 대로 PowerShell cmdlet입니다.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* hello에 설명 된 대로 hello 진단 구성을 XML에 포함 된 hello 경로 toohello 파일은 [샘플](#sample-diagnostics-configuration) 아래 합니다.  

Hello 진단 구성 파일을 지정 하는 경우는 **StorageAccount** 저장소 계정 이름 가진 요소가 다음 hello *집합 AzureRMVMDiagnosticsExtension* 스크립트에서 자동으로 hello 설정 진단 확장 toosend 진단 데이터 toothat 저장소 계정입니다. 이 toowork hello 저장소 계정이 필요 합니다.에 toobe hello VM으로 동일한 구독 hello 합니다.

없는 경우 **StorageAccount** hello에 toopass 필요 hello 진단 구성에 지정 된 *StorageAccountName* toohello cmdlet 매개 변수입니다. 경우 hello *StorageAccountName* hello cmdlet은 항상 hello 매개 변수에서 지정 된 hello 저장소 계정을 사용 하 여를 하지 hello 하나 hello 진단 구성 파일에 지정 된 다음 매개 변수를 지정 합니다.

Hello의 hello 진단 저장소 계정 tooexplicitly 필요 hello VM에서에서 다른 구독에는 통과 하면 *StorageAccountName* 및 *StorageAccountKey* toohello cmdlet 매개 변수입니다. hello *StorageAccountKey* 자동으로 쿼리 하 고 hello 진단 확장을 사용 하도록 설정할 때 hello 키 값을 설정할 수 hello cmdlet으로 hello 진단 저장소 계정이 동일한 구독을 hello 매개 변수가 필요 하지 않습니다. 그러나 hello 진단 저장소 계정이 다른 구독에는 hello cmdlet 하지 못할 수 tooget hello 키 자동으로 고 tooexplicitly 필요한 hello 통해 hello 키 지정 *StorageAccountKey* 매개 변수입니다.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Hello 진단 확장 VM에서 활성화 되 면 hello를 사용 하 여 hello 현재 설정을 가져올 수 있습니다 [Get AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

hello cmdlet 반환 *PublicSettings*, hello 진단 구성을 포함 하 합니다. WadCfg 및 xmlCfg의 두 종류의 구성이 지원됩니다. WadCfg는 JSON 구성이며 xmlCfg는 Base64 인코딩 형식의 XML 구성입니다. tooread XML hello, toodecode 필요한 것입니다.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

hello [제거 AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet hello VM에서에서 사용 되는 tooremove hello 진단 확장 될 수 있습니다.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Hello 클래식 배포 모델을 사용 하는 경우 hello 진단 확장을 사용 하도록 설정
Hello를 사용할 수 있습니다 [집합 AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable hello 클래식 배포 모델을 통해 만든 VM에 진단 확장 합니다. hello 다음 예제에서는 어떻게 toocreate hello 진단 확장이 적용 된 hello 클래식 배포 모델을 통해 새 VM 설정

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

hello 클래식 배포 모델을 처음 사용 하 여 hello 통해 생성 된 기존 VM에 tooenable hello 진단 확장 [Get-azurevm](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM 구성 합니다. 그런 다음 hello를 사용 하 여 hello VM 구성 tooinclude hello 진단 확장을 업데이트 [집합 AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet. 마지막으로 업데이트 하는 hello 구성 toohello VM 사용 하 여 적용 한 [Update-azurevm](/powershell/module/azure/update-azurevm)합니다.

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>샘플 진단 구성
hello 스크립트 위에 hello로 hello 진단 공용 구성에 다음 XML을 사용할 수 있습니다. 이 예제 구성에서는 다양 한 성능 카운터 toohello 진단 저장소 계정에서 hello 응용 프로그램, 보안 및 시스템 채널 hello Windows 이벤트 로그에 오류와 함께 및 오류에서에서 전송 hello 진단 인프라 로그 합니다.

hello 구성 toobe 업데이트 tooinclude hello 다음 항목이 필요합니다.

* hello *resourceID* hello 특성 **메트릭** 요소 toobe hello VM에 대 한 hello 리소스 ID로 업데이트 해야 합니다.
  
  * hello 리소스 hello 패턴을 사용 하 여 ID를 생성할 수 있습니다: "/ 구독 / {*VM hello로 hello 구독에 대 한 구독 ID*} /resourceGroups/ {*helloVM에대한리소스그룹이름을hello*} / providers/Microsoft.Compute/virtualMachines/ {*VM 이름 hello*} "입니다.
  * 예를 들어 hello hello VM 실행 되 고 있는 hello 구독에 대 한 구독 ID 인지 **11111111-1111-1111-1111-111111111111**, hello 리소스 그룹에 대 한 리소스 그룹 이름이 hello **MyResourceGroup**, 그리고 hello VM 이름이 **MyWindowsVM**, 다음에 대 한 값을 hello *resourceID* 됩니다:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * 메트릭 성능 카운터에 따라 생성 된 hello 및 메트릭 구성 방법에 대 한 자세한 내용은 참조 하십시오. [저장소의 Azure 진단 메트릭 테이블](extensions-diagnostics-template.md#wadmetrics-tables-in-storage)합니다.
* hello **StorageAccount** 요소 toobe hello 진단 저장소 계정의 hello 이름으로 업데이트 해야 합니다.
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for hello VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a>다음 단계
* Hello Azure 진단 기능 및 기타 기술 tootroubleshoot 문제 사용에 대 한 추가 지침을 참조 하십시오. [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 사용](../../cloud-services/cloud-services-dotnet-diagnostics.md)합니다.
* [진단 구성 스키마](https://msdn.microsoft.com/library/azure/mt634524.aspx) hello hello 진단 확장에 대 한 다양 한 XML 구성 옵션에 대해 설명 합니다.

