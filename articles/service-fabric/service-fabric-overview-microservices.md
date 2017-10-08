---
title: "Azure에서 aaaIntroduction toomicroservices | Microsoft Docs"
description: "microservices 접근 방식으로 클라우드 응용 프로그램을 구축이 최신 응용 프로그램 개발에 대 한 중요 한 이유 및 Azure 서비스 패브릭 제공 하는 방법을 플랫폼 tooachieve이의 개요."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>이유는 microservices toobuilding 응용 프로그램에 접근?
소프트웨어 개발자로서 응용 프로그램을 구성 요소 부분으로 팩터링하는 것에 대한 생각에는 새로울 것이 없습니다. 개체 방향, 소프트웨어 추상화 및 구성 요소화 hello 중앙 패러다임은 오늘이 factorization tootake hello 형태의 클래스와 인터페이스 공유 라이브러리 및 기술 계층 간에 경향이 있습니다. 일반적으로 백엔드 스토어, 중간 계층 비즈니스 논리, 프런트엔드 사용자 인터페이스(UI)를 통한 계층화된 접근 방식을 이용합니다. 어떤 *가* 있는지, 개발자로 작성은 지난 몇 년 hello에 따른 변화 hello 클라우드에 대 한 되는 응용 프로그램을 배포 하 고 hello 비즈니스에 의해 발생 합니다.

hello 변화 하는 비즈니스 요구 됩니다.

* 작성 되 고 (예) 새 지역에서 눈금 tooreach 고객에서 작동 하는 서비스입니다.
* Agile 방법으로 기능 및 특성 toobe 수 toorespond toocustomer 수요의 더 빠른 배달 합니다.
* 향상 된 리소스 사용률 tooreduce 비용입니다.

이러한 비즈니스 요구가 응용 프로그램을 구축하는 *방식* 에 영향을 미칩니다.

Azure toomicroservices hello 방법에 대 한 자세한 내용은 [Microservices: hello 클라우드에서 제공 하는 응용 프로그램 revolution](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/)합니다.

## <a name="monolithic-vs-microservice-design-approach"></a>모놀리식과 마이크로 서비스 디자인 방법 비교
모든 응용 프로그램은 시간에 따라 진화합니다. 응용 프로그램 성공 유용한 toopeople 됨으로써 개선 합니다. 실패한 응용 프로그램은 진화하지 않고 결국은 퇴출됩니다. hello 질문이: 양을 알아 요구 사항에 대해 오늘 및 됩니다 되 hello 나중에 있습니까? 예를 들어 한 부서에 대한 보고 응용 프로그램을 빌드하고 있다고 가정해 보겠습니다. 회사의 hello 범위 내에서 hello 응용 프로그램 하 게 유지 되도록 하 고 hello 보고서는 수명이 짧은 확실 합니다. 선택 하는 방법 간에 차이가 있는, 예를 들어, 수백만 개의 고객의 비디오 콘텐츠 tootens를 제공 하는 서비스를 작성 합니다. 

경우에 따라 특정 hello 도어 작업 개념 증명으로 가져오는 hello 응용 프로그램을 나중에 재설계 수 있는지 알고 있지만 hello 구동 요소입니다. 절대 사용되지 않을 무언가를 과하게 가공하는 것은 아무런 의미가 없습니다. hello 일반적인 엔지니어링 절충 값입니다. 다른 손 hello hello 클라우드, hello 기대 하는 발생 한 증가 및 사용에 대 한 빌드에 대 한 회사와 통신 하는 경우. hello 문제는 발생 한 증가 및 소수 자릿수를 예측할 수입니다. 같은 toobe 수 tooprototype 신속 하 게 이후 성공적으로 경로 toodeal에 한다고 아는 것도 하는 중입니다. 이 hello lean 시작 방법: 빌드를 측정, 배울 수 있으며 반복 합니다.

