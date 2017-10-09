---
title: "CLI를 사용 하 여 Azure 키 자격 aaaManage | Microsoft Docs"
description: "키 자격 증명 모음에이 자습서 tooautomate 일반적인 작업을 사용 하 여 hello CLI를 사용 하 여"
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
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="f200a-103">CLI를 사용하여 키 자격 증명 모음 관리</span><span class="sxs-lookup"><span data-stu-id="f200a-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="f200a-104">Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="f200a-105">자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="f200a-106">소개</span><span class="sxs-lookup"><span data-stu-id="f200a-106">Introduction</span></span>

<span data-ttu-id="f200a-107">이 자습서 toohelp 얻게를 사용 하 여 toostore Azure에서 확정 된 컨테이너 (볼트)을 Azure 주요 자격 증명 모음 toocreate를 시작 하 고 암호화 키 및 Azure에서 암호 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="f200a-108">이 과정을 보여 줍니다 hello toocreate Azure 크로스 플랫폼 명령줄 인터페이스를 사용 하 여 키 또는 암호 Azure 응용 프로그램과 함께 사용할 수 있는 포함 된 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="f200a-109">응용 프로그램이 수 해당 키 또는 암호를 사용할 수 있는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="f200a-110">**예상 시간 toocomplete:** 20 분</span><span class="sxs-lookup"><span data-stu-id="f200a-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="f200a-111">이 자습서는 toowrite Azure 응용 프로그램 hello 단계 중 하나를 포함 하는 방법을 tooauthorize 응용 프로그램 toouse 키 또는 암호에 hello 키 자격 증명 모음을 보여 주는 hello 하는 방법에 대 한 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
> 
> <span data-ttu-id="f200a-112">현재 hello Azure 포털에서에서 Azure 키 자격 증명 모음을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-112">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="f200a-113">대신 이러한 플랫폼 간 명령줄 인터페이스 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="f200a-114">또는 Azure PowerShell 지침의 경우 [이 자습서](key-vault-get-started.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="f200a-115">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f200a-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f200a-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f200a-116">Prerequisites</span></span>

