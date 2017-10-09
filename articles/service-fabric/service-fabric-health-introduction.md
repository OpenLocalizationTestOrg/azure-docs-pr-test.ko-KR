---
title: "서비스 패브릭에서 aaaHealth 모니터링 | Microsoft Docs"
description: "소개 toohello Azure 서비스 패브릭 상태 모니터링 hello 클러스터 및 응용 프로그램 및 서비스의 모니터링을 제공 하는 모델입니다."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>소개 tooService 패브릭 상태 모니터링
다양하고 유연하며 확장 가능한 상태 평가 및 보고 기능을 제공하는 상태 모델이 Azure 서비스 패브릭에 도입되었습니다. hello 모델 hello 상태에서 실행 되는 hello 서비스 및 hello 클러스터 근처 실시간 모니터링할 수 있습니다. 간편하게 상태 정보를 얻을 수 있고 잠재적인 문제로 인한 대규모 중단 사태가 발생하기 전에 해당 문제를 해결할 수 있습니다. Hello 일반적인 모델에서 서비스의 로컬 뷰를 기반으로 보고서를 보내고 정보를 집계 tooprovide 전반적인 클러스터 수준 보기.

서비스 패브릭 구성 요소는 현재 상태로 풍부한 상태 모델 tooreport이를 사용합니다. 에서는 응용 프로그램에서 동일한 메커니즘 tooreport 상태 hello 합니다. 사용자 지정 조건을 캡처하는 고품질의 상태 보고에 투자하면 실행 중인 응용 프로그램에 대한 문제를 훨씬 더 쉽게 감지하고 수정할 수 있습니다.

hello 다음 Microsoft Virtual Academy 비디오는 hello 서비스 패브릭 상태 모델 및 사용 방법에 설명 합니다.<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> Hello 상태 하위 시스템 tooaddress 모니터링 되는 업그레이드에 대 한 필요성을 시작 했습니다. 서비스 패브릭 전체 가용성, 가동 중지 시간 및 최소 toono 사용자 개입을 보장 하는 모니터링 된 응용 프로그램 및 클러스터 업그레이드를 제공 합니다. 이러한 목표를 hello 업그레이드 검사 상태에 따라 tooachieve 업그레이드 정책 구성. 상태가 바람직한 임계값에 부합하는 경우에만 업그레이드를 진행할 수 있습니다. 그렇지 않으면 hello 업그레이드 하거나 자동으로 롤백됩니다 또는 toogive 관리자 기회 toofix hello 문제를 일시 중지 합니다. 응용 프로그램 업그레이드에 대해 자세히 toolearn 참조 [이 여기서](service-fabric-application-upgrade.md)합니다.
> 
> 

## <a name="health-store"></a>Health 스토어
hello 상태 저장소 쉽게 검색 및 평가 대 한 hello 클러스터의 엔터티에 대 한 상태 관련 정보를 유지합니다. 서비스 패브릭 유지 상태 저장 서비스 tooensure 고가용성 및 확장성 구현 됩니다. hello 상태 저장소의 일부인 hello **패브릭: / 시스템** 응용 프로그램, 그리고 그 되어 실행 되 고 hello 클러스터가 실행 중이 경우에 사용할 수 있습니다.

## <a name="health-entities-and-hierarchy"></a>상태 엔터티 및 계층 구조
hello 상태 엔터티를 캡처하는 서로 다른 엔터티 간 종속성 및 상호 작용 논리적 계층 구조로 구성 됩니다. hello 상태 저장소 상태 엔터티 및 서비스 패브릭 구성 요소에서 받은 보고서에 기반 하는 계층 구조를 자동으로 작성 합니다.

hello 상태 엔터티 hello 서비스 패브릭 엔터티를 반영합니다. (예를 들어 **상태 응용 프로그램 엔터티** 응용 프로그램 인스턴스를 일치을 hello 클러스터에 배포 하는 동안 **상태 노드 엔터티** 일치 서비스 패브릭 클러스터 노드입니다.) hello 상태 계층 구조의 캡처 hello 간의 상호 작용 하며 hello 시스템 엔터티는 고급 상태 평가 대 한 hello 기반입니다. [서비스 패브릭 기술 개요](service-fabric-technical-overview.md)에서 주요 서비스 패브릭 개념에 대해 알아볼 수 있습니다. 응용 프로그램에 대한 자세한 내용은 [서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md)을 참조하세요.

hello 상태 엔터티 및 계층 구조 hello 클러스터와 응용 프로그램 toobe 효과적으로 보고, 디버깅 및 모니터링을 허용 합니다. hello 상태 모델이 정확한, 제공 *세부적인* 의 hello 상태의 표현을 hello hello 클러스터에 이동 많습니다.

