---
title: "서비스 관리 관리자 aaaStorSimple | Microsoft Docs"
description: "방법을 사용 하 여 StorSimple 장치에서 StorSimple Manager 서비스 hello toomanage hello Azure 클래식 포털에 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>StorSimple 장치의 StorSimple Manager 서비스 tooadminister hello를 사용 하 여
## <a name="overview"></a>개요
이 문서에서는 tooconnect tooit hello, 사용 가능한 다양 한 옵션 및이 UI를 통해 수행할 수 있는 특정 워크플로에 toohello 아웃 연결 방법을 포함 하 여 hello StorSimple 관리자 서비스 인터페이스를 설명 합니다. 이 설명서는 적용 가능한 tooboth; hello StorSimple 물리적 및 가상 장치 hello 합니다.

이 문서를 읽은 후 다음에 대해 알 수 있습니다.

* TooStorSimple 관리자 서비스를 연결 합니다.
* Hello StorSimple 관리자 UI를 이동 합니다.
* Hello StorSimple Manager 서비스를 통해 StorSimple 장치를 관리 합니다.

## <a name="connect-toostorsimple-manager-service"></a>TooStorSimple 관리자 서비스를 연결 합니다.
hello StorSimple Manager 서비스는 Microsoft Azure에서 실행 하 고 toomultiple StorSimple 장치를 연결 합니다. 이러한 장치는 브라우저 toomanage에서 실행 되는 중앙 Microsoft Azure 클래식 포털을 사용 합니다. tooconnect toohello StorSimple 관리자 서비스는 다음 hello지 않습니다.

