---
title: "Visual Studio MVC 프로젝트에서 Azure AD와 시작 됨 aaaGet | Microsoft Docs"
description: "연결 된 서비스 MVC 프로젝트에서 Azure Active Directory를 사용 하 여 Visual Studio를 사용 하 여 Azure AD를 만드는 tooor 연결한 후 tooget을 시작 하는 방법"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 807824dd6e4e57e443f8a7322cf2e5326384316d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a>Azure Active Directory 및 Visual Studio 연결 서비스 시작(MVC 프로젝트)
> [!div class="op_single_selector"]
> * [시작](vs-active-directory-dotnet-getting-started.md)
> * [변경된 내용](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>인증 tooaccess 컨트롤러 필요
프로젝트의 모든 컨트롤러 hello로 표시 된 **Authorize** 특성입니다. 이 특성에는 이러한 컨트롤러에 액세스 하기 전에 인증 하는 hello 사용자 toobe가 필요 합니다. 익명으로 액세스할 tooallow hello 컨트롤러 toobe hello 컨트롤러에서이 특성을 제거 합니다. 보다 세부적인 수준에서 tooset hello 사용 하려는 경우 toohello 컨트롤러 클래스를 적용 하는 대신 권한 부여를 사용 하는 hello 특성 tooeach 메서드에 적용 됩니다.

## <a name="adding-signin--signout-controls"></a>SignIn/SignOut 컨트롤 추가
tooadd hello SignIn/SignOut tooyour 보기를 제어, hello를 사용할 수 있습니다 **_LoginPartial.cshtml** 부분 뷰 tooadd hello 기능 tooone 보기. Hello 기능 추가 toohello 표준의 예로 **_Layout.cshtml** 보기. (참고 hello에서에서 마지막 요소 hello div 클래스 navbar 축소 포함):

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a>다음 단계
- [Azure Active Directory에 대한 자세한 정보](https://azure.microsoft.com/services/active-directory/) 

