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
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a><span data-ttu-id="c0025-103">Azure Active Directory 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="c0025-103">Administer an Azure Active Directory Domain Services managed domain</span></span>
<span data-ttu-id="c0025-104">이 문서에서는 tooadminister Azure AD (Active Directory) 도메인 서비스 도메인을 관리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-104">This article shows you how tooadminister an Azure Active Directory (AD) Domain Services managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c0025-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c0025-105">Before you begin</span></span>
<span data-ttu-id="c0025-106">이 문서에 나열 된 tooperform hello 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-106">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="c0025-107">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="c0025-107">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="c0025-108">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-108">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="c0025-109">**Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-109">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="c0025-110">그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-110">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="c0025-111">A **가상 컴퓨터를 도메인에 가입 된** hello Azure AD 도메인 서비스 관리 되는 도메인에서 관리 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-111">A **domain-joined virtual machine** from which you administer hello Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="c0025-112">가상 컴퓨터에 없으면 hello 문서에 설명 된 모든 hello 작업에 따라 [Windows 가상 컴퓨터 tooa 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-112">If you don't have such a virtual machine, follow all hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="c0025-113">hello 자격 증명이 필요는 **사용자 계정이 속하는 toohello ' AAD DC Administrators' 그룹** tooadminister 디렉터리에 관리 되는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-113">You need hello credentials of a **user account belonging toohello 'AAD DC Administrators' group** in your directory, tooadminister your managed domain.</span></span>

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a><span data-ttu-id="c0025-114">관리되는 도메인에서 수행할 수 있는 관리 작업</span><span class="sxs-lookup"><span data-stu-id="c0025-114">Administrative tasks you can perform on a managed domain</span></span>
<span data-ttu-id="c0025-115">Hello ' AAD DC Administrators' 그룹의 구성원에 있는 tooperform 작업 같은 hello 관리 되는 도메인에 대 한 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-115">Members of hello 'AAD DC Administrators' group are granted privileges on hello managed domain that enable them tooperform tasks such as:</span></span>

* <span data-ttu-id="c0025-116">컴퓨터 toohello 관리 되는 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-116">Join machines toohello managed domain.</span></span>
* <span data-ttu-id="c0025-117">Hello 관리 되는 도메인에서 hello hello ' AADDC 컴퓨터 ' 및 ' AADDC Users' 컨테이너에 대 한 기본 제공 GPO를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-117">Configure hello built-in GPO for hello 'AADDC Computers' and 'AADDC Users' containers in hello managed domain.</span></span>
* <span data-ttu-id="c0025-118">Hello 관리 되는 도메인의 DNS을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-118">Administer DNS on hello managed domain.</span></span>
* <span data-ttu-id="c0025-119">만들고 hello 관리 되는 도메인에서 사용자 지정 조직 구성 단위 (Ou)를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-119">Create and administer custom Organizational Units (OUs) on hello managed domain.</span></span>
* <span data-ttu-id="c0025-120">관리 액세스 toocomputers 이득 toohello 관리 되는 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-120">Gain administrative access toocomputers joined toohello managed domain.</span></span>

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a><span data-ttu-id="c0025-121">관리되는 도메인에 없는 관리자 권한</span><span class="sxs-lookup"><span data-stu-id="c0025-121">Administrative privileges you do not have on a managed domain</span></span>
<span data-ttu-id="c0025-122">hello 도메인 패치 적용, 모니터링 및, 백업을 수행 하는 등의 작업을 포함 하 여 Microsoft에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-122">hello domain is managed by Microsoft, including activities such as patching, monitoring and, performing backups.</span></span> <span data-ttu-id="c0025-123">따라서 hello 도메인은 잠겨 있으며 및 없는 권한 tooperform 특정 관리 작업도 hello 도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-123">Therefore, hello domain is locked down and you do not have privileges tooperform certain administrative tasks on hello domain.</span></span> <span data-ttu-id="c0025-124">수행할 수 없는 작업의 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-124">Some examples of tasks you cannot perform are below.</span></span>

