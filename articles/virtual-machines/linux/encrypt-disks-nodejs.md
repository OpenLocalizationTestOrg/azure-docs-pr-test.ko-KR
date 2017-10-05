---
title: "Azure CLI 1.0을 사용하여 Linux VM에서 디스크 암호화 | Microsoft Docs"
description: "Azure CLI 1.0 및 Resource Manager 배포 모델을 사용하여 Linux VM에서 디스크를 암호화하는 방법"
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
ms.openlocfilehash: b436f2d43c41000f4385889edb3fa3983d4a8c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="b078f-103">Azure CLI 1.0을 사용하여 Linux VM에서 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="b078f-103">Encrypt disks on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="b078f-104">가상 컴퓨터(VM)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 미사용 시 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="b078f-105">디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="b078f-106">이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="b078f-107">이 문서는 Azure CLI 1.0 및 Resource Manager 배포 모델을 사용하여 Linux VM에서 가상 디스크를 암호화하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="b078f-108">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="b078f-108">CLI versions to complete the task</span></span>
<span data-ttu-id="b078f-109">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="b078f-110">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="b078f-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b078f-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="b078f-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="b078f-112">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="b078f-112">Quick commands</span></span>
<span data-ttu-id="b078f-113">작업을 빠르게 완료해야 하는 경우 다음 섹션에서 VM에서 가상 디스크를 암호화하는 기본 명령에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b078f-113">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="b078f-114">각 단계에 대한 보다 자세한 내용 및 상황 설명은 [여기서부터](#overview-of-disk-encryption) 문서 끝까지 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b078f-114">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="b078f-115">[최신 Azure CLI 1.0](../../xplat-cli-install.md)이 설치되어 있고 다음과 같이 Resource Manager 모드를 사용하여 로그인되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-115">You need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="b078f-116">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-116">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b078f-117">예제 매개 변수 이름에 `myResourceGroup`, `myKeyVault` 및 `myVM`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="b078f-118">먼저 Azure 구독 내에서 Azure Key Vault 공급자를 사용하도록 설정하고 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-118">First, enable the Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="b078f-119">다음 예제는 `WestUS` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-119">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="b078f-120">Azure Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="b078f-121">다음 예제에서는`myKeyVault`라는 Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-121">The following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="b078f-122">Key Vault에 암호화 키를 만들고 디스크 암호화에 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="b078f-123">다음 예제는 `myKey`라는 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-123">The following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="b078f-124">Key Vault의 암호화 키를 교환하고 인증을 처리하기 위해 Azure Active Directory를 사용하여 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-124">Create an endpoint using Azure Active Directory for handling the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="b078f-125">`--home-page` 및 `--identifier-uris`에는 실제 라우팅이 가능한 주소를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-125">The `--home-page` and `--identifier-uris` do not need to be actual routable address.</span></span> <span data-ttu-id="b078f-126">최고 수준의 보안을 위해 암호 대신 클라이언트 암호가 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-126">For the highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="b078f-127">Azure CLI는 현재 클라이언트 암호를 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-127">The Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="b078f-128">클라이언트 암호는 Azure Portal에서만 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-128">Client secrets can only be generated in the Azure portal.</span></span> <span data-ttu-id="b078f-129">다음 예제는 `myAADApp`이라는 Azure Active Directory 끝점을 만들고 `myPassword`라는 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-129">The following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="b078f-130">다음과 같이 사용자 고유의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="b078f-131">위 명령의 출력에 표시된 `applicationId`를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-131">Note the `applicationId` shown in the output from the preceding command.</span></span> <span data-ttu-id="b078f-132">이 응용 프로그램 ID가 다음 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-132">This application ID is used in the following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="b078f-133">데이터 디스크를 기존 VM에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-133">Add a data disk to an existing VM.</span></span> <span data-ttu-id="b078f-134">다음 예제는 데이터 디스크를 `myVM`이라는 VM에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-134">The following example adds a data disk to a VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="b078f-135">생성한 Key Vault 및 키의 세부 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-135">Review the details for your Key Vault and the key you created.</span></span> <span data-ttu-id="b078f-136">마지막 단계에서 Key Vault ID, URI 및 키 URL이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-136">You need the Key Vault ID, URI, and key URL in the final step.</span></span> <span data-ttu-id="b078f-137">다음 예제는 `myKeyVault`라는 Key Vault와 `myKey`라는 키의 세부 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-137">The following example reviews the details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="b078f-138">사용자 고유의 매개 변수 이름을 입력하여 다음과 같이 디스크를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="b078f-139">Azure CLI는 암호화 프로세스 중에 자세한 오류를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-139">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="b078f-140">추가적인 문제 해결 정보는 `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b078f-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="b078f-141">이전 명령에 변수가 많기 때문에 프로세스가 실패한 이유에 대한 정보가 확실치 않을 수 있습니다. 전체 명령 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-141">As the preceding command has many variables and you may not get much indication as to why the process fails, a complete command example would be as follows:</span></span>

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

