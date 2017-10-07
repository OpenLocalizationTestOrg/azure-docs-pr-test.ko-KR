---
title: "aaaAdd 회사 브랜딩 tooyour 로그인 및 액세스 패널 페이지"
description: "어떻게 tooadd 회사 브랜딩 toohello Azure 로그인 페이지 및 hello 액세스 패널 페이지에 알아봅니다"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>회사 브랜딩 tooyour 로그인 및 액세스 패널 페이지 추가
tooavoid 혼동 많은 회사 모든 hello 웹 사이트 및 서비스 관리 tooapply 일관 된 모양과 느낌을 원합니다. Azure Active Directory toocustomize hello 모양의 hello 회사 로고 및 사용자 지정 색 구성표와 웹 페이지에 다음을 허용 하 여이 기능을 제공 합니다.

* **로그인 페이지** -tooOffice 365에에서 로그인 할 때 표시 되는 hello 페이지 또는 id 공급자로 Azure AD를 사용 하는 다른 웹 기반 응용 프로그램입니다. 자격 증명이 페이지는 홈 영역 검색 또는 tooenter 중 상호 작용 합니다. 홈 영역 검색 hello hello 시스템 tooredirect 페더레이션 사용자가 tootheir 온-프레미스 STS (예: AD FS)를 허용합니다.
* **액세스 패널 페이지** -hello 액세스 패널은 tooview 수 있는 웹 기반 포털 및에 대 한 hello 클라우드 기반 응용 프로그램을 시작 하려면 Azure AD 관리자 권한이 부여 된 액세스 합니다. tooaccess hello 액세스 패널을 사용 하 여 hello url: [https://myapps.microsoft.com](https://myapps.microsoft.com)합니다.

이 방법을 사용자 지정할 수 있습니다 hello 로그인 페이지와 액세스 패널 페이지 hello 설명 합니다.

> [!NOTE]
> * 회사 브랜딩은 Office 365 사용자 않거나 toohello Premium 또는 Azure Active directory Basic edition을 업그레이드 한 경우에 사용할 수 있는 기능. 자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.
> * Azure Active Directory Premium 및 Basic edition은 중국 고객의 사용 가능한 Azure Active Directory의 전세계 인스턴스 hello를 사용 하 여 합니다. Azure Active Directory Premium 및 Basic edition 중국의 21vianet이 운영 하는 hello Microsoft Azure 서비스에서 현재 지원 되지 않습니다. 자세한 내용은 주소로 문의 hello [Azure Active Directory 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)합니다.
>
>

## <a name="customizing-hello-sign-in-page"></a>Hello 로그인 페이지 사용자 지정
일반적으로 조직이 구독 하는 브라우저 기반 액세스 tooyour 클라우드 앱과 서비스를 필요 하면 hello 로그인 페이지를 사용 합니다.

변경 내용 tooyour 로그인 페이지를 적용 한 경우 변경 내용 tooappear hello에 대 한 tooan 시간까지 걸릴 수 있으므로 합니다.

https://outlook.com/**contoso**.com 또는 https://mail.**contoso**.com과 같은 테넌트 특정 URL로 서비스를 이용할 경우 브랜드가 지정된 로그인 페이지만이 나타납니다.

비테넌트 특정 URL (예: https://mail.office365.com ) 을 사용하여 서비스에 방문하는 경우 브랜드가 지정되지 않은 로그인 페이지가 나타납니다. 이 경우에 사용자 ID를 입력하거나 사용자 타일을 선택하면 브랜딩이 나타납니다.

> [!NOTE]
> * Hello에 도메인 이름이 "활성"으로 표시 해야 **Active Directory** > **디렉터리** > **도메인** hello Azure 클래식 포털의 섹션 여기서 브랜딩 구성 했습니다.
> * 로그인 페이지 브랜딩 toohello 소비자 로그인 페이지의 Microsoft 적용 되지 않습니다. 개인 Microsoft 계정으로 로그인 할 Azure AD를 통해 렌더링 된 사용자 타일의 브랜드가 지정 된 목록이 표시 될 수 있지만 조직의 브랜딩이 hello toohello Microsoft 계정 로그인 페이지는 적용 되지 않습니다.
>
>

회사 브랜드, 색 및이 페이지의 다른 사용자 지정 가능한 요소 tooshow를 원하는 경우 hello hello 두 환경 간의 이미지 toounderstand hello 차이 다음을 참조 하십시오.

다음 스크린 샷에 표시 및 데스크톱 컴퓨터에 Office 365 hello 로그인 페이지에 대 한 예제 hello **전에** 는 사용자 지정:

![사용자 지정하기 전 Office 365 로그인 페이지][1]

다음 스크린 샷에 표시 및 데스크톱 컴퓨터에 Office 365 hello 로그인 페이지에 대 한 예제 hello **후** 는 사용자 지정:

![사용자 지정한 후 Office 365 로그인 페이지][2]

hello 다음 스크린 샷에서 모양의 예제가 나와 hello Office 365 로그인 페이지는 모바일 장치에서 **전에** 는 사용자 지정:

![사용자 지정하기 전 Office 365 로그인 페이지][3]

hello 다음 스크린 샷에서 모양의 예제가 나와 hello Office 365 로그인 페이지는 모바일 장치에서 **후** 는 사용자 지정:

![사용자 지정한 후 Office 365 로그인 페이지][4]

브라우저 창 크기를 조정할 때 큰 그림 hello, hello와 같은 이전에 표시 된 하나는 종종 잘리는 tooaccommodate 다른 화면 가로 세로 비율입니다. 이 점을 고려 hello 왼쪽 위 모서리 (오른쪽 위 오른쪽에서 왼쪽 언어에 대 한)에 항상 표시 되도록 tookeep hello 주요 시각적 요소가 hello 그림에서을 시도해 야. 위쪽 / 왼쪽 hello에 대 한 hello 오른쪽 아래 모서리 않도록에서 또는 hello 위쪽 방향으로 hello 아래에서 발생 일반적으로 크기를 조정 하기 때문에 유용 합니다.

hello 다음 다음과 같은 순서로 hello 그림 hello 브라우저에서 크기가 조정 된 toohello 왼쪽 때 잘리는 방법을

![][6]

표시 되는 방식 hello 브라우저 hello 위쪽으로 크기 조정 후 다음과 같습니다.

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>Hello 페이지에서 어떤 요소 사용자 지정할 수 있습니까?
Hello 요소 hello 로그인 페이지에서 다음을 사용자 지정할 수 있습니다.

![][5]

| 페이지 요소 | Hello 페이지의 위치 |
|:--- | --- |
| 배너 로고 |Hello의 오른쪽 위에 hello 페이지에 표시 합니다. 로그인 하는 toodisplays (예: hello 로고 hello 대상 사이트를 대체 Office 365 또는 Azure)에 일반적으로 표시되는 로고를 대체합니다. |
| 큰 그림/배경색 |Hello hello 페이지 왼쪽에 표시 합니다. Toodisplays 로그인 하는 hello 이미지 hello 대상 사이트를 대체 합니다. 좁은 화면 또는 낮은 대역폭 연결에 hello 큰 그림 대신 배경색이 hello는 표시할 수 있습니다. |
| 로그인 유지 |Hello 암호 텍스트 상자 아래에 표시 합니다. |
| 로그인 페이지 텍스트 |회사 또는 학교 계정에 로그인 하기 전에 tooconvey 유용한 정보를 할 때 hello 페이지 바닥글 위에 표시 됩니다. 예를 들어 tooinclude hello 전화 번호 tooyour 지원 센터, 또는 법적 설명이 사용할 수 있습니다. |

> [!NOTE]
> 모든 요소는 선택 사항입니다. 예를 들어 배너 로고만 없는 큰 그림을 지정 하면 hello 로그인 페이지 hello 대상 사이트 (즉, hello Office 365 캘리포니아 고속도 이미지)에 대 한 로고 및 hello 그림에 표시 합니다.
>
>

로그인 페이지에 hello **로그인 상태 유지** 확인란을 사용 하는 사용자 tooremain 닫고 브라우저를 다시 열 때 로그인 합니다. 세션 수명에는 영향을 미치지 않습니다. Hello Azure Active Directory 로그인 페이지 hello 확인란을 숨길 수 있습니다.

hello 설정에 따라 hello 확인란이 표시 되는 여부 **숨기기 KMSI**합니다.

![][9]

toohide hello 확인란, 너무이 설정을 구성 하**Hidden**합니다.

> [!NOTE]
> SharePoint Online 및 Office 2010의 일부 기능은이 상자 toocheck 수 있는 사용자가에 따라 다릅니다. 이 설정은 toohidden를 구성 하면 toosign 기능을 추가 및 예기치 않은 메시지가 나타나면 사용자가 볼 수 있습니다.
>
>

이 페이지의 모든 요소를 지역화할 수도 있습니다. "기본" 사용자 지정 요소 집합을 구성한 후 다른 로캘로 추가 버전을 구성할 수 있습니다. 다양한 요소를 적절히 조합하여 사용할 수도 있습니다. 예를 들어 다음을 수행할 수 있습니다.

* 모든 문화권에 적용되는 "기본" 큰 그림을 만든 다음 영어와 프랑스어에 대한 특정 버전을 만듭니다. 이 두 언어의 브라우저 tooone 프로그램으로 설정 하면 다른 모든 언어에 대 한 hello 기본 그림이 표시 하는 동안 hello 특정 이미지가 표시 됩니다.
* 조직에 따라 다른 로고를 구성합니다(예: 일본어 또는 히브리어 버전).

## <a name="access-panel-page-customization"></a>액세스 패널 페이지 사용자 지정
hello 액세스 패널 페이지에는 포털 페이지 기본적으로 빠른 액세스 toohello 클라우드 앱 부여 된 액세스 tooby 관리자에 게 문의 합니다. 이 페이지에서 앱을 클릭 가능한 응용 프로그램 타일로 표시합니다.

hello 스크린 샷 다음 사용자 지정 후 액세스 패널 페이지의 예를 보여 줍니다.

![][8]

## <a name="configure-your-directory-with-company-branding"></a>회사 브랜딩으로 디렉터리 구성
Hello Azure 클래식 포털에서에서 디렉터리 당 사용자 지정 가능한 요소 하나의 기본 집합을 구성할 수 있습니다. 관리자가 서로 다른 언어에 대 한 각 요소의 지역화 된 버전을 추가할 수 hello 기본값을 저장 한 후 / 로캘에서 합니다. 모든 사용자 지정 가능한 요소는 선택 사항입니다.

예를 들어 기본 배너 로고만 없는 큰 그림을 구성한 경우 hello 로그인 페이지 hello 오른쪽 위 모서리에 로고를 표시 합니다. 그러나 hello 사이트의 hello 기본 그림이 표시 됩니다.

Hello를 같은 구성이 있다고 가정해 봅시다.

* 영어로 표시된 기본 배너 로고 및 로그인 페이지 텍스트
* 독일어에 대한 로그인 페이지 텍스트

기본 언어가 독일어 인 경우 hello 기본 배너 로고만 hello 독일어 텍스트를 가져옵니다.

기술적으로 Azure AD에서 지 원하는 각 언어에 대 한 다른 집합을 구성할 수 수 유지 하는 hello 변형의 유지 관리 및 성능을 이유로 낮은 것이 좋습니다.

> [!IMPORTANT]
> Yammer는 hello 사용자가 로그인 한 후 Azure AD 로그인 페이지까지의 브랜드 표시 hello를 하지 않습니다. 제네릭 Office 365 로그인 페이지를 먼저 hello 및 다음 hello 그 후 페이지의 브랜드 hello 사용자에 게 표시 합니다.   
 
 
**tooadd 회사 브랜딩 tooyour 디렉터리에 hello 다음 단계를 수행 합니다.**

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) toocustomize hello 디렉터리의 관리자로 서 원하는 합니다.
2. Toocustomize hello 디렉터리를 선택 합니다.
3. 도구 모음의 hello hello 위쪽에 클릭 **구성**합니다.
4. **브랜딩 사용자 지정**을 클릭합니다.
5. Toocustomize hello 요소를 수정 합니다. 모든 필드는 선택 사항입니다.
6. **Save**를 클릭합니다.

까지 걸릴 수 있으므로 새로운 변경에 대 한 tooan 시간 있습니다 toohello 로그인 페이지 브랜딩 tooappear를 수행 합니다.

**tooadd 언어별 회사 브랜딩 hello 다음 단계를 수행:**

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) toocustomize hello 디렉터리의 관리자로 서 원하는 합니다.
2. Toocustomize hello 디렉터리를 선택 합니다.
fs3. 도구 모음의 hello hello 위쪽에 클릭 **구성**합니다.
4. **브랜딩 사용자 지정**을 클릭합니다.
5. **특정 언어에 대한 브랜딩 추가**를 클릭합니다.
6. Hello 언어 toocustomize hello 로고를 하 고을 클릭 한 다음 선택 **다음**합니다.
7. Tooconfigure 언어별 재정의 하려는 hello 요소만 편집 합니다. 모든 필드는 선택 사항입니다. 필드에 정보를 입력 하지 않으면 다음 hello 사용자 지정 기본값이 대신 표시 됩니다 (또는 사용자 지정 기본값이 구성 되어 있지 않으면 Microsoft 기본값이 hello).
8. **Save**를 클릭합니다.

