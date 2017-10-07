---
title: "Azure aaaDesign 복잡 한 솔루션에 대 한 템플릿을 | Microsoft Docs"
description: "복잡한 시나리오에 대한 Azure Resource Manager 템플릿 디자인에 대한 모범 사례 표시"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ce1141d6-ece7-4976-acea-1db1f775409e
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: aa45e9a46d79a6336b696cff8fd37f65fa449f11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-azure-resource-manager-templates-when-deploying-complex-solutions"></a>복잡한 솔루션을 배포할 때 Azure Resource Manager 템플릿에 대한 디자인 패턴
Azure Resource Manager 템플릿을 기반으로 유연한 접근 방식을 사용하면 복잡한 토폴로지를 신속하고 일관되게 배포할 수 있습니다. 이러한 배포 제공 발전 코어 또는 이상 값 시나리오 또는 고객에 대 한 tooaccommodate 변형으로 쉽게 만들 수도 있습니다.

이 항목은 더 큰 백서의 일부입니다. 전체 용지 tooread hello 다운로드 [세계 클래스 Azure 리소스 관리자 템플릿 고려 사항 및 입증 된 사례](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf)합니다.

서식 파일의 hello 적응성 및 가독성의 JSON JavaScript Object Notation () 사용 하 여 Azure 리소스 관리자 기본 hello hello 이점을 결합 합니다. 템플릿을 사용하여 가능한 작업:

* 토폴로지 및 토폴로지의 워크로드를 일관되게 배포합니다.
* 리소스 그룹을 사용하여 하나의 응용 프로그램에서 모든 리소스를 함께 관리합니다.
* 역할 기반 액세스 제어 (RBAC) toogrant 적절 한 액세스 toousers, 그룹 및 서비스에 적용 됩니다.
* 롤업 청구 등의 태그 연결 toostreamline 작업을 사용 합니다.

이 문서는 Azure 고객 자문 팀(AzureCAT) 고객과의 실제 환경 템플릿 구현 및 설계 세션 중에 확인된 소비 시나리오, 아키텍처, 및 구현 패턴에 대해 자세한 내용을 제공합니다. 이러한 접근 방식을 들에 크게 못 미치는 사례 정보를 포함 하 여 hello top Linux 기반 OSS 기술의 12에 대 한 템플릿의 hello 개발 하 여 입증 됩니다: Apache Kafka, Apache Spark, Cloudera, Couchbase, Hortonworks HDP, 기반의 DataStax Enterprise Apache Cassandra Elasticsearch, Jenkins, MongoDB, PostgreSQL, Redis, 및 Nagios 합니다. 

이 문서는 세계 클래스 Azure 리소스 관리자 템플릿의 설계 하면 이러한 검증 된 사례 toohelp를 공유 합니다.  

고객과의 작업에서 엔터프라이즈, SI(시스템 통합자) 및 CSV의 몇몇 Resource Manager 템플릿 소비 경험을 확인했습니다. hello 다음 섹션에서는 일반적인 시나리오 및 패턴 상위 수준 개요를 서로 다른 고객 형식에 대 한 합니다.

## <a name="enterprises-and-system-integrators"></a>엔터프라이즈 및 시스템 통합 업체
큰 조직에는 일반적으로 두 가지 Resource Manager 템플릿 소비자(내부 소프트웨어 개발 팀 및 기업 IT)가 있습니다. आ म क ा SIs hello에 대 한 hello 시나리오 기업의 경우, toohello 시나리오로 너무 hello 동일한 고려 사항이 적용 됩니다.

### <a name="internal-software-development-teams"></a>내부 소프트웨어 개발 팀
팀 비즈니스 소프트웨어 toosupport에서 개발 하는 경우 템플릿은 쉽게 tooquickly 비즈니스 솔루션에서 사용 하기 위한 기술이 배포를 제공 합니다. 서식 파일을 사용할 수도 있습니다 toorapidly 있는 팀 멤버 toogain 필요한 기술 교육 환경을 만듭니다.

템플릿을으로 사용할 수 있습니다-은 또는 확장 하거나 tooaccommodate 쿼리를 작성 필요 합니다. 템플릿 내에서 태그 지정을 사용하면 팀, 프로젝트, 개인 및 교육과 같은 다양한 보기로 청구 요약을 제공할 수 있습니다.

기업은 소프트웨어 개발 팀이 솔루션의 일관 된 배포에 대 한 템플릿을 toocreate 원합니다. hello 템플릿 제약 조건을 용이 하 게 되므로 환경 내에서 특정 항목 고정 되어 있으며 재정의할 수 없습니다. 예를 들어 은행 수 필요 템플릿 tooinclude RBAC 하므로 프로그래머가 은행 솔루션을 수정할 수 없습니다 toosend 데이터 tooa 개인 저장소 계정입니다.

### <a name="corporate-it"></a>기업 IT
기업 IT 조직은 일반적으로 클라우드 용량 및 클라우드 호스티드 기능을 제공하기 위한 템플릿을 사용합니다.

#### <a name="cloud-capacity"></a>클라우드 용량
팀에 대 한 회사 IT 그룹 tooprovide 클라우드 용량에 대 한 작은, 보통, 같은 크기를 제공 하는 표준 및 큰 "티셔츠 크기"와 일반적인 방법은입니다. hello 티셔츠 크기의 제공 하면 가능한 toouse 서식 파일이 표준화 수준을 제공 하는 동안 여러 리소스 종류 및 수량을 혼합할 수 있습니다. hello 템플릿 회사 정책을 적용 하 고 태그 tooprovide 비용 정산 tooconsuming 조직을 사용 하는 일관 된 방식으로 용량을 제공 합니다.

