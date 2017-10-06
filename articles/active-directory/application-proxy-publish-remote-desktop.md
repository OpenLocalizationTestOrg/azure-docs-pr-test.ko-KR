---
title: "Azure AD 응용 프로그램 프록시를 통해 원격 데스크톱 aaaPublish | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대 한 hello 기본 사항에 설명합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a><span data-ttu-id="56a90-103">Azure AD 응용 프로그램 프록시를 사용하여 원격 데스크톱 게시</span><span class="sxs-lookup"><span data-stu-id="56a90-103">Publish Remote Desktop with Azure AD Application Proxy</span></span>

<span data-ttu-id="56a90-104">이 문서에서는 어떻게 toodeploy 서비스 RDS (원격 데스크톱) 응용 프로그램 프록시를 통해 원격 사용자 생산성 이루어질 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-104">This article covers how toodeploy Remote Desktop Services (RDS) with Application Proxy so that remote users can still be productive.</span></span>

<span data-ttu-id="56a90-105">이 문서에 대 한 대상 그룹은 대상 사용자는 hello.</span><span class="sxs-lookup"><span data-stu-id="56a90-105">hello intended audience for this article is:</span></span>
- <span data-ttu-id="56a90-106">현재 Azure AD 응용 프로그램 프록시 하려는 고객 toooffer 더 많은 응용 프로그램 tootheir 최종 사용자가 원격 데스크톱 서비스를 통해 온-프레미스 응용 프로그램을 게시 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-106">Current Azure AD Application Proxy customers who want toooffer more applications tootheir end users by publishing on-premises applications through Remote Desktop Services.</span></span>
- <span data-ttu-id="56a90-107">Azure AD 응용 프로그램 프록시를 사용 하 여 배포의 tooreduce hello 공격 노출 하려는 현재 원격 데스크톱 서비스 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-107">Current Remote Desktop Services customers who want tooreduce hello attack surface of their deployment by using Azure AD Application Proxy.</span></span> <span data-ttu-id="56a90-108">이 시나리오에서는 2 단계 인증의 제한 된 집합을 제공 하 고 조건부 액세스 tooRDS를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-108">This scenario gives a limited set of two-step verification and conditional access controls tooRDS.</span></span>

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a><span data-ttu-id="56a90-109">응용 프로그램 프록시 hello 표준 RDS 배포에 적용 되는 방식</span><span class="sxs-lookup"><span data-stu-id="56a90-109">How Application Proxy fits in hello standard RDS deployment</span></span>

