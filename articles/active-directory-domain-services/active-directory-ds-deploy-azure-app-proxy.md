---
title: "Azure Active Directory Domain Services: Azure Active Directory 응용 프로그램 프록시 배포 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서 Azure AD 응용 프로그램 프록시 사용"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c158c67a82e12501386179e19bc75fd852d7e308
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="8173f-103">Azure AD Domain Services 관리되는 도메인에서 Azure AD 응용 프로그램 프록시 배포</span><span class="sxs-lookup"><span data-stu-id="8173f-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="8173f-104">Azure AD(Active Directory) 응용 프로그램 프록시를 사용하면 인터넷을 통해 액세스할 수 있는 온-프레미스 응용 프로그램을 게시하여 원격 작업자를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="8173f-105">이제 Azure AD Domain Services를 통해 온-프레미스를 운영 중인 레거시 응용 프로그램을 Azure Infrastructure Services로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises to Azure Infrastructure Services.</span></span> <span data-ttu-id="8173f-106">그러면 Azure AD 응용 프로그램 프록시를 사용하는 이러한 응용 프로그램을 게시하여 조직 내 사용자에게 안전한 원격 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-106">You can then publish these applications using the Azure AD Application Proxy, to provide secure remote access to users in your organization.</span></span>

<span data-ttu-id="8173f-107">Azure AD 응용 프로그램 프록시를 처음 사용하는 경우 다음에 나오는 [온-프레미스 응용 프로그램에 보안된 원격 액세스를 제공하는 방법](../active-directory/active-directory-application-proxy-get-started.md) 문서에서 이 기능에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8173f-107">If you're new to the Azure AD Application Proxy, learn more about this feature with the following article: [How to provide secure remote access to on-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="8173f-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8173f-108">Before you begin</span></span>
<span data-ttu-id="8173f-109">이 문서에 나열된 작업을 수행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="8173f-110">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="8173f-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="8173f-111">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="8173f-112">Azure AD 응용 프로그램 프록시를 사용하려면 **Azure AD Basic 또는 Premium 라이선스**가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-112">An **Azure AD Basic or Premium license** is required to use the Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="8173f-113">**Azure AD 도메인 서비스**를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="8173f-114">그렇지 않은 경우 [시작 가이드](active-directory-ds-getting-started.md)에 간략히 설명된 모든 작업을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="8173f-115">작업 1 - Azure AD Directory에 대한 Azure AD 응용 프로그램 프록시 활성화</span><span class="sxs-lookup"><span data-stu-id="8173f-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="8173f-116">다음 단계를 수행하여 Azure AD Directory에 대해 Azure AD 응용 프로그램 프록시를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-116">Perform the following steps to enable the Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="8173f-117">[Azure Portal](http://portal.azure.com)에서 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-117">Sign in as an administrator in the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="8173f-118">**Azure Active Directory**를 클릭하여 디렉터리 개요를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-118">Click **Azure Active Directory** to bring up the directory overview.</span></span> <span data-ttu-id="8173f-119">**엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-119">Click **Enterprise applications**.</span></span>

    ![Azure AD Directory 선택](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="8173f-121">**응용 프로그램 프록시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-121">Click **Application proxy**.</span></span> <span data-ttu-id="8173f-122">Azure AD Basic 또는 Azure AD Premium 구독이 없을 경우 평가판을 사용하도록 설정하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option to enable a trial.</span></span> <span data-ttu-id="8173f-123">**응용 프로그램 프록시 사용?**을 **사용**으로 설정/해제하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-123">Toggle **Enable Application Proxy?** to **Enable** and click **Save**.</span></span>

    ![앱 프록시 사용](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="8173f-125">커넥터를 다운로드하려면 **커넥터** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-125">To download the connector, click the **Connector** button.</span></span>

    ![커넥터 다운로드](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="8173f-127">다운로드 페이지에서 사용 약관 및 개인 정보 보호 계약에 동의하고 **다운로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-127">On the download page, accept the license terms and privacy agreement and click the **Download** button.</span></span>

    ![다운로드 확인](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-to-deploy-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="8173f-129">작업 2 - 도메인에 가입된 Windows 서버를 프로비전하여 Azure AD 응용 프로그램 프록시 커넥터를 배포</span><span class="sxs-lookup"><span data-stu-id="8173f-129">Task 2 - Provision domain-joined Windows servers to deploy the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="8173f-130">Azure AD 응용 프로그램 프록시 커넥터를 설치할 수 있는 도메인에 가입된 Windows Server 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-130">You need domain-joined Windows Server virtual machines on which you can install the Azure AD Application Proxy connector.</span></span> <span data-ttu-id="8173f-131">게시되는 응용 프로그램에 따라 커넥터가 설치된 여러 서버를 프로비전하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-131">Depending on the applications being published, you may choose to provision multiple servers on which the connector is installed.</span></span> <span data-ttu-id="8173f-132">이 배포 옵션을 선택하면 가용성이 높아지고 더 많은 인증 부하를 처리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="8173f-133">Azure AD Domain Services 관리되는 도메인을 사용할 수 있는 동일한 가상 네트워크(또는 연결/피어링된 가상 네트워크)에서 커넥터 서버를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-133">Provision the connector servers on the same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="8173f-134">마찬가지로, 응용 프로그램 프록시를 통해 게시한 응용 프로그램을 호스팅하는 서버는 동일한 Azure 가상 네트워크에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-134">Similarly, the servers hosting the applications you publish via the Application Proxy need to be installed on the same Azure virtual network.</span></span>

<span data-ttu-id="8173f-135">커넥터 서버를 프로비전하려면 [Windows 가상 컴퓨터를 관리되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md) 문서에 설명된 작업을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="8173f-135">To provision connector servers, follow the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="8173f-136">작업 3 - Azure AD 응용 프로그램 프록시 커넥터 설치 및 등록</span><span class="sxs-lookup"><span data-stu-id="8173f-136">Task 3 - Install and register the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="8173f-137">사전에 Windows Server 가상 컴퓨터를 프로비전하고 관리되는 도메인에 가입했습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-137">Previously, you provisioned a Windows Server virtual machine and joined it to the managed domain.</span></span> <span data-ttu-id="8173f-138">이 작업에서는 이 가상 컴퓨터에 Azure AD 응용 프로그램 프록시 커넥터를 설치할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-138">In this task, you will install the Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="8173f-139">Azure AD 웹 응용 프로그램 프록시 커넥터를 설치하는 VM에 커넥터 설치 패키지를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-139">Copy the connector installation package to the VM on which you install the Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="8173f-140">**AADApplicationProxyConnectorInstaller.exe**를 가상 컴퓨터에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-140">Run **AADApplicationProxyConnectorInstaller.exe** on the virtual machine.</span></span> <span data-ttu-id="8173f-141">소프트웨어 사용 조건에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-141">Accept the software license terms.</span></span>

    ![설치 조건에 동의](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="8173f-143">설치하는 동안 Azure AD Directory의 응용 프로그램 프록시를 사용하여 커넥터를 등록하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-143">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="8173f-144">**Azure AD 전역 관리자 자격 증명**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="8173f-145">전역 관리자 테넌트는 Microsoft Azure 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="8173f-146">커넥터를 등록하는 데 사용되는 관리자 계정은 응용 프로그램 프록시 서비스를 사용할 수 있는 동일한 디렉터리에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-146">The administrator account used to register the connector must belong to the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="8173f-147">예를 들어, 테넌트 도메인이 contoso.com이면 관리자는 admin@contoso.com 또는 해당 도메인에 있는 다른 유효한 별칭이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-147">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="8173f-148">커넥터를 설치하는 서버에 IE 보안 강화 구성이 켜져 있으면 등록 화면이 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-148">If IE Enhanced Security Configuration is turned on for the server where you are installing the connector, the registration screen might be blocked.</span></span> <span data-ttu-id="8173f-149">액세스를 허용하려면 오류 메시지의 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-149">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="8173f-150">Internet Explorer 보안 강화가 해제되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="8173f-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="8173f-151">커넥터 등록에 실패한 경우 [응용 프로그램 프록시 문제 해결](../active-directory/active-directory-application-proxy-troubleshoot.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8173f-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![커넥터 설치됨](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="8173f-153">커넥터가 제대로 작동하는지 확인하려면 Azure AD 응용 프로그램 프록시 커넥터 문제 해결사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-153">To ensure the connector works properly, run the Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="8173f-154">문제 해결사를 실행한 후 성공적인 보고서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-154">You should see a successful report after running the troubleshooter.</span></span>

    ![문제 해결사 성공](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="8173f-156">새롭게 설치된 커넥터가 Azure AD Directory의 응용 프로그램 프록시 페이지에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-156">You should see the newly installed connector listed on the Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="8173f-157">커넥터를 여러 서버에 설치하도록 선택하면 Azure AD 응용 프로그램 프록시를 통해 게시된 응용 프로그램을 인증하는 데 고가용성을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-157">You may choose to install connectors on multiple servers to guarantee high availability for authenticating applications published through the Azure AD Application Proxy.</span></span> <span data-ttu-id="8173f-158">관리되는 도메인에 가입된 다른 서버에 커넥터를 설치하려면 위에 나열된 것과 동일한 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-158">Perform the same steps listed above to install the connector on other servers joined to your managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8173f-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8173f-159">Next Steps</span></span>
<span data-ttu-id="8173f-160">지금까지 Azure AD 응용 프로그램 프록시를 설정하고 Azure AD Domain Services 관리되는 도메인에 통합했습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-160">You have set up the Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="8173f-161">**응용 프로그램을 Azure 가상 컴퓨터로 마이그레이션:** 응용 프로그램을 온-프레미스 서버에서 관리되는 도메인에 가입된 Azure 가상 컴퓨터로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-161">**Migrate your applications to Azure virtual machines:** You can lift-and-shift your applications from on-premises servers to Azure virtual machines joined to your managed domain.</span></span> <span data-ttu-id="8173f-162">이를 통해 온-프레미스 운영 서버의 인프라 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-162">Doing so helps you get rid of the infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="8173f-163">**Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시:** Azure AD 응용 프로그램 프록시를 사용하여 Azure 가상 컴퓨터에서 실행 중인 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using the Azure AD Application Proxy.</span></span> <span data-ttu-id="8173f-164">자세한 내용은 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](../active-directory/application-proxy-publish-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8173f-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="8173f-165">배포 참고 - Azure AD 응용 프로그램 프록시를 사용하여 IWA(Windows 통합 인증) 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="8173f-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="8173f-166">응용 프로그램 프록시 커넥터 사용 권한을 부여하여 사용자를 가장하고 사용자를 대신해서 토큰을 보내고 받음으로써 IWA(Windows 통합 인증)를 사용하여 응용 프로그램에 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-166">Enable single sign-on to your applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission to impersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="8173f-167">커넥터에 대한 Kerberos 제한 위임(KCD)을 구성하여 관리되는 도메인의 리소스에 액세스하는 데 필요한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-167">Configure kerberos constrained delegation (KCD) for the connector to grant the required permissions to access resources on the managed domain.</span></span> <span data-ttu-id="8173f-168">보안 향상을 위해 관리되는 도메인에서 리소스 기반 KCD 메커니즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-168">Use the resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="8173f-169">Azure AD 응용 프로그램 프록시 커넥터에 대한 리소스 기반 Kerberos 제한 위임을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8173f-169">Enable resource-based kerberos constrained delegation for the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="8173f-170">관리되는 도메인에서 사용자를 가장할 수 있도록 Azure 응용 프로그램 프록시 커넥터는 Kerberos 제한 위임(KCD)에 대해 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-170">The Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on the managed domain.</span></span> <span data-ttu-id="8173f-171">Azure AD Domain Services 관리되는 도메인에서 도메인 관리자 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="8173f-172">따라서 **관리되는 도메인에 기존 계정 수준 KCD를 구성할 수 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="8173f-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="8173f-173">이 [문서](active-directory-ds-enable-kcd.md)에 설명된 대로 리소스 기반 KCD를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8173f-174">AD PowerShell cmdlet을 사용하여 관리되는 도메인을 관리하려면 'AAD DC 관리자' 그룹의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-174">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="8173f-175">Get-ADComputer PowerShell cmdlet을 사용하여 Azure AD 응용 프로그램 프록시 커넥터가 설치된 컴퓨터에 대한 설정을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-175">Use the Get-ADComputer PowerShell cmdlet to retrieve the settings for the computer on which the Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="8173f-176">그 후 Set-ADComputer cmdlet을 사용하여 리소스 서버에 대한 리소스 기반 KCD를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-176">Thereafter, use the Set-ADComputer cmdlet to set up resource-based KCD for the resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="8173f-177">관리되는 도메인에서 여러 응용 프로그램 프록시 커넥터를 배포한 경우 이러한 각 커넥터 인스턴스에 대한 리소스 기반 KCD를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8173f-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need to configure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="8173f-178">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="8173f-178">Related Content</span></span>
* [<span data-ttu-id="8173f-179">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="8173f-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="8173f-180">관리되는 도메인에서 Kerberos 제한 위임 구성</span><span class="sxs-lookup"><span data-stu-id="8173f-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="8173f-181">Kerberos 제한 위임 개요</span><span class="sxs-lookup"><span data-stu-id="8173f-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