예를 들어 tooprovide 개발, 테스트 또는 프로덕션 환경 소프트웨어 개발 팀이 어떤 hello 내에서 해당 솔루션을 배포할 수를 할 수 있습니다. hello 환경에는 미리 정의 된 네트워크 토폴로지 및 액세스 toohello 공용 인터넷 및 패킷 검사를 적용 되는 규칙 등 소프트웨어 개발 팀 hello 요소 변경할 수 없습니다. 또한 이러한 환경에 대 한 hello 환경에 대 한 별도 액세스 권한이 있는 조직 관련 역할을 할 수 있습니다.

#### <a name="cloud-hosted-capabilities"></a>클라우드 호스티드 기능
템플릿 toosupport 클라우드 호스팅 기능을 개별 소프트웨어 패키지 또는 업무 계통 toointernal 제공 되는 복합 제공을 포함 하 여 사용할 수 있습니다. 복합 제품의 예에는 미리 정의된 네트워크 토폴로지에 최적화되어 연결된 구성으로 제공되는 Analytics-as-a-service(분석, 시각화 및 기타 기술)가 있습니다.

클라우드 호스팅 기능 hello 보안 및 역할 고려 사항 hello 클라우드 용량에 작성 하는 제공 하 여 설정 된 영향을 받습니다. 이러한 기능은 있는 그대로 제공되거나 관리 서비스로 제공됩니다. 후자의 hello에 대 한 액세스 제한 된 역할은 필수 hello 환경으로 관리 목적을 위해 tooenable 액세스 합니다.

## <a name="cloud-service-vendors"></a>클라우드 서비스 공급업체
Toomany Csv와 이야기를 한 후 고객 및 관련된 요구 사항에 대 한 toodeploy 서비스를 수행할 수 있는 다양 한 접근 방식이 확인 했습니다.

### <a name="csv-hosted-offering"></a>CSV 호스티드 제품
사용자가 소유하는 Azure 구독 내에 제품을 호스트하는 경우 두 가지 호스팅 접근 방식이 일반적이며, 모든 고객을 위한 고유한 배포를 수행하거나 모든 고객에 대해 사용되는 공유 인프라의 기초가 되는 배율 단위를 배포합니다.

* **각 고객에 대한 고유한 배포.** 고객 당 고유한 배포에는 알려져 있는 다양한 구성에 대한 고정 토폴로지가 필요합니다. 이러한 배포를 통해 다양한 VM(가상 컴퓨터) 크기, 다양한 수의 노드, 다양한 크기의 관련 저장소가 포함될 수 있습니다. 배포 태그 지정은 각 고객의 롤업 청구에 사용됩니다. RBAC의 클라우드 환경 활성화 tooallow 고객 액세스 tooaspects 될 수 있습니다.
* **공유 다중 테넌트 환경의 배율 단위.** 템플릿은 다중 테넌트 환경에 대한 배율 단위를 나타낼 수 있습니다. 이 경우 동일한 인프라 hello는 toosupport 사용 되는 모든 고객 합니다. hello 배포 한 수준의 사용자 수 및 트랜잭션 수와 같은 제공 호스트 hello에 대 한 용량을 제공 하는 리소스 그룹을을 나타냅니다. 이러한 배율 단위는 요구 사항의 필요에 따라서 증가되거나 감소됩니다.

### <a name="csv-offering-injected-into-customer-subscription"></a>고객 구독에 삽입되는 CSV 제품
최종 고객 소유한 구독에 toodeploy 소프트웨어를 할 수 있습니다. 고객의 Azure 계정에 템플릿 toodeploy 고유한 배포를 사용할 수 있습니다.

이러한 배포를 업데이트 하 고 hello 고객의 계정 내에서 hello 배포를 관리할 수 있도록 RBAC를 사용 합니다.

### <a name="azure-marketplace"></a>Azure 마켓플레이스
tooadvertise Azure 마켓플레이스와 같은 마켓플레이스를 통해 제품을 판매 하 고, 템플릿을 toodeliver 고유 고객의 Azure 계정에서 실행 되는 배포 유형을 개발할 수 있습니다. 고유한 배포는 일반적으로 티셔츠 크기(대, 중, 소), 제품/대상 그룹 유형(커뮤니티, 개발자, 엔터프라이즈) 또는 기능 유형(기본, 고가용성)으로 명시됩니다.  경우에 따라 이러한 형식을 사용 하면 toospecify hello 배포 VM 유형 또는 디스크 수 등의 특정 한 특성입니다.

## <a name="oss-projects"></a>OSS 프로젝트
오픈 소스 프로젝트 내에서 리소스 관리자 템플릿을 신속 하 게 검증 된 사례를 사용 하는 솔루션 커뮤니티 toodeploy을 사용 합니다. Hello 커뮤니티 시간에 따라 수정할 수 있도록 GitHub 리포지토리에 서식 파일을 저장할 수 있습니다. 사용자는 자신의 Azure 구독에 이 템플릿을 배포합니다.

hello 다음 섹션에서는 식별 hello 작업 솔루션을 디자인 하기 전에 tooconsider 필요 합니다.

## <a name="identifying-what-is-outside-and-inside-a-vm"></a>VM의 외부 및 내부 항목 확인
서식 파일을 디자인할 때 유용한 toolook hello 가상 컴퓨터 (Vm) 내부 및 외부 측면에서 hello 요구 사항에서:

