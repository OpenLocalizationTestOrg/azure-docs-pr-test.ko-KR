---
title: "NoSQL 데이터베이스에 대 한 문서 데이터 aaaModeling | Microsoft Docs"
description: "NoSQL 데이터베이스의 데이터 모델링에 대해 알아봅니다."
keywords: "데이터 모델링"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a>NoSQL 데이터베이스의 문서 데이터 모델링
Azure Cosmos DB와 같은 스키마 없는 데이터베이스를 사용 하면 매우 쉽게 하는 동안 계속 사용 해야 하는 tooembrace 변경 tooyour 데이터 모델 잠시 데이터에 대해 생각 합니다. 

데이터가 어떻게 저장 toobe? 응용 프로그램 하락 tooretrieve 및 쿼리 데이터는 어떻게 합니까? 응용 프로그램 부하가 읽기 또는 쓰기 중 어디에 집중되어 있는가? 

이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.

* 문서 데이터베이스에서 문서는 무엇인가?
* 데이터 모델링은 무엇이고 어떻게 사용해야 하는가? 
* 문서 데이터베이스 다른 tooa 관계형 데이터베이스에서 데이터 모델링은 어떻게 합니까?
* 비관계형 데이터베이스에서 데이터 관계는 어떻게 표현하는가?
* 데이터를 포함 하는 경우 및 때 toodata 연결할 수 있나요?

## <a name="embedding-data"></a>데이터 포함
Azure Cosmos DB와 같은 문서 저장소에 데이터의 모델링을 시작 하면 tootreat으로 엔터티를 시도 **자체 포함 된 문서** JSON에서 표시 합니다.

자세한 설명을 시작하기 전에 먼저 이전 단계로 돌아가서 관계형 데이터베이스에서 모델링을 수행하는 방법에 대해 살펴보겠습니다. hello 다음 예제에서는 관계형 데이터베이스에는 사용자 수 저장 하는 방법을 

![관계형 데이터베이스 모델](./media/documentdb-modeling-data/relational-data-model.png)

에서는 언급 한 년 toonormalize 처럼 한 관계형 데이터베이스와 함께 작업 하는 경우 정규화, 정규화 합니다.

데이터 정규화에 일반적으로, 사용자 등의 엔터티를 차지 하 고 데이터의 toodiscrete 나누어에서 분석 해 서 작업이 포함 됩니다. Hello 위의 예에서 사람이 여러 주소 레코드 뿐만 아니라 여러 연락처 세부 레코드가 있을 수 있습니다. 여기에서는 한 단계 더 나가서 유형과 같은 공통 필드를 추출하여 연락처 세부 정보를 보다 세분화합니다. 주소와 마찬가지로 각 레코드에는 *홈* 또는 *비즈니스*와 같은 유형에 포함됩니다. 

데이터 정규화이 너무 프레미스 안내 hello**중복 데이터를 저장 하지 않도록** 각 기록 및 아니라 toodata를 참조 합니다. 이 예제에서는 모든 연락처 세부 정보 및 주소와 함께 개인 tooread toouse 조인 tooeffectively 집계에서 데이터 런타임에 해야 합니다.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

연락처 세부 정보 및 주소를 사용해서 단일 사용자를 업데이트하려면 여러 개별 테이블 간의 쓰기 작업이 필요합니다. 

에 모델링 방법을 동일 hello 보겠습니다 이제 문서 데이터베이스의 자체 포함 된 엔터티로 데이터입니다.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

Hello 방식을 위의 이제는 사용 하 여 **정규화 되지 않은** 개인 레코드 hello 여기서 म **포함** 모든 hello 예: 연락처 세부 정보 및 주소 tooa 단일 toothis 사용자와 관련 된 정보 JSON 문서입니다.
또한, 우리는 제한 되지 때문에 tooa 해결 스키마는 hello 유연성 toodo 등 다양 한 도형 연락처 세부 정보를 완전히 필요 합니다. 

읽기 작업을 단일 컬렉션에 대해 및 단일 문서에 대 한 단일 되었습니다 hello 데이터베이스에서 전체 개인 레코드를 검색 합니다. 연락처 세부 정보 및 주소로 사용자 레코드를 업데이트하는 작업도 단일 문서에 대해 단일 쓰기 작업을 수행하는 것과 같습니다.

데이터를 비 정규화 하 여 작업이 더 적게 쿼리 및 업데이트가 toocomplete 일반적인 응용 프로그램 tooissue 할 수 있습니다. 

### <a name="when-tooembed"></a>때 tooembed
일반적으로 다음과 같은 경우에 포함된 데이터 모델을 사용합니다.

