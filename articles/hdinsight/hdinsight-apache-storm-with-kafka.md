---
title: "HDInsight-Azure의 Storm와 Apache Kafka aaaUse | Microsoft Docs"
description: "Apache Kafka는 HDInsight에 Apache Storm과 함께 설치됩니다. 어떻게 toowrite tooKafka 및 사용 하 여 여기에서 다음 읽기 hello Storm 함께 제공 된 KafkaBolt 및 KafkaSpout 구성 요소에 알아봅니다. 또한 toouse 표적이 프레임 워크 toodefine hello 하 및 스톰 토폴로지를 제출 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="393c5-105">HDInsight의 Storm에서 Apache Kafka(미리 보기) 사용</span><span class="sxs-lookup"><span data-stu-id="393c5-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="393c5-106">자세한 방법에서 toouse Apache Storm tooread 및 tooApache Kafka 쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="393c5-107">이 예제에서는 또한 스톰 토폴로지 toohello HDFS 호환에서에서 toosave 데이터 파일을 시스템 HDInsight에서 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="393c5-108">이 문서의 단계 hello HDInsight의 Storm와 HDInsight 클러스터에서 Kafka 모두 포함 된 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="393c5-109">이 클러스터는 Storm 클러스터 toodirectly hello를는 Azure 가상 네트워크 내에 위치한 둘 다 hello Kafka 클러스터와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="393c5-110">Hello이이 문서의 단계를 완료 하는 경우 toodelete hello 클러스터 tooavoid 초과 요금을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="393c5-111">Hello 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="393c5-111">Get hello code</span></span>

