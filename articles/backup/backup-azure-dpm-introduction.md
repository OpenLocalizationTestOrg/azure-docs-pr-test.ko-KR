---
title: "작업 부하 tooAzure 포털 aaaUse DPM tooback | Microsoft Docs"
description: "소개 toobacking hello Azure 백업 서비스를 사용 하 여 DPM 서버를"
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: "System Center Data Protection Manager, 데이터 보호 관리자, dpm 백업"
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
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

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다. 이 문서에서는 hello 리소스 관리자 모델을 사용 하 여 배포 된 Vm을 복원 하기 위한 hello 정보 및 절차를 제공 합니다.
>
>

System Center DPM 백업 파일 및 애플리케이션 데이터 TooDPM 백업 된 데이터 디스크에 테이프에 저장할 또는 tooAzure Microsoft Azure 백업에 백업할 수 있습니다. DPM 은 Azure 백업과 다음과 같이 상호작용합니다.

* **물리적 서버 또는 온-프레미스 가상 컴퓨터로 배포 된 DPM** — DPM을 물리적 서버 또는 데이터 tooa를 백업할 수 있습니다는 온-프레미스 Hyper-v 가상 컴퓨터로 배포 되는 경우 복구 서비스 자격 증명 모음에 또한 toodisk 하 고 테이프 백업 합니다.
* **Azure 가상 컴퓨터로 배포하는 DPM** — System Center 2012 R2 업데이트 3부터 DPM을 Azure 가상 컴퓨터로 배포할 수 있습니다. DPM 하면 Azure 가상 컴퓨터로 배포 하는 경우 데이터 tooAzure 백업 디스크가 toohello DPM Azure 가상 컴퓨터를 연결 하거나 tooa 복구 서비스 자격 증명 모음에 백업 하 여 hello 데이터 저장소를 오프 로드할 수 있습니다.

## <a name="why-backup-from-dpm-tooazure"></a>DPM tooAzure에서 백업할 이유?
Azure 백업을 사용 하 여 DPM 서버를 백업 하기 위한의 hello 비즈니스 이점은 다음과 같습니다.

* 온-프레미스 DPM 배포에 대 한 대체 toolong 용어 배포 tootape로 Azure를 사용할 수 있습니다.
* Azure에서 내 DPM 배포를 Azure 백업 하면 hello Azure 디스크에서에서 toooffload 저장소 수 있게 tooscale를 복구 서비스 자격 증명 모음 및 최신 데이터를 디스크에 오래 된 데이터를 저장 하 여 합니다.

## <a name="prerequisites"></a>필수 조건
DPM 데이터를 Azure 백업 tooback를 다음과 같이 준비 합니다.

1. **복구 서비스 자격 증명 모음 만들기** - Azure 포털에 자격 증명 모음을 만듭니다.
2. **자격 증명 모음 자격 증명을 다운로드** -tooregister hello DPM 서버 tooRecovery 서비스 자격 증명 모음을 사용 하 여 hello 자격 증명을 다운로드 합니다.
3. **Hello Azure 백업 에이전트 설치** — Azure 백업에서 각 DPM 서버에 hello 에이전트를 설치 합니다.
4. **Hello 서버 등록** -레지스터 hello DPM 서버 tooRecovery 서비스 자격 증명 모음입니다.

