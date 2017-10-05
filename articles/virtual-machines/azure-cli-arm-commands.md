---
title: "Resource Manager 모드에서 Azure CLI 명령 | Microsoft Docs"
description: "리소스 관리자 배포 모델에서 리소스를 관리하는 Azure CLI(명령줄 인터페이스) 명령"
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: be957651af78519f678321aec511b71cb18a85f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="caf9d-103">리소스 관리자 모드에서 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="caf9d-104">이 문서에서는 Azure Resource Manager 배포 모델에서 일반적으로 Azure 리소스를 만들고 관리하는 데 사용한 Azure CLI(명령줄 인터페이스) 명령에 대한 구문 및 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use to create and manage Azure resources in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="caf9d-105">ARM(Azure Resource Manager) 모드에서 CLI를 실행하여 이러한 명령에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-105">You access these commands by running the CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="caf9d-106">전체 참조는 아니며 CLI 버전에서 약간 다른 명령 또는 매개 변수를 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="caf9d-107">Azure 리소스 및 리소스 그룹에 대한 일반적인 개요는 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="caf9d-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="caf9d-108">이 문서에서는 Azure CLI(또는 Azure CLI 1.0)에서의 Resource Manager 모드 명령을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-108">This article shows Resource Manager mode commands in the Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="caf9d-109">Resource Manager 모델에서 작업하기 위해 차세대 멀티 플랫폼 CLI인 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 사용해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-109">To work in the Resource Manager model, you can also try the [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="caf9d-110">[기존 및 새 Azure CLI](/cli/azure/old-and-new-clis)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="caf9d-110">Find out more about the [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="caf9d-111">시작하려면 먼저 [Azure CLI](../cli-install-nodejs.md)를 설치하고 [Azure 구독에 연결](../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-111">To get started, first [install the Azure CLI](../cli-install-nodejs.md) and [connect to your Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="caf9d-112">리소스 관리자 모드의 명령줄에 있는 현재 명령 구문 및 옵션의 경우 `azure help`를 입력합니다. 그렇지 않고 특정 명령에 대한 도움말을 표시하려면 `azure help [command]`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-112">For current command syntax and options at the command line in Resource Manager mode, type `azure help` or, to display help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="caf9d-113">또한 설명서에 특정 Azure 서비스 만들기 및 관리에 대한 CLI 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-113">Also find CLI examples in the documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="caf9d-114">선택적 매개 변수는 대괄호 안에 표시(예: `[parameter]`)됩니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="caf9d-115">모든 다른 매개 변수는 필수 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-115">All other parameters are required.</span></span>

<span data-ttu-id="caf9d-116">여기에 언급된 명령 관련 선택적 매개 변수 이외에 요청 옵션, 상태 코드 등과 같은 자세한 출력을 표시하는 데 사용할 수 있는 세 가지 선택적 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-116">In addition to command-specific optional parameters documented here, there are three optional parameters that can be used to display detailed output such as request options and status codes.</span></span> <span data-ttu-id="caf9d-117">`-v` 매개 변수는 자세한 정보를 출력하고 `-vv` 매개 변수는 훨씬 더 자세한 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-117">The `-v` parameter provides verbose output, and the `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="caf9d-118">`--json` 옵션은 결과를 원시 JSON 형식으로 결과를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-118">The `--json` option outputs the result in raw json format.</span></span>

## <a name="setting-the-resource-manager-mode"></a><span data-ttu-id="caf9d-119">리소스 관리자 모드 설정</span><span class="sxs-lookup"><span data-stu-id="caf9d-119">Setting the Resource Manager mode</span></span>
<span data-ttu-id="caf9d-120">다음 명령을 사용하여 Azure CLI Resource Manager 모드 명령을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-120">Use the following command to enable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="caf9d-121">CLI의 Azure Resource Manager 모드 및 Azure 서비스 관리 모드는 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-121">The CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="caf9d-122">즉, 한 모드에서 만든 리소스는 다른 모드에서 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-122">That is, resources created in one mode cannot be managed from the other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="caf9d-123">Azure account: 계정 정보 관리</span><span class="sxs-lookup"><span data-stu-id="caf9d-123">azure account: Manage your account information</span></span>
<span data-ttu-id="caf9d-124">Azure 구독 정보는 도구에서 계정에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-124">Your Azure subscription information is used by the tool to connect to your account.</span></span>

<span data-ttu-id="caf9d-125">**가져온 구독 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-125">**List the imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="caf9d-126">**구독에 대한 자세한 정보 표시**</span><span class="sxs-lookup"><span data-stu-id="caf9d-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="caf9d-127">**현재 구독 설정**</span><span class="sxs-lookup"><span data-stu-id="caf9d-127">**Set the current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="caf9d-128">**구독 또는 환경을 제거하거나 저장된 계정 및 환경 정보 모두 지우기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-128">**Remove a subscription or environment, or clear all of the stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="caf9d-129">**계정 환경을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-129">**Commands to manage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-to-display-active-directory-objects"></a><span data-ttu-id="caf9d-130">azure ad: Active Directory 개체를 표시하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-130">azure ad: Commands to display Active Directory objects</span></span>
<span data-ttu-id="caf9d-131">**Active Directory 응용 프로그램을 표시하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-131">**Commands to display active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="caf9d-132">**Active Directory 그룹을 표시하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-132">**Commands to display active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="caf9d-133">**Active Directory 하위 그룹 또는 멤버 정보를 제공하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-133">**Commands to provide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="caf9d-134">**Active Directory 서비스 주체를 표시하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-134">**Commands to display active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="caf9d-135">**Active Directory 사용자를 표시하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-135">**Commands to display active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-to-manage-your-availability-sets"></a><span data-ttu-id="caf9d-136">azure availset: 가용성 집합을 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-136">azure availset: commands to manage your availability sets</span></span>
<span data-ttu-id="caf9d-137">**리소스 그룹 내 가용성 집합 만들기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="caf9d-138">**리소스 그룹 내 가용성 집합 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-138">**Lists the availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="caf9d-139">**리소스 그룹 내 한 가용성 집합 가져오기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="caf9d-140">**리소스 그룹 내 한 가용성 집합 삭제**</span><span class="sxs-lookup"><span data-stu-id="caf9d-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-to-manage-your-local-settings"></a><span data-ttu-id="caf9d-141">azure config: 로컬 설정을 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-141">azure config: commands to manage your local settings</span></span>
<span data-ttu-id="caf9d-142">**Azure CLI 구성 설정 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="caf9d-143">**구성 설정 삭제**</span><span class="sxs-lookup"><span data-stu-id="caf9d-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="caf9d-144">**구성 설정 업데이트**</span><span class="sxs-lookup"><span data-stu-id="caf9d-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="caf9d-145">**Azure CLI 작업 모드를 `arm` 또는 `asm`으로 설정**</span><span class="sxs-lookup"><span data-stu-id="caf9d-145">**Sets the Azure CLI working mode to either `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-to-manage-account-features"></a><span data-ttu-id="caf9d-146">azure feature: 계정 기능을 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-146">azure feature: commands to manage account features</span></span>
<span data-ttu-id="caf9d-147">**구독에 대해 사용할 수 있는 모든 기능 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="caf9d-148">**기능 표시**</span><span class="sxs-lookup"><span data-stu-id="caf9d-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="caf9d-149">**리소스 공급자의 미리 본 기능 등록**</span><span class="sxs-lookup"><span data-stu-id="caf9d-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-to-manage-your-resource-groups"></a><span data-ttu-id="caf9d-150">azure group: 리소스 그룹을 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-150">azure group: Commands to manage your resource groups</span></span>
<span data-ttu-id="caf9d-151">**리소스 그룹 만들기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="caf9d-152">**리소스 그룹에 태그 설정**</span><span class="sxs-lookup"><span data-stu-id="caf9d-152">**Set tags to a resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="caf9d-153">**리소스 그룹 삭제**</span><span class="sxs-lookup"><span data-stu-id="caf9d-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="caf9d-154">**구독에 대한 리소스 그룹 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-154">**Lists the resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="caf9d-155">**구독에 대한 리소스 그룹 표시**</span><span class="sxs-lookup"><span data-stu-id="caf9d-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="caf9d-156">**리소스 그룹 로그를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-156">**Commands to manage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="caf9d-157">**리소스 그룹의 배포를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-157">**Commands to manage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="caf9d-158">**사용자 로컬 또는 갤러리 리소스 그룹 템플릿을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-158">**Commands to manage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-to-manage-your-hdinsight-clusters"></a><span data-ttu-id="caf9d-159">azure hdinsight: HDInsight 클러스터를 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-159">azure hdinsight: Commands to manage your HDInsight clusters</span></span>
<span data-ttu-id="caf9d-160">**클러스터 구성 파일을 만들거나 클러스터 구성 파일에 추가하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-160">**Commands to create or add to a cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="caf9d-161">예: 클러스터를 만들 때 실행할 스크립트 동작을 포함하는 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-161">Example: Create a configuration file that contains a script action to run when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="caf9d-162">**리소스 그룹에 클러스터를 만드는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-162">**Command to create a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="caf9d-163">예: Linux 클러스터에 Storm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting the request to create cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="caf9d-164">예: 스크립트 동작으로 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting the request to create cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="caf9d-165">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       The name of the resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for the cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url to use for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key to the storage account to use for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in the storage account to use for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for the cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes to use for the cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for the cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for the cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for the cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for the cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In the format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for the external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for the external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for the external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for the external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for the external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for the external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for the external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for the external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    The subscription id
    --tags <tags>                                              Tags to set to the cluster.
    Can be multiple.
    In the format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="caf9d-166">**클러스터를 삭제하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-166">**Command to delete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="caf9d-167">**클러스터 세부 정보를 표시하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-167">**Command to show cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="caf9d-168">**특정 리소스 그룹의 모든 클러스터(제공된 경우)를 나열하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-168">**Command to list all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="caf9d-169">**클러스터 크기를 조정하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-169">**Command to resize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="caf9d-170">**클러스터에 대한 HTTP 액세스를 사용하도록 설정하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-170">**Command to enable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="caf9d-171">**클러스터에 대한 HTTP 액세스를 사용하지 않도록 설정하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-171">**Command to disable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="caf9d-172">**클러스터에 대한 RDP 액세스를 사용하도록 설정하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-172">**Command to enable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="caf9d-173">**클러스터에 대한 HTTP 액세스를 사용하지 않도록 설정하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-173">**Command to disable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-to-monitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="caf9d-174">azure insight: Insights 모니터링 관련 명령(이벤트, 경고 규칙, 자동 크기 조정 설정, 메트릭)</span><span class="sxs-lookup"><span data-stu-id="caf9d-174">azure insights: Commands related to monitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="caf9d-175">**구독, 상관 관계 ID, 리소스 그룹, 리소스 또는 리소스 공급자에 대한 작업 로그 검색**</span><span class="sxs-lookup"><span data-stu-id="caf9d-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-to-get-the-available-locations-for-all-resource-types"></a><span data-ttu-id="caf9d-176">azure location: 모든 리소스 유형에 사용 가능한 위치를 가져오는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-176">azure location: Commands to get the available locations for all resource types</span></span>
<span data-ttu-id="caf9d-177">**사용 가능한 위치 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-177">**List the available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-to-manage-network-resources"></a><span data-ttu-id="caf9d-178">azure network: 네트워크 리소스를 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-178">azure network: Commands to manage network resources</span></span>
<span data-ttu-id="caf9d-179">**가상 네트워크를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-179">**Commands to manage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="caf9d-180">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-180">Creates a virtual network.</span></span> <span data-ttu-id="caf9d-181">다음 예제에서는 미국 서부 지역의 myresourcegroup 리소스 그룹에 대한 newvnet이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-181">In the following example we create a virtual network named newvnet for resource group myresourcegroup in the West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="caf9d-182">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      the name of the resource group
     -n, --name <name>                          the name of the virtual network
     -l, --location <location>                  the location
     -a, --address-prefixes <address-prefixes>  the comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            the comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          the tags set on this virtual network.
      Can be multiple. In the format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          the subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="caf9d-183">리소스 그룹 내에서 가상 네트워크 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="caf9d-184">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      the name of the resource group
       -n, --name <name>                          the name of the virtual network
       -a, --address-prefixes <address-prefixes>  the comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended to the current list of address prefixes.
        The address prefixes in this list should not overlap between them.
        The address prefixes in this list should not overlap with existing address prefixes in the vnet.

       -d, --dns-servers [dns-servers]            the comma separated list of DNS servers IP addresses.
        This list will be appended to the current list of DNS server IP addresses.

       -t, --tags <tags>                          the tags set on this virtual network.
        Can be multiple. In the format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended to the current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          the subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="caf9d-185">리소스 그룹의 모든 가상 네트워크를 나열하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-185">The command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="caf9d-186">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  the name of the resource group
      -s, --subscription <subscription>      the subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="caf9d-187">리소스 그룹의 가상 네트워크 속성을 보여주는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-187">The command shows the virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="caf9d-188">가상 네트워크를 제거하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-188">The command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="caf9d-189">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -n, --name <name>                      the name of the virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      the subscription identifier


<span data-ttu-id="caf9d-190">**가상 네트워크 서브넷을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-190">**Commands to manage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="caf9d-191">기존 가상 네트워크에 다른 서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-191">Adds another subnet to an existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up the subnet "subnet"
    + Creating subnet "subnet"
    + Looking up the subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="caf9d-192">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            the name of the resource group
     -e, --vnet-name <vnet-name>                                      the name of the virtual network
     -n, --name <name>                                                the name of the subnet
     -a, --address-prefix <address-prefix>                            the address prefix
     -w, --network-security-group-id <network-security-group-id>      the network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  the network security group name
     -s, --subscription <subscription>                                the subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="caf9d-193">리소스 그룹 내 특정 가상 네트워크 서브넷을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up the subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="caf9d-194">리소스 그룹 내 특정 가상 네트워크에 대한 모든 가상 네트워크 서브넷을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-194">Lists all the virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up the subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="caf9d-195">가상 네트워크 서브넷 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="caf9d-196">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -e, --vnet-name <vnet-name>            the name of the virtual network
    -n, --name <name>                      the name of the subnet
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="caf9d-197">기존 가상 네트워크에서 서브넷을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up the subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="caf9d-198">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -e, --vnet-name <vnet-name>            the name of the virtual network
     -n, --name <name>                      the subnet name
     -s, --subscription <subscription>      the subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="caf9d-199">**부하 분산 장치를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-199">**Commands to manage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="caf9d-200">부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up the load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="caf9d-201">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the load balancer
    -l, --location <location>              the location
    -t, --tags <tags>                      the list of tags.
     Can be multiple. In the format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="caf9d-202">리소스 그룹 내 부하 분산 장치 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting the load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="caf9d-203">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="caf9d-204">리소스 그룹 내 특정 부하 분산 장치의 부하 분산 장치 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="caf9d-205">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="caf9d-206">부하 분산 장치 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up the load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="caf9d-207">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -n, --name <name>                      the name of the load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="caf9d-208">**부하 분산 장치의 검색을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-208">**Commands to manage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="caf9d-209">부하 분산 장치의 상태 확인을 위해 검색 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-209">Create the probe configuration for health status in the load balancer.</span></span> <span data-ttu-id="caf9d-210">이 명령을 실행하려면 부하 분산 장치에 프런트엔드 IP 리소스가 필요합니다(부하 분산 장치에 IP 주소를 할당하려면 "azure network frontend-ip" 명령 확인).</span><span class="sxs-lookup"><span data-stu-id="caf9d-210">Keep in mind to run this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" to assign an ip address to load balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="caf9d-211">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the probe
    -p, --protocol <protocol>              the probe protocol
    -o, --port <port>                      the probe port
    -f, --path <path>                      the probe path
    -i, --interval <interval>              the probe interval in seconds
    -c, --count <count>                    the number of probes
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="caf9d-212">기존 부하 분산 장치 검색을 새 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="caf9d-213">매개 변수 옵션</span><span class="sxs-lookup"><span data-stu-id="caf9d-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the probe
    -e, --new-probe-name <new-probe-name>  the new name of the probe
    -p, --protocol <protocol>              the new value for probe protocol
    -o, --port <port>                      the new value for probe port
    -f, --path <path>                      the new value for probe path
    -i, --interval <interval>              the new value for probe interval in seconds
    -c, --count <count>                    the new value for number of probes
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="caf9d-214">부하 분산 장치 집합의 검색 속성을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-214">List the probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up the load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="caf9d-215">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="caf9d-216">부하 분산 장치에 대해 생성된 검색을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-216">Removes the probe created for the load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up the load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="caf9d-217">**부하 분산 장치의 프런트엔드 IP 구성을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-217">**Commands to manage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="caf9d-218">기존 부하 분산 장치 집합에 대한 프런트엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-218">Creates a frontend IP configuration to an existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up the load balancer "mylb"
    + Looking up the subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="caf9d-219">프런트 엔드 IP의 기존 구성을 업데이트합니다. 아래 명령은 myfrontendip라는 기존 부하 분산 장치 프런트 엔드 IP에 mypubip5라는 공용 IP를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-219">Updates an existing configuration of a frontend IP.The command below adds a public IP called mypubip5 to an existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up the load balancer "mylb"
    + Looking up the public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="caf9d-220">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              the name of the resource group
    -l, --lb-name <lb-name>                                            the name of the load balancer
    -n, --name <name>                                                  the name of the frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      the private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  the private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  the public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              the public ip name.
    This public ip must exist in the same resource group as the lb.
    Please use public-ip-id if that is not the case.
    -b, --subnet-id <subnet-id>                                        the subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    the subnet name
    -m, --vnet-name <vnet-name>                                        the virtual network name.
    This virtual network must exist in the same resource group as the lb.
    Please use subnet-id if that is not the case.
    -s, --subscription <subscription>                                  the subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="caf9d-221">부하 분산 장치에 대해 구성된 모든 프런트엔드 IP 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-221">Lists all the frontend IP resources configured for the load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up the load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="caf9d-222">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="caf9d-223">부하 분산 장치에 연결된 프런트엔드 IP 개체를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-223">Deletes the frontend IP object associated to load balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up the load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="caf9d-224">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="caf9d-225">**부하 분산 장치의 백엔드 주소 풀을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-225">**Commands to manage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="caf9d-226">부하 분산 장치의 백엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="caf9d-227">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the backend address pool
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="caf9d-228">특정 리소스 그룹에 대한 백엔드 IP 주소 풀 범위를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up the load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="caf9d-229">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -l, --lb-name <lb-name>                the name of the load balancer
     -s, --subscription <subscription>      the subscription identifier

<BR>
    <span data-ttu-id="caf9d-230">네트워크 lb 주소 풀이 삭제 [옵션] < 리소스 그룹 >< lb-이름 ><name></span><span class="sxs-lookup"><span data-stu-id="caf9d-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="caf9d-231">부하 분산 장치에서 백엔드 IP 풀 범위 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-231">Removes the backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up the load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="caf9d-232">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="caf9d-233">**부하 분산 장치 규칙을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-233">**Commands to manage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="caf9d-234">부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-234">Create load balancer rules.</span></span>

<span data-ttu-id="caf9d-235">부하 분산 장치의 프런트 엔드 끝점 및 들어오는 네트워크 트래픽을 수신하는 백 엔드 주소 풀 범위를 구성하는 부하 분산 장치 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-235">You can create a load balancer rule configuring the frontend endpoint for the load balancer and the backend address pool range to receive the incoming network traffic.</span></span> <span data-ttu-id="caf9d-236">설정에는 프런트엔드 IP 끝점의 포트 및 백엔드 주소 풀 범위의 포트도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-236">Settings also include the ports for frontend IP endpoint and ports for the backend address pool range.</span></span>

<span data-ttu-id="caf9d-237">다음 예제에서는 백 엔드 주소 풀 범위에서 부하 분산 장치 규칙, 80 TCP 포트를 수신 대기하는 프런트 엔드 끝점 및 포트 8080으로 보내는 부하 분산 네트워크 트래픽을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-237">The following example shows how to create a load balancer rule,  the frontend endpoint listening to port 80 TCP and load balancing network traffic sending to port 8080 for the backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="caf9d-238">특정 리소스 그룹의 기존 부하 분산 장치 규칙 집합을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="caf9d-239">다음 예제에서는 규칙 이름을 mylbrule에서 mynewlbrule로 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-239">In the following example, we changed the rule name from mylbrule to mynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="caf9d-240">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              the name of the resource group
    -l, --lb-name <lb-name>                            the name of the load balancer
    -n, --name <name>                                  the name of the rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          the rule protocol
    -f, --frontend-port <frontend-port>                the frontend port
    -b, --backend-port <backend-port>                  the backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  the idle timeout in minutes
    -a, --probe-name [probe-name]                      the name of the probe defined in the same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          the name of the frontend ip configuration in the same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of the backend address pool defined in the same load balancer
    -s, --subscription <subscription>                  the subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="caf9d-241">특정 리소스 그룹의 부하 분산 장치에 대해 구성된 모든 부하 분산 장치 규칙을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up the load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="caf9d-242">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="caf9d-243">부하 분산 장치 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up the load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="caf9d-244">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="caf9d-245">**부하 분산 장치 인바운드 NAT 규칙을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-245">**Commands to manage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="caf9d-246">부하 분산 장치의 인바운드 NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="caf9d-247">다음 예제에서는 부하 분산 장치가 네트워크 트래픽을 전송하는 데 사용하는 인바운드 수신 대기 포트 및 아웃바운드 포트로 프런트 엔드 IP("azure network frontend-ip" 명령을 사용하여 이전에 정의됨)에서 NAT 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-247">In the following example  we created a NAT rule from frontend IP (which was previously defined using the "azure network frontend-ip" command) with an inbound listening port and outbound port that the load balancer uses to send the network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="caf9d-248">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          the name of the resource group
    -l, --lb-name <lb-name>                        the name of the load balancer
    -n, --name <name>                              the name of the inbound NAT rule
    -p, --protocol <protocol>                      the rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            the frontend port [0-65535]
    -b, --backend-port <backend-port>              the backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                the name of the frontend ip configuration
    -m, --vm-id <vm-id>                            the VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        the VM name.This VM must exist in the same resource group as the lb.
    Please use vm-id if that is not the case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              the subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="caf9d-249">기존 인바운드 NAT 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="caf9d-250">다음 예제에서는 인바운드 수신 대기 포트를 80에서 81로 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-250">In the following example, we changed the inbound listening port from 80 to 81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="caf9d-251">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          the name of the resource group
    -l, --lb-name <lb-name>                        the name of the load balancer
    -n, --name <name>                              the name of the inbound NAT rule
    -p, --protocol <protocol>                      the rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            the frontend port [0-65535]
    -b, --backend-port <backend-port>              the backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                the name of the frontend ip configuration
    -m, --vm-id [vm-id]                            the VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        the VM name.
    This virtual machine must exist in the same resource group as the lb.
    Please use vm-id if that is not the case
    -s, --subscription <subscription>              the subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="caf9d-252">부하 분산 장치의 모든 인바운드 NAT 규칙을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up the load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="caf9d-253">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="caf9d-254">특정 리소스 그룹에서 부하 분산 장치에 대한 NAT 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-254">Deletes NAT rule for the load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up the load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="caf9d-255">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="caf9d-256">**공용 IP 주소를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-256">**Commands to manage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="caf9d-257">공용 IP 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-257">Creates a public ip resource.</span></span> <span data-ttu-id="caf9d-258">공용 IP 리소스를 만들고 도메인 이름에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-258">You will create the public ip resource and associate to a domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up the public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up the public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="caf9d-259">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        the name of the resource group
    -n, --name <name>                            the name of the public ip
    -l, --location <location>                    the location
    -d, --domain-name-label <domain-name-label>  the domain name label.
    This set DNS to <domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  the allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              the idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            the reverse fqdn
    -t, --tags <tags>                            the list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            the subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="caf9d-260">기존 공용 IP 리소스의 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-260">Updates the properties of an existing public ip resource.</span></span> <span data-ttu-id="caf9d-261">다음 예제에서는 공용 IP 주소를 Dynamic에서 Static으로 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-261">In the following example we changed the public IP address from Dynamic to Static.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up the public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up the public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="caf9d-262">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        the name of the resource group
    -n, --name <name>                            the name of the public ip
    -d, --domain-name-label [domain-name-label]  the domain name label.
    This set DNS to <domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  the allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              the idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            the reverse fqdn
    -t, --tags <tags>                            the list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            the subscription identifier

<br>
    <span data-ttu-id="caf9d-263">network public-ip list [options] &lt;resource-group&gt; 리소스 그룹 내 모든 공용 IP 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting the public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="caf9d-264">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -s, --subscription <subscription>      the subscription identifier
<BR>
    <span data-ttu-id="caf9d-265">네트워크 공개 ip [옵션] < 리소스 그룹 > 표시<name></span><span class="sxs-lookup"><span data-stu-id="caf9d-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="caf9d-266">리소스 그룹 내 공용 IP 리소스에 대한 공용 IP 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up the public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="caf9d-267">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the public IP
    -s, --subscription <subscription>      the subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="caf9d-268">공용 IP 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up the public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="caf9d-269">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier


<span data-ttu-id="caf9d-270">**네트워크 인터페이스를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-270">**Commands to manage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="caf9d-271">부하 분산 장치에 사용하거나 가상 컴퓨터에 연결할 수 있는 NIC(네트워크 인터페이스)라고 하는 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate to a Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up the network interface "testnic1"
    + Looking up the subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up the network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="caf9d-272">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="caf9d-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            the name of the resource group
    -n, --name <name>                                                the name of the network interface
    -l, --location <location>                                        the location
    -w, --network-security-group-id <network-security-group-id>      the network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  the network security group name.
    This network security group must exist in the same resource group as the nic.
    Please use network-security-group-id if that is not the case.
    -i, --public-ip-id <public-ip-id>                                the public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            the public IP name.
    This public ip must exist in the same resource group as the nic.
    Please use public-ip-id if that is not the case.
    -a, --private-ip-address <private-ip-address>                    the private IP address
    -u, --subnet-id <subnet-id>                                      the subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  the subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        the vnet name under which subnet-name exists
    -t, --tags <tags>                                                the comma seperated list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                the subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="caf9d-273">**네트워크 보안 그룹을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-273">**Commands to manage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="caf9d-274">**네트워크 보안 그룹 규칙을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-274">**Commands to manage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="caf9d-275">**트래픽 관리자 프로필을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-275">**Commands to manage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="caf9d-276">**트래픽 관리자 끝점을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-276">**Commands to manage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="caf9d-277">**가상 네트워크 게이트웨이를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-277">**Commands to manage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-to-manage-resource-provider-registrations"></a><span data-ttu-id="caf9d-278">azure provider: 리소스 공급자 등록을 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-278">azure provider: Commands to manage resource provider registrations</span></span>
<span data-ttu-id="caf9d-279">**Resource Manager에 현재 등록된 공급자 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="caf9d-280">**요청한 공급자 네임스페이스에 대한 자세한 정보 표시**</span><span class="sxs-lookup"><span data-stu-id="caf9d-280">**Show details about the requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="caf9d-281">**구독에 공급자 등록**</span><span class="sxs-lookup"><span data-stu-id="caf9d-281">**Register provider with the subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="caf9d-282">**구독에 공급자 등록 취소**</span><span class="sxs-lookup"><span data-stu-id="caf9d-282">**Unregister provider with the subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-to-manage-your-resources"></a><span data-ttu-id="caf9d-283">azure group: 리소스를 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-283">azure resource: Commands to manage your resources</span></span>
<span data-ttu-id="caf9d-284">**리소스 그룹에 리소스 만들기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="caf9d-285">**템플릿 또는 매개 변수 없이 리소스 그룹의 리소스 업데이트**</span><span class="sxs-lookup"><span data-stu-id="caf9d-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="caf9d-286">**리소스 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-286">**Lists the resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="caf9d-287">**리소스 그룹 또는 구독 내에서 한 리소스 가져오기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="caf9d-288">**리소스 그룹의 리소스 삭제**</span><span class="sxs-lookup"><span data-stu-id="caf9d-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-to-manage-your-azure-roles"></a><span data-ttu-id="caf9d-289">azure role: Azure 역할을 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-289">azure role: Commands to manage your Azure roles</span></span>
<span data-ttu-id="caf9d-290">**모든 사용 가능한 역할 정의 가져오기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="caf9d-291">**사용 가능한 역할 정의 가져오기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="caf9d-292">**역할 할당을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-292">**Commands to manage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-to-manage-your-storage-objects"></a><span data-ttu-id="caf9d-293">azure storage: 저장소 개체를 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-293">azure storage: Commands to manage your Storage objects</span></span>
<span data-ttu-id="caf9d-294">**저장소 계정을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-294">**Commands to manage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="caf9d-295">**저장소 계정 키를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-295">**Commands to manage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="caf9d-296">**저장소 연결 문자열을 표시하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-296">**Commands to show your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="caf9d-297">**저장소 컨테이너를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-297">**Commands to manage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="caf9d-298">**저장소 컨테이너의 공유 액세스 서명을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-298">**Commands to manage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="caf9d-299">**저장소 컨테이너의 저장된 액세스 정책을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-299">**Commands to manage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="caf9d-300">**저장소 BLOB를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-300">**Commands to manage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="caf9d-301">**BLOB 복사 작업을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-301">**Commands to manage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="caf9d-302">**저장소 BLOB의 공유 액세스 서명을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-302">**Commands to manage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="caf9d-303">**저장소 파일 공유를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-303">**Commands to manage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="caf9d-304">**저장소 파일을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-304">**Commands to manage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="caf9d-305">**저장소 파일 디렉터리를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-305">**Commands to manage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="caf9d-306">**저장소 대기열을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-306">**Commands to manage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="caf9d-307">**저장소 대기열의 공유 액세스 서명을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-307">**Commands to manage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="caf9d-308">**저장소 대기열의 공유 액세스 정책을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-308">**Commands to manage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="caf9d-309">**저장소 로깅 속성을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-309">**Commands to manage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="caf9d-310">**저장소 메트릭 속성을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-310">**Commands to manage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="caf9d-311">**저장소 테이블을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-311">**Commands to manage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="caf9d-312">**저장소 테이블의 공유 액세스 서명을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-312">**Commands to manage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="caf9d-313">**저장소 테이블의 공유 액세스 정책을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-313">**Commands to manage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-to-manage-your-resource-manager-tag"></a><span data-ttu-id="caf9d-314">azure tag: 리소스 관리자 태그를 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-314">azure tag: Commands to manage your resource manager tag</span></span>
<span data-ttu-id="caf9d-315">**태그 추가**</span><span class="sxs-lookup"><span data-stu-id="caf9d-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="caf9d-316">**전체 태그 또는 태그 값 제거**</span><span class="sxs-lookup"><span data-stu-id="caf9d-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="caf9d-317">**태그 정보 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-317">**Lists the tag information**</span></span>

    tag list [options]

<span data-ttu-id="caf9d-318">**태그 가져오기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-to-manage-your-azure-virtual-machines"></a><span data-ttu-id="caf9d-319">azure vm: Azure 가상 컴퓨터를 관리하는 명령</span><span class="sxs-lookup"><span data-stu-id="caf9d-319">azure vm: Commands to manage your Azure Virtual Machines</span></span>
<span data-ttu-id="caf9d-320">**VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="caf9d-321">**기본 리소스를 사용하여 VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="caf9d-322">CLI 0.10 버전부터 일부 인기 있는 마켓플레이스 이미지에 대한 `image-urn`으로 "UbuntuLTS" 또는 "Win2012R2Datacenter"와 같은 짧은 별칭을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as the `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="caf9d-323">옵션으로 `azure help vm quick-create`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="caf9d-324">또한 0.10 버전부터 `azure vm quick-create` 는 선택한 영역에서 사용 가능한 경우 기본적으로 프리미엄 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="caf9d-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in the selected region.</span></span>
> 
> 

<span data-ttu-id="caf9d-325">**계정 내에서 가상 컴퓨터 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-325">**List the virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="caf9d-326">**리소스 그룹 내 한 가상 컴퓨터 가져오기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="caf9d-327">**리소스 그룹 내 한 가상 컴퓨터 삭제**</span><span class="sxs-lookup"><span data-stu-id="caf9d-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="caf9d-328">**리소스 그룹 내 한 가상 컴퓨터 종료**</span><span class="sxs-lookup"><span data-stu-id="caf9d-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="caf9d-329">**리소스 그룹 내 한 가상 컴퓨터 다시 시작**</span><span class="sxs-lookup"><span data-stu-id="caf9d-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="caf9d-330">**리소스 그룹 내 한 가상 컴퓨터 시작**</span><span class="sxs-lookup"><span data-stu-id="caf9d-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="caf9d-331">**리소스 그룹 내 한 가상 컴퓨터를 종료하고 컴퓨팅 리소스 해제**</span><span class="sxs-lookup"><span data-stu-id="caf9d-331">**Shutdown one virtual machine within a resource group and releases the compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="caf9d-332">**사용 가능한 가상 컴퓨터 크기 나열**</span><span class="sxs-lookup"><span data-stu-id="caf9d-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="caf9d-333">**VM을 OS 이미지 또는 VM 이미지로 캡처**</span><span class="sxs-lookup"><span data-stu-id="caf9d-333">**Capture the VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="caf9d-334">**VM의 상태를 일반화됨으로 설정**</span><span class="sxs-lookup"><span data-stu-id="caf9d-334">**Set the state of the VM to Generalized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="caf9d-335">**VM의 인스턴스 보기 가져오기**</span><span class="sxs-lookup"><span data-stu-id="caf9d-335">**Get instance view of the VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="caf9d-336">**가상 컴퓨터에서 원격 데스크톱 액세스 또는 SSH 설정을 다시 설정하고 관리자 또는 sudo 권한이 있는 계정의 암호를 다시 설정할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="caf9d-336">**Enable you to reset Remote Desktop Access or SSH settings on a Virtual Machine and to reset the password for the account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="caf9d-337">**새 데이터로 VM 업데이트**</span><span class="sxs-lookup"><span data-stu-id="caf9d-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="caf9d-338">**가상 컴퓨터 데이터 디스크를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-338">**Commands to manage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="caf9d-339">**VM 리소스 확장을 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-339">**Commands to manage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="caf9d-340">**도커 가상 컴퓨터를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-340">**Commands to manage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="caf9d-341">**VM 이미지를 관리하는 명령**</span><span class="sxs-lookup"><span data-stu-id="caf9d-341">**Commands to manage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
