---
title: "VM에서 추세 Micro Deep Security aaaInstall | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooinstall 및 Azure의 hello 클래식 배포 모델을 사용 하 여 만든 VM에서 Trend Micro 보안을 구성 합니다."
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
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="f9608-103">어떻게 tooinstall 및 서비스로 Windows VM에서 Trend Micro Deep Security 구성</span><span class="sxs-lookup"><span data-stu-id="f9608-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f9608-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f9608-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f9608-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="f9608-107">이 문서에서는 어떻게 tooinstall 및 Trend Micro Deep Security를 서비스로 실행 하는 새로운 또는 기존 가상 컴퓨터 (VM) Windows Server에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="f9608-108">Deep Security as a Service는 맬웨어 방지 보호, 방화벽, 침입 방지 시스템 및 무결성 모니터링을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="f9608-109">hello 클라이언트 hello VM 에이전트를 통해 보안 확장 프로그램으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="f9608-110">새 가상 컴퓨터에 설치한 hello Deep Security Agent로 hello hello Azure 포털에서 VM 에이전트를 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="f9608-111">Hello 클래식 포털, hello Azure CLI 또는 PowerShell을 사용 하 여 만든 기존 VM에 VM 에이전트가 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="f9608-112">VM 에이전트 hello이 없는 기존 가상 컴퓨터에 대 한 toodownload 필요한 및 앱을 먼저 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="f9608-113">이 문서에서는 두 상황을 모두 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-113">This article covers both situations.</span></span>

<span data-ttu-id="f9608-114">온-프레미스 솔루션에 대 한 Trend Micro에서 현재 구독을 보유 하는 경우 파일을 사용할 수 toohelp Azure 가상 컴퓨터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="f9608-115">아직 구독 고객이 아닌 경우에는 평가판 구독에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="f9608-116">이 솔루션에 대 한 자세한 내용은 hello Trend Micro 블로그 게시물을 참조 하십시오. [Microsoft Azure VM 에이전트 확장에 대 한 전체 보안](http://go.microsoft.com/fwlink/p/?LinkId=403945)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="f9608-117">새 VM에 hello Deep Security Agent를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="f9608-118">hello [Azure 포털](http://portal.azure.com) hello에서 이미지를 사용 하는 경우 hello Trend Micro 보안 확장 프로그램을 설치 하면 **마켓플레이스** toocreate hello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="f9608-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="f9608-119">단일 가상 컴퓨터를 만드는 경우 hello 포털을 사용 하 여은 Trend Micro에서 쉽게 tooadd 보호 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="f9608-120">Hello에서 항목을 사용 하 여 **마켓플레이스** hello 가상 컴퓨터를 설정 하는 데 도움이 되는 마법사를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="f9608-121">Hello를 사용 하 여 **설정을** 블레이드, hello hello 마법사, tooinstall hello Trend Micro 보안 확장 프로그램의 세 번째 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="f9608-122">일반 지침은 [hello Azure 포털에서에서 Windows를 실행 중인 가상 컴퓨터를 만드는](tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="f9608-123">Toohello를 가져올 때 **설정을** 블레이드 hello 마법사의 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="f9608-124">클릭 **확장**, 클릭 **확장 추가** hello 다음 창에서.</span><span class="sxs-lookup"><span data-stu-id="f9608-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Hello 확장을 추가 하기 시작][1]

2. <span data-ttu-id="f9608-126">선택 **Deep Security Agent** hello에 **새 리소스** 창.</span><span class="sxs-lookup"><span data-stu-id="f9608-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="f9608-127">Hello Deep Security Agent 창에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Deep Security Agent 식별][2]

3. <span data-ttu-id="f9608-129">Hello 입력 **테 넌 트 식별자** 및 **테 넌 트 활성화 암호** hello 확장에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="f9608-130">선택적으로 **보안 정책 식별자**를 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="f9608-131">클릭 **확인** tooadd hello 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-131">Then, click **OK** tooadd hello client.</span></span>

   ![확장 세부 정보 제공][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="f9608-133">기존 VM에 hello Deep Security Agent를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="f9608-134">기존 VM에 tooinstall hello 에이전트, 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="f9608-135">hello Azure PowerShell 모듈, 0.8.2 버전 또는 최신, 로컬 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="f9608-136">Hello hello를 사용 하 여 설치 된 Azure PowerShell 버전을 확인할 수 있습니다 **Get-module azure | format-table 버전** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="f9608-137">지침 및 링크 toohello 최신 버전에 대 한 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="f9608-138">사용 하 여 Azure 구독 tooyour `Add-AzureAccount`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="f9608-139">hello VM 에이전트를 hello 대상 가상 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="f9608-140">첫째, VM 에이전트가 이미 설치 되어 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="f9608-141">Hello 클라우드 서비스 이름 및 가상 컴퓨터 이름을 입력 한 후 hello 다음 관리자 권한 Azure PowerShell 명령 프롬프트에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="f9608-142">Hello < 및 > 문자를 포함 하 여 hello 인용 부호 있는 모든 항목을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="f9608-143">Hello 클라우드 서비스 및 가상 컴퓨터 이름을 모르는 경우 실행 **Get-azurevm** hello 현재 구독에서 가상 컴퓨터를 모두에 대 한 정보는 toodisplay 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="f9608-144">경우 hello **쓰기 호스트** 명령에서 반환 **True**, hello VM 에이전트가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="f9608-145">반환 하는 경우 **False**, hello 지침 및 다운로드 hello Azure 블로그 게시물에서에서 링크 toohello 참조 [VM 에이전트 및 확장-2 부](http://go.microsoft.com/fwlink/p/?LinkId=403947)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="f9608-146">Hello VM 에이전트가 설치 된 경우 다음이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="f9608-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9608-147">Next steps</span></span>
<span data-ttu-id="f9608-148">Hello 에이전트 toostart 설치 될 때 실행에 대 한 몇 가지 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="f9608-149">그 후 전체 보안 관리자가 관리할 수 있도록 tooactivate Deep Security hello 가상 컴퓨터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9608-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="f9608-150">다음 추가 지침에 대 한 아티클을 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="f9608-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="f9608-151">이 솔루션과 관련된 Trend 문서, [Microsoft Azure에 대한 즉시 재생 가능한 클라우드 보안](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="f9608-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="f9608-152">A [샘플 Windows PowerShell 스크립트](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="f9608-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="f9608-153">[지침](http://go.microsoft.com/fwlink/?LinkId=404099) hello 샘플에 대 한</span><span class="sxs-lookup"><span data-stu-id="f9608-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9608-154">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f9608-154">Additional resources</span></span>
<span data-ttu-id="f9608-155">[어떻게 toolog Windows Server를 실행 tooa 가상 컴퓨터]</span><span class="sxs-lookup"><span data-stu-id="f9608-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="f9608-156">[Azure VM 확장 및 기능]</span><span class="sxs-lookup"><span data-stu-id="f9608-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[어떻게 toolog Windows Server를 실행 tooa 가상 컴퓨터]:connect-logon.md
[Azure VM 확장 및 기능]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
