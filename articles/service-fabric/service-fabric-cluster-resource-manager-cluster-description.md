---
title: "aaaCluster 리소스 관리자 클러스터 설명 | Microsoft Docs"
description: "서비스 패브릭 클러스터를 설명 하는 오류 도메인과 업그레이드 도메인, 노드 속성 hello 클러스터 리소스 관리자에 대 한 노드 용량을 지정 하 여 합니다."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>서비스 패브릭 클러스터 설명
hello 서비스 패브릭 클러스터 리소스 관리자는 클러스터를 설명 하기 위한 메커니즘을 제공 합니다. 런타임 중 hello 클러스터 리소스 관리자는이 정보 tooensure 서비스의 고가용성 hello hello 클러스터에서 실행을 사용 합니다. 이러한 중요 한 규칙을 적용 하는 동안 hello 클러스터 내에서 toooptimize hello 리소스 사용도 시도 합니다.

## <a name="key-concepts"></a>주요 개념
hello 클러스터 리소스 관리자는 클러스터를 설명 하는 몇 가지 기능을 지원 합니다.

* 장애 도메인
* 업그레이드 도메인
* 노드 속성
* 노드 용량

## <a name="fault-domains"></a>장애 도메인
장애 도메인은 통합된 오류는 영역입니다. 단일 컴퓨터 이므로 오류 도메인 (에 전원 공급 장치 오류 toodrive 오류 toobad NIC 펌웨어에서 자체에 대 한 다양 한 이유로 실패할 수 있기)입니다. 동일한 이더넷 스위치에 있는 연결 된 toohello는 동일한 장애 도메인으로 hello 컴퓨터는 전원 또는 단일 위치에서 단일 소스를 공유 하는 컴퓨터입니다. 하드웨어 오류 toooverlap에 대 한 자연 이므로, 오류 도메인은 기본적으로 계층 및 서비스 패브릭에서 Uri로 표시 됩니다.

오류 도메인 올바르게 설정 되어 있는지 서비스 패브릭이 정보 toosafely 위치 서비스를 사용 하므로 반드시 합니다. 서비스 패브릭 tooplace 서비스 (특정 구성 요소의 hello 오류로 인해 발생) 오류 도메인의 hello 손실로 아래로 서비스 toogo 인해 되도록 싶어하지 합니다. Hello 서비스 패브릭 hello 환경 toocorrectly에서 제공 하는 hello 장애 도메인 정보를 사용 하 여 Azure 환경에서에서 사용자 대신 hello hello 클러스터 노드를 구성 합니다. 해당 hello 클러스터 hello 시 정의 된 서비스 패브릭 독립 실행형, 오류 도메인에 대 한 설정 

