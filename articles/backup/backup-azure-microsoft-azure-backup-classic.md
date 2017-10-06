---
title: "작업 부하 tooAzure 클래식 포털을 aaaUse Azure 백업 서버 tooback | Microsoft Docs"
description: "사용자 환경에서 제대로 tooback Azure 백업 서버를 사용 하 여 워크 로드를 준비 하 고 있는지 확인"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: "azure 백업 서버; 백업 자격 증명 모음"
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Azure 백업 서버를 사용 하 여 워크 로드를 tooback 준비
> [!div class="op_single_selector"]
> * [Azure 백업 서버](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure 백업 서버(클래식)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM(클래식)](backup-azure-dpm-introduction-classic.md)
>
>

이 문서는 Azure 백업 서버를 사용 하 여 워크 로드를 사용자 환경 tooback 준비에 대 한 합니다. Azure 백업 서버로 Hyper-V VM, Microsoft SQL Server, SharePoint Server, 단일 콘솔의 Microsoft Exchange 및 Windows 클라이언트와 같은 응용 프로그램 워크로드를 보호할 수 있습니다.

> [!WARNING]
> Azure 백업 서버 작업을 백업에 대 한 hello 기능 Data Protection Manager (DPM)를 상속합니다. 이러한 기능 중 일부에 대 한 tooDPM 설명서 포인터를 찾을 수 있습니다. 그러나 Azure 백업 서버는 테이프에 대한 보호 기능을 제공하거나 System Center와 통합하지 않습니다.
>
>

## <a name="1-windows-server-machine"></a>1. Windows Server 컴퓨터
![1단계](./media/backup-azure-microsoft-azure-backup/step1.png)

Azure 백업 서버 hello 시작 및 실행 hello 첫 번째 단계는 toohave Windows Server 컴퓨터.

