---
title: "여러 번의 실패 후 로그인"
description: "여러 번의 로그인 시도를 연속해서 실패한 이후 로그인에 성공한 사용자를 나타내는 보고서입니다."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="545b7-103">여러 번의 실패 후 로그인</span><span class="sxs-lookup"><span data-stu-id="545b7-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="545b7-104">이 보고서에는 여러 번의 로그인 시도를 연속해서 실패한 이후 로그인에 성공한 사용자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="545b7-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="545b7-105">가능한 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="545b7-105">Possible causes include:</span></span>

* <span data-ttu-id="545b7-106">사용자가 암호를 잊어버린 경우</span><span class="sxs-lookup"><span data-stu-id="545b7-106">User had forgotten their password</span></span></li><li><span data-ttu-id="545b7-107">사용자의 계정이 암호 추측 무차별 암호 대입 공격(brute force attack)에 당한 경우</span><span class="sxs-lookup"><span data-stu-id="545b7-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="545b7-108">이 보고서의 결과에는 로그인하기 전에 연속해서 실패한 로그인 시도 수 및 처음 성공한 로그인과 연관된 타임스탬프가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="545b7-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="545b7-109">**보고서 설정**: 보고서에 표시되기 전에 먼저 발생해야 하는 연속 실패한 최소 로그인 시도 횟수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="545b7-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="545b7-110">이 설정을 변경할 때에는 해당 설정이 현재 기존 보고서에 표시되는 실패한 기존 로그인에 적용되지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="545b7-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="545b7-111">그러나 이러한 변경 사항은 향후 모든 로그인에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="545b7-111">However, they will be applied to all future sign-ins.</span></span> <span data-ttu-id="545b7-112">이 보고서에 대한 변경 작업은 허가받은 관리자만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="545b7-112">Changes to this report can only be made by licensed admins.</span></span>

![여러 번의 실패 후 로그인](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

