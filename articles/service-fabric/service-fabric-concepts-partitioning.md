---
title: "서비스 패브릭 서비스 aaaPartitioning | Microsoft Docs"
description: "설명 방법을 toopartition 서비스 패브릭 상태 저장 서비스입니다. 데이터 및 계산 함께 배율을 조정할 수 있으므로 파티션을 hello 로컬 컴퓨터에 데이터 저장소를 수 있습니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>서비스 패브릭 Reliable Services 분할
이 문서에서는 소개 toohello 분할 신뢰할 수 있는 Azure 서비스 패브릭 서비스의 기본 개념을 제공 합니다. hello hello 문서에 사용 되는 소스 코드에서 사용할 수도 있습니다 [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)합니다.

## <a name="partitioning"></a>분할
분할은 고유 tooService 패브릭 하지 않습니다. 사실, 분할은 확장 가능한 서비스 구축의 코어 패턴입니다. 넓은 의미에서 상태 (데이터)로 나눈 개념으로 서 분할 하는 방법에 대 한 생각 하 고 더 작은 액세스할 수 있는 단위 tooimprove 확장성 및 성능에 계산 수 있습니다. 분할의 잘 알려진 양식은 [데이터 분할][wikipartition]로서 분할이라고도 합니다.

### <a name="partition-service-fabric-stateless-services"></a>서비스 패브릭 상태 비저장 분할 서비스
상태 비저장 서비스의 경우 하나 이상의 서비스의 인스턴스를 포함하는 논리 단위가 되는 파티션으로 생각할 수 있습니다. 그림 1에서는 하나의 파티션을 사용하는 클러스터에 분산된 5개의 인스턴스로 상태 비저장 서비스를 보여 줍니다.

![상태 비저장 서비스](./media/service-fabric-concepts-partitioning/statelessinstances.png)

실제로 두 종류의 상태 비저장 서비스 솔루션이 있습니다. hello 먼저 하나입니다 (예: hello 세션 정보 및 데이터를 저장 하는 웹 사이트)는 Azure SQL 데이터베이스에서 예를 들어 외부적으로 상태를 유지 하는 서비스. hello 두 번째 메서드는 모든 영구 상태를 관리 하지 않는 서비스 (예: 미리 보기 계산기 또는 이미지) 계산 전용입니다.

두 경우 모두 상태 비저장 서비스 분할은 매우 드문 시나리오이며 확장성 및 가용성은 일반적으로 더 많은 인스턴스를 추가하여 이루어집니다. 상태 비저장 서비스 인스턴스를 여러 파티션에 특별 한 라우팅 toomeet 해야 할 때 tooconsider 원하는 hello 유일한 시간을 요청 합니다.

한 예로 특정 범위의 ID가 있는 사용자가 특정한 서비스 인스턴스로만 제공되어야 하는 경우 고려합니다. 상태 비저장 서비스를 분할 수 때의 또 다른 예는 진정으로 분할 된 백 엔드 (예: 분할 된 SQL 데이터베이스) 있고 toocontrol 대상 서비스 인스턴스 해야 toohello 데이터베이스 분할 영역-쓰거나 내에서 다른 준비 작업을 수행 하려는 경우 hello 요구 하는 상태 비저장 서비스 hello 동일 hello 백 엔드에 사용 되는 정보를 분할 합니다. 이러한 유형의 시나리오는 다른 방법으로 해결될 수 있으며 서비스 분할이 반드시 필요하지 않습니다.

이 연습의 나머지 부분에서는 hello 상태 저장 서비스에 중점을 둡니다.

### <a name="partition-service-fabric-stateful-services"></a>서비스 패브릭 상태 저장 분할 서비스
서비스 패브릭을 사용 하면 쉽게 toodevelop 확장 가능한 상태 저장 서비스는 최상의 방법을 제공 하 여 toopartition 상태 (데이터). 개념적으로 생각해볼 수 있겠습니다 상태 저장 서비스의 파티션을 통해 매우 신뢰할 수 있는 확장 단위로 [복제본](service-fabric-availability-services.md) 분산 되 고 클러스터의 노드 hello에서 균형이 조정 합니다.

