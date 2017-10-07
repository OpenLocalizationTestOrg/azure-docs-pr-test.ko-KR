---
title: "쿼리 문자열-프리미엄을 사용한 Azure CDN 캐싱 동작 aaaControl | Microsoft Docs"
description: "Azure CDN 쿼리 문자열 캐싱 방법을 파일은 쿼리 문자열을 포함 하는 경우 캐시 toobe 컨트롤입니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어 - Premium
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [Verizon의 Azure CDN Premium](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>개요
쿼리 문자열 캐싱 방법을 파일은 쿼리 문자열을 포함 하는 경우 캐시 toobe 컨트롤입니다.

> [!IMPORTANT]
> hello Standard 및 Premium CDN 제품은 hello 같은 쿼리 문자열 캐싱 기능 하지만 hello 사용자 인터페이스 다릅니다.  이 문서에는 hello 인터페이스에 설명 **Verizon에서 Azure CDN Premium**합니다.  **Akamai의 Azure CDN Standard** 및 **Verizon의 Azure CDN Standard**를 사용한 쿼리 문자열 캐싱에 대해서는 [쿼리 문자열이 포함된 CDN 요청의 캐싱 동작 제어](cdn-query-string.md)를 참조하세요.
> 
> 

다음 세 가지 모드를 사용할 수 있습니다.

* **표준 캐시**: hello 기본 모드입니다.  hello CDN 가장자리 노드 hello 첫 번째 요청 및 캐시 hello 자산에 hello 요청자 toohello 원점에서 hello 쿼리 문자열을 전달 합니다.  Hello 가장자리 노드에서 처리 되는 해당 자산에 대 한 모든 후속 요청은 캐시 된 자산 hello 만료 될 때까지 hello 쿼리 문자열을 무시 합니다.
* **no 캐시**:이 모드에서는 쿼리 문자열을 사용 하 여 요청에 hello CDN 가장자리 노드에서 캐시 되지 않습니다.  hello 가장자리 노드 hello 원본에서 직접 hello 자산을 검색 하 고 각 요청과 함께 toohello 요청자에 게 전달 합니다.
* **unique-cache**: 이 모드는 쿼리 문자열이 포함된 각 요청을 자체 캐시를 가진 고유한 자산으로 처리합니다.  예를 들어 hello 출처에 대 한 요청에 대 한 응답을 hello *foo.ashx?q=bar* hello 가장자리 노드에 캐시 되 고 후속 캐시의 해당 동일한 쿼리 문자열로 반환 합니다.  에 대 한 요청 *foo.ashx?q=somethingelse* toolive 자체 시간과 함께 별도 자산으로 캐시 합니다.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Premium CDN 프로필에 대한 쿼리 문자열 캐싱 설정 변경
1. Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
2. 마우스 포인터를 놓고 hello **HTTP 큰** 누른 마우스 포인터를 놓고 hello **캐시 설정** 플라이 아웃입니다.  **Query-String Caching**(쿼리 문자열 캐싱)을 클릭합니다.
   
    쿼리 문자열 캐싱 옵션이 표시됩니다.
   
    ![CDN 쿼리 문자열 캐싱 옵션](./media/cdn-query-string-premium/cdn-query-string.png)
3. 선택한 후 클릭 hello **업데이트** 단추입니다.

> [!IMPORTANT]
> hello CDN 통해 hello 등록 toopropagate 시간이 걸립니다 대로 hello 설정 변경 수 즉시 표시 되지 않습니다.  <b>Verizon의 Azure CDN</b> 프로필의 경우 일반적으로 90분 이내에 전파가 완료되지만 더 오래 소요될 수도 있습니다.
> 
> 

