---
title: "aaaView 및 Microsoft Azure StorSimple 가상 배열 경고 관리 | Microsoft Docs"
description: "StorSimple 가상 배열 경고 조건 및 심각도 및 toouse hello StorSimple Manager toomanage 경고를 서비스 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>StorSimple 가상 배열 hello에 대 한 StorSimple 장치 관리자를 사용 하 여 toomanage 경고

## <a name="overview"></a>개요

StorSimple 장치 관리자 서비스 hello hello 경고 기능 tooreview 수 있는 방법을 제공 하 고 경고 관련된 tooStorSimple 가상 배열을 실시간으로 취소 합니다. Hello 경고를 사용 하 여 hello에 **서비스 요약** 블레이드 toocentrally StorSimple 가상 배열 hello 상태 문제를 모니터링 하 고 전체 Microsoft Azure StorSimple 솔루션 hello 합니다.

이 자습서에 설명 하 고 일반 경고 조건 tooconfigure 경고 알림 경고 심각도 수준을 방법 tooview 및 트랙 경고 합니다. 또한 테이블 tooquickly 수 있도록 하는 특정 경고를 찾아서 적절 하 게 응답할 경고 빠른 참조를 포함 합니다.

![경고 페이지](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>경고 설정 구성

각 StorSimple 가상 배열에 대 한 hello 경고 조건의 전자 메일 알림을 받습니다 toobe 사용할지를 선택할 수 있습니다. Hello에가 전자 메일 주소를 입력 하 여 다른 경고 알림 받는 사람을 식별할 수 또한 **추가 전자 메일 받는 사람에 게** 상자, 세미콜론으로 구분 합니다.

> [!NOTE]
> 가상 배열 당 최대 20개의 메일 주소를 입력할 수 있습니다.


가상 배열에 대 한 전자 메일 알림을 사용 하도록 설정 하면 hello 알림 목록의 구성원이 중요 한 알림이 발생할 때마다 전자 메일 메시지를 받습니다. hello 메시지를 보내는  *storsimple-alerts-noreply@mail.windowsazure.com*  및 hello 경고 조건에 설명 합니다. 받는 사람 클릭 **Unsubscribe** tooremove hello 전자 메일 알림 목록에서 자신입니다.

#### <a name="tooenable-email-notification-for-alerts"></a>경고에 대 한 tooenable 전자 메일 알림

1. 서비스 및 hello tooyour StorSimple 장치 관리자 이동 **관리** 섹션에서 선택한 클릭 **장치**합니다. Hello 표시 하는 장치 목록에서 선택 하 고 장치를 클릭 합니다.
   
    ![경고 설정](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Hello를 열어서이 **설정을** 블레이드입니다. Hello에 **장치 설정** 섹션에서 **일반**합니다. Hello를 열어서이 **일반 설정** 블레이드입니다.
   
    ![경고 알림 구성](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. Hello에 **일반 설정** 블레이드에서 너무 이동**경고 설정** 섹션 및 hello 다음을 설정 합니다.
   
   1. Hello에 **전자 메일 알림 사용** 필드를 선택한 **예**합니다.
   2. Hello에 **서비스 관리자 메일** 필드를 선택한 **예** toohave hello 서비스 관리자를 선택 하 고 모든 공동 관리자 hello 경고 알림 받기.
   3. Hello에 **추가 전자 메일 받는 사람에 게** 필드에, 다른 메일 hello 경고 알림의 받을 hello 전자 메일 주소를 입력 합니다. Hello 형식 이름을 입력  *someone@somewhere.com* 합니다. 세미콜론 tooseparate hello 전자 메일 주소를 사용 합니다. 가상 장치당 최대 20개의 메일 주소를 구성할 수 있습니다.
      
       ![경고 알림 구성](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. 테스트 전자 메일 알림을 toosend 클릭 **테스트 메일 보내기**합니다. hello 테스트 알림을 전달 하 여 hello StorSimple 장치 관리자 서비스 상태 메시지가 표시 됩니다.
      
       ![전송된 경고 테스트 알림 메일](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Hello 테스트 하는 경우 hello StorSimple 장치 관리자 서비스에서 적절 한 메시지를 표시, 알림 메시지 보낼 수 없습니다. 클릭 **확인**몇 분 정도 기다린 후 다시 시도 하십시오 toosend 테스트 알림 메시지입니다.
      > 
      > 
   5. Hello hello 페이지의 아래쪽에 있는 클릭 **저장** toosave 구성 합니다. 확인하라는 메시지가 표시되면 **예**를 클릭합니다.
      
      ![전송된 경고 테스트 알림 메일](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>일반 경고 조건

StorSimple 가상 배열 응답 tooa 다양 한 조건에에서 경고를 생성합니다. hello 다음은 hello 가장 일반적인 유형의 경고 조건.

* **연결 문제** – 이러한 경고는 데이터 전송이 어려울 때 발생합니다. Hello Azure 저장소 계정 또는 기한 데이터 tooand의 전송 하는 동안 통신 문제가 발생할 수 있습니다 toolack hello 가상 장치 및 hello StorSimple 장치 관리자 서비스 간의 연결입니다. 통신 문제는 실패 지점이 매우 많으므로 있기 때문에 가장 어려운 toofix hello의 일부입니다. 네트워크 연결 및 인터넷 액세스를 사용할 수 있는지 고급 문제 해결 toomore를 계속 진행 하기 전에 항상 먼저 확인 해야 합니다. 포트 및 방화벽 설정에 대 한 내용은 이동 너무[StorSimple 가상 배열 시스템 요구 사항](storsimple-ova-system-requirements.md)합니다. 문제 해결에 도움이 필요 하면 이동 너무[hello Test-connection cmdlet으로 문제를 해결](storsimple-troubleshoot-deployment.md)합니다.
* **성능 문제** – 이러한 경고는 부하가 높을 때처럼 시스템이 최적으로 작동하지 않는 경우에 발생합니다.

또한 관련된 toosecurity 경고, 업데이트 또는 작업 실패를 표시 될 수 있습니다.

## <a name="alert-severity-levels"></a>경고 심각도 수준

경고 심각도 수준이 달라, hello hello 영향에 따라 경고 상황이 hello 응답 toohello 경고에 대 한 필요 합니다. hello 심각도 수준은 다음과 같습니다.

* **중요 한** – hello 시스템의 정상적인 성능 영향을 미치는 응답 tooa 조건에서이 경고는 합니다. 동작은 필요한 tooensure hello StorSimple 서비스가 중단 되지 않도록 합니다.
* **경고** – 이 상태는 확인되지 않은 경우 위험할 수 있습니다. Hello 상황을 조사 하 고 별도 작업이 필요 tooclear hello 문제가 있는지를 수행 해야 합니다.
* **정보** – 이 경고는 시스템의 추적 및 관리에 유용할 수 있는 정보를 포함합니다.

## <a name="view-and-track-alerts"></a>경고 보기 및 추적

hello StorSimple 장치 관리자 서비스에 대 한 요약 블레이드를 빠르게 확인할 수 경고 심각도 별로 정렬 하 여 가상 장치의 hello 수 제공 합니다.

![경고 대시보드](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Hello 심각도 수준 tooopen hello 클릭 **경고** 블레이드입니다. hello 결과 해당 심각도 수준과 일치 하는 hello 경고만 포함 됩니다.

![경고 보고서 tooalert 형식 범위](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Hello 목록 tooget hello 경고를 포함 하 여 hello를 마지막으로 hello 경고가 보고 된 hello hello 장치의 hello 경고 및 hello 권장된 조치 tooresolve hello 경고의 발생 수에 대 한 자세한 내용은에서 경고를 클릭 합니다.

![경고 목록 및 세부 정보](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

Toosend hello 정보 tooMicrosoft 지원 해야 할 경우 hello 경고 세부 정보 tooa 텍스트 파일을 복사할 수 있습니다. 뒤에 hello 권장 하 고 hello 경고 조건이 온-프레미스 해결 된 후 hello 목록에서 hello 경고를 지워야 합니다. Hello 목록에서 hello 경고를 선택한 다음 클릭 **지우기**합니다. 여러 개의 경고 경고 각 tooclear hello 제외한 모든 열을 클릭 **경고** 열을 마우스 클릭 한 다음 **지우기** 선택이 취소 경고 toobe hello 모두 선택한 후 합니다.

클릭할 때 **지우기**, hello 경고에 대 한 hello 기회 tooprovide 설명 및가 수행한 tooresolve hello 단계 hello 문제입니다. 

![경고 설명](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

새 정보로 다른 이벤트가 트리거되면 일부 이벤트는 hello 시스템에서 지워집니다. 

## <a name="sort-and-review-alerts"></a>경고 정렬 및 검토

hello **경고** 블레이드 too250 경고를 표시할 수 있습니다. 해당 경고의 수를 초과한 경우 일부 경고만 hello 기본 보기에 표시 됩니다. 다음 필드 toocustomize 표시할 경고를 hello를 결합할 수 있습니다.

* **상태** – **활성** 또는 **지워짐** 경고를 표시할 수 있습니다. 활성 경고는 계속 트리거되고 있는 시스템에 반면 지워짐된 경고 중 하나는 관리자가 수동으로 선택이 취소 되었거나 hello 시스템은 hello 경고 조건을 새 정보로 업데이트 하기 때문에 프로그래밍 방식으로 취소 합니다.
* **심각도** – 모든 심각도 수준(중요, 경고, 정보) 또는 중요한 경고와 같은 특정 심각도의 경고를 표시할 수 있습니다.
* **소스** 또는 모든 가상 장치를 환영 하 – hello 서비스 또는 하나에서 제공 하는 hello 경고 toothose 제한 하거나 모든 원본에서 경고를 표시할 수 있습니다.
* **시간 범위** – hello를 지정 하 여 **에서** 및 **를** hello에 관심 있는 기간 동안 경고 살펴볼 수 날짜 및 시간 스탬프입니다.

## <a name="alerts-quick-reference"></a>빠른 참조 경고

다음 표에서 hello 발생할 수 있는, 추가 정보 및 권장 사항 뿐만 아니라 사용 가능한 hello StorSimple 경고 중 일부를 나열 합니다. StorSimple 가상 배열 경고 hello 다음 범주 중 하나에 속합니다.

* [클라우드 연결 경고](#cloud-connectivity-alerts)
* [구성 경고](#configuration-alerts)
* [작업 실패 경고](#job-failure-alerts)
* [성능 경고](#performance-alerts)
* [보안 경고](#security-alerts)
* [업데이트 경고](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>클라우드 연결 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 장치  *<device name>*  은 toohello 클라우드를 연결 되지 않았습니다. |장치 이름이 hello toohello 클라우드를 연결할 수 없습니다. |Toohello 클라우드를 연결 하지 못했습니다. 때문일 수 있습니다 tooone hello 다음 중:<ul><li>장치에서 hello 네트워크 설정에 문제가 있을 수 있습니다.</li><li>Hello 저장소 계정 자격 증명에 문제가 있을 수 있습니다.</li></ul>연결 문제 해결에 대 한 자세한 내용은 toohello 이동 [로컬 웹 UI](storsimple-ova-web-ui-admin.md) hello 장치입니다. |

### <a name="configuration-alerts"></a>구성 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 온-프레미스 가상 장치 구성은 지원되지 않습니다. |성능 저하. |hello 현재 구성은 성능 저하 될 수 있습니다. 서버 hello 최소 구성 요구 사항을 충족 하는지 확인 합니다. 자세한 내용은 이동 너무[StorSimple 가상 배열 요구 사항](storsimple-ova-system-requirements.md)합니다. |
| <*장치 이름*>에서 프로비전된 디스크 공간이 부족합니다. |디스크 공간 경고입니다. |프로비전된 디스크 공간이 부족합니다. 공간을 toofree 작업 tooanother 볼륨 또는 공유를 이동 하거나 데이터를 삭제 하십시오. |

### <a name="job-failure-alerts"></a>작업 실패 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| <*장치 이름*>의 백업을 완료할 수 없습니다. |백업 작업이 실패했습니다. |백업을 만들 수 없습니다. Hello 다음 중 하나를 선택 하세요.<ul><li>백업 작업이 성공적으로 완료 hello 연결 문제로 인해 수 있습니다. 연결 문제가 없는지 확인합니다. 연결 문제 해결에 대 한 자세한 내용은 toohello 이동 [로컬 웹 UI](storsimple-ova-web-ui-admin.md) 가상 장치에 대 한 합니다.</li><li>Hello 사용 가능한 저장소 용량 한도 도달 했습니다. toofree 공간을 더 이상 필요 없는 백업이 모두 삭제 하십시오.</li></ul> Hello 문제를 해결 하 고 hello 경고를 지우세요 hello 작업을 다시 시도 합니다. |
| <*장치 이름*>의 복제를 완료할 수 없습니다. |복제 작업이 실패했습니다. |복제본을 만들 수 없습니다. Hello 다음 중 하나를 선택 하세요.<ul><li>백업 목록이 잘못되었을 수 있습니다. 여전히 유효 hello 목록 tooverify를 새로 고칩니다.</li><li>Hello 복제 작업이 성공적으로 완료 연결 문제로 인해 수 있습니다. 연결 문제가 없는지 확인합니다.</li><li>Hello 사용 가능한 저장소 용량 한도 도달 했습니다. toofree 공간을 더 이상 필요 없는 백업이 모두 삭제 하십시오.</li></ul>Hello 문제를 해결 하 고 hello 경고를 지우세요 hello 작업을 다시 시도 합니다. |

### <a name="performance-alerts"></a>성능 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 데이터 전송에 예기치 않은 대기 시간이 발생했습니다. |느린 데이터 전송. |저장소 서비스의 hello 확장성 대상을 초과 하면 제한 오류가 발생 합니다. hello 저장소 서비스는이 tooensure 하는 단일 클라이언트나 테 넌 트의 hello 부담 hello 서비스를 사용할 수 있습니다. Azure 저장소 계정 문제 해결에 대 한 자세한 내용은 이동 너무[모니터, 진단 및 해결 Microsoft Azure 저장소](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)합니다. |
| <*장치 이름*>의 로컬 예약 디스크 공간이 부족합니다. |느린 응답 시간. |hello의 10% 전체에 대 한 프로 비전 된 크기 <*장치 이름*>는 예약 되어 hello에 로컬 장치 사용자가 이제 예약 된 공간 hello에 부족 합니다. hello 작업에 <*장치 이름*>를 생성 하는 더 높은 변동을의 속도 수 최근에 마이그레이션한 많은 양의 데이터입니다. 이로 인해 성능이 저하될 수 있습니다. 중 하나를 고려 작업 tooresolve 다음이 hello:<ul><li>Hello 클라우드 대역폭 toothis 장치를 늘립니다.</li><li>줄이거나 작업 tooanother 볼륨 또는 공유를 이동 합니다.</li></ul> |

### <a name="security-alerts"></a>보안 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| <*장치 이름*>에 대한 암호가 <*숫자*> 일 후에 만료됩니다. |암호 경고. |암호가 <숫자>일에 만료됩니다. 암호를 변경하는 것이 좋습니다. 자세한 내용은 이동 너무[hello StorSimple 가상 배열 장치 관리자 암호 변경](storsimple-virtual-array-change-device-admin-password.md)합니다. |

### <a name="update-alerts"></a>업데이트 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 장치에 새 업데이트를 사용할 수 있습니다. |업데이트 toohello StorSimple 가상 배열 제공 됩니다. |Hello에서 새 업데이트를 설치할 수 있습니다 **유지 관리** 페이지. |
| <*장치 이름*>에서 새 업데이트를 스캔할 수 없습니다. |업데이트에 실패했습니다. |새 업데이트를 설치하는 동안 오류가 발생했습니다. Hello 업데이트를 수동으로 설치할 수 있습니다. Hello 문제가 계속 되 면 문의 [Microsoft 지원](storsimple-contact-microsoft-support.md)합니다. |

## <a name="next-steps"></a>다음 단계

* [StorSimple 가상 배열 hello에 대 한 자세한 내용은](storsimple-ova-overview.md)합니다.

