---
title: "aaaCreate, 연결, 삭제 또는 Azure 논리 앱에 통합 계정을 이동 | Microsoft Docs"
description: "어떻게 통합 toocreate 계정을 한 tooyour 논리 앱 연결"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="8b23b-103">통합 계정이란?</span><span class="sxs-lookup"><span data-stu-id="8b23b-103">What is an integration account?</span></span>

<span data-ttu-id="8b23b-104">통합 계정 toomanage 아티팩트, 스키마, 맵, 인증서, 파트너 및 규약을 포함 하 여 엔터프라이즈 통합 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="8b23b-105">만들 모든 통합 응용 프로그램 통합 계정 tooaccess를 사용 하 여 이러한 스키마, 맵, 인증서, 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="8b23b-106">통합 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="8b23b-106">Create an integration account</span></span>

1.  <span data-ttu-id="8b23b-107">Toohello 로그인 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="8b23b-108">Hello 왼쪽된 메뉴에서 선택 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-108">From hello left menu, select **More services**.</span></span>

    !["추가 서비스"를 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="8b23b-110">Hello 검색 상자에 필터에 대 한 "통합"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="8b23b-111">Hello 결과 목록에서 선택 **통합 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-111">In hello results list, select **Integration Accounts**.</span></span>

    !["통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="8b23b-113">Hello 페이지의 hello 위쪽 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-113">At hello top of hello page, choose **Add**.</span></span>

    ![[추가] 선택](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="8b23b-115">통합 계정 및 선택 hello toouse 되도록 Azure 구독 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="8b23b-116">새 **리소스 그룹**을 만들거나 기존 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="8b23b-117">그런 다음 호스팅 통합 계정의 **위치** 및 **가격 책정 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="8b23b-118">준비되면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-118">When you're ready, choose **Create**.</span></span>

    ![통합 계정의 세부 정보를 제공합니다.](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="8b23b-120">Azure에 1 분 내에 완료 해야 하는 hello 선택한 위치에 통합 계정 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="8b23b-121">Hello 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-121">Refresh hello page.</span></span> <span data-ttu-id="8b23b-122">새 통합 계정이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-122">You see your new integration account listed.</span></span>

    ![새 통합 계정이 표시됩니다.](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="8b23b-124">다음으로 hello 통합 계정을 해당 만든된 tooyour 논리 앱을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="8b23b-125">통합 계정 tooa 논리 앱 연결</span><span class="sxs-lookup"><span data-stu-id="8b23b-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="8b23b-126">toogive 논리 앱 toomaps, 스키마, 계약 및 기타 아티팩트 링크 hello 통합 계정 tooyour 논리 앱 통합 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8b23b-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8b23b-127">Prerequisites</span></span>

* <span data-ttu-id="8b23b-128">통합 계정</span><span class="sxs-lookup"><span data-stu-id="8b23b-128">An integration account</span></span>
* <span data-ttu-id="8b23b-129">논리 앱</span><span class="sxs-lookup"><span data-stu-id="8b23b-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="8b23b-130">통합 계정 및 논리 앱 hello에 있는지 확인 *동일한 Azure 위치* 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="8b23b-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="8b23b-131">Hello Azure 포털에서에서 논리 앱을 선택 하 고 논리 앱의 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![논리 앱을 선택하고 위치를 확인합니다.](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="8b23b-133">**설정**에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-133">Under **Settings**, select **Integration Account**.</span></span>

    !["통합 계정" 선택](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="8b23b-135">Hello에서 **통합 계정 선택** toolink tooyour 논리 앱을 원하는 선택 hello 통합 계정 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="8b23b-136">링크의 경우, toofinish 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-136">toofinish linking, choose **Save**.</span></span>

    ![통합 계정 선택](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="8b23b-138">계정이 연결 된 tooyour 논리 앱이 고 통합 계정에서 모든 아티팩트는 이제 사용 가능한 tooyour 논리 앱의 통합을 보여 주는 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![연결 된 논리 앱 tooyour 통합 계정](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="8b23b-140">이제을 통합 계정을 연결 된 tooyour 논리 앱, 논리 앱에서 B2B hello 커넥터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="8b23b-141">일반적인 B2B 커넥터 일부에는 XML 유효성 검사 및 플랫 파일 인코딩/디코딩이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="8b23b-142">통합 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="8b23b-142">Delete your integration account</span></span>

1. <span data-ttu-id="8b23b-143">**추가 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-143">Select **More services**.</span></span>

    !["추가 서비스"를 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="8b23b-145">Hello 검색 상자에 필터에 대 한 "통합"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="8b23b-146">Hello 결과 목록에서 선택 **통합 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-146">In hello results list, select **Integration Accounts**.</span></span>

    !["통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="8b23b-148">원하는 toodelete hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-148">Select hello integration account that you want toodelete.</span></span>

    ![통합 계정 toodelete 선택](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="8b23b-150">Hello 메뉴에서 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-150">On hello menu, choose **Delete**.</span></span>

    !["삭제" 선택](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="8b23b-152">Choice toodelete hello 통합 계정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="8b23b-153">통합 계정 이동</span><span class="sxs-lookup"><span data-stu-id="8b23b-153">Move your integration account</span></span>

<span data-ttu-id="8b23b-154">toomove 통합 계정 tooanother Azure 구독 또는 리소스 그룹에서 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b23b-155">통합 계정 이동한 후에 모든 스크립트 toouse hello 새 리소스 Id를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="8b23b-156">**추가 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-156">Select **More services**.</span></span>

    !["추가 서비스"를 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="8b23b-158">Hello 검색 상자에 필터에 대 한 "통합"을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="8b23b-159">Hello 결과 목록에서 선택 **통합 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-159">In hello results list, select **Integration Accounts**.</span></span>

    !["통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="8b23b-161">원하는 toomove hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="8b23b-162">**설정** 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-162">Under **Settings**, choose **Properties**.</span></span>

    ![통합 계정 toomove를 선택 합니다.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="8b23b-165">Hello 리소스 그룹 또는 통합 계정에 연결 된 Azure 구독으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b23b-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![리소스 그룹 변경 또는 구독 변경 선택](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="8b23b-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b23b-167">Next Steps</span></span>
* [<span data-ttu-id="8b23b-168">규약에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="8b23b-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  

