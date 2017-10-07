---
title: "Active Directory의 조건부 액세스 aaaAzure | Microsoft Docs"
description: "Tooapplications 액세스를 인증할 때 특정 조건에 대 한 Azure Active Directory toocheck에서 조건부 액세스 제어를 사용 합니다."
services: active-directory
keywords: "조건부 액세스 tooapps, Azure AD 사용 하 여 조건부 액세스 조건부 액세스 정책 toocompany 리소스 액세스 보안"
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
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a><span data-ttu-id="2bd07-104">Azure Active Directory 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="2bd07-104">Conditional access in Azure Active Directory</span></span>

<span data-ttu-id="2bd07-105">먼저 모바일, 클라우드 우선 세계에서 Azure Active Directory single sign on toodevices, 앱 및 서비스를 어디에서 든 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-105">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="2bd07-106">Hello (BYOD) 하는 장치의 확산으로 회사 네트워크에 해제 작업 하 고 타사 SaaS 앱, IT 전문가 두 가지 상반 되 목표를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-106">With hello proliferation of devices (including BYOD), work off corporate networks, and 3rd party SaaS apps, IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="2bd07-107">있어 선택의 폭 hello 최종 사용자에 게 toobe 생산성을 아무 곳에 나 때마다</span><span class="sxs-lookup"><span data-stu-id="2bd07-107">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="2bd07-108">언제 든 지 hello 회사 자산을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-108">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="2bd07-109">tooimprove 생산성, Azure Active Directory 옵션 tooaccess 광범위 한 범위를 가진 사용자가 회사 자산을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-109">tooimprove productivity, Azure Active Directory provides your users with a broad range of options tooaccess your corporate assets.</span></span> <span data-ttu-id="2bd07-110">응용 프로그램 액세스 관리를 Azure Active Directory 사용 하면 tooensure만 *적임자 hello* 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-110">With application access management, Azure Active Directory enables you tooensure that only *hello right people* can access your applications.</span></span> <span data-ttu-id="2bd07-111">어떻게 할까요 toohave hello 적임자 특정 조건에서 리소스 액세스 하는 방법을 보다 자세히 제어?</span><span class="sxs-lookup"><span data-stu-id="2bd07-111">What if you want toohave more control over how hello right people are accessing your resources under certain conditions?</span></span> <span data-ttu-id="2bd07-112">도 hello에 대해서도 tooblock 액세스 toocertain 앱 하려는 조건이 있는 경우에 어떻게 *사용자를 마우스 오른쪽 단추로*?</span><span class="sxs-lookup"><span data-stu-id="2bd07-112">What if you even have conditions under which you want tooblock access toocertain apps even for hello *right people*?</span></span> <span data-ttu-id="2bd07-113">예를 들어 것 확인 하면에 대 한 hello 적임자; 신뢰할 수 있는 네트워크에서 특정 앱에 액세스 하는 경우 그러나 있습니다 하지 않을 tooaccess로 신뢰 하지 않는 네트워크에서 이러한 앱.</span><span class="sxs-lookup"><span data-stu-id="2bd07-113">For example, it might be OK for you if hello right people are accessing certain apps from a trusted network; however, you might not want them tooaccess these apps from a network you don't trust.</span></span> <span data-ttu-id="2bd07-114">조건부 액세스를 사용하면 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-114">You can address these questions using conditional access.</span></span>

<span data-ttu-id="2bd07-115">조건부 액세스는 Azure Active Directory를 사용 하면 특정 조건에 따라 해당 환경에 대 한 액세스 tooapps hello에 tooenforce 컨트롤의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-115">Conditional access is a capability of Azure Active Directory that enables you tooenforce controls on hello access tooapps in your environment based on specific conditions.</span></span> <span data-ttu-id="2bd07-116">컨트롤을 사용 하거나 요구 사항이 추가로 적용 toohello 액세스에 연결할 수 있습니다 또는 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-116">With controls, you can either tie additional requirements toohello access or you can block it.</span></span> <span data-ttu-id="2bd07-117">hello 구현의 조건부 액세스 정책을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-117">hello implementation of conditional access is based on policies.</span></span> <span data-ttu-id="2bd07-118">정책 기반 접근 방식을 액세스 요구 사항에 대해 생각 하는 hello 방식에 따라 때문에 구성 환경을 단순화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-118">A policy-based approach simplifies your configuration experience because it follows hello way you think about your access requirements.</span></span>  

