---
title: "Visual Studio 프로젝트 템플릿-Azure 사용 하 여 일괄 처리 솔루션을 구축 aaaStart | Microsoft Docs"
description: "Visual Studio 프로젝트 템플릿을 통해 Azure Batch에서 계산 집약적인 워크로드를 어떻게 구현하고 실행할 수 있는지 알아봅니다."
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Visual Studio 프로젝트 템플릿 toojump 시작 일괄 처리 솔루션을 사용 하 여

hello **작업 관리자** 및 **작업 프로세서 Visual Studio 템플릿** 일괄 처리에 대 한 코드 toohelp 제공 하면 tooimplement 및 포함 된 일괄 처리에서 계산 집약적인 작업 hello 이상 실행 한 작업의 양을 합니다. 이 문서에서는 이러한 템플릿을 설명 하 고 방법에 대 한 지침을 제공 toouse 해당 합니다.

> [!IMPORTANT]
> 이 문서는 유일한 정보 적용 가능한 toothese 두 서식 파일에 설명 하 고 hello 일괄 처리 서비스 및 관련된 tooit 주요 개념에 익숙한 것으로 가정: 풀, 계산 노드, 작업 및 작업, 작업 관리자 태스크가, 환경 변수 및 기타 관련 정보입니다. 자세한 정보를 찾을 수 [Azure 배치 기본 사항](batch-technical-overview.md), [개발자를 위한 일괄 처리 기능 개요](batch-api-basics.md), 및 [.NET 용 hello Azure 배치 라이브러리 시작](batch-dotnet-get-started.md)합니다.
> 
> 

## <a name="high-level-overview"></a>대략적인 개요
hello 작업 관리자 태스크 프로세서 템플릿과 toocreate 사용 되는 두 개의 유용한 구성 될 수 있습니다.

* 작업을 독립적으로 병렬 실행 가능한 여러 태스크로 나눌 수 있는 작업 분할자를 구현하는 작업 관리자 태스크.
* 사용 되는 tooperform 전처리 및 후 처리 하는 응용 프로그램 명령줄 주위 수 있는 작업 프로세서입니다.

예를 들어 영화 렌더링 시나리오에서는 hello 작업 분할은 단일 동영상 작업으로 바꿀 수백 또는 수천 개의 개별 프레임을 별도로 처리는 별도 작업. 마찬가지로 hello 작업 프로세서는 호출 응용 프로그램 및 모든 종속 된 프로세스에 필요한 toorender 각 프레임을 렌더링 하는 hello 뿐만 아니라 추가 작업 (예를 들어 복사 렌더링 hello 프레임 tooa 저장소 위치)을 수행 합니다.

> [!NOTE]
> hello 작업 관리자와 작업 프로세서 템플릿은 서로 독립적으로 가로 및 세로 또는 hello 요구 사항 계산 작업의 및 기본 설정에 따라 둘 중 하나만 toouse를 선택할 수 있습니다.
> 
> 

Hello 다이어그램 아래에 나와 있는 것 처럼 이러한 템플릿을 사용 하는 계산 작업 3 가지 단계를 거치게 됩니다.

1. hello 클라이언트 코드 (예: 응용 프로그램, 웹 서비스 등)은 작업 관리자 태스크 hello 작업 관리자 프로그램으로 지정 하는 Azure에서 일괄 처리 서비스는 작업 toohello를 제출 합니다.
2. hello 일괄 처리 서비스가 계산 노드에서 hello 작업 관리자 태스크를 실행 하 고 hello 작업 분할자를 실행 하는 hello 작업 프로세서 작업의 수에 따라 지정 많은 계산 노드를 필요에 따라 hello 매개 변수 및 hello 작업 분할자 코드의 사양에 따라 키를 누릅니다.
3. hello 작업 프로세서 작업 독립적으로 실행, 병렬로 tooprocess hello 입력된 데이터 및 hello 출력 데이터를 생성 합니다.

![클라이언트 코드 hello 일괄 처리 서비스와 상호 작용 하는 방법을 보여 주는 다이어그램][diagram01]

## <a name="prerequisites"></a>필수 조건
toouse hello 일괄 처리 템플릿 hello 다음이 필요 합니다.

* Visual Studio 2015가 설치된 컴퓨터. 일괄 처리 템플릿은 현재 Visual Studio 2015에 대해서만 지원됩니다.
* hello에서 사용할 수 있는 hello 일괄 처리 템플릿 [Visual Studio 갤러리] [ vs_gallery] Visual Studio 확장으로 합니다. 두 가지가 tooget hello 템플릿:
  
  * Hello를 사용 하 여 hello 템플릿을 설치 **확장명 및 업데이트** Visual Studio에서 대화 상자 (자세한 내용은 참조 [찾기 및 사용 하 여 Visual Studio 확장명][vs_find_use_ext]). Hello에 **확장명 및 업데이트** 대화 상자에서 다음 두 가지 확장 검색 및 다운로드 hello:
    
    * Azure 배치 작업 관리자(작업 분할자 포함)
    * Azure 배치 태스크 프로세서
  * Hello 온라인 갤러리에서 Visual Studio에 대 한 hello 서식 파일을 다운로드: [Microsoft Azure 일괄 처리 프로젝트 템플릿][vs_gallery_templates]
