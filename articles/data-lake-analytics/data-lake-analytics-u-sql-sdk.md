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
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="9155f-103">Azure Data Lake U-SQL SDK를 사용하여 U-SQL 로컬 실행 및 테스트 규모 조정</span><span class="sxs-lookup"><span data-stu-id="9155f-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="9155f-104">U-SQL 스크립트를 개발할 때 일반적인 toorun 이며 테스트 U-SQL 스크립트를 로컬로 전에 제출 toocloud입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="9155f-105">Azure Data Lake는 이 시나리오에 대해 Azure Data Lake U-SQL SDK라는 Nuget 패키지를 제공합니다. 이를 통해 U-SQL 로컬 실행 및 테스트 규모를 쉽게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="9155f-106">이 U-SQL CI (연속 통합) 시스템 tooautomate hello 컴파일 및 테스트와 테스트 가능한 toointegrate 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="9155f-107">중요 하지 않은 경우에 대 한 방법을 toomanually 로컬 실행 하 고 디버깅 GUI 도구와 U-SQL 스크립트에 대 한 Visual Studio 용 Azure 데이터 레이크 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="9155f-108">[여기](data-lake-analytics-data-lake-tools-local-run.md)에서 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="9155f-109">Azure Data Lake U-SQL SDK 설치</span><span class="sxs-lookup"><span data-stu-id="9155f-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="9155f-110">Azure 데이터 레이크 U-SQL SDK hello를 얻을 수 [여기](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) Nuget.org에 있습니다. 및를 사용 하기 전에 필요 toomake 종속성을 다음과 같이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="9155f-111">종속성</span><span class="sxs-lookup"><span data-stu-id="9155f-111">Dependencies</span></span>