![상태 엔터티.][1]
hello 상태 엔터티를 부모-자식 관계를 기반으로 계층 구조로 구성 됩니다.

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

hello 상태 엔터티는:

* **클러스터**. 서비스 패브릭 클러스터의 hello 상태를 나타냅니다. 클러스터 상태 보고서 hello 전체 클러스터에 영향을 주는 조건에 설명 합니다. 이러한 조건은 hello 클러스터 또는 hello 클러스터 자체의 여러 엔터티를 영향을 줍니다. Hello 보고자 hello 조건에 따라, 아래쪽 tooone 또는 비정상적인 자식 hello 문제를 축소할 수는 없습니다. Hello 뇌 toonetwork 분할 또는 통신 문제로 인해 분할 hello 클러스터의 예로 있습니다.
* **노드**. 서비스 패브릭 노드의 hello 상태를 나타냅니다. 노드 상태 보고서 hello 노드 기능에 영향을 주는 조건에 설명 합니다. 일반적으로에서 실행 중인 모든 배포 된 hello 엔터티에 영향을 줍니다. 예를 들면 노드에 디스크 공간(또는 메모리, 연결 등 기타 컴퓨터 전반적인 속성)이 부족하거나 노드가 다운되는 경우가 포함됩니다. hello 노드 엔터티 hello 노드 이름 (문자열)으로 식별 됩니다.
* **응용 프로그램**. Hello hello 클러스터에서 실행 중인 응용 프로그램 인스턴스 상태를 나타냅니다. 응용 프로그램 상태 보고 조건을 hello에 영향을 주는 설명 hello 응용 프로그램의 전반적인 상태입니다. (서비스 또는 배포 된 응용 프로그램) tooindividual 자식 좁힐 수 없습니다. 예를 들면 hello 응용 프로그램의 서로 다른 서비스 간의 hello 종단 간 상호 작용 합니다. hello 응용 프로그램 엔터티 hello 응용 프로그램 이름 (URI)으로 식별 됩니다.
* **서비스**. Hello 클러스터에서 실행 되는 서비스의 hello 상태를 나타냅니다. 서비스 상태를 보고 조건을 hello에 영향을 주는 설명 hello 서비스의 전반적인 상태입니다. hello 보고자 hello 문제 tooan 비정상 파티션 또는 복제를 좁힐 수 없습니다. 예를 들면 모든 파티션에 대해 문제를 일으키는 서비스 구성(포트 또는 외부 파일 공유 등)이 포함됩니다. hello 서비스 이름 (URI)으로 hello 서비스 엔터티 식별 됩니다.
* **파티션**. 서비스 파티션이 hello 상태를 나타냅니다. 파티션 상태 보고서 hello 전체 복제 세트에 영향을 주는 조건에 설명 합니다. 쿼럼 손실에서 되는 경우 및 hello 복제본 수가 대상 개수 보다 낮으면을 예로 들 수 있습니다. hello 파티션 엔터티 hello 파티션 ID (GUID)로 식별 됩니다.
* **복제본**. 상태 저장 서비스 복제본 또는 상태 비저장 서비스 인스턴스의 hello 상태를 나타냅니다. hello 복제본은 hello watchdogs 및 시스템 구성 요소에서 응용 프로그램에 대해 보고할 수 있는 가장 작은 단위입니다. 상태 저장 서비스에 대 한 예로 주 복제본 작업 toosecondaries 및 느린 복제 복제할 수 없는 있습니다. 또한 상태 비저장 인스턴스는 리소스 부족 또는 연결 문제가 있는 경우에 보고할 수 있습니다. hello 복제 항목 (long) hello 파티션 ID (GUID) 및 hello 복제본 또는 인스턴스 ID로 식별 됩니다.
* **DeployedApplication**. 나타냅니다 hello의 상태는 *노드에서 실행 되는 응용 프로그램*합니다. 배포 응용 프로그램 상태 보고서 hello에 배포 된 tooservice 패키지 좁힐 수 없는 hello 노드에서 조건 특정 toohello 응용 프로그램에 설명 동일한 노드. 예로 응용 프로그램 패키지를 다운로드 하 여 해당 노드에서 없습니다 및 hello 노드에서 응용 프로그램 보안 주체를 설정 하는 문제 오류가 있습니다. 배포 된 hello 응용 프로그램은 응용 프로그램 이름 (URI) 및 노드 이름 (문자열)으로 식별 됩니다.
* **DeployedServicePackage**. Hello 클러스터의 노드에서 실행 되는 서비스 패키지의 hello 상태를 나타냅니다. Hello에 hello 영향을 미치지 않는 조건 특정 tooa 서비스 패키지를 다른 서비스 패키지 설명 hello에 대 한 동일한 노드에 동일한 응용 프로그램입니다. 예를 들면 시작할 수 없는 hello 서비스 패키지 및 읽을 수 없는 구성 패키지의 코드 패키지입니다. 배포 된 hello 서비스 패키지 응용 프로그램 이름 (URI), 노드 이름 (문자열), 서비스 매니페스트 이름 (문자열) 및 서비스 패키지 활성화 ID (문자열)으로 식별 됩니다.

