---
title: "Active Directory 응용 프로그램 매니페스트 Azure aaaUnderstanding hello | Microsoft Docs"
description: "Hello Azure Active Directory 응용 프로그램 매니페스트를 Azure AD 테 넌 트에 응용 프로그램 id 구성을 나타내며 toofacilitate 사용 되는 OAuth 인증, 승인 환경 등의 자세한 정보를 제공 합니다."
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Hello Azure Active Directory 응용 프로그램 매니페스트 이해
Hello 응용 프로그램에 대 한 영구 id 구성을 제공 하는 Azure AD 테 넌 트와 Azure AD (Active Directory) 통합 하는 응용 프로그램을 등록 되어야 합니다. 이 구성은 런타임 시 응용 프로그램 toooutsource 및 broker 인증/권한 부여 Azure AD 통해 사용할 수 있는 시나리오를 지원할 원격입니다. Hello Azure AD 응용 프로그램 모델에 대 한 자세한 내용은 참조 hello [추가, 업데이트 및 응용 프로그램을 제거] [ ADD-UPD-RMV-APP] 문서.

## <a name="updating-an-applications-identity-configuration"></a>응용 프로그램의 ID 구성 업데이트
응용 프로그램 id 구성에서 기능 및 난이도 hello 다음을 비롯 한도에 따라 각각 다른 hello 속성 업데이트에 사용할 수 있는 가지 실제로 여러 옵션이 있습니다.

* hello  **[Azure 포털의] [ AZURE-PORTAL] 웹 사용자 인터페이스** tooupdate hello 응용 프로그램의 가장 일반적인 속성이 있습니다. 이 가장 빠른 hello 및 응용 프로그램의 속성을 업데이트 하는 최소 오류가 발생 하기 쉬운 방식으로 참조 하지 않는 전체 액세스 tooall 속성을 다음 두 가지 방법을 hello와 같은 기능을 제공 합니다.
* Hello Azure 클래식 포털에에서 표시 되지 않은 tooupdate 속성 해야 하는 고급 시나리오에 대 한 hello를 수정할 수 있습니다 **응용 프로그램 매니페스트**합니다. 이 문서의 hello 핵심 이며 시작 hello 다음 섹션에서 자세히 설명 합니다.
* 것도 가능 너무**hello를 사용 하는 응용 프로그램 작성 [Graph API] [ GRAPH-API]**  tooupdate 프로그램 응용 프로그램에 가장 많은 노력이 hello 합니다. 그러나 관리 소프트웨어를 작성 하는 또는 정기적으로 자동화 된 방식으로 응용 프로그램 속성 tooupdate 필요한 경우 선택할 수 없었습니다 수 있습니다.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>응용 프로그램 id 구성 응용 프로그램 매니페스트 tooupdate hello를 사용 하 여
Hello를 통해 [Azure 포털][AZURE-PORTAL], hello 인라인 매니페스트 편집기를 사용 하 여 hello 응용 프로그램 매니페스트를 업데이트 하 여 응용 프로그램 id 구성을 관리할 수 있습니다. 다운로드 하 고 hello 응용 프로그램 매니페스트 JSON 파일을 업로드할 수도 있습니다. 실제 파일이 hello 디렉터리에 저장 됩니다. hello 응용 프로그램 매니페스트는 단순히 HTTP GET 작업에 hello Azure AD Graph API 응용 프로그램 엔터티 및 hello 업로드 하는 응용 프로그램 엔터티 hello에 대 한 HTTP PATCH 작업 합니다.

결과적으로, 순서 toounderstand hello 형식 및 hello 응용 프로그램 매니페스트 등록 정보 해야 tooreference hello Graph API [응용 프로그램 엔터티] [ APPLICATION-ENTITY] 설명서입니다. 응용 프로그램 매니페스트 업로드를 통해 수행할 수 있는 업데이트의 예는 다음을 포함합니다.

