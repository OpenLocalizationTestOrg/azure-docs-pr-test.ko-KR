---
title: "리소스 관리자 모드에서 aaaAzure CLI 명령을 | Microsoft Docs"
description: "Azure 명령줄 인터페이스 (CLI) 명령을 hello 리소스 관리자 배포 모델의 toomanage 리소스"
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
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="523fb-103">리소스 관리자 모드에서 Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="523fb-104">이 문서에서는 구문 및 옵션 일반적으로 Azure CLI (명령줄 인터페이스) 명령에 대 한 toocreate를 사용 하 고 hello Azure 리소스 관리자 배포 모델에서 Azure 리소스 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="523fb-105">Hello CLI 리소스 관리자 (arm) 모드에서 실행 하 여 이러한 명령에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="523fb-106">전체 참조는 아니며 CLI 버전에서 약간 다른 명령 또는 매개 변수를 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="523fb-107">Azure 리소스 및 리소스 그룹에 대한 일반적인 개요는 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="523fb-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="523fb-108">이 문서에서는 리소스 관리자 모드 명령 hello Azure CLI Azure CLI 1.0 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="523fb-109">리소스 관리자 모델 hello toowork를 시도해 볼 수 있습니다 hello [Azure CLI 2.0](/cli/azure/install-az-cli2), 다음 세대 다중 플랫폼 CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="523fb-110">Hello에 대 한 자세한 내용을 알아보려면 [이전 및 새 Azure Cli](/cli/azure/old-and-new-clis)합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="523fb-111">먼저 tooget 시작 [hello Azure CLI 설치](../cli-install-nodejs.md) 및 [tooyour Azure 구독 연결](../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="523fb-112">현재 명령 구문 및 옵션을 리소스 관리자 모드에서 hello 명령줄에서 입력 `azure help` 또는 특정 명령에 대 한 도움말 toodisplay `azure help [command]`합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="523fb-113">오류도 찾을 CLI 예제 hello 설명서 생성 및 특정 Azure 서비스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="523fb-114">선택적 매개 변수는 대괄호 안에 표시(예: `[parameter]`)됩니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="523fb-115">모든 다른 매개 변수는 필수 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-115">All other parameters are required.</span></span>