<span data-ttu-id="f200a-117">toocomplete이이 자습서에서는 다음 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-117">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="f200a-118">구독 tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="f200a-118">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="f200a-119">아직 구독하지 않은 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="f200a-120">명령줄 인터페이스 버전 0.9.1 이상.</span><span class="sxs-lookup"><span data-stu-id="f200a-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="f200a-121">tooinstall 최신 버전을 hello 및 tooyour Azure 구독 연결 참조 [설치 및 구성 hello Azure 크로스 플랫폼 명령줄 인터페이스](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-121">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="f200a-122">응용 프로그램 구성된 toouse hello 키 또는 암호를이 자습서에서 만드는 됩니다입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-122">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="f200a-123">샘플 응용 프로그램은 hello에서 사용할 수 있는 [Microsoft 다운로드 센터](http://www.microsoft.com/download/details.aspx?id=45343)합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-123">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="f200a-124">추가 정보 파일을 함께 제공 된 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f200a-124">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="f200a-125">Azure 플랫폼 간 명령줄 인터페이스 도움말 보기</span><span class="sxs-lookup"><span data-stu-id="f200a-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="f200a-126">이 자습서에서는 hello 명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트)에 익숙한 가정</span><span class="sxs-lookup"><span data-stu-id="f200a-126">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="f200a-127">hello-도움말 또는-h 매개 변수 수 특정 명령에 대 한 tooview 도움말을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-127">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="f200a-128">또는 azure hello 도움말 [command] [옵션] 형식을 사용 하는 tooreturn 될 수도 있습니다 hello 동일한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-128">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="f200a-129">예를 들어 hello 다음 명령을 모두 반환 hello 동일한 정보:</span><span class="sxs-lookup"><span data-stu-id="f200a-129">For example, hello following commands all return hello same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="f200a-130">명령에 필요한 hello 매개 변수에 대 한 의심 toohelp를 사용 하 여-참조 도움말,-h 또는 azure 도움말 [command].</span><span class="sxs-lookup"><span data-stu-id="f200a-130">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or azure help [command].</span></span>

<span data-ttu-id="f200a-131">Hello Azure 리소스 관리자의 Azure 플랫폼 간 명령줄 인터페이스와 친숙 한 자습서 tooget 다음 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-131">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="f200a-132">어떻게 tooinstall 및 Azure 플랫폼 간 명령줄 인터페이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-132">How tooinstall and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="f200a-133">Azure 리소스 관리자와 함께 Azure 플랫폼 간 명령줄 인터페이스 사용</span><span class="sxs-lookup"><span data-stu-id="f200a-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="f200a-134">Tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="f200a-134">Connect tooyour subscriptions</span></span>

<span data-ttu-id="f200a-135">다음 명령을 사용 하 여 hello 조직 계정을 사용 하 여 toolog:</span><span class="sxs-lookup"><span data-stu-id="f200a-135">toolog in using an organizational account, use hello following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="f200a-136">대화형으로 입력 하 여에 toolog 포함 하려는 경우 또는</span><span class="sxs-lookup"><span data-stu-id="f200a-136">or if you want toolog in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="f200a-137">hello 로그인 메서드 조직 계정 에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-137">hello login method only works with organizational account.</span></span> <span data-ttu-id="f200a-138">조직 계정은 조직에서 관리되고 조직 Azure Active Directory 테넌트에 정의된 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="f200a-139">현재 조직 계정이 없는 Microsoft 계정 toolog tooyour Azure 구독에서에서 사용 하는 경우 쉽게 만들 수 있습니다 하나를 사용 하 여 다음 단계 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-139">If you do not currently have an organizational account, and are using a Microsoft account toolog in tooyour Azure subscription, you can easily create one using hello following steps.</span></span>

1. <span data-ttu-id="f200a-140">로그인 toohello 로그인 toohello [Azure 관리 포털](https://manage.windowsazure.com/), Active Directory에서을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-140">Login toohello Login toohello [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="f200a-141">디렉터리가 있으면 디렉터리 만들기 하 고 제공 hello 요청 된 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-141">If no directory exists, select Create your directory and provide hello requested information.</span></span>
3. <span data-ttu-id="f200a-142">디렉터리를 선택하고 새 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-142">Select your directory and add a new user.</span></span> <span data-ttu-id="f200a-143">새 사용자는 조직 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-143">This new user is an organizational account.</span></span> <span data-ttu-id="f200a-144">Hello 사용자의 hello 만드는 동안 hello 사용자에 대 한 전자 메일 주소 및 임시 암호를 모두 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-144">During hello creation of hello user, you will be supplied with both an e-mail address for hello user and a temporary password.</span></span> <span data-ttu-id="f200a-145">이 정보는 다른 단계에서 사용되므로 저장해 두십시오.</span><span class="sxs-lookup"><span data-stu-id="f200a-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="f200a-146">Hello 포털에서 설정을 선택 하 고 관리자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-146">From hello portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="f200a-147">추가 선택 하 고 공동 관리자로 hello 새 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-147">Select Add, and add hello new user as a co-administrator.</span></span> <span data-ttu-id="f200a-148">이렇게 하면 hello 조직 계정 toomanage Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="f200a-148">This allows hello organizational account toomanage your Azure subscription.</span></span>
5. <span data-ttu-id="f200a-149">마지막으로, 로그 아웃 hello Azure 포털 한 다음 다시 로그인 hello 새 조직 계정을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-149">Finally, log out of hello Azure portal and then log back in using hello new organizational account.</span></span> <span data-ttu-id="f200a-150">이이 계정 사용 하 여 처음 로그온 hello, 입력 정보 요청된 toochange hello 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-150">If this is hello first time logging in with this account, you will be prompted toochange hello password.</span></span>

<span data-ttu-id="f200a-151">Microsoft Azure의 조직 계정 사용에 대한 자세한 내용은 [조직으로 Microsoft Azure에 등록](../active-directory/sign-up-organization.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f200a-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="f200a-152">구독이 여러 개 있고 Azure 키 자격 증명 모음에 대 한 특정 한 toouse toospecify 원하는 hello toosee hello 구독 계정에 대해 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-152">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="f200a-153">그런 다음 toospecify hello 구독 toouse, 유형:</span><span class="sxs-lookup"><span data-stu-id="f200a-153">Then, toospecify hello subscription toouse, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="f200a-154">Azure 플랫폼 간 명령줄 인터페이스를 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooInstall Azure 크로스 플랫폼 명령줄 인터페이스를 구성 하 고](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How tooInstall and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-toousing-azure-resource-manager"></a><span data-ttu-id="f200a-155">스위치 toousing Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="f200a-155">Switch toousing Azure Resource Manager</span></span>
<span data-ttu-id="f200a-156">hello 키 자격 증명 모음에 Azure 리소스 관리자가 필요 하므로 hello tooswitch tooAzure Resource Manager 모드를 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-156">hello Key Vault requires Azure Resource Manager, so type hello following tooswitch tooAzure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="f200a-157">새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f200a-157">Create a new resource group</span></span>
<span data-ttu-id="f200a-158">Azure 리소스 관리자를 사용하면 관련된 모든 리소스는 리소스 그룹의 내부에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="f200a-159">이 자습서에서는 'ContosoResourceGroup'이라는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="f200a-160">hello 첫 번째 매개 변수는 리소스 그룹 이름 및 hello 두 번째 매개 변수는 hello 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-160">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="f200a-161">위치에 대 한 hello 명령을 사용 하 여 `azure location list` tooidentify 어떻게 toospecify이 예에서 하나는 대체 위치 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-161">For location, use hello command `azure location list` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="f200a-162">자세한 정보가 필요한 경우 `azure help location`</span><span class="sxs-lookup"><span data-stu-id="f200a-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="f200a-163">Hello 주요 자격 증명 모음 리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="f200a-163">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="f200a-164">키 자격 증명 모음 리소스 공급자가 구독에 등록되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="f200a-165">이 toobe 구독 당 한 번만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-165">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="f200a-166">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="f200a-166">Create a key vault</span></span>

<span data-ttu-id="f200a-167">사용 하 여 hello `azure keyvault create` 명령 toocreate 주요 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-167">Use hello `azure keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="f200a-168">이 스크립트에 세 개의 필수 매개 변수: 리소스 그룹 이름, 주요 자격 증명 모음 이름 및 hello 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-168">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="f200a-169">예를 들어 hello 자격 증명 모음 이름을 ContosoKeyVault, hello ContosoResourceGroup, 리소스 그룹 이름 및 동아시아의 hello 위치를 사용 하는 경우 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-169">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="f200a-170">이 명령의 출력 hello 방금 만든 hello 키 자격 증명 모음의 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-170">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="f200a-171">hello 두 가장 중요 한 속성은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-171">hello two most important properties are:</span></span>

* <span data-ttu-id="f200a-172">**이름**: hello 예제 ContosoKeyVault입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-172">**Name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="f200a-173">다른 키 자격 증명 모음 cmdlet에 대해 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="f200a-174">**vaultUri**: hello 예제 https://contosokeyvault.vault.azure.net입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-174">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="f200a-175">REST API를 통해 사용자 자격 증명 모음을 사용하는 응용 프로그램은 URI를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="f200a-176">Azure 계정에 권한이 부여 된 tooperform이이 키에 대 한 모든 작업 자격 증명 모음에 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-176">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="f200a-177">아직 다른 사람은 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="f200a-178">키 또는 키 자격 증명 모음 보안 toohello 추가</span><span class="sxs-lookup"><span data-stu-id="f200a-178">Add a key or secret toohello key vault</span></span>

<span data-ttu-id="f200a-179">Hello를 사용 하 여 Azure 키 자격 증명 모음 toocreate 소프트웨어 보호 키를 하려는 경우 `azure key create` 명령을 실행 하 고 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-179">If you want Azure Key Vault toocreate a software-protected key for you, use hello `azure key create` command, and type hello following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="f200a-180">그러나 softkey.pem tooupload tooAzure 주요 자격 증명 모음을 지정 하 라는 파일에 로컬 파일로 저장.pem 파일에 있는 기존 키가 있으면 hello hello에서 다음 tooimport hello 키를 입력 합니다. PEM 파일-hello 키 자격 증명 모음 서비스에에서는 소프트웨어에 의해 hello 키를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="f200a-181">이제는 작성 되거나 해당 URI를 사용 하 여 tooAzure 주요 자격 증명을 업로드 한 hello 키를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-181">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="f200a-182">사용 하 여 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello 현재 버전을 가져오고 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget이 특정 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="f200a-183">tooadd SQLPassword 라는 암호 되었으며 Pa$ $w0rd tooAzure 주요 자격 증명 유형 hello 뒤의 hello 값 비밀 toohello 자격:</span><span class="sxs-lookup"><span data-stu-id="f200a-183">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="f200a-184">이제 해당 URI를 사용 하 여 tooAzure 자격 증명 모음 키를 추가 하는이 암호를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-184">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="f200a-185">사용 하 여 **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello 현재 버전을 가져오고 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget이 특정 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="f200a-186">Hello 키 또는 암호 방금 만든 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-186">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="f200a-187">tooview 프로그램 키, 유형:`azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="f200a-187">tooview your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="f200a-188">tooview 비밀을 형식:`azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="f200a-188">tooview your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="f200a-189">Azure Active Directory에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="f200a-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="f200a-190">이 단계는 일반적으로 별도의 컴퓨터에서 개발자가 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="f200a-191">특정 tooAzure 주요 자격 증명 모음 되지만 완전성을 위해 여기에서 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-191">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f200a-192">toocomplete hello 자습서, 계정, 자격 증명 모음 hello 및이 단계에서 등록 하는 hello 응용 프로그램 모두에 있어야 hello 같은 Azure 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-192">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
> 
> 

<span data-ttu-id="f200a-193">자격 증명 모음 키를 사용하는 응용 프로그램은 Azure Active Directory에서 토큰을 사용하여 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="f200a-194">toodo이,이 hello hello 응용 프로그램의 소유자가 Azure Active Directory에서 먼저 hello 응용 프로그램을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-194">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="f200a-195">등록의 hello 끝 hello 응용 프로그램 소유자 hello를 다음 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-195">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="f200a-196">**응용 프로그램 ID** (클라이언트 ID) 및 **인증 키** (라고도 hello 공유 암호).</span><span class="sxs-lookup"><span data-stu-id="f200a-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="f200a-197">hello 응용 프로그램에는 모두 이러한 값 tooAzure Active Directory tooget 토큰을 제시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-197">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="f200a-198">Hello 응용 프로그램은 어떻게 구성 toodo hello 응용 프로그램에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-198">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="f200a-199">Hello 키 자격 증명 모음 샘플 응용 프로그램에 대 한 응용 프로그램 소유자 hello hello app.config 파일에 이러한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-199">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="f200a-200">Azure Active Directory에서 tooregister hello 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="f200a-200">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="f200a-201">Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-201">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="f200a-202">Hello 왼쪽에서 클릭 **Active Directory**, 한 다음 응용 프로그램을 등록 하는 hello 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-202">On hello left, click **Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="f200a-203">Hello를 선택 해야 포함 된 같은 디렉터리 hello 주요 자격 증명 모음을 만들 때 사용한 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="f200a-203">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="f200a-204">알 수 없는 디렉터리가 인지, 클릭 **설정**, 주요 자격 증명 모음을 만들 때 사용한 hello 구독을 식별 하 고 hello 디렉터리의 참고 hello 이름이 hello 마지막 열에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-204">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="f200a-205">**APPLICATIONS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="f200a-206">이 페이지 hello만 표시 됩니다 앱이 없습니다. tooyour 디렉터리를 추가한 경우 **앱 추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-206">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="f200a-207">Hello 링크를 클릭 하거나 hello 클릭 해도, **추가** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-207">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="f200a-208">Hello에 **응용 프로그램 추가** hello에서 마법사 **하 신 toodo 원하는?** 페이지에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-208">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="f200a-209">Hello에 **응용 프로그램에 대해 알리기** 페이지 응용 프로그램에 대 한 이름을 지정 하 고 선택 **웹 응용 프로그램 및/또는 웹 API** (기본 hello).</span><span class="sxs-lookup"><span data-stu-id="f200a-209">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="f200a-210">Hello 다음 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-210">Click hello Next icon.</span></span>
6. <span data-ttu-id="f200a-211">Hello에 **앱 속성** 페이지에서 지정 하는 hello **로그온 URL** 및 **앱 ID URI** 웹 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-211">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="f200a-212">응용 프로그램에 이러한 값이 없는 경우 이 단계에서 만들 수 있습니다(예를 들어, 두 상자에 대해 http://test1.contoso.com을 지정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="f200a-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="f200a-213">이러한 사이트 존재 하는 경우 중요 하지 않습니다. 중요 한 것은 각 응용 프로그램에 대 한 hello 앱 ID URI는 디렉터리의 모든 응용 프로그램에 대 한 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-213">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="f200a-214">hello 디렉터리는이 문자열 tooidentify 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-214">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="f200a-215">Hello 완료 아이콘 toosave hello 마법사에서 변경 내용을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-215">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="f200a-216">Hello 빠른 시작 페이지에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-216">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="f200a-217">Toohello 스크롤하여 **키** 섹션 hello 기간, 선택한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-217">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="f200a-218">hello 페이지가 새로 고쳐지고 키 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-218">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="f200a-219">이 키 값 및 hello 응용 프로그램을 구성 해야 **클라이언트 ID** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-219">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="f200a-220">(이 구성에 대한 지침은 응용 프로그램에 특정된 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="f200a-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="f200a-221">다음 단계 tooset 권한을 hello에서 사용할 자격 증명 모음에 있는이 페이지에서 hello 클라이언트 ID 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-221">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="f200a-222">Hello 응용 프로그램 toouse hello 키 또는 암호를 권한 부여</span><span class="sxs-lookup"><span data-stu-id="f200a-222">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="f200a-223">키 또는 암호 hello 자격 증명 모음을 사용 하 여 hello에 tooauthorize hello 응용 프로그램 tooaccess hello `azure keyvault set-policy` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-223">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="f200a-224">예를 들어 자격 증명 모음 이름이 tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed의 클라이언트 ID가 중이 고 tooauthorize hello 응용 프로그램 toodecrypt 및 서명 키를 가진 자격 증명 모음에서 원하는 ContosoKeyVault 및 hello 응용 프로그램 이면 다음 실행 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="f200a-224">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="f200a-225">Windows 명령 프롬프트에서 실행 하는 경우에 큰따옴표를 작은따옴표로 바꿉니다 고도 hello 내부 큰따옴표를 이스케이프 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape hello internal double quotes.</span></span> <span data-ttu-id="f200a-226">예: "[\"해독\",\"기호\"]"</span><span class="sxs-lookup"><span data-stu-id="f200a-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="f200a-227">자격 증명 모음에는 동일한 응용 프로그램 tooread 비밀 tooauthorize 않으려면 hello 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-227">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="f200a-228">하드웨어 보안 모듈 (HSM) toouse 하려는 경우</span><span class="sxs-lookup"><span data-stu-id="f200a-228">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="f200a-229">추가 된 보증에 대 한 가져오기 또는 hello HSM 경계를 벗어날 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="f200a-230">hello Hsm은 FIPS 140-2 수준 2 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-230">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="f200a-231">이 요구 사항을 tooyou을 적용 하지 않는 경우이 섹션을 건너뛰고 이동 너무[hello 주요 자격 증명 모음 및 연결 된 키와 비밀 삭제](#delete-the-key-vault-and-associated-keys-and-secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-231">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="f200a-232">toocreate 이러한 HSM 보호 키를 지 원하는 HSM 보호 키 자격 증명 모음 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-232">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="f200a-233">Hello keyvault를 만들 때 hello 'sku' 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-233">When you create hello keyvault, add hello 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="f200a-234">(앞에서 보았듯이) 소프트웨어 보호 키를 추가 하 고 HSM 보호 키 toothis 자격 증명 모음 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-234">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="f200a-235">toocreate는 HSM 보호 키 집합 hello 대상 매개 변수 too'HSM':</span><span class="sxs-lookup"><span data-stu-id="f200a-235">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="f200a-236">Hello 명령 tooimport 키.pem 파일을 컴퓨터에에서 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-236">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="f200a-237">이 명령은 hello 키 자격 증명 모음 서비스에서에서 Hsm에 hello 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-237">This command imports hello key into HSMs in hello Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="f200a-238">다음 명령은 hello "bring your own key"을 가져옵니다 (BYOK) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-238">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="f200a-239">이렇게 하면 로컬 HSM의 키를 생성 하 여 hello HSM 경계를 종료 하는 hello 키 없이 tooHSMs hello 키 자격 증명 모음 서비스에에서 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-239">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="f200a-240">자세한 방법에 대 한 지침은 toogenerate이 BYOK 패키지 참조 [어떻게 toouse HSM-Protected 키는 Azure 키 자격 증명](key-vault-hsm-protected-keys.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-240">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="f200a-241">Hello 주요 자격 증명 모음 및 연결 된 키와 비밀 정보를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-241">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="f200a-242">Hello 주요 자격 증명 모음 및 hello 키 또는 암호에 포함 된 더 이상 필요 하면 azure hello keyvault delete 명령을 사용 하 여 hello 주요 자격 증명 모음을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-242">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="f200a-243">또는 hello 주요 자격 증명 모음 및 해당 그룹에 포함 된 다른 모든 리소스를 포함 하는 전체 Azure 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-243">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="f200a-244">다른 Azure 플랫폼 간 명령줄 인터페이스 명령</span><span class="sxs-lookup"><span data-stu-id="f200a-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="f200a-245">Azure 키 자격 증명 모음을 관리하는 데 유용할 수 있는 다른 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="f200a-246">이 명령은 모든 키와 선택한 속성을 테이블 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="f200a-247">이 명령은 hello 지정 된 키에 대 한 속성의 전체 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-247">This command displays a full list of properties for hello specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="f200a-248">이 명령은 모든 비밀 이름과 선택한 속성을 테이블 형식으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="f200a-249">방법의 예로 특정 키 tooremove:</span><span class="sxs-lookup"><span data-stu-id="f200a-249">Here's an example of how tooremove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="f200a-250">방법의 예로 특정 보안 tooremove:</span><span class="sxs-lookup"><span data-stu-id="f200a-250">Here's an example of how tooremove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="f200a-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f200a-251">Next steps</span></span>
<span data-ttu-id="f200a-252">프로그래밍 참조에 대 한 참조 [Azure 키 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f200a-252">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

