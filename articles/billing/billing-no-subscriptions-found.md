---
title: "오류를 발견 했습니다 aaaNo 구독 tooAzure 포털 또는 Azure 계정 센터에서 toosign 려 때 | Microsoft Docs"
description: "No 구독 오류가 발생 발견 된 문제에 대 한 hello 솔루션을 제공 하면 tooAzure 포털 또는 Azure 계정 센터에 로그인 합니다."
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
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="992ec-103">Azure Portal 또는 Azure 계정 센터에 로그인을 시도할 때 구독을 찾을 수 없음 오류 발생</span><span class="sxs-lookup"><span data-stu-id="992ec-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="992ec-104">Toohello에서 toosign 려 할 때 "구독을 찾을 수 없음" 오류 메시지를 받을 수 [Azure 포털](https://portal.azure.com/) 또는 hello [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="992ec-105">본 문서는 이 문제에 대한 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="992ec-106">증상</span><span class="sxs-lookup"><span data-stu-id="992ec-106">Symptom</span></span>

<span data-ttu-id="992ec-107">Toosign toohello에서 시도할 때 [Azure 포털](https://portal.azure.com/) 또는 hello [Azure 계정 센터](https://account.windowsazure.com/Subscriptions), hello 다음과 같은 오류 메시지가 나타나면: "구독을 찾을 수 없음"입니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="992ec-108">원인</span><span class="sxs-lookup"><span data-stu-id="992ec-108">Cause</span></span>

<span data-ttu-id="992ec-109">사용자 계정에 충분한 권한이 없는 경우 이 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="992ec-110">해결 방법</span><span class="sxs-lookup"><span data-stu-id="992ec-110">Solution</span></span>

<span data-ttu-id="992ec-111">올바른 관리자에 게로 로그인 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="992ec-112">계정 관리자만 계정 센터를 hello 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="992ec-113">서비스 관리자 (SA) 및 공동 관리자 (CA) 액세스 권한을 Azure 포털 toohello 없거나 hello Azure 클래식 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="992ec-114">시나리오 1: 오류 메시지가 수신 hello [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="992ec-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="992ec-115">toofix이이 문제:</span><span class="sxs-lookup"><span data-stu-id="992ec-115">toofix this issue:</span></span>

* <span data-ttu-id="992ec-116">해당 hello 올바른 Azure 디렉터리에서 오른쪽 위를 hello 계정을 클릭 하 여 선택 되어 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="992ec-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Hello에서 선택 hello 디렉터리 hello Azure 포털의 오른쪽 위에](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="992ec-118">Hello 오른쪽 Azure 디렉터리 선택 되어 있지만 경우 hello 오류 메시지가 계속 나타나면 [소유자로 추가 계정이 필요](billing-add-change-azure-subscription-administrator.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="992ec-119">시나리오 2: 오류 메시지가 수신 hello [Azure 계정 센터](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="992ec-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="992ec-120">Hello 사용한 계정으로 hello 계정 관리자 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="992ec-121">tooverify hello 계정 관리자 사용자는 다음이 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="992ec-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="992ec-122">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="992ec-123">Hello 허브 메뉴에서 선택 **구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="992ec-124">Hello 구독 toocheck을 원하는 한 다음 선택 하면 선택 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="992ec-125">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-125">Select **Properties**.</span></span> <span data-ttu-id="992ec-126">hello에 hello 구독의 계정 관리자에 게 표시 되 **계정 관리자** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="992ec-127">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="992ec-127">Need help?</span></span> <span data-ttu-id="992ec-128">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="992ec-128">Contact support.</span></span>
<span data-ttu-id="992ec-129">도움이 필요 하면 여전히 필요 하면 [지원에 문의](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget 문제가 해결 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="992ec-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
