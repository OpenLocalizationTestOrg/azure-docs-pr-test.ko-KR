---
title: "aaaDevelop 및 실행된 Azure 로컬로 함수 | Microsoft Docs"
description: "Toocode 및 테스트 Azure 작동 방식을 로컬 컴퓨터에 Azure 함수에서 실행 하기 전에 알아봅니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a>Azure Functions를 로컬로 코딩 및 테스트

Hello 동안 [Azure 포털] 전체 개발을 위한 도구 집합 및 많은 개발자에 게 테스트 Azure 기능은 선호 로컬 개발 환경을 제공 합니다. Azure 기능 쉽게 toouse를 사용 하면 즐겨 코드 편집기 및 로컬 개발 도구 toodevelop 및 로컬 컴퓨터에 함수를 테스트 합니다. 함수로 Azure에서 이벤트를 트리거할 수 있으며 로컬 컴퓨터에서 C# 및 JavaScript 함수를 디버깅할 수 있습니다. 

Visual Studio C# 개발자인 경우 Azure Functions은 [Visual Studio 2017과도 통합](functions-develop-vs.md)됩니다.

## <a name="install-hello-azure-functions-core-tools"></a>Hello Azure 함수 핵심 도구를 설치 합니다.

Azure 함수 핵심 도구는 로컬 Windows 컴퓨터에서 실행할 수 있는 hello Azure 함수 런타임의 로컬 버전입니다. 에뮬레이터 또는 시뮬레이터가 아닙니다. 같은 런타임 Azure 에서도 해당 powers hello에 것입니다.

