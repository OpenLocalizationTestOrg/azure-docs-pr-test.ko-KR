---
title: "Azure MFA 및 AD FS를 사용 하 여 클라우드 리소스 aaaSecure | Microsoft Docs"
description: "Azure MFA 및 AD FS hello 클라우드에서 tooget 시작 하는 방법을 설명 하는 hello Azure Multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="cfba3-103">Azure Multi-Factor Authentication 및 AD FS를 사용하여 클라우드 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="cfba3-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="cfba3-104">Azure Active Directory와 페더레이션 조직의 경우 Azure Multi-factor Authentication 또는 Azure AD에 액세스 하는 Active Directory Federation Services (AD FS) toosecure 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="cfba3-105">Azure Multi-factor Authentication 또는 Active Directory Federation Services를 사용 하 여 프로시저 toosecure Azure Active Directory 리소스를 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="cfba3-106">AD FS를 사용하여 Azure AD 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="cfba3-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="cfba3-107">toosecure 클라우드 리소스에 있도록를 설정 클레임 규칙 2 단계 인증을 성공적으로 수행할 때 Active Directory Federation Services hello multipleauthn 클레임을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="cfba3-108">이 클레임 tooAzure AD에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="cfba3-109">이 프로시저 toowalk hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="cfba3-110">AD FS 관리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="cfba3-111">Hello 왼쪽에서 선택 **신뢰 당사자 트러스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="cfba3-112">**Microsoft Office 365 ID 플랫폼**을 마우스 오른쪽 단추로 클릭하고 **클레임 규칙 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="cfba3-114">발급 변환 규칙에서 **규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="cfba3-116">변환 클레임 규칙 추가 마법사 hello, 선택 **통과 또는 들어오는 클레임 필터링** 에서 드롭 다운 hello 및 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="cfba3-118">규칙의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="cfba3-119">선택 **인증 방법 참조** 들어오는 hello로 클레임 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="cfba3-120">**모든 클레임 값 통과**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="cfba3-121">![변환 클레임 규칙 추가 마법사](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="cfba3-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="cfba3-122">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-122">Click **Finish**.</span></span> <span data-ttu-id="cfba3-123">Hello AD FS 관리 콘솔을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="cfba3-124">페더레이션 사용자를 위한 신뢰할 수 있는 IP</span><span class="sxs-lookup"><span data-stu-id="cfba3-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="cfba3-125">신뢰할 수 있는 Ip tooby 패스 2 단계 인증에 대 한 특정 IP 주소 또는 페더레이션된 사용자 자신의 인트라넷 내에서 발생 하는 요청에 대 한 관리자를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="cfba3-126">hello 다음 섹션에서는 설명 방법을 tooconfigure Azure Multi-factor Authentication 신뢰할 수 있는 Ip 페더레이션된 사용자와 페더레이션된 사용자 인트라넷 내에서 요청을 시작 하는 경우 2 단계 인증을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="cfba3-127">이 내부 회사 네트워크 클레임 유형 hello를 사용 하 여 AD FS toouse 통과 또는 필터는 들어오는 청구 서식 파일을 구성 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="cfba3-128">이 예제는 신뢰 당사자 트러스트에 대해 Office 365를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="cfba3-129">Hello AD FS 클레임 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="cfba3-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="cfba3-130">hello 먼저 toodo tooconfigure hello AD FS 클레임 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="cfba3-131">Hello 내부 회사 네트워크에 대 한 클레임 형식 및 다른 하나는 사용자의 로그인 페이지에 유지, 두 개의 클레임 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="cfba3-132">AD FS 관리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="cfba3-133">Hello 왼쪽에서 선택 **신뢰 당사자 트러스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="cfba3-134">**Microsoft Office 365 ID 플랫폼**을 마우스 오른쪽 단추로 클릭하고 **클레임 규칙 편집...**를 선택합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="cfba3-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="cfba3-135">발급 변환 규칙에서 **규칙 추가**를 클릭합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="cfba3-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="cfba3-136">변환 클레임 규칙 추가 마법사 hello, 선택 **통과 또는 들어오는 클레임 필터링** 에서 드롭 다운 hello 및 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="cfba3-137">![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="cfba3-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="cfba3-138">Hello 상자 다음 tooClaim 규칙 이름에 규칙 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="cfba3-139">예를 들어 InsideCorpNet입니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="cfba3-140">Hello 드롭다운 목록에서에서 다음 tooIncoming 클레임 유형, 선택 **내부 회사 네트워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="cfba3-141">![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="cfba3-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="cfba3-142">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-142">Click **Finish**.</span></span>
9. <span data-ttu-id="cfba3-143">발급 변환 규칙에서 **규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="cfba3-144">변환 클레임 규칙 추가 마법사 hello, 선택 **사용자 지정 규칙을 사용 하 여 클레임 보내기** 에서 드롭 다운 hello 및 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="cfba3-145">클레임 규칙 이름 아래의 상자 hello: 입력 *Keep Users Signed In*합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="cfba3-146">Hello 사용자 지정 규칙 상자에 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="cfba3-148">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-148">Click **Finish**.</span></span>
14. <span data-ttu-id="cfba3-149">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-149">Click **Apply**.</span></span>
15. <span data-ttu-id="cfba3-150">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-150">Click **Ok**.</span></span>
16. <span data-ttu-id="cfba3-151">AD FS 관리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="cfba3-152">페더레이션 사용자로 Azure Multi-Factor Authentication 신뢰할 수 있는 IP 구성</span><span class="sxs-lookup"><span data-stu-id="cfba3-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="cfba3-153">Hello 클레임을 저장 했으므로 신뢰할 수 있는 Ip를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="cfba3-154">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="cfba3-155">Hello 왼쪽에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="cfba3-156">디렉터리에서 신뢰할 수 있는 Ip tooset 저장할 hello 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="cfba3-157">선택한 디렉터리 hello 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="cfba3-158">Hello multi-factor 인증 섹션에서 클릭 **서비스 설정 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="cfba3-159">Hello 서비스 설정 페이지에서 신뢰할 수 있는 Ip 선택 **authentication을 건너뛰도록 다중-factor-요청에 대 한 페더레이션된 사용자의 내 인트라넷에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="cfba3-161">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-161">Click **save**.</span></span>
8. <span data-ttu-id="cfba3-162">Hello 업데이트를 적용 한 후 클릭 **닫습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="cfba3-163">끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-163">That’s it!</span></span> <span data-ttu-id="cfba3-164">이 시점에서 Office 365 페더레이션된 사용자 클레임 hello 회사 인트라넷 외부에서 발생 하는 경우에 toouse MFA 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfba3-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
