---
title: "Microsoft Azure StorSimple 및 클라우드 솔루션 공급자 프로그램 개요 | Microsoft Docs"
description: "StorSimple 파트너용 StorSimple 및 CSP에 대한 개요입니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: c8cb51093142146fc7d43b51a62d949f6cc38988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="0eaaa-103">클라우드 솔루션 공급자 프로그램용 StorSimple 가상 배열 배포</span><span class="sxs-lookup"><span data-stu-id="0eaaa-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="0eaaa-104">개요</span><span class="sxs-lookup"><span data-stu-id="0eaaa-104">Overview</span></span>

<span data-ttu-id="0eaaa-105">고객에게 CSP(클라우드 솔루션 공급자) 파트너를 통해 StorSimple 가상 배열을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="0eaaa-106">CSP 파트너는 StorSimple 장치 관리자 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="0eaaa-107">StorSimple 가상 배열 및 연결된 공유, 볼륨 및 백업을 배포하고 관리하는 데 이 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span></span>

<span data-ttu-id="0eaaa-108">이 문서에서는 CSP 파트너가 고객을 추가하거나 기존 고객에 새 구독을 추가한 다음 CSP에서 StorSimple 가상 배열을 배포하는 서비스를 만들 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0eaaa-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0eaaa-109">Prerequisites</span></span>

<span data-ttu-id="0eaaa-110">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="0eaaa-111">CSP 프로그램에서 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-111">You are enrolled under the CSP program.</span></span>
- <span data-ttu-id="0eaaa-112">올바른 [파트너 센터](http://partnercenter.microsoft.com/) 로그인 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="0eaaa-113">자격 증명을 사용하여 파트너 포털에 로그인하여 새 고객을 추가하고 고객을 검색하거나 파트너 대시보드에서 고객 계정으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span></span> <span data-ttu-id="0eaaa-114">CSP는 Azure Portal에서 고객을 대신하여 StorSimple 관리자로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="0eaaa-115">고객 추가</span><span class="sxs-lookup"><span data-stu-id="0eaaa-115">Add a customer</span></span>

<span data-ttu-id="0eaaa-116">고객을 추가하는 경우 구독이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="0eaaa-117">고객을 추가하려면(및 구독을 자동으로 만들려면) 파트너 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="0eaaa-118">[파트너 센터](http://partnercenter.microsoft.com/)로 이동하고 CSP 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="0eaaa-119">**대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-119">Click **Dashboard**.</span></span>

     ![파트너 센터의 대시보드](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="0eaaa-121">왼쪽 창에서 **고객**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-121">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="0eaaa-122">오른쪽 창에서 **고객 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-122">In the right-pane, click **Add customers**.</span></span> <span data-ttu-id="0eaaa-123">고객의 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-123">Enter the details of the customer.</span></span> <span data-ttu-id="0eaaa-124">**다음: 구독**을 클릭하여 고객 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-124">Click **Next: Subscriptions** to create a customer subscription.</span></span>

    ![고객 추가](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="0eaaa-126">**Microsoft Azure** 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="0eaaa-127">페이지의 아래쪽으로 스크롤하고 **검토**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-127">Scroll to the bottom of the page and click **Review**.</span></span>

    ![구독 정보 검토](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="0eaaa-129">정보를 검토하고 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-129">Review the information and click **Submit**.</span></span>

    ![구독 제출](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="0eaaa-131">나중에 참조할 수 있도록 확인 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-131">Save the confirmation information for future reference.</span></span>

    ![확인 저장](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="0eaaa-133">방금 추가한 고객을 찾거나 고객으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-133">Find or navigate to the customer you just added.</span></span> <span data-ttu-id="0eaaa-134">**회사 이름**을 클릭하여 세부 정보로 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-134">Click the **Company name** to drill down into the details.</span></span>

    ![고객 검색](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="0eaaa-136">왼쪽 창에서 **서비스 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-136">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="0eaaa-137">오른쪽 창의 **서비스 관리** 아래에서 **Microsoft Azure 관리 포털**을 클릭하여 고객에 대한 Azure 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Azure Portal에 로그인](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="0eaaa-139">StorSimple 장치 관리자를 만들려면 **+ 새로 만들기**를 클릭하고 **StorSimple 가상 장치 시리즈**를 검색하거나 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="0eaaa-140">자세한 내용은 [StorSimple 장치 관리자 서비스 배포](storsimple-virtual-array-manage-service.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![StorSimple 장치 관리자 서비스 만들기](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="0eaaa-142">구독 추가</span><span class="sxs-lookup"><span data-stu-id="0eaaa-142">Add a subscription</span></span>

<span data-ttu-id="0eaaa-143">일부 경우에는 기존 고객이 있을 수 있으며 구독을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-143">In some instances, you may have an existing customer, and you need to add a subscription.</span></span> <span data-ttu-id="0eaaa-144">기존 고객에 구독을 추가하려면 파트너 포털에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="0eaaa-145">[파트너 센터](http://partnercenter.microsoft.com/)로 이동하고 CSP 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="0eaaa-146">**대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-146">Click **Dashboard**.</span></span>

     ![파트너 센터의 대시보드](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="0eaaa-148">왼쪽 창에서 **고객**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-148">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="0eaaa-149">구독을 추가하려는 고객을 찾거나 고객으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-149">Find or navigate to the customer you want to add a subscription to.</span></span> <span data-ttu-id="0eaaa-150">![확인 아이콘 확장](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) 아이콘을 클릭하여 고객의 회사 이름에 대한 행을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-150">Click the ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span></span> <span data-ttu-id="0eaaa-151">세부 정보에서 **구독 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-151">In the details, click **Add subscriptions**.</span></span>

    ![고객](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="0eaaa-153">구독에서 **주요 제안**에 대해 **Microsoft Azure**를 선택하고 **제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span></span> <span data-ttu-id="0eaaa-154">그러면 새 구독이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-154">This creates a new subscription.</span></span>

    ![새 구독 추가](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="0eaaa-156">새 구독을 만든 후 왼쪽 창에서 **<-- 고객**을 클릭하여 **고객** 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span></span> <span data-ttu-id="0eaaa-157">방금 구독을 만든 고객을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-157">Search for the customer for whom you just created a subscription.</span></span> <span data-ttu-id="0eaaa-158">**회사 이름**을 클릭하여 세부 정보로 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-158">Click the **Company name** to drill down into the details.</span></span>

    ![고객 검색](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="0eaaa-160">왼쪽 창에서 **서비스 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-160">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="0eaaa-161">오른쪽 창의 **서비스 관리** 아래에서 **Microsoft Azure 관리 포털**을 클릭하여 고객에 대한 Azure 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Azure Portal에 로그인](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="0eaaa-163">StorSimple 장치 관리자를 만들려면 **+ 새로 만들기**를 클릭하고 **StorSimple 가상 장치 시리즈**를 검색하거나 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="0eaaa-164">자세한 내용은 [StorSimple 장치 관리자 서비스 배포](storsimple-virtual-array-manage-service.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![StorSimple 장치 관리자 서비스 만들기](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="0eaaa-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0eaaa-166">Next steps</span></span>

- <span data-ttu-id="0eaaa-167">CSP의 StorSimple에 대한 추가 질문이 있으면 [CSP의 StorSimple: 질문과 대답](storsimple-partner-csp-faq.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="0eaaa-168">StorSimple을 배포할 준비가 되면 [CSP에서 StorSimple 배포](storsimple-partner-csp-deploy.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaaa-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
