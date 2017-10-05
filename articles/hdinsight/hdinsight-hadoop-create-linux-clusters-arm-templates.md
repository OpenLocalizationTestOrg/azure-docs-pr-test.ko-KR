---
title: "템플릿을 사용하여 Hadoop 클러스터 만들기 - Azure HDInsight | Microsoft Docs"
description: "Resource Manager 템플릿을 사용하여 HDInsight 클러스터를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="e4ed0-103">Resource Manager 템플릿을 사용하여 HDInsight의 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="e4ed0-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="e4ed0-104">이 문서에서는 Azure Resource Manager 템플릿으로 Azure HDInsight 클러스터를 만드는 몇 가지 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="e4ed0-105">자세한 내용은 [Azure 리소스 관리자 템플릿을 사용하여 응용 프로그램 배포](../azure-resource-manager/resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="e4ed0-106">다른 클러스터 만들기 도구 및 기능을 알아보려면 이 페이지 위쪽에 있는 탭 선택기를 클릭하거나 [클러스터 생성 방법](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4ed0-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e4ed0-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="e4ed0-108">이 문서의 지침을 따르려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="e4ed0-109">[Azure 구독](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e4ed0-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e4ed0-110">Azure PowerShell 및/또는 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e4ed0-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="e4ed0-111">리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="e4ed0-111">Resource Manager templates</span></span>
<span data-ttu-id="e4ed0-112">Resource Manager 템플릿을 사용하면 조정된 단일 작업으로 응용 프로그램에 대해 다음을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="e4ed0-113">HDInsight 클러스터 및 해당 종속 리소스(예: 기본 저장소 계정)</span><span class="sxs-lookup"><span data-stu-id="e4ed0-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="e4ed0-114">기타 리소스(예: Apache Sqoop을 사용하는 Azure SQL Database)</span><span class="sxs-lookup"><span data-stu-id="e4ed0-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="e4ed0-115">템플릿에서 응용 프로그램에 필요한 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="e4ed0-116">또한 다양한 환경에 대한 값을 입력하기 위한 배포 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="e4ed0-117">템플릿은 배포에 대한 값을 생성하는 데 사용하는 JSON과 식으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="e4ed0-118">[Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/?term=hdinsight)에서 HDInsight 템플릿 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="e4ed0-119">[Resource Manager 확장](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) 또는 텍스트 편집기에서 플랫폼 간 [Visual Studio Code](https://code.visualstudio.com/#alt-downloads)를 사용하여 템플릿을 워크스테이션의 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="e4ed0-120">다양한 방법을 사용하여 템플릿을 호출하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="e4ed0-121">Resource Manager 템플릿에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="e4ed0-122">Azure 리소스 관리자 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="e4ed0-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="e4ed0-123">Azure Resource Manager 템플릿으로 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e4ed0-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="e4ed0-124">템플릿 생성</span><span class="sxs-lookup"><span data-stu-id="e4ed0-124">Generate templates</span></span>

<span data-ttu-id="e4ed0-125">Azure Portal을 사용하면 클러스터의 모든 속성을 구성한 다음 템플릿을 배포하기 전에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="e4ed0-126">따라서 템플릿을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-126">You can then reuse the template.</span></span>

<span data-ttu-id="e4ed0-127">**Azure Portal을 사용하여 템플릿을 생성하려면**</span><span class="sxs-lookup"><span data-stu-id="e4ed0-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="e4ed0-128">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e4ed0-129">왼쪽 메뉴에서 **새로 만들기**를 클릭하고 **인텔리전스 + 분석**을 클릭한 다음 **HDInsight**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="e4ed0-130">지침에 따라 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="e4ed0-131">**빠른 생성** 또는 **사용자 지정** 옵션 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="e4ed0-132">**요약** 탭에서 **템플릿 및 매개 변수 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![HDInsight Hadoop 클러스터 만들기 - Resource Manager 템플릿 다운로드](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="e4ed0-134">템플릿을 배포하는 데 사용된 템플릿 파일, 매개 변수 파일 및 코드 샘플의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![HDInsight Hadoop 클러스터 만들기 - Resource Manager 템플릿 다운로드 옵션](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="e4ed0-136">여기에서 템플릿을 다운로드하거나 템플릿 라이브러리에 저장하거나 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="e4ed0-137">라이브러리에 있는 템플릿에 액세스하려면 왼쪽 메뉴에서 **추가 서비스**를 클릭한 다음 **기타** 범주 아래에서 **템플릿**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="e4ed0-138">템플릿과 매개 변수 파일은 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="e4ed0-139">그렇지 않은 경우 예기치 않은 결과가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="e4ed0-140">예를 들어 기본 **clusterKind** 속성 값은 템플릿을 다운로드하기 전에 지정한 내용과 상관 없이 항상 **hadoop**입니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="e4ed0-141">PowerShell을 사용하여 배포 </span><span class="sxs-lookup"><span data-stu-id="e4ed0-141">Deploy with PowerShell</span></span>

<span data-ttu-id="e4ed0-142">다음 절차는 HDInsight에 Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="e4ed0-143">[부록](#appx-a-arm-template)의 JSON 파일을 워크스테이션에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="e4ed0-144">PowerShell 스크립트에서 파일 이름은 `C:\HDITutorials-ARM\hdinsight-arm-template.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="e4ed0-145">필요한 경우 매개 변수 및 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="e4ed0-146">다음 PowerShell 스크립트를 사용하여 템플릿을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-146">Run the template by using the following PowerShell script:</span></span>

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
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="e4ed0-147">PowerShell 스크립트에서는 클러스터 이름만 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="e4ed0-148">저장소 계정 이름은 템플릿에 하드 코드되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="e4ed0-149">클러스터 사용자 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="e4ed0-150">(기본 사용자 이름은 **admin**입니다.) 또한 SSH 사용자 암호를 입력하라는 메시지도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="e4ed0-151">(기본 SSH 사용자 이름은 **sshuser**입니다.)</span><span class="sxs-lookup"><span data-stu-id="e4ed0-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="e4ed0-152">자세한 내용은 [PowerShell로 배포](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="e4ed0-153">CLI를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="e4ed0-153">Deploy with CLI</span></span>
<span data-ttu-id="e4ed0-154">다음 샘플에서는 Azure CLI(명령줄 인터페이스)를 사용하며,</span><span class="sxs-lookup"><span data-stu-id="e4ed0-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="e4ed0-155">Resource Manager 템플릿을 호출하여 클러스터 및 해당 종속 저장소 계정과 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="e4ed0-156">다음을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-156">You are prompted to enter:</span></span>
* <span data-ttu-id="e4ed0-157">클러스터 이름</span><span class="sxs-lookup"><span data-stu-id="e4ed0-157">The cluster name.</span></span>
* <span data-ttu-id="e4ed0-158">클러스터 사용자 암호</span><span class="sxs-lookup"><span data-stu-id="e4ed0-158">The cluster user password.</span></span> <span data-ttu-id="e4ed0-159">(기본 사용자 이름은 **admin**입니다.)</span><span class="sxs-lookup"><span data-stu-id="e4ed0-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="e4ed0-160">SSH 사용자 암호</span><span class="sxs-lookup"><span data-stu-id="e4ed0-160">The SSH user password.</span></span> <span data-ttu-id="e4ed0-161">(기본 SSH 사용자 이름은 **sshuser**입니다.)</span><span class="sxs-lookup"><span data-stu-id="e4ed0-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="e4ed0-162">다음 코드에서는 인라인 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="e4ed0-163">REST API를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="e4ed0-163">Deploy with the REST API</span></span>
<span data-ttu-id="e4ed0-164">[REST API를 사용하여 배포](../azure-resource-manager/resource-group-template-deploy-rest.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="e4ed0-165">Visual Studio를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="e4ed0-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="e4ed0-166">Visual Studio를 사용하여 리소스 그룹 프로젝트를 만들고 사용자 인터페이스를 통해 Azure에 이 프로젝트를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="e4ed0-167">프로젝트에 포함할 리소스 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="e4ed0-168">이러한 리소스는 Resource Manager 템플릿에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="e4ed0-169">또한 프로젝트에서는 템플릿을 배포할 수 있는 PowerShell 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="e4ed0-170">Visual Studio를 리소스 그룹과 함께 사용하는 방법에 대한 소개는 [Visual Studio를 통해 Azure 리소스 그룹 생성 및 배포](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="e4ed0-171">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e4ed0-171">Troubleshoot</span></span>

<span data-ttu-id="e4ed0-172">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4ed0-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4ed0-173">Next steps</span></span>
<span data-ttu-id="e4ed0-174">이 문서에서는 HDInsight 클러스터를 만드는 여러 가지 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="e4ed0-175">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="e4ed0-176">.NET 클라이언트 라이브러리를 통해 리소스를 배포하는 예제는 [.NET 라이브러리 및 템플릿을 사용하여 리소스 배포](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="e4ed0-177">응용 프로그램 배포에 대한 자세한 예제는 [Azure에서 마이크로 서비스를 예측 가능하게 프로비전 및 배포](../app-service-web/app-service-deploy-complex-application-predictably.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="e4ed0-178">다른 환경에 솔루션 배포에 관한 지침은 [Microsoft Azure의 개발 및 테스트 환경](../solution-dev-test-environments.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="e4ed0-179">Azure Resource Manager 템플릿 섹션에 대한 자세한 내용은 [템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e4ed0-180">Azure Resource Manager 템플릿에서 사용할 수 있는 함수 목록은 [템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="e4ed0-181">부록: Hadoop 클러스터를 만들기 위한 Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="e4ed0-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="e4ed0-182">다음 Azure Resource Manager 템플릿은 종속 Azure Storage 계정을 사용하여 Linux 기반 Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="e4ed0-183">이 샘플에는 Hive metastore와 Oozie metastore에 대한 구성 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="e4ed0-184">템플릿을 사용하기 전에 섹션을 제거하거나 섹션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "The location where all azure resources will be deployed."
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
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
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

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="e4ed0-185">부록: Spark 클러스터를 만들기 위한 Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="e4ed0-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="e4ed0-186">이 섹션에서는 HDInsight Spark 클러스터를 만드는 데 사용할 수 있는 Resource Manager 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="e4ed0-187">이 템플릿에는 `spark-defaults` 및 `spark-thrift-sparkconf`(Spark 1.6 클러스터)에 대한 구성과 `spark2-defaults` 및 `spark2-thrift-sparkconf`(Spark 2 클러스터)에 대한 구성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="e4ed0-188">이외에도, HDInsight는 클러스터 크기에 따라 `spark.executor.instances`, `spark.executor.memory`, `spark.executor.cores` 등의 구성을 계산하고 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="e4ed0-189">템플릿 자체의 일부로 섹션에서 하나의 매개 변수를 설정하는 경우 HDInsight는 동일한 섹션의 다른 매개 변수를 계산 및 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="e4ed0-190">예를 들어 `spark.executor.instances` 매개 변수는 `spark-defaults` 구성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="e4ed0-191">`spark-defaults` 구성에서 다른 매개 변수(예: `spark.yarn.exector.memoryOverhead`)를 설정하는 경우 HDInsight는 `spark.executor.instances` 매개 변수도 계산 및 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ed0-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
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
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
