---
title: "Marketplace용 데이터 서비스 만들기 가이드 | Microsoft Docs"
description: "Azure 마켓플레이스에서 구매하기 위한 데이터 서비스를 만들고 인증하고 배포하는 방법에 대한 자세한 지침입니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: a853b4dbd1952ba4ea8ee68ea3ca98f588bb71a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="mapping-an-existing-web-service-to-odata-through-csdl"></a><span data-ttu-id="9e405-103">CSDL을 통해 기존 웹 서비스를 Odata에 매핑</span><span class="sxs-lookup"><span data-stu-id="9e405-103">Mapping an existing web service to OData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9e405-104">**현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="9e405-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="9e405-105">SaaS 비즈니스 응용 프로그램을 AppSource에 게시하려는 경우 [여기](https://appsource.microsoft.com/partners)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="9e405-106">IaaS 응용 프로그램 또는 개발자 서비스를 Azure Marketplace에 게시하려는 경우에는 [여기](https://azure.microsoft.com/marketplace/programs/certified/)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="9e405-107">이 문서에서는 CSDL을 사용하여 기존 서비스를 OData 호환 서비스에 매핑하는 방법에 대한 개요를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-107">This article gives an overview on how to use a CSDL to map an existing service to an OData compatible service.</span></span> <span data-ttu-id="9e405-108">서비스 호출을 통해 클라이언트의 입력 요청을 변환하고 OData 호환 피드를 통해 출력(데이터)을 다시 클라이언트로 변환하는 매핑 문서(CSDL) 작성 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-108">It explains how to create the mapping document (CSDL) that transforms the input request from the client via a service call and the output (data) back to the client via an OData compatible feed.</span></span> <span data-ttu-id="9e405-109">Microsoft의 Azure 마켓플레이스는 OData 프로토콜을 사용하여 최종 사용자에게 서비스를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-109">Microsoft’s Azure Marketplace exposes services to the end-users by using the OData protocol.</span></span> <span data-ttu-id="9e405-110">콘텐츠 공급자(데이터 소유자)가 노출하는 서비스는 REST, SOAP 등의 다양한 형태로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="9e405-111">CSDL이란 무엇이며 어떤 구조로 되어 있나요?</span><span class="sxs-lookup"><span data-stu-id="9e405-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="9e405-112">CSDL(개념 스키마 정의 언어)은 Azure 마켓플레이스에서 통용되는 XML 용어로 웹 서비스 또는 데이터베이스 서비스를 설명하는 방법을 정의하는 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span>

<span data-ttu-id="9e405-113">**요청 흐름**</span><span class="sxs-lookup"><span data-stu-id="9e405-113">Simple overview of the **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="9e405-114">**데이터 흐름** 은 반대 방향:</span><span class="sxs-lookup"><span data-stu-id="9e405-114">The **data flow** is in the opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="9e405-115">**그림 1** 은 클라이언트가 Azure 마켓플레이스를 통해 콘텐츠 공급자(서비스)로부터 데이터를 가져오는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through the Azure Marketplace.</span></span>  <span data-ttu-id="9e405-116">CSDL은 매핑/변환 구성 요소가 콘텐츠 공급자의 서비스와 요청하는 클라이언트 간에 요청을 처리하고 데이터를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-116">The CSDL is used by the Mapping/Transformation component to handle the request and data pass between the content provider’s service(s) and the requesting client.</span></span>

