---
title: "aaaGuide toocreating 마켓플레이스 hello에 대 한 데이터 서비스 | Microsoft Docs"
description: "Toocreate, 인증 하 고에 대 한 데이터 서비스를 배포 하는 방법의 자세한 지침은 hello Azure Marketplace에서 구입 합니다."
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
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a>기존 매핑의 예 웹 서비스 tooOData CSDLs 통해
> [!IMPORTANT]
> **현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.** SaaS 비즈니스 응용 프로그램의 경우 원하는 toopublish AppSource에 자세한 정보를 찾을 수 [여기](https://appsource.microsoft.com/partners)합니다. IaaS 응용 프로그램 또는 서비스 개발자 경우는 Azure 마켓플레이스에서 toopublish 같은 자세한 정보를 찾을 수 [여기](https://azure.microsoft.com/marketplace/programs/certified/)합니다.
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a>예: "POST"를 사용하여 반환된 "원시" 데이터에 대한 FunctionImport
새 하위 POST 원시 데이터 toocreate를 사용 하 고 해당 서버 URL(location) 또는 tooupdate hello hello 서버에서 하위 부분에서는 정의한 URL을 반환 합니다.  여기서 hello 하위 항목은 스트림, ex, 즉 구조화 되지 않은입니다. 텍스트 파일입니다.  POST는 위치 없는 idempotent가 아닙니다.

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

## <a name="example-functionimport-using-delete"></a>예: "DELETE"를 사용하는 FunctionImport
DELETE tooremove 지정된 된 URI를 사용 합니다.

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

## <a name="example-functionimport-using-post"></a>예: "POST"를 사용하는 FunctionImport
새 하위 POST 원시 데이터 toocreate를 사용 하 고 해당 서버 URL(location) 또는 tooupdate hello hello 서버에서 하위 부분에서는 정의한 URL을 반환 합니다.  여기서 hello 하위 구조입니다. POST는 위치 없는 idempotent가 아닙니다.

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

## <a name="example-functionimport-using-put"></a>예: "PUT"을 사용하는 FunctionImport
새 하위 toocreate PUT을 사용 하 여 또는 tooupdate hello 전체 하위 수준 서버에서 URL을 정의 합니다.  PUT 없으므로 여러 번 실행 발생 hello 동일 idempotent은 여기서 hello 하위 구조는, 상태, 즉, x = 5.  지정 된 hello의 전체 콘텐츠 hello로 put을 사용 해야 리소스입니다.

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


## <a name="example-functionimport-for-raw-data-returned-using-put"></a>예: "PUT"을 사용하여 반환된 "원시" 데이터에 대한 FunctionImport
정의 된 서버 URL에 넣을 원시 데이터 toocreate 새 하위 또는 tooupdate hello 전체 하위 항목을 사용 합니다.  여기서 hello 하위 항목은 스트림, ex, 즉 구조화 되지 않은입니다. 텍스트 파일입니다.  PUT은 idempotent 방식 이므로 없으므로 여러 번 실행 발생 hello 동일한 상태, 즉, x = 5.  지정 된 hello의 전체 콘텐츠 hello로 put을 사용 해야 리소스입니다.

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


## <a name="example-functionimport-for-raw-data-returned-using-get"></a>예: "GET"을 사용하여 반환된 "원시" 데이터에 대한 FunctionImport
원시 가져올 데이터 tooreturn 구조화 되지 않은 하위 항목 즉, 텍스트를 사용 합니다.

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

## <a name="example-functionimport-for-paging-through-returned-data"></a>예: 반환된 데이터를 통해 "페이징"에 대한 FunctionImport
GET을 사용한 데이터를 통해 RESTful 페이징 구현을 사용합니다.  기본 페이징 데이터의 각 페이지 마다 행을 too100 설정 됩니다.

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

## <a name="see-also"></a>참고 항목
* 이 문서를 읽을 전반적인 OData 매핑 프로세스 및 목적을 이해에서 하려는 경우 hello [데이터 서비스 OData 매핑](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview 정의 구조체 및 지침입니다.
* 학습 및 이해 hello 특정 노드 및 해당 매개 변수의 하려는 경우이 문서를 읽어 보세요. [데이터 서비스 OData 매핑 노드](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) 정의 및 설명을, 예제 및 사례 컨텍스트 사용에 대 한 합니다.
* 이 문서를 참조 데이터 서비스 toohello Azure 마켓플레이스에서 게시에 대 한 경로 지정 하는 tooreturn toohello [데이터 서비스에 대 한 게시 가이드](marketplace-publishing-data-service-creation.md)합니다.

