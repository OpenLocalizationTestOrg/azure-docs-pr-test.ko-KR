---
title: "Azure tooa Windows Server 또는 Windows 컴퓨터의 데이터를 aaaRestore | Microsoft Docs"
description: "Toorestore 데이터 Azure tooa Windows Server 또는 Windows 컴퓨터에 저장 하는 방법에 대해 알아봅니다."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>파일 tooa Windows server 또는 리소스 관리자 배포 모델을 사용 하 여 Windows 클라이언트 컴퓨터를 복원 합니다.
> [!div class="op_single_selector"]
> * [Azure 포털](backup-azure-restore-windows-server.md)
> * [클래식 포털](backup-azure-restore-windows-server-classic.md)
>
>

이 문서에서는 설명 어떻게 toorestore 데이터를 백업 자격 증명 모음입니다. hello Microsoft Azure 복구 서비스 (MARS) 에이전트에서 hello 데이터 복구 마법사를 사용 하면 toorestore 데이터입니다. 데이터를 복원하면 다음이 가능해집니다.

* 동일 컴퓨터에서 hello 백업을 복원 데이터 toohello 수행 되었습니다.
* 데이터 tooan 대체 컴퓨터를 복원 합니다.

2017 년 1 월 Microsoft는 미리 보기 업데이트 toohello MARS 에이전트를 릴리스 했습니다. 버그 수정 프로그램과 함께이 업데이트를 통해 toomount 수 있는 인스턴트 복원 쓰기 가능한 복구 지점 스냅숏을 복구 볼륨으로 합니다. 그런 다음 hello 복구 볼륨 및 복사 파일 tooa 로컬 컴퓨터 파일을 복원 함으로써 선택적으로 탐색할 수 있습니다.

