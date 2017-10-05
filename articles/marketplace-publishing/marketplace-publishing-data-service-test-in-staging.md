---
title: "Marketplace용 데이터 서비스 제품 테스트 | Microsoft Docs"
description: "Azure 마켓플레이스용 데이터 서비스 제품을 테스트 하는 방법을 이해합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 56a8aad7484fed18b74200ffa7acf22363625a15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="e39c6-103">스테이징에서 데이터 서비스 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="e39c6-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e39c6-104">**현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="e39c6-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="e39c6-105">SaaS 비즈니스 응용 프로그램을 AppSource에 게시하려는 경우 [여기](https://appsource.microsoft.com/partners)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="e39c6-106">IaaS 응용 프로그램 또는 개발자 서비스를 Azure Marketplace에 게시하려는 경우에는 [여기](https://azure.microsoft.com/marketplace/programs/certified/)에서 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="e39c6-107">[Microsoft 개발자 계정 만들기](marketplace-publishing-accounts-creation-registration.md) 및 [게시 포털에서 데이터 서비스 제품 만들기](marketplace-publishing-data-service-creation.md)의 처음 두 단계를 완료하고 나면 Azure Marketplace에 제품을 제공할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span></span> <span data-ttu-id="e39c6-108">이 항목에서는 "스테이징"이라고도 하는 첫 번째(중간) 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-108">This topic will walk you through the first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="e39c6-109">준비 단계에서는 제품을 프로덕션에 게시하기 전에 개인 "샌드박스"에 배포하여 기능을 테스트 및 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="e39c6-110">제품이 해당 제품을 배포한 고객에게 보이는 것처럼 준비 단계에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-110">The offer will appear in staging just as it would to a customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-to-staging"></a><span data-ttu-id="e39c6-111">1단계.</span><span class="sxs-lookup"><span data-stu-id="e39c6-111">Step 1.</span></span> <span data-ttu-id="e39c6-112">제품을 스테이징으로 푸시</span><span class="sxs-lookup"><span data-stu-id="e39c6-112">Pushing your offer to staging</span></span>
<span data-ttu-id="e39c6-113">스테이징으로 제품을 푸시하면 미래의 구독자에게 제품이 제공되기 전에 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span></span>  <span data-ttu-id="e39c6-114">데이터를 구독하는 사람들에게 제품이 어떻게 나타나고 작동하는지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-114">You can see how your offer will appear and function for those subscribing to your data.</span></span>  

  ![그리기](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="e39c6-116">[게시 포털](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="e39c6-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="e39c6-117">왼쪽 탐색 창에서 **데이터 서비스** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-117">Select **Data Services** in the left navigation window</span></span>
3. <span data-ttu-id="e39c6-118">스테이징에 푸시할 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-118">Select your offer you want to push to staging.</span></span> <span data-ttu-id="e39c6-119">위와 같은 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-119">You will see the above screen.</span></span>
4. <span data-ttu-id="e39c6-120">**Push To Staging** (스테이징으로 푸시) 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-120">Click **Push To Staging** button.</span></span>  
5. <span data-ttu-id="e39c6-121">스테이징에 푸시하기 전에 제품에 대해 마무리해야 하는 문제가 있으면 해당 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span></span>  <span data-ttu-id="e39c6-122">목록에서 각 항목을 클릭하여 이런 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-122">Correct these items by clicking on each item in the list.</span></span> <span data-ttu-id="e39c6-123">해결이 완료되면 **Push to Staging** (스테이징으로 푸시) 단추를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-123">When all corrections made, click **Push to Staging** button again.</span></span>

<span data-ttu-id="e39c6-124">제품에 문제가 없으면 아래와 같은 팝업 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-124">If there are no issues with your offer you will see the popup window below.</span></span>  

<span data-ttu-id="e39c6-125">Azure 포털에 제품을 공개할 계획이 없거나 승인을 받지 못한 경우에는(현재 용량이 제한되어 있음) 팝업 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span></span>

<span data-ttu-id="e39c6-126">DataMarket 포털 외에 Azure 포털에서도 데이터 서비스를 테스트하려면 테스트에 사용할 Azure 구독 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span></span>  <span data-ttu-id="e39c6-127">구독 ID를 통해 제품 테스트가 허용되는 계정을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-127">This Subscription ID will identify the account that will be allowed to test your offer.</span></span>  

<span data-ttu-id="e39c6-128">구독 ID를 잘라내어 붙여넣고 확인 표시를 클릭하여 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-128">Cut and paste your Subscription ID and click the checkmark to continue.</span></span>

  ![그리기](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="e39c6-130">Azure 구독 ID는 [Azure 관리 포털](https://manage.windowsazure.com)내에서의 테스트와 스테이징에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="e39c6-131">Azure 마켓플레이스에서 테스트하는 경우에는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-131">They are not required to test in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="e39c6-132">다음으로 표시되는 화면에서는 아래에 노란색으로 강조 표시된 “진행 중” 아이콘을 표시하여 게시가 이루어지고 있다는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="e39c6-133">스테이징으로 푸시는 10분에서 15분 정도 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-133">Pushing to staging takes between 10 to 15 minutes.</span></span>  <span data-ttu-id="e39c6-134">이보다 오래 걸리면 우선 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="e39c6-135">(IE에서 F5키를 누릅니다.) 드문 경우지만, 한 시간이 지난 후에도 제품을 스테이징으로 푸시하고 있으면, 문의처 링크를 클릭하여 문제가 있다는 것을 알려 주세요.</span><span class="sxs-lookup"><span data-stu-id="e39c6-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span></span>

  ![그리기](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="e39c6-137">스테이징으로 푸시가 완료되면 “진행 중” 아이콘이 움직임을 멈추고 상태가 “준비됨”으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span></span>  <span data-ttu-id="e39c6-138">이제 제품을 테스트할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-138">You are now ready to test your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="e39c6-139">2단계.</span><span class="sxs-lookup"><span data-stu-id="e39c6-139">Step 2.</span></span> <span data-ttu-id="e39c6-140">DataMarket에서 준비된 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="e39c6-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="e39c6-141">**“See Your service offer at…”**</span><span class="sxs-lookup"><span data-stu-id="e39c6-141">Click the link following the text **“See Your service offer at…”**</span></span> <span data-ttu-id="e39c6-142">텍스트 다음에 나오는 링크를 클릭하여 제품이 프로덕션으로 이동하고 DataMarket에 공개되면 구독자에게 보여질 화면을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span></span>

  ![그리기](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="e39c6-144">위에 표시된 12개 항목을 일일이 테스트하거나 검사하여 로고, 가격/트랜잭션, 텍스트, 이미지, 설명서, 링크가 모두 맞는지, 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="e39c6-145">제품을 만들 때 입력한 테스트 값이 실제 값으로 변경되었는지를 확인할 수 있는 좋은 기회입니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="e39c6-146">제품 로고</span><span class="sxs-lookup"><span data-stu-id="e39c6-146">Offer logo</span></span>
2. <span data-ttu-id="e39c6-147">Offer name</span><span class="sxs-lookup"><span data-stu-id="e39c6-147">Offer name</span></span>
3. <span data-ttu-id="e39c6-148">게시자 이름/회사 웹 사이트 링크</span><span class="sxs-lookup"><span data-stu-id="e39c6-148">Publisher name/link to your company's website</span></span>
4. <span data-ttu-id="e39c6-149">제품에 대한 검색 범주</span><span class="sxs-lookup"><span data-stu-id="e39c6-149">Search categories for your offer</span></span>
5. <span data-ttu-id="e39c6-150">구독자 지원을 위한 제품 지원 링크</span><span class="sxs-lookup"><span data-stu-id="e39c6-150">Your offer's support link to assist subscribers</span></span>
6. <span data-ttu-id="e39c6-151">제품에 대한 상황별 설명</span><span class="sxs-lookup"><span data-stu-id="e39c6-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="e39c6-152">청구 세부 정보를 설명하는 제품 계획</span><span class="sxs-lookup"><span data-stu-id="e39c6-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="e39c6-153">구현 코드에 대한 링크</span><span class="sxs-lookup"><span data-stu-id="e39c6-153">Link to implementation code</span></span>
9. <span data-ttu-id="e39c6-154">제품 데이터 사용을 보여주는 샘플 이미지</span><span class="sxs-lookup"><span data-stu-id="e39c6-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="e39c6-155">제품 내 각 서비스에 대한 입/출력 메타데이터</span><span class="sxs-lookup"><span data-stu-id="e39c6-155">Input/Output metadata for each service within the offer</span></span>
11. <span data-ttu-id="e39c6-156">제품 사용 약관</span><span class="sxs-lookup"><span data-stu-id="e39c6-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="e39c6-157">제품 데이터 미리 보기</span><span class="sxs-lookup"><span data-stu-id="e39c6-157">Preview of the offer's data</span></span>

<span data-ttu-id="e39c6-158">마지막으로 “EXPLORE THIS DATASET”(DATASET 탐색) 링크를 클릭하여 서비스가 Datamarket을 통과하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="e39c6-159">서비스에 대한 쿼리의 결과를 미리 볼 수 있도록 “Service Explorer”(서비스 탐색기)라는 도구에 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span></span>  <span data-ttu-id="e39c6-160">창에서 필요한 매개 변수를 입력하고 서비스에 대한 쿼리를 통해 표시되는 결과를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span></span>   <span data-ttu-id="e39c6-161">쿼리에 대한 URL로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-161">Also, displayed is the URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="e39c6-162">위쪽에 표시되는 서비스에 대한 텍스트 설명을 반드시 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-162">Be sure to review the textual description of the service displayed at the top.</span></span>  <span data-ttu-id="e39c6-163">제품이 둘 이상의 서비스 호출로 구성되는 경우에는 아래쪽의 탭을 클릭하고 다음 서비스로 전환하여 검토하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e39c6-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="e39c6-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e39c6-164">Next step</span></span>
<span data-ttu-id="e39c6-165">문제가 있고 해결하기 위해서 도움이 필요하면 [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e39c6-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="e39c6-166">결과가 만족스럽고 제품을 게시할 준비가 되면 [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) (프로덕션에 푸시할 승인 요청) 설명서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="e39c6-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="e39c6-167">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e39c6-167">See Also</span></span>
* [<span data-ttu-id="e39c6-168">시작: Azure 마켓플레이스에 제품을 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="e39c6-168">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

