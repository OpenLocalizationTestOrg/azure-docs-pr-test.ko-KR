---
title: "Windows 도메인 가입 장치의 Azure Active Directory 자동 등록을 구성하는 방법 | Microsoft Docs"
description: "Azure Active Directory에서 Windows 도메인 가입 장치를 자동으로 등록하도록 설정합니다."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="06509-103">Azure Active Directory 장치 등록 시작</span><span class="sxs-lookup"><span data-stu-id="06509-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="06509-104">Azure Active Directory 장치 등록은 장치 기반 조건부 액세스 시나리오의 기초입니다.</span><span class="sxs-lookup"><span data-stu-id="06509-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="06509-105">장치가 등록될 경우 Azure Active Directory 장치 등록은 사용자가 로그인할 때 장치를 인증하는 데 사용되는 ID로 장치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="06509-106">그런 다음 인증된 장치 및 그 장치의 특성을 사용하여 클라우드 및 온-프레미스에 호스트되는 응용 프로그램에 조건부 액세스 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="06509-107">Microsoft Intune과 같은 MDM(모바일 장치 관리) 솔루션과 함께 사용할 경우 Azure Active Directory의 장치 특성이 장치에 대한 추가 정보로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="06509-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="06509-108">이렇게 하면 장치의 액세스를 적용하여 보안 및 규정 준수에 대한 표준을 충족하는 조건부 액세스 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="06509-109">Microsoft Intune에서 장치를 등록하는 방법에 대한 자세한 내용은 Intune에서 관리에 대해 장치 등록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="06509-110">Azure Active Directory Device Registration으로 사용할 수 있는 시나리오. Azure Active Directory 장치 등록에서는 iOS, Android 및 Windows 장치를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="06509-111">Azure AD 장치 등록을 활용하는 개별 시나리오에는 보다 구체적인 요구 사항 및 플랫폼 지원이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="06509-112">이러한 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="06509-113">**Microsoft Intune을 사용한 Office 365 응용 프로그램에 대한 조건부 액세스:** IT 관리자는 조건부 액세스 장치 정책을 프로비전하여 규격 장치를 사용하는 정보 근로자가 서비스에 액세스할 수 있도록 하는 동시에 회사 리소스를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="06509-114">자세한 내용은 Office 365 서비스에 대한 조건부 액세스 장치 정책을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="06509-115">**온-프레미스에서 호스트되는 응용 프로그램에 대한 조건부 액세스:** Windows Server 2012 R2에서 AD FS를 사용하도록 구성된 응용 프로그램에 대한 액세스 정책이 있는 등록된 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="06509-116">온-프레미스에 대해 조건부 액세스를 설정하는 방법에 대한 자세한 내용은 [Azure Active Directory 장치 등록을 사용하여 온-프레미스 조건부 액세스 설정](active-directory-device-registration-on-premises-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="06509-117">Azure Active Directory Device Registration 설정</span><span class="sxs-lookup"><span data-stu-id="06509-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="06509-118">장치 등록을 설정하려면 다음과 같은 여러 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="06509-119">장치는 Azure AD 도메인에 조인될 경우 등록될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="06509-120">이 항목에 대한 자세한 내용은 Azure AD 조인 및 사용자가 Azure AD 도메인에 조입하는 데 필요한 설정을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="06509-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="06509-121">사용자가 회사 또는 학교 계정을 개인 장치의 Windows에 추가하거나 모바일 장치가 등록을 요구하는 작업 리소스에 연결될 때 장치가 등록될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="06509-122">이 작업이 수행되려면 Azure Portal에서 Azure AD 장치 등록을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="06509-123">기존 도메인 조인 컴퓨터에 대해서는 자동 장치 등록을 사용하여 장치를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="06509-124">먼저 Azure AD Connect를 설정해야만 자동 장치 등록이 진행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="06509-125">최신 지침을 보려면 [Windows 도메인 가입 장치의 Azure Active Directory 자동 등록을 구성하는 방법](active-directory-conditional-access-automatic-device-registration-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="06509-126">Azure Active Directory에서 관리자 포털을 사용하여 등록된 장치를 보고 사용하거나 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="06509-127">Azure Active Directory 장치 등록 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="06509-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="06509-128">**Azure Active Directory 장치 등록 서비스를 사용하도록 설정하려면**</span><span class="sxs-lookup"><span data-stu-id="06509-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="06509-129">관리자 권한으로 Microsoft Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="06509-130">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="06509-131">디렉터리 탭에서 해당 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="06509-132">**Configure**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="06509-133">**장치**로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="06509-134">“사용자가 장치를 Azure AD에 등록할 수 있습니다.”에 대해 모두를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="06509-135">사용자당 권한을 부여하려는 최대 장치 수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="06509-136">Office 365에 대한 모바일 장치 관리 및 Microsoft Intune에 등록하려면 장치가 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="06509-137">이러한 서비스 중 하나를 구성한 경우 **모두**가 선택되고 **없음** 단추는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="06509-138">이러한 서비스가 올바르게 구성되어 있는지와 적절한 라이선스가 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="06509-139">기본적으로 2단계 인증은 서비스에 대해 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="06509-140">그러나 장치를 등록하는 경우 2단계 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="06509-141">이 서비스에 대해 2단계 인증을 요구하기 전에 Azure Active Directory에서 2단계 인증 공급자를 구성하고 Multi-Factor Authentication에 대해 사용자 계정을 구성해야 합니다. Azure Active Directory에 Multi-Factor Authentication 추가를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="06509-142">Windows Server 2012 R2에서 AD FS를 사용하는 경우 AD FS에서 2단계 인증 모듈을 구성해야 합니다. Active Directory Federation Services로 Multi-Factor Authentication 사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="06509-143">Azure Active Directory에서 장치 개체 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="06509-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="06509-144">Azure 관리자 포털에서 장치를 보고 차단 및 차단 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="06509-145">차단된 장치는 등록된 장치만 허용하도록 구성된 응용 프로그램에 더 이상 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="06509-146">**Azure Active Directory에서 장치 개체를 보고 관리하려면**</span><span class="sxs-lookup"><span data-stu-id="06509-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="06509-147">관리자 권한으로 Microsoft Azure Portal에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="06509-148">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="06509-149">디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-149">Select your directory.</span></span>

4.  <span data-ttu-id="06509-150">**사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="06509-151">장치를 보도록 허용할 사용자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="06509-152">**장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="06509-153">**등록된 장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06509-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="06509-154">이제 사용자가 등록한 장치를 보거나 차단 또는 차단 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="06509-155">온-프레미스 도메인에 조인되고 자동으로 등록된 Windows 10 장치가 사용자 탭에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06509-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab.</span></span> <span data-ttu-id="06509-156">모든 엔터프라이즈 장치를 찾으려면 Get-MsolDevice PowerShell 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-156">Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="06509-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06509-157">Next steps</span></span>

<span data-ttu-id="06509-158">자동 장치 등록을 설정하려면 [Windows 도메인 조인 장치의 Azure Active Directory 자동 등록을 구성하는 방법](active-directory-conditional-access-automatic-device-registration-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06509-158">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