> [!WARNING]
> 해당 hello 장애 도메인 정보에 제공 된 패브릭 tooService는 정확 하 게 유용 합니다. 예를 들어 Service Fabric 클러스터의 노드가 5개의 물리적 호스트에서 실행되는 10개의 가상 컴퓨터에서 실행된다고 가정해 보겠습니다. 이 경우 10개의 가상 컴퓨터가 있지만 별도의 5개(최상위 수준) 장애 도메인만 있습니다. 동일한 실제 호스트 하면 hello 공유 hello Vm 경험의 실제 호스트가 실패 하면 오류를 조정 하므로 Vm tooshare hello 동일한 루트 장애 도메인입니다.  
>
> 서비스 패브릭에서는 이후 hello 노드 하지 toochange의 오류 도메인입니다. 와 같은 hello Vm의 고가용성을 보장의 다른 메커니즘 [HA Vm](https://technet.microsoft.com/en-us/library/cc967323.aspx), 하나의 호스트 tooanother에서 Vm의 투명 한 마이그레이션을 사용 하 여 합니다. 이러한 메커니즘 다시 구성 하지 않거나 hello VM 내부에서 코드를 실행 하는 hello를 알립니다. 따라서 Service Fabric 클러스터를 실행하기 위한 환경으로 **지원되지 않습니다**. 서비스 패브릭 hello 높은 가용성 기술을 사용 해야 합니다. 라이브 VM 마이그레이션, SAN 또는 기타와 같은 메커니즘은 필요하지 않습니다. 이러한 메커니즘은 Service Fabric과 함께 사용되는 경우 복잡성을 추가하고, 중앙 집중화된 오류 원인을 추가하며, Service Fabric과 충돌하는 안정성 및 가용성 전략을 사용하기 때문에 응용 프로그램 가용성 및 안정성을 _떨어뜨립니다_. 
>
>

Hello 그래픽 아래에서 발생 하는 여러 장애 도메인 hello 모든 tooFault 도메인 및 목록 영향을 주는 모든 hello 엔터티 색 했습니다. 이 예제에는 데이터센터("DC"), 랙("R") 및 블레이드("B")가 있습니다. 생각할, 하나 이상의 가상 컴퓨터를 포함 하는 각 블레이드 경우 hello 장애 도메인 계층 구조에에서는 또 다른 계층 수 있습니다.

<center>
![장애 도메인을 통해 구성된 노드][Image1]
</center>

런타임 중 hello 서비스 패브릭 클러스터 리소스 관리자는 hello 클러스터의 hello 오류 도메인을 고려 하 및 레이아웃을 계획 합니다. 상태 저장 복제본 hello 또는 지정된 된 서비스에 대 한 상태 비저장 인스턴스는 별도 오류 도메인에 맞게 배포 됩니다. 오류 도메인을 사용 하 여 hello 서비스 분산 hello 서비스의 가용성을 hello 장애 도메인 hello 계층의 모든 수준에서 실패 한 경우 손상 되지 않도록 보장 합니다.

서비스 패브릭 클러스터 리소스 관리자는 hello 장애 도메인 계층에 계층 수를 신경 쓰지 않습니다. 그러나 hello 계층의 한 일부 hello 손실에 실행 되는 서비스에 영향을 주지 tooensure 하려고 시도 합니다. 

있는 경우 것이 가장 좋습니다 깊이 hello 장애 도메인 계층 구조에서에서 각 수준의 노드 수가 같은 hello 합니다. 오류 도메인 "트리" hello를 클러스터의 균형 잡힌 없으면 어렵게 서비스의 hello 최상의 할당 아웃 클러스터 리소스 관리자 toofigure hello에 대 한 합니다. 불균형 오류 도메인 레이아웃 해당 hello 손실을 일부 도메인의 다른 도메인 보다 더 많은 서비스의 영향 hello 가용성을 의미합니다. 두 가지 목표 hello 클러스터 리소스 관리자 삭제 되는지 결과적으로,: 서비스에 배치 하 여 해당 "고급" 도메인에 toouse hello 시스템은 원하는 및 도메인의 hello 손실 문제가 발생 하지 않는 있도록은 원하는 다른 도메인에서 tooplace 서비스입니다. 

분산되지 않은 도메인은 어떤 모양일까요? 아래 hello 다이어그램에서는 두 개의 다른 클러스터 레이아웃을 보여 줍니다. Hello 첫 번째 예제에서는 hello 노드 hello 오류 도메인 간에 균등 하 게 배포 됩니다. Hello 두 번째 예제에서는 단일 장애 도메인에 많은 노드보다 hello 다른 오류 도메인입니다. 

<center>
![두 개의 다른 클러스터 레이아웃][Image2]
</center>

Azure의 hello 선택 장애 도메인에 노드가 드립니다 관리 됩니다. 그러나 hello 프로 비전 하는 노드 수에 따라 있습니다 수 시작할 최 오류 도메인 다른 항목 보다 더 많은 노드를 사용 합니다. 예를 들어 5 개의 오류 도메인 hello 클러스터에 있지만 특정된 노드 종류에 대 한 7 개의 노드를 프로 비전 합니다. 이 경우 hello 처음 두 개의 오류 도메인 서로 다른 노드. 몇 개의 인스턴스만와 자세한 NodeTypes toodeploy를 계속 하면 hello 문제가 악화 될 따라서 해당 hello 것이 좋습니다 각 노드 유형에의 노드 수의 배수가 hello 장애 도메인 수입니다.

## <a name="upgrade-domains"></a>업그레이드 도메인
업그레이드 도메인은 서비스 패브릭 클러스터 리소스 관리자 hello 도움이 되는 또 다른 기능은 hello 클러스터의 hello 레이아웃을 이해 합니다. Hello에서 업그레이드 된 집합을 정의 하는 업그레이드 도메인 동시 합니다. 업그레이드 도메인 도움말 hello 클러스터 리소스 관리자를 이해 하 고 업그레이드와 같은 관리 작업을 조정 합니다.

업그레이드 도메인은 장애 도메인과 많이 닮았지만 몇 가지 주요 차이점이 있습니다. 먼저 장애 도메인은 조정된 하드웨어 오류 영역으로 정의되지만, 업그레이드 도메인, 다른 손 hello, 정책에 의해 정의 됩니다. 얻게 toodecide hello 환경에 의해 결정 되 고 해당 하는 대신 사용할 수 있습니다. 노드를 갖추는 만큼 많은 업그레이드 도메인을 갖출 수 있습니다. 장애 도메인과 업그레이드 도메인의 또 다른 차이점은 업그레이드 도메인이 계층적 구조가 아니라는 것입니다. 대신, 간단한 태그와 비슷합니다. 

hello 다음 다이어그램에서는 세 개의 업그레이드 도메인은 세 개의 오류 도메인에 걸쳐 스트라이프된 또한 상태 저장 서비스의 세 개의 서로 다른 복제본을 배치하는 한 가지 방법을 보여줍니다. 여기서 각각 다른 장애 도메인 및 업그레이드 도메인에 배치됩니다. 이 배치 서비스 업그레이드의 hello 중간에 있는 동안 장애 도메인 hello 손실 있으며 hello 코드 및 데이터의 복사본이 두 개에 아직 합니다.  

<center>
![장애 도메인 및 업그레이드 도메인으로 배치][Image3]
</center>

업그레이드 도메인의 장점 및 단점 toohaving 많은 수 있습니다. 더 많은 업그레이드 도메인 hello 업그레이드의 각 단계는 보다 세부적인 및 적은 수의 노드 또는 서비스에 영향을 의미 합니다. 따라서 더 적은 서비스가지고 toomove 한 번에 적은 변동을 hello 시스템에 도입 합니다. 이 hello 업그레이드 하는 동안 도입 된 모든 문제의 영향을 받음 hello 서비스의 작은 이후 tooimprove 안정성을 경향이 있습니다. 더 많은 업그레이드 도메인 필요한 다른 노드 toohandle hello 영향의 hello에 사용할 수 있는 버퍼 덜 업그레이드 하는 의미 하기도 합니다. 예를 들어 5 개의 업그레이드 도메인이 있는 경우 각 hello 노드는 처리 중 약 20%의 트래픽입니다. 업그레이드 도메인 업그레이드 아래로 tootake 해야 할 경우 해당 부하 toogo 어딘가에 일반적으로 필요 합니다. 나머지 4 개의 업그레이드 도메인에 한 각 트래픽 당 총 hello의 약 5%를 위한 공간이 있어야 합니다. 더 많은 업그레이드 도메인 hello 클러스터의 hello 노드에서 작은 버퍼 필요한 것을 의미 합니다. 예를 들어 10개의 업그레이드 도메인을 대신 갖추는 경우를 고려합니다. 이 경우 각 UD만 처리할 수도 트래픽 당 총 hello의 약 10%입니다. Hello 클러스터 통해 업그레이드 단계는 경우 각 도메인에만 toohave 공간 트래픽 당 총 hello의 약 %에 1.1을 해야 합니다. 더 많은 업그레이드 도메인 일반적으로 사용 하면 toorun 높은 사용률 덜 예약 된 용량을 해야 하기 때문에 프로그램 노드. hello에 마찬가지입니다 오류 도메인입니다.  

여러 업그레이드 도메인의 hello 단점은 업그레이드는 긴 tootake 경향이 있음을입니다. 서비스 패브릭 도메인 업그레이드 완료 되 고 tooupgrade hello를 시작 하기 전에 검사를 수행 하는 시간 짧은 기간 동안 다음을 기다립니다. 이러한 지연은 hello 업그레이드 진행 하기 전에 hello 업그레이드에 의해 도입 된 검색 문제를 사용 하도록 설정 합니다. hello 적절 한 균형을 잘못 된 변경 내용에 영향을 미치는 hello 서비스의 과도 한 번에 없기 때문에 좋습니다.

업그레이드 도메인이 너무 적어도 많은 부작용이 있습니다. 개별 업그레이드 도메인이 각각 중단되고 업그레이드되는 동안 전체 용량 중 상당한 부분을 사용할 수 없습니다. 예를 들어, 세 개의 업그레이드 도메인만 있는 경우 전체 서비스 또는 클러스터 용량은 약 1/3로 저하됩니다. 클러스터 toohandle hello 워크 로드의 hello rest에서 toohave 충분 한 용량이 있어야 하므로 적절 하지 아래로 한 번에 서비스의 상당 부분이 필요 합니다. 해당 버퍼를 유지 관리하면 정상 작업 중에 이러한 노드가 다른 경우에 로드하는 것보다 더 적게 로드됩니다. 서비스 실행 hello 비용은 증가 합니다.

수는 없습니다 한계 toohello 총 결함 또는 업그레이드 도메인의 겹치는 방식을 대 한 제약 조건을 만들거나는 환경에서 합니다. 즉 일반적인 몇 가지 패턴이 있습니다.

- 1:1 매핑된 장애 도메인 및 업그레이드 도메인
- 노드(실제 또는 가상 OS 인스턴스) 당 하나의 업그레이드 도메인
- 여기서 hello 장애 도메인과 업그레이드 도메인 형성 행렬 hello 대각선 다운 일반적으로 실행 중인 컴퓨터와 함께 "스트라이프" 또는 "행렬" 모델

<center>
![장애 도메인 및 업그레이드 도메인 레이아웃][Image4]
</center>

없는 가장 대답 어떤 레이아웃 toochoose를 몇 가지 장점 및 단점에 각각. 예를 들어 hello 1FD:1UD 모델 된 최대 간단한 tooset입니다. hello 1 업그레이드 도메인 노드 모델당은 가장에 사용 되는 어떤 사람들은 적합 합니다. 업그레이드하는 동안 각 노드는 독립적으로 업데이트됩니다. 이것은 유사 toohow 작은 집합 컴퓨터의 과거 hello에서 수동으로 업그레이드 되었습니다. 

hello 가장 일반적인 모델은 hello FD/UD 행렬, 여기서 hello Ud와 Fd 형성 테이블 및 노드 대각선 hello를 따라 시작 배치 됩니다. Azure에서 서비스 패브릭 클러스터에는 기본적으로 사용 되는 hello 모델입니다. 노드가 여러 개인 클러스터에 대 한 모든 위의 hello 조밀한 매트릭스 패턴 같은 형태를 끝냅니다.

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>장애 도메인 및 업그레이드 도메인 제약 조건 및 결과 동작
hello 클러스터 리소스 관리자는 hello desire tookeep 서비스 장애 도메인과 업그레이드 도메인 제약 조건으로 간에 균형을 처리 합니다. [이 문서](service-fabric-cluster-resource-manager-management-integration.md)에서 제약 조건에 대한 자세한 내용을 확인할 수 있습니다. 장애 도메인과 업그레이드 도메인 제약 조건 상태 hello: "지정한 서비스 파티션에 대 한 없어야 차이가 *1 보다 큰* hello 수의 서비스 개체 (상태 비저장 서비스 인스턴스 또는 상태 저장 서비스 복제본)에 두 도메인. " 이렇게 하면 이 제약 조건을 위반하는 특정 이동 또는 배열을 방지합니다.

한 가지 예를 살펴보겠습니다. 6개의 노드를 포함하며 5개의 장애 도메인과 5개의 업그레이드 도메인으로 구성된 클러스터가 있다고 가정해 보겠습니다.

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

이제 TargetReplicaSetSize(또는 상태 비저장 서비스를 위한 InstanceCount)가 5인 서비스를 만든다고 가정해 보겠습니다. hello 복제본 N1 N5에 도착 합니다. 실제로 많은 서비스를 만들더라도 N6은 절대 사용되지 않습니다. 그렇지만 그 이유는 무엇일까요? Hello 사이의 차이 hello 현재 레이아웃 N6을 선택 하면 어떻게 되는지 살펴보겠습니다.

다음은 hello 레이아웃 म 및 hello 장애 도메인과 업그레이드 도메인 당 복제본의 총 수입니다.

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

이 레이아웃은 장애 도메인 및 업그레이드 도메인당 노드의 측면에서 균형을 이룹니다. Hello 장애 도메인과 업그레이드 도메인 당 스냅숏 수를 기준으로 균형이 조정도 됩니다. 각 도메인에는 노드 수가 같은 hello 및 hello 동일한 복제본 수입니다.

이제 N2 대신 N6를 사용하는 경우 발생하는 결과를 살펴보겠습니다. 어떻게 hello 복제본 배포 후?

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

이 레이아웃 hello 장애 도메인 제약 조건에 대 한 정의 위반합니다. FD0 FD1에 0이 함으로써 hello 차이 FD0 FD1 총 두 번의 동안 두 개의 복제본에 있습니다. hello 클러스터 리소스 관리자는 이러한 작업을 허용 하지 않습니다. 마찬가지로 N2 및 N6(N1 및 N2 대신)을 선택한 경우 다음에서 얻을 수 있습니다.

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

이 레이아웃은 장애 도메인 측면에서 분산됩니다. 그러나 이제 것 위반 hello 업그레이드 도메인 제약 조건입니다. 이는 UD0에는 복제본이 없고 UD1에는 두 개의 복제본이 있기 때문입니다. 따라서이 레이아웃도 잘못 되었으며 hello 클러스터 리소스 관리자에서 선택할 수 없습니다. 

## <a name="configuring-fault-and-upgrade-domains"></a>장애 도메인 및 업그레이드 도메인 구성
장애 도메인 및 업그레이드 도메인 정의는 Azure 호스티드 Service Fabric 배포에서 자동으로 수행됩니다. 서비스 패브릭을 선택 하 고 Azure의 hello 환경 정보를 사용 합니다.

자체 클러스터를 만드는 중입니다 (또는 원하는 toorun 개발의 특정 토폴로지)를 하는 경우에 사용자가 직접 hello 장애 도메인 및 업그레이드 도메인 정보를 제공할 수 있습니다. 이 예제에서는 각각 세 개의 랙을 가진 세 가지 "데이터 센터"에 걸쳐 있는 9개의 노드 로컬 개발 클러스터를 정의합니다. 이 클러스터에는 세 개의 해당 데이터 센터에 스트라이프된 3개의 업그레이드 도메인도 있습니다. Hello 구성의 예는 다음과 같습니다. 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

독립 실행형 배포의 경우 ClusterConfig.json을 통해

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> Azure 리소스 관리자를 통해 클러스터를 정의할 때 Azure에서 장애 도메인과 업그레이드 도메인이 할당됩니다. 따라서 Azure Resource Manager 템플릿에 노드 형식 및 가상 컴퓨터 크기 집합의 hello 정의 장애 도메인 또는 도메인 업그레이드 정보에는 포함 되지 않습니다.
>

## <a name="node-properties-and-placement-constraints"></a>노드 속성 및 배치 제약 조건
경우에 따라 (사실, 대부분의 hello) toowant tooensure hello 클러스터의 노드 중 특정 형식에 대해서만 특정 작업을 실행 하는 것입니다. 예를 들어, 일부 워크로드는GPU 또는 SSD가 필요할 수 있습니다. 하드웨어 tooparticular 워크 로드를 대상으로의 훌륭한 예는 거의 모든 n 계층 아키텍처 있는지입니다. 특정 컴퓨터의 역할 hello 프런트 엔드 또는 API hello 응용 프로그램의 역할을 하므로 고 노출된 toohello 클라이언트 또는 인터넷 hello 합니다. 다른 하드웨어 리소스를 서로 다른 컴퓨터 hello 계산 또는 저장소 계층의 hello 작업을 처리 합니다. 일반적으로 _하지_ tooclients 직접 노출 또는 인터넷을 환영 합니다. 서비스 패브릭 경우가 있음을 특정 작업 이곳 toorun 특정 하드웨어 구성에 필요 합니다. 예:

* 기존 n 계층 응용 프로그램은 서비스 패브릭 환경으로 "리프트 및 이동"되었습니다.
* 작업 성능, 배율 또는 보안상의 이유로 격리에 대 한 특정 하드웨어에 toorun가
* 워크로드는 정책 또는 리소스 소비를 이유로 다른 워크로드로부터 격리되어야 합니다.

toosupport 이러한 종류의 구성, 서비스 패브릭 toonodes 적용된 될 수 있는 태그의 첫 번째 클래스 개념이 있습니다. 이러한 태그를 **노드 속성**이라고 합니다. **배치 제약 조건** hello 문은 하나 이상의 노드 속성에 대 한 선택 tooindividual 서비스 연결 됩니다. 배치 제약 조건은 서비스를 실행해야 하는 위치를 정의합니다. 제약 조건 hello 집합은 확장 가능-모든 키/값 쌍 작업할 수 있습니다. 

<center>
![다양한 클러스터 레이아웃 워크로드][Image5]
</center>

### <a name="built-in-node-properties"></a>기본 제공 노드 속성
서비스 패브릭 hello 사용자 toodefine가 필요 하지 않고 자동으로 사용할 수 있는 몇 가지 기본 노드 속성을 정의 합니다. 해당 합니다. 각 노드에 정의 된 hello 기본 속성은 hello **NodeType** 및 hello **NodeName**합니다. 예를 들어 배치 제약 조건을 `"(NodeType == NodeType03)"`으로 작성할 수 있습니다. 일반적으로 발견 했습니다 NodeType toobe hello 가장 일반적으로 사용 되는 속성 중 하나입니다. 이는 컴퓨터 종류와 1:1로 대응하므로 유용합니다. 각 유형의 컴퓨터가 tooa 유형의 기존 n 계층 응용 프로그램에서 작업 부하를 해당합니다.

<center>
![배치 제약 조건 및 노드 속성][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>배치 제약 조건 및 노드 속성 구문 
hello 값 hello 노드 속성에 지정 된 string, bool, 이거나 긴 서명. hello 문을 hello 서비스에는 배치 라고 *제약 조건* hello 서비스 hello 클러스터에서 실행할 수 있는 제한 때문입니다. hello 제약 조건에는 hello 클러스터의 hello 다른 노드 속성에 작동 하는 모든 부울 문이 될 수 있습니다. 다음과 같은 부울 문에서 hello 유효한 선택기는:

1) 특정 문을 만들기 위한 조건부 검사

| 문 | 구문 |
| --- |:---:|
| "같음" | "==" |
| "다음과 같지 않음" | "!=" |
| "다음보다 큼" | ">" |
| "다음보다 크거나 같음" | ">=" |
| "다음보다 작음" | "<" |
| "다음보다 작거나 같음" | "<=" |

2) 그룹화 및 논리 작업에 대한 부울 문

