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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="9c51b-103">Azure Active Directory 도메인 서비스 hello Azure 포털 (미리 보기)를 사용 하 여 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9c51b-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="9c51b-104">작업 3: 관리 그룹 구성</span><span class="sxs-lookup"><span data-stu-id="9c51b-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="9c51b-105">이 구성 작업에서는 Azure AD 디렉터리에 관리 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="9c51b-106">이 특수 관리 그룹을 *AAD DC Administrators*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="9c51b-107">이 그룹의 구성원은 관리 되는 도메인 toohello 도메인에 가입 된 컴퓨터에 대 한 관리 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="9c51b-108">도메인에 가입 된 컴퓨터에서이 그룹은 toohello 관리자 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="9c51b-109">또한이 그룹의 구성원 원격 데스크톱 tooconnect 원격으로 toodomain에 가입 된 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="9c51b-110">Azure Active Directory 도메인 서비스를 사용 하 여 만든 hello 관리 되는 도메인에 도메인 관리자 또는 엔터프라이즈 관리자 권한이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9c51b-111">관리 되는 도메인에 이러한 hello 서비스에서 예약 된 사용 권한과 hello 테 넌 트 내에서 사용할 수 있는 toousers 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="9c51b-112">그러나 만든 hello 특별 한 관리 그룹을 사용할 수 있습니다이 구성 작업 tooperform에서 일부 권한 있는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="9c51b-113">이러한 작업 컴퓨터 toohello 도메인 가입, toohello 관리 그룹 도메인에 가입 된 컴퓨터에 속하는 및 그룹 정책 구성에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="9c51b-114">hello 마법사는 자동으로 Azure AD 디렉터리의 hello 관리 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="9c51b-115">이 그룹을 'AAD DC Administrators'라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="9c51b-116">Azure AD 디렉터리에이 이름 가진 기존 그룹 했다면 hello 마법사는이 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="9c51b-117">Hello를 사용 하 여 그룹 멤버 자격을 구성할 수 있습니다 **관리자 그룹** 마법사 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="9c51b-118">tooconfigure 그룹 구성원을 클릭 하 여 **AAD DC 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![그룹 멤버 자격 구성](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="9c51b-120">Hello 클릭 **멤버 추가** tooadd 사용자가 Azure AD 디렉터리 toohello 관리자 그룹에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="9c51b-121">완료 되 면 클릭 **확인** toohello에 toomove **요약** hello 마법사의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="9c51b-122">Hello에 **요약** hello hello 관리 되는 도메인에 대 한 구성 설정 검토 hello 마법사의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="9c51b-123">돌아갈 수 있습니다 tooany 단계 hello 마법사 toomake 변경 내용이 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="9c51b-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="9c51b-124">완료 되 면 클릭 **확인** toocreate hello 새 관리 되는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![요약](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="9c51b-126">Azure AD 도메인 서비스 배포의 실행 과정과 hello 보여 주는 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="9c51b-127">Hello 알림을 클릭 toosee hello 배포에 대 한 진행률을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![알림 - 배포 진행 중](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="9c51b-129">관리되는 도메인 프로비전</span><span class="sxs-lookup"><span data-stu-id="9c51b-129">Provision your managed domain</span></span>
<span data-ttu-id="9c51b-130">관리 되는 도메인 사용자를 프로 비전의 hello 프로세스 tooan 시간을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="9c51b-131">배포 진행 중에서 상태인 동안에 '도메인 서비스' hello에서 검색할 수 있습니다 **리소스 검색** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="9c51b-132">선택 **Azure AD 도메인 서비스** hello 검색 결과에서.</span><span class="sxs-lookup"><span data-stu-id="9c51b-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="9c51b-133">hello **Azure AD 도메인 서비스** 블레이드에 프로 비전 하는 hello 관리 되는 도메인을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![프로비전되는 관리되는 도메인 찾기](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="9c51b-135">Hello 도메인에 대 한 자세한 내용은 hello 관리 되는 도메인 (예를 들어 ' contoso100.com') toosee의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - 프로비저닝 상태](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="9c51b-137">hello **개요** 해당 hello 도메인이 현재 프로비저닝되 고 탭에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="9c51b-138">완전히 프로 비전 될 때까지 hello 관리 되는 도메인을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="9c51b-139">완전히 프로 비전 하 여 관리 되는 도메인 toobe tooan 시간을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="9c51b-140">도메인 서비스-hello 상태를 프로 비전 하는 동안 개요 탭</span><span class="sxs-lookup"><span data-stu-id="9c51b-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="9c51b-141">관리 되는 도메인 hello 완전히 프로 비전 때 hello **개요** hello 도메인 상태 탭에 표시 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Domain Services - 완전히 프로비전한 후 개요 탭](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="9c51b-143">Hello에 **속성** hello 가상 네트워크에 사용할 수 있는 컨트롤러는 도메인에 두 개의 IP 주소가 표시 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c51b-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Domain Services - 완전히 프로비전한 후 속성 탭](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="9c51b-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c51b-145">Next step</span></span>
[<span data-ttu-id="9c51b-146">작업 4: hello Azure 가상 네트워크에 대 한 hello DNS 설정을 업데이트합니다</span><span class="sxs-lookup"><span data-stu-id="9c51b-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
