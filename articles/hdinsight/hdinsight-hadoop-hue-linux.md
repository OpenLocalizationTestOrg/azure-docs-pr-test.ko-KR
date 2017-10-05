---
title: "HDInsight Linux 기반 클러스터에서 Hadoop으로 Hue - Azure | Microsoft Docs"
description: "HDInsight 클러스터에서 Hue를 설치하고 터널링을 사용하여 Hue로 요청을 라우팅하는 방법을 알아봅니다. Hue를 사용하여 저장소를 찾은 후 Hive 또는 Pig를 실행합니다."
keywords: hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 41a5c652a89c85f248039fc617c84a2b6b230f56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="5528e-105">HDInsight Hadoop 클러스터에 Hue 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="5528e-105">Install and use Hue on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="5528e-106">HDInsight 클러스터에서 Hue를 설치하고 터널링을 사용하여 Hue로 요청을 라우팅하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-106">Learn how to install Hue on HDInsight clusters and use tunneling to route the requests to Hue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5528e-107">이 문서의 단계에는 Linux를 사용하는 HDInsight 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-107">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5528e-108">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5528e-109">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5528e-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-is-hue"></a><span data-ttu-id="5528e-110">Hue 정의</span><span class="sxs-lookup"><span data-stu-id="5528e-110">What is Hue?</span></span>
<span data-ttu-id="5528e-111">Hue는 Hadoop 클러스터와 상호 작용하는 데 사용되는 웹 응용 프로그램 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-111">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span> <span data-ttu-id="5528e-112">Hue를 사용하여 Hadoop 클러스터(HDInsight 클러스터의 경우, WASB)와 연결된 저장소를 찾아보고 Hive 작업 및 Pig 스크립트 등을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-112">You can use Hue to browse the storage associated with a Hadoop cluster (WASB, in the case of HDInsight clusters), run Hive jobs and Pig scripts, and so on.</span></span> <span data-ttu-id="5528e-113">HDInsight Hadoop 클러스터에서 Hue 설치는 다음 구성 요소를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-113">The following components are available with Hue installations on an HDInsight Hadoop cluster.</span></span>

* <span data-ttu-id="5528e-114">Beeswax Hive 편집기</span><span class="sxs-lookup"><span data-stu-id="5528e-114">Beeswax Hive Editor</span></span>
* <span data-ttu-id="5528e-115">Pig</span><span class="sxs-lookup"><span data-stu-id="5528e-115">Pig</span></span>
* <span data-ttu-id="5528e-116">메타스토어 관리자</span><span class="sxs-lookup"><span data-stu-id="5528e-116">Metastore manager</span></span>
* <span data-ttu-id="5528e-117">Oozie</span><span class="sxs-lookup"><span data-stu-id="5528e-117">Oozie</span></span>
* <span data-ttu-id="5528e-118">FileBrowser (WASB 기본 컨테이너로 전달)</span><span class="sxs-lookup"><span data-stu-id="5528e-118">FileBrowser (which talks to WASB default container)</span></span>
* <span data-ttu-id="5528e-119">작업 브라우저</span><span class="sxs-lookup"><span data-stu-id="5528e-119">Job Browser</span></span>

> [!WARNING]
> <span data-ttu-id="5528e-120">HDInsight 클러스터와 함께 제공된 구성 요소는 완전히 지원되며 Microsoft 지원에서 이러한 구성 요소와 관련된 문제를 해결하는 데 도움을 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-120">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="5528e-121">사용자 지정 구성 요소는 문제 해결에 도움이 되는 합리적인 지원을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-121">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="5528e-122">지원을 통해 문제를 해결하거나 해당 기술에 대한 전문 지식이 있는, 오픈 소스 기술에 대해 사용 가능한 채널에 참여하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-122">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="5528e-123">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="5528e-124">Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="5528e-124">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
>
>

## <a name="install-hue-using-script-actions"></a><span data-ttu-id="5528e-125">스크립트 동작을 사용하여 Hue 설치</span><span class="sxs-lookup"><span data-stu-id="5528e-125">Install Hue using Script Actions</span></span>

<span data-ttu-id="5528e-126">Linux 기반 HDInsight 클러스터에 Hue를 설치하는 스크립트는 https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-126">The script to install Hue on a Linux-based HDInsight cluster is available at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span> <span data-ttu-id="5528e-127">이 스크립트를 사용하여 Azure Storage Blobs(WASB) 또는 Azure Data Lake Store를 기본 스토리지로 클러스터에 Hue를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-127">You can use this script to install Hue on clusters with either Azure Storage Blobs (WASB) or Azure Data Lake Store as default storage.</span></span>

