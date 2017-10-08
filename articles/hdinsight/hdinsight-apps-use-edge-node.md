---
title: "aaaUse 빈 Azure HDInsight의 Hadoop 클러스터에 지 노드에 | Microsoft Docs"
description: "어떻게 tooadd 빈 가장자리 노드 tooan HDInsight 클러스터를 클라이언트로 사용할 수 및 다음 테스트/호스트 HDInsight 응용 프로그램입니다."
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
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="3455a-103">HDInsight의 Hadoop 클러스터에서 빈 에지 노드 사용</span><span class="sxs-lookup"><span data-stu-id="3455a-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="3455a-104">Tooadd 빈 노드 tooan HDInsight 클러스터를 가장자리 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-104">Learn how tooadd an empty edge node tooan HDInsight cluster.</span></span> <span data-ttu-id="3455a-105">빈 가장자리 노드는 없는 Hadoop 서비스를 실행 하면서도 같은 클라이언트 도구는 설치 하 고 hello headnodes 처럼 구성 하는 hello로 Linux 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="3455a-105">An empty edge node is a Linux virtual machine with hello same client tools installed and configured as in hello headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="3455a-106">Hello 클러스터에 액세스, 클라이언트 응용 프로그램을 테스트 하 고, 클라이언트 응용 프로그램을 호스팅하기 위한 hello 가장자리 노드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-106">You can use hello edge node for accessing hello cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="3455a-107">Hello 클러스터를 만들 때 빈 가장자리 노드 tooan 기존 HDInsight 클러스터에 tooa 새 클러스터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-107">You can add an empty edge node tooan existing HDInsight cluster, tooa new cluster when you create hello cluster.</span></span> <span data-ttu-id="3455a-108">빈 에지 노드는 Azure Resource Manager 템플릿을 사용하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="3455a-109">hello 다음 샘플을 수행 하는 방법을 템플릿을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="3455a-109">hello following sample demonstrates how it is done using a template:</span></span>

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

