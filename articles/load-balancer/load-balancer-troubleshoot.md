---
title: "Azure 부하 분산 장치 aaaTroubleshoot | Microsoft Docs"
description: "Azure Load Balancer의 알려진 문제 해결"
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>Azure Load Balancer 문제 해결

이 페이지에서는 일반적인 Azure Load Balancer 질문에 대한 문제 해결 정보를 제공합니다. Hello 부하 분산 장치가 연결에 사용할 수 없는 경우 hello 가장 일반적인 증상은 다음과 같습니다. 
- Hello 부하 분산 장치 뒤에 있는 Vm toohealth 프로브 응답 하지 않습니다. 
- Hello 부하 분산 장치 뒤에 있는 Vm toohello 트래픽을 hello 구성 된 포트에서 응답 하지 않습니다.

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>증상: hello 부하 분산 장치 뒤에 있는 Vm toohealth 프로브 응답 하지 않습니다.
Hello 백 엔드 서버 hello 부하 분산 장치 집합의 tooparticipate에 대 한 hello 프로브 검사를 전달 해야 합니다. 상태 프로브에 대한 자세한 내용은 [Load Balancer 프로브 이해](load-balancer-custom-probe-overview.md)를 참조하세요. 

toohello 프로브 hello 부하 분산 장치 백 엔드 풀 Vm 응답 하지 않을 수 있습니다 hello 이유 뒤의 due tooany: 
- Load Balancer 백 엔드 풀 VM이 정상적인 상태가 아닙니다. 
- 부하 분산 장치 백 엔드 풀 VM hello 프로브 포트에서 수신 하지 않는 
- Hello 포트 hello 부하 분산 장치 백 엔드 풀 Vm에 차단 방화벽 또는 네트워크 보안 그룹 
- Load Balancer의 기타 구성 오류

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>원인 1: Load Balancer 백 엔드 풀 VM이 정상적인 상태가 아닙니다. 

**유효성 검사 및 해결**

tooresolve이이 문제를 toohello 참여 하 고 Vm에 로그인 하 고 hello VM 상태가 정상 인지 확인 하 고 너무 응답할 수**PsPing** 또는 **TCPing** hello 풀의 다른 VM에서. Hello VM 정상으로 아니거나은 없습니다 toorespond toohello 검색 hello 문제를 해결 하 고 부하 분산에 참여 하려면 먼저 VM tooa 정상 상태를 백업 하는 hello를 가져올 해야 합니다.

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>원인 2: 부하 분산 장치 백 엔드 풀 VM hello 프로브 포트에서 수신 하지 않는
Hello VM 정상 인지 표시 되지만 toohello 프로브 응답 하지 않는 경우 hello 프로브 포트에 열려 있지 않으면 VM에 참여 하 고 hello 또는 hello VM 해당 포트에서 수신 하지 않는 한 가지 가능한 이유 수 있습니다.

**유효성 검사 및 해결**

1. Toohello 백 엔드 VM에에서 로그인 합니다. 
2. 명령 프롬프트를 열고 다음 명령 toovalidate hello 프로브 포트에서 수신 대기 하는 응용 프로그램이 hello를 실행 합니다.   
            netstat -an
3. Hello 포트 상태로 나열 되지 않은 경우 **LISTENING**, hello 적절 한 포트를 구성 합니다. 
4. 또는 **LISTENING**으로 표시되는 다른 포트를 선택한 후 부하 분산 장치 구성을 적절하게 업데이트합니다.              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>원인 3: 방화벽 또는 네트워크 보안 그룹은 포트를 차단 hello hello 부하 분산 장치 백 엔드 풀 Vm에  
Hello 방화벽 hello 프로브 포트 또는 VM hello 또는 hello 서브넷에 구성 된 하나 이상의 네트워크 보안 그룹에 VM을 차단 하는 hello에서 허용 하는 hello 프로브 tooreach hello 포트는, hello VM은 없습니다 toorespond toohello 상태 검색.          

**유효성 검사 및 해결**

