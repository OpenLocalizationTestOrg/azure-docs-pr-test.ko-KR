---
title: "Azure 서비스 버스에서 AMQP 1.0의 aaaOverview | Microsoft Docs"
description: "사용에 대 한 자세한 내용은 고급 메시지 큐 (AMQP Protocol) 1.0 Azure의 hello 합니다."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>서비스 버스의 AMQP 1.0 지원
Azure 서비스 버스 클라우드 서비스와 온-프레미스 둘 다 hello [Service Bus for Windows Server (서비스 버스 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) 지원 hello 메시지 큐 프로토콜 AMQP (Advanced) 1.0입니다. AMQP 있습니다 toobuild 플랫폼 간 개방형 표준 프로토콜을 사용 하 여 하이브리드 응용 프로그램을 수 있습니다. 다른 언어 및 프레임워크로 빌드된 구성 요소를 사용하며 다른 운영 체제에서 실행되는 응용 프로그램을 생성할 수 있습니다. 이러한 모든 구성이 요소는 tooService 버스를 연결 하 고 원활 하 게 효율적이 고를 완전 하 게 구조적인된 비즈니스 메시지를 교환할 수 있습니다.

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>소개: AMQP 1.0이란 무엇이며 왜 중요한가요?
일반적으로 메시지 지향 미들웨어 제품은 클라이언트 응용 프로그램과 브로커 간에 통신하는 데 소유 프로토콜을 사용했습니다. 이 특정 공급 업체의 메시징 브로커를 선택한 후 사용 해야 하는 공급 업체의 라이브러리 tooconnect 프로그램 클라이언트 응용 프로그램 toothat 브로커 것을 의미 합니다. 이 인해 해당 공급 업체에 대 한 종속성 수준의 모든 hello 연결 된 응용 프로그램에서 코드를 변경 해야 응용 프로그램 tooa 다른 제품 이식 때문입니다. 

더구나 다른 공급업체의 메시징 브로커를 연결하는 것은 까다로우며, 일반적으로 응용 프로그램 수준 브리징 toomove 시스템 tooanother 및 메시지의 소유 메시지 형식 간의 tootranslate 지정 해야 합니다. 이 작업은 일반적인 필요 합니다. 예를 들어 해야 새 통합된 인터페이스 tooolder를 서로 다른 시스템 제공 하거나 때 합병 다음 IT 시스템을 통합 합니다.

hello 소프트웨어 업계는 빠르게 변화 비즈니스; 새 프로그래밍 언어 및 응용 프로그램 프레임 워크는 경우에 따라 이러한 능력에 따라 제공 됩니다. 마찬가지로, IT 시스템의 요구 사항을 hello 발전 하 고 있으며 개발자가 원하는 tootake hello 최신 플랫폼 기능 활용 합니다. 그러나 때로는 hello 선택한 메시징 공급 업체 지원 하지 않습니다 이러한 플랫폼. 다른 사용자에 대 한 수 없으면 메시징 프로토콜은 전용 이기 때문에 이러한 새 플랫폼에 대 한 tooprovide 라이브러리입니다. 따라서 게이트웨이 또는 수 있도록 브리지 toocontinue toouse hello 메시징 제품을 만드는 등의 접근 방식을 사용 해야 합니다.

hello 개발의 hello 고급 메시지 큐 (AMQP Protocol) 1.0이 문제의 동기 부여 되었습니다. 대부분의 금융 서비스 기업처럼 메시지 지향 미들웨어를 많이 사용하는 JP Morgan Chase에서 시작되었습니다. hello 목표는 간단한 형태 였습니다: toocreate 가능한 toobuild에 메시지 기반 응용 프로그램을 다른 언어, 프레임 워크 및 운영 체제를 사용 하 여 구축 된 구성 요소를 사용 하 여 수행 하는 개방형 표준 메시징 프로토콜 모두에서 최고의의 구성 요소를 사용 하는 공급 업체의 범위입니다.

## <a name="amqp-10-technical-features"></a>AMQP 1.0의 기술적 기능
AMQP 1.0은는 효율적이 고 신뢰할 수 있는 유선 수준 메시징 프로토콜 사용할 수 있는 toobuild 강력한 플랫폼 간 메시징 응용 프로그램입니다. hello 프로토콜의 목적은: hello 안정적이 고 효율적인 안전한 메시지 전송 두 파티 간의 toodefine hello 메커니즘입니다. hello 메시지 자체를 다른 유형의 발신자와 수신자 구조화 tooexchange 비즈니스 메시지 하를 완전 하 게 이식 가능 데이터 표현을 사용 하 여 인코딩됩니다. hello 다음은 hello 가장 중요 한 기능에 대 한 요약입니다.

* **효율적인**: AMQP 1.0은 연결 지향 프로토콜 이진 hello에 대 한 인코딩을 사용 하 여 프로토콜 지침 및 비즈니스 메시지를 통해 전송 되 hello 합니다. 정교한 흐름 제어 구성표가 toomaximize hello 활용 hello 네트워크와 연결 된 hello 구성 요소를 통합합니다. 즉, hello 프로토콜 디자인 된 toostrike 효율성, 유연성 및 상호 운용성 간의 균형을 했습니다.
* **신뢰할 수 있는**: hello AMQP 1.0 프로토콜 메시지 toobe 안정성 보장 및 잊어 화재 tooreliable에서의 범위와 정확 하 게 교환 허용-한 번만 승인 해 서 배달 합니다.
* **유연한**: AMQP 1.0은 여러 토폴로지를 사용 하는 toosupport 일 수 있는 유연한 프로토콜입니다. hello 같은 프로토콜에 사용할 수-클라이언트, 클라이언트-브로커 및를 broker 통신 합니다.
* **브로커 모델 독립성**: hello AMQP 1.0 사양 hello는 브로커에서 사용 되는 메시징 모델에 대 한 요구를 만들지 않습니다. 이 수 있다는 것을 의미 tooeasily 메시징 브로커 AMQP 1.0 지원 tooexisting를 추가 합니다.

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>AMQP 1.0 표준
AMQP 1.0은 ISO 및 IEC에 의해 ISO/IEC 19464:2014로 승인된 국제 표준합니다.

AMQP 1.0은 2008년 이래로 기술 공급업체와 최종 사용자 업체를 모두 포함하여 20여 개가 넘는 핵심 회사에 의해 개발되었습니다. 이 시간 동안 사용자 업체 실제 비즈니스 요구 사항을 적용 하 고 hello 기술 공급 업체 hello 프로토콜 toomeet 이러한 요구 사항을 발전 했습니다. Hello 과정 전반에 걸쳐 공급 업체는은 협력을 통해 구현 간의 toovalidate hello 상호 운용성 워크샵에 참여 합니다.

2011 년 10 월에에서 hello 개발 작업 tooa hello 조직 hello Advancement의 구조화 된 정보 표준 OASIS ()에 대 한 기술 위원회 전환 및 2012 년 10 월에에서 OASIS AMQP 1.0 표준이 hello 릴리스 되었습니다. hello 다음과 같은 업체가에 참여 한 hello 기술 위원회 hello 표준 hello 개발 하는 동안:

* **기술 공급업체**: Axway Software, Huawei Technologies, IIT Software, INETCO Systems, Kaazing, Microsoft, Mitre Corporation, Primeton Technologies, Progress Software, Red Hat, SITA, Software AG, Solace Systems, VMware, WSO2, Zenika.
* **사용자 업체**: Bank of America, Credit Suisse, Deutsche Boerse, Goldman Sachs, JPMorgan Chase.

Hello의 일반적으로 인용 개방형 표준의 이점은 같습니다.

* 공급업체 교착 상태 확률이 낮아짐
* 상호 운용성
* 다양한 라이브러리 및 도구 제공
* 구식화 방지
* 숙련된 직원에 대한 가용성
* 위험성 저하 및 관리 가능한 위험

## <a name="amqp-10-and-service-bus"></a>AMQP 1.0 및 서비스 버스
Azure 서비스 버스에서 AMQP 1.0 지원 이제 hello 서비스 버스 큐를 활용 하 고 수 있는 게시/구독 조정 된 메시징 기능 효율적인 이진 프로토콜을 사용 하 여 플랫폼의 범위에서을 의미 합니다. 뿐만 아니라 여러 언어, 프레임워크 및 운영 체제가 혼합되어 사용된 구성 요소로 이루어진 응용 프로그램을 만들 수 있습니다.

hello 다음 그림에 나와 있는 hello 표준 서비스 JMS (Java Message) API를 사용 하 여 작성 되었으며 Linux에서 실행 되는 Java 클라이언트와 Windows에서 AMQP 1.0을 사용 하 여 서비스 버스를 통해 메시지를 교환 하에서 실행 중인.NET 클라이언트에 배포 하는 예입니다.

![][0]

**그림 1: Service Bus와 AMQP 1.0을 사용하는 플랫폼 간 메시징을 보여 주는 예제 배포 시나리오**

이 시간 hello에서 클라이언트 라이브러리 toowork 서비스 버스에 알려진 있습니다.

| 언어 | 라이브러리 |
| --- | --- |
| Java |Apache Qpid JMS(Java Message Service) 클라이언트<br/>IIT Software SwiftMQ Java 클라이언트 |
| C |Apache Qpid Proton-C |
| PHP |Apache Qpid Proton-PHP |
| Python |Apache Qpid Proton-Python |
| C# |AMQP .Net Lite |

**그림 2: AMQP 1.0 클라이언트 라이브러리 테이블**

## <a name="summary"></a>요약
* AMQP 1.0 toobuild 플랫폼 간 하이브리드 응용 프로그램을 사용할 수 있는 개방형이 고 신뢰할 수 있는 메시징 프로토콜입니다. AMQP 1.0은 OASIS 표준입니다.
* 이제 Azure 서비스 버스와 Windows Server용 서비스 버스(서비스 버스 1.1)에서 모두 AMQP 1.0이 지원됩니다. 가격 책정은 hello 프로토콜 기존 hello와 같습니다.

## <a name="next-steps"></a>다음 단계
더 많은 toolearn 준비? Hello 다음 링크를 방문.

* [AMQP를 사용하여 .NET에서 Service Bus 사용]
* [AMQP를 사용하여 Java에서 Service Bus 사용]
* [Azure Linux VM에 Apache Qpid Proton-C 설치]
* [Windows Server용 Service Bus의 AMQP]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[AMQP를 사용하여 .NET에서 Service Bus 사용]: service-bus-amqp-dotnet.md
[AMQP를 사용하여 Java에서 Service Bus 사용]: service-bus-amqp-java.md
[Azure Linux VM에 Apache Qpid Proton-C 설치]: service-bus-amqp-apache.md
[Windows Server용 Service Bus의 AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
