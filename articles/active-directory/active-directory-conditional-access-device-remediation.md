---
title: "Windows 장치의 Azure Portal 상의 여기에서 가져올 수 없습니다 | Microsoft Docs"
description: "여기에서 가져올 수 없는 위치 및 이 대화 상자에서 실행되지 않도록 방지하기 위해 확인할 점에 대해 알아봅니다."
services: active-directory
keywords: "장치 기반 조건부 액세스, 장치 등록, 장치 등록 사용, 장치 등록 및 MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 16543c7bb7b6b236dcc24093c9963bc218ca1fa6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="8b923-104">Windows 장치 상에서 '여기에서 가져올 수 없습니다'</span><span class="sxs-lookup"><span data-stu-id="8b923-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="8b923-105">예를 들어 조직의 SharePoint Online 인트라넷에 액세스하려 할 때 *여기에서 가져올 수 없습니다*라는 메시지가 있는 페이지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="8b923-106">관리자가 특정 조건 하에서는 조직의 리소스에 액세스하지 못하도록 하는 조건부 액세스 정책을 구성했기 때문에 이 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access to your organization's resources under certain conditions.</span></span> <span data-ttu-id="8b923-107">이 문제를 해결하기 위해 기술 지원팀 또는 관리자에게 문의하기 전에 사용자가 직접 시도해 볼 수 있는 몇 가지 조치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-107">While it might be necessary to contact helpdesk or your administrator to get this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="8b923-108">**Windows** 장치를 사용하는 경우 다음을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-108">If you are using a **Windows** device, you should check the following:</span></span>

- <span data-ttu-id="8b923-109">지원되는 브라우저를 사용하고 있는가?</span><span class="sxs-lookup"><span data-stu-id="8b923-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="8b923-110">장치에서 지원되는 Windows 버전을 실행하고 있는가?</span><span class="sxs-lookup"><span data-stu-id="8b923-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="8b923-111">장치가 규격을 준수하는가?</span><span class="sxs-lookup"><span data-stu-id="8b923-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="8b923-112">지원되는 브라우저</span><span class="sxs-lookup"><span data-stu-id="8b923-112">Supported browser</span></span>

<span data-ttu-id="8b923-113">관리자가 조건부 액세스 정책을 구성한 경우, 지원되는 브라우저를 사용하여 조직의 리소스를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="8b923-114">Windows 장치에서는 **Internet Explorer** 및 **Edge**만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="8b923-115">오류 페이지의 세부 정보 섹션을 보면 리소스에 액세스할 수 없는 이유가 지원되지 않는 브라우저 때문인지 여부를 쉽게 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-115">You can easily identify whether you can't access a resource due to an unsupported browser by looking at the details section of the error page:</span></span>