<span data-ttu-id="9155f-112">데이터 레이크 U-SQL SDK hello를 hello를 종속성 다음 사항이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="9155f-113">[Microsoft .NET Framework 4.6 이상](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="9155f-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="9155f-114">Microsoft Visual C++ 14 및 Windows SDK 10.0.10240.0 이상(이 문서에서는 CppSDK로 지칭함).</span><span class="sxs-lookup"><span data-stu-id="9155f-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="9155f-115">두 가지 방법으로 tooget CppSDK 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="9155f-116">[Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="9155f-117">예를 들어 C:\Program Files (x86) \Windows Kits\10\ hello Program Files 폴더 아래에서 \Windows Kits\10 폴더를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="9155f-118">또한 \Windows Kits\10\Lib에서 hello Windows 10 SDK 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="9155f-119">이러한 폴더 보이지 않으면 Visual Studio를 다시 설치 하 고 있는지 tooselect hello Windows 10 SDK hello 설치 중 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="9155f-120">Visual Studio와 함께 설치 된이 있다면 hello U-SQL 로컬 컴파일러 것 자동으로.</span><span class="sxs-lookup"><span data-stu-id="9155f-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![Data Lake Tools for Visual Studio의 Windows 10 SDK 로컬 실행](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="9155f-122">[Visual Studio용 Data Lake 도구](http://aka.ms/adltoolsvs)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="9155f-123">Hello (x86) C:\Program Files \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK에서 Visual c + + 및 Windows SDK 파일을 사전 포장 된 고품위 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="9155f-124">이 경우 hello U-SQL 로컬 컴파일러 hello 종속성을 자동으로 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="9155f-125">에 대 한 toospecify hello CppSDK 경로가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="9155f-126">Hello 파일 tooanother 위치를 복사 하거나 있는 그대로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="9155f-127">기본 개념 이해</span><span class="sxs-lookup"><span data-stu-id="9155f-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="9155f-128">데이터 루트</span><span class="sxs-lookup"><span data-stu-id="9155f-128">Data root</span></span>

<span data-ttu-id="9155f-129">hello 데이터 루트 폴더는 hello 로컬 계산 계정에 대 한 "로컬 저장소".</span><span class="sxs-lookup"><span data-stu-id="9155f-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="9155f-130">이 Data Lake 분석 계정 해당 toohello Azure 데이터 레이크 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="9155f-131">다른 저장소 계정 tooa 전환와 동일 하 게 서로 다른 데이터 루트 폴더는 tooa 전환입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="9155f-132">Tooaccess 서로 다른 데이터 루트 폴더와 일반적으로 데이터를 공유 하려면 스크립트에서 절대 경로 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="9155f-133">또는 파일 시스템에 대 한 기호화 된 링크를 만듭니다 (예를 들어 **mklink** ntfs) hello 데이터 루트 폴더 toopoint toohello에서 데이터를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="9155f-134">hello 데이터 루트 폴더에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="9155f-135">데이터베이스, 테이블, TVF(테이블 반환 함수), 어셈블리 등의 로컬 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="9155f-136">입력 hello 및 U-SQL에 상대 경로로 정의 된 출력 경로를 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="9155f-137">상대 경로 사용 하 여 사용 하면 보다 쉽게 toodeploy U-SQL 프로젝트 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="9155f-138">U-SQL의 파일 경로</span><span class="sxs-lookup"><span data-stu-id="9155f-138">File path in U-SQL</span></span>

<span data-ttu-id="9155f-139">U-SQL 스크립트의 상대 경로 및 로컬 절대 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="9155f-140">hello 상대 경로 상대 toohello 지정한 데이터 루트 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="9155f-141">하면 사용 하 여 "/"로 hello 경로 구분 기호 toomake 스크립트 hello 서버 쪽와 호환 되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="9155f-142">다음은 상대 경로 및 이와 대등한 절대 경로의 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="9155f-143">다음 예에서 C:\LocalRunDataRoot는 hello 데이터 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="9155f-144">상대 경로</span><span class="sxs-lookup"><span data-stu-id="9155f-144">Relative path</span></span>|<span data-ttu-id="9155f-145">절대 경로</span><span class="sxs-lookup"><span data-stu-id="9155f-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="9155f-146">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="9155f-146">/abc/def/input.csv</span></span> |<span data-ttu-id="9155f-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="9155f-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="9155f-148">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="9155f-148">abc/def/input.csv</span></span>  |<span data-ttu-id="9155f-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="9155f-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="9155f-150">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="9155f-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="9155f-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="9155f-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="9155f-152">작업 디렉터리</span><span class="sxs-lookup"><span data-stu-id="9155f-152">Working directory</span></span>

<span data-ttu-id="9155f-153">Hello U-SQL 스크립트를 로컬로 실행할 때 현재 실행 중인 디렉터리에서 컴파일하는 동안 작업 디렉터리가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="9155f-154">또한 toohello 컴파일 출력 hello 필요한 로컬 실행에 대 한 런타임 파일 됩니다 섀도 복사한 toothis 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="9155f-155">작업 디렉터리 루트 폴더 hello "ScopeWorkDir" 라고 하 고 hello 작업 디렉터리 아래에 있는 hello 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="9155f-156">디렉터리/파일</span><span class="sxs-lookup"><span data-stu-id="9155f-156">Directory/file</span></span>|<span data-ttu-id="9155f-157">디렉터리/파일</span><span class="sxs-lookup"><span data-stu-id="9155f-157">Directory/file</span></span>|<span data-ttu-id="9155f-158">디렉터리/파일</span><span class="sxs-lookup"><span data-stu-id="9155f-158">Directory/file</span></span>|<span data-ttu-id="9155f-159">정의</span><span class="sxs-lookup"><span data-stu-id="9155f-159">Definition</span></span>|<span data-ttu-id="9155f-160">설명</span><span class="sxs-lookup"><span data-stu-id="9155f-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="9155f-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="9155f-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="9155f-162">런타임 버전의 해시 문자열</span><span class="sxs-lookup"><span data-stu-id="9155f-162">Hash string of runtime version</span></span>|<span data-ttu-id="9155f-163">로컬 실행에 필요한 런타임 파일의 섀도 복사본</span><span class="sxs-lookup"><span data-stu-id="9155f-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="9155f-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="9155f-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="9155f-165">스크립트 이름 + 스크립트 경로의 해시 문자열</span><span class="sxs-lookup"><span data-stu-id="9155f-165">Script name + hash string of script path</span></span>|<span data-ttu-id="9155f-166">컴파일 출력 및 실행 단계 로깅</span><span class="sxs-lookup"><span data-stu-id="9155f-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="9155f-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="9155f-167">\_script\_.abr</span></span>|<span data-ttu-id="9155f-168">컴파일러 출력</span><span class="sxs-lookup"><span data-stu-id="9155f-168">Compiler output</span></span>|<span data-ttu-id="9155f-169">대수 파일</span><span class="sxs-lookup"><span data-stu-id="9155f-169">Algebra file</span></span>|
| | |<span data-ttu-id="9155f-170">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="9155f-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="9155f-171">컴파일러 출력</span><span class="sxs-lookup"><span data-stu-id="9155f-171">Compiler output</span></span>|<span data-ttu-id="9155f-172">생성된 관리 코드</span><span class="sxs-lookup"><span data-stu-id="9155f-172">Generated managed code</span></span>|
| | |<span data-ttu-id="9155f-173">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="9155f-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="9155f-174">컴파일러 출력</span><span class="sxs-lookup"><span data-stu-id="9155f-174">Compiler output</span></span>|<span data-ttu-id="9155f-175">생성된 네이티브 코드</span><span class="sxs-lookup"><span data-stu-id="9155f-175">Generated native code</span></span>|
| | |<span data-ttu-id="9155f-176">참조된 어셈블리</span><span class="sxs-lookup"><span data-stu-id="9155f-176">referenced assemblies</span></span>|<span data-ttu-id="9155f-177">어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="9155f-177">Assembly reference</span></span>|<span data-ttu-id="9155f-178">참조된 어셈블리 파일</span><span class="sxs-lookup"><span data-stu-id="9155f-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="9155f-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="9155f-179">deployed_resources</span></span>|<span data-ttu-id="9155f-180">리소스 배포</span><span class="sxs-lookup"><span data-stu-id="9155f-180">Resource deployment</span></span>|<span data-ttu-id="9155f-181">리소스 배포 파일</span><span class="sxs-lookup"><span data-stu-id="9155f-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="9155f-182">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="9155f-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="9155f-183">실행 로그</span><span class="sxs-lookup"><span data-stu-id="9155f-183">Execution log</span></span>|<span data-ttu-id="9155f-184">실행 단계에 대한 로그</span><span class="sxs-lookup"><span data-stu-id="9155f-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="9155f-185">Hello 명령줄에서 SDK hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9155f-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="9155f-186">Hello 도우미 응용 프로그램의 명령줄 인터페이스</span><span class="sxs-lookup"><span data-stu-id="9155f-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="9155f-187">SDK directory\build\runtime에서 LocalRunHelper.exe 인터페이스의 일반적으로 사용 하는 hello toomost 로컬 실행 기능을 제공 하는 hello 명령줄 도우미 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="9155f-188">Note 명령을 모두 hello 및 hello 인수 스위치는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="9155f-189">tooinvoke 하기:</span><span class="sxs-lookup"><span data-stu-id="9155f-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="9155f-190">인수 없이 또는 hello로 LocalRunHelper.exe 실행 **도움말** 스위치 tooshow hello 도움말 정보:</span><span class="sxs-lookup"><span data-stu-id="9155f-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="9155f-191">Hello에 지원 정보:</span><span class="sxs-lookup"><span data-stu-id="9155f-191">In hello help information:</span></span>

-  <span data-ttu-id="9155f-192">**명령** 제공 hello 명령의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="9155f-193">**Required Argument**: 제공해야 하는 인수를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="9155f-194">**Optional Argument**: 선택적이며 기본값을 갖는 인수를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="9155f-195">선택적 부울 인수 매개 변수 및 모양을 음수 tootheir 기본값을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="9155f-196">반환 값 및 로깅</span><span class="sxs-lookup"><span data-stu-id="9155f-196">Return value and logging</span></span>

<span data-ttu-id="9155f-197">hello 도우미 응용 프로그램이 반환 **0** 성공 및 **-1** 실패에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="9155f-198">기본적으로 hello 도우미 모든 메시지 toohello 현재 콘솔을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="9155f-199">그러나 대부분의 hello 명령은 지원 hello **-MessageOut path_to_log_file** hello 리디렉션하는 선택적 인수 tooa 로그 파일을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="9155f-200">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="9155f-200">Environment variable configuring</span></span>

<span data-ttu-id="9155f-201">U-SQL 로컬 실행을 위해서는 지정된 데이터 루트가 로컬 저장소 계정으로 필요하고, 종속성에 대해 지정된 CppSDK 경로가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="9155f-202">명령줄 또는 설정 환경 변수에서 집합 hello 인수 둘 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="9155f-203">집합 hello **SCOPE_CPP_SDK** 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="9155f-204">Visual Studio에 대 한 데이터 레이크 도구를 설치 하 여 Microsoft Visual c + + 및 Windows SDK hello를 얻게 폴더 다음 hello 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="9155f-205">라는 새 환경 변수를 정의 **SCOPE_CPP_SDK** toopoint toothis 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="9155f-206">또는 hello 폴더 toohello 다른 위치를 복사 하 고 지정 **SCOPE_CPP_SDK** 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="9155f-207">또한 toosetting hello 환경 변수에서 hello를 지정할 수 있습니다 **-CppSDK** hello 명령줄을 사용 하는 경우에 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="9155f-208">이 인수는 기본 CppSDK 환경 변수를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="9155f-209">집합 hello **LOCALRUN_DATAROOT** 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="9155f-210">라는 새 환경 변수를 정의 **LOCALRUN_DATAROOT** toohello 데이터 루트를 가리키는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="9155f-211">또한 toosetting hello 환경 변수에서 hello를 지정할 수 있습니다 **-DataRoot** 인수 명령줄을 사용 하는 경우 hello 데이터 루트 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="9155f-212">이 인수는 기본 데이터 루트 환경 변수를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="9155f-213">이 인수 tooevery 명령줄 hello 모든 작업에 대 한 기본 데이터 루트 환경 변수를 덮어쓸 수 있도록 실행 하는 tooadd 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="9155f-214">SDK 명령줄 사용 샘플</span><span class="sxs-lookup"><span data-stu-id="9155f-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="9155f-215">컴파일 및 실행</span><span class="sxs-lookup"><span data-stu-id="9155f-215">Compile and run</span></span>

<span data-ttu-id="9155f-216">hello **실행** 명령을 사용 하 여 toocompile 스크립트 hello 및 다음 컴파일된 결과 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="9155f-217">명령줄 인수는 **compile**과 **execute**의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="9155f-218">hello 다음은 하기 위한 선택적 인수 **실행**:</span><span class="sxs-lookup"><span data-stu-id="9155f-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="9155f-219">인수</span><span class="sxs-lookup"><span data-stu-id="9155f-219">Argument</span></span>|<span data-ttu-id="9155f-220">기본값</span><span class="sxs-lookup"><span data-stu-id="9155f-220">Default value</span></span>|<span data-ttu-id="9155f-221">설명</span><span class="sxs-lookup"><span data-stu-id="9155f-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="9155f-222">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="9155f-222">-CodeBehind</span></span>|<span data-ttu-id="9155f-223">False</span><span class="sxs-lookup"><span data-stu-id="9155f-223">False</span></span>|<span data-ttu-id="9155f-224">hello 스크립트의.cs 코드 숨김</span><span class="sxs-lookup"><span data-stu-id="9155f-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="9155f-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="9155f-225">-CppSDK</span></span>| |<span data-ttu-id="9155f-226">CppSDK 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-226">CppSDK Directory</span></span>|
|<span data-ttu-id="9155f-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="9155f-227">-DataRoot</span></span>| <span data-ttu-id="9155f-228">DataRoot 환경 변수</span><span class="sxs-lookup"><span data-stu-id="9155f-228">DataRoot environment variable</span></span>|<span data-ttu-id="9155f-229">로컬 실행에 대 한 DataRoot 너무 기본 'LOCALRUN_DATAROOT' 환경 변수</span><span class="sxs-lookup"><span data-stu-id="9155f-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="9155f-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="9155f-230">-MessageOut</span></span>| |<span data-ttu-id="9155f-231">콘솔 tooa 파일에 메시지를 덤프 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="9155f-232">-Parallel</span><span class="sxs-lookup"><span data-stu-id="9155f-232">-Parallel</span></span>|<span data-ttu-id="9155f-233">1</span><span class="sxs-lookup"><span data-stu-id="9155f-233">1</span></span>|<span data-ttu-id="9155f-234">Hello 실행 계획 hello로 병렬 처리 수준 지정</span><span class="sxs-lookup"><span data-stu-id="9155f-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="9155f-235">-References</span><span class="sxs-lookup"><span data-stu-id="9155f-235">-References</span></span>| |<span data-ttu-id="9155f-236">구분 하 여 tooextra 참조 어셈블리 경로 또는 코드 숨김의 데이터 파일의 목록 ';'</span><span class="sxs-lookup"><span data-stu-id="9155f-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="9155f-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="9155f-237">-UdoRedirect</span></span>|<span data-ttu-id="9155f-238">False</span><span class="sxs-lookup"><span data-stu-id="9155f-238">False</span></span>|<span data-ttu-id="9155f-239">Udo 어셈블리 리디렉션 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="9155f-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="9155f-240">-UseDatabase</span></span>|<span data-ttu-id="9155f-241">master</span><span class="sxs-lookup"><span data-stu-id="9155f-241">master</span></span>|<span data-ttu-id="9155f-242">임시 어셈블리 등록 뒤에 있는 코드에 대 한 데이터베이스 toouse</span><span class="sxs-lookup"><span data-stu-id="9155f-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="9155f-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="9155f-243">-Verbose</span></span>|<span data-ttu-id="9155f-244">False</span><span class="sxs-lookup"><span data-stu-id="9155f-244">False</span></span>|<span data-ttu-id="9155f-245">런타임의 자세한 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="9155f-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="9155f-246">-WorkDir</span></span>|<span data-ttu-id="9155f-247">현재 디렉터리</span><span class="sxs-lookup"><span data-stu-id="9155f-247">Current Directory</span></span>|<span data-ttu-id="9155f-248">컴파일러 사용 및 출력을 위한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="9155f-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="9155f-249">-RunScopeCEP</span></span>|<span data-ttu-id="9155f-250">0</span><span class="sxs-lookup"><span data-stu-id="9155f-250">0</span></span>|<span data-ttu-id="9155f-251">ScopeCEP 모드 toouse</span><span class="sxs-lookup"><span data-stu-id="9155f-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="9155f-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="9155f-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="9155f-253">temp</span><span class="sxs-lookup"><span data-stu-id="9155f-253">temp</span></span>|<span data-ttu-id="9155f-254">스트리밍 데이터에 대 한 임시 경로 toouse</span><span class="sxs-lookup"><span data-stu-id="9155f-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="9155f-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="9155f-255">-OptFlags</span></span>| |<span data-ttu-id="9155f-256">쉼표로 구분된 최적화 프로그램 플래그 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="9155f-257">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="9155f-258">결합 외에도 **컴파일** 및 **실행**, 컴파일 및 hello 컴파일된 실행 파일을 개별적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="9155f-259">U-SQL 스크립트 컴파일</span><span class="sxs-lookup"><span data-stu-id="9155f-259">Compile a U-SQL script</span></span>

<span data-ttu-id="9155f-260">hello **컴파일** 명령에 사용 되는 toocompile는 U-SQL 스크립트 tooexecutables입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="9155f-261">hello 다음은 하기 위한 선택적 인수 **컴파일**:</span><span class="sxs-lookup"><span data-stu-id="9155f-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="9155f-262">인수</span><span class="sxs-lookup"><span data-stu-id="9155f-262">Argument</span></span>|<span data-ttu-id="9155f-263">설명</span><span class="sxs-lookup"><span data-stu-id="9155f-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="9155f-264">-CodeBehind [기본값 'False']</span><span class="sxs-lookup"><span data-stu-id="9155f-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="9155f-265">hello 스크립트의.cs 코드 숨김</span><span class="sxs-lookup"><span data-stu-id="9155f-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="9155f-266">-CppSDK [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="9155f-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="9155f-267">CppSDK 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-267">CppSDK Directory</span></span>|
| <span data-ttu-id="9155f-268">-DataRoot [기본값 'DataRoot 환경 변수']</span><span class="sxs-lookup"><span data-stu-id="9155f-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="9155f-269">로컬 실행에 대 한 DataRoot 너무 기본 'LOCALRUN_DATAROOT' 환경 변수</span><span class="sxs-lookup"><span data-stu-id="9155f-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="9155f-270">-MessageOut [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="9155f-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="9155f-271">콘솔 tooa 파일에 메시지를 덤프 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="9155f-272">-References [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="9155f-272">-References [default value '']</span></span>|<span data-ttu-id="9155f-273">구분 하 여 tooextra 참조 어셈블리 경로 또는 코드 숨김의 데이터 파일의 목록 ';'</span><span class="sxs-lookup"><span data-stu-id="9155f-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="9155f-274">-Shallow [기본값 'False']</span><span class="sxs-lookup"><span data-stu-id="9155f-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="9155f-275">단순 컴파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-275">Shallow compile</span></span>|
| <span data-ttu-id="9155f-276">-UdoRedirect [기본값 'False']</span><span class="sxs-lookup"><span data-stu-id="9155f-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="9155f-277">Udo 어셈블리 리디렉션 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="9155f-278">-UseDatabase [기본값 'master']</span><span class="sxs-lookup"><span data-stu-id="9155f-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="9155f-279">임시 어셈블리 등록 뒤에 있는 코드에 대 한 데이터베이스 toouse</span><span class="sxs-lookup"><span data-stu-id="9155f-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="9155f-280">-WorkDir [기본값 '현재 디렉터리']</span><span class="sxs-lookup"><span data-stu-id="9155f-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="9155f-281">컴파일러 사용 및 출력을 위한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="9155f-282">-RunScopeCEP [기본값 '0']</span><span class="sxs-lookup"><span data-stu-id="9155f-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="9155f-283">ScopeCEP 모드 toouse</span><span class="sxs-lookup"><span data-stu-id="9155f-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="9155f-284">-ScopeCEPTempPath [기본값 'temp']</span><span class="sxs-lookup"><span data-stu-id="9155f-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="9155f-285">스트리밍 데이터에 대 한 임시 경로 toouse</span><span class="sxs-lookup"><span data-stu-id="9155f-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="9155f-286">-OptFlags [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="9155f-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="9155f-287">쉼표로 구분된 최적화 프로그램 플래그 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="9155f-288">몇 가지 사용 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-288">Here are some usage examples.</span></span>

<span data-ttu-id="9155f-289">U-SQL 스크립트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="9155f-290">U-SQL 스크립트를 컴파일하고 hello 데이터 루트 폴더를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="9155f-291">Note 이렇게 환경 변수를 설정 하는 hello 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="9155f-292">U-SQL 스크립트를 컴파일하고 작업 디렉터리, 참조 어셈블리 및 데이터베이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="9155f-293">컴파일된 결과 실행</span><span class="sxs-lookup"><span data-stu-id="9155f-293">Execute compiled results</span></span>

<span data-ttu-id="9155f-294">hello **실행** 명령에 사용 되는 tooexecute 컴파일 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="9155f-295">hello 다음은 하기 위한 선택적 인수 **실행**:</span><span class="sxs-lookup"><span data-stu-id="9155f-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="9155f-296">인수</span><span class="sxs-lookup"><span data-stu-id="9155f-296">Argument</span></span>|<span data-ttu-id="9155f-297">설명</span><span class="sxs-lookup"><span data-stu-id="9155f-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="9155f-298">-DataRoot [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="9155f-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="9155f-299">메타데이터 실행을 위한 루트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-299">Data root for metadata execution.</span></span> <span data-ttu-id="9155f-300">기본적으로 toohello **LOCALRUN_DATAROOT** 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="9155f-301">-MessageOut [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="9155f-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="9155f-302">Hello 콘솔 tooa 파일에 메시지를 덤프 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="9155f-303">-Parallel [기본값 '1']</span><span class="sxs-lookup"><span data-stu-id="9155f-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="9155f-304">병렬 처리 수준을 지정 하는 hello 사용 하 여 표시기 toorun 생성 hello 로컬 실행 단계.</span><span class="sxs-lookup"><span data-stu-id="9155f-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="9155f-305">-Verbose [기본값 'False']</span><span class="sxs-lookup"><span data-stu-id="9155f-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="9155f-306">표시기 tooshow 자세한 런타임에서 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="9155f-307">사용 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="9155f-308">프로그래밍 인터페이스를 사용 하 여 hello SDK</span><span class="sxs-lookup"><span data-stu-id="9155f-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="9155f-309">hello 프로그래밍 인터페이스는 모두 LocalRunHelper.exe hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="9155f-310">Hello U-SQL SDK의 toointegrate hello 기능을 사용 하 고 hello C# 테스트 프레임 워크 tooscale U-SQL 스크립트 로컬 테스트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="9155f-311">이 문서에서는 hello 표준 C# 단위 테스트 프로젝트 tooshow를 어떻게 사용 합니다 toouse 이러한 U-SQL 스크립트 tootest 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="9155f-312">1단계: C# 단위 테스트 프로젝트 및 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="9155f-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="9155f-313">파일 > 새로 만들기 > 프로젝트 > Visual C# > 테스트 > 단위 테스트 프로젝트를 통해 C# 단위 테스트 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="9155f-314">LocalRunHelper.exe hello 프로젝트에 대 한 참조로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="9155f-315">hello LocalRunHelper.exe는 Nuget 패키지에 \build\runtime\LocalRunHelper.exe에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Azure Data Lake U-SQL SDK 참조 추가](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="9155f-317">U-SQL SDK **만** x64로 확인 되었는지 tooset 빌드 플랫폼 대상 x64 지원 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="9155f-318">프로젝트 속성 > 빌드 > 플랫폼 대상을 통해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Azure Data Lake U-SQL SDK x64 프로젝트 구성](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="9155f-320">X64로 있는지 tooset 테스트 환경을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="9155f-321">Visual Studio에서 테스트 > 테스트 설정 > 기본 프로세서 아키텍처 > x64를 통해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Azure Data Lake U-SQL SDK x64 테스트 환경 구성](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="9155f-323">일반적으로 ProjectFolder\bin\x64\Debug 아래 있는 NugetPackage\build\runtime\ tooproject 작업 디렉터리에 모든 종속 파일 toocopy 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="9155f-324">2단계: U-SQL 스크립트 테스트 사례 만들기</span><span class="sxs-lookup"><span data-stu-id="9155f-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="9155f-325">U-SQL 스크립트 테스트에 대 한 hello 샘플 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="9155f-326">Tooprepare 스크립트 테스트를 위해 필요한 입력된 파일 및 예상된 출력 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="9155f-327">LocalRunHelper.exe의 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="9155f-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="9155f-328">등 hello 인터페이스는 다음과 같이 나열 된, LocalRunHelper.exe hello 프로그래밍 U-SQL 로컬 컴파일, 실행에 대 한 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="9155f-329">**생성자**</span><span class="sxs-lookup"><span data-stu-id="9155f-329">**Constructor**</span></span>

<span data-ttu-id="9155f-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="9155f-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="9155f-331">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9155f-331">Parameter</span></span>|<span data-ttu-id="9155f-332">형식</span><span class="sxs-lookup"><span data-stu-id="9155f-332">Type</span></span>|<span data-ttu-id="9155f-333">설명</span><span class="sxs-lookup"><span data-stu-id="9155f-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="9155f-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="9155f-334">messageOutput</span></span>|<span data-ttu-id="9155f-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="9155f-335">System.IO.TextWriter</span></span>|<span data-ttu-id="9155f-336">출력 메시지에 대 한 설정 toonull toouse 콘솔</span><span class="sxs-lookup"><span data-stu-id="9155f-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="9155f-337">**속성**</span><span class="sxs-lookup"><span data-stu-id="9155f-337">**Properties**</span></span>

|<span data-ttu-id="9155f-338">속성</span><span class="sxs-lookup"><span data-stu-id="9155f-338">Property</span></span>|<span data-ttu-id="9155f-339">형식</span><span class="sxs-lookup"><span data-stu-id="9155f-339">Type</span></span>|<span data-ttu-id="9155f-340">설명</span><span class="sxs-lookup"><span data-stu-id="9155f-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="9155f-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="9155f-341">AlgebraPath</span></span>|<span data-ttu-id="9155f-342">string</span><span class="sxs-lookup"><span data-stu-id="9155f-342">string</span></span>|<span data-ttu-id="9155f-343">hello tooalgebra 파일 경로 (대 수 파일은 hello 컴파일 결과 중 하나)</span><span class="sxs-lookup"><span data-stu-id="9155f-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="9155f-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="9155f-344">CodeBehindReferences</span></span>|<span data-ttu-id="9155f-345">string</span><span class="sxs-lookup"><span data-stu-id="9155f-345">string</span></span>|<span data-ttu-id="9155f-346">Hello 스크립트에 대 한 참조 뒤에 있는 추가 코드를 구분 하 여 hello 경로 지정 ';'</span><span class="sxs-lookup"><span data-stu-id="9155f-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="9155f-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="9155f-347">CppSdkDir</span></span>|<span data-ttu-id="9155f-348">string</span><span class="sxs-lookup"><span data-stu-id="9155f-348">string</span></span>|<span data-ttu-id="9155f-349">CppSDK 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-349">CppSDK directory</span></span>|
|<span data-ttu-id="9155f-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="9155f-350">CurrentDir</span></span>|<span data-ttu-id="9155f-351">string</span><span class="sxs-lookup"><span data-stu-id="9155f-351">string</span></span>|<span data-ttu-id="9155f-352">현재 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-352">Current directory</span></span>|
|<span data-ttu-id="9155f-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="9155f-353">DataRoot</span></span>|<span data-ttu-id="9155f-354">string</span><span class="sxs-lookup"><span data-stu-id="9155f-354">string</span></span>|<span data-ttu-id="9155f-355">데이터 루트 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-355">Data root path</span></span>|
|<span data-ttu-id="9155f-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="9155f-356">DebuggerMailPath</span></span>|<span data-ttu-id="9155f-357">string</span><span class="sxs-lookup"><span data-stu-id="9155f-357">string</span></span>|<span data-ttu-id="9155f-358">hello 경로 toodebugger 메일 슬롯</span><span class="sxs-lookup"><span data-stu-id="9155f-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="9155f-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="9155f-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="9155f-360">bool</span><span class="sxs-lookup"><span data-stu-id="9155f-360">bool</span></span>|<span data-ttu-id="9155f-361">리디렉션 구성 재정의 toogenerate 어셈블리를 로드.</span><span class="sxs-lookup"><span data-stu-id="9155f-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="9155f-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="9155f-362">HasCodeBehind</span></span>|<span data-ttu-id="9155f-363">bool</span><span class="sxs-lookup"><span data-stu-id="9155f-363">bool</span></span>|<span data-ttu-id="9155f-364">Hello 스크립트가 코드를 포함 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9155f-364">If hello script has code behind</span></span>|
|<span data-ttu-id="9155f-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="9155f-365">InputDir</span></span>|<span data-ttu-id="9155f-366">string</span><span class="sxs-lookup"><span data-stu-id="9155f-366">string</span></span>|<span data-ttu-id="9155f-367">입력 데이터에 대한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-367">Directory for input data</span></span>|
|<span data-ttu-id="9155f-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="9155f-368">MessagePath</span></span>|<span data-ttu-id="9155f-369">string</span><span class="sxs-lookup"><span data-stu-id="9155f-369">string</span></span>|<span data-ttu-id="9155f-370">메시지 덤프 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-370">Message dump file path</span></span>|
|<span data-ttu-id="9155f-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="9155f-371">OutputDir</span></span>|<span data-ttu-id="9155f-372">string</span><span class="sxs-lookup"><span data-stu-id="9155f-372">string</span></span>|<span data-ttu-id="9155f-373">출력 데이터에 대한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-373">Directory for output data</span></span>|
|<span data-ttu-id="9155f-374">병렬 처리</span><span class="sxs-lookup"><span data-stu-id="9155f-374">Parallelism</span></span>|<span data-ttu-id="9155f-375">int</span><span class="sxs-lookup"><span data-stu-id="9155f-375">int</span></span>|<span data-ttu-id="9155f-376">병렬 처리 수준 toorun hello 대 수</span><span class="sxs-lookup"><span data-stu-id="9155f-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="9155f-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="9155f-377">ParentPid</span></span>|<span data-ttu-id="9155f-378">int</span><span class="sxs-lookup"><span data-stu-id="9155f-378">int</span></span>|<span data-ttu-id="9155f-379">어떤 hello에 서비스 모니터링 tooexit, 집합 too0 또는 음수 tooignore hello 부모의 PID</span><span class="sxs-lookup"><span data-stu-id="9155f-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="9155f-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="9155f-380">ResultPath</span></span>|<span data-ttu-id="9155f-381">string</span><span class="sxs-lookup"><span data-stu-id="9155f-381">string</span></span>|<span data-ttu-id="9155f-382">결과 덤프 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-382">Result dump file path</span></span>|
|<span data-ttu-id="9155f-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="9155f-383">RuntimeDir</span></span>|<span data-ttu-id="9155f-384">string</span><span class="sxs-lookup"><span data-stu-id="9155f-384">string</span></span>|<span data-ttu-id="9155f-385">런타임 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-385">Runtime directory</span></span>|
|<span data-ttu-id="9155f-386">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="9155f-386">ScriptPath</span></span>|<span data-ttu-id="9155f-387">string</span><span class="sxs-lookup"><span data-stu-id="9155f-387">string</span></span>|<span data-ttu-id="9155f-388">여기서 toofind hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="9155f-388">Where toofind hello script</span></span>|
|<span data-ttu-id="9155f-389">Shallow</span><span class="sxs-lookup"><span data-stu-id="9155f-389">Shallow</span></span>|<span data-ttu-id="9155f-390">bool</span><span class="sxs-lookup"><span data-stu-id="9155f-390">bool</span></span>|<span data-ttu-id="9155f-391">단순 컴파일이거나 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-391">Shallow compile or not</span></span>|
|<span data-ttu-id="9155f-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="9155f-392">TempDir</span></span>|<span data-ttu-id="9155f-393">string</span><span class="sxs-lookup"><span data-stu-id="9155f-393">string</span></span>|<span data-ttu-id="9155f-394">임시 디렉터리</span><span class="sxs-lookup"><span data-stu-id="9155f-394">Temp directory</span></span>|
|<span data-ttu-id="9155f-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="9155f-395">UseDataBase</span></span>|<span data-ttu-id="9155f-396">string</span><span class="sxs-lookup"><span data-stu-id="9155f-396">string</span></span>|<span data-ttu-id="9155f-397">기본적으로 마스터 임시 어셈블리 등록 뒤에 있는 코드에 대 한 데이터베이스 toouse hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="9155f-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="9155f-398">WorkDir</span></span>|<span data-ttu-id="9155f-399">string</span><span class="sxs-lookup"><span data-stu-id="9155f-399">string</span></span>|<span data-ttu-id="9155f-400">기본 설정 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-400">Preferred working directory</span></span>|


<span data-ttu-id="9155f-401">**메서드**</span><span class="sxs-lookup"><span data-stu-id="9155f-401">**Method**</span></span>

|<span data-ttu-id="9155f-402">메서드</span><span class="sxs-lookup"><span data-stu-id="9155f-402">Method</span></span>|<span data-ttu-id="9155f-403">설명</span><span class="sxs-lookup"><span data-stu-id="9155f-403">Description</span></span>|<span data-ttu-id="9155f-404">Return</span><span class="sxs-lookup"><span data-stu-id="9155f-404">Return</span></span>|<span data-ttu-id="9155f-405">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="9155f-406">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="9155f-406">public bool DoCompile()</span></span>|<span data-ttu-id="9155f-407">Hello U-SQL 스크립트 컴파일</span><span class="sxs-lookup"><span data-stu-id="9155f-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="9155f-408">성공 시 True입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-408">True on success</span></span>| |
|<span data-ttu-id="9155f-409">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="9155f-409">public bool DoExec()</span></span>|<span data-ttu-id="9155f-410">컴파일된 hello 결과 실행</span><span class="sxs-lookup"><span data-stu-id="9155f-410">Execute hello compiled result</span></span>|<span data-ttu-id="9155f-411">성공 시 True입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-411">True on success</span></span>| |
|<span data-ttu-id="9155f-412">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="9155f-412">public bool DoRun()</span></span>|<span data-ttu-id="9155f-413">(컴파일 + 실행) hello U-SQL 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="9155f-414">성공 시 True입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-414">True on success</span></span>| |
|<span data-ttu-id="9155f-415">public bool IsValidRuntimeDir(문자열 경로)</span><span class="sxs-lookup"><span data-stu-id="9155f-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="9155f-416">경로 지정 된 hello 런타임 유효한 경로 인지 확인</span><span class="sxs-lookup"><span data-stu-id="9155f-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="9155f-417">유효한 경우 True입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-417">True for valid</span></span>|<span data-ttu-id="9155f-418">런타임 디렉터리의 hello 경로</span><span class="sxs-lookup"><span data-stu-id="9155f-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="9155f-419">일반적인 문제에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="9155f-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="9155f-420">오류 1:</span><span class="sxs-lookup"><span data-stu-id="9155f-420">Error 1:</span></span>
<span data-ttu-id="9155f-421">E_CSC_SYSTEM_INTERNAL: 내부 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="9155f-422">파일 또는 어셈블리 'ScopeEngineManaged.dll'이나 해당 종속성 중 하나를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="9155f-423">hello 지정 된 모듈을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-423">hello specified module could not be found.</span></span>

<span data-ttu-id="9155f-424">Hello 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9155f-424">Please check hello following:</span></span>

- <span data-ttu-id="9155f-425">X64 환경인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="9155f-426">hello 빌드 대상 플랫폼 및 hello 테스트 환경 x64 합니다 너무 참조**1 단계: 만들기 C# 단위 테스트 프로젝트 및 구성** 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="9155f-427">모든 종속 파일 NugetPackage\build\runtime\ tooproject 작업 디렉터리에 복사한 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9155f-428">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9155f-428">Next steps</span></span>

* <span data-ttu-id="9155f-429">toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="9155f-430">toolog 진단 정보 참조 [Azure Data Lake 분석에 대 한 진단 로그에 액세스](data-lake-analytics-diagnostic-logs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="9155f-431">toosee 복잡 한 쿼리를 참조 [Azure 데이터 레이크 분석을 사용 하 여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="9155f-432">tooview 작업 세부 정보 참조 [사용 하 여 작업 브라우저와 Azure 데이터 레이크 분석 작업에 대 한 작업 보기](data-lake-analytics-data-lake-tools-view-jobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="9155f-433">toouse hello 꼭 짓 점 실행 보기 참조 [꼭 짓 점 실행 보기 데이터 레이크 Tools for Visual Studio에서에서 사용 하 여 hello](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9155f-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
