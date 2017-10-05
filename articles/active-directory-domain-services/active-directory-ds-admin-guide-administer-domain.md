---
title: "Azure Active Directory Domain Services: 관리되는 도메인 관리 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 관리되는 도메인 관리"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: a8292474b6b81172850c11f6cb5b04baf64aec77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a><span data-ttu-id="ea086-103">Azure Active Directory 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="ea086-103">Administer an Azure Active Directory Domain Services managed domain</span></span>
<span data-ttu-id="ea086-104">이 문서에서는 Azure AD(Active Directory) 도메인 서비스 관리되는 도메인을 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-104">This article shows you how to administer an Azure Active Directory (AD) Domain Services managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ea086-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ea086-105">Before you begin</span></span>
<span data-ttu-id="ea086-106">이 문서에 나열된 작업을 수행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-106">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="ea086-107">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="ea086-107">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="ea086-108">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="ea086-109">**Azure AD 도메인 서비스** 를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-109">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="ea086-110">그렇지 않은 경우 [시작 가이드](active-directory-ds-getting-started.md)에 간략히 설명된 모든 작업을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-110">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="ea086-111">Azure AD 도메인 서비스 관리되는 도메인을 관리하게 될 **도메인에 가입된 가상 컴퓨터** .</span><span class="sxs-lookup"><span data-stu-id="ea086-111">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="ea086-112">이러한 가상 컴퓨터가 없는 경우 [Windows 가상 컴퓨터를 관리되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)문서에 설명된 모든 작업을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="ea086-112">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="ea086-113">관리되는 도메인을 관리하려면 디렉터리의 **'AAD DC 관리자' 그룹에 속한 사용자 계정** 의 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-113">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer your managed domain.</span></span>

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a><span data-ttu-id="ea086-114">관리되는 도메인에서 수행할 수 있는 관리 작업</span><span class="sxs-lookup"><span data-stu-id="ea086-114">Administrative tasks you can perform on a managed domain</span></span>
<span data-ttu-id="ea086-115">'AAD DC 관리자' 그룹의 멤버에게는 다음과 같은 작업을 수행할 수 있는 관리되는 도메인에 대한 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-115">Members of the 'AAD DC Administrators' group are granted privileges on the managed domain that enable them to perform tasks such as:</span></span>

* <span data-ttu-id="ea086-116">컴퓨터를 관리되는 도메인에 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-116">Join machines to the managed domain.</span></span>
* <span data-ttu-id="ea086-117">관리되는 도메인에서 'AADDC 컴퓨터' 및 'AADDC 사용자' 컨테이너에 대한 기본 제공 GPO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-117">Configure the built-in GPO for the 'AADDC Computers' and 'AADDC Users' containers in the managed domain.</span></span>
* <span data-ttu-id="ea086-118">관리되는 도메인에서 DNS 관리</span><span class="sxs-lookup"><span data-stu-id="ea086-118">Administer DNS on the managed domain.</span></span>
* <span data-ttu-id="ea086-119">관리되는 도메인에서 사용자 지정 OU(조직 구성 단위)를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-119">Create and administer custom Organizational Units (OUs) on the managed domain.</span></span>
* <span data-ttu-id="ea086-120">관리되는 도메인에 가입된 컴퓨터에 대한 관리 액세스 권한을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-120">Gain administrative access to computers joined to the managed domain.</span></span>

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a><span data-ttu-id="ea086-121">관리되는 도메인에 없는 관리자 권한</span><span class="sxs-lookup"><span data-stu-id="ea086-121">Administrative privileges you do not have on a managed domain</span></span>
<span data-ttu-id="ea086-122">패치 적용, 모니터링 및 백업 수행과 같은 작업을 포함한 도메인 관리는 Microsoft에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-122">The domain is managed by Microsoft, including activities such as patching, monitoring and, performing backups.</span></span> <span data-ttu-id="ea086-123">따라서 도메인은 잠금 상태이고 도메인에 대해 특정 관리 작업을 수행할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-123">Therefore, the domain is locked down and you do not have privileges to perform certain administrative tasks on the domain.</span></span> <span data-ttu-id="ea086-124">수행할 수 없는 작업의 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-124">Some examples of tasks you cannot perform are below.</span></span>

