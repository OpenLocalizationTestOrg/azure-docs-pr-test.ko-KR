---
title: "Azure API 관리에서 개발자 포털 hello의에서 페이지 콘텐츠를 aaaModify | Microsoft Docs"
description: "Azure API 관리에서 개발자 포털 hello에 tooedit 페이지 목차 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Hello 내용 및 Azure API 관리에서 hello 개발자 포털에 있는 페이지의 레이아웃을 수정 합니다.
Azure API 관리에서 세 가지 기본 방법 toocustomize hello 개발자 포털이 있습니다.

* [정적 페이지 및 페이지 레이아웃 요소 hello 내용을 편집] [ modify-content-layout] (이 가이드에서 설명)
* [페이지 요소에 대 한 hello 개발자 포털에서 사용 하는 hello 스타일 업데이트][customize-styles]
* [Hello 포털에서 생성 된 페이지에 사용 되는 hello 템플릿을 수정] [ portal-templates] (예: API docs, 제품, 사용자 인증 등)

## <a name="page-structure"> </a>개발자 포털 페이지의 구조

hello 개발자 포털 콘텐츠 관리 시스템을 기반으로 합니다. 모든 페이지의 hello 레이아웃은 위젯 라고 하는 작은 페이지 요소의 집합을 기반으로 빌드됩니다.

![개발자 포털 페이지 구조][api-management-customization-widget-structure]

모든 위젯은 편집이 가능합니다. 
* hello 코어 내용 특정 tooeach 개별 페이지 hello "콘텐츠" 위젯에 있어야 합니다. 페이지 편집이 위젯의 hello 내용을 편집 하는 것을 의미 합니다.
* 가 hello 나머지 위젯에 모든 페이지 레이아웃 요소가 포함 되어 있습니다. 변경 내용을 toothese 위젯 tooall 페이지에 적용 됩니다. 참조 된 tooas "레이아웃 위젯" 됩니다.

일상적인 페이지에서 각 개별 페이지에 대 한 다른 콘텐츠를 포함 하는 hello 콘텐츠 위젯을 수정만 일반적으로 하나를 편집 합니다.

## <a name="modify-layout-widget"></a>Hello 내용의 레이아웃 위젯 수정

Hello Azure 포털에서에서 액세스할 수 있는 hello 게시자 포털을 통해 hello 개발자 포털 내에서 콘텐츠를 수정 합니다. tooreach, 클릭 **게시자 포털** API 관리 인스턴스 hello 서비스 도구 모음에서 합니다.

![게시자 포털][api-management-management-console]

해당 위젯의 tooedit hello 내용을 클릭 **위젯** hello에서 **개발자 포털** hello 왼쪽 메뉴. 이 예제를 사용에 대 한 hello hello 헤더 widget 내용의 압축을 수정 합니다. 선택 hello **헤더** hello 목록에서 위젯입니다.

![위젯 머리글][api-management-widgets-header]

hello 머리글의 내용 hello는 hello 내에서 편집할 수 **본문** 필드입니다. Hello 텍스트를 원하는 대로 변경한 다음 클릭 **저장** hello hello 페이지 맨 아래에 있습니다.

이제 수 toosee hello 새 헤더 hello 개발자 포털 내에서 모든 페이지에 있어야 합니다.

> hello 게시자 포털에 있는 동안 tooopen hello 개발자 포털 클릭 **개발자 포털** hello 위쪽 막대에서 합니다.
> 
> 

## <a name="edit-page-contents"></a>페이지의 hello 내용을 편집 합니다.

toosee hello 목록은 모든 기존 콘텐츠 페이지 클릭 **콘텐츠** hello에서 **개발자 포털** hello 게시자 포털 메뉴.

![콘텐츠 관리][api-management-customization-manage-content]

Hello 클릭 **시작** 페이지 tooedit hello 개발자 포털의 hello 홈 페이지에 표시 되는 내용입니다. Hello 변경 하려면, 필요한 경우 미리 보기 하 고 클릭 **지금 게시** toomake 해당 tooeveryone 표시 합니다.

> hello 홈 페이지 배너 toodisplay hello 위쪽에 허용 하는 특별 한 레이아웃을 사용 합니다. 이 배너 hello에서 편집할 수는 없습니다 **콘텐츠** 섹션. 이 배너 tooedit 클릭 **위젯** hello에서 **개발자 포털** 메뉴 선택 **홈 페이지** hello에서 **현재 레이어** 드롭다운 목록을 열고 hello **배너** hello 아래 항목 **섹션을 갖춘**합니다. 이 위젯의의 hello 내용이 다른 페이지와 마찬가지로 편집할 수 있습니다.
> 
> 

## <a name="next-steps"> </a>다음 단계
* [페이지 요소에 대 한 hello 개발자 포털에서 사용 하는 hello 스타일 업데이트][customize-styles]
* [Hello 포털에서 생성 된 페이지에 사용 되는 hello 템플릿을 수정] [ portal-templates] (예: API docs, 제품, 사용자 인증 등)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
