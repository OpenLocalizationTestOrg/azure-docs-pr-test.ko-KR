---
title: "Azure API 관리 정책에 aaaHow toouse 속성"
description: "자세한 내용은 방법 Azure API 관리 정책에 toouse 속성입니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>어떻게 Azure API 관리 정책에 toouse 속성
API 관리 정책은 hello 게시자의 구성을 통해 API hello toochange hello 동작을 허용 하는 hello 시스템의 강력한 기능입니다. 정책은은 API의 응답 또는 hello 요청에서 순차적으로 실행 되는 문 컬렉션 됩니다. 정책 설명은 리터럴 텍스트 값, 정책 식 및 속성을 사용하여 생성할 수 있습니다. 

각 API 관리 서비스 인스턴스는 전역 toohello 서비스 인스턴스가 포함 된 키/값 쌍의 properties 컬렉션. 이러한 속성에는 모든 API 구성 및 정책에서 상수 문자열 값을 사용 하는 toomanage 수 있습니다. 각 속성에는 hello 특성 뒤에 있습니다.

| 특성 | 형식 | 설명 |
| --- | --- | --- |
| Name |string |hello 속성의 hello 이름입니다. 문자, 숫자, 마침표, 대시 및 밑줄 문자만 포함할 수 있습니다. |
| 값 |string |hello hello 속성 값입니다. 비워 두거나 공백만으로 구성될 수 없습니다. |
| Secret |부울 |여부 hello 값 암호 이며을 암호화할지 여부를 결정 합니다. |
| 태그들 |문자열의 배열 |선택 사항 태그를 삽입 하는 사용 되는 toofilter hello 속성 목록 수를 제공 합니다. |

속성은 hello hello 게시자 포털에 구성 **속성** 탭 합니다. 다음 예제는 hello, 세 가지 속성이 구성 됩니다.

![properties][api-management-properties]

