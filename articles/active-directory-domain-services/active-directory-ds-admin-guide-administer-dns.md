---
title: "Azure Active Directory Domain Services: 관리되는 도메인에서 DNS 관리 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서 DNS 관리"
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
ms.openlocfilehash: 812641a3e4d5bf496d81b036d326595c5722b7fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="1739c-103">Azure AD 도메인 서비스 관리되는 도메인에서 DNS 관리</span><span class="sxs-lookup"><span data-stu-id="1739c-103">Administer DNS on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="1739c-104">Azure Active Directory 도메인 서비스는 관리되는 도메인에 대한 DNS 확인을 제공하는 DNS(도메인 이름 확인) 서버를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-104">Azure Active Directory Domain Services includes a DNS (Domain Name Resolution) server that provides DNS resolution for the managed domain.</span></span> <span data-ttu-id="1739c-105">경우에 따라 관리되는 도메인에서 DNS를 구성해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-105">Occasionally, you may need to configure DNS on the managed domain.</span></span> <span data-ttu-id="1739c-106">도메인에 가입되지 않은 컴퓨터에 대한 DNS 레코드를 만들고 부하 분산 장치에 대한 가상 IP 주소를 구성하거나 외부 DNS 전달자를 설정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-106">You may need to create DNS records for machines that are not joined to the domain, configure virtual IP addresses for load-balancers or setup external DNS forwarders.</span></span> <span data-ttu-id="1739c-107">이러한 이유로 'AAD DC 관리자' 그룹에 속한 사용자에게 관리되는 도메인에 대한 DNS 관리 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-107">For this reason, users who belong to the 'AAD DC Administrators' group are granted DNS administration privileges on the managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1739c-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1739c-108">Before you begin</span></span>
<span data-ttu-id="1739c-109">이 문서에 나열된 작업을 수행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="1739c-110">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="1739c-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="1739c-111">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="1739c-112">**Azure AD 도메인 서비스** 를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-112">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="1739c-113">그렇지 않은 경우 [시작 가이드](active-directory-ds-getting-started.md)에 간략히 설명된 모든 작업을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-113">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="1739c-114">Azure AD 도메인 서비스 관리되는 도메인을 관리하게 될 **도메인에 가입된 가상 컴퓨터** .</span><span class="sxs-lookup"><span data-stu-id="1739c-114">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="1739c-115">이러한 가상 컴퓨터가 없는 경우 [Windows 가상 컴퓨터를 관리되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)문서에 설명된 모든 작업을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="1739c-115">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="1739c-116">관리되는 도메인에 대한 DNS를 관리하려면 디렉터리의 **'AAD DC 관리자' 그룹에 속한 사용자 계정** 의 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-116">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer DNS for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-to-remotely-administer-dns-for-the-managed-domain"></a><span data-ttu-id="1739c-117">작업 1 - 관리되는 도메인에 대한 DNS를 원격으로 관리하기 위해 도메인에 가입된 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="1739c-117">Task 1 - Provision a domain-joined virtual machine to remotely administer DNS for the managed domain</span></span>
<span data-ttu-id="1739c-118">Azure AD 도메인 서비스 관리되는 도메인을 AD PowerShell 또는 ADAC(Active Directory 관리 센터)와 같은 친숙한 Active Directory 관리 도구를 사용하여 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-118">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="1739c-119">마찬가지로, DNS 서버 관리 도구를 사용하여 관리되는 도메인에 대한 DNS를 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-119">Similarly, DNS for the managed domain can be administered remotely using the DNS Server administration tools.</span></span>