* Toouse hello 하려는 경우 [응용 프로그램 패키지](batch-application-packages.md) 기능 toodeploy hello 작업 관리자 태스크 프로세서 toohello 일괄 처리는 계산 노드 toolink 저장소 계정 tooyour 일괄 처리 계정 사용 해야 합니다.

## <a name="preparation"></a>준비
작업 관리자와 작업 프로세서 프로그램 간에 더 쉽게 tooshare 코드를 만들 수 있습니다이 때문에 작업 관리자 뿐만 아니라 해당 작업 프로세서를 포함할 수 있는 솔루션을 만드는 것이 좋습니다. toocreate이이 솔루션에서는 다음이 단계를 수행 합니다.

1. Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.
2. **템플릿** 아래에서 **기타 프로젝트 형식**을 확장하고 **Visual Studio 솔루션**을 클릭한 후 **빈 솔루션**을 선택합니다.
3. 이 솔루션 (예: "LitwareBatchTaskPrograms")의 응용 프로그램 및 hello 용도 설명 하는 이름을 입력 합니다.
4. toocreate hello 새 솔루션을 클릭 하 여 **확인**합니다.

## <a name="job-manager-template"></a>작업 관리자 템플릿
hello 작업 관리자 템플릿을 tooimplement hello 다음 작업을 수행할 수 있는 작업 관리자 태스크를 사용 하면:

* 작업을 여러 태스크로 분할합니다.
* 이러한 작업 toorun 일괄 처리에 제출 합니다.