* 외부 Vm 및 태그 지정, 참조 toohello 인증/암호 및 역할 기반 액세스 제어 hello 네트워크 토폴로지, 같은 배포의 다른 리소스 hello를 의미 합니다. 이러한 모든 리소스가 템플릿의 일부입니다.
* 내부 의미 hello 소프트웨어를 설치 하 고 전반적인 원하는 상태 구성 합니다. 그 외에 VM 확장 또는 스크립트 같은 기타 메커니즘이 전체적으로 또는 부분적으로 사용됩니다. 이러한 메커니즘을 식별 하 고 hello 서식 파일에서 실행할 수 있습니다 하지만 그 안에 아닌 합니다.

일반적인 "내부"hello 상자 수행한 작업의 예로-  

* 서버 역할 및 기능을 설치 또는 제거
* 소프트웨어 설치 및 구성 hello 노드 또는 클러스터 수준에서
* 웹 서버에서 웹 사이트 배포
* 데이터베이스 스키마 배포
* 레지스트리 또는 다른 유형의 구성 설정 관리
* 파일 및 디렉터리 관리
* 프로세스 및 서비스 시작, 중지 및 관리
* 로컬 그룹 및 사용자 계정 관리
* 패키지(.msi, .exe, yum 등) 설치 및 관리
* 환경 변수 관리
* 네이티브 스크립트(Windows PowerShell, bash 등) 실행

### <a name="desired-state-configuration-dsc"></a>DSC(필요한 상태 구성)
배포 이외의 Vm의 내부 상태 hello에 대 한 생각이 toomake이이 배포 하지 않습니다 "드리프트" 정의 하 고 확인 하는 hello 구성에서 소스 제어에 있는지 원하는 합니다. 이 방법을 사용 하면 개발자 또는 운영 담당자는 없는 검사, 테스트 또는 소스 제어에 기록 하는 임시 변경 tooan 환경을 만들지 못합니다. 소스 제어에 hello 수동으로 변경 되지 않으므로이 컨트롤은 중요 합니다. 또한 hello 표준 배포의 일부가 아니고 hello 소프트웨어의 이후 자동화 된 배포에 영향을 줍니다.

내부 직원 외에 필요한 상태 구성은 보안적인 관점에서 중요합니다. 해커는 toocompromise 려 정기적으로 및 소프트웨어 시스템을 이용 합니다. 성공 하면 공용 tooinstall 파일 이며 그렇지 않은 경우 손상된 된 시스템의 hello 상태를 변경 합니다. 필요한 상태 구성을 사용 하 여, 실제 상태와 원하는 hello 간의 델타를 식별 및 알려진된 구성을 복원할 수 있습니다.

리소스 확장 메커니즘에 대해 hello 가장 인기 있는 DSC 기능에 대 한 PowerShell DSC, Chef 및 Puppet 있습니다. 각이 확장 hello VM의 초기 상태를 배포할 수 있으며 수도 사용된 toomake 있는지 hello 원하는 상태가 유지 됩니다.

## <a name="common-template-scopes"></a>일반적인 템플릿 범위
경험을 통해 세 가지 주요 솔루션 템플릿을 확인하였습니다. 이러한 세 가지 범위 – 용량, 기능 및 종단 간 솔루션 – hello 다음 섹션에에서 설명 되어 있습니다.

### <a name="capacity-scope"></a>용량 범위
용량 범위에는 미리 구성 된 toobe 정책과 규정을 준수 하는 표준 토폴로지 리소스 집합을 제공 합니다. 엔터프라이즈 IT 또는 SI 시나리오의 표준 개발 환경을 배포 하는 hello 가장 일반적인 예입니다.

### <a name="capability-scope"></a>기능 범위
기능 범위는 특정 기술에 대한 토폴로지를 배포 및 구성하는 것에 초점을 맞춥니다. 일반적인 시나리오는 SQL Server, Cassandra, Hadoop 같은 기술을 포함합니다.

### <a name="end-to-end-solution-scope"></a>종단간 솔루션 범위
종단 간 솔루션 범위는 단일 기능 이외의 대상 이며 대신 여러 기능으로 구성 하는 최종 tooend 솔루션 제공 하는 데 초점을 맞춘 합니다.  

솔루션 범위 템플릿의 범위는 솔루션 고유의 리소스, 논리 및 필요한 상태를 포함하는 하나 이상의 기능 범위 템플릿 집합으로 자체 명시됩니다. 솔루션 범위 서식 파일의 예는 최종 tooend 데이터 파이프라인 솔루션 템플릿을입니다. hello 템플릿 Kafka, 스톰을 Hadoop 등 여러 기능 범위 솔루션 템플릿으로 솔루션 별 토폴로지 및 상태를 혼합할 수 있습니다.

## <a name="choosing-free-form-vs-known-configurations"></a>자유 형식 또는 알려진 구성 선택
템플릿을 소비자 hello 무엇 보다도 유연성을 제공 해야 하지만 많은 고려 사항 냐 hello 선택에 영향을 처음 생각 toouse 자유 형식 구성 알려진된 구성 비교 합니다. 이 섹션에는 hello 키 고객 요구 사항 및 모양 hello 방법은이 문서에서 공유 하는 기술 고려 사항 알아봅니다.

### <a name="free-form-configurations"></a>자유 형식 구성
자유 형식 구성 사운드 hello 화면에 적합 합니다. 사용 하면 tooselect VM 유형 및 임의 개수의 노드 제공 및 연결 된 해당 노드에 대 한 디스크-매개 변수 tooa 템플릿으로 아무 키나 합니다. 그러나 이 접근 방식은 일부 시나리오에는 적합하지 않습니다.

