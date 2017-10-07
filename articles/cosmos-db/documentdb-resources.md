---
title: "Cosmos DB aaaAzure 리소스 모델 및 개념 | Microsoft Docs"
description: "데이터베이스, 컬렉션, 사용자 정의 함수 (UDF), 문서, 사용 권한 toomanage 리소스 등의 Azure Cosmos DB 계층적 모델에 알아봅니다."
keywords: "계층적 모델, cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Azure Cosmos DB 계층적 리소스 모델 및 핵심 개념
hello 데이터베이스 엔터티 Azure Cosmos DB를 관리 하는 참조 된 tooas **리소스**합니다. 각 리소스는 논리적 URI를 통해 고유하게 식별됩니다. 표준 HTTP 동사, 요청/응답 헤더 및 상태 코드를 사용 하 여 hello 리소스와 상호 작용할 수 있습니다. 

이 문서를 참조 하 여 다음 질문 수 tooanswer hello 수 있습니다.

* Cosmos DB의 리소스 모델이란?
* 시스템 리소스를 정의 하는 것과 반대로 toouser 리소스로 정의 했습니까?
* 리소스를 어떻게 해결하나요?
* 컬렉션을 어떻게 사용하나요?
* 저장된 프로시저, 트리거 및 UDF(사용자 정의 함수)를 사용하려면 어떻게 하나요?

## <a name="hierarchical-resource-model"></a>계층적 리소스 모델
에서처럼 hello 다음 다이어그램 hello Cosmos DB 계층적 **리소스 모델** 집합 논리적이 고 안정적인 URI를 통해 각 주소 지정 가능한 데이터베이스 계정 내 리소스도 구성 됩니다. 리소스 집합이 참조 tooas 됩니다는 **피드** 이 문서의 내용입니다. 

> [!NOTE]
> Hello를 통해 사용할 수 있는 해당 통신 모델에 RESTful 포함 되어 있는 매우 효율적인 TCP 프로토콜을 제공 하는 azure Cosmos DB [DocumentDB.NET 클라이언트 API](documentdb-sdk-dotnet.md)합니다.
> 
> 

![Azure Cosmos DB 계층적 리소스 모델][1]  
**계층적 리소스 모델**   

toostart 리소스, 작업을 수행 해야 [데이터베이스 계정 만들기](create-documentdb-dotnet.md) Azure 구독을 사용 하 여 합니다. 데이터베이스 계정은 각각 여러 **컬렉션**을 포함하는 **데이터베이스** 집합으로 구성될 수 있고, 각 컬렉션에는 다시 **저장 프로시저, 트리거, UDF, 문서** 및 관련 **첨부 파일**이 포함됩니다. 또한 데이터베이스에 연결 된 **사용자**의 집합을 가진 **사용 권한을** tooaccess 컬렉션 프로시저, 트리거, Udf, 문서, 첨부 파일을 저장 합니다. 데이터베이스, 사용자, 사용 권한 및 컬렉션은 잘 알려진 스키마가 있는 시스템 정의 리소스인 반면 문서 및 첨부 파일에는 임의의 사용자 정의 JSON 콘텐츠가 포함됩니다.  

| 리소스 | 설명 |
| --- | --- |
| 데이터베이스 계정 |데이터베이스 계정은 데이터베이스 집합 및 고정된 양의 첨부 파일용 Blob Storage에 연결됩니다. Azure 구독을 사용하여 데이터베이스 계정을 하나 이상 만들 수 있습니다. 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요. |
| 데이터베이스 |데이터베이스는 여러 컬렉션으로 분할된 문서 저장소의 논리적 컨테이너입니다. 또한 사용자 컨테이너입니다. |
| 사용자 |hello 권한 범위를 지정 하는 것에 대 한 논리적 네임 스페이스입니다. |
| 사용 권한 |액세스 tooa 특정 리소스에 대 한 사용자와 관련 된 권한 부여 토큰입니다. |
| 컬렉션 |컬렉션은 JSON 문서의 컨테이너 및 hello JavaScript 응용 프로그램 논리 합니다. 컬렉션은 청구 가능 엔터티에 hello [비용](performance-levels.md) hello 컬렉션과 연결 된 hello 성능 수준에 의해 결정 됩니다. 컬렉션 하나 이상의 파티션을/서버에 걸쳐 있을 수 없으며 확장할 수 toohandle 저장소나 처리량 거의 무제한 볼륨입니다. |
| 저장 프로시저 |컬렉션에 등록 되 고 hello 데이터베이스 엔진 내에서 트랜잭션 방식으로 실행 되는 JavaScript로 작성 된 응용 프로그램 논리입니다. |
| 트리거 |삽입, 바꾸기 또는 삭제 작업 전 후에 실행된 JavaScript로 작성된 응용 프로그램 논리입니다. |
| UDF |JavaScript로 작성된 응용 프로그램 논리입니다. Udf는 toomodel 사용자 지정 쿼리 연산자를 사용 하도록 설정 하 고 있으므로 hello 핵심 DocumentDB API 쿼리 언어를 확장 합니다. |
| 문서 |사용자 정의(임의) JSON 콘텐츠입니다. 기본적으로 없습니다 스키마에 정의 된 toobe 필요 하거나 보조 인덱스 필요가 toobe 모든 hello에 대 한 문서 추가 tooa 컬렉션 제공. |
| 첨부 파일 |첨부 파일은 외부 blob/미디어에 대한 참조 및 관련 메타데이터가 포함된 특수 문서입니다. hello 개발자 OneDrive, Dropbox 등의 외부 blob 서비스 공급자를 사용 하 여 저장 하거나 Cosmos DB에서 관리 되는 toohave hello blob을 선택할 수 있습니다. |

