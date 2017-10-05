---
title: "Azure Multi-Factor Authentication - 작동 방법"
description: "간단한 로그인 프로세스에 대한 사용자 요구를 충족하는 동안 Azure Multi-Factor Authentication을 사용하면 데이터와 응용 프로그램에 대한 액세스를 보호합니다. 두 번째 형식의 인증을 요구하여 추가 보안을 제공하고 다양한 쉬운 확인 옵션을 통해 강력한 인증을 제공합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="c6757-104">Azure Multi-Factor Authentication 작동 방법</span><span class="sxs-lookup"><span data-stu-id="c6757-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="c6757-105">2단계 인증의 보안은 계층화된 접근 방식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="c6757-106">다단계 인증 요소를 손상시키는 일은 공격자에게 매우 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="c6757-107">공격자가 사용자의 암호를 알게 된 경우에도 신뢰할 수 있는 장치가 없다면 어찌할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![검사](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="c6757-109">간단한 로그인 프로세스에 대한 사용자 요구를 충족하는 동안 Azure Multi-Factor Authentication을 사용하면 데이터와 응용 프로그램에 대한 액세스를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="c6757-110">두 번째 형식의 인증을 요구하여 추가 보안을 제공하고 다양한 쉬운 확인 옵션을 통해 강력한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="c6757-111">2단계 인증을 위한 방법</span><span class="sxs-lookup"><span data-stu-id="c6757-111">Methods available for two-step verification</span></span>
<span data-ttu-id="c6757-112">사용자가 로그인하면 사용자에게 추가 확인이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="c6757-113">이 두 번째 확인에 사용할 수 있는 방법의 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="c6757-114">확인 방법</span><span class="sxs-lookup"><span data-stu-id="c6757-114">Verification Method</span></span> | <span data-ttu-id="c6757-115">설명</span><span class="sxs-lookup"><span data-stu-id="c6757-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6757-116">전화 통화</span><span class="sxs-lookup"><span data-stu-id="c6757-116">Phone call</span></span> |<span data-ttu-id="c6757-117">사용자의 등록된 휴대폰으로 통화가 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="c6757-118">사용자는 필요한 경우 PIN을 입력한 후 # 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="c6757-119">문자 메시지</span><span class="sxs-lookup"><span data-stu-id="c6757-119">Text message</span></span> |<span data-ttu-id="c6757-120">6자리 코드가 있는 문자 메시지가 사용자의 휴대폰으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="c6757-121">사용자는 로그인 페이지에 이 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="c6757-122">모바일 앱 알림</span><span class="sxs-lookup"><span data-stu-id="c6757-122">Mobile app notification</span></span> |<span data-ttu-id="c6757-123">사용자의 스마트폰으로 확인 요청이 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="c6757-124">사용자는 필요한 경우 PIN을 입력한 후 모바일 앱에서 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="c6757-125">모바일 앱 확인 코드</span><span class="sxs-lookup"><span data-stu-id="c6757-125">Mobile app verification code</span></span> |<span data-ttu-id="c6757-126">사용자의 스마트폰에서 실행되고 있는 모바일 앱에 30초마다 변경되는 확인 코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="c6757-127">사용자가 가장 최근 코드를 찾아 로그인 페이지에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="c6757-128">타사 OATH 토큰</span><span class="sxs-lookup"><span data-stu-id="c6757-128">Third-party OATH tokens</span></span> | <span data-ttu-id="c6757-129">타사 확인 방법을 허용하도록 Azure Multi-Factor Authentication Server를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="c6757-130">Azure Multi-Factor Authentication은 클라우드와 서버 모두에 대해 선택 가능한 확인 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="c6757-131">전화 통화, 텍스트, 앱 알림, 앱 코드 중에서 사용자에게 제공할 방법을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="c6757-132">자세한 내용은 [선택 가능한 확인 방법](multi-factor-authentication-whats-next.md#selectable-verification-methods)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6757-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6757-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6757-133">Next steps</span></span>

- <span data-ttu-id="c6757-134">다른 [Azure Multi-Factor Authentication에 대한 다양한 버전 및 사용량 메서드](multi-factor-authentication-versions-plans.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="c6757-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="c6757-135">[클라우드 또는 온-프레미스](multi-factor-authentication-get-started.md)에서 Azure MFA를 배포할지 여부 선택</span><span class="sxs-lookup"><span data-stu-id="c6757-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="c6757-136">[자주 묻는 질문](multi-factor-authentication-faq.md)에 대한 답변을 읽어봅니다.</span><span class="sxs-lookup"><span data-stu-id="c6757-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>