* 엔터티 간에 **포함** 관계가 있습니다.
* 엔터티 사이에 **일 대 몇(one-to-few)** 의 관계가 있습니다.
* 포함된 데이터가 **자주 변경**되지 않습니다.
* 포함된 데이터가 **바인딩 없이**증가하지 않습니다.
* 가 포함 된 데이터는 **정수 계열** 문서에서 toodata 합니다.

> [!NOTE]
> 일반적으로 비정규화된 데이터 모델은 **읽기** 성능이 더 뛰어납니다.
> 
> 

### <a name="when-not-tooembed"></a>때 tooembed 하지
Hello 경험 문서 데이터베이스에서 toodenormalize 모든 항목은 하 tooa 단일 문서에 모든 데이터를 포함 하는 동안 피해 야 하는 toosome 상황 발생할 수 있습니다.

다음 JSON 코드 조각을 예로 들어 보겠습니다.

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

이 코드 조각은 일반적인 블로그 또는 CMS 시스템을 모델링할 때 나타날 수 있는 포함된 주석이 있는 포스트 엔터티를 나타낼 수 있습니다. hello 문제가이 예제는 해당 hello 주석 배열이 **unbounded**, 단일 게시물을 좋아하고 게시물 점이 주석의 없습니다 (실제) 제한이 toohello 수 있다는 것을 의미 합니다. Hello 문서 hello 크기가 상당히 커져서 서 문제가 드라이브가 될 것이 있습니다.

Hello 기능 tootransmit hello 데이터 읽기 뿐만 아니라 hello 유선을 통해 문서 hello의 hello 크기 만큼 증가 하 고 업데이트 hello 문서의 소수 자릿수에 영향을 받습니다.

이 경우 더 나은 tooconsider hello 모델을 따르는 것입니다.

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

이 모델에 hello 3 가장 최근의 주석 hello에 포함 된이 게시는 고정을 가진 배열인 자체 시간입니다. hello 기타 주석은 그룹화 100 주석의 toobatches에 되며 별도 문서에 저장 합니다. hello hello 일괄 처리 크기는 가상의 응용 프로그램을 허용 하므로 hello 사용자 tooload 100 설명을 한 번에 100으로 선택 되었습니다.  

데이터를 포함 하지 않은 것이 좋습니다 경우 hello 포함 하는 경우에 데이터 문서에서 자주 사용 하 고 자주 변경 됩니다. 

다음 JSON 코드 조각을 예로 들어 보겠습니다.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

이 예제는 한 사용자의 주식 포트폴리오를 나타낼 수 있습니다. Tooeach 포트폴리오 문서의 tooembed hello 주식 정보를 했습니다. 관련된 데이터는 주식 거래 응용 프로그램을 같은 자주 변경 되는 환경에서 자주 변경 되는 데이터를 포함 하려고 toomean 주식 매도 된 때마다 각 포트폴리오 문서 지속적으로 업데이트 하 합니다.

*zaza* 주식은 하루에도 수백 번 거래될 수 있으며 수천 명의 사용자 포트폴리오에 *zaza* 주식이 포함되어 있을 수 있습니다. 위의 hello와 같은 데이터 모델과 함께 것은 tooupdate 많은 포트폴리오 문서 상태일 때 잘 확장 되지 않습니다 tooa 시스템 선행 매일 여러 번 합니다. 

## <a id="Refer"></a>데이터 참조
따라서 데이터 포함 방식이 많은 경우에 효과적일 수 있지만, 데이터 비정규화로 인해 얻는 이득보다 잃게 되는 손실이 큰 경우도 있다는 것을 잘 알 수 있습니다. 그러면 이제 무엇을 해야 할까요? 

관계형 데이터베이스는 엔터티 간의 관계를 만들 수 있는 hello 유일한 공간 없습니다. 문서 데이터베이스에 실제로 다른 문서에서 toodata와 관련 한 문서에서 정보를 사용할 수 있습니다. 이제 I am 하지 지원 하 고 1 분도 Azure Cosmos DB에 더 적합 한 tooa 관계형 데이터베이스 또는 다른 문서 데이터베이스 시스템을 구축 했습니다 있지만 간단한 관계 만족 하는 매우 유용할 수 있습니다. 

Hello JSON 아래 toohello 재고 항목을 포함 하는 대신 hello 포트폴리오에 이라고 하지만 앞에서 스톡 포트폴리오의 toouse hello 예제를 선택 했습니다. 이 경우, hello 재고 항목 업데이트 toobe 필요한 hello 일 hello만 문서를 통해 자주 변경 되 면 hello 단일 스톡 문서 됩니다. 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


