---
title: "Azure Active Directory B2C: 언어 사용자 지정 사용 | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Azure Active Directory B2C: 언어 사용자 지정 사용

>[!NOTE] 
>이 기능은 공개 미리 보기 상태입니다.  이 기능을 사용할 때 테스트 테넌트를 사용하는 것이 좋습니다.  Hello 미리 보기 toohello 일반 공급 릴리스의 주요 변경 내용에 않으려고 예정 이지만 hello 오른쪽 toomake 이러한 변경 내용 tooimprove hello 기능.  기회 tootry 기능을 설치한 후에 경험에 대 한 피드백 및 어떻게 म 수 완성도 높이도록 입력 하세요.  오른쪽 위를 hello에 hello 웃는 얼굴 도구로 hello Azure 포털을 통해 피드백을 제공할 수 있습니다.   Hello 미리 보기 단계 중에이 기능을 사용 하 여 라이브 toogo 있습니다에 대 한 비즈니스 요구 사항인 경우 알려주시면 시나리오 및 hello 적절 한 지침과 지원을 제공할 수 있습니다.  [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)으로 문의할 수 있습니다.

언어의 사용자 지정 사용자 tooa 다양 한 언어 toosuit 고객이 필요한 여행 toochange가 있습니다.  36개 언어에 대한 번역이 제공됩니다([추가 정보](#additional-information) 참조).  단일 언어에 대 한 환경을 제공 하는 경우에 요구 사항 페이지 toosuit hello에서 모든 텍스트를 지정할 수 있습니다.  

## <a name="how-does-language-customization-work"></a>언어 사용자 지정이 작동하는 방식
사용자 지정 언어 tooselect을 언어로 된 사용자 여행은에서 사용할 수 있습니다.  Hello 기능이 활성화 되 면 hello 쿼리 문자열 매개 변수, ui_locales, 응용 프로그램에서 제공할 수 있습니다.  Azure AD B2C을 호출할 때 사용자가 지정한 페이지 toohello 로캘에서으로 변환 했습니다.  구성 유형을 사용 하 여 사용자 작업의 완전히 제어할 hello 언어를 제공 하 고 hello 고객의 브라우저의 언어 설정 hello를 무시 합니다. 또는 고객이 볼 수 있는 언어에 대한 제어 수준이 필요하지 않을 수 있습니다.  Ui_locales 매개 변수를 제공 하지 않으면 hello 고객의 경험은 브라우저의 설정에 의해 결정 됩니다.  여전히 제어 하는 사용자 작업은 언어 번역 tooby 지원 되는 언어로 추가 합니다.  고객의 브라우저 집합 tooshow 있으면 언어 원하지 toosupport, 다음 hello 언어를 지원 되는 culture의 기본값 대신 표시 된 대로 선택 합니다.

1. **언어를 지정 하는 ui 로캘에서** -사용자 작업은 여기에서 지정 된 하는 번역 된 toohello 언어 언어 사용자 지정을 사용 하도록 설정 하면
2. **브라우저 언어를 요청 했습니다.** -toohello 변환 없는 ui 로캘에 지정 된 경우 브라우저 언어에서 요청한 **지원 되는 언어에 포함 된 경우**
3. **기본 언어 정책** -toohello 정책 기본 언어 hello 브라우저 언어를 지정 하지 않거나 지원 되지 않는 하나 지정, 변환

>[!NOTE]
>사용자 지정 특성을 사용 하는 경우 사용자 고유의 번역 tooprovide 할 수 있습니다. 자세한 내용은 '[문자열 사용자 지정](#customize-your-strings)'을 참조하세요.
>

## <a name="support-uilocales-requested-languages"></a>ui_locales 요청 언어 지원 
정책에 ' 언어 사용자 지정'를 사용 하 여 hello ui_locales 매개 변수를 추가 하 여 이제 hello 사용자 여행의 hello 언어를 제어할 수 있습니다.
1. [Hello Azure 포털에 이러한 단계 toonavigate toohello B2C 기능 블레이드를 따릅니다.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. 번역에 대 한 tooenable 되도록 tooa 정책을 이동 합니다.
3. **언어 사용자 지정**을 클릭합니다.
4. 읽기 hello 신중 하 게 경고 합니다.  사용하도록 설정된 후에는 '언어 사용자 지정'을 해제할 수 없습니다.
5. Hello 기능을 설정 하 고 클릭 **확인**합니다.
6. Hello의 왼쪽된 위 모서리에서 사용자 정책을 저장 하면 **정책 편집** 블레이드입니다.

## <a name="select-which-languages-your-user-journey-supports"></a>사용자 경험에서 지원하는 언어 선택 
프로그램 사용자의 여행 toobe hello ui_locales 매개 변수는 제공 되지 않은 경우에 변환에 대 한 허용 된 언어의 목록을 만듭니다.
1. 이전 지침에서 정책에 '언어 사용자 지정'이 설정되었는지 확인합니다.
2. **정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.
3. Tooyour 취해집니다 **지원 되는 언어** 블레이드입니다.  여기에서 **언어 추가**를 선택할 수 있습니다.
4. 지원 되는 toobe 원하는 모든 hello 언어를 선택 합니다.  

>[!NOTE]
>Ui_locales 매개 변수가 제공 되지 않은 경우 다음 hello 페이지는 브라우저 언어 번역 된 toohello 고객의 경우에이 목록에 있음
>

5. 클릭 **확인** hello 맨 아래에
6. 닫기 hello **사용자 지정 언어** 블레이드 및 **저장** 정책입니다.

## <a name="customize-your-strings"></a>문자열 사용자 지정
'Language 사용자 지정을' 모든 사용자 여정에서 문자열 toocustomize 있습니다.
1. 정책에 '언어 사용자 지정' hello 이전 명령에서 사용 하도록 설정할 것을 확인 합니다.
2. **정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.
3. Hello 왼쪽 탐색 메뉴에서 선택 **콘텐츠 다운로드**합니다.
4. Tooedit hello 페이지를 선택 합니다.
5. Hello 드롭다운에서 tooedit에 대 한 hello 언어를 선택 합니다.
6. **다운로드**를 클릭합니다. 

이러한 단계는 사용자 문자열 편집 toostart를 사용할 수 있는 JSON 파일을 제공 합니다.

### <a name="changing-any-string-on-hello-page"></a>Hello 페이지에서 모든 문자열을 변경합니다.
1. JSON 파일 열기 hello JSON 편집기의 이전 지침에서 다운로드 됩니다.
2. 원하는 toochange 찾기 hello 요소입니다.  Hello를 찾을 수 있습니다 `StringId` 찾고 아니면 hello 찾을 hello 문자열의 `Value` toochange 원하는 합니다.
3. 업데이트 hello `Value` 특성으로 표시 하려는 내용입니다.
4. Hello 파일을 저장 하 고 변경 내용을 업로드 합니다.

### <a name="changing-extension-attributes"></a>확장 특성 변경
사용자 지정 특성에 대 한 toochange hello 문자열을 찾고 또는 tooadd 하나 toohello JSON 원하는 형식에 따라 hello 됨:
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>Toooverride 문자열, 필요한 경우 확인 되었는지 tooset hello `Override` 너무 값`true`합니다.  Hello 값 변경 되지 않고 hello 항목이 무시 됩니다. 
>

대체 `<ExtensionAttribute>` 사용자 지정 특성의 hello 이름의 합니다.  
대체 `<ExtensionAttributeValue>` hello 새 문자열 toobe 표시를 합니다.

### <a name="using-localizedcollections"></a>LocalizedCollections 사용
응답에 대 한 tooprovide 목록 값의 집합을 원하는 경우 toocreate는 `LocalizedCollections`합니다.  `LocalizedCollections`는 `Name` 및 `Value` 쌍의 배열입니다.  hello `Name` 표시 되 고 hello `Value` hello 클레임에 반환 되는 항목은 합니다.  tooadd는 `LocalizedCollections`, 형식에 따라 hello에:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>Toooverride 문자열, 필요한 경우 확인 되었는지 tooset hello `Override` 너무 값`true`합니다.  Hello 값 변경 되지 않고 hello 항목이 무시 됩니다. 
>

* `ElementId`hello 사용자 특성이 `LocalizedCollections` 에 대 한 응답
* `Name`이 값 표시 된 toohello 사용자 hello
* `Value`이 옵션을 선택 하는 hello 클레임에 반환 되는 항목은

### <a name="upload-your-changes"></a>변경 내용 업로드
1. Hello 변경 tooyour JSON 파일을 완료 한 후 뒤로 tooyour B2C 테 넌 트를 이동 합니다.
2. **정책 편집** 블레이드에서 **언어 사용자 지정**을 선택합니다.
3. Hello 왼쪽 탐색 메뉴에서 선택 **콘텐츠 업로드**합니다.
4. 에 대 한 변경 내용을 tooupload 원하는 hello 페이지를 선택 합니다.
5. Tooupload 언어에 대 한 JSON 이전에 제공한를 원하는 경우 toodelete hello 이전 항목을 해야 합니다.  Hello를 클릭 하 여 삭제할 수 있습니다 `...` 해당 언어의 오른쪽 hello 되 고 선택 **삭제**합니다.
6. 클릭 **추가** hello 상단 왼쪽에 있습니다.
7. JSON 파일의 hello 언어를 선택 합니다.
8. Hello 오른쪽에 hello 폴더 단추를 클릭 하 고 JSON 파일을 찾아봅니다.
9. Hello 클릭 **업로드** hello hello 블레이드 맨 단추입니다.
10. Tooyour 돌아가서 **정책 편집** 블레이드에 대 한 클릭 **저장**합니다.

## <a name="additional-information"></a>추가 정보
### <a name="recommendations-for-language-customization"></a>'언어 사용자 지정'에 대한 권장 사항
만에 넣는 문자열에 대 한 항목 tooyour 언어 리소스 하면 명시적으로 원하는 tooreplace 하는 것이 좋습니다.  에서는 모든 JSON 번역에서 컴파일되는 크기 제한 toohello 파일을 적용 합니다.  파일이 너무 큰 경우, 사용자 작업의 hello 성능 영향을 줍니다.
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>'언어 사용자 지정'을 사용하면 페이지 UI 사용자 지정 레이블이 제거됩니다.
'언어 사용자 지정'을 사용하도록 설정하면 사용자 지정 사용자 특성을 제외하고, 페이지 UI 사용자 지정을 사용한 레이블에 대한 이전 편집이 제거됩니다.  이 변경은 tooavoid 충돌을 방지 문자열을 편집할 수 있는 작업 수행 됩니다.  '언어 사용자 지정'의 언어 리소스를 업로드 하 여 레이블 및 기타 문자열 toochange를 계속할 수 있습니다.
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>Microsoft는 사용에 대 한 커밋된 tooprovide hello 최신 번역
지속적으로 번역을 개선하고 사용자에 맞게 유지할 예정입니다.  버그 및 글로벌 용어에서 변경 내용을 식별 하 고 사용자 여정에서 원활 하 게 작동 하는 hello 업데이트를 확인 합니다.
### <a name="support-for-right-to-left-languages"></a>오른쪽에서 왼쪽 언어 지원
오른쪽에서 왼쪽 언어에 대한 지원은 없습니다. 이 기능이 필요하면 [Azure 피드백](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag)에서 이 기능에 대해 투표하세요.
### <a name="social-identity-provider-translations"></a>소셜 ID 공급자 변환
Hello ui_locales OIDC 매개 변수 toosocial 로그인 제공 하지만 Facebook 및 Google 등 일부 소셜 id 공급자에는 적용 되지 않습니다. 
### <a name="browser-behavior"></a>브라우저 동작
Chrome 및 Firefox 둘 다의 언어 설정에 대 한 요청 및 지원 되는 언어 인 경우 hello 기본 하기 전에 표시 됩니다.  가장자리는 현재 언어를 요청 하지 않고와 직선 toohello 기본 언어를 이동 합니다.
### <a name="known-issues"></a>알려진 문제
* 프로필 편집 정책에서 MFA 페이지 hello에 대 한 언어 리소스를 업로드 하는 중 현재 제공 되지 않습니다.
* `LocalizedCollections`hello 응답 형식에 필요한 경우 값에 대해 생성 되지 않습니다.
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>지원되지 않는 언어가 필요하다면 어떻게 하나요?
예정 tooprovide tooupload '사용자 지정 언어'에 대 한 JSON 리소스 사용 하면이 기능을 확장 합니다.  hello 기능 있습니다 toospecify hello 이름 및 언어는 모든 언어에 대 한 코드 및 제공 *모든* 해당 언어에 대 한 번역을 hello 합니다.  이 기능이 필요한 경우 [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com)으로 시나리오를 보내 주세요.  

### <a name="what-languages-are-supported"></a>어떤 언어가 지원되나요?

| language              | 언어 코드 |
|-----------------------|---------------|
| 벵골어                | bn            |
| 체코어                 | cs            |
| 덴마크어                | da            |
| 독일어                | de            |
| 그리스어                 | el            |
| 영어               | en            |
| 스페인어               | es            |
| 핀란드어               | fi            |
| 프랑스어                | fr            |
| 구자라트어              | gu            |
| 힌디어                 | hi            |
| 크로아티아어              | hr            |
| 헝가리어             | hu            |
| 이탈리아어               | it            |
| 일본어              | ja            |
| 카나다어               | kn            |
| 한국어                | ko            |
| 말라얄람어             | ml            |
| 마라티어               | mr            |
| 말레이어                 | ms            |
| 노르웨이어 복말      | nb            |
| 네덜란드어                 | nl            |
| 펀잡어               | pa            |
| 폴란드어                | pl            |
| 포르투갈어 - 브라질   | pt-br         |
| 포르투갈어 - 포르투갈 | pt-pt         |
| 루마니아어              | ro            |
| 러시아어               | ru            |
| 슬로바키아어                | sk            |
| 스웨덴어               | sv            |
| 타밀어                 | ta            |
| 텔루구어                | te            |
| 태국어                  | th            |
| 터키어               | tr            |
| 중국어 - 간체  | zh-hans       |
| 중국어 - 번체 | zh-hant       |