| 문 | 구문 |
| --- |:---:|
| "및" | "&&" |
| "또는" | "&#124;&#124;" |
| "아님" | "!" |
| "단일 문인 그룹" | "()" |

다음은 기본 제약 조건문의 몇 가지 예입니다.

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

여기서 hello 전반적인 배치 제약 조건 평가 되 너무 "True" 노드만 hello 서비스 배치를 가질 수 있습니다. 정의된 속성이 없는 노드는 해당 속성을 포함하는 배치 제약 조건과 일치하지 않습니다.

속성이 지정 된 노드 형식에 대해 정의 하는 노드 다음에 해당 hello를 가정해 보십시오.

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

독립 실행형 배포의 경우 ClusterConfig.json, Azure 호스티드 클러스터의 경우 Template.json을 통해 수행됩니다. 

> [!NOTE]
> Azure 리소스 관리자 템플릿 hello 노드에 형식이 일반적으로 매개 변수화 합니다. "NodeType01" 대신 "[parameters('vmNodeType1Name')]"와 비슷합니다.
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

다음과 같이 서비스에 대한 서비스 배치 *제약 조건*을 만들 수 있습니다.

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

모든 노드의 NodeType01 올바르면 hello 제약 조건과 해당 노드 유형을 선택할 수도 있습니다 "(NodeType == NodeType01)"입니다.