<span data-ttu-id="8b923-116">![지원되지 않은 브라우저에 대한 "여기에서 가져올 수 없습니다" 메시지](./media/active-directory-conditional-access-device-remediation/02.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="8b923-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="8b923-117">유일하게 수정된 부분은 응용 프로그램이 장치 플랫폼에 지원하는 브라우저를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-117">The only remediation is to use a browser that the application supports for your device platform.</span></span> <span data-ttu-id="8b923-118">지원되는 브라우저의 전체 목록은 [지원되는 브라우저](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b923-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="8b923-119">지원되는 Windows 버전</span><span class="sxs-lookup"><span data-stu-id="8b923-119">Supported versions of Windows</span></span>

<span data-ttu-id="8b923-120">장치의 Windows 운영 체제는 다음을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-120">The following must be true about the Windows operating system on your device:</span></span> 

- <span data-ttu-id="8b923-121">장치에서 Windows 데스크톱 운영 체제를 실행하는 경우 Windows 7 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-121">If you are running a Windows desktop operating system on your device, it needs to be Windows 7 or later.</span></span>
- <span data-ttu-id="8b923-122">장치에서 Windows 서버 운영 체제를 실행하는 경우 Windows Server 2008 R2 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-122">If you are running a Windows server operating system on your device, it needs to be Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="8b923-123">규정 준수 장치</span><span class="sxs-lookup"><span data-stu-id="8b923-123">Compliant device</span></span>

<span data-ttu-id="8b923-124">관리자는 규정 준수 장치에서만 조직의 리소스에 액세스할 수 있도록 조건부 액세스 정책을 구성했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-124">Your administrator might have configured a conditional access policy that allows access to your organization's resources only from compliant devices.</span></span> <span data-ttu-id="8b923-125">규정을 준수하려면 장치가 온-프레미스 Active Directory에 조인하거나 Azure Active Directory에 조인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-125">To be compliant, your device must be either joined to your on-premises Active Directory or joined to your Azure Active Directory.</span></span>

<span data-ttu-id="8b923-126">오류 페이지의 세부 정보 섹션을 보면 리소스에 액세스할 수 없는 이유가 규정을 준수하지 않는 브라우저 때문인지 여부를 쉽게 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-126">You can easily identify whether you can't access a resource due to a device that is not compliant by looking at the details section of the error page:</span></span>
 
<span data-ttu-id="8b923-127">![등록되지 않은 장치에 대한 "여기에서 가져올 수 없습니다" 메시지](./media/active-directory-conditional-access-device-remediation/01.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="8b923-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="8b923-128">장치가 온-프레미스 Active Directory에 조인되어 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8b923-128">Is your device joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="8b923-129">**장치가 조직의 온-프레미스 Active Directory에 조인된 경우 다음을 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8b923-129">**If your device is joined to an on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="8b923-130">작업 계정(Active Directory 계정)을 사용하여 Windows에 로그인하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-130">Make sure that you sign in to Windows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="8b923-131">가상 사설망(VPN) 또는 DirectAccess를 통해 회사 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-131">Connect to your corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="8b923-132">일단 연결한 후에 Windows 로고 키 + L 키를 사용하여 Windows 세션을 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-132">After you are connected, press the Windows logo key + the L key to lock your Windows session.</span></span>
4. <span data-ttu-id="8b923-133">작업 계정 자격 증명을 입력하여 Windows 세션의 잠금을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="8b923-134">몇 분 기다렸다가 다시 응용 프로그램 또는 서비스에 액세스를 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="8b923-134">Wait for a minute, and then try again to access the application or service.</span></span>
6. <span data-ttu-id="8b923-135">동일한 페이지가 표시되면 **자세한 내용** 링크를 클릭한 후에 관리자에게 세부 정보를 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-135">If you see the same page, click the **More details** link, and then contact your administrator with the details.</span></span>


### <a name="is-your-device-not-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="8b923-136">장치가 온-프레미스 Active Directory에 조인되어 있지 않습니까?</span><span class="sxs-lookup"><span data-stu-id="8b923-136">Is your device not joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="8b923-137">장치가 온-프레미스 Active Directory에 조인되지 않고 Windows 10을 실행하는 경우 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-137">If your device is not joined to an on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="8b923-138">Azure AD 조인을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-138">Run Azure AD Join</span></span>
* <span data-ttu-id="8b923-139">Windows에 회사 또는 학교 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-139">Add your work or school account to Windows</span></span>

<span data-ttu-id="8b923-140">이러한 옵션의 차이점에 대한 자세한 내용은 [작업 공간에서 Windows 10 장치 사용](active-directory-azureadjoin-windows10-devices.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b923-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="8b923-141">장치가</span><span class="sxs-lookup"><span data-stu-id="8b923-141">If your device:</span></span>

- <span data-ttu-id="8b923-142">조직에 속해 있는 경우 Azure AD 조인을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-142">Belongs to your organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="8b923-143">개인 장치 또는 Windows Phone인 경우 Windows에 회사 또는 학교 계정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-143">Is a personal device or a Windows phone, you should add your work or school account to Windows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="8b923-144">Windows 10에서 Azure AD 조인</span><span class="sxs-lookup"><span data-stu-id="8b923-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="8b923-145">장치를 Azure AD에 조인하는 단계는 장치에서 실행하는 Windows 10의 버전에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-145">The steps to join your device to Azure AD are tied the version of Windows 10 you are running on it.</span></span> <span data-ttu-id="8b923-146">Windows 10 운영 체제의 버전을 확인하려면 다음과 같이 **winver** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-146">To determine the version of your Windows 10 operating system, run the **winver** command:</span></span> 

![Windows 버전](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="8b923-148">**Windows 10 1주년 업데이트(버전 1607):**</span><span class="sxs-lookup"><span data-stu-id="8b923-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="8b923-149">**설정** 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-149">Open the **Settings** app.</span></span>
2. <span data-ttu-id="8b923-150">**계정** > **회사 또는 학교에 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="8b923-151">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-151">Click **Connect**.</span></span>
4. <span data-ttu-id="8b923-152">**Azure AD에 이 장치 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-152">Click **Join this device to Azure AD**.</span></span>
5. <span data-ttu-id="8b923-153">조직에 인증하고 메시지가 표시되면 다단계 인증을 제공하고 제시되는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-153">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
6. <span data-ttu-id="8b923-154">로그아웃한 후 작업 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="8b923-155">응용 프로그램에 다시 액세스를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-155">Try again to access the application.</span></span>

<span data-ttu-id="8b923-156">**Windows 10 2015년 11월 업데이트(버전 1511):**</span><span class="sxs-lookup"><span data-stu-id="8b923-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="8b923-157">**설정** 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-157">Open the **Settings** app.</span></span>
2. <span data-ttu-id="8b923-158">**시스템** > **정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="8b923-159">**Azure AD 조인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="8b923-160">조직에 인증하고 메시지가 표시되면 다단계 인증을 제공하고 제시되는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-160">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="8b923-161">로그아웃한 후 작업 계정(Azure AD 계정)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="8b923-162">응용 프로그램에 다시 액세스를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-162">Try again to access the application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="8b923-163">Windows 8.1에서 작업 공간 연결</span><span class="sxs-lookup"><span data-stu-id="8b923-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="8b923-164">장치가 도메인에 조인되지 않고 Windows 8.1을 실행하는 경우 작업 공간 연결을 수행하고 Microsoft Intune에 등록하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-164">If your device is not domain-joined and runs Windows 8.1, to do a Workplace Join and enroll in Microsoft Intune, do the following steps:</span></span>

1. <span data-ttu-id="8b923-165">**PC 설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="8b923-166">**네트워크** > **작업 공간**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="8b923-167">**조인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-167">Click **Join**.</span></span>
4. <span data-ttu-id="8b923-168">조직에 인증하고 메시지가 표시되면 다단계 인증을 제공하고 제시되는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-168">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="8b923-169">**켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="8b923-170">응용 프로그램에 다시 액세스를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-170">Try again to access the application.</span></span>



#### <a name="add-your-work-or-school-account-to-windows"></a><span data-ttu-id="8b923-171">Windows에 회사 또는 학교 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-171">Add your work or school account to Windows</span></span> 


<span data-ttu-id="8b923-172">**Windows 10 1주년 업데이트(버전 1607):**</span><span class="sxs-lookup"><span data-stu-id="8b923-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="8b923-173">**설정** 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-173">Open the **Settings** app.</span></span>
2. <span data-ttu-id="8b923-174">**계정** > **회사 또는 학교에 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="8b923-175">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-175">Click **Connect**.</span></span>
4. <span data-ttu-id="8b923-176">조직에 인증하고 메시지가 표시되면 다단계 인증을 제공하고 제시되는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-176">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="8b923-177">응용 프로그램에 다시 액세스를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-177">Try again to access the application.</span></span>


<span data-ttu-id="8b923-178">**Windows 10 2015년 11월 업데이트(버전 1511):**</span><span class="sxs-lookup"><span data-stu-id="8b923-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="8b923-179">**설정** 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-179">Open the **Settings** app.</span></span>
2. <span data-ttu-id="8b923-180">**계정** > **사용자 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="8b923-181">**회사 또는 학교 계정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="8b923-182">조직에 인증하고 메시지가 표시되면 다단계 인증을 제공하고 제시되는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-182">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="8b923-183">응용 프로그램에 다시 액세스를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8b923-183">Try again to access the application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="8b923-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b923-184">Next steps</span></span>
[<span data-ttu-id="8b923-185">Azure Active Directory 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="8b923-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

