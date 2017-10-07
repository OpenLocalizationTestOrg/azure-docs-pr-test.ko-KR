---
title: "백업 정책이 aaaManage StorSimple 8000 시리즈 | Microsoft Docs"
description: "StorSimple 장치 관리자 서비스 toocreate hello를 사용 하 여 수동 백업, 백업 일정 및 StorSimple 8000 시리즈 장치에 백업 보존을 관리 하는 방법에 대해 설명 합니다."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>Hello StorSimple 장치 관리자 서비스를 사용 하 여 Azure 포털 toomanage 백업 정책에서


## <a name="overview"></a>개요

이 자습서에서는 어떻게 toouse hello StorSimple 장치 관리자 서비스에 설명 **백업 정책** 블레이드 toocontrol 백업 프로세스 및 StorSimple 볼륨에 대 한 백업 보존 합니다. 에 대해서도 설명 방법을 toocomplete 수동 백업 합니다.

볼륨을 백업 하는 경우에 로컬 스냅숏 또는 클라우드 스냅숏을 toocreate를 선택할 수 있습니다. 로컬로 고정된 볼륨을 백업하는 경우 클라우드 스냅숏을 지정하는 것이 좋습니다. 이탈 수가 많은 데이터 집합과 결합하여 로컬로 고정된 볼륨의 로컬 스냅숏을 많이 만들면 로컬 공간이 빨리 소진될 수 있습니다. 로컬 스냅숏 tootake를 선택 하면 더 적은 일일 스냅숏을 tooback hello 가장 최근 상태를 수행 하는 날에 대 한 유지 한 다음 삭제 하는 것이 좋습니다.

로컬로 고정 된 볼륨의 클라우드 스냅숏을 만들 때만 변경 하는 hello 데이터 toohello 클라우드, 중복 제거 및 압축 된 위치를 복사 합니다.

## <a name="hello-backup-policy-blade"></a>hello 백업 정책 블레이드

hello **백업 정책** toomanage 백업 정책과 일정 로컬 및 클라우드 스냅숏 블레이드 StorSimple 장치에 대 한 수 있습니다. 백업 정책이 사용 되는 tooconfigure 백업 일정 및 백업 보존 볼륨의 컬렉션에 대 한 않습니다. 백업 정책을 사용 하면 여러 볼륨의 스냅숏을 tootake 동시에 있습니다. 이 백업 정책에 의해 생성 된 hello 백업을 크래시 일관성이 있는 복사본 된다는 것을 의미 합니다.

hello 백업 정책이 테이블 형식 목록에는 수도 있습니다 toofilter hello 기존 백업 정책을 hello 필드를 다음 중 하나 이상이 있습니다.

* **정책 이름** – hello hello 정책과 연결 된 이름입니다. hello 여러 가지 유형의 정책 다음과 같습니다.

  * 예약 된 정책을 hello 사용자가 명시적으로 생성 합니다.
  * StorSimple 스냅숏 관리자 hello에서 원래 만든 하는 정책을 가져옵니다. 이러한 hello 정책에서 가져온 hello StorSimple 스냅숏 관리자 호스트를 설명 하는 태그가 포함 됩니다.

  > [!NOTE]
  > 자동 또는 기본 백업 정책은 볼륨 생성 hello 시 더 이상 활성화 됩니다.

* **마지막으로 성공한 백업** – hello 날짜 및 시간 hello 마지막으로 성공한 백업에이 정책을 사용 하 여 만든입니다.

* **다음 백업** – hello의 날짜 및 시간 hello 예약 된 다음 백업이이 정책에 의해 시작 됩니다.

* **볼륨** – hello hello 정책과 연결 된 볼륨입니다. 백업 정책과 연관 된 모든 hello 볼륨은 백업을 만들 때 함께 그룹화 됩니다.

* **일정** – hello hello 백업 정책과 연관 된 일정의 수입니다.

백업 정책에 대해 수행할 수 있는 hello 자주 사용 되는 연산은 다음과 같습니다.

* 백업 정책 추가
* 일정 추가 또는 수정
* 볼륨 추가 또는 제거
* 백업 정책 삭제
* 수동 백업 수행

## <a name="add-a-backup-policy"></a>백업 정책 추가

백업 정책 tooautomatically 일정 백업을 추가 합니다. 볼륨을 처음 만들 때는 볼륨과 연결된 기본 백업 정책이 없습니다. Tooadd 필요 하 고이 정보를 백업 정책 tooprotect 볼륨 데이터를 할당 합니다.

Azure 포털 tooadd StorSimple 장치에 대 한 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다. Hello 정책에 추가한 후에 일정을 정의할 수 있습니다 (참조 [추가 일정을 수정 하거나](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>일정 추가 또는 수정

추가 하거나 StorSimple 장치에 연결 된 tooan 기존 백업 정책이 있는 수정할 수 있습니다. Hello hello Azure 포털 tooadd의에서 단계를 실행 하거나 일정을 수정 합니다.

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>볼륨 추가 또는 제거

추가 하거나 tooa 백업 정책을 StorSimple 장치에 할당 된 볼륨을 제거할 수 있습니다. Azure 포털 tooadd hello 단계를 수행 하는 hello 하거나 볼륨을 제거 합니다.

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>백업 정책 삭제

StorSimple 장치에 Azure 포털 toodelete 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다.

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>수동 백업 수행

단일 볼륨에 대 한 hello Azure 포털 toocreate 주문형 (수동) 백업 단계를 수행 하는 hello를 수행 합니다.

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>다음 단계

에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple 장치 관리자 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.

