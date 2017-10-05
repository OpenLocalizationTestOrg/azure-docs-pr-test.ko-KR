---
title: "StorSimple 작업 보기 및 관리 | Microsoft Docs"
description: "StorSimple Manager 서비스 작업 페이지에 대해 설명하고 이 페이지를 사용하여 최근, 현재 및 예약된 백업 작업을 추적하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 7d9377bb8f3cb8c587823c2d71d61dfb9b50f52f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs"></a>StorSimple 관리자 서비스를 사용하여 StorSimple 작업 보기 및 관리
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>개요
**작업** 페이지에서는 StorSimple 관리자 서비스에 연결된 장치에서 시작한 작업을 보고 관리하기 위한 하나 중앙 포털을 제공합니다. 여러 장치에 대한 예약, 실행, 완료 및 실패한 작업을 볼 수 있습니다. 결과는 표 형식으로 나타납니다. 

![작업 페이지](./media/storsimple-manage-jobs/HCS_JobsPage.png)

다음과 같이 필드에서 필터링하여 관심 있는 작업을 빠르게 찾을 수 있습니다.

* **상태** – 작업 상태는 실행 중, 예약, 실패, 완료, 취소 중 또는 취소입니다.
* **유형** – 작업은 예약 또는 요청 시 백업(**백업 수행**), 복제, 장치 복원, 업데이트 작업의 결과로 만들어질 수 있습니다.
* **장치** – 작업은 서비스에 연결된 특정 장치에서 시작됩니다.
* **시작 및 종료** – 작업은 날짜 및 시간 범위에 따라 필터링할 수 있습니다.

필터링된 작업은 다음과 같은 특성을 기반으로 표로 정리됩니다.

* **유형** – 백업, 복제, 복원, 장애 조치(failover) 또는 업데이트입니다.
* **상태** – 실행 중, 예약, 실패, 완료, 취소 중 또는 취소입니다.
* **엔터티** – 작업은 볼륨, 백업 정책 또는 장치에 연관될 수 있습니다. 복제 작업은 볼륨과 연관되는 반면, 예약된 백업 작업은 백업 정책과 연관됩니다. 장치 작업은 DR(재해 복구) 또는 복원 작업의 결과로 만들어집니다.
* **장치** – 작업이 시작된 장치의 이름입니다.
* **시작 시간** – 작업이 시작된 시간입니다.
* **진행률** – 실행 중인 작업의 완료율입니다. 완료된 작업의 경우 항상 100%여야 합니다.

작업 목록은 30초마다 새로 고쳐집니다.

이 페이지에서 다음 작업과 관련된 작업을 수행할 수 있습니다.

* 작업 세부 정보 보기
* 작업 취소

## <a name="view-job-details"></a>작업 세부 정보 보기
다음 단계에 따라 작업 세부 정보를 봅니다.

#### <a name="to-view-job-details"></a>작업 세부 정보 보는 방법
1. **작업** 페이지에서 적절한 필터와 함께 쿼리를 실행하여 관심 있는 작업을 표시합니다. 완료되거나, 실행 중이거나, 취소된 작업을 검색할 수 있습니다.
2. 작업을 선택합니다.
3. 페이지 맨 아래에서 **세부 정보**를 클릭합니다.
4. **백업 작업 세부 정보** 대화 상자에서 상태, 세부 정보, 시간 통계 및 데이터 통계를 볼 수 있습니다.

## <a name="cancel-a-job"></a>작업 취소
다음 단계에 따라 실행 중인 작업을 취소합니다.

### <a name="to-cancel-a-job"></a>작업 취소 방법
1. **작업** 페이지에서 적절한 필터와 함께 쿼리를 실행하여 취소하려는 실행 중인 작업을 표시합니다.
2. 작업을 선택합니다.
3. 페이지 맨 아래에서 **취소**를 클릭합니다.
4. 확인하라는 메시지가 표시되면 **예**를 클릭합니다.

이 작업은 이제 취소됩니다.

## <a name="next-steps"></a>다음 단계
* [StorSimple 백업 정책을 관리](storsimple-manage-backup-policies.md)하는 방법을 알아봅니다.
* [StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 알아봅니다.

