---
title: "Azure Key Vault에 HSM 보호 키를 생성하고 전송하는 방법 | Microsoft Docs"
description: "이 문서를 통해 Azure 주요 자격 증명 모음에서 사용할 고유의 HSM 보호 키를 생성하고 전송하는 데 필요한 계획을 세울 수 있습니다. BYOK, 즉 Bring Your Own Key라고도 합니다."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 5dbee1221f64045c64fecb344de1e03b2183dfb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-generate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="a87f4-104">Azure 주요 자격 증명 모음에 대해 HSM 보호된 키를 생성하고 전송하는 방법</span><span class="sxs-lookup"><span data-stu-id="a87f4-104">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="a87f4-105">소개</span><span class="sxs-lookup"><span data-stu-id="a87f4-105">Introduction</span></span>
<span data-ttu-id="a87f4-106">보안을 강화하기 위해 Azure 주요 자격 증명 모음 사용 시 HSM 경계를 절대로 벗어나지 않고 HSM(하드웨어 보안 모듈)에서 키를 가져오거나 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="a87f4-107">이 시나리오를 흔히 BYOK( *Bring Your Own Key*)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-107">This scenario is often referred to as *bring your own key*, or BYOK.</span></span> <span data-ttu-id="a87f4-108">HSM은 FIPS 140-2 Level 2 유효성 검사가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-108">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="a87f4-109">Azure 주요 자격 증명 모음은 HSM의 Thales nShield 제품군을 사용하여 키를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-109">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span></span>

<span data-ttu-id="a87f4-110">이 토픽의 내용을 통해 Azure Key Vault에서 사용할 고유의 HSM 보호된 키를 생성하고 전송하는 데 필요한 계획을 세울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-110">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>

