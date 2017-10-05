---
title: "HDInsight용 Azure Resource Manager 도구에 마이그레이션 | Microsoft Docs"
description: "HDInsight 클러스터용 Azure Resource Manager 개발 도구에 마이그레이션하는 방법"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 708d22b9ce53d4dbc07c6bcde0c46dcd238291bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="1d578-103">HDInsight 클러스터용 Azure Resource Manager 기반 개발 도구에 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="1d578-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="1d578-104">HDInsight에서는 HDInsight용 ASM(Azure 서비스 관리자) 기반 도구를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="1d578-105">Azure PowerShell, Azure CLI 또는 HDInsight .NET SDK를 사용하여 HDInsight 클러스터와 함께 사용한 경우 앞으로 ARM(Azure Resource Manager) 기반 버전의 PowerShell, CLI 및 .NET SDK를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="1d578-106">이 문서는 새 ARM 기반 접근 방법에 마이그레이션하는 방법에 대한 포인터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="1d578-107">해당되는 경우 이 문서에서도 HDInsight에 대한 ASM 및 ARM 접근 방법 간의 차이점을 지적합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d578-108">ASM 기반 PowerShell, CLI 및 .NET SDK에 대한 지원은 **2017년 1월 1일**에 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="1d578-109">Azure Resource Manager로 Azure CLI 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="1d578-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="1d578-110">이전 설치에서 업그레이드하지 않은 경우 Azure CLI는 ARM(Azure Resource Manager) 모드를 기본값으로 합니다. 이 경우에 `azure config mode arm` 명령을 사용하여 ARM 모드로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="1d578-111">ASM(Azure 서비스 관리)를 사용하여 HDInsight와 함께 사용하도록 Azure CLI에서 제공한 기본 명령은 ARM을 사용하는 경우와 동일합니다. 그러나 일부 매개 변수 및 스위치는 이름이 다를 수 있고 ARM을 사용하는 경우 많은 새 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="1d578-112">예를 들어 이제 `azure hdinsight cluster create`을 사용하여 클러스터를 만들어야 할 Azure 가상 네트워크 또는 Hive 및 Oozie 메타저장소 정보를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="1d578-113">Azure Resource Manager를 통한 HDInsight를 사용하는 기본 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="1d578-114">`azure hdinsight cluster create` - 새 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="1d578-115">`azure hdinsight cluster delete` - 새 HDInsight 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="1d578-116">`azure hdinsight cluster show` - 기존 클러스터에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="1d578-117">`azure hdinsight cluster list` - Azure 구독에 대한 HDInsight 클러스터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="1d578-118">`-h` 을 사용하여 각 명령에 사용할 수 있는 매개 변수와 스위치를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="1d578-119">새 명령</span><span class="sxs-lookup"><span data-stu-id="1d578-119">New commands</span></span>
<span data-ttu-id="1d578-120">Azure Resource Manager로 사용할 수 있는 새 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="1d578-121">`azure hdinsight cluster resize` - 클러스터에서 작업자 노드 수를 동적으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="1d578-122">`azure hdinsight cluster enable-http-access` - 클러스터에 대한 HTTPs 액세스를 사용합니다(기본적으로).</span><span class="sxs-lookup"><span data-stu-id="1d578-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="1d578-123">`azure hdinsight cluster disable-http-access` - 클러스터에 대한 HTTPs 액세스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="1d578-124">`azure hdinsight script-action` - 클러스터에서 스크립트 작업을 만들기/관리하기 위한 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="1d578-125">`azure hdinsight config` - `hdinsight cluster create` 명령으로 사용할 수 있는 구성 파일을 만들기 위한 명령을 제공하여 구성 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="1d578-126">사용되지 않는 명령</span><span class="sxs-lookup"><span data-stu-id="1d578-126">Deprecated commands</span></span>
<span data-ttu-id="1d578-127">`azure hdinsight job` 명령을 사용하여 HDInsight 클러스터에 작업을 제출하는 경우 ARM 명령을 통해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="1d578-128">프로그래밍 방식으로 스크립트에서 HDInsight로 작업을 제출해야 하는 경우 HDInsight에서 제공하는 REST API를 대신 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="1d578-129">REST API를 사용하여 작업을 제출하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d578-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="1d578-130">cURL을 사용하여 HDInsight에서 Hadoop과 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="1d578-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="1d578-131">cURL을 사용하여 HDInsight에서 Hadoop과 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="1d578-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="1d578-132">cURL을 사용하여 HDInsight에서 Hadoop과 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="1d578-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="1d578-133">MapReduce, Hive 및 Pig를 대화형으로 실행하는 다른 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop과 MapReduce 사용](hdinsight-use-mapreduce.md), [HDInsight에서 Hadoop과 Hive 사용](hdinsight-use-hive.md) 및 [HDInsight에서 Hadoop과 Pig 사용](hdinsight-use-pig.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d578-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="1d578-134">예</span><span class="sxs-lookup"><span data-stu-id="1d578-134">Examples</span></span>
<span data-ttu-id="1d578-135">**클러스터 만들기**</span><span class="sxs-lookup"><span data-stu-id="1d578-135">**Creating a cluster**</span></span>

