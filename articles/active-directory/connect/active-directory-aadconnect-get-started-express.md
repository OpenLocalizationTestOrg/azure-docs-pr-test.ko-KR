---
title: "Azure AD Connect: 기본 설정을 사용하여 시작 | Microsoft Docs"
description: "Toodownload를 설치 하 고 Azure AD Connect에 대 한 hello 설치 마법사를 실행 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a><span data-ttu-id="b8ef2-103">기본 설정을 사용하여 Azure AD Connect 시작</span><span class="sxs-lookup"><span data-stu-id="b8ef2-103">Getting started with Azure AD Connect using express settings</span></span>
<span data-ttu-id="b8ef2-104">인증을 위한 단일 포리스트 토폴로지 및 **암호 동기화**가 있는 경우 Azure AD Connect [Express 설정](active-directory-aadconnectsync-implement-password-synchronization.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-104">Azure AD Connect **Express Settings** is used when you have a single-forest topology and [password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) for authentication.</span></span> <span data-ttu-id="b8ef2-105">**고속 설정** hello 기본 옵션이 며 가장 일반적으로 배포 된 hello 시나리오에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-105">**Express Settings** is hello default option and is used for hello most commonly deployed scenario.</span></span> <span data-ttu-id="b8ef2-106">하면 온-프레미스 디렉터리 toohello 클라우드만 몇 번의 클릭 짧은 트래버스하여 tooextend 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-106">You are only a few short clicks away tooextend your on-premises directory toohello cloud.</span></span>

<span data-ttu-id="b8ef2-107">Azure AD Connect 설치를 시작 하기 전에 있어야 너무[Azure AD Connect 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771) 및 전체 hello 필수 단계를 [Azure AD Connect: 하드웨어 및 필수 구성 요소](active-directory-aadconnect-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-107">Before you start installing Azure AD Connect, make sure too[download Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) and complete hello pre-requisite steps in [Azure AD Connect: Hardware and prerequisites](active-directory-aadconnect-prerequisites.md).</span></span>

<span data-ttu-id="b8ef2-108">Express 설정이 토폴로지와 일치하지 않는 경우 다른 시나리오는 [관련 설명서](#related-documentation) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-108">If express settings does not match your topology, see [related documentation](#related-documentation) for other scenarios.</span></span>

## <a name="express-installation-of-azure-ad-connect"></a><span data-ttu-id="b8ef2-109">Azure AD Connect의 빠른 설치</span><span class="sxs-lookup"><span data-stu-id="b8ef2-109">Express installation of Azure AD Connect</span></span>
<span data-ttu-id="b8ef2-110">Hello에 대 한 작업에서 다음이 단계를 확인할 수 있습니다 [비디오](#videos) 섹션.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-110">You can see these steps in action in hello [videos](#videos) section.</span></span>

1. <span data-ttu-id="b8ef2-111">Azure AD Connect tooinstall에 원하는 로컬 관리자 toohello 서버에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-111">Sign in as a local administrator toohello server you wish tooinstall Azure AD Connect on.</span></span> <span data-ttu-id="b8ef2-112">Hello 서버에서이 작업을 수행 해야 toobe hello 동기화 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-112">You should do this on hello server you wish toobe hello sync server.</span></span>
2. <span data-ttu-id="b8ef2-113">Tooand 두 번 클릭 탐색 **AzureADConnect.msi**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-113">Navigate tooand double-click **AzureADConnect.msi**.</span></span>
3. <span data-ttu-id="b8ef2-114">Hello 시작 화면에 hello 상자 합의 toohello 라이선스 조건을 선택 하 고 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-114">On hello Welcome screen, select hello box agreeing toohello licensing terms and click **Continue**.</span></span>  
4. <span data-ttu-id="b8ef2-115">Hello Express 설정 화면에서 클릭 **기본 설정 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-115">On hello Express settings screen, click **Use express settings**.</span></span>  
   <span data-ttu-id="b8ef2-116">![시작 tooAzure AD 연결](./media/active-directory-aadconnect-get-started-express/express.png)</span><span class="sxs-lookup"><span data-stu-id="b8ef2-116">![Welcome tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)</span></span>
5. <span data-ttu-id="b8ef2-117">Hello 연결 tooAzure AD 화면에서 Azure AD에 대 한 hello 사용자 이름 및 전역 관리자의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-117">On hello Connect tooAzure AD screen, enter hello username and password of a global administrator for your Azure AD.</span></span> <span data-ttu-id="b8ef2-118">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-118">Click **Next**.</span></span>  
   <span data-ttu-id="b8ef2-119">![TooAzure AD 연결](./media/active-directory-aadconnect-get-started-express/connectaad.png) 오류가 발생 하 고 연결에 문제가 있을 경우 다음 참조 [연결 문제를 해결](active-directory-aadconnect-troubleshoot-connectivity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-119">![Connect tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) If you receive an error and have problems with connectivity, then see [Troubleshoot connectivity problems](active-directory-aadconnect-troubleshoot-connectivity.md).</span></span>
6. <span data-ttu-id="b8ef2-120">Hello 연결 tooAD DS 화면에는 엔터프라이즈 관리자 계정에 대 한 hello 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-120">On hello Connect tooAD DS screen, enter hello username and password for an enterprise admin account.</span></span> <span data-ttu-id="b8ef2-121">Hello 도메인 부분, 즉 FABRIKAM\administrator 또는 fabrikam.com\administrator NetBios 또는 FQDN 형식으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-121">You can enter hello domain part in either NetBios or FQDN format, that is, FABRIKAM\administrator or fabrikam.com\administrator.</span></span> <span data-ttu-id="b8ef2-122">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-122">Click **Next**.</span></span>  
   <span data-ttu-id="b8ef2-123">![DS tooAD 연결](./media/active-directory-aadconnect-get-started-express/connectad.png)</span><span class="sxs-lookup"><span data-stu-id="b8ef2-123">![Connect tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)</span></span>
7. <span data-ttu-id="b8ef2-124">hello [ **Azure AD 로그인 구성** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) 페이지 완료 하지 않은 경우 표시 [도메인 확인](../active-directory-add-domain.md) hello에 [필수 구성 요소](active-directory-aadconnect-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-124">hello [**Azure AD sign-in configuration**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) page only shows if you did not complete [verify your domains](../active-directory-add-domain.md) in hello [prerequisites](active-directory-aadconnect-prerequisites.md).</span></span>
   <span data-ttu-id="b8ef2-125">![확인되지 않은 도메인](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)</span><span class="sxs-lookup"><span data-stu-id="b8ef2-125">![Unverified domains](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)</span></span>  
   <span data-ttu-id="b8ef2-126">이 페이지를 표시하는 경우 **추가되지 않음** 및 **확인되지 않음**으로 표시된 모든 도메인을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-126">If you see this page, then review every domain marked **Not Added** and **Not Verified**.</span></span> <span data-ttu-id="b8ef2-127">사용한 해당 도메인을 Azure AD에서 확인하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-127">Make sure those domains you use have been verified in Azure AD.</span></span> <span data-ttu-id="b8ef2-128">도메인을 확인 한 경우 hello 새로 고침 기호를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-128">Click hello Refresh symbol when you have verified your domains.</span></span>
8. <span data-ttu-id="b8ef2-129">Hello 준비 tooconfigure 화면 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-129">On hello Ready tooconfigure screen, click **Install**.</span></span>
   * <span data-ttu-id="b8ef2-130">필요에 따라 hello 준비 tooconfigure 페이지에서 선택 취소할 수 있습니다 hello **구성이 완료 되는 즉시 hello 동기화 프로세스를 시작** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-130">Optionally on hello Ready tooconfigure page, you can unselect hello **Start hello synchronization process as soon as configuration completes** checkbox.</span></span> <span data-ttu-id="b8ef2-131">와 같은 toodo의 추가 구성을 사용 하려는 경우이 확인란 선택을 취소 해야 [필터링](active-directory-aadconnectsync-configure-filtering.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-131">You should unselect this checkbox if you want toodo additional configuration, such as [filtering](active-directory-aadconnectsync-configure-filtering.md).</span></span> <span data-ttu-id="b8ef2-132">이 옵션의 선택을 취소 하면 hello 마법사 동기화 구성 되지만 hello 스케줄러를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-132">If you unselect this option, hello wizard configures sync but leaves hello scheduler disabled.</span></span> <span data-ttu-id="b8ef2-133">수동으로 설정할 때까지 실행 되지 않습니다 [hello 설치 마법사를 다시 실행](active-directory-aadconnectsync-installation-wizard.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-133">It does not run until you enable it manually by [rerunning hello installation wizard](active-directory-aadconnectsync-installation-wizard.md).</span></span>
   * <span data-ttu-id="b8ef2-134">Exchange 온-프레미스 Active Directory에 있는 경우 옵션 tooenable 있습니다 [ **Exchange 하이브리드 배포**](https://technet.microsoft.com/library/jj200581.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-134">If you have Exchange in your on-premises Active Directory, then you also have an option tooenable [**Exchange Hybrid deployment**](https://technet.microsoft.com/library/jj200581.aspx).</span></span> <span data-ttu-id="b8ef2-135">계획 toohave Exchange 사서함 모두 hello 클라우드 및 온-프레미스 hello에 동일 하는 경우이 옵션을 사용 하도록 설정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-135">Enable this option if you plan toohave Exchange mailboxes both in hello cloud and on-premises at hello same time.</span></span>
     <span data-ttu-id="b8ef2-136">![Azure AD Connect tooconfigure 준비 됨](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="b8ef2-136">![Ready tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)</span></span>
9. <span data-ttu-id="b8ef2-137">Hello 설치가 완료 되 면 클릭 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-137">When hello installation completes, click **Exit**.</span></span>
10. <span data-ttu-id="b8ef2-138">Hello 설치가 완료 된 후 로그 오프 하 고 동기화 서비스 관리자 또는 동기화 규칙 편집기를 사용 하기 전에 다시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-138">After hello installation has completed, sign off and sign in again before you use Synchronization Service Manager or Synchronization Rule Editor.</span></span>

## <a name="videos"></a><span data-ttu-id="b8ef2-139">비디오</span><span class="sxs-lookup"><span data-stu-id="b8ef2-139">Videos</span></span>
<span data-ttu-id="b8ef2-140">Hello 빠른 설치를 사용 하 여 관련 한 비디오를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-140">For a video on using hello express installation, see:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b8ef2-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8ef2-141">Next steps</span></span>
<span data-ttu-id="b8ef2-142">Azure AD Connect를 설치 했으므로 다음을 할 수 있습니다 [hello 설치 되었는지 확인 하 고 라이선스를 할당](active-directory-aadconnect-whats-next.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-142">Now that you have Azure AD Connect installed you can [verify hello installation and assign licenses](active-directory-aadconnect-whats-next.md).</span></span>

<span data-ttu-id="b8ef2-143">Hello 설치를 사용 하도록 설정 된 이러한 기능에 대 한 자세한 정보: [자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md), [실수로 삭제 금지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), 및 [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-143">Learn more about these features, which were enabled with hello installation: [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md), [Prevent accidental deletes](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), and [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).</span></span>

<span data-ttu-id="b8ef2-144">이러한 공통 항목에 대 한 자세한 정보: [스케줄러와 tootrigger 동기화 방법을](active-directory-aadconnectsync-feature-scheduler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-144">Learn more about these common topics: [scheduler and how tootrigger sync](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

<span data-ttu-id="b8ef2-145">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8ef2-145">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="related-documentation"></a><span data-ttu-id="b8ef2-146">관련 설명서</span><span class="sxs-lookup"><span data-stu-id="b8ef2-146">Related documentation</span></span>
| <span data-ttu-id="b8ef2-147">항목</span><span class="sxs-lookup"><span data-stu-id="b8ef2-147">Topic</span></span> |
| --- | --- |
| <span data-ttu-id="b8ef2-148">Azure AD Connect 개요</span><span class="sxs-lookup"><span data-stu-id="b8ef2-148">Azure AD Connect overview</span></span> |
| <span data-ttu-id="b8ef2-149">사용자 지정된 설정을 사용하여 설치</span><span class="sxs-lookup"><span data-stu-id="b8ef2-149">Install using customized settings</span></span> |
| <span data-ttu-id="b8ef2-150">DirSync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="b8ef2-150">Upgrade from DirSync</span></span> |
| <span data-ttu-id="b8ef2-151">설치에 사용되는 계정</span><span class="sxs-lookup"><span data-stu-id="b8ef2-151">Accounts used for installation</span></span> |

