---
title: "암호화와 함께 저장 된 상태의 개인 데이터 azure 보호 | Microsoft Docs"
description: "이 문서는 Azure를 사용 하 여 개인 데이터를 보호 하는 데 도움이 되는 시리즈의 일부"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: d0ef3ca8d48f5ba11a89c787ff59df39eeaf673b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="76fdf-103">Azure 암호화 기술: 암호화로 미사용 개인 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="76fdf-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="76fdf-104">이 문서는 Azure 암호화 기술을 이해하고 사용하여 미사용 데이터를 보호하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-104">This article helps you understand and use Azure encryption technologies to secure data at rest.</span></span>

<span data-ttu-id="76fdf-105">중요하거나 개인적인 데이터를 보호하고 규정 준수 및 데이터 개인 정보 보호 요구 사항을 충족하려면 미사용 데이터를 암호화하여 보관하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-105">Encryption of data at rest is essential as a best practice to protect sensitive or personal data and to meet compliance and data privacy requirements.</span></span>
<span data-ttu-id="76fdf-106">미사용 데이터 암호화는 디스크에 있을 때 데이터를 암호화하여 공격자가 암호화되지 않은 데이터에 액세스하지 못하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-106">Encryption at rest is designed to prevent the attacker from accessing the unencrypted data by ensuring the data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="76fdf-107">시나리오</span><span class="sxs-lookup"><span data-stu-id="76fdf-107">Scenario</span></span> 

<span data-ttu-id="76fdf-108">미국에 본사를 둔 대형 크루즈 회사는 영국 제도뿐만 아니라 지중해 및 발트해 연안의 여정도 제공하도록 사업을 확장하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="76fdf-109">이러한 노력을 지원하기 위해 이탈리아, 독일, 덴마크 및 영국에 기반을 둔 몇 개의 소형 크루즈 라인을 인수했습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="76fdf-110">회사에서 Microsoft Azure를 사용하여 클라우드에 회사 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="76fdf-111">이 수 직원 또는 고객 정보가 다음과 같은 포함</span><span class="sxs-lookup"><span data-stu-id="76fdf-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="76fdf-112">주소</span><span class="sxs-lookup"><span data-stu-id="76fdf-112">addresses</span></span>
- <span data-ttu-id="76fdf-113">전화 번호</span><span class="sxs-lookup"><span data-stu-id="76fdf-113">phone numbers</span></span>
- <span data-ttu-id="76fdf-114">납세자 번호</span><span class="sxs-lookup"><span data-stu-id="76fdf-114">tax identification numbers</span></span>
- <span data-ttu-id="76fdf-115">의료 보험 정보</span><span class="sxs-lookup"><span data-stu-id="76fdf-115">medical information</span></span>
- <span data-ttu-id="76fdf-116">신용 카드 정보</span><span class="sxs-lookup"><span data-stu-id="76fdf-116">credit card information</span></span>

<span data-ttu-id="76fdf-117">회사는 데이터를 필요로 하는 해당 부서에 액세스할 수 있도록 하는 동안 직원 및 고객 데이터의 개인 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="76fdf-118">액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="76fdf-119">또한 크루즈 라인에서 현재 및 과거 고객과의 관계를 추적하기 위해 개인 정보가 포함된 보상 및 충성도 프로그램 구성원에 대한 대규모 데이터베이스를 유지하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-119">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="76fdf-120">문제 설명</span><span class="sxs-lookup"><span data-stu-id="76fdf-120">Problem statement</span></span>

<span data-ttu-id="76fdf-121">데이터 (예: 부서 급여 및 예약) 해야 하는 해당 부서에 액세스할 수 있도록 하는 동안 회사 직원의 고 고객의 개인 데이터의 개인 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-121">The company must protect the privacy of employees’ and customers’ personal data while making data accessible to those departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="76fdf-122">이러한 개인 데이터는 회사에서 제어하는 데이터 센터 외부에 저장되며 회사의 물리적 통제하에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-122">This personal data is stored outside of the corporate-controlled data center and is not under the company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="76fdf-123">회사 목표</span><span class="sxs-lookup"><span data-stu-id="76fdf-123">Company goal</span></span>