Hello 클라이언트-서버 연대 하는 동안 각 계층에서 특정 기술을 사용 하 여 계층화 된 응용 프로그램을 구축에 toofocus를 경향을 했습니다. hello 용어 *모놀리식* 이러한 방법에 대 한 응용 프로그램 나타났습니다. hello 인터페이스 경향을 toobe hello 계층 간 및 더 밀접 하 게 결합 된 디자인 각 계층 내의 구성 요소 간에 사용 됩니다. 개발자들은 라이브러리에 컴파일되고 몇 개의 실행 파일과 DLL로 연결된 클래스를 설계하고 팩터링했습니다. 

모놀리식 디자인 방법 이점 toosuch가 됩니다. 종종 간단 toodesign 되며 (IPC) 프로세스 간 통신을 통해 이러한 호출은 경우가 많기 때문에 구성 요소 간의 더 빨리 호출을 했습니다. 또한 모든 사용자에 toobe 더 많은 사람들이 리소스가 효율적으로 단일 제품을 테스트 합니다. hello 단점은 계층화 된 레이어 간에 밀접 한 결합을를 개별 구성 요소를 확장할 수는 없습니다. 다른 사용자에 대 한 toowait 해야 tooperform 수정 또는 업그레이드를 할 경우 toofinish 사람은 테스트 합니다. 것이 더 어렵게 toobe agile 합니다.

Microservices 이러한 단점이 주소 및 더 근접 비즈니스 요구 사항, 앞에 오는 hello로 하지만 이점과 부채 합니다. hello microservices 이점은 각에 일반적으로 확장 또는 축소, 테스트, 배포 하 고 독립적으로 관리할 수 있는 간단한 비즈니스 기능을 캡슐화 합니다. 때문에 중요 한 한 마이크로 서비스 접근 방법의 중요 한 장점은 팀은 보다 비즈니스 시나리오에서 더에 의해 발생 하는 hello 계층화 된 접근 방식을 기술 합니다. 실제 상황에서 더 적은 규모의 팀이 고객 시나리오를 기반으로 마이크로 서비스를 개발하고 원하는 기술을 사용합니다. 

즉, hello 조직 toostandardize 기술 toomaintain 마이크로 서비스 응용 프로그램 필요 하지 않습니다. 개별 팀이 어떤 의미 팀 전문 지식에 따라에 대 한 통화를 하거나 가장 적합 한 toosolve hello 문제가 무엇입니까 직접 서비스를 수행할 수 있도록 합니다. 실제로 특정 NoSQL 스토어나 웹 응용 프로그램 프레임워크 등 일련의 권장 기술이 선호됩니다.

hello 단점은 microservices의 증가 하는 hello 별도 엔터티 수와 더 복잡 한 배포 및 버전 관리를 다루는 관리 됩니다. 네트워크 대기 시간을 해당 하는 hello 뿐만 아니라 hello microservices 간의 네트워크 트래픽이 증가합니다. 필요 이상으로 세밀한 서비스는 성능 문제를 야기합니다. 이러한 종속성을 보려면 도구 toohelp 없이 너무 "참조" hello 전체 시스템. 

표준 hello 마이크로 서비스 접근 방식으로 작동 확인 방법을 hello 속한 항목만의 허용 되 고 toocommunicate에서 필요한 엄격한 계약 보다는 한 서비스에 동의 하는 것입니다. 서비스에서 서로 독립적으로 업데이트 때문 hello에 이러한 계약을 디자인, 중요 한 toodefine입니다. 마이크로 서비스 접근 방식을 통한 설계와 연결된 또 다른 설명은 "세분화된 서비스 지향 아키텍처(SOA)"입니다.

***가장 간단한 hello microservices 디자인 방법은 독립 변경 tooeach 및 합의 표준을 사용 하 여 통신을 위해 서비스의 분리 된 페더레이션에 대 한 합니다.***

사용자는 사실을 발견 더 많은 클라우드 앱을 생산 되는 대로이 분해의 전반적인 hello 독립적이 고 시나리오에 중점을 둔 서비스로 응용 프로그램은 더 우수한 장기 접근 방식입니다.

