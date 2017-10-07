---
title: "aaaData 카탈로그 개발자 개념 | Microsoft Docs"
description: "소개 hello 카탈로그 REST API를 통해 노출 된 대로 Azure Data Catalog 개념적 모델의 주요 개념을 toohello 합니다."
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Azure 데이터 카탈로그 개발자 개념
Microsoft **Azure 데이터 카탈로그**는 데이터 원본 검색 및 크라우드소싱 데이터 원본 메타데이터에 대한 기능을 제공하는 완전히 관리되는 클라우드 서비스입니다. 개발자는 REST Api를 통해 hello 서비스를 사용할 수 있습니다. Hello 서비스에서 구현 된 hello 개념을 이해 하는 것이 중요 toosuccessfully와 통합 하는 개발자를 위한 **Azure Data Catalog**합니다.

## <a name="key-concepts"></a>주요 개념
hello **Azure Data Catalog** 개념적 모델은 4 개의 주요 개념을 기반: hello **카탈로그**, **사용자**, **자산**, 및 **주석**합니다.

![개념][1]

*그림 1-Azure 데이터 카탈로그 단순 개념적 모델*

### <a name="catalog"></a>카탈로그
A **카탈로그** 메타 데이터는 조직에서 저장 hello 모든 hello 최상위 컨테이너입니다. Azure 계정당 하나의 **카탈로그**가 허용합니다. 카탈로그는 동 점된 tooan 반드시 Azure 구독 **카탈로그** 계정에서 구독이 여러 개 있더라도 모든 지정 된 Azure 계정에 대해 만들 수 있습니다.

카탈로그에는 **사용자** 및 **자산**이 포함됩니다.

### <a name="users"></a>사용자
사용자가 권한을 tooperform 동작이 될 보안 주체 (hello 카탈로그를 검색, 추가, 편집 또는 제거 항목 등) hello 카탈로그에에서 있습니다.

사용자가 할 수 있는 여러 역할이 있습니다. 역할에 대 한 자세한 내용은 hello 섹션 역할 및 권한 부여를 참조 하십시오.

개별 사용자 및 보안 그룹을 추가할 수 있습니다.

Azure 데이터 카탈로그는 관리를 식별하고 액세스하기 위해 Azure Active Directory를 사용합니다. 각 카탈로그 사용자 hello 계정에 대 한 hello Active Directory의 구성원 이어야 합니다.

### <a name="assets"></a>자산
**카탈로그**에는 데이터 자산이 포함됩니다. **자산** 는 hello 단위 hello 카탈로그에서 관리 하는 세분성입니다.

hello 세분성은 자산의 데이터 원본에 따라 다릅니다. SQL Server 또는 Oracle 데이터베이스에서 자산은 테이블 또는 뷰가 될 수 있습니다. SQL Server Analysis Services에서 자산은 측정값, 차원, 또는 KPI(주요 성능 표시기)가 될 수 있습니다. SQL Server Reporting Services에서 자산은 보고서입니다.

**자산** 는 hello 항목 추가 또는 카탈로그에서 제거 합니다. 결과에서 다시 가져오는의 hello 단위 **검색**합니다.

**자산**은 이름, 위치, 형식과 자산을 자세히 설명하는 주석으로 구성됩니다.

### <a name="annotations"></a>주석
주석은 자산에 대한 메타데이터를 나타내는 항목입니다.

주석의 예는 설명, 태그, 스키마 및 설명서 등입니다. 전체 목록은 hello 에셋 유형 및 주석 유형 hello Asset 개체 모델 섹션에에서 있습니다.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>크라우드소싱 주석 및 사용자 관점(의견의 복합성)
Azure 데이터 카탈로그의 중요 한 측면 hello 시스템에서 메타 데이터의 hello crowdsourcing 지원 방식입니다. 것과 반대로 tooa wiki 방법으로 – 여기서는 하나의 의견 및 hello 마지막 기록자 우선 – hello Azure Data Catalog 모델을 사용 하면 여러 의견 toolive hello 시스템에 병렬입니다.

이 방법은 hello 실제 세계 엔터프라이즈 데이터의 다른 사용자 지정된 된 자산에 다른 큐브 뷰를 가질 수를 반영 합니다.

* 데이터베이스 관리자는 대량 ETL 작업에 대 한 서비스 수준 계약 또는 hello 사용 가능한 처리 창에 대 한 정보를 제공할 수 있습니다.
* Hello 비즈니스 프로세스 toowhich hello 자산에 대 한 내용은 적용 또는 비즈니스 hello hello 분류 tooit 적용할 데이터 관리자가 제공할 수 있습니다.
* 재무 분석가 기 말 보고 작업 하는 동안 hello 데이터 사용 방법에 대 한 정보를 제공할 수 있습니다.

