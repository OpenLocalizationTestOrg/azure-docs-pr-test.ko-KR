---
title: "Azure Marketplace 지급 보고 이해 | Microsoft Docs"
description: "Azure 마켓플레이스 지급 보고서를 검토하고 수집하는 방법을 알아봅니다."
services: marketplace-publishing
documentationcenter: na
author: v-jeana
manager: lakoch
editor: 
ms.assetid: 3e99aefe-abeb-414c-8689-15352d25aefd
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: v-jeana; hascipio; v-dabosl
ms.openlocfilehash: 5a89e9ba4376d0c4f49feb3783692e28a28902a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-marketplace-payout-reports"></a><span data-ttu-id="7053b-103">Azure 마켓플레이스 지급 보고서 이해</span><span class="sxs-lookup"><span data-stu-id="7053b-103">Understand your Azure Marketplace payout reports</span></span>
## <a name="access-and-view-your-payout-reports"></a><span data-ttu-id="7053b-104">지급 보고서 액세스 및 보기</span><span class="sxs-lookup"><span data-stu-id="7053b-104">Access and view your payout reports</span></span>
<span data-ttu-id="7053b-105">개발자 센터로 전환함에 따라 일부 지급 보고서는 https://dev.windows.com/en-us의 개발자 센터에서 제공되지만 일부는 https://publish.windowsazure.com의 게시 포털에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-105">While we transition to Dev Center some of your payout reports may be available in the Dev Center at https://dev.windows.com/en-us while others may still be found in Publishing Portal at https://publish.windowsazure.com.</span></span>

<span data-ttu-id="7053b-106">지급 보고는 최신 지급과 관련된 모든 마켓플레이스 제품에 대한 **개발자 센터** 에서 제공되며 현재 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-106">Payout reporting will now be available in **Dev Center** for any Marketplace offerings that are associated with modern payouts; this currently includes:</span></span>

* <span data-ttu-id="7053b-107">VM</span><span class="sxs-lookup"><span data-stu-id="7053b-107">VMs</span></span>
* <span data-ttu-id="7053b-108">B+C 제품</span><span class="sxs-lookup"><span data-stu-id="7053b-108">B+C offers</span></span>
* <span data-ttu-id="7053b-109">EA에서 제공되는 데이터 및 개발자 서비스</span><span class="sxs-lookup"><span data-stu-id="7053b-109">Data and Dev Services offered under EA</span></span>

<span data-ttu-id="7053b-110">다음에 대한 지급 보고는 **게시 포털** 에 계속 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-110">Payout reporting will still be in **Publishing Portal** for:</span></span>

* <span data-ttu-id="7053b-111">Direct 웹에 따라 제공되는 데이터 및 개발자 서비스(계속 레거시 지불 시스템 사용).</span><span class="sxs-lookup"><span data-stu-id="7053b-111">Data and Dev Services offered under Web Direct (which still uses the legacy payout system).</span></span>

<span data-ttu-id="7053b-112">보고서는 분기가 끝난 후 45일이 지나면 사용할 수 있으며 모든 환불이 이루어진 후에 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-112">Reports are available 45 days after the close of the quarter and are calculated after any refunds.</span></span>

### <a name="access-payout-reports-in-dev-center"></a><span data-ttu-id="7053b-113">개발자 센터에서 지급액 보고서 액세스</span><span class="sxs-lookup"><span data-stu-id="7053b-113">Access payout reports in Dev Center</span></span>
1. <span data-ttu-id="7053b-114">https://dev.windows.com/en-us에서 개발자 센터로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-114">Navigate to Dev Center at https://dev.windows.com/en-us.</span></span>
2. <span data-ttu-id="7053b-115">**대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-115">Click **Dashboard**.</span></span>

    ![LandingPageDashboardHighlight][1]
3. <span data-ttu-id="7053b-117">**지급액 요약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-117">Click **Payout Summary**.</span></span>

    ![DashboardPayoutSummary][2]

