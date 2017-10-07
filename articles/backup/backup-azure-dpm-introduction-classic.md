---
title: "DPM 작업 부하 tooAzure 클래식 포털을 aaaBack | Microsoft Docs"
description: "소개 toobacking hello Azure 백업 서비스를 사용 하 여 DPM 서버를"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: "System Center Data Protection Manager, 데이터 보호 관리자, dpm 백업"
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Dpm 작업 부하 tooAzure tooback 준비
> [!div class="op_single_selector"]
> * [Azure 백업 서버](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure 백업 서버(클래식)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM(클래식)](backup-azure-dpm-introduction-classic.md)
>
>

이 문서에서는 System Center Data Protection Manager (DPM) 서버 및 작업 소개 toousing Microsoft Azure 백업 tooprotect를 제공 합니다. 이 문서를 읽어 보면 다음을 이해하게 됩니다.

* Azure DPM 서버 백업 작동 방식
* hello 필수 구성 요소 tooachieve 부드러운 백업 경험
* 발생 하는 일반적인 오류 hello와 방법을 사람과 toodeal
* 지원되는 시나리오

System Center DPM 백업 파일 및 애플리케이션 데이터 TooDPM 백업 된 데이터 디스크에 테이프에 저장할 또는 tooAzure Microsoft Azure 백업에 백업할 수 있습니다. DPM 은 Azure 백업과 다음과 같이 상호작용합니다.

* **물리적 서버 또는 온-프레미스 가상 컴퓨터로 배포 된 DPM** — DPM을 물리적 서버 또는 백업할 수 있습니다는 온-프레미스 Hyper-v 가상 컴퓨터로 배포 되는 경우를 데이터 tooan Azure 백업 자격 증명 모음에 또한 toodisk 및 테이프 백업 합니다.
* **Azure 가상 컴퓨터로 배포하는 DPM** — System Center 2012 R2 업데이트 3부터 DPM을 Azure 가상 컴퓨터로 배포할 수 있습니다. DPM 데이터 tooAzure 디스크를 백업할 수는 Azure 가상 컴퓨터로 배포 하는 경우 toohello DPM Azure 가상 컴퓨터를 연결 하거나 tooan Azure 백업 자격 증명 모음을 백업 하 여 hello 데이터 저장소를 오프 로드할 수 있습니다.

## <a name="why-backup-your-dpm-servers"></a>DPM 서버를 백업하는 이유
Azure 백업을 사용 하 여 DPM 서버를 백업 하기 위한의 hello 비즈니스 이점은 다음과 같습니다.

* 온-프레미스 DPM 배포에 대 한 대체 toolong 용어 배포 tootape로 Azure 백업을 사용할 수 있습니다.
* Azure에서 내 DPM 배포를 Azure 백업 하면 hello Azure 디스크에서에서 toooffload 저장소 수 있게 tooscale를 Azure 백업 및 최신 데이터를 디스크에 오래 된 데이터를 저장 하 여 합니다.

## <a name="how-does-dpm-server-backup-work"></a>DPM 서버 백업 작동 방식
hello 데이터의 지정 시간 스냅숏이 필요한 첫 번째 가상 컴퓨터를 tooback 합니다. hello Azure 백업 서비스를 시작 hello 백업 작업 hello에 예약 된 시간, 및 트리거 hello 예비 내선 번호 tootake 스냅숏으로 합니다. hello 게스트 VSS와 hello 예비 내선 번호 좌표 tooachieve 일관성 서비스 및 일관성에 도달한 후 hello Azure 저장소 서비스의 hello blob 스냅샷 API를 호출 합니다. 이 tooshut 필요 없이 tooget hello 디스크 hello 가상 컴퓨터의 일관 된 스냅숏을 수행 아래로 것입니다.

Hello 스냅숏 수행 된 후 hello 데이터 hello Azure 백업 서비스 toohello 백업 자격 증명 모음으로 전송 됩니다. hello 서비스를 식별 하 고 hello 백업 저장소 및 네트워크를 효율적으로 만드는 hello 마지막 백업에서 변경 된 블록만 hello 전송 담당 합니다. Hello 데이터 전송이 완료 되 면 hello 스냅숏을 제거 되 고 복구 지점이 생성 됩니다. 이 복구 지점은 hello Azure 클래식 포털에서에서 볼 수 있습니다.

> [!NOTE]
> Linux 가상 컴퓨터의 경우 파일 일치 백업만 가능합니다.
>
>

