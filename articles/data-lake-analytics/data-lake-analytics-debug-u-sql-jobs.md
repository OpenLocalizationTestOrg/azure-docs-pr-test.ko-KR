---
title: "aaaDebug U-SQL 작업 | Microsoft Docs"
description: "U SQL toodebug Visual Studio를 사용 하 여 꼭 짓 점 실패 하는 방법에 대해 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a>실패한 U-SQL 작업에 대한 사용자 정의 C# 코드 디버그

U-SQL C#을 사용 하 여 코드 tooadd 기능 추출기 사용자 지정 또는 리 듀 서 같은 작성할 수 있습니다 확장성 모델을 제공 합니다. toolearn 더 참조 [U SQL 프로그래밍 기능 가이드](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf)합니다. 실제로 어떤 코드라도 디버깅이 필요하며 빅 데이터 시스템에는 로그 파일과 같이 제한된 런타임 디버깅 정보만 제공될 수 있습니다.

라는 기능을 제공 하는 azure 데이터 레이크 Tools for Visual Studio **꼭 짓 점 디버그 실패**, hello 클라우드 tooyour 디버깅을 위해 로컬 컴퓨터에서 실패 한 작업을 복제할 수 있습니다. 로컬 복제본 hello hello 전체 클라우드 환경을에서는 모든 입력된 데이터와 사용자 코드를 포함 하 여 캡처합니다.