## <a name="comparison-between-application-development-approaches"></a>응용 프로그램 개발 접근 방식 비교
![서비스 패브릭 플랫폼 응용 프로그램 개발][Image1]

1) 모놀리식 앱은 도메인 특정 기능을 포함하며 일반적으로 웹, 비즈니스, 데이터 등의 기능 계층으로 구분됩니다.

2) 모놀리식 앱은 여러 서버/가상 컴퓨터/컨테이너에 복제하여 확장합니다.

3) 마이크로 서비스 응용 프로그램은 기능을 더 작은 개별 서비스로 구분합니다.

4) hello microservices 접근 방식을 눈금으로 배포 하 여 각 서비스 하지 독립적으로 서버/가상 컴퓨터에서 이러한 서비스의 인스턴스를 만드는/컨테이너입니다.

마이크로 서비스를 사용 하 여 디자인 방법은 모든 프로젝트에 대 한 통치 하지 않습니다. 하지만 앞에서 설명한 hello 비즈니스 목표와 더욱 긴밀 하 게 정렬지 않습니다. 모놀리식 접근 방식으로 시작 하는 것은 microservices 디자인에 나중에 hello 기회 toorework hello 코드 해야 알고 있는 경우 사용할 수 있습니다. 더 일반적으로 모놀리식 응용 프로그램으로 시작 하 고 느린 나누십시오 단계별로 더 scalable 또는 agile toobe를 필요로 하는 기능 영역 hello로 시작 합니다.

toosummarize, hello 마이크로 서비스 방법은 toocompose 응용 프로그램의 많은 작은 서비스입니다. hello 서비스 컴퓨터의 클러스터 전체에서 배포 되는 컨테이너에서 실행 됩니다. 소규모 팀은 시나리오에 대 한 서비스를 개발 하 고 독립적으로 버전을 테스트 하지, 배포 및 hello 전체 응용 프로그램을 개발할 수 있도록 각 서비스의 크기를 조정 합니다.

## <a name="what-is-a-microservice"></a>마이크로 서비스란?
마이크로 서비스에 대한 정의는 여러 가지가 있습니다. Hello 인터넷을 검색 하는 경우 자신의 관점 및 정의 제공 하는 유용한 많은 리소스를 찾을 수 있습니다. 그러나 대부분의 hello microservices의 특성에 따라 광범위 하 게 합의:

* 고객 또는 비즈니스 시나리오를 캡슐화합니다. 해결 중인 hello 문제가 무엇입니까?
* 소규모 엔지니어링 팀에서 개발합니다.
* 어느 프로그래밍 언어로나 작성되고 모든 프레임워크에 사용합니다.
* 개별적으로 버전 관리, 배포 및 확장되는 코드 및 상태(필요한 경우)로 구성됩니다.
* 잘 정의된 인터페이스와 프로토콜을 통해 타 마이크로 서비스와 상호 작용합니다.
* 사용 되는 고유 이름 (Url) tooresolve 위치로 있어야 합니다.
* 일관 되 고 오류의 hello 현재 상태에서 사용할 수 있는 상태로 유지 합니다.

이러한 특징을 다음으로 요약할 수 있습니다.

***마이크로 서비스 응용 프로그램은 독립적으로 버전 관리되며 확장성 있는 소규모 고객 중심 서비스로 구성됩니다. 이 서비스들은 잘 정의된 인터페이스가 있는 표준 프로토콜을 통해 서로 통신합니다.***

Hello 섹션 앞의 처음 두 점은 hello 다룬 하 고 이제 확장 하 고 명확 하 게 hello 다른 키를 누릅니다.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>어느 프로그래밍 언어로나 작성되고 모든 프레임워크에 사용합니다.
개발자, 우리는 무료 toochoose 우리의 기술 또는 hello 서비스의 hello 요구에 따라 원하는 언어 또는 프레임 워크 것입니다. 일부 서비스에서 다른 모든 c + +의 성능 이점을 hello 값 수 있습니다. 다른 서비스에서는 C# 또는 Java에서 관리 되는 개발의 hello 용이성 가장 중요할 수 있습니다. 경우에 따라 데이터 저장소 기술을 toouse 특정 파트너 라이브러리를 할 수 있습니다 또는 수단 제공을 서비스 tooclients hello 합니다.

