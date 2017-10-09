---
title: "hello Azure CLI 1.0을 사용 하 여 Linux VM에서 aaaEncrypt 디스크 | Microsoft Docs"
description: "Tooencrypt 디스크를 사용 하 여 Linux VM에 Azure CLI 1.0 및 hello 리소스 관리자 배포 모델을 hello 하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="48632-103">Hello Azure CLI 1.0을 사용 하 여 Linux VM에서 디스크를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="48632-104">가상 컴퓨터(VM)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 미사용 시 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="48632-105">디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="48632-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="48632-106">이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="48632-107">이 문서 tooencrypt 가상 디스크를 사용 하 여 Linux VM에 Azure CLI 1.0 및 hello 리소스 관리자 배포 모델을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="48632-108">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="48632-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="48632-109">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="48632-110">[Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="48632-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="48632-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="48632-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="48632-112">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="48632-112">Quick commands</span></span>
<span data-ttu-id="48632-113">Hello 작업을 수행 tooquickly 해야 할 경우에 다음 섹션의 세부 정보 hello 기본 hello tooencrypt 가상 디스크를 VM에 명령, 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="48632-114">각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](#overview-of-disk-encryption)합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="48632-115">Hello 필요한 [최신 Azure CLI 1.0](../../xplat-cli-install.md) 설치 하 고 다음과 같이 hello Resource Manager 모드를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="48632-116">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="48632-117">예제 매개 변수 이름에 `myResourceGroup`, `myKeyVault` 및 `myVM`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="48632-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="48632-118">먼저, Azure 구독 내 hello Azure 키 자격 증명 모음 공급자를 사용 하도록 설정 하 고 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48632-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="48632-119">hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 `myResourceGroup` hello에 `WestUS` 위치:</span><span class="sxs-lookup"><span data-stu-id="48632-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="48632-120">Azure Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48632-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="48632-121">hello 다음 예제에서는 키 자격 증명 모음 이름이 `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="48632-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="48632-122">Key Vault에 암호화 키를 만들고 디스크 암호화에 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="48632-123">hello 다음 예제에서는 라는 키 `myKey`:</span><span class="sxs-lookup"><span data-stu-id="48632-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="48632-124">Azure Active Directory를 사용 하 여 hello 인증을 처리 하 고 주요 자격 증명 모음에서 암호화 키를 교환 하 고 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48632-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="48632-125">hello `--home-page` 및 `--identifier-uris` toobe 실제 라우팅할 수 있는 주소가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="48632-126">Hello 가장 높은 수준의 보안을 위해 암호 대신 클라이언트 암호를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="48632-127">hello Azure CLI 클라이언트 암호를 현재 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="48632-128">클라이언트 암호 hello Azure 포털에에서만 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="48632-129">hello 다음 예제에서는 끝점을 만들고 Azure Active Directory 라는 `myAADApp` 의 암호를 사용 하 여 `myPassword`합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="48632-130">다음과 같이 사용자 고유의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="48632-131">참고 hello `applicationId` hello 명령 앞의 hello 출력에 표시 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="48632-132">이 응용 프로그램 ID는 단계를 수행 하는 hello에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48632-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="48632-133">기존 VM 데이터 디스크 tooan를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="48632-134">hello 다음 예제에서는 추가 데이터 디스크 tooa 라는 VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="48632-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="48632-135">만든 키 자격 증명 모음과 hello 키에 대해 hello 세부 정보를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="48632-136">키 자격 증명 모음 ID, URI 및 키 hello 필요 hello 마지막 단계에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="48632-137">hello 다음 예제에서는 검토 hello 세부 정보 라는 키 자격 증명 모음에 대 한 `myKeyVault` 및 라는 키 `myKey`:</span><span class="sxs-lookup"><span data-stu-id="48632-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="48632-138">사용자 고유의 매개 변수 이름을 입력하여 다음과 같이 디스크를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="48632-139">hello Azure CLI hello 암호화 프로세스 동안 자세한 오류가 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="48632-140">추가적인 문제 해결 정보는 `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48632-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="48632-141">에 여러 변수를 명령 앞으로 hello 및 많은 표시 as toowhy hello 프로세스 실패를 얻지 못할 수도 있습니다, 전체 명령 예는 다음과 같은 것:</span><span class="sxs-lookup"><span data-stu-id="48632-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="48632-142">Hello 암호화 상태를 검토 하는 마지막으로, 가상 디스크 암호화 이제 tooconfirm 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="48632-143">hello 다음 예제에서는 상태를 검사 hello 라는 VM의 `myVM` hello에 `myResourceGroup` 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="48632-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="48632-144">디스크 암호화 개요</span><span class="sxs-lookup"><span data-stu-id="48632-144">Overview of disk encryption</span></span>
<span data-ttu-id="48632-145">Linux VM의 가상 디스크는 미사용 시 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt)를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="48632-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="48632-146">Azure에서 가상 디스크 암호화는 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="48632-147">암호화 키가 소프트웨어 보호를 사용 하 여 Azure 키 자격 증명 모음에 저장 하거나 가져오거나 140-2 수준 2 표준 tooFIPS 인증 된 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="48632-148">이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="48632-149">이러한 암호화 한 키를 사용 하는 tooencrypt 가상 디스크 연결 된 tooyour VM의 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="48632-150">Azure Active Directory 끝점은 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="48632-151">VM을 암호화 하기 위한 hello 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="48632-152">Azure Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48632-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="48632-153">암호화 키 toobe hello 디스크를 암호화 하는 데 사용할 수 있는 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="48632-154">hello Azure 키 자격 증명 모음에서에서 tooread hello 암호화 키 hello 적절 한 권한이 있는 Azure Active Directory를 사용 하 여 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48632-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="48632-155">Hello 명령 tooencrypt hello Azure Active Directory 끝점 및 적절 한 암호화 키 toobe 사용을 지정 하 여 가상 디스크를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="48632-156">Azure Active Directory 끝점 hello Azure 키 자격 증명 모음에서 hello 필요한 암호화 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="48632-157">hello 가상 디스크는 암호화 키를 제공 하는 hello를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48632-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="48632-158">지원 서비스 및 암호화 프로세스</span><span class="sxs-lookup"><span data-stu-id="48632-158">Supporting services and encryption process</span></span>
<span data-ttu-id="48632-159">다음과 같은 추가 구성 요소가 hello 디스크 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="48632-160">**Azure 키 자격 증명 모음** -toosafeguard 암호화 키 및 hello 디스크 암호화/암호 해독 프로세스에 사용 되는 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="48632-161">이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="48632-162">없는 toodedicate 주요 자격 증명 모음 tooencrypting 디스크.</span><span class="sxs-lookup"><span data-stu-id="48632-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="48632-163">tooseparate 관리 범위 및 키 가시성 전용된 키 자격 증명 모음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="48632-164">**Azure Active Directory** -핸들 hello 필요한 암호화 키의 보안 교환 및 인증에 대 한 작업을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="48632-165">일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="48632-166">hello 응용 프로그램이 이상의 hello 주요 자격 증명 모음에 대 한 끝점 및 가상 컴퓨터 서비스 toorequest 및 get hello 적절 한 암호화 키를 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="48632-167">Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="48632-168">요구 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="48632-168">Requirements and limitations</span></span>
<span data-ttu-id="48632-169">디스크 암호화에 대해 지원되는 시나리오 및 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="48632-170">Linux 서버 Sku-Ubuntu, CentOS, SUSE 및 SUSE Linux Enterprise Server (SLES), 및 Red Hat Enterprise Linux 다음 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="48632-171">모든 리소스 (예: 키 자격 증명 모음, 저장소 계정 및 VM) hello에 있어야 합니다. 같은 Azure 지역 및 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="48632-172">표준 A, D, DS, G 및 GS 시리즈 VM.</span><span class="sxs-lookup"><span data-stu-id="48632-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="48632-173">디스크 암호화 hello 다음 시나리오에서에서 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="48632-174">기본 계층 VM.</span><span class="sxs-lookup"><span data-stu-id="48632-174">Basic tier VMs.</span></span>
* <span data-ttu-id="48632-175">Hello 클래식 배포 모델을 사용 하 여 만든 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="48632-176">Linux VM에서 OS 디스크 암호화 비활성화.</span><span class="sxs-lookup"><span data-stu-id="48632-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="48632-177">Hello 이미 암호화 된 Linux VM에서 암호화 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="48632-178">만들 hello Azure 키 자격 증명 모음 및 키</span><span class="sxs-lookup"><span data-stu-id="48632-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="48632-179">hello 해야 toocomplete hello이이 가이드의 나머지 부분을 [최신 Azure CLI 1.0](../../xplat-cli-install.md) 설치 하 고 다음과 같이 hello Resource Manager 모드를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="48632-180">Hello 명령 예에서는 전체에서 고유한 이름, 위치 및 키 값으로 모든 예제에서는 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="48632-181">hello 다음 예에서는 사용의 규칙 `myResourceGroup`, `myKeyVault`, `myAADApp`등입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="48632-182">hello 첫 번째 단계는 Azure 키 자격 증명 모음 toostore toocreate 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="48632-183">Azure 주요 자격 증명, 비밀 키를 저장할 수 있습니다 또는 암호 toosecurely를 허용 하는 응용 프로그램 및 서비스에 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="48632-184">가상 디스크 암호화에 대 한 주요 자격 증명 모음 toostore tooencrypt 사용된 되는 암호화 키를 사용 하거나 가상 디스크의 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="48632-185">Azure 구독에서 hello Azure 키 자격 증명 모음 공급자 사용 후 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48632-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="48632-186">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `WestUS` 위치:</span><span class="sxs-lookup"><span data-stu-id="48632-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="48632-187">hello Azure 키 자격 증명 모음 포함 hello 암호화 키와 연결 된 계산 hello VM 자체 저장소 같은 리소스에 있어야 합니다. 동일한 지역을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="48632-188">hello 다음 만드는 예제는 Azure 키 자격 증명 모음 이름이 `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="48632-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="48632-189">소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="48632-190">HSM을 사용하려면 프리미엄 Key Vault가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="48632-191">소프트웨어 보호 키를 저장 하는 표준 주요 자격 증명 모음 보다는 주요 자격 증명 모음 프리미엄은 추가 비용 toocreating 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="48632-192">hello 앞 단계에서에서 프리미엄 주요 자격 증명 추가 toocreate `--sku Premium` toohello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="48632-193">hello 다음 예제에서는 소프트웨어 보호 키 이후 표준 주요 자격 증명 모음을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="48632-194">두 보호 모델에 대 한 hello Azure 플랫폼 toobe hello VM toodecrypt hello 가상 디스크를 부팅 될 때 액세스 toorequest hello에 대 한 암호화 키에 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="48632-195">Key Vault 내에서 암호화 키를 만든 후 가상 디스크 암호화에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="48632-196">hello 다음 예제에서는 라는 키 `myKey` 다음 디스크 암호화를 사용 하도록 설정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="48632-197">Hello Azure Active Directory 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="48632-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="48632-198">가상 디스크를 암호화 하거나 암호를 해독할 때 toohandle hello 인증 끝점 및 키 자격 증명 모음에서 암호화 키의 교환 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="48632-199">이 끝점으로 Azure Active Directory 응용 프로그램 hello Azure 플랫폼 toorequest hello VM hello 대신 하 여 적절 한 암호화 키를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="48632-200">기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="48632-201">전체 Azure Active Directory 응용 프로그램을 만들지 않고 대로 hello `--home-page` 및 `--identifier-uris` hello 다음 예제에서에서 매개 변수 toobe 실제 라우팅할 수 있는 주소가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="48632-202">hello 다음 예제에서는 또한 암호 기반 보안 대신 지정 hello Azure 포털 내에서 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="48632-203">이 시간으로 Azure CLI hello에서 키 생성을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="48632-204">Azure Active Directory 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48632-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="48632-205">hello 다음 예제에서는 응용 프로그램을 만듭니다 라는 `myAADApp` 의 암호를 사용 하 여 `myPassword`합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="48632-206">다음과 같이 사용자 고유의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="48632-207">Hello 메모 `applicationId` hello 명령 앞에서 hello 출력에 반환 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="48632-208">이 응용 프로그램 ID는 hello 나머지 단계 중 일부에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48632-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="48632-209">다음으로 hello 응용 프로그램은 사용자 환경 내에서 액세스할 수 있도록 서비스 사용자 이름 (SPN)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48632-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="48632-210">toosuccessfully 암호화 또는 가상 디스크를 암호 해독, 키 자격 증명 모음에 저장 된 hello 암호화 키에 대 한 권한 집합 toopermit hello Azure Active Directory 응용 프로그램 tooread hello 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="48632-211">Hello SPN 만들고 hello 적절 한 권한을 다음과 같이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="48632-212">가상 디스크를 추가하고 암호화 상태를 검토</span><span class="sxs-lookup"><span data-stu-id="48632-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="48632-213">tooactually 일부 가상 디스크가 암호화, 기존 VM 디스크 tooan를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="48632-214">VM을 다음과 같이 기존는 5gb 데이터 디스크 tooan를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="48632-215">가상 디스크 hello 현재 암호화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="48632-216">다음과 같이 VM의 hello 현재 암호화 상태를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="48632-217">가상 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="48632-217">Encrypt virtual disks</span></span>
<span data-ttu-id="48632-218">toonow hello 가상 디스크를 암호화, 모든 hello 이전 구성 요소로 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="48632-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="48632-219">Hello Azure Active Directory 응용 프로그램 및 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="48632-220">Hello 주요 자격 증명 모음 toostore hello 메타 데이터에 대 한 암호화 된 디스크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="48632-221">Hello 실제 암호화 및 암호 해독에 대 한 암호화 키 toouse hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="48632-222">Tooencrypt hello OS 디스크, hello 데이터 디스크 또는 모두 사용할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="48632-223">다음 hello 최종 단계에서 URL을 키 및 키 자격 증명 모음 ID, URI, hello 필요한 대로 만든 사용자의 Azure 키 자격 증명 모음과 hello 키에 대 한 hello 세부 정보를 검토 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="48632-224">Hello hello 출력을 사용 하 여 가상 디스크를 암호화 `azure keyvault show` 및 `azure keyvault key show` 다음과 같이 명령:</span><span class="sxs-lookup"><span data-stu-id="48632-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="48632-225">Hello 이전 명령에 여러 변수가, hello 다음 예제는 hello 전체 명령 참조에 대 한.</span><span class="sxs-lookup"><span data-stu-id="48632-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="48632-226">hello Azure CLI hello 암호화 프로세스 동안 자세한 오류가 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="48632-227">추가 문제 해결 정보를 검토 `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` hello 암호화 하는 VM에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="48632-228">마지막으로, hello 암호화 상태를 검토를 통해 가상 디스크 암호화 이제 tooconfirm 다시:</span><span class="sxs-lookup"><span data-stu-id="48632-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="48632-229">데이터 디스크 더 추가하기</span><span class="sxs-lookup"><span data-stu-id="48632-229">Add additional data disks</span></span>
<span data-ttu-id="48632-230">데이터 디스크를 암호화 한 후 나중에 추가로 가상 디스크 tooyour VM을 추가할 수 있으며도 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="48632-231">Hello를 실행 하는 경우 `azure vm enable-disk-encryption` 명령, hello를 사용 하 여 hello 시퀀스 버전 증가 `--sequence-version` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="48632-232">이 시퀀스 버전 매개 변수 있습니다 tooperform에서 반복된 하 여 연산 hello 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="48632-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="48632-233">예를 들어 다음과 같이 두 번째 가상 디스크 tooyour VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48632-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="48632-234">Hello 추가이 이번 hello 명령 tooencrypt hello 가상 디스크를 다시 실행 `--sequence-version` 매개 변수 및 증분 hello 값 첫에서 다음과 같이 실행:</span><span class="sxs-lookup"><span data-stu-id="48632-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="48632-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="48632-235">Next steps</span></span>
* <span data-ttu-id="48632-236">암호화 키 및 Key Vault 삭제를 비롯한 Azure Key Vault 관리에 대한 자세한 내용은 [CLI를 사용하여 Key Vault 관리](../../key-vault/key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48632-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="48632-237">암호화 된 사용자 지정 VM tooupload tooAzure를 준비 하 고 같은 디스크 암호화에 대 한 자세한 내용은 참조 하십시오. [Azure 디스크 암호화](../../security/azure-security-disk-encryption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="48632-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