<span data-ttu-id="9e405-117">*그림 1: Azure 마켓플레이스를 통해 요청하는 클라이언트에서 콘텐츠 공급자로의 구체적 흐름*</span><span class="sxs-lookup"><span data-stu-id="9e405-117">*Figure 1: Detailed flow from requesting client to content provider via Azure Marketplace*</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="9e405-119">Azure 마켓플레이스 확장 기능이 빌드되는 Atom, Atom Pub 및 OData 프로토콜에 대한 배경 정보는 [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="9e405-119">For background on Atom, Atom Pub, and the OData protocol upon which the Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="9e405-120">위 링크에서 발췌한 내용: *"개방형 데이터 프로토콜(이하 OData)의 목적은 데이터 서비스로 노출되는 리소스에 대해 CRUD 스타일 작업(만들기, 읽기, 업데이트 및 삭제)을 위한 REST 기반 프로토콜을 제공하는 것입니다. "데이터 서비스"는 하나 이상의 "컬렉션"에서 데이터가 노출되고 각 컬렉션의 "항목"이 0개 이상인 끝점이며, 항목은 형식화된 데이터-값 쌍으로 구성됩니다. 누구든지 로열티나 제한 없이 서버, 클라이언트 또는 도구를 구축할 수 있도록 Microsoft에서 OASIS(Organization for the Advancement of Structured Information Standards) 표준에 따라 OData를 게시합니다."*</span><span class="sxs-lookup"><span data-stu-id="9e405-120">Excerpt from above link: *“The purpose of the Open Data protocol (hereafter referred to as OData) is to provide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for the Advancement of Structured Information Standards) Standards so that anyone that wants to can build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-to-be-defined-by-the-csdl-are"></a><span data-ttu-id="9e405-121">CSDL에서 정의해야 하는 세 가지 중요한 것</span><span class="sxs-lookup"><span data-stu-id="9e405-121">Three Critical Pieces that have to be defined by the CSDL are:</span></span>
* <span data-ttu-id="9e405-122">서비스 공급자의 **끝점** 서비스의 웹 주소(URI)</span><span class="sxs-lookup"><span data-stu-id="9e405-122">The **endpoint** of the Service Provider The Web Address (URI) of the Service</span></span>
* <span data-ttu-id="9e405-123">서비스 공급자에 입력으로 전달되는 **데이터 매개 변수** 콘텐츠 공급자의 서비스에서 데이터 유형까지 전달되는 매개 변수 정의</span><span class="sxs-lookup"><span data-stu-id="9e405-123">The **data parameters** being passed as input to the Service Provider The definitions of the parameters being sent to the Content Provider’s service down to the data type.</span></span>
* <span data-ttu-id="9e405-124">요청하는 서비스로 반환되는 **스키마** 컨테이너, 컬렉션/테이블, 변수/열, 데이터 유형을 포함하여 콘텐츠 공급자의 서비스를 통해 전달되는 데이터의 스키마.</span><span class="sxs-lookup"><span data-stu-id="9e405-124">**Schema** of the data being returned to the Requesting Service The schema of the data being delivered by the Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="9e405-125">다음 다이어그램은 클라이언트가 OData 문(콘텐츠 공급자의 웹 서비스 호출)을 입력하고 결과/데이터를 받는 흐름을 개략적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-125">The following diagram shows an overview of the flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back.</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="9e405-127">단계:</span><span class="sxs-lookup"><span data-stu-id="9e405-127">Steps:</span></span>
1. <span data-ttu-id="9e405-128">입력 매개 변수가 XML로 정의되어 있는 서비스 호출을 통해 클라이언트가 Azure 마켓플레이스로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-128">Client sends request via Service call complete with Input Parameters defined in XML to the Azure Marketplace</span></span>
2. <span data-ttu-id="9e405-129">CSDL을 사용하여 서비스 호출의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-129">CSDL is used to validate the Service call.</span></span>
   * <span data-ttu-id="9e405-130">그런 다음 형식이 지정된 서비스 호출이 Azure 마켓플레이스를 통해 콘텐츠 공급자 서비스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-130">The Formatted Service Call is then sent to the Content Providers Service by the Azure Marketplace</span></span>
