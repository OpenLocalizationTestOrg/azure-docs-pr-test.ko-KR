---
title: "aaaView StorSimple 8000 시리즈에 대 한 작업을 관리 하 고 | Microsoft Docs"
description: "Hello StorSimple 장치 관리자 서비스 작업 블레이드 설명 방법과 toouse 것 tootrack 최근, 현재 및 예약 된 백업 작업입니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>StorSimple 장치 관리자 서비스 tooview hello를 사용 하 고 작업 (업데이트 3 이상)를 관리 합니다.

## <a name="overview"></a>개요
hello **작업** 블레이드 보기에 대 한 단일 중앙 포털이 제공 및 tooyour StorSimple 장치 관리자 서비스에 연결 된 장치에서 시작 된 작업을 관리 합니다. 여러 장치에 대해 예약, 실행 중, 완료, 취소, 실패한 작업을 볼 수 있습니다. 결과는 표 형식으로 나타납니다.

![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

와 같은 필드를 필터링 하 여 관심 있는 hello 작업을 빠르게 찾을 수 있습니다.

* **상태** – 작업은 진행 중, 성공, 취소됨, 실패, 취소 중 또는 오류를 나타내며 성공 상태일 수 있습니다.
* **시간 범위** – 작업에 따라 필터링 된 hello 날짜 및 시간 범위를 수 있습니다. hello 범위는 지난 1 시간, 지난 30 일, 지난 해 또는 사용자 지정 날짜 지난 7 일, 지난 24 시간.
* **형식** – 예약 된 백업, 수동 백업, 복원 백업 hello 작업 유형 수 볼륨을 복제 볼륨 컨테이너를 장애 조치할 로컬로 고정 된 볼륨, 볼륨 수정, 업데이트를 설치, 지원 로그 수집을 만들거나 만들 클라우드 어플라이언스에 합니다.
* **장치** – 작업은 특정 연결 된 장치 tooyour 서비스에서 시작 됩니다.
  
hello 필터링 된 작업은 표 형식으로 표시 hello 특성 뒤의 hello 기준:
  
* **이름** – 예약된 백업, 수동 백업, 백업 복원, 볼륨 복제, 볼륨 컨테이너 장애 조치, 로컬로 고정된 볼륨 만들기, 볼륨 수정, 업데이트 설치, 지원 로그 수집 또는 클라우드 어플라이언스 만들기
* **상태** – 실행 중, 완료, 취소, 실패, 취소 중 또는 완료되었으나 오류 발생입니다.
* **엔터티** – hello 작업은 볼륨, 백업 정책 또는 장치가 연결 될 수 있습니다. 예를 들어 복제 작업은 볼륨과 연관되는 반면, 예약된 백업 작업은 백업 정책과 연관됩니다. 장치 작업은 DR(재해 복구) 또는 복원 작업의 결과로 만들어집니다.
* **장치** – hello는 hello 작업이 시작 된 hello 장치의 이름입니다.
* **시작** – hello 작업이 시작 된 hello 시간입니다.
* **기간** – hello 타이머 필요한 toocomplete hello 작업을 수행 합니다.

hello 작업 목록은 30 초 마다 새로 고쳐집니다.

이 페이지에서 작업 관련 동작을 수행 하는 hello를 수행할 수 있습니다.

* 작업 세부 정보 보기
* 작업 취소

## <a name="view-job-details"></a>작업 세부 정보 보기
다음 작업의 단계 tooview hello 세부 정보는 hello를 수행 합니다.

#### <a name="tooview-job-details"></a>tooview 작업 세부 정보
1. StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **작업**합니다.

2. Hello에 **작업** 블레이드, 적절 한 필터가 포함 된 쿼리를 실행 하 여 관심 있는 hello 개의 작업이 표시 됩니다. 완료되거나, 실행 중이거나, 취소된 작업을 검색할 수 있습니다.

    ![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. 작업을 클릭하여 선택합니다.

    ![작업 블레이드](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. Hello 작업 세부 정보 블레이드에서 hello 상태, 세부 정보, 시간 통계 및 데이터 통계를 볼 수 있습니다.
   
    ![작업 세부 정보](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>작업 취소
Hello 다음 단계 toocancel 실행 중인 작업을 수행 합니다.

> [!NOTE]
> 볼륨 toochange hello 볼륨 형식을 수정 하거나, 볼륨 확장 같은 일부 작업을 취소할 수 없습니다.


### <a name="toocancel-a-job"></a>toocancel 작업
1. Hello에 **작업** 페이지에서 적절 한 필터가 포함 된 쿼리를 실행 하 여 toocancel 되도록 hello 실행 중인 작업을 표시 합니다. Hello 작업을 선택 합니다.

2. Hello 선택한 작업 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 클릭 **취소**합니다.

    ![작업 세부 정보](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. 확인하라는 메시지가 표시되면 **예**를 클릭합니다. 이 작업은 이제 취소됩니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 백업 정책 관리](storsimple-8000-manage-backup-policies-u2.md)합니다.
* 너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.

