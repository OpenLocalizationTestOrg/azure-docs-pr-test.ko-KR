---
title: "Microsoft Azure StorSimple 가상 배열에서 aaaInstall 업데이트 | Microsoft Docs"
description: "Hello 포털 및 핫픽스 메서드를 사용 하 여 toouse hello StorSimple 가상 배열 웹 UI tooapply을 업데이트 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7424abc7e46d4f08b4eae1194642b263f32c4318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a>StorSimple 가상 배열에 업데이트 설치 - Azure Portal

## <a name="overview"></a>개요

이 문서에서는 hello 로컬 웹 UI 통해 및 hello Azure 포털을 통해 StorSimple 가상 배열에 hello 단계 필요한 tooinstall 업데이트를 설명 합니다. 필요한 소프트웨어 업데이트 또는 핫픽스 tookeep tooapply StorSimple 가상 배열 최신 상태입니다. 

업데이트 또는 핫픽스를 설치하면 장치가 다시 시작됩니다. 주어진는 hello StorSimple 가상 배열은 단일 노드에 장치, 진행 중인 모든 I/O 중단 된와 장치에 가동 중지 시간이 발생 합니다. 

업데이트를 적용 하기 전에 수행한 hello 볼륨 또는 공유 hello에 오프 라인에서 먼저 호스트 및 다음 장치를 hello 하는 것이 좋습니다. 이렇게 하면 데이터 손상 가능성이 최소화됩니다.

> [!IMPORTANT]
> 업데이트 0.1 또는 GA 소프트웨어 버전을 실행 하는 경우에 hello 로컬 웹 UI tooinstall 업데이트 0.3 통해 hello 핫픽스 메서드를 사용 해야 합니다. 0.2 업데이트를 실행 하는 경우에 hello Azure 클래식 포털을 통해 hello 업데이트를 설치 하는 것이 좋습니다.
 

## <a name="use-hello-local-web-ui"></a>Hello 로컬 웹 UI를 사용 하 여

Hello 로컬 웹 UI를 사용 하는 데는 두 단계가 있습니다.

* Hello 업데이트 또는 hello 핫픽스를 다운로드 합니다.
* Hello 업데이트 또는 hello 핫픽스 설치

### <a name="download-hello-update-or-hello-hotfix"></a>Hello 업데이트 또는 hello 핫픽스를 다운로드 합니다.

Hello hello Microsoft Update 카탈로그에서에서 단계 toodownload hello 소프트웨어 업데이트를 다음을 수행 합니다.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload hello 업데이트나 hello 핫픽스

1. Internet Explorer를 시작 하 고 탐색 너무[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)합니다.

2. Microsoft Update 카탈로그 hello를 사용 하 여이 컴퓨터에 처음으로 이면 클릭 **설치** 때 메시지 표시 tooinstall hello Microsoft Update 카탈로그 추가 기능입니다.

3. Hello 기술 자료 (KB) 번호를 입력 hello Microsoft Update 카탈로그의 hello 검색 상자에 원하는 toodownload hello 핫픽스의 합니다. 업데이트 0.3의 경우 **3182061**을 입력하고 **검색**을 클릭합니다.
   
    hello 핫픽스 목록이 표시 되 면 예를 들어 **StorSimple 가상 배열 업데이트 0.3**합니다.
   
    ![카탈로그 검색](./media/storsimple-virtual-array-install-update/download1.png)

4. **추가**를 클릭합니다. hello 업데이트 toohello 바구니를 추가 됩니다.

5. **바구니 보기**를 클릭합니다.

6. **다운로드**를 클릭합니다. 지정 하거나 **찾아보기** tooa 로컬 위치 hello tooappear 다운로드 합니다. hello 업데이트는 다운로드 toohello 위치를 지정 하 고 hello 업데이트로 이름과 같은 이름을 hello로 하위 폴더에 배치 합니다. hello 폴더 hello 장치에서 연결할 수 있는 tooa 복사한 네트워크 공유 될 수도 있습니다.

