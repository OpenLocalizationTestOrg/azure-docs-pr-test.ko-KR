---
title: "Azure에서 Windows VM의 디스크 암호화 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 보안 강화를 위해 Windows VM에서 가상 디스크를 암호화하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 98b42b252a601af090579e3939f3c7ab91c3803b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="65b15-103">Windows VM에서 가상 디스크를 암호화하는 방법</span><span class="sxs-lookup"><span data-stu-id="65b15-103">How to encrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="65b15-104">VM(가상 컴퓨터)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="65b15-105">디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="65b15-106">이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="65b15-107">이 문서에서는 Azure PowerShell을 사용하여 Windows VM에서 가상 디스크를 암호화하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-107">This article details how to encrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="65b15-108">[Azure CLI 2.0을 사용하여 Linux VM을 암호화](../linux/encrypt-disks.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-108">You can also [encrypt a Linux VM using the Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="65b15-109">디스크 암호화 개요</span><span class="sxs-lookup"><span data-stu-id="65b15-109">Overview of disk encryption</span></span>
<span data-ttu-id="65b15-110">Windows VM의 가상 디스크는 미사용 시 Bitlocker를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="65b15-111">Azure에서 가상 디스크 암호화는 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="65b15-112">암호화 키는 소프트웨어 보호를 사용하여 Azure Key Vault에 저장되거나 FIPS 140-2 레벨 2 표준 인증 HSM(하드웨어 보안 모듈)에서 키를 가져오거나 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="65b15-113">이러한 암호화 키는 VM에 연결된 가상 디스크를 암호화하고 암호를 해독하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-113">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="65b15-114">이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="65b15-115">Azure Active Directory 서비스 사용자는 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="65b15-116">VM을 암호화하는 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-116">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="65b15-117">Azure Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="65b15-118">암호화하는 디스크에 사용될 수 있도록 암호화 키를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-118">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="65b15-119">Azure Key Vault에서 암호화 키를 읽어오려면 적절한 사용 권한을 통해 Azure Active Directory 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-119">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="65b15-120">가상 디스크를 암호화하도록 명령을 실행하고 사용될 Azure Active Directory 서비스 사용자와 적절한 암호화 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-120">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="65b15-121">Azure Active Directory 서비스 사용자는 Azure Key Vault에 필요한 암호화 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-121">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="65b15-122">가상 디스크는 제공된 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-122">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="65b15-123">암호화 프로세스</span><span class="sxs-lookup"><span data-stu-id="65b15-123">Encryption process</span></span>
<span data-ttu-id="65b15-124">디스크 암호화는 다음과 같은 추가 구성 요소에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-124">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="65b15-125">**Azure Key Vault** - 디스크 암호화/암호 해독 프로세스를 위한 암호화 키와 암호를 안전하게 보호하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-125">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="65b15-126">이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="65b15-127">Key Vault를 디스크 암호화에 전적으로 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-127">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="65b15-128">관리 범위 및 키 표시 여부를 분리하기 위해 전용 Key Vault를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-128">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="65b15-129">**Azure Active Directory** - 필요한 암호화 키의 안전한 교환과 요청된 작업에 대한 인증을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-129">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="65b15-130">일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="65b15-131">서비스 사용자는 해당 암호화 키를 요청하고 발급되도록 하는 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-131">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="65b15-132">Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="65b15-133">요구 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="65b15-133">Requirements and limitations</span></span>
<span data-ttu-id="65b15-134">디스크 암호화에 대해 지원되는 시나리오 및 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="65b15-135">Azure Marketplace 이미지 또는 사용자 지정 VHD 이미지에서 새 Windows VM에 대해 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="65b15-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="65b15-136">Azure에서 기존 Windows VM에 대해 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="65b15-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="65b15-137">저장소 공간을 사용하여 구성된 Windows VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="65b15-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="65b15-138">Windows VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="65b15-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="65b15-139">모든 리소스(예: Key Vault, 저장소 계정, VM)는 동일한 Azure 지역 및 구독 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-139">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="65b15-140">표준 계층 VM(예: A, D, DS, G 및 GS 시리즈 VM)</span><span class="sxs-lookup"><span data-stu-id="65b15-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="65b15-141">다음 시나리오의 경우 디스크 암호화가 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-141">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="65b15-142">기본 계층 VM.</span><span class="sxs-lookup"><span data-stu-id="65b15-142">Basic tier VMs.</span></span>
* <span data-ttu-id="65b15-143">클래식 배포 모델을 사용하여 만든 VM.</span><span class="sxs-lookup"><span data-stu-id="65b15-143">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="65b15-144">이미 암호화된 VM에서 암호화 키 업데이트</span><span class="sxs-lookup"><span data-stu-id="65b15-144">Updating the cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="65b15-145">온-프레미스 키 관리 서비스와의 통합</span><span class="sxs-lookup"><span data-stu-id="65b15-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="65b15-146">Azure Key Vault 및 키 만들기</span><span class="sxs-lookup"><span data-stu-id="65b15-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="65b15-147">시작하기 전에 최신 버전의 Azure PowerShell 모듈을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-147">Before you start, make sure that the latest version of the Azure PowerShell module has been installed.</span></span> <span data-ttu-id="65b15-148">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65b15-148">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="65b15-149">명령 예제 전체에서 모든 예제 매개 변수를 사용자 고유의 이름, 위치, 키 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-149">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="65b15-150">다음 예제에서는 *myResourceGroup*, *myKeyVault*, *myVM* 등의 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-150">The following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="65b15-151">첫 번째 단계는 암호화 키를 저장할 Azure Key Vault를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-151">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="65b15-152">Azure Key Vault는 응용 프로그램 및 서비스에 안전하게 구현할 수 있는 키와 암호를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-152">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="65b15-153">가상 디스크 암호화의 경우 Key Vault를 만들어 가상 디스크 암호화 또는 암호 해독에 사용되는 암호화 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-153">For virtual disk encryption, you create a Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="65b15-154">[Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider)를 사용하여 Azure 구독 내에서 Azure Key Vault 공급자를 사용하도록 설정하고 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-154">Enable the Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="65b15-155">다음 예제에서는 *미국 동부* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-155">The following example creates a resource group name *myResourceGroup* in the *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="65b15-156">암호화 키를 포함하는 Azure Key Vault와 저장소 및 VM과 같은 연결된 계산 리소스는 동일한 지역에 상주해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-156">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="65b15-157">[New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault)를 사용하여 Azure Key Vault을 만들고 디스크 암호화에 사용할 Key Vault를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="65b15-158">*keyVaultName*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="65b15-159">소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="65b15-160">HSM을 사용하려면 프리미엄 Key Vault가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="65b15-161">소프트웨어 보호 키를 저장하는 표준 Key Vault가 아닌 프리미엄 Key Vault를 만들려면 추가 비용이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-161">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="65b15-162">프리미엄 Key Vault를 만들려면 앞의 단계에서 *-Sku "Premium"* 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-162">To create a premium Key Vault, in the preceding step add the *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="65b15-163">표준 Key Vault를 만들었기 때문에 다음 예제는 소프트웨어 보호 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-163">The following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="65b15-164">두 가지 보호 모델 모두, 가상 디스크의 암호를 해독하기 위해 VM이 부팅될 때 암호화 키를 요청하려면 Azure 플랫폼에 액세스 권한이 허용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-164">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="65b15-165">[Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey)를 사용하여 Key Vault에 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="65b15-166">다음 예제는 *myKey*라는 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-166">The following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="65b15-167">Azure Active Directory 서비스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="65b15-167">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="65b15-168">가상 디스크가 암호화되거나 암호가 해독될 때 계정을 지정하여 Key Vault의 암호화 키 교환 및 인증을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-168">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="65b15-169">이 계정 즉, Azure Active Directory 서비스 사용자는 Azure 플랫폼이 VM을 대신하여 적절한 암호화 키를 요청하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-169">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="65b15-170">기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="65b15-171">[New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal)을 사용하여 Azure Active Directory에 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="65b15-172">보안 암호를 지정하려면 [Azure Active Directory의 암호 정책 및 제한 사항](../../active-directory/active-directory-passwords-policy.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-172">To specify a secure password, follow the [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="65b15-173">가상 디스크를 암호화하거나 암호를 해독하려면, Key Vault에 저장되어 있는 암호화 키에 대한 권한이 Azure Active Directory 서비스 사용자가 키를 읽는 것을 허용하도록 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-173">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="65b15-174">[Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="65b15-175">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="65b15-175">Create virtual machine</span></span>
<span data-ttu-id="65b15-176">암호화 프로세스를 테스트하기 위해 VM을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-176">To test the encryption process, let's create a VM.</span></span> <span data-ttu-id="65b15-177">다음 예제에서는 *Windows Server 2016 Datacenter* 이미지를 사용하여 *myVM*이라는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-177">The following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="65b15-178">가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="65b15-178">Encrypt virtual machine</span></span>
<span data-ttu-id="65b15-179">가상 디스크를 암호화하기 위해서 이전의 구성 요소를 모두 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-179">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="65b15-180">Azure Active Directory 서비스 사용자 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-180">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="65b15-181">암호화된 디스크에 대한 메타데이터를 저장할 Key Vault를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-181">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="65b15-182">실제 암호화 및 암호 해독에 사용될 암호화 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-182">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="65b15-183">OS 디스크, 데이터 디스크 또는 모든 디스크를 암호화할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-183">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="65b15-184">Azure Key Vault 키 및 Azure Active Directory 서비스 주체 자격 증명을 사용하여 [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension)을 통해 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using the Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="65b15-185">다음 예제에서는 모든 주요 정보를 검색한 후 *myVM*라는 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-185">The following example retrieves all the key information then encrypts the VM named *myVM*:</span></span>

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

<span data-ttu-id="65b15-186">확인 메시지를 수락하여 VM 암호화를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-186">Accept the prompt to continue with the VM encryption.</span></span> <span data-ttu-id="65b15-187">이 프로세스 동안 VM이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-187">The VM restarts during the process.</span></span> <span data-ttu-id="65b15-188">암호화 프로세스가 완료되고 VM이 재부팅되면 [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus)를 사용하여 암호화 상태를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-188">Once the encryption process completes and the VM has rebooted, review the encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="65b15-189">다음 예제와 유사하게 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="65b15-189">The output is similar to the following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="65b15-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65b15-190">Next steps</span></span>
* <span data-ttu-id="65b15-191">Azure Key Vault 관리 방법에 대한 자세한 내용은 [가상 컴퓨터에 대한 Key Vault 설정](key-vault-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65b15-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="65b15-192">Azure에 업로드할 암호화된 사용자 지정 VM 준비와 같은 디스크 암호화에 대한 자세한 내용은 [Azure Disk Encryption](../../security/azure-security-disk-encryption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65b15-192">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