#### <a name="tooconnect-toohello-service"></a>tooconnect toohello 서비스
1. 너무 이동[https://manage.windowsazure.com/](https://manage.windowsazure.com/)합니다.
2. Microsoft 계정 자격 증명을 사용 하는 (hello의 오른쪽 위에 hello 창에 있는) toohello Microsoft Azure 클래식 포털에 로그온 합니다.
3. 왼쪽 탐색 창 tooaccess hello StorSimple 관리자 서비스는 hello 아래로 스크롤하십시오.

## <a name="navigate-storsimple-manager-service-ui"></a>StorSimple Manager 서비스 UI로 이동
UI는 다음 표에 hello에 표시 되는 hello StorSimple Manager 서비스에 대 한 탐색 계층을 hello 합니다.

* **StorSimple Manager** 방문 페이지 toohello UI 서비스 수준 페이지 tooall 적용 가능한 장치는 서비스 내에서 이동 합니다.
* **장치** 페이지 toohello 장치 – 수준 UI 페이지 적용 가능한 tooa 특정 장치를 사용 합니다.
* **볼륨 컨테이너** 페이지는 장치와 관련 된 모든 hello 볼륨을 보여 주는 toohello 볼륨 페이지를 사용 합니다.

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>StorSimple Manager 서비스 탐색 계층
| 방문 페이지 | 서비스 수준 페이지 | 장치 수준 페이지 | 장치 수준 페이지 |
| --- | --- | --- | --- |
| StorSimple 관리자 서비스 |서비스 대시보드 |장치 대시보드 | |
| 장치 → |모니터 | | |
| 백업 카탈로그 |볼륨 컨테이너→ |볼륨 | |
| (서비스) 구성 |백업 정책 | | |
| 작업 |(장치) 구성 | | |
| 경고 |유지 관리 | | |

![동영상 사용 가능](./media/storsimple-manager-service-administration/Video_icon.png) **동영상 사용 가능**

hello StorSimple 관리자 서비스 사용자 인터페이스를 안내 하는 비디오 toowatch 클릭 [여기](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/)합니다.

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>StorSimple Manager 서비스를 사용한 StorSimple 장치 관리
hello 다음 표에 모든 hello 일반 관리 작업 및 hello StorSimple Manager 서비스 UI 내에서 수행할 수 있는 복잡 한 워크플로에 대 한 요약입니다. 이러한 작업은 시작 되는 hello UI 페이지에 따라 구성 됩니다.

각 워크플로에 대 한 자세한 내용은 hello hello 테이블에 적절 한 절차를 클릭 합니다.

#### <a name="storsimple-manager-workflows"></a>StorSimple Manager 워크플로
| 이 toodo 원하는 경우... | Toothis UI 페이지를 이동 하는 중... | 이 절차를 사용합니다. |
| --- | --- | --- |
| 서비스 만들기</br>서비스 삭제</br>서비스 등록 키 가져오기</br>서비스 등록 키 다시 생성 |StorSimple 관리자 서비스 |[StorSimple Manager 서비스 배포](storsimple-manage-service.md) |
| Hello 서비스 데이터 암호화 키 변경</br>Hello 작업 로그 보기 |StorSimple Manager 서비스 → 대시보드 |[Hello StorSimple 관리자 서비스 대시보드 사용](storsimple-service-dashboard.md) |
| 장치 비활성화</br>장치 삭제 |StorSimple Manager 서비스 → 장치 |[장치 비활성화 또는 장치 삭제](storsimple-deactivate-and-delete-device.md) |
| 재해 복구 및 장치 장애 조치(Failover)</br>장애 조치 tooa 물리적 장치</br>장애 조치 tooa 가상 장치</br>비즈니스 연속성 재해 복구(BCDR) |StorSimple Manager 서비스 → 장치 |[StorSimple 장치에 대한 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md) |
| 볼륨에 대한 백업 목록</br>백업 세트를 선택합니다.</br>백업 세트 삭제 |StorSimple Manager 서비스 → 백업 카탈로그 |[백업 관리](storsimple-manage-backup-catalog.md) |
| 볼륨 복제 |StorSimple Manager 서비스 → 백업 카탈로그 |[볼륨 복제](storsimple-clone-volume.md) |
| 백업 세트 복원 |StorSimple Manager 서비스 → 백업 카탈로그 |[백업 세트 복원](storsimple-restore-from-backup-set.md) |
| Storage 계정 정보</br>저장소 계정 추가</br>저장소 계정 편집</br>저장소 계정 삭제</br>저장소 계정의 키 회전 |StorSimple Manager 서비스 → 구성 |[저장소 계정 관리](storsimple-manage-storage-accounts.md) |
| 대역폭 템플릿 정보</br>대역폭 템플릿 추가</br>대역폭 템플릿 편집</br>대역폭 템플릿 삭제</br>기본 대역폭 템플릿 사용</br>지정된 시간에 시작되는 하루 종일 대역폭 템플릿 만들기 |StorSimple Manager 서비스 → 구성 |[대역폭 템플릿 관리](storsimple-manage-bandwidth-templates.md) |
| 액세스 제어 레코드 정보</br>액세스 제어 레코드 만들기</br>액세스 제어 레코드 편집</br>액세스 제어 레코드 삭제 |StorSimple Manager 서비스 → 구성 |[액세스 제어 레코드 관리](storsimple-manage-acrs.md) |
| 작업 세부 정보 보기</br>작업 취소 |StorSimple Manager 서비스 → 작업 |[작업 관리](storsimple-manage-jobs.md) |
| 경고 알림 받기</br>경고 관리</br>경고 검토 |StorSimple Manager 서비스 → 경고 |[StorSimple 경고 보기 및 관리](storsimple-manage-alerts.md) |
| 연결된 초기자 보기</br>Hello 장치 일련 번호 찾기</br>Hello 대상 IQN 찾기 |StorSimple Manager 서비스 → 장치 → 대시보드 |[Hello StorSimple 장치 대시보드 사용](storsimple-device-dashboard.md) |
| 모니터링 차트 만들기 |StorSimple Manager 서비스 → 장치 → 모니터링 |[StorSimple 장치 모니터링](storsimple-monitor-device.md) |
| 볼륨 컨테이너 추가</br>볼륨 컨테이너 수정</br>볼륨 컨테이너 삭제 |StorSimple Manager 서비스 → 장치 → 볼륨 컨테이너 |[볼륨 컨테이너 관리](storsimple-manage-volume-containers.md) |
| 볼륨 추가</br>볼륨 수정</br>볼륨을 오프라인으로 전환</br>볼륨 삭제</br>볼륨 모니터링 |StorSimple Manager 서비스 → 장치 → 볼륨 컨테이너 → 볼륨 |[볼륨 관리](storsimple-manage-volumes.md) |
| 장치 설정 수정</br>시간 설정 수정</br>DNS.md 설정 수정</br>네트워크 인터페이스 구성 |StorSimple Manager 서비스 → 장치 → 구성 |[StorSimple 장치에 대한 장치 구성 수정](storsimple-modify-device-config.md) |
| 웹 프록시 설정 보기 |StorSimple Manager 서비스 → 장치 → 구성 |[장치에 대한 웹 프록시 구성](storsimple-configure-web-proxy.md) |
| 장치 관리자 암호 수정</br>StorSimple 스냅숏 관리자 암호 수정 |StorSimple Manager 서비스 → 장치 → 구성 |[StorSimple 암호 변경](storsimple-change-passwords.md) |
| 원격 관리 구성 |StorSimple Manager 서비스 → 장치 → 구성 |[Tooyour StorSimple 장치를 원격으로 연결](storsimple-remote-connect.md) |
| 경고 설정 구성 |StorSimple Manager 서비스 → 장치 → 구성 |[StorSimple 경고 보기 및 관리](storsimple-manage-alerts.md) |
| StorSimple 장치에 대한 CHAP 구성 |StorSimple Manager 서비스 → 장치 → 구성 |[StorSimple 장치에 대한 CHAP 구성](storsimple-configure-chap.md) |
| 백업 정책 추가</br>일정 추가 또는 수정</br>백업 정책 삭제</br>수동 백업 수행</br>여러 볼륨 및 일정으로 사용자 지정 백업 정책 만들기 |StorSimple Manager 서비스 → 장치 → 백업 정책 |[백업 정책 관리](storsimple-manage-backup-policies.md) |
| 장치 컨트롤러 중지</br>장치 컨트롤러 다시 시작</br>장치 컨트롤러 종료</br>장치 toofactory 기본값 다시 설정</br>(위는 온-프레미스 장치용) |StorSimple Manager 서비스 → 장치 → 유지 관리 |[StorSimple 장치 컨트롤러 관리](storsimple-manage-device-controller.md) |
| StorSimple 하드웨어 구성 요소</br>하드웨어 상태 모니터링</br>(위는 온-프레미스 장치용) |StorSimple Manager 서비스 → 장치 → 유지 관리 |[하드웨어 구성 요소 모니터링](storsimple-monitor-hardware-status.md) |
| 지원 패키지 만들기 |StorSimple Manager 서비스 → 장치 → 유지 관리 |[지원 패키지 만들기 및 관리](storsimple-create-manage-support-package.md) |
| 소프트웨어 업데이트 설치 |StorSimple Manager 서비스 → 장치 → 유지 관리 |[장치 업데이트](storsimple-update-device.md) |

## <a name="next-steps"></a>다음 단계
StorSimple 장치의 hello 일상적인 작업이 나 해당 하드웨어 구성 요소를 사용 하 여 문제가 발생 하는 경우 참조 합니다.

* [작동 가능 장치 문제 해결](storsimple-troubleshoot-operational-device.md)
* [StorSimple 모니터링 표시기 LED 사용](storsimple-monitoring-indicators.md)

Hello 문제를 해결할 수 없는 toocreate 서비스 요청을 해야 하는 경우 너무 참조[Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)합니다.

