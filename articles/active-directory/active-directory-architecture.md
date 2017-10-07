---
title: "Azure Active Directory 아키텍처 aaaUnderstand | Microsoft Docs"
description: "파악할 수를 같은 Azure AD 테 넌 트와 방법을 toomanage Azure Active Directory를 통해 Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Azure Active Directory 아키텍처 이해
Azure Active Directory (Azure AD) 사용 하면 toosecurely 액세스 tooAzure 서비스 및 사용자를 위해 리소스를 관리 합니다. Azure AD에는 전체 ID 관리 기능이 포함됩니다. Azure AD 기능에 대한 정보는 [Azure Active Directory란?](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis)을 참조하세요.

Azure AD와 수 및 사용자 및 그룹, 관리 및 사용 권한을 tooallow 만들고 tooenterprise 리소스 액세스를 거부 합니다. Id 관리에 대 한 정보를 참조 하십시오. [Azure id 관리에 대 한 기본적인 hello](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)합니다.

## <a name="azure-ad-architecture"></a>Azure AD 아키텍처
복구 기능을 통해 toodeliver 엔터프라이즈 수준의 가용성과 성능을 tooour 고객 us 및 azure AD의 지리적으로 분산된 아키텍처 광범위 하 게 모니터링, 자동화 된 다시 라우팅할 경우, 장애 조치를 결합 합니다.

아키텍처 요소 다음 hello는이 문서에 포함 됩니다.
 *  서비스 아키텍처 디자인
 *  확장성 
 *  지속적인 가용성
 *  데이터 센터

### <a name="service-architecture-design"></a>서비스 아키텍처 디자인
hello 가장 일반적인 방법은 toobuild 독립 구성 요소 또는 데이터 계층 hello Azure AD에 대 한 배율 단위를 통해 확장성, 고가용성, 데이터 기반 시스템은, 배율 단위 이라고 *파티션을*합니다. 

hello 데이터 계층에 읽기 / 쓰기 기능을 제공 하는 몇 가지 프런트 엔드 서비스에 있습니다. 아래 hello 다이어그램 hello 구성 요소는 단일 디렉터리 파티션의 distrubuted 지리적으로 분산 데이터 센터 전체 배포 되는 방법을 보여 줍니다. 

  ![단일 디렉터리 파티션](./media/active-directory-architecture/active-directory-architecture.png)

Azure AD 아키텍처의 hello 구성 요소는 주 복제본과 보조 복제본을 포함 합니다.

**주 복제본**

hello *주 복제본* 모든 수신 *씁니다* hello 파티션의 속합니다. 쓰기 작업이 쓰기 지리적 중복 내구성 하는 데 성공 toohello 호출자에 반환 하기 전에 다른 데이터 센터에 보조 복제본을 즉시 복제 tooa 되었습니다.

**보조 복제본**

모든 디렉터리 *읽기*는 *보조 복제본*에서 처리되며, 물리적으로 여러 지역에 걸쳐 위치한 데이터 센터에 있습니다. 데이터가 비동기적으로 복제되는 경우 보조 복제본이 많이 생성됩니다. 인증 요청 등, 디렉터리 읽기 닫기 tooour 고객은 데이터 센터에서 서비스 됩니다. hello 보조 복제본은 읽기 확장성 담당 합니다.

### <a name="scalability"></a>확장성

확장성은 성능 요구가 증가 서비스 tooexpand toomeet의 hello 기능입니다. 확장성을 높일 수 hello 데이터를 분할 하 여 작성 합니다. Hello world 전체로 분산 하나의 파티션 toomultiple 보조 복제본에서 데이터를 복제 하 여 읽기 확장성을 높일 수 있습니다.

디렉터리 응용 프로그램의 요청은 일반적으로 라우팅된 toohello 데이터 센터에 물리적으로 가장 가까운 더 합니다. 쓰기는 투명 하 게 리디렉션된 toohello 주 복제본 tooprovide 읽기 / 쓰기 일관성입니다. 보조 복제본 hello 디렉터리에는 일반적으로 서비스 읽기 대부분의 hello 시간 때문에 파티션 hello 눈금을 크게 확장 합니다.

