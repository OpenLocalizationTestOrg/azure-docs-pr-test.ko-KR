---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>릴리스 정보

## <a name="431-07172017"></a>4.3.1 (07/17/2017)
* 호출할 때 거의 발생할 수 있는 충돌을 해결 `EngagementAgentUtils.isInDedicatedEngagementProcess`, hello에서 사용 되는 `EngagementApplication` 클래스입니다.

## <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8 지원 (이전 버전의 hello SDK는 Android 8에서 작동 하지 것입니다).
* 지원 라이브러리에 대한 종속성이 더 이상 없습니다.
* `EngagementFragmentActivity` 클래스를 제거합니다.
* 기한 너무[배경 실행 제한](https://developer.android.com/preview/features/background.html) Android 8에서 백그라운드로 로그 지연 될 수 있습니다 hello 사용자 hello 장치 상호 작용할 때까지, 푸시 캠페인에 영향을 미치게 됩니다이 **Delivered** 및 **시스템 알림 표시** 통계 hello 장치 중지 된 경우 지연 되 고 (hello 알림이 표시 됩니다, 링 되며 문제 없이 실시간으로 진동).
* 기한 너무[배경 위치 제한](https://developer.android.com/preview/features/background-location-limits.html), Android 8 hello 실시간으로 위치 백그라운드에서 자주 업데이트 되지 것입니다.

## <a name="424-03302017"></a>4.2.4 (03/30/2017)
* 앱 내 알림이 Android 7 toobe에서 텍스트 색 hello 동일 이전 Android 버전으로 수정 합니다.

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* 더 이상 WIFI 잠금은 없습니다.
* Init 이전에 getDeviceId를 호출할 경우 교착 상태를 해결합니다.(4.2.0에 유입된 버그)

## <a name="422-05172016"></a>4.2.2(2016/05/17)
* 안정성 향상

## <a name="421-05102016"></a>4.2.1(2016/05/10)
* 보안: 웹 보기 로컬 파일 액세스를 비활성화합니다.
* 보안: 사용되지 않고 보호되지 않는 `PreferenceActivity` 클래스를 확장하는 `EngagementPreferenceActivity` 클래스를 제거합니다.
* 보안: 활동은 이제 reach 문서화 toouse `exported="false"`, 이전 SDK 버전에도이 플래그를 사용할 수 있습니다.

## <a name="420-03112016"></a>4.2.0(2016/03/11)
* hello SDK는 이제 MIT 따라 사용이 허가 됩니다.
* SDK 초기화 시에 사용자 지정 장치 식별자를 지정할 수 있습니다.

## <a name="415-02012016"></a>4.1.5(2016/02/01)
* 안정성 향상

## <a name="414-01262016"></a>4.1.4(2016/01/26)
* 안정성 향상

## <a name="413-1292015"></a>4.1.3(2015/12/9)
* 안정성 향상

## <a name="412-11252015"></a>4.1.2(2015/11/25)
* 안정성 향상

## <a name="411-11042015"></a>4.1.1(2015/11/04)
* 안정성 향상

## <a name="410-08252015"></a>4.1.0(08/25/2015)
* Android M에 대한 새 권한 모델을 다룹니다.
* `AndroidManifest.xml`을 사용하는 대신 이제 런타임 시 위치 기능을 구성할 수 있습니다.
* 사용 권한 버그 수정: `ACCESS_FINE_LOCATION`을 사용하는 경우 `ACCESS_COARSE_LOCATION`이 더 이상 필요하지 않습니다.
* 안정성 향상

## <a name="400-07062015"></a>4.0.0(07/06/2015)
* 내부 프로토콜 toomake 분석 워크 로드와 푸시 안정적 수를 변경합니다.
* 네이티브 푸시 GCM/ADM ()는 이제에 사용 앱 알림에서 때문에 모든 유형의 푸시 캠페인에 대 한 hello 네이티브 푸시 자격 증명을 구성 해야 합니다.
* 큰 그림 알림을 수정합니다. 푸시된 후 10초만 표시되었습니다.
* 웹 보기의 버그 수정: 링크를 클릭 하면 기본 작업 URL hello 마찬가지로 실행 되었습니다.
* 드문 충돌 해결 toolocal 저장소 관리와 관련 된 합니다.
* 동적 구성 문자열 관리를 수정합니다.
* EULA를 업데이트합니다.

## <a name="300-02172015"></a>3.0.0(2015/02/17)
* Azure Mobile Engagement의 최초 릴리스입니다.
* appId 구성이 연결 문자열 구성으로 대체됩니다.
* API toosend를 제거 하 고 임의의 XMPP 엔터티에서 임의의 XMPP 메시지를 수신 합니다.
* API toosend를 제거 하 고 장치 간에 메시지를 수신 합니다.
* 보안이 개선되었습니다.
* Google Play 및 SmartAd 추적을 제거했습니다.

