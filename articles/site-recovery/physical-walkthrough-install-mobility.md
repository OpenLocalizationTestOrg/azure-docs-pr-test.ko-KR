---
title: "aaaInstall hello 물리적 서버 tooAzure 복제에 대 한 모바일 서비스 | Microsoft Docs"
description: "이 문서에서는 tooinstall hello Azure Site Recovery 서비스와 tooAzure를 복제 하는 물리적 서버에서 모바일 서비스 에이전트가 hello 하는 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>9 단계: hello 모바일 서비스를 설치 합니다.


이 문서에서는 어떻게 tooinstall hello 모바일 서비스 구성 요소를 복제할 때 온-프레미스 Windows/Linux 물리적 서버의 tooAzure, hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

hello 모바일 서비스는 컴퓨터에 데이터 쓰기를 캡처하고 toohello 프로세스 서버에 전달 합니다. Tooreplicate tooAzure 하려는 각 서버에 설치 해야 합니다.

Hello 모바일 서비스를 수동으로 설치할 수 있습니다 또는 복제를 사용 하는 경우 서버 또는 System Center Configuration Manager와 같은 도구를 사용 하 여 사이트 복구 처리 hello에서 강제 설치를 사용 하 여 합니다. 강제 설치를 사용 하는 경우 복제를 사용 하도록 설정 하면 hello 서비스는 hello 서버에 설치 됩니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="install-manually"></a>수동 설치

1. Hello 확인 [필수 구성 요소](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) 수동 설치를 위한 합니다.
2. 에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) hello 포털을 사용 하 여 수동 설치에 대 한 합니다.
3. Hello 명령줄에서 tooinstall를 선호 하는 경우에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)합니다.

## <a name="install-from-hello-process-server"></a>Hello 프로세스 서버에서 설치

컴퓨터에서 복제를 사용 하도록 설정 하면 toopush hello hello 프로세스 서버에서 모바일 서비스를 설치 하려는 경우 hello 프로세스 서버 tooaccess hello 컴퓨터에서 사용할 수 있는 계정이 필요 합니다. hello 계정 hello 강제 설치에만 사용 됩니다.

1. 계정이 생성되지 않은 경우 다음 지침에 따라 만듭니다.

    - 도메인 또는 로컬 계정을 사용할 수 있습니다.
    - Windows 도메인 계정을 사용 하지 않는 경우 필요 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 합니다. 이 hello에 등록할 toodo **찾아**, hello DWORD 항목을 추가 **LocalAccountTokenFilterPolicy**, 값이 1 인 합니다.
    - Windows에서 CLI tooadd hello 레지스트리 항목을 하려는 경우 다음을 입력 합니다.

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Linux 용 hello 계정은 hello 원본 Linux 서버에 루트 이어야 합니다.

2. 다음에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) toopush Windows 또는 Linux를 실행 하는 Vm에서 모바일 서비스를 hello 하려는 경우.

## <a name="other-installation-methods"></a>다른 설치 방법

- [에 대 한 자세한 내용은](site-recovery-install-mobility-service-using-sccm.md) Configuration Manager를 사용 하 여 hello 이동성 서비스를 설치 합니다.
- Azure Automation DSC로 설치에 대해 [자세히 알아보기](site-recovery-automate-mobility-service-install.md)


## <a name="next-steps"></a>다음 단계

너무 이동[10 단계: 복제 사용](physical-walkthrough-enable-replication.md)
