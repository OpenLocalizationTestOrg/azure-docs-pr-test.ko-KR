---
title: "Azure Active Directory의 aaaIntroduction toodevice 관리 | Microsoft Docs"
description: "장치 관리의 활용 방법 tooget 제어 환경에서 리소스에 액세스 하는 hello 장치에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="16872-103">Azure Active Directory의 toodevice 관리 소개</span><span class="sxs-lookup"><span data-stu-id="16872-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="16872-104">먼저 모바일, 클라우드 우선 세계에서 Azure Active Directory (Azure AD)에 single sign on toodevices, 앱 및 서비스를 어디에서 든 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="16872-105">장치-BYOD Bring Your Own 장치 ()를 포함 하 여 hello 확산 됨에 따라와 IT 전문가 문제에 직면 두 가지 상반 되 목표:</span><span class="sxs-lookup"><span data-stu-id="16872-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="16872-106">있어 선택의 폭 hello 최종 사용자에 게 toobe 생산성을 아무 곳에 나 때마다</span><span class="sxs-lookup"><span data-stu-id="16872-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="16872-107">언제 든 지 hello 회사 자산을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="16872-108">장치를 통해 tooyour 회사 자산 사용자가 액세스 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16872-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="16872-109">tooprotect 회사 자산을 IT 관리자는 toohave 제어를 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="16872-110">이렇게 하면 사용자가 보안 및 규정 준수 표준을 충족 하는 장치에서 사용자 리소스에 액세스 하는 있는지 toomake 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="16872-111">장치 관리에 대 한 hello foundation 이기도 [장치 기반 조건부 액세스](active-directory-conditional-access-policy-connected-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="16872-112">장치 기반 조건부 액세스를 통해 신뢰할 수 있는 장치 액세스 환경의 tooresources만를 사용할 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="16872-113">이 항목에서는 Azure Active Directory에서 장치 관리가 작동되는 방식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="16872-114">Azure AD의 hello 제어에서 사용 중인 장치 가져오기</span><span class="sxs-lookup"><span data-stu-id="16872-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="16872-115">Azure AD의 hello 제어 아래에 있는 장치 tooget 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="16872-116">등록</span><span class="sxs-lookup"><span data-stu-id="16872-116">Registering</span></span> 
- <span data-ttu-id="16872-117">가입</span><span class="sxs-lookup"><span data-stu-id="16872-117">Joining</span></span>

<span data-ttu-id="16872-118">**등록** 장치 tooAzure AD toomanage 있습니다는 장치 id를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="16872-119">장치를 등록할 때 Azure AD 장치 등록 id가 사용 되는 tooauthenticate hello 장치 경우는 사용자가 로그인 tooAzure AD 사용 하 여 hello 장치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="16872-120">Identity tooenable hello를 사용 하거나 장치를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="16872-121">Microsoft Intune 같은 모바일 장치 management(MDM) 솔루션을 함께 사용 하면 Azure AD의 장치 특성이 hello hello 장치에 대 한 추가 정보로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16872-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="16872-122">이렇게 하면 사용자의 보안 및 규정 준수에 대 한 표준 장치 toomeet에서 액세스를 적용 하는 toocreate 조건부 액세스 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="16872-123">Microsoft Intune에서 장치를 등록하는 방법에 대한 자세한 내용은 Intune에서 관리를 위한 장치 등록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16872-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="16872-124">**조인** 장치는 확장 tooregistering 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="16872-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="16872-125">이 즉, 제공 장치를 등록 하 고 더하기 toothis에 hello 혜택을 모두, hello 로컬 상태는 장치에도 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="16872-126">Hello 로컬 상태를 변경 합니다. 개인 계정 대신는 조직 회사 또는 학교 계정을 사용 하 여 사용자가 toosign-tooa 장치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="16872-127">Azure AD 등록 장치</span><span class="sxs-lookup"><span data-stu-id="16872-127">Azure AD registered devices</span></span>   

<span data-ttu-id="16872-128">hello 등록 하는 Azure AD 장치 ´ ֲ ° hello에 대 한 지원 된 tooprovide **BYOD Bring Your Own 장치 ()** 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="16872-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="16872-129">이 시나리오에서 사용자는 개인 장치를 사용하여 조직의 Azure Active Directory 제어 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Azure AD 등록 장치](./media/device-management-introduction/03.png)

<span data-ttu-id="16872-131">hello 액세스 hello 장치에서 입력 된 회사 또는 학교 계정을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="16872-132">예를 들어, 작업 또는 학교 계정 tooa 개인용 컴퓨터, 태블릿 또는 휴대폰 Windows 10 사용자 tooadd 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="16872-133">회사 또는 학교 계정, hello 장치는 사용자가 추가 하는 경우 Azure AD에 등록 되 고 필요에 따라 조직 구성 hello 모바일 장치 관리 (MDM) 시스템에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="16872-134">조직의 사용자는 작업을 추가 하거나 계정 tooa 개인 장치를 편리 하 게 학교 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="16872-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="16872-135">Hello에 대 한 작업 응용 프로그램에 액세스할 때 처음</span><span class="sxs-lookup"><span data-stu-id="16872-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="16872-136">Hello를 통해 수동으로 **설정을** hello 경우 Windows 10의 메뉴</span><span class="sxs-lookup"><span data-stu-id="16872-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="16872-137">Windows 10, iOS, Android 및 macOS용 Azure AD 등록 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="16872-138">Azure AD 가입 장치</span><span class="sxs-lookup"><span data-stu-id="16872-138">Azure AD joined devices</span></span>

<span data-ttu-id="16872-139">Azure AD 조인 장치의 hello 목표는 toosimplify를입니다.</span><span class="sxs-lookup"><span data-stu-id="16872-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="16872-140">회사 소유 장치의 Windows 배포</span><span class="sxs-lookup"><span data-stu-id="16872-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="16872-141">액세스 tooorganizational 앱 및 모든 Windows 장치에서 리소스</span><span class="sxs-lookup"><span data-stu-id="16872-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Azure AD 등록 장치](./media/device-management-introduction/02.png)


<span data-ttu-id="16872-143">이러한 목표는 Azure AD에 hello 제어 작업 소유 장치를 가져오기 위한 셀프 서비스 환경과 사용자가 제공 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16872-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="16872-144">**Azure AD 가입**은 클라우드 우선/클라우드 전용 조직을 위해 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="16872-145">일반적으로 온-프레미스 Windows Server Active Directory 인프라가 없는 소규모 및 중간 규모 비즈니스가 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="16872-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="16872-146">Azure AD 조인 장치의 구현 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="16872-147">**Single Sign-on (SSO)** tooyour Azure SaaS 앱 및 서비스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="16872-148">사용자가 회사 리소스에 액세스할 때 추가 인증 메시지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="16872-149">hello SSO 기능은 짝수 없는 시기 연결된 toohello 도메인 네트워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="16872-150">가입 장치 간 사용자 설정의 **엔터프라이즈 규정 준수 로밍**.</span><span class="sxs-lookup"><span data-stu-id="16872-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="16872-151">사용자가 장치에서 tooconnect Microsoft 계정 (예: Hotmail) toosee 설정을 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="16872-152">**액세스 tooWindows Store for Business** AD 계정을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="16872-153">사용자가 hello 조직에서 미리 선택 된 응용 프로그램의 인벤토리에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="16872-154">**Windows Hello** toowork 리소스에 안전 하 고 편리한 액세스에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="16872-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="16872-155">**액세스 제한** 규정 준수 정책을 충족 하는 장치만에서 tooapps 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="16872-156">Azure AD 가입은 기본적으로 온-프레미스 Windows Server Active Directory 인프라가 없는 조직을 위해 고안되었으나, 다음과 같은 시나리오에서 확실히 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="16872-157">태블릿 및 휴대폰 제어와 같은 모바일 장치를 tooget 해야 할 경우 예를 들어는 온-프레미스 도메인 가입을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="16872-158">사용자는 주로 tooaccess Office 365 또는 Azure AD와 통합 된 SaaS 응용 프로그램에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="16872-159">Active Directory에 대신 Azure AD에 toomanage 사용자 그룹을 원하는합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="16872-160">이 적용할 수, 예를 들어 tooseasonal 직원, 하청 업체 또는 학생 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="16872-161">제한 된 온-프레미스 인프라와 원거리 지사 사무실의 조인 기능 tooworkers를 tooprovide 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="16872-162">Windows 10 장치에 대한 Azure AD 가입 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="16872-163">하이브리드 Azure AD 가입 장치</span><span class="sxs-lookup"><span data-stu-id="16872-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="16872-164">10 년 이상,에 대 한 대부분의 조직에서는 hello 도메인 가입 tootheir 온-프레미스 Active Directory tooenable 사용:</span><span class="sxs-lookup"><span data-stu-id="16872-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="16872-165">IT 부서 toomanage 작업 소유 장치를 중앙 위치에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="16872-166">해당 Active Directory를 사용 하 여 tootheir 장치에서 사용자가 toosign 직장 이나 학교 계정을 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="16872-167">일반적으로 조직에 온-프레미스 공간 이미징 메서드 tooprovision 장치에 의존 하 고 자주 사용 **SCCM System Center Configuration Manager ()** 또는 **그룹 정책 (GP)** toomanage 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="16872-168">사용자 환경에 온-프레미스 AD 사용 공간을 Azure Active Directory에서 제공 하는 hello 기능에서 혜택을 하려면 또한, 하이브리드 Azure AD 조인 장치의 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="16872-169">둘 다 있는 장치, 조인 된 tooyour 온-프레미스 Active Directory와 Azure Active Directory 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Azure AD 등록 장치](./media/device-management-introduction/01.png)


<span data-ttu-id="16872-171">다음과 같은 경우에 Azure AD 하이브리드 가입 장치를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="16872-172">NTLM을 사용 하는 Win32 앱 배포 toothese 장치가 / Kerberos입니다.</span><span class="sxs-lookup"><span data-stu-id="16872-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="16872-173">GP 또는 SCCM 필요한 / DCM toomanage 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="16872-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="16872-174">직원에 게 toocontinue toouse 이미징 솔루션 tooconfigure 장치 원하는합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="16872-175">Windows 10 및 하위 수준 장치(예: Windows 8 및 Windows 7)에 대한 하이브리드 Azure AD 가입 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="16872-176">요약</span><span class="sxs-lookup"><span data-stu-id="16872-176">Summary</span></span>

<span data-ttu-id="16872-177">Azure AD의 장치 관리를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16872-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="16872-178">Azure AD의 hello 제어에서 사용 중인 장치를 가져와 hello 과정을 단순화</span><span class="sxs-lookup"><span data-stu-id="16872-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="16872-179">사용자가 쉽게 toouse 액세스 tooyour 조직의 클라우드 기반 리소스 제공</span><span class="sxs-lookup"><span data-stu-id="16872-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="16872-180">thumb의 규칙으로 인해 다음을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="16872-181">개인 장치를 위한 Azure AD 등록 장치</span><span class="sxs-lookup"><span data-stu-id="16872-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="16872-182">Azure AD에 가입 하지 않은 장치 tooan에 가입 된 장치 온-프레미스 AD</span><span class="sxs-lookup"><span data-stu-id="16872-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="16872-183">Azure AD 하이브리드 가입 하는 장치 tooan에 가입 된 장치 온-프레미스 AD</span><span class="sxs-lookup"><span data-stu-id="16872-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="16872-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16872-184">Next steps</span></span>

- <span data-ttu-id="16872-185">tooget toomanage 장치에 Azure 포털에서 참조 hello 하는 방법에 대해 간략하게 [hello Azure 포털을 사용 하 여 장치를 관리 합니다.](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="16872-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="16872-186">장치 기반 조건부 액세스에 대해 자세히 toolearn 참조 [Azure Active Directory 장치 기반 조건부 액세스 정책 구성](active-directory-conditional-access-policy-connected-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="16872-187">toosetup 하이브리드 가입 하는 Azure AD 장치 참조 [tooconfigure 하이브리드 Azure Active Directory에 가입 하는 장치](device-management-hybrid-azuread-joined-devices-setup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16872-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