3. <span data-ttu-id="9e405-131">웹 서비스에서 Http 동사(즉, GET)를 실행 및 수행합니다. 데이터가 Azure 마켓플레이스로 반환되고 요청된 데이터(있는 경우)는 CSDL에 정의된 매핑을 사용하여 클라이언트에 XML 형식으로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-131">The Webservice executes and preforms the action of the Http Verb (i.e. GET) The data is returned to Azure Marketplace where the requested data (if any) is exposes in XML Format to the Client using the Mapping defined in the CSDL.</span></span>
4. <span data-ttu-id="9e405-132">클라이언트에서 데이터(있는 경우)를 XML 또는 JSON 형식으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-132">The Client is sent the data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="9e405-133">정의</span><span class="sxs-lookup"><span data-stu-id="9e405-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="9e405-134">OData ATOM pub</span><span class="sxs-lookup"><span data-stu-id="9e405-134">OData ATOM pub</span></span>
<span data-ttu-id="9e405-135">ATOM pub의 확장 기능으로, 각 항목이 결과 집합의 한 행을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-135">An extension to the ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="9e405-136">항목의 콘텐츠 부분은 키 값 쌍으로 행 값을 포함하도록 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-136">The content part of the entry is enhanced to contain the values of the row – as key value pairs.</span></span> <span data-ttu-id="9e405-137">자세한 내용은 [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="9e405-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="9e405-138">CSDL - 개념 스키마 정의 언어</span><span class="sxs-lookup"><span data-stu-id="9e405-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="9e405-139">데이터베이스를 통해 노출되는 함수(SPROC) 및 엔터티를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="9e405-140">자세한 내용은 [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="9e405-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="9e405-141">문서가 보이지 않으면 **다른 버전** 드롭다운을 클릭하고 다른 버전을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="9e405-141">Click the **other versions** dropdown and select a version if you don’t see the article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="9e405-142">EDM - 항목 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="9e405-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="9e405-143">개요: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="9e405-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="9e405-144">미리 보기: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="9e405-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="9e405-145">데이터 형식: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="9e405-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="9e405-146">다음은 클라이언트가 OData 문(콘텐츠 공급자의 웹 서비스 호출)을 입력하고 결과/데이터를 받는 순차적 흐름을 자세히 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-146">The following shows the detailed Left to Right flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back:</span></span>

  ![그리기](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="9e405-148">CSDL 기본 사항</span><span class="sxs-lookup"><span data-stu-id="9e405-148">CSDL Basics</span></span>
<span data-ttu-id="9e405-149">CSDL(개념 스키마 정의 언어)은 Azure 마켓플레이스에서 통용되는 XML 용어로 웹 서비스 또는 데이터베이스 서비스를 설명하는 방법을 정의하는 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span> <span data-ttu-id="9e405-150">CSDL은 **데이터 원본에서 Azure Marketplace로의 데이터 전송을 가능하게 하는** 중요한 부분을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-150">CSDL describes the critical pieces that **makes the passing of data from the Data Source to the Azure Marketplace possible.**</span></span> <span data-ttu-id="9e405-151">중요한 부분은 여기에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-151">The main pieces are described here:</span></span>

* <span data-ttu-id="9e405-152">공개적으로 제공되는 함수(FunctionImport 노드)를 설명하는 인터페이스 정보</span><span class="sxs-lookup"><span data-stu-id="9e405-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="9e405-153">모든 메시지 요청(입력) 및 메시지 응답(출력)에 대한 데이터 유형 정보(EntityContainer/EntitySet/EntityType 노드)</span><span class="sxs-lookup"><span data-stu-id="9e405-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="9e405-154">사용할 전송 프로토콜에 대한 바인딩 정보(헤더 노드)</span><span class="sxs-lookup"><span data-stu-id="9e405-154">Binding information about the transport protocol to be used (Header Node)</span></span>
* <span data-ttu-id="9e405-155">지정된 서비스를 찾기 위한 주소 정보(BaseURI 특성)</span><span class="sxs-lookup"><span data-stu-id="9e405-155">Address information for locating the specified service (BaseURI attribute)</span></span>

<span data-ttu-id="9e405-156">간단히 말해서 CSDL은 서비스 요청자와 서비스 공급자 간에 이루어지는 플랫폼 및 언어에 독립적인 계약을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-156">In a nutshell, the CSDL represents a platform- and language-independent contract between the service requestor and the service provider.</span></span> <span data-ttu-id="9e405-157">클라이언트는 CSDL을 사용하여 웹 서비스/데이터베이스 서비스를 찾아서 공개적으로 제공되는 모든 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-157">Using the CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-to-a-database-or-a-collection"></a><span data-ttu-id="9e405-158">CSDL과 데이터베이스 또는 컬렉션 사이에 관계 설정</span><span class="sxs-lookup"><span data-stu-id="9e405-158">Relating a CSDL to a Database or a Collection</span></span>
<span data-ttu-id="9e405-159">**CSDL 사양**</span><span class="sxs-lookup"><span data-stu-id="9e405-159">**The CSDL Specification**</span></span>

<span data-ttu-id="9e405-160">CSDL은 웹 서비스를 설명하는 XML 문법입니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="9e405-161">사양 자체는 EntitySet, FunctionImport, NameSpace 및 EntityType의 4개 주요 요소로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-161">The specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="9e405-162">이 추상화를 보다 쉽게 이해하기 위해 CSDL과 테이블 사이에 관계를 설정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-162">To make this abstraction easier to understand lets relate a CSDL to a table.</span></span>

<span data-ttu-id="9e405-163">기억하세요!</span><span class="sxs-lookup"><span data-stu-id="9e405-163">Remember;</span></span>

  <span data-ttu-id="9e405-164">CSDL은 **서비스 요청자**와 **서비스 공급자** 간에 이루어지는 플랫폼 및 언어에 독립적인 계약을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-164">CSDL represents a platform- and language-independent contract between the **service requestor** and the **service provider**.</span></span> <span data-ttu-id="9e405-165">**클라이언트**는 CSDL을 사용하여 **웹 서비스/데이터베이스 서비스**를 찾아서 공개적으로 제공되는 모든 **함수**를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="9e405-166">데이터 서비스의 경우 데이터베이스, 테이블, 열 및 저장 프로시저의 관점에서 CSDL의 네 부분을 생각해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-166">For a Data Service the four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="9e405-167">데이터 서비스에 대해 다음과 같이 관련 지을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="9e405-168">EntityContainer  ~=  데이터베이스</span><span class="sxs-lookup"><span data-stu-id="9e405-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="9e405-169">EntitySet  ~=  테이블</span><span class="sxs-lookup"><span data-stu-id="9e405-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="9e405-170">EntityType  ~= 열</span><span class="sxs-lookup"><span data-stu-id="9e405-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="9e405-171">FunctionImport  ~=  저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="9e405-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="9e405-172">**허용되는 HTTP 동사**</span><span class="sxs-lookup"><span data-stu-id="9e405-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="9e405-173">GET – db의 값 반환(컬렉션 반환)</span><span class="sxs-lookup"><span data-stu-id="9e405-173">GET – returns values from the db (returns a Collection)</span></span>
* <span data-ttu-id="9e405-174">POST – db에 데이터를 전달하고 db에서 선택적으로 값을 반환하는 데 사용(컬렉션에 새 항목 만들기, id/URI 반환)</span><span class="sxs-lookup"><span data-stu-id="9e405-174">POST – used to pass data to and optional return values from the db (Create a new entry in the collection, return id/URI)</span></span>
* <span data-ttu-id="9e405-175">DELETE – DB에서 데이터 삭제(컬렉션 삭제)</span><span class="sxs-lookup"><span data-stu-id="9e405-175">DELETE – Deletes data from the DB (Deletes a collection)</span></span>
* <span data-ttu-id="9e405-176">PUT – DB로 데이터를 업데이트(컬렉션 바꾸기 또는 새로 만들기)</span><span class="sxs-lookup"><span data-stu-id="9e405-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="9e405-177">메타데이터/매핑 문서</span><span class="sxs-lookup"><span data-stu-id="9e405-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="9e405-178">메타데이터/매핑 문서는 Azure 마켓플레이스 시스템에서 웹 서비스를 OData 웹 서비스로 노출할 수 있도록 콘텐츠 공급자의 기존 웹 서비스를 매핑하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-178">The metadata/mapping document is used to map a content provider’s existing web services so that it can be exposed as an OData web service by the Azure Marketplace system.</span></span> <span data-ttu-id="9e405-179">CSDL을 기반으로 하며 Azure 마켓플레이스를 통해 노출되는 웹 서비스 기반의 REST를 수용할 수 있도록 CSDL에 몇 가지 확장 기능을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-179">It is based on CSDL and implements a few extensions to CSDL to accommodate the needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="9e405-180">확장 기능은 [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) 네임스페이스에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-180">The extensions are found in the [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="9e405-181">CSDL의 예는 다음과 같습니다. (아래의 예제 CSDL을 복사하여 XML 편집기에 붙여넣고 해당 서비스와 일치하도록 변경하세요.</span><span class="sxs-lookup"><span data-stu-id="9e405-181">An example of the CSDL follows:  (Copy and paste the below example CSDL into an XML editor and change to match your Service.</span></span>  <span data-ttu-id="9e405-182">그런 다음 [Azure Marketplace 게시 포털](https://publish.windowsazure.com)에서 서비스를 만들 때 DataService 탭 아래에 CSDL 매핑을 붙여넣으세요).</span><span class="sxs-lookup"><span data-stu-id="9e405-182">Then paste into CSDL Mapping under DataService tab when creating your service in the  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="9e405-183">**용어:** CSDL 용어와 PPUI( [게시 포털](https://publish.windowsazure.com) UI) 용어 간의 관련성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-183">**Terms:** Relating the CSDL terms to the [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="9e405-184">PPUI의 제품 "Title"은 MyWebOffer와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-184">Offer “Title” in the PPUI relates to MyWebOffer</span></span>
* <span data-ttu-id="9e405-185">PPUI의 MyCompany는 **Microsoft 개발자 센터** UI의 [게시자 표시 이름](http://dev.windows.com/registration?accountprogram=azure) 과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-185">MyCompany in the PPUI relates to **Publisher Display Name** in the [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="9e405-186">API는 웹 또는 데이터 서비스(PPUI의 계획)와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-186">Your API relates to a Web or Data Service (a Plan in the PPUI)</span></span>

<span data-ttu-id="9e405-187">**계층:** 회사(콘텐츠 공급자)는 API와 일직선상에 있는 플랜, 즉 서비스가 포함된 제품을 소유합니다.</span><span class="sxs-lookup"><span data-stu-id="9e405-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="9e405-188">웹 서비스 CSDL 예</span><span class="sxs-lookup"><span data-stu-id="9e405-188">WebService CSDL Example</span></span>
<span data-ttu-id="9e405-189">웹 응용 프로그램 끝점(예: C# 응용 프로그램)을 노출하는 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="9e405-189">Connects to a service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all the web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition near the bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is the entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines the service call, replace & with the encode value (&amp;).
        In the input name value pairs {param} represents passed in value.
        Or the value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows the CSDL to specifically specify the verb of the service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes the parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how the web service call is exposed to marketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, the {...} point to the parameters defined below.
        Marketplace will read the parameters from this URITemplate and fill the values into the corresponding parameters of the BaseUri or RequestBody (below) during calls to your service.  
        It is okay for @d:BaseUri to include information only for Marketplace consumption, it will not be exposed to end users. i.e. the hardcoded AccountKey in the above BaseURI does not show up in the client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of the RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders to insert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how to pass userid and password via the header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed to end users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with the value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited to appearing as the value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used to specify values to insert into the ATOM feed returned to the end user.  You can specify the element to contain a fixed message by providing a value for the element (this is the default value).  @d:Map is an XPath expression that points into the response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay to also add a d:Map attribute to override this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of the web service call:
        @Name should match exactly (case sensitive) the {…} placeholders in the @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether the parameter is required.
        @d:Regex - optional, attribute to describe the string, limiting unwanted input at the entry of the system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in the Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating the service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in the order listed.
        @d:Match is an Xpath query on the service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is the error code to return if an response matches the error.
        @d:errorMessage is the user friendly message to return when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect to the service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- The EntityContainer defines the output data schema -->
        </EntityContainer>
        <!-- The EntityType @d:Map defines the repeating node (an XPath query) in the response (output data schema). -->
        <!-- If these nodes are outside a namespace, add the prefix in the xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in the ATOM feed, so comply with the XML element naming restrictions (no spaces or other illegal characters).
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query to point at the location to extract the content from your services response.
        The "." is relative to the repeating node in the EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> <span data-ttu-id="9e405-190">[CSDL을 통해 기존 웹 서비스를 Odata에 매핑하는 예](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="9e405-190">View more CSDL Web Service examples in the article [Examples of mapping an existing web service to OData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="9e405-191">DataService CSDL 예</span><span class="sxs-lookup"><span data-stu-id="9e405-191">DataService CSDL Example</span></span>
<span data-ttu-id="9e405-192">데이터베이스 테이블 또는 보기를 끝점으로 노출하는 서비스에 연결 아래 예는 데이터베이스 기반 API CSDL의 두 API를 보여 줍니다(테이블 대신 보기 사용 가능).</span><span class="sxs-lookup"><span data-stu-id="9e405-192">Connects to a service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all the data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of the EntitySet as a Service
        @Name is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); the table (or view) and columns to be returned by the data service.)
            Map is the schema.tabel or schema.view
            dals.TableName is the table Name
            Name is the name identifier for the EntityType and the Name of the service exposed to the client via the UI.
            dals:IsExposed determines if the table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is the schema name of the table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines the column properties and the output of the service.
            dals:ColumnName is the name of the column in the table /view.
            Type is the emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is the maximum length of the output value
            Name is the name of the Property and is exposed to the client facing UI
            dals:IsReturned is the Boolean that determines if the Service exposes this value to the client.
            IsQueryable is the Boolean that determines if the column can be used in a database query
            (For data Services: To improve Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is the numerical position x in the table or the View, where x is from 1 to the number of columns in the table.
            dals:DatabaseDataType is the data type of the column in the database, i.e. SQL data type dals:IsPrimaryKey indicates if the column is the Primary key in the table/view.  (The columns marked ISPrimaryKey are used in the Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a><span data-ttu-id="9e405-193">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9e405-193">See Also</span></span>
* <span data-ttu-id="9e405-194">특정 노드 및 해당 매개 변수를 학습하고 이해하려면 문서 [데이터 서비스 OData 매핑 노드](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) 에서 정의 및 설명, 예제, 사용 사례 컨텍스트를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="9e405-194">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="9e405-195">예제를 검토하고 싶으면 [데이터 서비스 OData 매핑 예제](marketplace-publishing-data-service-creation-odata-mapping-examples.md) 문서를 통해 샘플 코드를 살펴보고 코드 구문 및 컨텍스트를 이해하세요.</span><span class="sxs-lookup"><span data-stu-id="9e405-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="9e405-196">Azure 마켓플레이스에 데이터 서비스를 게시하기 위한 규정된 경로로 반환하려면 문서 [데이터 서비스 게시 가이드](marketplace-publishing-data-service-creation.md)를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="9e405-196">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

