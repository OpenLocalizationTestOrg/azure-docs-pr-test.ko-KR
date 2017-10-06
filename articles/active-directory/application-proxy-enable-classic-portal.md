---
title: "hello 클래식 포털에서 Azure AD 응용 프로그램 프록시 aaaEnable | Microsoft Docs"
description: "Hello Azure 클래식 포털에서에서 응용 프로그램 프록시를 설정 하 고 hello 역방향 프록시에 대 한 hello 커넥터를 설치 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a><span data-ttu-id="4bbe8-103">Hello 클래식 포털에서 응용 프로그램 프록시를 사용 하도록 설정 하 고 커넥터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-103">Enable Application Proxy in hello classic portal and download connectors</span></span>
<span data-ttu-id="4bbe8-104">이 문서에서는 Azure AD의 hello 단계 tooenable 클라우드 디렉터리에 대 한 Microsoft Azure AD 응용 프로그램 프록시를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-104">This article walks you through hello steps tooenable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="4bbe8-105">어떤 응용 프로그램 프록시 도와 작업을 수행할 수 있는 잘 모르는 경우에 대해 자세히 알아보세요 [어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램](active-directory-application-proxy-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-105">If you're unfamiliar with what Application Proxy can help you do, learn more about [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="4bbe8-106">응용 프로그램 프록시 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4bbe8-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="4bbe8-107">사용 하도록 설정 하 고 응용 프로그램 프록시 서비스를 사용할 수 있습니다, toohave가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-107">Before you can enable and use Application Proxy services, you need toohave:</span></span>

* <span data-ttu-id="4bbe8-108">사용자가 전역 관리자인 [Microsoft Azure AD 기본 또는 프리미엄 구독](active-directory-editions.md) 및 Azure AD 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-108">A [Microsoft Azure AD basic or premium subscription](active-directory-editions.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="4bbe8-109">Hello 응용 프로그램 프록시 커넥터를 설치할 수 있는 2016 또는 Windows Server 2012 r 2를 실행 하는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-109">A server running Windows Server 2012 R2 or 2016, on which you can install hello Application Proxy Connector.</span></span> <span data-ttu-id="4bbe8-110">hello 서버 hello 클라우드에서 요청에 toohello 응용 프로그램 프록시 서비스를 보내고는 HTTP 또는 HTTPS 연결 toohello 응용 프로그램을 게시 하는 데 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-110">hello server sends requests toohello Application Proxy services in hello cloud, and it needs an HTTP or HTTPS connection toohello applications that you are publishing.</span></span>
  * <span data-ttu-id="4bbe8-111">게시 된 응용 프로그램을 single sign on tooyour에 대 한이 컴퓨터를 도메인에 가입할 수 hello 동일한 AD 도메인에 게시 하는 hello 응용 프로그램으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-111">For single sign-on tooyour published applications, this machine should be domain-joined in hello same AD domain as hello applications that you are publishing.</span></span> <span data-ttu-id="4bbe8-112">자세한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-112">For information, see [Single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)</span></span>
* <span data-ttu-id="4bbe8-113">조직에서 프록시를 사용 하는 경우 서버 tooconnect toohello 인터넷 읽을 [작업을 기존 온-프레미스 프록시 서버](application-proxy-working-with-proxy-servers.md) 방법에 대 한 자세한 내용은 tooconfigure 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-113">If your organization uses proxy servers tooconnect toohello internet, read [Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md) for details on how tooconfigure them.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="4bbe8-114">포트 열기</span><span class="sxs-lookup"><span data-stu-id="4bbe8-114">Open your ports</span></span>

