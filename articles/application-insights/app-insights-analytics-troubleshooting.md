---
title: "Azure Application Insights에서 분석 aaaTroubleshoot | Microsoft Docs"
description: "Application Insights Analytics에 문제가 있습니까? 여기에서 시작합니다. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Application Insights의 Analytics 문제 해결
[Application Insights Analytics](app-insights-analytics.md)에 문제가 있습니까? 여기에서 시작합니다. 분석은 Azure Application Insights의 hello 강력한 검색 도구입니다.

## <a name="limits"></a>제한
* 현재, 쿼리 결과가 제한 toojust를 과거 데이터의 주 동안 됩니다.
* 테스트 브라우저: Chrome, Edge 및 Internet Explorer 최신 버전.

## <a name="known-incompatible-browser-extensions"></a>알려진 호환되지 않는 브라우저 확장
* Ghostery

Hello 확장을 사용 하지 않도록 설정 하거나 다른 브라우저를 사용 합니다.

## <a name="e-a"></a> "예기치 않은 오류"
![예기치 않은 오류 화면](./media/app-insights-analytics-troubleshooting/010.png)

포털 런타임에 내부 오류 발생 – 처리되지 않은 예외.

* Hello 브라우저 캐시를 정리 합니다. 

## <a name="e-b"></a>403... tooreload를 시도 하십시오
![403... tooreload를 시도 하십시오](./media/app-insights-analytics-troubleshooting/020.png)

인증 관련 오류 발생(인증 또는 액세스 토크 생성 시). hello 포털 너무 브라우저 설정을 변경 하지 않고 복구 방법이 있을 수 있습니다.

* 확인 [제 3 자 쿠키가 활성화 되어](#cookies) hello 브라우저에서 합니다. 

## <a name="authentication"></a>403... 보안 영역 확인
![403... 보안 영역 확인](./media/app-insights-analytics-troubleshooting/030.png)

인증 관련 오류 발생(인증 또는 액세스 토크 생성 시). hello 포털 너무 브라우저 설정을 변경 하지 않고 복구 방법이 있을 수 있습니다.

1. 확인 [제 3 자 쿠키가 활성화 되어](#cookies) hello 브라우저에서 합니다. 
2. 즐겨찾기, 책갈피 또는 저장 된 링크 tooopen hello 분석 포털 사용 했나요? Hello 링크를 저장할 때 사용한 다른 자격 증명을 사용 하 여 서명?
3. 비공개/시크릿 브라우저 창을 사용하세요(모든 해당 창을 닫은 후). Tooprovide 자격 증명 해야 합니다. 
4. 다른 (일반) 브라우저 창을 열고 다음 너무 이동[Azure](https://portal.azure.com)합니다. 로그아웃합니다. 다음 링크를 열고 hello 올바른 자격 증명을 사용 하 여 로그인 합니다.
5. Edge와 Internet Explorer 사용자는 신뢰하는 영역 설정이 지원되지 않을 때 이 오류가 발생할 수 있습니다.
   
    둘 다 확인 [분석 포털](https://analytics.applicationinsights.io) 및 [Azure Active Directory 포털](https://portal.azure.com) hello에 동일한 보안 영역:
   
   * Internet Explorer에서 **인터넷 옵션**, **보안**, **신뢰할 수 있는 사이트**, **사이트**를 엽니다.
     
     ![인터넷 옵션 대화 상자에서 사이트를 추가 tooTrusted 사이트](./media/app-insights-analytics-troubleshooting/033.png)
     
     Hello 웹 사이트 목록에 hello 다음 Url 중 하나를 포함 해야 해당 hello 다른 사용자도 포함 됩니다.
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... 리소스를 찾을 수 없음
![404 ... 리소스를 찾을 수 없음](./media/app-insights-analytics-troubleshooting/040.png)

응용 프로그램 리소스가 Application Insights에서 삭제되어서 더는 사용할 수 없습니다. 이 hello URL toohello 분석 페이지를 저장 하는 경우 발생할 수 있습니다.

## <a name="e-e"></a>403 ... 권한 없음
![403 ... 권한 없음](./media/app-insights-analytics-troubleshooting/050.png)

사용 권한 tooopen이 응용이 프로그램에에서 없는 분석 합니다.

* 어 hello 링크 다른 사람 으로부터? Hello에 있는지 toomake 달라고 [판독기나이 리소스 그룹에 대 한 참가자](app-insights-resources-roles-access-control.md)합니다.
* 다른 자격 증명을 사용 하 여 hello 링크 저장 하셨습니까? 열기 hello [Azure 포털](https://portal.azure.com), 로그 아웃 한 후 hello 올바른 자격 증명을 제공이 링크를 다시 시도 하십시오.

## <a name="html-storage"></a>403 ... HTML5 저장소
포털에서는 HTML5 localStorage와 sessionStorage를 사용합니다.

* Chrome: 설정, 개인 정보 보호, 콘텐츠 설정.
* Internet Explorer: 인터넷 옵션, 고급 탭, 보안, DOM 저장소를 사용하도록 설정

![403... tooenable HTML5 저장소를 시도 하십시오.](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... 구독을 찾을 수 없음
![404 ... 구독을 찾을 수 없음](./media/app-insights-analytics-troubleshooting/070.png)

hello URL이 올바르지 않습니다. 

* Hello 응용 프로그램 리소스에서 열고 [Application Insights 포털](https://portal.azure.com)합니다. Hello 분석 단추를 사용 합니다.

## <a name="e-h"></a>404 ... 페이지가 없습니다.
![404 ... 페이지가 존재하지 않습니다.](./media/app-insights-analytics-troubleshooting/080.png)

hello URL이 올바르지 않습니다.

* Hello 응용 프로그램 리소스에서 열고 [Application Insights 포털](https://portal.azure.com)합니다. Hello 분석 단추를 사용 합니다.

## <a name="cookies"></a>타사 쿠키 사용
  참조 [toodisable는 타사 쿠키 방식을](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), 여기서 너무 필요 하지만**사용** 해당 합니다.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

