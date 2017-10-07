---
title: "백업-오프 라인 백업 또는 초기 시드를 사용 하 여 aaaAzure hello Azure 가져오기/내보내기 서비스 | Microsoft Docs"
description: "Azure 백업을 사용 하 여 방법을 toosend hello Azure 가져오기/내보내기 서비스를 사용 하 여 hello 네트워크에서 데이터에 알아봅니다. 이 문서에서는 hello 오프 라인 시드 hello 초기 백업 데이터의 hello Azure 가져오기 내보내기 서비스를 사용 하 여 설명 합니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Azure 백업의 오프라인 백업 워크플로
Azure 백업에는 데이터 tooAzure의 초기 전체 백업 hello 하는 동안 네트워크 및 저장소 비용을 절감 하는 몇 가지 기본 제공 효율성을 이용 합니다. 초기 전체 백업에서 일반적으로 많은 양의 데이터를 전송 하 고 비교 했을 때 네트워크 대역폭이 더 많이 필요만 hello 델타/증분 전송 toosubsequent 백업 합니다. Azure 백업에는 hello 초기 백업을 압축합니다. 오프 라인 시드 hello 프로세스를 통해 Azure 백업 צ ְ ײ 디스크 초기 백업 데이터를 오프 라인 tooAzure tooupload hello 압축 합니다.  

hello Azure 백업의 오프 라인 시드 프로세스 긴밀 하 게 통합 된 hello [Azure 가져오기/내보내기 서비스](../storage/common/storage-import-export-service.md) 수 있도록 하 tootransfer 데이터 tooAzure 디스크를 사용 하 여 합니다. Toobe 높은 대기 시간 및 낮은 대역폭 네트워크를 통해 전송 해야 하는 초기 백업 데이터까지 (TBs)를 사용 하도록 설정한 경우에 하나 이상의 하드 드라이브 tooan Azure 데이터 센터에 hello 오프 라인 시드 워크플로 tooship hello 초기 백업 복사본을 사용할 수 있습니다. 이 문서는이 워크플로 완료 하는 hello 단계의 개요를 제공 합니다.

## <a name="overview"></a>개요
Azure 백업 및 Azure 가져오기/내보내기의 hello 시드 오프 라인 기능을 통해 디스크를 사용 하 여 간단한 tooupload hello 데이터 오프 라인 tooAzure 됩니다. Hello 네트워크를 통해 hello 초기 전체 복사본을 전송 하지 않고 hello 백업 데이터가 쓰여집니다 tooa *스테이징 위치*합니다. Hello 복사 toohello 준비 위치는 hello Azure 가져오기/내보내기 도구를 사용 하 여 완료 되 면 tooone 또는 자세한 SATA 드라이브, hello 양의 데이터에 따라이 데이터가 쓰여집니다. 이러한 드라이브는 Azure 데이터 센터에 가장 가까운 결국 배송된 toohello입니다.

