---
title: "Azure Active Directory Domain Services: 시작 | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure Active Directory Domain Services 활성화(미리 보기)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="c1561-103">Azure Portal을 사용하여 Azure Active Directory Domain Services 활성화(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="c1561-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>
<span data-ttu-id="c1561-104">이 문서에서는 Azure Portal을 사용하여 Azure AD DS(Azure Active Directory Domain Services)를 사용하도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


<span data-ttu-id="c1561-105">**Azure AD Domain Services** 마법사를 시작하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-105">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="c1561-106">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-106">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c1561-107">왼쪽 창에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-107">In the left pane, click on **New**.</span></span>
3. <span data-ttu-id="c1561-108">**새로 만들기** 블레이드의 검색 창에 **Domain Services**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-108">In the **New** blade, type **Domain Services** into the search bar.</span></span>

    ![Domain Services 검색](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="c1561-110">검색 제안 목록에서 **Azure AD Domain Services**를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-110">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="c1561-111">**Azure AD Domain Services** 블레이드에서 **만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-111">On the **Azure AD Domain Services** blade, click the **Create** button.</span></span>

    ![Domain Services 블레이드](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="c1561-113">**Azure AD Domain Services 사용** 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-113">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="c1561-114">작업 1: 기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c1561-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="c1561-115">마법사의 **기본 사항** 페이지에서 관리되는 도메인에 대한 DNS 도메인 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-115">In the **Basics** page of the wizard, you can specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="c1561-116">관리되는 도메인이 배포되어야 하는 Azure 위치 및 리소스 그룹을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-116">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![기본 사항 구성](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="c1561-118">관리되는 도메인에 대한 **DNS 도메인 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-118">Choose the **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="c1561-119">디렉터리의 기본 도메인 이름(**.onmicrosoft.com** 접미사가 있음)이 기본적으로 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-119">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="c1561-120">사용자 지정 도메인 이름도 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="c1561-121">이 예에서 사용자 지정 도메인 이름은 *contoso100.com*입니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-121">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="c1561-122">지정한 도메인 이름의 접두사(예: *contoso100.com* 도메인 이름의 *contoso100*)는 15자 이내의 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-122">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="c1561-123">15자보다 긴 접두사로 관리되는 도메인을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="c1561-124">관리되는 도메인에서 선택한 DNS 도메인 이름은 가상 네트워크에 존재하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-124">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="c1561-125">특히,</span><span class="sxs-lookup"><span data-stu-id="c1561-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="c1561-126">이미 가상 네트워크에 동일한 DNS 도메인 이름을 가진 도메인이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="c1561-126">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="c1561-127">관리되는 도메인을 사용하도록 설정할 가상 네트워크에 온-프레미스 네트워크와의 VPN 연결이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-127">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="c1561-128">이 시나리오에서는 온-프레미스 네트워크에 동일한 DNS 도메인 이름을 가진 도메인이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-128">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="c1561-129">가상 네트워크에 해당 이름을 가진 기존 클라우드 서비스가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="c1561-129">You have an existing cloud service with that name on the virtual network.</span></span>

3. <span data-ttu-id="c1561-130">**가상 네트워크의 형식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-130">Choose the **type of virtual network**.</span></span> <span data-ttu-id="c1561-131">기본적으로는 **Resource Manager** 가상 네트워크 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-131">By default, the **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="c1561-132">새로 만든 관리되는 도메인 모두에 이 형식의 가상 네트워크를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="c1561-133">관리되는 도메인을 만들려는 Azure **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-133">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

5. <span data-ttu-id="c1561-134">관리되는 도메인이 속해야 하는 **리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-134">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="c1561-135">**새로 만들기** 또는 **기존 항목 사용** 옵션을 선택하여 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-135">You can choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

6. <span data-ttu-id="c1561-136">관리되는 도메인을 만들어야 하는 Azure **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-136">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="c1561-137">마법사의 **네트워크** 페이지에는 선택한 위치에 속하는 가상 네트워크만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-137">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

7. <span data-ttu-id="c1561-138">완료되면 **확인**을 클릭하여 마법사의 **네트워크** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1561-138">When you are done, click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="c1561-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1561-139">Next step</span></span>
[<span data-ttu-id="c1561-140">작업 2: 네트워크 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c1561-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
