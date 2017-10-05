---
title: "Azure AD 응용 프로그램 프록시를 통해 SharePoint에 원격 액세스를 사용하도록 설정 | Microsoft 문서"
description: "온-프레미스 SharePoint 서버를 Azure AD 응용 프로그램 프록시과 통합하는 방법에 대한 기본 사항을 다룹니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 97eeec3b3936bcbef6ac3966b890332901bcb153
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="7c85f-103">Azure AD 응용 프로그램 프록시를 통해 SharePoint에 원격 액세스를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7c85f-103">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="7c85f-104">이 문서에서는 온-프레미스 SharePoint 서버를 Azure AD(Azure Active Directory) 응용 프로그램 프록시와 통합하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="7c85f-105">Azure AD 응용 프로그램 프록시를 통해 SharePoint에 원격 액세스를 사용하도록 설정하려면 단계별로 이 문서의 섹션을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c85f-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7c85f-106">Prerequisites</span></span>

<span data-ttu-id="7c85f-107">이 문서에서는 사용자 환경에 SharePoint 2013 이상이 이미 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span></span> <span data-ttu-id="7c85f-108">또한 다음 필수 조건도 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="7c85f-108">In addition, consider the following prerequisites:</span></span>

* <span data-ttu-id="7c85f-109">SharePoint에는 기본 Kerberos 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-109">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="7c85f-110">따라서 Azure AD 응용 프로그램 프록시를 통해 원격으로 내부 사이트에 액세스하는 사용자는 SSO(Single Sign-On) 환경을 사용한다고 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="7c85f-111">SharePoint 서버에 대한 몇 가지 구성을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-111">You need to make a few configuration changes to your SharePoint server.</span></span> <span data-ttu-id="7c85f-112">스테이징 환경을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-112">We recommend using a staging environment.</span></span> <span data-ttu-id="7c85f-113">이 방법에서는 스테이징 서버로 먼저 업데이트할 수 있으므로 프로덕션으로 전환하기 전에 테스트 주기를 용이하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-113">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="7c85f-114">게시된 URL에 SSL이 필요하므로 SharePoint용 SSL을 이미 설정했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-114">We assume that you have already set up SSL for SharePoint, because we require SSL on the published URL.</span></span> <span data-ttu-id="7c85f-115">내부 사이트에는 SSL을 사용하도록 설정하여 해당 링크가 적절히 전송/매핑되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-115">You need to have SSL enabled on your internal site, to ensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="7c85f-116">SSL을 구성하지 않은 경우 지침에 대해서는 [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013)(SharePoint 2013용 SSL 구성)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c85f-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="7c85f-117">또한 커넥터 컴퓨터는 사용자가 발급한 인증서를 신뢰해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-117">Also, make sure that the connector machine trusts the certificate that you issue.</span></span> <span data-ttu-id="7c85f-118">인증서는 공개적으로 발급될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-118">(The certificate does not need to be publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a><span data-ttu-id="7c85f-119">1단계: SharePoint에 대한 Single Sign-On 설정</span><span class="sxs-lookup"><span data-stu-id="7c85f-119">Step 1: Set up single sign-on to SharePoint</span></span>

<span data-ttu-id="7c85f-120">고객은 백 엔드 응용 프로그램(이 경우 SharePoint 서버)에 대한 최상의 SSO 환경을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-120">Our customers want the best SSO experience for their back-end applications, SharePoint server in this case.</span></span> <span data-ttu-id="7c85f-121">일반적인 Azure AD 시나리오에서, 다시 인증하라는 메시지가 표시되지 않으므로 사용자는 한 번만 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-121">In this common Azure AD scenario, the user is authenticated only once, because they will not be prompted for authentication again.</span></span>

<span data-ttu-id="7c85f-122">Windows 인증을 사용하거나 필요로 하는 온-프레미스 응용 프로그램에 대해 Kerberos 인증 프로토콜 및 KCD(Kerberos 제한 위임)라는 기능을 사용하여 SSO를 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-122">For on-premises applications that require or use Windows authentication, you can achieve SSO by using the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="7c85f-123">KCD(구성된 경우)를 통해 응용 프로그램 프록시 커넥터는 사용자가 Windows에 직접 로그인하지 않더라도 사용자에 대한 windows 티켓/토큰을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-123">KCD, when configured, allows the Application Proxy connector to obtain a windows ticket/token for a user, even if the user hasn’t signed in to Windows directly.</span></span> <span data-ttu-id="7c85f-124">KCD에 대한 자세한 내용은 [Kerberos 제한 위임 개요](https://technet.microsoft.com/library/jj553400.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c85f-124">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="7c85f-125">SharePoint 서버에 대해 KCD를 설정하려면 다음에 나오는 순차 섹션의 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-125">To set up KCD for a SharePoint server, use the procedures in the following sequential sections:</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="7c85f-126">SharePoint가 서비스 계정으로 실행 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="7c85f-126">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="7c85f-127">먼저 SharePoint가 로컬 시스템, 로컬 서비스 또는 네트워크 서비스가 아닌 정의된 서비스 계정으로 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-127">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="7c85f-128">SPN(서비스 사용자 이름)을 유효한 계정에 연결하려면 이 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-128">Do this so that you can attach service principal names (SPNs) to a valid account.</span></span> <span data-ttu-id="7c85f-129">SPN은 Kerberos 프로토콜이 서로 다른 서비스를 식별하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-129">SPNs are how the Kerberos protocol identifies different services.</span></span> <span data-ttu-id="7c85f-130">나중에 KCD를 구성하려면 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-130">And you will need the account later to configure the KCD.</span></span>

<span data-ttu-id="7c85f-131">사이트가 정의된 서비스 계정으로 실행되는지 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-131">To ensure that your sites are running under a defined service account, perform the following steps:</span></span>

1. <span data-ttu-id="7c85f-132">**SharePoint 2013 중앙 관리** 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-132">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="7c85f-133">**보안**으로 이동하고 **서비스 계정 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-133">Go to **Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="7c85f-134">**웹 응용 프로그램 풀 – SharePoint – 80**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-134">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="7c85f-135">옵션은 기본적으로 웹 풀에서 SSL을 사용하는 경우 또는 웹 풀의 이름에 따라 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-135">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span></span>

  ![서비스 계정 구성 옵션](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. <span data-ttu-id="7c85f-137">**이 구성 요소에 대한 계정을 선택하세요.**가 **로컬 서비스** 또는 **네트워크 서비스**인 경우 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-137">If **Select an account for this component** is **Local Service** or **Network Service**, you need to create an account.</span></span> <span data-ttu-id="7c85f-138">그렇지 않은 경우 작업이 끝났으며 다음 섹션으로 진행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-138">If not, you're finished and can move to the next section.</span></span>
5. <span data-ttu-id="7c85f-139">**새 관리되는 계정을 등록하세요.**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-139">Select **Register new managed account**.</span></span> <span data-ttu-id="7c85f-140">계정이 생성되면 계정을 사용하기 전에 **웹 응용 프로그램 풀**을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-140">After your account is created, you must set **Web Application Pool** before you can use the account.</span></span>

> [!NOTE]
<span data-ttu-id="7c85f-141">서비스에 대해 이전에 생성된 Azure AD 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-141">You need to have a previously created Azure AD account for the service.</span></span> <span data-ttu-id="7c85f-142">자동 암호 변경을 허용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-142">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="7c85f-143">전체 단계 집합 및 문제 해결에 대한 자세한 내용은 [SharePoint 2013에서 자동 암호 변경 구성](https://technet.microsoft.com/library/ff724280.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c85f-143">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="7c85f-144">Kerberos용 SharePoint 구성</span><span class="sxs-lookup"><span data-stu-id="7c85f-144">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="7c85f-145">SharePoint 서버에 대한 Single Sign-On을 수행하는 데 KCD를 사용하며 KCD는 Kerberos에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-145">You use KCD to perform single sign-on to the SharePoint server, and this works only with Kerberos.</span></span>

<span data-ttu-id="7c85f-146">Kerberos 인증을 위한 SharePoint 사이트를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="7c85f-146">To configure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="7c85f-147">**SharePoint 2013 중앙 관리** 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-147">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="7c85f-148">**응용 프로그램 관리**로 이동하고 **웹 응용 프로그램 관리**를 선택하고 SharePoint 사이트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-148">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="7c85f-149">이 예제에서는 **SharePoint – 80**입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-149">In this example, it is **SharePoint - 80**.</span></span>

  ![SharePoint 사이트 선택](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. <span data-ttu-id="7c85f-151">도구 모음에서 **인증 공급자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-151">Click **Authentication Providers** on the toolbar.</span></span>
4. <span data-ttu-id="7c85f-152">**인증 공급자** 상자에서 **기본 영역**을 클릭하여 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-152">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span></span>
5. <span data-ttu-id="7c85f-153">**인증 편집** 대화 상자에서 **클레임 인증 유형**이 표시될 때까지 아래로 스크롤하고 **Windows 인증 사용** 및 **Windows 통합 인증**이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-153">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="7c85f-154">드롭다운 상자에서 **협상(Kerberos)**이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-154">In the drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![인증 편집 대화 상자](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. <span data-ttu-id="7c85f-156">**인증 편집** 대화 상자 맨 아래에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-156">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a><span data-ttu-id="7c85f-157">SharePoint 서비스 계정에 대한 서비스 주체 이름 설정</span><span class="sxs-lookup"><span data-stu-id="7c85f-157">Set a service principal name for the SharePoint service account</span></span>

<span data-ttu-id="7c85f-158">KCD를 구성하기 전에 구성한 서비스 계정으로 실행 중인 SharePoint 서비스를 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-158">Before you configure the KCD, you need to identify the SharePoint service running as the service account that you've configured.</span></span> <span data-ttu-id="7c85f-159">SPN을 설정하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-159">You do this by setting an SPN.</span></span> <span data-ttu-id="7c85f-160">자세한 내용은 [서비스 주체 이름](https://technet.microsoft.com/library/cc961723.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c85f-160">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="7c85f-161">SPN 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-161">The SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="7c85f-162">SPN 형식에서:</span><span class="sxs-lookup"><span data-stu-id="7c85f-162">In the SPN format:</span></span>

* <span data-ttu-id="7c85f-163">_서비스 클래스_는 서비스의 고유한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-163">_service class_ is a unique name for the service.</span></span> <span data-ttu-id="7c85f-164">SharePoint의 경우 **HTTP**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-164">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="7c85f-165">_호스트_는 해당 서비스가 실행 중인 호스트의 정규화된 도메인 이름 또는 NetBIOS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-165">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span></span> <span data-ttu-id="7c85f-166">SharePoint 사이트의 경우 사용 중인 IIS 버전에 따라 이 텍스트는 사이트의 URL이어야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-166">For a SharePoint site, this text might need to be the URL of the site, depending on the version of IIS that you're using.</span></span>

* <span data-ttu-id="7c85f-167">_포트_는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-167">_port_ is optional.</span></span>

<span data-ttu-id="7c85f-168">SharePoint 서버에 대한 FQDN이 다음과 같은 경우:</span><span class="sxs-lookup"><span data-stu-id="7c85f-168">If the FQDN of the SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="7c85f-169">SPN은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-169">Then the SPN is:</span></span>

```
HTTP/ sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="7c85f-170">또한 서버에서 특정 사이트에 대한 SPN을 설정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-170">You might also need to set SPNs for specific sites on your server.</span></span> <span data-ttu-id="7c85f-171">자세한 내용은 [Kerberos 인증 구성(Office SharePoint Server)](https://technet.microsoft.com/library/cc263449(v=office.12).aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c85f-171">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="7c85f-172">"Kerberos 인증을 사용하여 웹 응용 프로그램에 대한 서비스 주체 이름 만들기" 섹션을 특히 주의하여 보세요.</span><span class="sxs-lookup"><span data-stu-id="7c85f-172">Pay close attention to the section "Create Service Principal Names for your Web applications using Kerberos authentication."</span></span>

<span data-ttu-id="7c85f-173">SPN을 설정하는 가장 쉬운 방법은 사이트에 이미 있는 SPN 형식을 따르는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-173">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="7c85f-174">서비스 계정에 대해 등록할 SPN을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-174">Copy those SPNs to register against the service account.</span></span> <span data-ttu-id="7c85f-175">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-175">To do this:</span></span>

1. <span data-ttu-id="7c85f-176">SPN으로 다른 컴퓨터에서 해당 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-176">Browse to the site with the SPN from another machine.</span></span>
 <span data-ttu-id="7c85f-177">이 작업을 수행하면 관련 Kerberos 티켓 집합이 컴퓨터에서 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-177">When you do, the relevant set of Kerberos tickets is cached on the machine.</span></span> <span data-ttu-id="7c85f-178">이러한 티켓에는 탐색할 대상 사이트의 SPN이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-178">These tickets contain the SPN of the target site that you browsed to.</span></span>

2. <span data-ttu-id="7c85f-179">[Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html)라는 도구를 사용하여 해당 사이트에 대한 SPN을 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-179">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="7c85f-180">브라우저에서 사이트에 액세스한 사용자와 같은 컨텍스트에서 실행 중인 명령 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-180">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span></span>
```
Klist
```
<span data-ttu-id="7c85f-181">그러면 Klist가 대상 SPN 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-181">Klist then returns the set of target SPNs.</span></span> <span data-ttu-id="7c85f-182">이 예제에서 강조 표시된 값은 필요한 SPN입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-182">In this example, the highlighted value is the SPN that's needed:</span></span>

  ![Klist 예제의 결과](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. <span data-ttu-id="7c85f-184">이제 SPN이 있으므로 이전에 웹 응용 프로그램에 대해 설정한 서비스 계정에서 SPN이 제대로 구성되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-184">Now that you have the SPN, you need to make sure that it's configured correctly on the service account that you set up for the web application earlier.</span></span> <span data-ttu-id="7c85f-185">명령 프롬프트에서 도메인 관리자로 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-185">Run the following command from the command prompt as an administrator of the domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="7c85f-186">이 명령은 _demo\sp_svc_로 실행 중인 SharePoint 서비스 계정에 대한 SPN을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-186">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="7c85f-187">_http/sharepoint.demo.o365identity.us_를 서버에 대한 SPN으로, _demo\sp_svc_를 사용자 환경의 서비스 계정으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-187">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span></span> <span data-ttu-id="7c85f-188">추가하기 전에 Setspn 명령으로 SPN을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-188">The Setspn command searches for the SPN before it adds it.</span></span> <span data-ttu-id="7c85f-189">이 경우 **중복된 SPN 값** 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-189">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="7c85f-190">이 오류가 표시되면 값이 해당 서비스 계정과 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-190">If you see this error, make sure that the value is associated with the service account.</span></span>

<span data-ttu-id="7c85f-191">-l 옵션과 함께 Setspn 명령을 실행하여 SPN이 추가되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-191">You can verify that the SPN was added by running the Setspn command with the -l option.</span></span> <span data-ttu-id="7c85f-192">이 명령에 대해 자세히 알아보려면 [Setspn](https://technet.microsoft.com/library/cc731241.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c85f-192">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a><span data-ttu-id="7c85f-193">커넥터가 SharePoint에 대한 신뢰할 수 있는 대리자로 설정되는지 확인</span><span class="sxs-lookup"><span data-stu-id="7c85f-193">Ensure that the connector is set as a trusted delegate to SharePoint</span></span>

<span data-ttu-id="7c85f-194">Azure AD 응용 프로그램 프록시 서비스가 사용자 ID를 SharePoint 서비스에 위임할 수 있도록 KCD를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-194">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span></span> <span data-ttu-id="7c85f-195">응용 프로그램 프록시 커넥터에서 Azure AD에서 인증된 사용자에 대한 Kerberos 티켓을 검색할 수 있도록 하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-195">You do this by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="7c85f-196">그런 다음 해당 서버에서 컨텍스트를 대상 응용 프로그램(이 경우 SharePoint)에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-196">Then that server passes the context to the target application, or SharePoint in this case.</span></span>

<span data-ttu-id="7c85f-197">KCD를 구성하려면 각 커넥터 컴퓨터에 대해 다음 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-197">To configure the KCD, repeat the following steps for each connector machine:</span></span>

1. <span data-ttu-id="7c85f-198">도메인 관리자로 DC에 로그인한 후 **Active Directory 사용자 및 컴퓨터**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-198">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="7c85f-199">커넥터가 실행 중인 컴퓨터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-199">Find the computer that the connector is running on.</span></span> <span data-ttu-id="7c85f-200">이 예제에서는 동일한 SharePoint 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-200">In this example, it's the same SharePoint server.</span></span>
3. <span data-ttu-id="7c85f-201">컴퓨터를 두 번 클릭한 후 **위임** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-201">Double-click the computer, and then click the **Delegation** tab.</span></span>
4. <span data-ttu-id="7c85f-202">위임 설정이 **지정된 서비스에 대한 위임용으로만 이 컴퓨터 트러스트**로 설정되어 있는지 확인하고 **모든 인증 프로토콜 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-202">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**, and then select **Use any authentication protocol**.</span></span>

  ![위임 설정](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. <span data-ttu-id="7c85f-204">**추가** 단추를 클릭한 후 **사용자 또는 컴퓨터**를 클릭하고 서비스 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-204">Click the **Add** button, click **Users or Computers**, and locate the service account.</span></span>

  ![서비스 계정에 대한 SPN 추가](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. <span data-ttu-id="7c85f-206">SPN 목록에서 서비스 계정에 대해 이전에 만든 SPN을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-206">In the list of SPNs, select the one that you created earlier for the service account.</span></span>
7. <span data-ttu-id="7c85f-207">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-207">Click **OK**.</span></span> <span data-ttu-id="7c85f-208">**확인**을 다시 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-208">Click **OK** again to save the changes.</span></span>

## <a name="step-2-enable-remote-access-to-sharepoint"></a><span data-ttu-id="7c85f-209">2단계: SharePoint에 원격 액세스를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7c85f-209">Step 2: Enable remote access to SharePoint</span></span>

<span data-ttu-id="7c85f-210">이제 Kerberos에 대해 SharePoint를 사용하도록 설정했고 KCD를 구성했으므로 SharePoint에 대해 Single Sign-On을 설정할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to set up single sign-on to SharePoint.</span></span> <span data-ttu-id="7c85f-211">그런 다음 커넥터에서 Azure AD 응용 프로그램 프록시를 통해 원격 액세스를 위한 SharePoint 팜을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-211">Then from the connector, you can publish the SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

<span data-ttu-id="7c85f-212">다음 단계를 수행하려면 조직의 Azure Active Directory 계정 내에서 전역 관리자 역할의 멤버여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-212">To perform the following steps, you need to be a member of the Global Administrator Role in your organization's Azure Active Directory account.</span></span>

1. <span data-ttu-id="7c85f-213">[Azure Portal](https://manage.windowsazure.com)에 로그인하고 Azure AD 테넌트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-213">Sign in to the [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span></span>
2. <span data-ttu-id="7c85f-214">**응용 프로그램**을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-214">Click **Applications**, and then click **Add**.</span></span>
3. <span data-ttu-id="7c85f-215">**네트워크 외부에서 액세스할 수 있는 응용 프로그램 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-215">Select **Publish an application that will be accessible from outside your network**.</span></span> <span data-ttu-id="7c85f-216">이 옵션이 표시되지 않으면 테넌트에 Azure AD Basic 또는 Premium이 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-216">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in the tenant.</span></span>
4. <span data-ttu-id="7c85f-217">다음과 같이 각 옵션을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-217">Complete each of the options as follows:</span></span>
 * <span data-ttu-id="7c85f-218">**이름**: 원하는 임의 값을 사용합니다(예: **SharePoint**)</span><span class="sxs-lookup"><span data-stu-id="7c85f-218">**Name**: Use any value that you want--for example, **SharePoint**.</span></span>
 * <span data-ttu-id="7c85f-219">**내부 URL**: SharePoint 사이트의 내부 URL입니다(예: **https://SharePoint/**).</span><span class="sxs-lookup"><span data-stu-id="7c85f-219">**Internal URL**: This is the URL of the SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="7c85f-220">이 예제에서는 **https**를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-220">In this example, make sure to use **https**.</span></span>
 * <span data-ttu-id="7c85f-221">**사전 인증 방법**: **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-221">**Preauthentication Method**: Select **Azure Active Directory**.</span></span>

  ![응용 프로그램 추가 옵션](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. <span data-ttu-id="7c85f-223">앱이 게시된 후 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-223">After the app is published, click the **Configure** tab.</span></span>
6. <span data-ttu-id="7c85f-224">**헤더에서 URL 변환** 옵션으로 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-224">Scroll down to the option **Translate URL in Headers**.</span></span> <span data-ttu-id="7c85f-225">기본값은 **예**입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-225">The default value is **YES**.</span></span> <span data-ttu-id="7c85f-226">이 값을 **아니요**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-226">Change it to **NO**.</span></span>

 <span data-ttu-id="7c85f-227">SharePoint에서는 사이트를 조회하기 위해 _호스트 헤더_ 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-227">SharePoint uses the _Host Header_ value to look up the site.</span></span> <span data-ttu-id="7c85f-228">이 값을 토대로 링크도 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-228">It also generates links based on this value.</span></span> <span data-ttu-id="7c85f-229">이렇게 하면 SharePoint에서 생성하는 모든 링크가 외부 URL을 사용하도록 올바르게 설정된 게시된 URL인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-229">The net effect is to make sure that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span></span> <span data-ttu-id="7c85f-230">값을 **예**로 설정하는 방법으로도 커넥터에서 요청을 백 엔드 응용 프로그램으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-230">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span></span> <span data-ttu-id="7c85f-231">그러나 이 값을 **아니요**로 설정하면 커넥터가 내부 호스트 이름을 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-231">However, setting the value to **NO** means that the connector will not send the internal host name.</span></span> <span data-ttu-id="7c85f-232">대신 커넥터는 호스트 헤더를 게시된 URL로 백 엔드 응용 프로그램에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-232">Instead, the connector sends the host header as the published URL to the back-end application.</span></span>

 <span data-ttu-id="7c85f-233">또한 SharePoint가 이 URL을 허용하도록 보장하기 위해 SharePoint 서버에서 하나 이상의 구성을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-233">Also, to ensure that SharePoint accepts this URL, you need to complete one more configuration on the SharePoint server.</span></span> <span data-ttu-id="7c85f-234">다음 섹션에서 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-234">You'll do that in the next section.</span></span>

7. <span data-ttu-id="7c85f-235">**내부 인증 방법**을 **Windows 통합 인증**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-235">Change **Internal Authentication Method** to **Integrated Windows Authentication**.</span></span> <span data-ttu-id="7c85f-236">Azure AD 테넌트가 온-프레미스의 UPN과 다른 클라우드의 UPN을 사용하는 경우 **위임된 로그인 ID**도 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-236">If your Azure AD tenant uses a UPN in the cloud that's different from the UPN on-premises, remember to update **Delegated Login Identity** as well.</span></span>
8. <span data-ttu-id="7c85f-237">**내부 응용 프로그램 SPN**을 이전에 설정한 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-237">Set **Internal Application SPN** to the value that you set earlier.</span></span> <span data-ttu-id="7c85f-238">예를 들어 **http/sharepoint.demo.o365identity.us**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-238">For example, use **http/sharepoint.demo.o365identity.us**.</span></span>
9. <span data-ttu-id="7c85f-239">응용 프로그램을 대상 사용자에게 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-239">Assign the application to your target users.</span></span>

<span data-ttu-id="7c85f-240">응용 프로그램은 다음 예제와 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-240">Your application should look similar to the following example:</span></span>

  ![완성된 응용 프로그램](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a><span data-ttu-id="7c85f-242">3단계: SharePoint에서 외부 URL을 알고 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="7c85f-242">Step 3: Ensure that SharePoint knows about the external URL</span></span>

<span data-ttu-id="7c85f-243">마지막 단계는 SharePoint가 외부 URL을 토대로 사이트를 찾을 수 있는지 확인하여 외부 URL을 기반으로 링크를 렌더링하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-243">Your last step to ensure that SharePoint can find the site based on the external URL, so that it will render links based on that external URL.</span></span> <span data-ttu-id="7c85f-244">SharePoint 사이트에 대한 대체 액세스 매핑을 구성하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-244">You do this by configuring alternate access mappings for the SharePoint site.</span></span>

1. <span data-ttu-id="7c85f-245">**SharePoint 2013 중앙 관리** 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-245">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="7c85f-246">**시스템 설정** 아래에서 **대체 액세스 매핑 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-246">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span>

 <span data-ttu-id="7c85f-247">그러면 **대체 액세스 매핑** 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-247">This opens the **Alternate Access Mappings** box.</span></span>

  ![대체 액세스 매핑 상자](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. <span data-ttu-id="7c85f-249">**대체 액세스 매핑 컬렉션** 옆의 드롭다운 목록에서 **대체 액세스 매핑 컬렉션 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-249">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="7c85f-250">사이트를 선택합니다(예: **SharePoint – 80**).</span><span class="sxs-lookup"><span data-stu-id="7c85f-250">Select your site--for example, **SharePoint - 80**.</span></span>

  ![사이트 선택](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. <span data-ttu-id="7c85f-252">내부 URL 또는 공용 URL로 게시된 URL을 추가하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-252">You can choose to add the published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="7c85f-253">이 예제에서는 엑스트라넷으로 공용 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-253">This example uses a public URL as the extranet.</span></span>
6. <span data-ttu-id="7c85f-254">**엑스트라넷** 경로에서 **공용 URL 편집**을 클릭한 후 이전 단계에서처럼 게시된 응용 프로그램의 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-254">Click **Edit Public URLs** in the **Extranet** path, and then enter the path for the published application, as in the previous step.</span></span> <span data-ttu-id="7c85f-255">예를 들어 **https://sharepoint-iddemo.msappproxy.net**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-255">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![경로 입력](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. <span data-ttu-id="7c85f-257">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-257">Click **Save**.</span></span>

 <span data-ttu-id="7c85f-258">Azure AD 응용 프로그램 프록시를 통해 SharePoint 사이트를 외부에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c85f-258">You can now access the SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c85f-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c85f-259">Next steps</span></span>

- [<span data-ttu-id="7c85f-260">온-프레미스 응용 프로그램에 보안된 원격 액세스를 제공하는 방법</span><span class="sxs-lookup"><span data-stu-id="7c85f-260">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- [<span data-ttu-id="7c85f-261">Azure AD 응용 프로그램 프록시 커넥터 이해</span><span class="sxs-lookup"><span data-stu-id="7c85f-261">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
- [<span data-ttu-id="7c85f-262">Azure AD 응용 프로그램 프록시를 통해 SharePoint 2016 및 Office Online Server 게시</span><span class="sxs-lookup"><span data-stu-id="7c85f-262">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
