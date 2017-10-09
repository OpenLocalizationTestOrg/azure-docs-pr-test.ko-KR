---
title: aaaTemplates
description: "이 항목에서는 Azure 알림 허브용 템플릿에 대해 설명합니다."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>템플릿
## <a name="overview"></a>개요
템플릿을 사용 하는 클라이언트 응용 프로그램 toospecify hello 정확한 형식 tooreceive 브로드캐스트하며 hello 알림입니다. 템플릿을 사용 하는 응용 프로그램 hello 다음을 비롯 한 여러 가지 서로 다른 이점을 인식할 수 있습니다.

* 플랫폼 제약이 없는 백 엔드
* 개인화된 알림
* 클라이언트 버전 독립성
* 간편한 지역화

이 섹션에서는 어떻게 toouse 템플릿 toosend 플랫폼 제약 없는 알림 플랫폼과 toopersonalize 간에 모든 장치를 대상으로 브로드캐스팅 알림 tooeach 장치는 두 가지 심층 분석 예.

## <a name="using-templates-cross-platform"></a>플랫폼 간 템플릿 사용
hello 표준 방식으로 toosend 푸시 알림을 특정 페이로드 tooplatform notification services (WNS, APNS) toobe 전송 되는 각 알림에 대해 toosend입니다. 예를 들어, 경고는 tooAPNS toosend hello 페이로드는 hello 다음 폼의 Json 개체를 사용 하 여:

    {"aps": {"alert" : "Hello!" }}

Windows 스토어 응용 프로그램에서 비슷한 알림 메시지를 toosend hello XML 페이로드는 다음과 같습니다.

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

MPNS(Windows Phone) 및 GCM(Android) 플랫폼에 대해 유사한 페이로드를 만들 수 있습니다.

이 요구 사항을 hello 앱 백 엔드 tooproduce 다른 페이로드 각 플랫폼에 대 한 하 고 효과적으로 사용 하면 hello 백 엔드 hello 앱의 hello 프레젠테이션 계층의 일부를 담당 합니다. 이 경우 지역화 및 그래픽 레이아웃(특히 여러 유형의 타일에 대한 알림을 포함하는 Windows 스토어 앱의 경우)을 포함한 몇 가지 문제가 있습니다.

hello 알림 허브 템플릿 기능에 대 한 클라이언트 응용 프로그램 toocreate 특수 등록, 호출 또한 toohello 태그 집합으로, 서식 파일을 포함 하는 템플릿 등록을 사용 합니다. hello 알림 허브 템플릿 기능 설치 (기본 설정) 또는 등록을 사용 하 여 작업할 수 있는지 여부를 템플릿으로 클라이언트 응용 프로그램 tooassociate 장치를 있습니다. 페이로드 예제 앞 hello 들어 hello만 플랫폼 독립적인 정보는 hello 실제 경고 메시지 (Hello!)입니다. 템플릿은 일련의 어떻게 tooformat 플랫폼 독립적인 메시지 해당 특정 클라이언트 응용 프로그램의 hello 등록에 알림 허브 hello에 대 한 지침입니다. 앞 예제는 hello, hello 플랫폼 독립적인 메시지는 단일 속성: **메시지 = Hello!**합니다.

다음 그림 hello를 프로세스 위에 hello를 보여 줍니다.

![](./media/notification-hubs-templates/notification-hubs-hello.png)

hello iOS 클라이언트 앱 등록에 대 한 hello 서식 파일은 다음과 같습니다.

    {"aps": {"alert": "$(message)"}}

hello Windows 스토어 클라이언트 응용 프로그램에 대 한 hello 해당 서식 파일은입니다.

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

실제 메시지 hello는 hello 식 $(메시지)에 대 한 대체 됩니다. 이 식은 특정 등록을 하 고 hello 공통 값에 스위치 다음에 나오는 메시지 toobuild 메시지 toothis 보낼 때마다 hello 알림 허브에 지시 합니다.

설치 모델을 사용 하는 hello 설치 "템플릿" 키 여러 서식 파일의 JSON을 보유 합니다. 등록 모델을 사용 하는 hello 클라이언트 응용 프로그램에서에서 만들 수 여러 등록 순서 toouse 템플릿이 여러 개 있습니다. 예를 들어 경고 메시지에 대 한 템플릿과 템플릿이 타일에 대 한 업데이트합니다. 또한 클라이언트 응용 프로그램은 기본 등록(템플릿이 없는 등록)과 템플릿 등록을 혼합할 수 있습니다.

알림 허브 hello toohello 속하는지 여부를 고려 하지 않고 각 서식 파일에 대 한 알림을 보냅니다 같은 클라이언트 응용 프로그램입니다. 이 문제를 더 많은 사용된 tootranslate 플랫폼 독립적인 알림이 될 수 있습니다. 예를 들어 hello 동일한 플랫폼 독립적인 메시지 toohello hello 백 엔드 toobe 것을 요구 하지 않고 알림 경고 및 타일 업데이트 알림 허브를 원활 하 게 번역할 수 있습니다. 참고 일부 플랫폼 (예를 들어 iOS)가 여러 알림을 toohello를 축소할 수는 짧은 시간 내에 보낼 경우 동일한 장치입니다.