> [!NOTE]
> 작업 관리자 태스크에 대한 자세한 내용은 [개발자를 위한 배치 기능 개요](batch-api-basics.md#job-manager-task)를 참조하세요.
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Hello 템플릿을 사용 하 여 작업 관리자를 만듭니다
앞에서 만든 작업 관리자 toohello 솔루션 tooadd 다음이 단계를 따르십시오.

1. Visual Studio에서 기존 솔루션을 엽니다.
2. 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello 솔루션에서에서 클릭 **추가** > **새 프로젝트**합니다.
3. **Visual C#** 아래에서 **클라우드**를 클릭한 후 **Azure 배치 작업 관리자 및 작업 분할자**를 클릭합니다.
4. 응용 프로그램을 설명 하 고 (예: hello 작업 관리자와이 프로젝트를 식별 하는 이름을 입력 합니다. "LitwareJobManager").
5. toocreate hello 프로젝트 클릭 **확인**합니다.
6. 마지막으로 모든 빌드 hello 프로젝트 tooforce Visual Studio tooload NuGet 패키지를 참조 하 고 수정 하기 시작 하기 전에 프로젝트 hello tooverify 올바른지.

### <a name="job-manager-template-files-and-their-purpose"></a>작업 관리자 템플릿 파일 및 그 용도
Hello 작업 관리자 템플릿을 사용 하 여 프로젝트를 만들면 코드 파일의 세 그룹 발생 합니다.

* hello 주 프로그램 (Program.cs) 파일입니다. Hello 프로그램 진입점 및 최상위 예외 처리 포함합니다. 일반적으로 필요는 없습니다 toomodify이 있습니다.
* hello 프레임 워크 디렉터리입니다. 이 매개 변수를 추가 작업 toohello 일괄 작업 등의 압축을 푼 hello 작업 관리자 프로그램 –에서 수행 하는 hello '상용구' 작업을 담당 하는 hello 파일을 포함 합니다. 일반적으로 필요는 없습니다 toomodify 이러한 파일.
* hello 작업 분할자 파일 (JobSplitter.cs)입니다. 작업을 태스크로 분할하기 위해 응용 프로그램 관련 논리를 배치할 위치입니다.

물론 작업 분할자 코드 논리를 분할 하는 hello 작업의 hello 복잡성에 따라 필요한 toosupport로 추가 파일을 추가할 수 있습니다.

또한 hello 템플릿은.csproj 파일, app.config, packages.config 등과 같은 표준.NET 프로젝트 파일을 생성합니다.

이 섹션의 나머지 부분 hello hello 다른 파일 및 해당 코드 구조 및 각 클래스의 용도 설명 합니다.

![Hello 작업 관리자 템플릿 솔루션을 보여 주는 visual Studio 솔루션 탐색기][solution_explorer01]

**프레임워크 파일**

* `Configuration.cs`: Hello 로드 일괄 처리 계정 세부 정보, 연결 된 저장소 계정 자격 증명, 작업 및 작업 정보 및 작업 매개 변수 같은 작업 구성 데이터를 캡슐화합니다. 액세스 hello Configuration.EnvironmentVariable 클래스를 통해 tooBatch 정의 환경 변수 (hello 일괄 처리 설명서에서 작업에 대 한 환경 설정을 참조)도 제공 합니다.
* `IConfiguration.cs`: 요약이 hello hello 구성 클래스의 구현, 단위 테스트 가짜 또는 모의 구성 개체를 사용 하 여 작업 분할자 나타날 수 있습니다.
* `JobManager.cs`: 작업 관리자 프로그램 hello의 hello 구성 요소를 조정합니다. Hello 작업 분할자 호출 되는 hello 작업 분할을 초기화 하는 hello을 담당 하 고 hello 작업 분할자 toohello 작업 제출 자가 반환한 hello 작업 디스패치.
* `JobManagerException.cs`: 작업 관리자 tooterminate hello를 필요로 하는 오류를 나타냅니다. JobManagerException 종료의 일부로 관련 진단 정보가 수 제공 하는 경우 사용 되는 toowrap '예상 된' 오류입니다.
* `TaskSubmitter.cs`:이 클래스는 hello 작업 분할자 toohello 일괄 작업에서 반환 하는 책임 tooadding 작업입니다. hello JobManager 클래스 hello 일련의 작업을 시기 적절 하지만 효율적인 추가 toohello 작업에 대 한 일괄 처리로 집계 한 다음 각 일괄 처리에 대 한 백그라운드 스레드에서 TaskSubmitter.SubmitTasks를 호출 합니다.

**작업 분할자**

`JobSplitter.cs`:이 클래스는 작업으로 hello 작업 분할에 대 한 응용 프로그램별 논리를 포함 합니다. hello 프레임 워크 호출 시퀀스를 추가 하 여 작업을 hello JobSplitter.Split 메서드 tooobtain hello 메서드로 toohello 작업을 반환 합니다. 이 클래스는 hello 클래스 작업의 hello 논리를 삽입 합니다. Hello 분할 메서드 tooreturn toopartition hello 작업 하려는 hello 작업을 나타내는 CloudTask 인스턴스의 시퀀스를 구현 합니다.

**표준 .NET 명령줄 프로젝트 파일**

* `App.config`: 표준 .NET 응용 프로그램 구성 파일
* `Packages.config`: 표준 NuGet 패키지 종속성 파일
* `Program.cs`: Hello 프로그램 진입점 및 최상위 예외 처리 포함 되어 있습니다.

### <a name="implementing-hello-job-splitter"></a>Hello 작업 분할을 구현합니다.
Hello 작업 관리자 템플릿 프로젝트를 열면 hello 프로젝트 hello JobSplitter.cs 파일 기본적으로 적용 됩니다. Hello hello split () 메서드 아래에 표시를 사용 하 여 분할 작업에 대 한 hello 작업에 대 한 논리를 구현할 수 있습니다.

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> hello hello에 대 한 섹션을 주석 처리 `Split()` 메서드는 hello만 섹션 hello toomodify 하는 다른 작업으로 hello 논리 toosplit 작업을 추가 하 여 대상으로 하는 작업 관리자 템플릿 코드입니다. Toomodify hello 서식 파일의 다른 섹션을 원하는 경우의 일괄 처리의 작동 방식으로 개체는 확인 하세요 hello 중 몇 가지 사용을 및 [코드 샘플을 일괄 처리][github_samples]합니다.
> 
> 

Split() 구현에서는 다음에 액세스할 수 있습니다.

* hello 통해 작업 매개 변수를 hello `_parameters` 필드입니다.
* hello CloudJob 개체 hello 통해 나타내는 hello 작업 `_job` 필드입니다.
* hello CloudTask 개체 hello 통해 나타내는 hello 작업 관리자 태스크가 `_jobManagerTask` 필드입니다.

프로그램 `Split()` 구현 tooadd 작업 toohello 작업을 직접 필요 하지 않습니다. 대신 코드 CloudTask 개체의 시퀀스를 반환 해야 하 고 이러한 추가할 toohello 작업이 자동으로 hello 작업 분할자를 호출 하는 hello 프레임 워크 클래스. 일반적인 C#의 toouse 반복기는 (`yield return`)으로 계산 된 모든 작업 toobe 대기 하는 것이 아니라이 통해 실행 가능한 한 빨리 hello 작업 toostart tooimplement 작업 분할자 기능입니다.

**작업 분할자 실패**

작업 분할자에 오류가 발생하는 경우 다음 중 하나를 수행합니다.

* C# hello를 사용 하 여 hello 시퀀스 종료 `yield break` 는 case hello 작업 관리자 간주 되며 성공으로; 문 또는
* case hello 작업 관리자 실패 한 것으로 처리 되 고 hello 클라이언트 구성에 방식에 따라 다시 시도할 수 예외가 throw).

두 경우 모두 모든 작업은 이미 hello 작업 분할에서 반환 하 고 추가 된 toohello 일괄 작업에는 적격 toorun 됩니다. 이 toohappen 사용 하지 않으려는 경우 다음 수 있습니다.

