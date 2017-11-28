---
title: "aaaSet를 사용 하 여 컴퓨터 학습 권장 사항을 API hello | Microsoft Docs"
description: "Azure 기계 학습을 사용하여 빌드한 Microsoft 권장 사항 API FAQ"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="0b1e2-103">기계 학습 권장 사항 API 설정 및 사용에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="0b1e2-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="0b1e2-104">**권장 사항이란 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="0b1e2-105">이 버전 대신 hello 권장 API Cognitive 서비스를 사용 하 여 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-105">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="0b1e2-106">hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="0b1e2-107">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="0b1e2-108">에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="0b1e2-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="0b1e2-109">조직 및 권장 사항 toocross 판매 상향 판매 제품 및 서비스 tootheir 고객 필요로 하는 비즈니스에 대 한 Azure 기계 학습의 권장 사항을 셀프 서비스 권장 사항을 엔진을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-109">For organizations and businesses that rely on recommendations toocross-sell and up-sell products and services tootheir customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="0b1e2-110">이는 행렬 인수분해를 핵심 알고리즘으로 사용한 공동 작업 필터링 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="0b1e2-111">응용 프로그램 개발자는 REST API를 사용하여 RECOMMENDATIONS에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0b1e2-112">**권장 사항으로 무엇을 수행할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="0b1e2-113">권장 사항은 항목 또는 항목 집합을 입력으로 이용하고 관련 권장 사항 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="0b1e2-114">예를 들어 한 온라인 소매점의 고객이 제품을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="0b1e2-115">hello 온라인 상점 tooRECOMMENDATIONS 입력된으로 해당 제품을 보냅니다, 그리고 제품, 가져오고 toohello 고객을 표시 중 이러한 제품을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-115">hello online retailer sends that product as input tooRECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown toohello customer.</span></span> <span data-ttu-id="0b1e2-116">원하는 toouse 권장 사항을 toooptimize 서 온라인 상점 수도 tooinform 프로그램 내부에도 판매 부서 또는 call center 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-116">You may want toouse RECOMMENDATIONS toooptimize your online store or even tooinform your inside sales department or call center.</span></span>

<span data-ttu-id="0b1e2-117">**사용 제한이 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="0b1e2-118">권장 사항에는 다음과 같은 제한을 사용 하는 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-118">Recommendations has hello following usage limitations:</span></span>

* <span data-ttu-id="0b1e2-119">구독당 최대 모델 수: 10</span><span class="sxs-lookup"><span data-stu-id="0b1e2-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="0b1e2-120">카탈로그에 포함할 수 있는 최대 항목 수: 100,000</span><span class="sxs-lookup"><span data-stu-id="0b1e2-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="0b1e2-121">hello 사용 포인트 유지 되는 최대 수에는 ~ 5,000,000는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-121">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="0b1e2-122">새로 업로드 되거나 보고 되는 경우 가장 오래 된 hello 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-122">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="0b1e2-123">메일로 전송할 수 있는 최대 데이터 크기(예: 카탈로그 데이터 가져오기, 사용 현황 데이터 가져오기)는 200MB입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="0b1e2-124">활성화되지 않은 권장 사항 모델 빌드에 대한 TPS(초당 트랜잭션 수)는 최대 2TPS입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="0b1e2-125">활성화 된 권장 사항을 모델 빌드 too20 TPS를 보유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-125">A Recommendations model build that is active can hold up too20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="0b1e2-126">구매 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="0b1e2-126">Purchase and Billing</span></span>
<span data-ttu-id="0b1e2-127">**비용은 얼마 입니까 권장 사항을 hello 실행 기간 동안?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-127">**How much does Recommendations cost during hello launch period?**</span></span>