<span data-ttu-id="393c5-112">이 문서에 사용 되는 hello 예제에 대 한 hello 코드에서 사용할 수는 [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="393c5-113">toocompile이이 프로젝트를 hello 같은 개발 환경에 대 한 구성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="393c5-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상</span><span class="sxs-lookup"><span data-stu-id="393c5-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="393c5-115">- HDInsight 3.5 이상에는 Java 8이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="393c5-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="393c5-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="393c5-117">SSH 클라이언트 (hello 필요한 `ssh` 및 `scp` 명령)-내용은 참조 [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="393c5-118">텍스트 편집기 또는 IDE</span><span class="sxs-lookup"><span data-stu-id="393c5-118">A text editor or IDE.</span></span>

<span data-ttu-id="393c5-119">hello 다음과 같은 환경 변수 설정 되어 있습니다 Java와 hello JDK 개발용 워크스테이션에 설치 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="393c5-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="393c5-120">그러나 시스템에 대 한 올바른 값 hello를 포함 하 고 있는 것을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="393c5-121">`JAVA_HOME`-toohello hello JDK가 설치 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="393c5-122">`PATH`-경로 따라 hello를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="393c5-123">`JAVA_HOME`(또는 hello 해당 하는 경로)입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="393c5-124">`JAVA_HOME\bin`(또는 hello 해당 하는 경로)입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="393c5-125">Maven 설치 되어 있는 hello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="393c5-126">Hello 클러스터를 만들려면</span><span class="sxs-lookup"><span data-stu-id="393c5-126">Create hello clusters</span></span>

<span data-ttu-id="393c5-127">HDInsight의 Apache Kafka에서는 액세스 toohello Kafka 브로커를 통해 공용 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="393c5-128">토론에 tooKafka 있어야 hello hello 노드로 동일한 Azure 가상 네트워크는 모든 작업이 hello Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="393c5-129">예를 들어 hello Kafka 및 Storm 클러스터를 모두 Azure 가상 네트워크에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="393c5-130">hello 다음 그림에 hello 클러스터 간의 통신 흐름 방식을:</span><span class="sxs-lookup"><span data-stu-id="393c5-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Azure 가상 네트워크에 있는 Storm 및 Kafka 클러스터 다이어그램](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="393c5-132">SSH 및 Ambari를 통해 액세스할 수와 같은 hello 클러스터에 있는 다른 서비스는 인터넷에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="393c5-133">HDInsight와 사용할 수 있는 공용 포트 hello에 대 한 자세한 내용은 참조 하십시오. [포트 및 HDInsight에서 사용 하는 Uri](hdinsight-hadoop-port-settings-for-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="393c5-134">Storm 클러스터를 수동으로 Kafka, Azure 가상 네트워크를 만들 수는 것 보다 쉽게 toouse Azure 리소스 관리자 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="393c5-135">사용 하 여 hello 다음 단계는 Azure 가상 네트워크, Kafka toodeploy 및 Storm 클러스터 tooyour Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="393c5-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="393c5-136">Hello tooAzure에서 단추 toosign 및 hello Azure 포털에서에서 열기 hello 서식 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="393c5-137">hello Azure 리소스 관리자 템플릿에 위치한 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="393c5-138">다음 리소스는 hello를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="393c5-139">Azure 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="393c5-139">Azure resource group</span></span>
    * <span data-ttu-id="393c5-140">Azure 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="393c5-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="393c5-141">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="393c5-141">Azure Storage account</span></span>
    * <span data-ttu-id="393c5-142">HDInsight 버전 3.6의 Kafka(작업자 노드 3개)</span><span class="sxs-lookup"><span data-stu-id="393c5-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="393c5-143">HDInsight 버전 3.6의 Storm(작업자 노드 3개)</span><span class="sxs-lookup"><span data-stu-id="393c5-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="393c5-144">HDInsight의 Kafka의 tooguarantee 가용성, 클러스터 3 개 이상의 작업자 노드를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="393c5-145">이 템플릿은 세 개의 작업자 노드를 포함하는 Kafka 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="393c5-146">지침 toopopulate hello 항목에 나오는 hello에 사용 하 여 hello **사용자 지정 배포** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="393c5-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="393c5-148">**리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="393c5-149">이 그룹 hello HDInsight 클러스터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="393c5-150">**위치**: 위치 지리적으로 닫기 tooyou를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="393c5-151">**기본 클러스터 이름을**:이 값 hello hello 스톰 및 Kafka 클러스터에 대 한 기본 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="393c5-152">예를 들어 **hdi**를 입력하면 **storm-hdi**라는 Storm 클러스터와 **kafka-hdi**라는 Kafka 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="393c5-153">**클러스터 로그인 사용자 이름**: hello 스톰 및 Kafka 클러스터에 대 한 hello 관리자 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="393c5-154">**로그인 암호 클러스터**: hello 스톰 및 Kafka 클러스터에 대 한 hello 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="393c5-155">**SSH 사용자 이름이**: hello 스톰 및 Kafka 클러스터에 대 한 SSH 사용자 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="393c5-156">**SSH 암호**: hello 스톰 및 Kafka 클러스터에 대 한 SSH 사용자 hello에 대 한 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="393c5-157">읽기 hello **약관**를 선택한 후 **toohello 약관 위에서 설명한 동의**합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="393c5-158">마지막으로 확인 **Pin toodashboard** 선택한 후 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="393c5-159">Hello 클러스터 toocreate 약 20 분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="393c5-160">Hello 리소스를 만든 후 hello 리소스 그룹에 대 한 hello 블레이드가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Hello vnet 및 클러스터 리소스 그룹 블레이드](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="393c5-162">Hello HDInsight 클러스터의 이름이 hello **스톰 BASENAME** 및 **kafka BASENAME**, 여기서 BASENAME는 hello 이름이 toohello 서식 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="393c5-163">Toohello 클러스터를 연결 하는 경우 이후 단계에서 이러한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="393c5-164">Hello 코드 이해</span><span class="sxs-lookup"><span data-stu-id="393c5-164">Understanding hello code</span></span>

<span data-ttu-id="393c5-165">이 프로젝트에는 다음 두 가지 토폴로지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-165">This project contains two topologies:</span></span>

* <span data-ttu-id="393c5-166">**KafkaWriter**: hello 정의한 **writer.yaml** 파일을이 토폴로지에 Apache Storm와 함께 제공 되는 KafkaBolt hello를 사용 하 여 임의의 문장 tooKafka 씁니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="393c5-167">사용자 지정을 사용 하 여이 토폴로지 **SentenceSpout** toogenerate 임의의 문장 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="393c5-168">**KafkaReader**: hello 정의한 **reader.yaml** 파일을이 토폴로지에에서 데이터를 읽고 Kafka Apache Storm와 함께 제공 되는 KafkaSpout hello를 사용 하 여 다음 로그 데이터 toostdout hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="393c5-169">이 토폴로지는 hello Storm 클러스터에 대 한 hello 스톰 HdfsBolt toowrite 데이터 toodefault 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="393c5-170">Flux</span><span class="sxs-lookup"><span data-stu-id="393c5-170">Flux</span></span>

<span data-ttu-id="393c5-171">hello 토폴로지를 사용 하 여 정의 된 [표적이](https://storm.apache.org/releases/1.1.0/flux.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="393c5-172">결정에 도입 된 스톰 0.10. x 하 고 hello 코드에서 tooseparate hello 토폴로지 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="393c5-173">Hello 표적이 프레임 워크를 사용 하는 토폴로지에서 hello 토폴로지 YAML 파일에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="393c5-174">hello YAML 파일 hello 토폴로지의 일부로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="393c5-175">Hello 토폴로지를 전송할 때 사용 하는 독립 실행형 파일 일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="393c5-176">Flux는 런타임 시 변수 대체도 지원하며, 이 예제에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="393c5-177">hello 다음 매개 변수가 설정 이러한 토폴로지에 대 한 실행 시:</span><span class="sxs-lookup"><span data-stu-id="393c5-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="393c5-178">`${kafka.topic}`: hello 이름 hello Kafka 항목을 읽기/쓰기를 hello 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="393c5-179">`${kafka.broker.hosts}`: hello에서 실행 하는 hello Kafka 브로커를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="393c5-180">hello broker 정보 tooKafka를 작성할 때 hello KafkaBolt에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="393c5-181">`${kafka.zookeeper.hosts}`: 사육에서 실행 하는 hello 호스트 hello Kafka 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="393c5-182">Flux 토폴로지에 대한 자세한 내용은 [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="393c5-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="393c5-183">다운로드 하 고 hello 프로젝트 컴파일</span><span class="sxs-lookup"><span data-stu-id="393c5-183">Download and compile hello project</span></span>

1. <span data-ttu-id="393c5-184">hello 프로젝트를 다운로드 하 여 개발 환경에 [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)를 명령줄을 열고 hello 프로젝트를 다운로드 한 디렉터리 toohello 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="393c5-185">Hello에서 **스톰 java kafka hdinsight** 디렉터리 사용 하 여 hello 다음 toocompile hello 프로젝트 명령 및 배포에 대 한 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="393c5-186">hello 패키지 프로세스 라는 파일을 만듭니다 `KafkaTopology-1.0-SNAPSHOT.jar` hello에 `target` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="393c5-187">Hello 명령을 toocopy hello 패키지 tooyour 스톰 HDInsight 클러스터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="393c5-188">대체 **USERNAME** hello 클러스터에 대 한 hello SSH 사용자 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="393c5-189">대체 **BASENAME** hello 클러스터를 만들 때 사용한를 hello 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="393c5-190">메시지가 표시 되 면 hello 클러스터를 만들 때 사용한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="393c5-191">Hello 토폴로지 구성</span><span class="sxs-lookup"><span data-stu-id="393c5-191">Configure hello topology</span></span>

1. <span data-ttu-id="393c5-192">Hello toodiscover 메서드를 다음 중 하나를 사용 하 여 hello Kafka 브로커 호스트:</span><span class="sxs-lookup"><span data-stu-id="393c5-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
    > <span data-ttu-id="393c5-193">hello Bash 가정 `$CLUSTERNAME` hello HDInsight 클러스터의 hello 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="393c5-194">[jq](https://stedolan.github.io/jq/)도 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="393c5-195">메시지가 표시 되 면 hello 클러스터 로그인 계정에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="393c5-196">반환 된 hello 값은 텍스트 다음 비슷한 toohello:</span><span class="sxs-lookup"><span data-stu-id="393c5-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="393c5-197">클러스터에 대해 두 개 이상의 브로커 호스트 있을 수 있습니다 하는 동안에 모든 호스트 tooclients의 전체 목록은 tooprovide를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="393c5-198">하나 또는 두 개로도 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-198">One or two is enough.</span></span>

2. <span data-ttu-id="393c5-199">Hello 메서드 toodiscover hello Kafka 사육 호스트를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
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
    > <span data-ttu-id="393c5-200">hello Bash 가정 `$CLUSTERNAME` hello HDInsight 클러스터의 hello 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="393c5-201">[jq](https://stedolan.github.io/jq/)도 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="393c5-202">메시지가 표시 되 면 hello 클러스터 로그인 계정에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="393c5-203">반환 된 hello 값은 텍스트 다음 비슷한 toohello:</span><span class="sxs-lookup"><span data-stu-id="393c5-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="393c5-204">두 개 이상의 사육 노드가 하는 동안에 모든 호스트 tooclients의 전체 목록은 tooprovide를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="393c5-205">하나 또는 두 개로도 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-205">One or two is enough.</span></span>

    <span data-ttu-id="393c5-206">나중에 사용하므로 이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="393c5-207">Hello 편집 `dev.properties` hello 프로젝트의 hello 루트에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="393c5-208">이 파일에 hello 브로커 및 사육 호스트 정보 toohello 일치 하는 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="393c5-209">hello 다음 예제에서는 구성 된 hello 이전 단계에서 hello 예제 값을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="393c5-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="393c5-210">Hello 저장 `dev.properties` 파일과 hello 명령 tooupload 다음 그 toohello Storm 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="393c5-211">대체 **USERNAME** hello 클러스터에 대 한 hello SSH 사용자 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="393c5-212">대체 **BASENAME** hello 클러스터를 만들 때 사용한를 hello 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="393c5-213">Hello 작성기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-213">Start hello writer</span></span>

1. <span data-ttu-id="393c5-214">Hello tooconnect toohello Storm 클러스터 SSH를 사용 하 여 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="393c5-215">대체 **USERNAME** hello SSH 사용자 이름이 hello 클러스터를 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="393c5-216">대체 **BASENAME** 를 hello hello 클러스터를 만들 때 사용 되는 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="393c5-217">메시지가 표시 되 면 hello 클러스터를 만들 때 사용한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="393c5-218">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="393c5-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="393c5-219">SSH 연결 hello에서 다음 명령 toocreate hello Kafka 항목 hello 토폴로지에서 사용 하는 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="393c5-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="393c5-220">대체 `$KAFKAZKHOSTS` 사육 hello로 hello 이전 섹션에서 검색 된 정보를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="393c5-221">Hello SSH 연결 toohello Storm 클러스터에서 다음 명령 toostart hello 기록기 토폴로지 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="393c5-222">이 명령과 함께 사용 하는 hello 매개 변수는.</span><span class="sxs-lookup"><span data-stu-id="393c5-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="393c5-223">`org.apache.storm.flux.Flux`: 표적이 tooconfigure를 사용 하 고이 토폴로지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="393c5-224">`--remote`: Hello 토폴로지 tooNimbus 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="393c5-225">hello 토폴로지 hello 클러스터의 작업자 노드 hello 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="393c5-226">`-R /writer.yaml`: 사용 하 여 hello `writer.yaml` tooconfigure hello 토폴로지 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="393c5-227">`-R`이 리소스 hello jar 파일에 포함 되어 있는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="393c5-228">따라서 hello jar의 hello 루트에서이 `/writer.yaml` hello 경로 tooit 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="393c5-229">`--filter`: Hello에 항목을 채우는 `writer.yaml` hello에 값을 사용 하 여 토폴로지 `dev.properties` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="393c5-230">예를 들어 hello의 값을 hello `kafka.topic` hello 파일 항목에에서는 사용 되는 tooreplace hello `${kafka.topic}` hello 토폴로지 정의 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="393c5-231">Hello 토폴로지가 시작 되 면 다음 명령 tooverify 데이터 toohello Kafka 항목을 작성 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="393c5-232">대체 `$KAFKAZKHOSTS` 사육 hello로 hello 이전 섹션에서 검색 된 정보를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="393c5-233">이 명령은 Kafka toomonitor hello 항목와 함께 제공 되는 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="393c5-234">잠시 후 toohello 항목 기록 된 임의의 문장 반환 하기 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="393c5-235">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="393c5-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="393c5-236">Ctrl + c toostop hello 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="393c5-237">Hello 판독기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-237">Start hello reader</span></span>

1. <span data-ttu-id="393c5-238">Hello SSH 세션 toohello Storm 클러스터에서 다음 명령 toostart hello 판독기 토폴로지 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="393c5-239">Hello 토폴로지 시작 되 면 hello 스톰 UI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="393c5-240">이 웹 UI는 https://storm-BASENAME.azurehdinsight.net/stormui에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="393c5-241">대체 __BASENAME__ hello 기본 이름이 hello 클러스터를 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="393c5-242">요청 시 사용 hello 관리자 로그인 이름 (기본적으로 `admin`) 및 hello 클러스터를 만들 때 사용한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="393c5-243">다음 이미지는 웹 페이지와 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-243">You see a web page similar toohello following image:</span></span>

    ![Storm UI](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="393c5-245">Hello 스톰 UI에서에서 선택 hello __kafka 판독기__ hello에 대 한 링크 __토폴로지 요약__ hello에 대 한 toodisplay 정보 섹션 __kafka 판독기__ 토폴로지입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Hello 스톰 웹 UI의 요약 섹션 토폴로지](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="393c5-247">hello 인스턴스의 선택 hello hello로 거 볼트 구성 요소에 대 한 정보 toodisplay __로 거 볼트__ hello에 대 한 링크 __볼트 (항상)__ 섹션.</span><span class="sxs-lookup"><span data-stu-id="393c5-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Hello 볼트 섹션에서로 거 볼트 링크](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="393c5-249">Hello에 __Executor__ 섹션에서 hello에서 링크를 선택 __포트__ 열 toodisplay 기록은 hello 구성 요소의이 인스턴스에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![실행자 링크](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="393c5-251">hello 로그 hello Kafka 항목에서에서 읽은 hello 데이터 로그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="393c5-252">hello 로그의 hello 정보는 텍스트 다음 유사한 toohello:</span><span class="sxs-lookup"><span data-stu-id="393c5-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="393c5-253">Hello 토폴로지를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-253">Stop hello topologies</span></span>

<span data-ttu-id="393c5-254">SSH 세션 toohello Storm 클러스터에서 다음 명령을 toostop hello 스톰 토폴로지 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="393c5-255">Hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="393c5-256">이 문서의 단계 hello 만들 둘 다에서 클러스터 hello 같은 Azure 리소스 그룹, hello Azure 포털의에서 hello 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="393c5-257">이 문서에 따라 생성 된 모든 리소스를 제거 하는 hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="393c5-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="393c5-258">다음 단계</span><span class="sxs-lookup"><span data-stu-id="393c5-258">Next steps</span></span>

<span data-ttu-id="393c5-259">HDInsight의 Storm에서 사용할 수 있는 더 많은 예제 토폴로지는 [예제 Storm 토폴로지 및 구성 요소](hdinsight-storm-example-topology.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="393c5-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="393c5-260">Linux 기반 HDInsight에서 토폴로지 배포 및 모니터링에 대한 정보는 [Linux 기반 HDInsight에서 Apache Storm 토폴로지 배포 및 관리](hdinsight-storm-deploy-monitor-topology-linux.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="393c5-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>