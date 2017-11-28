---
title: "aaa \"Azure CDN 사용자 지정 도메인에서 HTTPS를 사용 하도록 설정 | \"Microsoft Docs"
description: "자세한 방법을 사용자 지정 도메인을 사용 하 여 Azure CDN 끝점에 HTTPS tooenable 합니다."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="d34b4-103">Azure CDN 사용자 지정 도메인에서 HTTPS를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d34b4-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="d34b4-104">Azure CDN 사용자 지정 도메인에 대 한 HTTPS 지원을 사용 하면 보안 콘텐츠에 대 한 고유한 도메인 이름을 tooimprove hello 데이터의 보안 전송 중에 사용 하 여 SSL 통해 toodeliver 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="d34b4-105">사용자 지정 도메인에 대 한 hello 종단 간 워크플로 tooenable HTTPS를 통해 한 번의 클릭 사용, 전체 인증서 관리 및 추가 비용 없이 포함 된 모두 간소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="d34b4-106">중요 한 tooensure hello 개인 정보 및 전송 중에 웹 응용 프로그램 중요 한 데이터의 모든 데이터 무결성.</span><span class="sxs-lookup"><span data-stu-id="d34b4-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="d34b4-107">인터넷 hello HTTPS 프로토콜을 통해 전송 될 때 중요 한 데이터 암호화는 되도록 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="d34b4-108">신뢰할 수 있는 인증을 제공하며 공격으로부터 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="d34b4-109">현재 Azure CDN은 CDN 끝점에서 HTTPS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="d34b4-110">예를 들어 Azure CDN(예: https://contoso.azureedge.net )에서 CDN 끝점을 만드는 경우 기본적으로 HTTPS가 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="d34b4-111">이제 사용자 지정 도메인 HTTPS를 사용하여 사용자 지정 도메인(예: https://www.contoso.com )에 대해서도 안전한 전달을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="d34b4-112">HTTPS 기능의 hello 키 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="d34b4-113">추가 비용 없음: 인증서 얻기 또는 갱신에 대해 비용이 없으며 HTTPS 트래픽에 대한 추가 비용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="d34b4-114">Hello CDN에서에서 GB 수신을 위해만 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="d34b4-115">간단한 구현 지원: 하나 클릭 하 여 프로 비전 하는 것은 hello에서 사용할 수 있는 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d34b4-116">또한 REST API 또는 다른 개발자 도구 tooenable hello 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="d34b4-117">완전한 인증서 관리: 사용자를 위해 모든 인증서 조달 및 관리가 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="d34b4-118">인증서는 자동으로 프로 비전 하 고 이전 tooexpiration 갱신 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="d34b4-119">이 인증서가 만료 결과로 서비스 중단의 위험 hello 완전히 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="d34b4-120">이전 tooenabling HTTPS를 지원 해야 이미 설정한는 [Azure CDN 사용자 지정 도메인](./cdn-map-content-to-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="d34b4-121">1 단계: hello 기능 활성화</span><span class="sxs-lookup"><span data-stu-id="d34b4-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="d34b4-122">Hello에 [Azure 포털](https://portal.azure.com), tooyour Verizon 표준 또는 프리미엄 CDN 프로필을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="d34b4-123">끝점의 hello 목록에서 사용자 지정 도메인을 포함 하는 hello 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="d34b4-124">HTTPS tooenable 원하는 hello 사용자 지정 도메인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![끝점 블레이드](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="d34b4-126">클릭 **에** tooenable HTTPS hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![사용자 지정 HTTPS 대화 상자](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="d34b4-128">2단계: 도메인 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="d34b4-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="d34b4-129">사용자 지정 도메인에서 HTTPS를 활성화하기 전에 도메인 유효성 검사를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="d34b4-130">6 비즈니스 일 tooapprove hello 도메인을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="d34b4-131">업무일 기준 6일 이내 도메인이 승인되지 않으면 요청이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="d34b4-132">사용자 지정 도메인에서 HTTPS를 사용 하도록 설정한 후 DigiCert 우리의 HTTPS 인증서 공급자는 기본적으로 전자 메일 또는 전화를 통해 WHOIS registrant 정보에 따라 해당 도메인에 대해 hello registrant에 연락 하 여 도메인의 소유권을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="d34b4-133">DigiCert 주소 아래 hello 확인 전자 메일 toohello도를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="d34b4-134">WHOIS 등록자 정보가 개인인 경우 이러한 주소 중 하나에서 직접 승인할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="d34b4-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="d34b4-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="d34b4-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="d34b4-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="d34b4-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="d34b4-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="d34b4-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="d34b4-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="d34b4-139">Hello 전자 메일을 받으면 두 가지 옵션이 있습니다 확인:</span><span class="sxs-lookup"><span data-stu-id="d34b4-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="d34b4-140">Hello에 동일한 계정 hello를 통해 받은 이후 모든 주문을 승인 예: consoto.com 같은 루트 도메인. 이 권장된 방법 tooadd hello hello에 대 한 향후에 추가 사용자 지정 도메인을 계획 하는 경우 동일한 루트 도메인.</span><span class="sxs-lookup"><span data-stu-id="d34b4-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="d34b4-141">이 요청에서 사용 되는 hello 특정 호스트 이름만 승인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="d34b4-142">이후 요청에 대해 추가 승인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="d34b4-143">전자 메일 예:</span><span class="sxs-lookup"><span data-stu-id="d34b4-143">Example email:</span></span>
    
    ![사용자 지정 HTTPS 대화 상자](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="d34b4-145">승인 후 DigiCert 사용자 지정 도메인 이름을 toohello SAN 인증서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="d34b4-146">1 년 동안 hello 인증서는 유효한 되 고 자동 갱신 전에 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="d34b4-147">3 단계: hello 전파에 대 한 초간 기다린 다음 기능을 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="d34b4-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="d34b4-148">Hello 도메인 이름을 확인 한 후 hello 사용자 지정 도메인 HTTPS 기능 toobe 활성화에 대 한 too6 8 시간이 소요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="d34b4-149">Hello 프로세스가 완료 되 면 hello Azure 포털에서에서 hello "사용자 지정 HTTPS" 상태 "Enabled" 너무 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="d34b4-150">이제 사용자 지정 도메인이 있는 HTTPS를 사용할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="d34b4-151">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="d34b4-151">Frequently asked questions</span></span>

1. <span data-ttu-id="d34b4-152">*Hello 인증서 공급자 및 인증서 종류에 사용 되는 누구 입니까?*</span><span class="sxs-lookup"><span data-stu-id="d34b4-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="d34b4-153">DigiCert가 제공한 주체 대체 이름(SAN) 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="d34b4-154">SAN 인증서는 한 개의 인증서로 여러 정규화된 도메인 이름을 보안 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="d34b4-155">*전용 인증서를 사용할 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="d34b4-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="d34b4-156">on hello 로드맵 하지만 현재는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="d34b4-157">*경우에 어떻게 hello 도메인 확인 전자 메일 DigiCert에서 받지 못합니다?*</span><span class="sxs-lookup"><span data-stu-id="d34b4-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="d34b4-158">24시간 이네 전자 메일을 받지 못하면 Microsoft에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d34b4-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="d34b4-159">*SAN 인증서를 사용하는 것보다 전용 인증서를 사용하는 것이 더 안전한가요?*</span><span class="sxs-lookup"><span data-stu-id="d34b4-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="d34b4-160">다음과 같이 hello 전용된 인증서와 동일한 암호화 및 보안 표준을 준수 하는 SAN 인증서입니다. 발급된 모든 SSL 인증서는 서버 보안 강화를 위해 SHA-256을 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="d34b4-161">*Akamai의 Azure CDN에서 사용자 지정 도메인 HTTPS를 사용할 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="d34b4-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="d34b4-162">현재 이 기능은 Verizon의 Azure CDN에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="d34b4-163">향후 몇 개월 hello Akamai에서 Azure CDN와 함께이 기능을 지 원하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d34b4-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d34b4-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d34b4-164">Next steps</span></span>

- <span data-ttu-id="d34b4-165">자세한 방법을를 tooset는 [Azure CDN 끝점에 사용자 지정 도메인](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="d34b4-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


