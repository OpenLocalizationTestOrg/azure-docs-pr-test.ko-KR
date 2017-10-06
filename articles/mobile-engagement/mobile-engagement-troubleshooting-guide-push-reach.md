---
title: "Mobile Engagement 문제 해결 가이드-aaaAzure 밀어넣기/범위"
description: "Azure Mobile Engagement에서 사용자 상호 작용 및 알림 문제 해결"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>푸시 및 도달률 문제에 대한 문제 해결 가이드
hello 다음은 Azure Mobile Engagement tooyour 사용자 정보를 보내는 방법에 발생할 수 있는 관련 문제입니다.

## <a name="push-failures"></a>푸시 오류
### <a name="issue"></a>문제
* 푸시가 앱 내부 또는 외부나 두 위치에서 모두 작동하지 않습니다.

### <a name="causes"></a>원인
* 여러 번 푸시 오류는 Azure Mobile Engagement, 범위, 또는 Azure Mobile Engagement의 고급 기능도 통합 되지 않은 경우 올바르게 되었다면 또는 하다 hello SDK toofix 새로운 운영 체제 또는 장치 플랫폼의 알려진된 문제로 필요 합니다.
* 문제가 있습니다. 앱에서 또는 앱의 문제는 앱에서 푸시만 하 고는 응용 프로그램의 푸시 toodetermine를 테스트 합니다.
* 어떤 추가 오류 정보를 사용할 수 있는 문제 해결 단계 toosee로 hello UI와 API hello에서 테스트할 두 곳입니다.
* 앱 외부 푸시 Azure Mobile Engagement와 Reach SDK hello에 통합 되어 하지 않으면 작동 하지 않습니다.
* 인증서가 유효하지 않거나 프로덕션/개발 버전을 올바르게 사용하고 있으면 푸시가 작동하지 않습니다(iOS에만 해당). (**참고:** "app" 부족 푸시 알림을 배달할 수 없는 tooiOS, 두 hello 개발 (DEV) 있으며 같은 hello에 (PROD) 프로덕션 버전 응용 프로그램의 설치 하는 경우 장치에 연결 하는 보안 토큰 hello 이후 인증서로 Apple에 의해 무효화 될 수 있습니다. tooresolve이이 문제를 hello 개발자와 응용 프로그램의 프로덕션 버전을 제거 하 고 장치에서 하나의 버전 hello만 다시 설치 합니다.)
* 앱 외부 푸시 횟수 (iOS 표시 Android 보다 적은 정보 네이티브 푸시에 사용할 수 없는지 여부 장치 API 누름 stats에 UI hello 보다 더 많은 정보를 제공할 수 hello) 다양 한 플랫폼에서 다르게 처리 됩니다.
* 고객이 OS(iOS 및 Android) 수준에서 앱 외부 푸시를 차단할 수 있습니다.
* 앱 외부 푸시를 제대로 통합 되지 않지만 hello API에서에서 자동으로 실패할 경우 hello Azure Mobile Engagement UI에서에서 비활성화 된 것으로 표시 됩니다.
* 응용 프로그램에서 푸시 Azure Mobile Engagement와 Reach SDK hello에 통합 되어 하지 않으면 작동 하지 않습니다.
* GCM 및 ADM 푸시 Azure Mobile Engagement 및 특정 서버 hello hello SDK (Android에만 해당)에 통합 되어 하지 않으면 작동 하지 않습니다.
* 응용 프로그램 시작 및 푸시 해야 하는 응용 프로그램의 테스트 별도로 toodetermine 밀어넣기 또는 Reach 문제가 경우.
* 앱 푸시에서 받은 열려 toobe 수 해당 hello 앱이 필요 합니다.
* 앱에 푸시는 경우가 설치 toobe 옵트인 또는 옵트아웃 앱 정보 태그에 의해 필터링 합니다.
* 사용자 지정 범주를 사용 하 여 Reach toodisplay 앱에 알림에서, toofollow hello 올바른의 수명 주기 hello 알림이 필요. 그렇지 않으면 hello 알림을 지울 수 없습니다 경우 때 hello 사용자 해제 합니다.
* 캠페인 종료 날짜 없음로 시작 하 여 장치 앱 알림 (에서 hello)를 받는 되었지만 아직 표시 되지 않는 경우 hello 사용자 여전히 hello 알림 hello 다음 때 받습니다 hello 앱에 로그인 할 hello 캠페인을 수동으로 종료 한 경우에 합니다.
* Hello 푸시 API로 문제에 대해 실제로 않도록 hello Reach API 대신 toouse hello 푸시 API (이후 hello Reach API는 더 자주 사용 됨)와 혼동 hello "페이로드" 및 "알림" 매개 변수 없는 확인 합니다.
* 문제의 가능한 원인으로 WIFI 및 3g tooeliminate hello 네트워크 연결을 통해 연결 된 장치 둘 다로 푸시 캠페인을 테스트 하십시오.

