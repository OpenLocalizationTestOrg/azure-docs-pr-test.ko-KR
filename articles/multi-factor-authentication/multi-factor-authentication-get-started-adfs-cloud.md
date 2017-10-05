---
title: "Azure MFA 및 AD FS를 사용하여 클라우드 리소스 보안 유지 | Microsoft Docs"
description: "클라우드에서 Azure MFA 및 AD FS 시작 방법을 설명하는 Azure Multi-Factor Authentication 페이지입니다."
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
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="e83ad-103">Azure Multi-Factor Authentication 및 AD FS를 사용하여 클라우드 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="e83ad-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="e83ad-104">조직이 Azure Active Directory와 페더레이션되어 있는 경우 Azure Multi-Factor Authentication 또는 AD FS(Active Directory Federation Services)를 사용하여 Azure AD에서 액세스하는 리소스를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="e83ad-105">Azure Multi-Factor Authentication 또는 Active Directory Federation Services를 사용하여 Azure Active Directory 리소스를 보호하려면 다음 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e83ad-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="e83ad-106">AD FS를 사용하여 Azure AD 리소스 보안 유지</span><span class="sxs-lookup"><span data-stu-id="e83ad-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="e83ad-107">클라우드 리소스를 보호하려면 사용자가 두 단계 인증을 성공적으로 수행했을 때 Active Directory Federation Services가 multipleauthn 클레임을 내보내도록 클레임 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="e83ad-108">이 클레임은 Azure AD에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="e83ad-109">다음 단계를 수행하려면 이 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e83ad-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="e83ad-110">AD FS 관리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="e83ad-111">왼쪽에서 **신뢰 당사자 트러스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e83ad-112">**Microsoft Office 365 ID 플랫폼**을 마우스 오른쪽 단추로 클릭하고 **클레임 규칙 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="e83ad-114">발급 변환 규칙에서 **규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="e83ad-116">변환 클레임 규칙 추가 마법사의 드롭다운 목록에서 **들어오는 클레임 통과 또는 필터링**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="e83ad-118">규칙의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="e83ad-119">들어오는 클레임 유형으로 **인증 방법 참조**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="e83ad-120">**모든 클레임 값 통과**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="e83ad-121">![변환 클레임 규칙 추가 마법사](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="e83ad-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="e83ad-122">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-122">Click **Finish**.</span></span> <span data-ttu-id="e83ad-123">AD FS 관리 콘솔을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="e83ad-124">페더레이션 사용자를 위한 신뢰할 수 있는 IP</span><span class="sxs-lookup"><span data-stu-id="e83ad-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="e83ad-125">신뢰할 수 있는 IP를 사용하면 관리자가 특정 IP 주소 또는 자신의 인트라넷 내에서 시작된 요청을 가진 페더레이션 사용자에 대한 2단계 확인을 바이패스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="e83ad-126">다음 섹션에서는 페더레이션 사용자 인트라넷에서 요청이 시작되는 경우 페더레이션 사용자로 Azure Multi-Factor Authentication 신뢰할 수 있는 IP를 구성하고 2단계 확인을 바이패스하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="e83ad-127">이 작업은 들어오는 클레임(회사 네트워크 내부 클레임 형식 사용) 통과 또는 필터링 템플릿을 사용하도록 AD FS를 구성하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="e83ad-128">이 예제는 신뢰 당사자 트러스트에 대해 Office 365를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="e83ad-129">AD FS 클레임 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="e83ad-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="e83ad-130">가장 먼저 AD FS 클레임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="e83ad-131">두 개의 클레임 규칙을 만듭니다. 하나는 회사 네트워크 내부 클레임 형식에 대한 규칙이고 다른 하나는 사용자의 로그인 상태를 유지하기 위한 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="e83ad-132">AD FS 관리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="e83ad-133">왼쪽에서 **신뢰 당사자 트러스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e83ad-134">**Microsoft Office 365 ID 플랫폼**을 마우스 오른쪽 단추로 클릭하고 **클레임 규칙 편집...**를 선택합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="e83ad-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="e83ad-135">발급 변환 규칙에서 **규칙 추가**를 클릭합니다.
   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="e83ad-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="e83ad-136">변환 클레임 규칙 추가 마법사의 드롭다운 목록에서 **들어오는 클레임 통과 또는 필터링**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="e83ad-137">![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="e83ad-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="e83ad-138">클레임 규칙 이름 옆에 있는 상자에 규칙의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="e83ad-139">예를 들어 InsideCorpNet입니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="e83ad-140">들어오는 클레임 형식 옆의 드롭다운 목록에서 **회사 네트워크 내부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="e83ad-141">![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="e83ad-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="e83ad-142">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-142">Click **Finish**.</span></span>
9. <span data-ttu-id="e83ad-143">발급 변환 규칙에서 **규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="e83ad-144">변환 클레임 규칙 추가 마법사의 드롭다운 목록에서 **사용자 지정 규칙을 사용하여 클레임 보내기**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="e83ad-145">클레임 규칙 이름 아래에 있는 상자에 *로그인한 사용자 유지*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="e83ad-146">사용자 지정 규칙 상자에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="e83ad-148">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-148">Click **Finish**.</span></span>
14. <span data-ttu-id="e83ad-149">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-149">Click **Apply**.</span></span>
15. <span data-ttu-id="e83ad-150">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-150">Click **Ok**.</span></span>
16. <span data-ttu-id="e83ad-151">AD FS 관리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="e83ad-152">페더레이션 사용자로 Azure Multi-Factor Authentication 신뢰할 수 있는 IP 구성</span><span class="sxs-lookup"><span data-stu-id="e83ad-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="e83ad-153">이제 클레임이 적용되었으므로 신뢰할 수 있는 IP를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="e83ad-154">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e83ad-155">왼쪽에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="e83ad-156">디렉터리에서 신뢰할 수 있는 IP를 설정하려는 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="e83ad-157">선택한 디렉터리에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="e83ad-158">Multi-Factor Authentication 섹션에서 **서비스 설정 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="e83ad-159">서비스 설정 페이지의 신뢰할 수 있는 IP에서 **내 인트라넷에서 페더레이션 사용자의 요청에 대한 Multi-Factor Authentication 건너뛰기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![클라우드](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="e83ad-161">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-161">Click **save**.</span></span>
8. <span data-ttu-id="e83ad-162">업데이트를 적용하면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-162">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="e83ad-163">끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-163">That’s it!</span></span> <span data-ttu-id="e83ad-164">이제 회사 인트라넷 외부에서 클레임이 시작하는 경우 Office 365 페더레이션 사용자만 MFA를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e83ad-164">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
