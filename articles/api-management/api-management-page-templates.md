---
title: "Azure API 관리에서 aaaPage 템플릿 | Microsoft Docs"
description: "Toocustomize 템플릿 집합을 사용 하 여 Azure API 관리에서 개발자 포털 페이지의 내용을 hello 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a>Azure API Management의 페이지 템플릿
Azure API 관리 개발자 포털 페이지 콘텐츠를 구성 하는 템플릿 집합을 사용 하 여 콘텐츠의 toocustomize hello 기능 hello를 제공 합니다. 사용 하 여 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 hello 편집기의 선택한와 같은 [디자이너에 대 한 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), 제공 된 집합을 지역화 [문자열 리소스](api-management-template-resources.md#strings), [ 문자 모양 리소스](api-management-template-resources.md#glyphs), 및 [컨트롤 페이지](api-management-page-controls.md), 이러한 템플릿을 사용 하 여 나타나며 hello 페이지의 뛰어난 유연성 tooconfigure hello 내용을 백업이 있어야 합니다.  
  
 이 섹션의 hello 템플릿을 사용 하면 toocustomize hello 내용의 hello 로그인으로 로그인의 로그인, 있으며 페이지 찾을 수 없음 페이지 hello 개발자 포털에서.  
  
-   [로그인](#SignIn)  
  
-   [등록](#SignUp)  
  
-   [페이지를 찾을 수 없음](#PageNotFound)  
  
> [!NOTE]
>  예제 기본 서식 파일 설명서, hello에 포함 되었지만 이러한 toocontinuous 개선 인해 주체 toochange 됩니다. 원하는 toohello 개별 서식 파일을 이동 하 여 hello 라이브 기본 템플릿 hello 개발자 포털에서 볼 수 있습니다. 서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.  
  
##  <a name="SignIn"></a> 로그인  
 hello **로그인** 템플릿을 사용 하 여 toocustomize hello 기호 hello 개발자 포털의 페이지에 있습니다.  
  
 ![로그인 페이지](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM 로그인 페이지 개발자 포털 템플릿")  
  
### <a name="default-template"></a>기본 템플릿  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a>컨트롤  
 이 템플릿은 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.  
  
-   [basic-signin](api-management-page-controls.md#basic-signin)  
  
-   [providers](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a>데이터 모델  
 [사용자 로그인](api-management-template-data-model-reference.md#UseSignIn) 엔터티입니다.  
  
### <a name="sample-template-data"></a>샘플 템플릿 데이터  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <a name="SignUp"></a> 등록  
 hello **등록** 템플릿을 사용 하 여 toocustomize hello 등록 페이지 hello 개발자 포털에서 합니다.  
  
 ![등록 페이지](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM 등록 페이지 개발자 포털 템플릿")  
  
### <a name="default-template"></a>기본 템플릿  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a>컨트롤  
 이 템플릿은 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.  
  
-   [sign-up](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a>데이터 모델  
 [사용자 등록](api-management-template-data-model-reference.md#UserSignUp) 엔터티입니다.  
  
### <a name="sample-template-data"></a>샘플 템플릿 데이터  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <a name="PageNotFound"></a> 페이지를 찾을 수 없음  
 hello **페이지 찾을 수 없음** 템플릿을 사용 하면 toocustomize hello 페이지 hello 개발자 포털에서 페이지를 찾을 수 없습니다.  
  
 ![페이지를 찾을 수 없음](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM 페이지를 찾을 수 없음 개발자 포털 템플릿")  
  
### <a name="default-template"></a>기본 템플릿  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a>컨트롤  
 이 템플릿은 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 없습니다.  
  
### <a name="data-model"></a>데이터 모델  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|referenceCode|string|이 페이지에서 내부 오류가의 hello 결과로 표시 된 경우 생성 된 코드입니다.|  
|errorCode|string|이 페이지에서 내부 오류가의 hello 결과로 표시 된 경우 생성 된 코드입니다.|  
|emailBody|string|이 페이지에서 내부 오류가의 hello 결과로 표시 된 경우 생성 된 본문 전자 메일입니다.|  
|requestedUrl|string|hello hello 페이지를 찾을 수 없는 경우 요청 된 URL입니다.|  
|referrerUrl|string|hello 참조 페이지 URL toohello 요청 된 URL입니다.|  
  
### <a name="sample-template-data"></a>샘플 템플릿 데이터  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a>다음 단계
서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.