<span data-ttu-id="0b1e2-128">권장 사항은 구독 기반 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="0b1e2-129">요금 청구는 월별 트랜잭션 볼륨 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="0b1e2-130">Hello를 확인할 수 있습니다 [페이지 제공](https://datamarket.azure.com/dataset/amla/recommendations) 가격 정보에 대 한 Microsoft Azure Marketplace에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-130">You can check hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="0b1e2-131">**권장 사항 추적 및 저장 사용자 활동을 포함하는 것과 관련된 비용이 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="0b1e2-132">에 hello 시점입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-132">Not at hello moment.</span></span>

<span data-ttu-id="0b1e2-133">**권장 사항에 무료 평가판이 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="0b1e2-134">제한 된 too10, 000 월별 트랜잭션 수 있는 무료 내역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-134">There is a free trail which is restricted too10,000 transactions per month.</span></span>

<span data-ttu-id="0b1e2-135">**권장 사항에 대한 요금은 언제 청구됩니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="0b1e2-136">유료 구독은 월별 요금이 있는 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="0b1e2-137">유료 구독을 구매 하는 경우 즉시 요금이 청구 되므로 hello에 대 한 처음 월의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-137">When you purchase a paid subscription, you are immediately charged for hello first month's use.</span></span> <span data-ttu-id="0b1e2-138">Hello 제공 서비스로 hello 구독 페이지 (및 해당 세금)에 연결 되어 있는 hello 금액을 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-138">You are charged hello amount that is associated with hello offer on hello subscription page (plus applicable taxes).</span></span> <span data-ttu-id="0b1e2-139">이 월별 요금은 hello 구독을 취소할 때까지 원래 구매한 날짜 달력 동일 hello에 각 달 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-139">This monthly charge is made each month on hello same calendar date as your original purchase until you cancel hello subscription.</span></span> 

<span data-ttu-id="0b1e2-140">**Tooa 더 높은 계층 서비스를 업그레이드 하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-140">**How do I upgrade tooa higher tier service?**</span></span>

<span data-ttu-id="0b1e2-141">구입 하거나 hello에서 구독을 업데이트할 수 있습니다 [페이지 제공](https://datamarket.azure.com/dataset/amla/recommendations) Microsoft Azure 마켓플레이스에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-141">You can buy or update your subscription from hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="0b1e2-142">구독을 업그레이드할 경우:</span><span class="sxs-lookup"><span data-stu-id="0b1e2-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="0b1e2-143">이전 구독에는 남은 트랜잭션은 새 구독 tooyour 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-143">Transactions that are remaining on your old subscription are not added tooyour new subscription.</span></span> 
* <span data-ttu-id="0b1e2-144">있더라도 hello 새 구독에 대 한 전체 가격을 지불 이전 구독에 사용 하지 않은 트랜잭션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-144">You pay full price for hello new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="0b1e2-145">프로세스 tooupgrade 구독:</span><span class="sxs-lookup"><span data-stu-id="0b1e2-145">Process tooupgrade a subscription:</span></span>

* <span data-ttu-id="0b1e2-146">Nevigate toohello [페이지 제공](https://datamarket.azure.com/dataset/amla/recommendations)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-146">Nevigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="0b1e2-147">로그인 하지 않은 경우 toohello Marketplace에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-147">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="0b1e2-148">Hello 사용 가능한 모든 계획은 hello 오른쪽 창에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-148">In hello right pane, all hello available plans are listed.</span></span> <span data-ttu-id="0b1e2-149">tooupgrade hello 계획에 대 한 hello 라디오 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-149">Click hello radio button for hello plan you want tooupgrade to.</span></span>
* <span data-ttu-id="0b1e2-150">Tooupgrade 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-150">If you want tooupgrade, click **OK**.</span></span> <span data-ttu-id="0b1e2-151">Tooupgrade 하지 않으려면 클릭 **취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-151">If you do not want tooupgrade, click **Cancel**.</span></span>

<span data-ttu-id="0b1e2-152">**중요 한** 대금 청구 및 사용에 영향을 줄 있기 때문에 업그레이드 하기 전에 신중 하 게 읽기 hello 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-152">**Important** Carefully read hello dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="0b1e2-153">**내 구독 tooRecommendations 끝납니다 하는 경우**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-153">**When will my subscription tooRecommendations end?**</span></span>

<span data-ttu-id="0b1e2-154">구독은 고객이 구독을 취소할 때 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="0b1e2-155">Toocancel 원하는 경우 구독 hello 다음 지침을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-155">If you would like toocancel your subscriptions, see hello following instructions.</span></span>

<span data-ttu-id="0b1e2-156">**권장 사항 구독을 취소하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="0b1e2-157">구독을 사용 하 여 hello 다음 단계를 toocancel 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-157">toocancel your subscription, use hello following steps.</span></span> <span data-ttu-id="0b1e2-158">유료 구독이 현재 구독을 사용 하는 경우 구독 청구 기간 현재 hello hello 끝날 때까지 적용 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-158">If your current subscription is a paid subscription, your subscription continues in effect until hello end of hello current billing period.</span></span> <span data-ttu-id="0b1e2-159">효과적인 취소 toobe를 즉시 hello 필요에 게 문의 하세요. [Microsoft 지원](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-159">If you need hello cancellation toobe effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="0b1e2-160">**참고** 요금은 환불 되지 않습니다 청구 기간에 청구 기간 또는 사용 하지 않는 트랜잭션에 대 한 hello 종료 전에 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-160">**Note** No refund is given if you cancel before hello end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="0b1e2-161">Toohello 이동 [페이지 제공](https://datamarket.azure.com/dataset/amla/recommendations)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-161">Navigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="0b1e2-162">로그인 하지 않은 경우 toohello Marketplace에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-162">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="0b1e2-163">클릭 **취소** toohello hello 데이터 집합 이름 및 상태 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-163">Click **Cancel** toohello right of hello dataset name and status.</span></span> <span data-ttu-id="0b1e2-164">현재 청구 기간 되거나 트랜잭션 제한 hello hello 끝 (중 먼저 발생)에 도달할 때까지이 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-164">You can use this subscription until hello end of hello current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="0b1e2-165">파일에서 티켓을 새 구독을 구입할 수 있으므로 즉시 구독 toocancel 원하는 경우 [Microsoft 지원](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-165">If you would like toocancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="0b1e2-166">권장 사항 시작하기</span><span class="sxs-lookup"><span data-stu-id="0b1e2-166">Getting started with Recommendations</span></span>
<span data-ttu-id="0b1e2-167">**권장 사항이 고객에게 적합합니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="0b1e2-168">기계 학습의 권장 사항을 조직 및 권장 사항 toocross 판매 및 상향 판매 제품 또는 서비스 tootheir 고객에 의존 하는 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations toocross-sell and up-sell products or services tootheir customers.</span></span> <span data-ttu-id="0b1e2-169">고객을 응대하는 웹 사이트, 영업 인력, 내부 판매 인력 또는 콜 센터가 있고 수십 개의 제품이나 서비스가 포함된 카탈로그를 제공하는 경우 권장 사항을 활용하여 수익을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="0b1e2-170">권장 사항을 작업할 수 있도록 설계 된 toobe 매우 단순한입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-170">Experimenting with Recommendations is designed toobe fairly simple.</span></span> <span data-ttu-id="0b1e2-171">hello 현재 API 기반 버전의 기본 프로그래밍 기술을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-171">hello current API-based version requires basic programming skills.</span></span> <span data-ttu-id="0b1e2-172">도움이 필요 하면 웹 사이트를 개발 하는 hello 공급 업체에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-172">If you need assistance, contact hello vendor who developed your website.</span></span> <span data-ttu-id="0b1e2-173">내부 IT 부서 또는 사내 개발자가 있으면 사용자에 대 한 권장 사항 toowork 수 tooget 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-173">If you have an internal IT department or an in-house developer, they should be able tooget Recommendations toowork for you.</span></span> 

<span data-ttu-id="0b1e2-174">**권장 사항을를 설정 하기 위한 필수 구성 요소 hello 이란?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-174">**What are hello prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="0b1e2-175">권장 사항 tooyour 카탈로그와 관련 사용자 선택 항목의 로그에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-175">Recommendations requires that you have a log of user choices as it relates tooyour catalog.</span></span> <span data-ttu-id="0b1e2-176">해당 로그가 없고 고객 응대 웹 사이트를 운영하는 경우 권장 사항에서 대신 사용자 활동을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="0b1e2-177">권장 사항에는 제품 또는 서비스에 대한 카탈로그도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="0b1e2-178">Hello 카탈로그를 설정 하지 않은 경우 권장 사항을 hello 실제 고객 사용 현황 데이터를 사용할 수 있으며 추출 카탈로그.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-178">If you don't have hello catalog, Recommendations can use hello actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="0b1e2-179">"묵시적" 카탈로그에는 사용자 트랜잭션의 일부로 "보고"되지 않은 항목이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="0b1e2-180">**어떻게 설정 하나요 권장 사항을 hello에 대 한 처음으로?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-180">**How do I set up Recommendations for hello first time?**</span></span>

<span data-ttu-id="0b1e2-181">후 [구독](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, hello에 hello API 설명서를 사용 해야 [Azure 시스템 학습 권장 사항-빠른 시작 가이드](machine-learning-recommendation-api-quick-start-guide.md) tooset hello 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, you should use hello API documentation in hello [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello service.</span></span>

<span data-ttu-id="0b1e2-182">**API 설명서는 어디서 찾을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="0b1e2-183">hello API 설명서는 [Azure 시스템 학습 권장 사항-빠른 시작 가이드](machine-learning-recommendation-api-quick-start-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-183">hello API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="0b1e2-184">**옵션의 대신할 tooupload 카탈로그 및 사용 현황 데이터 tooRecommendations 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-184">**What options do I have tooupload catalog and usage data tooRecommendations?**</span></span>

<span data-ttu-id="0b1e2-185">카탈로그 및 사용 현황 데이터를 업로드 하기 위한 두 가지 옵션이 있습니다: 하 여 CRM 시스템 이나 다른 로그에서 hello 데이터를 내보낼 tooRecommendations를 업로드 하거나 사용자 활동을 추적 하는 태그 tooyour 웹 사이트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-185">You have two options for uploading your catalog and usage data: You can export hello data from your CRM system or other logs and upload it tooRecommendations, or you can add tags tooyour website that will track user activities.</span></span> <span data-ttu-id="0b1e2-186">Hello 두 번째 방법을 사용 하는 경우 Azure의 hello 데이터 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-186">If you use hello latter method, hello data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="0b1e2-187">유지 관리 및 지원</span><span class="sxs-lookup"><span data-stu-id="0b1e2-187">Maintenance and support</span></span>
<span data-ttu-id="0b1e2-188">**내 데이터 집합은 얼마나 확장할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-188">**How large can my data set be?**</span></span>

<span data-ttu-id="0b1e2-189">각 데이터 집합 사용 현황 데이터의 too2048 MB를 too100, 000 카탈로그 항목을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-189">Each data set can contain up too100,000 catalog items and up too2048 MB of usage data.</span></span>
<span data-ttu-id="0b1e2-190">또한 구독 too10 데이터 집합 (모델)을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-190">In addition, a subscription can contain up too10 data sets (models).</span></span>

<span data-ttu-id="0b1e2-191">**권장 사항에 대한 기술 지원은 어디서 받을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="0b1e2-192">기술 지원은 hello에서 사용할 수 있는 [Microsoft Azure 지원](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-192">Technical support is available on hello [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="0b1e2-193">**사용 약관 hello 어디에 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="0b1e2-193">**Where can I find hello terms of use?**</span></span>

<span data-ttu-id="0b1e2-194">[Microsoft Azure 기계 학습 권장 사항 API 서비스 약관](https://datamarket.azure.com/dataset/amla/recommendations#terms)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b1e2-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