**tooremove 회사 디렉터리에서 이름이 hello 다음 단계를 수행:**

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) toocustomize hello 디렉터리의 관리자로 서 원하는 합니다.
2. Toocustomize hello 디렉터리를 선택 합니다.
3. 도구 모음의 hello hello 위쪽에 클릭 **구성**합니다.
4. **브랜딩 사용자 지정**을 클릭합니다.
5. Hello 브랜딩 사용자 지정 페이지에서 선택 **기존 브랜딩 설정 편집** toohello 다음 페이지로 이동 합니다.
6. 요소에 따라 tooremove 원하는 hello 다음 중 하나 이상을 수행 합니다.

    a. **배너 로고** 아래에서 **업로드된 로고 제거**를 선택합니다.

    b. **타일 로고** 아래에서 **업로드된 로고 제거**를 선택합니다.

    c. 모든 텍스트 상자에서 hello 텍스트를 제거 합니다.

    d. **Next**를 클릭합니다.

    e. 모든 텍스트 상자에서 hello 텍스트를 제거 합니다.
7. 클릭 **저장** tooremove hello 요소입니다.
8. 필요한 경우 클릭 **브랜딩 사용자 지정** 다시 제거 toobe 필요한 언어별 모든 브랜딩에 대해 이러한 단계를 반복 합니다.
    클릭 하면 모든 브랜딩 설정이 제거 **브랜딩 사용자 지정** hello 참조 및 **기본 브랜딩 사용자 지정** 없는 기존 설정이 구성 된 폼입니다.

