---
title: "hello 응용 프로그램 액세스 패널 브라우저 확장을 설치 하는 aaaProblem | Microsoft Docs"
description: "일반적인 오류 toofix hello 액세스 패널 브라우저 확장을 설치할 때 발생 하는 방법"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a><span data-ttu-id="07539-103">Hello 응용 프로그램 액세스 패널 브라우저 확장을 설치 하는 문제</span><span class="sxs-lookup"><span data-stu-id="07539-103">Problem installing hello application access panel browser extension</span></span>

<span data-ttu-id="07539-104">액세스 패널 hello 활성화 있는 사용자가 회사 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 관리자에 게 Azure AD는 웹 기반 포털이 부여 해 준에 대 한 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="07539-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="07539-105">Azure AD 버전을 가진 사용자는 셀프 서비스 그룹 및 hello 액세스 패널을 통해 응용 프로그램 관리 기능 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="07539-106">액세스 패널 hello는 hello Azure 포털에서에서 분리 되 고 사용자가 toohave Azure 구독이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="07539-107">toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="07539-108">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="07539-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="07539-109">액세스 패널 hello에 대 한 브라우저 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="07539-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="07539-110">hello 액세스 패널을 지 원하는 JavaScript 브라우저 필요 하 고 CSS를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="07539-111">toouse 암호 기반 single 로그온 (SSO)에서 액세스 패널 액세스 패널 확장 hello hello hello 사용자 브라우저에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="07539-112">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="07539-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="07539-113">암호 기반 SSO에 대 한 hello 최종 사용자의 브라우저 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="07539-114">Internet Explorer 8, 9, 10, 11 - Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="07539-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="07539-115">Windows 10 Anniversary Edition 이상 Edge</span><span class="sxs-lookup"><span data-stu-id="07539-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="07539-116">Chrome - Windows 7 이상 및 Mac OS X 이상</span><span class="sxs-lookup"><span data-stu-id="07539-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="07539-117">Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상</span><span class="sxs-lookup"><span data-stu-id="07539-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="07539-118">Tooinstall은 액세스 패널 브라우저 확장을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="07539-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="07539-119">아래의 hello 단계를 수행 하는 액세스 패널 브라우저 확장 tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="07539-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="07539-120">열기 hello [액세스 패널](https://myapps.microsoft.com) hello 지원 되는 브라우저와로 로그인 중 하나에 **사용자** Azure AD에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="07539-121">클릭는 **password SSO 응용 프로그램** hello 액세스 패널에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-121">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="07539-122">Hello 프롬프트 묻는 tooinstall hello 소프트웨어에서 선택 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="07539-123">브라우저에 따라 toohello 방향이 지정 된 다운로드 링크 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="07539-124">**추가** hello 확장 tooyour 브라우저.</span><span class="sxs-lookup"><span data-stu-id="07539-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="07539-125">브라우저를 요청 하면 선택 tooeither **사용** 또는 **허용** hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="07539-126">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="07539-127">Hello 액세스 패널에 로그인 하 고 참조 하면 **시작** password SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="07539-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="07539-128">Hello 직접 링크 아래에서 Edge 및 Chrome에 대 한 hello 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-128">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="07539-129">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="07539-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="07539-130">Edge 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="07539-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="07539-131">Internet Explorer에 대한 그룹 정책 설정</span><span class="sxs-lookup"><span data-stu-id="07539-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="07539-132">할 수 있도록 tooremotely 설치 hello 액세스 패널 확장 Internet Explorer에 대 한 사용자의 컴퓨터에서 그룹 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="07539-133">hello 필수 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="07539-134">설정한 후 [Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), 사용자의 컴퓨터 tooyour 도메인에 가입한 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07539-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="07539-135">Hello "설정 편집" 권한이 tooedit hello 그룹 정책 개체 (GPO) 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="07539-136">기본적으로 hello 다음 보안 그룹의 멤버는이 권한이 있는: Domain Administrators, 엔터프라이즈 관리자 및 Group Policy Creator Owners 합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="07539-137">[자세히 알아봅니다](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="07539-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="07539-138">Hello 자습서에 따라 [tooDeploy 그룹 정책을 사용 하 여 Internet Explorer에 대 한 액세스 패널 확장을 hello 하는 방법을](active-directory-saas-ie-group-policy.md) tooconfigure hello 그룹 정책 하 고 toousers 배포 하는 방법에 대 한 단계별 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="07539-139">Internet Explorer에서 액세스 패널 hello 문제 해결</span><span class="sxs-lookup"><span data-stu-id="07539-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="07539-140">Hello에 따라 [문제 해결 hello Internet Explorer에 대 한 액세스 패널 확장이](active-directory-saas-ie-troubleshooting.md) IE hello 확장 구성에 액세스에 대 한 진단 도구 및 단계별 지침 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="07539-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="07539-141">이러한 문제 해결 단계 hello 문제가 해결 되지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="07539-141">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="07539-142">사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07539-142">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="07539-143">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="07539-143">Correlation error ID</span></span>

-   <span data-ttu-id="07539-144">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="07539-144">UPN (user email address)</span></span>

-   <span data-ttu-id="07539-145">TenantID</span><span class="sxs-lookup"><span data-stu-id="07539-145">TenantID</span></span>

-   <span data-ttu-id="07539-146">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="07539-146">Browser type</span></span>

-   <span data-ttu-id="07539-147">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="07539-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="07539-148">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="07539-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="07539-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07539-149">Next steps</span></span>
[<span data-ttu-id="07539-150">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="07539-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