기술을 선택한 후 operational toohello 또는 수명 주기 관리 및 hello 서비스의 크기 조정을 제공 됩니다.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>배포 하 고 크기가 조정 코드와 상태 toobe 독립적으로 버전이 지정 허용
하지만 Microservices, hello 코드 및 필요에 따라 hello 상태 toowrite 선택 해야 독립적으로 배포, 업그레이드 및 크기를 조정 합니다. 실제로 hello 어렵게 하는 문제 toosolve 중 하나 때문에 이것이 tooyour 선택 하는 기술 두어야 합니다. 크기 조정, 어떻게 toopartition (또는 분할) 둘 다 hello 코드와 상태를 이해는 어려운입니다. Hello 코드와 상태는 오늘, 별도 기술을 사용할 때 프로그램 마이크로 서비스에 대 한 hello 배포 스크립트 toobe 수 toocope로 확장을 모두 필요. 이것은 또한 민첩성 및 유연성을 있으므로 tooupgrade 필요 없이 hello microservices 중 일부를 업그레이드할 수 있습니다 이러한 작업을 한 번에 모든 합니다.

잠시 동안 마이크로 서비스 접근 방식 비교 모놀리식 toohello 반환, hello 다음 다이어그램 차이점을 보여 줍니다 hello hello 접근 방식 toostoring 상태에 있습니다.

#### <a name="state-storage-between-application-styles"></a>응용 프로그램 스타일 간의 상태 저장
![서비스 패브릭 플랫폼 상태 저장][Image2]

***hello 왼쪽에 hello 모놀리식 방법에는 단일 데이터베이스와 계층의 특정 기술에 있습니다.***

***hello 오른쪽에 hello microservices 방법에는 상호 연결 된 microservices 다양 한 기술을 사용 하 고 있는 상태는 일반적으로 범위가 지정 된 toohello 마이크로 서비스에 대 한 그래프.***

일반적으로 모놀리식 방식으로 hello 응용이 단일 데이터베이스를 사용합니다. hello 장점은 단일 위치를 쉽게 toodeploy 하므로 된다는 점입니다. 각 구성 요소는 단일 테이블 toostore 상태로 있을 수 있습니다. 팀은 challenge 되 toostrictly 별도 상태와 해야 합니다. 필연적으로 되지 temptations tooadd 새 열 tooan 기존 고객 테이블, 테이블 간의 조인 작업을 수행할 수 있으며 hello 저장소 계층에서 종속성을 만듭니다. 이러한 경우가 발생하면, 개별 구성 요소를 확장할 수 없습니다. 

Hello microservices 방법에서는 각 서비스를 관리 하 고 자체의 상태를 저장 합니다. 각 서비스는 hello 서비스의 코드와 상태를 모두 함께 toomeet hello 요구 크기를 조정 해야 합니다. 한 가지 단점이 하는 경우에 필요 toocreate 뷰 또는 쿼리, 응용 프로그램의 데이터의 서로 다른 상태 저장소 tooquery 필요 합니다. 일반적으로 이 문제는 마이크로 서비스의 컬렉션에 걸쳐 뷰를 구축하는 개별 마이크로 서비스를 갖춤으로써 해결할 수 있습니다. Hello 데이터에 여러 개의 임시 쿼리 tooperform 해야 할 경우 각 마이크로 서비스 오프 라인 분석을 위해 데이터 tooa 데이터 웨어하우징 서비스 작성을 고려해 야 합니다.

