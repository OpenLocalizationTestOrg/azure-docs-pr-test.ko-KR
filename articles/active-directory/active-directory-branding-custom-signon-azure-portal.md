---
title: "페이지 hello Azure Active Directory에서에서 로그인에 aaaCustomize | Microsoft Docs"
description: "자세한 내용은 방법 tooadd 회사 브랜딩 toohello Azure 로그인 페이지"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>회사 hello Azure Active Directory에서에서 tooyour 로그인 페이지 브랜딩 추가
tooavoid 혼동 많은 회사 모든 hello 웹 사이트 및 서비스 관리 tooapply 일관 된 모양과 느낌을 원합니다. Azure Active Directory 회사 로고 및 사용자 지정 색 구성표와 hello 로그인 페이지의 toocustomize hello 모양을 허용 하 여이 기능을 제공 합니다. hello 로그인 페이지에는 365 또는 id 공급자로 Azure AD를 사용 하는 다른 웹 기반 응용 프로그램 tooOffice에 로그인 할 때 표시 되는 hello 페이지가입니다. 자격 증명 페이지 tooenter이 상호 작용합니다.

회사 브랜드, 색 및이 페이지의 다른 사용자 지정 가능한 요소 tooshow를 원하는 경우 hello hello 두 환경 간의 이미지 toounderstand hello 차이 다음을 참조 하십시오.

다음 스크린 샷에 표시 및 데스크톱 컴퓨터에 Office 365 hello 로그인 페이지에 대 한 예제 hello **전에** 는 사용자 지정:

![사용자 지정하기 전 Office 365 로그인 페이지](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

다음 스크린 샷에 표시 및 데스크톱 컴퓨터에 Office 365 hello 로그인 페이지에 대 한 예제 hello **후** 는 사용자 지정:

![사용자 지정한 후 Office 365 로그인 페이지](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Hello 로그인 페이지 사용자 지정
일반적으로 조직이 구독 하는 브라우저 기반 액세스 tooyour 클라우드 앱과 서비스를 필요 하면 hello 로그인 페이지를 사용 합니다.

변경 내용 tooyour 로그인 페이지를 적용 한 경우 변경 내용 tooappear hello에 대 한 tooan 시간까지 걸릴 수 있으므로 합니다.

https://outlook.com/**contoso**.com 또는 https://mail.**contoso**.com과 같은 테넌트 특정 URL로 서비스를 이용할 경우 브랜드가 지정된 로그인 페이지만이 나타납니다.

비테넌트 특정 URL (예: https://mail.office365.com ) 을 사용하여 서비스에 방문하는 경우 브랜드가 지정되지 않은 로그인 페이지가 나타납니다. 이 경우에 사용자 ID를 입력하거나 사용자 타일을 선택하면 브랜딩이 나타납니다.

> [!NOTE]
> * Hello에 도메인 이름이 "활성"으로 표시 해야 **도메인** 부분의 hello를 브랜딩을 구성한 Azure 포털입니다. 자세한 내용은 [사용자 지정 도메인 이름 추가](active-directory-domains-add-azure-portal.md)를 참조하세요.
> * 로그인 페이지 브랜딩 toohello 소비자 로그인 페이지의 Microsoft 적용 되지 않습니다. Microsoft 계정으로 로그인 하는 경우 Azure AD를 통해 렌더링 된 사용자 타일의 브랜드가 지정 된 목록이 표시 될 수 있지만 조직의 hello 브랜딩 toohello Microsoft 계정 로그인 페이지는 적용 되지 않습니다.
>
>

로그인 페이지에 hello **로그인 상태 유지** 확인란을 사용 하는 사용자 tooremain 닫고 브라우저를 다시 열 때 로그인 합니다.

   ![로그인 유지](./media/active-directory-branding-custom-signon-azure-portal/01.png)

세션 수명에는 영향을 미치지 않습니다. Hello Azure Active Directory 로그인 페이지 hello 확인란을 숨길 수 있습니다.
hello 설정에 따라 hello 확인란이 표시 되는 여부 **사용 안 함에**합니다.

   ![로그인 유지](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide hello 확인란, 너무이 설정을 구성 하**예**합니다.

> [!NOTE]
> SharePoint Online 및 Office 2010의 일부 기능은이 상자 toocheck 수 있는 사용자가에 따라 다릅니다. 이 설정은 toohidden를 구성 하면 toosign 기능을 추가 및 예기치 않은 메시지가 나타나면 사용자가 볼 수 있습니다.
>
>

**tooadd 회사 브랜딩 tooyour 디렉터리:**

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.
2. 선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.

   ![사용자 관리 열기](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Hello에 **사용자 및 그룹** 블레이드를 **회사 브랜딩**합니다.
4. Hello에 **사용자 및 그룹-회사 브랜딩** 블레이드, 선택 hello **편집** 명령입니다.

    ![사용자 지정 브랜딩 편집](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Toocustomize hello 요소를 수정 합니다. 모든 요소는 선택 사항입니다.
6. **Save**를 클릭합니다.

변경한 모든 toohello 로그인 페이지 브랜딩 tooappear에 대 한 tooan 시간까지 걸릴 수 있으므로 합니다.

## <a name="next-steps"></a>다음 단계
[언어별 회사 브랜딩 추가](active-directory-branding-localize-azure-portal.md)