* <span data-ttu-id="c0025-125">Hello 관리 되는 도메인에 도메인 관리자 또는 엔터프라이즈 관리자 권한이 부여 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-125">You are not granted Domain Administrator or Enterprise Administrator privileges for hello managed domain.</span></span>
* <span data-ttu-id="c0025-126">Hello 관리 되는 도메인의 hello 스키마를 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-126">You cannot extend hello schema of hello managed domain.</span></span>
* <span data-ttu-id="c0025-127">원격 데스크톱을 사용 하 여 hello 관리 되는 도메인에 대 한 toodomain 컨트롤러를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-127">You cannot connect toodomain controllers for hello managed domain using Remote Desktop.</span></span>
* <span data-ttu-id="c0025-128">도메인 컨트롤러 toohello 관리 되는 도메인을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-128">You cannot add domain controllers toohello managed domain.</span></span>

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a><span data-ttu-id="c0025-129">작업 1-프로 비전 도메인에 가입 된 Windows Server 가상 컴퓨터 tooremotely hello 관리 되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="c0025-129">Task 1 - Provision a domain-joined Windows Server virtual machine tooremotely administer hello managed domain</span></span>
<span data-ttu-id="c0025-130">Hello ADAC Active Directory 관리 센터 () 또는 AD PowerShell과 같은 친숙 한 Active Directory 관리 도구를 사용 하 여 azure AD 도메인 서비스 관리 되는 도메인을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-130">Azure AD Domain Services managed domains can be managed using familiar Active Directory administrative tools such as hello Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="c0025-131">테 넌 트 관리자에 원격 데스크톱을 통해 관리 되는 도메인 hello 권한 tooconnect toodomain 컨트롤러를 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-131">Tenant administrators do not have privileges tooconnect toodomain controllers on hello managed domain via Remote Desktop.</span></span> <span data-ttu-id="c0025-132">따라서 hello ' AAD DC Administrators' 그룹을 관리할 수의 구성원이 원격으로 관리 되는 도메인에 가입된 toohello 되는 Windows 서버/클라이언트 컴퓨터에서 AD 관리 도구를 사용 하 여 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-132">Therefore, members of hello 'AAD DC Administrators' group can administer managed domains remotely using AD administrative tools from a Windows Server/client computer that is joined toohello managed domain.</span></span> <span data-ttu-id="c0025-133">Windows 서버 및 클라이언트 컴퓨터에 원격 서버 관리 도구 (RSAT) 선택적 기능 hello 부분의 toohello 관리 되는 도메인에 가입 AD 관리 도구를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-133">AD administrative tools can be installed as part of hello Remote Server Administration Tools (RSAT) optional feature on Windows Server and client machines joined toohello managed domain.</span></span>

