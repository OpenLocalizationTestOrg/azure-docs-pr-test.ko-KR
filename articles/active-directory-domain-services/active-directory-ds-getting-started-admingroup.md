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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="19111-103">Azure Portal을 사용하여 Azure Active Directory Domain Services 활성화(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="19111-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="19111-104">작업 3: 관리 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="19111-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="19111-105">이 구성 작업에서는 Azure AD 디렉터리에 관리 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19111-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="19111-106">이 특수 관리 그룹을 *AAD DC Administrators*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="19111-107">이 그룹의 구성원에게는 관리되는 도메인에 연결된 컴퓨터에 대한 관리자 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="19111-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="19111-108">이 그룹은 도메인 가입 컴퓨터에서 Administrators 그룹에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="19111-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="19111-109">또한 이 그룹의 구성원은 원격 데스크톱을 사용하여 도메인에 가입한 컴퓨터에 원격으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="19111-110">Azure Active Directory Domain Services를 사용하여 만든 관리되는 도메인에 도메인 관리자 또는 엔터프라이즈 관리자 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="19111-111">관리되는 도메인에서 이러한 권한은 서비스별로 예약되며 테넌트 내의 사용자가 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="19111-112">하지만, 권한 있는 작업을 수행하기 위해 이 구성 태스크를 통해 만든 특수 관리자 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="19111-113">이 작업에는 도메인에 가입한 컴퓨터에서 관리자 그룹에 속하는 도메인에 컴퓨터를 가입시키고, 그룹 정책을 구성하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="19111-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="19111-114">마법사가 자동으로 Azure AD 디렉터리에 관리 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19111-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="19111-115">이 그룹을 'AAD DC Administrators'라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="19111-116">Azure AD 디렉터리에 이 이름 가진 기존 그룹이 있는 경우 마법사는 이 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="19111-117">**관리자 그룹** 마법사 페이지를 사용하여 그룹 멤버 자격을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="19111-118">그룹 멤버 자격을 구성하려면 **AAD DC Administrators**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![그룹 멤버 자격 구성](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="19111-120">**멤버 추가** 단추를 클릭하여 Azure AD 디렉터리의 사용자를 관리자 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="19111-121">완료되면 **확인**을 클릭하여 마법사의 **요약** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="19111-122">마법사의 **요약** 페이지에서 관리되는 도메인에 대한 구성 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="19111-123">필요한 경우 마법사의 임의 단계로 돌아가서 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="19111-124">완료되면 **확인**을 클릭하여 새 관리되는 도메인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19111-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![요약](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="19111-126">Azure AD Domain Services 배포의 진행 상황을 보여 주는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19111-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="19111-127">자세한 배포 진행률을 확인하려면 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![알림 - 배포 진행 중](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="19111-129">관리되는 도메인 프로비전</span><span class="sxs-lookup"><span data-stu-id="19111-129">Provision your managed domain</span></span>
<span data-ttu-id="19111-130">관리되는 도메인을 프로비전하는 프로세스는 최대 한 시간 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="19111-131">배포가 진행되는 동안 **리소스 검색** 검색 상자에서 'Domain Services'를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="19111-132">검색 결과에서 **Azure AD Domain Services**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="19111-133">**Azure AD Domain Services** 블레이드에 프로비전되는 관리되는 도메인이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="19111-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![프로비전되는 관리되는 도메인 찾기](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="19111-135">도메인에 대한 자세한 내용을 보려면 관리되는 도메인의 이름(예: 'contoso100.com')을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19111-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - 프로비저닝 상태](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="19111-137">**개요** 탭은 도메인이 현재 프로비전되고 있음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19111-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="19111-138">완전히 프로비전될 때까지 관리되는 도메인을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="19111-139">관리되는 도메인이 완전히 프로비전되려면 최대 한 시간 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19111-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="19111-140">Domain Services - 프로비전 상태 중 개요 탭</span><span class="sxs-lookup"><span data-stu-id="19111-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="19111-141">관리되는 도메인이 완전히 프로비전되면 **개요** 탭에 도메인 상태가 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19111-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Domain Services - 완전히 프로비전한 후 개요 탭](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="19111-143">**속성** 탭에 가상 네트워크에 도메인 컨트롤러를 사용할 수 있는 두 개의 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="19111-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Domain Services - 완전히 프로비전한 후 속성 탭](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="19111-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19111-145">Next step</span></span>
[<span data-ttu-id="19111-146">작업 4: Azure 가상 네트워크에 대한 DNS 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="19111-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
