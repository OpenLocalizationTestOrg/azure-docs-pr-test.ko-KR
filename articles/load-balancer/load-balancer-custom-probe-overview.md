---
title: "aaaLoad 분산 장치에 대 한 사용자 지정 검색 및 모니터링 상태 | Microsoft Docs"
description: "사용자 지정 toouse 부하 분산 장치 뒤의 Azure 부하 분산 장치 toomonitor 인스턴스를 조사 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>부하 분산 장치 프로브 이해

Azure 부하 분산 장치 프로브를 사용 하 여 hello 기능 toomonitor hello 서버 인스턴스의 상태를 제공 합니다. Toorespond는 검색이 실패 하면 새 연결 toohello 비정상 인스턴스를 보내는 부하 분산 장치 중지 됩니다. hello 기존 연결에 영향을 받지 않습니다 및 새 연결 toohealthy 인스턴스에 전송 됩니다.

클라우드 서비스 역할(작업자 역할 및 웹 역할)은 프로브 모니터링에 게스트 에이전트를 사용합니다. 부하 분산 장치 뒤의 가상 컴퓨터를 사용하는 경우 TCP 또는 HTTP 사용자 지정 프로브를 구성해야 합니다.

## <a name="understand-probe-count-and-timeout"></a>프로브 수 및 시간 제한 이해

프로브 동작은 다음 사항에 따라 달라집니다.

* 작동 중으로 표시 하는 인스턴스 toobe 허용 하는 성공적으로 검색 작업의 hello 수입니다.
* 인스턴스 toobe 레이블이 해제 상태로 인해 실패 한 검색 작업의 hello 수입니다.

SuccessFailCount에 설정 된 hello 제한 시간 및 빈도 값 인스턴스 실행 또는 실행 중 아님 확인된 toobe 되는지 확인 합니다. Hello Azure 포털에서에서 hello 제한 시간 hello 주파수 tootwo 번 hello 값으로 설정 되어 있습니다.

모든 부하 분산 된 인스턴스의 hello 프로브 구성 해야 (즉,: 부하 분산 된 집합) 끝점에 대 한 hello 동일 합니다. 즉, 다른 프로브 구성을 사용할 수 없는 각 역할 인스턴스 또는 가상 컴퓨터에 hello에 대 한 특정 끝점 조합에 대 한 서비스 호스트 동일 합니다. 예를 들어 각 인스턴스의 로컬 포트 및 시간 제한이 동일해야 합니다.

> [!IMPORTANT]
> 부하 분산 장치 프로브 hello IP 주소 168.63.129.16을 사용합니다. 이 공용 IP 주소는 hello bring your-소유-IP Azure 가상 네트워크 시나리오에 대 한 통신 toointernal 플랫폼 리소스를 지원합니다. hello 가상 공용 IP 주소 168.63.129.16은 모든 지역에 사용 하 고 변경 되지 않습니다. 모든 로컬 방화벽 정책에서 이 IP 주소를 허용하는 것이 좋습니다. 그 간주 되지 않아야 보안 위험 hello 내부 Azure 플랫폼만 해당 주소에서 메시지를 원본 수 있습니다. 다양 한 시나리오를 구성할 때 예기치 않은 동작이 됩니다 이렇게 하지 않으면 hello 168.63.129.16와 IP 주소를 중복 된 것의 동일한 IP 주소 범위입니다.

## <a name="learn-about-hello-types-of-probes"></a>프로브 유형의 hello에 대 한 자세한 내용은

### <a name="guest-agent-probe"></a>게스트 에이전트 프로브

이 프로브는 Azure 클라우드 서비스에만 제공됩니다. 부하 분산 장치는 hello 가상 컴퓨터 내의 게스트 에이전트 hello 사용 하 여 수신 대기 하 고 인스턴스는 hello 준비 상태에는 HTTP 200 정상 응답 경우에 hello를 사용 하 여 응답 (즉, 다른에 없는 상태로 사용 중, 중지 또는 재활용 등).