버전 관리는 한 마이크로 서비스의 배포 된 특정 toohello 버전 여러 하므로, 배포 하 고 함께 실행 하는 다양 한 버전입니다. 버전 관리는 마이크로 서비스의 최신 버전 업그레이드 하는 동안 오류가 발생 하 고 필요한 tooroll 백 tooan hello 시나리오에서는 이전 버전입니다. hello 버전 관리에 대 한 다른 시나리오에서 수행 중인 A/B-스타일 테스트, 여기서는 다른 사용자가 경험 hello 서비스의 여러 버전. 예를 들어, 공개 전에 더 광범위 하 게 일반적인 tooupgrade 특정 고객 tootest 새로운 기능 집합에 대 한 마이크로 서비스입니다. Microservices의 수명 주기 관리, 후이 구문은 이제 더 광범위 toocommunication 사이입니다.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>잘 정의된 인터페이스와 프로토콜을 통해 타 마이크로 서비스와 상호 작용
이 항목 지난 10 년 동안 hello를 통해 게시 한 서비스 지향 아키텍처에 대 한 광범위 한 홍보 자료 통신 패턴을 설명 하기 때문에 거의 관심이 여기에서 필요 합니다. 일반적으로 서비스 통신 방법을 사용 하 여는 REST를 HTTP 및 TCP 프로토콜 및 XML 또는 JSON hello serialization 형식으로. 인터페이스의 관점에서 hello 웹 디자인 방법 수용 하는 방법에 대 한 됩니다. 그러나 바이너리 프로토콜이나 자체 데이터 형식을 사용하지 않을 이유는 없습니다. 준비 사람 toohave 어려워지므로 공개적으로 사용할 수 있는 경우 프로그램 microservices를 사용 하 여 합니다.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>고유 이름 (URL)에 해당 위치를 tooresolve 사용
어떻게 म 유지 이라는 hello 마이크로 서비스 접근 방식을 hello 웹 같은 기억? 처럼 hello 웹 프로그램 마이크로 서비스 필요 toobe 주소 지정 가능한 때마다 실행 되 고 합니다. 컴퓨터 및 특정 마이크로 서비스를 실행할 컴퓨터에 대해 고려하면 급격한 문제가 발생합니다. 

특정 URL tooa 특정 컴퓨터를 동일한 방식으로 DNS 확인 hello, 현재 위치를 검색할 수 있도록 toohave 고유한 이름을 프로그램 마이크로 서비스에 필요 합니다. Microservices는 hello 인프라에서 실행 되는 별개는 주소 지정 가능 이름이 필요 합니다. 이 때문에 서비스의 배포 방법을 검색 방법을 사이의 상호 작용 임을 의미 toobe 서비스 레지스트리 필요 합니다. 마찬가지로, 한 컴퓨터에서 오류가 발생 hello 레지스트리 서비스가 해야 등에 대 한 이제 hello 서비스가 실행 됩니다. 

제기 toohello 다음 항목: 복원 력과 일관성을 유지 합니다.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>일관 되 고 오류의 hello 현재 상태에서 사용할 수 있는 상태로 유지 됩니다.
예기치 않은 오류를 처리 하는 분산된 시스템에서 특히 hello 가장 어려운 문제 toosolve, 중 하나입니다. 개발자로 작성 하는 hello 코드의 대부분은 예외 처리, 및에이 hello 대부분 시간이 소요 된 위치에서 테스트 합니다. hello 문제는 toohandle 오류 코드를 작성 보다 훨씬 복잡 합니다. Hello hello 마이크로 서비스 실행 중인 시스템에 실패 하면 어떻게 되나요? 뿐만 아니라 않습니다 toodetect이 마이크로 서비스 오류 (자체적으로 하드 문제)을 필요는 없지만 대상이 필요 하기 toorestart 프로그램 마이크로 서비스입니다. 

마이크로 서비스는 toobe 탄력적인 toofailures 되어야 하며 가용성 이유로 다른 컴퓨터에서 자주 다시 시작 합니다. 이 다운 toohello 저장 된 상태를 hello 마이크로 서비스를 대신 하 여 hello 마이크로 서비스에서이 상태를 복구할 수와 인지 hello 마이크로 서비스 수 toorestart 성공적으로 제공 됩니다. 즉, hello 계산 (hello 프로세스 다시 시작)에 toobe 복원 력을 부여할 뿐만 아니라 hello 상태 또는 데이터 (데이터 손실 및 hello 데이터가 없는 일관성 유지)에 복원 력을 부여할 필요 합니다.