<span data-ttu-id="4bbe8-115">tooprepare 환경을 Azure AD 응용 프로그램 프록시에 대 한 먼저 tooenable 통신 tooAzure 데이터 센터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-115">tooprepare your environment for Azure AD Application Proxy, you first need tooenable communication tooAzure data centers.</span></span> <span data-ttu-id="4bbe8-116">Hello 경로에 방화벽이 있는 경우 것는 열려 있으므로 커넥터에서 HTTPS (TCP)를 만들 수는 hello toohello 응용 프로그램 프록시를 요청 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-116">If there is a firewall in hello path, make sure that it's open so that hello Connector can make HTTPS (TCP) requests toohello Application Proxy.</span></span>

1. <span data-ttu-id="4bbe8-117">열기 hello 다음 포트가 너무**아웃 바운드** 트래픽:</span><span class="sxs-lookup"><span data-stu-id="4bbe8-117">Open hello following ports too**outbound** traffic:</span></span>

   | <span data-ttu-id="4bbe8-118">포트 번호</span><span class="sxs-lookup"><span data-stu-id="4bbe8-118">Port number</span></span> | <span data-ttu-id="4bbe8-119">사용 방법</span><span class="sxs-lookup"><span data-stu-id="4bbe8-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="4bbe8-120">80</span><span class="sxs-lookup"><span data-stu-id="4bbe8-120">80</span></span> | <span data-ttu-id="4bbe8-121">Hello SSL 인증서를 확인 하는 동안 다운로드 인증서 해지 목록 (Crl)</span><span class="sxs-lookup"><span data-stu-id="4bbe8-121">Downloading certificate revocation lists (CRLs) while validating hello SSL certificate</span></span> |
   | <span data-ttu-id="4bbe8-122">443</span><span class="sxs-lookup"><span data-stu-id="4bbe8-122">443</span></span> | <span data-ttu-id="4bbe8-123">응용 프로그램 프록시 서비스 hello로 모든 아웃 바운드 통신</span><span class="sxs-lookup"><span data-stu-id="4bbe8-123">All outbound communication with hello Application Proxy service</span></span> |

   <span data-ttu-id="4bbe8-124">방화벽에는 toooriginating 사용자에 따라 트래픽을 강제 적용을 네트워크 서비스로 실행 되는 Windows 서비스에서 들어오는 트래픽에 대해 이러한 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-124">If your firewall enforces traffic according toooriginating users, open these ports for traffic coming from Windows services running as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4bbe8-125">hello 반영 되어 1.5.132.0 커넥터 버전에 대 한 hello 포트 요구 사항 및 새 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-125">hello table reflects hello port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="4bbe8-126">이전 커넥터 버전을 계속 해야 하는 경우 또한 해야 포트 다음 tooenable hello: 5671, 8080, 9090, 9091, 9350, 9352, 및 10100 – 10120 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-126">If you still have an older connector version, you also need tooenable hello following ports: 5671, 8080, 9090, 9091, 9350, 9352, and 10100–10120.</span></span>
   >
   ><span data-ttu-id="4bbe8-127">커넥터 toohello 최신 버전을 업데이트 하는 방법에 대 한 정보를 참조 하십시오. [이해 Azure AD 응용 프로그램 프록시 커넥터](application-proxy-understand-connectors.md#automatic-updates)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-127">For information about updating your connectors toohello newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="4bbe8-128">방화벽 또는 프록시 DNS 허용 목록이 허용 하는 경우 허용 목록 연결 toomsappproxy.net 및 servicebus.windows.net 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections toomsappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="4bbe8-129">Tooallow 액세스 toohello 필요 그렇지 않은 경우 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)는 매주 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-129">If not, you need tooallow access toohello [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="4bbe8-130">사용 하 여 hello [Azure AD 응용 프로그램 프록시 커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify 커넥터 hello 응용 프로그램 프록시 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-130">Use hello [Azure AD Application Proxy Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify that your connector can reach hello Application Proxy service.</span></span> <span data-ttu-id="4bbe8-131">여기에 최소한 hello 중앙 미국 지역과 hello 지역 가장 가까운 tooyou는 모두 녹색 확인 표시가 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-131">At a minimum, make sure that hello Central US region and hello region closest tooyou have all green checkmarks.</span></span> <span data-ttu-id="4bbe8-132">그 외의 항목에도 녹색 확인 표시가 있으면 복원력이 더 뛰어난 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-132">Beyond that, more green checkmarks means greater resiliency.</span></span>

## <a name="enable-application-proxy-in-azure-ad"></a><span data-ttu-id="4bbe8-133">Azure AD에서 응용 프로그램 프록시를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="4bbe8-133">Enable Application Proxy in Azure AD</span></span>
1. <span data-ttu-id="4bbe8-134">Hello에 관리자 권한으로 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-134">Sign in as an administrator in hello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="4bbe8-135">디렉터리 tooActive 이동한 다음 응용 프로그램 프록시 tooenable 원하는 hello 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-135">Go tooActive Directory and select hello directory in which you want tooenable Application Proxy.</span></span>

    ![Active Directory - 아이콘](./media/active-directory-application-proxy-enable/ad_icon.png)
3. <span data-ttu-id="4bbe8-137">선택 **구성** hello 디렉터리 페이지에서 너무 아래로 스크롤하여 및**응용 프로그램 프록시**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-137">Select **Configure** from hello directory page, and scroll down too**Application Proxy**.</span></span>
4. <span data-ttu-id="4bbe8-138">설정/해제 **이 디렉터리에 대 한 응용 프로그램 프록시 서비스 사용** 너무**Enabled**합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-138">Toggle **Enable Application Proxy Services for this Directory** too**Enabled**.</span></span>

    ![응용 프로그램 프록시 사용](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. <span data-ttu-id="4bbe8-140">**지금 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-140">Select **Download now**.</span></span> <span data-ttu-id="4bbe8-141">hello **Azure AD 응용 프로그램 프록시 커넥터 다운로드** 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-141">hello **Azure AD Application Proxy Connector Download** opens.</span></span> <span data-ttu-id="4bbe8-142">Hello 사용 조건을 읽고 동의 클릭 **다운로드** hello 커넥터에 대 한 toosave hello Windows Installer 파일 (.exe).</span><span class="sxs-lookup"><span data-stu-id="4bbe8-142">Read and accept hello license terms and click **Download** toosave hello Windows Installer file (.exe) for hello connector.</span></span>

## <a name="install-and-register-hello-connector"></a><span data-ttu-id="4bbe8-143">설치 하 고 hello 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="4bbe8-143">Install and register hello Connector</span></span>
1. <span data-ttu-id="4bbe8-144">실행 **AADApplicationProxyConnectorInstaller.exe** hello 서버에 따라 toohello 필수 구성 요소를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-144">Run **AADApplicationProxyConnectorInstaller.exe** on hello server you prepared according toohello prerequisites.</span></span>
2. <span data-ttu-id="4bbe8-145">Hello 마법사 tooinstall의 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-145">Follow hello instructions in hello wizard tooinstall.</span></span>
3. <span data-ttu-id="4bbe8-146">설치 하는 동안 Azure AD 테 넌 트의 응용 프로그램 프록시 hello로 증명된 tooregister hello 커넥터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-146">During installation, you are prompted tooregister hello connector with hello Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="4bbe8-147">Azure AD 전역 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-147">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="4bbe8-148">전역 관리자 테넌트는 Microsoft Azure 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-148">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="4bbe8-149">Admin 님 안녕하세요 hello 커넥터가 레지스터 hello 설정한 같은 디렉터리는 응용 프로그램 프록시 서비스 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-149">Make sure hello admin who registers hello connector is in hello same directory where you enabled hello Application Proxy service.</span></span> <span data-ttu-id="4bbe8-150">예를 들어 hello 테 넌 트 도메인이 contoso.com 이면 admin 님 안녕하세요 해야 admin@contoso.com 또는 해당 도메인에 다른 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-150">For example, if hello tenant domain is contoso.com, hello admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="4bbe8-151">경우 **IE 보안 강화 구성** 너무 설정**에** hello 서버 hello 등록 화면이 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-151">If **IE Enhanced Security Configuration** is set too**On** on hello server, hello registration screen might be blocked.</span></span> <span data-ttu-id="4bbe8-152">hello 오류 메시지의 지침에 따라 hello tooallow 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-152">tooallow access, follow hello instructions in hello error message.</span></span> <span data-ttu-id="4bbe8-153">Internet Explorer 보안 강화가 해제되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-153">Make sure that Internet Explorer Enhanced Security is off.</span></span>
   * <span data-ttu-id="4bbe8-154">커넥터 등록에 실패한 경우 [응용 프로그램 프록시 문제 해결](active-directory-application-proxy-troubleshoot.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-154">If connector registration does not succeed, see [Troubleshoot Application Proxy](active-directory-application-proxy-troubleshoot.md).</span></span>  
4. <span data-ttu-id="4bbe8-155">Hello 설치가 완료 되 면 두 개의 새로운 서비스가 tooyour 서버를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-155">When hello installation completes, two new services are added tooyour server:</span></span>

   * <span data-ttu-id="4bbe8-156">**Microsoft AAD 응용 프로그램 프록시 커넥터** 에서 연결 사용</span><span class="sxs-lookup"><span data-stu-id="4bbe8-156">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

     * <span data-ttu-id="4bbe8-157">**Microsoft AAD 응용 프로그램 프록시 커넥터 업데이터**는 자동화된 업데이트 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-157">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="4bbe8-158">정기적으로 새 버전의 hello 커넥터에 대 한 확인 하 고 필요에 따라 hello 커넥터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-158">It periodically checks for new versions of hello connector and updates hello connector as needed.</span></span>

     ![앱 프록시 커넥터 서비스 - 스크린샷](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. <span data-ttu-id="4bbe8-160">클릭 **마침** hello 설치 창에서.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-160">Click **Finish** in hello installation window.</span></span>

<span data-ttu-id="4bbe8-161">커넥터에 대 한 정보는 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-161">For information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

<span data-ttu-id="4bbe8-162">고가용성을 위해 커넥터를 두 개 이상 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-162">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="4bbe8-163">toodeploy 자세한 커넥터 반복 2와 3 단계.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-163">toodeploy more connectors, repeat steps 2 and 3.</span></span> <span data-ttu-id="4bbe8-164">각 커넥터는 별도로 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-164">Each connector must be registered separately.</span></span>

<span data-ttu-id="4bbe8-165">Toouninstall hello 커넥터 원한다 면 hello 커넥터 서비스와 hello 업데이트 프로그램 서비스를 모두 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-165">If you want toouninstall hello Connector, uninstall both hello Connector service and hello Updater service.</span></span> <span data-ttu-id="4bbe8-166">컴퓨터 toofully 제거 hello 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-166">Restart your computer toofully remove hello service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bbe8-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4bbe8-167">Next steps</span></span>
<span data-ttu-id="4bbe8-168">이제 준비가 너무[응용 프로그램 프록시는 응용 프로그램 게시](active-directory-application-proxy-publish.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-168">You are now ready too[Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

<span data-ttu-id="4bbe8-169">별도 네트워크 또는 서로 다른 위치에 있는 응용 프로그램의 경우 논리 단위로 커넥터 그룹 tooorganize hello 다른 커넥터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-169">If you have applications that are on separate networks or different locations, you can use connector groups tooorganize hello different connectors into logical units.</span></span> <span data-ttu-id="4bbe8-170">[응용 프로그램 프록시 커넥터 작업](active-directory-application-proxy-connectors.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4bbe8-170">Learn more about [Working with Application Proxy connectors](active-directory-application-proxy-connectors.md).</span></span>
