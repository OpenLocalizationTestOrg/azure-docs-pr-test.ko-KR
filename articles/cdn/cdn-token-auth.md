---
title: "토큰 인증을 사용 하 여 aaaSecuring Azure CDN 자산 | Microsoft Docs"
description: "토큰 인증 toosecure tooyour Azure CDN 자산에 액세스를 사용합니다."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>보안 토큰 인증을 사용하여 Azure CDN 자산 보안 유지

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>개요

토큰 인증은 자산 toounauthorized 클라이언트 역할에서 Azure CDN tooprevent 수 있는 메커니즘입니다.  일반적으로 이렇게 tooprevent "hotlinking"의 콘텐츠를 다른 웹 사이트, 종종 메시지 보드의 허가 없이 자산을 사용 합니다.  콘텐츠 배달 비용에 영향을 줄 수 있습니다. CDN에서이 기능을 사용 하 여 요청 CDN 가장자리 hello 콘텐츠를 배달 하기 전에 팝 하 여 인증 됩니다. 

## <a name="how-it-works"></a>작동 방법

토큰 인증 요청 toocontain hello 요청자에 대 한 인코딩된 정보를 포함 하는 토큰 값을 요구 하 여 신뢰할 수 있는 사이트에서 생성 요청을 확인 합니다. 콘텐츠는만 제공 toorequester hello 충족 hello 요구 사항 정보를 인코딩할 경우, 그렇지 않으면 요청은 거부 됩니다. 하나 또는 여러 개의 아래 매개 변수를 사용 하 여 hello 요구를 설정할 수 있습니다.

