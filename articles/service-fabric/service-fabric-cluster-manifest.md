---
title: "aaaConfigure 독립 실행형 Azure 서비스 패브릭 클러스터 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 독립 실행형 또는 개인 서비스 패브릭 클러스터입니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>독립 실행형 Windows 클러스터에 대한 구성 설정
이 문서에서 설명 하는 방법을 사용 하 여 독립 실행형 서비스 패브릭 클러스터 tooconfigure hello ***ClusterConfig.JSON*** 파일입니다. 독립 실행형 프로그램에 대 한 hello 네트워크 토폴로지 장애/업그레이드 도메인의 관점에서 뿐만 아니라 hello 클러스터, hello 보안 구성에이 파일 toospecify 정보 hello 서비스 패브릭 노드 및 해당 IP 주소, 다른 유형의 노드를 사용할 수 있습니다. 클러스터입니다.

때 있습니다 [hello 독립 실행형 서비스 패브릭 패키지 다운로드](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), hello ClusterConfig.JSON 파일의 몇 가지 예제는 다운로드 한 tooyour 작업 컴퓨터입니다. 발생 하는 hello 샘플 *DevCluster* 이름에는 데 도움이 됩니다 hello 논리 노드 같이 동일한 컴퓨터에서 모든 세 개의 노드가 있는 클러스터를 만들 수 있습니다. 세 노드 중 하나 이상은 주 노드로 표시되어야 합니다. 이 클러스터는 개발 또는 테스트 환경에 유용하며, 프로덕션 클러스터로 지원되지 않습니다. 발생 하는 hello 샘플 *MultiMachine* 이름에 만들 수 있습니다는 프로덕션 품질 클러스터 각 노드에 별도 컴퓨터.

1. *ClusterConfig.Unsecure.DevCluster.JSON* 및 *ClusterConfig.Unsecure.MultiMachine.JSON* toocreate 안전 하지 않은 테스트 또는 프로덕션 각각 클러스터를 표시 합니다. 
2. *ClusterConfig.Windows.DevCluster.JSON* 및 *ClusterConfig.Windows.MultiMachine.JSON* toocreate 테스트 또는 프로덕션 클러스터를 사용 하 여 보안 방법을 표시 [Windows 보안](service-fabric-windows-cluster-windows-security.md)합니다.
3. *ClusterConfig.X509.DevCluster.JSON* 및 *ClusterConfig.X509.MultiMachine.JSON* toocreate 테스트 또는 프로덕션 클러스터를 사용 하 여 보안 방법을 표시 [X509 인증서 기반 보안이](service-fabric-windows-cluster-x509-security.md). 

이제는 살펴보겠습니다 hello의 다양 한 섹션을 ***ClusterConfig.JSON*** 아래와 같이 파일.

## <a name="general-cluster-configurations"></a>일반 클러스터 구성
이 hello 광범위 한 클러스터 특정 구성 아래 hello JSON 조각에 표시 된 대로 다룹니다.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

Toohello 할당 하 여 모든 이름을 tooyour 서비스 패브릭 클러스터를 제공할 수 있습니다 **이름** 변수입니다. hello **clusterConfigurationVersion** ; 클러스터의 버전 번호 hello 서비스 패브릭 클러스터를 업그레이드할 때마다 증가 해야 합니다. 그러나 유지 해야 합니다. hello **apiVersion** toohello 기본값입니다.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Hello 클러스터의 노드
Hello를 사용 하 여 서비스 패브릭 클러스터에서 hello 노드를 구성할 수 있습니다 **노드** 조각과 다음 hello 처럼 섹션.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Service Fabric 클러스터에는 세 개 이상의 노드가 있어야 합니다. 설치 프로그램에 따라 더 많은 노드 toothis 섹션을 추가할 수 있습니다. 다음 표에서 hello 각 노드에 대 한 hello 구성 설정에 설명 합니다.

