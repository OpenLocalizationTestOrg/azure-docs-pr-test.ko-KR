---
title: "Azure Active Directory의 장치 관리 소개 | Microsoft Docs"
description: "사용자 환경의 리소스에 액세스하는 장치를 제어하는 데 장치 관리가 어떻게 도움이 되는지에 대해 알아봅니다."
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
ms.openlocfilehash: bebbdddf6b591ea7e36cbac38b568bce614bb335
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-device-management-in-azure-active-directory"></a><span data-ttu-id="da53e-103">Azure Active Directory의 장치 관리 소개</span><span class="sxs-lookup"><span data-stu-id="da53e-103">Introduction to device management in Azure Active Directory</span></span>

<span data-ttu-id="da53e-104">모바일 우선, 클라우드 우선 세계에서 Azure AD(Active Directory)는 어디에서나 장치, 앱 및 서비스에 대한 Single Sign-On을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="da53e-105">BYOD(Bring Your Own Device)를 포함하는 장치의 확산에 따라 IT 전문가는 다음 두 가지 대립되는 목표에 직면하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-105">With the proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="da53e-106">최종 사용자가 언제 어디서나 생산성을 높일 수 있도록 지원</span><span class="sxs-lookup"><span data-stu-id="da53e-106">Empower the end users to be productive wherever and whenever</span></span>
- <span data-ttu-id="da53e-107">언제든지 회사 자산 보호</span><span class="sxs-lookup"><span data-stu-id="da53e-107">Protect the corporate assets at any time</span></span>

<span data-ttu-id="da53e-108">장치를 통해 사용자가 회사 자산에 액세스하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-108">Through devices, your users are getting access to your corporate assets.</span></span> <span data-ttu-id="da53e-109">IT 관리자로써 회사 자산을 보호하기 위해 이러한 장치를 제어할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-109">To protect your corporate assets, as an IT administrator, you want to have control over these devices.</span></span> <span data-ttu-id="da53e-110">이 기능을 사용하면 보안 및 규정 준수에 대한 표준을 충족하는 장치에서 사용자 리소스에 사용자가 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-110">This enables you to make sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="da53e-111">장치 관리는 [장치 기반 조건부 액세스](active-directory-conditional-access-policy-connected-applications.md)의 토대이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-111">Device management is also the foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="da53e-112">장치 기반 조건부 액세스를 사용할 경우 환경의 리소스에 신뢰할 수 있는 장치를 통해서만 액세스하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-112">With device-based conditional access, you can ensure that access to resources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="da53e-113">이 항목에서는 Azure Active Directory에서 장치 관리가 작동되는 방식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-the-control-of-azure-ad"></a><span data-ttu-id="da53e-114">Azure AD에서 제어하는 장치 얻기</span><span class="sxs-lookup"><span data-stu-id="da53e-114">Getting devices under the control of Azure AD</span></span>

<span data-ttu-id="da53e-115">Azure AD에서 제어하는 장치를 얻으려면 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-115">To get a device under the control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="da53e-116">등록</span><span class="sxs-lookup"><span data-stu-id="da53e-116">Registering</span></span> 
- <span data-ttu-id="da53e-117">가입</span><span class="sxs-lookup"><span data-stu-id="da53e-117">Joining</span></span>

<span data-ttu-id="da53e-118">Azure AD에 장치를 **등록**하면 장치의 ID를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-118">**Registering** a device to Azure AD enables you to manage a device’s identity.</span></span> <span data-ttu-id="da53e-119">장치가 등록되면 Azure AD 장치 등록은 사용자가 Azure AD에 로그인할 때 장치를 인증하는 데 사용되는 ID와 함께 장치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-119">When a device is registered, Azure AD device registration provides the device with an identity that is used to authenticate the device when a user signs-in to Azure AD.</span></span> <span data-ttu-id="da53e-120">ID를 사용하여 장치를 사용하도록 설정하거나 설정 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-120">You can use the identity to enable or disable a device.</span></span>

