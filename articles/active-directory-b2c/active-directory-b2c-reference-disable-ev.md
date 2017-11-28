---
title: "Azure Active Directory B2C: 소비자 등록 중에 전자 메일 확인 사용 안 함 | Microsoft Docs"
description: "Toodisable 소비자 Azure Active Directory B2C에 등록 하는 동안 확인 메일 하는 방법을 보여 주는 항목"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="49d0c-103">Azure Active Directory B2C: 소비자 등록 중에 전자 메일 확인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="49d0c-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="49d0c-104">사용 하도록 설정 하면 소비자 (Azure AD) Azure Active Directory B2C 제공 전자 메일 주소를 제공 하 여 로컬 계정을 만들어 응용 프로그램에 대해 기능 toosign을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="49d0c-105">Azure AD B2C 소비자 tooverify 요구 하 여 유효한 전자 메일 주소를 사용 하면 hello 등록 프로세스 중에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="49d0c-106">또한 악성 자동화 된 프로세스를에서 hello 응용 프로그램에 대 한 가짜 계정을 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="49d0c-107">일부 응용 프로그램 개발자가 선호 하는 hello 등록 프로세스 동안 tooskip 전자 메일 확인 하 고 소비자도 대신 나중에 hello 전자 메일 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="49d0c-108">이 Azure AD B2C 수 toosupport 수 구성된 toodisable 전자 메일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="49d0c-109">이렇게 원활 하 게 등록 프로세스를 생성 하 고 적용 되지 않은 이러한 소비자에서 메일 주소를 확인 하는 hello 유연성 toodifferentiate hello 소비자에서는 개발자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="49d0c-110">기본적으로 등록 정책에는 전자 메일 확인 기능이 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="49d0c-111">사용 하 여 hello 단계 tooturn 다음 그 오프:</span><span class="sxs-lookup"><span data-stu-id="49d0c-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="49d0c-112">[이러한 단계 toonavigate toohello B2C 기능 블레이드 hello Azure 포털에 따라](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="49d0c-113">등록 구성 방식에 따라 **등록 정책** 또는 **등록 또는 로그인 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="49d0c-114">정책 (예: "B2C_1_SiUp") tooopen 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="49d0c-115">클릭 **편집** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="49d0c-116">**페이지 UI 사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="49d0c-117">**로컬 계정 등록 페이지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="49d0c-118">클릭 **전자 메일 주소** hello에 **이름** hello 아래의 열 **등록 특성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="49d0c-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="49d0c-119">설정/해제 hello **영역에 있는 모든** 옵션**아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="49d0c-120">클릭 **확인** hello에 도달할 때까지 hello 아래쪽 **정책 편집** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="49d0c-121">클릭 **저장** hello hello 블레이드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="49d0c-122">완료되었습니다!</span><span class="sxs-lookup"><span data-stu-id="49d0c-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="49d0c-123">Hello 등록 프로세스에서 전자 메일 확인을 사용 하지 않도록 설정 하면 toospam을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="49d0c-124">Hello 기본을 비활성화 하면 사용자 고유의 인증 시스템을 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="49d0c-125">우리는 항상 열려 toofeedback 및 제안을!</span><span class="sxs-lookup"><span data-stu-id="49d0c-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="49d0c-126">이 항목에 문제가 발생 하거나이 콘텐츠를 개선 하기 위한 권장 사항이 있는 경우 hello hello 페이지 맨 아래에 사용자 의견 보내 주셔서 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="49d0c-127">기능 요청에 대 한 추가 너무[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)합니다.</span><span class="sxs-lookup"><span data-stu-id="49d0c-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