hello 상태 모델의 hello 세분성을 사용 하면 쉽게 toodetect 및 문제를 수정할 수 있습니다. 예를 들어 서비스가 응답 하지 않는 경우을 응용 프로그램 인스턴스가 hello tooreport 손상 되었습니다. 하지만 보고에 수준 아닌지 방식이 적절 hello 문제 해당 응용 프로그램 내의 모든 hello 서비스 영향 수도 있습니다. hello 보고서 방법은 toothat 파티션 하는 경우 적용 된 toohello 비정상적인 서비스 또는 tooa 특정 자식 파티션 여야 합니다. hello 데이터 자동으로 hello 계층 구조를 통해 화면 및 비정상 파티션 이루어집니다 표시 서비스 및 응용 프로그램 수준에서. 이 집계 toopinpoint 주며 보다 신속 하 게 hello 문제의 hello 근본 원인을 해결 합니다.

hello 상태 계층 구조의 부모-자식 관계가 구성 됩니다. 클러스터는 노드 및 응용 프로그램으로 구성됩니다. 응용 프로그램에는 서비스 및 배포된 응용 프로그램이 포함됩니다. 배포된 응용 프로그램에는 배포된 서비스 패키지가 포함됩니다. 서비스에는 파티션이 있고 각 파티션에는 하나 이상의 복제본이 있습니다. 노드 및 배포된 엔터티 간에는 특수한 관계가 있습니다. 비정상 노드 해당 기관 시스템 구성 요소, hello Failover Manager service가 보고에 영향을 줍니다 hello 배포 응용 프로그램, 서비스 패키지 및 복제본에 배포 합니다.

hello 상태 계층 구조는 거의 실시간 정보 인 hello 최신 상태 보고서를 기반으로 hello 시스템의 hello 최신 상태를 나타냅니다.
내부 및 외부 watchdogs 응용 프로그램별 논리 또는 사용자 지정 모니터링 대상된 상태에 따라 동일한 엔터티 hello에 보고할 수 있습니다. 사용자의 보고 hello 시스템 보고서 함께 사용할 수 있습니다.

큰 클라우드 서비스의 hello 중 toohealth tooreport 및 응답을 디자인 하는 방법에 대 한 tooinvest를 계획 합니다. 이 사전 investement hello 서비스 쉽게 toodebug을, 모니터링 하 고 작업을 만듭니다.

## <a name="health-states"></a>성능 상태
서비스 패브릭 인지 엔터티가 정상 상태 상태 toodescribe 세 가지 사용 하 여: 확인, 경고 및 오류입니다. 모든 보고서가 전송 toohello 상태 저장소 이러한 상태 중 하나를 지정 해야 합니다. hello 상태 계산 결과 이러한 상태 중 하나입니다.

가능한 hello [상태](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate) 됩니다.

* **확인**. hello 엔터티는 정상입니다. 엔터티 또는 자식(해당하는 경우)에 대해 보고된 알려진 문제가 없습니다.
* **경고**. hello 엔터티에 포함 된 몇 가지 문제가 있지만 올바르게 여전히 작동할 수 있습니다. 예를 들어, 지연이 있으나 아직 기능상의 문제는 없습니다. 경우에 따라 hello 경고 조건이 해결 될 수도 있습니다 자체 외부 개입 없이 합니다. 이러한 경우 상태 보고서는 알림을 전달하고 상황에 대한 정보를 제공합니다. 다른 경우 사용자 개입 없이 심각한 문제가 발생 hello 경고 조건이 저하 될 수 있습니다.
* **오류**. hello 엔터티 손상 되었습니다. 제대로 작동 하기 때문에 동작 hello 엔터티의 toofix hello 상태를 수행 해야 합니다.
* **알 수 없음**. hello 엔터티 hello health store에서 존재 하지 않습니다. 여러 구성 요소에서 결과 병합 하는 hello 분산 쿼리에서이 결과 얻을 수 있습니다. 예를 들어 hello get 노드 목록 쿼리 라인 너무**FailoverManager**, **ClusterManager**, 및 **HealthManager**; 응용 프로그램을 목록 쿼리 너무 라인 **ClusterManager** 및 **HealthManager**합니다. 이들 쿼리는 여러 시스템 구성 요소의 결과를 병합합니다. Health store에서 존재 하지 않는 엔터티를 반환 하는 다른 시스템 구성 요소 hello 병합 된 결과 알 수 없는 상태입니다. 엔터티는 아직 처리 되지 않은 상태 보고서 또는 hello 엔터티 삭제 후에 정리 하기 때문에 저장소에 없습니다.

