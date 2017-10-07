---
title: "aaaAdd 모니터링 및 진단 tooan Azure 가상 컴퓨터 | Microsoft Docs"
description: "Azure 진단 확장이 적용 된 Azure 리소스 관리자 템플릿 toocreate 새 Windows 가상 컴퓨터를 사용 합니다."
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Windows VM 및 Azure Resource Manager 템플릿을 사용하여 모니터링 및 진단 사용
Azure 진단 확장 hello hello 모니터링 하 고 진단 기능에는 Windows Azure 가상 컴퓨터를 기반으로 합니다. Hello azure 리소스 관리자 서식 파일의 일부로 hello 확장을 포함 하 여 hello 가상 컴퓨터에서 이러한 기능을 사용할 수 있습니다. 가상 컴퓨터 템플릿의 일부로 확장을 포함시키는 것과 관련된 자세한 내용은 [VM 확장을 사용하여 Azure 리소스 관리자 템플릿 작성](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) 을 참조하세요. 이 문서에서는 hello Azure 진단 확장 tooa windows 가상 컴퓨터 템플릿을 추가 하는 방법을 설명 합니다.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Hello Azure 진단 확장 toohello VM 리소스 정의 추가 합니다.
tooenable hello 진단 확장에서 VM 리소스로 tooadd hello 확장이 필요한 Windows 가상 컴퓨터의 리소스 관리자 템플릿을 hello 합니다.

간단한 리소스 관리자에 대 한 기반으로 가상 컴퓨터 추가 hello 확장 구성 toohello *리소스* hello 가상 컴퓨터에 대 한 배열: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


또 다른 일반적인 규칙은 hello 가상 컴퓨터의 리소스 노드 아래에서 정의 하는 대신 hello 서식 파일의 루트 리소스 노드에 hello hello 확장 구성을 추가 합니다. 이 방법을 사용 tooexplicitly hello를 사용 하 여 hello 확장과 hello 가상 컴퓨터 간의 계층 관계를 지정 해야 *이름* 및 *형식* 값입니다. 예: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

hello 확장은 항상 hello 가상 컴퓨터와 연결을 수 하거나 직접 hello 가상 컴퓨터의 리소스 노드 아래에서 직접 정의 또는 hello 기본 수준에서 정의 hello 계층적 명명 규칙 tooassociate를 사용 하 여 사용 하 여 hello 가상 컴퓨터입니다.

가상 컴퓨터 크기 집합 hello 확장에 대 한 구성이 지정 되어 있는 hello에 *extensionProfile* hello 속성 *VirtualMachineProfile*합니다.

hello *게시자* 의 hello 값을 갖는 속성 **Microsoft.Azure.Diagnostics** 및 hello *형식* 의 hello 값을 갖는 속성 **IaaSDiagnostics** hello Azure 진단 확장을 고유 하 게 식별 합니다.

값의 hello hello *이름* 속성 hello 리소스 그룹에 사용 되는 toorefer toohello 확장 될 수 있습니다. 설정 하면 특히 너무**Microsoft.Insights.VMDiagnosticsSettings** 쉽게 식별할 수 모니터링 차트 표시 hello Azure 포털에서 올바르게 hello Azure 포털 보장 hello toobe 사용 됩니다.

hello *typeHandlerVersion* hello 버전 지정 hello 확장의 toouse 원할 것입니다. 설정 *autoUpgradeMinorVersion* 부 버전이 너무**true** 하면 사용할 수 있는 hello 확장의 최신 부 버전 hello 얻을 수 있습니다. 항상 설정 하는 것이 좋습니다 *autoUpgradeMinorVersion* tooalways 수 **true** 항상 모든 hello 새로운 기능 및 버그 toouse hello 최신 사용 가능한 진단 확장을 얻을 수 있도록 해결합니다. 

