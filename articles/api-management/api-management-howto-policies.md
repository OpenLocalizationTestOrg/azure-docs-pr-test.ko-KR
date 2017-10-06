---
title: "Azure API 관리에서 aaaPolicies | Microsoft Docs"
description: "Toocreate, 편집 하 고 API 관리에서 정책을 구성 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a>Azure API 관리의 정책
Azure API 관리에서 정책은 hello 게시자의 구성을 통해 API hello toochange hello 동작을 허용 하는 hello 시스템의 강력한 기능이 사용 됩니다. 정책은은 API의 응답 또는 hello 요청에서 순차적으로 실행 되는 문 컬렉션 됩니다. 인기 있는 문은 XML tooJSON에서 형식 변환을 포함 하 고 호출 toorestrict hello 양을 개발자 로부터 들어오는 호출 속도입니다. 더 많은 정책을 hello 상자 바로 사용할 수 있는 됩니다.

Hello 참조 [정책 참조] [ Policy Reference] 정책 설명 및 해당 설정의 전체 목록은 합니다.

Hello API 소비자 및 관리 하는 hello API 사이 있는 hello 게이트웨이 내 정책이 적용 됩니다. hello 게이트웨이 모든 요청을 수신 하 고 일반적으로 변경 되지 않은 상태로 전달 toohello API 원본으로 사용 합니다. 그러나 변경 내용 tooboth hello 인바운드 요청과 아웃 바운드 응답에 정책을 적용할 수 있습니다.

정책 식은 hello 정책 지정 하지 않는 한 특성 값 또는 hello API 관리 정책에 텍스트 값으로 사용할 수 있습니다. Hello와 같은 일부 정책은 [제어 흐름] [ Control flow] 및 [변수 설정] [ Set variable] 정책은 정책 식을 기반으로 합니다. 자세한 내용은 [고급 정책][Advanced policies] 및 [정책 식][Policy expressions]을 참조하세요.

## <a name="scopes"></a>어떻게 tooconfigure 정책
전역으로 또는의 hello 범위에서 정책을 구성할 수 있습니다는 [제품][Product], [API] [ API] 또는 [작업] [Operation]. 클라이언트는 정책을 tooconfigure hello 게시자 포털에서 toohello 정책 편집기를 이동 합니다.

![정책 메뉴][policies-menu]

3 개의 주요 구역인 hello 정책 편집기로 구성 됩니다: hello 정책 범위의 (최상위) hello 정책 정의 여기서 정책 (왼쪽) 편집 하 고 hello 문 목록 (오른쪽):

![정책 편집기][policies-editor]

toobegin는 hello에 정책을 적용 해야 하는 hello 범위를 먼저 선택 해야 하는 정책을 구성 합니다. Hello 아래 스크린샷에서 hello **스타터** 제품을 선택 합니다. Note 해당 hello 정사각형 기호 다음 toohello 정책 이름 정책을이 수준에서 적용 이미 되었음을 나타냅니다.

![범위][policies-scope]

정책이 이미 적용 된 이후 hello 구성은 hello 정의 보기에 표시 됩니다.

![구성][policies-configure]

hello 정책 읽기 전용으로 표시 되는지 처음에 있습니다. 순서 tooedit hello 정의 클릭 hello **정책 구성** 동작 합니다.

![편집][policies-edit]

hello 정책 정의 인바운드 및 아웃 바운드 문의 시퀀스를 설명 하는 간단한 XML 문서입니다. hello XML hello 정의 창에서 직접 편집할 수 있습니다. 문 목록 toohello 오른쪽 및 문 적용 가능한 toohello 현재 범위는 활성화 강조; 제공 되며 hello에 나타난 것 처럼 **호출 속도 제한을** 또한 위의 스크린 샷에서 hello에 문의 합니다.

활성화 된 문을 클릭 하면 추가 됩니다 hello 정의 뷰에 hello 커서의 hello 위치에서 적절 한 XML hello 합니다. 