<span data-ttu-id="523fb-116">에 추가 toocommand 특정 선택적 매개 변수 설명 여기에서 toodisplay 사용된 될 수 있는 세 가지 선택적 매개 변수 요청 옵션 및 상태 코드와 같은 출력 된 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="523fb-117">hello `-v` 자세한 정보 출력 및 hello 매개 변수를 제공 `-vv` 더 자세한 자세한 정보를 출력 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="523fb-118">hello `--json` 옵션 원시 json 형식으로 hello 결과 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="523fb-119">Hello 리소스 관리자 모드 설정</span><span class="sxs-lookup"><span data-stu-id="523fb-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="523fb-120">다음 명령 tooenable Azure CLI 리소스 관리자 모드 명령 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="523fb-121">hello CLI Azure Resource Manager 모드와 Azure 서비스 관리 모드는 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="523fb-122">Hello에서 하나의 모드로 생성 된 리소스를 관리할 수 없습니다, 즉 다른 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="523fb-123">Azure account: 계정 정보 관리</span><span class="sxs-lookup"><span data-stu-id="523fb-123">azure account: Manage your account information</span></span>
<span data-ttu-id="523fb-124">Azure 구독 정보는 hello 도구 tooconnect tooyour 계정에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="523fb-125">**가져온 hello 구독 나열**</span><span class="sxs-lookup"><span data-stu-id="523fb-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="523fb-126">**구독에 대한 자세한 정보 표시**</span><span class="sxs-lookup"><span data-stu-id="523fb-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="523fb-127">**현재 구독 hello 설정**</span><span class="sxs-lookup"><span data-stu-id="523fb-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="523fb-128">**구독 또는 환경, 제거 하거나 저장 하는 hello 계정 및 환경 정보를 모두 지우기**</span><span class="sxs-lookup"><span data-stu-id="523fb-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="523fb-129">**사용자 계정 환경 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="523fb-130">azure ad: toodisplay Active Directory 개체 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="523fb-131">**명령 toodisplay active directory 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="523fb-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="523fb-132">**명령 toodisplay active directory 그룹**</span><span class="sxs-lookup"><span data-stu-id="523fb-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="523fb-133">**명령 tooprovide active directory 하위 그룹 또는 멤버 정보**</span><span class="sxs-lookup"><span data-stu-id="523fb-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="523fb-134">**명령 toodisplay active directory 서비스 사용자**</span><span class="sxs-lookup"><span data-stu-id="523fb-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="523fb-135">**명령 toodisplay active directory 사용자**</span><span class="sxs-lookup"><span data-stu-id="523fb-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="523fb-136">azure availset: 명령을 toomanage 가능 여부 설정</span><span class="sxs-lookup"><span data-stu-id="523fb-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="523fb-137">**리소스 그룹 내 가용성 집합 만들기**</span><span class="sxs-lookup"><span data-stu-id="523fb-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="523fb-138">**목록 hello 리소스 그룹 내의 가용성 집합**</span><span class="sxs-lookup"><span data-stu-id="523fb-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="523fb-139">**리소스 그룹 내 한 가용성 집합 가져오기**</span><span class="sxs-lookup"><span data-stu-id="523fb-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="523fb-140">**리소스 그룹 내 한 가용성 집합 삭제**</span><span class="sxs-lookup"><span data-stu-id="523fb-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="523fb-141">azure 구성: toomanage 로컬 설정 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="523fb-142">**Azure CLI 구성 설정 나열**</span><span class="sxs-lookup"><span data-stu-id="523fb-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="523fb-143">**구성 설정 삭제**</span><span class="sxs-lookup"><span data-stu-id="523fb-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="523fb-144">**구성 설정 업데이트**</span><span class="sxs-lookup"><span data-stu-id="523fb-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="523fb-145">**집합 작업 모드 tooeither Azure CLI hello `arm` 또는`asm`**</span><span class="sxs-lookup"><span data-stu-id="523fb-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="523fb-146">azure 기능: toomanage 계정 기능 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="523fb-147">**구독에 대해 사용할 수 있는 모든 기능 나열**</span><span class="sxs-lookup"><span data-stu-id="523fb-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="523fb-148">**기능 표시**</span><span class="sxs-lookup"><span data-stu-id="523fb-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="523fb-149">**리소스 공급자의 미리 본 기능 등록**</span><span class="sxs-lookup"><span data-stu-id="523fb-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="523fb-150">으로 azure 그룹: toomanage 리소스 그룹 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="523fb-151">**리소스 그룹 만들기**</span><span class="sxs-lookup"><span data-stu-id="523fb-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="523fb-152">**태그 tooa 리소스 그룹 설정**</span><span class="sxs-lookup"><span data-stu-id="523fb-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="523fb-153">**리소스 그룹 삭제**</span><span class="sxs-lookup"><span data-stu-id="523fb-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="523fb-154">**구독에 대 한 hello 리소스 그룹 나열**</span><span class="sxs-lookup"><span data-stu-id="523fb-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="523fb-155">**구독에 대한 리소스 그룹 표시**</span><span class="sxs-lookup"><span data-stu-id="523fb-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="523fb-156">**명령 toomanage 리소스 그룹 로그**</span><span class="sxs-lookup"><span data-stu-id="523fb-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="523fb-157">**Toomanage 리소스 그룹의 배포 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="523fb-158">**사용자 로컬 또는 갤러리 리소스 그룹 템플릿 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="523fb-159">azure hdinsight: 명령을 toomanage HDInsight 클러스터</span><span class="sxs-lookup"><span data-stu-id="523fb-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="523fb-160">**Toocreate 명령 또는 tooa 클러스터 구성 파일 추가**</span><span class="sxs-lookup"><span data-stu-id="523fb-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="523fb-161">예: 스크립트 작업 toorun 클러스터를 만들 때 포함 된 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="523fb-162">**명령 toocreate 리소스 그룹의 클러스터**</span><span class="sxs-lookup"><span data-stu-id="523fb-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="523fb-163">예: Linux 클러스터에 Storm을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="523fb-164">예: 스크립트 동작으로 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="523fb-165">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="523fb-166">**명령 toodelete 클러스터**</span><span class="sxs-lookup"><span data-stu-id="523fb-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="523fb-167">**명령 tooshow 클러스터 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="523fb-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="523fb-168">**모든 명령 toolist 클러스터를 (특정 리소스 그룹을 제공 하는 경우)**</span><span class="sxs-lookup"><span data-stu-id="523fb-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="523fb-169">**명령 tooresize 클러스터**</span><span class="sxs-lookup"><span data-stu-id="523fb-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="523fb-170">**클러스터에 대 한 HTTP tooenable 액세스 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="523fb-171">**클러스터에 대 한 HTTP toodisable 액세스 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="523fb-172">**클러스터에 대 한 명령 tooenable RDP 액세스**</span><span class="sxs-lookup"><span data-stu-id="523fb-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="523fb-173">**클러스터에 대 한 HTTP toodisable 액세스 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="523fb-174">azure insights: 명령 (예: 이벤트, 경고 규칙, 자동 크기 조정 설정, 메트릭) toomonitoring Insights 관련</span><span class="sxs-lookup"><span data-stu-id="523fb-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="523fb-175">**구독, 상관 관계 ID, 리소스 그룹, 리소스 또는 리소스 공급자에 대한 작업 로그 검색**</span><span class="sxs-lookup"><span data-stu-id="523fb-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="523fb-176">azure 위치: 모든 리소스 종류에 대 한 tooget hello 사용 가능한 위치 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="523fb-177">**목록 hello 사용 가능한 위치**</span><span class="sxs-lookup"><span data-stu-id="523fb-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="523fb-178">azure 네트워크: 명령을 toomanage 네트워크 리소스</span><span class="sxs-lookup"><span data-stu-id="523fb-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="523fb-179">**명령 toomanage 가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="523fb-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="523fb-180">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-180">Creates a virtual network.</span></span> <span data-ttu-id="523fb-181">Hello 다음 예제에서는 가상 네트워크를 만듭니다 newvnet hello 미국 서 부 지역에서 리소스 그룹 myresourcegroup에 대 한 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

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


