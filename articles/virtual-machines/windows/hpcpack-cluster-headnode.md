---
title: "Azure VM에서 HPC 팩 헤드 노드 만들기 | Microsoft Docs"
description: "Azure Portal 및 Resource Manager 배포 모델을 사용하여 Azure VM에 Microsoft HPC 팩 2012 R2 헤드 노드를 만드는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: b2bb9caf82a580dc5f67ea0b0b1c2e9a46363e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-the-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a><span data-ttu-id="9b78d-103">마켓플레이스 이미지를 사용하여 Azure VM에 HPC 팩 클러스터의 헤드 노드 만들기</span><span class="sxs-lookup"><span data-stu-id="9b78d-103">Create the head node of an HPC Pack cluster in an Azure VM with a Marketplace image</span></span>
<span data-ttu-id="9b78d-104">Azure Marketplace 및 Azure Portal에서 [Microsoft HPC 팩 2012 R2 가상 컴퓨터 이미지](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)를 사용하여 HPC 클러스터의 헤드 노드를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-104">Use a [Microsoft HPC Pack 2012 R2 virtual machine image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) from the Azure Marketplace and the Azure portal to create the head node of an HPC cluster.</span></span> <span data-ttu-id="9b78d-105">이 HPC 팩 VM 이미지는 HPC 팩 2012 R2 업데이트 3이 미리 설치된 Windows Server 2012 R2 Datacenter를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-105">This HPC Pack VM image is based on Windows Server 2012 R2 Datacenter with HPC Pack 2012 R2 Update 3 pre-installed.</span></span> <span data-ttu-id="9b78d-106">Azure에서 HPC 팩의 개념 증명 배포에 대해 이 헤드 노드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-106">Use this head node for a proof of concept deployment of HPC Pack in Azure.</span></span> <span data-ttu-id="9b78d-107">그런 다음 계산 노드를 HPC 워크로드를 실행하는 클러스터에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-107">You can then add compute nodes to the cluster to run HPC workloads.</span></span>

> [!TIP]
> <span data-ttu-id="9b78d-108">헤드 노드와 계산 노드를 포함하는 전체 HPC 팩 2012 R2 클러스터를 Azure에 배포하려면 자동화된 방법을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-108">To deploy a complete HPC Pack 2012 R2 cluster in Azure that includes the head node and compute nodes, we recommend that you use an automated method.</span></span> <span data-ttu-id="9b78d-109">옵션에는 [HPC 팩 IaaS 배포 스크립트](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 및 [Windows 워크로드에 대한 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)와 같은 Resource Manager 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-109">Options include the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and Resource Manager templates such as the [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/).</span></span> <span data-ttu-id="9b78d-110">Resource Manager 템플릿은 [Microsoft HPC 팩 2016 클러스터](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates)에 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-110">Resource Manager templates are also available for [Microsoft HPC Pack 2016 clusters](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates).</span></span> 
> 
> 

## <a name="planning-considerations"></a><span data-ttu-id="9b78d-111">고려 사항 계획</span><span class="sxs-lookup"><span data-stu-id="9b78d-111">Planning considerations</span></span>
<span data-ttu-id="9b78d-112">다음 그림에 나와 있는 것처럼 Azure 가상 네트워크의 Active Directory 도메인에 HPC Pack 헤드 노드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-112">As shown in the following figure, you deploy the HPC Pack head node in an Active Directory domain in an Azure virtual network.</span></span>

![HPC 팩 헤드 노드][headnode]

* <span data-ttu-id="9b78d-114">**Active Directory 도메인**: VM에서 HPC 서비스를 시작하기 전에 HPC 팩 2012 R2 헤드 노드를 Azure의 Active Directory 도메인에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-114">**Active Directory domain**: The HPC Pack 2012 R2 head node must be joined to an Active Directory domain in Azure before you start the HPC services on the VM.</span></span> <span data-ttu-id="9b78d-115">이 문서에서 설명한 것처럼 개념 증명 배포의 경우 HPC 서비스를 시작하기 전에 도메인 컨트롤러인 헤드 노드에 대해 만드는 VM을 승격할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-115">As shown in this article, for a proof of concept deployment, you can promote the VM you create for the head node as a domain controller before starting the HPC services.</span></span> <span data-ttu-id="9b78d-116">헤드 노드 VM을 연결하는 Azure에 별도의 도메인 컨트롤러 및 포리스트를 배포하는 방법도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-116">Another option is to deploy a separate domain controller and forest in Azure to which you join the head node VM.</span></span>