<span data-ttu-id="1739c-120">Azure AD 디렉터리의 테넌트 관리자는 원격 데스크톱을 통해 관리되는 도메인의 도메인 컨트롤러에 연결할 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-120">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="1739c-121">'AAD DC 관리자' 그룹의 멤버는 관리되는 도메인에 가입된 Windows Server/클라이언트 컴퓨터에서 DNS 서버 도구를 사용하여 관리되는 도메인에 대한 DNS를 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-121">Members of the 'AAD DC Administrators' group can administer DNS for managed domains remotely using DNS Server tools from a Windows Server/client computer that is joined to the managed domain.</span></span> <span data-ttu-id="1739c-122">DNS 서버 도구는 관리되는 도메인에 가입된 클라이언트 컴퓨터 및 Windows Server에서 원격 서버 관리 도구(RSAT) 선택적 기능의 일부로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-122">DNS Server tools can be installed as part of the Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="1739c-123">Windows Server 가상 컴퓨터를 프로비전하기 위한 첫 번째 작업은 관리되는 도메인에 가입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-123">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="1739c-124">지침은 [Windows Server 가상 컴퓨터를 Azure AD 도메인 서비스 관리되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)이라는 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1739c-124">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-dns-server-tools-on-the-virtual-machine"></a><span data-ttu-id="1739c-125">작업 2 - 가상 컴퓨터에 DNS 서버 도구 설치</span><span class="sxs-lookup"><span data-stu-id="1739c-125">Task 2 - Install DNS Server tools on the virtual machine</span></span>
<span data-ttu-id="1739c-126">도메인에 가입된 가상 컴퓨터에 DNS 관리 도구를 설치하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-126">Perform the following steps to install the DNS Administration tools on the domain joined virtual machine.</span></span> <span data-ttu-id="1739c-127">[원격 서버 관리 도구 설치 및 사용](https://technet.microsoft.com/library/hh831501.aspx)에 대한 자세한 내용은 TechNet을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1739c-127">For more information on [installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx), see Technet.</span></span>