<span data-ttu-id="523fb-182">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="523fb-183">리소스 그룹 내에서 가상 네트워크 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-183">Updates a virtual network configuration within a resource group.</span></span>

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

<span data-ttu-id="523fb-184">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="523fb-185">hello 명령은 리소스 그룹의 모든 가상 네트워크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-185">hello command lists all virtual networks in a resource group.</span></span>

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

<span data-ttu-id="523fb-186">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="523fb-187">hello 명령 리소스 그룹의 hello 가상 네트워크 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-187">hello command shows hello virtual network properties in a resource group.</span></span>

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
<span data-ttu-id="523fb-188">hello 명령은 가상 네트워크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="523fb-189">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="523fb-190">**명령 toomanage 가상 네트워크 서브넷**</span><span class="sxs-lookup"><span data-stu-id="523fb-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="523fb-191">다른 서브넷 tooan 기존 가상 네트워크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="523fb-192">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="523fb-193">리소스 그룹 내 특정 가상 네트워크 서브넷을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="523fb-194">리소스 그룹 내에서 특정 가상 네트워크에 대 한 모든 hello 가상 네트워크 서브넷을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="523fb-195">가상 네트워크 서브넷 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="523fb-196">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="523fb-197">기존 가상 네트워크에서 서브넷을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="523fb-198">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="523fb-199">**명령 toomanage 부하 분산 장치**</span><span class="sxs-lookup"><span data-stu-id="523fb-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="523fb-200">부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="523fb-201">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="523fb-202">리소스 그룹 내 부하 분산 장치 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="523fb-203">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="523fb-204">리소스 그룹 내 특정 부하 분산 장치의 부하 분산 장치 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="523fb-205">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="523fb-206">부하 분산 장치 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="523fb-207">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="523fb-208">**부하 분산 장치 프로브 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="523fb-209">Hello 부하 분산 장치에서 상태에 대 한 hello 프로브 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="523fb-210">이 명령은 주의 toorun에 보관, 부하 분산 장치 프런트 엔드 ip 리소스가 (체크아웃 명령 "azure 네트워크 프런트 엔드-ip" tooassign ip 주소 tooload 분산 장치) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="523fb-211">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="523fb-212">기존 부하 분산 장치 검색을 새 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="523fb-213">매개 변수 옵션</span><span class="sxs-lookup"><span data-stu-id="523fb-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="523fb-214">부하 분산 장치 집합에 대 한 hello 프로브 속성을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="523fb-215">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="523fb-216">Hello 부하 분산 장치에 대해 생성 하는 hello 프로브를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="523fb-217">**명령 toomanage 프런트 엔드 ip 구성의 부하 분산 장치**</span><span class="sxs-lookup"><span data-stu-id="523fb-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="523fb-218">프런트 엔드 IP 구성 tooan를 기존 부하 분산 장치 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="523fb-219">업데이트 아래 IP.hello 명령 프론트 엔드의 기존 구성 mypubip5 tooan 기존 부하 분산 장치 프런트 엔드 IP myfrontendip 라는 라는 공용 IP를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="523fb-220">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="523fb-221">Hello 부하 분산 장치에 대해 구성 된 모든 hello 프런트 엔드 IP 리소스를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="523fb-222">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="523fb-223">Hello 프런트 엔드 IP 연결 된 개체 tooload 분산 장치를 삭제</span><span class="sxs-lookup"><span data-stu-id="523fb-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="523fb-224">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="523fb-225">**부하 분산 장치 백 엔드 주소 풀 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="523fb-226">부하 분산 장치의 백엔드 주소 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="523fb-227">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="523fb-228">특정 리소스 그룹에 대한 백엔드 IP 주소 풀 범위를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="523fb-229">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="523fb-230">네트워크 lb 주소 풀이 삭제 [옵션] < 리소스 그룹 >< lb-이름 ><name></span><span class="sxs-lookup"><span data-stu-id="523fb-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="523fb-231">부하 분산 장치에서 hello 백 엔드 IP 풀 범위 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="523fb-232">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="523fb-233">**Toomanage 부하 분산 장치 규칙 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="523fb-234">부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-234">Create load balancer rules.</span></span>