toosupport이이 예제에서는 각 사용자-hello DBA, hello 데이터 관리자 및 hello 분석가 – hello 카탈로그에에서 등록 된 설명 tooa 단일 테이블을 추가할 수 있습니다. 모든 설명 hello 시스템에서 유지 관리 하 고 hello Azure Data Catalog 포털에서 모든 설명 표시 됩니다.

이 패턴 적용된 toomost hello 개체 모델의 hello 항목 이므로 hello JSON 페이로드의 개체 유형은 종종 배열 속성에 대 한 단일을 예상할 수 있습니다.

예를 들어 hello 자산에서 루트는 설명 개체의 배열입니다. hello 배열 속성을 "설명" 라고 합니다. 설명 개체에는 하나의 속성 - 설명이 있습니다. hello 패턴은 hello 사용자가 제공한 hello 값에 대 한 설명 개체를 가져옵니다 형식을 설명 하는 각 사용자 만들어졌는지입니다.

그러면 hello UX toodisplay 조합 hello 하는 방법을 선택할 수 있습니다. 디스플레이 대한 세 가지 다른 패턴이 있습니다.

* hello 가장 간단한 패턴은 "All 표시"입니다. 이 패턴에서는 모든 hello 개체 목록 보기에 표시 됩니다. hello Azure Data Catalog 포털 UX 설명에 대 한이 패턴을 사용합니다.
* 다른 패턴은 "병합"입니다. 이 패턴에서는 여러 사용자가 hello에서 모든 hello 값 중복 제거 된 함께 병합 됩니다. UX hello Azure Data Catalog 포털에서이 패턴의 예는 hello 태그와 전문가 속성입니다.
* 세 번째 패턴은 "마지막 기록자 우선"입니다. 이 패턴에서는 hello 가장 최근의 값에 입력 한 표시 됩니다. friendlyName은 이 패턴의 예입니다.

## <a name="asset-object-model"></a>자산 개체 모델
년 hello 주요 개념 섹션에 추가 하는 대로 hello **Azure Data Catalog** 자산 또는 주석 일 수 있는 항목을 포함 하는 개체 모델입니다. 항목에는 선택 또는 필수가 될 수 있는 속성이 있습니다. 일부 속성 tooall 항목을 적용 합니다. 일부 속성 tooall 자산을 적용 합니다. 일부 속성 toospecific 자산 유형에 적용 됩니다.

### <a name="system-properties"></a>시스템 속성
<table><tr><td><b>속성 이름</b></td><td><b>데이터 형식</b></td><td><b>설명</b></td></tr><tr><td>timestamp</td><td>DateTime</td><td>hello 마지막 시간 hello 항목이 수정 되었습니다. 이 필드는 항목을 삽입 하 고 항목이 업데이트 될 때마다 hello 서버에 의해 생성 됩니다. hello 값이이 속성은 무시 됩니다의 입력 작업을 게시 합니다.</td></tr><tr><td>id</td><td>Uri</td><td>Hello 항목 (읽기 전용)의 절대 url입니다. Hello hello 항목에 대 한 고유한 주소 지정 가능한 URI 이며  hello 값이이 속성은 무시 됩니다의 입력 작업을 게시 합니다.</td></tr><tr><td>type</td><td>문자열</td><td>hello 유형의 hello 자산 (읽기 전용).</td></tr><tr><td>etag</td><td>문자열</td><td>해당 toohello의 문자열 버전 hello 카탈로그의 항목을 업데이트 하는 작업을 수행 하는 경우 낙관적 동시성 제어에 사용할 수 있는 hello 항목입니다. "*" 값은 사용 되는 toomatch 수입니다.</td></tr></table>

### <a name="common-properties"></a>공용 속성
이러한 속성 tooall 루트 자산 형식 및 모든 주석 형식에 적용 됩니다.

<table>
<tr><td><b>속성 이름</b></td><td><b>데이터 형식</b></td><td><b>설명</b></td></tr>
<tr><td>fromSourceSystem</td><td>Boolean</td><td>항목의 데이터가 원본 시스템(예: Sql Server 데이터베이스, Oracle 데이터베이스 또는 사용자가 작성)에서 파생되었는지 여부를 나타냅니다.</td></tr>
</table>

### <a name="common-root-properties"></a>공용 루트 속성
<p>
이러한 속성에는 tooall 루트 자산 형식을 적용 합니다.