<span data-ttu-id="2bd07-119">일반적으로 hello 패턴을 기반으로 하는 문을 사용 하 여 액세스 요구 사항을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-119">Typically, you define your access requirements using statements that are based on hello following pattern:</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/10.png)

<span data-ttu-id="2bd07-121">Hello 두 항목을 바꿀 때 "*이*" 친숙 한 tooyou 하 게 보일 것 하는 정책 설명 위한 예로 실제 정보를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-121">When you replace hello two occurrences of “*this*” with real-world information, you have an example for a policy statement that probably looks familiar tooyou:</span></span>

<span data-ttu-id="2bd07-122">*계약자 tooaccess 신뢰할 수 없는 네트워크에서 우리의 클라우드 앱을 늘리려는 경우 액세스를 차단 합니다.*</span><span class="sxs-lookup"><span data-stu-id="2bd07-122">*When contractors are trying tooaccess our cloud apps from networks that are not trusted, then block access.*</span></span>

<span data-ttu-id="2bd07-123">위의 hello 정책 설명에는 조건부 액세스의 hello 전원 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-123">hello policy statement above highlights hello power of conditional access.</span></span> <span data-ttu-id="2bd07-124">계약자 toobasically 클라우드 앱에 액세스 하는 동안 사용할 수 있습니다 (**가**), 조건부 액세스로 정의할 수도 있습니다는 hello에서 액세스를 허용 하는 조건 (**어떻게**).</span><span class="sxs-lookup"><span data-stu-id="2bd07-124">While you can enable contractors toobasically access your cloud apps (**who**), with conditional access, you can also define conditions under which hello access is possible (**how**).</span></span>

<span data-ttu-id="2bd07-125">조건부 액세스는 Azure Active Directory의 hello 컨텍스트에서</span><span class="sxs-lookup"><span data-stu-id="2bd07-125">In hello context of Azure Active Directory conditional access,</span></span>

- <span data-ttu-id="2bd07-126">"**When this happens**"는 **조건 문**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-126">"**When this happens**" is called **condition statement**</span></span>
- <span data-ttu-id="2bd07-127">"**Then do this**"는 **제어 문**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-127">"**Then do this**" is called **controls**</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/11.png)

<span data-ttu-id="2bd07-129">컨트롤을 조건 문으로 hello 조합의 조건부 액세스 정책을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-129">hello combination of a condition statement with your controls represents a conditional access policy.</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a><span data-ttu-id="2bd07-131">컨트롤</span><span class="sxs-lookup"><span data-stu-id="2bd07-131">Controls</span></span>

<span data-ttu-id="2bd07-132">조건부 액세스 정책에서 제어 문은 조건 문을 충족할 때 발생해야 하는 상황을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-132">In a conditional access policy, controls define what it is that should happen when a condition statement has been satisfied.</span></span>  
<span data-ttu-id="2bd07-133">제어 문을 사용하면 추가 요구 사항에 따라 액세스를 차단하거나 액세스를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-133">With controls, you can either block access or allow access with additional requirements.</span></span>
<span data-ttu-id="2bd07-134">Tooselect 필요한 액세스를 허용 하는 정책을 구성할 때 하나 이상의 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-134">When you configure a policy that allows access, you need tooselect at least one requirement.</span></span>   

