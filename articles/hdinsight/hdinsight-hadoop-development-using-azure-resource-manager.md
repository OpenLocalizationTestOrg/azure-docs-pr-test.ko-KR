---
title: "HDInsight에 대 한 aaaMigrate tooAzure 리소스 관리자 도구 | Microsoft Docs"
description: "HDInsight 클러스터에 대 한 toomigrate tooAzure 리소스 관리자 개발 도구 하는 방법"
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
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="56b0c-103">HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구</span><span class="sxs-lookup"><span data-stu-id="56b0c-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="56b0c-104">HDInsight에서는 HDInsight용 ASM(Azure 서비스 관리자) 기반 도구를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="56b0c-105">사용 된 Azure PowerShell, Azure CLI 또는 hello HDInsight.NET SDK toowork HDInsight 클러스터를 모르는 경우 hello Azure 리소스 관리자 ARM 기반 PowerShell, CLI 및 앞으로.NET SDK 버전 toouse 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="56b0c-106">이 문서는 방법에 대 한 포인터를 제공 toomigrate toohello 새로운 ARM 기반 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="56b0c-107">해당 되는 경우이 문서의 링크 HDInsight에 대 한 hello ASM 및 ARM 방법 hello 차이점 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56b0c-108">ASM에 대 한 hello 지원 기반 CLI, PowerShell 및.NET SDK 중단 됩니다. **2017 년 1 월 1**합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="56b0c-109">마이그레이션 Azure CLI tooAzure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="56b0c-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="56b0c-110">hello Azure CLI tooAzure 리소스 관리자 (ARM) 모드를; 이전 설치에서 업그레이드 하는 경우가 아니면 이제 기본적으로 이 경우 toouse hello를 할 수 있습니다 `azure config mode arm` 명령 tooswitch tooARM 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="56b0c-111">Azure 서비스 관리 (ASM)를 사용 하 여 HDInsight toowork 제공 Azure CLI 해당 hello ARM;를 사용 하는 경우 동일한 hello는 hello 기본 명령 그러나 일부 매개 변수 및 스위치 새 이름을 없고 많은 새로운 매개 변수가 사용할 수 있는 ARM를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="56b0c-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="56b0c-112">예를 들어 이제 사용할 수 있습니다 `azure hdinsight cluster create` toospecify hello Azure 가상 네트워크를 클러스터에서를 만들지 또는 Hive 및 Oozie metastore 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="56b0c-113">Azure Resource Manager를 통한 HDInsight를 사용하는 기본 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="56b0c-114">`azure hdinsight cluster create` - 새 HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="56b0c-115">`azure hdinsight cluster delete` - 새 HDInsight 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="56b0c-116">`azure hdinsight cluster show` - 기존 클러스터에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="56b0c-117">`azure hdinsight cluster list` - Azure 구독에 대한 HDInsight 클러스터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="56b0c-118">사용 하 여 hello `-h` tooinspect hello 매개 변수 및 명령에 따라 사용할 수 있는 스위치를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="56b0c-119">새 명령</span><span class="sxs-lookup"><span data-stu-id="56b0c-119">New commands</span></span>
<span data-ttu-id="56b0c-120">Azure Resource Manager로 사용할 수 있는 새 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="56b0c-121">`azure hdinsight cluster resize`-동적으로 변경 내용을 hello hello 클러스터의 작업자 노드 수</span><span class="sxs-lookup"><span data-stu-id="56b0c-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="56b0c-122">`azure hdinsight cluster enable-http-access`-HTTPs 액세스 toohello 클러스터 (에 기본적으로)</span><span class="sxs-lookup"><span data-stu-id="56b0c-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="56b0c-123">`azure hdinsight cluster disable-http-access`-HTTPs 액세스 toohello 클러스터를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="56b0c-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="56b0c-124">`azure hdinsight script-action` - 클러스터에서 스크립트 작업을 만들기/관리하기 위한 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="56b0c-125">`azure hdinsight config`-hello로 사용 될 수 있는 구성 파일을 만드는 명령을 제공 `hdinsight cluster create` 명령 tooprovide 구성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="56b0c-126">사용되지 않는 명령</span><span class="sxs-lookup"><span data-stu-id="56b0c-126">Deprecated commands</span></span>
<span data-ttu-id="56b0c-127">Hello를 사용 하는 경우 `azure hdinsight job` 명령 toosubmit 작업 tooyour HDInsight 클러스터를 사용할 수 없는 hello ARM 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="56b0c-128">스크립트에서 전송 작업 tooHDInsight tooprogrammatically 해야 할 경우 hello HDInsight에서 제공 하는 REST Api를 대신 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="56b0c-129">REST Api를 사용 하 여 작업 등록에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="56b0c-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="56b0c-130">cURL을 사용하여 HDInsight에서 Hadoop과 MapReduce 작업 실행</span><span class="sxs-lookup"><span data-stu-id="56b0c-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="56b0c-131">cURL을 사용하여 HDInsight에서 Hadoop과 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="56b0c-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="56b0c-132">cURL을 사용하여 HDInsight에서 Hadoop과 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="56b0c-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="56b0c-133">다른 방법으로 toorun MapReduce 대 한 자세한 내용은, Hive 및 Pig 대화형으로 참조 하십시오 [HDInsight에서 Hadoop으로 사용 하 여 MapReduce](hdinsight-use-mapreduce.md), [HDInsight에서 Hadoop으로 사용 하 여 하이브](hdinsight-use-hive.md), 및 [Pig에서 Hadoop으로 HDInsight](hdinsight-use-pig.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="56b0c-134">예</span><span class="sxs-lookup"><span data-stu-id="56b0c-134">Examples</span></span>
<span data-ttu-id="56b0c-135">**클러스터 만들기**</span><span class="sxs-lookup"><span data-stu-id="56b0c-135">**Creating a cluster**</span></span>

* <span data-ttu-id="56b0c-136">이전 명령(ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="56b0c-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="56b0c-137">새 명령(ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="56b0c-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="56b0c-138">**클러스터 삭제**</span><span class="sxs-lookup"><span data-stu-id="56b0c-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="56b0c-139">이전 명령(ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="56b0c-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="56b0c-140">새 명령(ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="56b0c-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="56b0c-141">**클러스터 나열**</span><span class="sxs-lookup"><span data-stu-id="56b0c-141">**List clusters**</span></span>

* <span data-ttu-id="56b0c-142">이전 명령(ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="56b0c-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="56b0c-143">새 명령(ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="56b0c-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="56b0c-144">리소스 그룹을 사용 하 여 hello 지정 hello 목록 명령에 대 한 `-g` hello 지정 된 리소스 그룹의 hello 클러스터만을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="56b0c-145">**클러스터 정보 표시**</span><span class="sxs-lookup"><span data-stu-id="56b0c-145">**Show cluster information**</span></span>

* <span data-ttu-id="56b0c-146">이전 명령(ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="56b0c-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="56b0c-147">새 명령(ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="56b0c-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="56b0c-148">Azure PowerShell tooAzure 리소스 관리자가 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="56b0c-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="56b0c-149">hello Azure 리소스 관리자 (ARM) 모드에서 Azure PowerShell에 대 한 hello 일반 정보에서 찾을 수 있습니다 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](../powershell-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="56b0c-150">hello Azure PowerShell ARM cmdlet hello ASM cmdlet와 함께 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="56b0c-151">hello 두 가지 모드에서 hello cmdlet은 이름으로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="56b0c-152">hello ARM 모드는 *AzureRmHDInsight* 너무 비교 hello cmdlet 이름에서*AzureHDInsight* hello ASM 모드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="56b0c-153">예를 들면 *New-AzureRmHDInsightCluster* 및 *New-AzureHDInsightCluster*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="56b0c-154">매개 변수 및 스위치에는 새 이름이 있을 수 있고 ARM을 사용하는 경우 많은 새 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="56b0c-155">예를 들어 일부 cmdlet에는 *-ResourceGroupName*이라는 새 스위치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="56b0c-156">Hello HDInsight cmdlet을 사용 하려면 먼저 tooyour Azure 계정을 연결 하 고 새 리소스 그룹을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="56b0c-157">Login-AzureRmAccount 또는 [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="56b0c-158">[Azure Resource Manager를 사용하여 서비스 사용자 인증](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="56b0c-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="56b0c-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="56b0c-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="56b0c-160">이름이 바뀐 cmdlet</span><span class="sxs-lookup"><span data-stu-id="56b0c-160">Renamed cmdlets</span></span>
<span data-ttu-id="56b0c-161">toolist hello Windows PowerShell 콘솔에서 ASM HDInsight cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56b0c-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="56b0c-162">hello 다음 표에 hello ASM cmdlet 및 hello ARM 모드에 해당 이름을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="56b0c-163">ASM cmdlet</span><span class="sxs-lookup"><span data-stu-id="56b0c-163">ASM cmdlets</span></span> | <span data-ttu-id="56b0c-164">ARM cmdlet</span><span class="sxs-lookup"><span data-stu-id="56b0c-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="56b0c-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="56b0c-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="56b0c-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="56b0c-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="56b0c-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="56b0c-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="56b0c-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="56b0c-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="56b0c-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="56b0c-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="56b0c-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="56b0c-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="56b0c-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="56b0c-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="56b0c-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="56b0c-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="56b0c-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="56b0c-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="56b0c-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="56b0c-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="56b0c-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="56b0c-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="56b0c-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="56b0c-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="56b0c-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="56b0c-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="56b0c-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="56b0c-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="56b0c-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="56b0c-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="56b0c-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="56b0c-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="56b0c-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="56b0c-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="56b0c-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="56b0c-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="56b0c-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="56b0c-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="56b0c-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="56b0c-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="56b0c-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="56b0c-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="56b0c-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="56b0c-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="56b0c-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="56b0c-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="56b0c-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="56b0c-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="56b0c-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="56b0c-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="56b0c-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="56b0c-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="56b0c-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="56b0c-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="56b0c-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="56b0c-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="56b0c-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="56b0c-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="56b0c-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="56b0c-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="56b0c-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="56b0c-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="56b0c-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="56b0c-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="56b0c-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="56b0c-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="56b0c-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="56b0c-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="56b0c-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="56b0c-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="56b0c-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="56b0c-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="56b0c-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="56b0c-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="56b0c-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="56b0c-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="56b0c-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="56b0c-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="56b0c-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="56b0c-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="56b0c-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="56b0c-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="56b0c-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="56b0c-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="56b0c-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="56b0c-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="56b0c-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="56b0c-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="56b0c-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="56b0c-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="56b0c-219">새 cmdlet</span><span class="sxs-lookup"><span data-stu-id="56b0c-219">New cmdlets</span></span>
<span data-ttu-id="56b0c-220">hello 다음 hello 에서만 hello ARM 모드에서 사용할 수 있는 새로운 cmdlet은입니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="56b0c-221">**cmdlet 관련 스크립트 작업:**</span><span class="sxs-lookup"><span data-stu-id="56b0c-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="56b0c-222">**Get AzureRmHDInsightPersistedScriptAction**: 가져옵니다 hello 클러스터에 대 한 스크립트 작업을 유지 하 고 시간 순서로 나열 또는 지정 된 지속형된 스크립트 동작에 대 한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="56b0c-223">**Get AzureRmHDInsightScriptActionHistory**: 클러스터에 대 한 hello 스크립트 동작 기록을 가져옵니다 및 시간 순서 대로 나열 하거나 이전에 실행된 한 스크립트 작업의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="56b0c-224">**Remove-AzureRmHDInsightPersistedScriptAction**: HDInsight 클러스터에서 지속형 스크립트 동작을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="56b0c-225">**집합 AzureRmHDInsightPersistedScriptAction**: 이전에 실행된 한 스크립트 작업 toobe 지속형된 스크립트 동작을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="56b0c-226">**제출 AzureRmHDInsightScriptAction**: 새 스크립트 동작이 tooan Azure HDInsight 클러스터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="56b0c-227">추가 사용 정보는 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56b0c-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="56b0c-228">**cmdlet 관련 클러스터 ID:**</span><span class="sxs-lookup"><span data-stu-id="56b0c-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="56b0c-229">**추가 AzureRmHDInsightClusterIdentity**: hello HDInsight 클러스터에 액세스할 수 있는 Azure 데이터 레이크 저장소 클러스터 id tooa 클러스터 구성 개체를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="56b0c-230">[Azure PowerShell을 사용하여 Data Lake 저장소로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56b0c-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="56b0c-231">예</span><span class="sxs-lookup"><span data-stu-id="56b0c-231">Examples</span></span>
<span data-ttu-id="56b0c-232">**클러스터 만들기**</span><span class="sxs-lookup"><span data-stu-id="56b0c-232">**Create cluster**</span></span>

<span data-ttu-id="56b0c-233">이전 명령(ASM):</span><span class="sxs-lookup"><span data-stu-id="56b0c-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="56b0c-234">새 명령(ARM):</span><span class="sxs-lookup"><span data-stu-id="56b0c-234">New command (ARM):</span></span>

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


<span data-ttu-id="56b0c-235">**클러스터 삭제**</span><span class="sxs-lookup"><span data-stu-id="56b0c-235">**Delete cluster**</span></span>

<span data-ttu-id="56b0c-236">이전 명령(ASM):</span><span class="sxs-lookup"><span data-stu-id="56b0c-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="56b0c-237">새 명령(ARM):</span><span class="sxs-lookup"><span data-stu-id="56b0c-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="56b0c-238">**클러스터 나열**</span><span class="sxs-lookup"><span data-stu-id="56b0c-238">**List cluster**</span></span>

<span data-ttu-id="56b0c-239">이전 명령(ASM):</span><span class="sxs-lookup"><span data-stu-id="56b0c-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="56b0c-240">새 명령(ARM):</span><span class="sxs-lookup"><span data-stu-id="56b0c-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="56b0c-241">**클러스터 표시**</span><span class="sxs-lookup"><span data-stu-id="56b0c-241">**Show cluster**</span></span>

<span data-ttu-id="56b0c-242">이전 명령(ASM):</span><span class="sxs-lookup"><span data-stu-id="56b0c-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="56b0c-243">새 명령(ARM):</span><span class="sxs-lookup"><span data-stu-id="56b0c-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="56b0c-244">다른 샘플</span><span class="sxs-lookup"><span data-stu-id="56b0c-244">Other samples</span></span>
* [<span data-ttu-id="56b0c-245">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="56b0c-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="56b0c-246">Hive 작업 제출</span><span class="sxs-lookup"><span data-stu-id="56b0c-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="56b0c-247">Pig 작업 제출</span><span class="sxs-lookup"><span data-stu-id="56b0c-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="56b0c-248">Sqoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="56b0c-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="56b0c-249">마이그레이션 toohello ARM 기반 HDInsight.NET SDK</span><span class="sxs-lookup"><span data-stu-id="56b0c-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="56b0c-250">Azure 서비스 관리-기반 hello [(ASM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) 는 이제 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="56b0c-251">것이 좋습니다 toouse는 Azure 리소스 관리 기반 hello [(ARM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="56b0c-252">hello 다음 ASM 기반 HDInsight 패키지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="56b0c-253">이 섹션에서는 포인터 toomore 정보는 방법에 특정 작업을 사용 하 여 hello ARM 기반 SDK tooperform 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="56b0c-254">방법... ARM 기반 HDInsight SDK hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="56b0c-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="56b0c-255">링크</span><span class="sxs-lookup"><span data-stu-id="56b0c-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="56b0c-256">.NET SDK를 사용하여 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="56b0c-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="56b0c-257">[.NET SDK를 사용하여 HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="56b0c-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="56b0c-258">.NET SDK와 스크립트 작업을 사용하여 클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="56b0c-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="56b0c-259">[스크립트 작업을 사용하여 HDInsight Linux 클러스터 사용자 지정](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="56b0c-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="56b0c-260">.NET SDK와 Azure Active Directory를 사용하여 대화형으로 응용 프로그램 인증</span><span class="sxs-lookup"><span data-stu-id="56b0c-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="56b0c-261">[.NET SDK를 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56b0c-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="56b0c-262">이 문서에서 코드 조각 hello hello 대화형 인증 접근 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="56b0c-263">.NET SDK와 Azure Active Directory를 사용하여 비대화형으로 응용 프로그램 인증</span><span class="sxs-lookup"><span data-stu-id="56b0c-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="56b0c-264">[HDInsight에 대한 비대화형 응용 프로그램 만들기](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="56b0c-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="56b0c-265">.NET SDK를 사용하여 Hive 작업 제출</span><span class="sxs-lookup"><span data-stu-id="56b0c-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="56b0c-266">[Hive 작업 제출](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="56b0c-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="56b0c-267">.NET SDK를 사용하여 Pig 작업 제출</span><span class="sxs-lookup"><span data-stu-id="56b0c-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="56b0c-268">[Pig 작업 제출](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="56b0c-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="56b0c-269">.NET SDK를 사용하여 Sqoop 작업 제출</span><span class="sxs-lookup"><span data-stu-id="56b0c-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="56b0c-270">[Sqoop 작업 제출](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="56b0c-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="56b0c-271">.NET SDK를 사용하여 HDInsight 클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="56b0c-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="56b0c-272">[HDInsight 클러스터 나열](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="56b0c-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="56b0c-273">.NET SDK를 사용하여 HDInsight 클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="56b0c-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="56b0c-274">[HDInsight 클러스터 크기 조정](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="56b0c-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="56b0c-275">Grant/revoke access tooHDInsight.NET SDK를 사용 하는 클러스터</span><span class="sxs-lookup"><span data-stu-id="56b0c-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="56b0c-276">참조 [Grant/revoke access tooHDInsight 클러스터](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="56b0c-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="56b0c-277">.NET SDK를 사용하여 HDInsight 클러스터에 대한 HTTP 사용자 자격 증명 업데이트</span><span class="sxs-lookup"><span data-stu-id="56b0c-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="56b0c-278">[HDInsight 클러스터에 대한 HTTP 사용자 자격 증명 업데이트](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="56b0c-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="56b0c-279">.NET SDK를 사용 하 여 HDInsight 클러스터에 대 한 hello 기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="56b0c-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="56b0c-280">참조 [hello 기본 저장소 계정이 HDInsight 클러스터에 대 한 찾기](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="56b0c-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="56b0c-281">.NET SDK를 사용하여 HDInsight 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="56b0c-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="56b0c-282">[HDInsight 클러스터 삭제](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="56b0c-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="56b0c-283">예</span><span class="sxs-lookup"><span data-stu-id="56b0c-283">Examples</span></span>
<span data-ttu-id="56b0c-284">다음은 작업을 하는 방법을 보여 주는 예 hello ARM 기반 SDK에 대 한 hello ASM 기반 SDK 및 해당 하는 코드 조각 hello 사용 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b0c-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="56b0c-285">**클러스터 CRUD 클라이언트 만들기**</span><span class="sxs-lookup"><span data-stu-id="56b0c-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="56b0c-286">이전 명령(ASM)</span><span class="sxs-lookup"><span data-stu-id="56b0c-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="56b0c-287">새 명령(ARM)(서비스 주체 권한 부여)</span><span class="sxs-lookup"><span data-stu-id="56b0c-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="56b0c-288">새 명령(ARM)(사용자 권한 부여)</span><span class="sxs-lookup"><span data-stu-id="56b0c-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="56b0c-289">**클러스터 만들기**</span><span class="sxs-lookup"><span data-stu-id="56b0c-289">**Creating a cluster**</span></span>

* <span data-ttu-id="56b0c-290">이전 명령(ASM)</span><span class="sxs-lookup"><span data-stu-id="56b0c-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="56b0c-291">새 명령(ARM)</span><span class="sxs-lookup"><span data-stu-id="56b0c-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="56b0c-292">**HTTP 액세스 사용**</span><span class="sxs-lookup"><span data-stu-id="56b0c-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="56b0c-293">이전 명령(ASM)</span><span class="sxs-lookup"><span data-stu-id="56b0c-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="56b0c-294">새 명령(ARM)</span><span class="sxs-lookup"><span data-stu-id="56b0c-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="56b0c-295">**클러스터 삭제**</span><span class="sxs-lookup"><span data-stu-id="56b0c-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="56b0c-296">이전 명령(ASM)</span><span class="sxs-lookup"><span data-stu-id="56b0c-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="56b0c-297">새 명령(ARM)</span><span class="sxs-lookup"><span data-stu-id="56b0c-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