[가상 컴퓨터의 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), 각 VM 유형에서는 hello 및 사용 가능한 크기 및 (2, 4, 8, 16, 또는 32)는 있는 디스크 각각 hello 수가 내구성이 연결할 수 있습니다. 각각의 연결된 디스크는 500 IOPS를 제공하며 이 디스크의 배수는 해당 IOPS의 승수로 풀링될 수 있습니다. 예를 들어 16 개의 디스크 풀링된 tooprovide 8, 000 IOPS 수 있습니다. 풀링 hello 운영 체제에서 Microsoft Windows 저장소 공간 또는 저비용 (RAID) 디스크의 중복 배열을 사용 하 여 Linux에서 구성을 사용 하 여 수행 됩니다.

자유 형식 구성 통해 hello 선택 여러 VM 인스턴스 VM 다양 한 형식 및 해당 인스턴스용 VM 유형 hello에 대 한 다양 한 디스크의 크기를 조정 하 고 하나 이상의 스크립트 tooconfigure hello VM 내용을.

모든 노드 유형에 대해 유연성이 제공될 수 있도록 배포에는 마스터 및 데이터 노드 같이 여러 가지 유형의 노드를 포함하는 것이 일반적입니다.

모든 significance의 toodeploy 클러스터를 시작 하면 이러한 복잡 한 시나리오와 toowork를 시작 합니다. Hadoop 클러스터에 배포 하는 예를 들어 8 개의 노드로 구성 마스터 200 데이터 노드 및 각 마스터 노드에 4 풀링된 연결 된 디스크 및 데이터 노드를 당 16 풀링된 연결 된 디스크는 있으면 208 Vm 및 3,232 디스크 toomanage입니다.

저장소 계정 위의 식별 된 해당 20000 트랜잭션 수/초 제한, 저장소 계정 분할 확인 하 고 계산 toodetermine hello 적절 한 수의 스토리지 계정 tooaccommodate이이 토폴로지를 사용 해야 하므로 요청 조절 됩니다. Hello 다양 한 조합 hello 자유 형식 접근 방식으로 동적 계산에서 지 원하는 제공은 필수 toodetermine hello 적절 한 분할 합니다. hello 적절 한 세부 정보와 함께 고유, 하드 코드 된 서식 파일 생성 코드에서 이러한 계산을 수행 해야 있습니다 하므로 hello Azure 리소스 관리자 템플릿 언어 수치 연산 함수를 현재 제공 하지 않습니다.

엔터프라이즈 IT 및 SI 시나리오에서 누군가가 hello 서식 파일을 유지 하 고 하나 이상의 조직에 대 한 hello 배포 토폴로지를 지원 해야 합니다. 고객별로 구성과 템플릿이 다르기 때문에 발생하는 부가적인 오버헤드는 결코 바람직하지 않습니다.

이러한 템플릿 toodeploy 환경 고객의 Azure 구독에서 사용할 수 있지만 회사 IT 팀과 Csv 일반적으로 프로그램에 배포할 자체 구독 비용 청구 함수 toobill를 사용 하 여 고객에 게. 이러한 시나리오에서는 hello ´ ֲ toodeploy 용량 여러 고객에 대 한 구독 및 구독 toominimize 구독 무분별 hello에 채울 조밀 하 게 유지 배포 풀에서-즉, 더 많은 구독 toomanage 합니다. 동적인 배포 크기를 가진이 유형의 밀도 달성 필요 신중 하 게 계획 및 추가 개발 hello 조직 대신 하 여 스 캐 폴딩 작업에 대 한 합니다.

또한 API 호출을 통해 구독을 만들 수 없습니다 있지만 hello 포털을 통해 수동으로 수행 해야 합니다. 모든 결과 구독 무분별 사람의 개입이 필요 hello 구독 수가 증가 하면-자동화할 수 없습니다. 배포의 hello 크기에 많은 양의 가변성을 사용 해야 toopre 프로 비전 구독 수가 수동으로 tooensure 구독을 사용할 수 있습니다.

이러한 모든 요소를 고려하면 진정한 자유 형식 구성은 언뜻 보기에 덜 매력적입니다.

### <a name="known-configurations--hello-t-shirt-sizing-approach"></a>알려진 구성 — hello 티셔츠 크기 조정 방법
대신 총 유연 하 고 무수 한 변형 하는 서식 파일, 제공 하는 것 보다 경험에 따르면 일반적인 패턴은 알려진 구성을 tooprovide hello 기능 tooselect-실제로 소형, 중형 및 대형 샌드박스 등 표준 티셔츠 크기를 조정 합니다. 티셔츠 크기의 다른 예에는 커뮤니티 버전이나 엔터프라이즈 버전 같은 제품이 있습니다.  그 외 경우에는 Map Reduce 또는 No SQL 같은 특정 워크로드에 대한 기술 구성이 있습니다.

많은 엔터프라이즈 IT 조직, OSS 공급업체 및 SI에서 현재 이러한 방식으로 온-프레미스, 가상화된 환경(엔터프라이즈) 또는 SaaS(Software-as-a-Service) 제품(CSV 및 OSV)으로 자사의 제품을 제공합니다.

