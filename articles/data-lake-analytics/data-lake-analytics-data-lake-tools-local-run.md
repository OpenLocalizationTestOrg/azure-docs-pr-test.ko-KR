---
title: "aaaTest 및 디버그 U-SQL 작업을 사용 하 여 로컬 실행 및 Azure 데이터 레이크 U-SQL SDK hello | Microsoft Docs"
description: "로컬 워크스테이션 toouse Azure 데이터 레이크 Tools for Visual Studio 및 Azure 데이터 레이크 U-SQL SDK tootest hello 및 디버그 U-SQL 작업 하는 방법에 대해 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>테스트 및 U-SQL 작업을 사용 하 여 로컬 실행 hello Azure 데이터 레이크 U-SQL SDK 디버그

Hello Azure 데이터 레이크 서비스의 경우와 마찬가지로 워크스테이션에서 Visual Studio 및 hello Azure 데이터 레이크 U-SQL SDK toorun U-SQL 작업에 대해 Azure 데이터 레이크 도구를 사용할 수 있습니다. 이들 두 가지 로컬 실행 기능으로 U-SQL 작업을 테스트하고 디버그하는 시간을 절약할 수 있습니다.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Hello 데이터 루트 폴더 및 파일 경로 hello 이해

로컬 실행와 hello U-SQL SDK 모두 데이터 루트 폴더를이 필요 합니다. hello 데이터 루트 폴더는 hello 로컬 계산 계정에 대 한 "로컬 저장소". 이 Data Lake 분석 계정 해당 toohello Azure 데이터 레이크 저장소 계정입니다. 다른 저장소 계정 tooa 전환와 동일 하 게 서로 다른 데이터 루트 폴더는 tooa 전환입니다. Tooaccess 서로 다른 데이터 루트 폴더와 일반적으로 데이터를 공유 하려면 스크립트에서 절대 경로 사용 해야 합니다. 또는 파일 시스템에 대 한 기호화 된 링크를 만듭니다 (예를 들어 **mklink** ntfs) hello 데이터 루트 폴더 toopoint toohello에서 데이터를 공유 합니다.

hello 데이터 루트 폴더에 사용 됩니다.

- 데이터베이스, 테이블, TVF(테이블 반환 함수), 어셈블리 등의 메타데이터를 저장합니다.
- 입력 hello 및 U-SQL에 상대 경로로 정의 된 출력 경로를 조회 합니다. 상대 경로 사용 하 여 사용 하면 보다 쉽게 toodeploy U-SQL 프로젝트 tooAzure 합니다.

U-SQL 스크립트의 상대 경로 및 로컬 절대 경로를 사용할 수 있습니다. hello 상대 경로 상대 toohello 지정한 데이터 루트 폴더 경로입니다. 하면 사용 하 여 "/"로 hello 경로 구분 기호 toomake 스크립트 hello 서버 쪽와 호환 되는 것이 좋습니다. 다음은 상대 경로 및 이와 대등한 절대 경로의 몇 가지 예입니다. 다음 예에서 C:\LocalRunDataRoot는 hello 데이터 루트 폴더입니다.

|상대 경로|절대 경로|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Visual Studio에서 로컬 실행 사용

Data Lake Tools for Visual Studio는 Visual Studio에서 U-SQL 로컬 실행 환경을 제공합니다. 이 기능을 사용하면 다음을 수행할 수 있습니다.

