---
title: "Azure Active Directory Domain Services: 관리되는 도메인에서 그룹 정책 관리 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서 그룹 정책 관리"
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
ms.openlocfilehash: 299e09ef1bb1b1db9d64447bf4537c7c3a3cfd5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="59d04-103">Azure AD Domain Services 관리되는 도메인에서 그룹 정책 관리</span><span class="sxs-lookup"><span data-stu-id="59d04-103">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="59d04-104">Azure Active Directory Domain Services는 'AADDC 사용자' 및 'AADDC 컴퓨터' 컨테이너에 대한 기본 제공 GPO(그룹 정책 개체)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for the 'AADDC Users' and 'AADDC Computers' containers.</span></span> <span data-ttu-id="59d04-105">이러한 기본 제공 GPO를 사용자 지정하여 관리되는 도메인에서 그룹 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-105">You can customize these built-in GPOs to configure Group Policy on the managed domain.</span></span> <span data-ttu-id="59d04-106">또한 'AAD DC 관리자' 그룹의 구성원은 관리되는 도메인에서 자체 사용자 지정 OU를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-106">Additionally, members of the 'AAD DC Administrators' group can create their own custom OUs in the managed domain.</span></span> <span data-ttu-id="59d04-107">사용자 지정 GPO을 만들고 이러한 사용자 지정 OU에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-107">They can also create custom GPOs and link them to these custom OUs.</span></span> <span data-ttu-id="59d04-108">'AAD DC 관리자' 그룹에 속한 사용자에게 관리되는 도메인에 대한 그룹 정책 관리 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-108">Users who belong to the 'AAD DC Administrators' group are granted Group Policy administration privileges on the managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59d04-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="59d04-109">Before you begin</span></span>
<span data-ttu-id="59d04-110">이 문서에 나열된 작업을 수행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-110">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="59d04-111">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="59d04-111">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="59d04-112">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="59d04-113">**Azure AD 도메인 서비스** 를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="59d04-114">그렇지 않은 경우 [시작 가이드](active-directory-ds-getting-started.md)에 간략히 설명된 모든 작업을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="59d04-115">Azure AD 도메인 서비스 관리되는 도메인을 관리하게 될 **도메인에 가입된 가상 컴퓨터** .</span><span class="sxs-lookup"><span data-stu-id="59d04-115">A **domain-joined virtual machine** from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="59d04-116">이러한 가상 컴퓨터가 없는 경우 [Windows 가상 컴퓨터를 관리되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)문서에 설명된 모든 작업을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="59d04-116">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="59d04-117">관리되는 도메인에 대한 그룹 정책을 관리하려면 디렉터리의 **'AAD DC 관리자' 그룹에 속한 사용자 계정**의 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-117">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to administer Group Policy for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-to-remotely-administer-group-policy-for-the-managed-domain"></a><span data-ttu-id="59d04-118">작업 1 - 관리되는 도메인에 대한 그룹 정책을 원격으로 관리하기 위해 도메인에 가입된 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="59d04-118">Task 1 - Provision a domain-joined virtual machine to remotely administer Group Policy for the managed domain</span></span>
<span data-ttu-id="59d04-119">Azure AD 도메인 서비스 관리되는 도메인을 AD PowerShell 또는 ADAC(Active Directory 관리 센터)와 같은 친숙한 Active Directory 관리 도구를 사용하여 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="59d04-120">마찬가지로, 그룹 정책 관리 도구를 사용하여 관리되는 도메인에 대한 그룹 정책을 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-120">Similarly, Group Policy for the managed domain can be administered remotely using the Group Policy administration tools.</span></span>