서비스의 배치 제약 조건에 대 한 hello 유용한 기능 중 하나는 업데이트할 수 동적으로 런타임 중입니다. 따라서 해야 할 경우 hello 클러스터에서 서비스를 이동, 추가 및 제거할 수 있습니다 요구 사항, 등입니다. 서비스 패브릭 처리 된 hello 서비스 유지 및 사용 가능한도 경우 이러한 종류의 변경 내용이 적용 되었는지 확인 합니다.

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Powershell:

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

배치 제약 조건은 명명된 다른 모든 서비스 인스턴스에 대해 지정됩니다. 업데이트 항상도 일어나지 hello의 (덮어쓰기) 이전에 지정 된 항목입니다.

hello 클러스터 정의 노드에서 hello 속성을 정의합니다. 노드 속성을 변경하려면 클러스터 구성을 업그레이드해야 합니다. 업그레이드 된 노드 속성의 새 속성 각 영향을 받는 노드에서 toorestart tooreport 필요 합니다. 이러한 롤링 업그레이드는 Service Fabric에서 관리됩니다.

## <a name="describing-and-managing-cluster-resources"></a>클러스터 리소스 설명 및 관리
Hello 클러스터의 리소스 소비를 관리 하는 가장 중요 한 모든 orchestrator의 작업은 toohelp hello 중 하나입니다. 클러스터 리소스 관리는 여러 가지 다른 작업을 의미할 수 있습니다. 첫째, 컴퓨터에 과부하가 걸리지 않도록 해야 합니다. 즉 컴퓨터에서 처리할 수 있는 것보다 더 많은 서비스를 실행하지 않도록 하는 것입니다. 둘째, 균형 조정 및 최적화 효율적으로 중요 한 toorunning 서비스 되는. 유효 하지 않거나 중요 한 서비스 제공 비용된을 허용할 수 없습니다 일부 노드 toobe 핫 이지만 나머지는 콜드 합니다. 핫 노드 tooresource 경합 및 성능 저하 및 콜드 노드 불필요 하 게 나타내는 리소스 및 비용이 증가 될 있습니다. 