### <a name="grant-controls"></a><span data-ttu-id="2bd07-135">권한 부여 컨트롤</span><span class="sxs-lookup"><span data-stu-id="2bd07-135">Grant controls</span></span>
<span data-ttu-id="2bd07-136">Azure Active Directory의 현재 구현 hello tooconfigure hello를 부여 제어 요구 사항을 준수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-136">hello current implementation of Azure Active Directory enables you tooconfigure hello following grant control requirements:</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/05.png)

- <span data-ttu-id="2bd07-138">**다단계 인증**: 다단계 인증을 통해 강력한 인증을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-138">**Multi-factor Authentication** - You can require strong authentication through multi-factor authentication.</span></span> <span data-ttu-id="2bd07-139">AD FS(Active Directory Federation Service)와 결합된 Azure Multi-Factor 또는 온-프레미스 다단계 인증 공급자를 공급자로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-139">As provider, you can use Azure Multi-Factor or an on-premises multi-factor authentication provider, combined with Active Directory Federation Services (AD FS).</span></span> <span data-ttu-id="2bd07-140">Multi-factor authentication을 사용 하 여 수 있는 액세스 권한을 받을 유효한 사용자의 자격 증명 toohello 권한이 없는 사용자가 액세스 중인 리소스를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-140">Using multi-factor authentication helps protect resources from being accessed by an unauthorized user who might have gained access toohello credentials of a valid user.</span></span>

- <span data-ttu-id="2bd07-141">**준수 장치** -hello 장치 수준에서 조건부 액세스 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-141">**Compliant device** - You can set conditional access policies at hello device level.</span></span> <span data-ttu-id="2bd07-142">준수, 정책 tooonly 사용 컴퓨터를 설정할 수 있습니다는 모바일 장치 또는 조직의 리소스 모바일 장치 관리 tooaccess에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-142">You might set up a policy tooonly enable computers that are compliant, or mobile devices that are enrolled in a mobile device management tooaccess your organization's resources.</span></span> <span data-ttu-id="2bd07-143">예를 들어 Intune toocheck 장치 규정 준수를 사용할 수 있으며 다음 보고 tooAzure 적용에 대 한 AD hello 사용자가 응용 프로그램 tooaccess 시도할 때.</span><span class="sxs-lookup"><span data-stu-id="2bd07-143">For example, you can use Intune toocheck device compliance, and then report it tooAzure AD for enforcement when hello user attempts tooaccess an application.</span></span> <span data-ttu-id="2bd07-144">Toouse Intune tooprotect 앱 및 데이터를 참조 하는 방법에 대 한 자세한 지침은 [Microsoft Intune로 앱 및 데이터 보호](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-144">For detailed guidance about how toouse Intune tooprotect apps and data, see [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune).</span></span> <span data-ttu-id="2bd07-145">분실 하거나 도난당 한 장치에 대 한 Intune tooenforce 데이터 보호를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-145">You also can use Intune tooenforce data protection for lost or stolen devices.</span></span> <span data-ttu-id="2bd07-146">자세한 정보는 [Microsoft Intune을 사용하여 전체 또는 선택적 초기화로 데이터 보호](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bd07-146">For more information, see [Help protect your data with full or selective wipe using Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).</span></span>

- <span data-ttu-id="2bd07-147">**도메인 가입 장치** – hello 장치 tooconnect tooAzure Active Directory toobe 도메인에 가입 된 tooyour를 사용한 온-프레미스 AD (Active Directory)를 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-147">**Domain joined device** – You can require hello device you have used tooconnect tooAzure Active Directory toobe domain-joined tooyour on-premises Active Directory (AD).</span></span> <span data-ttu-id="2bd07-148">이 정책은 tooWindows 데스크톱, 랩톱 및 태블릿 엔터프라이즈 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-148">This policy applies tooWindows desktops, laptops, and enterprise tablets.</span></span> 

