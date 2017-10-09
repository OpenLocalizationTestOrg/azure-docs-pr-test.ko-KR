---
title: "SAP S/4HANA 또는 Azure VM에서 BW/4HANA aaaDeploy | Microsoft Docs"
description: "Azure VM에서 SAP S/4HANA 또는 BW/4HANA 배포"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="49e6a-103">Azure에서 SAP S/4HANA 또는 BW/4HANA 배포</span><span class="sxs-lookup"><span data-stu-id="49e6a-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="49e6a-104">이 문서를 사용 하 여 Azure에서 S/4HANA toodeploy SAP 클라우드 어플라이언스에 라이브러리 (SAP CAL) 3.0 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="49e6a-105">toodeploy hello를 수행 하는 다른 SAP HANA 기반 솔루션 BW/4HANA 같은 동일한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="49e6a-106">SAP CAL hello에 대 한 자세한 내용을 보려면 이동 toohello [SAP 클라우드 어플라이언스에 라이브러리](https://cal.sap.com/) 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="49e6a-107">SAP 역시 hello에 대 한 블로그 [SAP 클라우드 어플라이언스에 라이브러리 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="49e6a-108">2017 년 5 월 29의 hello Azure 리소스 관리자 배포 모델을 사용할 수 있는 클래식 배포 toohello 보다 toodeploy hello SAP CAL 모델 또한 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="49e6a-109">Hello 새 리소스 관리자 배포 모델을 사용 하 고 hello 클래식 배포 모델을 무시 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="49e6a-110">단계별 프로세스 toodeploy hello 솔루션</span><span class="sxs-lookup"><span data-stu-id="49e6a-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="49e6a-111">스크린 샷의 순서 따르면 hello를 사용 하 여 Azure에서 S/4HANA toodeploy SAP CAL hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="49e6a-112">hello 프로세스가 작동 하는 hello BW/4HANA 같은 다른 솔루션에 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="49e6a-113">hello **솔루션** 페이지 중 일부가 나와 hello CAL SAP HANA 기반 솔루션을 사용할 수 있는 Azure에서.</span><span class="sxs-lookup"><span data-stu-id="49e6a-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="49e6a-114">**SAP S/4HANA 1610 FPS01, Fully-Activated 기기** hello 중간 행에:</span><span class="sxs-lookup"><span data-stu-id="49e6a-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![SAP CAL 솔루션](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="49e6a-116">SAP CAL hello에 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="49e6a-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="49e6a-117">toosign hello에 대 한 SAP CAL toohello에 처음으로 SAP S-사용자 또는 다른 사용자가 sap 등록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="49e6a-118">Azure의 hello SAP CAL toodeploy 기기에서 사용 되는 SAP CAL 계정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="49e6a-119">Hello 계정 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="49e6a-120">a.</span><span class="sxs-lookup"><span data-stu-id="49e6a-120">a.</span></span> <span data-ttu-id="49e6a-121">(리소스 관리자 또는 클래식) Azure의 hello 배포 모델을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="49e6a-122">b.</span><span class="sxs-lookup"><span data-stu-id="49e6a-122">b.</span></span> <span data-ttu-id="49e6a-123">Azure 구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-123">Enter your Azure subscription.</span></span> <span data-ttu-id="49e6a-124">SAP CAL 계정 tooone 구독에만 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="49e6a-125">둘 이상의 구독이 필요한 경우 다른 SAP CAL 계정이 toocreate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="49e6a-126">c.</span><span class="sxs-lookup"><span data-stu-id="49e6a-126">c.</span></span> <span data-ttu-id="49e6a-127">Azure 구독에 hello SAP CAL 권한 toodeploy를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="49e6a-128">hello 다음 단계에서 SAP CAL toocreate 리소스 관리자 배포를 고려 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="49e6a-129">연결 된 toohello 클래식 배포 모델에 해당 하는 SAP CAL 계정을 이미 있는 경우 있습니다 *필요* toofollow 이러한 단계 toocreate 새 SAP CAL 계정.</span><span class="sxs-lookup"><span data-stu-id="49e6a-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="49e6a-130">새 SAP CAL 계정 hello toodeploy hello 리소스 관리자 모델에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="49e6a-131">새 SAP CAL 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="49e6a-132">hello **계정** 페이지 Azure에 대 한 세 가지 선택 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="49e6a-133">a.</span><span class="sxs-lookup"><span data-stu-id="49e6a-133">a.</span></span> <span data-ttu-id="49e6a-134">**Microsoft Azure (클래식)** hello 클래식 배포 모델 이며 더 이상 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="49e6a-135">b.</span><span class="sxs-lookup"><span data-stu-id="49e6a-135">b.</span></span> <span data-ttu-id="49e6a-136">**Microsoft Azure** 는 hello 새 리소스 관리자 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="49e6a-137">c.</span><span class="sxs-lookup"><span data-stu-id="49e6a-137">c.</span></span> <span data-ttu-id="49e6a-138">**Windows Azure 21vianet이 운영** 중국 hello 클래식 배포 모델을 사용 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="49e6a-139">hello 리소스 관리자 모델에서는 toodeploy 선택 **Microsoft Azure**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL 계정 세부 정보](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="49e6a-141">Azure hello 입력 **구독 ID** 있는 hello Azure 포털에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![SAP CAL 계정](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="49e6a-143">정의한 hello Azure 구독에 tooauthorize hello SAP CAL toodeploy, 클릭 **Authorize**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="49e6a-144">다음 페이지 hello hello 브라우저 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-144">hello following page appears in hello browser tab:</span></span>

   ![Internet Explorer 클라우드 서비스 로그인](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="49e6a-146">둘 이상의 사용자 목록에 hello Microsoft 계정으로 연결 된 toobe hello coadministrator의 hello 선택한 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="49e6a-147">다음 페이지 hello hello 브라우저 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-147">hello following page appears in hello browser tab:</span></span>

   ![Internet Explorer 클라우드 서비스 확인](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="49e6a-149">**Accept**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-149">Click **Accept**.</span></span> <span data-ttu-id="49e6a-150">Hello 권한 부여에 성공한 경우 다시 hello SAP CAL 계정 정의 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="49e6a-151">짧은 시간 후 메시지 hello 권한 부여 프로세스 성공적으로 수행 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="49e6a-152">tooassign hello 새로 만든 SAP CAL 계정 tooyour 사용자를 입력 하면 **사용자 ID** 에 텍스트 상자 오른쪽 hello에 hello 및 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![계정 toouser 연결](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="49e6a-154">tooassociate toosign toohello SAP CAL에서에서 사용 하는 hello 사용자와 계정을 클릭 **검토**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="49e6a-155">사용자 및 새로 만든 hello SAP CAL 계정 간의 toocreate hello 연결 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![사용자 tooSAP CAL 계정 연결](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="49e6a-157">다음을 할 수 있는 SAP CAL 계정을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="49e6a-158">Hello 리소스 관리자 배포 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="49e6a-159">Azure 구독에 SAP 시스템을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="49e6a-160">이제 Azure에서 사용자 구독에 S/4HANA toodeploy를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="49e6a-161">계속하기 전에 Azure H 시리즈 VM에 대한 Azure 코어 할당량이 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="49e6a-162">Hello 순간에 SAP CAL hello 사용 하 여 H 시리즈 Vm의 Azure toodeploy hello SAP HANA 기반 솔루션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="49e6a-163">Azure 구독은 H 시리즈에 대한 H 시리즈 코어 할당량이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="49e6a-164">이 경우 toocontact Azure 지원 tooget 16 H 시리즈 코어 할당량을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="49e6a-165">Azure에서 SAP CAL hello에서 솔루션을 배포할 때 Azure 지역 하나만 선택할 수 있는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="49e6a-166">SAP CAL hello에서 제안한 하나는 hello 이외의 Azure 지역에 toodeploy toopurchase SAP에서 CAL 구독 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="49e6a-167">또한 해야 tooopen SAP toohave 포함 된 메시지를 CAL 계정 설정 toodeliver hello 처음 제안 된 것 이외의 Azure 지역에 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="49e6a-168">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="49e6a-168">Deploy a solution</span></span>

<span data-ttu-id="49e6a-169">보겠습니다 hello에서 솔루션을 배포 **솔루션** hello SAP CAL의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="49e6a-170">SAP CAL hello에 두 개의 시퀀스 toodeploy가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="49e6a-171">배포 된 하나의 페이지 toodefine hello 시스템 toobe를 사용 하는 기본 순서</span><span class="sxs-lookup"><span data-stu-id="49e6a-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="49e6a-172">VM 크기에 특정 선택 사항을 제공하는 고급 시퀀스</span><span class="sxs-lookup"><span data-stu-id="49e6a-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="49e6a-173">여기에 기본 경로 toodeployment hello에 대해서도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="49e6a-174">Hello에 **계정 세부 정보** 페이지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="49e6a-175">a.</span><span class="sxs-lookup"><span data-stu-id="49e6a-175">a.</span></span> <span data-ttu-id="49e6a-176">SAP CAL 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-176">Select an SAP CAL account.</span></span> <span data-ttu-id="49e6a-177">(연결된 toodeploy hello 리소스 관리자 배포 모델에 해당 하는 계정을 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="49e6a-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="49e6a-178">b.</span><span class="sxs-lookup"><span data-stu-id="49e6a-178">b.</span></span> <span data-ttu-id="49e6a-179">인스턴스 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="49e6a-180">c.</span><span class="sxs-lookup"><span data-stu-id="49e6a-180">c.</span></span> <span data-ttu-id="49e6a-181">Azure **지역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-181">Select an Azure **Region**.</span></span> <span data-ttu-id="49e6a-182">SAP CAL hello 영역을 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="49e6a-183">다른 Azure 지역에 필요한 SAP CAL 구독이 없는 경우에 SAP와 CAL tooorder 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="49e6a-184">d.</span><span class="sxs-lookup"><span data-stu-id="49e6a-184">d.</span></span> <span data-ttu-id="49e6a-185">마스터 입력 **암호** 8 또는 9 개 문자의 hello 솔루션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="49e6a-186">hello 암호 hello 관리자 hello 다른 구성 요소에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-186">hello password is used for hello administrators of hello different components.</span></span>

   ![SAP CAL 기본 모드: 인스턴스 만들기](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="49e6a-188">클릭 **만들기**, hello 메시지 상자가 표시 되 면에서 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![SAP CAL 지원되는 VM 크기](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="49e6a-190">Hello에 **개인 키** 대화 상자를 클릭 **저장소** toostore hello hello SAP CAL의에서 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="49e6a-191">hello 개인 키에 대 한 암호 보호 toouse 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![SAP CAL 개인 키](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="49e6a-193">읽기 hello SAP CAL **경고** 클릭 하 고 메시지, **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![SAP CAL 경고](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="49e6a-195">이제 hello 배포 수행이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-195">Now hello deployment takes place.</span></span> <span data-ttu-id="49e6a-196">일정 시간이 지난 후 hello 솔루션 (hello SAP CAL 예상치를 제공)의 hello 크기와 복잡성에 따라 hello 상태가 표시 됩니다으로 활성 상태이 고 사용 하기 위해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="49e6a-197">toofind hello 가상 컴퓨터를 사용 하 여 수집한 한 리소스 그룹에 연결 된 다른 리소스 hello, Azure 포털 toohello 이동:</span><span class="sxs-lookup"><span data-stu-id="49e6a-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Hello 새 포털에 배포 된 SAP CAL 개체](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="49e6a-199">Hello SAP CAL 포털에서 hello 상태가으로 표시 **활성**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="49e6a-200">tooconnect toohello 솔루션 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="49e6a-201">다양 한 옵션 tooconnect toohello 서로 다른 구성 요소는이 솔루션 내에서 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![SAP CAL 인스턴스](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="49e6a-203">클릭 하 여 hello 옵션 tooconnect 배포 toohello 시스템 중 하나를 사용 하려면 먼저 **시작 가이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Toohello 인스턴스 연결](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="49e6a-205">hello 설명서 이름 각 hello 연결 방법에 대 한 사용자가 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="49e6a-206">해당 사용자에 대 한 hello 암호 hello 배포 프로세스의 hello 맨 앞에서 정의한 toohello 마스터 암호를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="49e6a-207">Hello 설명서에서 기능적 다른 사용자가 사용할 수 있는 암호를 함께 나열 됩니다에 toohello toosign 시스템을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="49e6a-208">예를 들어 hello Windows 원격 데스크톱 컴퓨터에 SAP GUI가 사전 설치 되어 있는 hello를 사용 하는 경우 hello S/4 시스템 다음과 같이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![Hello에 SM50 SAP GUI를 사전 설치](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="49e6a-210">또는 다음과 같은 hello 인스턴스 형식 hello DBACockpit을 사용 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="49e6a-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![Hello DBACockpit SAP GUI에 SM50](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="49e6a-212">몇 시간 이내에 정상 SAP S/4 어플라이언스가 Azure에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="49e6a-213">SAP CAL 구독을 구입한 경우, SAP Azure에서 SAP CAL hello 통해 배포를 완벽 하 게 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="49e6a-214">hello 지원 큐는 BC-VCM-CAL입니다.</span><span class="sxs-lookup"><span data-stu-id="49e6a-214">hello support queue is BC-VCM-CAL.</span></span>







