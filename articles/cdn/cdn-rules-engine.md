---
title: "hello Azure CDN 규칙 엔진을 사용 하 여 HTTP aaaOverride 동작 | Microsoft Docs"
description: "hello 규칙 엔진 toocustomize를 캐싱 정책을 정의 하 고 HTTP 헤더를 수정 하는 특정 유형의 콘텐츠를 차단 hello 배달와 같은 HTTP 요청 Azure CDN에서 처리 하는 방법이 있습니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Hello Azure CDN 규칙 엔진을 사용 하 여 HTTP 동작을 재정의
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>개요
hello 규칙 엔진에서는 특정 유형의 콘텐츠를 배달 hello 차단 캐싱 정책을 정의 HTTP 헤더를 수정 등으로 HTTP 요청 처리 되는 방법을 toocustomize가 있습니다.  이 자습서에서는 캐싱 동작 CDN 자산 hello는 규칙을 만들 바뀝니다 보여 줍니다.  Hello에서 사용할 수 있는 비디오 콘텐츠도는 "[참조](#see-also)" 섹션.

   > [!TIP] 
   > 자세히 참조 toohello 구문에 대 한 참조 [규칙 엔진 참조](cdn-rules-engine-reference.md)합니다.
   > 


## <a name="tutorial"></a>자습서
1. Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
2. Hello 클릭 **HTTP 큰** 탭, **규칙 엔진**합니다.
   
    새 규칙에 대한 옵션이 표시됩니다.
   
    ![CDN 새 규칙 옵션](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > hello 나열 된 여러 규칙의 영향을 줍니다 처리 됩니다. 후속 규칙 이전 규칙에 지정 된 hello 동작을 재정의할 수 있습니다.
   > 
   > 
3. Hello에 이름을 입력 **이름 / 설명** 텍스트 상자에 붙여넣습니다.
4. Hello 규칙을 적용할 요청 hello 유형을 식별 합니다.  기본적으로 hello **항상** 일치 조건을 선택 합니다.  이 자습서에서는 **항상** 을 사용하므로 선택된 상태 그대로 두면 됩니다.
   
   ![CDN 일치 조건](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Hello 드롭다운에서 사용할 수 있는 조건은 다양 한 유형의 일치 합니다.  왼쪽의 일치 조건 hello hello 파란색 정보 아이콘 toohello 클릭 하면 자세히 hello 현재 선택 된 조건을 설명 합니다.
   > 
   >  자세히 조건 식의 전체 목록을 hello에 대 한 참조 [규칙 엔진 조건식](cdn-rules-engine-reference-match-conditions.md)합니다.
   >  
   > 일치 조건 자세히의 전체 목록을 hello에 대 한 참조 [규칙 엔진의 일치 조건을](cdn-rules-engine-reference-match-conditions.md)합니다.
   > 
   > 
5. Hello 클릭  **+**  너무 단추 옆**기능** tooadd 새로운 기능입니다.  Hello 왼쪽에 hello 드롭다운에서 선택 **Force 내부 Max-age**합니다.  나타나는 hello 텍스트 상자에 입력 **300**합니다.  Hello 나머지 기본값을 그대로 둡니다.
   
   ![CDN 기능](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > 으로 일치 조건으로 hello 파란색 정보 아이콘 toohello 클릭 하면 남아 hello의 새 기능에는이 기능에 대 한 세부 정보가 표시 됩니다.  경우 hello **Force 내부 Max-age**, hello 자산을 재정의 하는 것 **캐시 제어** 및 **Expires** 헤더 toocontrol hello CDN 가장자리 노드 hello 새로 됩니다 hello 원점에서 자산입니다.  300 초의 예제는 hello CDN 가장자리 노드는 hello 자산 hello 자산 원본을 새로 고치기 전에 5 분 동안 캐시를 의미 합니다.
   > 
   > 기능을 자세히 설명의 전체 목록을 hello에 대 한 참조 [규칙 엔진 기능 정보](cdn-rules-engine-reference-features.md)합니다.
   > 
   > 
6. Hello 클릭 **추가** 단추 toosave hello에 대 한 새 규칙입니다.  이제 hello 새 규칙에는 승인 대기 중입니다. Hello 상태에서 변경 됩니다. 승인 되 면 **보류 중인 XML** 너무**활성 XML**합니다.
   
   > [!IMPORTANT]
   > 규칙 변경 내용을 hello CDN 통해 too90 분 toopropagate를 차지할 수 있습니다.
   > 
   > 

## <a name="see-also"></a>참고 항목
* [Azure CDN 개요](cdn-overview.md)
* [규칙 엔진 참조](cdn-rules-engine-reference.md)
* [규칙 엔진 일치 조건](cdn-rules-engine-reference-match-conditions.md)
* [규칙 엔진 조건식](cdn-rules-engine-reference-conditional-expressions.md)
* [규칙 엔진 기능](cdn-rules-engine-reference-features.md)
* [Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의](cdn-rules-engine.md)
* [Azure Fridays: Azure CDN의 강력하고 새로운 프리미엄 기능](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (동영상)