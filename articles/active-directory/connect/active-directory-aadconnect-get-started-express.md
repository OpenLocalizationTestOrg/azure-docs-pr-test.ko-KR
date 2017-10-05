---
title: "Azure AD Connect: 기본 설정을 사용하여 시작 | Microsoft Docs"
description: "Azure AD Connect용 설치 마법사를 다운로드, 설치 및 실행하는 방법을 알아봅니다."
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
ms.openlocfilehash: 8a08f6e441a856a06bf7870747ca20af45a0364e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a><span data-ttu-id="689b8-103">기본 설정을 사용하여 Azure AD Connect 시작</span><span class="sxs-lookup"><span data-stu-id="689b8-103">Getting started with Azure AD Connect using express settings</span></span>
<span data-ttu-id="689b8-104">인증을 위한 단일 포리스트 토폴로지 및 **암호 동기화**가 있는 경우 Azure AD Connect [Express 설정](active-directory-aadconnectsync-implement-password-synchronization.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-104">Azure AD Connect **Express Settings** is used when you have a single-forest topology and [password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) for authentication.</span></span> <span data-ttu-id="689b8-105">**Express 설정** 은 기본 옵션이며 가장 일반적으로 배포된 시나리오에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-105">**Express Settings** is the default option and is used for the most commonly deployed scenario.</span></span> <span data-ttu-id="689b8-106">몇 번의 클릭만으로 온-프레미스 디렉터리를 클라우드로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-106">You are only a few short clicks away to extend your on-premises directory to the cloud.</span></span>

<span data-ttu-id="689b8-107">Azure AD Connect 설치를 시작하기 전에 [Azure AD Connect를 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771)하고 [Azure AD Connect: 하드웨어 및 필수 구성 요소](active-directory-aadconnect-prerequisites.md)의 필수 구성 요소 단계를 완료하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-107">Before you start installing Azure AD Connect, make sure to [download Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) and complete the pre-requisite steps in [Azure AD Connect: Hardware and prerequisites](active-directory-aadconnect-prerequisites.md).</span></span>

<span data-ttu-id="689b8-108">Express 설정이 토폴로지와 일치하지 않는 경우 다른 시나리오는 [관련 설명서](#related-documentation) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="689b8-108">If express settings does not match your topology, see [related documentation](#related-documentation) for other scenarios.</span></span>

## <a name="express-installation-of-azure-ad-connect"></a><span data-ttu-id="689b8-109">Azure AD Connect의 빠른 설치</span><span class="sxs-lookup"><span data-stu-id="689b8-109">Express installation of Azure AD Connect</span></span>
<span data-ttu-id="689b8-110">[비디오](#videos) 섹션에서 실행 중인 다음 단계를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-110">You can see these steps in action in the [videos](#videos) section.</span></span>

1. <span data-ttu-id="689b8-111">Azure AD Connect를 설치하려는 서버에 로컬 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-111">Sign in as a local administrator to the server you wish to install Azure AD Connect on.</span></span> <span data-ttu-id="689b8-112">동기화 서버로 설정할 서버에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-112">You should do this on the server you wish to be the sync server.</span></span>
2. <span data-ttu-id="689b8-113">**AzureADConnect.msi**를 찾아서 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-113">Navigate to and double-click **AzureADConnect.msi**.</span></span>
3. <span data-ttu-id="689b8-114">시작 화면에서 사용권 계약에 동의하는 상자를 선택하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-114">On the Welcome screen, select the box agreeing to the licensing terms and click **Continue**.</span></span>  
4. <span data-ttu-id="689b8-115">기본 설정 화면에서 **Use express settings**(기본 설정 사용)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-115">On the Express settings screen, click **Use express settings**.</span></span>  
   <span data-ttu-id="689b8-116">![Azure AD Connect 시작](./media/active-directory-aadconnect-get-started-express/express.png)</span><span class="sxs-lookup"><span data-stu-id="689b8-116">![Welcome to Azure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)</span></span>
5. <span data-ttu-id="689b8-117">Azure AD에 연결 화면에서 Azure AD에 대한 전역 관리자의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-117">On the Connect to Azure AD screen, enter the username and password of a global administrator for your Azure AD.</span></span> <span data-ttu-id="689b8-118">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-118">Click **Next**.</span></span>  
   <span data-ttu-id="689b8-119">![Azure AD에 연결](./media/active-directory-aadconnect-get-started-express/connectaad.png) 오류가 발생하고 연결에 문제가 있는 경우 [연결 문제 해결](active-directory-aadconnect-troubleshoot-connectivity.md)의 필수 구성 요소 단계를 완료하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-119">![Connect to Azure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) If you receive an error and have problems with connectivity, then see [Troubleshoot connectivity problems](active-directory-aadconnect-troubleshoot-connectivity.md).</span></span>
6. <span data-ttu-id="689b8-120">AD DS에 연결 화면에서 엔터프라이즈 관리자 계정의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-120">On the Connect to AD DS screen, enter the username and password for an enterprise admin account.</span></span> <span data-ttu-id="689b8-121">NetBios 또는 FQDN 형식으로 도메인 부분을 입력할 수 있습니다(예: FABRIKAM\administrator 또는 fabrikam.com\administrator).</span><span class="sxs-lookup"><span data-stu-id="689b8-121">You can enter the domain part in either NetBios or FQDN format, that is, FABRIKAM\administrator or fabrikam.com\administrator.</span></span> <span data-ttu-id="689b8-122">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-122">Click **Next**.</span></span>  
   <span data-ttu-id="689b8-123">![AD DS에 연결](./media/active-directory-aadconnect-get-started-express/connectad.png)</span><span class="sxs-lookup"><span data-stu-id="689b8-123">![Connect to AD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)</span></span>
7. <span data-ttu-id="689b8-124">[필수 구성 요소](active-directory-aadconnect-prerequisites.md)에서 [도메인 확인](../active-directory-add-domain.md)을 완료하지 않은 경우 [**Azure AD 로그인 구성**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-124">The [**Azure AD sign-in configuration**](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) page only shows if you did not complete [verify your domains](../active-directory-add-domain.md) in the [prerequisites](active-directory-aadconnect-prerequisites.md).</span></span>
   <span data-ttu-id="689b8-125">![확인되지 않은 도메인](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)</span><span class="sxs-lookup"><span data-stu-id="689b8-125">![Unverified domains](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)</span></span>  
   <span data-ttu-id="689b8-126">이 페이지를 표시하는 경우 **추가되지 않음** 및 **확인되지 않음**으로 표시된 모든 도메인을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-126">If you see this page, then review every domain marked **Not Added** and **Not Verified**.</span></span> <span data-ttu-id="689b8-127">사용한 해당 도메인을 Azure AD에서 확인하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-127">Make sure those domains you use have been verified in Azure AD.</span></span> <span data-ttu-id="689b8-128">도메인을 확인한 경우 새로 고침 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-128">Click the Refresh symbol when you have verified your domains.</span></span>
8. <span data-ttu-id="689b8-129">구성 준비 화면에서 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-129">On the Ready to configure screen, click **Install**.</span></span>
   * <span data-ttu-id="689b8-130">선택적으로 구성 준비 완료 페이지에서 **구성이 완료되자마자 동기화 프로세스를 시작합니다.** 확인란의 선택을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-130">Optionally on the Ready to configure page, you can unselect the **Start the synchronization process as soon as configuration completes** checkbox.</span></span> <span data-ttu-id="689b8-131">[필터링](active-directory-aadconnectsync-configure-filtering.md)같은 추가적인 구성을 수행하려면 이 확인란을 선택하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-131">You should unselect this checkbox if you want to do additional configuration, such as [filtering](active-directory-aadconnectsync-configure-filtering.md).</span></span> <span data-ttu-id="689b8-132">이 옵션에 대한 선택을 취소하면, 마법사가 동기화를 구성하지만 스케줄러는 비활성 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-132">If you unselect this option, the wizard configures sync but leaves the scheduler disabled.</span></span> <span data-ttu-id="689b8-133">[설치 마법사를 다시 실행](active-directory-aadconnectsync-installation-wizard.md)하여 사용자가 수동으로 활성화할 때까지 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-133">It does not run until you enable it manually by [rerunning the installation wizard](active-directory-aadconnectsync-installation-wizard.md).</span></span>
   * <span data-ttu-id="689b8-134">온-프레미스 Active Directory에 Exchange가 있는 경우 [**Exchange 하이브리드 배포**](https://technet.microsoft.com/library/jj200581.aspx)를 사용하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-134">If you have Exchange in your on-premises Active Directory, then you also have an option to enable [**Exchange Hybrid deployment**](https://technet.microsoft.com/library/jj200581.aspx).</span></span> <span data-ttu-id="689b8-135">Exchange 사서함을 클라우드와 온-프레미스에 동시에 두려면 이 옵션을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-135">Enable this option if you plan to have Exchange mailboxes both in the cloud and on-premises at the same time.</span></span>
     <span data-ttu-id="689b8-136">![Azure AD Connect 구성 준비 완료](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="689b8-136">![Ready to configure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)</span></span>
9. <span data-ttu-id="689b8-137">설치가 완료되면 **끝내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-137">When the installation completes, click **Exit**.</span></span>
10. <span data-ttu-id="689b8-138">설치가 완료된 후 로그아웃하고 동기화 서비스 관리자 또는 동기화 규칙 편집기를 사용하기 전에 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-138">After the installation has completed, sign off and sign in again before you use Synchronization Service Manager or Synchronization Rule Editor.</span></span>

## <a name="videos"></a><span data-ttu-id="689b8-139">비디오</span><span class="sxs-lookup"><span data-stu-id="689b8-139">Videos</span></span>
<span data-ttu-id="689b8-140">빠른 설치 사용에 대한 비디오는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="689b8-140">For a video on using the express installation, see:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="689b8-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="689b8-141">Next steps</span></span>
<span data-ttu-id="689b8-142">Azure AD Connect를 설치했으므로 [설치를 확인하고 라이선스를 할당](active-directory-aadconnect-whats-next.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-142">Now that you have Azure AD Connect installed you can [verify the installation and assign licenses](active-directory-aadconnect-whats-next.md).</span></span>

<span data-ttu-id="689b8-143">[자동 업그레이드](active-directory-aadconnect-feature-automatic-upgrade.md), [실수로 인한 삭제 방지](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) 및 [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)를 설치하여 사용할 수 있는 이러한 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-143">Learn more about these features, which were enabled with the installation: [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md), [Prevent accidental deletes](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), and [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).</span></span>

<span data-ttu-id="689b8-144">공통 항목인 [스케줄러 및 동기화를 트리거하는 방법](active-directory-aadconnectsync-feature-scheduler.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-144">Learn more about these common topics: [scheduler and how to trigger sync](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

<span data-ttu-id="689b8-145">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="689b8-145">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="related-documentation"></a><span data-ttu-id="689b8-146">관련 설명서</span><span class="sxs-lookup"><span data-stu-id="689b8-146">Related documentation</span></span>
| <span data-ttu-id="689b8-147">항목</span><span class="sxs-lookup"><span data-stu-id="689b8-147">Topic</span></span> |
| --- | --- |
| <span data-ttu-id="689b8-148">Azure AD Connect 개요</span><span class="sxs-lookup"><span data-stu-id="689b8-148">Azure AD Connect overview</span></span> |
| <span data-ttu-id="689b8-149">사용자 지정된 설정을 사용하여 설치</span><span class="sxs-lookup"><span data-stu-id="689b8-149">Install using customized settings</span></span> |
| <span data-ttu-id="689b8-150">DirSync에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="689b8-150">Upgrade from DirSync</span></span> |
| <span data-ttu-id="689b8-151">설치에 사용되는 계정</span><span class="sxs-lookup"><span data-stu-id="689b8-151">Accounts used for installation</span></span> |