<span data-ttu-id="523fb-235">Hello 부하 분산 장치 및 hello 백 엔드 주소 풀 범위 tooreceive hello 들어오는 네트워크 트래픽을 hello 프런트 엔드 끝점을 구성 하는 부하 분산 장치 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="523fb-236">설정은 프런트 엔드 IP 끝점에 대 한 hello 포트와 백 엔드 주소 풀 범위 hello에 대 한 포트에도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="523fb-237">hello 다음 예제에서는 어떻게 toocreate 부하 분산 장치 규칙을 tooport 80 수신 대기 하는 hello 프런트 엔드 끝점이 TCP 및 부하 분산에 대 한 네트워크 트래픽 보내기 tooport 8080 hello 백 엔드 주소 풀 범위에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="523fb-238">특정 리소스 그룹의 기존 부하 분산 장치 규칙 집합을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="523fb-239">다음 예제는 hello에서 mylbrule toomynewlbrule에서 hello 규칙 이름을 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="523fb-240">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="523fb-241">특정 리소스 그룹의 부하 분산 장치에 대해 구성된 모든 부하 분산 장치 규칙을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="523fb-242">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="523fb-243">부하 분산 장치 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="523fb-244">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="523fb-245">**명령 toomanage 부하 분산 장치 인바운드 NAT 규칙**</span><span class="sxs-lookup"><span data-stu-id="523fb-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="523fb-246">부하 분산 장치의 인바운드 NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="523fb-247">Hello 만든 NAT 규칙 (이전에 정의 된 hello "azure 네트워크 프런트 엔드-ip" 명령을 사용 하 여)는 프런트 엔드 IP에서 수신 대기 포트를 인바운드 및 아웃 바운드 포트와 해당 hello 부하 분산 장치는 다음 예제에서는 toosend hello 네트워크 트래픽을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="523fb-248">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="523fb-249">기존 인바운드 NAT 규칙을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="523fb-250">다음 예제는 hello, hello 변경 too81 80에서 수신 대기 포트를 인바운드 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="523fb-251">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="523fb-252">부하 분산 장치의 모든 인바운드 NAT 규칙을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="523fb-253">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="523fb-254">특정 리소스 그룹의 hello 부하 분산 장치에 대 한 NAT 규칙을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="523fb-255">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="523fb-256">**명령 toomanage 공용 ip 주소**</span><span class="sxs-lookup"><span data-stu-id="523fb-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="523fb-257">공용 IP 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-257">Creates a public ip resource.</span></span> <span data-ttu-id="523fb-258">Hello 공용 ip 리소스를 만들고 tooa 도메인 이름을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
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


<span data-ttu-id="523fb-259">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="523fb-260">기존 공용 ip 리소스의 hello 속성을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="523fb-261">다음 예제는 hello에 동적 tooStatic에서 hello 공용 IP 주소를 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
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

<span data-ttu-id="523fb-262">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="523fb-263">network public-ip list [options] &lt;resource-group&gt; 리소스 그룹 내 모든 공용 IP 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="523fb-264">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="523fb-265">네트워크 공개 ip [옵션] < 리소스 그룹 > 표시<name></span><span class="sxs-lookup"><span data-stu-id="523fb-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="523fb-266">리소스 그룹 내 공용 IP 리소스에 대한 공용 IP 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
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

