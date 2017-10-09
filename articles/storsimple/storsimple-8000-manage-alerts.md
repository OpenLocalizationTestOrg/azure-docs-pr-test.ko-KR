---
title: "aaaView StorSimple 8000 시리즈 장치에 대 한 경고 및 관리 | Microsoft Docs"
description: "StorSimple 경고 조건 및 심각도, tooconfigure 알림, 경고 하는 방법 및 toouse hello StorSimple 장치 관리자 toomanage 경고를 서비스 하는 방법을 설명 합니다."
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
ms.workload: NA
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: fdd1a911ceff542bc6bdeae877e1f0fc381bf27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-storsimple-alerts"></a>StorSimple 장치 관리자 서비스 tooview hello를 사용 하 고 StorSimple 경고 관리

## <a name="overview"></a>개요

hello **경고** 블레이드 hello StorSimple 장치 관리자 서비스에서에서 사용 하면 있습니다 tooreview 및 지우기 StorSimple 장치 관련 경고를 실시간으로 합니다. 이 블레이드에서 StorSimple 장치 hello 상태 문제를 모니터링 하 고 전체 Microsoft Azure StorSimple 솔루션 hello 중앙 집중식으로 있습니다.

이 자습서에서는 일반 경고 조건, 경고 심각도 수준 및 tooconfigure 경고 알림 방법을 설명 합니다. 또한 테이블 tooquickly 수 있도록 하는 특정 경고를 찾아서 적절 하 게 응답할 경고 빠른 참조를 포함 합니다.

![경고 페이지](./media/storsimple-8000-manage-alerts/configure-alerts-email11.png)

## <a name="common-alert-conditions"></a>일반 경고 조건

StorSimple 장치 응답 tooa 다양 한 조건에에서 경고를 생성합니다. hello 다음은 hello 가장 일반적인 유형의 경고 조건.

* **하드웨어 문제** – 하드웨어의 hello 상태에 대 한 온라인입니다. 펌웨어 업그레이드가 필요하거나 네트워크 인터페이스에 문제가 있는 경우 또는 데이터 드라이브에 문제가 있으면 알 수 있습니다.
* **연결 문제** – 이러한 경고는 데이터 전송이 어려울 때 발생합니다. Hello Azure 저장소 계정 또는 기한 데이터 tooand의 전송 하는 동안 통신 문제가 발생할 수 있습니다 toolack hello 장치와 hello StorSimple 장치 관리자 서비스 간의 연결입니다. 통신 문제는 실패 지점이 매우 많으므로 있기 때문에 가장 어려운 toofix hello의 일부입니다. 네트워크 연결 및 인터넷 액세스를 사용할 수 있는지 고급 문제 해결 toomore를 계속 진행 하기 전에 항상 먼저 확인 해야 합니다. 문제 해결에 도움이 필요 하면 이동 너무[hello Test-connection cmdlet으로 문제를 해결](storsimple-troubleshoot-deployment.md)합니다.
* **성능 문제** – 이러한 경고는 부하가 높을 때처럼 시스템이 최적으로 작동하지 않는 경우에 발생합니다.

또한 관련된 toosecurity 경고, 업데이트 또는 작업 실패를 표시 될 수 있습니다.

## <a name="alert-severity-levels"></a>경고 심각도 수준

경고 심각도 수준이 달라, hello hello 영향에 따라 경고 상황이 hello 응답 toohello 경고에 대 한 필요 합니다. hello 심각도 수준은 다음과 같습니다.

* **중요 한** – hello 시스템의 정상적인 성능 영향을 미치는 응답 tooa 조건에서이 경고는 합니다. 동작은 필요한 tooensure hello StorSimple 서비스가 중단 되지 않도록 합니다.
* **경고** – 이 상태는 확인되지 않은 경우 위험할 수 있습니다. Hello 상황을 조사 하 고 별도 작업이 필요 tooclear hello 문제가 있는지를 수행 해야 합니다.
* **정보** – 이 경고는 시스템의 추적 및 관리에 유용할 수 있는 정보를 포함합니다.

## <a name="configure-alert-settings"></a>경고 설정 구성

각 StorSimple 장치에 대 한 경고 조건의 전자 메일 알림을 받습니다 toobe 사용할지를 선택할 수 있습니다. Hello에가 전자 메일 주소를 입력 하 여 다른 경고 알림 받는 사람을 식별할 수 또한 **다른 전자 메일 받는 사람** 상자, 세미콜론으로 구분 합니다.

