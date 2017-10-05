---
title: "Azure Active Directory 조건부 액세스 | Microsoft Docs"
description: "Azure Active Directory에서 조건부 액세스 제어를 사용하여 응용 프로그램에 대한 액세스를 인증할 때 특정 조건을 확인합니다."
services: active-directory
keywords: "앱에 조건부 액세스, Azure AD로 조건부 액세스, 회사 리소스에 대한 액세스 보호, 조건부 액세스 정책"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 20572ecbde79bc2722f3a25f297c92d8e722a3e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="conditional-access-in-azure-active-directory"></a><span data-ttu-id="fc2da-104">Azure Active Directory 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="fc2da-104">Conditional access in Azure Active Directory</span></span>

<span data-ttu-id="fc2da-105">모바일 우선, 클라우드 우선 세계에서 Azure Active Directory는 어디에서나 장치, 앱 및 서비스에 대한 Single Sign-On을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-105">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="fc2da-106">장치(BYOD 포함), 기업 네트워크 외 근무 및 타사 SaaS 앱의 확산에 따라 IT 전문가는 다음 두 가지 대립되는 목표에 직면하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-106">With the proliferation of devices (including BYOD), work off corporate networks, and 3rd party SaaS apps, IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="fc2da-107">최종 사용자가 언제 어디서나 생산성을 높일 수 있도록 지원</span><span class="sxs-lookup"><span data-stu-id="fc2da-107">Empower the end users to be productive wherever and whenever</span></span>
- <span data-ttu-id="fc2da-108">언제든지 회사 자산 보호</span><span class="sxs-lookup"><span data-stu-id="fc2da-108">Protect the corporate assets at any time</span></span>

<span data-ttu-id="fc2da-109">Azure Active Directory는 생산성을 높이기 위해 회사 자산에 액세스할 수 있는 광범위한 옵션을 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-109">To improve productivity, Azure Active Directory provides your users with a broad range of options to access your corporate assets.</span></span> <span data-ttu-id="fc2da-110">응용 프로그램 액세스 관리를 사용하면 *권한이 있는 사용자*만 Azure Active Directory를 통해 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-110">With application access management, Azure Active Directory enables you to ensure that only *the right people* can access your applications.</span></span> <span data-ttu-id="fc2da-111">권한이 있는 사용자가 특정 조건에서 리소스에 액세스하는 방법을 보다 효과적으로 제어하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="fc2da-111">What if you want to have more control over how the right people are accessing your resources under certain conditions?</span></span> <span data-ttu-id="fc2da-112">*권한이 있는 사용자*에게도 특정 앱에 대한 액세스를 차단하려는 조건이 있는 경우에는 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="fc2da-112">What if you even have conditions under which you want to block access to certain apps even for the *right people*?</span></span> <span data-ttu-id="fc2da-113">예를 들어 권한이 있는 사용자가 신뢰할 수 있는 네트워크에서 특정 앱에 액세스한다면 문제 없겠지만, 신뢰할 수 없는 네트워크에서 이러한 앱에 액세스하는 것을 원하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-113">For example, it might be OK for you if the right people are accessing certain apps from a trusted network; however, you might not want them to access these apps from a network you don't trust.</span></span> <span data-ttu-id="fc2da-114">조건부 액세스를 사용하면 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-114">You can address these questions using conditional access.</span></span>

<span data-ttu-id="fc2da-115">조건부 액세스는 특정 조건에 따라 사용자 환경의 응용 프로그램에 대한 액세스를 제어할 수 있는 Azure Active Directory의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-115">Conditional access is a capability of Azure Active Directory that enables you to enforce controls on the access to apps in your environment based on specific conditions.</span></span> <span data-ttu-id="fc2da-116">제어 문을 사용하면 추가 요구 사항을 액세스에 연결하거나 액세스를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-116">With controls, you can either tie additional requirements to the access or you can block it.</span></span> <span data-ttu-id="fc2da-117">조건부 액세스의 구현은 정책을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-117">The implementation of conditional access is based on policies.</span></span> <span data-ttu-id="fc2da-118">정책 기반 접근 방식은 원하는 액세스 요구 사항을 반영하므로 구성 환경을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-118">A policy-based approach simplifies your configuration experience because it follows the way you think about your access requirements.</span></span>  

