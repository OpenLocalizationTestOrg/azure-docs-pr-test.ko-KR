---
title: "Azure 자동화 DSC aaaGetting 시작 | Microsoft Docs"
description: "설명 및 예제는 hello 가장 일반적인 작업의 Azure 자동화 DSC 필요한 상태 구성)"
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
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="9b12e-103">Azure 자동화 DSC 시작하기</span><span class="sxs-lookup"><span data-stu-id="9b12e-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="9b12e-104">이 항목에서는 방법을 toodo hello와 Azure 자동화 DSC 필요한 상태 구성 (), 만들기, 가져오기 및 구성, 너무 컴퓨터를 관리 하는 온 보 딩 컴파일 및 보고서를 보는 등의 가장 일반적인 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="9b12e-105">Azure 자동화 DSC가 무엇인지의 개요는 [Azure 자동화 DSC 개요](automation-dsc-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b12e-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="9b12e-106">DSC 설명서는 [Windows PowerShell 필요한 상태 구성 개요](https://msdn.microsoft.com/PowerShell/dsc/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b12e-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="9b12e-107">이 항목에서는 단계별 가이드 toousing Azure 자동화 DSC를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="9b12e-108">이 항목에서 설명 하는 hello 단계를 수행 하지 않고 이미 설정 하는 샘플 환경을 원하는 경우 사용할 수 있습니다 [hello ARM 템플릿을 다음](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="9b12e-109">이 템플릿은 Azure 자동화 DSC에 의해 관리되는 Azure VM을 포함하는 완료된 Azure 자동화 DSC 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b12e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9b12e-110">Prerequisites</span></span>
<span data-ttu-id="9b12e-111">이 항목의 toocomplete hello 예제, hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="9b12e-112">Azure 자동화 계정.</span><span class="sxs-lookup"><span data-stu-id="9b12e-112">An Azure Automation account.</span></span> <span data-ttu-id="9b12e-113">Azure 자동화 실행 계정 만들기에 대한 지침은 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b12e-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="9b12e-114">Windows Server 2008 R2 이상을 실행하는 Azure Resource Manager VM(클래식 아님).</span><span class="sxs-lookup"><span data-stu-id="9b12e-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="9b12e-115">VM을 만드는 방법에 지침은 [hello Azure 포털에서에서 첫 번째 Windows 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="9b12e-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="9b12e-116">DSC 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="9b12e-116">Creating a DSC configuration</span></span>
<span data-ttu-id="9b12e-117">간단한 만듭니다 [DSC 구성을](https://msdn.microsoft.com/powershell/dsc/configurations) 중 hello의 유무 hello 검색이 설정 **웹 서버** Windows 기능 (IIS), 노드를 할당 하는 방법에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="9b12e-118">Windows PowerShell ISE hello (또는 다른 텍스트 편집기)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="9b12e-119">Hello 텍스트 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-119">Type hello following text:</span></span>
   
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
3. <span data-ttu-id="9b12e-120">Hello 파일으로 저장 `TestConfig.ps1`합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="9b12e-121">이 구성은 호출 자원을 하나씩 각 노드 블록에 hello [WindowsFeature 리소스](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), 검색이 설정 중 하나 hello의 유무 hello **웹 서버** 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="9b12e-122">Azure 자동화로 구성 가져오기</span><span class="sxs-lookup"><span data-stu-id="9b12e-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="9b12e-123">다음으로 hello 자동화 계정에 hello 구성을 가져옵니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="9b12e-124">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-125">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-126">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 구성을**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="9b12e-127">Hello에 **DSC 구성을** 블레이드에서 클릭 **구성을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="9b12e-128">Hello에 **구성 가져오기** 블레이드, 찾아보기 toohello `TestConfig.ps1` 파일을 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![Hello 스크린샷 * * 가져오기 구성 * * 블레이드](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="9b12e-130">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="9b12e-131">Azure 자동화에서 구성 보기</span><span class="sxs-lookup"><span data-stu-id="9b12e-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="9b12e-132">구성을 가져온 후에 hello Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="9b12e-133">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-134">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-135">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 구성**</span><span class="sxs-lookup"><span data-stu-id="9b12e-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="9b12e-136">Hello에 **DSC 구성을** 블레이드에서 클릭 **TestConfig** (hello 이전 절차에서이 가져온 hello 구성의 hello 이름).</span><span class="sxs-lookup"><span data-stu-id="9b12e-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="9b12e-137">Hello에 **TestConfig 구성** 블레이드에서 클릭 **구성 소스 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Hello TestConfig 구성 블레이드의 스크린샷](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="9b12e-139">A **TestConfig 구성 소스** 블레이드가 열리고 hello 구성에 대 한 hello PowerShell 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="9b12e-140">Azure 자동화에서 구성 컴파일</span><span class="sxs-lookup"><span data-stu-id="9b12e-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="9b12e-141">원하는 상태 tooa 노드를 적용 하려면 먼저 해당 상태를 정의 하는 DSC 구성은 하나 이상의 노드 구성 (MOF 문서)으로 컴파일됩니다 고 hello 자동화 DSC 끌어오기 서버에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="9b12e-142">Azure 자동화 DSC에서 구성 컴파일의 자세한 설명은 [Azure 자동화 DSC에서 구성을 컴파일](automation-dsc-compile.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b12e-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="9b12e-143">구성 컴파일에 대한 자세한 내용은 [DSC 구성](https://msdn.microsoft.com/PowerShell/DSC/configurations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b12e-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="9b12e-144">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-145">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-146">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 구성**</span><span class="sxs-lookup"><span data-stu-id="9b12e-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="9b12e-147">Hello에 **DSC 구성을** 블레이드에서 클릭 **TestConfig** (hello hello의 이전에 가져온 이름 구성).</span><span class="sxs-lookup"><span data-stu-id="9b12e-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="9b12e-148">Hello에 **TestConfig 구성** 블레이드에서 클릭 **컴파일**, 클릭 하 고 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="9b12e-149">컴파일 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-149">This starts a compilation job.</span></span>
   
    ![컴파일 단추를 강조 표시는 hello TestConfig 구성 블레이드의 스크린샷](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="9b12e-151">Azure 자동화에서 구성을 컴파일할 때 자동으로 모든 만든된 노드 구성 Mof toohello 끌어오기 서버를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="9b12e-152">컴파일 작업 보기</span><span class="sxs-lookup"><span data-stu-id="9b12e-152">Viewing a compilation job</span></span>
<span data-ttu-id="9b12e-153">컴파일을 시작 하 고 나면 hello에서 볼 수 있습니다 **컴파일 작업** hello에 바둑판식으로 배열 **구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="9b12e-154">hello **컴파일 작업** 타일 표시 현재 실행 되 고 완료 하 고 실패 한 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="9b12e-155">컴파일 작업 블레이드를 여는 경우 오류 또는 경고가 발생 한를 포함 하 여 해당 작업에 대 한 정보를 표시, 입력된 매개 변수 로그 hello 구성 및 컴파일에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="9b12e-156">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-157">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-158">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 구성을**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="9b12e-159">Hello에 **DSC 구성을** 블레이드에서 클릭 **TestConfig** (hello hello의 이전에 가져온 이름 구성).</span><span class="sxs-lookup"><span data-stu-id="9b12e-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="9b12e-160">Hello에 **컴파일 작업** 타일의 hello **TestConfig 구성** 블레이드를 나열 하는 hello 작업 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="9b12e-161">A **컴파일 작업** 시작 된 컴파일 작업 hello hello 날짜도 레이블이 지정 된이 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Hello 컴파일 작업 블레이드의 스크린샷](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="9b12e-163">Hello에서 모든 타일에서 클릭 **컴파일 작업** hello 작업에 대 한 세부 정보 블레이드에서 toosee 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="9b12e-164">노드 구성 보기</span><span class="sxs-lookup"><span data-stu-id="9b12e-164">Viewing node configurations</span></span>
<span data-ttu-id="9b12e-165">컴파일 작업을 성공적으로 완료하면 하나 이상의 새 노드 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="9b12e-166">노드 구성에 배포 된 toohello 끌어오기 서버와 준비 toobe 가져오고 하나 이상의 노드에 적용 MOF 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="9b12e-167">Hello에 자동화 계정에서 hello 노드 구성을 볼 수 있습니다 **DSC 노드 구성을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="9b12e-168">노드 구성 이름이 hello 양식으로 *ConfigurationName*. *NodeName*합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="9b12e-169">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-170">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-171">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드 구성을**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Hello DSC 노드 구성을 블레이드의 스크린샷](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="9b12e-173">Azure 자동화 DSC를 통한 관리를 위한 Azure VM 온보드</span><span class="sxs-lookup"><span data-stu-id="9b12e-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="9b12e-174">Azure 자동화 DSC toomanage Azure Vm (리소스 관리자 및 기본), 온-프레미스 Vm, Linux 컴퓨터, AWS Vm 및 온-프레미스 물리적 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="9b12e-175">이 항목에서는 다룹니다 어떻게 tooonboard Azure 리소스 관리자 Vm만 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="9b12e-176">다른 유형의 컴퓨터 온보드에 대한 정보는 [Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b12e-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="9b12e-177">Azure 자동화 DSC에 의해 관리에 대 한 Azure 리소스 관리자 VM tooonboard</span><span class="sxs-lookup"><span data-stu-id="9b12e-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="9b12e-178">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-179">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-180">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="9b12e-181">Hello에 **DSC 노드** 블레이드에서 클릭 **Azure VM 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Hello Azure VM 추가 단추를 강조 표시는 hello DSC 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="9b12e-183">Hello에 **Azure Vm 추가** 블레이드에서 클릭 **tooonboard 가상 컴퓨터를 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="9b12e-184">Hello에 **선택 Vm** 블레이드를 누르고 tooonboard, 원하는 VM 선택 hello **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9b12e-185">Windows Server 2008 R2 이상을 실행하는 Azure Resource Manager VM이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="9b12e-186">Hello에 **Azure Vm 추가** 블레이드에서 클릭 **등록 데이터를 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="9b12e-187">Hello에 **등록** 블레이드에서 hello 이름을 입력 hello에 대 한 VM tooapply toohello hello 노드 구성의 원하는 **노드 구성 이름은** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="9b12e-188">Hello hello 자동화 계정에서에서 노드 구성 이름이 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="9b12e-189">이 시점에서 이름을 제공하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="9b12e-190">온 보 딩 hello 노드 할당 hello 노드 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="9b12e-191">**필요한 경우 노드 다시 부팅**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Hello 등록 블레이드의 스크린샷](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="9b12e-193">지정한 hello 노드 구성을 hello 하 여 지정 된 간격에 적용 된 toohello VM 수 **구성 모드 빈도가**, hello VM은 업데이트 toohello 노드 구성 hello 하여지정된간격에있는지확인하고 **새로 고침 빈도**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="9b12e-194">이러한 값은 사용 하는 방법에 대 한 자세한 내용은 참조 [hello 구성 로컬 구성 관리자](https://msdn.microsoft.com/PowerShell/DSC/metaConfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="9b12e-195">Hello에 **Azure Vm 추가** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="9b12e-196">Azure의 온 보 딩 hello VM hello 프로세스를 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="9b12e-197">완료 되 면 hello VM에에서 나타납니다 hello **DSC 노드** 블레이드 hello 자동화 계정에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="9b12e-198">DSC 노드 hello 목록 보기</span><span class="sxs-lookup"><span data-stu-id="9b12e-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="9b12e-199">관리 hello의 자동화 계정에 대 한 등록 된 모든 컴퓨터의 hello 목록을 볼 수 있습니다 **DSC 노드** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="9b12e-200">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-201">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-202">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="9b12e-203">DSC 노드에 대한 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="9b12e-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="9b12e-204">관리 되는 노드에 대 한 일관성 확인을 수행 하는 Azure 자동화 DSC 때마다 hello 노드 상태 보고서 백 toohello 끌어오기 서버를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="9b12e-205">해당 노드에 대 한 hello 블레이드에서 이러한 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="9b12e-206">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-207">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-208">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="9b12e-209">Hello에 **보고서** 타일 hello 목록의 hello 보고서 중 하나를 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9b12e-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Hello 보고서 블레이드의 스크린샷](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="9b12e-211">개별 보고서에 대 한 hello 블레이드에서 확인 hello 다음 hello 해당 일관성에 대 한 상태 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="9b12e-212">상태 보고 hello-hello 노드는 hello 구성 "Failed", "준수" 여부 hello 노드는 "호환 되지 않는" (hello 노드 중인 **applyandmonitor** 모드와 hello 컴퓨터가 hello 원하는 상태에 있지 않은).</span><span class="sxs-lookup"><span data-stu-id="9b12e-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="9b12e-213">hello hello 일관성 확인에 대 한 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="9b12e-214">hello 일관성에 대 한 총 런타임을 hello 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="9b12e-215">hello 유형의 일관성 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-215">hello type of consistency check.</span></span>
* <span data-ttu-id="9b12e-216">Hello 오류 코드 및 오류 메시지를 포함 하 여 모든 오류.</span><span class="sxs-lookup"><span data-stu-id="9b12e-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="9b12e-217">(여부 hello 노드는 해당 리소스에 대 한 원하는 hello 상태)의 각 리소스의 hello 상태 및 hello 구성에 사용 되는 모든 DSC 리소스-클릭할 수 있는 자세한 정보를 해당 리소스에 대 한 각 리소스 tooget에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="9b12e-218">hello 이름, IP 주소 및 hello 노드의 구성 모드 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="9b12e-219">클릭할 수도 있습니다 **원시 보고서를 볼** toosee hello 실제 데이터는 노드 hello toohello 서버 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="9b12e-220">해당 데이터 사용에 대한 자세한 내용은 [DSC 보고서 서버 사용](https://msdn.microsoft.com/powershell/dsc/reportserver)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b12e-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="9b12e-221">Hello 첫 번째 보고서를 사용할 수 전에 노드는 등록 된 후에 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="9b12e-222">할 수 있습니다 too30 분을 toowait hello 첫 번째 보고서에 대 한 후 등록 노드.</span><span class="sxs-lookup"><span data-stu-id="9b12e-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="9b12e-223">다시 할당 하는 노드 tooa 다른 노드 구성</span><span class="sxs-lookup"><span data-stu-id="9b12e-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="9b12e-224">Hello 초기 할당 보다 다른 노드 구성 노드 toouse을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="9b12e-225">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-226">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-227">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="9b12e-228">Hello에 **DSC 노드** hello 이름 클릭 블레이드에서 원하는 tooreassign hello 노드의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="9b12e-229">해당 노드에 대 한 hello 블레이드에서 클릭 **할당 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Hello 노드 할당 단추를 강조 표시는 hello 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="9b12e-231">Hello에 **노드 구성을 할당** 블레이드, 선택 hello 노드 구성 toowhich tooassign hello 노드를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Hello 노드 구성을 할당 블레이드의 스크린샷](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="9b12e-233">노드 등록 취소</span><span class="sxs-lookup"><span data-stu-id="9b12e-233">Unregistering a node</span></span>
<span data-ttu-id="9b12e-234">Azure 자동화 DSC에 의해 관리 되는 노드 toobe를 더 이상 사용 하지 않으려면 하는 경우 등록 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="9b12e-235">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b12e-236">Hello 허브 메뉴에서 클릭 **모든 리소스** 및 다음 hello 사용자의 자동화 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="9b12e-237">Hello에 **자동화 계정** 블레이드에서 클릭 **DSC 노드**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="9b12e-238">Hello에 **DSC 노드** hello 이름 클릭 블레이드에서 원하는 toounregister hello 노드의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="9b12e-239">해당 노드에 대 한 hello 블레이드에서 클릭 **등록 취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b12e-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Hello 등록 취소 단추를 강조 표시는 hello 노드 블레이드의 스크린샷](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="9b12e-241">관련 문서</span><span class="sxs-lookup"><span data-stu-id="9b12e-241">Related Articles</span></span>
* [<span data-ttu-id="9b12e-242">Azure 자동화 DSC 개요</span><span class="sxs-lookup"><span data-stu-id="9b12e-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="9b12e-243">Azure 자동화 DSC를 통한 관리를 위한 컴퓨터 온보드</span><span class="sxs-lookup"><span data-stu-id="9b12e-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="9b12e-244">Windows PowerShell 필요한 상태 구성 개요</span><span class="sxs-lookup"><span data-stu-id="9b12e-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="9b12e-245">Azure 자동화 DSC cmdlets</span><span class="sxs-lookup"><span data-stu-id="9b12e-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="9b12e-246">Azure 자동화 DSC 가격 책정</span><span class="sxs-lookup"><span data-stu-id="9b12e-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

