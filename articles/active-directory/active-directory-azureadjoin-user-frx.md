---
title: "설치 하는 동안 Azure AD 사용 하 여 새 장치 aaaSet | Microsoft Docs"
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
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="b3a00-103">설치하는 동안 Azure AD로 새 장치 설정</span><span class="sxs-lookup"><span data-stu-id="b3a00-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="b3a00-104">Windows 10에서 사용자가 hello 첫 실행 경험 (FRX) 자신의 장치 tooAzure Active Directory (Azure AD)를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-104">In Windows 10, users can join their devices tooAzure Active Directory (Azure AD) in hello first-run experience (FRX).</span></span> <span data-ttu-id="b3a00-105">이 조직은 toodistribute 축소 래핑된 장치 tootheir 직원이 나 학생을 허용 하거나 자신의 장치 (CYOD)를 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-105">This allows organizations toodistribute shrink-wrapped devices tootheir employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="b3a00-106">장치에 Windows 10 Professional 또는 Windows 10 Enterprise edition이 설치 되어 hello 기본값 toohello 설치 프로세스는 회사 소유 장치에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, hello experience defaults toohello setup process for company-owned devices.</span></span>

## <a name="toojoin-a-device-tooazure-ad"></a><span data-ttu-id="b3a00-107">장치 tooAzure AD toojoin</span><span class="sxs-lookup"><span data-stu-id="b3a00-107">toojoin a device tooAzure AD</span></span>
1. <span data-ttu-id="b3a00-108">새 장치에서 설정 하 고 hello 설치 프로세스를 시작할 때 hello 나타나야 **준비** 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-108">When you turn on your new device and start hello setup process, you should see hello  **Getting Ready** message.</span></span> <span data-ttu-id="b3a00-109">장치를 hello 프롬프트 tooset를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-109">Follow hello prompts tooset up your device.</span></span>
2. <span data-ttu-id="b3a00-110">국가 및 언어를 사용자 지정하는 작업부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-110">Start by customizing your region and language.</span></span> <span data-ttu-id="b3a00-111">그런 다음 hello Microsoft 소프트웨어 사용 조건에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-111">Then accept hello Microsoft Software License Terms.</span></span>
   <span data-ttu-id="b3a00-112">![해당 지역에 대한 사용자 지정](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="b3a00-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="b3a00-113">Toouse toohello 인터넷에 연결 하기 위한 원하는 hello 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-113">Select hello network you want toouse for connecting toohello Internet.</span></span>
4. <span data-ttu-id="b3a00-114">개인 장치를 사용할지 또는 회사 소유의 장치를 사용할지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="b3a00-115">클릭 하 여 회사 소유의 이면 **toomy 조직 ज이**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-115">If it's company-owned, click **This device belongs toomy organization**.</span></span> <span data-ttu-id="b3a00-116">Azure AD 조인 환경 hello를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-116">This starts hello Azure AD Join experience.</span></span> <span data-ttu-id="b3a00-117">Windows 10 Professional을 사용하는 경우 다음 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="b3a00-118"><center>
   ![이 PC를 누가 소유하고 있나요? 화면](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="b3a00-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="b3a00-119">조직에서 tooyou 제공 된 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-119">Enter hello credentials that were provided tooyou by your organization.</span></span>
   <span data-ttu-id="b3a00-120"><center>
   ![로그인 화면](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="b3a00-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="b3a00-121">사용자 이름을 입력하면 일치하는 테넌트가 Azure AD에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="b3a00-122">페더레이션된 도메인에 있는 경우 리디렉션된 tooyour 온-프레미스 서비스 STS (보안 토큰) 서버--예를 들어 Active Directory Federation Services (AD FS) 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-122">If you are in a federated domain, you will be redirected tooyour on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="b3a00-123">페더레이션 되지 않은 도메인의 사용자 인 경우 hello Azure AD 호스트 페이지에 직접 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-123">If you are a user in a non-federated domain, enter your credentials directly on hello Azure AD-hosted page.</span></span> <span data-ttu-id="b3a00-124">회사 브랜딩이 구성된 경우 조직의 로고도 볼 수 있으며 텍스트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="b3a00-125">다단계 인증 질문에 대한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="b3a00-126">(이 문제는 IT 관리자가 구성할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="b3a00-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="b3a00-127">Azure AD는 이 사용자/장치를 모바일 장치 관리에 등록해야 하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="b3a00-128">Windows Azure AD에서 hello 조직의 디렉터리에서 hello 장치를 등록 하 고 해당 하는 경우 모바일 장치 관리에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-128">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="b3a00-129">관리 되는 사용자 인 경우 Windows hello 자동 로그인 프로세스를 통해 toohello 데스크톱을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-129">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in process.</span></span>
12. <span data-ttu-id="b3a00-130">전송 되는 페더레이션된 사용자 인 경우 toohello Windows 로그인 화면 tooenter 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-130">If you are a federated user, you are directed toohello Windows sign-in screen tooenter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="b3a00-131">Windows hello에서에서 온-프레미스 Windows Server Active Directory 도메인 가입 경험 기본적으로 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-131">Joining an on-premises Windows Server Active Directory domain in hello Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="b3a00-132">따라서 컴퓨터 tooa 도메인 toojoin 하려는 경우 링크를 선택 하면 hello **로컬 계정으로 Windows 설정** 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-132">Therefore, if you plan toojoin a computer tooa domain, you should select hello link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="b3a00-133">그런 다음 하기 전에 작업을 수행 하면 대로 hello 도메인 hello 설정에서 컴퓨터에 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-133">You can then join hello domain from hello settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="b3a00-134">추가 정보</span><span class="sxs-lookup"><span data-stu-id="b3a00-134">Additional information</span></span>
* [<span data-ttu-id="b3a00-135">Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치</span><span class="sxs-lookup"><span data-stu-id="b3a00-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="b3a00-136">Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b3a00-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="b3a00-137">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="b3a00-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="b3a00-138">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="b3a00-138">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="b3a00-139">Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="b3a00-139">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="b3a00-140">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="b3a00-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

