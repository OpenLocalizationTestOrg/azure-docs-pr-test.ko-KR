---
title: "Azure MFA의 2단계 검증에 대해 알아보기 | Microsoft Docs"
description: "Azure Multi-factor Authentication이란 무엇인가에 대해 설명하고 MFA를 사용하는 이유, Multi-Factor Authentication 클라이언트 및 사용 가능한 다양한 방법과 버전에 대해 설명합니다. "
keywords: "MFA 소개, mfa 개요, mfa 정의"
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
ms.openlocfilehash: 7334ab5b278c3339fdbc2e363fd5c609604d3e14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="e7e29-104">Azure Multi-Factor Authentication 정의</span><span class="sxs-lookup"><span data-stu-id="e7e29-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="e7e29-105">2단계 인증은 두 개 이상의 검증 방법이 필요하며 사용자 로그인 및 트랜잭션에 중요한 두 번째 계층을 추가하는 인증 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="e7e29-106">이러한 인증에서는 다음 중 두 가지 이상의 검증 방법을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-106">It works by requiring any two or more of the following verification methods:</span></span>

* <span data-ttu-id="e7e29-107">사용자가 알고 있는 정보(일반적으로 암호)</span><span class="sxs-lookup"><span data-stu-id="e7e29-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="e7e29-108">사용자가 보유한 장치(예: 휴대폰과 같이 쉽게 복제되지 않는 신뢰할 수 있는 장치)</span><span class="sxs-lookup"><span data-stu-id="e7e29-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="e7e29-109">사용자의 신원 정보(생체 인식)</span><span class="sxs-lookup"><span data-stu-id="e7e29-109">Something you are (biometrics)</span></span>

<span data-ttu-id="e7e29-110"><center>![사용자 이름 및 암호](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![인증서](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![스마트폰](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![스마트 카드](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![가상 스마트 카드](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![사용자 이름 및 암호](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="e7e29-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="e7e29-111">Azure Multi-factor Authentication(MFA)은 Microsoft의 2단계 인증 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="e7e29-112">Azure MFA는 간단한 로그인 프로세스에 대한 사용자 요구를 충족하는 동안 데이터와 응용 프로그램에 대한 액세스를 보호하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="e7e29-113">전화 통화, 문자 메시지 또는 모바일 앱 확인과 같은 다양한 확인 방법을 통해 강력한 인증을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="e7e29-114">Azure Multi-Factor Authentication을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="e7e29-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="e7e29-115">오늘날, 어느 때 보다 연결된 사람들이 늘어나고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="e7e29-116">스마트폰, 태블릿, 랩톱 및 PC를 사용하여, 사람들은 연결하고 언제든지 연결 상태를 유지하는 방법에 대한 여러 다른 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span></span> <span data-ttu-id="e7e29-117">사람들이 어디에서나 계정 및 응용 프로그램에 액세스할 수 있으며, 이는 더 많은 작업을 수행할 수 있고 고객에게 더 나은 서비스를 제공할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="e7e29-118">Azure Multi-Factor Authentication은 인증의 두번째 메서드를 제공하여 사용자가 항상 보호되는 사용하기 쉽고 확장 가능한 신뢰할 수 있는 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![용이성](./media/multi-factor-authentication/simple.png) | ![확장성](./media/multi-factor-authentication/scalable.png) | ![항상 보호](./media/multi-factor-authentication/protected.png) | ![안정성](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="e7e29-123">**용이성**</span><span class="sxs-lookup"><span data-stu-id="e7e29-123">**Easy to use**</span></span> |<span data-ttu-id="e7e29-124">**확장성**</span><span class="sxs-lookup"><span data-stu-id="e7e29-124">**Scalable**</span></span> |<span data-ttu-id="e7e29-125">**항상 보호**</span><span class="sxs-lookup"><span data-stu-id="e7e29-125">**Always Protected**</span></span> |<span data-ttu-id="e7e29-126">**안정성**</span><span class="sxs-lookup"><span data-stu-id="e7e29-126">**Reliable**</span></span> |

* <span data-ttu-id="e7e29-127">**용이성** - Azure Multi-Factor Authentication은 간단하게 설정하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span></span> <span data-ttu-id="e7e29-128">Azure Multi-Factor Authentication과 함께 제공되는 추가 보호를 사용하면 사용자가 자신의 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span></span> <span data-ttu-id="e7e29-129">무엇보다도 대부분의 경우 간단한 몇 번 클릭으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="e7e29-130">**확장성** - Azure Multi-Factor Authentication은 클라우드의 강력한 기능을 이용하며 온-프레미스 AD와 사용자 지정 앱을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="e7e29-131">이러한 보호는 고용량 업무상 중요 한 시나리오에도 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-131">This protection is even extended to your high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="e7e29-132">**항상 보호** -Azure Multi-Factor Authentication은 가장 높은 업계 표준을 사용하여 강력한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span></span>
* <span data-ttu-id="e7e29-133">**안정성** -Azure Multi-Factor Authentication의 99.9%의 가용성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="e7e29-134">2단계 인증 요청을 수신하거나 처리할 수 없는 경우 서비스는 사용할 수 없는 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7e29-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="e7e29-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7e29-135">Next steps</span></span>

- <span data-ttu-id="e7e29-136">[Azure Multi-Factor Authentication 작동 방법](multi-factor-authentication-how-it-works.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="e7e29-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="e7e29-137">다른 [Azure Multi-Factor Authentication에 대한 다양한 버전 및 사용량 메서드](multi-factor-authentication-versions-plans.md)에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="e7e29-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
