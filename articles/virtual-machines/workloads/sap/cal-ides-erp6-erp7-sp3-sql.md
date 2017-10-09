---
title: "aaaDeploy Azure에서 SAP ERP 6.0에 대 한 IDE EHP7 SP3 SAP | Microsoft Docs"
description: "Azure에서 SAP IDES EHP7 SP3 for SAP ERP 6.0 배포"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="d3c14-103">Azure에서 SAP IDES EHP7 SP3 for SAP ERP 6.0 배포</span><span class="sxs-lookup"><span data-stu-id="d3c14-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="d3c14-104">이 문서에서는 설명 방법을 toodeploy는 SAP IDE 시스템 hello SAP 클라우드 어플라이언스에 라이브러리 (SAP CAL) 3.0 통해 Azure에서 SQL Server와 Windows 운영 체제 hello 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="d3c14-105">hello 스크린 샷을 hello 단계별 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="d3c14-106">toodeploy를 다른 솔루션에 따라 동일한 단계를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="d3c14-107">SAP CAL, 이동 toohello hello로 toostart [SAP 클라우드 어플라이언스에 라이브러리](https://cal.sap.com/) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="d3c14-108">SAP에 hello에 대 한 블로그 새 [SAP 클라우드 어플라이언스에 라이브러리 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="d3c14-109">2017 년 5 월 29의 hello Azure 리소스 관리자 배포 모델을 사용할 수 있는 클래식 배포 toohello 보다 toodeploy hello SAP CAL 모델 또한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="d3c14-110">Hello 새 리소스 관리자 배포 모델을 사용 하 고 hello 클래식 배포 모델을 무시 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="d3c14-111">Hello 일반 모델을 사용 하는 SAP CAL 계정을 이미 만든 경우 *다른 SAP CAL 계정 toocreate 필요한*합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="d3c14-112">이 계정에 있어야 tooexclusively hello 리소스 관리자 모델을 사용 하 여 Azure에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="d3c14-113">SAP CAL toohello 로그인 한 후 첫 번째 페이지 hello 일반적으로 안내 toohello **솔루션** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d3c14-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="d3c14-114">SAP CAL hello에 제공 하는 hello 솔루션은 계속 증가 tooscroll 원하는 toofind hello 솔루션 상당한 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="d3c14-115">Azure에서 단독으로 사용할 수 있는 강조 표시 하는 hello SAP IDE Windows 기반 솔루션 hello 배포 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![SAP CAL 솔루션](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="d3c14-117">SAP CAL hello에 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d3c14-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="d3c14-118">toosign hello에 대 한 SAP CAL toohello에 처음으로 SAP S-사용자 또는 다른 사용자가 sap 등록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="d3c14-119">Azure의 hello SAP CAL toodeploy 기기에서 사용 되는 SAP CAL 계정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="d3c14-120">Hello 계정 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="d3c14-121">a.</span><span class="sxs-lookup"><span data-stu-id="d3c14-121">a.</span></span> <span data-ttu-id="d3c14-122">(리소스 관리자 또는 클래식) Azure의 hello 배포 모델을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="d3c14-123">b.</span><span class="sxs-lookup"><span data-stu-id="d3c14-123">b.</span></span> <span data-ttu-id="d3c14-124">Azure 구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-124">Enter your Azure subscription.</span></span> <span data-ttu-id="d3c14-125">SAP CAL 계정 tooone 구독에만 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="d3c14-126">둘 이상의 구독이 필요한 경우 다른 SAP CAL 계정이 toocreate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="d3c14-127">c.</span><span class="sxs-lookup"><span data-stu-id="d3c14-127">c.</span></span> <span data-ttu-id="d3c14-128">Azure 구독에 hello SAP CAL 권한 toodeploy를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="d3c14-129">hello 다음 단계에서 SAP CAL toocreate 리소스 관리자 배포를 고려 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="d3c14-130">연결 된 toohello 클래식 배포 모델에 해당 하는 SAP CAL 계정을 이미 있는 경우 있습니다 *필요* toofollow 이러한 단계 toocreate 새 SAP CAL 계정.</span><span class="sxs-lookup"><span data-stu-id="d3c14-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="d3c14-131">새 SAP CAL 계정 hello toodeploy hello 리소스 관리자 모델에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="d3c14-132">toocreate 새 SAP CAL 계정, hello **계정** 페이지 Azure에 대 한 두 가지 선택 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="d3c14-133">a.</span><span class="sxs-lookup"><span data-stu-id="d3c14-133">a.</span></span> <span data-ttu-id="d3c14-134">**Microsoft Azure (클래식)** hello 클래식 배포 모델 이며 더 이상 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="d3c14-135">b.</span><span class="sxs-lookup"><span data-stu-id="d3c14-135">b.</span></span> <span data-ttu-id="d3c14-136">**Microsoft Azure** 는 hello 새 리소스 관리자 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![SAP CAL 계정](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="d3c14-138">hello 리소스 관리자 모델에서는 toodeploy 선택 **Microsoft Azure**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL 계정](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="d3c14-140">Azure hello 입력 **구독 ID** 있는 hello Azure 포털에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![SAP CAL 구독 ID](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="d3c14-142">정의한 hello Azure 구독에 tooauthorize hello SAP CAL toodeploy, 클릭 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="d3c14-143">다음 페이지 hello hello 브라우저 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-143">hello following page appears in hello browser tab:</span></span>

    ![Internet Explorer 클라우드 서비스 로그인](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="d3c14-145">둘 이상의 사용자 목록에 hello Microsoft 계정으로 연결 된 toobe hello coadministrator의 hello 선택한 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="d3c14-146">다음 페이지 hello hello 브라우저 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-146">hello following page appears in hello browser tab:</span></span>

    ![Internet Explorer 클라우드 서비스 확인](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="d3c14-148">**Accept**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-148">Click **Accept**.</span></span> <span data-ttu-id="d3c14-149">Hello 권한 부여에 성공한 경우 다시 hello SAP CAL 계정 정의 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="d3c14-150">짧은 시간 후 메시지 hello 권한 부여 프로세스 성공적으로 수행 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="d3c14-151">tooassign hello 새로 만든 SAP CAL 계정 tooyour 사용자를 입력 하면 **사용자 ID** 에 텍스트 상자 오른쪽 hello에 hello 및 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![계정 toouser 연결](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="d3c14-153">tooassociate toosign toohello SAP CAL에서에서 사용 하는 hello 사용자와 계정을 클릭 **검토**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="d3c14-154">사용자 및 새로 만든 hello SAP CAL 계정 간의 toocreate hello 연결 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![사용자 tooaccount 연결](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="d3c14-156">다음을 할 수 있는 SAP CAL 계정을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="d3c14-157">Hello 리소스 관리자 배포 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="d3c14-158">Azure 구독에 SAP 시스템을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="d3c14-159">Windows 및 SQL Server를 기반으로 하는 hello SAP IDE 솔루션을 배포 하려면 먼저 toosign SAP CAL 구독 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="d3c14-160">그렇지 않으면 hello 솔루션 수로 표시 **잠금** hello 개요 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="d3c14-161">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="d3c14-161">Deploy a solution</span></span>
1. <span data-ttu-id="d3c14-162">SAP CAL 계정을 설정한 후 선택 **Windows 및 SQL Server에서 SAP IDE 솔루션 hello** 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="d3c14-163">클릭 **인스턴스 만들기**, hello 사용 현황 및 용어 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="d3c14-164">Hello에 **기본 모드: 인스턴스 만들기** 페이지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="d3c14-165">a.</span><span class="sxs-lookup"><span data-stu-id="d3c14-165">a.</span></span> <span data-ttu-id="d3c14-166">인스턴스 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="d3c14-167">b.</span><span class="sxs-lookup"><span data-stu-id="d3c14-167">b.</span></span> <span data-ttu-id="d3c14-168">Azure **지역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-168">Select an Azure **Region**.</span></span> <span data-ttu-id="d3c14-169">여러 Azure 지역에서 제공 되는 SAP CAL 구독 tooget을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="d3c14-170">c.</span><span class="sxs-lookup"><span data-stu-id="d3c14-170">c.</span></span>  <span data-ttu-id="d3c14-171">Hello 마스터 입력 **암호** hello 솔루션에서는 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="d3c14-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![SAP CAL 기본 모드: 인스턴스 만들기](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="d3c14-173">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-173">Click **Create**.</span></span> <span data-ttu-id="d3c14-174">일정 시간이 지난 후 hello 솔루션 (hello SAP CAL 예상치를 제공)의 hello 크기와 복잡성에 따라 hello 상태는 표시으로 활성 상태이 고 사용 하기 위해 준비:</span><span class="sxs-lookup"><span data-stu-id="d3c14-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![SAP CAL 인스턴스](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="d3c14-176">SAP CAL hello toofind hello 리소스 그룹 및 모든 해당 개체에서 생성 된 toohello Azure 포털을 이동 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d3c14-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="d3c14-177">동일한 인스턴스 이름을 SAP CAL hello에 제공 된 hello로 시작 hello 가상 컴퓨터를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![리소스 그룹 개체](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="d3c14-179">Hello SAP CAL 포털에 배포 된 toohello 인스턴스 이동를 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="d3c14-180">hello 다음 팝업 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-180">hello following pop-up window appears:</span></span> 

    ![Toohello 인스턴스 연결](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="d3c14-182">클릭 하 여 hello 옵션 tooconnect 배포 toohello 시스템 중 하나를 사용 하려면 먼저 **시작 가이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="d3c14-183">hello 설명서 이름 각 hello 연결 방법에 대 한 사용자가 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="d3c14-184">해당 사용자에 대 한 hello 암호 hello 배포 프로세스의 hello 맨 앞에서 정의한 toohello 마스터 암호를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="d3c14-185">Hello 설명서에서 기능적 다른 사용자가 사용할 수 있는 암호를 함께 나열 됩니다에 toohello toosign 시스템을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![SAP 시작 설명서](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="d3c14-187">몇 시간 이내에 정상 SAP IDES 시스템이 Azure에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="d3c14-188">SAP CAL 구독을 구입한 경우, SAP Azure에서 SAP CAL hello 통해 배포를 완벽 하 게 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="d3c14-189">hello 지원 큐는 BC-VCM-CAL입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c14-189">hello support queue is BC-VCM-CAL.</span></span>

