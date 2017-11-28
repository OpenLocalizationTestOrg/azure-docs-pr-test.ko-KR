---
title: "HDInsight의 Hadoop에서 Hive 및 Pig와 함께 C# 사용 - Azure | Microsoft Docs"
description: "Azure HDInsight에서 Hive 및 Pig 스트림과 함께 C# UDF(사용자 정의 함수)를 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 58e7af47be71c3e0389e5fb4641e124eb648494e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="31cfb-103">HDInsight에서 Hive 및 Pig 스트림과 함께 C# UDF(사용자 정의 함수) 사용</span><span class="sxs-lookup"><span data-stu-id="31cfb-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="31cfb-104">HDInsight에서 Apache Hive 및 Pig와 함께 C# UDF(사용자 정의 함수)를 사용하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-104">Learn how to use C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31cfb-105">이 문서의 단계는 Linux 기반 및 Windows 기반 HDInsight 클러스터에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-105">The steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="31cfb-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="31cfb-107">자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="31cfb-108">Hive 및 Pig 모두 외부 응용 프로그램으로 데이터를 전달해 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-108">Both Hive and Pig can pass data to external applications for processing.</span></span> <span data-ttu-id="31cfb-109">이 프로세스를 _스트리밍_이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-109">This process is known as _streaming_.</span></span> <span data-ttu-id="31cfb-110">.NET 응용 프로그램을 사용하는 경우 데이터가 STDIN의 응용 프로그램으로 전달된 다음 응용 프로그램이 STDOUT에서 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-110">When using a .NET applciation, the data is passed to the application on STDIN, and the application returns the results on STDOUT.</span></span> <span data-ttu-id="31cfb-111">STDIN 및 STDOUT에서 읽거나 쓰려면 콘솔 응용 프로그램에서 `Console.ReadLine()` 및 `Console.WriteLine()`을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-111">To read and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31cfb-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31cfb-112">Prerequisites</span></span>

