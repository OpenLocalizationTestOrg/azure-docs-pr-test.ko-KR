---
title: "Azure 기능을 개발 하는 것에 대 한 aaaGuidance | Microsoft Docs"
description: "Hello Azure 함수 개념과 모든 프로그래밍 언어 및 바인딩을 통해 azure에서 toodevelop 함수 해야 하는 기술에 알아봅니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "개발자 가이드, Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Azure Functions 개발자 가이드
Azure 함수에서 특정 기능 몇 가지 핵심 기술 개념 및 hello 언어 또는 바인딩 사용에 관계 없이 구성 요소를 공유 합니다. 지정 된 언어 또는 바인딩 세부 정보 특정 tooa 학습에 대해 알아보기, 그중에서 tooall 적용 되는이 개요를 통해 있는지 tooread 수 있습니다.

이 문서에서는 hello 이미 읽어본 가정 [Azure 함수 개요](functions-overview.md) 익숙하지 [트리거, 바인딩 및 hello JobHost 런타임 같은 WebJobs SDK 개념](../app-service-web/websites-dotnet-webjobs-sdk.md)합니다. Azure 함수 hello WebJobs SDK를 기반으로 합니다. 

## <a name="function-code"></a>함수 코드
A *함수* 는 hello Azure 함수에서 기본 개념입니다. 사용자가 선택한 언어는 함수에 대 한 코드를 작성 하 고 hello 코드를 저장 및 구성 파일에서 같은 폴더 hello 합니다. hello 구성의 이름은 `function.json`, JSON 구성 데이터가 들어 있는입니다. 다양 한 언어를 지원 하 고 각 옵션에 약간 다른 환경에 최적화 된 toowork 해당 언어에 가장 적합 합니다. 

hello function.json 파일 hello 함수 바인딩 및 기타 구성 설정을 정의합니다. hello 런타임은이 파일 toodetermine hello 이벤트 toomonitor 및 toopass 데이터를 한 반환 데이터에서 실행이 작동 방식을 사용 합니다. hello 다음은 function.json 파일의 예입니다.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

집합 hello `disabled` 속성 너무`true` tooprevent hello 함수 실행 되지 않도록 합니다.

hello `bindings` 속성은 트리거와 바인딩을 구성할 수 있습니다. 각 바인딩에 몇 가지 일반 설정 및 특정 tooa 특정 유형의 바인딩 일부 설정을 공유 합니다. 모든 바인딩에 hello를 설정을 다음 사항이 필요 합니다.

| 속성 | 값/형식 | 설명 |
| --- | --- | --- |
| `type` |string |바인딩 형식 예: `queueTrigger` |
| `direction` |'in', 'out' |Hello 바인딩이 hello 함수에 데이터를 받기 또는 hello 함수에서 데이터를 보내는 지 여부를 나타냅니다. |
| `name` |string |hello 함수에 데이터 바인딩된 하는 hello에 사용 되는 hello 이름입니다. C#의 경우이 프로그램 인수 이름입니다. JavaScript 용 hello 키/값 목록에는 키의 것입니다. |

## <a name="function-app"></a>함수 앱
함수 앱은 Azure 앱 서비스에서 함께 관리되는 하나 이상의 개별 함수 함수로 구성됩니다. 모든 함수 앱 공유에서 hello 함수 hello 같은 가격 계획, 지속적인 배포 및 런타임 버전입니다. 함수 hello를 공유 하는 모든으로 여러 언어로 작성 된 응용 프로그램을 작동 동일 합니다. 방법은 tooorganize로 함수 응용 프로그램의 생각 하 고 전체적으로 프로그램 기능을 관리 합니다. 

## <a name="runtime-script-host-and-web-host"></a>런타임(스크립트 호스트 및 웹 호스트)
hello 런타임 또는 스크립트 호스트는 이벤트를 수신, 수집 및 데이터를 보냅니다 및 궁극적으로 코드를 실행 하는 hello 원본으로 사용 하는 WebJobs SDK 호스트입니다. 

HTTP toofacilitate 트리거 디자인 된 toosit hello 스크립트 호스트 프로덕션 시나리오에서 앞에 있는 웹 호스트 이기도 합니다. 호스트 두 개 있으면 hello 웹 호스트에서 관리 하는 hello 프런트 엔드 트래픽에서 tooisolate hello 스크립트 호스트는 데 도움이 됩니다.

## <a name="folder-structure"></a>폴더 구조
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

때 함수 tooa 함수 응용 Azure 앱 서비스의 배포에 대 한 프로젝트 설정에, 사이트 코드와이 폴더 구조를 처리할 수 있습니다. 배포 시 패키지 설치 또는 코드 transpilation 수행을 위하여 지속적인 통합 및 배포 같은 기존 툴 또는 사용자 지정 배포 스크립트를 사용할 수 있습니다.

> [!NOTE]
> 있는지 toodeploy 확인 프로그램 `host.json` 파일과 함수 폴더 직접 toohello `wwwroot` 폴더입니다. Hello를 넣지 마십시오 `wwwroot` 폴더에 배포 합니다. 그렇지 않으면 `wwwroot\wwwroot` 폴더가 만들어집니다. 
> 
> 