* Hello 방화벽을 사용 하는 경우 구성 하는 경우 확인 tooallow hello 프로브 포트입니다. 그렇지 않은 경우 hello 방화벽 tooallow 트래픽을 hello 프로브 포트에서 구성 하 고 다시 테스트 합니다. 
* 네트워크 보안 그룹의 hello 목록에서 hello 프로브 포트에서 들어오거나 나가는 트래픽을 hello 간섭에 있는지를 확인 합니다. 
* 확인 하는 경우는 **모두 거부** 네트워크 보안 그룹의 hello VM NIC hello에서 규칙 또는 LB 프로브 & 트래픽을 허용 하는 hello 기본 규칙 보다 더 높은 우선 순위의 서브넷 hello (네트워크 보안 그룹 허용 해야의 부하 분산 장치 IP 168.63.129.16)입니다. 
* Hello 프로브 트래픽을 차단 이러한 규칙 중 하나를 제거 하 고 hello 규칙 tooallow hello 프로브 트래픽을 다시 구성.  
* Hello VM 시작 되었습니다. 다른 toohello 상태 프로브 응답를 테스트 합니다. 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>원인 4: 부하 분산 장치의 기타 구성 오류
Hello 모든 이전 원인을 toobe 유효성을 검사 하 고 올바르게 해결 및 VM 여전히 toohello 상태 검색 응답 한 후 수동으로 연결을 테스트 하며 하지 일부 추적 toounderstand hello 연결을 수집 hello 백 엔드 하실 것입니다.

**유효성 검사 및 해결**

* 사용 하 여 **Psping** hello 중 하나에서 다른 Vm 내에서 hello VNet tootest hello 프로브 포트 응답 (예:-t 10.0.0.4:3389.\psping.exe) 결과 기록 합니다. 
* 사용 하 여 **TCPing** hello 중 하나에서 다른 Vm 내에서 hello VNet tootest hello 프로브 포트 응답 (예:.\tcping.exe 10.0.0.4 3389) 결과 기록 합니다. 
* 이러한 ping 테스트에서 응답이 수신되지 않으면 다음을 수행합니다.
    - 동시 실행 Netsh 추적 hello 대상 백 엔드 풀 VM 및 hello에서 다른 테스트 VM에 동일한 VNet입니다. 이제 일정 시간 동안 PsPing 테스트를 실행 하 고 일부 네트워크 추적을 수집 hello 테스트 한 다음 중지 합니다. 
    - Hello 네트워크 캡처 분석 하 고 두 들어오고 나가는 패킷이 관련된 toohello ping 쿼리에 있는지 확인 합니다. 
        - 수신 패킷이 hello 백 엔드 풀 VM에서이 확인 되 면 잠재적으로 네트워크 보안 그룹 또는 hello 트래픽을 차단 UDR 구성. 
        - 나가는 패킷이 hello 백 엔드 풀 VM에서이 확인 되 면 hello VM toobe (eample hello 프로브 포트를 차단 하는 응용 프로그램)에 대 한 관련 되지 않은 모든 문제에 대해 확인 해야 합니다. 
    - Hello 프로브 패킷에 가능한 (UDR 설정)를 통해 강제 tooanother 대상 hello 부하 분산 장치에 도달 하기 전에 되는 경우를 확인 합니다. 이 인해 hello 트래픽 toonever reach hello 백엔드 VM 수 있습니다. 
* Hello 프로브 유형 (예: HTTP tooTCP) 바꾼 hello 문제는 프로브 응답의 hello 구성 하는 경우 네트워크 보안 그룹 Acl의에서 hello 해당 포트 및 방화벽 toovalidate를 구성 하십시오. 상태 프로브 구성에 대한 자세한 내용은 [끝점 부하 분산 장치 상태 프로브 구성](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/)을 참조하세요.

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>증상: 부하 분산 장치 뒤 Vm tootraffic hello 구성 데이터 포트에서 응답 하지 않습니다.

백 엔드 풀 VM 정상으로 나열 및 toohello 상태 프로브 응답 하지만 여전히 hello 부하 분산에 참여 하지 toohello 데이터 트래픽이 응답 하지 않습니다, 것 수 있습니다 due hello 이유 뒤의 tooany: 
* 부하 분산 장치 백 엔드 풀 VM hello 데이터 포트에서 수신 하지 않는 
* 네트워크 보안 그룹은 부하 분산 장치 백 엔드 풀 VM hello에 hello 포트를 차단 하는  
* NIC와 동일한 VM에서 부하 분산 장치 hello hello에 액세스 
* 부하 분산 장치 백 엔드 풀 VM 참여 하는 hello에서 hello 인터넷 부하 분산 장치 VIP에 액세스 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>원인 1: 부하 분산 장치 백 엔드 풀 VM hello 데이터 포트에서 수신 하지 않는 
VM toohello 데이터 트래픽이 응답 하지 않으면 hello 대상 포트에 열려 있지 않으면 VM에 참여 하는 hello 되었거나, 해당 포트에서 수신 대기 하지 않는 hello VM 수 있습니다. 

**유효성 검사 및 해결**

1. Toohello 백 엔드 VM에에서 로그인 합니다. 
2. 명령 프롬프트를 열고 다음 명령 toovalidate hello 데이터 포트에서 수신 대기 하는 응용 프로그램이 hello를 실행 합니다.  
            netstat -an 
