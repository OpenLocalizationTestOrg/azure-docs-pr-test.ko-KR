---
title: "Hive 및 Pig에서 Azure HDInsight에서 Hadoop aaaUse C# | Microsoft Docs"
description: "자세한 방법을 toouse C# 사용자 정의 함수 (UDF) Hive 및 Pig Azure HDInsight 스트리밍."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="af568-103">HDInsight에서 Hive 및 Pig 스트림과 함께 C# UDF(사용자 정의 함수) 사용</span><span class="sxs-lookup"><span data-stu-id="af568-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="af568-104">Toouse C# 사용자 HDInsight의 Apache Hive 및 Pig 함수 (UDF)을 정의 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="af568-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af568-105">이 문서의 단계 hello Windows 기반와 Linux 기반 HDInsight 클러스터와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="af568-106">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="af568-107">자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af568-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="af568-108">둘 다 Hive 및 Pig 처리를 위해 데이터 tooexternal 응용 프로그램에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af568-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="af568-109">이 프로세스를 _스트리밍_이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-109">This process is known as _streaming_.</span></span> <span data-ttu-id="af568-110">.NET 응용 프로그램을 사용 하 여 hello 데이터가 전달 됩니다 toohello 응용 프로그램에서 STDIN을 하 고 hello 응용 프로그램 STDOUT에 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="af568-111">tooread STDIN 및 STDOUT에서 쓰기를 사용 하면 `Console.ReadLine()` 및 `Console.WriteLine()` 콘솔 응용 프로그램에서입니다.</span><span class="sxs-lookup"><span data-stu-id="af568-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af568-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="af568-112">Prerequisites</span></span>

* <span data-ttu-id="af568-113">.NET Framework 4.5를 대상으로 하는 C# 코드 작성 및 빌드에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="af568-114">원하는 IDE를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-114">Use whatever IDE you want.</span></span> <span data-ttu-id="af568-115">[Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 또는 [Visual Studio Code](https://code.visualstudio.com/)를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="af568-116">이 문서 사용 하 여 Visual Studio 2017의에서 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="af568-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="af568-117">방식으로 tooupload.exe 파일을 toohello 클러스터와 Pig 및 Hive 작업을 실행된 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="af568-118">Visual Studio, Azure PowerShell 및 Azure CLI hello 데이터 레이크 도구 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="af568-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="af568-119">hello이 문서의 단계 Visual Studio tooupload hello 파일에 대 한 hello 데이터 레이크 도구를 사용 하 고 hello 예제 하이브 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="af568-120">다른 방법으로 toorun 하이브 쿼리 및 Pig 작업에 대 한 내용은 hello 다음 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="af568-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="af568-121">HDInsight에서 Apache Hive 사용</span><span class="sxs-lookup"><span data-stu-id="af568-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="af568-122">HDInsight에서 Apache Pig 사용</span><span class="sxs-lookup"><span data-stu-id="af568-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="af568-123">HDInsight 클러스터의 Hadoop.</span><span class="sxs-lookup"><span data-stu-id="af568-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="af568-124">클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-provision-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af568-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="af568-125">HDInsight에서.NET</span><span class="sxs-lookup"><span data-stu-id="af568-125">.NET on HDInsight</span></span>

