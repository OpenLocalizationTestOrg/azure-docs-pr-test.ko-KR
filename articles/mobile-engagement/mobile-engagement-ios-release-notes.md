---
title: "aaaAzure Mobile Engagement iOS SDK 릴리스 정보 | Microsoft Docs"
description: "Azure Mobile Engagement용 iOS SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a>Azure Mobile Engagement iOS SDK 릴리스 정보

## <a name="410-07172017"></a>4.1.0 (07/17/2017)
* 백그라운드에서 지워진 배지를 수정했습니다.
* 기본 큐에서 호출되지 않는 API에 대한 XCode 9의 경고를 수정했습니다.
* 도달률 설문에서 메모리 누수를 해결했습니다.
* iOS 6.X에 대한 지원을 삭제했습니다. 적어도 있어야 응용 프로그램의이 버전 hello 배포 대상에서 시작 iOS 7입니다.

## <a name="401-12132016"></a>4.0.1 (12/13/2016)
* 백그라운드에서 로그 전달을 개선하였습니다.

## <a name="400-09122016"></a>4.0.0(09/12/2016)
* iOS 10 장치에서 알림이 작동하지 않는 문제를 해결했습니다.
* XCode 7은 더 이상 사용되지 않습니다.

## <a name="324-06302016"></a>3.2.4(2016년 6월 30일)
* 기술 로그 및 기타 로그 간 집계를 수정했습니다.

## <a name="323-06072016"></a>3.2.3(06/07/2016)
* 고정된 hello 버그 hello 백그라운드에서 앱이 때 배달 피드백 보고 되지 않습니다.
* 최적화 된 hello 기술 로그의 보내는 중입니다.

## <a name="322-04072016"></a>3.2.2(2016/04/07)
* 수정 된 버그를 toocrash 때로는 크게 HTTP 요청 취소 합니다.

## <a name="321-12112015"></a>3.2.1(2015/12/11)
* 새 응용 프로그램 인스턴스 딥 링크와 알림이 트리거될 때 고정된 hello 지연

## <a name="320-10082015"></a>3.2.0(2015/10/08)
* 제대로 작동 하는 hello SDK toomake에서 Bitcode 활성화 **Xcode 7**합니다.
* 수정 된 버그 관련 tooin 앱 알림입니다.
* 앱에서 알림을 hello 배터리 부족 및 기타 이러한 시나리오의 경우 보다 안정적 수 있습니다.
* 타사 라이브러리에서 생성하는 추가 콘솔 로그를 제거했습니다.

## <a name="310-08262015"></a>3.1.0(08/26/2015)
* 타사 라이브러리와 iOS 9 호환성 버그를 수정합니다. 설문 조사 결과, 응용 프로그램 정보 또는 추가 데이터를 보내는 동안 충돌을 야기합니다.

## <a name="300-06192015"></a>3.0.0(2015/06/19)
* Mobile Engagement는 자동 푸시 알림을 사용합니다.
* iOS 4.X에 대한 지원을 삭제했습니다. 적어도 있어야 응용 프로그램의이 버전 hello 배포 대상에서 시작 iOS 6입니다.

## <a name="220-05212015"></a>2.2.0(05/21/2015)
* 장치에 대 한 hello Mobile Engagement 장치 id < iOS 6은 이제 설치 중에 생성 된 GUID를 기반 합니다.

## <a name="210-04242015"></a>2.1.0(2015/04/24)
* Swift 호환성을 추가하였습니다.
* 알림을 클릭할 때 URL이 이제 hello 동작 hello 응용 프로그램을 연 후 오른쪽을 실행 합니다.
* SDK 패키지에 누락된 헤더 파일을 추가하였습니다.
* Hello Mobile Engagement 크래시 보고서가 사용 되지 않을 때 문제를 해결 합니다.

## <a name="200-02172015"></a>2.0.0(2015/02/17)
* Azure Mobile Engagement의 최초 릴리스입니다.
* appId/sdkKey 구성이 연결 문자열 구성으로 바뀌었습니다.
* API toosend를 제거 하 고 임의의 XMPP 엔터티에서 임의의 XMPP 메시지를 수신 합니다.
* API toosend를 제거 하 고 장치 간에 메시지를 수신 합니다.
* 보안이 개선되었습니다.
* SmartAd 추적 기능이 제거되었습니다.
