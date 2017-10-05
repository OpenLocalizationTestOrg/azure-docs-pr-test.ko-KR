---
title: "HDInsight의 Hadoop 클러스터에서 빈 에지 노드 사용 - Azure | Microsoft Docs"
description: "클라이언트로 사용할 수 있는 HDInsight 클러스터에 빈 에지 노드를 추가한 다음 HDInsight 응용 프로그램을 테스트/호스트하는 방법입니다."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: e21dabcc6999b1f1047d334e782f723d0c03c2cb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="ac33d-103">HDInsight의 Hadoop 클러스터에서 빈 에지 노드 사용</span><span class="sxs-lookup"><span data-stu-id="ac33d-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="ac33d-104">HDInsight 클러스터에 빈 에지 노드를 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-104">Learn how to add an empty edge node to an HDInsight cluster.</span></span> <span data-ttu-id="ac33d-105">빈 에지 노드는 Hadoop 서비스는 실행되지 않지만 헤드 노드와 동일한 클라이언트 도구가 설치 및 구성된 Linux 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-105">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="ac33d-106">클러스터에 액세스하고, 클라이언트 응용 프로그램을 테스트하며 클라이언트 응용 프로그램을 호스트하는 데 에지 노드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-106">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="ac33d-107">빈 에지 노드를 기존 HDInsight 클러스터에 추가할 수 있습니다(클러스터를 만들 때는 새 클러스터에 추가).</span><span class="sxs-lookup"><span data-stu-id="ac33d-107">You can add an empty edge node to an existing HDInsight cluster, to a new cluster when you create the cluster.</span></span> <span data-ttu-id="ac33d-108">빈 에지 노드는 Azure Resource Manager 템플릿을 사용하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="ac33d-109">다음 예제는 템플릿을 사용하여 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-109">The following sample demonstrates how it is done using a template:</span></span>

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

