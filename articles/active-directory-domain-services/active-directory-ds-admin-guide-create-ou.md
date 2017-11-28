---
title: "Azure Active Directory Domain Services: 관리 가이드 | Microsoft Docs"
description: "Azure AD 도메인 서비스 관리되는 도메인에 OU(조직 구성 단위) 만들기"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2bc00-103">Azure AD 도메인 서비스 관리되는 도메인에 OU(조직 구성 단위) 만들기</span><span class="sxs-lookup"><span data-stu-id="2bc00-103">Create an Organizational Unit (OU) on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="2bc00-104">Azure AD 도메인 서비스 관리되는 도메인에는 'AADDC 컴퓨터'와 'AADDC 사용자'라는 두 개의 기본 제공 컨테이너가 각각 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-104">Azure AD Domain Services managed domains include two built-in containers called 'AADDC Computers' and 'AADDC Users' respectively.</span></span> <span data-ttu-id="2bc00-105">hello ' AADDC 컴퓨터가 ' 컨테이너에 있는 모든 컴퓨터에 대 한 컴퓨터 개체 가입 toohello 관리 되는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-105">hello 'AADDC Computers' container has computer objects for all computers that are joined toohello managed domain.</span></span> <span data-ttu-id="2bc00-106">hello ' AADDC Users' 컨테이너 hello Azure AD 테 넌 트에 사용자 및 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-106">hello 'AADDC Users' container includes users and groups in hello Azure AD tenant.</span></span> <span data-ttu-id="2bc00-107">경우에 따라 관리 되는 hello 도메인 toodeploy 워크 로드에 필요한 toocreate 서비스 계정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-107">Occasionally, it may be necessary toocreate service accounts on hello managed domain toodeploy workloads.</span></span> <span data-ttu-id="2bc00-108">이 작업을 위해 hello 관리 되는 도메인에는 사용자 지정 조직 구성 단위 (OU)를 만들 있고 해당 OU 내에서 서비스 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-108">For this purpose, you can create a custom Organizational Unit (OU) on hello managed domain and create service accounts within that OU.</span></span> <span data-ttu-id="2bc00-109">이 문서에서는 관리 되는 도메인의 OU toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-109">This article shows you how toocreate an OU in your managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2bc00-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="2bc00-110">Before you begin</span></span>
<span data-ttu-id="2bc00-111">이 문서에 나열 된 tooperform hello 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-111">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="2bc00-112">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-112">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="2bc00-113">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-113">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="2bc00-114">**Azure AD 도메인 서비스** hello Azure AD 디렉터리를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-114">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="2bc00-115">그렇게 하지 않은 경우에 따라 hello에 설명 된 모든 hello 작업 [시작 가이드](active-directory-ds-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-115">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="2bc00-116">Hello Azure AD 도메인 서비스를 관리 하는 도메인에 가입 된 가상 컴퓨터는 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-116">A domain-joined virtual machine from which you administer hello Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="2bc00-117">가상 컴퓨터에 없으면 hello 문서에 설명 된 모든 hello 작업에 따라 [Windows 가상 컴퓨터 tooa 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-117">If you don't have such a virtual machine, follow all hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="2bc00-118">hello 자격 증명이 필요는 **사용자 계정이 속하는 toohello ' AAD DC Administrators' 그룹** toocreate 관리 되는 도메인에서 사용자 지정 된 OU 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-118">You need hello credentials of a **user account belonging toohello 'AAD DC Administrators' group** in your directory, toocreate a custom OU on your managed domain.</span></span>

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a><span data-ttu-id="2bc00-119">도메인 가입된 가상 컴퓨터에 원격 관리를 위한 AD 관리 도구 설치</span><span class="sxs-lookup"><span data-stu-id="2bc00-119">Install AD administration tools on a domain-joined virtual machine for remote administration</span></span>
<span data-ttu-id="2bc00-120">Azure AD 도메인 서비스 관리 되는 도메인 hello AD PowerShell 또는 관리 센터 ADAC (Active Directory)와 같은 친숙 한 Active Directory 관리 도구를 사용 하 여 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-120">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as hello Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="2bc00-121">테 넌 트 관리자에 원격 데스크톱을 통해 관리 되는 도메인 hello 권한 tooconnect toodomain 컨트롤러를 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-121">Tenant administrators do not have privileges tooconnect toodomain controllers on hello managed domain via Remote Desktop.</span></span> <span data-ttu-id="2bc00-122">tooadminister hello 관리 되는 도메인, 가상 컴퓨터에 가입된 toohello 관리 되는 도메인에 hello AD 관리 도구 기능을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-122">tooadminister hello managed domain, install hello AD administration tools feature on a virtual machine joined toohello managed domain.</span></span> <span data-ttu-id="2bc00-123">Toohello 문서 참조 [Azure AD 도메인 서비스는 관리 되는 도메인을 관리할](active-directory-ds-admin-guide-administer-domain.md) 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-123">Refer toohello article titled [administer an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-domain.md) for instructions.</span></span>

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a><span data-ttu-id="2bc00-124">Hello 관리 되는 도메인에 조직 구성 단위 만들기</span><span class="sxs-lookup"><span data-stu-id="2bc00-124">Create an Organizational Unit on hello managed domain</span></span>
<span data-ttu-id="2bc00-125">Hello AD 관리 도구가 설치 되어 했으므로 hello에 도메인에 가입 된 가상 컴퓨터, hello 관리 되는 도메인에서 이러한 도구 toocreate 조직 구성 단위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-125">Now that hello AD Administrative Tools are installed on hello domain joined virtual machine, we can use these tools toocreate an organization unit on hello managed domain.</span></span> <span data-ttu-id="2bc00-126">Hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-126">Perform hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="2bc00-127">Hello ' AAD DC Administrators' 그룹의 구성원만 사용자 지정 된 OU 필요한 권한이 toocreate hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-127">Only members of hello 'AAD DC Administrators' group have hello required privileges toocreate a custom OU.</span></span> <span data-ttu-id="2bc00-128">Hello toothis 그룹에 속한 사용자로 다음 단계를 수행 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-128">Ensure that you perform hello following steps as a user who belongs toothis group.</span></span>
>
>

1. <span data-ttu-id="2bc00-129">Hello 시작 화면에서 클릭 **관리 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-129">From hello Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="2bc00-130">Hello 가상 컴퓨터에 설치 하는 hello AD 관리 도구 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-130">You should see hello AD administrative tools installed on hello virtual machine.</span></span>

    ![서버에 설치된 관리 도구](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. <span data-ttu-id="2bc00-132">**Active Directory 관리 센터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-132">Click **Active Directory Administrative Center**.</span></span>

    ![Active Directory 관리 센터](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. <span data-ttu-id="2bc00-134">tooview hello 도메인 (예를 들어 ' contoso100.com') hello 왼쪽된 창에서 hello 도메인 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-134">tooview hello domain, click hello domain name in hello left pane (for example, 'contoso100.com').</span></span>

    ![ADAC - 도메인 보기](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. <span data-ttu-id="2bc00-136">Hello 오른쪽에 **작업** 창에서 클릭 **새로** hello 도메인 이름 노드 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-136">On hello right side **Tasks** pane, click **New** under hello domain name node.</span></span> <span data-ttu-id="2bc00-137">이 예제에서는 클릭 **새로** hello 오른쪽에 hello 'contoso100(local)' 노드 아래의 **작업** 창.</span><span class="sxs-lookup"><span data-stu-id="2bc00-137">In this example, we click **New** under hello 'contoso100(local)' node on hello right side **Tasks** pane.</span></span>

    ![ADAC - 새 OU](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. <span data-ttu-id="2bc00-139">Hello 옵션 toocreate 조직 구성 단위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-139">You should see hello option toocreate an Organizational Unit.</span></span> <span data-ttu-id="2bc00-140">클릭 **조직 구성 단위** toolaunch hello **조직 구성 단위 만들기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2bc00-140">Click **Organizational Unit** toolaunch hello **Create Organizational Unit** dialog.</span></span>
6. <span data-ttu-id="2bc00-141">Hello에 **조직 구성 단위 만들기** 대화 상자에서 지정 된 **이름** 에 대 한 새 OU hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-141">In hello **Create Organizational Unit** dialog, specify a **Name** for hello new OU.</span></span> <span data-ttu-id="2bc00-142">Hello OU에 대 한 간략 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-142">Provide a short description for hello OU.</span></span> <span data-ttu-id="2bc00-143">Hello를 설정할 수도 있습니다 **관리자** hello OU에 대 한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-143">You may also set hello **Managed By** field for hello OU.</span></span> <span data-ttu-id="2bc00-144">toocreate hello 사용자 지정 OU를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-144">toocreate hello custom OU, click **OK**.</span></span>

    ![ADAC - OU 대화 상자 만들기](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. <span data-ttu-id="2bc00-146">이제 OU를 새로 만든 hello hello AD ADAC (관리 센터)에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-146">hello newly created OU should now appear in hello AD Administrative Center (ADAC).</span></span>

    ![ADAC - 만든 OU](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a><span data-ttu-id="2bc00-148">새로 만든 OU에 대한 사용 권한/보안</span><span class="sxs-lookup"><span data-stu-id="2bc00-148">Permissions/Security for newly created OUs</span></span>
<span data-ttu-id="2bc00-149">사용자 지정 OU에 대해 관리자 권한 (모든 권한)을 부여는 hello 만든 hello 사용자 (hello AAD ' DC Administrators' 그룹의 구성원)는 기본적으로 OU hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-149">By default, hello user (member of hello 'AAD DC Administrators' group) who created hello custom OU is granted administrative privileges (full control) over hello OU.</span></span> <span data-ttu-id="2bc00-150">그런 다음 hello 사용자 계속 진행 하 고 원하는 대로 toohello ' AAD DC Administrators' 그룹 또는 권한이 tooother 사용자 권한을 부여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-150">hello user can then go ahead and grant privileges tooother users or toohello 'AAD DC Administrators' group as desired.</span></span> <span data-ttu-id="2bc00-151">다음 스크린 샷에서 hello와 같이 사용자 hello 'bob@domainservicespreview.onmicrosoft.com' 만든된 hello 새 'MyCustomOU' 조직 구성 단위 것에 대 한 모든 권한을 부여 받은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-151">As seen in hello following screenshot, hello user 'bob@domainservicespreview.onmicrosoft.com' who created hello new 'MyCustomOU' organizational unit is granted full control over it.</span></span>

 ![ADAC - 새 OU 보안](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a><span data-ttu-id="2bc00-153">사용자 지정 OU 관리에 대한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="2bc00-153">Notes on administering custom OUs</span></span>
<span data-ttu-id="2bc00-154">이제 사용자 지정 OU를 만들었으므로 계속해서 이 OU에 사용자, 그룹, 컴퓨터 및 서비스 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-154">Now that you have created a custom OU, you can go ahead and create users, groups, computers, and service accounts in this OU.</span></span> <span data-ttu-id="2bc00-155">Hello ' AADDC Users' OU toocustom Ou에서에서 사용자 또는 그룹을 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-155">You cannot move users or groups from hello 'AADDC Users' OU toocustom OUs.</span></span>

> [!WARNING]
> <span data-ttu-id="2bc00-156">사용자 지정 OU에서 만든 사용자 계정, 그룹, 서비스 계정 및 컴퓨터 개체는 Azure AD 테넌트에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-156">User accounts, groups, service accounts, and computer objects that you create under custom OUs are not available in your Azure AD tenant.</span></span> <span data-ttu-id="2bc00-157">즉, 이러한 개체는 hello Azure AD Graph API를 사용 하 여 위나 hello Azure AD UI에서에서 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-157">In other words, these objects do not show up using hello Azure AD Graph API or in hello Azure AD UI.</span></span> <span data-ttu-id="2bc00-158">Azure AD Domain Services 관리되는 도메인에서만 이러한 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc00-158">These objects are only available in your Azure AD Domain Services managed domain.</span></span>
>
>

## <a name="related-content"></a><span data-ttu-id="2bc00-159">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="2bc00-159">Related Content</span></span>
* [<span data-ttu-id="2bc00-160">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="2bc00-160">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="2bc00-161">관리되는 도메인에서 그룹 정책 구성</span><span class="sxs-lookup"><span data-stu-id="2bc00-161">Configure Group Policy on a managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="2bc00-162">Active Directory 관리 센터: 시작</span><span class="sxs-lookup"><span data-stu-id="2bc00-162">Active Directory Administrative Center: Getting Started</span></span>](https://technet.microsoft.com/library/dd560651.aspx)
* [<span data-ttu-id="2bc00-163">서비스 계정 단계별 가이드</span><span class="sxs-lookup"><span data-stu-id="2bc00-163">Service Accounts Step-by-Step Guide</span></span>](https://technet.microsoft.com/library/dd548356.aspx)