<span data-ttu-id="59d04-121">Azure AD 디렉터리의 테넌트 관리자는 원격 데스크톱을 통해 관리되는 도메인의 도메인 컨트롤러에 연결할 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-121">Administrators in your Azure AD directory do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="59d04-122">'AAD DC 관리자' 그룹의 구성원은 관리되는 도메인에 대한 그룹 정책을 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-122">Members of the 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span></span> <span data-ttu-id="59d04-123">관리되는 도메인에 가입된 Windows 서버/클라이언트 컴퓨터의 그룹 정책 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-123">They can use Group Policy tools on a Windows Server/client computer joined to the managed domain.</span></span> <span data-ttu-id="59d04-124">그룹 정책 도구는 관리되는 도메인에 가입된 클라이언트 컴퓨터 및 Windows Server에서 그룹 정책 관리 선택적 기능의 일부로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-124">Group Policy tools can be installed as part of the Group Policy Management optional feature on Windows Server and client machines joined to the managed domain.</span></span>

<span data-ttu-id="59d04-125">Windows Server 가상 컴퓨터를 프로비전하기 위한 첫 번째 작업은 관리되는 도메인에 가입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-125">The first task is to provision a Windows Server virtual machine that is joined to the managed domain.</span></span> <span data-ttu-id="59d04-126">지침은 [Windows Server 가상 컴퓨터를 Azure AD 도메인 서비스 관리되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)이라는 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d04-126">For instructions, refer to the article titled [join a Windows Server virtual machine to an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-group-policy-tools-on-the-virtual-machine"></a><span data-ttu-id="59d04-127">작업 2 - 가상 컴퓨터에 그룹 정책 도구 설치</span><span class="sxs-lookup"><span data-stu-id="59d04-127">Task 2 - Install Group Policy tools on the virtual machine</span></span>
<span data-ttu-id="59d04-128">도메인에 가입된 가상 컴퓨터에 그룹 정책 관리 도구를 설치하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-128">Perform the following steps to install the Group Policy Administration tools on the domain joined virtual machine.</span></span>

1. <span data-ttu-id="59d04-129">Azure 클래식 포털에서 **가상 컴퓨터** 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-129">Navigate to **Virtual Machines** node in the Azure classic portal.</span></span> <span data-ttu-id="59d04-130">작업 1에서 만든 가상 컴퓨터를 선택하고 창 아래쪽에 있는 명령 모음에서 **연결** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-130">Select the virtual machine you created in Task 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![Windows 가상 컴퓨터에 연결](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="59d04-132">클래식 포털에 가상 컴퓨터에 연결하는 데 사용되는 ‘.rdp’ 확장명을 가진 파일을 열거나 저장하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-132">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="59d04-133">다운로드가 완료되면 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-133">Click the file when it has finished downloading.</span></span>
3. <span data-ttu-id="59d04-134">로그인 프롬프트에서 'AAD DC 관리자' 그룹에 속한 사용자의 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-134">At the login prompt, use the credentials of a user belonging to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="59d04-135">사용 예를 들어 'bob@domainservicespreview.onmicrosoft.com' 여기서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-135">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="59d04-136">시작 화면에서 **서버 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-136">From the Start screen, open **Server Manager**.</span></span> <span data-ttu-id="59d04-137">서버 관리자 창의 가운데 창에서 **역할 및 기능 추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-137">Click **Add Roles and Features** in the central pane of the Server Manager window.</span></span>

    ![가상 컴퓨터에서 서버 관리자 시작](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="59d04-139">**역할 및 기능 추가 마법사**의 **시작하기 전에** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-139">On the **Before You Begin** page of the **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![시작하기 전에 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="59d04-141">**설치 유형** 페이지에서 **역할 기반 또는 기능 기반 설치** 옵션을 선택한 상태로 두고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-141">On the **Installation Type** page, leave the **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![설치 유형 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="59d04-143">**서버 선택** 페이지에서 서버 풀의 현재 가상 컴퓨터를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-143">On the **Server Selection** page, select the current virtual machine from the server pool, and click **Next**.</span></span>

    ![서버 선택 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="59d04-145">**서버 역할** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-145">On the **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="59d04-146">서버에 어떠한 역할도 설치하지 않으므로 이 페이지는 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-146">We skip this page since we are not installing any roles on the server.</span></span>
9. <span data-ttu-id="59d04-147">**기능** 페이지에서 **그룹 정책 관리** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-147">On the **Features** page, select the **Group Policy Management** feature.</span></span>

    ![기능 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. <span data-ttu-id="59d04-149">**확인** 페이지에서 가상 컴퓨터에 그룹 정책 관리 기능을 설치하기 위해 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-149">On the **Confirmation** page, click **Install** to install the Group Policy Management feature on the virtual machine.</span></span> <span data-ttu-id="59d04-150">기능 설치를 성공적으로 완료하면 **닫기**를 클릭하여 **역할 및 기능 추가** 마법사를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-150">When feature installation completes successfully, click **Close** to exit the **Add Roles and Features** wizard.</span></span>

    ![확인 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-the-group-policy-management-console-to-administer-group-policy"></a><span data-ttu-id="59d04-152">작업 3 - 그룹 정책을 관리하는 그룹 정책 관리 콘솔 시작</span><span class="sxs-lookup"><span data-stu-id="59d04-152">Task 3 - Launch the Group Policy management console to administer Group Policy</span></span>
<span data-ttu-id="59d04-153">도메인에 가입된 가상 컴퓨터에서 그룹 정책 관리 콘솔을 사용하여 관리되는 도메인에서 그룹 정책을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-153">You can use the Group Policy management console on the domain-joined virtual machine to administer Group Policy on the managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="59d04-154">관리되는 도메인의 그룹 정책을 관리하려면 'AAD DC 관리자' 그룹의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-154">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="59d04-155">시작 화면에서 **관리 도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-155">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="59d04-156">가상 컴퓨터에 설치된 **그룹 정책 관리** 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-156">You should see the **Group Policy Management** console installed on the virtual machine.</span></span>

    ![그룹 정책 관리 시작](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. <span data-ttu-id="59d04-158">**그룹 정책 관리**를 클릭하여 그룹 정책 관리 콘솔을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-158">Click **Group Policy Management** to launch the Group Policy Management console.</span></span>

    ![그룹 정책 콘솔](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a><span data-ttu-id="59d04-160">작업 4 - 기본 제공 그룹 정책 개체 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="59d04-160">Task 4 - Customize built-in Group Policy Objects</span></span>
<span data-ttu-id="59d04-161">관리되는 도메인에서 'AADDC 컴퓨터' 및 'AADDC 사용자' 컨테이너 각각에 대한 두 개의 기본 제공 GPO(그룹 정책 개체)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-161">There are two built-in Group Policy Objects (GPOs) - one each for the 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span></span> <span data-ttu-id="59d04-162">이러한 GPO를 사용자 지정하여 관리되는 도메인에서 그룹 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-162">You can customize these GPOs to configure group policy on the managed domain.</span></span>

1. <span data-ttu-id="59d04-163">**그룹 정책 관리** 콘솔에서 **포리스트: contoso100.com** 및 **도메인** 노드를 클릭하여 확장하고 관리되는 도메인에 대한 그룹 정책을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-163">In the **Group Policy Management** console, click to expand the **Forest: contoso100.com** and **Domains** nodes to see the group policies for your managed domain.</span></span>

    ![기본 제공 GPO](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. <span data-ttu-id="59d04-165">이러한 기본 제공 GPO를 사용자 지정하여 관리되는 도메인에서 그룹 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-165">You can customize these built-in GPOs to configure group policies on your managed domain.</span></span> <span data-ttu-id="59d04-166">GPO를 마우스 오른쪽 단추로 클릭하고 **편집...**을 클릭하여 기본 제공 GPO를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-166">Right-click the GPO and click **Edit...** to customize the built-in GPO.</span></span> <span data-ttu-id="59d04-167">그룹 정책 구성 편집기 도구를 사용하여 GPO를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-167">The Group Policy Configuration Editor tool enables you to customize the GPO.</span></span>

    ![기본 제공 GPO 편집](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. <span data-ttu-id="59d04-169">이제 **그룹 정책 관리 편집기** 콘솔을 사용하여 기본 제공 GPO를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-169">You can now use the **Group Policy Management Editor** console to edit the built-in GPO.</span></span> <span data-ttu-id="59d04-170">예를 들어 다음 스크린샷은 기본 제공 'AADDC 컴퓨터' GPO를 사용자 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-170">For instance, the following screenshot shows how to customize the built-in 'AADDC Computers' GPO.</span></span>

    ![GPO 사용자 지정](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a><span data-ttu-id="59d04-172">작업 5 - 사용자 지정 GPO(그룹 정책 개체) 만들기</span><span class="sxs-lookup"><span data-stu-id="59d04-172">Task 5 - Create a custom Group Policy Object (GPO)</span></span>
<span data-ttu-id="59d04-173">사용자 지정 그룹 정책 개체를 만들거나 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-173">You can create or import your own custom group policy objects.</span></span> <span data-ttu-id="59d04-174">사용자 지정 GPO를 관리되는 도메인에서 만든 사용자 지정 OU에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-174">You can also link custom GPOs to a custom OU you have created in your managed domain.</span></span> <span data-ttu-id="59d04-175">사용자 지정 조직 구성 단위를 만드는 방법에 대한 자세한 내용은 [관리되는 도메인에서 사용자 지정 OU 만들기](active-directory-ds-admin-guide-create-ou.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59d04-175">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span></span>

> [!NOTE]
> <span data-ttu-id="59d04-176">관리되는 도메인의 그룹 정책을 관리하려면 'AAD DC 관리자' 그룹의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-176">You need to be a member of the 'AAD DC Administrators' group, to administer Group Policy on the managed domain.</span></span>
>
>

1. <span data-ttu-id="59d04-177">**그룹 정책 관리** 콘솔에서 사용자 지정 조직 구성 단위(OU)를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-177">In the **Group Policy Management** console, click to select your custom organizational unit (OU).</span></span> <span data-ttu-id="59d04-178">OU를 마우스 오른쪽 단추로 클릭하고 **이 도메인에서 GPO를 만들어 여기에 연결...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-178">Right-click the OU and click **Create a GPO in this domain, and Link it here...**.</span></span>

    ![사용자 지정 GPO 만들기](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. <span data-ttu-id="59d04-180">새 GPO의 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-180">Specify a name for the new GPO and click **OK**.</span></span>

    ![GPO의 이름 지정](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. <span data-ttu-id="59d04-182">새 GPO가 만들어지고 사용자 지정 OU로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-182">A new GPO is created and linked to your custom OU.</span></span> <span data-ttu-id="59d04-183">GPO를 마우스 오른쪽 단추로 클릭하고 메뉴에서 **편집...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-183">Right-click the GPO and click **Edit...** from the menu.</span></span>

    ![새로 만든 GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. <span data-ttu-id="59d04-185">새로 만든 GPO는 **그룹 정책 관리 편집기**를 사용하여 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-185">You can customize the newly created GPO using the **Group Policy Management Editor**.</span></span>

    ![새 GPO 사용자 지정](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


<span data-ttu-id="59d04-187">[그룹 정책 관리 콘솔](https://technet.microsoft.com/library/cc753298.aspx) 사용에 대한 자세한 내용은 Technet에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59d04-187">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span></span>

## <a name="related-content"></a><span data-ttu-id="59d04-188">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="59d04-188">Related Content</span></span>
* [<span data-ttu-id="59d04-189">Azure AD 도메인 서비스 - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="59d04-189">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="59d04-190">Windows Server 가상 컴퓨터를 Azure AD 도메인 서비스 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="59d04-190">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="59d04-191">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="59d04-191">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="59d04-192">그룹 정책 관리 콘솔</span><span class="sxs-lookup"><span data-stu-id="59d04-192">Group Policy Management Console</span></span>](https://technet.microsoft.com/library/cc753298.aspx)
