---
title: "Windows Server에서 독립 실행형 Azure Service Fabric 클러스터 업그레이드 | Microsoft 문서"
description: "클러스터 업데이트 모드 설정 등 독립 실행형 Service Fabric 클러스터를 실행하는 Azure Service Fabric 코드 및/또는 구성을 업그레이드합니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: ac40775ca62362a32184207857a0b965a798e135
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="a116a-103">Windows Server 클러스터에서 독립 실행형 Azure Service Fabric 업그레이드</span><span class="sxs-lookup"><span data-stu-id="a116a-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a116a-104">Azure 클러스터</span><span class="sxs-lookup"><span data-stu-id="a116a-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="a116a-105">독립 실행형 클러스터</span><span class="sxs-lookup"><span data-stu-id="a116a-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="a116a-106">최신 시스템에서 업그레이드하는 기능은 제품의 장기적인 성공을 위해 핵심적입니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-106">For any modern system, the ability to upgrade is a key to the long-term success of your product.</span></span> <span data-ttu-id="a116a-107">Azure 서비스 패브릭 클러스터는 사용자가 소유하는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="a116a-108">이 문서에서는 어떻게 클러스터가 Service Fabric 코드 및 구성의 지원되는 버전을 항상 실행하도록 하는지에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-108">This article describes how you can make sure that the cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-the-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="a116a-109">클러스터에서 실행되는 Service Fabric 버전 제어</span><span class="sxs-lookup"><span data-stu-id="a116a-109">Control the Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="a116a-110">Microsoft에서 새 버전을 출시할 때 Service Fabric 업데이트를 다운로드하도록 클러스터를 설정하려면 **fabricClusterAutoupgradeEnabled** 클러스터 구성을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-110">To set your cluster to download updates of Service Fabric when Microsoft releases a new version, set the **fabricClusterAutoupgradeEnabled** cluster configuration to true.</span></span> <span data-ttu-id="a116a-111">클러스터가 설정될 지원되는 Service Fabric 버전을 선택하려면 **fabricClusterAutoupgradeEnabled** 클러스터 구성을 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-111">To select a supported version of Service Fabric that you want your cluster to be on, set the **fabricClusterAutoupgradeEnabled** cluster configuration to false.</span></span>

