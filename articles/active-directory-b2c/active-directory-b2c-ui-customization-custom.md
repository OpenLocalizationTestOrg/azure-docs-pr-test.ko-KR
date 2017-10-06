---
title: "사용자 지정 정책을 사용하여 UI 사용자 지정 - Azure AD B2C | Microsoft Docs"
description: "Azure AD B2C에서 사용자 지정 정책을 사용하는 동안 UI(사용자 인터페이스)를 사용자 지정하는 방법에 대해 알아봅니다."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Azure Active Directory B2C: 사용자 지정 정책에서 UI 사용자 지정 구성

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

이 문서를 완료하면 브랜드와 모양이 포함된 등록 및 로그인 사용자 지정 정책을 갖습니다. 와 Azure Active Directory B2C (Azure AD B2C) hello HTML 및 CSS 콘텐츠의 거의 모든 권한 있는 게 toousers 제시한 합니다. 사용자 지정 정책을 사용 하는 경우 구성한 UI 사용자 지정 xml에서 hello Azure 포털에서에서 컨트롤을 사용 하는 대신 합니다. 

## <a name="prerequisites"></a>필수 조건

시작하기 전에 먼저 [사용자 지정 정책 시작](active-directory-b2c-get-started-custom.md)을 완료합니다. 로컬 계정을 사용하여 등록 및 로그인하기 위한 사용자 지정 정책이 작동해야 합니다.

## <a name="page-ui-customization"></a>페이지 UI 사용자 지정

Hello 페이지 UI 사용자 지정 기능을 사용 하 여 hello의 디자인을 사용자 지정 정책 사용자 지정할 수 있습니다. 또한 응용 프로그램과 Azure AD B2C 간에 브랜드와 시각적 개체 일관성을 유지할 수 있습니다.

