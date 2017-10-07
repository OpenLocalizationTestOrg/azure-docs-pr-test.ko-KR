---
title: "Azure CDN 끝점에 부하 aaaPre 자산 | Microsoft Docs"
description: "Toopre 부하 Azure CDN 끝점에서 콘텐츠를 캐시 하는 방법을 알아봅니다."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Azure CDN 끝점에 자산 미리 로드
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

기본적으로 요청되었으므로 자산이 먼저 캐시됩니다. 즉, 각 지역에서 첫 번째 요청 hello 오래 걸릴 수 있습니다, hello에 지 서버 됩니다 하지 않았으므로 hello 캐시 된 콘텐츠와 tooforward hello 요청 toohello 원본 서버에 필요 합니다. 콘텐츠를 미리 로드하면 첫 번째 적중 대기 시간이 발생하지 않습니다.

또한 캐시 된 자산을 미리 로드 더 나은 고객 만족도 tooproviding hello 원본 서버에서 네트워크 트래픽을 줄일 수 있습니다.

> [!NOTE]
> 자산을 미리 로드 큰 이벤트에 대 한 유용한 되거나 동시에 사용할 수 있는 tooa 수가 많은 사용자가 새 동영상 릴리스 또는 소프트웨어 업데이트와 같은 됩니다 하는 콘텐츠입니다.
> 
> 

이 자습서는 모든 Azure CDN 에지 노드에 캐시된 콘텐츠 미리 로드에 대해 안내합니다.

## <a name="walkthrough"></a>연습
1. Hello에 [Azure 포털](https://portal.azure.com), toopre 부하를 원하는 hello 끝점을 포함 하는 toohello CDN 프로필을 찾습니다.  hello 프로필 블레이드를 엽니다.
2. Hello 목록의 hello 끝점을 클릭 합니다.  hello 끝점 블레이드를 엽니다.
3. Hello CDN 끝점 블레이드에서 hello 로드 단추를 클릭 합니다.
   
    ![CDN 끝점 블레이드](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    hello 부하 블레이드를 엽니다.
   
    ![CDN 로드 블레이드](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Hello 전체 경로 입력 합니다. 원하는 tooload 각 자산 (예: `/pictures/kitten.png`) hello에 **경로** 텍스트 상자에 붙여넣습니다.
   
   > [!TIP]
   > 더 많은 **경로** tooallow 텍스트를 입력 한 후 입력란 나타납니다 toobuild 여러 자산 목록 중입니다.  Hello 줄임표 (...) 단추를 클릭 하 여 hello 목록에서 자산을 삭제할 수 있습니다.
   > 
   > 경로 hello 다음 적합 한 상대 URL 이어야 합니다. [정규식](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >단일 파일 경로 `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`를 업로드합니다.  
   > >쿼리 문자열 `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`을 사용하여 단일 파일을 로드합니다.  
   > 
   > 각 자산에는 자체 경로가 있어야 합니다.  미리 로드한 자산에 대한 와일드카드 기능은 없습니다.
   > 
   > 
   
    ![로드 단추](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Hello 클릭 **부하** 단추입니다.
   
    ![로드 단추](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> 로드 요청은 CDN 프로필별로 분당 10개로 제한됩니다. 요청당 50개의 경로만 허용됩니다. 각 경로의 길이는 1024자로 제한됩니다.
> 
> 

## <a name="see-also"></a>참고 항목
* [Azure CDN 끝점 제거](cdn-purge-endpoint.md)
* [Azure CDN REST API 참조 - 끝점 제거 또는 미리 로드](https://msdn.microsoft.com/library/mt634451.aspx)

