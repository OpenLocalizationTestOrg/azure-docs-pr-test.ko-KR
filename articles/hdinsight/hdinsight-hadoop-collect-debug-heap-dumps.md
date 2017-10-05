---
title: "힙 덤프를 사용하여 Hadoop 서비스 디버깅 및 분석 - Azure | Microsoft Docs"
description: "자동으로 Hadoop 서비스에 대한 힙 덤프를 수집하고 디버깅 및 분석을 위해 Azure Blob 저장소 계정 내부에 배치합니다."
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
ms.openlocfilehash: 6d1d4d47d279eb7a1f0bf1f587445683f0ace7a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="1ef06-103">Blob 저장소에서 힙 덤프를 수집하여 Hadoop 서비스 디버그 및 분석</span><span class="sxs-lookup"><span data-stu-id="1ef06-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="1ef06-104">힙 덤프는 덤프가 만들어질 당시의 변수 값을 비롯해 응용 프로그램의 메모리에 대한 스냅숏을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="1ef06-105">따라서 런타임에 발생하는 문제를 진단하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="1ef06-106">Hadoop 서비스의 힙 덤프가 자동으로 수집되어 사용자 Azure Blob 저장소 계정 내의 HDInsightHeapDumps/ 아래에 저장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="1ef06-107">개별 클러스터의 서비스에 대해 다양한 서비스의 힙 덤프 수집을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="1ef06-108">이 기능은 클러스터에 대해 기본적으로 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="1ef06-109">이러한 힙 덤프는 크기가 클 수 있으므로 수집을 사용하도록 설정했으면 힙 덤프가 저장되는 Blob 저장소 계정을 모니터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ef06-110">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1ef06-111">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ef06-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="1ef06-112">이 문서의 정보는 Windows 기반 HDInsight에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="1ef06-113">Linux 기반 HDInsight에 대한 자세한 내용은 [Linux 기반 HDInsight에서 Hadoop 서비스에 힙 덤프 사용](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1ef06-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="1ef06-114">힙 덤프에 적합한 서비스</span><span class="sxs-lookup"><span data-stu-id="1ef06-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="1ef06-115">다음 서비스에 힙 덤프를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="1ef06-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="1ef06-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="1ef06-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="1ef06-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="1ef06-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="1ef06-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="1ef06-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="1ef06-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="1ef06-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="1ef06-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="1ef06-121">힙 덤프를 사용하도록 설정하는 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1ef06-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="1ef06-122">서비스에 대해 힙 덤프를 설정하려면 사용자가 **service_name**에 지정된 해당 서비스의 섹션에 적절한 구성 요소를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="1ef06-123">**service_name**의 값은 여기에 나열된 tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode 또는 namenode 서비스 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-123">The value of **service_name** can be any of the services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="1ef06-124">Azure PowerShell을 사용하여 사용</span><span class="sxs-lookup"><span data-stu-id="1ef06-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="1ef06-125">예를 들어, jobhistoryserver에 대해 Azure PowerShell을 사용하여 힙 덤프를 사용 설정하려면 다음 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use the following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="1ef06-126">.NET SDK 사용하여 사용</span><span class="sxs-lookup"><span data-stu-id="1ef06-126">Enable using .NET SDK</span></span>
<span data-ttu-id="1ef06-127">예를 들어, jobhistoryserver에 대해 Azure HDInsight .NET SDK를 사용하여 힙 덤프를 사용 설정하려면 다음 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef06-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you can use the following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