<table><tr><td><b>속성 이름</b></td><td><b>데이터 형식</b></td><td><b>설명</b></td></tr><tr><td>name</td><td>문자열</td><td>Hello 데이터 원본 위치 정보에서 파생 된 이름</td></tr><tr><td>dsl</td><td>DataSourceLocation</td><td>고유 하 게 hello 데이터 원본에 설명 하 고 hello 자산에 대 한 hello 식별자 중 하나입니다. (이중 ID 섹션 참조).  hello dsl의 hello 구조 hello 프로토콜에 따라 원본 유형 및 합니다.</td></tr><tr><td>DataSource</td><td>DataSourceInfo</td><td>Hello 자산 유형에 대 한 세부 정보입니다.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>가장 최근에이 자산을 등록 하는 hello 사용자에 설명 합니다.  Hello hello 사용자 (hello upn)에 대 한 고유 id 및 표시 이름 (lastName 및 firstName) 모두 포함합니다.</td></tr><tr><td>containerId</td><td>문자열</td><td>Hello 데이터 원본에 대 한 hello 컨테이너 asset의 id입니다. 이 속성은 hello 컨테이너 형식에 대 한 지원 되지 않습니다.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>일반적인 단일 항목이 아닌 주석 속성
이러한 속성이 적용 tooall 단일 항목이 아닌 주석 유형 (toobe를 사용할 수 있는 주석 자산별 여러).

<table>
<tr><td><b>속성 이름</b></td><td><b>데이터 형식</b></td><td><b>설명</b></td></tr>
<tr><td>key</td><td>문자열</td><td>사용자는 hello 주석 hello 현재 컬렉션에서 고유 하 게 식별 하는 키를 지정 합니다. hello 키 길이 256 자를 초과할 수 없습니다.</td></tr>
</table>

### <a name="root-asset-types"></a>루트 자산 형식
루트 자산 유형은 이러한 형식을 나타내는 hello hello 카탈로그에 등록 될 수 있는 데이터 자산의 다양 한 형식입니다. 각 루트 형식에 대 한 hello 보기에 포함 된 주석 및 자산에 설명 하는 뷰가 있습니다. 뷰 이름은 REST API를 사용 하 여 자산을 게시 하는 경우 {view_name} url 세그먼트를 해당 하는 hello 사용 해야 합니다.

<table><tr><td><b>자산 형식(뷰 이름)</b></td><td><b>추가 속성</b></td><td><b>데이터 형식</b></td><td><b>허용된 주석</b></td><td><b>설명</b></td></tr><tr><td>테이블 ("tables")</td><td></td><td></td><td>설명<p>FriendlyName<p>태그<p>스키마<p>ColumnDescription<p>ColumnTag<p> 전문가<p>미리 보기<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>설명서<p></td><td>테이블은 모든 테이블 형식 데이터를 나타냅니다.  예를 들어 SQL 테이블, SQL 보기, Analysis Services 테이블 형식 테이블, Analysis Services 다차원 차원, Oracle 테이블 등이 포함됩니다.   </td></tr><tr><td>측정값("measures")</td><td></td><td></td><td>설명<p>FriendlyName<p>태그<p>전문가<p>AccessInstruction<p>설명서<p></td><td>이 유형은 Analysis Services 측정값을 나타냅니다.</td></tr><tr><td></td><td>측정값</td><td>열</td><td></td><td>메타 데이터 설명 하는 hello 측정값</td></tr><tr><td></td><td>isCalculated </td><td>Boolean</td><td></td><td>여부 hello 측정값이 계산 되는 경우를 지정 합니다.</td></tr><tr><td></td><td>측정값 그룹</td><td>String</td><td></td><td>측정값에 대한 물리적 컨테이너</td></tr><td>KPI("kpis")</td><td></td><td></td><td>설명<p>FriendlyName<p>태그<p>전문가<p>AccessInstruction<p>설명서</td><td></td></tr><tr><td></td><td>측정값 그룹</td><td>String</td><td></td><td>측정값에 대한 물리적 컨테이너</td></tr><tr><td></td><td>goalExpression</td><td>문자열</td><td></td><td>MDX 숫자 식 또는 hello KPI의 hello 대상 값을 반환 하는 계산 합니다.</td></tr><tr><td></td><td>valueExpression</td><td>문자열</td><td></td><td>Hello hello KPI의 실제 값을 반환 하는 MDX 숫자 식입니다.</td></tr><tr><td></td><td>statusExpression</td><td>문자열</td><td></td><td>MDX 식에에서 지정 된 기간의 KPI hello의 hello 상태를 나타내는입니다.</td></tr><tr><td></td><td>trendExpression</td><td>문자열</td><td></td><td>시간이 지남에 따라 hello KPI의 hello 값을 평가 하는 MDX 식입니다. hello 추세는 특정 비즈니스 컨텍스트에서 유용한 시간 기반 조건 조건은 될 수 있습니다.</td>
<tr><td>보고서("reports")</td><td></td><td></td><td>설명<p>FriendlyName<p>태그<p>전문가<p>AccessInstruction<p>설명서<p></td><td>이 형식은 SQL Server Reporting Services 보고서를 나타냅니다. </td></tr><tr><td></td><td>assetCreatedDate</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>String</td><td></td><td></td></tr><tr><td>컨테이너("containers")</td><td></td><td></td><td>설명<p>FriendlyName<p>태그<p>전문가<p>AccessInstruction<p>설명서<p></td><td>이 형식은 SQL 데이터베이스, Azure Blob 컨테이너 또는 Analysis Services 모델과 같은 다른 자산의 컨테이너를 나타냅니다.</td></tr></table>

