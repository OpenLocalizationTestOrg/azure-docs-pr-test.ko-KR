---
title: "Azure Active Directory의 조건부 액세스 시작 aaaGet | Microsoft Docs"
description: "위치 조건을 사용하여 조건부 액세스를 테스트합니다."
services: active-directory
keywords: "조건부 액세스 tooapps, Azure AD 사용 하 여 조건부 액세스 조건부 액세스 정책 toocompany 리소스 액세스 보안"
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
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="ff410-104">Azure Active Directory에서 조건부 액세스 시작</span><span class="sxs-lookup"><span data-stu-id="ff410-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="ff410-105">조건부 액세스는 하면 toodefine 조건 권한이 있는 사용자는 앱에 액세스할 수 있도록 Azure Active Directory의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="ff410-106">이 항목에서는 사용자 환경의 위치 조건에 따라 조건부 액세스를 테스트하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="ff410-107">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ff410-107">Scenario description</span></span>

<span data-ttu-id="ff410-108">많은 조직에서 일반적인 요구 사항 하나는 tooonly hello 회사 인트라넷에서 수행 되지 않는 액세스 tooapps에 대 한 multi-factor authentication을 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="ff410-109">Azure Active Directory를 사용하면 위치 기반 조건부 액세스 정책을 구성하여 이 목표를 쉽게 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="ff410-110">여기서는 관련 정책 구성에 대한 자세한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="ff410-111">정책을 이용 하 여 hello [신뢰할 수 있는 Ip](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) hello 회사에서 만든 액세스 시도 간에 toodistinguish 인트라넷 및 다른 모든 위치로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ff410-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ff410-112">Prerequisites</span></span>

