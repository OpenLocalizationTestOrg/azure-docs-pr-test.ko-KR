---
title: "Azure VM에서 SAP S/4HANA 또는 BW/4HANA 배포 | Microsoft Docs"
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
ms.openlocfilehash: 4788fa14a6c49d39b5a3096a69b6738f4a5d8cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="e4313-103">Azure에서 SAP S/4HANA 또는 BW/4HANA 배포</span><span class="sxs-lookup"><span data-stu-id="e4313-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="e4313-104">이 문서에서는 SAP CAL(SAP 클라우드 어플라이언스 라이브러리) 3.0을 통해 Azure에서 S/4HANA를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-104">This article describes how to deploy S/4HANA on Azure by using the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="e4313-105">BW/4HANA와 같은 다른 SAP HANA 기반 솔루션을 배포하려면 동일한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-105">To deploy other SAP HANA-based solutions, such as BW/4HANA, follow the same steps.</span></span>

> [!NOTE]
<span data-ttu-id="e4313-106">SAP CAL에 대한 자세한 내용은 [SAP 클라우드 어플라이언스 라이브러리](https://cal.sap.com/) 웹 사이트로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e4313-106">For more information about the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="e4313-107">SAP에는 [SAP 클라우드 어플라이언스 라이브러리 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)에 대한 블로그도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-107">SAP also has a blog about the [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="e4313-108">2017년 5월 29일 기준으로 SAP CAL을 배포하는 데 덜 선호되는 클래식 배포 모델 외에도 Azure Resource Manager 배포 모델을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-108">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="e4313-109">새 리소스 관리자 배포 모델을 사용하고 클래식 배포 모델을 무시하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-109">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

## <a name="step-by-step-process-to-deploy-the-solution"></a><span data-ttu-id="e4313-110">솔루션을 배포하는 단계별 프로세스</span><span class="sxs-lookup"><span data-stu-id="e4313-110">Step-by-step process to deploy the solution</span></span>

<span data-ttu-id="e4313-111">다음과 같은 일련의 스크린샷은 Azure에서 SAP CAL을 사용하여 S/4HANA를 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-111">The following sequence of screenshots shows you how to deploy S/4HANA on Azure by using the SAP CAL.</span></span> <span data-ttu-id="e4313-112">이 프로세스는 BW/4HANA와 같은 다른 솔루션과 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-112">The process works the same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="e4313-113">**솔루션** 페이지에서는 Azure에서 사용할 수 있는 일부 SAP CAL HANA 기반 솔루션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-113">The **Solutions** page shows some of the SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="e4313-114">**SAP S/4HANA 1610 FPS01, 완전히 활성화된 어플라이언스**는 중간 행에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in the middle row:</span></span>

![SAP CAL 솔루션](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="e4313-116">SAP CAL에서 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e4313-116">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="e4313-117">SAP CAL에 처음으로 로그인하려면 SAP S-사용자 또는 SAP로 등록된 다른 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-117">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="e4313-118">그런 다음 SAP CAL에서 Azure에 어플라이언스를 배포하는 데 사용되는 SAP CAL 계정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-118">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="e4313-119">계정 정의에서 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-119">In the account definition, you need to:</span></span>

    <span data-ttu-id="e4313-120">a.</span><span class="sxs-lookup"><span data-stu-id="e4313-120">a.</span></span> <span data-ttu-id="e4313-121">Azure에서 배포 모델을 선택합니다(리소스 관리자 또는 클래식).</span><span class="sxs-lookup"><span data-stu-id="e4313-121">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="e4313-122">b.</span><span class="sxs-lookup"><span data-stu-id="e4313-122">b.</span></span> <span data-ttu-id="e4313-123">Azure 구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-123">Enter your Azure subscription.</span></span> <span data-ttu-id="e4313-124">SAP CAL 계정은 하나의 구독에만 할당될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-124">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="e4313-125">둘 이상의 구독이 필요한 경우 다른 SAP CAL 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-125">If you need more than one subscription, you need to create another SAP CAL account.</span></span>

    <span data-ttu-id="e4313-126">c.</span><span class="sxs-lookup"><span data-stu-id="e4313-126">c.</span></span> <span data-ttu-id="e4313-127">Azure 구독에 배포하도록 SAP CAL 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-127">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="e4313-128">다음 단계에서는 리소스 관리자 배포를 위한 SAP CAL 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-128">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="e4313-129">클래식 배포 모델에 연결된 SAP CAL 계정이 이미 있는 경우 다음 단계를 따라 새 SAP CAL 계정을 *만들어야* 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-129">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="e4313-130">새 SAP CAL 계정을 리소스 관리자 모델에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-130">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="e4313-131">새 SAP CAL 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="e4313-132">**계정** 페이지는 Azure에 대한 세 가지 선택 항목을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-132">The **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="e4313-133">a.</span><span class="sxs-lookup"><span data-stu-id="e4313-133">a.</span></span> <span data-ttu-id="e4313-134">**Microsoft Azure(클래식)**는 클래식 배포 모델이며 더 이상 선호하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="e4313-135">b.</span><span class="sxs-lookup"><span data-stu-id="e4313-135">b.</span></span> <span data-ttu-id="e4313-136">**Microsoft Azure**는 새 리소스 관리자 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    <span data-ttu-id="e4313-137">c.</span><span class="sxs-lookup"><span data-stu-id="e4313-137">c.</span></span> <span data-ttu-id="e4313-138">**21Vianet에서 운영하는 Windows Azure**는 클래식 배포 모델을 사용하는 중국의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-138">**Windows Azure operated by 21Vianet** is an option in China that uses the classic deployment model.</span></span>

    <span data-ttu-id="e4313-139">리소스 관리자 모델을 배포하려면 **Microsoft Azure**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-139">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL 계정 세부 정보](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="e4313-141">Azure Portal에서 찾을 수 있는 Azure **구독 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-141">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span>

   ![SAP CAL 계정](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="e4313-143">정의한 Azure 구독에 배포하도록 SAP CAL에 권한을 부여하려면 **권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-143">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="e4313-144">다음 페이지가 브라우저 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-144">The following page appears in the browser tab:</span></span>

   ![Internet Explorer 클라우드 서비스 로그인](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="e4313-146">둘 이상의 사용자가 나열되는 경우 선택한 Azure 구독의 공동 관리자가 되도록 연결된 Microsoft 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-146">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="e4313-147">다음 페이지가 브라우저 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-147">The following page appears in the browser tab:</span></span>

   ![Internet Explorer 클라우드 서비스 확인](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="e4313-149">**Accept**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-149">Click **Accept**.</span></span> <span data-ttu-id="e4313-150">권한 부여에 성공한 경우 SAP CAL 계정 정의가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-150">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="e4313-151">짧은 시간 후 메시지에서 권한 부여 프로세스 성공적으로 수행되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-151">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="e4313-152">새로 만든 SAP CAL 계정을 사용자에게 할당하려면 오른쪽의 텍스트 상자에 **사용자 ID**를 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-152">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span>

   ![사용자 연결에 대한 계정](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="e4313-154">SAP CAL에 로그인하는 데 사용하는 사용자로 계정을 연결하려면 **검토**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-154">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="e4313-155">사용자와 새로 만든 SAP CAL 계정 간의 연결을 만들려면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-155">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

   ![SAP CAL 계정 연결에 대한 사용자](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="e4313-157">다음을 할 수 있는 SAP CAL 계정을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="e4313-158">리소스 관리자 배포 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-158">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="e4313-159">Azure 구독에 SAP 시스템을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="e4313-160">이제 Azure에서 사용자 구독에 S/4HANA 배포를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-160">Now you can start to deploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="e4313-161">계속하기 전에 Azure H 시리즈 VM에 대한 Azure 코어 할당량이 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="e4313-162">현재 SAP CAL은 Azure의 H 시리즈 VM을 사용하여 일부 SAP HANA 기반 솔루션을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-162">At the moment, the SAP CAL uses H-Series VMs of Azure to deploy some of the SAP HANA-based solutions.</span></span> <span data-ttu-id="e4313-163">Azure 구독은 H 시리즈에 대한 H 시리즈 코어 할당량이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="e4313-164">이 경우 16 H 시리즈 코어의 할당량을 가져오도록 Azure 지원에 문의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-164">If so, you might need to contact Azure support to get a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="e4313-165">SAP CAL에서 Azure에 솔루션을 배포하는 경우 Azure 지역 하나만 선택할 수 있는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-165">When you deploy a solution on Azure in the SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="e4313-166">SAP CAL에서 제안한 것과 다른 Azure 지역에 배포하려면 SAP에서 CAL 구독을 구입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-166">To deploy into Azure regions other than the one suggested by the SAP CAL, you need to purchase a CAL subscription from SAP.</span></span> <span data-ttu-id="e4313-167">또한 CAL 계정이 처음 제안된 곳 외의 Azure 지역에 제공할 수 있도록 SAP로 메시지를 열어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-167">You also might need to open a message with SAP to have your CAL account enabled to deliver into Azure regions other than the ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="e4313-168">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="e4313-168">Deploy a solution</span></span>

<span data-ttu-id="e4313-169">SAP CAL의 **솔루션** 페이지에서 솔루션을 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-169">Let's deploy a solution from the **Solutions** page of the SAP CAL.</span></span> <span data-ttu-id="e4313-170">SAP CAL에는 배포를 위한 두 개의 시퀀스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-170">The SAP CAL has two sequences to deploy:</span></span>

- <span data-ttu-id="e4313-171">배포될 시스템을 정의하도록 하나의 페이지를 사용하는 기본 시퀀스</span><span class="sxs-lookup"><span data-stu-id="e4313-171">A basic sequence that uses one page to define the system to be deployed</span></span>
- <span data-ttu-id="e4313-172">VM 크기에 특정 선택 사항을 제공하는 고급 시퀀스</span><span class="sxs-lookup"><span data-stu-id="e4313-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="e4313-173">여기에서 배포에 대한 기본 경로를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-173">We demonstrate the basic path to deployment here.</span></span>

1. <span data-ttu-id="e4313-174">**계정 세부 정보** 페이지에서 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-174">On the **Account Details** page, you need to:</span></span>

    <span data-ttu-id="e4313-175">a.</span><span class="sxs-lookup"><span data-stu-id="e4313-175">a.</span></span> <span data-ttu-id="e4313-176">SAP CAL 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-176">Select an SAP CAL account.</span></span> <span data-ttu-id="e4313-177">(리소스 관리자 배포 모델을 사용하여 배포하도록 연결된 계정을 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="e4313-177">(Use an account that is associated to deploy with the Resource Manager deployment model.)</span></span>

    <span data-ttu-id="e4313-178">b.</span><span class="sxs-lookup"><span data-stu-id="e4313-178">b.</span></span> <span data-ttu-id="e4313-179">인스턴스 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="e4313-180">c.</span><span class="sxs-lookup"><span data-stu-id="e4313-180">c.</span></span> <span data-ttu-id="e4313-181">Azure **지역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-181">Select an Azure **Region**.</span></span> <span data-ttu-id="e4313-182">SAP CAL은 지역을 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-182">The SAP CAL suggests a region.</span></span> <span data-ttu-id="e4313-183">다른 Azure 지역이 필요하고 SAP CAL 구독이 없는 경우 SAP로 CAL 구독을 주문해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-183">If you need another Azure region and you don't have an SAP CAL subscription, you need to order a CAL subscription with SAP.</span></span>

    <span data-ttu-id="e4313-184">d.</span><span class="sxs-lookup"><span data-stu-id="e4313-184">d.</span></span> <span data-ttu-id="e4313-185">8자 또는 9자로 솔루션에 대한 마스터 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-185">Enter a master **Password** for the solution of eight or nine characters.</span></span> <span data-ttu-id="e4313-186">암호는 다양한 구성 요소의 관리자에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-186">The password is used for the administrators of the different components.</span></span>

   ![SAP CAL 기본 모드: 인스턴스 만들기](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="e4313-188">**만들기**를 클릭하고 나타나는 메시지 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-188">Click **Create**, and in the message box that appears, click **OK**.</span></span>

   ![SAP CAL 지원되는 VM 크기](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="e4313-190">**개인 키** 대화 상자에서 **저장**을 클릭하여 SAP CAL에 개인 키를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-190">In the **Private Key** dialog box, click **Store** to store the private key in the SAP CAL.</span></span> <span data-ttu-id="e4313-191">개인 키에 대해 암호 보호를 사용하려면 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-191">To use password protection for the private key, click **Download**.</span></span> 

   ![SAP CAL 개인 키](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="e4313-193">SAP CAL **경고** 메시지를 읽고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-193">Read the SAP CAL **Warning** message, and click **OK**.</span></span>

   ![SAP CAL 경고](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="e4313-195">이제 배포가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-195">Now the deployment takes place.</span></span> <span data-ttu-id="e4313-196">솔루션의 크기 및 복잡성에 따라 잠시 후에(SAP CAL에서 예측값 제공) 상태가 활성으로 표시되고 사용할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-196">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="e4313-197">하나의 리소스 그룹에서 다른 연결된 리소스를 사용하여 수집된 가상 컴퓨터를 찾으려면 Azure Portal로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-197">To find the virtual machines collected with the other associated resources in one resource group, go to the Azure portal:</span></span> 

   ![새 포털에 배포된 SAP CAL 개체](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="e4313-199">SAP CAL 포털에서 상태는 **활성**으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-199">On the SAP CAL portal, the status appears as **Active**.</span></span> <span data-ttu-id="e4313-200">솔루션에 연결하려면 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-200">To connect to the solution, click **Connect**.</span></span> <span data-ttu-id="e4313-201">다양한 구성 요소에 연결하기 위한 다른 옵션이 이 솔루션 내에서 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-201">Different options to connect to the different components are deployed within this solution.</span></span>

   ![SAP CAL 인스턴스](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="e4313-203">배포된 시스템에 연결하는 옵션 중 하나를 사용하려면 **시작 가이드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-203">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> 

   ![인스턴스에 연결](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="e4313-205">설명서는 각 연결 방법에 대한 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-205">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="e4313-206">해당 사용자에 대한 암호는 배포 프로세스의 시작 부분에서 정의한 마스터 암호로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-206">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="e4313-207">설명서에서 배포된 시스템에 로그인하는 데 사용할 수 있는 암호와 함께 더 많은 기능 사용자가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-207">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span> 

    <span data-ttu-id="e4313-208">예를 들어 Windows 원격 데스크톱 컴퓨터에 미리 설치되어 있는 SAP GUI를 사용하는 경우 S/4 시스템은 다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-208">For example, if you use the SAP GUI that's preinstalled on the Windows Remote Desktop machine, the S/4 system might look like this:</span></span>

   ![사전 설치된 SAP GUI의 SM50](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="e4313-210">또는 DBACockpit을 사용하는 경우 인스턴스는 다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-210">Or if you use the DBACockpit, the instance might look like this:</span></span>

   ![DBACockpit SAP GUI의 SM50](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="e4313-212">몇 시간 이내에 정상 SAP S/4 어플라이언스가 Azure에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="e4313-213">SAP CAL 구독을 구입한 경우 SAP는 Azure에서 SAP CAL을 통해 배포를 완벽하게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-213">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="e4313-214">지원 큐는 BC-VCM-CAL입니다.</span><span class="sxs-lookup"><span data-stu-id="e4313-214">The support queue is BC-VCM-CAL.</span></span>







