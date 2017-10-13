---
title: "StorSimple Manager 서비스 대시보드 | Microsoft Docs"
description: "StorSimple 관리자 서비스 대시보드 및 이 대시보드를 사용하여 StorSimple 솔루션의 상태를 모니터링하는 방법을 설명합니다."
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
ms.openlocfilehash: 596431b7279b753ca4da838eb028cdde2022ce02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-dashboard"></a>StorSimple 관리자 서비스 대시보드 사용
## <a name="overview"></a>개요
StorSimple 관리자 서비스 대시보드 페이지는 StorSimple 관리자 서비스에 연결된 모든 장치에 대한 요약 보기를 통해 시스템 관리자의 주의가 필요한 정보를 중점적으로 제공합니다. 이 자습서에서는 대시보드 페이지를 소개하고, 대시보드의 콘텐츠와 기능 및 이 페이지에서 수행할 수 있는 작업에 대해 설명합니다.

![서비스 대시보드](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

StorSimple 관리자 서비스 대시보드에 다음 정보가 표시됩니다.

* **차트** 영역에서 장치 관련 메트릭 차트를 볼 수 있습니다. 일정 시간 동안 장치에서 사용된 클라우드 저장소는 물론, 모든 장치에 걸쳐 사용되는 기본 저장소(로컬로 고정되고 계층화됨)도 볼 수 있습니다. 1주, 1개월, 3개월 또는 1년 단위를 지정하려면 차트 오른쪽 위 모퉁이의 컨트롤을 사용하세요.
* **사용 개요** 에서는 모든 장치에서 사용 가능한 총 저장소를 기준으로 모든 장치에서 프로비전하여 사용하는 기본 저장소를 보여줍니다. **프로비전됨**은 사용을 위해 준비 및 할당된 저장소의 용량을 나타내며 **사용됨**은 장치에 연결된 초기자에 의해 표시된 볼륨의 사용량을 나타냅니다.
* **경고** 영역에서는 경고 심각도별로 그룹화된 모든 장치 간의 모든 활성 경고에 대한 스냅숏을 제공합니다. 심각도 수준을 클릭하면 이러한 경고를 표시하는 **경고** 페이지가 열립니다. **경고** 페이지에서 개별 경고를 클릭하면 권장 조치를 포함하여 해당 경고에 대한 추가적인 정보를 자세히 볼 수 있습니다. 또한 문제가 해결된 경고를 지울 수도 있습니다.
* **작업** 영역에서는 서비스에 연결된 모든 장치의 최근 작업에 대한 스냅숏을 제공합니다. 현재 진행 중인 작업, 지난 24시간 동안 실패한 작업 또는 다음 24시간 내에 실행하도록 예약된 작업을 확인하는 데 사용할 수 있는 링크들이 있습니다.
* **간략 상태** 영역에서는 서비스 상태, 서비스에 연결된 장치 수, 서비스의 위치, 서비스와 연결된 구독의 세부 정보 등과 같은 유용한 정보를 제공합니다. 또한 작업 로그에 대한 링크도 있습니다. 완료된 모든 StorSimple 관리자 서비스 작업 목록을 보려면 이 링크를 클릭하세요.

다음 작업을 수행하는 데 StorSimple 관리자 서비스 대시보드 페이지를 사용할 수 있습니다.

* 서비스 등록 키를 보거나 다시 생성합니다.
* 서비스 데이터 암호화 키를 변경합니다.
* 작업 로그를 봅니다.

## <a name="view-or-regenerate-the-service-registration-key"></a>서비스 등록 키 보기 또는 다시 생성
서비스 등록 키는 장치가 추가적인 관리 작업을 할 수 있는 Azure 클래식 포털에 표시되도록 StorSimple 관리자 서비스에 Microsoft Azure StorSimple 장치를 등록하는 데 사용됩니다. 이 키는 첫 번째 장치에서 만들어지고 나머지 장치와 공유됩니다.

**등록 키**(페이지의 맨 아래)를 클릭하면 **서비스 등록 키** 대화 상자가 열리고, 여기서 현재 서비스 등록 키를 클립보드에 복사하거나 서비스 등록 키를 다시 생성할 수 있습니다.

키를 다시 생성해도 이전에 등록된 장치에는 영향을 주지 않으며 해당 키를 다시 생성한 후 서비스에 등록한 장치에만 영향을 줍니다.

서비스 등록 키를 보고 생성하는 방법에 대한 자세한 내용은 [서비스 등록 키 가져오기](storsimple-manage-service.md#get-the-service-registration-key)를 참조하세요.

## <a name="change-the-service-data-encryption-key"></a>서비스 데이터 암호화 키 변경
서비스 데이터 암호화 키는 StorSimple 관리자 서비스에서 StorSimple 장치로 전송된 저장소 계정 자격 증명 등의 기밀 고객 데이터를 암호화하는 데 사용됩니다. IT 조직에 저장 장치에 대한 키 회전 정책이 있는 경우는 이러한 키를 주기적으로 변경해야 합니다. 키 변경 프로세스는 StorSimple 관리자 서비스에서 관리하는 장치가 단일 장치인지, 여러 장치인지에 따라 약간 달라질 수 있습니다.

서비스 데이터 암호화 키는 3단계 프로세스에 따라 변경됩니다.

1. Azure 클래식 포털을 사용하여 장치에 서비스 데이터 암호화 키를 변경할 권한을 부여합니다.
2. StorSimple용 Windows PowerShell을 사용하여 서비스 데이터 암호화 키 변경을 시작합니다.
3. 둘 이상의 StorSimple 장치를 사용하는 경우에는 다른 장치에서 서비스 데이터 암호화 키를 업데이트합니다.

다음 단계에서는 서비스 데이터 암호화 키의 롤오버 프로세스를 설명합니다.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-the-operations-logs"></a>작업 로그 보기
대시보드의 **간략 상태** 창에 있는 작업 로그 링크를 클릭하여 해당 작업 로그를 볼 수 있습니다. 링크를 클릭하면 관리 서비스 페이지로 이동하므로 여기서 StorSimple 관리자 서비스 관련 로그를 필터링하여 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [StorSimple 장치 문제 해결](storsimple-troubleshoot-operational-device.md)방법을 알아봅니다.
* [StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.