* <span data-ttu-id="9b78d-117">**배포 모델**: 새로운 배포는 대부분 Resource Manager 배포 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-117">**Deployment model**: For most new deployments, Microsoft recommends that you use the Resource Manager deployment model.</span></span> <span data-ttu-id="9b78d-118">이 문서에서는 배포 모델을 사용하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-118">This article assumes that you use this deployment model.</span></span>

* <span data-ttu-id="9b78d-119">**Azure Virtual Network**: Resource Manager 배포 모델을 사용하여 헤드 노드를 배포하는 경우 Azure Virtual Network를 지정하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-119">**Azure virtual network**: When you use the Resource Manager deployment model to deploy the head node, you specify or create an Azure virtual network.</span></span> <span data-ttu-id="9b78d-120">헤드 노드를 기존 Active Directory 도메인에 가입하는 경우 가상 네트워크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-120">You use the virtual network if you need to join the head node to an existing Active Directory domain.</span></span> <span data-ttu-id="9b78d-121">나중에 클러스터에 계산 노드 VM을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-121">You also need it later to add compute node VMs to the cluster.</span></span>

## <a name="steps-to-create-the-head-node"></a><span data-ttu-id="9b78d-122">헤드 노드를 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="9b78d-122">Steps to create the head node</span></span>
<span data-ttu-id="9b78d-123">다음은 Azure 포털에서 Resource Manager 배포 모델을 사용하여 HPC Pack 헤드 노드용 Azure VM을 만들기 위한 자세한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-123">Following are high-level steps to use the Azure portal to create an Azure VM for the HPC Pack head node by using the Resource Manager deployment model.</span></span> 

1. <span data-ttu-id="9b78d-124">별도 도메인 컨트롤러 VM으로 Azure에 새 Active Directory 포리스트를 만들려는 경우 [Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc)을 사용하는 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-124">If you want to create a new Active Directory forest in Azure with separate domain controller VMs, one option is to use a [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc).</span></span> <span data-ttu-id="9b78d-125">간단한 개념 증명 배포의 경우 이 단계를 생략하고 헤드 노드 VM 자체를 도메인 컨트롤러로 구성해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-125">For a simple proof of concept deployment, it's fine to omit this step and configure the head node VM itself as a domain controller.</span></span> <span data-ttu-id="9b78d-126">이 옵션은 이 문서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-126">This option is described later in this article.</span></span>
2. <span data-ttu-id="9b78d-127">Azure 마켓플레이스에서 [Windows Server 2012 R2의 HPC Pack 2012 R2 페이지](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) 에서 **가상 컴퓨터 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-127">On the [HPC Pack 2012 R2 on Windows Server 2012 R2 page](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) in the Azure Marketplace, click **Create Virtual Machine**.</span></span> 
3. <span data-ttu-id="9b78d-128">포털의 **Windows Server 2012 R2에 있는 HPC 팩 2012 R2** 페이지에서 **Resource Manager** 배포 모델을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-128">In the portal, on the **HPC Pack 2012 R2 on Windows Server 2012 R2** page, select the **Resource Manager** deployment model and then click **Create**.</span></span>
   
    ![HPC 팩 이미지][marketplace]
4. <span data-ttu-id="9b78d-130">포털을 사용하여 설정을 구성하고 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-130">Use the portal to configure the settings and create the VM.</span></span> <span data-ttu-id="9b78d-131">Azure를 처음 접하는 경우 자습서 [Azure Portal에서 Windows 가상 컴퓨터 만들기](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="9b78d-131">If you're new to Azure, follow the tutorial [Create a Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9b78d-132">개념 증명 배포의 경우 일반적으로 기본 설정 또는 권장 설정을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-132">For a proof of concept deployment, you can usually accept the default or recommended settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9b78d-133">Azure에서 기존 Active Directory 도메인에 헤드 노드를 가입하려는 경우 VM을 만들 때 해당 도메인에 대한 가상 네트워크를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-133">If you want to join the head node to an existing Active Directory domain in Azure, make sure you specify the virtual network for that domain when creating the VM.</span></span>
   > 
   > 
