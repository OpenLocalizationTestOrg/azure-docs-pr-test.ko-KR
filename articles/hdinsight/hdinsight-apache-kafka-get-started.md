---
title: "Apache Kafka-Azure HDInsight와 aaaStart | Microsoft Docs"
description: "Azure HDInsight의 Apache Kafka toocreate 클러스터링 하는 방법에 대해 알아봅니다. 자세한 내용은 방법 toocreate 항목, 구독자 및 소비자입니다."
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
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="c3f13-104">HDInsight의 Apache Kafka(미리 보기) 시작</span><span class="sxs-lookup"><span data-stu-id="c3f13-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="c3f13-105">자세한 방법을 toocreate 사용 하는 [Apache Kafka](https://kafka.apache.org) Azure HDInsight 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="c3f13-106">Kafka는 HDInsight와 함께 제공되는 오픈 소스 분산형 스트리밍 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="c3f13-107">대개 메시지 브로커로 유사한 기능을 제공 하는 대로 tooa 게시-구독 메시지 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="c3f13-108">현재 HDInsight에는 두 가지 버전의 Kafka, 즉 0.9.0(HDInsight 3.4) 및 0.10.0(HDInsight 3.5 및 3.6)이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="c3f13-109">이 문서에 hello 단계 HDInsight 3.6에 Kafka 사용 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="c3f13-110">Kafka 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="c3f13-110">Create a Kafka cluster</span></span>