서비스 패브릭 상태 저장 서비스의 hello 컨텍스트에서 분할은 특정 서비스 파티션 hello 서비스의 전체 상태 hello의 일부에 대 한 책임 지는 결정 하는 toohello 프로세스를 말합니다. (앞서 언급했듯이 파티션은 [복제본](service-fabric-availability-services.md)의 집합입니다.) 서비스 패브릭에 대 한 훌륭한 점 hello 파티션을 서로 다른 노드에 배치 하는 합니다. 따라서 toogrow tooa 노드 리소스 제한이 있습니다. Hello 데이터 요구 사항이 증가, 파티션을 증가 하 고 서비스 패브릭 노드 간에 파티션이 변경 합니다. 이렇게 하면 hello 계속 하드웨어 리소스를 효율적으로 사용 합니다.

toogive 예를 들어 알고 계십니까 있습니다 5 노드 클러스터와 구성 된 toohave 10 파티션과 대상 세 개의 복제본은 서비스를 시작 합니다. 이 경우 서비스 패브릭은 균형을 조정 hello 복제본 hello 클러스터-분산 고 결국에 두 개의 주와 [복제본](service-fabric-availability-services.md) 노드당 합니다.
Hello 클러스터 too10 노드 tooscale, 필요 하면 서비스 패브릭은 균형을 다시 조정할 hello 기본 [복제본](service-fabric-availability-services.md) 10 모든 노드에 걸쳐 합니다. 마찬가지로, 백 too5 노드를 배율 조정 경우 서비스 패브릭은 균형을 다시 조정 모든 hello 복제본 hello 5 노드에서 합니다.  

그림 2는 10 개의 파티션의 hello 클러스터 크기 조정을 전후 hello 배포를 보여줍니다.

![상태 저장 서비스](./media/service-fabric-concepts-partitioning/partitions.png)

결과적으로, 클라이언트의 요청 된 컴퓨터에 분산 hello 응용 프로그램의 전체적인 성능이 향상 됩니다 하 고 데이터 액세스 toochunks 경합이 감소 hello 확장 이루어집니다.

## <a name="plan-for-partitioning"></a>분할에 대한 계획
서비스를 구현 하기 전에 항상 분할 전략을 아웃 필요한 tooscale hello를 고려해 야 합니다. 다양 한 방식으로 있지만 어떤 hello 일일이 tooachieve에 집중 모두. 이 문서의 hello 컨텍스트에 대해 생각해 봅시다 일부 hello 더 중요 한 측면입니다.

좋은 방법은 toothink toobe hello 첫 번째 단계로 분할 해야 하는 hello 상태의 hello 구조에 대 한 합니다.

간단한 예를 살펴봅시다. Toobuild countywide 설문 조사에 대 한 서비스 인 경우 hello 지방의 각 도시에 대 한 파티션을 만들 수 있습니다. 그런 다음 해당 toothat 도시는 hello 파티션에 hello 도시에 있는 모든 사람에 대 한 hello 투표를 저장할 수 있습니다. 그림 3에 존재 하는 사람 및 hello city의 집합을 보여 줍니다.

![간단한 파티션](./media/service-fabric-concepts-partitioning/cities.png)

도시, 000 명의 hello 다르거나 처럼 많은 양의 데이터 (예: Seattle)를 포함 하는 일부 파티션이 거의 상태 (예: Kirkland)와 다른 파티션에 있는 될 수 있습니다. 따라서 불균형 한 양의 상태를 사용 하 여 파티션을의 hello 영향이 무엇입니까?

Hello 예에 대 한 다시 생각 되 면 hello 시애틀에 대 한 응답을 보유 하는 hello 파티션 하나 hello Kirkland 보다 더 많은 트래픽을 받게 됩니다을 쉽게 확인할 수 있습니다. 서비스 패브릭에서는 있어야 hello에 대 한 기본적으로 동일한 수의 각 노드에서 기본 및 보조 복제본입니다. 노드의 어떤 복제본은 트래픽을 더 많이 처리하고 어떤 복제본은 트래픽을 더 적게 처리하게 됩니다. 이 경우 가급적 할 tooavoid 핫 및 콜드 스폿은 클러스터에서 다음과 같이 합니다.