이러한 접근 방식은 고객을 위해 미리 구성된 다양한 크기의 좋은, 알려진 구성을 제공합니다. 알려진된 구성을 없이 최종 고객 해야 자체적으로 클러스터 크기를 확인, 플랫폼 리소스 제약 조건에 모아 놓은 수학 tooidentify hello 결과의 저장소 계정 및 기타 리소스 (기한 toocluster 크기 및 리소스 분할을 수행합니다 제약 조건)입니다. 알려진 구성을 사용 고객 tooeasily 선택 hello 오른쪽 티셔츠 크기-즉, 특정된 배포 합니다. 또한 hello 고객에 대 한 향상 된 환경 toomaking 적은 수의 알려진된 구성 쉽게 toosupport 이며 더 높은 수준의 밀도 제공 하는 데 도움이 합니다.

티셔츠 크기에 중점을 두는 알려진 구성 접근 방식은 하나의 크기 내에 다양한 수의 노드를 둘 수도 있습니다. 예를 들어 작은 티셔츠 크기는 3개에서 10개 사이의 노드가 될 수 있습니다.  hello 티셔츠 크기 too10 노드를 설계 된 tooaccommodate 라인과 hello 소비자 hello 기능 toomake 자유 형식 선택 toohello 식별 되는 최대 크기를 제공 합니다.  

작업 형식에 따라 티셔츠 크기는 배포할 수 있지만 hello 노드에서 작업 개별 노드 크기 및 hello 소프트웨어의 구성에는 노드의 hello 수 측면에서 본질적으로 더 많은 자유 형식 수 있습니다.

일반적으로 고유한 리소스 종류 및 배포할 수 있는 노드의 최대 수에 있을 수 있습니다 community 또는 Enterprise와 같은 제품 기능에 따라 티셔츠 크기에 걸쳐 다양 한 제품을 hello toolicensing 고려 사항 또는 기능 가용성이 연결 되어 있습니다.

Hello JSON 기반 템플릿을 사용 하 여 고유한 변형 된 고객을 수용할 수 있습니다. 이상 값을 처리할 때는 hello 적절 한 계획 및 개발, 지원 및 비용 계산에 대 한 고려 사항에 통합할 수 있습니다.

Hello 고객 템플릿 사용 시나리오 및이 문서의 hello 시작 될 때 요구 사항에 기반 템플릿 분해 하는 작업에 대 한 패턴을 확인 했습니다.

## <a name="capacity-and-capability-scoped-solution-templates"></a>용량 및 기능 범위 솔루션 템플릿
분해 모듈식 방법을 tootemplate 개발을 지 원하는 재사용, 확장성, 테스트 및 도구를 제공 합니다. 이 섹션에서는 분해 방법이 적용된 tootemplates 용량 또는 용량 범위를 갖는 수 있는 방법에 세부 정보를 제공 합니다.

이 접근 방식에서 주 템플릿 템플릿 소비자에서 매개 변수 값을 받는 다음 아래와 같이 다운스트림으로 tooseveral 유형의 서식 파일 및 스크립트에 연결 합니다. 매개 변수, 정적 변수 및 생성 된 변수는 연결 된 hello 템플릿 아웃 tooprovide 사용 되는 값입니다.

![템플릿 매개 변수](./media/best-practices-resource-manager-design-templates/template-parameters.png)

**주 템플릿 tooa 다음 toolinked 템플릿 매개 변수 전달**

hello에 나오는 섹션 포커스에 따라 hello 유형의 템플릿과 단일 서식 파일은로 분해 하는 스크립트입니다. hello 섹션 hello 템플릿 간에 상태 정보를 전달 하기 위한 방법을 제시 합니다. 각 템플릿 및 hello 스크립트 유형은 hello 이미지의 예제와 함께 설명 되어 있습니다. 상황별 예제를 보려면 이 문서의 뒷부분에서 “요약: 샘플 구현"을 참조하세요.

### <a name="template-metadata"></a>템플릿 메타데이터
템플릿 메타 데이터 (hello metadata.json 파일) 사람과 소프트웨어 시스템에서 읽을 수 있는 JSON으로 서식 파일을 설명 하는 키/값 쌍을 포함 합니다.

![템플릿 메타데이터](./media/best-practices-resource-manager-design-templates/template-metadata.png)

**Hello metadata.json 파일에서 템플릿 메타 데이터 설명**

소프트웨어 에이전트 수 hello metadata.json 파일을 검색 하 고 웹 페이지 또는 디렉터리의 hello 정보 및 링크 toohello 템플릿을 게시 합니다. 요소는 *itemDisplayName*, *description*, *summary*, *githubUsername* 및 *dateUpdated*를 포함합니다.

예제 파일 전체가 아래에 표시됩니다.

    {
        "itemDisplayName": "PostgreSQL 9.3 on Ubuntu VMs",
        "description": "This template creates a PostgreSQL streaming-replication between a master and one or more slave servers each with 2 striped data disks. hello database servers are deployed into a private-only subnet with one publicly accessible jumpbox VM in a DMZ subnet with public IP.",
        "summary": "PostgreSQL stream-replication with multiple slave servers and a publicly accessible jumpbox VM",
        "githubUsername": "arsenvlad",
        "dateUpdated": "2015-04-24"
    }

### <a name="main-template"></a>기본 템플릿
hello 주 템플릿 사용자 로부터 매개 변수를 수신 하 고, 해당 정보 toopopulate 복잡 한 개체 변수를 사용 하 여, 연결 된 hello 서식 파일을 실행 합니다.

![기본 템플릿](./media/best-practices-resource-manager-design-templates/main-template.png)

**사용자 로부터 매개 변수를 수신 하는 hello 주 템플릿**

