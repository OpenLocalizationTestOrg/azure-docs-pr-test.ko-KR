---
title: "보안 아키텍처 aaaIoT | Microsoft Docs"
description: "IoT 보안 아키텍처 지침 및 고려 사항"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 18ed3eb0-9406-44e1-8a3a-93dc6726c7ac
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 5b59133f6b1b45573318c3bd5b621d27b147d71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-architecture"></a>사물 인터넷 보안 아키텍처
시스템을 디자인할 때 중요 한 toounderstand hello 잠재적 위협 toothat 시스템 이며 hello 시스템을 디자인 하 고 설계 하는 대로 적절 한 방어를 적절 하 게 추가 합니다. 것이 특히 중요 toodesign 적절 한 완화 hello 처음부터 현재 위치에 있는지 확인 하는 사용 하면 공격자는 시스템 수 toocompromise 수 있습니다 어떻게 이해 하기 때문에 보안을 염두 hello 시작에서 제품을 hello 합니다. 

## <a name="security-starts-with-a-threat-model"></a>보안은 위협 모델에서 출발
Microsoft가 해당 제품에 대 한 위협 모델을 사용 시간 및 hello 회사의 위협 모델링 프로세스를 공개적으로 제공 했습니다. hello 회사 환경에서는 hello 모델링에 예기치 않은 이점 hello와 관련 된 대부분의 위협은 hello 이해 즉시 초과 합니다. 예를 들어 또한 만듭니다 열려 토론에 대 한 통로 다른 사용자와 외부 hello 개발팀 hello 제품에 toonew 아이디어 및 향상 될 수 있습니다.

hello 위협 모델링의 목적은 toounderstand 공격자는 시스템 수 toocompromise 되어를 다음 적절 한 완화 기능이 구현 되어 있는지 확인 방법입니다. 위협 모델링 hello 시스템 설계 된 대로 hello 디자인 팀 tooconsider 완화를 강제로 수행 하는 시스템에서 배포 된 후 보다는 합니다. 이 점은 매우 중요 한 hello 필드에 있는 장치의 보안 방어 tooa 무수 수정이 불가능 하기 때문에 오류가 발생할 위험에 고객 유지 됩니다.

대부분의 개발 팀 훌륭하게 수행 hello 기능적 요구 사항을 hello 시스템에 대 한 고객을 활용 하는 캡처를 수행 합니다. 그러나 hello 시스템을 오용 수 누군가가 불분명 방법을 식별 하는 좀 더 어렵습니다. 개발 팀은 위협 모델링을 통해 공격자가 어떤 이유로 어떤 행동을 하는지 파악할 수 있습니다. 위협 모델링에으로 hello 시스템 보안에 영향을 주는 hello 과정 적용 된 변경 내용 toohello 디자인에서 hello 보안에 대 한 토론 디자인 관련 결정을 작성 하는 구조화 된 프로세스입니다. 문서에 간단히 위협 모델을 사용 하는 동안이 설명서는 또한 위한 이상적인 방법을 단원 보존 지식의 tooensure 연속성 고 배운 등록할 새 팀을 신속 하 게 도움말을 나타냅니다. 마지막으로, 위협 모델링의 결과 tooenable 있습니다 tooconsider 보안 어떤 보안 약정 원하는 tooprovide tooyour 고객 등의 기타 측면. 이러한 약속을 위협 모델링과 함께 사용하여 IoT(사물 인터넷) 솔루션에 대해 조사하고 테스트할 수 있습니다.

### <a name="when-toothreat-model"></a>때 toothreat 모델
[위협 모델링](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) hello 디자인 단계에 통합 된 경우 제공 hello 가장 큰 값입니다. 을 디자인 하는 hello 가장 큰 유연성 toomake 변경 tooeliminate 위협 수 있습니다. Hello 원하는 결과 의도적인 위협 요소를 제거 합니다. 나중에 보안 기능을 추가하고, 테스트하고, 최신 상태를 유지하는 것보다는 설계 시에 위협 요소를 제거하는 것이 훨씬 간단합니다. 아무 때나 위협 요소를 제거할 수 있는 것이 아닙니다. 위협 제품 않아서 더 많은 발달 하 고 다시 궁극적으로 필요 합니다는 위협 모델링 hello 개발 초기에 보다 훨씬 더 어렵기 장단점 및 작업을 더 어렵게 tooeliminate 됩니다.

### <a name="what-toothreat-model"></a>어떤 toothreat 모델
전체 및 또한 hello 영역 뒤에 포커스와 모델 hello 솔루션 스레드 해야:

* hello 보안 및 개인 정보 보호 기능
* 해당 오류는 보안 관련 hello 기능
* 트러스트 경계를 수정 하는 hello 기능 

### <a name="who-threat-models"></a>위협 모델링 사용자
위협 모델링은 여느 프로세스와 다르지 않습니다.  Hello 솔루션의 다른 구성 요소가 같은 것이 좋습니다 tootreat hello 위협 모델 문서 이며 유효성을 검사 합니다. 대부분의 개발 팀 훌륭하게 수행 hello 기능적 요구 사항을 hello 시스템에 대 한 고객을 활용 하는 캡처를 수행 합니다. 그러나 hello 시스템을 오용 수 누군가가 불분명 방법을 식별 하는 좀 더 어렵습니다. 개발 팀은 위협 모델링을 통해 공격자가 어떤 이유로 어떤 행동을 하는지 파악할 수 있습니다.

### <a name="how-toothreat-model"></a>어떻게 toothreat 모델
hello 위협 모델링 프로세스; 네 단계로 구성 됩니다. hello 단계는 같습니다.