hello [Azure 백업의 (이상) 2016 년 8 월 업데이트](http://go.microsoft.com/fwlink/?LinkID=229525) hello 포함 *Azure 디스크 준비 도구*, AzureOfflineBackupDiskPrep, 라는입니다:

* Hello Azure 가져오기/내보내기 도구를 사용 하 여 Azure 가져오기에 대 한 드라이브를 준비 하는 데 도움이 됩니다.
* Hello에 hello Azure 가져오기/내보내기 서비스에 대 한 Azure 가져오기 작업을 자동으로 만듭니다 [Azure 클래식 포털](https://manage.windowsazure.com) 것과 반대로 toocreating으로 hello 동일 수동으로 이전 버전의 Azure 백업 합니다.

Hello 백업 데이터 tooAzure의 hello 업로드를 완료 한 후 Azure 백업 hello 백업 데이터 toohello 백업 자격 증명 모음을 복사 하 고 hello 증분 백업이 예약 되어 있습니다.

> [!NOTE]
> toouse hello Azure 디스크 준비 도구 확인 Azure 백업의 (또는 이상), hello 2016 년 8 월 업데이트를 설치 하 고 함께 hello 워크플로의 모든 hello 단계를 수행 하십시오. 이전 버전의 Azure Backup을 사용 하는 경우에이 문서의 뒷부분에 나오는 섹션에 설명 된 대로 hello Azure 가져오기/내보내기 도구를 사용 하 여 hello SATA 드라이브를 준비할 수 있습니다.
>
>

## <a name="prerequisites"></a>필수 조건
* [Hello Azure 가져오기/내보내기 워크플로 숙지](../storage/common/storage-import-export-service.md)합니다.
* Hello 워크플로 시작 하기 전에 hello 다음을 확인 합니다.
  * Azure 백업 자격 증명 모음이 만들어졌습니다.
  * 자격 증명 모음 자격 증명이 다운로드되었습니다.
  * Windows Server/Windows 클라이언트 또는 System Center Data Protection Manager 서버에 설치 되어 hello Azure 백업 에이전트 및 hello 컴퓨터는 hello Azure 백업 자격 증명 모음에 등록 합니다.
* [Hello Azure 게시 파일 설정 다운로드](https://manage.windowsazure.com/publishsettings) hello 컴퓨터 데이터를 tooback을 계획입니다.
* 네트워크 공유 또는 hello 컴퓨터에서 추가 드라이브 될 수 있는 스테이징 위치를 준비 합니다. hello 스테이징 위치는 임시 저장소 되며이 워크플로 중 일시적으로 사용 됩니다. 준비 위치는 hello에 충분 한 디스크 공간 toohold 초기 복사본 확인 하십시오. 예를 들어 500 GB 파일 서버를 tooback을 시도 하는 경우 해당 hello 준비 영역을 500 GB 이상 확인 합니다. (더 due는 toocompression.)
* 지원되는 드라이브를 사용하고 있는지 확인합니다. 2.5 인치만 SSD, 또는 2.5 또는 3.5 인치 SATA II/III 내부 하드 드라이브는 가져오기/내보내기 서비스 hello로 사용 하기 위해 지원 됩니다. 하드 드라이브 too10 TB 사용할 수 있습니다. Hello 확인 [Azure 가져오기/내보내기 서비스 설명서](../storage/common/storage-import-export-service.md#hard-disk-drives) hello 최신 집합이 hello 서비스가 지 원하는 드라이브에 대 한 합니다.
* BitLocker 사용 hello 컴퓨터 toowhich hello SATA 드라이브 기록기가 연결 되어 있습니다.
* [Hello Azure 가져오기/내보내기 도구를 다운로드](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) toohello 컴퓨터 toowhich hello SATA 드라이브 기록기 연결 되어 있습니다. 다운로드 하 고 Azure 백업의 (또는 이상) hello 2016 년 8 월 업데이트를 설치한 경우에이 단계가 필요 하지 않습니다.

## <a name="workflow"></a>워크플로
이 섹션의 hello 정보 데이터 tooan Azure 데이터 센터를 배달할 수 있도록 hello 오프 라인 백업 워크플로 완료 하 고 tooAzure 저장소에 업로드 합니다. Hello 가져오기 서비스 또는 hello 프로세스의 모든 측면에 대 한 질문이 있으면 참조 hello [가져오기 서비스 개요](../storage/common/storage-import-export-service.md) 이전 참조 설명서입니다.

### <a name="initiate-offline-backup"></a>오프라인 백업 시작
1. 백업을 예약할 때 hello 화면 (Windows Server, Windows 클라이언트 또는 System Center Data Protection Manager)에 따라 표시 됩니다.

    ![가져오기 화면](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    System Center Data Protection Manager에서 해당 hello 화면 키를 같습니다. <br/>
    ![DPM 가져오기 화면](./media/backup-azure-backup-import-export/dpmoffline.png)

    hello 설명은 hello 입력은 다음과 같습니다.

    * **스테이징 위치**: hello 임시 저장소 위치 toowhich hello 초기 백업 복사본이 작성 됩니다. 네트워크 공유 또는 로컬 컴퓨터에 있을 수 있습니다. 원본 컴퓨터와 hello 복사 컴퓨터에 다른 경우에 스테이징 위치 hello의 hello 전체 네트워크 경로 지정 하는 것이 좋습니다.
    * **Azure 가져오기 작업 이름**: hello 고유 이름으로는 Azure 가져오기 서비스 및 Azure 백업 전송 된 데이터의 hello 전송에서 추적 디스크 tooAzure 합니다.
    * **Azure 게시 설정**: 구독 프로필에 대한 정보를 포함하는 XML 파일입니다. 또한 구독에 연결된 보안 자격 증명도 포함합니다. 있습니다 수 [hello 파일을 다운로드](https://manage.windowsazure.com/publishsettings)합니다. 제공 게시 설정 파일을 로컬 경로 toohello hello 합니다.
    * **Azure 구독 ID**: hello tooinitiate hello Azure 가져오기 작업을 계획 하는 hello 구독에 대 한 Azure 구독 ID입니다. 여러 Azure 구독이 있는 경우 hello 가져오기 작업과 tooassociate hello 구독의 hello ID를 사용 합니다.
    * **Azure 저장소 계정**: hello에 hello 클래식 유형 저장소 계정이 hello Azure 가져오기 작업과 관련 된 Azure 구독을 제공 합니다.
    * **Azure 저장소 컨테이너**: hello이이 작업의이 데이터를 가져올 Azure 저장소 계정에 hello 대상 저장소 blob의 hello 이름입니다.

    > [!NOTE]
    > Azure 복구 서비스 hello에서 자격 증명 모음에 서버 tooan 등록 한 경우 [Azure 포털](https://portal.azure.com) 백업과 있지 않습니다. 클라우드 솔루션 공급자 (CSP) 구독을 만들 수 있습니다 여전히 클래식 유형 저장소 계정을 hello에서 Azure 포털 하 고 hello 오프 라인 백업 워크플로 사용 합니다.
    >
    >

     Tooenter 필요 하기 때문에 이러한 모든 정보를 저장 단계에서 다시 합니다. Hello만 *스테이징 위치* 는 hello Azure 디스크 준비 도구 tooprepare hello 디스크를 사용 하는 경우 필요 합니다.    
2. Hello 워크플로 완료 한 후 선택 **지금 백업** hello Azure 백업 관리 콘솔 tooinitiate hello 오프 라인 백업 복사본에서 합니다. hello 초기 백업은이 단계의 일부로 toohello 준비 영역에 기록 됩니다.

    ![지금 백업](./media/backup-azure-backup-import-export/backupnow.png)

    toocomplete hello 해당 워크플로에서 System Center Data Protection Manager를 hello를 마우스 오른쪽 단추로 클릭 **보호 그룹**, 선택한 후 hello **복구 지점 만들기** 옵션입니다. Hello를 눌러 **온라인 보호** 옵션입니다.

    ![DPM 지금 백업](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Hello 작업이 완료 되 면 hello 스테이징 위치는 디스크 준비에 사용 되는 준비 toobe입니다.

    ![백업 진행](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>SATA 드라이브를 준비 하 고 hello Azure 디스크 준비 도구를 사용 하 여 Azure 가져오기 작업 만들기
hello Azure 디스크 준비 도구는 hello 복구 서비스 에이전트의 설치 디렉터리에서 사용할 수 있는 (2016 년 8 월 업데이트 이상)의 경로 따라 hello 합니다.

   *\Microsoft* *Azure* *Recovery* *Services* *Agent\Utils\*

1. Toohello 디렉터리 및 복사 hello 이동 **AzureOfflineBackupDiskPrep** 디렉터리 tooa 복사 컴퓨터 드라이브 toobe 준비는 hello에 탑재 됩니다. Hello 큰지에 toohello 복사 컴퓨터 사용 하 여 다음을 확인 합니다.

    * hello 복사 컴퓨터에 액세스할 수 hello 동일 네트워크 hello에 제공 된 경로 사용 하 여 오프 라인 시드 워크플로 hello에 대 한 위치를 준비 하는 hello **오프 라인 백업을 시작할** 워크플로 합니다.
    * Hello 컴퓨터에서 BitLocker는 사용 하 고 있습니다.
    * hello 컴퓨터 hello Azure 포털에 액세스할 수 있습니다.

    필요한 경우 hello 복사 컴퓨터 수 수 hello hello 원본 컴퓨터와 동일 합니다.
2. Hello 현재 디렉터리와 hello Azure 디스크 준비 도구 디렉터리와 hello 복사 컴퓨터에서 관리자 권한 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다.

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | 매개 변수 | 설명 |
    | --- | --- |
    | s:&lt;*스테이징 위치 경로*&gt; |가 tooprovide hello 경로 toohello 스테이징 hello에 입력 된 위치를 사용 하는 필수 입력 **오프 라인 백업을 시작할** 워크플로 합니다. |
    | p:&lt;*경로 tooPublishSettingsFile*&gt; |Tooprovide hello 경로 toohello가 사용 하는 선택적 입력 **Azure 게시 설정** hello에 입력 한 파일 **오프 라인 백업을 시작할** 워크플로 합니다. |

    > [!NOTE]
    > hello &lt;경로 tooPublishSettingFile&gt; hello 복사 컴퓨터 및 원본 컴퓨터는 서로 다른 값은 필수입니다.
    >
    >

    Hello 명령을 실행 하면 hello 도구 toohello 드라이브 toobe 준비를 해야 하는 해당 하는 hello Azure 가져오기 작업의 hello 선택을 요청 합니다. 준비 위치를 제공 하는 hello로 단일 가져오기 작업이 연결 된만 순서에 hello와 같은 화면이 표시 합니다.

    ![Azure 디스크 준비 도구 입력](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Hello에 대 한 전송 tooAzure tooprepare 되도록 hello 탑재 된 디스크에 대 한 콜론 뒤에 없이 hello 드라이브 문자를 입력 합니다. 메시지가 표시 되 면 hello 드라이브의 서식을 hello에 대 한 확인을 제공 합니다.

    hello 도구에는 다음 tooprepare hello 디스크 hello 백업 데이터를 시작합니다. 대화 상자가 나타나면 hello 도구로 hello hello 백업 데이터에 대 한 충분 한 공간이 디스크를 제공 하는 경우 추가 디스크 tooattach 할 수 있습니다. <br/>

    Hello hello 도구의 성공적인 실행의 끝에 하나 이상의 디스크 사용자가 제공한 전달 tooAzure에 대 한 준비 됩니다. 또한 hello 이름 사용 하는 가져오기 작업 중에 제공한 hello **오프 라인 백업을 시작할** hello Azure 클래식 포털에서 워크플로 만듭니다. 마지막으로, hello 도구 hello 디스크 toobe 배송 해야 하는 Azure 데이터 센터에 배송 주소 toohello hello 및 표시 hello hello Azure 클래식 포털에서 링크 toolocate hello 가져오기 작업 합니다.

    ![Azure 디스크 준비 완료](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. 배송 hello 디스크 toohello 제공 하는 hello 도구를 해결 하 고 나중에 참조할 수를 추적 하는 hello를 보관 합니다.<br/>

5. 링크 표시 하는 hello 도구, hello에 지정 된 hello Azure 저장소 계정을 참조 toohello 이동할 때 **오프 라인 백업을 시작할** 워크플로 합니다. Hello에 새로 만든 hello 가져오기 작업을 볼 수는 여기 **가져오기/내보내기** hello 저장소 계정 탭 합니다.

    ![생성된 가져오기 작업](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. 클릭 **발송 정보** hello 페이지 tooupdate hello 맨 아래에 연락처 세부 정보 화면을 수행 하는 hello와 같이 합니다. Microsoft는이 정보 tooship hello 가져오기 작업 후에 디스크 백 tooyou 완료 된를 사용 합니다.

    ![연락처 정보](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Hello hello 다음 화면에서 전달 되는 정보를 입력 합니다. Hello 제공 **배달 운송 업체** 및 **추적 번호** toohello 디스크 toohello Azure 데이터 센터를 제공 하면 해당 하는 세부 정보입니다.

    ![배송 정보](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>전체 hello 워크플로
Hello 가져오기 작업이 완료 되 면 초기 백업 데이터는 저장소 계정에서 사용할 수 있습니다. 복구 서비스 에이전트 hello 다음 복사본 hello 내용의 hello 또는 데이터를이 계정 toohello 백업 자격 증명 모음의 복구 서비스 자격 증명 모음, 해당 되는 합니다. Hello 다음 예약 된 백업 시간 hello Azure 백업 에이전트 hello 초기 백업 복사본을 통해 증분 백업 hello를 수행합니다.

> [!NOTE]
> hello 다음 섹션에서는 적용 toousers 액세스 toohello Azure 디스크 준비 도구를 갖고 있지 않은 이전 버전의 Azure 백업 합니다.
>
>

### <a name="prepare-a-sata-drive"></a>SATA 드라이브 준비
1. Hello 다운로드 [Microsoft Azure 가져오기/내보내기 도구](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) toohello 복사 컴퓨터입니다. 준비 위치는 hello toorun hello 다음 명령 집합을 계획 하는 hello 컴퓨터에서 액세스할 수 있는 확인 하십시오. 필요한 경우 hello 복사 컴퓨터 수 수 hello hello 원본 컴퓨터와 동일 합니다.

2. Hello WAImportExport.zip 파일을 압축을 풉니다. Hello SATA 드라이브를 포맷 하 고 hello toohello SATA 드라이브를 백업 데이터를 기록 하 여 암호화 하는 hello WAImportExport 도구를 실행 합니다. Hello 다음 명령을 실행 하기 전에 hello 컴퓨터에서 BitLocker가 설정 되었는지 확인 합니다. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Azure 백업의 (또는 이상) hello 2016 년 8 월 업데이트를 설치한 경우 해당 hello 스테이징 위치 입력 한 hello에 하나씩 hello와 동일 hello은 확인 **지금 백업** 화면 및 AIB 및 기본 Blob 파일을 포함 합니다.
    >
    >

| 매개 변수 | 설명 |
| --- | --- |
| /j:<*JournalFile*> |hello toohello 저널 파일 경로입니다. 각 드라이브에는 정확히 하나의 저널 파일이 있어야 합니다. hello 대상 드라이브에 hello 저널 파일 수 없습니다. hello 저널 파일 확장명.jrn 이며이 명령을 실행 하는 과정으로 생성 됩니다. |
| /id:<*SessionId*> |hello 세션 ID는 복사 세션을 식별합니다. 중단된 된 복사 세션의 정확한 복구를 사용 하는 tooensure 것합니다. 복사 세션에서 복사 된 파일을 hello 세션 ID hello 대상 드라이브에 따라 명명 된 디렉터리에 저장 됩니다. |
| /sk:<*StorageAccountKey*> |hello 저장소 계정 toowhich hello 데이터에 대 한 hello 계정 키를 가져옵니다. hello 핵심 요구 toobe hello 백업 정책/보호 그룹을 만들 때 입력 했던 것과 동일 합니다. |
| /BlobType |blob의 hello 형식입니다. 이 워크플로는 **PageBlob** 이 지정된 경우에만 성공합니다. 하지 hello 기본 옵션 이므로이 명령에서 언급 해야 합니다. |
| /t:<*TargetDriveLetter*> |hello hello 현재 복사 세션에 대 한 hello 대상 하드 드라이브의 콜론을 후행 hello 없이 드라이브 문자입니다. |
| /format |hello 옵션 tooformat hello 드라이브입니다. Hello 드라이브 포맷; toobe 해야 하는 경우이 매개 변수를 지정 합니다. 그렇지 않으면 생략 합니다. Hello 드라이브를 포맷 하는 hello 도구, 전에 hello 콘솔에서 확인 메시지가 나타납니다. toosuppress hello 확인을 hello 않으려면 /silentmode 매개 변수를 지정 합니다. |
| /encrypt |hello 옵션 tooencrypt hello 드라이브입니다. Hello 드라이브 아직 BitLocker 및 요구 사항 toobe hello 도구를 통해 암호화 된 암호화 되지 않은 경우이 매개 변수를 지정 합니다. Hello 드라이브가 이미 BitLocker로 암호화 된,이 매개 변수 생략 hello /bk 매개 변수를 지정 및 hello 기존 BitLocker 키를 제공 합니다. Hello /format 매개 변수를 지정 하는 경우 hello를 지정 해야/매개 변수를 암호화 해야 합니다. |
| /srcdir:<*SourceDirectory*> |파일 toobe 있는 hello 소스 디렉터리 toohello 대상 드라이브를 복사 합니다. 해당 hello 지정 된 디렉터리 이름에 상대 아닌 전체 경로 확인 하십시오. |
| /dstdir:<*DestinationBlobVirtualDirectory*> |hello 경로 toohello 대상 가상 디렉터리에 Azure 저장소 계정입니다. Hello 대상 가상 디렉터리 또는 blob을 지정할 때 있는지 toouse 유효한 컨테이너 이름을 여야 합니다. 컨테이너 이름은 소문자여야 합니다.  이 컨테이너 이름은 hello 백업 정책/보호 그룹을 작성 하는 동안 입력 한 것 이어야 합니다. |

> [!NOTE]
> 저널 파일 hello 워크플로의 hello 전체 정보를 캡처하는 hello WAImportExport 폴더에 만들어집니다. Hello Azure 포털에서에서 가져오기 작업을 만들 때이 파일이 필요 합니다.
>
>

  ![PowerShell 출력](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Hello Azure 포털의에서 가져오기 작업 만들기
1. Hello tooyour 저장소 계정의 이동 [Azure 클래식 포털](https://manage.windowsazure.com/), 클릭 **가져오기/내보내기**, 차례로 **가져오기 작업 만들기** hello 작업창에 합니다.

    ![Hello Azure 포털의에서 가져오기/내보내기 탭](./media/backup-azure-backup-import-export/azureportal.png)

2. Hello 마법사의 1 단계에서 드라이브를 준비한 및 hello 드라이브 저널 파일을 사용할 수 있는지를 나타냅니다.

3. Hello 마법사의 2 단계에서이 가져오기 작업에 대 한 책임이 hello 사람에 대 한 연락처 정보를 제공 합니다.

4. 3 단계에서 hello 이전 섹션에서 가져온 hello 드라이브 저널 파일을 업로드 합니다.

5. 4 단계에서 설명 하는 백업 정책/보호 그룹을 만들 때 입력 hello 가져오기 작업에 대 한 이름을 입력 합니다. 소문자, 숫자, 하이픈, 입력 하는 hello 이름을 포함할 수 있으며 밑줄 문자로 시작 해야 하며 공백을 포함할 수 없습니다. 완료 되 고 진행 중인 동안 사용 되는 tootrack 작업은 선택 하는 hello 이름입니다.

6. 다음을 hello 목록에서 데이터 센터 지역을 선택 합니다. hello 데이터 센터 지역을 나타냅니다 hello 데이터 센터 및 주소 toowhich 서 패키지 배송 해야 합니다.

    ![데이터 센터 지역 선택](./media/backup-azure-backup-import-export/dc.png)

7. 5 단계에서 hello 목록에서 반송 운송 업체를 선택 하 고 운송 업체 계정 번호를 입력 합니다. Microsoft에이 계정을 사용 하 여 tooship 드라이브 tooyou 다시 가져오기 작업이 완료 되 면 합니다.

8. Hello 디스크를 배송 하 고 hello 배송의 숫자 tootrack hello 상태를 추적 하는 hello를 입력 합니다. hello 디스크 hello 데이터 센터에 도착 하면 toohello 저장소 계정에 복사 하 고 hello 상태가 업데이트 됩니다.

    ![완료 상태](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>전체 hello 워크플로
Hello 초기 백업 데이터를 사용할 저장소 계정의 hello이 계정 toohello 백업 자격 증명 모음 또는 복구 서비스 자격 증명 모음에서 hello 데이터의 hello 내용을 복사 하는 Microsoft Azure 복구 서비스 에이전트를 해당 되는 합니다. Hello 다음 일정에 백업 시간, Azure 백업 에이전트 hello hello 초기 백업 복사본을 통해 hello 증분 백업을 수행합니다.

## <a name="next-steps"></a>다음 단계
* 궁금한 hello Azure 가져오기/내보내기 워크플로에 대 한 참조 너무[hello Microsoft Azure 가져오기/내보내기 서비스 tootransfer 데이터 tooBlob 저장소를 사용 하 여](../storage/common/storage-import-export-service.md)합니다.
* Toohello 오프 라인 백업의 섹션을 참조 hello Azure 백업 [FAQ](backup-azure-backup-faq.md) hello 워크플로에 대 한 질문에 대 한 합니다.
