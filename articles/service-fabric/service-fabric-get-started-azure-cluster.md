---
title: "Azure 서비스 패브릭 클러스터를 aaaSet | Microsoft Docs"
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
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="1ab16-103">Azure에서 첫 번째 Service Fabric 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1ab16-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="1ab16-104">[Service Fabric 클러스터](service-fabric-deploy-anywhere.md): 마이크로 서비스가 배포되고 관리되는 네트워크로 연결된 가상 또는 실제 컴퓨터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="1ab16-105">이 퀵 스타트의 toocreate hello를 통해 Windows 또는 Linux를 실행 하는 다섯 개 노드 클러스터를 사용 하면. [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) 또는 [Azure 포털](http://portal.azure.com) 단 몇 분 후에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="1ab16-106">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="1ab16-107">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1ab16-107">Use hello Azure portal</span></span>

<span data-ttu-id="1ab16-108">Toohello Azure 포털에 로그인 [http://portal.azure.com](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="1ab16-109">Hello 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1ab16-109">Create hello cluster</span></span>

1. <span data-ttu-id="1ab16-110">Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="1ab16-111">선택 **계산** hello에서 **새로** 블레이드에 대 한 다음 선택 **서비스 패브릭 클러스터** hello에서 **계산** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="1ab16-112">서비스 패브릭 hello 채울 **기본 사항** 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="1ab16-113">에 대 한 **운영 체제**선택, hello 버전의 Windows 또는 Linux 클러스터 노드 toorun hello 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="1ab16-114">hello 사용자 이름 및 암호를 여기에 입력 된 toohello 가상 컴퓨터에서 사용 되는 toolog입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="1ab16-115">**리소스 그룹**에 대해 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="1ab16-116">리소스 그룹은 Azure 리소스가 만들어지고 전체적으로 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="1ab16-117">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-117">When complete, click **OK**.</span></span>

    ![클러스터 설정 출력][cluster-setup-basics]

4. <span data-ttu-id="1ab16-119">Hello 채울 **클러스터 구성** 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="1ab16-120">**노드 유형 개수**에는 "1"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="1ab16-121">선택 **노드 유형 1 (기본)** hello 확인 하 고 **노드 유형 구성** 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="1ab16-122">노드 유형 이름을 입력 하 고 hello 설정 [내구성 계층](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) 너무 "브론즈."</span><span class="sxs-lookup"><span data-stu-id="1ab16-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="1ab16-123">VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-123">Select a VM size.</span></span>

    <span data-ttu-id="1ab16-124">기타 설정에 대 한 해당 유형의 Vm hello 및 노드 형식은 hello VM 크기, Vm, 사용자 지정 끝점 수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="1ab16-125">정의 된 각 노드 형식 집합으로 사용 되는 toodeploy 및 관리 되는 가상 컴퓨터에이 별도 가상 컴퓨터 크기 집합으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="1ab16-126">각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="1ab16-127">hello 첫 번째 또는, 주 노드 유형 중 이며 여기서 서비스 패브릭 시스템 서비스 호스팅되는 Vm 5 개 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="1ab16-128">프로덕션 배포의 경우 [용량 계획](service-fabric-cluster-capacity.md)은 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="1ab16-129">하지만 이 빠른 시작의 경우 응용 프로그램을 실행하지 않으므로 *DS1_v2 표준* VM 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="1ab16-130">Hello에 대 한 "Silver"를 선택 [안정성 계층](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) 초기 가상 컴퓨터 크기는 5의 용량을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="1ab16-131">사용자 지정 끝점 hello 클러스터에서 실행 중인 응용 프로그램과 연결할 수 있도록 hello Azure 부하 분산 장치에 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="1ab16-132">포트 80 및 8172를 "80, 8172" tooopen를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="1ab16-133">Hello 검사 안 함 **고급 설정 구성** TCP/HTTP 관리 끝점, 응용 프로그램 포트 범위를 사용자 지정에 사용 되는 상자 [배치 제약 조건](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), 및 [용량 속성](service-fabric-cluster-resource-manager-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="1ab16-134">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-134">Select **OK**.</span></span>

6. <span data-ttu-id="1ab16-135">Hello에 **클러스터 구성** 양식에서 설정 **진단** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="1ab16-136">이 빠른 시작에 대 한 불필요 tooenter 어떤 [패브릭 설정](service-fabric-cluster-fabric-settings.md) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="1ab16-137">**패브릭 버전**선택, **자동** Microsoft hello 버전의 hello 클러스터를 실행 하는 hello 패브릭 코드를 자동으로 업데이트 되도록 모드를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="1ab16-138">너무 hello 모드 설정**수동** 너무 하려는 경우[지원 되는 버전 선택](service-fabric-cluster-upgrade.md) tooupgrade를 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![노드 유형 구성][node-type-config]

    <span data-ttu-id="1ab16-140">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-140">Select **OK**.</span></span>

7. <span data-ttu-id="1ab16-141">Hello 채울 **보안** 폼입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="1ab16-142">이 빠른 시작의 경우 **보안 해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="1ab16-143">그러나이 뛰어납니다 toocreate 프로덕션 작업에 대 한 보안 클러스터 하므로 권장 익명으로 tooan 보안 되지 않은 클러스터에 연결 하 고 관리 작업을 수행할 수 누구나 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="1ab16-144">인증서 서비스 패브릭 tooprovide toosecure 인증 및 암호화에에서 사용 되는 클러스터 및 해당 응용 프로그램의 다양 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="1ab16-145">Service Fabric에서 인증서가 사용되는 방식에 대한 자세한 내용은 [Service Fabric 클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ab16-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="1ab16-146">응용 프로그램 보안에 대 한 Azure Active Directory 또는 tooset 인증서를 사용 하 여 tooenable 사용자 인증 [리소스 관리자 템플릿에서 클러스터를 만드는](service-fabric-cluster-creation-via-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="1ab16-147">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-147">Select **OK**.</span></span>

8. <span data-ttu-id="1ab16-148">검토 hello를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-148">Review hello summary.</span></span>  <span data-ttu-id="1ab16-149">입력 hello 설정에서 작성 된 리소스 관리자 템플릿을 toodownload 원하는 경우, 선택 **템플릿 및 매개 변수를 다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="1ab16-150">선택 **만들기** toocreate hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="1ab16-151">Hello 알림이 hello 만들기 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="1ab16-152">(근처 hello 상태 표시줄 hello 오른쪽 상단의 화면에 "hello"벨 아이콘을 클릭 합니다.) 클릭 한 경우 **Pin tooStartboard** 참조 hello 클러스터를 만드는 동안 **서비스 패브릭 클러스터 배포** toohello 고정 **시작** 보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="1ab16-153">클러스터 상태 보기</span><span class="sxs-lookup"><span data-stu-id="1ab16-153">View cluster status</span></span>
<span data-ttu-id="1ab16-154">클러스터를 만든 후 hello에서 클러스터를 검사할 수 있습니다 **개요** 블레이드 hello 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="1ab16-155">이제 클러스터 대시보드에 hello hello 클러스터의 공용 끝점 및 링크 tooService 패브릭 탐색기 등의 hello 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![클러스터 상태][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="1ab16-157">서비스 패브릭 탐색기를 사용 하 여 hello 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="1ab16-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="1ab16-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)는 클러스터를 시각화하고 응용 프로그램을 관리할 수 있는 좋은 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="1ab16-159">서비스 패브릭 탐색기는 hello 클러스터에서 실행 되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="1ab16-160">웹 브라우저를 사용 하 여 hello를 클릭 하 여 액세스할 **서비스 패브릭 탐색기** hello 클러스터의 링크 **개요** hello 포털의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="1ab16-161">Hello 브라우저에 직접 hello 주소를 입력할 수도 있습니다: [http://quickstartcluster.westus.cloudapp.azure.com:19080/탐색기](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="1ab16-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="1ab16-162">hello 클러스터 대시보드는 응용 프로그램 및 노드 상태 요약을 포함 하 여 클러스터에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="1ab16-163">hello 노드 보기 hello hello 클러스터의 실제 레이아웃을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="1ab16-164">지정된 노드의 경우 해당 노드에 배포된 코드를 가진 응용 프로그램을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="1ab16-166">PowerShell을 사용 하 여 toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="1ab16-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="1ab16-167">PowerShell을 사용 하 여 연결 하 여 해당 hello 클러스터가 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="1ab16-168">hello ServiceFabric PowerShell 모듈이 설치 된 hello로 [서비스 패브릭 SDK](service-fabric-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="1ab16-169">hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet은 연결 toohello 클러스터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="1ab16-170">참조 [연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md) 연결 tooa 클러스터의 다른 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="1ab16-171">연결 toohello 클러스터 후 hello를 사용 하 여 [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello 클러스터 및 상태 정보를 각 노드에 대 한 노드 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="1ab16-172">**HealthState**는 노드마다 *OK* 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-172">**HealthState** should be *OK* for each node.</span></span>

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

### <a name="remove-hello-cluster"></a><span data-ttu-id="1ab16-173">Hello 클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="1ab16-173">Remove hello cluster</span></span>
<span data-ttu-id="1ab16-174">서비스 패브릭 클러스터 구성 된 다른 Azure 리소스로 또한 자체 toohello 클러스터 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="1ab16-175">Toocompletely 서비스 패브릭 클러스터를 삭제 하므로 toodelete 모든 hello 리소스 구성 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="1ab16-176">hello 가장 간단한 방법은 toodelete hello 클러스터와 사용 하는 모든 hello 리소스 toodelete hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="1ab16-177">다른 방법으로 toodelete 클러스터 나 toodelete 리소스 그룹의 일부 (모두는 아니지만) hello 리소스 참조에 대 한 [클러스터를 삭제](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="1ab16-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="1ab16-178">Hello Azure 포털에서에서 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="1ab16-179">원하는 toodelete toohello 서비스 패브릭 클러스터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="1ab16-180">Hello 클릭 **리소스 그룹** hello 클러스터 essentials 페이지 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="1ab16-181">Hello에 **리소스 그룹 Essentials** 페이지 **리소스 그룹 삭제** hello 리소스 그룹의 해당 페이지 toocomplete hello 삭제 시 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="1ab16-182">![Hello 리소스 그룹 삭제][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="1ab16-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="1ab16-183">Azure Powershell toodeploy 보안 클러스터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1ab16-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="1ab16-184">Hello 다운로드 [Azure Powershell 모듈 버전 4.0 이상이](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="1ab16-185">다음 명령을 실행 hello Windows PowerShell 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="1ab16-186">출력 유사한 toohello 다음을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-186">You should see an output similar toohello following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="1ab16-188">로그인 tooAzure 및 선택 hello 구독 toowhich toocreate hello 클러스터</span><span class="sxs-lookup"><span data-stu-id="1ab16-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="1ab16-189">다음 명령은 toonow 실행된 hello 보안 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="1ab16-190">Toocustomize hello 매개 변수를 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="1ab16-191">hello 명령에서 10 분 too30 분 toocomplete hello 끝 부분에서 아무 곳 이나 사용할 수 있는, 출력 유사한 toohello 다음을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="1ab16-192">hello 출력 hello 인증서를 업로드, KeyVault hello에 대 한 정보 및 hello 로컬 폴더 hello 인증서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="1ab16-194">Hello 전체 출력 복사한 toorefer tooit 필요 하므로 tooa 텍스트 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="1ab16-195">Hello hello 출력에서 다음 정보를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="1ab16-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="1ab16-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="1ab16-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="1ab16-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="1ab16-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="1ab16-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="1ab16-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="1ab16-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="1ab16-200">로컬 컴퓨터에 hello 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="1ab16-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="1ab16-201">tooconnect toohello 클러스터 hello 현재 사용자의 개인 (My) 저장소 hello로 tooinstall hello 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="1ab16-202">다음 PowerShell hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="1ab16-203">준비 tooconnect tooyour 보안 클러스터가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="1ab16-204">Tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="1ab16-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="1ab16-205">다음 PowerShell 명령을 tooconnect tooa 보안 클러스터 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="1ab16-206">hello 인증서 세부 정보는 hello 클러스터를 사용 하는 tooset 했던 인증서를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="1ab16-207">다음 예제에서는 hello hello 매개 변수를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="1ab16-208">다음 명령 toocheck 연결 하 고 hello 클러스터 상태가 정상이 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="1ab16-209">Visual Studio에서 앱 tooyour 클러스터 게시</span><span class="sxs-lookup"><span data-stu-id="1ab16-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="1ab16-210">에 Azure 클러스터를 설정 했으므로 다음 hello 하 여 Visual Studio에서 응용 프로그램 tooit 프로그램을 게시할 수 있습니다 [게시 tooan 클러스터](service-fabric-publish-app-remote-cluster.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="1ab16-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="1ab16-211">Hello 클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="1ab16-211">Remove hello cluster</span></span>
<span data-ttu-id="1ab16-212">클러스터 구성 된 다른 Azure 리소스로 또한 자체 toohello 클러스터 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="1ab16-213">hello 가장 간단한 방법은 toodelete hello 클러스터와 사용 하는 모든 hello 리소스 toodelete hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="1ab16-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ab16-214">Next steps</span></span>
<span data-ttu-id="1ab16-215">에 개발 클러스터를 설정 했으므로 hello 다음을 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="1ab16-216">Hello 포털에서 보안 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1ab16-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="1ab16-217">템플릿에서 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1ab16-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="1ab16-218">PowerShell을 사용하여 앱 배포</span><span class="sxs-lookup"><span data-stu-id="1ab16-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
