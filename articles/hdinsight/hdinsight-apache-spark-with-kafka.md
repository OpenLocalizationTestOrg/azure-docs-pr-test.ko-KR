---
title: "Kafka와 함께 Apache Spark 스트리밍 - Azure HDInsight | Microsoft Docs"
description: "Spark Apache Spark를 사용하여 DStreams로 Apache Kafka에(서) 데이터를 스트리밍하는 방법을 알아봅니다. 이 예제에서는 HDInsight의 Spark에서 Jupyter Notebook을 사용하여 데이터를 스트리밍합니다."
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="edcd1-105">HDInsight의 Kafka(미리 보기)를 사용한 Apache Spark 스트리밍(DStream) 예제</span><span class="sxs-lookup"><span data-stu-id="edcd1-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="edcd1-106">Spark Apache Spark를 사용하여 DStreams로 HDInsight의 Apache Kafka에(서) 데이터를 스트리밍하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="edcd1-107">이 예제에서는 Spark 클러스터에서 실행되는 Jupyter Notebook을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="edcd1-108">이 문서의 단계는 HDInsight의 Spark와 HDInsight의 Kafka 클러스터를 모두 포함하는 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="edcd1-109">이러한 클러스터는 모두 Azure Virtual Network에 있으며, 여기서는 Spark 클러스터와 Kafka 클러스터 간에 직접 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="edcd1-110">이 문서의 단계를 완료하는 경우 과도한 요금이 청구되지 않도록 클러스터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="edcd1-111">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="edcd1-111">Create the clusters</span></span>

<span data-ttu-id="edcd1-112">HDInsight의 Apache Kafka는 공용 인터넷을 통한 액세스를 Kafka broker에 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="edcd1-113">Kafka와 통신하는 대상은 Kafka 클러스터의 노드와 동일한 Azure 가상 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="edcd1-114">여기서는 Kafka 클러스터와 Spark 클러스터가 모두 Azure 가상 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="edcd1-115">클러스터 간의 통신 흐름을 보여 주는 다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-115">The following diagram shows how communication flows between the clusters:</span></span>

![Azure 가상 네트워크에 있는 Spark 및 Kafka 클러스터 다이어그램](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="edcd1-117">Kafka 자체는 가상 네트워크 내의 통신으로 제한되지만, 클러스터의 다른 서비스(예: SSH, Ambari)는 인터넷을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="edcd1-118">HDInsight에서 사용할 수 있는 공용 포트에 대한 자세한 내용은 [HDInsight에서 사용하는 포트 및 URI](hdinsight-hadoop-port-settings-for-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edcd1-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="edcd1-119">Azure 가상 네트워크, Kafka 클러스터 및 Spark 클러스터를 수동으로 만들 수 있지만 Azure Resource Manager 템플릿을 사용하는 것이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="edcd1-120">다음 단계에 따라 Azure 가상 네트워크, Kafka 클러스터 및 Spark 클러스터를 Azure 구독에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="edcd1-121">Azure에 로그인하고 Azure Portal에서 템플릿을 열려면 다음 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="edcd1-122">Azure Resource Manager 템플릿은 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="edcd1-123">HDInsight에서 Kafka의 사용 가능성을 보장하려면 클러스터에 작업자 노드가 3개 이상 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="edcd1-124">이 템플릿은 세 개의 작업자 노드를 포함하는 Kafka 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="edcd1-125">이 템플릿은 Kafka와 Spark 둘 다에 대해 HDInsight 3.6 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="edcd1-126">다음 정보를 사용하여 **사용자 지정 배포** 블레이드의 항목을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="edcd1-128">**리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="edcd1-129">이 그룹에는 HDInsight 클러스터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="edcd1-130">**위치**: 지리적으로 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="edcd1-131">**기본 클러스터 이름**: 이 값은 Spark 및 Kafka 클러스터의 기본 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="edcd1-132">예를 들어, **hdi**를 입력하면 spark-hdi__라는 Spark 클러스터와 **kafka-hdi**라는 Kafka 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="edcd1-133">**클러스터 로그인 사용자 이름**: Spark 및 Kafka 클러스터의 관리자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="edcd1-134">**클러스터 로그인 암호**: Spark 및 Kafka 클러스터의 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="edcd1-135">**SSH 사용자 이름**: Spark 및 Kafka 클러스터에 만들 SSH 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="edcd1-136">**SSH 암호**: Spark 및 Kafka 클러스터에 대한 SSH 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="edcd1-137">**사용 약관**을 읽은 다음 **위에 명시된 사용 약관에 동의함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="edcd1-138">마지막으로 **대시보드에 고정**을 선택한 다음 **구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="edcd1-139">클러스터를 만드는 데 약 20분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="edcd1-140">리소스를 만들면 클러스터 및 웹 대시보드를 포함하는 리소스 그룹에 대한 블레이드로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![vnet 및 클러스터에 대한 리소스 그룹 블레이드](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="edcd1-142">HDInsight 클러스터의 이름은 **spark-BASENAME** 및 **kafka-BASENAME**이며, 여기서 BASENAME은 템플릿에 제공된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="edcd1-143">이후 단계에서 클러스터에 연결할 때 이러한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="edcd1-144">노트북 사용</span><span class="sxs-lookup"><span data-stu-id="edcd1-144">Use the notebooks</span></span>

<span data-ttu-id="edcd1-145">이 문서에서 설명하는 예제 코드는 [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="edcd1-146">이 예제를 완료하려면 `README.md` 파일의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="edcd1-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="edcd1-147">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="edcd1-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="edcd1-148">이 문서의 단계를 수행하면 동일한 Azure 리소스 그룹에 두 클러스터가 모두 만들어지므로 Azure Portal에서 해당 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="edcd1-149">그룹을 삭제하면 이 문서의 단계를 수행하여 만들어진 모든 리소스, Azure Virtual Network 및 클러스터에서 사용하는 저장소 계정이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edcd1-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="edcd1-150">Next steps</span></span>

<span data-ttu-id="edcd1-151">이 예제에서는 Spark를 사용하여 Kafka에(서) 쓰고 읽는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="edcd1-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="edcd1-152">Kafka를 사용하는 다른 방법을 찾으려면 다음 링크를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="edcd1-152">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="edcd1-153">HDInsight에서 Apache Kafka 시작</span><span class="sxs-lookup"><span data-stu-id="edcd1-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="edcd1-154">MirrorMaker를 사용하여 HDInsight에 Kafka 복제본 만들기</span><span class="sxs-lookup"><span data-stu-id="edcd1-154">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="edcd1-155">HDInsight의 Kafka에서 Apache Storm 사용</span><span class="sxs-lookup"><span data-stu-id="edcd1-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