작동 방식은 다음과 같습니다. Azure AD B2C는 소비자의 브라우저에서 코드를 실행하고 [CORS(원본 간 리소스 공유)](http://www.w3.org/TR/cors/)라는 최신의 방법을 사용합니다. 첫째, 사용자 지정 된 HTML 콘텐츠가 있는 사용자 지정 정책 hello에에서 URL을 지정 합니다. Azure AD B2C hello URL에서 로드 되 고 다음 hello 페이지 toohello 고객을 표시 하는 HTML 콘텐츠를 사용 하 여 UI 요소를 병합 합니다.

## <a name="create-your-html5-content"></a>HTML5 콘텐츠 만들기

Hello 제목에 HTML 콘텐츠를 제품의 브랜드 이름을 만듭니다.

1. 다음 HTML 코드 조각을 hello를 복사 합니다. 올바른 형식이 HTML5 빈 요소와 함께 호출 * \<div id = "api"\>\</div\> * hello 내에 있는 * \<본문\> * 태그입니다. 이 요소는 Azure AD B2C 콘텐츠인지 toobe 삽입 위치를 나타냅니다.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >보안상의 이유로 hello를 사용 하 여 JavaScript의 현재 차단 된 사용자 지정 합니다.

2. 텍스트 편집기에 복사 hello 조각을 다음으로 hello 파일을 저장 *사용자 지정 ui.html*합니다.

## <a name="create-an-azure-blob-storage-account"></a>Azure Blob 저장소 계정 만들기

>[!NOTE]
> 이 문서에서 사용 하 여 Azure Blob 저장소 toohost 콘텐츠입니다. 웹 서버에서 콘텐츠 toohost를 선택할 수 있지만 해야 [CORS 웹 서버에서 사용할](https://enable-cors.org/server.html)합니다.

toohost Blob 저장소에이 HTML 콘텐츠에 따라 hello지 않습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **허브** 메뉴 선택 **새로** > **저장소** > **저장소 계정**합니다.
3. 저장소 계정의 고유한 **이름**을 입력합니다.
4. **배포 모델**은 **Resource Manager**로 유지하면 됩니다.
5. 변경 **계정 종류** 너무**Blob 저장소**합니다.
6. **성능**은 **표준**으로 유지하면 됩니다.
7. **복제**는**RA-GRS**로 유지하면 됩니다.
8. **액세스 계층**은 **핫**으로 유지하면 됩니다.
9. **저장소 서비스 암호화**는 **사용 안 함**으로 유지하면 됩니다.
10. 저장소 계정에 대한 **구독**을 선택합니다.
11. **리소스 그룹**을 만들거나 기존 그룹을 선택합니다.
12. 선택 hello **지리적 위치** 저장소 계정에 대 한 합니다.
13. 클릭 **만들기** toocreate hello 저장소 계정입니다.  
    Hello 배포가 완료 된 후 hello **저장소 계정** 블레이드 자동으로 열립니다.

## <a name="create-a-container"></a>컨테이너 만들기

Blob 저장소에서 공개 컨테이너 toocreate 다음 hello지 않습니다.

1. Hello 클릭 **개요** 탭 합니다.
2. **컨테이너**를 클릭합니다.
3. **이름**으로 **$root**를 입력합니다.
4. 설정 **액세스 형식** 너무**Blob**합니다.
5. 클릭 **$root** tooopen hello 새 컨테이너입니다.
6. **업로드**를 클릭합니다.
7. 다음 너무 hello 폴더 아이콘을 클릭**파일 선택**합니다.
8. 너무 이동**사용자 지정 ui.html**, hello 앞부분에서 만든 [페이지 UI 사용자 지정](#the-page-ui-customization-feature) 섹션.
9. **업로드**를 클릭합니다.
10. 업로드 hello ui.html 사용자 지정 blob을 선택 합니다.
11. 다음 너무**URL**, 클릭 **복사**합니다.
12. 브라우저에서 hello 복사한 URL을 붙여 넣고 toohello 사이트 이동 합니다. Hello 사이트에 액세스할 수 없는 경우 hello 컨테이너 액세스 형식을 너무 설정 되어 있는지 확인**blob**합니다.

## <a name="configure-cors"></a>CORS 구성

Hello 다음을 수행 하 여 크로스-원본 자원 공유에 대 한 Blob 저장소를 구성 합니다.

>[!NOTE]
>샘플 HTML 및 CSS 콘텐츠를 사용 하 여 hello UI 사용자 지정 기능을 미리 tootry를 선택 하십시오. Azure Blob 저장소 계정에 샘플 콘텐츠를 업로드하고 구성하는 [간단한 도우미 도구](active-directory-b2c-reference-ui-customization-helper-tool.md)를 제공했습니다. Hello 도구를 사용 하면 건너뛰어 너무[등록 또는 로그인 시 사용자 지정 정책을 수정](#modify-your-sign-up-or-sign-in-custom-policy)합니다.

1. Hello에 **저장소** 블레이드 아래 **설정**개방형 **CORS**합니다.
2. **추가**를 클릭합니다.
3. **허용된 원본**의 경우 별표(\*)를 입력합니다.
4. Hello에 **허용 된 동사** 드롭 다운 목록, 선택 **가져오기** 및 **옵션**합니다.
5. **허용된 헤더**의 경우 별표(\*)를 입력합니다.
6. **노출된 헤더**의 경우 별표(\*)를 입력합니다.
7. **최대 기간(초)**의 경우 **200**을 입력합니다.
8. **추가**를 클릭합니다.

## <a name="test-cors"></a>CORS 테스트

준비가 되 hello 다음을 수행 하 여 확인 합니다.

1. Toohello 이동 [테스트 cors.org](http://test-cors.org/) 웹 사이트로 이동한 다음 hello에 붙여넣기 hello URL **원격 URL** 상자입니다.
2. **요청 보내기**를 클릭합니다.  
    오류가 발생하는 경우 [CORS 설정](#configure-cors)이 올바른지 확인합니다. Tooclear 브라우저 캐시를 필요 또는 Ctrl + Shift + P를 눌러 개인 탐색 세션을 열 수 있습니다.

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>등록 또는 로그인 사용자 지정 정책 수정

최상위 hello에서 * \<TrustFrameworkPolicy\> * 태그를 찾아야 * \<직접\> * 태그입니다. Hello 내 * \<직접\> * 태그, 추가 * \<ContentDefinitions\> * hello 다음 예제를 복사 하 여는 태그입니다. 대체 *your_storage_account* hello 저장소 계정 이름을 사용 합니다.

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>업데이트된 사용자 지정 정책 업로드

1. Hello에 [Azure 포털](https://portal.azure.com), [Azure AD B2C 테 넌 트의 hello 컨텍스트로 전환](active-directory-b2c-navigate-to-b2c-context.md)를 연 다음 hello **Azure AD B2C** 블레이드 합니다.
2. **모든 정책**을 클릭합니다.
3. **업로드 정책**을 클릭합니다.
4. 업로드 `SignUpOrSignin.xml` hello로 * \<ContentDefinitions\> * 태그 이전에 추가 합니다.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Hello 사용자 지정 정책을 사용 하 여 테스트 **지금 실행**

1. Hello에 **Azure AD B2C** 블레이드에서 너무 이동**정책을 모든**합니다.
2. 업로드 하는 hello 사용자 지정 정책을 선택 하 고 hello 클릭 **지금 실행** 단추입니다.
3. 전자 메일 주소를 사용 하 여를 toosign 수 있어야 합니다.

## <a name="reference"></a>참조

UI 사용자 지정을 위한 샘플 템플릿은 다음에서 찾을 수 있습니다.

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

hello sample_templates/wingtip 폴더 hello를 다음 HTML 파일이 포함 되어 있습니다.

| HTML5 템플릿 | 설명 |
|----------------|-------------|
| *phonefactor.html* | 다단계 인증 페이지의 템플릿으로 사용합니다. |
| *resetpassword.html* | 암호 찾기 페이지의 템플릿으로 사용합니다. |
| *selfasserted.html* | 소셜 계정 등록 페이지, 로컬 계정 등록 페이지 또는 로컬 계정 로그인 페이지의 템플릿으로 사용합니다. |
| *unified.html* | 통합 등록 또는 로그인 페이지의 템플릿으로 사용합니다. |
| *updateprofile.html* | 프로필 업데이트 페이지의 템플릿으로 사용합니다. |

Hello에 [등록 또는 로그인 시 사용자 지정 정책 섹션은 수정](#modify-your-sign-up-or-sign-in-custom-policy), hello에 대 한 콘텐츠 정의 구성 `api.idpselections`합니다. 콘텐츠 정의 hello Azure AD B2C id 경험 프레임 워크와 해당 설명을 보려면에서 인식 하는 Id의 전체 집합 hello는 다음 표에 hello에 있습니다.

| 콘텐츠 정의 ID | 설명 | 
|-----------------------|-------------|
| *api.error* | **오류 페이지**입니다. 예외 또는 오류가 발생하면 이 페이지가 표시됩니다. |
| *api.idpselections* | **ID 공급자 선택 페이지**입니다. 이 페이지에는 로그인 시 사용자 hello 공급자에서 선택할 수는 id의 목록을 포함 합니다. 이러한 옵션은 엔터프라이즈 ID 공급자, 소셜 ID 공급자(예: Facebook, Google+) 또는 로컬 계정입니다. |
| *api.idpselections.signup* | **등록을 위한 ID 공급자 선택 페이지**입니다. 이 페이지에는 사용자 hello 공급자 등록 중에서 선택할 수는 id의 목록을 포함 합니다. 이러한 옵션은 엔터프라이즈 ID 공급자, 소셜 ID 공급자(예: Facebook, Google+) 또는 로컬 계정입니다. |
| *api.localaccountpasswordreset* | **암호 찾기 페이지**입니다. 이 페이지에서는 폼 hello 사용자 암호 재설정 tooinitiate 완료 해야 합니다.  |
| *api.localaccountsignin* | **로컬 계정 로그인 페이지**입니다. 이메일 주소 또는 사용자 이름을 기반으로 하는 로컬 계정으로 로그인하기 위한 양식이 있습니다. hello 폼에 텍스트 입력된 상자 및 암호 입력 상자가 포함 될 수 있습니다. |
| *api.localaccountsignup* | **로컬 계정 등록 페이지**입니다. 이메일 주소 또는 사용자 이름을 기반으로 하는 로컬 계정을 등록하기 위한 양식이 있습니다. hello 폼에 텍스트 입력된 상자, 암호 입력 상자, 라디오 단추, 단일 선택 드롭다운 목록 상자 및 확인란 여러 개 선택 등의 다양 한 입력된 컨트롤에 포함 될 수 있습니다. |
| *api.phonefactor* | **Multi-Factor Authentication 페이지**입니다. 등록 또는 로그인 중에 사용자가 이 페이지에서 텍스트 또는 음성을 사용하여 전화 번호를 확인할 수 있습니다. |
| *api.selfasserted* | **소셜 계정 등록 페이지**입니다. 소셜 ID 공급자(예: Facebook 또는 Google+)에서 기존 계정을 사용하여 등록할 때 사용자가 완성해야 하는 등록 양식이 있습니다. 이 페이지는 hello 암호 입력 필드를 제외 하 고 소셜 계정 등록 페이지를 앞으로 유사한 toohello입니다. |
| *api.selfasserted.profileupdate* | **프로필 업데이트 페이지**입니다. 이 페이지는 사용자가 사용할 수 있는 tooupdate 자신의 프로필 폼을 포함 합니다. 이 페이지는 비슷한 toohello 소셜 계정 등록 페이지 hello 암호 입력 필드를 제외 하 고 있습니다. |
| *api.signuporsignin* | **통합 등록 또는 로그인 페이지**입니다. 이 페이지는 모두 hello 등록 및 로그인의 엔터프라이즈 id 공급자, Facebook 또는 Google + 또는 로컬 계정 등과 같은 소셜 id 공급자를 사용할 수 있는 사용자를 처리 합니다.  |

## <a name="next-steps"></a>다음 단계

사용자 지정할 수 있는 UI 요소에 대한 추가 정보는 [기본 제공 정책의 UI 사용자 지정을 위한 참조 가이드](active-directory-b2c-reference-ui-customization.md)를 참조하세요.
