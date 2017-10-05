---
title: "Windows를 실행하는 Azure VM에서 독립 실행형 클러스터 만들기 | Microsoft Docs"
description: "Windows Server를 실행하는 Azure 가상 컴퓨터에서 Azure 서비스 패브릭 클러스터를 만들고 관리하는 방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: f8a0305a22c00f9bdbdb1bdb06dc299cccee23dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="1db5a-103">Windows Server를 실행하는 Azure 가상 컴퓨터에서 세 개 노드의 독립 실행형 서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1db5a-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="1db5a-104">이 문서에서는 Windows Server용 독립 실행형 Service Fabric 설치 관리자를 사용하여 Windows 기반 Azure 가상 컴퓨터(VM)에서 클러스터를 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="1db5a-105">이 시나리오는 [Windows Server에서 실행되는 클러스터 만들기 및 관리](service-fabric-cluster-creation-for-windows-server.md)의 특수한 경우이며, 여기서 VM은 [Windows Server를 실행하는 Azure VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)이지만 [Azure 클라우드 기반 Service Fabric 클러스터](service-fabric-cluster-creation-via-portal.md)를 만들지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="1db5a-106">이 패턴을 따를 때의 차이점은 사용자가 다음 단계에 따라 만든 독립 실행형 Service Fabric 클러스터를 전적으로 관리하는 반면, Service Fabric 리소스 공급자는 Azure 클라우드 기반 Service Fabric 클러스터를 관리 및 업그레이드한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span></span>

## <a name="steps-to-create-the-standalone-cluster"></a><span data-ttu-id="1db5a-107">독립 실형형 클러스터를 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="1db5a-107">Steps to create the standalone cluster</span></span>
1. <span data-ttu-id="1db5a-108">Azure Portal에 로그인하고 리소스 그룹에 새 Windows Server 2012 R2 Datacenter VM 또는 Windows Server 2016 Datacenter VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="1db5a-109">자세한 내용은 [Azure Portal에서 Windows VM 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1db5a-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="1db5a-110">동일한 리소스 그룹에 VM을 둘 이상 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-110">Add a couple more VMs to the same resource group.</span></span> <span data-ttu-id="1db5a-111">각 VM은 만들어질 때 동일한 관리자 사용자 이름 및 암호를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-111">Ensure that each of the VMs has the same administrator user name and password when created.</span></span> <span data-ttu-id="1db5a-112">만들어지면 동일한 가상 네트워크에 3개의 모든 VM이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-112">Once created you should see all three VMs in the same virtual network.</span></span>
3. <span data-ttu-id="1db5a-113">각 VM에 연결하고 [서버 관리자, 로컬 서버 대시보드](https://technet.microsoft.com/library/jj134147.aspx)를 사용하여 Windows 방화벽을 끕니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="1db5a-114">이렇게 하면 네트워크 트래픽은 컴퓨터 간에 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-114">This ensures that the network traffic can communicate between the machines.</span></span> <span data-ttu-id="1db5a-115">각 컴퓨터에 연결되어 있는 동안 명령 프롬프트를 열고 `ipconfig`를 입력하여 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="1db5a-116">또는 리소스 그룹에 대한 Virtual Network 리소스를 선택하고 이 컴퓨터 각각에 대해 만든 네트워크 인터페이스를 확인하여 포털에서 각 컴퓨터의 IP 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="1db5a-117">VM 중 하나에 연결하고 다른 두 VM을 성공적으로 ping할 수 있는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span></span>
5. <span data-ttu-id="1db5a-118">VM 중 하나에 연결하고 컴퓨터의 새 폴더에 [Windows Server용 독립 실행형 서비스 패브릭 패키지를 다운로드](http://go.microsoft.com/fwlink/?LinkId=730690) 하고 패키지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span></span>
6. <span data-ttu-id="1db5a-119">메모장에서 *ClusterConfig.Unsecure.MultiMachine.json* 파일을 열고 컴퓨터의 세 개의 IP 주소로 각 노드를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span></span> <span data-ttu-id="1db5a-120">위쪽에서 클러스터 이름을 변경하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-120">Change the cluster name at the top and save the file.</span></span>  <span data-ttu-id="1db5a-121">클러스터 매니페스트의 부분적인 예는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-121">A partial example of the cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="1db5a-122">안전한 클러스터가 되도록 하려면 사용하려는 보안 방법을 결정하고 [X509 인증서](service-fabric-windows-cluster-x509-security.md) 또는 [Windows 보안](service-fabric-windows-cluster-windows-security.md) 링크의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="1db5a-123">Windows 보안을 사용하여 클러스터를 설정하는 경우 Active Directory를 관리할 도메인 컨트롤러를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span></span> <span data-ttu-id="1db5a-124">도메인 컨트롤러 컴퓨터를 Service Fabric 노드로 사용하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="1db5a-125">[PowerShell ISE 창](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="1db5a-126">다운로드한 독립 실행형 설치 관리자 패키지의 압축을 풀고 클러스터 구성 파일을 저장한 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span></span> <span data-ttu-id="1db5a-127">다음 PowerShell 명령을 실행하여 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-127">Run the following PowerShell command to deploy the cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="1db5a-128">스크립트는 Service Fabric 클러스터를 원격으로 구성하고 배포를 롤업하면서 진행 상황을 보고해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="1db5a-129">약 1분 후 컴퓨터의 IP 주소 중 하나를 사용하여(예: `http://10.1.0.5:19080/Explorer/index.html` 사용) Service Fabric Explorer에 연결하여 클러스터가 작동되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1db5a-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1db5a-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1db5a-130">Next steps</span></span>
* [<span data-ttu-id="1db5a-131">Windows Server 또는 Linux에서 독립 실행형 서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1db5a-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="1db5a-132">독립 실행형 서비스 패브릭 클러스터에 노드 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="1db5a-132">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="1db5a-133">독립 실행형 Windows 클러스터에 대한 구성 설정</span><span class="sxs-lookup"><span data-stu-id="1db5a-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="1db5a-134">Windows 보안을 사용하여 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="1db5a-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="1db5a-135">X509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="1db5a-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

