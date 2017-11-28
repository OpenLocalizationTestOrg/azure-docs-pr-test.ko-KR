---
title: "Spark aaaApache Kafka-Azure HDInsight를 통해 스트리밍 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Spark Apache Spark toostream 데이터 DStreams를 사용 하 여 Apache Kafka 안팎으로 합니다. 이 예제에서는 HDInsight의 Spark에서 Jupyter Notebook을 사용하여 데이터를 스트리밍합니다."
keywords: "kafka 예제,kafka zookeeper,spark 스트리밍 kafka,spark 스트리밍 kafka 예제"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="413b0-105">HDInsight의 Kafka(미리 보기)를 사용한 Apache Spark 스트리밍(DStream) 예제</span><span class="sxs-lookup"><span data-stu-id="413b0-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="413b0-106">자세한 내용은 방법 toouse Spark Apache Spark toostream 데이터 DStreams를 사용 하 여 HDInsight의 Apache Kafka 안팎으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="413b0-107">이 예제에서는 hello Spark 클러스터에서 실행 되는 Jupyter 노트북을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="413b0-108">이 문서의 단계 hello HDInsight의 Spark와 HDInsight 클러스터에서 Kafka 모두 포함 된 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="413b0-109">이 클러스터는 Spark 클러스터 toodirectly hello를는 Azure 가상 네트워크 내에 위치한 둘 다 hello Kafka 클러스터와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="413b0-110">Hello이이 문서의 단계를 완료 하는 경우 toodelete hello 클러스터 tooavoid 초과 요금을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="413b0-111">Hello 클러스터를 만들려면</span><span class="sxs-lookup"><span data-stu-id="413b0-111">Create hello clusters</span></span>

<span data-ttu-id="413b0-112">HDInsight의 Apache Kafka에서는 액세스 toohello Kafka 브로커를 통해 공용 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="413b0-113">토론에 tooKafka 있어야 hello hello 노드로 동일한 Azure 가상 네트워크는 모든 작업이 hello Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="413b0-114">예를 들어 hello Kafka 및 Spark 클러스터를 모두 Azure 가상 네트워크에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="413b0-115">hello 다음 그림에 hello 클러스터 간의 통신 흐름 방식을:</span><span class="sxs-lookup"><span data-stu-id="413b0-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Azure 가상 네트워크에 있는 Spark 및 Kafka 클러스터 다이어그램](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="413b0-117">Kafka 자체는 hello 가상 네트워크 내에서 제한 된 toocommunication, SSH 같은 hello에 있는 다른 서비스 클러스터 및 Ambari를 통해 액세스할 수 있지만 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="413b0-118">HDInsight와 사용할 수 있는 공용 포트 hello에 대 한 자세한 내용은 참조 하십시오. [포트 및 HDInsight에서 사용 하는 Uri](hdinsight-hadoop-port-settings-for-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="413b0-119">수동으로 만들 수 있습니다는 Azure 가상 네트워크에서 Kafka, 및 Spark 클러스터를 보다 쉽게 Azure 리소스 관리자 템플릿 toouse는.</span><span class="sxs-lookup"><span data-stu-id="413b0-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="413b0-120">사용 하 여 hello 다음 단계는 Azure 가상 네트워크, Kafka toodeploy 및 Spark 클러스터 tooyour Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="413b0-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="413b0-121">Hello tooAzure에서 단추 toosign 및 hello Azure 포털에서에서 열기 hello 서식 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="413b0-122">hello Azure 리소스 관리자 템플릿에 위치한 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="413b0-123">HDInsight의 Kafka의 tooguarantee 가용성, 클러스터 3 개 이상의 작업자 노드를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="413b0-124">이 템플릿은 세 개의 작업자 노드를 포함하는 Kafka 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="413b0-125">이 템플릿은 Kafka와 Spark 둘 다에 대해 HDInsight 3.6 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="413b0-126">정보 toopopulate hello 항목에 나오는 hello에 사용 하 여 hello **사용자 지정 배포** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="413b0-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="413b0-128">**리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="413b0-129">이 그룹 hello HDInsight 클러스터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="413b0-130">**위치**: 위치 지리적으로 닫기 tooyou를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="413b0-131">**기본 클러스터 이름을**:이 값 hello hello Kafka 및 Spark 클러스터에 대 한 기본 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="413b0-132">예를 들어, **hdi**를 입력하면 spark-hdi__라는 Spark 클러스터와 **kafka-hdi**라는 Kafka 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="413b0-133">**클러스터 로그인 사용자 이름**: hello Kafka 및 Spark 클러스터에 대 한 hello 관리자 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="413b0-134">**로그인 암호 클러스터**: hello Kafka 및 Spark 클러스터에 대 한 hello 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="413b0-135">**SSH 사용자 이름이**: hello Kafka 및 Spark 클러스터에 대 한 SSH 사용자 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="413b0-136">**SSH 암호**: hello Kafka 및 Spark 클러스터에 대 한 SSH 사용자 hello에 대 한 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="413b0-137">읽기 hello **약관**를 선택한 후 **toohello 약관 위에서 설명한 동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="413b0-138">마지막으로 확인 **Pin toodashboard** 선택한 후 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="413b0-139">Hello 클러스터 toocreate 약 20 분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="413b0-140">Hello 리소스를 만든 hello 클러스터 및 웹 대시보드를 포함 하는 hello 리소스 그룹에 대 한 리디렉션된 tooa 블레이드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Hello vnet 및 클러스터 리소스 그룹 블레이드](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="413b0-142">Hello HDInsight 클러스터의 이름이 hello **spark BASENAME** 및 **kafka BASENAME**, 여기서 BASENAME는 hello 이름이 toohello 서식 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="413b0-143">Toohello 클러스터를 연결 하는 경우 이후 단계에서 이러한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="413b0-144">Hello 노트북을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="413b0-144">Use hello notebooks</span></span>

<span data-ttu-id="413b0-145">이 문서에서 설명 하는 hello 예제에 대 한 hello 코드에서 사용할 수는 [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka)합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="413b0-146">Hello에 hello 단계를 따라 `README.md` toocomplete이 예제 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="413b0-147">Hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="413b0-148">이 문서의 단계 hello 만들 둘 다에서 클러스터 hello 같은 Azure 리소스 그룹, hello Azure 포털의에서 hello 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="413b0-149">이 문서, hello Azure 가상 네트워크 및 hello 클러스터에서 사용 하는 저장소 계정에 따라 생성 된 모든 리소스를 제거 하는 hello 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="413b0-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="413b0-150">Next steps</span></span>

<span data-ttu-id="413b0-151">이 예제에서는 toouse tooread 멤버 및 tooKafka 작성 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="413b0-152">Kafka 다른 방법으로 toowork hello 링크 toodiscover 다음 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="413b0-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="413b0-153">HDInsight에서 Apache Kafka 시작</span><span class="sxs-lookup"><span data-stu-id="413b0-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="413b0-154">HDInsight의 MirrorMaker toocreate Kafka의 복제본을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="413b0-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="413b0-155">HDInsight의 Kafka에서 Apache Storm 사용</span><span class="sxs-lookup"><span data-stu-id="413b0-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

