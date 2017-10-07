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
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="4029f-103">Azure AD Domain Services 관리되는 도메인에서 그룹 정책 관리</span><span class="sxs-lookup"><span data-stu-id="4029f-103">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="4029f-104">Azure Active Directory 도메인 서비스는 hello ' AADDC 사용자 ' 및 ' AADDC 컴퓨터 ' 컨테이너에 대 한 기본 제공 그룹 정책 개체 (Gpo)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-104">Azure Active Directory Domain Services includes built-in Group Policy Objects (GPOs) for hello 'AADDC Users' and 'AADDC Computers' containers.</span></span> <span data-ttu-id="4029f-105">이러한 기본 제공 Gpo tooconfigure hello 관리 되는 도메인의 그룹 정책은 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-105">You can customize these built-in GPOs tooconfigure Group Policy on hello managed domain.</span></span> <span data-ttu-id="4029f-106">또한 hello ' AAD DC Administrators' 그룹의 구성원 hello 관리 되는 도메인에 자체 사용자 지정 Ou를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-106">Additionally, members of hello 'AAD DC Administrators' group can create their own custom OUs in hello managed domain.</span></span> <span data-ttu-id="4029f-107">사용자 지정 Gpo를 만들 수 있고 toothese 사용자 지정 연결은 Ou입니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-107">They can also create custom GPOs and link them toothese custom OUs.</span></span> <span data-ttu-id="4029f-108">Toohello ' AAD DC Administrators' 그룹에 속한 사용자는 hello 관리 되는 도메인에 대 한 그룹 정책 관리 권한은 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-108">Users who belong toohello 'AAD DC Administrators' group are granted Group Policy administration privileges on hello managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4029f-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4029f-109">Before you begin</span></span>
<span data-ttu-id="4029f-110">이 문서에 나열 된 tooperform hello 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-110">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="4029f-111">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="4029f-111">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="4029f-112">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-112">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="4029f-113">**Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-113">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="4029f-114">그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-114">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="4029f-115">A **가상 컴퓨터를 도메인에 가입 된** hello Azure AD 도메인 서비스 관리 되는 도메인에서 관리 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-115">A **domain-joined virtual machine** from which you administer hello Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="4029f-116">가상 컴퓨터에 없으면 hello 문서에 설명 된 모든 hello 작업에 따라 [Windows 가상 컴퓨터 tooa 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-116">If you don't have such a virtual machine, follow all hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="4029f-117">hello 자격 증명이 필요는 **사용자 계정이 속하는 toohello ' AAD DC Administrators' 그룹** tooadminister 그룹 정책 관리 되는 도메인에 대 한 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-117">You need hello credentials of a **user account belonging toohello 'AAD DC Administrators' group** in your directory, tooadminister Group Policy for your managed domain.</span></span>

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a><span data-ttu-id="4029f-118">작업 1-프로 비전 한 가상 컴퓨터를 도메인에 가입 된 tooremotely hello 관리 되는 도메인에 대 한 그룹 정책 관리</span><span class="sxs-lookup"><span data-stu-id="4029f-118">Task 1 - Provision a domain-joined virtual machine tooremotely administer Group Policy for hello managed domain</span></span>
<span data-ttu-id="4029f-119">Azure AD 도메인 서비스 관리 되는 도메인 hello AD PowerShell 또는 관리 센터 ADAC (Active Directory)와 같은 친숙 한 Active Directory 관리 도구를 사용 하 여 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-119">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as hello Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="4029f-120">마찬가지로, hello 관리 되는 도메인에 대 한 그룹 정책은 hello 그룹 정책 관리 도구를 사용 하 여 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-120">Similarly, Group Policy for hello managed domain can be administered remotely using hello Group Policy administration tools.</span></span>

<span data-ttu-id="4029f-121">Azure AD 디렉터리의 관리자가 원격 데스크톱을 통해 관리 되는 도메인 hello에 권한이 tooconnect toodomain 컨트롤러를 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-121">Administrators in your Azure AD directory do not have privileges tooconnect toodomain controllers on hello managed domain via Remote Desktop.</span></span> <span data-ttu-id="4029f-122">Hello ' AAD DC Administrators' 그룹의 멤버는 관리 되는 도메인에 대 한 원격으로 그룹 정책을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-122">Members of hello 'AAD DC Administrators' group can administer Group Policy for managed domains remotely.</span></span> <span data-ttu-id="4029f-123">Windows 서버/클라이언트 컴퓨터에 가입된 toohello 관리 되는 도메인에서 그룹 정책 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-123">They can use Group Policy tools on a Windows Server/client computer joined toohello managed domain.</span></span> <span data-ttu-id="4029f-124">Hello Windows 서버 및 클라이언트 컴퓨터에 선택적 기능 그룹 정책 관리의 일부 toohello 관리 되는 도메인에 가입 그룹 정책 도구를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-124">Group Policy tools can be installed as part of hello Group Policy Management optional feature on Windows Server and client machines joined toohello managed domain.</span></span>