복원 력 hello 문제가 응용 프로그램 업그레이드를 사용 하는 동안 오류가 발생할 때와 같은 다른 시나리오 중 중요 합니다. hello hello 배포 시스템을 사용 하는 마이크로 서비스 필요 하지 않은 toorecover 합니다. 또한 toothen 필요한 toomove 정방향 toohello 최신 버전을 계속 하거나 대신 롤백 이전 버전 toomaintain tooa 일관성 있는 상태로 수 있는지 여부를 결정 합니다. 와 같은 만큼 충분 한 컴퓨터가 되는지 앞으로 이동 하는 사용 가능한 tookeep 및 hello 마이크로 서비스의 이전 버전 toorecover toobe 것으로 간주 해야 하는 방법을 질문 합니다. 이렇게 하려면 hello 마이크로 서비스 tooemit 상태 정보 toobe 수 toomake 이러한 결정 합니다.

### <a name="reports-health-and-diagnostics"></a>보고서 상태 및 진단
당연하지만 자주 간과되는 것으로, 마이크로 서비스는 자신의 상태와 진단을 보고하는 것이 필수적입니다. 보고가 없으면 운영의 견지에서는 정보가 거의 없습니다. 독립 서비스 및 시스템 클록 스큐 toomake 감각 hello 이벤트 순서는 것은 어려울 처리의 조합에 대해 진단 이벤트를 상호 연결 합니다. Hello에서 같은 방식으로 합의 프로토콜 및 데이터에 대 한 마이크로 서비스 상호 작용 하는 형식, 쿼리 및 보기를 위한 toolog 상태 및 진단 이벤트는 결국에 이벤트를 저장 하는 방법에 대 한 표준화에 대 한 요구가 있습니다 시나리오입니다. 마이크로 서비스 접근 방식에서는 여러 팀이 단일 로깅 형식에 동의하는 것이 중요합니다. Hello 응용 프로그램 전체에서에서 일관적인 접근 방식을 tooviewing 진단 이벤트 toobe 필요합니다.

상태는 진단과 다릅니다. 현재 상태 tootake 적절 한 조치를 보고 하는 hello 마이크로 서비스에 대 한 상태가입니다. 좋은 예로 업그레이드 및 배포 메커니즘 toomaintain 가용성과 함께 작동 합니다. 서비스 tooa 프로세스 크래시 인해 현재 정상 상태가 되었거나 컴퓨터 다시 부팅, 있지만 hello 서비스 작동 중일 수 있습니다. hello 필요한 것 toomake이이 나빠지는 업그레이드를 수행 하면 됩니다. hello 가장 좋은 방법은 toodo 조사 먼저 또는 마이크로 서비스 toorecover hello에 대 한 시간을 허용 합니다. 마이크로 서비스의 상태 이벤트를 통해 정보에 입각한 의사 결정을 내리고 효과적인 자체 복구 서비스를 만들 수 있습니다.

## <a name="service-fabric-as-a-microservices-platform"></a>마이크로 서비스 플랫폼으로서의 서비스 패브릭
Azure 서비스 패브릭에서 Microsoft에서 전환 된 스타일에서 toodelivering 서비스 일반적으로 모놀리식 상자 제품을 제공 하지 못할 분명해졌습니다. 구축 및 작동 하는 큰 서비스와 Azure SQL 데이터베이스 및 Azure Cosmos DB 모양 서비스 패브릭 같은 hello 경험 합니다. hello 플랫폼 발전 함에 따라 시간이 지남에 따라 점점 더 많은 서비스 채택으로 합니다. 중요 한 사실은 Azure에서 뿐만 아니라 Windows 서버 배포의 독립 실행형 서비스 패브릭 toorun 해야 했습니다.

***서비스 패브릭의 hello 목표 toosolve 빌드 및 실행 하는 서비스의 hello 어려운 문제 이며 팀 microservices 방식을 사용 하 여 비즈니스 문제를 해결할 수 있도록 인프라 리소스를 효율적으로 활용 합니다.***