## <a name="health-policies"></a>상태 정책
상태 정책을 toodetermine 엔터티는 보고서 및 자식 함수에 따라 정상 여부를 적용 하는 hello 상태 저장소입니다.

> [!NOTE]
> 상태 정책 (대 한 상태 평가 클러스터 및 노드가) 클러스터 매니페스트에 hello 또는 (에 대 한 응용 프로그램 평가 및 해당 자식) hello 응용 프로그램 매니페스트에서 지정할 수 있습니다. 또한 해당 평가에만 사용되는 사용자 지정 상태 평가 정책에서 상태 평가 요청을 전달할 수도 있습니다.
> 
> 

기본적으로 서비스 패브릭 hello 부모-자식 계층 관계에 대 한 (모든 정상 상태 여야 합니다)는 엄격한 규칙을 적용 합니다. 한 비정상 이벤트 hello 자식 중 하나라도 있으면 hello 부모 비정상으로 간주 됩니다.

### <a name="cluster-health-policy"></a>클러스터 상태 정책
hello [클러스터 상태 정책](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy) 사용 되는 tooevaluate hello 클러스터 상태 상태와 노드 상태가 됩니다. 클러스터 매니페스트에 hello hello 정책을 정의할 수 있습니다. 표시 되지 않으면 hello 기본 정책 (허용된 실패 횟수 0)이 사용 됩니다.
hello 클러스터 상태 정책에 포함 되어 있습니다.

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror). 상태 평가 중 tootreat 경고 상태를 오류로 보고할지 여부를 지정 합니다. 기본값: false입니다.
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications). Hello 할 수 있는 정상 hello 클러스터 오류가 간주 되기 전에 응용 프로그램의 최대 허용된 비율을 지정 합니다.
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes). Hello 할 수 있는 정상 hello 클러스터 오류가 간주 되기 전에 노드의 최대 허용된 비율을 지정 합니다. 대규모 클러스터의 일부 노드는 항상 아래쪽 아웃 복구에 대 한 하므로이 백분율 되어야 하거나 구성 된 tootolerate입니다.
* [ApplicationTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap). 클러스터 상태 평가 toodescribe 특별 한 응용 프로그램 종류 중 hello 응용 프로그램 종류 상태 정책 맵을 사용할 수 있습니다. 기본적으로 모든 응용 프로그램은 풀에 배치되고 MaxPercentUnhealthyApplications를 사용하여 평가됩니다. 일부 응용 프로그램 종류는 다르게 처리 해야, 하면 hello 전역 풀에서 가져올 수 있습니다. 대신, 해당 응용 프로그램 종류 이름 hello 맵에서 관련 된 hello 백분율에 대해 평가 됩니다. 예를 들어 클러스터에는 다양한 유형의 응용 프로그램 수천 개와 특수 응용 프로그램 유형의 제어 응용 프로그램 인스턴스가 약간 있습니다. hello 제어 응용 프로그램 오류에 안 됩니다. 일부 오류 글로벌 MaxPercentUnhealthyApplications too20 %tootolerate 지정할 수는 있지만 hello에 대 한 응용 프로그램 종류 "ControlApplicationType" hello MaxPercentUnhealthyApplications too0를 설정 합니다. 이 이렇게 하면 일부 hello 많은 응용 프로그램이 정상 상태가 아닌, 있지만 hello 전역 비정상 백분율, 이하인 hello 클러스터 것 tooWarning를 평가 합니다. 경고 상태는 클러스터 업그레이드 또는 오류 상태에 의해 트리거되는 기타 모니터링에 영향을 주지 않습니다. 하지만 오류가 하나라도 제어 응용 프로그램 하 게 만드는 클러스터 비정상 hello 업그레이드 구성에 따라 hello 클러스터 업그레이드를 일시 중지 또는 롤백을 트리거합니다.
  Hello 지도에 정의 된 hello 응용 프로그램 형식에 대 한 모든 응용 프로그램 인스턴스는 응용 프로그램의 hello 전역 풀에서 수행 됩니다. Hello에서 특정 MaxPercentUnhealthyApplications 지도 hello를 사용 하 여, hello hello 응용 프로그램 종류의 응용 프로그램의 총 수에 따라 평가 됩니다. Hello 응용 프로그램의 모든 hello 나머지 hello 전역 풀에 남아 있으며 MaxPercentUnhealthyApplications를 사용 하 여 확인 됩니다.