### <a name="1-create-a-recovery-services-vault"></a>1. 복구 서비스 자격 증명 모음 만들기
toocreate 복구 서비스 자격 증명 모음:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 허브 메뉴에서 클릭 **찾아보기** hello 리소스 목록에 입력 하 고 **복구 서비스**합니다. Hello 목록이 필터링 됩니다 입력을 시작 하면 사용자의 입력에 기반 합니다. **복구 서비스 자격 증명 모음**을 클릭합니다.

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.
3. Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.

    ![복구 서비스 자격 증명 모음 만들기 5단계](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. 에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다. hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다. 이름을 2~50자 사이로 입력합니다. 문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.
5. 클릭 **구독** toosee hello 사용 가능한 구독 목록입니다. 어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다. 조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.
6. 클릭 **리소스 그룹** toosee 리소스 그룹의 사용 가능한 목록 hello 하거나 클릭 **새로** toocreate 새 리소스 그룹입니다. 리소스 그룹에 대한 전체 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.
7. 클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다.
8. **만들기**를 클릭합니다. 복구 서비스 자격 증명 모음에 만든 toobe hello에 대 한 시간이 걸릴 수 있습니다. Hello hello 포털의 상단 오른쪽 영역에서 상태 알림 hello를 모니터링 합니다.
   자격 증명 모음을 만든 후 hello 포털에서 엽니다.

### <a name="set-storage-replication"></a>저장소 복제 설정
hello 저장소 복제 옵션 지역 중복 저장소와 로컬 중복 저장소는 toochoose가 있습니다. 기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다. 이것이 기본 백업 hello 옵션 집합 toogeo 중복 저장소를 둡니다. 오래 지속되지 않는 저렴한 옵션을 원하는 경우에는 로컬 중복 저장소를 선택합니다. 에 대해 자세히 알아보세요 [지리적 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) hello에 대 한 저장소 옵션 [Azure 저장소 복제 개요](../storage/common/storage-redundancy.md)합니다.

tooedit hello 저장소 복제 설정입니다.

1. 자격 증명 모음 tooopen hello 자격 증명 모음 대시보드 및 hello 설정 블레이드를 선택 합니다. 경우 hello **설정** 블레이드를 열고 하지 않는 **모든 설정을** hello 자격 증명 모음 대시보드에서.
2. Hello에 **설정** 블레이드에서 클릭 **백업 인프라** > **백업 구성** tooopen hello **백업구성** 블레이드입니다. Hello에 **백업 구성** 블레이드에서 자격 증명 모음에 대 한 hello 저장소 복제 옵션을 선택 합니다.

    ![백업 자격 증명 모음 목록](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    자격 증명 모음에 대 한 hello 저장소 옵션을 선택한 후 hello 자격 증명 모음과 준비 tooassociate hello VM 됩니다. toobegin hello 연결 하면 검색 하 고 하는지 등록 hello Azure 가상 컴퓨터.

### <a name="2-download-vault-credentials"></a>2. 저장소 자격 증명 다운로드
hello 자격 증명 모음 자격 증명 파일은 각 백업 자격 증명 모음에 대 한 hello 포털에서 생성 한 인증서입니다. hello 포털 hello 공개 키 toohello 서비스 ACS (액세스 제어)를 업로드합니다. hello hello 인증서의 개인 키를 사용할 수 있는 toohello 사용자 hello 시스템 등록 워크플로에 대 한 입력으로 제공 된 hello 워크플로의 일부분으로 이루어집니다. Hello hello Azure 백업 서비스에서에서 컴퓨터 toosend 백업 데이터 tooan 식별 된 자격 증명 모음을 인증 합니다.

자격 증명 모음 hello hello 등록 워크플로 중에 사용 됩니다. 자격 증명 모음 파일 손상 되지 않도록 hello hello 사용자의 책임 tooensure 이며 Rogue 사용자의 hello 손에 올 경우 hello 자격 증명 모음 자격 증명 파일 일 수 있습니다 tooregister 사용 되는 다른 컴퓨터에 대해 동일한 자격 증명 모음 hello 합니다. 그러나 hello 백업 데이터 toohello 고객에 속한 암호로 암호화 되어, 기존 백업 데이터를 손상 될 수 없습니다. toomitigate이이 내용이 자격 증명 모음 자격 증명이 설정 tooexpire 48hrs에 있습니다. 여러 번 – 복구 서비스의 자격 증명 모음 hello를 다운로드할 수 있습니다 나타나지만 hello 등록 워크플로 중만 hello 최신 자격 증명 모음 자격 증명 파일을 적용할 수 있습니다.

hello Azure 포털에서에서 보안 채널을 통해 hello 자격 증명 모음 자격 증명 파일이 다운로드 됩니다. hello Azure 백업 서비스 hello hello 인증서의 개인 키를 인식 하지 않으며 hello 개인 키 hello 포털 또는 hello 서비스에 유지 되지 않습니다. 다음 단계 toodownload hello 자격 증명 모음 자격 증명 파일 tooa 로컬 컴퓨터 hello를 사용 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 열기 복구 서비스 자격 증명 모음 toowhich toowhich tooregister DPM 컴퓨터를 선택 합니다.
3. 설정 블레이드가 기본적으로 열립니다. 닫혀 있을 경우 클릭 하 여 **설정을** 자격 증명 모음 대시보드 tooopen hello 설정 블레이드에서 합니다. 설정 블레이드에서 **속성**을 클릭합니다.

    ![자격 증명 모음 블레이드 열기](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. Hello 속성 페이지에서 클릭 **다운로드** 아래 **백업 자격 증명**합니다. hello 포털 다운로드 하는 데 사용할 수 있는 hello 자격 증명 모음 자격 증명 파일을 생성 합니다.

    ![다운로드](./media/backup-azure-dpm-introduction/vault-credentials.png)

hello 포털 hello 자격 증명 모음 이름 및 hello의 조합을 현재 날짜를 사용 하 여 자격 증명 모음 자격 증명을 생성 합니다. 클릭 **저장** toodownload hello 자격 증명 모음 자격 증명 toohello 로컬 계정의 다운로드 폴더 또는 hello 자격 증명 모음 자격 증명에 대 한 위치 메뉴 toospecify 저장 hello에서 다른 이름으로 저장을 선택 합니다. 최대 hello 파일 toobe 생성에 대 일 분까지 걸립니다.

### <a name="note"></a>참고
* 해당 hello 자격 증명 모음 자격 증명 파일은 컴퓨터에서 액세스할 수 있는 위치에 저장 확인 합니다. 파일 공유/SMB에 저장 되는지를 hello 액세스 권한을 확인 합니다.
* hello 자격 증명 모음 자격 증명 파일이 hello 등록 워크플로 중에 사용 됩니다.
* hello 자격 증명 모음 자격 증명 파일 48hrs 후에 만료 되며 hello 포털에서 다운로드할 수 있습니다.

### <a name="3-install-backup-agent"></a>3. 백업 에이전트 설치
Hello Azure 백업 자격 증명 모음을 만든 후 각 백업 데이터와 응용 프로그램 수 있는 Windows 컴퓨터 (Windows Server, Windows 클라이언트, System Center Data Protection Manager 서버 또는 Azure 백업 서버 컴퓨터)에 에이전트를 설치 tooAzure 합니다.

1. 열기 복구 서비스 자격 증명 모음 toowhich toowhich tooregister DPM 컴퓨터를 선택 합니다.
2. 설정 블레이드가 기본적으로 열립니다. 닫혀 있을 경우 클릭 하 여 **설정을** tooopen hello 설정 블레이드에서 합니다. 설정 블레이드에서 **속성**을 클릭합니다.

    ![자격 증명 모음 블레이드 열기](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. Hello 설정 페이지에서 클릭 **다운로드** 아래 **Azure 백업 에이전트**합니다.

    ![다운로드](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   Hello 에이전트를 다운로드 한 후 두 번 클릭 MARSAgentInstaller.exe toolaunch hello hello Azure 백업 에이전트를 설치 합니다. Hello 설치 폴더 및 hello 에이전트에 필요한 스크래치 폴더를 선택 합니다. 지정 된 hello 캐시 위치는 hello 백업 데이터의 5% 이상 사용 가능한 공간에 있어야 합니다.
4. 프록시 서버 tooconnect toohello를 사용 하는 경우 인터넷 hello에 **프록시 구성을** 화면에서 hello 프록시 서버 정보를 입력 합니다. 인증 된 프록시를 사용 하면이 화면에 hello 사용자 이름 및 암호 세부 정보를 입력 합니다.
5. hello Azure 백업 에이전트 설치.NET Framework 4.5 및 Windows PowerShell (것 사용할 수 없는 경우 이미) toocomplete hello 설치 합니다.
6. Hello 에이전트가 설치 되 면 **닫기** hello 창.

   ![닫습니다](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. 너무**레지스터 hello DPM 서버** hello에서 toohello 자격 증명 모음의 **관리** 탭을 클릭 하 여에 **온라인**합니다. 그런 다음 **등록**을 선택합니다. Hello 등록 설치 마법사가 열립니다.
8. 프록시 서버 tooconnect toohello를 사용 하는 경우 인터넷 hello에 **프록시 구성을** 화면에서 hello 프록시 서버 정보를 입력 합니다. 인증 된 프록시를 사용 하면이 화면에 hello 사용자 이름 및 암호 세부 정보를 입력 합니다.

    ![프록시 구성](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. Hello 자격 증명 모음 자격 증명 화면에서 이전에 다운로드 된 tooand 선택 hello 자격 증명 모음 자격 증명 파일을 찾습니다.

    ![자격 증명 모음 자격 증명](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    hello 자격 증명 모음 자격 증명 파일이 48에만 유효 합니다. (hello 포털에서 다운로드 된) 후에 시간입니다. (예: "자격 증명 모음 자격 증명을 제공 하는 파일이 만료 되었습니다."),이 화면에 오류가 발생 하는 경우 로그인 toohello Azure 포털 및 다운로드 hello 자격 증명 모음 자격 증명 다시 파일.

    Hello 설치 응용 프로그램에서 액세스할 수 있는 위치에 해당 hello 자격 증명 모음 자격 증명 파일을 사용할 수 있는지 확인 합니다. 발생 하는 경우 액세스 관련된 오류 복사 hello에 대 한 자격 증명 모음 자격 증명 파일을이 컴퓨터의 임시 위치 tooa hello 작업을 다시 시도 합니다.

    잘못 된 자격 증명 모음 자격 증명 오류가 발생 하는 경우 (예를 들어, "잘못 된 자격 증명 모음 자격 증명 제공") hello 파일이 손상 되었거나 hello 복구 서비스와 연결 된 최신 자격도 hello가 없습니다. Hello hello 포털에서 새 자격 증명 모음 자격 증명 파일을 다운로드 한 후 작업을 다시 시도 하십시오. Hello hello 사용자가 클릭 하는 경우이 오류는 일반적으로 발생 **자격 증명 모음 다운로드** hello 연속적으로 Azure 포털에서에서 옵션입니다. 이 경우에 hello 두 번째 자격 증명 모음 자격 증명 파일은 유효 합니다.
10. 작업 시간 및 휴무 시간 hello에서 하는 동안 네트워크 대역폭 toocontrol hello 사용량 **제한 설정** 화면에서 있습니다 수 hello 대역폭 사용 제한을 설정 하 고 hello 작업 정의 및 휴무 시간입니다.

    ![제한 설정](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. Hello에 **복구 폴더 설정** 화면 hello 파일 Azure에서 다운로드 하는 hello 폴더를 임시로 준비에 대 한를 검색 합니다.

    ![복구 폴더 설정](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. Hello에 **암호화 설정** 화면에서 암호를 생성 하거나 (최소 16 자) 암호를 제공할 수 있습니다. 안전한 위치에 toosave hello 암호를 기억 합니다.

    ![암호화](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > 암호를 분실 하거나 잊어버린; 경우 hello Microsoft는 hello 백업 데이터를 복구할 수 없습니다. hello 최종 사용자 hello 암호화의 암호를 소유 하 고 hello 최종 사용자가 사용 되는 hello 암호에 대 한 가시성 갖고 있지 않습니다. 복구 작업 중 필요한는 hello 파일을 안전한 위치에 저장 하십시오.
    >
    >
13. Hello를 클릭 한 후 **등록** 단추, hello 컴퓨터 등록 하는 성공적으로 toohello 자격 증명 모음 사용자가 지금 준비 toostart tooMicrosoft Azure 백업 합니다.
14. Data Protection Manager를 사용할 때는 hello를 클릭 하 여 hello 등록 워크플로 중 지정 된 hello 설정을 수정할 수 있습니다 **구성** 옵션을 선택 하 여 **온라인** hello 아래  **관리** 탭 합니다.

## <a name="requirements-and-limitations"></a>요구 사항(및 제한 사항)
* DPM은 물리적 서버 또는 System Center 2012 SP1 또는 System Center 2012 R2에 설치된 Hyper-V 가상 컴퓨터로 실행할 수 있습니다. 최소 System Center 2012 R2 DPM 2012 R2 업데이트 롤업 3에서 실행되는 Azure 가상 컴퓨터 또는 최소 System Center 2012 R2 업데이트 롤업 5에서 실행되는 VMWare의 Windows 가상 컴퓨터로도 실행할 수 있습니다.
* DPM을 System Center 2012 SP1에서 실행 중인 경우,  System Center Data Protection Manager SP1용 업데이트 롤업 2를 설치해야 합니다. Hello Azure 백업 에이전트를 설치 하기 전에 이것이 필요 합니다.
* hello DPM 서버에 Windows PowerShell 및.Net 있어야 Framework 4.5가 설치 되어 있습니다.
* DPM은 대부분 작업 tooAzure 백업에 백업할 수 있습니다. Hello Azure 백업에 대 한 참조를 지원 되는 작업의 전체 목록은 아래 항목을 지원 합니다.
* Hello "tootape 복사" 옵션으로 Azure 백업에 저장 된 데이터를 복구할 수 없습니다.
* Azure 계정이 있으세요 hello Azure 백업 기능을 사용 해야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. [Azure 백업 가격 정책](https://azure.microsoft.com/pricing/details/backup/)을 읽어보십시오.
* Azure 백업을 사용 하 여 hello Azure 백업 에이전트 toobe tooback를 원하는 hello 서버에 설치 된 필요 합니다. 각 서버에 백업 되 고, 로컬 여유 저장소로 사용할 수 있는 hello 데이터의 hello 크기의 5% 이상이 있어야 합니다. 예를 들어, 100GB 데이터를 백업 하려면 hello 스크래치 위치에 사용 가능한 공간이 5GB 이상이 필요 합니다.
* 데이터는 hello Azure 자격 증명 모음 저장소에에서 저장 됩니다. 없는 제한 toohello 양의 데이터 tooan Azure 백업 자격 증명 모음에 백업할 수 있지만 (예: 가상 컴퓨터 또는 데이터베이스) 데이터 소스의 hello 크기 54400 GB를 초과 하지 않아야 합니다.

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
> System Center 2012 DPM s p 1부터에서 Microsoft Azure 백업을 사용 하 여 DPM tooAzure에 의해 보호 되는 워크 로드를 백업할 수 있습니다.
>
>