## <a name="testing-and-examples"></a>테스트 및 예제
프로덕션 환경을 변경하기 전에 테스트 테넌트를 시험하는 것이 좋습니다.

**tooverify 여부 브랜딩이 적용 되었습니다.**

1. InPrivate 또는 Incognito 브라우저 세션을 엽니다.
2. Https://outlook.com/contoso.com을 방문 contoso.com hello 도메인 사용자 지정한 경로로 바꿉니다.

또한 contoso.onmicrosoft.com과 같이 표시되는 도메인으로도 작동합니다.

효율적인 사용자 지정 집합을 만들 toohelp, hello 다음 두 가상 로그인 페이지 사용자 지정 했습니다.

* [http://aka.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://aka.ms/aaddemo002](http://aka.ms/aaddemo002)

tootest hello 언어별 설정을 사용자 지정에서 설정한 웹 브라우저 tooa 언어에 toomodify hello 기본 언어 설정이 있어야 합니다. Internet Explorer에서이에서 구성한 hello **인터넷 옵션** 메뉴.

## <a name="customizable-elements"></a>사용자 지정 가능한 요소
Azure AD의 일부 사용자 지정 가능한 요소에는 여러 가지 사용 사례가 있습니다. 회사 로고 디렉터리 당 한 번 구성 하 고이 정보를, hello 로그인 페이지와 액세스 패널 페이지 모두에서 사용 됩니다. 사용자 지정 가능한 요소가 일부 특정만 toohello 로그인 페이지를 보여 줍니다. hello 다음 표에서 자세히 설명 hello에 대 한 다양 한 사용자 지정 가능한 요소입니다.

| 이름 | 설명 | 제약 조건 | 추천 |
| --- | --- | --- | --- |
| 배너 로고 |배너 로고 hello hello 로그인 페이지 및 hello 액세스 패널에 표시 됩니다. |<p>JPG 또는 PNG</p><p>60x280픽셀</p><p>10KB</p> |<p>조직의 전체 로고 사용(픽토그램과 로고 형식 포함)</p><p>모바일 장치에서 스크롤 막대가 표시 30 픽셀 미만 높은 tooavoid 유지</p><p>4KB 미만으로 유지하세요.</p><p>아니므로 투명 PNG를 사용 하 여 (가정 하지 마십시오 해당 hello 로그인 페이지에 항상 흰색 배경에)</p> |
| 타일 로고 |(현재 사용 되지 않습니다 hello 로그인 페이지) Hello 이후,이 텍스트 사용된 tooreplace hello 제네릭 "회사 또는 학교 계정" 픽토그램 hello 환경의 여러 위치에서 수 있습니다. |<p>JPG 또는 PNG</p><p>120x120픽셀</p><p>10KB</p> |<p>단순하게 유지 하 고 (작은 텍스트 없음),이 이미지는 크기가 조정 된 too50% 수 있으므로 |
| </p> | | | |
| 로그인 페이지 사용자 이름 레이블 |(현재 사용 되지 않습니다 hello 로그인 페이지) Hello 이후에이 텍스트는 사용 되는 tooreplace hello hello 환경의 여러 위치에서 제네릭 "회사 또는 학교 계정" 문자열이 수 있습니다. "Contoso account" 또는 "Contoso ID"와 같은 toosomething를 설정할 수 있습니다. |<p>Too50 문자를 유니코드 텍스트</p><p>일반 텍스트 전용(링크 또는 HTML 태그 없음)</p> |<p>짧고 간단하게 만드세요.</p><p>Toohello 작업 일반적으로 참조 하는 방법을 사용자에 게 문의 하거나 학교 계정이 제공 하 합니다.</p> |
| 로그인 페이지 텍스트 |이 "상용구" 텍스트 hello 로그인 페이지 양식 아래에 나타나며 tooget 도움말 및 지원 위치 또는 toocommunicate 사용 되는 추가 명령이 될 수 있습니다. |<p>Too256 문자를 유니코드 텍스트</p><p>일반 텍스트 전용(링크 또는 HTML 태그 없음)</p> |250자 미만(약 텍스트 3 줄)으로 유지하세요. |
| 로그인 페이지 그림 |hello 그림은 hello 로그인 페이지 toohello hello 로그인 페이지 양식 왼쪽에 표시 되는 큰 이미지입니다. |<p>JPG 또는 PNG</p><p>1420x1200</p><p>500KB</p> |<p>1420x1200픽셀</p><p>중요: 최대한 작게(200KB 미만이 이상적임) 유지하세요. Hello 이미지가 캐시 되지 않을 때 hello 로그인 페이지의 hello 성능이 저하 되어이 이미지가 너무 큰 경우</p><p>이 이미지 종종 잘리는 tooaccommodate 각 화면 비율입니다. Hello 왼쪽 위 모서리 (오른쪽 위 RTL 언어에 대 한), 크기 조정 hello 아래쪽/오른쪽 모서리 hello 위쪽 / 왼쪽으로 hello 브라우저 창을 축소할 때는에서 발생 하기 때문에 기본 시각적 요소가 hello를 유지 합니다.</p> |
| 로그인 페이지 배경색 |hello 로그인 페이지 배경색 hello 영역 toohello hello 로그인 페이지 양식 왼쪽에 사용 됩니다. |16진수 형식(예: #FFFFFF)의 RGB 색이어야 합니다. |<p>hello 대신 hello 배경색이 표시 될 수 있습니다 낮은 대역폭 연결에 대 한 큰 그림</p><p>Hello 배너 로고의 hello 기본 색을 선택 하는 것이 좋습니다.</p> |

## <a name="next-steps"></a>다음 단계
* [Azure Active Directory Premium 시작](active-directory-get-started-premium.md)
* [액세스 및 사용 보고서 보기](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