디렉터리 응용 프로그램에 가장 가까운 데이터 센터 toohello를 연결합니다. 이렇게 하면 성능이 향상되고 따라서 확장이 가능합니다. 디렉터리 파티션 많은 보조 복제본을 가질 수, 있으므로 보조 복제본 자세히 toohello 디렉터리 클라이언트를 배치할 수 있습니다. 만 내부 디렉터리 서비스 구성 요소를 쓰기 집약적 대상 hello 현재 주 복제본 직접 합니다.

### <a name="continuous-availability"></a>지속적인 가용성

가용성 (또는 작동 시간)는 시스템 tooperform 중단 없이의 hello 기능을 정의합니다. hello 키 tooAzure AD의 가용성이 높은 서비스 여러 지리적으로 분산 데이터 센터 간 트래픽 이동할 신속 하 게 수입니다. 각 데이터 센터는 독립적이며 상관 관계가 지정되지 않은 오류 모드를 사용할 수 있게 해줍니다.

Azure AD의 파티션 디자인 간소화 된 비교 toohello 엔터프라이즈 hello 시스템 업그레이드에 대 한 중요 한 AD 디자인입니다. 신중하게 조정되고 결정된 주 복제본 장애 조치 프로세스에 포함된 단일 마스터 디자인을 채택했습니다.

**내결함성**

시스템은 이상 toohardware, 네트워크 및 소프트웨어 오류를 허용 하는 경우에 사용할 수 없습니다. 항상 사용 가능한 마스터 복제 존재 hello 디렉터리 파티션: hello 주 복제본입니다. 쓰기 toohello 파티션만이 복제본에서 수행 됩니다. 이 복제본이 고 지속적으로 모니터링, 고 쓰기 즉시 옮겨져 tooanother 복제 될 수 있습니다 (hello 되는 새로운 주) 오류가 검색 되는 경우. 장애 조치 중에 일반적으로 1~2분의 쓰기 가용성 손실이 발생할 수 있습니다. 이 시간 동안 읽기 가용성은 영향을 받지 않습니다.

읽기 작업 (쓰기 보다 월등히 많습니다 많은 훨씬 크기)만 toosecondary 복제 데이터베이스를 이동 합니다. 지정한 파티션에서 한 모든 복제본이 손실 쉽게 hello의 hello 읽기 tooanother 복제본을 일반적으로 보내 보정 된 보조 복제본은 idempotent 방식 이므로, 동일한 데이터 센터입니다.

**데이터 내구성**

쓰기를 지 속력 있게 커밋된 tooat 최소 두 데이터 센터 이전 tooit 인식 합니다. 이 hello, 주에 hello 쓰기를 먼저 커밋 및 다음 즉시 복제 hello 쓰기 tooat 최소 한 다른 데이터 센터에서 발생 합니다. 이렇게 하면 잠재적인 hello 데이터 센터 호스팅 hello 기본의 치명적인 손실을 데이터가 손실 되지 않습니다.