7. 폴더를 복사 하는 hello open, Microsoft Update 독립 실행형 패키지 파일이 `WindowsTH-KB3011067-x64`합니다. 이 파일이 사용 되는 tooinstall hello 업데이트나 핫픽스를 설치 합니다.

### <a name="install-hello-update-or-hello-hotfix"></a>Hello 업데이트 또는 hello 핫픽스 설치

이전 toohello 업데이트 또는 핫픽스 설치 hello 업데이트가 설치 되어 있거나 호스트에서 로컬로 hello 핫픽스 다운로드 하 고 있는지 또는 네트워크 공유를 통해 액세스할 수 있도록 합니다. 

GA를 실행 하는 장치에이 메서드가 tooinstall 업데이트를 사용 하거나 0.1 소프트웨어 버전으로 업데이트 합니다. 이 프로시저는 2 분 toocomplete 보다 작습니다. Hello 다음이 수행 단계 tooinstall hello 업데이트나 핫픽스를 설치 합니다.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall hello 업데이트나 hello 핫픽스

1. Hello 로컬 웹 UI에서에서 이동 너무**유지 관리** > **소프트웨어 업데이트**합니다.
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update/update1m.png)

2. **업데이트 파일 경로**, hello 업데이트에 대 한 hello 파일 이름을 입력 또는 핫픽스를 환영 합니다. 네트워크 공유에 배치 하는 경우에 toohello 업데이트 또는 핫픽스 설치 파일을 찾아볼 수 있습니다. **Apply**를 클릭합니다.
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update/update2m.png)

3. 경고가 표시됩니다. 이 지정 된 단일 노드 장치, hello 업데이트를 적용 하 고 hello 장치가 다시 시작 될 동안 가동 중지 후입니다. Hello 확인 아이콘을 클릭 합니다.
   
   ![장치 업데이트](./media/storsimple-virtual-array-install-update/update3m.png)

4. hello 업데이트를 시작합니다. Hello 장치를 업데이트 한 후 다시 시작 됩니다. hello 로컬 UI 액세스할 수 없는 경우이 기간 동안
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update/update5m.png)

5. Toohello 취해집니다 hello를 다시 시작이 완료 된 후 **로그인** 페이지. hello 장치 소프트웨어 hello 로컬 웹 UI에서에서 업데이트 된 tooverify 너무 이동**유지 관리** > **소프트웨어 업데이트**합니다. 표시 되는 hello 소프트웨어 버전 이어야 합니다 **10.0.0.0.0.10288.0** 업데이트 0.3에 대 한 합니다.
   
   > [!NOTE]
   > Hello 로컬 웹 UI에서에서 약간 다른 방식으로 hello 소프트웨어 버전을 보고 하 고 hello Azure 포털입니다. 예를 들어 로컬 웹 UI 보고서 hello **10.0.0.0.0.10288** Azure 포털 보고서 hello 및 **10.0.10288.0** hello에 대 한 동일한 버전입니다.
   
    ![장치 업데이트](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여

0.2 업데이트를 실행 하는 경우에 hello Azure 포털을 통해 업데이트를 설치 하는 것이 좋습니다. hello 포털 프로시저 hello 사용자 tooscan 필요 하 고, 다운로드 및 다음 hello 업데이트를 설치 합니다. 이 프로시저는 약 7 분 toocomplete. Hello 다음이 수행 단계 tooinstall hello 업데이트나 핫픽스를 설치 합니다.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

Hello 후 설치가 완료 (통해 알 수 있듯이 100%로 작업 상태), 이동 tooyour StorSimple 장치 관리자 서비스 되었습니다. 선택 **장치** 다음 선택 하 고 tooupdate 장치 toothis 연결 된 서비스의 hello 목록에서 원하는 hello 장치를 클릭 합니다. Hello에 **설정** 블레이드에서 너무 이동**관리** 선택한 섹션 **장치 업데이트**합니다. 표시 되는 hello 소프트웨어 버전 이어야 합니다 **10.0.10288.0**합니다.


## <a name="next-steps"></a>다음 단계

[StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)에 대해 자세히 알아봅니다.

