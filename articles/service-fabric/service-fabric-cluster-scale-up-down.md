---
title: "in 또는 out aaaScale 서비스 패브릭 클러스터 | Microsoft Docs"
description: "각 노드 형식/가상 컴퓨터 크기 집합에 대 한 자동 크기 조정 규칙을 설정 하 여 서비스 패브릭 클러스터 in 또는 out toomatch 요청 크기를 조정 합니다. 추가 또는 노드 tooa 서비스 패브릭 클러스터를 제거 합니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>자동 크기 조정 규칙을 사용하여 서비스 패브릭 클러스터 크기 조정
가상 컴퓨터 크기 집합은 toodeploy를 사용 하 고 집합으로 가상 컴퓨터의 컬렉션을 관리할 수 있는 한 Azure 계산 리소스입니다. Service Fabric 클러스터에 정의된 모든 노드 형식은 별도의 가상 컴퓨터 확장 집합으로 설정됩니다. 각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다. Hello에 대 한 자세한 설명 [서비스 패브릭 nodetypes](service-fabric-cluster-nodetypes.md) 문서. Hello 백 엔드에 가상 컴퓨터 크기 집합의 클러스터 서비스 패브릭 노드 유형에 hello 하므로 각 노드 형식/가상 컴퓨터 크기 집합에 대 한 자동 크기 조정 규칙을 tooset이 필요 합니다.

> [!NOTE]
> 구독에 새 Vm이이 클러스터를 구성 하는 hello 충분 한 코어가 tooadd가 있어야 합니다. 모델 유효성 검사 없이 현재 적중 hello 할당량 한도 경우 배포 시간 오류를 가져옵니다.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Hello 노드 유형/가상 컴퓨터 크기 집합 tooscale 선택
현재 hello 포털을 사용 하 여 가상 컴퓨터 크기 집합에 대 한 hello 자동 크기 조정 규칙 수 toospecify 없는, 따라서 응 Azure PowerShell (1.0 이상) toolist hello 노드 형식을 사용 하 고 자동 크기 조정 규칙 toothem를 추가 합니다.

가상 컴퓨터 크기 집합 하의 tooget hello 목록 hello 다음 cmdlet을 실행 하 여 클러스터를 구성 합니다.

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Hello 노드 유형/가상 컴퓨터 크기 집합에 대 한 자동 크기 조정 규칙 설정
클러스터에 여러 노드 형식, (in 또는 out) tooscale 되도록 설정 하는 각 노드 형식/가상 컴퓨터 크기에 대해이 반복 합니다. 계정 hello 노드 수를 고려 자동 크기 조정 설정 하기 전에 있어야 합니다. hello 기본 노드 형식에 대 한 해야 하는 노드의 최소 수 hello 선택한 hello 안정성 수준에 의해 이루어집니다. [안정성 수준](service-fabric-cluster-capacity.md)에 대해 자세히 알아보세요.

> [!NOTE]
> Hello 최소한 hello 클러스터 불안정 하거나 중단 시킬 보다 hello 주 노드 유형 tooless 축소 합니다. 이 hello 시스템 서비스 및 응용 프로그램에 대 한 데이터가 손실 될 수 있습니다.
> 
> 

현재 hello 자동 크기 조정 기능 하지 hello 로드 응용 프로그램 수 tooService 패브릭 보고 수에 의해 이루어집니다. 따라서이 시간 hello에 자동 크기 조정 얻게 각 hello 가상 컴퓨터 크기 조정 설정 인스턴스에 의해 발생 하는 hello 성능 카운터에 의해 좌우 순수 하 게 됩니다.  

다음이 지침에 따라 [각 가상 컴퓨터 크기 집합에 대 한 자동 크기 조정을 tooset](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md)합니다.

> [!NOTE]
> 시나리오 축소 노드 형식에 "gold" 또는 실버 내구성 수준 해야 toocall hello [제거 ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/azure/mt125993.aspx) hello 적합 한 노드 이름의 합니다.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Vm tooa 노드 유형/가상 컴퓨터 크기 집합을 수동으로 추가
Hello 샘플/의 지침에에서 따라 hello [빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) 각 Nodetype에 있는 Vm의 toochange hello 수 있습니다. 

> [!NOTE]
> Vm의 추가 데 하지 않을 hello 추가 toobe 순간 되므로 시간이 걸립니다. 따라서 tooallow hello VM 용량 hello 복제본에 대 한 사용 가능 해지기 전에 10 분 동안에 대 한 시간 내에 잘 tooadd 용량 계획/서비스 인스턴스 tooget 배치 합니다.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Hello 주 노드 유형/가상 컴퓨터 크기 집합에서 Vm을 수동으로 제거
> [!NOTE]
> 클러스터의 주 노드 종류 hello에서에서 hello 서비스 패브릭 시스템 서비스를 실행합니다. 종료 하거나 해당 노드 형식에 있는 인스턴스의 hello 수 축소 안 되므로 어떤 hello 안정성 계층 보다 작은 필요 합니다. 너무 참조[여기에 안정성 계층에 대 한 내용은 hello](service-fabric-cluster-capacity.md)합니다. 
> 
> 

Tooexecute 필요한 hello 다음 단계를 한 번에 하나의 VM 인스턴스. 이렇게 하면 hello 시스템 서비스 (및 상태 저장 서비스)에 대 한 toobe 정상적으로 종료를 제거 하는 hello VM 인스턴스 및 다른 노드에서 만든 새 복제 합니다.

