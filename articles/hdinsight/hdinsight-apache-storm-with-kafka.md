---
title: "HDInsight의 Storm에서 Apache Kafka 사용 - Azure | Microsoft Docs"
description: "Apache Kafka는 HDInsight에 Apache Storm과 함께 설치됩니다. Storm에서 제공하는 KafkaBolt 및 KafkaSpout 구성 요소를 사용하여 Kafka에(서) 쓰고 읽는 방법에 대해 알아봅니다. 또한 Flux 프레임워크를 사용하여 Storm 토폴로지를 정의하고 제출하는 방법도 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: e8895ef3c11aea48513e4060a20f5f49b11fc961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="11cdc-105">HDInsight의 Storm에서 Apache Kafka(미리 보기) 사용</span><span class="sxs-lookup"><span data-stu-id="11cdc-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="11cdc-106">Apache Storm을 사용하여 Apache Kafka에서 읽고 쓰는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-106">Learn how to use Apache Storm to read from and write to Apache Kafka.</span></span> <span data-ttu-id="11cdc-107">이 예제에서는 HDInsight를 사용하여 Storm 토폴로지의 데이터를 HDFS 호환 파일 시스템에 저장하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-107">This example also demonstrates how to save data from a Storm topology to the HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="11cdc-108">이 문서의 단계는 HDInsight의 Storm과 HDInsight의 Kafka 클러스터를 모두 포함하는 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-108">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="11cdc-109">이러한 클러스터는 모두 Azure Virtual Network에 있으며, 여기서는 Storm 클러스터와 Kafka 클러스터 간에 직접 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-109">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="11cdc-110">이 문서의 단계를 완료하는 경우 과도한 요금이 청구되지 않도록 클러스터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="11cdc-111">코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="11cdc-111">Get the code</span></span>