다음 예제는 hello 클러스터 매니페스트 발췌 구문입니다. hello 응용 프로그램의 toodefine 항목 맵을 접두사 hello 매개 변수 이름이 "ApplicationTypeMaxPercentUnhealthyApplications-"로, hello 응용 프로그램 유형 이름 다음을 입력 합니다.

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>응용 프로그램 상태 정책
hello [응용 프로그램 상태 정책](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy) 응용 프로그램 및 해당 하위 항목에 대 한 이벤트 및 하위 상태는 집계의 hello 평가 수행 되는 방법에 대해 설명 합니다. Hello 응용 프로그램 매니페스트를 정의할 수 있습니다 **ApplicationManifest.xml**, hello 응용 프로그램 패키지에 있습니다. 지정 된 정책이 없는 경우 서비스 패브릭 hello 엔터티 상태 보고서 나 자식 hello 경고 또는 오류 상태에 있는 경우 정상 임을 가정 합니다.
hello 구성 가능한 정책은 다음과 같습니다.

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx). 상태 평가 중 tootreat 경고 상태를 오류로 보고할지 여부를 지정 합니다. 기본값: false입니다.
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications). 할 수 있는 정상 hello 응용 프로그램 오류에 간주 되기 전에 배포 된 응용 프로그램의 트랜잭션당 hello 최대 비율을 지정 합니다. 이 비율은 hello hello 응용 프로그램은에 현재 배포 된 hello 클러스터의 노드 수를 통해 배포 된 비정상 응용 프로그램의 hello 수를 분할 하 여 계산 됩니다. hello 계산 노드 중 작은 번호에 대 한 오류 tootolerate로 반올림합니다. 기본 비율: 0.
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy). Hello 기본 서비스 유형을 상태 정책 hello 응용 프로그램의 모든 서비스 형식에 대 한 기본 상태 정책을 hello 대체를 지정 합니다.
* [ServiceTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap). 서비스 유형별 서비스 상태 정책의 맵을 제공합니다. 이러한 정책에는 각 지정 된 서비스 유형에 대 한 hello 기본 서비스 유형을 상태 정책을 대체합니다. 예를 들어 응용 프로그램에 상태 비저장 게이트웨이 서비스 유형 및 상태 저장 엔진 서비스 유형의 계산에 대 한 상태 정책을 hello를 다르게 구성할 수 있습니다. 정책 당 서비스 종류를 지정 하면 hello 서비스의 상태를 hello 더 세부적으로 제어를 얻을 수 있습니다.

### <a name="service-type-health-policy"></a>서비스 유형 상태 정책
hello [서비스 유형 상태 정책](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy) tooevaluate 및 집계 서비스 hello 하 고 서비스의 자식 hello 방법을 지정 합니다. hello 정책에 포함 되어 있습니다.

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice). 서비스가 비정상 간주 되기 전에 비정상 상태 파티션의의 트랜잭션당 최대 hello 비율을 지정 합니다. 기본 비율: 0.
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition). 파티션을 비정상 간주 되기 전에 비정상 복제본의 트랜잭션당 hello 최대 비율을 지정 합니다. 기본 비율: 0.
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices). Hello 응용 프로그램은 비정상 상태로 간주 되기 전에 비정상 상태 서비스의 트랜잭션당 hello 최대 비율을 지정 합니다. 기본 비율: 0.

다음 예제는 hello 응용 프로그램 매니페스트 발췌 구문입니다.

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>상태 평가
사용자 및 자동화된 서비스가 언제든지 엔터티의 상태를 평가할 수 있습니다. tooevaluate 엔터티 상태, hello 상태 저장소 집계 모든 상태 hello 엔터티를 보고 및이 모든 자식 (있는 경우)을 평가 하는 합니다. hello 상태 집계 알고리즘 tooevaluate 상태 보고서를 어떻게 하 고 tooaggregate 하위 상태 (있는 경우)를 명시 하는 방법을 지정 하는 상태 정책을 사용 합니다.

### <a name="health-report-aggregation"></a>상태 보고서 집계
하나의 엔터티에는 서로 다른 속성에 대해 서로 다른 보고자(시스템 구성 요소 또는 Watchdog)에서 보낸 여러 상태 보고서가 있을 수 있습니다. hello 집계 사용 하 여 연결 된 상태 정책을 hello, 특히 응용 프로그램의 ConsiderWarningAsError 구성원 hello 또는 클러스터 상태 정책 ConsiderWarningAsError 지정 방법을 tooevaluate 경고 합니다.

hello 집계 된 상태에 의해 트리거되는 hello *최악의* hello 엔터티 상태를 보고 합니다. 하나 이상의 오류 상태 보고서의 이면 hello 집계 된 상태는 오류입니다.