서비스 패브릭 제공 세 가지 넓은 영역 toohelp microservices 접근 방식을 사용 하는 응용 프로그램 빌드:

* 시스템 서비스 toodeploy 제공 하는 플랫폼 업그레이드, 검색 및 실패 한 서비스를 다시 시작, 서비스 검색, 메시지를 라우팅할 상태를 관리 및 상태를 모니터링 합니다. 이러한 시스템 서비스를 통해 앞에서 설명한 microservices의 hello 특징을 많이 적용 합니다.
* 기능 toodeploy 응용 프로그램으로 또는 컨테이너에서 실행 중 하나를 처리합니다. Service Fabric은 컨테이너 및 프로세스 조정자입니다.
* 생산적인 프로그래밍 Api microservices로 응용 프로그램을 빌드할 toohelp: [ASP.NET Core, Reliable Actors 및 신뢰할 수 있는 서비스](service-fabric-choose-framework.md)합니다. 모든 코드 toobuild 프로그램 마이크로 서비스를 선택할 수 있습니다. 하지만 이러한 Api hello 작업을 더 간단 하 게 확인 하 고 좀 더 깊게 hello 플랫폼에 통합 합니다. 예를 들어, 상태 및 진단 정보를 받거나 기본 제공되는 고가용성을 활용할 수 있습니다.

***Service Fabric은 서비스를 구축한 방법과 무관하며 어느 기술이나 사용할 수 있습니다. 그러나 toobuild microservices 더 쉽게 확인 하는 기본 제공 프로그래밍 Api 제공지 않습니다.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>기존 응용 프로그램 tooService 패브릭 마이그레이션
키 방법을 tooService 패브릭은 tooreuse 기존 코드와 새 microservices 현대화 된 수입니다. 5 단계 tooapplication 현대화 있으며 시작 하 고 hello 단계에서 중지할 수 있습니다. 이 단계는 다음과 같습니다.

1) 기존의 모놀리식 응용 프로그램 선택
2) 리프트 하 고 이동-서비스 패브릭에서 컨테이너 또는 게스트 실행 파일 toohost 기존 코드를 사용 합니다.
3) 현대화 - 컨테이너화된 기존 코드와 함께 새 마이크로 서비스가 추가되었습니다. 
4) 혁신-분해 합니다. hello 모놀리식 microservices 요구에 따라 순수 하 게 합니다.
5) Microservices-새 최적의 응용 프로그램을 구축 또는 기존 모놀리식 응용 프로그램의 hello 변환으로 변환 합니다.

![마이그레이션 tooMicroservices][Image3]

중요 한 tooemphasis 다시 설정할 수 있는 것이 **시작 하 고 위의 모든이 단계에서 중지**, 없는 toomoved toohello 다음 단계를 강요 합니다. 이제 이러한 각 단계에 대한 예제를 살펴보겠습니다.

**이동할** -많은 수의 회사는 아니며 해지 하 고 기존 모놀리식 응용 프로그램 컨테이너 toofor로 변화 하는 원인은 두;

- Tooconsolidation 및 더 높은 밀도에 기존 하드웨어 또는 실행 중인 응용 프로그램의 제거로 인해 비용된 절감. 
- 개발 및 운영 간의 일관된 배포 계약

비용된 절감 이해할 수 있으며 기존 응용 프로그램의 많은 되는 Microsoft에서 단순히 toomillions 달러의 컨테이너 화 된 합니다. 일관 된 배포는 동일 하 게 중요 하지만 쉽다는 점 tooevaluate 합니다. 개발자가 할 수 표시 가능한 toochoose hello 기술 해당 도구 모음을 수 있지만 hello 작업은 페이로드만 단 하나의 방식은 toodeploy를 허용 하 고 이러한 응용 프로그램을 관리 합니다. Toodeal hello 복잡 한 다양 한 기술 사용 하는 것과 작업 hello를 완화 하거나 특정 구성을 선택 개발자 tooonly 강제 적용 합니다. 기본적으로 모든 응용 프로그램은 자체 포함된 배포 이미지에 컨테이너화됩니다.