* <span data-ttu-id="ea086-125">관리되는 도메인에 대해 도메인 관리자 또는 엔터프라이즈 관리자 권한을 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-125">You are not granted Domain Administrator or Enterprise Administrator privileges for the managed domain.</span></span>
* <span data-ttu-id="ea086-126">관리되는 도메인의 스키마를 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-126">You cannot extend the schema of the managed domain.</span></span>
* <span data-ttu-id="ea086-127">원격 데스크톱을 사용하여 관리되는 도메인의 도메인 컨트롤러에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-127">You cannot connect to domain controllers for the managed domain using Remote Desktop.</span></span>
* <span data-ttu-id="ea086-128">관리되는 도메인에 도메인 컨트롤러를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-128">You cannot add domain controllers to the managed domain.</span></span>

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-to-remotely-administer-the-managed-domain"></a><span data-ttu-id="ea086-129">작업 1 - 관리되는 도메인을 원격으로 관리하기 위해 도메인에 가입된 Windows Server 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="ea086-129">Task 1 - Provision a domain-joined Windows Server virtual machine to remotely administer the managed domain</span></span>
<span data-ttu-id="ea086-130">Azure AD 도메인 서비스 관리되는 도메인을 AD PowerShell 또는 ADAC(Active Directory 관리 센터)와 같은 친숙한 Active Directory 관리 도구를 사용하여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-130">Azure AD Domain Services managed domains can be managed using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="ea086-131">테넌트 관리자는 원격 데스크톱을 통해 관리되는 도메인의 도메인 컨트롤러에 연결할 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-131">Tenant administrators do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="ea086-132">따라서 'AAD DC 관리자' 그룹의 멤버는 관리되는 도메인에 가입된 Windows Server/클라이언트 컴퓨터에서 AD 관리 도구를 사용하여 관리되는 도메인을 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-132">Therefore, members of the 'AAD DC Administrators' group can administer managed domains remotely using AD administrative tools from a Windows Server/client computer that is joined to the managed domain.</span></span> <span data-ttu-id="ea086-133">AD 관리 도구는 관리되는 도메인에 가입된 클라이언트 컴퓨터 및 Windows Server에서 원격 서버 관리 도구(RSAT) 선택적 기능의 일부로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-133">AD administrative tools can be installed as part of the Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="ea086-134">첫 번째 단계는 관리되는 도메인에 가입된 Windows Server 가상 컴퓨터를 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-134">The first step is to set up a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="ea086-135">지침은 [Windows Server 가상 컴퓨터를 Azure AD 도메인 서비스 관리되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)이라는 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea086-135">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

### <a name="remotely-administer-the-managed-domain-from-a-client-computer-for-example-windows-10"></a><span data-ttu-id="ea086-136">클라이언트 컴퓨터(예: Windows 10)에서 관리되는 도메인을 원격으로 관리</span><span class="sxs-lookup"><span data-stu-id="ea086-136">Remotely administer the managed domain from a client computer (for example, Windows 10)</span></span>
<span data-ttu-id="ea086-137">이 문서의 지침에서는 AAD-DS 관리되는 도메인을 관리하기 위해 Windows Server 가상 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-137">The instructions in this article use a Windows Server virtual machine to administer the AAD-DS managed domain.</span></span> <span data-ttu-id="ea086-138">하지만 이 작업을 위해 Windows 클라이언트(예: Windows 10) 가상 컴퓨터를 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-138">However, you can also choose to use a Windows client (for example, Windows 10) virtual machine to do so.</span></span>

