---
title: "aaaStorSimple 가상 배열 웹 UI 관리 | Microsoft Docs"
description: "Hello StorSimple 가상 배열 웹 UI 통해 tooperform 기본 장치 관리 작업 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a>Hello 웹 UI tooadminister StorSimple 가상 배열 사용
![설정 프로세스 흐름](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a>개요
이 문서의 자습서 hello toohello Microsoft Azure StorSimple 가상 배열 (라고도 hello StorSimple 온-프레미스 가상 장치) 실행 중인 2016 년 3 월 GA (일반 공급) 릴리스를 적용합니다. 이 문서는 hello 복잡 한 워크플로 및 hello StorSimple 가상 배열에서 수행할 수 있는 관리 작업의 일부를 설명 합니다. 관리할 수 있습니다 (참조 tooas hello 포털 UI) UI hello StorSimple Manager 서비스를 사용 하 여 StorSimple 가상 배열 hello 및 hello hello 장치에 대 한 로컬 웹 UI입니다. 본이 문서 hello 작업에서는 hello 웹 UI를 사용 하 여 수행할 수 있습니다.

이 문서에는 자습서를 따라 hello 포함 됩니다.

* Hello 서비스 데이터 암호화 키 가져오기
* 웹 UI 설정 오류 해결
* 로그 패키지 생성
* 장치 종료 또는 다시 시작

## <a name="get-hello-service-data-encryption-key"></a>Hello 서비스 데이터 암호화 키 가져오기
서비스 데이터 암호화 키는 StorSimple Manager 서비스 hello로 첫 번째 장치를 등록할 때 생성 됩니다. 이 키는 다음 hello 서비스 등록 키 tooregister 추가 장치를 StorSimple Manager 서비스 hello에 필요 합니다.

서비스 데이터 암호화 키를 분실 한 경우 및 tooretrieve 필요를 hello 다음이 수행 단계 hello 로컬 웹 UI hello 장치에서에서 서비스로 등록 합니다.

#### <a name="tooget-hello-service-data-encryption-key"></a>tooget hello 서비스 데이터 암호화 키
1. Toohello 로컬 웹 UI를 연결 합니다. 너무 이동**구성** > **클라우드 설정**합니다.
2. Hello hello 페이지의 아래쪽에 있는 클릭 **Get 서비스 데이터 암호화 키**합니다. 키가 표시됩니다. 이 키를 복사하여 저장합니다.
   
    ![서비스 데이터 암호화 키 가져오기 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a>웹 UI 설정 오류 해결
경우에 따라 hello 로컬 웹 UI 통해 hello 장치를 구성 오류에 실행할 수 있습니다. toodiagnose 이러한 오류를 해결 하 고, hello 진단 테스트를 실행할 수 있습니다.

#### <a name="toorun-hello-diagnostic-tests"></a>toorun hello 진단 테스트
1. Hello 로컬 웹 UI에서에서 이동 너무**문제 해결** > **진단 테스트**합니다.
   
    ![진단 실행 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. Hello hello 페이지의 아래쪽에 있는 클릭 **진단 테스트 실행**합니다. 그러면 시작 테스트 toodiagnose 모든 관련 문제를 네트워크, 장치, 웹 프록시, 시간 또는 클라우드 설정 합니다. 알려 해당 hello 장치에서 테스트를 실행 합니다.
3. Hello 테스트를 완료 한 후 hello 결과가 표시 됩니다. hello 다음 예제에서는 진단 테스트의 hello 결과 Note hello 웹 프록시 설정이이 장치에 대해 구성 되지 않은 하 고 따라서 hello 웹 프록시 테스트 실행 되지 않았습니다. 네트워크 설정, DNS 서버에 대 한 다른 테스트 모두 hello 및 시간 설정에 성공 했습니다.
   
    ![진단 실행 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a>로그 패키지 생성
로그 패키지 장치 문제 해결에 Microsoft 기술 지원 서비스를 지원할 수 있는 모든 hello 관련 로그로 구성 됩니다. 이 릴리스에서 hello 로컬 웹 UI 통해 로그 패키지를 생성할 수 있습니다.

#### <a name="toogenerate-hello-log-package"></a>toogenerate hello 로그 패키지
1. Hello 로컬 웹 UI에서에서 이동 너무**문제 해결** > **시스템 로그**합니다.
   
    ![로그 패키지 생성 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. Hello hello 페이지의 아래쪽에 있는 클릭 **로그 패키지 만들기**합니다. Hello 시스템 로그의 패키지 생성 됩니다. 이 작업에 몇 분 정도가 소요됩니다.
   
    ![로그 패키지 생성 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    Hello 패키지가 성공적으로 만들어지면 tooindicate hello 시간 및 날짜 hello 패키지를 만들 때 hello 페이지는 업데이트 후 알림이 표시 됩니다.
   
    ![로그 패키지 생성 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. **로그 패키지 다운로드**를 클릭합니다. 압축된 패키지가 시스템에 다운로드됩니다.
   
    ![로그 패키지 생성 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. Hello 로그 다운로드 한 패키지를 압축 해제 하 고 hello 시스템 로그 파일을 볼 수 있습니다.

## <a name="shut-down-and-restart-your-device"></a>장치 종료 및 다시 시작
종료 하거나 hello 로컬 웹 UI를 사용 하 여 가상 장치를 다시 시작할 수 있습니다. 다시 시작 하 고 hello 호스트에서 hello 볼륨 또는 공유가 오프 라인 장치를 다음 hello 전에 하는 권장 합니다. 이렇게 하면 데이터 손상 가능성이 최소화됩니다. 

#### <a name="tooshut-down-your-virtual-device"></a>가상 장치 아래로 tooshut
1. Hello 로컬 웹 UI에서에서 이동 너무**유지 관리** > **전원 설정**합니다.
2. Hello hello 페이지의 아래쪽에 있는 클릭 **종료**합니다.
   
    ![장치 종료 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. Hello 장치 종료는는 작동 중단, 진행 중인 어떤 IO를 중단 한다는 경고 메시지가 나타납니다. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-ova-web-ui-admin/image3.png)으로 이동합니다.
   
    ![장치 종료 경고](./media/storsimple-ova-web-ui-admin/image37.png)
   
    알려 hello을 늘려 종료를 시작 했습니다.
   
    ![장치 종료 시작됨](./media/storsimple-ova-web-ui-admin/image38.png)
   
    hello 장치 종료 됩니다. 장치 toostart 원하는 통해 Hyper-v 관리자 hello toodo를 해야 합니다.

#### <a name="toorestart-your-virtual-device"></a>toorestart 가상 장치
1. Hello 로컬 웹 UI에서에서 이동 너무**유지 관리** > **전원 설정**합니다.
2. Hello hello 페이지의 아래쪽에 있는 클릭 **다시 시작**합니다.
   
    ![장치 다시 시작](./media/storsimple-ova-web-ui-admin/image36.png)
3. 재시작 hello 장치는 작동 중단 IOs 진행 중인 경우 중단 되었다는 경고가 표시 됩니다. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-ova-web-ui-admin/image3.png)으로 이동합니다.
   
    ![다시 시작 경고](./media/storsimple-ova-web-ui-admin/image37.png)
   
    알려 해당 hello 다시 시작 되었습니다.
   
    ![다시 시작 시작됨](./media/storsimple-ova-web-ui-admin/image39.png)
   
    Hello를 다시 시작이 진행 중에서 상태인 동안 hello 연결 toohello UI는 손실 됩니다. Hello UI를 주기적으로 새로 고쳐 hello를 다시 시작을 모니터링할 수 있습니다. 또는 hello Hyper-v 관리자를 통해 hello 장치 다시 시작 상태를 모니터링할 수 있습니다.

## <a name="next-steps"></a>다음 단계
너무 방법에 대해 알아봅니다[사용 하 여 장치를 StorSimple Manager 서비스 toomanage hello](storsimple-virtual-array-manager-service-administration.md)합니다.