제공 되는 매개 변수 중 하나는 같은 작은, 보통, 또는 대형의 표준화 된 값이 알려진된 구성 유형 라고도 hello 티셔츠 크기 매개 변수. 실제로 이 매개 변수를 여러 가지 방식으로 사용할 수 있습니다. 자세한 내용은 이 문서의 뒷부분에서 “알려진 구성 리소스 템플릿"을 참조하십시오.

일부 리소스 user 매개 변수에 의해 지정 된 hello 알려진된 구성에 관계 없이 배포 됩니다. 이러한 리소스는 단일 공유 리소스 템플릿을 사용 하 여 하는 프로 비전 하 고 있으므로 첫 번째 실행 하는 hello 공유 리소스 서식 파일은 다른 서식 파일에서 공유 합니다.

일부 리소스는 hello 지정 된 알려진된 구성에 관계 없이 필요에 따라 배포 됩니다.

### <a name="shared-resources-template"></a>공유 리소스 템플릿
이 템플릿은 알려진 모든 구성에 공통적인 리소스를 제공합니다. Hello 가상 네트워크, 가용성 집합 및 배포 된 hello 알려진된 구성 템플릿을 관계 없이 필요한 기타 리소스를 포함 합니다.

![템플릿 리소스](./media/best-practices-resource-manager-design-templates/template-resources.png)

**공유 리소스 템플릿**

예: hello 가상 네트워크 이름 리소스 이름 hello 기본 서식 파일을 기반으로 합니다. 해당 서식 파일 내의 변수도 지정 하거나 조직에서 필요에 따라 hello 사용자에서 매개 변수로 받을 수 있습니다.

### <a name="optional-resources-template"></a>선택적 리소스 템플릿
hello 선택적 리소스 템플릿 매개 변수 또는 변수의 hello 값에 따라 프로그래밍 방식으로 배포 되는 리소스를 포함 합니다.

![선택적 리소스](./media/best-practices-resource-manager-design-templates/optional-resources.png)

**선택적 리소스 템플릿**

선택적 리소스 템플릿 tooconfigure hello에서 간접적으로 액세스 tooa 배포 된 환경을 사용 하도록 설정 하는 jumpbox를 사용할 수는 예를 들어 공용 인터넷 합니다. 매개 변수 또는 변수 tooidentify hello jumpbox 활성화할지 여부를 사용 하 고 hello *concat* 함수 hello 템플릿용으로 toobuild hello 대상 이름 같은 *jumpbox_enabled.json*합니다. 서식 파일 연결 결과 변수 tooinstall hello jumpbox hello를 사용 합니다.

여러 위치에서 선택적 리소스 템플릿을 hello를 연결할 수 있습니다.

* 경우 적용 가능한 tooevery 배포 hello 공유 리소스 서식 파일에서 매개 변수가 지정 링크를 만듭니다.
* 때 구성에 알려진 해당 tooselect-예를 들어 대규모 배포에만 설치-hello 알려진된 구성 템플릿에서 매개 변수 또는 변수 기반 링크를 만듭니다.

지정된 된 리소스 옵션 인지 하지 hello 템플릿 소비자에 의해 그 대신에 따라 결정 됩니다 hello 템플릿 공급자입니다. 예를 들어 특정 제품 요구 사항 또는 제품 추가 기능 (Csv에 대 한 공통) 또는 tooenforce 정책 toosatisfy 할 수 있습니다 (일반적으로 SIs와 엔터프라이즈 IT 그룹). 이러한 경우 hello 리소스를 배포 해야 하는지 여부를 변수 tooidentify를 사용할 수 있습니다.

### <a name="known-configuration-resources-template"></a>알려진 구성 리소스 템플릿
Hello 주 템플릿 매개 변수가 노출 된 tooallow hello 템플릿 소비자 toospecify 원하는 알려진된 구성 toodeploy 될 수 있습니다. 알려진 구성은 샌드박스, 대, 중, 소와 같은 고정된 구성 확장 집합으로 티셔츠 크기 접근 방식을 자주 사용합니다.

![알려진 구성 리소스](./media/best-practices-resource-manager-design-templates/known-config.png)

**알려진 구성 리소스 템플릿**

티셔츠 크기 접근 방식을 hello는 일반적으로 사용 되지 않지만 hello 매개 변수는 알려진된 구성 모든 집합을 나타낼 수 있습니다. 예를 들어 개발, 테스트, 제품 같은 엔터프라이즈 응용 프로그램을 위한 환경 집합을 지정할 수 있습니다. 다른 클라우드 서비스 toorepresent에 사용할 수 있습니다 또는 단위, 제품 버전 또는 커뮤니티, Developer 또는 Enterprise와 같은 제품 구성의 크기를 조정 합니다.

공유 리소스 템플릿 hello와 마찬가지로 변수 중 하나에서 toohello 알려진된 구성을 서식 파일을 전달 됩니다.

* 최종 사용자-즉, hello 매개 변수 toohello 기본 서식 파일을 전송 합니다.
* 조직-즉, 내부 요구 사항이 나 정책을 나타내는 hello 기본 서식 파일에 변수를 hello 합니다.

### <a name="member-resources-template"></a>멤버 리소스 템플릿
알려진 구성 내에는 하나 이상의 멤버 노드 유형이 포함됩니다. 예를 들어 Hadoop에 마스터 노드와 데이터 노드를 포함합니다. MongoDB를 설치하는 경우 데이터 노드와 중재자를 포함합니다. DataStax를 배포하는 경우 데이터 노드는 물론 OpsCenter가 설치된 VM을 포함합니다.