<span data-ttu-id="5528e-128">이 섹션에서는 Azure Portal을 사용하여 클러스터를 프로비전할 때 스크립트를 사용하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-128">This section provides instructions about how to use the script when provisioning the cluster using the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5528e-129">Azure PowerShell, Azure CLI, HDInsight .NET SDK 또는 Azure Resource Manager 템플릿을 스크립트 동작을 적용하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-129">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="5528e-130">이미 실행 중인 클러스터에도 스크립트 동작을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-130">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="5528e-131">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5528e-131">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
>
>

1. <span data-ttu-id="5528e-132">[Linux에서 HDInsight 클러스터 프로비전](hdinsight-hadoop-provision-linux-clusters.md)의 단계를 사용하여 클러스터 프로비전을 시작하는 한편 프로비전을 완료하지는 마세요.</span><span class="sxs-lookup"><span data-stu-id="5528e-132">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5528e-133">HDInsight 클러스터에 Hue를 설치하려면 권장 헤드 노드 크기는 A4(8개 코어, 14GB 메모리) 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-133">To install Hue on HDInsight clusters, the recommended headnode size is at least A4 (8 cores, 14 GB memory).</span></span>
   >
   >
2. <span data-ttu-id="5528e-134">**선택적 구성** 블레이드에서 **스크립트 동작**을 선택하고 아래와 같은 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-134">On the **Optional Configuration** blade, select **Script Actions**, and provide the information as shown below:</span></span>

    <span data-ttu-id="5528e-135">![색상에 대한 스크립트 작업 매개 변수 제공](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "색상에 대한 스크립트 작업 매개 변수 제공")</span><span class="sxs-lookup"><span data-stu-id="5528e-135">![Provide script action parameters for Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Provide script action parameters for Hue")</span></span>

   * <span data-ttu-id="5528e-136">**이름**: 스크립트 동작의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-136">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="5528e-137">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh</span><span class="sxs-lookup"><span data-stu-id="5528e-137">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh</span></span>
   * <span data-ttu-id="5528e-138">**HEAD**: 이 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="5528e-138">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="5528e-139">**작업자**: 이 옵션을 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-139">**WORKER**: Leave this blank.</span></span>
   * <span data-ttu-id="5528e-140">**ZOOKEEPER**: 이 옵션을 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-140">**ZOOKEEPER**: Leave this blank.</span></span>
   * <span data-ttu-id="5528e-141">**PARAMETERS**: 이 옵션을 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-141">**PARAMETERS**: Leave this blank.</span></span>
3. <span data-ttu-id="5528e-142">**스크립트 동작**의 아래 쪽에서 **선택** 단추를 사용하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-142">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="5528e-143">마지막으로 **선택적 구성** 블레이드의 아래 쪽에서 **선택** 단추를 사용하여 선택적 구성 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-143">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>
4. <span data-ttu-id="5528e-144">[Linux에서 HDInsight 클러스터 프로비전](hdinsight-hadoop-provision-linux-clusters.md)에서 설명한 대로 클러스터를 계속 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-144">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="use-hue-with-hdinsight-clusters"></a><span data-ttu-id="5528e-145">HDInsight 클러스터로 Hue 사용</span><span class="sxs-lookup"><span data-stu-id="5528e-145">Use Hue with HDInsight clusters</span></span>

<span data-ttu-id="5528e-146">SSH 터널링이 실행되면 클러스터에서 Hue를 액세스하는 유일한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-146">SSH Tunneling is the only way to access Hue on the cluster once it is running.</span></span> <span data-ttu-id="5528e-147">SSH를 통한 터널링을 사용하면 트래픽은 Hue가 실행되는 클러스터의 헤드 노드로 직접 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-147">Tunneling via SSH allows the traffic to go directly to the headnode of the cluster where Hue is running.</span></span> <span data-ttu-id="5528e-148">클러스터가 프로비전을 완료하면 다음 단계를 수행하여 HDInsight Linux 클러스터에서 Hue를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-148">After the cluster has finished provisioning, use the following steps to use Hue on an HDInsight Linux cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5528e-149">Firefox 웹 브라우저를 사용하여 아래 지침을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-149">We recommend using Firefox web browser to follow the instructions below.</span></span>
>
>

1. <span data-ttu-id="5528e-150">[SSH 터널링을 사용하여 Ambari 웹 UI, ResourceManager, JobHistory, NameNode, Oozie 및 다른 웹 UI에 액세스](hdinsight-linux-ambari-ssh-tunnel.md) 에 있는 정보를 사용하여 클라이언트 시스템에서 HDInsight 클러스터로 SSH 터널을 만들고 SSH 터널을 프록시로 사용하도록 웹 브라우저를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-150">Use the information in [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UI's](hdinsight-linux-ambari-ssh-tunnel.md) to create an SSH tunnel from your client system to the HDInsight cluster, and then configure your Web browser to use the SSH tunnel as a proxy.</span></span>

2. <span data-ttu-id="5528e-151">SSH 터널을 생성하고 이를 통해 프록시 트래픽에 대한 브라우저를 구성했으면 기본 헤드 노드의 호스트 이름을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-151">Once you have created an SSH tunnel and configured your browser to proxy traffic through it, you must find the host name of the primary head node.</span></span> <span data-ttu-id="5528e-152">포트 22에 SSH를 사용하는 클러스터에 연결하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-152">You can do this by connecting to the cluster using SSH on port 22.</span></span> <span data-ttu-id="5528e-153">예를 들어 `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`과 같으며, 여기서 **USERNAME**은 SSH 사용자 이름이고 **CLUSTERNAME**은 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-153">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` where **USERNAME** is your SSH user name and **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="5528e-154">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5528e-154">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="5528e-155">일단 연결되면 다음 명령을 사용하여 기본 헤드 노드의 정규화된 도메인 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-155">Once connected, use the following command to obtain the fully qualified domain name of the primary headnode:</span></span>

        hostname -f

    <span data-ttu-id="5528e-156">다음과 유사한 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-156">This will return a name similar to the following:</span></span>

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    <span data-ttu-id="5528e-157">Hue 웹 사이트가 위치한 기본 헤드의 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-157">This is the hostname of the primary headnode where the Hue website is located.</span></span>
4. <span data-ttu-id="5528e-158">브라우저를 사용하여 http://HOSTNAME:8888 에서 Hue 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-158">Use the browser to open the Hue portal at http://HOSTNAME:8888.</span></span> <span data-ttu-id="5528e-159">HOSTNAME을 이전 단계에서 얻은 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-159">Replace HOSTNAME with the name you obtained in the previous step.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5528e-160">처음으로 로그인할 때 Hue 포털에 로그인할 계정을 만들라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-160">When you log in for the first time, you will be prompted to create an account to log in to the Hue portal.</span></span> <span data-ttu-id="5528e-161">여기에서 지정한 자격 증명은 포털로 제한되며 클러스터를 프로비전하는 동안 지정한 관리자 또는 SSH 사용자 자격 증명과 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-161">The credentials you specify here will be limited to the portal and are not related to the admin or SSH user credentials you specified while provision the cluster.</span></span>
   >
   >

    <span data-ttu-id="5528e-162">![Hue 포털에 로그인](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "Hue 포털에 자격 증명 지정")</span><span class="sxs-lookup"><span data-stu-id="5528e-162">![Login to the Hue portal](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "Specify credentials for Hue portal")</span></span>

### <a name="run-a-hive-query"></a><span data-ttu-id="5528e-163">HIVE 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="5528e-163">Run a Hive query</span></span>
1. <span data-ttu-id="5528e-164">Hue 포털에서 **쿼리 편집기**를 클릭하고 **Hive**를 클릭하여 Hive 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-164">From the Hue portal, click **Query Editors**, and then click **Hive** to open the Hive editor.</span></span>

    <span data-ttu-id="5528e-165">![Hive 사용](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Hive 사용")</span><span class="sxs-lookup"><span data-stu-id="5528e-165">![Use Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Use Hive")</span></span>
2. <span data-ttu-id="5528e-166">**지원** 탭의 **데이터베이스**에서 **hivesampletable**이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-166">On the **Assist** tab, under **Database**, you should see **hivesampletable**.</span></span> <span data-ttu-id="5528e-167">HDInsight에서 모든 Hadoop 클러스터로 제공되는 예제 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-167">This is a sample table that is shipped with all Hadoop clusters on HDInsight.</span></span> <span data-ttu-id="5528e-168">스크린 캡처에 표시된 것처럼 오른쪽 창에서 예제 쿼리를 입력하면 **결과** 탭에서 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-168">Enter a sample query in the right pane and see the output on the **Results** tab in the pane below, as shown in the screen capture.</span></span>

    <span data-ttu-id="5528e-169">![Hive 쿼리 실행](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Hive 쿼리 실행")</span><span class="sxs-lookup"><span data-stu-id="5528e-169">![Run Hive query](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Run Hive query")</span></span>

    <span data-ttu-id="5528e-170">**차트** 탭을 사용하여 결과를 시각적으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-170">You can also use the **Chart** tab to see a visual representation of the result.</span></span>

### <a name="browse-the-cluster-storage"></a><span data-ttu-id="5528e-171">클러스터 저장소 찾아보기</span><span class="sxs-lookup"><span data-stu-id="5528e-171">Browse the cluster storage</span></span>
1. <span data-ttu-id="5528e-172">Hue 포털에서 메뉴 모음의 오른쪽 위에 있는 **파일 브라우저** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-172">From the Hue portal, click **File Browser** in the top-right corner of the menu bar.</span></span>
2. <span data-ttu-id="5528e-173">기본적으로 **/user/myuser** 디렉터리에서 파일 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-173">By default the file browser opens at the **/user/myuser** directory.</span></span> <span data-ttu-id="5528e-174">경로에서 사용자 디렉터리 바로 앞 슬래시를 클릭하여 클러스터와 연결된 Azure 저장소 컨테이너의 루트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-174">Click the forward slash right before the user directory in the path to go to the root of the Azure storage container associated with the cluster.</span></span>

    <span data-ttu-id="5528e-175">![파일 브라우저 사용](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "파일 브라우저 사용")</span><span class="sxs-lookup"><span data-stu-id="5528e-175">![Use file browser](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "Use file browser")</span></span>
3. <span data-ttu-id="5528e-176">파일 또는 폴더를 마우스 오른쪽 단추로 클릭하여 사용 가능한 작업을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5528e-176">Right-click on a file or folder to see the available operations.</span></span> <span data-ttu-id="5528e-177">오른쪽 모서리에서 **업로드** 단추를 사용하여 현재 디렉터리에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-177">Use the **Upload** button in the right corner to upload files to the current directory.</span></span> <span data-ttu-id="5528e-178">**새로 만들기** 단추를 사용하여 새 파일 또는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-178">Use the **New** button to create new files or directories.</span></span>

> [!NOTE]
> <span data-ttu-id="5528e-179">Hue 파일 브라우저는 HDInsight 클러스터와 연결된 기본 컨테이너의 콘텐츠만을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-179">The Hue file browser can only show the contents of the default container associated with the HDInsight cluster.</span></span> <span data-ttu-id="5528e-180">클러스터와 연결된 모든 추가 저장소 계정/컨테이너는 파일 브라우저를 사용하여 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-180">Any additional storage accounts/containers that you might have associated with the cluster will not be accessible using the file browser.</span></span> <span data-ttu-id="5528e-181">그러나 클러스터와 관련된 추가 컨테이너는 항상 Hive 작업에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-181">However, the additional containers associated with the cluster will always be accessible for the Hive jobs.</span></span> <span data-ttu-id="5528e-182">예를 들어 하이브 편집기에 명령 `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` 을 입력하는 경우 추가 컨테이너의 내용도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-182">For example, if you enter the command `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` in the Hive editor, you can see the contents of additional containers as well.</span></span> <span data-ttu-id="5528e-183">이 명령에서 **newcontainer** 는 클러스터와 연결된 기본 컨테이너가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-183">In this command, **newcontainer** is not the default container associated with a cluster.</span></span>
>
>

## <a name="important-considerations"></a><span data-ttu-id="5528e-184">중요 고려 사항</span><span class="sxs-lookup"><span data-stu-id="5528e-184">Important considerations</span></span>
1. <span data-ttu-id="5528e-185">Hue를 설치하는 데 사용한 스크립트는 클러스터의 기본 헤드 노드에만 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-185">The script used to install Hue installs it only on the primary headnode of the cluster.</span></span>

2. <span data-ttu-id="5528e-186">설치하는 동안 구성을 업데이트하기 위해 여러 Hadoop 서비스(HDFS, YARN, MR2, Oozie)를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-186">During installation, multiple Hadoop services (HDFS, YARN, MR2, Oozie) are restarted for updating the configuration.</span></span> <span data-ttu-id="5528e-187">스크립트가 Hue의 설치를 완료한 후에 다른 Hadoop 서비스를 시작하려면 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-187">After the script finishes installing Hue, it might take some time for other Hadoop services to start up.</span></span> <span data-ttu-id="5528e-188">처음에 Hue의 성능이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-188">This might affect Hue's performance initially.</span></span> <span data-ttu-id="5528e-189">모든 서비스를 시작하면 Hue는 완벽하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-189">Once all services start up, Hue will be fully functional.</span></span>
3. <span data-ttu-id="5528e-190">Hue는 Hive의 현재 기본값인 Tez 작업을 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-190">Hue does not understand Tez jobs, which is the current default for Hive.</span></span> <span data-ttu-id="5528e-191">MapReduce를 Hive 실행 엔진으로 사용하려는 경우 스크립트를 업데이트하여 스크립트에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-191">If you want to use MapReduce as the Hive execution engine, update the script to use the following command in your script:</span></span>

        set hive.execution.engine=mr;

4. <span data-ttu-id="5528e-192">Linux 클러스터의 경우 보조 헤드 노드에서 Resource Manager를 실행하는 반면 기본 헤드 노드에서 서비스를 실행하는 시나리오가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-192">With Linux clusters, you can have a scenario where your services are running on the primary headnode while the Resource Manager could be running on the secondary.</span></span> <span data-ttu-id="5528e-193">Hue를 사용하여 클러스터에서 실행 중인 작업의 세부 정보를 보려면  이러한 시나리오에 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-193">Such a scenario might result in errors (shown below) when using Hue to view details of RUNNING jobs on the cluster.</span></span> <span data-ttu-id="5528e-194">그러나 작업이 완료되었을 때 작업 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-194">However, you can view the job details when the job has completed.</span></span>

   <span data-ttu-id="5528e-195">![Hue 포털 오류](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Hue 포털 오류")</span><span class="sxs-lookup"><span data-stu-id="5528e-195">![Hue portal error](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Hue portal error")</span></span>

   <span data-ttu-id="5528e-196">이는 알려진 문제 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-196">This is due to a known issue.</span></span> <span data-ttu-id="5528e-197">해결 방법으로 Ambari를 수정하여 활성 Resource Manager가 기본 헤드 노드에서 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-197">As a workaround, modify Ambari so that the active Resource Manager also runs on the primary headnode.</span></span>
5. <span data-ttu-id="5528e-198">`wasb://`을 사용하여 HDInsight 클러스터가 Azure 저장소를 사용하는 동안 Hue는 WebHDFS를 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-198">Hue understands WebHDFS while HDInsight clusters use Azure Storage using `wasb://`.</span></span> <span data-ttu-id="5528e-199">따라서 스크립트 동작에 사용할 사용자 지정 스크립트는 WASB와 통신을 위한 WebHDFS와 호환 가능한 서비스인 WebWasb를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-199">So, the custom script used with script action installs WebWasb, which is a WebHDFS-compatible service for talking to WASB.</span></span> <span data-ttu-id="5528e-200">따라서 Hue 포털이 HDFS가 제대로 있다고 하더라도( **파일 브라우저**로 마우스를 이동할 때처럼) WASB로 해석되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-200">So, even though the Hue portal says HDFS in places (like when you move your mouse over the **File Browser**), it should be interpreted as WASB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5528e-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5528e-201">Next steps</span></span>
* <span data-ttu-id="5528e-202">[HDInsight 클러스터에 Giraph 설치](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5528e-202">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="5528e-203">클러스터 사용자 지정을 사용하여 HDInsight Hadoop 클러스터에 Giraph를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-203">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5528e-204">Giraph를 통해 Hadoop을 사용하여 그래프 처리를 수행할 수 있으며, Azure HDInsight에서 이를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-204">Giraph allows you to perform graph processing using Hadoop, and it can be used with Azure HDInsight.</span></span>
* <span data-ttu-id="5528e-205">[HDInsight 클러스터에 Solr 설치](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5528e-205">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="5528e-206">클러스터 사용자 지정을 사용하여 HDInsight Hadoop 클러스터에 Solr을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-206">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5528e-207">Solr을 사용하면 저장된 데이터에서 강력한 검색 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-207">Solr allows you to perform powerful search operations on stored data.</span></span>
* <span data-ttu-id="5528e-208">[HDInsight 클러스터에 R 설치](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5528e-208">[Install R on HDInsight clusters](hdinsight-hadoop-r-scripts-linux.md).</span></span> <span data-ttu-id="5528e-209">클러스터 사용자 지정을 사용하여 HDInsight Hadoop 클러스터에서 R을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-209">Use cluster customization to install R on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5528e-210">R은 통계 계산을 위한 오픈 소스 언어 및 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-210">R is an open-source language and environment for statistical computing.</span></span> <span data-ttu-id="5528e-211">수백 개의 기본 제공 통계 함수와 기능 및 개체 지향 프로그래밍의 측면을 결합하는 고유한 프로그래밍 언어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-211">It provides hundreds of built-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="5528e-212">또한 광범위한 그래픽 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5528e-212">It also provides extensive graphical capabilities.</span></span>

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