속성 값은 리터럴 문자열 및 [정책 식](https://msdn.microsoft.com/library/azure/dn910913.aspx)을 포함할 수 있습니다. hello 다음 표에 hello 이전 세 샘플 속성 및 해당 특성 있습니다. 값을 hello `ExpressionProperty` 은 포함 하는 문자열을 반환 하는 정책 식을 hello 현재 날짜 및 시간입니다. 속성을 hello `ContosoHeaderValue` 은 표시 되어는 암호로 있으므로 해당 값이 표시 됩니다.

| 이름 | 값 | Secret | 태그 |
| --- | --- | --- | --- |
| ContosoHeader |TrackingId |False |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |True |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |False | |

## <a name="toouse-a-property"></a>toouse 속성
정책에서 속성 toouse와 같은 이중 중괄호 쌍 내 위치 hello 속성 이름은 `{{ContosoHeader}}`hello 다음 예제에에서 나온 것 처럼 합니다.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

이 예제에서는 `ContosoHeader` 에 헤더의 hello 이름으로 사용 되는 `set-header` 정책 및 `ContosoHeaderValue` 해당 헤더의 hello 값으로 사용 됩니다. 이 정책은 요청 또는 응답 toohello API 관리 게이트웨이 중 평가 되는 경우 `{{ContosoHeader}}` 및 `{{ContosoHeaderValue}}` 해당 각 속성 값으로 대체 합니다.

전체 특성 또는 요소 값 hello 앞의 예제에 표시 된 대로 속성을 사용할 수 있지만 수에 삽입 하거나 수도 hello 다음 예제와 같이 리터럴 텍스트 식의 일부와 결합:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

또한 속성은 정책 식을 포함할 수 있습니다. 다음 예제는 hello에서 hello `ExpressionProperty` 사용 됩니다.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

이 정책을 평가할 때 `{{ExpressionProperty}}`는 해당 값 `@(DateTime.Now.ToString())`으로 바뀝니다. Hello 값에는 정책 식 이므로 hello 식이 계산 되 고 hello 정책 실행을 계속 진행 합니다.

에서 테스트할 수 있습니다이 out hello 개발자 포털에 속성을 가진 정책이 범위에는 작업을 호출 하 여 합니다. 다음 예제는 hello, 작업 hello 두 개의 이전 예제와 호출 `set-header` 속성을 사용 하 여 정책을 합니다. 참고 hello 응답 속성을 가진 정책을 사용 하 여 구성 된 두 개의 사용자 지정 헤더를 포함 합니다.

![개발자 포털][api-management-send-results]

Hello 보면 [관리자 API 추적](api-management-howto-api-inspector.md) hello 두 이전 샘플 정책을 속성을 포함 하는 호출에 대 한 두 hello를 볼 수 있습니다 `set-header` hello 정책 식 뿐만 아니라 삽입 된 hello 속성 값을 사용 하 여 정책을 hello 정책 식을 포함 하는 hello 속성에 대 한 평가 합니다.

![API 검사기 추적][api-management-api-inspector-trace]

속성 값은 정책 식을 포함할 수 있지만 다른 속성을 포함할 수는 없습니다. 속성 참조가 포함 된 텍스트와 같은 속성 값에 사용 되 면 `Property value text {{MyProperty}}`, 속성 참조 되지 및 hello 속성 값의 일부분으로 포함 됩니다.

## <a name="toocreate-a-property"></a>toocreate 속성
toocreate 속성을 클릭 하 여 **속성 추가** hello에 **속성** 탭 합니다.

![속성 추가][api-management-properties-add-property-menu]

**이름** 및 **값**은 필수 값입니다. 이 속성 값이 되는 암호를 확인 hello **이 암호는** 확인란을 선택 합니다. 속성을 구성 된 하나 이상의 선택적 태그 toohelp를 입력 하 고 클릭 **저장**합니다.

![속성 추가][api-management-properties-add-property]

새 속성을 저장할 때 hello **검색 속성** 텍스트 상자는 hello 새 속성의 hello 이름으로 채워지고 hello 새 속성이 표시 됩니다. 모든 속성의 선택을 취소 toodisplay hello **검색 속성** textbox enter 키를 누릅니다.

![properties][api-management-properties-property-saved]

Hello REST API를 사용 하는 속성을 만드는 방법에 대 한 정보를 참조 하십시오. [hello REST API를 사용 하 여 속성을 만들](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put)합니다.

## <a name="tooedit-a-property"></a>tooedit 속성
tooedit 속성을 클릭 하 여 **편집** hello 속성 tooedit 옆에 있는 합니다.

![속성 편집][api-management-properties-edit]

원하는 항목을 변경하고 **저장**을 클릭합니다. Hello 속성 이름을 변경 하면 해당 속성을 참조 하는 모든 정책은 자동으로 업데이트 된 toouse hello에 대 한 새 이름을 사용 됩니다.

![속성 편집][api-management-properties-edit-property]

Hello REST API를 사용 하는 속성을 편집에 대 한 자세한 내용은 참조 하십시오. [hello REST API를 사용 하는 속성을 편집](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch)합니다.

## <a name="toodelete-a-property"></a>toodelete 속성
toodelete 속성을 클릭 하 여 **삭제** hello 속성 toodelete 옆에 있는 합니다.

![속성 삭제][api-management-properties-delete]

클릭 **예, 삭제할** tooconfirm 합니다.

![삭제 확인][api-management-delete-confirm]

> [!IMPORTANT]
> Hello 속성은 정책에 의해 참조 되는 경우 수 없게 됩니다 toosuccessfully가 hello 속성을 사용 하는 모든 정책에서 제거할 때까지 삭제 합니다.
> 
> 

Hello REST API를 사용 하는 속성을 삭제에 대 한 정보를 참조 하십시오. [hello REST API를 사용 하 여 속성 삭제](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete)합니다.

## <a name="toosearch-and-filter-properties"></a>toosearch 및 필터 속성
hello **속성** 탭 검색 및 필터링 기능 toohelp 프로그램 속성 관리를 포함 합니다. hello에 검색 용어를 입력 하는 속성 이름으로 toofilter hello 속성 목록 **검색 속성** 텍스트 상자에 붙여넣습니다. 모든 속성의 선택을 취소 toodisplay hello **검색 속성** textbox enter 키를 누릅니다.

![검색][api-management-properties-search]

태그 값으로 toofilter hello 속성 목록 hello에 하나 이상의 태그를 입력 **태그로 필터** 텍스트 상자에 붙여넣습니다. 모든 속성의 선택을 취소 toodisplay hello **태그로 필터** textbox enter 키를 누릅니다.

![Filter][api-management-properties-filter]

## <a name="next-steps"></a>다음 단계
* 정책 작업에 대한 자세한 정보
  * [API 관리의 정책](api-management-howto-policies.md)
  * [정책 참조](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [정책 식](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>비디오 개요 보기
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

