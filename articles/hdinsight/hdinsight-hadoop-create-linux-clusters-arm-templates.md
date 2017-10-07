---
title: "템플릿-Azure HDInsight를 사용 하 여 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "리소스 관리자 템플릿을 사용 하 여 toocreate HDInsight에 대 한 클러스터 하는 방법에 대해 알아봅니다"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="432e5-103">Resource Manager 템플릿을 사용하여 HDInsight의 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="432e5-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="432e5-104">여러 가지 방법으로이 문서에서는 설명 toocreate Azure HDInsight 클러스터 Azure 리소스 관리자 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="432e5-105">자세한 내용은 [Azure 리소스 관리자 템플릿을 사용하여 응용 프로그램 배포](../azure-resource-manager/resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="432e5-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="432e5-106">이 페이지 또는 참조의 hello 상단에서 hello 탭 선택기를 클릭 하는 다른 클러스터 작성 도구와 기능을 하는 방법에 대 한 toolearn [클러스터 생성 방법](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods)합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="432e5-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="432e5-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="432e5-108">이 문서의 toofollow hello 지침 항목이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="432e5-109">[Azure 구독](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="432e5-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="432e5-110">Azure PowerShell 및/또는 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="432e5-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="432e5-111">리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="432e5-111">Resource Manager templates</span></span>
<span data-ttu-id="432e5-112">리소스 관리자 서식 파일을 쉽게 toocreate hello를 조정 된 단일 작업에서 응용 프로그램에 대 한 다음 사용:</span><span class="sxs-lookup"><span data-stu-id="432e5-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="432e5-113">HDInsight 클러스터와 해당 종속 리소스 (예: hello 기본 저장소 계정)</span><span class="sxs-lookup"><span data-stu-id="432e5-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="432e5-114">기타 리소스 (예: Azure SQL 데이터베이스 toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="432e5-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="432e5-115">Hello 템플릿 hello 응용 프로그램에 필요한 hello 리소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="432e5-116">또한 다양 한 환경에 대 한 배포 매개 변수 tooinput 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="432e5-117">JSON 및 배포에 대 한 tooconstruct 값을 사용 하는 식의 hello 템플릿은 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="432e5-118">[Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/?term=hdinsight)에서 HDInsight 템플릿 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="432e5-119">크로스 플랫폼을 사용 하 여 [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) hello로 [리소스 관리자 확장](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) 또는 텍스트 편집기 toosave hello 템플릿을 워크스테이션에 있는 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="432e5-120">다른 방법을 사용 하 여 toocall 템플릿 hello 어떻게 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="432e5-121">리소스 관리자 템플릿에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="432e5-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="432e5-122">Azure 리소스 관리자 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="432e5-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="432e5-123">Azure Resource Manager 템플릿으로 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="432e5-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="432e5-124">템플릿 생성</span><span class="sxs-lookup"><span data-stu-id="432e5-124">Generate templates</span></span>

<span data-ttu-id="432e5-125">Azure 포털 hello를 사용 하 여 클러스터의 모든 hello 속성을 구성할 수 있으며 배포 하기 전에 hello 서식 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="432e5-126">그런 다음 hello 서식 파일을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-126">You can then reuse hello template.</span></span>

<span data-ttu-id="432e5-127">**toogenerate hello Azure 포털을 사용 하 여 서식 파일**</span><span class="sxs-lookup"><span data-stu-id="432e5-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="432e5-128">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="432e5-129">클릭 **새로** hello 왼쪽된 메뉴에서 클릭 **Intelligence + 분석**, 클릭 하 고 **HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="432e5-130">Hello 지침 tooenter 속성을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="432e5-131">Hello 중 하나를 사용할 수 있습니다 **빨리 만들기** 또는 hello **사용자 지정** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="432e5-132">Hello에 **요약** 탭을 클릭 **템플릿 및 매개 변수를 다운로드**:</span><span class="sxs-lookup"><span data-stu-id="432e5-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![HDInsight Hadoop 클러스터 만들기 - Resource Manager 템플릿 다운로드](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="432e5-134">Hello 서식 파일, 매개 변수 파일 및 코드 사용 되는 샘플 toodeploy hello 템플릿 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="432e5-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![HDInsight Hadoop 클러스터 만들기 - Resource Manager 템플릿 다운로드 옵션](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="432e5-136">여기에서는 hello 템플릿을 다운로드, tooyour 템플릿 라이브러리를 저장 하거나 hello 템플릿을 배포 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="432e5-137">라이브러리에 템플릿을 tooaccess 클릭 **더 많은 서비스** hello 왼쪽된 메뉴에서 **템플릿** (hello에서 **다른** 범주)입니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="432e5-138">hello 템플릿 및 매개 변수 파일을 함께 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="432e5-139">그렇지 않은 경우 예기치 않은 결과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="432e5-140">예를 들어 기본 hello **clusterKind** 속성 값은 항상 **hadoop**, 했던 불구 하 고 hello 서식 파일을 다운로드 하기 전에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="432e5-141">PowerShell을 사용하여 배포 </span><span class="sxs-lookup"><span data-stu-id="432e5-141">Deploy with PowerShell</span></span>

<span data-ttu-id="432e5-142">다음 절차는 HDInsight에 Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="432e5-143">Hello에 hello JSON 파일을 저장 [부록](#appx-a-arm-template) tooyour 워크스테이션.</span><span class="sxs-lookup"><span data-stu-id="432e5-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="432e5-144">PowerShell 스크립트 hello hello 파일 이름은 `C:\HDITutorials-ARM\hdinsight-arm-template.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="432e5-145">필요한 경우 hello 매개 변수 및 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="432e5-146">PowerShell 스크립트 뒤 hello를 사용 하 여 hello 서식 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="432e5-147">PowerShell 스크립트 hello hello 클러스터 이름만 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="432e5-148">hello 저장소 계정 이름이 hello 서식 파일에 하드 코드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="432e5-149">입력 정보 요청된 tooenter hello 클러스터 사용자 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="432e5-150">(hello 기본 사용자 이름은 **admin**.) 입력 정보 요청된 tooenter hello SSH 사용자 암호 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="432e5-151">(hello 기본 SSH 사용자 이름은 **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="432e5-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="432e5-152">자세한 내용은 [PowerShell로 배포](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="432e5-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="432e5-153">CLI를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="432e5-153">Deploy with CLI</span></span>
<span data-ttu-id="432e5-154">다음 예제는 hello Azure CLI (명령줄 인터페이스)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="432e5-155">Resource Manager 템플릿을 호출하여 클러스터 및 해당 종속 저장소 계정과 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="432e5-156">사용자는 증명된 tooenter:</span><span class="sxs-lookup"><span data-stu-id="432e5-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="432e5-157">hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-157">hello cluster name.</span></span>
* <span data-ttu-id="432e5-158">hello 클러스터 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-158">hello cluster user password.</span></span> <span data-ttu-id="432e5-159">(hello 기본 사용자 이름은 **admin**.)</span><span class="sxs-lookup"><span data-stu-id="432e5-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="432e5-160">hello SSH 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-160">hello SSH user password.</span></span> <span data-ttu-id="432e5-161">(hello 기본 SSH 사용자 이름은 **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="432e5-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="432e5-162">hello 코드 다음 인라인 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="432e5-163">Hello REST API를 사용 하 여 배포</span><span class="sxs-lookup"><span data-stu-id="432e5-163">Deploy with hello REST API</span></span>
<span data-ttu-id="432e5-164">참조 [hello REST API를 사용 하 여 배포](../azure-resource-manager/resource-group-template-deploy-rest.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="432e5-165">Visual Studio를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="432e5-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="432e5-166">Visual Studio toocreate 리소스 그룹 프로젝트를 사용 하 하며 tooAzure hello 사용자 인터페이스를 통해 배포.</span><span class="sxs-lookup"><span data-stu-id="432e5-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="432e5-167">프로젝트에 리소스 tooinclude hello 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="432e5-168">이러한 리소스는 toohello 리소스 관리자 템플릿은 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="432e5-169">hello 프로젝트에는 PowerShell 스크립트 toodeploy hello 템플릿을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="432e5-170">리소스 그룹에는 소개 toousing Visual Studio를 참조 하십시오. [만들기 및 Visual Studio를 통해 Azure 리소스 그룹을 배포](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="432e5-171">문제 해결</span><span class="sxs-lookup"><span data-stu-id="432e5-171">Troubleshoot</span></span>

<span data-ttu-id="432e5-172">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="432e5-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="432e5-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="432e5-173">Next steps</span></span>
<span data-ttu-id="432e5-174">이 문서에서는 여러 가지 방법으로 toocreate HDInsight 클러스터에 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="432e5-175">더 toolearn hello 다음 문서를 참조:</span><span class="sxs-lookup"><span data-stu-id="432e5-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="432e5-176">리소스를 hello.NET 클라이언트 라이브러리를 통해 배포의 예제를 보려면 [.NET 라이브러리 및 템플릿을 사용 하 여 리소스를 배포](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="432e5-177">응용 프로그램 배포에 대한 자세한 예제는 [Azure에서 마이크로 서비스를 예측 가능하게 프로비전 및 배포](../app-service-web/app-service-deploy-complex-application-predictably.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="432e5-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="432e5-178">솔루션 toodifferent 환경 배포에 대 한 지침을 참조 하십시오. [Microsoft Azure에서 개발 및 테스트 환경](../solution-dev-test-environments.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="432e5-179">toolearn hello Azure Resource Manager 템플릿의 hello 섹션에 대 한 참조 [템플릿을 작성](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="432e5-180">Azure Resource Manager 템플릿에 사용 가능한 hello 함수 목록은 참조 [템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="432e5-181">부록: 리소스 관리자 템플릿 toocreate Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="432e5-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="432e5-182">hello 다음 Azure 리소스 관리자 템플릿을 만듭니다 Linux 기반 Hadoop 클러스터 hello 종속 Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="432e5-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="432e5-183">이 샘플에는 Hive metastore와 Oozie metastore에 대한 구성 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="432e5-184">Hello 섹션을 제거 하거나 hello 서식 파일을 사용 하기 전에 hello 섹션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="432e5-185">부록: 리소스 관리자 템플릿 toocreate Spark 클러스터</span><span class="sxs-lookup"><span data-stu-id="432e5-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="432e5-186">이 섹션에서는 리소스 관리자 템플릿 toocreate HDInsight Spark 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="432e5-187">이 템플릿에는 `spark-defaults` 및 `spark-thrift-sparkconf`(Spark 1.6 클러스터)에 대한 구성과 `spark2-defaults` 및 `spark2-thrift-sparkconf`(Spark 2 클러스터)에 대한 구성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="432e5-188">또한 toothis, HDInsight 계산 하 고와 같은 구성 설정 `spark.executor.instances`, `spark.executor.memory`, 및 `spark.executor.cores` hello 클러스터 크기를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="432e5-189">Hello 템플릿 자체의 일부로 섹션에서 하나의 매개 변수를 설정한 경우 HDInsight 고 되지 않는 계산 hello hello의 다른 매개 변수 설정 동일한 섹션.</span><span class="sxs-lookup"><span data-stu-id="432e5-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="432e5-190">예를 들어 매개 변수 `spark.executor.instances` hello에 `spark-defaults` 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="432e5-191">다른 매개 변수를 설정 하는 경우 (예를 들어 `spark.yarn.exector.memoryOverhead`) hello에 `spark-defaults` 구성, HDInsight 고 되지 않는 계산 hello 설정 `spark.executor.instances` 도 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="432e5-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
