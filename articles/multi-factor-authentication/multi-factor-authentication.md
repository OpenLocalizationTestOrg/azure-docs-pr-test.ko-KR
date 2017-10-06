---
title: "Azure MFA에서 2 단계 인증에 대 한 aaaLearn | Microsoft Docs"
description: "Azure multi-factor Authentication 이란, multi-factor Authentication 클라이언트 hello 및 hello 다양 한 방법을 사용할 수 있는 버전에 대 한 자세한 내용은 MFA를 사용 하는 이유입니다. "
keywords: "mfa 란 소개 tooMFA, mfa 개요"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="46c3b-104">Azure Multi-Factor Authentication 정의</span><span class="sxs-lookup"><span data-stu-id="46c3b-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="46c3b-105">2 단계 확인은 확인 방법을 두 개 이상 필요 하며 보안 toouser 로그인 및 트랜잭션에 중요 한 두 번째 계층을 추가 인증 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="46c3b-106">둘 이상 확인 방법을 따르는 hello 요구 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="46c3b-107">사용자가 알고 있는 정보(일반적으로 암호)</span><span class="sxs-lookup"><span data-stu-id="46c3b-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="46c3b-108">사용자가 보유한 장치(예: 휴대폰과 같이 쉽게 복제되지 않는 신뢰할 수 있는 장치)</span><span class="sxs-lookup"><span data-stu-id="46c3b-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="46c3b-109">사용자의 신원 정보(생체 인식)</span><span class="sxs-lookup"><span data-stu-id="46c3b-109">Something you are (biometrics)</span></span>

<span data-ttu-id="46c3b-110"><center>![사용자 이름 및 암호](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![인증서](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![스마트폰](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![스마트 카드](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![가상 스마트 카드](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![사용자 이름 및 암호](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="46c3b-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="46c3b-111">Azure Multi-factor Authentication(MFA)은 Microsoft의 2단계 인증 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="46c3b-112">Azure MFA 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="46c3b-113">전화 통화, 문자 메시지 또는 모바일 앱 확인과 같은 다양한 확인 방법을 통해 강력한 인증을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="46c3b-114">Azure Multi-Factor Authentication을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="46c3b-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="46c3b-115">오늘날, 어느 때 보다 연결된 사람들이 늘어나고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="46c3b-116">스마트 폰, 태블릿, 랩톱, Pc와 사람 몇 가지 옵션이 tooconnect 지 고 언제 든 지 연결을 유지할 방법에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="46c3b-117">사람들이 어디에서나 계정 및 응용 프로그램에 액세스할 수 있으며, 이는 더 많은 작업을 수행할 수 있고 고객에게 더 나은 서비스를 제공할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="46c3b-118">Azure Multi-factor Authentication은 확장성, 쉬운 toouse는 고 안정적인 솔루션 하 제공 보조 인증 방법을 사용자에 게는 항상 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![쉽게 tooUse](./media/multi-factor-authentication/simple.png) | ![확장성](./media/multi-factor-authentication/scalable.png) | ![항상 보호](./media/multi-factor-authentication/protected.png) | ![안정성](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="46c3b-123">**쉽게 toouse**</span><span class="sxs-lookup"><span data-stu-id="46c3b-123">**Easy toouse**</span></span> |<span data-ttu-id="46c3b-124">**확장성**</span><span class="sxs-lookup"><span data-stu-id="46c3b-124">**Scalable**</span></span> |<span data-ttu-id="46c3b-125">**항상 보호**</span><span class="sxs-lookup"><span data-stu-id="46c3b-125">**Always Protected**</span></span> |<span data-ttu-id="46c3b-126">**안정성**</span><span class="sxs-lookup"><span data-stu-id="46c3b-126">**Reliable**</span></span> |

* <span data-ttu-id="46c3b-127">**쉬운 tooUse** -Azure Multi-factor Authentication은 간단한 tooset 구성 및 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="46c3b-128">hello Azure Multi-factor Authentication과 함께 제공 되 장착할 toomanage 사용자가 자신의 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="46c3b-129">무엇보다도 대부분의 경우 간단한 몇 번 클릭으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="46c3b-130">**확장 가능한** -Azure Multi-factor Authentication의 hello 클라우드의 hello 전원 사용 및 온-프레미스와 통합 되어 AD 사용자 지정 응용 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="46c3b-131">이 보호 tooyour 높은 볼륨, 중요 한 시나리오를 확장도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="46c3b-132">**보호 된 항상** -Azure Multi-factor Authentication은 hello 가장 높은 업계 표준을 사용 하 여 강력한 인증을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="46c3b-133">**안정성** -Azure Multi-Factor Authentication의 99.9%의 가용성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="46c3b-134">hello 서비스 것으로 간주 됩니다 사용할 수 없는 경우 hello 2 단계 인증에 대 한 확인 요청 tooreceive 또는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="46c3b-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="46c3b-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46c3b-135">Next steps</span></span>

- <span data-ttu-id="46c3b-136">[Azure Multi-Factor Authentication 작동 방법](multi-factor-authentication-how-it-works.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="46c3b-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="46c3b-137">다른 hello에 대 한 읽기 [버전 및 Azure Multi-factor Authentication에 대 한 소비 메서드](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="46c3b-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
