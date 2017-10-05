---
title: "Azure Data Lake U-SQL SDK를 사용하여 U-SQL 로컬 실행 및 테스트 규모 조정 | Microsoft Docs"
description: "Azure Data Lake U-SQL SDK를 사용하여 로컬 워크스테이션의 명령줄 및 프로그래밍 인터페이스로 U-SQL 작업 로컬 실행 및 테스트 크기를 조정하는 방법을 알아봅니다."
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
ms.openlocfilehash: 55242bcf644ca0e7f30cfe7eada2130451c36e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="95e26-103">Azure Data Lake U-SQL SDK를 사용하여 U-SQL 로컬 실행 및 테스트 규모 조정</span><span class="sxs-lookup"><span data-stu-id="95e26-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="95e26-104">U-SQL 스크립트를 개발할 때 클라우드로 제출하기 전에 로컬에서 U-SQL 스크립트를 실행하고 테스트하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="95e26-105">Azure Data Lake는 이 시나리오에 대해 Azure Data Lake U-SQL SDK라는 Nuget 패키지를 제공합니다. 이를 통해 U-SQL 로컬 실행 및 테스트 규모를 쉽게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="95e26-106">이 U-SQL 테스트를 CI(연속 통합) 시스템에 통합하여 컴파일 및 테스트를 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="95e26-107">GUI 도구를 사용하여 U-SQL 스크립트를 수동으로 로컬 실행 및 디버깅하는 방법에 관심이 있는 경우 Azure Data Lake Tools for Visual Studio를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="95e26-108">[여기](data-lake-analytics-data-lake-tools-local-run.md)에서 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="95e26-109">Azure Data Lake U-SQL SDK 설치</span><span class="sxs-lookup"><span data-stu-id="95e26-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="95e26-110">Nuget.org의 [여기](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/)에서 Azure Data Lake U-SQL SDK를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org.</span></span> <span data-ttu-id="95e26-111">사용하기 전에 다음과 같이 종속성이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-111">And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="95e26-112">종속성</span><span class="sxs-lookup"><span data-stu-id="95e26-112">Dependencies</span></span>

