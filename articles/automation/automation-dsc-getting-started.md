---
title: "Azure Automation DSC 시작하기 | Microsoft Docs"
description: "Azure 자동화 DSC(필요한 상태 구성)에서 가장 일반적인 작업의 설명 및 예제"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="f4c65-103">Azure 자동화 DSC 시작하기</span><span class="sxs-lookup"><span data-stu-id="f4c65-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="f4c65-104">이 항목에서는 Azure 자동화 DSC(필요한 상태 구성)로 만들기, 가져오기 및 구성 컴파일링, 관리할 컴퓨터 온보드 및 보고서 보기 등과 같은 가장 일반적인 작업을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="f4c65-105">Azure 자동화 DSC가 무엇인지의 개요는 [Azure 자동화 DSC 개요](automation-dsc-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4c65-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="f4c65-106">DSC 설명서는 [Windows PowerShell 필요한 상태 구성 개요](https://msdn.microsoft.com/PowerShell/dsc/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4c65-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="f4c65-107">이 항목에서는 Azure 자동화 DSC 사용에 대한 단계별 가이드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="f4c65-108">이 항목에 설명된 단계를 수행하지 않고 이미 설정된 샘플 환경을 원하는 경우 [다음 ARM 템플릿](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="f4c65-109">이 템플릿은 Azure 자동화 DSC에 의해 관리되는 Azure VM을 포함하는 완료된 Azure 자동화 DSC 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4c65-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f4c65-110">Prerequisites</span></span>
<span data-ttu-id="f4c65-111">이 항목의 예제를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="f4c65-112">Azure 자동화 계정.</span><span class="sxs-lookup"><span data-stu-id="f4c65-112">An Azure Automation account.</span></span> <span data-ttu-id="f4c65-113">Azure 자동화 실행 계정 만들기에 대한 지침은 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4c65-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="f4c65-114">Windows Server 2008 R2 이상을 실행하는 Azure Resource Manager VM(클래식 아님).</span><span class="sxs-lookup"><span data-stu-id="f4c65-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="f4c65-115">VM 만들기에 대한 지침은 [Azure 포털에서 첫 번째 Windows 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="f4c65-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="f4c65-116">DSC 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="f4c65-116">Creating a DSC configuration</span></span>
<span data-ttu-id="f4c65-117">노드를 할당하는 방법에 따라 [웹 서버](https://msdn.microsoft.com/powershell/dsc/configurations) Windows 기능(IIS)의 존재 또는 부재를 확인하는 간단한 **DSC 구성** 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="f4c65-118">Windows PowerShell ISE(또는 다른 텍스트 편집기)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="f4c65-119">다음 텍스트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="f4c65-120">파일을 `TestConfig.ps1`(으)로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="f4c65-121">이 구성은 각 노드 블록에서 [웹 서버](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource)기능의 존재 또는 부재를 확인하는 하나의 리소스, **WindowsFeature 리소스** 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="f4c65-122">Azure 자동화로 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="f4c65-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="f4c65-123">다음으로 자동화 계정으로 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="f4c65-124">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-125">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-126">**자동화 계정** 블레이드에서 **DSC 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="f4c65-127">**DSC 구성** 블레이드에서 **구성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="f4c65-128">**구성 가져오기** 블레이드에서 컴퓨터의 `TestConfig.ps1` 파일로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![**구성 가져오기** 블레이드의 스크린샷](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="f4c65-130">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="f4c65-131">Azure 자동화에서 구성 보기</span><span class="sxs-lookup"><span data-stu-id="f4c65-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="f4c65-132">구성을 가져온 후에 Azure 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="f4c65-133">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-134">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-135">**자동화 계정** 블레이드에서 **DSC 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="f4c65-136">**DSC 구성 블레이드**에서 **TestConfig**(이전 절차에서 가져온 구성의 이름임)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="f4c65-137">**TestConfig 구성** 블레이드에서 **구성 원본 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![TestConfig 구성 블레이드의 스크린샷](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="f4c65-139">**TestConfig 구성 원본** 블레이드가 열리고 구성에 대한 PowerShell 코드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="f4c65-140">Azure 자동화에서 구성 컴파일</span><span class="sxs-lookup"><span data-stu-id="f4c65-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="f4c65-141">노드에 원하는 상태를 적용하려면 먼저 해당 상태를 정의하는 DSC 구성을 하나 이상의 노드 구성(MOF 문서)으로 컴파일한 다음 자동화 DSC 끌어오기 서버에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="f4c65-142">Azure 자동화 DSC에서 구성 컴파일의 자세한 설명은 [Azure 자동화 DSC에서 구성을 컴파일](automation-dsc-compile.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4c65-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="f4c65-143">구성 컴파일에 대한 자세한 내용은 [DSC 구성](https://msdn.microsoft.com/PowerShell/DSC/configurations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4c65-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="f4c65-144">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-145">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-146">**자동화 계정** 블레이드에서 **DSC 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="f4c65-147">**DSC 구성** 블레이드에서 **TestConfig**(이전에 가져온 구성의 이름)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="f4c65-148">**TestConfig 구성** 블레이드에서 **컴파일**을 클릭한 다음 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="f4c65-149">컴파일 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-149">This starts a compilation job.</span></span>
   
    ![컴파일 단추를 강조 표시하는 TestConfig 구성 블레이드의 스크린샷](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="f4c65-151">Azure 자동화에서 구성을 컴파일하면 생성된 모든 노드 구성 MOF를 끌어오기 서버에 자동으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="f4c65-152">컴파일 작업 보기</span><span class="sxs-lookup"><span data-stu-id="f4c65-152">Viewing a compilation job</span></span>
<span data-ttu-id="f4c65-153">컴파일을 시작한 후에 **구성** 블레이드의 **컴파일 작업** 타일에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="f4c65-154">**컴파일 작업** 타일은 현재 실행 중인, 완료된 및 실패한 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="f4c65-155">컴파일 작업 블레이드를 열면 발생한 모든 오류 또는 경고, 구성에서 사용된 입력 매개 변수 및 컴파일 로그를 포함한 해당 작업에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="f4c65-156">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-157">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-158">**자동화 계정** 블레이드에서 **DSC 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="f4c65-159">**DSC 구성** 블레이드에서 **TestConfig**(이전에 가져온 구성의 이름)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="f4c65-160">**TestConfig 구성** 블레이드의 **컴파일 작업** 타일에서 나열된 작업 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="f4c65-161">컴파일 작업이 시작된 날짜로 레이블이 지정된 **컴파일 작업** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![컴파일 작업 블레이드의 스크린샷](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="f4c65-163">**컴파일 작업** 블레이드에서 타일을 클릭하여 작업에 대한 추가 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="f4c65-164">노드 구성 보기</span><span class="sxs-lookup"><span data-stu-id="f4c65-164">Viewing node configurations</span></span>
<span data-ttu-id="f4c65-165">컴파일 작업을 성공적으로 완료하면 하나 이상의 새 노드 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="f4c65-166">노드 구성은 끌어오기 서버에 배포되고 하나 이상의 노드에서 가져오고 적용될 준비가 된 MOF 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="f4c65-167">**DSC 노드 구성** 블레이드의 자동화 계정에서 노드 구성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="f4c65-168">노드 구성은 *ConfigurationName*.*NodeName*의 형식으로 이름을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="f4c65-169">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-170">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-171">**자동화 계정** 블레이드에서 **DSC 노드 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![DSC 노드 구성 블레이드의 스크린샷](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="f4c65-173">Azure 자동화 DSC를 통한 관리를 위한 Azure VM 온보드</span><span class="sxs-lookup"><span data-stu-id="f4c65-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="f4c65-174">Azure 자동화 DSC를 사용하여 Azure VM(클래식 및 리소스 관리자), 온-프레미스 VM, Linux 컴퓨터, AWS VM 및 온-프레미스 물리적 컴퓨터를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="f4c65-175">이 항목에서는 Azure Resource Manager VM만을 온보드하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="f4c65-176">다른 유형의 컴퓨터 온보드에 대한 정보는 [Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4c65-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="f4c65-177">Azure 자동화 DSC를 통한 관리를 위한 Azure Resource Manager VM 온보드하기</span><span class="sxs-lookup"><span data-stu-id="f4c65-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="f4c65-178">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-179">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-180">**자동화 계정** 블레이드에서 **DSC 노드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="f4c65-181">**DSC 노드** 블레이드에서 **Azure VM 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Azure VM 추가 단추를 강조 표시하는 DSC 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="f4c65-183">**Azure VM 추가** 블레이드에서 **온보드할 가상 컴퓨터 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="f4c65-184">**VM 선택** 블레이드에서 온보드하려는 VM을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f4c65-185">Windows Server 2008 R2 이상을 실행하는 Azure Resource Manager VM이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="f4c65-186">**Azure VM 추가** 블레이드에서 **등록 데이터 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="f4c65-187">**등록** 블레이드에서 VM에 적용하려는 노드 구성의 이름을 **노드 구성 이름** 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="f4c65-188">자동화 계정의 노드 구성 이름과 정확하게 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="f4c65-189">이 시점에서 이름을 제공하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="f4c65-190">노드를 온보드한 후 할당된 노드 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="f4c65-191">**필요한 경우 노드 다시 부팅**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![등록 블레이드의 스크린샷](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="f4c65-193">지정한 노드 구성이 **구성 모드 빈도**에서 지정된 간격으로 VM에 적용되고 VM은 **새로 고침 빈도**에서 지정된 간격으로 노드 구성에 대한 업데이트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="f4c65-194">이러한 값을 사용하는 방법에 대한 자세한 내용은 [로컬 구성 관리자 구성](https://msdn.microsoft.com/PowerShell/DSC/metaConfig)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4c65-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="f4c65-195">**Azure VM 추가** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="f4c65-196">Azure는 VM 온보딩 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="f4c65-197">완료되면 VM이 자동화 계정의 **DSC 노드** 블레이드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="f4c65-198">DSC 노드 목록 보기</span><span class="sxs-lookup"><span data-stu-id="f4c65-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="f4c65-199">**DSC 노드** 블레이드의 자동화 계정에서 관리에 온보드된 모든 컴퓨터의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="f4c65-200">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-201">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-202">**자동화 계정** 블레이드에서 **DSC 노드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="f4c65-203">DSC 노드에 대한 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="f4c65-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="f4c65-204">Azure 자동화 DSC가 관리되는 노드에 대한 일관성 검사를 수행할 때마다 노드는 끌어오기 서버에 상태 보고서를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="f4c65-205">해당 노드에 대한 블레이드에서 이러한 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="f4c65-206">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-207">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-208">**자동화 계정** 블레이드에서 **DSC 노드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="f4c65-209">**보고서** 타일에서 목록의 보고서 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![보고서 블레이드의 스크린샷](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="f4c65-211">개별 보고서에 대한 블레이드에서 해당 일관성 검사에 대한 다음과 같은 상태 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="f4c65-212">보고서 상태 — 노드의 "준수" 여부, 구성 "실패" 또는 노드는 "비준수"입니다.(노드가 **applyandmonitor** 모드에 있는 경우 및 컴퓨터는 원하는 상태에 있지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="f4c65-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="f4c65-213">일관성 검사에 대한 시작 시간.</span><span class="sxs-lookup"><span data-stu-id="f4c65-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="f4c65-214">일관성 검사에 대한 총 런타임.</span><span class="sxs-lookup"><span data-stu-id="f4c65-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="f4c65-215">일관성 검사의 형식.</span><span class="sxs-lookup"><span data-stu-id="f4c65-215">The type of consistency check.</span></span>
* <span data-ttu-id="f4c65-216">오류 코드 및 오류 메시지를 포함하는 모든 오류.</span><span class="sxs-lookup"><span data-stu-id="f4c65-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="f4c65-217">구성에서 사용되는 모든 DSC 리소스 및 각 리소스의 상태(노드가 해당 리소스에 대해 원하는 상태 여부) — 각 리소스를 클릭하여 해당 리소스에 대한 자세한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="f4c65-218">노드의 이름, IP 주소 및 구성 모드.</span><span class="sxs-lookup"><span data-stu-id="f4c65-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="f4c65-219">**원시 보고서 보기** 를 클릭하여 노드가 서버에 전송하는 실제 데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="f4c65-220">해당 데이터 사용에 대한 자세한 내용은 [DSC 보고서 서버 사용](https://msdn.microsoft.com/powershell/dsc/reportserver)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4c65-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="f4c65-221">노드가 온보드된 후 첫 번째 보고서를 사용할 수 있기 전까지 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="f4c65-222">노드를 온보드한 후 첫 번째 보고서에 대해 최대 30분을 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="f4c65-223">다른 노드 구성에 노드 다시 할당</span><span class="sxs-lookup"><span data-stu-id="f4c65-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="f4c65-224">처음에 할당한 것과 다른 노드 구성을 사용하도록 노드를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="f4c65-225">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-226">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-227">**자동화 계정** 블레이드에서 **DSC 노드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="f4c65-228">**DSC 노드** 블레이드에서 다시 할당하려는 노드의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="f4c65-229">해당 노드에 대한 블레이드에서 **노드 할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![노드 할당 단추를 강조 표시하는 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="f4c65-231">**노드 구성 할당** 블레이드에서 노드를 할당하려는 노드 구성을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![노드 구성 할당 블레이드의 스크린샷](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="f4c65-233">노드 등록 취소</span><span class="sxs-lookup"><span data-stu-id="f4c65-233">Unregistering a node</span></span>
<span data-ttu-id="f4c65-234">Azure 자동화 DSC에 의해 노드를 더 이상 관리하지 않으려는 경우 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="f4c65-235">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4c65-236">허브 메뉴에서 **모든 리소스** 를 클릭한 다음 자동화 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="f4c65-237">**자동화 계정** 블레이드에서 **DSC 노드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="f4c65-238">**DSC 노드** 블레이드에서 등록 취소하려는 노드의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="f4c65-239">해당 노드에 대한 블레이드에서 **등록 취소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4c65-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![등록 취소 단추를 강조 표시하는 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="f4c65-241">관련 문서</span><span class="sxs-lookup"><span data-stu-id="f4c65-241">Related Articles</span></span>
* [<span data-ttu-id="f4c65-242">Azure 자동화 DSC 개요</span><span class="sxs-lookup"><span data-stu-id="f4c65-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="f4c65-243">Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드</span><span class="sxs-lookup"><span data-stu-id="f4c65-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="f4c65-244">Windows PowerShell 필요한 상태 구성 개요</span><span class="sxs-lookup"><span data-stu-id="f4c65-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="f4c65-245">Azure 자동화 DSC cmdlets</span><span class="sxs-lookup"><span data-stu-id="f4c65-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="f4c65-246">Azure 자동화 DSC 가격 책정</span><span class="sxs-lookup"><span data-stu-id="f4c65-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

