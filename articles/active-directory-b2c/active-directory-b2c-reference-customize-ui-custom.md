---
title: "Azure Active Directory B2C: 참조: hello 사용자 지정 정책을 사용 하 여 사용자 작업의 UI 사용자 지정 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책에 대한 항목"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Hello 사용자 지정 정책을 사용 하 여 사용자 작업의 UI 사용자 지정

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> 이 문서는 UI 사용자 지정의 작동 방식 및 방법을 사용 하 여 B2C 사용자 지정 정책 사용 하 여 tooenable hello Id 경험 프레임 워크에 대 한 고급 설명


비즈니스-소비자 솔루션에서는 원활한 사용자 환경이 핵심입니다. 원활한 사용자 환경에서 장치 또는 브라우저를 사용 하는 hello 고객 서비스의 서비스를 통해 사용자의 여정을 구별할 수 없으며에 된 경험을 의미 합니다.

## <a name="understand-hello-cors-way-for-ui-customization"></a>UI 사용자 지정에 대 한 hello CORS 방법을 이해합니다

Azure AD B2C 수 있도록 허용 하면 toocustomize hello 모양 및 느낌과 (UX) 사용자 환경의 hello에 잠재적으로 제공 및 사용자 지정 사용자 정책을 통해 Azure AD B2C 하 여 표시 될 수 있는 여러 페이지

