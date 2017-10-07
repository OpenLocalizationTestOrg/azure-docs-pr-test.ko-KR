---
title: "Azure CDN 끝점 aaaPurge | Microsoft Docs"
description: "모든 toopurge 캐시 하는 방법을 알아보려면 Azure CDN 끝점에서 콘텐츠입니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>Azure CDN 끝점 제거
## <a name="overview"></a>개요
Azure CDN 지 노드에 hello 자산 활성 시간 (TTL) 만료 될 때까지 자산을 캐시 합니다.  Hello 자산 TTL이 만료 되 면 클라이언트가 hello 가장자리 노드에서 hello 자산을 요청 하면, hello 가장자리 노드 hello 자산 tooserve hello 클라이언트 요청의 새 업데이트 된 복사본을 검색 하 고 hello 캐시 새로 고침을 저장 합니다.

hello 모범 사례 toomake 사용자는 항상 hello 자산의 최신 복사본 가져오기 있는지는 tooversion 각각에 대해 자산 업데이트 및 새 Url로 게시 합니다.  CDN에서 즉시 hello hello 다음 클라이언트 요청에 대 한 새 자산을 검색 합니다.  경우에 따라 toopurge 모든 가장자리 노드의 콘텐츠를 캐시 하 고 새 업데이트 된 모든 자산 tooretrieve를 강제로 지정할 수 있습니다.  이 기한 tooupdates tooyour 웹 응용 프로그램 또는 잘못 된 정보가 포함 된 tooquickly 업데이트 자산 수 있습니다.

> [!TIP]
> hello 지웁니다만 제거 하는 참고 hello CDN에 지 서버에서 콘텐츠를 캐시 합니다.  프록시 서버와 로컬 브라우저 캐시와 같은 모든 다운스트림 캐시 hello 파일의 캐시 된 복사본을 보유할 여전히 수 있습니다.  중요 한 tooremember는이 설정 하면 파일의 활성 시간입니다.  업데이트 될 때마다 고유한 이름을 지정 하 여 또는의 이용 하 여 파일의 다운스트림 클라이언트 toorequest hello 최신 버전을 강제로 실행할 수 있습니다 [쿼리 문자열 캐싱](cdn-query-string.md)합니다.  
> 
> 

이 자습서는 끝점의 모든 가장자리 노드에서 자산을 제거하는 과정을 안내합니다.

## <a name="walkthrough"></a>연습
1. Hello에 [Azure 포털](https://portal.azure.com), toopurge 원하는 hello 끝점을 포함 하는 toohello CDN 프로필을 찾습니다.
2. Hello CDN 프로필 블레이드에서 hello 제거 단추를 클릭 합니다.
   
    ![CDN 프로필 블레이드](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    hello 지우기 블레이드를 엽니다.
   
    ![CDN 제거 블레이드](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. Hello 블레이드를 제거 하 고 toopurge hello URL에 대 한 드롭다운에서 원하는 hello 서비스 주소를 선택 합니다.
   
    ![양식 제거](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > Hello를 클릭 하 여 toohello 지우기 블레이드를 가져올 수도 있습니다 **제거** hello CDN 끝점 블레이드에서 단추입니다.  이 경우 hello **URL** 필드는 해당 특정 끝점의 hello 서비스 주소와 미리 채워진 됩니다.
   > 
   > 
4. 어떤 자산 원하는 hello에서 toopurge 가장자리 노드를 선택 합니다.  Tooclear 모든 자산을 클릭 하 여 hello **모두** 확인란을 선택 합니다.  그렇지 않은 경우 각 자산의 hello 경로 형식의 toopurge에에서 원하는 hello **경로** 텍스트 상자에 붙여넣습니다. 형식 아래 hello 경로에서 지원 됩니다.
    1. **단일 URL 지우기**: hello 파일 확장명, 예: 유무 hello 전체 URL을 지정 하 여 개별 자산 지우기`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **와일드 카드 제거**: 별표(\*)를 와일드 카드로 사용할 수 있습니다. 모든 폴더, 하위 폴더 및 파일 끝점에서 제거 `/*` 경로 hello 또는 이어서 hello 폴더를 지정 하 여 모든 하위 폴더와 특정 폴더 아래에 있는 파일을 제거 `/*`, 예:`/pictures/*`합니다.  와일드 카드 제거는 현재 Akamai의 Azure CDN에서 지원되지 않습니다. 
    3. **루트 도메인 제거**: hello 경로에 "/"와 hello 끝점의 hello 루트를 제거 합니다.
   
   > [!TIP]
   > 경로 제거에 대 한 지정 해야 하며 hello 다음에 맞는 상대 URL 이어야 [정규식](https://msdn.microsoft.com/library/az24scfc.aspx)합니다. **모두 제거** 및 **와일드 카드 제거**는 현재 **Akamai의 Azure CDN**에서 지원되지 않습니다.
   > > 단일 URL 제거 `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > 쿼리 문자열 `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > 와일드 카드 제거 `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";` 
   > 
   > 더 많은 **경로** tooallow 텍스트를 입력 한 후 입력란 나타납니다 toobuild 여러 자산 목록 중입니다.  Hello 줄임표 (...) 단추를 클릭 하 여 hello 목록에서 자산을 삭제할 수 있습니다.
   > 
5. Hello 클릭 **제거** 단추입니다.
   
    ![제거 단추](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> 지우기 요청으로 약 2-3 분 tooprocess 걸릴 **Verizon에서 Azure CDN** (Standard 및 Premium) 및 사용 하는 약 7 분 **Akamai에서 Azure CDN**합니다.  Azure CDN은 동시 제거 요청이 항상 50개로 제한됩니다. 
> 
> 

## <a name="see-also"></a>참고 항목
* [Azure CDN 끝점에 자산 미리 로드](cdn-preload-endpoint.md)
* [Azure CDN REST API 참조 - 끝점 제거 또는 미리 로드](https://msdn.microsoft.com/library/mt634451.aspx)

