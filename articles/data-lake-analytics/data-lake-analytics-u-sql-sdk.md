---
title: "U-SQL aaaScale 로컬 실행 및 Azure 데이터 레이크 U-SQL SDK와 함께 테스트 | Microsoft Docs"
description: "로컬 toouse Azure 데이터 레이크 U-SQL SDK tooscale U-SQL 작업 실행 하 고 명령줄에서 로컬 워크스테이션 프로그래밍 인터페이스와 테스트 하는 방법에 대해 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Azure Data Lake U-SQL SDK를 사용하여 U-SQL 로컬 실행 및 테스트 규모 조정

U-SQL 스크립트를 개발할 때 일반적인 toorun 이며 테스트 U-SQL 스크립트를 로컬로 전에 제출 toocloud입니다. Azure Data Lake는 이 시나리오에 대해 Azure Data Lake U-SQL SDK라는 Nuget 패키지를 제공합니다. 이를 통해 U-SQL 로컬 실행 및 테스트 규모를 쉽게 조정할 수 있습니다. 이 U-SQL CI (연속 통합) 시스템 tooautomate hello 컴파일 및 테스트와 테스트 가능한 toointegrate 이기도 합니다.

중요 하지 않은 경우에 대 한 방법을 toomanually 로컬 실행 하 고 디버깅 GUI 도구와 U-SQL 스크립트에 대 한 Visual Studio 용 Azure 데이터 레이크 도구를 사용할 수 있습니다. [여기](data-lake-analytics-data-lake-tools-local-run.md)에서 자세히 알아볼 수 있습니다.

## <a name="install-azure-data-lake-u-sql-sdk"></a>Azure Data Lake U-SQL SDK 설치

Azure 데이터 레이크 U-SQL SDK hello를 얻을 수 [여기](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) Nuget.org에 있습니다. 및를 사용 하기 전에 필요 toomake 종속성을 다음과 같이 해야 합니다.

### <a name="dependencies"></a>종속성

데이터 레이크 U-SQL SDK hello를 hello를 종속성 다음 사항이 필요 합니다.

