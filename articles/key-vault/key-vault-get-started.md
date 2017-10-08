---
title: "Azure 키 자격 증명 모음 시작 aaaGet | Microsoft Docs"
description: "이 자습서 toohelp 얻게를 사용 하 여 azure에서 toostore 강화 된 컨테이너를 Azure 키 자격 증명 모음 toocreate와 시작 및 암호화 키 및 Azure에서 암호 관리 합니다."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a><span data-ttu-id="8e828-103">Azure 주요 자격 증명 모음 시작</span><span class="sxs-lookup"><span data-stu-id="8e828-103">Get started with Azure Key Vault</span></span>
<span data-ttu-id="8e828-104">Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="8e828-105">자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="8e828-106">소개</span><span class="sxs-lookup"><span data-stu-id="8e828-106">Introduction</span></span>
<span data-ttu-id="8e828-107">이 자습서 toohelp 얻게를 사용 하 여 toostore Azure에서 확정 된 컨테이너 (볼트)을 Azure 주요 자격 증명 모음 toocreate를 시작 하 고 암호화 키 및 Azure에서 암호 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="8e828-108">이 과정을 보여 줍니다 hello toocreate Azure PowerShell을 사용 하 여 키 또는 암호 Azure 응용 프로그램과 함께 사용할 수 있는 포함 된 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-108">It walks you through hello process of using Azure PowerShell toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="8e828-109">그런 다음 응용 프로그램이 해당 키 또는 암호를 사용할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-109">It then shows you how an application can use that key or password.</span></span>

<span data-ttu-id="8e828-110">**예상 시간 toocomplete:** 20 분</span><span class="sxs-lookup"><span data-stu-id="8e828-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="8e828-111">이 자습서는 어떻게 toowrite hello hello 단계 중 하나를 포함 하는 Azure 응용 프로그램, 즉 어떻게 tooauthorize 응용 프로그램 toouse 키 또는 암호에 hello 키 자격 증명 모음에 대 한 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-111">This tutorial does not include instructions for how toowrite hello Azure application that one of hello steps includes, namely how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="8e828-112">이 자습서에서는 Azure PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-112">This tutorial uses Azure PowerShell.</span></span> <span data-ttu-id="8e828-113">플랫폼 간 명령줄 인터페이스 지침은 [이 해당 자습서](key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e828-113">For Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
>

<span data-ttu-id="8e828-114">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="8e828-114">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e828-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8e828-115">Prerequisites</span></span>
<span data-ttu-id="8e828-116">toocomplete이이 자습서에서는 다음 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-116">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="8e828-117">구독 tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="8e828-117">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="8e828-118">아직 구독이 없는 경우 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-118">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8e828-119">Azure PowerShell, **최소 버전 1.1.0**.</span><span class="sxs-lookup"><span data-stu-id="8e828-119">Azure PowerShell, **minimum version of 1.1.0**.</span></span> <span data-ttu-id="8e828-120">Azure PowerShell tooinstall Azure 구독과 연결을 참조 하세요 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-120">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="8e828-121">Azure PowerShell을 이미 설치 되어 있는 hello Azure PowerShell 콘솔에서 hello 버전 알지 못할 경우 입력 `(Get-Module azure -ListAvailable).Version`합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-121">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span> <span data-ttu-id="8e828-122">Azure PowerShell 버전 0.9.1 ~ 0.9.8이 설치된 경우, 일부 약간의 변경이 있지만 이 자습서를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-122">When you have Azure PowerShell version 0.9.1 through 0.9.8 installed, you can still use this tutorial with some minor changes.</span></span> <span data-ttu-id="8e828-123">Hello를 사용 해야 하는 예를 들어 `Switch-AzureMode AzureResourceManager` 명령 및 hello Azure 키 자격 증명 모음 명령 중 일부 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-123">For example, you must use hello `Switch-AzureMode AzureResourceManager` command and some of hello Azure Key Vault commands have changed.</span></span> <span data-ttu-id="8e828-124">목록이 hello 버전 0.9.8 통해 0.9.1 키 자격 증명 모음 cmdlet에 대 한 참조 [Azure 키 자격 증명 모음 Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-124">For a list of hello Key Vault cmdlets for versions 0.9.1 through 0.9.8, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>
* <span data-ttu-id="8e828-125">응용 프로그램 구성된 toouse hello 키 또는 암호를이 자습서에서 만드는 됩니다입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-125">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="8e828-126">샘플 응용 프로그램은 hello에서 사용할 수 있는 [Microsoft 다운로드 센터](http://www.microsoft.com/en-us/download/details.aspx?id=45343)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-126">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span> <span data-ttu-id="8e828-127">추가 정보 파일을 함께 제공 된 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8e828-127">For instructions, see hello accompanying Readme file.</span></span>