<span data-ttu-id="b078f-142">마지막으로 암호화 상태를 다시 검토하여 이제 가상 디스크가 암호화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-142">Finally, review the encryption status again to confirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="b078f-143">다음 예제는 `myResourceGroup` 리소스 그룹의 `myVM`라는 VM의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-143">The following example checks the status of a VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="b078f-144">디스크 암호화 개요</span><span class="sxs-lookup"><span data-stu-id="b078f-144">Overview of disk encryption</span></span>
<span data-ttu-id="b078f-145">Linux VM의 가상 디스크는 미사용 시 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt)를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="b078f-146">Azure에서 가상 디스크 암호화는 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="b078f-147">암호화 키는 소프트웨어 보호를 사용하여 Azure Key Vault에 저장되거나 FIPS 140-2 레벨 2 표준 인증 HSM(하드웨어 보안 모듈)에서 키를 가져오거나 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="b078f-148">이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="b078f-149">이러한 암호화 키는 VM에 연결된 가상 디스크를 암호화하고 암호를 해독하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="b078f-150">Azure Active Directory 끝점은 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="b078f-151">VM을 암호화하는 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="b078f-152">Azure Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="b078f-153">암호화하는 디스크에 사용될 수 있도록 암호화 키를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="b078f-154">Azure Key Vault에서 암호화 키를 읽어오려면 적절한 사용 권한을 통해 Azure Active Directory를 사용하여 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-154">To read the cryptographic key from the Azure Key Vault, create an endpoint using Azure Active Directory with the appropriate permissions.</span></span>
4. <span data-ttu-id="b078f-155">가상 디스크를 암호화하도록 명령을 실행하고 사용될 Azure Active Directory 끝점과 적절한 암호화 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory endpoint and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="b078f-156">Azure Active Directory 끝점은 Azure Key Vault에 필요한 암호화 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-156">The Azure Active Directory endpoint requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="b078f-157">가상 디스크는 제공된 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="b078f-158">지원 서비스 및 암호화 프로세스</span><span class="sxs-lookup"><span data-stu-id="b078f-158">Supporting services and encryption process</span></span>
<span data-ttu-id="b078f-159">디스크 암호화는 다음과 같은 추가 구성 요소에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="b078f-160">**Azure Key Vault** - 디스크 암호화/암호 해독 프로세스를 위한 암호화 키와 암호를 안전하게 보호하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="b078f-161">이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="b078f-162">Key Vault를 디스크 암호화에 전적으로 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="b078f-163">관리 범위 및 키 표시 여부를 분리하기 위해 전용 Key Vault를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="b078f-164">**Azure Active Directory** - 필요한 암호화 키의 안전한 교환과 요청된 작업에 대한 인증을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="b078f-165">일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="b078f-166">응용 프로그램은 적절한 암호화 키를 요청하고 발급받기 위한 Virtual Machines 서비스 및 Key Vault의 끝점에 더 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-166">The application is more of an endpoint for the Key Vault and Virtual Machine services to request and get issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="b078f-167">Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="b078f-168">요구 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="b078f-168">Requirements and limitations</span></span>
<span data-ttu-id="b078f-169">디스크 암호화에 대해 지원되는 시나리오 및 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="b078f-170">다음 Linux Server SKU - Ubuntu, CentOS, SUSE 및 SLES(SUSE Linux Enterprise Server)와 Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="b078f-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="b078f-171">모든 리소스(예: Key Vault, 저장소 계정, VM)는 동일한 Azure 지역 및 구독 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="b078f-172">표준 A, D, DS, G 및 GS 시리즈 VM.</span><span class="sxs-lookup"><span data-stu-id="b078f-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="b078f-173">다음 시나리오의 경우 디스크 암호화가 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="b078f-174">기본 계층 VM.</span><span class="sxs-lookup"><span data-stu-id="b078f-174">Basic tier VMs.</span></span>
* <span data-ttu-id="b078f-175">클래식 배포 모델을 사용하여 만든 VM.</span><span class="sxs-lookup"><span data-stu-id="b078f-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="b078f-176">Linux VM에서 OS 디스크 암호화 비활성화.</span><span class="sxs-lookup"><span data-stu-id="b078f-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="b078f-177">이미 암호화된 Linux VM에서 암호화 키 업데이트.</span><span class="sxs-lookup"><span data-stu-id="b078f-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-the-azure-key-vault-and-keys"></a><span data-ttu-id="b078f-178">Azure Key Vault 및 키 만들기</span><span class="sxs-lookup"><span data-stu-id="b078f-178">Create the Azure Key Vault and keys</span></span>
<span data-ttu-id="b078f-179">이 가이드의 나머지 부분을 완료하려면 [최신 Azure CLI 1.0](../../xplat-cli-install.md)이 설치되어 있고 다음과 같이 Resource Manager 모드를 사용하여 로그인되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-179">To complete the remainder of this guide, you need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="b078f-180">명령 예제 전체에서 모든 예제 매개 변수를 사용자 고유의 이름, 위치, 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="b078f-181">다음 예제는 `myResourceGroup`, `myKeyVault`, `myAADApp` 등의 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="b078f-182">첫 번째 단계는 암호화 키를 저장할 Azure Key Vault를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="b078f-183">Azure Key Vault는 응용 프로그램 및 서비스에 안전하게 구현할 수 있는 키와 암호를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="b078f-184">가상 디스크 암호화의 경우 Key Vault를 사용하여 가상 디스크 암호화 또는 암호 해독에 사용되는 암호화 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="b078f-185">Azure 구독 내에서 Azure Key Vault 공급자를 사용하도록 설정한 후 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-185">Enable the Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="b078f-186">다음 예제에서는 `WestUS` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-186">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="b078f-187">암호화 키를 포함하는 Azure Key Vault와 저장소 및 VM과 같은 연결된 계산 리소스는 동일한 지역에 상주해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="b078f-188">다음 예제는 `myKeyVault`라는 Azure Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-188">The following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="b078f-189">소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="b078f-190">HSM을 사용하려면 프리미엄 Key Vault가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="b078f-191">소프트웨어 보호 키를 저장하는 표준 Key Vault가 아닌 프리미엄 Key Vault를 만들려면 추가 비용이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-191">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="b078f-192">프리미엄 Key Vault를 만들려면 앞의 단계에서 `--sku Premium`을 명령에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-192">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="b078f-193">표준 Key Vault를 만들었기 때문에 다음 예제는 소프트웨어 보호 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-193">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="b078f-194">두 가지 보호 모델 모두, 가상 디스크의 암호를 해독하기 위해 VM이 부팅될 때 암호화 키를 요청하려면 Azure 플랫폼에 액세스 권한이 허용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-194">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="b078f-195">Key Vault 내에서 암호화 키를 만든 후 가상 디스크 암호화에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="b078f-196">다음 예제는 `myKey`라는 키를 만든 후 이것을 디스크 암호화에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-196">The following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-the-azure-active-directory-application"></a><span data-ttu-id="b078f-197">Azure Active Directory 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b078f-197">Create the Azure Active Directory application</span></span>
<span data-ttu-id="b078f-198">가상 디스크가 암호화되거나 암호가 해독될 때 끝점을 사용하여 Key Vault의 암호화 키 교환 및 인증을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-198">When virtual disks are encrypted or decrypted, you use an endpoint to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="b078f-199">이 끝점 즉, Azure Active Directory 응용 프로그램은 Azure 플랫폼이 VM을 대신하여 적절한 암호화 키를 요청하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-199">This endpoint, an Azure Active Directory application, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="b078f-200">기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="b078f-201">전체 Azure Active Directory 응용 프로그램을 만드는 것이 아니므로 다음 예제의 `--home-page` 및 `--identifier-uris` 매개 변수에 실제 라우팅이 가능한 주소를 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-201">As you are not creating a full Azure Active Directory application, the `--home-page` and `--identifier-uris` parameters in the following example do not need to be actual routable address.</span></span> <span data-ttu-id="b078f-202">다음 예제는 Azure Portal 내에서 키를 생성하기 보다는 암호 기반 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-202">The following example also specifies a password-based secret rather than generating keys from within the Azure portal.</span></span> <span data-ttu-id="b078f-203">현재는 Azure CLI에서 키 생성을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-203">As this time, generating keys cannot be done from the Azure CLI.</span></span>

