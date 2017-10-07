---
title: "다시 시작 하거나 크기 조정 문제 aaaVM | Microsoft Docs"
description: "Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a>Azure의 기존 Linux 가상 컴퓨터 재시작 또는 크기 조정 관련 클래식 배포 문제 해결
> [!div class="op_single_selector"]
> * [클래식](restart-resize-error-troubleshooting.md)
> * [리소스 관리자](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

Toostart 중지 된 Azure 가상 컴퓨터 (VM)를 시도 하거나 기존 Azure VM의 크기를 조정할 때 발생 하는 hello 일반적인 오류는 할당 오류입니다. 이 오류는 hello 클러스터 또는 지역 중 하나에 없는 사용 가능한 리소스 또는 없습니다 지원 hello v M 크기를 요청 하는 경우에 발생 합니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. Hello 리소스 관리자 버전에 대 한 참조 [여기](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>감사 로그 수집
문제 해결, toostart 수집 hello 감사 hello 문제와 연결 된 tooidentify hello 오류를 기록 합니다.

Hello Azure 포털에서에서 클릭 **찾아보기** > **가상 컴퓨터** > *Linux 가상 컴퓨터*  >   **설정** > **감사 로그**합니다.

## <a name="issue-error-when-starting-a-stopped-vm"></a>문제: 중지된 VM 시작 시 오류
Toostart 중지 된 VM을 시도 하지만 할당에 실패 합니다.

### <a name="cause"></a>원인
toostart hello VM을 중지 하는 hello 요청에 toobe hello 클라우드 서비스를 호스팅하는 hello 원본 클러스터에 시도 되었습니다. 그러나 hello 클러스터 여유 공간이 사용 가능한 toofulfill hello 요청은 없습니다.

### <a name="resolution"></a>해결 방법
* 새 클라우드 서비스를 만들어서 지역 또는 지역 기반 가상 네트워크와 연결하지만 선호도 그룹과는 연결하지 않습니다.
* 삭제 hello VM을 중지 합니다.
* Hello 디스크를 사용 하 여 hello 새 클라우드 서비스에 VM hello를 다시 만듭니다.
* 시작 hello VM을 다시 생성 합니다.

Toocreate 새 클라우드 서비스는 동안 오류가 발생 합니다 나중에 다시 시도 하거나 다른 곳으로 hello 클라우드 서비스에 대 한 hello 영역을 변경 합니다.

> [!IMPORTANT]
> hello 새 클라우드 서비스는 없으므로 새 이름 및 VIP를 hello 기존 클라우드 서비스에 대 한 해당 정보를 사용 하는 모든 hello 종속성에 대 한 정보를 toochange를 해야 합니다.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>문제: 기존 VM 재시작 시 오류
Tooresize 기존 VM을 시도 하지만 할당에 실패 합니다.

### <a name="cause"></a>원인
tooresize hello VM에 toobe hello 요청 했으나 hello 원본 클러스터에서 해당 호스트 hello 클라우드 서비스 그러나 hello 클러스터를 지원 하지 않는 요청 된 VM 크기 hello 합니다.

### <a name="resolution"></a>해결 방법
줄일 hello v M 크기를 요청 하 고 요청을 조정 하는 재시도 hello 합니다.

* **모두 찾아보기** > **가상 컴퓨터(클래식)** > *사용자의 가상 컴퓨터* > **설정** > **크기**를 클릭합니다. 자세한 내용은 참조 [hello 가상 컴퓨터 크기를 조정한](https://msdn.microsoft.com/library/dn168976.aspx)합니다.

가능한 tooreduce hello VM 크기가 없는 경우 다음이 단계를 수행 합니다.

* 연결 된 tooan 선호도 그룹이 아닙니다 실행 하 고 있는 연결 된 tooan 선호도 그룹은 가상 네트워크와 연결 되지 않은 새 클라우드 서비스를 만듭니다.
* 그 안에 큰 규모의 VM을 새로 만듭니다.

모든 Vm을 통합할 수 hello에서 동일한 클라우드 서비스입니다. 기존 클라우드 서비스와 영역 기반 가상 네트워크와 연결 된 경우에 hello 새 클라우드 서비스 toohello 기존 가상 네트워크를 연결할 수 있습니다.

Hello 기존 클라우드 서비스 영역 기반 가상 네트워크에 연결 되어 있으면 다음 hello 기존 클라우드 서비스에 대 한 Vm toodelete hello에 있고 hello 해당 디스크에서 새 클라우드 서비스에서 다시 합니다. 그러나 것이 중요 한 tooremember hello 새 클라우드 서비스 들이 있는 새 이름 및 VIP를 tooupdate 해야 하므로 현재 hello 기존 클라우드 서비스에 대 한이 정보를 사용 하는 모든 hello 종속성에 대 한 이러한 합니다.

## <a name="next-steps"></a>다음 단계
Azure에서 새 Linux VM을 만들 때 문제가 발생하면 [Azure에서 새 Linux 가상 컴퓨터 생성 관련 배포 문제 해결](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.

