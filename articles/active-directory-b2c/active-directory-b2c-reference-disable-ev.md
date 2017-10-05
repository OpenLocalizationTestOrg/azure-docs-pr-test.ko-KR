---
title: "Azure Active Directory B2C: 소비자 등록 중에 전자 메일 확인 사용 안 함 | Microsoft Docs"
description: "Azure Active Directory B2C의 소비자 등록 중에 전자 메일 확인을 사용하지 않도록 설정하는 방법을 보여 주는 토픽입니다."
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
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="1744a-103">Azure Active Directory B2C: 소비자 등록 중에 전자 메일 확인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="1744a-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="1744a-104">Azure AD(Azure Active Directory) B2C를 사용하도록 설정하면 소비자는 전자 메일 주소를 제공하고 로컬 계정을 만들어 응용 프로그램에 등록할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="1744a-105">Azure AD B2C는 등록 프로세스 중에 소비자에게 전자 메일 주소를 확인하도록 요구하여 전자 메일 주소의 유효성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="1744a-106">또한 악의적인 자동화 프로세스를 통해 응용 프로그램에 대한 가짜 계정이 생성되지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="1744a-107">일부 응용 프로그램 개발자는 등록 프로세스 동안 전자 메일 확인을 건너뛰고 소비자에게 나중에 전자 메일 주소를 확인하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="1744a-108">이를 지원하는 경우 전자 메일 확인을 사용하지 않도록 Azure AD B2C를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="1744a-109">이를 통해 등록 프로세스가 좀 더 원활해지고 개발자는 전자 메일 주소를 확인한 소비자와 아직 전자 메일 주소를 확인하지 않은 소비자를 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="1744a-110">기본적으로 등록 정책에는 전자 메일 확인 기능이 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="1744a-111">해제하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="1744a-112">[다음 단계에 따라 Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="1744a-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="1744a-113">등록 구성 방식에 따라 **등록 정책** 또는 **등록 또는 로그인 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="1744a-114">정책(예: "B2C_1_SiUp")을 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="1744a-115">블레이드 위쪽에서 **편집** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="1744a-116">**페이지 UI 사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="1744a-117">**로컬 계정 등록 페이지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="1744a-118">**등록 특성** 섹션의 **이름** 열에 있는 **전자 메일 주소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="1744a-119">**확인 필요** 옵션을 **아니요**로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="1744a-120">**정책 편집** 블레이드에 도달할 때까지 아래쪽의 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="1744a-121">블레이드 위쪽에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="1744a-122">완료되었습니다!</span><span class="sxs-lookup"><span data-stu-id="1744a-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="1744a-123">등록 프로세스에서 전자 메일 확인을 사용하지 않도록 설정하면 스팸 메일이 수신될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="1744a-124">기본 기능을 사용하지 않도록 설정하는 경우에는 자체 확인 시스템을 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="1744a-125">Microsoft는 사용자 의견 및 제안을 항상 환영합니다!</span><span class="sxs-lookup"><span data-stu-id="1744a-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="1744a-126">이 토픽을 완료하기가 어렵거나 이 콘텐츠를 개선할 사항이 있는 경우 페이지의 맨 아래에 의견을 보내주시면 감사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1744a-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="1744a-127">기능 요청이 있는 경우 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)에 추가해 주세요.</span><span class="sxs-lookup"><span data-stu-id="1744a-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>