---
title: "aaaManage StorSimple 백업 정책 | Microsoft Docs"
description: "StorSimple Manager 서비스 toocreate hello를 사용 하 여 수동 백업, 백업 일정 및 백업 보유 관리 하는 방법에 대해 설명 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a>Hello StorSimple 관리자 서비스 toomanage 백업 정책을 사용 하 여
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>개요
이 자습서에서는 어떻게 toouse hello StorSimple Manager 서비스에 설명 **백업 정책** 페이지 toocontrol 백업 프로세스 및 StorSimple 볼륨에 대 한 백업 보존 합니다. 에 대해서도 설명 방법을 toocomplete 수동 백업 합니다.

hello **백업 정책** toomanage 백업 정책과 일정 로컬 및 클라우드 스냅숏 페이지에서는 있습니다. (백업 정책이 사용 되는 tooconfigure 백업 일정 및 백업 보존 볼륨의 컬렉션에 대 한 않습니다.) 백업 정책을 사용 하면 여러 볼륨의 스냅숏을 tootake 동시에 있습니다. 이 백업 정책에 의해 생성 된 hello 백업을 크래시 일관성이 있는 복사본 된다는 것을 의미 합니다. 이 페이지는 hello 백업 정책, 유형, 연결 된 hello 볼륨, 보존 된 백업 hello 수를 나열 하 고 이러한 정책을 옵션 tooenable hello 합니다.

hello **백업 정책** 페이지도 있습니다 toofilter hello 기존 백업 정책을 하나 이상의 필드를 다음 hello:

* **정책 이름** – hello hello 정책과 연결 된 이름입니다. hello 여러 가지 유형의 정책 다음과 같습니다.
  
  * 예약 된 정책을 hello 사용자가 명시적으로 생성 합니다.
  * 볼륨 만들기의 hello 시간에서이 볼륨 옵션에 대 한 기본 백업 hello를 설정할 때 만들어지는 자동 정책. 이러한 정책은 VolumeName_Default 볼륨 이름을 hello hello Azure 클래식 포털에서에서 hello 사용자가 구성 된 StorSimple 볼륨의 toohello 이름 여기서은 참조로 지정 됩니다. hello 자동 정책 22 시 30 장치 시간부터 시작 하는 일별 클라우드 스냅숏이 발생 합니다.
  * StorSimple 스냅숏 관리자 hello에서 원래 만든 하는 정책을 가져옵니다. 이러한 hello 정책에서 가져온 hello StorSimple 스냅숏 관리자 호스트를 설명 하는 태그가 포함 됩니다.
* **볼륨** – hello hello 정책과 연결 된 볼륨입니다. 백업 정책과 연관 된 모든 hello 볼륨은 백업을 만들 때 함께 그룹화 됩니다.
* **마지막으로 성공한 백업** – hello 날짜 및 시간 hello 마지막으로 성공한 백업에이 정책을 사용 하 여 만든입니다.
* **다음 백업** – hello의 날짜 및 시간 hello 예약 된 다음 백업이이 정책에 의해 시작 됩니다.
* **일정** – hello hello 백업 정책과 연관 된 일정의 수입니다.

이 페이지에서 수행할 수 있는 hello 자주 사용 되는 연산은 다음과 같습니다.

* 백업 정책 추가 
* 일정 추가 또는 수정 
* 백업 정책 삭제 
* 수동 백업 수행 
* 여러 볼륨과 일정의 사용자 지정 백업 정책 만들기 

## <a name="add-a-backup-policy"></a>백업 정책 추가
백업 정책 tooautomatically 일정 백업을 추가 합니다. Azure 클래식 포털 tooadd StorSimple 장치에 대 한 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다. Hello 정책에 추가한 후에 일정을 정의할 수 있습니다 (참조 [추가 일정을 수정 하거나](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

![동영상 사용 가능](./media/storsimple-manage-backup-policies/Video_icon.png) **동영상 사용 가능**

toowatch toocreate 로컬 또는 클라우드 백업 정책에 방법을 보여 주는 비디오에서 클릭 [여기](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/)합니다.

## <a name="add-or-modify-a-schedule"></a>일정 추가 또는 수정
추가 하거나 StorSimple 장치에 연결 된 tooan 기존 백업 정책이 있는 수정할 수 있습니다. Hello hello Azure 클래식 포털 tooadd의에서 단계를 실행 하거나 일정을 수정 합니다.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a>백업 정책 삭제
StorSimple 장치에서 Azure 클래식 포털 toodelete 백업 정책 hello 단계를 수행 하는 hello를 수행 합니다.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>수동 백업 수행
단일 볼륨에 대 한 hello Azure 클래식 포털 toocreate 주문형 (수동) 백업 단계를 수행 하는 hello를 수행 합니다.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>여러 볼륨과 일정의 사용자 지정 백업 정책 만들기
Hello hello Azure 클래식 포털 toocreate 여러 볼륨과 일정이 있는 사용자 지정 백업 정책에에서는 단계를 수행 합니다.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a>다음 단계
에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.

