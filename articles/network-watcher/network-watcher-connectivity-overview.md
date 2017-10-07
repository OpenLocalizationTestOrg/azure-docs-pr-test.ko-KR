---
title: "Azure 네트워크 감시자에서 aaaIntroduction tooconnectivity check | Microsoft Docs"
description: "이 페이지 hello 네트워크 감시자 연결 기능에 대 한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Azure 네트워크 감시자에서 소개 tooconnectivity 확인

hello 네트워크 감시자의 연결 기능을 제공 hello 기능 toocheck 가상 컴퓨터 tooa 가상 컴퓨터 (VM) 정규화 된 도메인 이름 (FQDN) URI의에서 직접 TCP 연결 또는 IPv4 주소입니다. 네트워크 시나리오는 복잡하며, Azure에서 제공하는 네트워크 보안 그룹, 방화벽, 사용자 정의 경로 및 리소스를 사용하여 구현됩니다. 복잡한 구성은 연결 문제 해결을 어렵게 만듭니다. 네트워크 감시자를 사용 하면 시간 toofind의 hello 양을 줄일 수 및 연결 문제를 감지 합니다. 반환 된 hello 결과 tooa 플랫폼 또는 사용자 구성 문제로 인해 연결에 문제가 인지에 대 한 정보를 제공할 수 있습니다. 연결은 [PowerShell](network-watcher-connectivity-powershell.md), [Azure CLI](network-watcher-connectivity-cli.md) 및 [REST API](network-watcher-connectivity-rest.md)로 확인할 수 있습니다.

> [!IMPORTANT]
> 연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다. Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>응답

다음 표에서 hello 연결성 확인의 실행이 완료 하는 경우 반환 하는 hello 속성을 보여 줍니다.

|속성  |설명  |
|---------|---------|
|ConnectionStatus     | hello 연결성 확인의 hello 상태입니다. 가능한 결과는 **연결 가능** 및 **연결 불가능**입니다.        |
|AvgLatencyInMs     | 평균 대기 시간 (밀리초) hello 연결 확인 중입니다. (검사 상태가 연결 가능인 경우에만 표시됩니다.)        |
|MinLatencyInMs     | Hello 연결 중 최소 대기 시간 (밀리초) 확인 합니다. (검사 상태가 연결 가능인 경우에만 표시됩니다.)        |
|MaxLatencyInMs     | Hello 연결 하는 동안 최대 대기 시간 (밀리초)를 확인 합니다. (검사 상태가 연결 가능인 경우에만 표시됩니다.)        |
|ProbesSent     | Hello 검사 중에 보낸 검색 작업의 수입니다. 최대값은 100입니다.        |
|ProbesFailed     | Hello 검사 중 실패 한 검색 작업의 수입니다. 최대값은 100입니다.        |
|Hops     | 소스 toodestination에서 홉 경로로 홉 합니다.        |
|Hops[].Type     | 리소스의 형식입니다. 가능한 값은 **Source**, **VirtualAppliance**, **VnetLocal** 및 **Internet**입니다.        |
|Hops[].Id | Hello 홉의 고유 식별자입니다.|
|Hops[].Address | Hello 홉의 IP 주소입니다.|
|Hops[].ResourceId | Hello 홉 hello 홉이 Azure 리소스의 리소스 Id입니다. 인터넷 리소스인 경우 ResourceID는 **Internet**입니다. |
|Hops[].NextHopIds | hello 수행 하는 hello 다음 홉의 고유 식별자입니다.|
|Hops[].Issues | 컬렉션에서이 홉 hello 검사 중 발생 한 문제입니다. 문제가 없는 인 경우 hello 값이 비어 있습니다.|
|Hops[].Issues[].Origin | 문제가 발생 한 hello 현재 한 홉 합니다. 가능한 값은 다음과 같습니다.<br/> **인바운드** -문제는 hello 이전 홉 toohello 현재 홉에서 hello 링크<br/>**아웃 바운드** -문제는 hello 현재 홉 toohello 다음 홉에서 hello 링크<br/>**로컬** -hello 현재 홉 문제입니다.|
|Hops[].Issues[].Severity | 검색 된 hello 문제의 hello 심각도입니다. 가능한 값은 **Error** 및 **Warning**입니다. |
|Hops[].Issues[].Type |hello 유형의 문제가 있습니다. 가능한 값은 다음과 같습니다. <br/>**CPU**<br/>**메모리**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Hops[].Issues[].Context |발견 한 문제를 hello에 대 한 세부 정보입니다.|
|Hops[].Issues[].Context[].key |Hello 키-값 쌍의 키를 반환 합니다.|
|Hops[].Issues[].Context[].value |Hello 키-값 쌍의 값이 반환 됩니다.|

hello 다음은 프로그램에서 문제가 발견 한 홉의 예입니다.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>오류 형식

hello 연결성 확인 hello 연결에 대 한 오류 유형을 반환합니다. hello 다음 표에서 목록을 제공 hello 현재 오류 유형을 반환 합니다.

|형식  |설명  |
|---------|---------|
|CPU     | 높은 CPU 사용률       |
|메모리     | 높은 메모리 사용률       |
|GuestFirewall     | 가상 컴퓨터 방화벽 구성 tooa 인해 트래픽이 차단 됩니다.        |
|DNSResolution     | Hello 대상 주소에 대 한 DNS 확인에 실패 했습니다.        |
|NetworkSecurityRule    | 트래픽이 NSG 규칙에 의해 차단되었습니다(규칙이 반환됨).        |
|UserDefinedRoute|트래픽은 기한 tooa 사용자 정의 또는 시스템 경로 삭제 됩니다. |

### <a name="next-steps"></a>다음 단계

자세한 내용은 방법 방문 하 여 tooverify 연결 tooa 리소스: [Azure 네트워크 감시자와의 연결을 확인](network-watcher-connectivity-powershell.md)합니다.

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