## <a name="push-testing"></a>푸시 테스트
### <a name="issue"></a>문제
* 푸시 id입니다. 장치에 따라 tooa 특정 장치를 보낼 수 있습니다.

### <a name="causes"></a>원인
* 테스트 장치는 각 플랫폼에 대해 다르게 설정 하지만 hello 포털에서 장치 ID를 찾아 테스트 장치에서 응용 프로그램에서 이벤트를 발생 해야 작동 toofind 모든 플랫폼에 대 한 장치 ID입니다.
* 테스트 장치는 IDFA와 IDFV에서 다르게 작동합니다(iOS에만 해당).

## <a name="push-customization"></a>푸시 사용자 지정
### <a name="issue"></a>문제
* 배지, 벨소리, 진동, 사진 등의 고급 푸시 콘텐츠 항목이 작동하지 않습니다.
* 푸시에서 링크 (앱, 앱, tooa 웹 사이트, 응용 프로그램에서 tooa 위치) 외부 작동 하지 않습니다.
* 밀어넣기 되지 않은 푸시 통계 표시 전송 tooas 예상 대로 많은 사람들이 (너무 많거나 충분 하지 않습니다).
* 중복 푸시가 두 번 수신됩니다.
* 직접 작성한 프로덕션 앱이나 개발 앱이 설치된 Azure Mobile Engagement 푸시용 테스트 장치를 등록할 수 없습니다.

### <a name="causes"></a>원인
* 또한 "categories" (Android에만 해당) 되어야 하는 응용 프로그램에서 toolink tooa 특정 위치입니다.
* 전체 연결 구성표 tooredirect 사용자 tooan 푸시 알림을 클릭 한 후 대체 위치 toobe에 만들어지며 Mobile Engagement가 아니라 응용 프로그램 및 hello 장치 운영 체제에서 직접 관리 해야 합니다. (**참고:** 앱에서 알림을 연결할 수 없습니다 직접 iOS 사용 하 여 응용 프로그램 위치의 tooin Android 수 있습니다.)
* 외부 이미지 서버 해야 toobe 수 toouse HTTP "GET" 및 "HEAD" 큰 그림 푸시 toowork (Android에만 해당)에 대 한 합니다.
* 코드에서 hello 키보드를 열 때 hello Azure Mobile Engagement 에이전트를 사용 하지 않도록 설정 하 고 수 hello 키보드 내용이 영향을 주지 hello 모양의 있도록 hello 키보드 닫히면 hello Azure Mobile Engagement 에이전트를 다시 활성화 코드 프로그램 알림 (iOS에만 해당)입니다.
* 일부 항목은 테스트 시뮬레이션에서 작동하지 않으며 실제 캠페인(배지, 벨소리, 진동, 사진 등)에서만 작동합니다.
* 너무 hello 단추를 사용 하는 경우 데이터는 기록 되지 서버 쪽 푸시 "test"입니다. 데이터는 실제 푸시 캠페인에 대해서만 기록됩니다.
* toohelp 문제를 격리 하에서는으로 문제 해결: 테스트, 시뮬레이션 및 구성 파일은 각각 약간 다르게 작동 하므로 실제 캠페인입니다.
* hello에 "app" 및 "항상" 캠페인은 예약 된 toorun 시간의 길이 영향을 줄 수 배달 숫자 캠페인만 전달 됩니다 toousers hello 캠페인 실행 되는 동안 "app"에 있는 (및 해당 장치 설정을 사용자 설정 tooreceive 이후 알림 "out of app")입니다.
* Android 및 iOS 핸들 응용 프로그램 알림을 사용 하 여 방법 어려운 toodirectly 차이점 hello hello Android 및 iOS 버전의 응용 프로그램 간의 푸시 통계를 비교 합니다. Android는 iOS보다 자세한 OS 수준 알림 정보를 제공합니다. Android에는 iOS hello 알림을 클릭 하지 않는 한이 정보를 보고 하지 않습니다 되지만 기본 알림을 수신를 클릭 하면 또는 hello 알림 센터에서는 삭제 하는 경우 보고 합니다. 
* "푸시" 다르면 시간 차이 대 한 "배달" 번호 캠페인에 도달 하는 보다는 "app" 및 "app" 부족 알림 다르게 계산 된 것 보다는 주된 이유 hello 합니다. Mobile Engagement에서 알림을 처리 하는 "app"에 있지만 "app" 부족 알림 hello 알림 센터 장치 OS hello에 의해 처리 됩니다.