### <a name="annotation-types"></a>주석 형식
주석 유형을 hello 카탈로그 내의 tooother 형식을 지정할 수 있는 메타 데이터의 유형을 나타냅니다.

<table>
<tr><td><b>주석 형식(중첩된 뷰 이름)</b></td><td><b>추가 속성</b></td><td><b>데이터 형식</b></td><td><b>설명</b></td></tr>

<tr><td>설명("descriptions")</td><td></td><td></td><td>이 속성은 자산에 대한 설명을 포함합니다. Hello 시스템의 각 사용자가 자신의 설명을 추가할 수 있습니다.  해당 사용자만 hello 설명 개체를 편집할 수 있습니다.  관리자 및 자산 소유자 수 hello 설명 개체를 삭제 되지만 편집할 수 없습니다. hello 시스템 사용자의 설명에 별도로 유지 합니다.  따라서은 배열 (한 각 사용자에 대해 사용자 자신의 지식을 hello 데이터 원본에서 파생 된 정보가 들어 있는 추가 toopossibly에 hello 자산에 대 한 기여 했습니다) 각 자산에 대 한 설명입니다.</td></tr>
<tr><td></td><td>설명</td><td>string</td><td>간단한 설명 (2-3 줄) hello 자산입니다.</td></tr>

<tr><td>태그("tags")</td><td></td><td></td><td>이 속성은 자산에 대한 태그를 정의합니다. Hello 시스템의 각 사용자는 자산에 대 한 여러 태그를 추가할 수 있습니다.  태그 개체를 만든 hello 사용자만 편집할 수 있습니다.  관리자 및 자산 소유자 수 hello 태그 개체를 삭제 되지만 편집할 수 없습니다. hello 시스템 사용자의 태그를 별도로 유지 합니다.  따라서 각 자산에 대한 태그 개체의 배열이 있습니다.</td></tr>
<tr><td></td><td>tag</td><td>string</td><td>태그에 설명 하는 hello 자산입니다.</td></tr>

<tr><td>이름("friendlyName")</td><td></td><td></td><td>이 속성은 자산에 대한 친숙한 이름을 포함합니다. FriendlyName가 단일 주석-하나만 FriendlyName tooan 자산을 추가할 수 있습니다.  FriendlyName 개체를 만든 hello 사용자만 편집할 수 있습니다. Admins 및 자산 소유자 수 hello FriendlyName 개체를 삭제할 수 있지만 편집할 수 없습니다. hello 시스템에 사용자의 이름을 개별적으로 유지 관리합니다.</td></tr>
<tr><td></td><td>friendlyName</td><td>string</td><td>Hello asset의 이름입니다.</td></tr>

<tr><td>스키마("schema")</td><td></td><td></td><td>hello 스키마 hello hello 데이터 구조를 설명합니다.  Hello 특성 (열, 속성, 필드, 등) 이름 목록도 다른 메타 데이터를 형식을 합니다.  이 정보는 모든 hello 데이터 원본에서 파생 됩니다.  스키마는 단일 주석입니다. 자산에 하나의 스키마만을 추가할 수 있습니다.</td></tr>
<tr><td></td><td>열</td><td>Column[]</td><td>열 개체의 배열입니다. Hello 열 hello 데이터 원본에서 파생으로 정보와 함께 설명 합니다.</td></tr>

<tr><td>ColumnDescription("columnDescriptions")</td><td></td><td></td><td>이 속성은 열에 대한 설명을 포함합니다.  Hello 시스템의 각 사용자 (최대 열 마다 하나씩)는 여러 열에 대 한 고유한 설명을 추가할 수 있습니다. ColumnDescription 개체를 만든 hello 사용자만 편집할 수 있습니다.  Admins 및 자산 소유자 수 hello ColumnDescription 개체를 삭제할 수 있지만 편집할 수 없습니다. hello 시스템 이러한 사용자의 열 설명에 별도로 유지 합니다.  없기 때문에 각 자산에 대해 ColumnDescription 개체의 배열 (각 사용자가 자신의 지식을 hello 열에 대 한 기여 했습니다에 대 한 열당 하나씩 또한 정보가 들어 있는 toopossibly hello 데이터 원본에서 파생).  hello ColumnDescription 느슨하게 바인딩된 toohello 스키마 이므로 동기화 되지 않을 수 있습니다. hello ColumnDescription hello 스키마에 존재 하지 않는 열을 설명 될 수 없습니다.  가 toohello 기록기 tookeep 설명 및 스키마를 동기화 합니다.  hello 데이터 소스 열 설명 정보 할 수도 있으며 hello 도구를 실행할 때 발생할 수 있는 ColumnDescription 개체를 추가 합니다.</td></tr>
<tr><td></td><td>columnName</td><td>문자열</td><td>이 설명에는 hello 열의 hello 이름입니다.</td></tr>
<tr><td></td><td>설명</td><td>문자열</td><td>hello 열의 짧은 설명 (2-3 줄).</td></tr>

