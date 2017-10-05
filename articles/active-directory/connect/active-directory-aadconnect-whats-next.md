---
title: "Azure AD Connect: 다음 단계 및 Azure AD Connect 관리 방법 | Microsoft Docs"
description: "Azure AD Connect에 대한 기본 구성 및 운영 작업을 확장하는 방법을 알아봅니다."
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
ms.openlocfilehash: beace24fa00c85a5038a3c39ae8f76af5fd12111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="65ca6-103">다음 단계 및 Azure AD Connect 관리 방법</span><span class="sxs-lookup"><span data-stu-id="65ca6-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="65ca6-104">이 문서의 운영 절차를 사용하여 조직 요구 사항 및 요건에 부합하도록 Azure Active Directory(Azure AD) Connect를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="65ca6-105">추가 동기화 관리자 추가</span><span class="sxs-lookup"><span data-stu-id="65ca6-105">Add additional sync admins</span></span>
<span data-ttu-id="65ca6-106">기본적으로 설치를 수행한 사용자와 로컬 관리자만 설치된 동기화 엔진을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="65ca6-107">추가 사용자가 동기화 엔진에 액세스하여 관리할 수 있도록 로컬 서버에서 그룹 이름으로 ADSyncAdmins를 찾아 이 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="65ca6-108">Azure AD Premium 및 Enterprise Mobility Suite 사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="65ca6-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="65ca6-109">이제 사용자가 클라우드로 동기화되었으므로, Office 365와 같은 클라우드 앱으로 작업할 수 있도록 라이선스를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="65ca6-110">Azure AD Premium 또는 엔터프라이즈 이동성 제품군 라이선스를 할당하려면</span><span class="sxs-lookup"><span data-stu-id="65ca6-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="65ca6-111">관리자 권한으로 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="65ca6-112">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="65ca6-113">**Active Directory** 페이지에서 설정하려는 사용자가 있는 디렉토리를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="65ca6-114">디렉토리 페이지의 맨 위에서 **라이센스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="65ca6-115">**라이선스** 페이지에서 **Active Directory Premium** 또는 **Enterprise Mobility Suite**를 선택한 후 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="65ca6-116">대화 상자에서 라이선스를 할당하려는 사용자를 선택 하고 확인 표시 아이콘을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="65ca6-117">예약된 동기화 작업 확인</span><span class="sxs-lookup"><span data-stu-id="65ca6-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="65ca6-118">Azure Portal을 사용하여 동기화 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="65ca6-119">예약된 동기화 작업을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="65ca6-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="65ca6-120">관리자 권한으로 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="65ca6-121">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="65ca6-122">**Active Directory** 페이지에서 설정하려는 사용자가 있는 디렉토리를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="65ca6-123">디렉토리 페이지의 맨 위에서 **디렉토리 통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="65ca6-124">**로컬 활성 디렉토리로 통합** 아래에서 마지막 동기화 시간을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="65ca6-125"><center>![디렉터리 동기화 시간](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="65ca6-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="65ca6-126">예약된 동기화 작업 시작</span><span class="sxs-lookup"><span data-stu-id="65ca6-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="65ca6-127">동기화 작업을 실행해야하는 경우, Azure AD Connect 마법사를 다시 실행하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="65ca6-128">Azure AD 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="65ca6-129">마법사에서 **동기화 옵션 사용자 지정** 작업을 선택하고 마법사를 통해 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="65ca6-130">끝으로 **구성이 완료되자마자 동기화 프로세스를 시작**란이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="65ca6-131"><center>![동기화 시작](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="65ca6-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="65ca6-132">Azure AD Connect 동기화 스케줄러에 대한 자세한 내용은 [Azure AD Connect 스케줄러](active-directory-aadconnectsync-feature-scheduler.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65ca6-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="65ca6-133">Azure AD Connect에서 사용할 수 있는 추가 작업</span><span class="sxs-lookup"><span data-stu-id="65ca6-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="65ca6-134">Azure AD Connect의 초기 설치 후, Azure AD Connect 시작 페이지 또는 바탕 화면 바로 가기에서 항상 마법사를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="65ca6-135">마법사를 다시 실행하면 몇가지 새로운 옵션이 추가 작업의 형태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="65ca6-136">다음 테이블에서는 작업에 대한 요약과 각 작업의 간략한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![추가 작업 목록](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="65ca6-138">추가 작업</span><span class="sxs-lookup"><span data-stu-id="65ca6-138">Additional task</span></span> | <span data-ttu-id="65ca6-139">설명</span><span class="sxs-lookup"><span data-stu-id="65ca6-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="65ca6-140">**선택한 시나리오 보기**</span><span class="sxs-lookup"><span data-stu-id="65ca6-140">**View the selected scenario**</span></span> |<span data-ttu-id="65ca6-141">현재 Azure AD Connect 솔루션을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="65ca6-142">일반 설정, 동기화된 디렉토리 및 동기화 설정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="65ca6-143">**동기화 옵션 사용자 지정**</span><span class="sxs-lookup"><span data-stu-id="65ca6-143">**Customize synchronization options**</span></span> |<span data-ttu-id="65ca6-144">추가 Active Directory 포리스트를 구성에 추가 또는 사용자, 그룹, 장치나 암호 쓰기 저장과 같은 동기화 옵션 사용 등 현재 구성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="65ca6-145">**스테이징 모드 사용**</span><span class="sxs-lookup"><span data-stu-id="65ca6-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="65ca6-146">즉시 동기화되지 않거나 Azure AD 또는 온-프레미스 Active Directory로 내보내지 않은 스테이지 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="65ca6-147">이 기능을 통해 동기화가 되기 전에 동기화를 미리볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="65ca6-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65ca6-148">Next steps</span></span>
<span data-ttu-id="65ca6-149">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="65ca6-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
