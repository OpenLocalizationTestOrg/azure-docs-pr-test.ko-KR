---
title: "Azure Active Directory에서 특성 매핑에 대 한 식 aaaWriting | Microsoft Docs"
description: "Azure Active Directory에 있는 SaaS 응용 프로그램 개체의 자동화 된 프로 비전 하는 동안 toouse 식 매핑 tootransform 특성 허용 가능한 형식으로 값 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: b13c51cd-1bea-4e5e-9791-5d951a518943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: markvi
ms.openlocfilehash: caa0dd8144f6e5279a869e015ed75bd24169d585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="writing-expressions-for-attribute-mappings-in-azure-active-directory"></a>Azure Active Directory의 특성 매핑에 대한 식 작성
프로 비전 tooa SaaS 응용 프로그램을 구성한 경우 식으로 매핑하는 hello 유형의 지정할 수 있는 특성 매핑 중 하나입니다. 이러한 경우를 위해 hello SaaS 응용 프로그램에 대 한 더 허용 되는 형식으로 tootransform를 허용 하는 스크립트와 유사한 식에 사용자의 데이터 작성 해야 합니다.

## <a name="syntax-overview"></a>구문 개요
특성 매핑에 대 한 식에 대 한 hello 구문은 VBA 함수에 대 한 Visual Basic의 연상입니다.

* hello 전체 식은 다음 괄호 안에 인수 이름으로 구성 하는 함수 측면에서 정의 되어야 합니다. <br>
  *FunctionName (<<인수 1>>,<<argument N>>)*
* 서로 함수를 중첩할 수 있습니다. 예: <br> *FunctionOne(FunctionTwo(<<argument1>>))*
* 함수에 3가지 다른 유형의 인수를 전달할 수 있습니다.
  
  1. 특성은 대괄호로 묶어야 합니다. 예: [attributeName]
  2. 문자열 상수는 큰따옴표로 묶어야 합니다. 예: "미국"
  3. 기타 함수 예: FunctionOne(<<argument1>>, FunctionTwo(<<argument2>>))
