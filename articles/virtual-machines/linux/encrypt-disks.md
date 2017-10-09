---
title: "Azure에서 Linux VM의 디스크 aaaEncrypt | Microsoft Docs"
description: "Tooencrypt 가상 디스크를 사용 하 여 향상 된 보안에 대 한 Linux VM에 Azure CLI 2.0 hello 하는 방법"
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
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="4b230-103">어떻게 tooencrypt Linux VM의 가상 디스크</span><span class="sxs-lookup"><span data-stu-id="4b230-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="4b230-104">VM(가상 컴퓨터)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="4b230-105">디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="4b230-106">이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="4b230-107">이 문서 tooencrypt 가상 디스크를 사용 하 여 Linux VM에 Azure CLI 2.0 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="4b230-108">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="4b230-109">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="4b230-109">Quick commands</span></span>
<span data-ttu-id="4b230-110">Hello 작업을 수행 tooquickly 해야 할 경우에 다음 섹션의 세부 정보 hello 기본 hello tooencrypt 가상 디스크를 VM에 명령, 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="4b230-111">각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](#overview-of-disk-encryption)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="4b230-112">최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="4b230-113">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4b230-114">예제 매개 변수 이름에는 *myResourceGroup*, *myKey*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="4b230-115">먼저, hello Azure 키 자격 증명 모음 공급자와 Azure 구독 내에서 사용할 수 있도록 [az 리소스 공급자 등록](/cli/azure/provider#register) 리소스 그룹을 만들고 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4b230-116">hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 *myResourceGroup* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="4b230-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4b230-117">Azure 키 자격 증명 모음 만들기와 [az keyvault 만들](/cli/azure/keyvault#create) 디스크 암호화와 함께 사용 하기 위해 주요 자격 증명 모음 hello를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="4b230-118">*keyvault_name*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="4b230-119">[az keyvault key create](/cli/azure/keyvault/key#create)를 사용하여 Key Vault에 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="4b230-120">hello 다음 예제에서는 라는 키 *myKey*:</span><span class="sxs-lookup"><span data-stu-id="4b230-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="4b230-121">[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)에서 Azure Active Directory를 사용하여 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="4b230-122">hello 서비스 보안 주체 핸들에는 인증 및 자격 증명 모음 키에서에서 암호화 키의 교환을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="4b230-123">다음 예제는 hello Id와 암호 이후 명령에서 사용 하도록 hello 서비스 사용자에 대 한 hello 값 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="4b230-124">hello 암호 hello 서비스 주체를 만들 때에 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="4b230-125">뷰와 레코드 hello 암호 필요 (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="4b230-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="4b230-126">[az ad sp list](/cli/azure/ad/sp#list)를 사용하여 서비스 사용자를 나열하고 [az ad sp show](/cli/azure/ad/sp#show)를 사용하여 특정 서비스 사용자에 대한 추가 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="4b230-127">[az keyvault set-policy](/cli/azure/keyvault#set-policy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="4b230-128">다음 예제는 hello에서 hello 서비스 보안 주체 ID에서에서 공급 되는 명령 앞 hello:</span><span class="sxs-lookup"><span data-stu-id="4b230-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="4b230-129">[az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들고 5GB 데이터 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="4b230-130">특정 Marketplace 이미지만 디스크 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="4b230-131">hello 다음 예제에서는 V `myVM` 를 사용 하는 **CentOS 7.2n** 이미지:</span><span class="sxs-lookup"><span data-stu-id="4b230-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="4b230-132">SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello 출력의 hello 명령 앞에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="4b230-133">파티션 및 파일 시스템 만듭니다 다음 hello 데이터 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="4b230-134">자세한 내용은 참조 [tooa Linux VM toomount hello에 대 한 새 디스크를 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="4b230-135">SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-135">Close your SSH session.</span></span>

<span data-ttu-id="4b230-136">[az vm encryption enable](/cli/azure/vm/encryption#enable)을 사용하여 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="4b230-137">hello 다음 예제에서는 hello `$sp_id` 및 `$sp_password` hello 앞에서 변수 `ad sp create-for-rbac` 명령:</span><span class="sxs-lookup"><span data-stu-id="4b230-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="4b230-138">디스크 암호화 프로세스 toocomplete hello에 대 한 몇 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="4b230-139">사용 하 여 hello 프로세스의 hello 상태를 모니터링 [az vm 암호화 표시](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="4b230-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4b230-140">상태 표시 hello **EncryptionInProgress**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="4b230-141">Hello OS 디스크 보고서에 대 한 hello 상태가 될 때까지 대기 **VMRestartPending**, 다시 시작 된 VM [az vm 다시 시작](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="4b230-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4b230-142">hello 디스크 암호화 프로세스가 완료 된 hello 부팅 프로세스 중, 따라서 사용 하 여 다시 암호화의 hello 상태를 확인 하기 전에 잠시 기다린 후 **az vm 암호화 표시**:</span><span class="sxs-lookup"><span data-stu-id="4b230-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4b230-143">hello 운영 체제 디스크와 같은 데이터 디스크를 모두 hello 상태를 보고 이제 해야 **암호화**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="4b230-144">디스크 암호화 개요</span><span class="sxs-lookup"><span data-stu-id="4b230-144">Overview of disk encryption</span></span>
<span data-ttu-id="4b230-145">Linux VM의 가상 디스크는 미사용 시 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt)를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="4b230-146">Azure에서 가상 디스크 암호화는 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="4b230-147">암호화 키가 소프트웨어 보호를 사용 하 여 Azure 키 자격 증명 모음에 저장 하거나 가져오거나 140-2 수준 2 표준 tooFIPS 인증 된 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="4b230-148">이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="4b230-149">이러한 암호화 한 키를 사용 하는 tooencrypt 가상 디스크 연결 된 tooyour VM의 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="4b230-150">Azure Active Directory 서비스 사용자는 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="4b230-151">VM을 암호화 하기 위한 hello 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="4b230-152">Azure Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="4b230-153">암호화 키 toobe hello 디스크를 암호화 하는 데 사용할 수 있는 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="4b230-154">hello Azure 키 자격 증명 모음에서에서 tooread hello 암호화 키 hello 적절 한 권한이 있는 사용자는 Azure Active Directory 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="4b230-155">Hello 명령 tooencrypt hello Azure Active Directory 서비스 사용자 및 사용 되는 적절 한 암호화 키 toobe 지정 하 여 가상 디스크를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="4b230-156">hello Azure Active Directory 서비스 보안 주체 요청 hello Azure 키 자격 증명 모음에서 필요한 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="4b230-157">hello 가상 디스크는 암호화 키를 제공 하는 hello를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="4b230-158">암호화 프로세스</span><span class="sxs-lookup"><span data-stu-id="4b230-158">Encryption process</span></span>
<span data-ttu-id="4b230-159">다음과 같은 추가 구성 요소가 hello 디스크 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="4b230-160">**Azure 키 자격 증명 모음** -toosafeguard 암호화 키 및 hello 디스크 암호화/암호 해독 프로세스에 사용 되는 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="4b230-161">이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="4b230-162">없는 toodedicate 주요 자격 증명 모음 tooencrypting 디스크.</span><span class="sxs-lookup"><span data-stu-id="4b230-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="4b230-163">tooseparate 관리 범위 및 키 가시성 전용된 키 자격 증명 모음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="4b230-164">**Azure Active Directory** -핸들 hello 필요한 암호화 키의 보안 교환 및 인증에 대 한 작업을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="4b230-165">일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="4b230-166">hello 서비스 사용자는 보안 메커니즘 toorequest 제공 하 고 hello 적절 한 암호화 키를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="4b230-167">Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="4b230-168">요구 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="4b230-168">Requirements and limitations</span></span>
<span data-ttu-id="4b230-169">디스크 암호화에 대해 지원되는 시나리오 및 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="4b230-170">Linux 서버 Sku-Ubuntu, CentOS, SUSE 및 SUSE Linux Enterprise Server (SLES), 및 Red Hat Enterprise Linux 다음 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="4b230-171">모든 리소스 (예: 키 자격 증명 모음, 저장소 계정 및 VM) hello에 있어야 합니다. 같은 Azure 지역 및 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="4b230-172">표준 A, D, DS, G 및 GS 시리즈 VM.</span><span class="sxs-lookup"><span data-stu-id="4b230-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="4b230-173">디스크 암호화 hello 다음 시나리오에서에서 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="4b230-174">기본 계층 VM.</span><span class="sxs-lookup"><span data-stu-id="4b230-174">Basic tier VMs.</span></span>
* <span data-ttu-id="4b230-175">Hello 클래식 배포 모델을 사용 하 여 만든 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="4b230-176">Linux VM에서 OS 디스크 암호화 비활성화.</span><span class="sxs-lookup"><span data-stu-id="4b230-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="4b230-177">Hello 이미 암호화 된 Linux VM에서 암호화 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="4b230-178">Azure Key Vault 및 키 만들기</span><span class="sxs-lookup"><span data-stu-id="4b230-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="4b230-179">최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="4b230-180">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4b230-181">예제 매개 변수 이름에는 *myResourceGroup*, *myKey*, *myVM*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="4b230-182">hello 첫 번째 단계는 Azure 키 자격 증명 모음 toostore toocreate 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="4b230-183">Azure 주요 자격 증명, 비밀 키를 저장할 수 있습니다 또는 암호 toosecurely를 허용 하는 응용 프로그램 및 서비스에 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="4b230-184">가상 디스크 암호화에 대 한 주요 자격 증명 모음 toostore tooencrypt 사용된 되는 암호화 키를 사용 하거나 가상 디스크의 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="4b230-185">Hello Azure 키 자격 증명 모음 공급자와 Azure 구독 내에서 사용 하도록 설정 [az 리소스 공급자 등록](/cli/azure/provider#register) 리소스 그룹을 만들고 [az 그룹 만들기](/cli/azure/group#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4b230-186">hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 *myResourceGroup* hello에 `eastus` 위치:</span><span class="sxs-lookup"><span data-stu-id="4b230-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4b230-187">hello Azure 키 자격 증명 모음 포함 hello 암호화 키와 연결 된 계산 hello VM 자체 저장소 같은 리소스에 있어야 합니다. 동일한 지역을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="4b230-188">Azure 키 자격 증명 모음 만들기와 [az keyvault 만들](/cli/azure/keyvault#create) 디스크 암호화와 함께 사용 하기 위해 주요 자격 증명 모음 hello를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="4b230-189">*keyvault_name*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="4b230-190">소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="4b230-191">HSM을 사용하려면 프리미엄 Key Vault가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="4b230-192">소프트웨어 보호 키를 저장 하는 표준 주요 자격 증명 모음 보다는 주요 자격 증명 모음 프리미엄은 추가 비용 toocreating 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="4b230-193">hello 앞 단계에서에서 프리미엄 주요 자격 증명 추가 toocreate `--sku Premium` toohello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="4b230-194">hello 다음 예제에서는 소프트웨어 보호 키 이후 표준 주요 자격 증명 모음을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="4b230-195">두 보호 모델에 대 한 hello Azure 플랫폼 toobe hello VM toodecrypt hello 가상 디스크를 부팅 될 때 액세스 toorequest hello에 대 한 암호화 키에 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="4b230-196">[az keyvault key create](/cli/azure/keyvault/key#create)를 사용하여 Key Vault에 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="4b230-197">hello 다음 예제에서는 라는 키 *myKey*:</span><span class="sxs-lookup"><span data-stu-id="4b230-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="4b230-198">Hello Azure Active Directory 서비스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4b230-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="4b230-199">가상 디스크를 암호화 하거나 암호를 해독할 때 계정 toohandle hello 인증 및 자격 증명 모음 키에서에서 암호화 키의 교환 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="4b230-200">이 계정에는 Azure Active Directory 서비스 사용자 hello Azure 플랫폼 toorequest hello VM hello 대신 하 여 적절 한 암호화 키를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="4b230-201">기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="4b230-202">[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)에서 Azure Active Directory를 사용하여 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="4b230-203">다음 예제는 hello Id와 암호 이후 명령에서 사용 하도록 hello 서비스 사용자에 대 한 hello 값 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="4b230-204">hello 암호 hello 서비스 보안 주체를 만들 때에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="4b230-205">뷰와 레코드 hello 암호 필요 (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="4b230-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="4b230-206">[az ad sp list](/cli/azure/ad/sp#list)를 사용하여 서비스 사용자를 나열하고 [az ad sp show](/cli/azure/ad/sp#show)를 사용하여 특정 서비스 사용자에 대한 추가 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="4b230-207">toosuccessfully 암호화 또는 가상 디스크를 암호 해독, 키 자격 증명 모음에 저장 된 hello 암호화 키에 대 한 권한 집합 toopermit hello Azure Active Directory 서비스 보안 주체 tooread hello 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="4b230-208">[az keyvault set-policy](/cli/azure/keyvault#set-policy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="4b230-209">다음 예제는 hello에서 hello 서비스 보안 주체 ID에서에서 공급 되는 명령 앞 hello:</span><span class="sxs-lookup"><span data-stu-id="4b230-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="4b230-210">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="4b230-210">Create virtual machine</span></span>
<span data-ttu-id="4b230-211">tooactually 일부 가상 디스크가 암호화, VM을 만들고 데이터 디스크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="4b230-212">만들기와 VM tooencrypt [az vm 만들기](/cli/azure/vm#create) 5gb 데이터 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="4b230-213">특정 Marketplace 이미지만 디스크 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="4b230-214">hello 다음 예제에서는 V *myVM* 를 사용 하는 **CentOS 7.2n** 이미지:</span><span class="sxs-lookup"><span data-stu-id="4b230-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="4b230-215">SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello 출력의 hello 명령 앞에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="4b230-216">파티션 및 파일 시스템 만듭니다 다음 hello 데이터 디스크를 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="4b230-217">자세한 내용은 참조 [tooa Linux VM toomount hello에 대 한 새 디스크를 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="4b230-218">SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="4b230-219">가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="4b230-219">Encrypt virtual machine</span></span>
<span data-ttu-id="4b230-220">tooencrypt hello 가상 디스크를 모아 놓은 모든 hello 이전 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="4b230-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="4b230-221">Hello Azure Active Directory 서비스 사용자 및 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="4b230-222">Hello 주요 자격 증명 모음 toostore hello 메타 데이터에 대 한 암호화 된 디스크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="4b230-223">Hello 실제 암호화 및 암호 해독에 대 한 암호화 키 toouse hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="4b230-224">Tooencrypt hello OS 디스크, hello 데이터 디스크 또는 모두 사용할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="4b230-225">[az vm encryption enable](/cli/azure/vm/encryption#enable)을 사용하여 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="4b230-226">hello 다음 예제에서는 hello `$sp_id` 및 `$sp_password` hello 앞에서 변수 `ad sp create-for-rbac` 명령:</span><span class="sxs-lookup"><span data-stu-id="4b230-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="4b230-227">디스크 암호화 프로세스 toocomplete hello에 대 한 몇 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="4b230-228">사용 하 여 hello 프로세스의 hello 상태를 모니터링 [az vm 암호화 표시](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="4b230-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4b230-229">hello는 비슷한 toohello 다음 잘린된 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="4b230-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="4b230-230">Hello OS 디스크 보고서에 대 한 hello 상태가 될 때까지 대기 **VMRestartPending**, 다시 시작 된 VM [az vm 다시 시작](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="4b230-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4b230-231">hello 디스크 암호화 프로세스가 완료 된 hello 부팅 프로세스 중, 따라서 사용 하 여 다시 암호화의 hello 상태를 확인 하기 전에 잠시 기다린 후 **az vm 암호화 표시**:</span><span class="sxs-lookup"><span data-stu-id="4b230-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4b230-232">hello 운영 체제 디스크와 같은 데이터 디스크를 모두 hello 상태를 보고 이제 해야 **암호화**합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="4b230-233">데이터 디스크 더 추가하기</span><span class="sxs-lookup"><span data-stu-id="4b230-233">Add additional data disks</span></span>
<span data-ttu-id="4b230-234">데이터 디스크를 암호화 한 후 나중에 추가로 가상 디스크 tooyour VM을 추가할 수 있으며도 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="4b230-235">예를 들어 다음과 같이 두 번째 가상 디스크 tooyour VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="4b230-236">다시 hello 명령 tooencrypt hello 가상 디스크를 다음과 같이 실행:</span><span class="sxs-lookup"><span data-stu-id="4b230-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="4b230-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b230-237">Next steps</span></span>
* <span data-ttu-id="4b230-238">암호화 키 및 Key Vault 삭제를 비롯한 Azure Key Vault 관리에 대한 자세한 내용은 [CLI를 사용하여 Key Vault 관리](../../key-vault/key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b230-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="4b230-239">암호화 된 사용자 지정 VM tooupload tooAzure를 준비 하 고 같은 디스크 암호화에 대 한 자세한 내용은 참조 하십시오. [Azure 디스크 암호화](../../security/azure-security-disk-encryption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b230-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
