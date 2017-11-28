---
title: "가상 네트워크에 HBase 클러스터 만들기 - Azure | Microsoft Docs"
description: "Azure HDInsight에서 HBase 사용 시작 Azure 가상 네트워크에 HDInsight HBase 클러스터를 만드는 방법을 알아봅니다."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 668bd494ce3274188af56cf7d6253cec7af9abbc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="0968d-104">Azure Virtual Network의 HDInsight에서 HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="0968d-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="0968d-105">[Azure Virtual Network][1]에서 Azure HDInsight HBase 클러스터를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="0968d-106">가상 네트워크 통합을 사용하면 응용 프로그램이 HBase와 직접 통신할 수 있도록 응용 프로그램과 동일한 가상 네트워크에 HBase 클러스터를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="0968d-107">이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-107">The benefits include:</span></span>

* <span data-ttu-id="0968d-108">웹 응용 프로그램을 HBase 클러스터의 노드에 직접 연결하므로 HBase Java RPC(원격 프로시저 호출) API를 통해 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="0968d-109">트래픽이 여러 게이트웨이 및 부하 분산 장치를 통과하지 않도록 하여 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="0968d-110">공용 끝점을 노출하지 않고 중요한 정보를 보다 안전한 방식으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0968d-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0968d-111">Prerequisites</span></span>
<span data-ttu-id="0968d-112">이 자습서를 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-112">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="0968d-113">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="0968d-113">**An Azure subscription**.</span></span> <span data-ttu-id="0968d-114">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0968d-115">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="0968d-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="0968d-116">[Azure PowerShell 설치 및 사용](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="0968d-117">가상 네트워크에 HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="0968d-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="0968d-118">이 섹션에서는 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-template-deploy.md)을 사용하여 Azure 가상 네트워크에서 종속 Azure Storage 계정으로 Linux 기반 HBase 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="0968d-119">기타 클러스터 생성 방법 및 설정에 대한 이해는 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="0968d-120">템플릿을 사용하여 HDInsight에서 Hadoop 클러스터를 만드는 방법에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-create-windows-clusters-arm-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="0968d-121">일부 속성이 템플릿에 하드 코딩되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="0968d-122">예:</span><span class="sxs-lookup"><span data-stu-id="0968d-122">For example:</span></span>
>
> * <span data-ttu-id="0968d-123">**위치**: 미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="0968d-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="0968d-124">**클러스터 버전**: 3.5</span><span class="sxs-lookup"><span data-stu-id="0968d-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="0968d-125">**클러스터 작업자 노드 수**: 2</span><span class="sxs-lookup"><span data-stu-id="0968d-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="0968d-126">**기본 저장소 계정**: 고유한 문자열</span><span class="sxs-lookup"><span data-stu-id="0968d-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="0968d-127">**가상 네트워크 이름**: &lt;클러스터 이름>-vnet</span><span class="sxs-lookup"><span data-stu-id="0968d-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="0968d-128">**가상 네트워크 주소 공간**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="0968d-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="0968d-129">**서브넷 이름**: subnet1</span><span class="sxs-lookup"><span data-stu-id="0968d-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="0968d-130">**서브넷 주소 범위**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="0968d-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="0968d-131">&lt;클러스터 이름>은 템플릿을 사용할 때 제공하는 클러스터 이름으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="0968d-132">Azure 포털에서 템플릿을 열려면 다음 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="0968d-133">템플릿은 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="0968d-134">**사용자 지정 배포** 블레이드에서 다음 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-134">From the **Custom deployment** blade, enter the following properties:</span></span>

   * <span data-ttu-id="0968d-135">**구독**: HDInsight 클러스터, 종속 Storage 계정 및 Azure 가상 네트워크를 만드는 데 사용한 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="0968d-136">**리소스 그룹**: **새로 만들기**를 선택하고 새 리소스 그룹 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="0968d-137">**위치**: 리소스 그룹의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="0968d-138">**ClusterName**: 만들려는 Hadoop 클러스터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="0968d-139">**클러스터 로그인 이름 및 암호**: 기본 로그인 이름은 **admin**입니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="0968d-140">**SSH 사용자 이름 및 암호**: 기본 사용자 이름은 **sshuser**입니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="0968d-141">이름은 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-141">You can rename it.</span></span>
   * <span data-ttu-id="0968d-142">**위에 명시된 사용 약관에 동의함**: (선택)</span><span class="sxs-lookup"><span data-stu-id="0968d-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="0968d-143">**구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-143">Click **Purchase**.</span></span> <span data-ttu-id="0968d-144">클러스터를 만들려면 20분 정도가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="0968d-145">클러스터가 만들어졌으면 포털에서 클러스터 블레이드를 클릭하면 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="0968d-146">이 자습서를 완료한 후에 클러스터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="0968d-147">HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="0968d-148">HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="0968d-149">클러스터에 대한 요금이 저장소에 대한 요금보다 몇 배 더 많기 때문에, 클러스터를 사용하지 않을 때는 삭제하는 것이 경제적인 면에서 더 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="0968d-150">클러스터 삭제에 대한 내용은 [Azure Portal을 사용하여 HDInsight에서 Hadoop 클러스터 관리](hdinsight-administer-use-management-portal.md#delete-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="0968d-151">새 HBase 클러스터 사용을 시작하려는 경우 [HDInsight에서 Hadoop을 통해 HBase 사용 시작](hdinsight-hbase-tutorial-get-started.md)의 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="0968d-152">HBase Java RPC API를 사용하여 HBase 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="0968d-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="0968d-153">동일한 Azure 가상 네트워크와 동일한 서브넷에 IaaS(infrastructure as a service) 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="0968d-154">새 IaaS 가상 컴퓨터를 만드는 지침은 [Windows Server를 실행하는 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="0968d-155">이 문서의 단계를 수행할 때 다음과 같은 네트워크 구성 값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-155">When following the steps in this document, you must use the following values for the Network configuration:</span></span>

   * <span data-ttu-id="0968d-156">**가상 네트워크**: &lt;클러스터 이름>-vnet</span><span class="sxs-lookup"><span data-stu-id="0968d-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="0968d-157">**서브넷**: subnet1</span><span class="sxs-lookup"><span data-stu-id="0968d-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0968d-158">&lt;클러스터 이름>을 이전 단계에서 HDInsight 클러스터를 만들 때 사용한 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="0968d-159">이러한 값을 사용하면 가상 컴퓨터가 HDInsight 클러스터와 동일한 가상 네트워크와 서브넷에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="0968d-160">이 구성을 사용하면 서로 직접 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="0968d-161">빈 에지 노드가 있는 HDInsight 클러스터를 만드는 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="0968d-162">에지 노드를 사용하여 클러스터를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="0968d-163">자세한 내용은 [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="0968d-164">Java 응용 프로그램을 사용하여 HBase에 원격으로 연결할 때는 FQDN(정규화된 도메인 이름)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="0968d-165">FQDN을 확인하려면 HBase 클러스터의 연결별 DNS 접미사를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="0968d-166">이렇게 하려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="0968d-167">웹 브라우저를 사용하여 Ambari를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="0968d-168">https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="0968d-169">JSON 파일의 DNS 접미사를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="0968d-170">Ambari 웹 사이트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="0968d-171">https://&lt;ClusterName>.azurehdinsight.net으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="0968d-172">상위 메뉴에서 **호스트** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="0968d-173">Curl을 사용하여 REST를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-173">Use Curl to make REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="0968d-174">반환되는 JSON(JavaScript Object Notation) 데이터에서 "host_name" 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="0968d-175">이 항목에는 클러스터의 노드에 대한 FQDN이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-175">It contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="0968d-176">예:</span><span class="sxs-lookup"><span data-stu-id="0968d-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="0968d-177">클러스터 이름으로 시작하는 도메인 이름 부분이 DNS 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="0968d-178">예를 들면 mycluster.b1.cloudapp.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="0968d-179">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="0968d-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="0968d-180">다음 Azure PowerShell 스크립트를 사용하여 DNS 접미사를 반환하는 데 사용할 수 있는 **Get-ClusterDetail** 함수를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
            .Description
            This command shows the following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run the HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows the FQDN suffix of hosts in the cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows the value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run the HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows the FQDN suffix of hosts in the cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="0968d-181">Azure PowerShell 스크립트를 실행한 후 다음 명령을 사용하여 **Get-ClusterDetail** 함수를 통해 DNS 접미사를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="0968d-182">이 명령을 사용할 때는 HDInsight HBase 클러스터 이름, 관리자 이름 및 관리자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="0968d-183">이 명령은 DNS 접미사를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-183">This command returns the DNS suffix.</span></span> <span data-ttu-id="0968d-184">예를 들면 **yourclustername.b4.internal.cloudapp.net**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="0968d-185">가상 컴퓨터가 HBase 클러스터와 통신할 수 있는지 확인하려면 가상 컴퓨터에서 `ping headnode0.<dns suffix>` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-185">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="0968d-186">예를 들면 ping headnode0.mycluster.b1.cloudapp.net을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="0968d-187">Java 응용 프로그램에서 이 정보를 사용하려는 경우 [Maven을 통해 HDInsight(Hadoop)와 함께 HBase를 사용하는 Java 응용 프로그램 작성](hdinsight-hbase-build-java-maven.md) 의 단계에 따라 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-187">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="0968d-188">응용 프로그램이 원격 HBase 서버에 연결하도록 하려면 이 예제의 **hbase-site.xml** 파일이 ZooKeeper의 FQDN을 사용하도록 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-188">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="0968d-189">예:</span><span class="sxs-lookup"><span data-stu-id="0968d-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="0968d-190">자체 DNS 서버를 사용하는 방법을 포함한 Azure Virtual Network의 이름 확인에 대한 자세한 내용은 [이름 확인(DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-190">For more information about name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0968d-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0968d-191">Next steps</span></span>
<span data-ttu-id="0968d-192">이 자습서에서는 HBase 클러스터를 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="0968d-192">In this tutorial, you learned how to create an HBase cluster.</span></span> <span data-ttu-id="0968d-193">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0968d-193">To learn more, see:</span></span>

* [<span data-ttu-id="0968d-194">HDInsight 시작</span><span class="sxs-lookup"><span data-stu-id="0968d-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="0968d-195">HDInsight에서 빈 에지 노드 사용</span><span class="sxs-lookup"><span data-stu-id="0968d-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="0968d-196">HDInsight에서 HBase 복제 구성</span><span class="sxs-lookup"><span data-stu-id="0968d-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="0968d-197">HDInsight에서 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="0968d-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="0968d-198">HDInsight의 Hadoop에서 HBase 사용 시작</span><span class="sxs-lookup"><span data-stu-id="0968d-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="0968d-199">HDInsight에서 HBase를 사용하여 Twitter 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="0968d-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="0968d-200">[Virtual Network 개요][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="0968d-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "새 HBase 클러스터에 대한 프로비전 정보"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "스크립트 작업을 사용하여 HBase 클러스터 사용자 지정"

[azure-preview-portal]: https://portal.azure.com