> [!NOTE]
> 장치 당 최대 20개의 메일 주소를 입력할 수 있습니다.

장치에 대 한 전자 메일 알림을 사용 하도록 설정 하면 hello 알림 목록의 구성원이 중요 한 알림이 발생할 때마다 전자 메일 메시지를 받습니다. hello 메시지를 보내는  *storsimple-alerts-noreply@mail.windowsazure.com*  및 hello 경고 조건에 설명 합니다. 받는 사람 클릭 **Unsubscribe** tooremove hello 전자 메일 알림 목록에서 자신입니다.

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>장치에 대 한 경고의 전자 메일 알림을 tooenable
1. Tooyour StorSimple 장치 관리자 서비스를 이동 합니다. Hello 장치 목록에서 선택 하 고 원하는 tooconfigure hello 장치를 클릭 합니다.
2. 너무 이동**설정** > **일반** hello 장치에 대 한 합니다.

   ![경고 블레이드](./media/storsimple-8000-manage-alerts/configure-alerts-email2.png)
   
2. Hello에 **일반 설정** 블레이드에서 너무 이동**경고 설정** hello 다음을 설정 하 고 있습니다.
   
   1. Hello에 **전자 메일 알림 보내기** 필드를 선택한 **예**합니다.
   2. Hello에 **서비스 관리자 메일** 필드를 선택한 **예** toohave hello 서비스 관리자와 모든 공동 관리자 hello 경고 알림을 받도록 합니다.
   3. Hello에 **다른 전자 메일 받는 사람** 필드에, 다른 메일 hello 경고 알림의 받을 hello 전자 메일 주소를 입력 합니다. Hello 형식 이름을 입력  *someone@somewhere.com* 합니다. 세미콜론 tooseparate hello 전자 메일 주소를 사용 합니다. 장치당 최대 20개의 메일 주소를 구성할 수 있습니다. 
      
3. 테스트 전자 메일 알림을 toosend 클릭 **테스트 메일 보내기**합니다. hello 테스트 알림을 전달 하 여 hello StorSimple 장치 관리자 서비스 상태 메시지가 표시 됩니다.

    ![경고 설정](./media/storsimple-8000-manage-alerts/configure-alerts-email3.png)

4. Hello 테스트 전자 메일을 보내면 알림이 표시 됩니다. 
   
    ![전송된 경고 테스트 알림 메일](./media/storsimple-8000-manage-alerts/configure-alerts-email4.png)
   
   > [!NOTE]
   > Hello 테스트 하는 경우 hello StorSimple 장치 관리자 서비스가 적절 한 오류 메시지가 표시 됩니다, 알림 메시지 보낼 수 없습니다. 몇 분 정도 기다린 후 다시 시도 하십시오 toosend 테스트 알림 메시지. 

5. Hello 구성을 완료 한 후 클릭 **저장**합니다. 확인하라는 메시지가 표시되면 **예**를 클릭합니다.

     ![전송된 경고 테스트 알림 메일](./media/storsimple-8000-manage-alerts/configure-alerts-email5.png)

## <a name="view-and-track-alerts"></a>경고 보기 및 추적

hello StorSimple 장치 관리자 서비스에 대 한 요약 블레이드 hello 수 경고 심각도 별로 정렬 하 여 사용자 장치에서의 빠른 보기를 제공 합니다.

![경고 대시보드](./media/storsimple-8000-manage-alerts/device-summary4.png)

Hello 열립니다 hello 심각도 수준을 클릭 하면 **경고** 블레이드입니다. hello 결과 해당 심각도 수준과 일치 하는 hello 경고만 포함 됩니다.

Hello 목록에서 경고를 클릭 하면 정보를 제공 추가 hello 경고에 대 한, 포함 하 여 hello 마지막 시간 hello 경고가 보고 된, hello hello 장치와 hello hello 경고의 발생 수 tooresolve hello 경고 작업을 권장 합니다. 하드웨어 경고 이면 hello 하드웨어 구성을 요소도 표시 됩니다.

![하드웨어 경고 예](./media/storsimple-8000-manage-alerts/configure-alerts-email14.png)