* 모델 hello 응용 프로그램
* 위협 요소 열거
* 위협 완화
* Hello 완화 유효성 검사

#### <a name="hello-process-steps"></a>hello 프로세스 단계
위협 모델을 작성할 때 염두에서 tookeep 세 규칙 설정:

1. 참조 아키텍처로 다이어그램을 만듭니다. 
2. 너비 우선으로 시작합니다. 개요, 하 고 더 세부적 설정 하기 전에 전체 hello 시스템을 이해 합니다.  이 사용이 하면 확인 하면 심층적 hello 오른쪽에 배치 합니다.
3. Hello 프로세스를 드라이브에 설치 되어 있습니다 드라이브 hello 프로세스 주저 하지 마시기 바랍니다. Hello 모델링 단계에서에서 문제가 발견 하 고 tooexplore를 원하는 경우에 대 한 이동 하기!  제시 slavishly toofollow 이러한 단계를 보려면 있습니다.  

#### <a name="threats"></a>위협
hello 위협 모델의 네 가지 핵심 요소입니다.

* 프로세스(웹 서비스, Win32 서비스, *nix daemons 등) 이 영역에서 기술적 드릴다운이 불가능한 경우 일부 복잡한 엔터티(예: 현장 게이트웨이 및 센서)를 추상화할 수 있습니다.
* 데이터 저장소(구성 파일 또는 데이터베이스처럼 데이터가 저장되는 모든 장소)
* 데이터 흐름 (여기서 사이 이동 hello 응용 프로그램의 다른 요소)
* 외부 엔터티 (hello 시스템과 상호 작용 하는 아무 것도 있지만 제어 하지 않는 hello hello 응용 프로그램의, 예로 사용자가 위성 피드)

