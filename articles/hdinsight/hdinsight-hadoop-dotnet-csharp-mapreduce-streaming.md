---
title: "HDInsight - Azure의 Hadoop에서 MapReduce와 함께 C# 사용 | Microsoft Docs"
description: "Azure HDInsight에서 Hadoop과 함께 C#을 사용하여 MapReduce 솔루션을 만드는 방법에 대해 알아보세요."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: adb454e56378a800c671614735aec78b6851aeb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="3e2d4-103">HDInsight의 Hadoop에서 MapReduce와 함께 C# 사용</span><span class="sxs-lookup"><span data-stu-id="3e2d4-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="3e2d4-104">HDInsight에서 C#을 사용하여 MapReduce 솔루션을 만드는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e2d4-105">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3e2d4-106">자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="3e2d4-107">Hadoop 스트리밍은 스크립트 또는 실행 파일을 사용하여 MapReduce 작업을 실행할 수 있는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="3e2d4-108">이 예제에서는 단어 수 세기 솔루션을 위해 .NET을 사용하여 매퍼와 리듀서를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="3e2d4-109">HDInsight에서.NET</span><span class="sxs-lookup"><span data-stu-id="3e2d4-109">.NET on HDInsight</span></span>

<span data-ttu-id="3e2d4-110">__Linux 기반 HDInsight__ 클러스터는 [Mono(https://mono-project.com)](https://mono-project.com)를 사용하여 .NET 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="3e2d4-111">Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="3e2d4-112">HDInsight와 함께 제공되는 Mono 버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="3e2d4-113">특정 버전의 Mono를 사용하려면 [Mono 설치 또는 업데이트](hdinsight-hadoop-install-mono.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-113">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="3e2d4-114">.NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="3e2d4-115">Hadoop 스트리밍 작동 방식</span><span class="sxs-lookup"><span data-stu-id="3e2d4-115">How Hadoop streaming works</span></span>

<span data-ttu-id="3e2d4-116">이 문서의 스트리밍에 사용된 기본 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-116">The basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="3e2d4-117">Hadoop이 STDIN의 매퍼(이 예제의 경우 mapper.exe)로 데이터를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-117">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="3e2d4-118">매퍼가 데이터를 처리하고 탭으로 구분된 키/값 쌍을 STDOUT으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-118">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span></span>
3. <span data-ttu-id="3e2d4-119">Hadoop에서 이 출력을 읽습니다. 그런 다음 STDIN의 리듀서(이 예제의 경우 reducer.exe)로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-119">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="3e2d4-120">리듀서는 탭으로 구분된 키/값 쌍을 읽고 데이터를 처리한 다음 STDOUT에서 탭으로 구분된 키/값 쌍의 결과를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-120">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="3e2d4-121">Hadoop에서 이 출력을 읽습니다. 그런 다음 출력 디렉터리에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-121">The output is read by Hadoop and written to the output directory.</span></span>

<span data-ttu-id="3e2d4-122">스트리밍에 대한 자세한 내용은 [Hadoop 스트리밍(https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e2d4-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3e2d4-123">Prerequisites</span></span>

* <span data-ttu-id="3e2d4-124">.NET Framework 4.5를 대상으로 하는 C# 코드 작성 및 빌드에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="3e2d4-125">이 문서의 단계는 Visual Studio 2017을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-125">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="3e2d4-126">클러스터로 .exe 파일을 업로드하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-126">A way to upload .exe files to the cluster.</span></span> <span data-ttu-id="3e2d4-127">이 문서의 단계는 Data Lake Tools for Visual Studio를 사용하여 클러스터의 기본 저장소로 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-127">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span></span>

* <span data-ttu-id="3e2d4-128">Azure PowerShell 또는 SSH 클라이언트</span><span class="sxs-lookup"><span data-stu-id="3e2d4-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="3e2d4-129">HDInsight 클러스터의 Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="3e2d4-130">클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-provision-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-the-mapper"></a><span data-ttu-id="3e2d4-131">매퍼 만들기</span><span class="sxs-lookup"><span data-stu-id="3e2d4-131">Create the mapper</span></span>

<span data-ttu-id="3e2d4-132">Visual Studio에서 __mapper__라는 새 __콘솔 응용 프로그램__을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="3e2d4-133">응용 프로그램에 대해 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-133">Use the following code for the application:</span></span>

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data to the mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over the words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

<span data-ttu-id="3e2d4-134">응용 프로그램을 생성한 다음 빌드하여 프로젝트 디렉터리에 `/bin/Debug/mapper.exe` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-134">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span></span>

## <a name="create-the-reducer"></a><span data-ttu-id="3e2d4-135">리듀서 만들기</span><span class="sxs-lookup"><span data-stu-id="3e2d4-135">Create the reducer</span></span>

<span data-ttu-id="3e2d4-136">Visual Studio에서 __reducer__라는 새 __콘솔 응용 프로그램__을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="3e2d4-137">응용 프로그램에 대해 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-137">Use the following code for the application:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get the word
                string word = sArr[0];
                // Get the count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for the word?
                if(words.ContainsKey(word))
                {
                    //If so, increment the count
                    words[word] += count;
                } else
                {
                    //Add the key to the collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

<span data-ttu-id="3e2d4-138">응용 프로그램을 생성한 다음 빌드하여 프로젝트 디렉터리에 `/bin/Debug/reducer.exe` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-138">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="3e2d4-139">저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="3e2d4-139">Upload to storage</span></span>

1. <span data-ttu-id="3e2d4-140">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="3e2d4-141">**Azure**를 확장한 다음 **HDInsight**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="3e2d4-142">메시지가 표시되면 Azure 구독 자격 증명을 입력한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="3e2d4-143">이 응용 프로그램을 배포하려는 HDInsight 클러스터를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-143">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="3e2d4-144">텍스트가 포함된 항목__(기본 저장소 계정)__이 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-144">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![클러스터에 대한 저장소 계정을 보여주는 서버 탐색기](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="3e2d4-146">이 항목을 확장할 수 있는 경우 클러스터의 기본 저장소로 __Azure Storage 계정__을 사용하고 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="3e2d4-147">클러스터의 기본 저장소에서 파일을 보려면 항목을 확장한 다음 __(기본 컨테이너)__를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-147">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="3e2d4-148">이 항목을 확장할 수 없는 경우 클러스터의 기본 저장소로 __Azure Data Lake Store__를 사용하고 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="3e2d4-149">클러스터의 기본 저장소에 있는 파일을 보려면 항목을 확장한 다음 __(기본 저장소 계정)__을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-149">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="3e2d4-150">.exe 파일을 업로드하려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-150">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="3e2d4-151">__Azure Storage 계정__을 사용하는 경우 업로드 아이콘을 클릭한 다음 **bin\debug** 폴더로 이동하여 **mapper** 프로젝트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-151">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span></span> <span data-ttu-id="3e2d4-152">마지막으로 **mapper.exe** 파일을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-152">Finally, select the **mapper.exe** file and click **Ok**.</span></span>

        ![업로드 아이콘](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="3e2d4-154">__Azure Data Lake Store__를 사용하는 경우 마우스 오른쪽 버튼으로 파일 목록의 빈 영역을 클릭한 다음 __업로드__를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-154">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="3e2d4-155">마지막으로 **mapper.exe** 파일을 선택한 다음 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-155">Finally, select the **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="3e2d4-156">__mapper.exe__ 업로드가 완료되면 __reducer.exe__ 파일의 업로드 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-156">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="3e2d4-157">작업 실행: SSH 세션 사용</span><span class="sxs-lookup"><span data-stu-id="3e2d4-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="3e2d4-158">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-158">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="3e2d4-159">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3e2d4-160">다음 명령을 사용하여 MapReduce 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-160">Use one of the following command to start the MapReduce job:</span></span>

    * <span data-ttu-id="3e2d4-161">기본 저장소로 __Data Lake Store__를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="3e2d4-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="3e2d4-162">기본 저장소로 __Azure Storage__를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="3e2d4-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="3e2d4-163">다음 목록은 각 매개 변수가 하는 기능에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-163">The following list describes what each parameter does:</span></span>

    * <span data-ttu-id="3e2d4-164">`hadoop-streaming.jar`: 스트리밍 MapReduce 기능이 포함된 jar 파일</span><span class="sxs-lookup"><span data-stu-id="3e2d4-164">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="3e2d4-165">`-files`: 이 작업에 `mapper.exe` 및 `reducer.exe` 파일을 추가합니다. </span><span class="sxs-lookup"><span data-stu-id="3e2d4-165">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span></span> <span data-ttu-id="3e2d4-166">각 파일 앞의 `adl:///` 및 `wasb:///`는 클러스터의 기본 저장소의 루트에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-166">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span></span>
    * <span data-ttu-id="3e2d4-167">`-mapper`: mapper를 구현하는 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-167">`-mapper`: Specifies which file implements the mapper.</span></span>
    * <span data-ttu-id="3e2d4-168">`-reducer`: reducer를 구현하는 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-168">`-reducer`: Specifies which file implements the reducer.</span></span>
    * <span data-ttu-id="3e2d4-169">`-input`: 입력 데이터</span><span class="sxs-lookup"><span data-stu-id="3e2d4-169">`-input`: The input data.</span></span>
    * <span data-ttu-id="3e2d4-170">`-output`: 출력 디렉터리</span><span class="sxs-lookup"><span data-stu-id="3e2d4-170">`-output`: The output directory.</span></span>

3. <span data-ttu-id="3e2d4-171">MapReduce 작업이 완료되면 다음을 사용하여 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-171">Once the MapReduce job completes, use the following to view the results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="3e2d4-172">다음 텍스트는 이 명령에서 반환된 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-172">The following text is an example of the data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="3e2d4-173">작업 실행: PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="3e2d4-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="3e2d4-174">다음 PowerShell 스크립트를 사용하여 MapReduce 작업을 실행하고 결과를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-174">Use the following PowerShell script to run a MapReduce job and download the results.</span></span>

<span data-ttu-id="3e2d4-175">[!code-powershell[기본](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span><span class="sxs-lookup"><span data-stu-id="3e2d4-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span></span>

<span data-ttu-id="3e2d4-176">이 스크립트는 클러스터 로그인 계정 이름과 암호와 HDInsight 클러스터 이름을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-176">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span></span> <span data-ttu-id="3e2d4-177">작업이 완료되면 출력이 스크립트가 실행된 디렉터리의 `output.txt` 파일로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-177">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span></span> <span data-ttu-id="3e2d4-178">다음 텍스트는 `output.txt` 파일의 데이터 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-178">The following text is an example of the data in the `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="3e2d4-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e2d4-179">Next steps</span></span>

<span data-ttu-id="3e2d4-180">HDInsight에서 MapReduce 사용에 대한 자세한 내용은 [HDInsight에서 MapReduce 사용](hdinsight-use-mapreduce.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-180">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="3e2d4-181">Hive 및 Pig에서 C#을 사용하는 방법에 대한 자세한 내용은 [Hive 및 Pig에서 C# 사용자 정의 기능 사용](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-181">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="3e2d4-182">HDInsight의 Storm에서 C# 사용에 대한 자세한 내용은 [HDInsight에서 Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e2d4-182">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>