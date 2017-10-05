---
title: "CLI를 사용하여 Azure Key Vault 관리 | Microsoft Docs"
description: "이 자습서에서는 CLI를 사용하여 키 자격 증명 모음의 일반 작업을 자동화하는 방법을 설명합니다."
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: c2565a742ce4f6ab5f7639a54c4a475f00cbc260
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="6f6fc-103">CLI를 사용하여 키 자격 증명 모음 관리</span><span class="sxs-lookup"><span data-stu-id="6f6fc-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="6f6fc-104">Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="6f6fc-105">자세한 내용은 [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="6f6fc-106">소개</span><span class="sxs-lookup"><span data-stu-id="6f6fc-106">Introduction</span></span>

<span data-ttu-id="6f6fc-107">이 자습서를 사용하면 Azure 키 자격 증명 모음으로 시작하여 확정된 컨테이너(자격 증명 모음)를 Azure에 만들고 Azure에서 암호화 키와 비밀을 저장하고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="6f6fc-108">Azure 플랫폼 간 명령줄 인터페이스를 사용하여 Azure 응용 프로그램과 함께 사용할 수 있는 키 또는 암호를 포함하는 자격 증명 모음을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="6f6fc-109">응용 프로그램이 수 해당 키 또는 암호를 사용할 수 있는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="6f6fc-110">**예상 완료 시간:** 20분</span><span class="sxs-lookup"><span data-stu-id="6f6fc-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="6f6fc-111">이 자습서에는 단계 중 하나에 포함되는 Azure 응용 프로그램을 작성하는 방법에 대한 지침을 포함하지 않으며, 키 자격 증명 모음에서 키나 비밀을 사용하도록 응용 프로그램을 인증하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="6f6fc-112">현재는 Azure 포털에서 Azure 키 자격 증명 모음을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="6f6fc-113">대신 이러한 플랫폼 간 명령줄 인터페이스 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="6f6fc-114">또는 Azure PowerShell 지침의 경우 [이 자습서](key-vault-get-started.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="6f6fc-115">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="6f6fc-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f6fc-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6f6fc-116">Prerequisites</span></span>

