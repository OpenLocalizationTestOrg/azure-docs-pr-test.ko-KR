---
title: "CLI를 사용하여 Azure Key Vault 관리 | Microsoft Docs"
description: "이 자습서에서는 CLI 2.0을 사용하여 Key Vault의 일반 작업을 자동화하는 방법을 설명합니다."
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
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="2d1f6-103">CLI 2.0을 사용하여 Key Vault 관리</span><span class="sxs-lookup"><span data-stu-id="2d1f6-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="2d1f6-104">Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="2d1f6-105">자세한 내용은 [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="2d1f6-106">소개</span><span class="sxs-lookup"><span data-stu-id="2d1f6-106">Introduction</span></span>
<span data-ttu-id="2d1f6-107">이 자습서를 사용하면 Azure 키 자격 증명 모음으로 시작하여 확정된 컨테이너(자격 증명 모음)를 Azure에 만들고 Azure에서 암호화 키와 비밀을 저장하고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="2d1f6-108">Azure 플랫폼 간 명령줄 인터페이스를 사용하여 Azure 응용 프로그램과 함께 사용할 수 있는 키 또는 암호를 포함하는 자격 증명 모음을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="2d1f6-109">응용 프로그램이 수 해당 키 또는 암호를 사용할 수 있는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="2d1f6-110">**예상 완료 시간:** 20분</span><span class="sxs-lookup"><span data-stu-id="2d1f6-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="2d1f6-111">이 자습서에는 단계 중 하나에 포함되는 Azure 응용 프로그램을 작성하는 방법에 대한 지침을 포함하지 않으며, 키 자격 증명 모음에서 키나 비밀을 사용하도록 응용 프로그램을 인증하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="2d1f6-112">이 자습서에서는 최신 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="2d1f6-113">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="2d1f6-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d1f6-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2d1f6-114">Prerequisites</span></span>
<span data-ttu-id="2d1f6-115">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="2d1f6-116">Microsoft Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="2d1f6-117">아직 구독하지 않은 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="2d1f6-118">명령줄 인터페이스 버전 2.0 이상.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="2d1f6-119">최신 버전을 설치하고 Azure 구독에 연결하려면 [Azure 플랫폼 간 명령줄 인터페이스 2.0 설치 및 구성](/cli/azure/install-azure-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="2d1f6-120">이 자습서에서 만드는 키 또는 암호를 사용하여 구성되는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="2d1f6-121">샘플 응용 프로그램은 [Microsoft 다운로드 센터](http://www.microsoft.com/download/details.aspx?id=45343)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="2d1f6-122">자세한 내용은 해당 추가 정보 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="2d1f6-123">Azure 플랫폼 간 명령줄 인터페이스 도움말 보기</span><span class="sxs-lookup"><span data-stu-id="2d1f6-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="2d1f6-124">이 자습서에서는 명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)를 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="2d1f6-125">--help 또는 -h 매개 변수를 사용하여 특정 명령에 대한 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="2d1f6-126">또는 azure help [command] [options] 형식을 사용하여 동일한 정보를 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="2d1f6-127">예를 들어 다음 명령은 모두 동일한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="2d1f6-128">명령에 필요한 매개 변수가 확실하지 않은 경우 --help, -h 또는 az help [command]를 사용하여 도움말을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="2d1f6-129">다음 자습서를 통해 Azure 플랫폼 간 명령줄 인터페이스의 Azure 리소스 관리자를 학습할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="2d1f6-130">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="2d1f6-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="2d1f6-131">Azure CLI 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="2d1f6-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="2d1f6-132">구독에 연결</span><span class="sxs-lookup"><span data-stu-id="2d1f6-132">Connect to your subscriptions</span></span>
<span data-ttu-id="2d1f6-133">조직 계정을 사용하여 로그인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="2d1f6-134">또는 대화형으로 입력하여 로그인하려는 경우</span><span class="sxs-lookup"><span data-stu-id="2d1f6-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="2d1f6-135">여러 구독이 있는 경우 Azure 키 자격 증명 모음에 사용할 특정 하나를 지정하려면, 다음을 입력하여 계정에 대한 구독을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="2d1f6-136">그런 후, 사용할 구독을 지정하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="2d1f6-137">Azure 플랫폼 간 명령줄 인터페이스를 구성하는 방법에 대한 자세한 내용은 [Azure CLI 설치](/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="2d1f6-138">새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="2d1f6-138">Create a new resource group</span></span>
<span data-ttu-id="2d1f6-139">Azure 리소스 관리자를 사용하면 관련된 모든 리소스는 리소스 그룹의 내부에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="2d1f6-140">이 자습서에서는 'ContosoResourceGroup'이라는 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="2d1f6-141">첫 번째 매개 변수는 리소스 그룹 이름이고, 두 번째 매개 변수 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="2d1f6-142">위치의 경우, `az account list-locations` 명령을 사용하여 이 예에서 대체 위치를 지정하는 방법을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="2d1f6-143">자세한 정보가 필요한 경우 `az account list-locations -h`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="2d1f6-144">키 자격 증명 모음 리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="2d1f6-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="2d1f6-145">키 자격 증명 모음 리소스 공급자가 구독에 등록되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="2d1f6-146">구독당 한 번만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="2d1f6-147">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="2d1f6-147">Create a key vault</span></span>
<span data-ttu-id="2d1f6-148">`az keyvault create` 명령을 사용하여 키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="2d1f6-149">이 스크립트에는 3개의 필수 매개 변수, 리소스 그룹 이름, 키 자격 증명 모음 이름 및 지리적 위치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="2d1f6-150">예를 들어, 이름이 ContosoKeyVault이고, 리소스 그룹 이름이 ContosoResourceGroup이며 위치가 동아시아인 형식의 자격 증명 모음인 경우, 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="2d1f6-151">이 명령의 출력에서는 방금 만든 자격 증명 모음의 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="2d1f6-152">가장 중요한 두 개의 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-152">The two most important properties are:</span></span>

* <span data-ttu-id="2d1f6-153">**name**: 이 예제에서는 ContosoKeyVault입니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="2d1f6-154">다른 Key Vault 명령에 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="2d1f6-155">**vaultUri**: 예제에서는 https://contosokeyvault.vault.azure.net입니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="2d1f6-156">REST API를 통해 사용자 자격 증명 모음을 사용하는 응용 프로그램은 URI를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="2d1f6-157">Azure 계정은 이제 이 키 자격 증명 모음에서 모든 작업을 수행할 권한을 가지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="2d1f6-158">아직 다른 사람은 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="2d1f6-159">키 또는 암호를 키 자격 증명 모음에 추가</span><span class="sxs-lookup"><span data-stu-id="2d1f6-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="2d1f6-160">소프트웨어 보호 키를 만들도록 Azure 키 자격 증명 모음을 사용하려면, `az key create` 명령을 사용하여 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="2d1f6-161">그러나 Azure 키 자격 증명 모음에 업로드하려는 softkey.pem이라는 파일에 로컬 파일로 저장된 .pem 파일의 기존 키가 있는 경우 다음을 입력하여 키 자격 증명 모음 서비스에서 소프트웨어로 키를 보호하는 .PEM 파일에서 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="2d1f6-162">이제 해당 URI를 사용하여 Azure 키 자격 증명 모음을 만들거나 업로드하는 이 키를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="2d1f6-163">**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey**를 사용하여 현재 버전을 가져오고 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87**을 사용하여 이 특정 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="2d1f6-164">자격 증명 모음에 암호를 추가하려면 다음을 입력합니다. 암호는 SQLPassword이며 Azure 키 자격 증명 모음에 대한 Pa$$w0rd 값을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="2d1f6-165">이제 해당 URI를 사용하여 Azure 키 자격 증명 모음에 추가한 이 암호를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="2d1f6-166">**https://ContosoVault.vault.azure.net/secrets/SQLPassword**를 사용하여 현재 버전을 가져오고 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d**를 사용하여 이 특정 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="2d1f6-167">방금 만든 키 또는 암호를 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="2d1f6-168">사용자의 키를 보려면 다음을 입력 합니다. `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="2d1f6-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="2d1f6-169">사용자의 비밀을 보려면 다음을 입력 합니다. `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="2d1f6-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="2d1f6-170">Azure Active Directory에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="2d1f6-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="2d1f6-171">이 단계는 일반적으로 별도의 컴퓨터에서 개발자가 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="2d1f6-172">Azure 키 자격 증명 모음에 특정한 것은 아니지만 완전성을 위해 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d1f6-173">이 단계에서 등록된 자습서, 계정, 해당 자격 증명 모음 및 응용 프로그램을 완료하려면, 모두 동일한 Azure 디렉터리에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="2d1f6-174">자격 증명 모음 키를 사용하는 응용 프로그램은 Azure Active Directory에서 토큰을 사용하여 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="2d1f6-175">이렇게 하려면 응용 프로그램의 소유자가 Azure Active Directory에 먼저 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="2d1f6-176">등록 끝에 응용 프로그램 소유자는 다음 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="2d1f6-177">**응용 프로그램 ID**(클라이언트 ID라고도 함) 및 **인증 키**(공유 비밀이라고도 함).</span><span class="sxs-lookup"><span data-stu-id="2d1f6-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="2d1f6-178">응용 프로그램은 토큰을 가져올 Azure Active Directory에 이 두 값 모두가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="2d1f6-179">응용 프로그램 구성 방식은 응용 프로그램에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="2d1f6-180">키 자격 증명 모음 샘플 응용 프로그램의 경우, 응용 프로그램 소유자는 app.config 파일에서 이러한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="2d1f6-181">Azure Active Directory에 응용 프로그램을 등록하려면:</span><span class="sxs-lookup"><span data-stu-id="2d1f6-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="2d1f6-182">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="2d1f6-183">왼쪽에서 **Azure Active Directory**를 클릭한 다음 응용 프로그램을 등록할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="2d1f6-184">주요 자격 증명 모음을 만든 Azure 구독을 포함하는 동일한 디렉터리를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="2d1f6-185">이 디렉터리를 모르는 경우, **설정**을 클릭하고, 사용자 키 자격 증명 모음을 만든 구독을 식별하고 마지막 열에 표시되는 디렉터리의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="2d1f6-186">**APPLICATIONS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="2d1f6-187">디렉터리에 추가한 앱이 없는 경우,이 페이지는 **앱 추가** 링크만을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="2d1f6-188">링크를 클릭하거나 명령 모음에서 **추가** 를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="2d1f6-189">**응용 프로그램 추가** 마법사에서 **무엇을 하고 싶나요?** 페이지를 클릭하고, **조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="2d1f6-190">**응용 프로그램에 대해 알려주세요** 페이지에서, 응용 프로그램 이름을 지정하고 **웹 응용 프로그램 및/또는 Web API**(기본값)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="2d1f6-191">다음 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-191">Click the Next icon.</span></span>
6. <span data-ttu-id="2d1f6-192">**앱 속성** 페이지에서 웹 응용 프로그램에 대한 **로그인 URL** 및 **앱 ID URI**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="2d1f6-193">응용 프로그램에 이러한 값이 없는 경우 이 단계에서 만들 수 있습니다(예를 들어, 두 상자에 대해 http://test1.contoso.com을 지정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="2d1f6-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="2d1f6-194">이러한 사이트가 존재하는 지가 중요하지 않습니다. 사용자 디렉토리의 각 응용 프로그램에 대해 각 응용 프로그램의 앱 ID URI가 다르다는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="2d1f6-195">디렉터리는 이 문자열을 사용하여 앱을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="2d1f6-196">마법사에서 변경 내용을 저장하려면 전체 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="2d1f6-197">빠른 시작 페이지에서 **CONFIGURE**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="2d1f6-198">**키** 섹션으로 스크롤하고 기간을 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="2d1f6-199">페이지가 새로 고쳐지고 이제 키 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="2d1f6-200">이 키 값 및 **클라이언트 ID** 가 있는 응용 프로그램을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="2d1f6-201">(이 구성에 대한 지침은 응용 프로그램에 특정된 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="2d1f6-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="2d1f6-202">사용자 자격 증명 모음에 사용 권한을 설정하려면 다음 단계에서 사용하는 이 페이지에서 클라이언트 ID 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="2d1f6-203">응용 프로그램에 키 또는 암호를 사용하도록 권한 부여</span><span class="sxs-lookup"><span data-stu-id="2d1f6-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="2d1f6-204">응용 프로그램이 자격 증명 모음의 키 또는 암호에 대한 액세스를 인증하려면 `az keyvault set-policy` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="2d1f6-205">예를 들어, 자격 증명 모음 이름은 ContosoKeyVault이고 권한을 부여하려는 응용 프로그램에 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed의 클라이언트 ID가 있고 자격 증명 모음에 있는 키로 서명하고 암호 해제하도록 응용 프로그램을 인증하려면, 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="2d1f6-206">자격 증명 모음에서 기밀 정보를 읽기 위해 동일한 응용 프로그램에 권한을 부여하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="2d1f6-207">하드웨어 보안 모듈(HSM)을 사용하려는 경우</span><span class="sxs-lookup"><span data-stu-id="2d1f6-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="2d1f6-208">추가된 보증을 위해, HSM 경계를 절대로 떠나지 않는 하드웨어 보안 모듈(HSMs)에서 키를 가져오거나 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="2d1f6-209">HSM은 FIPS 140-2 Level 2 유효성 검사가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="2d1f6-210">이 요구 사항이 사용자에게 적용되지 않는 경우, 이 섹션을 건너뛰고 [키 자격 증명 모음 및 연결된 키와 암호 삭제](#delete-the-key-vault-and-associated-keys-and-secrets)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="2d1f6-211">이러한 HSM 보호되는 키를 만들려면, HSM 보호되는 키를 지원하는 자격 증명 모음 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="2d1f6-212">keyvault를 만들 때 'sku' 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="2d1f6-213">이 자격 증명이 모음에 소프트웨어 보호 키(이전에 표시된 대로)와 HSM 보호되는 키를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="2d1f6-214">HSM으로 보호되는 키를 만들려면, 대상 매개 변수를 'HSM'으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="2d1f6-215">다음 명령을 사용하여 사용자 컴퓨터의 .pem 파일에서 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="2d1f6-216">이 명령은 키 자격 증명 모음 서비스에서 HSM으로 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="2d1f6-217">다음 명령은 "bring your own key"(BYOK) 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="2d1f6-218">이렇게 하면 로컬 HSM에 키를 생성하고 키가 HSM 경계를 벗어나지 않고 이를 키 자격 증명 모음 서비스의 HSM에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="2d1f6-219">이 BYOK 패키지를 생성하는 방법에 대한 자세한 내용은 [Azure 키 자격 증명 모음과 HSM-보호된 키를 사용하는 방법](key-vault-hsm-protected-keys.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="2d1f6-220">키 자격 증명 모음 및 연결된 키와 암호 삭제</span><span class="sxs-lookup"><span data-stu-id="2d1f6-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="2d1f6-221">Key Vault 및 이를 포함하는 키나 비밀이 더 이상 필요하지 않은 경우, `az keyvault delete` 명령을 사용하여 Key Vault를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="2d1f6-222">또는 키 자격 증명 모음 및 해당 그룹에 포함된 다른 모든 리소스 및 키를 포함하는 전체 Azure 리소스 그룹을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="2d1f6-223">다른 Azure 플랫폼 간 명령줄 인터페이스 명령</span><span class="sxs-lookup"><span data-stu-id="2d1f6-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="2d1f6-224">Azure 키 자격 증명 모음을 관리하는 데 유용할 수 있는 다른 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="2d1f6-225">이 명령은 모든 키와 선택한 속성을 테이블 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="2d1f6-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="2d1f6-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="2d1f6-227">이 명령은 지정된 키에 대한 속성의 전체 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="2d1f6-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="2d1f6-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="2d1f6-229">이 명령은 모든 비밀 이름과 선택한 속성을 테이블 형식으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="2d1f6-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="2d1f6-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="2d1f6-231">다음은 특정 키를 제거하는 방법에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="2d1f6-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="2d1f6-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="2d1f6-233">다음은 특정 암호를 제거하는 방법에 대한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="2d1f6-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="2d1f6-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="2d1f6-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d1f6-235">Next steps</span></span>
<span data-ttu-id="2d1f6-236">Key Vault 명령에 대한 전체 Azure CLI 참조에 대해서는 [Key Vault CLI 참조](/cli/azure/keyvault)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="2d1f6-237">프로그래밍 참조는 [Azure 주요 자격 증명 모음 개발자 가이드](key-vault-developers-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d1f6-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
