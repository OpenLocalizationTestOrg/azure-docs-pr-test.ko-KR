---
title: "Azure API Management의 응용 프로그램 템플릿 | Microsoft Docs"
description: "Azure API Management의 개발자 포털에서 응용 프로그램 페이지의 콘텐츠를 사용자 지정하는 방법을 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 6d2d44465800219f16866a621d4822614ac9e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="9d8dc-103">Azure API Management의 응용 프로그램 템플릿</span><span class="sxs-lookup"><span data-stu-id="9d8dc-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="9d8dc-104">Azure API Management는 해당 콘텐츠를 구성하는 템플릿 집합을 사용하여 개발자 포털 페이지의 콘텐츠를 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="9d8dc-105">이러한 템플릿에서 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) 및 제공된 지역화 [String 리소스](api-management-template-resources.md#strings), [Glyph 리소스](api-management-template-resources.md#glyphs) 및 [Page 컨트롤](api-management-page-controls.md)의 집합과 같은 선택한 편집기를 사용하여 필요에 따라 페이지 콘텐츠를 유연하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="9d8dc-106">이 섹션의 템플릿을 사용하여 개발자 포털의 응용 프로그램 페이지의 콘텐츠를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="9d8dc-107">응용 프로그램 목록</span><span class="sxs-lookup"><span data-stu-id="9d8dc-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="9d8dc-108">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9d8dc-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="9d8dc-109">다음 문서에는 샘플 기본 템플릿이 포함되어 있지만 지속적인 향상으로 인해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="9d8dc-110">원하는 개별 템플릿으로 이동하여 개발자 포털에서 라이브 기본 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="9d8dc-111">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="9d8dc-112"><a name="ProductList"></a> 응용 프로그램 목록</span><span class="sxs-lookup"><span data-stu-id="9d8dc-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="9d8dc-113">**응용 프로그램 목록** 템플릿을 사용하여 개발자 포털에서 응용 프로그램 목록 페이지의 본문을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="9d8dc-114">![응용 프로그램 목록 페이지 개발자 포털 템플릿](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM 응용 프로그램 목록 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="9d8dc-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="9d8dc-115">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="9d8dc-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="9d8dc-116">컨트롤</span><span class="sxs-lookup"><span data-stu-id="9d8dc-116">Controls</span></span>  
 <span data-ttu-id="9d8dc-117">`Product list` 템플릿에서 다음 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="9d8dc-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="9d8dc-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="9d8dc-119">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="9d8dc-119">Data model</span></span>  
  
|<span data-ttu-id="9d8dc-120">속성</span><span class="sxs-lookup"><span data-stu-id="9d8dc-120">Property</span></span>|<span data-ttu-id="9d8dc-121">형식</span><span class="sxs-lookup"><span data-stu-id="9d8dc-121">Type</span></span>|<span data-ttu-id="9d8dc-122">설명</span><span class="sxs-lookup"><span data-stu-id="9d8dc-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="9d8dc-123">페이징</span><span class="sxs-lookup"><span data-stu-id="9d8dc-123">Paging</span></span>|<span data-ttu-id="9d8dc-124">[페이징](api-management-template-data-model-reference.md#Paging) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="9d8dc-125">응용 프로그램 컬렉션에 대한 페이징 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="9d8dc-126">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9d8dc-126">Applications</span></span>|<span data-ttu-id="9d8dc-127">[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="9d8dc-128">현재 사용자에게 표시되는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="9d8dc-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="9d8dc-129">CategoryName</span></span>|<span data-ttu-id="9d8dc-130">string</span><span class="sxs-lookup"><span data-stu-id="9d8dc-130">string</span></span>|<span data-ttu-id="9d8dc-131">응용 프로그램의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="9d8dc-132">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="9d8dc-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="9d8dc-133"><a name="Application"></a> 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9d8dc-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="9d8dc-134">**응용 프로그램** 템플릿을 사용하여 개발자 포털에서 응용 프로그램 페이지의 본문을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="9d8dc-135">![응용 프로그램 페이지 개발자 포털 템플릿](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM 응용 프로그램 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="9d8dc-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="9d8dc-136">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="9d8dc-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="9d8dc-137">컨트롤</span><span class="sxs-lookup"><span data-stu-id="9d8dc-137">Controls</span></span>  
 <span data-ttu-id="9d8dc-138">`Application` 템플릿에서는 [컨트롤 페이지](api-management-page-controls.md) 사용을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="9d8dc-139">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="9d8dc-139">Data model</span></span>  
 <span data-ttu-id="9d8dc-140">[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="9d8dc-141">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="9d8dc-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="9d8dc-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d8dc-142">Next steps</span></span>
<span data-ttu-id="9d8dc-143">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](api-management-developer-portal-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d8dc-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>