---
title: "데이터 카탈로그 aaaHow toosecure 액세스 tooAzure | Microsoft Docs"
description: "이 문서에 설명 어떻게 toosecure 데이터 카탈로그 및 해당 데이터의 자산입니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Toosecure는 toodata 카탈로그 및 데이터 자산을 액세스 하는 방법
> [!IMPORTANT]
> 이 기능은 Azure Data Catalog hello standard edition 에서만 사용할 수 있습니다.

Azure Data Catalog 있습니다 toospecify hello 데이터 카탈로그 및 기능에 액세스할 수 있는 작업 (등록, 주석 달기, 소유권) hello 카탈로그에 대 한 메타 데이터에 대해 수행할 수 있습니다. 

## <a name="catalog-users-and-permissions"></a>카탈로그 사용자 및 사용 권한
toogive 사용자 또는 그룹 hello tooa 데이터 카탈로그 액세스 및 사용 권한을 설정 합니다.

1. Hello에 [데이터 카탈로그의 홈 페이지](http://www.azuredatacatalog.com), 클릭 **설정을** hello 도구 모음입니다.

    ![데이터 카탈로그 - 설정](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. Hello 설정 페이지에서 확장 hello **카탈로그 사용자** 섹션.
    ![카탈로그 사용자 - 추가](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. **추가**를 클릭합니다.
4. 정규화 된 hello 입력 **사용자 이름** hello의 또는 이름을 **보안 그룹** hello hello 카탈로그와 연결 된 Azure Active Directory (AAD)에서. 사용자나 그룹을 둘 이상 추가하는 경우 쉼표(`,’)를 구분 기호로 사용합니다.
    ![카탈로그 사용자 - 사용자 또는 그룹](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. 키를 눌러 **ENTER** 또는 **탭** hello 텍스트 상자를 벗어났습니다. 
6.  확인 하는 모든 사용 권한을 (**주석 달기**, **등록**, 및 **Take Ownership**) toothese 사용자 또는 그룹 기본적으로 할당 됩니다. Hello 사용자 또는 그룹의 수, 즉 [데이터 자산을 등록]( data-catalog-how-to-register.md), [데이터 자산에 주석 달기]( data-catalog-how-to-annotate.md), 및 [데이터 자산의 소유권]( data-catalog-how-to-manage.md)합니다. 
    ![카탈로그 사용자 - 기본 사용 권한](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  사용자 또는 그룹 toogive hello 읽기 액세스 toohello 카탈로그의 선택을 취소 hello **주석 달기** 해당 사용자나 그룹에 대 한 옵션입니다. 이렇게 하면 hello 사용자 또는 그룹에 데이터 자산 hello 카탈로그에 주석을 달 수 없습니다 하지만 볼 수 있습니다. 
8.  toodeny 사용자 또는 그룹의 데이터 자산을 등록 취소 hello **등록** 해당 사용자나 그룹에 대 한 옵션입니다.
9.  toodeny 지우기 hello 데이터 자산의 소유권 사용자 **소유권** 해당 사용자나 그룹에 대 한 옵션입니다. 
10. 카탈로그 사용자에 게에서 사용자/그룹 toodelete 클릭 **x** hello hello 목록 맨 아래에 hello 사용자/그룹에 대 한 합니다. 
    ![카탈로그 사용자 - 사용자 삭제](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > 추가 사용자가 아닌 보안 그룹 toocatalog 사용자가 직접 추가 사용 권한을 할당 하는 것이 좋습니다. 그런 다음 해당 역할 및 해당 필요한 액세스 toohello 카탈로그와 일치 하는 사용자 toohello 보안 그룹을 추가 합니다.

## <a name="special-considerations"></a>특별 고려 사항

- hello 사용 권한을 할당 toosecurity 그룹 누적 됩니다. 예를 들어 사용자가 두 그룹에 속한다고 가정합니다. 한 그룹에는 주석을 다는 권한이 있고 다른 그룹에는 이 권한이 없다면, 사용자는 주석을 달 수 있는 권한이 있습니다. 
- hello 사용 권한을 할당 된 사용 권한을 toogroups toowhich hello 사용자가 속한 tooa 사용자 재정의 hello 명시적으로 할당 합니다. Hello 이전 예제에서는 예를 들어, hello 사용자 toocatalog 사용자가 명시적으로 추가 하 고 할당 하지 않으면 권한 주석을 추가 합니다. hello 사용자 hello 사용자가 없는 그룹의 구성원 권한이 주석을 추가 하는 경우에 데이터 자산에 주석을 달 수 없습니다.

## <a name="next-steps"></a>다음 단계
- [Azure Azure Data Catalog 시작](data-catalog-get-started.md)

