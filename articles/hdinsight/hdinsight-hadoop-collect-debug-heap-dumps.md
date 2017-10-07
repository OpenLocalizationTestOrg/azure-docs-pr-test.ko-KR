---
title: "aaaDebug 및 힙 덤프-Azure 사용 하 여 Hadoop 서비스를 분석 | Microsoft Docs"
description: "자동으로 Hadoop 서비스에 대 한 힙 덤프를 수집 하 고 hello 디버깅 및 분석을 위해 Azure Blob 저장소 계정 내에 배치 합니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="0adf3-103">Blob 저장소 toodebug에 힙 덤프를 수집 하 고 Hadoop 서비스를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="0adf3-104">힙 덤프 hello 응용 프로그램의 메모리를 hello 변수 값을 포함 하 여 hello 덤프 생성 hello 시점에 스냅숏이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="0adf3-105">따라서 런타임에 발생하는 문제를 진단하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="0adf3-106">힙 덤프를 자동으로 Hadoop 서비스에 대해 수집 하 고 hello HDInsightHeapDumps 아래의 사용자의 Azure Blob 저장소 계정 내에 배치 수 / 합니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="0adf3-107">다양 한 서비스에 대 한 힙 덤프의 hello 컬렉션의 개별 클러스터 서비스에 대해 활성화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="0adf3-108">이 기능에 대 한 hello 기본값 꺼져 toobe 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="0adf3-109">이러한 힙 덤프 하므로 권장 toomonitor hello Blob 저장소 계정 되 고 저장 위치 hello 컬렉션이 활성화 된 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0adf3-110">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0adf3-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0adf3-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="0adf3-112">이 문서의 정보 hello에 tooWindows 기반 HDInsight만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="0adf3-113">Linux 기반 HDInsight에 대한 자세한 내용은 [Linux 기반 HDInsight에서 Hadoop 서비스에 힙 덤프 사용](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="0adf3-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="0adf3-114">힙 덤프에 적합한 서비스</span><span class="sxs-lookup"><span data-stu-id="0adf3-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="0adf3-115">다음 서비스는 hello에 대 한 힙 덤프를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="0adf3-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="0adf3-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="0adf3-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="0adf3-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="0adf3-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="0adf3-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="0adf3-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="0adf3-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="0adf3-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="0adf3-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="0adf3-121">힙 덤프를 사용하도록 설정하는 구성 요소</span><span class="sxs-lookup"><span data-stu-id="0adf3-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="0adf3-122">으로 지정 되는 해당 서비스에 대 한 hello 섹션에 있는 tooset hello 적절 한 구성 요소를 필요에 서비스에 대 한 덤프를 힙 tooturn, **service_name**합니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="0adf3-123">값을 hello **service_name** 여기에 나열 된 hello 서비스 중 하나일 수 있습니다: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, 또는 namenode 합니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="0adf3-124">Azure PowerShell을 사용하여 사용</span><span class="sxs-lookup"><span data-stu-id="0adf3-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="0adf3-125">예를 들어 jobhistoryserver 용 Azure PowerShell을 사용 하 여 힙 덤프에 tooturn, hello 다음 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="0adf3-126">.NET SDK 사용하여 사용</span><span class="sxs-lookup"><span data-stu-id="0adf3-126">Enable using .NET SDK</span></span>
<span data-ttu-id="0adf3-127">예를 들어 jobhistoryserver 용 hello Azure HDInsight.NET SDK를 사용 하 여 힙 덤프에 tooturn, 코드 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0adf3-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
