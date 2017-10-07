---
title: "hello Azure AD 동기화 서비스 관리자 UI에서에서 aaaConnectors | Microsoft Docs"
description: "Azure AD Connect에 대 한 hello 커넥터 탭에서 hello 동기화 서비스 관리자를 이해 합니다."
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
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="87fab-103">커넥터를 사용 하 여 Azure AD Connect 동기화 서비스 관리자 hello로</span><span class="sxs-lookup"><span data-stu-id="87fab-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="87fab-105">hello 커넥터 탭을 사용 하는 toomanage 모든 시스템 hello 동기화 엔진에 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="87fab-106">커넥터 작업</span><span class="sxs-lookup"><span data-stu-id="87fab-106">Connector actions</span></span>
| <span data-ttu-id="87fab-107">작업</span><span class="sxs-lookup"><span data-stu-id="87fab-107">Action</span></span> | <span data-ttu-id="87fab-108">주석</span><span class="sxs-lookup"><span data-stu-id="87fab-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="87fab-109">생성</span><span class="sxs-lookup"><span data-stu-id="87fab-109">Create</span></span> |<span data-ttu-id="87fab-110">사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="87fab-110">Do not use.</span></span> <span data-ttu-id="87fab-111">Tooadditional AD 포리스트를 연결 하기 위한 hello 설치 마법사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="87fab-112">properties</span><span class="sxs-lookup"><span data-stu-id="87fab-112">Properties</span></span> |<span data-ttu-id="87fab-113">모든 도메인 및 OU 필터링에 사용</span><span class="sxs-lookup"><span data-stu-id="87fab-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="87fab-114">삭제</span><span class="sxs-lookup"><span data-stu-id="87fab-114">Delete</span></span>](#delete) |<span data-ttu-id="87fab-115">사용 되는 tooeither hello 커넥터 공간 또는 포리스트에서 toodelete 연결 tooa hello 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="87fab-116">실행 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="87fab-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="87fab-117">아무 것도 필터링 하는 도메인을 제외한 tooconfigure 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="87fab-118">이 작업을 사용할 수 있습니다 toosee 이미 구성 된 실행 프로필.</span><span class="sxs-lookup"><span data-stu-id="87fab-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="87fab-119">실행</span><span class="sxs-lookup"><span data-stu-id="87fab-119">Run</span></span> |<span data-ttu-id="87fab-120">Toostart 일회용 프로필의 실행을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="87fab-121">중지</span><span class="sxs-lookup"><span data-stu-id="87fab-121">Stop</span></span> |<span data-ttu-id="87fab-122">현재 프로필을 실행하는 커넥터 중지</span><span class="sxs-lookup"><span data-stu-id="87fab-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="87fab-123">커넥터 내보내기</span><span class="sxs-lookup"><span data-stu-id="87fab-123">Export Connector</span></span> |<span data-ttu-id="87fab-124">사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="87fab-124">Do not use.</span></span> |
| <span data-ttu-id="87fab-125">커넥터 가져오기</span><span class="sxs-lookup"><span data-stu-id="87fab-125">Import Connector</span></span> |<span data-ttu-id="87fab-126">사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="87fab-126">Do not use.</span></span> |
| <span data-ttu-id="87fab-127">커넥터 업데이트</span><span class="sxs-lookup"><span data-stu-id="87fab-127">Update Connector</span></span> |<span data-ttu-id="87fab-128">사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="87fab-128">Do not use.</span></span> |
| <span data-ttu-id="87fab-129">스키마 새로 고침</span><span class="sxs-lookup"><span data-stu-id="87fab-129">Refresh Schema</span></span> |<span data-ttu-id="87fab-130">Hello 캐시 된 스키마를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="87fab-131">기본 toouse hello 옵션 이므로 hello 설치 마법사에서 대신는 이후에 업데이트 동기화 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="87fab-132">커넥터 공간 검색</span><span class="sxs-lookup"><span data-stu-id="87fab-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="87fab-133">사용 되는 toofind 개체 및 너무[개체 및 hello 시스템을 통해 해당 데이터에 따라](#follow-an-object-and-its-data-through-the-system)합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="87fab-134">삭제</span><span class="sxs-lookup"><span data-stu-id="87fab-134">Delete</span></span>
<span data-ttu-id="87fab-135">hello 삭제 동작이 서로 구분에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-135">hello delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="87fab-137">옵션 hello **커넥터 공간에만 삭제** 유지 hello 구성 하지만 모든 데이터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="87fab-138">옵션 hello **커넥터를 삭제 하 고 커넥터 공간** hello 데이터와 hello 구성 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="87fab-139">이 옵션은 tooconnect tooa 포리스트를 더 이상 원하지 않는 경우 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="87fab-140">두 옵션 모두 모든 개체를 동기화 하 고 hello 메타 버스 개체를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="87fab-141">이 작업은 장기 실행 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="87fab-142">실행 프로필 구성</span><span class="sxs-lookup"><span data-stu-id="87fab-142">Configure Run Profiles</span></span>
<span data-ttu-id="87fab-143">이 옵션을 사용 toosee hello를 실행 프로필 커넥터에 대해 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="87fab-145">커넥터 공간 검색</span><span class="sxs-lookup"><span data-stu-id="87fab-145">Search Connector Space</span></span>
<span data-ttu-id="87fab-146">hello 검색 커넥터 공간 작업은 유용한 toofind 개체 및 데이터 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="87fab-148">먼저 **범위**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="87fab-149">(RDN, DN 앵커, 하위 트리)에 따라 데이터를 검색할 수 있습니다 또는 hello 개체 (다른 모든 옵션의 경우)의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="87fab-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="87fab-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="87fab-151">예를 들어 하위 트리 검색을 수행하는 경우 모든 개체를 하나의 OU로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="87fab-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="87fab-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="87fab-153">이 표에서 개체를 선택, 선택 수 **속성**, 및 [뒤](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) hello 메타 버스를 통해 hello 원본 커넥터 공간 및 toohello 대상 커넥터 공간에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="87fab-154">Hello AD DS 계정 암호 변경</span><span class="sxs-lookup"><span data-stu-id="87fab-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="87fab-155">Hello 계정 암호를 변경 하는 경우 동기화 서비스 hello 됩니다 수 tooimport/내보내기 변경 tooon 온-프레미스 AD 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="87fab-156">Hello 다음을 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-156">You may see hello following:</span></span>

- <span data-ttu-id="87fab-157">hello AD 커넥터에 대 한 hello 가져오기/내보내기 단계 "-시작-자격 증명 없음" 오류와 함께 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="87fab-158">아래의 Windows 이벤트 뷰어 hello 응용 프로그램 이벤트 로그에 이벤트 ID 6000 및 메시지와 함께 오류 "hello 자격 증명이 잘못 되었기 때문에 관리 에이전트"contoso.com"실패 toorun hello."</span><span class="sxs-lookup"><span data-stu-id="87fab-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="87fab-159">tooresolve hello 실행 hello 다음을 사용 하 여 hello AD DS 사용자 계정 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="87fab-160">Hello 동기화 서비스 관리자 (→ 시작 동기화 서비스)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="87fab-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="87fab-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="87fab-162">Toohello 이동 **커넥터** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="87fab-163">Hello 구성된 toouse hello AD DS 계정에는 AD 커넥터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="87fab-164">작업 아래에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="87fab-165">Hello 팝업 대화 상자에서 연결 tooActive Directory 포리스트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="87fab-166">hello 포리스트 이름 나타냅니다 hello 해당 온-프레미스 AD 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="87fab-167">hello 사용자 이름은 hello AD DS 계정 동기화 사용을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="87fab-168">Hello 암호 텍스트 상자에 hello hello AD DS 계정의 새 암호를 입력 ![Azure AD 연결 동기화 암호화 키 유틸리티](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="87fab-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="87fab-169">확인 toosave hello에 대 한 새 암호를 클릭 하 고 hello 동기화 서비스 tooremove hello에서에서 이전 암호 메모리 캐시를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="87fab-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87fab-170">Next steps</span></span>
<span data-ttu-id="87fab-171">Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="87fab-172">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="87fab-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