<tr><td>ColumnTag("columnTags")</td><td></td><td></td><td>이 속성은 열에 대한 태그를 포함합니다. Hello 시스템의 각 사용자 지정된 된 열에 대 한 여러 태그를 추가할 수 하 고 여러 열에 대 한 태그를 추가할 수 있습니다. ColumnTag 개체를 만든 hello 사용자만 편집할 수 있습니다. Admins 및 자산 소유자 수 hello ColumnTag 개체를 삭제할 수 있지만 편집할 수 없습니다. hello 시스템 이러한 사용자의 열 태그를 별도로 유지 합니다.  따라서 각 자산에 대한 ColumnTag 개체의 배열이 있습니다.  hello ColumnTag 느슨하게 바인딩된 toohello 스키마 이므로 동기화 되지 않을 수 있습니다. hello ColumnTag hello 스키마에 존재 하지 않는 열을 설명 될 수 없습니다.  Toohello 기록기 tookeep 열 태그와 동기화 하는 스키마가 있습니다.</td></tr>
<tr><td></td><td>columnName</td><td>문자열</td><td>이 태그를 참조 하는 hello 열의 hello 이름입니다.</td></tr>
<tr><td></td><td>tag</td><td>문자열</td><td>태그에 설명 하는 hello 열입니다.</td></tr>

<tr><td>전문가("experts")</td><td></td><td></td><td>이 속성 hello 데이터 집합에 익숙하지 것으로 간주 되는 사용자를 포함 합니다. hello 전문가 opinions(descriptions) 거품형 toohello의 최상위 hello UX 설명 목록을 만들 때입니다. 각 사용자는 자신의 전문가를 지정할 수 있습니다. 해당 사용자만 hello 전문가 개체를 편집할 수 있습니다. 관리자 및 자산 소유자 수 hello 전문가 개체를 삭제 되지만 편집할 수 없습니다.</td></tr>
<tr><td></td><td>전문가</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>미리 보기("previews")</td><td></td><td></td><td>hello 미리 보기에는 hello 상위 20 행의 hello 자산에 대 한 데이터의 스냅숏을 포함 되어 있습니다. 미리 보기는 일부 형식의 자산에만 적합합니다(테이블에 대해서는 적합하지만 측정값에 대해서는 적합하지 않음).</td></tr>
<tr><td></td><td>미리 보기</td><td>object[]</td><td>열을 나타내는 개체의 배열입니다.  각 개체에 hello 행에 대 한 해당 열에 대 한 값을 가진 tooa 열 매핑 속성이 있습니다.</td></tr>

<tr><td>AccessInstruction("accessInstructions")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mimeType</td><td>string</td><td>hello hello 콘텐츠의 mime 형식입니다.</td></tr>
<tr><td></td><td>콘텐츠</td><td>string</td><td>hello tooget toothis 데이터 자산을 액세스 하는 방법을 설명 합니다. hello 콘텐츠 URL을, 전자 메일 주소 또는 일련의 지침을 수 있습니다.</td></tr>

