---
title: "aaaInstall hello VMware tooAzure 복제에 대 한 모바일 서비스 | Microsoft Docs"
description: "이 문서에서는 tooinstall hello Azure Site Recovery 서비스와 VMware tooAzure 복제에 대 한 모바일 서비스 에이전트가 hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>10 단계: hello 모바일 서비스를 설치 합니다.


이 문서에서는 어떻게 tooconfigure 원본 및 대상 설정을 복제할 때 온-프레미스 VMware 가상 컴퓨터 tooAzure hello를 사용 하 여 설명 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

hello 모바일 서비스는 컴퓨터에 데이터 쓰기를 캡처하고 toohello 프로세스 서버에 전달 합니다. Tooreplicate tooAzure 하려는 각 컴퓨터에 설치 해야 합니다.

복제를 사용 하는 경우 hello 사이트 복구 프로세스 서버에서 강제 설치를 사용 하 여 hello 모바일 서비스 설명서를 설치 하거나 System Center Configuration Manager 도구를 사용할 수 있습니다. 강제 설치를 사용 하는 경우 복제를 사용할 때 hello 서비스는 hello VM에 설치 됩니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="install-manually"></a>수동 설치

1. Hello 확인 [필수 구성 요소](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) 수동 설치를 위한 합니다.
2. 에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) hello 포털을 사용 하 여 수동 설치에 대 한 합니다.
3. Hello 명령줄에서 tooinstall를 선호 하는 경우에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)합니다.

## <a name="install-from-hello-process-server"></a>Hello 프로세스 서버에서 설치

VM에 대 한 복제를 사용 하도록 설정 하면 hello 프로세스 서버에서 toopush hello 모바일 서비스 설치를 수행 하는 경우에 hello 프로세스 서버 tooaccess hello VM에서 사용할 수 있는 계정이 필요 합니다. hello 계정 hello 강제 설치에만 사용 됩니다.

1. 푸시 설치에 사용할 수 있는 [계정을 만들](vmware-walkthrough-prepare-vmware.md)어야 합니다. 그런 다음 사이트 복구 배포 하는 동안 원본 설정을 구성할 때 원하는 toouse hello 계정을 지정 합니다.
2. 다음에 따라 [이러한 지침](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) toopush Windows 또는 Linux를 실행 하는 Vm에서 모바일 서비스를 hello 하려는 경우.

## <a name="other-methods"></a>다른 방법

에 대 한 자세한 내용은 [Configuration Manager를 사용 하 여 hello 모바일 서비스를 설치](site-recovery-install-mobility-service-using-sccm.md)를 사용 하 여 또는 [Azure 자동화 DSC](site-recovery-automate-mobility-service-install.md)합니다.

## <a name="next-steps"></a>다음 단계

너무 이동[11 단계: 복제 사용](vmware-walkthrough-enable-replication.md)
