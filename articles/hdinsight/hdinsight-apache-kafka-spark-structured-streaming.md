---
title: "Kafka에서 Apache Spark 구조적 스트림 - Azure HDInsight | Microsoft Docs"
description: "Apache Spark 스트림(DStream)을 사용하여 Apache Kafka 간에 데이터를 이동하는 방법을 알아봅니다. 이 예제에서는 HDInsight의 Spark에서 Jupyter Notebook을 사용하여 데이터를 스트리밍합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="05602-104">HDInsight의 Kafka(미리 보기)에서 Spark 구조적 스트림 사용</span><span class="sxs-lookup"><span data-stu-id="05602-104">Use Spark Structured Streaming with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="05602-105">Azure HDInsight의 Apache Kafka에서 데이터를 읽는 Spark 구조적 스트림을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="05602-105">Learn how to use Spark Structured Streaming to read data from Apache Kafka on Azure HDInsight.</span></span>

<span data-ttu-id="05602-106">Spark 구조적 스트림은 Spark SQL에서 작성된 스트림 처리 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="05602-106">Spark structured streaming is a stream processing engine built on Spark SQL.</span></span> <span data-ttu-id="05602-107">정적 데이터에 대한 일괄 처리 계산과 동일하게 스트리밍 계산을 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-107">It allows you to express streaming computations the same as batch computation on static data.</span></span> <span data-ttu-id="05602-108">구조적 스트림에 대한 자세한 내용은 Apache.org에서 [구조적 스트림 프로그래밍 가이드[알파]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05602-108">For more information on Structured Streaming, see the [Structured Streaming Programming Guide [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) at Apache.org.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05602-109">이 예제에서는 HDInsight 3.6에서 Spark 2.1을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-109">This example used Spark 2.1 on HDInsight 3.6.</span></span> <span data-ttu-id="05602-110">구조적 스트림은 Spark 2.1에서 __알파__로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-110">Structured Streaming is considered __alpha__ on Spark 2.1.</span></span>
>
> <span data-ttu-id="05602-111">이 문서의 단계는 HDInsight의 Spark와 HDInsight의 Kafka 클러스터를 모두 포함하는 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05602-111">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="05602-112">이러한 클러스터는 모두 Azure Virtual Network에 있으며, 여기서는 Spark 클러스터와 Kafka 클러스터 간에 직접 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-112">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="05602-113">이 문서의 단계를 완료하는 경우 과도한 요금이 청구되지 않도록 클러스터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-113">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="05602-114">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="05602-114">Create the clusters</span></span>

<span data-ttu-id="05602-115">HDInsight의 Apache Kafka는 공용 인터넷을 통한 액세스를 Kafka broker에 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-115">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="05602-116">Kafka와 통신하는 대상은 Kafka 클러스터의 노드와 동일한 Azure 가상 네트워크에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-116">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="05602-117">여기서는 Kafka 클러스터와 Spark 클러스터가 모두 Azure 가상 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-117">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="05602-118">클러스터 간의 통신 흐름을 보여 주는 다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-118">The following diagram shows how communication flows between the clusters:</span></span>

![Azure 가상 네트워크에 있는 Spark 및 Kafka 클러스터 다이어그램](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="05602-120">Kafka 서비스는 가상 네트워크 내에서 통신으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="05602-120">The Kafka service is limited to communication within the virtual network.</span></span> <span data-ttu-id="05602-121">SSH 및 Ambari와 같은 클러스터의 다른 서비스는 인터넷을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-121">Other services on the cluster, such as SSH and Ambari, can be accessed over the internet.</span></span> <span data-ttu-id="05602-122">HDInsight에서 사용할 수 있는 공용 포트에 대한 자세한 내용은 [HDInsight에서 사용하는 포트 및 URI](hdinsight-hadoop-port-settings-for-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05602-122">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="05602-123">Azure 가상 네트워크, Kafka 클러스터 및 Spark 클러스터를 수동으로 만들 수 있지만 Azure Resource Manager 템플릿을 사용하는 것이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-123">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="05602-124">다음 단계에 따라 Azure 가상 네트워크, Kafka 클러스터 및 Spark 클러스터를 Azure 구독에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-124">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="05602-125">Azure에 로그인하고 Azure Portal에서 템플릿을 열려면 다음 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-125">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="05602-126">Azure Resource Manager 템플릿은 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05602-126">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.</span></span>

    <span data-ttu-id="05602-127">이 템플릿은 다음과 같은 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05602-127">This template creates the following resources:</span></span>

    * <span data-ttu-id="05602-128">HDInsight 3.5 클러스터의 Kafka</span><span class="sxs-lookup"><span data-stu-id="05602-128">A Kafka on HDInsight 3.5 cluster.</span></span>
    * <span data-ttu-id="05602-129">HDInsight 3.6 클러스터의 Spark</span><span class="sxs-lookup"><span data-stu-id="05602-129">A Spark on HDInsight 3.6 cluster.</span></span>
    * <span data-ttu-id="05602-130">HDInsight 클러스터를 포함하는 Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="05602-130">An Azure Virtual Network, which contains the HDInsight clusters.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="05602-131">이 예에서 사용된 구조적 스트림 Notebook은 HDInsight 3.6의 Spark가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-131">The structured streaming notebook used in this example requires Spark on HDInsight 3.6.</span></span> <span data-ttu-id="05602-132">HDInsight에서 이전 버전의 Spark를 사용하면 Notebook을 사용하는 경우 발생하는 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-132">If you use an earlier version of Spark on HDInsight, you receive errors when using the notebook.</span></span>

2. <span data-ttu-id="05602-133">다음 정보를 사용하여 **사용자 지정 배포** 블레이드의 항목을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="05602-133">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![HDInsight 사용자 지정 배포](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="05602-135">**리소스 그룹**: 그룹을 만들거나 기존 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-135">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="05602-136">이 그룹에는 HDInsight 클러스터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="05602-136">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="05602-137">**위치**: 지리적으로 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-137">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="05602-138">**기본 클러스터 이름**: 이 값은 Spark 및 Kafka 클러스터의 기본 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="05602-138">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="05602-139">예를 들어, **hdi**를 입력하면 spark-hdi__라는 Spark 클러스터와 **kafka-hdi**라는 Kafka 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="05602-139">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="05602-140">**클러스터 로그인 사용자 이름**: Spark 및 Kafka 클러스터의 관리자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05602-140">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="05602-141">**클러스터 로그인 암호**: Spark 및 Kafka 클러스터의 관리자 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="05602-141">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="05602-142">**SSH 사용자 이름**: Spark 및 Kafka 클러스터에 만들 SSH 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="05602-142">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="05602-143">**SSH 암호**: Spark 및 Kafka 클러스터에 대한 SSH 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="05602-143">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="05602-144">**사용 약관**을 읽은 다음 **위에 명시된 사용 약관에 동의함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-144">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="05602-145">마지막으로 **대시보드에 고정**을 선택한 다음 **구매**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-145">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="05602-146">클러스터를 만드는 데 약 20분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="05602-146">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="05602-147">리소스를 만들면 리소스 그룹 블레이드로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="05602-147">Once the resources have been created, you are redirected to the resource group blade.</span></span>

![vnet 및 클러스터에 대한 리소스 그룹 블레이드](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="05602-149">HDInsight 클러스터의 이름은 **spark-BASENAME** 및 **kafka-BASENAME**이며, 여기서 BASENAME은 템플릿에 제공된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05602-149">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="05602-150">이후 단계에서 클러스터에 연결할 때 이러한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-150">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="get-the-kafka-brokers"></a><span data-ttu-id="05602-151">Kafka broker를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="05602-151">Get the Kafka brokers</span></span>

<span data-ttu-id="05602-152">이 예제의 코드는 Kafka 클러스터에 있는 Kafka broker 호스트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-152">The code in this example connects to the Kafka broker hosts in the Kafka cluster.</span></span> <span data-ttu-id="05602-153">Kafka broker 호스트를 찾으려면 다음 PowerShell 또는 Bash 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-153">To find the Kafka broker hosts, use the following PowerShell or Bash example:</span></span>

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> <span data-ttu-id="05602-154">이 예에서 `$PASSWORD`는 클러스터 로그인 암호를 포함하고 `$CLUSTERNAME`은 Kafka 클러스터의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-154">This example expects `$PASSWORD` to contain the password for the cluster login, and `$CLUSTERNAME` to contain the name of the Kafka cluster.</span></span>
>
> <span data-ttu-id="05602-155">이 예제에서는 [jq](https://stedolan.github.io/jq/) 유틸리티를 사용하여 JSON 문서에서 데이터를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-155">This example uses the [jq](https://stedolan.github.io/jq/) utility to parse data out of the JSON document.</span></span>

<span data-ttu-id="05602-156">다음 텍스트와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="05602-156">The output is similar to the following text:</span></span>

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

<span data-ttu-id="05602-157">이 문서의 다음 단계에서 사용되기 때문에 이 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-157">Save this information, as it is used in the following sections of this document.</span></span>

## <a name="get-the-notebooks"></a><span data-ttu-id="05602-158">Notebooks 가져오기</span><span class="sxs-lookup"><span data-stu-id="05602-158">Get the notebooks</span></span>

<span data-ttu-id="05602-159">이 문서에서 설명한 예제의 코드는 [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="05602-159">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).</span></span>

## <a name="upload-the-notebooks"></a><span data-ttu-id="05602-160">Notebooks 업로드</span><span class="sxs-lookup"><span data-stu-id="05602-160">Upload the notebooks</span></span>

<span data-ttu-id="05602-161">프로젝트에서 HDInsight 클러스터의 Spark로 Notebooks을 업로드하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-161">Use the following steps to upload the notebooks from the project to your Spark on HDInsight cluster:</span></span>

1. <span data-ttu-id="05602-162">웹 브라우저의 Spark 클러스터에 있는 Jupyter Notebook에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-162">In your web browser, connect to the Jupyter notebook on your Spark cluster.</span></span> <span data-ttu-id="05602-163">다음 URL에서 `CLUSTERNAME`을 Kafka 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="05602-163">In the following URL, replace `CLUSTERNAME` with the name of your Kafka cluster:</span></span>

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    <span data-ttu-id="05602-164">메시지가 표시되면 클러스터를 만들 때 사용한 클러스터 로그인(관리자) 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-164">When prompted, enter the cluster login (admin) and password used when you created the cluster.</span></span>

2. <span data-ttu-id="05602-165">페이지의 오른쪽 위에서 __업로드__ 단추를 사용하여 __Stream-Tweets-To_Kafka.ipynb__ 파일을 클러스터에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-165">From the upper right side of the page, use the __Upload__ button to upload the __Stream-Tweets-To_Kafka.ipynb__ file to the cluster.</span></span> <span data-ttu-id="05602-166">__열기__를 선택하여 업로드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-166">Select __Open__ to start the upload.</span></span>

    ![업로드 단추를 사용하여 Notebook을 선택하고 업로드](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![KafkaStreaming.ipynb 파일 선택](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. <span data-ttu-id="05602-169">Notebook 목록에서 __Stream-Tweets-To_Kafka.ipynb__ 항목을 찾아 그 옆에 있는 __업로드__ 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-169">Find the __Stream-Tweets-To_Kafka.ipynb__ entry in the list of notebooks, and select __Upload__ button beside it.</span></span>

    ![KafkaStreaming.ipynb 항목 옆의 업로드 단추를 사용하여 Notebook 서버에 업로드](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. <span data-ttu-id="05602-171">1~3 단계를 반복하여 __Spark-Structured-Streaming-From-Kafka.ipynb__ Notebook을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-171">Repeat steps 1-3 to load the __Spark-Structured-Streaming-From-Kafka.ipynb__ notebook.</span></span>

## <a name="load-tweets-into-kafka"></a><span data-ttu-id="05602-172">Kafka로 트윗 로드</span><span class="sxs-lookup"><span data-stu-id="05602-172">Load tweets into Kafka</span></span>

<span data-ttu-id="05602-173">파일이 업로드되면 __Stream-Tweets-To_Kafka.ipynb__ 항목을 선택하여 Notebook을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="05602-173">Once the files have been uploaded, select the __Stream-Tweets-To_Kafka.ipynb__ entry to open the notebook.</span></span> <span data-ttu-id="05602-174">Notebook의 단계를 따라 Kafka로 트윗을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-174">Follow the steps in the notebook to load tweets into Kafka.</span></span>

## <a name="process-tweets-using-spark-structured-streaming"></a><span data-ttu-id="05602-175">Spark 구조적 스트림을 사용하여 트윗 프로세스</span><span class="sxs-lookup"><span data-stu-id="05602-175">Process tweets using Spark Structured Streaming</span></span>

<span data-ttu-id="05602-176">Jupyter Notebook 홈페이지에서 __Spark-Structured-Streaming-From-Kafka.ipynb__ 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-176">From the Jupyter Notebook home page, select the __Spark-Structured-Streaming-From-Kafka.ipynb__ entry.</span></span> <span data-ttu-id="05602-177">Notebook의 단계를 따라 Spark 구조적 스트림을 사용하여 트윗을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="05602-177">Follow the steps in the notebook to load tweets from Kafka using Spark Structured Streaming.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05602-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05602-178">Next steps</span></span>

<span data-ttu-id="05602-179">이제 Spark 구조적 스트림을 사용하는 방법을 배웠으므로 Spark 및 Kafka에서 작업하는 방법에 대한 자세한 내용을 보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05602-179">Now that you have learned how to use Spark Structured Streaming, see the following documents to learn more about working with Spark and Kafka:</span></span>

* <span data-ttu-id="05602-180">[Kafka에서 Spark 스트림(DStream)을 사용하는 방법](hdinsight-apache-spark-with-kafka.md)</span><span class="sxs-lookup"><span data-stu-id="05602-180">[How to use Spark streaming (DStream) with Kafka](hdinsight-apache-spark-with-kafka.md).</span></span>
* [<span data-ttu-id="05602-181">Jupyter Notebook 및 HDInsight의 Spark 시작</span><span class="sxs-lookup"><span data-stu-id="05602-181">Start with Jupyter Notebook and Spark on HDInsight</span></span>](hdinsight-apache-spark-jupyter-spark-sql.md)