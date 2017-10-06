---
title: "aaaMirror Apache Kafka 항목-Azure HDInsight | Microsoft Docs"
description: "어떻게 toouse Apache Kafka 미러링 항목 tooa 보조 클러스터 미러링 여 toomaintain HDInsight 클러스터에서 Kafka의 복제 기능에 대해 알아봅니다."
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
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="655be-103">HDInsight (미리 보기)의 Kafka MirrorMaker tooreplicate Apache Kafka 항목 사용</span><span class="sxs-lookup"><span data-stu-id="655be-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="655be-104">Apache Kafka toouse 서버의 기능 tooreplicate 항목 tooa 보조 클러스터를 미러링 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="655be-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="655be-105">미러링 연속 되는 프로세스를 실행 하거나 사용할 수 간헐적으로 마이그레이션하는 방법으로 하나의 데이터를 tooanother를 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="655be-106">이 예제에서는 미러링은 두 HDInsight 클러스터 간에 사용 되는 tooreplicate 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="655be-107">Hello에 Azure 가상 네트워크에 있는 두 클러스터의 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="655be-108">미러링 수단 tooachieve 결함 허용으로 간주 되지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="655be-109">항목 내 오프셋된 tooitems hello hello 원본 및 대상 클러스터 간에 서로 다른 되므로 클라이언트는 두 개의 hello를 바꿔서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="655be-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="655be-110">내결함성 유지 하려는 경우에 클러스터 내에서 hello 항목에 대 한 복제를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="655be-111">자세한 내용은 [HDInsight에서 Kafka 시작](hdinsight-apache-kafka-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="655be-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="655be-112">Kafka 미러링 작동 방식</span><span class="sxs-lookup"><span data-stu-id="655be-112">How Kafka mirroring works</span></span>

<span data-ttu-id="655be-113">Hello MirrorMaker 도구 (Apache Kafka의 일부) tooconsume를 사용 하 여 미러링 작동 hello 원본 클러스터에 대 한 항목을 기록 하 고 hello 대상 클러스터에 로컬 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="655be-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="655be-114">MirrorMaker 하나 (이상)에 사용 하 여 *소비자* hello 원본 클러스터에서 읽은 및 *생산자* toohello 로컬 (대상) 클러스터를 작성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="655be-115">다음 다이어그램 hello hello 미러링 프로세스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="655be-115">hello following diagram illustrates hello Mirroring process:</span></span>

