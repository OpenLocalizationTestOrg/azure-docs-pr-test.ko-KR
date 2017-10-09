---
title: "Vm에 서버 응용 프로그램 패턴 aaaSQL | Microsoft Docs"
description: "이 문서에서는 Azure VM에서 SQL Server에 대한 응용 프로그램 패턴을 설명 합니다. 설계자와 개발자들에게 좋은 응용 프로그램 아키텍처 및 설계를 위한 기초를 제공합니다."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 41863c8d-f3a3-4584-ad86-b95094365e05
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: ninarn
ms.openlocfilehash: e18597598fdf9fe534ed07331d6f531d4dca0601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-patterns-and-development-strategies-for-sql-server-in-azure-virtual-machines"></a>Azure 가상 컴퓨터의 SQL Server에 대한 응용 프로그램 패턴 및 개발 전략
[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="summary"></a>요약:
응용 프로그램 패턴 또는 패턴 toouse를 결정 하 Azure에서 SQL 서버 기반 응용 프로그램에 대 한 환경은 중요 한 디자인 결정 이며 해야 SQL Server와 Azure의 각 인프라 구성 요소가 함께 작동의 확실 하 게 이해 . Azure 인프라 서비스에서 SQL server에서는 쉽게 마이그레이션, 유지 관리 및 모니터링할 수 여 기존 SQL Server 응용 프로그램에서 작성 된 Windows Server toovirtual Azure의 컴퓨터.

이 문서의 hello 목표 tooprovide 솔루션 설계자 고 훌륭한 응용 프로그램 아키텍처 및 기존 응용 프로그램 tooAzure로 마이그레이션할 때 따를 수 있는 디자인 하기 위한 기초는 개발자가 Azure에서 새 응용 프로그램으로 개발 제대로 작동 합니다.

각 응용 프로그램 패턴에 대 한 온-프레미스 시나리오, 해당 클라우드 사용 솔루션을 찾을 수 있습니다 및 hello 관련 한 기술 권장 사항을 합니다. 또한 hello 문서 응용 프로그램을 올바르게 디자인할 수 있도록 Azure 관련 개발 전략을 설명 합니다. 기한 toohello 여러 가능한 응용 프로그램 패턴을 것이 좋습니다 설계자와 개발자는 응용 프로그램 및 사용자에 대해 가장 적합 한 패턴 hello 선택 해야 합니다.

**기술 관련 도움 주신 분:** Luis Carlos Vargas Herring, Madhan Arumugam Ramakrishnan

**기술 검토자:** Corey Sanders, Drew McDaniel, Narayan Annamalai, Nir Mashkowski, Sanjay Mishra, Silvano Coriani, Stefan Schackow, Tim Hickey, Tim Wieman, Xin Jin

## <a name="introduction"></a>소개
별도 구성 요소 뿐만 아니라 여러 컴퓨터에서 다른 응용 프로그램 계층 hello의 hello 구성 요소를 구분 하 여 다양 한 유형의 n 계층 응용 프로그램을 개발할 수 있습니다. 예를 들어 hello 클라이언트 응용 프로그램을 배치할 수 있습니다 및 비즈니스 규칙 한 컴퓨터, 프런트 엔드 웹 계층 및 다른 컴퓨터의 데이터 액세스 계층 구성 요소와 다른 컴퓨터의 백 엔드 데이터베이스 계층에서 구성 요소입니다. 이러한 종류의 구조화는 계층을 서로 격리하는 데 도움이 됩니다. 데이터 원본 위치를 변경 하면 toochange hello 클라이언트 또는 웹 응용 프로그램 필요 하지 않지만 데이터 액세스 계층 구성 요소를 hello만 합니다.

일반적인 *n 계층* hello 프레젠테이션 계층, 비즈니스 계층 hello 및 hello 데이터 계층 응용 프로그램에 포함 됩니다.

| 계층 | 설명 |
| --- | --- |
| **프레젠테이션** |hello *프레젠테이션 계층* (웹 계층, 프런트 엔드 계층)은 사용자가 응용 프로그램 상호 작용 하는 hello 계층입니다. |
| **비즈니스** |hello *비즈니스 계층* (중간 계층)은 hello 계층 해당 hello 프레젠테이션 계층 및 hello 데이터 계층 사용 toocommunicate 서로 및 hello 시스템의 hello 핵심 기능이 포함 되어 있습니다. |
| **데이터** |hello *데이터 계층* hello 서버 응용 프로그램의 데이터 (예를 들어 SQL Server를 실행 하는 서버)를 저장 하는 기본적으로 합니다. |

응용 프로그램 계층은 응용 프로그램의 hello 기능 및 구성의 논리적 그룹인 hello를 설명합니다. 반면 계층 (tier) 별도 물리적 서버, 컴퓨터, 네트워크 또는 원격 위치에 hello hello 기능 및 구성 요소의 물리적 배포 합니다. hello 응용 프로그램의 계층에 상주할 수 있습니다 hello 동일한 물리적 컴퓨터 (동일한 계층 hello) 또는 별도 컴퓨터 (n 계층)를 통해 배포 될 수 있습니다 및 hello 각 계층의 구성 요소가 올바르게 정의 된 인터페이스를 통해 다른 계층의 구성 요소와 통신 합니다. N 계층 2 계층, 3 계층 등 toophysical 배포 패턴으로 계층 이라는 용어는 hello 생각할 수 있습니다. **2계층 응용 프로그램 패턴** 에는 응용 프로그램 서버와 데이터베이스 서버 등, 2개의 응용 프로그램 계층이 포함됩니다. hello 직접 통신 hello 응용 프로그램 서버와 데이터베이스 서버 hello 간에 수행 됩니다. hello 응용 프로그램 서버에는 웹 계층 및 비즈니스 계층 구성 요소 모두 포함 되어 있습니다. **3 계층 응용 프로그램 패턴**는 세 개의 응용 프로그램 계층: 웹 서버, hello 비즈니스 논리 계층 및/또는 비즈니스 계층 데이터 액세스 구성 요소에 포함 하는 응용 프로그램 서버와 데이터베이스 서버 hello 합니다. hello 웹 서버와 데이터베이스 서버 hello hello 통신 hello 응용 프로그램 서버를 통해 수행 됩니다. 응용 프로그램 계층 및 계층에 대한 자세한 내용은 [Microsoft 응용 프로그램 아키텍처 가이드](https://msdn.microsoft.com/library/ff650706.aspx)를 참조하세요.

이 문서를 읽기 시작 하기 전에 SQL Server와 Azure의 hello 기본 개념에 대 한 지식이 있어야 합니다. 관련 정보는 [SQL Server Books Online](https://msdn.microsoft.com/library/bb545450.aspx), [Azure Virtual Machines의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 및 [Azure.com](https://azure.microsoft.com/)을 참조하세요.

이 문서에서는 hello 매우 복잡 한 엔터프라이즈 응용 프로그램 뿐만 아니라 사용자는 간단한 응용 프로그램에 대 한 적합할 수 있는 여러 가지 응용 프로그램 패턴을 설명 합니다. 하기 전에 각 패턴을 자세히 나타내는 좋습니다 해야 알아 두는 Azure의 hello 사용 가능한 데이터 저장소 서비스와 같은 [Azure 저장소](../../../storage/common/storage-introduction.md), [Azure SQL 데이터베이스](../../../sql-database/sql-database-technical-overview.md), 및 [ Azure 가상 컴퓨터의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)합니다. 응용 프로그램에 대 한 toomake hello 최상의 디자인 결정 시기를 이해 toouse 데이터 저장소 서비스를 명확 하 게 합니다.

### <a name="choose-sql-server-in-an-azure-virtual-machine-when"></a>Azure 가상 컴퓨터에서의 SQL Server 선택 조건:
* SQL Server 및 Windows에서 제어를 해야 하는 경우. 예를 들어 hello SQL Server 버전, 특수 핫픽스, 성능 구성 등이 포함 될 수 있습니다.
* SQL Server 온-프레미스 완전 한 호환성이 필요 하 고 원하는으로 기존 응용 프로그램 tooAzure toomove-됩니다.
* Azure 환경 hello의 tooleverage hello 기능 하지만 Azure SQL 데이터베이스 응용 프로그램에 필요한 모든 hello 기능을 지원 하지 않습니다. 여기에 다음 영역 hello를 포함 될 수 있습니다.
  
  * **데이터베이스 크기**:이 문서를 업데이트 하는 hello 시간에 SQL 데이터베이스는 too1 t B의 데이터를의 데이터베이스를 지원 합니다. 응용 프로그램에 필요한 데이터 1TB 이상 tooimplement 사용자 지정 분할 솔루션을 원하는 경우 사용 하는 SQL Server는 Azure 가상 컴퓨터에서 것이 좋습니다. Hello 최신 정보를 참조 하십시오. [Azure SQL 데이터베이스 확장](https://msdn.microsoft.com/library/azure/dn495641.aspx) 및 [Azure SQL 데이터베이스 서비스 계층 및 성능 수준](../../../sql-database/sql-database-service-tiers.md)합니다.
  * **HIPAA 규정 준수**: Azure 가상 컴퓨터의 SQL Server는 HIPAA BAA(Business Associate Agreement)가 적용되므로, 의료 부문 고객 및 독립 소프트웨어 공급업체(ISV)는 [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md) 대신 [Azure Virtual Machines의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)를 선택할 수 있습니다. 규정 준수에 대한 자세한 내용은 [Microsoft Azure 보안 센터: 규정 준수](https://azure.microsoft.com/support/trust-center/compliance/)를 참조하세요.
  * **인스턴스 수준 기능**: SQL 데이터베이스,이 이번에 hello 데이터베이스 외부에 존재 하는 기능을 지원 하지 않습니다 (예: 연결 된 서버 에이전트 작업, FileStream, Service Broker 등.). 자세한 내용은 [Azure SQL 데이터베이스 지침 및 제한 사항](https://msdn.microsoft.com/library/azure/ff394102.aspx)을 참조하세요.

## <a name="1-tier-simple-single-virtual-machine"></a>1계층(단순): 단일 가상 컴퓨터
이 응용 프로그램 패턴에서는 SQL Server 응용 프로그램과 Azure의 데이터베이스 tooa 독립 실행형 가상 컴퓨터를 배포 합니다. hello 동일한 가상 컴퓨터에 클라이언트/웹 응용 프로그램, 비즈니스 구성 요소, 데이터 액세스 계층 및 hello 데이터베이스 서버. hello 프레젠테이션, 비즈니스 및 데이터 액세스 코드는 논리적으로 분리 되어 있지만 단일 서버 컴퓨터에 물리적으로 배치 됩니다. 대부분의 고객이이 응용 프로그램 패턴으로 시작 하 고 더 많은 웹 역할 또는 가상 컴퓨터 tootheir 시스템을 추가 하 여 확장은 합니다.

이 응용 프로그램 패턴은 다음과 같은 경우에 유용합니다.

* Hello 플랫폼 여부 응용 프로그램의 요구 사항에 응답 하는지 여부를 원하는 tooperform 간단한 마이그레이션 tooAzure 플랫폼 tooevaluate 합니다.
* 원하는 모든 호스팅 응용 프로그램 계층을 hello tookeep hello 동일한 가상 컴퓨터의 hello에 동일한 Azure 데이터 센터 계층 간 tooreduce hello 대기 시간입니다.
* 짧은 시간에 대 한 테스트 환경 및 tooquickly 프로 비전 개발을 원합니다.
* 다양 한 작업 수준에 대 한 하면서 동시 tooown 원하는 및 많은 실제 유지 관리 하지 않는 컴퓨터의 모든 hello 시간 hello에 tooperform 스트레스 테스트 하는 것이 좋습니다.

hello 다음 다이어그램에서는 간단한 온-프레미스 시나리오와 해당 클라우드 사용 솔루션에서 Azure에서 단일 가상 컴퓨터를 배포 하는 방법

![1계층 응용 프로그램 패턴](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728008.png)

Hello에 hello 비즈니스 계층 (비즈니스 논리 및 데이터 액세스 구성 요소)를 배포 tooscalability 또는 보안 문제로 인해 별도 계층을 사용 해야 하지 않는 한 동일한 물리적 계층 hello 프레젠테이션 계층으로 응용 프로그램 성능을 극대화할 수 있습니다.

다음 문서 마이그레이션 사용 하 여 데이터 tooyour SQL Server VM에서 hello와 매우 일반적인 패턴 toostart 이므로, 알 수 있습니다: [데이터베이스 tooSQL Azure VM에서 서버를 마이그레이션](virtual-machines-windows-migrate-sql.md)합니다.

## <a name="3-tier-simple-multiple-virtual-machines"></a>3계층(단순): 여러 가상 컴퓨터
이 응용 프로그램 패턴에서는 서로 다른 가상 컴퓨터에 각각의 응용 프로그램 계층을 배치하여 Azure에서 3계층 응용 프로그램을 배포합니다. 이 패턴은 간편한 수직 확장 및 수평 확장 시나리오를 위한 유연한 환경을 제공합니다. 하나의 가상 컴퓨터에 클라이언트/웹 응용 프로그램, 다른 하나는 hello 비즈니스 구성 요소를 호스트 하 고 다른 하나의 호스트 hello 데이터베이스 서버 hello 합니다.

이 응용 프로그램 패턴은 다음과 같은 경우에 유용합니다.

* Tooperform 복잡 한 데이터베이스 응용 프로그램 tooAzure 가상 컴퓨터의 마이그레이션을 사용 하는 것이 좋습니다.
* 다른 응용 프로그램 계층 toobe를 서로 다른 지역에서 호스트 되는 것이 좋습니다. 예를 들어 있습니다 공유 데이터베이스가 있을 수는 보고 목적으로 배포 된 toomultiple 영역입니다.
* 온-프레미스에서 toomove 엔터프라이즈 응용 프로그램 플랫폼 tooAzure 가상 컴퓨터를 가상화 하는 것이 좋습니다. 엔터프라이즈 응용 프로그램에 대한 자세한 내용은 [엔터프라이즈 응용 프로그램이란?](https://msdn.microsoft.com/library/aa267045.aspx)을 참조하세요.
* 짧은 시간에 대 한 테스트 환경 및 tooquickly 프로 비전 개발을 원합니다.
* 다양 한 작업 수준에 대 한 하면서 동시 tooown 원하는 및 많은 실제 유지 관리 하지 않는 컴퓨터의 모든 hello 시간 hello에 tooperform 스트레스 테스트 하는 것이 좋습니다.

hello 다음 다이어그램에서는 각 응용 프로그램 계층에 다른 가상 컴퓨터를 배치 하 여 Azure에서 간단한 3 계층 응용 프로그램을 배치 하는 방법을

![3계층 응용 프로그램 패턴](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728009.png)

이 응용 프로그램 패턴에서는 각 계층에 단일 가상 컴퓨터(VM)가 있습니다. Azure에 여러 VM이 있는 경우 가상 네트워크를 설정하는 것이 좋습니다. [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 신뢰할 수 있는 보안 경계를 만들고 hello 개인 IP 주소를 통해 자체 Vm toocommunicate 수도 있습니다. 또한 항상 있도록 모든 인터넷 연결이 프레젠테이션 계층 toohello만 전달 합니다. 이 응용 프로그램 패턴을 따르는 경우 hello 네트워크 보안 그룹 규칙 toocontrol 액세스를 관리 합니다. 자세한 내용은 참조 [Azure 포털 hello 허용 외부 액세스 tooyour 사용 하 여 VM](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

Hello 다이어그램에서 인터넷 프로토콜 TCP, UDP, HTTP 또는 HTTPS를 수 있습니다.

> [!NOTE]
> Azure에서의 가상 네트워크 설정은 무료입니다. 그러나 tooon 온-프레미스를 연결 하는 hello VPN 게이트웨이에 대 한 요금이 청구 됩니다. 대금이 청구 hello 양을 연결 프로 비전 되 고 사용할 수 있는 시간을 기반으로 합니다.
> 
> 

## <a name="2-tier-and-3-tier-with-presentation-tier-scale-out"></a>프레젠테이션 계층 확장이 있는 2계층 및 3계층 
이 응용 프로그램 패턴에서는 각 응용 프로그램 계층에 다른 가상 컴퓨터를 배치 하 여 2 계층 또는 3 계층 데이터베이스 응용 프로그램 tooAzure 가상 컴퓨터를 배포 합니다. 또한 들어오는 클라이언트 요청의 볼륨 tooincreased 인해 hello 프레젠테이션 계층을 확장할 수도 있습니다.

이 응용 프로그램 패턴은 다음과 같은 경우에 유용합니다.

* 온-프레미스에서 toomove 엔터프라이즈 응용 프로그램 플랫폼 tooAzure 가상 컴퓨터를 가상화 하는 것이 좋습니다.
* Tooscale 들어오는 클라이언트 요청의 볼륨 tooincreased 인해 hello 프레젠테이션 계층을 사용 하는 것이 좋습니다.
* 짧은 시간에 대 한 테스트 환경 및 tooquickly 프로 비전 개발을 원합니다.
* 다양 한 작업 수준에 대 한 하면서 동시 tooown 원하는 및 많은 실제 유지 관리 하지 않는 컴퓨터의 모든 hello 시간 hello에 tooperform 스트레스 테스트 하는 것이 좋습니다.
* Tooown 필요에 따라 확장 및 축소가 가능한 인프라 환경을 사용 하는 것이 좋습니다.

hello 다음 다이어그램에서는 들어오는 클라이언트 요청의 볼륨 tooincreased 인해 hello 프레젠테이션 계층을 확장 하 여 Azure에서 여러 가상 컴퓨터에 응용 프로그램 계층 hello를 배치 하는 방법을 Hello 다이어그램에서와 같이 Azure 부하 분산 장치는 여러 가상 컴퓨터 간의 트래픽을 분산 시키고를 결정 하는 웹 서버 tooconnect를 합니다. 부하 분산 장치 뒤에서 웹 서버 hello 여러 인스턴스가 있으면 hello hello 프레젠테이션 계층의 고가용성이 보장 합니다.

![응용 프로그램 패턴 - 프레젠테이션 계층 수평 확장](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728010.png)

### <a name="best-practices-for-2-tier-3-tier-or-n-tier-patterns-that-have-multiple-vms-in-one-tier"></a>한 계층에 여러 VM이 있는 2계층, 3계층 또는 n계층 패턴 모범 사례
동일한 계층에서 동일한 클라우드 서비스와의 동일한 hello hello toohello 속하는 hello 가상 컴퓨터를 배치 하는 것이 좋습니다. 가용성 집합 hello 합니다. 예를 들어, 웹 서버 집합을 **CloudService1** 및 **AvailabilitySet1**에, 데이터베이스 서버 집합을 **CloudService2** 및 **AvailabilitySet2**에 배치합니다. Azure의 가용성 집합에 별도 오류 도메인 및 업그레이드 도메인 tooplace hello 고가용성 노드 수입니다.

tooleverage 여러 VM 인스턴스는 계층의 응용 프로그램 계층 간에 Azure 부하 분산 장치 tooconfigure 해야 합니다. 각 계층에서 tooconfigure 부하 분산 장치 끝점을 만드는 부하 분산 된 각 계층의 Vm에 별도로 합니다. 특정 계층에 대 한 Vm 먼저 만들 hello에서 동일한 클라우드 서비스입니다. 이렇게 하면 hello 수 있는 동일한 공용 가상 IP 주소입니다. 다음으로 해당 계층에서 hello 가상 컴퓨터 중 하나에 끝점을 만듭니다. 그런 다음 할당 다른 가상 컴퓨터 부하 분산을 위해 해당 계층에 동일한 끝점 toohello를 hello 합니다. 부하 분산 집합을 만들어 여러 가상 컴퓨터에 트래픽을 분산 하 고 또한 백엔드 VM 노드 실패 한 경우 어떤 노드 tooconnect hello 부하 분산 장치 toodetermine를 허용 합니다. 예를 들어, 부하 분산 장치 뒤 hello 웹 서버의 인스턴스가 여러 개 있으면 hello hello 프레젠테이션 계층의 고가용성이 보장 됩니다.

모범 사례로 항상 모든 인터넷 연결이 프레젠테이션 계층 toohello 먼저 전달 되는지 확인 합니다. hello 프레젠테이션 계층 hello 비즈니스 계층에 액세스 하 한 다음 hello 비즈니스 계층 hello 데이터 계층에 액세스 합니다. Tooallow toohello 프레젠테이션 계층을 액세스 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 포털 hello 허용 외부 액세스 tooyour 사용 하 여 VM](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

Hello Azure 부하 분산 장치는 온-프레미스 환경에서 비슷한 tooload 분산 장치를 작동 합니다. 자세한 내용은 [Azure 인프라 서비스를 위한 부하 분산](../tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.

또한 Azure 가상 네트워크를 사용하여 가상 컴퓨터에 대한 개인용 네트워크를 설정하는 것이 좋습니다. 따라서 hello 개인 IP 주소를 통해 자체 toocommunicate가 있습니다. 자세한 내용은 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md)를 참조하세요.

## <a name="2-tier-and-3-tier-with-business-tier-scale-out"></a>비즈니스 계층 확장이 있는 2계층 및 3계층 
이 응용 프로그램 패턴에서는 각 응용 프로그램 계층에 다른 가상 컴퓨터를 배치 하 여 2 계층 또는 3 계층 데이터베이스 응용 프로그램 tooAzure 가상 컴퓨터를 배포 합니다. 또한 toodistribute hello 응용 프로그램 서버 구성 요소 toomultiple 가상 컴퓨터 응용 프로그램의 복잡성 toohello 인해 할 수 있습니다.

이 응용 프로그램 패턴은 다음과 같은 경우에 유용합니다.

* 온-프레미스에서 toomove 엔터프라이즈 응용 프로그램 플랫폼 tooAzure 가상 컴퓨터를 가상화 하는 것이 좋습니다.
* 원하는 toodistribute hello 응용 프로그램 서버 구성 요소 toomultiple 가상 컴퓨터 응용 프로그램의 toohello 복잡성 때문입니다.
* Toomove 비즈니스 논리가 많이 온-프레미스 LOB (기간 업무) 응용 프로그램 tooAzure 가상 컴퓨터 사용 하는 것이 좋습니다. LOB 응용 프로그램은 중요 한 toorunning 회계, hr (), 급여, 공급망 관리 및 응용 프로그램 계획 하는 리소스와 같은 엔터프라이즈 있는 중요 한 컴퓨터 응용 프로그램의 집합입니다.
* 짧은 시간에 대 한 테스트 환경 및 tooquickly 프로 비전 개발을 원합니다.
* 다양 한 작업 수준에 대 한 하면서 동시 tooown 원하는 및 많은 실제 유지 관리 하지 않는 컴퓨터의 모든 hello 시간 hello에 tooperform 스트레스 테스트 하는 것이 좋습니다.
* Tooown 필요에 따라 확장 및 축소가 가능한 인프라 환경을 사용 하는 것이 좋습니다.

다음 다이어그램 hello 온-프레미스 시나리오와 해당 클라우드 사용 솔루션을 보여 줍니다. 이 시나리오에서는 hello 비즈니스 논리 계층 및 데이터 액세스 구성 요소를 포함 된 hello 비즈니스 계층을 확장 하 여 Azure에서 여러 가상 컴퓨터에 hello 응용 프로그램 계층을 배치 합니다. Hello 다이어그램에서와 같이 Azure 부하 분산 장치는 여러 가상 컴퓨터 간의 트래픽을 분산 시키고를 결정 하는 웹 서버 tooconnect를 합니다. 부하 분산 장치 뒤 hello 응용 프로그램 서버의 인스턴스가 여러 개 있으면 hello hello 비즈니스 계층의 고가용성이 보장 합니다. 자세한 내용은 [한 계층에 여러 가상 컴퓨터가 있는 2계층, 3계층 또는 n계층 응용 프로그램 패턴 모범 사례](#best-practices-for-2-tier-3-tier-or-n-tier-patterns-that-have-multiple-vms-in-one-tier)를 참조하세요.

![비즈니스 계층 수평 확장이 있는 응용 프로그램 패턴 ](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728011.png)

## <a name="2-tier-and-3-tier-with-presentation-and-business-tiers-scale-out-and-hadr"></a>프레젠테이션 비즈니스 계층 확장 및 HADR이 있는 2계층 및 3계층
이 응용 프로그램 패턴에서는 hello 프레젠테이션 계층 (웹 서버)에 배포 하 여 2 계층 또는 3 계층 데이터베이스 응용 프로그램 tooAzure 가상 컴퓨터를 배포 하 고 비즈니스 계층 (응용 프로그램 서버) 구성 요소 toomultiple 가상 컴퓨터를 hello 합니다. 또한 Azure 가상 컴퓨터에서 데이터베이스를 위한 고가용성 및 재해 복구 솔루션을 구현합니다.

이 응용 프로그램 패턴은 다음과 같은 경우에 유용합니다.

* 원하는 SQL Server 높은 가용성 및 재해 복구 기능을 구현 하 여 가상화 된 플랫폼 온-프레미스 tooAzure에서 toomove 엔터프라이즈 응용 프로그램입니다.
* Tooscale hello 프레젠테이션 계층 및 기한 들어오는 클라이언트 요청의 tooincreased 볼륨 및 응용 프로그램의 hello 복잡성 hello 비즈니스 계층을 사용 하는 것이 좋습니다.
* 짧은 시간에 대 한 테스트 환경 및 tooquickly 프로 비전 개발을 원합니다.
* 다양 한 작업 수준에 대 한 하면서 동시 tooown 원하는 및 많은 실제 유지 관리 하지 않는 컴퓨터의 모든 hello 시간 hello에 tooperform 스트레스 테스트 하는 것이 좋습니다.
* Tooown 필요에 따라 확장 및 축소가 가능한 인프라 환경을 사용 하는 것이 좋습니다.

다음 다이어그램 hello 온-프레미스 시나리오와 해당 클라우드 사용 솔루션을 보여 줍니다. 이 시나리오에서는 hello 프레젠테이션 계층 및 Azure에서 여러 가상 컴퓨터에 비즈니스 계층 구성 요소 hello 확장 합니다. 또한 Azure에서 SQL Server 데이터베이스에 대한 고가용성 및 재해 복구(HADR) 기술을 구현합니다.

서로 다른 VM에서 여러 응용 프로그램 사본을 실행하면 해당 VM에서 요청의 부하를 분산할 수 있습니다. 를 여러 가상 컴퓨터가 있는 Vm에 액세스할 수 있고 한 지점에서 실행 중인에 있는지 시간 toomake가 필요 합니다. 부하 분산을 구성 하는 경우 Azure 부하 분산 장치 트랙 hello Vm의 상태를 들어오는 호출 toohello 정상 작동 VM 노드를 제대로 지시 합니다. 방법에 대 한 hello 가상 컴퓨터의 부하 분산을 tooset 참조 [부하 Azure 인프라 서비스에 대 한 분산](../tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 부하 분산 장치 뒤에 웹 및 응용 프로그램 서버의 인스턴스가 여러 개 있으면 프레젠테이션 및 비즈니스 계층의 hello 고가용성 hello 보장 됩니다.

![수평 확장 및 고가용성](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728012.png)

### <a name="best-practices-for-application-patterns-requiring-sql-hadr"></a>SQL HADR가 필요한 응용 프로그램 패턴 모범 사례
Azure 가상 컴퓨터에서 SQL Server 고가용성 및 재해 복구 솔루션을 설정할 때는 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 를 사용하는 가상 컴퓨터에 대해 가상 네트워크를 설정하는 것이 필수입니다.  DNS 이름 확인에 필요한 hello 업데이트 시간을 방지할 수 있으므로 가상 네트워크 내에서 가상 컴퓨터는 서비스 가동 중지 시간 후에 안정 된 개인 IP 주소를 갖게 됩니다. 또한 hello 가상 네트워크를 사용 하면 tooextend 온-프레미스 tooAzure 네트워크 및 신뢰할 수 있는 보안 경계를 만듭니다. 예를 들어, 응용 프로그램에 회사 도메인 제한 사항(예: Windows 인증, Active Directory)이 있는 경우 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 설정이 필요합니다.

Azure에서 프러덕션 코드를 실행하는 대부분의 고객은 Azure에 주 및 보조 복제본을 유지합니다.

고가용성 및 재해 복구 기술에 대한 종합 정보 및 자습서는 [Azure Virtual Machines의 SQL Server에 대한 고가용성 및 재해 복구](virtual-machines-windows-sql-high-availability-dr.md)를 참조하세요.

## <a name="2-tier-and-3-tier-using-azure-vms-and-cloud-services"></a>Azure VM 및 클라우드 서비스를 사용하는 2계층 및 3계층 
이 응용 프로그램 패턴에서는 모두 사용 하 여 2 계층 또는 3 계층 응용 프로그램 tooAzure 배포 [Azure 클라우드 서비스](../../../cloud-services/cloud-services-choose-me.md#tellmecs) (웹 및 작업자 역할-서비스 (PaaS) 플랫폼) 및 [Azure 가상 컴퓨터](../overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 드 ( Infrastructure as a Service (IaaS)). 사용 하 여 [Azure 클라우드 서비스](https://azure.microsoft.com/documentation/services/cloud-services/) hello 프레젠테이션 계층/비즈니스 계층 및 SQL Server에 대 한 [Azure 가상 컴퓨터](../overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello 데이터에 대 한 계층은 Azure에서 실행 되는 대부분 응용 프로그램에 유용 합니다. hello 이유는 클라우드 서비스에서 실행 중인 계산 인스턴스가 있으면 제공는 간편한 관리, 배포, 모니터링 및 확장입니다.

클라우드 서비스와 Azure hello 인프라를 유지 관리, 일상적인 유지 관리 수행, 패치 hello 운영 체제 및 서비스 및 하드웨어 오류 로부터 toorecover 시도 합니다. 스케일 아웃 응용 프로그램에 필요한 늘리거나 줄여 hello 인스턴스 또는 응용 프로그램에서 사용 되는 가상 컴퓨터 수, 자동 및 수동 확장 옵션 클라우드 서비스 프로젝트에 대해 사용할 수 있습니다. 또한 사용할 수 있습니다 Visual Studio toodeploy 온-프레미스 응용 프로그램 tooa 클라우드 서비스 프로젝트 Azure에서.

요약 하자면, hello 프레젠테이션/비즈니스 계층에 대해 tooown 광범위 한 관리 작업을 원하지 응용 프로그램 소프트웨어 또는 hello 운영 체제의 복잡 한 구성이 필요 하지 않는 경우 Azure 클라우드 서비스를 사용 합니다. Azure SQL 데이터베이스에 대 한 원하는 모든 hello 기능을 지원 하지 않으면 사용 하 여 SQL Server는 Azure 가상 컴퓨터에서 hello 데이터 계층에 대 한 합니다. Azure 클라우드 서비스에서 응용 프로그램을 실행 하며 Azure 가상 컴퓨터의 데이터를 저장 합니다. 두 서비스의 hello 이점을 결합 합니다. 자세한 비교에이 항목의 hello 섹션을 참조 [Azure에서 개발 전략 비교](#comparing-web-development-strategies-in-azure)합니다.

이 응용 프로그램 패턴에서는 프레젠테이션 계층 hello hello Azure 실행 환경에서 실행 하는 클라우드 서비스 구성 요소 및 IIS 및 ASP.NET에서 지 원하는 대로 웹 응용 프로그램 프로그래밍에 대 한 사용자가 웹 역할에 포함 됩니다. hello 비즈니스 또는 백엔드 계층 hello Azure 실행 환경에서 실행 하는 클라우드 서비스 구성 요소 및 일반적인된 개발에 유용 하 고 웹 역할에 대 한 백그라운드 처리를 수행할 수 있는 작업자 역할에 포함 됩니다. hello 데이터베이스 계층은 Azure에서 SQL Server 가상 컴퓨터에 상주합니다. hello 프레젠테이션 계층 및 hello 데이터베이스 계층 사이의 hello 통신 직접 또는 hello 비즈니스 계층 – 작업자 역할 구성 요소를 통해 수행 됩니다.

이 응용 프로그램 패턴은 다음과 같은 경우에 유용합니다.

* 원하는 SQL Server 높은 가용성 및 재해 복구 기능을 구현 하 여 가상화 된 플랫폼 온-프레미스 tooAzure에서 toomove 엔터프라이즈 응용 프로그램입니다.
* Tooown 필요에 따라 확장 및 축소가 가능한 인프라 환경을 사용 하는 것이 좋습니다.
* Azure SQL 데이터베이스 응용 프로그램 또는 데이터베이스에 필요한 모든 hello 기능을 지원 하지 않습니다.
* 다양 한 작업 수준에 대 한 하면서 동시 tooown 원하는 및 많은 실제 유지 관리 하지 않는 컴퓨터의 모든 hello 시간 hello에 tooperform 스트레스 테스트 하는 것이 좋습니다.

다음 다이어그램 hello 온-프레미스 시나리오와 해당 클라우드 사용 솔루션을 보여 줍니다. 이 시나리오에서는 웹 역할에서 프레젠테이션 계층 hello, 작업자 역할에 비즈니스 계층 hello 하지만 Azure의 가상 컴퓨터에서 hello 데이터 계층을 배치합니다. Hello 프레젠테이션 계층의 여러 복사본이 다른 웹 역할에서 실행 되 고 tooload 분산 요청을 확인 합니다. Azure 가상 컴퓨터에 Azure 클라우드 서비스를 결합할 경우 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 도 설정하는 것이 좋습니다. 와 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md), 안정성을 포함할 수 있습니다 및 hello 서비스에 동일한 클라우드 내의 영구 개인 IP 주소 hello 클라우드입니다. 가상 컴퓨터에 대 한 가상 네트워크를 정의 하 고 클라우드 서비스를 hello 개인 IP 주소를 통해 서로 통신을 시작할 수 있습니다. 또한 가상 컴퓨터와 Azure 웹/작업자 역할에 동일한 hello 있으면 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 대기 시간이 줄어들고 연결의 보안이 강화 됩니다. 자세한 내용은 [클라우드 서비스란?](../../../cloud-services/cloud-services-choose-me.md)을 참조하세요.

Azure 부하 분산 장치 hello 다이어그램에서와 같이 여러 가상 컴퓨터에 트래픽을 분산 하 고 또한 웹 서버 또는 응용 프로그램 서버를 결정 하려면 tooconnect 합니다. 부하 분산 장치 뒤 hello 웹 및 응용 프로그램 서버의 인스턴스가 여러 개 있으면 hello hello 프레젠테이션 계층 및 hello 비즈니스 계층의 고가용성이 보장 됩니다. 자세한 내용은 [SQL HADR가 필요한 응용 프로그램 패턴 모범 사례](#best-practices-for-application-patterns-requiring-sql-hadr)를 참조하세요.

![클라우드 서비스가 있는 응용 프로그램 패턴](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728013.png)

또 다른 방법은 tooimplement이 응용 프로그램 패턴은 toouse hello 다음과 같이 프레젠테이션 계층 및 비즈니스 계층 구성 요소를 포함 하는 통합된 웹 역할 다이어그램. 이 응용 프로그램 패턴은 안정적인 설계가 필요한 응용 프로그램에 유용합니다. Azure 웹 및 작업자 역할에서 상태 비저장 계산 노드가 제공 하므로 hello 다음 기술 중 하나를 사용 하 여 논리 toostore 세션 상태를 구현 하는 것이 좋습니다: [Azure Caching](https://azure.microsoft.com/documentation/services/redis-cache/), [Azure테이블저장소](../../../cosmos-db/table-storage-how-to-use-dotnet.md) 또는 [Azure SQL 데이터베이스](../../../sql-database/sql-database-technical-overview.md)합니다.

![클라우드 서비스가 있는 응용 프로그램 패턴](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728014.png)

## <a name="pattern-with-azure-vms-azure-sql-database-and-azure-app-service-web-apps"></a>Azure VM, Azure SQL 데이터베이스 및 Azure 앱 서비스(웹앱)가 있는 패턴
이 응용 프로그램 패턴의 hello 주요 목표는 tooshow 있습니다 어떻게 toocombine 솔루션에서 Azure 플랫폼으로-서비스 구성 (PaaS)와 서비스 (IaaS) 구성 요소로 Azure 인프라입니다. 이 패턴은 관계형 데이터 저장소를 위한 Azure SQL 데이터베이스에 초점을 맞춥니다. 이 포함 되지 않습니다 SQL Server는 Azure 가상 컴퓨터에 hello로 서비스를 제공 하는 Azure 인프라의 일부인.

이 응용 프로그램 패턴에서는 hello 프레젠테이션을 배치 하 여 데이터베이스 응용 프로그램 tooAzure를 배포 하 고 비즈니스 계층에 hello 동일한 가상 컴퓨터 및 Azure SQL 데이터베이스 (SQL 데이터베이스) 서버에서 데이터베이스에 액세스 합니다. 기존의 IIS 기반 웹 솔루션을 사용 하 여 hello 프레젠테이션 계층을 구현할 수 있습니다. 또는 [Azure 웹앱](https://azure.microsoft.com/documentation/services/app-service/web/)을 사용하여 결합된 프레젠테이션 및 비즈니스 계층을 구현할 수 있습니다.

이 응용 프로그램 패턴은 다음과 같은 경우에 유용합니다.

* 이미 Azure에서 구성 된 기존 SQL 데이터베이스 서버 및 원하는 tootest 응용 프로그램이 신속 하 게 합니다.
* Tootest hello Azure 환경의 기능을 사용 하는 것이 좋습니다.
* 짧은 시간에 대 한 테스트 환경 및 tooquickly 프로 비전 개발을 원합니다.
* 비즈니스 논리 및 데이터 액세스 구성 요소는 웹 응용 프로그램 안에 자체 포함될 수 있습니다.

다음 다이어그램 hello 온-프레미스 시나리오와 해당 클라우드 사용 솔루션을 보여 줍니다. 이 시나리오에서는 Azure SQL 데이터베이스의 데이터에 액세스 하 Azure의 단일 가상 컴퓨터에 hello 응용 프로그램 계층을 배치합니다.

![혼합 응용 프로그램 패턴](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728015.png)

Tooimplement를 선택 하는 경우에 Azure 웹 앱을 사용 하 여 결합 된 웹 및 응용 프로그램 계층, hello 중간 계층 또는 응용 프로그램 계층 웹 응용 프로그램의 hello 컨텍스트에서 동적 연결 라이브러리 (Dll)으로 유지 하는 것이 좋습니다.

또한 hello에 제공 된 hello 권장 사항을 검토 [Azure의 웹 개발 전략 비교](#comparing-web-development-strategies-in-azure) hello 프로그래밍 기술에 대 한 자세한 문서 toolearn이 끝나기 전에 섹션.

## <a name="n-tier-hybrid-application-pattern"></a>N계층 하이브리드 응용 프로그램 패턴
N계층 하이브리드 응용 프로그램 패턴에서는 온-프레미스와 Azure 간에 분산된 여러 계층에서 응용 프로그램을 구현합니다. 따라서 수정 하거나 추가할 수 있는 유연 하 고 재사용 가능한 하이브리드 시스템을 만들를 변경 하지 않고 특정 계층 hello 다른 계층입니다. tooextend 회사 네트워크 toohello 클라우드를 사용 하 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md) 서비스입니다.

이 하이브리드 응용 프로그램 패턴은 다음과 같은 경우에 유용합니다.

* 실행 하는 hello 클라우드에 부분적으로 부분적으로 온-프레미스 toobuild 응용 프로그램 사용 하는 것이 좋습니다.
* 기존 온-프레미스 응용 프로그램 toohello 클라우드에의 일부 또는 모든 요소를 toomigrate 할 수 있습니다.
* 온-프레미스 가상화 플랫폼 tooAzure에서 toomove 엔터프라이즈 응용 프로그램 사용 하는 것이 좋습니다.
* Tooown 필요에 따라 확장 및 축소가 가능한 인프라 환경을 사용 하는 것이 좋습니다.
* 짧은 시간에 대 한 테스트 환경 및 tooquickly 프로 비전 개발을 원합니다.
* 원하는 엔터프라이즈 데이터베이스 응용 프로그램에 대 한 비용 효율적인 방식으로 tootake 백업 합니다.

hello 다이어그램을 다음 온-프레미스와 Azure 전체의 걸쳐 있는 n 계층 하이브리드 응용 프로그램 패턴을 보여 줍니다. Hello 다이어그램에 나와 있는 것 처럼 온-프레미스 인프라에 포함 된 [Active Directory 도메인 서비스](https://technet.microsoft.com/library/hh831484.aspx) 도메인 컨트롤러 toosupport 사용자 인증 및 권한 부여 합니다. Note 해당 hello 다이어그램 hello 데이터 계층의 일부가 거주 온-프레미스 데이터 센터에서 Azure의 hello 데이터 계층의 일부가 라이브 반면는 시나리오를 보여 줍니다. 사용자 응용 프로그램의 요구에 따라 여러 다른 하이브리드 시나리오를 구현할 수 있습니다. 예를 들어 azure에서는 온-프레미스 환경을 없지만 hello 데이터 계층에 hello 프레젠테이션 계층 및 비즈니스 계층 hello 가질 수 있습니다.

![n계층 응용 프로그램 패턴](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728016.png)

Azure에서는 Active Directory를 조직의 독립 실행형 클라우드 디렉터리로 사용할 수 있지만 기존 온-프레미스 Active Directory와 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)를 통합할 수도 있습니다. Hello 다이어그램에서와 같이 hello 비즈니스 계층 구성 요소 수 toomultiple 데이터 원본에 액세스와 같은 너무[Azure의 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) 는 사설 내부 IP 주소를 통해 tooon 온-프레미스 SQL Server를 통해 [Azure가상네트워크](../../../virtual-network/virtual-networks-overview.md), 또는 너무[SQL 데이터베이스](../../../sql-database/sql-database-technical-overview.md) hello.NET Framework 데이터 공급자 기술을 사용 하 여 합니다. 이 그림에서 Azure SQL 데이터베이스는 선택적 데이터 저장소 서비스입니다.

N 계층 하이브리드 응용 프로그램 패턴에서는 지정 된 hello 순서 대로 워크플로 수행 하는 hello를 구현할 수 있습니다.

1. Toobe hello를 사용 하 여 toocloud 위로 이동 해야 하는 엔터프라이즈 데이터베이스 응용 프로그램 식별 [Microsoft Assessment and Planning (MAP) Toolkit](http://microsoft.com/map)합니다. MAP Toolkit hello 가상화에 대 한 고려 하는 컴퓨터에서 재고 및 성능 데이터를 수집 및 용량 및 평가 계획에 권장 사항을 제공 합니다.
2. Hello 저장소 계정 및 가상 컴퓨터와 같은 Azure 플랫폼에에서 필요한 hello 리소스 및 구성을 계획 합니다.
3. Hello 회사 네트워크 온-프레미스 간에 네트워크 연결을 설정 하 고 [Azure 가상 네트워크](../../../virtual-network/virtual-networks-overview.md)합니다. hello 회사 네트워크 온-프레미스와 azure에서 가상 컴퓨터 사이 hello 연결을 tooset hello 다음 두 가지 방법 중 하나를 사용 합니다.
   
   1. Azure의 가상 컴퓨터에 있는 공용 끝점을 통해 온-프레미스와 Azure 간의 연결을 설정합니다. 이 메서드는 쉽게 설정할 수를 제공 하 고 가상 컴퓨터에서 SQL Server 인증 toouse 있습니다. 또한 사용자 네트워크 보안 그룹 규칙 toocontrol 공용 트래픽 toohello VM 설정 합니다. 자세한 내용은 참조 [Azure 포털 hello 허용 외부 액세스 tooyour 사용 하 여 VM](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
   2. Azure 가상 사설망(VPN) 터널을 통해 온-프레미스와 Azure 간의 연결을 설정합니다. 이 방법을 사용 하면 있습니다 tooextend 도메인 정책 tooa 가상 컴퓨터가 Azure에서. 또한 방화벽 규칙을 설정하고 가상 컴퓨터에서 Windows 인증을 사용할 수 있습니다. 현재 Azure는 사이트 간 및 지점-사이트 간 보안 VPN 연결을 지원합니다.
      
      * 사이트 간 보안 연결을 통해 온-프레미스 네트워크와 Azure의 가상 네트워크 간에 네트워크 연결을 설정할 수 있습니다. 에 온-프레미스 데이터 센터 환경 tooAzure 연결 하기 위한 것이 좋습니다.
      * 안전한 지점-사이트 간 연결을 통해 Azure의 가상 네트워크와, 다른 어딘가에서 실행되는 개별 컴퓨터 간에 네트워크 연결을 설정할 수 있습니다. 주로 개발 및 테스트용으로 사용하는 것이 좋습니다.
      
      방법에 대 한 내용은 tooconnect tooSQL Azure의 서버 참조 [tooa Azure에서 SQL Server 가상 컴퓨터를 연결](virtual-machines-windows-sql-connect.md)합니다.
4. Azure의 가상 컴퓨터 디스크에 온-프레미스 데이터를 백업하는 예약 작업 및 알림을 설정합니다. 자세한 내용은 [Azure Blob Storage 서비스로 SQL Server 백업 및 복원](https://msdn.microsoft.com/library/jj919148.aspx)과 [Azure Virtual Machines에서 SQL Server의 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)을 참조하세요.
5. 응용 프로그램의 필요에 따라 다음 세 가지 일반적인 시나리오는 hello 중 하나를 구현할 수 있습니다.
   
   1. Hello 중요 한 온-프레미스 데이터를 유지 하지만 Azure에서 데이터베이스 서버에 웹 서버, 응용 프로그램 서버 및 중요 하지 않은 데이터를 유지할 수 있습니다.
   2. 웹 서버를 유지할 수 있습니다 및 응용 프로그램 서버를 온-프레미스에서 Azure 가상 컴퓨터에서 데이터베이스 서버 hello 합니다.
   3. 데이터베이스 서버, 웹 서버를 유지할 수 있습니다 및 응용 프로그램 서버 온-프레미스에서 Azure의 가상 컴퓨터 hello 데이터베이스 복제본을 보관 하 합니다. 이 설정을 hello 온-프레미스 웹 서버 또는 보고 응용 프로그램 tooaccess hello Azure에서 데이터베이스 복제본 사용. 따라서 온-프레미스 데이터베이스에 toolower hello 작업 부하를 얻을 수 있습니다. 이 시나리오는 읽기 워크로드가 매우 많은 개발 용도로 구현하는 것이 좋습니다. Azure에서 데이터베이스 복제본을 만드는 방법은 [Azure Virtual Machines의 SQL Server에 대한 고가용성 및 재해 복구](virtual-machines-windows-sql-high-availability-dr.md)의 AlwaysOn 가용성 그룹을 참조하세요.

## <a name="comparing-web-development-strategies-in-azure"></a>Azure에서의 웹 개발 전략 비교
tooimplement 및 다중 계층 응용 프로그램을 Azure에서 SQL Server 기반 배포, hello 다음 두 가지 프로그래밍 방법 중 하나를 사용할 수 있습니다.

* Azure 가상 컴퓨터의 SQL Server에서 Azure 및 액세스 데이터베이스에서 기존 웹 서버(IIS,인터넷 정보 서비스)를 설정합니다.
* 구현 하 고 클라우드 서비스 tooAzure를 배포 합니다. 그런 다음 이 클라우드 서비스가 Azure 가상 컴퓨터의 SQL Server에 액세스할 수 있는지 확인합니다. 클라우드 서비스는 여러 웹 및 작업자 역할을 포함할 수 있습니다.

다음 표에서 hello 존중 tooSQL 서버 Azure 가상 컴퓨터에서 기존 웹 개발과 Azure 클라우드 서비스 및 Azure 웹 앱의 비교를 제공 합니다. hello 테이블은 가능한 toouse Azure VM의 SQL Server는 공용 가상 IP 주소 또는 DNS 이름을 통해 Azure 웹 앱에 대 한 데이터 원본으로 하는 대로 Azure 웹 앱을 포함 합니다.

|  | Azure 가상 컴퓨터의 기존 웹 개발 | Azure의 클라우드 서비스 | Azure 웹앱에서 웹 호스팅 |
| --- | --- | --- | --- |
| **온-프레미스에서 응용 프로그램 마이그레이션** |기존 응용 프로그램 있는 그대로 사용합니다. |응용 프로그램에 웹 및 작업자 역할이 필요합니다. |기존 응용 프로그램 그대로이지만 빠른 확장성이 필요한 자체 포함된 웹 응용 프로그램 및 웹 서비스에 적합합니다. |
| **개발 및 배포** |Visual Studio, WebMatrix, Visual Web Developer, WebDeploy, FTP, TFS, IIS Manager, PowerShell. |Visual Studio, Azure SDK, TFS, PowerShell. 각 클라우드 서비스에 두 환경 toowhich 서비스 패키지와 구성을 배포할 수 있습니다: 스테이징 및 프로덕션 합니다. 환경 tootest를 준비 하는 클라우드 서비스 toohello를 배포할 수 전에 tooproduction 승격 합니다. |Visual Studio, WebMatrix, Visual Web Developer, FTP, GIT, BitBucket, CodePlex, DropBox, GitHub, Mercurial, TFS, Web Deploy, PowerShell. |
| **관리 및 설치** |Hello 응용 프로그램, 데이터, 방화벽 규칙, 가상 네트워크 및 운영 체제에서 관리 작업에 책임이 있습니다. |Hello 응용 프로그램, 데이터, 방화벽 규칙 및 가상 네트워크에 있는 관리 작업에 책임이 있습니다. |Hello 응용 프로그램 및 데이터에만 관리 작업에 책임이 있습니다. |
| **HADR(고가용성 및 재해 복구)** |동일한 가용성 집합과 동일한 hello hello에 가상 컴퓨터를 배치 하는 것이 좋습니다 클라우드 서비스입니다. 동일한 hello에 Vm을 유지 가용성 집합에서는 다음과 같은 Azure tooplace hello 고가용성 노드를 별도 오류 도메인 및 업그레이드 도메인으로 합니다. 마찬가지로, Vm을 유지 hello에서 동일한 클라우드 서비스를 사용 하면 부하 분산 및 Vm hello Azure 데이터 센터 내의 로컬 네트워크를 통해 서로 직접 통신할 수 있습니다.<br/><br/>고가용성 및 재해 복구 솔루션 구현 SQL Server에 대 한 tooavoid Azure 가상 컴퓨터에서에서 가동 중지 시간 책임이 있습니다. 지원되는 HADR 기술은 [Azure Virtual Machines의 SQL Server에 대한 고가용성 및 재해 복구](virtual-machines-windows-sql-high-availability-dr.md)를 참조하세요.<br/><br/>사용자 고유의 데이터와 응용 프로그램 백업을 담당해야 합니다.<br/><br/>Hello 데이터 센터에 호스트 컴퓨터 hello toohardware 문제 인해 실패할 경우 azure 가상 컴퓨터를 이동할 수 있습니다. 또한 있을 수 VM의 계획 된 가동 중지 hello 호스트 컴퓨터 보안 또는 소프트웨어 업데이트 될 때 업데이트 합니다. 따라서 두 개 이상의 Vm에서 각 응용 프로그램 계층 tooensure hello 지속적인 가용성을 유지 관리 하는 것이 좋습니다. Azure는 단일 가상 컴퓨터에 대한 SLA를 제공하지 않습니다. 자세한 내용은 [Azure 복원력 기술 지침](../../../resiliency/resiliency-technical-guidance.md)을 참조하세요. |Azure는 hello 기본 하드웨어 또는 운영 체제 소프트웨어로 인 한 hello 오류를 관리 합니다. 웹 또는 작업자 역할 tooensure hello 항상 사용 가능한 응용 프로그램의 여러 인스턴스를 구현 하는 것이 좋습니다. 자세한 내용은 [Cloud Services, Virtual Machines 및 Virtual Network Service Level Agreement(서비스 수준 약정)](http://www.microsoft.com/download/details.aspx?id=38427) 및 [Azure 응용 프로그램에 대한 재해 복구 및 고가용성](../../../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)을 참조하세요.<br/><br/>사용자 고유의 데이터와 응용 프로그램 백업을 담당해야 합니다.<br/><br/>Azure VM에서 SQL Server 데이터베이스에 있는 데이터베이스에 대 한 책임이 있습니다 높은 가용성 및 재해 복구 솔루션 tooavoid 가동 중지 시간을 구현 합니다. 지원되는 HDAR 기술은 Azure 가상 컴퓨터의 SQL Server에 대한 고가용성 및 재해 복구를 참조하세요.<br/><br/>**SQL Server 데이터베이스 미러링**: Azure 클라우드 서비스와 함께 사용합니다(웹/작업자 역할). SQL Server Vm 및 클라우드 서비스 프로젝트 수 수에 hello 동일한 Azure 가상 네트워크입니다. SQL Server VM에 없는 경우 동일한 가상 네트워크를 hello toocreate SQL Server의 SQL Server 별칭 tooroute 통신 toohello 인스턴스를 해야 합니다. 또한 hello 별칭 이름은 hello SQL Server 이름과 일치 해야 합니다. |고가용성은 Azure 작업자 역할, Azure BLOB 저장소 및 Azure SQL 데이터베이스에서 상속됩니다. 예를 들어, Azure 저장소는 모든 BLOB, 테이블 및 큐 데이터의 복제본 3개를 유지 관리합니다. 어느 시점에나 Azure SQL 데이터베이스는 실행 중인 데이터에 대해 주 복제본 1개와 보조 복제본 2개 등, 3개의 복제본을 보유하고 있습니다.  자세한 내용은 [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) 및 [Azure SQL Database](../../../sql-database/sql-database-technical-overview.md)를 참조하세요.<br/><br/>Azure Web Apps용 데이터 소스로 Azure VM의 SQL Server를 사용할 때는 Azure Web Apps가 Azure 가상 네트워크를 지원하지 않는다는 점에 유의합니다. 즉, Azure 웹 앱 tooSQL Azure의 서버 Vm에서에서 모든 연결 가상 컴퓨터의 공용 끝점을 통해 이동 해야 합니다. 이로 인해 고가용성 및 재해 복구 시나리오에 몇 가지 제한이 발생할 수 있습니다. 예를 들어 데이터베이스 미러링에서 tooSQL 서버 VM을 연결 하는 Azure 웹 앱에서 hello 클라이언트 응용 프로그램이 됩니다 수 tooconnect toohello 새 주 서버에서 SQL Server 호스트 Vm 간에 Azure 가상 네트워크를 설정 하는 사용 하려면 데이터베이스 미러링 Azure입니다. 따라서 Azure Web Apps로 **SQL Server Database 미러링**은 현재 지원되지 않습니다.<br/><br/>**SQL Server AlwaysOn 가용성 그룹**: Azure에서 SQL Server VM으로 Azure Web Apps를 사용하는 경우 AlwaysOn 가용성 그룹을 설정할 수 있습니다. 하지만 tooconfigure AlwaysOn 가용성 그룹 수신기 tooroute hello 통신 toohello을 통해 주 복제본으로 부하 분산 끝점을 공개 합니다. |
| **크로스 프레미스 연결** |Azure 가상 tooconnect tooon 온-프레미스 네트워크를 사용할 수 있습니다. |Azure 가상 tooconnect tooon 온-프레미스 네트워크를 사용할 수 있습니다. |Azure 가상 네트워크가 지원됩니다. 자세한 내용은 [웹앱 가상 네트워크 통합](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/)을 참조하세요. |
| **확장성** |수직 hello 가상 컴퓨터 크기를 늘리거나 디스크를 추가 하 여 ´ ù. 가상 컴퓨터 크기에 대한 자세한 내용은 [Azure에 대한 가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.<br/><br/>**데이터베이스 서버의 경우**: 데이터베이스 분할 기법 및 SQL Server AlwaysOn 가용성 그룹을 통해 확장을 사용할 수 있습니다.<br/><br/>많은 읽기 작업의 경우 여러 보조 노드 뿐만 아니라 SQL Server 복제에서 [AlwaysOn 가용성 그룹](https://msdn.microsoft.com/library/hh510230.aspx)을 사용할 수 있습니다.<br/><br/>과도 한 쓰기 작업에 대 한 여러 물리적 서버 tooprovide 응용 프로그램 확장 간에 데이터를 행 분할을 구현할 수 있습니다.<br/><br/>또한 [데이터 종속 라우팅으로 SQL Server](https://technet.microsoft.com/library/cc966448.aspx)를 사용하여 확장을 구현할 수 있습니다. 와 종속 라우팅 DDR (데이터), tooimplement hello 분할 메커니즘 hello 비즈니스 계층 레이어에서의 일반적으로 hello 클라이언트 응용 프로그램에 필요한, tooroute hello 데이터베이스 요청 toomultiple SQL Server 노드. hello 비즈니스 계층 매핑을 포함 toohow hello 데이터 분할 되 고 있는 노드 hello 데이터를 포함 합니다.<br/><br/>가상 컴퓨터를 실행 중인 응용 프로그램을 확장할 수 있습니다. 자세한 내용은 참조 [방법을 응용 프로그램 tooScale](../../../cloud-services/cloud-services-how-to-scale.md)합니다.<br/><br/>**중요 한 참고**: hello **자동 크기 조정** Azure 기능 tooautomatically 증가 허용 하거나 응용 프로그램에서 사용 되는 가상 컴퓨터 hello 감소 합니다. 이 기능은 사용량이 많은 기간 동안 hello 최종 사용자 환경을 부정적인 영향을 받지 않으며 hello 요구가 적을 때는 Vm이 종료를 보장 합니다. 설정 하지 않으면 hello 자동 크기 조정 옵션 클라우드 서비스에 대 한 SQL Server Vm을 포함 하는 것이 좋습니다. hello 이유는 해당 hello 자동 크기 조정 기능 hello 해당 VM의 CPU 사용량 보다 높은 경우 일부 임계값 및 가상 컴퓨터의 전원을 tooturn hello CPU 사용량 미만이 고 가상 컴퓨터에서 Azure tooturn를 수 있습니다. hello 자동 크기 조정 기능은 모든 VM 참조 tooany 이전 상태 없이 hello 작업 부하를 관리할 수는 웹 서버와 같은 상태 비저장 응용 프로그램에 유용 합니다. 그러나 hello 자동 크기 조정 기능은 한 인스턴스만 toohello 데이터베이스를 작성할 수 있습니다. 여기서 SQL Server와 같은 상태 저장 응용 프로그램에 유용 하지 않습니다. |여러 웹 및 작업자 역할을 사용하면 확장이 가능합니다. 웹 역할 및 작업자 역할의 가상 컴퓨터 크기에 대한 자세한 내용은 [Cloud Services에 대한 크기 구성](../../../cloud-services/cloud-services-sizes-specs.md)을 참조하세요.<br/><br/>사용 하는 경우 **클라우드 서비스**, 여러 역할 toodistribute 처리를 정의 하 고 응용 프로그램의 유연한 확장이 가능 합니다. 각각의 클라우드 서비스는 각기 고유한 응용 프로그램 파일 및 구성을 포함하는 하나 이상의 웹 역할 및/또는 작업자 역할을 포함합니다. 수직 확장 클라우드 서비스 역할에 대 한 배포 된 hello 역할 인스턴스 (가상 컴퓨터) 수를 증가 시켜 있고 hello 역할 인스턴스 수가 감소 하 여 클라우드 서비스 확장 / 축소 합니다. 자세한 내용은 [Azure 실행 모드](../../../cloud-services/cloud-services-choose-me.md)를 참조하세요.<br/><br/>확장은 [Cloud Services, Virtual Machines 및 Virtual Network Service Level Agreement(서비스 수준 약정)](http://www.microsoft.com/download/details.aspx?id=38427) 및 부하 분산 장치를 통한 기본 제공 Azure 고가용성 지원을 통해 사용 가능합니다.<br/><br/>다중 계층 응용 프로그램의 경우 웹/작업자 역할 응용 프로그램 toodatabase 서버 Azure 가상 네트워크를 통해 Vm에 연결 해야 하는 것이 좋습니다. Azure에서에서 부하 분산 Vm에 대 한 hello 동일를 제공 하는 또한 클라우드 서비스 간에 사용자 요청을 분배 합니다. 이러한 방식으로 연결 된 가상 컴퓨터는 hello Azure 데이터 센터 내의 로컬 네트워크를 통해 서로 직접 통신할 수 있습니다.<br/><br/>설정할 수 있습니다 **자동 크기 조정** hello 예약 시간: hello Azure 포털에 있습니다. 자세한 내용은 참조 [tooconfigure 자동 hello 포털에서 클라우드 서비스에 대 한 크기 조정 방법](../../../cloud-services/cloud-services-how-to-scale-portal.md)합니다. |**확장 및 축소가**: 있습니다 수 증가/감소 hello hello 인스턴스 (VM) 웹 사이트에 대 한 예약 크기입니다.<br/><br/>확장: 웹 사이트에 더 많은 예약된 인스턴스(VM)를 추가할 수 있습니다.<br/><br/>설정할 수 있습니다 **자동 크기 조정** hello 포털: hello 예약 시간에 있습니다. 자세한 내용은 참조 [어떻게 tooScale 웹 앱](../../../app-service-web/web-sites-scale.md)합니다. |

이러한 프로그래밍 메서드 중에서 선택에 대 한 자세한 내용은 참조 하십시오. [Azure 웹 앱, 클라우드 서비스 및 Vm: 때 toouse 있는](../../../app-service-web/choose-web-site-cloud-service-vm.md)합니다.

## <a name="next-steps"></a>다음 단계
Azure Virtual Machines의 SQL Server 실행에 대한 자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

