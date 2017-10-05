---
title: "설치하는 동안 Azure AD로 새 장치 설정| Microsoft Docs"
description: "첫 실행 경험 동안 사용자가 Azure AD 조인을 설정하는 방법에 대해 설명하는 항목입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 4367f453ef7c794653dfa9f305b137a168e0d207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="db93b-103">설치하는 동안 Azure AD로 새 장치 설정</span><span class="sxs-lookup"><span data-stu-id="db93b-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="db93b-104">Windows 10에서 사용자는 FRX(첫 실행 경험)에서 Azure AD(Azure Active Directory)에 장치를 조인시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-104">In Windows 10, users can join their devices to Azure Active Directory (Azure AD) in the first-run experience (FRX).</span></span> <span data-ttu-id="db93b-105">이를 통해 조직은 압축 포장된 장치를 직원 또는 학생들에게 배포하거나 자신의 장치를 선택(CYOD)하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-105">This allows organizations to distribute shrink-wrapped devices to their employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="db93b-106">Windows 10 Professional 또는 Windows 10 Enterprise 버전을 장치에 설치하는 경우 환경은 기본적으로 회사 소유의 장치에 대한 설정 프로세스로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, the experience defaults to the setup process for company-owned devices.</span></span>

## <a name="to-join-a-device-to-azure-ad"></a><span data-ttu-id="db93b-107">Azure AD에 장치를 조인시키려면</span><span class="sxs-lookup"><span data-stu-id="db93b-107">To join a device to Azure AD</span></span>
1. <span data-ttu-id="db93b-108">새 장치를 켜고 설정 프로세스를 시작하면 **준비 중** 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-108">When you turn on your new device and start the setup process, you should see the  **Getting Ready** message.</span></span> <span data-ttu-id="db93b-109">프롬프트에 따라 장치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-109">Follow the prompts to set up your device.</span></span>
2. <span data-ttu-id="db93b-110">국가 및 언어를 사용자 지정하는 작업부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-110">Start by customizing your region and language.</span></span> <span data-ttu-id="db93b-111">그런 다음 Microsoft 소프트웨어 사용 조건에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-111">Then accept the Microsoft Software License Terms.</span></span>
   <span data-ttu-id="db93b-112">![해당 지역에 대한 사용자 지정](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="db93b-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="db93b-113">인터넷에 연결하는 데 사용할 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-113">Select the network you want to use for connecting to the Internet.</span></span>
4. <span data-ttu-id="db93b-114">개인 장치를 사용할지 또는 회사 소유의 장치를 사용할지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="db93b-115">회사 소유인 경우 **이 장치는 내 조직에서 소유한 장치입니다**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-115">If it's company-owned, click **This device belongs to my organization**.</span></span> <span data-ttu-id="db93b-116">이렇게 하면 Azure AD 조인 경험을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-116">This starts the Azure AD Join experience.</span></span> <span data-ttu-id="db93b-117">Windows 10 Professional을 사용하는 경우 다음 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="db93b-118"><center>
   ![이 PC를 누가 소유하고 있나요? 화면](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="db93b-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="db93b-119">조직에서 제공한 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-119">Enter the credentials that were provided to you by your organization.</span></span>
   <span data-ttu-id="db93b-120"><center>
   ![로그인 화면](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="db93b-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="db93b-121">사용자 이름을 입력하면 일치하는 테넌트가 Azure AD에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="db93b-122">페더레이션된 도메인의 사용자인 경우 온-프레미스 STS(보안 토큰 서비스)가 서버(예: AD FS(Active Directory Federation Services))로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-122">If you are in a federated domain, you will be redirected to your on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="db93b-123">페더레이션되지 않은 도메인의 사용자의 경우 Azure AD 호스팅 페이지에 직접 자격 증명을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-123">If you are a user in a non-federated domain, enter your credentials directly on the Azure AD-hosted page.</span></span> <span data-ttu-id="db93b-124">회사 브랜딩이 구성된 경우 조직의 로고도 볼 수 있으며 텍스트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="db93b-125">다단계 인증 질문에 대한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="db93b-126">(이 문제는 IT 관리자가 구성할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="db93b-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="db93b-127">Azure AD는 이 사용자/장치를 모바일 장치 관리에 등록해야 하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="db93b-128">Windows에서 조직의 디렉터리에 있는 장치를 Azure AD에 등록하고 해당하는 경우 모바일 장치 관리에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-128">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="db93b-129">관리되는 사용자인 경우 Windows에서 자동 로그인 프로세스를 통해 바탕 화면으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-129">If you are a managed user, Windows takes you to the desktop through the automatic sign-in process.</span></span>
12. <span data-ttu-id="db93b-130">페더레이션 사용자의 경우, 자격 증명을 입력하도록 Windows 로그인 화면으로 직접 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-130">If you are a federated user, you are directed to the Windows sign-in screen to enter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="db93b-131">Windows 기본 환경에서 온-프레미스 Windows Server Active Directory 도메인 조인은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-131">Joining an on-premises Windows Server Active Directory domain in the Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="db93b-132">따라서 컴퓨터를 도메인에 조인시키려는 경우 **로컬 계정을 사용하여 Windows 설정** 링크를 대신 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-132">Therefore, if you plan to join a computer to a domain, you should select the link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="db93b-133">그런 다음 이전에 수행한 대로 컴퓨터의 설정에서 도메인에 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db93b-133">You can then join the domain from the settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="db93b-134">추가 정보</span><span class="sxs-lookup"><span data-stu-id="db93b-134">Additional information</span></span>
* [<span data-ttu-id="db93b-135">엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="db93b-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="db93b-136">Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장</span><span class="sxs-lookup"><span data-stu-id="db93b-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="db93b-137">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="db93b-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="db93b-138">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="db93b-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="db93b-139">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="db93b-139">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="db93b-140">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="db93b-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