> [!NOTE]
> <span data-ttu-id="a116a-112">클러스터가 지원되는 Service Fabric 버전을 항상 실행하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="a116a-113">Microsoft에서 새로운 버전의 Service Fabric 릴리스를 발표하면 이전 버전은 해당 발표일로부터 최소 60일 후 지원 종료되는 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-113">When Microsoft announces the release of a new version of Service Fabric, the previous version is marked for end of support after a minimum of 60 days from the date of the announcement.</span></span> <span data-ttu-id="a116a-114">새로운 릴리스는 [Service Fabric 팀 블로그](https://blogs.msdn.microsoft.com/azureservicefabric/)에서 발표됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-114">New releases are announced [on the Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="a116a-115">그러면 해당 시점에 새로운 릴리스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-115">The new release is available to choose at that point.</span></span>
>
>

<span data-ttu-id="a116a-116">각 Service Fabric 노드를 별도 물리적 컴퓨터 또는 가상 컴퓨터에 할당하는 프로덕션 스타일 노드 구성을 사용하는 경우에만 클러스터를 새 버전으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-116">You can upgrade your cluster to the new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="a116a-117">하나의 물리적 또는 가상 컴퓨터에 Service Fabric 노드가 여러 개 있는 개발 클러스터가 있는 경우 새 버전으로 클러스터를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create the cluster with the new version.</span></span>

<span data-ttu-id="a116a-118">클러스터를 최신 버전 또는 지원되는 Service Fabric 버전으로 업그레이드하는 데는 두 가지 워크플로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-118">Two distinct workflows can upgrade your cluster to the latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="a116a-119">한 가지 워크플로는 최신 버전을 자동으로 다운로드하도록 연결된 클러스터에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-119">One workflow is for clusters that have connectivity to download the latest version automatically.</span></span> <span data-ttu-id="a116a-120">또 다른 워크플로는 최신 Service Fabric 버전을 다운로드하기 위한 연결이 없는 클러스터에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-120">The other workflow is for clusters that do not have connectivity to download the latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="a116a-121">최신 코드와 구성을 다운로드하도록 연결된 클러스터 업그레이드</span><span class="sxs-lookup"><span data-stu-id="a116a-121">Upgrade clusters that have connectivity to download the latest code and configuration</span></span>
<span data-ttu-id="a116a-122">클러스터 노드가 [http://download.microsoft.com](http://download.microsoft.com)에 인터넷으로 연결되어 있는 경우 클러스터를 지원되는 버전으로 업그레이드하려면 이 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-122">Use these steps to upgrade your cluster to a supported version if your cluster nodes have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="a116a-123">[http://download.microsoft.com](http://download.microsoft.com)에 연결된 클러스터의 경우, Microsoft는 새 Service Fabric 버전의 가용성을 정기적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-123">For clusters that have connectivity to [http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for the availability of new Service Fabric versions.</span></span>

<span data-ttu-id="a116a-124">새 Service Fabric 버전을 사용할 수 있는 경우 패키지를 클러스터에 로컬로 다운로드하고 업그레이드를 위해 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-124">When a new Service Fabric version is available, the package is downloaded locally to the cluster and provisioned for upgrade.</span></span> <span data-ttu-id="a116a-125">또한 이 새로운 버전을 고객에게 알리기 위해 시스템은 다음과 같이 명시적인 클러스터 상태 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-125">Additionally, to inform the customer of this new version, the system shows an explicit cluster health warning that's similar to the following:</span></span>

<span data-ttu-id="a116a-126">"현재 클러스터 버전[버전 #] 지원은 [날짜]로 종료됩니다."</span><span class="sxs-lookup"><span data-stu-id="a116a-126">“The current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="a116a-127">클러스터가 최신 버전을 실행한 후 경고는 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-127">After the cluster is running the latest version, the warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="a116a-128">클러스터 업그레이드 워크플로</span><span class="sxs-lookup"><span data-stu-id="a116a-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="a116a-129">클러스터 상태 경고가 표시된 후 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-129">After you see the cluster health warning, do the following:</span></span>

1. <span data-ttu-id="a116a-130">클러스터에서 노드로 나열된 모든 컴퓨터에 대한 관리자 액세스 권한이 있는 모든 컴퓨터에서 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-130">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="a116a-131">이 스크립트가 실행되는 컴퓨터가 클러스터의 일부일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-131">The machine that this script is run on does not have to be part of the cluster.</span></span>

    ```powershell

    ###### connect to the secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="a116a-132">업그레이드할 수 있는 Service Fabric 버전의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-132">Get the list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="a116a-133">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-133">You should get an output similar to this:</span></span>

    ![패브릭 버전 가져오기][getfabversions]
3. <span data-ttu-id="a116a-135">[Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd 명령을 사용하여 사용 가능한 버전으로 클러스터 업그레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-135">Start a cluster upgrade to an available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="a116a-136">업그레이드 진행률을 모니터링하려면 Service Fabric Explorer를 사용하거나 다음 Windows PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-136">To monitor the progress of the upgrade, you can use Service Fabric Explorer or run the following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="a116a-137">클러스터 상태 정책이 충족되지 않는 경우 업그레이드가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-137">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="a116a-138">**Start-ServiceFabricClusterUpgrade** 명령에 대한 사용자 지정 상태 정책을 지정하려면 [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx)에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a116a-138">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="a116a-139">롤백을 일으킨 문제를 수정한 후 이전과 동일한 단계에 따라 업그레이드를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-139">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="a116a-140">최신 코드와 구성을 다운로드하도록 <U>연결되지 않은</u> 클러스터 업그레이드</span><span class="sxs-lookup"><span data-stu-id="a116a-140">Upgrade clusters that have <U>no connectivity</u> to download the latest code and configuration</span></span>
<span data-ttu-id="a116a-141">클러스터 노드가 [http://download.microsoft.com](http://download.microsoft.com)에 인터넷으로 연결되어 있지 않은 경우 클러스터를 지원되는 버전으로 업그레이드하려면 이 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-141">Use these steps to upgrade your cluster to a supported version if your cluster nodes do not have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="a116a-142">인터넷에 연결되지 않은 클러스터를 실행하는 경우 Service Fabric 팀 블로그를 모니터링하여 새 릴리스를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-142">If you are running a cluster that is not connected to the Internet, you will have to monitor the Service Fabric team blog to learn about a new release.</span></span> <span data-ttu-id="a116a-143">시스템은 새 릴리스를 알리는 클러스터 상태 경고를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-143">The system does not show a cluster health warning to alert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="a116a-144">자동 프로비전 및 수동 프로비전</span><span class="sxs-lookup"><span data-stu-id="a116a-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="a116a-145">최신 코드 버전의 자동 다운로드 및 등록을 사용하도록 설정하려면 Service Fabric 업데이트 서비스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-145">To enable automatic downloading and registration for the latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="a116a-146">지침에 대해서는 Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt [독립 실행형 패키지](service-fabric-cluster-standalone-package-contents.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a116a-146">Refer to the Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside the [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="a116a-147">수동 프로세스에 대해서는 아래의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="a116a-147">For manual process, follow the instructions below.</span></span>

<span data-ttu-id="a116a-148">구성 업그레이드를 시작하기 전에 클러스터 구성을 수정하여 다음 속성을 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-148">Modify your cluster configuration to set the following property to false before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="a116a-149">자세한 사용 방법은 [Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a116a-149">Refer to [Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="a116a-150">구성 업그레이드를 시작하기 전에 JSON에서 'clusterConfigurationVersion'을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-150">Make sure to update 'clusterConfigurationVersion' in your JSON before you start the configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="a116a-151">클러스터 업그레이드 워크플로</span><span class="sxs-lookup"><span data-stu-id="a116a-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="a116a-152">클러스터의 노드 중 하나에서 Get-ServiceFabricClusterUpgrade를 실행하고 TargetCodeVersion을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-152">Run Get-ServiceFabricClusterUpgrade from one of the nodes in the cluster and note the TargetCodeVersion.</span></span>
2. <span data-ttu-id="a116a-153">인터넷에 연결된 컴퓨터에서 다음을 실행하여 현재 버전과 호환 가능한 모든 업그레이드 버전을 나열하고 연결된 다운로드 링크에서 해당 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-153">Run the following from an internet connected machine to list all upgrade compatible versions with the current version and download the corresponding package from the associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="a116a-154">클러스터에서 노드로 나열된 모든 컴퓨터에 대한 관리자 액세스 권한이 있는 모든 컴퓨터에서 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-154">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="a116a-155">이 스크립트가 실행되는 컴퓨터가 클러스터의 일부일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-155">The machine that this script is run on does not have to be part of the cluster</span></span>

    ```powershell

   ###### Get the list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file including the path to it> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="a116a-156">다운로드 한 패키지를 클러스터 이미지 저장소에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-156">Copy the downloaded package into the cluster image store.</span></span>

5. <span data-ttu-id="a116a-157">복사된 패키지를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-157">Register the copied package.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="a116a-158">사용 가능한 버전으로의 클러스터 업그레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-158">Start a cluster upgrade to an available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="a116a-159">Service Fabric Explorer에서 업그레이드 진행률을 모니터링하거나 다음 PowerShell 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-159">You can monitor the progress of the upgrade on Service Fabric Explorer, or you can run the following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="a116a-160">클러스터 상태 정책이 충족되지 않는 경우 업그레이드가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-160">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="a116a-161">**Start-ServiceFabricClusterUpgrade** 명령에 대한 사용자 지정 상태 정책을 지정하려면 [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx)에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a116a-161">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="a116a-162">롤백을 일으킨 문제를 수정한 후 이전과 동일한 단계에 따라 업그레이드를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-162">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>


## <a name="upgrade-the-cluster-configuration"></a><span data-ttu-id="a116a-163">클러스터 구성 업그레이드</span><span class="sxs-lookup"><span data-stu-id="a116a-163">Upgrade the cluster configuration</span></span>
<span data-ttu-id="a116a-164">구성 업그레이드를 시작하기 전에 독립 실행형 패키지에서 PowerShell 스크립트를 실행하여 새 클러스터 구성 json을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-164">Before you initiate the configuration upgrade, you can test your new cluster configuration json by running the powershell script in the standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File>

```
<span data-ttu-id="a116a-165">또는</span><span class="sxs-lookup"><span data-stu-id="a116a-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File> -FabricRuntimePackagePath <Path to the .cab file which you want to test the configuration against>

```

<span data-ttu-id="a116a-166">끝점, 클러스터 이름, 노드 IP 등의 일부 구성은 업그레이드할 수 없습니다. 여기서는 새 클러스터 구성 json과 이전 json을 비교하여 테스트를 진행하며, 문제가 있으면 PowerShell 창에서 오류를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test the new cluster configuration json against the old one and throw errors in the Powershell window if there is any issue.</span></span>

<span data-ttu-id="a116a-167">클러스터 구성을 업그레이드하려면 **Start-ServiceFabricClusterConfigurationUpgrade**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-167">To upgrade the cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="a116a-168">업그레이드 도메인으로 구성 업그레이드가 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-168">The configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="a116a-169">클러스터 인증서 구성 업그레이드</span><span class="sxs-lookup"><span data-stu-id="a116a-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="a116a-170">오류는 클러스터 노드 간의 통신을 차단하므로 주의해서 인증서 롤오버가 실행될 수 있도록 클러스터 노드 간 인증에 클러스터 인증서가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-170">Cluster certificate is used for authentication between cluster nodes, so the certificate roll over should be performed with extra caution because failure will block the communication among cluster nodes.</span></span>  
<span data-ttu-id="a116a-171">기술적으로 세 가지 옵션이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="a116a-172">단일 인증서 업그레이드: 업그레이드 경로는 '인증서 A(기본) -> 인증서 B(기본) -> 인증서 C(기본) ->...'입니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-172">Single certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="a116a-173">이중 인증서 업그레이드: 업그레이드 경로는 '인증서 A(기본) -> 인증서 A(기본) 및 B(보조) -> 인증서 B(기본) -> 인증서 B(기본) 및 C(보조) -> 인증서 C(기본) ->...'입니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-173">Double certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="a116a-174">인증서 형식 업그레이드: 지문 기반 인증서 구성 <-> CommonName 기반 인증서 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="a116a-175">예를 들어, 인증서 지문 A(기본) 및 지문 B(보조) -> 인증서 CommonName C입니다.</span><span class="sxs-lookup"><span data-stu-id="a116a-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a116a-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a116a-176">Next steps</span></span>
* <span data-ttu-id="a116a-177">[Service Fabric 클러스터 설정](service-fabric-cluster-fabric-settings.md) 중 일부를 사용자 지정하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="a116a-177">Learn how to customize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="a116a-178">[클러스터를 확장 및 축소](service-fabric-cluster-scale-up-down.md)하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="a116a-178">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="a116a-179">[응용 프로그램 업그레이드](service-fabric-application-upgrade.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="a116a-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