Service Fabric은 리소스를 `Metrics`으로 나타냅니다. 메트릭은 toodescribe tooService 패브릭 원하는 논리적 또는 물리적 리소스 있습니다. 메트릭의 예로는 "WorkQueueDepth" 또는 "MemoryInMb" 등이 있습니다. 노드에서 서비스 패브릭 수 제어 하는 hello 물리적 리소스에 대 한 정보를 참조 하십시오. [리소스 관리](service-fabric-resource-governance.md)합니다. 사용자 지정 메트릭 및 해당 용도를 구성하는 방법에 대한 내용은 [이 문서](service-fabric-cluster-resource-manager-metrics.md)를 참조하세요.

메트릭은 배치 제약 조건 및 노드 속성이 서로 다릅니다. 노드 속성은 hello 노드 자체의 정적 설명자입니다. 메트릭은 노드에 있고 노드에서 실행될 때 서비스에서 사용하는 리소스를 설명합니다. 노드 속성 "HasSSD" 수 있으며 tootrue 또는 false로 설정할 수 없습니다. 해당 SSD 및 서비스에서 사용할 양을 사용 가능한 공간의 크기를 hello "DriveSpaceInMb"와 같은 메트릭을 것입니다. 

중요 한 toonote 동일 하 게 배치 제약 조건 및 노드 속성에 대 한 서비스 패브릭 클러스터 리소스 관리자 hello hello 메트릭 평균의 어떤 hello 이름을 인식 하지 못하는 하는 경우 메트릭 이름은 단순한 문자열입니다. 그는 hello 메트릭 이름이 모호할 때 만드는의 일부로 좋습니다 toodeclare 단위입니다.