hello [Azure 함수 핵심 도구] npm 패키지로 제공 됩니다. 먼저 npm이 포함된 [NodeJS를 설치](https://docs.npmjs.com/getting-started/installing-node)해야 합니다.  

>[!NOTE]
>Hello Azure 함수 핵심 도구 패키지 이때 Windows 컴퓨터에 설치할 수만 있습니다. 이 제한은 hello 함수 호스트에서 tooa 임시 제한 사항 때문입니다.

[Azure 함수 핵심 도구] hello 명령 별칭 뒤에 추가 합니다.
* **func**
* **azfun**
* **azurefunctions**

이러한 별칭의 모든 대신 사용할 수 있습니다 `func` 이 항목의 hello 예제에 표시 된 것입니다.

## <a name="create-a-local-functions-project"></a>로컬 Functions 프로젝트 만들기

로컬로 실행 하는 경우 함수 프로젝트 파일 host.json hello 및 local.settings.json 들어 있는 디렉터리입니다. 이 디렉터리는 Azure에서 함수 응용 프로그램의 해당 하는 hello는 합니다. toolearn hello Azure 함수 폴더 구조에 대 한 자세한 참조 hello [Azure 함수 개발자 가이드](functions-reference.md#folder-structure)합니다.

명령 프롬프트에서 다음 명령을 hello를 실행 합니다.

```
func init MyFunctionProj
```

hello 출력 hello 다음 예제와 같습니다.

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

Git 리포지토리, hello 옵션 사용을 만드는 tooopt `--no-source-control [-n]`합니다.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>로컬 설정 파일

hello 파일 local.settings.json 응용 프로그램 설정, 연결 문자열 및 Azure 함수 핵심 도구에 대 한 설정을 저장합니다. Hello 구조를 따르는 다음과 같습니다.

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| 설정      | 설명                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | 설정 된 경우 너무**true**, 모든 값은 로컬 컴퓨터 키를 사용 하 여 암호화 됩니다. `func settings` 명령과 함께 사용됩니다. 기본값은 **false**입니다. |
| **값** | 로컬에서 실행될 때 사용되는 응용 프로그램 설정의 컬렉션입니다. 응용 프로그램 설정 toothis 개체를 추가 합니다.  |
| **AzureWebJobsStorage** | 집합 hello 문자열 toohello hello Azure 함수 런타임에 의해 내부적으로 사용 되는 Azure 저장소 계정을 연결 합니다. hello 저장소 계정은 함수의 트리거를 지원합니다. 이 저장소 계정 연결 설정은 HTTP 트리거 함수를 제외한 모든 함수에 필요합니다.  |
| **AzureWebJobsDashboard** | Hello 연결 문자열 toohello Azure 저장소 계정으로 사용 되는 toostore hello 기능 로그를 설정 합니다. 이 옵션 값은 hello 로그 hello 포털에 액세스할 수 있도록 합니다.|
| **호스트** | 이 섹션의 설정을 로컬로 실행 하는 경우 hello 함수 호스트 프로세스를 사용자 지정 합니다. | 
| **LocalHttpPort** | 집합 hello hello 로컬 함수 호스트를 실행할 때 사용 되는 기본 포트 (`func host start` 및 `func run`). hello `--port` 명령줄 옵션이이 값 보다 우선 합니다. |
| **CORS** | 정의에 허용 되는 hello origin [크로스-원본 자원 공유 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)합니다. 원본은 공백 없이 쉼표로 구분된 목록으로 제공됩니다. 와일드 카드 값 hello (**\***)은 지원의 모든 원본 요청을 수 있습니다. |
| **ConnectionStrings** | 함수에 대 한 hello 데이터베이스 연결 문자열을 포함합니다. 이 개체의 연결 문자열의 hello 공급자 형식과 toohello 환경 추가 **System.Data.SqlClient**합니다.  | 

대부분의 트리거와 바인딩은는 **연결** 환경 변수 또는 응용 프로그램 설정의 toohello 이름을 매핑하는 속성입니다. 각 연결 속성에 대해 local.settings.json 파일에 정의된 앱 설정이 있어야 합니다. 

이러한 설정은 코드에서 환경 변수로 읽을 수도 있습니다. C#에서는 [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) 또는 [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx)를 사용합니다. JavaScript에서는 `process.env`를 사용합니다. 시스템 환경 변수로 지정 된 설정을 hello local.settings.json 파일의 값 보다 우선 합니다. 

Hello local.settings.json 파일의 설정은 로컬로 실행 하는 경우에 함수 도구에서 사용 됩니다. 기본적으로 이러한 설정은 마이그레이션되지 않습니다 자동으로 hello 프로젝트가 게시 된 tooAzure 있을 때. 사용 하 여 hello `--publish-local-settings` 전환 [게시 하는 경우](#publish) toomake 이러한 설정은 Azure에서 toohello 함수 앱 추가 되어 있는지 합니다.

올바른 저장소 연결 문자열에 대해 설정 된 경우 **AzureWebJobsStorage**, hello 다음과 같은 오류 메시지가 표시 됩니다.  

>local.settings.json에 AzureWebJobsStorage 값이 없습니다. 이 값은 HTTP 이외의 모든 트리거에 필요합니다. 'func azure functionary fetch-app-settings <functionAppName>'을 실행하거나 local.settings.json에 연결 문자열을 지정할 수 있습니다.
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>앱 설정 구성

연결 문자열에 대 한 값 tooset hello 다음 중 하나를 수행할 수 있습니다.
* 연결 문자열 hello 입력 [Azure 저장소 탐색기](http://storageexplorer.com/)합니다.
* Hello 다음 명령 중 하나를 사용 합니다.

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    두 명령 있습니다 toofirst 로그인 tooAzure 필요합니다.

## <a name="create-a-function"></a>함수 만들기

toocreate 함수 hello 다음 명령을 실행 하는 중:

```
func new
``` 
`func new`hello 다음 선택적 인수를 지원 합니다.

| 인수     | 설명                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | 프로그래밍 언어 C#, F #, JavaScript 등 hello 템플릿. |
| **`--template -t`** | hello 템플릿 이름입니다. |
| **`--name -n`** | hello 함수 이름입니다. |

예를 들어 toocreate JavaScript HTTP 트리거를 실행 합니다.

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

toocreate 큐 트리거 함수를 실행 합니다.

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>로컬로 함수 실행

toorun 함수 프로젝트 hello 함수 호스트를 실행 합니다. hello 호스트 hello 프로젝트의 모든 함수에 대 한 트리거를 사용 합니다.

```
func host start
```

`func host start`hello 다음 옵션을 지원 합니다.

| 옵션     | 설명                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | hello에 로컬 포트 toolisten 합니다. 기본값: 7071 |
| **`--debug <type>`** | hello 옵션은 `VSCode` 및 `VS`합니다. |
| **`--cors`** | CORS 원본의 공백 없이 쉼표로 구분된 목록입니다. |
| **`--nodeDebugPort -n`** | 노드 디버거 toouse hello에 대 한 hello 포트입니다. 기본값: launch.json 값 또는 5858 |
| **`--debugLevel -d`** | hello 콘솔 추적 수준 (해제, verbose, 정보, 경고 또는 오류). 기본값: 정보|
| **`--timeout -t`** | 시작에 대 한 hello 함수 호스트 t o, 초 단위로 hello 시간이 초과 됩니다. 기본값: 20초|
| **`--useHttps`** | Toohttps://localhost 바인딩: toohttp://localhost 대신 {port}: {port}. 기본적으로 이 옵션은 사용자 컴퓨터에 신뢰할 수 있는 인증서를 만듭니다.|
| **`--pause-on-error`** | Hello 프로세스를 종료 하기 전에 추가 입력에 대 한 일시 중지 합니다. IDE(통합 개발 환경)에서 Azure Functions 핵심 도구를 시작할 때 유용합니다.|

Hello 함수 호스트를 시작할 때 hello HTTP URL 트리거 함수 출력 합니다.

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>VS 코드 또는 Visual Studio에서 디버그

디버거, tooattach 전달 hello `--debug` 인수입니다. toodebug JavaScript 함수의 경우 Visual Studio 코드를 사용 합니다. C# 함수의 경우 Visual Studio를 사용합니다.

toodebug C# 함수를 사용 하 여 `--debug vs`합니다. [Azure Functions Visual Studio 2017 도구](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)를 사용할 수도 있습니다. 

toolaunch hello 호스트 및 JavaScript 디버깅 설정을 실행 합니다.

```
func host start --debug vscode
```

그런 다음 Visual Studio Code에서 hello **디버그** 뷰의 **tooAzure 함수 연결**합니다. 중단점을 연결하고, 변수를 검사하고, 코드를 단계별로 실행할 수 있습니다.

![Visual Studio Code를 사용한 JavaScript 디버깅](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>전달 테스트 데이터 tooa 함수

사용 하 여 직접 함수를 호출 또한 `func run <FunctionName>` hello 함수에 대 한 입력된 데이터를 제공 합니다. 이 명령은 비슷한 toorunning hello를 사용 하는 함수는 **테스트** hello Azure 포털에서에서 탭 합니다. 이 명령은 hello 전체 함수 호스트를 시작합니다.

`func run`hello 다음 옵션을 지원 합니다.

| 옵션     | 설명                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | 인라인 콘텐츠입니다. |
| **`--debug -d`** | Hello 함수를 실행 하기 전에 디버거 toohello 호스트 프로세스를 연결 합니다.|
| **`--timeout -t`** | Hello 로컬 함수 호스트 될 때까지 초 단위로 시간 toowait 것입니다.|
| **`--file -f`** | 파일 이름 toouse 콘텐츠로 hello 합니다.|
| **`--no-interactive`** | 입력에 대한 메시지를 표시하지 않습니다. 자동화 시나리오에 유용합니다.|

예를 들어 toocall HTTP 트리거 함수 및 hello 다음 명령을 실행 한 패스 콘텐츠 본문:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>TooAzure 게시

azure에서 사용 하 여 hello 함수 프로젝트 tooa 함수 앱 toopublish `publish` 명령:

```
func azure functionapp publish <FunctionAppName>
```

Hello 다음 옵션을 사용할 수 있습니다.

| 옵션     | 설명                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  게시 설정에 local.settings.json tooAzure, toooverwrite hello 설정에 이미 있는 경우 메시지를 표시 합니다.|
| **`--overwrite-settings -y`** | `-i`와 함께 사용해야 합니다. Azure의 AppSettings을 로컬 값으로 덮어씁니다(서로 다른 경우). 기본값은 프롬프트입니다.|

hello `publish` 명령 hello 함수 프로젝트 디렉터리의 hello 내용을 업로드 합니다. 로컬 파일을 삭제 하면 hello `publish` 명령 삭제 하지는 않습니다 Azure에서. Hello를 사용 하 여 Azure에서 파일을 삭제할 수 있습니다 [Kudu 도구](functions-how-to-use-azure-function-app-settings.md#kudu) hello에 [Azure 포털]합니다.

## <a name="next-steps"></a>다음 단계

Azure Functions 핵심 도구는 [오픈 소스이며 GitHub에서 호스팅](https://github.com/azure/azure-functions-cli)됩니다.  
버그 또는 기능 요청 toofile [GitHub 문제를 열고](https://github.com/azure/azure-functions-cli/issues)합니다. 

<!-- LINKS -->

[Azure 함수 핵심 도구]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure 포털]: https://portal.azure.com 
