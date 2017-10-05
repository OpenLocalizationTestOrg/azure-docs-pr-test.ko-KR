---
title: "Apache Kafka 시작 - Azure HDInsight | Microsoft 문서 도구"
description: "Azure HDInsight의 Apache Kafka 클러스터를 만드는 방법에 대해 알아봅니다. 토픽, 구독자 및 소비자를 만드는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 03e6996f0f44e04978080b3bd267e924f342b7fc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="a1e44-104">HDInsight의 Apache Kafka(미리 보기) 시작</span><span class="sxs-lookup"><span data-stu-id="a1e44-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="a1e44-105">Azure HDInsight의 [Apache Kafka](https://kafka.apache.org) 클러스터를 만들고 사용하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-105">Learn how to create and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="a1e44-106">Kafka는 HDInsight와 함께 제공되는 오픈 소스 분산형 스트리밍 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="a1e44-107">게시-구독 메시지 큐와 유사한 기능을 제공하므로 메시지 브로커로 자주 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-107">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="a1e44-108">현재 HDInsight에는 두 가지 버전의 Kafka, 즉 0.9.0(HDInsight 3.4) 및 0.10.0(HDInsight 3.5 및 3.6)이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="a1e44-109">이 문서의 단계에서는 HDInsight 3.6에서 Kafka를 사용하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-109">The steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="a1e44-110">Kafka 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a1e44-110">Create a Kafka cluster</span></span>

<span data-ttu-id="a1e44-111">다음 단계를 사용하여 HDInsight 클러스터에 Kafka를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-111">Use the following steps to create a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="a1e44-112">[Azure Portal](https://portal.azure.com)에서 **+ 새로 만들기**, **인텔리전스 + 분석**, **HDInsight**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-112">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![HDInsight 클러스터 만들기](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="a1e44-114">**기본**에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-114">From **Basics**, enter the following information:</span></span>

    * <span data-ttu-id="a1e44-115">**클러스터 이름**: HDInsight 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-115">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="a1e44-116">**구독**: 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-116">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="a1e44-117">**클러스터 로그인 사용자 이름** 및 **클러스터 로그인 암호**: HTTPS를 통해 클러스터에 액세스할 때 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-117">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="a1e44-118">이러한 자격 증명을 사용하여 Ambari Web UI 또는 REST API와 같은 서비스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-118">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="a1e44-119">**SSH(보안 셸) 사용자 이름**: SSH를 통해 클러스터에 액세스할 때 사용되는 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-119">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="a1e44-120">기본적으로 암호는 클러스터 로그인 암호와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-120">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="a1e44-121">**리소스 그룹**: 클러스터를 만들어 놓은 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-121">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="a1e44-122">**위치**: 클러스터를 만들어 놓은 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-122">**Location**: The Azure region to create the cluster in.</span></span>
   
 ![구독 선택](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="a1e44-124">**클러스터 유형**을 선택한 다음 **클러스터 구성**에서 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-124">Select **Cluster type**, and then set the following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="a1e44-125">**클러스터 유형**: Kafka</span><span class="sxs-lookup"><span data-stu-id="a1e44-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="a1e44-126">**버전**: Kafka 0.10.0(HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="a1e44-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="a1e44-127">**클러스터 계층**: 표준</span><span class="sxs-lookup"><span data-stu-id="a1e44-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="a1e44-128">마지막으로 **선택** 단추를 사용하여 이러한 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-128">Finally, use the **Select** button to save settings.</span></span>
     
 ![클러스터 유형 선택](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="a1e44-130">클러스터 유형을 선택한 후 __선택__ 단추를 사용하여 클러스터 유형을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-130">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="a1e44-131">그 다음, __다음__ 단추를 사용하여 기본 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-131">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="a1e44-132">**Storage**에서 Storage 계정을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="a1e44-133">이 문서의 단계에서는 다른 필드를 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-133">For the steps in this document, leave the other fields at the default values.</span></span> <span data-ttu-id="a1e44-134">__다음__ 단추를 사용하여 저장소 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-134">Use the __Next__ button to save storage configuration.</span></span>

    ![HDInsight에 대한 저장소 계정 설정 지정](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="a1e44-136">__응용 프로그램(선택 사항)__에서 __다음__을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-136">From __Applications (optional)__, select __Next__ to continue.</span></span> <span data-ttu-id="a1e44-137">이 예제에는 응용 프로그램이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="a1e44-138">__클러스터 크기__에서 __다음__을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-138">From __Cluster size__, select __Next__ to continue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="a1e44-139">HDInsight에서 Kafka의 사용 가능성을 보장하려면 클러스터에 작업자 노드가 3개 이상 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Kafka 클러스터 크기 설정](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="a1e44-141">**작업자 노드 항목당 디스크**에 따라 HDInsight에서 Kafka의 확장성이 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-141">The **disks per worker node** entry controls the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="a1e44-142">자세한 내용은 [HDInsight에서 저장소 및 Kafka의 확장성 구성](hdinsight-apache-kafka-scalability.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1e44-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="a1e44-143">__고급 설정__에서 __다음__을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-143">From __Advanced settings__, select __Next__ to continue.</span></span>

9. <span data-ttu-id="a1e44-144">**요약**에서 클러스터에 대한 구성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-144">From the **Summary**, review the configuration for the cluster.</span></span> <span data-ttu-id="a1e44-145">__편집__ 링크를 사용하여 올바르지 않은 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-145">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="a1e44-146">마지막으로 __만들기__ 단추를 사용하여 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-146">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![클러스터 구성 요약](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="a1e44-148">클러스터를 만드는 데 최대 20분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-148">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="a1e44-149">클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a1e44-149">Connect to the cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1e44-150">다음 단계를 수행하는 경우에 SSH 클라이언트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-150">When performing the following steps, you must use an SSH client.</span></span> <span data-ttu-id="a1e44-151">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1e44-151">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="a1e44-152">클라이언트에서 SSH를 다음과 같이 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-152">From your client, use SSH to connect to the cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="a1e44-153">**SSHUSER**는 클러스터를 만드는 중에 제공한 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-153">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span></span> <span data-ttu-id="a1e44-154">**CLUSTERNAME**은 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-154">Replace **CLUSTERNAME** with the name of the cluster.</span></span>

<span data-ttu-id="a1e44-155">메시지가 표시되면 SSH 계정에 사용한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-155">When prompted, enter the password you used for the SSH account.</span></span>

<span data-ttu-id="a1e44-156">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1e44-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="a1e44-157"><a id="getkafkainfo"></a>Zookeeper 및 Broker 호스트 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="a1e44-157"><a id="getkafkainfo"></a>Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="a1e44-158">Kafka를 사용할 때는 두 가지 호스트, 즉 *Zookeeper* 호스트와 *Broker* 호스트의 값을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-158">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span></span> <span data-ttu-id="a1e44-159">이러한 호스트는 Kafka API 및 Kafka와 함께 제공되는 다양한 유틸리티에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-159">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="a1e44-160">다음 단계를 사용하여 호스트 정보를 포함하는 환경 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-160">Use the following steps to create environment variables that contain the host information.</span></span> <span data-ttu-id="a1e44-161">이러한 환경 변수는 이 문서의 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-161">These environment variables are used in the steps in this document.</span></span>

1. <span data-ttu-id="a1e44-162">클러스터에 대한 SSH 연결에서 다음 명령을 사용하여 `jq` 유틸리티를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-162">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="a1e44-163">이 유틸리티는 JSON 문서를 구문 분석하는 데 사용되며 broker 호스트 정보 검색에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-163">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="a1e44-164">Ambari에서 검색한 정보로 환경 변수를 설정하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-164">To set the environment variables with information retrieved from Ambari, use the following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="a1e44-165">`CLUSTERNAME=`을 Kafka 클러스터의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-165">Set `CLUSTERNAME=` to the name of the Kafka cluster.</span></span> <span data-ttu-id="a1e44-166">`PASSWORD=`를 클러스터를 만들 때 사용한 로그인(관리자) 암호로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-166">Set `PASSWORD=` to the login (admin) password you used when creating the cluster.</span></span>

    <span data-ttu-id="a1e44-167">다음 텍스트는 `$KAFKAZKHOSTS` 내용의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-167">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="a1e44-168">다음 텍스트는 `$KAFKABROKERS` 내용의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-168">The following text is an example of the contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="a1e44-169">`cut` 명령은 호스트 목록을 두 개의 호스트 항목으로 자르는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-169">The `cut` command is used to trim the list of hosts to two host entries.</span></span> <span data-ttu-id="a1e44-170">Kafka 소비자 또는 생산자를 만들 때 호스트의 전체 목록을 제공할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-170">You do not need to provide the full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="a1e44-171">항상 정확하도록 이 세션에서 반환된 정보에 의존하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a1e44-171">Do not rely on the information returned from this session to always be accurate.</span></span> <span data-ttu-id="a1e44-172">클러스터를 확장하면 새 broker가 추가되거나 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-172">If you scale the cluster, new brokers are added or removed.</span></span> <span data-ttu-id="a1e44-173">오류가 발생하고 노드가 대체되면 노드의 호스트 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-173">If a failure occurs and a node is replaced, the host name for the node may change.</span></span>
    >
    > <span data-ttu-id="a1e44-174">Zookeeper와 broker 호스트 정보는 올바른 정보를 얻기 위해 사용하기 직전에 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="a1e44-175">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="a1e44-175">Create a topic</span></span>

<span data-ttu-id="a1e44-176">Kafka는 *토픽*이라는 범주에 데이터 스트림을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="a1e44-177">클러스터 헤드 노드에 대한 SSH 연결에서 Kafka와 함께 제공된 다음 스크립트를 사용하여 토픽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="a1e44-178">이 명령은 `$KAFKAZKHOSTS`에 저장된 호스트 정보를 사용하여 Zookeeper에 연결한 다음 **test**라는 Kafka 토픽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="a1e44-179">토픽을 나열하는 다음 스크립트를 사용하면 해당 토픽이 만들어졌는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-179">You can verify that the topic was created by using the following script to list topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="a1e44-180">이 명령의 출력에서 **test** 토픽이 포함된 Kafka 토픽이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-180">The output of this command lists Kafka topics, which contains the **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="a1e44-181">레코드 생성 및 소비</span><span class="sxs-lookup"><span data-stu-id="a1e44-181">Produce and consume records</span></span>

<span data-ttu-id="a1e44-182">Kafka는 토픽에 *레코드*를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="a1e44-183">*생산자*에서 레코드를 생성하고, *소비자*에서 이 레코드를 소비합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="a1e44-184">생산자는 Kafka *broker*로부터 레코드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="a1e44-185">HDInsight 클러스터의 각 작업자 노드는 Kafka broker입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="a1e44-186">앞에서 만든 test 토픽에 레코드를 저장한 다음 소비자를 통해 레코드를 읽으려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="a1e44-187">SSH 세션에서 Kafka와 함께 제공되는 스크립트를 사용하여 토픽에 레코드를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="a1e44-188">이 명령 이후에는 프롬프트로 돌아가지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-188">You are not returned to the prompt after this command.</span></span> <span data-ttu-id="a1e44-189">그 대신 몇 가지 텍스트 메시지를 입력한 다음 **Ctrl+C**를 사용하여 토픽 전송을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span></span> <span data-ttu-id="a1e44-190">각 행은 별도의 레코드로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="a1e44-191">Kafka와 함께 제공된 다음 스크립트를 사용하여 토픽에서 레코드를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-191">Use a script provided with Kafka to read records from the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="a1e44-192">이 명령은 토픽에서 레코드를 검색하여 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-192">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="a1e44-193">`--from-beginning`을 사용하면 스트림 시작 부분부터 시작하도록 소비자에 지시하여 모든 레코드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="a1e44-194">__Ctrl+C__를 사용하여 소비자를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-194">Use __Ctrl + C__ to stop the consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="a1e44-195">생산자 및 소비자 API</span><span class="sxs-lookup"><span data-stu-id="a1e44-195">Producer and consumer API</span></span>

<span data-ttu-id="a1e44-196">[Kafka API](http://kafka.apache.org/documentation#api)를 사용하면 프로그래밍 방식으로 레코드를 생성하고 소비할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="a1e44-197">Java 생산자와 소비자를 작성하려면 개발 환경에서 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-197">To build a Java producer and consumer, use the following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1e44-198">개발 환경에 다음 구성 요소가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-198">You must have the following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="a1e44-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 또는 이와 동등한 프로그램(예: OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="a1e44-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="a1e44-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="a1e44-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="a1e44-201">SSH 클라이언트 및 `scp` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-201">An SSH client and the `scp` command.</span></span> <span data-ttu-id="a1e44-202">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1e44-202">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="a1e44-203">[https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started)에서 예제를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-203">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="a1e44-204">생산자/소비자 예제의 경우 `Producer-Consumer` 디렉터리의 프로젝트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-204">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span></span> <span data-ttu-id="a1e44-205">이 예제에는 다음과 같은 클래스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-205">This example contains the following classes:</span></span>
   
    * <span data-ttu-id="a1e44-206">**Run** - 소비자 또는 생산자 중 하나를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-206">**Run** - starts either the consumer or producer.</span></span>

    * <span data-ttu-id="a1e44-207">**Producer** - 1,000,000개 레코드를 토픽에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-207">**Producer** - stores 1,000,000 records to the topic.</span></span>

    * <span data-ttu-id="a1e44-208">**Consumer** - 토픽에서 레코드를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-208">**Consumer** - reads records from the topic.</span></span>

2. <span data-ttu-id="a1e44-209">jar 패키지를 만들려면 디렉터리를 `Producer-Consumer` 디렉터리 위치로 변경한 후 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-209">To create a jar package, change directories to the location of the `Producer-Consumer` directory and use the following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="a1e44-210">이 명령은 `kafka-producer-consumer-1.0-SNAPSHOT.jar`라는 파일이 포함된 `target`이라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="a1e44-211">다음 명령을 사용하여 `kafka-producer-consumer-1.0-SNAPSHOT.jar` 파일을 HDInsight 클러스터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-211">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="a1e44-212">**SSHUSER**는 클러스터의 SSH 사용자로 바꾸고, **CLUSTERNAME**은 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-212">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="a1e44-213">메시지가 표시되면 SSH 사용자의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-213">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="a1e44-214">`scp` 명령이 파일 복사를 완료하면 SSH를 사용하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-214">Once the `scp` command finishes copying the file, connect to the cluster using SSH.</span></span> <span data-ttu-id="a1e44-215">다음 명령을 사용하여 테스트 토픽에 레코드를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-215">Use the following command to write records to the test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="a1e44-216">프로세스가 완료되면 다음 명령을 사용하여 토픽에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-216">Once the process has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="a1e44-217">레코드 수와 함께 읽은 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-217">The records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="a1e44-218">이전 단계의 스크립트를 사용하여 몇 가지 레코드를 토픽으로 보내면 1,000,000개 이상이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-218">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="a1e44-219">__Ctrl+C__를 사용하여 소비자를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-219">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="a1e44-220">여러 소비자</span><span class="sxs-lookup"><span data-stu-id="a1e44-220">Multiple consumers</span></span>

<span data-ttu-id="a1e44-221">Kafka 소비자는 레코드를 읽을 때 소비자 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="a1e44-222">여러 소비자와 같은 그룹을 사용하면 부하가 분산되어 토픽에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-222">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="a1e44-223">그룹의 각 소비자는 레코드의 일부를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-223">Each consumer in the group receives a portion of the records.</span></span> <span data-ttu-id="a1e44-224">동작 중인 이 프로세스를 확인하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-224">To see this process in action, use the following steps:</span></span>

1. <span data-ttu-id="a1e44-225">클러스터에 대한 새로운 SSH 세션을 열어 두 세션을 갖도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-225">Open a new SSH session to the cluster, so that you have two of them.</span></span> <span data-ttu-id="a1e44-226">각 세션에서 다음을 사용하여 동일한 소비자 그룹 ID를 가진 소비자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-226">In each session, use the following to start a consumer with the same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="a1e44-227">이 명령은 그룹 ID `mygroup`을 사용하여 소비자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-227">This command starts a consumer using the group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1e44-228">[Zookeeper 및 Broker 호스트 정보 가져오기](#getkafkainfo) 섹션의 명령을 사용하여 이 SSH 세션에 대해 `$KAFKABROKERS`를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-228">Use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="a1e44-229">각 세션에서 토픽으로부터 받은 레코드를 계산하는 것을 지켜봅니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-229">Watch as each session counts the records it receives from the topic.</span></span> <span data-ttu-id="a1e44-230">두 세션의 합계는 앞서 한 소비자로부터 받은 것과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-230">The total of both sessions should be the same as you received previously from one consumer.</span></span>

<span data-ttu-id="a1e44-231">동일한 그룹 내에서 클라이언트에 의한 소비는 토픽에 대한 파티션을 통해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-231">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="a1e44-232">앞에서 만든 `test` 토픽에는 8개의 파티션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-232">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="a1e44-233">8개 SSH 세션을 열고 모든 세션에서 소비자를 시작하면 각 소비자는 해당 토픽에 대한 단일 파티션에서 레코드를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1e44-234">소비자 그룹에는 파티션보다 더 많은 소비자 인스턴스가 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="a1e44-235">이 예제에서 하나의 소비자 그룹은 토픽의 파티션 수이기 때문에 최대 8개 소비자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-235">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="a1e44-236">또는 소비자가 8개 이하인 소비자 그룹이 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="a1e44-237">Kafka에 저장된 레코드는 파티션에서 받은 순서대로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-237">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="a1e44-238">*파티션 내의* 레코드에 대해 순서대로 전달하려면 파티션 수와 일치하는 소비자 인스턴스가 있는 소비자 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-238">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="a1e44-239">*토픽 내의* 레코드에 대해 순서대로 전달하려면 하나의 소비자 인스턴스만 사용하는 소비자 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-239">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="a1e44-240">스트리밍 API</span><span class="sxs-lookup"><span data-stu-id="a1e44-240">Streaming API</span></span>

<span data-ttu-id="a1e44-241">스트리밍 API 버전 0.10.0이 Kafka에 추가되었습니다. 이전 버전은 스트림 처리를 위해 Apache Spark 또는 Storm에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-241">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="a1e44-242">아직 그렇게 하지 않았으면 [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started)에서 개발 환경으로 예제를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-242">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span></span> <span data-ttu-id="a1e44-243">스트리밍 예제의 경우 `streaming` 디렉터리의 프로젝트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-243">For the streaming example, use the project in the `streaming` directory.</span></span>
   
    <span data-ttu-id="a1e44-244">이 프로젝트에는 이전에 만들어진 `test` 토픽에서 레코드를 읽는 `Stream` 클래스 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-244">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span></span> <span data-ttu-id="a1e44-245">읽은 단어를 집계하여 각 단어를 내보내고 `wordcounts`라는 토픽에 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-245">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span></span> <span data-ttu-id="a1e44-246">`wordcounts` 토픽은 이 섹션의 이후 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-246">The `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="a1e44-247">개발 환경의 명령줄에서 `Streaming` 디렉터리 위치로 디렉터리를 변경한 후 다음 명령을 사용하여 jar 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-247">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="a1e44-248">이 명령은 `kafka-streaming-1.0-SNAPSHOT.jar`라는 파일이 포함된 `target`이라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="a1e44-249">다음 명령을 사용하여 `kafka-streaming-1.0-SNAPSHOT.jar` 파일을 HDInsight 클러스터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-249">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="a1e44-250">**SSHUSER**는 클러스터의 SSH 사용자로 바꾸고, **CLUSTERNAME**은 클러스터 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-250">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="a1e44-251">메시지가 표시되면 SSH 사용자의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-251">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="a1e44-252">`scp` 명령으로 파일 복사를 완료하면 SSH를 사용하여 클러스터에 연결한 후 다음 명령을 사용하여 `wordcounts` 토픽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-252">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="a1e44-253">그런 후 다음 명령을 사용하여 스트리밍 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-253">Next, start the streaming process by using the following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="a1e44-254">이 명령은 백그라운드에서 스트리밍 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-254">This command starts the streaming process in the background.</span></span>

6. <span data-ttu-id="a1e44-255">다음 명령을 사용하여 `test` 토픽으로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-255">Use the following command to send messages to the `test` topic.</span></span> <span data-ttu-id="a1e44-256">스트리밍 예제에서 처리되는 이러한 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-256">These messages are processed by the streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="a1e44-257">다음 명령을 사용하여 스트리밍 프로세스에 의해 `wordcounts` 토픽에 기록된 출력을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-257">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="a1e44-258">데이터를 보려면 소비자에게 키를 인쇄하고 역직렬 변환기에 키와 값을 사용하도록 알려주어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-258">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span></span> <span data-ttu-id="a1e44-259">키 이름은 단어이며, 키 값에는 개수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-259">The key name is the word, and the key value contains the count.</span></span>
   
    <span data-ttu-id="a1e44-260">다음 텍스트와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-260">The output is similar to the following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="a1e44-261">단어가 발생할 때마다 개수가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-261">The count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="a1e44-262">__Ctrl+C__를 사용하여 소비자를 종료한 다음 `fg` 명령을 사용하여 스트리밍 백그라운드 작업을 다시 포그라운드 상태로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-262">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span></span> <span data-ttu-id="a1e44-263">마찬가지로 __Ctrl+C__를 사용하여 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-263">Use __Ctrl + C__ to exit it also.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="a1e44-264">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="a1e44-264">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="a1e44-265">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a1e44-265">Troubleshoot</span></span>

<span data-ttu-id="a1e44-266">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1e44-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1e44-267">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1e44-267">Next steps</span></span>

<span data-ttu-id="a1e44-268">이 문서에서 HDInsight에서 Apache Kafka를 사용할 때 필요한 기본 사항을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a1e44-268">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="a1e44-269">Kafka 작업에 대해 자세히 알아보려면 다음을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a1e44-269">Use the following to learn more about working with Kafka:</span></span>

* [<span data-ttu-id="a1e44-270">HDInsight의 Kafka를 통한 데이터 고가용성 보장</span><span class="sxs-lookup"><span data-stu-id="a1e44-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="a1e44-271">HDInsight에서 Kafka로 관리 디스크를 구성하여 확장성 높이기</span><span class="sxs-lookup"><span data-stu-id="a1e44-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="a1e44-272">kafka.apache.org의 [Apache Kafka 문서](http://kafka.apache.org/documentation.html)</span><span class="sxs-lookup"><span data-stu-id="a1e44-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="a1e44-273">MirrorMaker를 사용하여 HDInsight에 Kafka 복제본 만들기</span><span class="sxs-lookup"><span data-stu-id="a1e44-273">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="a1e44-274">HDInsight의 Kafka에서 Apache Storm 사용</span><span class="sxs-lookup"><span data-stu-id="a1e44-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="a1e44-275">HDInsight의 Kafka에서 Apache Spark 사용</span><span class="sxs-lookup"><span data-stu-id="a1e44-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="a1e44-276">Azure Virtual Network를 통해 Kafka에 연결</span><span class="sxs-lookup"><span data-stu-id="a1e44-276">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
