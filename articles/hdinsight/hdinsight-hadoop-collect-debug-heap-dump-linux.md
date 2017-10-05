---
title: "HDInsight에서 Hadoop 서비스의 힙 덤프 사용 - Azure | Microsoft Docs"
description: "디버깅 및 분석을 위해 Linux 기반 HDInsight 클러스터에서 Hadoop 서비스에 힙 덤프를 사용하도록 설정합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 59942e989d622c2486edf181d76e13344c71e6f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="0edcd-103">Linux 기반 HDInsight에서 Hadoop 서비스에 힙 덤프 사용</span><span class="sxs-lookup"><span data-stu-id="0edcd-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="0edcd-104">힙 덤프는 덤프가 만들어질 당시의 변수 값을 비롯해 응용 프로그램의 메모리에 대한 스냅숏을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="0edcd-105">따라서 런타임에 발생하는 문제를 진단하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0edcd-106">이 문서의 단계는 Linux를 사용하는 HDInsight 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="0edcd-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0edcd-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0edcd-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="0edcd-109"><a name="whichServices"></a>Services</span><span class="sxs-lookup"><span data-stu-id="0edcd-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="0edcd-110">다음 서비스에 힙 덤프를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="0edcd-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="0edcd-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="0edcd-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="0edcd-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="0edcd-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="0edcd-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="0edcd-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="0edcd-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="0edcd-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="0edcd-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="0edcd-116">HDInsight에서 실행하는 map 및 reduce프로세스에 힙 덤프를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="0edcd-117"><a name="configuration"></a>힙 덤프 구성 이해</span><span class="sxs-lookup"><span data-stu-id="0edcd-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="0edcd-118">힙 덤프를 사용하려면 서비스를 시작할 때 JVM으로 옵션(opts 또는 매개 변수라고도 함)을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="0edcd-119">대부분의 Hadoop 서비스에서는 서비스를 시작하는 데 사용하는 셸 스크립트를 수정하여 이러한 옵션을 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="0edcd-120">각 스크립트에는 JVM으로 전달되는 옵션이 포함된 **\*\_OPTS**에 대한 내보내기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="0edcd-121">예를 들어 **hadoop-env.sh** 스크립트에는 `export HADOOP_NAMENODE_OPTS=`로 시작하는 줄에 NameNode 서비스에 대한 옵션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="0edcd-122">map 프로세스와 reduce 프로세스는 MapReduce 서비스의 자식 프로세스이므로 서로 약간 다른 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="0edcd-123">각 map 또는 reduce 프로세스는 자식 컨테이너에서 실행되며, JVM 옵션이 포함된 두 가지 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="0edcd-124">**mapred-site.xml**에 포함된 두 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="0edcd-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="0edcd-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="0edcd-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="0edcd-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="0edcd-127">Ambari는 클러스터의 노드 간에 변경 내용 복제를 처리하므로 Ambari를 사용하여 스크립트 및 mapred-site.xml 설정을 모두 수정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="0edcd-128">구체적인 단계는 [Ambari 사용](#using-ambari) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0edcd-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="0edcd-129">힙 덤프 사용</span><span class="sxs-lookup"><span data-stu-id="0edcd-129">Enable heap dumps</span></span>

<span data-ttu-id="0edcd-130">다음 옵션은 OutOfMemoryError가 발생한 경우 힙 덤프를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="0edcd-131">**+** 는 이 옵션이 사용하도록 설정되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="0edcd-132">기본적으로 이 옵션은 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="0edcd-133">덤프 파일은 용량이 클 수 있기 때문에 HDInsight의 Hadoop 서비스에는 기본적으로 힙 덤프가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="0edcd-134">문제 해결을 위해 사용하도록 설정한 경우에는 문제를 재현하고 덤프 파일을 수집한 후 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="0edcd-135">덤프 위치</span><span class="sxs-lookup"><span data-stu-id="0edcd-135">Dump location</span></span>

<span data-ttu-id="0edcd-136">덤프 파일의 기본 위치는 현재 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="0edcd-137">다음 옵션을 사용하여 파일이 저장되는 위치를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="0edcd-138">예를 들어 `-XX:HeapDumpPath=/tmp`를 사용하면 덤프가 /tmp 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="0edcd-139">스크립트</span><span class="sxs-lookup"><span data-stu-id="0edcd-139">Scripts</span></span>

<span data-ttu-id="0edcd-140">**OutOfMemoryError** 가 발생한 경우 스크립트를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="0edcd-141">예를 들어 오류가 발생했음을 알 수 있도록 알림을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="0edcd-142">__OutOfMemoryError__에서 스크립트를 트리거하려면 다음 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="0edcd-143">Hadoop은 분산 시스템이므로 사용되는 모든 스크립트는 서비스가 실행되는 클러스터의 모든 노드에 배치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="0edcd-144">또한 스크립트는 서비스 실행 계정에서 액세스할 수 있는 위치에 있어야 하며, 실행 권한을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="0edcd-145">예를 들어 `/usr/local/bin`에 스크립트를 저장하고 `chmod go+rx /usr/local/bin/filename.sh`를 사용하여 읽기 및 실행 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="0edcd-146">Ambari 사용</span><span class="sxs-lookup"><span data-stu-id="0edcd-146">Using Ambari</span></span>

<span data-ttu-id="0edcd-147">서비스에 대한 구성을 수정하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="0edcd-148">클러스터에 대한 Ambari 웹 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="0edcd-149">URL은 https://YOURCLUSTERNAME.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="0edcd-150">메시지가 나타나면 클러스터의 HTTP 계정 이름(기본값: admin) 및 암호를 사용하여 사이트를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0edcd-151">Ambari에서 사용자 이름 및 암호를 묻는 메시지가 다시 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="0edcd-152">이 경우 동일한 계정 이름 및 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="0edcd-153">왼쪽의 목록을 사용하여 수정할 서비스 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="0edcd-154">예를 들어 **HDFS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-154">For example, **HDFS**.</span></span> <span data-ttu-id="0edcd-155">가운데 영역에서 **Configs** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-155">In the center area, select the **Configs** tab.</span></span>

    ![HDFS Configs 탭이 선택된 Ambari 웹의 이미지](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="0edcd-157">**Filter...** 항목에 **opts**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="0edcd-158">이 텍스트가 포함된 항목만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-158">Only items containing this text are displayed.</span></span>

    ![필터링된 목록](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="0edcd-160">힙 덤프를 사용할 서비스에 대한 **\*\_OPTS** 항목을 찾아서 사용할 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="0edcd-161">다음 그림에서는 **HADOOP\_NAMENODE\_OPTS** 항목에 `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/`를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![-XX가 포함된 HADOOP_NAMENODE_OPTS:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="0edcd-163">map 또는 reduce 자식 프로세스에 힙 덤프를 사용할 경우 **mapreduce.admin.map.child.java.opts** 및 **mapreduce.admin.reduce.child.java.opts** 필드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="0edcd-164">**Save** 단추를 사용하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="0edcd-165">변경 내용을 설명하는 간단한 메모를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="0edcd-166">변경 내용이 적용되면 하나 이상의 서비스 옆에 **다시 시작 필요** 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![restart required 단추 및 restart 단추](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="0edcd-168">다시 시작해야 하는 각 서비스를 선택하고 **Service Actions** 단추를 사용하여 **Turn On Maintenance Mode**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="0edcd-169">유지 관리 모드에서는 다시 시작할 때 서비스에서 경고가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![Turn on maintenance mode 메뉴](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="0edcd-171">유지 관리 모드를 설정한 후에는 **Restart** 단추를 사용하여 서비스에 대해 **Restart All Effected**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![Restart All Affected 항목](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="0edcd-173">**Restart** 단추의 항목은 서비스마다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="0edcd-174">서비스가 다시 시작되면 **Service Actions** 단추를 사용하여 **Turn Off Maintenance Mode**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="0edcd-175">그러면 Ambari에서 서비스에 대한 경고 모니터링을 재개합니다.</span><span class="sxs-lookup"><span data-stu-id="0edcd-175">This Ambari to resume monitoring for alerts for the service.</span></span>