* **사용 권한 범위(oauth2Permissions)** 를 선언합니다. Hello "웹 Api 노출 tooOther 응용 프로그램" 항목을 참조 [Azure Active Directory와 응용 프로그램 통합] [ INTEGRATING-APPLICATIONS-AAD] hello를 사용 하는 사용자 가장 구현 정보에 대 한 oauth2Permissions 위임 된 권한 범위입니다. 응용 프로그램 엔터티 속성 hello Graph API에에서 설명 되어 이전에 설명한 것 처럼 [엔터티 및 복합 형식] [ APPLICATION-ENTITY] 참조 문서를 포함 하는 hello oauth2Permissions 속성이 형식의 컬렉션 [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION]합니다.
* **앱에서 노출된 응용 프로그램 역할(appRoles)을 선언**합니다. hello 응용 프로그램 엔터티 appRoles 속성은 컬렉션 형식의 [AppRole][APPLICATION-ENTITY-APP-ROLE]합니다. Hello 참조 [역할 기반 액세스 제어는 Azure AD를 사용 하 여 클라우드 응용 프로그램] [ RBAC-CLOUD-APPS-AZUREAD] 구현 예에 대 한 문서입니다.
* **알려진된 클라이언트 응용 프로그램 (knownClientApplications) 선언**, hello의 toologically 동률 hello 동의 수 있는 클라이언트 응용 프로그램 toohello 리소스/웹 API를 지정 합니다.
* **Azure AD tooissue 그룹 구성원 자격 클레임을 요청** hello (groupMembershipClaims) 사용자를 로그인에 대 한 합니다.  이 hello 사용자의 디렉터리 역할 멤버 자격에 대 한 구성된 tooissue 클레임 될 수도 있습니다. Hello 참조 [AD 그룹을 사용 하 여 클라우드 응용 프로그램에서 권한 부여] [ AAD-GROUPS-FOR-AUTHORIZATION] 구현 예에 대 한 문서입니다.
* **응용 프로그램 toosupport OAuth 2.0 Implicit grant 허용** 흐름 (oauth2AllowImplicitFlow). 이 형식의 허용 흐름은 포함된 JavaScript 웹 페이지 또는 단일 페이지 응용 프로그램(SPA)을 통해 사용됩니다. Hello 암시적 권한 부여에 대 한 자세한 내용은 참조 하십시오. [이해 hello OAuth2 암시적 부여 흐름이 Azure Active Directory에서][IMPLICIT-GRANT]합니다.
* **X509 사용할 수 있도록 hello 비밀 키로 인증서** (keyCredentials). Hello 참조 [Office 365에서 앱을 서비스와 데몬 빌드] [ O365-SERVICE-DAEMON-APPS] 및 [Azure 리소스 관리자 API를 개발자 가이드 tooauth] [ DEV-GUIDE-TO-AUTH-WITH-ARM] 구현 예제에 대 한 문서입니다.
* 응용 프로그램에 대한 **새 앱 ID URI 추가**(identifierURIs[]). 앱 ID Uri를 사용 하 toouniquely 해당 Azure AD 테 넌 트 내에서 (또는 여러 Azure AD 테 넌 트 간에, 확인 된 사용자 지정 도메인을 통해 정규화 경우 다중 테 넌 트 시나리오에 대 한) 응용 프로그램을 식별 합니다. 사용 권한 tooa 리소스 응용 프로그램을 요청할 때 사용 하는 리소스를 응용 프로그램에 대 한 액세스 토큰 획득 또는 합니다. 이 요소를 업데이트할 때 hello 같은 업데이트가 수행 hello 응용 프로그램의 홈 테 넌 트에 거주 하 고 있는 toohello 해당 서비스 사용자의 servicePrincipalNames 컬렉션입니다.

hello 응용 프로그램 매니페스트도 제공 좋은 방법 tootrack hello 응용 프로그램 등록의 상태입니다. JSON 형식으로 사용할 수 있기 때문에 응용 프로그램의 소스 코드와 함께 해당 소스 제어에 hello 파일 표시를 확인할 수 있습니다.

## <a name="step-by-step-example"></a>단계별 예제
이제 있습니다 안내 hello 단계 필요한 tooupdate hello 응용 프로그램 매니페스트를 통해 응용 프로그램 id 구성. 중점적으로 다루겠습니다 예제를 보려면 앞 hello 중 어떻게 toodeclare 새 사용 권한 범위를 리소스 응용 프로그램에서 보여 주는:

