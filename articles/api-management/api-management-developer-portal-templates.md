---
title: "템플릿을 사용 하 여 aaaCustomize hello API 관리 개발자 포털-Azure | Microsoft Docs"
description: "Toocustomize 템플릿을 사용 하 여 Azure API 관리 개발자 포털 hello 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>어떻게 toocustomize hello 템플릿을 사용 하 여 Azure API 관리 개발자 포털

Azure API 관리에서 세 가지 기본 방법 toocustomize hello 개발자 포털이 있습니다.

* [정적 페이지 및 페이지 레이아웃 요소 hello 내용을 편집합니다][modify-content-layout]
* [페이지 요소에 대 한 hello 개발자 포털에서 사용 하는 hello 스타일 업데이트][customize-styles]
* [Hello 포털에서 생성 된 페이지에 사용 되는 hello 템플릿을 수정] [ portal-templates] (이 가이드에서 설명)

템플릿은 사용 되는 toocustomize hello 시스템에서 생성 된 개발자 포털 페이지 (예: API docs, 제품, 사용자 인증 등)의 콘텐츠입니다. 사용 하 여 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 지역화 된 문자열 리소스, 아이콘 및 페이지 컨트롤, 제공 된 집합이 나타나며 hello 페이지의 뛰어난 유연성 tooconfigure hello 내용을 백업이 있어야 합니다.

## <a name="developer-portal-templates-overview"></a>개발자 포털 템플릿 개요
템플릿 편집은 hello에서 수행 **개발자 포털** 관리자 권한으로 로그인 하는 중입니다. 먼저 hello Azure 포털을 열고 마우스 클릭 tooget 있습니다 **게시자 포털** API 관리 인스턴스 hello 서비스 도구 모음에서 합니다.

![게시자 포털][api-management-management-console]

다음에서 클릭 **개발자 포털** hello 오른쪽에 있습니다. 

![개발자 포털 메뉴][api-management-developer-portal-menu]

tooaccess 개발자 포털 템플릿 hello, hello 클릭 hello 왼쪽된 toodisplay hello 사용자 지정 메뉴에서 아이콘을 사용자 지정 하 고 클릭 **템플릿**합니다.

![개발자 포털 템플릿][api-management-customize-menu]

hello 템플릿 목록에는 hello hello 개발자 포털에서 서로 다른 페이지를 포함 하는 서식 파일의 여러 범주가 표시 됩니다. 각 서식 파일은 다른 경우 하지만 hello 단계 tooedit 해당 hello 변경 내용을 게시 하 고 동일 hello 됩니다. tooedit 템플릿을 hello 템플릿의 hello 이름을 클릭 합니다.

![개발자 포털 템플릿][api-management-templates-menu]

서식 파일을 클릭 하면 해당 템플릿에서 사용자 지정할 수 있는 toohello 개발자 포털 페이지를 이동 합니다. 이 예제에서는 hello에 **제품 목록을** 템플릿이 표시 됩니다. hello **제품 목록을** 템플릿 컨트롤 hello hello 빨간색 사각형으로 표시 하는 hello 화면 영역입니다. 

![제품 목록 템플릿][api-management-developer-portal-templates-overview]

Hello와 같은 일부 템플릿에서 **사용자 프로필** hello의 다른 부분을 사용자 지정 서식 파일을 같은 페이지입니다. 

![사용자 프로필 템플릿][api-management-user-profile-templates]

각 개발자 포털 서식 파일에 대 한 hello 편집기 hello hello 페이지 맨 아래에 표시 되는 두 개의 섹션에 있습니다. hello 왼쪽 창의 hello 서식 파일을 편집 하는 hello를 표시 하 고 hello 오른쪽 hello 서식 파일에 대 한 데이터 모델 hello를 표시 합니다. 

