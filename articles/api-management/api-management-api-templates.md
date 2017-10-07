---
title: "Azure API 관리에서 aaaAPI 템플릿 | Microsoft Docs"
description: "Toocustomize hello Azure API 관리 개발자 포털에 hello API 페이지의 내용을 hello 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3642fd09-ba98-4358-93a6-c48ab0500431
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: fdfa76167cfaf3b23b22d6321904f34da077fecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="api-templates-in-azure-api-management"></a><span data-ttu-id="26a27-103">Azure API Management의 API 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-103">API templates in Azure API Management</span></span>
<span data-ttu-id="26a27-104">Azure API 관리 개발자 포털 페이지 콘텐츠를 구성 하는 템플릿 집합을 사용 하 여 콘텐츠의 toocustomize hello 기능 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="26a27-105">사용 하 여 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 hello 편집기의 선택한와 같은 [디자이너에 대 한 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), 제공 된 집합을 지역화 [문자열 리소스](api-management-template-resources.md#strings), [ 문자 모양 리소스](api-management-template-resources.md#glyphs), 및 [컨트롤 페이지](api-management-page-controls.md), 이러한 템플릿을 사용 하 여 나타나며 hello 페이지의 뛰어난 유연성 tooconfigure hello 내용을 백업이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="26a27-106">이 섹션의 hello 템플릿 hello 개발자 포털에서 hello API 페이지의 toocustomize hello 내용을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-106">hello templates in this section allow you toocustomize hello content of hello API pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="26a27-107">API 목록</span><span class="sxs-lookup"><span data-stu-id="26a27-107">API list</span></span>](#APIList)  
-   [<span data-ttu-id="26a27-108">작업</span><span class="sxs-lookup"><span data-stu-id="26a27-108">Operation</span></span>](#Product)  
-   [<span data-ttu-id="26a27-109">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="26a27-109">Code samples</span></span>](#CodeSamples)  
    -   [<span data-ttu-id="26a27-110">Curl</span><span class="sxs-lookup"><span data-stu-id="26a27-110">Curl</span></span>](#Curl)  
    -   [<span data-ttu-id="26a27-111">C#</span><span class="sxs-lookup"><span data-stu-id="26a27-111">C#</span></span>](#CSharp)  
    -   [<span data-ttu-id="26a27-112">Java</span><span class="sxs-lookup"><span data-stu-id="26a27-112">Java</span></span>](#Stub)  
    -   [<span data-ttu-id="26a27-113">JavaScript</span><span class="sxs-lookup"><span data-stu-id="26a27-113">JavaScript</span></span>](#JavaScript)  
    -   [<span data-ttu-id="26a27-114">Objective C</span><span class="sxs-lookup"><span data-stu-id="26a27-114">Objective C</span></span>](#ObjectiveC)  
    -   [<span data-ttu-id="26a27-115">PHP</span><span class="sxs-lookup"><span data-stu-id="26a27-115">PHP</span></span>](#PHP)  
    -   [<span data-ttu-id="26a27-116">Python</span><span class="sxs-lookup"><span data-stu-id="26a27-116">Python</span></span>](#Python)  
    -   [<span data-ttu-id="26a27-117">Ruby</span><span class="sxs-lookup"><span data-stu-id="26a27-117">Ruby</span></span>](#Ruby)  

> [!NOTE]
>  <span data-ttu-id="26a27-118">예제 기본 서식 파일 설명서, hello에 포함 되었지만 이러한 toocontinuous 개선 인해 주체 toochange 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-118">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="26a27-119">원하는 toohello 개별 서식 파일을 이동 하 여 hello 라이브 기본 템플릿 hello 개발자 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-119">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="26a27-120">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-120">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="26a27-121"><a name="APIList"></a> API 목록</span><span class="sxs-lookup"><span data-stu-id="26a27-121"><a name="APIList"></a> API list</span></span>  
 <span data-ttu-id="26a27-122">hello **API 목록** 템플릿을 사용 하 여 hello API 목록 페이지의 toocustomize hello 본문 hello 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-122">hello **API list** template allows you toocustomize hello body of hello API list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="26a27-123">![개발자 포털 API 목록](./media/api-management-api-templates/APIM-Developer-Portal-Templates-API-List.png "APIM 개발자 포털 템플릿 API 목록")</span><span class="sxs-lookup"><span data-stu-id="26a27-123">![Developer Portal API List](./media/api-management-api-templates/APIM-Developer-Portal-Templates-API-List.png "APIM Developer Portal Templates API List")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="26a27-124">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-124">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ApisStrings|PageTitleApis" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if apis.size > 0 %}  
    <ol class="list-unstyled">  
    {% for api in apis %}  
        <li>  
        <h3>  
          <a href="/docs/services/{{api.id}}">{{api.name}}</a>  
        </h3>  
       {{api.description}}  
      </li>  
    {% endfor %}  
    </ol>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="26a27-125">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-125">Controls</span></span>  
 <span data-ttu-id="26a27-126">hello `API list` 템플릿 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-126">hello `API list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="26a27-127">paging-control</span><span class="sxs-lookup"><span data-stu-id="26a27-127">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="26a27-128">검색 컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-128">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="26a27-129">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-129">Data model</span></span>  
  
|<span data-ttu-id="26a27-130">속성</span><span class="sxs-lookup"><span data-stu-id="26a27-130">Property</span></span>|<span data-ttu-id="26a27-131">형식</span><span class="sxs-lookup"><span data-stu-id="26a27-131">Type</span></span>|<span data-ttu-id="26a27-132">설명</span><span class="sxs-lookup"><span data-stu-id="26a27-132">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="26a27-133">apis</span><span class="sxs-lookup"><span data-stu-id="26a27-133">apis</span></span>|<span data-ttu-id="26a27-134">[API 요약](api-management-template-data-model-reference.md#APISummary) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-134">Collection of [API summary](api-management-template-data-model-reference.md#APISummary) entities.</span></span>|<span data-ttu-id="26a27-135">hello Api 표시 toohello 현재 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-135">hello APIs visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="26a27-136">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-136">Sample template data</span></span>  
  
```json  
{  
    "apis": [  
        {  
            "id": "570275f1b16653124c8f9ba3",  
            "name": "Basic Calculator",  
            "description": "Arithmetics is just a call away!"  
        },  
        {  
            "id": "57026e30de15d80041040001",  
            "name": "Echo API",  
            "description": null  
        }  
    ],  
    "pageTitle": "APIs"  
}  
```  
  
##  <span data-ttu-id="26a27-137"><a name="Product"></a> 작업</span><span class="sxs-lookup"><span data-stu-id="26a27-137"><a name="Product"></a> Operation</span></span>  
 <span data-ttu-id="26a27-138">hello **작업** 템플릿을 사용 하 여 hello 작업 페이지의 toocustomize hello 본문 hello 개발자 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-138">hello **Operation** template allows you toocustomize hello body of hello operation page in hello developer portal.</span></span>  
  
 <span data-ttu-id="26a27-139">![개발자 포털 작업 페이지](./media/api-management-api-templates/APIM-Developer-Portal-templates-Operation-page.png "APIM 개발자 포털 템플릿 작업 페이지")</span><span class="sxs-lookup"><span data-stu-id="26a27-139">![Developer Portal Operation page](./media/api-management-api-templates/APIM-Developer-Portal-templates-Operation-page.png "APIM Developer Portal templates Operation page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="26a27-140">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-140">Default template</span></span>  
  
```xml  
<h2>{{api.name}}</h2>  
<p>{{api.description }}</p>  
  
<div class="panel">  
    <h3>{{operation.name}}</h3>  
    <p>{{operation.description }}</p>  
    <a class="btn btn-primary" href="{{consoleUrl}}" id="btnOpenConsole" role="button">  
        Try it  
    </a>  
</div>  
  
<h4>{% localized "Documentation|SectionHeadingRequestUrl" %}</h4>  
<div class="panel">  
    <div class="panel-body">  
        <label>{{ sampleUrl | escape }}</label>  
    </div>  
</div>  
  
{% if operation.request %}  
    {% if operation.request.parameters.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestParameters" %}</h4>  
  
        <div class="panel">  
            {% for parameter in operation.request.parameters %}  
                 <div class="row panel-body">  
                    <div class="col-md-3">  
                        <label>{{parameter.name}}</label>  
                        {% unless parameter.required %}  
                            <span class="text-muted">({% localized "Documentation|FormLabelSubtextOptional" %})</span>  
                        {% endunless %}  
                    </div>  
                    <div class="col-md-1">  
                        {{parameter.typeName}}  
                    </div>  
                    <div class="col-md-8">  
                        {{parameter.description}}  
                    </div>  
                 </div>  
            {% endfor %}  
        </div>  
    {% endif %}  
  
    {% if operation.request.headers.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestHeaders" %}</h4>  
        <div class="panel">  
            {% for header in operation.request.headers %}  
                 <div class="row panel-body">  
                    <div class="col-md-3">  
                        <label>{{header.name}}</label>  
                        {%unless header.required %}  
                            <span class="text-muted">({% localized "Documentation|FormLabelSubtextOptional" %})</span>  
                        {% endunless %}  
                    </div>  
                    <div class="col-md-1">  
                        {{header.typeName}}  
                    </div>  
                    <div class="col-md-8">  
                        {{header.description}}  
                    </div>  
                 </div>  
            {% endfor %}  
        </div>  
    {% endif %}  
  
    {% if operation.request.description or operation.request.representations.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestBody" %}</h4>  
        <div class="panel">  
            {% if operation.request.description %}  
                <p>{{operation.request.description }}</p>     
            {% endif %}  
  
            {% if operation.request.representations.size > 0 %}  
                <div role="tabpanel">  
                    <ul class="nav nav-tabs" role="tablist">  
                        {% for representation in operation.request.representations %}  
                            <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                                <a href="#requesttab{{forloop.index}}" role="tab" data-toggle="tab">  
                                    {{representation.contentType}}  
                                </a>  
                            </li>  
                        {% endfor %}  
                    </ul>  
                    <div class="tab-content tab-content-boxed">  
                        {% for representation in operation.request.representations %}  
                            <div id="requesttab{{forloop.index}}" role="tabpanel" class="tab-pane snippet{% if forloop.first %} active{% endif %}">  
  
                                {% if representation.sample or representation.schema %}   
                                <div role="tabpanel">  
                                    {% if representation.sample and representation.schema %}   
                                    <ul class="nav nav-tabs-borderless" role="tablist">  
                                        <li role="presentation" class="active">  
                                            <a href="#requesttab{{forloop.index}}sample" role="tab" data-toggle="tab">Sample</a>  
                                        </li>  
                                        <li role="presentation">  
                                            <a href="#requesttab{{forloop.index}}schema" role="tab" data-toggle="tab">Schema</a>  
                                        </li>  
                                    </ul>  
                                    {% endif %}  
  
                                    <div class="tab-content">  
                                        {% if representation.sample %}  
                                        <div id="requesttab{{forloop.index}}sample" role="tabpanel" class="tab-pane snippet active">  
                                            <pre><code class="{{representation.Brush}}">{{ representation.sample | escape }}</code></pre>  
                                        </div>  
                                        {% endif %}  
  
                                        {% if representation.schema %}  
                                        <div id="requesttab{{forloop.index}}schema" role="tabpanel" class="tab-pane snippet">  
                                            <pre><code class="{{representation.Brush}}">{{ representation.schema | escape }}</code></pre>  
                                        </div>  
                                        {% endif %}  
                                    </div>  
                                </div>  
                                {% endif %}  
                            </div>  
                        {% endfor %}  
                    </div>  
                </div>  
            {% endif %}  
  
            <div class="clearfix"></div>  
        </div>  
    {% endif %}  
{% endif %}  
  
{% if operation.responses.size > 0 %}  
    {% for response in operation.responses %}  
        {% if response.description or response.representations.size > 0 %}  
            <h4>{% localized "Documentation|SectionHeadingResponse" %} {{response.statusCode}}</h4>  
  
            <div class="panel">  
                {% if response.description %}  
                    <p>{{ response.description }}</p>  
                {% endif %}  
  
                {% if response.representations.size > 0 %}  
                    <div role="tabpanel">  
                        <ul class="nav nav-tabs" role="tablist">  
                            {% for representation in response.representations %}  
                                <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                                    <a href="#response{{response.statusCode}}tab{{forloop.index}}" role="tab" data-toggle="tab">  
                                        {{representation.contentType}}  
                                    </a>  
                                </li>  
                            {% endfor %}  
                        </ul>  
                        <div class="tab-content tab-content-boxed">  
                            {% for representation in response.representations %}  
                                <div id="response{{response.statusCode}}tab{{forloop.index}}" role="tabpanel" class="tab-pane snippet{% if forloop.first %} active{% endif %}">  
  
                                    {% if representation.sample or representation.schema %}  
                                    <div role="tabpanel">  
  
                                        {% if representation.sample and representation.schema %}  
                                        <ul class="nav nav-tabs-borderless" role="tablist">  
                                            <li role="presentation" class="active">  
                                                <a href="#response{{response.statusCode}}tab{{forloop.index}}sample" role="tab" data-toggle="tab">  
                                                    Sample  
                                                </a>  
                                            </li>  
                                            <li role="presentation">  
                                                <a href="#response{{response.statusCode}}tab{{forloop.index}}schema" role="tab" data-toggle="tab">  
                                                    Schema  
                                                </a>  
                                            </li>  
                                        </ul>  
                                        {% endif %}  
  
                                        <div class="tab-content">  
                                            {% if representation.sample %}  
                                            <div id="response{{response.statusCode}}tab{{forloop.index}}sample" role="tabpanel" class="tab-pane snippet active">  
                                                <pre><code class="{{representation.Brush}}">{{ representation.sample | escape }}</code></pre>  
                                            </div>  
                                            {% endif %}  
  
                                            {% if representation.schema %}  
                                            <div id="response{{response.statusCode}}tab{{forloop.index}}schema" role="tabpanel" class="tab-pane snippet">  
                                                <pre><code class="{{representation.Brush}}">{{ representation.schema | escape }}</code></pre>  
                                            </div>  
                                            {% endif %}  
                                        </div>  
                                    </div>  
                                    {% endif %}  
                                </div>  
                            {% endfor %}  
                        </div>  
                    </div>  
                {% endif %}  
  
                <div class="clearfix"></div>  
            </div>  
  
        {% endif %}  
    {% endfor %}  
{% endif %}  
  
<h4>{% localized "Documentation|SectionHeadingCodeSamples" %}</h4>  
<div role="tabpanel">  
    <ul class="nav nav-tabs" role="tablist">  
        {% for sample in samples %}  
            <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                <a href="#{{sample.brush}}" aria-controls="{{sample.brush}}" role="tab" data-toggle="tab">  
                    {{sample.title}}  
                </a>  
            </li>  
        {% endfor %}  
    </ul>  
    <div class="tab-content tab-content-boxed" title="{% localized "Documentation|TooltipTextDoubleClickToSelectAll=""" %}">  
        {% for sample in samples %}  
            <div role="tabpanel" class="tab-pane tab-content-boxed {% if forloop.first %} active{% endif %} snippet snippet-resizable" id="{{sample.brush}}" >  
                <pre><code class="{{sample.brush}}">{% partial sample.template for sample in samples %}</code></pre>  
            </div>  
        {% endfor %}  
    </div>  
    <div class="clearfix"></div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="26a27-141">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-141">Controls</span></span>  
 <span data-ttu-id="26a27-142">hello `Operation` 서식 파일의 hello 사용 하지 못하도록 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-142">hello `Operation` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="26a27-143">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-143">Data model</span></span>  
  
|<span data-ttu-id="26a27-144">속성</span><span class="sxs-lookup"><span data-stu-id="26a27-144">Property</span></span>|<span data-ttu-id="26a27-145">형식</span><span class="sxs-lookup"><span data-stu-id="26a27-145">Type</span></span>|<span data-ttu-id="26a27-146">설명</span><span class="sxs-lookup"><span data-stu-id="26a27-146">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="26a27-147">apiId</span><span class="sxs-lookup"><span data-stu-id="26a27-147">apiId</span></span>|<span data-ttu-id="26a27-148">string</span><span class="sxs-lookup"><span data-stu-id="26a27-148">string</span></span>|<span data-ttu-id="26a27-149">hello 현재 API의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-149">hello id of hello current API.</span></span>|  
|<span data-ttu-id="26a27-150">apiName</span><span class="sxs-lookup"><span data-stu-id="26a27-150">apiName</span></span>|<span data-ttu-id="26a27-151">string</span><span class="sxs-lookup"><span data-stu-id="26a27-151">string</span></span>|<span data-ttu-id="26a27-152">hello API의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-152">hello name of hello API.</span></span>|  
|<span data-ttu-id="26a27-153">apiDescription</span><span class="sxs-lookup"><span data-stu-id="26a27-153">apiDescription</span></span>|<span data-ttu-id="26a27-154">string</span><span class="sxs-lookup"><span data-stu-id="26a27-154">string</span></span>|<span data-ttu-id="26a27-155">Hello API의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-155">A description of hello API.</span></span>|  
|<span data-ttu-id="26a27-156">api</span><span class="sxs-lookup"><span data-stu-id="26a27-156">api</span></span>|<span data-ttu-id="26a27-157">[API 요약](api-management-template-data-model-reference.md#APISummary) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-157">[API summary](api-management-template-data-model-reference.md#APISummary) entity.</span></span>|<span data-ttu-id="26a27-158">hello 현재 API입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-158">hello current API.</span></span>|  
|<span data-ttu-id="26a27-159">operation</span><span class="sxs-lookup"><span data-stu-id="26a27-159">operation</span></span>|[<span data-ttu-id="26a27-160">작업</span><span class="sxs-lookup"><span data-stu-id="26a27-160">Operation</span></span>](api-management-template-data-model-reference.md#Operation)|<span data-ttu-id="26a27-161">hello는 현재 작업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-161">hello currently displayed operation.</span></span>|  
|<span data-ttu-id="26a27-162">sampleUrl</span><span class="sxs-lookup"><span data-stu-id="26a27-162">sampleUrl</span></span>|<span data-ttu-id="26a27-163">string</span><span class="sxs-lookup"><span data-stu-id="26a27-163">string</span></span>|<span data-ttu-id="26a27-164">hello 현재 작업에 대 한 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-164">hello URL for hello current operation.</span></span>|  
|<span data-ttu-id="26a27-165">operationMenu</span><span class="sxs-lookup"><span data-stu-id="26a27-165">operationMenu</span></span>|[<span data-ttu-id="26a27-166">작업 메뉴</span><span class="sxs-lookup"><span data-stu-id="26a27-166">Operation menu</span></span>](api-management-template-data-model-reference.md#Menu)|<span data-ttu-id="26a27-167">이 API에 대한 작업 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-167">A menu of operations for this API.</span></span>|  
|<span data-ttu-id="26a27-168">consoleUrl</span><span class="sxs-lookup"><span data-stu-id="26a27-168">consoleUrl</span></span>|<span data-ttu-id="26a27-169">URI</span><span class="sxs-lookup"><span data-stu-id="26a27-169">URI</span></span>|<span data-ttu-id="26a27-170">hello에 대 한 URI hello **실습** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-170">hello URI for hello **Try it** button.</span></span>|  
|<span data-ttu-id="26a27-171">샘플</span><span class="sxs-lookup"><span data-stu-id="26a27-171">samples</span></span>|<span data-ttu-id="26a27-172">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-172">Collection of [Code sample](api-management-template-data-model-reference.md#Sample) entities.</span></span>|<span data-ttu-id="26a27-173">hello hello 현재 작업에 대 한 코드 샘플.</span><span class="sxs-lookup"><span data-stu-id="26a27-173">hello code samples for hello current operation..</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="26a27-174">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-174">Sample template data</span></span>  
  
```json  
{  
    "apiId": "570275f1b16653124c8f9ba3",  
    "apiName": "Basic Calculator",  
    "apiDescription": "Arithmetics is just a call away!",  
    "api": {  
        "id": "570275f1b16653124c8f9ba3",  
        "name": "Basic Calculator",  
        "description": "Arithmetics is just a call away!"  
    },  
    "operation": {  
        "id": "570275f2b1665305c811cf49",  
        "name": "Add two integers",  
        "description": "Produces a sum of two numbers.",  
        "scheme": "https",  
        "uriTemplate": "calc/add?a={a}&b={b}",  
        "host": "sdcontoso5.azure-api.net",  
        "httpMethod": "GET",  
        "request": {  
            "description": null,  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": [  
                {  
                    "name": "a",  
                    "description": "First operand. Default value is <code>51</code>.",  
                    "value": "51",  
                    "options": [  
                        "51"  
                    ],  
                    "required": true,  
                    "kind": 1,  
                    "typeName": null  
                },  
                {  
                    "name": "b",  
                    "description": "Second operand. Default value is <code>49</code>.",  
                    "value": "49",  
                    "options": [  
                        "49"  
                    ],  
                    "required": true,  
                    "kind": 1,  
                    "typeName": null  
                }  
            ],  
            "representations": []  
        },  
        "responses": []  
    },  
    "sampleUrl": "https://sdcontoso5.azure-api.net/calc/add?a={a}&b={b}",  
    "operationMenu": {  
        "ApiId": "570275f1b16653124c8f9ba3",  
        "CurrentOperationId": "570275f2b1665305c811cf49",  
        "Action": "Operation",  
        "MenuItems": [  
            {  
                "Id": "570275f2b1665305c811cf49",  
                "Title": "Add two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4c",  
                "Title": "Divide two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4b",  
                "Title": "Multiply two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4a",  
                "Title": "Subtract two integers",  
                "HttpMethod": "GET"  
            }  
        ]  
    },  
    "consoleUrl": "/docs/services/570275f1b16653124c8f9ba3/operations/570275f2b1665305c811cf49/console",  
    "samples": [  
        {  
            "title": "Curl",  
            "snippet": null,  
            "brush": "plain",  
            "template": "DocumentationSamplesCurl",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "C#",  
            "snippet": null,  
            "brush": "csharp",  
            "template": "DocumentationSamplesCsharp",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Java",  
            "snippet": null,  
            "brush": "java",  
            "template": "DocumentationSamplesJava",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "JavaScript",  
            "snippet": null,  
            "brush": "xml",  
            "template": "DocumentationSamplesJs",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "ObjC",  
            "snippet": null,  
            "brush": "objc",  
            "template": "DocumentationSamplesObjc",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "PHP",  
            "snippet": null,  
            "brush": "php",  
            "template": "DocumentationSamplesPhp",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Python",  
            "snippet": null,  
            "brush": "python",  
            "template": "DocumentationSamplesPython",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Ruby",  
            "snippet": null,  
            "brush": "ruby",  
            "template": "DocumentationSamplesRuby",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="26a27-175"><a name="CodeSamples"></a> 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="26a27-175"><a name="CodeSamples"></a> Code samples</span></span>  
 <span data-ttu-id="26a27-176">hello 다음 템플릿을 사용 하면 hello 개별 코드 샘플의 toocustomize hello 본문 hello 작업 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-176">hello following templates allow you toocustomize hello body of hello individual code samples on hello operation page.</span></span>  
  
 <span data-ttu-id="26a27-177">![개발자 포털 템플릿 코드 샘플](./media/api-management-api-templates/APIM-Developer-Portal-Templates-Code-samples.png "APIM 개발자 포털 템플릿 코드 샘플")</span><span class="sxs-lookup"><span data-stu-id="26a27-177">![Developer Portal Templates Code samples](./media/api-management-api-templates/APIM-Developer-Portal-Templates-Code-samples.png "APIM Developer Portal Templates Code samples")</span></span>  
  
-   [<span data-ttu-id="26a27-178">Curl</span><span class="sxs-lookup"><span data-stu-id="26a27-178">Curl</span></span>](#Curl)  
  
-   [<span data-ttu-id="26a27-179">C#</span><span class="sxs-lookup"><span data-stu-id="26a27-179">C#</span></span>](#CSharp)  
  
-   [<span data-ttu-id="26a27-180">Java</span><span class="sxs-lookup"><span data-stu-id="26a27-180">Java</span></span>](#Stub)  
  
-   [<span data-ttu-id="26a27-181">JavaScript</span><span class="sxs-lookup"><span data-stu-id="26a27-181">JavaScript</span></span>](#JavaScript)  
  
-   [<span data-ttu-id="26a27-182">Objective C</span><span class="sxs-lookup"><span data-stu-id="26a27-182">Objective C</span></span>](#ObjectiveC)  
  
-   [<span data-ttu-id="26a27-183">PHP</span><span class="sxs-lookup"><span data-stu-id="26a27-183">PHP</span></span>](#PHP)  
  
-   [<span data-ttu-id="26a27-184">Python</span><span class="sxs-lookup"><span data-stu-id="26a27-184">Python</span></span>](#Python)  
  
-   [<span data-ttu-id="26a27-185">Ruby</span><span class="sxs-lookup"><span data-stu-id="26a27-185">Ruby</span></span>](#Ruby)  
  
###  <span data-ttu-id="26a27-186"><a name="Curl"></a> Curl</span><span class="sxs-lookup"><span data-stu-id="26a27-186"><a name="Curl"></a> Curl</span></span>  
 <span data-ttu-id="26a27-187">hello **DocumentationSamplesCurl** 템플릿을 사용 하 여 코드 hello 작업 페이지의 hello 코드 샘플 섹션에는 샘플 toocustomize 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-187">hello **DocumentationSamplesCurl** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="26a27-188">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-188">Default template</span></span>  
  
```xml  
@ECHO OFF  
  
curl -v -X {{method}} "{{scheme}}://{{host}}{{path}}{{query | escape }}"  
{% for header in headers -%}  
-H "{{ header.name }}: {{ header.value }}"  
{% endfor -%}  
{% if body -%}   
--data-ascii "{{ body | replace:'"','^"' }}"   
{% endif -%}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="26a27-189">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-189">Controls</span></span>  
 <span data-ttu-id="26a27-190">hello 코드 예제 서식 파일 hello 사용 불가 모든 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-190">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="26a27-191">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-191">Data model</span></span>  
 <span data-ttu-id="26a27-192">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-192">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="26a27-193">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-193">Sample template data</span></span>  
  
```json  
{  
    "title": "Curl",  
    "snippet": null,  
    "brush": "plain",  
    "template": "DocumentationSamplesCurl",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="26a27-194"><a name="CSharp"></a> C#</span><span class="sxs-lookup"><span data-stu-id="26a27-194"><a name="CSharp"></a> C#</span></span>  
 <span data-ttu-id="26a27-195">hello **DocumentationSamplesCsharp** 템플릿을 사용 하 여 코드 hello 작업 페이지의 hello 코드 샘플 섹션에는 샘플 toocustomize 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-195">hello **DocumentationSamplesCsharp** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="26a27-196">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-196">Default template</span></span>  
  
```xml  
using System;  
using System.Net.Http.Headers;  
using System.Text;  
using System.Net.Http;  
using System.Web;  
  
namespace CSHttpClientSample  
{  
    static class Program  
    {  
        static void Main()  
        {  
            MakeRequest();  
            Console.WriteLine("Hit ENTER tooexit...");  
            Console.ReadLine();  
        }  
  
        static async void MakeRequest()  
        {  
            var client = new HttpClient();  
            var queryString = HttpUtility.ParseQueryString(string.Empty);  
  
{% if headers.size > 0 -%}  
            // Request headers  
{% for header in headers -%}  
{% case header.Name -%}  
{% when "Accept"%}  
            client.DefaultRequestHeaders.Accept.Add(MediaTypeWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Charset" -%}  
            client.DefaultRequestHeaders.AcceptCharset.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Encoding" -%}  
            client.DefaultRequestHeaders.AcceptEncoding.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Language" -%}  
            client.DefaultRequestHeaders.AcceptLanguage.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Cache-Control" -%}  
            client.DefaultRequestHeaders.CacheControl = CacheControlHeaderValue.Parse("{{header.value}}");  
{% when "Connection" -%}  
            client.DefaultRequestHeaders.Connection.Add("{{header.value}}");  
{% when "Date" -%}  
            client.DefaultRequestHeaders.Date = DateTimeOffset.Parse("{{header.value}}");  
{% when "Expect" -%}  
            client.DefaultRequestHeaders.Expect.Add(NameValueWithParametersHeaderValue.Parse("{{header.value}}"));  
{% when "If-Match" -%}  
            client.DefaultRequestHeaders.IfMatch.Add(EntityTagHeaderValue.Parse("{{header.value}}"));  
{% when "If-Modified-Since" -%}  
            client.DefaultRequestHeaders.IfModifiedSince = DateTimeOffset.Parse("{{header.value}}");  
{% when "If-None-Match" -%}  
            client.DefaultRequestHeaders.IfNoneMatch.Add(EntityTagHeaderValue.Parse("{{header.value}}"));  
{% when "If-Range" -%}  
            client.DefaultRequestHeaders.IfRange = RangeConditionHeaderValue.Parse("{{header.value}}");  
{% when "If-Unmodified-Since" -%}  
            client.DefaultRequestHeaders.IfUnmodifiedSince = DateTimeOffset.Parse("{{header.value}}");  
{% when "Max-Forwards" -%}  
            client.DefaultRequestHeaders.MaxForwards = int.Parse("{{header.value}}");  
{% when "Pragma" -%}  
            client.DefaultRequestHeaders.Pragma.Add(NameValueHeaderValue.Parse("{{header.value}}"));  
{% when "Range" -%}  
            client.DefaultRequestHeaders.Range = RangeHeaderValue.Parse("{{header.value}}");  
{% when "Referer" -%}  
            client.DefaultRequestHeaders.Referrer = new Uri("{{header.value}}");  
{% when "TE" -%}  
            client.DefaultRequestHeaders.TE.Add(TransferCodingWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Transfer-Encoding" -%}  
            client.DefaultRequestHeaders.TransferEncoding.Add(TransferCodingHeaderValue.Parse("{{header.value}}"));  
{% when "Upgrade" -%}  
            client.DefaultRequestHeaders.Upgrade.Add(ProductHeaderValue.Parse("{{header.value}}"));  
{% when "User-Agent" -%}  
            client.DefaultRequestHeaders.UserAgent.Add(ProductInfoHeaderValue.Parse("{{header.value}}"));  
{% when "Via" -%}                
            client.DefaultRequestHeaders.Via.Add(ViaHeaderValue.Parse("{{header.value}}"));  
{% when "Warning" -%}  
            client.DefaultRequestHeaders.Warning.Add(WarningHeaderValue.Parse("{{header.value}}"));  
{% when "Content-Type" -%}  
{% else -%}  
            client.DefaultRequestHeaders.Add("{{header.Name}}", "{{header.value}}");  
{% endcase -%}  
{% endfor -%}  
{% endif -%}  
  
{% if parameters.size > 0 -%}  
            // Request parameters  
{% for parameter in parameters -%}  
            queryString["{{parameter.Name}}"] = "{{parameter.Value}}";  
{% endfor -%}  
{% endif -%}  
            var uri = "{{scheme}}://{{host}}{{path}}{% if path contains '?' %}&{% else %}?{% endif %}" + queryString;  
  
{% case method -%}  
  
{% when "POST" -%}  
            HttpResponseMessage response;  
  
            // Request body  
            byte[] byteData = Encoding.UTF8.GetBytes("{{ body | replace:'"','\"'}}");  
  
            using (var content = new ByteArrayContent(byteData))  
            {  
{% if body -%}  
               content.Headers.ContentType = new MediaTypeHeaderValue("< your content type, i.e. application/json >");  
{% endif -%}  
               response = await client.PostAsync(uri, content);  
            }  
  
{% when "GET" -%}  
            var response = await client.GetAsync(uri);  
{% when "DELETE" -%}  
            var response = await client.DeleteAsync(uri);  
{% when "PUT" -%}  
            HttpResponseMessage response;  
  
            // Request body  
            byte[] byteData = Encoding.UTF8.GetBytes("{{ body | replace:'"','\"'}}");  
  
            using (var content = new ByteArrayContent(byteData))  
            {  
{% if body -%}  
                content.Headers.ContentType = new MediaTypeHeaderValue("< your content type, i.e. application/json >");  
{% endif -%}  
                response = await client.PutAsync(uri, content);  
            }  
{% when "HEAD" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Head, uri));  
{% when "OPTIONS" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Options, uri));  
{% when "TRACE" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Trace, uri));  
  
            if (response.Content != null)  
            {  
                var responseString = await response.Content.ReadAsStringAsync();  
                Console.WriteLine(responseString);      
            }  
{% endcase -%}  
        }  
    }  
}     
```  
  
#### <a name="controls"></a><span data-ttu-id="26a27-197">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-197">Controls</span></span>  
 <span data-ttu-id="26a27-198">hello 코드 예제 서식 파일 hello 사용 불가 모든 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-198">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="26a27-199">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-199">Data model</span></span>  
 <span data-ttu-id="26a27-200">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-200">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="26a27-201">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-201">Sample template data</span></span>  
  
```json  
{  
    "title": "C#",  
    "snippet": null,  
    "brush": "csharp",  
    "template": "DocumentationSamplesCsharp",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="26a27-202"><a name="Stub"></a> Java</span><span class="sxs-lookup"><span data-stu-id="26a27-202"><a name="Stub"></a> Java</span></span>  
 <span data-ttu-id="26a27-203">hello **DocumentationSamplesJava** 템플릿을 사용 하 여 코드 hello 작업 페이지의 hello 코드 샘플 섹션에는 샘플 toocustomize 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-203">hello **DocumentationSamplesJava** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="26a27-204">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-204">Default template</span></span>  
  
```xml  
// // This sample uses hello Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)  
import java.net.URI;  
import org.apache.http.HttpEntity;  
import org.apache.http.HttpResponse;  
import org.apache.http.client.HttpClient;  
import org.apache.http.client.methods.HttpGet;  
import org.apache.http.client.utils.URIBuilder;  
import org.apache.http.impl.client.HttpClients;  
import org.apache.http.util.EntityUtils;  
  
public class JavaSample   
{  
    public static void main(String[] args)   
    {  
        HttpClient httpclient = HttpClients.createDefault();  
  
        try  
        {  
            URIBuilder builder = new URIBuilder("{{scheme}}://{{host}}{{path}}");  
  
{% if parameters.size > 0 -%}  
{% for parameter in parameters -%}  
            builder.setParameter("{{parameter.name}}", "{{parameter.value}}");  
{% endfor -%}  
{% endif -%}  
  
            URI uri = builder.build();  
            Http{{ method | downcase | capitalize }} request = new Http{{ method | downcase | capitalize }}(uri);  
{% for header in headers -%}  
            request.setHeader("{{header.Name}}", "{{header.value}}");  
{% endfor %}  
  
{% if body -%}  
            // Request body  
            StringEntity reqEntity = new StringEntity("{{ body | replace:'"','\"' }}");  
            request.setEntity(reqEntity);  
{% endif -%}  
  
            HttpResponse response = httpclient.execute(request);  
            HttpEntity entity = response.getEntity();  
  
            if (entity != null)   
            {  
                System.out.println(EntityUtils.toString(entity));  
            }  
        }  
        catch (Exception e)  
        {  
            System.out.println(e.getMessage());  
        }  
    }  
}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="26a27-205">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-205">Controls</span></span>  
 <span data-ttu-id="26a27-206">hello 코드 예제 서식 파일 hello 사용 불가 모든 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-206">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="26a27-207">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-207">Data model</span></span>  
 <span data-ttu-id="26a27-208">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-208">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="26a27-209">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-209">Sample template data</span></span>  
  
```json  
{  
    "title": "Java",  
    "snippet": null,  
    "brush": "java",  
    "template": "DocumentationSamplesJava",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="26a27-210"><a name="JavaScript"></a> JavaScript</span><span class="sxs-lookup"><span data-stu-id="26a27-210"><a name="JavaScript"></a> JavaScript</span></span>  
 <span data-ttu-id="26a27-211">hello **DocumentationSamplesJs** 템플릿을 사용 하 여 코드 hello 작업 페이지의 hello 코드 샘플 섹션에는 샘플 toocustomize 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-211">hello **DocumentationSamplesJs** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="26a27-212">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-212">Default template</span></span>  
  
```xml  
<!DOCTYPE html>  
<html>  
<head>  
    <title>JSSample</title>  
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>  
</head>  
<body>  
  
<script type="text/javascript">  
    $(function() {  
        var params = {  
{% if parameters.size > 0 -%}  
            // Request parameters  
{% for parameter in parameters -%}  
            "{{parameter.name}}": "{{parameter.value}}",  
{% endfor -%}  
{% endif -%}  
        };  
  
        $.ajax({  
            url: "{{scheme}}://{{host}}{{path}}{% if path contains '?' %}&{% else %}?{% endif %}" + $.param(params),  
{% if headers.size > 0 -%}  
            beforeSend: function(xhrObj){  
                // Request headers  
{% for header in headers -%}  
                xhrObj.setRequestHeader("{{header.name}}","{{header.value}}");  
{% endfor -%}  
            },  
{% endif -%}  
            type: "{{method}}",  
{% if body -%}  
            // Request body  
            data: "{{ body | replace:'"','\"' }}",  
{% endif -%}  
        })  
        .done(function(data) {  
            alert("success");  
        })  
        .fail(function() {  
            alert("error");  
        });  
    });  
</script>  
</body>  
</html>  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="26a27-213">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-213">Controls</span></span>  
 <span data-ttu-id="26a27-214">hello 코드 예제 서식 파일 hello 사용 불가 모든 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-214">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="26a27-215">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-215">Data model</span></span>  
 <span data-ttu-id="26a27-216">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-216">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="26a27-217">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-217">Sample template data</span></span>  
  
```json  
{  
    "title": "JavaScript",  
    "snippet": null,  
    "brush": "xml",  
    "template": "DocumentationSamplesJs",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="26a27-218"><a name="ObjectiveC"></a> Objective C</span><span class="sxs-lookup"><span data-stu-id="26a27-218"><a name="ObjectiveC"></a> Objective C</span></span>  
 <span data-ttu-id="26a27-219">hello **DocumentationSamplesObjc** 템플릿을 사용 하 여 코드 hello 작업 페이지의 hello 코드 샘플 섹션에는 샘플 toocustomize 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-219">hello **DocumentationSamplesObjc** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="26a27-220">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-220">Default template</span></span>  
  
```xml  
#import <Foundation/Foundation.h>  
  
int main(int argc, const char * argv[])  
{  
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];  
  
    NSString* path = @"{{scheme}}://{{host}}{{path}}";  
    NSArray* array = @[  
                         // Request parameters  
                         @"entities=true",  
{% if parameters.size > 0 -%}  
{% for parameter in parameters -%}  
                         @"{{parameter.name}}={{parameter.value}}",  
{% endfor -%}  
{% endif -%}  
                      ];  
  
    NSString* string = [array componentsJoinedByString:@"&"];  
    path = [path stringByAppendingFormat:@"?%@", string];  
  
    NSLog(@"%@", path);  
  
    NSMutableURLRequest* _request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:path]];  
    [_request setHTTPMethod:@"{{method}}"];  
{% if headers.size > 0 -%}  
    // Request headers  
{% for header in headers -%}  
    [_request setValue:@"{{header.value}}" forHTTPHeaderField:@"{{header.name}}"];  
{% endfor -%}  
{% endif -%}  
{% if body -%}  
    // Request body  
    [_request setHTTPBody:[@"{{ body | replace:'"','\"' }}" dataUsingEncoding:NSUTF8StringEncoding]];  
{% endif -%}  
  
    NSURLResponse *response = nil;  
    NSError *error = nil;  
    NSData* _connectionData = [NSURLConnection sendSynchronousRequest:_request returningResponse:&response error:&error];  
  
    if (nil != error)  
    {  
        NSLog(@"Error: %@", error);  
    }  
    else  
    {  
        NSError* error = nil;  
        NSMutableDictionary* json = nil;  
        NSString* dataString = [[NSString alloc] initWithData:_connectionData encoding:NSUTF8StringEncoding];  
        NSLog(@"%@", dataString);  
  
        if (nil != _connectionData)  
        {  
            json = [NSJSONSerialization JSONObjectWithData:_connectionData options:NSJSONReadingMutableContainers error:&error];  
        }  
  
        if (error || !json)  
        {  
            NSLog(@"Could not parse loaded json with error:%@", error);  
        }  
  
        NSLog(@"%@", json);  
        _connectionData = nil;  
    }  
  
    [pool drain];  
  
    return 0;  
}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="26a27-221">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-221">Controls</span></span>  
 <span data-ttu-id="26a27-222">hello 코드 예제 서식 파일 hello 사용 불가 모든 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-222">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="26a27-223">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-223">Data model</span></span>  
 <span data-ttu-id="26a27-224">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-224">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="26a27-225">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-225">Sample template data</span></span>  
  
```json  
{  
    "title": "ObjC",  
    "snippet": null,  
    "brush": "objc",  
    "template": "DocumentationSamplesObjc",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="26a27-226"><a name="PHP"></a> PHP</span><span class="sxs-lookup"><span data-stu-id="26a27-226"><a name="PHP"></a> PHP</span></span>  
 <span data-ttu-id="26a27-227">hello **DocumentationSamplesPhp** 템플릿을 사용 하 여 코드 hello 작업 페이지의 hello 코드 샘플 섹션에는 샘플 toocustomize 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-227">hello **DocumentationSamplesPhp** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="26a27-228">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-228">Default template</span></span>  
  
```xml  
<?php  
// This sample uses hello Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)  
require_once 'HTTP/Request2.php';  
  
$request = new Http_Request2('{{scheme}}://{{host}}{{path}}');  
$url = $request->getUrl();  
  
{% if headers.size > 0 -%}  
$headers = array(  
    // Request headers  
{% for header in headers -%}  
    '{{header.name}}' => '{{header.value}}',  
{% endfor -%}  
);  
  
$request->setHeader($headers);  
{% endif -%}  
  
{% if parameters.size > 0 -%}  
$parameters = array(  
    // Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}' => '{{parameter.value}}',  
{% endfor -%}  
);  
  
$url->setQueryVariables($parameters);  
{% endif -%}  
  
$request->setMethod(HTTP_Request2::METHOD_{{method}});  
  
{% if body -%}  
// Request body  
$request->setBody("{{ body | replace:'"','\"' }}");  
{% endif -%}  
  
try  
{  
    $response = $request->send();  
    echo $response->getBody();  
}  
catch (HttpException $ex)  
{  
    echo $ex;  
}  
  
?>  
```  
  
#### <a name="controls"></a><span data-ttu-id="26a27-229">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-229">Controls</span></span>  
 <span data-ttu-id="26a27-230">hello 코드 예제 서식 파일 hello 사용 불가 모든 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-230">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="26a27-231">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-231">Data model</span></span>  
 <span data-ttu-id="26a27-232">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-232">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="26a27-233">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-233">Sample template data</span></span>  
  
```json  
{  
    "title": "PHP",  
    "snippet": null,  
    "brush": "php",  
    "template": "DocumentationSamplesPhp",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="26a27-234"><a name="Python"></a> Python</span><span class="sxs-lookup"><span data-stu-id="26a27-234"><a name="Python"></a> Python</span></span>  
 <span data-ttu-id="26a27-235">hello **DocumentationSamplesPython** 템플릿을 사용 하 여 코드 hello 작업 페이지의 hello 코드 샘플 섹션에는 샘플 toocustomize 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-235">hello **DocumentationSamplesPython** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="26a27-236">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-236">Default template</span></span>  
  
```xml  
########### Python 2.7 #############  
import httplib, urllib, base64  
  
headers = {  
{% if headers.size > 0 -%}  
    # Request headers  
{% for header in headers -%}  
    '{{header.name}}': '{{header.value}}',  
{% endfor -%}  
{% endif -%}  
}  
  
params = urllib.urlencode({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}': '{{parameter.value}}',  
{% endfor -%}  
{% endif -%}  
})  
  
try:  
{% case scheme -%}  
{% when "http" -%}  
    conn = httplib.HTTPConnection('{{host}}')  
{% when "https" -%}  
    conn = httplib.HTTPSConnection('{{host}}')  
{% endcase -%}  
    conn.request("{{method}}", "{{path}}{% if path contains '?' %}&{% else %}?{% endif %}%s" % params{% if body %}, "{{ body | replace:'"','\"' }}"{% endif %}, headers)  
    response = conn.getresponse()  
    data = response.read()  
    print(data)  
    conn.close()  
except Exception as e:  
    print("[Errno {0}] {1}".format(e.errno, e.strerror))  
  
####################################  
  
########### Python 3.2 #############  
import http.client, urllib.request, urllib.parse, urllib.error, base64  
  
headers = {  
{% if headers.size > 0 -%}  
    # Request headers  
{% for header in headers -%}  
    '{{header.name}}': '{{header.value}}',  
{% endfor -%}  
{% endif -%}  
}  
  
params = urllib.parse.urlencode({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}': '{{parameter.value}}',  
{% endfor -%}  
{% endif -%}  
})  
  
try:  
{% case scheme -%}  
{% when "http" -%}  
    conn = http.client.HTTPConnection('{{host}}')  
{% when "https" -%}  
    conn = http.client.HTTPSConnection('{{host}}')  
{% endcase -%}  
    conn.request("{{method}}", "{{path}}{% if path contains '?' %}&{% else %}?{% endif %}%s" % params{% if body %}, "{{ body | replace:'"','\"' }}"{% endif %}, headers)  
    response = conn.getresponse()  
    data = response.read()  
    print(data)  
    conn.close()  
except Exception as e:  
    print("[Errno {0}] {1}".format(e.errno, e.strerror))  
  
####################################  
```  
  
#### <a name="controls"></a><span data-ttu-id="26a27-237">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-237">Controls</span></span>  
 <span data-ttu-id="26a27-238">hello 코드 예제 서식 파일 hello 사용 불가 모든 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-238">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="26a27-239">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-239">Data model</span></span>  
 <span data-ttu-id="26a27-240">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-240">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="26a27-241">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-241">Sample template data</span></span>  
  
```json  
{  
    "title": "Python",  
    "snippet": null,  
    "brush": "python",  
    "template": "DocumentationSamplesPython",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="26a27-242"><a name="Ruby"></a> Ruby</span><span class="sxs-lookup"><span data-stu-id="26a27-242"><a name="Ruby"></a> Ruby</span></span>  
 <span data-ttu-id="26a27-243">hello **DocumentationSamplesRuby** 템플릿을 사용 하 여 코드 hello 작업 페이지의 hello 코드 샘플 섹션에는 샘플 toocustomize 합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-243">hello **DocumentationSamplesRuby** template allows you toocustomize that code sample in hello code samples section of hello operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="26a27-244">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="26a27-244">Default template</span></span>  
  
```xml  
require 'net/http'  
  
uri = URI('{{scheme}}://{{host}}{{path}}')  
uri.query = URI.encode_www_form({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}' => '{{parameter.value}}'{% unless forloop.last %},{% endunless %}  
{% endfor -%}  
{% endif -%}  
})  
  
request = Net::HTTP::{{ method | downcase | capitalize }}.new(uri.request_uri)  
{% for header in headers -%}  
# Request headers  
request['{{header.name}}'] = '{{header.value}}'  
{% endfor -%}  
{% if body -%}  
# Request body  
request.body = "{{ body | replace:'"','\"' }}"  
{% endif -%}  
  
response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|  
    http.request(request)  
end  
  
puts response.body  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="26a27-245">컨트롤</span><span class="sxs-lookup"><span data-stu-id="26a27-245">Controls</span></span>  
 <span data-ttu-id="26a27-246">hello 코드 예제 서식 파일 hello 사용 불가 모든 [컨트롤 페이지](api-management-page-controls.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-246">hello code sample templates do not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="26a27-247">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="26a27-247">Data model</span></span>  
 <span data-ttu-id="26a27-248">[코드 샘플](api-management-template-data-model-reference.md#Sample) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-248">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="26a27-249">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="26a27-249">Sample template data</span></span>  
  
```json  
{  
    "title": "Ruby",  
    "snippet": null,  
    "brush": "ruby",  
    "template": "DocumentationSamplesRuby",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access toothis API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```

## <a name="next-steps"></a><span data-ttu-id="26a27-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26a27-250">Next steps</span></span>
<span data-ttu-id="26a27-251">서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="26a27-251">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
