---
title: "Azure Active Directory B2C: 페이지 UI 사용자 지정 도우미 도구 | Microsoft Docs"
description: "Azure Active Directory B2C에서 toodemonstrate hello 페이지 UI 사용자 지정 기능을 사용 하는 도우미 도구"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>Azure Active Directory B2C: 도우미 도구 toodemonstrate hello 페이지 사용자 인터페이스 (UI) 사용자 지정 기능 사용
이 문서는 도우미 toohello [주 UI 사용자 지정 문서](active-directory-b2c-reference-ui-customization.md) (Azure AD) Azure Active Directory B2C에 있습니다. hello 다음 단계에서는 tooexercise 나와 있는 샘플 HTML 및 CSS 콘텐츠를 사용 하 여 페이지 UI 사용자 지정 기능을 hello 하는 방법.

## <a name="get-an-azure-ad-b2c-tenant"></a>Azure AD B2C 테넌트 가져오기
전에 아무 것도 사용자 지정할 수 있어야 합니다 너무[Azure AD B2C 테 넌 트를 가져오는](active-directory-b2c-get-started.md) 아직 없는 경우.

## <a name="create-a-sign-up-or-sign-in-policy"></a>등록 또는 로그인 정책 만들기
hello 나와 샘플 콘텐츠 수에 사용 되는 toocustomze 두 페이지는 [등록 또는 로그인 시 정책](active-directory-b2c-reference-policies.md): hello [통합된 로그인 페이지](active-directory-b2c-reference-ui-customization.md) 및 hello [자체 어설션된 특성페이지](active-directory-b2c-reference-ui-customization.md). [등록 또는 로그인 정책을 만드는](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy)경우 로컬 계정(메일 주소), Facebook, Google 및 Microsoft를 **ID 공급자**로 추가합니다. 이러한 샘플 HTML 콘텐츠가 수락할 IDPs만 hello 됩니다.  또한 원하는 경우 이러한 IDP의 하위 집합을 추가할 수 있습니다.

## <a name="register-an-application"></a>응용 프로그램 등록
너무 필요 합니다[응용 프로그램 등록](active-directory-b2c-app-registration.md) 에 프로그램 B2C 테 넌 트를 사용 하는 tooexecute 정책 일 수 있습니다. 응용 프로그램을 등록 한 후는 몇 가지 옵션을 tooactually 등록 정책 실행을 사용할 수 있습니다.

