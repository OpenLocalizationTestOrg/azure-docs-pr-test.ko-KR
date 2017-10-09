---
title: "다중 테 넌 트 SaaS 응용 프로그램 및 Azure SQL 데이터베이스에 대 한 aaaDesign 패턴 | Microsoft Docs"
description: "이 문서에서는 hello 요구 사항 및 클라우드 환경에서 실행 되는 다중 테 넌 트 데이터베이스 응용 프로그램의 일반적인 데이터 아키텍처 패턴 tooconsider 필요 하며 이러한 패턴와 관련 된 다양 한 장단점 hello 합니다. 그리고 Azure SQL Database가 탄력적 풀 및 탄력적 도구를 통해 다른 기능도 동일하게 제공하면서 이러한 요구 사항의 처리를 지원하는 방법도 설명합니다."
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>다중 테넌트 SaaS 응용 프로그램 및 Azure SQL Database에 대한 디자인 패턴
이 문서에서는 클라우드 환경에서 실행 되는 saas () 데이터베이스 응용 프로그램으로 hello 요구 사항 및 다중 테 넌 트 소프트웨어의 일반적인 데이터 아키텍처 패턴에 대해 알 수 있습니다. 또한 tooconsider 필요 하 고 다양 한 디자인 패턴의 장단점을 hello hello 요소에 설명 합니다. Azure SQL Database의 탄력적 풀 및 탄력적 도구를 사용하면 다른 목표도 달성하면서 특정 요구 사항을 충족할 수 있습니다.

경우에 따라 개발자가 다중 테 넌 트 응용 프로그램의 데이터 계층 hello에 대 한 테 넌 트 모델을 디자인할 때 장기 이익을 대해 작동 하는 선택 항목을 확인 합니다. 처음에 적어도 개발자 수 바뀌고 간편한 개발 및 응용 프로그램의 테 넌 트 격리 또는 hello 확장성 보다 더 중요 한으로 클라우드 서비스 공급자 비용 절감 합니다. 나중에이 선택은 toocustomer 만족도 사항과 비용이 많이 드는 과정 수정 될 수 있습니다.

다중 테 넌 트 응용 프로그램은 클라우드 환경에서 호스팅되는 응용 프로그램 및 서비스 toohundreds 또는 수천 개의 공유 하지 않거나 다른 사용자의 데이터를 볼 수 있는 테 넌 트가 집합이 동일한 hello를 제공 하는 합니다. 예로 서비스 tootenants 클라우드 호스팅 환경에서 제공 하는 SaaS 응용 프로그램.

## <a name="multi-tenant-applications"></a>다중 테넌트 응용 프로그램
다중 테넌트 응용 프로그램에서는 데이터 및 워크로드를 쉽게 분할할 수 있습니다. 분할할 수 있습니다 데이터 및 작업, 예를 들어 테 넌 트 경계에 따라 테 넌 트의 hello 범위 내에서 대부분의 요청 발생 하기 때문에. 해당 속성을 hello 데이터 및 hello 작업 부하에 내재 된 하 고이 문서에서 설명 하는 hello 응용 프로그램 패턴을 우선 합니다.

개발자는 이러한 유형의 응용 프로그램을 사용 하 여 클라우드 기반 응용 프로그램을 포함 하 여 hello 전체 스펙트럼에서:

* SaaS 응용 프로그램으로 클라우드 전환된 toohello 되는 파트너 데이터베이스 응용 프로그램
* Hello 접지에서 hello 클라우드 용으로 작성 된 SaaS 응용 프로그램
* 직접 고객에게 표시되는 응용 프로그램
* 직원이 접하는 엔터프라이즈 응용 프로그램