Hello 아키텍처 다이어그램에서 모든 요소는 주체 toovarious 위협; STRIDE 니모닉 hello를 사용 합니다. 읽기 [위협 모델링 다시, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow hello STRIDE 요소에 대 한 자세한 합니다.

Hello 응용 프로그램 다이어그램의 서로 다른 요소는 주체 toocertain STRIDE 위협:

* 프로세스는 주체 tooSTRIDE
* 데이터 흐름은 주체 tooTID
* 데이터 저장소는 주체 tooTID 및 경우에 따라 R을 hello 데이터 저장소 로그 파일이 경우입니다.
* 외부 엔터티는 주체 tooSRD

## <a name="security-in-iot"></a>IoT의 보안
연결 된 특수 한 용도의 장치 발생할 수 있는 상호 작용 노출 영역 및 상호 작용 패턴을 모두 고려해 야 할 tooprovide 디지털 액세스 toothose 장치 보안을 위한 프레임 워크의 중요 한 번호가 없습니다. hello 용어 "디지털 액세스"가 실제 액세스 제어를 통해 액세스 보안을 제공 하는 경우 장치 직접 상호 작용을 통해 수행 되는 모든 작업에서 사용 되는 여기서 toodistinguish입니다. 예를 들어 hello 도어의 잠금 가진 대화방에 hello 장치를 저장합니다. 소프트웨어 및 하드웨어를 사용 하 여 물리적으로 액세스를 거부할 수 없습니다, 동안 측정값 toosystem 간섭 선두적인 tooprevent 물리적으로 액세스를 수행할 수 있습니다. 

Hello 상호 작용 패턴을 탐색에 대해서 "장치 제어" 되며 "장치 데이터"와 같은 수준의 주의 기울여야 hello 됩니다. "장치 제어" tooa 장치를 변경 하거나 상태 또는 해당 환경의 hello 상태 방향으로 동작에 영향을 주는의 hello 목표와의 모든 당사자에 의해 제공 되는 모든 정보로 분류할 수 있습니다. "장치 데이터" 장치를는 tooany 해당 상태 및 해당 환경의 상태를 관찰 하는 hello에 대 한 다른 파티를 내보냅니다 모든 정보로 분류할 수 있습니다.

순서 toooptimize 보안 모범 사례를 일반적인 IoT 아키텍처 있는지 hello 위협 모델링 훈련의 일부로 여러 구성 요소/영역으로 분할 하도록 것이 좋습니다. 이러한 영역은 이 섹션 전체에 자세히 설명되어 있으며 다음 내용이 포함됩니다.

* 장치
* 현장 게이트웨이
* 클라우드 게이트웨이
* 권한 부여.

영역에는 광범위 한 방식으로 toosegment 솔루션; 각 영역에는 자체 데이터 및 인증 및 권한 부여 요구 사항에 경우가 많습니다. 영역에 사용 되는 tooisolation 될 수도 있습니다 손상 하 고 더 높은 신뢰 영역에 낮은 신뢰 영역의 hello 영향을 제한 합니다.

각 영역은 hello hello 다이어그램 아래에 빨간색 선이 점선으로 기록 되는 신뢰 경계를로 구분 됩니다. 하나의 소스 tooanother에서 전환을 하는 데이터/정보를 나타냅니다. 이 전환 하는 동안 hello 데이터/정보 변조, 부인, 정보 공개, 서비스 거부 및 권한 상승 (STRIDE) 주체 tooSpoofing 수 있습니다.

![IoT 보안 영역](media/iot-security-architecture/iot-security-architecture-fig1.png) 

hello 구성 요소에 사용 된 각 경계 내에서 또한 전체 360을 사용 하도록 설정의 대상 tooSTRIDE 위협 hello 솔루션의 보기를 모델링 합니다. hello 구성 요소 및 특정 보안 문제를 구현 해야 하는 솔루션의 각 hello 섹션 아래에 자세히 설명 합니다.

hello 다음 섹션에서는 이러한 영역에서 일반적으로 발견 하는 표준 구성 요소에 설명 합니다.

### <a name="hello-device-zone"></a>hello 장치 영역
hello 장치 환경 공간이 hello 즉시 물리적 hello 장치를 물리적으로 액세스 및/또는 "로컬 네트워크" 피어-투-피어 디지털이 toohello 액세스 주위 장치는 불가능 합니다. "로컬 네트워크" toobe 고유 하며 –에서 인슐레이션된 하지만 너무 hello-공용 인터넷을 잠재적으로 브리지를 장치의 피어-투-피어 통신을 허용 하는 모든 근거리 무선 기술을 포함 한 네트워크를 가정 합니다. 그렇게 *하지* hello 감 로컬 네트워크를 만드는 모든 네트워크 가상화 기술을 포함 하 고 필요한 모든 장치 두 개가 toocommunicate 공용 네트워크 공간을 수행 하는 공용 연산자 네트워크도 포함 하지 않습니다 피어-투-피어 tooenter 통신 관계 것입니다.

### <a name="hello-field-gateway-zone"></a>hello 필드 게이트웨이 영역
현장 게이트웨이는 통신 인에이블러로 작동하고 잠재적으로 장치 제어 시스템 및 장치 데이터 처리 허브 역할을 하는 장치 어플라이언스 또는 범용 서버 컴퓨터 소프트웨어입니다. 모든 장치에 연결 tooit 및 hello 필드 게이트웨이 영역에는 hello 필드 게이트웨이 자체 포함 됩니다. Hello 이름에서 알 수 있듯이 필드 게이트웨이 전용된 외부 데이터 처리 기능을 역할은 일반적으로 위치 바인딩된, 주체 toophysical 침입은 될 수 및 operational 중복 제한 됩니다. 필드 게이트웨이 일반적으로 모든 toosay 하나는 일 수 및 해당 함수는 하는 동안 파괴 누릅니다. 

현장 게이트웨이는 액세스 및 정보 흐름을 관리하는 활성 역할이 있다는 점에서, 다시 말해서 응용 프로그램 주소 지정 엔터티이자 네트워크 연결 또는 세션 터미널이라는 점에서 단순한 트래픽 라우터와 다릅니다. 한편, NAT 장치 또는 방화벽은 명시적인 연결 또는 세션 터미널이 아니고 이를 통과하는 연결 또는 세션을 라우팅(또는 차단)하므로 현장 게이트웨이로 간주되지 않습니다. hello 필드 게이트웨이 두 개의 고유한 노출 영역에 있습니다. 하나 hello는 장치에 연결 된 tooit 향하도록 hello 영역 안에 hello 나타냅니다 되며, 다른 hello 모든 외부 당사자가 직면 hello 영역의 hello 가장자리가 합니다.   

### <a name="hello-cloud-gateway-zone"></a>hello 클라우드 게이트웨이 영역
클라우드 게이트웨이 클라우드 기반 제어 및 데이터 분석 시스템 이러한 시스템의 페더레이션으로 일반적으로 공용 네트워크 공간에서의 원격 통신 및 여러 사이트에서 게이트웨이 toodevices 또는 필드를 사용할 수 있는 시스템. 경우에 따라 클라우드 게이트웨이 즉시 태블릿 또는 휴대폰과 같은 쉽다는 toospecial 용도의 장치에 액세스도 기여할 수 있습니다. 설명 hello 컨텍스트에서 여기에서 "클라우드" toorefer tooa 전용 데이터 처리 시스템 바인딩된 toohello hello 연결 장치 또는 필드 게이트웨이 사이트 동일 하지 않은 것입니다. 또한 클라우드 영역 operational 측정값 대상으로 지정 된 물리적 액세스를 방지 하며 반드시 노출 된 tooa "공용 클라우드" 인프라 되지 않습니다.  

클라우드 게이트웨이 네트워크 가상화 오버레이 tooinsulate hello 클라우드 게이트웨이 및 모든 해당 연결 된 장치 또는 다른 네트워크 트래픽과에서 필드 게이트웨이에 잠재적으로 매핑할 수 있습니다. hello 클라우드 게이트웨이 자체는 장치 제어 시스템 또는 처리 또는 장치 데이터;에 대 한 저장소 시설 모두 이러한 기능의 hello 클라우드 게이트웨이와 인터페이스입니다. 직접 또는 간접적으로 연결 된 장치 tooit 및 hello 클라우드 게이트웨이 영역에는 모든 필드 게이트웨이 함께 자체 hello 클라우드 게이트웨이 포함 됩니다. hello 가장자리가 hello 영역에 모든 외부 당사자를 통해 통신 하는 고유한 노출 영역입니다.

### <a name="hello-services-zone"></a>hello 서비스 영역
현재 문맥에서 “서비스”는 데이터 수집 및 분석과 명령 및 제어를 위해 현장 또는 클라우드 게이트웨이를 통해 장치와 상호 작용하는 모든 소프트웨어 구성 요소 또는 모듈로 정의됩니다.  서비스는 중재자입니다. 식별 하기 위한 게이트웨이 및 다른 하위 시스템에서 역할은, 저장 하 고 데이터 분석, 문제 명령 toodevices 데이터 통찰력 또는 일정에 따라 하 고 정보 및 제어 기능 tooauthorized 최종 사용자에 게 노출 하는 자치 적으로 작동 합니다.

### <a name="information-devices-vs-special-purpose-devices"></a>정보 장치와 특수 장치의 비교
PC, 스마트폰 및 태블릿은 주로 대화형 정보 장치입니다. 스마트폰과 태블릿은 배터리 수명을 최대화하기 위해 명시적으로 최적화됩니다. 가급적 부분적으로 즉시 사용자와 상호 작용할 때 설정 하거나 해제할 tooa 특정 위치 음악 재생 또는 소유자 안내와 같은 서비스를 제공 하지 않을 경우. 시스템의 관점에서 이러한 정보 기술 장치는 주로 사람에 대한 프록시 역할을 합니다. 작업을 제안하는 “사람 작동기”이자 입력을 수집하는 “사람 센서”입니다. 

특수 한 용도의 장치 구성 요소 내에 수천 간단한 온도 센서 toocomplex 팩터리에서는 생산 라인에서 서로 다릅니다. 이러한 장치 목적에 훨씬 더 범위 포함 되며 일부 사용자 인터페이스를 제공 하는 경우에와 크게 범위가 지정 된 toointerfacing 인지 hello 실제 세계에서 자산에 통합할 수 있습니다. 환경적 상황을 측정 및 보고하고, 밸브를 조절하고, 서보를 제어하고, 소리로 알림을 전달하고, 조명을 조절하는 등 여러 작업을 수행합니다. 그렇게 쉽게 작동 toodo 있는 정보 장치는 너무 일반적, 너무 비쌉니다., 너무 커서 또는 너무 불안정 있습니다. 즉시 hello 구체적인 용도 프로덕션 및 수명 예약 된 작업에 대해 사용 가능한 금액 예산 안녕하세요도 기술 디자인을 결정합니다. 이러한 두 가지 주요 요소 조합의 hello hello 사용할 수 있는 operational 에너지 예산, 물리적 공간 및 따라서 사용 가능한 저장소, 계산 및 보안 기능을 제한합니다.  

값 "이 되는 잘못 된" 예를 들어, 자동 또는 원격 제어할 수 있는 장치를 사용 하는 경우 실제 결함 또는 제어 논리 결함 toowillful 권한이 없음 침입 및 조작 합니다. hello 프로덕션 많은 소멸 됩니다, 건물 looted 하거나 다운 구울 수 및 사용자 사람과 많아지고 있으며 다이 될 수 있습니다. 이러한 사고는 누군가가 훔친 신용 카드를 한도까지 사용하는 것과는 피해 규모의 차원이 다릅니다. hello 작업 하는 장치에 대 한 보안 수준을 이동 및 또한 센서 데이터에 대 한는 결국 작업 toomove 발생 하는 명령에 결과 보다 높아야 전자 상거래 또는 뱅킹 시나리오에서. 

### <a name="device-control-and-device-data-interactions"></a>장치 제어 및 장치 데이터 상호 작용
연결 된 특수 한 용도의 장치 발생할 수 있는 상호 작용 노출 영역 및 상호 작용 패턴을 모두 고려해 야 할 tooprovide 디지털 액세스 toothose 장치 보안을 위한 프레임 워크의 중요 한 번호가 없습니다. hello 용어 "디지털 액세스"가 실제 액세스 제어를 통해 액세스 보안을 제공 하는 경우 장치 직접 상호 작용을 통해 수행 되는 모든 작업에서 사용 되는 여기서 toodistinguish입니다. 예를 들어 hello 도어의 잠금 가진 대화방에 hello 장치를 저장합니다. 소프트웨어 및 하드웨어를 사용 하 여 물리적으로 액세스를 거부할 수 없습니다, 동안 측정값 toosystem 간섭 선두적인 tooprevent 물리적으로 액세스를 수행할 수 있습니다. 

Hello 상호 작용 패턴을 탐색에 대해서 "장치 제어" 되며 "장치 데이터"와 같은 수준의 위협 모델링 하는 동안 주의 기울여야 hello 됩니다. "장치 제어" tooa 장치를 변경 하거나 상태 또는 해당 환경의 hello 상태 방향으로 동작에 영향을 주는의 hello 목표와의 모든 당사자에 의해 제공 되는 모든 정보로 분류할 수 있습니다. "장치 데이터" 장치를는 tooany 해당 상태 및 해당 환경의 상태를 관찰 하는 hello에 대 한 다른 파티를 내보냅니다 모든 정보로 분류할 수 있습니다. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>위협 모델링 hello Azure IoT 참조 아키텍처
Microsoft는 toodo 위협 모델링에 대 한 Azure IoT 위에서 설명한 hello 프레임 워크를 사용 합니다. 따라서 아래 hello 섹션에서 Azure IoT 참조 아키텍처 toodemonstrate toothink 모델링 IoT 및 tooaddress 위협 hello 하는 방법에 대 한 위협에 대 한 식별 하는 방법의 hello 구체적인 예를 사용 합니다. 이 예에서는 다음 네 가지 주요 포커스 영역이 확인되었습니다.

* 장치 및 데이터 원본
* 데이터 전송
* 장치 및 이벤트 처리
* 프레젠테이션

![Azure IoT 위협 모델링](media/iot-security-architecture/iot-security-architecture-fig2.png) 

아래 hello 다이어그램 hello Microsoft 위협 모델링 도구에서 사용 되는 데이터 흐름 다이어그램 모델을 사용 하 여 Microsoft의 IoT 아키텍처의 대략적인된 개요를 제공 합니다.

![MS Threat Modeling Tool을 사용하여 Azure IoT 위협 모델링](media/iot-security-architecture/iot-security-architecture-fig3.png)

아키텍처 hello toonote hello 장치 및 게이트웨이 기능을 구분 합니다. 이렇게 하면 hello 사용자 tooleverage 더 안전 하는 게이트웨이 장치: hello 클라우드 보안 프로토콜을 사용 하 여 일반적으로 필요한 게이트웨이 큰 처리 오버 헤드가 자동 온도 조절기-예: 기본 장치-수 있는지와 통신할 수 자체적으로 제공 합니다. Hello Azure 서비스 영역에 클라우드 게이트웨이 hello Azure IoT 허브 서비스를 나타내는 해당 hello를 가정 합니다.

### <a name="device-and-data-sourcesdata-transport"></a>장치 및 데이터 원본/데이터 전송
이 섹션 위협 모델링의 hello 렌즈를 통해 위에서 설명한 hello 아키텍처를 탐색 하 고 어떻게 것 들이 직면 hello 내재 된 문제 중 일부에 대해 간략하게를 제공 합니다. 위협 모델의 hello 핵심 요소에 대해 살펴볼 것:

* 프로세스(내부에서 제어 가능한 프로세스 및 외부 항목)
* 통신(데이터 흐름이라고도 함)
* 저장소(데이터 저장소라고도 함)

#### <a name="processes"></a>프로세스
수많은 hello 여러 단계 데이터/정보에서 위협에 존재 하는 toomitigate 시도 각 hello Azure IoT 아키텍처에서에서 설명 하는 hello 범주: 프로세스, 통신 및 저장 합니다. 아래 hello에 대 한 개요 hello "프로세스" 범주를 어떻게 이러한 수 가장 완화 될의 개요에 대 한 가장 자주 제공: 

**(S) 스푸핑을**: 공격자는 hello 소프트웨어 또는 하드웨어 수준에서 장치에서 암호화 키 자료를 추출 하 고 이후에 hello 장치 hello의 hello id는 다른 실제 또는 가상 장치를 사용 하 여 hello 시스템을 액세스할 수 있습니다 키 자료에서 사용 되었습니다. 모든 TV를 켜고 끌 수 있어서 사람들이 장난을 치기 위한 도구로 많이 구입하는 원격 리모콘이 대표적인 예입니다.

**서비스 거부(D)**: 무선 주파수를 방해하거나 와이어를 절단하여 장치의 정상 작동 또는 통신을 불가능하게 만들 수 있습니다. 예를 들어 감시 카메라의 자체 전원 또는 네트워크 연결을 고의적으로 끊으면 감시 카메라가 데이터를 전혀 보고하지 않습니다.

**(T) 변조**: 공격자가 부분적으로 나 완전히 바꿀 수 hello 장치에서 실행 되는 hello 소프트웨어, 키 자료 또는 암호화 hello 경우 hello 대체 hello 소프트웨어 tooleverage hello 정품 id hello 장치의 수 있으므로 키 자료를 보유 하는 기능에 사용할 수 있는 toohello 불법 프로그램 했습니다. 예를 들어 하면 공격자가 될 수 있습니다 압축 푼된 키 재료 toointercept 및 hello 통신 경로에 hello 장치에서 데이터를 표시 하지 않는 및 활용할 도난 hello 키 자료와 인증 된 false 데이터로 바꿉니다.

**정보 공개 (I)**: hello 장치 조작된 소프트웨어를 실행 하는 경우 해당 조작된 소프트웨어 toounauthorized 파티 데이터 누수가 발생할 수 있습니다. 예를 들어 공격자 압축 푼된 키 재료 tooinject 자체 hello 장치와 컨트롤러나 필드 게이트웨이 간의 통신 경로 hello로 활용할 수도에서 정보가 게이트웨이 toosiphon 클라우드 있습니다.

**권한 (E)의 상승**: 특정 기능을 수행 하는 장치에 다른 값인지 강제 toodo 일 수 있습니다. 예를 들어 프로그래밍 된 tooopen 수 방식으로 절반은 밸브 아닌 모든 hello tooopen 악성 스크립트가 방법입니다.

| **구성 요소** | **위협** | **해결 방법** | **위험** | **구현** |
| --- | --- | --- | --- | --- |
| 장치 |S |Identity toohello 장치를 할당 하 고 hello 장치 인증 |교체 장치 또는 일부 다른 장치를 사용 하 여 hello 장치입니다. 올바른 장치 toohello 하는지 어떻게 알 수 있습니까? |보안 TLS (전송 계층) 또는 IPSec을 사용 하 여 hello 장치를 인증 합니다. 전체 비대칭 암호화를 처리할 수 없는 PSK(미리 공유한 키)를 해당 장치에서 사용할 수 있도록 인프라가 지원해야 합니다. Azure AD, [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt)를 활용하세요. |
| TRID |예를 들어 매우 어려운 tooimpossible tooextract 키와 다른 암호화 관련 자료 hello 장치에서 만들어 변조 방지 메커니즘 toohello 장치를 적용 됩니다. |hello 위험은 무단 변경을 hello 장치 (물리적 간섭)는 사용자입니다. 장치가 변조되지 않았는지 확인하려면 어떻게 해야 할까요? |hello 가장 효과적인 완화 특수 칩에서 회로 hello에서 키를 읽을 수 없는 하지만 hello 키를 사용 하지만 hello 키를 공개 하지 않습니다는 암호화 작업에만 사용할 수의 키를 저장할 수 있도록 신뢰할 수 있는 플랫폼 모듈 (TPM) 기능입니다. . Hello 장치의 메모리 암호화 합니다. Hello 장치에 대 한 키 관리 합니다. Hello 코드를 서명 합니다. | |
| E |Hello 장치의 액세스 제어를 때 발생합니다. 권한 부여 체계. |Hello 장치 toobe를 외부 소스에 포함 된 명령을 기반으로 수행 되거나 심지어 센서 손상 된 개별 작업에 허용 하는 경우 허용 됩니다 hello 공격 tooperform 작업 그렇지 않은 경우 액세스할 수 없습니다. |Hello 장치에 대 한 권한 부여 체계를 필요합니다. | |
| 현장 게이트웨이 |S |Hello 필드 게이트웨이 tooCloud (인증서 기반, PSK, 클레임 기반,..) 게이트웨이 인증 |누군가가 현장 게이트웨이를 스푸핑할 수 있다면 현장 게이트웨이가 모든 장치로 제공될 수 있습니다. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). 모든 hello 동일한 키 저장소 및 일반-최상의 경우에서에서 장치 증명 문제는 TPM을 사용 합니다. IPSec toosupport 무선 센서 네트워크 (WSN)에 대 한 6LowPAN 확장입니다. |
| TRID |필드 게이트웨이 hello (TPM?) 변조 방지 |스푸핑 공격 속일 toofield와 통신할 thinking hello 클라우드 게이트웨이 게이트웨이 정보 공개 및 데이터 훼손 될 수 있습니다. |메모리 암호화, TPM 사용, 인증. | |
| E |현장 게이트웨이에 대한 액세스 제어 메커니즘 | | | |

