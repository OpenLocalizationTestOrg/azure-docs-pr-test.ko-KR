---
title: "Azure API Management의 페이지 템플릿 | Microsoft Docs"
description: "Azure API Management에서 템플릿 집합을 사용하여 개발자 포털 페이지의 콘텐츠를 사용자 지정하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 7f9ef37a694bce786b6acaa428df83f0cb23c2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="ed6e6-103">Azure API Management의 페이지 템플릿</span><span class="sxs-lookup"><span data-stu-id="ed6e6-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="ed6e6-104">Azure API Management는 해당 콘텐츠를 구성하는 템플릿 집합을 사용하여 개발자 포털 페이지의 콘텐츠를 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="ed6e6-105">이러한 템플릿에서 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) 및 제공된 지역화 [String 리소스](api-management-template-resources.md#strings), [Glyph 리소스](api-management-template-resources.md#glyphs) 및 [Page 컨트롤](api-management-page-controls.md)의 집합과 같은 선택한 편집기를 사용하여 필요에 따라 페이지 콘텐츠를 유연하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="ed6e6-106">이 섹션의 템플릿을 통해 개발자 포털에서 로그인, 등록, 페이지를 찾을 수 없음 페이지의 콘텐츠를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="ed6e6-107">로그인</span><span class="sxs-lookup"><span data-stu-id="ed6e6-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="ed6e6-108">등록</span><span class="sxs-lookup"><span data-stu-id="ed6e6-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="ed6e6-109">페이지를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="ed6e6-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="ed6e6-110">다음 문서에는 샘플 기본 템플릿이 포함되어 있지만 지속적인 향상으로 인해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="ed6e6-111">원하는 개별 템플릿으로 이동하여 개발자 포털에서 라이브 기본 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="ed6e6-112">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="ed6e6-113"><a name="SignIn"></a> 로그인</span><span class="sxs-lookup"><span data-stu-id="ed6e6-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="ed6e6-114">**로그인** 템플릿을 통해 개발자 포털에서 로그인 페이지를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="ed6e6-115">![로그인 페이지](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM 로그인 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="ed6e6-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ed6e6-116">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="ed6e6-116">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="ed6e6-117">컨트롤</span><span class="sxs-lookup"><span data-stu-id="ed6e6-117">Controls</span></span>  
 <span data-ttu-id="ed6e6-118">이 템플릿에서 다음 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-118">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ed6e6-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="ed6e6-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="ed6e6-120">providers</span><span class="sxs-lookup"><span data-stu-id="ed6e6-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="ed6e6-121">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="ed6e6-121">Data model</span></span>  
 <span data-ttu-id="ed6e6-122">[사용자 로그인](api-management-template-data-model-reference.md#UseSignIn) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="ed6e6-123">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="ed6e6-123">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="ed6e6-124"><a name="SignUp"></a> 등록</span><span class="sxs-lookup"><span data-stu-id="ed6e6-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="ed6e6-125">**로그인** 템플릿을 통해 개발자 포털에서 로그인 페이지를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="ed6e6-126">![등록 페이지](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM 등록 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="ed6e6-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ed6e6-127">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="ed6e6-127">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="ed6e6-128">컨트롤</span><span class="sxs-lookup"><span data-stu-id="ed6e6-128">Controls</span></span>  
 <span data-ttu-id="ed6e6-129">이 템플릿에서 다음 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-129">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ed6e6-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="ed6e6-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="ed6e6-131">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="ed6e6-131">Data model</span></span>  
 <span data-ttu-id="ed6e6-132">[사용자 등록](api-management-template-data-model-reference.md#UserSignUp) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="ed6e6-133">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="ed6e6-133">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="ed6e6-134"><a name="PageNotFound"></a> 페이지를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="ed6e6-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="ed6e6-135">**페이지를 찾을 수 없음** 템플릿을 통해 개발자 포털에서 페이지를 찾을 수 없음 페이지를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span></span>  
  
 <span data-ttu-id="ed6e6-136">![페이지를 찾을 수 없음](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM 페이지를 찾을 수 없음 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="ed6e6-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ed6e6-137">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="ed6e6-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="ed6e6-138">컨트롤</span><span class="sxs-lookup"><span data-stu-id="ed6e6-138">Controls</span></span>  
 <span data-ttu-id="ed6e6-139">이 템플릿은 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="ed6e6-140">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="ed6e6-140">Data model</span></span>  
  
|<span data-ttu-id="ed6e6-141">속성</span><span class="sxs-lookup"><span data-stu-id="ed6e6-141">Property</span></span>|<span data-ttu-id="ed6e6-142">형식</span><span class="sxs-lookup"><span data-stu-id="ed6e6-142">Type</span></span>|<span data-ttu-id="ed6e6-143">설명</span><span class="sxs-lookup"><span data-stu-id="ed6e6-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ed6e6-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="ed6e6-144">referenceCode</span></span>|<span data-ttu-id="ed6e6-145">string</span><span class="sxs-lookup"><span data-stu-id="ed6e6-145">string</span></span>|<span data-ttu-id="ed6e6-146">이 페이지가 내부 오류의 결과로 표시된 경우에 생성되는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-146">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="ed6e6-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="ed6e6-147">errorCode</span></span>|<span data-ttu-id="ed6e6-148">string</span><span class="sxs-lookup"><span data-stu-id="ed6e6-148">string</span></span>|<span data-ttu-id="ed6e6-149">이 페이지가 내부 오류의 결과로 표시된 경우에 생성되는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-149">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="ed6e6-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="ed6e6-150">emailBody</span></span>|<span data-ttu-id="ed6e6-151">string</span><span class="sxs-lookup"><span data-stu-id="ed6e6-151">string</span></span>|<span data-ttu-id="ed6e6-152">내부 오류로 인해이 페이지 표시 된 경우 생성 된 본문을 전자 메일로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-152">Email body generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="ed6e6-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="ed6e6-153">requestedUrl</span></span>|<span data-ttu-id="ed6e6-154">string</span><span class="sxs-lookup"><span data-stu-id="ed6e6-154">string</span></span>|<span data-ttu-id="ed6e6-155">페이지를 찾을 수 없는 경우 요청되는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-155">The URL requested when the page was not found.</span></span>|  
|<span data-ttu-id="ed6e6-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="ed6e6-156">referrerUrl</span></span>|<span data-ttu-id="ed6e6-157">string</span><span class="sxs-lookup"><span data-stu-id="ed6e6-157">string</span></span>|<span data-ttu-id="ed6e6-158">요청된 URL의 참조 페이지 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-158">The referrer URL to the requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ed6e6-159">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="ed6e6-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="ed6e6-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed6e6-160">Next steps</span></span>
<span data-ttu-id="ed6e6-161">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](api-management-developer-portal-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed6e6-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>