* Hello Azure AD B2C hello "시작" 섹션에 나열 된 빠른 시작 응용 프로그램 중 하나를 빌드 [로그인 및 사용자가 응용 프로그램에 로그인](active-directory-b2c-overview.md#get-started)합니다.
* 사용 하 여 hello 미리 작성 된 [Azure AD B2C Playground](https://aadb2cplayground.azurewebsites.net) 응용 프로그램입니다. Hello를 사용 하 여 B2C 테 넌 트에 응용 프로그램을 등록 해야 toouse hello 필드를 선택 하면 **리디렉션 URI** `https://aadb2cplayground.azurewebsites.net/`합니다.
* 사용 하 여 hello **지금 실행** hello에서 정책에는 단추 [Azure 포털](https://portal.azure.com/)합니다.

## <a name="customize-your-policy"></a>정책 사용자 지정
toofirst 해야 toocustomize hello 디자인 정책 hello Azure AD B2C의 특정 규칙을 사용 하 여 HTML 및 CSS 파일을 만듭니다. 그런 다음 Azure AD B2C에서 액세스할 수 있도록 정적 콘텐츠 tooa 공개적으로 사용할 수 있는 위치를 업로드할 수 있습니다. 사용자 전용 웹 서버, Azure Blob 저장소, Azure 콘텐츠 배달 네트워크 또는 그 밖의 고정 리소스 호스팅 공급자일 수 있습니다. hello 단 된 콘텐츠는 HTTPS를 통해 사용할 수 및 CORS를 사용 하 여 액세스할 수 있습니다. Hello 웹에서 정적 콘텐츠를 노출 한 후에 정책 toopoint toothis 위치와 tooyour 고객 콘텐츠는 편집할 수 있습니다. hello [주 UI 사용자 지정 문서](active-directory-b2c-reference-ui-customization.md) hello Azure AD B2C 사용자 지정 기능이 작동 하는 방법을 자세히 설명 합니다.

Hello 목적으로이 자습서에서는 이미 생성 된 몇 가지 샘플 콘텐츠 하 고 Azure Blob 저장소에서 호스트 합니다. hello 샘플 콘텐츠는 가상의 본사 "Wingtip Toys"의 hello 테마의 매우 기본적인 사용자 지정 합니다. tootry 다음이 단계를 수행 하는 사용자 지정 정책에서 로그 아웃 합니다.

1. Hello에 tooyour 테 넌 트에 로그인 [Azure 포털](https://portal.azure.com/) toohello B2C 기능 블레이드를 탐색 합니다.
2. **등록 또는 로그인 정책**을 클릭한 다음 사용자의 정책(예: "b2c\_1\_sign\_up\_sign\_in")을 클릭합니다.
3. **페이지 UI 사용자 지정**을 클릭한 다음 **통합 등록 또는 로그인 페이지**를 클릭합니다.
4. 설정/해제 hello **사용 하 여 사용자 지정 페이지** 너무 전환**예**합니다. Hello에 **사용자 지정 페이지 URI** 필드에, 입력 `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`합니다. **확인**을 클릭합니다.
5. **로컬 계정 등록 페이지**를 클릭합니다. 설정/해제 hello **사용 하 여 사용자 지정 템플릿을** 너무 전환**예**합니다. Hello에 **사용자 지정 페이지 URI** 필드에, 입력 `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`합니다.
6. Hello에 대 한 단계 동일한 반복 hello **소셜 계정 등록 페이지**합니다.
   클릭 **확인** 두 번 tooclose hello UI 사용자 지정 블레이드입니다.
7. **Save**를 클릭합니다.

이제 사용자가 지정한 정책을 사용해 볼 수 있습니다. 또한 클릭 hello 하지만, 않으려는 경우 사용자 고유의 응용 프로그램이 나 hello Azure AD B2C playground를 사용할 수 있습니다 **지금 실행** hello 정책 블레이드에서 명령입니다. Hello 드롭다운 목록 상자에서 응용 프로그램을 선택 하 고 hello 적절 한 리디렉션 URI를 선택 합니다. Hello 클릭 **지금 실행** 단추입니다. 새 브라우저 탭이 열리고 원위치에서 hello 새 콘텐츠로 응용 프로그램에 등록의 hello 사용자 환경을 통해 실행할 수 있습니다!

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Hello 샘플 콘텐츠 tooAzure Blob 저장소에 업로드
Azure Blob 저장소 toohost toouse 원하는 경우 페이지 콘텐츠를 사용자 고유의 저장소 계정을 만들고 우리의 B2C 도우미 도구 tooupload 파일을 사용할 수 있습니다.

### <a name="create-a-storage-account"></a>저장소 계정 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. **+ 새로 만들기** > **데이터 + 저장소** > **저장소 계정**을 클릭합니다. Azure 구독 toocreate Azure Blob 저장소 계정이 필요 합니다. Hello에 무료 평가판에 등록할 수 [Azure 웹 사이트](https://azure.microsoft.com/pricing/free-trial/)합니다.
3. 제공 된 **이름** hello 저장소 계정 (예: "contoso") 및 선택 hello에 대 한 적절 한 선택에 대 한 **가격 책정 계층**, **리소스 그룹** 및  **구독**합니다. Hello 갖도록 **Pin tooStartboard** 옵션을 선택 합니다. **만들기**를 클릭합니다.
4. 시작 보드 toohello와 방금 만든 hello 저장소 계정을 클릭 하십시오.
5. Hello에 **요약** 섹션에서 클릭 **컨테이너**, 클릭 하 고 **+ 추가**합니다.
6. 제공 된 **이름** hello 컨테이너 (예: "b2c") 및 선택에 대 한 **Blob** hello로 **액세스 형식**합니다. **확인**을 클릭합니다.
7. 만든 hello 컨테이너에서 hello hello 목록에 표시 됩니다 **Blob** 블레이드입니다. Hello URL hello 컨테이너;의 기록 예를 들어 비슷해야 너무`https://contoso.blob.core.windows.net/b2c`합니다. 닫기 hello **Blob** 블레이드입니다.
8. Hello 저장소 계정 블레이드에서 클릭 **키** hello의 hello 값 기록 **저장소 계정 이름** 및 **기본 액세스 키** 필드입니다.

> [!NOTE]
> **기본 선택키** 는 중요한 보안 자격 증명입니다.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Hello 도우미 도구 및 샘플 파일을 다운로드
Hello를 다운로드할 수 있습니다 [Azure Blob 저장소 도우미 도구 및 샘플 파일을.zip 파일로](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) 또는 GitHub에서 복제:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

이 리포지토리는 예제 HTML, CSS 및 이미지를 포함하는 `sample_templates\wingtip` 디렉터리를 포함합니다. 이러한 템플릿 tooreference 자신의 Azure Blob 저장소 계정이 필요 합니다 tooedit hello HTML 파일입니다. 열기 `unified.html` 및 `selfasserted.html` 바꿉니다 및 `https://localhost` hello 이전 단계에서 적어 둔 컨테이너의 hello URL로 합니다. Hello hello hello 도메인에서 Azure AD를 통해 HTML hello는 제공 하는 경우에 때문에 HTML 파일의 절대 경로 사용 해야 `https://login.microsoftonline.com`합니다.

### <a name="upload-hello-sample-files"></a>Hello 샘플 파일 업로드
같은 리포지토리 hello 하의 압축을 푸는 `B2CAzureStorageClient.zip` 및 실행된 hello `B2CAzureStorageClient.exe` 내에 파일이 있습니다. 이 프로그램 tooyour 저장소 계정을 지정 하 고 해당 파일에 대 한 CORS 액세스를 사용 하는 hello 디렉터리에서 모든 hello 파일을 업로드 하기만 합니다. 위의 hello 단계를 따른 경우 hello HTML 및 CSS 파일은 이제 향하고 tooyour 저장소 계정입니다. 해당 hello 참고 저장소 계정 이름은 hello 부분 앞에 오는 `blob.core.windows.net`; 예를 들어, `contoso`합니다. Tooaccess 시도 하 여 hello 콘텐츠가 올바르게 업로드 되었는지 확인할 수 있습니다 `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` 브라우저에서 합니다. 또한 사용 하 여 [http://test-cors.org/](http://test-cors.org/) toomake 인지 hello 콘텐츠 이제 CORS를 사용 하도록 설정 합니다. (찾아보십시오 "XHR 상태: 200" hello 결과에.)

### <a name="customize-your-policy-again"></a>정책 사용자 지정 다시 하기
등록 정책 tooreference를 편집 해야 hello 샘플 콘텐츠 tooyour 고유한 저장소 계정, 업로드 한 했으므로 것입니다. Hello부터 hello 단계를 반복 ["사용자 지정 정책에"](#customize-your-policy) 사용자 고유의 저장소 계정의 Url을 사용 하 여이 시간, 위의 섹션. 예를 들어,의 위치를 hello 프로그램 `unified.html` 파일 `<url-of-your-container>/wingtip/unified.html`합니다.

Hello를 사용 하 여 수 **지금 실행** 단추를 클릭 하거나 사용자 고유의 응용 프로그램 tooexecute 다시 정책. hello 결과 해야 봐 거의 정확 하 게 hello에서 사용한 동일한-hello 동일한 두 경우 모두에서 HTML 및 CSS를 샘플링 합니다. 그러나 이제 정책을 Azure Blob 저장소의 인스턴스를 직접 참조 하 고 있습니다 무료 tooedit는 하십시오으로 다시 hello 파일을 업로드 합니다. 사용자 지정에 대 한 자세한 내용은 HTML 및 CSS hello에 대 한 참조 toohello [주 UI 사용자 지정 문서](active-directory-b2c-reference-ui-customization.md)합니다.