![미러링 프로세스 hello의 다이어그램](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="655be-117">HDInsight의 Apache Kafka hello를 통해 액세스 toohello Kafka 서비스를 제공 하지 않습니다 공용 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="655be-118">Hello에 Kafka 생산자 또는 소비자 있어야 hello Kafka 클러스터에서에서 노드 hello와 동일한 Azure 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="655be-119">이 예제에서는 hello Kafka 소스와 대상 클러스터는 Azure 가상 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="655be-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="655be-120">hello 다음 그림에 hello 클러스터 간의 통신 흐름 방식을:</span><span class="sxs-lookup"><span data-stu-id="655be-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Azure 가상 네트워크에 있는 원본 및 대상 Kafka 클러스터 다이어그램](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="655be-122">hello 원본 및 대상 클러스터의 노드 및 파티션 hello 번호에 서로 다를 수와 hello 항목 내의 오프셋 서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="655be-123">미러링 키 당 별로 레코드 순서는 유지 되므로 hello 키 값을 분할에 사용 되는 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="655be-124">네트워크 경계를 넘은 미러링</span><span class="sxs-lookup"><span data-stu-id="655be-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="655be-125">서로 다른 네트워크에 Kafka 클러스터 간의 toomirror 해야 할 경우 다음 추가 고려 사항 hello 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="655be-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="655be-126">**게이트웨이**: hello 네트워크 수 toocommunicate hello TCPIP 수준에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="655be-127">**이름 확인**: hello Kafka 각 네트워크에서 클러스터 호스트 이름을 사용 하 여 다른 수 tooconnect tooeach 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="655be-128">이 각 네트워크의 도메인 이름 (DNS System) 서버 tooforward 요청 toohello 다른 네트워크를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="655be-129">Hello 네트워크와 함께 제공 된 자동 DNS hello를 사용 하는 대신 Azure 가상 네트워크를 만들 때 사용자 지정 DNS 서버 및 hello IP 주소를 hello 서버를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="655be-130">가상 네트워크를 만든 hello, 후 있습니다 다음 해당 IP 주소를 사용 하는 Azure 가상 컴퓨터를 만드는 다음 설치 및 구성 해야 DNS 소프트웨어에 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="655be-131">만들고 HDInsight hello 가상 네트워크에 설치 하기 전에 hello 사용자 지정 DNS 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="655be-132">HDInsight toouse hello DNS 서버 hello 가상 네트워크에 대해 구성 하는 데 필요한 추가 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="655be-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="655be-133">두 개의 Azure Virtual Network 연결에 대한 자세한 내용은 [VNet 간 연결 구성](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="655be-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="655be-134">Kafka 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="655be-134">Create Kafka clusters</span></span>

<span data-ttu-id="655be-135">Azure 가상 네트워크를 만들고 Kafka 수동으로 클러스터를 보다 쉽게 toouse Azure 리소스 관리자 템플릿을.</span><span class="sxs-lookup"><span data-stu-id="655be-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="655be-136">다음 단계 toodeploy hello를 사용 하 여 Azure 가상 네트워크 및 두 개의 Kafka 클러스터 tooyour Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="655be-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="655be-137">Hello tooAzure에서 단추 toosign 및 hello Azure 포털에서에서 열기 hello 서식 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="655be-138">hello Azure 리소스 관리자 템플릿에 위치한 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="655be-139">HDInsight의 Kafka의 tooguarantee 가용성, 클러스터 3 개 이상의 작업자 노드를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="655be-140">이 템플릿은 세 개의 작업자 노드를 포함하는 Kafka 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="655be-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="655be-141">정보 toopopulate hello 항목에 나오는 hello에 사용 하 여 hello **사용자 지정 배포** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="655be-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="655be-143">**리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="655be-144">이 그룹 hello HDInsight 클러스터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="655be-145">**위치**: 위치 지리적으로 닫기 tooyou를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="655be-146">**기본 클러스터 이름을**:이 값 hello Kafka 클러스터 hello에 대 한 기본 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="655be-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="655be-147">예를 들어 **hdi**를 입력하면 **source-hdi** 및 **dest-hdi** 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="655be-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="655be-148">**클러스터 로그인 사용자 이름**: Kafka 클러스터 hello 원본과 대상에 대 한 hello 관리자 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="655be-149">**로그인 암호 클러스터**: hello 원본과 대상에 대 한 hello 관리자 사용자 암호 Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="655be-150">**SSH 사용자 이름이**: hello 원본과 대상에 대 한 hello SSH 사용자 toocreate Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="655be-151">**SSH 암호**: hello 원본과 대상에 대 한 SSH 사용자 hello에 대 한 hello 암호 Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="655be-152">읽기 hello **약관**를 선택한 후 **toohello 약관 위에서 설명한 동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="655be-153">마지막으로 확인 **Pin toodashboard** 선택한 후 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="655be-154">Hello 클러스터 toocreate 약 20 분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="655be-155">Hello 리소스를 만든 hello 클러스터 및 웹 대시보드를 포함 하는 hello 리소스 그룹에 대 한 리디렉션된 tooa 블레이드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="655be-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Hello vnet 및 클러스터 리소스 그룹 블레이드](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="655be-157">Hello HDInsight 클러스터의 이름이 hello **소스 BASENAME** 및 **dest BASENAME**, 여기서 BASENAME는 hello 이름이 toohello 서식 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="655be-158">Toohello 클러스터를 연결 하는 경우 이후 단계에서 이러한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="655be-159">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="655be-159">Create topics</span></span>

1. <span data-ttu-id="655be-160">Toohello 연결 **소스** SSH를 사용 하 여 클러스터:</span><span class="sxs-lookup"><span data-stu-id="655be-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="655be-161">대체 **sshuser** hello SSH 사용자 이름이 hello 클러스터를 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="655be-162">대체 **BASENAME** 를 hello hello 클러스터를 만들 때 사용 되는 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="655be-163">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="655be-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="655be-164">사용 하 여 hello 다음 toofind hello 사육 호스트 hello 원본 클러스터에 대 한 명령:</span><span class="sxs-lookup"><span data-stu-id="655be-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="655be-165">다음 항목을 hello 명령 tooverify 사용 하 여 hello는 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="655be-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="655be-166">hello 응답에 포함 된 `testtopic`합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="655be-167">다음 tooview hello 사육 호스트 정보를 사용 하 여 hello (hello **소스**) 클러스터:</span><span class="sxs-lookup"><span data-stu-id="655be-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="655be-168">정보 비슷한 toohello를 다음 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="655be-169">이 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-169">Save this information.</span></span> <span data-ttu-id="655be-170">Hello 다음 섹션에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="655be-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="655be-171">미러링 구성</span><span class="sxs-lookup"><span data-stu-id="655be-171">Configure mirroring</span></span>

1. <span data-ttu-id="655be-172">Toohello 연결 **대상** 다른 SSH 세션을 사용 하 여 클러스터:</span><span class="sxs-lookup"><span data-stu-id="655be-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="655be-173">대체 **sshuser** hello SSH 사용자 이름이 hello 클러스터를 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="655be-174">대체 **BASENAME** 를 hello hello 클러스터를 만들 때 사용 되는 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="655be-175">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="655be-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="655be-176">사용 하 여 hello 다음 명령은 toocreate는 `consumer.properties` 파일에 설명 하는 방법을 hello로 toocommunicate **소스** 클러스터:</span><span class="sxs-lookup"><span data-stu-id="655be-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="655be-177">콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello `consumer.properties` 파일:</span><span class="sxs-lookup"><span data-stu-id="655be-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="655be-178">대체 **SOURCE_ZKHOSTS** 사육 hello로 hello에서 정보를 호스트 **소스** 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="655be-179">이 파일 hello 원본 Kafka 클러스터에서에서 읽을 때 hello 소비자 정보 toouse를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="655be-180">소비자 구성에 대한 자세한 내용은 kafka.apache.org의 [소비자 구성](https://kafka.apache.org/documentation#consumerconfigs)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="655be-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="655be-181">toosave hello 파일을 사용 하 여 **Ctrl + X**, **Y**, 차례로 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="655be-182">Hello 대상 클러스터와 통신 하는 hello 생산자를 구성 하기 전에 찾아야 하는데 hello 브로커 호스트 hello에 대 한 **대상** 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="655be-183">이 정보 다음 명령을 tooretrieve hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="655be-184">대체 `$PASSWORD` hello 클러스터에 대 한 hello 로그인 계정 (관리자) 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="655be-185">대체 `$CLUSTERNAME` hello 대상 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="655be-186">이 명령은 비슷한 toohello 다음 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="655be-187">사용 하 여 hello toocreate 뒤는 `producer.properties` 파일에 설명 하는 방법을 hello로 toocommunicate **대상** 클러스터:</span><span class="sxs-lookup"><span data-stu-id="655be-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="655be-188">콘텐츠로 사용 hello hello 텍스트를 다음으로 사용 하 여 hello `producer.properties` 파일:</span><span class="sxs-lookup"><span data-stu-id="655be-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="655be-189">대체 **DEST_BROKERS** hello broker 정보 hello 이전 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="655be-190">생산자 구성에 대한 자세한 내용은 kafka.apache.org의 [생산자 구성](https://kafka.apache.org/documentation#producerconfigs)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="655be-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="655be-191">MirrorMaker 시작</span><span class="sxs-lookup"><span data-stu-id="655be-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="655be-192">SSH 연결 toohello hello에서에서 **대상** 클러스터 명령 toostart hello MirrorMaker 프로세스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="655be-193">이 예제에서 사용 하는 hello 매개 변수는.</span><span class="sxs-lookup"><span data-stu-id="655be-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="655be-194">**-consumer.config**: 소비자 속성을 포함 하는 hello 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="655be-195">이러한 속성은 사용 되는 toocreate hello에서 읽는 소비자 *소스* Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="655be-196">**-producer.config**: 생산자 속성을 포함 하는 hello 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="655be-197">이러한 속성은 사용 되는 toocreate toohello 쓰는 생산자 *대상* Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="655be-198">**-화이트 리스트**: MirrorMaker hello 원본 클러스터 toohello 대상에서 복제 하는 항목의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="655be-199">**-num.streams**: hello 소비자 스레드 toocreate의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="655be-200">시작 시 MirrorMaker 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="655be-201">SSH 연결 toohello hello에서에서 **소스** 클러스터 명령 toostart 생산자 다음 hello를 사용 하 고 toohello 부분 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="655be-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="655be-202">대체 `$PASSWORD` hello 원본 클러스터에 대 한 hello 로그인 (관리자) 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="655be-203">대체 `$CLUSTERNAME` hello 원본 클러스터의 hello 이름을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="655be-204">커서로 빈 라인에 도달하면 몇 개의 텍스트 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="655be-205">Hello toohello 항목 전송 되므로 이러한 **소스** 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="655be-206">사용을 완료 한 후 **Ctrl + C** tooend hello 생산자 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="655be-207">SSH 연결 toohello hello에서에서 **대상** 클러스터를 사용 하 여 **Ctrl + C** tooend hello MirrorMaker 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="655be-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="655be-208">사용 하 여 hello 다음 명령을 tooverify 해당 hello 다음 `testtopic` 항목 만들어지고 hello 항목의 해당 데이터를 복제 된 toothis 미러:</span><span class="sxs-lookup"><span data-stu-id="655be-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="655be-209">대체 `$PASSWORD` hello 대상 클러스터에 대 한 hello 로그인 (관리자) 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="655be-210">대체 `$CLUSTERNAME` hello 대상 클러스터의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="655be-211">hello 목록 항목에 포함 `testtopic`, hello 원본 클러스터 toohello 대상에서 hello 항목을 미러링합니다. MirrorMaster 때 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="655be-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="655be-212">hello 항목에서 검색 된 hello 메시지는 hello hello 원본 클러스터에 입력 된 것과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="655be-213">Hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="655be-214">이 문서의 단계 hello 만들 둘 다에서 클러스터 hello 같은 Azure 리소스 그룹, hello Azure 포털의에서 hello 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="655be-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="655be-215">이 문서, hello Azure 가상 네트워크 및 hello 클러스터에서 사용 하는 저장소 계정에 따라 생성 된 모든 리소스를 제거 하는 hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="655be-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="655be-216">Next Steps</span></span>

<span data-ttu-id="655be-217">이 문서에서는 어떻게 toouse MirrorMaker toocreate는 Kafka의 복제본 클러스터 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="655be-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="655be-218">Kafka 다른 방법으로 toowork hello 링크 toodiscover 다음 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="655be-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="655be-219">[Apache Kafka MirrorMaker 문서](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330)(cwiki.apache.org)</span><span class="sxs-lookup"><span data-stu-id="655be-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="655be-220">HDInsight에서 Apache Kafka 시작</span><span class="sxs-lookup"><span data-stu-id="655be-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="655be-221">HDInsight의 Kafka에서 Apache Spark 사용</span><span class="sxs-lookup"><span data-stu-id="655be-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="655be-222">HDInsight의 Kafka에서 Apache Storm 사용</span><span class="sxs-lookup"><span data-stu-id="655be-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="655be-223">Azure 가상 네트워크를 통해 tooKafka 연결</span><span class="sxs-lookup"><span data-stu-id="655be-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