<span data-ttu-id="8e828-128">이 자습서는 Azure PowerShell 초보자를 위한 만들어졌지만 모듈, cmdlet 및 세션 같은 hello 기본 개념을 이해 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-128">This tutorial is designed for Azure PowerShell beginners, but it assumes that you understand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="8e828-129">자세한 내용은 [Windows PowerShell 시작](https://technet.microsoft.com/library/hh857337.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e828-129">For more information, see [Getting started with Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="8e828-130">자세한이 자습서를 사용 하 여 hello에서 볼 수 있는 모든 cmdlet에 대 한 도움말을 tooget **Get-help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8e828-130">tooget detailed help for any cmdlet that you see in this tutorial, use hello **Get-Help** cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="8e828-131">예를 들어 hello에 대 한 도움말을 tooget **로그인 AzureRmAccount** cmdlet, 유형:</span><span class="sxs-lookup"><span data-stu-id="8e828-131">For example, tooget help for hello **Login-AzureRmAccount** cmdlet, type:</span></span>

    Get-Help Login-AzureRmAccount -Detailed

<span data-ttu-id="8e828-132">또한 다음 Azure PowerShell에서 Azure 리소스 관리자와 친숙 한 자습서 tooget hello를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-132">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure PowerShell:</span></span>

* [<span data-ttu-id="8e828-133">어떻게 tooinstall Azure PowerShell 및 구성</span><span class="sxs-lookup"><span data-stu-id="8e828-133">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="8e828-134">리소스 관리자로 Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="8e828-134">Using Azure PowerShell with Resource Manager</span></span>](../powershell-azure-resource-manager.md)

## <span data-ttu-id="8e828-135"><a id="connect"></a>Tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="8e828-135"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="8e828-136">Azure PowerShell 세션을 시작 하 고 다음 명령을 hello로 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-136">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="8e828-137">예를 들어 Azure Government Azure의 특정 인스턴스를 사용 하는 경우 사용 하 여 hello-이 명령 사용 하 여 환경 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-137">Note that if you are using a specific instance of Azure, for example, Azure Government, use hello -Environment parameter with this command.</span></span> <span data-ttu-id="8e828-138">예: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`</span><span class="sxs-lookup"><span data-stu-id="8e828-138">For example: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`</span></span>

<span data-ttu-id="8e828-139">Hello 팝업 브라우저 창에서 Azure 계정 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-139">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="8e828-140">Azure PowerShell을이 계정 및 기본적으로 관련 된 모든 hello 등록이 사용 하 여 첫 번째 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-140">Azure PowerShell gets all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="8e828-141">구독이 여러 개 있고 Azure 키 자격 증명 모음에 대 한 특정 한 toouse toospecify 원하는 hello toosee hello 구독 계정에 대해 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-141">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="8e828-142">그런 다음 toospecify hello 구독 toouse, 유형:</span><span class="sxs-lookup"><span data-stu-id="8e828-142">Then, toospecify hello subscription toouse, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

<span data-ttu-id="8e828-143">Azure PowerShell을 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-143">For more information about configuring Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="8e828-144"><a id="resource"></a>새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8e828-144"><a id="resource"></a>Create a new resource group</span></span>
<span data-ttu-id="8e828-145">Azure 리소스 관리자를 사용하면 관련된 모든 리소스는 리소스 그룹의 내부에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-145">When you use Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="8e828-146">이 자습서에서는 **ContosoResourceGroup** 이라는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-146">We will create a new resource group named **ContosoResourceGroup** for this tutorial:</span></span>

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <span data-ttu-id="8e828-147"><a id="vault"></a>키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="8e828-147"><a id="vault"></a>Create a key vault</span></span>
<span data-ttu-id="8e828-148">사용 하 여 hello [새로 AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate 주요 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-148">Use hello [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate a key vault.</span></span> <span data-ttu-id="8e828-149">이 cmdlet에는 세 가지 필수 매개 변수:는 **리소스 그룹 이름은**, **주요 자격 증명 모음 이름**, hello 및 **지리적 위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-149">This cmdlet has three mandatory parameters: a **resource group name**, a **key vault name**, and hello **geographic location**.</span></span>

<span data-ttu-id="8e828-150">예를 들어, 자격 증명 모음 이름을 hello를 사용 하는 경우 **ContosoKeyVault**의 hello 리소스 그룹 이름은 **ContosoResourceGroup**, 및의 hello 위치 **동아시아**, 유형:</span><span class="sxs-lookup"><span data-stu-id="8e828-150">For example, if you use hello vault name of **ContosoKeyVault**, hello resource group name of **ContosoResourceGroup**, and hello location of **East Asia**, type:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

<span data-ttu-id="8e828-151">이 cmdlet의 출력 hello 방금 만든 hello 키 자격 증명 모음의 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-151">hello output of this cmdlet shows properties of hello key vault that you’ve just created.</span></span> <span data-ttu-id="8e828-152">hello 두 가장 중요 한 속성은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-152">hello two most important properties are:</span></span>

* <span data-ttu-id="8e828-153">**자격 증명 모음에 이름**: hello 예에서이 **ContosoKeyVault**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-153">**Vault Name**: In hello example, this is **ContosoKeyVault**.</span></span> <span data-ttu-id="8e828-154">다른 키 자격 증명 모음 cmdlet에 대해 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-154">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="8e828-155">**자격 증명 모음 URI**: hello 예제 https://contosokeyvault.vault.azure.net/입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-155">**Vault URI**: In hello example, this is https://contosokeyvault.vault.azure.net/.</span></span> <span data-ttu-id="8e828-156">REST API를 통해 사용자 자격 증명 모음을 사용하는 응용 프로그램은 URI를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="8e828-157">Azure 계정에 권한이 부여 된 tooperform이이 키에 대 한 모든 작업 자격 증명 모음에 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="8e828-158">아직 다른 사람은 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-158">As yet, nobody else is.</span></span>

> [!NOTE]
> <span data-ttu-id="8e828-159">Hello 오류가 나타나는 경우 **hello 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 'Microsoft.KeyVault'** toocreate 시도 하 여 새 키 자격 증명 모음을 실행 `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` 후 새로 AzureRmKeyVault 명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-159">If you see hello error **hello subscription is not registered toouse namespace 'Microsoft.KeyVault'** when you try toocreate your new key vault, run `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` and then rerun your New-AzureRmKeyVault command.</span></span> <span data-ttu-id="8e828-160">자세한 내용은 [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e828-160">For more information, see [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).</span></span>
>
>

## <span data-ttu-id="8e828-161"><a id="add"></a>키 또는 키 자격 증명 모음 보안 toohello 추가</span><span class="sxs-lookup"><span data-stu-id="8e828-161"><a id="add"></a>Add a key or secret toohello key vault</span></span>
<span data-ttu-id="8e828-162">Hello를 사용 하 여 Azure 키 자격 증명 모음 toocreate 소프트웨어 보호 키를 하려는 경우 [Add-azurekeyvaultkey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-162">If you want Azure Key Vault toocreate a software-protected key for you, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet, and type hello following:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

<span data-ttu-id="8e828-163">그러나에 기존 소프트웨어 보호 키 있으면는 합니다. PFX 파일을 저장 tooyour C:\ 드라이브 softkey.pfx tooupload tooAzure 형식 hello tooset hello 변수 다음 주요 자격 증명을 지정 하 라는 파일에 **securepfxpwd** 의 암호에 대 한 **123** hello에 대 한 합니다. PFX 파일:</span><span class="sxs-lookup"><span data-stu-id="8e828-163">However, if you have an existing software-protected key in a .PFX file saved tooyour C:\ drive in a file named softkey.pfx that you want tooupload tooAzure Key Vault, type hello following tooset hello variable **securepfxpwd** for a password of **123** for hello .PFX file:</span></span>

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

<span data-ttu-id="8e828-164">Hello hello에서 다음 tooimport hello 키를 입력 합니다. 소프트웨어 키 자격 증명 모음 서비스 hello에서 hello 키를 보호 하 PFX 파일:</span><span class="sxs-lookup"><span data-stu-id="8e828-164">Then type hello following tooimport hello key from hello .PFX file, which protects hello key by software in hello Key Vault service:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


<span data-ttu-id="8e828-165">이제는 작성 되거나 해당 URI를 사용 하 여 tooAzure 주요 자격 증명을 업로드 한이 키를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-165">You can now reference this key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="8e828-166">사용 하 여 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello 현재 버전을 가져오고 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget이 특정 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-166">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>  

<span data-ttu-id="8e828-167">이 키 형식에 대 한 toodisplay hello URI:</span><span class="sxs-lookup"><span data-stu-id="8e828-167">toodisplay hello URI for this key, type:</span></span>

    $Key.key.kid

<span data-ttu-id="8e828-168">먼저 tooadd는 비밀 toohello 자격 증명 모음 SQLPassword 라는 암호 이며 Pa$ $w0rd tooAzure 주요 자격 증명 모음 hello 값 hello 다음을 입력 하 여 Pa$ $w0rd tooa 보안 문자열의 hello 값을 변환:</span><span class="sxs-lookup"><span data-stu-id="8e828-168">tooadd a secret toohello vault, which is a password named SQLPassword and has hello value of Pa$$w0rd tooAzure Key Vault, first convert hello value of Pa$$w0rd tooa secure string by typing hello following:</span></span>

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

<span data-ttu-id="8e828-169">그런 다음 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-169">Then, type hello following:</span></span>

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

<span data-ttu-id="8e828-170">이제 해당 URI를 사용 하 여 tooAzure 자격 증명 모음 키를 추가 하는이 암호를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-170">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="8e828-171">사용 하 여 **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello 현재 버전을 가져오고 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget이 특정 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-171">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="8e828-172">이 암호 형식에 대 한 toodisplay hello URI:</span><span class="sxs-lookup"><span data-stu-id="8e828-172">toodisplay hello URI for this secret, type:</span></span>

    $secret.Id

<span data-ttu-id="8e828-173">Hello 키 또는 암호 방금 만든 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-173">Let’s view hello key or secret that you just created:</span></span>

* <span data-ttu-id="8e828-174">tooview 프로그램 키, 유형:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="8e828-174">tooview your key, type: `Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="8e828-175">tooview 비밀을 형식:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="8e828-175">tooview your secret, type: `Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`</span></span>

<span data-ttu-id="8e828-176">이제 주요 자격 증명 모음 및 키 또는 암호 응용 프로그램 toouse 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-176">Now, your key vault and key or secret is ready for applications toouse.</span></span> <span data-ttu-id="8e828-177">응용 프로그램 toouse에 권한을 부여 해야 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-177">You must authorize applications toouse them.</span></span>  

## <span data-ttu-id="8e828-178"><a id="register"></a>Azure Active Directory에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="8e828-178"><a id="register"></a>Register an application with Azure Active Directory</span></span>
<span data-ttu-id="8e828-179">이 단계는 일반적으로 별도의 컴퓨터에서 개발자가 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-179">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="8e828-180">특정 tooAzure 주요 자격 증명 되지만 여기서는 완전성을 위해.</span><span class="sxs-lookup"><span data-stu-id="8e828-180">It is not specific tooAzure Key Vault, but is included here for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e828-181">toocomplete hello 자습서, 계정, 자격 증명 모음 hello 및이 단계에서 등록 하는 hello 응용 프로그램 모두에 있어야 hello 같은 Azure 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-181">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="8e828-182">자격 증명 모음 키를 사용하는 응용 프로그램은 Azure Active Directory에서 토큰을 사용하여 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-182">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="8e828-183">toodo이,이 hello hello 응용 프로그램의 소유자가 Azure Active Directory에서 먼저 hello 응용 프로그램을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-183">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="8e828-184">등록의 hello 끝 hello 응용 프로그램 소유자 hello를 다음 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-184">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="8e828-185">**응용 프로그램 ID** (클라이언트 ID) 및 **인증 키** (라고도 hello 공유 암호).</span><span class="sxs-lookup"><span data-stu-id="8e828-185">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="8e828-186">hello 응용 프로그램 둘 다 이러한 값 tooAzure Active Directory tooget 토큰을 제시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-186">hello application must present both these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="8e828-187">Hello 응용 프로그램은 어떻게 구성 toodo hello 응용 프로그램에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-187">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="8e828-188">Hello 키 자격 증명 모음 샘플 응용 프로그램에 대 한 응용 프로그램 소유자 hello hello app.config 파일에 이러한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-188">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="8e828-189">Azure Active Directory에서 tooregister hello 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="8e828-189">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="8e828-190">Azure 클래식 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-190">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="8e828-191">Hello 왼쪽에서 클릭 **Active Directory**, 한 다음 응용 프로그램을 등록 하는 hello 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-191">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> <span data-ttu-id="8e828-192">**참고:** hello를 선택 해야 포함 된 같은 디렉터리 hello 주요 자격 증명 모음을 만들 때 사용한 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="8e828-192">**Note:** You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="8e828-193">알 수 없는 디렉터리가 인지, 클릭 **설정**, 주요 자격 증명 모음을 만들 때 사용한 hello 구독을 식별 하 고 hello 디렉터리의 참고 hello 이름이 hello 마지막 열에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-193">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>
3. <span data-ttu-id="8e828-194">**APPLICATIONS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-194">Click **APPLICATIONS**.</span></span> <span data-ttu-id="8e828-195">앱이 없습니다. tooyour 디렉터리를 추가한 경우이 페이지만 hello를 표시 하는 **앱 추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-195">If no apps have been added tooyour directory, this page shows only hello **Add an App** link.</span></span> <span data-ttu-id="8e828-196">Hello 링크를 클릭 하거나 클릭 수 있습니다 **추가** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-196">Click hello link, or alternatively, you can click **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="8e828-197">Hello에 **응용 프로그램 추가** hello에서 마법사 **하 신 toodo 원하는?** 페이지에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-197">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="8e828-198">Hello에 **응용 프로그램에 대해 알리기** 페이지, 응용 프로그램에 대 한 이름을 지정 하 고 다음 선택 **웹 응용 프로그램 및/또는 웹 API** (기본 hello).</span><span class="sxs-lookup"><span data-stu-id="8e828-198">On hello **Tell us about your application** page, specify a name for your application, and then select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="8e828-199">Hello 클릭 **다음** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-199">Click hello **Next** icon.</span></span>
6. <span data-ttu-id="8e828-200">Hello에 **앱 속성** 페이지에서 지정 하는 hello **로그온 URL** 및 **앱 ID URI** 웹 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-200">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="8e828-201">응용 프로그램에 이러한 값이 없는 경우 이 단계에서 만들 수 있습니다(예를 들어, 두 상자에 대해 http://test1.contoso.com을 지정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="8e828-201">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="8e828-202">이러한 사이트가 존재하는 경우 중요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-202">It does not matter if these sites exist.</span></span> <span data-ttu-id="8e828-203">중요 한 것은 각 응용 프로그램에 대 한 hello 앱 ID URI는 디렉터리의 모든 응용 프로그램에 대 한 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-203">What is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="8e828-204">hello 디렉터리는이 문자열 tooidentify 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-204">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="8e828-205">Hello 클릭 **완료** 아이콘 toosave hello 마법사에서 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-205">Click hello **Complete** icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="8e828-206">Hello에 **빠른 시작** 페이지 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-206">On hello **Quick Start** page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="8e828-207">Toohello 스크롤하여 **키** 섹션 hello 기간, 선택한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-207">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="8e828-208">hello 페이지가 새로 고쳐지고 키 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-208">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="8e828-209">이 키 값 및 hello 응용 프로그램을 구성 해야 **클라이언트 ID** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-209">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="8e828-210">(이 구성에 대한 지침은 응용 프로그램에 특정된 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="8e828-210">(Instructions for this configuration are application-specific.)</span></span>
10. <span data-ttu-id="8e828-211">다음 단계 tooset 권한을 hello에서 사용할 자격 증명 모음에 있는이 페이지에서 hello 클라이언트 ID 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-211">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <span data-ttu-id="8e828-212"><a id="authorize"></a>Hello 응용 프로그램 toouse hello 키 또는 암호를 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8e828-212"><a id="authorize"></a>Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="8e828-213">키 또는 암호에 hello 자격 증명 모음을 사용 하 여 tooauthorize hello 응용 프로그램 tooaccess hello는 [Set-azurermkeyvaultaccesspolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8e828-213">tooauthorize hello application tooaccess hello key or secret in hello vault, use the [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>

<span data-ttu-id="8e828-214">예를 들어 자격 증명 모음 이름이 **ContosoKeyVault** 및 tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed의 클라이언트 ID가 중이 고 tooauthorize hello 응용 프로그램 toodecrypt 및 서명 된 키의 원하는 hello 응용 프로그램 자격 증명 모음을 hello 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="8e828-214">For example, if your vault name is **ContosoKeyVault** and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, run hello following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

<span data-ttu-id="8e828-215">자격 증명 모음에는 동일한 응용 프로그램 tooread 비밀 tooauthorize 않으려면 hello 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-215">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <span data-ttu-id="8e828-216"><a id="HSM"></a>하드웨어 보안 모듈 (HSM) toouse 하려는 경우</span><span class="sxs-lookup"><span data-stu-id="8e828-216"><a id="HSM"></a>If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="8e828-217">추가 된 보증에 대 한 가져오기 또는 hello HSM 경계를 벗어날 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-217">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="8e828-218">hello Hsm은 FIPS 140-2 수준 2 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-218">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="8e828-219">이 요구 사항을 tooyou을 적용 하지 않는 경우이 섹션을 건너뛰고 이동 너무[hello 주요 자격 증명 모음 및 연결 된 키와 비밀 삭제](#delete)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-219">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete).</span></span>

<span data-ttu-id="8e828-220">toocreate 이러한 HSM 보호 키 hello를 사용 해야 [Azure 키 자격 증명 모음 Premium 서비스 계층 toosupport HSM 보호 키](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-220">toocreate these HSM-protected keys, you must use hello [Azure Key Vault Premium service tier toosupport HSM-protected keys](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="8e828-221">또한 이 기능은 Azure 중국에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-221">In addition, note that this functionality is not available for Azure China.</span></span>

<span data-ttu-id="8e828-222">Hello 주요 자격 증명 모음을 만들 때 추가 hello **-SKU** 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="8e828-222">When you create hello key vault, add hello **-SKU** parameter:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



<span data-ttu-id="8e828-223">소프트웨어 보호 키 (같이 이전) 및 HSM 보호 키 toothis 자격 증명 모음 키를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-223">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis key vault.</span></span> <span data-ttu-id="8e828-224">toocreate는 HSM 보호 키 집합 hello **-대상** 매개 변수 too'HSM':</span><span class="sxs-lookup"><span data-stu-id="8e828-224">toocreate an HSM-protected key, set hello **-Destination** parameter too'HSM':</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

<span data-ttu-id="8e828-225">다음 명령은 tooimport hello에서 키를 사용할 수 있습니다는 합니다. PFX 파일을 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-225">You can use hello following command tooimport a key from a .PFX file on your computer.</span></span> <span data-ttu-id="8e828-226">이 명령은 hello 키 자격 증명 모음 서비스에서에서 Hsm에 hello 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-226">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


<span data-ttu-id="8e828-227">다음 명령은 hello "bring your own key"을 가져옵니다 (BYOK) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-227">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="8e828-228">이 시나리오를 사용 하 여 로컬 HSM의 키를 생성 한 후 hello HSM 경계를 종료 하는 hello 키 없이 tooHSMs hello 키 자격 증명 모음 서비스에에서 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-228">This scenario lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

<span data-ttu-id="8e828-229">자세한 방법에 대 한 지침은 toogenerate이 BYOK 패키지 참조 [어떻게 toogenerate 및 전송 HSM 보호 키 Azure 키 자격 증명 모음에 대 한](key-vault-hsm-protected-keys.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-229">For more detailed instructions about how toogenerate this BYOK package, see [How toogenerate and transfer HSM-protected keys for Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <span data-ttu-id="8e828-230"><a id="delete"></a>Hello 주요 자격 증명 모음 및 연결 된 키와 비밀 정보를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-230"><a id="delete"></a>Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="8e828-231">Hello 주요 자격 증명 모음 및 hello 키 또는 암호에 포함 된 더 이상 필요 하면 hello를 사용 하 여 hello 주요 자격 증명 모음을 삭제할 수 없습니다 [제거 AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8e828-231">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello [Remove-AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:</span></span>

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

<span data-ttu-id="8e828-232">또는 hello 주요 자격 증명 모음 및 해당 그룹에 포함 된 다른 모든 리소스를 포함 하는 전체 Azure 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-232">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <span data-ttu-id="8e828-233"><a id="other"></a>기타 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="8e828-233"><a id="other"></a>Other Azure PowerShell Cmdlets</span></span>
<span data-ttu-id="8e828-234">Azure 주요 자격 증명 모음을 관리하는 데 유용한 기타 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-234">Other commands that you might find useful for managing Azure Key Vault:</span></span>

* <span data-ttu-id="8e828-235">`$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: 이 명령은 모든 키와 선택한 속성을 테이블 형식으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-235">`$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: This command gets a tabular display of all keys and selected properties.</span></span>
* <span data-ttu-id="8e828-236">`$Keys[0]`:이 명령은 hello 지정 된 키에 대 한 속성의 전체 목록을 표시합니다</span><span class="sxs-lookup"><span data-stu-id="8e828-236">`$Keys[0]`: This command displays a full list of properties for hello specified key</span></span>
* <span data-ttu-id="8e828-237">`Get-AzureKeyVaultSecret`: 이 명령은 모든 비밀 이름과 선택한 속성을 테이블 형식으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-237">`Get-AzureKeyVaultSecret`: This command lists a tabular display of all secret names and selected properties.</span></span>
* <span data-ttu-id="8e828-238">`Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: 예제 어떻게 tooremove 특정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-238">`Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Example how tooremove a specific key.</span></span>
* <span data-ttu-id="8e828-239">`Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: 예제 어떻게 tooremove 특정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-239">`Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Example how tooremove a specific secret.</span></span>

## <span data-ttu-id="8e828-240"><a id="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e828-240"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="8e828-241">웹 응용 프로그램에서 Azure 주요 자격 증명 모음을 사용하는 후속 자습서는 [웹 응용 프로그램에서 Azure 주요 자격 증명 모음 사용](key-vault-use-from-web-application.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e828-241">For a follow-up tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="8e828-242">toosee 주요 자격 증명 모음 사용 중인 참조 [Azure 키 자격 증명 모음 로깅](key-vault-logging.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-242">toosee how your key vault is being used, see [Azure Key Vault Logging](key-vault-logging.md).</span></span>

<span data-ttu-id="8e828-243">목록이 hello Azure 키 자격 증명 모음에 대 한 최신 Azure PowerShell cmdlet에 대 한 참조 [Azure 키 자격 증명 모음 Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-243">For a list of hello latest Azure PowerShell cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="8e828-244">프로그래밍 참조에 대 한 참조 [Azure 키 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8e828-244">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
