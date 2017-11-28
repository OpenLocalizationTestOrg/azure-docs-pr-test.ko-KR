---
title: "Visual Studio 및 C#-Azure HDInsight aaaApache 스톰 토폴로지 | Microsoft Docs"
description: "자세한 방법을 C#의 toocreate 스톰 토폴로지입니다. Visual Studio에 대 한 hello Hadoop 도구를 사용 하 여 Visual Studio에서 간단한 단어 개수 토폴로지를 만듭니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="5d119-104">Visual Studio에 대 한 hello 데이터 레이크 도구를 사용 하 여 Apache Storm의 C# 토폴로지를 개발</span><span class="sxs-lookup"><span data-stu-id="5d119-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="5d119-105">어떻게 toocreate hello Azure 데이터 레이크 (Hadoop)를 사용 하 여 C# 스톰 토폴로지 l 용 도구 Visual Studio에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="5d119-106">이 문서 Visual Studio에서 Storm 프로젝트 만들기, 로컬 컴퓨터에서 테스트 및 Azure HDInsight 클러스터에서 Apache Storm tooan 배포 hello 프로세스를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="5d119-107">또한 학습 방법 C#과 Java 구성 요소를 사용 하는 toocreate 하이브리드 토폴로지에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="5d119-108">이 문서의 단계 hello Visual Studio와 함께 Windows 개발 환경에 사용 해야 하는 동안 hello 컴파일된 프로젝트 제출 된 tooeither Linux 또는 Windows 기반 HDInsight 클러스터 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="5d119-109">2016년 10월 28일 이후에 만든 Linux 기반 클러스터만 SCP.NET 토폴로지를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="5d119-110">Linux 기반 클러스터와 toouse C# 토폴로지를 hello 이상을 사용 하 여 프로젝트 tooversion 0.10.0.6에서 Microsoft.SCP.Net.SDK NuGet 패키지를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="5d119-111">또한 hello 버전의 hello 패키지 hello HDInsight에 설치 된 Storm의 주 버전을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="5d119-112">HDInsight 버전</span><span class="sxs-lookup"><span data-stu-id="5d119-112">HDInsight version</span></span> | <span data-ttu-id="5d119-113">Storm 버전</span><span class="sxs-lookup"><span data-stu-id="5d119-113">Storm version</span></span> | <span data-ttu-id="5d119-114">SCP.NET 버전</span><span class="sxs-lookup"><span data-stu-id="5d119-114">SCP.NET version</span></span> | <span data-ttu-id="5d119-115">기본 모노 버전</span><span class="sxs-lookup"><span data-stu-id="5d119-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="5d119-116">3.3</span><span class="sxs-lookup"><span data-stu-id="5d119-116">3.3</span></span> |<span data-ttu-id="5d119-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="5d119-117">0.10.x</span></span> |<span data-ttu-id="5d119-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="5d119-118">0.10.x.x</span></span></br><span data-ttu-id="5d119-119">(Windows 기반 HDInsight만 해당)</span><span class="sxs-lookup"><span data-stu-id="5d119-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="5d119-120">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5d119-120">NA</span></span> |
| <span data-ttu-id="5d119-121">3.4</span><span class="sxs-lookup"><span data-stu-id="5d119-121">3.4</span></span> | <span data-ttu-id="5d119-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="5d119-122">0.10.0.x</span></span> | <span data-ttu-id="5d119-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="5d119-123">0.10.0.x</span></span> | <span data-ttu-id="5d119-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="5d119-124">3.2.8</span></span> |
| <span data-ttu-id="5d119-125">3.5</span><span class="sxs-lookup"><span data-stu-id="5d119-125">3.5</span></span> | <span data-ttu-id="5d119-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="5d119-126">1.0.2.x</span></span> | <span data-ttu-id="5d119-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="5d119-127">1.0.0.x</span></span> | <span data-ttu-id="5d119-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="5d119-128">4.2.1</span></span> |
| <span data-ttu-id="5d119-129">3.6</span><span class="sxs-lookup"><span data-stu-id="5d119-129">3.6</span></span> | <span data-ttu-id="5d119-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="5d119-130">1.1.0.x</span></span> | <span data-ttu-id="5d119-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="5d119-131">1.0.0.x</span></span> | <span data-ttu-id="5d119-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="5d119-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5d119-133">Linux 기반 클러스터에서 C# 토폴로지는.NET 4.5를 사용 하 고 모노 toorun hello HDInsight 클러스터에서 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="5d119-134">[Mono 호환성](http://www.mono-project.com/docs/about-mono/compatibility/)에서 잠재적인 비호환성을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5d119-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="5d119-135">Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="5d119-135">Install Visual Studio</span></span>