![오류 보고서가 있는 상태 보고서 집계.][2]

하나 이상의 오류 상태 보고가 있는 상태 엔터티는 오류로 평가됩니다. hello에 마찬가지입니다 해당 상태에 관계 없이 만료 된 상태 보고서.

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

하나 이상의 경고와 오류 보고서가 없는 경우 hello 집계 된 상태는 경고 또는 오류 hello ConsiderWarningAsError 정책 플래그에 따라.

![경고 보고서가 있고 ConsiderWarningAsError false인 상태 보고서 집계.][3]

경고 보고서와 ConsiderWarningAsError 상태 보고서 집계 toofalse (기본값)을 설정합니다.

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>자식 상태 집계
hello 엔터티의 집계 된 상태를 반영 hello 하위 상태 (있는 경우) 합니다. 하위 상태를 집계 하기 위한 hello 알고리즘 hello 상태 적용 가능한 정책은 해당 hello 엔터티 형식을 기반으로 사용 합니다.

![자식 엔터티 상태 집계.][4]

상태 정책에 따른 자식 집계.

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

상태 저장소 hello이 모든 hello 자식을 계산 후 해당 상태 비정상 자식의 hello 구성 된 최대 백분율을 기반으로 집계 됩니다. 이 백분율은 hello 엔터티 및 자식 형식을 기반으로 하는 hello 정책에서 가져옵니다.

* 모든 자식 항목 확인 상태 있으면 hello 집계는 자식 상태 확인입니다.
* 자식 및가 둘 다 확인 경고 상태 하는 경우 hello 자식 집계 상태가 경고 임 합니다.
* 오류 상태 모두 hello 최대 허용 되는 비정상 자식의 백분율을 고려 하지 않는 있는 자식에 없으면 hello 집계 된 상태는 오류입니다.
* 최대 오류 상태 존중 hello로 hello 자식 hello 허용 되는 백분율 비정상 자식의 경우 집계 된 상태 (경고).

## <a name="health-reporting"></a>상태 보고
시스템 구성 요소, 시스템 패브릭 응용 프로그램 및 내부/외부 Watchdog에서 Service Fabric 엔터티에 대해 보고할 수 있습니다. hello reporters 확인 *로컬* hello 상태를 모니터링 하 고 hello 조건에 따라 모니터링 hello 엔터티의으로 결정 합니다. 이러한 모든 전역 상태 또는 데이터를 집계 toolook이 필요 하지 않습니다. hello는 동작은 여러 가지 tooinfer에서 toolook 어떤 정보 toosend 해야 하는 복잡 하지 organisms toohave 간단한 reporters 원하는입니다.

