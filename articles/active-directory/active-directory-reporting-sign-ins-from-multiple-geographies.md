---
title: "여러 지역에서의 로그인"
description: "한 사용자의 두 로그인이 각각 다른 지역에서 시작된 것으로 보이고 로그인 간격이 사용자가 두 지역 간에 이동하기에는 불가능한 시간임을 나타내는 보고서입니다."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a><span data-ttu-id="4fb51-103">여러 지역에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="4fb51-103">Sign-ins from multiple geographies</span></span>
<span data-ttu-id="4fb51-104">한 사용자의 두 로그인이 각각 다른 지역에서 시작된 것으로 보이고 로그인 간격이 사용자가 두 지역 간에 이동하기에는 불가능한 시간인 경우 해당 사용자의 모든 성공적인 로그인이 이 보고서에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fb51-104">This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions.</span></span> <span data-ttu-id="4fb51-105">가능한 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb51-105">Possible causes include:</span></span>

* <span data-ttu-id="4fb51-106">사용자가 다른 사용자와 암호를 공유하고 있는 경우</span><span class="sxs-lookup"><span data-stu-id="4fb51-106">User is sharing their password with other users</span></span>
* <span data-ttu-id="4fb51-107">사용자가 로그인을 위해 웹 브라우저를 시작하는 데 원격 데스크톱을 사용하고 있는 경우</span><span class="sxs-lookup"><span data-stu-id="4fb51-107">User is using a remote desktop to launch a web browser for sign-in</span></span>
* <span data-ttu-id="4fb51-108">해커가 다른 국가에서 사용자의 계정에 로그인한 경우</span><span class="sxs-lookup"><span data-stu-id="4fb51-108">A hacker has signed in to the account of a user from a different country</span></span>
* <span data-ttu-id="4fb51-109">사용자가 VPN 또는 프록시를 사용하고 있는 경우</span><span class="sxs-lookup"><span data-stu-id="4fb51-109">User is using a VPN or proxy</span></span>
* <span data-ttu-id="4fb51-110">사용자가 데스크톱, 휴대폰 등 여러 장치에서 동시에 로그인했고 휴대폰의 IP 주소가 일반적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb51-110">User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.</span></span>

<span data-ttu-id="4fb51-111">이 보고서의 결과에는 로그인 간 시간, 로그인이 발생한 것으로 보이는 지역 및 해당 지역 간 예상되는 이동 시간과 함께 성공적인 로그인 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fb51-111">Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions.</span></span> <span data-ttu-id="4fb51-112">표시된 이동 시간은 예상치이며 위치 사이의 실제 이동 시간과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fb51-112">The travel time shown is only an estimate and may be different from the actual travel time between the locations.</span></span>

![여러 지역에서의 로그인](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