## <a name="capacity"></a>용량
모든 리소스 *분산*을 해제한 경우에도 Service Fabric의 클러스터 리소스 관리자는 여전히 노드가 해당 용량을 초과하지 않도록 합니다. 관리 용량 오버런 hello 클러스터 꽉 hello 작업은 모든 노드에 보다 큰 경우가 아니면 불가능 합니다. 용량은 또 다른 *제약 조건* toounderstand을 사용 하 여 해당 hello 클러스터 리소스 관리자에서 노드는 리소스의 양을 했습니다. 남은 용량을 전체적으로 hello 클러스터에 대 한 추적도 합니다. Hello 용량과 hello 서비스 수준에서 hello 사용 메트릭을 기준으로 표현 됩니다. 예를 들어 hello 메트릭을 "ClientConnections" 될 수 있습니다 및 지정된 된 노드의 32768의 "ClientConnections"에 대 한 용량 있을 수 있습니다. 다른 노드는 노드 수 있는에서 실행 중인 일부 서비스 예를 들어 현재 사용 중인 "ClientConnections" hello 메트릭의 32256 기타 제한을 가질 수 있습니다.

런타임 중 hello 클러스터 리소스 관리자는 노드 및 hello 클러스터에서 남아 있는 용량을 추적합니다. 순서 tootrack 용량 hello 클러스터 리소스 관리자는 hello 서비스를 실행 하는 노드의 용량에서 각 서비스의 사용을 뺍니다. 이 정보를 통해 서비스 패브릭 클러스터 리소스 관리자 hello 알아낼 수 where tooplace 또는 노드 용량 지나치게 있도록 복제 데이터베이스를 이동 합니다.