* <span data-ttu-id="1d578-136">이전 명령(ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="1d578-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="1d578-137">새 명령(ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="1d578-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="1d578-138">**클러스터 삭제**</span><span class="sxs-lookup"><span data-stu-id="1d578-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="1d578-139">이전 명령(ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="1d578-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="1d578-140">새 명령(ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="1d578-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="1d578-141">**클러스터 나열**</span><span class="sxs-lookup"><span data-stu-id="1d578-141">**List clusters**</span></span>

* <span data-ttu-id="1d578-142">이전 명령(ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="1d578-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="1d578-143">새 명령(ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="1d578-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="1d578-144">나열 명령의 경우 `-g`을 사용하여 리소스 그룹을 지정하면 지정된 리소스 그룹에 클러스터만을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="1d578-145">**클러스터 정보 표시**</span><span class="sxs-lookup"><span data-stu-id="1d578-145">**Show cluster information**</span></span>

* <span data-ttu-id="1d578-146">이전 명령(ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="1d578-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="1d578-147">새 명령(ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="1d578-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="1d578-148">Azure Resource Manager로 Azure PowerShell 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="1d578-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="1d578-149">[Azure 리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)에서 ARM(Azure Resource Manager) 모드인 Azure PowerShell에 대한 일반 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="1d578-150">Azure PowerShell ARM cmdlet은 ASM cmdlet과 나란히 설치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="1d578-151">두 가지 모드에서 cmdlet을 이름으로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="1d578-152">ARM 모드에는 ASM 모드의 *AzureRmHDInsight*와 비교되는 cmdlet 이름의 *AzureHDInsight*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="1d578-153">예를 들면 *New-AzureRmHDInsightCluster* 및 *New-AzureHDInsightCluster*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="1d578-154">매개 변수 및 스위치에는 새 이름이 있을 수 있고 ARM을 사용하는 경우 많은 새 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="1d578-155">예를 들어 일부 cmdlet에는 *-ResourceGroupName*이라는 새 스위치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="1d578-156">HDInsight cmdlet를 사용하기 전에 Azure 계정에 연결하고 새 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="1d578-157">Login-AzureRmAccount 또는 [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="1d578-158">[Azure Resource Manager를 사용하여 서비스 사용자 인증](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="1d578-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="1d578-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1d578-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="1d578-160">이름이 바뀐 cmdlet</span><span class="sxs-lookup"><span data-stu-id="1d578-160">Renamed cmdlets</span></span>
<span data-ttu-id="1d578-161">Windows PowerShell 콘솔에서 HDInsight ASM cmdlet을 나열하려면:</span><span class="sxs-lookup"><span data-stu-id="1d578-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="1d578-162">다음 테이블에서 ASM cmdlet 및 ARM 모드인 해당 이름을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="1d578-163">ASM cmdlet</span><span class="sxs-lookup"><span data-stu-id="1d578-163">ASM cmdlets</span></span> | <span data-ttu-id="1d578-164">ARM cmdlet</span><span class="sxs-lookup"><span data-stu-id="1d578-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="1d578-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="1d578-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="1d578-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="1d578-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="1d578-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="1d578-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="1d578-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="1d578-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="1d578-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="1d578-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="1d578-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="1d578-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="1d578-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="1d578-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="1d578-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="1d578-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="1d578-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="1d578-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="1d578-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="1d578-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="1d578-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="1d578-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="1d578-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="1d578-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="1d578-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="1d578-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="1d578-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="1d578-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="1d578-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="1d578-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="1d578-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="1d578-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="1d578-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="1d578-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="1d578-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="1d578-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="1d578-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="1d578-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="1d578-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="1d578-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="1d578-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="1d578-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="1d578-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="1d578-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="1d578-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="1d578-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="1d578-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="1d578-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="1d578-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="1d578-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="1d578-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="1d578-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="1d578-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="1d578-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="1d578-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="1d578-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="1d578-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="1d578-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="1d578-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="1d578-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="1d578-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="1d578-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="1d578-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="1d578-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="1d578-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="1d578-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="1d578-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="1d578-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="1d578-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="1d578-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="1d578-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="1d578-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="1d578-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="1d578-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="1d578-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="1d578-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="1d578-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="1d578-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="1d578-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="1d578-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="1d578-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="1d578-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="1d578-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="1d578-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="1d578-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="1d578-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="1d578-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="1d578-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="1d578-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="1d578-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="1d578-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="1d578-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="1d578-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="1d578-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="1d578-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="1d578-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="1d578-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="1d578-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="1d578-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="1d578-219">새 cmdlet</span><span class="sxs-lookup"><span data-stu-id="1d578-219">New cmdlets</span></span>
<span data-ttu-id="1d578-220">ARM 모드에서만 사용할 수 있는 새 cmdlet은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="1d578-221">**cmdlet 관련 스크립트 작업:**</span><span class="sxs-lookup"><span data-stu-id="1d578-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="1d578-222">**Get-AzureRmHDInsightPersistedScriptAction**: 클러스터에 대한 지속형 스크립트 동작을 가져와 시간 순서로 나열하거나 지정된 지속형 스크립트 동작에 대한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="1d578-223">**Get-AzureRmHDInsightScriptActionHistory**: 클러스터에 대한 스크립트 동작 기록을 가져와 시간 순서로 나열하거나 이전에 실행된 스크립트 동작의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="1d578-224">**Remove-AzureRmHDInsightPersistedScriptAction**: HDInsight 클러스터에서 지속형 스크립트 동작을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="1d578-225">**Set-AzureRmHDInsightPersistedScriptAction**: 이전에 실행된 스크립트 동작을 지속형 스크립트 동작으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="1d578-226">**Submit-AzureRmHDInsightScriptAction**: Azure HDInsight 클러스터에 새 스크립트 동작을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="1d578-227">추가 사용 정보는 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d578-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="1d578-228">**cmdlet 관련 클러스터 ID:**</span><span class="sxs-lookup"><span data-stu-id="1d578-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="1d578-229">**Add-AzureRmHDInsightClusterIdentity**: HDInsight 클러스터가 Azure Data Lake Stores에 액세스할 수 있도록 클러스터 구성 개체에 클러스터 ID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="1d578-230">[Azure PowerShell을 사용하여 Data Lake 저장소로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d578-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="1d578-231">예</span><span class="sxs-lookup"><span data-stu-id="1d578-231">Examples</span></span>
<span data-ttu-id="1d578-232">**클러스터 만들기**</span><span class="sxs-lookup"><span data-stu-id="1d578-232">**Create cluster**</span></span>

<span data-ttu-id="1d578-233">이전 명령(ASM):</span><span class="sxs-lookup"><span data-stu-id="1d578-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="1d578-234">새 명령(ARM):</span><span class="sxs-lookup"><span data-stu-id="1d578-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="1d578-235">**클러스터 삭제**</span><span class="sxs-lookup"><span data-stu-id="1d578-235">**Delete cluster**</span></span>

<span data-ttu-id="1d578-236">이전 명령(ASM):</span><span class="sxs-lookup"><span data-stu-id="1d578-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="1d578-237">새 명령(ARM):</span><span class="sxs-lookup"><span data-stu-id="1d578-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="1d578-238">**클러스터 나열**</span><span class="sxs-lookup"><span data-stu-id="1d578-238">**List cluster**</span></span>

<span data-ttu-id="1d578-239">이전 명령(ASM):</span><span class="sxs-lookup"><span data-stu-id="1d578-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="1d578-240">새 명령(ARM):</span><span class="sxs-lookup"><span data-stu-id="1d578-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="1d578-241">**클러스터 표시**</span><span class="sxs-lookup"><span data-stu-id="1d578-241">**Show cluster**</span></span>

<span data-ttu-id="1d578-242">이전 명령(ASM):</span><span class="sxs-lookup"><span data-stu-id="1d578-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="1d578-243">새 명령(ARM):</span><span class="sxs-lookup"><span data-stu-id="1d578-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="1d578-244">다른 샘플</span><span class="sxs-lookup"><span data-stu-id="1d578-244">Other samples</span></span>
* [<span data-ttu-id="1d578-245">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1d578-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="1d578-246">Hive 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1d578-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="1d578-247">Pig 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1d578-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="1d578-248">Sqoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1d578-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="1d578-249">ARM 기반 HDInsight .NET SDK로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="1d578-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="1d578-250">Azure 서비스 관리 기반 [(ASM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) 는 이제 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="1d578-251">Azure 리소스 관리 기반 [(ARM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="1d578-252">다음 ASM 기반 HDInsight 패키지는 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="1d578-253">이 섹션에서는 ARM 기반 SDK를 사용하여 특정 작업을 수행하는 방법에 대한 자세한 정보의 포인터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="1d578-254">방법... ARM 기반 HDInsight SDK 사용</span><span class="sxs-lookup"><span data-stu-id="1d578-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="1d578-255">링크</span><span class="sxs-lookup"><span data-stu-id="1d578-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="1d578-256">.NET SDK를 사용하여 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1d578-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="1d578-257">[.NET SDK를 사용하여 HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="1d578-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="1d578-258">.NET SDK와 스크립트 작업을 사용하여 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1d578-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="1d578-259">[스크립트 작업을 사용하여 HDInsight Linux 클러스터 사용자 지정](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="1d578-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="1d578-260">.NET SDK와 Azure Active Directory를 사용하여 대화형으로 응용 프로그램 인증</span><span class="sxs-lookup"><span data-stu-id="1d578-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="1d578-261">[.NET SDK를 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d578-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="1d578-262">이 문서의 코드 조각에서는 대화형 인증 접근 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="1d578-263">.NET SDK와 Azure Active Directory를 사용하여 비대화형으로 응용 프로그램 인증</span><span class="sxs-lookup"><span data-stu-id="1d578-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="1d578-264">[HDInsight에 대한 비대화형 응용 프로그램 만들기](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="1d578-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="1d578-265">.NET SDK를 사용하여 Hive 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1d578-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="1d578-266">[Hive 작업 제출](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="1d578-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="1d578-267">.NET SDK를 사용하여 Pig 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1d578-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="1d578-268">[Pig 작업 제출](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="1d578-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="1d578-269">.NET SDK를 사용하여 Sqoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="1d578-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="1d578-270">[Sqoop 작업 제출](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="1d578-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="1d578-271">.NET SDK를 사용하여 HDInsight 클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="1d578-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="1d578-272">[HDInsight 클러스터 나열](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="1d578-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="1d578-273">.NET SDK를 사용하여 HDInsight 클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="1d578-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="1d578-274">[HDInsight 클러스터 크기 조정](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="1d578-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="1d578-275">.NET SDK를 사용하여 HDInsight 클러스터에 대한 액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="1d578-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="1d578-276">[HDInsight 클러스터에 대한 액세스 권한 부여/해지](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="1d578-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="1d578-277">.NET SDK를 사용하여 HDInsight 클러스터에 대한 HTTP 사용자 자격 증명 업데이트</span><span class="sxs-lookup"><span data-stu-id="1d578-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="1d578-278">[HDInsight 클러스터에 대한 HTTP 사용자 자격 증명 업데이트](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="1d578-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="1d578-279">.NET SDK를 사용하여 HDInsight 클러스터에 대한 기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="1d578-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="1d578-280">[HDInsight 클러스터에 대한 기본 저장소 계정 찾기](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="1d578-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="1d578-281">.NET SDK를 사용하여 HDInsight 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="1d578-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="1d578-282">[HDInsight 클러스터 삭제](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="1d578-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="1d578-283">예</span><span class="sxs-lookup"><span data-stu-id="1d578-283">Examples</span></span>
<span data-ttu-id="1d578-284">다음은 ARM 기반 SDK 및 ASM 기반 SDK에 해당하는 코드 조각을 사용하여 작업을 수행하는 방법에 대한 일부 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1d578-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="1d578-285">**클러스터 CRUD 클라이언트 만들기**</span><span class="sxs-lookup"><span data-stu-id="1d578-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="1d578-286">이전 명령(ASM)</span><span class="sxs-lookup"><span data-stu-id="1d578-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="1d578-287">새 명령(ARM)(서비스 주체 권한 부여)</span><span class="sxs-lookup"><span data-stu-id="1d578-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="1d578-288">새 명령(ARM)(사용자 권한 부여)</span><span class="sxs-lookup"><span data-stu-id="1d578-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="1d578-289">**클러스터 만들기**</span><span class="sxs-lookup"><span data-stu-id="1d578-289">**Creating a cluster**</span></span>

* <span data-ttu-id="1d578-290">이전 명령(ASM)</span><span class="sxs-lookup"><span data-stu-id="1d578-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="1d578-291">새 명령(ARM)</span><span class="sxs-lookup"><span data-stu-id="1d578-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="1d578-292">**HTTP 액세스 사용**</span><span class="sxs-lookup"><span data-stu-id="1d578-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="1d578-293">이전 명령(ASM)</span><span class="sxs-lookup"><span data-stu-id="1d578-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="1d578-294">새 명령(ARM)</span><span class="sxs-lookup"><span data-stu-id="1d578-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="1d578-295">**클러스터 삭제**</span><span class="sxs-lookup"><span data-stu-id="1d578-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="1d578-296">이전 명령(ASM)</span><span class="sxs-lookup"><span data-stu-id="1d578-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="1d578-297">새 명령(ARM)</span><span class="sxs-lookup"><span data-stu-id="1d578-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

