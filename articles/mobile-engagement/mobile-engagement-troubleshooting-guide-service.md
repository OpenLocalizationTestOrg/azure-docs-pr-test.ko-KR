---
title: "aaaAzure Mobile Engagement 문제 해결 가이드-서비스"
description: "Azure Mobile Engagement에 대한 문제 해결 가이드"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>서비스 문제에 대한 문제 해결 가이드
hello 다음은 Azure Mobile Engagement 실행 하는 방법에 발생할 수 있는 관련 문제입니다.

## <a name="service-outages"></a>서비스 중단
### <a name="issue"></a>문제
* Azure Mobile Engagement 서비스 중단 때문일 toobe 나타나는 문제가 있습니다.

### <a name="causes"></a>원인
* Azure Mobile Engagement 서비스 중단 때문일 toobe 표시 하는 문제는 여러 다른 문제로 인해 발생할 수 있습니다.
  * 원래 Azure Mobile Engagement의 구조적 tooall를 표시 하는 격리 된 문제
  * 서버 중단으로 인한 알려진 문제(서버 상태에 항상 표시되지는 않음):
  * 지연, 대상 지정 오류, 배지 업데이트 문제, 수집, 푸시 작동을 중지 하는 통계 중지 예약, API의 작동을 중지, 새로운 앱 또는 사용자가 만들 수 없습니다, DNS 오류 및 시간 초과 오류 장치에서 hello UI, API 또는 앱에서.
  * 클라우드 종속성 작동 중단 [Azure 서비스 상태](http://status.azure.com/)
  * PNS(푸시 알림 서비스) 종속성 작동 중단
  * 앱 스토어 작동 중단

1) 구조적 hello 문제가 발생 한 경우 tootest toosee hello 동일한 다른 함수를 테스트할 수 있습니다.

* Azure Mobile Engagement 통합 응용 프로그램
* 테스트 장치
* 테스트 장치 OS 버전
* 캠페인
* 관리자 사용자 계정
* 브라우저(IE, Firefox, Chrome 등)
* 컴퓨터

2) tootest hello 문제만 영향을 주는 hello UI 또는 hello API의 경우:

* 동일 두 hello Azure Mobile Engagement UI에서에서 작동 하 고 Azure Mobile Engagement API hello hello를 테스트 합니다.

3) tootest 휴대폰 네트워크와 hello 문제가 발생 한 경우:

* 연결 된 toohello 휴대폰 3g 네트워크를 통해 연결 되어 있는 동안 및 WIFI를 통해 인터넷 하는 동안 테스트 합니다.
* 방화벽에서 차단 하지 않는지 hello Azure Mobile Engagement IP 주소 또는 포트를 확인 합니다.

4) tootest 장치와 함께 hello 문제가 발생 한 경우:

* 장치는 다른 Azure Mobile Engagement 통합 앱 수 tooconnect tooAzure Mobile Engagement를 테스트 합니다.
* Hello Azure Mobile Engagement UI에서에서 볼 수 있는 휴대폰에서 이벤트, 작업, 및 작동 중단을 생성할 수 있는 테스트 합니다. 
* Id입니다. 해당 장치에 따라 hello Azure Mobile Engagement UI tooyour 장치에서 푸시 알림을 보낼 수 있는 경우에 테스트 

5) tootest 응용 프로그램과 함께 hello 문제가 발생 한 경우:

* 실제 장치 대신 에뮬레이터에서 응용 프로그램을 설치하고 테스트합니다.

6) os hello 문제가 발생 한 경우 tootest tooend 사용자 SDK 업그레이드 tooresolve 해야 하는 장치를 업그레이드 합니다.

* 다른 버전의 운영 체제 hello와 서로 다른 장치에서 응용 프로그램을 테스트 합니다.
* Hello hello SDK의 최신 버전을 사용 하 고 있는지 확인 합니다.

## <a name="connectivity-and-incorrect-information-issues"></a>연결 및 잘못된 정보 문제
### <a name="issue"></a>문제
* Azure Mobile Engagement UI hello 하는 문제에 로그인 합니다.
* Hello로 Azure Mobile Engagement API의 연결 오류입니다.
* Hello Device API를 통해 응용 프로그램 정보 태그를 업로드 하는 중에 문제가 있습니다.
* Azure Mobile Engagement에서 로그나 내보낸 데이터를 다운로드하는 데 문제가 있습니다.
* Hello Azure Mobile Engagement UI에에서 표시 된 잘못 된 정보입니다.
* Azure Mobile Engagement 로그에 잘못된 정보가 표시됩니다.

### <a name="causes"></a>원인
* 사용자 계정에 충분 한 사용 권한을 tooperform hello 작업을 확인 합니다.
* Hello 이러한 문제는 격리 된 tooone 컴퓨터 또는 로컬 네트워크를 확인 합니다.
* 해당 hello Azure Mobile Engagement 서비스에 보고 된 중단 없는 있는지 확인 합니다.
* 앱 정보 태그 파일이 다음 규칙을 모두 따르는지 확인합니다.
  * 사용에만 UTF8 문자 세트 hello (hello ANSI 문자 집합이 지원 되지 않음).
  * 쉼표를 사용 하 여 "," hello 구분 기호 문자로 (쉼표에서 서비스 요청 toorequest toochange hello.csv 구분 문자를 열 수 세미콜론 같은 tooanother 문자 "," ";").
  * 부울 값 "true"와 "false"에 소문자만 사용합니다.
  * 35MB의 hello 최대 파일 크기 보다 작은 파일을 사용 합니다.