<span data-ttu-id="95e26-113">Data Lake U-SQL SDK에는 다음과 같은 종속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-113">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="95e26-114">[Microsoft .NET Framework 4.6 이상](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="95e26-114">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="95e26-115">Microsoft Visual C++ 14 및 Windows SDK 10.0.10240.0 이상(이 문서에서는 CppSDK로 지칭함).</span><span class="sxs-lookup"><span data-stu-id="95e26-115">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="95e26-116">CppSDK는 다음 두 가지 방법으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-116">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="95e26-117">[Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-117">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="95e26-118">프로그램 파일 폴더 아래에 \Windows Kits\10 폴더가 생성됩니다(예: C:\Program Files (x86)\Windows Kits\10\).</span><span class="sxs-lookup"><span data-stu-id="95e26-118">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="95e26-119">또한 \Windows Kits\10\Lib 아래에서 Windows 10 SDK 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-119">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="95e26-120">이들 폴더가 보이지 않으면 Visual Studio를 다시 설치하고 설치하는 동중 Windows 10 SDK를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-120">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="95e26-121">Visual Studio와 함께 설치된 경우에는 U-SQL 로컬 컴파일러가 해당 버전을 자동으로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-121">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![Data Lake Tools for Visual Studio의 Windows 10 SDK 로컬 실행](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="95e26-123">[Visual Studio용 Data Lake 도구](http://aka.ms/adltoolsvs)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-123">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="95e26-124">미리 패키지된 Visual C++ 및 Windows SDK 파일은 C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-124">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="95e26-125">이 경우 U-SQL 로컬 컴파일러는 이러한 종속성을 자동으로 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-125">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="95e26-126">이에 대한 CppSDK 경로를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-126">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="95e26-127">파일을 다른 위치로 복사하거나 그대로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-127">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="95e26-128">기본 개념 이해</span><span class="sxs-lookup"><span data-stu-id="95e26-128">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="95e26-129">데이터 루트</span><span class="sxs-lookup"><span data-stu-id="95e26-129">Data root</span></span>

<span data-ttu-id="95e26-130">데이터 루트 폴더는 로컬 계산 계정의 "로컬 저장소"입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-130">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="95e26-131">이는 Data Lake Analytics 계정의 Azure Data Lake Store 계정과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-131">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="95e26-132">다른 데이터 루트 폴더로 전환하는 것은 다른 저장소 계정으로 전환하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-132">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="95e26-133">다른 데이터 루트 폴더와 공유된 데이터에 액세스하려는 경우 스크립트에서 절대 경로를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-133">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="95e26-134">또는 데이터 루트 폴더 아래에 파일 시스템 심볼 링크를 만들어 공유 데이터를 가리키도록 합니다(예, NTFS의 **mklink**).</span><span class="sxs-lookup"><span data-stu-id="95e26-134">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="95e26-135">데이터 루트 폴더는 다음 용도로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-135">The data-root folder is used to:</span></span>

- <span data-ttu-id="95e26-136">데이터베이스, 테이블, TVF(테이블 반환 함수), 어셈블리 등의 로컬 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-136">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="95e26-137">U-SQL에서 상대 경로로 정의된 입력 및 출력 경로 조회 -</span><span class="sxs-lookup"><span data-stu-id="95e26-137">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="95e26-138">상대 경로를 사용하면 U-SQL 프로젝트를 Azure에 보다 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-138">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="95e26-139">U-SQL의 파일 경로</span><span class="sxs-lookup"><span data-stu-id="95e26-139">File path in U-SQL</span></span>

<span data-ttu-id="95e26-140">U-SQL 스크립트의 상대 경로 및 로컬 절대 경로를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-140">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="95e26-141">상대 경로는 지정된 데이터-루트 폴더 경로 기준으로 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-141">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="95e26-142">스크립트를 서버 쪽과 호환되게 하려면 경로 구분 기호로 "/"를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-142">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="95e26-143">다음은 상대 경로 및 이와 대등한 절대 경로의 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-143">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="95e26-144">이 예에서 C:\LocalRunDataRoot는 데이터 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-144">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="95e26-145">상대 경로</span><span class="sxs-lookup"><span data-stu-id="95e26-145">Relative path</span></span>|<span data-ttu-id="95e26-146">절대 경로</span><span class="sxs-lookup"><span data-stu-id="95e26-146">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="95e26-147">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="95e26-147">/abc/def/input.csv</span></span> |<span data-ttu-id="95e26-148">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="95e26-148">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="95e26-149">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="95e26-149">abc/def/input.csv</span></span>  |<span data-ttu-id="95e26-150">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="95e26-150">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="95e26-151">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="95e26-151">D:/abc/def/input.csv</span></span> |<span data-ttu-id="95e26-152">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="95e26-152">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="95e26-153">작업 디렉터리</span><span class="sxs-lookup"><span data-stu-id="95e26-153">Working directory</span></span>

<span data-ttu-id="95e26-154">U-SQL 스크립트를 로컬로 실행하면 컴파일 중에 현재 실행 중인 디렉터리 아래에 작업 디렉터리가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-154">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="95e26-155">컴파일 결과 외에도 로컬 실행에 필요한 런타임 파일이 이 작업 디렉터리에 섀도 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-155">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="95e26-156">작업 디렉터리 루트 폴더를 "ScopeWorkDir"이라고 하고 작업 디렉터리 아래의 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-156">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="95e26-157">디렉터리/파일</span><span class="sxs-lookup"><span data-stu-id="95e26-157">Directory/file</span></span>|<span data-ttu-id="95e26-158">디렉터리/파일</span><span class="sxs-lookup"><span data-stu-id="95e26-158">Directory/file</span></span>|<span data-ttu-id="95e26-159">디렉터리/파일</span><span class="sxs-lookup"><span data-stu-id="95e26-159">Directory/file</span></span>|<span data-ttu-id="95e26-160">정의</span><span class="sxs-lookup"><span data-stu-id="95e26-160">Definition</span></span>|<span data-ttu-id="95e26-161">설명</span><span class="sxs-lookup"><span data-stu-id="95e26-161">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="95e26-162">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="95e26-162">C6A101DDCB470506</span></span>| | |<span data-ttu-id="95e26-163">런타임 버전의 해시 문자열</span><span class="sxs-lookup"><span data-stu-id="95e26-163">Hash string of runtime version</span></span>|<span data-ttu-id="95e26-164">로컬 실행에 필요한 런타임 파일의 섀도 복사본</span><span class="sxs-lookup"><span data-stu-id="95e26-164">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="95e26-165">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="95e26-165">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="95e26-166">스크립트 이름 + 스크립트 경로의 해시 문자열</span><span class="sxs-lookup"><span data-stu-id="95e26-166">Script name + hash string of script path</span></span>|<span data-ttu-id="95e26-167">컴파일 출력 및 실행 단계 로깅</span><span class="sxs-lookup"><span data-stu-id="95e26-167">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="95e26-168">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="95e26-168">\_script\_.abr</span></span>|<span data-ttu-id="95e26-169">컴파일러 출력</span><span class="sxs-lookup"><span data-stu-id="95e26-169">Compiler output</span></span>|<span data-ttu-id="95e26-170">대수 파일</span><span class="sxs-lookup"><span data-stu-id="95e26-170">Algebra file</span></span>|
| | |<span data-ttu-id="95e26-171">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="95e26-171">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="95e26-172">컴파일러 출력</span><span class="sxs-lookup"><span data-stu-id="95e26-172">Compiler output</span></span>|<span data-ttu-id="95e26-173">생성된 관리 코드</span><span class="sxs-lookup"><span data-stu-id="95e26-173">Generated managed code</span></span>|
| | |<span data-ttu-id="95e26-174">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="95e26-174">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="95e26-175">컴파일러 출력</span><span class="sxs-lookup"><span data-stu-id="95e26-175">Compiler output</span></span>|<span data-ttu-id="95e26-176">생성된 네이티브 코드</span><span class="sxs-lookup"><span data-stu-id="95e26-176">Generated native code</span></span>|
| | |<span data-ttu-id="95e26-177">참조된 어셈블리</span><span class="sxs-lookup"><span data-stu-id="95e26-177">referenced assemblies</span></span>|<span data-ttu-id="95e26-178">어셈블리 참조</span><span class="sxs-lookup"><span data-stu-id="95e26-178">Assembly reference</span></span>|<span data-ttu-id="95e26-179">참조된 어셈블리 파일</span><span class="sxs-lookup"><span data-stu-id="95e26-179">Referenced assembly files</span></span>|
| | |<span data-ttu-id="95e26-180">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="95e26-180">deployed_resources</span></span>|<span data-ttu-id="95e26-181">리소스 배포</span><span class="sxs-lookup"><span data-stu-id="95e26-181">Resource deployment</span></span>|<span data-ttu-id="95e26-182">리소스 배포 파일</span><span class="sxs-lookup"><span data-stu-id="95e26-182">Resource deployment files</span></span>|
| | |<span data-ttu-id="95e26-183">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="95e26-183">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="95e26-184">실행 로그</span><span class="sxs-lookup"><span data-stu-id="95e26-184">Execution log</span></span>|<span data-ttu-id="95e26-185">실행 단계에 대한 로그</span><span class="sxs-lookup"><span data-stu-id="95e26-185">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="95e26-186">명령줄에서 SDK 사용</span><span class="sxs-lookup"><span data-stu-id="95e26-186">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="95e26-187">도우미 응용 프로그램의 명령줄 인터페이스</span><span class="sxs-lookup"><span data-stu-id="95e26-187">Command-line interface of the helper application</span></span>

<span data-ttu-id="95e26-188">SDK directory\build\runtime에서 LocalRunHelper.exe는 일반적으로 사용되는 대부분의 로컬 실행 기능에 대한 인터페이스를 제공하는 명령줄 도우미 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-188">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="95e26-189">명령 및 인수 스위치는 모두 대소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-189">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="95e26-190">도우미를 호출하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-190">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="95e26-191">인수를 사용하지 않거나 다음과 같이 **help** 스위치와 함께 LocalRunHelper.exe를 실행하여 도움말 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-191">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="95e26-192">도움말 정보에서 다음과 같이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-192">In the help information:</span></span>

-  <span data-ttu-id="95e26-193">**Command**: 명령의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-193">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="95e26-194">**Required Argument**: 제공해야 하는 인수를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-194">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="95e26-195">**Optional Argument**: 선택적이며 기본값을 갖는 인수를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-195">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="95e26-196">선택적 부울 인수에는 매개 변수가 없으며, 이 매개 변수의 출현은 기본값에 부정적이라는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-196">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="95e26-197">반환 값 및 로깅</span><span class="sxs-lookup"><span data-stu-id="95e26-197">Return value and logging</span></span>

<span data-ttu-id="95e26-198">도우미 응용 프로그램은 성공한 경우 **0**을, 실패한 경우 **-1**을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-198">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="95e26-199">기본적으로 도우미는 모든 메시지를 현재 콘솔로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-199">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="95e26-200">그러나 대부분의 명령은 출력을 로그 파일로 리디렉션하는 **-MessageOut path_to_log_file** 선택적 인수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-200">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="95e26-201">환경 변수 구성</span><span class="sxs-lookup"><span data-stu-id="95e26-201">Environment variable configuring</span></span>

<span data-ttu-id="95e26-202">U-SQL 로컬 실행을 위해서는 지정된 데이터 루트가 로컬 저장소 계정으로 필요하고, 종속성에 대해 지정된 CppSDK 경로가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-202">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="95e26-203">명령줄에서 인수를 설정하고 그에 대한 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-203">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="95e26-204">**SCOPE_CPP_SDK** 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-204">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="95e26-205">Data Lake Tools for Visual Studio를 설치하여 Microsoft Visual C++ 및 Windows SDK를 가져온 경우 다음 폴더가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-205">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="95e26-206">이 디렉터리를 가리키도록 **SCOPE_CPP_SDK**라는 새로운 환경 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-206">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="95e26-207">또는 다른 위치에 폴더를 복사하고 **SCOPE_CPP_SDK**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-207">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="95e26-208">환경 변수를 설정하는 것 외에도 명령줄을 사용할 때 **-CppSDK** 인수를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-208">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="95e26-209">이 인수는 기본 CppSDK 환경 변수를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-209">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="95e26-210">**LOCALRUN_DATAROOT** 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-210">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="95e26-211">데이터 루트를 가리키는 **LOCALRUN_DATAROOT**라는 새로운 환경 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-211">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="95e26-212">환경 변수를 설정하는 것 외에도 명령줄을 사용할 때 데이터 루트 경로로 **-DataRoot** 인수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-212">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="95e26-213">이 인수는 기본 데이터 루트 환경 변수를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-213">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="95e26-214">모든 작업에 대해 기본 데이터 루트 환경 변수를 덮어 쓸 수 있도록 실행 중인 모든 명령줄에 이 인수를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-214">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="95e26-215">SDK 명령줄 사용 샘플</span><span class="sxs-lookup"><span data-stu-id="95e26-215">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="95e26-216">컴파일 및 실행</span><span class="sxs-lookup"><span data-stu-id="95e26-216">Compile and run</span></span>

<span data-ttu-id="95e26-217">**run** 명령은 스크립트를 컴파일한 다음 컴파일 결과를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-217">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="95e26-218">명령줄 인수는 **compile**과 **execute**의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-218">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="95e26-219">다음은 **run**에 대한 선택적 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-219">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="95e26-220">인수</span><span class="sxs-lookup"><span data-stu-id="95e26-220">Argument</span></span>|<span data-ttu-id="95e26-221">기본값</span><span class="sxs-lookup"><span data-stu-id="95e26-221">Default value</span></span>|<span data-ttu-id="95e26-222">설명</span><span class="sxs-lookup"><span data-stu-id="95e26-222">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="95e26-223">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="95e26-223">-CodeBehind</span></span>|<span data-ttu-id="95e26-224">False</span><span class="sxs-lookup"><span data-stu-id="95e26-224">False</span></span>|<span data-ttu-id="95e26-225">스크립트에는 .cs 코드 숨김이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-225">The script has .cs code behind</span></span>|
|<span data-ttu-id="95e26-226">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="95e26-226">-CppSDK</span></span>| |<span data-ttu-id="95e26-227">CppSDK 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-227">CppSDK Directory</span></span>|
|<span data-ttu-id="95e26-228">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="95e26-228">-DataRoot</span></span>| <span data-ttu-id="95e26-229">DataRoot 환경 변수</span><span class="sxs-lookup"><span data-stu-id="95e26-229">DataRoot environment variable</span></span>|<span data-ttu-id="95e26-230">로컬 실행을 위한 데이터 루트이며, 기본값은 'LOCALRUN_DATAROOT' 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-230">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="95e26-231">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="95e26-231">-MessageOut</span></span>| |<span data-ttu-id="95e26-232">콘솔의 메시지를 파일에 덤프합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-232">Dump messages on console to a file</span></span>|
|<span data-ttu-id="95e26-233">-Parallel</span><span class="sxs-lookup"><span data-stu-id="95e26-233">-Parallel</span></span>|<span data-ttu-id="95e26-234">1</span><span class="sxs-lookup"><span data-stu-id="95e26-234">1</span></span>|<span data-ttu-id="95e26-235">지정된 병렬 처리로 계획을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-235">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="95e26-236">-References</span><span class="sxs-lookup"><span data-stu-id="95e26-236">-References</span></span>| |<span data-ttu-id="95e26-237">';'(세미콜론)으로 구분된 코드 참조의 추가 참조 어셈블리 또는 데이터 파일의 경로 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-237">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="95e26-238">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="95e26-238">-UdoRedirect</span></span>|<span data-ttu-id="95e26-239">False</span><span class="sxs-lookup"><span data-stu-id="95e26-239">False</span></span>|<span data-ttu-id="95e26-240">Udo 어셈블리 리디렉션 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-240">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="95e26-241">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="95e26-241">-UseDatabase</span></span>|<span data-ttu-id="95e26-242">master</span><span class="sxs-lookup"><span data-stu-id="95e26-242">master</span></span>|<span data-ttu-id="95e26-243">코드 숨김 임시 어셈블리 등록에 사용할 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-243">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="95e26-244">-Verbose</span><span class="sxs-lookup"><span data-stu-id="95e26-244">-Verbose</span></span>|<span data-ttu-id="95e26-245">False</span><span class="sxs-lookup"><span data-stu-id="95e26-245">False</span></span>|<span data-ttu-id="95e26-246">런타임의 자세한 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-246">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="95e26-247">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="95e26-247">-WorkDir</span></span>|<span data-ttu-id="95e26-248">현재 디렉터리</span><span class="sxs-lookup"><span data-stu-id="95e26-248">Current Directory</span></span>|<span data-ttu-id="95e26-249">컴파일러 사용 및 출력을 위한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-249">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="95e26-250">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="95e26-250">-RunScopeCEP</span></span>|<span data-ttu-id="95e26-251">0</span><span class="sxs-lookup"><span data-stu-id="95e26-251">0</span></span>|<span data-ttu-id="95e26-252">사용할 ScopeCEP 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-252">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="95e26-253">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="95e26-253">-ScopeCEPTempPath</span></span>|<span data-ttu-id="95e26-254">temp</span><span class="sxs-lookup"><span data-stu-id="95e26-254">temp</span></span>|<span data-ttu-id="95e26-255">데이터 스트리밍에 사용할 임시 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-255">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="95e26-256">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="95e26-256">-OptFlags</span></span>| |<span data-ttu-id="95e26-257">쉼표로 구분된 최적화 프로그램 플래그 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-257">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="95e26-258">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-258">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="95e26-259">**compile**과 **execute**를 조합하는 것 외에도 컴파일된 실행 파일을 개별적으로 컴파일하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-259">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="95e26-260">U-SQL 스크립트 컴파일</span><span class="sxs-lookup"><span data-stu-id="95e26-260">Compile a U-SQL script</span></span>

<span data-ttu-id="95e26-261">**compile** 명령은 U-SQL 스크립트를 실행 파일로 컴파일하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-261">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="95e26-262">다음은 **compile**에 대한 선택적 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-262">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="95e26-263">인수</span><span class="sxs-lookup"><span data-stu-id="95e26-263">Argument</span></span>|<span data-ttu-id="95e26-264">설명</span><span class="sxs-lookup"><span data-stu-id="95e26-264">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="95e26-265">-CodeBehind [기본값 'False']</span><span class="sxs-lookup"><span data-stu-id="95e26-265">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="95e26-266">스크립트에는 .cs 코드 숨김이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-266">The script has .cs code behind</span></span>|
| <span data-ttu-id="95e26-267">-CppSDK [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="95e26-267">-CppSDK [default value '']</span></span>|<span data-ttu-id="95e26-268">CppSDK 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-268">CppSDK Directory</span></span>|
| <span data-ttu-id="95e26-269">-DataRoot [기본값 'DataRoot 환경 변수']</span><span class="sxs-lookup"><span data-stu-id="95e26-269">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="95e26-270">로컬 실행을 위한 데이터 루트이며, 기본값은 'LOCALRUN_DATAROOT' 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-270">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="95e26-271">-MessageOut [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="95e26-271">-MessageOut [default value '']</span></span>|<span data-ttu-id="95e26-272">콘솔의 메시지를 파일에 덤프합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-272">Dump messages on console to a file</span></span>|
| <span data-ttu-id="95e26-273">-References [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="95e26-273">-References [default value '']</span></span>|<span data-ttu-id="95e26-274">';'(세미콜론)으로 구분된 코드 참조의 추가 참조 어셈블리 또는 데이터 파일의 경로 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-274">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="95e26-275">-Shallow [기본값 'False']</span><span class="sxs-lookup"><span data-stu-id="95e26-275">-Shallow [default value 'False']</span></span>|<span data-ttu-id="95e26-276">단순 컴파일입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-276">Shallow compile</span></span>|
| <span data-ttu-id="95e26-277">-UdoRedirect [기본값 'False']</span><span class="sxs-lookup"><span data-stu-id="95e26-277">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="95e26-278">Udo 어셈블리 리디렉션 구성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-278">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="95e26-279">-UseDatabase [기본값 'master']</span><span class="sxs-lookup"><span data-stu-id="95e26-279">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="95e26-280">코드 숨김 임시 어셈블리 등록에 사용할 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-280">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="95e26-281">-WorkDir [기본값 '현재 디렉터리']</span><span class="sxs-lookup"><span data-stu-id="95e26-281">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="95e26-282">컴파일러 사용 및 출력을 위한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-282">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="95e26-283">-RunScopeCEP [기본값 '0']</span><span class="sxs-lookup"><span data-stu-id="95e26-283">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="95e26-284">사용할 ScopeCEP 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-284">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="95e26-285">-ScopeCEPTempPath [기본값 'temp']</span><span class="sxs-lookup"><span data-stu-id="95e26-285">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="95e26-286">데이터 스트리밍에 사용할 임시 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-286">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="95e26-287">-OptFlags [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="95e26-287">-OptFlags [default value '']</span></span>|<span data-ttu-id="95e26-288">쉼표로 구분된 최적화 프로그램 플래그 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-288">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="95e26-289">몇 가지 사용 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-289">Here are some usage examples.</span></span>

<span data-ttu-id="95e26-290">U-SQL 스크립트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-290">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="95e26-291">U-SQL 스크립트를 컴파일하고 데이터 루트 폴더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-291">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="95e26-292">이는 환경 변수 설정을 덮어 씁니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-292">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="95e26-293">U-SQL 스크립트를 컴파일하고 작업 디렉터리, 참조 어셈블리 및 데이터베이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-293">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="95e26-294">컴파일된 결과 실행</span><span class="sxs-lookup"><span data-stu-id="95e26-294">Execute compiled results</span></span>

<span data-ttu-id="95e26-295">**execute** 명령은 컴파일된 결과를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-295">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="95e26-296">다음은 **compile**에 대한 선택적 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-296">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="95e26-297">인수</span><span class="sxs-lookup"><span data-stu-id="95e26-297">Argument</span></span>|<span data-ttu-id="95e26-298">설명</span><span class="sxs-lookup"><span data-stu-id="95e26-298">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="95e26-299">-DataRoot [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="95e26-299">-DataRoot [default value '']</span></span>|<span data-ttu-id="95e26-300">메타데이터 실행을 위한 루트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-300">Data root for metadata execution.</span></span> <span data-ttu-id="95e26-301">**LOCALRUN_DATAROOT** 환경 변수로 기본 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-301">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="95e26-302">-MessageOut [기본값 '']</span><span class="sxs-lookup"><span data-stu-id="95e26-302">-MessageOut [default value '']</span></span>|<span data-ttu-id="95e26-303">콘솔의 메시지를 파일에 덤프합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-303">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="95e26-304">-Parallel [기본값 '1']</span><span class="sxs-lookup"><span data-stu-id="95e26-304">-Parallel [default value '1']</span></span>|<span data-ttu-id="95e26-305">지정된 병렬 처리 수준으로 생성된 로컬 실행 단계를 실행하는 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-305">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="95e26-306">-Verbose [기본값 'False']</span><span class="sxs-lookup"><span data-stu-id="95e26-306">-Verbose [default value 'False']</span></span>|<span data-ttu-id="95e26-307">런타임의 자세한 출력을 보여주는 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-307">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="95e26-308">사용 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-308">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="95e26-309">프로그래밍 인터페이스와 함께 SDK 사용</span><span class="sxs-lookup"><span data-stu-id="95e26-309">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="95e26-310">프로그래밍 인터페이스는 모두 LocalRunHelper.exe에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-310">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="95e26-311">이 인터페이스를 사용하여 U-SQL SDK 및 C# 테스트 프레임워크의 기능을 통합하여 U-SQL 스크립트 로컬 테스트의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-311">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="95e26-312">이 문서에서는 이러한 인터페이스를 사용하여 U-SQL 스크립트를 테스트하는 방법을 보여 주기 위해 표준 C# 단위 테스트 프로젝트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-312">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="95e26-313">1단계: C# 단위 테스트 프로젝트 및 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="95e26-313">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="95e26-314">파일 > 새로 만들기 > 프로젝트 > Visual C# > 테스트 > 단위 테스트 프로젝트를 통해 C# 단위 테스트 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-314">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="95e26-315">프로젝트에 대한 참조로 LocalRunHelper.exe를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-315">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="95e26-316">LocalRunHelper.exe는 Nuget 패키지의 \build\runtime\LocalRunHelper.exe에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-316">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Azure Data Lake U-SQL SDK 참조 추가](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="95e26-318">U-SQL SDK는 x64 환경**만** 지원합니다. 따라서 빌드 플랫폼 대상을 x64로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-318">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="95e26-319">프로젝트 속성 > 빌드 > 플랫폼 대상을 통해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-319">You can set that through Project Property > Build > Platform target.</span></span>

    ![Azure Data Lake U-SQL SDK x64 프로젝트 구성](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="95e26-321">테스트 환경을 x64로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-321">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="95e26-322">Visual Studio에서 테스트 > 테스트 설정 > 기본 프로세서 아키텍처 > x64를 통해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-322">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Azure Data Lake U-SQL SDK x64 테스트 환경 구성](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="95e26-324">NugetPackage\build\runtime\ 아래에 있는 모든 종속성 파일을 일반적으로 ProjectFolder\bin\x64\Debug 아래에 있는 프로젝트 작업 디렉터리로 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-324">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="95e26-325">2단계: U-SQL 스크립트 테스트 사례 만들기</span><span class="sxs-lookup"><span data-stu-id="95e26-325">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="95e26-326">다음은 U-SQL 스크립트 테스트에 대한 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-326">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="95e26-327">테스트를 위해 스크립트, 입력 파일 및 예상 출력 파일을 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-327">For testing, you need to prepare scripts, input files and expected output files.</span></span>

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
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
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

                //Don't forget to close MessageOutput to get logs into file
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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="95e26-328">LocalRunHelper.exe의 프로그래밍 인터페이스</span><span class="sxs-lookup"><span data-stu-id="95e26-328">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="95e26-329">LocalRunHelper.exe는 U-SQL 로컬 컴파일, 실행 등을 위한 프로그래밍 인터페이스를 제공합니다. 이러한 인터페이스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-329">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="95e26-330">**생성자**</span><span class="sxs-lookup"><span data-stu-id="95e26-330">**Constructor**</span></span>

<span data-ttu-id="95e26-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="95e26-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="95e26-332">매개 변수</span><span class="sxs-lookup"><span data-stu-id="95e26-332">Parameter</span></span>|<span data-ttu-id="95e26-333">형식</span><span class="sxs-lookup"><span data-stu-id="95e26-333">Type</span></span>|<span data-ttu-id="95e26-334">설명</span><span class="sxs-lookup"><span data-stu-id="95e26-334">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="95e26-335">messageOutput</span><span class="sxs-lookup"><span data-stu-id="95e26-335">messageOutput</span></span>|<span data-ttu-id="95e26-336">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="95e26-336">System.IO.TextWriter</span></span>|<span data-ttu-id="95e26-337">출력 메시지의 경우 콘솔을 사용하도록 null로 설정</span><span class="sxs-lookup"><span data-stu-id="95e26-337">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="95e26-338">**속성**</span><span class="sxs-lookup"><span data-stu-id="95e26-338">**Properties**</span></span>

|<span data-ttu-id="95e26-339">속성</span><span class="sxs-lookup"><span data-stu-id="95e26-339">Property</span></span>|<span data-ttu-id="95e26-340">형식</span><span class="sxs-lookup"><span data-stu-id="95e26-340">Type</span></span>|<span data-ttu-id="95e26-341">설명</span><span class="sxs-lookup"><span data-stu-id="95e26-341">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="95e26-342">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="95e26-342">AlgebraPath</span></span>|<span data-ttu-id="95e26-343">string</span><span class="sxs-lookup"><span data-stu-id="95e26-343">string</span></span>|<span data-ttu-id="95e26-344">대수 파일의 경로입니다(대수 파일은 컴파일 결과 중 하나임).</span><span class="sxs-lookup"><span data-stu-id="95e26-344">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="95e26-345">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="95e26-345">CodeBehindReferences</span></span>|<span data-ttu-id="95e26-346">string</span><span class="sxs-lookup"><span data-stu-id="95e26-346">string</span></span>|<span data-ttu-id="95e26-347">스크립트에 추가 코드 숨김 참조가 있으면 경로를 ';'으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-347">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="95e26-348">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="95e26-348">CppSdkDir</span></span>|<span data-ttu-id="95e26-349">string</span><span class="sxs-lookup"><span data-stu-id="95e26-349">string</span></span>|<span data-ttu-id="95e26-350">CppSDK 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-350">CppSDK directory</span></span>|
|<span data-ttu-id="95e26-351">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="95e26-351">CurrentDir</span></span>|<span data-ttu-id="95e26-352">string</span><span class="sxs-lookup"><span data-stu-id="95e26-352">string</span></span>|<span data-ttu-id="95e26-353">현재 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-353">Current directory</span></span>|
|<span data-ttu-id="95e26-354">DataRoot</span><span class="sxs-lookup"><span data-stu-id="95e26-354">DataRoot</span></span>|<span data-ttu-id="95e26-355">string</span><span class="sxs-lookup"><span data-stu-id="95e26-355">string</span></span>|<span data-ttu-id="95e26-356">데이터 루트 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-356">Data root path</span></span>|
|<span data-ttu-id="95e26-357">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="95e26-357">DebuggerMailPath</span></span>|<span data-ttu-id="95e26-358">string</span><span class="sxs-lookup"><span data-stu-id="95e26-358">string</span></span>|<span data-ttu-id="95e26-359">디버거 메일 슬롯에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-359">The path to debugger mailslot</span></span>|
|<span data-ttu-id="95e26-360">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="95e26-360">GenerateUdoRedirect</span></span>|<span data-ttu-id="95e26-361">bool</span><span class="sxs-lookup"><span data-stu-id="95e26-361">bool</span></span>|<span data-ttu-id="95e26-362">어셈블리 로딩 리디렉션 오버라이드 구성을 생성하려는 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-362">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="95e26-363">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="95e26-363">HasCodeBehind</span></span>|<span data-ttu-id="95e26-364">bool</span><span class="sxs-lookup"><span data-stu-id="95e26-364">bool</span></span>|<span data-ttu-id="95e26-365">스크립트에는 코드 숨김이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-365">If the script has code behind</span></span>|
|<span data-ttu-id="95e26-366">InputDir</span><span class="sxs-lookup"><span data-stu-id="95e26-366">InputDir</span></span>|<span data-ttu-id="95e26-367">string</span><span class="sxs-lookup"><span data-stu-id="95e26-367">string</span></span>|<span data-ttu-id="95e26-368">입력 데이터에 대한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-368">Directory for input data</span></span>|
|<span data-ttu-id="95e26-369">MessagePath</span><span class="sxs-lookup"><span data-stu-id="95e26-369">MessagePath</span></span>|<span data-ttu-id="95e26-370">string</span><span class="sxs-lookup"><span data-stu-id="95e26-370">string</span></span>|<span data-ttu-id="95e26-371">메시지 덤프 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-371">Message dump file path</span></span>|
|<span data-ttu-id="95e26-372">OutputDir</span><span class="sxs-lookup"><span data-stu-id="95e26-372">OutputDir</span></span>|<span data-ttu-id="95e26-373">string</span><span class="sxs-lookup"><span data-stu-id="95e26-373">string</span></span>|<span data-ttu-id="95e26-374">출력 데이터에 대한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-374">Directory for output data</span></span>|
|<span data-ttu-id="95e26-375">병렬 처리</span><span class="sxs-lookup"><span data-stu-id="95e26-375">Parallelism</span></span>|<span data-ttu-id="95e26-376">int</span><span class="sxs-lookup"><span data-stu-id="95e26-376">int</span></span>|<span data-ttu-id="95e26-377">대수 실행을 위한 병렬 처리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-377">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="95e26-378">ParentPid</span><span class="sxs-lookup"><span data-stu-id="95e26-378">ParentPid</span></span>|<span data-ttu-id="95e26-379">int</span><span class="sxs-lookup"><span data-stu-id="95e26-379">int</span></span>|<span data-ttu-id="95e26-380">종료할 서비스 모니터에 대한 상위 모니터 PID입니다. 무시하려면 0 또는 음수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-380">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="95e26-381">ResultPath</span><span class="sxs-lookup"><span data-stu-id="95e26-381">ResultPath</span></span>|<span data-ttu-id="95e26-382">string</span><span class="sxs-lookup"><span data-stu-id="95e26-382">string</span></span>|<span data-ttu-id="95e26-383">결과 덤프 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-383">Result dump file path</span></span>|
|<span data-ttu-id="95e26-384">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="95e26-384">RuntimeDir</span></span>|<span data-ttu-id="95e26-385">string</span><span class="sxs-lookup"><span data-stu-id="95e26-385">string</span></span>|<span data-ttu-id="95e26-386">런타임 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-386">Runtime directory</span></span>|
|<span data-ttu-id="95e26-387">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="95e26-387">ScriptPath</span></span>|<span data-ttu-id="95e26-388">string</span><span class="sxs-lookup"><span data-stu-id="95e26-388">string</span></span>|<span data-ttu-id="95e26-389">스크립트를 찾을 수 있는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-389">Where to find the script</span></span>|
|<span data-ttu-id="95e26-390">Shallow</span><span class="sxs-lookup"><span data-stu-id="95e26-390">Shallow</span></span>|<span data-ttu-id="95e26-391">bool</span><span class="sxs-lookup"><span data-stu-id="95e26-391">bool</span></span>|<span data-ttu-id="95e26-392">단순 컴파일이거나 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-392">Shallow compile or not</span></span>|
|<span data-ttu-id="95e26-393">TempDir</span><span class="sxs-lookup"><span data-stu-id="95e26-393">TempDir</span></span>|<span data-ttu-id="95e26-394">string</span><span class="sxs-lookup"><span data-stu-id="95e26-394">string</span></span>|<span data-ttu-id="95e26-395">임시 디렉터리</span><span class="sxs-lookup"><span data-stu-id="95e26-395">Temp directory</span></span>|
|<span data-ttu-id="95e26-396">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="95e26-396">UseDataBase</span></span>|<span data-ttu-id="95e26-397">string</span><span class="sxs-lookup"><span data-stu-id="95e26-397">string</span></span>|<span data-ttu-id="95e26-398">코드 숨김 임시 어셈블리 등록에 사용할 데이터베이스를 지정합니다. 기본값은 master입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-398">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="95e26-399">WorkDir</span><span class="sxs-lookup"><span data-stu-id="95e26-399">WorkDir</span></span>|<span data-ttu-id="95e26-400">string</span><span class="sxs-lookup"><span data-stu-id="95e26-400">string</span></span>|<span data-ttu-id="95e26-401">기본 설정 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-401">Preferred working directory</span></span>|


<span data-ttu-id="95e26-402">**메서드**</span><span class="sxs-lookup"><span data-stu-id="95e26-402">**Method**</span></span>

|<span data-ttu-id="95e26-403">메서드</span><span class="sxs-lookup"><span data-stu-id="95e26-403">Method</span></span>|<span data-ttu-id="95e26-404">설명</span><span class="sxs-lookup"><span data-stu-id="95e26-404">Description</span></span>|<span data-ttu-id="95e26-405">Return</span><span class="sxs-lookup"><span data-stu-id="95e26-405">Return</span></span>|<span data-ttu-id="95e26-406">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-406">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="95e26-407">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="95e26-407">public bool DoCompile()</span></span>|<span data-ttu-id="95e26-408">U-SQL 스크립트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-408">Compile the U-SQL script</span></span>|<span data-ttu-id="95e26-409">성공 시 True입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-409">True on success</span></span>| |
|<span data-ttu-id="95e26-410">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="95e26-410">public bool DoExec()</span></span>|<span data-ttu-id="95e26-411">컴파일된 결과를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-411">Execute the compiled result</span></span>|<span data-ttu-id="95e26-412">성공 시 True입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-412">True on success</span></span>| |
|<span data-ttu-id="95e26-413">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="95e26-413">public bool DoRun()</span></span>|<span data-ttu-id="95e26-414">U-SQL 스크립트(Compile + Execute)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-414">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="95e26-415">성공 시 True입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-415">True on success</span></span>| |
|<span data-ttu-id="95e26-416">public bool IsValidRuntimeDir(문자열 경로)</span><span class="sxs-lookup"><span data-stu-id="95e26-416">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="95e26-417">지정된 경로가 유효한 런타임 경로인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-417">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="95e26-418">유효한 경우 True입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-418">True for valid</span></span>|<span data-ttu-id="95e26-419">런타임 디렉터리의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-419">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="95e26-420">일반적인 문제에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="95e26-420">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="95e26-421">오류 1:</span><span class="sxs-lookup"><span data-stu-id="95e26-421">Error 1:</span></span>
<span data-ttu-id="95e26-422">E_CSC_SYSTEM_INTERNAL: 내부 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="95e26-423">파일 또는 어셈블리 'ScopeEngineManaged.dll'이나 해당 종속성 중 하나를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="95e26-424">지정된 모듈을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-424">The specified module could not be found.</span></span>

<span data-ttu-id="95e26-425">다음 항목을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="95e26-425">Please check the following:</span></span>

- <span data-ttu-id="95e26-426">X64 환경인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-426">Make sure you have x64 environment.</span></span> <span data-ttu-id="95e26-427">빌드 대상 플랫폼 및 테스트 환경은 x64여야 합니다. 위의 **1단계: C# 단위 테스트 프로젝트 및 구성 만들기**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e26-427">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="95e26-428">NugetPackage\build\runtime\ 아래의 모든 종속 파일을 프로젝트 작업 디렉터리로 복사했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95e26-428">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="95e26-429">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95e26-429">Next steps</span></span>

* <span data-ttu-id="95e26-430">U-SQL을 알아보려면 [Azure Data Lake Analytics U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e26-430">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="95e26-431">진단 정보를 기록하려면 [Azure Data Lake Analytics에 대한 진단 로그에 액세스](data-lake-analytics-diagnostic-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e26-431">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="95e26-432">더 복잡한 쿼리를 보려면 [Azure Data Lake Analytics을 사용하여 웹 사이트 로그 분석](data-lake-analytics-analyze-weblogs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e26-432">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="95e26-433">작업 세부 정보를 보려면, [Azure Data lake Analytics 작업에 대한 작업 브라우저 및 작업 보기 사용하기](data-lake-analytics-data-lake-tools-view-jobs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e26-433">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="95e26-434">꼭짓점 실행 보기를 사용하려면 [Data Lake Tools for Visual Studio에서 Vertex Execution View 사용](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95e26-434">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
