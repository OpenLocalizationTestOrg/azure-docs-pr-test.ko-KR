---
title: "aaaAuthenticating 및 Power BI embedded 권한 부여"
description: "Power BI Embedded에서 인증 및 권한 부여"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Power BI Embedded에서 인증 및 권한 부여

Power BI 포함 서비스 hello를 사용 하 여 **키** 및 **앱 토큰** 인증 및 권한 부여 명시적 최종 사용자 인증 대신 합니다. 이 모델에서 응용 프로그램이 최종 사용자에 대한 인증 및 권한 부여를 관리합니다. 필요한 경우 응용 프로그램 만들고 우리의 서비스 toorender에 알리는 hello 앱 토큰 hello 요청한 보고서를 보냅니다. 이 디자인 여전히 수는 있지만 사용자 인증 및 권한 부여에 대 한 Azure Active Directory에 앱 toouse가 필요 하지 않습니다.

## <a name="two-ways-tooauthenticate"></a>두 가지 방법으로 tooauthenticate

**키** - 모든 Power BI Embedded REST API 호출에 키를 사용할 수 있습니다. hello에 hello 키를 찾을 수 **Azure 포털** 를 클릭 하 여 **모든 설정을** 차례로 **액세스 키**합니다. 키는 항상 암호처럼 처리해야 합니다. 이러한 키에는 사용 권한을 toomake 특정 작업 영역 컬렉션에서 모든 REST API를 호출 합니다.

toouse REST 호출의 키를 권한 부여 헤더 뒤에 오는 hello를 추가 합니다.            

    Authorization: AppKey {your key}

**앱 토큰** - 앱 토큰은 모든 포함 요청에 사용됩니다. 제한 하므로 실행 하는 디자인 된 toobe 클라이언트 쪽 하기가 tooa 단일 보고서 및 해당 하는 모범 사례 tooset 만료 시간입니다.

앱 토큰은 사용자 키 중 하나로 서명된 JWT(JSON Web Token)입니다.

응용 프로그램 토큰 클레임에 따라 hello를 포함할 수 있습니다.

| 클레임 | 설명 |
| --- | --- |
| **ver** |hello 응용 프로그램 토큰의 hello 버전입니다. 0.2.0는 hello 현재 버전입니다. |
| **aud** |hello는 hello 토큰의 올바른 받는 것입니다. Power BI Embedded의 경우 "https://analysis.windows.net/powerbi/api"를 사용합니다. |
| **iss** |Hello 토큰을 발급 한 hello 응용 프로그램을 나타내는 문자열입니다. |
| **type** |생성 되 고 있는 응용 프로그램 토큰의 hello 형식입니다. Hello만 지원 됩니다. 현재 유형은 **포함**합니다. |
| **wcn** |에 대 한 작업 영역 컬렉션 이름 hello 토큰을 발급 되 고 됩니다. |
| **wid** |작업 영역 ID hello 토큰에 대해 실행 되 고 됩니다. |
| **rid** |에 대 한 ID hello 토큰 발급 되 고 보고 합니다. |
| **username** (선택 사항) |RLS로 사용 되는, RLS 규칙을 적용할 때 hello 사용자를 식별 하는 데 도움이 되는 문자열입니다. |
| **roles** (선택 사항) |행 수준 보안 규칙을 적용할 때 hello 역할 tooselect를 포함 하는 문자열입니다. 둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다. |
| **scp**(선택 사항) |Hello 권한 범위를 포함 하는 문자열입니다. 둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다. |
| **exp** (선택 사항) |hello 토큰이 만료 되므로 hello 시간을 나타냅니다. Unix 타임스탬프로 전달되어야 합니다. |
| **nbf** (선택 사항) |hello에 토큰 유효 시작 hello 시간을 나타냅니다. Unix 타임스탬프로 전달되어야 합니다. |

샘플 앱 토큰은 다음과 같이 표시됩니다.

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

디코딩되면 결과는 다음과 같습니다.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Hello apptokens 만드는 쉽게 해 주는 Sdk에서 사용할 수 있는 메서드가 있습니다. 예를 들어.net 살펴보면 hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) 클래스 및 hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) 메서드.