<span data-ttu-id="6f6fc-117">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="6f6fc-118">Microsoft Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="6f6fc-119">아직 구독하지 않은 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="6f6fc-120">명령줄 인터페이스 버전 0.9.1 이상.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="6f6fc-121">최신 버전을 설치하고 Azure 구독에 연결하려면 [Azure 플랫폼 간 명령줄 인터페이스 설치 및 구성](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="6f6fc-122">이 자습서에서 만드는 키 또는 암호를 사용하여 구성되는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="6f6fc-123">샘플 응용 프로그램은 [Microsoft 다운로드 센터](http://www.microsoft.com/download/details.aspx?id=45343)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="6f6fc-124">자세한 내용은 해당 추가 정보 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="6f6fc-125">Azure 플랫폼 간 명령줄 인터페이스 도움말 보기</span><span class="sxs-lookup"><span data-stu-id="6f6fc-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="6f6fc-126">이 자습서에서는 명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)를 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="6f6fc-127">--help 또는 -h 매개 변수를 사용하여 특정 명령에 대한 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="6f6fc-128">또는 azure help [command] [options] 형식을 사용하여 동일한 정보를 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="6f6fc-129">예를 들어 다음 명령은 모두 동일한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="6f6fc-130">명령에 필요한 매개 변수가 확실하지 않은 경우 --help, -h 또는 azure help [command]를 사용하여 도움말을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="6f6fc-131">다음 자습서를 통해 Azure 플랫폼 간 명령줄 인터페이스의 Azure 리소스 관리자를 학습할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="6f6fc-132">Azure 플랫폼 간 명령줄 인터페이스를 설치 및 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="6f6fc-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="6f6fc-133">Azure 리소스 관리자와 함께 Azure 플랫폼 간 명령줄 인터페이스 사용</span><span class="sxs-lookup"><span data-stu-id="6f6fc-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="6f6fc-134">구독에 연결</span><span class="sxs-lookup"><span data-stu-id="6f6fc-134">Connect to your subscriptions</span></span>

<span data-ttu-id="6f6fc-135">조직 계정을 사용하여 로그인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="6f6fc-136">또는 대화형으로 입력하여 로그인하려는 경우</span><span class="sxs-lookup"><span data-stu-id="6f6fc-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="6f6fc-137">로그인 방법은 조직 계정에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-137">The login method only works with organizational account.</span></span> <span data-ttu-id="6f6fc-138">조직 계정은 조직에서 관리되고 조직 Azure Active Directory 테넌트에 정의된 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="6f6fc-139">현재 조직 계정이 없고 Microsoft 계정을 사용하여 Azure 구독에 로그인하는 경우 다음 단계에 따라 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="6f6fc-140">[Azure 관리 포털](https://manage.windowsazure.com/)에 로그인한 후 Active Directory를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="6f6fc-141">디렉터리가 없는 경우 디렉터리 만들기를 선택하고 요청된 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="6f6fc-142">디렉터리를 선택하고 새 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-142">Select your directory and add a new user.</span></span> <span data-ttu-id="6f6fc-143">새 사용자는 조직 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-143">This new user is an organizational account.</span></span> <span data-ttu-id="6f6fc-144">사용자를 만드는 동안 사용자의 전자 메일 주소와 임시 암호가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="6f6fc-145">이 정보는 다른 단계에서 사용되므로 저장해 두십시오.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="6f6fc-146">포털에서 설정을 선택한 후 관리자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="6f6fc-147">추가를 선택하고 새 사용자를 공동 관리자로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="6f6fc-148">그러면 조직 계정이 Azure 구독을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="6f6fc-149">마지막으로, Azure 포털에서 로그아웃한 후 새 조직 계정을 사용하여 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="6f6fc-150">이 계정으로 처음 로그인하는 경우 암호를 변경하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="6f6fc-151">Microsoft Azure의 조직 계정 사용에 대한 자세한 내용은 [조직으로 Microsoft Azure에 등록](../active-directory/sign-up-organization.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="6f6fc-152">여러 구독이 있는 경우 Azure 키 자격 증명 모음에 사용할 특정 하나를 지정하려면, 다음을 입력하여 계정에 대한 구독을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="6f6fc-153">그런 후, 사용할 구독을 지정하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="6f6fc-154">Azure 플랫폼 간 명령줄 인터페이스 구성에 대한 자세한 내용은 [Azure 플랫폼 간 명령줄 인터페이스를 설치 및 구성하는 방법](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="6f6fc-155">Azure 리소스 관리자로 전환</span><span class="sxs-lookup"><span data-stu-id="6f6fc-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="6f6fc-156">키 자격 증명 모음에는 Azure 리소스 관리자가 필요로 하므로 다음을 입력하여 Azure 리소스 관리자 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="6f6fc-157">새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6f6fc-157">Create a new resource group</span></span>
<span data-ttu-id="6f6fc-158">Azure 리소스 관리자를 사용하면 관련된 모든 리소스는 리소스 그룹의 내부에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="6f6fc-159">이 자습서에서는 'ContosoResourceGroup'이라는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="6f6fc-160">첫 번째 매개 변수는 리소스 그룹 이름이고, 두 번째 매개 변수 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="6f6fc-161">위치의 경우, `azure location list` 명령을 사용하여 이 예에서 대체 위치를 지정하는 방법을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="6f6fc-162">자세한 정보가 필요한 경우 `azure help location`</span><span class="sxs-lookup"><span data-stu-id="6f6fc-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="6f6fc-163">키 자격 증명 모음 리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="6f6fc-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="6f6fc-164">키 자격 증명 모음 리소스 공급자가 구독에 등록되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="6f6fc-165">구독당 한 번만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="6f6fc-166">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="6f6fc-166">Create a key vault</span></span>

<span data-ttu-id="6f6fc-167">`azure keyvault create` 명령을 사용하여 키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="6f6fc-168">이 스크립트에는 3개의 필수 매개 변수, 리소스 그룹 이름, 키 자격 증명 모음 이름 및 지리적 위치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="6f6fc-169">예를 들어, 이름이 ContosoKeyVault이고, 리소스 그룹 이름이 ContosoResourceGroup이며 위치가 동아시아인 형식의 자격 증명 모음인 경우, 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="6f6fc-170">이 명령의 출력에서는 방금 만든 자격 증명 모음의 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="6f6fc-171">가장 중요한 두 개의 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-171">The two most important properties are:</span></span>

* <span data-ttu-id="6f6fc-172">**Name**: ContosoKeyVault이는 예제에서입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="6f6fc-173">다른 키 자격 증명 모음 cmdlet에 대해 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="6f6fc-174">**vaultUri**: 예제에서는 https://contosokeyvault.vault.azure.net입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="6f6fc-175">REST API를 통해 사용자 자격 증명 모음을 사용하는 응용 프로그램은 URI를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="6f6fc-176">Azure 계정은 이제 이 키 자격 증명 모음에서 모든 작업을 수행할 권한을 가지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="6f6fc-177">아직 다른 사람은 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="6f6fc-178">키 또는 암호를 키 자격 증명 모음에 추가</span><span class="sxs-lookup"><span data-stu-id="6f6fc-178">Add a key or secret to the key vault</span></span>

<span data-ttu-id="6f6fc-179">소프트웨어 보호 키를 만들도록 Azure 키 자격 증명 모음을 사용하려면, `azure key create` 명령을 사용하여 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="6f6fc-180">그러나 Azure 키 자격 증명 모음에 업로드하려는 softkey.pem이라는 파일에 로컬 파일로 저장된 .pem 파일의 기존 키가 있는 경우 다음을 입력하여 키 자격 증명 모음 서비스에서 소프트웨어로 키를 보호하는 .PEM 파일에서 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="6f6fc-181">이제 해당 URI를 사용하여 Azure 키 자격 증명 모음을 만들거나 업로드하는 이 키를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="6f6fc-182">**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey**를 사용하여 현재 버전을 가져오고 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87**을 사용하여 이 특정 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="6f6fc-183">자격 증명 모음에 암호를 추가하려면 다음을 입력합니다. 암호는 SQLPassword이며 Azure 키 자격 증명 모음에 대한 Pa$$w0rd 값을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="6f6fc-184">이제 해당 URI를 사용하여 Azure 키 자격 증명 모음에 추가한 이 암호를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="6f6fc-185">**https://ContosoVault.vault.azure.net/secrets/SQLPassword**를 사용하여 현재 버전을 가져오고 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d**를 사용하여 이 특정 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="6f6fc-186">방금 만든 키 또는 암호를 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="6f6fc-187">사용자의 키를 보려면 다음을 입력 합니다. `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="6f6fc-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="6f6fc-188">사용자의 비밀을 보려면 다음을 입력 합니다. `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="6f6fc-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="6f6fc-189">Azure Active Directory에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="6f6fc-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="6f6fc-190">이 단계는 일반적으로 별도의 컴퓨터에서 개발자가 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="6f6fc-191">Azure 키 자격 증명 모음에 특정한 것은 아니지만 완전성을 위해 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f6fc-192">이 단계에서 등록된 자습서, 계정, 해당 자격 증명 모음 및 응용 프로그램을 완료하려면, 모두 동일한 Azure 디렉터리에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="6f6fc-193">자격 증명 모음 키를 사용하는 응용 프로그램은 Azure Active Directory에서 토큰을 사용하여 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="6f6fc-194">이렇게 하려면 응용 프로그램의 소유자가 Azure Active Directory에 먼저 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="6f6fc-195">등록 끝에 응용 프로그램 소유자는 다음 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="6f6fc-196">**응용 프로그램 ID**(클라이언트 ID라고도 함) 및 **인증 키**(공유 비밀이라고도 함).</span><span class="sxs-lookup"><span data-stu-id="6f6fc-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="6f6fc-197">응용 프로그램은 토큰을 가져올 Azure Active Directory에 이 두 값 모두가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="6f6fc-198">응용 프로그램 구성 방식은 응용 프로그램에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="6f6fc-199">키 자격 증명 모음 샘플 응용 프로그램의 경우, 응용 프로그램 소유자는 app.config 파일에서 이러한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="6f6fc-200">Azure Active Directory에 응용 프로그램을 등록하려면:</span><span class="sxs-lookup"><span data-stu-id="6f6fc-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="6f6fc-201">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="6f6fc-202">왼쪽에서 **Active Directory**를 클릭한 다음 응용 프로그램을 등록할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="6f6fc-203">주요 자격 증명 모음을 만든 Azure 구독을 포함하는 동일한 디렉터리를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-203">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="6f6fc-204">이 디렉터리를 모르는 경우, **설정**을 클릭하고, 사용자 키 자격 증명 모음을 만든 구독을 식별하고 마지막 열에 표시되는 디렉터리의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="6f6fc-205">**APPLICATIONS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="6f6fc-206">디렉터리에 추가한 앱이 없는 경우,이 페이지는 **앱 추가** 링크만을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="6f6fc-207">링크를 클릭하거나 명령 모음에서 **추가** 를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="6f6fc-208">**응용 프로그램 추가** 마법사에서 **무엇을 하고 싶나요?** 페이지를 클릭하고, **조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="6f6fc-209">**응용 프로그램에 대해 알려주세요** 페이지에서, 응용 프로그램 이름을 지정하고 **웹 응용 프로그램 및/또는 Web API**(기본값)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="6f6fc-210">다음 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-210">Click the Next icon.</span></span>
6. <span data-ttu-id="6f6fc-211">**앱 속성** 페이지에서 웹 응용 프로그램에 대한 **로그인 URL** 및 **앱 ID URI**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="6f6fc-212">응용 프로그램에 이러한 값이 없는 경우 이 단계에서 만들 수 있습니다(예를 들어, 두 상자에 대해 http://test1.contoso.com을 지정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="6f6fc-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="6f6fc-213">이러한 사이트가 존재하는 지가 중요하지 않습니다. 사용자 디렉토리의 각 응용 프로그램에 대해 각 응용 프로그램의 앱 ID URI가 다르다는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="6f6fc-214">디렉터리는 이 문자열을 사용하여 앱을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="6f6fc-215">마법사에서 변경 내용을 저장하려면 전체 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="6f6fc-216">빠른 시작 페이지에서 **CONFIGURE**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="6f6fc-217">**키** 섹션으로 스크롤하고 기간을 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="6f6fc-218">페이지가 새로 고쳐지고 이제 키 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="6f6fc-219">이 키 값 및 **클라이언트 ID** 가 있는 응용 프로그램을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="6f6fc-220">(이 구성에 대한 지침은 응용 프로그램에 특정된 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="6f6fc-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="6f6fc-221">사용자 자격 증명 모음에 사용 권한을 설정하려면 다음 단계에서 사용하는 이 페이지에서 클라이언트 ID 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="6f6fc-222">응용 프로그램에 키 또는 암호를 사용하도록 권한 부여</span><span class="sxs-lookup"><span data-stu-id="6f6fc-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="6f6fc-223">응용 프로그램이 자격 증명 모음의 키 또는 암호에 대한 액세스를 인증하려면 `azure keyvault set-policy` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="6f6fc-224">예를 들어, 자격 증명 모음 이름은 ContosoKeyVault이고 권한을 부여하려는 응용 프로그램에 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed의 클라이언트 ID가 있고 자격 증명 모음에 있는 키로 서명하고 암호 해제하도록 응용 프로그램을 인증하려면, 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="6f6fc-225">Windows 명령 프롬프트에서 실행하는 경우 작은따옴표를 큰따옴표로 바꾸고 내부 큰따옴표를 이스케이프해야</span><span class="sxs-lookup"><span data-stu-id="6f6fc-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="6f6fc-226">예: "[\"해독\",\"기호\"]"</span><span class="sxs-lookup"><span data-stu-id="6f6fc-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="6f6fc-227">자격 증명 모음에서 기밀 정보를 읽기 위해 동일한 응용 프로그램에 권한을 부여하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="6f6fc-228">하드웨어 보안 모듈(HSM)을 사용하려는 경우</span><span class="sxs-lookup"><span data-stu-id="6f6fc-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="6f6fc-229">추가된 보증을 위해, HSM 경계를 절대로 떠나지 않는 하드웨어 보안 모듈(HSMs)에서 키를 가져오거나 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="6f6fc-230">HSM은 FIPS 140-2 Level 2 유효성 검사가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="6f6fc-231">이 요구 사항이 사용자에게 적용되지 않는 경우, 이 섹션을 건너뛰고 [키 자격 증명 모음 및 연결된 키와 암호 삭제](#delete-the-key-vault-and-associated-keys-and-secrets)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="6f6fc-232">이러한 HSM 보호되는 키를 만들려면, HSM 보호되는 키를 지원하는 자격 증명 모음 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="6f6fc-233">keyvault를 만들 때 'sku' 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="6f6fc-234">이 자격 증명이 모음에 소프트웨어 보호 키(이전에 표시된 대로)와 HSM 보호되는 키를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="6f6fc-235">HSM으로 보호되는 키를 만들려면, 대상 매개 변수를 'HSM'으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="6f6fc-236">다음 명령을 사용하여 사용자 컴퓨터의 .pem 파일에서 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="6f6fc-237">이 명령은 키 자격 증명 모음 서비스에서 HSM으로 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="6f6fc-238">다음 명령은 "bring your own key"(BYOK) 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="6f6fc-239">이렇게 하면 로컬 HSM에 키를 생성하고 키가 HSM 경계를 벗어나지 않고 이를 키 자격 증명 모음 서비스의 HSM에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="6f6fc-240">이 BYOK 패키지를 생성하는 방법에 대한 자세한 내용은 [Azure 키 자격 증명 모음과 HSM-보호된 키를 사용하는 방법](key-vault-hsm-protected-keys.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="6f6fc-241">키 자격 증명 모음 및 연결된 키와 암호 삭제</span><span class="sxs-lookup"><span data-stu-id="6f6fc-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="6f6fc-242">키 자격 증명 모음 및 이를 포함하는 키나 비밀이 더 이상 필요하지 않은 경우, azure keyvault delete 명령을 사용하여 키 자격 증명 모음을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="6f6fc-243">또는 키 자격 증명 모음 및 해당 그룹에 포함된 다른 모든 리소스 및 키를 포함하는 전체 Azure 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="6f6fc-244">다른 Azure 플랫폼 간 명령줄 인터페이스 명령</span><span class="sxs-lookup"><span data-stu-id="6f6fc-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="6f6fc-245">Azure 키 자격 증명 모음을 관리하는 데 유용할 수 있는 다른 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="6f6fc-246">이 명령은 모든 키와 선택한 속성을 테이블 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="6f6fc-247">이 명령은 지정된 키에 대한 속성의 전체 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="6f6fc-248">이 명령은 모든 비밀 이름과 선택한 속성을 테이블 형식으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="6f6fc-249">다음은 특정 키를 제거하는 방법에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="6f6fc-250">다음은 특정 암호를 제거하는 방법에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="6f6fc-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6f6fc-251">Next steps</span></span>
<span data-ttu-id="6f6fc-252">프로그래밍 참조는 [Azure 주요 자격 증명 모음 개발자 가이드](key-vault-developers-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f6fc-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

