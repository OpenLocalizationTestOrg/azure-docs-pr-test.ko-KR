---
title: "API 관리 템플릿 리소스 aaaAzure | Microsoft Docs"
description: "Hello 유형의 Azure API 관리에서 개발자 포털 서식 파일에 사용할 수 있는 리소스에 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Azure API Management 템플릿 리소스
Azure API 관리 hello 다음 유형의 hello 개발자 포털 서식 파일에서 사용 하기 위해 리소스를 제공 합니다.  
  
-   [문자열 리소스](#strings)  
  
-   [문자 모양 리소스](#glyphs)  
  
##  <a name="strings"></a> 문자열 리소스  
 API 관리 hello 개발자 포털에서 사용 하기 위해 다양 한 문자열 리소스를 제공합니다. 이러한 리소스는 모든 API 관리에서 지 원하는 hello 언어의로 지역화 됩니다. 서식 파일의 기본 집합 hello 페이지 머리글, 레이블 및 hello 개발자 포털에 표시 되는 모든 상수 문자열에 대 한 이러한 리소스를 사용 합니다. toouse 템플릿에 문자열 리소스 hello 다음 예제와 같이 hello 리소스 문자열 접두사 뒤에 hello 문자열 이름에 제공 합니다.  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 hello 다음 예제는 hello 제품 목록 서식 파일에서 한 표시 **제품** hello hello 페이지 위쪽에 있습니다.  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 Toohello 다음 개발자 포털 서식 파일에서 사용 하기 위해 사용할 수 있는 hello 문자열 리소스에 대 한 표를 참조 하십시오. 해당 테이블의 hello 문자열 리소스에 대 한 hello 접두사로 테이블 이름이 hello를 사용 합니다.  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [설명서](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [UserProfile](#UserProfile)  
  
###  <a name="ApisStrings"></a> ApisStrings  
  
|이름|텍스트|  
|----------|----------|  
|PageTitleApis|API|  
  
###  <a name="AppDetailsStrings"></a> AppDetailsStrings  
  
|이름|텍스트|  
|----------|----------|  
|WebApplicationsDetailsTitle|응용 프로그램 미리 보기|  
|WebApplicationsRequirementsHeader|요구 사항|  
|WebApplicationsScreenshotAlt|스크린샷|  
|WebApplicationsScreenshotsHeader|스크린샷|  
  
###  <a name="ApplicationListStrings"></a> ApplicationListStrings  
  
|이름|텍스트|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|응용 프로그램 tooremove 시겠습니까 입니까?|  
|WebDevelopersAppNotPublished|게시되지 않음|  
|WebDevelopersAppNotSubminted|제출되지 않음|  
|WebDevelopersAppTableCategoryHeader|Category|  
|WebDevelopersAppTableNameHeader|이름|  
|WebDevelopersAppTableStateHeader|시스템 상태|  
|WebDevelopersEditLink|편집|  
|WebDevelopersRegisterAppLink|응용 프로그램 등록|  
|WebDevelopersRemoveLink|제거|  
|WebDevelopersSubmitLink|Submit|  
|WebDevelopersYourApplicationsHeader|응용 프로그램|  
  
###  <a name="AppStrings"></a> AppStrings  
  
|이름|텍스트|  
|----------|----------|  
|WebApplicationsHeader|응용 프로그램|  
  
###  <a name="CommonResources"></a> CommonResources  
  
|이름|텍스트|  
|----------|----------|  
|NoItemsToDisplay|결과를 찾을 수 없습니다.|  
|GeneralExceptionMessage|오류가 발생했습니다. 일시적인 결함이나 버그일 수 있습니다. 다시 시도하세요.|  
|GeneralJsonExceptionMessage|오류가 발생했습니다. 일시적인 결함이나 버그일 수 있습니다. Hello 페이지를 다시 로드 하 고 다시 시도 하십시오.|  
|ConfirmationMessageUnsavedChanges|저장되지 않은 몇 가지 변경 내용이 있습니다. ? Toocancel을 hello 변경 취소|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|Http 요청 본문이 너무 큽니다.|  
  
###  <a name="CommonStrings"></a> CommonStrings  
  
|이름|텍스트|  
|----------|----------|  
|ButtonLabelCancel|취소|  
|ButtonLabelSave|저장|  
|GeneralExceptionMessage|오류가 발생했습니다. 일시적인 결함이나 버그일 수 있습니다. 다시 시도하세요.|  
|NoItemsToDisplay|없는 항목 toodisplay가 있습니다.|  
|PagerButtonLabelFirst|처음|  
|PagerButtonLabelLast|마지막|  
|PagerButtonLabelNext|다음|  
|PagerButtonLabelPrevious|이전|  
|PagerLabelPageNOfM|{0} / {1} 페이지|  
|PasswordTooShort|hello 암호가 너무 짧습니다.|  
|EmailAsPassword|전자 메일을 암호로 사용하지 마세요.|  
|PasswordSameAsUserName|암호에는 사용자 이름을 포함할 수 없습니다.|  
|PasswordTwoCharacterClasses|다른 문자 클래스를 사용하세요.|  
|PasswordTooManyRepetitions|반복이 너무 많습니다.|  
|PasswordSequenceFound|암호에 시퀀스가 포함되어 있습니다.|  
|PagerLabelPageSize|페이지 크기|  
|CurtainLabelLoading|로드 중...|  
|TablePlaceholderNothingToDisplay|Hello 선택한 기간 및 범위에 대 한 데이터가 없습니다|  
|ButtonLabelClose|닫습니다|  
  
###  <a name="Documentation"></a>문서화  
  
|이름|텍스트|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|잘못된 헤더 '{0}'|  
|WebDocumentationInvalidRequestErrorMessage|잘못된 요청 URL|  
|TextboxLabelAccessToken|액세스 토큰 *|  
|DropdownOptionPrimaryKeyFormat|기본-{0}|  
|DropdownOptionSecondaryKeyFormat|보조-{0}|  
|WebDocumentationSubscriptionKeyText|구독 키|  
|WebDocumentationTemplatesAddHeaders|필수 HTTP 헤더를 추가합니다.|  
|WebDocumentationTemplatesBasicAuthSample|기본 권한 부여 샘플|  
|WebDocumentationTemplatesCurlForBasicAuth|기본 권한 부여를 사용할 경우: --user {username}:{password}|  
|WebDocumentationTemplatesCurlValuesForPath|경로 매개 변수 값({...}로 표시), 구독 키 및 쿼리 매개 변수 값을 지정합니다.|  
|WebDocumentationTemplatesDeveloperKey|구독 키를 지정합니다.|  
|WebDocumentationTemplatesJavaApache|이 샘플에서는 HTTP 구성 요소 (http://hc.apache.org/httpcomponents-client-ga/)에서 hello Apache HTTP 클라이언트|  
|WebDocumentationTemplatesOptionalParams|필요에 따라 선택적 매개 변수 값을 지정합니다.|  
|WebDocumentationTemplatesPhpPackage|이 예제는 hello HTTP_Request2 패키지를 사용합니다. (자세한 내용: http://pear.php.net/package/HTTP_Request2)|  
|WebDocumentationTemplatesPythonValuesForPath|경로 매개 변수 값({...}로 표시)을 지정하고 필요한 경우 본문을 요청합니다.|  
|WebDocumentationTemplatesRequestBody|요청 본문을 지정합니다.|  
|WebDocumentationTemplatesRequiredParams|필수 매개 변수 뒤 hello에 대 한 값을 지정 합니다.|  
|WebDocumentationTemplatesValuesForPath|경로 매개 변수 값({...}로 표시)을 지정합니다.|  
|OAuth2AuthorizationEndpointDescription|hello 권한 부여 끝점 hello 리소스 소유자와 함께 사용 되는 toointeract 이며 인증 부여를 가져옵니다.|  
|OAuth2AuthorizationEndpointName|권한 부여 끝점|  
|OAuth2TokenEndpointDescription|hello 토큰 끝점 사용 되는 hello 클라이언트 tooobtain 권한 부여를 제공 하 여 액세스 토큰에서 권한을 부여 하거나 새로 고침 토큰입니다.|  
|OAuth2TokenEndpointName|토큰 끝점|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> hello 클라이언트 hello 리소스 소유자의 사용자 에이전트 toohello 권한 부여 끝점에 연결 하 여 hello 흐름을 시작 합니다.  hello 클라이언트는 해당 클라이언트 식별자, 요청 된 범위, 로컬 상태 및 리디렉션 URI toowhich hello 권한 부여 서버는 액세스 부여 (또는 거부) 되 면 hello 사용자 에이전트에 보냅니다.     </p\> < p\> hello 권한 부여 서버 hello 리소스 소유자 (hello 사용자 에이전트)를 통해 인증 하 고 hello 리소스 소유자 부여 되거나 hello 클라이언트의 액세스 요청을 거부 여부를 설정 합니다.     </p\> < p\> hello 권한 부여 서버 hello 리디렉션 제공 된 URI를 사용 하 여 hello 사용자 에이전트 백 toohello 클라이언트를 리디렉션합니다 hello 리소스 소유자에 대 한 액세스 권한을 부여 하는 것으로 가정 합니다 (hello 요청 또는 클라이언트 중 이전 t 등록)입니다.  hello 리디렉션 URI는 인증 코드 및 이전 버전의 hello 클라이언트에서 제공 되는 모든 로컬 상태를 포함 합니다.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\> hello 클라이언트 toohello 리디렉션에 추가 하는 매개 변수 뒤 hello를 사용 하 여 알려 드립니다 hello 요청이 유효 하지 않을 경우의 hello 액세스 요청을 거부 하는 hello 사용자, 경우: </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|권한 부여 요청|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello 클라이언트 응용 프로그램 순서 tooinitiate hello OAuth 프로세스에에서 hello 사용자 toohello 권한 부여 끝점을 보내야 합니다.          Hello 권한 부여 끝점에서 hello 사용자를 인증 하 고 허용 하거나 toohello 앱 액세스를 거부 합니다.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\> hello 리소스 소유자에 대 한 액세스 권한을 부여 라고 가정할 경우 권한 부여 서버 리디렉션합니다 hello 리디렉션 제공 된 URI를 사용 하 여 hello 사용자 에이전트 백 toohello 클라이언트 이전 (hello 요청에 또는 클라이언트 등록 하는 동안).  hello 리디렉션 URI는 인증 코드 및 이전 버전의 hello 클라이언트에서 제공 되는 모든 로컬 상태를 포함 합니다. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> hello 권한 부여 서버의 액세스 토큰을 요청 하는 클라이언트 hello ' hello 이전 단계에서 받은 hello 인증 코드를 포함 하 여 s 토큰 끝점입니다.  Hello 요청을 만들 때는 hello 클라이언트 hello 권한 부여 서버를 인증 합니다.  hello 클라이언트 hello 리디렉션 사용 되는 URI tooobtain hello 인증 코드를 확인을 위해 포함 됩니다. </p\> < p\> hello 권한 부여 서버 hello 클라이언트 인증 hello 인증 코드의 유효성을 검사 하 고 해당 hello 리디렉션 URI 단계 (C)에서 일치 항목 hello URI 사용 되는 tooredirect hello 클라이언트 받은 보장 합니다.  유효한 경우 hello 권한 부여 서버의 액세스 토큰 및 필요에 따라 새로 고침 토큰을 사용 하 여 다시 응답 합니다. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> hello 요청 클라이언트 인증이 실패 하거나 유효 하지, hello 권한 부여 서버 (지정 하지 않는 이상)는 HTTP 400 (잘못 된 요청) 상태 코드를 사용 하 여 응답 하 고 hello hello 응답 매개 변수 뒤에 포함 됩니다. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> hello 클라이언트 hello hello HTTP 요청 엔터티 본문에 u t F-8의 문자 인코딩을 사용 하 여 hello "응용 프로그램/x-www-형식-urlencoded" 형식을 사용 하 여 매개 변수 뒤에 전송 하 여 요청 toohello 토큰 끝점을 만듭니다. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> 구문 hello 매개 변수 toohello-응답의 엔터티 본문 hello HTTP 200 (정상) 상태 코드와 함께 다음을 추가 하 여 응답 hello 및 hello 권한 부여 서버는 액세스 토큰 및 선택적 새로 고침 토큰을 발급 합니다. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> hello 클라이언트 hello 권한 부여 서버를 사용 하 여 인증 하 고 hello 토큰 끝점에서 액세스 토큰을 요청 합니다. </p\> < p\> hello 권한 부여 서버 hello 클라이언트를 인증 하 고 유효한 경우 액세스 토큰을 발급 합니다. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> hello 요청이 클라이언트 인증 되지 않았거나 올바르지 않습니다 경우 hello 권한 부여 서버 (지정 하지 않는 이상)는 HTTP 400 (잘못 된 요청) 상태 코드를 사용 하 여 응답 하 고 hello hello 응답 매개 변수 뒤에 포함 됩니다. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> hello 클라이언트 hello hello HTTP 요청 엔터티 본문에 u t F-8의 문자 인코딩을 사용 하 여 hello "응용 프로그램/x-www-형식-urlencoded" 형식을 사용 하 여 매개 변수 뒤에 추가 하 여 요청 toohello 토큰 끝점을 만듭니다. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> hello 액세스 토큰 요청은 유효 하 고 권한 있는 hello 권한 부여 서버는 액세스 토큰 및 선택적 새로 고침 토큰을 발급 및 구문은 다음 매개 변수 toohello 엔터티 본문의 hello HTTP hello를 추가 하 여 응답 hello 200 (OK) 상태 코드로 응답입니다. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> hello 리소스 소유자를 연결 하 여 hello 흐름을 시작 하는 클라이언트 hello ' s 사용자 에이전트 toohello 권한 부여 끝점입니다.  hello 클라이언트는 해당 클라이언트 식별자, 요청 된 범위, 로컬 상태 및 리디렉션 URI toowhich hello 권한 부여 서버는 액세스 부여 (또는 거부) 되 면 hello 사용자 에이전트에 보냅니다. </p\> < p\> hello 권한 부여 서버 (hello 사용자 에이전트)를 통해 hello 리소스 소유자를 인증 하 고 있는지 여부를 hello 리소스 소유자를 허용 하거나 거부 hello 클라이언트 설정 ' s 액세스를 요청 합니다. </p\> < p\> hello 리소스 소유자에 대 한 액세스 권한을 부여 라고 가정할 경우 hello 권한 부여 서버 hello 사용자 에이전트 백 toohello 클라이언트 hello 리디렉션 URI 윗부분를 사용 하 여를 리디렉션합니다.  hello 리디렉션 URI는 hello URI 조각에 hello 액세스 토큰을 포함합니다. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\> 경우 hello 액세스 요청을 거부 하는 hello 리소스 소유자 또는 권한 부여 서버 hello hello 클라이언트에 다음 매개 변수 toohello fragme hello를 추가 하 여 알립니다 hello 요청이 없거나 잘못 되었습니다. 리디렉션 URI 외에 다른 이유로 실패 하는 경우 사용 하 여 hello 리디렉션 URI의 nt 구성 요소 hello "응용 프로그램/x-www-형식-urlencoded" 형식입니다. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello 클라이언트 응용 프로그램 순서 tooinitiate hello OAuth 프로세스에에서 hello 사용자 toohello 권한 부여 끝점을 보내야 합니다.      Hello 권한 부여 끝점에서 hello 사용자를 인증 하 고 허용 하거나 toohello 앱 액세스를 거부 합니다. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> hello 리소스 소유자 부여 hello 액세스 요청을 hello 권한 부여 서버의 액세스 토큰을 발급 한 hello 다음과 같은 hello 리디렉션 URI의 매개 변수 toohello 조각 구성 요소를 추가 하 여 toohello 클라이언트 배달 hello를 사용 하 여 "a pplication/x-www-형식-urlencoded "형식입니다. </p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|클라이언트 자격 증명 (예: 웹 서버 응용 프로그램, PHP, Java, Python, Ruby, ASP.NET, 등을 사용 하 여 구현 합니다.)의 hello 기밀성을 유지 관리할 수에 대 한 권한 부여 코드 흐름 최적화 되어 있습니다.|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|인증 코드 부여|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|클라이언트 자격 증명 흐름은 hello 클라이언트 (응용 프로그램)에서 제어 toohello 보호 된 리소스에 액세스를 요청 하는 경우에 적합 합니다. 클라이언트 hello 하므로 최종 사용자 개입이 필요 리소스 소유자로 간주 됩니다.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|클라이언트 자격 증명 부여|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|암시적 흐름 불가능 자신의 자격 증명 알려진된 toooperate 특정 리디렉션 URI의 hello 기밀성을 유지 관리 하기 위한 클라이언트에 대 한 최적화 됩니다. 이러한 클라이언트는 일반적으로 JavaScript와 같은 스크립팅 언어를 사용하는 브라우저에서 구현됩니다.|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|암시적 부여|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|리소스 소유자 암호 자격 증명 흐름은에 있는 경우 hello 리소스 소유자 트러스트 관계 hello 클라이언트 (응용 프로그램)와 hello 장치 운영 체제 또는 높은 권한이 가진된 응용 프로그램과 같은 적합 합니다. 이 흐름은 hello 리소스 소유자의 자격 증명 (사용자 이름 및 암호를 일반적으로 대화형 양식 사용 하 여)을 가져올 수 있는 클라이언트에 적합 합니다.|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|리소스 소유자 암호 자격 증명 부여|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> hello 리소스 소유자의 사용자 이름 및 암호로 hello 클라이언트를 제공 합니다. </p\> < p\> hello 권한 부여 서버의 액세스 토큰을 요청 하는 클라이언트 hello ' hello 리소스 소유자 로부터 받은 hello 자격 증명을 포함 하 여 s 토큰 끝점입니다.  Hello 요청을 만들 때는 hello 클라이언트 hello 권한 부여 서버를 인증 합니다. </p\> < p\> hello 권한 부여 서버가 인증 hello 클라이언트 및 hello 리소스 소유자 자격 증명의 유효성을 검사 하 고 유효한 경우 액세스 토큰을 발급 합니다. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> hello 요청이 클라이언트 인증 되지 않았거나 올바르지 않습니다 경우 hello 권한 부여 서버 (지정 하지 않는 이상)는 HTTP 400 (잘못 된 요청) 상태 코드를 사용 하 여 응답 하 고 hello hello 응답 매개 변수 뒤에 포함 됩니다. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> hello 클라이언트 hello hello HTTP 요청 엔터티 본문에 u t F-8의 문자 인코딩을 사용 하 여 hello "응용 프로그램/x-www-형식-urlencoded" 형식을 사용 하 여 매개 변수 뒤에 추가 하 여 요청 toohello 토큰 끝점을 만듭니다. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> hello 액세스 토큰 요청은 유효 하 고 권한 있는 hello 권한 부여 서버는 액세스 토큰 및 선택적 새로 고침 토큰을 발급 및 구문은 다음 매개 변수 toohello 엔터티 본문의 hello HTTP respo hello를 추가 하 여 응답 hello 200 (OK) 상태 코드와 함께 nse 합니다. </p\>|  
|OAuth2Step_AccessTokenRequest_Name|액세스 토큰 요청|  
|OAuth2Step_AuthorizationRequest_Name|권한 부여 요청|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|필수. hello 권한 부여 서버에서 발급 한 hello 액세스 토큰입니다.|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|필수. hello 권한 부여 서버에서 발급 한 hello 액세스 토큰입니다.|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|필수. hello 권한 부여 서버에서 발급 한 hello 액세스 토큰입니다.|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|필수. hello 권한 부여 서버에서 발급 한 hello 액세스 토큰입니다.|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|필수. 클라이언트 식별자입니다.|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|Hello 권한 부여 서버와 하지 hello 클라이언트를 인증 하는 경우 필요 합니다.|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|필수. hello 클라이언트 식별자입니다.|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|필수. hello 인증 코드 권한 부여 서버 hello에 의해 생성 됩니다.|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|필수. hello 권한 부여 서버에서 받은 hello 권한 부여 코드입니다.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|옵션. 사람이 읽을 수 있는 추가 정보를 제공하는 ASCII 텍스트입니다.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|옵션. 사람이 읽을 수 있는 추가 정보를 제공하는 ASCII 텍스트입니다.|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|옵션. 사람이 읽을 수 있는 추가 정보를 제공하는 ASCII 텍스트입니다.|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|옵션. 사람이 읽을 수 있는 추가 정보를 제공하는 ASCII 텍스트입니다.|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|옵션. 사람이 읽을 수 있는 추가 정보를 제공하는 ASCII 텍스트입니다.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|옵션. Hello 오류에 대 한 정보로 사용자를 읽을 수 있는 웹 페이지를 식별 하는 URI입니다.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|옵션. Hello 오류에 대 한 정보로 사용자를 읽을 수 있는 웹 페이지를 식별 하는 URI입니다.|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|옵션. Hello 오류에 대 한 정보로 사용자를 읽을 수 있는 웹 페이지를 식별 하는 URI입니다.|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|옵션. Hello 오류에 대 한 정보로 사용자를 읽을 수 있는 웹 페이지를 식별 하는 URI입니다.|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|옵션. Hello 오류에 대 한 정보로 사용자를 읽을 수 있는 웹 페이지를 식별 하는 URI입니다.|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|필수. Hello 다음에서 단일 ASCII 오류 코드: invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable 합니다.|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|필수. Hello 다음에서 단일 ASCII 오류 코드: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope 합니다.|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|필수. Hello 다음에서 단일 ASCII 오류 코드: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope 합니다.|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|필수. Hello 다음에서 단일 ASCII 오류 코드: invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable 합니다.|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|필수. Hello 다음에서 단일 ASCII 오류 코드: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope 합니다.|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|권장. hello 수명 hello 액세스 토큰의 시간 (초)입니다.|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|권장. hello 수명 hello 액세스 토큰의 시간 (초)입니다.|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|권장. hello 수명 hello 액세스 토큰의 시간 (초)입니다.|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|권장. hello 수명 hello 액세스 토큰의 시간 (초)입니다.|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|필수. 값이 너무 설정 해야 합니다 "authorization_code"입니다.|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|필수. 값이 너무 설정 해야 합니다 "client_credentials"입니다.|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|필수. 값이 너무 설정 해야 합니다 "password"입니다.|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|필수. hello 리소스 소유자 암호입니다.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|옵션. hello 리디렉션 끝점 URI는 절대 URI 이어야 합니다.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|필요한 경우 hello 권한 부여 요청에 포함 된 hello "redirect_uri" 매개 변수 및 해당 값이 동일 해야 합니다.|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|옵션. hello 리디렉션 끝점 URI는 절대 URI 이어야 합니다.|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|옵션. hello 새로 고침 토큰 사용된 tooobtain 새 액세스 토큰 일 수 있습니다.|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|옵션. hello 새로 고침 토큰 사용된 tooobtain 새 액세스 토큰 일 수 있습니다.|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|옵션. hello 새로 고침 토큰 사용된 tooobtain 새 액세스 토큰 일 수 있습니다.|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|필수. 값을 설정 해야 너무 "코드"입니다.|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|필수. 값 "token" 너무 설정 되어야 합니다.|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|옵션. hello 액세스 요청의 hello 범위입니다.|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|클라이언트 hello; 동일한 toohello 범위를 요청할 경우 선택 사항 그렇지 않은 경우 필요합니다.|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|옵션. hello 액세스 요청의 hello 범위입니다.|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|클라이언트 hello;에서 요청한 동일한 경우에 선택적 toohello 범위 그렇지 않은 경우 필요합니다.|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|옵션. hello 액세스 요청의 hello 범위입니다.|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|클라이언트 hello; 동일한 toohello 범위를 요청할 경우 선택 사항 그렇지 않은 경우 필요합니다.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|옵션. hello 액세스 요청의 hello 범위입니다.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|클라이언트 hello;에서 요청한 동일한 경우에 선택적 toohello 범위 그렇지 않은 경우 필요합니다.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|Hello "state" 매개 변수 hello 클라이언트 권한 부여 요청에 있었던 경우 필요 합니다.  hello 클라이언트에서 받은 정확한 값을 hello입니다.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|권장. Hello 요청과 콜백 간에 hello 클라이언트 toomaintain 상태에서 사용 하는 불투명 값입니다.  hello 권한 부여 서버는 hello 사용자 에이전트 백 toohello 클라이언트를 리디렉션할 때이 값을 포함 합니다.  hello 매개 변수를 사용 하 여 교차 사이트 요청 위조를 방지 하는 데 해야 합니다.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|Hello "state" 매개 변수 hello 클라이언트 권한 부여 요청에 있었던 경우 필요 합니다.  hello 클라이언트에서 받은 정확한 값을 hello입니다.|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|Hello "state" 매개 변수 hello 클라이언트 권한 부여 요청에 있었던 경우 필요 합니다.  hello 클라이언트에서 받은 정확한 값을 hello입니다.|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|권장. Hello 요청과 콜백 간에 hello 클라이언트 toomaintain 상태에서 사용 하는 불투명 값입니다.  hello 권한 부여 서버는 hello 사용자 에이전트 백 toohello 클라이언트를 리디렉션할 때이 값을 포함 합니다.  hello 매개 변수를 사용 하 여 교차 사이트 요청 위조를 방지 하는 데 해야 합니다.|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|Hello "state" 매개 변수 hello 클라이언트 권한 부여 요청에 있었던 경우 필요 합니다.  hello 클라이언트에서 받은 정확한 값을 hello입니다.|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|필수. hello 유형의 hello 토큰을 발급 합니다.|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|필수. hello 유형의 hello 토큰을 발급 합니다.|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|필수. hello 유형의 hello 토큰을 발급 합니다.|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|필수. hello 유형의 hello 토큰을 발급 합니다.|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|필수. hello 리소스 소유자 사용자 이름입니다.|  
|OAuth2UnsupportedTokenType|"{0}" 토큰 형식은 지원되지 않습니다.|  
|OAuth2InvalidState|잘못된 권한 부여 서버 응답|  
|OAuth2GrantType_AuthorizationCode|인증 코드|  
|OAuth2GrantType_Implicit|암시적|  
|OAuth2GrantType_ClientCredentials|클라이언트 자격 증명|  
|OAuth2GrantType_ResourceOwnerPassword|리소스 소유자 암호|  
|WebDocumentation302Code|302 있음|  
|WebDocumentation400Code|400(잘못된 요청)|  
|OAuth2SendingMethod_AuthHeader|권한 부여 헤더|  
|OAuth2SendingMethod_QueryParam|쿼리 매개 변수|  
|OAuth2AuthorizationServerGeneralException|{0}을(를) 통해 액세스 권한을 부여하는 동안 오류가 발생했습니다.|  
|OAuth2AuthorizationServerCommunicationException|HTTP 연결 tooauthorization 서버를 설정할 수 없습니다 또는 예기치 않게 종료 되었습니다.|  
|WebDocumentationOAuth2GeneralErrorMessage|예기치 않은 오류가 발생했습니다.|  
|AuthorizationServerCommunicationException|권한 부여 서버 통신 예외가 발생했습니다. 관리자에게 문의하세요.|  
|TextblockSubscriptionKeyHeaderDescription|액세스 toothis API를 제공 하는 구독 키입니다. <a href='/developer'\>Profile</a\>에 있습니다.|  
|TextblockOAuthHeaderDescription|<i\>{0}</i\>에서 가져온 OAuth 2.0 액세스 토큰입니다. 지원되는 권한 부여 유형: <i\>{1}</i\>.|  
|TextblockContentTypeHeaderDescription|Toohello API를 전송 하는 hello 본문의 미디어 유형입니다.|  
|ErrorMessageApiNotAccessible|이 이번 hello toocall 고치려는 API를 액세스할 수 없습니다. Hello API 게시자에 게 문의 하십시오 <는 href = "/ 문제"\>여기 </a\>합니다.|  
|ErrorMessageApiTimedout|hello toocall 고치려는 API 다시 정상적인 tooget 응답 시간 보다 오래 걸립니다. Hello API 게시자에 게 문의 하십시오 <는 href = "/ 문제"\>여기 </a\>합니다.|  
|BadRequestParameterExpected|"'{0}'매개 변수가 필요합니다."|  
|TooltipTextDoubleClickToSelectAll|모든 tooselect를 두 번 클릭 합니다.|  
|TooltipTextHideRevealSecret|표시/숨기기|  
|ButtonLinkOpenConsole|시도|  
|SectionHeadingRequestBody|요청 본문|  
|SectionHeadingRequestParameters|요청 매개 변수|  
|SectionHeadingRequestUrl|요청 URL|  
|SectionHeadingResponse|응답|  
|SectionHeadingRequestHeaders|헤더 요청|  
|FormLabelSubtextOptional|선택 사항|  
|SectionHeadingCodeSamples|코드 샘플|  
|TextblockOpenidConnectHeaderDescription|<i\>{0}</i\>에서 가져온 OpenID 연결 ID 토큰입니다. 지원되는 권한 부여 유형: <i\>{1}</i\>.|  
  
###  <a name="ErrorPageStrings"></a> ErrorPageStrings  
  
|이름|텍스트|  
|----------|----------|  
|LinkLabelBack|뒤로|  
|LinkLabelHomePage|홈페이지|  
|LinkLabelSendUsEmail|전자 메일 보내기|  
|PageTitleError|했습니다 문제가 처리 hello 요청된 페이지|  
|TextblockPotentialCauseIntermittentIssue|이미 사라진 일시적인 데이터 액세스 문제일 수 있습니다.|  
|TextblockPotentialCauseOldLink|hello 링크를 클릭 하면 오래 된 것일 수 하 고 지점 toohello 하지 위치를 더 이상 수정 하십시오.|  
|TextblockPotentialCauseTechnicalProblem|이 쪽에 기술적 문제가 있을 수 있습니다.|  
|TextblockPotentialSolutionRefresh|Hello 페이지를 새로 고쳐 보십시오.|  
|TextblockPotentialSolutionStartOver|{0}에서 다시 시작합니다.|  
|TextblockPotentialSolutionTryAgain|{0} 이동한 hello 작업을 다시 시도 하십시오.|  
|TextReportProblem|{0}에서 무엇이 잘못되었는지 설명하고 최대한 빨리 살펴보겠습니다.|  
|TitlePotentialCause|가능한 원인|  
|TitlePotentialSolution|방금 일시적인 문제, 몇 가지 tootry 내용이 있을 수|  
  
###  <a name="IssuesStrings"></a> IssuesStrings  
  
|이름|텍스트|  
|----------|----------|  
|WebIssuesIndexTitle|문제|  
|WebIssuesNoActiveSubscriptions|활성 구독이 없습니다. 제품 tooreport 문제 toosubscribe가 필요합니다.|  
|WebIssuesNotSignin|로그인하지 않습니다. 메모를 게시 하거나 {0} tooreport 문제 하십시오.|  
|WebIssuesReportIssueButton|보고서 문제|  
|WebIssuesSignIn|로그인|  
|WebIssuesStatusReportedBy|상태: {0} | {1}이(가) 보고함|  
  
###  <a name="NotFoundStrings"></a> NotFoundStrings  
  
|이름|텍스트|  
|----------|----------|  
|LinkLabelHomePage|홈페이지|  
|LinkLabelSendUsEmail|전자 메일 보내기|  
|PageTitleNotFound|죄송 합니다. 원하는 hello 페이지를 찾을 수 없습니다|  
|TextblockPotentialCauseMisspelledUrl|잘못 입력 했습니다 hello URL 입력 한 것입니다.|  
|TextblockPotentialCauseOldLink|hello 링크를 클릭 하면 오래 된 것일 수 하 고 지점 toohello 하지 위치를 더 이상 수정 하십시오.|  
|TextblockPotentialSolutionRetype|Hello URL을 다시 입력 해 보십시오.|  
|TextblockPotentialSolutionStartOver|{0}에서 다시 시작합니다.|  
|TextReportProblem|{0}에서 무엇이 잘못되었는지 설명하고 최대한 빨리 살펴보겠습니다.|  
|TitlePotentialCause|가능한 원인|  
|TitlePotentialSolution|잠재적 솔루션|  
  
###  <a name="ProductDetailsStrings"></a> ProductDetailsStrings  
  
|이름|텍스트|  
|----------|----------|  
|WebProductsAgreement|너무 가입 하 여 {0} 제품 toohello 동의 `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`합니다.|  
|WebProductsLegalTermsLink|사용 약관|  
|WebProductsSubscribeButton|구독|  
|WebProductsUsageLimitsHeader|사용 제한|  
|WebProductsYouAreNotSubscribed|구독 된 toothis 제품 됩니다.|  
|WebProductsYouRequestedSubscription|구독 toothis 제품을 요청 했습니다.|  
|ErrorYouNeedtoAgreeWithLegalTerms|계속 하려면 먼저 toohello 사용 약관을 동의 해야 합니다.|  
|ButtonLabelAddSubscription|구독 추가|  
|LinkLabelChangeSubscriptionName|변경|  
|ButtonLabelConfirm|Confirm|  
|TextblockMultipleSubscriptionsCount|{0} 구독 toothis 제품을 사용할 수 있습니다.|  
|TextblockSingleSubscriptionsCount|{0} 구독 toothis 제품을 사용할 수 있습니다.|  
|TextblockSingleApisCount|이 제품에는 {0}개 API가 포함되어 있습니다.|  
|TextblockMultipleApisCount|이 제품에는 {0}개 API가 포함되어 있습니다.|  
|TextblockHeaderSubscribe|Tooproduct 구독|  
|TextblockSubscriptionDescription|새 구독은 다음과 같이 만들어집니다.|  
|TextblockSubscriptionLimitReached|구독 제한에 도달했습니다.|  
  
###  <a name="ProductsStrings"></a> ProductsStrings  
  
|이름|텍스트|  
|----------|----------|  
|PageTitleProducts|제품|  
  
###  <a name="ProviderInfoStrings"></a> ProviderInfoStrings  
  
|이름|텍스트|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|로그인은 hello 순간에 hello 관리자가 비활성화 됩니다.|  
|TextboxExternalIdentitiesSigninInvitation|또는 다음 계정으로 로그인합니다.|  
|TextboxExternalIdentitiesSigninInvitationPrimary|로그인에 사용할 계정:|  
  
###  <a name="SigninResources"></a> SigninResources  
  
|이름|텍스트|  
|----------|----------|  
|PrincipalNotFound|주체가 없거나 서명이 유효하지 않습니다.|  
|ErrorSsoAuthenticationFailed|SSO 인증에 실패했습니다.|  
|ErrorSsoAuthenticationFailedDetailed|잘못된 토큰이 제공되었거나 서명을 확인할 수 없습니다.|  
|ErrorSsoTokenInvalid|SSO 토큰이 잘못되었습니다.|  
|ValidationErrorSpecificEmailAlreadyExists|'{0}' 전자 메일은 이미 등록되어 있습니다.|  
|ValidationErrorSpecificEmailInvalid|'{0}' 전자 메일이 잘못되었습니다.|  
|ValidationErrorPasswordInvalid|암호가 잘못되었습니다. Hello 오류를 수정 하 고 다시 시도 하세요.|  
|PropertyTooShort|{0}이(가) 너무 짧습니다.|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|잘못된 전자 메일 주소입니다.|  
|ValidationMessageNewPasswordConfirmationRequired|새 암호 확인|  
|ValidationErrorPasswordConfirmationRequired|암호 확인이 비어 있습니다.|  
|WebAuthenticationEmailChangeNotice|너무 hello에 변경 확인 전자 메일은 {0}. 지침 내 tooconfirm 따라 새 전자 메일 주소입니다. Hello 전자 메일 hello에서 tooyour 받은 편지 함으로 다음 몇 분 동안 도착 하지 않으면, 정크 메일 폴더를 확인 하십시오.|  
|WebAuthenticationEmailChangeNoticeHeader|전자 메일 변경 요청이 성공적으로 처리되었습니다.|  
|WebAuthenticationEmailChangeNoticeTitle|전자 메일 변경 요청됨|  
|WebAuthenticationEmailHasBeenRevertedNotice|전자 메일이 이미 있습니다. 요청이 되돌려졌습니다.|  
|ValidationErrorEmailAlreadyExists|이미 있는 전자 메일|  
|ValidationErrorEmailInvalid|잘못된 전자 메일 주소|  
|TextboxLabelEmail|Email|  
|ValidationErrorEmailRequired|전자 메일은 필수입니다.|  
|WebAuthenticationErrorNoticeHeader|오류|  
|WebAuthenticationFieldLengthErrorMessage|{0}은(는) {1}의 최대 길이여야 합니다.|  
|TextboxLabelEmailFirstName|이름|  
|ValidationErrorFirstNameRequired|이름은 필수입니다.|  
|ValidationErrorFirstNameInvalid|잘못된 이름|  
|NoticeInvalidInvitationToken|확인 링크는 48시간 동안만 유효합니다. 아직 이 기간 내에 있으면 링크가 올바른지 확인하세요. 링크가 만료 된 경우 다음 하십시오 작업을 반복 hello tooconfirm 만들려고 합니다.|  
|NoticeHeaderInvalidInvitationToken|잘못된 초대 토큰|  
|NoticeTitleInvalidInvitationToken|확인 오류|  
|WebAuthenticationLastNameInvalidErrorMessage|잘못된 성|  
|TextboxLabelEmailLastName|성|  
|ValidationErrorLastNameRequired|성은 필수입니다.|  
|WebAuthenticationLinkExpiredNotice|Tooyou 발송 된 확인 링크가 만료 되었습니다. `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|암호 재설정 링크가 잘못되었거나 만료되었습니다.|  
|WebAuthenticationLinkExpiredNoticeTitle|링크 보냄|  
|WebAuthenticationNewPasswordLabel|새 암호|  
|ValidationMessageNewPasswordRequired|새 암호가 필요합니다.|  
|TextboxLabelNotificationsSenderEmail|알림 보낸 사람 전자 메일|  
|TextboxLabelOrganizationName|조직 이름|  
|WebAuthenticationOrganizationRequiredErrorMessage|조직 이름이 비어 있습니다.|  
|WebAuthenticationPasswordChangedNotice|암호가 성공적으로 업데이트되었습니다.|  
|WebAuthenticationPasswordChangedNoticeTitle|암호 업데이트됨|  
|WebAuthenticationPasswordCompareErrorMessage|암호가 일치하지 않습니다.|  
|WebAuthenticationPasswordConfirmLabel|암호 확인|  
|ValidationErrorPasswordInvalidDetailed|암호가 너무 약합니다.|  
|WebAuthenticationPasswordLabel|암호|  
|ValidationErrorPasswordRequired|암호는 필수입니다.|  
|WebAuthenticationPasswordResetSendNotice|너무 hello에 변경 암호 확인 전자 메일은 {0}. 암호 변경 프로세스 hello 지침 hello 전자 메일 toocontinue 내에서 키를 따르십시오.|  
|WebAuthenticationPasswordResetSendNoticeHeader|암호 재설정 요청이 성공적으로 처리되었습니다.|  
|WebAuthenticationPasswordResetSendNoticeTitle|암호 재설정 요청됨|  
|WebAuthenticationRequestNotFoundNotice|요청을 찾을 수 없음|  
|WebAuthenticationSenderEmailRequiredErrorMessage|알림 보낸 사람 전자 메일이 비어 있습니다.|  
|WebAuthenticationSigninPasswordLabel|암호를 입력 하 여 hello 변경을 확인 하십시오.|  
|WebAuthenticationSignupConfirmNotice|등록 확인 전자 메일입니다. 너무 {0}. < b r /\> hello 내에 있는 다음 명령 하세요 tooactivate 전자 메일 계정 < b r /\> hello 전자 메일 도착 하지 않으면 hello 내에서 받은 편지함에 다음 몇 분 정도 확인 하십시오 정크 메일 폴더입니다.|  
|WebAuthenticationSignupConfirmNoticeHeader|계정이 성공적으로 만들어졌습니다.|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|등록 확인 전자 메일을 다시 보냈습니다.|  
|WebAuthenticationSignupConfirmNoticeTitle|만든 계정|  
|WebAuthenticationTokenRequiredErrorMessage|토큰이 비어 있습니다.|  
|WebAuthenticationUserAlreadyRegisteredNotice|이 전자 메일을 가진 사용자 hello 시스템에 이미 등록 된 것 같습니다. 암호를 잊었으면 시도 하십시오. toorestore 또는 연락처 지원 팀입니다.|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|이미 등록된 사용자|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|이미 등록됨|  
|ButtonLabelChangePassword|암호 변경|  
|ButtonLabelChangeAccountInfo|계정 정보 변경|  
|ButtonLabelCloseAccount|계정 사용 중지|  
|WebAuthenticationInvalidCaptchaErrorMessage|입력 한 텍스트 hello 그림에는 텍스트와 일치 하지 않습니다. 나중에 다시 시도하세요.|  
|ValidationErrorCredentialsInvalid|전자 메일 또는 암호가 잘못되었습니다. Hello 오류를 수정 하 고 다시 시도 하세요.|  
|WebAuthenticationRequestIsNotValid|요청이 잘못되었습니다.|  
|WebAuthenticationUserIsNotConfirm|toosign 시도 하기 전에 등록을 확인 하세요.|  
|WebAuthenticationInvalidEmailFormated|잘못된 전자 메일: {0}|  
|WebAuthenticationUserNotFound|사용자를 찾을 수 없음|  
|WebAuthenticationTenantNotRegistered|계정은 tooa Azure Active Directory 테 넌 트 권한 있는 tooaccess 되지 않는이 포털을 속해 있습니다.|  
|WebAuthenticationAuthenticationFailed|인증에 실패했습니다.|  
|WebAuthenticationGooglePlusNotEnabled|인증에 실패했습니다. Hello 응용 프로그램에 권한이 부여 다음 hello admin toomake에 문의 하세요 Google 인증이 구성 되어 있어야 올바르게 합니다.|  
|ValidationErrorAllowedTenantIsRequired|허용된 테넌트는 필수입니다.|  
|ValidationErrorTenantIsNotValid|hello Azure Active Directory 테 넌 트 ' {'이 (0) 올바르지 않습니다.|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|{0} 계정을 사용하여 로그인합니다.|  
|WebAuthenticationUserLimitNotice|이 서비스는 hello 최대 허용 된 사용자 수에 도달 했습니다. 하십시오 `<a href="mailto:{0}"\>contact hello administrator</a\>` tooupgrade 사용자 등록 서비스와 다시 사용 하도록 설정 합니다.|  
|WebAuthenticationUserLimitNoticeHeader|사용자 등록 사용 해제됨|  
|WebAuthenticationUserLimitNoticeTitle|사용자 등록 사용 해제됨|  
|WebAuthenticationUserRegistrationDisabledNotice|사용자의 등록 hello 관리자에 의해 비활성화 되었습니다. 외부 ID 공급자를 통해 로그인합니다.|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|사용자 등록 사용 해제됨|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|사용자 등록 사용 해제됨|  
|WebAuthenticationSignupPendingConfirmationNotice|에서는 사용자의 계정 hello 생성을 완료 하기 전에 tooverify 전자 메일 주소가 필요 합니다. 전자 메일 너무 보내 드렸습니다 {0}. 계정 hello 전자 메일 tooactivate 내 hello 명령을 키를 따르십시오. 다음 몇 분 내 hello hello 전자 메일 하지 않는 도착 하는 경우 정크 메일 폴더를 확인 하십시오.|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|Hello 전자 메일 주소가 {0}에 대 한 확인 되지 않은 계정이 있습니다. 사용자의 계정 전자 메일 주소 tooverify 필요 toocomplete hello 생성 합니다. 전자 메일 너무 보내 드렸습니다 {0}. 계정 hello 전자 메일 tooactivate 내 hello 명령을 키를 따르십시오. 다음 몇 분 내 hello hello 전자 메일 하지 않는 도착 하는 경우 정크 메일 폴더를 확인 하십시오|  
|WebAuthenticationSignupConfirmationAlmostDone|거의 완료됨|  
|WebAuthenticationSignupConfirmationEmailSent|전자 메일 너무 보내 드렸습니다 {0}. 계정 hello 전자 메일 tooactivate 내 hello 명령을 키를 따르십시오. 다음 몇 분 내 hello hello 전자 메일 하지 않는 도착 하는 경우 정크 메일 폴더를 확인 하십시오.|  
|WebAuthenticationEmailSentNotificationMessage|전자 메일을 성공적으로 보낼 너무 {0}|  
|WebAuthenticationNoAadTenantConfigured|Hello 서비스용으로 구성 된 Azure Active Directory 테 넌 트입니다.|  
|CheckboxLabelUserRegistrationTermsConsentRequired|동의 함 toohello `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`합니다.|  
|TextblockUserRegistrationTermsProvided|`<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`을(를) 검토하세요.|  
|DialogHeadingTermsOfUse|사용 약관|  
|ValidationMessageConsentNotAccepted|계속 하려면 먼저 toohello 사용 약관을 동의 해야 합니다.|  
  
###  <a name="SigninStrings"></a> SigninStrings  
  
|이름|텍스트|  
|----------|----------|  
|WebAuthenticationForgotPassword|암호를 잊으셨습니까?|  
|WebAuthenticationIfAdministrator|관리자이면 `<a href="{0}"\>here</a\>`에 로그인해야 합니다.|  
|WebAuthenticationNotAMember|아직 회원이 아니십니까? `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|이 컴퓨터에 사용자 이름 및 암호 저장|  
|WebAuthenticationSigininWithPassword|사용자 이름과 암호로 로그인합니다.|  
|WebAuthenticationSigninTitle|로그인|  
|WebAuthenticationSignUpNow|지금 등록하십시오.|  
  
###  <a name="SignupStrings"></a> SignupStrings  
  
|이름|텍스트|  
|----------|----------|  
|PageTitleSignup|등록|  
|WebAuthenticationAlreadyAMember|이미 회원이십니까?|  
|WebAuthenticationCreateNewAccount|새 API Management 계정 만들기|  
|WebAuthenticationSigninNow|지금 로그인|  
|ButtonLabelSignup|등록|  
  
###  <a name="SubscriptionListStrings"></a> SubscriptionListStrings  
  
|이름|텍스트|  
|----------|----------|  
|SubscriptionCancelConfirmation|시겠습니까 toocancel이이 구독 입니까?|  
|SubscriptionRenewConfirmation|시겠습니까 toorenew이이 구독 입니까?|  
|WebDevelopersManageSubscriptions|구독 관리|  
|WebDevelopersPrimaryKey|기본 키|  
|WebDevelopersRegenerateLink|다시 생성|  
|WebDevelopersSecondaryKey|보조 키|  
|ButtonLabelShowKey|표시|  
|ButtonLabelRenewSubscription|갱신|  
|WebDevelopersSubscriptionReqested|{0}에 요청됨|  
|WebDevelopersSubscriptionRequestedState|요청됨|  
|WebDevelopersSubscriptionTableNameHeader|이름|  
|WebDevelopersSubscriptionTableStateHeader|시스템 상태|  
|WebDevelopersUsageStatisticsLink|분석 보고서|  
|WebDevelopersYourSubscriptions|구독|  
|SubscriptionPropertyLabelRequestedDate|요청 날짜|  
|SubscriptionPropertyLabelStartedDate|시작 날짜|  
|PageTitleRenameSubscription|구독 이름 바꾸기|  
|SubscriptionPropertyLabelName|구독 이름|  
  
###  <a name="SubscriptionStrings"></a> SubscriptionStrings  
  
|이름|텍스트|  
|----------|----------|  
|SectionHeadingCloseAccount|계정 tooclose를 찾고 있습니까?|  
|PageTitleDeveloperProfile|프로필|  
|ButtonLabelHideKey|숨기기|  
|ButtonLabelRegenerateKey|다시 생성|  
|InformationMessageKeyWasRegenerated|시겠습니까 tooregenerate이이 키는 입니까?|  
|ButtonLabelShowKey|표시|  
  
###  <a name="UpdateProfileStrings"></a> UpdateProfileStrings  
  
|이름|텍스트|  
|----------|----------|  
|ButtonLabelUpdateProfile|프로필 업데이트|  
|PageTitleUpdateProfile|계정 정보 업데이트|  
  
###  <a name="UserProfile"></a> UserProfile  
  
|이름|텍스트|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|계정 정보 변경|  
|ButtonLabelChangePassword|암호 변경|  
|ButtonLabelCloseAccount|계정 사용 중지|  
|TextboxLabelEmail|Email|  
|TextboxLabelEmailFirstName|이름|  
|TextboxLabelEmailLastName|성|  
|TextboxLabelNotificationsSenderEmail|알림 보낸 사람 전자 메일|  
|TextboxLabelOrganizationName|조직 이름|  
|SubscriptionStateActive|Active|  
|SubscriptionStateCancelled|Cancelled|  
|SubscriptionStateExpired|만료됨|  
|SubscriptionStateRejected|거부됨|  
|SubscriptionStateRequested|요청됨|  
|SubscriptionStateSuspended|일시 중단|  
|DefaultSubscriptionNameTemplate|{0}(기본값)|  
|SubscriptionNameTemplate|개발자 액세스 #{0}|  
|TextboxLabelSubscriptionName|구독 이름|  
|ValidationMessageSubscriptionNameRequired|구독 이름은 비워 둘 수 없습니다.|  
|ApiManagementUserLimitReached|이 서비스는 hello 최대 허용 된 사용자 수에 도달 했습니다. Tooa 높은 가격 책정 계층을 업그레이드 하십시오.|  
  
##  <a name="glyphs"></a> 문자 모양 리소스  
 API 관리 개발자 포털 템플릿 hello 문자 모양에서 צ ְ ײ [부트스트랩에서 Glyphicons](http://getbootstrap.com/components/#glyphicons)합니다. Hello에서 글꼴 형식의 250 개 이상의 문자를 포함 하는 문자 모양이이 집합 [Glyphicon](http://glyphicons.com/) Halflings 설정 합니다. 이 문자 모양 toouse 구문 다음 hello를 사용 하 여을 설정 합니다.  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Hello 문자 모양의 전체 목록을 보려면를 참조 하십시오. [부트스트랩에서 Glyphicons](http://getbootstrap.com/components/#glyphicons)합니다.

## <a name="next-steps"></a>다음 단계
서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.
