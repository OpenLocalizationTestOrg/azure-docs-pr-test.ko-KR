---
title: "Azure Active Directory Domain Services: Azure Active Directory Domain Services 활성화 | Microsoft Docs"
description: "Azure 클래식 포털을 사용하여 Azure Active Directory Domain Services 활성화"
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
ms.openlocfilehash: ed72325ca9db99405c6173eb882a92f80cd77f47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="4aea4-103">Azure 클래식 포털을 사용하여 Azure Active Directory Domain Services 활성화</span><span class="sxs-lookup"><span data-stu-id="4aea4-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="4aea4-104">작업 3: Azure Active Directory Domain Services 활성화</span><span class="sxs-lookup"><span data-stu-id="4aea4-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="4aea4-105">이 작업에서는 다음 단계를 수행하여 디렉터리에 Azure AD DS(Azure Active Directory Domain Services)를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing the following steps:</span></span>

1. <span data-ttu-id="4aea4-106">[Azure 클래식 포털](https://manage.windowsazure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-106">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4aea4-107">왼쪽 창에서 **Active Directory** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-107">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="4aea4-108">Azure AD DS를 사용하도록 설정하려는 Azure AD(Azure Active Directory) 테넌트(디렉터리)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-108">Select the Azure Active Directory (Azure AD) tenant (directory) for which you want to enable Azure AD DS.</span></span>

    ![Azure AD 디렉터리 선택](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="4aea4-110">**미리 보기 디렉터리** 페이지에서 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-110">On the **preview directory** page, click the **Configure** tab.</span></span>

    ![디렉터리의 탭 구성](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="4aea4-112">**도메인 서비스**에서 **이 디렉터리에 대해 도메인 서비스 사용** 옵션을 **예**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-112">Under **domain services**, change the **Enable domain services for this directory** option to **Yes**.</span></span>  
    <span data-ttu-id="4aea4-113">이 페이지에는 추가 Azure Active Directory Domain Services 구성 옵션도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-113">Additional Azure Active Directory Domain Services configuration options appear on the page.</span></span>

    ![Domain Services 사용](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="4aea4-115">테넌트에 대해 Azure Active Directory Domain Services를 사용하도록 설정하면 Azure AD는 사용자를 인증하는 데 필요한 Kerberos 및 NTLM 자격 증명 해시를 생성하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores the Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="4aea4-116">**도메인 서비스의 DNS 도메인 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-116">Specify the **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="4aea4-117">디렉터리의 기본 도메인 이름(**.onmicrosoft.com** 접미사가 있음)이 기본적으로 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-117">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="4aea4-118">목록에는 **도메인** 탭에서 구성한 확인된 도메인과 확인되지 않은 도메인을 모두 포함하여 Azure AD 디렉터리에 대해 구성된 도메인이 모두 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-118">The list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on the **Domains** tab.</span></span>

   * <span data-ttu-id="4aea4-119">사용자 지정 도메인 이름도 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="4aea4-120">이 예에서 사용자 지정 도메인 이름은 *contoso100.com*입니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-120">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="4aea4-121">지정한 도메인 이름의 접두사(예: *contoso100.com* 도메인 이름의 *contoso100*)는 15자 이내의 문자를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-121">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="4aea4-122">15자를 초과하는 접두사가 포함된 Azure Active Directory Domain Services 도메인은 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="4aea4-123">관리되는 도메인에서 선택한 DNS 도메인 이름은 가상 네트워크에 존재하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-123">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="4aea4-124">특히 다음과 같은 경우인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-124">Specifically, check to see whether:</span></span>

   * <span data-ttu-id="4aea4-125">이미 가상 네트워크에 동일한 DNS 도메인 이름을 가진 도메인이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="4aea4-125">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="4aea4-126">선택한 가상 네트워크에 온-프레미스 네트워크와 연결된 VPN이 있고, 온-프레미스 네트워크에 동일한 DNS 도메인 이름을 가진 도메인이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="4aea4-126">The virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="4aea4-127">가상 네트워크에 해당 이름을 가진 기존 클라우드 서비스가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="4aea4-127">You have an existing cloud service with that name on the virtual network.</span></span>
8. <span data-ttu-id="4aea4-128">Azure Active Directory Domain Services를 사용할 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-128">Select a virtual network on which you want Azure Active Directory Domain Services to be available.</span></span> <span data-ttu-id="4aea4-129">**가상 네트워크에 도메인 서비스 연결**이라는 드롭다운 목록에서 만든 가상 네트워크와 전용 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-129">Select the virtual network and dedicated subnet you created in the **Connect domain services to this virtual network** drop-down list.</span></span> <span data-ttu-id="4aea4-130">또한 다음 사항도 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-130">Also consider the following:</span></span>

   * <span data-ttu-id="4aea4-131">지정한 가상 네트워크가 Azure Active Directory Domain Services에서 지원하는 Azure 지역에 속해 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-131">Ensure that the virtual network that you have specified belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="4aea4-132">Azure Active Directory Domain Services를 사용할 수 있는 Azure 지역을 확인하려면 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4aea4-132">To ascertain the Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="4aea4-133">Azure Active Directory Domain Services를 지원하지 않는 지역에 속한 가상 네트워크는 드롭다운 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-133">Virtual networks that belong to a region where Azure Active Directory Domain Services is not supported do not show up in the drop-down list.</span></span>

   * <span data-ttu-id="4aea4-134">Azure Active Directory Domain Services에 대한 가상 네트워크 내에서 전용 서브넷을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-134">Use a dedicated subnet within the virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="4aea4-135">게이트웨이 서브넷은 선택하지 *마세요*.</span><span class="sxs-lookup"><span data-stu-id="4aea4-135">Do *not* select the gateway subnet.</span></span> <span data-ttu-id="4aea4-136">[네트워킹 고려 사항](active-directory-ds-networking.md)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="4aea4-137">마찬가지로 Azure Resource Manager를 사용하여 만든 가상 네트워크는 드롭다운 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in the drop-down list.</span></span> <span data-ttu-id="4aea4-138">Resource Manager 기반 가상 네트워크가 현재 Azure Active Directory Domain Services에서 지원되지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="4aea4-139">Azure Active Directory Domain Services를 활성화하려면 페이지 아래쪽의 작업 창에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-139">To enable Azure Active Directory Domain Services, in the task pane at the bottom of the page, click **Save**.</span></span>
    * <span data-ttu-id="4aea4-140">디렉터리에 대해 Azure Active Directory Domain Services가 활성화되어 있는 동안에는 해당 페이지에서 *보류 중* 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-140">While Azure Active Directory Domain Services is being enabled for your directory, the page displays a status of *Pending*.</span></span>

        ![Domain Services 사용 창](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="4aea4-142">Azure Active Directory Domain Services는 관리되는 도메인에 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="4aea4-143">Azure Active Directory Domain Services를 활성화하면 가상 네트워크에서 도메인 서비스를 사용할 수 있는 IP 주소가 한 번에 하나씩 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-143">After you enable Azure Active Directory Domain Services, the IP addresses at which domain services are available on the virtual network are displayed one at a time.</span></span> <span data-ttu-id="4aea4-144">서비스에서 도메인에 대한 고가용성을 활성화하는 즉시 두 번째 IP 주소가 첫 번째 IP 주소 바로 뒤에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-144">The second IP address is displayed shortly after the first, as soon the service enables high availability for your domain.</span></span> <span data-ttu-id="4aea4-145">높은 가용성이 구성되고 도메인에 활성화되면 **구성** 탭의 **도메인 서비스** 섹션에서 두 개의 IP 주소를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-145">When high availability is configured and active for your domain, you should see two IP addresses in the **domain services** section of the **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="4aea4-146">약 20-30분 후에 **구성** 페이지의 **IP 주소** 필드에는 가상 네트워크에서 도메인 서비스를 사용할 수 있는 첫 번째 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-146">After about 20 to 30 minutes, the first IP address at which domain services are available on your virtual network in the **IP address** field on the **Configure** page.</span></span>

        ![첫 번째 프로비전된 IP를 보여 주는 Domain Services 창](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="4aea4-148">도메인에 대해 고가용성이 작동하면 두 개의 IP 주소가 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-148">When high availability is operational for your domain, two IP addresses are displayed on the page.</span></span> <span data-ttu-id="4aea4-149">관리되는 도메인은 이 두 IP 주소에서 선택한 가상 네트워크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="4aea4-150">가상 네트워크에 대한 DNS 설정을 업데이트할 수 있도록 두 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-150">Note the two IP addresses so that you can update the DNS settings for your virtual network.</span></span> <span data-ttu-id="4aea4-151">이렇게 하면 가상 네트워크의 가상 컴퓨터가 도메인 가입과 같은 작업을 위해 도메인에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-151">Doing so enables virtual machines on the virtual network to connect to the domain for operations such as domain join.</span></span>

    ![프로비전된 IP를 보여 주는 Domain Services 창](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="4aea4-153">Azure AD 테넌트의 크기(사용자 또는 그룹의 수)에 따라 관리되는 도메인에 동기화하는 데 시간이 다소 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-153">Depending on the size of your Azure AD tenant (for example, the number of users or groups), synchronization to your managed domain takes a while.</span></span> <span data-ttu-id="4aea4-154">이 동기화 프로세스는 백그라운드에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-154">This synchronization process happens in the background.</span></span> <span data-ttu-id="4aea4-155">수만 개의 개체가 있는 대형 테넌트의 경우, 모든 사용자, 그룹 멤버 자격 및 자격 증명을 동기화하는 데 1-2일이 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4aea4-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials to be synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="4aea4-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4aea4-156">Next step</span></span>
[<span data-ttu-id="4aea4-157">작업 4: Azure 가상 네트워크에 대한 DNS 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="4aea4-157">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