## <a name="system-vs-user-defined-resources"></a>시스템 정의 리소스와 사용자 정의 리소스 비교
데이터베이스 계정, 데이터베이스, 컬렉션, 사용자, 사용 권한, 저장 프로시저, 트리거 및 UDF와 같은 리소스에는 모두 고정 스키마가 있으며 시스템 리소스라고 합니다. 반면, 문서 첨부 파일 등의 리소스 제한이에 hello 스키마 있고은 사용자 정의 리소스의 예입니다. Cosmos DB에서는 시스템 및 사용자 정의 리소스 둘 다 표준 규격 JSON으로 표시되고 관리됩니다. 모든 리소스, 시스템 또는 사용자 정의 다음과 같은 일반적인 속성 hello 됩니다.

> [!NOTE]
> JSON 표현에서는 리소스의 모든 시스템 생성 속성 앞에 밑줄(_)이 추가됩니다.
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>속성</strong></p></td>
            <td valign="top"><p><strong>사용자 설정 가능 또는 시스템 생성?</strong></p></td>
            <td valign="top"><p><strong>목적</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>시스템 생성</p></td>
            <td valign="top"><p>시스템 생성 된 hello 리소스의 고유 하 고 계층 구조 식별자</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>시스템 생성</p></td>
            <td valign="top"><p>낙관적 동시성 제어에 필요한 hello 리소스의 etag</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>시스템 생성</p></td>
            <td valign="top"><p>Hello 리소스의 마지막 업데이트 타임 스탬프</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>시스템 생성</p></td>
            <td valign="top"><p>Hello 리소스의 고유 주소 지정 가능한 URI</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>시스템 생성</p></td>
            <td valign="top"><p>사용자 정의 hello 리소스의 고유 이름 (hello로 동일한 분할 키 값). Hello 사용자 id를 지정 하지 않는 경우 id 시스템에서 생성 됩니다.</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>리소스의 네트워크 표현
Cosmos DB 모든 고유 확장 프로그램이 toohello JSON 표준 또는 특수 인코딩;는 필요 하지 않습니다. 표준 규격 JSON 문서와 함께 작동합니다.  

### <a name="addressing-a-resource"></a>리소스 주소 지정
모든 리소스는 URI로 주소 지정이 가능합니다. 값의 hello hello **_self** 속성 리소스의 나타냅니다 hello hello 리소스의 상대 URI입니다. hello hello URI의 형식은 이루어져 hello /\<피드\>/ {_rid} 경로 세그먼트:  

| Hello _self의 값 | 설명 |
| --- | --- |
| /dbs |데이터베이스 계정의 데이터베이스 피드 |
| /dbs/{dbName} |{DbName} hello 값과 일치 하는 id 사용 하 여 데이터베이스 |
| /dbs/{dbName}/colls/ |데이터베이스의 컬렉션 피드 |
| /dbs/{dbName}/colls/{collName} |{CollName} hello 값과 일치 하는 id 사용 하 여 컬렉션 |
| /dbs/{dbName}/colls/{collName}/docs |컬렉션의 문서 피드 |
| /dbs/{dbName}/colls/{collName}/docs/{docId} |{Doc} hello 값과 일치 하는 id를 사용 하 여 문서 |
| /dbs/{dbName}/users/ |데이터베이스의 사용자 피드 |
| /dbs/{dbName}/users/{userId} |{User} hello 값과 일치 하는 id 가진 사용자 |
| /dbs/{dbName}/users/{userId}/permissions |사용자의 사용 권한 피드 |
| /dbs/{dbName}/users/{userId}/permissions/{permissionId} |{권한} hello 값과 일치 하는 id 가진 사용 권한 |

각 리소스에 hello id 속성을 통해 노출 되는 고유한 사용자 정의 이름입니다. 참고: 문서에 대 한 hello 사용자 id를 지정 하지 않는 경우 지원 되는 Sdk 자동으로 생성 됩니다 hello 문서에 대 한 고유 id입니다. hello id는 특정 부모 리소스의 hello 컨텍스트 내에서 고유한 too256 문자를의 사용자 정의 문자열입니다. 

각 리소스에는 시스템 생성 계층적 리소스 식별자 (또한 참조 tooas에서 RID)를 hello _rid 속성을 통해 사용할 수 있습니다. hello RID hello 전체 계층의 지정된 된 리소스의 인코딩하고 편리한 내부 표현에 분산된 방식으로 tooenforce 참조 무결성을 사용 합니다. hello RID 데이터베이스 계정 내에서 고유 하며 크로스 파티션 조회 필요 없이 효율적인 라우팅에 Cosmos DB에서 내부적으로 사용 됩니다. hello hello _self 및 hello _rid 속성 값은 리소스의 대체 및 정식 표시입니다. 

hello 리소스의 주소를 지정 하 고 hello id와 hello _rid 속성 모두 요청 라우팅을 REST Api 지원 합니다.

## <a name="database-accounts"></a>데이터베이스 계정
Azure 구독을 사용하여 Cosmos DB 데이터베이스 계정을 하나 이상 프로비전할 수 있습니다.

