---
title: "스냅숏 관리자 관리 aaaStorSimple | Microsoft Docs"
description: "StorSimple 스냅숏 관리자 솔루션 관리 작업 및 워크플로에 대 한 toomore 정보 한 개요와 링크를 제공 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 1cdbb61d-bd16-4be4-ade2-ceab11508acb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2016
ms.author: v-sharos
ms.openlocfilehash: d875f2efbdeb844b412cf8d9f1f971f18da7526e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooadminister-your-storsimple-solution"></a>StorSimple 스냅숏 관리자 tooadminister StorSimple 솔루션 사용

## <a name="overview"></a>개요
StorSimple 스냅숏 관리자는 Microsoft Azure StorSimple 환경에서 데이터 보호 및 백업 관리를 간소화하는 Microsoft Management Console(MMC) 스냅인입니다. StorSimple 스냅숏 관리자를 관리할 수 있습니다 hello 클라우드 및 hello 데이터 센터에서 데이터를 Microsoft Azure StorSimple 단일 통합된 저장소 솔루션으로 따라서 있어 백업 프로세스가 단순화 되 고 비용이 절감 합니다.

hello StorSimple 스냅숏 관리자 중앙 관리 콘솔을 사용 하면 toocreate 일관 되 고 지정 시간 백업 복사본의 로컬 및 클라우드 데이터 있습니다. 예를 들어 hello 콘솔을 사용할 수 있습니다.

* 볼륨을 구성, 백업 및 삭제합니다.
* 볼륨 구성 데이터를 백업 하는 그룹 tooensure는 응용 프로그램 일치 합니다.
* 미리 정해진 일정에 따라 데이터가 백업되도록 백업 정책을 관리합니다.
* Hello 클라우드에 저장 하 고 재해 복구에 사용할 수 있는 데이터의 독립적인 복사본을 만듭니다.

이 문서에서는 링크 tootutorials StorSimple 스냅숏 관리자를 설명 하는 방법과 toouse 것 toocomplete 시스템 관리 작업 및 워크플로 합니다.

* StorSimple 스냅숏 관리자 구성 요소 및 아키텍처에 대한 자세한 내용은 [StorSimple 스냅숏 관리자란?](storsimple-what-is-snapshot-manager.md) 
* StorSimple 스냅숏 관리자 toodownload 너무 이동[hello StorSimple 스냅숏 관리자 다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=44220)합니다.
* StorSimple 스냅숏 관리자 배포 절차에 대 한 이동 너무[StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md)합니다.

> [!NOTE]
> StorSimple 스냅숏 관리자 toomanage Microsoft Azure StorSimple 가상 배열 (라고도 StorSimple 온-프레미스 가상 장치)를 사용할 수 없습니다.


## <a name="storsimple-snapshot-manager-tasks-and-workflows"></a>StorSimple 스냅숏 관리자 작업 및 워크플로
StorSimple 스냅숏 관리자 toomonitor hello를 사용 하 고 현재, 예약 및 완료 된 백업 작업을 관리할 수 있습니다. 또한 StorSimple 스냅숏 관리자 완료 too64 백업 카탈로그를 제공합니다. Hello 카탈로그 toofind 사용 및 볼륨 또는 개별 파일을 복원할 수 있습니다. 

| 경우에 원하는 tooDO THIS 중... | 자습서의 참조 위치 |
|:--- |:--- |
| StorSimple 스냅숏 관리자에 대해 자세히 알아봅니다. |[StorSimple 스냅숏 관리자란? ](storsimple-what-is-snapshot-manager.md) |
| StorSimple 스냅숏 관리자 설치<br>StorSimple Snapshot Manager 다시 설치<br>StorSimple 스냅숏 관리자 제거 |[StorSimple 스냅숏 관리자 배포](storsimple-snapshot-manager-deployment.md) |
| StorSimple 스냅숏 관리자 메뉴 및 기능 사용:<ul><li>메뉴 모음</li><li>도구 모음</li><li>범위 창</li><li>결과 창</li><li>작업 창</li><li>키보드 탐색 및 바로 가기</li></ul> |[StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md) |
| StorSimple 스냅숏 관리자에 포함 된 hello 일반적인 MMC 기능을 사용 합니다.<ul><li>보기</li><li>여기에서 창 새로 만들기</li><li>새로 고침</li><li>목록 내보내기</li><li>도움말</li></ul> |[StorSimple 스냅숏 관리자 hello MMC 메뉴 작업을 사용 하 여](storsimple-snapshot-manager-mmc-menu.md) |
| 장치 추가 또는 교체<br>장치 연결<br>가져온 볼륨 그룹 확인<br>연결된 장치 새로 고침<br>장치 인증<br>장치 세부 정보 보기<br>장치 구성 삭제<br>장치 암호 변경<br>실패한 장치 바꾸기<br> |[StorSimple 스냅숏 관리자 tooconnect를 사용 하 고 StorSimple 장치를 관리 합니다.](storsimple-snapshot-manager-manage-devices.md) |
| 볼륨 탑재<br>볼륨에 대한 정보 보기<br>볼륨 삭제<br>볼륨 다시 검사<br>기본 볼륨 구성 및 백업<br>동적 미러 볼륨 구성 및 백업 |[StorSimple 스냅숏 관리자 tooview를 사용 하 고 볼륨 관리](storsimple-snapshot-manager-manage-volumes.md) |
| 볼륨 그룹 보기<br>볼륨 그룹 만들기<br>볼륨 그룹 백업<br>볼륨 그룹 편집<br>볼륨 그룹 삭제 |[StorSimple 스냅숏 관리자 toocreate를 사용 하 고 볼륨 그룹 관리](storsimple-snapshot-manager-manage-volume-groups.md) |
| 백업 정책 만들기 <br>백업 정책 편집<br>백업 정책 삭제 |[StorSimple 스냅숏 관리자 toocreate를 사용 하 고 백업 정책 관리](storsimple-snapshot-manager-manage-backup-policies.md) |
| 예약된 백업 작업 보기 및 관리<br>최근 백업 작업 보기 및 관리<br>현재 실행 중인 백업 작업 보기 및 관리 |[StorSimple 스냅숏 관리자 tooview를 사용 하 고 백업 작업 관리](storsimple-snapshot-manager-manage-backup-jobs.md) |
| 볼륨 복원<br>볼륨 또는 볼륨 그룹 복제<br>백업 삭제<br>파일 복구<br>Hello StorSimple 스냅숏 관리자 데이터베이스 복원 |[StorSimple 스냅숏 관리자를 사용 하 여 toomanage hello 백업 카탈로그](storsimple-snapshot-manager-manage-backup-catalog.md) |

## <a name="next-steps"></a>다음 단계
[StorSimple 스냅숏 관리자 다운로드](https://www.microsoft.com/download/details.aspx?id=44220)

