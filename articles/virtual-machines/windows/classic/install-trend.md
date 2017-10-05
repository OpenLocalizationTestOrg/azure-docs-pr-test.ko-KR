---
title: "VM에 Trend Micro Deep Security 설치 | Microsoft Docs"
description: "이 문서에서는 Azure에서 클래식 배포 모델을 사용하여 만든 VM에 Trend Micro 보안을 설치하고 구성하는 방법을 설명합니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: 911b8f12472dcbda3e6bfeb8c97bf1d04a63e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="40f6c-103">Windows VM에 Trend Micro Deep Security as a Service를 설치하고 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="40f6c-103">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="40f6c-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="40f6c-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="40f6c-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="40f6c-107">이 문서에서는 Windows Server가 실행되는 새 VM(가상 컴퓨터) 또는 기존 VM에서 Trend Micro Deep Security as a Service를 설치 및 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-107">This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="40f6c-108">Deep Security as a Service는 맬웨어 방지 보호, 방화벽, 침입 방지 시스템 및 무결성 모니터링을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="40f6c-109">이 클라이언트는 VM 에이전트를 통해 보안 확장 프로그램으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-109">The client is installed as a security extension via the VM Agent.</span></span> <span data-ttu-id="40f6c-110">VM 에이전트는 Azure Portal에서 자동으로 생성되므로 새 가상 컴퓨터에서 Deep Security Agent를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-110">On a new virtual machine, you install the Deep Security Agent, as the VM Agent is created automatically by the Azure portal.</span></span>

<span data-ttu-id="40f6c-111">클래식 포털, Azure CLI 또는 PowerShell을 사용하여 만든 기존 VM에는 VM 에이전트가 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-111">An existing VM created using the classic portal, the Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="40f6c-112">VM 에이전트가 없는 기존 가상 컴퓨터에서는 이 에이전트를 먼저 다운로드하여 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-112">For an existing virtual machine that doesn't have the VM Agent, you need to download and install it first.</span></span> <span data-ttu-id="40f6c-113">이 문서에서는 두 상황을 모두 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-113">This article covers both situations.</span></span>