<span data-ttu-id="b078f-204">Azure Active Directory 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="b078f-205">다음 예제는 `myAADApp`이라는 응용 프로그램을 만들고 `myPassword`라는 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-205">The following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="b078f-206">다음과 같이 사용자 고유의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="b078f-207">앞의 명령에서 출력으로 반환된 `applicationId`를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-207">Make a note of the `applicationId` that is returned in the output from the preceding command.</span></span> <span data-ttu-id="b078f-208">이 응용 프로그램 ID는 일부 나머지 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-208">This application ID is used in some of the remaining steps.</span></span> <span data-ttu-id="b078f-209">다음으로, 환경 내에서 응용 프로그램에 액세스할 수 있도록 SPN(서비스 사용자 이름)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-209">Next, create a service principal name (SPN) so that the application is accessible within your environment.</span></span> <span data-ttu-id="b078f-210">가상 디스크를 암호화하거나 암호를 해독하려면, Key Vault에 저장되어 있는 암호화 키에 대한 권한이 Azure Active Directory 응용 프로그램이 키를 읽는 것을 허용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-210">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory application to read the keys.</span></span>

<span data-ttu-id="b078f-211">다음과 같이 SPN을 만들고 적절한 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-211">Create the SPN and set the appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="b078f-212">가상 디스크를 추가하고 암호화 상태를 검토</span><span class="sxs-lookup"><span data-stu-id="b078f-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="b078f-213">일부 가상 디스크를 실제로 암호화하기 위해 기존 VM에 디스크를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-213">To actually encrypt some virtual disks, lets add a disk to an existing VM.</span></span> <span data-ttu-id="b078f-214">다음과 같이 5GB 데이터 디스크를 기존 VM에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-214">Add a 5Gb data disk to an existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="b078f-215">가상 디스크는 현재 암호화되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-215">The virtual disks are not currently encrypted.</span></span> <span data-ttu-id="b078f-216">다음과 같이 VM의 현재 암호화 상태를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-216">Review the current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="b078f-217">가상 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="b078f-217">Encrypt virtual disks</span></span>
<span data-ttu-id="b078f-218">이제 가상 디스크를 암호화하기 위해서 이전의 구성 요소를 모두 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-218">To now encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="b078f-219">Azure Active Directory 응용 프로그램 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-219">Specify the Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="b078f-220">암호화된 디스크에 대한 메타데이터를 저장할 Key Vault를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-220">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="b078f-221">실제 암호화 및 암호 해독에 사용될 암호화 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-221">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="b078f-222">OS 디스크, 데이터 디스크 또는 모든 디스크를 암호화할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-222">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="b078f-223">Key Vault ID, URI 및 마지막 단계에서 키 URL이 필요하므로 생성한 키 및 Azure Key Vault에 대한 세부 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-223">Lets review the details for your Azure Key Vault and the key you created, as you need the Key Vault ID, URI, and then key URL in the final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="b078f-224">다음과 같이 `azure keyvault show` 및 `azure keyvault key show` 명령의 출력을 사용하여 가상 디스크를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-224">Encrypt your virtual disks using the output from the `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="b078f-225">앞의 명령에 변수가 많으므로 다음 예제에서 전체 명령을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-225">As the preceding command has many variables, the following example is the complete command for reference:</span></span>

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

