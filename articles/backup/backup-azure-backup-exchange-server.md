---
title: "Exchange server tooAzure System Center 2012 R2 DPM을 사용 하 여 백업을 aaaBack | Microsoft Docs"
description: "자세한 내용은 System Center 2012 R2 DPM을 사용 하 여 Exchange server tooAzure tooback을 백업 하는 방법"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a>Exchange server tooAzure System Center 2012 R2 DPM을 사용 하 여 백업 백업
이 문서에서는 설명 방법을 Microsoft Exchange 서버를 System Center 2012 R2 Data Protection Manager (DPM) 서버 tooback tooconfigure 너무 Azure 백업 합니다.  

## <a name="updates"></a>업데이트
toosuccessfully 레지스터 hello DPM 서버 Azure 백업을 사용 하 여 hello hello Azure 백업 에이전트의 최신 버전을 System Center 2012 R2 DPM 및 hello에 대 한 최신 업데이트 롤업을 설치 해야 합니다. Hello에서 hello 최신 업데이트 롤업을 가져올 [Microsoft 카탈로그](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager)합니다.

> [!NOTE]
> 이 문서의 예제 hello에 대 한 2.0.8719.0 hello Azure 백업 에이전트의 버전을 설치 하면 및 업데이트 롤업 6 ´ â System Center 2012 R2 DPM 합니다.
>
>

