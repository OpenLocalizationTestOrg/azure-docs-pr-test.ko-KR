---
title: "감염 가능성이 있는 장치에서의 로그인"
description: "일부 맬웨어(악성 소프트웨어)를 실행 중일 수 있는 장치에서 실행된 로그인 시도를 포함하는 보고서입니다."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: d0361662-d970-4a66-8eb3-72e9f8824dcf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 3809e20937d8d9829675e20f893101cb849dcea2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-possibly-infected-devices"></a><span data-ttu-id="204f6-103">감염 가능성이 있는 장치에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="204f6-103">Sign ins from possibly infected devices</span></span>
<span data-ttu-id="204f6-104">이 보고서는 감염되었으며 이제 봇넷의 일부인 사용자 장치를 식별하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="204f6-104">This report attempts to identify your users' devices that that have become infected and are now part of a botnet.</span></span> <span data-ttu-id="204f6-105">봇넷 서버에 연결되어 있음을 알고 있는 IP 주소와 사용자 로그인의 IP 주소를 상호 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="204f6-105">We correlate IP addresses of users' sign-ins against IP addresses that we know to be in contact with botnet servers.</span></span>

<span data-ttu-id="204f6-106">권장 사항: 이 보고서는 사용자 장치가 아니라 IP 주소에 플래그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="204f6-106">Recommendation: This report flags IP addresses, not user devices.</span></span> <span data-ttu-id="204f6-107">확실히 하려면 사용자에게 연락하고 모든 사용자 장치를 검사하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="204f6-107">We recommend that you contact the user and scan all the user's devices to be certain.</span></span> <span data-ttu-id="204f6-108">사용자의 개인 장치가 감염되었거나 사용자와 동일한 IP 주소를 사용한 사용자 이외의 다른 사람에게 감염된 장치가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204f6-108">It is also possible that a user's personal device is infected, or that someone other than the user, who was using the same IP address as the user, has an infected device.</span></span>

<span data-ttu-id="204f6-109">맬웨어 감염을 해결하는 방법에 대한 자세한 내용은 [맬웨어 보호 센터](http://go.microsoft.com/fwlink/?linkid=335773)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="204f6-109">For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773).</span></span>

![감염 가능성이 있는 장치에서의 로그인](./media/active-directory-reporting-sign-ins-from-possibly-infected-devices/signInsFromPossiblyInfectedDevices.PNG)

