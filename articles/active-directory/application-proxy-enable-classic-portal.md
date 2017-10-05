---
title: "클래식 포털에서 Azure AD 응용 프로그램 프록시 사용 | Microsoft Docs"
description: "Azure 클래식 포털에서 응용 프로그램 프록시를 설정하고 역방향 프록시에 커넥터를 설치합니다."
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
ms.openlocfilehash: ea97fdc8d146ed524a932018b572ceda0982738b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-application-proxy-in-the-classic-portal-and-download-connectors"></a><span data-ttu-id="db892-103">클래식 포털에서 응용 프로그램 프록시를 사용하도록 설정하고 커넥터 다운로드</span><span class="sxs-lookup"><span data-stu-id="db892-103">Enable Application Proxy in the classic portal and download connectors</span></span>
<span data-ttu-id="db892-104">이 문서에서는 Azure AD에서 클라우드 디렉터리에 Microsoft Azure AD 응용 프로그램 프록시를 사용하도록 설정하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-104">This article walks you through the steps to enable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="db892-105">도움을 받을 수 있는 응용 프로그램 프록시에 익숙하지 않은 경우 [온-프레미스 응용 프로그램에 안전한 원격 액세스를 제공하는 방법](active-directory-application-proxy-get-started.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db892-105">If you're unfamiliar with what Application Proxy can help you do, learn more about [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="db892-106">응용 프로그램 프록시 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="db892-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="db892-107">응용 프로그램 프록시 서비스를 사용하도록 설정하고 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-107">Before you can enable and use Application Proxy services, you need to have:</span></span>