> [!NOTE]
> hello [2017 년 1 월 Azure Backup 업데이트](https://support.microsoft.com/en-us/help/3216528?preview) 는 toouse toorestore 데이터 인스턴트 복원 하려는 경우에 필요 합니다. 또한 로캘에서 hello 지원 문서에 나열 된 자격 증명 모음에 hello 백업 데이터를 보호 합니다. Hello 참조 [2017 년 1 월 Azure Backup 업데이트](https://support.microsoft.com/en-us/help/3216528?preview) hello 최신 목록은 로캘 지 원하는 즉시 복원 합니다. 즉시 복원은 현재 **일부** 로캘에서만 사용할 수 있습니다.
>

클래식 포털 hello 인스턴트 복원 hello Azure 포털에서에서 복구 서비스 자격 증명 모음에서 사용 하 고 백업 자격 증명 모음은 제공 됩니다. Toouse 인스턴트 복원 하려는 경우 hello MARS 업데이트를 다운로드 하 고 인스턴트 복원 언급 하는 hello 절차를 따르십시오.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>Toorecover 데이터 toohello 인스턴트 Restore를 사용 하 여 동일한 컴퓨터

파일 및 희망 toorestore 실수로 삭제 한 경우이 단계를 같은 컴퓨터 (어떤 hello에서 백업을 수행할 때) 다음 hello toohello hello 데이터를 복구 하는 데 도움이 됩니다.

1. 열기 hello **Microsoft Azure 백업** 에 snap 합니다. Hello 컴퓨터 또는 서버 hello 스냅인에 설치 된 알 수 없는 경우 검색 **Microsoft Azure 백업**합니다.

    hello를 데스크톱 응용 프로그램 hello 검색 결과에 표시 됩니다.

2. 클릭 **데이터 복구** toostart hello 마법사.

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

3. Hello에 **시작** 창, toorestore hello 데이터 toohello 동일한 서버 또는 컴퓨터 선택 **이 서버 (`<server name>`)** 클릭 **다음**합니다.

    ![이 서버 옵션 toorestore hello 데이터 toohello 선택 동일한 컴퓨터](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. Hello에 **복구 모드 선택** 창 선택 **개별 파일과 폴더** 클릭 하 고 **다음**합니다.

    ![파일 찾아보기](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. Hello에 **볼륨 및 날짜 선택** 창, hello 파일 및/또는 toorestore 폴더를 포함 하는 select hello 볼륨입니다.

    Hello 달력에서 복구 지점을 선택 합니다. 어떤 복구 시점에서라도 복원할 수 있습니다. 날짜 **굵게** 복구 지점이 하나 이상 hello 가용성을 나타냅니다. 여러 복구 지점을 사용할 수 있는 경우 날짜를 선택 하면 hello에서 hello 특정 복구 지점 선택 **시간** 드롭 다운 메뉴.

    ![볼륨 및 날짜](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. 복구 지점 toorestore hello를 선택 하면 클릭 **탑재**합니다.

    Azure 백업 탑재 hello 로컬 복구 지점으로 사용 하 여 복구 볼륨입니다.

7. Hello에 **찾아보기 및 파일 복구** 창에서 클릭 **찾아보기** 원하는 tooopen Windows 탐색기 및 찾기 hello 파일 및 폴더.

    ![복구 옵션](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. Windows 탐색기, hello 파일 복사 및/또는 폴더에서 toorestore 원하고 tooany 위치 toohello 로컬 서버 또는 컴퓨터에 붙여 넣습니다. 있습니다 수 또는 hello 복구 볼륨에서 직접 hello 파일 스트림 열고 hello 올바른 버전은 복구를 확인 합니다.

    ![복사 및 붙여넣기 toolocal 위치 탑재 된 볼륨에서에서 파일 및 폴더](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. 끝나면 hello 파일 및/또는 폴더 hello에 복원 중인 **찾아보기 및 복구 파일** 창에서 클릭 **탑재 해제**합니다. 클릭 **예** tooconfirm toounmount hello 볼륨 되도록 합니다.

    ![Hello 볼륨을 분리 하 고 확인](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > 탑재 해제를 클릭 하지 않으면 경우 탑재 된 경우 hello 시간에서 6 시간 동안 hello 복구 볼륨 탑재 된 상태로 유지 됩니다. 그러나 hello 탑재 시간은 확장된 키는 최대 진행 중인 파일 복사의 경우 24 시간입니다. Hello 볼륨이 탑재 하는 동안 백업 작업이 실행 됩니다. Hello 볼륨 탑재 되는 경우 hello 시간 동안 모든 예약 된 백업 작업 toorun hello 복구 볼륨 탑재 된 후 실행 됩니다.
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>인스턴트 복원 toorestore 데이터 tooan 대체 컴퓨터 사용
전체 서버를 잃어버린 경우 Azure 백업 tooa 서로 다른 컴퓨터에서 데이터를 복구할 수 있습니다. 단계를 수행 하는 hello hello 워크플로를 보여 줍니다.


다음이 단계에 사용 된 hello 용어에는 다음이 포함 됩니다.

* *원본 컴퓨터* – hello 원래 컴퓨터 hello 백업에서 백업 하 고 있는 현재 사용할 수 없는 합니다.
* *대상 컴퓨터* – hello 컴퓨터 toowhich hello 데이터 복구 되 고 있습니다.
* *샘플 자격 증명 모음* – hello 복구 서비스 자격 증명 모음 toowhich hello *원본 컴퓨터* 및 *대상 컴퓨터* 등록 됩니다. <br/>

> [!NOTE]
> 백업을 이전 버전의 hello 운영 체제를 실행 하는 복원 된 tooa 대상 컴퓨터 일 수 없습니다. 예를 들어, Windows 7 컴퓨터에서 가져온 백업은 Windows 8 이상의 컴퓨터에서 복원할 수 있습니다. Windows 8 컴퓨터에서 수행한 백업 복원된 tooa Windows 7 컴퓨터 일 수 없습니다.
>
>

1. 열기 hello **Microsoft Azure 백업** hello에 snap *대상 컴퓨터*합니다.

2. Hello 확인 *대상 컴퓨터* 및 hello *원본 컴퓨터* 동일한 복구 서비스 자격 증명 모음에 등록 된 toohello 됩니다.

3. 클릭 **데이터 복구** tooopen hello **데이터 복구 마법사**합니다.

    ![데이터 복구](./media/backup-azure-restore-windows-server/recover.png)

4. Hello에 **시작** 창 선택 **다른 서버**

    ![다른 서버](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. Hello toohello 해당 하는 자격 증명 모음 자격 증명 파일을 제공 *샘플 자격 증명 모음*를 클릭 하 고 **다음**합니다.

    Hello 자격 증명 모음 자격 증명 파일을 잘못 된 (또는 만료 된) 경우 hello에서 새 자격 증명 모음 자격 증명 파일을 다운로드 *샘플 자격 증명 모음* hello Azure 포털의에서. 올바른 자격 증명 모음 자격 증명을 제공한 경우 백업 자격 증명 모음에 해당 하는 hello hello 이름이 표시 됩니다.


6. Hello에 **백업 서버 선택** 창, 선택 hello *원본 컴퓨터* hello 목록이 표시 된 컴퓨터에서 및 hello 암호를 제공 합니다. 그런 후 **Next**를 클릭합니다.

    ![컴퓨터 목록](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. Hello에 **복구 모드 선택** 창, 선택 **개별 파일과 폴더** 클릭 **다음**합니다.

    ![검색](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. Hello에 **볼륨 및 날짜 선택** 창, hello 파일 및/또는 toorestore 폴더를 포함 하는 select hello 볼륨입니다.

    Hello 달력에서 복구 지점을 선택 합니다. 어떤 복구 시점에서라도 복원할 수 있습니다. 날짜 **굵게** 복구 지점이 하나 이상 hello 가용성을 나타냅니다. 여러 복구 지점을 사용할 수 있는 경우 날짜를 선택 하면 hello에서 hello 특정 복구 지점 선택 **시간** 드롭 다운 메뉴.

    ![검색 항목](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. 클릭 **탑재** toolocally 탑재 hello 복구 지점에서 복구 볼륨으로 프로그램 *대상 컴퓨터*합니다.

10. Hello에 **찾아보기 및 파일 복구** 창에서 클릭 **찾아보기** 원하는 tooopen Windows 탐색기 및 찾기 hello 파일 및 폴더.

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. Windows 탐색기에서 hello 복구 볼륨에서 hello 파일 및/또는 폴더를 복사 하 고 tooyour 붙여넣을 *대상 컴퓨터* 위치 합니다. 있습니다 수 또는 hello 복구 볼륨에서 직접 hello 파일 스트림 열고 hello 올바른 버전은 복구를 확인 합니다.

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. 끝나면 hello 파일 및/또는 폴더 hello에 복원 중인 **찾아보기 및 복구 파일** 창에서 클릭 **탑재 해제**합니다. 클릭 **예** tooconfirm toounmount hello 볼륨 되도록 합니다.

    ![암호화](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > 탑재 해제를 클릭 하지 않으면 경우 탑재 된 경우 hello 시간에서 6 시간 동안 hello 복구 볼륨 탑재 된 상태로 유지 됩니다. 그러나 hello 탑재 시간은 확장된 키는 최대 진행 중인 파일 복사의 경우 24 시간입니다. Hello 볼륨이 탑재 하는 동안 백업 작업이 실행 됩니다. Hello 볼륨 탑재 되는 경우 hello 시간 동안 모든 예약 된 백업 작업 toorun hello 복구 볼륨 탑재 된 후 실행 됩니다.
    >

## <a name="troubleshooting"></a>문제 해결
Azure 백업 hello 복구 볼륨 클릭 몇 분 정도 후에 성공적으로 탑재 되지 않는 경우 **탑재** 하거나 하나 이상의 오류가 발생 한 실패 toomount hello 복구 볼륨 일반적으로 복구 toobegin 아래 hello 단계를 수행 합니다.

1.  몇 분 동안 실행 된 경우 hello 진행 중인 탑재 프로세스를 취소 합니다.

2.  Hello hello Azure 백업 에이전트의 최신 버전에 있는지 확인 하십시오. Azure 백업 에이전트의 버전 정보 hello toofind 클릭 **Microsoft Azure 복구 서비스 에이전트에 대 한** hello에 **동작** 창의 Microsoft Azure 백업 콘솔 하 고 해당 hello 확인 **버전** 번호는 같은 tooor에 언급 된 hello 버전 보다 높은 [이 여기서](https://go.microsoft.com/fwlink/?linkid=229525)합니다. Hello에서 최신 버전을 다운로드할 수 있습니다 [여기](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  너무 이동**장치 관리자** -> **저장소 컨트롤러** 찾을 수 있는지 확인 하 고 **Microsoft iSCSI 초기자**합니다. 찾을 수 있는 경우 아래의 7 toostep 직접 이동 합니다. 

4.  3 단계에서 설명한 것 처럼 Microsoft iSCSI 초기자 서비스를 찾을 수 없는 경우에 항목을 찾을 수 없다면 toosee 확인 **장치 관리자** -> **저장소 컨트롤러** 호출  **알 수 없는 장치** 하드웨어 ID와 **ROOT\ISCSIPRT**합니다.

5.  **알 수 없는 장치**를 마우스 오른쪽 단추로 클릭하고 **업데이트 드라이버 소프트웨어**를 선택합니다.

6.  너무 hello 옵션을 선택 하 여 hello 드라이버 업데이트 **업데이트 된 드라이버 소프트웨어 자동으로 검색**합니다. Hello 업데이트 완료 변경할지 **알 수 없는 장치** 너무**Microsoft iSCSI 초기자** 다음과 같이 합니다. 

    ![암호화](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  너무 이동**작업 관리자** -> **서비스 (로컬)** -> **Microsoft iSCSI 초기자 서비스**합니다. 

    ![암호화](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  Hello 서비스를 클릭 하면 마우스 오른쪽 단추로 클릭 하 여 hello Microsoft iSCSI 초기자 서비스를 다시 시작 **중지** 마우스 오른쪽 단추로 다시 클릭 하 고 클릭 하면 추가 **시작**합니다.

9.  인스턴트 복원을 사용하여 복구를 다시 시도하세요. 

Hello 복구 계속 실패 하면 서버/클라이언트를 다시 부팅 합니다. 다시 부팅은 바람직하지 않습니다. hello 복구 hello 서버를 다시 부팅 한 후에 계속 실패 하면, 다른 시스템에서 복구를 시도 하 고 너무 이동 하 여 Azure 지원에 문의[Azure 포털](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 및 지원 요청을 제출 합니다.

## <a name="next-steps"></a>다음 단계
* 파일과 폴더를 복구했으므로 [백업을 관리](backup-azure-manage-windows-server.md)할 수 있습니다.
