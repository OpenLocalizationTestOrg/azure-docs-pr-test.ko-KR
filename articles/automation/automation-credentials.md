---
title: "Azure 자동화에서 aaaCredential 자산 | Microsoft Docs"
description: "Azure 자동화에서 자격 증명 자산 사용된 tooauthenticate tooresources hello runbook 또는 DSC 구성에 액세스할 수 있는 보안 자격 증명을 포함 합니다. 이 문서에서는 toocreate 자산 자격 증명 하 고 runbook 또는 DSC 구성을 사용 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a><span data-ttu-id="980ea-104">Azure 자동화의 자격 증명 자산</span><span class="sxs-lookup"><span data-stu-id="980ea-104">Credential assets in Azure Automation</span></span>
<span data-ttu-id="980ea-105">자동화 자격 증명 자산은 사용자 이름과 암호 등의 보안 자격 증명을 포함하는 [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 개체를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-105">An Automation credential asset holds a [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential)  object which contains security credentials such as a username and password.</span></span> <span data-ttu-id="980ea-106">Hello 사용자 이름 및 hello PSCredential 개체 tooprovide toosome 응용 프로그램의 암호 또는 인증을 요구 하는 서비스를 추출할 수 있습니다 또는 Runbook 및 DSC 구성을 인증용으로 PSCredential 개체를 허용 하는 cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-106">Runbooks and DSC configurations may use cmdlets that accept a PSCredential object for authentication, or they may extract hello username and password of hello PSCredential object tooprovide toosome application or service requiring authentication.</span></span> <span data-ttu-id="980ea-107">hello 자격 증명에 대 한 Azure 자동화에 안전 하 게 저장 된 속성과 hello runbook 또는 hello로 DSC 구성에 액세스할 수 [Get-automationpscredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-107">hello properties for a credential are stored securely in Azure Automation and can be accessed in hello runbook or DSC configuration with hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) activity.</span></span>

> [!NOTE]
> <span data-ttu-id="980ea-108">Azure 자동화의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-108">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="980ea-109">이러한 자산 암호화 및 hello 각 자동화 계정에 대해 생성 되는 고유 키를 사용 하 여 Azure 자동화에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-109">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="980ea-110">이 키는 마스터 인증서로 암호화되어 Azure 자동화에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-110">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="980ea-111">보안 자산을 저장 하기 전에 hello 자동화 계정에 대 한 hello 키 hello 마스터 인증서를 사용 하 여 암호가 해독 됩니다와 tooencrypt hello 자산을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-111">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>  

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="980ea-112">Windows PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="980ea-112">Windows PowerShell cmdlets</span></span>
<span data-ttu-id="980ea-113">다음 표에 hello의 hello cmdlet 사용 되는 toocreate 됩니다 하 고 Windows PowerShell을 사용 하 여 자동화 자격 증명 자산을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-113">hello cmdlets in hello following table are used toocreate and manage automation credential assets with Windows PowerShell.</span></span>  <span data-ttu-id="980ea-114">Hello의 일부분으로 제공 [Azure PowerShell 모듈](/powershell/azure/overview) 자동화 runbook 및 DSC 구성에 사용 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-114">They ship as part of hello [Azure PowerShell module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span></span>

| <span data-ttu-id="980ea-115">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="980ea-115">Cmdlets</span></span> | <span data-ttu-id="980ea-116">설명</span><span class="sxs-lookup"><span data-stu-id="980ea-116">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="980ea-117">Get-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="980ea-117">Get-AzureAutomationCredential</span></span>](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="980ea-118">자격 증명 자산에 대한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-118">Retrieves information about a credential asset.</span></span> <span data-ttu-id="980ea-119">Hello 자격 증명 자체에 정보만 검색할 수 있습니다에서 **Get-automationpscredential** 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-119">You can only retrieve hello credential itself from **Get-AutomationPSCredential** activity.</span></span> |
| [<span data-ttu-id="980ea-120">New-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="980ea-120">New-AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="980ea-121">새 자동화 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-121">Creates a new Automation credential.</span></span> |
| [<span data-ttu-id="980ea-122">Remove- AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="980ea-122">Remove- AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="980ea-123">자동화 자격 증명을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-123">Removes an Automation credential.</span></span> |
| [<span data-ttu-id="980ea-124">Set- AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="980ea-124">Set- AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="980ea-125">집합 hello 기존 자동화 자격 증명에 대 한 속성.</span><span class="sxs-lookup"><span data-stu-id="980ea-125">Sets hello properties for an existing Automation credential.</span></span> |

## <a name="runbook-activities"></a><span data-ttu-id="980ea-126">Runbook 활동</span><span class="sxs-lookup"><span data-stu-id="980ea-126">Runbook activities</span></span>
<span data-ttu-id="980ea-127">hello 활동 hello 표 다음에 runbook 및 DSC 구성에 사용 되는 tooaccess 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="980ea-127">hello activities in hello following table are used tooaccess credentials in a runbook and DSC configurations.</span></span>

| <span data-ttu-id="980ea-128">활동</span><span class="sxs-lookup"><span data-stu-id="980ea-128">Activities</span></span> | <span data-ttu-id="980ea-129">설명</span><span class="sxs-lookup"><span data-stu-id="980ea-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="980ea-130">Get-AutomationPSCredential</span><span class="sxs-lookup"><span data-stu-id="980ea-130">Get-AutomationPSCredential</span></span> |<span data-ttu-id="980ea-131">Runbook 또는 DSC 구성에서 자격 증명 toouse를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-131">Gets a credential toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="980ea-132">[System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-132">Returns a [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) object.</span></span> |

> [!NOTE]
> <span data-ttu-id="980ea-133">변수를 사용 하면 안 hello – Get-automationpscredential runbook 또는 DSC 구성 간의 종속성을 검색 하기가 어려워질 하 고 자격 증명 자산을 디자인 타임에이의 Name 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-133">You should avoid using variables in hello –Name parameter of Get-AutomationPSCredential since this can complicate discovering dependencies between runbooks or DSC configurations, and credential assets at design time.</span></span>
> 
> 

## <a name="creating-a-new-credential-asset"></a><span data-ttu-id="980ea-134">새 자격 증명 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="980ea-134">Creating a new credential asset</span></span>

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a><span data-ttu-id="980ea-135">Azure 포털 hello로 새 자격 증명 자산 toocreate</span><span class="sxs-lookup"><span data-stu-id="980ea-135">toocreate a new credential asset with hello Azure portal</span></span>
1. <span data-ttu-id="980ea-136">자동화 계정에서 클릭 hello **자산** 부분 tooopen hello **자산** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-136">From your automation account, click hello **Assets** part tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="980ea-137">Hello 클릭 **자격 증명** 부분 tooopen hello **자격 증명** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-137">Click hello **Credentials** part tooopen hello **Credentials** blade.</span></span>
3. <span data-ttu-id="980ea-138">클릭 **자격 증명 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-138">Click **Add a credential** at hello top of hello blade.</span></span>
4. <span data-ttu-id="980ea-139">Hello 양식을 작성 하 고 클릭 **만들기** toosave hello 새 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-139">Complete hello form and click **Create** toosave hello new credential.</span></span>

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a><span data-ttu-id="980ea-140">Windows PowerShell과 함께 새 자격 증명 자산 toocreate</span><span class="sxs-lookup"><span data-stu-id="980ea-140">toocreate a new credential asset with Windows PowerShell</span></span>
<span data-ttu-id="980ea-141">hello 다음 명령 예제에서는 toocreate 새 자동화 자격 증명 하는 방법</span><span class="sxs-lookup"><span data-stu-id="980ea-141">hello following sample commands show how toocreate a new automation credential.</span></span> <span data-ttu-id="980ea-142">PSCredential 개체를 먼저 hello 이름 및 암호 만들어지고 toocreate hello 자격 증명 자산을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-142">A PSCredential object is first created with hello name and password and then used toocreate hello credential asset.</span></span> <span data-ttu-id="980ea-143">또는 hello를 사용할 수 있습니다 **Get-credential** cmdlet toobe tootype 이름 및 암호를 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-143">Alternatively, you could use hello **Get-Credential** cmdlet toobe prompted tootype in a name and password.</span></span>

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a><span data-ttu-id="980ea-144">Azure 클래식 포털 hello로 새 자격 증명 자산 toocreate</span><span class="sxs-lookup"><span data-stu-id="980ea-144">toocreate a new credential asset with hello Azure classic portal</span></span>
1. <span data-ttu-id="980ea-145">자동화 계정에서 클릭 **자산** hello 창의 위쪽에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-145">From your automation account, click **Assets** at hello top of hello window.</span></span>
2. <span data-ttu-id="980ea-146">Hello hello 창의 아래쪽에 있는 클릭 **설정 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-146">At hello bottom of hello window, click **Add Setting**.</span></span>
3. <span data-ttu-id="980ea-147">**자격 증명 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-147">Click **Add Credential**.</span></span>
4. <span data-ttu-id="980ea-148">Hello에 **자격 증명 형식을** 드롭다운 **PowerShell 자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-148">In hello **Credential Type** dropdown, select **PowerShell Credential**.</span></span>
5. <span data-ttu-id="980ea-149">Hello 마법사를 완료 하 고 hello 확인란 toosave hello 새 자격 증명을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-149">Complete hello wizard and click hello checkbox toosave hello new credential.</span></span>

## <a name="using-a-powershell-credential"></a><span data-ttu-id="980ea-150">PowerShell 자격 증명 사용</span><span class="sxs-lookup"><span data-stu-id="980ea-150">Using a PowerShell credential</span></span>
<span data-ttu-id="980ea-151">Runbook 또는 hello로 DSC 구성에서 자격 증명 자산을 검색할 **Get-automationpscredential** 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-151">You retrieve a credential asset in a runbook or DSC configuration with hello **Get-AutomationPSCredential** activity.</span></span> <span data-ttu-id="980ea-152">그러면 PSCredential 매개 변수가 필요한 활동 또는 cmdlet에서 사용할 수 있는 [PSCredential 개체](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) 가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-152">This returns a [PSCredential object](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) that you can use with an activity or cmdlet that requires a PSCredential parameter.</span></span> <span data-ttu-id="980ea-153">또한 hello 자격 증명 개체 toouse의 hello 속성을 개별적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-153">You can also retrieve hello properties of hello credential object toouse individually.</span></span> <span data-ttu-id="980ea-154">hello 개체에 대 한 속성이 hello 사용자 이름과 암호를 보안 하는 hello 하거나 hello를 사용할 수 있습니다 **GetNetworkCredential** 메서드 tooreturn는 [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) 는 보안 되지 않은 제공 하는 개체 hello 암호의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-154">hello object has a property for hello username and hello secure password, or you can use hello **GetNetworkCredential** method tooreturn a [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) object that will provide an unsecured version of hello password.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="980ea-155">텍스트 Runbook 샘플</span><span class="sxs-lookup"><span data-stu-id="980ea-155">Textual runbook sample</span></span>
<span data-ttu-id="980ea-156">hello 다음 명령 예제에서는 toouse는 PowerShell runbook에서 자격 증명 하는 방법</span><span class="sxs-lookup"><span data-stu-id="980ea-156">hello following sample commands show how toouse a PowerShell credential in a runbook.</span></span> <span data-ttu-id="980ea-157">이 예제에서는 hello 자격 증명 검색 되 고 해당 사용자 이름과 암호가 toovariables 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-157">In this example, hello credential is retrieved and its username and password assigned toovariables.</span></span>

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a><span data-ttu-id="980ea-158">그래픽 Runbook 샘플</span><span class="sxs-lookup"><span data-stu-id="980ea-158">Graphical runbook sample</span></span>
<span data-ttu-id="980ea-159">추가한는 **Get-automationpscredential** hello 자격 증명을 선택 하 고 hello 그래픽 편집기의 hello 라이브러리 창에서 마우스 오른쪽 단추로 클릭 하 여 활동 tooa 그래픽 runbook **toocanvas 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-159">You add a **Get-AutomationPSCredential** activity tooa graphical runbook by right-clicking on hello credential in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![자격 증명 toocanvas 추가](media/automation-credentials/credential-add-canvas.png)

<span data-ttu-id="980ea-161">hello 다음 이미지의 예가 나와 그래픽 runbook에서 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-161">hello following image shows an example of using a credential in a graphical runbook.</span></span>  <span data-ttu-id="980ea-162">이 경우에 있어 runbook tooAzure 리소스에 대 한 사용된 tooprovide 인증에 설명 된 대로 [Azure AD 사용자 계정으로 인증 Runbook](automation-create-aduser-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-162">In this case, it is being used tooprovide authentication for a runbook tooAzure resources as described in [Authenticate Runbooks with Azure AD User account](automation-create-aduser-account.md).</span></span>  <span data-ttu-id="980ea-163">첫 번째 활동 hello 액세스 toohello Azure 구독 hello 자격 증명을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-163">hello first activity retrieves hello credential that has access toohello Azure subscription.</span></span>  <span data-ttu-id="980ea-164">hello **Add-azureaccount** 작업 뒤에 오는 모든 활동에 대 한 다음이 자격 증명 tooprovide 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-164">hello **Add-AzureAccount** activity then uses this credential tooprovide authentication for any activities that come after it.</span></span>  <span data-ttu-id="980ea-165">[Get-AutomationPSCredential](automation-graphical-authoring-intro.md#links-and-workflow) 에는 단일 개체가 필요하기 때문에 여기에서는 **파이프라인 링크** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-165">A [pipeline link](automation-graphical-authoring-intro.md#links-and-workflow) is here since **Get-AutomationPSCredential** is expecting a single object.</span></span>  

![자격 증명 toocanvas 추가](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a><span data-ttu-id="980ea-167">DSC에서 PowerShell 자격 증명을 사용</span><span class="sxs-lookup"><span data-stu-id="980ea-167">Using a PowerShell credential in DSC</span></span>
<span data-ttu-id="980ea-168">Azure 자동화에서 DSC 구성은 **Get-AutomationPSCredential**을 사용하여 자격 증명 자산을 참조할 수 있지만 원하는 경우 자격 증명 자산은 매개 변수를 통해 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="980ea-168">While DSC configurations in Azure Automation can reference credential assets using **Get-AutomationPSCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="980ea-169">자세한 내용은 [Azure 자동화 DSC에서 구성을 컴파일](automation-dsc-compile.md#credential-assets)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="980ea-169">For more information, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md#credential-assets).</span></span>

## <a name="next-steps"></a><span data-ttu-id="980ea-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="980ea-170">Next Steps</span></span>
* <span data-ttu-id="980ea-171">참조 링크 그래픽 제작에 대 한 자세한 정보는 toolearn [그래픽 제작에 대 한 링크](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="980ea-171">toolearn more about links in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="980ea-172">자동화를 toounderstand hello 다른 인증 방법을 참조 [Azure 자동화의 보안](automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="980ea-172">toounderstand hello different authentication methods with Automation, see [Azure Automation Security](automation-security-overview.md)</span></span>
* <span data-ttu-id="980ea-173">그래픽 runbook 시작 tooget 참조 [내 첫 번째 그래픽 runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="980ea-173">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="980ea-174">PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="980ea-174">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span> 

