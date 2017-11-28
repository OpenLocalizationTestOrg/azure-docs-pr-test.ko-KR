---
title: "Azure API 관리에서 aaaApplication 템플릿 | Microsoft Docs"
description: "Toocustomize hello Azure API 관리 개발자 포털에 hello 응용 프로그램 페이지의 내용을 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="d600b-103">Azure API Management의 응용 프로그램 템플릿</span><span class="sxs-lookup"><span data-stu-id="d600b-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="d600b-104">Azure API 관리 개발자 포털 페이지 콘텐츠를 구성 하는 템플릿 집합을 사용 하 여 콘텐츠의 toocustomize hello 기능 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="d600b-105">사용 하 여 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 hello 편집기의 선택한와 같은 [디자이너에 대 한 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), 제공 된 집합을 지역화 [문자열 리소스](api-management-template-resources.md#strings), [ 문자 모양 리소스](api-management-template-resources.md#glyphs), 및 [컨트롤 페이지](api-management-page-controls.md), 이러한 템플릿을 사용 하 여 나타나며 hello 페이지의 뛰어난 유연성 tooconfigure hello 내용을 백업이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="d600b-106">이 섹션의 hello 템플릿을 hello 개발자 포털에서 toocustomize hello 내용의 hello 응용 프로그램 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="d600b-107">응용 프로그램 목록</span><span class="sxs-lookup"><span data-stu-id="d600b-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="d600b-108">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d600b-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="d600b-109">예제 기본 서식 파일 설명서, hello에 포함 되었지만 이러한 toocontinuous 개선 인해 주체 toochange 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="d600b-110">원하는 toohello 개별 서식 파일을 이동 하 여 hello 라이브 기본 템플릿 hello 개발자 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="d600b-111">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="d600b-112"><a name="ProductList"></a> 응용 프로그램 목록</span><span class="sxs-lookup"><span data-stu-id="d600b-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="d600b-113">hello **응용 프로그램 목록** 템플릿을 사용 하 여 hello 응용 프로그램 목록 페이지의 toocustomize hello 본문 hello 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d600b-114">![응용 프로그램 목록 페이지 개발자 포털 템플릿](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM 응용 프로그램 목록 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="d600b-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d600b-115">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="d600b-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="d600b-116">컨트롤</span><span class="sxs-lookup"><span data-stu-id="d600b-116">Controls</span></span>  
 <span data-ttu-id="d600b-117">hello `Product list` 템플릿 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="d600b-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="d600b-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="d600b-119">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="d600b-119">Data model</span></span>  
  
|<span data-ttu-id="d600b-120">속성</span><span class="sxs-lookup"><span data-stu-id="d600b-120">Property</span></span>|<span data-ttu-id="d600b-121">형식</span><span class="sxs-lookup"><span data-stu-id="d600b-121">Type</span></span>|<span data-ttu-id="d600b-122">설명</span><span class="sxs-lookup"><span data-stu-id="d600b-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d600b-123">페이징</span><span class="sxs-lookup"><span data-stu-id="d600b-123">Paging</span></span>|<span data-ttu-id="d600b-124">[페이징](api-management-template-data-model-reference.md#Paging) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="d600b-125">hello hello 응용 프로그램 컬렉션에 대 한 페이징 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="d600b-126">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d600b-126">Applications</span></span>|<span data-ttu-id="d600b-127">[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="d600b-128">hello 응용 프로그램 표시 toohello 현재 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="d600b-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="d600b-129">CategoryName</span></span>|<span data-ttu-id="d600b-130">string</span><span class="sxs-lookup"><span data-stu-id="d600b-130">string</span></span>|<span data-ttu-id="d600b-131">응용 프로그램의 hello 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d600b-132">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="d600b-132">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="d600b-133"><a name="Application"></a> 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d600b-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="d600b-134">hello **응용 프로그램** 템플릿을 사용 하 여 hello 응용 프로그램 페이지의 toocustomize hello 본문 hello 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d600b-135">![응용 프로그램 페이지 개발자 포털 템플릿](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM 응용 프로그램 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="d600b-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d600b-136">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="d600b-136">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="d600b-137">컨트롤</span><span class="sxs-lookup"><span data-stu-id="d600b-137">Controls</span></span>  
 <span data-ttu-id="d600b-138">hello `Application` 서식 파일의 hello 사용 하지 못하도록 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="d600b-139">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="d600b-139">Data model</span></span>  
 <span data-ttu-id="d600b-140">[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="d600b-141">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="d600b-141">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="d600b-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d600b-142">Next steps</span></span>
<span data-ttu-id="d600b-143">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d600b-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