<span data-ttu-id="76fdf-124">다계층 심층 방어 보안 전략의 일부로 클라우드 저장소에 있는 데이터를 포함하여 개인 데이터가 포함된 모든 데이터 원본을 암호화하는 것이 회사의 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal to ensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="76fdf-125">권한 없는 사람이 개인 데이터에 액세스하는 경우 읽을 수 없는 형식으로 렌더링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-125">If unauthorized persons gain access to the personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="76fdf-126">암호화를 적용하는 경우 사용자 또는 관리자에게 쉽고 투명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="76fdf-127">솔루션</span><span class="sxs-lookup"><span data-stu-id="76fdf-127">Solutions</span></span>

<span data-ttu-id="76fdf-128">Azure 서비스는 미사용 개인 데이터를 암호화하여 보호할 수 있는 여러 도구와 기술을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-128">Azure services provide multiple tools and technologies to help you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="76fdf-129">Azure 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="76fdf-129">Azure Key Vault</span></span>

<span data-ttu-id="76fdf-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)는 Azure 서비스에서 미사용 데이터를 암호화하는 데 사용되는 키에 안전한 저장소를 제공하며 권장되는 키 저장소 및 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for the keys used to encrypt data at rest in Azure services and is the recommended key storage and management solution.</span></span> <span data-ttu-id="76fdf-131">암호화 키 관리는 저장된 데이터를 보호하는 데 필수적입니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-131">Encryption key management is essential to securing stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-to-protect-keys-that-encrypt-personal-data"></a><span data-ttu-id="76fdf-132">Azure Key Vault를 사용하여 개인 데이터를 암호화하는 키를 보호하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="76fdf-132">How do I use Azure Key Vault to protect keys that encrypt personal data?</span></span>

<span data-ttu-id="76fdf-133">Azure Key Vault를 사용하려면 Azure 계정에 대한 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-133">To use Azure Key Vault, you need a subscription to an Azure account.</span></span> <span data-ttu-id="76fdf-134">Azure PowerShell도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="76fdf-135">PowerShell cmdlet을 사용하여 다음을 수행하는 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-135">Steps include using PowerShell cmdlets to do the following:</span></span>

1. <span data-ttu-id="76fdf-136">구독에 연결</span><span class="sxs-lookup"><span data-stu-id="76fdf-136">Connect to your subscriptions</span></span>

2. <span data-ttu-id="76fdf-137">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="76fdf-137">Create a key vault</span></span>

3. <span data-ttu-id="76fdf-138">키 또는 암호를 키 자격 증명 모음에 추가</span><span class="sxs-lookup"><span data-stu-id="76fdf-138">Add a key or secret to the key vault</span></span>

4. <span data-ttu-id="76fdf-139">키 자격 증명 모음을 사용할 응용 프로그램을 Azure Active Directory에 등록</span><span class="sxs-lookup"><span data-stu-id="76fdf-139">Register applications that will use the key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="76fdf-140">키 또는 비밀을 사용하여 응용 프로그램에 권한 부여</span><span class="sxs-lookup"><span data-stu-id="76fdf-140">Authorize the applications to use the key or secret</span></span>

<span data-ttu-id="76fdf-141">키 자격 증명 모음을 만들려면 New-AzureRmKeyVault PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-141">To create a key vault, use the New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="76fdf-142">자격 증명 모음 이름, 리소스 그룹 이름 및 지리적 위치를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="76fdf-143">다른 cmdlet을 통해 키를 관리하는 경우 자격 증명 모음 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-143">You’ll use the vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="76fdf-144">REST API를 통해 자격 증명 모음을 사용하는 응용 프로그램은 자격 증명 모음 URI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-144">Applications that use the vault through the REST API will use the vault URI.</span></span>

