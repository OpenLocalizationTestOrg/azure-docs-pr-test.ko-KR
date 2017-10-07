---
title: "aaaStorSimple 관리자 서비스 대시보드 | Microsoft Docs"
description: "Hello StorSimple 관리자 서비스 대시보드를 설명 하 고 설명 어떻게 toouse 것 StorSimple 솔루션의 toomonitor hello 상태입니다."
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>Hello StorSimple 관리자 서비스 대시보드 사용
## <a name="overview"></a>개요
hello StorSimple 관리자 서비스 대시보드 페이지 모든 hello 장치 연결된 toohello 시스템 관리자의 주의가 필요한 사용자를 강조 표시 되는 StorSimple Manager 서비스에 대 한 요약 보기를 제공 합니다. 이 자습서 hello 대시보드 페이지를 소개 하 고 hello 대시보드 콘텐츠 및 함수를 설명 하며이 페이지에서 수행할 수 있는 hello 작업에 설명 합니다.

![서비스 대시보드](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

hello StorSimple 관리자 서비스 대시보드는 hello 다음 정보를 표시 합니다.

* Hello에 **차트** 영역을 표시 하는 장치에 대 한 hello 관련 메트릭 차트입니다. Hello 기본 저장소 (로컬로 고정 된 및 계층)를 볼 수 시간 동안 장치에서 사용 하는 hello 클라우드 저장소 뿐만 아니라 모든 hello 장치에서 사용 합니다. Hello 차트 toospecify 1 주, 1 개월, 3 개월 또는 1 년 간 시간 간격의 hello 오른쪽 위 모서리에서 hello 컨트롤을 사용 합니다.
* hello **사용 개요** 프로 비전 되 고 모든 장치에서 모든 장치 상대 toohello 총 사용 가능한 저장소에서 사용 되는 기본 저장소를 hello 보여 줍니다. **사용자를 프로 비전** toohello 양의 준비 되 고 사용 하기 위해 할당 된 저장소 참조 **사용** toohello 연결된 장치로 되는 hello 초기자에 의해 표시 된 대로 toousage 볼륨의를 참조 합니다.
* hello **경고** 영역 경고 심각도 별로 그룹화 하는 모든 hello 장치에서 모든 hello 활성 경고에 대 한 스냅숏을 제공 합니다. Hello 열립니다 hello 심각도 수준을 클릭 하면 **경고** 페이지, 범위가 지정 된 tooshow 경고 합니다. Hello에 **경고** 페이지 권장된 조치를 포함 하 여 해당 경고에 대 한 개별 경고 tooview 추가 세부 정보 클릭 수 있습니다. Hello 문제가 해결 된 경우에 hello 경고를 지울 수 있습니다.
* hello **작업** 영역에는 연결 된 모든 장치에서 최근 작업 스냅숏이 제공 tooyour 서비스입니다. Toolook 현재 지난 24 시간 동안 hello에 실패 하는 진행 중인 작업에 사용할 수 있는 링크 또는 다음 24 시간 동안 toorun hello에 예약 되는 것입니다.
* hello **눈에 보는** 영역에서는 서비스 상태, 장치 연결 된 toohello 서비스, hello 서비스의 위치와 hello 서비스와 관련 된 hello 구독 세부 정보와 수 등 유용한 정보를 제공 합니다. 링크 toohello 작업 로그 이기도합니다. Hello 링크 toosee 목록이 완료 된 모든 StorSimple Manager 서비스 작업을 클릭 합니다.

Hello StorSimple 관리자 서비스 대시보드 페이지 tooinitiate hello 다음 작업을 사용할 수 있습니다.

* 보거나 hello 서비스 등록 키 다시 생성 합니다.
* Hello 서비스 데이터 암호화 키를 변경 합니다.
* Hello 작업 로그를 봅니다.

## <a name="view-or-regenerate-hello-service-registration-key"></a>보거나 hello 서비스 등록 키 다시 생성
hello 서비스 등록 키는 hello 장치에에서 표시 되도록 hello 추가 관리 작업을 위해 Azure 클래식 포털 사용 되는 tooregister hello StorSimple Manager 서비스를 사용 하 여 Microsoft Azure StorSimple 장치를입니다. hello 키 hello 첫 번째 장치에 만들어지고 나머지 장치 hello와 공유 합니다.

클릭 하면 **등록 키** (hello hello 페이지 맨) hello 열립니다 **서비스 등록 키** 어느 hello 현재 서비스 등록 키 toohello 클립보드로 복사를 수행할 수 있는 대화 상자 또는 hello 서비스 등록 키 다시 생성 합니다.

Hello 키 다시 생성 이전에 등록 된 장치에는 영향을 주지: hello 장치 서비스에 등록 된 hello hello 키가 다시 생성 한 후에 영향을 줍니다.

보기 및 너무 hello 서비스 등록 키를 이동 생성 하는 방법에 대 한 자세한 내용은[Get hello 서비스 등록 키](storsimple-manage-service.md#get-the-service-registration-key)합니다.

## <a name="change-hello-service-data-encryption-key"></a>Hello 서비스 데이터 암호화 키 변경
서비스 데이터 암호화 키는 StorSimple 관리자 서비스 toohello StorSimple 장치에서 전송 된 저장소 계정 자격 증명과 같은 사용 되는 tooencrypt 고객 기밀 데이터입니다. 필요 합니다 toochange 이러한 키는 정기적으로 IT 조직 hello 저장 장치에 대 한 키 순환 정책을 경우. hello 키 변경 프로세스 수 약간 다를 수 있는지에 따라 장치를 하나 또는 여러 장치 hello StorSimple Manager 서비스에서 관리 합니다.

Hello 서비스 데이터 암호화 키 변경 3 단계로 구성 됩니다.

1. Azure 클래식 포털 hello using, 장치 toochange hello 서비스 데이터 암호화 키 권한을 부여 합니다.
2. StorSimple 용 Windows PowerShell을 사용 하 여, hello 서비스 데이터 암호화 키 변경을 시작 합니다.
3. 하나 이상의 StorSimple 장치가 있는 경우 hello 서비스 데이터 암호화 키 hello에 다른 장치를 업데이트 합니다.

hello 다음 단계에서는 hello 서비스 데이터 암호화 키에 대 한 hello 롤오버 프로세스.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>Hello 작업 로그 보기
Hello에서 사용할 수 있는 hello 작업 로그 링크를 클릭 하 여 hello 작업 로그를 볼 수 **눈에 보는** hello 대시보드의 창이 있습니다. 그러면 toohello 관리 서비스 페이지에서 필터링 하 고 hello 참조 수 로그 특정 tooyour StorSimple Manager 서비스입니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[StorSimple 장치 문제 해결](storsimple-troubleshoot-operational-device.md)합니다.
* 너무 방법에 대 한 자세한[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