<center>
![클러스터 노드 및 용량][Image7]
</center>

C#:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

Hello 클러스터 매니페스트에서 정의 된 용량을 확인할 수 있습니다.

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

독립 실행형 배포의 경우 ClusterConfig.json, Azure 호스티드 클러스터의 경우 Template.json을 통해 수행됩니다. 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

일반적으로 서비스의 로드는 동적으로 변경됩니다. 복제본의 부하 "ClientConnections"의 1024 too2048를 가져오지만 hello 노드에서 실행 되 고 그런 다음 해당 메트릭에 대 한 남은 512 용량 만으로는 변경 되었음을 말하십시오. 이제 해당 노드에 있는 충분한 공간이 없기 때문에 해당 복제본 또는 인스턴스의 배치가 유효하지 않습니다. hello 클러스터 리소스 관리자 tookick을 갖고 있으며 용량 보다 다시 hello 노드를 가져옵니다. 해당 노드 tooother 노드에서 하나 이상의 hello 복제본 또는 인스턴스를 이동 하 여 용량을 통해 있는 hello 노드에 대 한 부하를 줄입니다. 복제 데이터베이스를 이동할 때 hello 클러스터 리소스 관리자는 해당 이동의 toominimize hello 비용을 시도 합니다. 이동 비용에 대해서는 설명 [이 여기서](service-fabric-cluster-resource-manager-movement-cost.md) 및 더 hello에 대 한 클러스터 리소스 관리자의 작업 재 분산 전략, 규칙 설명 [여기](service-fabric-cluster-resource-manager-metrics.md)합니다.

## <a name="cluster-capacity"></a>클러스터 용량
어떻게는 hello 서비스 패브릭 클러스터 리소스 관리자 유지 hello 전체에서 클러스터 꽉 찬 되 고 있습니까? 물론 동적 로드로 수행할 수 있는 작업은 많지 않습니다. 서비스는 hello 클러스터 리소스 관리자가 수행한 작업을 독립적으로 자신의 부하 스파이크를 가질 수 있습니다. 즉, 오늘은 여유가 많은 클러스터가 내일은 수요가 많아져 전력이 부족해질 수 있습니다. 즉, tooprevent 문제에서 구운 컨트롤이 몇 가지 있습니다. hello 먼저 할 수 있는 점은 hello 클러스터 toobecome 전체를 발생 시키는 새 워크 로드의 hello 생성을 방지 합니다.

