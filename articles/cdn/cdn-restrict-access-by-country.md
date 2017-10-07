---
title: "Azure CDN 콘텐츠 국가별로 aaaRestrict | Microsoft Docs"
description: "지역 필터링 기능을 hello toorestrict tooyour Azure CDN 콘텐츠 사용 하 여 액세스 방법에 대해 알아봅니다."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>국가별 Azure CDN 콘텐츠 제한

## <a name="overview"></a>개요
기본적으로 콘텐츠를 요청 하는 사용자, hello 콘텐츠 페이지가 hello 사용자에서이 요청을 생성 하는 위치에 관계 없이 제공 됩니다. 경우에 따라 toorestrict 국가별로 tooyour 내용에 액세스할 수도 있습니다. 이 항목에서는 설명 어떻게 toouse hello **지역 필터링** 순서 tooconfigure hello 서비스 tooallow 또는 블록 액세스의 국가별 기능입니다.

> [!IMPORTANT]
> hello Verizon 및 Akamai 제품 지 원하는 te 국가 코드에 약간의 차이가 설치 했지만 hello 동일한 지역 필터링 기능을 제공 합니다. 링크 toohello 차이점에 대 한 3 단계를 참조 하십시오.


Tooconfiguring 적용 되는 고려 사항에 대 한 내용은이 유형의 제한 참조 hello [고려 사항](cdn-restrict-access-by-country.md#considerations) hello 항목의 hello 끝에 나오는 섹션.  

![국가 필터링](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>1 단계: hello 디렉터리 경로 정의 합니다.
Hello 포털 내에서 끝점을 선택 하 고 hello 지역 필터링 탭 왼쪽의 탐색 toofind hello에이 기능을 찾을 수 있습니다.

국가 필터를 구성할 때 hello 상대 경로 toohello 위치 toowhich 사용자 허용 또는 액세스 거부를 지정 해야 합니다. 디렉터리 경로 "/pictures/"를 지정하여 "/" 또는 선택된 폴더를 사용하여 모든 파일에 대해 지역 필터링을 적용할 수 있습니다. Hello 파일을 지정 하 여 지리적 필터링 tooa를 단일 파일 적용할 수도 있습니다 하 고 뒤에 슬래시가 hello 맞추고 나머지 "/ pictures/city.png"입니다.

예제 디렉터리 경로 필터:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>2 단계: hello 동작 정의: 차단 또는 허용
**차단:** hello에서 사용자가 지정한 해당 재귀 경로에서 요청 된 액세스 tooassets 국가 거부 됩니다. 해당 위치에 대해 다른 국가 필터링 옵션이 구성되지 않은 경우에는 다른 모든 사용자는 액세스가 허용 됩니다

**허용:** hello 사용자만 지정 국가 해당 재귀 경로에서 요청 된 액세스 tooassets 허용 됩니다.

## <a name="step-3-define-hello-countries"></a>3 단계: hello 국가 정의 합니다.
Hello 국가 tooblock 싶거나 hello 경로 대 한 허용을 선택 합니다. 

예를 들어 차단 /Photos/Strasbourg/hello 규칙 포함 하 여 파일을 필터링 합니다.

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>국가 코드
hello **지역 필터링** 기능은 있는 요청을 허용 또는 차단 된 국가 코드 toodefine hello 국가 사용 하 여 보안 된 디렉터리에 대 한 합니다. Hello에 국가 코드를 찾을 수 있습니다 [Azure CDN 국가 코드](https://msdn.microsoft.com/library/mt761717.aspx)합니다. 

## <a id="considerations"></a>고려 사항
* Too90 Verizon, 분 또는 Akamai, 변경 내용 tooyour 국가 필터링 구성 tootake 효과 대 일 분이 걸릴 수도 있습니다.
* 이 기능은 와일드카드 문자를 지원하지 않습니다 (예: '*').
* hello 상대 경로와 관련 된 hello 지역 필터링 구성 toothat 경로 재귀적으로 적용된 됩니다.
* 규칙을 하나만 적용 된 toohello 수 동일한 상대 경로 (해당 지점 toohello 여러 국가 필터를 만들 수 없습니다 동일한 상대 경로입니다. (동일한 상대 경로를 가리키는 여러 국가 필터를 만들 수 없습니다  그러나 폴더에는 여러 국가 필터가 있을 수 있습니다. 국가 필터의 toohello 재귀적 특징 때문입니다. 즉, 이전에 구성된 폴더의 하위 폴더에 다른 국가 필터를 할당할 수 있습니다.