<span data-ttu-id="da53e-121">Microsoft Intune과 같은 MDM(모바일 장치 관리) 솔루션과 함께 사용할 경우 Azure AD의 장치 특성이 장치에 대한 추가 정보로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure AD are updated with additional information about the device.</span></span> <span data-ttu-id="da53e-122">이렇게 하면 장치의 액세스를 적용하여 보안 및 규정 준수에 대한 표준을 충족하는 조건부 액세스 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-122">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="da53e-123">Microsoft Intune에서 장치를 등록하는 방법에 대한 자세한 내용은 Intune에서 관리를 위한 장치 등록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da53e-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="da53e-124">장치 **가입**은 장치를 등록하는 것에 대한 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-124">**Joining** a device is an extension to registering a device.</span></span> <span data-ttu-id="da53e-125">즉, 장치 등록 혜택을 모두 제공하면서, 추가로 장치의 로컬 상태를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-125">This means, it provides you with all the benefits of registering a device and in addition to this, it also changes the local state of a device.</span></span> <span data-ttu-id="da53e-126">로컬 상태를 변경하면 사용자가 개인 계정 대신 조직 회사 또는 학교 계정을 사용하여 장치에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-126">Changing the local state enables your users to sign-in to a device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="da53e-127">Azure AD 등록 장치</span><span class="sxs-lookup"><span data-stu-id="da53e-127">Azure AD registered devices</span></span>   

<span data-ttu-id="da53e-128">Azure AD 등록 장치의 목표는 **BYOD(Bring Your Own Device)** 시나리오를 지원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-128">The goal of Azure AD registered devices is to provide you with support for the **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="da53e-129">이 시나리오에서 사용자는 개인 장치를 사용하여 조직의 Azure Active Directory 제어 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Azure AD 등록 장치](./media/device-management-introduction/03.png)

<span data-ttu-id="da53e-131">액세스는 장치에서 입력된 회사 또는 학교 계정을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-131">The access is based on a work or school account that has been entered on the device.</span></span>  
<span data-ttu-id="da53e-132">예를 들어 Windows 10을 사용하면 사용자가 회사 또는 학교 계정을 개인용 컴퓨터, 태블릿 또는 휴대폰에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-132">For example, Windows 10 enables users to add a work or school account to a personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="da53e-133">사용자가 회사 또는 학교 계정을 추가하면 장치가 Azure AD에 등록되고 필요에 따라 조직이 구성한 MDM(모바일 장치 관리) 시스템에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-133">When a user has added a work or school account, the device is registered with Azure AD and optionally enrolled in the mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="da53e-134">조직의 사용자가 회사 또는 학교 계정을 개인 장치에 매우 간편하게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-134">Your organization’s users can add a work or school account to a personal device conveniently:</span></span>

- <span data-ttu-id="da53e-135">처음으로 회사 응용 프로그램에 액세스 하는 경우</span><span class="sxs-lookup"><span data-stu-id="da53e-135">When accessing a work application for the first time</span></span>
- <span data-ttu-id="da53e-136">Windows 10의 경우 **설정** 메뉴를 통해 수동으로</span><span class="sxs-lookup"><span data-stu-id="da53e-136">Manually via the **Settings** menu in the case of Windows 10</span></span> 

<span data-ttu-id="da53e-137">Windows 10, iOS, Android 및 macOS용 Azure AD 등록 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="da53e-138">Azure AD 가입 장치</span><span class="sxs-lookup"><span data-stu-id="da53e-138">Azure AD joined devices</span></span>

<span data-ttu-id="da53e-139">Azure AD 가입 장치의 목표는 단순화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-139">The goal of Azure AD joined devices is to simplify:</span></span>

- <span data-ttu-id="da53e-140">회사 소유 장치의 Windows 배포</span><span class="sxs-lookup"><span data-stu-id="da53e-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="da53e-141">모든 Windows 장치에서 조직의 앱 및 리소스에 액세스</span><span class="sxs-lookup"><span data-stu-id="da53e-141">Access to organizational apps and resources from any Windows device</span></span>

![Azure AD 등록 장치](./media/device-management-introduction/02.png)