이 위해 Azure AD B2C 소비자의 브라우저에서 코드를 실행 하 고 사용 하 여 hello 현대적이 고 표준 접근 방식을 [크로스-원본 자원 공유 (CORS)](http://www.w3.org/TR/cors/) tooload 사용자 지정 정책에 지정 하는 특정 URL에서 사용자 지정 콘텐츠 toopoint tooyour HTML5/CSS 템플릿입니다. CORS는 hello 리소스의 원본이 되는 hello 도메인 외부의 다른 도메인에서 요청 된 웹 페이지 toobe에 글꼴 등 제한 된 리소스를 허용 하는 메커니즘입니다.

Toohello 이전 전통적인 방식 템플릿 페이지 제한 된 텍스트를 제공 하 고 여기서 레이아웃 및 느낌의 제한 된 제어 하는 데 문제가 tooachieve 원활한 환경 보다 선행 toomore 공급, 이미지, CORS hello hello 솔루션이 소유한 비교 HTML5 및 CSS를 지원 하 고 수를 허용 하는 방법:

- Hello 콘텐츠를 호스트 하 고 hello 솔루션을 삽입 합니다. 클라이언트 쪽 스크립트를 사용 하 여 해당 컨트롤입니다.
- 레이아웃과 느낌의 모든 픽셀을 완벽하게 제어할 수 있습니다.

HTML5/CSS 파일을 적절하게 선별하여 원하는 만큼 콘텐츠 페이지를 제공할 수 있습니다.

> [!NOTE]
> 보안상의 이유로 hello를 사용 하 여 JavaScript의 현재 차단 된 사용자 지정 합니다. JavaScript를 사용 하 여 Azure AD B2C 테 넌 트에 대 한 사용자 지정 도메인 이름의 toounblock 필요 합니다.

각 HTML5/CSS 서식 파일에서 제공 하는 *앵커* 필요한 toohello에 해당 하는 요소를 `<div id=”api”>` hello HTML 또는 hello 콘텐츠 페이지에서이 설명으로 요소입니다. Azure AD B2C에서는 모든 콘텐츠 페이지에 이 특정 div가 있어야 합니다.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Azure AD B2C 관련 내용을 hello 페이지 삽입 되는 hello 페이지의 나머지 부분 hello 하는 동안이 div는 원하는 대로 toocontrol 합니다. Azure AD B2C hello JavaScript 코드에는이 특정 div 요소를 삽입 하는 HTML를 콘텐츠에 가져오며 합니다. Hello 다음 적절 하 게 컨트롤을 삽입 하는 azure AD B2C: 계정 선택 컨트롤, login 컨트롤, multi-factor (전화 기반 현재) 컨트롤 및 특성 컬렉션 컨트롤입니다. Azure AD B2C를 수행 하면 모든 hello 컨트롤은 규정을 준수 하 고 액세스 가능한 HTML5, 모든 hello 컨트롤 완전히 스타일을 지정할 수 제어 버전 이전 상태로 되돌아갈 되지 것입니다.

hello 병합 된 콘텐츠는 결국 표시 hello 동적 문서 tooyour 소비자로.

위의 hello의 tooensure 예상 대로 작동 해야 합니다.

- 콘텐츠가 HTML5 호환되고 액세스 가능해야 함
- 콘텐츠 서버가 CORS에 대해 사용하도록 설정되어야 함
- HTTPS를 통해 콘텐츠를 제공
- 모든 링크 및 CSS 콘텐츠에 대해 절대 URL(예: https://yourdomain/content) 사용

> [!TIP]
> 사이트에 콘텐츠를 호스팅하는 hello tooverify 사용 하도록 설정 하는 CORS 개이고 테스트 CORS 요청, hello 사이트 http://test-cors.org/를 사용할 수 있습니다. 감사 toothis 사이트 있습니다 수 단순히 보내기 hello CORS 요청 tooa 원격 서버 (tootest CORS 지원 되는 경우) 또는 보내기 hello CORS 요청 tooa 테스트 서버 (tooexplore CORS의 특정 기능은).

> [!TIP]
> 또한 hello 사이트 http://enable-cors.org/ CORS에 유용한 리소스 보다 더를 구성합니다.

고마워요 CORS 기반 접근 방식을 toothis hello 최종 사용자가 응용 프로그램 및 Azure AD B2C에서 제공 하는 hello 페이지 간에 일관 된 환경을 제공 합니다.

## <a name="create-a-storage-account"></a>저장소 계정 만들기

필수 구성 요소를 저장소 계정 toocreate를 해야합니다. Azure 구독 toocreate Azure Blob 저장소 계정이 필요 합니다. Hello에 무료 평가판에 등록할 수 [Azure 웹 사이트](https://azure.microsoft.com/en-us/pricing/free-trial/)합니다.

1. 검색 세션을 열고 toohello 이동 [Azure 포털](https://portal.azure.com)합니다.
2. 관리자 자격 증명으로 로그인합니다.
3. **새로 만들기** > **데이터 + 저장소** > **저장소 계정**을 클릭합니다.  **저장소 계정 만들기** 블레이드가 열립니다.
4. **이름**, 예를 들어 hello 저장소 계정의 이름을 제공 *contoso369b2c*합니다. 이 값은 나중에 라고 너무*storageAccountName*합니다.
5. 가격 책정 계층, hello 리소스 그룹 및 hello 구독 hello에 대 한 hello 적절 한 선택 항목을 선택 합니다. Hello 갖도록 **Pin tooStartboard** 옵션을 선택 합니다. **만들기**를 클릭합니다.
6. 시작 보드 toohello와 방금 만든 hello 저장소 계정을 클릭 하십시오.
7. Hello에 **서비스** 섹션에서 클릭 **Blob**합니다. **Blob service 블레이드**가 열립니다.
8. **+ 컨테이너**를 클릭합니다.
9. **이름**, 예를 들어 hello 컨테이너에 대 한 이름을 제공 *b2c*합니다. 이 값은 됩니다 나중에 참조 된 tooas *containerName*합니다.
9. 선택 **Blob** hello로 **액세스 형식**합니다. **만들기**를 클릭합니다.
10. 만든 hello 컨테이너에서 hello hello 목록에 표시 됩니다 **Blob 서비스 블레이드**합니다.
11. 닫기 hello **Blob** 블레이드입니다.
12. Hello에 **저장소 계정 블레이드**, hello 클릭 **키** 아이콘입니다. **액세스 키 블레이드**가 열립니다.  
13. Hello 수가 적어 **key1**합니다. 이 값은 나중에 *key1*로 참조됩니다.

## <a name="downloading-hello-helper-tool"></a>Hello 도우미 도구를 다운로드합니다.

1.  Hello 도우미 도구를 다운로드할 [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip)합니다.
2.  Hello 저장 *AzureBlobStorage 클라이언트 master.zip B2C* 로컬 컴퓨터의 파일입니다.
3.  Hello 콘텐츠 hello AzureBlobStorage 클라이언트 master.zip B2C hello 아래 예를 들어 로컬 디스크에 있는 파일의 압축 **UI 사용자 지정 팩** 폴더입니다. 그러면 그 아래 *B2C-AzureBlobStorage-Client-master* 폴더가 생성됩니다.
4.  해당 폴더를 열고 hello 콘텐츠 hello 보관 파일의 압축 *B2CAzureStorageClient.zip* 그 안에 있습니다.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Hello UI 사용자 지정 팩 샘플 파일 업로드

1.  Windows 탐색기를 사용 하 여 이동 toohello 폴더 *AzureBlobStorage 클라이언트 마스터 B2C* hello 아래에 있는 *UI 사용자 지정 팩* hello 이전 섹션에서 만든 폴더에 있습니다.
2.  Hello 실행 *B2CAzureStorageClient.exe* 파일입니다. 이 프로그램 tooyour 저장소 계정을 지정 하 고 해당 파일에 대 한 CORS 액세스를 사용 하는 hello 디렉터리에서 모든 hello 파일을 업로드 하기만 합니다.
3.  메시지가 표시되면 다음을 지정합니다. a.  저장소 계정의 이름 hello *storageAccountName*, 예를 들어 *contoso369b2c*합니다.
    b.  azure blob 저장소의 기본 액세스 키 hello *key1*, 예를 들어 *contoso369b2c*합니다.
    c.  저장소 blob 저장소 컨테이너의 hello 이름 *containerName*, 예를 들어 *b2c*합니다.
    d.  hello의 hello 경로 *스타터 팩* 샘플 파일, 예를 들어 *... \B2CTemplates\wingtiptoys*합니다.

위의 hello 단계를 따른 경우 hello hello의 HTML5 및 CSS 파일 *UI 사용자 지정 팩* 가상의 회사인 hello **wingtiptoys** tooyour 저장소 계정을 가리키는 이제 됩니다.  Hello 관련된 컨테이너 블레이드 hello Azure 포털에서에서 열어 hello 콘텐츠가 올바르게 업로드 되었는지 확인할 수 있습니다. 또는 브라우저에서 hello 페이지에 액세스 하 여 hello 콘텐츠가 올바르게 업로드 되었는지 확인할 수 있습니다. 자세한 내용은 참조 [Azure Active Directory B2C: toodemonstrate hello 페이지 사용자 인터페이스 (UI) 사용자 지정 기능을 사용 하는 도우미 도구](active-directory-b2c-reference-ui-customization-helper-tool.md)합니다.

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>Hello 저장소 계정에 CORS 사용

CORS (크로스-원본 자원 공유) 해야 콘텐츠 tooload Azure AD B2C 프리미엄에 대 한 끝점에서 사용 하도록 설정 합니다. 즉, Azure AD B2C 프리미엄 hello 도메인에서 hello 페이지를 제공 합니다 보다 콘텐츠 다른 도메인에서 호스팅됩니다.

tooverify에 콘텐츠를 호스팅하는 hello 저장소가 사용 하도록 설정 하는 CORS를 포함 하는 단계를 수행 하는 hello로 계속:

1. 검색 세션을 열고 toohello 페이지를 이동 *unified.html* hello 저장소 계정의 위치의 전체 URL을 사용 하 여 `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`합니다. 예를 들면, https://contoso369b2c.blob.core.windows.net/b2c/unified.html입니다.
2. Toohttp://test-cors.org를 이동 합니다. 이 사이트 있습니다 tooverify 페이지를 사용 하는 hello를 사용 하도록 설정 하는 CORS가 수 있습니다.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. **원격 URL**unified.html 콘텐츠용으로 hello 전체 URL을 입력 하 고 클릭 **요청 보내기**합니다.
4. Hello에 해당 hello 출력 확인 **결과** 섹션에 포함 되어 *XHR 상태: 200*합니다. 이것은 CORS가 사용하도록 설정되었음을 나타냅니다.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
저장소 계정 hello 라는 blob 컨테이너 포함 *b2c* hello에서 wingtiptoys 서식 파일을 다음 hello를 포함 하는 그림에 *스타터 팩*합니다.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

hello 다음 표에 HTML5 페이지 위에 hello hello 목적이 있습니다.

| HTML5 템플릿 | 설명 |
|----------------|-------------|
| *phonefactor.html* | 이 페이지를 Multi-Factor Authentication 페이지에 대한 템플릿으로 사용할 수 있습니다. |
| *resetpassword.html* | 이 페이지를 암호 찾기 페이지에 대한 템플릿으로 사용할 수 있습니다. |
| *selfasserted.html* | 이 페이지를 소셜 계정 등록 페이지, 로컬 계정 등록 페이지 또는 로컬 계정 로그인 페이지에 대한 템플릿을 사용할 수 있습니다. |
| *unified.html* | 이 페이지를 통합 등록 또는 로그인 페이지에 대한 템플릿으로 사용할 수 있습니다. |
| *updateprofile.html* | 이 페이지를 프로필 업데이트 페이지에 대한 템플릿으로 사용할 수 있습니다. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>링크 tooyour HTML5/CSS 템플릿 tooyour 사용자 여행 추가

사용자 지정 정책을 직접 편집 하 여는 링크 tooyour HTML5/CSS 템플릿 tooyour 사용자 여행을 추가할 수 있습니다.

hello 사용자 지정 HTML5/CSS 템플릿 toouse 사용자 여정에서 toobe 해당 사용자 친구에 사용할 수 있는 콘텐츠 정의의 목록에 지정 된 경우 이 위해 선택적  *<ContentDefinitions>*  hello에서 XML 요소를 선언 해야  *<BuildingBlocks>*  사용자 지정 정책 XML 파일의 섹션입니다.

hello 다음 설명 hello 집합이 hello Azure AD B2C identity 경험 엔진 및 toothem 관련 된 페이지 hello 종류로 인식 콘텐츠 정의 id입니다.

| 콘텐츠 정의 ID | 설명 |
|-----------------------|-------------|
| *api.error* | **오류 페이지**입니다. 예외 또는 오류가 발생하면 이 페이지가 표시됩니다. |
| *api.idpselections* | **ID 공급자 선택 페이지**입니다. 이 페이지에는 로그인 시 사용자 hello 공급자에서 선택할 수는 id의 목록을 포함 합니다. Facebook, Google+ 또는 로컬 계정(이메일 주소 또는 사용자 이름 기반)과 같은 소셜 ID 공급자, 엔터프라이즈 ID 공급자입니다. |
| *api.idpselections.signup* | **등록을 위한 ID 공급자 선택 페이지**입니다. 이 페이지에는 사용자 hello 공급자 등록 중에서 선택할 수는 id의 목록을 포함 합니다. Facebook, Google+ 또는 로컬 계정(이메일 주소 또는 사용자 이름 기반)과 같은 소셜 ID 공급자, 엔터프라이즈 ID 공급자입니다. |
| *api.localaccountpasswordreset* | **암호 찾기 페이지**입니다. 이 페이지에서는 폼 해당 hello 사용자에 게 toofill tooinitiate가 암호 다시 설정 합니다.  |
| *api.localaccountsignin* | **로컬 계정 로그인 페이지**입니다. 이 페이지에서는 로그인 폼 해당 hello 사용자 사용자 이름 또는 전자 메일 주소를 기반으로 하는 로컬 계정을 사용해 로그인 하는 경우에 toofill을 포함 합니다. hello 폼에 텍스트 입력된 상자 및 암호 입력 상자가 포함 될 수 있습니다. |
| *api.localaccountsignup* | **로컬 계정 등록 페이지**입니다. 이 페이지에서는 등록 양식에 해당 hello 사용자에 게 toofill 사용자 이름 또는 전자 메일 주소를 기반으로 하는 로컬 계정에 등록 하는 경우. hello 양식 텍스트 입력된 상자, 암호 입력 상자, 라디오 단추, 단일 선택 드롭다운 목록 상자, 다중 선택 확인란 등 서로 다른 입력된 컨트롤을 포함할 수 있습니다. |
| *api.phonefactor* | **Multi-Factor Authentication 페이지**. 이 페이지에서 등록 또는 로그인하는 동안 사용자가 텍스트 또는 음성을 사용하여 전화 번호를 확인할 수 있습니다. |
| *api.selfasserted* | **소셜 계정 등록 페이지**입니다. 이 페이지에서는 등록 양식에 hello이 사용자는 Facebook 또는 Google +와 같은 소셜 id 공급자에서 때 계정을 기존를 사용 하 여 등록에서 toofill 합니다. 이 페이지는 hello 암호 입력 필드의 hello 예외로 소셜 계정 등록 페이지의 위쪽 비슷한 toohello입니다. |
| *api.selfasserted.profileupdate* | **프로필 업데이트 페이지**입니다. 이 페이지에서는 폼 hello 사용자 tooupdate 해당 프로필을 사용할 수 있습니다. 이 페이지는 hello 암호 입력 필드의 hello 예외로 소셜 계정 등록 페이지의 위쪽 비슷한 toohello입니다. |
| *api.signuporsignin* | **통합 등록 또는 로그인 페이지**.  이 페이지는 Facebook, Google+ 또는 로컬 계정과 같은 소셜 ID 공급자, 엔터프라이즈 ID 공급자를 사용할 수 있는 사용자의 등록 및 로그인을 모두 다룹니다.

## <a name="next-steps"></a>다음 단계
[참조: 방법을 사용자 지정 정책을 이해 hello B2C에 Id 경험 프레임 워크로 작동](active-directory-b2c-reference-custom-policies-understanding-contents.md)