- 국가: 지정된 국가에서 시작된 요청을 허용하거나 거부합니다.  [올바른 국가 코드 목록](https://msdn.microsoft.com/library/mt761717.aspx) 
- URL: 지정 된 자산 또는 경로 toorequest을 허용 합니다.  
- 호스트: 허용 하거나 hello 요청 헤더에 지정 된 호스트를 사용 하 여 요청을 거부 합니다.
- 참조 페이지: 허용 하거나 지정 된 참조 페이지 toorequest를 거부 합니다.
- IP 주소: 특정 IP 주소 또는 IP 서브넷에서 시작된 요청만 허용합니다.
- 프로토콜: 허용 하거나 toorequest hello 콘텐츠를 사용 하는 hello 프로토콜에 따라 요청을 차단 합니다.
- 만료 시간: 할당 날짜와 기간 tooensure 링크만 하 게 유지 되도록 유효한 제한 된 기간에 대 한 시간입니다.

각 매개 변수에 대한 자세한 구성 예제를 참조하세요.

## <a name="reference-architecture"></a>참조 아키텍처

웹 앱과 함께 CDN toowork에 토큰 인증 설정의 참조 아키텍처 아래를 참조 하십시오.

![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>CDN 끝점의 토큰 유효성 검사 논리
    
이 차트에서는 CDN 끝점에 토큰 인증이 구성된 경우 Azure CDN 클라이언트에서 요청의 유효성을 검사하는 방법을 설명합니다.

![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>토큰 인증 설정

1. Hello에서 [Azure 포털](https://portal.azure.com)tooyour CDN 프로필을 찾아 클릭 hello **관리** 단추 toolaunch hello 보조 포털입니다.

    ![CDN 프로필 블레이드 관리 단추](./media/cdn-rules-engine/cdn-manage-btn.png)

2. 위로 마우스를 가져가고 **HTTP 큰**, 클릭 하 고 **토큰 Auth** hello 플라이 아웃에서 합니다. 이 탭에서 암호화 키 및 암호화 매개 변수를 설정합니다.

    1. **기본 키**에 대한 고유한 암호화 키를 입력합니다.  **백업 키**에 대한 또 다른 고유한 암호화 키를 입력합니다.

        ![CDN 토큰 인증 설정 키](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. 암호화 도구를 사용하여 암호화 매개 변수를 설정합니다(만료 시간, 참조 페이지, 프로토콜, 클라이언트 IP를 기반으로 요청을 허용하거나 거부하며, 원하는 조합을 사용할 수 있음).

        ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - ec-expire: 지정된 기간 이후의 토큰 만료 시간을 할당합니다. 요청을 제출 hello 만료 시간을 거부 합니다. 이 매개 변수는 Unix 타임스탬프를 사용합니다(표준 Epoch인 1970년 1월 1일 00:00:00 GMT 이후의 초 단위. 사용할 수 있습니다 표준시 / Unix 시간 온라인 도구 tooprovide 변환 합니다.)  2016 년 12 월 31 일에 hello 토큰 toobe 만료 된 tooset를 원하는 경우 예를 들어 12시: 00 GMT, 아래와 같이 hello Unix 시간: 1483185600 사용:
    
        ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - ec url 허용: tootailor 토큰 tooa 특정 자산 또는 경로 있습니다. 특정 상대 경로와 URL을 시작 하는 액세스 toorequests을 제한 합니다. 각 경로를 쉼표로 구분하여 여러 경로를 입력할 수 있습니다. URL은 대/소문자를 구분합니다. Hello 요구 사항에 따라 다른 값 tooprovide 서로 다른 수준의 액세스를 설정할 수 있습니다. 다음은 몇 가지 시나리오입니다.
        
            URL이 http://www.mydomain.com/pictures/city/strasbourg.png인 경우 입력 값("")과 해당 액세스 수준을 확인합니다.

            1. 입력 값 "/": 모든 요청이 허용됩니다.
            2. 입력 값 "/ 그림": 요청을 수행 하는 모든 hello를 허용 합니다
            
                - http://www.mydomain.com/pictures.png
                - http://www.mydomain.com/pictures/city/strasbourg.png
                - http://www.mydomain.com/picturesnew/city/strasbourgh.png
            3. 입력 값 "/pictures/": /pictures/에 대한 요청만 허용됩니다.
            4. 입력 값 "/ pictures/city/strasbourg.png": 이 자산에 대한 요청만 허용됩니다.
    
        ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - ec-country-allow: 하나 이상의 지정된 국가에서 시작된 요청만 허용합니다. 다른 모든 국가에서 시작된 요청은 거부됩니다. 국가 코드 tooset hello 매개 변수 및 각 국가 코드는 쉼표로 구분 하를 사용 합니다. 예를 들어 미국과 프랑스에서 tooallow 액세스 하려는 경우 입력 US, 아래 hello 열에 FR입니다.  
        
        ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - ec-country-deny: 하나 이상의 지정된 국가에서 시작된 요청을 거부합니다. 다른 모든 국가에서 시작된 요청은 허용됩니다. 국가 코드 tooset hello 매개 변수 및 각 국가 코드는 쉼표로 구분 하를 사용 합니다. 예를 들어 미국과 프랑스에서 toodeny 액세스 하려는 경우 입력 US, FR hello 열에서입니다.
    
        - ec-ref-allow: 지정된 참조 페이지의 요청만 허용합니다. 참조 페이지는 요청 된 toohello 리소스를 연결 하는 hello 웹 페이지의 hello URL을 식별 합니다. hello referrer 매개 변수 값 hello 프로토콜을 포함 하지 않아야 합니다. 호스트 이름 및/또는 해당 호스트 이름의 특정 경로를 입력할 수 있습니다. 또한 단일 매개 변수 내에 쉼표로 구분하여 여러 참조 페이지를 추가할 수 있습니다. 참조 페이지 값을 지정 했습니다. hello 참조 페이지 정보 hello 요청 toosome 브라우저 구성 때문에 전송 되지 않습니다 되지만 기본적으로 이러한 요청은 거부 됩니다. 참조 페이지 정보를 누락 된 이러한 요청 "Missing" 또는 hello 매개 변수 tooallow 빈 값을 할당할 수 있습니다. 사용할 수 있습니다 "*. consoto.com" tooallow consoto.com의 모든 하위 도메인입니다.  예를 들어 www.consoto.com, consoto2.com 및 비어 있거나 누락 reffers와 erquests 아래의 모든 하위 도메인과의 요청에 대 한 tooallow 액세스 하려는 경우에 아래에 있는 값 입력:
        
        ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - ec-ref-deny: 지정된 참조 페이지의 요청을 거부합니다. Toodetails 및 매개 변수 "ec-ref-허용"의 예제를 참조 하십시오.
         
        - ec-proto-allow: 지정된 프로토콜(예: http 또는 https)의 요청만 허용합니다.
        
        ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - ec-proto-allow: 지정된 프로토콜(예: http 또는 https)의 요청을 거부합니다.
    
        - clientip ec: 액세스 toospecified 요청자의 IP 주소를 제한 합니다. IPV4 및 IPV6 모두 지원됩니다. 단일 요청 IP 주소 또는 IP 서브넷을 지정할 수 있습니다.
            
        ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. Hello 설명 도구로 토큰을 테스트할 수 있습니다.

    4. 반환 되는 toouser 요청이 거부 되는 경우 응답의 hello 형식의 사용자 지정할 수 있습니다. 기본적으로 403을 사용합니다.

3. 이제 **HTTP Large** 아래에서 **규칙 엔진** 탭을 클릭합니다. 이 탭 toodefine 경로 tooapply hello 기능을 사용 하 여 hello 토큰 인증 기능을 활성화 및 사용 하도록 설정 됩니다 추가 토큰 인증 관련 기능입니다.

    - "IF" 열 toodefine 자산 또는 tooapply 토큰 인증 경로 사용 합니다. 
    - Hello 기능 드롭다운 tooenable 토큰 인증에서 tooadd "토큰 인증"을 클릭 합니다.
        
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. Hello에 **규칙 엔진** 탭, 몇 가지 추가 기능을 사용 하도록 설정할 수 있습니다.
    
    - 인증 거부 코드 토큰: 반환 될 toouser 요청이 거부 되는 경우 응답의 hello 유형을 결정 합니다. 규칙이 여기 설정 hello 토큰 인증 탭에서 hello 거부 코드 설정을 덮어씁니다.
    - 토큰 인증 무시: 사용 되는 URL toovalidate 토큰은 대/소문자 구분 되는지 여부를 결정 합니다.
    - 토큰 인증 매개 변수: hello 토큰 인증 쿼리 문자열 매개 변수를 보여주는 hello에 요청 된 URL 이름을 변경 합니다. 
        
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-token-auth/cdn-rules-engine2.png)

5. 토큰 기반 인증 기능에 대한 토큰을 생성하는 응용 프로그램인 토큰을 사용자 지정할 수 있습니다. 소스 코드는 [GitHub](https://github.com/VerizonDigital/ectoken)에서 액세스할 수 있습니다.
사용 가능한 언어는 다음과 같습니다.
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Azure CDN 기능 및 공급자 가격 책정

Hello 참조 [CDN 개요](cdn-overview.md) 항목입니다.