<span data-ttu-id="3455a-110">Hello 예제와 같이 필요에 따라를 호출할 수 있습니다는 [태스크 스크립팅할](hdinsight-hadoop-customize-cluster-linux.md) tooperform 등의 추가 구성을 설치 [Apache 색상을 나타내는](hdinsight-hadoop-hue-linux.md) hello 가장자리 노드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-110">As shown in hello sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) tooperform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in hello edge node.</span></span> <span data-ttu-id="3455a-111">hello 스크립트 동작 스크립트 hello 웹에서 공개적으로 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-111">hello script action script must be publicly accessible on hello web.</span></span>  <span data-ttu-id="3455a-112">예를 들어 hello 스크립트는 Azure 저장소에 저장 되 면 공용 컨테이너 또는 공용 blob 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-112">For example, if hello script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="3455a-113">hello 가장자리 노드 가상 컴퓨터 크기는 hello HDInsight 클러스터 작업자 노드 vm 크기 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-113">hello edge node virtual machine size must meet hello HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="3455a-114">Hello 권장 되는 작업자 노드 vm 크기에 대 한 참조 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-114">For hello recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="3455a-115">가장자리 노드를 만든 후에 toohello 가장자리 노드 SSH를 사용 하 여 연결 하 고 HDInsight의 클라이언트 도구 tooaccess hello Hadoop 클러스터를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-115">After you have created an edge node, you can connect toohello edge node using SSH, and run client tools tooaccess hello Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="3455a-116">HDInsight에서 빈 에지 노드를 사용하는 기능은 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="3455a-117">Microsoft에서 상업적으로 적절 한 지원을 받을 하는 hello 가장자리 노드에 설치 되어 있는 사용자 지정 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="3455a-117">Custom components that are installed on hello edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="3455a-118">이를 통해 발생한 문제가 해결될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="3455a-119">또는 추가 지원을 요청에 대 한 참조 toocommunity 리소스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-119">Or you may be referred toocommunity resources for further assistance.</span></span> <span data-ttu-id="3455a-120">hello 커뮤니티에서 도움말을 가져오기 위한 대부분의 활성 사이트 hello hello 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-120">hello following are some of hello most active sites for getting help from hello community:</span></span>
>
> * [<span data-ttu-id="3455a-121">HDInsight에 대한 MSDN 포럼</span><span class="sxs-lookup"><span data-stu-id="3455a-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="3455a-122">[http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="3455a-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="3455a-123">Apache 기술을 사용 하는 것일 수 있습니다 수 toofind 지원을 통해 hello Apache 프로젝트 사이트에 [http://apache.org](http://apache.org), hello 같은 [Hadoop](http://hadoop.apache.org/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-123">If you are using an Apache technology, you may be able toofind assistance through hello Apache project sites on [http://apache.org](http://apache.org), such as hello [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-tooan-existing-cluster"></a><span data-ttu-id="3455a-124">가장자리 노드 tooan 기존 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-124">Add an edge node tooan existing cluster</span></span>
<span data-ttu-id="3455a-125">이 섹션에서는 리소스 관리자 템플릿 tooadd 가장자리 노드 tooan 기존 HDInsight 클러스터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-125">In this section, you use a Resource Manager template tooadd an edge node tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="3455a-126">hello 리소스 관리자 템플릿을 찾을 수 [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-126">hello Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="3455a-127">hello 리소스 관리자 템플릿 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh에 있는 스크립트 작업을 호출 합니다. hello 스크립트는 모든 작업을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-127">hello Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. hello script doesn't perform any actions.</span></span>  <span data-ttu-id="3455a-128">것 toodemonstrate 리소스 관리자 템플릿으로 스크립트 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-128">It is toodemonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="3455a-129">**tooadd 빈 가장자리 노드 tooan 기존 클러스터**</span><span class="sxs-lookup"><span data-stu-id="3455a-129">**tooadd an empty edge node tooan existing cluster**</span></span>

1. <span data-ttu-id="3455a-130">아직 없는 경우 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="3455a-131">[Hadoop 자습서: HDInsight에서 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3455a-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="3455a-132">Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello Azure 리소스 관리자 템플릿을 다음를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-132">Click hello following image toosign in tooAzure and open hello Azure Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. <span data-ttu-id="3455a-133">Hello 다음과 같은 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-133">Configure hello following properties:</span></span>
   
   * <span data-ttu-id="3455a-134">**구독**: hello 클러스터를 만드는 데 사용 되는 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-134">**Subscription**: Select an Azure subscription used for creating hello cluster.</span></span>
   * <span data-ttu-id="3455a-135">**리소스 그룹**: hello 기존 HDInsight 클러스터에 사용 되는 선택 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-135">**Resource group**: Select hello resource group used for hello existing HDInsight cluster.</span></span>
   * <span data-ttu-id="3455a-136">**위치**: hello 기존 HDInsight 클러스터의 hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-136">**Location**: Select hello location of hello existing HDInsight cluster.</span></span>
   * <span data-ttu-id="3455a-137">**클러스터 이름**: 기존 HDInsight 클러스터의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-137">**Cluster Name**: Enter hello name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="3455a-138">**노드 크기를 가장자리**: hello VM 크기 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-138">**Edge Node Size**: Select one of hello VM sizes.</span></span> <span data-ttu-id="3455a-139">hello vm 크기는 hello 작업자 노드 vm 크기 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-139">hello vm size must meet hello worker node vm size requirements.</span></span> <span data-ttu-id="3455a-140">Hello 권장 되는 작업자 노드 vm 크기에 대 한 참조 [HDInsight 클러스터를 만드는 Hadoop](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-140">For hello recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="3455a-141">**노드 접두사 가장자리**: hello 기본값은 **새**합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-141">**Edge Node Prefix**: hello default value is **new**.</span></span>  <span data-ttu-id="3455a-142">Hello 기본값을 사용 하 여 hello 가장자리 노드 이름이 **새 edgenode**합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-142">Using hello default value, hello edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="3455a-143">Hello 접두사 hello 포털에서 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-143">You can customize hello prefix from hello portal.</span></span> <span data-ttu-id="3455a-144">또한 hello 템플릿에서 hello 전체 이름을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-144">You can also customize hello full name from hello template.</span></span>

4. <span data-ttu-id="3455a-145">확인 **toohello 약관 위에서 설명한 동의**, 클릭 하 고 **구매** toocreate hello 가장자리 노드.</span><span class="sxs-lookup"><span data-stu-id="3455a-145">Check **I agree toohello terms and conditions stated above**, and then click  **Purchase** toocreate hello edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="3455a-146">Hello 기존 HDInsight 클러스터에 대 한 있는지 tooselect hello Azure 리소스 그룹을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-146">Make sure tooselect hello Azure resource group for hello existing HDInsight cluster.</span></span>  <span data-ttu-id="3455a-147">그렇지 않으면 오류가 hello 메시지 "을 수행할 수 없습니다 중첩 된 리소스에 대해 요청 된 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-147">Otherwise, you get hello error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="3455a-148">부모 리소스 '&lt;ClusterName>' 찾을 수 없음"이라는 오류 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="3455a-149">클러스터를 만들 때 에지 노드 추가</span><span class="sxs-lookup"><span data-stu-id="3455a-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="3455a-150">이 섹션에서는 리소스 관리자 템플릿 toocreate HDInsight 클러스터를 사용 하 여 가장자리 노드 사용.</span><span class="sxs-lookup"><span data-stu-id="3455a-150">In this section, you use a Resource Manager template toocreate HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="3455a-151">hello에 hello 리소스 관리자 템플릿을 찾을 수 [Azure 빠른 시작 템플릿 갤러리](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-151">hello Resource Manager template can be found in hello [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="3455a-152">hello 리소스 관리자 템플릿 https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh에 있는 스크립트 작업을 호출 합니다. hello 스크립트는 모든 작업을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-152">hello Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. hello script doesn't perform any actions.</span></span>  <span data-ttu-id="3455a-153">것 toodemonstrate 리소스 관리자 템플릿으로 스크립트 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-153">It is toodemonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="3455a-154">**tooadd 빈 가장자리 노드 tooan 기존 클러스터**</span><span class="sxs-lookup"><span data-stu-id="3455a-154">**tooadd an empty edge node tooan existing cluster**</span></span>

1. <span data-ttu-id="3455a-155">아직 없는 경우 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="3455a-156">[HDInsight에서 Hadoop 사용 시작](hdinsight-hadoop-linux-tutorial-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3455a-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="3455a-157">Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello Azure 리소스 관리자 템플릿을 다음를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-157">Click hello following image toosign in tooAzure and open hello Azure Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. <span data-ttu-id="3455a-158">Hello 다음과 같은 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-158">Configure hello following properties:</span></span>
   
   * <span data-ttu-id="3455a-159">**구독**: hello 클러스터를 만드는 데 사용 되는 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-159">**Subscription**: Select an Azure subscription used for creating hello cluster.</span></span>
   * <span data-ttu-id="3455a-160">**리소스 그룹**: hello 클러스터에 사용 되는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-160">**Resource group**: Create a new resource group used for hello cluster.</span></span>
   * <span data-ttu-id="3455a-161">**위치**: hello 리소스 그룹에 대 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-161">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="3455a-162">**클러스터 이름**: 새 클러스터 toocreate hello에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-162">**Cluster Name**: Enter a name for hello new cluster toocreate.</span></span>
   * <span data-ttu-id="3455a-163">**클러스터 로그인 사용자 이름**: hello Hadoop HTTP 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-163">**Cluster Login User Name**: Enter hello Hadoop HTTP user name.</span></span>  <span data-ttu-id="3455a-164">기본 이름은 hello **admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-164">hello default name is **admin**.</span></span>
   * <span data-ttu-id="3455a-165">**로그인 암호 클러스터**: hello Hadoop HTTP 사용자 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-165">**Cluster Login Password**: Enter hello Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="3455a-166">**Ssh 사용자 이름이**: hello SSH 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-166">**Ssh User Name**: Enter hello SSH user name.</span></span> <span data-ttu-id="3455a-167">기본 이름은 hello **sshuser**합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-167">hello default name is **sshuser**.</span></span>
   * <span data-ttu-id="3455a-168">**Ssh 암호**: hello SSH 사용자 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-168">**Ssh Password**: Enter hello SSH user password.</span></span>
   * <span data-ttu-id="3455a-169">**설치 스크립트 작업**:이 자습서를 진행 하 고 hello 기본값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-169">**Install Script Action**: Keep hello default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="3455a-170">일부 속성이 hello 템플릿에 하드 코드 된: 클러스터 종류, 클러스터 작업자 노드 수, 가장자리 노드 크기 및 가장자리 노드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-170">Some properties have been hardcoded in hello template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="3455a-171">확인 **toohello 약관 위에서 설명한 동의**, 클릭 하 고 **구매** hello 가장자리 노드와 toocreate hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-171">Check **I agree toohello terms and conditions stated above**, and then click  **Purchase** toocreate hello cluster with hello edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="3455a-172">에지 노드 액세스</span><span class="sxs-lookup"><span data-stu-id="3455a-172">Access an edge node</span></span>
<span data-ttu-id="3455a-173">hello 가장자리 노드 ssh 끝점은 &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-173">hello edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="3455a-174">예: new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22</span><span class="sxs-lookup"><span data-stu-id="3455a-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="3455a-175">hello 가장자리 노드가 hello Azure 포털에서 응용 프로그램으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-175">hello edge node appears as an application on hello Azure portal.</span></span>  <span data-ttu-id="3455a-176">hello 포털 제공 정보 tooaccess hello hello SSH를 사용 하 여 노드를 가장자리입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-176">hello portal gives you hello information tooaccess hello edge node using SSH.</span></span>

<span data-ttu-id="3455a-177">**tooverify hello 가장자리 노드 SSH 끝점**</span><span class="sxs-lookup"><span data-stu-id="3455a-177">**tooverify hello edge node SSH endpoint**</span></span>

1. <span data-ttu-id="3455a-178">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-178">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3455a-179">가장자리 노드도 hello HDInsight 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-179">Open hello HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="3455a-180">클릭 **응용 프로그램** hello 클러스터 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-180">Click **Applications** from hello cluster blade.</span></span> <span data-ttu-id="3455a-181">Hello 가장자리 노드를 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-181">You shall see hello edge node.</span></span>  <span data-ttu-id="3455a-182">기본 이름은 hello **새 edgenode**합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-182">hello default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="3455a-183">Hello 가장자리 노드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-183">Click hello edge node.</span></span> <span data-ttu-id="3455a-184">Hello SSH 끝점에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-184">You shall see hello SSH endpoint.</span></span>

<span data-ttu-id="3455a-185">**hello 가장자리 노드에서 toouse 하이브**</span><span class="sxs-lookup"><span data-stu-id="3455a-185">**toouse Hive on hello edge node**</span></span>

1. <span data-ttu-id="3455a-186">SSH tooconnect toohello 가장자리 노드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-186">Use SSH tooconnect toohello edge node.</span></span> <span data-ttu-id="3455a-187">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3455a-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3455a-188">SSH를 사용 하 여 toohello 가장자리 노드를 연결한 후 다음 명령 tooopen hello 하이브 콘솔 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-188">After you have connected toohello edge node using SSH, use hello following command tooopen hello Hive console:</span></span>
   
        hive
3. <span data-ttu-id="3455a-189">다음 명령은 tooshow 하이브 표 hello 클러스터의 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-189">Run hello following command tooshow Hive tables in hello cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="3455a-190">에지 노드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-190">Delete an edge node</span></span>
<span data-ttu-id="3455a-191">Hello Azure 포털에서에서 가장자리 노드를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-191">You can delete an edge node from hello Azure portal.</span></span>

<span data-ttu-id="3455a-192">**tooaccess 가장자리 노드**</span><span class="sxs-lookup"><span data-stu-id="3455a-192">**tooaccess an edge node**</span></span>

1. <span data-ttu-id="3455a-193">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-193">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3455a-194">가장자리 노드도 hello HDInsight 클러스터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-194">Open hello HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="3455a-195">클릭 **응용 프로그램** hello 클러스터 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-195">Click **Applications** from hello cluster blade.</span></span> <span data-ttu-id="3455a-196">에지 노드의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="3455a-197">마우스 오른쪽 단추로 클릭 hello 가장자리 사용할 노드 toodelete, 마우스 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-197">Right-click hello edge node you want toodelete, and then click **Delete**.</span></span>
5. <span data-ttu-id="3455a-198">클릭 **예** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-198">Click **Yes** tooconfirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3455a-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3455a-199">Next steps</span></span>
<span data-ttu-id="3455a-200">이 문서에서는 배웠습니다 어떻게 tooadd 방법을 tooaccess hello 가장자리 노드 및 가장자리 노드.</span><span class="sxs-lookup"><span data-stu-id="3455a-200">In this article, you have learned how tooadd an edge node and how tooaccess hello edge node.</span></span> <span data-ttu-id="3455a-201">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="3455a-201">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="3455a-202">[HDInsight 응용 프로그램을 설치](hdinsight-apps-install-applications.md): tooinstall HDInsight 응용 프로그램 tooyour 클러스터 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how tooinstall an HDInsight application tooyour clusters.</span></span>
* <span data-ttu-id="3455a-203">[사용자 지정 HDInsight 응용 프로그램을 설치](hdinsight-apps-install-custom-applications.md): 자세한 방법을 toodeploy 게시 되지 않은 HDInsight 응용 프로그램 tooHDInsight 합니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how toodeploy an unpublished HDInsight application tooHDInsight.</span></span>
* <span data-ttu-id="3455a-204">[HDInsight는 응용 프로그램 게시](hdinsight-apps-publish-applications.md): 자세한 방법을 toopublish 사용자 사용자 지정 HDInsight 응용 프로그램 tooAzure 마켓플레이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how toopublish your custom HDInsight applications tooAzure Marketplace.</span></span>
* <span data-ttu-id="3455a-205">[MSDN: HDInsight 응용 프로그램을 설치 하](https://msdn.microsoft.com/library/mt706515.aspx): 자세한 방법을 toodefine HDInsight 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how toodefine HDInsight applications.</span></span>
* <span data-ttu-id="3455a-206">[스크립트 동작을 사용 하 여 Linux 기반 HDInsight 클러스터를 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md): 자세한 방법을 toouse 스크립트 동작 tooinstall 추가 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how toouse Script Action tooinstall additional applications.</span></span>
* <span data-ttu-id="3455a-207">[리소스 관리자 템플릿을 사용 하 여 HDInsight의 Linux 기반 Hadoop 클러스터를 만들어](hdinsight-hadoop-create-linux-clusters-arm-templates.md): 방법을 toocall 리소스 관리자 템플릿 toocreate HDInsight 클러스터에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3455a-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how toocall Resource Manager templates toocreate HDInsight clusters.</span></span>

