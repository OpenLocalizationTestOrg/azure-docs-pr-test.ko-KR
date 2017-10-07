---
title: "Azure AD 도메인 서비스에서 LDAP (LDAPS) Secure aaaConfigure | Microsoft Docs"
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
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="f34fa-103">Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성</span><span class="sxs-lookup"><span data-stu-id="f34fa-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f34fa-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f34fa-104">Before you begin</span></span>
<span data-ttu-id="f34fa-105">완료 했으면 확인 [작업 2-내보내기 hello 보안 LDAP 인증서 tooa 합니다. PFX 파일](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="f34fa-106">Toouse 미리 보기 포털 Azure 환경 hello Azure 클래식 포털 toocomplete이이 작업을 hello 하는지 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="f34fa-107">**Azure 포털 (미리 보기)**: [사용 hello Azure 포털을 사용 하 여 LDAP 보안](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="f34fa-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="f34fa-108">**Azure 클래식 포털**: [사용 hello 클래식 Azure 포털을 사용 하 여 LDAP 보안](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="f34fa-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="f34fa-109">작업 3-hello Azure 포털 (미리 보기)를 사용 하 여 hello 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f34fa-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="f34fa-110">tooenable 보안 LDAP에 hello 다음 구성 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="f34fa-111">Toohello 이동  **[Azure 포털](https://portal.azure.com)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="f34fa-112">'도메인 서비스' hello에 대 한 검색 **리소스 검색** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="f34fa-113">선택 **Azure AD 도메인 서비스** hello 검색 결과에서.</span><span class="sxs-lookup"><span data-stu-id="f34fa-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="f34fa-114">hello **Azure AD 도메인 서비스** 블레이드에 관리 되는 도메인을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![프로비전되는 관리되는 도메인 찾기](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="f34fa-116">Hello 도메인에 대 한 자세한 내용은 hello 관리 되는 도메인 (예를 들어 ' contoso100.com') toosee의 hello 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - 프로비저닝 상태](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="f34fa-118">클릭 **LDAP 보안** hello 탐색 창에서.</span><span class="sxs-lookup"><span data-stu-id="f34fa-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Domain Services - 보안 LDAP 블레이드](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="f34fa-120">기본적으로 보안 LDAP 액세스 tooyour 관리 되는 도메인은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="f34fa-121">설정/해제 **LDAP 보안** 너무**사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![보안 LDAP를 사용하도록 설정](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="f34fa-123">기본적으로 보안 LDAP 액세스 tooyour 인터넷을 사용할 수 없습니다. hello를 통해 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="f34fa-124">설정/해제 **를 통해 보안 LDAP 액세스를 허용 hello 인터넷** 너무**사용**사용할 경우.</span><span class="sxs-lookup"><span data-stu-id="f34fa-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="f34fa-125">Hello 폴더 아이콘 다음 클릭 **합니다. 보안 LDAP 인증서 인 PFX 파일이**합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="f34fa-126">보안 LDAP 액세스 toohello 관리 되는 도메인에 대 한 hello 인증서로 hello toohello PFX 파일 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="f34fa-127">Hello 지정 **암호 toodecrypt 합니다. PFX 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="f34fa-128">Hello 제공 hello 인증서 toohello PFX 파일을 내보낼 때 사용한 동일한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="f34fa-129">완료 되 면 클릭 hello **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="f34fa-130">Hello 관리 되는 도메인에 대 한 보안 LDAP 구성 중인 알려 주는 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="f34fa-131">이 작업이 완료 될 때까지 hello 도메인에 대 한 다른 설정을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Hello 관리 되는 도메인에 대 한 보안 LDAP를 구성합니다.](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="f34fa-133">관리 되는 도메인에 대 한 보안 LDAP tooenable 약 10 개 too15 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="f34fa-134">Hello 제공 보안 LDAP 인증서가 일치 하지 않으면 hello 필수 조건, 보안 LDAP 디렉터리를 사용할 수 없습니다 및 오류가 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="f34fa-135">예를 들어 hello 도메인 이름이 잘못 되었습니다, 그리고 hello 인증서가 이미 만료 되었거나 곧 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="f34fa-136">이 경우 유효한 인증서로 다시 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f34fa-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="f34fa-137">작업 4-DNS tooaccess hello hello에서 관리 되는 도메인 구성 인터넷</span><span class="sxs-lookup"><span data-stu-id="f34fa-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="f34fa-138">**선택적 작업** -LDAPS를 사용 하 여 tooaccess hello 관리 되는 도메인 하지 않을 경우 넘는 인터넷 hello를이 구성 작업을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="f34fa-139">이 작업을 시작 하기 전에 확인에 설명 된 hello 단계를 완료 한 [작업 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="f34fa-140">통해 보안 LDAP 액세스를 설정한 후 hello 인터넷 관리 되는 도메인에 필요한 tooupdate DNS 클라이언트 컴퓨터는 관리 되는이 도메인을 찾을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="f34fa-141">Hello에 표시 되는 외부 IP 주소 작업 3의 hello 끝 **속성** 블레이드 **외부 IP 주소에 대 한 LDAPS 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="f34fa-142">Hello의 hello DNS 이름을 도메인 (예를 들어 ' ldaps.contoso100.com') 포인트 toothis 외부 IP 주소를 관리 하므로 외부 DNS 공급자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="f34fa-143">예에서 toocreate hello DNS 항목을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="f34fa-144">이제 끝났습니다-현재 위치 관리 되는 준비 tooconnect toohello는를 통해 보안 LDAP를 사용 하 여 도메인에 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="f34fa-145">클라이언트 컴퓨터가 hello LDAPS 인증서 toobe 수 tooconnect의 hello 발급자를 성공적으로 신뢰 해야 기억 toohello LDAPS를 사용 하 여 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="f34fa-146">공개적으로 신뢰할 수 있는 인증 기관을 사용 하는 경우 불필요 toodo 아무 것도 하므로 이러한 인증서 발급자를 신뢰 하는 클라이언트 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="f34fa-147">자체 서명 된 인증서를 사용 하는 경우 hello 자체 서명 된 인증서의 공개 부분이 hello hello 신뢰할 수 있는 인증서 저장소 hello 클라이언트 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="f34fa-148">작업 5-잠금 LDAPS 액세스 tooyour 관리 되는 도메인을 통해 인터넷 hello</span><span class="sxs-lookup"><span data-stu-id="f34fa-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="f34fa-149">**선택적 작업** -LDAPS를 설정 하지 않은 경우 액세스 toohello 관리 되는 도메인 넘는 인터넷 hello,이 구성 작업을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="f34fa-150">이 작업을 시작 하기 전에 확인에 설명 된 hello 단계를 완료 한 [작업 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="f34fa-151">LDAPS 액세스를 위한 관리 되는 도메인 hello를 통해 노출 인터넷 보안 위협이 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="f34fa-152">hello 관리 되는 도메인은 hello에서 연결할 수 있는 보안 LDAP에 사용 되는 hello 포트에서 인터넷 (즉, 636 포트).</span><span class="sxs-lookup"><span data-stu-id="f34fa-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="f34fa-153">따라서 toorestrict 액세스 관리 toohello 도메인 toospecific 알려진 IP 주소를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="f34fa-154">보안 향상된을 위해 NSG ()를 네트워크 보안 그룹을 만들고 Azure AD 도메인 서비스를 설정한 hello 서브넷과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="f34fa-155">hello 다음 표에서 설명 샘플 NSG를 구성할 수 hello 통해 보안 LDAP 액세스 아래로 toolock 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="f34fa-156">hello NSG에는 TCP 포트를 통해 636 지정된 된 집합 에서만에서 IP 주소의 인바운드 LDAPS 액세스를 허용 하는 규칙 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="f34fa-157">hello 기본 'DenyAll' 규칙 적용 tooall 인바운드 트래픽을 다른 hello에서 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="f34fa-158">hello NSG 규칙 tooallow LDAPS 액세스 hello 통해 지정 된 IP 주소에서 인터넷에 hello DenyAll NSG 규칙 보다 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="f34fa-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![샘플 NSG toosecure LDAPS 액세스를 통해 인터넷 hello](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="f34fa-160">**자세한 정보** - [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f34fa-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="f34fa-161">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="f34fa-161">Related content</span></span>
* [<span data-ttu-id="f34fa-162">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="f34fa-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="f34fa-163">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="f34fa-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="f34fa-164">Azure AD Domain Services 관리되는 도메인에서 그룹 정책 관리</span><span class="sxs-lookup"><span data-stu-id="f34fa-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="f34fa-165">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="f34fa-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="f34fa-166">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f34fa-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