<span data-ttu-id="ff410-113">hello이 항목에 설명 된 시나리오에서는 가정에 설명 된 hello 개념에 익숙한 [Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="ff410-114">tootest이이 시나리오를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="ff410-115">테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ff410-115">Create a test user</span></span> 

- <span data-ttu-id="ff410-116">할당 된 Azure AD Premium 라이선스 toohello 테스트 사용자</span><span class="sxs-lookup"><span data-stu-id="ff410-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="ff410-117">관리 되는 앱을 구성 하 고 테스트 사용자 tooit를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="ff410-118">신뢰할 수 있는 IP 구성</span><span class="sxs-lookup"><span data-stu-id="ff410-118">Configure trusted IPs</span></span>

<span data-ttu-id="ff410-119">신뢰할 수 있는 IP에 대한 자세한 내용은 [신뢰할 수 있는 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff410-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="ff410-120">정책 구성 단계</span><span class="sxs-lookup"><span data-stu-id="ff410-120">Policy configuration steps</span></span>

<span data-ttu-id="ff410-121">**tooconfigure 조건부 액세스 정책에 수행:**</span><span class="sxs-lookup"><span data-stu-id="ff410-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="ff410-122">Hello hello 왼쪽된 탐색 모음에서 Azure 포털에서에서 클릭 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="ff410-124">Hello에 **Azure Active Directory** 블레이드 hello **관리** 섹션에서 클릭 **조건부 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="ff410-126">Hello에 **조건부 액세스** 블레이드, tooopen hello **새로** 블레이드 hello 바탕 화면에서 hello 도구 모음에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="ff410-128">Hello에 **새로** 블레이드 hello **이름** 텍스트 상자 정책의 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="ff410-130">Hello에 **할당** 섹션에서 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="ff410-132">Hello에 **사용자 및 그룹** 블레이드에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="ff410-134">a.</span><span class="sxs-lookup"><span data-stu-id="ff410-134">a.</span></span> <span data-ttu-id="ff410-135">**사용자 및 그룹 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="ff410-136">b.</span><span class="sxs-lookup"><span data-stu-id="ff410-136">b.</span></span> <span data-ttu-id="ff410-137">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-137">Click **Select**.</span></span>

    <span data-ttu-id="ff410-138">c.</span><span class="sxs-lookup"><span data-stu-id="ff410-138">c.</span></span> <span data-ttu-id="ff410-139">Hello에 **선택** 블레이드에서 테스트 사용자를 선택한 다음 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="ff410-140">d.</span><span class="sxs-lookup"><span data-stu-id="ff410-140">d.</span></span> <span data-ttu-id="ff410-141">Hello에 **사용자 및 그룹** 블레이드에서 클릭 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="ff410-142">Hello에 **새로** 블레이드, tooopen hello **클라우드 앱** 블레이드 hello **할당** 섹션에서 클릭 **클라우드 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="ff410-144">Hello에 **클라우드 앱** 블레이드에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="ff410-146">a.</span><span class="sxs-lookup"><span data-stu-id="ff410-146">a.</span></span> <span data-ttu-id="ff410-147">**앱 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-147">Click **Select apps**.</span></span>

    <span data-ttu-id="ff410-148">b.</span><span class="sxs-lookup"><span data-stu-id="ff410-148">b.</span></span> <span data-ttu-id="ff410-149">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-149">Click **Select**.</span></span>

    <span data-ttu-id="ff410-150">c.</span><span class="sxs-lookup"><span data-stu-id="ff410-150">c.</span></span> <span data-ttu-id="ff410-151">Hello에 **선택** 블레이드에서 클라우드 응용 프로그램을 선택한 다음 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="ff410-152">d.</span><span class="sxs-lookup"><span data-stu-id="ff410-152">d.</span></span> <span data-ttu-id="ff410-153">Hello에 **클라우드 앱** 블레이드에서 클릭 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="ff410-154">Hello에 **새로** 블레이드, tooopen hello **조건** 블레이드 hello **할당** 섹션에서 클릭 **조건**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="ff410-156">Hello에 **조건** 블레이드, tooopen hello **위치** 블레이드에서 클릭 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="ff410-158">Hello에 **위치** 블레이드에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="ff410-160">a.</span><span class="sxs-lookup"><span data-stu-id="ff410-160">a.</span></span> <span data-ttu-id="ff410-161">**구성** 아래에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="ff410-162">b.</span><span class="sxs-lookup"><span data-stu-id="ff410-162">b.</span></span> <span data-ttu-id="ff410-163">**포함**에서 **모든 위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="ff410-164">c.</span><span class="sxs-lookup"><span data-stu-id="ff410-164">c.</span></span> <span data-ttu-id="ff410-165">**제외**를 클릭한 다음 **모든 신뢰할 수 있는 IP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="ff410-167">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="ff410-167">d.</span></span> <span data-ttu-id="ff410-168">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-168">Click **Done**.</span></span>

12. <span data-ttu-id="ff410-169">Hello에 **조건** 블레이드에서 클릭 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="ff410-170">Hello에 **새로** 블레이드, tooopen hello **Grant** 블레이드 hello **컨트롤** 섹션에서 클릭 **Grant**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="ff410-172">Hello에 **Grant** 블레이드에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="ff410-174">a.</span><span class="sxs-lookup"><span data-stu-id="ff410-174">a.</span></span> <span data-ttu-id="ff410-175">**다단계 인증 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="ff410-176">b.</span><span class="sxs-lookup"><span data-stu-id="ff410-176">b.</span></span> <span data-ttu-id="ff410-177">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-177">Click **Select**.</span></span>

15. <span data-ttu-id="ff410-178">Hello에 **새로** 블레이드 아래 **정책 사용**, 클릭 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![조건부 액세스](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="ff410-180">Hello에 **새로** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="ff410-181">Hello 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="ff410-181">Testing hello policy</span></span>

<span data-ttu-id="ff410-182">tootest 정책에 장치에서 앱에 액세스 해야 하는:</span><span class="sxs-lookup"><span data-stu-id="ff410-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="ff410-183">구성된 신뢰할 수 있는 IP에 속한 IP 주소가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="ff410-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="ff410-184">구성된 신뢰할 수 있는 IP에 속하지 않은 IP 주소가 있는 장치</span><span class="sxs-lookup"><span data-stu-id="ff410-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="ff410-185">다단계 인증은 구성된 신뢰할 수 있는 IP에 속하지 않은 장치에서 수행되는 연결 시도에서만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="ff410-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff410-186">Next steps</span></span>

<span data-ttu-id="ff410-187">조건부 액세스에 대 한 자세한 toolearn 싶으시면 참조 [Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff410-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

