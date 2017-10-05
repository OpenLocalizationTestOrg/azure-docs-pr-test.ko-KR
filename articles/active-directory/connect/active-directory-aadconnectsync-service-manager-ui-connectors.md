---
title: "Azure AD Synchronization Service Manager UI의 커넥터 | Microsoft Docs"
description: "Azure AD Connect의 Synchronization Service Manager에 있는 커넥터 탭을 이해합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0fae4b1755ca95466eeffb5ce61c1c7855d7381
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="85e23-103">Auzre AD Connect Sync Service Manager에서 커넥터 사용</span><span class="sxs-lookup"><span data-stu-id="85e23-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="85e23-105">커넥터 탭은 동기화 엔진이 연결된 모든 시스템을 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="85e23-106">커넥터 작업</span><span class="sxs-lookup"><span data-stu-id="85e23-106">Connector actions</span></span>
| <span data-ttu-id="85e23-107">작업</span><span class="sxs-lookup"><span data-stu-id="85e23-107">Action</span></span> | <span data-ttu-id="85e23-108">주석</span><span class="sxs-lookup"><span data-stu-id="85e23-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="85e23-109">생성</span><span class="sxs-lookup"><span data-stu-id="85e23-109">Create</span></span> |<span data-ttu-id="85e23-110">사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="85e23-110">Do not use.</span></span> <span data-ttu-id="85e23-111">추가 AD 포리스트에 연결하려면 설치 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="85e23-112">속성</span><span class="sxs-lookup"><span data-stu-id="85e23-112">Properties</span></span> |<span data-ttu-id="85e23-113">모든 도메인 및 OU 필터링에 사용</span><span class="sxs-lookup"><span data-stu-id="85e23-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="85e23-114">삭제</span><span class="sxs-lookup"><span data-stu-id="85e23-114">Delete</span></span>](#delete) |<span data-ttu-id="85e23-115">커넥터 공간에서 데이터를 삭제하거나 포리스트에 대한 연결을 삭제하는 데 사용</span><span class="sxs-lookup"><span data-stu-id="85e23-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="85e23-116">실행 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="85e23-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="85e23-117">여기서는 도메인 필터링만 구성</span><span class="sxs-lookup"><span data-stu-id="85e23-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="85e23-118">이 작업을 사용하여 이미 구성된 실행 프로필을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="85e23-119">실행</span><span class="sxs-lookup"><span data-stu-id="85e23-119">Run</span></span> |<span data-ttu-id="85e23-120">프로필의 일회성 실행을 시작하는 데 사용</span><span class="sxs-lookup"><span data-stu-id="85e23-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="85e23-121">중지</span><span class="sxs-lookup"><span data-stu-id="85e23-121">Stop</span></span> |<span data-ttu-id="85e23-122">현재 프로필을 실행하는 커넥터 중지</span><span class="sxs-lookup"><span data-stu-id="85e23-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="85e23-123">커넥터 내보내기</span><span class="sxs-lookup"><span data-stu-id="85e23-123">Export Connector</span></span> |<span data-ttu-id="85e23-124">사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="85e23-124">Do not use.</span></span> |
| <span data-ttu-id="85e23-125">커넥터 가져오기</span><span class="sxs-lookup"><span data-stu-id="85e23-125">Import Connector</span></span> |<span data-ttu-id="85e23-126">사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="85e23-126">Do not use.</span></span> |
| <span data-ttu-id="85e23-127">커넥터 업데이트</span><span class="sxs-lookup"><span data-stu-id="85e23-127">Update Connector</span></span> |<span data-ttu-id="85e23-128">사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="85e23-128">Do not use.</span></span> |
| <span data-ttu-id="85e23-129">스키마 새로 고침</span><span class="sxs-lookup"><span data-stu-id="85e23-129">Refresh Schema</span></span> |<span data-ttu-id="85e23-130">캐시된 스키마를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-130">Refreshes the cached schema.</span></span> <span data-ttu-id="85e23-131">동기화 규칙도 업데이트되므로 대신 설치 마법사를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="85e23-132">커넥터 공간 검색</span><span class="sxs-lookup"><span data-stu-id="85e23-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="85e23-133">개체를 찾고 [시스템 전체에서 개체 및 해당 데이터의 흐름을 따르는](#follow-an-object-and-its-data-through-the-system)데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="85e23-134">삭제</span><span class="sxs-lookup"><span data-stu-id="85e23-134">Delete</span></span>
<span data-ttu-id="85e23-135">삭제 작업은 두 가지 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-135">The delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="85e23-137">**커넥터 공간만 삭제** 옵션은 모든 데이터를 제거하지만 구성은 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="85e23-138">**커넥터 및 커넥터 공간 삭제** 옵션은 데이터와 구성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="85e23-139">이 옵션은 포리스트에 더 이상 연결하지 않으려는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="85e23-140">두 옵션 모두 모든 개체를 동기화하고 메타버스 개체를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="85e23-141">이 작업은 장기 실행 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="85e23-142">실행 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="85e23-142">Configure Run Profiles</span></span>
<span data-ttu-id="85e23-143">이 옵션을 사용하면 커넥터에 대해 구성된 실행 프로필을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="85e23-145">커넥터 공간 검색</span><span class="sxs-lookup"><span data-stu-id="85e23-145">Search Connector Space</span></span>
<span data-ttu-id="85e23-146">커넥터 공간 검색 작업은 개체를 찾아 데이터 문제를 해결하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="85e23-148">먼저 **범위**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="85e23-149">데이터(RDN, DN 앵커, 하위 트리) 또는 개체의 상태(다른 모든 옵션)에 따라 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="85e23-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="85e23-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="85e23-151">예를 들어 하위 트리 검색을 수행하는 경우 모든 개체를 하나의 OU로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="85e23-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="85e23-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="85e23-153">이 표에서 개체를 선택하고, **속성**을 선택한 다음 원본 커넥터 공간의 메타버스, 대상 커넥터 공간으로 이어지는 [흐름을 따릅니다](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md).</span><span class="sxs-lookup"><span data-stu-id="85e23-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="85e23-154">AD DS 계정 암호 변경</span><span class="sxs-lookup"><span data-stu-id="85e23-154">Changing the AD DS account password</span></span>
<span data-ttu-id="85e23-155">계정 암호를 변경하는 경우 동기화 서비스가 더 이상 온-프레미스 AD에 대한 변경 내용을 가져오거나 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="85e23-156">다음이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-156">You may see the following:</span></span>

- <span data-ttu-id="85e23-157">AD 커넥터에 대한 가져오기/내보내기 단계가 "no-start-credentials" 오류를 나타내며 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="85e23-158">Windows 이벤트 뷰어에서 응용 프로그램 이벤트 로그에는 이벤트 ID 6000 오류 및 메시지 “자격 증명이 잘못되었기 때문에 "contoso.com" 관리 에이전트를 실행하지 못했습니다.”가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="85e23-159">이 문제를 해결하려면 다음을 사용하여 AD DS 사용자 계정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="85e23-160">Synchronization Service Manager를 시작합니다(시작 → 동기화 서비스).</span><span class="sxs-lookup"><span data-stu-id="85e23-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="85e23-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="85e23-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="85e23-162">**커넥터** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="85e23-163">AD DS 계정을 사용하도록 구성된 AD 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="85e23-164">작업 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="85e23-165">팝업 대화 상자에서 Active Directory 포리스트에 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="85e23-166">포리스트 이름은 해당 온-프레미스 AD를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="85e23-167">사용자 이름은 동기화에 사용되는 AD DS 계정을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="85e23-168">암호 텍스트 상자에 AD DS 계정의 새 암호를 입력합니다. ![Azure AD Connect 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="85e23-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="85e23-169">확인을 클릭하여 새 암호를 저장하고 동기화 서비스를 다시 시작하여 메모리 캐시에서 이전 암호를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="85e23-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85e23-170">Next steps</span></span>
<span data-ttu-id="85e23-171">[Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="85e23-172">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="85e23-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
