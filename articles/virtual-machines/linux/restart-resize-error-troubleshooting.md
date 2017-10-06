---
title: "Azure에서 다시 시작 하거나 크기를 조정할 aaaVM 발급 | Microsoft Docs"
description: "Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 Resource Manager 배포 문제 해결"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>Azure에서 기존 Linux VM 재시작 또는 크기 조정 관련 배포 문제 해결
Toostart 중지 된 Azure 가상 컴퓨터 (VM)를 시도 하거나 기존 Azure VM의 크기를 조정할 때 발생 하는 hello 일반적인 오류는 할당 오류입니다. 이 오류는 hello 클러스터 또는 지역 중 하나에 없는 사용 가능한 리소스 또는 없습니다 지원 hello v M 크기를 요청 하는 경우에 발생 합니다.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>활동 로그 선택
문제 해결, toostart 수집 hello 활동 hello 문제와 연결 된 tooidentify hello 오류를 기록 합니다. hello 프로세스에 대 한 자세한 정보를 포함 하는 링크를 따라 hello:

[배포 작업 보기](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Azure 활동 로그 toomanage 보기 리소스](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>문제: 중지된 VM 시작 시 오류
Toostart 중지 된 VM을 시도 하지만 할당에 실패 합니다.

### <a name="cause"></a>원인
toostart hello VM을 중지 하는 hello 요청에 toobe hello 클라우드 서비스를 호스팅하는 hello 원본 클러스터에 시도 되었습니다. 그러나 hello 클러스터 여유 공간이 사용 가능한 toofulfill hello 요청은 없습니다.

### <a name="resolution"></a>해결 방법
* 모든 hello hello 가용성의 Vm을 설정 하 고 각 VM을 다시 중지 합니다.
  
  1. **리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.
  2. 모든 Vm 중지 hello 중지 hello Vm의 각 선택 하 고 시작을 클릭 합니다.
* 나중에 hello를 다시 시작 요청을 다시 시도 합니다.

## <a name="issue-error-when-resizing-an-existing-vm"></a>문제: 기존 VM 재시작 시 오류
Tooresize 기존 VM을 시도 하지만 할당에 실패 합니다.

### <a name="cause"></a>원인
tooresize hello VM에 toobe hello 요청 했으나 hello 원본 클러스터에서 해당 호스트 hello 클라우드 서비스 그러나 hello 클러스터를 지원 하지 않는 요청 된 VM 크기 hello 합니다.

### <a name="resolution"></a>해결 방법
* 더 작은 VM 크기를 사용 하 여 hello 요청을 다시 시도 하십시오.
* Hello 크기인 요청한 경우 hello VM을 변경할 수 없습니다.
  
  1. Hello 가용성 집합에 있는 모든 hello Vm을 중지 합니다.
     
     * **리소스 그룹** > *사용자의 리소스 그룹* > **리소스** > *사용자의 가용성 집합* > **가상 컴퓨터** > *사용자의 가상 컴퓨터* > **중지**를 클릭합니다.
  2. 결국 hello 가상 컴퓨터를 중지, 원하는 hello VM tooa 더 큰 크기의 크기를 조정 합니다.
  3. Select hello 크기를 조정 VM 및 클릭 **시작**, 각 시작의 hello Vm 중지 합니다.

## <a name="next-steps"></a>다음 단계
Azure에서 새 Linux VM을 만들 때 문제가 발생하면 [Azure에서 새 Linux 가상 컴퓨터 생성 관련 배포 문제 해결](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.

