---
title: "Azure HDInsight의 Hadoop 서비스에 대해 aaaEnable 힙 덤프 | Microsoft Docs"
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
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="03c1b-103">Linux 기반 HDInsight에서 Hadoop 서비스에 힙 덤프 사용</span><span class="sxs-lookup"><span data-stu-id="03c1b-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="03c1b-104">힙 덤프 hello 응용 프로그램의 메모리를 hello 변수 값을 포함 하 여 hello 덤프 생성 hello 시점에 스냅숏이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="03c1b-105">따라서 런타임에 발생하는 문제를 진단하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03c1b-106">hello이 문서의 단계 에서만 사용 가능 Linux를 사용 하는 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="03c1b-107">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="03c1b-108">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03c1b-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="03c1b-109"><a name="whichServices"></a>Services</span><span class="sxs-lookup"><span data-stu-id="03c1b-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="03c1b-110">다음 서비스는 hello에 대 한 힙 덤프를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="03c1b-111">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="03c1b-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="03c1b-112">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="03c1b-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="03c1b-113">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="03c1b-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="03c1b-114">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="03c1b-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="03c1b-115">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="03c1b-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="03c1b-116">Hello 지도 대 한 힙 덤프를 사용 하도록 설정 하 고 줄일 수도 있습니다는 HDInsight 프로세스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="03c1b-117"><a name="configuration"></a>힙 덤프 구성 이해</span><span class="sxs-lookup"><span data-stu-id="03c1b-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="03c1b-118">옵션을 전달 하 여 힙 덤프는 사용 (종종, opts으로 알려진 또는 매개 변수)는 서비스를 시작할 때 JVM toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="03c1b-119">대부분의 Hadoop 서비스에 대 한 hello 셸 사용 되는 스크립트 toostart hello 서비스 toopass 이러한 옵션을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="03c1b-120">각 스크립트에는 대 한 내보내기를  **\* \_OPTS**, hello 옵션이 포함 되어 있는 toohello JVM을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="03c1b-121">예를 들어 hello에에서 **hadoop env.sh** 스크립트로 시작 하는 hello 줄 `export HADOOP_NAMENODE_OPTS=` hello NameNode 서비스에 대 한 hello 옵션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="03c1b-122">매핑 및 줄이기 이러한 작업은 자식 프로세스의 hello MapReduce 서비스 프로세스는 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="03c1b-123">매핑하거나 줄일 각 자식 컨테이너에서 프로세스를 실행 하 고 hello JVM 옵션을 포함 하는 두 개의 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="03c1b-124">**mapred-site.xml**에 포함된 두 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="03c1b-125">**mapreduce.admin.map.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="03c1b-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="03c1b-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="03c1b-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="03c1b-127">Ambari를 사용 하 여 두 toomodify hello 스크립트 및 mapred-site.xml 설정 Ambari로 hello 클러스터의 노드에서 변경 내용 복제를 처리할 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="03c1b-128">Hello 참조 [Ambari를 사용 하 여](#using-ambari) 특정 단계에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="03c1b-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="03c1b-129">힙 덤프 사용</span><span class="sxs-lookup"><span data-stu-id="03c1b-129">Enable heap dumps</span></span>

<span data-ttu-id="03c1b-130">hello 다음 옵션을 사용 하면 힙 덤프는 OutOfMemoryError 발생할 때:</span><span class="sxs-lookup"><span data-stu-id="03c1b-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="03c1b-131">hello  **+**  이 옵션은 사용할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="03c1b-132">hello 기본값은 disabled입니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="03c1b-133">힙 덤프는 하지 사용할 수 HDInsight의 Hadoop 서비스에 대해 기본적으로 hello 덤프 파일이 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="03c1b-134">수행을 설정한 경우 해당 문제 해결을 위해 수집한 hello 덤프 파일과 문제를 재현 한 후에 hello toodisable를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="03c1b-135">덤프 위치</span><span class="sxs-lookup"><span data-stu-id="03c1b-135">Dump location</span></span>

<span data-ttu-id="03c1b-136">hello 덤프 파일에 대 한 hello 기본 위치는 hello 현재 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="03c1b-137">여기서 hello를 제어할 수 있습니다 옵션 다음 hello를 사용 하 여 파일 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="03c1b-138">예를 들어,를 사용 하 여 `-XX:HeapDumpPath=/tmp` hello 덤프 toobe hello /tmp 디렉터리에 저장 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="03c1b-139">스크립트</span><span class="sxs-lookup"><span data-stu-id="03c1b-139">Scripts</span></span>

<span data-ttu-id="03c1b-140">**OutOfMemoryError** 가 발생한 경우 스크립트를 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="03c1b-141">예를 들어 hello 오류를 확인할 수 있도록 알림을 트리거하지 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="03c1b-142">사용 하 여 hello 다음 옵션 tootrigger 스크립트에는 __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="03c1b-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="03c1b-143">Hadoop 분산된 시스템 이므로 hello 서비스에서 실행 하는 hello 클러스터의 모든 노드에 사용 되는 모든 스크립트를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="03c1b-144">hello 스크립트도 될 다른 이름으로 hello 계정 hello 서비스 실행을 통해 액세스할 수 있으며 제공 해야 하는 위치에 실행 해야 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="03c1b-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="03c1b-145">예를 들어의 toostore 스크립트 수도 `/usr/local/bin` 사용 하 여 `chmod go+rx /usr/local/bin/filename.sh` toogrant 읽기 및 실행 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="03c1b-146">Ambari 사용</span><span class="sxs-lookup"><span data-stu-id="03c1b-146">Using Ambari</span></span>

<span data-ttu-id="03c1b-147">서비스를 사용 하 여 hello 다음 단계에 대 한 toomodify hello 구성:</span><span class="sxs-lookup"><span data-stu-id="03c1b-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="03c1b-148">클러스터에 대 한 hello Ambari web UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="03c1b-149">hello URL은 https://YOURCLUSTERNAME.azurehdinsight.net입니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="03c1b-150">대화 상자가 나타나면 toohello 사이트 hello HTTP 계정 이름을 사용 하 여 인증 (기본값: 관리자) 및 클러스터에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="03c1b-151">라는 수 있다 수를 두 번째로 Ambari hello 사용자 이름 및 암호에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="03c1b-152">이 경우 입력 hello 동일한 계정 이름 및 암호</span><span class="sxs-lookup"><span data-stu-id="03c1b-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="03c1b-153">Hello 목록을 사용 하 여 hello 왼쪽에, toomodify 원하는 hello 서비스 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="03c1b-154">예를 들어 **HDFS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-154">For example, **HDFS**.</span></span> <span data-ttu-id="03c1b-155">Hello 센터 영역 선택 hello **Configs** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-155">In hello center area, select hello **Configs** tab.</span></span>

    ![HDFS Configs 탭이 선택된 Ambari 웹의 이미지](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="03c1b-157">Hello를 사용 하 여 **필터...**  항목 입력 **opts**합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="03c1b-158">이 텍스트가 포함된 항목만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-158">Only items containing this text are displayed.</span></span>

    ![필터링된 목록](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="03c1b-160">Hello  **\* \_OPTS** 에 대 한 tooenable 힙 덤프를 원하고 hello 옵션을 추가 하는 hello 서비스에 대 한 항목이 원하는 tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="03c1b-161">다음 이미지는 hello에서 추가한 `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** 항목:</span><span class="sxs-lookup"><span data-stu-id="03c1b-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![-XX가 포함된 HADOOP_NAMENODE_OPTS:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="03c1b-163">Hello에 대 한 권한 부여 힙 덤프 매핑할 하거나 자식 프로세스를 찾습니다 hello 필드 라는 **mapreduce.admin.map.child.java.opts** 및 **mapreduce.admin.reduce.child.java.opts**합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="03c1b-164">사용 하 여 hello **저장** toosave hello 변경 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="03c1b-165">Hello 변경 내용을 설명 하는 짧은 메모를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="03c1b-166">Hello 변경 내용, 적용 되 면 hello **다시 시작 필요** 하나 이상의 서비스 옆에 아이콘이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![restart required 단추 및 restart 단추](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="03c1b-168">다시 시작 해야 하는 각 서비스를 선택 하 고 hello를 사용 하 여 **서비스 작업** 너무 단추**유지 관리 모드에서 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="03c1b-169">유지 관리 모드에서 다시 시작할 때 hello 서비스에서 생성 되 고 경고를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![Turn on maintenance mode 메뉴](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="03c1b-171">Hello를 사용 하 여 유지 관리 모드를 설정한 후 **다시 시작** 너무 hello 서비스에 대 한 단추**모든 영향을 다시 시작**</span><span class="sxs-lookup"><span data-stu-id="03c1b-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![Restart All Affected 항목](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="03c1b-173">hello에 대 한 항목 hello **다시 시작** 단추는 다른 서비스에 대해 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="03c1b-174">Hello를 사용 하 여 hello 서비스를 다시 시작한 후 **서비스 작업** 너무 단추**유지 관리 모드 해제 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="03c1b-175">Hello 서비스에 대 한 경고에 대 한 모니터링이 Ambari tooresume 합니다.</span><span class="sxs-lookup"><span data-stu-id="03c1b-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