즉시 단점은 toothis 접근 방식을 통해 않은 경우에 응용 프로그램 개인의 포트폴리오;을 표시할 때 열리는 각 주식의 대 한 필요한 tooshow 정보 이 경우 해야 toomake 데이터베이스 tooload hello 정보에 대 한 여러의 트립을 toohello 스톡 각 문서에 대 한 합니다. 여기 hello 하루 종일 자주 발생 하지만 읽기이 특정 시스템의 hello 성능에 큰 영향을 미칠 작업 hello에 손상에 쓰기 작업의 의사 결정 tooimprove hello 효율성을 만들었습니다.

> [!NOTE]
> 정규화 된 데이터 모델 **더 왕복을 요구할 수** toohello 서버입니다.
> 
> 

### <a name="what-about-foreign-keys"></a>외래 키의 경우는 어떻게 될까요?
있기 때문에 현재 제약 조건의 개념이 없으므로, 외래 키 또는 그렇지는 간 문서 관계 문서에서 사용 하는 효율적인 "취약 한 연결" 및 hello 데이터베이스 자체가 확인 하지 않습니다. 문서 참조 데이터 hello tooensure 원하는 tooactually 없으면 필요한 toodo이 응용 프로그램 또는 서버 쪽 트리거 또는 저장된 프로시저 Azure Cosmos db hello 사용을 통해.

### <a name="when-tooreference"></a>때 tooreference
일반적으로 정규화된 데이터 모델은 다음과 같은 경우에 사용합니다.

* **일대다** 관계를 나타내는 경우
* **다대다** 관계를 나타내는 경우
* 관련 데이터가 **자주 변경**되는 경우
* 참조 데이터가 **바인딩되지 않는**경우

> [!NOTE]
> 일반적으로 정규화에서는 **쓰기** 성능이 더 뛰어납니다.
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>Hello 관계를 설정 하는 위치
hello 관계의 hello 증가 문서 toostore hello 참조 내에서 결정 하는 데 도움이 됩니다.

Hello 아래 게시자 및 설명서를 모델링 하는 JSON 표시 합니다.

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

게시자 별 hello 책 hello 수 제한 증가와 작을 경우에 hello 게시자 문서 안의 hello 책 참조를 저장 한 다음 유용할 수 있습니다. 그러나 hello 게시자 당 책 수를 제하지 없는 경우 다음이 데이터 모델은 될 toomutable, 배열, 위의 hello 예제 게시자 문서 처럼 증가. 

비트 작업만 전환는 여전히 나타내는 동일한 데이터를 하지만 이제 hello 모델의 결과 방지 이러한 큰 변경 가능한 컬렉션 합니다.

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

위 예제는 hello에서 삭제 한 우리 hello hello 게시자 문서에 바인딩되지 않은 컬렉션입니다. 대신는 한 각 책 문서에서 참조 toohello 게시자입니다.

### <a name="how-do-i-model-manymany-relationships"></a>다대다 관계는 어떻게 모델링할 수 있을까요?
관계형 데이터베이스에서 *다대다* 관계는 다른 테이블의 레코드를 단순히 하나로 조인하는 조인 테이블을 사용해서 모델링되는 경우가 많습니다. 

![테이블 조인](./media/documentdb-modeling-data/join-table.png)

로드할된 tooreplicate hello 사용 하 여 동일한 작업에 설명 및 다음과 비슷한 toohello 다음 데이터 모델을 생성할 수 있습니다.

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

이러한 모델도 작동은 가능합니다. 그러나 작성자의 설명서를 로드 하거나 책 저자 함께 로드 항상 필요 hello 데이터베이스에 대해 두 개 이상의 추가 쿼리 합니다. 한 쿼리에서 toohello 문서와 다른 쿼리 toofetch hello 실제 문서 조인 된 결합 합니다. 

이 조인 테이블이 수행하는 작업이 두 가지 데이터를 하나로 묶는 작업뿐이라면 이를 완전히 삭제할 수도 있을 것입니다.
Hello 다음 사항을 고려 합니다.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

이제 작성자 있으면 즉시 여부를 확인 하는 설명서를 작성 한을 반대로 책 문서 로드를 썼 hello 작성자의 hello id 확인 합니다. 서버 hello 수를 줄입니다 hello 조인 테이블에 대 한 중간 쿼리를 저장 하는이 응용 프로그램에 toomake 라운드트립 합니다. 

## <a id="WrapUp"></a>하이브리드 데이터 모델
지금까지 데이터 포함(또는 비정규화)과 참조(또는 정규화)에 대해 살펴봤습니다. 이러한 데이터 포함과 참조는 위에서 살펴본 것처럼 각각 장점과 단점을 갖고 있습니다. 

해당 하지 않는 항상 toobe 하거나 했거나를 하지 않는 약간를 무서 toomix 작업 수입니다. 