## <a name="prerequisites"></a>필수 조건
DPM 데이터를 Azure 백업 tooback를 다음과 같이 준비 합니다.

1. **백업 자격 증명 모음을 만듭니다**. 구독에서 백업 자격 증명 모음을 만들지 않은 경우 참조 hello Azure이 문서의-포털 버전 [dpm 작업 부하 tooAzure tooback 준비](backup-azure-dpm-introduction.md)합니다.

  > [!IMPORTANT]
  > 2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.
  > 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> 2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다. **2017년 11월 1일까지**:
  >- 모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
  >- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
  >

2. **자격 증명 모음 자격 증명을 다운로드** -에 Azure 백업으로 toohello 자격 증명 모음을 만든 hello 관리 인증서를 업로드 합니다.
3. **Hello Azure 백업 에이전트를 설치 하 고 hello 서버 등록** -에서 Azure 백업, 각 DPM 서버에 hello 에이전트를 설치 하 고 hello 백업 자격 증명 모음에 hello DPM 서버를 등록 합니다.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>요구 사항(및 제한 사항)
* DPM은 물리적 서버 또는 System Center 2012 SP1 또는 System Center 2012 R2에 설치된 Hyper-V 가상 컴퓨터로 실행할 수 있습니다. 최소 System Center 2012 R2 DPM 2012 R2 업데이트 롤업 3에서 실행되는 Azure 가상 컴퓨터 또는 최소 System Center 2012 R2 업데이트 롤업 5에서 실행되는 VMWare의 Windows 가상 컴퓨터로도 실행할 수 있습니다.
* DPM을 System Center 2012 SP1에서 실행 중인 경우 System Center Data Protection Manager SP1용 업데이트 롤업 2를 설치해야 합니다. Hello Azure 백업 에이전트를 설치 하기 전에 이것이 필요 합니다.
* hello DPM 서버에 Windows PowerShell 및.Net 있어야 Framework 4.5가 설치 되어 있습니다.
* DPM은 대부분 작업 tooAzure 백업에 백업할 수 있습니다. Hello Azure 백업에 대 한 참조를 지원 되는 작업의 전체 목록은 아래 항목을 지원 합니다.
* Hello "tootape 복사" 옵션으로 Azure 백업에 저장 된 데이터를 복구할 수 없습니다.
* Azure 계정이 있으세요 hello Azure 백업 기능을 사용 해야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. [Azure 백업 가격 정책](https://azure.microsoft.com/pricing/details/backup/)을 읽어보십시오.
* Azure 백업을 사용 하 여 hello Azure 백업 에이전트 toobe tooback를 원하는 hello 서버에 설치 된 필요 합니다. 각 서버에 백업 되 고, 로컬 여유 저장소로 사용할 수 있는 hello 데이터의 hello 크기의 10% 이상 있어야 합니다. 예를 들어, 100GB 데이터의 백업 10GB의 사용 가능한 공간 hello 스크래치 위치에는 최소가 필요 합니다. Hello 최소 10% 이지만, 가능 hello 캐시 위치에 사용할 로컬 여유 저장소 공간 toobe의 15%를 사용 하는 것이 좋습니다.
* 데이터는 hello Azure 자격 증명 모음 저장소에에서 저장 됩니다. 없는 제한 toohello 양의 데이터 tooan Azure 백업 자격 증명 모음에 백업할 수 있지만 (예: 가상 컴퓨터 또는 데이터베이스) 데이터 소스의 hello 크기 54,400 GB를 초과 하지 않아야 합니다.

이러한 파일 형식은 tooAzure 백업에 대 한 지원 됩니다.

* 암호화(전체 백업에만 해당)
* 압축(증분 백업 지원)
* 스파스(증분 백업 지원)
* 압축 및 스파스(스파스로 처리됨)

다음은 지원하지 않습니다.

* 대/소문자 구분 파일 시스템의 서버는 지원하지 않습니다.
* 하드 링크(건너뜀)
* 재분석 지점(건너뜀)
* 암호화 및 압축(건너뜀)
* 암호화 및 스파스(건너뜀)
* 압축된 스트림
* 스파스 스트림

> [!NOTE]
> s p 1부터, System Center 2012 DPM의 Microsoft Azure 백업을 사용 하 여 DPM tooAzure에 의해 보호 되는 워크 로드를 백업할 수 있습니다.
>
>