* Hello 작업 분할에서 반환 하기 전에 hello 작업 종료
* 반환 하기 전에 전체 작업 컬렉션 hello 공식화 (즉, 반환 된 `ICollection<CloudTask>` 또는 `IList<CloudTask>` C# 반복기를 사용 하 여 작업 분할을 구현 하는 대신)
* 작업 종속성 toomake hello 작업 관리자의 hello 성공적으로 완료에 종속 된 모든 작업을 사용 하 여

**작업 관리자 재시도**

Hello 작업 관리자가 실패 하는 경우 hello 클라이언트 다시 시도 설정에 따라 hello 일괄 처리 서비스에서 다시 시도할 수 있습니다. 일반적으로이 보안상 hello 프레임 워크 추가 작업 toohello 작업을 하는 경우 이미 존재 하는 모든 작업에서 무시 합니다. 그러나 작업 계산 비용이 많이 드는 경우 하지 않을 toohello 작업, 이미 추가 된 작업을 다시 계산의 tooincur hello 비용 반대로, hello를 다시 실행 하는 경우는 보장된 되지 않음 toogenerate hello 동일한 작업 Id 다음 hello '중복을 무시 합니다.' 동작 작업을 시작 하지 않습니다. 이러한 경우 작업 분할 toodetect hello는 작업에 이미 수행 되었습니다 및 반복 되지 것, 예를 들어 한 CloudJob.ListTasks tooyield 작업을 시작 하기 전에 수행 하 여 디자인 해야 합니다.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>종료 코드와 hello 작업 관리자 서식 파일의 예외
종료 코드와 예외는 프로그램을 실행 하는의 메커니즘 toodetermine hello 결과 제공 하 고 tooidentify 문제 hello hello 프로그램 실행에 도움이 될 수 있습니다. 작업 관리자 템플릿 hello hello 종료 코드 및이 섹션에 설명 된 예외를 구현 합니다.

Hello 작업 관리자 템플릿을 사용 하 여 구현 되는 작업 관리자 태스크는 세 가지 가능한 종료 코드를 반환할 수 있습니다.

| 코드 | 설명 |
| --- | --- |
| 0 |hello 작업 관리자가 성공적으로 완료 합니다. 작업 분할 코드 toocompletion, 실행 되 고 모든 작업 toohello 작업이 추가 되었습니다. |
| 1 |'예상된' hello 프로그램 부분에 예외와 함께 hello 작업 관리자 태스크가 실패 했습니다. hello 예외는 번역 된 tooa JobManagerException와 진단 정보 및 해결에 대 한 제안을 오류 hello 가능한 경우. |
| 2 |작업 관리자 태스크가 hello '예기치 않은' 예외로 인해 실패 했습니다. hello 예외는 출력 기록된 toostandard 했지만 hello 작업 관리자 수 없습니다 tooadd 추가 진단 또는 업데이트 관리 정보입니다. |

Hello 작업 관리자 작업 실패의 경우에서 일부 작업 여전히 추가 된 toohello 서비스 전에 hello 오류가 발생 했습니다. 이러한 태스크는 정상적으로 실행됩니다. 이 코드 경로에 대한 설명은 위의 "작업 분할자 오류"를 참조하세요.

예외에서 반환 하는 모든 hello 정보 stderr.txt 및 stdout.txt 파일에 기록 됩니다. 자세한 내용은 [오류 처리](batch-api-basics.md#error-handling)를 참조하세요.

### <a name="client-considerations"></a>클라이언트 고려 사항
이 섹션에서는 이 템플릿을 기반으로 작업 관리자를 호출할 때 일부 클라이언트 구현 요구 사항에 대해 설명합니다. 참조 [toopass 매개 변수 및 환경 변수를 hello 클라이언트 코드에 어떻게](#pass-environment-settings) 전달 매개 변수 및 환경 설정에 대 한 내용은 합니다.

**필수 자격 증명**

순서 tooadd 작업 toohello Azure 일괄 처리 작업에서 작업 관리자 태스크가 hello Azure 배치 계정 URL과 키 필요합니다. YOUR_BATCH_URL 및 YOUR_BATCH_KEY라는 환경 변수에 이를 전달해야 합니다. Hello 작업 관리자에서에서 이러한 작업 환경 설정을 설정할 수 있습니다. 예를 들어 C# 클라이언트에서 다음과 같이 설정합니다.

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Storage 자격 증명**

일반적으로 hello 클라이언트 필요가 없는 tooprovide hello 연결 된 저장소 계정 자격 증명 toohello 작업 관리자 태스크는 (a) 대부분의 작업 관리자 tooexplicitly 액세스 hello 연결 된 저장소 계정이 필요 하지 않습니다 (b) hello 연결 된 저장소 계정을 제공 하기 때문에 hello 작업에 대 한 일반적인 환경 설정으로 tooall 작업입니다. 제공 하지 않으면 hello 연결 된 공통 환경 설정 hello 통해 저장소 계정 및 hello 작업 관리자 액세스 toolinked 저장소 필요 후 다음과 같이 hello 연결 된 저장소 자격 증명을 제공 해야 합니다.

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**작업 관리자 태스크 설정**

hello 클라이언트 hello 작업 관리자를 설정 해야 *killJobOnCompletion* 너무 플래그**false**합니다.

일반적으로 클라이언트 tooset hello에 대 한 *runExclusive* 너무**false**합니다.

hello 클라이언트는 hello를 사용 하 여 *resourceFiles* 또는 *applicationPackageReferences* toohello 계산 노드를 배포한 컬렉션 toohave hello 작업 관리자 실행 (및 필요한 Dll)입니다.

기본적으로 hello 작업 관리자 재시도 되지 않습니다 실패 합니다. 사용자 작업 관리자 논리에 따라 hello 클라이언트를 통해 tooenable 다시 시도 하는 경우가 *제약 조건을*/*maxTaskRetryCount*합니다.

**작업 설정**

Hello 작업 분할 작업 종속성을 가진 이면 hello 클라이언트 hello 작업 usesTaskDependencies tootrue를 설정 해야 합니다.

Hello 작업 분할 모델에서는 어떤 hello 작업 분할자 만듭니다 외 toowish tooadd 작업 toojobs 클라이언트에 대 한 거의 하지 않습니다. 따라서 hello 클라이언트 hello 작업이 정상적으로 설정 해야 *onAllTasksComplete* 너무**terminatejob**합니다.

## <a name="task-processor-template"></a>태스크 프로세서 템플릿
작업 프로세서 템플릿 tooimplement hello 다음 작업을 수행할 수 있는 작업 프로세서 수 있습니다.

* 각 일괄 처리 작업 toorun에서 필요한 hello 정보를 설정 합니다.
* 각 배치 태스크에 필요한 모든 작업을 실행합니다.
* Toopersistent 저장소 작업 출력을 저장 합니다.

작업 프로세서 일괄 처리에 필요한 toorun 작업 하지는 않지만 제공 하는 래퍼 tooimplement 한 위치에서 작업 실행 작업을 모두를 hello 작업 프로세서 사용의 이점이 있습니다. 예를 들어 각 작업의 hello 컨텍스트에 여러 응용 프로그램 toorun 필요한 경우 또는 필요한 경우 toocopy 데이터 toopersistent 저장소 완료 한 후 각각의 작업입니다.

hello 작업 프로세서에 의해 실행 hello 작업은 단순 또는 복합 및 많은 또는 워크 로드에 필요한 최소한 수 있습니다. 또한 작업 프로세서가 두 개에 모든 작업 동작을 구현 하 여 손쉽게 업데이트 하거나 추가할 수 있습니다 변경 tooapplications 또는 작업 부하 요구 사항에 따라 동작 합니다. 그러나 경우에 따라 임무 프로세서 아닐 수 있습니다 hello 최적의 솔루션 구현에 대 한 예를 들어 경우 간단한 명령줄에서 신속 하 게 시작할 수 있는 작업을 실행 하는 불필요 한 복잡성을 추가할 수 있습니다.

### <a name="create-a-task-processor-using-hello-template"></a>Hello 템플릿을 사용 하 여 작업 프로세서 만들기
앞에서 만든 작업 프로세서 toohello 솔루션 tooadd 다음이 단계를 따르십시오.

1. Visual Studio에서 기존 솔루션을 엽니다.
2. 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello 솔루션에서에서 클릭 **추가**, 클릭 하 고 **새 프로젝트**합니다.
3. **Visual C#** 아래에서 **클라우드**를 클릭한 후 **Azure 배치 태스크 프로세서**를 클릭합니다.
4. 응용 프로그램을 설명 하 고 작업 프로세서 (예: hello으로이 프로젝트를 식별 하는 이름을 입력 합니다. "LitwareTaskProcessor").
5. toocreate hello 프로젝트 클릭 **확인**합니다.
6. 마지막으로 모든 빌드 hello 프로젝트 tooforce Visual Studio tooload NuGet 패키지를 참조 하 고 수정 하기 시작 하기 전에 프로젝트 hello tooverify 올바른지.

### <a name="task-processor-template-files-and-their-purpose"></a>태스크 프로세서 템플릿 파일 및 그 용도
Hello 작업 프로세서 템플릿을 사용 하 여 프로젝트를 만들면 코드 파일의 세 그룹 발생 합니다.

* hello 주 프로그램 (Program.cs) 파일입니다. Hello 프로그램 진입점 및 최상위 예외 처리 포함합니다. 일반적으로 필요는 없습니다 toomodify이 있습니다.
* hello 프레임 워크 디렉터리입니다. 이 매개 변수를 추가 작업 toohello 일괄 작업 등의 압축을 푼 hello 작업 관리자 프로그램 –에서 수행 하는 hello '상용구' 작업을 담당 하는 hello 파일을 포함 합니다. 일반적으로 필요는 없습니다 toomodify 이러한 파일.
* hello 작업 프로세서 파일 (TaskProcessor.cs)입니다. (일반적으로 호출 하 여 기존 실행 파일 tooan out) 작업을 실행 하기 위한 응용 프로그램별 논리를 입력할입니다. 전처리 및 후처리 코드(예: 추가 데이터 다운로드 또는 결과 파일 업로드 등)도 여기에 포함됩니다.

물론 작업 프로세서 코드 논리를 분할 하는 hello 작업의 hello 복잡성에 따라 필요한 toosupport로 추가 파일을 추가할 수 있습니다.

또한 hello 템플릿은.csproj 파일, app.config, packages.config 등과 같은 표준.NET 프로젝트 파일을 생성합니다.

이 섹션의 나머지 부분 hello hello 다른 파일 및 해당 코드 구조 및 각 클래스의 용도 설명 합니다.

![Hello 프로세서 작업 서식 파일 솔루션을 보여 주는 visual Studio 솔루션 탐색기][solution_explorer02]

**프레임워크 파일**

* `Configuration.cs`: Hello 로드 일괄 처리 계정 세부 정보, 연결 된 저장소 계정 자격 증명, 작업 및 작업 정보 및 작업 매개 변수 같은 작업 구성 데이터를 캡슐화합니다. 액세스 hello Configuration.EnvironmentVariable 클래스를 통해 tooBatch 정의 환경 변수 (hello 일괄 처리 설명서에서 작업에 대 한 환경 설정을 참조)도 제공 합니다.
* `IConfiguration.cs`: 요약이 hello hello 구성 클래스의 구현, 단위 테스트 가짜 또는 모의 구성 개체를 사용 하 여 작업 분할자 나타날 수 있습니다.
* `TaskProcessorException.cs`: 작업 관리자 tooterminate hello를 필요로 하는 오류를 나타냅니다. TaskProcessorException 종료의 일부로 관련 진단 정보가 수 제공 하는 경우 사용 되는 toowrap '예상 된' 오류입니다.

**태스크 프로세서**

* `TaskProcessor.cs`: Hello 작업을 실행합니다. hello 프레임 워크 hello TaskProcessor.Run 메서드를 호출합니다. 이 클래스는 hello 클래스 해당 작업의 hello 응용 프로그램별 논리를 삽입 합니다. Hello 실행 메서드를 구현 합니다.
  * 태스크 매개 변수 구문 분석 및 유효성 검사
  * Hello 명령줄 작성 tooinvoke 하려는 모든 외부 프로그램에 대 한
  * 디버깅 용도로 필요할 수 있는 모든 진단 정보 기록
  * 해당 명령줄을 사용하는 프로세스 시작
  * Hello 프로세스 tooexit 때까지 대기
  * 성공 또는 실패 하는 경우 hello 프로세스 toodetermine hello 종료 코드를 캡처
  * 출력 파일에 저장 tookeep toopersistent 공간 절약

**표준 .NET 명령줄 프로젝트 파일**

* `App.config`: 표준 .NET 응용 프로그램 구성 파일
* `Packages.config`: 표준 NuGet 패키지 종속성 파일
* `Program.cs`: Hello 프로그램 진입점 및 최상위 예외 처리 포함 되어 있습니다.

## <a name="implementing-hello-task-processor"></a>Hello 작업 프로세서 구현
Hello 프로세서 작업 서식 파일 프로젝트를 열면 hello 프로젝트 hello TaskProcessor.cs 파일 기본적으로 적용 됩니다. 아래에 표시 된 hello run () 메서드를 사용 하 여 작업에서 hello 작업에 대 한 hello 실행 논리를 구현할 수 있습니다.

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> hello run () 메서드 hello에 주석이 추가 된 섹션은 hello만 섹션 toomodify 하는 작업에서 hello 작업에 대 한 hello 실행 논리를 추가 하 여 대상으로 하는 hello 프로세서 작업 템플릿 코드입니다. Toomodify hello 서식 파일의 다른 섹션을 사용 하도록 하려는 경우 먼저 파악해 두십시오 hello 일괄 처리 설명서를 검토 하 고 일부 hello 일괄 처리 코드 샘플을 시험 하 여 일괄 처리 작동 하는 방식을 합니다.
> 
> 

hello run () 메서드는 hello 명령줄을 시작, 하나 이상의 프로세스를 시작, 모든 프로세스 toocomplete 기다리는 hello 결과 저장 및 마지막 종료 코드를 반환 하는 일을 담당 합니다. run () 메서드 hello hello 처리 작업에 대 한 논리를 구현 하는 위치입니다. 드립니다; hello run () 메서드를 호출 하는 hello 작업 프로세서 프레임 워크 toocall 필요가 없습니다 것 직접 합니다.

Run() 구현에서는 다음에 액세스할 수 있습니다.

* hello 통해 작업 매개 변수를 hello `_parameters` 필드입니다.
* hello 통해 작업 및 작업 id hello `_jobId` 및 `_taskId` 필드입니다.
* hello 통해 hello 작업 구성 `_configuration` 필드입니다.

**태스크 실패**

오류가 발생 한 경우 예외를 throw 하 여 hello run () 메서드를 종료할 수 있습니다 되지만이 hello 최상위 수준의 예외 처리기 hello 작업 종료 코드를 제어 합니다. Hello 작업 및 기타 되어서는 안 진단 목적을 위해 다양 한 유형의 실패, 예를 들어 구분할 수 있도록 toocontrol hello 종료 코드를 필요 하거나 몇 가지 오류 모드를 종료 해야 하기 때문에 다음을 반환 하 여 hello run () 메서드를 종료 해야는 0이 아닌 종료 코드입니다. 이 hello 작업 종료 코드입니다.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>종료 코드와 hello 프로세서 작업 서식 파일의 예외
종료 코드와 예외는 프로그램을 실행 하는의 메커니즘 toodetermine hello 결과 제공 하 고 hello 프로그램 hello 실행 된 모든 문제를 식별에 도움이 될 수 있습니다. hello 프로세서 작업 템플릿 hello 종료 코드 및이 섹션에 설명 된 예외를 구현 합니다.

Hello 프로세서 작업 템플릿을 사용 하 여 구현 되는 프로세서 작업 세 가지 가능한 종료 코드를 반환할 수 있습니다.

| 코드 | 설명 |
| --- | --- |
| [Process.ExitCode][process_exitcode] |hello 작업 프로세서 toocompletion 실행 했습니다. 이 의미 하지는 성공적으로 호출 된 해당 hello 프로그램 참고-hello 작업 프로세서만 성공적으로 실행 하 고 예외 없이 후 처리를 수행 합니다. hello 종료 코드의 hello 의미 hello 호출 프로그램에 따라 다릅니다. – hello 프로그램 성공 했 고 다른 종료 코드 이면 hello 프로그램 실패 종료 코드 0 일반적으로 의미 합니다. |
| 1 |hello 작업 프로세서에서 '예상된' 부분이 hello 프로그램의 예외로 인해 실패 했습니다. hello 예외는 번역 된 tooa `TaskProcessorException` 와 진단 정보 및 해결에 대 한 제안을 오류 hello 가능한 경우. |
| 2 |hello 작업 프로세서 '예기치 않은' 예외로 인해 실패 했습니다. hello 예외는 출력 기록된 toostandard 했지만 hello 작업 프로세서 수 없습니다 tooadd 추가 진단 또는 업데이트 관리 정보입니다. |

> [!NOTE]
> 호출 하는 hello 프로그램이 종료 코드 1 및 2 tooindicate 특정 오류 모드를 사용 하는 경우 다음 종료 코드 1과 2를 사용 하 여 프로세서 작업 오류에 대 한가 모호 합니다. Hello Program.cs 파일의 hello 예외 사례를 편집 하 여 이러한 작업 오류 코드 프로세서 toodistinctive 종료 코드를 변경할 수 있습니다.
> 
> 

예외에서 반환 하는 모든 hello 정보 stderr.txt 및 stdout.txt 파일에 기록 됩니다. 자세한 내용은 hello 일괄 처리 설명서에서에서 오류 처리를 참조 합니다.

### <a name="client-considerations"></a>클라이언트 고려 사항
**Storage 자격 증명**

예를 들어 hello 파일 규칙 도우미 라이브러리를 사용 하 여 Azure blob 저장소 toopersist 출력을 사용 하 여 작업 프로세서 경우 너무 액세스 해야*어느* 클라우드 스토리지 계정 자격 증명 hello *또는* 공유 액세스 서명 (SAS)를 포함 하는 blob 컨테이너 URL입니다. hello 서식 파일에는 일반적인 환경 변수를 통해 자격 증명을 제공 하는 것에 대 한 지원이 포함 됩니다. 클라이언트는 다음과 같이 hello 저장소 자격 증명을 전달할 수 있습니다.

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

hello 저장소 계정은 hello hello 통해 TaskProcessor 클래스에서에서 사용할 수 있는 다음 `_configuration.StorageAccount` 속성입니다.

Toouse 된 SAS는 컨테이너 URL을 선호 하는 경우 작업 일반적인 환경 설정, 통해 이름을 전달할 수도 있습니다 하지만 hello 작업 프로세서 템플릿을 포함 하지는 않습니다이 기본적으로 지원 합니다.

**Storage 설정**

해당 hello 클라이언트 또는 작업 관리자 태스크가 hello 작업 toohello 작업을 추가 하기 전에 작업에 필요한 모든 컨테이너를 만드는 것이 좋습니다. 컨테이너 URL을 사용 하 여 SAS로으로 URL을 포함 하지 않을 경우 권한 toocreate hello 컨테이너 필수입니다. Toocall CloudBlobContainer.CreateIfNotExistsAsync hello 컨테이너에 있는 모든 작업을 저장 하는 대로 저장소 계정 자격 증명을 전달 하는 경우에 권장 됩니다.

## <a name="pass-parameters-and-environment-variables"></a>매개 변수 및 환경 변수 전달
### <a name="pass-environment-settings"></a>환경 설정 전달
클라이언트 환경 설정의 hello 형태로 정보 toohello 작업 관리자 태스크를 전달할 수 있습니다. Hello의 일부로 실행 될 hello 작업 프로세서 작업 생성 작업을 계산 하는 경우이 정보 hello 작업 관리자 태스크에서 사용할 수 있습니다. 환경 설정으로 전달할 수 있는 hello 정보의 예입니다.

* Storage 계정 이름 및 계정 키
* 배치 계정 URL
* 배치 계정 키

hello를 사용 하 여 hello 일괄 처리 서비스에 간단한 메커니즘 toopass 환경 설정을 tooa 작업 관리자 태스크가 `EnvironmentSettings` 속성 [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask]합니다.

예를 들어 tooget hello `BatchClient` 인스턴스 일괄 처리 계정에 대 한 hello 클라이언트에서 환경 변수는 hello URL을 코딩 하 고 공유 hello 일괄 처리 계정에 대 한 키 자격 증명을 전달할 수 있습니다. 마찬가지로, tooaccess hello 저장소 계정을 연결 된 toohello 일괄 처리 계정, 환경 변수로 hello 저장소 계정 이름 및 hello 저장소 계정 키를 전달할 수 있습니다.

### <a name="pass-parameters-toohello-job-manager-template"></a>Toohello 작업 관리자 템플릿 매개 변수 전달
대부분의 경우에서 유용 toopass 작업당 매개 변수 toohello 작업 관리자 작업 프로세스 toocontrol hello 작업 중 하나 또는 tooconfigure hello 작업에 대 한 hello 작업 합니다. 이렇게 하려면 hello 작업 관리자 태스크에 대 한 리소스 파일로 parameters.json 라는 JSON 파일을 업로드 합니다. hello 매개 변수 hello에서 제공 될 수 있습니다 `JobSplitter._parameters` hello 작업 관리자 서식 파일의 필드입니다.

> [!NOTE]
> hello 기본 제공 매개 변수 처리기 문자열-문자열 사전만 지원합니다. 매개 변수 값으로 toopass 복잡 한 JSON 값을 원하는 됩니다 필요 toopass 문자열로 이러한 및 hello 작업 분할에 구문 분석 하거나 경우 hello 프레임 워크의 수정 `Configuration.GetJobParameters` 메서드.
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Toohello 작업 프로세서 템플릿 매개 변수 전달
전달할 수도 있습니다 매개 변수 tooindividual 작업 hello 프로세서 작업 서식 파일을 사용 하 여 구현 합니다. 마찬가지로 hello 작업 관리자 템플릿을 사용 하 여 hello 작업 프로세서 템플릿은 찾습니다 라는 리소스 파일

parameters.json, 고이 있는 경우 hello 매개 변수 사전으로 로드 합니다. 두 가지 방법을 toopass 매개 변수 toohello 작업 프로세서 작업에 대 한 옵션이 있습니다.

* Hello JSON 작업 매개 변수를 다시 사용 합니다. Hello 유일한 매개 변수는 작업 수준 요소 (예: 렌더링 높이 너비) 경우에 적합 합니다. toodo이 hello 작업 분할에는 CloudTask을 만들 때 ResourceFiles hello 작업 관리자 태스크에서에서 참조 toohello parameters.json 리소스 파일 개체를 추가 (`JobSplitter._jobManagerTask.ResourceFiles`) toohello CloudTask ResourceFiles 컬렉션입니다.
* 생성 및 작업 분할 실행의 일부로 작업별 parameters.json 문서를 업로드 하 고 hello 작업의 리소스 파일 컬렉션에 해당 blob을 참조 합니다. 다양한 태스크에 서로 다른 매개 변수가 있는 경우 필요합니다. Hello 프레임 인덱스를 매개 변수로 toohello 태스크를 전달 되는 3D 렌더링 시나리오를 예로 들 수 있습니다.

> [!NOTE]
> hello 기본 제공 매개 변수 처리기 문자열-문자열 사전만 지원합니다. 매개 변수 값으로 toopass 복잡 한 JSON 값을 원하는 됩니다 필요 toopass 문자열로 이러한 및 hello 작업 프로세서에서 구문 분석 하거나 경우 hello 프레임 워크의 수정 `Configuration.GetTaskParameters` 메서드.
> 
> 

## <a name="next-steps"></a>다음 단계
### <a name="persist-job-and-task-output-tooazure-storage"></a>작업을 유지 하 고 출력 tooAzure 저장소 작업
Batch 솔루션 개발 시 다른 유용한 도구는 [Azure Batch 파일 규칙][nuget_package]입니다. 일괄 처리.NET 응용 프로그램 tooeasily 저장소에서 (현재 미리 보기)에이.NET 클래스 라이브러리를 사용 하 고 Azure 저장소에서 작업 출력 tooand를 검색 합니다. [Azure 일괄 처리 작업 및 태스크 출력 유지](batch-task-output.md) hello 라이브러리와 사용법에 대 한 자세한 내용은 포함 되어 있습니다.

### <a name="batch-forum"></a>배치 포럼
hello [Azure 배치 포럼] [ forum] 는 좋은 toodiscuss 일괄 처리를 놓고 hello 서비스에 대 한 질문은 msdn 합니다. 유용한 "고정" 게시물을 참조하고 Batch 솔루션을 빌드하는 동안 질문이 생기면 즉시 게시합니다.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