<span data-ttu-id="5d119-136">C# 토폴로지 SCP.NET hello 버전의 Visual Studio를 다음 중 하나를 사용 하 여 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="5d119-137">Visual Studio 2012 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="5d119-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="5d119-138">Visual Studio 2013 [업데이트 4](http://www.microsoft.com/download/details.aspx?id=44921) 또는 [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="5d119-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="5d119-139">Visual Studio 2015 또는 [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="5d119-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="5d119-140">Visual Studio 2017(모든 버전)</span><span class="sxs-lookup"><span data-stu-id="5d119-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="5d119-141">Data Lake Tools for Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="5d119-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="5d119-142">tooinstall 데이터 레이크 tools for Visual Studio에서 다음과 같이 hello [데이터 레이크 도구를 사용 하 여 Visual Studio 용 시작](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="5d119-143">Java 설치</span><span class="sxs-lookup"><span data-stu-id="5d119-143">Install Java</span></span>

<span data-ttu-id="5d119-144">Visual Studio에서 Storm 토폴로지를 제출 하면 SCP.NET hello 토폴로지 및 종속성이 포함 된 zip 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="5d119-145">Java는 사용 되는 toocreate 보다 Linux 기반 클러스터와 호환 되는 형식을 사용 하기 때문에이 zip 파일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="5d119-146">Hello 키트 JDK (Java 개발자) 7 또는 나중에 개발 환경을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="5d119-147">가져올 수에서 Oracle JDK hello [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="5d119-148">[다른 Java 배포](http://openjdk.java.net/)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="5d119-149">hello `JAVA_HOME` Java 포함 되어 있는 환경 변수 해야 지점 toohello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="5d119-150">hello `PATH` 환경 변수는 hello를 포함 해야 `%JAVA_HOME%\bin` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="5d119-151">다음 Java 및 hello JDK 올바르게 설치 되어 C# 콘솔 응용 프로그램 tooverify hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="5d119-152">Storm 템플릿</span><span class="sxs-lookup"><span data-stu-id="5d119-152">Storm templates</span></span>

<span data-ttu-id="5d119-153">Visual Studio에 대 한 hello 데이터 레이크 도구 hello 다음 서식 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="5d119-154">프로젝트 형식</span><span class="sxs-lookup"><span data-stu-id="5d119-154">Project type</span></span> | <span data-ttu-id="5d119-155">데모</span><span class="sxs-lookup"><span data-stu-id="5d119-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="5d119-156">Storm 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5d119-156">Storm Application</span></span> |<span data-ttu-id="5d119-157">빈 Storm 토폴로지 프로젝트</span><span class="sxs-lookup"><span data-stu-id="5d119-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="5d119-158">Storm Azure SQL 기록기 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="5d119-159">어떻게 toowrite tooAzure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="5d119-160">Storm Azure Cosmos DB 판독기 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="5d119-161">어떻게 Azure Cosmos DB에서 tooread 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="5d119-162">Storm Azure Cosmos DB 기록기 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="5d119-163">어떻게 toowrite tooAzure Cosmos DB입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="5d119-164">Storm 이벤트 허브 판독기 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="5d119-165">어떻게 Azure 이벤트 허브에서 tooread 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="5d119-166">Storm 이벤트 허브 기록기 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="5d119-167">어떻게 toowrite tooAzure 이벤트 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="5d119-168">Storm HBase 판독기 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="5d119-169">어떻게 HDInsight에서 HBase에서 tooread를 클러스터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="5d119-170">Storm HBase 기록기 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="5d119-171">어떻게 toowrite tooHBase에 HDInsight 클러스터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="5d119-172">Storm 하이브리드 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="5d119-173">어떻게 toouse Java 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="5d119-174">Storm 샘플</span><span class="sxs-lookup"><span data-stu-id="5d119-174">Storm Sample</span></span> |<span data-ttu-id="5d119-175">기본 단어 카운트 토폴로지</span><span class="sxs-lookup"><span data-stu-id="5d119-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="5d119-176">일부 템플릿은 Linux 기반 HDInsight에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="5d119-177">Hello 템플릿으로 사용 되는 Nuget 패키지는 모노 호환 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="5d119-178">Hello 확인 [모노 호환성](http://www.mono-project.com/docs/about-mono/compatibility/) 문서화 하 고 hello를 사용 하 여 [.NET 이식성 분석기](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify 잠재적인 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="5d119-179">이 문서의 단계 hello hello 기본 스톰 응용 프로그램 프로젝트 형식을 toocreate 토폴로지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="5d119-180">HBase 템플릿 정보</span><span class="sxs-lookup"><span data-stu-id="5d119-180">HBase templates notes</span></span>

<span data-ttu-id="5d119-181">hello HBase 판독기 및 작성기 템플릿 하지 hello HBase Java API HDInsight 클러스터에서 HBase와 toocommunicate hello HBase REST API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="5d119-182">EventHub 템플릿 정보</span><span class="sxs-lookup"><span data-stu-id="5d119-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d119-183">EventHub Java 기반 hello spout EventHub 판독기 템플릿 스톰 HDInsight 버전 3.5 이상에서 작동 하지 hello로 포함 된 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="5d119-184">이 구성 요소의 업데이트 된 버전은 [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="5d119-185">이 구성 요소를 사용하고 HDInsight 3.5의 Storm에서 작동하는 토폴로지의 예는 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d119-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="5d119-186">C# 토폴로지 만들기</span><span class="sxs-lookup"><span data-stu-id="5d119-186">Create a C# topology</span></span>

1. <span data-ttu-id="5d119-187">Visual Studio를 열고 **파일** > **새로 만들기**를 선택한 다음 **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="5d119-188">Hello에서 **새 프로젝트** 창 확장 **설치 됨** > **템플릿**를 선택 하 고 **Azure 데이터 레이크**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="5d119-189">Hello 템플릿 목록에서 선택 **스톰 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="5d119-190">Hello 화면 hello 맨 아래에 입력 **WordCount** hello 응용 프로그램의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![새 프로젝트 창의 스크린샷](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="5d119-192">Hello 프로젝트를 만든 후 hello 다음 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="5d119-193">**Program.cs**:이 파일은 프로젝트에 대 한 hello 토폴로지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="5d119-194">기본적으로 하나의 Spout 및 하나의 Bolt로 구성된 기본 토폴로지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="5d119-195">**Spout.cs**: 난수를 내보내는 예제 Spout입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="5d119-196">**Bolt.cs**: hello 배출구에서 내보낸 번호 개수를 유지 하는 예제 볼트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="5d119-197">NuGet 다운로드 최신 hello hello 프로젝트를 만들 때 [SCP.NET 패키지](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="5d119-198">Hello 배출구 구현</span><span class="sxs-lookup"><span data-stu-id="5d119-198">Implement hello spout</span></span>

1. <span data-ttu-id="5d119-199">**Spout.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-199">Open **Spout.cs**.</span></span> <span data-ttu-id="5d119-200">Spouts은 외부 원본에서 토폴로지에서 사용 되는 tooread 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="5d119-201">배출구에 대 한 hello 주 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="5d119-202">**NextTuple**: hello 배출구 tooemit 새 튜플 허용 될 때 스톰에 의해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="5d119-203">**Ack** (트랜잭션 토폴로지에만 해당): 튜플 hello 배출구에서 전송에 대 한 hello 토폴로지 내의 다른 구성 요소에서 시작 된 승인을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="5d119-204">튜플을 승인 hello 배출구를 다운스트림 구성 요소에 의해 성공적으로 처리 된 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="5d119-205">**실패** (트랜잭션 토폴로지에만 해당): 튜플 하는 실패 처리 hello 토폴로지 내의 다른 구성 요소를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="5d119-206">Fail 메서드를 구현 하면 toore-다시 처리할 수 있도록 hello 튜플을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="5d119-207">Hello hello 내용 바꾸기 **Spout** 텍스트 다음 hello 사용 하 여 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="5d119-208">임의로이 배출구 hello 토폴로지 문장을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="5d119-209">Hello 볼트 구현</span><span class="sxs-lookup"><span data-stu-id="5d119-209">Implement hello bolts</span></span>

1. <span data-ttu-id="5d119-210">Hello 기존 삭제 **Bolt.cs** hello 프로젝트에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="5d119-211">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="5d119-212">Hello 목록에서 선택 **스톰 볼트**, 입력 **Splitter.cs** hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="5d119-213">명명 된 두 번째는 이외의 경우이 프로세스 toocreate 반복 **Counter.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="5d119-214">**Splitter.cs**: 문장을 개별 단어로 분리하는 Bolt를 구현하고 새로운 단어 스트림을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="5d119-215">**Counter.cs**: 각 단어 수를 계산 하는 새 스트림을 단어와 각 단어에 대 한 hello 수는 이외의 경우 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5d119-216">하지만 이러한 볼트 한 읽기 및 쓰기 toostreams, 데이터베이스 또는 서비스와 같은 원본 볼트 toocommunicate을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="5d119-217">**Splitter.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="5d119-218">기본적으로 **Execute**라는 하나의 메서드만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="5d119-219">hello Execute 메서드는 hello 볼트 처리에 대 한 튜플이 받을 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="5d119-220">여기에서 들어오는 튜플을 읽고 처리하며 나가는 튜플을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="5d119-221">Hello hello 내용 바꾸기 **분할자** 코드 다음 hello 사용 하 여 클래스:</span><span class="sxs-lookup"><span data-stu-id="5d119-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="5d119-222">열기 **Counter.cs**, hello 클래스 내용을 hello 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="5d119-223">Hello 토폴로지 정의</span><span class="sxs-lookup"><span data-stu-id="5d119-223">Define hello topology</span></span>

<span data-ttu-id="5d119-224">Spouts 및 볼트는 구성 요소 간 hello 데이터 흐름 방식을 정의 하는 그래프를 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="5d119-225">이 토폴로지의 경우 hello 그래프는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-225">For this topology, hello graph is as follows:</span></span>

![구성 요소 정렬 방식 다이어그램](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="5d119-227">Hello 배출구에서 내보내집니다 문장과 hello 분할자 볼트의 분산된 tooinstances 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="5d119-228">hello 분할자 볼트 분산된 toohello 카운터 볼트는 단어로 hello 문장을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="5d119-229">특정 단어 toohello 흐름는 있는지 toomake 원하는 단어 개수는 hello 카운터 인스턴스에 로컬로 보유 되므로, 카운터 볼트 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="5d119-230">각 인스턴스는 특정 단어를 계속 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="5d119-231">Hello 분할자 볼트 없음 상태를 관리 하는 경우 이후 실제로 문제가 되지 않습니다 hello 분할자의 인스턴스는 문장 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="5d119-232">**Program.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-232">Open **Program.cs**.</span></span> <span data-ttu-id="5d119-233">hello 중요 한 메서드는 **GetTopologyBuilder**, tooStorm 제출 하는 사용 되는 toodefine hello 토폴로지는입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="5d119-234">Hello 내용 바꾸기 **GetTopologyBuilder** 코드 tooimplement hello 토폴로지 앞에서 설명한 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="5d119-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="5d119-235">Hello 토폴로지 전송</span><span class="sxs-lookup"><span data-stu-id="5d119-235">Submit hello topology</span></span>

1. <span data-ttu-id="5d119-236">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **HDInsight의 tooStorm 제출**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5d119-237">메시지가 표시 되 면 Azure 구독에 대 한 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="5d119-238">구독이 둘 이상 있는 경우 프로그램 스톰 HDInsight 클러스터에 포함 된 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="5d119-239">Hello에서 HDInsight 클러스터에서 프로그램 스톰 선택 **Storm 클러스터** 드롭 다운 목록에서 선택한 후 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="5d119-240">Hello 제출 hello를 사용 하 여 성공한 경우를 모니터링할 수 있습니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="5d119-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="5d119-241">Hello 토폴로지 성공적으로 제출 되 면 hello **스톰 토폴로지** hello 클러스터 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="5d119-242">선택 hello **WordCount** 토폴로지를 실행 하는 hello에 대 한 hello 목록 tooview 정보에서 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5d119-243">**서버 탐색기**에서 **Storm 토폴로지**를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="5d119-244">**Azure** > **HDInsight**를 확장하고 HDInsight 클러스터에서 Storm을 마우스 오른쪽 단추로 클릭한 다음 **Storm 토폴로지 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="5d119-245">hello 토폴로지의 hello 구성 요소에 대 한 정보 tooview hello 다이어그램의 hello 구성 요소를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="5d119-246">Hello에서 **토폴로지 요약** 보려면 클릭 하십시오. **Kill** toostop hello 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5d119-247">Storm 토폴로지는 비활성화 되거나 hello 클러스터 삭제 될 때까지 toorun를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="5d119-248">트랜잭션 토폴로지</span><span class="sxs-lookup"><span data-stu-id="5d119-248">Transactional topology</span></span>

<span data-ttu-id="5d119-249">hello 이전 토폴로지는 비트랜잭션 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="5d119-250">hello 토폴로지의 hello 구성 요소 기능 tooreplaying 메시지를 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="5d119-251">트랜잭션 토폴로지의 예로에 대 한 프로젝트를 만들고 선택 **스톰 샘플** hello 프로젝트 형식을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="5d119-252">트랜잭션 토폴로지 toosupport 재생 데이터의 다음 hello를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="5d119-253">**메타 데이터 캐싱을**: hello 배출구 내보내는 hello 데이터를 검색 하 고 실패 한 경우 다시 내보낼 수 있도록 하는 hello 데이터에 대 한 메타 데이터를 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="5d119-254">Hello 샘플에서 내보내는 hello 데이터 작은 이기 때문에 각 튜플에 대해 hello 원시 데이터를 재생 하기 위해 사전에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="5d119-255">**Ack**: hello 토폴로지에서 각 볼트 호출할 수 `this.ctx.Ack(tuple)` 튜플을 성공적으로 처리 했음을 tooacknowledge 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="5d119-256">모든 볼트 했지만 hello 튜플 경우 hello `Ack` hello 배출구의 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="5d119-257">hello `Ack` hello 배출구 tooremove 데이터를 재생 하기 위해 캐시 된 메서드를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="5d119-258">**실패**: 각 볼트 호출할 수 `this.ctx.Fail(tuple)` tooindicate 처리 하는 튜플을 대 한 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="5d119-259">hello 오류 전파 toohello `Fail` 메서드를 사용 하 여 hello 튜플을 재생할 수 있습니다 위치 하는 hello 배출구의 캐시 된 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="5d119-260">**Sequence ID**: 튜플을 내보낼 때 고유한 시퀀스 ID를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="5d119-261">이 값 (Ack 및 실패) 재생 처리에 대 한 hello 튜플이 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="5d119-262">예를 들어 hello에 배출구 hello **스톰 샘플** 프로젝트 hello 다음 사용 하 여 데이터를 내보낼 때:</span><span class="sxs-lookup"><span data-stu-id="5d119-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="5d119-263">이 코드에 포함 된 hello 시퀀스 ID 값을 가진 문장 toohello 기본 스트림이 포함 하는 튜플을 내보냅니다 **lastSeqId**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="5d119-264">이 예제에서 **lastSeqId** 는 제출된 모든 튜플마다 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="5d119-265">Hello에서와 같이 **스톰 샘플** 프로젝트에서 구성 요소는 트랜잭션 여부 구성에 따라 런타임에 설정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="5d119-266">C# 및 Java를 통한 하이브리드 토폴로지</span><span class="sxs-lookup"><span data-stu-id="5d119-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="5d119-267">또한 일부 구성 요소가 C# 하 고 나머지는 Java Visual Studio toocreate 하이브리드 토폴로지에서 사용에 대 한 데이터 레이크 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="5d119-268">하이브리드 토폴로지의 예를 보려면 프로젝트를 만들고 **Storm 하이브리드 샘플**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="5d119-269">이 샘플 형식 hello 다음 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="5d119-270">**Java spout** 및 **C# bolt**: **HybridTopology_javaSpout_csharpBolt**에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="5d119-271">트랜잭션 버전은 **HybridTopologyTx_javaSpout_csharpBolt**에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="5d119-272">**C# spout** 및 **Java bolt**: **HybridTopology_csharpSpout_javaBolt**에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="5d119-273">트랜잭션 버전은 **HybridTopologyTx_csharpSpout_javaBolt**에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5d119-274">이 버전에는 텍스트 파일을 Java 구성 요소에서 발생 한 toouse Clojure 코드 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="5d119-275">hello 프로젝트 제출 될 때 사용 되는 tooswitch hello 토폴로지 hello 이동 하기만 `[Active(true)]` toouse, toohello 클러스터 제출 하기 전에 원하는 문 toohello 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5d119-276">필요한 모든 hello Java 파일 hello에서이 프로젝트의 일부로 제공 됩니다 **JavaDependency** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="5d119-277">만들고 하이브리드 토폴로지를 제출 하려는 경우 다음을 hello를 고려 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5d119-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="5d119-278">사용 해야 **JavaComponentConstructor** toocreate hello 배출구 또는 번개에 대 한 Java 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="5d119-279">사용 해야 **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** Java에서 Java 구성 요소 안팎으로 데이터를 tooserialize tooJSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="5d119-280">Hello를 사용 해야 hello 토폴로지 toohello 서버를 전송할 때 **추가 구성을** 옵션 toospecify hello **Java 파일 경로**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="5d119-281">지정 된 hello 경로는 Java 클래스를 포함 하는 hello JAR 파일이 포함 된 hello 디렉터리 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="5d119-282">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5d119-282">Azure Event Hubs</span></span>

<span data-ttu-id="5d119-283">0.9.4.203 SCP.NET 버전에는 새 클래스 및 메서드 hello 이벤트 허브 배출구 (이벤트 허브에서 읽을 수 있는 Java 배출구)를 사용 하기 위한 구체적으로 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="5d119-284">이벤트 허브 배출구를 사용 하는 토폴로지를 만들 때 다음 메서드는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="5d119-285">**EventHubSpoutConfig** 클래스: hello 배출구 구성 요소에 대 한 hello 구성을 포함 하는 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="5d119-286">**TopologyBuilder.SetEventHubSpout** 메서드: hello 이벤트 허브 배출구 구성 요소 toohello 토폴로지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="5d119-287">Hello 반드시 사용 해야 **CustomizedInteropJSONSerializer** hello 배출구에 의해 생성 된 tooserialize 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="5d119-288"><a id="configurationmanager"></a>ConfigurationManager 사용</span><span class="sxs-lookup"><span data-stu-id="5d119-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="5d119-289">사용 하지 않는 **ConfigurationManager** tooretrieve 구성에서 값 볼트 및 spout 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="5d119-290">이렇게 하면 null 포인터 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="5d119-291">대신, 프로젝트에 대 한 hello 구성은 hello 토폴로지 컨텍스트에서 키 및 값 쌍으로 hello 스톰 토폴로지로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="5d119-292">구성 값을 사용 하는 각 구성 요소에서에서 검색 해야 해당 hello 컨텍스트 초기화 중.</span><span class="sxs-lookup"><span data-stu-id="5d119-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="5d119-293">hello 다음 코드에서는 방법을 tooretrieve 이러한 값:</span><span class="sxs-lookup"><span data-stu-id="5d119-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="5d119-294">사용 하는 경우는 `Get` 메서드 tooreturn 구성 요소의 인스턴스를 확인 해야 두 hello을 통과 하는지 `Context` 및 `Dictionary<string, Object>` toohello 생성자 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="5d119-295">hello 다음 예제는 기본 `Get` 제대로 이러한 값을 전달 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="5d119-296">어떻게 tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="5d119-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="5d119-297">SCP.NET의 최신 릴리스는 NuGet을 통해 패키지 업그레이드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="5d119-298">새 업데이트를 사용할 수 있을 때 업그레이드 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="5d119-299">업그레이드에 대 한 toomanually 검사는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="5d119-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="5d119-300">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="5d119-301">Hello 패키지 관리자에서에서 선택 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="5d119-302">사용할 수 있는 업데이트가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-302">If an update is available, it is listed.</span></span> <span data-ttu-id="5d119-303">클릭 **업데이트** 패키지 tooinstall hello에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d119-304">NuGet을 사용 하지 않은 SCP.NET의 이전 버전에서 프로젝트를 만든 경우 hello 단계 tooupdate tooa 최신 버전을 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="5d119-305">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="5d119-306">Hello를 사용 하 여 **검색** 필드를 검색 한 다음 추가 **Microsoft.SCP.Net.SDK** toohello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="5d119-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="5d119-307">토폴로지의 일반적인 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5d119-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="5d119-308">Null 포인터 예외</span><span class="sxs-lookup"><span data-stu-id="5d119-308">Null pointer exceptions</span></span>

<span data-ttu-id="5d119-309">Linux 기반 HDInsight 클러스터와 C# 토폴로지를 사용 하는 경우 볼트 및 구성 요소를 사용 하는 spout **ConfigurationManager** 런타임에 tooread 구성 설정에는 null 포인터 예외가 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="5d119-310">프로젝트에 대 한 hello 구성 hello 스톰 토폴로지 hello 토폴로지 컨텍스트에서 키 및 값 쌍으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="5d119-311">초기화 되 면 tooyour 구성 요소에 전달 되는 hello 사전 개체에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="5d119-312">자세한 내용은 참조 hello [ConfigurationManager](#configurationmanager) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="5d119-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="5d119-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="5d119-313">System.TypeLoadException</span></span>

<span data-ttu-id="5d119-314">Linux 기반 HDInsight 클러스터와 C# 토폴로지를 사용 하는 경우에 hello 다음 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="5d119-315">이 오류는 hello 버전의.NET에서 지 원하는 모노와 호환 되지 않습니다는 바이너리를 사용 하는 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="5d119-316">Linux 기반 HDInsight 클러스터의 경우 프로젝트에서 .NET 4.5에 대해 컴파일된 이진 파일을 사용하는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="5d119-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="5d119-317">로컬로 토폴로지 테스트</span><span class="sxs-lookup"><span data-stu-id="5d119-317">Test a topology locally</span></span>

<span data-ttu-id="5d119-318">쉽게 toodeploy 토폴로지 tooa 클러스터 일부 경우에는 토폴로지를 로컬로 tootest을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="5d119-319">다음 단계 toorun hello를 사용 하 고 로컬 개발 환경에서에서이 자습서에서는 hello 토폴로지 예제를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="5d119-320">로컬 테스트는 기본 C# 전용 토폴로지에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="5d119-321">하이브리드 토폴로지나 여러 스트림을 사용하는 토폴로지에는 로컬 테스트를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="5d119-322">**솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="5d119-323">Hello 프로젝트 속성에서 변경 hello **출력 형식이** 너무**콘솔 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![출력 유형이 강조 표시된 프로젝트 속성의 스크린샷](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="5d119-325">Toochange hello 기억 **출력 형식이** 너무 다시**클래스 라이브러리** hello 토폴로지 tooa 클러스터를 배포 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5d119-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="5d119-326">**솔루션 탐색기**를 hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 선택 **추가** > **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="5d119-327">선택 **클래스**, 입력 **LocalTest.cs** hello 클래스 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="5d119-328">마지막으로 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="5d119-329">열기 **LocalTest.cs**, hello 다음 추가 및 **를 사용 하 여** hello 위쪽에 문의:</span><span class="sxs-lookup"><span data-stu-id="5d119-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="5d119-330">사용 하 여 hello 다음 hello의 hello 콘텐츠로 코드 **LocalTest** 클래스:</span><span class="sxs-lookup"><span data-stu-id="5d119-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="5d119-331">Hello 코드 주석을 통해 순간 tooread를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="5d119-332">이 코드를 사용 하 여 **LocalContext** hello 로컬 드라이브에 tootext 파일 구성 요소 간의 데이터 스트림을 hello을 계속 되 면 hello 개발 환경에 toorun hello 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="5d119-333">열기 **Program.cs**, hello toohello 다음 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="5d119-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="5d119-334">Hello 변경 내용을 저장 한 다음 클릭 **F5** 선택 또는 **디버그** > **디버깅 시작** toostart hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="5d119-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="5d119-335">콘솔 창 표시를 hello 테스트 진행률 상태를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="5d119-336">때 **테스트가 완료** 표시 되 면 아무 키 tooclose hello 창 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="5d119-337">사용 하 여 **Windows 탐색기** 프로젝트를 포함 하는 toolocate hello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="5d119-338">예: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="5d119-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="5d119-339">이 디렉터리에서 **Bin**을 열고 **디버그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="5d119-340">Hello 테스트를 실행할 때 생성 된 hello 텍스트 파일에 표시 됩니다: sentences.txt, counter.txt, 및 splitter.txt 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="5d119-341">각 텍스트 파일을 열고 hello 데이터를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5d119-342">문자열 데이터는 이러한 파일에 10진수 값의 배열로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="5d119-343">예를 들어 \[[97,103,111]] hello에 **splitter.txt** 파일은 hello 단어 *및*합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="5d119-344">수 있는지 tooset hello **프로젝트 형식을** 너무 다시**클래스 라이브러리** tooa 스톰 HDInsight 클러스터에 배포 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5d119-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="5d119-345">로그 정보</span><span class="sxs-lookup"><span data-stu-id="5d119-345">Log information</span></span>

<span data-ttu-id="5d119-346">`Context.Logger`를 사용하여 토폴로지 구성 요소에서 정보를 쉽게 로깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="5d119-347">예를 들어 hello 다음 정보 로그 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="5d119-348">Hello에서 기록 된 정보를 볼 수 있습니다 **Hadoop 서비스 로그**에 있는 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="5d119-349">HDInsight 클러스터에서 프로그램 Storm의 hello 항목을 확장 한 다음 확장 **Hadoop 서비스 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="5d119-350">마지막으로, 로그 파일 tooview hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="5d119-351">hello 로그 hello 클러스터에서 사용 되는 Azure 저장소 계정에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="5d119-352">Visual Studio에서 tooview hello 로그, toohello hello 저장소 계정을 소유한 Azure 구독에에서 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="5d119-353">오류 정보 보기</span><span class="sxs-lookup"><span data-stu-id="5d119-353">View error information</span></span>

<span data-ttu-id="5d119-354">tooview 발생 한 오류를 실행 중인 토폴로지에서 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="5d119-355">**서버 탐색기**hello 스톰 HDInsight 클러스터에서를 마우스 오른쪽 단추로 클릭 하 고 선택 **보기 스톰 토폴로지**합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="5d119-356">Hello에 대 한 **Spout** 및 **쐐기**, hello **마지막 오류** 열 hello 마지막 오류에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="5d119-357">선택 hello **Spout Id** 또는 **볼트 Id** 나열 된 오류가 있는 hello 구성 요소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="5d119-358">Hello에 hello 세부 정보 페이지를 표시 하 고 추가 오류 정보가 나열 됩니다 **오류** hello hello 페이지 맨 아래에 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="5d119-359">tooobtain 자세한 정보는 **포트** hello에서 **Executor** hello 페이지의 섹션, 마지막 몇 분 동안 hello에 대 한 toosee hello Storm 작업자 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="5d119-360">토폴로지 제출 중 오류</span><span class="sxs-lookup"><span data-stu-id="5d119-360">Errors submitting topologies</span></span>

<span data-ttu-id="5d119-361">토폴로지 tooHDInsight 전송 오류가 발생 하는 경우에 HDInsight 클러스터에 제출 토폴로지를 처리 하는 hello 서버 쪽 구성 요소에 대 한 로그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="5d119-362">tooretrieve 이러한 로그, 명령줄에서 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="5d119-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="5d119-363">대체 __sshuser__ hello hello 클러스터에 대 한 SSH 사용자 계정 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="5d119-364">대체 __clustername__ hello HDInsight 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="5d119-365">HDInsight에서 `scp` 및 `ssh` 사용에 대한 자세한 내용은 [HDInsight에서 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d119-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="5d119-366">여러 가지 이유로 제출이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="5d119-367">JDK 설치 되지 않았거나 hello 경로에 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="5d119-368">필요한 Java 종속성 hello 전송에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="5d119-369">종속성이 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="5d119-370">토폴로지 이름이 중복되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-370">Duplicate topology names.</span></span>

<span data-ttu-id="5d119-371">경우 hello `hdinsight-scpwebapi.out` 로그에는 `FileNotFoundException`, hello 다음 조건에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="5d119-372">hello JDK hello 개발 환경에 hello 경로에 없는 경우</span><span class="sxs-lookup"><span data-stu-id="5d119-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="5d119-373">Hello 개발 환경에 설치 된 JDK 해당 hello 확인 `%JAVA_HOME%/bin` hello 경로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="5d119-374">Java 종속성이 누락되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-374">You are missing a Java dependency.</span></span> <span data-ttu-id="5d119-375">모든 필수.jar 파일을 포함 하는 hello 전송의 일부분으로 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d119-376">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d119-376">Next steps</span></span>

<span data-ttu-id="5d119-377">Event Hubs에서 데이터를 처리하는 방법의 예는 [HDInsight의 Storm으로 Azure Event Hubs에서 이벤트 처리](hdinsight-storm-develop-csharp-event-hub-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d119-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="5d119-378">스트림 데이터를 여러 스트림으로 분할하는 C# 토폴로지의 예제는 [C# Storm 예제](https://github.com/Blackmist/csharp-storm-example)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d119-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="5d119-379">toodiscover C# 토폴로지를 만드는 방법은 참조 [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5d119-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="5d119-380">HDInsight와 자세한 방법으로 toowork 및 HDInsight 샘플에 더 많은 스톰 hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="5d119-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="5d119-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="5d119-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="5d119-382">SCP 프로그래밍 가이드</span><span class="sxs-lookup"><span data-stu-id="5d119-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="5d119-383">**HDInsight의 Apache Storm**</span><span class="sxs-lookup"><span data-stu-id="5d119-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="5d119-384">HDInsight에서 Apache Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="5d119-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="5d119-385">HDInsight의 Storm에 대한 예제 토폴로지</span><span class="sxs-lookup"><span data-stu-id="5d119-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="5d119-386">**HDInsight의 Apache Hadoop**</span><span class="sxs-lookup"><span data-stu-id="5d119-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="5d119-387">HDInsight에서 Hadoop과 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="5d119-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5d119-388">HDInsight에서 Hadoop과 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="5d119-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5d119-389">HDInsight에서 Hadoop과 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="5d119-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5d119-390">**HDInsight의 Apache HBase**</span><span class="sxs-lookup"><span data-stu-id="5d119-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="5d119-391">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="5d119-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