<span data-ttu-id="da53e-143">이러한 목표는 Azure AD에서 제어하는 회사 소유 장치를 가져오기 위한 자체 서비스 환경 제공을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under the control of Azure AD.</span></span>  
<span data-ttu-id="da53e-144">**Azure AD 가입**은 클라우드 우선/클라우드 전용 조직을 위해 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="da53e-145">일반적으로 온-프레미스 Windows Server Active Directory 인프라가 없는 소규모 및 중간 규모 비즈니스가 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="da53e-146">Azure AD 가입 장치를 구현하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-146">Implementing Azure AD joined devices provides you with the following benefits:</span></span>

- <span data-ttu-id="da53e-147">Azure 관리 SaaS 앱 및 서비스에 대한 **SSO(Single Sign-On)**.</span><span class="sxs-lookup"><span data-stu-id="da53e-147">**Single-Sign-On (SSO)** to your Azure managed SaaS apps and services.</span></span> <span data-ttu-id="da53e-148">사용자가 회사 리소스에 액세스할 때 추가 인증 메시지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="da53e-149">SSO 기능은 사용할 수 있는 도메인 네트워크에 연결되지 않은 경우에도 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-149">The SSO functionality is even when they are not connected to the domain network available.</span></span>

- <span data-ttu-id="da53e-150">가입 장치 간 사용자 설정의 **엔터프라이즈 규정 준수 로밍**.</span><span class="sxs-lookup"><span data-stu-id="da53e-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="da53e-151">사용자는 장치 간에 설정을 보기 위해 Microsoft 계정(예: Hotmail)을 연결할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-151">Users don’t need to connect a Microsoft account (for example, Hotmail) to see settings across devices.</span></span>

- <span data-ttu-id="da53e-152">AD 계정을 사용하는 **비즈니스용 Windows 스토어에 대한 액세스**.</span><span class="sxs-lookup"><span data-stu-id="da53e-152">**Access to Windows Store for Business** using AD account.</span></span> <span data-ttu-id="da53e-153">사용자가 조직에서 미리 선택된 응용 프로그램의 인벤토리에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-153">Your users can choose from an inventory of applications pre-selected by the organization.</span></span>

- <span data-ttu-id="da53e-154">**Windows Hello**는 회사 리소스에 대한 안전하고 편리한 액세스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-154">**Windows Hello** support for secure and convenient access to work resources.</span></span>

- <span data-ttu-id="da53e-155">앱에 대한 **액세스 제한**은 규정 준수 정책을 충족하는 장치에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-155">**Restriction of access** to apps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="da53e-156">Azure AD 가입은 기본적으로 온-프레미스 Windows Server Active Directory 인프라가 없는 조직을 위해 고안되었으나, 다음과 같은 시나리오에서 확실히 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="da53e-157">온-프레미스 도메인 가입을 사용할 수 없습니다. 예를 들어 제어되는 태블릿 및 휴대폰과 같은 모바일 장치가 필요한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-157">You can’t use an on-premises domain join, for example, if you need to get mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="da53e-158">사용자가 기본적으로 Office 365 또는 Azure AD와 통합된 다른 SaaS 앱에 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-158">Your users primarily need to access Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="da53e-159">Active Directory 대신 Azure AD에서 사용자 그룹을 관리하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-159">You want to manage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="da53e-160">이는 예를 들어 계절 노동자, 하청업체 또는 학생에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-160">This can apply, for example, to seasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="da53e-161">제한된 온-프레미스 인프라를 사용하는 원격 지사에서 작업자에게 조인 기능을 제공하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-161">You want to provide joining capabilities to workers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="da53e-162">Windows 10 장치에 대한 Azure AD 가입 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="da53e-163">하이브리드 Azure AD 가입 장치</span><span class="sxs-lookup"><span data-stu-id="da53e-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="da53e-164">10년 이상, 많은 조직은 다음을 가능케 하기 위해 온-프레미스 Active Directory에 도메인 가입을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-164">For more than a decade, many organizations have used the domain join to their on-premises Active Directory to enable:</span></span>

- <span data-ttu-id="da53e-165">IT 부서가 중앙 위치에서 회사 소유 장치를 관리하도록</span><span class="sxs-lookup"><span data-stu-id="da53e-165">IT departments to manage work-owned devices from a central location.</span></span>

