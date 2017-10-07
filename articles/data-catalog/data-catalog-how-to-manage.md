---
title: "Azure Data Catalog에서 데이터 자산 aaaManage | Microsoft Docs"
description: "hello 문서 toocontrol 표시 유형 및 데이터 자산의 소유권 Azure Data Catalog에 등록 하는 방법을 강조 표시 합니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>Azure Data Catalog에서 데이터 자산 관리
## <a name="introduction"></a>소개
Azure Data Catalog는 쉽게 검색 하 고 이해 hello 데이터 원본 tooperform 분석 필요 하 고 내릴 수 있도록 데이터 원본 검색을 위해 설계 되었습니다. 이러한 검색 기능 및 다른 사용자가 찾아 hello 광범위 한 사용 가능한 데이터 소스를 이해할 수 때 hello 가장 큰 영향을 확인 합니다. 에 이러한 요소와 데이터 카탈로그의 hello 기본 동작은 모든 등록 된 데이터 원본 toobe 표시 tooand 검색 가능한 모든 카탈로그 사용자에 대 한입니다.

데이터 카탈로그 얻지 자체 toohello 데이터에 액세스 합니다. 데이터 액세스는 hello hello 데이터 원본 소유자에 의해 제어 됩니다. 데이터 카탈로그와 데이터 소스를 검색 하 고 hello 카달로그에 등록 하는 관련된 toohello 원본 hello 메타 데이터를 볼 수 있습니다.

그러나 데이터 원본 표시 toospecific 사용자 또는 특정 그룹의 toomembers 수만 해야 경우가 있을 수 있습니다. 이러한 시나리오에서는 사용자 hello 카탈로그 내에서 등록 된 데이터 자산의 소유권을 가져올 수 있습니다 및 다음 hello 자산을 소유한 hello 표시 여부를 제어 합니다.

> [!NOTE]
> 이 문서에 설명 된 hello 기능은 hello 표준 버전의 Azure Data Catalog에만 사용할 수 있습니다. hello 무료 버전을 제공 하지 않습니다 소유권 및 데이터 자산 가시성 제한에 대 한 기능.
>
>

## <a name="manage-ownership-of-data-assets"></a>데이터 자산의 소유권 관리
기본적으로 데이터 카탈로그에 등록된 데이터 자산은 소유되지 않습니다. 권한 tooaccess hello 카탈로그에 있는 모든 사용자 검색 하 고 이러한 자산에 주석을 달 수 있습니다. 사용자가 소유 하지 않은 데이터 자산의 소유권을 가져올 다음 hello 자산을 소유한 hello 가시성 제한 수 있으며

데이터 카탈로그에서 데이터 자산을 소유 하 고 hello 소유자가 권한이 있는 사용자만는 hello 자산을 검색 하 고 해당 메타 데이터를 볼 수 및 hello 소유자만 hello 카탈로그에서 hello 자산을 삭제할 수 있습니다.

> [!NOTE]
> 데이터 카탈로그에 소유권 hello 카탈로그에 저장 된 hello 메타를 데이터만 영향을 줍니다. 소유권은 hello 데이터 원본에 대 한 모든 권한을 제공 하지 않습니다.
>
>

### <a name="take-ownership"></a>소유권 가져오기
Hello를 선택 하 여 데이터 자산의 소유권을 가져올 수 사용자 **Take Ownership** hello Data Catalog 포털에 대 한 옵션입니다. 특별 권한은 없습니다 소유 되지 않은 데이터 자산의 필요한 tootake 소유권을 보여 줍니다. 모든 사용자는 소유되지 않은 데이터 자산을 소유할 수 있습니다.

### <a name="add-owners-and-co-owners"></a>소유자 및 공동 소유자 추가
데이터 자산이 이미 소유된 경우 다른 사용자는 소유권을 가질 수 없습니다. 기존 소유자에 의해 공동 소유자로 추가되어야 합니다. 소유자는 추가 사용자 또는 보안 그룹을 공동 소유자로 추가할 수 있습니다.

> [!NOTE]
> 이 모든 소유한 데이터 자산에 대 한 모범 사례 toohave 소유자로 두 개 이상의 개인은 합니다.
>
>

### <a name="remove-owners"></a>소유자 제거
자산 소유자가 공동 소유자를 추가할 수 있는 것처럼 자산 소유자는 공동 소유자를 제거할 수 있습니다.

소유자로 본인을 제거 하는 자산 소유자 hello 자산을 관리할 더 이상 수 없습니다. Hello 자산 소유자 소유자로 본인 제거 되 고 다른 없습니다 공동 소유자는, hello 자산 상태 소유 tooan로 돌아갑니다.

## <a name="control-visibility"></a>컨트롤 표시 여부
데이터 자산 소유자는 자신이 소유한 hello 데이터 자산의 hello 표시 유형을 제어할 수 있습니다. hello 기본값으로 toorestrict 표시 유형, 모든 사용자를 검색할 수는 데이터 카탈로그 및 보기 hello 데이터 자산 여기서 hello 자산 소유자 설정/해제할 수에서 hello 표시 유형 설정이 **Everyone** 너무**소유자 및 이러한 사용자** hello 자산에 대 한 hello 속성에 있습니다. 그런 다음 소유자는 특정 사용자 및 보안 그룹을 추가할 수 있습니다.

> [!NOTE]
> 가능 하면 항상 toosecurity 그룹 및 사용자가 tooindividual 아닌 자산 소유권 및 표시 유형 사용 권한 할당 되어야 합니다.
>
>

## <a name="catalog-administrators"></a>카탈로그 관리자
데이터 카탈로그 관리자는 암시적으로 공동 소유자 hello 카탈로그에 있는 모든 자산입니다. 자산 소유자 관리자에 게 가시성을 제거할 수 없습니다 및 관리자 소유권과 hello 카탈로그에 있는 모든 데이터 자산에 대 한 표시 유형을 관리할 수 있습니다.

## <a name="summary"></a>요약
모든 카탈로그 사용자 toocontribute 허용 하 고 검색 하는 hello 데이터 카탈로그 crowdsourcing 모델 toometadata 및 데이터 자산을 검색 합니다. 데이터 카탈로그의 Standard Edition hello 소유권 및 관리 toolimit hello 표시 유형 및 특정 데이터 자산 사용을 위해 설계 되었습니다.