파트너 데이터베이스 응용 프로그램은 일반적으로 다중 테 넌 트 응용 프로그램은 루트와 hello 클라우드 권한과 위해 디자인 된 SaaS 응용 프로그램입니다. 이러한 SaaS 응용 프로그램 서비스 tootheir 테 넌 트 특수화 된 소프트웨어 응용 프로그램을 제공합니다. 테 넌 트 hello 응용 프로그램 서비스를 액세스 하 고 hello 응용 프로그램의 일부로 저장 하는 연결 된 데이터의 완전 한 소유권을 가질 수 있습니다. 하지만 tootake SaaS, 테 넌 트의 hello 이점 활용 하는 자신의 데이터를 일부 제어 항복 해야 합니다. 해당 데이터를 안전 하 고 다른 테 넌 트의 데이터에서 격리 hello SaaS 서비스 공급자 tookeep을 신뢰합니다. 이러한 종류의 다중 테넌트 SaaS 응용 프로그램의 예로 MYOB, SnelStart 및 Salesforce.com이 있습니다. 이러한 응용 프로그램의 각 테 넌 트 경계 및이 문서에서 설명 하는 지원 hello 응용 프로그램 디자인 패턴을 따라 분할할 수 있습니다.

직접 서비스 toocustomers 또는 tooemployees (자주 참조 tooas 사용자 보다는 테 넌 트)는 조직 내에서 제공 하는 응용 프로그램은 hello 다중 테 넌 트 응용 프로그램 스펙트럼에서 다른 범주입니다. 고객은 toohello 서비스를 구독 하 고 수집 하 고 저장 하는 서비스 공급자 hello hello 데이터를 소유 하지 않습니다. 서비스 공급자는 덜 엄격한 요구 사항을 tookeep 정부 위임 개인 정보 보호 규정을 벗어나는 서로 격리 하는 고객 데이터는 합니다. 이러한 종류의 고객에게 표시되는 다중 테넌트 응용 프로그램의 예로 Netflix, Spotify 및 Xbox LIVE 같은 미디어 콘텐츠 공급자가 있습니다. 쉽게 분할이 가능한 응용 프로그램의 다른 예로는 고객에게 표시되는 인터넷 규모 응용 프로그램이나, 각 고객 또는 장치가 파티션 역할을 할 수 있는 IoT(사물 인터넷) 응용 프로그램이 있습니다. 파티션 경계를 통해 사용자와 장치를 분리할 수 있습니다.

응용 프로그램이 테넌트, 고객, 사용자 또는 장치 같은 단일 속성에 따라 쉽게 분할되지 않는 경우도 있습니다. 예를 들어 복잡한 전사적 자원 관리(ERP) 응용 프로그램은 제품, 주문 및 고객을 포함합니다. 이러한 응용 프로그램은 일반적으로 매우 복잡하게 상호 연결된 테이블을 수천 개 포함하는 복잡한 스키마를 가지고 있습니다.

없는 단일 파티션 전략 tooall 테이블을 적용 하 고 응용 프로그램의 작업에서 사용할 수 있습니다. 이 문서는 쉽게 분할이 가능한 데이터 및 워크로드를 포함한 다중 테넌트 응용 프로그램에 초점을 맞춥니다.

## <a name="multi-tenant-application-design-trade-offs"></a>다중 테넌트 응용 프로그램 디자인의 장단점
다중 테 넌 트 응용 프로그램 개발자가 일반적으로 선택 하는 hello 디자인 패턴 hello 요소 다음의 고려 사항일 뿐를 기반으로 합니다.

* **테넌트 격리**. hello 개발자 tooensure 테 넌 트에 원치 않는 액세스 tooother 테 넌 트의 데이터가 있는지 필요 합니다. hello 격리 요구 사항을 시끄러운 이웃에서 보호를 제공, 수 toorestore 테 넌 트의 데이터 되 고, 테 넌 트 관련 사용자 지정 구현 등 tooother 속성을 확장 합니다.
* **클라우드 리소스 비용**. SaaS 응용 프로그램 비용 경쟁 toobe가 필요합니다. 다중 테 넌 트 응용 프로그램 개발자 hello 저장소와 같은 클라우드 리소스 사용에서 toooptimize 저렴 한 비용에 대 한를 선택 하 고 비용을 계산 될 수 있습니다.
* **DevOps 편의성**. 다중 테 넌 트 응용 프로그램 개발자 tooincorporate 격리 보호가 필요한, 유지 및 해당 응용 프로그램 및 데이터베이스 스키마의 hello 상태를 모니터링 하 고, 테 넌 트 문제를 해결 합니다. 복잡 한 응용 프로그램 개발 및 운영 tooincreased 비용 직접 변환 및 테 넌 트 만족도와 문제를 제기 합니다.
* **확장성**. hello 기능 tooincrementally 테 넌 트 및 명령적 tooa 성공 SaaS 작업 필요로 하는 테 넌 트에 대 한 용량을 추가 합니다.