## <a name="push-targeting"></a>푸시 대상 지정
### <a name="issue"></a>문제
* 기본 제공 대상 지정 기능이 정상적으로 작동하지 않습니다.
* 앱 정보 태그 대상 지정 기능이 정상적으로 작동하지 않습니다.
* 지리적 위치 대상 지정 기능이 정상적으로 작동하지 않습니다.
* 언어 옵션이 정상적으로 작동하지 않습니다.

### <a name="causes"></a>원인
* Azure Mobile Engagement UI hello 또는 API를 통해 응용 프로그램 정보 태그를 업로드 하 고 있는지 확인 합니다.
* 조정 hello 푸시 속도 또는 푸시 할당량 hello 응용 프로그램 수준 또는 제한 hello audience hello 캠페인 수준에서 다른 대상 조건을 충족 하는 경우에 특정 푸시를 받지 못하도록 사용자를 방지할 수 있습니다. 
* "언어"를 설정하는 것은 국가나 로캘에 따라 대상을 지정하는 것과는 다르며, 휴대폰 위치나 GPS 위치에 따라 지리적 위치를 기준으로 대상을 지정하는 것과도 다릅니다.
* hello 메시지 hello "기본 language"에 지정한 hello 대체 언어의 tooone 설정 자신의 장치를 설치 하지 않은 tooany 고객을 전송 됩니다.

## <a name="push-scheduling"></a>푸시 예약
### <a name="issue"></a>문제
* 푸시 예약이 정상적으로 작동하지 않습니다(푸시가 너무 빨리 전송되거나 전송이 지연됨).

### <a name="causes"></a>원인
* 표준 시간대 hello 최종 사용자 표준 시간대를 사용 하는 경우에 특히 일정 관리, 문제를 수 있습니다.
* 고급 푸시 기능을 사용하는 경우 푸시가 지연될 수 있습니다.
* Azure Mobile Engagement 푸시를 보내기 전에 toorequest hello 전화 실시간으로 데이터를 가질 수 있으므로 푸시 전화 설정 (대신 응용 프로그램 정보 태그) 지연 시킬 수에 따라 대상으로 지정 합니다.
* 종료 날짜 없이 만든 캠페인 hello 장치에서 hello 푸시를 로컬로 저장 하 고 hello 앱 hello 캠페인 수동으로 종료 될 경우에 열릴 때 hello 표시 합니다.
* 둘 이상의 캠페인 시작 hello에서 같은 시간 걸릴 수 있습니다 더 긴 시간 tooscan 사용자 기반 (4의 최대 한 번에 tooonly 시작 하나의 캠페인 시도, 이전 사용자를 검색 한 toobe 없는 있도록 tooyour 활성 사용자만을 대상).
* Toosend 해야는 hello "대상 그룹 무시, 푸시가 전송 되지 hello API 통해 toousers" 옵션 사용 Reach 캠페인의 hello "는 캠페인" 섹션에 hello 캠페인은 자동으로 보내지 않습니다 hello Reach API를 통해 수동으로 합니다.
* 사용자 지정 범주를 사용 하 여 Reach toodisplay 앱에 알림에서, toofollow hello 올바른의 수명 주기 알림 필요. 그렇지 않으면 hello 알림을 지울 수 없습니다 경우 때 hello 사용자 해제 합니다.