hello 다음 비디오에서는 Azure 데이터 레이크 도구에서 꼭 짓 점 디버깅 하지 못했습니다 Visual Studio에 대 한 합니다.

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> 아직 설치 되지 않은 경우 visual Studio 필요한 두 업데이트를 수행 하는 hello: [Microsoft Visual c + + 2015 재배포 가능 패키지 업데이트 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) 및 [유니버설 C 런타임에 대 한 Windows](https://www.microsoft.com/download/details.aspx?id=50410)합니다.

## <a name="download-failed-vertex-toolocal-machine"></a>꼭 짓 점 toolocal 컴퓨터 다운로드 실패

Visual Studio 용 Azure 데이터 레이크 도구에서 실패 한 작업을 열면 hello 오류 탭에서 자세한 오류 메시지가 포함 된 노란색 경고 표시줄을 표시 합니다.

1. 클릭 **다운로드** toodownload hello 모든 필요한 리소스 및 입력된 스트림을 합니다. 클릭 하 여 hello 다운로드 완료 하지 **을 다시 시도**합니다.

2. 클릭 **열려** hello 다운로드에는 로컬 디버깅 환경을 toogenerate 완료 된 후입니다. 디버깅 솔루션이 있는 새로운 Visual Studio 인스턴스가 자동으로 생성되고 열립니다.

![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 정점 다운로드](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

작업에는 코드 숨김 소스 파일이나 등록된 어셈블리가 포함될 수 있으며 이러한 두 가지 유형에는 서로 다른 디버깅 시나리오가 있습니다.

- [코드 숨김을 사용하여 실패한 작업 디버그](#debug-job-failed-with-code-behind)
- [어셈블리를 사용하여 실패한 작업 디버그](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a>코드 숨김으로 인해 실패한 작업 디버그

U-SQL 작업에 실패 하 고 사용자 코드를 포함 하는 hello 작업 하는 경우 (일반적으로 이름이 `Script.usql.cs` U-SQL 프로젝트에서), 해당 소스 코드는 솔루션을 디버깅 하는 hello로 가져온 합니다.  여기에서 hello Visual Studio 디버깅 도구 (조사식, 변수 등) tootroubleshoot hello 문제를 사용할 수 있습니다.

> [!NOTE]
> 를 디버깅 하려면 먼저 수 있는지 toocheck **공용 언어 런타임 예외** hello 예외 설정 창에서 (**Ctrl + Alt + E**).

![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 설정](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. 키를 눌러 **F5** toorun hello 코드 숨김 코드입니다. 예외로 인해 중지될 때까지 실행됩니다.

2. 열기 hello `ADLTool_Codebehind.usql.cs` 중단점을 설정 하 고 파일 키를 누릅니다 **F5** toodebug hello 코드 단계별 합니다.

    ![Azure Data Lake Analytics U-SQL 디버그 예외](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a>어셈블리로 인해 실패한 작업 디버그

U-SQL 스크립트에서 등록 된 어셈블리를 사용 하는 경우 hello 시스템 hello 소스 코드를 자동으로 가져올 수 없습니다. 이 경우 hello 어셈블리의 소스 코드 파일 toohello 솔루션을 수동으로 추가 합니다.

### <a name="configure-hello-solution"></a>Hello 솔루션 구성

1. 마우스 오른쪽 단추로 클릭 **솔루션 'VertexDebug' > 추가 > 기존 프로젝트...**  toofind 어셈블리의 소스 코드를 hello 및 솔루션을 디버깅 하는 hello 프로젝트 toohello를 추가 합니다.

    ![Azure Data Lake Analytics U-SQL 디버그 - 프로젝트 추가](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. 마우스 오른쪽 단추로 클릭 **LocalVertexHost > 속성** hello 솔루션 및 복사 hello에 **작업 디렉터리** 경로입니다.

3. 마우스 오른쪽 단추로 클릭 **어셈블리 소스 코드 프로젝트 > 속성**선택, hello **빌드** 왼쪽을 탭 하 고으로 복사 하는 hello 경로 붙여 넣습니다 **출력 > 출력 경로**합니다.

    ![Azure Data Lake Analytics U-SQL 디버그 - pdb 경로 설정](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. **Ctrl + Alt + E**를 누르고 예외 설정 창에서 **공용 언어 런타임 예외**를 확인합니다.

### <a name="start-debug"></a>디버그 시작

1. 마우스 오른쪽 단추로 클릭 **어셈블리 소스 코드 프로젝트 > 다시 작성** toooutput.pdb 파일 toohello `LocalVertexHost` 작업 디렉터리입니다.

2. 키를 눌러 **F5** hello 프로젝트 예외로 인해 중지 될 때까지 실행 됩니다. Hello 안전 하 게 무시할 수 있는 경고 메시지의 뒤에 표시 될 수 있습니다. Tooa 분 tooget toohello 디버그 화면을 걸릴 수 있습니다.

    ![Azure Data Lake Analytics U-SQL 디버그 Visual Studio 경고](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. 소스 코드를 열고 중단점을 설정 키를 누릅니다 **F5** toodebug hello 코드 단계별 지침.

Hello Visual Studio 디버깅 도구 (조사식, 변수 등) tootroubleshoot hello 문제를 사용할 수 있습니다.

> [!NOTE]
> Hello 코드 업데이트 toogenerate.pdb 파일을 수정한 후 때마다 hello 어셈블리 소스 코드 프로젝트를 다시 작성 합니다.

디버깅 후 hello 프로젝트 완료 되 면 hello 출력 창에는 hello 메시지의 뒤에 표시:

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL 디버그 성공](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a>Hello 작업을 다시 제출 하십시오.

디버깅을 완료 한 후에 hello 실패 한 작업을 다시 전송 하십시오.

1. 코드 숨김 솔루션으로 작업에 대 한 C# 코드 hello 코드 숨김 소스 파일에 복사 (일반적으로 `Script.usql.cs`).
2. 어셈블리를 사용한 작업에 대 한 ADLA 데이터베이스로 업데이트 hello.dll 어셈블리를 등록 합니다.
    1. 서버 탐색기 또는 클라우드 탐색기에서 확장 hello **ADLA 계정 > 데이터베이스** 노드.
    2. 마우스 오른쪽 단추로 클릭 **어셈블리** hello ADLA 데이터베이스와 새.dll 어셈블리를 등록 하 고: ![어셈블리를 등록 하는 Azure 데이터 레이크 분석 U-SQL 디버그](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)
3. 작업을 다시 제출합니다.

## <a name="next-steps"></a>다음 단계

- [U-SQL 프로그래밍 기능 가이드](data-lake-analytics-u-sql-programmability-guide.md)
- [Azure Data Lake Analytics 작업에 대한 U-SQL 사용자 정의 연산자를 개발합니다.](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [자습서: Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)