* <span data-ttu-id="db892-108">사용자가 전역 관리자인 [Microsoft Azure AD 기본 또는 프리미엄 구독](active-directory-editions.md) 및 Azure AD 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="db892-108">A [Microsoft Azure AD basic or premium subscription](active-directory-editions.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="db892-109">응용 프로그램 프록시 커넥터를 설치할 수 있는 Windows Server 2012 R2 또는 2016을 실행하는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="db892-109">A server running Windows Server 2012 R2 or 2016, on which you can install the Application Proxy Connector.</span></span> <span data-ttu-id="db892-110">이 서버는 클라우드의 응용 프로그램 프록시 서비스에 요청을 보내고 게시 중인 응용 프로그램에 대한 HTTP 및 HTTPS 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-110">The server sends requests to the Application Proxy services in the cloud, and it needs an HTTP or HTTPS connection to the applications that you are publishing.</span></span>
  * <span data-ttu-id="db892-111">게시된 응용 프로그램에 대한 Single Sign-On의 경우 이 컴퓨터는 게시하는 응용 프로그램과 동일한 AD 도메인에 가입되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-111">For single sign-on to your published applications, this machine should be domain-joined in the same AD domain as the applications that you are publishing.</span></span> <span data-ttu-id="db892-112">자세한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db892-112">For information, see [Single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)</span></span>
* <span data-ttu-id="db892-113">조직에서 프록시 서버를 사용하여 인터넷에 연결하려면 구성하는 방법에 대한 세부 내용은 [기존 온-프레미스 프록시 서버로 작업](application-proxy-working-with-proxy-servers.md)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="db892-113">If your organization uses proxy servers to connect to the internet, read [Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md) for details on how to configure them.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="db892-114">포트 열기</span><span class="sxs-lookup"><span data-stu-id="db892-114">Open your ports</span></span>

<span data-ttu-id="db892-115">Azure AD 응용 프로그램 프록시를 위한 환경을 준비하려면 먼저 Azure 데이터 센터와 통신할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-115">To prepare your environment for Azure AD Application Proxy, you first need to enable communication to Azure data centers.</span></span> <span data-ttu-id="db892-116">방화벽이 경로에 있는 경우 커넥터가 응용 프로그램 프록시에 HTTPS(TCP) 요청을 할 수 있도록 방화벽이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-116">If there is a firewall in the path, make sure that it's open so that the Connector can make HTTPS (TCP) requests to the Application Proxy.</span></span>

1. <span data-ttu-id="db892-117">**아웃바운드** 트래픽에 대한 다음 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db892-117">Open the following ports to **outbound** traffic:</span></span>

   | <span data-ttu-id="db892-118">포트 번호</span><span class="sxs-lookup"><span data-stu-id="db892-118">Port number</span></span> | <span data-ttu-id="db892-119">사용 방법</span><span class="sxs-lookup"><span data-stu-id="db892-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="db892-120">80</span><span class="sxs-lookup"><span data-stu-id="db892-120">80</span></span> | <span data-ttu-id="db892-121">SSL 인증서의 유효성을 검사하는 동안 CRL(인증서 해지 목록) 다운로드</span><span class="sxs-lookup"><span data-stu-id="db892-121">Downloading certificate revocation lists (CRLs) while validating the SSL certificate</span></span> |
   | <span data-ttu-id="db892-122">443</span><span class="sxs-lookup"><span data-stu-id="db892-122">443</span></span> | <span data-ttu-id="db892-123">응용 프로그램 프록시 서비스와의 모든 아웃바운드 통신</span><span class="sxs-lookup"><span data-stu-id="db892-123">All outbound communication with the Application Proxy service</span></span> |

   <span data-ttu-id="db892-124">방화벽이 원래 사용자에 따라 트래픽에 적용되는 경우 네트워크 서비스로 실행되는 Windows 서비스에서 오는 트래픽에 대해 이러한 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db892-124">If your firewall enforces traffic according to originating users, open these ports for traffic coming from Windows services running as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="db892-125">표에는 커넥터 버전 1.5.132.0 이상에 대한 포트 요구 사항이 반영되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db892-125">The table reflects the port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="db892-126">이전 커넥터 버전이 아직도 있는 경우 5671, 8080, 9090, 9091, 9350, 9352 및 10100-10120 포트를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-126">If you still have an older connector version, you also need to enable the following ports: 5671, 8080, 9090, 9091, 9350, 9352, and 10100–10120.</span></span>
   >
   ><span data-ttu-id="db892-127">커넥터를 최신 버전으로 업데이트하는 방법에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md#automatic-updates)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db892-127">For information about updating your connectors to the newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="db892-128">방화벽이나 프록시에서 DNS 허용 목록을 허용하면 msappproxy.net 및 servicebus.windows.net에 대한 연결을 허용 목록에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db892-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections to msappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="db892-129">그렇지 않으면 매주 업데이트되는 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)에 액세스하도록 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-129">If not, you need to allow access to the [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="db892-130">[Azure AD 응용 프로그램 프록시 커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/)를 사용하여 커넥터가 응용 프로그램 프록시 서비스에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-130">Use the [Azure AD Application Proxy Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) to verify that your connector can reach the Application Proxy service.</span></span> <span data-ttu-id="db892-131">최소한 미국 중부 하위 지역 및 사용자에게 가까운 지역에는 모두 녹색 확인 표시가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-131">At a minimum, make sure that the Central US region and the region closest to you have all green checkmarks.</span></span> <span data-ttu-id="db892-132">그 외의 항목에도 녹색 확인 표시가 있으면 복원력이 더 뛰어난 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db892-132">Beyond that, more green checkmarks means greater resiliency.</span></span>

## <a name="enable-application-proxy-in-azure-ad"></a><span data-ttu-id="db892-133">Azure AD에서 응용 프로그램 프록시를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="db892-133">Enable Application Proxy in Azure AD</span></span>
1. <span data-ttu-id="db892-134">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-134">Sign in as an administrator in the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="db892-135">Active Directory로 이동하여 응용 프로그램 프록시를 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-135">Go to Active Directory and select the directory in which you want to enable Application Proxy.</span></span>

    ![Active Directory - 아이콘](./media/active-directory-application-proxy-enable/ad_icon.png)
3. <span data-ttu-id="db892-137">디렉터리 페이지에서 **구성**을 선택하고 **응용 프로그램 프록시**까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-137">Select **Configure** from the directory page, and scroll down to **Application Proxy**.</span></span>
4. <span data-ttu-id="db892-138">**이 디렉터리에 응용 프로그램 프록시 서비스 사용**을 **사용**하도록 설정/해제합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-138">Toggle **Enable Application Proxy Services for this Directory** to **Enabled**.</span></span>

    ![응용 프로그램 프록시 사용](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. <span data-ttu-id="db892-140">**지금 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-140">Select **Download now**.</span></span> <span data-ttu-id="db892-141">**Azure AD 응용 프로그램 프록시 커넥터 다운로드**가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="db892-141">The **Azure AD Application Proxy Connector Download** opens.</span></span> <span data-ttu-id="db892-142">사용 조건을 읽어보고 동의한 다음 **다운로드** 를 클릭하여 커넥터의 Windows Installer 파일(.exe)을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-142">Read and accept the license terms and click **Download** to save the Windows Installer file (.exe) for the connector.</span></span>

## <a name="install-and-register-the-connector"></a><span data-ttu-id="db892-143">커넥터 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="db892-143">Install and register the Connector</span></span>
1. <span data-ttu-id="db892-144">필수 구성 요소에 따라 준비한 서버에서 **AADApplicationProxyConnectorInstaller.exe** 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-144">Run **AADApplicationProxyConnectorInstaller.exe** on the server you prepared according to the prerequisites.</span></span>
2. <span data-ttu-id="db892-145">마법사의 지침에 따라 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-145">Follow the instructions in the wizard to install.</span></span>
3. <span data-ttu-id="db892-146">설치하는 동안 Azure AD 테넌트의 응용 프로그램 프록시를 사용하여 커넥터를 등록하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db892-146">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="db892-147">Azure AD 전역 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-147">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="db892-148">전역 관리자 테넌트는 Microsoft Azure 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db892-148">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="db892-149">커넥터를 등록하는 관리자가 응용 프로그램 프록시 서비스를 사용할 수 있는 동일한 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-149">Make sure the admin who registers the connector is in the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="db892-150">예를 들어, 테넌트 도메인이 contoso.com이면 관리자는 admin@contoso.com 또는 해당 도메인에 있는 다른 별칭이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-150">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="db892-151">서버에서 **IE 보안 강화 구성**이 **켜기**로 설정되어 있으면 등록 화면이 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db892-151">If **IE Enhanced Security Configuration** is set to **On** on the server, the registration screen might be blocked.</span></span> <span data-ttu-id="db892-152">액세스를 허용하려면 오류 메시지의 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="db892-152">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="db892-153">Internet Explorer 보안 강화가 해제되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="db892-153">Make sure that Internet Explorer Enhanced Security is off.</span></span>
   * <span data-ttu-id="db892-154">커넥터 등록에 실패한 경우 [응용 프로그램 프록시 문제 해결](active-directory-application-proxy-troubleshoot.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db892-154">If connector registration does not succeed, see [Troubleshoot Application Proxy](active-directory-application-proxy-troubleshoot.md).</span></span>  
4. <span data-ttu-id="db892-155">설치가 완료되면 두 개의 새 서비스가 서버에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="db892-155">When the installation completes, two new services are added to your server:</span></span>

   * <span data-ttu-id="db892-156">**Microsoft AAD 응용 프로그램 프록시 커넥터** 에서 연결 사용</span><span class="sxs-lookup"><span data-stu-id="db892-156">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

     * <span data-ttu-id="db892-157">**Microsoft AAD 응용 프로그램 프록시 커넥터 업데이터**는 자동화된 업데이트 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="db892-157">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="db892-158">이 서비스는 주기적으로 새 버전의 커넥터가 있는지 확인하고 필요에 따라 커넥터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-158">It periodically checks for new versions of the connector and updates the connector as needed.</span></span>

     ![앱 프록시 커넥터 서비스 - 스크린샷](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. <span data-ttu-id="db892-160">설치 창에서 **마침** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-160">Click **Finish** in the installation window.</span></span>

<span data-ttu-id="db892-161">커넥터에 대 한 정보는 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db892-161">For information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

<span data-ttu-id="db892-162">고가용성을 위해 커넥터를 두 개 이상 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-162">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="db892-163">추가 커넥터를 배포하려면 2단계와 3단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-163">To deploy more connectors, repeat steps 2 and 3.</span></span> <span data-ttu-id="db892-164">각 커넥터는 별도로 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-164">Each connector must be registered separately.</span></span>

<span data-ttu-id="db892-165">커넥터를 제거하려면 커넥터 서비스와 업데이트 프로그램 서비스를 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-165">If you want to uninstall the Connector, uninstall both the Connector service and the Updater service.</span></span> <span data-ttu-id="db892-166">서비스를 완전히 제거하려면 컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db892-166">Restart your computer to fully remove the service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db892-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db892-167">Next steps</span></span>
<span data-ttu-id="db892-168">이제 [응용 프로그램 프록시를 사용하여 응용 프로그램을 게시](active-directory-application-proxy-publish.md)할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="db892-168">You are now ready to [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

<span data-ttu-id="db892-169">별도 네트워크 또는 다른 위치에 응용 프로그램이 있는 경우 다른 커넥터 그룹을 사용하여 커넥터를 논리 단위로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db892-169">If you have applications that are on separate networks or different locations, you can use connector groups to organize the different connectors into logical units.</span></span> <span data-ttu-id="db892-170">[응용 프로그램 프록시 커넥터 작업](active-directory-application-proxy-connectors.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="db892-170">Learn more about [Working with Application Proxy connectors](active-directory-application-proxy-connectors.md).</span></span>
