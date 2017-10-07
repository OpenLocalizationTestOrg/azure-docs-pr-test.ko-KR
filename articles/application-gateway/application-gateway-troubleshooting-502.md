---
title: "Azure 응용 프로그램 게이트웨이 잘못 된 게이트웨이 (502) 오류 aaaTroubleshoot | Microsoft Docs"
description: "자세한 방법을 응용 프로그램 게이트웨이 502 tootroubleshoot 오류"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>응용 프로그램 게이트웨이의 잘못된 게이트웨이 오류 문제 해결

응용 프로그램 게이트웨이 사용 하는 경우 tootroubleshoot 잘못 된 게이트웨이 (502) 오류 수신 하는 방법에 대해 알아봅니다.

## <a name="overview"></a>개요

응용 프로그램 게이트웨이 구성한 후 사용자가 발생할 수 있는 hello 오류 중 하나는 "서버 오류: 502-웹 서버는 게이트웨이 또는 프록시 서버 역할을 하는 동안 잘못 된 응답을 받았습니다"입니다. 이 오류는 toohello 다음 인해 발생할 수 있습니다는 주요 이유:

* Azure Application Gateway의 [백 엔드 풀은 구성되어 있지 않거나 비어 있습니다](#empty-backendaddresspool).
* Hello Vm 또는에서 인스턴스 [정상은 VM 크기 집합](#unhealthy-instances-in-backendaddresspool)합니다.
* 백 엔드 Vm 또는 VM 크기 집합의 인스턴스는 [응답 하지 않는 toohello 기본 상태 프로브](#problems-with-default-health-probe.md)합니다.
* 사용자 지정 상태 프로브의 구성이 [잘못되었거나 부적절합니다](#problems-with-custom-health-probe.md).
* 사용자 요청과 관련된 [요청 시간 초과 또는 연결 문제입니다](#request-time-out).

## <a name="empty-backendaddresspool"></a>비어 있는 BackendAddressPool

### <a name="cause"></a>원인

응용 프로그램 게이트웨이 hello에 Vm이 없는 경우 hello 백 엔드 주소 풀에 구성 된 VM 크기 집합, 모든 고객의 요청을 라우팅할 수 없으면 하 고 잘못 된 게이트웨이 오류를 throw 합니다.

### <a name="solution"></a>해결 방법

Hello 백 엔드 주소 풀이 비어 있지 않은지 확인 하십시오. PowerShell, CLI 또는 포털을 통해 수행할 수 있습니다.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

hello 출력 hello cmdlet 앞에서 비어 있지 않은 백 엔드 주소 풀을 포함 해야 합니다. 다음은 백 엔드 VM에 대한 FQDN 또는 IP 주소로 구성된 두 개의 풀을 반환하는 예제입니다. 프로비저닝 상태입니다. hello BackendAddressPool hello 해야 ' 성공 ' 이어야 합니다.

BackendAddressPoolsText:

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>BackendAddressPool의 비정상 인스턴스

### <a name="cause"></a>원인

모든 hello 인스턴스의 BackendAddressPool 요소가 비정상적인 경우 응용 프로그램 게이트웨이 백 엔드 tooroute 사용자 요청을 없을 것. 백 엔드 인스턴스 올바르게 작동 하지만 hello 필요한 응용 프로그램을 배포 하지 않은 경우에이 hello 사례 수 있습니다.

### <a name="solution"></a>해결 방법

Hello 인스턴스 정상이 고 hello 올바르게 구성 되어 있는지 확인 합니다. 검사는 hello 백 엔드 인스턴스 수 toorespond tooa ping 내 다른 VM에는 동일한 VNet hello 합니다. 공용 끝점을 구성 하는 경우 브라우저 요청 toohello 웹 응용 프로그램 서비스 가능 인지 확인 합니다.

## <a name="problems-with-default-health-probe"></a>기본 상태 검색의 문제

### <a name="cause"></a>원인

502 오류는 또한 기본 상태 프로브 hello 부당한 수 없는 상태 tooreach 백 엔드 Vm은 합니다. 응용 프로그램 게이트웨이 인스턴스를 프로 비전 되 면 자동으로 구성 기본 상태 프로브 tooeach BackendAddressPool hello BackendHttpSetting의 속성을 사용 하 여 합니다. 사용자 입력은 필수 tooset이이 검색 합니다. 특히, 부하 분산 규칙을 구성한 경우 BackendHttpSetting와 BackendAddressPool 간에 연결이 만들어집니다. 기본 검색 이러한 연결 및 응용 프로그램 게이트웨이 시작 하에서 정기 상태 검사 연결 tooeach 인스턴스 hello BackendAddressPool hello BackendHttpSetting 요소에 지정 된 hello 포트에서 각각에 대해 구성 되어 있습니다. 다음 표에서 hello 기본 상태 프로브와 관련 된 hello 값을 나열 합니다.

| 프로브 속성 | 값 | 설명 |
| --- | --- | --- |
| 프로브 URL |http://127.0.0.1/ |URL 경로 |
| 간격 |30 |프로브 간격(초) |
| 시간 제한 |30 |프로브 시간 제한(초) |
| 비정상 임계값 |3 |프로브 재시도 횟수. hello 연속 프로브 오류 발생 횟수 hello 비정상 임계값에 도달 하면 hello 백 엔드 서버가 표시 됩니다. |

### <a name="solution"></a>해결 방법

* 기본 사이트를 구성하고 127.0.0.1에서 수신 대기 중인지를 확인합니다.
* BackendHttpSetting 80 이외의 포트를 지정 하는 경우 hello 기본 사이트에 해당 포트에서 구성 된 toolisten 이어야 합니다.
* hello 호출 toohttp://127.0.0.1:port 반환 해야 HTTP 결과 코드는 200 합니다. 이 hello 30 초 제한 시간 내 반환 되어야 합니다.
* 구성 된 포트가 열려 있고 Azure 네트워크 보안 그룹 구성 된 hello 포트에서 들어오거나 나가는 트래픽을 차단 없거나 방화벽 규칙은 확인 합니다.
* Azure 클래식 Vm 이나 클라우드 서비스 공용 IP 또는 FQDN을 사용 하는 경우 해당 하는 hello 확인 [끝점](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) 열립니다.
* Hello VM Azure Resource Manager를 통해 구성 된 응용 프로그램 게이트웨이 배포 하는 VNet hello 외부 경우 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 구성 해야 tooallow 액세스 hello에 필요한 포트입니다.

## <a name="problems-with-custom-health-probe"></a>사용자 지정 상태 검색의 문제

### <a name="cause"></a>원인

사용자 지정 상태 검색이 허용 유연성이 toohello 기본 동작을 조사 합니다. 사용자 지정 프로브를 사용할 경우 사용자는 hello 백 엔드 풀 인스턴스 비정상으로 표시 하기 전에 hello 프로브 간격, hello URL 및 경로 tootest 및 개수 실패 응답 tooaccept 구성할 수 있습니다. 다음과 같은 추가 속성 hello 추가 됩니다.

| 프로브 속성 | 설명 |
| --- | --- |
| 이름 |Hello 검색의 이름입니다. 이 이름은 백 엔드 HTTP 설정에 사용 되는 toorefer toohello 프로브입니다. |
| 프로토콜 |프로토콜은 toosend hello 프로브를 사용합니다. hello 백 엔드 HTTP 설정에 정의 된 hello 프로토콜을 사용 하는 hello 프로브 |
| 호스트 |호스트 이름 toosend hello 프로브 다중 사이트를 응용 프로그램 게이트웨이에 구성하는 경우에만 적용할 수 있습니다. VM 호스트 이름과 다릅니다. |
| Path |Hello 프로브의 상대 경로입니다. hello 유효한 경로가에서 시작 하 고 '/'입니다. hello 프로브 너무 보내집니다\<프로토콜\>://\<호스트\>:\<포트\>\<경로\> |
| 간격 |프로브 간격(초). 두 개의 연속 프로브 사이의 hello 시간 간격입니다. |
| 시간 제한 |프로브 시간 제한(초) 이 시간 제한 기간 내에서 유효한 응답 받지 hello 프로브 실패로 표시 됩니다. |
| 비정상 임계값 |프로브 재시도 횟수. hello 연속 프로브 오류 발생 횟수 hello 비정상 임계값에 도달 하면 hello 백 엔드 서버가 표시 됩니다. |

### <a name="solution"></a>해결 방법

Hello 테이블 앞으로 올바르게 구성 된 사용자 지정 상태 프로브 해당 hello 유효성을 검사 합니다. 또한 이전 toohello hello 다음 확인 문제 해결 단계:

* 해당 hello 프로브 hello를 기준으로 올바르게 지정 되어 확인 [가이드](application-gateway-create-probe-ps.md)합니다.
* 응용 프로그램 게이트웨이 단일 사이트에 대해 구성 된 경우 기본 hello 호스트에서 이름은로 지정 해야 '127.0.0.1', 그렇지 않으면 사용자 지정 프로브를 구성 하지 않는 한 합니다.
* 호출 toohttp 확인: / /\<호스트\>:\<포트\>\<경로\> HTTP 결과 코드 200 반환 합니다.
* 제한 시간 간격과 UnhealtyThreshold hello 허용 가능한 범위 이내 인지 확인 합니다.
* 프로브는 HTTPS를 사용 하는 경우 해당 hello 백 엔드 서버 hello 백 엔드 서버 자체에 fallback 인증서를 구성 하 여 SNI 필요가 있는지 확인 합니다. 
* 제한 시간 간격과 UnhealtyThreshold hello 허용 가능한 범위 이내 인지 확인 합니다.

## <a name="request-time-out"></a>요청 시간 초과

### <a name="cause"></a>원인

사용자 요청을 받으면 응용 프로그램 게이트웨이 구성 hello 규칙 toohello 요청을 적용 하 고 tooa 백 엔드 풀 인스턴스 라우팅합니다. 구성 가능한 간격의 시간에 hello 백 엔드 인스턴스의 응답을에서 기다립니다. 기본적으로 이 간격은 **30초**입니다. Application Gateway가 이 간격에서 백 엔드 응용 프로그램의 응답을 수신하지 않으면 사용자 요청에 502 오류가 표시됩니다.

### <a name="solution"></a>해결 방법

응용 프로그램 게이트웨이 사용 하면 사용자 tooconfigure이이 설정을 통해 BackendHttpSetting toodifferent 풀 적용 된 다음 일 수 있습니다. 다른 백 엔드 풀에서는 다른 BackendHttpSetting 및 다른 요청 시간 초과를 구성할 수 있습니다.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>다음 단계

Hello 앞의 단계 문제가 해결 되지 않으면 hello를 열고는 [지원 티켓](https://azure.microsoft.com/support/options/)합니다.

