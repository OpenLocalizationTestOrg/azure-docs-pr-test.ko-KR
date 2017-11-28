---
title: "aaaAzure 암호화와 함께 저장 된 상태의 개인 데이터 보호 | Microsoft Docs"
description: "이 문서는 Azure tooprotect 개인 데이터를 사용 하는 데 도움이 되는 시리즈의 일부"
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
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="7891c-103">Azure 암호화 기술: 암호화로 미사용 개인 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="7891c-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="7891c-104">이 문서를 사용 하 여 이해 하 고 Azure 암호화 기술을 toosecure 데이터를 사용 하 여 저장 된 상태의 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="7891c-105">미사용 데이터 암호화 toomeet 규정 준수와 데이터 개인 정보 보호 요구 사항 및 모범 사례 tooprotect 중요 하거나 개인적인 데이터 반드시 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="7891c-106">휴지 암호화 hello 디스크에 있는 경우 데이터는 암호화 되도록 하 여 hello 암호화 되지 않은 데이터에 액세스 하지 못하도록 설계 된 tooprevent hello 공격자가입니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="7891c-107">시나리오</span><span class="sxs-lookup"><span data-stu-id="7891c-107">Scenario</span></span> 

<span data-ttu-id="7891c-108">Hello 미국에서에서 본사는 큰 크루즈 회사 hello 영국 제도 뿐만 아니라 hello 지중해 발트어 바다에서 해당 작업 toooffer 일정 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="7891c-109">toosupport 이탈리아, 독일, 덴마크, hello 영국에 따라 여러 개의 더 작은 크루즈 줄 획득 비슷한 작업</span><span class="sxs-lookup"><span data-stu-id="7891c-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="7891c-110">hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="7891c-111">이 수 직원 또는 고객 정보가 다음과 같은 포함</span><span class="sxs-lookup"><span data-stu-id="7891c-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="7891c-112">주소</span><span class="sxs-lookup"><span data-stu-id="7891c-112">addresses</span></span>
- <span data-ttu-id="7891c-113">전화 번호</span><span class="sxs-lookup"><span data-stu-id="7891c-113">phone numbers</span></span>
- <span data-ttu-id="7891c-114">납세자 번호</span><span class="sxs-lookup"><span data-stu-id="7891c-114">tax identification numbers</span></span>
- <span data-ttu-id="7891c-115">의료 보험 정보</span><span class="sxs-lookup"><span data-stu-id="7891c-115">medical information</span></span>
- <span data-ttu-id="7891c-116">신용 카드 정보</span><span class="sxs-lookup"><span data-stu-id="7891c-116">credit card information</span></span>

<span data-ttu-id="7891c-117">hello 회사 필요로 하는 데이터 액세스 가능한 toothose 부서 이와 동시에 직원 및 고객 데이터의 hello 개인 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="7891c-118">액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="7891c-119">hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="7891c-120">문제 설명</span><span class="sxs-lookup"><span data-stu-id="7891c-120">Problem statement</span></span>

<span data-ttu-id="7891c-121">hello 회사 (예: 부서 급여 및 예약) 해야 하는 데이터 액세스 가능한 toothose 부서 이와 동시에 직원의 고 고객의 개인 데이터의 hello 개인 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="7891c-122">이 개인 데이터 hello 제어 기업 데이터 센터 외부에서 저장 되 고 hello 회사의 물리적으로 제어 아래에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="7891c-123">회사 목표</span><span class="sxs-lookup"><span data-stu-id="7891c-123">Company goal</span></span>

<span data-ttu-id="7891c-124">다중 계층된 방어 보안 전략의 일부로, 클라우드 저장소에 상주 하는 것을 포함 하 여 개인 데이터가 포함 된 모든 데이터 원본의 암호화는 회사 목표 tooensure 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="7891c-125">Persons 이득 액세스 toohello 개인 데이터를 권한이 없으면 렌더링 하 고 읽을 수 없는 형식에서 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="7891c-126">암호화를 적용하는 경우 사용자 또는 관리자에게 쉽고 투명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="7891c-127">솔루션</span><span class="sxs-lookup"><span data-stu-id="7891c-127">Solutions</span></span>

<span data-ttu-id="7891c-128">Azure 서비스는 여러 도구와 기술 toohelp 제공 암호화 하 여 저장 된 상태의 개인 데이터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="7891c-129">Azure 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="7891c-129">Azure Key Vault</span></span>

<span data-ttu-id="7891c-130">[Azure 키 자격 증명 모음](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) hello 키에서 Azure 서비스의 tooencrypt 데이터를 사용 하 고는 hello 권장 키 저장소 및 관리 솔루션에 대 한 안전한 저장소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="7891c-131">암호화 키 관리는 필수 toosecuring 저장 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="7891c-132">개인 데이터를 암호화 하는 Azure 키 자격 증명 모음 tooprotect 키를 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7891c-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="7891c-133">Azure 키 자격 증명 모음 toouse 구독 tooan Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="7891c-134">Azure PowerShell도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="7891c-135">단계는 PowerShell cmdlet toodo hello 다음을 사용 하 여 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="7891c-136">Tooyour 구독 연결</span><span class="sxs-lookup"><span data-stu-id="7891c-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="7891c-137">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="7891c-137">Create a key vault</span></span>

