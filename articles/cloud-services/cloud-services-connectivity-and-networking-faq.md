---
title: "Microsoft Azure 클라우드 서비스 FAQ에 대 한 aaaConnectivity 및 네트워킹 문제 | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure 클라우드 서비스에 대 한 네트워킹 및 연결에 대 한 질문과 대답 hello를 나열 합니다."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure Cloud Services의 연결 및 네트워킹 문제: FAQ(질문과 대답)

이 문서는 [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services)의 연결 및 네트워킹에 대한 질문과 대답을 포함합니다. Hello를 참조할 수 있습니다 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 크기 정보에 대 한 합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>여러 VIP 클라우드 서비스에서 IP를 예약할 수 없습니다.
먼저, tooreserve hello IP를 만들려고 하는 hello 가상 컴퓨터 인스턴스의 켜져 있는지 확인 합니다. 둘째, 스테이징 및 프로덕션 배포를 hello 둘 다에 대해 예약 된 Ip를 사용 하는 확인 합니다. **없는** hello 배포를 업그레이드 하는 동안 hello 설정을 변경 합니다.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>NSG가 있을 때 원격 데스크톱을 어떻게 수행하나요?
포트에서 트래픽을 허용 하는 NSG 규칙 toohello 추가 **3389** 및 **20000**합니다.  원격 데스크톱은 포트 **3389**를 사용합니다.  클라우드 서비스 인스턴스 부하 분산이 되므로 어떤 인스턴스 tooconnect을 직접 제어할 수 없습니다.  hello *RemoteForwarder* 및 *RemoteAccess* 에이전트 RDP 트래픽을 관리 하 고 hello 클라이언트 toosend RDP 쿠키를 허용 및는 개별 인스턴스 tooconnect를 지정 합니다.  hello *RemoteForwarder* 및 *RemoteAccess* 에이전트에 해당 포트 필요 **20000** 열 수 있는 NSG 있는 경우 차단 될 수 있습니다.

## <a name="can-i-ping-a-cloud-service"></a>클라우드 서비스를 ping할 수 있나요?

Hello normal "ping"를 사용 하 여 아니요 / ICMP 프로토콜입니다. hello ICMP 프로토콜 hello Azure 부하 분산 장치를 통해 허용 되지 않습니다.

tootest 연결 포트에 ping을 수행 하는 것이 좋습니다. Ping.exe가 ICMP를 사용 하는 동안 PSPing, Nmap, 및 텔넷 같은 다른 도구를 사용 하면 tootest 연결 tooa 특정 TCP 포트 있습니다.

자세한 내용은 참조 [ICMP tootest Azure VM에 연결 하는 대신 포트 ping을 사용 하 여](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/)합니다.

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>수신 방지 하려면 어떻게 수천 일종의 악의적인 공격이 toohello 나타내는 알 수 없는 IP 주소에서 적중 횟수의 클라우드 서비스?
Azure는 플랫폼 서비스 분산 된 서비스 거부 (DDoS) 공격에 대 한 다중 계층 네트워크 보안 tooprotect를 구현합니다. hello Azure DDoS 방어 시스템에는 Azure의 연속 모니터링 하는 프로세스가 침투 테스트를 통해 지속적으로 개선의 일부입니다. 이 DDoS 철저 한 방어 시스템은 설계 toowithstand hello 외부에서 하지만 다른 Azure 테 넌 트에서 뿐만 아니라 공격입니다. 자세한 내용은 [Microsoft Azure 네트워크 보안](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf)을 참조하세요.

또한 일부 특정 IP 주소는 시작 작업 tooselectively 블록을 만들 수 있습니다. 자세한 내용은 [특정 IP 주소 차단](cloud-services-startup-tasks-common.md#block-a-specific-ip-address)을 참조하세요.

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Hello 메시지를 할 때 tooRDP toomy 클라우드 서비스 인스턴스, "hello 사용자 계정이 만료 되었습니다."
RDP 설정에 구성 된 hello 만료 날짜를 바이패스 하면 "이 사용자 계정 만료 되었습니다." hello 오류 메시지가 발생할 수 있습니다. Hello 포털에서 다음이 단계를 수행 하 여 hello 만료 날짜를 변경할 수 있습니다.
1. Azure 관리 콘솔 (https://manage.windowsazure.com) toohello 로그인 tooyour 클라우드 서비스 이동한 hello 선택 **구성** 탭 합니다.
2. **원격**을 선택합니다.
3. 날짜 "만료에" hello를 변경 하 고 hello 구성을 저장 합니다.

이제 수 tooRDP tooyour 컴퓨터 있어야 합니다.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>LoadBalancer가 트래픽을 동일하게 분산하지 않는 이유는 무엇인가요?
내부 부하 분산 장치 작동 방법에 대한 정보는 [Azure Load Balancer 새 배포 모드](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/)를 참조하세요.

사용 되는 hello 배포 알고리즘은 5-튜플 (원본 IP, 원본 포트 대상 IP, 대상 포트 프로토콜 유형) toomap 트래픽 tooavailable 서버 해시 합니다. 전송 세션 내에서만 연결이 유지됩니다. 동일한 TCP 또는 UDP 세션이 hello 패킷에 toohello hello 부하 분산 된 끝점 뒤에 동일한 데이터 센터 IP (DIP) 인스턴스를 이동 합니다. 클라이언트 hello 및 hello 연결을 다시 엽니다. 닫거나 hello에서 새 세션을 시작 동일 원본 IP, hello 원본 포트 변경 하 고 hello 트래픽 toogo tooa 다른 DIP 끝점 발생 합니다.