<span data-ttu-id="b078f-226">Azure CLI는 암호화 프로세스 중에 자세한 오류를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-226">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="b078f-227">추가적인 문제 해결 정보는 암호화하는 VM의 `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="b078f-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on the VM you are encrypting.</span></span>

<span data-ttu-id="b078f-228">마지막으로 암호화 상태를 다시 검토하여 이제 가상 디스크가 암호화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-228">Finally, lets review the encryption status again to confirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="b078f-229">데이터 디스크 더 추가하기</span><span class="sxs-lookup"><span data-stu-id="b078f-229">Add additional data disks</span></span>
<span data-ttu-id="b078f-230">데이터 디스크를 암호화하고 나면 나중에 VM에 가상 디스크를 더 추가하고 암호화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-230">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="b078f-231">`azure vm enable-disk-encryption` 명령을 실행할 때 `--sequence-version` 매개 변수를 사용하여 시퀀스 버전을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-231">When you run the `azure vm enable-disk-encryption` command, increment the sequence version using the `--sequence-version` parameter.</span></span> <span data-ttu-id="b078f-232">이 시퀀스 버전 매개 변수를 사용하면 동일한 VM에서 반복 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-232">This sequence version parameter allows you to perform repeated operations on the same VM.</span></span>

<span data-ttu-id="b078f-233">예를 들어 다음과 같이 VM에 두 번째 가상 디스크를 추가해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-233">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="b078f-234">명령을 다시 실행하여 가상 디스크를 암호화 하고, 이번에는 `--sequence-version` 매개 변수를 추가하여, 다음과 같이 첫 번째 실행의 값을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b078f-234">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="b078f-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b078f-235">Next steps</span></span>
* <span data-ttu-id="b078f-236">암호화 키 및 Key Vault 삭제를 비롯한 Azure Key Vault 관리에 대한 자세한 내용은 [CLI를 사용하여 Key Vault 관리](../../key-vault/key-vault-manage-with-cli2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b078f-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="b078f-237">Azure에 업로드할 암호화된 사용자 지정 VM 준비와 같은 디스크 암호화에 대한 자세한 내용은 [Azure Disk Encryption](../../security/azure-security-disk-encryption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b078f-237">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
