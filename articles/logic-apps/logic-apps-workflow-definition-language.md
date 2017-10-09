---
title: "aaaWorkflow 정의 언어 스키마-Azure 논리 앱 | Microsoft Docs"
description: "Azure 논리 앱에 대 한 hello 워크플로 정의 스키마를 기준으로 워크플로 정의 합니다."
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Azure Logic Apps에 대한 워크플로 정의 언어 스키마

워크플로 정의 논리 앱의 일부로 실행 되는 hello 실제 논리를 포함 합니다. 이 정의는 하나 이상의 hello 논리 앱을 시작 하는 트리거 및 논리 앱 tootake hello에 대 한 하나 이상의 동작이 포함 됩니다.  
  
## <a name="basic-workflow-definition-structure"></a>기본 워크플로 정의 구조

Hello 워크플로 정의의 기본 구조는 다음과 같습니다.  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> hello [워크플로 관리 REST API](https://docs.microsoft.com/rest/api/logic/workflows) 설명서에는 방법에 대 한 정보가 toocreate 논리 앱 워크플로 및 관리 합니다.
  
|요소 이름|필수|설명|  
|------------------|--------------|-----------------|  
|$schema|아니요|Hello 버전의 hello 정의 언어를 설명 하는 hello JSON 스키마 파일에 대 한 hello 위치를 지정 합니다. 정의를 외부에서 참조할 때 이 위치가 필요합니다. 이 문서에 대 한 hello 위치는입니다. <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|아니요|Hello 정의 버전을 지정합니다. Hello 정의 사용 하 여 워크플로 배포 하면이 값 toomake hello 오른쪽 정의 사용 되도록 사용할 수 있습니다.|  
|매개 변수|아니요|Hello 정의에 사용 되는 tooinput 데이터 매개 변수를 지정 합니다. 최대 50개의 매개 변수를 정의할 수 있습니다.|  
|트리거|아니요|Hello 워크플로 시작 하는 hello 트리거에 대 한 정보를 지정 합니다. 최대 10개의 트리거를 정의할 수 있습니다.|  
|actions|아니요|Hello 흐름 실행 될 때 수행 된 작업을 지정 합니다. 최대 250개의 작업을 정의할 수 있습니다.|  
|outputs|아니요|배포 된 hello 리소스에 대 한 정보를 지정합니다. 최대 10개의 출력을 정의할 수 있습니다.|  
  
## <a name="parameters"></a>매개 변수

이 섹션 배포 시 hello 워크플로 정의에 사용 되는 모든 hello 매개 변수를 지정 합니다. 모든 매개 변수는 hello 정의의 다른 섹션에서 사용 하려면 먼저이 섹션에 선언 되어야 합니다.  
  
hello 다음 예제는 매개 변수 정의의 hello 구조.  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|요소 이름|필수|설명|  
|------------------|--------------|-----------------|  
|type|예|**형식**: string <p> **선언**: `"parameters": {"parameter1": {"type": "string"}` <p> **사양**: `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **형식**: securestring <p> **선언**: `"parameters": {"parameter1": {"type": "securestring"}}` <p> **사양**: `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **형식**: int <p> **선언**: `"parameters": {"parameter1": {"type": "int"}}` <p> **사양**: `"parameters": {"parameter1": {"value" : 5}}` <p> **형식**: bool <p> **선언**: `"parameters": {"parameter1": {"type": "bool"}}` <p> **사양**: `"parameters": {"parameter1": { "value": true }}` <p> **형식**: array <p> **선언**: `"parameters": {"parameter1": {"type": "array"}}` <p> **사양**: `"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **형식**: object <p> **선언**: `"parameters": {"parameter1": {"type": "object"}}` <p> **사양**: `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **형식**: secureobject <p> **선언**: `"parameters": {"parameter1": {"type": "object"}}` <p> **사양**: `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **참고:** hello `securestring` 및 `secureobject` 형식은에 반환 되지 않습니다 `GET` 작업 합니다. 모든 암호, 키 및 비밀은 이 형식을 사용해야 합니다.|  
|defaultValue|아니요|값이 없는 시간에 지정 됩니다 hello hello 리소스를 만들 때 hello 매개 변수에 대 한 hello 기본값을 지정 합니다.|  
|allowedValues|아니요|Hello 매개 변수에 대해 허용 된 값의 배열을 지정합니다.|  
|metadata|아니요|Hello 매개 변수를 읽을 수 있는 설명 등 Visual Studio 또는 다른 도구에서 사용 하는 디자인 타임 데이터에 대 한 추가 정보를 지정 합니다.|  
  
이 예제는 작업의 hello 본문 섹션에는 매개 변수를 사용 하는 방법을 보여 줍니다.  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 매개 변수는 출력에도 사용할 수 있습니다.  
  
## <a name="triggers-and-actions"></a>트리거 및 작업  

트리거 및 작업 워크플로 실행에 참여할 수 있는 hello 호출을 지정 합니다. 이 섹션에 대한 자세한 내용은 [워크플로 작업 및 트리거](logic-apps-workflow-actions-triggers.md)를 참조하세요.
  
## <a name="outputs"></a>outputs  

출력은 워크플로 실행에서 반환할 수 있는 정보를 지정합니다. 예를 들어 특정 상태 또는 실행 시 마다 tootrack를 구할 값이 있으면 출력을 실행 하는 hello에 대 한 데이터를 포함할 수 있습니다. hello 데이터 hello Azure 포털에서에서 해당 실행에 대 한 hello 관리 UI 및 해당 실행에 대 한 hello 관리 REST API에에서 표시 합니다. 대시보드를 만들기 위한 PowerBI 같은 이러한 출력 tooother 외부 시스템 진행 될 수도 있습니다. 출력은 *하지* hello 서비스 REST API에서 toorespond tooincoming 요청을 사용 합니다. hello를 사용 하 여 toorespond tooan 들어오는 요청 `response` 동작 유형, 예를 들면 같습니다.
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|요소 이름|필수|설명|  
|------------------|--------------|-----------------|  
|key1|예|Hello hello 출력에 대 한 키 식별자를 지정합니다. 대체 **key1** toouse tooidentify hello 출력 원하는 이름으로 합니다.|  
|값|예|Hello 출력의 hello 값을 지정 합니다.|  
|type|예|지정 된 hello 값에 대 한 hello 유형을 지정 합니다. 가능한 값 형식은 다음과 같습니다. <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>식  

Hello 정의의 JSON 값, 리터럴일 수 또는 hello 정의 사용할 때 계산 되는 식이 될 수 있습니다. 예:  
  
```json
"name": "value"
```

 또는  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> 일부 식은 hello hello 실행 시작에서 존재 하지 않을 런타임 작업에서 값을 가져옵니다. 사용할 수 있습니다 **함수** toohelp 이러한 값 중 일부를 검색 합니다.  
  
식은 JSON 문자열 값에서 어느 위치에나 나타날 수 있으며 그 결과 항상 다른 JSON 값이 발생합니다. JSON 값에 대 한 식이 결정된 toobe를 수행한 hello 식의 본문이 hello hello 기호를 제거 하 여 추출 됩니다 (@). @로 시작하는 리터럴 문자열이 필요한 경우 해당 문자열은 @@를 사용하여 이스케이프해야 합니다. hello 다음 예제에서는 식의 평가 방법  
  
|JSON 값|결과|  
|----------------|------------|  
|"parameters"|'parameters' hello 문자가 반환 됩니다.|  
|"parameters[1]"|'parameters [1]' hello 문자가 반환 됩니다.|  
|"@@"|'@'를 포함하는 1개 문자열이 반환됩니다.|  
|" @"|' @'를 포함하는 2개 문자열이 반환됩니다.|  
  
*문자열 보간*을 사용하면 식이 `@{ ... }`로 묶인 문자열 내부에 나타날 수도 있습니다. 예: <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

hello 결과 항상이 기능이 비슷한 toohello 낮추는 문자열로 `concat` 함수입니다. `myNumber`를 `42`로, `myString`을 `sampleString`으로 정의했다고 가정해 보겠습니다.  
  
|JSON 값|결과|  
|----------------|------------|  
|"@parameters('myString')"|`sampleString`을 문자열로 반환합니다.|  
|"@{parameters('myString')}"|`sampleString`을 문자열로 반환합니다.|  
|"@parameters('myNumber')"|`42`를 *숫자*로 반환합니다.|  
|"@{parameters('myNumber')}"|`42`를 *문자열*로 반환합니다.|  
|"Answer is: @{parameters('myNumber')}"|반환 문자열 hello `Answer is: 42`합니다.|  
|"@concat('Answer is: ', string(parameters('myNumber')))"|Hello 문자열을 반환`Answer is: 42`|  
|"Answer is: @@{parameters('myNumber')}"|반환 문자열 hello `Answer is: @{parameters('myNumber')}`합니다.|  
  
## <a name="operators"></a>연산자  

연산자는 식 또는 함수에서 사용할 수 있는 hello 문자입니다. 
  
|연산자|설명|  
|--------------|-----------------|  
|에서도 확인할 수 있습니다.|hello 점 연산자는 개체의 속성을 tooreference 수 있습니다.|  
|?|hello 물음표 연산자를 사용 하면 런타임 오류가 없는 개체의 null 속성을 참조할 수 있습니다. 이 식 toohandle null을 사용할 수는 예를 들어 출력을 트리거합니다. <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|hello 작은따옴표는 hello 유일한 방법은 toowrap 문자열 리터럴을입니다. 이 문장 부호 hello 전체 식에서 래핑하는 hello JSON 따옴표와 충돌 하기 때문에 식 내부 큰따옴표를 사용할 수 없습니다.|  
|[]|hello 대괄호 특정 인덱스를 가진 배열에서 값을 사용 하는 tooget 될 수 있습니다. 예를 들어, 전달 되는 작업이 있는 경우 `range(0,10)`toohello에 `forEach` 함수, 배열 아웃이 함수 tooget 항목을 사용할 수 있습니다.  <p>`myArray[item()]`|  
  
## <a name="functions"></a>함수  

또한 식 내에서 함수를 호출할 수도 있습니다. hello 다음 표에 사용할 수 있는 hello 함수 식에 있습니다.  
  
|식|평가|  
|----------------|----------------|  
|"@function('Hello')"|호출 hello 함수 멤버 hello 첫 번째 매개 변수로 hello 리터럴 문자열 Hello 함께 hello 정의 합니다.|  
|"@function('It's Cool!')"|리터럴 문자열 hello 함께 hello 정의 'It's Cool!' hello 함수 멤버를 호출 합니다. hello 첫 번째 매개 변수로|  
|"@function().prop1"|반환 값의 hello hello prop1 속성의 hello `myfunction` hello 정의의 멤버입니다.|  
|"@function('Hello').prop1"|호출은 hello 첫 번째 매개 변수 및 반환 hello prop1 개체의 속성으로 hello 함수 멤버와 'Hello' hello 리터럴 문자열 hello 정의의 hello 합니다.|  
|"@function(parameters('Hello'))"|Hello Hello 매개 변수를 평가 하 고 hello 값 toofunction 전달|  
  
### <a name="referencing-functions"></a>참조 함수  

이러한 함수 tooreference 출력 hello 논리 앱 또는 hello 논리 앱을 만들 때 전달 된 값에 다른 작업에서 사용할 수 있습니다. 예를 들어 hello 데이터 toouse 한 단계에서에서 참조할 수 있습니다 다른 것입니다.  
  
|함수 이름|설명|  
|-------------------|-----------------|  
|매개 변수|Hello 정의에 정의 된 매개 변수 값을 반환 합니다. <p>`parameters('password')` <p> **매개 변수 번호**: 1 <p> **이름**: Parameter <p> **설명**: 필수. hello 매개 변수 값이 포함의 hello 이름입니다.|  
|action|다른 JSON 이름 및 값 쌍 또는 hello 현재 런타임 동작의 hello 출력에서 해당 값을 식 tooderive를 수 있습니다. 다음 예제는 hello에서 propertyPath로 표시 되는 hello 속성 선택 사항입니다. PropertyPath를 지정 하지 않으면 hello 참조 toohello 전체 작업 개체입니다. 이 함수는 작업의 do-until 조건 내부에만 사용할 수 있습니다. <p>`action().outputs.body.propertyPath`|  
|actions|다른 JSON 이름 및 값 쌍 또는 hello 런타임 동작의 hello 출력에서 해당 값을 식 tooderive를 수 있습니다. 이러한 식은 한 작업이 다른 작업에 종속되어 있음을 명시적으로 선언합니다. 다음 예제는 hello에서 propertyPath로 표시 되는 hello 속성 선택 사항입니다. PropertyPath를 지정 하지 않으면 hello 참조 toohello 전체 작업 개체입니다. 이 두 요소 중 하나를 사용할 수 있습니다 또는 hello 요소 toospecify 종속성 조건을 하지만 hello에 대 한 두 toouse를 필요 하지 않은 같은 종속 리소스입니다. <p>`actions('myAction').outputs.body.propertyPath` <p> **매개 변수 번호**: 1 <p> **이름**: Action name <p> **설명**: 필수. 값이 포함 hello 동작의 hello 이름입니다. <p> Hello 작업 개체에서 사용할 수 있는 속성은 같습니다. <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Hello 참조 [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=850646) 해당 속성에 대 한 자세한 내용은 합니다.|
|trigger|다른 JSON 이름 및 값 쌍 또는 hello 런타임 트리거의 hello 출력에서 해당 값을 식 tooderive를 수 있습니다. 다음 예제는 hello에서 propertyPath로 표시 되는 hello 속성 선택 사항입니다. PropertyPath를 지정 하지 않으면 hello 참조 toohello 전체 트리거 개체입니다. <p>`trigger().outputs.body.propertyPath` <p>입력 한 트리거 내에서 사용 하는 경우 hello 함수 hello 이전 실행의 hello 출력을 반환 합니다. 그러나 사용 하는 트리거 조건 내 경우 hello `trigger` 함수 hello 현재 실행의 hello 출력을 반환 합니다. <p> Hello 트리거 개체에 사용할 수 있는 속성은 같습니다. <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Hello 참조 [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=850644) 해당 속성에 대 한 자세한 내용은 합니다.|
|actionOutputs|이 함수는 `actions('actionName').outputs`의 약식입니다. <p> **매개 변수 번호**: 1 <p> **이름**: Action name <p> **설명**: 필수. 값이 포함 hello 동작의 hello 이름입니다.|  
|actionBody 및 body|이 함수는 `actions('actionName').outputs.body`의 약식입니다. <p> **매개 변수 번호**: 1 <p> **이름**: Action name <p> **설명**: 필수. 값이 포함 hello 동작의 hello 이름입니다.|  
|triggerOutputs|이 함수는 `trigger().outputs`의 약식입니다.|  
|triggerBody|이 함수는 `trigger().outputs.body`의 약식입니다.|  
|항목|내부 반복 작업을 사용 하는 경우이 함수는 hello 동작의이 반복에 대 한 hello 배열에 있는 hello 항목을 반환 합니다. 예를 들어 메시지 배열의 각 항목에 대해 실행하는 작업이 있는 경우 다음 구문을 사용할 수 있습니다. <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>컬렉션 함수  

이러한 함수는 컬렉션을 통해 작동 하 고 일반적으로 tooArrays, 문자열 및 경우에 따라 사전을 적용 합니다.  
  
|함수 이름|설명|  
|-------------------|-----------------|  
|contains|사전에 키가 포함되거나, 목록에 값이 포함되거나, 문자열에 하위 문자열이 포함된 경우 true를 반환합니다. 예를 들어 이 함수는 `true`를 반환합니다. <p>`contains('abacaba','aca')` <p> **매개 변수 번호**: 1 <p> **이름**: Within collection <p> **설명**: 필수. 내 hello 컬렉션 toosearch 합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Find object <p> **설명**: 필수. hello 내부 개체 toofind hello **컬렉션 내에서**합니다.|  
|length|반환 hello 배열 또는 문자열에 있는 요소의 수입니다. 예를 들어 이 함수는 `3`을 반환합니다.  <p>`length('abc')` <p> **매개 변수 번호**: 1 <p> **이름**: Collection <p> **설명**: 필수. 어떤 tooget hello 길이 대 한 hello 컬렉션입니다.|  
|empty|개체, 배열 또는 문자열이 비어 있으면 true를 반환합니다. 예를 들어 이 함수는 `true`를 반환합니다. <p>`empty('')` <p> **매개 변수 번호**: 1 <p> **이름**: Collection <p> **설명**: 필수. 비어 있는 경우 컬렉션 toocheck을 hello 합니다.|  
|교집합|전달된 배열 또는 개체 간에 공통의 요소가 있는 단일 배열 또는 개체를 반환합니다. 예를 들어 이 함수는 `[1, 2]`을 반환합니다. <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>hello 함수에 대 한 hello 매개 변수 개체의 집합 또는 배열 (하지 둘 모두) 집합이 수 있습니다. Hello로 개체 두 개가 동일한 이름을, hello 최종 개체에 해당 이름의 hello 마지막 개체 표시 합니다. <p> **매개 변수 번호**: 1 ... *n* <p> **이름**: Collection *n* <p> **설명**: 필수. hello 컬렉션 tooevaluate 합니다. 개체는 tooappear hello 결과에 전달 된 모든 컬렉션에 있어야 합니다.|  
|union|단일 배열 또는 개체 배열 또는 개체에 전달 된 toothis 함수 hello 요소가 모두 반환 합니다. 예를 들어 이 함수는 `[1, 2, 3, 10, 101]`을 반환합니다. <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>hello 함수에 대 한 hello 매개 변수 개체의 집합 또는 배열 (하지는 혼합 된 그) 집합이 수 있습니다. Hello 최종 출력에 hello 이름과 같은 이름을 사용 하 여 두 개체 있을 경우 해당 이름의 마지막 개체 hello hello 최종 개체에 나타납니다. <p> **매개 변수 번호**: 1 ... *n* <p> **이름**: Collection *n* <p> **설명**: 필수. hello 컬렉션 tooevaluate 합니다. Hello 컬렉션에 표시 되는 개체는 또한 hello 결과에 나타납니다.|  
|first|반환 hello hello 배열의 첫 번째 요소 또는 문자열이 전달 되었습니다. 예를 들어 이 함수는 `0`을 반환합니다. <p>`first([0,2,3])` <p> **매개 변수 번호**: 1 <p> **이름**: Collection <p> **설명**: 필수. hello 컬렉션 tootake hello 첫 번째 개체입니다.|  
|last|반환 hello hello 배열에서 마지막 요소 또는 문자열이 전달 되었습니다. 예를 들어 이 함수는 `3`을 반환합니다. <p>`last('0123')` <p> **매개 변수 번호**: 1 <p> **이름**: Collection <p> **설명**: 필수. hello 컬렉션 tootake hello 마지막 개체입니다.|  
|take|반환 먼저 hello **Count** hello 배열 또는 문자열에서 요소를 전달 합니다. 예를 들어 이 함수는 `[1, 2]`을 반환합니다.  <p>`take([1, 2, 3, 4], 2)` <p> **매개 변수 번호**: 1 <p> **이름**: Collection <p> **설명**: 필수. tootake 먼저 hello에서 hello 컬렉션 **Count** 개체입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Count <p> **설명**: 필수. hello에서 개체 tootake 수가 hello **컬렉션**합니다. 양의 정수여야 합니다.|  
|skip|반환 hello 인덱스에서 시작 하는 hello 배열의 요소 **Count**합니다. 예를 들어 이 함수는 `[3, 4]`을 반환합니다. <p>`skip([1, 2 ,3 ,4], 2)` <p> **매개 변수 번호**: 1 <p> **이름**: Collection <p> **설명**: 필수. 먼저 컬렉션 tooskip hello hello **Count** 에서 개체를 합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Count <p> **설명**: 필수. hello 앞에서 개체 tooremove 수가 hello **컬렉션**합니다. 양의 정수여야 합니다.|  
|join|구분 기호로 조인된 배열의 각 항목이 있는 문자열을 반환합니다. 예를 들어 `"1,2,3,4"`를 반환합니다.<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **매개 변수 번호**: 1<br /><br /> **이름**: Collection<br /><br /> **설명**: 필수. hello 컬렉션 toojoin 항목입니다.<br /><br /> **매개 변수 번호**: 2<br /><br /> **이름**: Delimiter<br /><br /> **설명**: 필수. hello 문자열 toodelimit 된 항목입니다.|  
  
### <a name="string-functions"></a>문자열 함수

함수에만 다음 hello toostrings를 적용 됩니다. 문자열에서 몇 가지 컬렉션 함수도 사용할 수 있습니다.  
  
|함수 이름|설명|  
|-------------------|-----------------|  
|concat|임의 개수 문자열을 함께 결합합니다. 예를 들어 매개 변수 1이 `p1`이면 이 함수는 `somevalue-p1-somevalue`를 반환합니다. <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **매개 변수 번호**: 1 ... *n* <p> **이름**: String *n* <p> **설명**: 필수. 단일 문자열로 hello 문자열 toocombine 합니다.|  
|substring|문자열의 하위 집합을 반환합니다. 예를 들어 이 함수는 `abc`를 반환합니다. <p>`substring('somevalue-abc-somevalue',10,3)` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. 어떤 hello를 부분 문자열을 가져오는 hello 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Start index <p> **설명**: 필수. hello 인덱스 매개 변수 1에에서 hello 부분 문자열이 시작 되는 위치입니다. <p> **매개 변수 번호**: 3 <p> **이름**: Length <p> **설명**: 필수. hello 부분 문자열의 hello 길이입니다.|  
|replace|문자열을 지정된 문자열로 바꿉니다. 예를 들어 이 함수는 `hello new string`을 반환합니다. <p>`replace('hello old string', 'old', 'new')` <p> **매개 변수 번호**: 1 <p> **이름**: string <p> **설명**: 필수. 매개 변수 2에 대 한 검색 해 서 매개 변수 2는 매개 변수 1에서에서 발견 된 경우 매개 변수 3으로 업데이트 하는 hello 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Old string <p> **설명**: 필수. 매개 변수 3, 매개 변수 1에에서 일치 하는 경우 문자열 tooreplace hello <p> **매개 변수 번호**: 3 <p> **이름**: New string <p> **설명**: 필수. hello 매개 변수 1에에서 일치 하는 경우 매개 변수 2에에서 사용 되는 tooreplace hello 문자열 즉 문자열입니다.|  
|GUID|이 함수는 전역적으로 고유한 문자열(GUID)을 생성합니다. 예를 들어 이 함수는 다음 GUID를 생성할 수 있습니다. `c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **매개 변수 번호**: 1 <p> **이름**: Format <p> **설명**: 선택 사항. 나타내는 단일 형식 지정자 [어떻게 tooformat hello이 Guid의 값](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx)합니다. hello 형식 매개 변수는 "N", "D", "B", "P" 또는 "X" 될 수 있습니다. 형식이 제공되지 않으면 "D"가 사용됩니다.|  
|toLower|문자열 toolowercase를 변환합니다. 예를 들어 이 함수는 `two by two is four`을 반환합니다. <p>`toLower('Two by Two is Four')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 문자열 tooconvert toolower 대/소문자 구분 합니다. Hello 문자열의 문자에 해당 하는 소문자 이거나 없는 경우 hello 문자가 변경 되지 않고 문자열을 반환 하는 hello에 포함 됩니다.|  
|toUpper|문자열 toouppercase를 변환합니다. 예를 들어 이 함수는 `TWO BY TWO IS FOUR`을 반환합니다. <p>`toUpper('Two by Two is Four')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 문자열 tooconvert tooupper 대/소문자 구분 합니다. Hello 문자열의 문자에 해당 하는 대문자 이거나 없는 경우 hello 문자가 변경 되지 않고 문자열을 반환 하는 hello에 포함 됩니다.|  
|indexof|하 문자열 사례 내 값의 hello 인덱스를 찾습니다. 예를 들어 이 함수는 `7`을 반환합니다. <p>`indexof('hello, world.', 'world')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 값을 포함할 수 있는 hello 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: String <p> **설명**: 필수. hello 값 toosearch hello의 인덱스입니다.|  
|lastindexof|하 hello 문자열 case 내에 있는 값의 마지막 인덱스를 찾습니다. 예를 들어 이 함수는 `3`을 반환합니다. <p>`lastindexof('foofoo', 'foo')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 값을 포함할 수 있는 hello 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: String <p> **설명**: 필수. hello 값 toosearch hello의 인덱스입니다.|  
|startswith|Hello 문자열 값 사례와 하 시작을 확인 합니다. 예를 들어 이 함수는 `true`을 반환합니다. <p>`startswith('hello, world', 'hello')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 값을 포함할 수 있는 hello 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: String <p> **설명**: 필수. hello 값 hello 문자열으로 시작할 수 있습니다.|  
|endswith|Hello 문자열 값 사례와 하 끝납니다 확인 합니다. 예를 들어 이 함수는 `true`을 반환합니다. <p>`endswith('hello, world', 'world')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 값을 포함할 수 있는 hello 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: String <p> **설명**: 필수. hello 값 hello 문자열으로 끝날 수 있습니다.|  
|분할|구분 기호를 사용 하 여 hello 문자열을 분할 합니다. 예를 들어 이 함수는 `["a", "b", "c"]`을 반환합니다. <p>`split('a;b;c',';')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. 분할 된 hello 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: String <p> **설명**: 필수. hello 구분 기호입니다.|  
  
### <a name="logical-functions"></a>논리 함수  

이러한 함수는 조건 내부에서 유용 되며 사용 되는 tooevaluate 논리의 형식일 수 있습니다.  
  
|함수 이름|설명|  
|-------------------|-----------------|  
|equals|두 값이 같으면 true를 반환합니다. 예를 들어 매개 변수 1이 어떤 값이면 이 함수는 `true`를 반환합니다. <p>`equals(parameters('parameter1'), 'someValue')` <p> **매개 변수 번호**: 1 <p> **이름**: Object 1 <p> **설명**: 필수. 개체 toocompare 너무 hello**개체 2**합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Object 2 <p> **설명**: 필수. 개체 toocompare 너무 hello**개체 1**합니다.|  
|less|Hello 첫 번째 인수 보다 작으면 hello 둘째 true를 반환 합니다. 값은 integer, float 또는 string 형식만 가능합니다. 예를 들어 이 함수는 `true`를 반환합니다. <p>`less(10,100)` <p> **매개 변수 번호**: 1 <p> **이름**: Object 1 <p> **설명**: 필수. 이 경우 개체 toocheck hello 보다 작은 **개체 2**합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Object 2 <p> **설명**: 필수. 보다 큰 경우 개체 toocheck hello **개체 1**합니다.|  
|lessOrEquals|Hello 첫 번째 인수는 경우 true를 반환 미만 또는 toohello 값이 두 번째입니다. 값은 integer, float 또는 string 형식만 가능합니다. 예를 들어 이 함수는 `true`를 반환합니다. <p>`lessOrEquals(10,10)` <p> **매개 변수 번호**: 1 <p> **이름**: Object 1 <p> **설명**: 필수. 너무 크거나 작은 경우 개체 toocheck hello**개체 2**합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Object 2 <p> **설명**: 필수. 보다 큰 경우 개체 toocheck hello 또는 값이 너무**개체 1**합니다.|  
|greater|Hello 첫 번째 인수가 두 번째 hello 보다 큰 경우 true를 반환 합니다. 값은 integer, float 또는 string 형식만 가능합니다. 예를 들어 이 함수는 `false`를 반환합니다.  <p>`greater(10,10)` <p> **매개 변수 번호**: 1 <p> **이름**: Object 1 <p> **설명**: 필수. 보다 큰 경우 개체 toocheck hello **개체 2**합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Object 2 <p> **설명**: 필수. 이 경우 개체 toocheck hello 보다 작은 **개체 1**합니다.|  
|greaterOrEquals|Hello 첫 번째 인수는 두 번째 toohello 보다 크거나 같은 경우 true를 반환 합니다. 값은 integer, float 또는 string 형식만 가능합니다. 예를 들어 이 함수는 `false`를 반환합니다. <p>`greaterOrEquals(10,100)` <p> **매개 변수 번호**: 1 <p> **이름**: Object 1 <p> **설명**: 필수. 보다 큰 경우 개체 toocheck hello 또는 값이 너무**개체 2**합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Object 2 <p> **설명**: 필수. 보다 작거나 같은 경우 개체 toocheck hello 너무**개체 1**합니다.|  
|and|두 매개 변수가 true이면 true를 반환합니다. 두 인수 toobe 부울 필요합니다. 예를 들어 이 함수는 `false`을 반환합니다. <p>`and(greater(1,10),equals(0,0))` <p> **매개 변수 번호**: 1 <p> **이름**: Boolean 1 <p> **설명**: 필수. 첫 번째 인수 해야 하는 hello `true`합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Boolean 2 <p> **설명**: 필수. 두 번째 인수 hello 여야 `true`합니다.|  
|또는|매개 변수 중 하나라도 true이면 true를 반환합니다. 두 인수 toobe 부울 필요합니다. 예를 들어 이 함수는 `true`을 반환합니다. <p>`or(greater(1,10),equals(0,0))` <p> **매개 변수 번호**: 1 <p> **이름**: Boolean 1 <p> **설명**: 필수. 첫 번째 인수 일 수 있는 hello `true`합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Boolean 2 <p> **설명**: 필수. 두 번째 인수 hello 될 수 있습니다 `true`합니다.|  
|not|Hello 매개 변수는 경우 true를 반환 `false`합니다. 두 인수 toobe 부울 필요합니다. 예를 들어 이 함수는 `true`을 반환합니다. <p>`not(contains('200 Success','Fail'))` <p> **매개 변수 번호**: 1 <p> **이름**: Boolean <p> **설명**: hello 매개 변수는 경우 true를 반환 `false`합니다. 두 인수 toobe 부울 필요합니다. 다음 함수는 `true`를 반환합니다. `not(contains('200 Success','Fail'))`|  
|if|Hello 식에서 발생 하는지 여부에 따라 지정 된 값을 반환 `true` 또는 `false`합니다.  예를 들어 이 함수는 `"yes"`을 반환합니다. <p>`if(equals(1, 1), 'yes', 'no')` <p> **매개 변수 번호**: 1 <p> **이름**: Expression <p> **설명**: 필수. 어떤 값 hello 식을 결정 하는 부울 값을 반환 해야 합니다. <p> **매개 변수 번호**: 2 <p> **이름**: True <p> **설명**: 필수. hello 식이 값 tooreturn hello `true`합니다. <p> **매개 변수 번호**: 3 <p> **이름**: False <p> **설명**: 필수. hello 식이 값 tooreturn hello `false`합니다.|  
  
### <a name="conversion-functions"></a>변환 함수  

이러한 함수는 각 hello 언어에서 hello 네이티브 형식 간에 사용 되는 tooconvert:  
  
- string  
  
- 정수  
  
- float  
  
- 부울  
  
- arrays  
  
- dictionaries  

-   forms  
  
|함수 이름|설명|  
|-------------------|-----------------|  
|int|Hello tooan 정수 매개 변수를 변환 합니다. 예를 들어 이 함수는 문자열이 아닌 숫자로 100을 반환합니다. <p>`int('100')` <p> **매개 변수 번호**: 1 <p> **이름**: Value <p> **설명**: 필수. 변환 된 tooan 정수가 hello 값입니다.|  
|string|Hello 매개 변수 tooa 문자열을 변환 합니다. 예를 들어 이 함수는 `'10'`을 반환합니다. <p>`string(10)` <p>또한 개체 tooa 문자열을 변환할 수 있습니다. 예를 들어 경우 hello, `myPar` 매개 변수는 하나의 속성이 있는 개체 `abc : xyz`,이 함수가 반환 후 `{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **매개 변수 번호**: 1 <p> **이름**: Value <p> **설명**: 필수. hello tooa 변환 된 문자열 값입니다.|  
|json :|Hello 매개 변수 tooa JSON 형식 값을 변환 하 고는의 반대 hello `string()`합니다. 예를 들어 이 함수는 문자열이 아닌 배열로 `[1,2,3]`을 반환합니다. <p>`json('[1,2,3]')` <p>마찬가지로, 문자열 tooan 개체로 변환할 수 있습니다. 예를 들어 이 함수는 `{ "abc" : "xyz" }`을 반환합니다. <p>`json('{"abc" : "xyz"}')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 문자열 변환 된 tooa 네이티브 형식 값입니다. <p>hello `json()` 함수 너무 입력 XML을 지원 합니다. 예를 들어 hello 매개 변수 값: <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>변환 된 toothis JSON은: <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|float|Hello 매개 변수 인수 tooa 부동 소수점 숫자를 변환 합니다. 예를 들어 이 함수는 `10.333`을 반환합니다. <p>`float('10.333')` <p> **매개 변수 번호**: 1 <p> **이름**: Value <p> **설명**: 필수. hello 변환 된 tooa 부동 소수점 숫자 값입니다.|  
|bool|Hello 매개 변수 tooa 부울 값으로 변환 합니다. 예를 들어 이 함수는 `false`을 반환합니다. <p>`bool(0)` <p> **매개 변수 번호**: 1 <p> **이름**: Value <p> **설명**: 필수. 값을 변환 된 tooa hello 부울입니다.|  
|coalesce|에 전달 하는 hello 인수에 hello 첫 번째 null이 아닌 개체를 반환 합니다. **참고**: 빈 문자열은 null이 아닙니다. 예를 들어 매개 변수 1 및 2가 정의되지 않은 경우 이 함수는 `fallback`을 반환합니다.  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **매개 변수 번호**: 1 ... *n* <p> **이름**: Object*n* <p> **설명**: 필수. null에 대 한 hello 개체 toocheck 합니다.|  
|base64|반환 hello hello 입력된 문자열의 base64 표현입니다. 예를 들어 이 함수는 `c29tZSBzdHJpbmc=`을 반환합니다. <p>`base64('some string')` <p> **매개 변수 번호**: 1 <p> **이름**: String 1 <p> **설명**: 필수. base64 표현으로 hello 문자열 tooencode 합니다.|  
|base64ToBinary|base64 인코딩 문자열의 이진 표현을 반환합니다. 이 함수에서의 이진 표현 hello를 반환 하는 예를 들어 `some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello base64 인코딩 문자열입니다.|  
|base64ToString|based64 인코딩 문자열의 문자열 표현을 반환합니다. 예를 들어 이 함수는 `some string`을 반환합니다. <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello base64 인코딩 문자열입니다.|  
|이진|값의 이진 표현을 반환합니다.  예를 들어 이 함수는 `some string`의 이진 표현을 반환합니다. <p>`binary('some string')` <p> **매개 변수 번호**: 1 <p> **이름**: Value <p> **설명**: 필수. hello 값 변환된 toobinary입니다.|  
|dataUriToBinary|데이터 URI의 이진 표현을 반환합니다. 이 함수에서의 이진 표현 hello를 반환 하는 예를 들어 `some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 데이터 URI tooconvert toobinary 표현입니다.|  
|dataUriToString|데이터 URI의 문자열 표현을 반환합니다. 예를 들어 이 함수는 `some string`을 반환합니다. <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **매개 변수 번호**: 1 <p> **이름**: String<p> **설명**: 필수. hello 데이터 URI tooconvert tooString 표현입니다.|  
|dataUri|값의 데이터 URI를 반환합니다. 예를 들어 이 함수는 데이터 URI `text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=`를 반환합니다. <p>`dataUri('some string')` <p> **매개 변수 번호**: 1<p> **이름**: Value<p> **설명**: 필수. hello 값 tooconvert toodata URI입니다.|  
|decodeBase64|입력 based64 문자열의 문자열 표현을 반환합니다. 예를 들어 이 함수는 `some string`을 반환합니다. <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 입력 based64 문자열의 문자열 표현을 반환합니다.|  
|encodeUriComponent|에 전달 되는 URL 이스케이프 hello 문자열입니다. 예를 들어 이 함수는 `You+Are%3ACool%2FAwesome`을 반환합니다. <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello에서 tooescape URL 안전 하지 않은 문자를 문자열입니다.|  
|decodeUriComponent|에 전달 되는 문자열을 URL 이스케이프 해제 hello입니다. 예를 들어 이 함수는 `You Are:Cool/Awesome`을 반환합니다. <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. hello 문자열 toodecode hello URL 안전 하지 않은 문자입니다.|  
|decodeDataUri|입력 데이터 URI 문자열의 이진 표현을 반환합니다. 이 함수에서의 이진 표현 hello를 반환 하는 예를 들어 `some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **매개 변수 번호**: 1 <p> **이름**: String <p> **설명**: 필수. 이진 표현으로 hello dataURI toodecode 합니다.|  
|uriComponent|값의 URI 인코딩 표현을 반환합니다. 예를 들어 이 함수는 `You+Are%3ACool%2FAwesome`을 반환합니다. <p>`uriComponent('You Are:Cool/Awesome')` <p> **매개 변수 번호**: 1<p> **이름**: String <p> **설명**: 필수. hello 문자열 toobe URI 인코딩됩니다.|  
|uriComponentToBinary|URI 인코딩 문자열의 이진 표현을 반환합니다. 예를 들어 이 함수는 `You Are:Cool/Awesome`의 이진 표현을 반환합니다. <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **매개 변수 번호**: 1 <p> **이름**: String<p> **설명**: 필수. hello URI 인코딩된 문자열입니다.|  
|uriComponentToString|URI 인코딩 문자열의 문자열 표현을 반환합니다. 예를 들어 이 함수는 `You Are:Cool/Awesome`을 반환합니다. <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **매개 변수 번호**: 1<p> **이름**: String<p> **설명**: 필수. hello URI 인코딩된 문자열입니다.|  
|xml|Hello 값의 XML 표현을 반환 합니다. 예를 들어 이 함수는 `'\<name>Alan\</name>'`으로 표시된 XML 콘텐츠를 반환합니다. <p>`xml('\<name>Alan\</name>')` <p>hello `xml()` 함수 너무 입력 JSON 개체를 지원 합니다. 예를 들어, 매개 변수를 hello `{ "abc": "xyz" }` 는 변환 된 tooXML 콘텐츠:`\<abc>xyz\</abc>` <p> **매개 변수 번호**: 1<p> **이름**: Value<p> **설명**: 필수. hello 값 tooconvert tooXML 합니다.|  
|xpath|Hello xpath 식을 계산 하는 값의 hello xpath 식과 일치 하는 XML 노드의 배열을 반환 합니다. <p> **예 1** <p>Hello 매개 변수 값을 가정 `p1` 이 XML의 문자열 표현입니다. <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>다음 코드는 `xpath(xml(parameters('p1'), '/lab/robot/name')` <p>다음을 반환합니다. <p>`[ <name>R1</name>, <name>R2</name> ]` <p>반면에 다음 코드는 <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>다음을 반환합니다. <p>`13` <p> <p> **예 2** <p>다음 XML 콘텐츠 지정된 hello: <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>다음 코드는 `@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>또는 다음 코드는 <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>다음을 반환합니다. <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>그리고 다음 코드는 `@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>다음을 반환합니다. <p>``xyz`` <p> **매개 변수 번호**: 1 <p> **이름**: Xml <p> **설명**: 필수. hello XML에는 tooevaluate hello XPath 식입니다. <p> **매개 변수 번호**: 2 <p> **이름**: XPath <p> **설명**: 필수. XPath 식 tooevaluate hello 합니다.|  
|array|Hello 매개 변수 tooan 배열을 변환 합니다. 예를 들어 이 함수는 `["abc"]`을 반환합니다. <p>`array('abc')` <p> **매개 변수 번호**: 1 <p> **이름**: Value <p> **설명**: 필수. hello 값은 변환 된 tooan 배열입니다.|
|createArray|Hello 매개 변수에서 배열을 만듭니다. 예를 들어 이 함수는 `["a", "c"]`을 반환합니다. <p>`createArray('a', 'c')` <p> **매개 변수 번호**: 1 ... *n* <p> **이름**: Any *n* <p> **설명**: 필수. 배열에 대 한 hello 값 toocombine 합니다.|
|triggerFormDataValue|양식 데이터 또는 트리거 양식 인코딩된 출력에서 hello 키 이름과 일치 하는 단일 값을 반환 합니다.  일치 항목이 여러 개이면 오류입니다.  예를 들어 hello 다음 반환 합니다 `bar`:`triggerFormDataValue('foo')`<br /><br />**매개 변수 번호**: 1<br /><br />**이름**: Key Name<br /><br />**설명**: 필수. hello hello 양식 데이터 값 tooreturn의 키 이름입니다.|
|triggerFormDataMultiValues|양식 데이터 또는 트리거 양식 인코딩된 출력에서 hello 키 이름과 일치 하는 값의 배열을 반환 합니다.  예를 들어 hello 다음 반환 합니다 `["bar"]`:`triggerFormDataValue('foo')`<br /><br />**매개 변수 번호**: 1<br /><br />**이름**: Key Name<br /><br />**설명**: 필수. hello 양식 데이터의 키 이름 hello tooreturn을 값입니다.|
|triggerMultipartBody|반환 hello hello 트리거의 부분 다중 파트 출력에 대 한 본문입니다.<br /><br />**매개 변수 번호**: 1<br /><br />**이름**: Index<br /><br />**설명**: 필수. hello 파트 tooretrieve의 hello 인덱스입니다.|
|formDataValue|양식 데이터 또는 폼 인코딩 작업 출력에서 hello 키 이름과 일치 하는 단일 값을 반환 합니다.  일치 항목이 여러 개이면 오류입니다.  예를 들어 hello 다음 반환 합니다 `bar`:`formDataValue('someAction', 'foo')`<br /><br />**매개 변수 번호**: 1<br /><br />**이름**: Action Name<br /><br />**설명**: 필수. 양식 데이터 또는 폼 인코딩 응답으로 hello 동작의 hello 이름입니다.<br /><br />**매개 변수 번호**: 2<br /><br />**이름**: Key Name<br /><br />**설명**: 필수. hello hello 양식 데이터 값 tooreturn의 키 이름입니다.|
|formDataMultiValues|양식 데이터 또는 폼 인코딩 작업 출력에서 hello 키 이름과 일치 하는 값의 배열을 반환 합니다.  예를 들어 hello 다음 반환 합니다 `["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**매개 변수 번호**: 1<br /><br />**이름**: Action Name<br /><br />**설명**: 필수. 양식 데이터 또는 폼 인코딩 응답으로 hello 동작의 hello 이름입니다.<br /><br />**매개 변수 번호**: 2<br /><br />**이름**: Key Name<br /><br />**설명**: 필수. hello 양식 데이터의 키 이름 hello tooreturn을 값입니다.|
|multipartBody|반환 작업의 부분을 여러 출력에 대 한 본문을 hello 합니다.<br /><br />**매개 변수 번호**: 1<br /><br />**이름**: Action Name<br /><br />**설명**: 필수. 다중 파트 응답으로 hello 동작의 hello 이름입니다.<br /><br />**매개 변수 번호**: 2<br /><br />**이름**: Index<br /><br />**설명**: 필수. hello 파트 tooretrieve의 hello 인덱스입니다.|

### <a name="math-functions"></a>수학 함수  

이 함수는 **integers** 및 **floats**의 숫자 형식에 사용할 수 있습니다.  
  
|함수 이름|설명|  
|-------------------|-----------------|  
|추가|가 두 숫자 hello 추가 hello 결과 반환 합니다. 예를 들어 이 함수는 `20.333`을 반환합니다. <p>`add(10,10.333)` <p> **매개 변수 번호**: 1 <p> **이름**: Summand 1 <p> **설명**: 필수. 숫자 tooadd 너무 hello**Summand 2**합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Summand 2 <p> **설명**: 필수. 숫자 tooadd 너무 hello**Summand 1**합니다.|  
|sub|두 숫자를 뺀 결과로 hello 결과 반환 합니다. 예를 들어 이 함수는 `-0.333`을 반환합니다. <p>`sub(10,10.333)` <p> **매개 변수 번호**: 1 <p> **이름**: Minuend <p> **설명**: 필수. hello 번호 **감수** 에서 제거 됩니다. <p> **매개 변수 번호**: 2 <p> **이름**: Subtrahend <p> **설명**: 필수. hello에서 숫자 tooremove hello **피 감수**합니다.|  
|mul|두 숫자 hello에서 hello 결과 반환 합니다. 예를 들어 이 함수는 `103.33`을 반환합니다. <p>`mul(10,10.333)` <p> **매개 변수 번호**: 1 <p> **이름**: Multiplicand 1 <p> **설명**: 필수. 숫자 toomultiply hello **승수 2** 사용 합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Multiplicand 2 <p> **설명**: 필수. 숫자 toomultiply hello **승수 1** 사용 합니다.|  
|div|Hello 두 숫자를 나눈 hello 결과 반환 합니다. 예를 들어 이 함수는 `1.0333`을 반환합니다. <p>`div(10.333,10)` <p> **매개 변수 번호**: 1 <p> **이름**: Dividend <p> **설명**: 필수. hello 하 여 숫자 toodivide hello **Divisor**합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Divisor <p> **설명**: 필수. hello 숫자 toodivide hello **피제수** 여 합니다.|  
|mod|(모듈로) hello 두 숫자를 나누고 hello 나머지를 반환 합니다. 예를 들어 이 함수는 `2`을 반환합니다. <p>`mod(10,4)` <p> **매개 변수 번호**: 1 <p> **이름**: Dividend <p> **설명**: 필수. hello 하 여 숫자 toodivide hello **Divisor**합니다. <p> **매개 변수 번호**: 2 <p> **이름**: Divisor <p> **설명**: 필수. hello 숫자 toodivide hello **피제수** 여 합니다. Hello, 나누기 hello 나머지 수행 되지 않습니다.|  
|Min|이 함수를 호출하는 데는 두 가지 다른 패턴이 있습니다. <p>여기 `min` 변수로 구성 된 배열을 hello 함수를 반환 하 고 `0`: <p>`min([0,1,2])` <p>또는 이 함수는 쉼표로 구분된 값 목록을 사용하고 `0`를 반환할 수도 있습니다. <p>`min(0,1,2)` <p> **참고**: 모든 값에는 숫자 여야 하며, hello 매개 변수 배열이 면 hello 배열에 있도록 tooonly 번호입니다. <p> **매개 변수 번호**: 1 <p> **이름**: Collection 또는 Value <p> **설명**: 필수. 배열을 값 toofind hello 최소 값 또는 hello 집합의 첫 번째 값입니다. <p> **매개 변수 번호**: 2 ... *n* <p> **이름**: Value *n* <p> **설명**: 선택 사항. Hello 첫 번째 매개 변수 값이 있으면 추가 값을 전달할 수는 다음 고 hello 전달 된 모든 값의 최소값 반환 됩니다.|  
|max|이 함수를 호출하는 데는 두 가지 다른 패턴이 있습니다. <p>여기 `max` 변수로 구성 된 배열을 hello 함수를 반환 하 고 `2`: <p>`max([0,1,2])` <p>또는 이 함수는 쉼표로 구분된 값 목록을 사용하고 `2`를 반환할 수도 있습니다. <p>`max(0,1,2)` <p> **참고**: 모든 값에는 숫자 여야 하며, hello 매개 변수 배열이 면 hello 배열에 있도록 tooonly 번호입니다. <p> **매개 변수 번호**: 1 <p> **이름**: Collection 또는 Value <p> **설명**: 필수. 배열을 값 toofind hello 최대 값 또는 hello 집합의 첫 번째 값입니다. <p> **매개 변수 번호**: 2 ... *n* <p> **이름**: Value *n* <p> **설명**: 선택 사항. Hello 첫 번째 매개 변수 값이 있으면 추가 값을 전달할 수는 다음 고 hello 전달 된 값 중 최대값 반환 됩니다.|  
|range|특정 숫자부터 시작되는 정수 배열을 생성합니다. 배열을 반환 하는 hello hello 길이 정의 합니다. <p>예를 들어 이 함수는 `[3,4,5,6]`을 반환합니다. <p>`range(3,4)` <p> **매개 변수 번호**: 1 <p> **이름**: Start index <p> **설명**: 필수. hello hello 배열의 첫 번째 정수입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Count <p> **설명**: 필수. 이 값은 정수의 hello 배열에 있는 hello 수입니다.|  
|rand|임의 생성 hello 내의 정수 범위 (첫 번째 끝에만 포함)를 지정 합니다. 예를 들어 다음 함수에서는 `0` 또는 '1'을 반환할 수 있습니다. <p>`rand(0,2)` <p> **매개 변수 번호**: 1 <p> **이름**: Minimum <p> **설명**: 필수. 반환 될 수 있는 가장 작은 정수 hello입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Maximum <p> **설명**: 필수. 이 값은 반환 될 수 있는 가장 큰 정수를 hello 후 hello 다음 정수입니다.|  
  
### <a name="date-functions"></a>날짜 함수  
  
|함수 이름|설명|  
|-------------------|-----------------|  
|utcnow|반환을 문자열로 예를 들어 현재 타임 스탬프를 hello: `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **매개 변수 번호**: 1 <p> **이름**: Format <p> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.|  
|addseconds|시간 (초) tooa 문자열 타임 스탬프를 전달 하는 정수 번호를 추가 합니다. hello 시간 (초)은 양수 또는 음수일 수 있습니다. 기본적으로 hello 결과 ISO 8601에서 문자열 형식 ("o") 서식 지정자를 제공 하지 않으면입니다. 예: `2015-03-15T13:27:00Z`: <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **매개 변수 번호**: 1 <p> **이름**: Timestamp <p> **설명**: 필수. Hello 시간을 포함 하는 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Seconds <p> **설명**: 필수. 시간 (초) tooadd hello 수입니다. 음수 toosubtract 초 수 있습니다. <p> **매개 변수 번호**: 3 <p> **이름**: Format <p> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.|  
|addminutes|분 tooa 문자열 타임 스탬프를 전달 하는 정수 번호를 추가 합니다. hello 시간 (분)은 양수 또는 음수일 수 있습니다. 기본적으로 hello 결과 ISO 8601에서 문자열 형식 ("o") 서식 지정자를 제공 하지 않으면입니다. 예: `2015-03-15T14:00:36Z`: <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **매개 변수 번호**: 1 <p> **이름**: Timestamp <p> **설명**: 필수. Hello 시간을 포함 하는 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Minutes <p> **설명**: 필수. 분 tooadd hello 수입니다. 음수 toosubtract 시간 (분) 될 수 있습니다. <p> **매개 변수 번호**: 3 <p> **이름**: Format <p> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.|  
|addhours|시간 tooa 문자열 타임 스탬프를 전달 하는 정수 번호를 추가 합니다. 시간 hello 수는 양수 또는 음수일 수 있습니다. 기본적으로 hello 결과 ISO 8601에서 문자열 형식 ("o") 서식 지정자를 제공 하지 않으면입니다. 예: `2015-03-16T01:27:36Z`: <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **매개 변수 번호**: 1 <p> **이름**: Timestamp <p> **설명**: 필수. Hello 시간을 포함 하는 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Hours <p> **설명**: 필수. 시간 tooadd hello 수입니다. 음수 toosubtract 시간 일 수 있습니다. <p> **매개 변수 번호**: 3 <p> **이름**: Format <p> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.|  
|adddays|일 tooa 문자열 타임 스탬프를 전달 하는 정수 번호를 추가 합니다. hello 일 수는 양수 또는 음수일 수 있습니다. 기본적으로 hello 결과 ISO 8601에서 문자열 형식 ("o") 서식 지정자를 제공 하지 않으면입니다. 예: `2015-02-23T13:27:36Z`: <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **매개 변수 번호**: 1 <p> **이름**: Timestamp <p> **설명**: 필수. Hello 시간을 포함 하는 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Days <p> **설명**: 필수. 일 tooadd hello 수입니다. 음수 toosubtract 일 수 있습니다. <p> **매개 변수 번호**: 3 <p> **이름**: Format <p> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.|  
|formatDateTime|날짜 형식으로 문자열을 반환합니다. 기본적으로 hello 결과 ISO 8601에서 문자열 형식 ("o") 서식 지정자를 제공 하지 않으면입니다. 예: `2015-02-23T13:27:36Z`: <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **매개 변수 번호**: 1 <p> **이름**: Date <p> **설명**: 필수. Hello 날짜를 포함 하는 문자열입니다. <p> **매개 변수 번호**: 2 <p> **이름**: Format <p> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.|  
|startOfHour|반환 hello hello 시간 tooa 문자열 타임 스탬프의 전달 된 시작 합니다. 예 `2017-03-15T13:00:00Z`:<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **매개 변수 번호**: 1<br /><br /> **이름**: Timestamp<br /><br /> **설명**: 필수. 이것이 hello 시간을 포함 하는 문자열입니다.<br /><br />**매개 변수 번호**: 2<br /><br /> **이름**: Format<br /><br /> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.|  
|startOfDay|반환 hello hello 일 tooa 문자열 타임 스탬프의 전달 된 시작 합니다. 예 `2017-03-15T00:00:00Z`:<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **매개 변수 번호**: 1<br /><br /> **이름**: Timestamp<br /><br /> **설명**: 필수. 이것이 hello 시간을 포함 하는 문자열입니다.<br /><br />**매개 변수 번호**: 2<br /><br /> **이름**: Format<br /><br /> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.| 
|startOfMonth|반환 hello hello 월 tooa 문자열 타임 스탬프의 전달 된 시작 합니다. 예 `2017-03-01T00:00:00Z`:<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **매개 변수 번호**: 1<br /><br /> **이름**: Timestamp<br /><br /> **설명**: 필수. 이것이 hello 시간을 포함 하는 문자열입니다.<br /><br />**매개 변수 번호**: 2<br /><br /> **이름**: Format<br /><br /> **설명**: 선택 사항. 중 하나는 [단일 형식 지정자 문자](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) 또는 [사용자 지정 형식 패턴이](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) 방법을 tooformat hello이 타임 스탬프의 값을 나타내는입니다. 형식이 제공 되지 않은 경우 hello ISO 8601 형식 ("o")이 사용 됩니다.| 
|dayOfWeek|반환 hello 문자열 타임 스탬프의 요일 구성 요소입니다.  일요일은 0, 월요일은 1 등입니다. 예 `3`:<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **매개 변수 번호**: 1<br /><br /> **이름**: Timestamp<br /><br /> **설명**: 필수. 이것이 hello 시간을 포함 하는 문자열입니다.| 
|dayOfMonth|반환 hello 요일을 문자열 타임 스탬프의 월 구성 요소입니다. 예 `15`:<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **매개 변수 번호**: 1<br /><br /> **이름**: Timestamp<br /><br /> **설명**: 필수. 이것이 hello 시간을 포함 하는 문자열입니다.| 
|dayOfYear|반환 hello 요일을 문자열 타임 스탬프의 연도 구성 요소입니다. 예 `74`:<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **매개 변수 번호**: 1<br /><br /> **이름**: Timestamp<br /><br /> **설명**: 필수. 이것이 hello 시간을 포함 하는 문자열입니다.| 
|ticks|반환 hello 틱 문자열 타임 스탬프의 속성입니다. 예 `1489603019`:<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **매개 변수 번호**: 1<br /><br /> **이름**: Timestamp<br /><br /> **설명**: 필수. 이것이 hello 시간을 포함 하는 문자열입니다.| 
  
### <a name="workflow-functions"></a>워크플로 함수  

이러한 함수에는 런타임 시 hello 워크플로 자체에 대 한 정보를 얻을 수 있습니다.  
  
|함수 이름|설명|  
|-------------------|-----------------|  
|listCallbackUrl|문자열 toocall tooinvoke hello 트리거 또는 작업을 반환합니다. <p> **참고**: 이 함수는 **httpWebhook** 및 **apiConnectionWebhook**에서만 사용할 수 있으며 **manual**, **recurrence**, **http** 또는 **apiConnection**에서는 사용할 수 없습니다. <p>예를 들어 hello `listCallbackUrl()` 함수에서 반환 합니다. <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|워크플로|이 함수 hello 워크플로 자체 hello 런타임에 대 한 모든 hello 세부 정보를 제공합니다. <p> Hello 워크플로 개체에서 사용할 수 있는 속성은 같습니다. <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> 값의 hello hello `run` 속성은 다음 속성을 가진 개체: <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>Hello 참조 [Rest API](http://go.microsoft.com/fwlink/p/?LinkID=525617) 해당 속성에 대 한 자세한 내용은 합니다.<p> 예를 들어 tooget hello의 이름을 현재 hello 실행을 사용 하 여 hello `"@workflow().run.name"` 식입니다. |

## <a name="next-steps"></a>다음 단계

[워크플로 작업 및 트리거](logic-apps-workflow-actions-triggers.md)