- C# 어셈블리와 함께 U-SQL 스크립트를 로컬로 실행합니다.
- C# 어셈블리를 로컬로 디버그합니다.
- [서버 탐색기]에서 U-SQL 카탈로그(로컬 데이터베이스, 어셈블리, 스키마 및 테이블)를 만들고, 보고, 삭제합니다. 서버 탐색기에서도 hello 로컬 카탈로그를 찾을 수도 있습니다.

    ![Data Lake Tools for Visual Studio의 로컬 카탈로그 로컬 실행](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

hello 기본 데이터 루트 폴더로 사용할 C:\LocalRunRoot 폴더 toobe hello 데이터 레이크 도구 설치 프로그램을 만듭니다. hello 기본 로컬 실행 병렬 처리는 1입니다.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure 로컬 Visual Studio에서 실행

1. Visual Studio를 엽니다.
2. **서버 탐색기**를 엽니다.
3. **Azure** > **Data Lake Analytics**를 차례로 확장합니다.
4. Hello 클릭 **데이터 레이크** 메뉴를 차례로 클릭 **옵션 및 설정**합니다.
5. Hello 왼쪽 트리에서 **Azure 데이터 레이크**을 펼친 다음 **일반**합니다.

    ![Data Lake Tools for Visual Studio의 로컬 실행 구성 설정](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

로컬 실행을 수행하려면 Visual Studio U-SQL 프로젝트가 필요합니다. 이 점이 Azure에서 실행하는 U-SQL 스크립트와 다릅니다.

### <a name="toorun-a-u-sql-script-locally"></a>로컬로 toorun는 U-SQL 스크립트
1. Visual Studio에서 U-SQL 프로젝트를 엽니다.   
2. [솔루션 탐색기]에서 U-SQL 스크립트를 마우스 오른쪽 단추로 클릭한 다음 **스크립트 제출**을 클릭합니다.
3. 선택 **(Local)** hello 분석 계정 toorun 로컬로 스크립트입니다.
Hello를 클릭할 수도 있습니다 **(Local)** hello 스크립트 창 위쪽의 계정 및 클릭 **전송** (또는 안녕하세요 Ctrl + F5 바로 가기 키 사용).

    ![Data Lake Tools for Visual Studio의 로컬 실행 작업 제출](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>로컬에서 스크립트 및 C# 어셈블리 디버그

제출 하 고 tooAzure 데이터 레이크 분석 서비스를 등록 하지 않고 C# 어셈블리를 디버깅할 수 있습니다. 참조 된 C# 프로젝트 및 두 hello 코드 숨김 파일에서에서 중단점을 설정할 수 있습니다.

#### <a name="toodebug-local-code-in-code-behind-file"></a>toodebug 로컬 코드 코드 숨김 파일에

1. Hello 코드 숨김 파일에에서 중단점을 설정 합니다.
2. F5 toodebug hello 스크립트 로컬 키를 누릅니다.

> [!NOTE]
   > 다음 절차에서 Visual Studio 2015 에서만 작동 하는 번호입니다. 이전 Visual Studio에서 할 수 있습니다 toomanually hello pdb 파일을 추가 합니다.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>참조 된 C# 프로젝트의 toodebug 로컬 코드

1. C# 어셈블리 프로젝트를 만들고 toogenerate hello 출력 dll을 빌드하십시오.
2. U SQL 문을 사용 하 여 hello dll을 등록 합니다.

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Hello C# 코드에에서 중단점을 설정 합니다.
4. 로컬로 hello C# dll 참조를 사용한 toodebug hello 스크립트 F5 키를 누릅니다.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>데이터 레이크 U-SQL SDK hello에서 사용 하 여 로컬 실행

Visual Studio를 사용 하 여 로컬로 toorunning U-SQL 스크립트 뿐만 아니라, 명령줄 및 프로그래밍 인터페이스 로컬로 hello Azure 데이터 레이크 U-SQL SDK toorun U-SQL 스크립트를 사용할 수 있습니다. 이를 통해 U-SQL 로컬 테스트를 확장할 수 있습니다.

[Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md)에 대해 자세히 알아보세요.


## <a name="next-steps"></a>다음 단계

* toosee 복잡 한 쿼리를 참조 [Azure 데이터 레이크 분석을 사용 하 여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)합니다.
* tooview 작업 세부 정보 참조 [사용 하 여 작업 브라우저와 Azure 데이터 레이크 분석 작업에 대 한 작업 보기](data-lake-analytics-data-lake-tools-view-jobs.md)합니다.
* toouse hello 꼭 짓 점 실행 보기 참조 [꼭 짓 점 실행 보기 데이터 레이크 Tools for Visual Studio에서에서 사용 하 여 hello](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)합니다.
