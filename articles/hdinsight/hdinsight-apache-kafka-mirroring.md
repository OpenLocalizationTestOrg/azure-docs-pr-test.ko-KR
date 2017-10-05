---
title: "Apache Kafka 토픽 미러링 - Azure HDInsight | Microsoft Docs"
description: "Apache Kafka의 미러링 기능으로 보조 클러스터에 토픽을 미러링하여 HDInsight 클러스터에서 Kafka 복제본을 유지하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: e418cb01e1a9168e3662e8d6242903e052b6047b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-mirrormaker-to-replicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="b1705-103">MirrorMaker를 사용하여 HDInsight에서 Kafka와 함께 Apache Kafka 토픽 복제(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="b1705-103">Use MirrorMaker to replicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="b1705-104">Apache Kafka의 미러링 기능을 사용하여 토픽을 보조 클러스터로 복제하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-104">Learn how to use Apache Kafka's mirroring feature to replicate topics to a secondary cluster.</span></span> <span data-ttu-id="b1705-105">미러링은 연속적 프로세스로 실행되거나 한 클러스터에서 다른 클러스터로 데이터를 마이그레이션하는 방법으로 단속적으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span></span>

<span data-ttu-id="b1705-106">이 예제에서 미러링은 두 HDInsight 클러스터 간에 항목을 복제하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-106">In this example, mirroring is used to replicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="b1705-107">두 클러스터 모두 동일한 지역의 Azure Virtual Network에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-107">Both clusters are in an Azure Virtual Network in the same region.</span></span>

> [!WARNING]
> <span data-ttu-id="b1705-108">미러링이 내결함성을 달성하는 수단으로 간주되어서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-108">Mirroring should not be considered as a means to achieve fault-tolerance.</span></span> <span data-ttu-id="b1705-109">토픽 내의 항목에 대한 오프셋은 원본 및 대상 클러스터 간에 서로 다르므로 클라이언트에서는 이 두 가지를 서로 교환하여 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-109">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span></span>
>
> <span data-ttu-id="b1705-110">내결함성이 염려되는 경우 클러스터 내의 토픽에 대한 복제를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-110">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span></span> <span data-ttu-id="b1705-111">자세한 내용은 [HDInsight에서 Kafka 시작](hdinsight-apache-kafka-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1705-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="b1705-112">Kafka 미러링 작동 방식</span><span class="sxs-lookup"><span data-stu-id="b1705-112">How Kafka mirroring works</span></span>

<span data-ttu-id="b1705-113">미러링은 MirrorMaker 도구(Apache Kafka의 일부)를 사용하여 원본 클러스터의 토픽에서 레코드를 소비한 다음 대상 클러스터에 로컬 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-113">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span></span> <span data-ttu-id="b1705-114">MirrorMaker는 원본 클러스터에서 읽은 *소비자*(0개 이상)와 로컬(대상) 클러스터에 쓰는 *생산자*(1개)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-114">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span></span>

<span data-ttu-id="b1705-115">미러링 프로세스를 보여 주는 다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-115">The following diagram illustrates the Mirroring process:</span></span>