<span data-ttu-id="4029f-125">hello 첫 번째 작업은 관리 되는 도메인에 가입된 toohello 되는 Windows Server 가상 컴퓨터 tooprovision입니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-125">hello first task is tooprovision a Windows Server virtual machine that is joined toohello managed domain.</span></span> <span data-ttu-id="4029f-126">자세한 내용은 toohello 문서를 참조 [Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-126">For instructions, refer toohello article titled [join a Windows Server virtual machine tooan Azure AD Domain Services managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a><span data-ttu-id="4029f-127">작업 2-hello 가상 컴퓨터에 설치 그룹 정책 도구</span><span class="sxs-lookup"><span data-stu-id="4029f-127">Task 2 - Install Group Policy tools on hello virtual machine</span></span>
<span data-ttu-id="4029f-128">Hello 단계 tooinstall hello 그룹 정책 관리 도구 hello 도메인에 가입 된 가상 컴퓨터에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-128">Perform hello following steps tooinstall hello Group Policy Administration tools on hello domain joined virtual machine.</span></span>

1. <span data-ttu-id="4029f-129">너무 이동**가상 컴퓨터** hello Azure 클래식 포털에서에서 노드.</span><span class="sxs-lookup"><span data-stu-id="4029f-129">Navigate too**Virtual Machines** node in hello Azure classic portal.</span></span> <span data-ttu-id="4029f-130">작업 1에서 만든 hello 가상 컴퓨터를 선택 하 고 클릭 **연결** hello hello 창 맨 아래에 hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-130">Select hello virtual machine you created in Task 1 and click **Connect** on hello command bar at hello bottom of hello window.</span></span>

    ![TooWindows 가상 컴퓨터에 연결](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="4029f-132">hello 클래식 포털 묻는 tooopen 또는 변수인 사용 되는 tooconnect toohello 가상 컴퓨터 '.rdp' 확장명을 가진 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-132">hello classic portal prompts you tooopen or save a file with a '.rdp' extension, which is used tooconnect toohello virtual machine.</span></span> <span data-ttu-id="4029f-133">다운로드를 마쳤을 때 hello 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-133">Click hello file when it has finished downloading.</span></span>
3. <span data-ttu-id="4029f-134">Hello 로그인 프롬프트 toohello ' AAD DC Administrators' 그룹에 속한 사용자의 hello 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-134">At hello login prompt, use hello credentials of a user belonging toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="4029f-135">사용 예를 들어 'bob@domainservicespreview.onmicrosoft.com' 여기서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-135">For example, we use 'bob@domainservicespreview.onmicrosoft.com' in our case.</span></span>
4. <span data-ttu-id="4029f-136">Hello 시작 화면에서 엽니다 **서버 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-136">From hello Start screen, open **Server Manager**.</span></span> <span data-ttu-id="4029f-137">클릭 **역할 및 기능 추가** hello 중앙 창의 hello 서버 관리자 창에서.</span><span class="sxs-lookup"><span data-stu-id="4029f-137">Click **Add Roles and Features** in hello central pane of hello Server Manager window.</span></span>

    ![가상 컴퓨터에서 서버 관리자 시작](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. <span data-ttu-id="4029f-139">Hello에 **시작 하기 전에** hello 페이지 **추가 역할 및 기능 마법사**, 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-139">On hello **Before You Begin** page of hello **Add Roles and Features Wizard**, click **Next**.</span></span>

    ![시작하기 전에 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. <span data-ttu-id="4029f-141">Hello에 **설치 유형을** 페이지에서 hello **역할 기반 또는 기능 기반 설치** 옵션을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-141">On hello **Installation Type** page, leave hello **Role-based or feature-based installation** option checked and click **Next**.</span></span>

    ![설치 유형 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. <span data-ttu-id="4029f-143">Hello에 **서버 선택** 페이지 hello 서버 풀의 hello 현재 가상 컴퓨터를 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-143">On hello **Server Selection** page, select hello current virtual machine from hello server pool, and click **Next**.</span></span>

    ![서버 선택 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. <span data-ttu-id="4029f-145">Hello에 **서버 역할** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-145">On hello **Server Roles** page, click **Next**.</span></span> <span data-ttu-id="4029f-146">에서는 이후 hello 서버에 있는 모든 역할 설치 하지 않는 것이 페이지를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-146">We skip this page since we are not installing any roles on hello server.</span></span>
9. <span data-ttu-id="4029f-147">Hello에 **기능** 페이지, 선택 hello **그룹 정책 관리** 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-147">On hello **Features** page, select hello **Group Policy Management** feature.</span></span>

    ![기능 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. <span data-ttu-id="4029f-149">Hello에 **확인** 페이지 **설치** hello 가상 컴퓨터에 tooinstall hello 그룹 정책 관리 기능.</span><span class="sxs-lookup"><span data-stu-id="4029f-149">On hello **Confirmation** page, click **Install** tooinstall hello Group Policy Management feature on hello virtual machine.</span></span> <span data-ttu-id="4029f-150">기능 설치가 완료 되 면 클릭 **닫기** tooexit hello **역할 및 기능 추가** 마법사.</span><span class="sxs-lookup"><span data-stu-id="4029f-150">When feature installation completes successfully, click **Close** tooexit hello **Add Roles and Features** wizard.</span></span>

    ![확인 페이지](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a><span data-ttu-id="4029f-152">작업 3-실행 hello 그룹 정책 관리 콘솔 tooadminister 그룹 정책</span><span class="sxs-lookup"><span data-stu-id="4029f-152">Task 3 - Launch hello Group Policy management console tooadminister Group Policy</span></span>
<span data-ttu-id="4029f-153">가상 컴퓨터를 도메인에 가입 된 tooadminister hello hello 관리 되는 도메인에서 그룹 정책에 hello 그룹 정책 관리 콘솔을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-153">You can use hello Group Policy management console on hello domain-joined virtual machine tooadminister Group Policy on hello managed domain.</span></span>

> [!NOTE]
> <span data-ttu-id="4029f-154">Toobe tooadminister hello 관리 되는 도메인의 그룹 정책은 hello AAD ' DC Administrators' 그룹의 멤버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-154">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister Group Policy on hello managed domain.</span></span>
>
>

1. <span data-ttu-id="4029f-155">Hello 시작 화면에서 클릭 **관리 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-155">From hello Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="4029f-156">Hello 표시 되어야 **그룹 정책 관리** 콘솔 hello 가상 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-156">You should see hello **Group Policy Management** console installed on hello virtual machine.</span></span>

    ![그룹 정책 관리 시작](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. <span data-ttu-id="4029f-158">클릭 **그룹 정책 관리** toolaunch hello 그룹 정책 관리 콘솔.</span><span class="sxs-lookup"><span data-stu-id="4029f-158">Click **Group Policy Management** toolaunch hello Group Policy Management console.</span></span>

    ![그룹 정책 콘솔](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a><span data-ttu-id="4029f-160">작업 4 - 기본 제공 그룹 정책 개체 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4029f-160">Task 4 - Customize built-in Group Policy Objects</span></span>
<span data-ttu-id="4029f-161">두 개의 기본 제공 그룹 정책 개체 (Gpo)-관리 되는 도메인의 hello ' AADDC 컴퓨터 ' 및 ' AADDC Users' 컨테이너에 대해 각각 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-161">There are two built-in Group Policy Objects (GPOs) - one each for hello 'AADDC Computers' and 'AADDC Users' containers in your managed domain.</span></span> <span data-ttu-id="4029f-162">이러한 Gpo tooconfigure 그룹 정책 hello 관리 되는 도메인을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-162">You can customize these GPOs tooconfigure group policy on hello managed domain.</span></span>

1. <span data-ttu-id="4029f-163">Hello에 **그룹 정책 관리** 콘솔에서 tooexpand hello **포리스트: contoso100.com** 및 **도메인** 노드 toosee hello 그룹 정책 관리 되는 도메인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-163">In hello **Group Policy Management** console, click tooexpand hello **Forest: contoso100.com** and **Domains** nodes toosee hello group policies for your managed domain.</span></span>

    ![기본 제공 GPO](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. <span data-ttu-id="4029f-165">관리 되는 도메인에서 이러한 기본 제공의 Gpo tooconfigure 그룹 정책을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-165">You can customize these built-in GPOs tooconfigure group policies on your managed domain.</span></span> <span data-ttu-id="4029f-166">Hello GPO를 마우스 오른쪽 단추로 클릭 하 고 클릭 **편집...**  toocustomize hello에 대 한 기본 제공 GPO 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-166">Right-click hello GPO and click **Edit...** toocustomize hello built-in GPO.</span></span> <span data-ttu-id="4029f-167">그룹 정책 구성 편집기 도구 hello toocustomize hello GPO 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-167">hello Group Policy Configuration Editor tool enables you toocustomize hello GPO.</span></span>

    ![기본 제공 GPO 편집](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. <span data-ttu-id="4029f-169">이제 hello를 사용할 수 있습니다 **그룹 정책 관리 편집기** tooedit hello에 대 한 기본 제공 GPO 콘솔.</span><span class="sxs-lookup"><span data-stu-id="4029f-169">You can now use hello **Group Policy Management Editor** console tooedit hello built-in GPO.</span></span> <span data-ttu-id="4029f-170">예를 들어, 다음 스크린 샷 hello toocustomize 기본 제공 ' AADDC 컴퓨터 ' GPO hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-170">For instance, hello following screenshot shows how toocustomize hello built-in 'AADDC Computers' GPO.</span></span>

    ![GPO 사용자 지정](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a><span data-ttu-id="4029f-172">작업 5 - 사용자 지정 GPO(그룹 정책 개체) 만들기</span><span class="sxs-lookup"><span data-stu-id="4029f-172">Task 5 - Create a custom Group Policy Object (GPO)</span></span>
<span data-ttu-id="4029f-173">사용자 지정 그룹 정책 개체를 만들거나 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-173">You can create or import your own custom group policy objects.</span></span> <span data-ttu-id="4029f-174">사용자 지정 Gpo tooa 사용자 지정을 연결할 수도 있습니다. 관리 되는 도메인 내에서 만든 OU입니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-174">You can also link custom GPOs tooa custom OU you have created in your managed domain.</span></span> <span data-ttu-id="4029f-175">사용자 지정 조직 구성 단위를 만드는 방법에 대한 자세한 내용은 [관리되는 도메인에서 사용자 지정 OU 만들기](active-directory-ds-admin-guide-create-ou.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4029f-175">For more information on creating custom organizational units, see [create a custom OU on a managed domain](active-directory-ds-admin-guide-create-ou.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4029f-176">Toobe tooadminister hello 관리 되는 도메인의 그룹 정책은 hello AAD ' DC Administrators' 그룹의 멤버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-176">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister Group Policy on hello managed domain.</span></span>
>
>

1. <span data-ttu-id="4029f-177">Hello에 **그룹 정책 관리** 콘솔 tooselect 사용자 지정 조직 구성 단위 (OU)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-177">In hello **Group Policy Management** console, click tooselect your custom organizational unit (OU).</span></span> <span data-ttu-id="4029f-178">Hello OU를 마우스 오른쪽 단추로 클릭 하 고 클릭 **이 도메인에서 GPO를 만들고 여기에 연결...** .</span><span class="sxs-lookup"><span data-stu-id="4029f-178">Right-click hello OU and click **Create a GPO in this domain, and Link it here...**.</span></span>

    ![사용자 지정 GPO 만들기](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. <span data-ttu-id="4029f-180">Hello 새 GPO의 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-180">Specify a name for hello new GPO and click **OK**.</span></span>

    ![GPO의 이름 지정](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. <span data-ttu-id="4029f-182">새 GPO 만들어져 tooyour 사용자 지정 연결 OU입니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-182">A new GPO is created and linked tooyour custom OU.</span></span> <span data-ttu-id="4029f-183">Hello GPO를 마우스 오른쪽 단추로 클릭 하 고 클릭 **편집...**  hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-183">Right-click hello GPO and click **Edit...** from hello menu.</span></span>

    ![새로 만든 GPO](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. <span data-ttu-id="4029f-185">Hello를 사용 하 여 hello 새로 만든 GPO를 사용자 지정할 수 있습니다 **그룹 정책 관리 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-185">You can customize hello newly created GPO using hello **Group Policy Management Editor**.</span></span>

    ![새 GPO 사용자 지정](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


<span data-ttu-id="4029f-187">[그룹 정책 관리 콘솔](https://technet.microsoft.com/library/cc753298.aspx) 사용에 대한 자세한 내용은 Technet에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4029f-187">More information about using [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is available on Technet.</span></span>

## <a name="related-content"></a><span data-ttu-id="4029f-188">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="4029f-188">Related Content</span></span>
* [<span data-ttu-id="4029f-189">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="4029f-189">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="4029f-190">Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="4029f-190">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="4029f-191">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="4029f-191">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="4029f-192">그룹 정책 관리 콘솔</span><span class="sxs-lookup"><span data-stu-id="4029f-192">Group Policy Management Console</span></span>](https://technet.microsoft.com/library/cc753298.aspx)