이러한 각 요인의 척도로 상대적 비교 tooanother에 있습니다. hello 최저 비용 클라우드 hello 가장 편리 하 게 개발 환경을 제공 하지 못하는 제공 합니다. 이 개발자에 대 한 중요 toomake hello 응용 프로그램 디자인 프로세스 중 이러한 옵션과 해당 장단점이 대 한 선택 항목 정보입니다.

일반적인 개발 패턴은 toopack 하나 또는 몇 가지 데이터베이스에 여러 테 넌 트입니다. hello이 방식의 이점은 저렴 한 비용 몇 가지 데이터베이스 및 제한 된 수의 데이터베이스 작업의 비교적 간단 hello에 대 한 지불 하기 때문에 있습니다. 하지만 시간이 지남에 따라 SaaS 다중 테넌트 응용 프로그램 개발자는 이 선택이 테넌트 격리 및 확장성 면에서 상당한 단점이 있다는 것을 깨닫게 됩니다. 테 넌 트 격리가 중요 해지면 추가 작업이 필요한 tooprotect 테 넌 트 데이터에에서 경우 무단으로 액세스 또는 시끄러운 이웃 공유 저장소 이러한 추가 작업으로 인해 개발 작업 및 격리 유지 관리 비용이 대폭 증가할 수 있습니다. 마찬가지로, 테 넌 트 추가 필요한 경우이 디자인 패턴 전문 지식을 tooredistribute 테 넌 트 데이터 데이터베이스 tooproperly 눈금 hello 데이터 계층 응용 프로그램에서 일반적으로 필요 합니다.  

테 넌 트 격리를 종종은 toobusinesses 및 조직에 제공 하는 SaaS 다중 테 넌 트 응용 프로그램의 기본 요구 사항입니다. 개발자들은 테넌트 격리 및 확장성보다 단순성과 비용에서 인지된 장점의 유혹에 넘어갈 수도 있습니다. 이 따른이 결과 증명할 수 복잡 하 고 비용이 많이 드는 hello 서비스 증가 하 고 테 넌 트 격리 요구 사항은 더욱 중요 하 고 hello 응용 프로그램 계층에서 관리 되는 합니다. 그러나 테 넌 트 격리 직접적으로 소비자 용 서비스 toocustomers 제공 하는 다중 테 넌 트 응용 프로그램에서 클라우드 리소스 비용을 최적화 하는 보다 우선 순위가 낮은 수 있습니다.

## <a name="multi-tenant-data-models"></a>다중 테넌트 데이터 모델
테넌트 데이터 배치에 대한 일반적인 디자인 방식은 그림 1과 같은 세 가지로 구분되는 모델을 따릅니다.

