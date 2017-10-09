---
title: "페이지 hello Azure Active Directory에서에서 로그인에 aaaCustomize | Microsoft Docs"
description: "자세한 내용은 방법 tooadd 회사 브랜딩 toohello Azure 로그인 페이지"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>빠른 시작: 회사 Azure AD에서 tooyour 로그인 페이지 브랜딩 추가
tooavoid 혼동 많은 회사 모든 hello 웹 사이트 및 서비스 관리 tooapply 일관 된 모양과 느낌을 원합니다. Azure Active Directory (Azure AD) toocustomize hello 모양의 회사 로고 및 사용자 지정 색 구성표와 hello 로그인 페이지를 허용 하 여이 기능을 제공 합니다. hello 로그인 페이지에는 365 또는 id 공급자로 Azure AD를 사용 하는 다른 웹 기반 응용 프로그램 tooOffice에 로그인 할 때 표시 되는 hello 페이지가입니다. 자격 증명 페이지 tooenter이 상호 작용합니다.

> [!NOTE]
> * 회사 브랜딩은 toohello Premium 또는 Basic edition의 Azure AD 업그레이드 하는 경우에 사용할 수 또는 Office 365 라이선스가 있어야 합니다. toolearn 기능이 해당 라이선스 형식에서 지원 되는지 확인 hello [Azure Active Directory 가격 정보 페이지](https://azure.microsoft.com/pricing/details/active-directory/)합니다.
> 
> * Azure Active Directory Premium 및 Basic edition은 중국 고객의 사용 가능한 Azure Active Directory의 전세계 인스턴스 hello를 사용 하 여 합니다. Azure Active Directory Premium 및 Basic edition 중국의 21vianet이 운영 하는 hello Microsoft Azure 서비스에서 현재 지원 되지 않습니다. 자세한 내용은 주소로 문의 hello [Azure Active Directory 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)합니다.

## <a name="customizing-hello-sign-in-page"></a>Hello 로그인 페이지 사용자 지정

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

회사 브랜딩 사용자 지정 사용자가 테 넌 트 별 URL을와 같은 액세스 hello Azure AD 로그인 페이지에 나타납니다 [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com)합니다.

사용자가 방문 www.office.com 같은 제네릭 URL, hello 로그인 페이지에는 회사 hello 시스템 hello 사용자 알 없기 때문에 사용자 지정 브랜딩 포함 되어 있지 않습니다. 사용자가 사용자 ID를 입력하거나 사용자 타일을 선택한 후에는 회사 브랜딩이 표시됩니다.

> [!NOTE]
> * Hello에 도메인 이름이 "활성"으로 표시 해야 **도메인** 부분의 hello를 브랜딩을 구성한 Azure 포털입니다. 자세한 내용은 [사용자 지정 도메인 이름 추가](add-custom-domain.md)를 참조하세요.
> * 로그인 페이지 브랜딩 toohello 로그인 페이지 개인 Microsoft 계정에 대 한 적용 되지 않습니다. 직원이 나 비즈니스 게스트 개인 Microsoft 계정으로 로그인 하는 경우 해당 로그인 페이지 사용자 조직의 hello 브랜딩 반영 하지 않습니다.


### <a name="banner-logo"></a>배너 로고 

설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
hello 배너 로고 hello에 대 한 로그인 및 hello 액세스 패널 페이지에 표시 됩니다.<br>Hello 로그인 페이지에서 hello 사용자의 조직 hello 사용자 이름을 입력 한 후에 일반적으로 결정 되 면 표시 됩니다.  | 투명 JPG 또는 PNG<br>최대 높이: 36px<br>최대 너비: 245px | 여기에서 조직의 로고를 사용합니다.<br>투명 이미지를 사용합니다. Hello 배경 흰색 된다는 가정 하지 마십시오.<br>로고 주위의 여백 hello 이미지에 추가 하지 마십시오 또는 로고 비례적 작은 표시 됩니다.

### <a name="username-hint"></a>사용자 이름 힌트   
설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
이 사용자 hello 사용자 이름 필드의 hello 힌트 텍스트를 지정합니다. | Too64 문자를 유니코드 텍스트<br>일반 텍스트 전용 | 설정 하지 않으면이 게스트 사용자가 사용자 조직 toosign tooyour 응용 프로그램에서 외부 예상 되는 경우는 것이 좋습니다.
            
### <a name="sign-in-page-text"></a>로그인 페이지 텍스트   
설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
이 hello 로그인 폼 hello 맨 아래에 표시 되 고 hello 전화 번호 tooyour 지원 센터, 또는 법적 문과 같은 추가 정보를 사용 하는 toocommunicate 수 있습니다. | Too256 문자를 유니코드 텍스트<br>일반 텍스트 전용(링크 또는 HTML 태그 없음) 

### <a name="sign-in-page-image"></a>로그인 페이지 이미지  
설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
Hello 배경의 hello 로그인 페이지에 나타납니다 hello 볼 수 있는 공간이 고정된 toohello 센터인 인과 크기를 조정 하 고 toofill 자르기 hello 브라우저 창.  <br>전화와 같은 좁은 화면에서는 이 이미지가 표시되지 않습니다.<br>0.55 불투명도 검은색 마스크에 의해 적용 됨이 이미지에 대해 코드 hello 페이지가 로드 될 때입니다. | JPG 또는 PNG<br>이미지 크기: 1920x1080px<br>파일 크기: &gt; 300KB | <br>강력한 제목 포커스가 없는 곳에 이미지를 사용합니다. hello 불투명-로그인 양식이이 이미지의 hello 센터를 통해 표시 되 고 hello 브라우저 창의 hello 크기에 따라 hello 이미지의 모든 부분에 나타날 수 있습니다.<br>Hello 파일 크기를 가능한 tooensure 빠른 로드 시간을 짧게 유지 합니다. 

### <a name="background-color"></a>배경색
설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
이 색은 낮은 대역폭 연결에 hello 배경 이미지 대신 사용 됩니다. |   16진수(예: #FFFFFF)의 RGB 색 | Hello 배너 로고의 hello 기본 색 또는 사용자 조직 색을 사용 하는 것이 좋습니다.

### <a name="show-option-tooremain-signed-in"></a>로그인 옵션 tooremain 표시
설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
Azure AD 로그인 제공 hello 사용자 hello 옵션 tooremain 닫고 브라우저를 다시 열 때 로그인 합니다. 이 toohide 옵션을 사용 합니다.<br>이 너무 "설정" toohide 사용자가이 옵션입니다. | &nbsp; | 세션 수명에는 영향을 미치지 않습니다.<br>SharePoint Online 및 Office 2010의 일부 기능은 사용자가 로그인 수 toochoose tooremain에 따라 다릅니다. 숨겨진이 toobe 설정한 toosign 기능을 추가 및 예기치 않은 메시지가 나타나면 사용자가 볼 수 있습니다.

> [!NOTE]
> 모든 요소는 선택 사항입니다. 예를 들어 배너 로고 없는 배경 이미지를 지정 하면 hello 로그인 페이지 hello 대상 사이트 (예를 들어 Office 365)에 대 한 로고 및 hello 배경 이미지를 표시 됩니다.

## <a name="add-company-branding-tooyour-directory"></a>회사 브랜딩 tooyour 디렉터리 추가

1. 역시 로그인[Azure 포털 hello](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.

   ![사용자 관리 열기](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Hello에 **사용자 및 그룹** 블레이드를 **회사 브랜딩**합니다.
4. Hello에 **사용자 및 그룹-회사 브랜딩** 블레이드, 선택 hello **편집** 명령입니다.

    ![사용자 지정 브랜딩 편집](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Toocustomize hello 요소를 수정 합니다. 모든 요소는 선택 사항입니다.
6. **Save**를 클릭합니다.

변경한 모든 toohello 로그인 페이지 브랜딩 tooappear에 대 한 tooan 시간까지 걸릴 수 있으므로 합니다.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>언어별 회사 브랜딩 tooyour 디렉터리 추가

1. Toohello 로그인 [Azure AD 관리 센터](https://aad.portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.

   ![사용자 관리 열기](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Hello에 **사용자 및 그룹** 블레이드를 **회사 브랜딩**합니다.
4. Hello에 **사용자 및 그룹-회사 브랜딩** 블레이드, 선택 hello **언어 추가** 명령입니다.

    ![언어별 브랜딩 요소 추가](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Toocustomize hello 요소를 수정 합니다. 모든 요소는 선택 사항입니다.
6. **Save**를 클릭합니다.

변경한 모든 toohello 로그인 페이지 브랜딩 tooappear에 대 한 tooan 시간까지 걸릴 수 있으므로 합니다.

## <a name="next-steps"></a>다음 단계
이 퀵 스타트의 tooadd 브랜딩 tooyour Azure AD 디렉터리를 회사 하는 방법을 배웠습니다. 

다음 링크 tooconfigure hello에서 Azure AD에서 Azure 포털 브랜딩 회사 hello를 사용할 수 있습니다.

> [!div class="nextstepaction"]
> [회사 브랜딩 구성](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 