---
title: "프로그램 사물 인터넷에서 hello 접지 aaaSecuring | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure IoT Suite hello의 hello 기본 제공 보안 기능 설명"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 10252dfa-8313-4a97-9bd6-a3f1345dd3be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: a97e8cea753641e1e3c895f44e3fde1e5739d665
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-from-hello-ground-up"></a>Hello 접지에서 사물 인터넷 보안
인터넷의 IoT (사물) hello 헤드로 고유한 보안, 개인 정보 보호 및 규정 준수 문제 toobusinesses 전 세계 수 있습니다. 여기서 이러한 문제를 중심으로 소프트웨어 및 구현 하는 전통적인 사이버 기술, 달리 IoT hello 사이버 및 hello 실제 세계 수렴 하는 경우와 관련 됩니다. IoT 솔루션 보호 장치, 이러한 장치 및 hello 클라우드 및 처리 및 저장 시 hello 클라우드에서 데이터의 보안 보호 간의 보안 연결의 보안 프로 비전 되었는지 확인 해야 합니다. 그러나 이러한 기능에 대한 작업에는 리소스가 제한된 장치, 배포의 지리적 분산 및 솔루션 내 많은 수의 장치에 대한 작업이 포함됩니다.

이 문서는 Microsoft Azure IoT Suite hello 보안 및 개인 사물 인터넷 클라우드 솔루션을 제공 하는 방법을 탐색 합니다. hello Azure IoT Suite 접지 hello에서 모든 단계에 기본 제공 되는 보안이 포함 된 완벽 한 종단 간 솔루션을 제공 합니다. Microsoft는 보안 소프트웨어 개발의 일부인 hello 소프트웨어 엔지니어링 연습, 온 수십 년간에 보안 소프트웨어 개발의 긴 환경입니다. tooensure이 주기 SDL (Security Development)는 작업 보안을 보증 (OSA) 및 Microsoft Digital Crimes Unit hello와 같은 인프라 수준의 보안 서비스 호스트를 함께 사용 되는 hello 기본 개발 방법론 Microsoft 보안 대응 센터 및 Microsoft 맬웨어 보호 센터를 제공 합니다. 

hello Azure IoT Suite 제공 고유 기능을 프로 비전에 연결 하 고 간편 하 고 투명 IoT 장치에서 데이터를 저장 하 고, 최대 보안. 이 문서에서는 hello Azure IoT Suite 보안 기능을 살펴볼 및 배포 전략 tooensure 보안, 개인 정보 보호 및 규정 준수 문제를 해결할 수 있습니다. 

## <a name="introduction"></a>소개
hello 인터넷 IoT (사물)는 기업 즉시 제공 이후 hello hello 유입 및 실제 기회 tooreduce 비용 수익를 개선 하 고 비즈니스를 변환 합니다. 많은 기업 사항은 망설 toodeploy IoT 자신의 조직에서 보안, 개인 정보 보호 및 규정 준수에 대 한 due tooconcerns 합니다. 문제의 주요 지점 hello 사이버 및 실제 세계가 두 환경을에 내재 된 개별 위험 그래야만 함께 병합 하는 hello IoT 인프라의 hello 고유성에서 제공 됩니다. 보안을 IoT 장치에서 실행 되, 장치 및 사용자 인증을 제공 하 고 장치 (으로 해당 장치에서 생성 된 데이터)를 지우기 소유권을 정의 및 되 고 코드 tooensuring hello 무결성 관련 된 복원 력 있는 toocyber 및 물리적 공격입니다. 

그런 다음 개인 정보 보호의 hello 문제가 됩니다. 회사는 데이터 수집과 관련하여 투명성을 원합니다. 즉, 어떤 데이터가 왜 수집되며 누가 볼 수 있고 누가 액세스를 제어할 수 있는지 투명하게 알고 싶어합니다. 마지막으로, 운영 hello 사람 함께 hello 장비 일반적인 보안 문제 및 문제 업계 표준의 규정 준수를 유지 관리 하는 합니다.