응용 프로그램의 특정 사용 패턴 및 사용할 수는 있지만 함께 포함 된 작업 부하에 따라 및 참조 되는 데이터는 것이 좋습니다 수 더 적은 수의 서버와 겹치는 toosimpler 응용 프로그램 논리 왕복 유지 하면서도 성능이 어느 정도 .

Hello를 JSON을 따르는 것이 좋습니다. 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

여기 했습니다 (주로) 따랐습니다 hello 포함 된 모델, 여기서 다른 엔터티에서 데이터 hello 최상위 문서에 포함 되어 있지만 다른 데이터를 참조 합니다. 

Hello 책 문서를 보면 몇 가지 볼 수 있습니다 작성자의 hello 배열에서 살펴볼 때 필드 흥미로운 합니다. 한 *id* hello 필드인 toorefer 백 tooan 만든 문서, 정규화 된 모델 했지만 다음에서 표준 방식 또한 사용 필드에 사용할 *이름* 및 *thumbnailUrl*. म 수 했습니다 구축할와 *id* hello 응용 프로그램 tooget 필요한 추가 정보 "링크" hello를 사용 하 여 hello 각각 만든 문서에서 유지 되었지만 응용 프로그램 hello 작성자의 이름을 표시 하기 때문에 대 한 모든도 서 표시 된 축소판 그림 수 저장 책 당 왕복 toohello 서버 목록에 비 정규화 하 여 **일부** hello 만든이의 데이터입니다.

물론, hello 저자의 이름이 변경 되었거나 해당 사진 tooupdate 원했습니다는 있는지 toogo 업데이트 만으로는 모든도 서는 적이 게시 되었지만 작성자 이름, 자주 변경 되지 않도록 하는 hello 가정에 따라 샘플 응용 프로그램에서는 이것은 허용 되는 디자인 의사 결정 합니다.  

Hello 예제는 **미리 집계를 계산** toosave 읽기 작업에 대 한 처리 비용이 많이 드는 값입니다. Hello 예제 hello 작성자 문서에 포함 된 hello 데이터 중 일부는 데이터 실행 시 계산입니다. 작성 되는 책 문서가 새 책을 게시할 때마다, **및** hello countOfBooks 필드에 특정 한 만든 대 한 책 문서 hello 수에 따라 tooa 계산 된 값으로 설정 되어 있습니다. 이 최적화 좋을 읽기 많은 시스템에서 toodo 계산 순서 toooptimize 읽기에 대 한 쓰기 중에 허용 수는 위치입니다.

Azure Cosmos DB 지원 하기 때문에 미리 계산 된 필드를 사용 하 여 모델을 가능한 이루어집니다 기능 toohave hello **다중 문서 트랜잭션**합니다. 많은 NoSQL 저장소는 문서 간에 트랜잭션을 수행 하 고 따라서 "항상 모든 항목"을 포함 toothis 제한 인해 같은 디자인 관련 결정을 대표 수 없습니다. Azure Cosmos DB에서는 서버 쪽 트리거 또는 저장 프로시저를 사용해서 ACID 트랜잭션 내에서 책을 삽입하고 저자를 업데이트할 수 있습니다. 그렇지 않으면 이제 **가** tooembed tooone의 모든 개체 데이터의 일관성이 유지 되는지 정당한 toobe 문서.

## <a name="NextSteps"></a>다음 단계
이 문서에서 가장 큰 자 hello는 toounderstand 같이 현재까지 데이터 모델링 스키마가 없는 환경에서이 중요 합니다. 

방금 없는 단 하나의 방식은 toorepresent 화면에 데이터의 일부 이면은 단 하나의 방식은 toomodel 없는 데이터. Toounderstand 응용 프로그램 및 해야 생성 됩니다을 소비 하는 방법과 hello 데이터를 처리 합니다. 그런 다음 hello 중 일부를 적용 하 여 여기서 설명 지침은 응용 프로그램의 hello 즉시 요구 사항을 해결 하는 모델을 만드는 방법에 대해 설정할 수 있습니다. 응용 프로그램 toochange을 할 때에 변경 하 고 데이터 모델에 따라 쉽게 발전할 하는 스키마 없는 데이터베이스 tooembrace의 hello 유연성을 활용할 수 있습니다. 

Azure Cosmos DB에 대해 자세히 toolearn toohello 서비스 참조 [설명서](https://azure.microsoft.com/documentation/services/cosmos-db/) 페이지. 

toounderstand tooshard 여러 파티션에서 데이터 참조 어떻게 너무[Azure Cosmos DB의 데이터를 분할](documentdb-partition-data.md)합니다. 
