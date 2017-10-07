---
title: "대규모 Azure 가상 컴퓨터 크기 집합으로 aaaWorking | Microsoft Docs"
description: "필요한 항목 집합의 크기를 조정 tooknow toouse 대규모 Azure 가상 컴퓨터"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>대규모 Virtual Machine Scale Sets와 작동
이제 Azure를 만들 수 있습니다 [가상 컴퓨터 크기 집합](/azure/virtual-machine-scale-sets/) too1, 000 Vm 구성의 용량을 사용 합니다. 이 문서에는 _큰 가상 컴퓨터 크기 집합_ 에 크기 집합 Vm 100 보다 toogreater 확장할 수 있는로 정의 됩니다. 이 기능은 확장 집합 속성에 의해 설정됩니다(_singlePlacementGroup=False_). 

부하 분산 및 오류 도메인 tooa 표준 크기 집합으로 동작이 같은 대규모의 특정 측면 설정 합니다. 이 문서는 대규모 집합의 hello 특성에 설명 하 고 어떤 필요한 tooknow toosuccessfully 사용 응용 프로그램 설명 합니다. 

클라우드 인프라에 대규모 배포를 위한 일반적인 방법은 toocreate의 집합이 _확장 단위_, 예를 들어 여러 Vm을 만들어 여러 Vnet 및 저장소 계정에서 집합 확장 합니다. 이 방법은 더 쉽게 비교 하는 관리 toosingle Vm에 제공 되며 여러 확장 단위 특히 여러 개의 가상 네트워크와 끝점 같은 다른 스택이 가능 구성 요소를 필요로 하는 많은 응용 프로그램에 유용 합니다. 하지만 응용 프로그램을 단일 대규모 클러스터 필요한 경우 더 간단한 toodeploy 단일 크기 조정 설정의 too1, 000 Vm 수 있습니다. 예제 시나리오에는 중앙 집중화된 빅 데이터 배포 또는 작업자 노드의 대용량 풀을 간단하게 관리해야 하는 계산 그리드가 있습니다. VM 크기 집합을 함께 [연결 된 데이터 디스크](virtual-machine-scale-sets-attached-disks.md), 대규모 모음을 사용 하면 toodeploy 수천 개의 코어와 페타바이트 규모의 저장소를 단일 작업으로 구성 된 확장 가능한 인프라입니다.

## <a name="placement-groups"></a>배치 그룹 
어떤 원리에 의해는 _큰_ 크기 특별 한 집합은 Vm 수 hello 아니라 hello 수가 _배치 그룹_ 포함 합니다. 배치 그룹은 구문을 비슷한 tooan Azure 가용성 집합을 자체 장애 도메인과 업그레이드 도메인으로. 기본적으로 확장 집합은 최대 100대의 VM을 갖춘 단일 배치 그룹으로 구성됩니다. 눈금 라는 속성을 설정 하는 경우 _singlePlacementGroup_ too_false_, 설정 된 hello 크기 집합의 여러 배치 그룹 구성 될 수 있습니다 및 범위는 0-1, 000 Vm입니다. toohello 기본값을 설정 하면 _true_, 0-100의 범위는 단일 배치 그룹의 구성 크기 집합 되며 Vm입니다.

## <a name="checklist-for-using-large-scale-sets"></a>대규모 확장 집합을 사용하는 경우 검사 목록
응용 프로그램에 대규모 집합을 효율적으로 사용 가능 여부를 toodecide 고려 hello 요구 사항을 준수 합니다.

