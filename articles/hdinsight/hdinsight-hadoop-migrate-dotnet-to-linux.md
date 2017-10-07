---
title: "Linux 기반 HDInsight-Azure의 Hadoop MapReduce.NET aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 toouse.NET 응용 프로그램에서 Linux 기반 HDInsight는 MapReduce 스트리밍에 대 한 합니다."
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
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="335c9-103">Windows 기반 HDInsight에 대 한.NET 솔루션을 마이그레이션하려면 HDInsight tooLinux 기반</span><span class="sxs-lookup"><span data-stu-id="335c9-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="335c9-104">Linux 기반 HDInsight 클러스터 사용 [모노 (https://mono-project.com)](https://mono-project.com) toorun.NET 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="335c9-105">모노는 toouse.NET 구성 요소를와 Linux 기반 HDInsight MapReduce 응용 프로그램과 같은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="335c9-106">이 문서에서는 Linux 기반 HDInsight의 모노와 Windows 기반 HDInsight 클러스터 toowork에 대 한 toomigrate.NET 솔루션을 생성 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="335c9-107">Mono와 .NET의 호환성</span><span class="sxs-lookup"><span data-stu-id="335c9-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="335c9-108">Mono 버전 4.2.1은 HDInsight 버전 3.5에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="335c9-109">HDInsight에 포함 된 모노 길이의 hello에 대 한 자세한 내용은 참조 하십시오. [HDInsight 구성 요소 버전](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="335c9-110">tooinstall 모노의 특정 버전 참조 hello [설치 또는 업데이트 모노](hdinsight-hadoop-install-mono.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="335c9-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="335c9-111">모노 및.NET 간의 호환성에 대 한 자세한 내용은 참조 hello [모노 호환성 (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) 문서.</span><span class="sxs-lookup"><span data-stu-id="335c9-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="335c9-112">hello SCP.NET 프레임 워크는 모노 호환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="335c9-113">모노 SCP.NET 사용에 대 한 자세한 내용은 참조 하십시오. [HDInsight의 Apache Storm의 Visual Studio를 사용 하 여 toodevelop C# 토폴로지](hdinsight-storm-develop-csharp-visual-studio-topology.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="335c9-114">자동 이식성 분석</span><span class="sxs-lookup"><span data-stu-id="335c9-114">Automated portability analysis</span></span>

<span data-ttu-id="335c9-115">hello [.NET 이식성 분석기](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) toogenerate 사용 되는 응용 프로그램 및 모노 간의 비 호환성 보고서를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="335c9-116">모노 이식성에 대 한 hello 단계 tooconfigure hello 분석기 toocheck 다음 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="335c9-117">Hello 설치 [.NET 이식성 분석기](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="335c9-118">설치 하는 동안 Visual Studio toouse의 hello 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="335c9-119">Visual Studio 2015에서 선택 __분석__ > __Portability Analyzer 설정__, 있는지 확인 하 고 __4.5__ 체크 인 hello __모노__  섹션.</span><span class="sxs-lookup"><span data-stu-id="335c9-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![4.5는 hello 분석기 설정에 대 한 모노 섹션에서 선택](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="335c9-121">선택 __확인__ toosave hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="335c9-122">__Analyze__ > __Analyze Assembly Portability__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="335c9-123">솔루션에 포함 된 hello 어셈블리를 선택한 다음 선택 __열려__ toobegin 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="335c9-124">분석이 완료되면 __Analyze__ > __View analysis reports__를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="335c9-125">__이식성 분석 결과__선택, __보고서를 열고__ tooopen 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![이식성 분석기 결과 대화 상자](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="335c9-127">hello 분석기 솔루션과 모든 문제를 catch 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="335c9-128">예를 들어의 파일 경로 `c:\temp\file.txt` 모노 Windows에서 실행 되 고 hello 경로가 해당 컨텍스트에서 유효 하기 때문에 정상으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="335c9-129">그러나 hello 경로 Linux 플랫폼에 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="335c9-130">수동 이식성 분석</span><span class="sxs-lookup"><span data-stu-id="335c9-130">Manual portability analysis</span></span>

<span data-ttu-id="335c9-131">Hello에 hello 정보를 사용 하 여 코드의 수동 감사 수행 [응용 프로그램 이식성 (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) 문서.</span><span class="sxs-lookup"><span data-stu-id="335c9-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="335c9-132">수정 및 빌드</span><span class="sxs-lookup"><span data-stu-id="335c9-132">Modify and build</span></span>

<span data-ttu-id="335c9-133">HDInsight에 대 한 Visual Studio toobuild toouse.NET 솔루션을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="335c9-134">그러나 해당 hello 프로젝트는 구성 된 toouse.NET Framework 4.5 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="335c9-135">배포 및 테스트</span><span class="sxs-lookup"><span data-stu-id="335c9-135">Deploy and test</span></span>

<span data-ttu-id="335c9-136">Hello 권장 사항을 hello.NET 이식성 분석기 또는 수동 분석에서 사용 하 여 솔루션을 수정 하면 HDInsight와 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="335c9-137">Linux 기반 HDInsight 클러스터에서 hello 솔루션 테스트 toobe 수정 해야 하는 미묘한 문제를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="335c9-138">테스트하는 동안 응용 프로그램에서 추가 기록을 활성화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="335c9-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="335c9-139">로그 액세스에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="335c9-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="335c9-140">Linux 기반 HDInsight에서 YARN 응용 프로그램 로그에 액세스</span><span class="sxs-lookup"><span data-stu-id="335c9-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="335c9-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="335c9-141">Next steps</span></span>

* [<span data-ttu-id="335c9-142">HDInsight에서 MapReduce와 함께 C# 사용</span><span class="sxs-lookup"><span data-stu-id="335c9-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="335c9-143">Hive 및 Pig과 함께 C# 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="335c9-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="335c9-144">HDInsight에서 Storm용 C# 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="335c9-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)