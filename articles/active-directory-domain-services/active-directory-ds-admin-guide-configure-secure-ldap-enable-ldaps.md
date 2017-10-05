---
title: "Azure AD Domain Services에서 보안 LDAP(LDAPS) 구성 | Microsoft Docs"
description: "Azure AD 도메인 서비스 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 3b19f078b0d6dc3e02d951014056406fd1b099a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="eea66-103">Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성</span><span class="sxs-lookup"><span data-stu-id="eea66-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eea66-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="eea66-104">Before you begin</span></span>
<span data-ttu-id="eea66-105">[작업 2 - 보안 LDAP 인증서를 .PFX 파일로 내보내기](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)를 완료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="eea66-106">이 작업을 완료하는 데 미리 보기 Azure Portal 환경을 사용할 것인지 Azure 클래식 포털을 사용할 것인지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="eea66-107">**Azure Portal(미리 보기)**: [Azure Portal을 사용하여 보안 LDAP를 사용하도록 설정](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="eea66-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="eea66-108">**Azure 클래식 포털**: [클래식 Azure Portal을 사용하여 보안 LDAP를 사용하도록 설정](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="eea66-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a><span data-ttu-id="eea66-109">작업 3 - Azure Portal(미리 보기)을 사용하여 관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="eea66-109">Task 3 - enable secure LDAP for the managed domain using the Azure portal (Preview)</span></span>
<span data-ttu-id="eea66-110">보안 LDAP를 사용하도록 설정하려면 다음 구성 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="eea66-111">**[Azure Portal](https://portal.azure.com)**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-111">Navigate to the **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="eea66-112">**리소스 검색** 검색 상자에서 'domain services'를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-112">Search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="eea66-113">검색 결과에서 **Azure AD Domain Services**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-113">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="eea66-114">**Azure AD Domain Services** 블레이드에 관리되는 도메인이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-114">The **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![프로비전되는 관리되는 도메인 찾기](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="eea66-116">도메인에 대한 자세한 내용을 보려면 관리되는 도메인의 이름(예: 'contoso100.com')을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-116">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - 프로비저닝 상태](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="eea66-118">탐색 창에서 **보안 LDAP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-118">Click **Secure LDAP** on the navigation pane.</span></span>

    ![Domain Services - 보안 LDAP 블레이드](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="eea66-120">기본적으로 관리되는 도메인에 대한 보안 LDAP 액세스는 사용하지 않도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-120">By default, secure LDAP access to your managed domain is disabled.</span></span> <span data-ttu-id="eea66-121">**보안 LDAP**를 **사용**으로 토글합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-121">Toggle **Secure LDAP** to **Enable**.</span></span>

    ![보안 LDAP를 사용하도록 설정](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="eea66-123">기본적으로 인터넷에서 관리되는 도메인에 대한 보안 LDAP 액세스는 사용하지 않도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-123">By default, secure LDAP access to your managed domain over the internet is disabled.</span></span> <span data-ttu-id="eea66-124">필요한 경우 **Allow secure LDAP access over the internet**(인터넷을 통한 보안 LDAP 액세스 허용)을 **사용**으로 토글합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-124">Toggle **Allow secure LDAP access over the internet** to **Enable**, if desired.</span></span> 

6. <span data-ttu-id="eea66-125">**보안 LDAP 인증서가 포함된 .PFX 파일** 뒤의 폴더 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="eea66-126">관리되는 도메인에 대한 보안 LDAP 액세스를 위해 인증서를 사용하여 PFX 파일의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span></span>

7. <span data-ttu-id="eea66-127">**.PFX 파일의 암호를 해독하도록 암호를** 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-127">Specify the **Password to decrypt .PFX file**.</span></span> <span data-ttu-id="eea66-128">인증서를 PFX 파일로 내보낼 때 사용한 것과 동일한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-128">Provide the same password you used when exporting the certificate to the PFX file.</span></span>

8. <span data-ttu-id="eea66-129">완료되면 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-129">When you are done, click the **Save** button.</span></span>

9. <span data-ttu-id="eea66-130">관리되는 도메인에 대해 보안 LDAP가 구성되었음을 알려 주는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span></span> <span data-ttu-id="eea66-131">이 작업이 완료될 때까지 도메인에 대한 다른 설정을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-131">Until this operation is complete, you cannot modify other settings for the domain.</span></span>

    ![관리되는 도메인에 대해 보안 LDAP 구성](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="eea66-133">관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정하는 데 약 10-15분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="eea66-134">제공된 보안 LDAP 인증서가 필수 조건을 만족하지 않으면 보안 LDAP는 디렉터리에 사용할 수 없으며 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="eea66-135">도메인 이름이 올바르지 않거나 인증서가 만료되었거나 곧 만료된다는 오류 등이 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span> <span data-ttu-id="eea66-136">이 경우 유효한 인증서로 다시 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="eea66-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="eea66-137">작업 4 - 인터넷에서 관리되는 도메인에 액세스할 DNS 구성</span><span class="sxs-lookup"><span data-stu-id="eea66-137">Task 4 - configure DNS to access the managed domain from the internet</span></span>
> [!NOTE]
> <span data-ttu-id="eea66-138">**선택적 태스크** - 인터넷을 통해 LDAPS를 사용하여 관리되는 도메인에 액세스하지 않으려면 이 구성 태스크를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-138">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="eea66-139">이 태스크를 시작하기 전에 [태스크 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)에 나와 있는 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-139">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="eea66-140">관리되는 도메인에 대한 인터넷을 통한 보안 LDAP 액세스를 사용하도록 설정했으면 클라이언트 컴퓨터가 관리되는 도메인을 찾을 수 있도록 DNS를 업데이트 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-140">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="eea66-141">작업 3이 완료되면 외부 IP 주소가 **LDAPS 액세스를 위한 외부 IP 주소**의 **속성** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-141">At the end of task 3, an external IP address is displayed on the **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="eea66-142">관리되는 도메인의 DNS 이름(예: 'ldaps.contoso100.com')이 이 외부 IP 주소를 가리키도록 외부 DNS 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-142">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="eea66-143">이 예에서는 다음과 같은 DNS 항목을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-143">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="eea66-144">이것으로 끝입니다. 이제 인터넷을 통해 보안 LDAP를 사용하여 관리되는 도메인에 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-144">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="eea66-145">클라이언트 컴퓨터가 LDAPS를 사용하여 관리되는 도메인에 성공적으로 연결하려면 LDAPS 인증서의 발급자를 신뢰해야 한다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="eea66-145">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="eea66-146">공개적으로 신뢰할 수 있는 인증 기관을 사용하는 경우 클라이언트 컴퓨터가 이러한 인증서 발급자를 신뢰하므로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-146">If you are using a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="eea66-147">자체 서명된 인증서를 사용하는 경우 자체 서명된 인증서의 공개 부분을 클라이언트 컴퓨터의 신뢰할 수 있는 인증서 저장소에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-147">If you are using a self-signed certificate, install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="eea66-148">작업 5 - 인터넷을 통해 관리되는 도메인에 대한 LDAPS 액세스 잠금</span><span class="sxs-lookup"><span data-stu-id="eea66-148">Task 5 - lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="eea66-149">**선택적 작업** - 인터넷을 통해 관리되는 도메인에 대한 LDAPS 액세스를 사용하여 않는 경우 이 구성 작업을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-149">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="eea66-150">이 태스크를 시작하기 전에 [태스크 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)에 나와 있는 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-150">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="eea66-151">인터넷을 통해 LDAPS 액세스가 가능하도록 관리되는 도메인을 노출하면 보안 위협이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-151">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="eea66-152">관리되는 도메인은 보안 LDAP에 사용되는 포트(즉, 포트 636)에서 인터넷을 통해 접속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-152">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="eea66-153">따라서 관리되는 도메인에 대한 액세스를 알려진 특정 IP 주소로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-153">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="eea66-154">보안이 향상되도록 NSG(네트워크 보안 그룹)를 만들고 Azure AD Domain Services를 사용하도록 설정된 서브넷과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-154">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="eea66-155">다음 표에서는 구성 가능한 예제 NSG를 통해 인터넷을 통한 보안 LDAP 액세스를 잠그는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-155">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="eea66-156">이 NSG에는 지정된 IP 주소 집합에서만 TCP 포트 636을 통해 인바운드 LDAPS 액세스를 허용하는 규칙 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-156">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="eea66-157">기본 'DenyAll' 규칙은 인터넷의 다른 모든 인바운드 트래픽에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-157">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="eea66-158">지정된 IP 주소에서 인터넷을 통해 LDAPS 액세스를 허용하는 NSG 규칙은 DenyAll NSG 규칙보다 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="eea66-158">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![인터넷을 통해 LDAPS 액세스를 보안하는 예제 NSG](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="eea66-160">**자세한 정보** - [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="eea66-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="eea66-161">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="eea66-161">Related content</span></span>
* [<span data-ttu-id="eea66-162">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="eea66-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="eea66-163">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="eea66-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="eea66-164">Azure AD Domain Services 관리되는 도메인에서 그룹 정책 관리</span><span class="sxs-lookup"><span data-stu-id="eea66-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="eea66-165">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="eea66-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="eea66-166">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="eea66-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