다음은 이 범주의 위협에 대한 몇 가지 예입니다.

스푸핑: 공격자 수 추출 암호화 키 자료는 장치에서 등 hello 장치 hello 키 자료의 다른 실제 또는 가상 장치 hello id hello 시스템 된 hello 소프트웨어 또는 하드웨어 수준에서 이후에 액세스 중 하나 가져옵니다.

**서비스 거부**: 무선 주파수를 방해하거나 와이어를 절단하여 장치의 정상 작동 또는 통신을 불가능하게 만들 수 있습니다. 예를 들어 감시 카메라의 자체 전원 또는 네트워크 연결을 고의적으로 끊으면 감시 카메라가 데이터를 전혀 보고하지 않습니다.

**변조**: 공격자가 부분적으로 나 완전히 바꿀 수 hello 장치에서 실행 되는 hello 소프트웨어, 키 자료 또는 암호화 hello 경우 hello 대체 hello 소프트웨어 tooleverage hello 정품 id hello 장치의 수 있으므로 키 자료를 보유 하는 기능에 사용할 수 있는 toohello 불법 프로그램 했습니다.

**변조**: 빈 복도의 가시 스펙트럼 그림을 보여 주는 감시 카메라가 이러한 복도의 사진을 비추도록 변조될 수 있습니다. 연기 또는 화재 센서가 누군가가 그 아래에서 라이터를 대고 있다고 보고할 수 있습니다. 두 경우 모두 hello 장치를 hello 시스템으로 완전히 신뢰할 수 있는 기술적으로 있을 수 있지만 조작된 정보를 보고 합니다.