<span data-ttu-id="fc2da-119">일반적으로 다음 패턴에 기반한 문을 사용하여 액세스 요구 사항을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-119">Typically, you define your access requirements using statements that are based on the following pattern:</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/10.png)

<span data-ttu-id="fc2da-121">두 개의 "*this*"를 실제 정보로 바꾸면 다음과 같이 일반적인 정책 문의 예제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-121">When you replace the two occurrences of “*this*” with real-world information, you have an example for a policy statement that probably looks familiar to you:</span></span>

<span data-ttu-id="fc2da-122">*계약자가 신뢰할 수 없는 네트워크에서 클라우드 앱에 액세스하려고 시도하는 경우 액세스를 차단합니다.*</span><span class="sxs-lookup"><span data-stu-id="fc2da-122">*When contractors are trying to access our cloud apps from networks that are not trusted, then block access.*</span></span>

<span data-ttu-id="fc2da-123">위 정책 문은 조건부 액세스의 권한을 강조하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-123">The policy statement above highlights the power of conditional access.</span></span> <span data-ttu-id="fc2da-124">계약자(**주체**)가 기본적으로 조건부 액세스로 클라우드 앱에 액세스할 수 있도록 허용하는 한편 액세스할 수 있는 조건을 정의할 수도 있습니다(**방법**).</span><span class="sxs-lookup"><span data-stu-id="fc2da-124">While you can enable contractors to basically access your cloud apps (**who**), with conditional access, you can also define conditions under which the access is possible (**how**).</span></span>

<span data-ttu-id="fc2da-125">Azure Active Directory 조건부 액세스의 컨텍스트에서</span><span class="sxs-lookup"><span data-stu-id="fc2da-125">In the context of Azure Active Directory conditional access,</span></span>

- <span data-ttu-id="fc2da-126">"**When this happens**"는 **조건 문**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-126">"**When this happens**" is called **condition statement**</span></span>
- <span data-ttu-id="fc2da-127">"**Then do this**"는 **제어 문**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-127">"**Then do this**" is called **controls**</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/11.png)

<span data-ttu-id="fc2da-129">조건 문과 제어 문의 조합은 조건부 액세스 정책을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-129">The combination of a condition statement with your controls represents a conditional access policy.</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a><span data-ttu-id="fc2da-131">컨트롤</span><span class="sxs-lookup"><span data-stu-id="fc2da-131">Controls</span></span>

<span data-ttu-id="fc2da-132">조건부 액세스 정책에서 제어 문은 조건 문을 충족할 때 발생해야 하는 상황을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-132">In a conditional access policy, controls define what it is that should happen when a condition statement has been satisfied.</span></span>  
<span data-ttu-id="fc2da-133">제어 문을 사용하면 추가 요구 사항에 따라 액세스를 차단하거나 액세스를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-133">With controls, you can either block access or allow access with additional requirements.</span></span>
<span data-ttu-id="fc2da-134">액세스를 허용하는 정책을 구성할 때는 요구 사항을 하나 이상 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-134">When you configure a policy that allows access, you need to select at least one requirement.</span></span>   

### <a name="grant-controls"></a><span data-ttu-id="fc2da-135">권한 부여 컨트롤</span><span class="sxs-lookup"><span data-stu-id="fc2da-135">Grant controls</span></span>
<span data-ttu-id="fc2da-136">Azure Active Directory의 현재 구현을 사용하면 다음 권한 부여 컨트롤 요구 사항을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-136">The current implementation of Azure Active Directory enables you to configure the following grant control requirements:</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/05.png)

- <span data-ttu-id="fc2da-138">**다단계 인증**: 다단계 인증을 통해 강력한 인증을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-138">**Multi-factor Authentication** - You can require strong authentication through multi-factor authentication.</span></span> <span data-ttu-id="fc2da-139">AD FS(Active Directory Federation Service)와 결합된 Azure Multi-Factor 또는 온-프레미스 다단계 인증 공급자를 공급자로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-139">As provider, you can use Azure Multi-Factor or an on-premises multi-factor authentication provider, combined with Active Directory Federation Services (AD FS).</span></span> <span data-ttu-id="fc2da-140">다단계 인증을 사용하면 유효한 사용자의 자격 증명에 액세스 할 수 있는 권한이 없는 사용자가 리소스에 액세스하지 못하도록 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-140">Using multi-factor authentication helps protect resources from being accessed by an unauthorized user who might have gained access to the credentials of a valid user.</span></span>

