---
title: "aaaYou에서에서 가져올 수 없는 있습니다 hello에 Windows 장치에서 Azure 포털 | Microsoft Docs"
description: "고정할 수 없는 위치에 대해 알아봅니다 여기에서에서 이릅니다 get 접근자와 어떤를 확인 하는 tooavoid이 대화이 상자를 실행 합니다."
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
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="e396c-104">Windows 장치 상에서 '여기에서 가져올 수 없습니다'</span><span class="sxs-lookup"><span data-stu-id="e396c-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="e396c-105">예를 들어 조직의 SharePoint Online 인트라넷에 액세스하려 할 때 *여기에서 가져올 수 없습니다*라는 메시지가 있는 페이지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="e396c-106">관리자가 특정 조건에 대 한 액세스 tooyour 조직 리소스를 방지 하는 조건부 액세스 정책을 구성 때문에이 페이지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="e396c-107">필요한 toocontact 기술 지원팀 또는 사용자 관리자 tooget이이 문제를 해결할 수 있습니다, 하는 동안 몇 가지 방법으로, 직접 아웃 먼저 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="e396c-108">사용 하는 경우는 **Windows** 장치를 다음 hello 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="e396c-109">지원되는 브라우저를 사용하고 있는가?</span><span class="sxs-lookup"><span data-stu-id="e396c-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="e396c-110">장치에서 지원되는 Windows 버전을 실행하고 있는가?</span><span class="sxs-lookup"><span data-stu-id="e396c-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="e396c-111">장치가 규격을 준수하는가?</span><span class="sxs-lookup"><span data-stu-id="e396c-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="e396c-112">지원되는 브라우저</span><span class="sxs-lookup"><span data-stu-id="e396c-112">Supported browser</span></span>

