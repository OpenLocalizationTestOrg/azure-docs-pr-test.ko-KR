---
title: "응용 프로그램 액세스 패널 브라우저 확장 설치 관련 문제 | Microsoft Docs"
description: "액세스 패널 브라우저 확장을 설치할 때 발생하는 일반적인 오류를 해결하는 방법"
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
ms.openlocfilehash: 8b7327508633e33917d1fa9c1f35ed1bde5a26e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-access-panel-browser-extension"></a><span data-ttu-id="60fd3-103">응용 프로그램 액세스 패널 브라우저 확장 설치 관련 문제</span><span class="sxs-lookup"><span data-stu-id="60fd3-103">Problem installing the application access panel browser extension</span></span>

<span data-ttu-id="60fd3-104">액세스 패널은 웹 기반 포털로 Azure AD(Azure Active Directory)에 회사 또는 학교 계정이 있는 사용자가 Azure AD 관리자를 통해 액세스 권한을 부여받은 클라우드 기반 응용 프로그램을 보고 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="60fd3-105">또한 Azure AD 버전의 사용자는 액세스 패널을 통해 셀프 서비스 그룹 및 앱 관리 기능을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="60fd3-106">액세스 패널은 Azure Portal과 별개이며, 사용자에게 Azure 구독을 요구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="60fd3-107">액세스 패널에서 암호 기반 SSO(Single Sign-On)를 사용하려면 사용자의 브라우저에 액세스 패널 확장이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="60fd3-108">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="60fd3-109">액세스 패널에 대한 브라우저 요구 사항 충족</span><span class="sxs-lookup"><span data-stu-id="60fd3-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="60fd3-110">액세스 패널에는 JavaScript를 지원하고 CSS를 사용하도록 설정한 브라우저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="60fd3-111">액세스 패널에서 암호 기반 SSO(Single Sign-On)를 사용하려면 사용자의 브라우저에 액세스 패널 확장이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="60fd3-112">사용자가 암호 기반 SSO에 구성된 응용 프로그램을 선택할 때 이 확장이 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="60fd3-113">암호 기반 SSO의 경우 최종 사용자 브라우저는 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="60fd3-114">Internet Explorer 8, 9, 10, 11 - Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="60fd3-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="60fd3-115">Windows 10 Anniversary Edition 이상 Edge</span><span class="sxs-lookup"><span data-stu-id="60fd3-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="60fd3-116">Chrome - Windows 7 이상 및 Mac OS X 이상</span><span class="sxs-lookup"><span data-stu-id="60fd3-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="60fd3-117">Firefox 26.0 이상 - Windows XP SP2 이상 및 Mac OS X 10.6 이상</span><span class="sxs-lookup"><span data-stu-id="60fd3-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="60fd3-118">액세스 패널 브라우저 확장을 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="60fd3-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="60fd3-119">액세스 패널 브라우저 확장을 설치하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="60fd3-120">지원되는 브라우저 중 하나에서 [액세스 패널](https://myapps.microsoft.com)을 열고 Azure AD에서 **사용자**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="60fd3-121">액세스 패널에서 **암호-SSO 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-121">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="60fd3-122">소프트웨어를 설치하라는 프롬프트에서 **지금 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="60fd3-123">브라우저에 따라 다운로드 링크로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="60fd3-124">브라우저에 확장을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="60fd3-125">브라우저에서 요청하면 확장을 **사용** 또는 **허용**하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="60fd3-126">설치되면 브라우저 세션을 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="60fd3-127">액세스 패널에 로그인하고 암호 SSO 응용 프로그램을 **시작**할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="60fd3-128">아래와 같은 직접 링크에서 Chrome 및 Edge에 대한 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-128">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="60fd3-129">Chrome 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="60fd3-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="60fd3-130">Edge 액세스 패널 확장</span><span class="sxs-lookup"><span data-stu-id="60fd3-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="60fd3-131">Internet Explorer에 대한 그룹 정책 설정</span><span class="sxs-lookup"><span data-stu-id="60fd3-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="60fd3-132">사용자의 컴퓨터에 Internet Explorer용 액세스 패널 확장을 원격으로 설치할 수 있는 그룹 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="60fd3-133">필수 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-133">The prerequisites include:</span></span>

-   <span data-ttu-id="60fd3-134">[Active Directory 도메인 서비스](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)를 설정하고, 사용자 컴퓨터를 도메인에 가입시킨 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="60fd3-135">그룹 정책 개체(GPO)를 편집하는 "설정 편집" 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="60fd3-136">기본적으로 도메인 관리자, 엔터프라이즈 관리자 및 그룹 정책 작성자/소유자 보안 그룹의 멤버에게 이 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="60fd3-137">[자세히 알아보기](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="60fd3-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="60fd3-138">자습서에 따라 그룹 정책을 구성하고 사용자에게 배포하는 방법에 대한 단계별 지침은 [그룹 정책을 사용하여 Internet Explorer용 액세스 패널 확장을 배포하는 방법](active-directory-saas-ie-group-policy.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="60fd3-139">Internet Explorer에서 액세스 패널 문제 해결</span><span class="sxs-lookup"><span data-stu-id="60fd3-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="60fd3-140">진단 도구 및 IE용 확장을 구성하는 방법에 대한 단계별 지침에 액세스하려면 [Internet Explorer의 액세스 패널 확장 문제 해결](active-directory-saas-ie-troubleshooting.md) 가이드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="60fd3-141">이러한 문제 해결 단계로 문제가 해결되지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="60fd3-141">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="60fd3-142">사용할 수 있는 경우 다음 정보로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="60fd3-142">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="60fd3-143">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="60fd3-143">Correlation error ID</span></span>

-   <span data-ttu-id="60fd3-144">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="60fd3-144">UPN (user email address)</span></span>

-   <span data-ttu-id="60fd3-145">TenantID</span><span class="sxs-lookup"><span data-stu-id="60fd3-145">TenantID</span></span>

-   <span data-ttu-id="60fd3-146">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="60fd3-146">Browser type</span></span>

-   <span data-ttu-id="60fd3-147">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="60fd3-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="60fd3-148">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="60fd3-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="60fd3-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60fd3-149">Next steps</span></span>
[<span data-ttu-id="60fd3-150">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="60fd3-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
