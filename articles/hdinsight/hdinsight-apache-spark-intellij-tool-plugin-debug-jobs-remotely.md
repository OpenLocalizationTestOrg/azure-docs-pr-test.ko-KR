---
title: "IntelliJ용 Azure 도구 키트 - HDInsight Spark에서 원격으로 응용 프로그램 디버그 | Microsoft Docs"
description: "IntelliJ용 Azure 도구 키트의 HDInsight 도구를 사용하여 VPN을 통해 HDInsight Spark 클러스터에서 실행 중인 응용 프로그램을 원격으로 디버그하는 방법을 알아봅니다."
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
ms.openlocfilehash: 5ce282aac94d0f22ea587cbe4005819310e23b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-debug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="14cd2-103">IntelliJ용 Azure 도구 키트를 사용하여 VPN을 통해 HDInsight Spark에서 원격으로 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="14cd2-103">Use Azure Toolkit for IntelliJ to debug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="14cd2-104">ssh를 통해 원격으로 spark 응용 프로그램을 디버그하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-104">We recommend the way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="14cd2-105">자세한 내용은 [IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14cd2-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="14cd2-106">이 문서에서는 IntelliJ용 Azure 도구 키트의 HDInsight 도구를 사용하여 HDInsight Spark 클러스터에서 Spark 작업을 제출한 다음 데스크톱 컴퓨터에서 원격으로 디버그하는 방법에 대한 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="14cd2-107">이렇게 하려면 다음과 같은 개략적인 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-107">To do so, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="14cd2-108">사이트 간 또는 지점 및 사이트 간 Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="14cd2-109">이 문서의 단계에서는 사이트 간 네트워크를 사용하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-109">The steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="14cd2-110">사이트 간 Azure 가상 네트워크의 일부인 Azure HDInsight에서 Spark 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-110">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="14cd2-111">클러스터 헤드 노드 및 데스크톱 간의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-111">Verify the connectivity between the cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="14cd2-112">IntelliJ IDEA에서 Scala 응용 프로그램을 만들고 원격 디버깅을 위해 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="14cd2-113">응용 프로그램을 실행하고 디버그합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-113">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14cd2-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="14cd2-114">Prerequisites</span></span>
* <span data-ttu-id="14cd2-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="14cd2-115">An Azure subscription.</span></span> <span data-ttu-id="14cd2-116">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14cd2-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="14cd2-117">HDInsight의 Apache Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="14cd2-118">자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](hdinsight-apache-spark-jupyter-spark-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14cd2-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="14cd2-119">Oracle Java Development 키트.</span><span class="sxs-lookup"><span data-stu-id="14cd2-119">Oracle Java Development kit.</span></span> <span data-ttu-id="14cd2-120">[여기](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="14cd2-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="14cd2-121">IntelliJ IDEA.</span></span> <span data-ttu-id="14cd2-122">이 문서에서는 버전 2017.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-122">This article uses version 2017.1.</span></span> <span data-ttu-id="14cd2-123">[여기](https://www.jetbrains.com/idea/download/)에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="14cd2-124">IntelliJ용 Azure 도구 키트의 HDInsight 도구.</span><span class="sxs-lookup"><span data-stu-id="14cd2-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="14cd2-125">IntelliJ용 HDInsight 도구는 IntelliJ용 Azure 도구 키트에 포함되어 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-125">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="14cd2-126">Azure 도구 키트를 설치하는 방법에 대한 지침은 [IntelliJ용 Azure 도구 키트 설치](../azure-toolkit-for-intellij-installation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14cd2-126">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="14cd2-127">IntelliJ IDEA에서 Azure 구독에 로그인.</span><span class="sxs-lookup"><span data-stu-id="14cd2-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="14cd2-128">[여기](hdinsight-apache-spark-intellij-tool-plugin.md)에 나와 있는 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="14cd2-128">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="14cd2-129">Windows 컴퓨터에서 원격으로 디버깅하기 위해 Spark Scala 응용 프로그램을 실행하는 중에 [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356)에서 설명한 예외가 발생할 수 있습니다. 이 예외는 Windows에 WinUtils.exe가 없는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="14cd2-130">이 오류를 해결하려면 [여기서 실행 파일을 다운로드](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe)하여 **C:\WinUtils\bin** 등의 위치에 저장한 다음</span><span class="sxs-lookup"><span data-stu-id="14cd2-130">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="14cd2-131">**HADOOP_HOME** 환경 변수를 추가하고 이 변수 값을 **C\WinUtils**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-131">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="14cd2-132">1단계: Azure 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="14cd2-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="14cd2-133">아래 링크의 지침을 따라 Azure 가상 네트워크를 만든 다음 데스크톱 및 Azure 가상 네트워크 간의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-133">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="14cd2-134">Azure 포털을 사용하여 사이트 간 VPN 연결로 VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="14cd2-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="14cd2-135">PowerShell을 사용하여 사이트 간 VPN 연결로 VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="14cd2-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="14cd2-136">PowerShell을 사용하여 가상 네트워크에 지점 및 사이트 간 연결 구성</span><span class="sxs-lookup"><span data-stu-id="14cd2-136">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="14cd2-137">2단계: HDInsight Spark 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="14cd2-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="14cd2-138">또한 만든 Azure 가상 네트워크의 일부인 Azure HDInsight에서 Apache Spark 클러스터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span></span> <span data-ttu-id="14cd2-139">[HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)에서 제공되는 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-139">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="14cd2-140">선택적 구성의 일부로 이전 단계에서 만든 Azure 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-140">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a><span data-ttu-id="14cd2-141">3단계: 클러스터 헤드 노드 및 데스크톱 간의 연결 확인</span><span class="sxs-lookup"><span data-stu-id="14cd2-141">Step 3: Verify the connectivity between the cluster headnode and your desktop</span></span>
1. <span data-ttu-id="14cd2-142">헤드 노드의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-142">Get the IP address of the headnode.</span></span> <span data-ttu-id="14cd2-143">클러스터에 대한 Ambari UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-143">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="14cd2-144">클러스터 블레이드에서 **대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-144">From the cluster blade, click **Dashboard**.</span></span>

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="14cd2-146">Ambari UI의 오른쪽 위 모서리에서 **호스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-146">From the Ambari UI, from the top-right corner, click **Hosts**.</span></span>

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="14cd2-148">헤드 노드, 작업자 노드 및 zookeeper 노드 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="14cd2-149">헤드 노드는 **hn*** 접두사를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-149">The headnodes have the **hn*** prefix.</span></span> <span data-ttu-id="14cd2-150">첫 번째 헤드 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-150">Click the first headnode.</span></span>

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="14cd2-152">열리는 페이지의 아래쪽에 **요약** 상자에서 헤드 노드의 IP 주소 및 호스트 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-152">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span></span>

    ![헤드 노드 IP 찾기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="14cd2-154">헤드 노드의 IP 주소 및 호스트 이름을 Spark 작업을 실행하고 원격으로 디버그하려는 컴퓨터의 **호스트** 파일에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-154">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span></span> <span data-ttu-id="14cd2-155">이렇게 하면 IP 주소뿐만 아니라 호스트 이름을 사용하여 헤드 노드와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-155">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span></span>

   1. <span data-ttu-id="14cd2-156">관리자 권한으로 메모장을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="14cd2-157">파일 메뉴에서 **열기** 를 클릭한 다음 호스트 파일의 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-157">From the file menu, click **Open** and then navigate to the location of the hosts file.</span></span> <span data-ttu-id="14cd2-158">Windows 컴퓨터에서 `C:\Windows\System32\Drivers\etc\hosts`입니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="14cd2-159">**호스트** 파일에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-159">Add the following to the **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="14cd2-160">HDInsight 클러스터에서 사용되는 Azure 가상 네트워크에 연결된 컴퓨터에서 IP 주소뿐만 아니라 호스트 이름을 사용하여 두 헤드 노드에 ping을 실행할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-160">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span></span>
7. <span data-ttu-id="14cd2-161">[SSH를 사용하여 HDInsight 클러스터에 연결](hdinsight-hadoop-linux-use-ssh-unix.md)의 지침을 사용하여 클러스터 헤드 노드에 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-161">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="14cd2-162">클러스터 헤드 노드에서 데스크톱 컴퓨터의 IP 주소에 ping을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-162">From the cluster headnode, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="14cd2-163">컴퓨터에 할당된 두 IP 주소에 대한 연결을 테스트해야 합니다. 하나는 네트워크 연결이고 다른 하나는 컴퓨터가 연결된 Azure 가상 네트워크에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-163">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span></span>
8. <span data-ttu-id="14cd2-164">다른 헤드 노드에서도 해당 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-164">Repeat the steps for the other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="14cd2-165">4단계: IntelliJ용 Azure 도구 키트의 HDInsight 도구를 사용하여 Spark Scala 응용 프로그램 만들기 및 원격 디버깅이 가능하도록 구성</span><span class="sxs-lookup"><span data-stu-id="14cd2-165">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="14cd2-166">IntelliJ IDEA를 시작하고 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="14cd2-167">새 프로젝트 대화 상자에서 다음과 같이 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-167">In the new project dialog box, make the following choices, and then click **Next**.</span></span>

    ![Spark Scala 응용 프로그램 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="14cd2-169">왼쪽 창에서 **HDInsight**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-169">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="14cd2-170">오른쪽 창에서 **HDInsight의 Spark(Scala)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-170">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="14cd2-171">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-171">Click **Next**.</span></span>
2. <span data-ttu-id="14cd2-172">다음 창에서 다음 프로젝트 세부 정보를 제공하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-172">In the next window, provide the following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="14cd2-173">프로젝트 이름과 프로젝트 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="14cd2-174">**프로젝트 SDK**의 경우 Spark 2.x 클러스터에 Java 1.8을 사용하고 Spark 1.x 클러스터에 Java 1.7을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="14cd2-175">**Spark 버전**의 경우 Scala 프로젝트 생성 마법사는 Spark SDK 및 Scala SDK.에 대한 적절한 버전을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="14cd2-176">Spark 클러스터 2.0 이하 버전을 사용하는 경우 Spark 1.x을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-176">If the spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="14cd2-177">그렇지 않으면 Spark 2.x를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="14cd2-178">이 예제에서는 Spark 2.0.2(Scala 2.11.8)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="14cd2-179">![Spark Scala 응용 프로그램 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="14cd2-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="14cd2-180">Spark 프로젝트가 자동으로 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-180">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="14cd2-181">아티팩트를 확인하려면 이 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-181">To see the artifact, follow these steps.</span></span>

   1. <span data-ttu-id="14cd2-182">**파일** 메뉴에서 **프로젝트 구조**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-182">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="14cd2-183">**프로젝트 구조** 대화 상자에서 **아티팩트**를 클릭하여 만들어지는 기본 아티팩트를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-183">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
   <span data-ttu-id="14cd2-184">![JAR 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="14cd2-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="14cd2-185">위의 그림에서 강조 표시된 **+** 아이콘을 클릭하여 사용자 고유의 아티팩트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-185">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>

4. <span data-ttu-id="14cd2-186">프로젝트에 라이브러리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-186">Add libraries to your project.</span></span> <span data-ttu-id="14cd2-187">라이브러리를 추가하려면 프로젝트 트리에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭한 다음 **모듈 설정 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-187">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="14cd2-188">**프로젝트 구조** 대화 상자의 왼쪽 창에서 **라이브러리**, (+) 기호, **Maven에서**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-188">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span></span>

    ![라이브러리 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="14cd2-190">**Maven 리포지토리에서 라이브러리 다운로드** 대화 상자에서 다음 라이브러리를 검색하고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-190">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="14cd2-191">클러스터 헤드 노드에서 `yarn-site.xml` 및 `core-site.xml`을(를) 복사하고 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-191">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span></span> <span data-ttu-id="14cd2-192">다음 명령을 사용하여 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-192">Use the following commands to copy the files.</span></span> <span data-ttu-id="14cd2-193">[Cygwin](https://cygwin.com/install.html)을 사용하여 클러스터 헤드 노드에서 파일을 복사하도록 다음 `scp` 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-193">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="14cd2-194">데스크톱의 호스트 파일에 대한 클러스터 헤드 노드 IP 주소 및 호스트 이름을 이미 추가했으므로 다음과 같이 **scp** 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-194">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="14cd2-195">프로젝트 트리의 **/src** 폴더 아래에 복사하여 이러한 파일을 프로젝트에 추가합니다(예: `<your project directory>\src`).</span><span class="sxs-lookup"><span data-stu-id="14cd2-195">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="14cd2-196">`core-site.xml` 을(를) 업데이트하여 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-196">Update the `core-site.xml` to make the following changes.</span></span>

   1. <span data-ttu-id="14cd2-197">`core-site.xml` 은(는) 클러스터와 연결된 저장소 계정에 암호화된 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-197">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="14cd2-198">프로젝트에 추가한 `core-site.xml` 에서 암호화된 키를 기본 저장소 계정과 연결된 실제 저장소 키로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-198">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="14cd2-199">[저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14cd2-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="14cd2-200">`core-site.xml`에서 다음 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-200">Remove the following entries from the `core-site.xml`.</span></span>

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
   3. <span data-ttu-id="14cd2-201">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-201">Save the file.</span></span>
7. <span data-ttu-id="14cd2-202">응용 프로그램에 대한 기본 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-202">Add the Main class for your application.</span></span> <span data-ttu-id="14cd2-203">**프로젝트 탐색기**에서 **src**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **Scala 클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-203">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>

    ![소스 코드 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="14cd2-205">**새 Scala 클래스 만들기** 대화 상자에서 이름을 제공하고 **종류**에 대해 **개체**를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-205">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![소스 코드 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="14cd2-207">`MyClusterAppMain.scala` 파일에서 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-207">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="14cd2-208">이 코드는 Spark 컨텍스트를 만들고 `SparkSample` 개체에서 `executeJob` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-208">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span></span>

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

10. <span data-ttu-id="14cd2-209">위의 8 및 9단계를 반복하여 `SparkSample`(이)라는 새 Scala 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-209">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="14cd2-210">이 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-210">To this class add the following code.</span></span> <span data-ttu-id="14cd2-211">이 코드는 HVAC.csv(모든 HDInsight Spark 클러스터에서 사용 가능)에서 데이터를 읽고, CSV의 일곱 번째 열에 한 자리 수만 있는 행을 검색하고, 출력을 클러스터의 기본 저장 컨테이너 아래의 **/HVACOut** 에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-211">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="14cd2-212">위의 8 및 9단계를 반복하여 `RemoteClusterDebugging`(이)라는 새 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-212">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="14cd2-213">이 클래스는 응용 프로그램 디버깅에 사용되는 Spark 테스트 프레임워크를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-213">This class implements the Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="14cd2-214">`RemoteClusterDebugging` 클래스에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-214">Add the following code to the `RemoteClusterDebugging` class.</span></span>

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

     <span data-ttu-id="14cd2-215">유의해야 할 몇 가지 중요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-215">Couple of important things to note here:</span></span>

   * <span data-ttu-id="14cd2-216">`.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`의 경우 Spark 어셈블리 JAR를 지정된 경로의 클러스터 저장소에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
   * <span data-ttu-id="14cd2-217">`setJars`의 경우 아티팩트 jar를 만들 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-217">For `setJars`, specify the location where the artifact jar will be created.</span></span> <span data-ttu-id="14cd2-218">일반적으로 `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`입니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="14cd2-219">`RemoteClusterDebugging` 클래스에서 마우스 오른쪽 단추로 `test` 키워드를 클릭하고 **RemoteClusterDebugging 구성 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-219">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="14cd2-221">대화 상자에서 구성에 대한 이름을 제공하고 **테스트 이름**으로 **테스트 종류**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-221">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span></span> <span data-ttu-id="14cd2-222">기본적으로 다른 모든 값을 그대로 두고 **적용**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="14cd2-224">이제 메뉴 모음에서 **원격 실행** 구성 드롭다운이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-224">You should now see a **Remote Run** configuration drop-down in the menu bar.</span></span>

    ![원격 구성 만들기](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="14cd2-226">5단계: 디버그 모드에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="14cd2-226">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="14cd2-227">IntelliJ IDEA 프로젝트에서 `SparkSample.scala` 을(를) 열고 'val rdd1' 옆에 중단점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span></span> <span data-ttu-id="14cd2-228">중단점을 만들기 위한 팝업 메뉴에서 **함수 executeJob에서 줄**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-228">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![중단점 추가](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="14cd2-230">**원격 실행** 구성 드롭다운 옆의 **디버그 실행** 단추를 클릭하여 응용 프로그램 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-230">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span></span>

    ![디버그 모드에서 프로그램 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="14cd2-232">프로그램 실행이 중단점에 도달하면 아래 창에 **디버거** 탭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-232">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span></span>

    ![디버그 모드에서 프로그램 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="14cd2-234">(**+**) 아이콘을 클릭하여 아래 이미지에 표시된 것처럼 시계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-234">Click the (**+**) icon to add a watch as shown in the image below.</span></span>

    ![디버그 모드에서 프로그램 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="14cd2-236">여기에서 변수 `rdd1`이(가) 만들어지기 전에 응용 프로그램이 중단되기 때문에 이 시계를 사용하여 변수 `rdd`에서 첫 번째 5행이 무엇인지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-236">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span></span> <span data-ttu-id="14cd2-237">**ENTER**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-237">Press **ENTER**.</span></span>

    ![디버그 모드에서 프로그램 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="14cd2-239">위의 이미지에서 보는 것은 런타임 시이며 테라바이트의 데이터를 쿼리하고 응용 프로그램이 진행되는 방법을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-239">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="14cd2-240">예를 들어 위의 이미지에 표시된 출력에서 출력의 첫 번째 행이 헤더임을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-240">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="14cd2-241">이를 기반으로 필요한 경우 응용 프로그램 코드를 헤더 행을 건너뛰도록 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-241">Based on this, you can modify your application code to skip the header row if required.</span></span>
5. <span data-ttu-id="14cd2-242">이제 **프로그램 다시 시작** 아이콘을 클릭하여 응용 프로그램 실행을 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-242">You can now click the **Resume Program** icon to proceed with your application run.</span></span>

    ![디버그 모드에서 프로그램 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="14cd2-244">응용 프로그램이 성공적으로 완료되면 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14cd2-244">If the application completes successfully, you should see an output like the following.</span></span>

    ![디버그 모드에서 프로그램 실행](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="14cd2-246"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="14cd2-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="14cd2-247">개요: Azure HDInsight에서 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="14cd2-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="14cd2-248">데모</span><span class="sxs-lookup"><span data-stu-id="14cd2-248">Demo</span></span>
* <span data-ttu-id="14cd2-249">Scala 프로젝트 만들기(비디오): [Spark Scala 응용 프로그램 만들기](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="14cd2-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="14cd2-250">원격 디버그(비디오): [IntelliJ용 Azure 도구 키트를 사용하여 HDInsight 클러스터에서 원격으로 Spark 응용 프로그램 디버그](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="14cd2-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="14cd2-251">시나리오</span><span class="sxs-lookup"><span data-stu-id="14cd2-251">Scenarios</span></span>
* [<span data-ttu-id="14cd2-252">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="14cd2-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="14cd2-253">기계 학습과 Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="14cd2-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="14cd2-254">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="14cd2-254">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="14cd2-255">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="14cd2-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="14cd2-256">HDInsight의 Spark를 사용하여 웹 사이트 로그 분석</span><span class="sxs-lookup"><span data-stu-id="14cd2-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="14cd2-257">응용 프로그램 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="14cd2-257">Create and run applications</span></span>
* [<span data-ttu-id="14cd2-258">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="14cd2-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="14cd2-259">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="14cd2-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="14cd2-260">도구 및 확장</span><span class="sxs-lookup"><span data-stu-id="14cd2-260">Tools and extensions</span></span>
* [<span data-ttu-id="14cd2-261">IntelliJ용 Azure 도구 키트의 HDInsight 도구를 사용하여 Spark Scala 응용 프로그램 만들기 및 제출</span><span class="sxs-lookup"><span data-stu-id="14cd2-261">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="14cd2-262">IntelliJ용 Azure 도구 키트를 사용하여 SSH를 통해 원격으로 Spark 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="14cd2-262">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="14cd2-263">Hortonworks 샌드박스에서 IntelliJ용 HDInsight Tools 사용</span><span class="sxs-lookup"><span data-stu-id="14cd2-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="14cd2-264">Eclipse용 Azure 도구 키트의 HDInsight 도구를 사용하여 Spark 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="14cd2-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="14cd2-265">HDInsight에서 Spark 클러스터와 함께 Zeppelin Notebook 사용</span><span class="sxs-lookup"><span data-stu-id="14cd2-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="14cd2-266">HDInsight의 Spark 클러스터에서 Jupyter Notebook에 사용할 수 있는 커널</span><span class="sxs-lookup"><span data-stu-id="14cd2-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="14cd2-267">Jupyter 노트북에서 외부 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="14cd2-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="14cd2-268">컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="14cd2-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="14cd2-269">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="14cd2-269">Manage resources</span></span>
* [<span data-ttu-id="14cd2-270">Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="14cd2-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="14cd2-271">HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그</span><span class="sxs-lookup"><span data-stu-id="14cd2-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
