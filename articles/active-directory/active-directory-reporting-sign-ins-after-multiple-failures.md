---
title: "aaaSign 여러 번 실패 후 기능"
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
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="b0683-103">여러 번의 실패 후 로그인</span><span class="sxs-lookup"><span data-stu-id="b0683-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="b0683-104">이 보고서에는 여러 번의 로그인 시도를 연속해서 실패한 이후 로그인에 성공한 사용자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0683-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="b0683-105">가능한 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b0683-105">Possible causes include:</span></span>

* <span data-ttu-id="b0683-106">사용자가 암호를 잊어버린 경우</span><span class="sxs-lookup"><span data-stu-id="b0683-106">User had forgotten their password</span></span></li><li><span data-ttu-id="b0683-107">사용자가 암호 추측 무차별 암호 대입 공격 hello 교착 상태가 발생</span><span class="sxs-lookup"><span data-stu-id="b0683-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="b0683-108">이 보고서의 결과 실패 한 로그인 시도 연속적으로 만든 이전 toohello 성공한 로그인 수를 hello 및 처음 성공한 로그인 hello와 연결 된 타임 스탬프 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0683-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="b0683-109">**보고서 설정을**: hello 보고서에 표시 하려면 먼저 발생 해야 하는 시도에서 연속 된 실패 한 로그인의 hello 최소 수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0683-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="b0683-110">속성을 설정 하는 toothis은 변경 하면 중요 한 toonote 이러한 변경 내용은 실패 한 기존 적용된 tooany 되지 것입니다 현재 기존 보고서에 표시 하는 기능을 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0683-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="b0683-111">그러나 적용 된 tooall 이후 로그인 됩니다. 변경 toothis 보고서 허가 받은 관리자만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0683-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![여러 번의 실패 후 로그인](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

