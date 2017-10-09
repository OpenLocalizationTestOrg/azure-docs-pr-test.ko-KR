---
title: "Azure StorSimple Manager에 대 한 가상 배열 관리 aaaMicrosoft | Microsoft Docs"
description: "Toomanage StorSimple 온-프레미스 가상 배열 hello StorSimple 장치 관리자 서비스에서 사용 하 여 Azure 포털을 hello 하는 방법에 대해 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 958244a5-f9f5-455e-b7ef-71a65558872e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 1fabf9ca524b461266346a6cabf49aef772032ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooadminister-your-storsimple-virtual-array"></a>Hello StorSimple 장치 관리자 서비스 tooadminister StorSimple 가상 배열 사용
![설정 프로세스 흐름](./media/storsimple-virtual-array-manager-service-administration/manage4.png)

## <a name="overview"></a>개요
이 문서에서는이 UI를 통해 tooconnect tooit 및 다양 한 옵션을 사용할 수 및 toohello 특정 워크플로에 대 한 링크를 제공 하는 hello 수 수행 하는 방법을 포함 하 여 hello StorSimple 장치 관리자 서비스 인터페이스를 설명 합니다.

이 문서를 읽은 후 다음 방법에 대해 알 수 있습니다.

* Toohello StorSimple 장치 관리자 서비스 연결
* Hello StorSimple 장치 관리자 UI를 이동 합니다.
* Hello StorSimple 장치 관리자 서비스를 통해 StorSimple 가상 배열 관리

> [!NOTE]
> tooview hello 관리 옵션 hello StorSimple 8000 시리즈 장치에 사용할 수 있는 이동 너무[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.
> 
> 

## <a name="connect-toohello-storsimple-device-manager-service"></a>Toohello StorSimple 장치 관리자 서비스 연결
hello StorSimple 장치 관리자 서비스는 Microsoft Azure에서 실행 하 고 toomultiple StorSimple 가상 배열을 연결 합니다. 이러한 장치는 브라우저 toomanage에서 실행 되는 중앙 Microsoft Azure 포털을 사용 하는 경우. tooconnect toohello StorSimple 장치 관리자 서비스는 다음 hello지 않습니다.

#### <a name="tooconnect-toohello-service"></a>tooconnect toohello 서비스
1. 너무 이동[https://ms.portal.azure.com](https://ms.portal.azure.com)합니다.
2. Microsoft 계정 자격 증명을 사용 하는 (hello의 오른쪽 위에 hello 창에 있는) toohello Microsoft Azure 포털에 로그온 합니다.
3. 탐색 tooBrowse-StorSimple 장치 관리자 tooview에 'Filter'-지정된 된 구독에서 모든 장치 관리자 > 합니다.

## <a name="use-hello-storsimple-device-manager-service-tooperform-management-tasks"></a>Hello StorSimple 장치 관리자 서비스 tooperform 관리 작업을 사용 하 여
hello 다음 표에 모든 hello 일반 관리 작업 및 hello StorSimple 장치 관리자 서비스에 대 한 요약 블레이드 내에서 수행할 수 있는 복잡 한 워크플로에 대 한 요약입니다. 이러한 작업은 시작 되는 hello 블레이드에 따라 구성 됩니다.

각 워크플로에 대 한 자세한 내용은 hello hello 테이블에 적절 한 절차를 클릭 합니다.

#### <a name="storsimple-device-manager-workflows"></a>StorSimple 장치 관리자 워크플로
| 이 toodo 원하는 경우... | 이 절차 사용 |
| --- | --- | --- |
| 서비스 만들기</br>서비스 삭제</br>Hello 서비스 등록 키 가져오기</br>Hello 서비스 등록 키 다시 생성 |[Hello StorSimple 장치 관리자 서비스를 배포 합니다.](storsimple-virtual-array-manage-service.md) |
| Hello 활동 로그 보기 |[요약 hello StorSimple 서비스를 사용 하 여](storsimple-virtual-array-service-summary.md) |
| 가상 배열 비활성화</br>가상 배열 삭제 |[가상 배열 비활성화 또는 삭제](storsimple-virtual-array-deactivate-and-delete-device.md) |
| 재해 복구 및 장치 장애 조치(Failover)</br>장애 조치 필수 구성 요소</br>비즈니스 연속성 재해 복구(BCDR)</br>재해 복구 중 오류 |[StorSimple 가상 배열에 대한 재해 복구 및 장치 장애 조치(failover)](storsimple-virtual-array-failover-dr.md) |
| 공유 및 볼륨 백업</br>수동 백업 수행</br>Hello 백업 일정 변경</br>기존 백업 확인 |[StorSimple 가상 배열 백업](storsimple-virtual-array-backup.md) |
| 백업 세트에서 공유 복제</br>백업 세트에서 볼륨 복제</br>항목 수준 복구(파일 서버에만 해당) |[StorSimple 가상 배열의 백업에서 복제](storsimple-virtual-array-clone.md) |
| Storage 계정 정보</br>저장소 계정 추가</br>저장소 계정 편집</br>저장소 계정 삭제 |[StorSimple 가상 배열 hello에 대 한 저장소 계정 관리](storsimple-virtual-array-manage-storage-accounts.md) |
| 액세스 제어 레코드 정보</br>액세스 제어 레코드 추가 또는 수정 </br>액세스 제어 레코드 삭제 |[StorSimple 가상 배열 hello에 대 한 액세스 제어 레코드 관리](storsimple-virtual-array-manage-acrs.md) |
| 작업 세부 정보 보기 |[StorSimple 가상 배열 작업 관리](storsimple-virtual-array-manage-jobs.md) |
| 경고 설정 구성</br>경고 알림 받기</br>경고 관리</br>경고 검토 |[StorSimple 가상 배열 hello에 대 한 경고 보기 및 관리](storsimple-virtual-array-manage-alerts.md) |
| Hello 장치 관리자 암호를 수정 합니다. |[Hello StorSimple 가상 배열 장치 관리자 암호를 변경 합니다.](storsimple-virtual-array-change-device-admin-password.md) |
| 소프트웨어 업데이트 설치 |[가상 배열 업데이트](storsimple-virtual-array-install-update.md) |

> [!NOTE]
> Hello를 사용 해야 [로컬 웹 UI](storsimple-ova-web-ui-admin.md) hello 작업 다음에 대 한 합니다.
> 
> * [Hello 서비스 데이터 암호화 키를 검색 합니다.](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)
> * [지원 패키지 만들기](storsimple-ova-web-ui-admin.md#generate-a-log-package)
> * [가상 배열 중지 및 다시 시작](storsimple-ova-web-ui-admin.md#shut-down-and-restart-your-device)
> 
> 

## <a name="next-steps"></a>다음 단계
Hello에 대 한 내용은 웹 UI와 방법을 toouse, 너무 이동[사용 하 여 hello StorSimple 웹 UI tooadminister StorSimple 가상 배열](storsimple-ova-web-ui-admin.md)합니다.