**변조**: 공격자 수 압축 푼된 키 재료 toointercept 활용 하 여 및 hello 통신 경로에 hello 장치에서 데이터를 표시 하지 않는 하 고 교체 도난 hello 키 자료와 인증 된 잘못 된 데이터입니다.

**변조**: 공격자가 부분적으로 또는 완전히 바꿀 수 hello 장치에서 실행 되는 hello 소프트웨어, 키 자료 또는 암호화 hello 경우 hello 대체 hello 소프트웨어 tooleverage hello 정품 id hello 장치의 수 있으므로 키 자료를 보유 하는 기능에 사용할 수 있는 toohello 불법 프로그램 했습니다.

**정보 공개**: hello 장치 조작된 소프트웨어를 실행 하는 경우 해당 조작된 소프트웨어 toounauthorized 파티 데이터 누수가 발생할 수 있습니다.

**정보 공개**: 공격자를 압축 푼된 키 재료 tooinject 자체 hello 장치와 컨트롤러나 필드 게이트웨이 hello 통신 경로에 활용 또는에서 정보가 게이트웨이 toosiphon 클라우드 수 있습니다.

**서비스 거부**: hello 장치를 해제 또는 통신이 (변수인 산업 많은 시스템에서 의도적으로) 가능 하지 않으면 모드로 설정 되어 있습니다.

