---
title: "aaaHow toogenerate 및 전송 HSM 보호 키 Azure 키 자격 증명 모음에 대 한 | Microsoft Docs"
description: "이 문서 toohelp 계획을 생성 및 다음 Azure 키 자격 증명 모음 HSM 보호 키 toouse 직접 전송 사용 합니다. BYOK, 즉 Bring Your Own Key라고도 합니다."
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
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="63ea5-104">어떻게 toogenerate 및 전송 HSM 보호 키를 Azure 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="63ea5-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="63ea5-105">소개</span><span class="sxs-lookup"><span data-stu-id="63ea5-105">Introduction</span></span>
<span data-ttu-id="63ea5-106">추가 된 보증에 대 한 Azure 키 자격 증명 모음을 사용 하는 경우 수 가져오거나 hello HSM 경계를 벗어날 하드웨어 보안 모듈 (Hsm)의 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="63ea5-107">이 시나리오는 종종 참조 tooas *고유한 키를 가져올*, byok 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="63ea5-108">hello Hsm은 FIPS 140-2 수준 2 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="63ea5-109">Azure 키 자격 증명 모음은 Thales nShield Hsm tooprotect 제품군 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="63ea5-110">이 항목 toohelp 계획을 생성 및 다음 Azure 키 자격 증명 모음 HSM 보호 키 toouse 직접 전송의 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="63ea5-111">이 기능은 Azure 중국에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="63ea5-112">Azure 주요 자격 증명 모음에 대한 자세한 내용은 [Azure 주요 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="63ea5-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="63ea5-113">HSM 보호된 키를 위해 주요 자격 증명 모음 만들기가 포함된 자습서를 시작하려면 [Azure 주요 자격 증명 모음 시작](key-vault-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63ea5-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="63ea5-114">생성 하 고 hello 인터넷을 통해 HSM 보호 키를 전송 하는 방법에 대 한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="63ea5-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="63ea5-115">Hello 공격 노출 영역을 줄일 수 있는 오프 라인 워크스테이션에서 hello 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="63ea5-116">hello 키와는 키 KEK (키 교환), 암호화 상태를 유지 전송된 toohello Azure 키 자격 증명 모음 Hsm 될 때까지 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="63ea5-117">키의 암호화 된 버전 hello만 hello 원래 워크스테이션을 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="63ea5-118">hello 도구 집합 키 toohello Azure 키 자격 증명 모음 보안 권역에 바인딩하는 테 넌 트 키에 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="63ea5-119">따라서 후 hello Azure 키 자격 증명 모음 Hsm를 받아 암호를 해독 키만 이러한 Hsm 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="63ea5-120">키는 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-120">Your key cannot be exported.</span></span> <span data-ttu-id="63ea5-121">이 바인딩은 Thales Hsm hello로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="63ea5-122">hello 키 교환 KEK (키)를 사용 하는 tooencrypt 키 hello Azure 키 자격 증명 모음 Hsm 내부에서 생성 되며 되며 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="63ea5-123">hello Hsm 적용 hello Hsm 외부 hello KEK의 일반 버전이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="63ea5-124">또한 hello 도구 집합 되지 하 고 KEK가 Thales에서 제조한 정품 HSM 내부에서 생성 하는 hello 나타내는 Thales 로부터의 증명이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="63ea5-125">hello 도구 집합에는 Azure 키 자격 증명 모음 보안 권역도 Thales에서 제조한 정품 HSM에서 생성 하는 hello 나타내는 Thales 로부터의 증명이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="63ea5-126">이 증명 증명 tooyou는 Microsoft가 정품 하드웨어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="63ea5-127">Microsoft는 각 지역별로 별도의 보안 권역과 별도의 KEK를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="63ea5-128">이러한 분리는 암호화 된 hello 지역의 데이터 센터 에서만에서 키를 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="63ea5-129">예를 들어 유럽 고객의 키는 북아메리카 또는 아시아의 데이터 센터에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="63ea5-130">Thales HSM 및 Microsoft 서비스에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="63ea5-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="63ea5-131">Thales e-보안은 데이터 암호화 및 사이버 보안 솔루션 toohello 금융 서비스, 첨단 기술, 제조, 정부 및 기술 부문에는 선도적인 글로벌 기업입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="63ea5-132">40 년 역사가 보호 회사 및 정부 정보를 Thales 솔루션은 hello 5 명의 가장 큰 에너지 및 항공 우주 회사의 4/에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="63ea5-133">또한 22개 NATO 국가에서 사용되고 있으며 전세계 지불 거래의 80퍼센트 이상의 보안을 담당하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="63ea5-134">Microsoft는 Hsm에 대 한 아트 Thales tooenhance hello 상태와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="63ea5-135">이러한 향상 된이 기능을 사용 하면 tooget hello 프로그램은 키에 대 한 제어권을 포기 하지 않고 호스팅된 서비스의 일반적인 이점을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="63ea5-136">특히, 이러한 향상 된 고객이 Microsoft가를 보유 하지 않는 hello Hsm을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="63ea5-137">클라우드 서비스, Azure 주요 자격 증명 모음 없이 소집 toomeet 수직 확장로 조직의 사용 급증 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="63ea5-138">At hello 동일 time, Microsoft Hsm 내부에서 사용자의 키 보호 됩니다: hello 키를 생성 하 고 tooMicrosoft의 Hsm을 전송 했으므로 hello 키 수명 주기에 대 한 제어권을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="63ea5-139">Azure 주요 자격 증명 모음에 대한 BYOK(Bring Your Own Key) 구현</span><span class="sxs-lookup"><span data-stu-id="63ea5-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="63ea5-140">사용 하 여 hello HSM 보호 키 생성 되며, 주요 자격 증명 모음 tooAzure 전송 하는 경우 정보 및 절차를 따라-hello bring 키 (BYOK) 하는 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="63ea5-141">BYOK에 대한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="63ea5-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="63ea5-142">다음 표를 위한 필수 구성 요소의 목록에 대 한 hello (byok)를 통해 Azure 키 자격 증명 모음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="63ea5-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="63ea5-143">요구 사항</span><span class="sxs-lookup"><span data-stu-id="63ea5-143">Requirement</span></span> | <span data-ttu-id="63ea5-144">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="63ea5-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="63ea5-145">구독 tooAzure</span><span class="sxs-lookup"><span data-stu-id="63ea5-145">A subscription tooAzure</span></span> |<span data-ttu-id="63ea5-146">Azure 구독이 필요 toocreate Azure 키 자격 증명 모음: [무료 평가판에 등록](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="63ea5-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="63ea5-147">hello Azure 키 자격 증명 모음 Premium 서비스 계층 toosupport HSM 보호 키</span><span class="sxs-lookup"><span data-stu-id="63ea5-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="63ea5-148">Azure 키 자격 증명 모음에 대 한 hello 서비스 계층과 기능에 대 한 자세한 내용은 참조 hello [Azure 키 자격 증명 모음 가격](https://azure.microsoft.com/pricing/details/key-vault/) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="63ea5-149">Thales HSM, 스마트 카드 및 지원 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="63ea5-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="63ea5-150">있어야 tooa Thales 하드웨어 보안 모듈 및 Thales Hsm의 기본적인 작동 지식이 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="63ea5-151">참조 [Thales 하드웨어 보안 모듈](https://www.thales-esecurity.com/msrms/buy) 호환 모델 또는 toopurchase 하지 않은 경우 하나 HSM hello 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="63ea5-152">다음 하드웨어 및 소프트웨어 hello:</span><span class="sxs-lookup"><span data-stu-id="63ea5-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="63ea5-153">Windows 운영 체제 Windows 7 이상 및 Thales nShield 소프트웨어 버전 11.50 이상이 설치된 오프라인 x64 워크스테이션.</span><span class="sxs-lookup"><span data-stu-id="63ea5-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="63ea5-154">이 워크스테이션에서 Windows 7을 실행하는 경우 [Microsoft.NET Framework 4.5를 설치](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="63ea5-155">연결 된 toohello 인터넷 이며 최소 Windows 운영 체제의 Windows 7 인 워크스테이션 및 [Azure PowerShell](/powershell/azure/overview) **최소 버전 1.1.0** 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="63ea5-156">여유 공간이 16MB 이상인 USB 드라이브 또는 기타 휴대용 저장 장치 </span><span class="sxs-lookup"><span data-stu-id="63ea5-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="63ea5-157">보안상의 이유로 hello 첫 번째 워크스테이션의 연결 된 tooa 네트워크 않습니다 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="63ea5-158">그러나 이 권고는 프로그램 방식으로 강제 적용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="63ea5-159">뒤에 나오는 hello 지침에서이 워크스테이션은 참조 tooas hello 연결이 끊어진 워크스테이션 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="63ea5-160">또한 테 넌 트 키가 프로덕션 네트워크용, 별도 두 번째 워크스테이션 toodownload hello 도구 집합 및 업로드 hello 테 넌 트 키를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="63ea5-161">테스트를 위해 사용할 수 있습니다 하지만 첫 번째 hello 처럼 동일한 워크스테이션을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="63ea5-162">뒤에 나오는 hello 지침에서이 두 번째 워크스테이션은 참조 tooas hello 인터넷에 연결 된 워크스테이션 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="63ea5-163">생성 및 사용자 키 tooAzure 자격 증명 모음 HSM 키를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="63ea5-164">5 단계 toogenerate 다음 hello를 사용 하 고 키 tooan Azure 키 자격 증명 모음 HSM에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="63ea5-165">1단계: 인터넷에 연결된 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="63ea5-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="63ea5-166">2단계: 연결이 끊어진 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="63ea5-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="63ea5-167">3단계: 키 생성</span><span class="sxs-lookup"><span data-stu-id="63ea5-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="63ea5-168">4단계: 전송할 키 준비</span><span class="sxs-lookup"><span data-stu-id="63ea5-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="63ea5-169">5 단계: 키 자격 증명 모음에 키 tooAzure 전송</span><span class="sxs-lookup"><span data-stu-id="63ea5-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="63ea5-170">1단계: 인터넷에 연결된 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="63ea5-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="63ea5-171">이 첫 번째 단계 수행 hello 있는 연결 된 toohello 인터넷 워크스테이션에서 다음 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="63ea5-172">1.1단계: Azure PowerShell 설치</span><span class="sxs-lookup"><span data-stu-id="63ea5-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="63ea5-173">Hello 인터넷에 연결 된 워크스테이션에서 다운로드 하 고 hello cmdlet toomanage Azure 키 자격 증명 모음을 포함 하는 hello Azure PowerShell 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="63ea5-174">이를 위해 0.8.13 이상 버전이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="63ea5-175">설치 지침을 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="63ea5-176">1.2단계: Azure 구독 ID 얻기</span><span class="sxs-lookup"><span data-stu-id="63ea5-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="63ea5-177">Azure PowerShell 세션을 시작 하 고 다음 명령을 hello를 사용 하 여 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="63ea5-178">Hello 팝업 브라우저 창에서 Azure 계정 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="63ea5-179">그런 다음 사용 하는 hello [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) 명령:</span><span class="sxs-lookup"><span data-stu-id="63ea5-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="63ea5-180">Hello 출력에서 Azure 키 자격 증명 모음에 사용할 hello 구독에 대 한 hello ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="63ea5-181">이 구독 ID는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="63ea5-182">Hello Azure PowerShell 창을 닫지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="63ea5-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="63ea5-183">1.3 단계: Azure 키 자격 증명 모음에 대 한 hello BYOK 도구 집합 다운로드</span><span class="sxs-lookup"><span data-stu-id="63ea5-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="63ea5-184">Microsoft 다운로드 센터 toohello 이동 및 [hello Azure 키 자격 증명 모음 BYOK 도구 집합 다운로드](http://www.microsoft.com/download/details.aspx?id=45345) 지역 또는 Azure의 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="63ea5-185">Hello 다음을 사용 하 여 정보 tooidentify hello 패키지 이름 toodownload 및 해당 해당 s h A-256 패키지 해시:</span><span class="sxs-lookup"><span data-stu-id="63ea5-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="63ea5-186">**미국:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-186">**United States:**</span></span>

<span data-ttu-id="63ea5-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="63ea5-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="63ea5-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="63ea5-189">**유럽:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-189">**Europe:**</span></span>

<span data-ttu-id="63ea5-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="63ea5-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="63ea5-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="63ea5-192">**아시아:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-192">**Asia:**</span></span>

<span data-ttu-id="63ea5-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="63ea5-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="63ea5-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="63ea5-195">**라틴 아메리카:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-195">**Latin America:**</span></span>

<span data-ttu-id="63ea5-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="63ea5-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="63ea5-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="63ea5-198">**일본:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-198">**Japan:**</span></span>

<span data-ttu-id="63ea5-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="63ea5-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="63ea5-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="63ea5-201">**한국:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-201">**Korea:**</span></span>

<span data-ttu-id="63ea5-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="63ea5-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="63ea5-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="63ea5-204">**오스트레일리아:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-204">**Australia:**</span></span>

<span data-ttu-id="63ea5-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="63ea5-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="63ea5-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="63ea5-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="63ea5-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="63ea5-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="63ea5-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="63ea5-210">**미국 정부 DOD:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-210">**US Government DOD:**</span></span>

<span data-ttu-id="63ea5-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="63ea5-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="63ea5-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="63ea5-213">**캐나다:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-213">**Canada:**</span></span>

<span data-ttu-id="63ea5-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="63ea5-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="63ea5-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="63ea5-216">**독일:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-216">**Germany:**</span></span>

<span data-ttu-id="63ea5-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="63ea5-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="63ea5-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="63ea5-219">**인도:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-219">**India:**</span></span>

<span data-ttu-id="63ea5-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="63ea5-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="63ea5-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="63ea5-222">**영국:**</span><span class="sxs-lookup"><span data-stu-id="63ea5-222">**United Kingdom:**</span></span>

<span data-ttu-id="63ea5-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="63ea5-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="63ea5-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="63ea5-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="63ea5-225">Azure PowerShell 세션을 사용 하 여 hello에서 프로그램 다운로드 한 BYOK 도구 집합의 toovalidate hello 무결성 [Get-filehash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="63ea5-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="63ea5-226">hello 도구 집합 hello 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="63ea5-227">이름이 **BYOK-KEK-pkg-**</span><span class="sxs-lookup"><span data-stu-id="63ea5-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="63ea5-228">이름이 **BYOK-SecurityWorld-pkg-**</span><span class="sxs-lookup"><span data-stu-id="63ea5-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="63ea5-229">이름이 **verifykeypackage.py**인 python 스크립트</span><span class="sxs-lookup"><span data-stu-id="63ea5-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="63ea5-230">이름이 **KeyTransferRemote.exe** 인 명령줄 실행 파일 및 관련 DLL</span><span class="sxs-lookup"><span data-stu-id="63ea5-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="63ea5-231">이름이 **vcredist_x64.exe**인 Visual C++ 재배포 가능 패키지</span><span class="sxs-lookup"><span data-stu-id="63ea5-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="63ea5-232">Hello 패키지 tooa USB 드라이브 또는 기타 휴대용 저장소에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="63ea5-233">2단계: 연결이 끊어진 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="63ea5-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="63ea5-234">이 두 번째 단계에 대 한 않습니다 hello (hello 인터넷 또는 내부 네트워크) 연결 된 tooa 네트워크 하지 않은 hello 워크스테이션에서 다음 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="63ea5-235">2.1 단계: Thales HSM에 hello 연결이 끊어진 워크스테이션 준비</span><span class="sxs-lookup"><span data-stu-id="63ea5-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="63ea5-236">Windows 컴퓨터에 hello nCipher (Thales) 지원 소프트웨어를 설치 하 고 Thales HSM toothat 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="63ea5-237">Thales 도구 hello 해당 경로에 있는지 확인 하십시오 (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="63ea5-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="63ea5-238">예를 들어 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="63ea5-239">자세한 내용은 hello Thales HSM에 포함 된 hello 사용자 가이드를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="63ea5-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="63ea5-240">2.2 단계: 설치 hello BYOK 도구 집합 hello 연결이 끊어진 워크스테이션에서</span><span class="sxs-lookup"><span data-stu-id="63ea5-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="63ea5-241">Hello USB 드라이브 또는 기타 휴대용 저장소에서 hello BYOK 도구 집합 패키지를 복사 하 고 수행가 다음를 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="63ea5-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="63ea5-242">Hello 다운로드 패키지에서 임의 폴더로 hello 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="63ea5-243">해당 폴더에서 vcredist_x64.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="63ea5-244">Visual Studio 2013 용 hello Visual c + + 런타임 구성 요소를 설치 하는 toohello hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="63ea5-245">3단계: 키 생성</span><span class="sxs-lookup"><span data-stu-id="63ea5-245">Step 3: Generate your key</span></span>
<span data-ttu-id="63ea5-246">이 세 번째 단계에 대해 수행 hello hello 연결이 끊어진 워크스테이션에서 다음 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="63ea5-247">toocomplete이이 단계 HSM 초기화 모드에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="63ea5-248">3.1 단계: hello HSM 모드 too'I 변경 '</span><span class="sxs-lookup"><span data-stu-id="63ea5-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="63ea5-249">Thales nShield 경계 면 toochange hello 모드를 사용 하는 경우: 1입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="63ea5-250">Hello 모드 단추 toohighlight hello 필요한 모드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="63ea5-251">2.</span><span class="sxs-lookup"><span data-stu-id="63ea5-251">2.</span></span> <span data-ttu-id="63ea5-252">몇 초 안에 hello 지우기 단추를 누르고 몇 초 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="63ea5-253">Hello 모드 변경 되 면 hello 새로운 모드 LED 깜박임 멈추고 켜져 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="63ea5-254">hello 상태 LED 몇 초간 불규칙 한 플래시 수 및 다음 hello 장치를 준비 하는 경우에 정기적으로 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="63ea5-255">그렇지 않으면 hello 장치 남아 있으며 hello 적절 한 모드 LED hello 현재 모드 켜 졌습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="63ea5-256">3.2단계: 보안 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="63ea5-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="63ea5-257">명령 프롬프트를 시작 하 고 hello Thales new-world 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="63ea5-258">이 프로그램을 만듭니다는 **보안 권역** % NFAST_KMDATA%\local\world toohello C:\ProgramData\nCipher\Key Management Data\local 폴더에 해당 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="63ea5-259">Hello 쿼럼에 대 한 다른 값을 사용할 수 있습니다 하는데이 예제에서는 있습니다 증명된 tooenter 3 개의 빈 카드와 핀 각각에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="63ea5-260">그런 다음 임의의 두 카드에 대 한 모든 권한을 toohello 보안 권역을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="63ea5-261">이러한 카드 될 hello **관리자 카드 집합** hello 새 보안 권역의 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="63ea5-262">그런 다음 않습니다 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="63ea5-262">Then do hello following:</span></span>

* <span data-ttu-id="63ea5-263">Hello world 파일을 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-263">Back up hello world file.</span></span> <span data-ttu-id="63ea5-264">보안을 설정 하 고 hello world 파일, hello 관리자 카드 및 해당 핀을 보호 한 사람이 액세스 toomore 보다 카드 하나에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="63ea5-265">3.3 단계: hello HSM 모드 too'O 변경 '</span><span class="sxs-lookup"><span data-stu-id="63ea5-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="63ea5-266">Thales nShield 경계 면 toochange hello 모드를 사용 하는 경우: 1입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="63ea5-267">Hello 모드 단추 toohighlight hello 필요한 모드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="63ea5-268">2.</span><span class="sxs-lookup"><span data-stu-id="63ea5-268">2.</span></span> <span data-ttu-id="63ea5-269">몇 초 안에 hello 지우기 단추를 누르고 몇 초 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="63ea5-270">Hello 모드 변경 되 면 hello 새로운 모드 LED 깜박임 멈추고 켜져 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="63ea5-271">hello 상태 LED 몇 초간 불규칙 한 플래시 수 및 다음 hello 장치를 준비 하는 경우에 정기적으로 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="63ea5-272">그렇지 않으면 hello 장치 남아 있으며 hello 적절 한 모드 LED hello 현재 모드 켜 졌습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="63ea5-273">3.4 단계: hello 다운로드 한 패키지 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="63ea5-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="63ea5-274">이 단계는 선택 사항 이지만 hello 다음을 확인할 수 있도록 권장.</span><span class="sxs-lookup"><span data-stu-id="63ea5-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="63ea5-275">hello hello 도구 집합에 포함 된 키 교환 키가 정품 Thales HSM에서 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="63ea5-276">hello hello 도구 집합에 포함 된 보안 권역의 hello 해시가 정품 Thales HSM에서 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="63ea5-277">hello 키 교환 키를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="63ea5-278">toovalidate hello 패키지를 다운로드 한, hello HSM 연결 되어 있어야, 전원이 켜져 방금 만든 하나 hello) (예: 보안 권역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="63ea5-279">toovalidate hello 다운로드 한 패키지:</span><span class="sxs-lookup"><span data-stu-id="63ea5-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="63ea5-280">Azure의 인스턴스 나 지리적 지역에 따라 hello 다음 중 하나를 입력 하 여 hello verifykeypackage.py 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="63ea5-281">북아메리카:</span><span class="sxs-lookup"><span data-stu-id="63ea5-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="63ea5-282">유럽:</span><span class="sxs-lookup"><span data-stu-id="63ea5-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="63ea5-283">아시아:</span><span class="sxs-lookup"><span data-stu-id="63ea5-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="63ea5-284">라틴 아메리카:</span><span class="sxs-lookup"><span data-stu-id="63ea5-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="63ea5-285">일본:</span><span class="sxs-lookup"><span data-stu-id="63ea5-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="63ea5-286">한국:</span><span class="sxs-lookup"><span data-stu-id="63ea5-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="63ea5-287">오스트레일리아:</span><span class="sxs-lookup"><span data-stu-id="63ea5-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="63ea5-288">에 대 한 [Azure Government](https://azure.microsoft.com/features/gov/), Azure의 hello 미국 정부 인스턴스를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="63ea5-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="63ea5-289">미국 정부 DOD:</span><span class="sxs-lookup"><span data-stu-id="63ea5-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="63ea5-290">캐나다:</span><span class="sxs-lookup"><span data-stu-id="63ea5-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="63ea5-291">독일:</span><span class="sxs-lookup"><span data-stu-id="63ea5-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="63ea5-292">인도:</span><span class="sxs-lookup"><span data-stu-id="63ea5-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="63ea5-293">hello Thales 소프트웨어는 %NFAST_HOME%\python\bin에 python 포함</span><span class="sxs-lookup"><span data-stu-id="63ea5-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="63ea5-294">유효성 검사 성공을 나타냄 hello 다음 표시 되는지 확인 합니다: **결과: 성공**</span><span class="sxs-lookup"><span data-stu-id="63ea5-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="63ea5-295">이 스크립트에는 toohello Thales 루트 키를 hello 서명자 체 이닝 되는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="63ea5-296">이 루트 키의 해시 hello hello 스크립트에 포함 되어 있으며 해당 값 **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="63ea5-297">Hello를 방문 하 여이 값을 개별적으로 확인할 수도 있습니다 [Thales 웹 사이트](http://www.thalesesec.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="63ea5-298">이제 새 키를 준비 toocreate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="63ea5-299">3.5단계: 새 키 만들기</span><span class="sxs-lookup"><span data-stu-id="63ea5-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="63ea5-300">Thales hello를 사용 하 여 키를 생성 **generatekey** 프로그램.</span><span class="sxs-lookup"><span data-stu-id="63ea5-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="63ea5-301">다음 명령은 toogenerate hello 키 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="63ea5-302">이 명령을 실행할 때 다음 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="63ea5-303">매개 변수를 hello *보호* toohello 값을 설정 해야 **모듈**표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="63ea5-304">이렇게 하면 모듈 보호 키가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-304">This creates a module-protected key.</span></span> <span data-ttu-id="63ea5-305">hello BYOK 도구 집합 OCS 보호 키는 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="63ea5-306">Hello 값의 대체 *contosokey* hello에 대 한 **ident** 및 **plainname** 임의의 문자열 값으로.</span><span class="sxs-lookup"><span data-stu-id="63ea5-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="63ea5-307">관리 오버 헤드가 toominimize hello 위험을 줄이고 오류의 hello 둘 다에 대해 같은 값을 사용 하는 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="63ea5-308">hello **ident** 값 숫자, 대시 및 소문자만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="63ea5-309">hello pubexp은 비워 뒀 지만 (기본값)이 예제에서는 하지만 특정 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="63ea5-310">자세한 내용은 Thales 문서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="63ea5-311">이 명령은으로 이름을 시작 하 여 %NFAST_KMDATA%\local 폴더에 토큰화 된 키 파일을 만들고 **key_simple_**hello와 **ident** hello 명령에 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="63ea5-312">예들 들어 **key_simple_contosokey**입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="63ea5-313">이 파일은 암호화된 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="63ea5-314">안전한 위치에 이 토큰화된 키 파일을 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63ea5-315">나중에 키 자격 증명 모음에 키 tooAzure를 전송할 때 Microsoft는 것이 매우 중요 한를 백업 하는 키와 보안 권역 안전 하 게이 키 백 tooyou를 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="63ea5-316">키 백업에 대한 지침 및 모범 사례는 Thales에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="63ea5-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="63ea5-317">사용자는 이제 준비 tootransfer 주요 자격 증명 모음에 키 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="63ea5-318">4단계: 전송할 키 준비</span><span class="sxs-lookup"><span data-stu-id="63ea5-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="63ea5-319">이 네 번째 단계에 대해 수행 hello hello 연결이 끊어진 워크스테이션에서 다음 절차를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="63ea5-320">4.1단계: 축소된 권한을 가진 키의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="63ea5-321">새 명령 프롬프트를 열고 hello 현재 디렉터리 toohello 위치 hello BYOK zip 파일의 압축을 푼 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="63ea5-322">명령 프롬프트에서 사용자의 키에 대 한 hello 권한을 tooreduce 인스턴스의 Azure 나 지리적 지역에 따라 hello 다음 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="63ea5-323">북아메리카:</span><span class="sxs-lookup"><span data-stu-id="63ea5-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="63ea5-324">유럽:</span><span class="sxs-lookup"><span data-stu-id="63ea5-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="63ea5-325">아시아:</span><span class="sxs-lookup"><span data-stu-id="63ea5-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="63ea5-326">라틴 아메리카:</span><span class="sxs-lookup"><span data-stu-id="63ea5-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="63ea5-327">일본:</span><span class="sxs-lookup"><span data-stu-id="63ea5-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="63ea5-328">한국:</span><span class="sxs-lookup"><span data-stu-id="63ea5-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="63ea5-329">오스트레일리아:</span><span class="sxs-lookup"><span data-stu-id="63ea5-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="63ea5-330">에 대 한 [Azure Government](https://azure.microsoft.com/features/gov/), Azure의 hello 미국 정부 인스턴스를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="63ea5-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="63ea5-331">미국 정부 DOD:</span><span class="sxs-lookup"><span data-stu-id="63ea5-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="63ea5-332">캐나다:</span><span class="sxs-lookup"><span data-stu-id="63ea5-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="63ea5-333">독일:</span><span class="sxs-lookup"><span data-stu-id="63ea5-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="63ea5-334">인도:</span><span class="sxs-lookup"><span data-stu-id="63ea5-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="63ea5-335">이 명령을 실행할 때 *contosokey* hello와 같은 값에서 지정한 **단계 3.5: 새 키 만들기** hello에서 [트 키 생성](#step-3-generate-your-key) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="63ea5-336">사용자 보안 권역 관리자 카드에서 tooplug는 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="63ea5-337">Hello 명령이 완료 되 면 표시 **결과: SUCCESS** 있으며 권한이 낮춰 키의 hello 복사본이 key_xferacId_ 라는 hello 파일에서<contosokey>합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="63ea5-338">Hello ACL 검사 수 Thales 유틸리티를 hello 다음 명령을 사용 하 여 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="63ea5-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="63ea5-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="63ea5-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="63ea5-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="63ea5-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="63ea5-341">이러한 명령을 실행할 때 contosokey hello에 지정한 같은 값으로 대체 **단계 3.5: 새 키 만들기** hello에서 [트 키 생성](#step-3-generate-your-key) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="63ea5-342">4.2단계: Microsoft의 키 교환 키를 사용하여 키 암호화</span><span class="sxs-lookup"><span data-stu-id="63ea5-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="63ea5-343">Hello 명령을 Azure 인스턴스의 나 지리적 지역에 따라 다음 중 하나를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="63ea5-344">북아메리카:</span><span class="sxs-lookup"><span data-stu-id="63ea5-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-345">유럽:</span><span class="sxs-lookup"><span data-stu-id="63ea5-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-346">아시아:</span><span class="sxs-lookup"><span data-stu-id="63ea5-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-347">라틴 아메리카:</span><span class="sxs-lookup"><span data-stu-id="63ea5-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-348">일본:</span><span class="sxs-lookup"><span data-stu-id="63ea5-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-349">한국:</span><span class="sxs-lookup"><span data-stu-id="63ea5-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-350">오스트레일리아:</span><span class="sxs-lookup"><span data-stu-id="63ea5-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-351">에 대 한 [Azure Government](https://azure.microsoft.com/features/gov/), Azure의 hello 미국 정부 인스턴스를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="63ea5-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-352">미국 정부 DOD:</span><span class="sxs-lookup"><span data-stu-id="63ea5-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-353">캐나다:</span><span class="sxs-lookup"><span data-stu-id="63ea5-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-354">독일:</span><span class="sxs-lookup"><span data-stu-id="63ea5-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="63ea5-355">인도:</span><span class="sxs-lookup"><span data-stu-id="63ea5-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="63ea5-356">이 명령을 실행할 때 다음 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="63ea5-357">대체 *contosokey* 에 toogenerate hello 키를 사용 하는 hello 식별자를 가진 **단계 3.5: 새 키 만들기** hello에서 [트 키 생성](#step-3-generate-your-key) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="63ea5-358">대체 *SubscriptionID* hello hello 주요 자격 증명 모음을 포함 하는 Azure 구독 ID로 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="63ea5-359">이 값을 검색에서 이전에 **1.2 단계: Azure 구독 ID를 가져올** hello에서 [인터넷에 연결 된 워크스테이션 준비](#step-1-prepare-your-internet-connected-workstation) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="63ea5-360">*ContosoFirstHSMKey*를 출력 파일 이름에 사용할 레이블로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="63ea5-361">이 성공적으로 완료 되 면 표시 **결과: 성공** hello 이름 뒤에 있는 hello 현재 폴더에 새 파일 이며: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="63ea5-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="63ea5-362">4.3 단계: 키 전송 패키지 toohello 인터넷에 연결 된 워크스테이션을 복사</span><span class="sxs-lookup"><span data-stu-id="63ea5-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="63ea5-363">Hello 이전 단계 (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour 인터넷에 연결 된 워크스테이션에서 USB 드라이브 또는 기타 휴대용 저장소 toocopy hello 출력 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="63ea5-364">5 단계: 키 자격 증명 모음에 키 tooAzure 전송</span><span class="sxs-lookup"><span data-stu-id="63ea5-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="63ea5-365">이 마지막 단계에 대 한 hello 인터넷에 연결 된 워크스테이션에서 사용 하 여 hello [Add-azurekeyvaultkey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) hello에서 복사한 cmdlet tooupload hello 키 전송 패키지 끊긴 워크스테이션 toohello Azure 키 자격 증명 모음 HSM:</span><span class="sxs-lookup"><span data-stu-id="63ea5-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="63ea5-366">Hello 업로드에 성공한 경우 방금 추가한 hello 키의 표시 된 hello 속성 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63ea5-367">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63ea5-367">Next steps</span></span>
<span data-ttu-id="63ea5-368">이제 주요 자격 증명 모음에서 이 HSM 보호된 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="63ea5-369">자세한 내용은 참조 hello **toouse 하드웨어 보안 모듈 (HSM) 하려는 경우** hello에 대 한 섹션 [Azure 키 자격 증명 모음 시작 하기](key-vault-get-started.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="63ea5-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