1. 실행 [사용 안 함 ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) 의도 'RemoveNode' toodisable hello 노드 (노드 형식에서 가장 높은 인스턴스 hello) tooremove 겠 군요.
2. 실행 [Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake hello 노드에 toodisabled 실제로 전환 하십시오. 파일이 없으면 hello 노드 해제 될 때까지 대기 합니다. 이 단계는 서두를 수 없습니다.
3. Hello 샘플/의 지침에에서 따라 hello [빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) 해당 Nodetype에 따라 Vm의 toochange hello 수 있습니다. 제거 하는 hello 인스턴스는 hello 가장 높은 VM 인스턴스입니다. 
4. 단계 1-3 필요에 따라 반복 hello 주 노드 종류에서 어떤 hello 안정성 계층 수행 되도록 하는 보다 작은 인스턴스의 hello 수를 축소 하지 마십시오. 너무 참조[여기에 안정성 계층에 대 한 내용은 hello](service-fabric-cluster-capacity.md)합니다. 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Hello 기본이 아닌 노드 유형/가상 컴퓨터 크기 집합에서에서 Vm을 수동으로 제거 합니다.
> [!NOTE]
> 상태 저장 서비스에 대 한 필요한 특정 개수의 노드 toobe 항상 toomaintain 가용성과 preserve 서비스의 상태를 합니다. Hello 매우 최소에서 hello 수가 hello 파티션/서비스의 노드 같은 toohello 대상 복제본 집합 수 해야 합니다. 
> 
> 

Hello 필요한 hello 한 번에 하나의 VM 인스턴스 단계를 따라를 실행 합니다. 이렇게 하면 toobe 정상적으로 종료 hello에 VM 인스턴스를 제거 하는 hello 시스템 서비스 (및 상태 저장 서비스)에 대 한 있고 else where 새 복제본은 생성.

1. 실행 [사용 안 함 ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) 의도 'RemoveNode' toodisable hello 노드 (노드 형식에서 가장 높은 인스턴스 hello) tooremove 겠 군요.
2. 실행 [Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake hello 노드에 toodisabled 실제로 전환 하십시오. 그렇지 않으면 요 hello 노드를 사용할 수 없습니다. 이 단계는 서두를 수 없습니다.
3. Hello 샘플/의 지침에에서 따라 hello [빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) 해당 Nodetype에 따라 Vm의 toochange hello 수 있습니다. 이제 hello 가장 높은 VM 인스턴스를 제거 합니다. 
4. 단계 1-3 필요에 따라 반복 hello 주 노드 종류에서 어떤 hello 안정성 계층 수행 되도록 하는 보다 작은 인스턴스의 hello 수를 축소 하지 마십시오. 너무 참조[여기에 안정성 계층에 대 한 내용은 hello](service-fabric-cluster-capacity.md)합니다.

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Service Fabric Explorer에서 볼 수 있는 동작
클러스터 hello 수직 확장 서비스 패브릭 탐색기 hello hello 클러스터의 일부인 (가상 컴퓨터 크기는 인스턴스를 설정 하는 데 사용) 하는 노드 수를 반영 합니다.  그러나 크기를 조정할 때 다운 클러스터 볼 수를 호출 하지 않으면 비정상 상태에 표시 되는 제거 하는 hello 노드/v M 인스턴스에 [제거 ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) hello 적합 한 노드 이름의 합니다.   

이 동작에 대 한 hello 설명은 다음과 같습니다.

hello 서비스 패브릭 탐색기에 나열 된 노드를 반영 하 고 hello 서비스 패브릭 시스템 서비스의 (FM 특히) hello에 /가 노드 hello 클러스터 수에 대해 알고 있습니다. 가상 컴퓨터 크기 집합 hello 크기를 조정할 때 hello VM이 에서만 삭제 FM 시스템 서비스 여전히 것으로 생각 (있던, 매핑된 toohello 삭제 된 VM) 해당 hello 노드는 다시 시도 됩니다. 따라서 서비스 패브릭 탐색기 계속 toodisplay 해당 노드 (하지만 hello 성능 상태는 오류 또는 알 수 없는 일 수 있음).

순서 toomake 노드 VM 제거 될 때 제거 되었는지에 두 가지 옵션이 있습니다.

1) "Gold" 또는 실버 내구성 수준을 선택 (사용 가능한 빨리) 클러스터의 노드 형식을 hello에 대 한를 제공 하는 hello infrastructure 통합 합니다. 다음 자동으로 제거 됩니다 hello 노드 우리의 시스템 (FM) 서비스 상태에서 규모 축소 하는 경우.
너무 참조[hello 내구성 수준 여기에 세부 정보](service-fabric-cluster-capacity.md)

2) Hello VM 인스턴스 축소 되어, 해야 toocall hello [제거 ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/mt125993.aspx)합니다.

> [!NOTE]
> 서비스 패브릭 클러스터 노드 toobe 특정 수를에서 필요한 모든 hello 시간 순서 toomaintain 가용성 및 preserve 상태-참조 tooas "쿼럼을 유지 관리 합니다." 따라서 것이 일반적으로 안전 하지 않은 tooshut hello 클러스터의 모든 hello 컴퓨터 다운 처음 수행 하지 않는 한는 [시/도의 전체 백업](service-fabric-reliable-services-backup-restore.md)합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
클러스터 용량 계획, 클러스터를 업그레이드 및 서비스를 분할 하는 방법에 대 한 자세한 내용은 tooalso 다음 읽기 hello:

* [클러스터 용량 계획](service-fabric-cluster-capacity.md)
* [클러스터 업그레이드](service-fabric-cluster-upgrade.md)
* [최대 크기를 위해 상태 저장 서비스 분할](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
