---
title: "명명 지침-Linux aaaAzure 인프라 | Microsoft Docs"
description: "Hello 주요 디자인 및 구현에 대 한 지침 Azure 인프라 서비스에서 이름에 대해 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>Linux VM에 대한 Azure 인프라 명명 지침 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

이 문서는 tooapproach 명명 규칙에 다양 한 모든 Azure 리소스 toobuild 논리 and 쉽게 식별할 수에 대 한 리소스의 환경 전체에서 설정 하는 방법을 이해에 중점을 둡니다.

## <a name="implementation-guidelines-for-naming-conventions"></a>명명 규칙에 대한 구현 지침
의사 결정:

* Azure 리소스에 대한 명명 규칙은 무엇인가?

작업:

* 리소스 toomaintain 일관성 hello affixes toouse를 정의 합니다.
* 저장소 계정 이름을 hello 요구 사항에 대 한 전역 고유 toobe를 정의 합니다.
* 사용 되는 배포 간에 tooall 당사자와 관련 된 tooensure 일관성을 분산 하는 명명 규칙 toobe 문서 hello 합니다.

## <a name="naming-conventions"></a>명명 규칙
Azure에서 항목을 만들기 전에 좋은 명명 규칙이 구현되어 있어야 합니다. 명명 규칙 모든 hello 리소스 hello 관리 비용이 절감 이러한 리소스 관리와 관련 된는 데 도움이 되는 예측 가능한 이름이 있는지 확인 합니다.

전체 조직에 대해 또는 특정 Azure 구독 또는 계정에 대해 정의 된 명명 규칙의 특정 집합 toofollow를 선택할 수 있습니다. 수도 있지만 조직 tooestablish 암시적 규칙 내에서 개별 사용자를 쉽게 Azure 리소스를 사용 하는 경우, Azure에서 함께 작업 하는 팀 toobe 수 tooscale가 필요 합니다.

사전에 명명 규칙 집합을 합의합니다. 규칙 집합에 영향을 미치는 명명 규칙과 관련한 고려 사항이 있습니다.

## <a name="affixes"></a>접사
Toodefine 명명 규칙을 볼 때 결정 인지 여부 hello를 붙일에서:

* hello 이름 시작 부분 hello (접두사)
* hello 이름 끝에 hello (접미사)

Hello를 사용 하 여 리소스 그룹에 대 한 두 가지 가능한 이름 예를 들어, 다음은 `rg` 붙입니다.

* Rg-WebApp(접두사)
* WebApp-Rg(접미사)

Affixes는 hello 특정 리소스를 설명 하는 toodifferent 측면을 참조할 수 있습니다. hello 다음 표에서 일반적으로 사용 되는 몇 가지 예입니다.

| 측면 | 예 | 참고 사항 |
|:--- |:--- |:--- |
| Environment |dev, stg, prod |에 따라 hello 용도 각 환경의 이름입니다. |
| 위치 |usw(West US), use(East US 2) |Hello 데이터 센터의 hello 지역 또는 hello 조직의 hello 지역에 따라. |
| Azure 구성 요소, 서비스 또는 제품 |리소스 그룹은 RG, 가상 네트워크는 VNet |hello에 대 한 리소스를 제공 하는 hello 제품에 따라 다음을 지원 합니다. |
| 역할 |db, 앱, 웹 |Hello 가상 컴퓨터의 hello 역할에 따라. |
| 인스턴스 |01, 02, 03 등 |둘 이상의 인스턴스가 있는 리소스의 경우. 예를들어, 클라우드 서비스의 분산된 웹 서버를 로드합니다. |

명명 규칙을 설정할 때 확인 있는 명확 하 게 상태는 리소스의 위치 (접두사 및 접미사) 각 유형에 toouse affixes 합니다.

## <a name="dates"></a>날짜
리소스의 생성 hello 이름에서 중요 한 toodetermine hello 날짜 방식은 합니다. Hello YYYYMMDD 날짜 형식을 사용 하는 것이 좋습니다. 이 형식을 사용 하면 뿐만 아니라 hello 전체 날짜, 기록 하지만 이름이 hello 날짜만 다른 두 자원을 사전순으로 및 시간순으로 정렬 됩니다.

## <a name="naming-resources"></a>리소스 명명
각 유형의 리소스 hello 명명 규칙에 정의 방법을 tooassign tooeach 리소스의 이름을 정의 하는 규칙 있어야 만들어집니다. 이러한 규칙에는 예를 들어 tooall 유형의 리소스를 적용 해야:

* 구독
* 계정
* 저장소 계정
* 가상 네트워크
* 서브넷
* 가용성 집합
* 리소스 그룹
* 가상 컴퓨터
* 끝점
* 네트워크 보안 그룹
* 역할

설명이 포함 된 이름을 사용 하도록, 이름 hello tooensure 참조 충분 한 정보 toodetermine toowhich 리소스를 제공 합니다.

## <a name="computer-names"></a>컴퓨터 이름
가상 컴퓨터 (VM)를 만들 때 Azure는 VM의 이름을 too64 문자를 hello 리소스 이름에 사용 되는 필요 합니다. Azure 사용 하 여 hello hello VM에에서 설치 된 hello 운영 체제에 대 한 동일한 이름입니다. 그러나 이러한 이름은 수 하지 항상 될 hello 동일한 합니다.

VM를 운영 체제에 이미 있는.vhd 이미지 파일에서 만든 경우에 VM의 운영 체제 컴퓨터 이름으로 hello에서 Azure의 hello VM 이름을 달라질 수 있습니다. 이 경우 난이도 tooVM 관리 하므로 권장 하지는 않습니다, 수준을 추가할 수 있습니다. Hello Azure VM 리소스 hello 이름과 같은 해당 VM의 운영 체제 toohello 할당 하는 hello 컴퓨터 이름으로 이름을 할당 합니다.

Hello Azure VM 이름이 hello 기본 운영 체제 컴퓨터 이름으로 같은 hello 되는 것이 좋습니다.

## <a name="storage-account-names"></a>저장소 계정 이름
이 섹션이 너무 적용 되지 않습니다[Azure 관리 되는 디스크](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)별도 저장소 계정을 만들지 않으면 처럼 합니다. 관리되지 않는 디스크의 경우 저장소 계정 이름에 적용되는 특별한 규칙이 있습니다. 소문자와 숫자만 사용할 수 있습니다. 자세한 내용은 [저장소 계정 만들기](../../storage/storage-create-storage-account.md#create-a-storage-account) 를 참조하세요. 또한, core.windows.net으로 hello 저장소 계정 이름에는 전역적으로 유효 하 고 고유한 DNS 이름 이어야 합니다. 예를 들어 hello 저장소 계정 mystorageaccount을 라고 hello 다음 결과 DNS 이름은 고유 해야 합니다.

* mystorageaccount.blob.core.windows.net
* mystorageaccount.table.core.windows.net
* mystorageaccount.queue.core.windows.net

## <a name="next-steps"></a>다음 단계
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

