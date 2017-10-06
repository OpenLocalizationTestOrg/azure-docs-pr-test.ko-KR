---
title: "aaaGuide toocreating 마켓플레이스 hello에 대 한 데이터 서비스 | Microsoft Docs"
description: "Toocreate, 인증 하 고에 대 한 데이터 서비스를 배포 하는 방법의 자세한 지침은 hello Azure Marketplace에서 구입 합니다."
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
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>기존 웹 서비스 tooOData CSDL 통해 매핑
> [!IMPORTANT]
> **현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.** SaaS 비즈니스 응용 프로그램의 경우 원하는 toopublish AppSource에 자세한 정보를 찾을 수 [여기](https://appsource.microsoft.com/partners)합니다. IaaS 응용 프로그램 또는 서비스 개발자 경우는 Azure 마켓플레이스에서 toopublish 같은 자세한 정보를 찾을 수 [여기](https://azure.microsoft.com/marketplace/programs/certified/)합니다.
> 
> 

이 문서에서는 방법에 대 한 개요를 제공 toouse CSDL toomap 기존 서비스 tooan OData 호환 되는 서비스입니다. Toocreate hello 매핑 문서 (CSDL) hello 입력된 서비스 호출 및 hello를 통해 hello 클라이언트 요청을 변환 하는 OData 호환 피드를 통해 (데이터) 다시 toohello 클라이언트를 출력 하는 방법을 설명 합니다. Microsoft Azure 마켓플레이스에서 hello OData 프로토콜을 사용 하 여 서비스 toohello 최종 사용자가 노출 합니다. 콘텐츠 공급자(데이터 소유자)가 노출하는 서비스는 REST, SOAP 등의 다양한 형태로 노출됩니다.

## <a name="what-is-a-csdl-and-its-structure"></a>CSDL이란 무엇이며 어떤 구조로 되어 있나요?
CSDL (개념 스키마 정의 언어)는 어떻게 toodescribe 웹 서비스나 데이터베이스 서비스 공통 XML 스크립트 toohello Azure 마켓플레이스를 정의 하는 사양입니다.

Hello의 간단한 개요 **흐름 요청:**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

hello **데이터 흐름** hello에 반대 방향:

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**그림 1** 클라이언트가 것을 얻는 방법을 데이터 콘텐츠 공급자 (서비스)에서 hello Azure 마켓플레이스를 통해 이동 하 여 다이어그램을 사용 합니다.  hello 콘텐츠 공급자의 서비스 및 클라이언트 요청 hello 간에 데이터 전달 및 hello CSDL hello 매핑/변환을 구성 요소 toohandle hello 요청에서 사용 됩니다.

*그림 1: Azure 마켓플레이스를 통해 클라이언트 toocontent 공급자 에서도 자세한 흐름*

  ![drawing](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

Atom, Atom Pub 및 어떤 hello Azure 마켓플레이스 확장 빌드 시 hello OData 프로토콜에 대 한 배경을 검토 하십시오: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

위 링크 발췌: *"hello hello 개방형 데이터 프로토콜 (이후 참조 tooas OData)의 목적은 데이터 서비스로 노출 되는 리소스에 대 한 스타일 CRUD 작업 (만들기, 읽기, 업데이트 및 삭제)에 대 한 REST 기반 tooprovide 프로토콜입니다. "데이터 서비스"는 하나 이상의 "컬렉션"에서 데이터가 노출되고 각 컬렉션의 "항목"이 0개 이상인 끝점이며, 항목은 형식화된 데이터-값 쌍으로 구성됩니다. OData는 Microsoft에서 게시 OASIS (기구 hello Advancement of Structured 정보 Standards) 표준에서 서버, 클라이언트 또는 로열티 또는 제한 없이 도구를 빌드 toocan를가 하는 모든 사용자에 게 되도록 합니다. "*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Toobe hello CSDL에 정의 된 세 가지 중요 한 부분에는
* hello **끝점** hello 서비스 공급자의 웹 주소 (URI)의 서비스 hello hello
* hello **데이터 매개 변수** toohello 콘텐츠 공급자의 서비스 toohello 데이터 형식 다운 송신할 hello 매개 변수의 hello 정의 입력된 toohello 서비스 공급자 변수로 전달 된입니다.
* **스키마** toohello 서비스 요청 hello 데이터의 스키마 hello hello 콘텐츠 공급자의 서비스에 의해 전달 되 고 반환 되는 hello 데이터의 컨테이너, 컬렉션/테이블, 변수/열 및 데이터 형식을 포함 합니다.

다이어그램을 다음 hello hello 클라이언트가 hello OData 문 (호출 toohello 콘텐츠 공급자의 웹 서비스) toogetting hello 결과/데이터 다시에서 hello 흐름의 개요를 보여 줍니다.

  ![drawing](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>단계:
1. 요청을 보내면 서비스 호출을 통해 완료 되었으나 XML toohello Azure Marketplace에에서 정의 된 입력 매개 변수
2. CSDL은 사용 되는 toovalidate hello 서비스 호출입니다.
   * hello 서식이 지정 된 서비스 호출 toohello 콘텐츠 공급자 서비스 하 여 전송 됩니다 hello Azure 마켓플레이스
3. hello 웹 서비스를 실행 하 고 hello Http 동사의 hello 동작 preforms (즉, GET) tooAzure 마켓플레이스 (있는 경우) hello에서 데이터를 요청 하는 위치는 XML 형식의 toohello 클라이언트에에서 노출 hello 데이터가 반환 됩니다 매핑 hello CSDL에에서 정의 된 hello를 사용 하 여 합니다.
4. 클라이언트 hello hello 데이터 (있는 경우) 형식으로 보내집니다 XML 또는 JSON

## <a name="definitions"></a>정의
### <a name="odata-atom-pub"></a>OData ATOM pub
여기서 각 항목은 결과의 행을 하나는 확장 toohello ATOM pub 설정 합니다. hello 항목의 hello 콘텐츠 부분은 키/값 쌍으로 hello 행 –의 향상 된 toocontain hello 값을입니다. 자세한 내용은 [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL - 개념 스키마 정의 언어
데이터베이스를 통해 노출되는 함수(SPROC) 및 엔터티를 정의할 수 있습니다. 자세한 내용은 [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Hello 클릭 **다른 버전** 드롭다운 hello 문서 표시 되지 않으면 버전을 선택 합니다.
> 
> 

### <a name="edm---entry-data-model"></a>EDM - 항목 데이터 모델
* 개요: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* 미리 보기: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* 데이터 형식: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

hello 다음 hello hello 클라이언트가 hello OData 문 (호출 toohello 콘텐츠 공급자의 웹 서비스) toogetting hello 결과/데이터 다시에서 왼쪽된 tooRight 흐름을 자세히 보여 줍니다.

  ![drawing](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>CSDL 기본 사항
CSDL (개념 스키마 정의 언어)는 어떻게 toodescribe 웹 서비스나 데이터베이스 서비스 공통 XML 스크립트 toohello Azure 마켓플레이스를 정의 하는 사양입니다. CSDL에 설명 하는 중요 한 hello pieces **hello 데이터 소스 toohello Azure Marketplace에서에서 데이터의 hello 전달을 가능 하 게 합니다.** 다음은 hello 주요 작업에 대 한 설명입니다.

* 공개적으로 제공되는 함수(FunctionImport 노드)를 설명하는 인터페이스 정보
* 모든 메시지 요청(입력) 및 메시지 응답(출력)에 대한 데이터 유형 정보(EntityContainer/EntitySet/EntityType 노드)
* (헤더 노드)에 사용 되는 바인딩 전송 프로토콜 toobe hello에 대 한 정보
* Hello를 찾기 위한 주소 정보 서비스 (BaseURI 특성)를 지정 합니다.

간단히 말해서 hello CSDL hello 서비스 요청자와 hello 서비스 공급자 사이의 플랫폼 및 언어 독립적인 계약을 나타냅니다. 클라이언트 수 CSDL hello를 사용 하 여 웹 서비스/데이터베이스 서비스를 찾을 고 공개적으로 사용할 수 있는 기능 중 하나를 호출 합니다.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>컬렉션 또는 CSDL tooa 데이터베이스와 관련 된
**hello CSDL 사양**

CSDL은 웹 서비스를 설명하는 XML 문법입니다. hello 사양 자체는 4 개의 주요 요소가 나뉩니다: EntitySet, FunctionImport; 네임 스페이스 및 EntityType입니다.

toomake이 추상화 쉽게 toounderstand CSDL tooa 테이블 연결 수 있습니다.

기억하세요!

  CSDL hello 간에 플랫폼 및 언어 독립적인 계약을 나타냅니다 **서비스 요청자** 및 hello **서비스 공급자**합니다. **클라이언트**는 CSDL을 사용하여 **웹 서비스/데이터베이스 서비스**를 찾아서 공개적으로 제공되는 모든 **함수**를 호출할 수 있습니다.

데이터 서비스 hello에 대 한 csdl 네 부분 데이터베이스, 테이블, 열 및 저장 프로시저 측면에서 생각할 수 있습니다.

데이터 서비스에 대해 다음과 같이 관련 지을 수 있습니다.

* EntityContainer  ~=  데이터베이스
* EntitySet  ~=  테이블
* EntityType  ~= 열
* FunctionImport  ~=  저장 프로시저

**허용되는 HTTP 동사**

* – Hello db (컬렉션을 반환 합니다.)에서 반환 값 가져오기
* 게시-toopass 데이터 tooand 선택적 반환 값 (반환 id/URI hello 컬렉션에 새 항목 만들기) hello db에서 사용 되는
* Hello DB (컬렉션을 삭제 합니다.)의 데이터를 삭제-삭제
* PUT – DB로 데이터를 업데이트(컬렉션 바꾸기 또는 새로 만들기)

## <a name="metadatamapping-document"></a>메타데이터/매핑 문서
hello 메타 데이터/매핑 문서가 사용 되는 toomap 콘텐츠 공급자의 기존 웹 서비스는 hello Azure 마켓플레이스 시스템에서 OData 웹 서비스로 노출 될 수 있도록 합니다. CSDL을 기반으로 하며 REST의 몇 가지 확장 tooCSDL tooaccommodate hello 요구 Azure Marketplace를 통해 노출 되는 웹 서비스에 따라 구현 합니다. hello 확장 hello에 부여 [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) 네임 스페이스입니다.

Hello CSDL의 예는 다음과 같습니다: (아래 예제에서는 CSDL XML 편집기에 hello 복사 및 붙여넣기 및 toomatch 서비스를 변경 합니다.  그런 다음 붙여 CSDL 매핑 DataService 탭 아래의 hello에서 서비스를 만들 때 [Azure 마켓플레이스에 게시 포털](https://publish.windowsazure.com)).

**조건:** Relating hello CSDL 조건 toohello [게시 포털](https://publish.windowsazure.com) UI (PPUI) 조건입니다.

* "제목" hello PPUI에서에서 관련 tooMyWebOffer 제공
* Hello PPUI의에서 MyCompany 너무 관련**게시자 표시 이름** hello에 [Microsoft 개발자 센터](http://dev.windows.com/registration?accountprogram=azure) UI
* API 관련 tooa 웹 또는 데이터 서비스 (hello PPUI 계획)

**계층:** 회사(콘텐츠 공급자)는 API와 일직선상에 있는 플랜, 즉 서비스가 포함된 제품을 소유합니다.

### <a name="webservice-csdl-example"></a>웹 서비스 CSDL 예
웹 응용 프로그램 (예: C# 응용 프로그램) 끝점을 공개 tooa 서비스 연결

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
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
> Hello 문서에 더 많은 CSDL 웹 서비스 예제를 보려면 [기존 매핑의 예 웹 서비스 tooOData CSDLs 통해](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>DataService CSDL 예
Tooa 서비스를 공개 하는 데이터베이스 테이블 또는 뷰 볼 수 있듯이 끝점 아래 예제에서는 두 개의 기본 데이터에 대 한 Api 기반 API CSDL (테이블 대신 뷰 사용할 수 있음)를 연결 합니다.

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
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

## <a name="see-also"></a>참고 항목
* 학습 및 이해 hello 특정 노드 및 해당 매개 변수의 하려는 경우이 문서를 읽어 보세요. [데이터 서비스 OData 매핑 노드](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) 정의 및 설명을, 예제 및 사례 컨텍스트 사용에 대 한 합니다.
* 예를 검토 하려는 경우이 문서를 읽어 보세요. [데이터 서비스 OData 매핑 예제](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee 샘플 코드와 코드 구문 및 컨텍스트를 이해 합니다.
* 이 문서를 참조 데이터 서비스 toohello Azure 마켓플레이스에서 게시에 대 한 경로 지정 하는 tooreturn toohello [데이터 서비스에 대 한 게시 가이드](marketplace-publishing-data-service-creation.md)합니다.

