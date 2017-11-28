---
title: "데이터 서비스 마켓플레이스 hello에 대 한 제공 aaaTesting | Microsoft Docs"
description: "이해 어떻게 tootest 데이터 서비스는 hello Azure Marketplace에 대 한을 제공 합니다."
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
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="9df65-103">스테이징에서 데이터 서비스 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="9df65-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9df65-104">**현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="9df65-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="9df65-105">SaaS 비즈니스 응용 프로그램의 경우 원하는 toopublish AppSource에 자세한 정보를 찾을 수 [여기](https://appsource.microsoft.com/partners)합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="9df65-106">IaaS 응용 프로그램 또는 서비스 개발자 경우는 Azure 마켓플레이스에서 toopublish 같은 자세한 정보를 찾을 수 [여기](https://azure.microsoft.com/marketplace/programs/certified/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="9df65-107">Hello의 처음 두 단계를 완료 한 후 [Microsoft 개발자 계정 만들기](marketplace-publishing-accounts-creation-registration.md) 및 [게시 포털에서 데이터 서비스 제공을 만드는](marketplace-publishing-data-service-creation.md) hello에서 제안을 사용 가능 준비가 되었습니다. Azure 마켓플레이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="9df65-108">이 항목은 과정을 단계별로 hello 먼저, 중간, 호출된 "준비" 단계</span><span class="sxs-lookup"><span data-stu-id="9df65-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="9df65-109">개인 테스트 하 고 tooproduction 푸시하기 전에 해당 기능을 확인 수 "샌드박스"에 있는 제품을 배포 하는 수단을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="9df65-110">hello 제공이 배포 tooa 고객과 마찬가지로 준비에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="9df65-111">1단계.</span><span class="sxs-lookup"><span data-stu-id="9df65-111">Step 1.</span></span> <span data-ttu-id="9df65-112">제안 toostaging 푸시</span><span class="sxs-lookup"><span data-stu-id="9df65-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="9df65-113">제안 toostaging 푸시하여 있습니다 tootest hello 제안을 사용할 수 있는 toofuture 구독자 되기 전에.</span><span class="sxs-lookup"><span data-stu-id="9df65-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="9df65-114">제안을 표시 되 고 tooyour 데이터를 구독 하는 것에 대 한 작동 방식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![drawing](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="9df65-116">Hello에 로그인 [게시 포털](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="9df65-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="9df65-117">선택 **데이터 서비스** hello 왼쪽된 탐색 창에서</span><span class="sxs-lookup"><span data-stu-id="9df65-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="9df65-118">Toopush toostaging 원하는 제안을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="9df65-119">Hello 화면 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="9df65-120">클릭 **tooStaging 푸시** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="9df65-121">문제가 있는 경우 hello로 toobe 필요한 제안을 완료 이전 toopushing toostaging, 표시 된 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="9df65-122">Hello 목록의 각 항목을 클릭 하 여 이러한 항목을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="9df65-123">모든 수정 사항은를 클릭 하면 **tooStaging 푸시** 단추를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="9df65-124">제안 된 문제가 없는지 아래 hello 팝업 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="9df65-125">모르는 경우 계획/not 승인 toosurface Azure 포털에 있는 제품 (현재을 제한 한 용량) 한 다음 방금 닫기 hello 팝업 창.</span><span class="sxs-lookup"><span data-stu-id="9df65-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="9df65-126">tootest (더하기 toohello DataMarket 포털)에서 Azure 포털에서 데이터 서비스를 사용 하는 Azure 구독 ID tootest이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="9df65-127">이 구독 ID는 hello 계정 명시 됩니다 tootest 제안을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="9df65-128">잘라내기 구독 ID를 붙여 넣고 hello 확인 표시 toocontinue를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![drawing](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="9df65-130">Azure 구독 Id는만 테스트 하 고 hello를 준비 하는 데 필요한 [Azure 관리 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="9df65-131">Azure Marketplace에서 필요한 tootest 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="9df65-132">hello 다음 화면에 나타나는 표시는 게시 수행 되 고 "진행 중" 에"hello를 표시 하 여 아이콘 아래 노란색으로 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="9df65-133">10 too15 분 걸리며 toostaging 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="9df65-134">이보다 오래 걸리면 우선 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="9df65-135">Hello 드문 경우 지만 자신의 구독 한 시간 후 toostaging 푸시할 여전히는 us 연결 문제가 있다는 것을 알려주세요 toolet hello 연락처를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![drawing](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="9df65-137">Hello 푸시 tooStaging hello 완료 되 면 "에서"진행 중 아이콘 이동 중지 되 고 너무 "준비" hello 상태가 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="9df65-138">사용자는 이제 준비 tootest 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="9df65-139">2단계.</span><span class="sxs-lookup"><span data-stu-id="9df65-139">Step 2.</span></span> <span data-ttu-id="9df65-140">DataMarket에서 준비된 제품 테스트</span><span class="sxs-lookup"><span data-stu-id="9df65-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="9df65-141">Hello 텍스트 다음 hello 링크를 클릭 **"에서 제공 하 여 서비스를 참조 하십시오. …"**</span><span class="sxs-lookup"><span data-stu-id="9df65-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="9df65-142">구독자 hello toodisplay hello 화면 제안을 tooproduction 될 때 표시 되 고 DataMarket에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![drawing](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="9df65-144">모든 로고, 가격/트랜잭션, 텍스트, 이미지, 설명서, tooensure 위에 표시 된 각 hello 12 항목 제대로 링크는 작업 하 고 올바른지 확인 하거나 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="9df65-145">이 실제 값으로 대체 되었습니다 제안을 만들 때 입력 한 모든 테스트 값 좋은 시간 tooensure입니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="9df65-146">제품 로고</span><span class="sxs-lookup"><span data-stu-id="9df65-146">Offer logo</span></span>
2. <span data-ttu-id="9df65-147">Offer name</span><span class="sxs-lookup"><span data-stu-id="9df65-147">Offer name</span></span>
3. <span data-ttu-id="9df65-148">게시자 이름/링크 tooyour 회사 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="9df65-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="9df65-149">제품에 대한 검색 범주</span><span class="sxs-lookup"><span data-stu-id="9df65-149">Search categories for your offer</span></span>
5. <span data-ttu-id="9df65-150">제품의 지원 링크 tooassist 구독자</span><span class="sxs-lookup"><span data-stu-id="9df65-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="9df65-151">제품에 대한 상황별 설명</span><span class="sxs-lookup"><span data-stu-id="9df65-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="9df65-152">청구 세부 정보를 설명하는 제품 계획</span><span class="sxs-lookup"><span data-stu-id="9df65-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="9df65-153">링크 tooimplementation 코드</span><span class="sxs-lookup"><span data-stu-id="9df65-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="9df65-154">제품 데이터 사용을 보여주는 샘플 이미지</span><span class="sxs-lookup"><span data-stu-id="9df65-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="9df65-155">Hello 제공 내에서 각 서비스에 대 한 입/출력 메타 데이터</span><span class="sxs-lookup"><span data-stu-id="9df65-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="9df65-156">제품 사용 약관</span><span class="sxs-lookup"><span data-stu-id="9df65-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="9df65-157">Hello 제품 데이터의 미리 보기</span><span class="sxs-lookup"><span data-stu-id="9df65-157">Preview of hello offer's data</span></span>

<span data-ttu-id="9df65-158">마지막으로 검사 hello 서비스는 hello 링크 "이 데이터 집합 탐색" 클릭 하 여 hello Datamarket 통해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="9df65-159">새 창이 열립니다 hello 도구에서 이라고 "서비스 탐색기" 서비스에 대해 hello 쿼리 결과 미리 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="9df65-160">이 창에서 매개 변수는 필요 하 고 서비스에 대 한 쿼리에서 표시 hello 결과 확인 하는 hello를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="9df65-161">또한 표시 된 쿼리에 대 한 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="9df65-162">수 있는지 tooreview hello 텍스트 hello 서비스 설명 hello 위쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="9df65-163">제안을 하나 이상의 서비스로 구성 된 호출 hello 아래쪽 tooswitch toohello 다음 서비스 tooreview에 hello 탭 클릭 및 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="9df65-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9df65-164">Next step</span></span>
<span data-ttu-id="9df65-165">문제가 있고 해결하기 위해서 도움이 필요하면 [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="9df65-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="9df65-166">만족 스 러 우면 및 준비 toopublish 읽기 hello 하십시오 제안을 [요청 승인 tooPush tooProduction](marketplace-publishing-push-to-production.md) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="9df65-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="9df65-167">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9df65-167">See Also</span></span>
* [<span data-ttu-id="9df65-168">시작 하기: 어떻게 toopublish 제안 toohello Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="9df65-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

