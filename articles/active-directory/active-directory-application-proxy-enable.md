---
title: "Azure AD 앱 프록시 - 커넥터 설치 시작 | Microsoft Docs"
description: "Azure Portal에서 응용 프로그램 프록시를 설정하고 역방향 프록시에 커넥터를 설치합니다."
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
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 77acb23f33fd656a12c27107cb159613a8b2aec4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-proxy-and-install-the-connector"></a><span data-ttu-id="f7097-103">응용 프로그램 프록시 시작 및 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="f7097-103">Get started with Application Proxy and install the connector</span></span>
<span data-ttu-id="f7097-104">이 문서에서는 Azure AD에서 클라우드 디렉터리에 Microsoft Azure AD 응용 프로그램 프록시를 사용하도록 설정하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-104">This article walks you through the steps to enable Microsoft Azure AD Application Proxy for your cloud directory in Azure AD.</span></span>

<span data-ttu-id="f7097-105">응용 프로그램 프록시가 조직에 가져오는 보안 및 생산성의 이점을 잘 모르는 경우 [온-프레미스 응용 프로그램에 보안된 원격 액세스를 제공하는 방법](active-directory-application-proxy-get-started.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-105">If you're not yet aware of the security and productivity benefits Application Proxy brings to your organization, learn more about [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

## <a name="application-proxy-prerequisites"></a><span data-ttu-id="f7097-106">응용 프로그램 프록시 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f7097-106">Application Proxy prerequisites</span></span>
<span data-ttu-id="f7097-107">응용 프로그램 프록시 서비스를 사용하도록 설정하고 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-107">Before you can enable and use Application Proxy services, you need to have:</span></span>

* <span data-ttu-id="f7097-108">사용자가 전역 관리자인 [Microsoft Azure AD 기본 또는 프리미엄 구독](active-directory-editions.md) 및 Azure AD 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-108">A [Microsoft Azure AD basic or premium subscription](active-directory-editions.md) and an Azure AD directory for which you are a global administrator.</span></span>
* <span data-ttu-id="f7097-109">응용 프로그램 프록시 커넥터를 설치할 수 있는 Windows Server 2012 R2 또는 2016을 실행하는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-109">A server running Windows Server 2012 R2 or 2016, on which you can install the Application Proxy Connector.</span></span> <span data-ttu-id="f7097-110">서버는 클라우드의 응용 프로그램 프록시 서비스 및 게시 중인 온-프레미스 응용 프로그램에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-110">The server needs to be able to connect to the Application Proxy services in the cloud, and the on-premises applications that you are publishing.</span></span>
  * <span data-ttu-id="f7097-111">Kerberos 제한된 위임을 사용하는 게시된 응용 프로그램에 대한 Single Sign-On의 경우 이 컴퓨터는 게시하는 응용 프로그램과 동일한 AD 도메인에 가입되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-111">For single sign-on to your published applications using Kerberos Constrained Delegation, this machine should be domain-joined in the same AD domain as the applications that you are publishing.</span></span> <span data-ttu-id="f7097-112">자세한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On용 KCD](active-directory-application-proxy-sso-using-kcd.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7097-112">For information, see [KCD for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

<span data-ttu-id="f7097-113">조직에서 프록시 서버를 사용하여 인터넷에 연결하려면 응용 프로그램 프록시를 시작하기 전에 구성하는 방법에 대한 세부 내용은 [기존 온-프레미스 프록시 서버로 작업](application-proxy-working-with-proxy-servers.md)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="f7097-113">If your organization uses proxy servers to connect to the internet, read [Work with existing on-premises proxy servers](application-proxy-working-with-proxy-servers.md) for details on how to configure them before you get started with Application Proxy.</span></span>

## <a name="open-your-ports"></a><span data-ttu-id="f7097-114">포트 열기</span><span class="sxs-lookup"><span data-stu-id="f7097-114">Open your ports</span></span>

<span data-ttu-id="f7097-115">Azure AD 응용 프로그램 프록시를 위한 환경을 준비하려면 먼저 Azure 데이터 센터와 통신할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-115">To prepare your environment for Azure AD Application Proxy, you first need to enable communication to Azure data centers.</span></span> <span data-ttu-id="f7097-116">방화벽이 경로에 있는 경우 커넥터가 응용 프로그램 프록시에 HTTPS(TCP) 요청을 할 수 있도록 방화벽이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-116">If there is a firewall in the path, make sure that it's open so that the Connector can make HTTPS (TCP) requests to the Application Proxy.</span></span>

1. <span data-ttu-id="f7097-117">**아웃바운드** 트래픽에 대한 다음 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-117">Open the following ports to **outbound** traffic:</span></span>

   | <span data-ttu-id="f7097-118">포트 번호</span><span class="sxs-lookup"><span data-stu-id="f7097-118">Port number</span></span> | <span data-ttu-id="f7097-119">사용 방법</span><span class="sxs-lookup"><span data-stu-id="f7097-119">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="f7097-120">80</span><span class="sxs-lookup"><span data-stu-id="f7097-120">80</span></span> | <span data-ttu-id="f7097-121">SSL 인증서의 유효성을 검사하는 동안 CRL(인증서 해지 목록) 다운로드</span><span class="sxs-lookup"><span data-stu-id="f7097-121">Downloading certificate revocation lists (CRLs) while validating the SSL certificate</span></span> |
   | <span data-ttu-id="f7097-122">443</span><span class="sxs-lookup"><span data-stu-id="f7097-122">443</span></span> | <span data-ttu-id="f7097-123">응용 프로그램 프록시 서비스와의 모든 아웃바운드 통신</span><span class="sxs-lookup"><span data-stu-id="f7097-123">All outbound communication with the Application Proxy service</span></span> |

   <span data-ttu-id="f7097-124">방화벽이 원래 사용자에 따라 트래픽에 적용되는 경우 네트워크 서비스로 실행하는 Windows 서비스의 트래픽에 대해 이러한 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-124">If your firewall enforces traffic according to originating users, open these ports for traffic from Windows services that run as a Network Service.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f7097-125">표에는 커넥터 버전 1.5.132.0 이상에 대한 포트 요구 사항이 반영되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-125">The table reflects the port requirements for connector versions 1.5.132.0 and newer.</span></span> <span data-ttu-id="f7097-126">이전 커넥터 버전이 아직도 있는 경우 80 및 443 외에 5671, 8080, 9090-9091, 9350, 9352, 10100–10120 포트를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-126">If you still have an older connector version, you also need to enable the following ports in addition to 80 and 443: 5671, 8080, 9090-9091, 9350, 9352, 10100–10120.</span></span>
   >
   ><span data-ttu-id="f7097-127">커넥터를 최신 버전으로 업데이트하는 방법에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md#automatic-updates)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7097-127">For information about updating your connectors to the newest version, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md#automatic-updates).</span></span>

2. <span data-ttu-id="f7097-128">방화벽이나 프록시에서 DNS 허용 목록을 허용하면 msappproxy.net 및 servicebus.windows.net에 대한 연결을 허용 목록에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-128">If your firewall or proxy allows DNS whitelisting, you can whitelist connections to msappproxy.net and servicebus.windows.net.</span></span> <span data-ttu-id="f7097-129">그렇지 않으면 매주 업데이트되는 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)에 액세스하도록 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-129">If not, you need to allow access to the [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated each week.</span></span>

3. <span data-ttu-id="f7097-130">Microsoft는 4개의 주소를 사용하여 인증서를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-130">Microsoft uses four addresses to verify certificates.</span></span> <span data-ttu-id="f7097-131">다른 제품에 대해 이 작업을 수행하지 않은 경우 다음 URL에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-131">Allow access to the following URLs if you haven't done so for other products:</span></span>
   * <span data-ttu-id="f7097-132">mscrl.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="f7097-132">mscrl.microsoft.com:80</span></span>
   * <span data-ttu-id="f7097-133">crl.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="f7097-133">crl.microsoft.com:80</span></span>
   * <span data-ttu-id="f7097-134">ocsp.msocsp.com:80</span><span class="sxs-lookup"><span data-stu-id="f7097-134">ocsp.msocsp.com:80</span></span>
   * <span data-ttu-id="f7097-135">www.microsoft.com:80</span><span class="sxs-lookup"><span data-stu-id="f7097-135">www.microsoft.com:80</span></span>

4. <span data-ttu-id="f7097-136">커넥터는 등록 프로세스에 대한 login.windows.net 및 login.microsoftonline.net에 대한 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-136">Your connector needs access to login.windows.net and login.microsoftonline.net for the registration process.</span></span>

5. <span data-ttu-id="f7097-137">[Azure AD 응용 프로그램 프록시 커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/)를 사용하여 커넥터가 응용 프로그램 프록시 서비스에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-137">Use the [Azure AD Application Proxy Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) to verify that your connector can reach the Application Proxy service.</span></span> <span data-ttu-id="f7097-138">최소한 미국 중부 하위 지역 및 사용자에게 가까운 지역에는 모두 녹색 확인 표시가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-138">At a minimum, make sure that the Central US region and the region closest to you have all green checkmarks.</span></span> <span data-ttu-id="f7097-139">그 외의 항목에도 녹색 확인 표시가 있으면 복원력이 더 뛰어난 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-139">Beyond that, more green checkmarks means greater resiliency.</span></span>

## <a name="install-and-register-a-connector"></a><span data-ttu-id="f7097-140">커넥터 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="f7097-140">Install and register a connector</span></span>
1. <span data-ttu-id="f7097-141">[Azure Portal](https://portal.azure.com/)에서 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-141">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f7097-142">현재 디렉터리가 오른쪽 위 구석의 사용자 이름을 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-142">Your current directory appears under your username in the top right corner.</span></span> <span data-ttu-id="f7097-143">디렉터리를 변경해야 하는 경우 해당 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-143">If you need to change directories, select that icon.</span></span>
3. <span data-ttu-id="f7097-144">**Azure Active Directory** > **응용 프로그램 프록시**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-144">Go to **Azure Active Directory** > **Application Proxy**.</span></span>

   ![응용 프로그램 프록시로 이동](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. <span data-ttu-id="f7097-146">**커넥터 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-146">Select **Download Connector**.</span></span>

   ![커넥터 다운로드](./media/active-directory-application-proxy-enable/download_connector.png)

5. <span data-ttu-id="f7097-148">필수 구성 요소에 따라 준비한 서버에서 **AADApplicationProxyConnectorInstaller.exe** 를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-148">Run **AADApplicationProxyConnectorInstaller.exe** on the server you prepared according to the prerequisites.</span></span>
6. <span data-ttu-id="f7097-149">마법사의 지침에 따라 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-149">Follow the instructions in the wizard to install.</span></span> <span data-ttu-id="f7097-150">설치하는 동안 Azure AD 테넌트의 응용 프로그램 프록시를 사용하여 커넥터를 등록하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-150">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD tenant.</span></span>

   * <span data-ttu-id="f7097-151">Azure AD 전역 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-151">Provide your Azure AD global administrator credentials.</span></span> <span data-ttu-id="f7097-152">전역 관리자 테넌트는 Microsoft Azure 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-152">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
   * <span data-ttu-id="f7097-153">커넥터를 등록하는 관리자가 응용 프로그램 프록시 서비스를 사용할 수 있는 동일한 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-153">Make sure the admin who registers the connector is in the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="f7097-154">예를 들어, 테넌트 도메인이 contoso.com이면 관리자는 admin@contoso.com 또는 해당 도메인에 있는 다른 별칭이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-154">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other alias on that domain.</span></span>
   * <span data-ttu-id="f7097-155">커넥터를 설치하는 서버에 **IE 보안 강화 구성**이 **켜기**로 설정되어 있으면 등록 화면이 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-155">If **IE Enhanced Security Configuration** is set to **On** on the server where you are installing the connector, you may not see the registration screen.</span></span> <span data-ttu-id="f7097-156">액세스하려면 오류 메시지의 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-156">To get access, follow the instructions in the error message.</span></span> <span data-ttu-id="f7097-157">Internet Explorer 보안 강화가 해제되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f7097-157">Make sure that Internet Explorer Enhanced Security is off.</span></span>

<span data-ttu-id="f7097-158">고가용성을 위해 커넥터를 두 개 이상 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-158">For high availability purposes, you should deploy at least two connectors.</span></span> <span data-ttu-id="f7097-159">각 커넥터는 별도로 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-159">Each connector must be registered separately.</span></span>

## <a name="test-that-the-connector-installed-correctly"></a><span data-ttu-id="f7097-160">커넥터가 제대로 설치되었는지 테스트</span><span class="sxs-lookup"><span data-stu-id="f7097-160">Test that the connector installed correctly</span></span>

<span data-ttu-id="f7097-161">Azure Portal 또는 서버에서 확인하여 새 커넥터가 올바르게 설치되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-161">You can confirm that a new connector installed correctly by checking for it in either the Azure portal or on your server.</span></span> 

<span data-ttu-id="f7097-162">Azure Portal에서 테넌트로 로그인하고 **Azure Active Directory** > **응용 프로그램 프록시**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-162">In the Azure portal, sign in to your tenant and navigate to **Azure Active Directory** > **Application Proxy**.</span></span> <span data-ttu-id="f7097-163">모든 커넥터 및 커넥터 그룹이 이 페이지에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-163">All of your connectors and connector groups appear on this page.</span></span> <span data-ttu-id="f7097-164">커넥터를 선택하여 해당 세부 정보를 보거나 다른 커넥터 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-164">Select a connector to see its details or move it into a different connector group.</span></span> 

<span data-ttu-id="f7097-165">서버에서 커넥터 및 커넥터 업데이터에 대한 활성 서비스 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-165">On your server, check the list of active services for the connector and the connector updater.</span></span> <span data-ttu-id="f7097-166">두 서비스는 즉시 실행을 시작해야 하지만 그렇지 않은 경우 이 기능을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-166">The two services should start running immediately, but if not, turn them on:</span></span> 

   * <span data-ttu-id="f7097-167">**Microsoft AAD 응용 프로그램 프록시 커넥터** 에서 연결 사용</span><span class="sxs-lookup"><span data-stu-id="f7097-167">**Microsoft AAD Application Proxy Connector** enables connectivity</span></span>

   * <span data-ttu-id="f7097-168">**Microsoft AAD 응용 프로그램 프록시 커넥터 업데이터**는 자동화된 업데이트 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-168">**Microsoft AAD Application Proxy Connector Updater** is an automated update service.</span></span> <span data-ttu-id="f7097-169">업데이터에서 새 버전의 커넥터가 있는지 확인하고 필요에 따라 커넥터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-169">The updater checks for new versions of the connector and updates the connector as needed.</span></span>

   ![앱 프록시 커넥터 서비스 - 스크린샷](./media/active-directory-application-proxy-enable/app_proxy_services.png)

<span data-ttu-id="f7097-171">커넥터에 대한 정보 및 최신 상태로 유지하는 방법은 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7097-171">For information about connectors and how they stay up to date, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7097-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7097-172">Next steps</span></span>
<span data-ttu-id="f7097-173">이제 [응용 프로그램 프록시를 사용하여 응용 프로그램을 게시](application-proxy-publish-azure-portal.md)할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-173">You are now ready to [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

<span data-ttu-id="f7097-174">별도 네트워크 또는 다른 위치에 응용 프로그램이 있는 경우 다른 커넥터 그룹을 사용하여 커넥터를 논리 단위로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-174">If you have applications that are on separate networks or different locations, use connector groups to organize the different connectors into logical units.</span></span> <span data-ttu-id="f7097-175">[응용 프로그램 프록시 커넥터 작업](active-directory-application-proxy-connectors-azure-portal.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7097-175">Learn more about [Working with Application Proxy connectors](active-directory-application-proxy-connectors-azure-portal.md).</span></span>
