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
ms.openlocfilehash: 017a8cabe81743af4c0cbb694098df799a904468
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="ced83-103">Azure AD 도메인 서비스 관리되는 도메인에 OU(조직 구성 단위) 만들기</span><span class="sxs-lookup"><span data-stu-id="ced83-103">Create an Organizational Unit (OU) on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="ced83-104">Azure AD 도메인 서비스 관리되는 도메인에는 'AADDC 컴퓨터'와 'AADDC 사용자'라는 두 개의 기본 제공 컨테이너가 각각 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-104">Azure AD Domain Services managed domains include two built-in containers called 'AADDC Computers' and 'AADDC Users' respectively.</span></span> <span data-ttu-id="ced83-105">'AADDC 컴퓨터' 컨테이너에는 관리되는 도메인에 가입된 모든 컴퓨터에 대한 컴퓨터 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-105">The 'AADDC Computers' container has computer objects for all computers that are joined to the managed domain.</span></span> <span data-ttu-id="ced83-106">'AADDC 사용자' 컨테이너는 Azure AD 테넌트의 사용자 및 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-106">The 'AADDC Users' container includes users and groups in the Azure AD tenant.</span></span> <span data-ttu-id="ced83-107">경우에 따라 워크로드를 배포하기 위해 관리되는 도메인에 서비스 계정을 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-107">Occasionally, it may be necessary to create service accounts on the managed domain to deploy workloads.</span></span> <span data-ttu-id="ced83-108">이 용도로 관리되는 도메인에 사용자 지정 OU(조직 구성 단위)를 만들고 해당 OU 내에 서비스 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-108">For this purpose, you can create a custom Organizational Unit (OU) on the managed domain and create service accounts within that OU.</span></span> <span data-ttu-id="ced83-109">이 문서에서는 관리되는 도메인에 OU를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-109">This article shows you how to create an OU in your managed domain.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ced83-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ced83-110">Before you begin</span></span>
<span data-ttu-id="ced83-111">이 문서에 나열된 작업을 수행하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-111">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="ced83-112">유효한 **Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="ced83-112">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="ced83-113">**Azure AD 디렉터리** - 온-프레미스 디렉터리 또는 클라우드 전용 디렉터리와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-113">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="ced83-114">**Azure AD 도메인 서비스** 를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-114">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="ced83-115">그렇지 않은 경우 [시작 가이드](active-directory-ds-getting-started.md)에 간략히 설명된 모든 작업을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-115">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="ced83-116">Azure AD Domain Services 관리되는 도메인을 관리하게 될 도메인에 가입된 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-116">A domain-joined virtual machine from which you administer the Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="ced83-117">이러한 가상 컴퓨터가 없는 경우 [Windows 가상 컴퓨터를 관리되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)문서에 설명된 모든 작업을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="ced83-117">If you don't have such a virtual machine, follow all the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>
5. <span data-ttu-id="ced83-118">관리되는 도메인에 대한 사용자 지정 OU를 만들려면 디렉터리의 **'AAD DC 관리자' 그룹에 속한 사용자 계정**의 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-118">You need the credentials of a **user account belonging to the 'AAD DC Administrators' group** in your directory, to create a custom OU on your managed domain.</span></span>

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a><span data-ttu-id="ced83-119">도메인 가입된 가상 컴퓨터에 원격 관리를 위한 AD 관리 도구 설치</span><span class="sxs-lookup"><span data-stu-id="ced83-119">Install AD administration tools on a domain-joined virtual machine for remote administration</span></span>
<span data-ttu-id="ced83-120">Azure AD 도메인 서비스 관리되는 도메인을 AD PowerShell 또는 ADAC(Active Directory 관리 센터)와 같은 친숙한 Active Directory 관리 도구를 사용하여 원격으로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-120">Azure AD Domain Services managed domains can be managed remotely using familiar Active Directory administrative tools such as the Active Directory Administrative Center (ADAC) or AD PowerShell.</span></span> <span data-ttu-id="ced83-121">테넌트 관리자는 원격 데스크톱을 통해 관리되는 도메인의 도메인 컨트롤러에 연결할 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-121">Tenant administrators do not have privileges to connect to domain controllers on the managed domain via Remote Desktop.</span></span> <span data-ttu-id="ced83-122">관리되는 도메인을 관리하려면 관리되는 도메인에 가입된 가상 컴퓨터에 AD 관리 도구 기능을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-122">To administer the managed domain, install the AD administration tools feature on a virtual machine joined to the managed domain.</span></span> <span data-ttu-id="ced83-123">지침은 [Azure AD 도메인 서비스 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md) 라는 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ced83-123">Refer to the article titled [administer an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-domain.md) for instructions.</span></span>

