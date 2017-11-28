---
title: "Azure AD Connect: 다음 단계와 방법을 Azure AD Connect toomanage | Microsoft Docs"
description: "Tooextend Azure AD Connect에 대 한 기본 구성 및 운영 작업을 hello 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="99522-103">다음 단계 및 방법 toomanage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="99522-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="99522-104">이 문서 toocustomize Azure Active Directory (Azure AD) Connect toomeet의 hello 운영 절차를 사용 하 여 조직의 요구 사항 및 요구 사항.</span><span class="sxs-lookup"><span data-stu-id="99522-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="99522-105">추가 동기화 관리자 추가</span><span class="sxs-lookup"><span data-stu-id="99522-105">Add additional sync admins</span></span>
<span data-ttu-id="99522-106">기본적으로 설치 및 로컬 관리자 hello가 있는 유일한 hello 사용자 수 toomanage 설치 hello 동기화 엔진은 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="99522-107">다른 사람들 toobe 수 tooaccess에 대 한 고 hello 동기화 엔진 관리 ADSyncAdmins hello 로컬 서버에서 명명 된 hello 그룹을 찾아서 toothis 그룹에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="99522-108">라이선스 tooAzure AD Premium 및 Enterprise Mobility Suite 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="99522-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="99522-109">사용자 된 했으므로 toohello 클라우드를 동기화 tooassign 해야 해당 라이선스 및 Office 365와 같은 클라우드 앱 준비 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="99522-110">Azure AD Premium 또는 Enterprise Mobility Suite 라이선스 tooassign</span><span class="sxs-lookup"><span data-stu-id="99522-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="99522-111">관리자로 Azure 포털을 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="99522-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="99522-112">Hello 왼쪽에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="99522-113">Hello에 **Active Directory** 페이지, tooset를 원하는 hello 사용자가 있는 hello 디렉터리를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="99522-114">Hello 디렉터리 페이지의 hello 위쪽 선택 **라이선스**합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="99522-115">Hello에 **라이선스** 페이지에서 **Active Directory Premium** 또는 **Enterprise Mobility Suite**, 클릭 하 고 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="99522-116">Hello 대화 상자에서 tooassign 라이선스를 누르고 원하는 다음 hello 확인 표시 아이콘이 toosave hello 변경 hello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="99522-117">Hello 예약 된 동기화 작업을 확인</span><span class="sxs-lookup"><span data-stu-id="99522-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="99522-118">Hello Azure 포털 toocheck hello 동기화 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="99522-119">tooverify hello 예약 된 동기화 작업</span><span class="sxs-lookup"><span data-stu-id="99522-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="99522-120">관리자로 Azure 포털을 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="99522-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="99522-121">Hello 왼쪽에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="99522-122">Hello에 **Active Directory** 페이지, tooset를 원하는 hello 사용자가 있는 hello 디렉터리를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="99522-123">Hello 디렉터리 페이지의 hello 위쪽 선택 **디렉터리 통합**합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="99522-124">아래 **로컬 active directory와의 통합**, 참고 hello 마지막 동기화 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="99522-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="99522-125"><center>![디렉터리 동기화 시간](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="99522-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="99522-126">예약된 동기화 작업 시작</span><span class="sxs-lookup"><span data-stu-id="99522-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="99522-127">Toorun 동기화 작업이 필요한 경우 hello Azure AD Connect 마법사를 통해 다시 실행 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99522-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="99522-128">Tooprovide Azure AD 자격 증명 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="99522-129">Hello 마법사에서 선택 hello **동기화 옵션을 사용자 지정** 작업을 마우스 클릭 **다음** hello 마법사를 통해 toomove 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="99522-130">Hello 끝에 해당 hello 확인 **hello 초기 구성이 완료 되는 즉시 hello 동기화 프로세스를 시작** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="99522-131"><center>![동기화 시작](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="99522-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="99522-132">Hello Azure AD Connect 동기화 스케줄러에 대 한 자세한 내용은 참조 하십시오. [Azure AD 연결 스케줄러](active-directory-aadconnectsync-feature-scheduler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="99522-133">Azure AD Connect에서 사용할 수 있는 추가 작업</span><span class="sxs-lookup"><span data-stu-id="99522-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="99522-134">Azure AD Connect의 사용자 초기 설치 후 항상 hello 마법사를 다시 시작할 수 hello Azure AD Connect 시작 페이지 또는 바탕 화면 바로 가기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="99522-135">Hello 마법사를 통해 다시 전환 hello 형태의 추가 작업에 몇 가지 새 옵션이 제공 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99522-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="99522-136">hello 다음 표에서 이러한 작업에 대 한 요약 및 각 작업의 간략 한 설명.</span><span class="sxs-lookup"><span data-stu-id="99522-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![추가 작업 목록](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="99522-138">추가 작업</span><span class="sxs-lookup"><span data-stu-id="99522-138">Additional task</span></span> | <span data-ttu-id="99522-139">설명</span><span class="sxs-lookup"><span data-stu-id="99522-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="99522-140">**보기 hello 선택한 시나리오**</span><span class="sxs-lookup"><span data-stu-id="99522-140">**View hello selected scenario**</span></span> |<span data-ttu-id="99522-141">현재 Azure AD Connect 솔루션을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="99522-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="99522-142">일반 설정, 동기화된 디렉토리 및 동기화 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="99522-143">**동기화 옵션 사용자 지정**</span><span class="sxs-lookup"><span data-stu-id="99522-143">**Customize synchronization options**</span></span> |<span data-ttu-id="99522-144">추가 Active Directory 포리스트 toohello 구성 추가 또는 사용자, 그룹, 장치 또는 암호 쓰기 저장과 같은 동기화 옵션 활성화와 같은 hello 현재 구성을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="99522-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="99522-145">**스테이징 모드 사용**</span><span class="sxs-lookup"><span data-stu-id="99522-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="99522-146">즉시 동기화 되지 않은 하며 있지 않은지 스테이지 정보는 tooAzure AD 또는 온-프레미스 Active Directory를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="99522-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="99522-147">이 기능을 발생 하기 전에 hello 동기화를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99522-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="99522-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99522-148">Next steps</span></span>
<span data-ttu-id="99522-149">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="99522-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