![다중 테넌트 응용 프로그램 데이터 모델](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

그림 1: 다중 테넌트 데이터 모델에 대한 일반적인 디자인 방식

* **테넌트별 데이터베이스**. 각 테넌트가 자기만의 데이터베이스를 가지고 있습니다. 모든 테 넌 트 관련 데이터는 예외일된 toohello 테 넌 트의 데이터베이스와 다른 테 넌 트 및 해당 멤버 데이터에서 격리 합니다.
* **공유 데이터베이스-분할**. 여러 테넌트가 여러 데이터베이스 중 하나를 공유합니다. 테 넌 트의 고유 집합 해시, 범위 또는 목록 분할 같은 분할 전략을 사용 하 여 tooeach 데이터베이스를 할당 됩니다. 이 데이터 배포 전략에는 자주 참조 tooas 분할은입니다.
* **공유 데이터베이스-단일**. 때로는 큰 단일 데이터베이스는 테넌트 ID 열에서 명확하게 구분되는 모든 테넌트를 위한 데이터를 포함합니다.

> [!NOTE]
> 응용 프로그램 개발자는 서로 다른 데이터베이스 스키마의 tooplace 다른 테 넌 트를 선택 하 고 hello 스키마 이름 toodisambiguate hello 다른 테 넌 트를 사용 하 여 수 있습니다. 권장 하지는 않습니다이 방법을 사용 하므로 일반적으로 동적 SQL의 hello 사용 해야 하 고 계획을 캐시에 적용 되지 않습니다. 이 문서의 나머지 부분을 hello, 다중 테 넌 트 응용 프로그램의이 범주에 대 한 공유 hello 테이블 접근 방식을 집중 합니다.
> 
> 

## <a name="popular-multi-tenant-data-models"></a>인기 있는 다중 테넌트 데이터 모델
이 hello 응용 프로그램 디자인 상충 관계 이미 확인 되었습니다 측면에서 다중 테 넌 트 데이터 모델의 중요 한 tooevaluate hello 다른 형식입니다. 이러한 요소 앞에서 설명한 hello 3 가장 일반적인 다중 테 넌 트 데이터 모델 및 해당 데이터베이스 사용량 그림 2에 나와 있는 것 처럼 특징을 결정 하는 데 도움이 됩니다.

* **격리**. 테 넌 트 간에 격리 수준을 hello 위해 데이터 모델에서는 얼마나 많은 테 넌 트 격리를 측정 될 수 있습니다.
* **클라우드 리소스 비용**. 테 넌 트 간에 공유 되는 리소스의 hello 양에 클라우드 리소스 비용을 최적화할 수 있습니다. Hello 계산 및 저장소 비용으로 리소스를 정의할 수 있습니다.
* **DevOps 비용**. 응용 프로그램 개발, 배포 및 관리가 매우 쉽습니다 hello 전체 SaaS 운영 비용을 줄입니다.  

그림 2 hello Y 축은 hello 수준을 테 넌 트 격리를 나타냅니다. hello X 축에는 리소스를 공유 hello 수준을 표시 합니다. hello 회색 대각선 hello 가운데에 화살표가의 DevOps 비용을 높이 거 나 낮춥니다 tooincrease 맞춤형 hello 방향입니다.

![인기 있는 다중 테넌트 응용 프로그램 디자인 패턴](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

그림 2: 인기 있는 다중 테넌트 데이터 모델

hello 그림 2의 오른쪽 아래 사분면 잠재적으로 큰 공유 단일 데이터베이스를 사용 하는 응용 프로그램 패턴 보여주며, hello 공유 테이블 (또는 별도 스키마) 접근 방식입니다. 모든 테 넌 트 hello 동일한 데이터베이스를 단일 데이터베이스에 있는 리소스 (CPU, 메모리, 입/출력)를 사용 하기 때문에 공유 리소스에 대 한 것이 좋습니다. 그러나 테넌트 격리는 제한됩니다. Tootake 추가 단계 tooprotect 테 넌 트를 서로 hello 응용 프로그램 계층에서 할 수 있습니다. 다음 추가 단계는 개발 하 고 hello 응용 프로그램 관리의 hello DevOps 비용을 길어질 수 있습니다. 확장성은 hello hello 데이터베이스를 호스팅하는 hello 하드웨어 사이의 값으로 제한 됩니다.

그림 2의 왼쪽 아래 사분면 hello 여러 데이터베이스 간에 분할 여러 테 넌을 보여 줍니다. (일반적으로 다른 하드웨어 확장 단위)입니다. 각 데이터베이스는 다른 패턴의 hello 확장성 문제를 해결 하는 테 넌 트의 하위 집합을 호스트 합니다. 더 많은 용량을 더 많은 테 넌 트에 대 한 필요한 경우 toonew 하드웨어 배율 단위를 할당 된 새 데이터베이스에 hello 테 넌 트를 쉽게 배치할 수 있습니다. 그러나 hello 리소스 공유 양이 줄어듭니다. 동일한 hello에 테 넌 트가 배치만 배율 단위는 리소스를 공유 합니다. 이 방법은 많은 테 넌 트가 다른 사용자의 작업에서 자동으로 보호 되 고 하지 않고 계속 배치 하기 때문에 거의 개선 tootenant 격리를 제공 합니다. 응용 프로그램 복잡성의 높게 유지됩니다.

그림 2의 왼쪽 위 사분면 hello는 hello 세 번째 방법입니다. 각 테넌트를 테넌트의 자체 데이터베이스에 배치합니다. 이 방식은 테넌트 격리 속성이 뛰어나지만 각 데이터베이스가 각각의 전용 리소스를 갖기 때문에 리소스 공유를 제한합니다. 모든 테넌트의 작업을 예측할 수 있는 경우에는 이 방식이 적절합니다. 테 넌 트 작업을 예측 하기 어려운 되 면 hello 공급자 리소스를 공유을 최적화할 수 없습니다. SaaS 응용 프로그램의 경우에는 대개 작업을 예측하기가 어렵습니다. hello 공급자 하거나 초과 프로 비전 해야 toomeet 요구 또는 하위 리소스입니다. 두 작업 모두 비용을 증가시키거나 테넌트의 만족을 떨어뜨립니다. 더 높은 수준의 리소스 테 넌 트 간에 공유 바람직한 toomake hello 솔루션 더 비용 효율적으로 바뀝니다. 또한 데이터베이스의 증가 하는 hello 숫자 DevOps 비용 toodeploy 증가 하 고 hello 응용 프로그램 유지 관리 합니다. 이러한 문제를 불구 하 고이 메서드는 테 넌 트에 대 한 hello 가장 쉽고 빠른 격리를 제공합니다.

이러한 요소 고객이 선택 hello 디자인 패턴을도 영향을 미칩니다.

* **테넌트 데이터 소유권**. 테 넌 트 자신의 데이터의 소유권을 유지 하는 응용 프로그램의 테 넌 트 당 단일 데이터베이스 hello 패턴을 우선으로 합니다.
* **확장**. 수십만 또는 수백만 테넌트를 대상으로 하는 응용 프로그램은 분할과 같은 데이터베이스 공유 방식을 선호합니다. 격리 요구 사항도 여전히 문제가 될 수 있습니다.
* **가치 및 비즈니스 모델**. 응용 프로그램의 테넌트별 수익이 1달러 미만 등으로 적은 경우에는 격리 요구 사항의 중요성이 낮아지므로 공유 데이터베이스를 사용하는 것이 적절합니다. 테넌트별 수익이 몇 달러 이상이면 테넌트별 데이터베이스 모델이 더 타당합니다. 개발 비용을 줄이는 데에도 도움이 될 수 있습니다.

그림 2에 표시 된 hello 디자인 절충 사항을 들어 이상적인 다중 테 넌 트 모델 테 넌 트 간에 공유 되는 최적의 리소스와 tooincorporate 좋은 테 넌 트 격리 속성을 필요 합니다. 이 모델은 그림 2의 hello 오른쪽 위 사분면에 설명 된 hello 범주에 적합 합니다.

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Azure SQL Database에서 다중 테넌트 지원
Azure SQL Database는 그림 2에 제시한 다중 테넌트 응용 프로그램 패턴을 모두 지원합니다. 탄력적 풀을 사용도 좋은 리소스 공유 결합 하는 응용 프로그램 패턴을 지원 하 고 hello 데이터베이스 당-테 넌 트의 격리 이점 hello 접근 (hello 오른쪽 위 사분면 그림 3에서 참조). 탄력적 데이터베이스 도구와 SQL 데이터베이스의 기능 줄이고 hello 비용 toodevelop (그림 3에 hello 음영 처리 된 영역에 표시) 하는 많은 데이터베이스는 응용 프로그램을 작동 합니다. 이러한 도구는 빌드 하 고 hello 다중 데이터베이스 패턴 중 하나를 사용 하는 응용 프로그램을 관리할 수 있습니다.

![Azure SQL 데이터베이스의 패턴](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

그림 3: Azure SQL Database의 다중 테넌트 응용 프로그램 패턴

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>탄력적 풀 및 도구를 사용하는 테넌트별 데이터베이스 모델
SQL 데이터베이스의 탄력적 풀 테 넌 트 데이터베이스 toobetter 지원 hello 테 넌 당 데이터베이스 방법을 간에 공유 되는 리소스와 테 넌 트 격리를 결합 합니다. SQL Database는 다중 테넌트 응용 프로그램을 작성하는 SaaS 공급자용 데이터 계층 솔루션입니다. 테 넌 트 간에 공유 되는 리소스의 hello 부담 hello 응용 프로그램 계층 toohello 데이터베이스 서비스 계층에서 이동 합니다. 관리 하 고 대규모 데이터베이스 간 쿼리의 hello 복잡성 탄력적 작업, 탄력적 쿼리, 탄력적 트랜잭션을 hello 탄력적 데이터베이스 클라이언트 라이브러리와 간소화 됩니다.

| 응용 프로그램 요구 사항 | SQL 데이터베이스 기능 |
| --- | --- |
| 테넌트 격리 및 리소스 공유 |[탄력적 풀](sql-database-elastic-pool.md): SQL 데이터베이스 리소스 풀에 할당 하 고 여러 데이터베이스 간에 hello 리소스를 공유 합니다. 또한 개별 데이터베이스를 그릴 수 많은 리소스 hello 풀에서 필요한 tooaccommodate 용량 수요 급증으로 테 넌 트 작업에서 due toochanges 합니다. 탄력적 풀 자체 hello 필요에 따라 위아래로 확장할 수 있습니다. 탄력적 풀 관리의 용이성 및 모니터링과 hello 풀 수준에서 문제 해결을 제공 합니다. |
| 데이터베이스 전반에 대한 DevOps 편의성 |[탄력적 풀](sql-database-elastic-pool.md): 위의 설명을 참조하세요. |
| | [탄력적 쿼리](sql-database-elastic-query-horizontal-partitioning.md): 보고 또는 테넌트 전반에 대한 분석을 위해 데이터베이스 전반에 쿼리를 수행합니다. |
| | [탄력적 작업](sql-database-elastic-jobs-overview.md): 패키지 및 안정적으로 배포 데이터베이스 유지 관리 작업 또는 데이터베이스 스키마가 toomultiple 데이터베이스 변경 합니다. |
| | [탄력적 트랜잭션을](sql-database-elastic-transactions-overview.md): 프로세스를 원자성과 격리 된 방식으로 tooseveral 데이터베이스를 변경 합니다. 응용 프로그램에서 다수의 데이터베이스 작업에 대해 "양자택일"을 보장해야 하는 경우에는 탄력적 트랜잭션이 필요합니다. |
| | [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md): 데이터 배포를 관리 하 고 지도 toodatabases 테 넌 트가 있습니다. |

## <a name="shared-models"></a>공유 모델
앞서 언급했듯이, 대부분의 SaaS 공급자에게 공유 모델 방식은 테넌트 격리 문제는 물론 응용 프로그램 개발 및 유지 관리의 복잡성과 관련해서도 문제를 유발할 수 있습니다. 그러나 직접 tooconsumers, 테 넌 트 서비스를 제공 하는 다중 테 넌 트 응용 프로그램에 대 한 격리 요구 사항을 아니어야 최소화 비용으로 높은 우선 순위 합니다. 이들은 고밀도 tooreduce 비용에서 하나 이상의 데이터베이스에 테 넌 트 수 toopack 수 있습니다. 단일 데이터베이스 또는 다수의 분할된 데이터베이스를 사용하는 공유 데이터베이스 모델은 리소스 공유 효율을 높이고 전체 비용을 낮출 수 있습니다. Azure SQL 데이터베이스 고객 있는 몇 가지 기능이 향상 된 보안 및 hello 데이터 계층의 규모에 관리에 대 한 격리를 빌드를 제공 합니다.

| 응용 프로그램 요구 사항 | SQL 데이터베이스 기능 |
| --- | --- |
| 보안 격리 기능 |[행 수준 보안](https://msdn.microsoft.com/library/dn765131.aspx) |
| [데이터베이스 스키마](https://msdn.microsoft.com/library/dd207005.aspx) | |
| 데이터베이스 전반에 대한 DevOps 편의성 |[탄력적 쿼리](sql-database-elastic-query-horizontal-partitioning.md) |
| | [탄력적 작업](sql-database-elastic-jobs-overview.md) |
| | [탄력적 트랜잭션](sql-database-elastic-transactions-overview.md) |
| | [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md) |
| | [탄력적 데이터베이스 분할 및 병합](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>요약
테넌트 격리 요구 사항은 대부분의 SaaS 다중 테넌트 응용 프로그램에서 중요합니다. hello 최상의 옵션 tooprovide 격리 leans hello 테 넌 당 데이터베이스 접근 방식으로 과도 하 게 합니다. hello 두 가지 다른 접근 방법이 필요 비용 및 위험을 크게 향상 시키는 숙련 된 개발 직원 tooprovide 격리 해야 하는 복잡 한 응용 프로그램 계층에 대 한 투자 합니다. Hello 서비스 개발 초기에 격리 요구 사항을 고려 하지 않습니다, 수정 하 hello 처음 두 모델에서 훨씬 더 비용이 많이 들 수 있습니다. hello 테 넌 당 데이터베이스 모델에 연결 된 hello 주요 단점 되 관련된 tooincreased 클라우드 리소스 비용 기한 tooreduced 공유, 유지 관리 및 많은 데이터베이스 관리 됩니다. SaaS 응용 프로그램 개발자는 이러한 절충에 어려움을 겪는 경우가 많습니다.

장단점에 있을 수 있고 주요 장벽을 대부분 클라우드 데이터베이스 서비스 공급자와 수, Azure SQL 데이터베이스의 탄력적 풀과 탄력적 데이터베이스 기능으로 hello 장애물을 제거 합니다. SaaS 개발자 데이터베이스 당 테 넌 트 모델의 hello 격리 특성을 결합 하 고 탄력적 풀과 관련된 도구를 사용 하 여 많은 데이터베이스의 리소스 공유 및 hello 관리 효율성 향상을 최적화할 수 있습니다.

테넌트 격리 요구 사항이 없으며 테넌트를 데이터베이스에 높은 밀도로 압축할 수 있는 다중 테넌트 응용 프로그램 공급자의 경우 공유 데이터 모델을 사용하면 리소스 공유의 효율성을 추가로 개선하고 전체 비용을 줄일 수 있습니다. Azure SQL Database 탄력적 데이터베이스 도구, 분할 라이브러리 및 보안 기능은 SaaS 공급자가 다중 테넌트 응용 프로그램을 구축하고 관리하는 데 도움을 제공합니다.

## <a name="next-steps"></a>다음 단계
[탄력적 데이터베이스 도구 시작](sql-database-elastic-scale-get-started.md) hello 클라이언트 라이브러리를 보여 주는 샘플 앱을 사용 합니다.

비용 효율적이고 확장성 있는 데이터베이스 솔루션을 위해 탄력적 풀을 사용하는 샘플 앱으로 [SaaS에 대한 탄력적 풀 사용자 지정 대시보드](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) 를 만듭니다.

Hello Azure SQL 데이터베이스 도구를 사용 하 여 너무[아웃 기존 데이터베이스 tooscale 마이그레이션할](sql-database-elastic-convert-to-use-elastic-tools.md)합니다.

사용 하 여 탄력적 풀 toocreate hello Azure 포털에서 참조 [탄력적 풀을 만들](sql-database-elastic-pool-manage-portal.md)합니다.  

너무 방법에 대해 알아봅니다[모니터링 하 고 탄력적 풀 관리](sql-database-elastic-pool-manage-portal.md)합니다.

## <a name="additional-resources"></a>추가 리소스

* [Azure SQL Database를 사용하는 다중 테넌트 응용 프로그램 배포 및 탐색 - Wingtip SaaS](sql-database-saas-tutorial.md)
* [Azure 탄력적 풀이란?](sql-database-elastic-pool.md)
* [Azure SQL 데이터베이스를 사용하여 확장](sql-database-elastic-scale-introduction.md)
* [탄력적 데이터베이스 도구 및 행 수준 보안을 제공하는 다중 테넌트 응용 프로그램](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [Azure Active Directory 및 OpenID Connect를 사용하여 다중 테넌트 앱에서 인증](../guidance/guidance-multitenant-identity-authenticate.md)
* [Tailspin 설문 조사 응용 프로그램](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>질문 및 기능 요청

질문에 대 한 hello에 찾기 [SQL 데이터베이스 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)합니다. Hello에 기능 요청을 추가 [SQL 데이터베이스 피드백 포럼](https://feedback.azure.com/forums/217321-sql-database/)합니다.