![멤버 리소스](./media/best-practices-resource-manager-design-templates/member-resources.png)

**멤버 리소스 템플릿**

각 노드 유형이 서로 다른 크기의 Vm에 연결 된 디스크, 스크립트 tooinstall 수가 하 고 hello 노드, Vm hello에 대 한 포트 구성, 인스턴스 수, 및 기타 세부 정보를 설정. 각 노드 유형에 고유한 하므로 hello 포함 된 멤버 리소스 템플릿 배포 및 구성 하는 인프라와 같은 스크립트 toodeploy 실행에 대해 자세히 설명 하 고 hello VM 내에서 소프트웨어를 구성 합니다.

VM의 경우 일반적으로 두 가지 유형의 스크립트(광범위한 재사용이 가능한 스크립트와 사용자 지정 스크립트)가 사용됩니다.

### <a name="widely-reusable-scripts"></a>광범위한 재사용이 가능한 스크립트
광범위한 재사용이 가능한 스크립트는 여러 가지 유형의 템플릿에서 사용될 수 있습니다. 광범위 하 게 다시 사용할 수 있는 이러한 스크립트의 hello 더 나은 예 중 하나 Linux toopool 디스크에는 RAID를 설정 하 고 IOPS 수를 더 얻을 수 있습니다. Hello VM에에서 설치 되 고 hello 소프트웨어에 관계 없이이 스크립트는 일반적인 시나리오에 대해 검증 된 사례를 다시 사용할을 제공 합니다.

![재사용이 가능한 스크립트](./media/best-practices-resource-manager-design-templates/reusable-scripts.png)

**멤버 리소스 템플릿은 광범위한 재사용이 가능한 스크립트를 호출할 수 있습니다.**

### <a name="custom-scripts"></a>사용자 지정 스크립트
템플릿은 일반적으로 VM 내에 소프트웨어를 설치 및 구성하는 스크립트를 하나 이상 호출합니다. 하나 이상의 멤버 유형의 여러 인스턴스가 배포되는 큰 토폴로지에서 일반적인 패턴이 보입니다. 설치 스크립트가 병렬 실행이 가능한 모든 VM에 대해 시작되고 모든 VM(또는 지정된 멤버 유형의 모든 VM)이 배포된 후에 호출되는 설정 스크립트가 그 뒤를 따릅니다.

![사용자 지정 스크립트](./media/best-practices-resource-manager-design-templates/custom-scripts.png)

**멤버 리소스 템플릿은 VM 구성 같은 특정 목적을 위한 스크립트를 호출할 수 있습니다.**

## <a name="capability-scoped-solution-template-example---redis"></a>기능 범위 솔루션 템플릿 예 - Redis
tooshow는 구현을 작용 수 하는 방법에 대해 살펴보겠습니다 실제 예의 hello 배포 및 구성 표준 티셔츠 크기에 Redis 용이 하 게 하는 템플릿을 작성 합니다.  

Hello 배포에 대 한 공유 리소스 (가상 네트워크, 저장소 계정, 가용성 집합) 및 선택적 리소스 (jumpbox) 집합이 있습니다. 티셔츠 크기(대, 중, 소)로 표시되지만 각각 단일 노드 유형을 포함하는 여러 개의 알려진 구성이 있습니다. 또한 특정 목적에 따른 스크립트(설치, 구성)가 두 개 있습니다.

### <a name="creating-hello-template-files"></a>Hello 서식 파일 만들기
이름이 azuredeploy.json인 기본 템플릿을 만듭니다.

이름이 shared-resources.json인 공유 리소스 템플릿을 만듭니다.

Jumpbox_enabled.json 라는 jumpbox의 선택적 리소스 템플릿 tooenable hello 배포를 만들려면

Redis는 단일 노드 유형만을 사용하므로 이름이 node-resources.json인 단일 멤버 리소스 템플릿을 만듭니다.

Redis를와 함께 각 개별 노드 tooinstall 사용 하려면 고 hello 클러스터를 설정 합니다.  스크립트 tooaccommodate hello 설치 하 고 redis-클러스터-install.sh 및 redis-클러스터-setup.sh 설정 합니다.

### <a name="linking-hello-templates"></a>Hello 템플릿 연결
Hello 가상 네트워크를 설정 하는 toohello 공유 리소스 템플릿 아웃 hello 주 템플릿 연결 서식 파일 링크를 사용 합니다.

논리는 jumpbox 배포할지 여부를 hello 템플릿 toospecify의 hello 주 템플릿 tooenable 소비자 내에서 추가 됩니다. *활성화* hello에 대 한 값 *EnableJumpbox* hello 고객이 toodeploy는 jumpbox 해당 매개 변수를 나타냅니다. 이 값을 제공 하는 경우 hello 템플릿 연결 *_enabled* hello jumpbox 기능에 대 한 접미사 tooa 기본 서식 파일 이름으로 합니다.

hello 주 템플릿 적용 hello *큰* 매개 변수 값에 접미사 tooa 기본 서식 파일 이름을 한 티셔츠 크기 및 사용 합니다 아웃 템플릿 링크에 값을 너무*technology_on_os_large.json*합니다.

hello 토폴로지는이 그림을 유사 합니다.

![Redis 템플릿](./media/best-practices-resource-manager-design-templates/redis-template.png)

**Redis 템플릿에 대한 템플릿 구조**