- 대규모 확장 집합은 Azure Managed Disks가 필요합니다. Managed Disks로 만들어지지 않은 확장 집합은 여러 저장소 계정이 필요합니다(20대의 VM에 대해 하나씩). 대규모 집합은 저장소 계정에 대 한 저장소 오버 헤드를 관리 및 tooavoid hello 실행 위험을 구독으로 제한 하는 관리 하는 디스크 tooreduce 만으로 디자인 된 toowork입니다. 관리 하는 디스크를 사용 하지 않는 경우 제한 too100 Vm 크기 집합에는 합니다.
- Too1, 000 Vm 크기 집합이 Azure 마켓플레이스 이미지에서 만든 확장할 수 있습니다.
- Too100 Vm 크기 집합 (이미지 만들기 및 업로드 하는 사용자가 직접 VM) 사용자 지정 이미지에서 만든 현재 확장할 수 있습니다.
- 계층 4 부하 분산 hello Azure 부하 분산 장치 및 여러 배치 그룹으로 구성 하는 크기 집합에 대해 아직 지원 되지 않습니다. Toouse hello Azure 부하 분산 장치 있는지 hello에 크기 집합을 확인 해야 할 경우이 구성 된 toouse 단일 배치 그룹인 경우, hello 기본 설정 합니다.
- -7 부하 분산 hello Azure 응용 프로그램 게이트웨이 및 모든 크기 집합에 지원 됩니다.
- 크기 집합은 단일 서브넷 정의-여 서브넷 필요한 모든 hello Vm에 대 한 충분히 큰 주소 공간에 있는지 확인 합니다. 기본적으로 눈금 설정 overprovisions (에 대 한 비용이 청구 되지 않습니다는 추가 Vm 배포 시 또는 수평 확장을 만드는) tooimprove 배포 안정성과 성능을 높입니다. 주소 공간 20%를 tooscale를 계획 하는 Vm의 hello 수보다 큰를 허용 합니다.
- Toodeploy 많은 Vm 계획이 있는 경우 프로그램 계산 코어 할당량 제한을 toobe 증가 해야 합니다.
- 장애 도메인 및 업그레이드 도메인은 배치 그룹 내에서만 일관됩니다. 이 아키텍처는 hello 바뀌지 않으면 전반적인 규모의 가용성 때문에 설정할 별개의 물리적 하드웨어와 전체에 고르게 분산 된 Vm 하지만 tooguarantee 두 Vm이 다른 하드웨어에 필요한 경우 서로 다른 오류에 있는지 확인 하는 방법 도메인에 동일한 배치 그룹을 hello 합니다. 오류 도메인 및 배치 그룹 ID는 hello에 표시 된 _인스턴스 보기_ 규모의 VM을 설정 합니다. Hello에 크기 집합 VM의 hello 인스턴스 보기를 볼 수 있습니다 [Azure 리소스 탐색기](https://resources.azure.com/)합니다.


## <a name="creating-a-large-scale-set"></a>대규모 확장 집합 만들기
크기 hello Azure 포털에서에서 집합을 만들 때 허용할 수 있습니다 tooscale toomultiple 배치 그룹 hello 설정 하 여 _제한 tooa 단일 배치 그룹_ hello에 옵션 too_False_ _기본 사항_ 블레이드입니다. 이 옵션 집합 too_False_을 지정할 수는 _인스턴스 수를_ too1, 000의 값입니다.

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

큰 VM 크기 집합 hello를 사용 하 여 만들 수 있습니다 [Azure CLI](https://github.com/Azure/azure-cli) _az vmss 만들_ 명령입니다. 이 명령은 hello를 기반으로 하는 서브넷 크기 같은 지능형 기본값 설정 _인스턴스 수_ 인수:

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
해당 hello 참고 _vmss 만들_ 명령을 지정 하지 않을 경우 특정 구성 값을 기본값입니다. 재정의할 수 있는 toosee hello 사용할 수 있는 옵션을 시도 하십시오.
```bash
az vmss create --help
```

대규모 Azure 리소스 관리자 템플릿을 작성 하 여 집합을 만드는 경우 hello 서식 파일은 Azure 관리 되는 디스크 기반 크기 집합을 만듭니다 있는지 확인 합니다. Hello를 설정할 수 있습니다 _singlePlacementGroup_ hello에 대 한 속성 too_false_ _속성_ hello 섹션 _Microsoft.Compute/virtualMAchineScaleSets_ 리소스입니다. hello 다음 JSON 조각은 표시 hello 1,000 VM 용량 및 hello를 포함 하 여, 확장 집합 템플릿의 hello 시작 _"singlePlacementGroup": false_ 설정:
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
대규모의 전체 예제에 대 한 템플릿을 설정에 너무 참조[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json)합니다.

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>여러 배치 그룹 toospan를 설정 하는 기존 범위로 변환 합니다.
기존 VM 크기 집합 Vm 100 보다 toomore 확장할 수 있는 toomake, 해야 toochange hello _singplePlacementGroup_ 속성 too_false_ hello 규모에 맞게 모델을 설정 합니다. Hello로이 속성을 변경 테스트할 수 [Azure 리소스 탐색기](https://resources.azure.com/)합니다. 기존의 눈금 집합을 선택 찾기 _편집_ hello 변경 _singlePlacementGroup_ 속성입니다. 이 속성을 표시 되지 않으면 hello 크기는 이전 버전의 hello Microsoft.Compute API 집합 확인 될 수 있습니다.

>[!NOTE] 
크기는 단일 배치 그룹만 (hello 기본 동작) tooa 여러 배치 그룹을 지 원하는 지 원하는에서 집합을 변경할 수 있지만 hello 반대로 변환할 수 없습니다. 따라서 대규모 집합 변환 하기 전에 hello 속성을 이해 해야 합니다. 특히, 계층 4 부하 분산 hello Azure 부하 분산 장치 및 필요 하지 않습니다 확인 합니다.