Hello.NET SDK를 참조할 수 있습니다 너무[범위](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes)합니다.

## <a name="scopes"></a>범위

Embed 토큰을 사용 하 여 hello 리소스에 대 한 액세스를 부여 toorestrict 사용을 할 수 있습니다. 이러한 이유로 범위가 지정된 사용 권한으로 토큰을 생성할 수 있습니다.

Power BI 포함에 대 한 hello 사용할 수 있는 범위는 hello 다음과가 같습니다.

|범위|설명|
|---|---|
|Dataset.Read|권한을 제공 tooread hello 데이터 집합을 지정 합니다.|
|Dataset.Write|지정 된 사용 권한 toowrite toohello 제공 데이터 집합입니다.|
|Dataset.ReadWrite|사용 권한 tooread 및 쓰기 toohello 컴파일되고 데이터 집합을 제공합니다.|
|Report.Read|권한을 제공 tooview hello 보고서를 지정 합니다.|
|Report.ReadWrite|사용 권한 tooview 및 편집 hello 지정 된 보고서를 제공 합니다.|
|Workspace.Report.Create|제공 사용 권한 toocreate 지정 hello 내에서 새 보고서 작업 영역입니다.|
|Workspace.Report.Copy|제공 사용 권한 tooclone 지정 hello 내의 기존 보고서 작업 영역입니다.|

Hello 다음과 같은 hello 범위 사이 공백을 사용 하 여 여러 범위를 제공할 수 있습니다.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**필요한 클레임 - 범위**

scp: {scopesClaim} scopesClaim 문자열 또는 허용 된 권한을 tooworkspace 리소스 (예: 보고서, 데이터 집합) hello 주목할 문자열의 배열 될 수 있습니다

범위를 정의 하는 디코딩된 토큰을 비슷한 toohello 다음과 유사할 것입니다.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>작업 및 범위

|작업|대상 리소스|토큰 사용 권한|
|---|---|---|
|데이터 집합을 기반으로 새 메모리 내 보고서를 만듭니다.|데이터 집합|Dataset.Read|
|(메모리) 데이터 집합을 기반으로 새 보고서 만들고 hello 보고서를 저장 합니다.|데이터 집합|* Dataset.Read<br>* Workspace.Report.Create|
|기존 메모리 내 보고서를 보고 탐색/편집합니다. Report.Read는 Dataset.Read를 의미합니다. 이것은 toosave 편집 권한이 없도록 합니다.|보고서|Report.Read|
|기존 보고서를 편집하고 저장합니다.|보고서|Report.ReadWrite|
|보고서(다른 이름으로 저장)의 복사본을 저장합니다.|보고서|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Hello 흐름이 작동 하는 방법을 다음과 같습니다.
1. Hello API 키 tooyour 응용 프로그램을 복사 합니다. hello 키를 확인할 수 있습니다 **Azure 포털**합니다.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. 토큰이 클레임을 어설션하며 만료 시간이 있습니다.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. 토큰이 API 액세스 키로 서명됩니다.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. 사용자가 보고서 tooview를 요청 합니다.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. API 액세스 키로 토큰의 유효성이 검사됩니다.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI 포함 보고서 toouser를 보냅니다.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

후 **Power BI 포함** 보고서 toohello 사용자 보냅니다 hello 사용자 사용자 지정 응용 프로그램에서 hello 보고서를 볼 수 있습니다. 예를 들어, hello를 가져온 경우 [샘플 판매 데이터 분석 PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello 샘플 웹 응용 프로그램은 다음과 같습니다.

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>참고 항목

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Microsoft Power BI Embedded 샘플 시작](power-bi-embedded-get-started-sample.md)  
[일반적인 Microsoft Power BI Embedded 시나리오](power-bi-embedded-scenarios.md)  
[Microsoft Power BI Embedded 시작](power-bi-embedded-get-started.md)  
[PowerBI-CSharp Git 리포지토리](https://github.com/Microsoft/PowerBI-CSharp)  
궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)

