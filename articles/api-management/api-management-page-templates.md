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
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="b3dd5-103">Azure API Management의 페이지 템플릿</span><span class="sxs-lookup"><span data-stu-id="b3dd5-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="b3dd5-104">Azure API 관리 개발자 포털 페이지 콘텐츠를 구성 하는 템플릿 집합을 사용 하 여 콘텐츠의 toocustomize hello 기능 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="b3dd5-105">사용 하 여 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 hello 편집기의 선택한와 같은 [디자이너에 대 한 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), 제공 된 집합을 지역화 [문자열 리소스](api-management-template-resources.md#strings), [ 문자 모양 리소스](api-management-template-resources.md#glyphs), 및 [컨트롤 페이지](api-management-page-controls.md), 이러한 템플릿을 사용 하 여 나타나며 hello 페이지의 뛰어난 유연성 tooconfigure hello 내용을 백업이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="b3dd5-106">이 섹션의 hello 템플릿을 사용 하면 toocustomize hello 내용의 hello 로그인으로 로그인의 로그인, 있으며 페이지 찾을 수 없음 페이지 hello 개발자 포털에서.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-106">hello templates in this section allow you toocustomize hello content of hello sign in, sign up, and page not found pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="b3dd5-107">로그인</span><span class="sxs-lookup"><span data-stu-id="b3dd5-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="b3dd5-108">등록</span><span class="sxs-lookup"><span data-stu-id="b3dd5-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="b3dd5-109">페이지를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="b3dd5-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="b3dd5-110">예제 기본 서식 파일 설명서, hello에 포함 되었지만 이러한 toocontinuous 개선 인해 주체 toochange 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-110">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="b3dd5-111">원하는 toohello 개별 서식 파일을 이동 하 여 hello 라이브 기본 템플릿 hello 개발자 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-111">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="b3dd5-112">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-112">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="b3dd5-113"><a name="SignIn"></a> 로그인</span><span class="sxs-lookup"><span data-stu-id="b3dd5-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="b3dd5-114">hello **로그인** 템플릿을 사용 하 여 toocustomize hello 기호 hello 개발자 포털의 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-114">hello **sign in** template allows you toocustomize hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="b3dd5-115">![로그인 페이지](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM 로그인 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="b3dd5-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b3dd5-116">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="b3dd5-116">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="b3dd5-117">컨트롤</span><span class="sxs-lookup"><span data-stu-id="b3dd5-117">Controls</span></span>  
 <span data-ttu-id="b3dd5-118">이 템플릿은 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-118">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="b3dd5-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="b3dd5-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="b3dd5-120">providers</span><span class="sxs-lookup"><span data-stu-id="b3dd5-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="b3dd5-121">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="b3dd5-121">Data model</span></span>  
 <span data-ttu-id="b3dd5-122">[사용자 로그인](api-management-template-data-model-reference.md#UseSignIn) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="b3dd5-123">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="b3dd5-123">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="b3dd5-124"><a name="SignUp"></a> 등록</span><span class="sxs-lookup"><span data-stu-id="b3dd5-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="b3dd5-125">hello **등록** 템플릿을 사용 하 여 toocustomize hello 등록 페이지 hello 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-125">hello **sign up** template allows you toocustomize hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="b3dd5-126">![등록 페이지](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM 등록 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="b3dd5-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b3dd5-127">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="b3dd5-127">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="b3dd5-128">컨트롤</span><span class="sxs-lookup"><span data-stu-id="b3dd5-128">Controls</span></span>  
 <span data-ttu-id="b3dd5-129">이 템플릿은 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-129">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="b3dd5-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="b3dd5-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="b3dd5-131">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="b3dd5-131">Data model</span></span>  
 <span data-ttu-id="b3dd5-132">[사용자 등록](api-management-template-data-model-reference.md#UserSignUp) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="b3dd5-133">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="b3dd5-133">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="b3dd5-134"><a name="PageNotFound"></a> 페이지를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="b3dd5-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="b3dd5-135">hello **페이지 찾을 수 없음** 템플릿을 사용 하면 toocustomize hello 페이지 hello 개발자 포털에서 페이지를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-135">hello **page not found** template allows you toocustomize hello page not found page in hello developer portal.</span></span>  
  
 <span data-ttu-id="b3dd5-136">![페이지를 찾을 수 없음](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM 페이지를 찾을 수 없음 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="b3dd5-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b3dd5-137">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="b3dd5-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="b3dd5-138">컨트롤</span><span class="sxs-lookup"><span data-stu-id="b3dd5-138">Controls</span></span>  
 <span data-ttu-id="b3dd5-139">이 템플릿은 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="b3dd5-140">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="b3dd5-140">Data model</span></span>  
  
|<span data-ttu-id="b3dd5-141">속성</span><span class="sxs-lookup"><span data-stu-id="b3dd5-141">Property</span></span>|<span data-ttu-id="b3dd5-142">형식</span><span class="sxs-lookup"><span data-stu-id="b3dd5-142">Type</span></span>|<span data-ttu-id="b3dd5-143">설명</span><span class="sxs-lookup"><span data-stu-id="b3dd5-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="b3dd5-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="b3dd5-144">referenceCode</span></span>|<span data-ttu-id="b3dd5-145">string</span><span class="sxs-lookup"><span data-stu-id="b3dd5-145">string</span></span>|<span data-ttu-id="b3dd5-146">이 페이지에서 내부 오류가의 hello 결과로 표시 된 경우 생성 된 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-146">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="b3dd5-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="b3dd5-147">errorCode</span></span>|<span data-ttu-id="b3dd5-148">string</span><span class="sxs-lookup"><span data-stu-id="b3dd5-148">string</span></span>|<span data-ttu-id="b3dd5-149">이 페이지에서 내부 오류가의 hello 결과로 표시 된 경우 생성 된 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-149">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="b3dd5-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="b3dd5-150">emailBody</span></span>|<span data-ttu-id="b3dd5-151">string</span><span class="sxs-lookup"><span data-stu-id="b3dd5-151">string</span></span>|<span data-ttu-id="b3dd5-152">이 페이지에서 내부 오류가의 hello 결과로 표시 된 경우 생성 된 본문 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-152">Email body generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="b3dd5-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="b3dd5-153">requestedUrl</span></span>|<span data-ttu-id="b3dd5-154">string</span><span class="sxs-lookup"><span data-stu-id="b3dd5-154">string</span></span>|<span data-ttu-id="b3dd5-155">hello hello 페이지를 찾을 수 없는 경우 요청 된 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-155">hello URL requested when hello page was not found.</span></span>|  
|<span data-ttu-id="b3dd5-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="b3dd5-156">referrerUrl</span></span>|<span data-ttu-id="b3dd5-157">string</span><span class="sxs-lookup"><span data-stu-id="b3dd5-157">string</span></span>|<span data-ttu-id="b3dd5-158">hello 참조 페이지 URL toohello 요청 된 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-158">hello referrer URL toohello requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="b3dd5-159">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="b3dd5-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="b3dd5-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3dd5-160">Next steps</span></span>
<span data-ttu-id="b3dd5-161">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3dd5-161">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