## <a name="create-an-organizational-unit-on-the-managed-domain"></a><span data-ttu-id="ced83-124">관리 도메인에서 조직 구성 단위 만들기</span><span class="sxs-lookup"><span data-stu-id="ced83-124">Create an Organizational Unit on the managed domain</span></span>
<span data-ttu-id="ced83-125">이제 도메인에 가입된 가상 컴퓨터에 AD 관리 도구가 설치되었습니다. 이러한 도구를 사용하여 관리되는 도메인에 조직 구성 단위를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-125">Now that the AD Administrative Tools are installed on the domain joined virtual machine, we can use these tools to create an organization unit on the managed domain.</span></span> <span data-ttu-id="ced83-126">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-126">Perform the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="ced83-127">'AAD DC 관리자' 그룹의 구성원에게만 사용자 지정 OU를 만드는 데 필요한 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-127">Only members of the 'AAD DC Administrators' group have the required privileges to create a custom OU.</span></span> <span data-ttu-id="ced83-128">이 그룹에 속한 사용자로 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-128">Ensure that you perform the following steps as a user who belongs to this group.</span></span>
>
>

1. <span data-ttu-id="ced83-129">시작 화면에서 **관리 도구**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-129">From the Start screen, click **Administrative Tools**.</span></span> <span data-ttu-id="ced83-130">가상 컴퓨터에 설치된 AD 관리 도구가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-130">You should see the AD administrative tools installed on the virtual machine.</span></span>

    ![서버에 설치된 관리 도구](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. <span data-ttu-id="ced83-132">**Active Directory 관리 센터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-132">Click **Active Directory Administrative Center**.</span></span>

    ![Active Directory 관리 센터](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. <span data-ttu-id="ced83-134">도메인을 보려면 왼쪽 창에서 도메인 이름(예: 'contoso100.com')을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-134">To view the domain, click the domain name in the left pane (for example, 'contoso100.com').</span></span>

    ![ADAC - 도메인 보기](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. <span data-ttu-id="ced83-136">오른쪽 **태스크** 창의 도메인 이름 노드에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-136">On the right side **Tasks** pane, click **New** under the domain name node.</span></span> <span data-ttu-id="ced83-137">이 예제에서는 오른쪽 **태스크** 창의 'contoso100(로컬)' 노드에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-137">In this example, we click **New** under the 'contoso100(local)' node on the right side **Tasks** pane.</span></span>

    ![ADAC - 새 OU](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. <span data-ttu-id="ced83-139">조직 구성 단위 만들기에 대한 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-139">You should see the option to create an Organizational Unit.</span></span> <span data-ttu-id="ced83-140">**조직 구성 단위**를 클릭하여 **조직 구성 단위 만들기** 대화 상자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-140">Click **Organizational Unit** to launch the **Create Organizational Unit** dialog.</span></span>
6. <span data-ttu-id="ced83-141">**조직 구성 단위 만들기** 대화 상자에서 새 OU의 **이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-141">In the **Create Organizational Unit** dialog, specify a **Name** for the new OU.</span></span> <span data-ttu-id="ced83-142">OU에 대한 간략한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-142">Provide a short description for the OU.</span></span> <span data-ttu-id="ced83-143">OU에 대한 **관리자** 필드를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-143">You may also set the **Managed By** field for the OU.</span></span> <span data-ttu-id="ced83-144">사용자 지정 OU를 만들려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-144">To create the custom OU, click **OK**.</span></span>

    ![ADAC - OU 대화 상자 만들기](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. <span data-ttu-id="ced83-146">이제 새로 만든 OU가 ADAC(AD 관리 센터)에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-146">The newly created OU should now appear in the AD Administrative Center (ADAC).</span></span>

    ![ADAC - 만든 OU](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a><span data-ttu-id="ced83-148">새로 만든 OU에 대한 사용 권한/보안</span><span class="sxs-lookup"><span data-stu-id="ced83-148">Permissions/Security for newly created OUs</span></span>
<span data-ttu-id="ced83-149">기본적으로 사용자 지정 OU를 만든 사용자('AAD DC 관리자' 그룹의 구성원)는 OU에 대해 관리자 권한(모든 권한)이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-149">By default, the user (member of the 'AAD DC Administrators' group) who created the custom OU is granted administrative privileges (full control) over the OU.</span></span> <span data-ttu-id="ced83-150">사용자는 계속해서 원하는 대로 다른 사용자에게 또는 'AAD DC 관리자' 그룹에 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-150">The user can then go ahead and grant privileges to other users or to the 'AAD DC Administrators' group as desired.</span></span> <span data-ttu-id="ced83-151">사용자 다음 스크린샷에 표시 된 대로 'bob@domainservicespreview.onmicrosoft.com' 새 'MyCustomOU' 조직 구성 단위를 만든 사람 것에 대 한 모든 권한을 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-151">As seen in the following screenshot, the user 'bob@domainservicespreview.onmicrosoft.com' who created the new 'MyCustomOU' organizational unit is granted full control over it.</span></span>

 ![ADAC - 새 OU 보안](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a><span data-ttu-id="ced83-153">사용자 지정 OU 관리에 대한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="ced83-153">Notes on administering custom OUs</span></span>
<span data-ttu-id="ced83-154">이제 사용자 지정 OU를 만들었으므로 계속해서 이 OU에 사용자, 그룹, 컴퓨터 및 서비스 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-154">Now that you have created a custom OU, you can go ahead and create users, groups, computers, and service accounts in this OU.</span></span> <span data-ttu-id="ced83-155">'AADDC 사용자' OU에서 사용자 지정 OU로 사용자 또는 그룹을 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-155">You cannot move users or groups from the 'AADDC Users' OU to custom OUs.</span></span>

> [!WARNING]
> <span data-ttu-id="ced83-156">사용자 지정 OU에서 만든 사용자 계정, 그룹, 서비스 계정 및 컴퓨터 개체는 Azure AD 테넌트에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-156">User accounts, groups, service accounts, and computer objects that you create under custom OUs are not available in your Azure AD tenant.</span></span> <span data-ttu-id="ced83-157">즉, 이러한 개체는 Azure AD Graph API를 사용하여 또는 Azure AD UI에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-157">In other words, these objects do not show up using the Azure AD Graph API or in the Azure AD UI.</span></span> <span data-ttu-id="ced83-158">Azure AD Domain Services 관리되는 도메인에서만 이러한 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-158">These objects are only available in your Azure AD Domain Services managed domain.</span></span>
>
>

## <a name="related-content"></a><span data-ttu-id="ced83-159">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="ced83-159">Related Content</span></span>
* [<span data-ttu-id="ced83-160">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="ced83-160">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="ced83-161">관리되는 도메인에서 그룹 정책 구성</span><span class="sxs-lookup"><span data-stu-id="ced83-161">Configure Group Policy on a managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="ced83-162">Active Directory 관리 센터: 시작</span><span class="sxs-lookup"><span data-stu-id="ced83-162">Active Directory Administrative Center: Getting Started</span></span>](https://technet.microsoft.com/library/dd560651.aspx)
* [<span data-ttu-id="ced83-163">서비스 계정 단계별 가이드</span><span class="sxs-lookup"><span data-stu-id="ced83-163">Service Accounts Step-by-Step Guide</span></span>](https://technet.microsoft.com/library/dd548356.aspx)