자세한 내용은 참조 [상태 프로브에 대해 구성 hello 서비스 정의 파일 (csdef)](https://msdn.microsoft.com/library/azure/ee758710.aspx) 또는 [클라우드 서비스에 대 한 인터넷 연결 부하 분산 장치를 만들기 전에](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services)합니다.

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>게스트 에이전트 프로브에서 인스턴스를 비정상으로 표시하는 경우

Hello 게스트 에이전트가 HTTP 200 정상 toorespond 실패 hello 부하 분산 장치 표시 hello 인스턴스를 응답 없음으로 / 중지 toothat 인스턴스에 트래픽을 전송 합니다. 부하 분산 장치 hello tooping hello 인스턴스를 계속합니다. Hello 게스트 에이전트가 HTTP 200에 응답, hello 부하 분산 장치에서 트래픽을 toothat 인스턴스를 다시 보냅니다.

웹 역할을 사용 하는 경우 hello 웹 사이트 코드는 일반적으로 hello Azure 패브릭 또는 게스트 에이전트에서 모니터링 하지 않는 w3wp.exe에서 실행 됩니다. 즉, w3wp.exe (예를 들어 HTTP 500 응답)에서 오류를 보고 toohello 게스트 에이전트 됩니다. hello 부하 분산 장치는 해당 인스턴스가 회전 하지 수행 되지 것입니다.

### <a name="http-custom-probe"></a>HTTP 사용자 지정 프로브

사용자 지정 HTTP 부하 분산 장치 프로브 hello 사용자 고유의 사용자 지정 논리 toodetermine hello hello 역할 인스턴스의 상태를 만들 수 있다는 의미는 hello 기본 게스트 에이전트 검색을 재정의 합니다. hello 부하 분산 장치 프로브를 끝점 15 초 간격으로 기본적으로 합니다. hello 인스턴스 hello 제한 시간 (기본적으로 31 초) 내에서 HTTP 200에 응답 하는 경우 hello 부하 분산 장치 순환에서 toobe를 간주 됩니다.

Tooimplement 부하 분산 장치 순환 순서에서 사용자 고유의 논리 tooremove 인스턴스를 원하는 경우에 유용할 수 있습니다. 예를 들어 90%의 CPU 위에 되 고 200 이외의 상태를 반환 경우 tooremove 인스턴스를 결정할 수 있습니다. 웹 역할이 w3wp.exe를 사용 하는 경우 즉, 자동 얻게 코드를 웹 사이트에서 오류를 반환 하므로 200 이외의 상태 toohello 부하 분산 장치 검색의 웹 사이트를 모니터링 합니다.

> [!NOTE]
> hello HTTP 사용자 지정 프로브 상대 경로 및 HTTP 프로토콜만 지원합니다. HTTPS는 지원되지 않습니다.

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>HTTP 사용자 지정 프로브에서 인스턴스를 비정상으로 표시하는 경우

* hello HTTP 응용 프로그램 (예를 들어 403, 404, 또는 500) 200 이외의 HTTP 응답 코드를 반환합니다. 이 응용 프로그램 hello 긍정 승인을 서비스에서 즉시 인스턴스를 제거 해야 합니다.
* hello HTTP 서버 hello 제한 시간 후에 응답 하지 않습니다. 설정 된 hello 제한 시간 값에 따라 즉 해당 여러 프로브 요청으로 실행 되 고 있지 hello 프로브 가져옵니다 표시 되기 전에 응답이 go (즉, SuccessFailCount 하기 전에 프로브 전송) 합니다.
* hello 서버 TCP 재설정을 통해 hello 연결을 닫습니다.

### <a name="tcp-custom-probe"></a>TCP 사용자 지정 프로브

TCP 프로브 hello 정의 된 포트와 3 방향 핸드셰이크를 수행 하 여 연결을 시작 합니다.

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>TCP 사용자 지정 프로브에서 인스턴스를 비정상으로 표시하는 경우

* hello TCP 서버 hello 제한 시간 후에 응답 하지 않습니다. 실행 되 고 있지에 따라 달라 지므로 실패 한 프로브 hello 수가 hello 프로브 표시 되 면 실행 되 고 있지으로 hello 프로브 표시 하기 전에 응답이 구성 된 toogo 상태로 있었던 요청 합니다.
* hello 프로브 재설정 hello 역할 인스턴스에서 TCP를 받습니다.

HTTP 상태 프로브 또는 TCP 프로브 구성에 대한 자세한 내용은 [PowerShell을 사용하여 리소스 관리자에서 인터넷 연결 부하 분산 장치 만들기 시작](load-balancer-get-started-internet-arm-ps.md)을 참조하세요.

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>부하 분산 장치 회전에 다시 정상 인스턴스 추가

TCP 및 HTTP 프로브 정상인 상태로 간주 하 고 hello 역할 인스턴스의 경우에 비정상으로 표시 합니다.

* hello 부하 분산 장치는 양의 프로브 hello 첫 번째 시간 hello를 VM 부팅을 가져옵니다.
* hello 숫자 (앞에서 설명한) SuccessFailCount 정상으로 필요한 toomark hello 역할 인스턴스는 성공적으로 검색 작업의 hello 값을 정의 합니다. 역할 인스턴스를 제거 하는 경우, 연속 프로브 hello 수 동일 하거나 SuccessFailCount toomark hello 역할 인스턴스의 실행 중으로 hello 값을 초과 해야 합니다.

> [!NOTE]
> Hello는 역할 인스턴스 상태는 변동이, 경우 hello 부하 분산 장치 정상 상태로 hello에 다시 hello 역할 인스턴스를 넣기 전에 더 이상 대기 합니다. 이 정책 tooprotect hello 사용자 및 hello 인프라를 통해 수행 됩니다.

## <a name="use-log-analytics-for-load-balancer"></a>부하 분산 장치에 대한 로그 분석

사용할 수 있습니다 [부하 분산 장치에 대 한 로그 분석](load-balancer-monitor-log.md) toocheck hello 프로브 상태 프로브와 상태 수에 있습니다. 로깅 부하 분산 장치 상태에 대 한 Power BI 또는 Azure Operational Insights tooprovide 통계로 사용할 수 있습니다.