> [!NOTE]
> Tooadd hello 정책을 사용 하지 않는 경우 해당 정책에 대 한 hello 올바른 범위에 있는지 확인 합니다. 각 정책 문은 특정 범위 및 정책 섹션에서 사용하도록 되어 있습니다. tooreview hello 정책 섹션 및 정책에 대 한 범위 확인 hello **사용량** hello에서 해당 정책에 대 한 섹션 [정책 참조][Policy Reference]합니다.
> 
> 

정책 설명의 전체 목록과 해당 설정을 hello에서 사용할 수 있는 [정책 참조][Policy Reference]합니다.

Hello의 hello 콘텐츠 내 hello 커서를 tooadd 들어오는 새 문 toorestrict toospecified IP 주소를 요청 하는 예를 들어 `inbound` XML 요소와 클릭 hello **Restrict 호출자 Ip** 문.

![제한 정책][policies-restrict]

XML 조각 toohello 추가 합니다. `inbound` tooconfigure 문을 hello 하는 방법에 지침을 제공 하는 요소입니다.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit 인바운드 요청 क र च 1.2.3.4는 IP 주소에서 항목만 hello XML을 다음과 같이 수정 합니다.

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![저장][policies-save]

완료 hello 정책에 대 한 hello 문을 구성 되 면 **저장** hello 변경은 전파 toohello API 관리 게이트웨이 즉시 수 있습니다.

## <a name="sections"> </a>정책 구성 이해
정책은 요청 및 응답의 순서로 실행되는 일련의 명령문입니다. hello 구성으로 적절 하 게 나뉘어 `inbound`, `backend`, `outbound`, 및 `on-error` 같은 구성이 hello에 나와 있는 것 처럼 섹션.

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

Hello에서 hello 요청을 처리 하는 동안 오류가 발생 하는 경우 모든 나머지 단계를 `inbound`, `backend`, 또는 `outbound` 섹션 건너뛰고 hello에 toohello 문 실행이 이동 `on-error` 섹션. Hello에 정책 문을 배치 하 여 `on-error` 섹션 hello를 사용 하 여 hello 오류를 검토할 수 있습니다 `context.LastError` 속성을 검사 하 고 hello를 사용 하 여 hello 오류 응답을 사용자 지정 `set-body` 정책을 하 고 오류가 발생 한 경우 수행 되는 작업을 구성 합니다. 오류 코드에 대 한 기본 제공 단계 및 hello 정책 문 처리 하는 동안 발생할 수 있는 오류에 대 한 있습니다. 자세한 내용은 [API Management 정책에서 오류 처리](https://msdn.microsoft.com/library/azure/mt629506.aspx)를 참조하세요.

정책 (전역, 제품, api 및 작업)의 서로 다른 수준에서 지정할 수 있으므로 hello 구성을 사용 하면 있습니다 toospecify hello 순서 존중 toohello 부모 정책을 사용 하 여 hello 정책 정의 문을 실행 합니다. 

정책 범위 hello 순서에 따라 평가 됩니다.

1. 전역 범위
2. 제품 범위
3. API 범위
4. 작업 범위

hello 그 안에서 문에서 hello toohello 배치에 따라 `base` 요소를 제공 합니다. 부모 정책 없음 및 hello를 사용 하 여 글로벌 정책에 `<base>` 에 요소에 영향을 주지 않습니다.

예를 들어 hello 전역 수준 및 API에 대해 구성 된 정책에서 정책을 경우 다음 해당 특정 API가 사용 될 때마다 두 정책이 적용 됩니다. API 관리의 결합 된 정책 문을 hello 기본 요소를 통해 결정적 순서 지정을 허용 합니다. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

Hello 예제 정책 정의에 위의 hello `cross-domain` 차례로 하는 더 높은 정책을 hello 올 수 전에 문을 실행 합니다 `find-and-replace` 정책입니다. 

hello hello 정책 편집기에서 현재 범위에서 toosee hello 정책 클릭 **선택한 범위에 대 한 실제 정책 다시 계산**합니다.

## <a name="next-steps"></a>다음 단계
다음과 같은 정책 식 관련 비디오를 확인하세요.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
