---
title: "Azure Portal 또는 Azure 계정 센터에 로그인을 시도할 때 구독을 찾을 수 없음 오류 발생 | Microsoft Docs"
description: "Azure Portal 또는 Azure 계정 센터에 로그인할 때 구독을 찾을 수 없음 오류가 발생하는 문제에 대한 해결 방법을 제공합니다."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="5e9d6-103">Azure Portal 또는 Azure 계정 센터에 로그인을 시도할 때 구독을 찾을 수 없음 오류 발생</span><span class="sxs-lookup"><span data-stu-id="5e9d6-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="5e9d6-104">[Azure Portal](https://portal.azure.com/) 또는 [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)에 로그인을 시도할 때 “구독을 찾을 수 없음” 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="5e9d6-105">본 문서는 이 문제에 대한 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="5e9d6-106">증상</span><span class="sxs-lookup"><span data-stu-id="5e9d6-106">Symptom</span></span>

<span data-ttu-id="5e9d6-107">[Azure Portal](https://portal.azure.com/) 또는 [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)에 로그인을 시도할 때 “구독을 찾을 수 없음” 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="5e9d6-108">원인</span><span class="sxs-lookup"><span data-stu-id="5e9d6-108">Cause</span></span>

<span data-ttu-id="5e9d6-109">사용자 계정에 충분한 권한이 없는 경우 이 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="5e9d6-110">해결 방법</span><span class="sxs-lookup"><span data-stu-id="5e9d6-110">Solution</span></span>

<span data-ttu-id="5e9d6-111">올바른 관리자 권한으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-111">Make sure that you log in as the correct administrator.</span></span> <span data-ttu-id="5e9d6-112">계정 관리자는 계정 센터에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-112">An Account Administrator can access only the Account Center.</span></span> <span data-ttu-id="5e9d6-113">SA(서비스 관리자) 및 CA(공동 관리자)는 Azure Portal 또는 Azure 클래식 포털에 대한 액세스 권한만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only to the Azure portal or the Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a><span data-ttu-id="5e9d6-114">시나리오 1: [Azure Portal](https://portal.azure.com)에서 오류 메시지가 표시됨</span><span class="sxs-lookup"><span data-stu-id="5e9d6-114">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="5e9d6-115">이 문제를 해결하려면</span><span class="sxs-lookup"><span data-stu-id="5e9d6-115">To fix this issue:</span></span>

* <span data-ttu-id="5e9d6-116">오른쪽 위에 있는 계정을 클릭하여 올바른 Azure 디렉터리를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-116">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span></span>

  ![Azure Portal 오른쪽 위에 있는 디렉터리를 선택합니다.](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="5e9d6-118">올바른 Azure 디렉터리를 선택했으나 여전히 오류 메시지가 표시되면 [계정을 소유자로 추가](billing-add-change-azure-subscription-administrator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-118">If the right Azure directory is selected but you still receive the error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="5e9d6-119">시나리오 2: [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)에서 오류 메시지가 표시됨</span><span class="sxs-lookup"><span data-stu-id="5e9d6-119">Scenario 2: Error message is received in the [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="5e9d6-120">사용한 계정이 계정 관리자인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-120">Check whether the account that you used is the Account Administrator.</span></span> <span data-ttu-id="5e9d6-121">계정 관리자가 누구인지 확인하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-121">To verify who the Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="5e9d6-122">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5e9d6-123">허브 메뉴에서 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-123">On the Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="5e9d6-124">확인하려는 구독을 선택한 다음 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-124">Select the subscription that you want to check, and then select **Settings**.</span></span>
4. <span data-ttu-id="5e9d6-125">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-125">Select **Properties**.</span></span> <span data-ttu-id="5e9d6-126">구독의 계정 관리자는 **계정 관리자** 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-126">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="5e9d6-127">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="5e9d6-127">Need help?</span></span> <span data-ttu-id="5e9d6-128">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-128">Contact support.</span></span>
<span data-ttu-id="5e9d6-129">다른 도움이 필요한 경우 [지원에 문의](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="5e9d6-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 