만들고 hello Azure 포털을 통해 Cosmos DB 데이터베이스 계정을 관리할 수 있습니다에 [http://portal.azure.com/](https://portal.azure.com/)합니다. 데이터베이스 계정을 만들고 관리하려면 관리 액세스 권한이 필요하며 Azure 구독으로만 수행할 수 있습니다. 

### <a name="database-account-properties"></a>데이터베이스 계정 속성
데이터베이스 계정 관리 및 프로 비전의 일부로 구성 하 고 hello 다음과 같은 속성을 읽을 수 있습니다.  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>속성 이름</strong></p></td>
            <td valign="top"><p><strong>설명</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>일관성 정책</p></td>
            <td valign="top"><p>이 속성 tooconfigure hello 기본 일관성 수준이 데이터베이스 계정에서 모든 hello 컬렉션을 설정 합니다. Hello 일관성 수준이 hello [x-ms-일관성-수준] 요청 헤더를 사용 하 여 요청 별로 재정의할 수 있습니다. <p><p>이 속성에만 toohello 적용 참고 <i>사용자 정의 리소스</i>합니다. 모든 시스템 정의 된 리소스는 강력한 일관성과 함께 구성 된 toosupport 읽기/쿼리입니다.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>권한 부여 키</p></td>
            <td valign="top"><p>기본 hello와 보조 마스터 및 읽기 전용 키 관리를 제공 하는 hello hello 데이터베이스 계정 내 리소스의 tooall 액세스.</p></td>
        </tr>
    </tbody>
</table>

또한 tooprovisioning, 구성 및 hello Azure 포털에서에서 데이터베이스 계정 관리에서 있습니다 수 또한 프로그래밍 방식으로 계정을 만들고 관리할 Cosmos DB 데이터베이스 hello를 사용 하 여 참고 [Azure Cosmos DB REST Api](/rest/api/documentdb/) 으로 뿐만 아니라 [클라이언트 Sdk](documentdb-sdk-dotnet.md)합니다.  

## <a name="databases"></a>데이터베이스
Cosmos DB 데이터베이스는 hello 다음 다이어그램에에서 나와 있는 것 처럼 하나 이상의 컬렉션 및 사용자에의 한 논리적 컨테이너입니다. 제한 개수에 관계 없이 Cosmos DB 데이터베이스 계정 주체 toooffer에서 데이터베이스를 만들 수 있습니다.  

![데이터베이스 계정 및 컬렉션 계층적 모델][2]  
**데이터베이스는 사용자 및 컬렉션의 논리적 컨테이너입니다.**

한 데이터베이스에는 컬렉션 내에서 분할된 거의 무제한의 문서 저장소를 포함할 수 있습니다.

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Cosmos DB 데이터베이스의 탄력적인 확장
Cosmos DB 데이터베이스는 백업 SSD 문서 저장 및 프로 비전 된 처리량의 몇 가지 GB toopetabytes에서 범위의 – 기본적으로 탄력적입니다. 

기존의 RDBMS에서 데이터베이스와 달리 Cosmos DB에는 데이터베이스를 tooa 범위가 지정 된 단일 컴퓨터 없습니다. Cosmos DB와 함께 응용 프로그램의 배율 toogrow, 요구에 따라 더 많은 컬렉션, 데이터베이스 또는 둘 다 만들 수 있습니다. 실제로 Microsoft 내의 다양한 자사 응용 프로그램은 각각 테라바이트의 문서 저장소가 있는 컬렉션이 수천 개 포함된 대형 Cosmos DB 데이터베이스를 만들어 소비자 배율로 Cosmos DB를 사용했습니다. 확대 하거나 추가 하거나 컬렉션 toomeet 응용 프로그램의 확장 요구 사항을 제거 하 여 데이터베이스를 축소할 수 있습니다. 

컬렉션을 데이터베이스 주체 toohello 제안 개수에 관계 없이 만들 수 있습니다. 각 컬렉션에 백업 하는 SSD 저장소 및 hello 선택한 성능 계층에 따라 사용자에 대 한 프로 비전 된 처리량이 있습니다.

Cosmos DB 데이터베이스는 사용자 컨테이너이기도 합니다. 사용자를 하는 세분화 된 권한 부여 및 액세스 toocollections, 문서, 첨부 파일을 제공 하는 사용 권한 집합에 대 한 논리적 네임 스페이스입니다.  

Hello Cosmos DB 리소스 모델에서 다른 리소스와 데이터베이스를 만들 수 있습니다, 대체, 삭제, 읽기 또는 hello 중 하나를 사용 하 여 쉽게 열거 [REST Api](/rest/api/documentdb/) 또는 hello [클라이언트 Sdk](documentdb-sdk-dotnet.md)합니다. Cosmos DB 읽기 또는 데이터베이스 리소스의 hello 메타 데이터를 쿼리 하는 강력한 일관성을 보장 합니다. 데이터베이스를 자동으로 삭제 하면 hello 컬렉션 또는 그 안에 포함 된 사용자가 액세스할 수 없습니다.   

## <a name="collections"></a>컬렉션
Cosmos DB 컬렉션은 JSON 문서의 컨테이너입니다. 

### <a name="elastic-ssd-backed-document-storage"></a>탄력적 SSD 지원 문서 저장소
컬렉션은 본질적으로 탄력적입니다. 문서를 추가하거나 제거하면 자동으로 확장 및 축소됩니다. 컬렉션은 하나 이상의 물리적 파티션 또는 서버에 걸쳐 있을 수 있는 논리적 리소스입니다. 컬렉션 내에서 파티션 수 hello Cosmos db hello 저장소 크기와 hello 컬렉션의 프로 비전 된 처리량에 따라 결정 됩니다. Cosmos DB의 모든 파티션은 고정된 양의 SSD 지원 저장소에 연결되며, 고가용성을 위해 복제됩니다. 파티션 관리 Azure Cosmos DB에서 관리 하는 완벽 하 게 하 고 toowrite 복잡 한 코드가 있는 또는 파티션을 관리 하지 않는 합니다. Cosmos DB 컬렉션은 저장소 및 처리량이 **거의 무제한**입니다. 

### <a name="automatic-indexing-of-collections"></a>컬렉션의 자동 인덱싱
Cosmos DB는 진정한 스키마 없는 데이터베이스 시스템입니다. 가정 하거나 hello JSON 문서에 대 한 모든 스키마가 필요 하지 않습니다. 문서 tooa 컬렉션을 추가 하면 Cosmos DB에서 자동으로 인덱싱됩니다 고 tooquery 있습니다 사용할 수 있는 합니다. 스키마 또는 보조 인덱스가 필요 없는 자동 문서 인덱싱은 Cosmos DB의 주요 기능이며 쓰기 최적화되고 잠금이 없으며 로그 구조화된 인덱스 유지 관리 기술을 통해 사용할 수 있습니다. Cosmos DB는 일관성 있는 쿼리를 제공하는 동시에 매우 빠른 쓰기의 지속적인 볼륨을 지원합니다. 문서와 인덱스 저장소는 각 컬렉션에 의해 사용 되는 toocalculate hello 저장소를 사용 합니다. Hello 저장 및 성능의 장단점 hello 컬렉션에 대 한 인덱싱 정책을 구성 하 여 인덱싱 연관 제어할 수 있습니다. 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>컬렉션의 hello 인덱싱 정책을 구성합니다.
인덱싱 정책 각 컬렉션의 hello toomake 성능 및 저장소 장점과 단점을 이해 하는 인덱스가 연관 수 있습니다. hello 다음 옵션을 사용할 수 있는 tooyou 인덱싱 구성의 일부분으로.  

* 여부 hello 컬렉션 자동으로 인덱싱됩니다 모든 hello 문서 여부를 선택 합니다. 기본적으로 모든 문서가 자동으로 인덱싱됩니다. 자동 인덱싱을 해제 tooturn 선택할 수 있으며 특정 문서 toohello 인덱스만 선택적으로 추가 합니다. 반대로, 선택할 수 있습니다 tooexclude 특정 문서에만 합니다. 컬렉션의 hello indexingPolicy에 hello 자동 속성 toobe true 또는 false를 설정 하 고 삽입, 교체 또는 문서를 삭제 하는 동안 hello [x ms indexingdirective] 요청 헤더를 사용 하 여이 작업을 수행할 수 있습니다.  
* Tooinclude 또는 exclude 특정 경로 또는 패턴에서 문서에서 인덱스 hello 여부를 선택 합니다. 이 위해서는 설정 includedPaths 및 excludedPaths hello indexingPolicy의 컬렉션에 각각 있습니다. Hello 저장 및 성능의 장단점 범위에 대 한를 구성 하 고 특정 경로 패턴에 대 한 쿼리 해시 수도 있습니다. 
* 동기(일관성) 및 비동기(지연) 인덱스 업데이트 간에 선택합니다. 기본적으로 hello 인덱스가 삽입, 교체 또는 삭제 문서 toohello 컬렉션의 각에 동기적으로 업데이트 됩니다. 이렇게 하면 hello 쿼리 toohonor hello hello 문서 읽기와 같은 일관성 수준이 있습니다. Cosmos DB 쓰기가 최적화 하 고 동기 인덱스 유지 관리 및 일관 된 쿼리를 처리할 함께 문서 쓰기 지속적인된 볼륨을 지 원하는, 구성할 수 있습니다 컬렉션 tooupdate 특정 해당 인덱스를 지연 합니다. Lazy 인덱싱을 hello 쓰기 성능이 더욱 증폭 이며 주로 읽기 작업이 너무 많은 컬렉션에 대 한 대량 수집 시나리오에 적합 합니다.

인덱싱 정책을 hello PUT hello 컬렉션에서 실행 하 여 변경할 수 있습니다. 이 수 hello 통해 달성 [클라이언트 SDK](documentdb-sdk-dotnet.md), hello [Azure 포털](https://portal.azure.com) 또는 hello [REST Api](/rest/api/documentdb/)합니다.

### <a name="querying-a-collection"></a>컬렉션 쿼리
컬렉션 내에서 hello 문서 수 임의의 스키마를 스키마 나 보조 인덱스를 충분히 제공 하지 않고 컬렉션 내에서 문서를 쿼리할 수 있습니다. Hello를 사용 하 여 hello 컬렉션을 쿼리할 수 [Azure Cosmos DB DocumentDB API: SQL 구문 참조](https://msdn.microsoft.com/library/azure/dn782250.aspx), 풍부한 계층적, 관계형 및 공간 연산자 및 JavaScript 기반 Udf 통해 확장성을 제공 합니다. 트리로의 레이블의 hello 트리 노드를 사용 하 여 JSON 문서를 모델링 하기 위한 JSON 문법 수 있습니다. 이 기능은 DocumentDB API의 자동 인덱싱 기술과 DocumentDB API의 SQL 언어 둘 다에서 사용됩니다. hello DocumetDB API 쿼리 언어의 세 가지 주요 측면으로 구성 됩니다.   

1. 작은 집합 자연스럽 게 프로젝션 및 계층적 쿼리를 포함 하 여 toohello 트리 구조를 매핑하는 쿼리 작업입니다. 
2. 컴퍼지션, 필터, 프로젝션, 집계 및 자체 조인을 포함하는 관계형 작업 하위 집합 
3. (1) 및 (2)로 작동하는 순수 JavaScript기반 UDF  

hello Cosmos DB 쿼리 모델 toostrike 기능, 효율성 및 단순성이 간의 균형을 시도합니다. hello Cosmos DB 데이터베이스 엔진이 기본적으로 컴파일하고 hello SQL 쿼리 문을 실행 합니다. Hello를 사용 하 여 컬렉션을 쿼리할 수 [REST Api](/rest/api/documentdb/) 또는 hello [클라이언트 Sdk](documentdb-sdk-dotnet.md)합니다. .NET SDK hello LINQ 공급자와 함께 제공 됩니다.

> [!TIP]
> Hello DocumentDB API 사용을 지정 하 고 hello에서이 데이터 집합에 대해 SQL 쿼리를 실행할 수 [Query Playground](https://www.documentdb.com/sql/demo)합니다.
> 
> 

## <a name="multi-document-transactions"></a>다중 문서 트랜잭션
데이터베이스 트랜잭션을 toohello 데이터 동시 변경 처리 하기 위한 안전 하 고 예측 가능한 프로그래밍 모델을 제공 합니다. RDBMS에서 hello 전통적인 방법 toowrite 비즈니스 논리는 toowrite **저장 프로시저** 및/또는 **트리거** 하 여 트랜잭션 실행을 위해 toohello 데이터베이스 서버를 제공 합니다. RDBMS hello 응용 프로그램 프로그래머는 두 개의 서로 다른 프로그래밍 언어와 필요한 toodeal입니다. 

* hello (비트랜잭션) 응용 프로그래밍 언어 (예: JavaScript, Python, C#, Java 등)
* T-SQL, hello 트랜잭션 프로그래밍 언어 hello 데이터베이스에서 고유 하 게 실행

해당 전체 약정 tooJavaScript 및 hello 데이터베이스 엔진 내에서 직접 JSON을 통해 Cosmos DB 직관적인 프로그래밍 모델을 제공 저장된 프로시저를 기준으로 hello 컬렉션에서 직접 응용 프로그램 논리를 기반으로 하는 실행 중인 JavaScript 및 트리거입니다. 이 hello 다음 둘 다에 대해 수 있습니다.

* 동시성의 유효 구현을 제어 hello 데이터베이스 엔진에서 직접 hello JSON 개체 그래프의 인덱싱 자동 복구
* 제어 흐름, 변수 범위 지정, 할당 및 예외 처리 기본 형식 hello JavaScript 프로그래밍 언어의 관점에서 직접 데이터베이스 트랜잭션과 통합을 자연스럽 게 표현

컬렉션 수준에서 등록 하는 hello JavaScript 논리 컬렉션을 제공 하는 hello hello 문서에서 데이터베이스 작업을 발급할 수 있습니다. 암시적으로 JavaScript 기반 저장된 프로시저 및 트리거에서 스냅숏 격리는 앰비언트 트랜잭션의 ACID 트랜잭션 내에서 래핑합니다 hello cosmos DB 컬렉션 내에서 설명 합니다. 실행의 hello 과정 JavaScript 예외를 throw 하는 hello에는 다음 전체 트랜잭션이 hello 중단 됩니다. hello 결과 프로그래밍 모델은 매우 간단 하면서도 강력한 합니다. JavaScript 개발자는 익숙한 언어 구문과 라이브러리 기본 형식을 사용하는 동시에 "내구성" 있는 프로그래밍 모델을 얻게 됩니다.   

hello hello 데이터베이스 내에서 직접 기능 tooexecute JavaScript 엔진에 hello 같은 주소 공간으로 hello 버퍼 풀은 고성능 및 hello 문서에 대해 컬렉션의 데이터베이스 작업의 트랜잭션 실행 합니다. 또한 Cosmos DB 데이터베이스 엔진에서는 전체 약정 toohello JSON 및 JavaScript 응용 프로그램의 hello 형식 시스템 및 hello 데이터베이스 간의 임피던스 불일치를 제거 합니다.   

컬렉션을 만든 후에 등록할 수 있는 저장된 프로시저, 트리거 및 Udf hello를 사용 하 여 컬렉션과 [REST Api](/rest/api/documentdb/) 또는 hello [클라이언트 Sdk](documentdb-sdk-dotnet.md)합니다. 등록이 완료되면 참조하고 실행할 수 있습니다. Hello 다음 저장 프로시저를 완전히 JavaScript로 작성 된 아래 hello 코드는 두 개의 인수 (책 이름 및 작성자 이름) 및 새 문서를 만들고, 문서를 쿼리하고 다음 업데이트-암시적 ACID 트랜잭션 내에서 모든 것이 좋습니다. 언제 든 지 hello 실행 하는 동안 JavaScript 예외가 throw 되 면 hello 전체 트랜잭션이 중단 합니다.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

hello 클라이언트 수 "배송" hello HTTP POST를 통해 트랜잭션 실행에 대 한 JavaScript 논리 toohello 데이터베이스 위에. HTTP 메서드 사용에 대한 자세한 내용은 [Azure Cosmos DB 리소스와 RESTful 상호 작용](https://msdn.microsoft.com/library/azure/mt622086.aspx)을 참조하세요. 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


Hello 데이터베이스 JSON 및 JavaScript를 기본적으로 이해, 때문에 포함 되어 있음을 알 필요 코드 생성 매직 또는 없습니다 형식 시스템 불일치를 "OR 매핑" 됩니다.   

저장된 프로시저 및 트리거 hello 현재 컬렉션 컨텍스트를 노출 하는 잘 정의 된 개체 모델을 통해 컬렉션의 컬렉션 및 hello 문서와 상호 작용 합니다.  

DocumentDB API를 만들고 삭제 하는 hello에서 컬렉션을 읽거나 hello 중 하나를 사용 하 여 쉽게 열거 [REST Api](/rest/api/documentdb/) 또는 hello [클라이언트 Sdk](documentdb-sdk-dotnet.md)합니다. hello DocumentDB API는 항상 읽기 또는 컬렉션의 hello 메타 데이터를 쿼리 하는 강력한 일관성을 제공 합니다. Hello 문서, 첨부 파일, 저장된 프로시저, 트리거 중 하나에 액세스할 수 없습니다 및 그 안에 포함 된 Udf 되도록 컬렉션을 자동으로 삭제 합니다.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>저장 프로시저, 트리거 및 UDF(사용자 정의 함수)
Hello 이전 섹션에서 설명한 대로 응용 프로그램 논리 toorun hello 데이터베이스 엔진 내에서 트랜잭션 내에서 직접 작성할 수 있습니다. hello 응용 프로그램 논리는 전적으로 JavaScript에서 작성할 수 있습니다 및 저장된 프로시저, 트리거 또는 UDF로 모델링할 수 있습니다. hello 저장된 프로시저 또는 트리거 내에서 JavaScript 코드 수 삽입, 교체, 컬렉션 내에서 읽기 또는 쿼리 문서를 삭제 합니다. 에 다른 손 hello, UDF 내에서 JavaScript hello 없습니다 삽입, 바꾸기 또는 문서를 삭제 합니다. Udf는 쿼리 결과 집합의 hello 문서를 열거 한 다른 결과 집합을 생성 합니다. 다중 테넌트 지원을 위해 Cosmos DB는 엄격한 예약 기반 리소스 거버넌스를 적용합니다. 각 저장 프로시저, 트리거 또는 UDF의 운영 체제 리소스 toodo 고정된 퀀텀 작업을 가져옵니다. 또한 저장된 프로시저, 트리거 또는 Udf 외부 JavaScript 라이브러리에 대해 연결할 수 없습니다 및 toothem 할당 hello 리소스 예산을 초과 하는 경우 차단 목록에 포함할 됩니다. 등록, 저장된 프로시저를 등록 취소할 수도 있고, 트리거 또는 Udf를 사용 하 여 컬렉션을 컬렉션으로 hello REST Api입니다.  등록하면 저장 프로시저, 트리거 또는 UDF가 사전 컴파일되고 나중에 실행되는 바이트 코드로 저장됩니다. 다음 단원을 hello Cosmos DB JavaScript SDK tooregister hello를 사용 하 여를 실행 하는 방법이 저장된 프로시저, 트리거 및 UDF를 등록 취소를 보여 줍니다. hello JavaScript SDK hello를 통해 간단한 래퍼는 [REST Api](/rest/api/documentdb/)합니다. 

### <a name="registering-a-stored-procedure"></a>저장 프로시저 등록
저장 프로시저 등록은 HTTP POST를 통해 컬렉션에 새 저장 프로시저 리소스를 만드는 것입니다.  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>저장 프로시저 실행
저장된 프로시저의 실행 hello 요청 본문에 toohello 프로시저 매개 변수를 전달 하 여 기존 저장된 프로시저 리소스에 대해 HTTP POST를 실행 하 여 수행 됩니다.

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>저장 프로시저 등록 취소
저장 프로시저 등록 취소는 단순히 기존 저장 프로시저 리소스에 대해 HTTP DELETE를 실행하여 수행합니다.   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>사전 트리거 등록
트리거 등록은 HTTP POST를 통해 컬렉션에 새 트리거 리소스를 만들어 수행합니다. Hello 트리거는 사전 또는 작업의 post 트리거와 hello 유형 수 (예: 만들기, Replace, Delete 또는 모두)와 연결 하는 경우를 지정할 수 있습니다.   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>사전 트리거 실행
트리거가 실행 hello 요청 헤더를 통해 문서 리소스의 hello DELETE/PUT/POST 요청을 발행 hello 시 hello 이름을 기존 트리거를 지정 하 여 수행 됩니다.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>사전 트리거 등록 취소
트리거 등록 취소는 단순히 기존 트리거 리소스에 대해 HTTP DELETE를 실행하여 수행합니다.  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>UDF 등록
UDF 등록은 HTTP POST를 통해 컬렉션에 새 UDF 리소스를 만들어 수행합니다.  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>Hello 쿼리의 일환으로 UDF를 실행합니다.
UDF hello SQL 쿼리의 일부로 지정할 수 있으며 사용 하는 방식으로 tooextend hello 코어로 [hello DocumentDB API에 대 한 SQL 쿼리 언어](https://msdn.microsoft.com/library/azure/dn782250.aspx)합니다.

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>UDF 등록 취소
UDF 등록 취소는 단순히 기존 UDF 리소스에 대해 HTTP DELETE를 실행하여 수행합니다.  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

위의 hello 조각 hello 등록 (POST), 등록 취소 (PUT), 목록 읽기 (GET) 및 실행 (POST) hello 통해 표시 하지만 [JavaScript SDK](https://github.com/Azure/azure-documentdb-js), hello를 사용할 수도 있습니다 [REST Api](/rest/api/documentdb/) 또는 다른 [클라이언트 Sdk](documentdb-sdk-dotnet.md)합니다. 

## <a name="documents"></a>문서
컬렉션의 임의 JSON 문서를 삽입하고, 바꾸고, 삭제하고, 읽고, 열거하고, 쿼리할 수 있습니다. Cosmos DB은 어떤 스키마도 요구 하지 않습니다 및 컬렉션의 문서에 대해 쿼리 하는 순서 toosupport에 보조 인덱스는 필요 하지 않습니다. 문서에 대 한 최대 크기 hello은 2MB입니다.   

진정한 개방형 데이터베이스 서비스인 Cosmos DB는 특수화된 데이터 형식(예: 날짜/시간) 또는 JSON 문서에 대한 특정 인코딩을 고안하지 않습니다. Cosmos DB 특수 한 JSON 규칙 toocodify hello 간의 관계가 한 다양 한 문서; 필요 하지 않습니다 Cosmos db hello SQL 구문을 tooquery 및 프로젝트 문서를 특별 한 주석이 나 고유 속성을 사용 하 여 문서 간의 필요 toocodify 관계 없이 매우 강력한 계층적 및 관계형 쿼리 연산자를 제공 합니다.  

다른 모든 리소스와 문서를 만들 수 있습니다, 대체, 삭제, 읽기, 열거 및 REST Api 또는 hello 중 하나를 사용 하 여 쉽게 쿼리할 [클라이언트 Sdk](documentdb-sdk-dotnet.md)합니다. 문서를 즉시 삭제 공간 hello 할당량 해당 tooall 중첩 hello 첨부 파일을 만듭니다. hello 읽을 문서 일관성 수준이 데이터베이스 계정 hello에 hello 일관성 정책을 따릅니다. 응용 프로그램의 데이터 일관성 요구 사항에 따라 요청 단위로 이 정책을 재정의할 수 있습니다. 문서를 쿼리할 때 hello를 읽기 일관성 다음과 hello 인덱싱 hello 모음에 설정 하는 모드입니다. 이 "일치"에 대 한 hello 계정 일관성 정책을 따릅니다. 

## <a name="attachments-and-media"></a>첨부 파일 및 미디어
Cosmos DB toostore 이진 blob/미디어 Cosmos DB (계정당 최대 2gb) 또는 tooyour 직접 원격 미디어 스토어를 사용 하 여 있습니다. 또한, 첨부 파일 라는 특별 한 문서를 기준으로 미디어의 toorepresent hello 메타 데이터를 있습니다. Cosmos DB에 첨부 파일은 특수 (JSON) 문서 참조 hello 다른 위치에 저장 된 미디어/blob입니다. 첨부 파일은 hello 메타 데이터 (예: 위치, 작성자 등)의 원격 미디어 저장소에 저장 된 미디어를 캡처하는 특별 한 문서는 단순히입니다. 

책갈피, 등급, like/싫어하는 것 등 등 특정된 사용자의 전자책에 대 한 연결 된 주석을 포함 한 메타 데이터를 강조 표시 및 Cosmos DB toostore 잉크 주석을 사용 하는 소셜 읽기 응용 프로그램을 고려 하세요.   

* hello 자체 hello 책의 콘텐츠는 저장소에 저장 hello 미디어 하거나 원격 미디어 스토어 또는 Cosmos DB 데이터베이스 계정의 일부로 사용할 수 있습니다. 
* 응용 프로그램은 각 사용자의 메타데이터를 개별 문서로 저장할 수 있습니다. 예를 들어 book1에 대한 Joe의 메타데이터는 /colls/joe/docs/book1로 참조된 문서에 저장됩니다. 
* 첨부 파일 사용자의 특정된 책의 toohello 콘텐츠 페이지를 가리키는 hello 해당 문서 /colls/joe/docs/book1/chapter1 예를 들어 아래에 저장 됩니다 /colls/joe/docs/book1/chapter2 등입니다. 

위에 나열 된 hello 예제는 친숙 한 id tooconvey hello 리소스 계층 구조를 사용 합니다. 리소스는 고유한 리소스 id 통해 hello REST Api를 통해 액세스 됩니다. 

Cosmos DB에서 관리 되는 hello 미디어에 대 한 hello _media 속성 hello 첨부 파일의 URI로 hello 미디어를 참조 합니다. Cosmos DB는 hello 미해결 참조가 모두 삭제 됩니다 때 toogarbage 수집 hello 미디어를 확인 합니다. Cosmos DB는 자동으로 hello 새 미디어를 업로드할 때 hello 첨부 파일을 생성 하 고 hello _media toopoint toohello 새로 추가 된 미디어를 채웁니다. 사용자 (예: Azure 저장소, OneDrive, DropBox 등)가 관리 하는 원격 blob 저장소에 toostore hello 미디어를 선택 하면 tooreference hello 미디어 첨부 파일을 계속 사용할 수 있습니다. 이 경우 hello 첨부 파일 직접 만들고 해당 _media 속성을 채웁니다.   

다른 모든 리소스와 마찬가지로 첨부 파일 또는 만들 수 있습니다, 대체, 삭제, 읽기 쉽게 REST Api 또는 hello 클라이언트 Sdk 중 하나를 사용 하 여 열거 합니다. Hello 읽기 첨부 파일의 일관성 수준 문서와 같이 hello 데이터베이스 계정에 hello 일관성 정책을 따릅니다. 응용 프로그램의 데이터 일관성 요구 사항에 따라 요청 단위로 이 정책을 재정의할 수 있습니다. 첨부 파일을 쿼리할 때 hello를 읽기 일관성 다음과 hello 인덱싱 hello 모음에 설정 하는 모드입니다. 이 "일치"에 대 한 hello 계정 일관성 정책을 따릅니다. 
 

## <a name="users"></a>사용자
Cosmos DB 사용자는 사용 권한 그룹화를 위한 논리적 네임스페이스를 나타냅니다. Cosmos DB 사용자 id 관리 시스템 또는 미리 정의 된 응용 프로그램 역할에 tooa 사용자를 해당할 수 있습니다. Cosmos DB에 대 한 사용자는 단순히 추상화 toogroup을 데이터베이스 아래 사용 권한 집합을 나타냅니다.   

응용 프로그램에서 다중 테 넌 트를 구현 하기 위한 Cosmos db tooyour 실제 사용자 또는 응용 프로그램의 hello 테 넌 트가 해당 하는 사용자가 만들 수 있습니다. 해당 하는 다양 한 컬렉션, 문서, 첨부 파일 등을 통해 toohello 액세스 제어는 지정된 된 사용자에 대 한 권한을 만들 수 있습니다.   

Tooscale 사용자 증가와 응용 프로그램을 데이터에 다양 한 방법으로 tooshard 적용할 수 있습니다. 각 사용자를 다음과 같이 모델링할 수 있습니다.   

* 각 사용자 데이터베이스를 tooa 매핑됩니다.
* 각 사용자 tooa 컬렉션을 매핑합니다. 
* Toomultiple 사용자에 해당 하는 문서 tooa 전용 컬렉션을 이동 합니다. 
* Toomultiple 사용자에 해당 하는 문서 tooa 집합 컬렉션을 이동 합니다.   

선택한 hello 특정 분할 전략에 관계 없이 실제 사용자 Cosmos DB 데이터베이스 사용자로 모델링 수 있으며 세밀 하 게 세분화 된 권한을 tooeach 사용자에 연결할 수 있습니다.  

![사용자 컬렉션][3]  
**분할 전략 및 사용자 모델링**

다른 모든 리소스와 마찬가지로 Cosmos DB에는 사용자를 만들 수 있습니다, 대체, 삭제, 읽기 또는 REST Api 또는 hello 클라이언트 Sdk 중 하나를 사용 하 여 쉽게 열거 합니다. Cosmos DB는 항상 읽기 또는 사용자 리소스의 hello 메타 데이터를 쿼리 하는 강력한 일관성을 제공 합니다. 것 불과하며 여기에 포함 된 hello 사용 권한 중 하나에 액세스할 수 없다고는 사용자를 자동으로 삭제 되도록 합니다. Hello 사용 권한 할당량 hello hello 백그라운드에서 삭제 하는 hello 사용자의 일환으로 회수 하는 hello Cosmos DB, 경우에 hello 삭제 권한을 사용할 수 즉시 다시 toouse 있습니다.  

## <a name="permissions"></a>권한
액세스 제어 관점에서 데이터베이스 계정, 데이터베이스, 사용자, 사용 권한 등의 리소스는 관리 권한이 필요하기 때문에 *관리* 리소스로 간주됩니다. 다른 손 hello 컬렉션, 문서, 첨부 파일, 저장된 프로시저, 트리거를 포함 하 여 리소스를 hello 및 Udf 지정된 된 데이터베이스에서 범위가 한정 되 고 것으로 간주 *응용 프로그램 리소스*합니다. Hello 권한 부여 모델 정의 toohello 라는 두 가지 유형의 리소스 (관리자에 게 및 사용자)에 액세스 하는 hello 역할에 해당, 두 가지 유형의 *선택키가*: *마스터 키* 및 *리소스 키*합니다. hello 마스터 키 hello 데이터베이스 계정의 일부 이며 toohello 개발자 (또는 관리자)에 제공 되는 hello 데이터베이스 계정 프로 비전 합니다. 이 마스터 키 사용된 tooauthorize 액세스 tooboth 관리 및 응용 프로그램 리소스 사용 될 수 있다는 점에서 관리자 의미 체계를 있습니다. 리소스 키 액세스 tooa 수 있는 세분화 된 액세스 키를가 하는 반면, *특정* 응용 프로그램 리소스입니다. 따라서 hello hello 사용자 데이터베이스의 관계를 캡처할 않으며 hello 권한을 hello 사용자에 게 특정 리소스 (예:: 컬렉션, 문서, 첨부 파일, 저장된 프로시저, 트리거 또는 UDF).   

hello 유일한 방법은 tooobtain 리소스 키를 지정된 된 사용자 아래 사용 권한 리소스를 만드는 것입니다. 순서 toocreate에서 또는 사용 권한을 검색, hello 인증 헤더에 마스터 키를 제공 해야 합니다. 사용 권한 리소스 hello 리소스, 액세스 및 hello 사용자를 연결합니다. 사용 권한 리소스를 만든 후 hello 사용자 toopresent hello 연결된 리소스 키 순서 toogain 액세스 toohello 관련 리소스에만 필요 합니다. 따라서 리소스 키 hello 사용 권한 리소스의 압축 된 논리 표현으로 볼 수 있습니다.  

다른 모든 리소스와 마찬가지로 Cosmos DB에서 사용 권한을 만들 수 있습니다, 대체, 삭제, 읽기 또는 REST Api 또는 hello 클라이언트 Sdk 중 하나를 사용 하 여 쉽게 열거 합니다. Cosmos DB는 항상 읽기 또는 사용 권한의 hello 메타 데이터를 쿼리 하는 강력한 일관성을 제공 합니다. 

## <a name="next-steps"></a>다음 단계
[Cosmos DB 리소스와의 RESTful 상호 작용](https://msdn.microsoft.com/library/azure/mt622086.aspx)에서 HTTP 명령을 사용하여 리소스를 사용하는 방법을 알아봅니다.

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