대부분의 조직에서는 여기까지만 수행합니다. 컨테이너의 hello 이점이 이미 있는 및 서비스 패브릭 배포, 업그레이드, 버전 관리, 롤백, 상태 모니터링 등의 hello 전체 관리 환경을 제공 합니다.

**현대화** -는 컨테이너 화 된 기존 코드와 함께 새 서비스의 hello 추가 합니다. Toowrite 새 코드를 사용 하도록 하려는 경우 hello microservices 경로 아래의 최상의 toodecide tootake 작은 단계입니다. 그러면 새 REST API 끝점 또는 새로운 비즈니스 논리를 추가할 수 있습니다. 이러한 방식으로 새 microservices 건물 및 개발 및 배포 연습 여행 hello에서 시작 하면 합니다.

**혁신** -이러한 원래 변화 비즈니스 요구가 문서의 hello 시작 시 hello microservices 접근 방식에 영향을 주는 기억? 이 단계 hello에 의사 결정은, 이러한 상황이 발생 toomy 현재 응용 프로그램은 및 toostart hello monolith 분할 하거나 혁신 그렇다면 싶습니다. 여기에 있는 예제는 데이터베이스가 워크플로 큐로 사용되어 병목 상태를 처리 중인 경우입니다. Hello hello 증가 하는 워크플로 요청 수로 눈금에 대 한 분산 요구 toobe를 작동 합니다. 따라서 크기 조정이 아니라는 hello 응용 프로그램의 해당 특정 부분에 있어야 tooupdate 더 자주는 마이크로 서비스를 분할이 out 시키고 혁신 하도록 돕습니다. 

**마이크로 서비스로 변환** - 응용 프로그램이 마이크로 서비스로 완벽하게 구성(또는 분리)된 경우입니다. 여기에 tooreach hello microservices 여행을 했습니다. 시작할 수 있습니다 여기서 toodo 하지만이 microservices 플랫폼 toohelp 없이 상당한 투자가 없는지 확인 합니다. 

### <a name="are-microservices-right-for-my-application"></a>마이크로 서비스가 내 응용 프로그램에 적합할까요?
아마도 그렇습니다. Microsoft에서 점점 더 많은 팀 toobuild 업무 용도 대 한 hello 클라우드에 대 한 시작으로 그 중 대부분 실현 마이크로 서비스와 비슷한 접근 방식을 활용 하는 hello에서 발생 했습니다. 예를 들어, Bing은 수년 동안 검색에서 마이크로 서비스를 개발하고 있습니다. 다른 팀에 대 한 hello microservices 접근 방식은 새로운 이었습니다. 팀 강도의 자신의 핵심 영역 외부 어려운 문제 toosolve 했음을 발견 합니다. 이 때문에 서비스 패브릭 서비스를 구축 하기 위한 선택 항목의 hello 기술로 계속 해 서 기반을 획득 합니다.

서비스 패브릭의 hello 목표는 마이크로 서비스 접근 방식으로 응용 프로그램 구축 tooreduce hello 복잡성을 많은 비용이 많이 드는 다시 디자인으로 통해 toogo 보유 하지 않습니다. 작은 항목부터 시작, 필요한 경우 크기를 조정, 서비스 사용 안 함, 새 값을 추가 및 발전 고객 사용량은 hello 접근 방식입니다. 또한 toobe 대부분 개발자를 위한 보다 쉽게 수행할 toomake microservices 해결 아직 많은 다른 문제가 있는 알고 있습니다. 컨테이너 및 hello 행위자 프로그래밍 모델은 해당 방향에 작은 단계 예 있고 함수 우리는 더 많은 혁신으로 인해 나옵니다 toomake이 더 쉽습니다.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>다음 단계
* [서비스 패브릭 용어 개요](service-fabric-technical-overview.md)
* [Microservices:는 응용 프로그램 revolution hello 클라우드 기반의](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
