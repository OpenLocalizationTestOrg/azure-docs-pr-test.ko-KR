---
title: "Azure Automation DSC를 통한 관리를 위한 컴퓨터 온보드 | Microsoft Docs"
description: "Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 설정 방법"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: cc9b1ea19b4e17374d47e12f970cb333a8051559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a><span data-ttu-id="9c493-103">Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드</span><span class="sxs-lookup"><span data-stu-id="9c493-103">Onboarding machines for management by Azure Automation DSC</span></span>

## <a name="why-manage-machines-with-azure-automation-dsc"></a><span data-ttu-id="9c493-104">Azure 자동화 DSC로 컴퓨터를 관리하는 이유</span><span class="sxs-lookup"><span data-stu-id="9c493-104">Why manage machines with Azure Automation DSC?</span></span>

<span data-ttu-id="9c493-105">[PowerShell 필요 상태 구성](https://technet.microsoft.com/library/dn249912.aspx)과 마찬가지로 Azure 자동화 필요 상태 구성은 클라우드나 온-프레미스 데이터 센터의 DSC 노드(물리적 및 가상 컴퓨터)를 위한 간단하지만 강력한 구성 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-105">Like [PowerShell Desired State Configuration](https://technet.microsoft.com/library/dn249912.aspx), Azure Automation Desired State Configuration is a simple, yet powerful, configuration management service for DSC nodes (physical and virtual machines) in any cloud or on-premises datacenter.</span></span> <span data-ttu-id="9c493-106">안전한 중앙 위치에서 수천 대의 컴퓨터를 빠르고 간편하게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-106">It enables scalability across thousands of machines quickly and easily from a central, secure location.</span></span> <span data-ttu-id="9c493-107">컴퓨터를 쉽게 온보드하고, 컴퓨터에 선언적 구성을 할당하고, 사용자가 지정한 필요 상태에 대한 각 컴퓨터의 규정 준수를 나타내는 보고서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-107">You can easily onboard machines, assign them declarative configurations, and view reports showing each machine's compliance to the desired state you specified.</span></span> <span data-ttu-id="9c493-108">Azure 자동화 관리 계층이 PowerShell 스크립팅에 대한 것이라면 Azure 자동화 DSC 관리 계층은 DSC에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-108">The Azure Automation DSC management layer is to DSC what the Azure Automation management layer is to PowerShell scripting.</span></span> <span data-ttu-id="9c493-109">즉, Azure 자동화에서 PowerShell 스크립트 관리를 지원하는 동일한 방법으로 DSC 구성 관리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-109">In other words, in the same way that Azure Automation helps you manage PowerShell scripts, it also helps you manage DSC configurations.</span></span> <span data-ttu-id="9c493-110">Azure 자동화 DSC를 사용할 경우의 이점에 대한 자세한 내용은 [Azure 자동화 DSC 개요](automation-dsc-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c493-110">To learn more about the benefits of using Azure Automation DSC, see [Azure Automation DSC overview](automation-dsc-overview.md).</span></span>

<span data-ttu-id="9c493-111">Azure 자동화 DSC를 다양한 컴퓨터의 관리에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-111">Azure Automation DSC can be used to manage a variety of machines:</span></span>

* <span data-ttu-id="9c493-112">Azure 가상 컴퓨터(기본)</span><span class="sxs-lookup"><span data-stu-id="9c493-112">Azure virtual machines (classic)</span></span>
* <span data-ttu-id="9c493-113">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9c493-113">Azure virtual machines</span></span>
* <span data-ttu-id="9c493-114">AWS(Amazon Web Services) 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9c493-114">Amazon Web Services (AWS) virtual machines</span></span>
* <span data-ttu-id="9c493-115">온-프레미스나 Azure/AWS 이외의 클라우드에 있는 실제/가상 Windows 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9c493-115">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>
* <span data-ttu-id="9c493-116">온-프레미스, Azure 또는 Azure 이외의 클라우드에 있는 실제/가상 Linux 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9c493-116">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="9c493-117">또한 클라우드에서 컴퓨터 구성을 관리할 수 없는 경우 Azure 자동화 DSC는 보고서 전용 끝점으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-117">In addition, if you are not ready to manage machine configuration from the cloud, Azure Automation DSC can also be used as a report-only endpoint.</span></span> <span data-ttu-id="9c493-118">이 옵션을 사용하면 DSC 온-프레미스를 통해 원하는 구성을 설정(푸시)하고 Azure 자동화에서 원하는 상태로 노드 준수에서 다양하게 보고하는 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-118">This allows you to set (push) desired configuration through DSC on-premises and view rich reporting details on node compliance with the desired state in Azure Automation.</span></span>

<span data-ttu-id="9c493-119">다음 섹션에서는 Azure 자동화 DSC에 대해 각 컴퓨터 형식을 온보드하는 방법을 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-119">The following sections outline how you can onboard each type of machine to Azure Automation DSC.</span></span>

## <a name="azure-virtual-machines-classic"></a><span data-ttu-id="9c493-120">Azure 가상 컴퓨터(기본)</span><span class="sxs-lookup"><span data-stu-id="9c493-120">Azure virtual machines (classic)</span></span>

<span data-ttu-id="9c493-121">Azure 자동화 DSC를 사용하면 Azure 포털이나 PowerShell을 사용하는 구성 관리를 위해 Azure 가상 컴퓨터(기본)를 간편하게 온보드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-121">With Azure Automation DSC, you can easily onboard Azure virtual machines (classic) for configuration management using either the Azure portal, or PowerShell.</span></span> <span data-ttu-id="9c493-122">내부적으로, VM에 대한 관리자의 원격 작업 없이 Azure VM 필요 상태 구성 확장이 VM을 Azure 자동화 DSC에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-122">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="9c493-123">Azure VM 필요 상태 구성 확장은 비동기적으로 실행되므로 진행 상황을 추적하거나 문제를 해결하기 위한 절차는 아래의 [**Azure 가상 컴퓨터 온보드 문제 해결**](#troubleshooting-azure-virtual-machine-onboarding) 섹션에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-123">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="9c493-124">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9c493-124">Azure portal</span></span>

<span data-ttu-id="9c493-125">[Azure Portal](http://portal.azure.com/)에서 **찾아보기** -> **가상 컴퓨터(클래식)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-125">In the [Azure portal](http://portal.azure.com/), click **Browse** -> **Virtual machines (classic)**.</span></span> <span data-ttu-id="9c493-126">온보드할 Windows VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-126">Select the Windows VM you want to onboard.</span></span> <span data-ttu-id="9c493-127">가상 컴퓨터의 대시보드 블레이드에서 **모든 설정** -> **확장** -> **추가** -> **Azure 자동화 DSC** -> **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-127">On the virtual machine's dashboard blade, click **All settings** -> **Extensions** -> **Add** -> **Azure Automation DSC** -> **Create**.</span></span> <span data-ttu-id="9c493-128">사용 사례에 필요한 [PowerShell DSC 로컬 구성 관리자 값](https://msdn.microsoft.com/powershell/dsc/metaconfig4), 자동화 계정의 등록 키 및 등록 URL과, 선택적으로 VM에 할당할 노드 구성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-128">Enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, your Automation account's registration key and registration URL, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

<span data-ttu-id="9c493-129">컴퓨터를 온보드하기 위해 자동화 계정에 대한 등록 URL과 키를 찾으려면 아래의 [**등록 보호**](#secure-registration) 섹션에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-129">To find the registration URL and key for the Automation account to onboard the machine to, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="9c493-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c493-130">PowerShell</span></span>

```powershell
# log in to both Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in the name of a Node Configuration in Azure Automation DSC, for this VM to conform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use the DSC extension to onboard the VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a><span data-ttu-id="9c493-131">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9c493-131">Azure virtual machines</span></span>

<span data-ttu-id="9c493-132">Azure 자동화 DSC를 사용하면 Azure 포털, Azure 리소스 관리자 템플릿 또는 PowerShell을 사용하는 구성 관리를 위해 Azure 가상 컴퓨터를 간편하게 온보드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-132">Azure Automation DSC lets you easily onboard Azure virtual machines for configuration management, using either the Azure portal, Azure Resource Manager templates, or PowerShell.</span></span> <span data-ttu-id="9c493-133">내부적으로, VM에 대한 관리자의 원격 작업 없이 Azure VM 필요 상태 구성 확장이 VM을 Azure 자동화 DSC에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-133">Under the hood, and without an administrator having to remote into the VM, the Azure VM Desired State Configuration extension registers the VM with Azure Automation DSC.</span></span> <span data-ttu-id="9c493-134">Azure VM 필요 상태 구성 확장은 비동기적으로 실행되므로 진행 상황을 추적하거나 문제를 해결하기 위한 절차는 아래의 [**Azure 가상 컴퓨터 온보드 문제 해결**](#troubleshooting-azure-virtual-machine-onboarding) 섹션에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-134">Since the Azure VM Desired State Configuration extension runs asynchronously, steps to track its progress or troubleshoot it are provided in the [**Troubleshooting Azure virtual machine onboarding**](#troubleshooting-azure-virtual-machine-onboarding) section below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="9c493-135">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9c493-135">Azure portal</span></span>

<span data-ttu-id="9c493-136">[Azure 포털](https://portal.azure.com/)에서 가상 컴퓨터를 온보드할 Azure 자동화 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-136">In the [Azure portal](https://portal.azure.com/), navigate to the Azure Automation account where you want to onboard virtual machines.</span></span> <span data-ttu-id="9c493-137">자동화 계정 대시보드에서 **DSC 노드** -> **Azure VM 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-137">On the Automation account dashboard, click **DSC Nodes** -> **Add Azure VM**.</span></span>

<span data-ttu-id="9c493-138">**온보드할 가상 컴퓨터 선택**에서 온보드할 하나 이상의 Azure 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-138">Under **Select virtual machines to onboard**, select one or more Azure virtual machines to onboard.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

<span data-ttu-id="9c493-139">**등록 데이터 구성**에서 사용 사례에 필요한 [PowerShell DSC 로컬 구성 관리자 값](https://msdn.microsoft.com/powershell/dsc/metaconfig4) 과, 선택적으로 VM에 할당할 노드 구성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-139">Under **Configure registration data**, enter the [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) required for your use case, and optionally a node configuration to assign to the VM.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="9c493-140">Azure 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="9c493-140">Azure Resource Manager templates</span></span>

<span data-ttu-id="9c493-141">Azure 가상 컴퓨터는 Azure 리소스 관리자 템플릿을 통해 Azure 자동화 DSC에 배포 및 온보드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-141">Azure virtual machines can be deployed and onboarded to Azure Automation DSC via Azure Resource Manager templates.</span></span> <span data-ttu-id="9c493-142">기존 VM을 Azure 자동화 DSC에 온보드하는 템플릿 예는 [DSC 확장 및 Azure 자동화 DSC를 통한 VM 구성](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c493-142">See [Configure a VM via DSC extension and Azure Automation DSC](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) for an example template that onboards an existing VM to Azure Automation DSC.</span></span> <span data-ttu-id="9c493-143">이 템플릿에서 입력으로 가져온 등록 키와 등록 URL을 찾으려면 아래의 [**등록 보호**](#secure-registration) 섹션에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-143">To find the registration key and registration URL taken as input in this template, see the [**Secure registration**](#secure-registration) section below.</span></span>

### <a name="powershell"></a><span data-ttu-id="9c493-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c493-144">PowerShell</span></span>

<span data-ttu-id="9c493-145">PowerShell을 통해 Azure 포털의 가상 컴퓨터를 온보드하는 데 [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-145">The [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet can be used to onboard virtual machines in the Azure portal via PowerShell.</span></span>

## <a name="amazon-web-services-aws-virtual-machines"></a><span data-ttu-id="9c493-146">AWS(Amazon Web Services) 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9c493-146">Amazon Web Services (AWS) virtual machines</span></span>

<span data-ttu-id="9c493-147">AWS DSC 도구 키트를 사용하여 Azure 자동화 DSC에 의한 구성 관리를 위해 Amazon Web Services 가상 컴퓨터를 쉽게 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-147">You can easily onboard Amazon Web Services virtual machines for configuration management by Azure Automation DSC using the AWS DSC Toolkit.</span></span> <span data-ttu-id="9c493-148">이러한 도구 키트에 대한 자세한 내용은 [여기](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-148">You can learn more about the toolkit [here](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).</span></span>

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a><span data-ttu-id="9c493-149">온-프레미스나 Azure/AWS 이외의 클라우드에 있는 실제/가상 Windows 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9c493-149">Physical/virtual Windows machines on-premises, or in a cloud other than Azure/AWS</span></span>

<span data-ttu-id="9c493-150">온-프레미스 Windows 컴퓨터와 비 Azure 클라우드(예: Amazon Web Services)의 Windows 컴퓨터도 인터넷에 대한 아웃바운드 액세스 권한이 있다면 Azure 자동화 DSC에 간단한 절차를 통해 온보드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-150">On-premises Windows machines and Windows machines in non-Azure clouds (such as Amazon Web Services) can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="9c493-151">최신 버전의 [WMF 5](http://aka.ms/wmf5latest) 가 Azure 자동화 DSC에 온보드하려는 컴퓨터에 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-151">Make sure the latest version of [WMF 5](http://aka.ms/wmf5latest) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="9c493-152">아래 [**DSC 메타 구성 생성**](#generating-dsc-metaconfigurations) 섹션의 지침에 따라 필요한 DSC 메타 구성을 포함하는 폴더를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-152">Follow the directions in section [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) below to generate a folder containing the needed DSC metaconfigurations.</span></span>
3. <span data-ttu-id="9c493-153">등록할 컴퓨터에 PowerShell DSC 메타 구성을 원격으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-153">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard.</span></span> <span data-ttu-id="9c493-154">**이 명령이 실행되는 컴퓨터에는 최신 버전의 [WMF 5](http://aka.ms/wmf5latest) 가 설치되어 있어야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9c493-154">**The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed**:</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. <span data-ttu-id="9c493-155">PowerShell DSC 메타 구성을 원격으로 적용할 수 없는 경우 2단계의 메타 구성 폴더를 등록할 각 컴퓨터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-155">If you cannot apply the PowerShell DSC metaconfigurations remotely, copy the metaconfigurations folder from step 2 onto each machine to onboard.</span></span> <span data-ttu-id="9c493-156">그런 다음 등록할 각 컴퓨터에서 **Set-DscLocalConfigurationManager** 를 로컬로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-156">Then call **Set-DscLocalConfigurationManager** locally on each machine to onboard.</span></span>
5. <span data-ttu-id="9c493-157">Azure 포털 또는 cmdlet를 사용하여 Azure 자동화 계정에서 등록된 DSC 노드로 온보드할 컴퓨터가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-157">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a><span data-ttu-id="9c493-158">온-프레미스, Azure 또는 Azure 이외의 클라우드에 있는 실제/가상 Linux 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9c493-158">Physical/virtual Linux machines on-premises, in Azure, or in a cloud other than Azure</span></span>

<span data-ttu-id="9c493-159">온-프레미스 Linux 컴퓨터, Azure의 Linux 컴퓨터 및 비 Azure 클라우드의 Linux 컴퓨터 또한  몇 가지 간단한 절차를 통해 인터넷으로의 아웃 바운드 액세스 권한만큼 Azure 자동화 DSC에 온보드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-159">On-premises Linux machines, Linux machines in Azure, and Linux machines in non-Azure clouds can also be onboarded to Azure Automation DSC, as long as they have outbound access to the internet, via a few simple steps:</span></span>

1. <span data-ttu-id="9c493-160">최신 버전의 [Linux용 PowerShell DSC(필요한 상태 구성)](https://github.com/Microsoft/PowerShell-DSC-for-Linux)가 Azure Automation DSC에 온보딩하려는 컴퓨터에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-160">Make sure the latest version of [PowerShell Desired State Configuration for Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) is installed on the machines you want to onboard to Azure Automation DSC.</span></span>
2. <span data-ttu-id="9c493-161">[PowerShell DSC 로컬 구성 관리자 기본값](https://msdn.microsoft.com/powershell/dsc/metaconfig4) 이 해당 사용 사례와 일치하는 경우 Azure 자동화 DSC에서 끌어오고 보고하는 **모든** 컴퓨터를 등록하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-161">If the [PowerShell DSC Local Configuration Manager defaults](https://msdn.microsoft.com/powershell/dsc/metaconfig4) match your use case, and you want to onboard machines such that they **both** pull from and report to Azure Automation DSC:</span></span>

   + <span data-ttu-id="9c493-162">Azure 자동화 DSC에 온보드할 각 Linux 컴퓨터에서 PowerShell DSC 로컬 구성 관리자 기본값으로 Register.py를 사용하여 온보드합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-162">On each Linux machine to onboard to Azure Automation DSC, use Register.py to onboard using the PowerShell DSC Local Configuration Manager defaults:</span></span>

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + <span data-ttu-id="9c493-163">자동화 계정에 대한 등록 키와 등록 URL을 확인하려면 아래의 [**등록 보호**](#secure-registration) 섹션에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-163">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>

     <span data-ttu-id="9c493-164">PowerShell DSC 로컬 구성 관리자 기본값이 해당 사용 사례와 일치**하지** **않거나** Azure 자동화 DSC에 보고하지만 구성 또는 PowerShell 모듈을 끌어오지 않는 컴퓨터를 등록하려면 3-6단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-164">If the PowerShell DSC Local Configuration Manager defaults **do** **not** match your use case, or you want to onboard machines such that they only report to Azure Automation DSC, but do not pull configuration or PowerShell modules from it,  follow steps 3 - 6.</span></span> <span data-ttu-id="9c493-165">그렇지 않으면 6단계로 직접 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-165">Otherwise, proceed directly to step 6.</span></span>

3. <span data-ttu-id="9c493-166">아래 [**DSC 메타 구성 생성**](#generating-dsc-metaconfigurations) 섹션의 지침에 따라 필요한 DSC 메타 구성을 포함하는 폴더를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-166">Follow the directions in the [**Generating DSC metaconfigurations**](#generating-dsc-metaconfigurations) section below to generate a folder containing the needed DSC metaconfigurations.</span></span>
4. <span data-ttu-id="9c493-167">온보드할 컴퓨터에 PowerShell DSC 메타 구성을 원격으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-167">Remotely apply the PowerShell DSC metaconfiguration to the machines you want to onboard:</span></span>

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine to onboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

<span data-ttu-id="9c493-168">이 명령이 실행되는 컴퓨터에는 최신 버전의 [WMF 5](http://aka.ms/wmf5latest) 가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-168">The machine this command is run from must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>

1. <span data-ttu-id="9c493-169">PowerShell DSC 메타 구성을 원격으로 적용할 수 없는 경우 온보드할 각 Linux 컴퓨터에 대해 5단계의 폴더에서 해당 컴퓨터에 대한 메타 구성을 Linux 컴퓨터에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-169">If you cannot apply the PowerShell DSC metaconfigurations remotely, for each Linux machine to onboard, copy the metaconfiguration corresponding to that machine from the folder in step 5 onto the Linux machine.</span></span> <span data-ttu-id="9c493-170">그런 다음 Azure 자동화 DSC에 온보드할 각 Linux 컴퓨터에서 로컬로 `SetDscLocalConfigurationManager.py` 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-170">Then call `SetDscLocalConfigurationManager.py` locally on each Linux machine you want to onboard to Azure Automation DSC:</span></span>

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path to metaconfiguration file>`

2. <span data-ttu-id="9c493-171">Azure 포털 또는 cmdlet를 사용하여 Azure 자동화 계정에서 등록된 DSC 노드로 온보드할 컴퓨터가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-171">Using the Azure portal or cmdlets, check that the machines to onboard now show up as DSC nodes registered in your Azure Automation account.</span></span>

## <a name="generating-dsc-metaconfigurations"></a><span data-ttu-id="9c493-172">DSC 메타 구성 생성</span><span class="sxs-lookup"><span data-stu-id="9c493-172">Generating DSC metaconfigurations</span></span>

<span data-ttu-id="9c493-173">일반적으로 컴퓨터를 Azure Automation DSC에 등록하려면 [DSC 메타 구성](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig)은 적용될 때 생성될 수 있으며 컴퓨터의 DSC 에이전트가 Azure Automation DSC에서 끌어오거나 보고하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-173">To generically onboard any machine to Azure Automation DSC, a [DSC metaconfiguration](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) can be generated that, when applied, tells the DSC agent on the machine to pull from and/or report to Azure Automation DSC.</span></span> <span data-ttu-id="9c493-174">Azure 자동화 DSC에 대한 DSC 메타 구성은 PowerShell DSC 구성 또는 Azure 자동화 PowerShell cmdlet을 사용하여 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-174">DSC metaconfigurations for Azure Automation DSC can be generated using either a PowerShell DSC configuration, or the Azure Automation PowerShell cmdlets.</span></span>

> [!NOTE]
> <span data-ttu-id="9c493-175">DSC 메타 구성은 관리를 위해 자동화 계정에 컴퓨터를 등록하는 데 필요한 암호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-175">DSC metaconfigurations contain the secrets needed to onboard a machine to an Automation account for management.</span></span> <span data-ttu-id="9c493-176">사용한 후에 만들거나 삭제한 DSC 메타 구성을 제대로 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-176">Make sure to properly protect any DSC metaconfigurations you create, or delete them after use.</span></span>

### <a name="using-a-dsc-configuration"></a><span data-ttu-id="9c493-177">DSC 구성 사용</span><span class="sxs-lookup"><span data-stu-id="9c493-177">Using a DSC Configuration</span></span>

1. <span data-ttu-id="9c493-178">로컬 환경의 컴퓨터에서 관리자 권한으로 PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-178">Open the PowerShell ISE as an administrator in a machine in your local environment.</span></span> <span data-ttu-id="9c493-179">이 컴퓨터에는 최신 버전의 [WMF 5](http://aka.ms/wmf5latest) 가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-179">The machine must have the latest version of [WMF 5](http://aka.ms/wmf5latest) installed.</span></span>
2. <span data-ttu-id="9c493-180">다음 스크립트를 로컬로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-180">Copy the following script locally.</span></span> <span data-ttu-id="9c493-181">이 스크립트는 메타 구성을 만들기 위한 PowerShell DSC 구성 및 메타 구성 생성을 시작하는 명령을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-181">This script contains a PowerShell DSC configuration for creating metaconfigurations, and a command to kick off the metaconfiguration creation.</span></span>

    ```powershell
    # The DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create the metaconfigurations
    # TODO: edit the below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM to onboard>', '<some other VM to onboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set to $True to have machines only report to AA DSC but not pull from it
    }

    # Use PowerShell splatting to pass parameters to the DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. <span data-ttu-id="9c493-182">등록할 컴퓨터의 이름 뿐만 아니라 자동화 계정에 대한 등록 키 및 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-182">Fill in the registration key and URL for your Automation account, as well as the names of the machines to onboard.</span></span> <span data-ttu-id="9c493-183">모든 다른 매개 변수는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-183">All other parameters are optional.</span></span> <span data-ttu-id="9c493-184">자동화 계정에 대한 등록 키와 등록 URL을 확인하려면 아래의 [**등록 보호**](#secure-registration) 섹션에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-184">To find the registration key and registration URL for your Automation account, see the [**Secure registration**](#secure-registration) section below.</span></span>
4. <span data-ttu-id="9c493-185">컴퓨터가 Azure 자동화 DSC에 DSC 상태 정보를 보고하지만 구성 또는 PowerShell 모듈을 끌어오지 않도록 하려면 **ReportOnly** 매개 변수를 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-185">If you want the machines to report DSC status information to Azure Automation DSC, but not pull configuration or PowerShell modules, set the **ReportOnly** parameter to true.</span></span>
5. <span data-ttu-id="9c493-186">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-186">Run the script.</span></span> <span data-ttu-id="9c493-187">이제 작업 디렉터리에 **DscMetaConfigs**라는 폴더가 있어야 하며 이는 등록할 컴퓨터에 대한 PowerShell DSC 메타 구성을 포함합니다(관리자로).</span><span class="sxs-lookup"><span data-stu-id="9c493-187">You should now have a folder called **DscMetaConfigs** in your working directory, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-the-azure-automation-cmdlets"></a><span data-ttu-id="9c493-188">Azure 자동화 cmdlet 사용</span><span class="sxs-lookup"><span data-stu-id="9c493-188">Using the Azure Automation cmdlets</span></span>

<span data-ttu-id="9c493-189">PowerShell DSC 로컬 구성 관리자 기본값이 해당 사용 사례와 일치하는 경우 Azure 자동화 DSC에서 끌어오고 보고하는 모든 컴퓨터를 등록하려 합니다. Azure 자동화 cmdlet은 필요한 DSC 메타 구성을 생성하는 단순화된 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-189">If the PowerShell DSC Local Configuration Manager defaults match your use case, and you want to onboard machines such that they both pull from and report to Azure Automation DSC, the Azure Automation cmdlets provide a simplified method of generating the DSC metaconfigurations needed:</span></span>

1. <span data-ttu-id="9c493-190">로컬 환경의 컴퓨터에서 관리자 권한으로 PowerShell 콘솔이나 PowerShell ISE를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-190">Open the PowerShell console or PowerShell ISE as an administrator in a machine in your local environment.</span></span>
2. <span data-ttu-id="9c493-191">**Add-AzureRmAccount**</span><span class="sxs-lookup"><span data-stu-id="9c493-191">Connect to Azure Resource Manager using **Add-AzureRmAccount**</span></span>
3. <span data-ttu-id="9c493-192">노드를 등록하려는 자동화 계정에서 등록하려 컴퓨터에 대한 PowerShell DSC 메타 구성을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-192">Download the PowerShell DSC metaconfigurations for the machines you want to onboard from the Automation account to which you want to onboard nodes:</span></span>

    ```powershell
    # Define the parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # The name of the ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # The name of the Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # The names of the computers that the meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting to pass parameters to the Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. <span data-ttu-id="9c493-193">이제 ***DscMetaConfigs***라는 폴더가 있어야 하며 이는 등록할 컴퓨터에 대한 PowerShell DSC 메타 구성을 포함합니다(관리자로).</span><span class="sxs-lookup"><span data-stu-id="9c493-193">You should now have a folder called ***DscMetaConfigs***, containing the PowerShell DSC metaconfigurations for the machines to onboard (as an administrator):</span></span>
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a><span data-ttu-id="9c493-194">등록 보호</span><span class="sxs-lookup"><span data-stu-id="9c493-194">Secure registration</span></span>

<span data-ttu-id="9c493-195">PowerShell DSC 풀 또는 보고 서버(Azure 자동화 DSC 포함)에 대한 DSC 노드 인증을 허용하는 V2WMF 5 DSC 등록 프로토콜을 통해 Azure 자동화 계정에 컴퓨터를 안전하게 온보드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-195">Machines can securely onboard to an Azure Automation account through the WMF 5 DSC registration protocol, which allows a DSC node to authenticate to a PowerShell DSC V2 Pull or Reporting server (including Azure Automation DSC).</span></span> <span data-ttu-id="9c493-196">노드는 **등록 URL**에 있는 서버에 등록되며 **등록 키**를 통해 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-196">The node registers to the server at a **Registration URL**, authenticating using a **Registration key**.</span></span> <span data-ttu-id="9c493-197">등록하는 동안 DSC 노드와 DSC 풀/보고 서버가 이 노드에 대해, 서버 게시-등록에 대한 인증에 사용할 고유 인증서를 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-197">During registration, the DSC node and DSC Pull/Reporting server negotiate a unique certificate for this node to use for authentication to the server post-registration.</span></span> <span data-ttu-id="9c493-198">이 프로세스는 노드가 손상되어 악의적 동작을 수행하는 등, 온보드된 노드가 다른 노드를 가장하는 것을 방지합니다. </span><span class="sxs-lookup"><span data-stu-id="9c493-198">This process prevents onboarded nodes from impersonating one another, such as if a node is compromised and behaving maliciously.</span></span> <span data-ttu-id="9c493-199">등록 후 해당 등록 키는 다시 인증에 사용되지 않으며 노드에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-199">After registration, the Registration key is not used for authentication again, and is deleted from the node.</span></span>

<span data-ttu-id="9c493-200">Azure Preview 포털의 **키 관리** 블레이드에서 DSC 등록 프로토콜에 필요한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-200">You can get the information required for the DSC registration protocol from the **Manage Keys** blade in the Azure preview portal.</span></span> <span data-ttu-id="9c493-201">자동화 계정의 **Essentials** 패널에서 키 아이콘을 클릭하여 이 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-201">Open this blade by clicking the key icon on the **Essentials** panel for the Automation account.</span></span>

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* <span data-ttu-id="9c493-202">등록 URL은 키 관리 블레이드의 URL 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-202">Registration URL is the URL field in the Manage Keys blade.</span></span>
* <span data-ttu-id="9c493-203">등록 키는 키 관리 블레이드에서 주기본 액세스 키 또는 보조 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-203">Registration key is the Primary Access Key or Secondary Access Key in the Manage Keys blade.</span></span> <span data-ttu-id="9c493-204">둘 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-204">Either key can be used.</span></span>

<span data-ttu-id="9c493-205">이전 키를 사용한 추가적인 노드 등록 차단을 위해 자동화 계정의 기본 액세스 키와 보조 액세스 키는 언제든 다시 생성하여 보안을 강화할 수 있습니다( **키 관리** 블레이드에서).</span><span class="sxs-lookup"><span data-stu-id="9c493-205">For added security, the primary and secondary access keys of an Automation account can be regenerated at any time (on the **Manage Keys** blade) to prevent future node registrations using previous keys.</span></span>

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a><span data-ttu-id="9c493-206">Azure 가상 컴퓨터 온보드 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9c493-206">Troubleshooting Azure virtual machine onboarding</span></span>

<span data-ttu-id="9c493-207">Azure 자동화 DSC를 사용하면 구성 관리를 위해 간편하게 Azure Windows VM을 온보드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-207">Azure Automation DSC lets you easily onboard Azure Windows VMs for configuration management.</span></span> <span data-ttu-id="9c493-208">내부적으로 Azure VM 필요 상태 구성 확장은 VM을 Azure 자동화 DSC에 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-208">Under the hood, the Azure VM Desired State Configuration extension is used to register the VM with Azure Automation DSC.</span></span> <span data-ttu-id="9c493-209">Azure VM 필요 상태 구성 확장은 비동기적으로 실행되므로 그 진행 상황 추적과 실행 문제 해결이 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-209">Since the Azure VM Desired State Configuration extension runs asynchronously, tracking its progress and troubleshooting its execution may be important.</span></span>

> [!NOTE]
> <span data-ttu-id="9c493-210">Azure VM 필요 상태 구성 확장을 사용하는 Azure 자동화 DSC에 Azure Windows VM을 온보드하는 모든 방법에서 노드가 Azure 자동화에 등록된 것으로 나타나는 데는 최대 1시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-210">Any method of onboarding an Azure Windows VM to Azure Automation DSC that uses the Azure VM Desired State Configuration extension could take up to an hour for the node to show up as registered in Azure Automation.</span></span> <span data-ttu-id="9c493-211">이것은 Azure 자동화 DSC의 VM을 온보드하기 위해 필요한 Azure VM DSC 확장에 의한 VM의 Windows 관리 프레임워크 5.0의 설치 때문에 꼭 필요한 일입니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-211">This is due to the installation of Windows Management Framework 5.0 on the VM by the Azure VM DSC extension, which is required to onboard the VM to Azure Automation DSC.</span></span>

<span data-ttu-id="9c493-212">Azure VM 필요 상태 구성 확장의 상태를 보거나 문제를 해결하려면 Azure Portal에서 온보드할 VM으로 이동한 다음 **모든 설정** -> **확장** -> **DSC**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-212">To troubleshoot or view the status of the Azure VM Desired State Configuration extension, in the Azure portal navigate to the VM being onboarded, then click -> **All settings** -> **Extensions** -> **DSC**.</span></span> <span data-ttu-id="9c493-213">자세한 내용을 보려면 **자세한 상태 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-213">For more details, you can click **View detailed status**.</span></span>

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a><span data-ttu-id="9c493-214">인증서 만료 및 다시 등록</span><span class="sxs-lookup"><span data-stu-id="9c493-214">Certificate expiration and reregistration</span></span>

<span data-ttu-id="9c493-215">컴퓨터를 Azure 자동화 DSC의 DSC 노드로 등록한 후에 해당 노드를 나중에 등록해야 하는 많은 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-215">After registering a machine as a DSC node in Azure Automation DSC, there are a number of reasons why you may need to reregister that node in the future:</span></span>

* <span data-ttu-id="9c493-216">등록 후에는 1년 후 만료되는 인증에 대해 각 노드가 자동으로 고유의 인증서를 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-216">After registering, each node automatically negotiates a unique certificate for authentication that expires after one year.</span></span> <span data-ttu-id="9c493-217">현재 PowerShell DSC 등록 프로토콜이 만료가 임박한 인증서를 자동으로 갱신할 수 없으므로 1년 기한 후 노드를 다시 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-217">Currently, the PowerShell DSC registration protocol cannot automatically renew certificates when they are nearing expiration, so you need to reregister the nodes after a year's time.</span></span> <span data-ttu-id="9c493-218">다시 등록하기 전에 각 노드가 Windows Management Framework 5.0 RTM을 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-218">Before reregistering, ensure that each node is running Windows Management Framework 5.0 RTM.</span></span> <span data-ttu-id="9c493-219">노드의 인증 인증서가 만료되고 노드가 다시 등록되지 않은 경우, 노드가 Azure 자동화와 통신할 수 없으며 '응답 없음'으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-219">If a node's authentication certificate expires, and the node is not reregistered, the node will be unable to communicate with Azure Automation and will be marked 'Unresponsive.'</span></span> <span data-ttu-id="9c493-220">노드 만료 시점으로부터 90일 안이나, 인증서 만료 이후에 재등록을 수행하면 새 인증서를 생성하여 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-220">Reregistration performed 90 days or less from the certificate expiration time, or at any point after the certificate expiration time, will result in a new certificate being generated and used.</span></span>
* <span data-ttu-id="9c493-221">ConfigurationMode와 같은 노드의 초기 등록 중에 설정된 [PowerShell DSC 로컬 구성 관리자 값](https://msdn.microsoft.com/powershell/dsc/metaconfig4)을 변경하려면</span><span class="sxs-lookup"><span data-stu-id="9c493-221">To change any [PowerShell DSC Local Configuration Manager values](https://msdn.microsoft.com/powershell/dsc/metaconfig4) that were set during initial registration of the node, such as ConfigurationMode.</span></span> <span data-ttu-id="9c493-222">현재 DSC 에이전트 값은 다시 등록을 통해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-222">Currently, these DSC agent values can only be changed through reregistration.</span></span> <span data-ttu-id="9c493-223">한 가지 예외는 노드에 할당된 노드 구성입니다. 이는 직접 Azure 자동화 DSC에서 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-223">The one exception is the Node Configuration assigned to the node -- this can be changed in Azure Automation DSC directly.</span></span>

<span data-ttu-id="9c493-224">다시 등록은 이 문서에서 설명하는 등록 방법 중 하나를 사용하여 처음에 노드를 등록한 동일한 방법으로 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-224">Reregistration can be performed in the same way you registered the node initially, using any of the onboarding methods described in this document.</span></span> <span data-ttu-id="9c493-225">다시 등록하기 전에 Azure 자동화 DSC에서 노드를 등록 취소할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c493-225">You do not need to unregister a node from Azure Automation DSC before reregistering it.</span></span>

## <a name="related-articles"></a><span data-ttu-id="9c493-226">관련 문서</span><span class="sxs-lookup"><span data-stu-id="9c493-226">Related Articles</span></span>

* [<span data-ttu-id="9c493-227">Azure 자동화 DSC 개요</span><span class="sxs-lookup"><span data-stu-id="9c493-227">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="9c493-228">Azure 자동화 DSC cmdlets</span><span class="sxs-lookup"><span data-stu-id="9c493-228">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="9c493-229">Azure 자동화 DSC 가격 책정</span><span class="sxs-lookup"><span data-stu-id="9c493-229">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)