3. Hello 포트 상태와 함께 나열 되지 않은 경우 "수신" hello 적절 한 수신기 포트를 구성 
4. Hello 포트 Listening으로 표시 되 면 모든 관련 문제에 대 한 해당 포트에서 hello 대상 응용 프로그램을 확인 합니다. 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>원인 2: 네트워크 보안 그룹에 부하 분산 장치 백 엔드 풀 VM hello hello 포트를 차단 하는  

하나 이상의 네트워크 보안 그룹 또는 hello VM hello 서브넷에 구성 된 경우 차단 hello 원본 IP 또는 포트를 hello VM이 없습니다 toorespond 합니다.

* Hello 백 엔드 VM에 구성 된 hello 네트워크 보안 그룹을 나열 합니다. 자세한 내용은 다음을 참조하세요.
    -  [Hello 포털을 사용 하 여 네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [PowerShell을 사용하여 네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* 네트워크 보안 그룹의 hello 목록에서 하는 경우를 확인 합니다.
    - hello 데이터 포트의 hello 들어오거나 나가는 트래픽을 방해를 있습니다. 
    - **모두 거부** 네트워크 보안 그룹 규칙에 hello 캡슐화 된 트래픽과 부하 분산 장치 프로브를 허용 하는 hello 기본 규칙 더 높은 우선 순위의 hello VM 또는 hello 서브넷의 NIC (네트워크 보안 그룹 허용 해야의 부하 분산 장치 IP 프로브 포트를 168.63.129.16) 
* Hello 트래픽을 차단 hello 규칙 중 하나를 제거 하 고 해당 규칙 tooallow hello 데이터 트래픽을 다시 구성.  
* Hello VM toorespond toohello 상태 검색이 시작를 테스트 합니다.

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>원인 3: hello에서 부하 분산 장치를 hello 액세스 같은 VM 및 네트워크 인터페이스 

Hello 백 엔드 부하 분산의 VM에서에서 호스팅되는 응용 프로그램 tooaccess 다른 응용 프로그램에서 호스트 하는 hello hello 통해 동일한 백 엔드 VM 동일한 네트워크 인터페이스를 지원 되지 않는 시나리오 되 고 실패 합니다. 

**해결 방법** hello 메서드를 다음 중 하나를 통해이 문제를 해결할 수 있습니다.
* 응용 프로그램마다 별도 백 엔드 풀 VM을 구성합니다. 
* 각 응용 프로그램에서 자체 네트워크 인터페이스 및 IP 주소를 사용 하므로 이중 NIC Vm에서 hello 응용 프로그램을 구성 합니다. 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>부하 분산 장치 백 엔드 풀 VM 참여 하는 hello에서 hello 내부 부하 분산 장치 VIP에 액세스 하는 원인 4:

ILB VIP는 VNet 내의 구성 되어 있고 hello 참가자 백 엔드 Vm 중 하나를 시도 하는 경우 tooaccess 오류가 발생 하는 내부 부하 분산 장치 VIP hello 합니다. 이것은 지원되지 않는 시나리오입니다.
**해상도** 평가 응용 프로그램 게이트웨이 또는 다른 프록시 (예를 들어 nginx 또는 haproxy와) toosupport 시나리오의 종류입니다. Application Gateway에 대한 자세한 내용은 [Application Gateway에 대한 개요](../application-gateway/application-gateway-introduction.md)를 참조하세요.

## <a name="additional-network-captures"></a>추가 네트워크 캡처
Tooopen 지원 케이스를 결정 한 경우에 hello 다음 빠른 해결에 대 한 정보를 수집 합니다. 테스트를 수행 하는 단일 백엔드 VM tooperform hello를 선택 합니다.
- Psping hello 백 엔드 hello VNet tootest hello 프로브 포트 응답 내에서 Vm 중 하나를 사용 하 여 (예: psping 10.0.0.4:3389) 결과 기록 합니다. 
- TCPing hello 백 엔드 hello VNet tootest hello 프로브 포트 응답 내에서 Vm 중 하나를 사용 하 여 (예: psping 10.0.0.4:3389) 결과 기록 합니다.
- 이러한 ping 테스트에 수신 된 응답이 없는 hello 백 엔드 VM에서 동시 Netsh 추적을 실행 및 VNet 테스트 VM을 실행 하는 PsPing 다음 hello Netsh 추적을 중지 하는 동안 hello 합니다. 
  
## <a name="next-steps"></a>다음 단계

Hello 앞의 단계 문제가 해결 되지 않으면 hello를 열고는 [지원 티켓](https://azure.microsoft.com/support/options/)합니다.