Toosend hello 정보 tooMicrosoft 지원 해야 할 경우 hello 경고 세부 정보 tooa 텍스트 파일을 복사할 수 있습니다. Hello에 hello 경고를 선택 하 여 hello 장치에서 hello 경고를 지우세요 해야 하면 뒤에 hello 추천을 해결 한 hello 경고 조건이 온-프레미스 후 **경고** 블레이드를 클릭 하 고 **의선택을취소**. 여러 개의 경고 경고 각 tooclear hello 제외한 모든 열을 클릭 **경고** 열을 마우스 클릭 한 다음 **지우기** 선택이 취소 경고 toobe hello 모두 선택한 후 합니다. Note hello 문제 해결 되거나 hello 시스템 hello 경고를 새 정보로 업데이트 하는 경우 일부 경고 자동으로 정리 됩니다.

클릭할 때 **지우기**, hello 경고에 대 한 hello 기회 tooprovide 설명 및가 수행한 tooresolve hello 단계 hello 문제입니다. 새 정보로 다른 이벤트가 트리거되면 일부 이벤트는 hello 시스템에서 지워집니다. 이 경우 hello 메시지의 뒤에 표시 됩니다.

![경고 메시지 지우기](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>경고 정렬 및 검토

검토 하 고 그룹에서 지울 수 있도록 경고에 대 한 보다 효율적인 toorun 보고서 찾을 수 있습니다. 또한 hello **경고** 블레이드 too250 경고를 표시할 수 있습니다. 해당 경고의 수를 초과한 경우 일부 경고만 hello 기본 보기에 표시 됩니다. 다음 필드 toocustomize 표시할 경고를 hello를 결합할 수 있습니다.

* **상태** – **활성** 또는 **지워짐** 경고를 표시할 수 있습니다. 활성 경고는 계속 트리거되고 있는 시스템에 반면 지워짐된 경고 중 하나는 관리자가 수동으로 선택이 취소 되었거나 hello 시스템은 hello 경고 조건을 새 정보로 업데이트 하기 때문에 프로그래밍 방식으로 취소 합니다.
* **심각도** – 모든 심각도 수준(중요, 경고, 정보) 또는 중요한 경고와 같은 특정 심각도의 경고를 표시할 수 있습니다.
* **소스** – hello 서비스 또는 하나 또는 모든 hello 장치에서 발생 하는 hello 경고 toothose 제한 하거나 모든 원본에서 경고를 표시할 수 있습니다.
* **시간 범위** – hello를 지정 하 여 **에서** 및 **를** hello에 관심 있는 기간 동안 경고 살펴볼 수 날짜 및 시간 스탬프입니다.

![경고 목록](./media/storsimple-8000-manage-alerts/configure-alerts-email11.png)

## <a name="alerts-quick-reference"></a>빠른 참조 경고

다음 표에서 hello 일부 hello Microsoft Azure StorSimple 경고가 발생할 수 있는, 추가 정보 및 권장 사항 뿐만 아니라 사용 가능한 나열 합니다. StorSimple 장치 경고 hello 다음 범주 중 하나에 속합니다.

* [클라우드 연결 경고](#cloud-connectivity-alerts)
* [클러스터 경고](#cluster-alerts)
* [재해 복구 경고](#disaster-recovery-alerts)
* [하드웨어 경고](#hardware-alerts)
* [작업 실패 경고](#job-failure-alerts)
* [로컬로 고정된 볼륨 경고](#locally-pinned-volume-alerts)
* [네트워킹 경고](#networking-alerts)
* [성능 경고](#performance-alerts)
* [보안 경고](#security-alerts)
* [지원 패키지 경고](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>클라우드 연결 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 연결 너무 <*클라우드 자격 증명 이름*> 설정할 수 없습니다. |Toohello 저장소 계정을 연결할 수 없습니다. |장치에 연결 문제가 있을 수 있습니다. Hello를 실행 하십시오 `Test-HcsmConnection` cmdlet에서 StorSimple 용 Windows PowerShell 인터페이스를 장치 tooidentify에 hello 및 hello 문제를 해결 합니다. Hello 설정이 올바른 경우 hello 경고가 발생 한 hello 저장소 계정의 hello 자격 증명으로 hello 문제가 발생할 수 있습니다. 이 경우 hello를 사용 하 여 `Test-HcsStorageAccountCredential` cmdlet toodetermine 해결할 수 있는 문제가 있는 경우.<ul><li>네트워크 설정을 확인합니다.</li><li>저장소 계정 자격 증명을 확인합니다.</li></ul> |
| 수신 하지 않았습니다 하트 비트 hello에 대 한 장치에서 마지막 <*번호*> 시간 (분)입니다. |Toodevice를 연결할 수 없습니다. |장치에 연결 문제가 있을 수 있습니다. Hello를 사용 하 여 하십시오 `Test-HcsmConnection` cmdlet에서 장치 tooidentify에서 StorSimple 용 Windows PowerShell 인터페이스를 hello 및 hello 문제를 해결 하거나 네트워크 관리자에 게 문의 합니다. |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>클라우드 연결에 실패할 경우의 StorSimple 동작

프로덕션 환경에서 실행 중인 내 StorSimple 장치에 대한 클라우드 연결에 실패하면 어떻게 되나요?

프로덕션 StorSimple 장치에서 클라우드 연결 실패 하면 다음 장치 hello 상태에 따라 hello 다음 발생할 수 있습니다.

* **장치에서 로컬 데이터 hello에 대 한**: 일정 시간 동안 중단 없이 있고이 읽기 작업은 계속 toobe 제공 합니다. 그러나 Io hello 수가 증가 하 고 한도 초과 hello 읽기 toofail를 시작할 수 있습니다.

    장치에서 데이터의 양을 hello 따라 hello 쓰기도에서 계속 됩니다 toooccur hello에 대 한 hello 중단 후 처음 몇 시간 동안 hello 클라우드 연결 합니다. hello 쓰기 다음 속도가 저하 되 고 몇 시간 동안 hello 클라우드 연결에 문제가 있을 경우 toofail 결국 시작 됩니다. (저장소가 임시 데이터 toobe toohello 클라우드 푸시에 대 한 hello 장치 에서입니다. 이 영역은 hello 데이터를 보낼 때 플러시됩니다. 연결에 실패 하면이 저장소 영역에서 데이터 toohello 클라우드 푸시되 지 고 IO 실패 합니다.)
* **Hello 클라우드에서 hello 데이터에 대 한**: 대부분의 클라우드 연결 오류에 대 한 오류가 반환 됩니다. Hello 연결이 복원 되 면 hello IOs hello 사용자 toobring hello 볼륨을 온라인가 필요 하지 않고 다시 시작 됩니다. 경우에 따라에서 사용자 개입이 필요한 toobring 백 hello 볼륨을 온라인 hello Azure 포털에서에서 수 있습니다.
* **클라우드 스냅숏 진행에서에 대 한**: hello 작업 4-5 시간 내에서 여러 번 다시 시도 되 고 hello 연결, 복원 되지 않으면 hello 클라우드 스냅숏 실패 합니다.

### <a name="cluster-alerts"></a>클러스터 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 장치 장애 조치 너무 <*장치 이름*> 합니다. |장치는 유지 관리 모드입니다. |장치 장애 조치 기한 tooentering 또는 기존 유지 관리 모드. 정상이며 어떤 조치가 필요하지 않습니다. 이 경고를 승인 하는 후 hello 경고 페이지에서 선택을 취소 합니다. |
| 장치 장애 조치 너무 <*장치 이름*> 합니다. |장치 펌웨어 또는 소프트웨어가 업데이트되었습니다. |클러스터 장애 조치로 인해 tooan 업데이트 했습니다. 정상이며 어떤 조치가 필요하지 않습니다. 이 경고를 승인 하는 후 hello 경고 페이지에서 선택을 취소 합니다. |
| 장치 장애 조치 너무 <*장치 이름*> 합니다. |컨트롤러를 종료하거나 다시 시작합니다. |Hello 활성 컨트롤러를 종료 하거나 관리자에 의해 다시 시작 하는 장치가 장애 조치 합니다. 어떤 조치가 필요하지 않습니다. 이 경고를 승인 하는 후 hello 경고 페이지에서 선택을 취소 합니다. |
| 장치 장애 조치 너무 <*장치 이름*> 합니다. |계획된 장애 조치입니다. |계획된 장애 조치인지 확인합니다. 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요. |
| 장치 장애 조치 너무 <*장치 이름*> 합니다. |계획되지 않은 장애 조치입니다. |StorSimple은 계획 되지 않은 장애 조치에서 tooautomatically 복구가 빌드됩니다. 이러한 알림이 많이 표시되면 Microsoft 지원에 문의합니다. |
| 장치 장애 조치 너무 <*장치 이름*> 합니다. |기타 / 알 수 없는 원인입니다. |이러한 알림이 많이 표시되면 Microsoft 지원에 문의합니다. Hello 문제를 해결 한 후 hello 경고 페이지에서이 경고를 지우세요. |
| 중요한 장치 서비스는 상태를 실패한 것으로 보고합니다. |데이터 경로 서비스가 실패했습니다. |Microsoft 지원에 문의합니다. |
| 네트워크 인터페이스 <*데이터 #*>에 대한 가상 IP 주소는 상태를 실패한 것으로 보고합니다. |기타 / 알 수 없는 원인입니다. |때로 일시적인 조건으로 인해 이러한 경고가 발생할 수 있습니다. Hello 대/소문자 인 경우 자동으로이 경고 일정 시간이 지난 후 지워집니다 됩니다. Hello 문제가 지속 되 면 Microsoft 지원에 문의 합니다. |
| 네트워크 인터페이스 <*데이터 #*>에 대한 가상 IP 주소는 상태를 실패한 것으로 보고합니다. |인터페이스 이름: <*데이터 #*> IP 주소 <IP address> hello 네트워크에서 중복 IP 주소를 검색 되었기 때문에 온라인 할 수 없습니다. |중복 IP 주소가 hello hello 네트워크에서 제거 됩니다. 또는 다른 IP 주소를 가진 hello 인터페이스를 다시 구성 하십시오. |

### <a name="disaster-recovery-alerts"></a>재해 복구 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 복구 작업의 모든이 서비스에 대 한 hello 설정을 복원 하지 못했습니다. 장치 구성 데이터는 일부 장치에 대해 일관성 없는 상태입니다. |재해 복구 후에 데이터 일치가 검색되었습니다. |Hello 장치의 hello 서비스에 암호화 된 데이터와 동기화 되지 않습니다. Hello 장치 권한 부여 <*장치 이름*> StorSimple 장치 관리자 toostart hello 동기화 프로세스에서 합니다. StorSimple toorun hello에 대 한 Windows PowerShell 인터페이스 사용 하 여 hello `Restore-HcsmEncryptedServiceData` 장치에 <*장치 이름*> cmdlet을 cmdlet toorestore hello 보안 프로필 입력된 toothis로 hello 이전 암호를 제공 합니다. 그러고 나 서 hello `Invoke-HcsmServiceDataEncryptionKeyChange` cmdlet tooupdate hello 서비스 데이터 암호화 키입니다. 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요. |

### <a name="hardware-alerts"></a>하드웨어 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 하드웨어 구성 요소 <*구성 요소 ID*>에서 상태를 <*상태*>로 보고합니다. | |때로 일시적인 조건으로 인해 이러한 경고가 발생할 수 있습니다. 그렇다면 이 경고는 일정 시간 후에 자동으로 지워집니다. Hello 문제가 지속 되 면 Microsoft 지원에 문의 합니다. |
| 오작동하는 수동 컨트롤러입니다. |hello 수동 (보조) 컨트롤러가 작동 하지 않습니다. |장치는 작동하지만 컨트롤러 중 하나가 작동하지 않습니다. 해당 컨트롤러를 다시 시작하세요. Hello 문제가 해결 되지 않으면 Microsoft 지원에 문의 합니다. |

### <a name="job-failure-alerts"></a>작업 실패 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| <*원본 볼륨 그룹 ID*>의 백업에 실패했습니다. |백업 작업이 실패했습니다. |백업 작업이 성공적으로 완료 hello 연결 문제로 인해 수 있습니다. 연결 문제가 없으면 hello 최대 백업 수에 도달한 수 있습니다. Hello 작업을 다시 시도 하 고 필요 하지 않은 백업을 삭제 합니다. 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요. |
| 복제 <*백업 요소 Id 원본*> 너무 <*대상 볼륨 일련 번호*> 하지 못했습니다. |복제 작업이 실패했습니다. |백업 hello 새로 고침 hello 백업 목록 tooverify 계속 유효 합니다. Hello 백업이 유효한 경우 클라우드 연결 문제로 인해 hello 복제 작업이 성공적으로 완료 하지 않음을 가능한 됩니다. 연결 문제가 없으면 hello 저장소 용량 한도 초과한 것 같습니다. Hello 작업을 다시 시도 하 고 필요 하지 않은 백업을 삭제 합니다. Tooresolve hello 문제 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요. |
| <*원본 백업 요소 ID*>의 복원에 실패했습니다. |복원 작업이 실패했습니다. |백업 hello 새로 고침 hello 백업 목록 tooverify 계속 유효 합니다. Hello 백업이 유효한 경우 클라우드 연결 문제로 인해 hello 복원 작업이 성공적으로 완료 하지 않음을 가능한 됩니다. 연결 문제가 없으면 hello 저장소 용량 한도 초과한 것 같습니다. Hello 작업을 다시 시도 하 고 필요 하지 않은 백업을 삭제 합니다. Tooresolve hello 문제 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요. |

### <a name="locally-pinned-volume-alerts"></a>로컬로 고정된 볼륨 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 로컬 볼륨 <*볼륨 이름*> 만들기에 실패했습니다. |hello 볼륨 만들기 작업이 실패 했습니다. <*오류 메시지에 대 한 해당 toohello 실패 오류 코드*> 합니다. |Hello 공간 만들기 작업이 성공적으로 완료 연결 문제로 인해 수 있습니다. 로컬로 고정 된 볼륨은 씩 프로 비전 하 고 hello 공간 만들기 프로세스는 것과 관련이 toohello 클라우드 계층화 된 볼륨입니다. 연결 문제가 없는지, hello hello 장치의 로컬 공간이 소진 되었을 수 있습니다. 이 작업을 다시 시도 하기 전에 hello 장치에 공간이 있는지 확인 합니다. |
| 로컬 볼륨 <*볼륨 이름*> 확장에 실패했습니다. |hello 볼륨 수정 작업이 실패 했습니다 기한 너무 <*오류 메시지에 대 한 해당 toohello 실패 오류 코드*> 합니다. |Hello 볼륨 확장 작업이 성공적으로 완료 연결 문제로 인해 수 있습니다. 로컬로 고정 된 볼륨은 씩 프로 비전 하 고 hello 공간 확장 프로세스는 hello 기존 것과 관련이 toohello 클라우드 계층화 된 볼륨입니다. 연결 문제가 없는지, hello hello 장치의 로컬 공간이 소진 되었을 수 있습니다. 이 작업을 다시 시도 하기 전에 hello 장치에 공간이 있는지 확인 합니다. |
| 볼륨 <*볼륨 이름*> 변환에 실패했습니다. |hello 볼륨 변환 작업이 tooconvert hello 볼륨 유형 로컬로 고정 된 tootiered에서 실패 했습니다. |로컬로 고정 형식 tootiered hello 볼륨의 변환을 완료할 수 없습니다. 인해 hello 작업이 성공적으로 완료 하는 연결 문제가 없는지 확인 합니다. 문제 해결을 위해 문제 이동 너무[hello Test-hcsmconnection cmdlet으로 문제를 해결](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet)합니다.<br>로컬로 고정 hello 원래 볼륨 toohello 클라우드 hello 변환 하는 동안 유출 hello 로컬로 고정 된 볼륨에서 hello 데이터 중 일부가 있으므로 이제 계층화 된 볼륨으로 표시 되었습니다. hello 결과 계층화 된 볼륨 여전히 향후 로컬 볼륨에 대 한 다시 사용할 수 없습니다는 hello 장치에서 로컬 공간을 차지 하 고 있습니다.<br>연결 문제를 해결 하 고 hello 경고를 지우세요이 볼륨 백 toohello 원래 로컬 고정된 볼륨 유형 tooensure 모든 hello 데이터를 제공할 로컬로 다시 변환 합니다. |
| 볼륨 <*볼륨 이름*> 변환에 실패했습니다. |hello 볼륨 변환 작업이 tooconvert hello 볼륨 유형 고정 된 계층화 된 toolocally에서 실패 했습니다. |Hello 볼륨의 계층화 된 toolocally 고정 하는 형식에서 변환을 완료할 수 없습니다. 인해 hello 작업이 성공적으로 완료 하는 연결 문제가 없는지 확인 합니다. 문제 해결을 위해 문제 이동 너무[hello Test-hcsmconnection cmdlet으로 문제를 해결](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet)합니다.<br>hello 원래 계층화 된 볼륨 이제 hello 변환 프로세스 계속 hello 씩이 볼륨에 대 한 hello 장치에 공간을 프로 비전 하는 동안 hello 클라우드에 있는 toohave 데이터도 로컬로 고정 된 볼륨으로 표시는 향후 로컬 더 이상 다시 사용할 수 없습니다. 볼륨입니다.<br>모든 연결 문제, 지우기 hello 경고 및이 볼륨 백 toohello 원래 계층화 된 볼륨 유형 tooensure 로컬 씩 hello 장치에서 프로 비전 확보할 수 있는 공간이 convert 해결 합니다. |
| <*볼륨 그룹 이름*>의 로컬 스냅숏에 대한 로컬 공간 소비에 거의 도달 |곧 hello 백업 정책의 로컬 스냅숏 공간이 부족 하 고 무효화 tooavoid 호스트 쓰기 실패 수 수 있습니다. |이 백업 정책 그룹과 연결 된 hello 볼륨의 데이터 변동이 로컬 스냅숏을 자주 로컬 공간 빠르게 사용 하는 hello 장치 toobe에 발생 합니다. 더 이상 필요 없는 로컬 스냅숏을 삭제합니다. 또한이 백업 정책 tootake 로컬 스냅숏 자주 덜에 대 한 사용자의 로컬 스냅숏 일정을 업데이트 하 고 클라우드 스냅숏을 정기적으로 만드는 있는지 확인 하십시오. 이러한 동작은 수행 되지 않습니다, 이러한 스냅숏에 대 한 로컬 공간이 곧 소진 될 수 있습니다 및 hello 시스템에서 자동으로 하는 경우 호스트 쓰기가 계속 성공적으로 처리 toobe tooensure 삭제. |
| <*볼륨 그룹 이름*>에 대한 로컬 스냅숏이 무효화되었습니다. |에 대 한 로컬 스냅숏을 hello <*볼륨 그룹 이름을*> 무효화 되 고 hello hello 장치의 로컬 공간을 초과 된 다음 삭제 되었습니다. |hello, 향후에이 문제가 반복 되지 tooensure hello이 백업 정책의 로컬 스냅숏 일정을 검토 하 고 필요 하지 않은 로컬 스냅숏을 삭제 합니다. 이 백업 정책 그룹과 연결 된 hello 볼륨의 데이터 변동이 로컬 스냅숏을 자주 빠르게 사용 하는 hello 장치 toobe에서 로컬 공간을 발생할 수 있습니다. |
| <*원본 백업 요소 ID*>의 복원에 실패했습니다. |hello 복원 작업이 실패 했습니다. |로컬로 고정 된 경우이 백업 정책 백업 hello 새로 고침 hello 백업 목록 tooverify에서에서 고정 된 로컬과 계층화 된 볼륨을 혼합 하 여 여전히 유효 합니다. Hello 백업이 유효한 경우 클라우드 연결 문제로 인해 hello 복원 작업이 성공적으로 완료 하지 않음을 가능한 됩니다. 로컬로 hello이 스냅숏 그룹의 일부 데이터 다운로드 한 toohello 장치를 모두가지고 있지 않습니다 및 계층 구성 및 로컬 고정 볼륨의 혼합이 스냅숏 그룹에 있으면 됩니다 서로와 동기화 된 복원 되 고 볼륨을 고정 합니다. toosuccessfully는 hello 복원 작업 완료, hello 볼륨 hello 호스트에서 오프 라인으로이 그룹의 걸리고 hello 복원 작업을 다시 시도 하십시오. 참고 hello 중에 수행 된 모든 수정 내용을 toohello 볼륨 데이터 복원 프로세스는 손실 됩니다. |

### <a name="networking-alerts"></a>네트워킹 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| StorSimple 서비스를 시작하지 못했습니다. |데이터 경로 오류 |Hello 문제가 계속 되 면 Microsoft 지원에 문의 합니다. |
| 'Data0'에 대한 중복 IP 주소가 검색되었습니다. | |hello 시스템에서 IP 주소 '10.0.0.1'에 대 한 충돌을 감지 했습니다. hello 장치에서 네트워크 리소스 'Data0' hello  *<device1>*  오프 라인 상태입니다. 이 IP 주소가 이 네트워크의 다른 엔터티에서 사용되지 않음을 확인합니다. tootroubleshoot 네트워크 문제가 너무 이동[hello Get-netadapter cmdlet으로 문제를 해결](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet)합니다. 이 문제 해결에 대한 도움은 네트워크 관리자에게 문의합니다. Hello 문제가 계속 되 면 Microsoft 지원에 문의 합니다. |
| 'Data0'에 대한 IPv4(또는 IPv6) 주소가 오프라인 상태입니다. | |'10.0.0.1'의 IP 주소를 사용 하 여 hello 네트워크 리소스 'Data0' hello 장치에 접두사 길이 '22' 및  *<device1>*  오프 라인 상태입니다. 이 인터페이스가 연결 된 해당 hello 스위치 포트 toowhich 작동 되는지 확인 합니다. tootroubleshoot 네트워크 문제가 너무 이동[hello Get-netadapter cmdlet으로 문제를 해결](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet)합니다. |
| Toohello 인증 서비스를 연결 하지 못했습니다. |데이터 경로 오류 |hello URLthat 사용 tooauthenticate에 연결할 수 없습니다. 방화벽 규칙에 포함 hello StorSimple 장치에 지정 된 hello URL 패턴 있는지 확인 합니다. Azure 포털의 URL 패턴에 대 한 자세한 내용은 toohttps://aka.ms/ss-8000-network-reqs를 이동 합니다. Azure Government 클라우드를 사용 하는 경우 https://aka.ms/ss8000-gov-network-reqs의 toohello URL 패턴을 이동 합니다.|

### <a name="performance-alerts"></a>성능 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| hello 장치 로드 초과한 <*임계값*> 합니다. |예상된 응답 시간보다 느립니다. |장치는 입/출력 부하가 높은 상태에서 사용률을 보고합니다. 이 장치 toonot 작업을 인해 예상 대로 있습니다. Toohello 장치 연결 상태 tooanother 장치나는 더 이상 필요 없는 이동 될 수 있는 있는지 확인 하는 hello 작업을 검토 합니다.| StorSimple 서비스를 시작하지 못했습니다. |데이터 경로 오류 |Hello 문제가 계속 되 면 Microsoft 지원에 문의 합니다. |현재 상태를 hello, 너무 이동 및[사용 하 여 장치를 StorSimple 장치 관리자 서비스 toomonitor hello](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>보안 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| Microsoft Support 세션이 시작되었습니다. |타사가 지원 세션에 액세스했습니다. |이 액세스에 권한이 부여되었는지 확인하세요. 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요. |
| <*요소*>의 암호가 <*시간 길이*> 후에 만료됩니다. |암호 만료 날짜가 다가오고 있습니다. |만료되기 전에 암호를 변경합니다. |
| <*요소 ID*>에 대한 보안 구성 정보가 없습니다. | |이 볼륨 컨테이너와 연결 된 볼륨 hello 사용된 tooreplicate StorSimple 구성 될 수 없습니다. 데이터가 안전 하 게 저장 되어 tooensure, hello 볼륨 컨테이너와 hello 볼륨 컨테이너와 연결 된 모든 볼륨을 삭제 하는 것이 좋습니다. 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요. |
| <*요소 ID*>에 대한 로그인 시도가 <*숫자*>회 실패했습니다. |로그온 시도가 여러 번 실패했습니다. |잘못 된 암호로 tooconnect 시도 하는 권한 있는 사용자 또는 장치가 공격을 받고 수 있습니다.<ul><li>권한이 있는 사용자에게 문의하고 합법적인 출처에서 이러한 시도가 있었는지 확인합니다. Toosee 많은 수의 실패 한 로그인 시도 계속 진행 하면 원격 관리를 사용 하지 않도록 설정 하 고 네트워크 관리자에 게 문의 하십시오. 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요.</li><li>Snapshot 관리자 인스턴스가 hello 올바른 암호로 구성 되어 있는지 확인 합니다. 적절 한 조치를 수행한 후 hello 경고 페이지에서이 경고를 지우세요.</li></ul>자세한 내용은 이동 너무[만료 된 장치 암호 변경](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password)합니다. |
| Hello 서비스 데이터 암호화 키를 변경 하는 동안 하나 이상의 오류가 발생 했습니다. | |Hello 서비스 데이터 암호화 키를 변경 하는 동안 오류가 발생 했습니다. Hello 오류 상황을 해결 한 후 실행 hello `Invoke-HcsmServiceDataEncryptionKeyChange` 장치 tooupdate hello 서비스에서 hello StorSimple 용 Windows PowerShell 인터페이스에서에서 cmdlet. 문제가 지속되면 Microsoft 지원에 문의하세요. Hello 문제를 해결 한 후에 hello 경고 페이지에서이 경고를 지우세요. |

### <a name="support-package-alerts"></a>지원 패키지 경고

| 경고 텍스트 | 이벤트 | 자세한 내용 / 권장 작업 |
|:--- |:--- |:--- |
| 지원 패키지를 만들지 못했습니다. |StorSimple는 hello 패키지를 생성할 수 없습니다. |이 작업을 다시 시도하세요. Hello 문제가 지속 되 면 Microsoft 지원에 문의 합니다. Hello 문제를 해결 한 후에 hello 경고 페이지에서이 경고를 지우세요. |

## <a name="next-steps"></a>다음 단계

[StorSimple 오류 및 운영 장치 문제 해결](storsimple-troubleshoot-operational-device.md)에 대해 알아봅니다.