3. <span data-ttu-id="7891c-138">키 또는 키 자격 증명 모음 보안 toohello 추가</span><span class="sxs-lookup"><span data-stu-id="7891c-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="7891c-139">Hello 주요 자격 증명 모음을 사용 하 여 Azure Active directory는 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="7891c-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="7891c-140">Hello 응용 프로그램 toouse hello 키 또는 암호를 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7891c-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="7891c-141">주요 자격 증명 모음 toocreate hello 새로 AzureRmKeyVault PowerShell CmDlt을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="7891c-142">자격 증명 모음 이름, 리소스 그룹 이름 및 지리적 위치를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="7891c-143">다른 Cmdlet 통해 키를 관리 하는 경우 자격 증명 모음 이름 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="7891c-144">Hello REST API를 통해 hello 자격 증명 모음을 사용 하는 응용 프로그램 hello 자격 증명 모음 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="7891c-145">Azure Key Vault에서는 소프트웨어로 보호된 키를 제공하거나 .PFX 파일에서 기존 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="7891c-146">또한 hello 자격 증명 모음에 암호를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="7891c-147">로컬 HSM에 키를 생성 하 고 hello HSM 경계를 종료 하는 hello 키 없이 tooHSMs hello 키 자격 증명 모음 서비스에에서 전송할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="7891c-148">단계를 hello Azure 키 자격 증명 모음을 사용 하는 자세한 방법은 다음과 [Azure 키 자격 증명 모음 시작 합니다.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="7891c-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="7891c-149">Azure Key Vault와 함께 사용되는 PowerShell cmdlet 목록은 [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7891c-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="7891c-150">Windows용 Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="7891c-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="7891c-151">[Windows 및 Linux IaaS VM용 Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)은 Azure 가상 컴퓨터에서 미사용 개인 데이터를 보호하고 Azure Key Vault와 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="7891c-152">Azure 디스크 암호화를 사용 하 여 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) windows에서 및 [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) OS 및 hello 데이터 디스크를 둘 다 hello Linux tooencrypt 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="7891c-153">Azure Disk Encryption은 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows 8 및 Windows 10 클라이언트에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="7891c-154">Azure 디스크 암호화 tooprotect 개인 데이터를 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7891c-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="7891c-155">Azure 디스크 암호화 toouse 구독 tooan Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="7891c-156">Windows 용 tooenable Azure 디스크 암호화와 Linux Vm의 경우, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="7891c-157">Hello Azure 디스크 암호화 리소스 관리자 템플릿, PowerShell 또는 hello 명령줄 인터페이스 (CLI) tooenable 디스크 암호화를 사용 하 고 암호화 구성을 지정 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="7891c-158">주요 자격 증명 모음에서 Azure 플랫폼 tooread hello 암호화 자료 toohello를 액세스 하는 권한 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="7891c-159">Azure Active Directory (AAD) 응용 프로그램 identity toowrite hello 암호화 키 재료 tooyour 키 자격 증명 모음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="7891c-160">Azure VM hello 및 hello 주요 자격 증명 모음 구성 업데이트 하 고 암호화 된 VM을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="7891c-161">Azure 디스크 암호화 하 여 주요 자격 증명 모음 toosupport을 설정할 때 추가 보안 및 암호화 된 가상 컴퓨터의 toosupport 백업에 대 한 키 암호화 키 KEK ()를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="7891c-162">특정 배포 시나리오 및 사용자 환경에 대한 자세한 지침은 [Windows 및 Linux IaaS VM용 Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="7891c-163">Azure 저장소 서비스 암호화</span><span class="sxs-lookup"><span data-stu-id="7891c-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="7891c-164">[Azure 저장소 서비스 암호화 SSE () 미사용 데이터에 대 한](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) 하면 보호 하 고 데이터 toomeet 조직 보안 및 규정 준수 행 결과 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="7891c-165">Azure 저장소는 자동으로 256 비트 AES 암호화 이전 toopersisting toostorage를 사용 하 여 데이터를 암호화 하 고 이전 tooretrieval 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="7891c-166">이 서비스는 Azure Blob 및 파일에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="7891c-167">저장소 서비스 암호화 tooprotect 개인 데이터를 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7891c-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="7891c-168">저장소 서비스 암호화 tooenable 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="7891c-169">Azure 포털 hello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="7891c-170">저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-170">Select a storage account.</span></span>

3. <span data-ttu-id="7891c-171">설정에서 hello Blob 서비스 섹션에서 암호화를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="7891c-172">Hello 파일 서비스 섹션에서 암호화를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="7891c-173">Hello 암호화 설정을 클릭 한 후 사용 하도록 설정 하거나 저장소 서비스 암호화를 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="7891c-174">새 데이터가 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-174">New data will be encrypted.</span></span> <span data-ttu-id="7891c-175">이 저장소 계정에 있는 기존 파일의 데이터는 암호화되지 않은 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="7891c-176">암호화를 사용 하도록 설정한 후 hello 메서드를 다음 중 하나를 사용 하 여 데이터 toohello 저장소 계정에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="7891c-177">Blob 또는 hello 사용 하 여 파일 복사 [AzCopy 명령 줄 유틸리티](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy)합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="7891c-178">[SMB를 사용 하 여 파일 공유를 탑재](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) Robocopy toocopy 파일과 같은 유틸리티를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="7891c-179">Blob 또는 파일 데이터 tooand 사이 또는 blob 저장소에서 사용 하 여 저장소 계정을 복사 [.NET 등의 저장소 클라이언트 라이브러리](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs)합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="7891c-180">사용 하 여 한 [저장소 탐색기](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload 암호화가 설정 되어 tooyour 저장소 계정 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="7891c-181">투명한 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="7891c-181">Transparent Data Encryption</span></span>

<span data-ttu-id="7891c-182">투명 한 데이터 암호화 (TDE)는의 기능이 며 SQL Azure는 기준인 hello 데이터베이스 및 서버 수준 모두에 데이터를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="7891c-183">TDE는 이제 기본적으로 새로 만든 모든 데이터베이스에서 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="7891c-184">TDE는 실시간 I/O 암호화 및 hello 데이터 및 로그 파일의 암호 해독을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="7891c-185">TDE tooprotect 개인 데이터를 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7891c-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="7891c-186">Hello REST API를 사용 하 여 또는 PowerShell을 사용 하 여 hello Azure 포털을 통해 TDE를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="7891c-187">hello Azure 포털을 사용 하 여 기존 데이터베이스에 TDE tooenable 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="7891c-188">방문 hello Azure 포털에서 <https://portal.azure.com> 및 Azure 관리자 또는 참가자 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="7891c-189">Hello 왼쪽된 배너에서 tooBROWSE를 클릭 한 다음 SQL 데이터베이스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="7891c-190">Hello 왼쪽된 창에서 선택한 SQL 데이터베이스, 사용자 데이터베이스를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="7891c-191">Hello 데이터베이스 블레이드 모든 설정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="7891c-192">Hello 설정 블레이드에서에서 투명 한 데이터 암호화 부분 tooopen hello 투명 한 데이터 암호화 블레이드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="7891c-193">Hello 데이터 암호화 단추 tooOn 이동한 다음 (hello 페이지의 위쪽 hello) 저장을 클릭 hello 데이터 암호화 블레이드에서 tooapply hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="7891c-194">hello 암호화 상태는 hello 투명 한 데이터 암호화의 진행률과를 hello 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![데이터 암호화를 사용하도록 설정](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="7891c-196">Hello 문서에서 TDE로 보호 된 데이터베이스를 암호 해독에 방법과 tooenable TDE 수 발견 하는 방법에 대 한 지침 [Azure SQL 데이터베이스를 사용한 투명 한 데이터 암호화 합니다.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="7891c-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="7891c-197">요약</span><span class="sxs-lookup"><span data-stu-id="7891c-197">Summary</span></span>

<span data-ttu-id="7891c-198">hello 회사 hello Azure 클라우드에에서 저장 된 개인 데이터를 암호화할 해당 목표를 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="7891c-199">Azure 디스크 암호화를 사용 하 여 이렇게 하려면 너무 전체 볼륨을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="7891c-200">여기에 hello 운영 체제 파일 및 개인 식별이 가능한 정보 및 기타 중요 한 데이터를 저장 된 데이터 파일을 모두 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="7891c-201">Azure 저장소 서비스 암호화 blob 및 파일에 저장 되어 있는 개인 데이터를 사용 하는 tooprotect 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="7891c-202">Azure SQL 데이터베이스에 저장된 데이터의 경우 투명한 데이터 암호화는 무단 노출로부터 개인 정보를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="7891c-203">Azure에서 사용 되는 tooencrypt 데이터 있는 tooprotect hello 키는 hello 회사는 Azure 키 자격 증명 모음 사용.</span><span class="sxs-lookup"><span data-stu-id="7891c-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="7891c-204">이 hello 키 관리 프로세스를 간소화 하 고 활성화 hello에 액세스 하 고 개인 데이터 암호화 키의 회사 toomaintain 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7891c-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7891c-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7891c-205">Next steps</span></span>

- [<span data-ttu-id="7891c-206">Azure Disk Encryption 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="7891c-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="7891c-207">Azure 가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="7891c-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="7891c-208">Azure Data Lake Store의 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="7891c-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="7891c-209">미사용 Azure Cosmos DB 데이터베이스 암호화</span><span class="sxs-lookup"><span data-stu-id="7891c-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
