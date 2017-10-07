---
title: "Azure에서 Linux Vm에 대 한 aaaResource 그룹 | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Azure 인프라 서비스에서 리소스 그룹을 배포 하기 위한 방법을 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8809cb5eeb9a166d2bcf1946cd26b0ee748f8cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Linux VM에 대한 Azure 리소스 그룹 지침 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

이 문서는 toologically 환경을 구축 하 고 리소스 그룹의 모든 hello 구성 요소를 그룹화 하는 방법을 이해에 중점을 둡니다.

## <a name="implementation-guidelines-for-resource-groups"></a>리소스 그룹에 대한 구현 지침
의사 결정:

* Hello 핵심 인프라 구성 요소에 의해 또는 완전 한 응용 프로그램 배포 하 여 리소스 그룹 아웃 toobuild 예정 입니까?
* Toorestrict 액세스 tooResource 해야 역할 기반 액세스 제어를 사용 하 여 그룹화?

작업:

* 필요한 핵심 인프라 구성 요소와 전용 리소스 그룹을 정의합니다.
* 검토 방법 tooimplement 리소스 관리자 템플릿을 일치, 재현할 수 있는 배포에 유용 합니다.
* 사용자 액세스 제어에 필요한 역할 액세스 tooResource 그룹 정의 합니다.
* 명명 규칙을 사용 하 여 리소스 그룹의 hello 집합을 만듭니다. Hello Azure CLI 또는 포털을 사용할 수 있습니다.

## <a name="resource-groups"></a>리소스 그룹
Azure에서 하면 논리적으로 저장소 계정, 가상 네트워크 및 가상 컴퓨터 (Vm) toodeploy 같이 관련된 리소스를 그룹화, 관리 및 단일 엔터티로 유지 관리 합니다. 이러한 방식을 통해 toodeploy 응용 프로그램을 더 쉽게 모든 hello 유지 관련 정보 이지만 리소스 함께 toogrant 또는 관리 측면에서 다른 사용자의 리소스 액세스 toothat 그룹입니다. 리소스 그룹 이름은 90자까지 지정할 수 있습니다. 리소스 그룹을 보다 포괄적인 이해 hello를 읽을 수 있습니다 [Azure 리소스 관리자 개요](../../azure-resource-manager/resource-group-overview.md)합니다.

Hello 기능 toobuild hello 저장소, 네트워킹, 선언 하는 JSON 파일을 사용 하 여 사용자 환경 및 계산 리소스를 tooResource 그룹은 핵심 기능입니다. 모든 관련된 사용자 지정 스크립트 또는 구성 tooapply 정의할 수 있습니다. 이러한 JSON 템플릿을 사용하여 응용 프로그램에 대해 일관되고 재현 가능한 배포를 만듭니다. 이 방법을 사용 하면 개발에서 환경을 구축 하 고 해당 동일한 템플릿 toocreate 프로덕션 배포를 사용 하 여 또는 그 반대의 경우도 마찬가지입니다. 더 잘 이해 템플릿을 사용 하는 방법에 대 한,에 대 한 읽기 [템플릿 연습 hello](../../azure-resource-manager/resource-manager-template-walkthrough.md) 하는 과정을 안내해 각 단계는 JSON 템플릿 구축 합니다.

리소스 그룹을 사용하여 환경을 디자인할 때 다음 두 가지 방식을 활용할 수 있습니다.

* 리소스 그룹 hello 저장소 계정, 가상 네트워크 및 서브넷으로 Vm 결합 하는 각 응용 프로그램 배포에 대 한 분산 장치 등을 로드 합니다.
* 핵심 가상 네트워킹과 서브넷 또는 저장소 계정이 포함된 중앙 집중식 리소스 그룹. 사용자의 응용 프로그램은 VM, 부하 분산 장치, 네트워크 인터페이스 등만을 포함하는 자체 리소스 그룹에 있게 됩니다.

가상 네트워킹에 대 한 중앙 집중식된 리소스 그룹을 만드는 out, 확장 및 서브넷을 통해 보다 쉽게 toobuild 것 처럼 크로스-프레미스 하이브리드 연결 옵션에 대 한 연결 네트워크입니다. hello 또 다른 방법은 각 응용 프로그램 toohave에 대 한 자체 가상 네트워크에 필요한 구성 및 유지 관리 합니다. [역할 기반 액세스 제어](../../active-directory/role-based-access-control-what-is.md) tooResource 그룹 구체적으로 toocontrol 액세스를 제공 합니다. 프로덕션 응용 프로그램에 대 한 해당 리소스에 액세스할 수 있는 hello 사용자가 제어할 수 있습니다 또는 hello 핵심 인프라 리소스에 대 한 이러한 엔지니어 toowork만 인프라를 제한할 수 있습니다. 응용 프로그램 소유자에 하나만 리소스 그룹 하지 hello 핵심 Azure 인프라의 사용자 환경 내에서 액세스 toohello 응용 프로그램 구성 요소. 환경을 디자인할 때 hello 사용자를 toohello 리소스에 액세스 해야 하 고 그에 따라 리소스 그룹을 디자인 하는 것이 좋습니다. 

## <a name="next-steps"></a>다음 단계
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

