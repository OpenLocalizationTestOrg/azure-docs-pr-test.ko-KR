---
title: "aaaCreate HBase 클러스터를 Azure 가상 네트워크-| Microsoft Docs"
description: "Azure HDInsight에서 HBase 사용 시작 Azure 가상 네트워크에서 toocreate HDInsight HBase 클러스터 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="6d60e-104">Azure Virtual Network의 HDInsight에서 HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="6d60e-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="6d60e-105">toocreate Azure HDInsight HBase 클러스터 하는 방법에 대해 알아봅니다는 [Azure 가상 네트워크][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="6d60e-106">가상 네트워크 통합 HBase 클러스터 동일한 가상 네트워크로 응용 프로그램 이므로 배포 된 toohello 수 있는 응용 프로그램 HBase와 직접 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="6d60e-107">hello 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-107">hello benefits include:</span></span>

* <span data-ttu-id="6d60e-108">Hello 웹 응용 프로그램 toohello 노드 HBase Java 원격 프로시저를 통해 통신할 수 있도록 하는 hello HBase 클러스터의 직접 연결 (RPC) Api를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="6d60e-109">트래픽이 여러 게이트웨이 및 부하 분산 장치를 통과하지 않도록 하여 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="6d60e-110">hello 기능 tooprocess의에서 중요 한 정보는 공용 끝점을 노출 하지 않고 더 안전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6d60e-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d60e-111">Prerequisites</span></span>
<span data-ttu-id="6d60e-112">이 자습서를 시작 하기 전에 다음 항목 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="6d60e-113">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="6d60e-113">**An Azure subscription**.</span></span> <span data-ttu-id="6d60e-114">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d60e-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="6d60e-115">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="6d60e-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="6d60e-116">[Azure PowerShell 설치 및 사용](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d60e-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="6d60e-117">가상 네트워크에 HBase 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="6d60e-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="6d60e-118">이 섹션에서는 hello 종속 Azure 저장소 계정을 사용 하 여 Azure 가상 네트워크에서 사용 하 여 Linux 기반 HBase 클러스터를 만들는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="6d60e-119">다른 클러스터 생성 방법 및 참조 hello 설정을 이해, [만들 HDInsight 클러스터](hdinsight-hadoop-provision-linux-clusters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="6d60e-120">HDInsight 클러스터를 템플릿 toocreate Hadoop을 사용 하는 방법에 대 한 자세한 내용은 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 HDInsight 클러스터를 만들기 Hadoop](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="6d60e-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="6d60e-121">일부 속성 hello 서식 파일에 하드 코드 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="6d60e-122">예:</span><span class="sxs-lookup"><span data-stu-id="6d60e-122">For example:</span></span>
>
> * <span data-ttu-id="6d60e-123">**위치**: 미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="6d60e-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="6d60e-124">**클러스터 버전**: 3.5</span><span class="sxs-lookup"><span data-stu-id="6d60e-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="6d60e-125">**클러스터 작업자 노드 수**: 2</span><span class="sxs-lookup"><span data-stu-id="6d60e-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="6d60e-126">**기본 저장소 계정**: 고유한 문자열</span><span class="sxs-lookup"><span data-stu-id="6d60e-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="6d60e-127">**가상 네트워크 이름**: &lt;클러스터 이름>-vnet</span><span class="sxs-lookup"><span data-stu-id="6d60e-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="6d60e-128">**가상 네트워크 주소 공간**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6d60e-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="6d60e-129">**서브넷 이름**: subnet1</span><span class="sxs-lookup"><span data-stu-id="6d60e-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="6d60e-130">**서브넷 주소 범위**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6d60e-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="6d60e-131">&lt;클러스터 이름 > hello 서식 파일을 사용 하는 경우 제공 하는 hello 클러스터 이름 아래 템플릿으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="6d60e-132">Hello 이미지 tooopen hello 템플릿을 hello Azure 포털에서에서 다음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="6d60e-133">hello 서식 파일에 있는 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="6d60e-134">Hello에서 **사용자 지정 배포** 블레이드에서 hello 다음과 같은 속성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="6d60e-135">**구독**: 사용 된 Azure 구독 toocreate hello HDInsight 클러스터를 선택 하 고, hello 종속 저장소 계정, Azure 가상 네트워크를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="6d60e-136">**리소스 그룹**: **새로 만들기**를 선택하고 새 리소스 그룹 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="6d60e-137">**위치**: hello 리소스 그룹에 대 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="6d60e-138">**ClusterName**: hello Hadoop 클러스터 toobe 생성에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="6d60e-139">**로그인 이름 및 암호를 클러스터**: hello 기본 로그인 이름은 **admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="6d60e-140">**SSH 사용자 이름 및 암호**: hello 기본 사용자 이름은 **sshuser**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="6d60e-141">이름은 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-141">You can rename it.</span></span>
   * <span data-ttu-id="6d60e-142">**Toohello 약관 hello 위에서 설명한 동의**: (선택)</span><span class="sxs-lookup"><span data-stu-id="6d60e-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="6d60e-143">**구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-143">Click **Purchase**.</span></span> <span data-ttu-id="6d60e-144">클러스터에 대 한 약 20 분 toocreate 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="6d60e-145">Hello 클러스터를 만든 후 클릭할 수 있는 hello 포털 tooopen hello 클러스터 블레이드 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="6d60e-146">Hello 자습서를 완료 한 후 toodelete hello 클러스터를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="6d60e-147">HDInsight를 사용하면 데이터가 Azure 저장소에 저장되기 때문에 클러스터를 사용하지 않을 때 안전하게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="6d60e-148">HDInsight 클러스터를 사용하지 않는 기간에도 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="6d60e-149">Hello 클러스터에 대 한 hello 요금이 저장소에 대 한 hello 요금 보다 많은 배 더 많은 경우 이렇게 하면 경제 toodelete 클러스터 사용에서 되지 않은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="6d60e-150">클러스터를 삭제할 경우의 hello 지침은 참조 [를 사용 하 여 HDInsight의 Hadoop 관리 클러스터에 Azure 포털 hello](hdinsight-administer-use-management-portal.md#delete-clusters)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="6d60e-151">새 HBase 클러스터를 사용 하는 toobegin hello 프로시저에 사용할 수 있습니다 [HDInsight에서 Hadoop으로 HBase를 사용 하 여 시작](hdinsight-hbase-tutorial-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="6d60e-152">HBase Java RPC Api를 사용 하 여 toohello HBase 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="6d60e-153">인프라에는 서비스 (IaaS) 가상 컴퓨터로 만드는 hello 동일한 Azure 가상 네트워크와 동일한 서브넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="6d60e-154">새 IaaS 가상 컴퓨터를 만드는 지침은 [Windows Server를 실행하는 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d60e-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="6d60e-155">이 문서의 hello 단계를 수행 하는 경우 다음 hello 네트워크 구성에 대 한 값에는 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="6d60e-156">**가상 네트워크**: &lt;클러스터 이름>-vnet</span><span class="sxs-lookup"><span data-stu-id="6d60e-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="6d60e-157">**서브넷**: subnet1</span><span class="sxs-lookup"><span data-stu-id="6d60e-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6d60e-158">대체 &lt;클러스터 이름 > 이전 단계에서 hello HDInsight 클러스터를 만들 때 사용한 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="6d60e-159">이러한 값을 사용 하 여 hello 가상 컴퓨터가 배치 된 hello에 동일한 가상 네트워크 및 서브넷 hello HDInsight 클러스터와 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="6d60e-160">이 구성은 수 있도록 toodirectly 서로 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="6d60e-161">빈 가장자리 노드에 HDInsight 클러스터는 방식으로 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="6d60e-162">hello 가장자리 노드 사용된 toomanage hello 클러스터가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="6d60e-163">자세한 내용은 [HDInsight에서 빈 에지 노드 사용](hdinsight-apps-use-edge-node.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d60e-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="6d60e-164">Java 응용 프로그램 tooconnect tooHBase를 원격으로 사용 하는 경우에 hello 정규화 된 도메인 이름 (FQDN)를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="6d60e-165">toodetermine이 hello HBase 클러스터의 hello 연결별 DNS 접미사를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="6d60e-166">toodo, hello 메서드를 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="6d60e-167">웹 브라우저 toomake Ambari 호출을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="6d60e-168">Toohttps 찾아보기: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > 호스트 /? minimal_response = true입니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="6d60e-169">Hello DNS 접미사와 JSON 파일을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="6d60e-170">Hello Ambari 웹 사이트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="6d60e-171">너무 찾아보기 https://&lt;ClusterName >. azurehdinsight.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="6d60e-172">클릭 **호스트** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="6d60e-173">Curl toomake REST 호출을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="6d60e-174">반환 된 hello 개체 JSON (JavaScript Notation) 데이터에서 hello "host_name" 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="6d60e-175">Hello 클러스터의 노드 hello에 대 한 FQDN hello를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="6d60e-176">예:</span><span class="sxs-lookup"><span data-stu-id="6d60e-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="6d60e-177">hello 클러스터 이름으로 시작 하는 hello 도메인 이름 부분은 hello hello DNS 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="6d60e-178">예를 들면 mycluster.b1.cloudapp.net과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="6d60e-179">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="6d60e-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="6d60e-180">다음 Azure PowerShell 스크립트 tooregister hello 사용 하 여 hello **Get ClusterDetail** 함수를 사용 하는 tooreturn hello DNS 접미사를 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

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
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
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

     <span data-ttu-id="6d60e-181">Hello를 사용 하 여 사용 하 여 hello 다음 명령은 tooreturn hello DNS 접미사 hello Azure PowerShell 스크립트 실행 후 **Get ClusterDetail** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="6d60e-182">이 명령을 사용할 때는 HDInsight HBase 클러스터 이름, 관리자 이름 및 관리자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="6d60e-183">이 명령은 hello DNS 접미사를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="6d60e-184">예를 들면 **yourclustername.b4.internal.cloudapp.net**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="6d60e-185">가상 컴퓨터를 hello tooverify HBase 클러스터 hello와 통신할 수, hello 명령을 사용 하 여 `ping headnode0.<dns suffix>` hello 가상 컴퓨터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="6d60e-186">예를 들면 ping headnode0.mycluster.b1.cloudapp.net을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="6d60e-187">toouse Java 응용 프로그램에서이 정보를 참고할 수의 hello 단계 [(Hadoop) HDInsight HBase를 사용 하는 사용 하 여 Maven toobuild Java 응용 프로그램](hdinsight-hbase-build-java-maven.md) toocreate 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="6d60e-188">toohave hello 응용 프로그램 tooa 원격 HBase 서버에 연결, hello 수정 **hbase-site.xml** 사육에 대 한 FQDN이 예제에서는 toouse hello에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="6d60e-189">예:</span><span class="sxs-lookup"><span data-stu-id="6d60e-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="6d60e-190">Azure 가상 네트워크에서 이름 확인에 대 한 자세한 내용은 방법을 비롯 하 여 toouse 자체 DNS 서버 참조 [이름 확인 (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6d60e-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d60e-191">Next steps</span></span>
<span data-ttu-id="6d60e-192">이 자습서에서는 방법에 대해 배웠습니다 toocreate HBase 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="6d60e-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="6d60e-193">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6d60e-193">toolearn more, see:</span></span>

* [<span data-ttu-id="6d60e-194">HDInsight 시작</span><span class="sxs-lookup"><span data-stu-id="6d60e-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="6d60e-195">HDInsight에서 빈 에지 노드 사용</span><span class="sxs-lookup"><span data-stu-id="6d60e-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="6d60e-196">HDInsight에서 HBase 복제 구성</span><span class="sxs-lookup"><span data-stu-id="6d60e-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="6d60e-197">HDInsight에서 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="6d60e-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="6d60e-198">HDInsight의 Hadoop에서 HBase 사용 시작</span><span class="sxs-lookup"><span data-stu-id="6d60e-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="6d60e-199">HDInsight에서 HBase를 사용하여 Twitter 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="6d60e-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="6d60e-200">[Virtual Network 개요][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="6d60e-200">[Virtual Network Overview][vnet-overview]</span></span>

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
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "HBase 클러스터를 새 hello에 대 한 프로 비전 정보"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "스크립트 동작 toocustomize HBase 클러스터를 사용 하 여"

[azure-preview-portal]: https://portal.azure.com
