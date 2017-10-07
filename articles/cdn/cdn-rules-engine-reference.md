---
title: "CDN aaaAzure 규칙 엔진 참조 | Microsoft Docs"
description: "Azure CDN 규칙 엔진 일치 조건 및 기능에 대한 참조 설명서"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Azure CDN 규칙 엔진
이 항목에 대 한 자세한 설명을 사용할 수 있는 일치 조건을 hello 및 기능에 대 한 Azure 네트워크 CDN (콘텐츠 배달)에서는 [규칙 엔진](cdn-rules-engine.md)합니다.

hello HTTP 규칙 엔진 디자인 된 toobe hello 최종 용도 특정 유형의 요청에는 hello CDN에 의해 처리 됩니다.

**일반적인 사용**:

- 사용자 지정 캐시 정책을 재정의하거나 정의합니다.
- 중요한 콘텐츠에 대한 요청에 대해 보안을 유지하거나 거부합니다.
- 요청을 리디렉션합니다.
- 사용자 지정 로그 데이터를 저장합니다.

## <a name="terminology"></a>용어
규칙의 hello 사용을 통해 정의 됩니다 [ **조건식**](cdn-rules-engine-reference-conditional-expressions.md), [ **일치**](cdn-rules-engine-reference-match-conditions.md), 및 [  **기능**](cdn-rules-engine-reference-features.md)합니다. 이러한 요소는 hello 다음 그림에에서 강조 표시 됩니다.

 ![CDN 일치 조건](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>구문

hello 방식으로 특수 문자를 처리 됩니다 따라 toohow 일치 조건 또는 기능 핸들 텍스트 값에 따라 달라 집니다. 일치 조건 또는 기능 hello 같은 방법으로 다음 중 하나에서 텍스트를 해석할 수 있습니다.

1. [**리터럴 값**](#literal-values) 
2. [**와일드카드 값**](#wildcard-values)
3. [**정규식**](#regular-expressions)

### <a name="literal-values"></a>리터럴 값
리터럴 값으로 해석 되는 텍스트와 일치 해야 하는 hello 값의 일부로 hello % 기호의 hello 예외와 함께 모든 특수 문자를 처리 합니다. 즉, 리터럴 일치 조건 너무 세트`\'*'\` 하는 정확한 값 했을 때만 충족 됩니다 (즉, `\'*'\`)를 찾을 수 있습니다.
 
백분율 기호를 사용 하는 tooindicate URL 인코딩 (예: `%20`).

### <a name="wildcard-values"></a>와일드카드 값
텍스트는 와일드 카드 값으로 해석 되는 추가적인 의미 toospecial 문자를 할당 합니다. 다음 표에서 hello 문자 집합을 추적 하는 hello 됩니다 해석 하는 방법을 설명 합니다.

문자 | 설명
----------|------------
\ | 백슬래시는 사용 되는 tooescape이이 테이블에 지정 된 hello 문자입니다. 백슬래시를 이스케이프 해야 하는 hello 특수 문자 바로 앞 지정 되어야 합니다.<br/>예를 들어 hello 구문 다음에 별표를 이스케이프:`\*`
% | 백분율 기호를 사용 하는 tooindicate URL 인코딩 (예: `%20`).
* | 별표는 하나 이상의 문자를 나타내는 와일드카드입니다.
공백 | 공백 문자 일치 조건을 지정 하는 hello 중 하나라도 충족 될 수를 나타내는 값 또는 패턴과 합니다.
'value' | 작은따옴표는 특별한 의미가 없습니다. 그러나 단일 따옴표 집합이 사용 됩니다 tooindicate 값 이어야 하는 리터럴 값으로 처리 합니다. 다음 방법으로 hello에 사용할 수 있습니다.<br><br/>-허용 일치 조건 toobe 충족 hello hello 비교 값의 모든 부분 일치 항목 값을 지정 합니다.  예를 들어 `'ma'` hello 문자열을 다음 중 하 나와 일치 합니다. <br/><br/>/business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/business/template.**ma**p<br /><br />-리터럴 문자로 지정 된 특수 문자 toobe가 있습니다. 예를 들어 공백 문자를 작은따옴표 쌍으로 묶어 리터럴 공백 문자를 지정할 수 있습니다(즉, `' '` 또는 `'sample value'`).<br/>-지정 된 빈 값 toobe가 있습니다. 작은따옴표 쌍(예: '')을 지정하여 빈 값을 지정합니다.<br /><br/>**중요:**<br/>-Hello 값에는 와일드 카드를 지정 하는 경우 다음 자동으로 간주 리터럴 값입니다. 이 필요한 toospecify 작은따옴표 집합 되지 않은 것을 의미 합니다.<br/>- 백슬래시가 이 표의 다른 문자를 이스케이프하지 않으면 작은따옴표로 묶어서 지정할 때 무시됩니다.<br/>-다른 방식으로 toospecify 특수 문자를 리터럴 문자로 tooescape는 백슬래시를 사용 하 여 (즉, `\`).

### <a name="regular-expressions"></a>정규식

정규식은 텍스트 값 내에서 검색될 패턴을 정의합니다. 정규식 표기법 특별 한 의미 tooa 다양 한 기호를 정의합니다. hello 다음 표에 방법을 특수 문자 일치 조건과 정규식을 지 원하는 기능으로 처리 됩니다.

특수 문자 | 설명
------------------|------------
\ | 백슬래시 이스케이프 hello 문자 hello 그 다음에 오는 합니다. 이렇게 하면 해당 문자 toobe 정규식 의미에서 수행 하는 대신 리터럴 값으로 처리 됩니다. 예를 들어 hello 구문 다음에 별표를 이스케이프:`\*`
% | 백분율 기호의 hello 의미의 사용법에 따라 달라 집니다.<br/><br/> `%{HTTPVariable}`: 이 구문은 HTTP 변수를 식별합니다.<br/>`%{HTTPVariable%Pattern}`:이 구문은 백분율 기호 tooidentify HTTP 변수 및 구분 기호로 사용합니다.<br />`\%`: 리터럴 값 또는 tooindicate URL 인코딩용으로 사용 하는 toobe 허용 백분율 기호를 이스케이프 합니다. (예: `\%20`).
* | 별표 앞에 0 번 이상 일치 하는 문자 toobe hello 수 있습니다. 
공백 | 공백 문자는 일반적으로 리터럴 문자로 취급됩니다. 
'value' | 작은따옴표는 리터럴 문자로 처리됩니다. 작은따옴표 쌍은 특별한 의미가 없습니다.


## <a name="next-steps"></a>다음 단계
* [규칙 엔진 일치 조건](cdn-rules-engine-reference-match-conditions.md)
* [규칙 엔진 조건식](cdn-rules-engine-reference-conditional-expressions.md)
* [규칙 엔진 기능](cdn-rules-engine-reference-features.md)
* [Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의](cdn-rules-engine.md)
* [Azure CDN 개요](cdn-overview.md)