- <span data-ttu-id="fc2da-141">**준수 장치** - 장치 수준에서 조건부 액세스 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-141">**Compliant device** - You can set conditional access policies at the device level.</span></span> <span data-ttu-id="fc2da-142">정책을 준수하는 컴퓨터 또는 모바일 장치 관리에 등록된 모바일 장치만 조직의 리소스에 액세스할 수 있도록 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-142">You might set up a policy to only enable computers that are compliant, or mobile devices that are enrolled in a mobile device management to access your organization's resources.</span></span> <span data-ttu-id="fc2da-143">예를 들어 Intune을 사용하여 장치의 정책 준수를 확인한 다음 사용자가 응용 프로그램에 액세스하려고 할 때 해당 정책을 적용하기 위해 Azure AD에 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-143">For example, you can use Intune to check device compliance, and then report it to Azure AD for enforcement when the user attempts to access an application.</span></span> <span data-ttu-id="fc2da-144">Intune을 사용하여 앱 및 데이터를 보호하는 방법에 대한 자세한 지침은 [Microsoft Intune을 사용하여 앱 및 데이터 보호](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc2da-144">For detailed guidance about how to use Intune to protect apps and data, see [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune).</span></span> <span data-ttu-id="fc2da-145">또한 Intune을 사용하여 분실되거나 도난당한 장치에 대한 데이터 보호도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-145">You also can use Intune to enforce data protection for lost or stolen devices.</span></span> <span data-ttu-id="fc2da-146">자세한 정보는 [Microsoft Intune을 사용하여 전체 또는 선택적 초기화로 데이터 보호](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc2da-146">For more information, see [Help protect your data with full or selective wipe using Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).</span></span>

- <span data-ttu-id="fc2da-147">**도메인 가입 장치** - Azure Active Directory에 연결하는 데 사용한 장치가 온-프레미스 AD(Active Directory)에 도메인 가입되도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-147">**Domain joined device** – You can require the device you have used to connect to Azure Active Directory to be domain-joined to your on-premises Active Directory (AD).</span></span> <span data-ttu-id="fc2da-148">이 정책은 Windows 데스크톱, 랩톱 및 엔터프라이즈 태블릿에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-148">This policy applies to Windows desktops, laptops, and enterprise tablets.</span></span> 

