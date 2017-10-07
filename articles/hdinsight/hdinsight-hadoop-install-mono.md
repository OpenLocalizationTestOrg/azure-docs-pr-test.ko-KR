---
title: "aaaInstall 또는 Azure HDInsight에 모노 업데이트 | Microsoft Docs"
description: "자세한 내용은 방법 toouse HDInsight 클러스터와 모노의 특정 버전입니다. 모노는 Linux 기반 HDInsight 클러스터에서 사용 되는 toorun.NET 응용 프로그램입니다."
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
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="1174f-104">HDInsight에서 Mono 설치 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="1174f-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="1174f-105">자세한 내용은 방법 tooinstall 특정 버전의 [모노](https://www.mono-project.com) HDInsight 3.4 이상.</span><span class="sxs-lookup"><span data-stu-id="1174f-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="1174f-106">모노는 HDInsight 3.4 이상에서는 설치 된 되며 사용 되는 toorun.NET 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="1174f-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="1174f-107">각 HDInsight 버전에 포함 된 모노 길이의 hello에 대 한 정보를 참조 하십시오. [HDInsight 구성 요소 버전 관리](hdinsight-component-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="1174f-108">tooinstall 클러스터,이 문서에서 사용 하 여 hello 스크립트 동작에서 다른 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="1174f-109">작동 방법</span><span class="sxs-lookup"><span data-stu-id="1174f-109">How it works</span></span>

<span data-ttu-id="1174f-110">이 스크립트는 매개 변수 다음 hello를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="1174f-111">__모노 버전 번호__: 모노 tooinstall의 hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="1174f-112">hello 버전에서 사용할 수 있어야 [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="1174f-113">hello 스크립트 hello 다음 모노 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="1174f-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="1174f-114">__mono-complete__</span></span>

* <span data-ttu-id="1174f-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="1174f-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="1174f-116">hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="1174f-116">hello script</span></span>

<span data-ttu-id="1174f-117">__스크립트 위치__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="1174f-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="1174f-118">__요구 사항__:</span><span class="sxs-lookup"><span data-stu-id="1174f-118">__Requirements__:</span></span>

* <span data-ttu-id="1174f-119">hello에 hello 스크립트를 적용 해야 __헤드 노드__ 및 __작업자 노드__합니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="1174f-120">toouse hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="1174f-120">toouse hello script</span></span>

<span data-ttu-id="1174f-121">HDInsight 포함 하 여이 스크립트를 참조 하는 toouse 방법에 대 한 내용은 hello [스크립트 동작을 사용 하 여 사용자 지정 하는 Linux 기반 HDInsight 클러스터](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) 문서.</span><span class="sxs-lookup"><span data-stu-id="1174f-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="1174f-122">Hello Azure 포털, Azure PowerShell을 통해 hello 스크립트를 사용 하거나 Azure CLI hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="1174f-123">다음 스크립트 동작 문서 hello, 다음 URI는 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="1174f-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="1174f-124">HDInsight이 스크립트를 구성할 때 표시 hello 스크립팅 __Persisted__합니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="1174f-125">이 설정을 HDInsight tooapply 작업 크기 조정을 통해 추가 된 hello 스크립트 tooworker 노드를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1174f-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1174f-126">Next steps</span></span>

<span data-ttu-id="1174f-127">배웠습니다 어떻게 tooupgrade 하거나 HDInsight에 모노의 특정 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1174f-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="1174f-128">HDInsight의 모노.NET 응용 프로그램 사용에 대 한 자세한 내용은 hello 다음 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1174f-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="1174f-129">HDInsight의 MapReduce 스트리밍에 .NET 사용</span><span class="sxs-lookup"><span data-stu-id="1174f-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="1174f-130">HDInsight에서 Hive 및 Pig와 함께 .NET 사용</span><span class="sxs-lookup"><span data-stu-id="1174f-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="1174f-131">HDInsight에서 Storm으로 C# 솔루션 개발</span><span class="sxs-lookup"><span data-stu-id="1174f-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="1174f-132">.NET 솔루션 마이그레이션 HDInsight tooLinux 기반</span><span class="sxs-lookup"><span data-stu-id="1174f-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="1174f-133">스크립트 동작 사용에 대한 자세한 내용은 [스크립트 동작을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1174f-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>