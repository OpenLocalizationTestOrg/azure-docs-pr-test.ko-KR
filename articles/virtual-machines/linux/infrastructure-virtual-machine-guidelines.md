---
title: "Linux 가상 컴퓨터 지침 aaaAzure | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Linux 가상 컴퓨터를 Azure로 배포 하기 위한 방법을 알아봅니다"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 740767d7-9a40-407b-93e7-c29dd976ffd7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: 0f779f791005441b6b16e106a3dc5a095bb33034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a>Linux용 Azure 가상 컴퓨터 지침
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

이 문서에서는 Azure 환경 내에서 이해 hello 계획 단계를 만들고 가상 컴퓨터 (Vm)를 관리 하는 데 필요한 합니다.

## <a name="implementation-guidelines-for-vms"></a>VM에 대한 구현 지침
의사 결정:

* 인프라의 다양한 응용 프로그램 계층 및 구성 요소를 위해 몇 개의 VM이 필요한가?
* 각 VM에 CPU 및 메모리 리소스를 필요, 및 hello 저장소 요구 사항은 무엇입니까?

작업:

* Vm이 필요 하면 응용 프로그램 및 hello 리소스 hello에 대 한 hello 작업을 정의 합니다.
* 적절 한 VM 크기 및 저장소 형식 hello 사용 하 여 각 VM에 대 한 hello 리소스 수요를 맞춥니다.
* Hello 다양 한 계층 및 인프라의 구성 요소에 대 한 리소스 그룹을 정의 합니다.
* VM 명명 규칙을 정의합니다.
* Hello Azure CLI, 웹 포털, 또는 리소스 관리자 템플릿을 사용 하 여 Vm을 만듭니다.

## <a name="virtual-machines"></a>가상 컴퓨터
Hello Azure 환경 내에서 주 리소스 중 하나 가능성이 Vm입니다. 이 리소스에서 응용 프로그램, 데이터베이스, 인증, 서비스 등을 실행합니다.

중요 한 toounderstand hello [다른 VM 크기](sizes.md) toocorrectly 사용자 환경, 성능 및 비용 측면에서 크기 조정 합니다. VM에 충분한 CPU 코어 또는 메모리가 없으면 디자인 및 개발 품질과 관계없이 응용 프로그램의 성능이 저하됩니다. 검토 hello 인프라에서 각 구성 요소에 대 한 어떤 크기 VM toouse를 결정 하는 대로 시작 지점으로 각 VM 시리즈에 대 한 작업을 권장 합니다. 있습니다 수 [VM의 hello 크기 변경](change-vm-size.md) 배포 후 합니다.

저장소는 VM의 성능에 중요한 역할을 합니다. 일반 스핀 디스크를 사용하는 Standard 저장소를 사용할 수도 있고, I/O 워크로드가 높고 최고의 성능이 필요한 경우에는 SSD 디스크를 사용하는 Premium 저장소를 사용할 수도 있습니다. 으로 hello v M 크기와 비용을 고려 사항 tooselecting hello 저장 미디어입니다. Hello를 읽을 수 [저장소 인프라 지침 문서](infrastructure-storage-solutions-guidelines.md) toounderstand toodesign Vm의 최적의 성능을 위해 저장소를 적절 하는 방법입니다.

## <a name="resource-groups"></a>리소스 그룹
VM과 같은 구성 요소는 손쉬운 관리 및 유지 관리를 위해 [Azure 리소스 그룹](../../azure-resource-manager/resource-group-overview.md)을 사용하여 논리적으로 그룹화됩니다. 리소스 그룹을 사용 하 여 만들 관리 고 지정된 된 응용 프로그램을 구성 하는 모든 hello 리소스를 모니터링할 수 있습니다. 구현할 수도 있습니다 [역할 기반 액세스 제어](../../active-directory/role-based-access-control-what-is.md) toogrant 액세스 tooothers 필요한 팀 tooonly hello 리소스 내에서. 시간 tooplan 리소스 그룹 및 역할 할당을 수행 합니다. 다양 한 접근 방법 tooactually 디자인 및 구현 리소스 그룹, 있는지 tooread hello 수 있으므로 [리소스 그룹 지침 문서](infrastructure-resource-groups-guidelines.md) toounderstand 최선의 방법 toobuild Vm 아웃 합니다.

## <a name="templates"></a>템플릿
Toocreate 선언적 JSON 파일에 정의 된 서식 파일을 빌드할 수 Vm입니다. 일반적으로 만드는 템플릿을 hello 필요한 저장소, 네트워킹, 네트워크 인터페이스, IP 주소 지정, hello Vm 함께 등입니다. 개발 및 테스트 목적으로 tooeasily 복제 프로덕션 환경에 대 한 템플릿 toocreate 일관 되 고 재현할 수 있는 환경을 사용할 수 있습니다 및 그 반대의 경우도 마찬가지입니다. 에 대 한 자세한 내용은 [빌드 및 템플릿을 사용 하 여](../../azure-resource-manager/resource-group-overview.md#template-deployment) 사용 하 여 Vm에 배포 하기 위한 하는 방법을 toounderstand 합니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

