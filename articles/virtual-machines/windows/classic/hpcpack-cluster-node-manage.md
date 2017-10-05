---
title: "HPC 팩 클러스터 계산 노드 관리 | Microsoft Docs"
description: "Azure에서 HPC 팩 2012 R2 클러스터 계산 노드를 추가, 제거, 시작, 중지하는 PowerShell 스크립트 도구에 대해 알아보세요."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="41cf0-103">Azure의 HPC 팩 클러스터에 있는 계산 노드의 수 및 가용성 관리</span><span class="sxs-lookup"><span data-stu-id="41cf0-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="41cf0-104">Azure VM에 HPC Pack 2012 R2 클러스터를 만든 경우 클러스터에서 일부 계산 노드 VM을 손쉽게 추가, 제거, 시작(프로비전), 중지(프로비전 해제)할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="41cf0-105">이러한 작업을 하려면 헤드 노드 VM에 설치된 Azure PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="41cf0-106">이러한 스크립트로 HPC 팩 클러스터 리소스의 수와 가용성을 관리하여 비용을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="41cf0-107">이 문서는 클래식 배포 모델을 사용하여 만든 Azure의 HPC Pack 2012 R2 클러스터에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="41cf0-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="41cf0-109">또한 이 문서에 설명된 PowerShell 스크립트는 HPC Pack 2016에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41cf0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41cf0-110">Prerequisites</span></span>
* <span data-ttu-id="41cf0-111">**Azure VM의 HPC Pack 2012 R2 클러스터**: 클래식 배포 모델로 HPC Pack 2012 R2 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="41cf0-112">예를 들어 Azure Marketplace 및 Azure PowerShell 스크립트에서 HPC Pack 2012 R2 VM 이미지를 사용하여 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="41cf0-113">자세한 내용 및 필수 구성 요소는 [HPC 팩 IaaS 배포 스크립트를 사용하여 HPC 클러스터 만들기](hpcpack-cluster-powershell-script.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41cf0-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="41cf0-114">배포 후 헤드 노드의 %CCP\_HOME%bin 폴더에서 노드 관리 스크립트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="41cf0-115">각 스크립트는 관리자 권한으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="41cf0-116">**Azure 게시 설정 파일 또는 관리 인증서**: 헤드 노드에서 다음 중 하나를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="41cf0-117">**Azure 게시 설정 파일을 가져옵니다**.</span><span class="sxs-lookup"><span data-stu-id="41cf0-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="41cf0-118">이렇게 하려면 헤드 노드에서 다음 Azure PowerShell cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="41cf0-119">**헤드 노드에서 Azure 관리 인증서를 구성합니다**.</span><span class="sxs-lookup"><span data-stu-id="41cf0-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="41cf0-120">.cer 파일이 있는 경우 CurrentUser\My certificate 저장소로 가져온 다음 Azure 환경(AzureCloud 또는 AzureChinaCloud)에 대해 다음 Azure PowerShell cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="41cf0-121">계산 노드 VM 추가</span><span class="sxs-lookup"><span data-stu-id="41cf0-121">Add compute node VMs</span></span>
<span data-ttu-id="41cf0-122">**Add-HpcIaaSNode.ps1** 스크립트를 사용하여 계산 노드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="41cf0-123">구문</span><span class="sxs-lookup"><span data-stu-id="41cf0-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="41cf0-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="41cf0-124">Parameters</span></span>
* <span data-ttu-id="41cf0-125">**ServiceName**: 새 계산 노드 VM이 추가될 클라우드 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="41cf0-126">**ImageName**: Azure VM 이미지 이름으로, Azure 클래식 포털 또는 Azure PowerShell cmdlet **Get-AzureVMImage**를 통해 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="41cf0-127">이 이미지는 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="41cf0-128">Windows 운영 체제를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="41cf0-129">HPC 팩을 계산 노드 역할로 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="41cf0-130">이 이미지는 공용 Azure VM 이미지가 아닌 사용자 범주의 개인 이미지여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="41cf0-131">**Quantity**: 추가할 계산 노드 VM의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="41cf0-132">**InstanceSize**: 계산 노드 VM의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="41cf0-133">**DomainUserName**: 도메인 사용자 이름으로 새 VM을 도메인에 연결하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="41cf0-134">**DomainUserPassword**: 도메인 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="41cf0-135">**NodeNameSeries**(선택 사항): 계산 노드의 명명 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="41cf0-136">형식은 &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="41cf0-137">예를 들어 MyCN%10%은 MyCN11부터 시작하는 계산 노드 이름의 시리즈를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="41cf0-138">이 매개 변수를 지정하지 않을 경우 스크립트는 HPC 클러스터에서 구성된 노드 명명 시리즈를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="41cf0-139">예제</span><span class="sxs-lookup"><span data-stu-id="41cf0-139">Example</span></span>
<span data-ttu-id="41cf0-140">다음 예제는 VM 이미지인 *hpccnimage1*을 기준으로 클라우드 서비스 *hpcservice1*에 20개의 대형 크기 컴퓨터 노드 VM을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="41cf0-141">계산 노드 VM 제거</span><span class="sxs-lookup"><span data-stu-id="41cf0-141">Remove compute node VMs</span></span>
<span data-ttu-id="41cf0-142">**Remove-HpcIaaSNode.ps1** 스크립트를 사용하여 계산 노드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="41cf0-143">구문</span><span class="sxs-lookup"><span data-stu-id="41cf0-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="41cf0-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="41cf0-144">Parameters</span></span>
* <span data-ttu-id="41cf0-145">**Name**: 제거할 클러스터 노드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="41cf0-146">와일드카드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-146">Wildcards are supported.</span></span> <span data-ttu-id="41cf0-147">매개 변수 설정 이름은 Name입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-147">The parameter set name is Name.</span></span> <span data-ttu-id="41cf0-148">**Name** 및 **Node** 매개 변수를 모두 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="41cf0-149">**Node**: 제거할 노드의 HpcNode 개체로 HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx)를 통해 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="41cf0-150">매개 변수 설정 이름은 Node입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-150">The parameter set name is Node.</span></span> <span data-ttu-id="41cf0-151">**Name** 및 **Node** 매개 변수를 모두 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="41cf0-152">**DeleteVHD**(선택 사항): 제거된 VM의 관련 디스크를 삭제하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="41cf0-153">**Force**(선택 사항): HPC 노드를 제거하기 전에 HPC 노드를 오프라인으로 강제 전환하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="41cf0-154">**확인**(선택 사항): 명령을 실행하기 전 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="41cf0-155">**WhatIf**: 실제로 명령을 실행하지 않고 명령을 실행할 경우에 상황에 대해 설명하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="41cf0-156">예제</span><span class="sxs-lookup"><span data-stu-id="41cf0-156">Example</span></span>
<span data-ttu-id="41cf0-157">다음 예제는 이름이 *HPCNode-CN-*으로 시작하는 노드를 오프라인으로 강제 전환한 다음 노드와 관련 디스크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="41cf0-158">계산 노드 VM 시작</span><span class="sxs-lookup"><span data-stu-id="41cf0-158">Start compute node VMs</span></span>
<span data-ttu-id="41cf0-159">**Start-HpcIaaSNode.ps1** 스크립트를 사용하여 계산 노드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="41cf0-160">구문</span><span class="sxs-lookup"><span data-stu-id="41cf0-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="41cf0-161">매개 변수</span><span class="sxs-lookup"><span data-stu-id="41cf0-161">Parameters</span></span>
* <span data-ttu-id="41cf0-162">**Name**: 시작할 클러스터 노드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="41cf0-163">와일드카드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-163">Wildcards are supported.</span></span> <span data-ttu-id="41cf0-164">매개 변수 설정 이름은 Name입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-164">The parameter set name is Name.</span></span> <span data-ttu-id="41cf0-165">**Name** 및 **Node** 매개 변수를 모두 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="41cf0-166">**Node**- 시작할 노드의 HpcNode 개체로 HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx)를 통해 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="41cf0-167">매개 변수 설정 이름은 Node입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-167">The parameter set name is Node.</span></span> <span data-ttu-id="41cf0-168">**Name** 및 **Node** 매개 변수를 모두 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="41cf0-169">예제</span><span class="sxs-lookup"><span data-stu-id="41cf0-169">Example</span></span>
<span data-ttu-id="41cf0-170">다음 예제는 이름이 *HPCNode-CN-*로 시작하는 노드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="41cf0-171">계산 노드 VM 중지</span><span class="sxs-lookup"><span data-stu-id="41cf0-171">Stop compute node VMs</span></span>
<span data-ttu-id="41cf0-172">**Stop-HpcIaaSNode.ps1** 스크립트를 사용하여 컴퓨터 노드를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="41cf0-173">구문</span><span class="sxs-lookup"><span data-stu-id="41cf0-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="41cf0-174">매개 변수</span><span class="sxs-lookup"><span data-stu-id="41cf0-174">Parameters</span></span>
* <span data-ttu-id="41cf0-175">**Name** - 중지할 클러스터 노드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="41cf0-176">와일드카드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-176">Wildcards are supported.</span></span> <span data-ttu-id="41cf0-177">매개 변수 설정 이름은 Name입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-177">The parameter set name is Name.</span></span> <span data-ttu-id="41cf0-178">**Name** 및 **Node** 매개 변수를 모두 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="41cf0-179">**Node**: 중지할 노드의 HpcNode 개체로 HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx)를 통해 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="41cf0-180">매개 변수 설정 이름은 Node입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-180">The parameter set name is Node.</span></span> <span data-ttu-id="41cf0-181">**Name** 및 **Node** 매개 변수를 모두 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="41cf0-182">**Force**(선택 사항): HPC 노드를 중지하기 전에 HPC 노드를 오프라인으로 강제 전환하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="41cf0-183">예제</span><span class="sxs-lookup"><span data-stu-id="41cf0-183">Example</span></span>
<span data-ttu-id="41cf0-184">다음 예제는 이름이 *HPCNode-CN-* 로 시작하는 노드를 오프라인으로 강제 전환한 다음 노드를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf0-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="41cf0-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41cf0-185">Next steps</span></span>
* <span data-ttu-id="41cf0-186">클러스터 노드를 현재 클러스터 작업의 워크로드에 따라 자동으로 증가 또는 축소하려면 [클러스터 워크로드에 따라 Azure에서 HPC 팩 클러스터 리소스를 자동으로 증가 및 축소](hpcpack-cluster-node-autogrowshrink.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41cf0-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

