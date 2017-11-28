---
title: "Multi-factor Authentication-aaaAzure 작동 방법"
description: "Azure Multi-factor Authentication 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다. 두 번째 형식의 인증을 요구하여 추가 보안을 제공하고 다양한 쉬운 확인 옵션을 통해 강력한 인증을 제공합니다."
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="3d31a-104">Azure Multi-Factor Authentication 작동 방법</span><span class="sxs-lookup"><span data-stu-id="3d31a-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="3d31a-105">2 단계 인증의 hello 보안은 계층형된 방식을 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="3d31a-106">다단계 인증 요소를 손상시키는 일은 공격자에게 매우 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="3d31a-107">공격자가 toolearn hello 사용자의 암호를 관리 하는 경우에 것은 의미가 없습니다 hello 신뢰할 수 있는 장치를 확보 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![검사](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="3d31a-109">Azure Multi-factor Authentication 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="3d31a-110">두 번째 형식의 인증을 요구하여 추가 보안을 제공하고 다양한 쉬운 확인 옵션을 통해 강력한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="3d31a-111">2단계 인증을 위한 방법</span><span class="sxs-lookup"><span data-stu-id="3d31a-111">Methods available for two-step verification</span></span>
<span data-ttu-id="3d31a-112">사용자가 로그인 할 때 추가 확인 toohello 사용자를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="3d31a-113">hello 다음은이 두 번째 확인에 사용할 수 있는 메서드의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="3d31a-114">확인 방법</span><span class="sxs-lookup"><span data-stu-id="3d31a-114">Verification Method</span></span> | <span data-ttu-id="3d31a-115">설명</span><span class="sxs-lookup"><span data-stu-id="3d31a-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d31a-116">전화 통화</span><span class="sxs-lookup"><span data-stu-id="3d31a-116">Phone call</span></span> |<span data-ttu-id="3d31a-117">호출은 tooa 사용자의 등록 된 전화 번호에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="3d31a-118">hello 사용자 필요한 경우 PIN을 입력 한 다음 hello # 키를 누를 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="3d31a-119">문자 메시지</span><span class="sxs-lookup"><span data-stu-id="3d31a-119">Text message</span></span> |<span data-ttu-id="3d31a-120">문자 메시지 tooa 사용자의 휴대폰 6 자리 코드가 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="3d31a-121">hello 사용자 hello 로그인 페이지에서이 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="3d31a-122">모바일 앱 알림</span><span class="sxs-lookup"><span data-stu-id="3d31a-122">Mobile app notification</span></span> |<span data-ttu-id="3d31a-123">확인 요청 tooa 사용자의 스마트폰을 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="3d31a-124">hello 사용자 필요한 경우 PIN을 입력 한 다음 선택 **확인** hello 모바일 앱에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="3d31a-125">모바일 앱 확인 코드</span><span class="sxs-lookup"><span data-stu-id="3d31a-125">Mobile app verification code</span></span> |<span data-ttu-id="3d31a-126">사용자의 스마트 폰에서 실행 되는 모바일 앱, hello 30 초 간격으로 변경 하는 확인 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="3d31a-127">hello 사용자 hello 가장 최근 코드를 찾아 hello 로그인 페이지에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="3d31a-128">타사 OATH 토큰</span><span class="sxs-lookup"><span data-stu-id="3d31a-128">Third-party OATH tokens</span></span> | <span data-ttu-id="3d31a-129">Azure Multi-factor Authentication 서버에 구성 된 tooaccept 제 3 자 확인 방법을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="3d31a-130">Azure Multi-Factor Authentication은 클라우드와 서버 모두에 대해 선택 가능한 확인 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="3d31a-131">전화 통화, 텍스트, 앱 알림, 앱 코드 중에서 사용자에게 제공할 방법을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="3d31a-132">자세한 내용은 [선택 가능한 확인 방법](multi-factor-authentication-whats-next.md#selectable-verification-methods)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d31a-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d31a-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d31a-133">Next steps</span></span>

- <span data-ttu-id="3d31a-134">다른 hello에 대 한 읽기 [버전 및 Azure Multi-factor Authentication에 대 한 소비 메서드](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="3d31a-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="3d31a-135">선택 여부 toodeploy Azure MFA [hello 클라우드 또는 온-프레미스](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="3d31a-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="3d31a-136">[자주 묻는 질문](multi-factor-authentication-faq.md)에 대한 답변을 읽어봅니다.</span><span class="sxs-lookup"><span data-stu-id="3d31a-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>