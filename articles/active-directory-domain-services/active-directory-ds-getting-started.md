---
title: "Azure Active Directory Domain Services: 시작 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 hello Azure 포털 (미리 보기)를 사용 하 여 사용 하도록 설정"
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
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="dfca8-103">Azure Active Directory 도메인 서비스 hello Azure 포털 (미리 보기)를 사용 하 여 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="dfca8-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="dfca8-104">이 문서에서는 tooenable Azure Active Directory 도메인 서비스 (Azure AD DS)를 사용 하 여 Azure 포털을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="dfca8-105">toolaunch hello **Azure AD 도메인을 사용 하도록 설정 서비스** 마법사, 완전 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="dfca8-106">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dfca8-107">Hello 왼쪽된 창에서 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="dfca8-108">Hello에 **새로** 블레이드, 형식 **도메인 서비스** hello 검색 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Domain Services 검색](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="dfca8-110">Tooselect 클릭 **Azure AD 도메인 서비스** 검색 제안 hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="dfca8-111">Hello에 **Azure AD 도메인 서비스** 블레이드에서 hello 클릭 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Domain Services 블레이드](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="dfca8-113">hello **Azure AD 도메인을 사용 하도록 설정 서비스** 마법사가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="dfca8-114">작업 1: 기본 설정 구성</span><span class="sxs-lookup"><span data-stu-id="dfca8-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="dfca8-115">Hello에 **기본 사항** 페이지 hello 마법사의 hello 관리 되는 도메인에 대 한 hello DNS 도메인 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="dfca8-116">Hello 리소스 그룹을 선택할 수도 있습니다 및 Azure 위치 toowhich hello에 대 한 관리 되는 도메인을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![기본 사항 구성](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="dfca8-118">Hello 선택 **DNS 도메인 이름을** 관리 되는 도메인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="dfca8-119">hello 디렉터리의 기본 도메인 이름을 hello (으로 **. onmicrosoft.com** 접미사)에 기본적으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="dfca8-120">사용자 지정 도메인 이름도 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="dfca8-121">이 예제에서는 hello 사용자 지정 도메인 이름이 *contoso100.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="dfca8-122">지정 된 도메인 이름 hello 접두사 (예를 들어 *contoso100* hello에 *contoso100.com* 도메인 이름) 15 자 이하의 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="dfca8-123">15자보다 긴 접두사로 관리되는 도메인을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="dfca8-124">선택한 관리 되는 hello에 대 한 도메인 hello 가상 네트워크에 이미 존재 하지 않는 hello DNS 도메인 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="dfca8-125">특히,</span><span class="sxs-lookup"><span data-stu-id="dfca8-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="dfca8-126">Hello 사용 하 여 도메인을 이미 있으면 hello 가상 네트워크에 동일한 DNS 도메인 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="dfca8-127">tooenable hello에 대 한 관리 되는 도메인을 계획 하는 hello 가상 네트워크와 온-프레미스 네트워크의 VPN 연결을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="dfca8-128">Hello 사용 하 여 도메인 없는 확인이 시나리오에서는 온-프레미스 네트워크에 동일한 DNS 도메인 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="dfca8-129">Hello 가상 네트워크에 해당 이름 가진 기존 클라우드 서비스를가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="dfca8-130">Hello 선택 **유형의 가상 네트워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="dfca8-131">기본적으로 hello **리소스 관리자** 가상 네트워크 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="dfca8-132">새로 만든 관리되는 도메인 모두에 이 형식의 가상 네트워크를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="dfca8-133">선택 hello Azure **구독** 를 원하는 toocreate hello에 대 한 관리 되는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="dfca8-134">선택 hello **리소스 그룹** toowhich hello에 대 한 관리 되는 도메인에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="dfca8-135">Hello 중 하나를 선택할 수 있습니다 **새로 만들기** 또는 **기존 항목 사용** 옵션 tooselect hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="dfca8-136">Azure hello 선택 **위치** 는 hello 관리 되는 도메인 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="dfca8-137">Hello에 **네트워크** 페이지 toohello 선택한 위치에 속하는 가상 네트워크의 hello 마법사를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="dfca8-138">완료 되 면 클릭 **확인** toohello에 toomove **네트워크** hello 마법사의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="dfca8-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="dfca8-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfca8-139">Next step</span></span>
[<span data-ttu-id="dfca8-140">작업 2: 네트워크 설정 구성</span><span class="sxs-lookup"><span data-stu-id="dfca8-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
