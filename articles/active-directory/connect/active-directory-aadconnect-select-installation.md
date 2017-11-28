---
title: "Azure AD Connect: 설치 유형 선택 | Microsoft Docs"
description: "이 항목에서는 Azure AD Connect에 대 한 tooselect hello 설치 toouse 입력 하는 방법"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="9689a-103">Azure AD Connect에 대 한 설치 유형을 toouse 어떤 선택</span><span class="sxs-lookup"><span data-stu-id="9689a-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="9689a-104">Azure AD Connect에서는 새 설치에 대해 기본 및 사용자 지정의 두 가지 설치 유형을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="9689a-105">이 항목 toouse 옵션을 설치 하는 동안 toodecide 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="9689a-106">Express</span><span class="sxs-lookup"><span data-stu-id="9689a-106">Express</span></span>
<span data-ttu-id="9689a-107">Express는 hello 가장 일반적인 옵션이 며 모든 새 설치의 약 90%에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="9689a-108">디자인 된 tooprovide hello 가장 일반적인 고객 시나리오에 적합 한 구성이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="9689a-109">이 옵션에서는 다음과 같이 전제합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-109">It assumes:</span></span>

- <span data-ttu-id="9689a-110">단일 Active Directory 포리스트 온-프레미스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="9689a-111">사용자에 게 엔터프라이즈 관리자 계정이 hello 설치에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="9689a-112">온-프레미스 Active Directory에 100,000개 미만의 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="9689a-113">다음 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-113">You get:</span></span>

- <span data-ttu-id="9689a-114">[암호 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 에서 single sign on에 대 한 온-프레미스 tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="9689a-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="9689a-115">[사용자, 그룹, 연락처 및 Windows 10 컴퓨터](active-directory-aadconnectsync-understanding-default-configuration.md)를 동기화하는 구성</span><span class="sxs-lookup"><span data-stu-id="9689a-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="9689a-116">모든 도메인 및 모든 OU에 포함된 적합한 모든 개체의 동기화</span><span class="sxs-lookup"><span data-stu-id="9689a-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="9689a-117">[자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md) 활성화 toomake hello 사용 가능한 최신 버전을 항상 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="9689a-118">기본을 계속 사용할 수 있는 경우의 옵션:</span><span class="sxs-lookup"><span data-stu-id="9689a-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="9689a-119">하지 않을 경우 toosynchronize 모든 Ou, Express를 사용 하 고 수 있습니다를 hello 마지막 페이지에서 선택 취소 **hello 동기화 프로세스를 시작 중...** *.</span><span class="sxs-lookup"><span data-stu-id="9689a-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="9689a-120">Hello 설치 마법사를 다시 실행 하 고 변경의 hello Ou [구성 옵션](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) 예약 된 동기화를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="9689a-121">암호 쓰기 저장 등 tooenable hello Azure AD Premium 기능 중 하나 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="9689a-122">Express tooget hello 초기 설치가 완료를 먼저 거치지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="9689a-123">Hello 설치 마법사를 다시 실행 하 고 hello 변경 [구성 옵션](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options)합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="9689a-124">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9689a-124">Custom</span></span>
<span data-ttu-id="9689a-125">사용자 지정 된 경로 hello express 보다 더 많은 옵션을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="9689a-126">Express에 대 한 이전 섹션에서 설명 하는 hello 구성을 조직에 대 한 대표 하지 않은 모든 경우에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="9689a-127">사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="9689a-127">Use when:</span></span>

- <span data-ttu-id="9689a-128">Active Directory에 액세스 tooan 엔터프라이즈 관리자 계정이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="9689a-129">둘 이상의 포리스트 했거나 toosynchronize 이후 hello에서 둘 이상의 포리스트를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="9689a-130">Hello 연결 서버와에서 연결할 수 없는 포리스트 내의 도메인 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="9689a-131">Toouse 페더레이션 또는 사용자 로그인에 대 한 통과 인증을 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="9689a-132">100, 000 개 이상의 개체에 있고 toouse 전체 SQL Server 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="9689a-133">확인할 계획 toouse 그룹 기반 필터링 및 뿐만 아니라 도메인 이나 OU 기반 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="9689a-134">DirSync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9689a-134">Upgrade from DirSync</span></span>
<span data-ttu-id="9689a-135">현재 디렉터리 동기화를 사용 하는 경우 다음에서 다음과 같이 hello [DirSync에서 업그레이드](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade 기존 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="9689a-136">업그레이드 옵션에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="9689a-137">동일한 hello의 현재 위치 업그레이드 tooinstall 연결할 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="9689a-138">기존 DirSync 서버 hello 계속 작동 하는 동안 새 서버에 배포 tooinstall Connect와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="9689a-139">Azure AD Sync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9689a-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="9689a-140">현재 Azure AD Sync를 사용 하는 경우 hello 참고할 수 [동일한 단계](active-directory-aadconnect-upgrade-previous-version.md) 으로 하나의 연결 버전 tooa 최신에서 업그레이드 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="9689a-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="9689a-141">업그레이드 옵션에는 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="9689a-142">동일한 hello의 현재 위치 업그레이드 tooinstall 연결할 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="9689a-143">기존 Azure AD Sync 서버 hello 하는 동안 새 서버에서 마이그레이션 회전 tooinstall 연결도 계속 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="9689a-144">FIM2010 또는 MIM2016에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="9689a-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="9689a-145">사용 중인 경우 현재 Forefront Identity Manager 2010 또는 Microsoft Identity Manager 2016 hello Azure AD 커넥터 있는 유일한 옵션은 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="9689a-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="9689a-146">에 설명 된 hello 단계에 따라 [회전 마이그레이션](active-directory-aadconnect-upgrade-previous-version.md#swing-migration)합니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="9689a-147">Hello 단계에서는 Azure AD Sync의 모든 댓글을 FIM2010/MIM2016 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9689a-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9689a-148">Next steps</span></span>
<span data-ttu-id="9689a-149">Toouse hello 옵션에 따라 선택한, hello 테이블을 사용 하 여 hello로 문서 콘텐츠 toohello 왼쪽된 toofind의 자세한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9689a-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
