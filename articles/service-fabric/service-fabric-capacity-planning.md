---
title: "서비스 패브릭 응용 프로그램에 대 한 계획 aaaCapacity | Microsoft Docs"
description: "Tooidentify 서비스 패브릭 응용 프로그램에 필요한 계산 노드 수를 hello 하는 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>서비스 패브릭 응용 프로그램의 용량 계획
이 문서에 설명 어떻게 tooestimate hello 양 리소스 (Cpu, RAM, 디스크 저장소)의 필요한 toorun Azure 서비스 패브릭 응용 프로그램입니다. 시간이 지남에 따라 것이 일반적 리소스 요구 사항 toochange입니다. 일반적으로 서비스를 개발/테스트하는 단계에서는 리소스가 적게 필요하고, 프로덕션 단계로 넘어가서 응용 프로그램의 인기가 높아지면 더 많은 리소스가 필요하게 됩니다. 응용 프로그램을 디자인할 때는 hello 장기 요구 사항을 통해 생각 하 고 서비스 tooscale toomeet 높은 고객 요구를 허용 하는 항목을 선택 합니다.

 서비스 패브릭 클러스터를 만들 때 가상 컴퓨터 (Vm)의 종류 hello 클러스터를 하 게 결정할 수 있습니다. 각 VM 제한 된 양의 Cpu (코어 및 속도), 네트워크 대역폭, RAM 및 디스크 저장소의 hello 형태로 리소스 함께 제공 됩니다. 까지 확장 되면서 서비스 시간이 지남에 따라 tooVMs 더 큰 리소스를 제공 및/또는 더 많은 Vm tooyour 클러스터를 추가 하는 업그레이드할 수 있습니다. 후자의 toodo hello, 설계 해야 서비스에 처음 toohello 클러스터 동적으로 추가 하는 새 Vm를 이용할 수 있도록 합니다.

일부 서비스는 hello Vm 자체에서 거의 toono 데이터를 관리합니다. 따라서 용량 계획 hello를 선택 하는 성능에 주로 초점을 맞추어야 이러한 서비스에 대 한 Cpu (코어 및 속도) hello Vm의 적절 한 합니다. 또한 네트워크 대역폭을 고려해야 하고 네트워크 전송 빈도와 전송되는 데이터 양을 고려해야 합니다. 서비스를 서비스 사용량 증가 함에 따라 잘 tooperform 필요한 경우 더 많은 Vm toohello 클러스터를 추가할 수 있으며 모든 hello Vm 간에 부하를 hello 네트워크 요청을 분산 시킵니다.

Hello Vm에 많은 양의 데이터를 관리 하는 서비스에 대 한 용량 계획 노력을 기울여야 주로 크기입니다. 따라서 hello VM의 RAM 및 디스크 저장소의 hello 용량을 신중 하 게 고려해 야 합니다. windows에서 hello 가상 메모리 관리 시스템을 사용 하면 디스크 공간 RAM tooapplication 코드와 같습니다. 또한 hello 서비스 패브릭 런타임에서 메모리와 이동 hello 콜드 데이터 toodisk에만 핫 데이터를 유지 하는 스마트 페이징을 제공 합니다. 따라서 응용 프로그램 hello VM에 실제로 사용할 수 있는 것 보다 많은 메모리를 사용할 수 있습니다. Hello VM RAM에 더 많은 디스크 저장소를 유지할 수 있으므로 성능이 향상 단순히 더 많은 RAM이 필요 합니다. 선택한 VM hello hello VM에서 원하는 디스크 충분히 큰 toostore hello 데이터가 있어야 합니다. 마찬가지로, VM hello 원하는 성능 hello는 충분 한 RAM tooprovide가 있어야 합니다. 시간이 지남에 따라 증가 하는 서비스의 데이터를 모든 hello Vm에서 더 많은 Vm toohello 클러스터 및 파티션 hello 데이터를 추가할 수 있습니다.

## <a name="determine-how-many-nodes-you-need"></a>필요한 노드 수를 결정합니다.
서비스를 분할 하면 tooscale 서비스의 데이터. 분할에 대한 자세한 내용은 [Service Fabric 분할](service-fabric-concepts-partitioning.md)을 참조하세요. 각 파티션은 단일 VM에 맞는 크기여야 합니다. 하지만 여러(작은) 파티션을 단일 VM에 배치할 수도 있습니다. 따라서 큰 파티션을 몇 개만 두는 것보다 작은 파티션을 여러 개 두는 것이 훨씬 유연합니다. hello 절충 경우 서비스 패브릭 오버 헤드가 증가 파티션의 많은 것 파티션에서 트랜잭션 처리 작업을 수행할 수 없습니다. 이기도 잠재적인 느려지고 네트워크 트래픽이 서비스 코드 tooaccess 가지 서로 다른 파티션을에 거주 하는 데이터를 자주 있어야 하는 경우. 서비스를 디자인할 때 이러한 장점 및 단점 tooarrive 효과적인 분할 전략에 신중 하 게 고려해 야 합니다.

