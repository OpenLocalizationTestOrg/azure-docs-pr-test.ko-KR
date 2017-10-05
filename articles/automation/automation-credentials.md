---
title: "Azure 자동화의 자격 증명 자산 | Microsoft Docs"
description: "Azure 자동화의 자격 증명 자산은 runbook 또는 DSC 구성을 통해 액세스 되는 리소스를 인증하는 보안 자격 증명을 포함합니다. 이 문서에서는 자격 증명 자산을 만들고 runbook 또는 DSC 구성에 사용하는 방법을 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: e2857515f3842a875ef7b5a9327392818931168f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="credential-assets-in-azure-automation"></a><span data-ttu-id="27c4d-104">Azure 자동화의 자격 증명 자산</span><span class="sxs-lookup"><span data-stu-id="27c4d-104">Credential assets in Azure Automation</span></span>
<span data-ttu-id="27c4d-105">자동화 자격 증명 자산은 사용자 이름과 암호 등의 보안 자격 증명을 포함하는 [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 개체를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-105">An Automation credential asset holds a [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential)  object which contains security credentials such as a username and password.</span></span> <span data-ttu-id="27c4d-106">Runbook과 DSC 구성은 인증을 위해 PSCredential 개체를 허용하는 cmdlet를 사용할 수 있고, 일부 응용 프로그램 도는 인증이 필요한 서비스에 제공하기 위해 PScredential 개체의 사용자 이름과 암호를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-106">Runbooks and DSC configurations may use cmdlets that accept a PSCredential object for authentication, or they may extract the username and password of the PSCredential object to provide to some application or service requiring authentication.</span></span> <span data-ttu-id="27c4d-107">자격 증명의 속성은 Azure 자동화에 안전하게 저장되며 [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) 활동을 통해 runbook과 DSC 구성에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-107">The properties for a credential are stored securely in Azure Automation and can be accessed in the runbook or DSC configuration with the [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) activity.</span></span>

> [!NOTE]
> <span data-ttu-id="27c4d-108">Azure 자동화의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-108">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="27c4d-109">이러한 자산은 각 자동화 계정에 대해 생성되는 고유 키를 사용하여 암호화되고 Azure 자동화에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-109">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="27c4d-110">이 키는 마스터 인증서로 암호화되어 Azure 자동화에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-110">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="27c4d-111">자동화 계정에 대한 키는 보안 자산을 저장하기 전에 마스터 인증서를 사용하여 암호가 해독된 후 자산을 암호화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-111">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>  

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="27c4d-112">Windows PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="27c4d-112">Windows PowerShell cmdlets</span></span>
<span data-ttu-id="27c4d-113">다음 표의 cmdlet은 Windows PowerShell을 사용하여 자동화 자격 증명 자산을 만들고 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-113">The cmdlets in the following table are used to create and manage automation credential assets with Windows PowerShell.</span></span>  <span data-ttu-id="27c4d-114">자동화 runbook과 DSC 구성에 사용할 수 있는 [Azure PowerShell 모듈](/powershell/azure/overview) 의 일부로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-114">They ship as part of the [Azure PowerShell module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span></span>

| <span data-ttu-id="27c4d-115">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="27c4d-115">Cmdlets</span></span> | <span data-ttu-id="27c4d-116">설명</span><span class="sxs-lookup"><span data-stu-id="27c4d-116">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="27c4d-117">Get-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="27c4d-117">Get-AzureAutomationCredential</span></span>](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="27c4d-118">자격 증명 자산에 대한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-118">Retrieves information about a credential asset.</span></span> <span data-ttu-id="27c4d-119">**Get-AutomationPSCredential** 활동에서는 자격 증명 자체만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-119">You can only retrieve the credential itself from **Get-AutomationPSCredential** activity.</span></span> |
| [<span data-ttu-id="27c4d-120">New-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="27c4d-120">New-AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="27c4d-121">새 자동화 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-121">Creates a new Automation credential.</span></span> |
| [<span data-ttu-id="27c4d-122">Remove- AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="27c4d-122">Remove- AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="27c4d-123">자동화 자격 증명을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-123">Removes an Automation credential.</span></span> |
| [<span data-ttu-id="27c4d-124">Set- AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="27c4d-124">Set- AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="27c4d-125">기존 자동화 자격 증명에 대한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-125">Sets the properties for an existing Automation credential.</span></span> |

## <a name="runbook-activities"></a><span data-ttu-id="27c4d-126">Runbook 활동</span><span class="sxs-lookup"><span data-stu-id="27c4d-126">Runbook activities</span></span>
<span data-ttu-id="27c4d-127">다음 표의 활동은 runbook과 DSC 구성의 자격 증명에 액세스하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-127">The activities in the following table are used to access credentials in a runbook and DSC configurations.</span></span>

| <span data-ttu-id="27c4d-128">활동</span><span class="sxs-lookup"><span data-stu-id="27c4d-128">Activities</span></span> | <span data-ttu-id="27c4d-129">설명</span><span class="sxs-lookup"><span data-stu-id="27c4d-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="27c4d-130">Get-AutomationPSCredential</span><span class="sxs-lookup"><span data-stu-id="27c4d-130">Get-AutomationPSCredential</span></span> |<span data-ttu-id="27c4d-131">Runbook 또는 DSC 구성에 사용하는 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-131">Gets a credential to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="27c4d-132">[System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-132">Returns a [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) object.</span></span> |

> [!NOTE]
> <span data-ttu-id="27c4d-133">Get-AutomationPSCredential의 Name 매개변수에서는 변수를 사용하면 안 됩니다. runbook 또는 DSC 구성과 design time의 자격 증명 간에 종속성이 발견되어 복잡해질 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-133">You should avoid using variables in the –Name parameter of Get-AutomationPSCredential since this can complicate discovering dependencies between runbooks or DSC configurations, and credential assets at design time.</span></span>
> 
> 

## <a name="creating-a-new-credential-asset"></a><span data-ttu-id="27c4d-134">새 자격 증명 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="27c4d-134">Creating a new credential asset</span></span>

### <a name="to-create-a-new-credential-asset-with-the-azure-portal"></a><span data-ttu-id="27c4d-135">Azure 포털을 사용하여 새 자격 증명 자산을 만들려면</span><span class="sxs-lookup"><span data-stu-id="27c4d-135">To create a new credential asset with the Azure portal</span></span>
1. <span data-ttu-id="27c4d-136">자동화 계정에서 **자산** 파트를 클릭하여 **자산** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-136">From your automation account, click the **Assets** part to open the **Assets** blade.</span></span>
2. <span data-ttu-id="27c4d-137">**자격 증명** 파트를 클릭하여 **자격 증명** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-137">Click the **Credentials** part to open the **Credentials** blade.</span></span>
3. <span data-ttu-id="27c4d-138">블레이드의 위쪽에서 **자격 증명 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-138">Click **Add a credential** at the top of the blade.</span></span>
4. <span data-ttu-id="27c4d-139">양식을 완료하고 **만들기** 를 클릭하여 새 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-139">Complete the form and click **Create** to save the new credential.</span></span>

### <a name="to-create-a-new-credential-asset-with-windows-powershell"></a><span data-ttu-id="27c4d-140">Windows PowerShell을 사용하여 새 자격 증명 자산을 만들려면</span><span class="sxs-lookup"><span data-stu-id="27c4d-140">To create a new credential asset with Windows PowerShell</span></span>
<span data-ttu-id="27c4d-141">다음 명령 예제에서는 새 자동화 자격 증명을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-141">The following sample commands show how to create a new automation credential.</span></span> <span data-ttu-id="27c4d-142">먼저 이름 및 암호를 사용하여 PSCredential 개체를 만든 다음 이를 사용하여 자격 증명 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-142">A PSCredential object is first created with the name and password and then used to create the credential asset.</span></span> <span data-ttu-id="27c4d-143">또는 **Get-Credential** cmdlet을 사용하여 이름 및 암호를 입력하라는 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-143">Alternatively, you could use the **Get-Credential** cmdlet to be prompted to type in a name and password.</span></span>

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="to-create-a-new-credential-asset-with-the-azure-classic-portal"></a><span data-ttu-id="27c4d-144">Azure 클래식 포털을 사용하여 새 자격 증명 자산을 만들려면</span><span class="sxs-lookup"><span data-stu-id="27c4d-144">To create a new credential asset with the Azure classic portal</span></span>
1. <span data-ttu-id="27c4d-145">자동화 계정에서 창의 위쪽에 있는 **자산** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-145">From your automation account, click **Assets** at the top of the window.</span></span>
2. <span data-ttu-id="27c4d-146">창의 아래쪽의 **설정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-146">At the bottom of the window, click **Add Setting**.</span></span>
3. <span data-ttu-id="27c4d-147">**자격 증명 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-147">Click **Add Credential**.</span></span>
4. <span data-ttu-id="27c4d-148">**자격 증명 형식** 드롭다운에서 **PowerShell 자격 증명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-148">In the **Credential Type** dropdown, select **PowerShell Credential**.</span></span>
5. <span data-ttu-id="27c4d-149">마법사를 완료하고 새 자격 증명을 저장하는 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-149">Complete the wizard and click the checkbox to save the new credential.</span></span>

## <a name="using-a-powershell-credential"></a><span data-ttu-id="27c4d-150">PowerShell 자격 증명 사용</span><span class="sxs-lookup"><span data-stu-id="27c4d-150">Using a PowerShell credential</span></span>
<span data-ttu-id="27c4d-151">**Get-AutomationPSCredential** 활동을 사용하여 runbook 또는 DSC 구성의 자격 증명 자산을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-151">You retrieve a credential asset in a runbook or DSC configuration with the **Get-AutomationPSCredential** activity.</span></span> <span data-ttu-id="27c4d-152">그러면 PSCredential 매개 변수가 필요한 활동 또는 cmdlet에서 사용할 수 있는 [PSCredential 개체](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) 가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-152">This returns a [PSCredential object](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) that you can use with an activity or cmdlet that requires a PSCredential parameter.</span></span> <span data-ttu-id="27c4d-153">자격 증명 개체의 속성을 검색하여 개별적으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-153">You can also retrieve the properties of the credential object to use individually.</span></span> <span data-ttu-id="27c4d-154">이 개체에는 사용자 이름 및 보안 암호에 대한 속성이 있으며, **GetNetworkCredential** 메서드를 사용하여 보안되지 않은 버전의 암호를 제공하는 [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) 개체를 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-154">The object has a property for the username and the secure password, or you can use the **GetNetworkCredential** method to return a [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) object that will provide an unsecured version of the password.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="27c4d-155">텍스트 Runbook 샘플</span><span class="sxs-lookup"><span data-stu-id="27c4d-155">Textual runbook sample</span></span>
<span data-ttu-id="27c4d-156">다음 명령 예제에서는 Runbook에서 PowerShell 자격 증명을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-156">The following sample commands show how to use a PowerShell credential in a runbook.</span></span> <span data-ttu-id="27c4d-157">이 예제에서는 자격 증명을 검색하고 해당 사용자 이름 및 암호를 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-157">In this example, the credential is retrieved and its username and password assigned to variables.</span></span>

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a><span data-ttu-id="27c4d-158">그래픽 Runbook 샘플</span><span class="sxs-lookup"><span data-stu-id="27c4d-158">Graphical runbook sample</span></span>
<span data-ttu-id="27c4d-159">그래픽 편집기의 라이브러리 창에서 자격 증명을 마우스 오른쪽 단추로 클릭하고 **캔버스에 추가**를 선택하여 **Get-AutomationPSCredential**를 그래픽 Runbook에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-159">You add a **Get-AutomationPSCredential** activity to a graphical runbook by right-clicking on the credential in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![캔버스에 자격 증명 추가](media/automation-credentials/credential-add-canvas.png)

<span data-ttu-id="27c4d-161">다음 그림에서는 그래픽 Runbook에서 자격 증명을 사용하는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-161">The following image shows an example of using a credential in a graphical runbook.</span></span>  <span data-ttu-id="27c4d-162">이 예제에서는 [Azure AD 사용자 계정으로 Runbook 인증](automation-create-aduser-account.md)에 설명된 대로 자격 증명을 사용하여 Azure 리소스에 Runbook에 대한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-162">In this case, it is being used to provide authentication for a runbook to Azure resources as described in [Authenticate Runbooks with Azure AD User account](automation-create-aduser-account.md).</span></span>  <span data-ttu-id="27c4d-163">첫 번째 활동에서는 Azure 구독에 액세스할 수 있는 자격 증명을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-163">The first activity retrieves the credential that has access to the Azure subscription.</span></span>  <span data-ttu-id="27c4d-164">그런 다음 **Add-AzureAccount** 활동에서 이 자격 증명을 사용하여 이후의 모든 활동에 대한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-164">The **Add-AzureAccount** activity then uses this credential to provide authentication for any activities that come after it.</span></span>  <span data-ttu-id="27c4d-165">[Get-AutomationPSCredential](automation-graphical-authoring-intro.md#links-and-workflow) 에는 단일 개체가 필요하기 때문에 여기에서는 **파이프라인 링크** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-165">A [pipeline link](automation-graphical-authoring-intro.md#links-and-workflow) is here since **Get-AutomationPSCredential** is expecting a single object.</span></span>  

![캔버스에 자격 증명 추가](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a><span data-ttu-id="27c4d-167">DSC에서 PowerShell 자격 증명을 사용</span><span class="sxs-lookup"><span data-stu-id="27c4d-167">Using a PowerShell credential in DSC</span></span>
<span data-ttu-id="27c4d-168">Azure 자동화에서 DSC 구성은 **Get-AutomationPSCredential**을 사용하여 자격 증명 자산을 참조할 수 있지만 원하는 경우 자격 증명 자산은 매개 변수를 통해 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c4d-168">While DSC configurations in Azure Automation can reference credential assets using **Get-AutomationPSCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="27c4d-169">자세한 내용은 [Azure 자동화 DSC에서 구성을 컴파일](automation-dsc-compile.md#credential-assets)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27c4d-169">For more information, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md#credential-assets).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27c4d-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27c4d-170">Next Steps</span></span>
* <span data-ttu-id="27c4d-171">그래픽 작성 링크에 대해 자세히 알아보려면 [그래픽 작성 링크](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="27c4d-171">To learn more about links in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="27c4d-172">자동자동화가 포함된 다양한 메서드를 이해하려면 [Azure 자동화 보안](automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="27c4d-172">To understand the different authentication methods with Automation, see [Azure Automation Security](automation-security-overview.md)</span></span>
* <span data-ttu-id="27c4d-173">그래픽 Runbook을 시작하려면 [내 첫 번째 그래픽 Runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="27c4d-173">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="27c4d-174">PowerShell 워크플로 Runbook을 시작하려면 [내 첫 번째 PowerShell 워크플로 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="27c4d-174">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span> 