* 문자열 상수에 대 한 백슬래시 (\) 또는 hello 문자열에 따옴표 (")가 필요한 경우 이스케이프 해야 hello 백슬래시 (\) 기호로 합니다. 예: "회사 이름: \"Contoso\""

## <a name="list-of-functions"></a>함수 목록
[추가](#append) &nbsp;&nbsp;&nbsp;&nbsp; [FormatDateTime](#formatdatetime) &nbsp;&nbsp;&nbsp;&nbsp; [Join](#join) &nbsp;&nbsp;&nbsp;&nbsp; [Mid](#mid) &nbsp;&nbsp;&nbsp;&nbsp; [Not](#not) &nbsp;&nbsp;&nbsp;&nbsp; [Replace](#replace) &nbsp;&nbsp;&nbsp;&nbsp; [StripSpaces](#stripspaces) &nbsp;&nbsp;&nbsp;&nbsp; [Switch](#switch)

- - -
### <a name="append"></a>추가
**함수:**<br> Append(source, suffix)

**설명:**<br> 소스 문자열 값을 사용 하 고 hello toohello 끝에 접미사를 추가 합니다.

**매개 변수:**<br> 

| 이름 | 필수/ 반복 | 형식 | 참고 사항 |
| --- | --- | --- | --- |
| **원본** |필수 |문자열 |일반적으로 hello 원본 개체에서 hello 특성의 이름 |
| **접미사** |필수 |문자열 |hello 문자열 hello 소스 값의 tooappend toohello 끝 한다는 것입니다. |

- - -
### <a name="formatdatetime"></a>FormatDateTime
**함수:**<br> FormatDateTime(source, inputFormat, outputFormat)

**설명:**<br> 한 형식의 날짜 문자열을 다른 형식으로 변환합니다.

**매개 변수:**<br> 

| 이름 | 필수/ 반복 | 형식 | 참고 사항 |
| --- | --- | --- | --- |
| **원본** |필수 |문자열 |일반적으로 이름 사용 하 여 hello 원본 개체에서 hello 특성입니다. |
| **inputFormat** |필수 |문자열 |Hello 소스 값의 예상된 형식입니다. 지원되는 형식은 [http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx](http://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx)를 참조하세요. |
| **outputFormat** |필수 |문자열 |Hello 출력 날짜의 서식을 지정 합니다. |

- - -
### <a name="join"></a>Join
**함수:**<br> Join(separator, source1, source2, …)

**설명:**<br> Join ()은 유사한 tooAppend() 점을 제외 하 고 결합할 수 있다는 점을 다중 **소스** 단일 문자열로 문자열 값 및 각 값으로 구분 됩니다는 **구분 기호** 문자열입니다.

이면 hello 소스 값 중 하나는 다중 값 특성 해당 특성의 각 값이 함께 조인, 분리 된 hello 구분 기호 값 됩니다.

**매개 변수:**<br> 

| 이름 | 필수/ 반복 | 형식 | 참고 사항 |
| --- | --- | --- | --- |
| **구분 기호** |필수 |문자열 |문자열을 하나의 문자열로 연결할 때 tooseparate 소스 값을 사용 합니다. 구분 기호가 필요하지 않은 경우 ""일 수 있습니다. |
| **source1  … sourceN ** |필수, 시간 변수 |문자열 |문자열 값 toobe 함께 결합 합니다. |

- - -
### <a name="mid"></a>Mid
**함수:**<br> Mid(source, start, length)

**설명:**<br> Hello 소스 값의 부분 문자열을 반환합니다. 부분 문자열은 hello 소스 문자열에서 문자를 hello 중 일부만 포함 하는 문자열입니다.

**매개 변수:**<br> 

| 이름 | 필수/ 반복 | 형식 | 참고 사항 |
| --- | --- | --- | --- |
| **원본** |필수 |문자열 |일반적으로 이름 사용 하 여 hello 특성입니다. |
| **시작** |필수 |정수 |Hello에서 인덱스 **소스** 하위 문자열이 시작 되어야 하는 문자열입니다. Hello 문자열의 첫 번째 문자를 갖게 됩니다 인덱스 1의 두 번째 문자 인덱스 2가 되며 등. |
| **length** |필수 |정수 |Hello 부분 문자열의 길이입니다. 길이 외부 hello 종료 되 면 **소스** 문자열 함수에서 부분 문자열을 반환 합니다 **시작** 인덱스의 끝까지 **소스** 문자열입니다. |

- - -
### <a name="not"></a>not
**함수:**<br> Not(source)

**설명:**<br> 대칭 hello의 부울 값을 hello **소스**합니다. **원본** 값이 "*True*"인 경우 "*False*"를 반환합니다. 그렇지 않은 경우 "*True*"를 반환합니다.

**매개 변수:**<br> 

| 이름 | 필수/ 반복 | 형식 | 참고 사항 |
| --- | --- | --- | --- |
| **원본** |필수 |부울 문자열 |예상 **원본** 값은 "True" 또는 "False"입니다. |

- - -
### <a name="replace"></a>Replace
**함수:**<br> ObsoleteReplace(source, oldValue, regexPattern, regexGroupName, replacementValue, replacementAttributeName, template)

**설명:**<br>
문자열 내 값을 대체합니다. 제공 하는 hello 매개 변수에 따라 다르게 작동 합니다.

* **oldValue** 및 **replacementValue**가 제공되는 경우:
  
  * OldValue hello 소스에 나타나는 모든 replacementValue 바꿉니다.
* **oldValue** 및 **template**이 제공되는 경우:
  
  * Hello을 모두 바꿉니다 **oldValue** hello에 **템플릿** hello로 **소스** 값
* **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementValue**가 제공되는 경우:
  
  * OldValueRegexPattern replacementValue 사용 hello 원본 문자열에 일치 하는 모든 값을 대체 합니다.
* **oldValueRegexPattern**, **oldValueRegexGroupName**, **replacementPropertyName**이 제공되는 경우:
  
  * **원본**에 값이 있는 경우 **원본**이 반환됩니다.
  * 경우 **소스** 값이 없는 사용 하 여 **oldValueRegexPattern** 및 **oldValueRegexGroupName** tooextract 대체 값으로 hello 속성에서  **replacementPropertyName**합니다. 대체 값 hello 결과로 반환 됩니다.

**매개 변수:**<br> 

| 이름 | 필수/ 반복 | 형식 | 참고 사항 |
| --- | --- | --- | --- |
| **원본** |필수 |문자열 |일반적으로 이름 사용 하 여 hello 원본 개체에서 hello 특성입니다. |
| **oldValue** |옵션 |문자열 |대체 toobe 값 **소스** 또는 **템플릿**합니다. |
| **regexPattern** |옵션 |문자열 |Regex 패턴에서 대체 hello 값 toobe입니다 **소스**합니다. 또는 replacementPropertyName이 사용 된 경우 tooextract 값 대체 속성의 패턴을 사용 합니다. |
| **regexGroupName** |옵션 |문자열 |내부 hello 그룹의 이름 **regexPattern**합니다. replacementPropertyName를 사용하는 경우에만 replacement 속성에서 replacementValue로 이 그룹의 값을 추출합니다. |
| **replacementValue** |옵션 |문자열 |새 값 tooreplace 이전과 사용 합니다. |
| **replacementAttributeName** |옵션 |문자열 |소스에 값이 없으면 대체 값에 사용 되는 hello 특성 toobe의 이름입니다. |
| **template** |옵션 |문자열 |때 **템플릿** 값이 제공을 볼 수에 대 한 **oldValue** 내부 템플릿을 hello와 소스 값으로 대체 합니다. |

- - -
### <a name="stripspaces"></a>StripSpaces
**함수:**<br> StripSpaces(source)

**설명:**<br> 모든 공백을 제거 ("") 문자 hello에서 원본 문자열입니다.

**매개 변수:**<br> 

| 이름 | 필수/ 반복 | 형식 | 참고 사항 |
| --- | --- | --- | --- |
| **원본** |필수 |문자열 |**소스** 값 tooupdate 합니다. |

- - -
### <a name="switch"></a>Switch
**함수:**<br> Switch(source, defaultValue, key1, value1, key2, value2, …)

**설명:**<br> **원본** 값이 **key**와 일치하면, 해당 **key**의 **value**를 반환합니다. **원본** 값과 일치하는 키가 없으면 **defaultValue**를 반환합니다.  **Key** 및 **value** 매개 변수는 항상 쌍으로 제공되어야 합니다. hello 함수는 항상 짝수 개수의 매개 변수가 필요합니다.

**매개 변수:**<br> 

| 이름 | 필수/ 반복 | 형식 | 참고 사항 |
| --- | --- | --- | --- |
| **원본** |필수 |문자열 |**소스** 값 tooupdate 합니다. |
| **defaultValue** |옵션 |문자열 |기본 값 toobe 소스 모든 키와도 일치 하지 않는 경우 사용 합니다. 빈 문자열("")일 수 있습니다. |
| **key** |필수 |문자열 |**키** toocompare **소스** 를 갖는 값입니다. |
| **값** |필수 |문자열 |Hello에 대 한 대체 값 **소스** 일치 하는 hello 키입니다. |

## <a name="examples"></a>예
### <a name="strip-known-domain-name"></a>알려진 도메인 이름 제거
사용자의 전자 메일 tooobtain 사용자 이름에서에서 알려진된 도메인 이름을 toostrip이 필요합니다. <br>
예를 들어 hello 도메인이 "contoso.com" 인 경우 hello 다음 식은 사용할 수 있습니다.

**식:** <br>
`Replace([mail], "@contoso.com", , ,"", ,)`

**샘플 입출력:** <br>

* **입력**(메일): “john.doe@contoso.com”
* **출력**: "john.doe"

### <a name="append-constant-suffix-toouser-name"></a>Toouser 이름을 상수 접미사 추가
Salesforce 샌드박스를 사용 하는 경우 해야 tooappend 추가 접미사 tooall 사용자 이름을 동기화 하기 전에 합니다.

**식:** <br>
`Append([userPrincipalName], ".test"))`

**샘플 입/출력:** <br>

* **입력**: (userPrincipalName): “John.Doe@contoso.com”
* **출력**:  “John.Doe@contoso.com.test”

### <a name="generate-user-alias-by-concatenating-parts-of-first-and-last-name"></a>이름과 성의 부분을 연결하여 사용자 별칭을 생성합니다.
사용자의 이름 중 처음 3 문자 및 사용자의 성 처음 5 개 문자를 수행 하 여 사용자 별칭 toogenerate를 해야 합니다.

**식:** <br>
`Append(Mid([givenName], 1, 3), Mid([surname], 1, 5))`

**샘플 입/출력:** <br>

* **입력** (givenName): "John"
* **입력** (surname): "Doe"
* **출력**: "JohDoe"

### <a name="output-date-as-a-string-in-a-certain-format"></a>특정 형식에서 문자열로 출력 날짜
원하는 toosend 날짜 tooa SaaS 응용 프로그램 특정 형식에서입니다. <br>
예를 들어 ServiceNow에 대 한 tooformat 날짜를 선택 합니다.

**식:** <br>

`FormatDateTime([extensionAttribute1], "yyyyMMddHHmmss.fZ", "yyyy-MM-dd")`

**샘플 입/출력:**

* **입력** (extensionAttribute1): "20150123105347.1Z"
* **출력**: “2015-01-23”

### <a name="replace-a-value-based-on-predefined-set-of-options"></a>미리 정의된 옵션 집합을 기반으로 값 바꾸기
Azure AD에 저장 된 hello 상태 코드를 기반으로 하는 hello 사용자의 toodefine hello 표준 시간대 필요 합니다. <br>
Hello 상태 코드는 미리 정의 된 hello 옵션 중 하나는 일치 하지 않으면, "Australia/Sydney"의 기본값을 사용 합니다.

**식:** <br>

`Switch([state], "Australia/Sydney", "NSW", "Australia/Sydney","QLD", "Australia/Brisbane", "SA", "Australia/Adelaide")`

**샘플 입/출력:**

* **입력** (상태): "QLD"
* **출력**: "오스트레일리아/브리즈번"

## <a name="related-articles"></a>관련 문서
* [Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스](active-directory-apps-index.md)
* [사용자 프로 비전/프로 비전 해제 tooSaaS 응용 프로그램 자동화](active-directory-saas-app-provisioning.md)
* [사용자 프로비저닝에 대한 특성 매핑 사용자 지정](active-directory-saas-customizing-attribute-mappings.md)
* [사용자 프로 비전에 대 한 필터 범위 지정](active-directory-saas-scoping-filters.md)
* [SCIM tooenable 자동으로 프로 tooapplications Azure Active Directory에서에서 사용자 및 그룹을 사용 하 여](active-directory-scim-provisioning.md)
* [계정 프로비전 알림](active-directory-saas-account-provisioning-notifications.md)
* [방법에 대 한 자습서 목록 tooIntegrate SaaS 앱](active-directory-saas-tutorial-list.md)