<tr><td>TableDataProfile("tableDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>int</td><td>hello hello 데이터 집합의 행 수</td></tr>
<tr><td></td><td>size</td><td>long</td><td>hello hello 데이터 집합의 바이트 크기입니다.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>string</td><td>hello 시간 hello 스키마를 마지막으로 수정한</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>string</td><td>hello 마지막 시간 hello 데이터 집합으로 수정 된 (데이터 추가, 수정 또는 삭제)</td></tr>

<tr><td>ColumnsDataProfile("columnsDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>열</td></td><td>ColumnDataProfile[]</td><td>열 데이터 프로필의 배열입니다.</td></tr>

<tr><td>ColumnDataClassification("columnDataClassifications")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName</td><td>문자열</td><td>이 분류를 참조 하는 hello 열의 hello 이름입니다.</td></tr>
<tr><td></td><td>분류</td><td>문자열</td><td>이 열에 hello 데이터의 hello 분류 합니다.</td></tr>

<tr><td>설명서("documentation")</td><td></td><td></td><td>지정된 자산은 하나의 설명서에만 연결될 수 있습니다.</td></tr>
<tr><td></td><td>mimeType</td><td>string</td><td>hello hello 콘텐츠의 mime 형식입니다.</td></tr>
<tr><td></td><td>콘텐츠</td><td>string</td><td>hello 설명서 내용입니다.</td></tr>

</table>

### <a name="common-types"></a>일반 형식
일반적인 유형은 속성에 대 한 hello 형식으로 사용할 수 있지만 항목이 아닙니다.

<table>
<tr><td><b>일반 형식</b></td><td><b>속성</b></td><td><b>데이터 형식</b></td><td><b>설명</b></td></tr>
<tr><td>DataSourceInfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>sourceType</td><td>string</td><td>Hello 유형의 데이터 원본에 설명합니다.  예: SQL Server, Oracle 데이터베이스 등.  </td></tr>
<tr><td></td><td>ObjectType</td><td>string</td><td>Hello 유형의 hello 데이터 원본에 개체를 설명합니다. 예: 테이블, SQL Server용 뷰.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>protocol</td><td>string</td><td>필수입니다. Hello 데이터 원본으로 사용 되는 프로토콜 toocommunicate에 설명합니다. 예: SQl Server의 경우 "tds", Oracle의 경우 "oracle" 등. 너무 참조[데이터 원본 참조 사양-DSL 구조](data-catalog-dsr.md) hello 목록은 현재 지원 되는 프로토콜입니다.</td></tr>
<tr><td></td><td>address</td><td>Dictionary<string, object></td><td>필수입니다. 주소는 사용 되는 tooidentify hello 데이터 원본이 참조 되는 데이터 특정 toohello 프로토콜의 집합입니다. hello 주소 데이터 범위 hello 프로토콜을 알지 못해도 의미 없는 않음 tooa 특정 프로토콜.</td></tr>
<tr><td></td><td>인증</td><td>string</td><td>선택 사항입니다. hello 인증 체계 hello 데이터 원본과 toocommunicate를 사용합니다. 예: windows, oauth, 등.</td></tr>
<tr><td></td><td>connectionProperties</td><td>Dictionary<string, object></td><td>선택 사항입니다. 방법 알아보려면 tooconnect tooa 데이터 원본입니다.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>hello 백 엔드 게시 하는 동안 AAD에 대해 제공 되는 속성의 유효성 검사를 수행 하지 않습니다.</td></tr>
<tr><td></td><td>upn</td><td>string</td><td>사용자의 고유한 전자 메일 주소입니다. ObjectId 제공 되지 않은 경우 또는 그렇지 않은 경우 선택 사항 "lastRegisteredBy" 속성의 hello 컨텍스트에서 지정 되어야 합니다.</td></tr>
<tr><td></td><td>objectId</td><td>Guid</td><td>사용자 또는 보안 그룹 AAD ID입니다. 선택 사항입니다. upn이 제공되지 않은 경우 지정해야 합니다. 그렇지 않은 경우 선택 사항입니다.</td></tr>
<tr><td></td><td>firstname</td><td>string</td><td>사용자의 이름(표시 용). 선택 사항입니다. "LastRegisteredBy" 속성의 hello 컨텍스트에서 유효 합니다. "역할", "권한" 및 "전문가"에 대한 보안 주체를 제공할 때 지정할 수 없습니다.</td></tr>
<tr><td></td><td>Lastname</td><td>string</td><td>사용자 성(표시 용). 선택 사항입니다. "LastRegisteredBy" 속성의 hello 컨텍스트에서 유효 합니다. "역할", "권한" 및 "전문가"에 대한 보안 주체를 제공할 때 지정할 수 없습니다.</td></tr>

<tr><td>열</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>Hello 열 또는 특성의 이름입니다.</td></tr>
<tr><td></td><td>type</td><td>string</td><td>hello 열 또는 특성의 데이터 형식입니다. hello 허용 되는 형식을 hello 자산의 데이터 원본 형식에 따라 달라 집니다.  형식의 하위 집합만 지원됩니다.</td></tr>
<tr><td></td><td>maxLength</td><td>int</td><td>hello 열 또는 특성에 대해 허용 된 최대 길이 hello 합니다. 데이터 소스에서 파생됩니다. 만 해당 toosome 원본 유형입니다.</td></tr>
<tr><td></td><td>자릿수</td><td>byte</td><td>hello 열 또는 특성에 대 한 hello 전체 자릿수입니다. 데이터 소스에서 파생됩니다. 만 해당 toosome 원본 유형입니다.</td></tr>
<tr><td></td><td>isNullable</td><td>Boolean</td><td>Hello 열 인지 여부 toohave null 값을 허용 합니다. 데이터 소스에서 파생됩니다. 만 해당 toosome 원본 유형입니다.</td></tr>
<tr><td></td><td>식</td><td>string</td><td>Hello 값이 계산된 열 이면이 필드는 hello 값을 제시 하는 hello 식을 포함 합니다. 데이터 소스에서 파생됩니다. 만 해당 toosome 원본 유형입니다.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName </td><td>string</td><td>hello 열의 hello 이름</td></tr>
<tr><td></td><td>type </td><td>string</td><td>hello 유형의 hello 열</td></tr>
<tr><td></td><td>Min </td><td>string</td><td>hello hello 데이터 집합의 최소값</td></tr>
<tr><td></td><td>max </td><td>string</td><td>hello hello 데이터 집합의 최대값</td></tr>
<tr><td></td><td>avg </td><td>double</td><td>hello hello 데이터 집합의 평균 값</td></tr>
<tr><td></td><td>stdev </td><td>double</td><td>hello 데이터 집합에 대 한 hello 표준 편차</td></tr>
<tr><td></td><td>nullCount </td><td>int</td><td>hello hello 데이터 집합의 null 값 개수</td></tr>
<tr><td></td><td>distinctCount  </td><td>int</td><td>hello 데이터 집합의 고유한 값의 hello 개수</td></tr>


</table>

## <a name="asset-identity"></a>자산 ID
"프로토콜"을 사용 하 여 azure 데이터 카탈로그 및 hello 사용 되는 tooaddress는 hello 자산의 hello DataSourceLocation "dsl" 속성 toogenerate id의 속성 모음은 "address"에서 id 속성 hello hello 카탈로그 내 자산입니다.
예를 들어 hello "tds" 프로토콜 id 속성 "server", "database", "스키마" 및 "개체"에 있습니다. hello hello 프로토콜 및 hello id 속성의 조합은 hello SQL Server 테이블 자산의 hello id를 사용 하는 toogenerate 합니다.
Azure Data Catalog에는 몇 가지 데이터 원본 프로토콜이 기본으로 제공되며 [데이터 원본 참조 사양 - DSL 구조](data-catalog-dsr.md)에 목록이 있습니다.
hello의 지원 되는 프로토콜 집합을 확장할 수 프로그래밍 방식으로 (참조 tooData 카탈로그 REST API 참조). Hello 카탈로그의 관리자는 사용자 지정 데이터 원본 프로토콜을 등록할 수 있습니다. hello 다음 설명 hello 필요한 속성 tooregister 사용자 지정 프로토콜입니다.

### <a name="custom-data-source-protocol-specification"></a>사용자 지정 데이터 원본 프로토콜 사양
<table>
<tr><td><b>형식</b></td><td><b>속성</b></td><td><b>데이터 형식</b></td><td><b>설명</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>namespace</td><td>string</td><td>hello 프로토콜의 hello 네임 스페이스입니다. 점 (.)으로 구분 된 하나 이상의 비어 있지 않은 파트가 포함 될 Namespace too255 1 자에서 여야 합니다. 각 부분 해야 1 too255 자 여야 하며 문자로 시작 되며 문자와 숫자 포함 합니다.</td></tr>
<tr><td></td><td>name</td><td>string</td><td>hello 프로토콜의 hello 이름입니다. 이름의 해야 too255 1 자 여야 하며 문자로 시작 되며 문자, 숫자 및 hello 대시 (-) 문자를 포함 합니다.</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty[]</td><td>ID 속성 목록이며, 하나 이상 20 이하의 속성을 포함해야 합니다. 예: "server", "database", "스키마", "개체" hello "tds" 프로토콜의 id 속성은 합니다.</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet[]</td><td>ID 목록 집합입니다. 유효한 자산의 ID를 나타내는 ID 속성 집합을 정의합니다. 하나 이상 20 이하의 집합을 포함해야 합니다. 예를 들어, {"server", "database", "schema" and "object"}는 "tds" 프로토콜에 대한 ID 집합이며, Sql Server 테이블 자산의 ID를 정의합니다.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>hello 속성의 hello 이름입니다. 이름은 1 too100 문자로 long, 문자로 시작 해야 하며 문자와 숫자만 포함 될 수 있습니다.</td></tr>
<tr><td></td><td>type</td><td>string</td><td>hello 유형의 hello 등록 합니다. 지원되는 값: "bool", boolean", "byte", "guid", "int", "integer", "long", "string", "url"</td></tr>
<tr><td></td><td>ignoreCase</td><td>bool</td><td>속성 값을 사용할 때 대/소문자를 무시할지 여부를 나타냅니다. "string" 형식의 속성에 대해서만 지정할 수 있습니다. 기본값은 False입니다.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>bool[]</td><td>Hello url 경로의 각 세그먼트에 대해 대/소문자를 무시할지 여부를 나타냅니다. "url" 형식의 속성에 대해서만 지정할 수 있습니다. 기본값은 [false]입니다.</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>hello id의 hello 이름이 설정합니다.</td></tr>
<tr><td></td><td>properties</td><td>string[]</td><td>이 id를 포함 하는 id 속성의 hello 목록이 설정 합니다. 중복 항목을 포함할 수 없습니다. Id 집합에서 참조 하는 각 속성의 "identityProperties" hello 프로토콜의 hello 목록에 정의 되어야 합니다.</td></tr>

</table>

## <a name="roles-and-authorization"></a>역할 및 권한 부여
Microsoft Azure 데이터 카탈로그는 자산 및 주석에 대한 CRUD 작업에 대해 권한 부여 기능을 제공합니다.

## <a name="key-concepts"></a>주요 개념
hello Azure Data Catalog는 두 가지 권한 부여 메커니즘을 사용합니다.

* 역할 기반 권한 부여
* 사용 권한 기반의 권한 부여

### <a name="roles"></a>역할
**관리자**, **소유자** 및 **참여자** 등 3가지 역할이 있습니다.  각 역할의 범위와 권한으로, 다음 표에 hello에 요약 되어 있습니다.

<table><tr><td><b>역할</b></td><td><b>범위</b></td><td><b>권한</b></td></tr><tr><td>관리자</td><td>카탈로그 (모든 자산/주석 hello 카탈로그)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>소유자</td><td>각 자산(루트 항목)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>참여자</td><td>각 개별 자산 및 주석</td><td>읽기 업데이트 삭제 ViewRoles 참고: 모든 hello 권한이 해지 됩니다 hello 읽을 마우스 오른쪽 단추로 hello 항목 hello 참가자에서에서 해지 된 경우</td></tr></table>

> [!NOTE]
> **읽기**, **업데이트**, **삭제**, **ViewRoles** 권한은 하면서 해당 tooany 항목 (자산 또는 주석) **TakeOwnership**, **ChangeOwnership**, **ChangeVisibility**, **ViewPermissions** 적용 가능한 toohello 루트 자산만 됩니다.
> 
> **삭제** tooan 항목 및 하위 항목 또는 그 아래에 있는 단일 항목 권한은 적용 됩니다. 예를 들어, 자산을 삭제하면 해당 자산에 대한 모든 주석도 삭제됩니다.
> 
> 

### <a name="permissions"></a>권한
권한은 액세스 제어 항목의 목록입니다. 각 액세스 제어 항목 집합이 권한 tooa 보안 주체에 할당합니다. 사용 권한 자산 (즉, 루트 항목)에 지정할 수 있습니다 및 toohello 자산 및 모든 하위 항목을 적용 합니다.

Hello 동안 **Azure Data Catalog** 미리만 **읽기** 오른쪽 hello 사용 권한 목록 tooenable 시나리오 toorestrict의 표시 유형을 자산에서 지원 됩니다.

기본적으로 모든 인증 된 사용자에 게 **읽기** 가시성 제한 되어 있지 않으면 hello 카탈로그의 모든 항목에 대해 마우스 오른쪽 단추로 toohello hello 사용 권한에서 보안 주체 집합입니다.

## <a name="rest-api"></a>REST API
**배치** 및 **POST** 보기 항목을 사용 하는 toocontrol 역할 및 사용 권한 수 요청: 더하기 tooitem 페이로드 두 개의 시스템 속성을 지정할 수 **역할** 및  **사용 권한**합니다.

> [!NOTE]
> **사용 권한** 만 적용 가능한 tooa 루트 항목입니다.
> 
> **소유자** 역할에만 적용할 수 tooa 루트 항목입니다.
> 
> Hello 카탈로그에서 항목을 만들 때 기본적으로 해당 **참가자** toohello 현재 인증 된 사용자를 설정 합니다. 항목이 모든 사용자를 업데이트할 수 있어야 합니다. **참가자** 너무 설정 해야&lt;Everyone&gt; hello에서 특수 보안 주체 **역할** 속성 항목이 있을 때에 먼저 (게시 다음 예에서는 toohello 참조). **참가자** 변경할 수 없는 유지 되며 항목의 수명 동안 동일한 hello 및 (도 **관리자** 또는 **소유자** hello 오른쪽 toochange hello 없는  **참가자**). 안녕하세요 명시적으로 설정 hello에 대 한 지원 되는 값만 hello **참가자** 은 &lt;Everyone&gt;: **참가자** 는 항목을 만든 사용자만 될 수 있습니다 또는 &lt; 모든 사용자&gt;합니다.
> 
> 

### <a name="examples"></a>예
**참가자를 너무 설정&lt;Everyone&gt; 항목을 게시 하는 경우.**
특수 보안 주체 &lt;Everyone&gt;에는 objectId "00000000-0000-0000-0000-000000000201"이 있습니다.
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> 일부 HTTP 클라이언트 구현에 자동으로 응답 tooa 302 hello 서버에서의 요청을 다시 발급 받으십시오 있지만 일반적으로 hello 요청에서 권한 부여 헤더를 스트립 수 있습니다. Hello 권한 부여 헤더에 필요한 toomake 요청 tooAzure 데이터 카탈로그 이므로 Azure Data Catalog에서 지정 하는 요청 tooa 리디렉션 위치를 다시 발급 권한 부여 헤더를 hello 계속 제공 됩니다 확인 해야 합니다. hello 다음 샘플 코드에서는 hello.NET HttpWebRequest 개체를 사용 하 여 합니다.
> 
> 

**본문**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **소유자를 할당하고 기존 루트 항목에 대한 표시를 제한**: **PUT** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> PUT에 필요 하지는 hello 본문에는 항목 페이로드 toospecify: PUT 사용된 tooupdate 정당한 역할 및/또는 공개 될 수 있습니다.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