<span data-ttu-id="40f6c-114">온-프레미스 솔루션용 Trend Micro의 현재 구독이 있는 경우 Azure Virtual Machines를 보호하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it to help protect your Azure virtual machines.</span></span> <span data-ttu-id="40f6c-115">아직 구독 고객이 아닌 경우에는 평가판 구독에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="40f6c-116">이 솔루션에 대한 자세한 내용은 Trend Micro 블로그 게시물 [Deep Security에 대한 Microsoft Azure VM 에이전트 확장](http://go.microsoft.com/fwlink/p/?LinkId=403945)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40f6c-116">For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-the-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="40f6c-117">새 VM에 Deep Security Agent 설치</span><span class="sxs-lookup"><span data-stu-id="40f6c-117">Install the Deep Security Agent on a new VM</span></span>

<span data-ttu-id="40f6c-118">**Marketplace**의 이미지를 사용하여 가상 컴퓨터를 만드는 경우 [Azure Portal](http://portal.azure.com)에서 Trend Micro 보안 확장을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-118">The [Azure portal](http://portal.azure.com) lets you install the Trend Micro security extension when you use an image from the **Marketplace** to create the virtual machine.</span></span> <span data-ttu-id="40f6c-119">포털을 사용하면 단일 가상 컴퓨터를 만들 때 Trend Micro의 보호 기능을 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-119">If you're creating a single virtual machine, using the portal is an easy way to add protection from Trend Micro.</span></span>

<span data-ttu-id="40f6c-120">**Marketplace**의 항목을 사용하면 가상 컴퓨터 설치에 도움이 되는 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-120">Using an entry from the **Marketplace** opens a wizard that helps you set up the virtual machine.</span></span> <span data-ttu-id="40f6c-121">마법사의 세 번째 패널인 **설정** 블레이드를 사용하여 Trend Micro 보안 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-121">You use the **Settings** blade, the third panel of the wizard, to install the Trend Micro security extension.</span></span>  <span data-ttu-id="40f6c-122">일반적인 지침은 [Azure Portal에서 Windows를 실행하는 가상 컴퓨터 만들기](tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40f6c-122">For general instructions, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>

<span data-ttu-id="40f6c-123">마법사의 **설정** 블레이드로 이동한 후 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-123">When you get to the **Settings** blade of the wizard, do the following steps:</span></span>

1. <span data-ttu-id="40f6c-124">**확장**을 클릭한 후 다음 창에서 **확장 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-124">Click **Extensions**, then click **Add extension** in the next pane.</span></span>

   ![확장 추가 시작][1]

2. <span data-ttu-id="40f6c-126">**새 리소스** 창에서 **Deep Security Agent**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-126">Select **Deep Security Agent** in the **New resource** pane.</span></span> <span data-ttu-id="40f6c-127">Deep Security Agent 창에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-127">In the Deep Security Agent pane, click **Create**.</span></span>

   ![Deep Security Agent 식별][2]

3. <span data-ttu-id="40f6c-129">확장에 대한 **테넌트 식별자** 및 **테넌트 활성화 암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-129">Enter the **Tenant Identifier** and **Tenant Activation Password** for the extension.</span></span> <span data-ttu-id="40f6c-130">선택적으로 **보안 정책 식별자**를 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="40f6c-131">그런 후 **확인**을 클릭하여 클라이언트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-131">Then, click **OK** to add the client.</span></span>

   ![확장 세부 정보 제공][3]

## <a name="install-the-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="40f6c-133">기존 VM에 Deep Security Agent 설치</span><span class="sxs-lookup"><span data-stu-id="40f6c-133">Install the Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="40f6c-134">기존 VM에 에이전트를 설치하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-134">To install the agent on an existing VM, you need the following items:</span></span>

* <span data-ttu-id="40f6c-135">Azure PowerShell 모듈 버전 0.8.2 이상이 로컬 컴퓨터에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-135">The Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="40f6c-136">**Get-Module azure | format-table version** 명령을 사용하여 설치한 Azure PowerShell 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-136">You can check the version of Azure PowerShell that you have installed by using the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="40f6c-137">지침 및 최신 버전에 대한 링크를 보려면 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40f6c-137">For instructions and a link to the latest version, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="40f6c-138">`Add-AzureAccount`를 사용하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-138">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="40f6c-139">VM 에이전트가 대상 가상 컴퓨터에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-139">The VM Agent installed on the target virtual machine.</span></span>

<span data-ttu-id="40f6c-140">먼저 VM 에이전트가 이미 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-140">First, verify that the VM Agent is already installed.</span></span> <span data-ttu-id="40f6c-141">클라우드 서비스 이름과 가상 컴퓨터 이름을 입력하고 관리자 수준의 Azure PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-141">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="40f6c-142">< 및 > 문자를 포함하여 따옴표 안의 모든 항목을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-142">Replace everything within the quotes, including the < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="40f6c-143">클라우드 서비스 및 가상 컴퓨터 이름을 모르는 경우 **Get-AzureVM** 을 실행하여 현재 구독의 모든 가상 컴퓨터에 대한 해당 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-143">If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.</span></span>

<span data-ttu-id="40f6c-144">**write-host** 명령에서 **True**가 반환되면 VM 에이전트가 설치되어 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-144">If the **write-host** command returns **True**, the VM Agent is installed.</span></span> <span data-ttu-id="40f6c-145">**False**가 반환되면 Azure 블로그 게시물 [VM 에이전트 및 확장 - 2부](http://go.microsoft.com/fwlink/p/?LinkId=403947)에서 지침 및 다운로드 링크를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-145">If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="40f6c-146">VM 에이전트가 설치되어 있는 경우 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-146">If the VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="40f6c-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40f6c-147">Next steps</span></span>
<span data-ttu-id="40f6c-148">에이전트가 설치되어 있는 경우 실행을 시작하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-148">It takes a few minutes for the agent to start running when it is installed.</span></span> <span data-ttu-id="40f6c-149">그 이후에는 Deep Security Manager를 통해 관리할 수 있도록 가상 컴퓨터에서 Deep Security를 정품 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40f6c-149">After that, you need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="40f6c-150">추가 지침은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40f6c-150">See the following articles for additional instructions:</span></span>

* <span data-ttu-id="40f6c-151">이 솔루션과 관련된 Trend 문서, [Microsoft Azure에 대한 즉시 재생 가능한 클라우드 보안](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="40f6c-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="40f6c-152">가상 컴퓨터 구성을 위한 [샘플 Windows PowerShell 스크립트](http://go.microsoft.com/fwlink/?LinkId=404100)</span><span class="sxs-lookup"><span data-stu-id="40f6c-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine</span></span>
* <span data-ttu-id="40f6c-153">[지침](http://go.microsoft.com/fwlink/?LinkId=404099) </span><span class="sxs-lookup"><span data-stu-id="40f6c-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for the sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40f6c-154">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="40f6c-154">Additional resources</span></span>
<span data-ttu-id="40f6c-155">[Windows Server를 실행하는 가상 컴퓨터에 로그온하는 방법]</span><span class="sxs-lookup"><span data-stu-id="40f6c-155">[How to log on to a virtual machine running Windows Server]</span></span>

<span data-ttu-id="40f6c-156">[Azure VM 확장 및 기능]</span><span class="sxs-lookup"><span data-stu-id="40f6c-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
<span data-ttu-id="40f6c-157">[Windows Server를 실행하는 가상 컴퓨터에 로그온하는 방법]:connect-logon.md</span><span class="sxs-lookup"><span data-stu-id="40f6c-157">[How to log on to a virtual machine running Windows Server]:connect-logon.md</span></span>
<span data-ttu-id="40f6c-158">[Azure VM 확장 및 기능]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="40f6c-158">[Azure VM Extensions and features]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span></span>
