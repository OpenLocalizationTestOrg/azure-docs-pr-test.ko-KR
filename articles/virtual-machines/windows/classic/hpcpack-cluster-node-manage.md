---
title: "aaaManage HPC Pack 클러스터 계산 노드 | Microsoft Docs"
description: "PowerShell 스크립트 도구 tooadd, 제거, 시작을 확인 하 고 Azure의 HPC Pack 2012 R2 클러스터 계산 노드를 중지 합니다."
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
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="2268e-103">Hello 번호와 Azure에서 HPC Pack 클러스터에서 계산 노드의 가용성 관리</span><span class="sxs-lookup"><span data-stu-id="2268e-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="2268e-104">Azure Vm에서 HPC Pack 2012 R2 클러스터를 만든 경우 tooeasily 추가, 제거, 시작 (프로 비전), 또는 중지 (프로 비전 해제) 몇 가지 방법으로 클러스터의 노드 Vm을 계산 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="2268e-105">toodo 이러한 작업을 hello 헤드 노드 VM에 설치 된 Azure PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="2268e-106">이러한 스크립트 도움말 비용을 제어할 수 있도록 hello 번호 및 HPC 팩 클러스터 리소스의 가용성을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2268e-107">이 문서에는 hello 클래식 배포 모델을 사용 하 여 만든 azure에서 Pack 2012 R2 클러스터만 tooHPC 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="2268e-108">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="2268e-109">또한이 문서에서 설명 하는 hello PowerShell 스크립트 HPC 팩 2016에서 사용할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2268e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2268e-110">Prerequisites</span></span>
* <span data-ttu-id="2268e-111">**Azure Vm에서 HPC Pack 2012 R2 클러스터**: hello 클래식 배포 모델에는 HPC Pack 2012 R2 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="2268e-112">예를 들어 hello Azure Marketplace에서에서 hello HPC Pack 2012 R2 VM 이미지와 Azure PowerShell 스크립트를 사용 하 여 hello 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="2268e-113">정보 및 필수 구성 요소에 대 한 참조 [hello HPC Pack IaaS 배포 스크립트는 HPC 클러스터 만들기](hpcpack-cluster-powershell-script.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="2268e-114">배포 후 hello 노드 관리 스크립트에서에서 찾기 hello %CCP\_홈 hello 헤드 노드의 %bin 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="2268e-115">관리자 권한으로 각각 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="2268e-116">**Azure 게시 설정 파일 또는 관리 인증서**: hello 헤드 노드에서 toodo hello 다음 중 하나를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="2268e-117">**가져오기 hello Azure 게시 설정 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="2268e-118">toodo hello 헤드 노드에 Azure PowerShell cmdlet을 다음이 실행된 hello:</span><span class="sxs-lookup"><span data-stu-id="2268e-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="2268e-119">**헤드 노드에 hello hello Azure 관리 인증서를 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="2268e-120">Hello.cer 파일이 있으면 hello CurrentUser\My 인증서 저장소에 가져온 후 hello Azure PowerShell cmdlet (azure 클라우드 또는 AzureChinaCloud) Azure 환경에 대 한 다음를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="2268e-121">계산 노드 VM 추가</span><span class="sxs-lookup"><span data-stu-id="2268e-121">Add compute node VMs</span></span>
<span data-ttu-id="2268e-122">Hello로 계산 노드를 추가 **Add-hpciaasnode.ps1** 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="2268e-123">구문</span><span class="sxs-lookup"><span data-stu-id="2268e-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="2268e-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2268e-124">Parameters</span></span>
* <span data-ttu-id="2268e-125">**ServiceName**: hello 새 계산 노드 Vm 클라우드 서비스의 이름에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="2268e-126">**ImageName**: hello Azure 클래식 포털 또는 Azure PowerShell cmdlet을 통해 가져올 수 있는 Azure VM 이미지 이름을 **Get-azurevmimage**합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="2268e-127">hello 이미지 hello 요구 사항을 준수를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="2268e-128">Windows 운영 체제를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="2268e-129">HPC Pack hello 계산 노드 역할에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="2268e-130">hello 이미지가 공용 Azure VM 이미지가 하지 hello 사용자 범주의 개인 이미지 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="2268e-131">**수량**: 계산 노드 Vm toobe 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="2268e-132">**InstanceSize**: 계산 노드 Vm hello의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="2268e-133">**DomainUserName**: 사용 되는 toojoin hello 새 Vm toohello 도메인은 도메인 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="2268e-134">**DomainUserPassword**: hello 도메인 사용자의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="2268e-135">**NodeNameSeries** (선택 사항): 노드 이름 지정 패턴 hello에 대 한 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="2268e-136">hello 형식 이어야 &lt; *루트\_이름*&gt;&lt;*시작\_번호*&gt;%입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="2268e-137">예를 들어 MyCN %10% 의미는 일련의 hello MyCN11에서 시작 하는 노드 이름을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="2268e-138">지정 하지 않으면 hello 스크립트 사용 하 여 hello hello HPC 클러스터에서 노드 명명 시리즈를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="2268e-139">예제</span><span class="sxs-lookup"><span data-stu-id="2268e-139">Example</span></span>
<span data-ttu-id="2268e-140">hello 다음 예제에서는 추가 20 크기가 대형 인 계산 노드 Vm 클라우드 서비스의 hello *hpcservice1*hello VM 이미지에 따라 *hpccnimage1*합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="2268e-141">계산 노드 VM 제거</span><span class="sxs-lookup"><span data-stu-id="2268e-141">Remove compute node VMs</span></span>
<span data-ttu-id="2268e-142">Hello로 계산 노드 제거 **Remove-hpciaasnode.ps1** 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="2268e-143">구문</span><span class="sxs-lookup"><span data-stu-id="2268e-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="2268e-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2268e-144">Parameters</span></span>
* <span data-ttu-id="2268e-145">**이름**: 클러스터 노드 toobe의 이름을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="2268e-146">와일드카드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-146">Wildcards are supported.</span></span> <span data-ttu-id="2268e-147">hello 매개 변수 집합 이름은 Name가입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-147">hello parameter set name is Name.</span></span> <span data-ttu-id="2268e-148">두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2268e-149">**노드**: hello HPC PowerShell cmdlet을 통해 가져올 수 있는 hello HpcNode 개체를 제거 하는 hello 노드 toobe [Get-hpcnode](https://technet.microsoft.com/library/dn887927.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="2268e-150">hello 매개 변수 집합 이름은 Node입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-150">hello parameter set name is Node.</span></span> <span data-ttu-id="2268e-151">두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2268e-152">**DeleteVHD** (선택 사항): toodelete hello 제거 된 Vm에 대 한 hello 연결 된 디스크를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="2268e-153">**Force** (선택 사항): 제거 하기 전에 tooforce HPC 노드를 오프 라인으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="2268e-154">**확인** (선택 사항): 확인 hello 명령을 실행 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="2268e-155">**WhatIf**: toodescribe 어떤 설정 했을 때 hello 명령을 실제로 실행 하지 않고도 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="2268e-156">예제</span><span class="sxs-lookup"><span data-stu-id="2268e-156">Example</span></span>
<span data-ttu-id="2268e-157">hello 다음 예제에서는 오프 라인 hello 노드를 강제 시작 하는 이름을 *HPCNode-CN-* hello 노드와 연결 된 디스크를 제거 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="2268e-158">계산 노드 VM 시작</span><span class="sxs-lookup"><span data-stu-id="2268e-158">Start compute node VMs</span></span>
<span data-ttu-id="2268e-159">시작 하는 계산 노드 hello로 **Start-hpciaasnode.ps1** 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="2268e-160">구문</span><span class="sxs-lookup"><span data-stu-id="2268e-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="2268e-161">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2268e-161">Parameters</span></span>
* <span data-ttu-id="2268e-162">**이름**: hello 클러스터 노드 toobe 형태의 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="2268e-163">와일드카드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-163">Wildcards are supported.</span></span> <span data-ttu-id="2268e-164">hello 매개 변수 집합 이름은 Name가입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-164">hello parameter set name is Name.</span></span> <span data-ttu-id="2268e-165">두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2268e-166">**노드**-hello HPC PowerShell cmdlet을 통해 가져올 수 있는 hello HpcNode 개체를 시작 하는 hello 노드 toobe [Get-hpcnode](https://technet.microsoft.com/library/dn887927.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="2268e-167">hello 매개 변수 집합 이름은 Node입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-167">hello parameter set name is Node.</span></span> <span data-ttu-id="2268e-168">두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="2268e-169">예제</span><span class="sxs-lookup"><span data-stu-id="2268e-169">Example</span></span>
<span data-ttu-id="2268e-170">hello 다음 예제에서는 시작 노드 이름이 시작 *HPCNode-CN-*합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="2268e-171">계산 노드 VM 중지</span><span class="sxs-lookup"><span data-stu-id="2268e-171">Stop compute node VMs</span></span>
<span data-ttu-id="2268e-172">Hello로 계산 노드 중지 **중지 HpcIaaSNode.ps1** 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="2268e-173">구문</span><span class="sxs-lookup"><span data-stu-id="2268e-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="2268e-174">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2268e-174">Parameters</span></span>
* <span data-ttu-id="2268e-175">**이름**-hello 클러스터 노드 toobe 형태의 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="2268e-176">와일드카드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-176">Wildcards are supported.</span></span> <span data-ttu-id="2268e-177">hello 매개 변수 집합 이름은 Name가입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-177">hello parameter set name is Name.</span></span> <span data-ttu-id="2268e-178">두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2268e-179">**노드**: hello HPC PowerShell cmdlet을 통해 가져올 수 있는 hello HpcNode 개체를 중지 하는 hello 노드 toobe [Get-hpcnode](https://technet.microsoft.com/library/dn887927.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="2268e-180">hello 매개 변수 집합 이름은 Node입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-180">hello parameter set name is Node.</span></span> <span data-ttu-id="2268e-181">두 hello를 지정할 수 없습니다 **이름** 및 **노드** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2268e-182">**Force** (선택 사항): 중지 하기 전에 tooforce HPC 노드를 오프 라인으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="2268e-183">예제</span><span class="sxs-lookup"><span data-stu-id="2268e-183">Example</span></span>
<span data-ttu-id="2268e-184">hello 다음 예제에서는 오프 라인 노드를 강제 시작 하는 이름을 *HPCNode-CN-* 다음 중지 hello 노드 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="2268e-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="2268e-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2268e-185">Next steps</span></span>
* <span data-ttu-id="2268e-186">증가 또는 hello 작업 및 hello 클러스터에서 작업의 현재 작업량에 따라 hello 클러스터 노드를 축소, 참조 tooautomatically [자동으로 리소스 확장 및 축소 hello HPC Pack 클러스터에서 Azure에 따라 toohello 클러스터 작업](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="2268e-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

