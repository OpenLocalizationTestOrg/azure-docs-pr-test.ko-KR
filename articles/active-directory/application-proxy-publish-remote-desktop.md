---
title: "Azure AD 앱 프록시를 사용하여 원격 데스크톱 게시 | Microsoft 문서"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대한 기본 사항을 제공합니다."
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
ms.openlocfilehash: 785bb4f893cf6861ef3b090d99780fd9b6b08c0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a><span data-ttu-id="9b31e-103">Azure AD 응용 프로그램 프록시를 사용하여 원격 데스크톱 게시</span><span class="sxs-lookup"><span data-stu-id="9b31e-103">Publish Remote Desktop with Azure AD Application Proxy</span></span>

<span data-ttu-id="9b31e-104">이 문서에서는 원격 사용자가 생산성을 높일 수 있도록 응용 프로그램 프록시를 사용하여 RDS(원격 데스크톱 서비스)를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-104">This article covers how to deploy Remote Desktop Services (RDS) with Application Proxy so that remote users can still be productive.</span></span>

<span data-ttu-id="9b31e-105">이 문서의 대상은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-105">The intended audience for this article is:</span></span>
- <span data-ttu-id="9b31e-106">원격 데스크톱 서비스를 통해 온-프레미스 응용 프로그램을 게시하여 최종 사용자에게 더 많은 응용 프로그램을 제공하려고 하는 현재 Azure AD 응용 프로그램 프록시 고객.</span><span class="sxs-lookup"><span data-stu-id="9b31e-106">Current Azure AD Application Proxy customers who want to offer more applications to their end users by publishing on-premises applications through Remote Desktop Services.</span></span>
- <span data-ttu-id="9b31e-107">Azure AD 응용 프로그램 프록시를 사용하여 배포의 공격에 대한 취약성을 줄이려고 하는 현재 원격 데스크톱 서비스 고객.</span><span class="sxs-lookup"><span data-stu-id="9b31e-107">Current Remote Desktop Services customers who want to reduce the attack surface of their deployment by using Azure AD Application Proxy.</span></span> <span data-ttu-id="9b31e-108">이 시나리오에서는 RDS에 대한 제한된 2단계 확인 및 조건부 액세스 제어 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-108">This scenario gives a limited set of two-step verification and conditional access controls to RDS.</span></span>

## <a name="how-application-proxy-fits-in-the-standard-rds-deployment"></a><span data-ttu-id="9b31e-109">응용 프로그램 프록시를 표준 RDS 배포에 맞추는 방법</span><span class="sxs-lookup"><span data-stu-id="9b31e-109">How Application Proxy fits in the standard RDS deployment</span></span>

<span data-ttu-id="9b31e-110">표준 RDS 배포에는 Windows Server에서 실행되는 다양한 원격 데스크톱 역할 서비스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-110">A standard RDS deployment includes various Remote Desktop role services running on Windows Server.</span></span> <span data-ttu-id="9b31e-111">[Remote Desktop Services architecture](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture)(원격 데스크톱 서비스 아키텍처)에는 다양한 배포 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-111">Looking at the [Remote Desktop Services architecture](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), there are multiple deployment options.</span></span> <span data-ttu-id="9b31e-112">[RDS deployment with Azure AD Application Proxy](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture)(Azure AD 응용 프로그램 프록시를 사용한 RDS 배포)와 기타 배포 옵션 간의 가장 눈에 띄는 차이점은 응용 프로그램 프록시 시나리오에는 커넥터 서비스를 실행하는 서버에서 영구 아웃바운드 연결이 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-112">The most noticeable difference between the [RDS deployment with Azure AD Application Proxy](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (shown in the following diagram) and the other deployment options is that the Application Proxy scenario has a permanent outbound connection from the server running the connector service.</span></span> <span data-ttu-id="9b31e-113">기타 배포에서는 부하 분산 장치를 통해 열린 인바운드 연결을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-113">Other deployments leave open inbound connections through a load balancer.</span></span>

