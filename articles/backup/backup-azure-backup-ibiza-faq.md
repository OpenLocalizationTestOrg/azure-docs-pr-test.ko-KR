---
title: "aaaRecovery 서비스 자격 증명 모음에 FAQ | Microsoft Docs"
description: "이 버전의 hello FAQ hello Azure 백업 서비스의 hello 공개 미리 보기 릴리스를 지원 합니다. Hello 백업 에이전트가 있는 경우, 백업 및 보존, 복구, 보안 및 Azure 백업 솔루션 hello에 대 한 다른 일반적인 질문에 대 한 질문과 대답 toofrequently 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "백업 솔루션; 백업 서비스"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>복구 서비스 자격 증명 모음 - FAQ
이 문서에서는 특정 tooRecovery 서비스 자격 증명 모음 정보를 제공 하 고 hello을 보완 [Azure 백업 FAQ](backup-azure-backup-faq.md)합니다. hello Azure 백업 FAQ 질문 및 답변 hello Azure 백업 서비스에 대 한 hello 전체 집합을 제공합니다.  

이 문서 또는 관련된 문서 Disqus 섹션 hello에 Azure 백업에 대 한 질문을 요청할 수 있습니다. Hello에 hello Azure 백업 서비스에 대 한 질문을 게시할 수도 있습니다 [토론 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)합니다.

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Recovery Services 자격 증명 모음은 Resource Manager에 기반합니다. Backup 자격 증명 모음(기본 모드)은 계속 지원되나요? <br/>
예, 백업 자격 증명 모음도 계속 지원됩니다. Hello에서 백업 자격 증명 모음 만들기 [클래식 포털](https://manage.windowsazure.com)합니다. Hello에 복구 서비스 자격 증명 모음 만들기 [Azure 포털](https://portal.azure.com)합니다. 그러나 모든 향후 기능 향상으로 있습니다 toocreate 복구 서비스 자격 증명 모음 권장 복구 서비스 자격 증명 모음에만 사용할 수 있습니다.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>백업 자격 증명 모음 tooa 복구 서비스 자격 증명 모음을 마이그레이션할 수 있습니까? <br/>
아쉽게도 아니요, 지금은 마이그레이션할 수 없습니다 hello 복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 내용의 압축 합니다. 이 기능을 추가하려고 노력하고 있지만 공개 미리 보기의 일환으로 사용할 수 없습니다.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>복구 서비스 자격 증명 모음은 클래식 VM 또는 Resource Manager 기반 VM을 지원하나요? <br/>
Recovery Services 자격 증명 모음은 두 모델을 모두 지원합니다.  (임 클래식 모드 Vm) hello 클래식 포털에서 만들어진 VM 백업할 수 있습니다 또는 VM hello (임 기반 리소스 관리자)는 Azure 포털에서에서 만든 tooa 복구 서비스 자격 증명 모음입니다.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>백업 자격 증명 모음에 내 클래식 VM을 백업했습니다. 이제 toomigrate 클래식 모드 tooResource 관리자 모드에서 내 Vm 합니다.  복구 서비스 자격 증명 모음에서 백업하려면 어떻게 해야 하나요?
백업 자격 증명 모음에 있는 기존 Vm의 백업을 않습니다 자동으로 toorecovery 서비스 자격 증명 모음 마이그레이션할 때 마이그레이션할 hello Vm 클래식 tooResource 관리자 모드에서. VM 백업의 마이그레이션을 위한 다음 단계를 따르세요.

1. 백업 자격 증명 모음에서 이동 너무**보호 된 항목** 탭 하 고 hello VM을 선택 합니다. [보호 중지](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)를 클릭합니다. *연결된 백업 데이터 삭제* 옵션을 **검사하지 않음**으로 둡니다.
2. Hello에 [Azure 포털](https://portal.azure.com), toohello 이동 **확장** 메뉴에 대 한 VM hello 및 hello 제거 **VMSnapshot/VMSnapshotLinux** 확장 합니다.
3. 클래식 모드 tooResource 관리자 모드에서 hello 가상 컴퓨터를 마이그레이션하십시오. 저장소 및 toovirtual 컴퓨터에 해당 하는 네트워크는도 마이그레이션된 tooResource 관리자 모드에 있는지 확인 합니다.
4. 복구 서비스 자격 증명 모음 만들기 및 구성 hello에 백업 마이그레이션된 가상 컴퓨터를 사용 하 여 **백업** 자격 증명 모음 대시보드를 기반으로 동작 합니다. 너무 자세한 방법에 대 한 자세한 내용은[복구 서비스 자격 증명 모음에는 백업을 사용 하도록 설정](backup-azure-vms-first-look-arm.md)