## <a name="view-your-payout-reports-in-dev-center"></a><span data-ttu-id="7053b-119">개발자 센터에서 지급 보고서 확인</span><span class="sxs-lookup"><span data-stu-id="7053b-119">View your payout reports in Dev Center</span></span>
<span data-ttu-id="7053b-120">각 분기에 대한 지급 보고서는 해당 분기 내에 발생한 모든 트랜잭션을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-120">The payout report for each quarter records all transactions that occurred within that quarter.</span></span>

* <span data-ttu-id="7053b-121">예약된 금액은 예정된 결제 주기를 벗어나 발생하는 모든 지급을 나타냅니다(예: 이 금액은 다음 달 다음 결제로 이월됨).</span><span class="sxs-lookup"><span data-stu-id="7053b-121">The Reserved amount indicates any payments that are accruing outside of the upcoming payment cycle (e.g. this amount will move to upcoming payment the following month).</span></span>  <span data-ttu-id="7053b-122">이 금액은 일반적으로 $0(고객이 사전에 제대로 지불하지 않은 경우)입니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-122">This amount will typically be $0 (unless a customer pays well in advance).</span></span>
* <span data-ttu-id="7053b-123">해당 지급에 대한 정보를 확인하려면 예정된 결제 또는 최근 결제 **세부 정보 보기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-123">Click on the Upcoming payment or Most recent payment **View details** links to see a note about those payouts.</span></span>
* <span data-ttu-id="7053b-124">앱/제품별 수익 세부 정보를 보려면 **지불 명세서** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-124">Click on **Payment Statements** to view the details under proceeds by app/product.</span></span>
* <span data-ttu-id="7053b-125">개별 명세서를 보려면 **보기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-125">Click on the **View** link to see individual statements.</span></span>

    ![PayoutSummaryUpcomingMostRecentLinksStatement][3]
* <span data-ttu-id="7053b-127">여러 앱/제품을 보려면 개별 명세서 하단에 있는 **수익 분석** 필터를 사용합니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="7053b-127">Use the **Proceeds Breakdown** filter at the bottom of the individual statement to view multiple apps/products if they exist.</span></span>

    ![PayoutSummaryPaymentStatementsFilterControl][4]

## <a name="view-your-payout-reports-in-publishing-portal"></a><span data-ttu-id="7053b-129">게시 포털에서 지급 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="7053b-129">View your payout reports in Publishing Portal</span></span>
<span data-ttu-id="7053b-130">각 분기에 대한 지급 보고서는 해당 분기 내에 발생한 모든 트랜잭션을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-130">The payout report for each quarter records all transactions that occurred within that quarter.</span></span>

1. <span data-ttu-id="7053b-131">https://publish.windowsazure.com에서 게시 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-131">Navigate to the publishing portal at https://publish.windowsazure.com.</span></span>
2. <span data-ttu-id="7053b-132">**게시자** 섹션에서 **지급 보고서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-132">From the **Publishers** section, click **Payout Reports**.</span></span>
3. <span data-ttu-id="7053b-133">드롭다운을 클릭하면 사용할 수 있는 모든 분기별 지급 보고서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-133">Click the drop-down to display all available quarterly payout reports.</span></span>

    ![accessingpayoutreport][5]

### <a name="read-your-payout-reports"></a><span data-ttu-id="7053b-135">지급 보고서 읽기</span><span class="sxs-lookup"><span data-stu-id="7053b-135">Read your payout reports</span></span>
<span data-ttu-id="7053b-136">각 분기에 대한 지급 보고서는 해당 분기 내에 발생한 모든 트랜잭션을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-136">The payout report for each quarter records all transactions that occurred within that quarter.</span></span>