응용 프로그램에 단일 상태 저장 서비스 toogrow tooDB_Size GB 1 년에 예상 되는 저장소 크기를 가진 경우를 가정해 봅니다. 더 많은 응용 프로그램 (및 파티션)으로 기꺼이 tooadd는 해당 년 이상 증가 발생 합니다.  hello 복제 계수로 (RF) hello 복제본 수에 따라 서비스 영향 총 DB_Size hello에 있습니다. hello 모든 복제본에서 총 DB_Size는 hello DB_Size 곱한 복제 요소입니다.  Node_Size hello 디스크 공간/RAM 나타내는 노드당 toouse에 원하는 서비스입니다. 최상의 성능을 위해 hello DB_Size hello 클러스터 및 VM을 선택 해야 하는 hello의 RAM hello 주위에 있는 Node_Size 메모리에 적합 해야 합니다. Hello RAM 용량 보다 큰 Node_Size를 할당 하 여 hello 서비스 패브릭 런타임에서 제공 하는 hello 페이징에 의존 하 고 있습니다. 따라서 성능 전체 데이터로 간주 되 면 toobe 핫 데이터 입/출력을 페이징 되 후 hello) (이후 최적이 아닐 수 있습니다. 그러나 많은 서비스의 hello 데이터의 일부만 뜨거움, 비용 효율적인는 합니다.

최상의 성능을 위해 필요한 노드 hello 수는 다음과 같이 계산할 수 있습니다.

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>성장 고려
또한 하 여 서비스 toogrow 예상 되는 DB_Size hello에 따라 노드 toocompute hello 수 toohello DB_Size로 시작 하는 것이 좋습니다. 그런 다음까지 확장 되면서 서비스 하지 과도 하 게 프로 비전 하는 노드의 hello 수 있도록 hello 노드 수를 증가 합니다. 하지만 hello 파티션 수가 최대 증가에 서비스를 실행 하는 경우 필요한 노드 hello 수 기반으로 해야 합니다.

그 좋은 toohave 언제 든 지 사용할 수 있는 몇 가지 추가 하는 컴퓨터 (예를 들어 경우 몇 가지 Vm 작동이) 모든 예기치 않은 스파이크 또는 오류를 처리할 수 있도록 됩니다.  예상된 프로그램 스파이크를 사용 하 여 hello 여분의 공간을 결정 해야, 시작 지점 tooreserve는 몇 가지 추가 Vm (5-10% 추가).

hello 위의 단일 상태 저장 서비스를 가정합니다. 상태 저장 서비스의 여러 개 있는 경우 hello 방정식에 다른 서비스 hello tooadd hello와 관련 된 DB_Size 해야 합니다. 또는 hello 개별적으로 각 상태 저장 서비스에 대 한 노드 수를 계산할 수 있습니다.  분산되지 않은 복제본 또는 파티션이 서비스 내에 존재할 수 있습니다. 파티션이 다른 파티션보다 더 많은 데이터를 포함할 수도 있습니다. 분할에 대한 자세한 내용은 [모범 사례의 분할 문서](service-fabric-concepts-partitioning.md)을 참조하세요. 그러나 hello 이전 식은 파티션 및 복제본 서비스 패브릭 보장는 hello 복제본 사이 분산 되어 hello 노드 최적화 된 방식에서 때문에 중립적입니다.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>비용 계산을 위한 스프레드시트 사용
이제 hello 수식에 몇 가지 실수 해 보겠습니다. [예제 스프레드시트](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) tooplan 세 가지 유형의 데이터 개체를 포함 하는 응용 프로그램에 대 한 용량을 hello 하는 방법을 보여 줍니다. 각 개체에 대 한 우리 대략적인 크기와 toohave 라고 생각 하는 개체 수입니다. 또한 각 개체 유형에 대해 원하는 복제본 수를 선택합니다. hello 스프레드시트 hello 총 메모리 toobe hello 클러스터에 저장 된 양을 계산 합니다.

그런 다음 VM 크기와 월간 비용을 입력합니다. Hello VM 크기에 따라, hello 스프레드시트 최소 데이터 toophysically 맞게 toosplit hello 노드에서 사용 해야 하는 파티션 수를 hello 지시 합니다. 많은 수의 응용 프로그램의 특정 계산 및 네트워크 트래픽 수요 파티션의 tooaccommodate 원하는 수 있습니다. hello 스프레드시트 하나의 toosix에서 hello hello 사용자 프로필 개체를 관리 하는 파티션 수에 증가 보여 줍니다.

이제,이 모든 정보에 따라, hello 스프레드시트 표시 26 개 노드 클러스터에 필요한 hello 파티션과 복제본을 사용 하 여 모든 hello 데이터를 물리적으로 가져올 수 있습니다. 그러나이 클러스터는 수 빽빽하게 묶여 있으므로 몇 가지 추가 노드 tooaccommodate 노드 오류 및 업그레이드 할 수도 있습니다. hello 스프레드시트는 빈 노드를 갖기 때문에 없는 추가 가치를 얻을 57 개 이상의 노드가 표시 됩니다. 다시 할 수 있습니다 57 노드 위에 toogo 그래도 tooaccommodate 노드 오류 및 업그레이드. Hello 스프레드시트 toomatch 응용 프로그램의 특정 요구를 수정할 수 있습니다.   

![비용 계산을 위한 스프레드시트][Image1]

## <a name="next-steps"></a>다음 단계
체크 아웃 [분할 서비스 패브릭 서비스] [ 10] toolearn 서비스를 분할 하는 방법에 대 한 자세한 합니다.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