1. <span data-ttu-id="1739c-128">Azure 클래식 포털에서 **가상 컴퓨터** 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-128">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="1739c-129">작업 1에서 만든 가상 컴퓨터를 선택하고 창 아래쪽에 있는 명령 모음에서 **연결** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-129">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![Windows 가상 컴퓨터에 연결](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="1739c-131">클래식 포털에 가상 컴퓨터에 연결하는 데 사용되는 ‘.rdp’ 확장명을 가진 파일을 열거나 저장하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-131">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="1739c-132">다운로드가 완료되면 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-132">Click the file when it has finished downloading.</span></span>
3. <span data-ttu-id="1739c-133">로그인 프롬프트에서 'AAD DC 관리자' 그룹에 속한 사용자의 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-133">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="1739c-134">사용 예를 들어 'bob@domainservicespreview.onmicrosoft.com' 여기서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-134">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="1739c-135">시작 화면에서 **서버 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-135">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="1739c-136">서버 관리자 창의 가운데 창에서 **역할 및 기능 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-136">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![가상 컴퓨터에서 서버 관리자 시작](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="1739c-138">**역할 및 기능 추가 마법사**의 **시작하기 전에** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-138">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![시작하기 전에 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="1739c-140">**설치 유형** 페이지에서 **역할 기반 또는 기능 기반 설치** 옵션을 선택한 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-140">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![설치 유형 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="1739c-142">**서버 선택** 페이지에서 서버 풀의 현재 가상 컴퓨터를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-142">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![서버 선택 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="1739c-144">**서버 역할** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-144">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="1739c-145">서버에 어떠한 역할도 설치하지 않으므로 이 페이지는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-145">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="1739c-146">**기능** 페이지에서 **원격 서버 관리 도구** 노드를 클릭하여 확장한 후 **역할 관리 도구** 노드를 클릭하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-146">On the **Features** page, click to expand the **Remote Server Administration Tools** node and then click to expand the **Role Administration Tools** node.</span></span> <span data-ttu-id="1739c-147">역할 관리 도구 목록에서 **DNS 서버 도구** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-147">Select **DNS Server Tools** feature from the list of role administration tools.</span></span>

    ![기능 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. <span data-ttu-id="1739c-149">**확인** 페이지에서 가상 컴퓨터에 DNS 서버 도구를 설치하기 위해 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-149">On the **Confirmation** page, click **Install** to install the DNS Server tools feature on the virtual machine.</span></span> <span data-ttu-id="1739c-150">기능 설치를 성공적으로 완료하면 **닫기**를 클릭하여 **역할 및 기능 추가** 마법사를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![확인 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-the-dns-management-console-to-administer-dns"></a><span data-ttu-id="1739c-152">작업 3 - DNS 관리 콘솔을 실행하여 DNS 관리</span><span class="sxs-lookup"><span data-stu-id="1739c-152">Task 3 - Launch the DNS management console to administer DNS</span></span>
<span data-ttu-id="1739c-153">이제 DNS 서버 도구 기능을 도메인에 가입된 가상 컴퓨터에 설치했으므로 DNS 도구를 사용하여 관리되는 도메인에서 DNS를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-153">Now that the DNS Server Tools feature is installed on the domain joined virtual machine, we can use the DNS tools to administer DNS on the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="1739c-154">관리되는 도메인의 DNS를 관리하려면 'AAD DC 관리자' 그룹의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-154">You need to be a member of the 'AAD DC Administrators' group, to administer DNS on the managed domain.</span></span>
>
>

1. <span data-ttu-id="1739c-155">시작 화면에서 **관리 도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-155">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="1739c-156">가상 컴퓨터에 설치된 **DNS** 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-156">You should see the **DNS** console installed on the virtual machine.</span></span>

    ![관리 도구 - DNS 콘솔](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. <span data-ttu-id="1739c-158">**DNS** 를 클릭하여 DNS 관리 콘솔을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-158">Click **DNS** to launch the DNS Management console.</span></span>
3. <span data-ttu-id="1739c-159">**DNS 서버에 연결** 대화 상자에서 **다음 컴퓨터** 옵션을 클릭하고 관리되는 도메인의 DNS 도메인 이름을 입력합니다(예: 'contoso100.com').</span><span class="sxs-lookup"><span data-stu-id="1739c-159">In the **Connect to DNS Server** dialog, click the option titled **The following computer**, and enter the DNS domain name of the managed domain (for example, 'contoso100.com').</span></span>

    ![DNS 콘솔 - 도메인에 연결](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. <span data-ttu-id="1739c-161">DNS 콘솔이 관리되는 도메인에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-161">The DNS Console connects to the managed domain.</span></span>

    ![DNS 콘솔 - 도메인 관리](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. <span data-ttu-id="1739c-163">이제 AAD 도메인 서비스를 활성화한 가상 네트워크 내에 있는 컴퓨터에 대한 DNS 항목을 추가하는 데 DNS 콘솔을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-163">You can now use the DNS console to add DNS entries for computers within the virtual network in which you've enabled AAD Domain Services.</span></span>

> [!WARNING]
> <span data-ttu-id="1739c-164">DNS 관리 도구를 사용하여 관리되는 도메인에 대한 DNS를 관리할 때는 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-164">Be careful when administering DNS for the managed domain using DNS administration tools.</span></span> <span data-ttu-id="1739c-165">**도메인의 도메인 서비스에서 사용하는 기본 제공 DNS 레코드를 삭제 또는 수정하지 않도록**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-165">Ensure that you **do not delete or modify the built-in DNS records that are used by Domain Services in the domain**.</span></span> <span data-ttu-id="1739c-166">기본 제공 DNS 레코드는 도메인 DNS 레코드, 이름 서버 레코드 및 DC 위치에 사용되는 기타 레코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-166">Built-in DNS records include domain DNS records, name server records, and other records used for DC location.</span></span> <span data-ttu-id="1739c-167">이러한 레코드를 수정하는 경우 가상 네트워크에서 도메인 서비스가 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="1739c-167">If you modify these records, domain services are disrupted on the virtual network.</span></span>
>
>

<span data-ttu-id="1739c-168">DNS 관리에 대한 자세한 내용은 [Technet의 DNS 도구 문서](https://technet.microsoft.com/library/cc753579.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1739c-168">See the [DNS tools article on Technet](https://technet.microsoft.com/library/cc753579.aspx) for more information about managing DNS.</span></span>

## <a name="related-content"></a><span data-ttu-id="1739c-169">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="1739c-169">Related Content</span></span>
* [<span data-ttu-id="1739c-170">Azure AD 도메인 서비스 - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="1739c-170">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="1739c-171">Windows Server 가상 컴퓨터를 Azure AD 도메인 서비스 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="1739c-171">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="1739c-172">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="1739c-172">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="1739c-173">DNS 관리 도구</span><span class="sxs-lookup"><span data-stu-id="1739c-173">DNS administration tools</span></span>](https://technet.microsoft.com/library/cc753579.aspx)