Azure AD에 0을 유지 관리 [복구 시간 목표 (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) 토큰 발급 및 디렉터리에 대 한 읽기 및 쓰기 시간 (분) (5 분) RTO 디렉터리에 대 한 hello 순서로 합니다. 또한 [복구 지점 목표(RPO)](https://en.wikipedia.org/wiki/Recovery_point_objective)를 0으로 유지하고 장애 조치에 대한 데이터는 손실되지 않습니다.

### <a name="data-centers"></a>데이터 센터

Azure AD의 복제본에 있는 hello 전세계 데이터 센터에 저장 됩니다. 자세한 내용은 [Azure 데이터 센터](https://azure.microsoft.com/en-us/overview/datacenters)를 참조하세요.

Azure AD는 다음 특성 hello로 데이터 센터에서 작동 합니다.

 * 인증, 그래프 및 기타 AD 서비스 게이트웨이 서비스 hello 뒤에 있는 합니다. hello 게이트웨이 이러한 서비스의 부하 분산을 관리 합니다. 비정상적인 서버가 트랜잭션 상태 프로브를 사용하여 감지되는 경우 자동으로 장애 조치합니다. 트래픽 toohealthy 데이터 센터는 hello 게이트웨이 동적으로 라우트 이러한 상태 검색에 따라, 합니다.
 * 에 대 한 *읽고*, hello 디렉터리에 여러 데이터 센터에서 운영 하는 활성-활성 구성에 보조 복제본과 해당 프런트 엔드 서비스를 포함 합니다. 전체 데이터 센터의 오류가 발생 한 경우 트래픽을 다른 데이터 센터에 자동으로 라우팅된 tooa 됩니다.
 *  에 대 한 *씁니다*, hello 디렉터리는 장애 조치 주 (마스터) 복제본을 통해 데이터 센터에서 계획 된 (새 주 데이터베이스는 동기화 된 tooold 기본 임) 또는 응급 장애 조치 프로시저입니다. 데이터 내구성 모든 커밋 tooat 최소 두 데이터 센터에 복제 하 여 이루어집니다.

**데이터 일관성**

hello 디렉터리 모델 결과적 일관성 중 하나입니다. 분산된 비동기적으로 복제 시스템의 한 가지 일반적인 문제는 "특정" 복제본에서 반환 된 hello 데이터 toodate를 아닐 수도 있습니다. 

Azure AD는 라우팅의 쓰기 toohello 주 복제본에서 보조 복제본을 대상으로 응용 프로그램에 대 한 읽기 / 쓰기 일관성을 제공 하 고 동기적으로 hello를 끌어오는 toohello 보조 복제본 다시 씁니다.

응용 프로그램을 선호도 tooa 디렉터리 복제본 읽기 / 쓰기 일관성을 유지 관리할 수 있도록 추상화 그래프 API Azure AD는 hello를 사용 하 여 기록 합니다. hello Azure AD 그래프 서비스에 선호도 tooa 보조 복제본이 읽기;에 사용 되는 논리적 세션을 유지 관리 분산된 캐시를 사용 하 여 그래프 서비스 캐시 hello 하는 "복제본 토큰" 선호도가 캡처됩니다. 이 토큰을 hello의 후속 작업에 대 한 사용 같은 논리적 세션입니다. 

 >[!NOTE]
 >쓰기는 즉시 복제 toohello 보조 복제본 toowhich hello 논리적 세션의 읽기를 발행 했습니다.
 >

**백업 보호**

hello 디렉터리 사용자 및 고객 실수로 삭제 발생할 경우 쉽게 복구를 위해 테 넌 트에 대 한 하드 삭제 하는 대신 소프트 삭제를 구현합니다. 실수로 테 넌 트 관리자 사용자를 삭제 하면 수 쉽게 실행 취소 하 고 삭제 하는 hello 사용자가 복원. 

Azure AD는 모든 데이터의 매일 백업을 구현하고 따라서 논리 삭제 또는 손상의 경우에 데이터를 정식으로 복원할 수 있습니다. 데이터 계층은 오류 수정 코드를 사용하므로 오류를 확인하고 특정 유형의 디스크 오류를 자동으로 수정할 수 있습니다.

**메트릭 및 모니터**

고가용성 서비스를 실행하려면 세계적 수준의 메트릭 및 모니터링 기능이 필요합니다. Azure AD는 각 서비스에 대한 주요 서비스 상태 메트릭 및 성공 조건을 지속적으로 분석하고 보고합니다. 각 Azure AD 서비스 및 모든 서비스에서 각 시나리오의 메트릭, 모니터링 및 경고를 지속적으로 개발하고 미세 조정합니다.

모든 Azure AD 서비스 예상 대로 작동 하지 않는 경우에서는 즉시 작업 toorestore 기능 최대한 빨리 합니다. 가장 중요 한 메트릭을 Azure AD 트랙 얼마나 빨리 검색 하 고 고객을 완화 하거나 수 라이브 사이트 문제는 번호입니다. 과도 하 게 모니터링 및 경고 toominimize 시간 toodetect 투자 했습니다 (TTD 대상: < 5 분) 및 운영 준비 toominimize 시간 toomitigate (TTM 대상: < 30 분)입니다.

**보안 작업**

모든 작업에 대해 감사뿐만 아니라 MFA(Multi-Factor Authentication)와 같은 운영 제어를 사용합니다. 또한 적시에 상승 시스템 toogrant 필요한 임시 액세스 모든 operational 작업-필요 시 지속적으로 사용 합니다. 자세한 내용은 참조 [신뢰할 수 있는 클라우드 hello](https://azure.microsoft.com/en-us/support/trust-center)합니다.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory 개발자 가이드](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

