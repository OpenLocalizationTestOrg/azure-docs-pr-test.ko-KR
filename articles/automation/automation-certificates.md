---
title: "Azure 자동화에서 aaaCertificate 자산 | Microsoft Docs"
description: "인증서는 runbook 또는 Azure 및 타사 리소스에 대해 DSC 구성 tooauthenticate 액세스할 수 있도록 Azure 자동화에 안전 하 게 저장할 수 있습니다.  이 문서에서는 인증서의 hello 세부 정보를 설명 방법과 텍스트와 그래픽 제작에 이러한 toowork 합니다."
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
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="2a68b-104">Azure 자동화의 인증서 자산</span><span class="sxs-lookup"><span data-stu-id="2a68b-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="2a68b-105">인증서에에서 저장할 수 안전 하 게 Azure 자동화 runbook 또는 hello를 사용 하 여 DSC 구성을 액세스할 수 있도록 **Get AzureRmAutomationRmCertificate** Azure 리소스 관리자 리소스에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="2a68b-106">이 toocreate runbook 및 인증에 인증서를 사용 하는 DSC 구성을 사용 하면 또는 tooAzure 또는 타사 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="2a68b-107">Azure 자동화의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="2a68b-108">이러한 자산 암호화 및 hello 각 자동화 계정에 대해 생성 되는 고유 키를 사용 하 여 Azure 자동화에에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="2a68b-109">이 키는 마스터 인증서로 암호화되어 Azure 자동화에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="2a68b-110">보안 자산을 저장 하기 전에 hello 자동화 계정에 대 한 hello 키 hello 마스터 인증서를 사용 하 여 암호가 해독 됩니다와 tooencrypt hello 자산을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="2a68b-111">Windows PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="2a68b-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="2a68b-112">다음 표에 hello의 hello cmdlet 사용 되는 toocreate 됩니다 하 고 Windows PowerShell을 사용 하 여 자동화 인증서 자산을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="2a68b-113">Hello의 일부분으로 제공 [Azure PowerShell 모듈](../powershell-install-configure.md) 자동화 runbook 및 DSC 구성에 사용 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="2a68b-114">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="2a68b-114">Cmdlets</span></span>|<span data-ttu-id="2a68b-115">설명</span><span class="sxs-lookup"><span data-stu-id="2a68b-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="2a68b-116">Get AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="2a68b-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="2a68b-117">Runbook 또는 DSC 구성에서 인증서 toouse에 대 한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="2a68b-118">Get-automationcertificate 작업에서 hello 인증서 자체 에서만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="2a68b-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="2a68b-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="2a68b-120">Azure Automation으로 새 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="2a68b-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="2a68b-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="2a68b-122">Azure 자동화에서 인증서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="2a68b-123">Azure Automation으로 새 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="2a68b-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="2a68b-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="2a68b-125">업로드 hello 인증서 파일 및.pfx에 대 한 hello 암호 설정 포함 하 여 기존 인증서에 대 한 hello 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="2a68b-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="2a68b-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="2a68b-127">Hello에 대 한 서비스 인증서 업로드 클라우드 서비스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="2a68b-128">새 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="2a68b-128">Creating a new certificate</span></span>

<span data-ttu-id="2a68b-129">새 인증서를 만들 때 자동화를.cer 또는.pfx 파일 tooAzure 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="2a68b-130">Hello 인증서를 내보낼 수 있도록 표시 하는 경우 다음를 전송할 수 있습니다 hello Azure 자동화 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="2a68b-131">내보낼 수 없는 경우 다음만 사용할 수 있습니다 hello runbook 또는 DSC 구성 내에서 서명에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="2a68b-132">Azure 포털 hello로 새 인증서를 toocreate</span><span class="sxs-lookup"><span data-stu-id="2a68b-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="2a68b-133">자동화 계정에서 클릭 hello **자산** 타일 tooopen hello **자산** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="2a68b-134">Hello 클릭 **인증서** 타일 tooopen hello **인증서** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="2a68b-135">클릭 **인증서 추가** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="2a68b-136">Hello에 hello 인증서에 대 한 이름을 입력 **이름** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="2a68b-137">클릭 **파일 선택** 아래 **인증서 파일 업로드** toobrowse.cer 또는.pfx 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="2a68b-138">.Pfx 파일을 선택 하는 경우 암호 및 여부 허용 하도록 내보낸 toobe를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="2a68b-139">클릭 **만들기** toosave hello 새 인증서 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="2a68b-140">Windows PowerShell과 함께 새 인증서를 toocreate</span><span class="sxs-lookup"><span data-stu-id="2a68b-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="2a68b-141">hello 다음 예제에서는 어떻게 toocreate 새 자동화 인증서 하 고 내보낼 수 있도록 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="2a68b-142">이 예제에서는 기존 .pfx 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="2a68b-143">인증서 사용</span><span class="sxs-lookup"><span data-stu-id="2a68b-143">Using a certificate</span></span>

<span data-ttu-id="2a68b-144">Hello를 사용 해야 **Get-automationcertificate** 활동 toouse 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="2a68b-145">Hello를 사용할 수 없습니다 [Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet hello 인증서 자산 있지만 hello 인증서가 아닌 자체에 대 한 정보를 반환 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="2a68b-146">텍스트 Runbook 샘플</span><span class="sxs-lookup"><span data-stu-id="2a68b-146">Textual runbook sample</span></span>

<span data-ttu-id="2a68b-147">다음 샘플 코드는 hello 인증서 tooa tooadd 클라우드 runbook에서 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="2a68b-148">이 샘플에서는 hello 암호는 암호화 된 자동화 변수에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="2a68b-149">그래픽 Runbook 샘플</span><span class="sxs-lookup"><span data-stu-id="2a68b-149">Graphical runbook sample</span></span>

<span data-ttu-id="2a68b-150">추가한는 **Get-automationcertificate** hello 인증서 hello 그래픽 편집기 및 선택의 hello 라이브러리 창에서 마우스 오른쪽 단추로 클릭 하 여 그래픽 runbook tooa **toocanvas 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![인증서 toohello 캔버스 추가](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="2a68b-152">hello 다음 이미지의 예가 나와 그래픽 runbook에서 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="2a68b-153">이 hello 텍스트 runbook에서 인증서 tooa 클라우드 서비스를 추가 하는 데 위에 표시 된 동일한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="2a68b-154">그래픽 작성 예제</span><span class="sxs-lookup"><span data-stu-id="2a68b-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="2a68b-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a68b-155">Next steps</span></span>

- <span data-ttu-id="2a68b-156">활동의 링크 toocontrol hello 논리적 흐름 runbook 작업에 대 한 자세한 toolearn 설계 tooperform를 참조 [그래픽 제작에 대 한 링크](automation-graphical-authoring-intro.md#links-and-workflow)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a68b-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