## <a id="fileupdate"></a>Tooupdate 앱 파일을 작동 하는 방법
hello Azure 포털에 내장 된 hello 함수 편집기를 사용 하면 hello 업데이트 *function.json* 파일 및 함수에 대 한 hello 코드 파일. tooupload 또는 다른 업데이트와 같은 파일 *package.json* 또는 *project.json* 또는 종속성을 다른 배포 방법 toouse 만들 수 있습니다.

기능 앱은 기반으로 앱 서비스 하므로 모든 hello [배포 옵션을 사용할 수 있는 toostandard 웹 앱](../app-service-web/web-sites-deploy.md) 기능 앱에서 사용할 수 있습니다. 다음은 일부 방법 tooupload 사용 하거나 함수 응용 프로그램 파일을 업데이트할 수 있습니다. 

#### <a name="toouse-app-service-editor"></a>toouse 응용 프로그램 서비스 편집기
1. Hello 함수 Azure 포털에서 클릭 **앱 설정 작동**합니다.
2. Hello에 **고급 설정** 섹션에서 클릭 **tooApp 서비스 설정 이동**합니다.
3. **개발 도구** 아래 앱 메뉴 탐색 창에서 **App Service 편집기**를 클릭합니다.
4. **이동**을 클릭합니다.
   
   서비스 응용 프로그램 편집기를 로드 한 후 표시 hello *host.json* 아래에 있는 파일 및 함수 폴더 *wwwroot*합니다. 
5. 열려 있는 파일 tooedit, 또는에서 끌어서 놓기 development 컴퓨터 tooupload 파일입니다.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>toouse hello 함수 응용 프로그램의 SCM (Kudu) 끝점
1. `https://<function_app_name>.scm.azurewebsites.net`로 이동합니다.
2. **디버그 콘솔 > CMD**를 클릭합니다.
3. 너무 이동`D:\home\site\wwwroot\` tooupdate *host.json* 또는 `D:\home\site\wwwroot\<function_name>` tooupdate 함수의 파일입니다.
4. Tooupload hello hello 파일 표에서 적절 한 폴더에 파일을 끌어서 드롭. 두 가지 영역을 hello 파일 표에서 파일을 삭제할 수 있습니다. 에 대 한 *.zip* 파일 hello 레이블을 사용 하는 상자가 나타납니다. "여기 tooupload 끌어서의 압축을 풉니다." 다른 파일 형식에 대 한 hello "의 압축을 푸는" 상자 외부에 있으면 서 hello 파일 눈금에서 삭제 합니다.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>toouse 연속 배포
Hello 항목의 지침을 hello [Azure 함수에 대 한 연속 배포](functions-continuous-deployment.md)합니다.

## <a name="parallel-execution"></a>병렬 실행
여러 개의 트리거 이벤트가 함수가 단일 스레드 런타임 처리할 수 있는 것 보다 빠르게 발생할 때 hello 런타임 동시에 여러 번 hello 함수를 호출할 수도 있습니다.  함수 앱 hello를 사용 하는 경우 [호스팅 계획 소비](functions-scale.md#how-the-consumption-plan-works), hello 함수 앱 자동으로 확장할 수 없습니다.  Hello 함수 응용 프로그램의 각 인스턴스에 hello 앱 실행 하는지 hello 호스팅 계획 또는 일반 소비 [앱 서비스 계획을 호스팅](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), 여러 스레드를 사용 하 여 병렬로 동시 함수 호출을 처리할 수 있습니다.  각 함수 응용 프로그램 인스턴스에서 동시 함수 호출의 최대 수 hello hello 함수 앱 내에서 다른 함수에서 사용 하는 hello 리소스와 마찬가지로 잘 사용 되 고 트리거 hello 유형을에 따라 다릅니다.

## <a name="functions-runtime-versioning"></a>Functions 런타임 버전 관리

Hello 런타임 버전을 hello 함수 hello를 사용 하 여 구성할 수 있습니다 `FUNCTIONS_EXTENSION_VERSION` 앱 설정 합니다. 예를 들어 hello 값 "~ 1" 함수에서 사용 하는 앱으로 사용 하 여 1의 주 버전을 나타냅니다. 출시 되는 함수 앱은 업그레이드 된 tooeach 새 부 버전. Hello에 hello 함수 응용 프로그램의 정확한 버전을 볼 수 있습니다 **설정을** hello Azure 포털에서에서 탭 합니다.

## <a name="repositories"></a>리포지토리
Azure 기능에 대 한 hello 코드는 오픈 소스 이며 GitHub 리포지토리에 저장:

* [Azure Functions 런타임](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Azure Functions 포털](https://github.com/projectkudu/AzureFunctionsPortal)
* [Azure Functions 템플릿](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/)
* [Azure WebJobs SDK 확장](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>바인딩
지원되는 모든 바인딩을 포함하는 테이블입니다.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>문제 보고
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 리소스는 hello 참조:

* [Azure Functions에 대한 모범 사례](functions-best-practices.md)
* [Azure Functions C# 개발자 참조](functions-reference-csharp.md)
* [Azure Functions F# 개발자 참조](functions-reference-fsharp.md)
* [Azure Functions NodeJS 개발자 참조](functions-reference-node.md)
* [Azure Functions 트리거 및 바인딩](functions-triggers-bindings.md)
* [Azure 함수: hello 여행](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) hello Azure 앱 서비스 팀 블로그에 합니다. Azure Functions 개발에 대한 기록