- [Microsoft .NET Framework 4.6 이상](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 및 Windows SDK 10.0.10240.0 이상(이 문서에서는 CppSDK로 지칭함). 두 가지 방법으로 tooget CppSDK 가지가 있습니다.

    - [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou)을 설치합니다. 예를 들어 C:\Program Files (x86) \Windows Kits\10\ hello Program Files 폴더 아래에서 \Windows Kits\10 폴더를 해야 합니다. 또한 \Windows Kits\10\Lib에서 hello Windows 10 SDK 버전을 찾을 수 있습니다. 이러한 폴더 보이지 않으면 Visual Studio를 다시 설치 하 고 있는지 tooselect hello Windows 10 SDK hello 설치 중 수입니다. Visual Studio와 함께 설치 된이 있다면 hello U-SQL 로컬 컴파일러 것 자동으로.

    ![Data Lake Tools for Visual Studio의 Windows 10 SDK 로컬 실행](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - [Visual Studio용 Data Lake 도구](http://aka.ms/adltoolsvs)를 설치합니다. Hello (x86) C:\Program Files \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK에서 Visual c + + 및 Windows SDK 파일을 사전 포장 된 고품위 찾을 수 있습니다. 이 경우 hello U-SQL 로컬 컴파일러 hello 종속성을 자동으로 찾을 수 없습니다. 에 대 한 toospecify hello CppSDK 경로가 필요 합니다. Hello 파일 tooanother 위치를 복사 하거나 있는 그대로 사용할 수 있습니다.

## <a name="understand-basic-concepts"></a>기본 개념 이해

### <a name="data-root"></a>데이터 루트

hello 데이터 루트 폴더는 hello 로컬 계산 계정에 대 한 "로컬 저장소". 이 Data Lake 분석 계정 해당 toohello Azure 데이터 레이크 저장소 계정입니다. 다른 저장소 계정 tooa 전환와 동일 하 게 서로 다른 데이터 루트 폴더는 tooa 전환입니다. Tooaccess 서로 다른 데이터 루트 폴더와 일반적으로 데이터를 공유 하려면 스크립트에서 절대 경로 사용 해야 합니다. 또는 파일 시스템에 대 한 기호화 된 링크를 만듭니다 (예를 들어 **mklink** ntfs) hello 데이터 루트 폴더 toopoint toohello에서 데이터를 공유 합니다.

hello 데이터 루트 폴더에 사용 됩니다.

- 데이터베이스, 테이블, TVF(테이블 반환 함수), 어셈블리 등의 로컬 메타데이터를 저장합니다.
- 입력 hello 및 U-SQL에 상대 경로로 정의 된 출력 경로를 조회 합니다. 상대 경로 사용 하 여 사용 하면 보다 쉽게 toodeploy U-SQL 프로젝트 tooAzure 합니다.

### <a name="file-path-in-u-sql"></a>U-SQL의 파일 경로

U-SQL 스크립트의 상대 경로 및 로컬 절대 경로를 사용할 수 있습니다. hello 상대 경로 상대 toohello 지정한 데이터 루트 폴더 경로입니다. 하면 사용 하 여 "/"로 hello 경로 구분 기호 toomake 스크립트 hello 서버 쪽와 호환 되는 것이 좋습니다. 다음은 상대 경로 및 이와 대등한 절대 경로의 몇 가지 예입니다. 다음 예에서 C:\LocalRunDataRoot는 hello 데이터 루트 폴더입니다.

|상대 경로|절대 경로|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>작업 디렉터리

Hello U-SQL 스크립트를 로컬로 실행할 때 현재 실행 중인 디렉터리에서 컴파일하는 동안 작업 디렉터리가 만들어집니다. 또한 toohello 컴파일 출력 hello 필요한 로컬 실행에 대 한 런타임 파일 됩니다 섀도 복사한 toothis 작업 디렉터리입니다. 작업 디렉터리 루트 폴더 hello "ScopeWorkDir" 라고 하 고 hello 작업 디렉터리 아래에 있는 hello 파일은 다음과 같습니다.

|디렉터리/파일|디렉터리/파일|디렉터리/파일|정의|설명|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |런타임 버전의 해시 문자열|로컬 실행에 필요한 런타임 파일의 섀도 복사본|
| |Script_66AE4909AA0ED06C| |스크립트 이름 + 스크립트 경로의 해시 문자열|컴파일 출력 및 실행 단계 로깅|
| | |\_script\_.abr|컴파일러 출력|대수 파일|
| | |\_ScopeCodeGen\_.*|컴파일러 출력|생성된 관리 코드|
| | |\_ScopeCodeGenEngine\_.*|컴파일러 출력|생성된 네이티브 코드|
| | |참조된 어셈블리|어셈블리 참조|참조된 어셈블리 파일|
| | |deployed_resources|리소스 배포|리소스 배포 파일|
| | |xxxxxxxx.xxx[1..n]\_\*.*|실행 로그|실행 단계에 대한 로그|


## <a name="use-hello-sdk-from-hello-command-line"></a>Hello 명령줄에서 SDK hello를 사용 하 여

### <a name="command-line-interface-of-hello-helper-application"></a>Hello 도우미 응용 프로그램의 명령줄 인터페이스

SDK directory\build\runtime에서 LocalRunHelper.exe 인터페이스의 일반적으로 사용 하는 hello toomost 로컬 실행 기능을 제공 하는 hello 명령줄 도우미 응용 프로그램입니다. Note 명령을 모두 hello 및 hello 인수 스위치는 대/소문자 구분 합니다. tooinvoke 하기:

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

인수 없이 또는 hello로 LocalRunHelper.exe 실행 **도움말** 스위치 tooshow hello 도움말 정보:

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

Hello에 지원 정보:

-  **명령** 제공 hello 명령의 이름입니다.  
-  **Required Argument**: 제공해야 하는 인수를 나열합니다.  
-  **Optional Argument**: 선택적이며 기본값을 갖는 인수를 나열합니다.  선택적 부울 인수 매개 변수 및 모양을 음수 tootheir 기본값을 의미 합니다.

### <a name="return-value-and-logging"></a>반환 값 및 로깅

hello 도우미 응용 프로그램이 반환 **0** 성공 및 **-1** 실패에 대 한 합니다. 기본적으로 hello 도우미 모든 메시지 toohello 현재 콘솔을 보냅니다. 그러나 대부분의 hello 명령은 지원 hello **-MessageOut path_to_log_file** hello 리디렉션하는 선택적 인수 tooa 로그 파일을 출력 합니다.

### <a name="environment-variable-configuring"></a>환경 변수 구성

U-SQL 로컬 실행을 위해서는 지정된 데이터 루트가 로컬 저장소 계정으로 필요하고, 종속성에 대해 지정된 CppSDK 경로가 필요합니다. 명령줄 또는 설정 환경 변수에서 집합 hello 인수 둘 다를 수 있습니다.

- 집합 hello **SCOPE_CPP_SDK** 환경 변수입니다.

    Visual Studio에 대 한 데이터 레이크 도구를 설치 하 여 Microsoft Visual c + + 및 Windows SDK hello를 얻게 폴더 다음 hello 있는지를 확인 합니다.

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    라는 새 환경 변수를 정의 **SCOPE_CPP_SDK** toopoint toothis 디렉터리입니다. 또는 hello 폴더 toohello 다른 위치를 복사 하 고 지정 **SCOPE_CPP_SDK** 된 것입니다.

    또한 toosetting hello 환경 변수에서 hello를 지정할 수 있습니다 **-CppSDK** hello 명령줄을 사용 하는 경우에 인수입니다. 이 인수는 기본 CppSDK 환경 변수를 덮어씁니다.

- 집합 hello **LOCALRUN_DATAROOT** 환경 변수입니다.

    라는 새 환경 변수를 정의 **LOCALRUN_DATAROOT** toohello 데이터 루트를 가리키는 합니다.

    또한 toosetting hello 환경 변수에서 hello를 지정할 수 있습니다 **-DataRoot** 인수 명령줄을 사용 하는 경우 hello 데이터 루트 경로 사용 합니다. 이 인수는 기본 데이터 루트 환경 변수를 덮어씁니다. 이 인수 tooevery 명령줄 hello 모든 작업에 대 한 기본 데이터 루트 환경 변수를 덮어쓸 수 있도록 실행 하는 tooadd 필요 합니다.

### <a name="sdk-command-line-usage-samples"></a>SDK 명령줄 사용 샘플

#### <a name="compile-and-run"></a>컴파일 및 실행

hello **실행** 명령을 사용 하 여 toocompile 스크립트 hello 및 다음 컴파일된 결과 실행 합니다. 명령줄 인수는 **compile**과 **execute**의 조합입니다.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

hello 다음은 하기 위한 선택적 인수 **실행**:


|인수|기본값|설명|
|--------|-------------|-----------|
|-CodeBehind|False|hello 스크립트의.cs 코드 숨김|
|-CppSDK| |CppSDK 디렉터리입니다.|
|-DataRoot| DataRoot 환경 변수|로컬 실행에 대 한 DataRoot 너무 기본 'LOCALRUN_DATAROOT' 환경 변수|
|-MessageOut| |콘솔 tooa 파일에 메시지를 덤프 합니다.|
|-Parallel|1|Hello 실행 계획 hello로 병렬 처리 수준 지정|
|-References| |구분 하 여 tooextra 참조 어셈블리 경로 또는 코드 숨김의 데이터 파일의 목록 ';'|
|-UdoRedirect|False|Udo 어셈블리 리디렉션 구성을 생성합니다.|
|-UseDatabase|master|임시 어셈블리 등록 뒤에 있는 코드에 대 한 데이터베이스 toouse|
|-Verbose|False|런타임의 자세한 출력을 표시합니다.|
|-WorkDir|현재 디렉터리|컴파일러 사용 및 출력을 위한 디렉터리입니다.|
|-RunScopeCEP|0|ScopeCEP 모드 toouse|
|-ScopeCEPTempPath|temp|스트리밍 데이터에 대 한 임시 경로 toouse|
|-OptFlags| |쉼표로 구분된 최적화 프로그램 플래그 목록입니다.|


예를 들면 다음과 같습니다.

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

결합 외에도 **컴파일** 및 **실행**, 컴파일 및 hello 컴파일된 실행 파일을 개별적으로 실행할 수 있습니다.

#### <a name="compile-a-u-sql-script"></a>U-SQL 스크립트 컴파일

hello **컴파일** 명령에 사용 되는 toocompile는 U-SQL 스크립트 tooexecutables입니다.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

hello 다음은 하기 위한 선택적 인수 **컴파일**:


|인수|설명|
|--------|-----------|
| -CodeBehind [기본값 'False']|hello 스크립트의.cs 코드 숨김|
| -CppSDK [기본값 '']|CppSDK 디렉터리입니다.|
| -DataRoot [기본값 'DataRoot 환경 변수']|로컬 실행에 대 한 DataRoot 너무 기본 'LOCALRUN_DATAROOT' 환경 변수|
| -MessageOut [기본값 '']|콘솔 tooa 파일에 메시지를 덤프 합니다.|
| -References [기본값 '']|구분 하 여 tooextra 참조 어셈블리 경로 또는 코드 숨김의 데이터 파일의 목록 ';'|
| -Shallow [기본값 'False']|단순 컴파일입니다.|
| -UdoRedirect [기본값 'False']|Udo 어셈블리 리디렉션 구성을 생성합니다.|
| -UseDatabase [기본값 'master']|임시 어셈블리 등록 뒤에 있는 코드에 대 한 데이터베이스 toouse|
| -WorkDir [기본값 '현재 디렉터리']|컴파일러 사용 및 출력을 위한 디렉터리입니다.|
| -RunScopeCEP [기본값 '0']|ScopeCEP 모드 toouse|
| -ScopeCEPTempPath [기본값 'temp']|스트리밍 데이터에 대 한 임시 경로 toouse|
| -OptFlags [기본값 '']|쉼표로 구분된 최적화 프로그램 플래그 목록입니다.|


몇 가지 사용 예제는 다음과 같습니다.

U-SQL 스크립트를 컴파일합니다.

    LocalRunHelper compile -Script d:\test\test1.usql

U-SQL 스크립트를 컴파일하고 hello 데이터 루트 폴더를 설정 합니다. Note 이렇게 환경 변수를 설정 하는 hello 덮어쓰게 됩니다.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

U-SQL 스크립트를 컴파일하고 작업 디렉터리, 참조 어셈블리 및 데이터베이스를 설정합니다.

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>컴파일된 결과 실행

hello **실행** 명령에 사용 되는 tooexecute 컴파일 결과입니다.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

hello 다음은 하기 위한 선택적 인수 **실행**:

|인수|설명|
|--------|-----------|
|-DataRoot [기본값 '']|메타데이터 실행을 위한 루트 데이터입니다. 기본적으로 toohello **LOCALRUN_DATAROOT** 환경 변수입니다.|
|-MessageOut [기본값 '']|Hello 콘솔 tooa 파일에 메시지를 덤프 합니다.|
|-Parallel [기본값 '1']|병렬 처리 수준을 지정 하는 hello 사용 하 여 표시기 toorun 생성 hello 로컬 실행 단계.|
|-Verbose [기본값 'False']|표시기 tooshow 자세한 런타임에서 출력 합니다.|

사용 예는 다음과 같습니다.

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>프로그래밍 인터페이스를 사용 하 여 hello SDK

hello 프로그래밍 인터페이스는 모두 LocalRunHelper.exe hello에 있습니다. Hello U-SQL SDK의 toointegrate hello 기능을 사용 하 고 hello C# 테스트 프레임 워크 tooscale U-SQL 스크립트 로컬 테스트 수 있습니다. 이 문서에서는 hello 표준 C# 단위 테스트 프로젝트 tooshow를 어떻게 사용 합니다 toouse 이러한 U-SQL 스크립트 tootest 인터페이스입니다.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>1단계: C# 단위 테스트 프로젝트 및 구성 만들기

- 파일 > 새로 만들기 > 프로젝트 > Visual C# > 테스트 > 단위 테스트 프로젝트를 통해 C# 단위 테스트 프로젝트를 만듭니다.
- LocalRunHelper.exe hello 프로젝트에 대 한 참조로 추가 합니다. hello LocalRunHelper.exe는 Nuget 패키지에 \build\runtime\LocalRunHelper.exe에 있습니다.

    ![Azure Data Lake U-SQL SDK 참조 추가](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- U-SQL SDK **만** x64로 확인 되었는지 tooset 빌드 플랫폼 대상 x64 지원 환경입니다. 프로젝트 속성 > 빌드 > 플랫폼 대상을 통해 설정할 수 있습니다.

    ![Azure Data Lake U-SQL SDK x64 프로젝트 구성](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- X64로 있는지 tooset 테스트 환경을 확인 합니다. Visual Studio에서 테스트 > 테스트 설정 > 기본 프로세서 아키텍처 > x64를 통해 설정할 수 있습니다.

    ![Azure Data Lake U-SQL SDK x64 테스트 환경 구성](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- 일반적으로 ProjectFolder\bin\x64\Debug 아래 있는 NugetPackage\build\runtime\ tooproject 작업 디렉터리에 모든 종속 파일 toocopy 있는지를 확인 합니다.

### <a name="step-2-create-u-sql-script-test-case"></a>2단계: U-SQL 스크립트 테스트 사례 만들기

U-SQL 스크립트 테스트에 대 한 hello 샘플 코드는 다음과 같습니다. Tooprepare 스크립트 테스트를 위해 필요한 입력된 파일 및 예상된 출력 파일입니다.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>LocalRunHelper.exe의 프로그래밍 인터페이스

등 hello 인터페이스는 다음과 같이 나열 된, LocalRunHelper.exe hello 프로그래밍 U-SQL 로컬 컴파일, 실행에 대 한 인터페이스를 제공 합니다.

**생성자**

public LocalRunHelper([System.IO.TextWriter messageOutput = null])

|매개 변수|형식|설명|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|출력 메시지에 대 한 설정 toonull toouse 콘솔|

**속성**

|속성|형식|설명|
|--------|----|-----------|
|AlgebraPath|string|hello tooalgebra 파일 경로 (대 수 파일은 hello 컴파일 결과 중 하나)|
|CodeBehindReferences|string|Hello 스크립트에 대 한 참조 뒤에 있는 추가 코드를 구분 하 여 hello 경로 지정 ';'|
|CppSdkDir|string|CppSDK 디렉터리입니다.|
|CurrentDir|string|현재 디렉터리입니다.|
|DataRoot|string|데이터 루트 경로입니다.|
|DebuggerMailPath|string|hello 경로 toodebugger 메일 슬롯|
|GenerateUdoRedirect|bool|리디렉션 구성 재정의 toogenerate 어셈블리를 로드.|
|HasCodeBehind|bool|Hello 스크립트가 코드를 포함 하는 경우|
|InputDir|string|입력 데이터에 대한 디렉터리입니다.|
|MessagePath|string|메시지 덤프 파일 경로입니다.|
|OutputDir|string|출력 데이터에 대한 디렉터리입니다.|
|병렬 처리|int|병렬 처리 수준 toorun hello 대 수|
|ParentPid|int|어떤 hello에 서비스 모니터링 tooexit, 집합 too0 또는 음수 tooignore hello 부모의 PID|
|ResultPath|string|결과 덤프 파일 경로입니다.|
|RuntimeDir|string|런타임 디렉터리입니다.|
|ScriptPath|string|여기서 toofind hello 스크립트|
|Shallow|bool|단순 컴파일이거나 그렇지 않습니다.|
|TempDir|string|임시 디렉터리|
|UseDataBase|string|기본적으로 마스터 임시 어셈블리 등록 뒤에 있는 코드에 대 한 데이터베이스 toouse hello를 지정 합니다.|
|WorkDir|string|기본 설정 작업 디렉터리입니다.|


**메서드**

|메서드|설명|Return|매개 변수를 포함해야 합니다.|
|------|-----------|------|---------|
|public bool DoCompile()|Hello U-SQL 스크립트 컴파일|성공 시 True입니다.| |
|public bool DoExec()|컴파일된 hello 결과 실행|성공 시 True입니다.| |
|public bool DoRun()|(컴파일 + 실행) hello U-SQL 스크립트를 실행 합니다.|성공 시 True입니다.| |
|public bool IsValidRuntimeDir(문자열 경로)|경로 지정 된 hello 런타임 유효한 경로 인지 확인|유효한 경우 True입니다.|런타임 디렉터리의 hello 경로|


## <a name="faq-about-common-issue"></a>일반적인 문제에 대한 FAQ

### <a name="error-1"></a>오류 1:
E_CSC_SYSTEM_INTERNAL: 내부 오류입니다. 파일 또는 어셈블리 'ScopeEngineManaged.dll'이나 해당 종속성 중 하나를 로드할 수 없습니다. hello 지정 된 모듈을 찾을 수 없습니다.

Hello 다음을 참조 하세요.

- X64 환경인지 확인합니다. hello 빌드 대상 플랫폼 및 hello 테스트 환경 x64 합니다 너무 참조**1 단계: 만들기 C# 단위 테스트 프로젝트 및 구성** 위에 있습니다.
- 모든 종속 파일 NugetPackage\build\runtime\ tooproject 작업 디렉터리에 복사한 있는지 확인 합니다.


## <a name="next-steps"></a>다음 단계

* toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.
* toolog 진단 정보 참조 [Azure Data Lake 분석에 대 한 진단 로그에 액세스](data-lake-analytics-diagnostic-logs.md)합니다.
* toosee 복잡 한 쿼리를 참조 [Azure 데이터 레이크 분석을 사용 하 여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)합니다.
* tooview 작업 세부 정보 참조 [사용 하 여 작업 브라우저와 Azure 데이터 레이크 분석 작업에 대 한 작업 보기](data-lake-analytics-data-lake-tools-view-jobs.md)합니다.
* toouse hello 꼭 짓 점 실행 보기 참조 [꼭 짓 점 실행 보기 데이터 레이크 Tools for Visual Studio에서에서 사용 하 여 hello](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)합니다.
