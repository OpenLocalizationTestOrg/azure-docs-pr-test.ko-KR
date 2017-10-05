---
title: "HDInsight에서 Mono 설치 또는 업데이트 - Azure | Microsoft Docs"
description: "HDInsight 클러스터에서 특정 버전의 Mono를 사용하는 방법을 알아봅니다. Mono는 Linux 기반 HDInsight 클러스터에서 .NET 응용 프로그램을 실행하는 데 사용됩니다."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: fd284542e1de65f323f1e3a092689f847e025be6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="684f2-104">HDInsight에서 Mono 설치 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="684f2-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="684f2-105">HDInsight 3.4 이상에서 특정 버전의 [Mono](https://www.mono-project.com)를 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-105">Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="684f2-106">Mono는 HDInsight 3.4 이상에서 설치되고 .NET 응용 프로그램을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-106">Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications.</span></span> <span data-ttu-id="684f2-107">각 HDInsight 버전에 포함된 Mono 버전에 대한 자세한 내용은 [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="684f2-107">For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="684f2-108">클러스터에서 다른 버전을 설치하려면 이 문서의 스크립트 동작을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-108">To install a different version on your cluster, use the script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="684f2-109">작동 방법</span><span class="sxs-lookup"><span data-stu-id="684f2-109">How it works</span></span>

<span data-ttu-id="684f2-110">이 스크립트는 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-110">This script accepts the following parameter:</span></span>

* <span data-ttu-id="684f2-111">__Mono 버전 번호__: 설치할 Mono의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-111">__Mono version number__: The version of Mono to install.</span></span> <span data-ttu-id="684f2-112">이 버전은 [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-112">The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="684f2-113">스크립트는 다음 Mono 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-113">The script installs the following Mono packages:</span></span>

* <span data-ttu-id="684f2-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="684f2-114">__mono-complete__</span></span>

* <span data-ttu-id="684f2-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="684f2-115">__ca-certificates-mono__</span></span>

## <a name="the-script"></a><span data-ttu-id="684f2-116">스크립트</span><span class="sxs-lookup"><span data-stu-id="684f2-116">The script</span></span>

<span data-ttu-id="684f2-117">__스크립트 위치__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="684f2-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="684f2-118">__요구 사항__:</span><span class="sxs-lookup"><span data-stu-id="684f2-118">__Requirements__:</span></span>

* <span data-ttu-id="684f2-119">스크립트는 __헤드 노드__ 및 __작업자 노드__에 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-119">The script must be applied on the __head nodes__ and __worker nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="684f2-120">스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="684f2-120">To use the script</span></span>

<span data-ttu-id="684f2-121">HDInsight에서 이 스크립트를 사용하는 방법에 대한 자세한 내용은 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="684f2-121">For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="684f2-122">Azure Portal, Azure PowerShell 또는 Azure CLI에서 이 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-122">You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="684f2-123">스크립트 동작 문서를 진행하는 동안 다음 URI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-123">While following the script action document, use the following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="684f2-124">이 스크립트로 HDInsight를 구성할 때 스크립트를 __Persisted__로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-124">When configuring HDInsight with this script, mark the script as __Persisted__.</span></span> <span data-ttu-id="684f2-125">이 설정을 사용하면 HDInsight에서 해당 스크립트가 크기 조정 작업을 통해 추가된 작업자 노드에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-125">This setting allows HDInsight to apply the script to worker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="684f2-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="684f2-126">Next steps</span></span>

<span data-ttu-id="684f2-127">HDInsight에서 특정 버전의 Mono를 업그레이드하거나 설치하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="684f2-127">You have learned how to upgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="684f2-128">HDInsight의 Mono에서 .NET 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="684f2-128">For more information on using .NET applications with Mono on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="684f2-129">HDInsight의 MapReduce 스트리밍에 .NET 사용</span><span class="sxs-lookup"><span data-stu-id="684f2-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="684f2-130">HDInsight에서 Hive 및 Pig와 함께 .NET 사용</span><span class="sxs-lookup"><span data-stu-id="684f2-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="684f2-131">HDInsight에서 Storm으로 C# 솔루션 개발</span><span class="sxs-lookup"><span data-stu-id="684f2-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="684f2-132">Linux 기반 HDInsight로 .NET 솔루션 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="684f2-132">Migrate .NET solutions to Linux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="684f2-133">스크립트 동작 사용에 대한 자세한 내용은 [스크립트 동작을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="684f2-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>