<span data-ttu-id="ea086-139">TechNet의 지침에 따라 Windows 클라이언트 가상 컴퓨터에 [원격 서버 관리 도구(RSAT)를 설치](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-139">You can [install Remote Server Administration Tools (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) on a Windows client virtual machine by following the instructions on TechNet.</span></span>

## <a name="task-2---install-active-directory-administration-tools-on-the-virtual-machine"></a><span data-ttu-id="ea086-140">작업 2 - 가상 컴퓨터에 Active Directory 관리 도구 설치</span><span class="sxs-lookup"><span data-stu-id="ea086-140">Task 2 - Install Active Directory administration tools on the virtual machine</span></span>
<span data-ttu-id="ea086-141">도메인에 가입된 가상 컴퓨터에 Active Directory 관리 도구를 설치하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-141">Perform the following steps to install the Active Directory Administration tools on the domain joined virtual machine.</span></span> <span data-ttu-id="ea086-142">[원격 서버 관리 도구 설치 및 사용](https://technet.microsoft.com/library/hh831501.aspx)에 대한 자세한 내용은 TechNet을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea086-142">See Technet for more [information on installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx).</span></span>

1. <span data-ttu-id="ea086-143">Azure 클래식 포털에서 **가상 컴퓨터** 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-143">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="ea086-144">작업 1에서 만든 가상 컴퓨터를 선택하고 창 아래쪽에 있는 명령 모음에서 **연결** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-144">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![Windows 가상 컴퓨터에 연결](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="ea086-146">클래식 포털에 가상 컴퓨터에 연결하는 데 사용되는 ‘.rdp’ 확장명을 가진 파일을 열거나 저장하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-146">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="ea086-147">다운로드가 완료되면 클릭하여 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-147">Click to open the file when it has finished downloading.</span></span>
3. <span data-ttu-id="ea086-148">로그인 프롬프트에서 'AAD DC 관리자' 그룹에 속한 사용자의 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-148">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="ea086-149">사용 예를 들어 'bob@domainservicespreview.onmicrosoft.com' 여기서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-149">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="ea086-150">시작 화면에서 **서버 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-150">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="ea086-151">서버 관리자 창의 가운데 창에서 **역할 및 기능 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-151">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![가상 컴퓨터에서 서버 관리자 시작](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="ea086-153">**역할 및 기능 추가 마법사**의 **시작하기 전에** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-153">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![시작하기 전에 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="ea086-155">**설치 유형** 페이지에서 **역할 기반 또는 기능 기반 설치** 옵션을 선택한 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-155">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![설치 유형 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="ea086-157">**서버 선택** 페이지에서 서버 풀의 현재 가상 컴퓨터를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-157">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![서버 선택 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="ea086-159">**서버 역할** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-159">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="ea086-160">서버에 어떠한 역할도 설치하지 않으므로 이 페이지는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-160">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="ea086-161">**기능** 페이지에서 **원격 서버 관리 도구** 노드를 클릭하여 확장한 후 **역할 관리 도구** 노드를 클릭하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-161">On the **Features** page, click to expand the **Remote Server Administration Tools** node and then click to expand the **Role Administration Tools** node.</span></span> <span data-ttu-id="ea086-162">역할 관리 도구 목록에서 **AD DS 및 AD LDS 도구** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-162">Select **AD DS and AD LDS Tools** feature from the list of role administration tools.</span></span>

    ![기능 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. <span data-ttu-id="ea086-164">**확인** 페이지에서 **설치**를 클릭하여 가상 컴퓨터에 AD 및 AD LDS 도구 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-164">On the **Confirmation** page, click **Install** to install the AD and AD LDS tools feature on the virtual machine.</span></span> <span data-ttu-id="ea086-165">기능 설치를 성공적으로 완료하면 **닫기**를 클릭하여 **역할 및 기능 추가** 마법사를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-165">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![확인 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-to-and-explore-the-managed-domain"></a><span data-ttu-id="ea086-167">작업 3 - 관리되는 도메인에 연결 및 탐색</span><span class="sxs-lookup"><span data-stu-id="ea086-167">Task 3 - Connect to and explore the managed domain</span></span>
<span data-ttu-id="ea086-168">이제 도메인에 가입된 가상 컴퓨터에 AD 관리 도구가 설치되었으므로 이러한 도구를 사용하여 관리되는 도메인을 탐색하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-168">Now that the AD Administrative Tools are installed on the domain joined virtual machine, we can use these tools to explore and administer the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="ea086-169">관리되는 도메인을 관리하려면 'AAD DC 관리자' 그룹의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-169">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain.</span></span>
>
>

1. <span data-ttu-id="ea086-170">시작 화면에서 **관리 도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-170">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="ea086-171">가상 컴퓨터에 설치된 AD 관리 도구가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-171">You should see the AD administrative tools installed on the virtual machine.</span></span>

    ![서버에 설치된 관리 도구](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. <span data-ttu-id="ea086-173">**Active Directory 관리 센터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-173">Click **Active Directory Administrative Center**.</span></span>

    ![Active Directory 관리 센터](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. <span data-ttu-id="ea086-175">도메인을 탐색하려면 왼쪽 창에서 도메인 이름(예: 'contoso100.com')을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-175">To explore the domain, click the domain name in the left pane (for example, 'contoso100.com').</span></span> <span data-ttu-id="ea086-176">각각 'AADDC 컴퓨터' 및 'AADDC 사용자'라는 두 개의 컨테이너를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-176">Notice two containers called 'AADDC Computers' and 'AADDC Users' respectively.</span></span>

    ![ADAC - 도메인 보기](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. <span data-ttu-id="ea086-178">**AADDC 사용자** 라는 컨테이너를 클릭하면 관리되는 도메인에 속하는 모든 사용자 및 그룹이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-178">Click the container called **AADDC Users** to see all users and groups belonging to the managed domain.</span></span> <span data-ttu-id="ea086-179">이 컨테이너에 표시되는 Azure AD 테넌트의 사용자 계정 및 그룹이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-179">You should see user accounts and groups from your Azure AD tenant show up in this container.</span></span> <span data-ttu-id="ea086-180">이 예에서는 'bob'이라는 사용자에 대한 사용자 계정 및 'AAD DC 관리자'라는 그룹이 이 컨테이너에 제공되는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-180">Notice in this example, a user account for the user called 'bob' and a group called 'AAD DC Administrators' are available in this container.</span></span>

    ![ADAC - 도메인 사용자](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. <span data-ttu-id="ea086-182">**AADDC 컴퓨터** 라는 컨테이너를 클릭하면 이 관리되는 도메인에 가입된 컴퓨터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-182">Click the container called **AADDC Computers** to see the computers joined to this managed domain.</span></span> <span data-ttu-id="ea086-183">도메인에 가입된 현재 가상 컴퓨터에 대한 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-183">You should see an entry for the current virtual machine, which is joined to the domain.</span></span> <span data-ttu-id="ea086-184">Azure AD 도메인 서비스 관리되는 도메인에 가입된 모든 컴퓨터에 대한 컴퓨터 계정이 이 'AADDC 컴퓨터' 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea086-184">Computer accounts for all computers that are joined to the Azure AD Domain Services managed domain are stored in this 'AADDC Computers' container.</span></span>

    ![ADAC - 도메인 가입 컴퓨터](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a><span data-ttu-id="ea086-186">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="ea086-186">Related Content</span></span>
* [<span data-ttu-id="ea086-187">Azure AD 도메인 서비스 - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="ea086-187">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="ea086-188">Windows Server 가상 컴퓨터를 Azure AD 도메인 서비스 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="ea086-188">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="ea086-189">원격 서버 관리 도구 배포</span><span class="sxs-lookup"><span data-stu-id="ea086-189">Deploy Remote Server Administration Tools</span></span>](https://technet.microsoft.com/library/hh831501.aspx)
