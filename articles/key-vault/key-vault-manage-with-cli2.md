---
title: "CLI를 사용 하 여 Azure 키 자격 aaaManage | Microsoft Docs"
description: "키 자격 증명 모음에이 자습서 tooautomate 일반적인 작업을 사용 하 여 hello CLI 2.0을 사용 하 여"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="b0fab-103">CLI 2.0을 사용하여 Key Vault 관리</span><span class="sxs-lookup"><span data-stu-id="b0fab-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="b0fab-104">Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="b0fab-105">자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="b0fab-106">소개</span><span class="sxs-lookup"><span data-stu-id="b0fab-106">Introduction</span></span>
<span data-ttu-id="b0fab-107">이 자습서 toohelp 얻게를 사용 하 여 toostore Azure에서 확정 된 컨테이너 (볼트)을 Azure 주요 자격 증명 모음 toocreate를 시작 하 고 암호화 키 및 Azure에서 암호 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="b0fab-108">이 과정을 보여 줍니다 hello toocreate Azure 크로스 플랫폼 명령줄 인터페이스를 사용 하 여 키 또는 암호 Azure 응용 프로그램과 함께 사용할 수 있는 포함 된 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="b0fab-109">응용 프로그램이 수 해당 키 또는 암호를 사용할 수 있는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="b0fab-110">**예상 시간 toocomplete:** 20 분</span><span class="sxs-lookup"><span data-stu-id="b0fab-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="b0fab-111">이 자습서는 toowrite Azure 응용 프로그램 hello 단계 중 하나를 포함 하는 방법을 tooauthorize 응용 프로그램 toouse 키 또는 암호에 hello 키 자격 증명 모음을 보여 주는 hello 하는 방법에 대 한 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="b0fab-112">이 자습서에서는 최신 Azure CLI 2.0 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="b0fab-113">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="b0fab-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0fab-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b0fab-114">Prerequisites</span></span>
<span data-ttu-id="b0fab-115">toocomplete이이 자습서에서는 다음 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="b0fab-116">구독 tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="b0fab-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="b0fab-117">아직 구독하지 않은 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="b0fab-118">명령줄 인터페이스 버전 2.0 이상.</span><span class="sxs-lookup"><span data-stu-id="b0fab-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="b0fab-119">tooinstall 최신 버전을 hello 및 tooyour Azure 구독 연결 참조 [설치 및 구성 hello Azure 크로스 플랫폼 명령줄 인터페이스 2.0](/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="b0fab-120">응용 프로그램 구성된 toouse hello 키 또는 암호를이 자습서에서 만드는 됩니다입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="b0fab-121">샘플 응용 프로그램은 hello에서 사용할 수 있는 [Microsoft 다운로드 센터](http://www.microsoft.com/download/details.aspx?id=45343)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="b0fab-122">추가 정보 파일을 함께 제공 된 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b0fab-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="b0fab-123">Azure 플랫폼 간 명령줄 인터페이스 도움말 보기</span><span class="sxs-lookup"><span data-stu-id="b0fab-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="b0fab-124">이 자습서에서는 hello 명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트)에 익숙한 가정</span><span class="sxs-lookup"><span data-stu-id="b0fab-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="b0fab-125">hello-도움말 또는-h 매개 변수 수 특정 명령에 대 한 tooview 도움말을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="b0fab-126">또는 azure hello 도움말 [command] [옵션] 형식을 사용 하는 tooreturn 될 수도 있습니다 hello 동일한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="b0fab-127">예를 들어 hello 다음 명령을 모두 반환 hello 동일한 정보:</span><span class="sxs-lookup"><span data-stu-id="b0fab-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="b0fab-128">명령에 필요한 hello 매개 변수에 대 한 의심 toohelp를 사용 하 여-참조 도움말,-h 또는 az help [명령].</span><span class="sxs-lookup"><span data-stu-id="b0fab-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="b0fab-129">Hello Azure 리소스 관리자의 Azure 플랫폼 간 명령줄 인터페이스와 친숙 한 자습서 tooget 다음 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="b0fab-130">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="b0fab-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="b0fab-131">Azure CLI 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="b0fab-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="b0fab-132">Tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="b0fab-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="b0fab-133">다음 명령을 사용 하 여 hello 조직 계정을 사용 하 여 toolog:</span><span class="sxs-lookup"><span data-stu-id="b0fab-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="b0fab-134">대화형으로 입력 하 여에 toolog 포함 하려는 경우 또는</span><span class="sxs-lookup"><span data-stu-id="b0fab-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="b0fab-135">구독이 여러 개 있고 Azure 키 자격 증명 모음에 대 한 특정 한 toouse toospecify 원하는 hello toosee hello 구독 계정에 대해 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="b0fab-136">그런 다음 toospecify hello 구독 toouse, 유형:</span><span class="sxs-lookup"><span data-stu-id="b0fab-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="b0fab-137">Azure 플랫폼 간 명령줄 인터페이스를 구성하는 방법에 대한 자세한 내용은 [Azure CLI 설치](/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0fab-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="b0fab-138">새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b0fab-138">Create a new resource group</span></span>
<span data-ttu-id="b0fab-139">Azure 리소스 관리자를 사용하면 관련된 모든 리소스는 리소스 그룹의 내부에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="b0fab-140">이 자습서에서는 'ContosoResourceGroup'이라는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="b0fab-141">hello 첫 번째 매개 변수는 리소스 그룹 이름 및 hello 두 번째 매개 변수는 hello 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="b0fab-142">위치에 대 한 hello 명령을 사용 하 여 `az account list-locations` tooidentify 어떻게 toospecify이 예에서 하나는 대체 위치 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="b0fab-143">자세한 정보가 필요한 경우 `az account list-locations -h`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="b0fab-144">Hello 주요 자격 증명 모음 리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="b0fab-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="b0fab-145">키 자격 증명 모음 리소스 공급자가 구독에 등록되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="b0fab-146">이 toobe 구독 당 한 번만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="b0fab-147">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="b0fab-147">Create a key vault</span></span>
<span data-ttu-id="b0fab-148">사용 하 여 hello `az keyvault create` 명령 toocreate 주요 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="b0fab-149">이 스크립트에 세 개의 필수 매개 변수: 리소스 그룹 이름, 주요 자격 증명 모음 이름 및 hello 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="b0fab-150">예를 들어 hello 자격 증명 모음 이름을 ContosoKeyVault, hello ContosoResourceGroup, 리소스 그룹 이름 및 동아시아의 hello 위치를 사용 하는 경우 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="b0fab-151">이 명령의 출력 hello 방금 만든 hello 키 자격 증명 모음의 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="b0fab-152">hello 두 가장 중요 한 속성은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-152">hello two most important properties are:</span></span>

* <span data-ttu-id="b0fab-153">**이름**: hello 예제 ContosoKeyVault입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="b0fab-154">다른 Key Vault 명령에 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="b0fab-155">**vaultUri**: hello 예제 https://contosokeyvault.vault.azure.net입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="b0fab-156">REST API를 통해 사용자 자격 증명 모음을 사용하는 응용 프로그램은 URI를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="b0fab-157">Azure 계정에 권한이 부여 된 tooperform이이 키에 대 한 모든 작업 자격 증명 모음에 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="b0fab-158">아직 다른 사람은 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="b0fab-159">키 또는 키 자격 증명 모음 보안 toohello 추가</span><span class="sxs-lookup"><span data-stu-id="b0fab-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="b0fab-160">Hello를 사용 하 여 Azure 키 자격 증명 모음 toocreate 소프트웨어 보호 키를 하려는 경우 `az key create` 명령을 실행 하 고 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="b0fab-161">그러나 softkey.pem tooupload tooAzure 주요 자격 증명 모음을 지정 하 라는 파일에 로컬 파일로 저장.pem 파일에 있는 기존 키가 있으면 hello hello에서 다음 tooimport hello 키를 입력 합니다. PEM 파일-hello 키 자격 증명 모음 서비스에에서는 소프트웨어에 의해 hello 키를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="b0fab-162">이제는 작성 되거나 해당 URI를 사용 하 여 tooAzure 주요 자격 증명을 업로드 한 hello 키를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="b0fab-163">사용 하 여 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello 현재 버전을 가져오고 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget이 특정 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="b0fab-164">tooadd SQLPassword 라는 암호 되었으며 Pa$ $w0rd tooAzure 주요 자격 증명 유형 hello 뒤의 hello 값 비밀 toohello 자격:</span><span class="sxs-lookup"><span data-stu-id="b0fab-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="b0fab-165">이제 해당 URI를 사용 하 여 tooAzure 자격 증명 모음 키를 추가 하는이 암호를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="b0fab-166">사용 하 여 **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello 현재 버전을 가져오고 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget이 특정 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="b0fab-167">Hello 키 또는 암호 방금 만든 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="b0fab-168">tooview 프로그램 키, 유형:`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="b0fab-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="b0fab-169">tooview 비밀을 형식:`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="b0fab-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="b0fab-170">Azure Active Directory에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="b0fab-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="b0fab-171">이 단계는 일반적으로 별도의 컴퓨터에서 개발자가 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="b0fab-172">특정 tooAzure 주요 자격 증명 모음 되지만 완전성을 위해 여기에서 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0fab-173">toocomplete hello 자습서, 계정, 자격 증명 모음 hello 및이 단계에서 등록 하는 hello 응용 프로그램 모두에 있어야 hello 같은 Azure 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="b0fab-174">자격 증명 모음 키를 사용하는 응용 프로그램은 Azure Active Directory에서 토큰을 사용하여 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="b0fab-175">toodo이,이 hello hello 응용 프로그램의 소유자가 Azure Active Directory에서 먼저 hello 응용 프로그램을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="b0fab-176">등록의 hello 끝 hello 응용 프로그램 소유자 hello를 다음 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="b0fab-177">**응용 프로그램 ID** (클라이언트 ID) 및 **인증 키** (라고도 hello 공유 암호).</span><span class="sxs-lookup"><span data-stu-id="b0fab-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="b0fab-178">hello 응용 프로그램에는 모두 이러한 값 tooAzure Active Directory tooget 토큰을 제시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="b0fab-179">Hello 응용 프로그램은 어떻게 구성 toodo hello 응용 프로그램에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="b0fab-180">Hello 키 자격 증명 모음 샘플 응용 프로그램에 대 한 응용 프로그램 소유자 hello hello app.config 파일에 이러한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="b0fab-181">Azure Active Directory에서 tooregister hello 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="b0fab-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="b0fab-182">Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="b0fab-183">Hello 왼쪽에서 클릭 **Azure Active Directory**, 한 다음 응용 프로그램을 등록 하는 hello 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="b0fab-184">Hello를 선택 해야 포함 된 같은 디렉터리 hello 주요 자격 증명 모음을 만들 때 사용한 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="b0fab-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="b0fab-185">알 수 없는 디렉터리가 인지, 클릭 **설정**, 주요 자격 증명 모음을 만들 때 사용한 hello 구독을 식별 하 고 hello 디렉터리의 참고 hello 이름이 hello 마지막 열에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="b0fab-186">**APPLICATIONS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="b0fab-187">이 페이지 hello만 표시 됩니다 앱이 없습니다. tooyour 디렉터리를 추가한 경우 **앱 추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="b0fab-188">Hello 링크를 클릭 하거나 hello 클릭 해도, **추가** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="b0fab-189">Hello에 **응용 프로그램 추가** hello에서 마법사 **하 신 toodo 원하는?** 페이지에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="b0fab-190">Hello에 **응용 프로그램에 대해 알리기** 페이지 응용 프로그램에 대 한 이름을 지정 하 고 선택 **웹 응용 프로그램 및/또는 웹 API** (기본 hello).</span><span class="sxs-lookup"><span data-stu-id="b0fab-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="b0fab-191">Hello 다음 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="b0fab-192">Hello에 **앱 속성** 페이지에서 지정 하는 hello **로그온 URL** 및 **앱 ID URI** 웹 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="b0fab-193">응용 프로그램에 이러한 값이 없는 경우 이 단계에서 만들 수 있습니다(예를 들어, 두 상자에 대해 http://test1.contoso.com을 지정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="b0fab-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="b0fab-194">이러한 사이트 존재 하는 경우 중요 하지 않습니다. 중요 한 것은 각 응용 프로그램에 대 한 hello 앱 ID URI는 디렉터리의 모든 응용 프로그램에 대 한 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="b0fab-195">hello 디렉터리는이 문자열 tooidentify 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="b0fab-196">Hello 완료 아이콘 toosave hello 마법사에서 변경 내용을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="b0fab-197">Hello 빠른 시작 페이지에서 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="b0fab-198">Toohello 스크롤하여 **키** 섹션 hello 기간, 선택한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="b0fab-199">hello 페이지가 새로 고쳐지고 키 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="b0fab-200">이 키 값 및 hello 응용 프로그램을 구성 해야 **클라이언트 ID** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="b0fab-201">(이 구성에 대한 지침은 응용 프로그램에 특정된 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="b0fab-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="b0fab-202">다음 단계 tooset 권한을 hello에서 사용할 자격 증명 모음에 있는이 페이지에서 hello 클라이언트 ID 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="b0fab-203">Hello 응용 프로그램 toouse hello 키 또는 암호를 권한 부여</span><span class="sxs-lookup"><span data-stu-id="b0fab-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="b0fab-204">키 또는 암호 hello 자격 증명 모음을 사용 하 여 hello에 tooauthorize hello 응용 프로그램 tooaccess hello `az keyvault set-policy` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="b0fab-205">예를 들어 자격 증명 모음 이름이 tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed의 클라이언트 ID가 중이 고 tooauthorize hello 응용 프로그램 toodecrypt 및 서명 키를 가진 자격 증명 모음에서 원하는 ContosoKeyVault 및 hello 응용 프로그램 이면 다음 실행 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="b0fab-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="b0fab-206">자격 증명 모음에는 동일한 응용 프로그램 tooread 비밀 tooauthorize 않으려면 hello 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="b0fab-207">하드웨어 보안 모듈 (HSM) toouse 하려는 경우</span><span class="sxs-lookup"><span data-stu-id="b0fab-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="b0fab-208">추가 된 보증에 대 한 가져오기 또는 hello HSM 경계를 벗어날 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="b0fab-209">hello Hsm은 FIPS 140-2 수준 2 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="b0fab-210">이 요구 사항을 tooyou을 적용 하지 않는 경우이 섹션을 건너뛰고 이동 너무[hello 주요 자격 증명 모음 및 연결 된 키와 비밀 삭제](#delete-the-key-vault-and-associated-keys-and-secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="b0fab-211">toocreate 이러한 HSM 보호 키를 지 원하는 HSM 보호 키 자격 증명 모음 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="b0fab-212">Hello keyvault를 만들 때 hello 'sku' 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="b0fab-213">(앞에서 보았듯이) 소프트웨어 보호 키를 추가 하 고 HSM 보호 키 toothis 자격 증명 모음 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="b0fab-214">toocreate는 HSM 보호 키 집합 hello 대상 매개 변수 too'HSM':</span><span class="sxs-lookup"><span data-stu-id="b0fab-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="b0fab-215">Hello 명령 tooimport 키.pem 파일을 컴퓨터에에서 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="b0fab-216">이 명령은 hello 키 자격 증명 모음 서비스에서에서 Hsm에 hello 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="b0fab-217">다음 명령은 hello "bring your own key"을 가져옵니다 (BYOK) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="b0fab-218">이렇게 하면 로컬 HSM의 키를 생성 하 여 hello HSM 경계를 종료 하는 hello 키 없이 tooHSMs hello 키 자격 증명 모음 서비스에에서 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="b0fab-219">자세한 방법에 대 한 지침은 toogenerate이 BYOK 패키지 참조 [어떻게 toouse HSM-Protected 키는 Azure 키 자격 증명](key-vault-hsm-protected-keys.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="b0fab-220">Hello 주요 자격 증명 모음 및 연결 된 키와 비밀 정보를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="b0fab-221">Hello 주요 자격 증명 모음 및 hello 키 또는 암호에 포함 된 더 이상 필요 하면 hello를 사용 하 여 hello 주요 자격 증명 모음을 삭제할 수 없습니다 `az keyvault delete` 명령:</span><span class="sxs-lookup"><span data-stu-id="b0fab-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="b0fab-222">또는 hello 주요 자격 증명 모음 및 해당 그룹에 포함 된 다른 모든 리소스를 포함 하는 전체 Azure 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="b0fab-223">다른 Azure 플랫폼 간 명령줄 인터페이스 명령</span><span class="sxs-lookup"><span data-stu-id="b0fab-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="b0fab-224">Azure 키 자격 증명 모음을 관리하는 데 유용할 수 있는 다른 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="b0fab-225">이 명령은 모든 키와 선택한 속성을 테이블 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="b0fab-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="b0fab-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="b0fab-227">이 명령은 hello 지정 된 키에 대 한 속성의 전체 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="b0fab-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="b0fab-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="b0fab-229">이 명령은 모든 비밀 이름과 선택한 속성을 테이블 형식으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="b0fab-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="b0fab-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="b0fab-231">방법의 예로 특정 키 tooremove:</span><span class="sxs-lookup"><span data-stu-id="b0fab-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="b0fab-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="b0fab-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="b0fab-233">방법의 예로 특정 보안 tooremove:</span><span class="sxs-lookup"><span data-stu-id="b0fab-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="b0fab-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="b0fab-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="b0fab-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b0fab-235">Next steps</span></span>
<span data-ttu-id="b0fab-236">Key Vault 명령에 대한 전체 Azure CLI 참조에 대해서는 [Key Vault CLI 참조](/cli/azure/keyvault)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0fab-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="b0fab-237">프로그래밍 참조에 대 한 참조 [Azure 키 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0fab-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
