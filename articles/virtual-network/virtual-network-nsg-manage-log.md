---
title: "aaaMonitor 작업, 이벤트 및 Nsg에 대 한 카운터 | Microsoft Docs"
description: "자세한 내용은 방법 tooenable 카운터, 이벤트 및 Nsg에 대 한 작업 로깅"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a>NSG(네트워크 보안 그룹)에 대한 로그 분석

Nsg에 대 한 진단 로그 범주를 수행 하는 hello를 설정할 수 있습니다.

* **이벤트:** 어떤 NSG에 대 한 규칙은 적용 된 tooVMs 및 MAC 주소에 따라 인스턴스 역할 항목을 포함 합니다. 이러한 규칙에 대 한 hello 상태 60 초 마다 수집 됩니다.
* **규칙 카운터:** Contains 항목 각 NSG 횟수에 대 한 규칙을 적용 된 toodeny 되었거나 트래픽을 허용 합니다.

> [!NOTE]
> 진단 로그는 hello Azure 리소스 관리자 배포 모델을 통해 배포 된 Nsg 수만 있습니다. Nsg hello 클래식 배포 모델을 통해 배포에 대 한 진단 로깅을 활성화할 수 없습니다. 더 잘 이해 hello 두 모델의,에 대 한 참조 hello [이해 Azure 배포 모델](../resource-manager-deployment-model.md) 문서.

활동 로깅(이전의 감사 또는 작업 로그)은 Azure 배포 모델 중 하나를 통해 만든 NSG에 대해 기본적으로 사용됩니다. 리소스 유형에 따라 hello를 포함 하는 항목에 대 한 모양 hello 활동 로그에 Nsg에 어떤 작업을 완료 된 toodetermine: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

읽기 hello [hello Azure 활동 로그 간략하게](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) 활동 로그에 대 한 자세한 문서 toolearn 합니다. 

## <a name="enable-diagnostic-logging"></a>진단 로깅 사용

에 대 한 진단 로깅을 활성화 해야 *각* NSG 원하는 toocollect 데이터에 대 한 합니다. hello [개요의 Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 진단 로그를 보낼 수 있는 문서에 설명 합니다. 전체 hello hello의 단계를 기존 NSG가 없는 경우 [네트워크 보안 그룹 만들기](virtual-networks-create-nsg-arm-pportal.md) 문서 toocreate 하나입니다. NSG 진단 hello 메서드를 다음 중 하나를 사용 하 여 로깅을 설정할 수 있습니다.

### <a name="azure-portal"></a>Azure portal

toouse hello 포털 tooenable 로깅, 로그인 toohello [포털](https://portal.azure.com)합니다. **더 많은 서비스**를 클릭한 다음 *네트워크 보안 그룹*을 입력합니다. Hello에 대 한 로깅을 tooenable 원하는 NSG를 선택 합니다. hello 비계산 리소스에 대 한 hello 지침에 따라 [hello 포털에서 진단 로그를 사용 하도록 설정](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서. **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** 또는 두 범주의 로그를 선택합니다.

### <a name="powershell"></a>PowerShell

로깅, toouse PowerShell tooenable hello 지침 hello에 따라 [PowerShell 통해 진단 로그를 사용 하도록 설정](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서. Hello 정보 hello 아티클에서 명령을 입력할 수 있도록 하기 전에 다음을 확인 합니다.

- Hello에 대 한 hello 값 toouse를 확인할 수 있습니다 `-ResourceId` hello 다음 [텍스트]를 적절 하 게 다음 hello 명령 입력을 대체 하 여 매개 변수 `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`합니다. hello 명령에서 hello ID 출력은 너무 유사*/subscriptions/ [구독 Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*합니다.
- Toocollect 데이터 로그 범주를 원하는 경우 추가 `-Categories [category]` toohello 범주는 하나 hello 문서의 hello 명령 끝 *NetworkSecurityGroupEvent* 또는 *NetworkSecurityGroupRuleCounter*. Hello를 사용 하지 않으면 `-Categories` 범주 로그 둘 다에 대 한 데이터 컬렉션 매개 변수를 사용 하도록 설정 합니다.

### <a name="azure-command-line-interface-cli"></a>Azure CLI(명령줄 인터페이스)

toouse CLI tooenable 로깅 hello, hello 지침 hello에 따라 [CLI 통해 진단 로그를 사용 하도록 설정](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) 문서. Hello 정보 hello 아티클에서 명령을 입력할 수 있도록 하기 전에 다음을 확인 합니다.

- Hello에 대 한 hello 값 toouse를 확인할 수 있습니다 `-ResourceId` hello 다음 [텍스트]를 적절 하 게 다음 hello 명령 입력을 대체 하 여 매개 변수 `azure network nsg show [resource-group-name] [nsg-name]`합니다. hello 명령에서 hello ID 출력은 너무 유사*/subscriptions/ [구독 Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*합니다.
- Toocollect 데이터 로그 범주를 원하는 경우 추가 `-Categories [category]` toohello 범주는 하나 hello 문서의 hello 명령 끝 *NetworkSecurityGroupEvent* 또는 *NetworkSecurityGroupRuleCounter*. Hello를 사용 하지 않으면 `-Categories` 범주 로그 둘 다에 대 한 데이터 컬렉션 매개 변수를 사용 하도록 설정 합니다.

## <a name="logged-data"></a>기록된 데이터

JSON 형식 데이터는 두 로그에 기록됩니다. 각 로그 형식에 대해 작성 된 hello 특정 데이터 hello 다음 섹션에에서 나열 됩니다.

### <a name="event-log"></a>이벤트 로그
이 로그에는 어떤 NSG에 대 한 규칙은 적용 된 tooVMs과는 클라우드 서비스 역할 인스턴스를 기반으로 MAC 주소 정보가 포함 됩니다. 다음 예에서는 데이터 hello 각 이벤트에 대해 기록 됩니다.

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a>규칙 카운터 로그

이 로그는 각 규칙을 적용 tooresources에 대 한 정보를 포함합니다. hello 다음 예제에서는 데이터 때마다 기록 됩니다는 규칙이 적용 됩니다.

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a>로그 보기 및 분석

toolearn tooview 활동 데이터를 기록 하는 방법을 읽고 hello [hello Azure 활동 로그 간략하게](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 문서. toolearn 방법 tooview 진단 로그 데이터를 읽을 hello [개요의 Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) 문서. 진단 데이터 tooLog 분석을 보내면 hello를 사용할 수 있습니다 [Azure 네트워크 보안 그룹 분석](../log-analytics/log-analytics-azure-networking-analytics.md) 향상 된 insights (미리 보기) 관리 솔루션입니다. 
