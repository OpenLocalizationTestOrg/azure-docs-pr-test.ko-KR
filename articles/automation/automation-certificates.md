---
title: "Azure 자동화의 인증서 자산 | Microsoft Docs"
description: "인증서는 Azure 자동화에 안전하게 저장되어 Azure 및 타사 리소스에 대해 인증하는 runbook과 DSC 구성에 액세스할 수 있게 합니다.  이 문서에서는 인증서에 대해 자세히 알아보고 텍스트 작성과 그래픽 작성 모두에서 인증서를 사용하는 방법을 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="5a284-104">Azure 자동화의 인증서 자산</span><span class="sxs-lookup"><span data-stu-id="5a284-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="5a284-105">인증서는 Azure Automation에 안전하게 저장되어 runbook 또는 DSC 구성이 Azure Resource Manager 리소스에 대한 **Get-AzureRmAutomationRmCertificate** 활동을 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="5a284-106">인증에 대한 인증서를 사용하는 runboo과 DSC 구성을 만들거나 Azure 또는 타사 리소스에 추가할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="5a284-107">Azure 자동화의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="5a284-108">이러한 자산은 각 자동화 계정에 대해 생성되는 고유 키를 사용하여 암호화되고 Azure 자동화에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="5a284-109">이 키는 마스터 인증서로 암호화되어 Azure 자동화에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="5a284-110">자동화 계정에 대한 키는 보안 자산을 저장하기 전에 마스터 인증서를 사용하여 암호가 해독된 후 자산을 암호화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="5a284-111">Windows PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="5a284-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="5a284-112">다음 표의 cmdlet은 Windows PowerShell을 사용하여 자동화 인증서 자산을 만들고 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="5a284-113">자동화 runbook과 DSC 구성에 사용할 수 있는 [Azure PowerShell 모듈](../powershell-install-configure.md) 의 일부로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="5a284-114">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="5a284-114">Cmdlets</span></span>|<span data-ttu-id="5a284-115">설명</span><span class="sxs-lookup"><span data-stu-id="5a284-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="5a284-116">Get AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="5a284-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="5a284-117">Runbook 또는 DSC 구성에 사용할 인증서 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="5a284-118">Get-AutomationCertificate 활동에서는 인증서 자체만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="5a284-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="5a284-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="5a284-120">Azure Automation으로 새 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="5a284-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="5a284-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="5a284-122">Azure 자동화에서 인증서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="5a284-123">Azure Automation으로 새 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="5a284-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="5a284-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="5a284-125">인증서 파일 업로드 및 .pfx 암호 설정을 포함하여 기존 인증서에 대한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="5a284-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="5a284-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="5a284-127">지정된 클라우드 서비스에 대한 서비스 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="5a284-128">새 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="5a284-128">Creating a new certificate</span></span>

<span data-ttu-id="5a284-129">새 인증서를 만들 때 .cer 또는 .pfx 파일을 Azure 자동화에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="5a284-130">인증서를 내보내기 가능한 것으로 표시한 경우 Azure 자동화 인증서 저장소 외부로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="5a284-131">내보낼 수 없는 경우, runbook 또는 DSC 구성내 에서 사용할 수 있는 것만 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="5a284-132">Azure 포털을 사용하여 새 인증서를 만들려면</span><span class="sxs-lookup"><span data-stu-id="5a284-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="5a284-133">Automation 계정에서 **자산** 타일을 클릭하여 **자산** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="5a284-134">**인증서** 타일을 클릭하여 **인증서** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="5a284-135">블레이드의 위쪽에서 **인증서 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="5a284-136">**이름** 상자에 인증서 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="5a284-137">**인증서 파일 업로드** 아래에서 **파일 선택**을 클릭하여 .cer 또는 .pfx 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="5a284-138">.pfx 파일을 선택한 경우 암호 및 내보내기 허용 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="5a284-139">**만들기** 를 클릭하여 새 인증서 자산을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="5a284-140">Windows PowerShell을 사용하여 새 인증서를 만들려면</span><span class="sxs-lookup"><span data-stu-id="5a284-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="5a284-141">다음 예제에서는 새 Automation 인증서를 만들고 내보내기 가능한 것으로 표시하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="5a284-142">이 예제에서는 기존 .pfx 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="5a284-143">인증서 사용</span><span class="sxs-lookup"><span data-stu-id="5a284-143">Using a certificate</span></span>

<span data-ttu-id="5a284-144">**Get-AutomationCertificate** 활동만 사용하여 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="5a284-145">[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet은 인증서 자산에 대한 정보를 반환하지만 인증서 자체는 반환하지 않으므로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="5a284-146">텍스트 Runbook 샘플</span><span class="sxs-lookup"><span data-stu-id="5a284-146">Textual runbook sample</span></span>

<span data-ttu-id="5a284-147">다음 샘플 코드에서는 Runbook에서 클라우드 서비스에 인증서를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="5a284-148">이 샘플에서는 암호화된 자동화 변수에서 암호를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="5a284-149">그래픽 Runbook 샘플</span><span class="sxs-lookup"><span data-stu-id="5a284-149">Graphical runbook sample</span></span>

<span data-ttu-id="5a284-150">그래픽 편집기의 라이브러리 창에서 인증서를 마우스 오른쪽 단추로 클릭하고 **캔버스에 추가**를 선택하여 **Get-AutomationCertificate**를 그래픽 Runbook에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![캔버스에 인증서 추가](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="5a284-152">다음 그림에서는 그래픽 Runbook에서 인증서를 사용하는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="5a284-153">이 예제는 텍스트 Runbook에서 클라우드 서비스에 인증서를 추가하는 위의 예제와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="5a284-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="5a284-154">그래픽 작성 예제</span><span class="sxs-lookup"><span data-stu-id="5a284-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="5a284-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a284-155">Next steps</span></span>

- <span data-ttu-id="5a284-156">Runbook이 수행하도록 설계된 활동의 논리적 흐름을 제어하도록 링크로 작업하는 방법에 대한 자세한 정보는 [그래픽 작성의 링크](automation-graphical-authoring-intro.md#links-and-workflow)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a284-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