## <a name="using-templates-for-personalization"></a>개인 설정에 템플릿 사용
또 다른 이점은 toousing 템플릿 hello 기능 toouse 알림의 알림 허브 tooperform 등록 당 개인 설정입니다. 예를 들어 날씨 응용 프로그램을 특정 위치에 hello 날씨 조건 사용 하 여 타일을 표시 하는 것이 좋습니다. 사용자는 섭씨 또는 화씨 온도 및 1일 또는 5일 예보 중에서 선택할 수 있습니다. 템플릿을 사용 하 여, 필요한 hello 형식에 대 한 각 클라이언트 응용 프로그램 설치를 등록할 수 (1 일 섭씨, 1 일 화씨, 5 한 일 섭씨, 화씨), 있고 hello 정보가 모두 들어 있는 단일 메시지 필요한 toofill 하는 것을 전송 하는 hello 백 엔드 서식 파일 (예를 들어는 5 일 섭씨 및 화씨도 예측 하는 경우).

hello 템플릿 hello 하루 섭씨를 예측 하는 온도 다음과 같습니다.

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

hello 메시지 전송 toohello 알림 허브는 모든 hello를 다음 속성이 포함 되어 있습니다.

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

이 패턴을 사용 하 여 hello 백 엔드 hello 응용 프로그램 사용자에 대 한 특정 개인 설정 옵션 toostore 필요 없이 단일 메시지만 보냅니다. hello 다음 그림에서는이 시나리오를 보여 줍니다.

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>어떻게 tooregister 템플릿
hello 설치 모델 (기본 설정)를 사용 하 여 템플릿을 또는 hello 등록 모델 tooregister 참조 [등록 관리](notification-hubs-push-notification-registration-management.md)합니다.

## <a name="template-expression-language"></a>템플릿 식 언어
서식 파일은 제한 된 tooXML 또는 JSON 문서 형식입니다. 또한 식을 특정 장소에만 배치할 수 있습니다. 예를 들어 XML은 노드 속성 또는 값에, JSON은 문자열 속성 값에 배치할 수 있습니다.

hello 아래 표에 나와 hello 언어 템플릿에서 허용.

| 식 | 설명 |
| --- | --- |
| $(prop) |Hello 지정 된 이름의 tooan 이벤트 속성 참조입니다. 속성 이름은 대/소문자를 구분하지 않습니다. 이 식은 hello 속성이 없으면 hello 속성의 텍스트 값 또는 빈 문자열을 해결 합니다. |
| $(prop, n) |위의 예와 같지만 hello 텍스트가 명시적으로 대로 n 문자에 맞게 잘립니다, 예를 들어 $(제목, 20) hello title 속성의 hello 내용을에서 클립 20 자까지 허용 합니다. |
| .(prop, n) |위, 같지만 hello 텍스트를 잘라냅니다 대로 세 개의 점 접미사로 합니다. hello hello의 전체 크기 문자열 잘리고 hello 접미사 n 자를 초과 하지 않는 됩니다. . (제목, 20)에서 "hello 제목 줄은" 결과의 입력된 속성이 있는 **hello 제목 이것이...** |
| %(prop) |해당 hello 출력을 제외한 비슷한 too$(name)는 URI로 인코딩됩니다. |
| #(prop) |JSON 템플릿(예: iOS 및 Android 템플릿)에 사용됩니다.<br><br>이 함수 작동 정확 하 게 hello 동일으로 $(prop) JSON 템플릿 (예를 들어, 사과 템플릿)에 사용 되는 경우를 제외 하 고 이전에 지정 합니다. 이 경우,이 함수는 둘러싸인 되지 "{','을 (를)" (예를 들어 'myJsonProperty': '#(이름)'), 예를 들어 regexp Javascript 형태로 tooa 수를 계산 하 고: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 &#93;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, hello JSON은 숫자를 출력 합니다.<br><br>예를 들어 ‘badge : ‘#(name)’은 ‘badge’ : 40 이 됩니다(‘40‘이 아니라). |
| 'text' 또는 "text" |리터럴입니다. 리터럴에는 작은따옴표 또는 큰따옴표로 묶인 임의의 텍스트가 포함됩니다. |
| expr1 + expr2 |hello 연결 연산자 두 식을 단일 문자열로 조인 합니다. |

hello 식 앞에 forms hello 중 하나일 수 있습니다.

연결을 사용할 경우 hello 전체 식은 {}로 묶어야 합니다. 예: {$(prop) + ‘ - ’ + $(prop2)}. |

예를 들어 hello 다음 유효한 XML 서식 파일은 아닙니다.

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


위에서 설명한 대로 연결을 사용하는 경우 식을 중괄호로 묶어야 합니다. 예:

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