**변조**: hello 장치 상태에서 재구성 되었습니다 toooperate 일 수 있습니다 알 수 없는 toohello 알려진된 보정 매개 변수) (외부 시스템을 제어 하 고 있으므로 잘못 해석 될 수 있는 데이터를 제공 합니다.

**권한 상승 문제점**: 특정 기능을 수행 하는 장치에 다른 값인지 강제 toodo 일 수 있습니다. 예를 들어 프로그래밍 된 tooopen 수 방식으로 절반은 밸브 아닌 모든 hello tooopen 악성 스크립트가 방법입니다.

**서비스 거부**: hello 장치 통신 수 없으면 상태로 변환할 수 있습니다.

**변조**: hello 장치 상태에서 재구성 되었습니다 toooperate 일 수 있습니다 알 수 없는 toohello 알려진된 보정 매개 변수) (외부 시스템을 제어 하 고 있으므로 잘못 해석 될 수 있는 데이터를 제공 합니다.

**스푸핑/변조/거부**: 보안이 설정 되지 (있는 경우 거의 hello와 소비자 원격 제어) 공격자는 장치의 상태 hello를 익명으로 조작할 수 있습니다. 모든 TV를 켜고 끌 수 있어서 사람들이 장난을 치기 위한 도구로 많이 구입하는 원격 리모콘이 대표적인 예입니다.

#### <a name="communication"></a>통신
장치 간, 장치와 현장 게이트웨이 간, 장치와 클라우드 게이트웨이 간의 통신 경로와 관련된 위협이 있습니다. hello 표에서 몇 가지 지침 hello 장치/v p N에 열려 있는 소켓 주위에 있습니다.

| **구성 요소** | **위협** | **해결 방법** | **위험** | **구현** |
| --- | --- | --- | --- | --- |
| 장치 IoT Hub |TID |(D) TLS (PSK/RSA) tooencrypt hello 트래픽 |도청 또는 hello 장치와 hello 게이트웨이 hello 통신을 방해 합니다. |Hello 프로토콜 수준에서 보안입니다. 사용자 지정 프로토콜을 사용 방법에 대해 toofigure 필요 tooprotect 해당 합니다. 대부분의 경우에서 통신 hello를 사용 하면 hello 장치 toohello (장치 hello 연결을 시작 하는 데 사용) IoT 허브에서에서 이루어집니다. |
| 장치 장치 |TID |(D) TLS (PSK/RSA) tooencrypt hello 트래픽이입니다. |장치 간에 전송 중인 데이터 읽기. Hello 데이터를 변조입니다. 새 연결을 사용 하 여 hello 장치 오버 로드 |프로토콜 수준 (MQTT/AMQP/HTTP/CoAP hello에 대 한 보안. 사용자 지정 프로토콜을 사용 방법에 대해 toofigure 필요 tooprotect 해당 합니다. hello 완화 hello DoS 위협에 대 한 클라우드 또는 필드 게이트웨이 통해 toopeer 장치 하며 hello 네트워크 쪽으로 클라이언트로 act 있어야 합니다. hello 피어 링 hello 게이트웨이에서 중개 된 발생 후 hello 피어 간 직접 연결 될 수 있습니다. |
| 외부 엔터티 장치 |TID |Hello 외부 엔터티 toohello 장치의 강력한 쌍 |도청 hello 연결 toohello 장치입니다. Hello 장치와 간섭 hello 통신 |안전 하 게 hello 외부 엔터티 toohello 장치 Bluetooth NFC/LE 쌍입니다. Hello 작동 패널 (실제) hello 장치의 제어 |
| 현장 게이트웨이 클라우드 게이트웨이 |TID |TLS (PSK/RSA) tooencrypt hello 트래픽이입니다. |도청 또는 hello 장치와 hello 게이트웨이 hello 통신을 방해 합니다. |Hello 프로토콜 수준 (MQTT/AMQP/HTTP/CoAP)의 보안. 사용자 지정 프로토콜을 사용 방법에 대해 toofigure 필요 tooprotect 해당 합니다. |
| 장치 클라우드 게이트웨이 |TID |TLS (PSK/RSA) tooencrypt hello 트래픽이입니다. |도청 또는 hello 장치와 hello 게이트웨이 hello 통신을 방해 합니다. |Hello 프로토콜 수준 (MQTT/AMQP/HTTP/CoAP)의 보안. 사용자 지정 프로토콜을 사용 방법에 대해 toofigure 필요 tooprotect 해당 합니다. |

다음은 이 범주의 위협에 대한 몇 가지 예입니다.

**서비스 거부**: 능동적으로 수신 대기 인바운드 연결 또는 네트워크에 예기치 않은 데이터 그램에 대 한 공격자 또는 수 있으므로 동시에 많은 연결을 열고 및 하지 서비스 서비스 DoS 위협에서 제한 된 장치 일반적으로 이러한 매우 느리게 또는 hello 장치 원치 않는 트래픽이 쇄도 일 수 있습니다. 두 경우 모두 hello 장치 효과적으로 렌더링할 수 hello 네트워크에서 작동 하지 않습니다.

**스푸핑, 정보 노출**: 제한 된 장치 및 특수 한 용도의 장치 종종 암호 또는 PIN 보호와 같은 중 하나에 대 한 모든 보안 시설 또는 트러스팅 hello 네트워크에 대 한 액세스 권한이 부여 됩니다. 이러한 의미를 완전히 사용 tooinformation 장치 hello에 있으면 동일한 네트워크 및 해당 네트워크는 종종만 공유 키로 보호 됩니다. 즉,는 hello 비밀 toodevice 공유 또는 네트워크 공개 됩니다 때 가능한 toocontrol hello 장치 인지 hello 장치에서 내보낸 데이터를 관찰 합니다.  

**스푸핑**: 공격자 가로채 거 나 부분적으로 hello 브로드캐스트와 스 푸 프 hello 송신자 (hello 가운데에 매뉴얼)을 재정의할 수 있습니다

**변조**: 공격자는 가로채 또는 부분적으로 hello 브로드캐스트를 재정의 잘못 된 정보 보내기 

**정보 노출:** 공격자 브로드캐스트를 가로챌 수 있습니다 및 권한 부여가 불가능 한 정보를 가져올 **서비스 거부:** 공격자 hello 방송 신호 걸림 및 정보 배포를 거부 될 수 있습니다

#### <a name="storage"></a>저장소
모든 장치 및 필드 게이트웨이 일종의 저장소 (임시 hello 데이터 큐의 경우 운영 체제 (OS) 이미지 저장소)에 있습니다.

| **구성 요소** | **위협** | **해결 방법** | **위험** | **구현** |
| --- | --- | --- | --- | --- |
| 장치 저장소 |TRID |저장소 암호화, 서명 hello 로그 |원격 분석 데이터를 변조 hello 저장소 (PII 데이터)에서 데이터를 읽고 있습니다. 큐에 대기 중이거나 캐시된 명령 제어 데이터 변조. 구성 또는 펌웨어 업데이트 패키지에 변조 캐시 되거나 로컬 큐에 대기 하는 동안 발생할 수 있습니다 손상 tooOS 및/또는 시스템 구성 |암호화, MAC(메시지 인증 코드) 또는 디지털 서명. 가능하다면 리소스 ACL(액세스 제어 목록) 사용 권한을 통해 강력한 액세스 제어. |
| 장치 OS 이미지 |TRID | |OS 변조/hello OS 구성 요소 교체 |읽기 전용 OS 파티션, 서명한 OS 이미지, 암호화 |
| 필드 게이트웨이 저장소 (큐 hello 데이터) |TRID |저장소 암호화, 서명 hello 로그 |원격 분석 데이터를 변조 hello 저장소 (PII 데이터)에서 데이터를 읽는 큐에 대기 변조 또는 명령 컨트롤 데이터를 캐시 합니다. 구성 또는 펌웨어 업데이트 패키지 (장치 또는 필드 게이트웨이 보내는) 변조 캐시 되거나 로컬 큐에 대기 하는 동안 발생할 수 있습니다 손상 tooOS 및/또는 시스템 구성 |BitLocker |
| 현장 게이트웨이 OS 이미지 |TRID | |OS 변조/hello OS 구성 요소 교체 |읽기 전용 OS 파티션, 서명한 OS 이미지, 암호화 |

### <a name="device-and-event-processingcloud-gateway-zone"></a>장치 및 이벤트 처리/클라우드 게이트웨이 영역
클라우드 게이트웨이 클라우드 기반 제어 및 데이터 분석 시스템 이러한 시스템의 페더레이션으로 일반적으로 공용 네트워크 공간에서의 원격 통신 및 여러 사이트에서 게이트웨이 toodevices 또는 필드를 사용할 수 있는 시스템. 경우에 따라 클라우드 게이트웨이 즉시 태블릿 또는 휴대폰과 같은 쉽다는 toospecial 용도의 장치에 액세스도 기여할 수 있습니다. 설명 hello 컨텍스트에서 여기에서 "클라우드" 것 같은 사이트 hello 필드 게이트웨이 또는 장치 연결 및 operational 측정값 방지 위치 물리적으로 액세스를 대상으로 하지 않으면이 바인딩된 toohello 없는 toorefer tooa 전용 데이터 처리 시스템 반드시 tooa "공용 클라우드" 인프라입니다.  클라우드 게이트웨이 네트워크 가상화 오버레이 tooinsulate hello 클라우드 게이트웨이 및 모든 해당 연결 된 장치 또는 다른 네트워크 트래픽과에서 필드 게이트웨이에 잠재적으로 매핑할 수 있습니다. hello 클라우드 게이트웨이 자체는 장치 제어 시스템 또는 처리 또는 장치 데이터;에 대 한 저장소 시설 모두 이러한 기능의 hello 클라우드 게이트웨이와 인터페이스입니다. 직접 또는 간접적으로 연결 된 장치 tooit 및 hello 클라우드 게이트웨이 영역에는 모든 필드 게이트웨이 함께 자체 hello 클라우드 게이트웨이 포함 됩니다.

클라우드 게이트웨이 주로 사용자 지정 작성 된 소프트웨어의 일부분이 노출 된 끝점 toowhich 필드 게이트웨이 통해 서비스를 실행 하 고 장치 연결 합니다. 따라서 보안을 염두에 두고 설계해야 합니다. 이 서비스를 설계하고 구축하려면 [SDL](http://www.microsoft.com/sdl) 프로세스를 따르세요. 

#### <a name="services-zone"></a>서비스 영역
제어 시스템 (또는 컨트롤러)은 장치 또는 필드 게이트웨이 또는 클라우드 게이트웨이 하나 또는 여러 장치 및/또는 toocollect 및/또는 저장소 제어 hello 목적을 위해 상호 작용 및/또는 프레젠테이션용, 장치 데이터를 분석 하는 소프트웨어 솔루션 또는 후속 제어 목적으로 합니다. 제어 시스템은 사용자와 상호 작용을 바로 쉽게 만들 수 있습니다이 설명의 hello 범위에 hello 유일한 엔터티입니다. hello 예외는 중간 물리적 컨트롤 해제 tooturn hello 장치와 사용자를 허용 하는 스위치와 장치에서 나 다른 속성을 변경 고 디지털 방식으로 액세스할 수 있는 기능 해당 키 없음입니다. 

중간 물리적 컨트롤 표면이 해당 기능을 원격으로 시작 될 수 있습니다. 또는 회피 – 원격 입력이 포함 된 입력된 충돌 될 수 있습니다 모든 종류의 논리를 제어 hello 물리적 컨트롤 화면의 hello 기능을 제한 하는 위치 컨트롤 화면 중재 됩니다는 개념적으로 연결 된 tooa 로컬 제어 시스템을 활용 하 여 장치 hello 하는 모든 원격 제어 시스템에 연결 된 tooin 병렬 수 있으므로 동일한 기본 기능 hello는입니다. 위협 toohello 클라우드 컴퓨팅에 읽을 수 있습니다 [클라우드 보안 Alliance (CSA)](https://cloudsecurityalliance.org/research/top-threats/) 페이지.

## <a name="additional-resources"></a>추가 리소스
Toohello 아티클에 대 한 자세한 내용은 다음을 참조 하십시오.

* [SDL Threat Modeling Tool](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Microsoft Azure IoT 참조 아키텍처](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

## <a name="see-also"></a>참고 항목
보안 하면 IoT 솔루션에 대 한 더 toolearn 참조 [보안 IoT 배포][lnk-security-deployment]합니다.

탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:

* [예측 정비 사전 구성 솔루션 개요][lnk-predictive-overview]
* [IoT Suite에 대한 질문과 대답][lnk-faq]

IoT Hub 보안에 대 한 읽을 수 [컨트롤 액세스 tooIoT 허브] [ lnk-devguide-security] hello IoT 허브 개발자 가이드에서에서.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md