상태 비저장 서비스를 만들고 여기에는 이 서비스와 연결되는 일부 로드가 있습니다. Hello 서비스 "DiskSpaceInMb" 메트릭을 hello에 대 한 데 관심이 있는 경우를 가정해 봅니다. 또한 경우를 가정해 하락 tooconsume 5 단위에 "DiskSpaceInMb" 모든 인스턴스에 대해 hello 서비스 인지 합니다. Hello 서비스의 세 인스턴스 toocreate 사용 하는 것이 좋습니다. 잘하셨습니다. 15 단위 "DiskSpaceInMb" toobe의 필요한 의미 tooeven 하기 위해에서 hello 클러스터의 표시 되도록 이러한 서비스 인스턴스 수 toocreate 수 있습니다. 클러스터 리소스 관리자 hello 지속적으로 계산 hello 용량 및 각 메트릭의 소비 hello 클러스터의 hello 남은 용량을 결정할 수 있도록 합니다. 충분 한 공간이 없으면 hello 클러스터 리소스 관리자를 거절 hello 서비스 호출을 만듭니다.

이므로 hello 요구 사항에 있는 15 단위를 사용할 수, 여러 가지 방법으로이 공간 할당할 수 없습니다. 예를 들어, 다른 15개의 노드에서 남은 1단위의 용량이나 다른 5개의 노드에서 남은 3단위의 용량일 수 있습니다. Hello 클러스터 리소스 관리자 세 개의 노드에서 5 단위는 작업을 다시 정렬할 수를 찾으면 hello 서비스를 배치 합니다. 다시 정렬 hello 클러스터 hello 클러스터 거의 꽉 찼습니다 hello 기존 서비스 어떤 이유로 통합 될 수 없는 경우가 아니면 일반적으로 불가능 합니다.

## <a name="buffered-capacity"></a>버퍼링된 용량
버퍼링 된 용량에는 hello 클러스터 리소스 관리자의 또 다른 기능은 합니다. Hello 중 일부의 예약을 통해 전체 노드 용량입니다. 이 용량 버퍼는 업그레이드 및 노드 실패 하는 동안 사용 되는 유일한 tooplace 서비스입니다. 버퍼링된 용량은 모든 노드에 대해 메트릭별로 전역으로 지정됩니다. hello 예약 용량에 대해 선택 하는 hello 값은 장애 도메인과 업그레이드 도메인 hello 클러스터에 있는 hello 수의 함수입니다. 장애 도메인과 업그레이드 도메인이 증가하면 버퍼링된 용량에 대해 낮은 값을 선택할 수 있습니다. 더 많은 도메인이 업그레이드 및 실패 하는 동안 사용할 수 없는 적은 수의 클러스터 toobe 기대할 수 있습니다. 버퍼링 된 용량을 지정만 합리적 지정된 hello 노드 용량 메트릭에 대 한도 있는 경우입니다.

Toospecify 용량을 버퍼링 하는 방법의 예는 다음과 같습니다.

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

독립 실행형 배포의 경우 ClusterConfig.json 또는 Azure 호스티드 클러스터의 경우 Template.json를 통해 수행됩니다.

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

버퍼링 된 용량 메트릭에 대 한 hello 클러스터는 경우 새 서비스의 hello 만들기 실패 합니다. 새 서비스 toopreserve hello 버퍼의 hello 생성을 방지 조치용 업그레이드 및 오류 노드 toogo 발생 하지는 보장 합니다. 버퍼링된 용량은 선택적이지만 메트릭에 대한 용량을 정의하는 모든 클러스터에 권장됩니다.

hello 클러스터 리소스 관리자는이 부하 정보를 노출 합니다. 각 메트릭에 대해 다음 정보가 포함됩니다. 
  - hello 버퍼링 용량 설정
  - hello 총 용량
  - hello 현재 사용량
  - 각 메트릭이 분산된 것으로 간주되는지 여부
  - hello 표준 편차에 대 한 통계
  - hello 노드 hello 대부분 및 최소 부하는  
  
해당 출력의 예제는 다음과 같습니다.

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>다음 단계
* 에 대 한 내용은 hello 클러스터 리소스 관리자 내에서 hello 아키텍처 및 정보 흐름을 체크 아웃 [이 문서](service-fabric-cluster-resource-manager-architecture.md)
* 조각 모음 메트릭을 정의 하는 것은 확산 하는 대신 노드에 대 한 가지 방법은 tooconsolidate 로드 합니다. toolearn 어떻게 tooconfigure 조각 모음, 너무 참조[이 문서](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Hello 처음부터 시작 하 고 [소개 toohello 서비스 패브릭 클러스터 리소스 관리자 가져오기](service-fabric-cluster-resource-manager-introduction.md)
* toofind 아웃 hello 클러스터 리소스 관리자를 관리 하 고 hello 클러스터의 로드 균형을 조정 하는 방법에 체크 아웃 hello 문서에 [부하 분산](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