5. <span data-ttu-id="9b78d-134">VM을 만든 다음 VM이 실행되면 원격 데스크톱을 사용하여 [VM에 연결합니다](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="9b78d-134">After you create the VM and the VM is running, [connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) by Remote Desktop.</span></span> 
6. <span data-ttu-id="9b78d-135">다음 옵션 중 하나를 선택하여 Active Directory 도메인 포리스트에 VM을 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-135">Join the VM to an Active Directory domain forest by choosing one of the following options:</span></span>
   
   * <span data-ttu-id="9b78d-136">기존 도메인 포리스트가 있는 Azure 가상 네트워크에 VM을 만든 경우 표준 서버 관리자 또는 Windows PowerShell 도구를 사용하여 포리스트에 VM을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-136">If you created the VM in an Azure virtual network with an existing domain forest, join the VM to the forest by using standard Server Manager or Windows PowerShell tools.</span></span> <span data-ttu-id="9b78d-137">그런 다음 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-137">Then restart.</span></span>
   * <span data-ttu-id="9b78d-138">기존 도메인 포리스트가 없는 새 가상 네트워크에 VM을 만든 경우 VM을 도메인 컨트롤러로 승격합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-138">If you created the VM in a new virtual network (without an existing domain forest), then promote the VM as a domain controller.</span></span> <span data-ttu-id="9b78d-139">표준 단계를 사용하여 헤드 노드에 Active Directory 도메인 서비스 역할을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-139">Use standard steps to install and configure the Active Directory Domain Services role on the head node.</span></span> <span data-ttu-id="9b78d-140">자세한 단계를 보려면 [새 Windows Server 2012 Active Directory 포리스트 설치](https://technet.microsoft.com/library/jj574166.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b78d-140">For detailed steps, see [Install a New Windows Server 2012 Active Directory Forest](https://technet.microsoft.com/library/jj574166.aspx).</span></span>
7. <span data-ttu-id="9b78d-141">VM이 실행되고 Active Directory 포리스트에 연결되면 다음과 같이 HPC Pack 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-141">After the VM is running and is joined to an Active Directory forest, start the HPC Pack services as follows:</span></span>
   
    <span data-ttu-id="9b78d-142">a.</span><span class="sxs-lookup"><span data-stu-id="9b78d-142">a.</span></span> <span data-ttu-id="9b78d-143">로컬 관리자 그룹의 구성원인 도메인 계정을 사용하여 헤드 노드 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-143">Connect to the head node VM using a domain account that is a member of the local Administrators group.</span></span> <span data-ttu-id="9b78d-144">예를 들어 헤드 노드 VM을 만들 때 설정한 관리자 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-144">For example, use the administrator account you set up when you created the head node VM.</span></span>
   
    <span data-ttu-id="9b78d-145">b.</span><span class="sxs-lookup"><span data-stu-id="9b78d-145">b.</span></span> <span data-ttu-id="9b78d-146">기본 헤드 노드 구성의 경우 관리자 권한으로 Windows PowerShell을 시작하고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-146">For a default head node configuration, start Windows PowerShell as an administrator and type the following:</span></span>
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    <span data-ttu-id="9b78d-147">HPC 팩 서비스가 시작하는 데 몇 분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-147">It can take several minutes for the HPC Pack services to start.</span></span>
   
    <span data-ttu-id="9b78d-148">추가 헤드 노드 구성 옵션을 보려면 `get-help HPCHNPrepare.ps1`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-148">For additional head node configuration options, type `get-help HPCHNPrepare.ps1`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b78d-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b78d-149">Next steps</span></span>
* <span data-ttu-id="9b78d-150">이제 HPC 팩 클러스터의 헤드 노드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-150">You can now work with the head node of your HPC Pack cluster.</span></span> <span data-ttu-id="9b78d-151">예를 들어 HPC 클러스터 관리자를 시작하고 [배포할 일 모음](https://technet.microsoft.com/library/jj884141.aspx)을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-151">For example, start HPC Cluster Manager, and complete the [Deployment To-do List](https://technet.microsoft.com/library/jj884141.aspx).</span></span>
* <span data-ttu-id="9b78d-152">필요 시 클러스터 계산 용량을 늘리려면 클라우드 서비스에 [Azure 버스트 노드](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-152">If you want to increase the cluster compute capacity on-demand, add [Azure burst nodes](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) in a cloud service.</span></span> 
* <span data-ttu-id="9b78d-153">클러스터에서 테스트 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b78d-153">Try running a test workload on the cluster.</span></span> <span data-ttu-id="9b78d-154">예를 보려면 HPC 팩 [시작하기 가이드](https://technet.microsoft.com/library/jj884144)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b78d-154">For an example, see the HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