- <span data-ttu-id="da53e-166">사용자가 Active Directory 회사 또는 학교 계정으로 자신의 장치에 로그인하도록</span><span class="sxs-lookup"><span data-stu-id="da53e-166">Users to sign in to their devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="da53e-167">온-프레미스 공간이 있는 조직에서는 일반적으로 이미징 메서드에 의존하여 장치를 프로비전하며, 이를 관리하는 데 **SCCM(System Center Configuration Manager)** 또는 **GP(그룹 정책)**를 사용하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-167">Typically, organizations with an on-premises footprint rely on imaging methods to provision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** to manage them.</span></span>

<span data-ttu-id="da53e-168">사용자 환경에 온-프레미스 AD 공간이 있고 Azure Active Directory에서 제공하는 기능의 혜택을 활용하려는 경우 하이브리드 Azure AD 가입 장치를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-168">If your environment has an on-premises AD footprint and you also want benefit from the capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="da53e-169">이는 온-프레미스 Azure Active Directory 및 Azure Active Directory에 모두 가입되어 있는 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-169">These are devices that are both, joined to your on-premises Active Directory and your Azure Active Directory.</span></span>

![Azure AD 등록 장치](./media/device-management-introduction/01.png)


<span data-ttu-id="da53e-171">다음과 같은 경우에 Azure AD 하이브리드 가입 장치를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="da53e-172">NTLM/Kerberos를 사용하는 이러한 장치에 배포된 Win32 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-172">You have Win32 apps deployed to these devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="da53e-173">장치를 관리하는 데 GP 또는 SCCM/DCM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-173">You require GP or SCCM / DCM to manage devices.</span></span>

- <span data-ttu-id="da53e-174">직원에 대해 장치를 구성하도록 이미징 솔루션을 계속 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-174">You want to continue to use imaging solutions to configure devices for your employees.</span></span>

<span data-ttu-id="da53e-175">Windows 10 및 하위 수준 장치(예: Windows 8 및 Windows 7)에 대한 하이브리드 Azure AD 가입 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="da53e-176">요약</span><span class="sxs-lookup"><span data-stu-id="da53e-176">Summary</span></span>

<span data-ttu-id="da53e-177">Azure AD의 장치 관리를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="da53e-178">Azure AD의 제어를 받는 장치를 가져오는 프로세스를 단순화</span><span class="sxs-lookup"><span data-stu-id="da53e-178">Simplify the process of bringing devices under the control of Azure AD</span></span>

- <span data-ttu-id="da53e-179">사용자가 조직의 클라우드 기반 리소스에 대한 액세스를 편리하게 사용할 수 있도록 제공</span><span class="sxs-lookup"><span data-stu-id="da53e-179">Provide your users with an easy to use access to your organization’s cloud-based resources</span></span>

<span data-ttu-id="da53e-180">thumb의 규칙으로 인해 다음을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da53e-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="da53e-181">개인 장치를 위한 Azure AD 등록 장치</span><span class="sxs-lookup"><span data-stu-id="da53e-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="da53e-182">온-프레미스 AD에 가입되지 않은 장치를 위한 Azure AD 가입 장치</span><span class="sxs-lookup"><span data-stu-id="da53e-182">Azure AD joined devices for devices that are not joined to an on-premises AD</span></span> 

- <span data-ttu-id="da53e-183">온-프레미스 AD에 가입된 장치를 위한 하이브리드 Azure AD 가입 장치</span><span class="sxs-lookup"><span data-stu-id="da53e-183">Hybrid Azure AD joined devices for devices that are joined to an on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="da53e-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da53e-184">Next steps</span></span>

- <span data-ttu-id="da53e-185">Azure Portal에서 장치를 관리하는 방법에 대한 개요를 보려면 [Azure Portal을 사용하여 장치 관리](device-management-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da53e-185">To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="da53e-186">장치 기반 조건부 액세스에 대한 자세한 내용은 [Azure Active Directory 장치 기반 조건부 액세스 정책 구성](active-directory-conditional-access-policy-connected-applications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da53e-186">To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="da53e-187">하이브리드 Azure AD 가입 장치를 설정하려면 [하이브리드 Azure Active Directory 가입 장치를 구성하는 방법](device-management-hybrid-azuread-joined-devices-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da53e-187">To setup hybrid Azure AD joined devices, see [how to configure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