* <span data-ttu-id="7053b-137">특정 분기와 관련된 원장 항목을 찾으려면 드롭다운에서 해당 분기에 대한 지급 보고서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-137">If you are looking for ledger entries that relate to a particular quarter, select the payout report for that quarter from the drop-down.</span></span> <span data-ttu-id="7053b-138">예를 들어 2015년 4~6월에 대한 원장 항목을 보려면 드롭다운 메뉴에서 해당 날짜 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-138">For example, if you are interested in ledger entries for April to June 2015, select that date range from the drop-down.</span></span>
* <span data-ttu-id="7053b-139">특정 분기와 관련된 지급 정보를 찾으려면 드롭다운에서 후속 분기에 대한 지급 보고서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-139">If you are looking for details of payouts that relate to a particular quarter, select the payout report for the subsequent quarter.</span></span> <span data-ttu-id="7053b-140">예를 들어 2015년 4~6월에 대한 지급을 보려는 경우 2015년 7~9월에 대한 후속 지급 보고서에 해당 금액이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-140">For example, if you are interested in the payouts for April to June 2015, these amounts will appear in the subsequent payout report for July to September 2015.</span></span>
  <span data-ttu-id="7053b-141">![readingpayoutreport][6]</span><span class="sxs-lookup"><span data-stu-id="7053b-141">![readingpayoutreport][6]</span></span>
* <span data-ttu-id="7053b-142">재무 요약 패널은 잔액, 대변과 차변을 범주별로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-142">The financial summary panel shows balances, credits, and debits by category.</span></span>
* <span data-ttu-id="7053b-143">원장 항목은 개별 트랜잭션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-143">Ledger entries show individual transactions.</span></span>

## <a name="definitions"></a><span data-ttu-id="7053b-144">정의</span><span class="sxs-lookup"><span data-stu-id="7053b-144">Definitions</span></span>
<span data-ttu-id="7053b-145">**재무 요약 패널:**</span><span class="sxs-lookup"><span data-stu-id="7053b-145">**Financial summary panel:**</span></span>

![financialdefinitions][7]

<span data-ttu-id="7053b-147">**원장 항목:**</span><span class="sxs-lookup"><span data-stu-id="7053b-147">**Ledger entries:**</span></span>

![ledgerdefinitions][8]

## <a name="payout-questions"></a><span data-ttu-id="7053b-149">지급 질문</span><span class="sxs-lookup"><span data-stu-id="7053b-149">Payout questions</span></span>
<span data-ttu-id="7053b-150">지급에 관한 질문이 있는 경우 지원 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7053b-150">If you have a question related to your payouts, contact our support team.</span></span>

![payoutquestions][9]

1. <span data-ttu-id="7053b-152">지원 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-152">Navigate to the support pages.</span></span>
2. <span data-ttu-id="7053b-153">**지급액**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-153">Select **Payouts**.</span></span>
3. <span data-ttu-id="7053b-154">**지급액 관련 문의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-154">Select **Payout related inquiries**.</span></span>
4. <span data-ttu-id="7053b-155">**요청 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7053b-155">Click **Start request**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7053b-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7053b-156">Next steps</span></span>
<span data-ttu-id="7053b-157">기타 지원 쿼리는 <https://portal.azure.com>에서 문제를 기록하세요.</span><span class="sxs-lookup"><span data-stu-id="7053b-157">For other support queries, please log an issue at <https://portal.azure.com>.</span></span>

[1]: ./media/marketplace-publishing-report-payout/LandingPage-DashboardHighlight.png
[2]: ./media/marketplace-publishing-report-payout/Dashboard-PayoutSummary.png
[3]: ./media/marketplace-publishing-report-payout/PayoutSummary-UpcomingOrMostRecentPaymentLinksSingleStatementLink.png
[4]: ./media/marketplace-publishing-report-payout/PayoutSummary-PaymentStatements-SingleStatement-FilterControl.png
[5]: ./media/marketplace-publishing-report-payout/accessingpayoutreport.png
[6]: ./media/marketplace-publishing-report-payout/readingpayoutreport.png
[7]: ./media/marketplace-publishing-report-payout/financialdefinitions.png
[8]: ./media/marketplace-publishing-report-payout/ledgerdefinitions.png
[9]: ./media/marketplace-publishing-report-payout/payoutquestions.png
