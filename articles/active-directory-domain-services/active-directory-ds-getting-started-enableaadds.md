---
title: "Azure Active Directory Domain Services: Azure Active Directory Domain Services 활성화 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 hello Azure 클래식 포털을 사용 하 여 사용 하도록 설정"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="d26bf-103">Azure Active Directory 도메인 서비스 hello Azure 클래식 포털을 사용 하 여 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d26bf-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="d26bf-104">작업 3: Azure Active Directory Domain Services 활성화</span><span class="sxs-lookup"><span data-stu-id="d26bf-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="d26bf-105">이 태스크에서는 단계를 수행 하는 hello를 수행 하 여 디렉터리에 대 한 Azure Active Directory 도메인 서비스 (Azure AD DS)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="d26bf-106">Toohello 이동 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d26bf-107">Hello 왼쪽된 창에서 선택 hello **Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="d26bf-108">Hello Azure Active Directory (Azure AD) 테 넌 트 (디렉터리) Azure AD DS tooenable 원하는 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Azure AD 디렉터리 선택](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="d26bf-110">Hello에 **미리 보기 디렉터리** 페이지에서 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![디렉터리의 탭 구성](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="d26bf-112">아래 **도메인 서비스**, hello 변경 **이 디렉터리에 대 한 도메인 서비스 사용** 옵션**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="d26bf-113">추가 Azure Active Directory 도메인 서비스 구성 옵션 hello 페이지에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Domain Services 사용](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="d26bf-115">테 넌 트에 대 한 Azure Active Directory 도메인 서비스를 사용 하도록 설정 하면 Azure AD를 생성 하 고 사용자를 인증에 필요한 hello Kerberos 및 NTLM 자격 증명 해시를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="d26bf-116">Hello 지정 **도메인 서비스의 DNS 도메인 이름을**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="d26bf-117">hello 디렉터리의 기본 도메인 이름을 hello (으로 **. onmicrosoft.com** 접미사) 기본적으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="d26bf-118">hello 목록에 포함 되어 Azure AD 디렉터리에 대해 구성 된 모든 도메인을 둘 다를 포함 하 여 확인 및 hello에서 구성 하는 도메인을 확인 되지 않은 **도메인** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="d26bf-119">사용자 지정 도메인 이름도 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="d26bf-120">이 예제에서는 hello 사용자 지정 도메인 이름이 *contoso100.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="d26bf-121">지정 된 도메인 이름 hello 접두사 (예를 들어 *contoso100* hello에 *contoso100.com* 도메인 이름) 15 자 이하의 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="d26bf-122">15자를 초과하는 접두사가 포함된 Azure Active Directory Domain Services 도메인은 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="d26bf-123">선택한 관리 되는 hello에 대 한 도메인 hello 가상 네트워크에 이미 존재 하지 않는 hello DNS 도메인 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="d26bf-124">특히, toosee 여부 확인:</span><span class="sxs-lookup"><span data-stu-id="d26bf-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="d26bf-125">Hello 사용 하 여 도메인을 이미 있으면 hello 가상 네트워크에 동일한 DNS 도메인 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="d26bf-126">hello 선택한 가상 네트워크에 온-프레미스 네트워크에 VPN 연결이 있게 되며 hello 사용 하 여 도메인 온-프레미스 네트워크에 동일한 DNS 도메인 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="d26bf-127">Hello 가상 네트워크에 해당 이름 가진 기존 클라우드 서비스를가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="d26bf-128">사용할 수 있는 Azure Active Directory 도메인 서비스 toobe 원하는 가상 네트워크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="d26bf-129">Hello 가상 네트워크와 전용된 서브넷 hello에서 만든 선택 **연결 도메인 toothis 가상 네트워크 서비스** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="d26bf-130">또한 hello 다음을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-130">Also consider hello following:</span></span>

   * <span data-ttu-id="d26bf-131">사용자가 지정한 해당 hello 가상 네트워크 속해 tooan Azure Active Directory 도메인 서비스에서 지원 되는 Azure 지역을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d26bf-132">tooascertain Azure Active Directory 도메인 서비스를 사용할 수 있는 Azure 지역 hello를 참조 하십시오. [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="d26bf-133">Azure Active Directory 도메인 서비스에 지원 되지 않습니다 tooa 영역에 속하는 가상 네트워크 hello 드롭 다운 목록에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="d26bf-134">Azure Active Directory 도메인 서비스에 대 한 hello 가상 네트워크 내에서 전용된 서브넷을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d26bf-135">수행 *하지* 선택 hello 게이트웨이 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="d26bf-136">[네트워킹 고려 사항](active-directory-ds-networking.md)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="d26bf-137">마찬가지로, 가상 네트워크를 Azure 리소스 관리자를 사용 하 여 만든 hello 드롭 다운 목록에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="d26bf-138">Resource Manager 기반 가상 네트워크가 현재 Azure Active Directory Domain Services에서 지원되지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="d26bf-139">hello 작업창 hello hello 페이지 맨 아래에 Azure Active Directory 도메인 서비스 tooenable 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="d26bf-140">Azure Active Directory 도메인 서비스에 대 한 디렉터리를 활성화 하는 동안 hello 페이지의 상태를 표시 하는 *보류 중인*합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Domain Services 사용 창](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="d26bf-142">Azure Active Directory Domain Services는 관리되는 도메인에 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="d26bf-143">Azure Active Directory 도메인 서비스를 활성화 한 후 서비스는 hello 가상 네트워크에서 사용할 수 있는 도메인에서 hello IP 주소는 한 번만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="d26bf-144">hello 두 번째 IP 주소가 표시 됩니다 hello 직후 먼저 곧 hello 서비스를 사용 하면 도메인에 대 한 고가용성 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="d26bf-145">고가용성 구성 된 도메인에 대 한 활성, 표시 되어야 hello에 두 개의 IP 주소 시점과 **도메인 서비스** hello 섹션 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="d26bf-146">서비스는 hello에 가상 네트워크에서 사용할 수 있는 도메인에서 hello 첫 번째 IP 주소가 약 20 too30 분 후 **IP 주소** 필드 hello에 **구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d26bf-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![첫 번째 프로비전된 IP를 보여 주는 Domain Services 창](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="d26bf-148">고가용성은 도메인에 대 한 운영, 두 개의 IP 주소 hello 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="d26bf-149">관리되는 도메인은 이 두 IP 주소에서 선택한 가상 네트워크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="d26bf-150">가상 네트워크에 대 한 hello DNS 설정을 업데이트할 수 있도록 두 개의 IP 주소 hello note 합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="d26bf-151">이렇게 하면 특정 도메인 가입 등의 작업에 대 한 hello tooconnect toohello 도메인을 가상 네트워크에 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="d26bf-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![프로비전된 IP를 보여 주는 Domain Services 창](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="d26bf-153">에 Azure AD 테 넌 트 (예를 들어 hello 수 사용자 또는 그룹)의 hello 크기에 따라 tooyour 관리 되는 컨텍스트의 동기화 도메인 약간의 시간이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="d26bf-154">이 동기화 프로세스 hello 백그라운드에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="d26bf-155">큰 테 넌 트에는 수십 개의 개체에 대 한 하루 또는 모든 사용자, 그룹 멤버 자격 및 자격 증명 toobe 동기화에 대 한 두 개의 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d26bf-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="d26bf-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d26bf-156">Next step</span></span>
[<span data-ttu-id="d26bf-157">작업 4: hello Azure 가상 네트워크에 대 한 hello DNS 설정을 업데이트합니다</span><span class="sxs-lookup"><span data-stu-id="d26bf-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
