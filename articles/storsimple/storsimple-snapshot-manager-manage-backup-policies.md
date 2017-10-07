---
title: "aaaStorSimple 스냅숏 관리자에 대 한 백업 정책 | Microsoft Docs"
description: "Toouse StorSimple 스냅숏 관리자 MMC 스냅인 toocreate hello 하 및 예약 된 백업 제어 하는 hello 백업 정책을 관리 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>StorSimple 스냅숏 관리자 toocreate를 사용 하 고 백업 정책 관리
## <a name="overview"></a>개요
백업 정책을 로컬로 또는 hello 클라우드에 볼륨 데이터를 백업 하기 위한 일정을 만듭니다. 백업 정책을 만들 때 보존 정책을 지정할 수도 있습니다. (최대 64개의 스냅숏을 유지할 수 있습니다.) 백업 정책에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 솔루션](storsimple-overview.md)에서 [백업 형식](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies)을 참조하세요.

이 자습서에서는 다음을 수행하는 방법을 설명합니다.

* 백업 정책 만들기
* 백업 정책 편집
* 백업 정책 삭제

## <a name="create-a-backup-policy"></a>백업 정책 만들기
다음 프로시저 toocreate 새 백업 정책을 hello를 사용 합니다.

#### <a name="toocreate-a-backup-policy"></a>백업 정책 toocreate
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창에서 마우스 오른쪽 단추로 클릭 **백업 정책**를 클릭 하 고 **백업 정책 만들기**합니다.

    ![백업 정책 만들기](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    hello **정책 만들기** 대화 상자가 나타납니다.

    ![정책 만들기 - 일반 탭](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. Hello에 **일반** 탭, 다음 정보는 전체 hello:

   1. Hello에 **이름** 입력란 hello 정책에 대 한 이름을 입력 합니다.
   2. Hello에 **볼륨 그룹** 텍스트 상자 hello 정책과 연결 된 hello 볼륨 그룹의 hello 이름을 입력 합니다.
   3. **로컬 스냅숏** 또는 **클라우드 스냅숏** 중 하나를 선택합니다.
   4. 스냅숏 tooretain hello 수를 선택 합니다. 선택 하는 경우 **모든**, 64 개의 스냅숏을 유지 됩니다 (최대 hello).
4. Hello 클릭 **일정** 탭 합니다.

    ![정책 만들기 - 일정 탭](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. Hello에 **일정** 탭, 다음 정보는 전체 hello:

   1. Hello 클릭 **사용** 확인란 tooschedule hello에 대 한 다음 백업 합니다.
   2. **설정** 아래에서 **한 번**, **매일**, **매주** 또는 **매월**을 선택합니다.
   3. Hello에 **시작** 텍스트 상자 hello 달력 아이콘을 클릭 하 고 시작 날짜를 선택 합니다.
   4. **고급 설정**아래에서 선택적 반복 일정과 종료 날짜를 설정할 수 있습니다.
   5. **확인**을 클릭합니다.

다음 정보는 hello hello에 표시 되는 백업 정책을 만든 후 **결과** 창:

* **이름** – hello 백업 정책의 이름입니다.
* **유형** – 로컬 스냅숏 또는 클라우드 스냅숏
* **볼륨 그룹** – hello hello 정책과 연결 된 볼륨 그룹입니다.
* **보존** – hello 보유 스냅숏 개수; hello 최대 64입니다.
* **만든** – hello이이 정책이 생성 된 날짜입니다.
* **활성화** hello 정책 현재 적용 되는지 여부를 –: **True** 있음을 나타냅니다. **False** 적용에서 하지 임을 나타냅니다.

## <a name="edit-a-backup-policy"></a>백업 정책 편집
다음 프로시저 tooedit 기존 백업 정책이 hello를 사용 합니다.

#### <a name="tooedit-a-backup-policy"></a>백업 정책 tooedit
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창의 hello 클릭 **백업 정책** 노드. Hello에 모든 hello 백업 정책 표시 **결과** 창.
3. Hello 정책 tooedit를 원하고 클릭을 마우스 오른쪽 단추로 클릭 **편집**합니다.

    ![백업 정책 편집](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Hello 때 **정책 만들기** 창이 나타나면 변경 내용을 입력 한 다음 클릭 **확인**합니다.

## <a name="delete-a-backup-policy"></a>백업 정책 삭제
다음 프로시저 toodelete 백업 정책을 hello를 사용 합니다.

#### <a name="toodelete-a-backup-policy"></a>백업 정책 toodelete
1. Hello 바탕 화면 아이콘 toostart StorSimple 스냅숏 관리자를 클릭 합니다.
2. Hello에 **범위** 창의 hello 클릭 **백업 정책** 노드. Hello에 모든 hello 백업 정책 표시 **결과** 창.
3. Hello toodelete를 원하고 클릭 한 다음 백업 정책을 마우스 오른쪽 단추로 **삭제**합니다.
4. Hello 확인 메시지가 나타나면 클릭 **예**합니다.

    ![백업 정책 삭제 확인](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.
* 너무 방법에 대해 알아봅니다[tooview StorSimple 스냅숏 관리자를 사용 하 고 백업 작업을 관리](storsimple-snapshot-manager-manage-backup-jobs.md)합니다.