hello 템플릿 창 편집 hello hello 개발자 포털에서 해당 페이지의 hello 모양 및 동작을 제어 하는 hello 태그를 포함 합니다. hello 템플릿에서 hello 태그 hello를 사용 하 여 [DotLiquid](http://dotliquidmarkup.org/) 구문입니다. [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers)가 DotLiquid용 편집기로 많이 사용됩니다. 모든 변경 내용을 toohello 템플릿을 편집 하는 동안 표시 되는 실시간 hello 브라우저에서 하지만 표시 되지 않는 tooyour 고객 할 때까지 [저장](#to-save-a-template) 및 [게시](#to-publish-a-template) hello 서식 파일.

![템플릿 태그][api-management-template]

hello **템플릿 데이터** 창 toohello 데이터 한 지침을 제공 특정 서식 파일에서 사용 하기 위해 사용할 수 있는 hello 엔터티에 대 한 모델입니다. 현재 hello 개발자 포털에 표시 되는 hello 라이브 데이터를 표시 하 여이 가이드를 제공 합니다. Hello의 hello 오른쪽 위 모서리에 hello 사각형을 클릭 하 여 hello 템플릿 창을 확장 있습니다 **템플릿 데이터** 창.

![템플릿 데이터 모델][api-management-template-data]

Hello 앞 예제에서는 hello에 표시 된 hello 데이터에서 검색 된 hello 개발자 포털에 표시 되는 두 개의 제품 **템플릿 데이터** hello 다음 예제와 같이 창.

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

hello에 hello 태그 **제품 목록을** 템플릿 프로세스 제품 toodisplay 정보 및 링크 tooeach 개별 제품의 hello 컬렉션을 반복 하 여 데이터 tooprovide hello 원하는 출력 hello 합니다. 참고 hello `<search-control>` 및 `<page-control>` hello 태그에 있는 요소입니다. 이러한 검색 및 hello 페이지의 컨트롤 페이징 hello의 hello 표시를 제어 합니다. `ProductsStrings|PageTitleProducts`hello를 포함 하는 지역화 된 문자열 참조 `h2` hello 페이지에 대 한 머리글 텍스트입니다. 개발자 포털 템플릿에서 사용할 수 있는 문자열 리소스, 페이지 컨트롤 및 아이콘 목록은 [API 관리 개발자 포털 템플릿 참조](api-management-developer-portal-templates-reference.md)를 참조하세요.

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
        </li>    
    {% endfor %}
    </ul>
    <paging-control></paging-control>
    {% else %}
    {% localized "CommonResources|NoItemsToDisplay" %}
    {% endif %}
    </div>
</div>
```

## <a name="toosave-a-template"></a>toosave 서식 파일
toosave 서식 파일을 저장 hello 템플릿 편집기에서 클릭 합니다.

![템플릿 저장][api-management-save-template]

저장 된 변경 내용을 게시 될 때까지 hello 개발자 포털에서 라이브있지 않습니다.

## <a name="toopublish-a-template"></a>toopublish 서식 파일
저장된 템플릿은 개별적으로 또는 모두 함께 게시할 수 있습니다. 개별 템플릿을 toopublish 클릭 hello 템플릿 편집기에 게시 합니다.

![템플릿 게시][api-management-publish-template]

클릭 **예** tooconfirm 확인 hello 개발자 포털에서 사용 중인 hello 템플릿.

![게시 확인][api-management-publish-template-confirm]

toopublish 중인 모든 게시 되지 않은 템플릿 버전을 클릭 **게시** hello 템플릿 목록에서입니다. 게시 되지 않은 템플릿 hello 템플릿 이름 다음에 별표 지정 됩니다. 이 예제에서는 hello **제품 목록** 및 **제품** 템플릿을 게시 되 고 있습니다.

![템플릿 게시][api-management-publish-templates]

클릭 **갖추어야** tooconfirm 합니다.

![게시 확인][api-management-publish-customizations]

새로 게시 된 템플릿을 hello 개발자 포털에서 즉시 적용 됩니다.

## <a name="toorevert-a-template-toohello-previous-version"></a>toorevert 템플릿 toohello 이전 버전
toorevert 템플릿 toohello 이전 게시 된 버전을 클릭 하 여 hello 템플릿 편집기에서 되돌립니다.

![템플릿 되돌리기][api-management-revert-template]

클릭 **예** tooconfirm 합니다.

![Confirm][api-management-revert-template-confirm]

서식 파일의 게시 된 버전은 hello 되돌리기 작업이 면 hello 개발자 포털에 살고 있는 이전에 hello 완료 되었습니다.

## <a name="toorestore-a-template-toohello-default-version"></a>toorestore 템플릿 toohello 기본 버전
복원 중인 템플릿 tootheir 기본 버전은 두 단계로 이루어집니다. 첫 번째 hello 서식 파일, 복원 해야 하 고 복원 하는 hello 버전을 게시 해야 합니다.

단일 템플릿 toohello 기본 버전 toorestore hello 템플릿 편집기에서 복원을 클릭 합니다.

![템플릿 되돌리기][api-management-reset-template]

클릭 **예** tooconfirm 합니다.

![Confirm][api-management-reset-template-confirm]

toorestore 모든 템플릿 tootheir 기본 버전을 클릭 하 여 **기본 서식 파일을 복원** hello 템플릿 목록에 있습니다.

![템플릿 복원][api-management-restore-templates]

hello 복원 된 템플릿 다음 게시 해야 개별적으로 또는 한 번에 모두의 hello 단계를 수행 하 여 [toopublish 템플릿으로](#to-publish-a-template)합니다.

## <a name="next-steps"></a>다음 단계
개발자 포털 템플릿, 문자열 리소스, 아이콘 및 페이지 컨트롤에 대한 참조 정보는 [API 관리 개발자 포털 템플릿 참조](api-management-developer-portal-templates-reference.md)를 참조하세요.

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