<span data-ttu-id="fc2da-149">여러 컨트롤을 선택한 경우 정책이 처리될 때 모든 컨트롤이 필요한지 여부도 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-149">If you have multiple controls selected, you can also configure whether all of them are required when your policy is processed.</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a><span data-ttu-id="fc2da-151">세션 컨트롤</span><span class="sxs-lookup"><span data-stu-id="fc2da-151">Session controls</span></span>
<span data-ttu-id="fc2da-152">세션 컨트롤을 통해 클라우드 앱 내에서 환경을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-152">Session controls enable limiting experience within a cloud app.</span></span> <span data-ttu-id="fc2da-153">세션 컨트롤은 클라우드 앱에서 적용되고 Azure AD가 앱에 제공한 세션에 대한 추가 정보에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-153">The session controls are enforced by cloud apps and rely on additional information provided by Azure AD to the app about the session.</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a><span data-ttu-id="fc2da-155">앱에서 적용된 제한 사항 사용</span><span class="sxs-lookup"><span data-stu-id="fc2da-155">Use app enforced restrictions</span></span>
<span data-ttu-id="fc2da-156">이 컨트롤을 사용하여 Azure AD가 장치 정보를 클라우드 앱에 전달하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-156">You can use this control to require Azure AD to pass the device information to the cloud app.</span></span> <span data-ttu-id="fc2da-157">클라우드 앱은 이 컨트롤을 통해 사용자가 규격 장치 또는 도메인 가입 장치에서 들어오는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-157">This helps the cloud app know if the user is coming from a compliant device or domain joined device.</span></span> <span data-ttu-id="fc2da-158">이 컨트롤은 현재 SharePoint를 통해 클라우드 앱으로만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-158">This control is currently only supported with SharePoint as the cloud app.</span></span> <span data-ttu-id="fc2da-159">SharePoint에서는 장치 정보를 사용하여 사용자에게 장치 상태에 따라 제한된 환경이나 전체 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-159">SharePoint uses the device information to provide users a limited or full experience depending on the device state.</span></span>
<span data-ttu-id="fc2da-160">SharePoint를 통해 제한된 액세스를 요구하는 방법을 알아보려면[여기](https://aka.ms/spolimitedaccessdocs)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-160">To learn more about how to require limited access with SharePoint, go [here](https://aka.ms/spolimitedaccessdocs).</span></span>

## <a name="condition-statement"></a><span data-ttu-id="fc2da-161">조건 문</span><span class="sxs-lookup"><span data-stu-id="fc2da-161">Condition Statement</span></span>

<span data-ttu-id="fc2da-162">이전 섹션에서는 제어 문 형식으로 리소스에 대한 액세스를 차단하거나 제한하기 위해 지원되는 옵션을 소개했습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-162">The previous section has introduced you to supported options to block or restrict access to your resources in form of controls.</span></span> <span data-ttu-id="fc2da-163">조건부 액세스 정책에서는 제어 문이 조건 문의 형식으로 적용될 수 있도록 충족해야 할 조건을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-163">In a conditional access policy, you define the criteria that need to be met for your controls to be applied in form of a condition statement.</span></span>  

<span data-ttu-id="fc2da-164">조건 문에는 다음과 같은 할당이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-164">You can include the following assignments into your condition statement:</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/07.png)


- <span data-ttu-id="fc2da-166">**주체** - 대부분의 경우 제어 문을 특정 사용자 집합에 적용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-166">**Who** - In many cases, you want your controls to be applied to a specific set of users.</span></span> <span data-ttu-id="fc2da-167">조건 문에서 정책이 적용되는 사용자 및 그룹을 선택하여 이러한 집합을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-167">In a condition statement, you can define this set by selecting the users and groups your policy applies to.</span></span> <span data-ttu-id="fc2da-168">필요한 경우 사용자 집합을 제외하여 정책 대상에서 명시적으로 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-168">If necessary, you can also explicitly exclude a set of users from your policy by exempting them.</span></span>  
<span data-ttu-id="fc2da-169">사용자 및 그룹을 선택하여 정책이 적용되는 사용자 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-169">By selecting users and groups, you define the scope of users your policy applies to.</span></span>    

    ![제어](./media/active-directory-conditional-access-azure-portal/08.png)



- <span data-ttu-id="fc2da-171">**대상** - 일반적으로, 보호 관점에서 다른 앱보다 특별한 주의가 필요한, 사용자 환경에서 실행되는 특정 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-171">**What** - Typically, there are certain apps that are running in your environment requiring, from a protection perspective, more attention than others.</span></span> <span data-ttu-id="fc2da-172">예를 들어, 중요한 데이터에 액세스할 수 있는 앱이 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-172">This affects, for example, apps that have access to sensitive data.</span></span>
<span data-ttu-id="fc2da-173">클라우드 앱을 선택하면 정책이 적용되는 클라우드 앱의 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-173">By selecting cloud apps, you define the scope of cloud apps your policy applies to.</span></span> <span data-ttu-id="fc2da-174">필요한 경우 정책에서 일단의 앱을 명시적으로 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-174">If necessary, you can also explicitly exclude a set of apps from your policy.</span></span>

    ![제어](./media/active-directory-conditional-access-azure-portal/09.png)


- <span data-ttu-id="fc2da-176">**방법** - 앱에 대한 액세스를 제어할 수 있는 조건에서 수행하는 한, 사용자가 클라우드 앱에 액세스하는 방법에 대한 추가 제어 문을 부과할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-176">**How** - As long as access to your apps is performed under conditions you can control, there might be no need for imposing additional controls on how your cloud apps are accessed by your users.</span></span> <span data-ttu-id="fc2da-177">그러나 신뢰할 수 없는 네트워크 또는 정책을 준수하지 않는 장치에서 클라우드 앱에 대한 액세스를 수행하는 경우에는 상황이 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-177">However, things might look different if access to your cloud apps is performed, for example, from networks that are not trusted or devices that are not compliant.</span></span> <span data-ttu-id="fc2da-178">조건 문에서 앱에 대한 액세스를 수행하는 방법에 대한 추가 요구 사항이 있는 특정 액세스 조건을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-178">In a condition statement, you can define certain access conditions that have additional requirements for how access to your apps is performed.</span></span>

    ![조건](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a><span data-ttu-id="fc2da-180">조건</span><span class="sxs-lookup"><span data-stu-id="fc2da-180">Conditions</span></span>

<span data-ttu-id="fc2da-181">Azure Active Directory의 현재 구현에서 다음 영역에 대한 조건을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-181">In the current implementation of Azure Active Directory, you can define conditions for the following areas:</span></span>

- <span data-ttu-id="fc2da-182">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="fc2da-182">Sign-in risk</span></span>
- <span data-ttu-id="fc2da-183">장치 플랫폼</span><span class="sxs-lookup"><span data-stu-id="fc2da-183">Device platforms</span></span>
- <span data-ttu-id="fc2da-184">위치</span><span class="sxs-lookup"><span data-stu-id="fc2da-184">Locations</span></span>
- <span data-ttu-id="fc2da-185">클라이언트 앱</span><span class="sxs-lookup"><span data-stu-id="fc2da-185">Client apps</span></span>

![조건](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a><span data-ttu-id="fc2da-187">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="fc2da-187">Sign-in risk</span></span>

<span data-ttu-id="fc2da-188">로그인 위험은 로그인 시도를 사용자 계정의 합법적인 소유자가 수행하지 않았을 가능성을 추적하기 위해 Azure Active Directory에서 사용하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-188">A sign-in risk is an object that is used by Azure Active Directory to track the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span> <span data-ttu-id="fc2da-189">이 개체에서 가능성(높음, 중간 또는 낮음)은 [로그인 위험 수준](active-directory-reporting-risk-events.md#risk-level)이라는 특성의 형태로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-189">In this object, the likelihood (High, Medium, or Low) is stored in form of an attribute called [sign-in risk level](active-directory-reporting-risk-events.md#risk-level).</span></span> <span data-ttu-id="fc2da-190">Azure Active Directory에서 로그인 위험을 검색한 경우 이 개체는 사용자의 로그인 동안 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-190">This object is generated during a sign-in of a user if sign-in risks have been detected by Azure Active Directory.</span></span> <span data-ttu-id="fc2da-191">자세한 내용은 [위험한 로그인](active-directory-identityprotection.md#risky-sign-ins)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc2da-191">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span>  
<span data-ttu-id="fc2da-192">계산된 로그인 위험 수준을 조건부 액세스 정책의 조건으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-192">You can use the calculated sign-in risk level as condition in a conditional access policy.</span></span> 

![조건](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a><span data-ttu-id="fc2da-194">장치 플랫폼</span><span class="sxs-lookup"><span data-stu-id="fc2da-194">Device platforms</span></span>

<span data-ttu-id="fc2da-195">장치 플랫폼은 다음 장치에서 실행되는 운영 체제를 특징으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-195">The device platform is characterized by the operating system that is running on your device:</span></span>

- <span data-ttu-id="fc2da-196">Android</span><span class="sxs-lookup"><span data-stu-id="fc2da-196">Android</span></span>
- <span data-ttu-id="fc2da-197">iOS</span><span class="sxs-lookup"><span data-stu-id="fc2da-197">iOS</span></span>
- <span data-ttu-id="fc2da-198">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fc2da-198">Windows Phone</span></span>
- <span data-ttu-id="fc2da-199">Windows</span><span class="sxs-lookup"><span data-stu-id="fc2da-199">Windows</span></span>
- <span data-ttu-id="fc2da-200">macOS(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="fc2da-200">macOS (preview).</span></span> 

![조건](./media/active-directory-conditional-access-azure-portal/02.png)

<span data-ttu-id="fc2da-202">정책의 대상에 포함된 장치 플랫폼뿐만 아니라 정책에서 제외되는 장치 플랫폼도 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-202">You can define the device platforms that are included as well as device platforms that are exempted from a policy.</span></span>  
<span data-ttu-id="fc2da-203">정책에서 장치 플랫폼을 사용하려면 먼저 [구성] 토글을 **예**로 변경한 다음, 정책이 적용되는 장치 플랫폼을 모두 또는 개별적으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-203">To use device platforms in the policy, first change the configure toggles to **Yes**, and then select all or individual device platforms the policy applies to.</span></span> <span data-ttu-id="fc2da-204">개별 장치 플랫폼을 선택하면 해당 플랫폼에만 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-204">If you select individual device platforms, the policy has only an impact on these platforms.</span></span> <span data-ttu-id="fc2da-205">이 경우 지원되는 다른 플랫폼에 대한 로그인은 정책의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-205">In this case, sign-ins to other supported platforms are not impacted by the policy.</span></span>


### <a name="locations"></a><span data-ttu-id="fc2da-206">위치</span><span class="sxs-lookup"><span data-stu-id="fc2da-206">Locations</span></span>

<span data-ttu-id="fc2da-207">위치는 Azure Active Directory에 연결하는 데 사용한 클라이언트의 IP 주소로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-207">The location is identified by the IP address of the client you have used to connect to Azure Active Directory.</span></span> <span data-ttu-id="fc2da-208">이 조건에서는 **명명된 위치** 및 **MFA 신뢰할 수 있는 IP**를 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-208">This condition requires you to be familiar with **named locations** and **MFA trusted IPs**.</span></span>  

<span data-ttu-id="fc2da-209">**명명된 위치**는 조직 내에서 신뢰할 수 있는 IP 주소 범위에 레이블을 지정할 수 있는 Azure Active Directory의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-209">**Named locations** is a feature of Azure Active Directory which allows you to label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="fc2da-210">사용자 환경에서 조건부 액세스와 함께 [위험 이벤트](active-directory-reporting-risk-events.md) 검색의 컨텍스트에서 명명된 위치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-210">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md) as well as conditional access.</span></span> <span data-ttu-id="fc2da-211">Azure Active Directory에서 명명된 위치 구성에 대한 자세한 내용은 [Azure Active Directory의 명명된 위치](active-directory-named-locations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc2da-211">For more details about configuring named locations in Azure Active Directory, see [named locations in Azure Active Directory](active-directory-named-locations.md).</span></span>

<span data-ttu-id="fc2da-212">구성할 수 있는 위치의 수는 Azure AD에서 관련된 개체의 크기에 따라 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-212">The number of locations you can configure is constrained by the size of the related object in Azure AD.</span></span> <span data-ttu-id="fc2da-213">다음을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-213">You can configure:</span></span>
 
 - <span data-ttu-id="fc2da-214">최대 500개 IP 범위로 명명된 하나의 위치</span><span class="sxs-lookup"><span data-stu-id="fc2da-214">One named location with up to 500 IP ranges</span></span>
 - <span data-ttu-id="fc2da-215">각각에 한 개의 IP 범위로 할당된 최대 60개의 명명된 위치(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="fc2da-215">A maximum of 60 named locations (preview) with one IP range assigned to each of them</span></span> 


<span data-ttu-id="fc2da-216">**MFA 신뢰할 수 있는 IP**는 조직의 로컬 인트라넷을 나타내는 신뢰할 수 있는 IP 주소 범위를 정의할 수 있는 다단계 인증 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-216">**MFA trusted IPs** is a feature of multi-factor authentication that enables you to define trusted IP address ranges representing your organization's local intranet.</span></span> <span data-ttu-id="fc2da-217">위치 조건을 구성하면 신뢰할 수 있는 IP를 통해 조직의 네트워크와 다른 모든 위치에서 수행되는 연결을 구별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-217">When you configure a location conditions, Trusted IPs enables you to distinguish between connections made from your organization's network and all other locations.</span></span> <span data-ttu-id="fc2da-218">자세한 내용은 [신뢰할 수 있는 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc2da-218">For more details, see [trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>  



<span data-ttu-id="fc2da-219">모든 위치 또는 모든 신뢰할 수 있는 IP를 포함하거나, 모든 신뢰할 수 있는 IP를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-219">You can either include all locations or all trusted IPs and you can exclude all trusted IPs.</span></span>

![조건](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a><span data-ttu-id="fc2da-221">클라이언트 앱</span><span class="sxs-lookup"><span data-stu-id="fc2da-221">Client app</span></span>

<span data-ttu-id="fc2da-222">클라이언트 앱은 Azure Active Directory에 연결하는 데 사용한 일반적 수준의 앱(웹 브라우저, 모바일 앱, 데스크톱 클라이언트)이거나, 구체적으로 Exchange Active Sync를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-222">The client app can be either on a generic level the app (web browser, mobile app, desktop client) you have used to connect to Azure Active Directory or you can specifically select Exchange Active Sync.</span></span>  
<span data-ttu-id="fc2da-223">레거시 인증은 최신 인증을 사용하지 않는 이전 Office 클라이언트와 같은 기본 인증을 사용하는 클라이언트를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-223">Legacy authentication refers to clients using basic authentication such as older Office clients that don’t use modern authentication.</span></span> <span data-ttu-id="fc2da-224">현재 레거시 인증에서는 조건부 액세스를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-224">Conditional access is currently not supported with legacy authentication.</span></span>

![조건](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a><span data-ttu-id="fc2da-226">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="fc2da-226">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="fc2da-227">앱에 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="fc2da-227">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="fc2da-228">대다수 사용 환경에서는 다른 앱보다 특히 높은 수준의 보호를 요구하는 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-228">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="fc2da-229">예를 들어 중요한 데이터에 액세스할 수 있는 앱의 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-229">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="fc2da-230">이러한 앱에 또 다른 보호 계층을 추가하려는 경우 사용자가 이러한 앱에 액세스할 때 다단계 인증을 요구하는 조건부 액세스 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-230">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="fc2da-231">신뢰할 수 없는 네트워크에서 액세스하기 위한 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="fc2da-231">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="fc2da-232">이 시나리오는 다단계 인증에 대한 요구 사항을 추가하기 때문에 이전 시나리오와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-232">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="fc2da-233">그러나 주요 차이점은 이 요구 사항에 대한 조건에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-233">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="fc2da-234">이전 시나리오는 중요한 데이터에 액세스할 수 있는 앱에 초점을 맞추었지만, 이 시나리오는 신뢰할 수 있는 위치에 초점을 맞추고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-234">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="fc2da-235">즉 사용자가 신뢰할 수 없는 네트워크에서 앱에 액세스하는 경우 다단계 인증에 대한 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-235">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="fc2da-236">신뢰할 수 있는 장치만 Office 365 서비스에 액세스 가능</span><span class="sxs-lookup"><span data-stu-id="fc2da-236">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="fc2da-237">사용자 환경에서 Intune을 사용하는 경우 Azure 콘솔에서 조건부 액세스 정책 인터페이스를 즉시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-237">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="fc2da-238">많은 Intune 고객이 조건부 액세스를 사용하여 신뢰할 수 있는 장치만 Office 365 서비스에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-238">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="fc2da-239">즉 모바일 장치가 Intune에 등록되고 준수 정책 요구 사항을 충족하며 Windows PC가 온-프레미스 도메인에 가입되어 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-239">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="fc2da-240">주요 개선 사항은 각 Office 365 서비스마다 동일한 정책을 설정할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-240">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="fc2da-241">즉, 새 정책을 만들 때 조건부 액세스로 보호하려는 각 Office 365 앱을 포함하도록 클라우드 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fc2da-241">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc2da-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc2da-242">Next steps</span></span>

<span data-ttu-id="fc2da-243">조건부 액세스 정책을 구성하는 방법을 알아보려면 [Azure Active Directory에서 조건부 액세스 시작](active-directory-conditional-access-azure-portal-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc2da-243">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>

<span data-ttu-id="fc2da-244">사용자 환경에 대한 조건부 액세스 정책을 구성할 준비가 완료된 경우 [Azure Active Directory의 조건부 액세스 모범 사례](active-directory-conditional-access-best-practices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc2da-244">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span> 