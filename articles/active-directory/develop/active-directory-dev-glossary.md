---
title: "Active Directory 개발자 용어집 aaaAzure | Microsoft Docs"
description: "일반적으로 사용되는 Azure Active Directory 개발자 개념 및 기능에 대한 용어 목록입니다."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Azure Active Directory 개발자 용어집
이 문서는 Azure AD에 대 한 응용 프로그램 개발에 대 한 학습 하는 경우에 유용 하 hello 핵심 Azure AD (Active Directory) 개발자 개념, 중 일부에 대 한 정의 포함 합니다.

## <a name="access-token"></a>액세스 토큰
형식 [보안 토큰](#security-token) 에서 발급 한는 [권한 부여 서버](#authorization-server)에서 사용 하 고는 [클라이언트 응용 프로그램](#client-application) 순서 tooaccess에는 [리소스 서버를 보호 합니다. ](#resource-server). Hello 형태에서 일반적으로 [JSON 웹 토큰 (JWT)][JWT], toohello 클라이언트 hello 부여 hello 권한 부여를 구현 하는 hello 토큰 [리소스 소유자](#resource-owner), 요청 된 수준에 대 한 액세스 합니다. hello 토큰에 포함 되어 해당 되는 모든 [클레임](#claim) hello 클라이언트 응용 프로그램 toouse 사용에 대 한 hello 제목, 지정된 된 리소스에 액세스할 때 자격 증명 형식을 합니다. 따라서 hello 리소스 소유자 tooexpose 자격 증명 toohello 클라이언트에 대 한 hello 필요성도 제거 됩니다.

액세스 토큰은 경우에 따라 참조 tooas "사용자 + App" 또는 "응용 프로그램 전용", hello에 따라 표시 되 고 자격 증명입니다. 예를 들어 클라이언트 응용 프로그램이 다음을 사용할 경우.

* [권한 부여 허용 "권한 부여 코드"](#authorization-grant), hello 최종 사용자가 처음 hello 리소스 소유자로 인증, 권한 부여 toohello 위임 클라이언트 tooaccess hello 리소스입니다. hello 클라이언트 hello 액세스 토큰을 가져올 때 나중에 인증 합니다. hello 토큰 나타내므로 두 hello 사용자 권한이 부여 된 hello 클라이언트 응용 프로그램과 hello 응용 프로그램에는 "사용자 + App" 토큰으로 특별히 참조 toomore 경우가 있습니다.
* ["클라이언트 자격 증명" 권한 부여 허용](#authorization-grant), hello 유일한 인증을 제공 하는 클라이언트 hello, 참조 tooas "응용 프로그램 전용" 토큰 수 hello 토큰 간혹 하므로 hello 리소스-소유자의 인증/권한 부여 없이 작동 합니다.

자세한 내용은 [Azure AD 토큰 참조][AAD-Tokens-Claims]를 참조하세요.

## <a name="application-manifest"></a>응용 프로그램 매니페스트
Hello에서 제공 하는 기능의 [Azure 포털][AZURE-portal], 연결 된 업데이트 하기 위한 메커니즘으로 사용 되는 hello 응용 프로그램 id 구성의 JSON 표현을 생성 [ 응용 프로그램] [ AAD-Graph-App-Entity] 및 [ServicePrincipal] [ AAD-Graph-Sp-Entity] 엔터티. 참조 [이해 hello Azure Active Directory 응용 프로그램 매니페스트] [ AAD-App-Manifest] 내용을 확인 합니다.

## <a name="application-object"></a>응용 프로그램 개체
때 하면 레지스터/업데이트 hello에서 응용 프로그램 [Azure 포털][AZURE-portal], hello 포털 만들기/업데이트 응용 프로그램 개체 및 해당 [서비스 사용자 개체](#service-principal-object)해당 테 넌 트에 대 한 합니다. hello application 개체 *정의* 전역 (모든 테 넌 트 간에 액세스 가진) 응용 프로그램의 id 구성 hello, 해당 해당 서비스 보안 주체 객체에는 있는 템플릿을 제공  *파생 된* 로컬로 실행 시 (특정 테 넌 트)에 사용 합니다.

자세한 내용은 [응용 프로그램 및 서비스 주체 개체][AAD-App-SP-Objects]를 참조하세요.

## <a name="application-registration"></a>응용 프로그램 등록
순서로 tooallow와 응용 프로그램 toointegrate 및 대리자 Id 및 액세스 관리 기능 tooAzure AD, Azure AD에 등록 해야 [테 넌 트](#tenant)합니다. Azure AD와 응용 프로그램을 등록할 때 제공 하는 id 구성을 응용 프로그램에 대 한 Azure AD와 toointegrate 허용 하 고와 같은 기능을 사용 하 여:

* Azure AD ID 관리 및 [OpenID Connect][OpenIDConnect] 프로토콜 구현을 사용한 Single Sign-On의 강력한 관리
* 액세스를 너무 중개[보호 된 리소스](#resource-server) 여 [클라이언트 응용 프로그램](#client-application), Azure AD의 OAuth 2.0을 통해 [권한 부여 서버](#authorization-server) 구현
* [승인 프레임 워크](#consent) 리소스 소유자 권한 부여에 따라 클라이언트 액세스 tooprotected 리소스를 관리 합니다.

자세한 내용은 [Azure Active Directory와 응용 프로그램 통합][AAD-Integrating-Apps]을 참조하세요.

## <a name="authentication"></a>인증
hello 작업 id 및 액세스 제어에 사용 되는 보안 주체 toobe 만들기 위한 hello 기반을 제공 하는 적합 한 자격 증명에 대 한 파티 검사입니다. 동안는 [OAuth2 권한 부여 허용](#authorization-grant) 인증 hello 파티의 hello 역할 채우는 예를 들어 [리소스 소유자](#resource-owner) 또는 [클라이언트 응용 프로그램](#client-application)에 따라 hello 사용 권한을 부여 합니다.

## <a name="authorization"></a>권한 부여
인증 된 보안 사용자 권한 toodo 문제가 부여 hello 작업. Hello Azure AD 프로그래밍 모델에서 두 가지 주요 사례가 있습니다.

* 중는 [OAuth2 권한 부여 허용](#authorization-grant) 흐름: hello 때 [리소스 소유자](#resource-owner) 권한 부여 toohello 부여 [클라이언트 응용 프로그램](#client-application), tooaccess hello hello 클라이언트를 허용 합니다. 리소스 소유자의 리소스입니다.
* Hello 클라이언트에서 리소스 액세스 하는 동안: hello에 의해 구현 된 [리소스 서버](#resource-server), hello를 사용 하 여 [클레임](#claim) hello에 값이 있는 [액세스 토큰](#access-token) toomake 액세스 제어 그에 따라 기초 하 여 결정 합니다.

## <a name="authorization-code"></a>인증 코드
짧은 동안 활성 상태로 유지 "token" tooa 제공 [클라이언트 응용 프로그램](#client-application) hello 여 [권한 부여 끝점](#authorization-endpoint), 4 개의 OAuth2 hello 중 하나는 hello "인증 코드" 흐름의 일환으로, [권한 부여 ](#authorization-grant). hello 코드가 toohello 클라이언트 응용 프로그램의 응답 tooauthentication에서 반환 되는 [리소스 소유자](#resource-owner), 요청 된 리소스를 나타내는 hello 리소스 소유자가 권한 부여 tooaccess hello를 위임 합니다. Hello 흐름의 일환으로, hello 코드에 대 한 교환 나중 됩니다는 [액세스 토큰](#access-token)합니다.

## <a name="authorization-endpoint"></a>권한 부여 끝점
Hello 구현한 hello 끝점 중 하나 [권한 부여 서버](#authorization-server), toointeract hello로 사용 되는 [리소스 소유자](#resource-owner) 순서 tooprovide에는 [인증 부여](#authorization-grant) 중 OAuth2 권한 부여 흐름을 부여 합니다. 부여 흐름을 사용 하는 실제 hello hello 권한 부여에 따라 포함 하 여 제공 하는 권한 부여는 달라질 수는 [인증 코드](#authorization-code) 또는 [보안 토큰](#security-token)합니다.

Hello OAuth2 사양을 참조 [권한 부여 권한 유형을] [ OAuth2-AuthZ-Grant-Types] 및 [권한 부여 끝점] [ OAuth2-AuthZ-Endpoint] 섹션 및 hello [OpenIDConnect 사양] [ OpenIDConnect-AuthZ-Endpoint] 내용을 확인 합니다.

## <a name="authorization-grant"></a>권한 부여
Hello 나타내는 자격 증명 [리소스 소유자의](#resource-owner) [권한 부여](#authorization) tooaccess tooa 부여 하는 보호 된 리소스 [클라이언트 응용 프로그램](#client-application)합니다. 클라이언트 응용 프로그램 hello 중 하나를 사용 [hello OAuth2 권한 부여 프레임 워크에서 정의 된 형식이 부여 4] [ OAuth2-AuthZ-Grant-Types] tooobtain 클라이언트 유형/요구 사항에 따라 권한 부여: "인증 코드 부여", " 클라이언트 자격 증명 부여","implicit grant"및"리소스 소유자 암호 자격 증명 부여"입니다. hello 자격 증명 toohello 클라이언트는 반환 되는 [액세스 토큰](#access-token), 또는 [인증 코드](#authorization-code) (나중에 대해 교환 된 액세스 토큰), 사용 권한 부여 허용 hello 유형에 따라 합니다.

## <a name="authorization-server"></a>권한 부여 서버
Hello에 정의 된 대로 [OAuth2 권한 부여 프레임 워크][OAuth2-Role-Def], toohello 토큰을 발급 하는 액세스 하는 일을 담당 하는 hello 서버 [클라이언트](#client-application) 성공적으로 인증 한 후 hello [리소스 소유자](#resource-owner) 권한 부여를 취득 하 합니다. A [클라이언트 응용 프로그램](#client-application) 를 통해 런타임 시 hello 권한 부여 서버와 상호 작용 하는 [권한 부여](#authorization-endpoint) 및 [토큰](#token-endpoint) hello OAuth2 정의 따라 끝점 [권한 부여 부여](#authorization-grant)합니다.

Azure AD, Azure AD 응용 프로그램 통합의 hello 경우에 Azure AD 응용 프로그램 및 Microsoft 서비스 Api에 대 한 권한 부여 서버 역할 hello 예를 들어 구현 [Microsoft Graph Api][Microsoft-Graph]합니다.

## <a name="claim"></a>클레임
A [보안 토큰](#security-token) 어설션을 엔터티 하나에 대 한 정보를 제공 하는 클레임을 포함 (예: 한 [클라이언트 응용 프로그램](#client-application) 또는 [리소스 소유자](#resource-owner)) tooanother 엔터티 (예: hello [리소스 서버](#resource-server)). 클레임은 토큰 제목의 hello에 대 한 팩트를 릴레이 하는 이름/값 쌍 (예를 들어 hello 보안 주체는 hello로 인증 되었음을 [권한 부여 서버](#authorization-server)). 지정 된 토큰에 있는 hello 클레임은 여러 변수를 토큰의 hello 형식, 사용 된 자격 증명 tooauthenticate hello 제목, hello 응용 프로그램 구성 등의 hello 형식 포함에 따라 달라 집니다.

자세한 내용은 [Azure AD 토큰 참조][AAD-Tokens-Claims]를 참조하세요.

## <a name="client-application"></a>클라이언트 응용 프로그램
Hello에 정의 된 대로 [OAuth2 권한 부여 프레임 워크][OAuth2-Role-Def], 하는 응용 프로그램 보호 hello 대신 리소스 요청 [리소스 소유자](#resource-owner)합니다. (예를 들어, 여부는 서버, 데스크톱, 또는 다른 장치에서 실행 되는 hello 응용 프로그램) hello "클라이언트" 라는 용어는 특정 하드웨어 구현 특성을 의미 하지 않습니다.  

클라이언트 응용 프로그램이 요청 [권한 부여](#authorization) 에서 리소스 소유자 tooparticipate에서는 [OAuth2 권한 부여 허용](#authorization-grant) 흐름, 및 hello 리소스 소유자를 대신 하 여 Api/데이터에 액세스할 수 있습니다. hello OAuth2 권한 부여 프레임 워크 [클라이언트의 두 가지 형식을 정의][OAuth2-Client-Types], "confidential" 및 "public", 해당 자격 증명의 hello 클라이언트의 기능 toomaintain hello 기밀성에 따라 합니다. 응용 프로그램은 웹 서버에서 실행되는 [웹 클라이언트(기밀)](#web-client), 장치에 설치된 [네이티브 클라이언트(공용)](#native-client) 또는 장치의 브라우저에서 실행되는 [사용자 에이전트 기반 클라이언트(공용)](#user-agent-based-client)를 구현할 수 있습니다.

## <a name="consent"></a>동의
프로세스의 hello는 [리소스 소유자](#resource-owner) 권한 부여 tooa 부여 [클라이언트 응용 프로그램](#client-application), tooaccess 보호 되는 특정 관련에서 리소스 [권한을](#permissions), hello를 대신 하 여 리소스 소유자입니다. Hello 클라이언트에서 요청한 hello 사용 권한에 따라 관리자 또는 사용자가 묻습니다 동의 tooallow tootheir 조직/개별 데이터 액세스에 대 한 각각. 참고에 [다중 테 넌 트](#multi-tenant-application) 시나리오, hello 응용 프로그램의 [서비스 사용자](#service-principal-object) hello 승인 사용자의 테 넌 트 hello에에서도 기록 됩니다.

## <a name="id-token"></a>ID 토큰
[OpenID Connect] [ OpenIDConnect-ID-Token] [보안 토큰](#security-token) 에서 제공 되는 [권한 부여 서버의](#authorization-server) [권한부여끝점](#authorization-endpoint), 포함 된 [클레임](#claim) 최종 사용자의 toohello 인증 관련 된 [리소스 소유자](#resource-owner)합니다. 액세스 토큰과 마찬가지로 ID 토큰도 또한 디지털로 서명된 [JWT(JSON Web Token)][JWT]로 표시됩니다. 액세스 토큰 달리 하지만 ID 토큰의 클레임에 사용 되지 않는 목적으로 관련된 tooresource 액세스 및 구체적으로 액세스 제어 합니다.

자세한 내용은 [Azure AD 토큰 참조][AAD-Tokens-Claims]를 참조하세요.

## <a name="multi-tenant-application"></a>다중 테넌트 응용 프로그램
로그인 수 있는 응용 프로그램의 클래스 및 [동의](#consent) 모든 Azure AD에서 사용자를 프로 비전 하는 사용자가 [테 넌 트](#tenant), hello 클라이언트가 등록 되었는지 하나 hello 이외의 테 넌 트를 포함 합니다. [네이티브 클라이언트](#native-client) 응용 프로그램은 기본적으로 다중 테 넌 트 반면 [웹 클라이언트](#web-client) 및 [리소스/API 웹](#resource-server) 응용 프로그램에는 단일 컴퓨터 또는 다중 테 넌 트 간의 hello 기능 tooselect 합니다. 반면, 웹 응용 프로그램 단일 테 넌 트로 등록만 수 hello 동일 하나 hello로 테 넌 트에 사용자를 프로 비전 하는 사용자 계정에서 로그인 hello 응용 프로그램 등록 되어 있습니다.

참조 [방법을 사용 하 여 모든 Azure AD 사용자의 toosign hello 다중 테 넌 트 응용 프로그램 패턴] [ AAD-Multi-Tenant-Overview] 내용을 확인 합니다.

## <a name="native-client"></a>네이티브 클라이언트
장치에 고유하게 설치된 [클라이언트 응용 프로그램](#client-application) 의 유형. 장치에서 모든 코드를 실행 하므로 tooits 불가능 toostore 자격 증명 개인적 으로/기밀 상태로 인해 "public" 클라이언트를 간주 됩니다. 더 자세한 내용은 [OAuth2 클라이언트 형식 및 프로필][OAuth2-Client-Types]을 참조하세요.

## <a name="permissions"></a>권한
A [클라이언트 응용 프로그램](#client-application) 향상 액세스 tooa [리소스 서버](#resource-server) 권한 요청을 선언 하 여 합니다. 두 가지 유형이 있습니다.

* 사용 권한을 지정 하는 "위임" [범위 기반](#scopes) 로그인 hello에서 권한을 위임 된 액세스를 사용 하 여 [리소스 소유자](#resource-owner), toohello 리소스와 실행 시간에 나타난 ["scp "클레임](#claim) hello 클라이언트에서 [액세스 토큰](#access-token)합니다.
* 지정 하는 "application" 권한이 [역할 기반](#roles) hello 클라이언트 응용 프로그램의 자격 증명/id를 사용 하 여 액세스, toohello 리소스와 실행 시간에 나타난 ["역할" 클레임](#claim) hello에 클라이언트의 액세스 토큰입니다.

또한 hello 하는 동안 화면 [동의](#consent) 프로세스, 자신의 테 넌 트의 관리자에 게 하거나 리소스 소유자 hello 기회 toogrant/거부 hello 클라이언트 액세스 tooresources을 제공 합니다.

권한 요청 "응용 프로그램" hello에 구성 된 "설정" 탭 hello에 / [Azure 포털][AZURE-portal], 아래에서 "에 필요한 권한", hello를 선택 하 여 원하는 "위임 된 권한" 및 " 응용 프로그램 사용 권한"(hello 후자는 hello 전역 관리자 역할의 멤버 자격이 필요). 때문에 [공용 클라이언트](#client-application) 자격 증명을 안전 하 게 유지할 수 없습니다 위임 된 사용 권한을 요청만 할 수 하는 동안는 [기밀 클라이언트](#client-application) hello 기능 toorequest 위임 및 응용 프로그램에 사용 권한입니다. 클라이언트 hello [application 개체](#application-object) 저장소 hello 선언에서 사용 권한을 해당 [requiredResourceAccess 속성][AAD-Graph-App-Entity]합니다.

## <a name="resource-owner"></a>리소스 소유자
Hello에 정의 된 대로 [OAuth2 권한 부여 프레임 워크][OAuth2-Role-Def], 보호 된 리소스 액세스 tooa 권한을 부여할 수 있는 엔터티. Hello 리소스 소유자 사용자 인 경우 참조 된 tooas 최종 사용자 있습니다. 예를 들어는 [클라이언트 응용 프로그램](#client-application) tooaccess hello 통해 사용자의 사서함이 [Microsoft Graph API][Microsoft-Graph]의 hello 리소스 소유자의 사용 권한이 필요 hello 사서함입니다.

## <a name="resource-server"></a>리소스 서버
Hello에 정의 된 대로 [OAuth2 권한 부여 프레임 워크][OAuth2-Role-Def], 호스트 리소스를 수락 하 고 tooprotected 리소스 응답 수는 보호 된 서버에서 요청 [클라이언트 응용 프로그램](#client-application) 없는 [액세스 토큰](#access-token)합니다. 보호된 리소스 서버 또는 리소스 응용 프로그램이라고도 합니다.

Api를 표시 하 고 통해 tooits 보호 된 리소스에 액세스를 적용 하는 리소스 서버 [범위](#scopes) 및 [역할](#roles), OAuth 2.0 Authorization Framework hello를 사용 하 여 합니다. 예로 hello Azure AD Graph API 액세스 tooAzure AD 테 넌 트 데이터 및 hello 메일 및 일정 같은 toodata 액세스를 제공 하는 Office 365 Api를 제공 합니다. 두 가지 hello를 통해 액세스할 수 또한 [Microsoft Graph API][Microsoft-Graph]합니다.  

리소스 응용 프로그램 id 구성을 통해 설정 됩니다는 클라이언트 응용 프로그램에서와 마찬가지로 [등록](#application-registration) Azure AD 테 넌 트에 hello 응용 프로그램 및 서비스 사용자 개체를 모두 제공 합니다. Hello Azure AD Graph API 같은 Microsoft에서 제공한 Api를 등록 했습니다. 미리 프로 비전 시 모든 테 넌 트에 사용할 수 있는 서비스 사용자

## <a name="roles"></a>roles
마찬가지로 [범위](#scopes), 역할을 하는 방법을 제공는 [리소스 서버](#resource-server) toogovern 액세스 tooits 보호 되는 리소스입니다. 두 종류가 있습니다: "user" 역할 "application" 역할을 구현 하는 동안 액세스 toohello 리소스를 필요로 하는 사용자/그룹에 대해 동일 hello에 대 한 역할 기반 액세스 제어를 구현 [클라이언트 응용 프로그램](#client-application) 액세스 해야 하는 합니다.

역할은 문자열 리소스 정의 (예를 들어 "Expense 승인자", "읽기 전용", "Directory.ReadWrite.All"), 관리 하는 hello [Azure 포털] [ AZURE-portal] hello 리소스를 통해 [응용 프로그램 매니페스트](#application-manifest), hello 리소스에 저장 하 고 [appRoles 속성][AAD-Graph-Sp-Entity]합니다. hello Azure 포털은 또한 사용자가 사용 되는 tooassign 너무 "user" 역할 및 클라이언트 구성 [응용 프로그램 사용 권한](#permissions) tooaccess "application" 역할.

Azure AD Graph API에서 노출 하는 hello 응용 프로그램 역할의 자세한 논의 알려면 [Graph API 권한 범위][AAD-Graph-Perm-Scopes]합니다. 단계별 구현 예제는 [Azure AD를 사용하여 클라우드 응용 프로그램에서 역할 기반 액세스 제어][Duyshant-Role-Blog]를 참조하세요.

## <a name="scopes"></a>범위
마찬가지로 [역할](#roles), 범위에 대 한 방법을 제공는 [리소스 서버](#resource-server) toogovern 액세스 tooits 보호 되는 리소스입니다. 범위는 사용 되는 tooimplement [범위 기반] [ OAuth2-Access-Token-Scopes] 에 대 한 액세스 제어는 [클라이언트 응용 프로그램](#client-application) 하에 부여 된 위임 된 액세스 toohello 리소스 소유자가 있습니다.

범위는 리소스 정의 문자열 (예를 들어 "Mail.Read", "Directory.ReadWrite.All") hello에서 관리 되는 [Azure 포털] [ AZURE-portal] hello 리소스를 통해 [응용 프로그램 매니페스트](#application-manifest), hello 리소스에 저장 하 고 [oauth2Permissions 속성][AAD-Graph-Sp-Entity]합니다. hello Azure 포털은 또한 tooconfigure 사용 되는 클라이언트 응용 프로그램 [위임 된 권한이](#permissions) tooaccess 범위입니다.

모범 사례 명명 규칙은 toouse "resource.operation.constraint" 형식입니다. Azure AD Graph API에서 노출 하는 hello 범위를 대 한 자세한 내용은 참조 하십시오. [Graph API 권한 범위][AAD-Graph-Perm-Scopes]합니다. Office 365 서비스에 의해 노출되는 범위는 [Office 365 API 사용 권한 참조][O365-Perm-Ref]를 참조하세요.

## <a name="security-token"></a>보안 토큰
OAuth2 토큰 또는 SAML 2.0 어설션과 같은 클레임을 포함한 서명된 문서입니다. OAuth2 [권한 부여](#authorization-grant)의 경우 [액세스 토큰](#access-token)(OAuth2)과 [ID 토큰](http://openid.net/specs/openid-connect-core-1_0.html#IDToken)은 보안 토큰의 유형으로서 둘 다 [JWT(JSON Web Token)][JWT] 형식으로 구현됩니다.

## <a name="service-principal-object"></a>서비스 주체 개체
때 하면 레지스터/업데이트 hello에서 응용 프로그램 [Azure 포털][AZURE-portal], hello 포털 만들기/업데이트 모두는 [application 개체](#application-object) 및 해당 서비스 사용자 해당 테 넌 트에 대 한 개체입니다. hello application 개체 *정의* 전역 (모든 테 넌 트 간에 있는 hello 연결 된 응용 프로그램 액세스 권한이 부여 된), 응용 프로그램의 id 구성 hello는 있는 hello 서식 파일 및 해당 서비스 주 개체는 *파생* 로컬로 실행 시 (특정 테 넌 트)에 사용 합니다.

자세한 내용은 [응용 프로그램 및 서비스 주체 개체][AAD-App-SP-Objects]를 참조하세요.

## <a name="sign-in"></a>로그인
프로세스의 hello는 [클라이언트 응용 프로그램](#client-application) 관련 된 상태를 획득 하기 위해 hello 목적을 위해 최종 사용자 인증을 시작 하 고 캡처하는 [보안 토큰](#security-token) 및 hello 응용 프로그램 세션 toothat 범위 지정 상태입니다. 상태는 사용자 프로필 정보, 토큰 클레임에서 파생된 정보 등과 같은 아티팩트를 포함할 수 있습니다.

응용 프로그램 로그인 기능은 hello (SSO) 단일 로그온 일반적으로 사용 되는 tooimplement 것입니다. 것도 올 수 있습니다 "등록" 함수 hello 최종 사용자 toogain access tooan 응용 프로그램 (에 처음 로그인)에 대 한 진입점으로 합니다. hello 등록 함수 사용 되는 toogather 및 추가 상태 특정 toohello 사용자 유지 이며 필요할 수 있습니다 [사용자 동의](#consent)합니다.

## <a name="sign-out"></a>로그 아웃
hello와 관련 된 hello 사용자 상태를 분리 하는 최종 사용자의 인증 되지 않은 프로세스 hello [클라이언트 응용 프로그램](#client-application) 동안 세션 [로그인](#sign-in)

## <a name="tenant"></a>tenant
Azure AD 디렉터리의 인스턴스는 참조 된 tooas Azure AD 테 넌 트입니다. 다음을 비롯한 다양한 기능을 제공합니다.

* 통합 응용 프로그램에 대한 레지스트리 서비스
* 사용자 계정 및 등록된 응용 프로그램의 인증
* REST 끝점 필요한 toosupport OAuth2 및 hello를 포함 하 여 SAML 등의 다양 한 프로토콜 [권한 부여 끝점](#authorization-endpoint), [토큰 끝점](#token-endpoint) "common" 끝점에서 사용 하는 hello 및 [ 다중 테 넌 트 응용 프로그램](#multi-tenant-application)합니다.

테 넌 트도 Azure AD와 연결 됩니다. 또는 Office 365 구독 hello 구독에 대 한 Id 및 액세스 관리 기능을 제공 하는 hello 구독을 프로 비전 하는 중입니다. 참조 [tooget Azure Active Directory 테 넌 트] [ AAD-How-To-Tenant] 액세스 tooa 얻을 수 있는 다양 한 방법으로 hello에 대 한 내용은 테 넌 트입니다. 참조 [Azure 구독과 Azure Active Directory와 연결 된] [ AAD-How-Subscriptions-Assoc] 구독 및 Azure AD 테 넌 트 간의 hello 관계에 대 한 자세한 내용은 합니다.

## <a name="token-endpoint"></a>토큰 끝점
Hello 구현한 hello 끝점 중 하나 [권한 부여 서버](#authorization-server) toosupport OAuth2 [권한 부여 부여](#authorization-grant)합니다. Hello grant에 따라 사용 되는 tooacquire 수는 [액세스 토큰](#access-token) (및 관련된 "새로 고침" 토큰) tooa [클라이언트](#client-application), 또는 [ID 토큰](#ID-token) hello와 함께 사용할 경우 [ OpenID Connect] [ OpenIDConnect] 프로토콜입니다.

## <a name="user-agent-based-client"></a>사용자 에이전트 기반 클라이언트
웹 서버에서 코드를 다운로드하고 단일 페이지 응용 프로그램(SPA)와 같은 사용자 에이전트(예: 웹 브라우저) 내에서 실행하는 [클라이언트 응용 프로그램](#client-application) 의 유형입니다. 장치에서 모든 코드를 실행 하므로 tooits 불가능 toostore 자격 증명 개인적 으로/기밀 상태로 인해 "public" 클라이언트를 간주 됩니다. 더 자세한 내용은 [OAuth2 클라이언트 형식 및 프로필][OAuth2-Client-Types]을 참조하세요.

## <a name="user-principal"></a>사용자 주체
서비스 사용자 개체에 사용 되는 toorepresent 응용 프로그램 인스턴스는 이와 비슷한 toohello 방식으로 사용자 주 개체는 다른 유형의 보안 주체 사용자를 나타냅니다. Azure AD 그래프 hello [사용자 엔터티] [ AAD-Graph-User-Entity] 성 및 이름, 사용자 계정 이름, 디렉터리 역할 멤버 자격 등과 같은 사용자 관련 속성을 포함 하는 사용자 개체에 대 한 hello 스키마를 정의 합니다. Azure AD tooestablish 런타임 시 사용자에 대 한 hello 사용자 id 구성을 제공합니다. hello 사용자 보안 주체는 사용 되는 toorepresent에 대 한 Single Sign On, 인증된 된 사용자 기록 [동의](#consent) 위임, 액세스 제어 결정에 등을 수행 합니다.

## <a name="web-client"></a>웹 클라이언트
유형의 [클라이언트 응용 프로그램](#client-application) 에서 실행 하는 모든 코드 웹 서버 및 수 toofunction "confidential" 클라이언트로 hello 서버에서 해당 자격 증명을 안전 하 게 저장 하 여 합니다. 더 자세한 내용은 [OAuth2 클라이언트 형식 및 프로필][OAuth2-Client-Types]을 참조하세요.

## <a name="next-steps"></a>다음 단계
hello [Azure AD 개발자 가이드] [ AAD-Dev-Guide] 모든 Azure AD 개발에 대 한 hello 포털 toouse은 관련 항목을 개략적으로 [응용 프로그램 통합] [ AAD-How-To-Integrate] 및의 기본 사항 hello [Azure AD 인증 및 지원 되는 인증 시나리오][AAD-Auth-Scenarios]합니다.

다음 설명 섹션 tooprovide 피드백 hello를 사용 하 고 구체화 하 고 새 정의 대 한 요청을 비롯 한 기존 정보를 업데이트 하거나 콘텐츠를 셰이핑 하는 데 도움이!

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