toosend 상태 데이터 toohello 상태 저장소를 보고자 tooidentify hello 영향을 받는 엔터티 필요 하 고 상태 보고서를 만듭니다. toosend hello 보고서를 사용 하 여 hello [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API, Api hello에 노출 된 상태를 보고 `Partition` 또는 `CodePackageActivationContext` 개체, PowerShell cmdlet 또는 REST 합니다.

### <a name="health-reports"></a>상태 보고서
hello [상태 보고서](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport) 각 hello 클러스터의 hello 엔터티에 대 한 hello 다음 정보를 포함 합니다.

* **SourceId**. Hello 보고자 hello 상태 이벤트의 고유 하 게 식별 하는 문자열입니다.
* **엔터티 식별자**. Hello 엔터티 hello 보고서 적용 되는 위치를 식별 합니다. Hello에 따라 다릅니다 [엔터티 형식](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * 클러스터. 없음.
  * 노드. 노드 이름(문자열).
  * 응용 프로그램을 클릭합니다. 응용 프로그램 이름(URI). Hello 클러스터에 배포 된 hello 응용 프로그램 인스턴스의 hello 이름을 나타냅니다.
  * 서비스. 서비스 이름(URI). Hello 클러스터에 배포 된 hello 서비스 인스턴스의 hello 이름을 나타냅니다.
  * 파티션. 파티션 ID(GUID). Hello 파티션 고유 식별자를 나타냅니다.
  * 복제본. hello 상태 저장 서비스 복제본 ID 또는 hello 상태 비저장 서비스 인스턴스 ID (입니다 INT64).
  * DeployedApplication. 응용 프로그램 이름(URI) 및 노드 이름(문자열).
  * DeployedServicePackage. 응용 프로그램 이름(URI), 노드 이름(문자열) 및 서비스 매니페스트 이름(문자열).
* **속성**. A *문자열* (고정된 열거 되지) 수 있도록 해 주는 hello 보고자 toocategorize hello 상태 hello 엔터티의 특정 속성에 대 한 이벤트입니다. 예를 들어 A 보고자 hello Node01 "Storage" 속성의 hello 상태를 보고할 수 있습니다 및 보고자 B hello Node01 "연결" 속성의 hello 상태를 보고할 수 있습니다. Hello health store에서 이러한 보고서는 Node01 엔터티 hello에 대 한 별도 상태 이벤트로 처리 됩니다.
* **설명**. 보고자 tooprovide 허용 하는 문자열 hello 상태 이벤트에 대 한 정보를 자세히 설명 합니다. **SourceId**, **속성**, 및 **HealthState** hello 보고서를 완전 하 게 설명 해야 합니다. hello 설명 hello 보고서에 대 한 사용자를 읽을 수 있는 정보를 추가합니다. hello 텍스트 toounderstand hello 상태 보고서 관리자와 사용자가 쉽게 있습니다.
* **HealthState**. [열거형](service-fabric-health-introduction.md#health-states) hello 보고서의 hello 성능 상태를 설명 하는 합니다. hello 사용 가능한 값은 정상, 경고 및 오류입니다.
* **TimeToLive**. Hello 상태 보고서 기간을 나타내는 시간 범위는 유효 합니다. 와 결합 되어 **RemoveWhenExpired**, hello 상태 저장소 tooevaluate 이벤트를 만료 하는 방법을 알 수 있습니다. 기본적으로 hello 값이 무한, 및 hello 보고서가 계속 유효 합니다.
* **RemoveWhenExpired**. 부울. 경우 tootrue 설정, hello 만료 된 상태 보고서가 자동으로 hello health store에서 제거 하 고 hello 보고서 엔터티 상태 평가 영향을 주지 않습니다. Hello 보고서 시간만 및 hello 보고자 지정한 기간 동안 유효한 경우에 사용 하지 않습니다 필요 tooexplicitly 채워지므로 삭제 해야 합니다. 또한 hello health store에서 toodelete 보고서 사용 (예를 들어는 watchdog 변경 되 고 이전 소스와 속성을 사용 하 여 보고서를 보내는 것을 중지) 합니다. Hello health store에서 이전 상태를 RemoveWhenExpired tooclear 함께 간단한 TimeToLive 사용 하 여 보고서에 보낼 수 있습니다. Hello 값 toofalse을 설정 하는 경우 hello 만료 된 보고서로 처리 됩니다 hello 상태 평가에서 오류. 값이 false hello toohello 상태 저장소 신호를이 속성에 해당 hello 소스 주기적으로 보고 해야 합니다. 그렇지 않은 경우 다음 있어야 문제가 있는 hello 감시 합니다. hello watchdog 상태를 오류로 hello 이벤트를 고려 하 여 캡처됩니다.
* **SequenceNumber**. Toobe 증가 해야 하는 양의 정수 hello 보고서의 hello 순서를 나타냅니다. Hello 상태 저장소 toodetect 오래 된 보고서에서 네트워크 지연을 또는 다른 문제로 인해 늦게 받은 사용 됩니다. Hello 시퀀스 번호 보다 작거나 같은 경우 보고서는 거부 동일한 엔터티, 소스 및 속성에 대 한 가장 최근에 적용 된 toohello 번호 hello 합니다. 지정 하지 않으면 hello 시퀀스 번호가 자동으로 생성 됩니다. 상태 전환에 대 한 보고 하는 경우에 필요한 tooput hello 시퀀스 번호에 유용 합니다. 이 경우 hello 소스 tooremember 보고서 전송 하 고 복구에 대 한 장애 조치 시 hello 정보를 유지 해야 합니다.

SourceId, 엔터티 식별자, 속성 및 HealthState의 4가지 정보는 모든 상태 보고서에서 필요합니다. 원본 Id 문자열 hello toostart hello 접두사로 사용할 수 없습니다 "**시스템**", 시스템 보고서에 대 한 예약 되어 있는 합니다. Hello에 대 한 동일한 엔터티 hello에 대 한 하나의 보고서가 동일한 소스와 속성입니다. 여러 보고서에 대 한 동일한 소스 hello 및 hello 상태 클라이언트 쪽 (일괄 처리 되) 하는 경우 또는 hello 상태 저장소 쪽 서로 속성 재정의 합니다. 시퀀스 번호를 기반으로 하는 hello 대체 더 높은 시퀀스 번호) (포함 하는 최신 보고서는 이전 보고서를 대체합니다.

### <a name="health-events"></a>상태 이벤트
Hello 상태 저장소를 유지 내부적으로 [상태 이벤트](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent), hello 보고서 및 추가 메타 데이터에서 모든 hello 정보를 포함 하는 합니다. hello 서버 쪽에서 수정 된 hello 시간과 hello 보고서 toohello 상태 클라이언트에 제공 된 hello 시간 hello 메타 데이터에 포함 되어 있습니다. hello 상태 이벤트에 반환한 [상태 쿼리 수](service-fabric-view-entities-aggregated-health.md#health-queries)합니다.

hello 추가 된 메타 데이터가 포함 되어 있습니다.

* **SourceUtcTimestamp**. hello 시간 hello 보고서 toohello 상태 클라이언트 (협정 세계시) 제공 되었습니다.
* **LastModifiedUtcTimestamp**. hello hello 보고서 시간 (협정 세계시) hello 서버 쪽에서 마지막으로 수정 된 합니다.
* **IsExpired**. A 플래그 tooindicate hello 보고서 hello 쿼리 hello 상태 저장소에 의해 실행 될 때 만료 된 여부. RemoveWhenExpired가 false인 경우에만 이벤트가 만료될 수 있습니다. 그렇지 않으면 hello 이벤트 쿼리에 의해 반환 되지 않습니다 고 hello 저장소에서 제거 됩니다.
* **LastOkTransitionAt**, **LastWarningTransitionAt**, **LastErrorTransitionAt**. hello 확인/경고/오류 전환에 대 한 마지막 시간입니다. 이러한 필드는 hello 이벤트에 대 한 hello 상태 상태 전환의 hello 기록을 제공합니다.

더 효율적인 경고 또는 이벤트 정보 "기록" 상태에 대 한 hello 상태 전환 필드를 사용할 수 있습니다. 따라서 다음과 같은 시나리오가 가능해집니다.

* 속성이 X분 넘게 경고/오류 상태일 때 알림. 일시적인 상태에 대해 경고를 방지 일정 기간에 대 한 hello 조건을 확인 합니다. 예를 들어 5 분에 대 한 hello 상태가 경고 되었습니다에 경고 번역할 수 있습니다 (HealthState 경고를 지금-LastWarningTransitionTime를 = = > 5 분)입니다.
* X 분 마지막 hello에서 변경 된 조건에만 경고 합니다. 보고서를가 이미 오류 hello 시간을 지정 하기 전에 이미 신호를 받은 이전에 때문에 무시할 수 있습니다.
* 속성이 경고와 오류 사이에 전환되고 있는 경우, 얼마나 오래 비정상(즉, 정상이 아닌 상태)이었는지 결정합니다. 예를 들어 5 분에 대 한 정상 hello 속성 되지 않았는지 경고 번역할 수 있습니다 (HealthState! = 정상, 이제-LastOkTransitionTime > 5 분)입니다.

## <a name="example-report-and-evaluate-application-health"></a>예: 응용 프로그램 상태 보고 및 평가
hello 다음 예제에서는 보내는 hello 응용 프로그램에서 PowerShell 통해 상태 보고서 **패브릭: / WordCount** hello 원본의 **MyWatchdog**합니다. hello 상태 보고서는 hello 상태 속성 "availability" 무한 TimeToLive와에서 오류 성능 상태에 대 한 정보를 포함합니다. 다음 hello 응용 프로그램 상태를 쿼리 상태 이벤트의 hello 목록에 대 한 상태 이벤트를 보고 집계 된 상태 상태 오류 및 hello를 반환 합니다.

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>상태 모델 사용
hello 상태 모델 hello 클러스터 내에서 여러 모니터 hello 간에 분포 되는 모니터링 및 상태 결정 하기 때문에 클라우드 서비스 및 서비스 패브릭 플랫폼 tooscale 원본으로 사용 하는 hello 허용 합니다.
다른 시스템에는 모든 hello를 구문 분석 하는 hello 클러스터 수준에서 단일 중앙 집중식된 서비스가 *잠재적으로* 유용한 정보를 서비스에서 내보내집니다. 이 방법으로 인해 확장성이 저하됩니다. 것도 하지 않습니다 허용 가능한 닫기 toohello 근본 원인으로 잠재적인 문제 및 문제를 식별 하는 toohelp toocollect 특정 정보입니다.

모니터링 및 진단에 대 한, 클러스터 및 응용 프로그램 상태를 평가 하기 위한 및 모니터링 되는 업그레이드에 대 한 hello 상태 모델 과도 하 게 사용 됩니다. 다른 서비스 상태 데이터 tooperform 자동 복구를 사용 하 여 클러스터 상태 기록 빌드하고 특정 조건에 경고를 생성 합니다.

## <a name="next-steps"></a>다음 단계
[서비스 패브릭 상태 보고서 보기](service-fabric-view-entities-aggregated-health.md)

[시스템 상태 보고서를 문제 해결에 사용](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[어떻게 tooreport 및 확인 서비스 상태](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[사용자 지정 서비스 패브릭 상태 보고서 추가](service-fabric-report-health.md)

[로컬로 서비스 모니터링 및 진단](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)

