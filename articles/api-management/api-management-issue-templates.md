---
title: "Azure API Management의 문제 템플릿 | Microsoft Docs"
description: "Azure API Management의 개발자 포털에서 문제 페이지의 콘텐츠를 사용자 지정하는 방법을 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="38648-103">Azure API Management의 문제 템플릿</span><span class="sxs-lookup"><span data-stu-id="38648-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="38648-104">Azure API Management는 해당 콘텐츠를 구성하는 템플릿 집합을 사용하여 개발자 포털 페이지의 콘텐츠를 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="38648-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="38648-105">이러한 템플릿에서 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) 및 제공된 지역화 [String 리소스](api-management-template-resources.md#strings), [Glyph 리소스](api-management-template-resources.md#glyphs) 및 [Page 컨트롤](api-management-page-controls.md)의 집합과 같은 선택한 편집기를 사용하여 필요에 따라 페이지 콘텐츠를 유연하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38648-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="38648-106">이 섹션의 템플릿을 통해 개발자 포털에서 문제 페이지의 콘텐츠를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38648-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="38648-107">문제 목록</span><span class="sxs-lookup"><span data-stu-id="38648-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="38648-108">다음 문서에는 샘플 기본 템플릿이 포함되어 있지만 지속적인 향상으로 인해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38648-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="38648-109">원하는 개별 템플릿으로 이동하여 개발자 포털에서 라이브 기본 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38648-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="38648-110">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](api-management-developer-portal-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38648-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="38648-111"><a name="IssueList"></a> 문제 목록</span><span class="sxs-lookup"><span data-stu-id="38648-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="38648-112">**문제 목록** 템플릿을 통해 개발자 포털에서 문제 목록 페이지의 본문을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38648-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="38648-113">![문제 목록 개발자 포털](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM 문제 목록 개발자 포털")</span><span class="sxs-lookup"><span data-stu-id="38648-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="38648-114">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="38648-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="38648-115">컨트롤</span><span class="sxs-lookup"><span data-stu-id="38648-115">Controls</span></span>  
 <span data-ttu-id="38648-116">`Issue list` 템플릿에서 다음 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38648-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="38648-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="38648-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="38648-118">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="38648-118">Data model</span></span>  
  
|<span data-ttu-id="38648-119">속성</span><span class="sxs-lookup"><span data-stu-id="38648-119">Property</span></span>|<span data-ttu-id="38648-120">형식</span><span class="sxs-lookup"><span data-stu-id="38648-120">Type</span></span>|<span data-ttu-id="38648-121">설명</span><span class="sxs-lookup"><span data-stu-id="38648-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="38648-122">문제</span><span class="sxs-lookup"><span data-stu-id="38648-122">Issues</span></span>|<span data-ttu-id="38648-123">[문제](api-management-template-data-model-reference.md#Issue) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="38648-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="38648-124">현재 사용자에게 표시되는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="38648-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="38648-125">페이징</span><span class="sxs-lookup"><span data-stu-id="38648-125">Paging</span></span>|<span data-ttu-id="38648-126">[페이징](api-management-template-data-model-reference.md#Paging) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="38648-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="38648-127">응용 프로그램 컬렉션에 대한 페이징 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="38648-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="38648-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="38648-128">IsAuthenticated</span></span>|<span data-ttu-id="38648-129">부울</span><span class="sxs-lookup"><span data-stu-id="38648-129">boolean</span></span>|<span data-ttu-id="38648-130">현재 사용자가 개발자 포털에 로그인했는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="38648-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="38648-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="38648-131">CanReportIssues</span></span>|<span data-ttu-id="38648-132">부울</span><span class="sxs-lookup"><span data-stu-id="38648-132">boolean</span></span>|<span data-ttu-id="38648-133">현재 사용자에게 문제를 접수할 권한이 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="38648-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="38648-134">이를 통해 검색</span><span class="sxs-lookup"><span data-stu-id="38648-134">Search</span></span>|<span data-ttu-id="38648-135">string</span><span class="sxs-lookup"><span data-stu-id="38648-135">string</span></span>|<span data-ttu-id="38648-136">이 속성은 사용되지 않으며 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="38648-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="38648-137">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="38648-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="38648-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38648-138">Next steps</span></span>
<span data-ttu-id="38648-139">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](api-management-developer-portal-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38648-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>