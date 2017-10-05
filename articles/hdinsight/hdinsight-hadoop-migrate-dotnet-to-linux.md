---
title: "Linux 기반 HDInsight - Azure에서 Hadoop MapReduce와 함께 .NET 사용 | Microsoft Docs"
description: "Linux 기반 HDInsight에서 MapReduce 스트리밍을 위해 .NET 응용 프로그램을 사용하는 방법에 대해 알아보세요."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 6ad188fb752474ff5c7d8a3fb9d609eefe8c7a9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="9cd72-103">Windows 기반 HDInsight용 .NET 솔루션을 Linux 기반 HDInsight로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="9cd72-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="9cd72-104">Linux 기반 HDInsight 클러스터는 [Mono (https://mono-project.com)](https://mono-project.com)를 사용하여 .NET 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="9cd72-105">Mono에서는 MapReduce 응용 프로그램 등의 .NET 구성 요소와 Linux 기반 HDInsight를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="9cd72-106">이 문서에서는 Linux 기반 HDInsight의 Mono와 함께 사용할 수 있도록 Windows 기반 HDInsight 클러스터용으로 만든 .NET 솔루션을 마이그레이션하는 방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="9cd72-107">Mono와 .NET의 호환성</span><span class="sxs-lookup"><span data-stu-id="9cd72-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="9cd72-108">Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="9cd72-109">HDInsight와 함께 제공되는 Mono 버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cd72-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="9cd72-110">특정 버전의 Mono를 설치하려면 [Mono 설치 또는 업데이트](hdinsight-hadoop-install-mono.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cd72-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="9cd72-111">Mono와 .NET 간 호환성에 대한 자세한 내용은 [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cd72-111">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cd72-112">SCP.NET 프레임워크는 Mono와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="9cd72-113">Mono와 함께 SCP.NET을 사용하는 방법에 대한 자세한 내용은 [Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cd72-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="9cd72-114">자동 이식성 분석</span><span class="sxs-lookup"><span data-stu-id="9cd72-114">Automated portability analysis</span></span>

<span data-ttu-id="9cd72-115">[.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)를 사용하여 응용 프로그램과 Mono 간 비호환성 보고서를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="9cd72-116">분석기를 구성하여 응용 프로그램의 Mono 이식성을 확인하려면 다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9cd72-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="9cd72-117">[.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="9cd72-118">설치 중 사용하려는 Visual Studio의 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="9cd72-119">Visual Studio 2015에서 __Analyze__ > __Portability Analyzer Settings__를 선택한 다음 __Mono__ 섹션에서 __4.5__가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![분석기 설정의 Mono 섹션에 4.5가 선택되어 있음](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="9cd72-121">__확인__을 클릭하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="9cd72-122">__Analyze__ > __Analyze Assembly Portability__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="9cd72-123">솔루션이 포함된 어셈블리를 선택한 다음 __열기__를 선택하여 분석을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="9cd72-124">분석이 완료되면 __Analyze__ > __View analysis reports__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="9cd72-125">__Portability Analysis Results__에서 __Open report__를 선택하여 보고서를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![이식성 분석기 결과 대화 상자](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="9cd72-127">분석기는 솔루션의 모든 문제를 탐지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="9cd72-128">예를 들어 `c:\temp\file.txt` 파일 경로는 Mono가 Windows에서 실행되고 경로가 해당 컨텍스트에서 유효하기 때문에 정상인 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="9cd72-129">하지만 이 경로는 Linux 플랫폼에서 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-129">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="9cd72-130">수동 이식성 분석</span><span class="sxs-lookup"><span data-stu-id="9cd72-130">Manual portability analysis</span></span>

<span data-ttu-id="9cd72-131">[응용 프로그램 이식성(http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) 문서의 정보를 사용하여 코드를 수동으로 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="9cd72-132">수정 및 빌드</span><span class="sxs-lookup"><span data-stu-id="9cd72-132">Modify and build</span></span>

<span data-ttu-id="9cd72-133">계속해서 Visual Studio를 사용하여 HDInsight를 위한 .NET 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="9cd72-134">하지만 프로젝트가 .NET Framework 4.5를 사용하도록 구성되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="9cd72-135">배포 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9cd72-135">Deploy and test</span></span>

<span data-ttu-id="9cd72-136">.NET Portability Analyzer 또는 수동 분석의 권장 사항을 사용하여 솔루션을 수정한 후에는 HDInsight로 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="9cd72-137">Linux 기반 HDInsight 클러스터에서 솔루션을 테스트할 경우 해결해야 할 사소한 문제가 발견될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="9cd72-138">테스트하는 동안 응용 프로그램에서 추가 기록을 활성화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cd72-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="9cd72-139">로그에 액세스하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cd72-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="9cd72-140">Linux 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="9cd72-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="9cd72-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cd72-141">Next steps</span></span>

* [<span data-ttu-id="9cd72-142">HDInsight에서 MapReduce와 함께 C# 사용</span><span class="sxs-lookup"><span data-stu-id="9cd72-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="9cd72-143">Hive 및 Pig과 함께 C# 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="9cd72-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="9cd72-144">HDInsight에서 Storm용 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="9cd72-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)