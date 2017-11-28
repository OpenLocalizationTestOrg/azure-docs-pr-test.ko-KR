---
title: "Azure에서 Linux VM의 디스크 암호화 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 보안 강화를 위해 Linux VM에서 가상 디스크를 암호화하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 172b4c8f5c098d776cb689543f5d8f163b8895b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="0a712-103">Linux VM에서 가상 디스크를 암호화하는 방법</span><span class="sxs-lookup"><span data-stu-id="0a712-103">How to encrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="0a712-104">VM(가상 컴퓨터)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="0a712-105">디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="0a712-106">이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="0a712-107">이 문서에서는 Azure CLI 2.0을 사용하여 Linux VM에서 가상 디스크를 암호화하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span></span> <span data-ttu-id="0a712-108">[Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0a712-109">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="0a712-109">Quick commands</span></span>
<span data-ttu-id="0a712-110">작업을 빠르게 완료해야 하는 경우 다음 섹션에서 VM에서 가상 디스크를 암호화하는 기본 명령에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="0a712-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="0a712-111">각 단계에 대한 보다 자세한 내용 및 상황 설명은 [여기서부터](#overview-of-disk-encryption) 문서 끝까지 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a712-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="0a712-112">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="0a712-113">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0a712-114">예제 매개 변수 이름에는 *myResourceGroup*, *myKey*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="0a712-115">먼저 Azure 구독 내에서 [az provider register](/cli/azure/provider#register)를 사용하여 Azure Key Vault 공급자를 사용하도록 설정하고 [az group create](/cli/azure/group#create)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0a712-116">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-116">The following example creates a resource group name *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0a712-117">[az keyvault create](/cli/azure/keyvault#create)를 사용하여 Azure Key Vault을 만들고 디스크 암호화에 사용할 Key Vault를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="0a712-118">*keyvault_name*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="0a712-119">[az keyvault key create](/cli/azure/keyvault/key#create)를 사용하여 Key Vault에 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="0a712-120">다음 예제는 *myKey*라는 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-120">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="0a712-121">[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)에서 Azure Active Directory를 사용하여 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="0a712-122">서비스 사용자는 인증 및 Key Vault에서의 암호화 키 교환을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="0a712-123">다음 예제에서는 후속 명령에서 사용하기 위해 서비스 사용자 ID 및 암호 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-123">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="0a712-124">암호는 서비스 사용자를 만들 때만 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-124">The password is only output when you create the service principal.</span></span> <span data-ttu-id="0a712-125">원할 경우 암호(`echo $sp_password`)를 보고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-125">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="0a712-126">[az ad sp list](/cli/azure/ad/sp#list)를 사용하여 서비스 사용자를 나열하고 [az ad sp show](/cli/azure/ad/sp#show)를 사용하여 특정 서비스 사용자에 대한 추가 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="0a712-127">[az keyvault set-policy](/cli/azure/keyvault#set-policy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="0a712-128">다음 예제에서는 이전 명령의 서비스 사용자 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-128">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="0a712-129">[az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들고 5GB 데이터 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="0a712-130">특정 Marketplace 이미지만 디스크 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="0a712-131">다음 예제는 **CentOS 7.2n** 이미지를 사용하여 `myVM`이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="0a712-132">위 명령의 출력에 표시된 `publicIpAddress`를 사용해서 VM에 대해 SSH를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-132">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="0a712-133">파티션 및 파일 시스템을 만든 후 데이터 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-133">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="0a712-134">자세한 내용은 [Linux VM에 연결하여 새 디스크 탑재](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a712-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="0a712-135">SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-135">Close your SSH session.</span></span>

<span data-ttu-id="0a712-136">[az vm encryption enable](/cli/azure/vm/encryption#enable)을 사용하여 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="0a712-137">다음 예제에서는 이전 `ad sp create-for-rbac` 명령의 `$sp_id` 및 `$sp_password` 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="0a712-138">디스크 암호화 프로세스를 완료하는 데 약간의 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-138">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="0a712-139">[az vm encryption show](/cli/azure/vm/encryption#show)를 사용하여 프로세스의 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="0a712-140">상태에는 **EncryptionInProgress**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-140">The status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="0a712-141">OS 디스크의 상태가 **VMRestartPending**을 보고할 때까지 기다린 후 [az vm restart](/cli/azure/vm#restart)를 사용하여 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="0a712-142">부팅 프로세스 동안 디스크 암호화 프로세스가 완료되므로, 몇 분 정도 기다렸다가 **az vm encryption show**를 사용하여 암호화 상태를 다시 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0a712-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="0a712-143">이제 상태는 OS 디스크와 데이터 디스크를 둘 다 **Encrypted**로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-143">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="0a712-144">디스크 암호화 개요</span><span class="sxs-lookup"><span data-stu-id="0a712-144">Overview of disk encryption</span></span>
<span data-ttu-id="0a712-145">Linux VM의 가상 디스크는 미사용 시 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt)를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="0a712-146">Azure에서 가상 디스크 암호화는 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="0a712-147">암호화 키는 소프트웨어 보호를 사용하여 Azure Key Vault에 저장되거나 FIPS 140-2 레벨 2 표준 인증 HSM(하드웨어 보안 모듈)에서 키를 가져오거나 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="0a712-148">이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="0a712-149">이러한 암호화 키는 VM에 연결된 가상 디스크를 암호화하고 암호를 해독하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="0a712-150">Azure Active Directory 서비스 사용자는 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="0a712-151">VM을 암호화하는 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="0a712-152">Azure Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="0a712-153">암호화하는 디스크에 사용될 수 있도록 암호화 키를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="0a712-154">Azure Key Vault에서 암호화 키를 읽어오려면 적절한 사용 권한을 통해 Azure Active Directory 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="0a712-155">가상 디스크를 암호화하도록 명령을 실행하고 사용될 Azure Active Directory 서비스 사용자와 적절한 암호화 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="0a712-156">Azure Active Directory 서비스 사용자는 Azure Key Vault에 필요한 암호화 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="0a712-157">가상 디스크는 제공된 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="0a712-158">암호화 프로세스</span><span class="sxs-lookup"><span data-stu-id="0a712-158">Encryption process</span></span>
<span data-ttu-id="0a712-159">디스크 암호화는 다음과 같은 추가 구성 요소에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="0a712-160">**Azure Key Vault** - 디스크 암호화/암호 해독 프로세스를 위한 암호화 키와 암호를 안전하게 보호하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="0a712-161">이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="0a712-162">Key Vault를 디스크 암호화에 전적으로 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="0a712-163">관리 범위 및 키 표시 여부를 분리하기 위해 전용 Key Vault를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="0a712-164">**Azure Active Directory** - 필요한 암호화 키의 안전한 교환과 요청된 작업에 대한 인증을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="0a712-165">일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="0a712-166">서비스 사용자는 해당 암호화 키를 요청하고 발급되도록 하는 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="0a712-167">Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="0a712-168">요구 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="0a712-168">Requirements and limitations</span></span>
<span data-ttu-id="0a712-169">디스크 암호화에 대해 지원되는 시나리오 및 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="0a712-170">다음 Linux Server SKU - Ubuntu, CentOS, SUSE 및 SLES(SUSE Linux Enterprise Server)와 Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="0a712-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="0a712-171">모든 리소스(예: Key Vault, 저장소 계정, VM)는 동일한 Azure 지역 및 구독 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="0a712-172">표준 A, D, DS, G 및 GS 시리즈 VM.</span><span class="sxs-lookup"><span data-stu-id="0a712-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="0a712-173">다음 시나리오의 경우 디스크 암호화가 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="0a712-174">기본 계층 VM.</span><span class="sxs-lookup"><span data-stu-id="0a712-174">Basic tier VMs.</span></span>
* <span data-ttu-id="0a712-175">클래식 배포 모델을 사용하여 만든 VM.</span><span class="sxs-lookup"><span data-stu-id="0a712-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="0a712-176">Linux VM에서 OS 디스크 암호화 비활성화.</span><span class="sxs-lookup"><span data-stu-id="0a712-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="0a712-177">이미 암호화된 Linux VM에서 암호화 키 업데이트.</span><span class="sxs-lookup"><span data-stu-id="0a712-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="0a712-178">Azure Key Vault 및 키 만들기</span><span class="sxs-lookup"><span data-stu-id="0a712-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="0a712-179">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="0a712-180">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-180">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0a712-181">예제 매개 변수 이름에는 *myResourceGroup*, *myKey*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="0a712-182">첫 번째 단계는 암호화 키를 저장할 Azure Key Vault를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="0a712-183">Azure Key Vault는 응용 프로그램 및 서비스에 안전하게 구현할 수 있는 키와 암호를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="0a712-184">가상 디스크 암호화의 경우 Key Vault를 사용하여 가상 디스크 암호화 또는 암호 해독에 사용되는 암호화 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="0a712-185">Azure 구독 내에서 [az provider register](/cli/azure/provider#register)를 사용하여 Azure Key Vault 공급자를 사용하도록 설정하고 [az group create](/cli/azure/group#create)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-185">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0a712-186">다음 예제에서는 `eastus` 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-186">The following example creates a resource group name *myResourceGroup* in the `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0a712-187">암호화 키를 포함하는 Azure Key Vault와 저장소 및 VM과 같은 연결된 계산 리소스는 동일한 지역에 상주해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="0a712-188">[az keyvault create](/cli/azure/keyvault#create)를 사용하여 Azure Key Vault을 만들고 디스크 암호화에 사용할 Key Vault를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="0a712-189">*keyvault_name*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="0a712-190">소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="0a712-191">HSM을 사용하려면 프리미엄 Key Vault가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="0a712-192">소프트웨어 보호 키를 저장하는 표준 Key Vault가 아닌 프리미엄 Key Vault를 만들려면 추가 비용이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-192">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="0a712-193">프리미엄 Key Vault를 만들려면 앞의 단계에서 `--sku Premium`을 명령에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-193">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="0a712-194">표준 Key Vault를 만들었기 때문에 다음 예제는 소프트웨어 보호 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-194">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="0a712-195">두 가지 보호 모델 모두, 가상 디스크의 암호를 해독하기 위해 VM이 부팅될 때 암호화 키를 요청하려면 Azure 플랫폼에 액세스 권한이 허용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-195">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="0a712-196">[az keyvault key create](/cli/azure/keyvault/key#create)를 사용하여 Key Vault에 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="0a712-197">다음 예제는 *myKey*라는 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-197">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="0a712-198">Azure Active Directory 서비스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0a712-198">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="0a712-199">가상 디스크가 암호화되거나 암호가 해독될 때 계정을 지정하여 Key Vault의 암호화 키 교환 및 인증을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-199">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="0a712-200">이 계정 즉, Azure Active Directory 서비스 사용자는 Azure 플랫폼이 VM을 대신하여 적절한 암호화 키를 요청하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-200">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="0a712-201">기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="0a712-202">[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)에서 Azure Active Directory를 사용하여 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="0a712-203">다음 예제에서는 후속 명령에서 사용하기 위해 서비스 사용자 ID 및 암호 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-203">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="0a712-204">암호는 서비스 사용자를 만들 때만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-204">The password is only displayed when you create the service principal.</span></span> <span data-ttu-id="0a712-205">원할 경우 암호(`echo $sp_password`)를 보고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-205">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="0a712-206">[az ad sp list](/cli/azure/ad/sp#list)를 사용하여 서비스 사용자를 나열하고 [az ad sp show](/cli/azure/ad/sp#show)를 사용하여 특정 서비스 사용자에 대한 추가 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="0a712-207">가상 디스크를 암호화하거나 암호를 해독하려면, Key Vault에 저장되어 있는 암호화 키에 대한 권한이 Azure Active Directory 서비스 사용자가 키를 읽는 것을 허용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-207">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="0a712-208">[az keyvault set-policy](/cli/azure/keyvault#set-policy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="0a712-209">다음 예제에서는 이전 명령의 서비스 사용자 ID가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-209">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="0a712-210">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="0a712-210">Create virtual machine</span></span>
<span data-ttu-id="0a712-211">일부 가상 디스크를 실제로 암호화하기 위해 VM을 만들고 데이터 디스크를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-211">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="0a712-212">[az vm create](/cli/azure/vm#create)를 사용하여 암호화할 VM을 만들고 5GB 데이터 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-212">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="0a712-213">특정 Marketplace 이미지만 디스크 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="0a712-214">다음 예제는 **CentOS 7.2n** 이미지를 사용하여 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-214">The following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="0a712-215">위 명령의 출력에 표시된 `publicIpAddress`를 사용해서 VM에 대해 SSH를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-215">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="0a712-216">파티션 및 파일 시스템을 만든 후 데이터 디스크를 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-216">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="0a712-217">자세한 내용은 [Linux VM에 연결하여 새 디스크 탑재](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a712-217">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="0a712-218">SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="0a712-219">가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="0a712-219">Encrypt virtual machine</span></span>
<span data-ttu-id="0a712-220">가상 디스크를 암호화하기 위해서 이전의 구성 요소를 모두 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-220">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="0a712-221">Azure Active Directory 서비스 사용자 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-221">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="0a712-222">암호화된 디스크에 대한 메타데이터를 저장할 Key Vault를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-222">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="0a712-223">실제 암호화 및 암호 해독에 사용될 암호화 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-223">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="0a712-224">OS 디스크, 데이터 디스크 또는 모든 디스크를 암호화할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-224">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="0a712-225">[az vm encryption enable](/cli/azure/vm/encryption#enable)을 사용하여 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="0a712-226">다음 예제에서는 이전 `ad sp create-for-rbac` 명령의 `$sp_id` 및 `$sp_password` 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-226">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="0a712-227">디스크 암호화 프로세스를 완료하는 데 약간의 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-227">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="0a712-228">[az vm encryption show](/cli/azure/vm/encryption#show)를 사용하여 프로세스의 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-228">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="0a712-229">다음의 잘린 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-229">The output is similar to the following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="0a712-230">OS 디스크의 상태가 **VMRestartPending**을 보고할 때까지 기다린 후 [az vm restart](/cli/azure/vm#restart)를 사용하여 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-230">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="0a712-231">부팅 프로세스 동안 디스크 암호화 프로세스가 완료되므로, 몇 분 정도 기다렸다가 **az vm encryption show**를 사용하여 암호화 상태를 다시 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0a712-231">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="0a712-232">이제 상태는 OS 디스크와 데이터 디스크를 둘 다 **Encrypted**로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-232">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="0a712-233">데이터 디스크 더 추가하기</span><span class="sxs-lookup"><span data-stu-id="0a712-233">Add additional data disks</span></span>
<span data-ttu-id="0a712-234">데이터 디스크를 암호화하고 나면 나중에 VM에 가상 디스크를 더 추가하고 암호화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-234">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="0a712-235">예를 들어 다음과 같이 VM에 두 번째 가상 디스크를 추가해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-235">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="0a712-236">명령을 다시 실행하여 다음과 같이 가상 디스크를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="0a712-236">Re-run the command to encrypt the virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="0a712-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a712-237">Next steps</span></span>
* <span data-ttu-id="0a712-238">암호화 키 및 Key Vault 삭제를 비롯한 Azure Key Vault 관리에 대한 자세한 내용은 [CLI를 사용하여 Key Vault 관리](../../key-vault/key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a712-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="0a712-239">Azure에 업로드할 암호화된 사용자 지정 VM 준비와 같은 디스크 암호화에 대한 자세한 내용은 [Azure Disk Encryption](../../security/azure-security-disk-encryption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a712-239">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