![응용 프로그램 프록시는 RDS VM과 공용 인터넷 간에 놓입니다.](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

<span data-ttu-id="9b31e-115">RDS 배포에서 RD 웹 역할 및 RD 게이트웨이 역할은 인터넷 연결 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-115">In an RDS deployment, the RD Web role and the RD Gateway role run on Internet-facing machines.</span></span> <span data-ttu-id="9b31e-116">이러한 끝점은 다음 이유로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-116">These endpoints are exposed for the following reasons:</span></span>
- <span data-ttu-id="9b31e-117">RD 웹에서는 사용자에게 액세스할 수 있는 다양한 온-프레미스 응용 프로그램 및 데스크톱에 로그인하고 이를 볼 수 있는 공용 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-117">RD Web provides the user a public endpoint to sign in and view the various on-premises applications and desktops they can access.</span></span> <span data-ttu-id="9b31e-118">리소스 선택 시 OS에서 네이티브 앱을 사용하여 RDP 연결이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-118">Upon selecting a resource, an RDP connection is created using the native app on the OS.</span></span>
- <span data-ttu-id="9b31e-119">사용자가 RDP 연결을 시작하면 RD 게이트웨이가 중요해집니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-119">RD Gateway comes into the picture once a user launches the RDP connection.</span></span> <span data-ttu-id="9b31e-120">RD 게이트웨이는 인터넷을 통해 나오는 암호화된 RDP 트래픽을 처리하고 사용자가 연결되어 있는 온-프레미스 서버로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-120">The RD Gateway handles the encrypted RDP traffic coming over the Internet and translates it to the on-premises server that the user is connecting to.</span></span> <span data-ttu-id="9b31e-121">이 시나리오에서 RD 게이트웨이가 수신하는 트래픽은 Azure AD 응용 프로그램 프록시에서 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-121">In this scenario, the traffic the RD Gateway is receiving comes from the Azure AD Application Proxy.</span></span>

>[!TIP]
><span data-ttu-id="9b31e-122">이전에 RDS를 배포하지 않았거나 시작하기 전에 추가 정보가 필요한 경우 [seamlessly deploy RDS with Azure Resource Manager and Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)(Azure Resource Manager 및 Azure Marketplace를 사용하여 원활하게 RDS 배포)를 수행하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="9b31e-122">If you haven't deployed RDS before, or want more information before you begin, learn how to [seamlessly deploy RDS with Azure Resource Manager and Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).</span></span>

## <a name="requirements"></a><span data-ttu-id="9b31e-123">요구 사항</span><span class="sxs-lookup"><span data-stu-id="9b31e-123">Requirements</span></span>

- <span data-ttu-id="9b31e-124">RD 웹 및 RD 게이트웨이 끝점은 둘 다 같은 컴퓨터에 있고 공통 루트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-124">Both the RD Web and RD Gateway endpoints must be located on the same machine, and with a common root.</span></span> <span data-ttu-id="9b31e-125">RD 웹 및 RD 게이트웨이는 단일 응용 프로그램으로 게시되므로 두 응용 프로그램 간에 Single Sign-On 환경이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-125">RD Web and RD Gateway will be published as a single application so you can have a single sign-on experience between the two applications.</span></span>

- <span data-ttu-id="9b31e-126">이미 [RDS를 배포](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)하고 [응용 프로그램 프록시를 사용하도록 설정](active-directory-application-proxy-enable.md)했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-126">You should already have [deployed RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure), and [enabled Application Proxy](active-directory-application-proxy-enable.md).</span></span>

- <span data-ttu-id="9b31e-127">이 시나리오에서는 최종 사용자가 RD 웹 페이지를 통해 연결하는 Windows 7 또는 Windows 10 데스크톱에서 Internet Explorer를 수행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-127">This scenario assumes that your end users go through Internet Explorer on Windows 7 or Windows 10 desktops that connect through the RD Web page.</span></span> <span data-ttu-id="9b31e-128">다른 운영 체제를 지원해야 하는 경우 [다른 클라이언트 구성 지원](#support-for-other-client-configurations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b31e-128">If you need to support other operating systems, see [Support for other client configurations](#support-for-other-client-configurations).</span></span>

  >[!NOTE]
  ><span data-ttu-id="9b31e-129">Windows 10 Creator's Update는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-129">Windows 10 Creator's Update is not currently supported.</span></span>

- <span data-ttu-id="9b31e-130">Internet Explorer에서 RDS ActiveX 추가 기능을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-130">On Internet Explorer, enable the RDS ActiveX add-on.</span></span>

## <a name="deploy-the-joint-rds-and-application-proxy-scenario"></a><span data-ttu-id="9b31e-131">공동 RDS 및 응용 프로그램 프록시 시나리오 배포</span><span class="sxs-lookup"><span data-stu-id="9b31e-131">Deploy the joint RDS and Application Proxy scenario</span></span>

<span data-ttu-id="9b31e-132">환경에 대해 RDS 및 Azure AD 응용 프로그램 프록시를 설정한 후 두 가지 솔루션을 결합하는 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-132">After setting up RDS and Azure AD Application Proxy for your environment, follow the steps to combine the two solutions.</span></span> <span data-ttu-id="9b31e-133">이러한 단계에서는 두 개의 웹 연결 RDS 끝점(RD 웹 및 RD 게이트웨이)을 응용 프로그램으로 게시하고 나서 응용 프로그램 프록시를 통과하도록 RDS의 트래픽을 전달하는 작업을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-133">These steps walk through publishing the two web-facing RDS endpoints (RD Web and RD Gateway) as applications, and then directing traffic on your RDS to go through Application Proxy.</span></span>

### <a name="publish-the-rd-host-endpoint"></a><span data-ttu-id="9b31e-134">RD 호스트 끝점 게시</span><span class="sxs-lookup"><span data-stu-id="9b31e-134">Publish the RD host endpoint</span></span>

1. <span data-ttu-id="9b31e-135">다음 값을 사용하여 [새 응용 프로그램 프록시 응용 프로그램을 게시](application-proxy-publish-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-135">[Publish a new Application Proxy application](application-proxy-publish-azure-portal.md) with the following values:</span></span>
   - <span data-ttu-id="9b31e-136">내부 URL: https://\<rdhost\>.com/, 여기서 \<rdhost\>는 RD 웹 및 RD 게이트웨이에서 공유하는 공통 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-136">Internal URL: https://\<rdhost\>.com/, where \<rdhost\> is the common root that RD Web and RD Gateway share.</span></span>
   - <span data-ttu-id="9b31e-137">외부 URL: 이 필드는 응용 프로그램 이름에 따라 자동으로 채워지지만 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-137">External URL: This field is automatically populated based on the name of the application, but you can modify it.</span></span> <span data-ttu-id="9b31e-138">사용자는 RDS에 액세스하면 이 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-138">Your users will go to this URL when they access RDS.</span></span>
   - <span data-ttu-id="9b31e-139">사전 인증 방법: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b31e-139">Preauthentication method: Azure Active Directory</span></span>
   - <span data-ttu-id="9b31e-140">URL 헤더 변환: 아니요</span><span class="sxs-lookup"><span data-stu-id="9b31e-140">Translate URL headers: No</span></span>
2. <span data-ttu-id="9b31e-141">게시된 RD 응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-141">Assign users to the published RD application.</span></span> <span data-ttu-id="9b31e-142">모든 사용자가 RDS에도 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-142">Make sure they all have access to RDS, too.</span></span>
3. <span data-ttu-id="9b31e-143">응용 프로그램에 대한 Single Sign-On 방법을 **Azure AD Single Sign-On 사용 안 함**으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-143">Leave the single sign-on method for the application as **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="9b31e-144">사용자에게는 Azure AD 및 RD 웹에 대해 한 번씩 인증하도록 요청되지만 RD 게이트웨이에 대한 Single Sign-On이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-144">Your users are asked to authenticate once to Azure AD and once to RD Web, but have single sign-on to RD Gateway.</span></span>
4. <span data-ttu-id="9b31e-145">**Azure Active Directory** > **앱 등록** > *응용 프로그램* > **설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-145">Go to **Azure Active Directory** > **App Registrations** > *Your application* > **Settings**.</span></span>
5. <span data-ttu-id="9b31e-146">**속성**을 선택하고 **홈페이지 URL** 필드를 업데이트하여 RD 웹 끝점(예: https://\<rdhost\>.com/RDWeb)을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-146">Select **Properties** and update the **Home-page URL** field to point to your RD Web endpoint (like https://\<rdhost\>.com/RDWeb).</span></span>

### <a name="direct-rds-traffic-to-application-proxy"></a><span data-ttu-id="9b31e-147">응용 프로그램 프록시에 대한 직접 RDS 트래픽</span><span class="sxs-lookup"><span data-stu-id="9b31e-147">Direct RDS traffic to Application Proxy</span></span>

<span data-ttu-id="9b31e-148">관리자로 RDS 배포에 연결하고 배포에 대한 RD 게이트웨이 서버 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-148">Connect to the RDS deployment as an administrator and change the RD Gateway server name for the deployment.</span></span> <span data-ttu-id="9b31e-149">이렇게 하면 연결이 Azure AD 응용 프로그램 프록시를 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-149">This ensures that connections go through the Azure AD Application Proxy.</span></span>

1. <span data-ttu-id="9b31e-150">RD 연결 브로커 역할을 실행하는 RDS 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-150">Connect to the RDS server running the RD Connection Broker role.</span></span>
2. <span data-ttu-id="9b31e-151">**서버 관리자**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-151">Launch **Server Manager**.</span></span>
3. <span data-ttu-id="9b31e-152">왼쪽 창에서 **원격 데스크톱 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-152">Select **Remote Desktop Services** from the pane on the left.</span></span>
4. <span data-ttu-id="9b31e-153">**개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-153">Select **Overview**.</span></span>
5. <span data-ttu-id="9b31e-154">배포 개요 섹션에서 드롭다운 메뉴를 선택하고 **배포 속성 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-154">In the Deployment Overview section, select the drop-down menu and choose **Edit deployment properties**.</span></span>
6. <span data-ttu-id="9b31e-155">[RD 게이트웨이] 탭에서 **서버 이름** 필드를 응용 프로그램 프록시에서 RD 호스트 끝점에 대해 설정한 외부 URL로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-155">In the RD Gateway tab, change the **Server name** field to the External URL that you set for the RD host endpoint in Application Proxy.</span></span>
7. <span data-ttu-id="9b31e-156">**로그온 방법** 필드를 **암호 인증**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-156">Change the **Logon method** field to **Password Authentication**.</span></span>

  ![RDS의 배포 속성 화면](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. <span data-ttu-id="9b31e-158">각 컬렉션에 대해 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-158">For each collection, run the following command.</span></span> <span data-ttu-id="9b31e-159">*\<yourcollectionname\>* 및 *\<proxyfrontendurl\>*을 사용자 고유의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-159">Replace *\<yourcollectionname\>* and *\<proxyfrontendurl\>* with your own information.</span></span> <span data-ttu-id="9b31e-160">이 명령은 RD 웹과 RD 게이트웨이 간에 Single Sign-On을 사용하도록 설정하고 성능을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-160">This command enables single sign-on between RD Web and RD Gateway, and optimizes performance:</span></span>

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   <span data-ttu-id="9b31e-161">**예:**</span><span class="sxs-lookup"><span data-stu-id="9b31e-161">**For example:**</span></span>
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. <span data-ttu-id="9b31e-162">이 컬렉션의 RDWeb에서 다운로드할 RDP 파일 콘텐츠를 보고 사용자 지정 RDP 속성의 수정 내용을 확인하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-162">To verify the modification of the custom RDP properties as well as view the RDP file contents that will be downloaded from RDWeb for this collection, run the following command:</span></span>
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

<span data-ttu-id="9b31e-163">이제 원격 데스크톱을 구성했으므로 Azure AD 응용 프로그램 프록시가 RDS의 인터넷 연결 구성 요소로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-163">Now that you've configured Remote Desktop, Azure AD Application Proxy has taken over as the internet-facing component of RDS.</span></span> <span data-ttu-id="9b31e-164">RD 웹 및 RD 게이트웨이 끝점에서 다른 공용 인터넷 연결 끝점을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-164">You can remove the other public internet-facing endpoints on your RD Web and RD Gateway machines.</span></span>

## <a name="test-the-scenario"></a><span data-ttu-id="9b31e-165">시나리오 테스트</span><span class="sxs-lookup"><span data-stu-id="9b31e-165">Test the scenario</span></span>

<span data-ttu-id="9b31e-166">Windows 7 또는 10 컴퓨터에서 Internet Explorer를 사용하여 시나리오를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-166">Test the scenario with Internet Explorer on a Windows 7 or 10 computer.</span></span>

1. <span data-ttu-id="9b31e-167">설정한 외부 URL로 이동하거나 [MyApps](https://myapps.microsoft.com) 패널에서 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-167">Go to the external URL you set up, or find your application in the [MyApps panel](https://myapps.microsoft.com).</span></span>
2. <span data-ttu-id="9b31e-168">Azure Active Directory에 대해 인증할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-168">You are asked to authenticate to Azure Active Directory.</span></span> <span data-ttu-id="9b31e-169">응용 프로그램에 할당한 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-169">Use an account that you assigned to the application.</span></span>
3. <span data-ttu-id="9b31e-170">RD 웹에 대해 인증할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-170">You are asked to authenticate to RD Web.</span></span>
4. <span data-ttu-id="9b31e-171">RDS 인증이 성공하면 원하는 데스크톱 또는 응용 프로그램을 선택하고 작동을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-171">Once your RDS authentication succeeds, you can select the desktop or application you want, and start working.</span></span>

## <a name="support-for-other-client-configurations"></a><span data-ttu-id="9b31e-172">다른 클라이언트 구성에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="9b31e-172">Support for other client configurations</span></span>

<span data-ttu-id="9b31e-173">이 문서에 요약된 구성은 Internet Explorer와 RDS ActiveX 추가 기능을 사용하는 Windows 7 또는 10 사용자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-173">The configuration outlined in this article is for users on Windows 7 or 10, with Internet Explorer plus the RDS ActiveX add-on.</span></span> <span data-ttu-id="9b31e-174">그러나 필요한 경우 다른 운영 체제 또는 브라우저를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-174">If you need to, however, you can support other operating systems or browsers.</span></span> <span data-ttu-id="9b31e-175">차이점은 사용하는 인증 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-175">The difference is in the authentication method that you use.</span></span>

| <span data-ttu-id="9b31e-176">인증 방법</span><span class="sxs-lookup"><span data-stu-id="9b31e-176">Authentication method</span></span> | <span data-ttu-id="9b31e-177">지원되는 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="9b31e-177">Supported client configuration</span></span> |
| --------------------- | ------------------------------ |
| <span data-ttu-id="9b31e-178">사전 인증</span><span class="sxs-lookup"><span data-stu-id="9b31e-178">Pre-authentication</span></span>    | <span data-ttu-id="9b31e-179">Internet Explorer + RDS ActiveX 추가 기능을 사용하는 Windows 7/10</span><span class="sxs-lookup"><span data-stu-id="9b31e-179">Windows 7/10 using Internet Explorer + RDS ActiveX add-on</span></span> |
| <span data-ttu-id="9b31e-180">통과</span><span class="sxs-lookup"><span data-stu-id="9b31e-180">Passthrough</span></span> | <span data-ttu-id="9b31e-181">Microsoft 원격 데스크톱 응용 프로그램을 지원하는 다른 운영 체제</span><span class="sxs-lookup"><span data-stu-id="9b31e-181">Any other operating system that supports the Microsoft Remote Desktop application</span></span> |

<span data-ttu-id="9b31e-182">사전 인증 흐름은 통과 흐름보다 더 많은 보안 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-182">The pre-authentication flow offers more security benefits than the passthrough flow.</span></span> <span data-ttu-id="9b31e-183">사전 인증을 사용하면 온-프레미스 리소스에 대해 Single Sign-On, 조건부 액세스 및 2단계 인증과 같은 Azure AD 인증 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-183">With pre-authentication you can leverage Azure AD authentication features like single sign-on, conditional access, and two-step verification for your on-premises resources.</span></span> <span data-ttu-id="9b31e-184">또한 인증된 트래픽만 네트워크에 도달하도록합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-184">You also ensure that only authenticated traffic reaches your network.</span></span>

<span data-ttu-id="9b31e-185">통과 인증을 사용하려면 이 문서에 나열된 단계를 두 번만 수정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-185">To use passthrough authentication, there are just two modifications to the steps listed in this article:</span></span>
1. <span data-ttu-id="9b31e-186">[RD 호스트 끝점 게시](#publish-the-rd-host-endpoint)의 1단계에서 사전 인증 방법을 **통과**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-186">In [Publish the RD host endpoint](#publish-the-rd-host-endpoint) step 1, set the Preauthentication method to **Passthrough**.</span></span>
2. <span data-ttu-id="9b31e-187">[응용 프로그램 프록시에 대한 직접 RDS 트래픽](#direct-rds-traffic-to-application-proxy)에서 8단계 전체를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="9b31e-187">In [Direct RDS traffic to Application Proxy](#direct-rds-traffic-to-application-proxy), skip step 8 entirely.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b31e-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b31e-188">Next steps</span></span>

[<span data-ttu-id="9b31e-189">Azure AD 응용 프로그램 프록시를 사용하여 SharePoint에 원격 액세스 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9b31e-189">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)  
[<span data-ttu-id="9b31e-190">Azure AD 응용 프로그램 프록시를 사용하여 앱에 원격으로 액세스하는 경우 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="9b31e-190">Security considerations for accessing apps remotely by using Azure AD Application Proxy</span></span>](application-proxy-security-considerations.md)