<span data-ttu-id="523fb-267">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="523fb-268">공용 IP 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="523fb-269">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="523fb-270">**명령 toomanage 네트워크 인터페이스**</span><span class="sxs-lookup"><span data-stu-id="523fb-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="523fb-271">Tooa 가상 컴퓨터를 연결 하거나 부하 분산 장치에 사용할 수 있는 네트워크 인터페이스 (NIC) 라고 하는 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
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

<span data-ttu-id="523fb-272">매개 변수 옵션:</span><span class="sxs-lookup"><span data-stu-id="523fb-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="523fb-273">**명령 toomanage 네트워크 보안 그룹**</span><span class="sxs-lookup"><span data-stu-id="523fb-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="523fb-274">**명령 toomanage 네트워크 보안 그룹 규칙**</span><span class="sxs-lookup"><span data-stu-id="523fb-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="523fb-275">**명령 toomanage 트래픽 관리자 프로필**</span><span class="sxs-lookup"><span data-stu-id="523fb-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="523fb-276">**명령 toomanage 트래픽 관리자 끝점**</span><span class="sxs-lookup"><span data-stu-id="523fb-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="523fb-277">**명령 toomanage 가상 네트워크 게이트웨이**</span><span class="sxs-lookup"><span data-stu-id="523fb-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="523fb-278">azure 공급자: 명령을 toomanage 리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="523fb-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="523fb-279">**Resource Manager에 현재 등록된 공급자 나열**</span><span class="sxs-lookup"><span data-stu-id="523fb-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="523fb-280">**공급자 네임 스페이스를 요청 하는 hello에 대 한 자세한 정보 표시**</span><span class="sxs-lookup"><span data-stu-id="523fb-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="523fb-281">**공급자 hello 구독에 등록**</span><span class="sxs-lookup"><span data-stu-id="523fb-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="523fb-282">**Hello 구독을 사용 하 여 공급자를 등록 취소**</span><span class="sxs-lookup"><span data-stu-id="523fb-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="523fb-283">azure 리소스: 리소스 toomanage 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="523fb-284">**리소스 그룹에 리소스 만들기**</span><span class="sxs-lookup"><span data-stu-id="523fb-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="523fb-285">**템플릿 또는 매개 변수 없이 리소스 그룹의 리소스 업데이트**</span><span class="sxs-lookup"><span data-stu-id="523fb-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="523fb-286">**Hello 리소스 목록**</span><span class="sxs-lookup"><span data-stu-id="523fb-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="523fb-287">**리소스 그룹 또는 구독 내에서 한 리소스 가져오기**</span><span class="sxs-lookup"><span data-stu-id="523fb-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="523fb-288">**리소스 그룹의 리소스 삭제**</span><span class="sxs-lookup"><span data-stu-id="523fb-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="523fb-289">azure 역할: toomanage Azure 역할 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="523fb-290">**모든 사용 가능한 역할 정의 가져오기**</span><span class="sxs-lookup"><span data-stu-id="523fb-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="523fb-291">**사용 가능한 역할 정의 가져오기**</span><span class="sxs-lookup"><span data-stu-id="523fb-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="523fb-292">**역할 할당 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="523fb-293">azure 저장소: toomanage 저장소 개체 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="523fb-294">**저장소 계정 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="523fb-295">**저장소 계정 키 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="523fb-296">**저장소 연결 문자열 tooshow 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="523fb-297">**저장소 컨테이너 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="523fb-298">**저장소 컨테이너의 명령 toomanage 공유 액세스 서명**</span><span class="sxs-lookup"><span data-stu-id="523fb-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="523fb-299">**저장 된 저장소 컨테이너의 액세스 정책을 명령 toomanage**</span><span class="sxs-lookup"><span data-stu-id="523fb-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="523fb-300">**저장소 blob toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="523fb-301">**Blob 복사 작업 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="523fb-302">**저장소 blob의 명령 toomanage 공유 액세스 서명**</span><span class="sxs-lookup"><span data-stu-id="523fb-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="523fb-303">**저장소 파일 공유 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="523fb-304">**저장소 파일 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="523fb-305">**저장소 파일 디렉터리 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="523fb-306">**저장소 큐 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="523fb-307">**저장소 큐의 명령 toomanage 공유 액세스 서명**</span><span class="sxs-lookup"><span data-stu-id="523fb-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="523fb-308">**저장 된 저장소 큐의 액세스 정책을 명령 toomanage**</span><span class="sxs-lookup"><span data-stu-id="523fb-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="523fb-309">**저장소 로깅 속성 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="523fb-310">**저장소 메트릭 속성 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="523fb-311">**저장소 테이블 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="523fb-312">**저장소 테이블의 명령 toomanage 공유 액세스 서명**</span><span class="sxs-lookup"><span data-stu-id="523fb-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="523fb-313">**저장 된 저장소 테이블의 액세스 정책을 명령 toomanage**</span><span class="sxs-lookup"><span data-stu-id="523fb-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="523fb-314">azure 태그: 리소스 관리자 태그 toomanage 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="523fb-315">**태그 추가**</span><span class="sxs-lookup"><span data-stu-id="523fb-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="523fb-316">**전체 태그 또는 태그 값 제거**</span><span class="sxs-lookup"><span data-stu-id="523fb-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="523fb-317">**Hello 태그 정보를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="523fb-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="523fb-318">**태그 가져오기**</span><span class="sxs-lookup"><span data-stu-id="523fb-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="523fb-319">azure vm: toomanage Azure 가상 컴퓨터 명령</span><span class="sxs-lookup"><span data-stu-id="523fb-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="523fb-320">**VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="523fb-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="523fb-321">**기본 리소스를 사용하여 VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="523fb-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="523fb-322">CLI 버전 0.10 부터는 "UbuntuLTS" 또는 "Win2012R2Datacenter" hello와 같은 짧은 별칭을 제공할 수 있습니다 `image-urn` 인기 있는 일부 마켓플레이스 이미지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="523fb-323">옵션으로 `azure help vm quick-create`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="523fb-324">또한 0.10으로 버전부터 `azure vm quick-create` hello 선택한 영역에 사용 되는 경우 프리미엄 저장소는 기본적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="523fb-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="523fb-325">**계정 내에서 목록 hello 가상 컴퓨터**</span><span class="sxs-lookup"><span data-stu-id="523fb-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="523fb-326">**리소스 그룹 내 한 가상 컴퓨터 가져오기**</span><span class="sxs-lookup"><span data-stu-id="523fb-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="523fb-327">**리소스 그룹 내 한 가상 컴퓨터 삭제**</span><span class="sxs-lookup"><span data-stu-id="523fb-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="523fb-328">**리소스 그룹 내 한 가상 컴퓨터 종료**</span><span class="sxs-lookup"><span data-stu-id="523fb-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="523fb-329">**리소스 그룹 내 한 가상 컴퓨터 다시 시작**</span><span class="sxs-lookup"><span data-stu-id="523fb-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="523fb-330">**리소스 그룹 내 한 가상 컴퓨터 시작**</span><span class="sxs-lookup"><span data-stu-id="523fb-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="523fb-331">**리소스 그룹 및 릴리스 hello 내에서 하나의 가상 컴퓨터를 종료할 계산 리소스**</span><span class="sxs-lookup"><span data-stu-id="523fb-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="523fb-332">**사용 가능한 가상 컴퓨터 크기 나열**</span><span class="sxs-lookup"><span data-stu-id="523fb-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="523fb-333">**Hello 운영 체제 이미지로 VM 또는 VM 이미지 캡처**</span><span class="sxs-lookup"><span data-stu-id="523fb-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="523fb-334">**Hello VM tooGeneralized의 hello 상태 설정**</span><span class="sxs-lookup"><span data-stu-id="523fb-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="523fb-335">**Hello VM의 인스턴스 뷰 가져오기**</span><span class="sxs-lookup"><span data-stu-id="523fb-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="523fb-336">**가상 컴퓨터 및 관리자 또는 sudo 권한이 있는 hello 계정의 tooreset hello 암호 tooreset 원격 데스크톱 액세스 또는 SSH 설정을 사용 하면**</span><span class="sxs-lookup"><span data-stu-id="523fb-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="523fb-337">**새 데이터로 VM 업데이트**</span><span class="sxs-lookup"><span data-stu-id="523fb-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="523fb-338">**가상 컴퓨터 데이터 디스크 toomanage 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="523fb-339">**명령 toomanage VM 리소스 확장**</span><span class="sxs-lookup"><span data-stu-id="523fb-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="523fb-340">**Toomanage Docker 가상 컴퓨터 명령**</span><span class="sxs-lookup"><span data-stu-id="523fb-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="523fb-341">**명령 toomanage VM 이미지**</span><span class="sxs-lookup"><span data-stu-id="523fb-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