hello *설정을* 요소 설정 하 고 hello 확장 (경우에 따라 참조 tooas 공용 구성)에서 다시 읽을 수 있는 hello 확장에 대 한 구성 속성을 포함 합니다. hello *xmlcfg* 속성 hello 진단 로그에 대 한 xml 기반 구성을 포함 hello 진단 에이전트에서 수집 되는 등 성능 카운터입니다. 참조 [진단 구성 스키마](https://msdn.microsoft.com/library/azure/dn782207.aspx) hello xml 스키마 자체에 대 한 자세한 내용은 합니다. 일반적인 방법은 toostore hello 실제 xml 구성 변수 hello Azure 리소스 관리자 템플릿에서 한 다음 concatenate 및 base64 인코딩 tooset hello 값에 대 한 대로 *xmlcfg*합니다. Hello 섹션을 참조 하십시오 [진단 구성 변수](#diagnostics-configuration-variables) toounderstand toostore 변수에 xml hello 하는 방법에 대 한 자세한 합니다. hello *storageAccount* 속성 지정 hello 저장소 계정 toowhich 진단 데이터의 hello 이름을 전송 됩니다. 

속성에 hello *protectedSettings* (경우에 따라 참조 tooas 개인 구성) 설정할 수 있지만 설정 된 후 다시 읽을 수 없습니다. 특성을 쓰기 전용 hello *protectedSettings* hello 저장소 계정 키와 같은 기밀 정보를 저장 하는 데 유용 hello 진단 데이터가 기록 될 합니다.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>진단 저장소 계정을 매개 변수로 지정
위의 hello 진단 확장 json 조각은 두 매개 변수를 가정 *existingdiagnosticsStorageAccountName* 및 *existingdiagnosticsStorageResourceGroup* toospecify hello 진단 진단 데이터를 저장할 저장소 계정입니다. 매개 변수가 쉽게 toochange hello 진단 저장소 계정을 사용 하면 hello 진단 저장소 계정을 지정 하 서로 다른 환경에서 예를 들어 수도 있습니다 toouse 여러 진단 저장소 계정에 대 한 한와 테스트에 대 한 사용자 프로덕션 배포 합니다.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

것이 모범 사례 toospecify hello 가상 컴퓨터에 대 한 hello 리소스 그룹이 아니라 다른 리소스 그룹의 진단 저장소 계정입니다. 리소스 그룹 toobe 배포 단위는 자체 유효 기간으로 간주할 수, 가상 컴퓨터를 배포 하 고이 새 구성을 업데이트 수행 됨에 따라 다시 배포할 수 tooit 하지만 수도 있습니다 hello에 hello 진단 데이터를 저장 하는 toocontinue 동일한 저장소 계정 해당 가상 컴퓨터 배포 합니다. 다른 리소스 사용 hello 저장소 계정 tooaccept 데이터를 쉽게 tootroubleshoot을 만드는 다양 한 가상 컴퓨터를 배포할 수 있는 hello 저장소 계정 간에 문제는 다양 한 버전 hello 합니다.

> [!NOTE]
> Hello 기본 저장소 계정을 설정할 수도 있고 Visual Studio에서 windows 가상 컴퓨터 템플릿을 만들면 toouse hello hello 가상 컴퓨터 VHD 업로드 되는 동일한 저장소 계정입니다. 이 hello VM toosimplify 초기 설정 합니다. Hello 템플릿 toouse 매개 변수로 전달 될 수 있는 다른 저장소 계정을 다시 감안해 야 합니다. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>진단 구성 변수
hello 진단 확장 json 조각은 위의 정의 *accountid* 변수 toosimplify hello 진단 저장소에 대 한 hello 저장소 계정 키 가져오기:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


hello *xmlcfg* hello 진단 확장에 대 한 속성은 서로 연결 되는 여러 변수를 사용 하 여 정의 됩니다. 이러한 변수의 hello 값은 xml 하므로, toobe hello json 변수를 설정 하는 경우 올바르게 이스케이프 처리 합니다.

hello 다음 일부 windows 이벤트 로그 및 진단 인프라 로그와 함께 표준 시스템 수준 성능 카운터를 수집 하는 hello 진단 구성 xml을 설명 합니다. 이스케이프 및 hello 구성 수 직접 붙여 넣을 있도록 서식 파일의 hello 변수 섹션에 형식이 잘못 되었습니다 했습니다. Hello 참조 [진단 구성 스키마](https://msdn.microsoft.com/library/azure/dn782207.aspx) hello 구성 xml 보다 사람이 읽을 수 있는 예입니다.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

hello 성능 카운터의 hello xml의 앞부분에 나오는 정의 하는 방법을 정의 하는 대로 구성 이상 hello hello 메트릭 정의 xml 노드에 중요 한 구성 요소 *PerformanceCounter* 노드 집계 됩니다 및 저장 됩니다. 

> [!IMPORTANT]
> 이러한 메트릭을 드라이브 hello 차트 및 hello Azure 포털에서에서 경고를 모니터링 합니다.  hello **메트릭** hello로 노드 *resourceID* 및 **MetricAggregation** toosee hello VM을 원하는 경우 VM에 대 한 hello 진단 구성에 포함 되어야 합니다 hello Azure 포털에서에서 데이터를 모니터링 합니다. 
> 
> 

hello 다음은 메트릭 정의 대 한 hello xml의 예입니다. 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

hello *resourceID* 특성 구독에서 hello 가상 컴퓨터를 고유 하 게 식별 합니다. Toouse hello subscription() 있는지를 확인 하 고 resourceGroup() 함수 hello 템플릿을 자동으로 업데이트 되도록에 배포 하는 hello 구독 및 리소스 그룹에 따라 이러한 값.

루프에서 여러 가상 컴퓨터를 만드는 경우 toopopulate hello 해야 *resourceID* copyIndex() 함수 toocorrectly 사용 하 여 값에는 각 개별 VM 구분 합니다. hello *xmlCfg* 값 업데이트 toosupport이 다음과 같을 수 있습니다.  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

MetricAggregation 값 hello *PT1H* 및 *PT1M* 분 당 집계 및 1 시간 이상 집계를 나타냅니다.

## <a name="wadmetrics-tables-in-storage"></a>저장소의 WADMetrics 테이블
위의 hello 메트릭 구성 명명 규칙을 따르는 hello로 진단 저장소 계정에서 테이블을 생성 합니다.

* **WADMetrics** : 모든 WADMetrics 테이블에 대한 표준 접두사
* **PT1H** 또는 **PT1M** : 해당 hello 테이블은 1 시간 또는 1 분 집계 데이터를 의미 합니다.
* **P10D** : hello 테이블은 hello 테이블 데이터 수집 시작 로부터 10 일에 대 한 데이터를 포함 하는 의미 합니다.
* **V2S** : 문자열 상수입니다.
* **yyyymmdd** : 테이블에는 hello 데이터 수집을 시작 하는 hello 날짜

예제: *WADMetricsPT1HP10DV2S20151108* 은 2015년 11월 11일부터 10일간 1시간 동안 수집한 메트릭 데이터를 포함합니다.    

각 WADMetrics 테이블 열을 다음 hello를 포함 됩니다.

* **PartitionKey**: hello partitionkey hello에 따라 생성 된 *resourceID* 값 toouniquely hello VM 리소스를 식별 합니다. 예: 002Fsubscriptions:<subscriptionID>:002FresourceGroups:002F<ResourceGroupName>:002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : 다음과 같이 hello 형식 <Descending time tick>:<Performance Counter Name>합니다. 시간 틱 계산 내림차순 hello는 최대 시간 틱 hello hello hello 집계 기간 시작 시간을 뺀 값입니다. 예: 샘플 기간 hello 2015-10-11 월에서 시작 되 고 00:00Hrs UTC 다음 hello 계산 하는 경우: DateTime.MaxValue.Ticks-(새 DateTime(2015,11,10,0,0,0,DateTimeKind.Utc) 합니다. 틱)입니다. Hello 메모리 bytes 성능 카운터 hello 행 키 보이는지과 같은: 2519551871999999999__:005CMemory:005CAvailable:0020 바이트
* **: _Total counterName** : hello hello 성능 카운터 이름입니다. Hello 일치 *counterSpecifier* hello xml 구성에서 정의 합니다.
* **최대** : hello 집계 기간 동안 hello 성능 카운터의 최대값을 hello 합니다.
* **최소** : hello 집계 기간 동안 hello 성능 카운터의 최소값을 hello 합니다.
* **총** : hello 성능 카운터의 모든 값의 hello 합계 hello 집계 기간에 따라 보고 합니다.
* **Count** : hello 성능 카운터에 대 한 hello 값의 총 수를 보고 합니다.
* **평균** : hello 집계 기간 동안 hello 성능 카운터의 평균 (총/개수) 값을 hello 합니다.

## <a name="next-steps"></a>다음 단계
* 진단 확장을 포함하는 Windows 가상 컴퓨터의 샘플 템플릿은 [201-vm-monitoring-diagnostics-extension](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Hello 리소스 관리자 템플릿을 사용 하 여 배포 [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Azure 명령줄](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Azure 리소스 관리자 템플릿 작성](../../resource-group-authoring-templates.md)