## <a name="prerequisites"></a>필수 조건
계속 하기 전에 hello 모두 있는지 확인 [필수 구성 요소](backup-azure-dpm-introduction.md#prerequisites) Microsoft Azure 백업을 사용 하기 위한 tooprotect 작업 충족 합니다. 이러한 필수 구성이 요소는 hello 다음과를 같습니다.

* Hello Azure 사이트에서 백업 자격 증명 모음이 생성 되었습니다.
* 에이전트 및 자격 증명 모음 자격 증명을 다운로드 한 toohello DPM 서버 되었습니다.
* hello 에이전트 hello DPM 서버에 설치 됩니다.
* hello 자격 증명 모음 자격 증명이 사용 되는 tooregister hello DPM 서버.
* Exchange 2016을 보호 하는 경우 2012 R2 UR9 tooDPM를 업그레이드 하십시오 이상 버전

## <a name="dpm-protection-agent"></a>DPM 보호 에이전트
tooinstall hello DPM 보호 에이전트 hello Exchange 서버에서 다음이 단계를 따르십시오.

1. Hello 방화벽이 제대로 구성 되어 있는지 확인 합니다. 참조 [hello 에이전트에 대 한 방화벽 예외 구성](https://technet.microsoft.com/library/Hh758204.aspx)합니다.
2. 클릭 하 여 hello 에이전트 hello Exchange 서버에 설치 **관리 > 에이전트 > 설치** DPM 관리자 콘솔에서 합니다. 참조 [hello DPM 보호 에이전트 설치](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) 자세한 단계입니다.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Hello Exchange 서버에 대 한 보호 그룹 만들기
1. Hello DPM 관리자 콘솔에서에서 클릭 **보호**, 클릭 하 고 **새로** hello 도구 리본 tooopen hello에 **새 보호 그룹 만들기** 마법사.
2. Hello에 **시작** hello 마법사 클릭의 화면 **다음**합니다.
3. Hello에 **보호 그룹 종류 선택** 화면에서 선택 **서버** 클릭 **다음**합니다.
4. 선택 hello Exchange 서버 데이터베이스 tooprotect 원하고 클릭 **다음**합니다.

   > [!NOTE]
   > Exchange 2013을 보호 하는 경우 확인 hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx)합니다.
   >
   >

    다음 예제는 hello, hello Exchange 2010 데이터베이스 선택 되어 있습니다.

    ![그룹 구성원 선택](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Hello 데이터 보호 방법을 선택 합니다.

    Hello 보호 그룹 이름을 지정 하 고 hello 다음 옵션을 모두 선택 합니다.

   * 디스크를 사용하여 단기 보호를 하려고 합니다.
   * 온라인 보호를 사용하려고 합니다.
6. **다음**을 누릅니다.
7. 선택 hello **eseutil 실행 하 여 toocheck 데이터 무결성** hello Exchange Server 데이터베이스의 toocheck hello 무결성을 원하는 경우 옵션입니다.

    이 옵션을 선택한 후 백업 일관성 검사에서 실행 될 hello DPM 서버 tooavoid hello I/O 트래픽을 hello를 실행 하 여 생성 되는 **eseutil** hello Exchange 서버에서 명령을 합니다.

   > [!NOTE]
   > toouse이 옵션을 hello Ese.dll 및 Eseutil.exe 파일 toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin 디렉터리 hello DPM 서버에 복사 해야 합니다. 그렇지 않으면 다음 오류가 hello 트리거될 수 있습니다.  
   > ![eseutil 오류](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. **다음**을 누릅니다.
9. 에 대 한 데이터베이스 선택 hello **복사 백업**, 클릭 하 고 **다음**합니다.

   > [!NOTE]
   > 데이터베이스의 DAG 복사본 하나 이상에 대한 "전체 백업"을 선택하지 않으면 로그는 잘리지 않습니다.
   >
   >
10. 구성에 대 한 hello 목표 **단기 백업**, 클릭 하 고 **다음**합니다.
11. Hello 사용 가능한 디스크 공간을 검토 한 다음 클릭 **다음**합니다.
12. 서버는 hello DPM에서 만들고 hello 초기 복제를 클릭 한 다음 hello 시간 선택 **다음**합니다.
13. Hello 일관성 확인 옵션을 선택한 다음 클릭 **다음**합니다.
14. Hello 데이터베이스 tooback tooAzure을 선택 하 고 클릭 선택 **다음**합니다. 예:

    ![온라인 보호 데이터 지정](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. 에 대 한 hello 일정 정의 **Azure 백업**, 클릭 하 고 **다음**합니다. 예:

    ![온라인 백업 일정 지정](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > 온라인 복구 지점은 Express 전체 복구 지점을 기반으로 합니다. Hello 온라인 복구 지점 예약 해야 따라서 hello에 대 한 지정 된 hello 시간 후 전체 복구 지점 express입니다.
    >
    >
16. Hello 보존 정책에 대 한 구성 **Azure 백업**, 클릭 하 고 **다음**합니다.
17. 온라인 복제 옵션을 선택하고 **다음**을 클릭합니다.

    큰 데이터베이스를 설정한 경우 hello 초기 백업 toobe hello 네트워크를 통해 만든 시간이 많이 걸리는 합니다. tooavoid이이 문제를 오프 라인 백업을 만들 수 있습니다.  

    ![온라인 보존 정책 지정](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Hello 설정을 확인 한 다음 클릭 **그룹 만들기**합니다.
19. **닫기**를 클릭합니다.

## <a name="recover-hello-exchange-database"></a>Hello Exchange 데이터베이스 복구
1. Exchange 데이터베이스 toorecover 클릭 **복구** hello DPM 관리자 콘솔에에서 있습니다.
2. 원하는 toorecover hello Exchange 데이터베이스를 찾습니다.
3. Hello에서 온라인 복구 지점을 선택 *복구 시간* 드롭 다운 목록입니다.
4. 클릭 **복구** toostart hello **복구 마법사**합니다.

온라인 복구 지점의 경우 다섯 가지 형식의 복구가 있습니다.

* **복구할 Exchange Server 위치 toooriginal:** hello 데이터가 복구 된 toohello 원래 Exchange 서버 됩니다.
* **Exchange 서버의 tooanother 데이터베이스 복구:** hello 데이터가 다른 Exchange 서버에서 복구 된 tooanother 데이터베이스 됩니다.
* **Tooa 복구 데이터베이스 복구:** hello 데이터가 복구 된 tooan Exchange 복구 데이터베이스 (RDB) 됩니다.
* **Tooa 네트워크 폴더에 복사:** hello 데이터가 복구 된 tooa 네트워크 폴더 됩니다.
* **Tootape 복사:** 경우 테이프 라이브러리 또는 독립 실행형 테이프 드라이브에 구성 되어 연결 된 hello DPM 서버에서 복구 지점 hello 됩니다 tooa 사용 가능한 테이프를 복사 합니다.

    ![온라인 복제 선택](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>다음 단계
* [Azure 백업 - FAQ](backup-azure-backup-faq.md)