<span data-ttu-id="ac33d-110">샘플에서 보여 주듯이 필요에 따라 [스크립트 동작](hdinsight-hadoop-customize-cluster-linux.md)을 호출하여 추가 구성을 수행할 수 있습니다(예: 에지 노드에서 [Apache Hue](hdinsight-hadoop-hue-linux.md) 설치).</span><span class="sxs-lookup"><span data-stu-id="ac33d-110">As shown in the sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) to perform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in the edge node.</span></span> <span data-ttu-id="ac33d-111">스크립트 작업 스크립트는 웹에서 공개적으로 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-111">The script action script must be publicly accessible on the web.</span></span>  <span data-ttu-id="ac33d-112">예를 들어 스크립트가 Azure Storage에 저장된 경우 공용 컨테이너 또는 공용 Blob을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-112">For example, if the script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="ac33d-113">에지 노드 가상 컴퓨터 크기는 HDInsight 클러스터 작업자 노드 VM 크기 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-113">The edge node virtual machine size must meet the HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="ac33d-114">권장되는 작업자 노드 VM 크기에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac33d-114">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="ac33d-115">에지 노드를 만든 후 SSH를 사용하여 에지 노드에 연결할 수 있고 HDInsight에서 Hadoop 클러스터에 액세스하는 클라이언트 도구를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-115">After you have created an edge node, you can connect to the edge node using SSH, and run client tools to access the Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="ac33d-116">HDInsight에서 빈 에지 노드를 사용하는 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="ac33d-117">에지 노드에 설치된 사용자 지정 구성 요소는 Microsoft에서 상업적으로 적절한 지원을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-117">Custom components that are installed on the edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="ac33d-118">이를 통해 발생한 문제가 해결될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="ac33d-119">또는 추가 지원을 위해 커뮤니티 리소스가 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-119">Or you may be referred to community resources for further assistance.</span></span> <span data-ttu-id="ac33d-120">다음은 커뮤니티의 도움을 받을 수 있는 가장 활발한 사이트 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-120">The following are some of the most active sites for getting help from the community:</span></span>
>
> * [<span data-ttu-id="ac33d-121">HDInsight에 대한 MSDN 포럼</span><span class="sxs-lookup"><span data-stu-id="ac33d-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="ac33d-122">[http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="ac33d-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="ac33d-123">Apache 기술을 사용하는 경우 [http://apache.org](http://apache.org)에서 [Hadoop](http://hadoop.apache.org/) 사이트 등의 Apache 프로젝트 사이트를 통해 지원을 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-123">If you are using an Apache technology, you may be able to find assistance through the Apache project sites on [http://apache.org](http://apache.org), such as the [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-to-an-existing-cluster"></a><span data-ttu-id="ac33d-124">기존 클러스터에 에지 노드 추가</span><span class="sxs-lookup"><span data-stu-id="ac33d-124">Add an edge node to an existing cluster</span></span>
<span data-ttu-id="ac33d-125">이 섹션에서는 Resource Manager 템플릿을 사용하여 기존 HDInsight 클러스터에 에지 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-125">In this section, you use a Resource Manager template to add an edge node to an existing HDInsight cluster.</span></span>  <span data-ttu-id="ac33d-126">Resource Manager 템플릿은 [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-126">The Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="ac33d-127">리소스 관리자 템플릿은 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh에 있는 스크립트 동작을 호출합니다. 스크립트는 어떤 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-127">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="ac33d-128">Resource Manager 템플릿에서 스크립트 호출 작업을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-128">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="ac33d-129">**기존 클러스터에 빈 에지 노드를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="ac33d-129">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="ac33d-130">아직 없는 경우 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="ac33d-131">[Hadoop 자습서: HDInsight에서 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac33d-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="ac33d-132">Azure에 로그인하여 Azure Portal에서 Azure Resource Manager 템플릿을 열려면 다음 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-132">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="ac33d-133">다음 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-133">Configure the following properties:</span></span>
   
   * <span data-ttu-id="ac33d-134">**구독**: 이 클러스터를 만드는 데 사용되는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-134">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="ac33d-135">**리소스 그룹**: 기존 HDInsight 클러스터에 사용되는 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-135">**Resource group**: Select the resource group used for the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="ac33d-136">**위치**: 기존 HDInsight 클러스터의 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-136">**Location**: Select the location of the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="ac33d-137">**클러스터 이름**: 기존 HDInsight 클러스터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-137">**Cluster Name**: Enter the name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="ac33d-138">**에지 노드 크기**: VM 크기 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-138">**Edge Node Size**: Select one of the VM sizes.</span></span> <span data-ttu-id="ac33d-139">VM 크기는 작업자 노드 VM 크기 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-139">The vm size must meet the worker node vm size requirements.</span></span> <span data-ttu-id="ac33d-140">권장되는 작업자 노드 VM 크기에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac33d-140">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="ac33d-141">**에지 노드 접두사**: 기본값은 **new**입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-141">**Edge Node Prefix**: The default value is **new**.</span></span>  <span data-ttu-id="ac33d-142">에지 노드 이름의 기본값은 **new-edgenode**가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-142">Using the default value, the edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="ac33d-143">포털에서 접두사를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-143">You can customize the prefix from the portal.</span></span> <span data-ttu-id="ac33d-144">템플릿에서 전체 이름을 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-144">You can also customize the full name from the template.</span></span>

4. <span data-ttu-id="ac33d-145">**위에 명시된 사용 약관에 동의함**을 선택한 다음 **구매**를 클릭하여 에지 노드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-145">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ac33d-146">기존 HDInsight 클러스터에 대한 Azure 리소스 그룹을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-146">Make sure to select the Azure resource group for the existing HDInsight cluster.</span></span>  <span data-ttu-id="ac33d-147">그렇지 않으면 "중첩된 리소스에서 요청한 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-147">Otherwise, you get the error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="ac33d-148">부모 리소스 '&lt;ClusterName>' 찾을 수 없음"이라는 오류 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="ac33d-149">클러스터를 만들 때 에지 노드 추가</span><span class="sxs-lookup"><span data-stu-id="ac33d-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="ac33d-150">이 섹션에서는 Resource Manager 템플릿을 사용하여 에지 노드로 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-150">In this section, you use a Resource Manager template to create HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="ac33d-151">Resource Manager 템플릿은 [Azure 빠른 시작 템플릿 갤러리](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-151">The Resource Manager template can be found in the [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="ac33d-152">리소스 관리자 템플릿은 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh에있는 스크립트 동작을 호출합니다. 스크립트는 어떤 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-152">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="ac33d-153">Resource Manager 템플릿에서 스크립트 호출 작업을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-153">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="ac33d-154">**기존 클러스터에 빈 에지 노드를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="ac33d-154">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="ac33d-155">아직 없는 경우 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="ac33d-156">[HDInsight에서 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac33d-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="ac33d-157">Azure에 로그인하여 Azure Portal에서 Azure Resource Manager 템플릿을 열려면 다음 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-157">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="ac33d-158">다음 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-158">Configure the following properties:</span></span>
   
   * <span data-ttu-id="ac33d-159">**구독**: 이 클러스터를 만드는 데 사용되는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-159">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="ac33d-160">**리소스 그룹**: 클러스터에 사용되는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-160">**Resource group**: Create a new resource group used for the cluster.</span></span>
   * <span data-ttu-id="ac33d-161">**위치**: 리소스 그룹의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-161">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="ac33d-162">**클러스터 이름**: 만들려는 새 클러스터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-162">**Cluster Name**: Enter a name for the new cluster to create.</span></span>
   * <span data-ttu-id="ac33d-163">**클러스터 로그인 사용자 이름**: Hadoop HTTP 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-163">**Cluster Login User Name**: Enter the Hadoop HTTP user name.</span></span>  <span data-ttu-id="ac33d-164">기본 이름은 **admin**입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-164">The default name is **admin**.</span></span>
   * <span data-ttu-id="ac33d-165">**클러스터 로그인 암호**: Hadoop HTTP 사용자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-165">**Cluster Login Password**: Enter the Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="ac33d-166">**Ssh 사용자 이름**: SSH 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-166">**Ssh User Name**: Enter the SSH user name.</span></span> <span data-ttu-id="ac33d-167">기본 이름은 **sshuser**입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-167">The default name is **sshuser**.</span></span>
   * <span data-ttu-id="ac33d-168">**Ssh 암호**: SSH 사용자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-168">**Ssh Password**: Enter the SSH user password.</span></span>
   * <span data-ttu-id="ac33d-169">**스크립트 동작 설치**: 이 자습서를 진행하기 위한 기본값을 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-169">**Install Script Action**: Keep the default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="ac33d-170">클러스터 유형, 클러스터 작업자 노드 수, 에지 노드 크기 및 에지 노드 이름과 같은 일부 속성은 템플릿에 하드 코드되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-170">Some properties have been hardcoded in the template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="ac33d-171">**위에 명시된 사용 약관에 동의함**을 선택한 다음 **구매**를 클릭하여 에지 노드가 있는 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-171">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the cluster with the edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="ac33d-172">에지 노드 액세스</span><span class="sxs-lookup"><span data-stu-id="ac33d-172">Access an edge node</span></span>
<span data-ttu-id="ac33d-173">에지 노드 ssh 끝점은 &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-173">The edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="ac33d-174">예: new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22</span><span class="sxs-lookup"><span data-stu-id="ac33d-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="ac33d-175">에지 노드는 Azure Portal에서 응용 프로그램으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-175">The edge node appears as an application on the Azure portal.</span></span>  <span data-ttu-id="ac33d-176">포털은 SSH를 사용하여 에지 노드에 액세스하는 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-176">The portal gives you the information to access the edge node using SSH.</span></span>

<span data-ttu-id="ac33d-177">**에지 노드 SSH 끝점을 확인하려면**</span><span class="sxs-lookup"><span data-stu-id="ac33d-177">**To verify the edge node SSH endpoint**</span></span>

1. <span data-ttu-id="ac33d-178">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-178">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ac33d-179">에지 노드를 사용하여 HDInsight 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-179">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="ac33d-180">클러스터 블레이드에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-180">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="ac33d-181">에지 노드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-181">You shall see the edge node.</span></span>  <span data-ttu-id="ac33d-182">기본 이름은 **new-edgenode**입니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-182">The default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="ac33d-183">에지 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-183">Click the edge node.</span></span> <span data-ttu-id="ac33d-184">SSH 끝점이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-184">You shall see the SSH endpoint.</span></span>

<span data-ttu-id="ac33d-185">**에지 노드에서 Hive를 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="ac33d-185">**To use Hive on the edge node**</span></span>

1. <span data-ttu-id="ac33d-186">SSH를 사용하여 에지 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-186">Use SSH to connect to the edge node.</span></span> <span data-ttu-id="ac33d-187">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac33d-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ac33d-188">SSH를 사용하여 에지 노드를 연결한 후 다음 명령을 사용하여 Hive 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-188">After you have connected to the edge node using SSH, use the following command to open the Hive console:</span></span>
   
        hive
3. <span data-ttu-id="ac33d-189">클러스터의 Hive 테이블을 표시하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-189">Run the following command to show Hive tables in the cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="ac33d-190">에지 노드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-190">Delete an edge node</span></span>
<span data-ttu-id="ac33d-191">Azure Portal에서 에지 노드를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-191">You can delete an edge node from the Azure portal.</span></span>

<span data-ttu-id="ac33d-192">**에지 노드에 액세스하려면**</span><span class="sxs-lookup"><span data-stu-id="ac33d-192">**To access an edge node**</span></span>

1. <span data-ttu-id="ac33d-193">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-193">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ac33d-194">에지 노드를 사용하여 HDInsight 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-194">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="ac33d-195">클러스터 블레이드에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-195">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="ac33d-196">에지 노드의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="ac33d-197">삭제할 에지 노드를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-197">Right-click the edge node you want to delete, and then click **Delete**.</span></span>
5. <span data-ttu-id="ac33d-198">**예** 를 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-198">Click **Yes** to confirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac33d-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac33d-199">Next steps</span></span>
<span data-ttu-id="ac33d-200">이 문서에서 에지 노드를 추가하는 방법과 에지 노드에 액세스하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-200">In this article, you have learned how to add an edge node and how to access the edge node.</span></span> <span data-ttu-id="ac33d-201">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac33d-201">To learn more, see the following articles:</span></span>

* <span data-ttu-id="ac33d-202">[HDInsight 응용 프로그램 설치](hdinsight-apps-install-applications.md): HDInsight 응용 프로그램을 클러스터에 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="ac33d-203">[사용자 지정 HDInsight 응용 프로그램 설치](hdinsight-apps-install-custom-applications.md): HDInsight로 게시 취소된 HDInsight 응용 프로그램을 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="ac33d-204">[HDInsight 응용 프로그램 게시](hdinsight-apps-publish-applications.md): 사용자 지정 HDInsight 응용 프로그램을 Azure Marketplace에 게시하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="ac33d-205">[MSDN: HDInsight 응용 프로그램 설치](https://msdn.microsoft.com/library/mt706515.aspx): HDInsight 응용 프로그램을 정의하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="ac33d-206">[스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 스크립트 작업을 사용하여 추가 응용 프로그램을 설치하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="ac33d-207">[Resource Manager 템플릿을 사용하여 HDInsight의 Linux 기반 Hadoop 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Resource Manager 템플릿을 호출하여 HDInsight 클러스터를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac33d-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>