* <span data-ttu-id="af568-126">__Linux 기반 HDInsight__ 사용 하는 클러스터 [모노 (https://mono-project.com)](https://mono-project.com) toorun.NET 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="af568-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="af568-127">Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af568-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="af568-128">.NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af568-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="af568-129">toouse 모노의 특정 버전 참조 hello [설치 또는 업데이트 모노](hdinsight-hadoop-install-mono.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="af568-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="af568-130">__Windows 기반 HDInsight__ 클러스터 hello Microsoft.NET CLR toorun.NET 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="af568-131">Hello.NET framework 및 HDInsight 버전에 포함 된 모노의 hello 버전에 대 한 자세한 내용은 참조 하십시오. [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="af568-132">Hello C 만들기\# 프로젝트</span><span class="sxs-lookup"><span data-stu-id="af568-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="af568-133">Hive UDF</span><span class="sxs-lookup"><span data-stu-id="af568-133">Hive UDF</span></span>

1. <span data-ttu-id="af568-134">Visual Studio를 열고 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af568-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="af568-135">Hello 프로젝트 형식에 대 한 선택 **콘솔 응용 프로그램 (.NET Framework)**, 및 이름 hello에 대 한 새 프로젝트 **HiveCSharp**합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="af568-136">Linux 기반 HDInsight 클러스터를 사용하는 경우 __.NET Framework 4.5__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="af568-137">.NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af568-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="af568-138">Hello 내용 바꾸기 **Program.cs** hello 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-138">Replace hello contents of **Program.cs** with hello following:</span></span>

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. <span data-ttu-id="af568-139">Hello 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="af568-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="af568-140">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="af568-140">Pig UDF</span></span>

1. <span data-ttu-id="af568-141">Visual Studio를 열고 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af568-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="af568-142">Hello 프로젝트 형식에 대 한 선택 **콘솔 응용 프로그램**, 및 이름 hello에 대 한 새 프로젝트 **PigUDF**합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="af568-143">Hello hello 내용 바꾸기 **Program.cs** 코드 다음 hello로 파일:</span><span class="sxs-lookup"><span data-stu-id="af568-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="af568-144">Hello Pig에서 보낸 선과 다시 포맷으로 시작 하는 구문 분석 하는이 응용 프로그램 `java.lang.Exception`합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="af568-145">저장 **Program.cs**, 다음 hello 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="af568-146">Toostorage 업로드</span><span class="sxs-lookup"><span data-stu-id="af568-146">Upload toostorage</span></span>

1. <span data-ttu-id="af568-147">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="af568-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="af568-148">**Azure**를 확장한 다음 **HDInsight**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="af568-149">메시지가 표시되면 Azure 구독 자격 증명을 입력한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="af568-150">Hello HDInsight 클러스터를 toodeploy이 응용이 프로그램을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="af568-151">Hello 텍스트 있는 항목이 __(기본 저장소 계정)__ 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af568-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Hello 클러스터에 대 한 hello 저장소 계정을 보여 주는 서버 탐색기](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="af568-153">사용 중인 경우이 항목에서 확장할 수는 __Azure 저장소 계정__ hello 클러스터에 대 한 기본 저장소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="af568-154">hello 클러스터에 대 한 hello 기본 저장소에 tooview hello 파일 hello 항목을 확장 하 고 hello 두 번 클릭 __(기본 컨테이너)__합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="af568-155">사용 하는이 항목을 확장할 수 없으면, __Azure 데이터 레이크 저장소__ hello 클러스터에 대 한 기본 저장소 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="af568-156">hello 클러스터에 대 한 hello 기본 저장소에 tooview hello 파일 hello를 두 번 클릭 __(기본 저장소 계정)__ 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="af568-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="af568-157">tooupload hello.exe 파일을 사용 하 여 hello 메서드를 다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="af568-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="af568-158">사용 하는 경우는 __Azure 저장소 계정__hello 업로드 아이콘을 클릭 한 다음 toohello 찾아보기, **bin\debug** hello에 대 한 폴더 **HiveCSharp** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="af568-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="af568-159">마지막으로 hello 선택 **HiveCSharp.exe** 파일을 클릭 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![업로드 아이콘](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="af568-161">사용 하는 경우 __Azure 데이터 레이크 저장소__를 hello 파일 목록에서 빈 영역을 마우스 오른쪽 단추로 클릭 한 다음 선택 __업로드__합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="af568-162">마지막으로 hello 선택 **HiveCSharp.exe** 파일을 클릭 하 여 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="af568-163">한 번 hello __HiveCSharp.exe__ 업로드가 완료 되 면 hello에 대 한 반복 hello 업로드 프로세스 __PigUDF.exe__ 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="af568-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="af568-164">HIVE 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="af568-164">Run a Hive query</span></span>

1. <span data-ttu-id="af568-165">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="af568-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="af568-166">**Azure**를 확장한 다음 **HDInsight**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="af568-167">Hello를 배포 하는 마우스 오른쪽 단추로 클릭 hello 클러스터 **HiveCSharp** , 응용 프로그램을 다음 선택 **는 하이브 쿼리를 작성할**합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="af568-168">Hello 하이브 쿼리에 대 한 텍스트 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-168">Use hello following text for hello Hive query:</span></span>

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="af568-169">Hello를 주석 처리 제거 `add file` hello 유형의 클러스터에 대해 사용 되는 기본 저장소와 일치 하는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="af568-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="af568-170">이 쿼리는 hello 선택 `clientid`, `devicemake`, 및 `devicemodel` 에서 필드 `hivesampletable`, hello 필드 toohello HiveCSharp.exe 응용 프로그램을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="af568-171">hello 쿼리 hello 응용 프로그램 tooreturn 세 개의 필드가으로 저장 되는 예상 `clientid`, `phoneLabel`, 및 `phoneHash`합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="af568-172">hello 쿼리는 또한 toofind HiveCSharp.exe hello 기본 저장소 컨테이너의 hello 루트에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="af568-173">클릭 **전송** toosubmit hello 작업 toohello HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="af568-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="af568-174">hello **작업 요약 하이브** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="af568-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="af568-175">클릭 **새로 고침** 까지 요약 toorefresh hello **작업 상태** 쪽 변경**Completed**합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="af568-176">클릭 tooview hello 작업 출력 **작업 출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="af568-177">Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="af568-177">Run a Pig job</span></span>

1. <span data-ttu-id="af568-178">Hello 메서드 tooconnect tooyour HDInsight 클러스터를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="af568-179">__Linux 기반__ HDInsight 클러스터를 사용하는 경우 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="af568-180">예: `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="af568-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="af568-181">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af568-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="af568-182">사용 하는 경우는 __Windows 기반__ HDInsight 클러스터 [원격 데스크톱을 사용 하 여 연결 toohello 클러스터](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="af568-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="af568-183">다음 명령은 toostart hello Pig 명령 줄 하나 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="af568-184">Windows 기반 클러스터를 사용 하는 경우 명령 대신 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="af568-185">`grunt>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af568-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="af568-186">Hello toorun hello.NET Framework 응용 프로그램을 사용 하는 Pig 작업을 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="af568-187">hello `DEFINE` 문을의 별칭을 만들어 `streamer` hello pigudf.exe 응용 프로그램 및 `CACHE` hello 클러스터에 대 한 기본 저장소에서 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="af568-188">이상에서는 `streamer` hello와 함께 사용 되 `STREAM` 연산자 tooprocess hello 일련의 열으로 로그와 반환 hello 데이터에 포함 된 단일 행.</span><span class="sxs-lookup"><span data-stu-id="af568-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af568-189">스트리밍에 사용 되는 hello 응용 프로그램 이름 hello로 묶어야 \` (억음 악센트 기호) 때 문자 별칭이 지정 하 고 ' (작은따옴표)와 함께 사용할 경우 `SHIP\`합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="af568-190">Hello 마지막 줄을 입력 한 후 hello 작업을 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="af568-191">출력 유사한 toohello를 다음 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="af568-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af568-192">Next steps</span></span>

<span data-ttu-id="af568-193">이 문서에서는 배웠습니다 어떻게 toouse Hive 및 Pig HDInsight의에서.NET Framework 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="af568-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="af568-194">Hive 및 Pig, Python toouse 참조 toolearn 원하는 경우 [Hive 및 Pig HDInsight에서 Python 사용](hdinsight-python.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="af568-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="af568-195">다른 방법으로 toouse Pig 및 Hive, 및 MapReduce 사용에 대 한 toolearn hello 다음 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="af568-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="af568-196">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="af568-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="af568-197">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="af568-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="af568-198">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="af568-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