<span data-ttu-id="c0025-134">hello 첫 번째 단계는 관리 되는 조인 된 toohello 도메인은 Windows Server 가상 컴퓨터를 tooset입니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-134">hello first step is tooset up a Windows Server virtual machine that is joined toohello managed domain.</span></span> <span data-ttu-id="c0025-135">자세한 내용은 toohello 문서를 참조 [Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-135">For instructions, refer toohello article titled [join a Windows Server virtual machine tooan Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a><span data-ttu-id="c0025-136">클라이언트 컴퓨터 (예를 들어 Windows 10)에서 관리 되는 도메인 hello를 원격으로 관리</span><span class="sxs-lookup"><span data-stu-id="c0025-136">Remotely administer hello managed domain from a client computer (for example, Windows 10)</span></span>
<span data-ttu-id="c0025-137">이 문서 사용 하 여 Windows Server 가상 컴퓨터 tooadminister hello AAD DS의에서 hello 지침 도메인을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-137">hello instructions in this article use a Windows Server virtual machine tooadminister hello AAD-DS managed domain.</span></span> <span data-ttu-id="c0025-138">그러나 수도 있습니다 toouse Windows 클라이언트 (예를 들어 Windows 10) 가상 컴퓨터 toodo 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-138">However, you can also choose toouse a Windows client (for example, Windows 10) virtual machine toodo so.</span></span>

<span data-ttu-id="c0025-139">있습니다 수 [원격 서버 관리 도구 (RSAT)를 설치](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) technet hello 지침에 따라 Windows 클라이언트 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="c0025-139">You can [install Remote Server Administration Tools (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) on a Windows client virtual machine by following hello instructions on TechNet.</span></span>

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a><span data-ttu-id="c0025-140">작업 2-hello 가상 컴퓨터에 설치 Active Directory 관리 도구</span><span class="sxs-lookup"><span data-stu-id="c0025-140">Task 2 - Install Active Directory administration tools on hello virtual machine</span></span>
<span data-ttu-id="c0025-141">Hello 단계 tooinstall hello Active Directory 관리 도구 hello 도메인에 가입 된 가상 컴퓨터에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-141">Perform hello following steps tooinstall hello Active Directory Administration tools on hello domain joined virtual machine.</span></span> <span data-ttu-id="c0025-142">[원격 서버 관리 도구 설치 및 사용](https://technet.microsoft.com/library/hh831501.aspx)에 대한 자세한 내용은 TechNet을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0025-142">See Technet for more [information on installing and using Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx).</span></span>

1. <span data-ttu-id="c0025-143">너무 이동**가상 컴퓨터** hello Azure 클래식 포털에서에서 노드.</span><span class="sxs-lookup"><span data-stu-id="c0025-143">Navigate too**Virtual Machines** node in hello Azure classic portal.</span></span> <span data-ttu-id="c0025-144">작업 1에서 만든 hello 가상 컴퓨터를 선택 하 고 클릭 **연결** hello hello 창 맨 아래에 hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-144">Select hello virtual machine you created in Task 1 and click **Connect** on hello command bar at hello bottom of hello window.</span></span>

    ![TooWindows 가상 컴퓨터에 연결](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="c0025-146">hello 클래식 포털 묻는 tooopen 또는 변수인 사용 되는 tooconnect toohello 가상 컴퓨터 '.rdp' 확장명을 가진 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-146">hello classic portal prompts you tooopen or save a file with a '.rdp' extension, which is used tooconnect toohello virtual machine.</span></span> <span data-ttu-id="c0025-147">다운로드를 마쳤을 때 tooopen hello 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-147">Click tooopen hello file when it has finished downloading.</span></span>
3. <span data-ttu-id="c0025-148">Hello 로그인 프롬프트 toohello ' AAD DC Administrators' 그룹에 속한 사용자의 hello 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-148">At hello login prompt, use hello credentials of a user belonging toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="c0025-149">사용 예를 들어 'bob@domainservicespreview.onmicrosoft.com' 여기서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-149">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="c0025-150">Hello 시작 화면에서 엽니다 **서버 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-150">From hello Start screen, open **Server Manager**.</span></span> <span data-ttu-id="c0025-151">클릭 **역할 및 기능 추가** hello 중앙 창의 hello 서버 관리자 창에서.</span><span class="sxs-lookup"><span data-stu-id="c0025-151">Click **Add Roles and Features** in hello central pane of hello Server Manager window.</span></span>

    ![가상 컴퓨터에서 서버 관리자 시작](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="c0025-153">Hello에 **시작 하기 전에** hello 페이지 **추가 역할 및 기능 마법사**, 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-153">On hello **Before You Begin** page of hello **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![시작하기 전에 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="c0025-155">Hello에 **설치 유형을** 페이지에서 hello **역할 기반 또는 기능 기반 설치** 옵션을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-155">On hello **Installation Type** page, leave hello **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![설치 유형 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="c0025-157">Hello에 **서버 선택** 페이지 hello 서버 풀의 hello 현재 가상 컴퓨터를 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-157">On hello **Server Selection** page, select hello current virtual machine from hello server pool, and click **Next**.</span></span>

    ![서버 선택 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="c0025-159">Hello에 **서버 역할** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-159">On hello **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="c0025-160">에서는 이후 hello 서버에 있는 모든 역할 설치 하지 않는 것이 페이지를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-160">We skip this page since we are not installing any roles on hello server.</span></span>
9. <span data-ttu-id="c0025-161">Hello에 **기능** 페이지에서 tooexpand hello **원격 서버 관리 도구** 노드 tooexpand hello를 클릭 한 다음 **역할 관리 도구** 노드.</span><span class="sxs-lookup"><span data-stu-id="c0025-161">On hello **Features** page, click tooexpand hello **Remote Server Administration Tools** node and then click tooexpand hello **Role Administration Tools** node.</span></span> <span data-ttu-id="c0025-162">선택 **AD DS 및 AD LDS 도구** hello 역할 관리 도구 목록에서 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-162">Select **AD DS and AD LDS Tools** feature from hello list of role administration tools.</span></span>

    ![기능 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. <span data-ttu-id="c0025-164">Hello에 **확인** 페이지 **설치** hello 가상 컴퓨터에서 tooinstall hello AD와 AD LDS 도구 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-164">On hello **Confirmation** page, click **Install** tooinstall hello AD and AD LDS tools feature on hello virtual machine.</span></span> <span data-ttu-id="c0025-165">기능 설치가 완료 되 면 클릭 **닫기** tooexit hello **역할 및 기능 추가** 마법사.</span><span class="sxs-lookup"><span data-stu-id="c0025-165">When feature installation completes successfully, click **Close** tooexit hello **Add Roles and Features** wizard.</span></span>

    ![확인 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a><span data-ttu-id="c0025-167">작업 3-tooand 연결 hello 관리 되는 도메인 탐색</span><span class="sxs-lookup"><span data-stu-id="c0025-167">Task 3 - Connect tooand explore hello managed domain</span></span>
<span data-ttu-id="c0025-168">Hello AD 관리 도구가 설치 되어 했으므로 hello에 도메인에 가입 된 가상 컴퓨터, 이러한 도구 tooexplore를 사용 하 여를 hello 관리 되는 도메인을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-168">Now that hello AD Administrative Tools are installed on hello domain joined virtual machine, we can use these tools tooexplore and administer hello managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="c0025-169">구성원 toobe 필요한 tooadminister hello hello ' AAD DC Administrators' 그룹의 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-169">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister hello managed domain.</span></span>
>
>

1. <span data-ttu-id="c0025-170">Hello 시작 화면에서 클릭 **관리 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-170">From hello Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="c0025-171">Hello 가상 컴퓨터에 설치 하는 hello AD 관리 도구 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-171">You should see hello AD administrative tools installed on hello virtual machine.</span></span>

    ![서버에 설치된 관리 도구](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. <span data-ttu-id="c0025-173">**Active Directory 관리 센터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-173">Click **Active Directory Administrative Center**.</span></span>

    ![Active Directory 관리 센터](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. <span data-ttu-id="c0025-175">tooexplore hello 도메인 (예를 들어 ' contoso100.com') hello 왼쪽된 창에서 hello 도메인 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-175">tooexplore hello domain, click hello domain name in hello left pane (for example, 'contoso100.com').</span></span> <span data-ttu-id="c0025-176">각각 'AADDC 컴퓨터' 및 'AADDC 사용자'라는 두 개의 컨테이너를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-176">Notice two containers called 'AADDC Computers' and 'AADDC Users' respectively.</span></span>

    ![ADAC - 도메인 보기](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. <span data-ttu-id="c0025-178">호출 하는 hello 컨테이너를 클릭 **AADDC 사용자** toosee 관리 되는 모든 사용자 및 그룹 toohello 속한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-178">Click hello container called **AADDC Users** toosee all users and groups belonging toohello managed domain.</span></span> <span data-ttu-id="c0025-179">이 컨테이너에 표시되는 Azure AD 테넌트의 사용자 계정 및 그룹이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-179">You should see user accounts and groups from your Azure AD tenant show up in this container.</span></span> <span data-ttu-id="c0025-180">이 예에서는, 'bob' 라고 하는 hello 사용자 및 ' AAD DC Administrators' 그룹에 대 한 사용자 계정에는이 컨테이너에서 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-180">Notice in this example, a user account for hello user called 'bob' and a group called 'AAD DC Administrators' are available in this container.</span></span>

    ![ADAC - 도메인 사용자](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. <span data-ttu-id="c0025-182">호출 하는 hello 컨테이너를 클릭 **AADDC 컴퓨터** toosee hello 컴퓨터 toothis 관리 되는 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-182">Click hello container called **AADDC Computers** toosee hello computers joined toothis managed domain.</span></span> <span data-ttu-id="c0025-183">도메인에 가입된 toohello hello 현재 가상 컴퓨터에 대 한 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-183">You should see an entry for hello current virtual machine, which is joined toohello domain.</span></span> <span data-ttu-id="c0025-184">모든 컴퓨터에 대 한 컴퓨터 계정을 조인 toohello Azure AD 도메인 서비스를 관리 되는 도메인이 ' AADDC 컴퓨터 ' 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0025-184">Computer accounts for all computers that are joined toohello Azure AD Domain Services managed domain are stored in this 'AADDC Computers' container.</span></span>

    ![ADAC - 도메인 가입 컴퓨터](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a><span data-ttu-id="c0025-186">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="c0025-186">Related Content</span></span>
* [<span data-ttu-id="c0025-187">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="c0025-187">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="c0025-188">Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="c0025-188">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="c0025-189">원격 서버 관리 도구 배포</span><span class="sxs-lookup"><span data-stu-id="c0025-189">Deploy Remote Server Administration Tools</span></span>](https://technet.microsoft.com/library/hh831501.aspx)
