---
title: "Windows Azure Active directory 도메인에 가입 된 장치 aaaHow tooconfigure 자동 등록 | Microsoft Docs"
description: "설정 하면 도메인에 가입 된 Windows 장치 tooregister 자동으로 Azure Active Directory와 합니다."
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
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="e3472-103">Azure Active Directory 장치 등록 시작</span><span class="sxs-lookup"><span data-stu-id="e3472-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="e3472-104">Azure Active Directory device registration은 장치 기반 조건부 액세스 시나리오에 대 한 hello foundation 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="e3472-105">장치가 등록 되 면 Azure Active Directory 장치 등록 hello 사용자가 로그인 할 때 사용 되는 tooauthenticate hello를 장치가 되는 id 사용 하 여 hello 장치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="e3472-106">인증 된 hello 장치와 hello 장치의 hello 특성 수 hello 클라우드 및 온-프레미스에서 호스트 되는 응용 프로그램에 대 한 조건부 액세스 정책을 사용 하는 tooenforce 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="e3472-107">Microsoft Intune 같은 모바일 장치 management(MDM) 솔루션을 함께 사용 하면 Azure Active Directory의 장치 특성이 hello hello 장치에 대 한 추가 정보로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="e3472-108">이렇게 하면 사용자의 보안 및 규정 준수에 대 한 표준 장치 toomeet에서 액세스를 적용 하는 toocreate 조건부 액세스 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="e3472-109">Microsoft Intune에서 장치를 등록하는 방법에 대한 자세한 내용은 Intune에서 관리에 대해 장치 등록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3472-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="e3472-110">Azure Active Directory Device Registration으로 사용할 수 있는 시나리오. Azure Active Directory 장치 등록에서는 iOS, Android 및 Windows 장치를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="e3472-111">Azure AD Device Registration을 활용 하는 hello 개별 시나리오는 보다 구체적인 요구 사항 및 플랫폼 지원이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="e3472-112">이러한 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="e3472-113">**Microsoft Intune을 사용한 Office 365 응용 프로그램에 대 한 조건부 액세스:** hello에서 동일한 시간 규격 장치에서 정보 근로자를 허용 하는 동안 IT 관리자는 다음 조건부 액세스 장치 정책을 toosecure 회사 리소스를 프로 비전 할 수 tooaccess hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="e3472-114">자세한 내용은 Office 365 서비스에 대한 조건부 액세스 장치 정책을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3472-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="e3472-115">**조건부 액세스 tooapplications 온-프레미스 호스팅:** 응용 프로그램을 Windows Server 2012 r 2를 사용 하 여 toouse AD FS 구성에 대 한 액세스 정책을 사용 하 여 등록 된 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="e3472-116">온-프레미스에 대해 조건부 액세스를 설정하는 방법에 대한 자세한 내용은 [Azure Active Directory 장치 등록을 사용하여 온-프레미스 조건부 액세스 설정](active-directory-device-registration-on-premises-setup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3472-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="e3472-117">Azure Active Directory Device Registration 설정</span><span class="sxs-lookup"><span data-stu-id="e3472-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="e3472-118">toosetup 장치 등록을 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="e3472-119">장치를 등록할 때 수 조인된 tooAzure AD 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="e3472-120">이 항목에 대 한 자세한에 대 한 사용자가 toojoin Azure AD 도메인에 필요한 Azure AD Join 및 hello 설정을 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="e3472-121">사용자가 추가 작업 또는 학교 계정 tooWindows 개인 장치에서 모바일 장치 등록에 필요한 tooa 작업 리소스를 연결 하는 경우 장치를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="e3472-122">tooensure이 hello Azure 포털에서에서 Azure AD Device Registration을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="e3472-123">기존 도메인 조인 컴퓨터에 대해서는 자동 장치 등록을 사용하여 장치를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="e3472-124">tooensure이를 자동 장치 등록을 계속 하기 전에 설치 프로그램이 Azure AD Connect를 첫 번째 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="e3472-125">최신 지침을 참조 하십시오. [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-conditional-access-automatic-device-registration-setup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="e3472-126">검토 하 고 사용 하도록 설정 하거나 수도 hello 관리자 포털을 사용 하 여 Azure Active Directory에 등록 된 장치를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="e3472-127">Hello Azure Active Directory 장치 등록 서비스를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e3472-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="e3472-128">**tooenable hello Azure Active Directory 장치 등록 서비스:**</span><span class="sxs-lookup"><span data-stu-id="e3472-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="e3472-129">관리자 권한으로 Microsoft Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="e3472-130">Hello 왼쪽된 창에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="e3472-131">Hello 디렉터리 탭에서 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="e3472-132">**Configure**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="e3472-133">너무 스크롤하여**장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="e3472-134">“사용자가 장치를 Azure AD에 등록할 수 있습니다.”에 대해 모두를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="e3472-135">Hello 최대 수를 선택 하려는 tooauthorize 사용자 당 장치의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="e3472-136">Office 365에 대 한 Microsoft Intune 또는 모바일 장치 관리 hello 등록 장치 등록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="e3472-137">이러한 서비스 중 하나를 구성한 경우 **모두**가 선택되고 **없음** 단추는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="e3472-138">이러한 올바르게 구성 되어 있고 hello 적절 한 라이선스를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e3472-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="e3472-139">기본적으로 hello 서비스에 대 한 2 단계 인증이 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="e3472-140">그러나 장치를 등록하는 경우 2단계 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="e3472-141">이 서비스에 대 한 2 단계 인증을 요구 하기 전에 해야 합니다 Azure Active Directory에서 다단계 인증 공급자를 구성 하 고 Multi-factor Authentication에 대 한 사용자 계정을 구성 하십시오 다단계 인증 추가 참조 Active Directory tooAzure</span><span class="sxs-lookup"><span data-stu-id="e3472-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="e3472-142">Windows Server 2012 R2에서 AD FS를 사용하는 경우 AD FS에서 2단계 인증 모듈을 구성해야 합니다. Active Directory Federation Services로 Multi-Factor Authentication 사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3472-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="e3472-143">Azure Active Directory에서 장치 개체 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="e3472-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="e3472-144">Hello Azure 관리자 포털에서 볼, 차단, 있고 장치를 차단 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="e3472-145">차단 된 장치는 등록 된 장치 에서만 tooallow 구성된 된 액세스 tooapplications가 더 이상.</span><span class="sxs-lookup"><span data-stu-id="e3472-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="e3472-146">**tooview 및 Azure Active Directory의 장치 개체를 관리 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e3472-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="e3472-147">관리자 권한으로 Microsoft Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="e3472-148">Hello 왼쪽된 창에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="e3472-149">디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-149">Select your directory.</span></span>

4.  <span data-ttu-id="e3472-150">**사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="e3472-151">Toosee hello 장치 원하는 hello 사용자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="e3472-152">**장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="e3472-153">**등록된 장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="e3472-154">이제, 검토, 차단, 또는 hello 사용자의 등록 된 장치를 차단 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="e3472-155">온-프레미스 도메인에 가입 하 고 자동으로 등록 된 Windows 10 장치 hello 사용자 탭 아래에 표시 되지 않습니다. 모든 엔터프라이즈 장치를 hello Get MsolDevice PowerShell 명령 toofind 키를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e3472-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="e3472-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3472-156">Next steps</span></span>

<span data-ttu-id="e3472-157">toosetup 자동 장치 등록 참조 [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-conditional-access-automatic-device-registration-setup.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e3472-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


