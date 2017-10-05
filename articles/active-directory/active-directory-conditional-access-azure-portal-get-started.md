---
title: "Azure Active Directory에서 조건부 액세스 시작 | Microsoft Docs"
description: "위치 조건을 사용하여 조건부 액세스를 테스트합니다."
services: active-directory
keywords: "앱에 조건부 액세스, Azure AD로 조건부 액세스, 회사 리소스에 대한 액세스 보호, 조건부 액세스 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="04e75-104">Azure Active Directory에서 조건부 액세스 시작</span><span class="sxs-lookup"><span data-stu-id="04e75-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="04e75-105">조건부 액세스는 권한 있는 사용자가 앱에 액세스할 수 있는 조건을 정의할 수 있게 해주는 Azure Active Directory의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="04e75-106">이 항목에서는 사용자 환경의 위치 조건에 따라 조건부 액세스를 테스트하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="04e75-107">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="04e75-107">Scenario description</span></span>

<span data-ttu-id="04e75-108">많은 조직의 일반적 요구 사항 중 하나는 회사 인트라넷에서 수행되지 않는 앱 액세스를 위해 다단계 인증만 필요하다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="04e75-109">Azure Active Directory를 사용하면 위치 기반 조건부 액세스 정책을 구성하여 이 목표를 쉽게 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="04e75-110">여기서는 관련 정책 구성에 대한 자세한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="04e75-111">정책은 [신뢰할 수 있는 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)를 활용하여 회사 인트라넷과 다른 모든 위치 간에 시도되는 액세스를 구별합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="04e75-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="04e75-112">Prerequisites</span></span>

<span data-ttu-id="04e75-113">이 항목의 시나리오에서는 [Azure Active Directory 조건부 액세스](active-directory-conditional-access-azure-portal.md)에서 설명한 개념을 잘 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="04e75-114">이 시나리오를 테스트하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="04e75-115">테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="04e75-115">Create a test user</span></span> 

- <span data-ttu-id="04e75-116">테스트 사용자에게 Azure AD Premium 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="04e75-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="04e75-117">관리되는 앱 구성 및 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="04e75-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="04e75-118">신뢰할 수 있는 IP 구성</span><span class="sxs-lookup"><span data-stu-id="04e75-118">Configure trusted IPs</span></span>

<span data-ttu-id="04e75-119">신뢰할 수 있는 IP에 대한 자세한 내용은 [신뢰할 수 있는 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04e75-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="04e75-120">정책 구성 단계</span><span class="sxs-lookup"><span data-stu-id="04e75-120">Policy configuration steps</span></span>

<span data-ttu-id="04e75-121">**조건부 액세스 정책을 구성하려면 다음을 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="04e75-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="04e75-122">Azure Portal의 왼쪽 탐색 모음에서 **Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="04e75-124">**Azure Active Directory** 블레이드의 **관리** 섹션에서 **조건부 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="04e75-126">**조건부 액세스** 블레이드에서 **새로 만들기** 블레이드를 열려면 위쪽의 도구 모음에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="04e75-128">**새로 만들기** 블레이드의 **이름** 텍스트 상자에서 정책 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="04e75-130">**할당** 섹션에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="04e75-132">**사용자 및 그룹** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="04e75-134">a.</span><span class="sxs-lookup"><span data-stu-id="04e75-134">a.</span></span> <span data-ttu-id="04e75-135">**사용자 및 그룹 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="04e75-136">b.</span><span class="sxs-lookup"><span data-stu-id="04e75-136">b.</span></span> <span data-ttu-id="04e75-137">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-137">Click **Select**.</span></span>

    <span data-ttu-id="04e75-138">c.</span><span class="sxs-lookup"><span data-stu-id="04e75-138">c.</span></span> <span data-ttu-id="04e75-139">**선택** 블레이드에서 테스트 사용자를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="04e75-140">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="04e75-140">d.</span></span> <span data-ttu-id="04e75-141">**사용자 및 그룹** 블레이드에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="04e75-142">**새로 만들기** 블레이드에서 **클라우드 앱** 블레이드를 열려면 **할당** 섹션에서 **클라우드 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="04e75-144">**클라우드 앱** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="04e75-146">a.</span><span class="sxs-lookup"><span data-stu-id="04e75-146">a.</span></span> <span data-ttu-id="04e75-147">**앱 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-147">Click **Select apps**.</span></span>

    <span data-ttu-id="04e75-148">b.</span><span class="sxs-lookup"><span data-stu-id="04e75-148">b.</span></span> <span data-ttu-id="04e75-149">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-149">Click **Select**.</span></span>

    <span data-ttu-id="04e75-150">c.</span><span class="sxs-lookup"><span data-stu-id="04e75-150">c.</span></span> <span data-ttu-id="04e75-151">**선택** 블레이드에서 클라우드 앱을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="04e75-152">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="04e75-152">d.</span></span> <span data-ttu-id="04e75-153">**클라우드 앱** 블레이드에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="04e75-154">**새로 만들기** 블레이드에서 **조건** 블레이드를 열려면 **할당** 섹션에서 **조건**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="04e75-156">**조건** 블레이드에서 **위치** 블레이드를 열려면 **위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="04e75-158">**위치** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-158">On the **Locations** blade, perform the following steps:</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="04e75-160">a.</span><span class="sxs-lookup"><span data-stu-id="04e75-160">a.</span></span> <span data-ttu-id="04e75-161">**구성** 아래에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="04e75-162">b.</span><span class="sxs-lookup"><span data-stu-id="04e75-162">b.</span></span> <span data-ttu-id="04e75-163">**포함**에서 **모든 위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="04e75-164">c.</span><span class="sxs-lookup"><span data-stu-id="04e75-164">c.</span></span> <span data-ttu-id="04e75-165">**제외**를 클릭한 다음 **모든 신뢰할 수 있는 IP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="04e75-167">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="04e75-167">d.</span></span> <span data-ttu-id="04e75-168">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-168">Click **Done**.</span></span>

12. <span data-ttu-id="04e75-169">**조건** 블레이드에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="04e75-170">**새로 만들기** 블레이드에서 **허용** 블레이드를 열려면 **제어** 섹션에서 **허용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="04e75-172">**허용** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-172">On the **Grant** blade, perform the following steps:</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="04e75-174">a.</span><span class="sxs-lookup"><span data-stu-id="04e75-174">a.</span></span> <span data-ttu-id="04e75-175">**다단계 인증 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="04e75-176">b.</span><span class="sxs-lookup"><span data-stu-id="04e75-176">b.</span></span> <span data-ttu-id="04e75-177">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-177">Click **Select**.</span></span>

15. <span data-ttu-id="04e75-178">**새로 만들기** 블레이드의 **정책 사용**에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="04e75-180">**새로 만들기** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="04e75-181">정책 테스트</span><span class="sxs-lookup"><span data-stu-id="04e75-181">Testing the policy</span></span>

<span data-ttu-id="04e75-182">정책을 테스트하려면 다음과 같은 장치에서 앱에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="04e75-183">구성된 신뢰할 수 있는 IP에 속한 IP 주소가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="04e75-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="04e75-184">구성된 신뢰할 수 있는 IP에 속하지 않은 IP 주소가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="04e75-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="04e75-185">다단계 인증은 구성된 신뢰할 수 있는 IP에 속하지 않은 장치에서 수행되는 연결 시도에서만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="04e75-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="04e75-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04e75-186">Next steps</span></span>

<span data-ttu-id="04e75-187">조건부 액세스에 대한 자세한 내용은 [Azure Active Directory 조건부 액세스](active-directory-conditional-access-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04e75-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

