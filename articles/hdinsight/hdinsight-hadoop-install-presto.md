---
title: "Azure HDInsight Linux 클러스터에 Presto 설치 | Microsoft Docs"
description: "스크립트 작업을 사용하여 Linux 기반 HDInsight Hadoop 클러스터에 Presto 및 Airpal을 설치하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 406ef84e72d253fec51a0b37c48f326dafd511b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="75866-103">HDInsight Hadoop 클러스터에 Presto 설치 및 사용</span><span class="sxs-lookup"><span data-stu-id="75866-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="75866-104">이 항목에서는 스크립트 작업을 사용하여 HDInsight Hadoop 클러스터에 Presto를 설치하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75866-104">In this topic, you learn how to install Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="75866-105">또한 기존 Presto HDInsight 클러스터에 Airpal을 설치하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75866-105">You also learn how to install Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75866-106">이 문서의 단계에는 Linux를 사용하는 **HDInsight 3.5 Hadoop 클러스터**가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-106">The steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="75866-107">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="75866-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="75866-108">자세한 내용은 [HDInsight 버전](hdinsight-component-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="75866-109">Presto란?</span><span class="sxs-lookup"><span data-stu-id="75866-109">What is Presto?</span></span>
<span data-ttu-id="75866-110">[Presto](https://prestodb.io/overview.html)는 빅 데이터에 대한 빠른 분산된 SQL 쿼리 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="75866-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="75866-111">Presto는 페타바이트의 데이터를 대화형으로 쿼리하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="75866-112">Presto의 구성 요소 및 작동 방법에 대한 자세한 내용은 [Presto 개념](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-112">For more information on the components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="75866-113">HDInsight 클러스터와 함께 제공된 구성 요소는 완전히 지원되며 Microsoft 지원에서 이러한 구성 요소와 관련된 문제를 해결하는 데 도움을 드릴 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75866-113">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
> 
> <span data-ttu-id="75866-114">Presto와 같은 사용자 지정 구성 요소는 문제 해결에 도움이 되는 합리적인 지원을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-114">Custom components, such as Presto, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="75866-115">지원을 통해 문제를 해결하거나 해당 기술에 대한 전문 지식이 있는, 오픈 소스 기술에 대해 사용 가능한 채널에 참여하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-115">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="75866-116">예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="75866-117">Apache 프로젝트는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="75866-117">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="75866-118">스크립트 작업을 사용하여 Presto 설치</span><span class="sxs-lookup"><span data-stu-id="75866-118">Install Presto using script action</span></span>

<span data-ttu-id="75866-119">이 섹션에서는 Azure 포털을 사용하여 새 클러스터를 만들면서 샘플 스크립트를 사용하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-119">This section provides instructions on how to use the sample script when creating a new cluster by using the Azure portal.</span></span> 

1. <span data-ttu-id="75866-120">[Linux 기반 HDInsight 클러스터 프로비전](hdinsight-hadoop-create-linux-clusters-portal.md)의 단계를 사용하여 클러스터 프로비전을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-120">Start provisioning a cluster by using the steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="75866-121">**사용자 지정** 클러스터 만들기 흐름을 사용하여 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75866-121">Make sure you create the cluster using the **Custom** cluster creation flow.</span></span> <span data-ttu-id="75866-122">만드는 클러스터가 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-122">You must ensure that the cluster you create meets the following requirements.</span></span>

    <span data-ttu-id="75866-123">a.</span><span class="sxs-lookup"><span data-stu-id="75866-123">a.</span></span> <span data-ttu-id="75866-124">HDInsight 버전 3.5를 사용하는 Hadoop 클러스터여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-124">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="75866-125">b.</span><span class="sxs-lookup"><span data-stu-id="75866-125">b.</span></span> <span data-ttu-id="75866-126">데이터 저장소로 Azure Storage를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-126">It must use Azure Storage as the data store.</span></span> <span data-ttu-id="75866-127">저장소 옵션으로 Azure Data Lake Store를 사용하는 클러스터에서 Presto 사용은 아직 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-127">Using Presto on a cluster that uses Azure Data Lake Store as the storage option is not yet supported.</span></span> 

    ![사용자 지정 옵션을 사용하여 HDInsight 클러스터 만들기](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="75866-129">**고급 설정** 블레이드에서 **스크립트 작업**을 선택하고 아래 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-129">On the **Advanced settings** blade, select **Script Actions**, and provide the information below:</span></span>
   
   * <span data-ttu-id="75866-130">**이름**: 스크립트 동작의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-130">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="75866-131">**Bash 스크립트 URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="75866-131">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="75866-132">**HEAD**: 이 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="75866-132">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="75866-133">**WORKER**: 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-133">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="75866-134">**ZOOKEEPER**: 이 확인란의 선택 취소</span><span class="sxs-lookup"><span data-stu-id="75866-134">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="75866-135">**PARAMETERS**: 이 필드는 공백으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="75866-135">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="75866-136">**스크립트 작업** 블레이드의 아래쪽에서 **선택** 단추를 클릭하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-136">At the bottom of the **Script Actions** blade, click the **Select** button to save the configuration.</span></span> <span data-ttu-id="75866-137">마지막으로 **고급 설정** 블레이드 아래쪽의 **선택** 단추를 클릭하여 구성 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-137">Finally, click  the **Select** button at the bottom of the **Advanced Settings** blade to save the configuration information.</span></span>

4. <span data-ttu-id="75866-138">[Linux 기반 HDInsight 클러스터 프로비전](hdinsight-hadoop-create-linux-clusters-portal.md)에서 설명한 대로 클러스터를 계속 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-138">Continue provisioning the cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="75866-139">Azure PowerShell, Azure CLI, HDInsight .NET SDK 또는 Azure Resource Manager 템플릿을 스크립트 동작을 적용하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-139">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="75866-140">이미 실행 중인 클러스터에도 스크립트 동작을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-140">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="75866-141">자세한 내용은 [스크립트 작업을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-141">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="75866-142">HDInsight와 함께 Presto 사용</span><span class="sxs-lookup"><span data-stu-id="75866-142">Use Presto with HDInsight</span></span>

<span data-ttu-id="75866-143">위에 설명된 단계를 사용하여 설치한 후 다음 단계를 수행하여 HDInsight 클러스터에서 Presto를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-143">Perform the following steps to use Presto in an HDInsight cluster after you have installed it using the steps described above.</span></span>

1. <span data-ttu-id="75866-144">SSH를 사용하여 HDInsight 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-144">Connect to the HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="75866-145">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="75866-146">다음 명령을 사용하여 Presto 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-146">Start the Presto shell using the following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="75866-147">모든 HDInsight 클러스터에서 기본으로 사용할 수 있는 **hivesampletable** 샘플 테이블에서 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-147">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="75866-148">기본적으로 Presto에 대한 [Hive](https://prestodb.io/docs/current/connector/hive.html) 및 [TPCH](https://prestodb.io/docs/current/connector/tpch.html) 커넥터는 이미 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-148">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="75866-149">Hive 커넥터는 기본 설치된 Hive 설치를 사용하도록 구성되므로 Hive의 모든 테이블은 Presto에 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75866-149">Hive connector is configured to use the default installed Hive installation, so all the tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="75866-150">Presto를 사용하는 방법에 대한 자세한 설명은 [Presto 설명서](https://prestodb.io/docs/current/index.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-150">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="75866-151">Presto와 함께 Airpal 사용</span><span class="sxs-lookup"><span data-stu-id="75866-151">Use Airpal with Presto</span></span>

<span data-ttu-id="75866-152">[Airpal](https://github.com/airbnb/airpal#airpal)은 Presto에 대한 오픈 소스 웹 기반 쿼리 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="75866-152">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="75866-153">Airpal에 대한 자세한 내용은 [Airpal 설명서](https://github.com/airbnb/airpal#airpal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-153">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="75866-154">이 섹션에서는 이미 설치된 Presto가 있는 HDInsight Hadoop 클러스터의 **에지 노드에 Airpal 설치**에 대한 단계를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="75866-154">In this section, we look at the steps to **install Airpal on the edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="75866-155">이렇게 하면 인터넷을 통해 Airpal 웹 쿼리 인터페이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-155">This ensures that the Airpal web query interface is available over the Internet.</span></span>

1. <span data-ttu-id="75866-156">SSH를 사용하여 Presto를 설치한 HDInsight 클러스터의 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-156">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="75866-157">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-157">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="75866-158">연결한 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-158">Once you are connected, run the following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="75866-159">다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75866-159">You should see an output like the following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="75866-160">출력에서 **값** 속성에 대한 값을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="75866-160">From the output, note the value for the **value** property.</span></span> <span data-ttu-id="75866-161">클러스터 에지 노드에 Airpal을 설치하는 동안 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-161">You will need this while installing Airpal on the cluster edgenode.</span></span> <span data-ttu-id="75866-162">위의 출력에서 필요한 값은 **10.0.0.12:9090**입니다.</span><span class="sxs-lookup"><span data-stu-id="75866-162">From the output above, the value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="75866-163">**[여기](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**의 템플릿을 사용하여 HDInsight 클러스터 에지 노드를 만들고 다음 스크린샷에 표시된 대로 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-163">Use the template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** to create an HDInsight cluster edgenode and provide the values as shown in the following screenshot.</span></span>

    ![HDInsight에서 Presto 클러스터에 Airpal 설치](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="75866-165">**구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-165">Click **Purchase**.</span></span>

6. <span data-ttu-id="75866-166">변경 내용이 클러스터 구성에 적용되면 다음 단계를 사용하여 Airpal 웹 인터페이스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-166">Once the changes are applied to the cluster configuration, you can access the Airpal web interface by using the following steps.</span></span>

    <span data-ttu-id="75866-167">a.</span><span class="sxs-lookup"><span data-stu-id="75866-167">a.</span></span> <span data-ttu-id="75866-168">클러스터 블레이드에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-168">From the cluster blade, click **Applications**.</span></span>

    ![HDInsight에서 Presto 클러스터에 Airpal 시작](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="75866-170">b.</span><span class="sxs-lookup"><span data-stu-id="75866-170">b.</span></span> <span data-ttu-id="75866-171">**설치된 앱** 블레이드에서 airpal에 대한 **포털**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-171">From the **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![HDInsight에서 Presto 클러스터에 Airpal 시작](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="75866-173">c.</span><span class="sxs-lookup"><span data-stu-id="75866-173">c.</span></span> <span data-ttu-id="75866-174">대화 상자가 나타나면 HDInsight Hadoop 클러스터를 만들 때 지정한 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-174">When prompted, enter the admin credentials that you specified while creating the HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="75866-175">HDInsight 클러스터에서 Presto 설치 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="75866-175">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="75866-176">HDInsight Hadoop 클러스터에 Presto를 설치한 후 메모리 설정 업데이트, 커넥터 변경 등과 같은 변경을 만들도록 설치를 사용자 지정할 수 있습니다. 이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-176">After you have installed Presto on an HDInsight Hadoop cluster, you can customize the installation to make changes such as update memory settings, change connectors, etc. Perform the following steps to do so.</span></span>

1. <span data-ttu-id="75866-177">SSH를 사용하여 Presto를 설치한 HDInsight 클러스터의 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-177">Using SSH, connect to the headnode of the HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="75866-178">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-178">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="75866-179">`/var/lib/presto/presto-hdinsight-master/appConfig-default.json` 파일에서 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-179">Make your configuration changes in the file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="75866-180">Presto 구성에 대한 자세한 내용은 [YARN 기반 클러스터에 대한 Presto 구성](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-180">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="75866-181">현재 실행 중인 Presto 인스턴스를 중지하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-181">Stop and kill the current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="75866-182">사용자 지정으로 Presto의 새 인스턴스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-182">Start a new instance of Presto with the customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="75866-183">새 인스턴스가 준비될 때까지 기다리고 presto 코디네이터 주소를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="75866-183">Wait for the new instance to be ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="75866-184">Presto를 실행하는 HDInsight 클러스터에 대한 벤치마크 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-184">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="75866-185">TPC-DS는 빅 데이터 시스템을 비롯한 여러 의사 결정 지원 시스템의 성능을 측정하기 위한 업계 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="75866-185">TPC-DS is the industry standard for measuring the performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="75866-186">HDInsight 클러스터에서 Presto를 사용하여 데이터를 생성하고 사용자 고유의 HDInsight 벤치마크 데이터와 비교하는 방법을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-186">You can use Presto on HDInsight clusters to generate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="75866-187">자세한 내용은 [여기](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75866-187">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="75866-188">참고 항목</span><span class="sxs-lookup"><span data-stu-id="75866-188">See also</span></span>
* <span data-ttu-id="75866-189">[HDInsight 클러스터에서 Hue 설치 및 사용](hdinsight-hadoop-hue-linux.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="75866-189">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="75866-190">Hue는 기본 저장소에서 HDInsight 클러스터를 쉽게 찾을 뿐만 아니라 Pig 및 Hive 작업을 편리하게 만들고 실행하고 저장할 수 있도록 하는 웹 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="75866-190">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="75866-191">[HDInsight 클러스터에 Giraph 설치](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="75866-191">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="75866-192">클러스터 사용자 지정을 사용하여 HDInsight Hadoop 클러스터에 Giraph를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-192">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="75866-193">Giraph를 통해 Hadoop을 사용하여 그래프 처리를 수행할 수 있으며, Azure HDInsight에서 이를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-193">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="75866-194">[HDInsight 클러스터에 Solr 설치](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="75866-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="75866-195">클러스터 사용자 지정을 사용하여 HDInsight Hadoop 클러스터에 Solr을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75866-195">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="75866-196">Solr을 사용하면 저장된 데이터에서 강력한 검색 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75866-196">Solr allows you to perform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