| 위치 | 최소 요구 사항 | 추가 지침 |
| --- | --- | --- |
| Azure |Azure IaaS 가상 컴퓨터<br><br>A2 표준: 2개 코어, 3.5GB RAM |Windows Server 2012 R2 데이터 센터의 간단한 갤러리 이미지로 시작할 수 있습니다. [Azure 백업 서버(DPM)를 사용하여 IaaS 워크로드를 보호하는 데는](https://technet.microsoft.com/library/jj852163.aspx) 미묘한 많은 차이가 있습니다. 읽어 hello 문서 완전히 hello 컴퓨터를 배포 하기 전에 확인 합니다. |
| 온-프레미스 |Hyper-V VM,<br> VMWare VM,<br> 또는 물리적 호스트<br><br>2개 코어 및 4GB RAM |Windows Server 중복 제거를 사용 하 여 hello DPM 저장소 중복 제거 수 있습니다. [DPM 및 중복 제거](https://technet.microsoft.com/library/dn891438.aspx) 가 Hyper-V VM에 배포될 때 함께 작동하는 방법에 대해 자세히 알아보세요. |

> [!NOTE]
> Windows Server 2012 R2 데이터 센터가 있는 컴퓨터에 Azure 백업 서버를 설치하는 것이 좋습니다. Hello 필수 소프트웨어의 많은 hello hello Windows 운영 체제의 최신 버전으로 자동으로 다룹니다.
>
>

Azure 백업 서버 tooa 도메인 toojoin 하려는 경우 hello Azure 백업 서버 소프트웨어를 설치 하기 전에 hello 물리적 서버 또는 가상 컴퓨터 toohello 도메인을 조인 하는 것이 좋습니다. 배포 후 Azure 백업 서버 tooa 새 도메인 이동이 *지원 되지 않습니다*합니다.

## <a name="2-backup-vault"></a>2. 백업 자격 증명 모음
![2단계](./media/backup-azure-microsoft-azure-backup/step2.png)

백업 데이터 tooAzure 보내거나 로컬로 유지 여부를 Azure 백업 서버 hello 자격 증명 모음 등록된 tooa 이어야 합니다. 새로운 Azure Backup 사용자 toouse Azure 백업 서버를 사용할 경우 참조 hello Azure이 문서의-포털 버전 [tooback Azure 백업 서버를 사용 하 여 워크 로드를 준비](backup-azure-microsoft-azure-backup.md)합니다.

> [!IMPORTANT]
> 2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> 2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다. **2017년 11월 1일까지**:
>- 모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>



## <a name="3-software-package"></a>3. 소프트웨어 패키지
![3단계](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Hello 소프트웨어 패키지를 다운로드합니다.
비슷한 toovault 자격 증명을 다운로드할 수 있습니다 Microsoft Azure 백업을 hello에서 응용 프로그램 작업에 대 한 **빠른 시작 페이지** hello 백업 자격 증명 모음의 합니다.

1. 클릭 **에 대 한 응용 프로그램 작업 (디스크 tooDisk tooCloud)**합니다. 그러면 이동 toohello 다운로드 센터 페이지에서 hello 소프트웨어 패키지를 다운로드할 수 있습니다.

    ![Microsoft Azure 백업 시작 화면](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. **다운로드**를 클릭합니다.

    ![다운로드 센터 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. 모든 hello 파일을 선택 하 고 클릭 **다음**합니다. 다운로드 파일 hello Microsoft Azure 백업 다운로드 페이지에서 들어오는 hello 모든 및 위치에 있는 파일을 hello 모든 hello 동일한 폴더입니다.
   ![다운로드 센터 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    이므로 hello 모든 hello 파일의 다운로드 크기 함께 > 3g, too60까지 걸릴 수 있으므로 10Mbps 다운로드 링크에서 hello에 대 한 분 toocomplete을 다운로드 합니다.

### <a name="extracting-hello-software-package"></a>Hello 소프트웨어 패키지를 추출합니다.
모든 hello 파일을 다운로드 한 후 클릭 **MicrosoftAzureBackupInstaller.exe**합니다. Hello을 시작 합니다. **Microsoft Azure 백업 설정 마법사** tooextract hello 설치 프로그램 파일을 사용자가 지정한 tooa 위치입니다. Hello 마법사를 계속 하 고 hello에서 클릭 **추출** toobegin hello 추출 프로세스 단추입니다.

> [!WARNING]
> 4GB 이상의 여유 공간이 필요한 tooextract hello 설치 파일입니다.
>
>

![Microsoft Azure 백업 설정 마법사](./media/backup-azure-microsoft-azure-backup/extract/03.png)

한 번 hello 추출 프로세스 완료를 확인 hello 상자 toolaunch hello 새로 추출한 *setup.exe* toobegin Microsoft Azure 백업 서버를 설치 하 고 hello에서 클릭 **마침** 단추 합니다.

### <a name="installing-hello-software-package"></a>Hello 소프트웨어 패키지 설치
1. 클릭 **Microsoft Azure 백업** toolaunch hello 설정 마법사입니다.

    ![Microsoft Azure 백업 설정 마법사](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Hello 시작 화면에 hello 클릭 **다음** 단추입니다. 이렇게 하면 toohello *Prerequisite Checks* 섹션. 이 화면에서 hello 클릭 **확인** Azure 백업 서버에 대 한 hello 하드웨어 및 소프트웨어 필수 조건이 갖추어 졌 toodetermine 단추입니다. 모든 필수 구성 요소는 hello 조건이 충족 되 성공적으로 해당 hello 컴퓨터 hello 요구 사항을 충족 하는지 나타내는 메시지가 표시 됩니다. Hello 클릭 **다음** 단추입니다.

    ![Azure 백업 서버 - 시작 및 필수 조건 확인](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Microsoft Azure 백업 서버에 SQL Server Standard 필요 하 고 hello Azure 백업 서버 설치 패키지 필요한 hello 적절 한 SQL Server 바이너리 번들로 묶은 제공 합니다. 새 Azure 백업 서버 설치를 시작할 때 hello 옵션을 선택 해야 **이 설치를 새 SQL Server 인스턴스 설치** hello 클릭 **확인 후 설치** 단추입니다. Hello 필수 구성 요소가 성공적으로 설치 되 면 클릭 **다음**합니다.

    ![Azure 백업 서버 - SQL 확인](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    권장 사항 toorestart hello 컴퓨터와 함께 실패 한 경우 작업을 수행 하 고 클릭 **다시 확인**합니다.

   > [!NOTE]
   > Azure 백업 서버는 원격 SQL Server 인스턴스에서 작동하지 않습니다. Azure 백업 서버에서 사용 하 고 hello 인스턴스 toobe 로컬 필요 합니다.
   >
   >

4. Microsoft Azure 백업 서버 파일의 hello 설치에 대 한 위치를 입력 하 고 클릭 **다음**합니다.

    ![Microsoft Azure 백업 PreReq2](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    hello 스크래치 위치는 tooAzure 백업에 대 한 요구 사항입니다. Hello 스크래치 위치는 hello 데이터의 5% 이상이 toobe toohello 클라우드 백업 계획을 확인 합니다. 디스크 보호에 대 한 별도 디스크 toobe hello 설치가 완료 된 후 구성 해야 합니다. 저장소 풀에 관련된 자세한 내용은 [저장소 풀 및 디스크 저장소 구성](https://technet.microsoft.com/library/hh758075.aspx)을 참조하세요.
5. 제한된 로컬 사용자 계정에 강력한 암호를 제공하고 **다음**을 클릭합니다.

    ![Microsoft Azure 백업 PreReq2](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Toouse 것인지 선택 *Microsoft Update* 업데이트 및 클릭 toocheck **다음**합니다.

   > [!NOTE]
   > Windows Update에서는 Windows 및 Microsoft Azure 백업 서버과 같은 다른 제품에 대 한 보안 및 중요 업데이트는 업데이트를 tooMicrosoft 리디렉션됩니다 발생 하는 것이 좋습니다.
   >
   >

    ![Microsoft Azure 백업 PreReq2](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. 검토 hello *설정 요약* 클릭 **설치**합니다.

    ![Microsoft Azure 백업 PreReq2](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. hello 설치 단계에서 발생합니다. 첫 번째 단계 hello hello에서에서 Microsoft Azure 복구 서비스 에이전트는 hello 서버에 설치 됩니다. hello 마법사는 또한 인터넷 연결을 확인합니다. 인터넷 연결을 사용할 수 있는 경우 설치를 계속 진행할 수 없으면 tooprovide 프록시 세부 정보 tooconnect toohello 인터넷 필요.

    hello 다음 단계는 tooconfigure hello Microsoft Azure 복구 서비스 에이전트입니다. Hello 구성의 일부로 tooprovide 백업 자격 증명 hello 자격 증명 모음 자격 증명 tooregister hello 컴퓨터 toohello 모음을 해야 합니다. 또한 Azure와 고객의 프레미스 간에 전송 되는 암호 tooencrypt/암호 해독 hello 데이터를 제공 합니다. 자동으로 암호를 생성하거나 최소 16자인 고유의 암호를 제공할 수 있습니다. Hello 에이전트 구성 될 때까지 hello 마법사를 계속 합니다.

    ![Azure 백업 서버 PreReq2](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Hello Microsoft Azure 백업 서버를 등록 성공적으로 완료 되 면 hello 전반적인 설치 마법사 진행 toohello 설치 하 고 SQL Server 및 hello Azure 백업 서버 구성 요소 구성 됩니다. Hello SQL Server 구성 요소 설치가 완료 되 면 hello Azure 백업 서버 구성 요소가 설치 됩니다.

    ![Azure Backup 서버](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Hello 설치 단계 완료 되 면 hello 제품의 바탕 화면 아이콘 만들어집니다도 합니다. Hello 아이콘 toolaunch hello 제품을 두 번 클릭 합니다.

### <a name="add-backup-storage"></a>백업 저장소 추가
hello 첫 번째 백업 복사본은 연결 된 저장소 toohello Azure 백업 서버 컴퓨터에 유지 됩니다. 디스크 추가에 대한 자세한 내용은 [저장소 풀 및 디스크 저장소 구성](https://technet.microsoft.com/library/hh758075.aspx)을 참조하세요.

> [!NOTE]
> Toosend 데이터 tooAzure를 계획 하는 경우에 tooadd 백업 저장소가 필요 합니다. Azure 백업 서버의 현재 아키텍처 hello hello Azure 백업 자격 증명 모음 보유 hello *두 번째* hello 로컬 저장소 hello 첫 번째 (및 필수) 백업 복사본을 보유 하는 동안 hello 데이터의 복사본입니다.  
>
>

## <a name="4-network-connectivity"></a>4. 네트워크 연결
![4단계](./media/backup-azure-microsoft-azure-backup/step4.png)

Azure 백업 서버 제품 toowork hello에 대 한 연결 toohello Azure 백업 서비스를 성공적으로 필요합니다. toovalidate hello 컴퓨터 hello 연결 tooAzure에 있는지 여부를 사용 하 여 hello ```Get-DPMCloudConnection``` hello Azure 백업 서버 PowerShell 콘솔에서 commandlet 합니다. 경우 hello hello commandlet의 출력이 TRUE로 연결, 다른 연결이 없습니다.

Hello에 동시 hello Azure 구독 toobe 정상 상태에 있어야합니다. 구독 및 toomanage hello 상태 toofind 것 toohello 로그인 [구독 포털](https://account.windowsazure.com/Subscriptions)합니다.

Hello Azure 구독 및 hello Azure 연결의 hello 상태를 확인 했으면 hello 영향 아웃 toofind 아래 hello 표 제공 하는 hello 백업/복원 기능에 사용할 수 있습니다.

| 연결 상태 | Azure 구독 | 백업 tooAzure | 백업 toodisk | Azure에서 복구 | 디스크에서 복구 |
| --- | --- | --- | --- | --- | --- |
| 연결됨 |Active |허용됨 |허용됨 |허용됨 |허용됨 |
| 연결됨 |만료됨 |중지됨 |중지됨 |허용됨 |허용됨 |
| 연결됨 |프로비전 해제됨 |중지됨 |중지됨 |중지되고 Azure 복구 지점 삭제됨 |중지됨 |
| 손실된 연결 > 15일 |Active |중지됨 |중지됨 |허용됨 |허용됨 |
| 손실된 연결 > 15일 |만료됨 |중지됨 |중지됨 |허용됨 |허용됨 |
| 손실된 연결 > 15일 |프로비전 해제됨 |중지됨 |중지됨 |중지되고 Azure 복구 지점 삭제됨 |중지됨 |

### <a name="recovering-from-loss-of-connectivity"></a>연결 끊김 복구
방화벽 또는 프록시 액세스 tooAzure를 방해 하는 경우 도메인 주소 hello 방화벽/프록시 프로필에 따라 toowhitelist hello가 필요 합니다.

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

연결 tooAzure에 대 한 복원된 toohello Azure 백업 서버 컴퓨터를 수행한 후에 수행할 수 있는 hello 작업 hello Azure 구독 상태에 의해 결정 됩니다. 위의 hello 테이블 hello 컴퓨터 "연결"을 허용 하는 hello 작업에 대 한 세부 정보를 포함 합니다.

### <a name="handling-subscription-states"></a>구독 상태 처리
Azure 구독에서 가능한 tootake는는 *만료 됨* 또는 *Deprovisioned* 상태 toohello *활성* 상태입니다. 그러나이 일부 영향에 hello 제품 동작 hello 상태가 아닌 동안 *활성*:

* A *Deprovisioned* 구독 프로 비전이 해제 되는 기간에 hello에 대 한 기능을 손실 합니다. 선반에 *활성*, 백업/복원의 hello 제품 기능 다시 되 합니다. 또한 hello hello 로컬 디스크에 백업 데이터는 충분히 긴 보존 기간으로 유지 한 경우으로 검색할 수 있습니다. 그러나 Azure의 hello 백업 데이터는 hello hello 시작 되 면 영구적으로 손실 *Deprovisioned* 상태입니다.
* *만료됨* 구독은 다시 *활성* 상태로 되기 전까지 기능을 상실합니다. Hello 구독 하는 모든 백업은 hello 기간 중 예약 된 *만료 됨* 실행 되지 것입니다.

## <a name="troubleshooting"></a>문제 해결
Microsoft Azure 백업 서버 hello 설치 단계 (또는 백업 또는 복원) 하는 동안 오류와 함께 실패 하는 경우 참조 toothis [오류 코드 문서](https://support.microsoft.com/kb/3041338) 자세한 정보에 대 한 합니다.
너무 참조할 수도 있습니다[Azure 백업 관련 Faq](backup-azure-backup-faq.md)

## <a name="next-steps"></a>다음 단계
에 대 한 자세한 정보를 얻을 수 [DPM을 위한 환경 준비](https://technet.microsoft.com/library/hh758176.aspx) hello Microsoft TechNet 사이트에서. 또한 여기에는 Azure 백업 서버를 배포 및 사용하는 데 지원되는 구성에 대한 정보도 포함되어 있습니다.

이러한 문서 toogain Microsoft Azure 백업 서버를 사용 하는 작업 보호에 대 한 깊은 이해가 사용할 수 있습니다.

* [SQL Server 백업](backup-azure-backup-sql.md)
* [SharePoint 서버 백업](backup-azure-backup-sharepoint.md)
* [대체 서버 백업](backup-azure-alternate-dpm-server.md)
