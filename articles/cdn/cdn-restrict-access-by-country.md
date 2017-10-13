---
title: "국가별 Azure CDN 콘텐츠 제한 | Microsoft Docs"
description: "[지역 필터링] 기능을 사용하여 Azure CDN 콘텐츠에 대한 액세스를 제한하는 방법을 알아봅니다."
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
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>국가별 Azure CDN 콘텐츠 제한

## <a name="overview"></a>개요
기본적으로 사용자가 콘텐츠를 요청하는 경우 사용자가 이 요청을 수행하는 위치에 관계 없이 콘텐츠 페이지가 제공됩니다. 경우에 따라 국가별로 콘텐츠에 액세스를 제한 할 수 있습니다. 이 항목에서는 국가별로 액세스를 허용하거나 차단하도록 서비스를 구성하기 위해 **지역 필터링** 기능을 사용하는 방법을 설명합니다.

> [!IMPORTANT]
> Verizon 및 Akamai 제품은 동일한 지역 필터링 기능을 제공하지만 지원하는 국가 코드가 약간 다릅니다. 차이점에 대한 링크는 3단계를 참조하세요.


이 유형의 제한 구성에 적용되는 고려 사항에 대한 자세한 내용은 항목의 끝에 있는 [고려 사항](cdn-restrict-access-by-country.md#considerations) 섹션을 참조하세요.  

![국가 필터링](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a>1 단계: 디렉터리 경로 정의
포털 안에서 끝점을 선택하고 왼쪽 탐색에서 지역 필터링 탭을 찾아 이 기능을 확인합니다.

국가 필터를 구성하는 경우 사용자에게 액세스를 허용하거나 거부하는 위치에 대한 상대 경로를 지정해야 합니다. 디렉터리 경로 "/pictures/"를 지정하여 "/" 또는 선택된 폴더를 사용하여 모든 파일에 대해 지역 필터링을 적용할 수 있습니다. 마지막 슬래시를 생략하고 파일을 지정하여 "/pictures/city.png"로 단일 파일에 지역 필터링을 적용할 수도 있습니다.

예제 디렉터리 경로 필터:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a>2 단계: 차단 또는 허용 동작을 정의
**차단** : 지정한 국가의 사용자는 해당 재귀 경로에서 요청된 자산에 대해 액세스가 거부됩니다. 해당 위치에 대해 다른 국가 필터링 옵션이 구성되지 않은 경우에는 다른 모든 사용자는 액세스가 허용 됩니다

**허용** : 지정한 국가의 사용자만 해당 재귀 경로에서 요청된 자산에 대해 액세스가 허용됩니다.

## <a name="step-3-define-the-countries"></a>3 단계: 국가 정의하기
경로에 대해 차단 또는 허용하기 원하는 국가를 선택합니다. 

예를 들어 /Photos/Strasbourg/ 차단 규칙은 다음을 포함하는 파일을 필터링합니다.

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>국가 코드
**지역 필터링** 기능은 국가 코드를 사용하여 보안된 디렉터리에 대해 요청이 허용 또는 차단될 국가를 정의합니다. [Azure CDN 국가 코드](https://msdn.microsoft.com/library/mt761717.aspx)에서 국가 코드를 찾을 수 있습니다. 

## <a id="considerations"></a>고려 사항
* 지리 필터링 구성에 대한 변경이 적용되려면 Verizon의 경우 최대 90분, Akamai의 경우 2~3분 정도 걸릴 수 있습니다.
* 이 기능은 와일드카드 문자를 지원하지 않습니다 (예: '*').
* 상대 경로와 관련된 지역 필터링 구성은 해당 경로에 재귀적으로 적용됩니다.
* 동일한 상대 경로에 하나의 규칙만 적용할 수 있습니다. (동일한 상대 경로를 가리키는 여러 국가 필터를 만들 수 없습니다  그러나 폴더에는 여러 국가 필터가 있을 수 있습니다. 이는 국가 필터의 재귀적 특성 때문입니다. 즉, 이전에 구성된 폴더의 하위 폴더에 다른 국가 필터를 할당할 수 있습니다.

