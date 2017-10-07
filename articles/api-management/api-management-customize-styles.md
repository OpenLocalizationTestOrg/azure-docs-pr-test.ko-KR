---
title: "Azure API 관리에서 hello 개발자 포털에서 aaaCustomize 스타일 | Microsoft Docs"
description: "Azure API 관리에서 hello 개발자 포털에서 모든 페이지에 대 한 toomodify hello 스타일을 사용 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Azure API 관리에서 개발자 포털 hello의 hello 스타일을 사용자 지정
Azure API 관리에서 세 가지 기본 방법 toocustomize hello 개발자 포털이 있습니다.

* [정적 페이지 및 페이지 레이아웃 요소 hello 내용을 편집합니다][modify-content-layout]
* [페이지 요소에 대 한 hello 개발자 포털에서 사용 하는 hello 스타일 업데이트] [ customize-styles] (이 가이드에서 설명)
* [Hello 포털에서 생성 된 페이지에 사용 되는 hello 템플릿을 수정] [ portal-templates] (예: API docs, 제품, 사용자 인증 등)

## <a name="change-headers-styling"></a>페이지 요소의 hello 스타일 변경

hello 색, 글꼴, 크기, 간격, 및 hello 포털에서 모든 페이지의 기타 스타일 관련 요소 정의 된 스타일 규칙에 의해 합니다. 

Hello 스타일 규칙은 방식 hello에서 **개발자 포털** 관리자 권한으로 로그인 하는 중입니다. 먼저 hello Azure 포털을 열고 마우스 클릭 tooget 있습니다 **게시자 포털** API 관리 인스턴스 hello 서비스 도구 모음에서 합니다.

![게시자 포털][api-management-management-console]

다음에서 클릭 **개발자 포털** hello 오른쪽에 있습니다. 

![Hello 게시자 포털의 개발자 포털 링크][api-management-pp-dp-link]

hello 사용자 지정 아이콘 위로 마우스를 이동 (또는 선택) tooopen hello에 대 한 사용자 지정 도구 모음 및 다음 클릭 "스타일을" hello 도구 모음에서 합니다.

![사용자 지정 도구 모음 단추][api-management-customization-toolbar-button]

스타일 지정 규칙을 편집 하는 두 개의 주요 방법을-기본적으로 표시 되는 모든 hello 스타일 규칙을 사용 하는 hello 목록을 검색 하 고 필요에 따라 스타일을 수정할 수 없거나 없는 선택할 수 있습니다 **hello 페이지에서 요소 선택** 한 다음 해당 요소에 대 한 hello 페이지 toosee 유일한 hello 스타일 아무 곳 이나 클릭 합니다.

![사용자 지정 도구 모음][api-management-customization-toolbar]

Hello 클릭 **hello 페이지에서 요소 선택** 이 예제에 대 한 옵션입니다.  요소 이제 될 강조 표시를 가리키면 hello 마우스 toosignify와 어떤 요소 스타일을 클릭 한 경우 편집을 시작 합니다. 이동 hello 위로 마우스를 hello 헤더 (일반적으로 hello 회사 이름이 있는 여기) 및 클릭 hello 텍스트 것입니다. Hello 스타일 편집기 내에서 명명 된 인수와 분류 된 스타일 지정 규칙 집합이 표시 됩니다. 각 규칙 hello 선택 된 요소의 스타일 속성을 나타냅니다. 예를 들어 위에서 선택한 hello 머리글 텍스트에 대 한 hello hello 텍스트 크기가에 @font-size-h1 대안 hello 글꼴의 이름이 고 hello 중인 동안 @headings-font-family합니다.

> 익숙한 경우 [부트스트랩][bootstrap], 이러한 규칙은 실제로 [LESS 변수] [ LESS variables] hello 사용 되는 hello 부트스트랩 테마 내에서 개발자 포털입니다.
> 
> 

Hello hello 머리글 텍스트 색을 변경해 보겠습니다. Hello에서 hello 항목을 선택  **@headings-color**  필드와 형식 **#000000**합니다. Hello 검정 hello 색에 대 한 16 진수 코드입니다. 이렇게 하면 사각형 색 표시기 hello 끝 hello 텍스트 상자에 표시 되는지 볼 수 있습니다. 색 선택이이 표시기를 클릭 하면 toochoose 색.

![색 선택][api-management-customization-toolbar-color-picker]

변경 내용은이 미리 보기를 실시간으로, 하지만 표시만 tooadministrators 됩니다. toomake hello 클릭, 이러한 변경 사항은 표시 tooeveryone **게시** hello 스타일 지정 편집기에서 단추 및 hello 변경 사항을 확인 합니다.

![게시 메뉴][api-management-customization-toolbar-publish-form]

> toochange hello tooany 적용 되는 규칙 다른 요소의 스타일 hello 페이지에서 다음과 같은 hello hello 헤더에 대 한 프로시저 처럼 않았습니다. 클릭 **hello 페이지에서 요소 선택** hello 스타일 지정 편집기, select hello 요소에 관심이 및 시작 hello 화면에 표시 된 hello 스타일 규칙의 hello 값을 수정 합니다.
> 
> 


## <a name="next-steps"> </a>다음 단계
* 개발자 포털의 toocustomize hello 콘텐츠 페이지를 사용 하 여 하는 방식에 대해 알아봅니다 [개발자 포털 템플릿](api-management-developer-portal-templates.md)합니다.

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