<span data-ttu-id="e396c-113">관리자가 조건부 액세스 정책을 구성한 경우, 지원되는 브라우저를 사용하여 조직의 리소스를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="e396c-114">Windows 장치에서는 **Internet Explorer** 및 **Edge**만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="e396c-115">Hello 오류 페이지 hello 세부 정보 섹션을 보면 tooan 지원 되지 않는 브라우저 인해는 리소스를 액세스할 수 있는지 여부를 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="e396c-116">![지원되지 않은 브라우저에 대한 "여기에서 가져올 수 없습니다" 메시지](./media/active-directory-conditional-access-device-remediation/02.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="e396c-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="e396c-117">hello만 재구성 toouse hello 응용 프로그램이 지 원하는 장치 플랫폼에 대 한 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="e396c-118">지원되는 브라우저의 전체 목록은 [지원되는 브라우저](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e396c-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="e396c-119">지원되는 Windows 버전</span><span class="sxs-lookup"><span data-stu-id="e396c-119">Supported versions of Windows</span></span>

<span data-ttu-id="e396c-120">hello 다음 장치에서 Windows 운영 체제 hello에 대 한 적용 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="e396c-121">장치에서 Windows 데스크톱 운영 체제를 실행 하는 경우 toobe Windows 7 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="e396c-122">장치에서 Windows server 운영 체제를 실행 하는 경우 필요한 toobe Windows Server 2008 R2 이상.</span><span class="sxs-lookup"><span data-stu-id="e396c-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="e396c-123">규정 준수 장치</span><span class="sxs-lookup"><span data-stu-id="e396c-123">Compliant device</span></span>

<span data-ttu-id="e396c-124">관리자가 규격 장치 에서만에서 액세스 tooyour 조직 리소스를 허용 하는 조건부 액세스 정책을 구성 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="e396c-125">toobe 규격 장치에 조인 된 tooyour 중 하나 여야 합니다. 온-프레미스 Active Directory 또는 Azure Active Directory tooyour 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="e396c-126">Hello 오류 페이지의 hello 세부 정보 섹션을 검색 하 여 호환 되지 않는 tooa 장치 인해는 리소스를 액세스할 수 있는지 여부를 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="e396c-127">![등록되지 않은 장치에 대한 "여기에서 가져올 수 없습니다" 메시지](./media/active-directory-conditional-access-device-remediation/01.png "시나리오")</span><span class="sxs-lookup"><span data-stu-id="e396c-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="e396c-128">가입 된 장치 tooan 온-프레미스 Active Directory 인가요?</span><span class="sxs-lookup"><span data-stu-id="e396c-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="e396c-129">**장치에 가입 되어 있으면 tooan 온-프레미스 Active Directory 조직에서:**</span><span class="sxs-lookup"><span data-stu-id="e396c-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="e396c-130">작업 계정 (Active Directory 계정)를 사용 하 여 tooWindows에 로그인 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="e396c-131">가상 사설망 (VPN) 또는 DirectAccess를 통해 tooyour 회사 네트워크에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="e396c-132">연결 된 후 hello Windows 로고 키 + L hello 키 toolock 키를 눌러 Windows 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="e396c-133">작업 계정 자격 증명을 입력하여 Windows 세션의 잠금을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="e396c-134">잠시 기다렸다가 tooaccess hello 응용 프로그램 또는 서비스 후 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e396c-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="e396c-135">표시 되 면 hello 동일한 페이지에서 hello **자세히** 링크를 선택한 다음 hello 세부 정보를 사용 하 여 관리자에 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e396c-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="e396c-136">조인 되지 장치 tooan 온-프레미스 Active Directory 인가요?</span><span class="sxs-lookup"><span data-stu-id="e396c-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="e396c-137">장치에 가입 되지 않은 경우 tooan 온-프레미스 Active Directory 및 Windows 10을 실행, 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="e396c-138">Azure AD 조인을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-138">Run Azure AD Join</span></span>
* <span data-ttu-id="e396c-139">작업을 추가 또는 학교 계정 tooWindows</span><span class="sxs-lookup"><span data-stu-id="e396c-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="e396c-140">이러한 옵션의 차이점에 대한 자세한 내용은 [작업 공간에서 Windows 10 장치 사용](active-directory-azureadjoin-windows10-devices.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e396c-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="e396c-141">장치가</span><span class="sxs-lookup"><span data-stu-id="e396c-141">If your device:</span></span>

- <span data-ttu-id="e396c-142">Tooyour 조직에 속한 Azure AD Join을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="e396c-143">개인 장치 또는 Windows phone 작업 추가 또는 학교 계정 tooWindows 해야</span><span class="sxs-lookup"><span data-stu-id="e396c-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="e396c-144">Windows 10에서 Azure AD 조인</span><span class="sxs-lookup"><span data-stu-id="e396c-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="e396c-145">hello 단계 toojoin 장치 tooAzure AD 사용자는 연결의 Windows 10을 실행 하는 hello 버전.</span><span class="sxs-lookup"><span data-stu-id="e396c-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="e396c-146">hello를 실행 중인 Windows 10 운영 체제의 toodetermine hello 버전 **winver** 명령:</span><span class="sxs-lookup"><span data-stu-id="e396c-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Windows 버전](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="e396c-148">**Windows 10 1주년 업데이트(버전 1607):**</span><span class="sxs-lookup"><span data-stu-id="e396c-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="e396c-149">열기 hello **설정을** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="e396c-150">**계정** > **회사 또는 학교에 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="e396c-151">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-151">Click **Connect**.</span></span>
4. <span data-ttu-id="e396c-152">클릭 **이 장치 tooAzure AD Join**합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="e396c-153">Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="e396c-154">로그아웃한 후 작업 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="e396c-155">Tooaccess hello 응용 프로그램을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="e396c-156">**Windows 10 2015년 11월 업데이트(버전 1511):**</span><span class="sxs-lookup"><span data-stu-id="e396c-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="e396c-157">열기 hello **설정을** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="e396c-158">**시스템** > **정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="e396c-159">**Azure AD 조인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="e396c-160">Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="e396c-161">로그아웃한 후 작업 계정(Azure AD 계정)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="e396c-162">Tooaccess hello 응용 프로그램을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="e396c-163">Windows 8.1에서 작업 공간 연결</span><span class="sxs-lookup"><span data-stu-id="e396c-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="e396c-164">장치가 도메인에 가입 되지 않은 작업 공간 연결 toodo, Windows 8.1 실행 및 Microsoft Intune에 등록을 하는 경우 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="e396c-165">**PC 설정**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="e396c-166">**네트워크** > **작업 공간**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="e396c-167">**조인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-167">Click **Join**.</span></span>
4. <span data-ttu-id="e396c-168">Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="e396c-169">**켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="e396c-170">Tooaccess hello 응용 프로그램을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="e396c-171">작업을 추가 또는 학교 계정 tooWindows</span><span class="sxs-lookup"><span data-stu-id="e396c-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="e396c-172">**Windows 10 1주년 업데이트(버전 1607):**</span><span class="sxs-lookup"><span data-stu-id="e396c-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="e396c-173">열기 hello **설정을** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="e396c-174">**계정** > **회사 또는 학교에 액세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="e396c-175">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-175">Click **Connect**.</span></span>
4. <span data-ttu-id="e396c-176">Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="e396c-177">Tooaccess hello 응용 프로그램을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="e396c-178">**Windows 10 2015년 11월 업데이트(버전 1511):**</span><span class="sxs-lookup"><span data-stu-id="e396c-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="e396c-179">열기 hello **설정을** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="e396c-180">**계정** > **사용자 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="e396c-181">**회사 또는 학교 계정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="e396c-182">Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="e396c-183">Tooaccess hello 응용 프로그램을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e396c-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="e396c-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e396c-184">Next steps</span></span>
[<span data-ttu-id="e396c-185">Azure Active Directory 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="e396c-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

