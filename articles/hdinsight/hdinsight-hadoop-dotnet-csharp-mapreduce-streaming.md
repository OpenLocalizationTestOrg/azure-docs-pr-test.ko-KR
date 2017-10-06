---
title: "C#에서 Azure HDInsight에서 Hadoop MapReduce로 aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 Azure HDInsight에서 Hadoop으로 toouse C# toocreate MapReduce 솔루션입니다."
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
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="378cd-103">HDInsight의 Hadoop에서 MapReduce와 함께 C# 사용</span><span class="sxs-lookup"><span data-stu-id="378cd-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="378cd-104">자세한 내용은 방법 toouse C# toocreate HDInsight에서 MapReduce 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="378cd-105">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="378cd-106">자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378cd-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="378cd-107">Hadoop 스트리밍는 스크립트 또는 실행 파일을 사용 하 여 toorun MapReduce 작업을 허용 하는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="378cd-108">이 예제에서는.NET은 사용 되는 tooimplement hello 매퍼 및 리 듀 서 단어 개수 솔루션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="378cd-109">HDInsight에서.NET</span><span class="sxs-lookup"><span data-stu-id="378cd-109">.NET on HDInsight</span></span>

<span data-ttu-id="378cd-110">__Linux 기반 HDInsight__ 사용 하 여 클러스터 [모노 (https://mono-project.com)](https://mono-project.com) toorun.NET 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="378cd-111">Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="378cd-112">HDInsight에 포함 된 모노 길이의 hello에 대 한 자세한 내용은 참조 하십시오. [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="378cd-113">toouse 모노의 특정 버전 참조 hello [설치 또는 업데이트 모노](hdinsight-hadoop-install-mono.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="378cd-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="378cd-114">.NET 프레임워크 버전과 Mono의 호환성에 대한 자세한 내용은 [Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378cd-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="378cd-115">Hadoop 스트리밍 작동 방식</span><span class="sxs-lookup"><span data-stu-id="378cd-115">How Hadoop streaming works</span></span>

<span data-ttu-id="378cd-116">이 문서에 스트리밍에 사용 되는 hello 기본 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="378cd-117">Hadoop에서 STDIN 데이터 toohello 매퍼 (이 예제의 mapper.exe)를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="378cd-118">hello 매퍼 hello 데이터를 처리 하 고 탭으로 구분 된 키/값 쌍 tooSTDOUT를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="378cd-119">hello 출력 hadoop를 읽고 STDIN의 toohello 리 듀 서 (이 예제의 reducer.exe)를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="378cd-120">hello 리 듀 서 hello 탭으로 구분 된 키/값 쌍을 읽습니다 하 고 hello 데이터를 처리 하 고 STDOUT에 탭으로 구분 된 키/값 쌍으로 hello 결과 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="378cd-121">hello 출력 hadoop 읽고 toohello 출력 디렉터리를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="378cd-122">스트리밍에 대한 자세한 내용은 [Hadoop 스트리밍(https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378cd-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="378cd-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="378cd-123">Prerequisites</span></span>

* <span data-ttu-id="378cd-124">.NET Framework 4.5를 대상으로 하는 C# 코드 작성 및 빌드에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="378cd-125">이 문서 사용 하 여 Visual Studio 2017의에서 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="378cd-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="378cd-126">방식으로 tooupload.exe 파일을 toohello 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="378cd-127">hello 단계가이 문서에 사용 하 여 hello 데이터 레이크 도구 hello 클러스터에 대 한 Visual Studio tooupload hello 파일 tooprimary 저장소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="378cd-128">Azure PowerShell 또는 SSH 클라이언트</span><span class="sxs-lookup"><span data-stu-id="378cd-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="378cd-129">HDInsight 클러스터의 Hadoop.</span><span class="sxs-lookup"><span data-stu-id="378cd-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="378cd-130">클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight 클러스터 만들기](hdinsight-provision-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378cd-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="378cd-131">Hello 매퍼 만들기</span><span class="sxs-lookup"><span data-stu-id="378cd-131">Create hello mapper</span></span>

<span data-ttu-id="378cd-132">Visual Studio에서 __mapper__라는 새 __콘솔 응용 프로그램__을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="378cd-133">Hello 응용 프로그램에 대 한 코드 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-133">Use hello following code for hello application:</span></span>

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
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
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

<span data-ttu-id="378cd-134">Hello 응용 프로그램을 만든 후 빌드합니다 tooproduce hello `/bin/Debug/mapper.exe` hello 프로젝트 디렉터리의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="378cd-135">Hello 리 듀 서 만들기</span><span class="sxs-lookup"><span data-stu-id="378cd-135">Create hello reducer</span></span>

<span data-ttu-id="378cd-136">Visual Studio에서 __reducer__라는 새 __콘솔 응용 프로그램__을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="378cd-137">Hello 응용 프로그램에 대 한 코드 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-137">Use hello following code for hello application:</span></span>

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
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
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

<span data-ttu-id="378cd-138">Hello 응용 프로그램을 만든 후 빌드합니다 tooproduce hello `/bin/Debug/reducer.exe` hello 프로젝트 디렉터리의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="378cd-139">Toostorage 업로드</span><span class="sxs-lookup"><span data-stu-id="378cd-139">Upload toostorage</span></span>

1. <span data-ttu-id="378cd-140">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="378cd-141">**Azure**를 확장한 다음 **HDInsight**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="378cd-142">메시지가 표시되면 Azure 구독 자격 증명을 입력한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="378cd-143">Hello HDInsight 클러스터를 toodeploy이 응용이 프로그램을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="378cd-144">Hello 텍스트 있는 항목이 __(기본 저장소 계정)__ 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Hello 클러스터에 대 한 hello 저장소 계정을 보여 주는 서버 탐색기](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="378cd-146">사용 중인 경우이 항목에서 확장할 수는 __Azure 저장소 계정__ hello 클러스터에 대 한 기본 저장소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="378cd-147">hello 클러스터에 대 한 hello 기본 저장소에 tooview hello 파일 hello 항목을 확장 하 고 hello 두 번 클릭 __(기본 컨테이너)__합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="378cd-148">사용 하는이 항목을 확장할 수 없으면, __Azure 데이터 레이크 저장소__ hello 클러스터에 대 한 기본 저장소 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="378cd-149">hello 클러스터에 대 한 hello 기본 저장소에 tooview hello 파일 hello를 두 번 클릭 __(기본 저장소 계정)__ 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="378cd-150">tooupload hello.exe 파일을 사용 하 여 hello 메서드를 다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="378cd-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="378cd-151">사용 하는 경우는 __Azure 저장소 계정__hello 업로드 아이콘을 클릭 한 다음 toohello 찾아보기, **bin\debug** hello에 대 한 폴더 **매퍼** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="378cd-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="378cd-152">마지막으로 hello 선택 **mapper.exe** 파일을 클릭 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![업로드 아이콘](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="378cd-154">사용 하는 경우 __Azure 데이터 레이크 저장소__를 hello 파일 목록에서 빈 영역을 마우스 오른쪽 단추로 클릭 한 다음 선택 __업로드__합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="378cd-155">마지막으로 hello 선택 **mapper.exe** 파일을 클릭 하 여 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="378cd-156">한 번 hello __mapper.exe__ 업로드가 완료 되 면 hello에 대 한 반복 hello 업로드 프로세스 __reducer.exe__ 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="378cd-157">작업 실행: SSH 세션 사용</span><span class="sxs-lookup"><span data-stu-id="378cd-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="378cd-158">SSH tooconnect toohello HDInsight 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="378cd-159">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378cd-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="378cd-160">Hello 명령 toostart hello MapReduce 작업을 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="378cd-161">기본 저장소로 __Data Lake Store__를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="378cd-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="378cd-162">기본 저장소로 __Azure Storage__를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="378cd-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="378cd-163">hello 목록 다음 각 매개 변수에 용도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="378cd-164">`hadoop-streaming.jar`: hello 스트리밍 MapReduce 기능을 포함 하는 hello jar 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="378cd-165">`-files`: Hello 추가 `mapper.exe` 및 `reducer.exe` 파일 toothis 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="378cd-166">hello `adl:///` 또는 `wasb:///` 각 파일은 hello 클러스터에 대 한 기본 저장소의 hello 경로 toohello 루트 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="378cd-167">`-mapper`: Hello 맵 편집기를 구현 하는 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="378cd-168">`-reducer`: Hello 리 듀 서를 구현 하는 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="378cd-169">`-input`: hello 입력 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="378cd-170">`-output`: hello 출력 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="378cd-171">Hello MapReduce 작업 완료 되 면 다음 tooview hello 결과 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="378cd-172">hello 다음 텍스트는이 명령에서 반환 된 hello 데이터의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="378cd-173">작업 실행: PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="378cd-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="378cd-174">PowerShell 스크립트 toorun MapReduce 작업을 수행 하는 hello를 사용 하 고 hello 결과 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="378cd-175">이 스크립트를 hello 클러스터 로그인 계정 이름 및 hello HDInsight 클러스터 이름 함께 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="378cd-176">Hello 출력은 다운로드 한 toohello hello 작업이 완료 되 면 `output.txt` hello 디렉터리 hello 스크립트에는 파일에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="378cd-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="378cd-177">hello 다음 텍스트는 hello에 hello 데이터의 예로 `output.txt` 파일:</span><span class="sxs-lookup"><span data-stu-id="378cd-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="378cd-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="378cd-178">Next steps</span></span>

<span data-ttu-id="378cd-179">HDInsight에서 MapReduce 사용에 대한 자세한 내용은 [HDInsight에서 MapReduce 사용](hdinsight-use-mapreduce.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378cd-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="378cd-180">Hive 및 Pig에서 C#을 사용하는 방법에 대한 자세한 내용은 [Hive 및 Pig에서 C# 사용자 정의 기능 사용](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378cd-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="378cd-181">HDInsight의 Storm에서 C# 사용에 대한 자세한 내용은 [HDInsight에서 Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="378cd-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>