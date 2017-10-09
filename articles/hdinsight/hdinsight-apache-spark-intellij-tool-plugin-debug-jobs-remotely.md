---
title: "IntelliJ-HDInsight Spark에 원격으로 디버그 응용 프로그램에 대 한 도구 키트 aaaAzure | Microsoft Docs"
description: "자세한 내용은 방법 IntelliJ tooremotely 디버그 실행 중인 응용 프로그램 vpn 통해 HDInsight Spark 클러스터에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 합니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="b9220-103">Azure 도구 키트를 사용 하 여 VPN 통해 HDInsight Spark에 원격으로 IntelliJ toodebug 응용 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="b9220-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="b9220-104">디버깅을 통해 원격으로 spark applicaltion ssh hello 방식 으로를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="b9220-105">자세한 내용은 [IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9220-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="b9220-106">이 문서에서는 toouse IntelliJ toosubmit HDInsight Spark 클러스터에서 Spark 작업에 대 한 Azure 도구 키트의 HDInsight 도구 hello 하 고 다음 데스크톱 컴퓨터에서 원격으로 디버깅 하는 방법에 대 한 단계별 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="b9220-107">toodo hello 상위 수준 단계를 수행 해야 하는.</span><span class="sxs-lookup"><span data-stu-id="b9220-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="b9220-108">사이트 간 또는 지점 및 사이트 간 Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="b9220-109">이 문서에 hello 단계는 사이트 간 네트워크를 사용 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="b9220-110">Hello 사이트 및 사이트 간 Azure 가상 네트워크의 일부인 Azure HDInsight의 Spark 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="b9220-111">Hello hello 클러스터 헤드 노드 및 데스크톱 연결 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="b9220-112">IntelliJ IDEA에서 Scala 응용 프로그램을 만들고 원격 디버깅을 위해 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="b9220-113">실행 하 고 hello 응용 프로그램을 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9220-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b9220-114">Prerequisites</span></span>
* <span data-ttu-id="b9220-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="b9220-115">An Azure subscription.</span></span> <span data-ttu-id="b9220-116">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9220-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b9220-117">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b9220-118">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9220-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="b9220-119">Oracle Java Development 키트.</span><span class="sxs-lookup"><span data-stu-id="b9220-119">Oracle Java Development kit.</span></span> <span data-ttu-id="b9220-120">[여기](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="b9220-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b9220-121">IntelliJ IDEA.</span></span> <span data-ttu-id="b9220-122">이 문서에서는 버전 2017.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-122">This article uses version 2017.1.</span></span> <span data-ttu-id="b9220-123">[여기](https://www.jetbrains.com/idea/download/)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="b9220-124">IntelliJ용 Azure 도구 키트의 HDInsight 도구.</span><span class="sxs-lookup"><span data-stu-id="b9220-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="b9220-125">IntelliJ에 대 한 HDInsight 도구를 사용할 수 hello IntelliJ 용 Azure 도구 키트의 일환으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="b9220-126">에 대 한 지침은 어떻게 tooinstall hello Azure 도구 키트를 참조 하세요. [IntelliJ 용 Azure 도구 키트 설치 hello](../azure-toolkit-for-intellij-installation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="b9220-127">IntelliJ IDEA에서 Azure 구독에 로그인.</span><span class="sxs-lookup"><span data-stu-id="b9220-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="b9220-128">Hello 지침에 따라 [여기](hdinsight-apache-spark-intellij-tool-plugin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="b9220-129">Windows 컴퓨터에서 원격 디버깅을 위해 Spark Scala 응용 프로그램을 실행 하는 동안 발생할 수에 설명 된 대로 예외 [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) tooa 누락 인해 발생 하는 Windows에서 WinUtils.exe 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="b9220-130">이 오류를 해결 toowork를 수행 해야 [여기에서 실행 하는 hello 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa 위치 **C:\WinUtils\bin**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="b9220-131">그런 다음 환경 변수를 추가 해야 **HADOOP_HOME** 너무 hello hello 변수 값을 설정 하 고**C\WinUtils**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="b9220-132">1단계: Azure 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="b9220-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="b9220-133">아래 링크 toocreate Azure 가상 네트워크는 hello에서 hello 지침에 따라 하 고 hello 데스크톱 및 Azure 가상 네트워크 간의 hello 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="b9220-134">Azure 포털을 사용하여 사이트 간 VPN 연결로 VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="b9220-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="b9220-135">PowerShell을 사용하여 사이트 간 VPN 연결로 VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="b9220-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="b9220-136">PowerShell을 사용 하 여 지점 및 사이트 연결 tooa 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="b9220-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="b9220-137">2단계: HDInsight Spark 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b9220-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="b9220-138">또한 hello 만든 Azure 가상 네트워크의 일부인 Azure HDInsight의 Apache Spark 클러스터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="b9220-139">사용할 수 있는 hello 정보를 사용 하 여 [HDInsight에서 클러스터 만들기 Linux 기반](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="b9220-140">선택적 구성의 일부로 hello hello 이전 단계에서 만든 Azure 가상 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="b9220-141">3 단계: 클러스터 헤드 노드에 hello와 데스크톱 사이 hello 연결을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b9220-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="b9220-142">Hello 헤드 노드에의 hello IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="b9220-143">Hello 클러스터에 대 한 Ambari UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="b9220-144">Hello 클러스터 블레이드에서 클릭 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="b9220-146">Hello 오른쪽 위 모서리에서 hello Ambari UI에서에서 클릭 **호스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="b9220-148">헤드 노드, 작업자 노드 및 zookeeper 노드 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="b9220-149">hello headnodes 있는 hello **hn*** 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="b9220-150">첫 번째 헤드 노드에 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-150">Click hello first headnode.</span></span>

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="b9220-152">Hello hello에서 열리는 hello 페이지 맨 아래에 **요약** 상자의 hello 헤드 노드에 및 hello 호스트 이름을 복사 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="b9220-154">Hello IP 주소 및 hello 헤드 노드에 toohello의 hello 호스트 이름 포함 **호스트** toorun 원하는 및 hello Spark 작업을 원격으로 디버그 hello 컴퓨터에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="b9220-155">이렇게 하면 toocommunicate hello IP 주소 뿐만 아니라 hello 호스트 이름을 사용 하 여 hello 헤드 노드에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="b9220-156">관리자 권한으로 메모장을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="b9220-157">Hello 파일 메뉴에서 클릭 **열려** hello 호스트 파일의 toohello 위치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="b9220-158">Windows 컴퓨터에서 `C:\Windows\System32\Drivers\etc\hosts`입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="b9220-159">Hello toohello 다음 추가 **호스트** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="b9220-160">Toohello hello HDInsight 클러스터에서 사용 되는 Azure 가상 네트워크를 연결 하는 hello 컴퓨터에서 모두 hello headnodes hello IP 주소 뿐만 아니라 hello 호스트 이름을 사용 하 여 ping 수 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="b9220-161">Hello 지침을 사용 하 여 클러스터 헤드 노드에 hello에 대 한 SSH [SSH를 사용 하 여 연결 tooan HDInsight 클러스터](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="b9220-162">Hello 클러스터 헤드 노드에에서 hello 데스크톱 컴퓨터의 hello IP 주소를 ping 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="b9220-163">Hello 네트워크 연결에 대해 하나씩 toohello 컴퓨터를 할당 하는 연결 tooboth hello IP 주소를 테스트 해야 하 고 hello 컴퓨터 hello Azure 가상 네트워크에 대 한 다른 hello에 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="b9220-164">Hello도 다른 헤드 노드에 hello 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="b9220-165">4 단계: IntelliJ Azure 도구 키트의 hello HDInsight 도구를 사용 하 여 Spark Scala 응용 프로그램을 만들고 원격 디버깅 구성</span><span class="sxs-lookup"><span data-stu-id="b9220-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="b9220-166">IntelliJ IDEA를 시작하고 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="b9220-167">Hello 새 프로젝트 대화 상자에서 확인 클릭 및 선택 항목을 다음 hello **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Spark Scala 응용 프로그램 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="b9220-169">Hello 왼쪽된 창에서 선택 **HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="b9220-170">Hello 오른쪽 창에서 선택 **(Scala) HDInsight의 Spark**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="b9220-171">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-171">Click **Next**.</span></span>
2. <span data-ttu-id="b9220-172">Hello 다음 창의 hello 다음 프로젝트 세부 정보를 입력 한 다음 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="b9220-173">프로젝트 이름과 프로젝트 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="b9220-174">**프로젝트 SDK**의 경우 Spark 2.x 클러스터에 Java 1.8을 사용하고 Spark 1.x 클러스터에 Java 1.7을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="b9220-175">**Spark 버전**의 경우 Scala 프로젝트 생성 마법사는 Spark SDK 및 Scala SDK.에 대한 적절한 버전을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="b9220-176">더 낮은 2.0 hello spark 클러스터 버전을 사용 하는 경우 선택 1.x 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="b9220-177">그렇지 않으면 Spark 2.x를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="b9220-178">이 예제에서는 Spark 2.0.2(Scala 2.11.8)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="b9220-179">![Spark Scala 응용 프로그램 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="b9220-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="b9220-180">hello Spark 프로젝트는 자동으로 만들 아티팩트입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="b9220-181">toosee hello 아티팩트를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="b9220-182">Hello에서 **파일** 메뉴를 클릭 하 여 **프로젝트 구조**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="b9220-183">Hello에 **프로젝트 구조** 대화 상자를 클릭 **아티팩트** 만들어진 toosee hello 기본 아티팩트입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="b9220-184">![JAR 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="b9220-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="b9220-185">사용자 고유의 아티팩트를 만들 수도 있습니다 bly hello 클릭 하면  **+**  아이콘을 위 hello 이미지에서 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="b9220-186">라이브러리 tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-186">Add libraries tooyour project.</span></span> <span data-ttu-id="b9220-187">라이브러리를 tooadd hello 프로젝트 트리에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 **모듈 설정 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="b9220-188">Hello에 **프로젝트 구조** hello 왼쪽된 창에서 대화 상자를 클릭 **라이브러리**, hello (+) 기호를 클릭 하 고 클릭 **에서 Maven**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![라이브러리 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="b9220-190">Hello에 **Maven 리포지토리에서 라이브러리 다운로드** 대화 상자, 검색 및 라이브러리를 수행 하는 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="b9220-191">복사 `yarn-site.xml` 및 `core-site.xml` hello에서 toohello 프로젝트를 추가 하 고 클러스터 헤드 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="b9220-192">다음 명령은 toocopy hello 파일이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="b9220-193">사용할 수 있습니다 [Cygwin](https://cygwin.com/install.html) toorun hello 다음 `scp` hello 클러스터 headnodes에서 toocopy hello 파일 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="b9220-194">Hello 클러스터 헤드 노드에 IP 주소 및 호스트 이름은 fo hello 호스트 hello 바탕 화면에 파일을 이미 추가 했으므로 hello를 사용할 수 있습니다 **scp** hello 방식으로 다음에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="b9220-195">Hello에서 복사 하 여 이러한 파일 tooyour 프로젝트 추가 **/src** 예를 들어 프로그램 프로젝트 트리에서 폴더 `<your project directory>\src`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="b9220-196">업데이트 hello `core-site.xml` toomake hello 변경 내용을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="b9220-197">`core-site.xml`hello 클러스터와 연결 된 암호화 hello 키 toohello 저장소 계정이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="b9220-198">Hello에 `core-site.xml` toohello 프로젝트, 바꾸기 hello hello 기본 저장소 계정에 연결 된 hello 실제 저장소 키로 암호화 된 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="b9220-199">[저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9220-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="b9220-200">Hello에서 항목을 다음 hello 제거 `core-site.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="b9220-201">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-201">Save hello file.</span></span>
7. <span data-ttu-id="b9220-202">응용 프로그램에 대 한 hello 기본 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-202">Add hello Main class for your application.</span></span> <span data-ttu-id="b9220-203">Hello에서 **프로젝트 탐색기**를 마우스 오른쪽 단추로 클릭 **src**, 너무 가리킨**새로**, 클릭 하 고 **Scala 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![소스 코드 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="b9220-205">Hello에 **새 Scala 클래스 만들기** 대화 상자에서 대 한 이름을 제공 **종류** 선택 **개체**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![소스 코드 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="b9220-207">Hello에 `MyClusterAppMain.scala` 파일, 코드 다음 hello를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="b9220-208">이 코드 hello Spark 컨텍스트 연결을 만들고 시작 프로그램 `executeJob` hello 메서드에서 `SparkSample` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="b9220-209">8 단계와 9 단계 위에 새 Scala 개체 라는 tooadd 반복 `SparkSample`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="b9220-210">toothis 클래스 코드 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-210">toothis class add hello following code.</span></span> <span data-ttu-id="b9220-211">이 코드 hello HVAC.csv (모든 HDInsight Spark 클러스터에서 사용 가능)에서 hello 데이터를 읽고, hello hello CSV의에서 일곱 번째 열에 숫자를 하나만 hello 행을 검색 및 너무 hello 출력을 기록**/HVACOut** hello 기본 hello 클러스터에 대 한 저장소 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="b9220-212">8, 9 라는 새 클래스가 tooadd 위의 단계를 반복 `RemoteClusterDebugging`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="b9220-213">이 클래스는 응용 프로그램 디버깅에 사용 되는 hello Spark 테스트 프레임 워크를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="b9220-214">다음 코드 toohello hello 추가 `RemoteClusterDebugging` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="b9220-215">여기에 중요 한 사항이 toonote 몇:</span><span class="sxs-lookup"><span data-stu-id="b9220-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="b9220-216">에 대 한 `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, Spark 어셈블리 JAR hello hello 지정된 경로에 hello 클러스터 저장소에 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="b9220-217">에 대 한 `setJars`, hello 아티팩트 jar 만들어지는 hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="b9220-218">일반적으로 `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`입니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="b9220-219">Hello에 `RemoteClusterDebugging` 클래스, hello를 마우스 오른쪽 단추로 클릭 `test` 키워드와 선택 **RemoteClusterDebugging 구성 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="b9220-221">Hello 대화 상자에서 hello 구성에 대 한 이름을 입력 하 고 hello를 선택 **종류 테스트** 으로 **테스트 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="b9220-222">기본적으로 다른 모든 값을 그대로 두고 **적용**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="b9220-224">이제는 **원격 실행** 드롭 다운 hello 메뉴 모음에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="b9220-226">5 단계: hello 응용 프로그램을 디버그 모드에서 실행</span><span class="sxs-lookup"><span data-stu-id="b9220-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="b9220-227">IntelliJ 아이디어 프로젝트를 열고 `SparkSample.scala` 중단점 다음 too'val rdd1 만들고 '.</span><span class="sxs-lookup"><span data-stu-id="b9220-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="b9220-228">중단점을 만들기 위한 hello 팝업 메뉴에서 선택 **함수 executeJob에 줄**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![중단점 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="b9220-230">Hello 클릭 **실행 디버그** 단추 다음 toohello **원격 실행** 구성 드롭 다운 toostart hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="b9220-232">Hello 프로그램 실행 hello 중단점에 도달 하면 표시 됩니다는 **디버거** hello 아래쪽 창의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="b9220-234">Hello 클릭 (**+**) 아이콘 tooadd hello 이미지 아래에 나와 있는 것 처럼 감시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="b9220-236">Hello 변수 하기 전에 hello 응용 프로그램 중단 때문에 여기서 `rdd1` 를 사용 하 여 만들어진 hello 변수에서 처음 5 개 행을 hello은 무엇을 볼 수 있습니다이 조사식 `rdd`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="b9220-237">**ENTER**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-237">Press **ENTER**.</span></span>

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="b9220-239">런타임 시 데이터와 디버그 terrabytes 쿼리할 수는 위의 hello 그림에서 볼 수 있는 방법을 응용 프로그램 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="b9220-240">예를 들어 위의 hello 이미지에 표시 된 hello 출력에 나타나면 해당 hello hello 출력의 첫 번째 행은 헤더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="b9220-241">이에 따라 필요한 경우 응용 프로그램 코드 tooskip hello 머리글 행을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="b9220-242">Hello을 클릭할 수 있습니다 **Resume 프로그램** 아이콘 tooproceed와 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="b9220-244">Hello 응용 프로그램 성공적으로 완료 되 면 hello 다음과 같은 출력을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Hello 프로그램을 디버그 모드에서 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="b9220-246"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="b9220-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b9220-247">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="b9220-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="b9220-248">데모</span><span class="sxs-lookup"><span data-stu-id="b9220-248">Demo</span></span>
* <span data-ttu-id="b9220-249">Scala 프로젝트 만들기(비디오): [Spark Scala 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b9220-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="b9220-250">원격 디버그 (비디오): [HDInsight 클러스터에 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트 사용](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="b9220-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="b9220-251">시나리오</span><span class="sxs-lookup"><span data-stu-id="b9220-251">Scenarios</span></span>
* [<span data-ttu-id="b9220-252">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="b9220-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b9220-253">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="b9220-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b9220-254">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="b9220-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b9220-255">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="b9220-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b9220-256">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="b9220-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b9220-257">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="b9220-257">Create and run applications</span></span>
* [<span data-ttu-id="b9220-258">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b9220-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b9220-259">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="b9220-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b9220-260">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="b9220-260">Tools and extensions</span></span>
* [<span data-ttu-id="b9220-261">IntelliJ toocreate에 대 한 Azure 도구 키트의 HDInsight 도구를 사용 하 고 스파크 Scala 개 제출</span><span class="sxs-lookup"><span data-stu-id="b9220-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b9220-262">SSH 통해 원격으로 IntelliJ toodebug Spark 응용 프로그램에 대 한 Azure 도구 키트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="b9220-263">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="b9220-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="b9220-264">Azure Toolkit for Eclipse toocreate Spark 응용 프로그램에서에서 사용 하 여 HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="b9220-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="b9220-265">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="b9220-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b9220-266">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="b9220-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b9220-267">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="b9220-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b9220-268">Jupyter 사용자 컴퓨터에 설치 하 고 tooan HDInsight Spark 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b9220-269">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="b9220-269">Manage resources</span></span>
* [<span data-ttu-id="b9220-270">Azure HDInsight의 Apache Spark 클러스터 hello에 대 한 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9220-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b9220-271">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="b9220-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