이 tooavoid 주문에서 분할 관점에서 다음 두 가지를 수행 해야 합니다.

* 모든 파티션에 균등 하 게 분포 되도록 toopartition hello 상태를 보십시오.
* 각각 hello 서비스에 대 한 hello 복제본의 부하를 보고 합니다. (방법에 대한 자세한 정보는 이 문서의 [메트릭 및 부하](service-fabric-cluster-resource-manager-metrics.md)를 확인하세요). 서비스 패브릭 레코드의 수 또는 메모리 양 등의 서비스에서 사용 하는 hello 기능 tooreport 부하를 제공 합니다. Hello 메트릭을 보고에 따르면 서비스 패브릭 일부 파티션이 다른 항목 보다 높은 부하를 서비스 하 고 이동 복제본 toomore 적합 한 노드를 통해 hello 클러스터 변경 되도록 검색 전반적인 노드가 없습니다는 오버 로드 합니다.

때때로 지정된 파티션에 얼마나 많은 데이터가 있는지 알 수 없는 경우가 있으므로 일반적인 권장 사항은 두-toodo 이므로 먼저 분할 전략을 채택 하 여 하는 전체에 분산 hello 데이터 균등 하 게 hello 파티션 및 두 번째 보고 로드에서.  첫 번째 방법은 hello hello hello 둘째 데는 도움이 되지만 액세스 또는 부하에서 임시 차이 부드러운 시간이 지남에 따라 예제에서 투표에 설명 된 상황을 방지 합니다.

파티션 계획의 또 다른 측면에는 toochoose hello 올바른 수와 파티션 toobegin입니다.
서비스 패브릭 관점에서 시나리오의 예상 파티션 수보다 더 많은 파티션으로 시작하지 못할 이유는 없습니다.
실제로 가정 hello 최대 파티션 수는 올바른 방법입니다.

드물기는 하지만 처음에 선택한 것보다 더 많은 파티션이 필요하게 될 수도 있습니다. Hello 팩트 후 hello 파티션 수를 변경할 수 없습니다, 해야 tooapply 일부 고급 파티션 방법, 동일한 서비스 유형을 hello의 새 서비스 인스턴스를 만드는 등. 또한 tooimplement hello 라우팅하는 일부 클라이언트 쪽 논리가 toohello 올바른 서비스 인스턴스를 클라이언트 코드를 유지 해야 하는 클라이언트 정보에 따라를 요청 해야 합니다.

계획을 분할에 대 한 또 다른 고려 사항은 hello 사용할 수 있는 컴퓨터 리소스입니다. Hello 상태 toobe 액세스 하 고 저장 요구 사항에 맞춰, 바인딩된 toofollow 됩니다.

* 네트워크 대역폭 제한
* 시스템 메모리 제한
* 디스크 저장소 제한

따라서 실행 중인 클러스터의 리소스 제약 조건으로 실행 하는 경우는 것이 되나요? hello 대답은 간단히 hello 클러스터 tooaccommodate hello 새 요구 사항을 확장할 수입니다.

[hello 용량 계획 가이드](service-fabric-capacity-planning.md) 방법에 대 한 지침을 제공 toodetermine 얼마나 많은 노드를 클러스터 해야 합니다.

## <a name="get-started-with-partitioning"></a>분할 시작
이 섹션에서는 서비스를 분할 tooget 시작 하는 방법을 설명 합니다.

서비스 패브릭은 세 가지 파티션 체계를 제공합니다.

* 범위 지정된 분할(UniformInt64Partition이라고도 함)
* 이름 지정된 분할. 일반적으로 이 모델을 사용한 응용 프로그램에는 제한된 집합 내에 버킷 가능한 데이터가 있습니다. 이름 지정된 파티션 키로 사용되는 데이터 필드의 몇 가지 일반적인 예는 지역, 우편 번호, 고객 그룹 또는 기타 비즈니스 경계입니다.
* 단일 분할 단일 파티션이 hello 서비스 추가 라우팅가 필요 하지 않는 경우에 일반적으로 사용 됩니다. 예를 들어 상태 비저장 서비스는 기본적으로 이 파티션 체계를 사용합니다.

