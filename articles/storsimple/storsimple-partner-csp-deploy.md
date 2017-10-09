---
title: "aaaMicrosoft Azure StorSimple 및 클라우드 솔루션 공급자 프로그램 개요 | Microsoft Docs"
description: "StorSimple 파트너에 대 한 StorSimple hello 및 CSP에 대 한 개요."
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
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="c8604-103">클라우드 솔루션 공급자 프로그램용 StorSimple 가상 배열 배포</span><span class="sxs-lookup"><span data-stu-id="c8604-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="c8604-104">개요</span><span class="sxs-lookup"><span data-stu-id="c8604-104">Overview</span></span>

<span data-ttu-id="c8604-105">StorSimple 가상 배열 hello 클라우드 솔루션 공급자 (CSP) 파트너가 고객에 게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="c8604-106">CSP 파트너는 StorSimple 장치 관리자 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="c8604-107">그런 다음 사용된 toodeploy 수 하 고 StorSimple 가상 배열을 관리할 수이 서비스 및 hello 공유, 볼륨 및 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="c8604-108">이 문서에서는 CSP 파트너는 고객 또는 새 구독 tooan 기존 고객을 추가 하 고 다음 CSP 서비스 toodeploy StorSimple 가상 배열을 만들 수 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8604-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c8604-109">Prerequisites</span></span>

<span data-ttu-id="c8604-110">시작하기 전에 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="c8604-111">Hello CSP 프로그램에서 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="c8604-112">올바른 [파트너 센터](http://partnercenter.microsoft.com/) 로그인 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="c8604-113">hello 자격 증명 toosign toohello 파트너 포털 tooadd 새로운 고객에서을 사용 하 고 고객에 대 한 검색 하거나 hello 파트너 대시보드에서 tooa 고객 계정 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="c8604-114">hello CSP hello Azure 포털에에서 hello 고객을 대신 하 여 StorSimple 관리자 권한으로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="c8604-115">고객 추가</span><span class="sxs-lookup"><span data-stu-id="c8604-115">Add a customer</span></span>

<span data-ttu-id="c8604-116">고객을 추가하는 경우 구독이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="c8604-117">tooadd 고객 (및 구독을 자동으로 만들기) hello hello 파트너 포털의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="c8604-118">Toohello 이동 [파트너 센터](http://partnercenter.microsoft.com/) CSP 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="c8604-119">**Dashboard**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-119">Click **Dashboard**.</span></span>

     ![파트너 센터의 대시보드](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="c8604-121">Hello 왼쪽 창에서 클릭 **고객**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="c8604-122">Hello 오른쪽 창에서 클릭 **고객 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="c8604-123">Hello 고객의 hello 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="c8604-124">클릭 **다음: 구독** toocreate 고객 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![고객 추가](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="c8604-126">**Microsoft Azure** 제품을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="c8604-127">클릭 하 고 hello 페이지의 맨 아래로 스크롤 toohello **검토**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![구독 정보 검토](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="c8604-129">Hello 정보를 검토 하 고 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-129">Review hello information and click **Submit**.</span></span>

    ![구독 제출](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="c8604-131">나중에 참조할 hello 확인 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-131">Save hello confirmation information for future reference.</span></span>

    ![확인 저장](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="c8604-133">페이지를 찾거나 방금 추가한 toohello 고객을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="c8604-134">Hello 클릭 **회사 이름** hello 세부 정보로 다운 toodrill 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Hello 고객에 대 한 검색](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="c8604-136">Hello 왼쪽 창에서 선택 **서비스 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="c8604-137">오른쪽 창에서을 아래 hello **서비스 관리**, 클릭 **Microsoft Azure 관리 포털** toosign에서 고객을 위해 Azure 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![TooAzure 포털에 로그인](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="c8604-139">StorSimple 장치 관리자 toocreate 클릭 **+ 새로 만들기** 검색 하거나 너무 탐색 및**StorSimple 가상 장치 시리즈**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="c8604-140">자세한 내용은 이동 너무[StorSimple 장치 관리자 서비스를 배포](storsimple-virtual-array-manage-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![StorSimple 장치 관리자 서비스 만들기](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="c8604-142">구독 추가</span><span class="sxs-lookup"><span data-stu-id="c8604-142">Add a subscription</span></span>

<span data-ttu-id="c8604-143">어떤 경우에는 기존 고객을 할 수 있습니다 하 고 tooadd 구독 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="c8604-144">tooadd 구독 tooan 기존 고객 hello hello 파트너 포털의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="c8604-145">Toohello 이동 [파트너 센터](http://partnercenter.microsoft.com/) CSP 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="c8604-146">**Dashboard**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-146">Click **Dashboard**.</span></span>

     ![파트너 센터의 대시보드](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="c8604-148">Hello 왼쪽 창에서 클릭 **고객**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="c8604-149">페이지를 찾거나 tooadd에 대 한 구독을 원하는 toohello 고객을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="c8604-150">Hello 클릭 ![확장 확인 아이콘](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) 고객을 위해 hello 회사 이름에 대 한 아이콘 tooexpand hello 행입니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="c8604-151">Hello 정보에서 **구독 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-151">In hello details, click **Add subscriptions**.</span></span>

    ![고객](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="c8604-153">확인 **Microsoft Azure** hello에 대 한 **제공 상위** hello 구독 및 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="c8604-154">그러면 새 구독이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-154">This creates a new subscription.</span></span>

    ![새 구독 추가](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="c8604-156">새 구독을 만든 후 클릭 **<-고객** hello 왼쪽 창 tooreturn toohello에 **고객** 페이지.</span><span class="sxs-lookup"><span data-stu-id="c8604-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="c8604-157">에 방금 구독이 만든 hello 고객에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="c8604-158">Hello 클릭 **회사 이름** hello 세부 정보로 다운 toodrill 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Hello 고객에 대 한 검색](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="c8604-160">Hello 왼쪽 창에서 선택 **서비스 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="c8604-161">오른쪽 창에서을 아래 hello **서비스 관리**, 클릭 **Microsoft Azure 관리 포털** toosign에서 고객을 위해 Azure 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![TooAzure 포털에 로그인](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="c8604-163">StorSimple 장치 관리자 toocreate 클릭 **+ 새로 만들기** 검색 하거나 너무 탐색 및**StorSimple 가상 장치 시리즈**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="c8604-164">자세한 내용은 이동 너무[StorSimple 장치 관리자 서비스를 배포](storsimple-virtual-array-manage-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![StorSimple 장치 관리자 서비스 만들기](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="c8604-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8604-166">Next steps</span></span>

- <span data-ttu-id="c8604-167">CSP에서 StorSimple hello에 대 한 추가 질문이 있으면 경우 너무 이동[CSP에서 StorSimple: 질문과 대답](storsimple-partner-csp-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="c8604-168">중인 경우 대기 중인 toodeploy go StorSimple 너무[CSP에 StorSimple을 배포](storsimple-partner-csp-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8604-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
