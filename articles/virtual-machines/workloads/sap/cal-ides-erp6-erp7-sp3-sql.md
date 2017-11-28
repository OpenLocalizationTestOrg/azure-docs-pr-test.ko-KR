---
title: "Azure에서 SAP IDES EHP7 SP3 for SAP ERP 6.0 배포 | Microsoft Docs"
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
ms.openlocfilehash: 91eed294077ff72d0760018b10c98f32db88f3be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="bdf2b-103">Azure에서 SAP IDES EHP7 SP3 for SAP ERP 6.0 배포</span><span class="sxs-lookup"><span data-stu-id="bdf2b-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="bdf2b-104">이 문서에서는 SAP CAL(SAP 클라우드 어플라이언스 라이브러리) 3.0을 통해 Azure에서 SQL Server 및 Windows OS와 함께 실행되는 SAP IDES 시스템을 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-104">This article describes how to deploy an SAP IDES system running with SQL Server and the Windows operating system on Azure via the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="bdf2b-105">스크린샷은 단계별 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-105">The screenshots show the step-by-step process.</span></span> <span data-ttu-id="bdf2b-106">다른 솔루션을 배포하려면 동일한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-106">To deploy a different solution, follow the same steps.</span></span>

<span data-ttu-id="bdf2b-107">SAP CAL을 시작하려면 [SAP 클라우드 어플라이언스 라이브러리](https://cal.sap.com/) 웹 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-107">To start with the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="bdf2b-108">SAP에는 새로운 [SAP 클라우드 어플라이언스 라이브러리 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)에 대한 블로그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-108">SAP also has a blog about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="bdf2b-109">2017년 5월 29일 기준으로 SAP CAL을 배포하는 데 덜 선호되는 클래식 배포 모델 외에도 Azure Resource Manager 배포 모델을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-109">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="bdf2b-110">새 리소스 관리자 배포 모델을 사용하고 클래식 배포 모델을 무시하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-110">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

<span data-ttu-id="bdf2b-111">클래식 모델을 사용하는 SAP CAL 계정을 이미 만든 경우 *다른 SAP CAL 계정을 만들어야 합니다*.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-111">If you already created an SAP CAL account that uses the classic model, *you need to create another SAP CAL account*.</span></span> <span data-ttu-id="bdf2b-112">이 계정은 리소스 관리자 모델을 사용하여 단독으로 Azure에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-112">This account needs to exclusively deploy into Azure by using the Resource Manager model.</span></span>

<span data-ttu-id="bdf2b-113">SAP CAL에 로그인한 후 첫 번째 페이지는 일반적으로 **솔루션** 페이지로 이동할 수 있도록 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-113">After you sign in to the SAP CAL, the first page usually leads you to the **Solutions** page.</span></span> <span data-ttu-id="bdf2b-114">SAP CAL에서 제공되는 솔루션은 계속 증가하므로 원하는 솔루션을 찾으려면 상당히 스크롤해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-114">The solutions offered on the SAP CAL are steadily increasing, so you might need to scroll quite a bit to find the solution you want.</span></span> <span data-ttu-id="bdf2b-115">Azure에서 단독으로 사용할 수 있는 강조 표시된 Windows 기반 SAP IDE 솔루션은 배포 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-115">The highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates the deployment process:</span></span>

![SAP CAL 솔루션](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="bdf2b-117">SAP CAL에서 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="bdf2b-117">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="bdf2b-118">SAP CAL에 처음으로 로그인하려면 SAP S-사용자 또는 SAP로 등록된 다른 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-118">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="bdf2b-119">그런 다음 SAP CAL에서 Azure에 어플라이언스를 배포하는 데 사용되는 SAP CAL 계정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-119">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="bdf2b-120">계정 정의에서 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-120">In the account definition, you need to:</span></span>

    <span data-ttu-id="bdf2b-121">a.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-121">a.</span></span> <span data-ttu-id="bdf2b-122">Azure에서 배포 모델을 선택합니다(리소스 관리자 또는 클래식).</span><span class="sxs-lookup"><span data-stu-id="bdf2b-122">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="bdf2b-123">b.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-123">b.</span></span> <span data-ttu-id="bdf2b-124">Azure 구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-124">Enter your Azure subscription.</span></span> <span data-ttu-id="bdf2b-125">SAP CAL 계정은 하나의 구독에만 할당될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-125">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="bdf2b-126">둘 이상의 구독이 필요한 경우 다른 SAP CAL 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-126">If you need more than one subscription, you need to create another SAP CAL account.</span></span>
    
    <span data-ttu-id="bdf2b-127">c.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-127">c.</span></span> <span data-ttu-id="bdf2b-128">Azure 구독에 배포하도록 SAP CAL 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-128">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="bdf2b-129">다음 단계에서는 리소스 관리자 배포를 위한 SAP CAL 계정을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-129">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="bdf2b-130">클래식 배포 모델에 연결된 SAP CAL 계정이 이미 있는 경우 다음 단계를 따라 새 SAP CAL 계정을 *만들어야* 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-130">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="bdf2b-131">새 SAP CAL 계정을 리소스 관리자 모델에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-131">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="bdf2b-132">새 SAP CAL 계정을 만들기 위해 **계정** 페이지는 Azure에 대한 두 가지 선택 항목을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-132">To create a new SAP CAL account, the **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="bdf2b-133">a.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-133">a.</span></span> <span data-ttu-id="bdf2b-134">**Microsoft Azure(클래식)**는 클래식 배포 모델이며 더 이상 선호하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="bdf2b-135">b.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-135">b.</span></span> <span data-ttu-id="bdf2b-136">**Microsoft Azure**는 새 리소스 관리자 배포 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    ![SAP CAL 계정](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="bdf2b-138">리소스 관리자 모델을 배포하려면 **Microsoft Azure**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-138">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL 계정](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="bdf2b-140">Azure Portal에서 찾을 수 있는 Azure **구독 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-140">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span> 

    ![SAP CAL 구독 ID](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="bdf2b-142">정의한 Azure 구독에 배포하도록 SAP CAL에 권한을 부여하려면 **권한 부여**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-142">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="bdf2b-143">다음 페이지가 브라우저 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-143">The following page appears in the browser tab:</span></span>

    ![Internet Explorer 클라우드 서비스 로그인](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="bdf2b-145">둘 이상의 사용자가 나열되는 경우 선택한 Azure 구독의 공동 관리자가 되도록 연결된 Microsoft 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-145">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="bdf2b-146">다음 페이지가 브라우저 탭에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-146">The following page appears in the browser tab:</span></span>

    ![Internet Explorer 클라우드 서비스 확인](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="bdf2b-148">**Accept**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-148">Click **Accept**.</span></span> <span data-ttu-id="bdf2b-149">권한 부여에 성공한 경우 SAP CAL 계정 정의가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-149">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="bdf2b-150">짧은 시간 후 메시지에서 권한 부여 프로세스 성공적으로 수행되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-150">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="bdf2b-151">새로 만든 SAP CAL 계정을 사용자에게 할당하려면 오른쪽의 텍스트 상자에 **사용자 ID**를 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-151">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span> 

    ![사용자 연결에 대한 계정](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="bdf2b-153">SAP CAL에 로그인하는 데 사용하는 사용자로 계정을 연결하려면 **검토**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-153">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="bdf2b-154">사용자와 새로 만든 SAP CAL 계정 간의 연결을 만들려면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-154">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

    ![계정 연결에 대한 사용자](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="bdf2b-156">다음을 할 수 있는 SAP CAL 계정을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="bdf2b-157">리소스 관리자 배포 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-157">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="bdf2b-158">Azure 구독에 SAP 시스템을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="bdf2b-159">Windows 및 SQL Server를 기반으로 SAP IDE 솔루션을 배포하려면 먼저 SAP CAL 구독에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-159">Before you can deploy the SAP IDES solution based on Windows and SQL Server, you might need to sign up for an SAP CAL subscription.</span></span> <span data-ttu-id="bdf2b-160">그렇지 않은 경우 솔루션은 개표 페이지에 **잠금**으로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-160">Otherwise, the solution might show up as **Locked** on the overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="bdf2b-161">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="bdf2b-161">Deploy a solution</span></span>
1. <span data-ttu-id="bdf2b-162">SAP CAL 계정을 설정한 후 **Windows 및 SQL Server의 SAP IDE 솔루션** 솔루션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-162">After you set up an SAP CAL account, select **The SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="bdf2b-163">**인스턴스 만들기**를 클릭하고 사용 및 약관을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-163">Click **Create Instance**, and confirm the usage and terms conditions.</span></span> 

2. <span data-ttu-id="bdf2b-164">**기본 모드: 인스턴스 만들기** 페이지에서 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-164">On the **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="bdf2b-165">a.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-165">a.</span></span> <span data-ttu-id="bdf2b-166">인스턴스 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="bdf2b-167">b.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-167">b.</span></span> <span data-ttu-id="bdf2b-168">Azure **지역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-168">Select an Azure **Region**.</span></span> <span data-ttu-id="bdf2b-169">제공된 여러 Azure 지역을 가져오려면 SAP CAL 구독이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-169">You might need an SAP CAL subscription to get multiple Azure regions offered.</span></span>

    <span data-ttu-id="bdf2b-170">c.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-170">c.</span></span>  <span data-ttu-id="bdf2b-171">표시된 것처럼 솔루션에 대한 마스터 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-171">Enter the master **Password** for the solution, as shown:</span></span>

    ![SAP CAL 기본 모드: 인스턴스 만들기](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="bdf2b-173">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-173">Click **Create**.</span></span> <span data-ttu-id="bdf2b-174">솔루션의 크기 및 복잡성에 따라 잠시 후에(SAP CAL에서 예측값 제공) 상태가 활성으로 표시되고 사용할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-174">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use:</span></span> 

    ![SAP CAL 인스턴스](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="bdf2b-176">리소스 그룹 및 SAP CAL에서 생성된 모든 해당 개체를 찾으려면 Azure Portal로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-176">To find the resource group and all its objects that were created by the SAP CAL, go to the Azure portal.</span></span> <span data-ttu-id="bdf2b-177">가상 컴퓨터가 SAP CAL에 지정된 것과 동일한 인스턴스 이름으로 시작하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-177">The virtual machine can be found starting with the same instance name that was given in the SAP CAL.</span></span>

    ![리소스 그룹 개체](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="bdf2b-179">SAP CAL 포털에서 배포된 인스턴스로 이동하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-179">On the SAP CAL portal, go to the deployed instances and click **Connect**.</span></span> <span data-ttu-id="bdf2b-180">다음과 같은 팝업 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-180">The following pop-up window appears:</span></span> 

    ![인스턴스에 연결](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="bdf2b-182">배포된 시스템에 연결하는 옵션 중 하나를 사용하려면 **시작 가이드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-182">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="bdf2b-183">설명서는 각 연결 방법에 대한 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-183">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="bdf2b-184">해당 사용자에 대한 암호는 배포 프로세스의 시작 부분에서 정의한 마스터 암호로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-184">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="bdf2b-185">설명서에서 배포된 시스템에 로그인하는 데 사용할 수 있는 암호와 함께 더 많은 기능 사용자가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-185">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span>

    ![SAP 시작 설명서](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="bdf2b-187">몇 시간 이내에 정상 SAP IDES 시스템이 Azure에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="bdf2b-188">SAP CAL 구독을 구입한 경우 SAP는 Azure에서 SAP CAL을 통해 배포를 완벽하게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-188">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="bdf2b-189">지원 큐는 BC-VCM-CAL입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf2b-189">The support queue is BC-VCM-CAL.</span></span>