<span data-ttu-id="76fdf-145">Azure Key Vault에서는 소프트웨어로 보호된 키를 제공하거나 .PFX 파일에서 기존 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="76fdf-146">자격 증명 모음에 비밀(암호)을 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-146">You can also store secrets (passwords) in the vault.</span></span>

<span data-ttu-id="76fdf-147">또한 로컬 HSM에서 키를 생성하고, 키가 HSM 경계를 벗어나지 않고 키 자격 증명 모음 서비스의 HSM에 전송할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-147">You can also generate a key in your local HSM and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary.</span></span>

<span data-ttu-id="76fdf-148">Azure Key Vault 사용에 대한 자세한 지침은 [Azure Key Vault 시작](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="76fdf-148">For detailed instructions on using Azure Key Vault, follow the steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="76fdf-149">Azure Key Vault와 함께 사용되는 PowerShell cmdlet 목록은 [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76fdf-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="76fdf-150">Windows용 Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="76fdf-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="76fdf-151">[Windows 및 Linux IaaS VM용 Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)은 Azure 가상 컴퓨터에서 미사용 개인 데이터를 보호하고 Azure Key Vault와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="76fdf-152">Azure Disk Encryption은 Windows에서 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx)를, Linux에서 [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt)를 사용하여 OS 및 데이터 드라이브를 모두 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux to encrypt both the OS and the data disks.</span></span> <span data-ttu-id="76fdf-153">Azure Disk Encryption은 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows 8 및 Windows 10 클라이언트에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-to-protect-personal-data"></a><span data-ttu-id="76fdf-154">Azure Disk Encryption을 사용하여 개인 데이터를 보호하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="76fdf-154">How do I use Azure Disk Encryption to protect personal data?</span></span>

<span data-ttu-id="76fdf-155">Azure Disk Encryption을 사용하려면 Azure 계정에 대한 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-155">To use Azure Disk Encryption, you need a subscription to an Azure account.</span></span> <span data-ttu-id="76fdf-156">Windows 및 Linux VM용 Azure Disk Encryption을 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-156">To enable Azure Disk Encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="76fdf-157">Azure Disk Encryption Resource Manager 템플릿, PowerShell 또는 CLI(명령줄 인터페이스)를 사용하여 디스크 암호화를 사용하도록 설정하고 암호화 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-157">Use the Azure Disk Encryption Resource Manager template, PowerShell, or the command line interface (CLI) to enable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="76fdf-158">Azure 플랫폼에 대한 액세스 권한을 부여하여 키 자격 증명 모음에서 암호화 자료를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-158">Grant access to the Azure platform to read the encryption material from your key vault.</span></span>

3. <span data-ttu-id="76fdf-159">AAD(Azure Active Directory) 응용 프로그램 ID를 제공하여 암호화 키 자료를 키 자격 증명 모음에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-159">Provide an Azure Active Directory (AAD) application identity to write the encryption key material to your key vault.</span></span>

<span data-ttu-id="76fdf-160">Azure에서 VM과 키 자격 증명 모음 구성을 업데이트하고 암호화된 VM을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-160">Azure will update the VM and the key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="76fdf-161">Azure Disk Encryption를 지원하도록 키 자격 증명 모음을 설정하면, 보안을 강화하고 암호화된 가상 컴퓨터의 백업을 지원하기 위해 KEK(키 암호화 키)를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-161">When you set up your key vault to support Azure Disk Encryption, you can add a key encryption key (KEK) for added security and to support backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="76fdf-162">특정 배포 시나리오 및 사용자 환경에 대한 자세한 지침은 [Windows 및 Linux IaaS VM용 Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="76fdf-163">Azure 저장소 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="76fdf-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="76fdf-164">[미사용 데이터에 대한 Azure SSE(저장소 서비스 암호화)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption)를 사용하면 조직의 보안 및 규정 준수 약정을 충족하도록 데이터를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="76fdf-165">Azure Storage에서 저장소에 저장하기 전에 256비트 AES 암호화를 사용하여 데이터를 자동으로 암호화하고 검색하기 전에 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior to persisting to storage, and decrypts it prior to retrieval.</span></span> <span data-ttu-id="76fdf-166">이 서비스는 Azure Blob 및 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-to-protect-personal-data"></a><span data-ttu-id="76fdf-167">저장소 서비스 암호화를 사용하여 개인 데이터를 보호하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="76fdf-167">How do I use Storage Service Encryption to protect personal data?</span></span>

<span data-ttu-id="76fdf-168">저장소 서비스 암호화를 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-168">To enable Storage Service Encryption, do the following:</span></span>

1. <span data-ttu-id="76fdf-169">Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-169">Log into the Azure portal.</span></span>

2. <span data-ttu-id="76fdf-170">저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-170">Select a storage account.</span></span>

3. <span data-ttu-id="76fdf-171">[설정]의 [Blob Service] 섹션에서 [암호화]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-171">In Settings, under the Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="76fdf-172">[File Service] 섹션 아래에서 [암호화]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-172">Under the File Service section, select Encryption.</span></span>

<span data-ttu-id="76fdf-173">암호화 설정을 클릭하면 저장소 서비스 암호화를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-173">After you click the Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="76fdf-174">새 데이터가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-174">New data will be encrypted.</span></span> <span data-ttu-id="76fdf-175">이 저장소 계정에 있는 기존 파일의 데이터는 암호화되지 않은 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="76fdf-176">암호화를 사용하도록 설정한 후에는 다음 방법 중 하나를 사용하여 저장소 계정에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-176">After enabling encryption, copy data to the storage account using one of the following methods:</span></span>

1. <span data-ttu-id="76fdf-177">[AzCopy 명령줄 유틸리티](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy)를 사용하여 Blob 또는 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-177">Copy blobs or files with the [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="76fdf-178">[SMB를 사용하여 파일 공유를 탑재](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows)하면 Robocopy와 같은 유틸리티를 사용하여 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy to copy files.</span></span>

3. <span data-ttu-id="76fdf-179">[저장소 클라이언트 라이브러리(예: .NET)](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs)를 사용하여 Blob 저장소 간에 또는 저장소 계정 간에 또는 Blob 또는 파일 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-179">Copy blob or file data to and from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="76fdf-180">[저장소 탐색기](https://docs.microsoft.com/en-us/azure/storage/storage-explorers)를 사용하여 암호화를 사용하도록 설정된 저장소 계정에 Blob을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) to upload blobs to your storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="76fdf-181">투명한 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="76fdf-181">Transparent Data Encryption</span></span>

<span data-ttu-id="76fdf-182">TDE(투명한 데이터 암호화)는 데이터베이스 및 서버 수준 모두에서 데이터를 암호화할 수 있는 SQL Azure의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both the database and server levels.</span></span> <span data-ttu-id="76fdf-183">TDE는 이제 기본적으로 새로 만든 모든 데이터베이스에서 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="76fdf-184">TDE는 데이터 및 로그 파일에 대한 실시간 I/O 암호화 및 암호 해독을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-184">TDE performs real-time I/O encryption and decryption of the data and log files.</span></span>

#### <a name="how-do-i-use-tde-to-protect-personal-data"></a><span data-ttu-id="76fdf-185">TDE를 사용하여 개인 데이터를 보호하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="76fdf-185">How do I use TDE to protect personal data?</span></span>

<span data-ttu-id="76fdf-186">Azure Portal, REST API 또는 PowerShell을 사용하여 TDE를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-186">You can configure TDE through the Azure portal, by using the REST API, or by using PowerShell.</span></span> <span data-ttu-id="76fdf-187">Azure Portal을 사용하여 기존 데이터베이스에서 TDE를 사용하도록 설정하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-187">To enable TDE on an existing database using the Azure Portal, do the following:</span></span>

1. <span data-ttu-id="76fdf-188"><https://portal.azure.com>의 Azure Portal을 방문하여 Azure 관리자 또는 참가자 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-188">Visit the Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="76fdf-189">왼쪽 배너에서 [찾아보기]를 클릭한 다음 SQL 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-189">On the left banner, click to BROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="76fdf-190">왼쪽 창에서 SQL 데이터베이스를 선택한 상태에서 사용자 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-190">With SQL databases selected in the left pane, click your user database.</span></span>

4. <span data-ttu-id="76fdf-191">데이터베이스 블레이드에서 [모두] 설정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-191">In the database blade, click All settings.</span></span>

5. <span data-ttu-id="76fdf-192">[설정] 블레이드에서 [투명한 데이터 암호화] 부분을 클릭하여 [투명한 데이터 암호화] 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-192">In the Settings blade, click Transparent data encryption part to open the Transparent data encryption blade.</span></span>

6. <span data-ttu-id="76fdf-193">[데이터 암호화] 블레이드에서 [데이터 암호화] 단추를 [설정]으로 전환한 다음, 페이지 맨 위에 있는 [저장]을 클릭하여 해당 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-193">In the Data encryption blade, move the Data encryption button to On, and then click Save (at the top of the page) to apply the setting.</span></span> <span data-ttu-id="76fdf-194">암호화 상태는 투명한 데이터 암호화 진행률과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-194">The Encryption status will approximate the progress of the transparent data encryption.</span></span>

![데이터 암호화를 사용하도록 설정](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="76fdf-196">TDE를 사용하도록 설정하는 방법에 대한 지침, TDE로 보호되는 데이터베이스의 암호 해독에 대한 내용 및 기타 자세한 내용은 [Azure SQL Database를 사용한 투명한 데이터 암호화](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) 문서에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-196">Instructions on how to enable TDE and information on decrypting TDE-protected databases and more can be found in the article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="76fdf-197">요약</span><span class="sxs-lookup"><span data-stu-id="76fdf-197">Summary</span></span>

<span data-ttu-id="76fdf-198">회사에서 Azure 클라우드에 저장된 개인 데이터를 암호화하는 목표를 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-198">The company can accomplish its goal of encrypting personal data stored in the Azure cloud.</span></span> <span data-ttu-id="76fdf-199">이렇게 하려면 Azure Disk Encryption을 사용하여 전체 볼륨을 보호하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-199">They can do this by using Azure Disk Encryption to  protect entire volumes.</span></span> <span data-ttu-id="76fdf-200">여기에는 식별 가능한 개인 정보 및 기타 중요한 데이터를 보관하는 운영 체제 파일과 데이터 파일이 모두 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-200">This may include both the operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="76fdf-201">Azure 저장소 서비스 암호화는 Blob 및 파일에 저장된 개인 데이터를 보호하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-201">Azure Storage Service encryption can be used to protect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="76fdf-202">Azure SQL 데이터베이스에 저장된 데이터의 경우 투명한 데이터 암호화는 무단 노출로부터 개인 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="76fdf-203">Azure에서 데이터를 암호화하는 데 사용되는 키를 보호하기 위해 회사에서 Azure Key Vault를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-203">To protect the keys that are used to encrypt data in Azure, the company can use Azure Key Vault.</span></span> <span data-ttu-id="76fdf-204">이렇게 하면 키 관리 프로세스가 간소화되고 회사에서 개인 데이터를 액세스하고 암호화하는 키를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76fdf-204">This streamlines the key management process and enables the company to maintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76fdf-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76fdf-205">Next steps</span></span>

- [<span data-ttu-id="76fdf-206">Azure Disk Encryption 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="76fdf-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="76fdf-207">Azure 가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="76fdf-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="76fdf-208">Azure Data Lake Store의 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="76fdf-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="76fdf-209">미사용 Azure Cosmos DB 데이터베이스 암호화</span><span class="sxs-lookup"><span data-stu-id="76fdf-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