* <span data-ttu-id="31cfb-113">.NET Framework 4.5를 대상으로 하는 C# 코드 작성 및 빌드에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="31cfb-114">원하는 IDE를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-114">Use whatever IDE you want.</span></span> <span data-ttu-id="31cfb-115">[Visual Studio](https://www.visualstudio.com/vs) 2015, 2017 또는 [Visual Studio Code](https://code.visualstudio.com/)를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="31cfb-116">이 문서의 단계는 Visual Studio 2017을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-116">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="31cfb-117">.exe 파일을 클러스터로 업로드하고 Pig 및 Hive 작업을 실행하는 방법.</span><span class="sxs-lookup"><span data-stu-id="31cfb-117">A way to upload .exe files to the cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="31cfb-118">Data Lake Tools for Visual Studio, Azure PowerShell 및 Azure CLI를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-118">We recommend the Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="31cfb-119">이 문서의 단계는 Data Lake Tools for Visual Studio를 사용하여 파일을 업로드하고 예제 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-119">The steps in this document use the Data Lake Tools for Visual Studio to upload the files and run the example Hive query.</span></span>

    <span data-ttu-id="31cfb-120">Hive 쿼리 및 Pig 작업을 실행하는 다른 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-120">For information on other ways to run Hive queries and Pig jobs, see the following documents:</span></span>

    * [<span data-ttu-id="31cfb-121">HDInsight에서 Apache Hive 사용</span><span class="sxs-lookup"><span data-stu-id="31cfb-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="31cfb-122">HDInsight에서 Apache Pig 사용</span><span class="sxs-lookup"><span data-stu-id="31cfb-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="31cfb-123">HDInsight 클러스터의 Hadoop.</span><span class="sxs-lookup"><span data-stu-id="31cfb-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="31cfb-124">클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-provision-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="31cfb-125">HDInsight에서.NET</span><span class="sxs-lookup"><span data-stu-id="31cfb-125">.NET on HDInsight</span></span>

* <span data-ttu-id="31cfb-126">[Mono(https://mono-project.com)](https://mono-project.com)를 사용하여 .NET 응용 프로그램을 실행하는 __Linux 기반 HDInsight__ 클러스터.</span><span class="sxs-lookup"><span data-stu-id="31cfb-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="31cfb-127">Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="31cfb-128">.NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="31cfb-129">특정 버전의 Mono를 사용하려면 [Mono 설치 또는 업데이트](hdinsight-hadoop-install-mono.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-129">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="31cfb-130">__Windows 기반 HDInsight__ 클러스터는 Microsoft .NET CLR을 사용하여 .NET 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-130">__Windows-based HDInsight__ clusters use the Microsoft .NET CLR to run .NET applications.</span></span>

<span data-ttu-id="31cfb-131">.NET Framework 버전 및 HDInsight 버전과 함께 제공되는 Mono에 대한 자세한 내용은 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-131">For more information on the version of the .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-the-c-projects"></a><span data-ttu-id="31cfb-132">C\# 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="31cfb-132">Create the C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="31cfb-133">Hive UDF</span><span class="sxs-lookup"><span data-stu-id="31cfb-133">Hive UDF</span></span>

1. <span data-ttu-id="31cfb-134">Visual Studio를 열고 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="31cfb-135">프로젝트 형식의 경우, **콘솔 앱(.NET Framework)**을 선택하고 새 프로젝트의 이름을 **HiveCSharp**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-135">For the project type, select **Console App (.NET Framework)**, and name the new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="31cfb-136">Linux 기반 HDInsight 클러스터를 사용하는 경우 __.NET Framework 4.5__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="31cfb-137">.NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="31cfb-138">**Program.cs** 의 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-138">Replace the contents of **Program.cs** with the following:</span></span>

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
                    // Parse the string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data to stdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for the given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array to hex string
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

3. <span data-ttu-id="31cfb-139">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-139">Build the project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="31cfb-140">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="31cfb-140">Pig UDF</span></span>

1. <span data-ttu-id="31cfb-141">Visual Studio를 열고 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="31cfb-142">프로젝트 형식의 경우, **콘솔 응용 프로그램**을 선택하고 새 프로젝트의 이름을 **PigUDF**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-142">For the project type, select **Console Application**, and name the new project **PigUDF**.</span></span>

2. <span data-ttu-id="31cfb-143">**Program.cs** 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-143">Replace the contents of the **Program.cs** file with the following code:</span></span>

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
                        // Trim the error info off the beginning and add a note to the end of the line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split the fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="31cfb-144">이 응용 프로그램은 Pig에서 보낸 줄을 구문 분석하고 `java.lang.Exception`로 시작하는 줄의 형식을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-144">This application parses the lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="31cfb-145">**Program.cs**를 저장한 다음 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-145">Save **Program.cs**, and then build the project.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="31cfb-146">저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="31cfb-146">Upload to storage</span></span>

1. <span data-ttu-id="31cfb-147">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="31cfb-148">**Azure**를 확장한 다음 **HDInsight**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="31cfb-149">메시지가 표시되면 Azure 구독 자격 증명을 입력한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="31cfb-150">이 응용 프로그램을 배포하려는 HDInsight 클러스터를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-150">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="31cfb-151">텍스트가 포함된 항목__(기본 저장소 계정)__이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-151">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![클러스터에 대한 저장소 계정을 보여주는 서버 탐색기](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="31cfb-153">이 항목을 확장할 수 있는 경우 클러스터의 기본 저장소로 __Azure Storage 계정__을 사용하고 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="31cfb-154">클러스터의 기본 저장소에서 파일을 보려면 항목을 확장한 다음 __(기본 컨테이너)__를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-154">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="31cfb-155">이 항목을 확장할 수 없는 경우 클러스터의 기본 저장소로 __Azure Data Lake Store__를 사용하고 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="31cfb-156">클러스터의 기본 저장소에 있는 파일을 보려면 항목을 확장한 다음 __(기본 저장소 계정)__을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-156">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="31cfb-157">.exe 파일을 업로드하려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-157">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="31cfb-158">__Azure Storage 계정__을 사용하는 경우 업로드 아이콘을 클릭한 다음 **bin\debug** 폴더로 이동하여 **HiveCSharp** 프로젝트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-158">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **HiveCSharp** project.</span></span> <span data-ttu-id="31cfb-159">마지막으로 **HiveCSharp.exe** 파일을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-159">Finally, select the **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![업로드 아이콘](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="31cfb-161">__Azure Data Lake Store__를 사용하는 경우 마우스 오른쪽 버튼으로 파일 목록의 빈 영역을 클릭한 다음 __업로드__를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-161">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="31cfb-162">마지막으로 **HiveCSharp.exe** 파일을 선택하고 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-162">Finally, select the **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="31cfb-163">__HiveCSharp.exe__ 업로드가 완료되면 __PigUDF.exe__ 파일의 업로드 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-163">Once the __HiveCSharp.exe__ upload has finished, repeat the upload process for the __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="31cfb-164">HIVE 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="31cfb-164">Run a Hive query</span></span>

1. <span data-ttu-id="31cfb-165">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="31cfb-166">**Azure**를 확장한 다음 **HDInsight**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="31cfb-167">**HiveCSharp** 응용 프로그램을 배포한 클러스터를 마우스 오른쪽 단추로 클릭하고 **Hive 쿼리 작성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-167">Right-click the cluster that you deployed the **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="31cfb-168">Hive 쿼리로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-168">Use the following text for the Hive query:</span></span>

    ```hiveql
    -- Uncomment the following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment the following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="31cfb-169">클러스터에 사용되는 기본 저장소의 유형과 일치하는 `add file` 문에서 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-169">Uncomment the `add file` statement that matches the type of default storage used for your cluster.</span></span>

    <span data-ttu-id="31cfb-170">이 쿼리는 `hivesampletable`에서 `clientid`, `devicemake` 및 `devicemodel` 필드를 선택하고 해당 필드를 HiveCSharp.exe 응용 프로그램으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-170">This query selects the `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes the fields to the HiveCSharp.exe application.</span></span> <span data-ttu-id="31cfb-171">쿼리는 응용 프로그램이 3개의 필드를 반환할 것을 예상하며 `clientid`, `phoneLabel` 및 `phoneHash`로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-171">The query expects the application to return three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="31cfb-172">또한 쿼리는 기본 저장소 컨테이너의 루트에서 HiveCSharp.exe를 찾는다고 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-172">The query also expects to find HiveCSharp.exe in the root of the default storage container.</span></span>

5. <span data-ttu-id="31cfb-173">**제출** 을 클릭하여 HDInsight 클러스터에 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-173">Click **Submit** to submit the job to the HDInsight cluster.</span></span> <span data-ttu-id="31cfb-174">**Hive 작업 요약** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-174">The **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="31cfb-175">**새로 고침**을 클릭하여 **작업 상태**가 **Completed**로 변경될 때까지 요약을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-175">Click **Refresh** to refresh the summary until **Job Status** changes to **Completed**.</span></span> <span data-ttu-id="31cfb-176">작업 출력을 보려면 **작업 출력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-176">To view the job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="31cfb-177">Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="31cfb-177">Run a Pig job</span></span>

1. <span data-ttu-id="31cfb-178">다음 중 한 가지 방법을 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-178">Use one of the following methods to connect to your HDInsight cluster:</span></span>

    * <span data-ttu-id="31cfb-179">__Linux 기반__ HDInsight 클러스터를 사용하는 경우 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="31cfb-180">예: `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="31cfb-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="31cfb-181">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="31cfb-182">__Windows 기반__ HDInsight 클러스터를 사용하는 경우 [원격 데스크톱을 사용하여 클러스터에 연결](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-182">If you are using a __Windows-based__ HDInsight cluster, [Connect to the cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="31cfb-183">Pig 명령줄을 시작하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-183">Use one the following command to start the Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="31cfb-184">Windows 기반 클러스터를 사용하는 경우 대신 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-184">If you are using a Windows-based cluster, use the following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="31cfb-185">`grunt>` 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="31cfb-186">.NET Framework 응용 프로그램을 사용하는 Pig 작업을 실행하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-186">Enter the following to run a Pig job that uses the .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="31cfb-187">`DEFINE` 문은 pigudf.exe 응용 프로그램에 대한 `streamer`의 별칭을 만들고 `CACHE`는 클러스터의 기본 저장소에서 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-187">The `DEFINE` statement creates an alias of `streamer` for the pigudf.exe applications, and `CACHE` loads it from default storage for the cluster.</span></span> <span data-ttu-id="31cfb-188">나중에 `streamer`는 `STREAM` 연산자와 함께 사용되어 로그에 포함된 단일 줄을 처리하고 일련의 열로 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-188">Later, `streamer` is used with the `STREAM` operator to process the single lines contained in LOG and return the data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="31cfb-189">스트리밍에 사용되는 응용 프로그램 이름은 별칭이 지정된 경우 \`(기호) 문자로 묶어야 하며 `SHIP\`와 함께 사용된 경우 '(작은따옴표)로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-189">The application name that is used for streaming must be surrounded by the \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="31cfb-190">마지막 줄을 입력하면 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-190">After entering the last line, the job should start.</span></span> <span data-ttu-id="31cfb-191">다음 텍스트와 비슷한 출력이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-191">It returns output similar to the following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="31cfb-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31cfb-192">Next steps</span></span>

<span data-ttu-id="31cfb-193">이 문서에서는 HDInsight의 Hive 및 Pig에서 .NET Framework 응용 프로그램을 사용하는 방법에 대해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="31cfb-193">In this document, you have learned how to use a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="31cfb-194">Python을 Hive 및 Pig와 함께 사용하는 방법에 대해 알고 싶으면 [HDInsight에서 Hive 및 Pig와 함께 Python 사용](hdinsight-python.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-194">If you would like to learn how to use Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="31cfb-195">Pig 및 Hive를 사용하고 MapReduce 사용에 대해 배우는 다른 방법은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31cfb-195">For other ways to use Pig and Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="31cfb-196">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="31cfb-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="31cfb-197">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="31cfb-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="31cfb-198">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="31cfb-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
