---
title: "Linux VM 배포 RM aaaTroubleshoot | Microsoft Docs"
description: "Azure에서 새 Linux 가상 컴퓨터 생성 시 Resource Manager 배포 문제 해결"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Azure에서 새 Linux 가상 컴퓨터 생성 관련 Resource Manager 배포 문제 해결
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>주요 문제
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

VM 배포 문제 및 질문은 [Azure에서 Linux 가상 컴퓨터 배포 문제 해결](troubleshoot-deploy-vm.md)을 참조하세요.
## <a name="collect-activity-logs"></a>활동 로그 선택
문제 해결, toostart 수집 hello 활동 hello 문제와 연결 된 tooidentify hello 오류를 기록 합니다. hello 다음 링크 포함 프로세스 toofollow hello에 대 한 자세한 정보.

[배포 작업 보기](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Azure 활동 로그 toomanage 보기 리소스](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** hello OS 일반화, Linux 및 이며 업로드 또는 설정, 일반화 hello를 사용 하 여 캡처할 경우 모든 오류 수 없습니다. 마찬가지로, Linux 특수화 되 고 업로드 하거나 사용 하 여 캡처할 운영 체제 hello는 hello 오류 않을 다음 설정을 특수화 된입니다.

**업로드 오류:**

**N<sup>1</sup>:** hello OS 일반화, Linux 이며으로 업로드 되는 경우 특수화 했으므로 발생 합니다 프로비저닝 시간 초과 오류가 hello VM 단계 프로 비전 하는 hello에서 중단 됩니다.

**N<sup>2</sup>:** hello 새 VM으로 실행 되 고 hello 원래 컴퓨터 이름, 사용자 이름 및 암호 때문에 프로 비전 실패 오류가 발생 합니다 hello OS 이면 Linux 특수화 및 일반화으로 업로드 됩니다.

**해결 방법:**

tooresolve 이러한 두 오류 업로드 원본 VHD를 사용할 수 있는 온-프레미스 hello, 동일한 hello hello (일반화/특수화) 운영 체제에 대 한 유형을 설정 합니다. 일반화 하면 대로 tooupload 기억 toorun-먼저 프로 비전 해제 합니다.

**캡처 오류:**

**N<sup>3</sup>:** hello OS 일반화, Linux 이며로 캡처된 경우 특수화를 얻게 됩니다 프로비저닝 시간 초과 오류가 hello 원래 VM 사용 가능 하지 않습니다 일반화 된 상태로 표시 되기 때문에 있습니다.

**N<sup>4</sup>:** hello 새 VM으로 실행 hello 원래 컴퓨터 이름, 사용자 이름 및 암호 프로 비전 실패 오류가 hello OS Linux 특수화 및 일반화 된 대로 캡처 이면 발생 합니다. 또한 hello 원본 VM을 사용할 수 없으면 표시 되어 있으므로 같이 특수 합니다.

**해결 방법:**

tooresolve 이러한 두 오류 hello 포털에서 hello 현재 이미지를 삭제 하 고 [hello에서 다시 캡처 현재 Vhd](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 와 hello hello (일반화/특수화) 운영 체제에 대 한 설정 것과 동일한 합니다.

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>문제: 사용자 지정/ 갤러리/ 마켓플레이스 이미지; 할당 오류
이 오류는 hello 새 VM 요청은 요청 되 고 hello v M 크기를 지원할 수 없는 또는 사용 가능한 공간 tooaccommodate hello 요청에 없는 고정 된 tooa 클러스터 때 경우에 발생 합니다.

**원인 1:** hello 클러스터를 지원할 수 없는 hello 요청 된 VM 크기입니다.

**해결 방법 1:**

* 더 작은 VM 크기를 사용 하 여 hello 요청을 다시 시도 하십시오.
* Hello 크기인 요청한 경우 hello VM을 변경할 수 없습니다.
  * Hello 가용성 집합에 있는 모든 hello Vm을 중지 합니다.
    **리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.
  * 모든 Vm 중지 hello, 끝났으면 hello hello에 새 VM 원하는 크기입니다.
  * 시작 새 VM을 먼저 hello 하 고 각 선택의 hello 클릭 하 고 Vm을 중지 하는 다음 **시작**합니다.

**원인 2:** hello 클러스터 리소스를 해제가 없습니다.

**해결 방법 2:**

* 나중에 hello 요청을 다시 시도 합니다.
* Hello 새 VM 수 있는 경우 다른 가용성의 일부 설정 합니까
  * 다른 가용성 집합에 새 VM을 만듭니다 (hello에 동일한 지역).
  * 새 VM toohello hello 추가 동일한 가상 네트워크입니다.

## <a name="next-steps"></a>다음 단계
중지된 Linux VM을 시작하거나 Azure에서 기존 Linux VM의 크기를 조정할 때 문제가 발생하면 [Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 Resource Manager 배포 문제 해결](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.

