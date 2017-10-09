---
title: "hello 테이블 디자이너에 대 한 필터 문자열 aaaConstructing | Microsoft Docs"
description: "Hello 테이블 디자이너에 대 한 필터 문자열 생성"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a>테이블 디자이너 hello에 대 한 필터 문자열 생성
## <a name="overview"></a>개요
에 표시 되는 Azure 테이블의 데이터를 toofilter hello Visual Studio **테이블 디자이너**, 필터 문자열을 생성 하 고 hello 필터 필드에 입력 합니다. hello 필터 문자열 구문은 hello WCF 데이터 서비스에 의해 정의 됩니다 및 유사한 tooa SQL WHERE 절, 하지만 toohello HTTP 요청을 통해 테이블 서비스로 전송 됩니다. hello **테이블 디자이너** 핸들 적합 한 인코딩을, 원하는 속성 값에 따라서 toofilter hello, hello 속성 이름, 비교 연산자, 조건 값을 입력만 필요 하 고 hello의 부울 연산자 필터링 하는 필요에 따라 필드입니다. Hello 통해 URL tooquery hello 테이블을 생성 하는 경우와 마찬가지로 tooinclude hello $filter 쿼리 옵션 불필요 [저장소 서비스 REST API 참조](http://go.microsoft.com/fwlink/p/?LinkId=400447)합니다.

hello WCF Data Services 기반 hello로 [개방형 데이터 프로토콜](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Hello 필터 시스템 쿼리 옵션에 대 한 자세한 내용은 (**$filter**), 참조 hello [OData URI 규칙 사양](http://go.microsoft.com/fwlink/p/?LinkId=214806)합니다.

## <a name="comparison-operators"></a>비교 연산자
hello 다음과 같은 논리 연산자는 모든 유형에 대해 지원 속성:

| 논리 연산자 | 설명 | 필터 문자열의 예 |
| --- | --- | --- |
| eq |같음 |'Redmond'와 같은 도시 |
| gt |다음보다 큼 |20보다 큰 가격 |
| ge |보다 크거나 같은 너무|10보다 크거나 같은 가격 |
| lt |다음보다 적음 |20보다 적은 가격 |
| le |다음보다 적거나 같음 |100보다 적거나 같은 가격 |
| ne |다음과 같지 않음 |'London'과 같지 않은 도시 |
| and |and |200보다 적거나 같은 가격 및 3.5보다 큰 가격 |
| 또는 |또는 |3.5보다 적거나 같은 가격 또는 200보다 큰 가격 |
| not |not |not isAvailable |

필터 문자열을 생성할 때는 hello 다음 규칙은 중요 합니다.

* Hello 논리 연산자 toocompare 속성 tooa 값을 사용 합니다. 가능한 toocompare 속성 tooa 동적 값; 아닌지 참고 hello 식의 한 쪽은 상수 여야 합니다.
* Hello 필터 문자열의 모든 부분은 대/소문자를 구분 하지 않습니다.
* hello hello 상수 값 이어야 합니다 hello 필터 tooreturn 유효한 결과에서 hello 속성으로 동일한 데이터 형식입니다. 지원 되는 속성 형식에 대 한 자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://go.microsoft.com/fwlink/p/?LinkId=400448)합니다.

## <a name="filtering-on-string-properties"></a>문자열 속성 필터링
문자열 속성으로 필터링 할 때 hello 문자열 상수가 작은따옴표로 묶습니다.

에 나오는 예제에서는 필터에 따라 hello hello **PartitionKey** 및 **RowKey** ; 키가 아닌 추가 속성 속성 toohello 필터 문자열 추가할 수도 있습니다.

    PartitionKey eq 'Partition1' and RowKey eq '00001'

필수는 아니지만 각 필터 식을 괄호로 묶을 수 있습니다.

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

테이블 서비스 hello 와일드 카드 쿼리를 지원 하지 않습니다 및 지원 되지 않습니다 hello 테이블 디자이너에서에서 하거나 note 합니다. 그러나 원하는 접두사 hello에 비교 연산자를 사용 하 여 접두사 일치를 수행할 수 있습니다. hello 다음 예제에서는 엔터티를 반환 합니다 hello 문자 'A'로 시작 하는 LastName 속성:

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>숫자 속성 필터링
정수 또는 부동 소수점 숫자 toofilter 따옴표 없이 hello 번호를 지정 합니다.

이 예제는 값이 30보다 큰 Age 속성을 가진 모든 엔터티를 반환합니다.

    Age gt 30

같은 AmountDue 속성 값이 포함 된 모든 엔터티를 반환 하는이 예제 보다 작거나 같은 too100.25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>부울 속성 필터링
부울 값에 toofilter 지정 **true** 또는 **false** 인용 부호 제외 합니다.

hello 다음 예제에서는 반환 모든 엔터티가 너무 hello IsActive 속성이 설정 되어 있는**true**:

    IsActive eq true

Hello 논리 연산자 없이이 필터 식을 작성할 수도 있습니다. 다음 예제는 hello, hello 테이블 서비스는 모든 엔터티도 반환 IsActive가 **true**:

    IsActive

모든 엔터티 IsActive가 false 이면 사용할 수 없습니다 hello tooreturn 연산자:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>DateTime 속성 필터링
날짜/시간 값에 toofilter 지정 hello **datetime** 키워드와 작은따옴표로 hello date/time 상수입니다. 에 설명 된 대로 hello date/time 상수 결합 된 UTC 형식에서 이어야 합니다 [DateTime 속성 값 서식 지정](http://go.microsoft.com/fwlink/p/?LinkId=400449)합니다.

다음 예에서는 hello 여기서 hello CustomerSince 속성은 같은 tooJuly 10, 2008 엔터티를 반환 합니다.

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