<span data-ttu-id="a87f4-111">이 기능은 Azure 중국에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="a87f4-112">Azure 주요 자격 증명 모음에 대한 자세한 내용은 [Azure 주요 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a87f4-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="a87f4-113">HSM 보호된 키를 위해 주요 자격 증명 모음 만들기가 포함된 자습서를 시작하려면 [Azure 주요 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="a87f4-114">다음은 인터넷을 통해 HSM 보호된 키를 생성하고 전송하는 작업에 대한 추가 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-114">More information about generating and transferring an HSM-protected key over the Internet:</span></span>

* <span data-ttu-id="a87f4-115">공격에 대한 취약성을 줄이기 위해 오프라인 워크스테이션에서 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-115">You generate the key from an offline workstation, which reduces the attack surface.</span></span>
* <span data-ttu-id="a87f4-116">키는 KEK(키 교환 키)로 암호화되어 Azure 주요 자격 증명 모음 HSM으로 전송될 때까지 암호화 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-116">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span></span> <span data-ttu-id="a87f4-117">암호화된 버전의 키만 원래 워크스테이션을 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-117">Only the encrypted version of your key leaves the original workstation.</span></span>
* <span data-ttu-id="a87f4-118">도구 집합은 Azure 주요 자격 증명 모음 보안 영역에 키를 바인딩하는 테넌트 키에 대한 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-118">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span></span> <span data-ttu-id="a87f4-119">따라서 Azure 주요 자격 증명 모음 HSM이 키를 받고 암호를 해독한 후에는 이 HSM만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-119">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="a87f4-120">키는 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-120">Your key cannot be exported.</span></span> <span data-ttu-id="a87f4-121">이 바인딩은 Thales HSM에 의해 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-121">This binding is enforced by the Thales HSMs.</span></span>
* <span data-ttu-id="a87f4-122">키 암호화에 사용되는 KEK(키 교환 키)는 Azure 주요 자격 증명 모음 HSM 내에서 생성되며 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-122">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="a87f4-123">HSM은 HSM 외부에 클리어 버전의 KEK가 있을 수 없도록 강제합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-123">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span></span> <span data-ttu-id="a87f4-124">또한 도구 집합에는 KEK는 내보낼 수 없으며 Thales에서 제조한 정품 HSM 내에서 생성된 것이라는 Thales의 증명이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-124">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="a87f4-125">도구 집합에는 Azure 주요 자격 증명 모음 보안 영역도 Thales에서 제조한 정품 HSM에서 생성된 것이라는 Thales의 증명이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-125">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="a87f4-126">이를 통해 Microsoft가 정품 하드웨어를 사용하고 있다는 것을 입증합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-126">This attestation proves to you that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="a87f4-127">Microsoft는 각 지역별로 별도의 보안 권역과 별도의 KEK를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="a87f4-128">이러한 구분을 통해 해당 키가 사용자가 암호화한 지역의 데이터 센터에서만 사용되게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-128">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span></span> <span data-ttu-id="a87f4-129">예를 들어 유럽 고객의 키는 북아메리카 또는 아시아의 데이터 센터에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="a87f4-130">Thales HSM 및 Microsoft 서비스에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="a87f4-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="a87f4-131">Thales e-Security는 금융 서비스, 첨단 기술, 제조, 정부 및 기술 분야에서 데이터 암호화 및 사이버 보안 솔루션을 제공하는 선도적인 글로벌 기업입니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="a87f4-132">기업과 정부의 정보를 보호하는 지난 40년간 누적된 성과를 바탕으로, Thales 솔루션은 최대 에너지 및 항공 우주 기업 다섯 곳 중 네 곳에서 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span></span> <span data-ttu-id="a87f4-133">또한 22개 NATO 국가에서 사용되고 있으며 전세계 지불 거래의 80퍼센트 이상의 보안을 담당하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="a87f4-134">Microsoft는 Thales과의 협력을 통해 HSM을 최첨단 상태로 향상시켰습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-134">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span></span> <span data-ttu-id="a87f4-135">이렇게 향상된 기능을 통해 사용자는 자신의 키에 대한 제어를 포기하지 않으면서 호스트된 서비스의 일반적인 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-135">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="a87f4-136">Microsoft에서 이러한 향상된 기능을 사용하여 HSM을 관리해 주므로 이 부분에 신경 쓰지 않아도 된다는 것이 특별한 장점입니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-136">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span></span> <span data-ttu-id="a87f4-137">클라우드 서비스로써 Azure 주요 자격 증명 모음은 급박한 요청에도 크기 확장이 가능하기 때문에 조직의 급증하는 사용량을 맞출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-137">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span></span> <span data-ttu-id="a87f4-138">그와 동시에 키는 Microsoft의 HSM 내에서 보호됩니다. 키를 생성하고 Microsoft의 HSM에 전송하기 때문에 키의 수명 주기 동안 사용자가 키에 대한 제어를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-138">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="a87f4-139">Azure 주요 자격 증명 모음에 대한 BYOK(Bring Your Own Key) 구현</span><span class="sxs-lookup"><span data-stu-id="a87f4-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="a87f4-140">고유의 HSM 보호된 키를 생성한 다음 Azure 주요 자격 증명 모음으로 전송하는 경우(BYOK(Bring Your Own Key) 시나리오) 다음 내용 및 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-140">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="a87f4-141">BYOK에 대한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="a87f4-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="a87f4-142">Azure 주요 자격 증명 모음에 대해 BYOK(Bring Your Own Key)를 위한 필수 조건 목록은 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-142">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="a87f4-143">요구 사항</span><span class="sxs-lookup"><span data-stu-id="a87f4-143">Requirement</span></span> | <span data-ttu-id="a87f4-144">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="a87f4-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="a87f4-145">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="a87f4-145">A subscription to Azure</span></span> |<span data-ttu-id="a87f4-146">Azure Key Vault를 만들려면 Azure 구독이 필요합니다([무료 평가판 가입](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="a87f4-146">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="a87f4-147">HSM 보호 키를 지원하는 Azure Key Vault 프리미엄 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="a87f4-147">The Azure Key Vault Premium service tier to support HSM-protected keys</span></span> |<span data-ttu-id="a87f4-148">Azure 주요 자격 증명 모음에 대한 서비스 계층 및 기능에 대한 자세한 내용은 [Azure 주요 자격 증명 모음 가격 책정](https://azure.microsoft.com/pricing/details/key-vault/) 웹 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-148">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="a87f4-149">Thales HSM, 스마트 카드 및 지원 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="a87f4-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="a87f4-150">Thales 하드웨어 보안 모듈에 대한 액세스 권한 및 Thales HSM의 기본 작동 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-150">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="a87f4-151">호환되는 모델 목록을 보거나, HSM이 없는 경우 구매하려면 [Thales 하드웨어 보안 모듈](https://www.thales-esecurity.com/msrms/buy) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="a87f4-152">다음 하드웨어 및 소프트웨어:</span><span class="sxs-lookup"><span data-stu-id="a87f4-152">The following hardware and software:</span></span><ol><li><span data-ttu-id="a87f4-153">Windows 운영 체제 Windows 7 이상 및 Thales nShield 소프트웨어 버전 11.50 이상이 설치된 오프라인 x64 워크스테이션.</span><span class="sxs-lookup"><span data-stu-id="a87f4-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="a87f4-154">이 워크스테이션에서 Windows 7을 실행하는 경우 [Microsoft.NET Framework 4.5를 설치](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="a87f4-155">인터넷에 연결되어 있으며 Windows 7 이상의 Windows 운영 체제 및 [Azure PowerShell](/powershell/azure/overview) **최소 버전 1.1.0**이 설치된 워크스테이션</span><span class="sxs-lookup"><span data-stu-id="a87f4-155">A workstation that is connected to the Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="a87f4-156">여유 공간이 16MB 이상인 USB 드라이브 또는 기타 휴대용 저장 장치 </span><span class="sxs-lookup"><span data-stu-id="a87f4-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="a87f4-157">보안상의 이유로 첫 번째 워크스테이션은 네트워크에 연결하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-157">For security reasons, we recommend that the first workstation is not connected to a network.</span></span> <span data-ttu-id="a87f4-158">그러나 이 권고는 프로그램 방식으로 강제 적용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="a87f4-159">이후의 지침에서는 이 워크스테이션을 분리된 워크스테이션이라 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-159">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="a87f4-160">또한 테넌트 키가 프로덕션 네트워크용인 경우 별도의 두 번째 워크스테이션을 사용하여 도구 집합을 다운로드하고 테넌트 키를 업로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span></span> <span data-ttu-id="a87f4-161">그러나 테스트 목적인 경우에는 첫 번째와 동일한 워크스테이션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-161">But for testing purposes, you can use the same workstation as the first one.</span></span><br/><br/><span data-ttu-id="a87f4-162">이후의 지침에서는 이 두 번째 워크스테이션을 인터넷에 연결된 워크스테이션이라 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-162">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-to-azure-key-vault-hsm"></a><span data-ttu-id="a87f4-163">키 생성 및 Azure 주요 자격 증명 모음에 전송</span><span class="sxs-lookup"><span data-stu-id="a87f4-163">Generate and transfer your key to Azure Key Vault HSM</span></span>
<span data-ttu-id="a87f4-164">다음 5단계에 따라 키를 생성하여 Azure Key Vault HSM으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-164">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="a87f4-165">1단계: 인터넷에 연결된 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="a87f4-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="a87f4-166">2단계: 연결이 끊어진 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="a87f4-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="a87f4-167">3단계: 키 생성</span><span class="sxs-lookup"><span data-stu-id="a87f4-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="a87f4-168">4단계: 전송할 키 준비</span><span class="sxs-lookup"><span data-stu-id="a87f4-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="a87f4-169">5단계: Azure 주요 자격 증명 모음에 키 전송</span><span class="sxs-lookup"><span data-stu-id="a87f4-169">Step 5: Transfer your key to Azure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="a87f4-170">1단계: 인터넷에 연결된 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="a87f4-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="a87f4-171">이 첫 번째 단계는 인터넷에 연결된 워크스테이션에서 다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-171">For this first step, do the following procedures on your workstation that is connected to the Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="a87f4-172">1.1단계: Azure PowerShell 설치</span><span class="sxs-lookup"><span data-stu-id="a87f4-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="a87f4-173">인터넷에 연결된 워크스테이션에서 Azure 주요 자격 증명 모음을 관리하기 위해 cmdlet이 포함된 Azure PowerShell 모듈을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-173">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span></span> <span data-ttu-id="a87f4-174">이를 위해 0.8.13 이상 버전이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="a87f4-175">설치 지침은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-175">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="a87f4-176">1.2단계: Azure 구독 ID 얻기</span><span class="sxs-lookup"><span data-stu-id="a87f4-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="a87f4-177">Azure PowerShell 세션을 시작하고 다음 명령을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-177">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="a87f4-178">팝업 브라우저 창에 Azure 계정 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-178">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="a87f4-179">그런 다음 [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-179">Then, use the [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="a87f4-180">출력된 내용에서 Azure 주요 자격 증명 모음에 사용할 구독 ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-180">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="a87f4-181">이 구독 ID는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="a87f4-182">Azure PowerShell 창을 닫지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-182">Do not close the Azure PowerShell window.</span></span>

### <a name="step-13-download-the-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="a87f4-183">1.3단계: Azure 주요 자격 증명 모음에 대한 BYOK 도구 집합 다운로드</span><span class="sxs-lookup"><span data-stu-id="a87f4-183">Step 1.3: Download the BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="a87f4-184">Microsoft 다운로드 센터로 이동하여 해당 지리적 지역 또는 Azure 인스턴스에 대한 [Azure 주요 자격 증명 모음 BYOK 도구 집합을 다운로드](http://www.microsoft.com/download/details.aspx?id=45345) 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-184">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="a87f4-185">다음 정보를 사용하여 패키지 이름을 식별하고 해당 SHA-256 패키지 해시를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-185">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="a87f4-186">**미국:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-186">**United States:**</span></span>

<span data-ttu-id="a87f4-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="a87f4-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="a87f4-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="a87f4-189">**유럽:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-189">**Europe:**</span></span>

<span data-ttu-id="a87f4-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="a87f4-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="a87f4-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="a87f4-192">**아시아:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-192">**Asia:**</span></span>

<span data-ttu-id="a87f4-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="a87f4-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="a87f4-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="a87f4-195">**라틴 아메리카:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-195">**Latin America:**</span></span>

<span data-ttu-id="a87f4-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="a87f4-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="a87f4-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="a87f4-198">**일본:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-198">**Japan:**</span></span>

<span data-ttu-id="a87f4-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="a87f4-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="a87f4-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="a87f4-201">**한국:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-201">**Korea:**</span></span>

<span data-ttu-id="a87f4-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="a87f4-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="a87f4-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="a87f4-204">**오스트레일리아:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-204">**Australia:**</span></span>

<span data-ttu-id="a87f4-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="a87f4-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="a87f4-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="a87f4-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="a87f4-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="a87f4-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="a87f4-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="a87f4-210">**미국 정부 DOD:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-210">**US Government DOD:**</span></span>

<span data-ttu-id="a87f4-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="a87f4-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="a87f4-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="a87f4-213">**캐나다:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-213">**Canada:**</span></span>

<span data-ttu-id="a87f4-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="a87f4-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="a87f4-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="a87f4-216">**독일:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-216">**Germany:**</span></span>

<span data-ttu-id="a87f4-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="a87f4-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="a87f4-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="a87f4-219">**인도:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-219">**India:**</span></span>

<span data-ttu-id="a87f4-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="a87f4-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="a87f4-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="a87f4-222">**영국:**</span><span class="sxs-lookup"><span data-stu-id="a87f4-222">**United Kingdom:**</span></span>

<span data-ttu-id="a87f4-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="a87f4-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="a87f4-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="a87f4-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="a87f4-225">다운로드한 BYOK 도구 집합의 무결성을 확인하려면 Azure PowerShell 세션에서 [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-225">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="a87f4-226">도구 집합에는 다음이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-226">The toolset includes the following:</span></span>

* <span data-ttu-id="a87f4-227">이름이 **BYOK-KEK-pkg-**</span><span class="sxs-lookup"><span data-stu-id="a87f4-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="a87f4-228">이름이 **BYOK-SecurityWorld-pkg-**</span><span class="sxs-lookup"><span data-stu-id="a87f4-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="a87f4-229">이름이 **verifykeypackage.py**인 python 스크립트</span><span class="sxs-lookup"><span data-stu-id="a87f4-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="a87f4-230">이름이 **KeyTransferRemote.exe** 인 명령줄 실행 파일 및 관련 DLL</span><span class="sxs-lookup"><span data-stu-id="a87f4-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="a87f4-231">이름이 **vcredist_x64.exe**인 Visual C++ 재배포 가능 패키지</span><span class="sxs-lookup"><span data-stu-id="a87f4-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="a87f4-232">USB 드라이브 또는 기타 휴대용 저장소에 패키지를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-232">Copy the package to a USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="a87f4-233">2단계: 연결이 끊어진 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="a87f4-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="a87f4-234">이 두 번째 단계에서는 네트워크(인터넷 또는 내부 네트워크)에 연결되지 않은 워크스테이션에서 다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-234">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span></span>

### <a name="step-21-prepare-the-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="a87f4-235">2.1단계: Thales HSM이 있는 연결이 끊어진 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="a87f4-235">Step 2.1: Prepare the disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="a87f4-236">Windows 컴퓨터에 nCipher(Thales) 지원 소프트웨어를 설치한 다음 Thales HSM을 해당 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-236">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span></span>

<span data-ttu-id="a87f4-237">Thales 도구가 해당 경로(**%nfast_home%\bin**)에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-237">Ensure that the Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="a87f4-238">예를 들어 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-238">For example, type the following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="a87f4-239">자세한 내용은 Thales HSM에 포함된 사용자 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-239">For more information, see the user guide included with the Thales HSM.</span></span>

### <a name="step-22-install-the-byok-toolset-on-the-disconnected-workstation"></a><span data-ttu-id="a87f4-240">2.2단계: 연결이 끊어진 워크스테이션에 BYOK 도구 집합 설치</span><span class="sxs-lookup"><span data-stu-id="a87f4-240">Step 2.2: Install the BYOK toolset on the disconnected workstation</span></span>
<span data-ttu-id="a87f4-241">USB 드라이브 또는 기타 휴대용 저장소에서 BYOK 도구 집합 패키지를 복사한 후 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-241">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span></span>

1. <span data-ttu-id="a87f4-242">다운로드한 패키지에서 임의 폴더로 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-242">Extract the files from the downloaded package into any folder.</span></span>
2. <span data-ttu-id="a87f4-243">해당 폴더에서 vcredist_x64.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="a87f4-244">지침에 따라 Visual Studio 2013용 Visual C++ 런타임 구성 요소를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-244">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="a87f4-245">3단계: 키 생성</span><span class="sxs-lookup"><span data-stu-id="a87f4-245">Step 3: Generate your key</span></span>
<span data-ttu-id="a87f4-246">이 3단계에서는 연결이 끊어진 워크스테이션에서 다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-246">For this third step, do the following procedures on the disconnected workstation.</span></span> <span data-ttu-id="a87f4-247">이 단계를 완료하려면 HSM이 초기화 모드에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-247">To complete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-the-hsm-mode-to-i"></a><span data-ttu-id="a87f4-248">3.1단계: HSM 모드를 'I'로 변경</span><span class="sxs-lookup"><span data-stu-id="a87f4-248">Step 3.1: Change the HSM mode to 'I'</span></span>
<span data-ttu-id="a87f4-249">Thales nShield Edge를 사용하는 경우 모드를 1로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-249">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="a87f4-250">모드 단추를 사용하여 필요한 모드를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-250">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="a87f4-251">2.</span><span class="sxs-lookup"><span data-stu-id="a87f4-251">2.</span></span> <span data-ttu-id="a87f4-252">몇 초 안에 지우기 단추를 몇 초간 길게 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-252">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="a87f4-253">모드가 변경되면 새로운 모드의 LED가 깜박임을 중지하고 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-253">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="a87f4-254">상태 LED가 몇 초간 불규칙하게 깜박일 수도 있으며, 장치가 준비되면 정기적으로 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-254">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="a87f4-255">그렇지 않으면 장치가 현재 모드로 유지되고 해당 모드 LED가 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-255">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="a87f4-256">3.2단계: 보안 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="a87f4-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="a87f4-257">명령 프롬프트를 시작하고 Thales의 새 영역 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-257">Start a command prompt and run the Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="a87f4-258">이 프로그램은 C:\ProgramData\nCipher\Key Management Data\local 폴더에 해당하는 %NFAST_KMDATA%\local\world에 **Security World** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="a87f4-259">쿼럼에 다른 값을 사용할 수 있지만, 이 예에서는 각각에 대해 3개의 빈 카드와 핀을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-259">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span></span> <span data-ttu-id="a87f4-260">그러면 임의의 두 카드에서 보안 영역에 대한 모든 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-260">Then, any two cards give full access to the security world.</span></span> <span data-ttu-id="a87f4-261">이러한 카드가 새 보안 영역에 대한 **관리자 카드 집합** 이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-261">These cards become the **Administrator Card Set** for the new security world.</span></span>

<span data-ttu-id="a87f4-262">그런 다음 아래 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-262">Then do the following:</span></span>

* <span data-ttu-id="a87f4-263">영역 파일을 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-263">Back up the world file.</span></span> <span data-ttu-id="a87f4-264">영역 파일, 관리자 카드, 해당 핀을 보호하고 한 사람이 둘 이상의 카드에 액세스 권한을 가지지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-264">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span></span>

### <a name="step-33-change-the-hsm-mode-to-o"></a><span data-ttu-id="a87f4-265">3.3단계: HSM 모드를 'O'로 변경</span><span class="sxs-lookup"><span data-stu-id="a87f4-265">Step 3.3: Change the HSM mode to 'O'</span></span>
<span data-ttu-id="a87f4-266">Thales nShield Edge를 사용하는 경우 모드를 1로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-266">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="a87f4-267">모드 단추를 사용하여 필요한 모드를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-267">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="a87f4-268">2.</span><span class="sxs-lookup"><span data-stu-id="a87f4-268">2.</span></span> <span data-ttu-id="a87f4-269">몇 초 안에 지우기 단추를 몇 초간 길게 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-269">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="a87f4-270">모드가 변경되면 새로운 모드의 LED가 깜박임을 중지하고 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-270">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="a87f4-271">상태 LED가 몇 초간 불규칙하게 깜박일 수도 있으며, 장치가 준비되면 정기적으로 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-271">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="a87f4-272">그렇지 않으면 장치가 현재 모드로 유지되고 해당 모드 LED가 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-272">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>


### <a name="step-34-validate-the-downloaded-package"></a><span data-ttu-id="a87f4-273">3.4단계: 다운로드한 패키지의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="a87f4-273">Step 3.4: Validate the downloaded package</span></span>
<span data-ttu-id="a87f4-274">이 단계는 선택 사항이지만 다음 사항을 확인할 수 있으므로 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-274">This step is optional but recommended so that you can validate the following:</span></span>

* <span data-ttu-id="a87f4-275">도구 집합에 포함된 키 교환 키가 정품 Thales HSM에서 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-275">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="a87f4-276">도구 집합에 포함된 Security World의 해시가 정품 Thales HSM에서 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-276">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="a87f4-277">키 교환 키를 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-277">The Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="a87f4-278">다운로드한 패키지의 유효성을 검사하려면 HSM이 연결되고 전원이 켜져 있어야 하며 그 안에 지금 만든 것 같은 보안 영역이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-278">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span></span>
>
>

<span data-ttu-id="a87f4-279">다운로드한 패키지의 유효성을 검사하려면:</span><span class="sxs-lookup"><span data-stu-id="a87f4-279">To validate the downloaded package:</span></span>

1. <span data-ttu-id="a87f4-280">해당하는 지리적 지역 또는 Azure 인스턴스에 따라 다음 중 하나를 입력하여 verifykeypackage.py 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-280">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="a87f4-281">북아메리카:</span><span class="sxs-lookup"><span data-stu-id="a87f4-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="a87f4-282">유럽:</span><span class="sxs-lookup"><span data-stu-id="a87f4-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="a87f4-283">아시아:</span><span class="sxs-lookup"><span data-stu-id="a87f4-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="a87f4-284">라틴 아메리카:</span><span class="sxs-lookup"><span data-stu-id="a87f4-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="a87f4-285">일본:</span><span class="sxs-lookup"><span data-stu-id="a87f4-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="a87f4-286">한국:</span><span class="sxs-lookup"><span data-stu-id="a87f4-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="a87f4-287">오스트레일리아:</span><span class="sxs-lookup"><span data-stu-id="a87f4-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="a87f4-288">[Azure Government](https://azure.microsoft.com/features/gov/)(Azure의 미국 정부 인스턴스 사용):</span><span class="sxs-lookup"><span data-stu-id="a87f4-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="a87f4-289">미국 정부 DOD:</span><span class="sxs-lookup"><span data-stu-id="a87f4-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="a87f4-290">캐나다:</span><span class="sxs-lookup"><span data-stu-id="a87f4-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="a87f4-291">독일:</span><span class="sxs-lookup"><span data-stu-id="a87f4-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="a87f4-292">인도:</span><span class="sxs-lookup"><span data-stu-id="a87f4-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="a87f4-293">Thales 소프트웨어에는 %NFAST_HOME%\python\bin에 python이 포함되어 있습니다. </span><span class="sxs-lookup"><span data-stu-id="a87f4-293">The Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="a87f4-294">다음 내용이 표시되는지 확인합니다. 이는 유효성 검사가 성공했다는 것입니다. **Result: SUCCESS**</span><span class="sxs-lookup"><span data-stu-id="a87f4-294">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="a87f4-295">이 스크립트는 서명자 체인의 유효성을 Thales 루트 키까지 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-295">This script validates the signer chain up to the Thales root key.</span></span> <span data-ttu-id="a87f4-296">이 루트 키의 해시는 스크립트에 포함되어 있으며 해당 값은 **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-296">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="a87f4-297">[Thales 웹 사이트](http://www.thalesesec.com/)에서 이 값을 개별적으로 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-297">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="a87f4-298">이제 새 키를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-298">You’re now ready to create a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="a87f4-299">3.5단계: 새 키 만들기</span><span class="sxs-lookup"><span data-stu-id="a87f4-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="a87f4-300">Thales **generatekey** 프로그램을 사용하여 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-300">Generate a key by using the Thales **generatekey** program.</span></span>

<span data-ttu-id="a87f4-301">다음 명령을 실행하여 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-301">Run the following command to generate the key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="a87f4-302">이 명령을 실행할 때 다음 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="a87f4-303">매개 변수 *보호* 는 다음과 같이 값 **모듈**에 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-303">The parameter *protect* must be set to the value **module**, as shown.</span></span> <span data-ttu-id="a87f4-304">이렇게 하면 모듈 보호 키가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-304">This creates a module-protected key.</span></span> <span data-ttu-id="a87f4-305">BYOK 도구 집합은 OCS 보호 키를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-305">The BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="a87f4-306">**ident** 및 **plainname**의 *contosokey* 값을 임의의 문자열 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-306">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="a87f4-307">관리 오버헤드를 최소화하고 오류 위험성을 줄이려면 두 가지에 동일한 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-307">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span></span> <span data-ttu-id="a87f4-308">**ident** 값은 숫자, 대시 및 소문자만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-308">The **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="a87f4-309">pubexp는 이 예에서 비어 있지만(기본값) 특정 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-309">The pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="a87f4-310">자세한 내용은 Thales 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-310">For more information, see the Thales documentation.</span></span>

<span data-ttu-id="a87f4-311">이 명령은 %NFAST_KMDATA%\local 폴더에 토큰화된 키 파일을 만듭니다. 이 파일은 이름이 **key_simple_**로 시작하며 명령에서 지정한 **ident**가 뒤에 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span></span> <span data-ttu-id="a87f4-312">예들 들어 **key_simple_contosokey**입니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="a87f4-313">이 파일은 암호화된 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="a87f4-314">안전한 위치에 이 토큰화된 키 파일을 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a87f4-315">나중에 Azure 주요 자격 증명 모음에 키를 전송하는 경우 Microsoft에서는 이 키를 사용자에게 다시 내보낼 수 없으므로 키 및 보안 영역을 안전하게 백업하는 것이 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-315">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="a87f4-316">키 백업에 대한 지침 및 모범 사례는 Thales에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="a87f4-317">이제 Azure 주요 자격 증명 모음에 키를 전송할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-317">You are now ready to transfer your key to Azure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="a87f4-318">4단계: 전송할 키 준비</span><span class="sxs-lookup"><span data-stu-id="a87f4-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="a87f4-319">이 4단계에서는 연결이 끊어진 워크스테이션에서 다음 절차를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-319">For this fourth step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="a87f4-320">4.1단계: 축소된 권한을 가진 키의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="a87f4-321">새 명령 프롬프트를 열고 현재 디렉터리를 BYOK zip 파일의 압축이 풀린 위치로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-321">Open a new command prompt and change the current directory to the location where you unzipped the BYOK zip file.</span></span> <span data-ttu-id="a87f4-322">키에 대한 권한을 축소하려면 명령 프롬프트에서 해당 지리적 지역 또는 Azure 인스턴스에 따라 다음 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-322">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="a87f4-323">북아메리카:</span><span class="sxs-lookup"><span data-stu-id="a87f4-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="a87f4-324">유럽:</span><span class="sxs-lookup"><span data-stu-id="a87f4-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="a87f4-325">아시아:</span><span class="sxs-lookup"><span data-stu-id="a87f4-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="a87f4-326">라틴 아메리카:</span><span class="sxs-lookup"><span data-stu-id="a87f4-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="a87f4-327">일본:</span><span class="sxs-lookup"><span data-stu-id="a87f4-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="a87f4-328">한국:</span><span class="sxs-lookup"><span data-stu-id="a87f4-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="a87f4-329">오스트레일리아:</span><span class="sxs-lookup"><span data-stu-id="a87f4-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="a87f4-330">[Azure Government](https://azure.microsoft.com/features/gov/)(Azure의 미국 정부 인스턴스 사용):</span><span class="sxs-lookup"><span data-stu-id="a87f4-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="a87f4-331">미국 정부 DOD:</span><span class="sxs-lookup"><span data-stu-id="a87f4-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="a87f4-332">캐나다:</span><span class="sxs-lookup"><span data-stu-id="a87f4-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="a87f4-333">독일:</span><span class="sxs-lookup"><span data-stu-id="a87f4-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="a87f4-334">인도:</span><span class="sxs-lookup"><span data-stu-id="a87f4-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="a87f4-335">이 명령을 실행할 때 [키 생성](#step-3-generate-your-key) 단계의 **3.5단계: 새 키 만들기**에서 지정한 값과 동일한 값으로 *contosokey*를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-335">When you run this command, replace *contosokey* with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="a87f4-336">보안 영역 관리자 카드를 플러그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-336">You are asked to plug in your security world admin cards.</span></span>

<span data-ttu-id="a87f4-337">명령이 완료되면 **Result: SUCCESS**가 표시되고 축소된 권한을 가진 키 복사본이 key_xferacId_<contosokey>라는 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-337">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="a87f4-338">Thales 유틸리티에서 다음 명령을 사용하여 ACL을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-338">You may inspects the ACLS using following commands using the Thales utilities:</span></span>

* <span data-ttu-id="a87f4-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="a87f4-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="a87f4-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="a87f4-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="a87f4-341">이러한 명령을 실행할 때 [키 생성](#step-3-generate-your-key) 단계의 **3.5단계: 새 키 만들기**에서 지정한 값과 동일한 값으로 contosokey를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-341">When you run these commands, replace contosokey with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="a87f4-342">4.2단계: Microsoft의 키 교환 키를 사용하여 키 암호화</span><span class="sxs-lookup"><span data-stu-id="a87f4-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="a87f4-343">지리적 지역 또는 Azure의 인스턴스에 따라 다음 명령 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-343">Run one of the following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="a87f4-344">북아메리카:</span><span class="sxs-lookup"><span data-stu-id="a87f4-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-345">유럽:</span><span class="sxs-lookup"><span data-stu-id="a87f4-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-346">아시아:</span><span class="sxs-lookup"><span data-stu-id="a87f4-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-347">라틴 아메리카:</span><span class="sxs-lookup"><span data-stu-id="a87f4-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-348">일본:</span><span class="sxs-lookup"><span data-stu-id="a87f4-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-349">한국:</span><span class="sxs-lookup"><span data-stu-id="a87f4-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-350">오스트레일리아:</span><span class="sxs-lookup"><span data-stu-id="a87f4-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-351">[Azure Government](https://azure.microsoft.com/features/gov/)(Azure의 미국 정부 인스턴스 사용):</span><span class="sxs-lookup"><span data-stu-id="a87f4-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-352">미국 정부 DOD:</span><span class="sxs-lookup"><span data-stu-id="a87f4-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-353">캐나다:</span><span class="sxs-lookup"><span data-stu-id="a87f4-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-354">독일:</span><span class="sxs-lookup"><span data-stu-id="a87f4-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="a87f4-355">인도:</span><span class="sxs-lookup"><span data-stu-id="a87f4-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="a87f4-356">이 명령을 실행할 때 다음 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="a87f4-357">[키 생성](#step-3-generate-your-key) 단계의 **3.5단계: 새 키 만들기**에서 키를 생성하기 위해 사용한 식별자로 *contosokey*를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-357">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="a87f4-358">*SubscriptionID* 를 주요 자격 증명 모음이 포함된 Azure 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-358">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span></span> <span data-ttu-id="a87f4-359">**인터넷에 연결된 워크스테이션 준비** 단계의 [1.2단계: Azure 구독 ID 가져오기](#step-1-prepare-your-internet-connected-workstation) 에서 이 값을 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="a87f4-360">*ContosoFirstHSMKey*를 출력 파일 이름에 사용할 레이블로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="a87f4-361">이 작업이 성공적으로 완료되면 **Result: SUCCESS**가 표시되고 현재 폴더에 KeyTransferPackage-*ContosoFirstHSMkey*.byok라는 이름의 새 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-to-the-internet-connected-workstation"></a><span data-ttu-id="a87f4-362">4.3단계: 인터넷에 연결된 워크스테이션에 키 전송 패키지 복사</span><span class="sxs-lookup"><span data-stu-id="a87f4-362">Step 4.3: Copy your key transfer package to the Internet-connected workstation</span></span>
<span data-ttu-id="a87f4-363">USB 드라이브 또는 기타 휴대용 저장소를 사용하여 인터넷에 연결된 워크스테이션에 이전 단계의 출력 파일(KeyTransferPackage-ContosoFirstHSMkey.byok)을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-363">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-to-azure-key-vault"></a><span data-ttu-id="a87f4-364">5단계: Azure 주요 자격 증명 모음에 키 전송</span><span class="sxs-lookup"><span data-stu-id="a87f4-364">Step 5: Transfer your key to Azure Key Vault</span></span>
<span data-ttu-id="a87f4-365">이 마지막 단계에서는 인터넷에 연결된 워크스테이션에서 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet을 사용하여 연결이 끊어진 워크스테이션에서 Azure Key Vault HSM으로 복사한 키 전송 패키지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-365">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="a87f4-366">업로드가 성공하면 방금 추가한 키의 속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-366">If the upload is successful, you see displayed the properties of the key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a87f4-367">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a87f4-367">Next steps</span></span>
<span data-ttu-id="a87f4-368">이제 주요 자격 증명 모음에서 이 HSM 보호된 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a87f4-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="a87f4-369">자세한 내용은 **Azure 주요 자격 증명 모음 시작** 자습서에서 [HSM(하드웨어 보안 모듈)을 사용하려는 경우](key-vault-get-started.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a87f4-369">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