### <a name="configuring-state"></a>구성 상태
Hello hello 클러스터의 노드에 대 한 두 가지 단계가 tooconfiguring hello 상태, 모두 용도 특정 스크립트로 표시 합니다.  Redis "redis 클러스터 install.sh" 설치 하 고 "redis 클러스터 setup.sh" hello 클러스터를 설정 합니다.

### <a name="supporting-different-size-deployments"></a>갖가지 크기의 배포 지원
Hello 티셔츠 크기 템플릿 변수 내 각 유형의 노드에 hello 수를 지정 toodeploy hello에 대 한 지정 된 크기 (*큰*). 해당 개수 까지의 숫자 시퀀스 번호는 노드 이름을 추가 하 여 고유한 이름을 tooresources를 제공 하는 리소스 루프를 사용 하 여 VM 인스턴스를 다음 배포 *copyIndex()*합니다. Hello 티셔츠 이름 서식 파일에 정의 된 대로 두 핫 및 웜 영역 Vm에 대 한 이러한 단계 수행

## <a name="decomposition-and-end-to-end-solution-scoped-templates"></a>분해 및 종단간 솔루션 범위 템플릿
종단간 솔루션 범위를 포함하는 솔루션 템플릿은 종단간 솔루션을 제공하는데 중점을 둡니다.  일반적으로 이 접근 방식은 추가적인 리소스, 논리 및 상태를 포함하는 복수의 기능 범위 템플릿의 컴퍼지션입니다.

Hello 이미지 아래에 강조 표시 된 대로 hello 기능 범위가 지정 된 서식 파일에 사용 되는 동일한 모델에 대해 확장 되는 종단 간 솔루션 범위를 사용 하 여 템플릿을 합니다.

리소스 템플릿을 공유 및 선택적 리소스 템플릿을 제공 hello hello 용량 및 기능에서와 같이 동일한 함수 템플릿 접근 방식을 범위 하지만 hello 끝 tooend 솔루션에 대 한 범위가 지정 됩니다.

범위 끝 tooend 솔루션 템플릿은 일반적으로 가질 수 티셔츠 크기, hello 구성 리소스 알려진 서식 파일은 hello 솔루션의 지정 된 알려진된 구성에 필요한를 반영.

hello로 알려진 구성 리소스 템플릿 링크 tooone 또는 더 많은 기능에는 관련 toohello 엔드 tooend 솔루션 및 hello hello 끝 tooend 솔루션에 필요한 멤버 리소스 템플릿 솔루션 템플릿을 범위가 제한 됩니다.

Hello로 알려진 구성 리소스 템플릿 내에 있는 변수는 사용 되는 tooprovide hello 적절 한 값 범위는 다운스트림 기능 솔루션에 대 한 hello 티셔츠 크기 hello 솔루션의 다른 템플릿보다 hello 개별 기능 범위 만큼 템플릿 toodeploy hello 적절 한 티셔츠 크기입니다.

![종단간](./media/best-practices-resource-manager-design-templates/end-to-end.png)

**용량에 대 한 hello 모델을 사용 또는 끝 tooend 솔루션 템플릿 범위에 대 한 범위 지정 기능이 솔루션 템플릿을 쉽게 확장할 수 있습니다.**

## <a name="preparing-templates-for-hello-marketplace"></a>마켓플레이스 hello에 대 한 템플릿 준비
hello 접근 방식을 쉽게 앞 시나리오 기업과 SIs, Csv 원하는 tooeither hello 템플릿을 직접 배포 하거나 자체적으로 자신의 고객 toodeploy 사용 위치를 수용 합니다.

또 다른 원하는 시나리오 hello 마켓플레이스를 통해 서식 파일은 배포입니다.  이 분해 방법은 hello 마켓플레이스도 몇 가지 사소한 변경으로 작동합니다.

이전에 설명한 것 처럼 템플릿 hello 시장에 판매에 대 한 고유 배포 유형을 사용 하는 toooffer 될 수 있습니다. 고유 배포 유형은 티셔츠 크기(대, 중, 소), 제품/대상 그룹 유형(커뮤니티, 개발자, 엔터프라이즈) 또는 기능 유형(기본, 고가용성)이 될 수 있습니다.

기존 끝 tooend, 다음과 같이 hello로 솔루션 또는 범위가 지정 된 서식 파일을 쉽게 수 용량 toolist hello 다른 알려진된 구성을 hello 시장에서 활용.

hello toohello 주 템플릿 매개 변수는 처음 수정 tooremove hello tshirtSize 라는 인바운드 매개 변수입니다.

Hello 고유한 배포 형식이 매핑되는 toohello로 알려진 구성 리소스 템플릿, 해야 hello 공용 리소스 및 구성에서 찾을 수 하는 동안 공유 리소스 서식 파일 요소와 잠재적으로 선택적 리소스 템플릿 hello 합니다.

서식 파일 toohello 마켓플레이스 toopublish을 원하는 경우 tshirtSize tooa 변수의 인바운드 매개 변수에 사용할 수 있는 hello 템플릿 내에 포함 된 이전에 hello를 대체 하는 기본 서식 파일의 사본을 각각 설정 합니다.

![마켓플레이스](./media/best-practices-resource-manager-design-templates/marketplace.png)

**Hello marketplace에 대 한 템플릿을 범위는 솔루션을 위해 조정**

## <a name="next-steps"></a>다음 단계
* 내부 / 외부로 템플릿 상태를 공유 하는 방법에 대 한 toolearn 참조 [상태에서 Azure 리소스 관리자 템플릿 공유](best-practices-resource-manager-state.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