1. Toohello 로그인 [Azure 포털][AZURE-PORTAL]합니다.
2. 인증 한 후 hello의 오른쪽 위 모서리 hello 페이지에서에서 선택 하 여 Azure AD 테 넌 트를 선택 합니다.
3. 선택 **Azure Active Directory** hello에 왼쪽 탐색 패널 및 클릭에서 확장 **앱 등록**합니다.
4. Tooupdate hello 목록에서 원하는 항목을 클릭 하면 hello 응용 프로그램을 찾습니다.
5. Hello 응용 프로그램 페이지에서 클릭 **매니페스트** tooopen hello 인라인 매니페스트 편집기입니다. 
6. 이 편집기를 사용 하 여 hello 매니페스트를 직접 편집할 수 있습니다. 해당 hello 매니페스트에 hello에 대 한 hello 스키마를 따르는 참고 [응용 프로그램 엔터티] [ APPLICATION-ENTITY] 앞에서 설명한 대로: 예를 들면 "Employees.Read.All" 라는 새 사용 권한 tooimplement/노출 원하는 가정 합니다. 이 리소스 응용 프로그램 (API)에서 단순히 추가 새로운/두 번째 요소 toohello auth2permissions 컬렉션 ie.
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    따라서 새 전역적으로 고유 ID (GUID) hello에 대 한 생성 해야 하 고 hello 항목은 고유 해야 합니다. `"id"` 속성입니다. 이 경우 지정 했기 때문에 `"type": "User"`,이 사용 권한이 승인된 tooby는 hello 리소스/API 응용 프로그램이 등록 되는 Azure AD 테 넌 트 hello에서 모든 계정 인증할 수 있습니다. 이 부여 hello 클라이언트 응용 프로그램 사용 권한 tooaccess hello 계정 대신 것입니다. hello 설명 및 표시 이름 문자열 hello Azure 포털에에서 표시 하기 위해 동의 하는 동안 사용 됩니다.
6. Hello 매니페스트를 업데이트 작업을 완료 하는 경우 클릭 **저장** toosave hello 매니페스트 합니다.  
   
Hello 매니페스트를 저장 했으므로 응용 프로그램 액세스 toohello 새 권한을 위에 추가 등록 된 클라이언트를 제공할 수 있습니다. 사용할 수 있습니다이 시간 hello 클라이언트 응용 프로그램의 매니페스트를 편집 하는 대신 Azure 포털의 웹 UI hello:  

1. 먼저 toohello 이동 **설정** hello의 블레이드에서 원하는 tooadd 액세스 toohello 새로운 API, 클라이언트 응용 프로그램 toowhich 클릭 **필요한 권한** 선택 **API 선택** .
2. 그런 다음 있습니다 나타납니다 hello 테 넌 트의 등록 된 리소스 응용 프로그램 (Api) hello 목록입니다. 또는 hello 응용 프로그램 hello 검색 상자의 유형 hello 이름 hello 리소스 응용 프로그램 tooselect를 클릭 합니다. 클릭 하 여 hello 응용 프로그램을 찾은 경우 **선택**합니다.  
3. 그러면 toohello **Select 권한만** 페이지 hello 응용 프로그램 사용 권한 및 hello 리소스 응용 프로그램에 사용할 수 있는 위임 된 권한 목록이 표시 됩니다. 선택 hello 순서 tooadd에 새로운 사용 권한은 것 toohello 클라이언트의 사용 권한 목록을 요청 합니다. 이 새로운 사용 권한은 hello "requiredResourceAccess" 컬렉션 속성에 hello 클라이언트 응용 프로그램의 id 구성에 저장 됩니다.


이것으로 끝입니다. 이제 응용 프로그램은 새 ID 구성을 사용하여 실행됩니다.

## <a name="next-steps"></a>다음 단계
* 응용 프로그램의 응용 프로그램 및 서비스 사용자 개체 간의 hello 관계에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 및 Azure AD에서 서비스 보안 주체 개체][AAD-APP-OBJECTS]합니다.
* Hello 참조 [Azure AD 개발자 용어집] [ AAD-DEVELOPER-GLOSSARY] hello 핵심 Azure AD (Active Directory) 개발자 개념 중 일부에 대 한 정의입니다.

Tooprovide 피드백 아래 hello 설명 섹션을 사용 하 고 구체화 하 고 콘텐츠를 셰이핑 하는 데 도움이 됩니다.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

