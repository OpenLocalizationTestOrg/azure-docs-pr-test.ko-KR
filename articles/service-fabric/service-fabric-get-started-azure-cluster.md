---
title: "Azure Service Fabric 클러스터 설정 | Microsoft Docs"
description: "빠른 시작 - Azure에서 Windows 또는 Linux Service Fabric 클러스터를 만듭니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: ec59450052b377412a28f7eaf55d1f1512b55195
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="9046f-103">Azure에서 첫 번째 Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="9046f-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="9046f-104">[Service Fabric 클러스터](service-fabric-deploy-anywhere.md): 마이크로 서비스가 배포되고 관리되는 네트워크로 연결된 가상 또는 실제 컴퓨터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="9046f-105">이 빠른 시작을 사용하여 몇 분만에 [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) 또는 [Azure Portal](http://portal.azure.com)을 통해 Windows 또는 Linux에서 실행하는 다섯 개의 노드 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-105">This quickstart helps you to create a five-node cluster, running on either Windows or Linux, through the [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="9046f-106">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-the-azure-portal"></a><span data-ttu-id="9046f-107">Azure 포털 사용</span><span class="sxs-lookup"><span data-stu-id="9046f-107">Use the Azure portal</span></span>

<span data-ttu-id="9046f-108">Azure Portal[http://portal.azure.com](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-108">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-the-cluster"></a><span data-ttu-id="9046f-109">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="9046f-109">Create the cluster</span></span>

1. <span data-ttu-id="9046f-110">Azure Portal의 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="9046f-111">**새로 만들기** 블레이드에서 **계산**을 선택한 다음 **계산** 블레이드에서 **Service Fabric 클러스터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-111">Select **Compute** from the **New** blade and then select **Service Fabric Cluster** from the **Compute** blade.</span></span>
3. <span data-ttu-id="9046f-112">Service Fabric **기본 사항** 양식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-112">Fill out the Service Fabric **Basics** form.</span></span> <span data-ttu-id="9046f-113">**운영 체제**의 경우 클러스터 노드를 실행하려는 Windows 또는 Linux의 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-113">For **Operating system**, select the version of Windows or Linux you want the cluster nodes to run.</span></span> <span data-ttu-id="9046f-114">여기에서 입력한 이사용자 이름과 암호는 가상 컴퓨터에 로그인하는 데 사용됩니다</span><span class="sxs-lookup"><span data-stu-id="9046f-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="9046f-115">**리소스 그룹**에 대해 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="9046f-116">리소스 그룹은 Azure 리소스가 만들어지고 전체적으로 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="9046f-117">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-117">When complete, click **OK**.</span></span>

    ![클러스터 설정 출력][cluster-setup-basics]

4. <span data-ttu-id="9046f-119">**클러스터 구성** 양식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-119">Fill out the **Cluster configuration** form.</span></span>  <span data-ttu-id="9046f-120">**노드 유형 개수**에는 "1"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="9046f-121">**노드 유형 1(기본)**을 선택하고 **노드 유형 구성** 양식을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-121">Select **Node type 1 (Primary)** and fill out the **Node type configuration** form.</span></span>  <span data-ttu-id="9046f-122">노드 유형 이름을 입력하고 [내구성 계층](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster)을 "동"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-122">Enter a node type name and set the [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) to "Bronze."</span></span>  <span data-ttu-id="9046f-123">VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-123">Select a VM size.</span></span>

    <span data-ttu-id="9046f-124">노드 유형은 VM 크기, VM 수, 사용자 지정 끝점 및 해당 유형 VM의 기타 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-124">Node types define the VM size, number of VMs, custom endpoints, and other settings for the VMs of that type.</span></span> <span data-ttu-id="9046f-125">정의된 각 노드 유형은 별도의 가상 컴퓨터 크기 집합으로 설정되고 가상 컴퓨터를 집합으로 배포하고 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-125">Each node type defined is set up as a separate virtual machine scale set, which is used to deploy and managed virtual machines as a set.</span></span> <span data-ttu-id="9046f-126">각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="9046f-127">첫 번째 또는 주 노드 유형은 Service Fabric 시스템 서비스가 호스팅되는 위치이며 5개 이상의 VM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-127">The first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="9046f-128">프로덕션 배포의 경우 [용량 계획](service-fabric-cluster-capacity.md)은 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="9046f-129">하지만 이 빠른 시작의 경우 응용 프로그램을 실행하지 않으므로 *DS1_v2 표준* VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="9046f-130">[안정성 계층](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) 및 초기 가상 컴퓨터 크기 집합인 5에서 "은"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-130">Select "Silver" for the [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="9046f-131">클러스터에서 실행 중인 응용 프로그램과 연결할 수 있도록 사용자 지정 끝점은 Azure Load Balancer에서 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-131">Custom endpoints open up ports in the Azure load balancer so that you can connect with applications running on the cluster.</span></span>  <span data-ttu-id="9046f-132">"80, 8172"를 입력하여 80 및 8172 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-132">Enter "80, 8172" to open up ports 80 and 8172.</span></span>

    <span data-ttu-id="9046f-133">TCP/HTTP 관리 끝점, 응용 프로그램 포트 범위, [배치 제약 조건](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints) 및 [용량 속성](service-fabric-cluster-resource-manager-metrics.md)을 사용자 지정하는 데 사용하는 **고급 설정 구성** 상자를 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-133">Do not check the **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="9046f-134">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-134">Select **OK**.</span></span>

6. <span data-ttu-id="9046f-135">**클러스터 구성** 양식에서 **진단**을 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-135">In the **Cluster configuration** form, set **Diagnostics** to **On**.</span></span>  <span data-ttu-id="9046f-136">이 빠른 시작의 경우 [패브릭 설정](service-fabric-cluster-fabric-settings.md) 속성을 입력하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-136">For this quickstart, you do not need to enter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="9046f-137">Microsoft에서 클러스터를 실행하는 패브릭 코드의 버전을 자동으로 업데이트하도록 **패브릭 버전**에서 **자동** 업그레이드 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates the version of the fabric code running the cluster.</span></span>  <span data-ttu-id="9046f-138">업그레이드할 [지원되는 버전을 선택](service-fabric-cluster-upgrade.md)하려는 경우 모드를 **수동**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-138">Set the mode to **Manual** if you want to [choose a supported version](service-fabric-cluster-upgrade.md) to upgrade to.</span></span> 

    ![노드 유형 구성][node-type-config]

    <span data-ttu-id="9046f-140">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-140">Select **OK**.</span></span>

7. <span data-ttu-id="9046f-141">**보안** 양식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-141">Fill out the **Security** form.</span></span>  <span data-ttu-id="9046f-142">이 빠른 시작의 경우 **보안 해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="9046f-143">하지만 누구든지 안전하지 않은 클러스터에 연결하고 관리 작업을 수행할 수 있게 되므로 프로덕션 워크로드에 대한 보안 클러스터를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-143">It is highly recommended to create a secure cluster for production workloads, however, since anyone can anonymously connect to an unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="9046f-144">인증서는 서비스 패브릭에서 클러스터 및 해당 응용 프로그램의 다양한 측면을 보호하기 위해 인증 및 암호화를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-144">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="9046f-145">Service Fabric에서 인증서가 사용되는 방식에 대한 자세한 내용은 [Service Fabric 클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9046f-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="9046f-146">Azure Active Directory를 사용하여 사용자 인증을 사용하거나 응용 프로그램 보안에 대한 인증서를 설정하려면 [Resource Manager 템플릿에서 클러스터를 만듭니다](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9046f-146">To enable user authentication using Azure Active Directory or to set up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="9046f-147">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-147">Select **OK**.</span></span>

8. <span data-ttu-id="9046f-148">요약을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-148">Review the summary.</span></span>  <span data-ttu-id="9046f-149">입력한 설정에서 빌드된 Resource Manager 템플릿을 다운로드하려는 경우 **템플릿 및 매개 변수 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-149">If you'd like to download a Resource Manager template built from the settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="9046f-150">**만들기**를 선택하여 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-150">Select **Create** to create the cluster.</span></span>

    <span data-ttu-id="9046f-151">알림에서 만들기 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-151">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="9046f-152">(화면 오른쪽 위의 상태 표시줄 근처에 있는 "종" 모양 아이콘을 클릭합니다.) 클러스터를 만드는 동안 **시작 보드에 고정**을 클릭하면 **Service Fabric 클러스터 배포 중**이 **시작** 보드에 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-152">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="9046f-153">클러스터 상태 보기</span><span class="sxs-lookup"><span data-stu-id="9046f-153">View cluster status</span></span>
<span data-ttu-id="9046f-154">클러스터를 만들면 포털의 **개요** 블레이드에서 클러스터를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-154">Once your cluster is created, you can inspect your cluster in the **Overview** blade in the portal.</span></span> <span data-ttu-id="9046f-155">이제 대시보드에서 클러스터의 공용 끝점 및 Service Fabric Explorer에 대한 링크를 포함한 클러스터 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-155">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

![클러스터 상태][cluster-status]

### <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="9046f-157">Service Fabric Explorer를 사용하여 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="9046f-157">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="9046f-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)는 클러스터를 시각화하고 응용 프로그램을 관리할 수 있는 좋은 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="9046f-159">Service Fabric Explorer는 클러스터에서 실행되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-159">Service Fabric Explorer is a service that runs in the cluster.</span></span>  <span data-ttu-id="9046f-160">포털의 클러스터 **개요** 페이지의 **Service Fabric Explorer** 링크를 클릭하여 웹 브라우저를 사용하는 서비스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-160">Access it using a web browser by clicking the **Service Fabric Explorer** link of the cluster **Overview** page in the portal.</span></span>  <span data-ttu-id="9046f-161">브라우저에 직접 주소를 입력할 수도 있습니다. [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="9046f-161">You can also enter the address directly into the browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="9046f-162">클러스터 대시보드는 응용 프로그램 및 노드 상태에 대한 요약을 포함하여 클러스터에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-162">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="9046f-163">노드 보기는 클러스터의 물리적 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-163">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="9046f-164">지정된 노드의 경우 해당 노드에 배포된 코드를 가진 응용 프로그램을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-to-the-cluster-using-powershell"></a><span data-ttu-id="9046f-166">PowerShell을 사용하여 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="9046f-166">Connect to the cluster using PowerShell</span></span>
<span data-ttu-id="9046f-167">PowerShell을 사용하도록 연결하여 클러스터가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-167">Verify that the cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="9046f-168">ServiceFabric PowerShell 모듈은 [Service Fabric SDK](service-fabric-get-started.md)에서 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-168">The ServiceFabric PowerShell module is installed with the [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="9046f-169">[Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet은 클러스터에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-169">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="9046f-170">클러스터에 연결하는 다른 예제는 [보안 클러스터에 연결](service-fabric-connect-to-secure-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9046f-170">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="9046f-171">클러스터에 연결한 후에는 [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet을 사용하여 클러스터의 노드 목록과 각 노드에 대한 상태 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-171">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="9046f-172">**HealthState**는 노드마다 *OK* 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-the-cluster"></a><span data-ttu-id="9046f-173">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="9046f-173">Remove the cluster</span></span>
<span data-ttu-id="9046f-174">Service Fabric 클러스터는 클러스터 리소스 외에도 다른 Azure 리소스로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-174">A Service Fabric cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="9046f-175">따라서 서비스 패브릭 클러스터를 완벽하게 삭제하려면 구성되어 있는 모든 리소스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-175">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span> <span data-ttu-id="9046f-176">클러스터 및 클러스터에서 사용하는 모든 리소스를 삭제하는 가장 간단한 방법은 리소스 그룹을 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-176">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> <span data-ttu-id="9046f-177">클러스터를 삭제하거나 리소스 그룹에서 리소스 일부(전부가 아님)를 삭제하는 다른 방법은 [클러스터 삭제](service-fabric-cluster-delete.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9046f-177">For other ways to delete a cluster or to delete some (but not all) the resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="9046f-178">Azure Portal에서 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-178">Delete a resource group in the Azure portal:</span></span>
1. <span data-ttu-id="9046f-179">삭제하려는 서비스 패브릭 클러스터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-179">Navigate to the Service Fabric cluster you want to delete.</span></span>
2. <span data-ttu-id="9046f-180">클러스터 필수 페이지에서 **리소스 그룹** 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-180">Click the **Resource Group** name on the cluster essentials page.</span></span>
3. <span data-ttu-id="9046f-181">**Resource Group Essentials**(필수 리소스 그룹) 페이지에서 **리소스 그룹 삭제**를 클릭하고 해당 페이지의 지침에 따라 리소스 그룹의 삭제를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-181">In the **Resource Group Essentials** page, click **Delete resource group** and follow the instructions on that page to complete the deletion of the resource group.</span></span>
    <span data-ttu-id="9046f-182">![리소스 그룹 삭제][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="9046f-182">![Delete the resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-to-deploy-a-secure-cluster"></a><span data-ttu-id="9046f-183">Azure PowerShell을 사용하여 보안 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="9046f-183">Use Azure Powershell to deploy a secure cluster</span></span>
1. <span data-ttu-id="9046f-184">[Azure PowerShell 모듈 버전 4.0 이상](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)을 컴퓨터에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-184">Download the [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="9046f-185">Windows PowerShell 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-185">Open a Windows PowerShell window, Run the following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="9046f-186">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-186">You should see an output similar to the following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="9046f-188">Azure에 로그인하고 클러스터를 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-188">Login to Azure and Select the subscription to which you want to create the cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="9046f-189">이제 다음 명령을 실행하여 보안 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-189">Run the following command to now create a secure cluster.</span></span> <span data-ttu-id="9046f-190">매개 변수를 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-190">Do not forget to customize the parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also the name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="9046f-191">명령을 완료하는 데 10~30분이 걸릴 수 있습니다. 작업이 끝나면 다음과 유사한 출력이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-191">The command can take anywhere from 10 minutes to 30 minutes to complete, at the end of it, you should get an output similar to the following.</span></span> <span data-ttu-id="9046f-192">출력에는 인증서, KeyVault 업로드 위치 및 인증서가 복사되는 위치에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-192">The output has information about the certificate, the KeyVault where it was uploaded to, and the local folder where the certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="9046f-194">참조하는 데 필요하기 때문에 전체 출력을 복사하고 텍스트 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-194">Copy the entire output and save to a text file as we need to refer to it.</span></span> <span data-ttu-id="9046f-195">출력에서 다음 정보를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-195">Make a note of the following information from the output.</span></span> 

    - <span data-ttu-id="9046f-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="9046f-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="9046f-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="9046f-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="9046f-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="9046f-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="9046f-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="9046f-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-the-certificate-on-your-local-machine"></a><span data-ttu-id="9046f-200">로컬 컴퓨터에 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="9046f-200">Install the certificate on your local machine</span></span>
  
<span data-ttu-id="9046f-201">클러스터에 연결하려면 현재 사용자의 개인 (내) 저장소에 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-201">To connect to the cluster, you need to install the certificate into the Personal (My) store of the current user.</span></span> 

<span data-ttu-id="9046f-202">다음 PowerShell 실행</span><span class="sxs-lookup"><span data-stu-id="9046f-202">Run the following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\the name of the cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="9046f-203">이제 보안 클러스터에 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-203">You are now ready to connect to your secure cluster.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="9046f-204">보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="9046f-204">Connect to a secure cluster</span></span> 

<span data-ttu-id="9046f-205">다음 PowerShell 명령을 실행하여 보안 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-205">Run the following PowerShell command to connect to a secure cluster.</span></span> <span data-ttu-id="9046f-206">인증서 세부 정보는 클러스터를 설정하는 데 사용된 인증서와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-206">The certificate details must match a certificate that was used to set up the cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="9046f-207">다음 예제에서는 완료된 매개 변수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-207">The following example shows the completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="9046f-208">다음 명령을 실행하여 사용자가 연결되어 있고 클러스터 상태가 정상인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-208">Run the following command to check that you are connected and the cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-to-your-cluster-from-visual-studio"></a><span data-ttu-id="9046f-209">Visual Studio에서 클러스터에 앱 게시</span><span class="sxs-lookup"><span data-stu-id="9046f-209">Publish your apps to your cluster from Visual Studio</span></span>

<span data-ttu-id="9046f-210">이제 Azure 클러스터를 설정했으므로 [클러스터에 게시](service-fabric-publish-app-remote-cluster.md) 문서를 수행하여 Visual Studio에서 Azure 클러스터에 이 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-210">Now that you have set up an Azure cluster, you can publish your applications to it from Visual Studio by following the [Publish to an cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-the-cluster"></a><span data-ttu-id="9046f-211">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="9046f-211">Remove the cluster</span></span>
<span data-ttu-id="9046f-212">클러스터는 클러스터 리소스 외에도 다른 Azure 리소스로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-212">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="9046f-213">클러스터 및 클러스터에서 사용하는 모든 리소스를 삭제하는 가장 간단한 방법은 리소스 그룹을 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9046f-213">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="9046f-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9046f-214">Next steps</span></span>
<span data-ttu-id="9046f-215">이제 개발 클러스터를 설정했으며 다음을 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="9046f-215">Now that you have set up a development cluster, try the following:</span></span>
* [<span data-ttu-id="9046f-216">포털에서 보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="9046f-216">Create a secure cluster in the portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="9046f-217">템플릿에서 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="9046f-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="9046f-218">PowerShell을 사용하여 앱 배포</span><span class="sxs-lookup"><span data-stu-id="9046f-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