<span data-ttu-id="c3f13-111">Hello 단계 toocreate는 Kafka HDInsight 클러스터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="c3f13-112">Hello에서 [Azure 포털](https://portal.azure.com)선택, **+ 새로 만들기**, **인텔리전스 + 분석**를 선택한 후 **HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![HDInsight 클러스터 만들기](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="c3f13-114">**기본 사항**, hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="c3f13-115">**클러스터 이름**: hello HDInsight 클러스터의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="c3f13-116">**구독**: hello 구독 toouse를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="c3f13-117">**클러스터 로그인 사용자 이름과** 및 **클러스터 로그인 암호**: HTTPS를 통해 hello 클러스터에 액세스할 때 hello 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="c3f13-118">Hello Ambari 웹 UI 또는 REST API와 같은 이러한 자격 증명 tooaccess 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="c3f13-119">**SSH 사용자 이름 보안**: SSH를 통해 hello 클러스터에 액세스할 때 사용 하는 hello 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="c3f13-120">기본적으로 hello 암호 hello 클러스터 로그인 암호와 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="c3f13-121">**리소스 그룹**: hello 리소스 그룹 toocreate hello 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="c3f13-122">**위치**: hello Azure 지역 toocreate hello 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![구독 선택](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="c3f13-124">선택 **형식 클러스터**, 집합 hello에서 값을 누른 다음 **클러스터 구성**:</span><span class="sxs-lookup"><span data-stu-id="c3f13-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="c3f13-125">**클러스터 유형**: Kafka</span><span class="sxs-lookup"><span data-stu-id="c3f13-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="c3f13-126">**버전**: Kafka 0.10.0(HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="c3f13-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="c3f13-127">**클러스터 계층**: 표준</span><span class="sxs-lookup"><span data-stu-id="c3f13-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="c3f13-128">마지막으로 hello를 사용 하 여 **선택** toosave 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![클러스터 유형 선택](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="c3f13-130">Hello 클러스터 종류를 선택한 후 hello를 사용 하 여 __선택__ tooset hello 클러스터 유형 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="c3f13-131">를 사용 하 여 hello __다음__ 단추 toofinish 기본 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="c3f13-132">**Storage**에서 Storage 계정을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="c3f13-133">이 문서의 단계 hello에 대 한 hello 나머지 필드는 hello 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="c3f13-134">사용 하 여 hello __다음__ 단추 toosave 저장소 구성.</span><span class="sxs-lookup"><span data-stu-id="c3f13-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![HDInsight에 대 한 저장소 계정 설정을 hello 설정](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="c3f13-136">__(선택 사항) 응용 프로그램__선택, __다음__ toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="c3f13-137">이 예제에는 응용 프로그램이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="c3f13-138">__클러스터 크기__선택, __다음__ toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c3f13-139">HDInsight의 Kafka의 tooguarantee 가용성, 클러스터 3 개 이상의 작업자 노드를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![집합 hello Kafka 클러스터 크기](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="c3f13-141">hello **작업자 노드당 디스크** 입력 컨트롤 hello HDInsight의 Kafka의 확장성입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="c3f13-142">자세한 내용은 [HDInsight에서 저장소 및 Kafka의 확장성 구성](hdinsight-apache-kafka-scalability.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f13-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="c3f13-143">__고급 설정__선택, __다음__ toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="c3f13-144">Hello에서 **요약**, hello 클러스터에 대 한 hello 구성을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="c3f13-145">사용 하 여 hello __편집__ toochange 올바르지 않은 설정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="c3f13-146">마지막으로, the__Create__ 단추 toocreate hello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![클러스터 구성 요약](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="c3f13-148">Too20 분 toocreate hello 클러스터를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="c3f13-149">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="c3f13-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3f13-150">Hello 다음 단계를 수행할 때는 SSH 클라이언트를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="c3f13-151">자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c3f13-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="c3f13-152">사용자 클라이언트에서 SSH tooconnect toohello 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="c3f13-153">대체 **SSHUSER** hello SSH username 클러스터 생성 중에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="c3f13-154">대체 **CLUSTERNAME** hello 클러스터의 hello 이름을 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="c3f13-155">메시지가 표시 되 면 hello SSH 계정에 사용한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="c3f13-156">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f13-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="c3f13-157"><a id="getkafkainfo"></a>Hello 사육 및 브로커 호스트 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="c3f13-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="c3f13-158">두 개의 호스트 값을 알고 있어야 Kafka를 사용할 때 hello *사육* 호스트 및 hello *브로커* 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="c3f13-159">이러한 호스트와 Kafka hello Kafka API와 많은 hello 제공 하는 유틸리티에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="c3f13-160">Hello 호스트 정보를 포함 하는 단계 toocreate 환경 변수를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="c3f13-161">이러한 환경 변수는 hello이이 문서의 단계에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="c3f13-162">SSH 연결 toohello 클러스터에서 사용 하 여 hello 다음 명령은 tooinstall hello `jq` 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="c3f13-163">이 유틸리티는 사용 되는 tooparse JSON 문서 그리고 hello broker 호스트 정보를 검색 하는 데 유용:</span><span class="sxs-lookup"><span data-stu-id="c3f13-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="c3f13-164">다음 명령을 사용 하 여 hello Ambar에서 tooset hello 환경 변수가 해당 정보로 검색:</span><span class="sxs-lookup"><span data-stu-id="c3f13-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="c3f13-165">설정 `CLUSTERNAME=` toohello 이름 hello Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="c3f13-166">설정 `PASSWORD=` hello 클러스터를 만들 때 사용한 toohello 로그인 (관리자) 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="c3f13-167">hello 다음 텍스트는 hello 내용의 예로 `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="c3f13-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="c3f13-168">hello 다음 텍스트는 hello 내용의 예로 `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="c3f13-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="c3f13-169">hello `cut` 명령 호스트 tootwo 호스트 항목의 사용 되는 tootrim hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="c3f13-170">Kafka 소비자 또는 공급자를 만들 때 호스트 tooprovide hello 전체 목록을 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="c3f13-171">Tooalways 정확할이 세션에서 반환 된 hello 정보에 의존 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c3f13-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="c3f13-172">Hello 클러스터를 크기를 조정 하는 경우 새 브로커 추가 또는 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="c3f13-173">오류가 발생 하는 경우 노드는 대체 hello 노드에 대 한 hello 호스트 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="c3f13-174">Tooensure 유효한 정보를 사용 하기 전에 잠시 후에 hello 사육 및 브로커 호스트 정보를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="c3f13-175">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="c3f13-175">Create a topic</span></span>

<span data-ttu-id="c3f13-176">Kafka는 *토픽*이라는 범주에 데이터 스트림을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="c3f13-177">프로그램의 SSH 연결 tooa 클러스터 헤드 노드에에서 항목을 Kafka toocreate 함께 제공 되는 스크립트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="c3f13-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="c3f13-178">이 명령은 연결에 저장 된 hello 호스트 정보를 사용 하 여 tooZookeeper `$KAFKAZKHOSTS`, 한 다음 이라는 Kafka 항목을 만들 **테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="c3f13-179">다음 스크립트 toolist 항목 hello를 사용 하 여 해당 hello 항목을 만든 날짜를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="c3f13-180">hello이 명령의 출력에 항목을 나열 Kafka, hello가 포함 되어 있는 **테스트** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="c3f13-181">레코드 생성 및 소비</span><span class="sxs-lookup"><span data-stu-id="c3f13-181">Produce and consume records</span></span>

<span data-ttu-id="c3f13-182">Kafka는 토픽에 *레코드*를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="c3f13-183">*생산자*에서 레코드를 생성하고, *소비자*에서 이 레코드를 소비합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="c3f13-184">생산자는 Kafka *broker*로부터 레코드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="c3f13-185">HDInsight 클러스터의 각 작업자 노드는 Kafka broker입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="c3f13-186">이전에 만든 및 소비자를 사용 하 여를 읽을 hello 테스트 항목으로 단계 toostore 레코드 로우 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="c3f13-187">Hello SSH 세션에서 Kafka toowrite 레코드 toohello 항목을 제공 하는 스크립트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="c3f13-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="c3f13-188">하면 반환 되지 않습니다 toohello 프롬프트이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="c3f13-189">대신, 몇 가지 문자 메시지를 입력 하 고 사용 하 여 **Ctrl + C** toostop toohello 항목을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="c3f13-190">각 행은 별도의 레코드로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="c3f13-191">Hello 항목에서 Kafka tooread 레코드와 함께 제공 되는 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="c3f13-192">이 명령은 hello 항목에서 hello 레코드를 검색 하 고 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="c3f13-193">사용 하 여 `--from-beginning` 모든 레코드를 검색 하므로 hello 소비자 toostart hello 스트림의 hello 시작 부분에서 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="c3f13-194">사용 하 여 __Ctrl + C__ toostop hello 소비자입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="c3f13-195">생산자 및 소비자 API</span><span class="sxs-lookup"><span data-stu-id="c3f13-195">Producer and consumer API</span></span>

<span data-ttu-id="c3f13-196">또한 프로그래밍 방식으로 생성 하 고 hello를 사용 하 여 레코드 사용 수 [Kafka Api](http://kafka.apache.org/documentation#api)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="c3f13-197">toobuild Java 생산자와 소비자를 hello 개발 환경에서 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3f13-198">Hello 다음과 같은 구성 요소가 개발 환경에 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="c3f13-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 또는 이와 동등한 프로그램(예: OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="c3f13-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="c3f13-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="c3f13-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="c3f13-201">SSH 클라이언트와 hello `scp` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="c3f13-202">자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c3f13-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="c3f13-203">Hello 예제를 다운로드 [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="c3f13-204">예: hello 생산자/소비자 hello 프로젝트 hello에서 사용 하 여 `Producer-Consumer` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="c3f13-205">이 예제는 hello를 아래의 클래스가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="c3f13-206">**실행** -hello 소비자 또는 공급자 중 하나를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="c3f13-207">**생산자** -저장소 1000000 레코드 toohello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="c3f13-208">**소비자** -hello 항목에서 레코드를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="c3f13-209">hello의 디렉터리 toohello 위치를 변경 하는 jar 패키지 toocreate `Producer-Consumer` 다음 명령을 디렉터리 및 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="c3f13-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="c3f13-210">이 명령은 `kafka-producer-consumer-1.0-SNAPSHOT.jar`라는 파일이 포함된 `target`이라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="c3f13-211">사용 하 여 hello 다음 명령을 toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` 파일 tooyour HDInsight 클러스터:</span><span class="sxs-lookup"><span data-stu-id="c3f13-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="c3f13-212">대체 **SSHUSER** 클러스터 및 바꾸기에 대 한 hello SSH 사용자와 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="c3f13-213">메시지가 표시 되 면 hello SSH 사용자 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="c3f13-214">한 번 hello `scp` hello 파일 복사 완료, SSH를 사용 하 여 toohello 클러스터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="c3f13-215">Hello 명령 toowrite 레코드 toohello 테스트 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="c3f13-216">Hello 프로세스가 완료 되 면 hello 명령 tooread hello 항목에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="c3f13-217">hello 레코드 읽기, 레코드의 수와 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="c3f13-218">이전 단계에서 스크립트를 사용 하 여 여러 레코드 toohello 항목 전송 기록 1000000 보다 몇 가지 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="c3f13-219">사용 하 여 __Ctrl + C__ tooexit hello 소비자입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="c3f13-220">여러 소비자</span><span class="sxs-lookup"><span data-stu-id="c3f13-220">Multiple consumers</span></span>

<span data-ttu-id="c3f13-221">Kafka 소비자는 레코드를 읽을 때 소비자 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="c3f13-222">여러 소비자와 같은 그룹 hello를 사용 하 여 항목에서 읽기 분산 된 부하의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="c3f13-223">Hello 그룹의 각 소비자는 hello 레코드의 일부를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="c3f13-224">이 과정을 사용 하 여 hello 다음 단계를 toosee:</span><span class="sxs-lookup"><span data-stu-id="c3f13-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="c3f13-225">그 중 두 개 있을 수 있도록 새 SSH 세션 toohello 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="c3f13-226">Hello를 사용 하 여 각 세션에서 다음 toostart 인 소비자 hello 같은 소비자 그룹 ID:</span><span class="sxs-lookup"><span data-stu-id="c3f13-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="c3f13-227">이 명령은 hello 그룹 ID를 사용 하 여 소비자 시작 `mygroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c3f13-228">Hello 명령을 사용 하 여 hello에 [hello 사육 및 브로커 호스트 정보를 얻을](#getkafkainfo) 섹션 tooset `$KAFKABROKERS` 이 SSH 세션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="c3f13-229">Hello 항목에서 받는 각 세션 개수 hello 레코드 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="c3f13-230">두 세션의 hello 합계는 하나의 소비자에서 이전에 받은 대로 동일한 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="c3f13-231">클라이언트 hello hello 항목에 대 한 hello 파티션을 통해 처리 같은 그룹 내의 사용입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="c3f13-232">Hello에 대 한 `test` , 이전에 만든 항목 8 개의 파티션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="c3f13-233">8 개의 SSH 세션을 열고 모든 세션에서 소비자를 시작 하는 경우 각 소비자 hello 항목에 대 한 단일 파티션을에서 레코드를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3f13-234">소비자 그룹에는 파티션보다 더 많은 소비자 인스턴스가 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="c3f13-235">이 예제에서는 하나의 소비자 그룹 hello hello 항목의 파티션 수가 이므로 tooeight 소비자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="c3f13-236">또는 소비자가 8개 이하인 소비자 그룹이 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="c3f13-237">Kafka에 저장 된 레코드 파티션 내에서 수신 된 hello 순서에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="c3f13-238">레코드에 대 한 tooachieve 순차적에서 전달 *파티션 내에서*, 소비자 인스턴스 수가 hello hello 파티션 수와 일치 하는 소비자 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="c3f13-239">레코드에 대 한 tooachieve 순차적에서 전달 *hello 항목 내에서*를 하나만 소비자 인스턴스와 소비자 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="c3f13-240">스트리밍 API</span><span class="sxs-lookup"><span data-stu-id="c3f13-240">Streaming API</span></span>

<span data-ttu-id="c3f13-241">hello 스트리밍 API 버전 0.10.0; tooKafka 추가한 이전 버전 스트림 처리에 대 한 Apache Spark 또는 스톰에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="c3f13-242">그렇게 이미 하지 않은 경우 다운로드에서 hello 예제 [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="c3f13-243">스트리밍 예제는 hello에 대 한 hello 프로젝트 hello에서 사용 하 여 `streaming` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="c3f13-244">이 프로젝트에는 하나의 클래스만 `Stream`, hello에서 레코드를 읽고 있는 `test` 이전에 만든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="c3f13-245">읽기, hello 단어 수를 계산 하 고 명명 된 각 단어 및 count tooa 항목 내보냅니다 `wordcounts`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="c3f13-246">hello `wordcounts` 주제는이 단원의 이후 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="c3f13-247">Hello 명령줄에서 개발 환경에서의 hello 디렉터리 toohello 위치를 변경 `Streaming` 디렉터리와 다음 명령 toocreate jar 패키지를 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="c3f13-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="c3f13-248">이 명령은 `kafka-streaming-1.0-SNAPSHOT.jar`라는 파일이 포함된 `target`이라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="c3f13-249">사용 하 여 hello 다음 명령을 toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` 파일 tooyour HDInsight 클러스터:</span><span class="sxs-lookup"><span data-stu-id="c3f13-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="c3f13-250">대체 **SSHUSER** 클러스터 및 바꾸기에 대 한 hello SSH 사용자와 **CLUSTERNAME** 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="c3f13-251">메시지가 표시 되 면 hello SSH 사용자 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="c3f13-252">한 번 hello `scp` hello 파일 복사 완료 명령, SSH를 사용 하 여 toohello 클러스터 연결 및 명령 toocreate hello 다음 hello를 사용 하 여 `wordcounts` 항목:</span><span class="sxs-lookup"><span data-stu-id="c3f13-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="c3f13-253">다음으로 hello 다음 명령을 사용 하 여 프로세스를 스트리밍 hello를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="c3f13-254">이 명령은 hello 스트리밍 hello 백그라운드에서 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="c3f13-255">사용 하 여 hello 다음 명령은 toosend 메시지 toohello `test` 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="c3f13-256">Hello 스트리밍 예제에서 이러한 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="c3f13-257">사용 하 여 hello toohello 작성 된 명령 tooview hello 출력 다음 `wordcounts` 프로세스 스트리밍 hello 하 여 항목:</span><span class="sxs-lookup"><span data-stu-id="c3f13-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="c3f13-258">tooview hello 데이터 hello 소비자 tooprint hello 키와 hello deserializer toouse hello 키와 값에 대 한 설명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="c3f13-259">hello 키 이름은 hello 단어가 고 hello 키 값 hello 수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="c3f13-260">hello는 텍스트 다음 비슷한 toohello 출력:</span><span class="sxs-lookup"><span data-stu-id="c3f13-260">hello output is similar toohello following text:</span></span>
   
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
    > <span data-ttu-id="c3f13-261">hello 개수에는 단어 발생할 때마다를 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="c3f13-262">Hello를 사용 하 여 __Ctrl + C__ tooexit 소비자 hello 다음 hello를 사용 하 여 `fg` toobring hello 스트리밍 백그라운드 작업 백 toohello 전경 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="c3f13-263">사용 하 여 __Ctrl + C__ tooexit 것도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="c3f13-264">Hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="c3f13-265">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c3f13-265">Troubleshoot</span></span>

<span data-ttu-id="c3f13-266">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f13-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3f13-267">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3f13-267">Next steps</span></span>

<span data-ttu-id="c3f13-268">이 문서에서는 hello의 기본적인 사용 HDInsight의 Apache Kafka 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="c3f13-269">다음 Kafka 사용에 대 한 더 toolearn hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f13-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="c3f13-270">HDInsight의 Kafka를 통한 데이터 고가용성 보장</span><span class="sxs-lookup"><span data-stu-id="c3f13-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="c3f13-271">HDInsight에서 Kafka로 관리 디스크를 구성하여 확장성 높이기</span><span class="sxs-lookup"><span data-stu-id="c3f13-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="c3f13-272">kafka.apache.org의 [Apache Kafka 문서](http://kafka.apache.org/documentation.html)</span><span class="sxs-lookup"><span data-stu-id="c3f13-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="c3f13-273">HDInsight의 MirrorMaker toocreate Kafka의 복제본을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c3f13-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="c3f13-274">HDInsight의 Kafka에서 Apache Storm 사용</span><span class="sxs-lookup"><span data-stu-id="c3f13-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="c3f13-275">HDInsight의 Kafka에서 Apache Spark 사용</span><span class="sxs-lookup"><span data-stu-id="c3f13-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="c3f13-276">Azure 가상 네트워크를 통해 tooKafka 연결</span><span class="sxs-lookup"><span data-stu-id="c3f13-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