![미러링 프로세스 다이어그램](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="b1705-117">HDInsight의 Apache Kafka는 공용 인터넷을 통한 액세스를 Kafka 서비스에 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-117">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span></span> <span data-ttu-id="b1705-118">Kafka 생산자 또는 소비자는 Kafka 클러스터의 노드와 동일한 Azure 가상 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-118">Kafka producers or consumers must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="b1705-119">이 예제에서는 Kafka 원본 및 대상 클러스터가 모두 동일한 Azure 가상 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-119">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="b1705-120">클러스터 간의 통신 흐름을 보여 주는 다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-120">The following diagram shows how communication flows between the clusters:</span></span>

![Azure 가상 네트워크에 있는 원본 및 대상 Kafka 클러스터 다이어그램](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="b1705-122">원본 및 대상 클러스터는 노드와 파티션 수에 따라 다를 수 있으며 토픽 내의 오프셋도 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-122">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span></span> <span data-ttu-id="b1705-123">미러링은 분할에 사용되는 키 값을 유지하므로 레코드 순서는 키 기준으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-123">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="b1705-124">네트워크 경계를 넘은 미러링</span><span class="sxs-lookup"><span data-stu-id="b1705-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="b1705-125">다른 네트워크의 Kafka 클러스터 간에 미러링해야 하는 경우 다음과 같은 추가 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-125">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span></span>

* <span data-ttu-id="b1705-126">**게이트웨이**: 네트워크는 TCPIP 수준에서 통신할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-126">**Gateways**: The networks must be able to communicate at the TCPIP level.</span></span>

* <span data-ttu-id="b1705-127">**이름 확인**: 각 네트워크의 Kafka 클러스터는 호스트 이름을 사용하여 서로 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-127">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span></span> <span data-ttu-id="b1705-128">이렇게 하려면 요청을 다른 네트워크로 전달하도록 구성된 DNS(도메인 이름 시스템) 서버가 각 네트워크에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-128">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span></span>

    <span data-ttu-id="b1705-129">Azure Virtual Network를 만들 때 네트워크에서 제공되는 자동 DNS를 사용하는 대신 사용자 지정 DNS 서버와 해당 서버의 IP 주소를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-129">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span></span> <span data-ttu-id="b1705-130">가상 네트워크를 만든 후에는 해당 IP 주소를 사용하는 Azure Virtual Network를 만든 다음 DNS 소프트웨어를 설치하고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-130">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b1705-131">HDInsight를 Virtual Network에 설치하기 전에 사용자 지정 DNS 서버를 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-131">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span></span> <span data-ttu-id="b1705-132">Virtual Network에 구성된 DNS 서버를 사용하기 위해 HDInsight를 추가로 구성할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-132">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span></span>

<span data-ttu-id="b1705-133">두 개의 Azure Virtual Network 연결에 대한 자세한 내용은 [VNet 간 연결 구성](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1705-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="b1705-134">Kafka 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="b1705-134">Create Kafka clusters</span></span>

<span data-ttu-id="b1705-135">Azure 가상 네트워크와 Kafka 클러스터를 수동으로 만들 수 있지만 Azure Resource Manager 템플릿을 사용하는 것이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="b1705-136">다음 단계에 따라 Azure 가상 네트워크와 두 Kafka 클러스터를 Azure 구독에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-136">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="b1705-137">Azure에 로그인하고 Azure Portal에서 템플릿을 열려면 다음 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-137">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="b1705-138">Azure Resource Manager 템플릿은 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-138">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b1705-139">HDInsight에서 Kafka의 사용 가능성을 보장하려면 클러스터에 작업자 노드가 3개 이상 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="b1705-140">이 템플릿은 세 개의 작업자 노드를 포함하는 Kafka 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="b1705-141">다음 정보를 사용하여 **사용자 지정 배포** 블레이드의 항목을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-141">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
    
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="b1705-143">**리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="b1705-144">이 그룹에는 HDInsight 클러스터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-144">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="b1705-145">**위치**: 지리적으로 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-145">**Location**: Select a location geographically close to you.</span></span>
     
    * <span data-ttu-id="b1705-146">**기본 클러스터 이름**: 이 값은 Kafka 클러스터의 기본 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-146">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span></span> <span data-ttu-id="b1705-147">예를 들어 **hdi**를 입력하면 **source-hdi** 및 **dest-hdi** 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="b1705-148">**클러스터 로그인 사용자 이름**: 원본 및 대상 Kafka 클러스터의 관리자 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-148">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="b1705-149">**클러스터 로그인 암호**: 원본 및 대상 Kafka 클러스터의 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-149">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="b1705-150">**SSH 사용자 이름**: 원본 및 대상 Kafka 클러스터에 만들 SSH 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-150">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="b1705-151">**SSH 암호**: 원본 및 대상 Kafka 클러스터에 대한 SSH 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-151">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="b1705-152">**사용 약관**을 읽은 다음 **위에 명시된 사용 약관에 동의함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="b1705-153">마지막으로 **대시보드에 고정**을 선택한 다음 **구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="b1705-154">클러스터를 만드는 데 약 20분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-154">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="b1705-155">리소스를 만들면 클러스터 및 웹 대시보드를 포함하는 리소스 그룹에 대한 블레이드로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-155">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![vnet 및 클러스터에 대한 리소스 그룹 블레이드](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="b1705-157">HDInsight 클러스터의 이름은 **source-BASENAME** 및 **dest-BASENAME**입니다. 여기서 BASENAME은 템플릿에 제공된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-157">Notice that the names of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="b1705-158">이후 단계에서 클러스터에 연결할 때 이러한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-158">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="b1705-159">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="b1705-159">Create topics</span></span>

1. <span data-ttu-id="b1705-160">SSH를 사용하여 **원본** 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-160">Connect to the **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="b1705-161">**sshuser**은 클러스터를 만들 때 사용한 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-161">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="b1705-162">**BASENAME**은 클러스터를 만들 때 사용한 기본 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-162">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="b1705-163">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1705-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b1705-164">다음 명령을 사용하여 원본 클러스터에 대한 Zookeeper 호스트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-164">Use the following commands to find the Zookeeper hosts for the source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get the zookeeper hosts for the source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with the password for the cluster.

    Replace `$CLUSTERNAME` with the name of the source cluster.

3. To create a topic named `testtopic`, use the following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="b1705-165">다음 명령을 사용하여 토픽이 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-165">Use the following command to verify that the topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="b1705-166">응답에 `testtopic`이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-166">The response contains `testtopic`.</span></span>

4. <span data-ttu-id="b1705-167">다음 명령을 사용하여 이 클러스터(**원본**)에 대한 Zookeeper 호스트 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-167">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="b1705-168">이 명령은 다음 텍스트와 비슷한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-168">This returns information similar to the following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="b1705-169">이 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-169">Save this information.</span></span> <span data-ttu-id="b1705-170">해당 정보는 다음 섹션에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-170">It is used in the next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="b1705-171">미러링 구성</span><span class="sxs-lookup"><span data-stu-id="b1705-171">Configure mirroring</span></span>

1. <span data-ttu-id="b1705-172">다른 SSH 세션을 사용하여 **대상** 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-172">Connect to the **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="b1705-173">**sshuser**은 클러스터를 만들 때 사용한 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-173">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="b1705-174">**BASENAME**은 클러스터를 만들 때 사용한 기본 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-174">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="b1705-175">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1705-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b1705-176">다음 명령을 사용하여 **원본** 클러스터와 통신하는 방법을 설명하는 `consumer.properties` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-176">Use the following command to create a `consumer.properties` file that describes how to communicate with the **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="b1705-177">`consumer.properties` 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-177">Use the following text as the contents of the `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="b1705-178">**SOURCE_ZKHOSTS**를 **원본** 클러스터의 Zookeeper 호스트 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-178">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span></span>

    <span data-ttu-id="b1705-179">이 파일은 원본 Kafka 클러스터에서 읽을 때 사용할 소비자 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-179">This file describes the consumer information to use when reading from the source Kafka cluster.</span></span> <span data-ttu-id="b1705-180">소비자 구성에 대한 자세한 내용은 kafka.apache.org의 [소비자 구성](https://kafka.apache.org/documentation#consumerconfigs)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1705-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="b1705-181">파일을 저장하려면 **Ctrl + X**, **Y** 및 **Enter** 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-181">To save the file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="b1705-182">대상 클러스터와 통신하는 생산자를 구성하기 전에 **대상** 클러스터에 대한 broker 호스트를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-182">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span></span> <span data-ttu-id="b1705-183">다음 명령을 사용하여 이 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-183">Use the following commands to retrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="b1705-184">`$PASSWORD`를 클러스터에 대한 로그인 계정(관리자) 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-184">Replace `$PASSWORD` with the login account (admin) password for the cluster.</span></span>

    <span data-ttu-id="b1705-185">`$CLUSTERNAME`을 대상 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-185">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="b1705-186">이러한 명령은 다음과 비슷한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-186">These commands return information similar to the following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="b1705-187">다음을 사용하여 **대상** 클러스터와 통신하는 방법을 설명하는 `producer.properties` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-187">Use the following to create a `producer.properties` file that describes how to communicate with the **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="b1705-188">`producer.properties` 파일의 내용으로 다음 텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-188">Use the following text as the contents of the `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="b1705-189">**DEST_BROKERS**를 이전 단계의 broker 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-189">Replace **DEST_BROKERS** with the broker information from the previous step.</span></span>

    <span data-ttu-id="b1705-190">생산자 구성에 대한 자세한 내용은 kafka.apache.org의 [생산자 구성](https://kafka.apache.org/documentation#producerconfigs)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1705-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="b1705-191">MirrorMaker 시작</span><span class="sxs-lookup"><span data-stu-id="b1705-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="b1705-192">**대상** 클러스터에 대한 SSH 연결에서 다음 명령을 사용하여 MirrorMaker 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-192">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="b1705-193">이 예제에 사용된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-193">The parameters used in this example are:</span></span>

    * <span data-ttu-id="b1705-194">**--consumer.config**: 소비자 속성이 포함된 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-194">**--consumer.config**: Specifies the file that contains consumer properties.</span></span> <span data-ttu-id="b1705-195">이러한 속성은 *원본* Kafka 클러스터에서 읽는 소비자를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-195">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span></span>

    * <span data-ttu-id="b1705-196">**--producer.config**: 생산자 속성이 포함된 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-196">**--producer.config**: Specifies the file that contains producer properties.</span></span> <span data-ttu-id="b1705-197">이러한 속성은 *대상* Kafka 클러스터에 쓰는 생산자를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-197">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="b1705-198">**--whitelist**: MirrorMaker를 통해 원본 클러스터에서 대상 클러스터로 복제하는 항목의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-198">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span></span>

    * <span data-ttu-id="b1705-199">**--num.streams**: 생성할 소비자 스레드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-199">**--num.streams**: The number of consumer threads to create.</span></span>

 <span data-ttu-id="b1705-200">시작할 때 MirrorMaker는 다음 텍스트와 비슷한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-200">On startup, MirrorMaker returns information similar to the following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="b1705-201">SSH 연결부터 **원본** 클러스터까지, 다음 명령을 사용하여 Producer를 시작하고 토픽에 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-201">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="b1705-202">`$PASSWORD`를 원본 클러스터에 대한 로그인(관리자) 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-202">Replace `$PASSWORD` with the login (admin) password for the source cluster.</span></span>

    <span data-ttu-id="b1705-203">`$CLUSTERNAME`을 원본 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-203">Replace `$CLUSTERNAME` with the name of the source cluster.</span></span>

     <span data-ttu-id="b1705-204">커서로 빈 라인에 도달하면 몇 개의 텍스트 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="b1705-205">이러한 메시지는 **원본** 클러스터의 토픽으로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-205">These are sent to the topic on the **source** cluster.</span></span> <span data-ttu-id="b1705-206">완료되면 **Ctrl + C**를 클릭하여 프로듀서 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-206">When done, use **Ctrl + C** to end the producer process.</span></span>

3. <span data-ttu-id="b1705-207">**대상** 클러스터에 대한 SSH 연결에서 **Ctrl + C**를 사용하여 MirrorMaker 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-207">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span></span> <span data-ttu-id="b1705-208">그런 다음, 다음 명령을 사용하여 `testtopic` 항목이 만들어졌으며 항목의 해당 데이터가 이 미러로 복제되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-208">Then use the following commands to verify that the `testtopic` topic was created, and that data in the topic was replicated to this mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="b1705-209">`$PASSWORD`를 대상 클러스터에 대한 로그인(관리자) 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-209">Replace `$PASSWORD` with the login (admin) password for the destination cluster.</span></span>

    <span data-ttu-id="b1705-210">`$CLUSTERNAME`을 대상 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-210">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="b1705-211">이제 항목 목록에 MirrorMaster가 원본 클러스터에서 대상으로 토픽을 미러링할 때 만들어진 `testtopic`이(가) 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-211">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span></span> <span data-ttu-id="b1705-212">이 항목에서 검색한 메시지는 원본 클러스터에 입력한 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-212">The messages retrieved from the topic are the same as entered on the source cluster.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="b1705-213">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="b1705-213">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="b1705-214">이 문서의 단계를 수행하면 동일한 Azure 리소스 그룹에 두 클러스터가 모두 만들어지므로 Azure Portal에서 해당 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-214">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="b1705-215">리소스 그룹을 삭제하면 이 문서의 단계를 수행하여 만들어진 모든 리소스, Azure Virtual Network 및 클러스터에서 사용하는 저장소 계정이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-215">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1705-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1705-216">Next Steps</span></span>

<span data-ttu-id="b1705-217">이 문서에서는 MirrorMaker를 사용하여 Kafka 클러스터 복제본을 만드는 방법을 알아봤습니다.</span><span class="sxs-lookup"><span data-stu-id="b1705-217">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span></span> <span data-ttu-id="b1705-218">Kafka를 사용하는 다른 방법을 찾으려면 다음 링크를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b1705-218">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="b1705-219">[Apache Kafka MirrorMaker 문서](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330)(cwiki.apache.org)</span><span class="sxs-lookup"><span data-stu-id="b1705-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="b1705-220">HDInsight에서 Apache Kafka 시작</span><span class="sxs-lookup"><span data-stu-id="b1705-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="b1705-221">HDInsight의 Kafka에서 Apache Spark 사용</span><span class="sxs-lookup"><span data-stu-id="b1705-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="b1705-222">HDInsight의 Kafka에서 Apache Storm 사용</span><span class="sxs-lookup"><span data-stu-id="b1705-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="b1705-223">Azure Virtual Network를 통해 Kafka에 연결</span><span class="sxs-lookup"><span data-stu-id="b1705-223">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
