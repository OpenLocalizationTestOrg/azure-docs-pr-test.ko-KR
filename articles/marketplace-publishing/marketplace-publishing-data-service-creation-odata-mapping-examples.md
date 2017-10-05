---
title: "Marketplace용 데이터 서비스 만들기 가이드 | Microsoft Docs"
description: "Azure 마켓플레이스에서 구매하기 위한 데이터 서비스를 만들고 인증하고 배포하는 방법에 대한 자세한 지침입니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2ab624941fc385f14b62bb5d743927f157955845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="examples-of-mapping-an-existing-web-service-to-odata-through-csdls"></a><span data-ttu-id="6b2b1-103">CSDL을 통해 기존 웹 서비스를 Odata에 매핑하는 예</span><span class="sxs-lookup"><span data-stu-id="6b2b1-103">Examples of mapping an existing web service to OData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6b2b1-104">**현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="6b2b1-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="6b2b1-105">SaaS 비즈니스 응용 프로그램을 AppSource에 게시하려는 경우 [여기](https://appsource.microsoft.com/partners)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="6b2b1-106">IaaS 응용 프로그램 또는 개발자 서비스를 Azure Marketplace에 게시하려는 경우에는 [여기](https://azure.microsoft.com/marketplace/programs/certified/)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="6b2b1-107">예: "POST"를 사용하여 반환된 "원시" 데이터에 대한 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="6b2b1-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="6b2b1-108">원시 데이터 POST를 사용하여 새 하위를 만들고 해당 서버의 정의된 URL(위치)을 반환하거나 서버의 정의된 URL에서 하위 일부를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-108">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="6b2b1-109">여기서는 하위 항목은 스트림, 즉</span><span class="sxs-lookup"><span data-stu-id="6b2b1-109">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="6b2b1-110">구조화 되지 않은 경우, 예:</span><span class="sxs-lookup"><span data-stu-id="6b2b1-110">unstructured, ex.</span></span> <span data-ttu-id="6b2b1-111">텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-111">a text file.</span></span>  <span data-ttu-id="6b2b1-112">POST는 위치 없는 idempotent가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-112">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="6b2b1-113">예: "DELETE"를 사용하는 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="6b2b1-113">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="6b2b1-114">DELETE를 사용하여 지정된 URI를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-114">Use DELETE to remove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="6b2b1-115">예: "POST"를 사용하는 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="6b2b1-115">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="6b2b1-116">원시 데이터 POST를 사용하여 새 하위를 만들고 해당 서버의 정의된 URL(위치)을 반환하거나 서버의 정의된 URL에서 하위 일부를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-116">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="6b2b1-117">여기서 하위는 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-117">Where the subordinate is a structure.</span></span> <span data-ttu-id="6b2b1-118">POST는 위치 없는 idempotent가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-118">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="6b2b1-119">예: "PUT"을 사용하는 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="6b2b1-119">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="6b2b1-120">PUT을 사용하여 새 하위를 만들거나 서버의 정의된 URL에서 전체 하위를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-120">Use PUT to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="6b2b1-121">PUT 없으므로 동일한 상태를 여러 번 실행 발생 idempotent은 하위 구조가 두 즉,</span><span class="sxs-lookup"><span data-stu-id="6b2b1-121">Where the subordinate is a structure, PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="6b2b1-122">x = 5.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-122">x=5.</span></span>  <span data-ttu-id="6b2b1-123">PUT은 지정된 리소스의 전체 콘텐츠에서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-123">Put should be used with the full content of the specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="6b2b1-124">예: "PUT"을 사용하여 반환된 "원시" 데이터에 대한 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="6b2b1-124">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="6b2b1-125">원시 데이터 PUT을 사용하여 새 하위를 만들거나 서버의 정의된 URL에서 전체 하위를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-125">Use PUT Raw data to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="6b2b1-126">여기서는 하위 항목은 스트림, 즉</span><span class="sxs-lookup"><span data-stu-id="6b2b1-126">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="6b2b1-127">구조화 되지 않은 경우, 예:</span><span class="sxs-lookup"><span data-stu-id="6b2b1-127">unstructured, ex.</span></span> <span data-ttu-id="6b2b1-128">텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-128">a text file.</span></span>  <span data-ttu-id="6b2b1-129">없으므로 동일한 상태를 여러 번 실행 발생 PUT은 idempotent 방식 이므로 즉,</span><span class="sxs-lookup"><span data-stu-id="6b2b1-129">PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="6b2b1-130">x = 5.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-130">x=5.</span></span>  <span data-ttu-id="6b2b1-131">PUT은 지정된 리소스의 전체 콘텐츠에서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-131">Put should be used with the full content of the specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="6b2b1-132">예: "GET"을 사용하여 반환된 "원시" 데이터에 대한 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="6b2b1-132">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="6b2b1-133">원시 데이터 GET을 사용하여 구조화되지 않은 하위, 즉 텍스트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-133">Use GET Raw data to return a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="6b2b1-134">예: 반환된 데이터를 통해 "페이징"에 대한 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="6b2b1-134">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="6b2b1-135">GET을 사용한 데이터를 통해 RESTful 페이징 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-135">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="6b2b1-136">기본 페이징은 데이터 페이지당 100행으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-136">Default paging is set to 100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="6b2b1-137">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6b2b1-137">See Also</span></span>
* <span data-ttu-id="6b2b1-138">전체 OData 매핑 프로세스와 목적을 이해하려는 경우 문서 [데이터 서비스 OData 매핑](marketplace-publishing-data-service-creation-odata-mapping.md) 을 읽고 정의, 구조 및 지침을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-138">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="6b2b1-139">특정 노드 및 해당 매개 변수를 학습하고 이해하려면 문서 [데이터 서비스 OData 매핑 노드](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) 에서 정의 및 설명, 예제, 사용 사례 컨텍스트를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-139">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="6b2b1-140">Azure 마켓플레이스에 데이터 서비스를 게시하기 위한 규정된 경로로 반환하려면 문서 [데이터 서비스 게시 가이드](marketplace-publishing-data-service-creation.md)를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="6b2b1-140">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

