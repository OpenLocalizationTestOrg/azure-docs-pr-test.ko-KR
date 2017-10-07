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
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="d3453-103">Azure AD Domain Services 관리되는 도메인에서 Azure AD 응용 프로그램 프록시 배포</span><span class="sxs-lookup"><span data-stu-id="d3453-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="d3453-104">Azure AD (Active Directory) 응용 프로그램 프록시를 사용 하면 온-프레미스 응용 프로그램 toobe hello를 통해 액세스를 게시 하 여 원격 작업자를 지 원하는 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="d3453-105">Azure AD 도메인 서비스와 온-프레미스 tooAzure 인프라 서비스를 실행 중인 이제 리프트 및-시프트 레거시 응용 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises tooAzure Infrastructure Services.</span></span> <span data-ttu-id="d3453-106">그런 다음 Azure AD 응용 프로그램 프록시, 조직에서 보안 된 원격 액세스 toousers tooprovide hello를 사용 하 여 이러한 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-106">You can then publish these applications using hello Azure AD Application Proxy, tooprovide secure remote access toousers in your organization.</span></span>

<span data-ttu-id="d3453-107">새 toohello Azure AD 응용 프로그램 프록시를 사용 하는 경우 자세한 내용은이 기능에 대 한 다음 문서는 hello로: [어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램](../active-directory/active-directory-application-proxy-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-107">If you're new toohello Azure AD Application Proxy, learn more about this feature with hello following article: [How tooprovide secure remote access tooon-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="d3453-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d3453-108">Before you begin</span></span>
<span data-ttu-id="d3453-109">이 문서에 나열 된 tooperform hello 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-109">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="d3453-110">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="d3453-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="d3453-111">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="d3453-112">**Azure AD Basic 또는 Premium 라이선스** Azure AD 응용 프로그램 프록시 hello toouse 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-112">An **Azure AD Basic or Premium license** is required toouse hello Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="d3453-113">**Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-113">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="d3453-114">그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-114">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="d3453-115">작업 1 - Azure AD Directory에 대한 Azure AD 응용 프로그램 프록시 활성화</span><span class="sxs-lookup"><span data-stu-id="d3453-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="d3453-116">Hello 단계 tooenable hello Azure AD 디렉터리에 대 한 Azure AD 응용 프로그램 프록시를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-116">Perform hello following steps tooenable hello Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="d3453-117">Hello에 관리자 권한으로 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-117">Sign in as an administrator in hello [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="d3453-118">클릭 **Azure Active Directory** toobring hello directory 개요를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-118">Click **Azure Active Directory** toobring up hello directory overview.</span></span> <span data-ttu-id="d3453-119">**엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-119">Click **Enterprise applications**.</span></span>

    ![Azure AD Directory 선택](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="d3453-121">**응용 프로그램 프록시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-121">Click **Application proxy**.</span></span> <span data-ttu-id="d3453-122">Azure AD Basic 또는 Azure AD Premium 구독이 없는 경우 옵션 tooenable 평가판을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option tooenable a trial.</span></span> <span data-ttu-id="d3453-123">설정/해제 **응용 프로그램 프록시를 사용 하도록 설정?** 너무**사용** 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-123">Toggle **Enable Application Proxy?** too**Enable** and click **Save**.</span></span>

    ![앱 프록시 사용](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="d3453-125">toodownload 커넥터 hello, hello 클릭 **커넥터** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-125">toodownload hello connector, click hello **Connector** button.</span></span>

    ![커넥터 다운로드](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="d3453-127">Hello 다운로드 페이지에서 hello 사용 약관 및 개인 정보 보호 계약에 동의 하 고 hello 클릭 **다운로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-127">On hello download page, accept hello license terms and privacy agreement and click hello **Download** button.</span></span>

    ![다운로드 확인](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="d3453-129">작업 2-프로 비전 도메인에 가입 된 Windows 서버 toodeploy hello Azure AD 응용 프로그램 프록시 커넥터</span><span class="sxs-lookup"><span data-stu-id="d3453-129">Task 2 - Provision domain-joined Windows servers toodeploy hello Azure AD Application Proxy connector</span></span>
<span data-ttu-id="d3453-130">Hello Azure AD 응용 프로그램 프록시 커넥터를 설치할 수 있는 도메인에 가입 된 Windows Server 가상 컴퓨터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-130">You need domain-joined Windows Server virtual machines on which you can install hello Azure AD Application Proxy connector.</span></span> <span data-ttu-id="d3453-131">게시 되는 hello 응용 프로그램에 따라 tooprovision hello 커넥터가 설치 된 여러 서버를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-131">Depending on hello applications being published, you may choose tooprovision multiple servers on which hello connector is installed.</span></span> <span data-ttu-id="d3453-132">이 배포 옵션을 선택하면 가용성이 높아지고 더 많은 인증 부하를 처리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="d3453-133">커넥터 서버 hello를 프로 비전 동일한 가상 네트워크 (또는 연결/겹치기 가상 네트워크)를 사용 하도록 설정한에 hello Azure AD 도메인 서비스 관리 되는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-133">Provision hello connector servers on hello same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="d3453-134">Hello 응용 프로그램 프록시를 통해 게시 하는 hello 응용 프로그램을 호스트 하는 hello 서버 toobe hello에 설치 해야 하는 마찬가지로 동일한 Azure 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-134">Similarly, hello servers hosting hello applications you publish via hello Application Proxy need toobe installed on hello same Azure virtual network.</span></span>

<span data-ttu-id="d3453-135">tooprovision 커넥터 서버 hello 문서에 설명 된 hello 작업에 따라 [Windows 가상 컴퓨터 tooa 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-135">tooprovision connector servers, follow hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="d3453-136">작업 3-설치 및 등록 hello Azure AD 응용 프로그램 프록시 커넥터</span><span class="sxs-lookup"><span data-stu-id="d3453-136">Task 3 - Install and register hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="d3453-137">이전에 Windows Server 가상 컴퓨터를 프로 비전 하 고 toohello 관리 되는 도메인 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-137">Previously, you provisioned a Windows Server virtual machine and joined it toohello managed domain.</span></span> <span data-ttu-id="d3453-138">이 작업에서는이 가상 컴퓨터에 hello Azure AD 응용 프로그램 프록시 커넥터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-138">In this task, you will install hello Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="d3453-139">Hello Azure AD 웹 응용 프로그램 프록시 커넥터를 설치 하는 hello 커넥터 설치 패키지 toohello VM을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-139">Copy hello connector installation package toohello VM on which you install hello Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="d3453-140">실행 **AADApplicationProxyConnectorInstaller.exe** hello 가상 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-140">Run **AADApplicationProxyConnectorInstaller.exe** on hello virtual machine.</span></span> <span data-ttu-id="d3453-141">Hello 소프트웨어 사용 조건에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-141">Accept hello software license terms.</span></span>

    ![설치 조건에 동의](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="d3453-143">설치 하는 동안 Azure AD 디렉터리의 응용 프로그램 프록시 hello로 증명된 tooregister hello 커넥터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-143">During installation, you are prompted tooregister hello connector with hello Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="d3453-144">**Azure AD 전역 관리자 자격 증명**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="d3453-145">전역 관리자 테넌트는 Microsoft Azure 자격 증명과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="d3453-146">hello 관리자 사용 되는 계정 tooregister hello 커넥터 속해야 toohello hello 응용 프로그램 프록시 서비스를 사용할 수 있는 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-146">hello administrator account used tooregister hello connector must belong toohello same directory where you enabled hello Application Proxy service.</span></span> <span data-ttu-id="d3453-147">예를 들어 hello 테 넌 트 도메인이 contoso.com 이면 admin 님 안녕하세요 해야 admin@contoso.com 또는 해당 도메인에 있는 다른 모든 유효한 별칭.</span><span class="sxs-lookup"><span data-stu-id="d3453-147">For example, if hello tenant domain is contoso.com, hello admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="d3453-148">IE 보안 강화 구성 켜져 hello 서버에 대 한 hello 커넥터 설치 하는 hello 등록 화면이 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-148">If IE Enhanced Security Configuration is turned on for hello server where you are installing hello connector, hello registration screen might be blocked.</span></span> <span data-ttu-id="d3453-149">hello 오류 메시지의 지침에 따라 hello tooallow 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-149">tooallow access, follow hello instructions in hello error message.</span></span> <span data-ttu-id="d3453-150">Internet Explorer 보안 강화가 해제되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d3453-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="d3453-151">커넥터 등록에 실패한 경우 [응용 프로그램 프록시 문제 해결](../active-directory/active-directory-application-proxy-troubleshoot.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3453-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![커넥터 설치됨](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="d3453-153">tooensure hello 커넥터 실행된 hello Azure AD 응용 프로그램 프록시 커넥터 문제 해결사는 올바르게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-153">tooensure hello connector works properly, run hello Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="d3453-154">Hello 문제 해결사를 실행 한 후 성공 보고서에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-154">You should see a successful report after running hello troubleshooter.</span></span>

    ![문제 해결사 성공](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="d3453-156">Azure AD 디렉터리의 hello 응용 프로그램 프록시 페이지에 나열 된 hello 새로 설치 된 커넥터에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-156">You should see hello newly installed connector listed on hello Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="d3453-157">여러 서버에서 tooinstall 커넥터 tooguarantee 고가용성 hello Azure AD 응용 프로그램 프록시를 통해 게시 된 응용 프로그램을 인증 하기 위해 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-157">You may choose tooinstall connectors on multiple servers tooguarantee high availability for authenticating applications published through hello Azure AD Application Proxy.</span></span> <span data-ttu-id="d3453-158">Hello tooinstall hello 커넥터 다른 서버에 가입된 tooyour 관리 되는 도메인에 위에 나열 된 동일한 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-158">Perform hello same steps listed above tooinstall hello connector on other servers joined tooyour managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d3453-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3453-159">Next Steps</span></span>
<span data-ttu-id="d3453-160">Hello Azure AD 응용 프로그램 프록시를 설정에 있고 도메인 관리 되는 Azure AD 도메인 서비스와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-160">You have set up hello Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="d3453-161">**응용 프로그램 tooAzure 가상 컴퓨터 마이그레이션:** 리프트 시프트 온-프레미스 서버 tooAzure 가상 컴퓨터에 가입된 tooyour 관리 되는 도메인에서 응용 프로그램 수입니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-161">**Migrate your applications tooAzure virtual machines:** You can lift-and-shift your applications from on-premises servers tooAzure virtual machines joined tooyour managed domain.</span></span> <span data-ttu-id="d3453-162">이렇게 하면 서버 온-프레미스를 실행 중인 hello 인프라 비용을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-162">Doing so helps you get rid of hello infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="d3453-163">**Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램 게시:** hello Azure AD 응용 프로그램 프록시를 사용 하 여 Azure 가상 컴퓨터에서 실행 되는 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using hello Azure AD Application Proxy.</span></span> <span data-ttu-id="d3453-164">자세한 내용은 [Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](../active-directory/application-proxy-publish-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3453-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="d3453-165">배포 참고 - Azure AD 응용 프로그램 프록시를 사용하여 IWA(Windows 통합 인증) 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="d3453-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="d3453-166">Tooimpersonate 사용자 응용 프로그램 프록시 커넥터 권한을 부여 하 여 통합 IWA (Windows 인증)를 사용 하 여 single sign on tooyour 응용 프로그램을 사용 하도록 설정 하 고 보내고 사용자 대신 토큰을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-166">Enable single sign-on tooyour applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission tooimpersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="d3453-167">리소스에 대 한 hello 커넥터 toogrant hello 필요한 사용 권한 tooaccess hello 관리 되는 도메인에서 kerberos 제한 위임을 KCD ()를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-167">Configure kerberos constrained delegation (KCD) for hello connector toogrant hello required permissions tooaccess resources on hello managed domain.</span></span> <span data-ttu-id="d3453-168">보안 향상된을 위해 관리 되는 도메인에 hello 리소스 기반 KCD 메커니즘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-168">Use hello resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="d3453-169">Hello Azure AD 응용 프로그램 프록시 커넥터에 대 한 리소스 기반 kerberos 제한 위임을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d3453-169">Enable resource-based kerberos constrained delegation for hello Azure AD Application Proxy connector</span></span>
<span data-ttu-id="d3453-170">hello Azure 응용 프로그램 프록시 커넥터에서 구성 해야 (KCD) kerberos 제한 위임에 대 한 사용자를 가장할 수 있으므로 hello 관리 되는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-170">hello Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on hello managed domain.</span></span> <span data-ttu-id="d3453-171">Azure AD Domain Services 관리되는 도메인에서 도메인 관리자 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="d3453-172">따라서 **관리되는 도메인에 기존 계정 수준 KCD를 구성할 수 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="d3453-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="d3453-173">이 [문서](active-directory-ds-enable-kcd.md)에 설명된 대로 리소스 기반 KCD를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d3453-174">구성원 toobe 필요한 tooadminister hello hello ' AAD DC Administrators' 그룹의 AD PowerShell cmdlet을 사용 하 여 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-174">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister hello managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="d3453-175">Hello는 hello Azure AD 응용 프로그램 프록시 커넥터가 설치 된 컴퓨터에 대 한 hello Get-adcomputer PowerShell cmdlet tooretrieve hello 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-175">Use hello Get-ADComputer PowerShell cmdlet tooretrieve hello settings for hello computer on which hello Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="d3453-176">그 후 hello Set-adcomputer cmdlet tooset 리소스 기반 KCD 사용 하 여 리소스 서버 hello에 대 한.</span><span class="sxs-lookup"><span data-stu-id="d3453-176">Thereafter, use hello Set-ADComputer cmdlet tooset up resource-based KCD for hello resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="d3453-177">Tooconfigure 필요한 관리 되는 도메인에서 여러 응용 프로그램 프록시 커넥터를 배포한 경우 이러한 각 커넥터 인스턴스에 대 한 KCD 리소스 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3453-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need tooconfigure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="d3453-178">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="d3453-178">Related Content</span></span>
* [<span data-ttu-id="d3453-179">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="d3453-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="d3453-180">관리되는 도메인에서 Kerberos 제한 위임 구성</span><span class="sxs-lookup"><span data-stu-id="d3453-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="d3453-181">Kerberos 제한 위임 개요</span><span class="sxs-lookup"><span data-stu-id="d3453-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
