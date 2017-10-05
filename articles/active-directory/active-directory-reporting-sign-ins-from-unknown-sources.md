---
title: "알 수 없는 원본에서 로그인"
description: "익명 프록시 IP 주소에서 사용자의 디렉터리에 로그인한 사용자를 나타내는 보고서입니다."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: 2f045543-1578-4972-bf70-b35310f23110
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 90006121e4b3392f6e3ecffb4a56aca330feb02f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-unknown-sources"></a><span data-ttu-id="c8e65-103">알 수 없는 원본에서 로그인</span><span class="sxs-lookup"><span data-stu-id="c8e65-103">Sign ins from unknown sources</span></span>
<span data-ttu-id="c8e65-104">이 보고서에는 Microsoft에서 익명 프록시 IP 주소로 인식한 클라이언트 IP 주소가 디렉터리에 할당되는 동안 사용자의 디렉터리에 로그인한 다른 사용자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8e65-104">This report indicates users who have successfully signed in to your directory while assigned a client IP address that has been recognized by Microsoft as an anonymous proxy IP address (for example, a Tor IP address).</span></span> <span data-ttu-id="c8e65-105">이 프록시는 흔히 자신의 컴퓨터의 IP 주소를 숨기려는 사용자가 사용하며 악의적인 의도로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8e65-105">These proxies are often used by users that want to hide their computer’s IP address, and may be used for malicious intent.</span></span>

<span data-ttu-id="c8e65-106">이 보고서의 결과는 사용자가 해당 주소 및 프록시의 IP 주소에서 디렉터리에 로그인한 횟수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8e65-106">Results from this report will show the number of times a user successfully signed in to your directory from that address and the proxy’s IP address.</span></span>

![알 수 없는 원본에서 로그인](./media/active-directory-reporting-sign-ins-from-unknown-sources/signInsFromUnknownSources.PNG)