Hello 보안, 개인 정보, 투명도 및 규정 준수 문제 들어 hello 오른쪽 IoT 솔루션 공급자 선택 challenge 상태로 유지 됩니다. IoT 소프트웨어 및 다양 한 공급 업체에서 제공 하는 서비스의 개별 조각을 함께 연결할 보안, 개인 정보, 투명도 및 해결 감당할 하드 toodetect 될 수 있는 규정 준수의 간격을 소개 합니다. 소프트웨어 및 서비스 공급자 찾기 직종 및 지리적 위치에 걸쳐 하면서 수 tooscale 안전 하 고 투명 한 방식으로는 서비스를 실행 하는 광범위 한 경험을 포함 하는 공급자 기반 IoT hello 권한의 hello 선택입니다. 마찬가지로, 컴퓨터를 전 세계 수많은에서 실행 되는 보안 소프트웨어 개발 경험이 수십 공급자 toohave 선택한 hello에 대 한 도움이 될 수 하 고 있는 hello 인터넷의 새로운 세계에 의해 제기 되 hello 기능 tooappreciate hello 위협 상황의 작업입니다.

## <a name="secure-infrastructure-from-hello-ground-up"></a>Hello 접지에서 안전한 인프라
hello [Microsoft 클라우드](https://www.microsoft.com/enterprise/microsoftcloud/default.aspx#fbid=WzBsRQi6aGk) 인프라 127 국가에서 십억을 하나 이상 고객을 지원 합니다. 엔터프라이즈 소프트웨어를 빌드하고 일부 hello 가장 큰 온라인에서 서비스가 실행 되는 hello world 년간 장기 경험을 그릴 제공 더 높은 수준의 강화 된 보안, 개인 정보, 준수 및 위협 완화 사례 보다 대부분의 고객 자체적으로 달성 합니다.

우리의 [수명 주기 SDL (Security Development)](https://www.microsoft.com/sdl/) hello 전체 소프트웨어 과정에 보안 요구 사항을 포함 하는 필수 회사 전체 개발 프로세스를 제공 합니다. toohelp 운영 활동 hello 따르는지 확인 같은 수준의 보안 사례, 작동 보안 보증 (OSA) 진행 중에 배치 하는 엄격한 보안 지침 사용 합니다. 또한 지속적인 확인 우리의 준수 의무 충족 하는지와 Microsoft 보안 Digital Crimes Unit Microsoft hello를 포함 하 여 어떻게 센터 hello 생성을 통해 광범위 한 보안 노력에 참여 하는 것에 대 한 공급 업체 감사 기업 협력 응답 Center 및 Microsoft 맬웨어 보호 센터입니다.

## <a name="microsoft-azure---secure-iot-infrastructure-for-your-business"></a>Microsoft Azure - 비즈니스를 위한 보안 IoT 인프라
Microsoft Azure는 지속적으로 통합 된 클라우드 서비스의 컬렉션을 결합 하는 완전 한 클라우드 솔루션 제공-분석, 기계 학습, 저장소, 보안, 네트워킹 및 웹-업계를 주도하 약정 toohello 보호 및 데이터의 개인 정보 보호 합니다. 우리의 [위반 가정](https://azure.microsoft.com/blog/red-teaming-using-cutting-edge-threat-simulation-to-harden-the-microsoft-enterprise-cloud/) 전략 사용 전용된 "빨간색 팀" toodetect Azure의 hello 기능 테스트 공격을 시뮬레이션, 새로운 위협 으로부터 보호 및 침해에서 복구 하는 소프트웨어 보안 전문가 들입니다. 우리의 [글로벌 사고 대응](https://www.microsoft.com/TrustCenter/Security/DesignOpSecurity) hello 해결 팀 작업 클록 공격 및 악의적인 활동의 toomitigate hello 효과입니다. hello 팀 인시던트 관리, 통신 및 복구에 대해 설정 된 프로시저를 검색 가능 하 고 예측 가능한 인터페이스를 사용 하 여 내부 및 외부 파트너와 합니다.

시스템은 지속적인 침입 탐지 및 방지, 서비스 거부 공격 방지, 일반적인 침투 테스트, 외부 도구를 통해 위협을 식별하고 완화할 수 있습니다. [Multi-factor authentication](../multi-factor-authentication/multi-factor-authentication.md) 최종 사용자에 게 tooaccess hello 네트워크에 대 한 추가 보안 계층을 제공 합니다. 및 액세스 제어, 모니터링, 맬웨어 방지, 취약점 검색, 패치 및 구성 관리 제공 hello 응용 프로그램 및 hello 호스트 공급자에 대 한 합니다.

Microsoft Azure IoT Suite hello hello 보안 활용 및 보안 개발 및 모든 Microsoft 소프트웨어의 작동을 위해 OSA 및 SDL 프로세스와 함께 Azure 플랫폼 hello에 내장 된 개인 정보 보호 합니다. 이러한 절차는 인프라 보호, 네트워크 보호 및 모든 솔루션 id 및 관리 기능 기본 toohello 보안을 제공합니다. 

hello [Azure IoT Hub](../iot-hub/iot-hub-what-is-iot-hub.md) hello 내 [IoT Suite](iot-suite-what-is-azure-iot.md) IoT 장치와 과같은Azure서비스간의안정적이고안전한양방향통신하는완전히관리되는서비스를제공[Azure 기계 학습](../machine-learning/machine-learning-what-is-machine-learning.md) 및 [Azure 스트림 분석](../stream-analytics/stream-analytics-introduction.md) -장치 보안 자격 증명 및 액세스 제어를 사용 하 여 합니다.

toobest hello Azure IoT Suite에 기본 제공 되는 보안 및 개인 정보 보호 기능을 통신, 우리 hello 세 가지 기본 보안 영역에 hello 테스트 도구 모음을 세분화 했습니다. 

![Azure IoT Suite](media/securing-iot-ground-up/securing-iot-ground-up-fig3.png)

### <a name="secure-device-provisioning-and-authentication"></a>보안 장치를 프로비전 및 인증
Azure IoT Suite hello 중일 때 아웃 hello 필드에 작업 중인 동안 hello IoT 인프라 toocommunicate hello 장치에는 사용할 수 있는 각 장치에 대 한 고유한 id 키를 제공 하 여 장치를 보호 합니다. hello 프로세스를 신속 하 고 쉽게 tooset를 합니다. hello는 hello Azure IoT Hub와 hello 장치 간의 모든 통신에 사용 되는 토큰의 사용자가 선택한 장치 ID forms hello 단위로 사용 하 여 키를 생성 합니다.

장치 ID는 제조 중에 장치에 연결하거나(예: 하드웨어 트러스트 모듈에서 플래시됨) 기존 고정된 ID를 프록시로 사용할 수 있습니다(예: CPU 일련 번호). Hello 장치에서이 식별 정보를 변경, 단순 아니므로 hello 기본 장치 하드웨어 변경 되지만 hello 논리적 장치는 hello 동일한 경우 중요 한 toointroduce 논리 장치 Id입니다. 경우에 따라 장치 id의 hello 연결 (즉, 인증 된 필드 엔지니어 물리적으로 구성 새 장치 hello 솔루션 백 엔드와 통신 하는 동안) 장치 배포 시 발생할 수 있습니다. hello [Azure IoT Hub id 레지스트리에](../iot-hub/iot-hub-devguide.md) 장치 id 및 솔루션에 대 한 보안 키의 안전한 저장소를 제공 합니다. 장치 id의 그룹이 나 개인을 추가할 수 있습니다 tooan 허용 목록 또는 차단 목록, 완벽 하 게 장치 액세스 제어를 사용 하도록 설정 합니다.

Hello 클라우드에서 azure IoT Hub 액세스 제어 정책을 활성화 및 방식으로 toodisassociate 필요할 때 프로그램 IoT 배포에서 장치를 제공 하는 장치 id를 사용 하지 않도록 설정 사용 하도록 설정 합니다. 장치의 연결 및 분리는 각 장치 ID를 기반으로 합니다.

Hello 다음 포함 하는 추가 장치 보안 기능:

* 장치는 요청하지 않은 네트워크 연결을 허용하지 않습니다. 아웃바운드 전용 방식으로 모든 연결 및 경로를 설정합니다. Hello 장치는 장치 tooreceive hello 백 엔드에서 명령에 대 한 모든 보류 중인 명령 tooprocess에 대 한 연결 toocheck을 시작 해야 합니다. IoT Hub hello 장치 사이 연결이 안전 하 게 설정 되 면 hello 클라우드 toohello 장치 및 장치 toohello에서 메시징 클라우드 보낼 수 투명 하 게 합니다.  
* 장치에만 tooor 연결 된 이러한 피어로 설정 되어, Azure IoT Hub와 같은 경로 toowell 알려진 서비스를 설정 합니다.
* 시스템 수준 권한 부여 및 인증은 장치 ID를 사용하며 액세스 자격 증명 및 권한은 즉시 취소 가능합니다.

### <a name="secure-connectivity"></a>보안 연결
메시징의 내구성은 IoT 솔루션의 중요한 기능입니다. hello 필요 toodurably 명령을 배달 및/또는 장치에서 데이터를 받을 hello 인터넷 또는 신뢰할 수 있는 하지 않을 수 있는 유사한 다른 네트워크를 통해 연결 된 IoT 장치 hello 팩트도 밑줄이 표시 됩니다. Azure IoT Hub 클라우드와 승인 응답 toomessages에서의 시스템을 통해 장치 사이의 메시징 내 구성을 제공 합니다. 메시징에 대 한 추가 지 속성은 원격 분석을 위한 tooseven 일 및 명령에 대 한 일을 hello에 대 한 IoT Hub에서 캐싱 메시지 낼 수 있습니다.

효율성은 리소스 및 리소스 제한 된 환경에서 작업의 중요 한 tooensure 보존 합니다. 효율적인 통신을 사용 하도록 설정, Azure IoT Hub에서 HTTPS (HTTP 보안), hello 업계 표준 보안 버전의 hello 인기 있는 http 프로토콜을 사용할 수 있습니다. AMQP(Advanced Message Queuing Protocol) 및 MQTT(Message Queuing Telemetry Transport)가 Azure IoT Hub에서 지원되며 리소스 사용에 관한 효율성뿐만 아니라 안정적인 메시지 전달을 위해서 설계되었습니다. 

확장성은 hello 기능 toosecurely 다양 한 장치와 interoperate 필요합니다. Azure IoT 허브를 사용 하면 보안 연결 tooboth IP 사용 및 IP 사용 가능 장치입니다. IP 사용 장치는 수 toodirectly 연결 하 고 보안 연결을 통해 hello IoT Hub와 통신 합니다. IP 미사용 장치는 리소스가 제한되며 Zwave, ZigBee 및 Bluetooth와 같은 단거리 통신 프로토콜을 통해서만 연결됩니다. 필드 게이트웨이 사용 되는 tooaggregate 이러한 장치는 하 고 hello 클라우드와 프로토콜 변환 tooenable 보안 양방향 통신을 수행 합니다.

추가 연결 보안 기능에는 hello 다음 포함:

* hello 또는 게이트웨이 Azure IoT Hub 장치와 Azure IoT Hub 간의 통신 경로 사용 하 여 보안 업계 표준 보안 TLS (전송 계층) X.509 프로토콜을 사용 하 여 인증 하는 Azure IoT Hub와 합니다.
* 무단된 인바운드 연결에서 순서 tooprotect 장치에서 Azure IoT 허브는 모든 연결 toohello 장치를 열지 않습니다. hello 장치는 모든 연결을 시작합니다. 
* Azure IoT Hub는 지속적으로 장치에 대 한 메시지를 저장 하 고 hello 장치 tooconnect 될 때까지 기다립니다. 이러한 명령은 tooreceive toopower 또는 연결 문제로 인해 산발적으로 연결 하는 장치의 이러한 명령을 사용 하는 2 일에 대 한 저장 됩니다. Azure IoT Hub는 각 장치에 대한 장치별 큐를 유지 관리합니다.

### <a name="secure-processing-and-storage-in-hello-cloud"></a>보안 처리 및 hello 클라우드 저장소
Hello 클라우드에서 암호화 된 통신 tooprocessing 데이터, Azure IoT Suite hello 데이터를 보안 유지할 수 있습니다. 유연성 tooimplement 추가 암호화 및 보안 키의 관리를 제공합니다. Azure Active Directory (AAD)를 사용 하 여 사용자 인증 및 권한 부여, Azure IoT Suite 제공할 수 있습니다는 정책 기반 권한 부여 모델 hello 클라우드에서 데이터에 대 한 감사 하 고 검토할 수 있는 간편한 액세스 관리를 사용 하도록 설정 합니다. 또한이 모델에는 거의 즉시 해지를 hello 클라우드에서 액세스 toodata 및 장치 연결 된 toohello Azure IoT Suite 수 있습니다.

Hello 클라우드에서 데이터를 처리 하 고 모든 사용자 정의 워크플로가에 저장 될 수 있습니다. Hello 데이터의 액세스 tooeach 부분 hello 저장소 서비스 사용에 따라 Azure Active Directory에 의해 제어 됩니다.

Hello IoT 인프라에서 사용 되는 모든 키 대비 키 다시 프로 비전 toobe hello 클라우드를 통해 hello 기능 tooroll와 보안 저장소에 저장 됩니다. 데이터에 저장할 수 [Azure Cosmos DB](../documentdb/documentdb-introduction.md) 또는 [SQL 데이터베이스](../sql-database/sql-database-faq.md)를 원하는 보안 수준 hello의 정의 사용 하도록 설정 합니다. 또한 Azure 방식으로 toomonitor 제공 하 고 모든 액세스 tooyour 데이터 tooalert 감사 모든 침입 또는 무단으로 액세스 하는 경우.

## <a name="conclusion"></a>결론
hello 사물 인터넷으로 시작 하면 작업-hello 대부분 toobusinesses 중요 한 문제입니다. IoT는 비용을 절감 하 고, 수익, 증가, 비즈니스를 변환 하 여 놀라운 일 값 tooa 비즈니스를 제공할 수 있습니다. 이 변환의 성공 여부는 대체로 hello 오른쪽 IoT 소프트웨어 및 서비스 공급자 선택에 따라 다릅니다. 즉, 비즈니스 요구 및 요구 사항을 이해하여 이 변환을 촉진시킬 뿐만 아니라 주요 설계 고려 사항으로 보안, 개인 정보, 투명성 및 규정 준수가 기본 제공되는 서비스 및 소프트웨어를 제공하는 공급자를 찾는 것입니다. Microsoft는 방대한 경험을 개발 하 고 보안 소프트웨어 및 서비스 배포 하 고 새 시대 사물 인터넷 toobe 선두를 계속 합니다. 

Microsoft Azure IoT Suite hello 보안 조치에 디자인, 자산 tooimprove 효율성 운영 성과 tooenable 혁신을 추구 하 고의 보안 모니터링을 사용 하 여 빌드되고 사용 고급 tootransform 기업 데이터 분석 됩니다. 보안, 여러 보안 기능 및 디자인 패턴으로은 계층형된 방식을와 Azure IoT Suite 모든 비즈니스 신뢰할 수 있는 tootransform 될 수 있는 인프라를 배포할 수 있습니다. 

## <a name="additional-information"></a>추가 정보
각 Azure IoT Suite 미리 구성 된 솔루션 hello 다음과 같은 Azure 서비스의 인스턴스를 만듭니다.

* [**Azure IoT Hub**](https://azure.microsoft.com/services/iot-hub/): 너무 hello 클라우드를 연결 하는 게이트웨이 "구성 요소"입니다. 솔루션을 보호 하는 데 도움이 되는 장치 단위 인증 지원 toomillions 허브 및 프로세스 대규모 볼륨 데이터의 당 연결을 확장할 수 있습니다.
* [**Azure Cosmos DB**](https://azure.microsoft.com/services/documentdb/): hello 장치에 대 한 메타 데이터를 관리 하는 반 구조화 된 데이터에 대 한 확장성, 완벽 하 게 인덱싱할 데이터베이스 서비스를 프로 비전 할 같은 특성, 구성 및 보안 속성입니다. Cosmos DB는 높은 성능 및 처리량 처리, 데이터의 스키마와 관계 없는 인덱싱 및 풍부한 SQL 쿼리 인터페이스를 제공합니다.
* [**Azure 스트림 분석**](https://azure.microsoft.com/services/stream-analytics/): toorapidly 있습니다 수 있도록 하는 hello 클라우드에서 처리 하는 실시간 스트림 개발 하 고는 저렴 한 비용 솔루션 toouncover 실시간에서 얻은 분석 통찰 장치, 센서, 인프라를 배포 하 고 응용 프로그램입니다. hello 서비스에서에서 데이터를이 완전히 관리 되는 높은 처리량, 짧은 대기 시간 및 복원 력을 확보 tooany 볼륨을 확장할 수 있습니다.
* [**Azure 앱 서비스**](https://azure.microsoft.com/services/app-service/): 클라우드 플랫폼 toobuild 강력한 웹 및 모바일 앱 toodata 아무 곳 이나;에 연결 하는 hello 클라우드 또는 온-프레미스에 있습니다. iOS, Android 및 Windows를 위한 유용한 모바일 앱을 빌드하세요. 클라우드 기반 서비스의 기본 연결 toodozens로 응용 프로그램 및 엔터프라이즈 응용 프로그램 소프트웨어와 함께 Saas () 및 엔터프라이즈 통합 합니다. 즐겨 찾는 언어 및 IDE에서 코드를-.NET, Node.js, PHP, Python 또는 Java-그 어느 때 보다 더 빠르게 toobuild 웹 앱 및 Api입니다.
* [**논리 앱**](https://azure.microsoft.com/services/app-service/logic/): hello 논리 앱 Azure 앱 서비스의 기능은 IoT 솔루션 tooyour 기존 기간 업무 시스템 통합 및 워크플로 프로세스를 자동화 합니다. 응용 프로그램 논리는 트리거에서 시작 하 고 다음 일련의 단계를 실행 하는 개발자가 toodesign 워크플로 사용 하면-규칙 및 비즈니스 프로세스와 toointegrate 강력한 커넥터를 사용 하는 작업입니다. 논리 앱의 기본 연결 tooa vast 생태계 SaaS, 클라우드 기반을 제공 하며 온-프레미스 응용 프로그램.
* [**Azure blob 저장소**](https://azure.microsoft.com/services/storage/): 장치는 toohello 클라우드를 전송 하는 hello 데이터에 대 한 경제적이 고, 신뢰할 수 있는 클라우드 저장소입니다.

## <a name="next-steps"></a>다음 단계
toolearn 하면 IoT 솔루션 보안 설정에 대해 자세히 알아보려면

* [IoT 보안 모범 사례][lnk-security-best-practices]
* [IoT 보안 아키텍처][lnk-security-architecture]
* [IoT 배포 보안 유지][lnk-security-deployment]

[lnk-security-best-practices]: iot-security-best-practices.md
[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md

탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:

* [예측 정비 사전 구성 솔루션 개요][lnk-predictive-overview]
* [IoT Suite에 대한 질문과 대답][lnk-faq]

IoT Hub 보안에 대 한 읽을 수 [컨트롤 액세스 tooIoT 허브] [ lnk-devguide-security] hello IoT 허브 개발자 가이드에서에서.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
