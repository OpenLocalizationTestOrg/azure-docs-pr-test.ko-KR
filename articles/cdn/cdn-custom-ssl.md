---
title: "Azure CDN 사용자 지정 도메인에서 HTTPS를 사용하도록 설정 | Microsoft Docs"
description: "사용자 지정 도메인의 Azure CDN 끝점에서 HTTPS를 사용하도록 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="9ed71-103">Azure CDN 사용자 지정 도메인에서 HTTPS를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9ed71-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="9ed71-104">Azure CDN 사용자 지정 도메인에 대한 HTTPS 지원을 통해 자신의 고유한 도메인 이름을 사용하는 SSL로 안전한 콘텐츠를 제공하고 전송 중에 데이터 보안을 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="9ed71-105">사용자 지정 도메인에 대해 HTTPS를 사용하는 종단 간 워크플로는 클릭 한 번 사용, 완전한 인증서 관리를 통해 간소화되며 이 모든 것을 추가 비용 없이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="9ed71-106">전송 중에 모든 웹 응용 프로그램의 중요한 데이터에 대해 프라이버시 및 무결성을 보장하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="9ed71-107">HTTPS 프로토콜을 사용하면 인터넷 간에 전송되는 중요한 데이터를 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="9ed71-108">신뢰할 수 있는 인증을 제공하며 공격으로부터 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="9ed71-109">현재 Azure CDN은 CDN 끝점에서 HTTPS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="9ed71-110">예를 들어 Azure CDN(예: https://contoso.azureedge.net )에서 CDN 끝점을 만드는 경우 기본적으로 HTTPS가 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="9ed71-111">이제 사용자 지정 도메인 HTTPS를 사용하여 사용자 지정 도메인(예: https://www.contoso.com )에 대해서도 안전한 전달을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="9ed71-112">HTTPS 기능의 주요 특성 몇 가지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="9ed71-113">추가 비용 없음: 인증서 얻기 또는 갱신에 대해 비용이 없으며 HTTPS 트래픽에 대한 추가 비용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="9ed71-114">CDN에서 송신되는 양(GB)에 대한 비용만 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="9ed71-115">간단한 사용: [Azure Portal](https://portal.azure.com)에서 클릭 한 번으로 프로비전이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9ed71-116">REST API 또는 기타 개발자 도구를 사용하여 기능을 활성화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="9ed71-117">완전한 인증서 관리: 사용자를 위해 모든 인증서 조달 및 관리가 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="9ed71-118">인증서가 만료되기 전에 자동으로 프로비전 및 갱신됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="9ed71-119">따라서 인증서 만료로 인한 서비스 중단 위험이 완전히 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="9ed71-120">HTTPS 지원을 사용하도록 설정하기 전에 [Azure CDN 사용자 지정 도메인](./cdn-map-content-to-custom-domain.md)을 미리 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="9ed71-121">1단계: 기능 활성화</span><span class="sxs-lookup"><span data-stu-id="9ed71-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="9ed71-122">[Azure Portal](https://portal.azure.com)에서 Verizon 표준 또는 프리미엄 CDN 프로필로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="9ed71-123">끝점 목록에서 사용자 지정 도메인을 포함하는 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="9ed71-124">HTTPS를 사용하도록 설정할 사용자 지정 도메인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![끝점 블레이드](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="9ed71-126">**설정**을 클릭하여 HTTPS를 사용하도록 설정하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![사용자 지정 HTTPS 대화 상자](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="9ed71-128">2단계: 도메인 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9ed71-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="9ed71-129">사용자 지정 도메인에서 HTTPS를 활성화하기 전에 도메인 유효성 검사를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="9ed71-130">업무일 기준 6일 이내 도메인이 승인되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="9ed71-131">업무일 기준 6일 이내 도메인이 승인되지 않으면 요청이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="9ed71-132">사용자 지정 도메인에서 HTTPS를 사용하도록 설정한 후에는, HTTPS 인증서 공급자 DigiCert가 도메인 등록자에게 연락하여 전자 메일(기본값) 또는 전화로 WHOIS 등록자 정보를 토대로 도메인 소유권의 유효성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="9ed71-133">또한 DigiCert는 아래 주소로 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="9ed71-134">WHOIS 등록자 정보가 개인인 경우 이러한 주소 중 하나에서 직접 승인할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="9ed71-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="9ed71-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="9ed71-136">webmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="9ed71-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="9ed71-137">hostmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="9ed71-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="9ed71-138">postmaster@<your-domain-name.com></span><span class="sxs-lookup"><span data-stu-id="9ed71-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="9ed71-139">전자 메일을 받으면 두 가지 확인 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="9ed71-140">동일한 루트 도메인의 동일한 계정을 통해 이루어진 모든 향후 주문을 승인할 수 있습니다(예: consoto.com).</span><span class="sxs-lookup"><span data-stu-id="9ed71-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="9ed71-141">향후 동일한 루트 도메인에 대해 사용자 지정 도메인을 추가할 예정인 경우 권장되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="9ed71-142">이 요청에 사용된 특정 호스트 이름을 승인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="9ed71-143">이후 요청에 대해 추가 승인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="9ed71-144">전자 메일 예:</span><span class="sxs-lookup"><span data-stu-id="9ed71-144">Example email:</span></span>
    
    ![사용자 지정 HTTPS 대화 상자](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="9ed71-146">승인 후에는 DigiCert가 사용자 지정 도메인 이름을 SAN 인증서에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="9ed71-147">인증서는 1년 동안 유효하며 만료되기 전 자동으로 갱신됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="9ed71-148">3단계: 적용될 때까지 기다린 후 기능 사용 시작</span><span class="sxs-lookup"><span data-stu-id="9ed71-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="9ed71-149">도메인 이름이 확인된 후 사용자 지정 도메인 HTTPS 기능이 활성 상태가 될 때까지는 최대 6-8시간 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="9ed71-150">프로세스가 완료되면 Azure Portal에서 "사용자 지정 HTTPS" 상태가 "사용"으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="9ed71-151">이제 사용자 지정 도메인이 있는 HTTPS를 사용할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="9ed71-152">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="9ed71-152">Frequently asked questions</span></span>

1. <span data-ttu-id="9ed71-153">*인증서 공급자는 누구이며 어떤 유형의 인증서가 사용되나요?*</span><span class="sxs-lookup"><span data-stu-id="9ed71-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="9ed71-154">DigiCert가 제공한 주체 대체 이름(SAN) 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="9ed71-155">SAN 인증서는 한 개의 인증서로 여러 정규화된 도메인 이름을 보안 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="9ed71-156">*전용 인증서를 사용할 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="9ed71-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="9ed71-157">현재는 불가능하지만 준비 중입니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="9ed71-158">*DigiCert로부터 도메인 확인 메일을 받지 못한 경우 어떻게 하나요?*</span><span class="sxs-lookup"><span data-stu-id="9ed71-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="9ed71-159">24시간 이네 전자 메일을 받지 못하면 Microsoft에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="9ed71-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="9ed71-160">*SAN 인증서를 사용하는 것보다 전용 인증서를 사용하는 것이 더 안전한가요?*</span><span class="sxs-lookup"><span data-stu-id="9ed71-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="9ed71-161">SAN 인증서는 전용 인증서와 동일한 암호화 및 보안 표준을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="9ed71-162">발급된 모든 SSL 인증서는 서버 보안 강화를 위해 SHA-256을 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="9ed71-163">*Akamai의 Azure CDN에서 사용자 지정 도메인 HTTPS를 사용할 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="9ed71-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="9ed71-164">현재 이 기능은 Verizon의 Azure CDN에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="9ed71-165">Akamai의 Azure CDN에서 이 기능을 몇 달 이내 지원하기 위한 작업 중입니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9ed71-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ed71-166">Next steps</span></span>

- <span data-ttu-id="9ed71-167">[Azure CDN 끝점에서 사용자 지정 도메인을 사용하도록 설정](./cdn-map-content-to-custom-domain.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ed71-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