이름 지정된 분할 체계 및 단일 분할 체계는 범위 지정된 파티션의 특별한 형태입니다. 기본적으로 서비스 패브릭 사용에 대 한 Visual Studio 템플릿 hello 범위 분할을 hello 그대로 하나 가장 일반적이 고 유용 합니다. 이 문서의 나머지 부분에서는 hello hello 범위가 지정 된 파티션 구성표에 중점을 둡니다.

### <a name="ranged-partitioning-scheme"></a>범위 지정된 분할 체계
이 사용 되는 toospecify 정수 범위 (낮은 키와 높은 키로 식별) 및 (n) 파티션의 수입니다. 각각의 hello 겹치지 않는 하위 범위를 담당 n 파티션을 만듭니다 전체 키 범위를 분할 합니다. 예를 들어 하위 키 0, 상위 키 99 및 숫자 4로 범위 지정된 분할 체계는 다음과 같이 4개의 파티션을 만듭니다.

![범위 분할](./media/service-fabric-concepts-partitioning/range-partitioning.png)

일반적인 방법은 toocreate hello 데이터 집합 내에서 고유 키에 기반 하 여 해시 합니다. 키의 일부 일반적인 예로는 차량 식별 번호(VIN), 직원 ID 또는 고유 문자열을 들 수 있습니다. 이 고유 키를 사용 하 여 있습니다 다음 생성 된 해시 코드, 모듈러스 hello 키 범위, toouse 키로 합니다. Hello 상한 및 하 한의 hello 허용 되는 키 범위를 지정할 수 있습니다.

### <a name="select-a-hash-algorithm"></a>해시 알고리즘 선택
해시의 중요한 부분은 해시 알고리즘을 선택하는 것입니다. 고려 하는 것이 hello 목표 인지 (집약성 중요 한 해시)-서로 가까이 toogroup 유사한 키 또는 활동 (배포 해시) 하는 모든 파티션에 광범위 하 게 배포 되어야 합니다는 더 일반적입니다.

적절 한 배포 해시 알고리즘의 hello 특성에는 쉽게 toocompute, 몇 가지 충돌이 되며 hello 키 균등 하 게 분산은 합니다. 효율적인 해시 알고리즘의 좋은 예는 hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) 해시 알고리즘입니다.