<span data-ttu-id="56a90-110">표준 RDS 배포에는 Windows Server에서 실행되는 다양한 원격 데스크톱 역할 서비스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-110">A standard RDS deployment includes various Remote Desktop role services running on Windows Server.</span></span> <span data-ttu-id="56a90-111">Hello를 살펴보면 [원격 데스크톱 서비스 아키텍처](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), 여러 배포 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-111">Looking at hello [Remote Desktop Services architecture](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), there are multiple deployment options.</span></span> <span data-ttu-id="56a90-112">가장 눈에 띄는 차이점 hello hello [Azure AD 응용 프로그램 프록시 RDS 배포](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (hello 다음 다이어그램에에서 표시) hello 다른 배포 옵션은 해당 hello 응용 프로그램 프록시 시나리오에는 영구적이 아웃 바운드 및 hello 커넥터 서비스를 실행 하는 hello 서버에서 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-112">hello most noticeable difference between hello [RDS deployment with Azure AD Application Proxy](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (shown in hello following diagram) and hello other deployment options is that hello Application Proxy scenario has a permanent outbound connection from hello server running hello connector service.</span></span> <span data-ttu-id="56a90-113">기타 배포에서는 부하 분산 장치를 통해 열린 인바운드 연결을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-113">Other deployments leave open inbound connections through a load balancer.</span></span>

![RDS VM hello와 공용 인터넷 hello 간 응용 프로그램 프록시가 위치](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

<span data-ttu-id="56a90-115">RDS 배포에서 hello RD 웹 역할 및 hello RD 게이트웨이 역할 인터넷 연결 컴퓨터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-115">In an RDS deployment, hello RD Web role and hello RD Gateway role run on Internet-facing machines.</span></span> <span data-ttu-id="56a90-116">이러한 끝점은 다음의 이유로 hello에 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-116">These endpoints are exposed for hello following reasons:</span></span>
- <span data-ttu-id="56a90-117">보기 hello 다양 한 온-프레미스 응용 프로그램 및 데스크톱에 액세스할 수 있습니다 및 RD 웹의 공용 끝점 toosign hello 사용자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-117">RD Web provides hello user a public endpoint toosign in and view hello various on-premises applications and desktops they can access.</span></span> <span data-ttu-id="56a90-118">리소스를 선택 하면 hello 네이티브 앱을 사용 하 여 hello 운영 체제에 대 한 RDP 연결 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-118">Upon selecting a resource, an RDP connection is created using hello native app on hello OS.</span></span>
- <span data-ttu-id="56a90-119">RD 게이트웨이 사용자가 hello RDP 연결 되 면 hello 그림으로 도착 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-119">RD Gateway comes into hello picture once a user launches hello RDP connection.</span></span> <span data-ttu-id="56a90-120">RD 게이트웨이 hello hello 인터넷을 통해 들어오는 hello 암호화 RDP 트래픽을 처리 및 toohello 사용자 hello 온-프레미스 서버를 통해 연결 하는 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-120">hello RD Gateway handles hello encrypted RDP traffic coming over hello Internet and translates it toohello on-premises server that hello user is connecting to.</span></span> <span data-ttu-id="56a90-121">이 시나리오에서는 RD 게이트웨이 받고 hello 트래픽 hello hello Azure AD 응용 프로그램 프록시에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-121">In this scenario, hello traffic hello RD Gateway is receiving comes from hello Azure AD Application Proxy.</span></span>

>[!TIP]
><span data-ttu-id="56a90-122">이전에 RDS를 배포 하지 않은 하거나 시작 하기 전에 자세한 정보를 원하는 경우 너무 방법을 알아보려면[원활 하 게 Azure 리소스 관리자 및 Azure 마켓플레이스와 RDS 배포](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-122">If you haven't deployed RDS before, or want more information before you begin, learn how too[seamlessly deploy RDS with Azure Resource Manager and Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).</span></span>

## <a name="requirements"></a><span data-ttu-id="56a90-123">요구 사항</span><span class="sxs-lookup"><span data-stu-id="56a90-123">Requirements</span></span>

- <span data-ttu-id="56a90-124">RD 웹 hello 둘 다 및 끝점에 위치 해야 하는 RD 게이트웨이 hello 시스템과 공통 루트와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-124">Both hello RD Web and RD Gateway endpoints must be located on hello same machine, and with a common root.</span></span> <span data-ttu-id="56a90-125">RD 게이트웨이 및 RD 웹 hello 두 응용 프로그램 간에 single sign-on 환경을 가질 수 있도록 단일 응용 프로그램으로 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-125">RD Web and RD Gateway will be published as a single application so you can have a single sign-on experience between hello two applications.</span></span>

- <span data-ttu-id="56a90-126">이미 [RDS를 배포](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)하고 [응용 프로그램 프록시를 사용하도록 설정](active-directory-application-proxy-enable.md)했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-126">You should already have [deployed RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure), and [enabled Application Proxy](active-directory-application-proxy-enable.md).</span></span>

- <span data-ttu-id="56a90-127">이 시나리오 hello RD 웹 페이지를 통해 연결 하는 Windows 7 또는 Windows 10 데스크톱에서 최종 사용자가 Internet Explorer를 통해 이동 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-127">This scenario assumes that your end users go through Internet Explorer on Windows 7 or Windows 10 desktops that connect through hello RD Web page.</span></span> <span data-ttu-id="56a90-128">다른 운영 체제 toosupport 해야 할 경우 참조 [다른 클라이언트 구성에 대 한 지원을](#support-for-other-client-configurations)합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-128">If you need toosupport other operating systems, see [Support for other client configurations](#support-for-other-client-configurations).</span></span>

  >[!NOTE]
  ><span data-ttu-id="56a90-129">Windows 10 Creator's Update는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-129">Windows 10 Creator's Update is not currently supported.</span></span>

- <span data-ttu-id="56a90-130">Internet Explorer에서 hello RDS ActiveX 추가 기능을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-130">On Internet Explorer, enable hello RDS ActiveX add-on.</span></span>

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a><span data-ttu-id="56a90-131">Hello joint RDS 및 응용 프로그램 프록시 시나리오를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-131">Deploy hello joint RDS and Application Proxy scenario</span></span>

<span data-ttu-id="56a90-132">RDS 및 사용자 환경에 대 한 Azure AD 응용 프로그램 프록시를 설정한 후 hello 단계 toocombine hello 두 가지 솔루션을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-132">After setting up RDS and Azure AD Application Proxy for your environment, follow hello steps toocombine hello two solutions.</span></span> <span data-ttu-id="56a90-133">이러한 단계는 응용 프로그램으로 hello 두 개의 웹 RDS 끝점 (RD 웹 및 RD 게이트웨이)을 게시 하 고 다음 응용 프로그램 프록시를 통해 프로그램 RDS toogo에 트래픽을 보내는 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-133">These steps walk through publishing hello two web-facing RDS endpoints (RD Web and RD Gateway) as applications, and then directing traffic on your RDS toogo through Application Proxy.</span></span>

### <a name="publish-hello-rd-host-endpoint"></a><span data-ttu-id="56a90-134">Hello RD 호스트 끝점을 게시</span><span class="sxs-lookup"><span data-stu-id="56a90-134">Publish hello RD host endpoint</span></span>

1. <span data-ttu-id="56a90-135">[새 응용 프로그램 프록시 응용 프로그램 게시](application-proxy-publish-azure-portal.md) 다음 값에는 hello로:</span><span class="sxs-lookup"><span data-stu-id="56a90-135">[Publish a new Application Proxy application](application-proxy-publish-azure-portal.md) with hello following values:</span></span>
   - <span data-ttu-id="56a90-136">내부 URL: https://\<rdhost\>.com / 여기서 \<rdhost\> RD 게이트웨이 및 RD 웹 공유 하는 hello 공통 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-136">Internal URL: https://\<rdhost\>.com/, where \<rdhost\> is hello common root that RD Web and RD Gateway share.</span></span>
   - <span data-ttu-id="56a90-137">외부 URL:이 필드는 자동으로 채워지며 hello 응용 프로그램의 hello 이름에 따라 있지만 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-137">External URL: This field is automatically populated based on hello name of hello application, but you can modify it.</span></span> <span data-ttu-id="56a90-138">Rds.에 액세스할 때 사용자에 게 toothis URL 되돌려집니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-138">Your users will go toothis URL when they access RDS.</span></span>
   - <span data-ttu-id="56a90-139">사전 인증 방법: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56a90-139">Preauthentication method: Azure Active Directory</span></span>
   - <span data-ttu-id="56a90-140">URL 헤더 변환: 아니요</span><span class="sxs-lookup"><span data-stu-id="56a90-140">Translate URL headers: No</span></span>
2. <span data-ttu-id="56a90-141">사용자 할당 toohello RD 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-141">Assign users toohello published RD application.</span></span> <span data-ttu-id="56a90-142">액세스 tooRDS 너무가 모두 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-142">Make sure they all have access tooRDS, too.</span></span>
3. <span data-ttu-id="56a90-143">Hello single sign-on 방법으로 hello 응용 프로그램에 대 한 둡니다 **Azure AD에서 single sign-on 사용 하지 않도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-143">Leave hello single sign-on method for hello application as **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="56a90-144">Tooauthenticate 프로그램 사용자에 게 요청 하 고 나면 AD tooAzure를 한 번 tooRD 웹, 하지만 single sign on tooRD 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-144">Your users are asked tooauthenticate once tooAzure AD and once tooRD Web, but have single sign-on tooRD Gateway.</span></span>
4. <span data-ttu-id="56a90-145">너무 이동**Azure Active Directory** > **앱 등록** > *응용 프로그램* > **설정**.</span><span class="sxs-lookup"><span data-stu-id="56a90-145">Go too**Azure Active Directory** > **App Registrations** > *Your application* > **Settings**.</span></span>
5. <span data-ttu-id="56a90-146">선택 **속성** 및 업데이트 hello **홈 페이지 URL** 필드 toopoint tooyour RD 웹 끝점 (https:// 같은\<rdhost\>.com/RDWeb).</span><span class="sxs-lookup"><span data-stu-id="56a90-146">Select **Properties** and update hello **Home-page URL** field toopoint tooyour RD Web endpoint (like https://\<rdhost\>.com/RDWeb).</span></span>

### <a name="direct-rds-traffic-tooapplication-proxy"></a><span data-ttu-id="56a90-147">직접 RDS 트래픽 tooApplication 프록시</span><span class="sxs-lookup"><span data-stu-id="56a90-147">Direct RDS traffic tooApplication Proxy</span></span>

<span data-ttu-id="56a90-148">관리자 권한으로 toohello RDS 배포를 연결 하 고 hello 배포에 대 한 hello RD 게이트웨이 서버 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-148">Connect toohello RDS deployment as an administrator and change hello RD Gateway server name for hello deployment.</span></span> <span data-ttu-id="56a90-149">이렇게 하면 연결 hello Azure AD 응용 프로그램 프록시를 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-149">This ensures that connections go through hello Azure AD Application Proxy.</span></span>

1. <span data-ttu-id="56a90-150">Hello RD 연결 브로커 역할을 실행 하는 toohello RDS 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-150">Connect toohello RDS server running hello RD Connection Broker role.</span></span>
2. <span data-ttu-id="56a90-151">**서버 관리자**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-151">Launch **Server Manager**.</span></span>
3. <span data-ttu-id="56a90-152">선택 **원격 데스크톱 서비스** hello hello 왼쪽 창에서.</span><span class="sxs-lookup"><span data-stu-id="56a90-152">Select **Remote Desktop Services** from hello pane on hello left.</span></span>
4. <span data-ttu-id="56a90-153">**개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-153">Select **Overview**.</span></span>
5. <span data-ttu-id="56a90-154">배포 개요 섹션 hello에서 hello 드롭다운 메뉴를 선택 하 고 선택 **배포 속성 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-154">In hello Deployment Overview section, select hello drop-down menu and choose **Edit deployment properties**.</span></span>
6. <span data-ttu-id="56a90-155">Hello RD 게이트웨이 탭에서 변경 hello **서버 이름** 필드 toohello hello RD 호스트 끝점 응용 프로그램 프록시에 대해 설정 하는 외부 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-155">In hello RD Gateway tab, change hello **Server name** field toohello External URL that you set for hello RD host endpoint in Application Proxy.</span></span>
7. <span data-ttu-id="56a90-156">변경 hello **메서드 로그온** 너무 필드**암호 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-156">Change hello **Logon method** field too**Password Authentication**.</span></span>

  ![RDS의 배포 속성 화면](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. <span data-ttu-id="56a90-158">각 컬렉션에 대 한 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-158">For each collection, run hello following command.</span></span> <span data-ttu-id="56a90-159">*\<yourcollectionname\>* 및 *\<proxyfrontendurl\>*을 사용자 고유의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-159">Replace *\<yourcollectionname\>* and *\<proxyfrontendurl\>* with your own information.</span></span> <span data-ttu-id="56a90-160">이 명령은 RD 웹과 RD 게이트웨이 간에 Single Sign-On을 사용하도록 설정하고 성능을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-160">This command enables single sign-on between RD Web and RD Gateway, and optimizes performance:</span></span>

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   <span data-ttu-id="56a90-161">**예:**</span><span class="sxs-lookup"><span data-stu-id="56a90-161">**For example:**</span></span>
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. <span data-ttu-id="56a90-162">hello 다음 명령을 실행 하는이 컬렉션에 대해 RDWeb에서 다운로드할 수 있는 보기 hello RDP 파일 내용을 뿐만 아니라 사용자 지정 RDP 속성 hello tooverify hello 수정:</span><span class="sxs-lookup"><span data-stu-id="56a90-162">tooverify hello modification of hello custom RDP properties as well as view hello RDP file contents that will be downloaded from RDWeb for this collection, run hello following command:</span></span>
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

<span data-ttu-id="56a90-163">원격 데스크톱을 구성 했으므로, Azure AD 응용 프로그램 프록시로 전송.rds 입니다의 hello 인터넷 구성 요소로</span><span class="sxs-lookup"><span data-stu-id="56a90-163">Now that you've configured Remote Desktop, Azure AD Application Proxy has taken over as hello internet-facing component of RDS.</span></span> <span data-ttu-id="56a90-164">제거할 수 있습니다 hello RD 웹 및 RD 게이트웨이 컴퓨터에서 다른 공용 인터넷 연결 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-164">You can remove hello other public internet-facing endpoints on your RD Web and RD Gateway machines.</span></span>

## <a name="test-hello-scenario"></a><span data-ttu-id="56a90-165">테스트 hello 시나리오</span><span class="sxs-lookup"><span data-stu-id="56a90-165">Test hello scenario</span></span>

<span data-ttu-id="56a90-166">Windows 7 또는 10 컴퓨터에서 Internet Explorer로 hello 시나리오를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-166">Test hello scenario with Internet Explorer on a Windows 7 or 10 computer.</span></span>

1. <span data-ttu-id="56a90-167">Toohello 외부 URL을 설정 하거나 hello에 응용 프로그램을 찾고 [MyApps 패널](https://myapps.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-167">Go toohello external URL you set up, or find your application in hello [MyApps panel](https://myapps.microsoft.com).</span></span>
2. <span data-ttu-id="56a90-168">Tooauthenticate tooAzure Active Directory는 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-168">You are asked tooauthenticate tooAzure Active Directory.</span></span> <span data-ttu-id="56a90-169">Toohello 응용 프로그램을 할당 하는 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-169">Use an account that you assigned toohello application.</span></span>
3. <span data-ttu-id="56a90-170">Tooauthenticate tooRD 웹은 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-170">You are asked tooauthenticate tooRD Web.</span></span>
4. <span data-ttu-id="56a90-171">RDS 인증이 성공 하면 hello 데스크톱 또는 응용 프로그램 및 ְ ֳ  선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-171">Once your RDS authentication succeeds, you can select hello desktop or application you want, and start working.</span></span>

## <a name="support-for-other-client-configurations"></a><span data-ttu-id="56a90-172">다른 클라이언트 구성에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="56a90-172">Support for other client configurations</span></span>

<span data-ttu-id="56a90-173">이 문서에 설명 된 hello 구성은 Windows 7 또는 10, Internet Explorer 및 hello RDS ActiveX 추가 기능에서 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-173">hello configuration outlined in this article is for users on Windows 7 or 10, with Internet Explorer plus hello RDS ActiveX add-on.</span></span> <span data-ttu-id="56a90-174">그러나 필요한 경우 다른 운영 체제 또는 브라우저를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-174">If you need to, however, you can support other operating systems or browsers.</span></span> <span data-ttu-id="56a90-175">hello 인증 방법을 사용 하는 hello 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-175">hello difference is in hello authentication method that you use.</span></span>

| <span data-ttu-id="56a90-176">인증 방법</span><span class="sxs-lookup"><span data-stu-id="56a90-176">Authentication method</span></span> | <span data-ttu-id="56a90-177">지원되는 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="56a90-177">Supported client configuration</span></span> |
| --------------------- | ------------------------------ |
| <span data-ttu-id="56a90-178">사전 인증</span><span class="sxs-lookup"><span data-stu-id="56a90-178">Pre-authentication</span></span>    | <span data-ttu-id="56a90-179">Internet Explorer + RDS ActiveX 추가 기능을 사용하는 Windows 7/10</span><span class="sxs-lookup"><span data-stu-id="56a90-179">Windows 7/10 using Internet Explorer + RDS ActiveX add-on</span></span> |
| <span data-ttu-id="56a90-180">통과</span><span class="sxs-lookup"><span data-stu-id="56a90-180">Passthrough</span></span> | <span data-ttu-id="56a90-181">Hello Microsoft 원격 데스크톱 응용 프로그램을 지 원하는 다른 운영 체제</span><span class="sxs-lookup"><span data-stu-id="56a90-181">Any other operating system that supports hello Microsoft Remote Desktop application</span></span> |

<span data-ttu-id="56a90-182">hello 사전 인증 흐름 hello 통과 흐름 보다 많은 보안 혜택을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-182">hello pre-authentication flow offers more security benefits than hello passthrough flow.</span></span> <span data-ttu-id="56a90-183">사전 인증을 사용하면 온-프레미스 리소스에 대해 Single Sign-On, 조건부 액세스 및 2단계 인증과 같은 Azure AD 인증 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-183">With pre-authentication you can leverage Azure AD authentication features like single sign-on, conditional access, and two-step verification for your on-premises resources.</span></span> <span data-ttu-id="56a90-184">또한 인증된 트래픽만 네트워크에 도달하도록합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-184">You also ensure that only authenticated traffic reaches your network.</span></span>

<span data-ttu-id="56a90-185">toouse 통과 인증, 있습니다이 문서에 나열 된 두 가지 수정 사항을 toohello 단계:</span><span class="sxs-lookup"><span data-stu-id="56a90-185">toouse passthrough authentication, there are just two modifications toohello steps listed in this article:</span></span>
1. <span data-ttu-id="56a90-186">[hello RD 호스트 끝점을 게시](#publish-the-rd-host-endpoint) 1 단계, 너무 hello 사전 인증 방법을 설정**통과**합니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-186">In [Publish hello RD host endpoint](#publish-the-rd-host-endpoint) step 1, set hello Preauthentication method too**Passthrough**.</span></span>
2. <span data-ttu-id="56a90-187">[직접 RDS tooApplication 프록시 트래픽](#direct-rds-traffic-to-application-proxy), 완전히 8 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="56a90-187">In [Direct RDS traffic tooApplication Proxy](#direct-rds-traffic-to-application-proxy), skip step 8 entirely.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56a90-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56a90-188">Next steps</span></span>

[<span data-ttu-id="56a90-189">원격 액세스 tooSharePoint Azure AD 응용 프로그램 프록시를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="56a90-189">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)  
[<span data-ttu-id="56a90-190">Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="56a90-190">Security considerations for accessing apps remotely by using Azure AD Application Proxy</span></span>](application-proxy-security-considerations.md)