| **노드 구성** | **설명** |
| --- | --- |
| nodeName |식별 이름 toohello 노드를 지정할 수 있습니다. |
| iPAddress |명령 창을 열고을 입력 하 여 노드의 hello IP 주소를 찾으려면 `ipconfig`합니다. Hello IPV4 주소를 확인 하 고 toohello 할당 **iPAddress** 변수입니다. |
| nodeTypeRef |노드마다 다른 노드 형식을 할당할 수 있습니다. hello [노드 형식](#nodetypes) hello 섹션 아래에 정의 되어 있습니다. |
| faultDomain |Tooshared 물리적 종속성 인해 시간이 오류 도메인 사용 되는 클러스터 관리자 toodefine hello 실제 노드 hello에 실패할 수 있습니다. |
| upgradeDomain |서비스 패브릭에 업그레이드 hello에 대 한 동일에 대 한 종료 된 노드 집합을 설명 하는 업그레이드 도메인 시간입니다. 모든 물리적 요구 사항에 따라 제한 되지 않습니다 대로 업그레이드 도메인 노드 tooassign toowhich를 선택할 수 있습니다. |

## <a name="cluster-properties"></a>클러스터 속성
hello **속성** 섹션 hello ClusterConfig.JSON에에서 사용 되는 tooconfigure hello 클러스터는 다음과 같습니다.

<a id="reliability"></a>

### <a name="reliability"></a>안정성
hello 개념 **reliabilityLevel** 복제본 수가 hello 또는 hello 클러스터의 hello 주 노드에서 실행 될 수 있는 hello 서비스 패브릭 시스템 서비스의 인스턴스를 정의 합니다. 따라서 클러스터를 hello 및 이러한 서비스의 hello 안정성을 결정 합니다. hello 기간은 hello 시스템에 의해 계산 된 클러스터 만들기 및 업그레이드 시입니다.

### <a name="diagnostics"></a>진단
hello **diagnosticsStore** 섹션 있습니다 tooconfigure 매개 변수 tooenable 진단 및 문제 해결 노드 또는 클러스터 오류 hello 다음 코드 조각에에서 나와 있는 것 처럼 합니다. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

hello **메타 데이터** 클러스터 진단에 대 한 설명을 이며 설치 프로그램에 따라 설정할 수 있습니다. 이러한 변수는 성능 카운터는 물론 ETW 추적 로그, 크래시 덤프를 수집하는 데 유용합니다. ETW 추적 로그에 대한 자세한 내용은 [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) 및 [ETW 추적](https://msdn.microsoft.com/library/ms751538.aspx)을 읽어보세요. 포함 한 모든 로그 [크래시 덤프](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) 및 [÷ ´ ֹ](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) toohello 방향이 지정 된 수 **connectionString** 컴퓨터의 폴더에 있습니다. 진단을 저장하는 데 *AzureStorage* 를 사용할 수도 있습니다. 샘플 코드 조각에 대해서는 아래를 참조하세요.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>보안
hello **보안** 섹션은 보안 독립 실행형 서비스 패브릭 클러스터에 필요 합니다. 다음 코드 조각 hello이이 섹션의 일부를 보여 줍니다.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

hello **메타 데이터** 보안 클러스터에 대 한 설명을 이며 설치 프로그램에 따라 설정할 수 있습니다. hello **ClusterCredentialType** 및 **ServerCredentialType** hello hello 클러스터 및 hello 노드는 구현 하는 보안 형식을 결정 합니다. Tooeither를 설정할 수 있습니다 *X509* 인증서 기반 보안을 위해 또는 *Windows* Azure Active Directory 기반 보안에 대 한 합니다. hello 나머지 hello **보안** 섹션 hello 유형의 hello 보안에 따라 달라 집니다. 읽기 [독립 실행형 클러스터에서 인증서 기반 보안](service-fabric-windows-cluster-x509-security.md) 또는 [독립 실행형 클러스터에서 Windows 보안](service-fabric-windows-cluster-windows-security.md) hello 아웃 toofill hello 나머지 방법에 대 한 내용은 **보안**섹션.

<a id="nodetypes"></a>

### <a name="node-types"></a>노드 형식
hello **nodeTypes** 섹션에는 클러스터에 있는 hello 노드의 hello 유형에 대해 설명 합니다. 하나 이상의 노드 유형에 아래 hello 조각에 나와 있는 것 처럼 클러스터에 대해 지정 되어야 합니다. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

hello **이름** 이 특정 노드 형식에 대 한 hello 친근 한 이름입니다. 이 노드 유형의 노드 toocreate 할당의 식별 이름 toohello **nodeTypeRef** 설명 했 듯이 해당 노드에 대 한 변수 [위에](#clusternodes)합니다. 각 노드 유형에 대해 사용 되는 hello 연결 끝점을 정의 합니다. 이 클러스터의 다른 끝점과 충돌하지 않는 한, 이러한 연결 끝점에 대해 어떤 포트 번호도 선택할 수 있습니다. 다중 노드 클러스터를 하나 이상의 주 노드가 됩니다 (즉, **isPrimary** 도*true*) hello에 따라 [ **reliabilityLevel** ](#reliability). 읽기 [서비스 패브릭 클러스터 용량 계획 고려 사항](service-fabric-cluster-capacity.md) 에 대 한 내용은 **nodeTypes** 및 **reliabilityLevel**, 및는 주 대상과 hello tooknow 기본이 아닌 노드 형식입니다. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>끝점 사용 tooconfigure hello 노드 형식
* *clientConnectionEndpointPort* hello 클라이언트 Api를 사용 하는 경우 hello 클라이언트 tooconnect toohello 클러스터에서 사용 하는 hello 포트입니다. 
* *clusterConnectionEndpointPort* hello 노드는 서로 통신 하는 hello 포트입니다.
* *leaseDriverEndpointPort* hello 노드가 아직 활성 상태인 경우 hello 아웃 임대 드라이버 toofind 클러스터에서 사용 하는 hello 포트입니다. 
* *serviceConnectionEndpointPort* 는 hello 응용 프로그램에서 사용 되는 hello 포트 및 서비스에 해당 특정 노드의 서비스 패브릭 클라이언트 hello와 toocommunicate 노드를 배포 합니다.
* *httpGatewayEndpointPort* hello 서비스 패브릭 탐색기 tooconnect toohello 클러스터에서 사용 하는 hello 포트입니다.
* *ephemeralPorts* hello 재정의 [hello 운영 체제에서 사용 하는 동적 포트](https://support.microsoft.com/kb/929851)합니다. 서비스 패브릭 응용 프로그램 포트로 이러한 일부 ´ ֲ 및 hello 남은 hello OS에 사용할 수 있습니다. 것도 매핑됩니다이 범위 toohello 기존 범위 hello OS에 있는 모든 용도 대 한 hello 샘플 JSON 파일에 지정 된 hello 범위를 사용할 수 있습니다. Toomake hello 차이 hello 시작 및 끝 포트 hello 이상 255 되는지 확인 해야 합니다. 이러한 차이 hello 운영 체제와 공유 하는이 범위 때문에 너무 낮은 경우 충돌이 발생할 수 있습니다. 실행 하 여 동적 포트 범위를 구성 하는 hello 참조 `netsh int ipv4 show dynamicport tcp`합니다.
* *applicationPorts* 는 hello 서비스 패브릭 응용 프로그램에서 사용할 수는 hello 포트입니다. hello 응용 프로그램 포트 범위는 응용 프로그램의 hello 끝점 요구 사항을 충분히 큰 toocover 여야 합니다. 이 범위, 즉 hello hello 머신에서 hello 동적 포트 범위에서 배타적 해야 *ephemeralPorts* hello 구성에 설정 된 대로 범위입니다.  서비스 패브릭 새 포트 필요한으로 이러한 포트에 대 한 hello 방화벽을 열어 처리할 때마다이 사용 합니다. 
* *reverseProxyEndpointPort*는 선택적 역방향 프록시 끝점입니다. 자세한 내용은 [Service Fabric 역방향 프록시](service-fabric-reverseproxy.md)를 참조하세요. 

### <a name="log-settings"></a>로그 설정
hello **fabricSettings** 섹션에서는 hello 서비스 패브릭 데이터와 로그에 대 한 tooset hello 루트 디렉터리입니다. Hello 초기 클러스터 생성 중에 이러한를 사용자 지정할 수 있습니다. 이 섹션의 샘플 코드 조각에 대해서는 아래를 참조하세요.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

및 사용 하 여 hello FabricDataRoot와 OS가 아닌 드라이브 FabricLogRoot OS 충돌에 대 한 안정성을 제공 하는 것이 좋습니다. Note만 hello 데이터 루트를 사용자 지정 하는 경우 다음 hello 로그 루트는 배치 하는 것 보다 한 수준 아래 hello 데이터 루트입니다.

### <a name="stateful-reliable-service-settings"></a>상태 저장 신뢰할 수 있는 서비스 설정
hello **KtlLogger** 섹션에서는 신뢰할 수 있는 서비스에 대 한 tooset hello 전역 구성 설정입니다. 이러한 설정에 대한 자세한 내용 [상태 저장 신뢰할 수 있는 서비스 구성](service-fabric-reliable-services-configuration.md)을 참조하세요.
다음 예제에서는 hello toochange hello hello 공유 트랜잭션 로그를 가져오는 만드는 방법을 tooback 상태 저장 서비스에 대 한 신뢰할 수 있는 모든 컬렉션 보여 줍니다.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>추가 기능
tooconfigure 추가 기능 hello apiVersion 구성으로 ' 04-2017' 이상 이어야 합니다 하며 addonFeatures toobe 구성:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>컨테이너 지원
tooenable 컨테이너에 대 한 지원을 모두 windows server 컨테이너와 hyper-v 컨테이너 독립 실행형 클러스터에 대 한 hello 'DnsService' 부가 기능 toobe 사용 하도록 설정 해야 합니다.


## <a name="next-steps"></a>다음 단계
독립 실행형 클러스터 설치에 따라 구성 된 전체 ClusterConfig.JSON 파일을 만든 후 다음 hello 문서를 통해 클러스터를 배포할 수 있습니다 [독립 실행형 서비스 패브릭 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md) 너무 진행할[서비스 패브릭 탐색기를 사용 하 여 클러스터 시각화](service-fabric-visualizing-your-cluster.md)합니다.