일반 해시 코드 알고리즘 선택에 대 한 좋은 자료는 hello [해시 함수에 대 한 Wikipedia 페이지](http://en.wikipedia.org/wiki/Hash_function)합니다.

## <a name="build-a-stateful-service-with-multiple-partitions"></a>여러 파티션으로 상태 저장 서비스 구축
여러 파티션으로 첫 번째 신뢰할 수 있는 상태 저장 서비스를 만들어 보겠습니다. 이 예제에서는 작성 합니다 toostore 원하는 매우 간단한 응용 프로그램 hello에 문자 동일 hello로 시작 하는 성이 같은 파티션에 합니다.

모든 코드를 작성 하기 전에 hello 파티션과 파티션 키에 대 한 toothink을 해야 합니다. 에 대 한 (하나씩 hello 알파벳의 각 문자에 대 한) 26 파티션이 제공 하기는 하지만 필요 하면 낮은 임계값과 높은 키 hello?
문자 당 하나의 파티션을 toohave 문자 그대로 원하는 대로 사용할 수 있습니다 0 hello 낮은 키와 25로 hello 높은 키로 각 문자가 자체 키.

> [!NOTE]
> 이 실제로 hello 배포는 일정 하지 않게는 간단한 시나리오입니다. "S" 또는 "M"는 "X"로 시작 하는 hello 것 보다 일반적 hello 문자로 시작 하는 마지막 이름 또는 "Y"입니다.
> 
> 

1. **Visual Studio** > **파일** > **새로 만들기** > **프로젝트**를 엽니다.
2. Hello에 **새 프로젝트** 대화 상자에서 hello 서비스 패브릭 응용 프로그램을 선택 합니다.
3. "AlphabetPartitions" hello 프로젝트를 호출 합니다.
4. Hello에 **서비스를 만들** 대화 상자에서 선택 **Stateful** 서비스 및 hello 이미지 아래에 나와 있는 것 처럼 "Alphabet.Processing"을 호출 합니다.
       ![Visual Studio의 새 서비스 대화 상자][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Hello 파티션 수를 설정 합니다. 열기 hello Applicationmanifest.xml 파일 hello AlphabetPartitions 프로젝트 및 업데이트 hello 매개 변수 아래와 같이 Processing_PartitionCount too26 ApplicationPackageRoot 폴더를 hello에 있습니다.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    LowKey tooupdate hello와 ApplicationManifest.xml 아래와 같이 hello에 대 한 hello StatefulService 요소의 HighKey 속성이 필요 합니다.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Hello 서비스 toobe 액세스할 수 있는에 대 한 hello 아래와 같이 Alphabet.Processing 서비스에 대 한 (hello PackageRoot 폴더에 있음) ServiceManifest.xml의 hello 끝점 요소를 추가 하 여 포트에서 끝점을 엽니다.
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    이제 hello 서비스는 구성 된 toolisten 26 파티션과 tooan 내부 끝점입니다.
7. 다음으로, toooverride hello 해야 `CreateServiceReplicaListeners()` hello 처리 클래스의 메서드.
   
   > [!NOTE]
   > 이 샘플의 경우 간단한 HttpCommunicationListener를 사용하고 있다고 가정합니다. 신뢰할 수 있는 서비스 통신에 대 한 자세한 내용은 참조 하십시오. [hello 신뢰할 수 있는 서비스 통신 모델](service-fabric-reliable-services-communication.md)합니다.
   > 
   > 
8. 복제를 수신 하는 hello URL에 대 한 권장된 패턴은 형식에 따라 hello: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`합니다.
    따라서 원하는 tooconfigure 통신 수신기 toolisten hello 올바른 끝점에이 패턴을 사용 합니다.
   
    Hello에 호스트할 수는이 서비스의 여러 복제본이이 주소 toobe 고유 toohello 복제 하므로 동일한 컴퓨터. 이 때문에 파티션 ID + 복제본 ID hello URL에는 합니다. HttpListener는 hello hello URL 접두사는 고유으로 동일한 포트에서 주소에서 수신 대기할 수 있습니다.
   
    hello 추가 GUID는 보조 복제본이도 읽기 전용 요청을 수신 하는 고급 경우가 있습니다. 않은 hello 경우 원하는 toomake व न 기본 toosecondary tooforce 클라이언트 toore 해결 hello 주소에서 전환할 때 사용 되도록 합니다. '+' hello 주소를 여기 hello 복제 복 수신 대기 모든 사용 가능한 호스트 (예: IP, FQDM, localhost, 등) hello 코드 아래에 있도록 예를 보여 줍니다으로 사용 됩니다.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    또한 해당 hello 게시 URL을 확인 하는 것은 URL 접두사를 수신 대기 하는 hello과 약간 다릅니다.
    hello 수신 URL tooHttpListener 제공 됩니다. 게시 된 URL이 hello URL을 게시 된 toohello 서비스 패브릭 명명 서비스, 서비스 검색에 사용 되는 번호입니다. 클라이언트는 해당 검색 서비스를 통해 이 주소에 대해 요청합니다. 클라이언트 요구 toohave hello에 대 한 실제 IP 또는 FQDN hello 노드의 순서 tooconnect에서 발생 하는 hello 주소입니다. Tooreplace 필요는 '+'와 노드의 IP 또는 FQDN 같이 위의 hello 합니다.
9. hello 마지막 단계는 아래와 같이 논리 toohello 서비스 처리 tooadd hello입니다.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`읽기 값 hello 쿼리 문자열 매개 변수가 사용 toocall hello 파티션 및 호출 hello `AddUserAsync` tooadd hello lastname toohello 신뢰할 수 있는 사전 `dictionary`합니다.
10. 상태 비저장 서비스 toohello 프로젝트 toosee 추가해보겠습니다 어떻게 특정 파티션의 호출할 수 있습니다.
    
    이 서비스는 hello lastname 쿼리 문자열 매개 변수로 수락 하 고, hello 파티션 키를 결정 하며, 처리를 위해 toohello Alphabet.Processing 서비스로 전송 하는 간단한 웹 인터페이스로 사용 됩니다.
11. Hello에 **서비스를 만들** 대화 상자에서 선택 **Stateless** 서비스 하 고 아래와 같이 "Alphabet.Web"을 호출 합니다.
    
    ![상태 비저장 서비스 스크린 샷](./media/service-fabric-concepts-partitioning/createnewstateless.png)에서도 확인할 수 있습니다.
12. 아래 표시 된 대로 포트를 hello Alphabet.WebApi 서비스 tooopen의 hello ServiceManifest.xml의에서 hello 끝점 정보를 업데이트 합니다.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. Tooreturn hello 클래스 웹에서에서 ServiceInstanceListeners 집합이 필요합니다. 다시, 간단한 HttpCommunicationListener tooimplement를 선택할 수 있습니다.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. 이제 tooimplement hello 처리 논리가 필요 합니다. HttpCommunicationListener 호출 hello `ProcessInputRequest` 요청 제공 하는 경우. 따라서 계속 해 서 하 고 아래 hello 코드를 추가 합니다.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    단계 별로 안내하겠습니다. hello 코드 hello 첫 문자 hello 쿼리 문자열 매개 변수를 읽고 `lastname` char에 있습니다. 그런 다음,이 문자에 대 한 hello 파티션 키의 hello 16 진수 값을 빼는 방식으로 결정 `A` hello hello 성 첫 번째 문자의 16 진수 값에서 합니다.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    이 예제에서 파티션당 하나의 파티션 키를 가진 26개의 파티션을 사용합니다.
    Hello 서비스 파티션을 구한 다음으로, `partition` hello를 사용 하 여이 키에 대 한 `ResolveAsync` 메서드 hello `servicePartitionResolver` 개체입니다. `servicePartitionResolver` 는 다음으로 정의됩니다.
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    hello `ResolveAsync` 메서드는 hello 서비스 URI, hello 파티션 키와 매개 변수로 취소 토큰입니다. 처리 서비스는 hello에 대 한 서비스 URI를 hello `fabric:/AlphabetPartitions/Processing`합니다. 다음으로 hello 파티션의 hello 끝점을 구했습니다.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    마지막으로 hello 끝점 URL 및 hello 쿼리 문자열을 작성 하 고 처리 서비스는 hello를 호출 합니다.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    Hello 처리 작업이 완료 되 면에서는 쓰기 hello 출력 저장 합니다.
15. hello 마지막 단계는 tootest hello 서비스입니다. Visual Studio에서는 로컬 및 클라우드 배포에 대해 응용 프로그램 매개 변수를 사용합니다. 26 파티션과 로컬로 tootest hello 서비스 해야 tooupdate hello `Local.xml` 아래와 같이 hello AlphabetPartitions 프로젝트의 hello ApplicationParameters 폴더에 파일:
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. 배포를 마치면 hello 서비스와 모든 파티션에 hello 서비스 패브릭 탐색기에서에서 확인할 수 있습니다.
    
    ![서비스 패브릭 탐색기 스크린 샷](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. 브라우저에서 분할을 입력 하 여 hello를 테스트할 수 있습니다 `http://localhost:8081/?lastname=somename`합니다. 동일한 문자 hello 저장 되 고 hello로 시작 하 각 성 나타납니다 같은 파티션에 합니다.
    
    ![브라우저 스크린 샷](./media/service-fabric-concepts-partitioning/samplerunning.png)

hello 샘플의 hello 전체 소스 코드에서 사용할 수는 [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions)합니다.

## <a name="next-steps"></a>다음 단계
서비스 패브릭 개념에 대 한 정보를 보려면 hello 다음을 참조 하세요.

* [서비스 패브릭 서비스의 가용성](service-fabric-availability-services.md)
* [서비스 패브릭 서비스의 확장성](service-fabric-concepts-scalability.md)
* [서비스 패브릭 응용 프로그램의 용량 계획](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png