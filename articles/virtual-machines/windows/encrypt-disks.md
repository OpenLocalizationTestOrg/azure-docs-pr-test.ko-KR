---
title: "Azure에서 Windows VM에서 디스크 aaaEncrypt | Microsoft Docs"
description: "Tooencrypt 가상 디스크에 대 한 Windows VM에 Azure PowerShell을 사용 하 여 보안을 강화 하는 방법"
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
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="707fd-103">어떻게 tooencrypt Windows VM에서 가상 디스크</span><span class="sxs-lookup"><span data-stu-id="707fd-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="707fd-104">VM(가상 컴퓨터)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="707fd-105">디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="707fd-106">이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="707fd-107">이 세부 정보를 어떻게 문서 tooencrypt Azure PowerShell을 사용 하 여 Windows VM에서 가상 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="707fd-108">수도 있습니다 [hello Azure CLI 2.0을 사용 하 여 Linux VM 암호화](../linux/encrypt-disks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="707fd-109">디스크 암호화 개요</span><span class="sxs-lookup"><span data-stu-id="707fd-109">Overview of disk encryption</span></span>
<span data-ttu-id="707fd-110">Windows VM의 가상 디스크는 미사용 시 Bitlocker를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="707fd-111">Azure에서 가상 디스크 암호화는 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="707fd-112">암호화 키가 소프트웨어 보호를 사용 하 여 Azure 키 자격 증명 모음에 저장 하거나 가져오거나 140-2 수준 2 표준 tooFIPS 인증 된 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="707fd-113">이러한 암호화 한 키를 사용 하는 tooencrypt 가상 디스크 연결 된 tooyour VM의 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="707fd-114">이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="707fd-115">Azure Active Directory 서비스 사용자는 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="707fd-116">VM을 암호화 하기 위한 hello 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="707fd-117">Azure Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="707fd-118">암호화 키 toobe hello 디스크를 암호화 하는 데 사용할 수 있는 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="707fd-119">hello Azure 키 자격 증명 모음에서에서 tooread hello 암호화 키 hello 적절 한 권한이 있는 사용자는 Azure Active Directory 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="707fd-120">Hello 명령 tooencrypt hello Azure Active Directory 서비스 사용자 및 사용 되는 적절 한 암호화 키 toobe 지정 하 여 가상 디스크를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="707fd-121">hello Azure Active Directory 서비스 보안 주체 요청 hello Azure 키 자격 증명 모음에서 필요한 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="707fd-122">hello 가상 디스크는 암호화 키를 제공 하는 hello를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="707fd-123">암호화 프로세스</span><span class="sxs-lookup"><span data-stu-id="707fd-123">Encryption process</span></span>
<span data-ttu-id="707fd-124">다음과 같은 추가 구성 요소가 hello 디스크 암호화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="707fd-125">**Azure 키 자격 증명 모음** -toosafeguard 암호화 키 및 hello 디스크 암호화/암호 해독 프로세스에 사용 되는 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="707fd-126">이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="707fd-127">없는 toodedicate 주요 자격 증명 모음 tooencrypting 디스크.</span><span class="sxs-lookup"><span data-stu-id="707fd-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="707fd-128">tooseparate 관리 범위 및 키 가시성 전용된 키 자격 증명 모음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="707fd-129">**Azure Active Directory** -핸들 hello 필요한 암호화 키의 보안 교환 및 인증에 대 한 작업을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="707fd-130">일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="707fd-131">hello 서비스 사용자는 보안 메커니즘 toorequest 제공 하 고 hello 적절 한 암호화 키를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="707fd-132">Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="707fd-133">요구 사항 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="707fd-133">Requirements and limitations</span></span>
<span data-ttu-id="707fd-134">디스크 암호화에 대해 지원되는 시나리오 및 요구 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="707fd-135">Azure Marketplace 이미지 또는 사용자 지정 VHD 이미지에서 새 Windows VM에 대해 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="707fd-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="707fd-136">Azure에서 기존 Windows VM에 대해 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="707fd-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="707fd-137">저장소 공간을 사용하여 구성된 Windows VM에서 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="707fd-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="707fd-138">Windows VM에 대한 OS 및 데이터 드라이브에서 암호화 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="707fd-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="707fd-139">모든 리소스 (예: 키 자격 증명 모음, 저장소 계정 및 VM) hello에 있어야 합니다. 같은 Azure 지역 및 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="707fd-140">표준 계층 VM(예: A, D, DS, G 및 GS 시리즈 VM)</span><span class="sxs-lookup"><span data-stu-id="707fd-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="707fd-141">디스크 암호화 hello 다음 시나리오에서에서 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="707fd-142">기본 계층 VM.</span><span class="sxs-lookup"><span data-stu-id="707fd-142">Basic tier VMs.</span></span>
* <span data-ttu-id="707fd-143">Hello 클래식 배포 모델을 사용 하 여 만든 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="707fd-144">Hello 이미 암호화 된 VM에서 암호화 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="707fd-145">온-프레미스 키 관리 서비스와의 통합</span><span class="sxs-lookup"><span data-stu-id="707fd-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="707fd-146">Azure Key Vault 및 키 만들기</span><span class="sxs-lookup"><span data-stu-id="707fd-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="707fd-147">시작 하기 전에 있는지 확인 hello 최신 버전의 hello Azure PowerShell 모듈 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="707fd-148">자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="707fd-149">Hello 명령 예에서는 전체에서 고유한 이름, 위치 및 키 값으로 모든 예제에서는 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="707fd-150">hello 다음 예에서는 사용의 규칙 *myResourceGroup*, *myKeyVault*, *myVM*등입니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="707fd-151">hello 첫 번째 단계는 Azure 키 자격 증명 모음 toostore toocreate 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="707fd-152">Azure 주요 자격 증명, 비밀 키를 저장할 수 있습니다 또는 암호 toosecurely를 허용 하는 응용 프로그램 및 서비스에 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="707fd-153">가상 디스크 암호화, 키 자격 증명 모음 toostore tooencrypt 사용된 되는 암호화 키를 만들거나 가상 디스크의 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="707fd-154">Hello Azure 키 자격 증명 모음 공급자와 Azure 구독 내에서 사용 하도록 설정 [레지스터 AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), 리소스 그룹을 만드는 다음 [새로 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="707fd-155">hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 *myResourceGroup* hello에 *미국 동부* 위치:</span><span class="sxs-lookup"><span data-stu-id="707fd-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="707fd-156">hello Azure 키 자격 증명 모음 포함 hello 암호화 키와 연결 된 계산 hello VM 자체 저장소 같은 리소스에 있어야 합니다. 동일한 지역을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="707fd-157">Azure 키 자격 증명 모음 만들기와 [새로 AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) 디스크 암호화와 함께 사용 하기 위해 주요 자격 증명 모음 hello를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="707fd-158">*keyVaultName*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="707fd-159">소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="707fd-160">HSM을 사용하려면 프리미엄 Key Vault가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="707fd-161">소프트웨어 보호 키를 저장 하는 표준 주요 자격 증명 모음 보다는 주요 자격 증명 모음 프리미엄은 추가 비용 toocreating 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="707fd-162">toocreate hello 앞 단계에서에서 프리미엄 주요 자격 증명 추가 hello *-Sku "프리미엄"* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="707fd-163">hello 다음 예제에서는 소프트웨어 보호 키 이후 표준 주요 자격 증명 모음을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="707fd-164">두 보호 모델에 대 한 hello Azure 플랫폼 toobe hello VM toodecrypt hello 가상 디스크를 부팅 될 때 액세스 toorequest hello에 대 한 암호화 키에 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="707fd-165">[Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey)를 사용하여 Key Vault에 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="707fd-166">hello 다음 예제에서는 라는 키 *myKey*:</span><span class="sxs-lookup"><span data-stu-id="707fd-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="707fd-167">Hello Azure Active Directory 서비스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="707fd-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="707fd-168">가상 디스크를 암호화 하거나 암호를 해독할 때 계정 toohandle hello 인증 및 자격 증명 모음 키에서에서 암호화 키의 교환 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="707fd-169">이 계정에는 Azure Active Directory 서비스 사용자 hello Azure 플랫폼 toorequest hello VM hello 대신 하 여 적절 한 암호화 키를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="707fd-170">기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="707fd-171">[New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal)을 사용하여 Azure Active Directory에 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="707fd-172">hello를 수행 하는 보안 암호 toospecify [암호 정책 및 Azure Active Directory에서 제한](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="707fd-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="707fd-173">toosuccessfully 암호화 또는 가상 디스크를 암호 해독, 키 자격 증명 모음에 저장 된 hello 암호화 키에 대 한 권한 집합 toopermit hello Azure Active Directory 서비스 보안 주체 tooread hello 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="707fd-174">[Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="707fd-175">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="707fd-175">Create virtual machine</span></span>
<span data-ttu-id="707fd-176">tootest 암호화 프로세스를 hello, VM을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="707fd-177">hello 다음 예제에서는 V *myVM* 를 사용 하는 *Windows Server 2016 Datacenter* 이미지:</span><span class="sxs-lookup"><span data-stu-id="707fd-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="707fd-178">가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="707fd-178">Encrypt virtual machine</span></span>
<span data-ttu-id="707fd-179">tooencrypt hello 가상 디스크를 모아 놓은 모든 hello 이전 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="707fd-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="707fd-180">Hello Azure Active Directory 서비스 사용자 및 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="707fd-181">Hello 주요 자격 증명 모음 toostore hello 메타 데이터에 대 한 암호화 된 디스크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="707fd-182">Hello 실제 암호화 및 암호 해독에 대 한 암호화 키 toouse hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="707fd-183">Tooencrypt hello OS 디스크, hello 데이터 디스크 또는 모두 사용할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="707fd-184">암호화를 사용 하 여 VM [집합 AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) hello Azure 키 자격 증명 모음 키와 Azure Active Directory 서비스 사용자 자격 증명을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="707fd-185">hello 다음 예제에서는 hello 키 정보를 모두 검색 한 다음 암호화 hello 라는 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="707fd-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

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

<span data-ttu-id="707fd-186">Hello 프롬프트 toocontinue hello VM 암호화를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="707fd-187">hello 프로세스 중 hello VM 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="707fd-188">Hello 암호화 상태를 검토 하는 hello 암호화 프로세스가 완료 되 면 hello VM 다시 부팅 했습니다. [Get AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="707fd-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="707fd-189">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="707fd-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="707fd-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="707fd-190">Next steps</span></span>
* <span data-ttu-id="707fd-191">Azure Key Vault 관리 방법에 대한 자세한 내용은 [가상 컴퓨터에 대한 Key Vault 설정](key-vault-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="707fd-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="707fd-192">암호화 된 사용자 지정 VM tooupload tooAzure를 준비 하 고 같은 디스크 암호화에 대 한 자세한 내용은 참조 하십시오. [Azure 디스크 암호화](../../security/azure-security-disk-encryption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="707fd-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
