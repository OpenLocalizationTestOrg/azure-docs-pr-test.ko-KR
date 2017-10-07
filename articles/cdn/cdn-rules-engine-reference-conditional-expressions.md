---
title: "CDN aaaAzure 규칙 엔진 조건식 | Microsoft Docs"
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
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Azure CDN 규칙 엔진 조건식
이 항목에 자세히 설명 조건식 hello에 대 한 Azure 네트워크 CDN (콘텐츠 배달)에서는 [규칙 엔진](cdn-rules-engine.md)합니다.

규칙의 첫 번째 부분 hello는 hello 조건식입니다.

조건식 | 설명
-----------------------|-------------
IF | IF 식을 규칙의 첫 번째 문은 hello의 일부인 항상 합니다. 다른 모든 조건식과 마찬가지로 이 IF 문은 일치와 관련이 있어야 합니다. 추가 조건 식이 없는 정의한 경우 속성이이 일치 기능 집합이 적용 된 tooa 요청 수 전에 충족 해야 하는 hello 조건을 결정 합니다.
AND IF | 및 IF 식은 다음 조건부 식: IF, 및 IF 유형의으로 hello 후만 추가할 수 있습니다. 이 초기 IF 문이 hello에 대 한 충족 해야 하는 다른 조건 임을 나타냅니다.
ELSE IF| ELSE IF 식을 기능 특정 toothis ELSE IF 문 집합을 수행 하기 전에 충족 해야 하는 대체 상태를 지정 합니다. ELSE IF 문의 hello 있으면 hello hello 이전 문의 끝을 나타냅니다. hello만 조건식 ELSE IF 문 다음에 배치 될 수 있습니다 하는 또 다른 ELSE IF 문입니다. 즉, ELSE IF 문을 사용 하는 toospecify toobe 충족 된 단일 추가 조건에만 사용할 수 있습니다.

**예**: ![CDN 일치 조건](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > 후속 규칙 이전 규칙에 지정 된 hello 동작을 재정의할 수 있습니다. 예: catch-all 규칙은 토큰 기반 인증을 통해 모든 요청을 보호합니다. 바로 아래에 다른 규칙을 만들 수 있습니다 toomake 특정 유형의 요청에 대 한 예외입니다.

### <a name="next-steps"></a>다음 단계
* [Azure CDN 개요](cdn-overview.md)
* [규칙 엔진 참조](cdn-rules-engine-reference.md)
* [규칙 엔진 일치 조건](cdn-rules-engine-reference-match-conditions.md)
* [규칙 엔진 기능](cdn-rules-engine-reference-features.md)
* [Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의](cdn-rules-engine.md)