<span data-ttu-id="2bd07-149">여러 컨트롤을 선택한 경우 정책이 처리될 때 모든 컨트롤이 필요한지 여부도 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-149">If you have multiple controls selected, you can also configure whether all of them are required when your policy is processed.</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a><span data-ttu-id="2bd07-151">세션 컨트롤</span><span class="sxs-lookup"><span data-stu-id="2bd07-151">Session controls</span></span>
<span data-ttu-id="2bd07-152">세션 컨트롤을 통해 클라우드 앱 내에서 환경을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-152">Session controls enable limiting experience within a cloud app.</span></span> <span data-ttu-id="2bd07-153">hello 세션 컨트롤은 클라우드 응용 프로그램에 의해 적용 및 hello 세션에 대 한 Azure AD toohello 응용 프로그램에서 제공 하는 추가 정보에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-153">hello session controls are enforced by cloud apps and rely on additional information provided by Azure AD toohello app about hello session.</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a><span data-ttu-id="2bd07-155">앱에서 적용된 제한 사항 사용</span><span class="sxs-lookup"><span data-stu-id="2bd07-155">Use app enforced restrictions</span></span>
<span data-ttu-id="2bd07-156">이 제어 toorequire Azure AD toopass hello 장치 정보 toohello 클라우드 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-156">You can use this control toorequire Azure AD toopass hello device information toohello cloud app.</span></span> <span data-ttu-id="2bd07-157">이로써 hello 클라우드 앱 hello 사용자는 준수 장치 또는 도메인에 가입 된 장치에서 발생 하는지 여부를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-157">This helps hello cloud app know if hello user is coming from a compliant device or domain joined device.</span></span> <span data-ttu-id="2bd07-158">이 컨트롤은 현재 SharePoint hello 클라우드 앱 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-158">This control is currently only supported with SharePoint as hello cloud app.</span></span> <span data-ttu-id="2bd07-159">SharePoint은 hello 장치 상태에 따라 hello 장치 정보 tooprovide 사용자가 제한 된 또는 전체 환경을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-159">SharePoint uses hello device information tooprovide users a limited or full experience depending on hello device state.</span></span>
<span data-ttu-id="2bd07-160">toorequire SharePoint 사용 하 여 액세스를 제한 하는 방법에 대 한 자세한 toolearn 이동 [여기](https://aka.ms/spolimitedaccessdocs)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-160">toolearn more about how toorequire limited access with SharePoint, go [here](https://aka.ms/spolimitedaccessdocs).</span></span>

## <a name="condition-statement"></a><span data-ttu-id="2bd07-161">조건 문</span><span class="sxs-lookup"><span data-stu-id="2bd07-161">Condition Statement</span></span>

<span data-ttu-id="2bd07-162">이전 섹션 hello toosupported 옵션 tooblock가 도입 하거나 컨트롤의 형태로 tooyour 리소스에 액세스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-162">hello previous section has introduced you toosupported options tooblock or restrict access tooyour resources in form of controls.</span></span> <span data-ttu-id="2bd07-163">조건부 액세스 정책에서 조건 문의 폼에 적용 하 여 컨트롤 toobe에 대 한 toobe 충족 해야 하는 hello 조건을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-163">In a conditional access policy, you define hello criteria that need toobe met for your controls toobe applied in form of a condition statement.</span></span>  

<span data-ttu-id="2bd07-164">Hello에 조건 문으로 할당 다음을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-164">You can include hello following assignments into your condition statement:</span></span>

![제어](./media/active-directory-conditional-access-azure-portal/07.png)


- <span data-ttu-id="2bd07-166">**가** -사용자 제어 적용 toobe tooa 특정 사용자 집합을 원하는 대부분의 경우에서.</span><span class="sxs-lookup"><span data-stu-id="2bd07-166">**Who** - In many cases, you want your controls toobe applied tooa specific set of users.</span></span> <span data-ttu-id="2bd07-167">조건 문으로 hello 사용자 및 사용자 정책이 적용 되는 그룹을 선택 하 여이 집합을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-167">In a condition statement, you can define this set by selecting hello users and groups your policy applies to.</span></span> <span data-ttu-id="2bd07-168">필요한 경우 사용자 집합을 제외하여 정책 대상에서 명시적으로 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-168">If necessary, you can also explicitly exclude a set of users from your policy by exempting them.</span></span>  
<span data-ttu-id="2bd07-169">사용자 및 그룹을 선택 하면 사용자 정책에 적용 됩니다. hello 범위를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-169">By selecting users and groups, you define hello scope of users your policy applies to.</span></span>    

    ![제어](./media/active-directory-conditional-access-azure-portal/08.png)



- <span data-ttu-id="2bd07-171">**대상** - 일반적으로, 보호 관점에서 다른 앱보다 특별한 주의가 필요한, 사용자 환경에서 실행되는 특정 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-171">**What** - Typically, there are certain apps that are running in your environment requiring, from a protection perspective, more attention than others.</span></span> <span data-ttu-id="2bd07-172">이 영향을 주는 예를 들어 toosensitive 데이터에 액세스 되는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-172">This affects, for example, apps that have access toosensitive data.</span></span>
<span data-ttu-id="2bd07-173">클라우드 앱을 선택 하면 사용자 정책이 적용 되는 클라우드 응용 프로그램의 hello 범위를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-173">By selecting cloud apps, you define hello scope of cloud apps your policy applies to.</span></span> <span data-ttu-id="2bd07-174">필요한 경우 정책에서 일단의 앱을 명시적으로 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-174">If necessary, you can also explicitly exclude a set of apps from your policy.</span></span>

    ![제어](./media/active-directory-conditional-access-azure-portal/09.png)


- <span data-ttu-id="2bd07-176">**어떻게** -으로 tooyour 앱 액세스 조건 제어할 수 없어 수에 추가 컨트롤을 부과 필요가 없을 수 어떻게 클라우드 앱 액세스 사용자에 게에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-176">**How** - As long as access tooyour apps is performed under conditions you can control, there might be no need for imposing additional controls on how your cloud apps are accessed by your users.</span></span> <span data-ttu-id="2bd07-177">그러나 작업은 수행 하는 경우 액세스 tooyour 클라우드 앱은, 예를 들어 신뢰할 수 없는 네트워크 또는 규정을 준수 하지 않은 장치에서 다르게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-177">However, things might look different if access tooyour cloud apps is performed, for example, from networks that are not trusted or devices that are not compliant.</span></span> <span data-ttu-id="2bd07-178">조건 문에서 액세스 tooyour 앱을 수행 하는 방법에 대 한 추가 요구 사항이 포함 된 특정 액세스 조건을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-178">In a condition statement, you can define certain access conditions that have additional requirements for how access tooyour apps is performed.</span></span>

    ![조건](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a><span data-ttu-id="2bd07-180">조건</span><span class="sxs-lookup"><span data-stu-id="2bd07-180">Conditions</span></span>

<span data-ttu-id="2bd07-181">Hello Azure Active Directory의 현재 구현에서는 다음 영역 hello에 대 한 조건을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-181">In hello current implementation of Azure Active Directory, you can define conditions for hello following areas:</span></span>

- <span data-ttu-id="2bd07-182">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="2bd07-182">Sign-in risk</span></span>
- <span data-ttu-id="2bd07-183">장치 플랫폼</span><span class="sxs-lookup"><span data-stu-id="2bd07-183">Device platforms</span></span>
- <span data-ttu-id="2bd07-184">위치</span><span class="sxs-lookup"><span data-stu-id="2bd07-184">Locations</span></span>
- <span data-ttu-id="2bd07-185">클라이언트 앱</span><span class="sxs-lookup"><span data-stu-id="2bd07-185">Client apps</span></span>

![조건](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a><span data-ttu-id="2bd07-187">로그인 위험</span><span class="sxs-lookup"><span data-stu-id="2bd07-187">Sign-in risk</span></span>

<span data-ttu-id="2bd07-188">로그인 위험은 로그인 시도 하는 사용자 계정의 hello 합법적인 소유자에 의해 수행 되지 않았습니다 tootrack hello 가능성 Azure Active Directory에서 사용 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-188">A sign-in risk is an object that is used by Azure Active Directory tootrack hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span> <span data-ttu-id="2bd07-189">이 개체에 hello 가능성 (높음, 중간 또는 낮음) 라는 특성의 형식으로 저장 됩니다 [로그인 위험 수준](active-directory-reporting-risk-events.md#risk-level)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-189">In this object, hello likelihood (High, Medium, or Low) is stored in form of an attribute called [sign-in risk level](active-directory-reporting-risk-events.md#risk-level).</span></span> <span data-ttu-id="2bd07-190">Azure Active Directory에서 로그인 위험을 검색한 경우 이 개체는 사용자의 로그인 동안 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-190">This object is generated during a sign-in of a user if sign-in risks have been detected by Azure Active Directory.</span></span> <span data-ttu-id="2bd07-191">자세한 내용은 [위험한 로그인](active-directory-identityprotection.md#risky-sign-ins)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bd07-191">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span>  
<span data-ttu-id="2bd07-192">조건부 액세스 정책에서 조건으로 계산 하는 hello 로그인 위험 수준을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-192">You can use hello calculated sign-in risk level as condition in a conditional access policy.</span></span> 

![조건](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a><span data-ttu-id="2bd07-194">장치 플랫폼</span><span class="sxs-lookup"><span data-stu-id="2bd07-194">Device platforms</span></span>

<span data-ttu-id="2bd07-195">hello 장치 플랫폼의 장치에서 실행 되는 hello 운영 체제 특징은:</span><span class="sxs-lookup"><span data-stu-id="2bd07-195">hello device platform is characterized by hello operating system that is running on your device:</span></span>

- <span data-ttu-id="2bd07-196">Android</span><span class="sxs-lookup"><span data-stu-id="2bd07-196">Android</span></span>
- <span data-ttu-id="2bd07-197">iOS</span><span class="sxs-lookup"><span data-stu-id="2bd07-197">iOS</span></span>
- <span data-ttu-id="2bd07-198">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="2bd07-198">Windows Phone</span></span>
- <span data-ttu-id="2bd07-199">Windows</span><span class="sxs-lookup"><span data-stu-id="2bd07-199">Windows</span></span>
- <span data-ttu-id="2bd07-200">macOS(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="2bd07-200">macOS (preview).</span></span> 

![조건](./media/active-directory-conditional-access-azure-portal/02.png)

<span data-ttu-id="2bd07-202">정책에서 제외 하는 장치 플랫폼 뿐만 아니라 포함 된 hello 장치 플랫폼을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-202">You can define hello device platforms that are included as well as device platforms that are exempted from a policy.</span></span>  
<span data-ttu-id="2bd07-203">toouse hello 정책에서 장치 플랫폼에 첫 번째 변경 hello 구성 설정/해제 너무**예**, 모두를 선택 하거나 개별 장치 플랫폼 hello 정책에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-203">toouse device platforms in hello policy, first change hello configure toggles too**Yes**, and then select all or individual device platforms hello policy applies to.</span></span> <span data-ttu-id="2bd07-204">개별 장치 플랫폼을 선택 하면 hello 정책 이러한 플랫폼에만 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-204">If you select individual device platforms, hello policy has only an impact on these platforms.</span></span> <span data-ttu-id="2bd07-205">이 경우 로그인 tooother 지원 플랫폼 hello 정책에 의해의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-205">In this case, sign-ins tooother supported platforms are not impacted by hello policy.</span></span>


### <a name="locations"></a><span data-ttu-id="2bd07-206">위치</span><span class="sxs-lookup"><span data-stu-id="2bd07-206">Locations</span></span>

<span data-ttu-id="2bd07-207">hello 위치 식별 tooconnect tooAzure Active Directory의 hello 클라이언트의 hello IP 주소로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-207">hello location is identified by hello IP address of hello client you have used tooconnect tooAzure Active Directory.</span></span> <span data-ttu-id="2bd07-208">이 조건은 필요 toobe 익숙한 **명명 된 위치를** 및 **MFA 신뢰할 수 있는 Ip**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-208">This condition requires you toobe familiar with **named locations** and **MFA trusted IPs**.</span></span>  

<span data-ttu-id="2bd07-209">**지정 된 위치** 조직에 toolabel 신뢰할 수 있는 IP 주소 범위 수 있는 Azure Active Directory의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-209">**Named locations** is a feature of Azure Active Directory which allows you toolabel trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="2bd07-210">사용자 환경에서의 hello 검색의 hello 컨텍스트에서 명명 된 위치를 사용할 수 있습니다 [이벤트 위험](active-directory-reporting-risk-events.md) 조건부 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-210">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md) as well as conditional access.</span></span> <span data-ttu-id="2bd07-211">Azure Active Directory에서 명명된 위치 구성에 대한 자세한 내용은 [Azure Active Directory의 명명된 위치](active-directory-named-locations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bd07-211">For more details about configuring named locations in Azure Active Directory, see [named locations in Azure Active Directory](active-directory-named-locations.md).</span></span>

<span data-ttu-id="2bd07-212">구성할 수 있습니다 위치 hello 수는 Azure AD에서 hello 관련된 개체의 hello 크기에 따라 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-212">hello number of locations you can configure is constrained by hello size of hello related object in Azure AD.</span></span> <span data-ttu-id="2bd07-213">다음을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-213">You can configure:</span></span>
 
 - <span data-ttu-id="2bd07-214">명명 된 위치를 하나 too500 IP 범위를</span><span class="sxs-lookup"><span data-stu-id="2bd07-214">One named location with up too500 IP ranges</span></span>
 - <span data-ttu-id="2bd07-215">그 중 하나의 IP 할당 범위 tooeach와 최대 60 명명 된 위치 (미리 보기)</span><span class="sxs-lookup"><span data-stu-id="2bd07-215">A maximum of 60 named locations (preview) with one IP range assigned tooeach of them</span></span> 


<span data-ttu-id="2bd07-216">**신뢰할 수 있는 Ip MFA** 조직의 로컬 인트라넷 나타내는 toodefine 신뢰할 수 있는 IP 주소 범위를 사용 하면 multi-factor authentication의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-216">**MFA trusted IPs** is a feature of multi-factor authentication that enables you toodefine trusted IP address ranges representing your organization's local intranet.</span></span> <span data-ttu-id="2bd07-217">위치 조건을 구성할 때 신뢰할 수 있는 Ip 사용 하면 조직 네트워크의 모든 위치에서 만든 연결 사이의 toodistinguish 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-217">When you configure a location conditions, Trusted IPs enables you toodistinguish between connections made from your organization's network and all other locations.</span></span> <span data-ttu-id="2bd07-218">자세한 내용은 [신뢰할 수 있는 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bd07-218">For more details, see [trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>  



<span data-ttu-id="2bd07-219">모든 위치 또는 모든 신뢰할 수 있는 IP를 포함하거나, 모든 신뢰할 수 있는 IP를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-219">You can either include all locations or all trusted IPs and you can exclude all trusted IPs.</span></span>

![조건](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a><span data-ttu-id="2bd07-221">클라이언트 앱</span><span class="sxs-lookup"><span data-stu-id="2bd07-221">Client app</span></span>

<span data-ttu-id="2bd07-222">hello 클라이언트 응용 프로그램 (웹 브라우저, 모바일 앱, 데스크톱 클라이언트) 제네릭 수준 hello 앱 tooconnect tooAzure Active Directory를 사용한 또는 Exchange Active Sync를 구체적으로 선택할 수 있습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-222">hello client app can be either on a generic level hello app (web browser, mobile app, desktop client) you have used tooconnect tooAzure Active Directory or you can specifically select Exchange Active Sync.</span></span>  
<span data-ttu-id="2bd07-223">레거시 인증 tooclients 최신 인증을 사용 하지 않는 오래 된 Office 클라이언트와 같은 기본 인증을 사용 하 여 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-223">Legacy authentication refers tooclients using basic authentication such as older Office clients that don’t use modern authentication.</span></span> <span data-ttu-id="2bd07-224">현재 레거시 인증에서는 조건부 액세스를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-224">Conditional access is currently not supported with legacy authentication.</span></span>

![조건](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a><span data-ttu-id="2bd07-226">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="2bd07-226">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="2bd07-227">앱에 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="2bd07-227">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="2bd07-228">많은 환경 다른 hello 보다 더 높은 수준의 보호를 요구 하는 앱에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-228">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="2bd07-229">이 경우, 예를 들어 hello toosensitive 데이터에 액세스 된 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-229">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="2bd07-230">보호 toothese 앱의 다른 레이어 tooadd을 원하는 경우 사용자가 이러한 앱에 액세스 하는 다단계 인증을 요구 하는 조건부 액세스 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-230">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="2bd07-231">신뢰할 수 없는 네트워크에서 액세스하기 위한 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="2bd07-231">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="2bd07-232">이 시나리오는 multi-factor authentication에 대해 요구 사항을 추가 하기 때문에 비슷한 toohello 이전 시나리오는입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-232">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="2bd07-233">그러나 hello 주요 차이점은이 요구 사항에 대 한 hello 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-233">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="2bd07-234">Hello 이전 시나리오의 hello 포커스 toosensitve 데이터 액세스를 사용 하 여 앱에 때 hello이이 시나리오는 신뢰할 수 있는 위치에.</span><span class="sxs-lookup"><span data-stu-id="2bd07-234">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="2bd07-235">즉 사용자가 신뢰할 수 없는 네트워크에서 앱에 액세스하는 경우 다단계 인증에 대한 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-235">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="2bd07-236">신뢰할 수 있는 장치만 Office 365 서비스에 액세스 가능</span><span class="sxs-lookup"><span data-stu-id="2bd07-236">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="2bd07-237">사용자 환경에서 Intune을 사용 하는 경우 hello Azure 콘솔에서에서 조건부 액세스 정책 인터페이스 hello 사용을 즉시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-237">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="2bd07-238">많은 Intune 고객 신뢰할 수 있는 장치에만 Office 365 서비스에 액세스할 수 있도록 조건부 액세스 tooensure를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-238">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="2bd07-239">이 의미 있고 Windows Pc 조인된 tooan 온-프레미스 도메인은 모바일 장치는 Intune에 등록 된 및 규정 준수 정책 요구 사항을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-239">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="2bd07-240">주요한 개선 사항은 하지 않았는지 tooset 각 hello Office 365 서비스에 대해 같은 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-240">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="2bd07-241">새 정책을 만들 때 hello 클라우드 앱 tooinclude 각와 tooprotect 조건부 액세스를 사용 하 여 원하는 hello O365 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-241">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bd07-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2bd07-242">Next steps</span></span>

<span data-ttu-id="2bd07-243">Tooknow tooconfigure 조건부 액세스 정책을 참조 하는 방법을 원하면 [Azure Active Directory의 조건부 액세스 시작](active-directory-conditional-access-azure-portal-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-243">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>

<span data-ttu-id="2bd07-244">사용자 환경에 대 한 조건부 액세스 정책 준비 tooconfigure 있다면 참조 hello [Azure Active Directory의 조건부 액세스에 대 한 유용한](active-directory-conditional-access-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bd07-244">If you are ready tooconfigure conditional access policies for your environment, see hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span> 