<span data-ttu-id="11cdc-112">이 문서에서 사용하는 예제의 코드는 [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-112">The code for the example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="11cdc-113">이 프로젝트를 컴파일하려면 개발 환경에 대한 다음 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-113">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="11cdc-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상</span><span class="sxs-lookup"><span data-stu-id="11cdc-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="11cdc-115">- HDInsight 3.5 이상에는 Java 8이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="11cdc-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="11cdc-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="11cdc-117">SSH 클라이언트(`ssh` 및 `scp` 명령 필요) - 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-117">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="11cdc-118">텍스트 편집기 또는 IDE</span><span class="sxs-lookup"><span data-stu-id="11cdc-118">A text editor or IDE.</span></span>

<span data-ttu-id="11cdc-119">Java 및 JDK를 설치할 때 사용자의 개발 워크스테이션에 다음 환경 변수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-119">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="11cdc-120">하지만 변수가 존재하며 시스템에 대한 올바른 값을 포함하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-120">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="11cdc-121">`JAVA_HOME` - JDK가 설치된 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-121">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="11cdc-122">`PATH` - 다음 경로를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-122">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="11cdc-123">`JAVA_HOME`(또는 이와 동등한 경로)</span><span class="sxs-lookup"><span data-stu-id="11cdc-123">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="11cdc-124">`JAVA_HOME\bin`(또는 이와 동등한 경로)</span><span class="sxs-lookup"><span data-stu-id="11cdc-124">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="11cdc-125">Maven이 설치된 디렉터리</span><span class="sxs-lookup"><span data-stu-id="11cdc-125">The directory where Maven is installed.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="11cdc-126">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="11cdc-126">Create the clusters</span></span>

<span data-ttu-id="11cdc-127">HDInsight의 Apache Kafka는 공용 인터넷을 통한 액세스를 Kafka broker에 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-127">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="11cdc-128">Kafka와 통신하는 대상은 Kafka 클러스터의 노드와 동일한 Azure 가상 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-128">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="11cdc-129">여기서는 Kafka 클러스터와 Storm 클러스터가 모두 Azure 가상 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-129">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="11cdc-130">클러스터 간의 통신 흐름을 보여 주는 다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-130">The following diagram shows how communication flows between the clusters:</span></span>

![Azure 가상 네트워크에 있는 Storm 및 Kafka 클러스터 다이어그램](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="11cdc-132">SSH 및 Ambari와 같은 클러스터의 다른 서비스는 인터넷을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-132">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="11cdc-133">HDInsight에서 사용할 수 있는 공용 포트에 대한 자세한 내용은 [HDInsight에서 사용하는 포트 및 URI](hdinsight-hadoop-port-settings-for-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11cdc-133">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="11cdc-134">Azure 가상 네트워크, Kafka 클러스터 및 Storm 클러스터를 수동으로 만들 수 있지만 Azure Resource Manager 템플릿을 사용하는 것이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="11cdc-135">다음 단계에 따라 Azure 가상 네트워크, Kafka 클러스터 및 Storm 클러스터를 Azure 구독에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-135">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="11cdc-136">Azure에 로그인하고 Azure Portal에서 템플릿을 열려면 다음 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-136">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="11cdc-137">Azure Resource Manager 템플릿은 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-137">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="11cdc-138">이 템플릿은 다음 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-138">It creates the following resources:</span></span>
    
    * <span data-ttu-id="11cdc-139">Azure 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="11cdc-139">Azure resource group</span></span>
    * <span data-ttu-id="11cdc-140">Azure 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="11cdc-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="11cdc-141">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="11cdc-141">Azure Storage account</span></span>
    * <span data-ttu-id="11cdc-142">HDInsight 버전 3.6의 Kafka(작업자 노드 3개)</span><span class="sxs-lookup"><span data-stu-id="11cdc-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="11cdc-143">HDInsight 버전 3.6의 Storm(작업자 노드 3개)</span><span class="sxs-lookup"><span data-stu-id="11cdc-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="11cdc-144">HDInsight에서 Kafka의 사용 가능성을 보장하려면 클러스터에 작업자 노드가 3개 이상 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-144">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="11cdc-145">이 템플릿은 세 개의 작업자 노드를 포함하는 Kafka 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="11cdc-146">다음 지침을 사용하여 **사용자 지정 배포** 블레이드의 항목을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-146">Use the following guidance to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="11cdc-148">**리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="11cdc-149">이 그룹에는 HDInsight 클러스터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-149">This group contains the HDInsight cluster.</span></span>
   
    * <span data-ttu-id="11cdc-150">**위치**: 지리적으로 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-150">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="11cdc-151">**기본 클러스터 이름**: 이 값은 Storm 및 Kafka 클러스터의 기본 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-151">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span></span> <span data-ttu-id="11cdc-152">예를 들어 **hdi**를 입력하면 **storm-hdi**라는 Storm 클러스터와 **kafka-hdi**라는 Kafka 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="11cdc-153">**클러스터 로그인 사용자 이름**: Storm 및 Kafka 클러스터의 관리자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-153">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="11cdc-154">**클러스터 로그인 암호**: Storm 및 Kafka 클러스터의 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-154">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="11cdc-155">**SSH 사용자 이름**: Storm 및 Kafka 클러스터에 만들 SSH 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-155">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="11cdc-156">**SSH 암호**: Storm 및 Kafka 클러스터에 대한 SSH 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-156">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="11cdc-157">**사용 약관**을 읽은 다음 **위에 명시된 사용 약관에 동의함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="11cdc-158">마지막으로 **대시보드에 고정**을 선택한 다음 **구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="11cdc-159">클러스터를 만드는 데 약 20분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-159">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="11cdc-160">리소스를 만들면 리소스 그룹의 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-160">Once the resources have been created, the blade for the resource group is displayed.</span></span>

![vnet 및 클러스터에 대한 리소스 그룹 블레이드](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="11cdc-162">HDInsight 클러스터의 이름은 **storm-BASENAME** 및 **kafka-BASENAME**이며, 여기서 BASENAME은 템플릿에 제공된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-162">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="11cdc-163">이후 단계에서 클러스터에 연결할 때 이러한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-163">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="11cdc-164">코드 이해</span><span class="sxs-lookup"><span data-stu-id="11cdc-164">Understanding the code</span></span>

<span data-ttu-id="11cdc-165">이 프로젝트에는 다음 두 가지 토폴로지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-165">This project contains two topologies:</span></span>

* <span data-ttu-id="11cdc-166">**KafkaWriter**: **writer.yaml** 파일에 정의된 토폴로지이며, Apache Storm에서 제공하는 KafkaBolt를 사용하여 Kafka에 임의의 문장을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-166">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="11cdc-167">이 토폴로지는 사용자 지정 **SentenceSpout** 구성 요소를 사용하여 임의의 문장을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-167">This topology uses a custom **SentenceSpout** component to generate random sentences.</span></span>

* <span data-ttu-id="11cdc-168">**KafkaReader**: **reader.yaml** 파일에 정의된 토폴로지이며, Apache Storm에서 제공하는 KafkaSpout을 사용하여 Kafka에서 데이터를 읽은 다음 stdout에 데이터를 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-168">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span></span>

    <span data-ttu-id="11cdc-169">이 토폴로지는 Storm HdfsBolt를 사용하여 Storm 클러스터의 기본 저장소에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-169">This topology uses the Storm HdfsBolt to write data to default storage for the Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="11cdc-170">Flux</span><span class="sxs-lookup"><span data-stu-id="11cdc-170">Flux</span></span>

<span data-ttu-id="11cdc-171">토폴로지는 [Flux](https://storm.apache.org/releases/1.1.0/flux.html)를 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-171">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="11cdc-172">Flux는 Storm 0.10.x에서 소개되었으며, 토폴로지 구성을 코드에서 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-172">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="11cdc-173">Flux 프레임워크를 사용하는 토폴로지의 경우 토폴로지는 YAML 파일에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-173">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="11cdc-174">YAML 파일은 토폴로지의 일부로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-174">The YAML file can be included as part of the topology.</span></span> <span data-ttu-id="11cdc-175">또는 토폴로지를 전송할 때 독립 실행형 파일로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-175">It can also be a standalone file used when you submit the topology.</span></span> <span data-ttu-id="11cdc-176">Flux는 런타임 시 변수 대체도 지원하며, 이 예제에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="11cdc-177">이러한 토폴로지에 대해 런타임에 다음 매개 변수가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-177">The following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="11cdc-178">`${kafka.topic}`: 토폴리지에서 읽고 쓰는 Kafka 토픽의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-178">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="11cdc-179">`${kafka.broker.hosts}`: Kafka broker가 실행되는 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-179">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="11cdc-180">broker 정보는 Kafka에 쓸 때 KafkaBolt에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-180">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="11cdc-181">`${kafka.zookeeper.hosts}`: Kafka 클러스터에서 Zookeeper가 실행되는 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-181">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span></span>

<span data-ttu-id="11cdc-182">Flux 토폴로지에 대한 자세한 내용은 [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11cdc-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-the-project"></a><span data-ttu-id="11cdc-183">프로젝트 다운로드 및 컴파일</span><span class="sxs-lookup"><span data-stu-id="11cdc-183">Download and compile the project</span></span>

1. <span data-ttu-id="11cdc-184">개발 환경에서 [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)로부터 프로젝트를 다운로드하고, 명령줄을 열어 다운로드한 위치로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-184">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

2. <span data-ttu-id="11cdc-185">**hdinsight-storm-java-kafka** 디렉터리에서 다음 명령을 사용하여 프로젝트를 컴파일하고 배포할 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-185">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="11cdc-186">패키지 프로세스는 `target` 디렉터리에 `KafkaTopology-1.0-SNAPSHOT.jar`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-186">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="11cdc-187">다음 명령을 사용하여 HDInsight 클러스터의 Storm에 패키지를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-187">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="11cdc-188">**USERNAME**은 클러스터의 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-188">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="11cdc-189">**BASENAME**은 클러스터를 만들 때 사용한 기본 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-189">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="11cdc-190">메시지가 표시되면 클러스터를 만들 때 사용한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-190">When prompted, enter the password you used when creating the clusters.</span></span>

## <a name="configure-the-topology"></a><span data-ttu-id="11cdc-191">토폴로지 구성</span><span class="sxs-lookup"><span data-stu-id="11cdc-191">Configure the topology</span></span>

1. <span data-ttu-id="11cdc-192">다음 방법 중 하나를 사용하여 Kafka broker 호스트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-192">Use one of the following methods to discover the Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="11cdc-193">Bash 예제에서는 `$CLUSTERNAME`에 HDInsight 클러스터 이름이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-193">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="11cdc-194">[jq](https://stedolan.github.io/jq/)도 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="11cdc-195">메시지가 표시되면 클러스터 로그인 계정에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-195">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="11cdc-196">반환되는 값은 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-196">The value returned is similar to the following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="11cdc-197">클러스터에 대해 두 개 이상의 브로커 호스트가 있을 수 있습니다. 클라이언트에 대한 모든 호스트의 전체 목록을 제공할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-197">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="11cdc-198">하나 또는 두 개로도 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-198">One or two is enough.</span></span>

2. <span data-ttu-id="11cdc-199">다음 방법 중 하나를 사용하여 Kafka Zookeeper 호스트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-199">Use one of the following methods to discover the Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="11cdc-200">Bash 예제에서는 `$CLUSTERNAME`에 HDInsight 클러스터 이름이 포함되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-200">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="11cdc-201">[jq](https://stedolan.github.io/jq/)도 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="11cdc-202">메시지가 표시되면 클러스터 로그인 계정에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-202">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="11cdc-203">반환되는 값은 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-203">The value returned is similar to the following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="11cdc-204">두 개 이상의 Zookeeper 노드가 있습니다. 클라이언트에 대한 모든 호스트의 전체 목록을 제공할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-204">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="11cdc-205">하나 또는 두 개로도 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-205">One or two is enough.</span></span>

    <span data-ttu-id="11cdc-206">나중에 사용하므로 이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="11cdc-207">프로젝트의 루트에서 `dev.properties` 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-207">Edit the `dev.properties` file in the root of the project.</span></span> <span data-ttu-id="11cdc-208">이 파일에서 일치하는 줄에 Broker 및 Zookeeper 호스트 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-208">Add the Broker and Zookeeper hosts information to the matching lines in this file.</span></span> <span data-ttu-id="11cdc-209">다음 예제는 이전 단계의 예제 값을 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-209">The following example is configured using the sample values from the previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="11cdc-210">`dev.properties` 파일을 저장하고 다음 명령을 사용하여 Storm 클러스터로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-210">Save the `dev.properties` file and then use the following command to upload it to the Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="11cdc-211">**USERNAME**은 클러스터의 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-211">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="11cdc-212">**BASENAME**은 클러스터를 만들 때 사용한 기본 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-212">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="11cdc-213">기록기 시작</span><span class="sxs-lookup"><span data-stu-id="11cdc-213">Start the writer</span></span>

1. <span data-ttu-id="11cdc-214">다음을 사용하여 SSH를 사용하는 Storm 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-214">Use the following to connect to the Storm cluster using SSH.</span></span> <span data-ttu-id="11cdc-215">**USERNAME**은 클러스터를 만들 때 사용한 SSH 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-215">Replace **USERNAME** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="11cdc-216">**BASENAME**은 클러스터를 만들 때 사용한 기본 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-216">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="11cdc-217">메시지가 표시되면 클러스터를 만들 때 사용한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-217">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="11cdc-218">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11cdc-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="11cdc-219">SSH 연결에서 다음 명령을 사용하여 토폴로지에서 사용하는 Kafka 토픽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-219">From the SSH connection, use the following command to create the Kafka topic used by the topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="11cdc-220">`$KAFKAZKHOSTS`를 이전 섹션에서 검색한 Zookeeper 호스트 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-220">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

2. <span data-ttu-id="11cdc-221">Storm 클러스터에 대한 SSH 연결에서 다음 명령을 사용하여 기록기 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-221">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="11cdc-222">이 명령에서 사용된 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-222">The parameters used with this command are:</span></span>

    * <span data-ttu-id="11cdc-223">`org.apache.storm.flux.Flux`: Flux를 사용하여 이 토폴로지를 구성하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-223">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="11cdc-224">`--remote`: Nimbus에 토폴로지를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-224">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="11cdc-225">토폴로지가 클러스터의 작업자 노드에 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-225">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="11cdc-226">`-R /writer.yaml`: `writer.yaml` 파일을 사용하여 토폴로지를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-226">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="11cdc-227">`-R`은 이 리소스가 jar 파일에 포함되어 있는지를 나타내며,</span><span class="sxs-lookup"><span data-stu-id="11cdc-227">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="11cdc-228">jar의 루트에 있으므로 `/writer.yaml`이 그 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-228">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="11cdc-229">`--filter`: `dev.properties` 파일의 값을 사용하여 `writer.yaml` 토폴로지의 항목을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-229">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span></span> <span data-ttu-id="11cdc-230">예를 들어 파일에서 `kafka.topic` 항목의 값으로 토폴로지 정의의 `${kafka.topic}` 항목을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-230">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span></span>

5. <span data-ttu-id="11cdc-231">토폴로지가 시작되면 다음 명령을 사용하여 Kafka 토픽에 데이터를 쓰는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-231">Once the topology has started, use the following command to verify that it is writing data to the Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="11cdc-232">`$KAFKAZKHOSTS`를 이전 섹션에서 검색한 Zookeeper 호스트 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-232">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

    <span data-ttu-id="11cdc-233">이 명령은 Kafka에서 제공하는 스크립트를 사용하여 토픽을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-233">This command uses a script shipped with Kafka to monitor the topic.</span></span> <span data-ttu-id="11cdc-234">잠시 후에 토픽에 기록된 임의의 문장을 반환하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-234">After a moment, it should start returning random sentences that have been written to the topic.</span></span> <span data-ttu-id="11cdc-235">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-235">The output is similar to the following example:</span></span>

        i am at two with nature             
        an apple a day keeps the doctor away
        snow white and the seven dwarfs     
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        four score and seven years ago      
        snow white and the seven dwarfs     
        snow white and the seven dwarfs     
        i am at two with nature             
        an apple a day keeps the doctor away

    <span data-ttu-id="11cdc-236">Ctrl+C를 사용하여 스크립트를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-236">Use Ctrl+c to stop the script.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="11cdc-237">판독기 시작</span><span class="sxs-lookup"><span data-stu-id="11cdc-237">Start the reader</span></span>

1. <span data-ttu-id="11cdc-238">Storm 클러스터에 대한 SSH 세션에서 다음 명령을 사용하여 판독기 토폴로지를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-238">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="11cdc-239">토폴로지가 시작되면 Storm UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-239">Once the topology starts, open the Storm UI.</span></span> <span data-ttu-id="11cdc-240">이 웹 UI는 https://storm-BASENAME.azurehdinsight.net/stormui에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="11cdc-241">__BASENAME__은 클러스터를 만들 때 사용한 기본 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-241">Replace __BASENAME__ with the base name used when the cluster was created.</span></span> 

    <span data-ttu-id="11cdc-242">메시지가 표시되면 클러스터를 만들 때 사용한 관리자 로그인 이름(기본값: `admin`)과 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-242">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span></span> <span data-ttu-id="11cdc-243">다음 이미지와 비슷한 웹 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-243">You see a web page similar to the following image:</span></span>

    ![Storm UI](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="11cdc-245">Storm UI의 __토폴로지 요약__ 섹션에서 __kafka-reader__ 링크를 선택하여 __kafka-reader__ 토폴로지에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-245">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span></span>

    ![Storm 웹 UI의 토폴로지 요약 섹션](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="11cdc-247">logger-bolt 구성 요소의 인스턴스에 대한 정보를 표시하려면 __Bolt(모든 시간)__ 섹션에서 __logger-bolt__ 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-247">To display information about the instances of the logger-bolt component, select the __logger-bolt__ link in the __Bolts (All time)__ section.</span></span>

    ![Bolt 섹션의 logger-bolt 링크](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="11cdc-249">__실행자__ 섹션에서 __포트__ 열의 링크를 선택하여 구성 요소의 이 인스턴스에 대한 로깅 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-249">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span></span>

    ![실행자 링크](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="11cdc-251">로그에는 Kafka 토픽에서 읽은 데이터의 로그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-251">The log contains a log of the data read from the Kafka topic.</span></span> <span data-ttu-id="11cdc-252">로그 정보는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-252">The information in the log is similar to the following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] the cow jumped over the moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: the cow jumped over the moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps the doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="11cdc-253">토폴로지 중지</span><span class="sxs-lookup"><span data-stu-id="11cdc-253">Stop the topologies</span></span>

<span data-ttu-id="11cdc-254">Storm 클러스터에 대한 SSH 세션에서 다음 명령을 사용하여 Storm 토폴로지를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-254">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-the-cluster"></a><span data-ttu-id="11cdc-255">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="11cdc-255">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="11cdc-256">이 문서의 단계를 수행하면 동일한 Azure 리소스 그룹에 두 클러스터가 모두 만들어지므로 Azure Portal에서 해당 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-256">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="11cdc-257">리소스 그룹을 삭제하면 이 문서에 따라 만든 리소스가 모두 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="11cdc-257">Deleting the resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11cdc-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11cdc-258">Next steps</span></span>

<span data-ttu-id="11cdc-259">HDInsight의 Storm에서 사용할 수 있는 더 많은 예제 토폴로지는 [예제 Storm 토폴로지 및 구성 요소](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11cdc-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="11cdc-260">Linux 기반 HDInsight에서 토폴로지 배포 및 모니터링에 대한 정보는 [Linux 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11cdc-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>