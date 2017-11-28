---
title: "Azure AD 도메인 서비스에서 LDAP (LDAPS) Secure aaaConfigure | Microsoft Docs"
description: "Azure AD 도메인 서비스 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="7d54c-103">Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성</span><span class="sxs-lookup"><span data-stu-id="7d54c-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7d54c-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7d54c-104">Before you begin</span></span>
<span data-ttu-id="7d54c-105">완료 했으면 확인 [작업 2-내보내기 hello 보안 LDAP 인증서 tooa 합니다. PFX 파일](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="7d54c-106">Toouse 미리 보기 포털 Azure 환경 hello Azure 클래식 포털 toocomplete이이 작업을 hello 하는지 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7d54c-107">**Azure 포털 (미리 보기)**: [사용 hello Azure 포털을 사용 하 여 LDAP 보안](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="7d54c-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="7d54c-108">**Azure 클래식 포털**: [사용 hello 클래식 Azure 포털을 사용 하 여 LDAP 보안](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="7d54c-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="7d54c-109">작업 3-hello 클래식 Azure 포털을 사용 하 여 hello 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7d54c-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="7d54c-110">tooenable 보안 LDAP에 hello 다음 구성 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="7d54c-111">Toohello 이동 ** [Azure 클래식 포털](https://manage.windowsazure.com)**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="7d54c-112">선택 hello **Active Directory** hello 왼쪽된 창에서 노드.</span><span class="sxs-lookup"><span data-stu-id="7d54c-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="7d54c-113">Hello Azure AD 디렉터리 (또한 참조 tooas 'tenant'), 설정한 Azure AD 도메인 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Azure AD 디렉터리 선택](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="7d54c-115">Hello 클릭 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-115">Click hello **Configure** tab.</span></span>

    ![디렉터리의 탭 구성](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="7d54c-117">Toohello 단원 아래로 스크롤하여 **도메인 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="7d54c-118">이라는 프로그램 옵션 표시 되어야 **보안 LDAP (LDAPS)** hello 스크린 샷 뒤에 표시 된 대로:</span><span class="sxs-lookup"><span data-stu-id="7d54c-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![도메인 서비스 구성 섹션](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="7d54c-120">Hello 클릭 **인증서 구성... ** hello 단추 toobring **보안 LDAP에 대 한 인증서 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="7d54c-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![보안 LDAP에 대한 인증서 구성](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="7d54c-122">Hello 폴더 아이콘 다음 클릭 **인증서로 PFX 파일** toospecify hello PFX 파일에 대 한 보안 LDAP 액세스 toohello toouse 원하는 hello 인증서가 포함 된 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="7d54c-123">또한 hello 인증서 toohello PFX 파일을 내보낼 때 지정한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="7d54c-124">그런 다음 hello 수행 hello 아래쪽에 있는 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-124">Then, click hello done button on hello bottom.</span></span>

    ![보안 LDAP PFX 파일 및 암호 지정](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="7d54c-126">hello **도메인 서비스** hello 섹션 **구성** 탭 해야 가져올 회색으로 나타나고 hello에 **보류 중... ** 몇 분 동안 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="7d54c-127">이 기간 동안 정확도 대 한 hello LDAPS 인증서가 확인 및 관리 되는 도메인에 대 한 보안 LDAP 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![보안 LDAP - 보류 중 상태](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="7d54c-129">관리 되는 도메인에 대 한 보안 LDAP tooenable 약 10 개 too15 분 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="7d54c-130">Hello 제공 보안 LDAP 인증서가 일치 하지 않으면 hello 필수 조건, 보안 LDAP 디렉터리를 사용할 수 없습니다 및 오류가 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="7d54c-131">예를 들어 hello 도메인 이름이 잘못 되었습니다, 그리고 hello 인증서가 이미 만료 되었거나 곧 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="7d54c-132">보안 LDAP 성공적으로 관리 되는 도메인에 설정 되어 있으면, hello **보류 중... ** 메시지가 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="7d54c-133">표시 된 hello 인증서의 hello 지문을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![보안 LDAP 사용](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="7d54c-135">작업 4 hello를 통해 보안 LDAP 액세스 사용-인터넷</span><span class="sxs-lookup"><span data-stu-id="7d54c-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="7d54c-136">**선택적 작업** -LDAPS를 사용 하 여 tooaccess hello 관리 되는 도메인 하지 않을 경우 넘는 인터넷 hello를이 구성 작업을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="7d54c-137">이 작업을 시작 하기 전에 확인에 설명 된 hello 단계를 완료 한 [작업 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="7d54c-138">표시 되어야 옵션 너무**사용 보안 LDAP 액세스를 통해 hello 인터넷** hello에 **도메인 서비스** hello 섹션 **구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7d54c-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="7d54c-139">이 옵션은 너무 설정**아니요** 기본적으로 인터넷 액세스 toohello 관리 되므로 도메인 보안 LDAP 통해 기본적으로 비활성화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![보안 LDAP 사용](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="7d54c-141">설정/해제 **사용 보안 LDAP 액세스를 통해 hello 인터넷** 너무**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="7d54c-142">Hello 클릭 **저장** hello 아래쪽 패널에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="7d54c-143">![보안 LDAP 사용](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="7d54c-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="7d54c-144">hello **도메인 서비스** hello 섹션 **구성** 탭 해야 가져올 회색으로 나타나고 hello에 **보류 중... ** 몇 분 동안 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="7d54c-145">일정 시간이 지난 후 인터넷 액세스 tooyour 보안 LDAP 통해 관리 되는 도메인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![보안 LDAP - 보류 중 상태](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="7d54c-147">10 분 걸립니다 관리 되는 도메인에 대 한 보안 LDAP 통해 tooenable 인터넷 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="7d54c-148">보안 LDAP 액세스 tooyour 인터넷 성공적으로 사용 하도록 설정 하는 hello을 통해 도메인을 관리 때 hello **보류 중... ** 메시지가 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="7d54c-149">Hello 외부 IP 주소에 표시 되어야 사용된 tooaccess 디렉터리 통해 수 hello 필드에 대 한 LDAPS **외부 IP 주소에 대 한 LDAPS 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![보안 LDAP 사용](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="7d54c-151">작업 5-DNS tooaccess hello hello에서 관리 되는 도메인 구성 인터넷</span><span class="sxs-lookup"><span data-stu-id="7d54c-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="7d54c-152">**선택적 작업** -LDAPS를 사용 하 여 tooaccess hello 관리 되는 도메인 하지 않을 경우 넘는 인터넷 hello를이 구성 작업을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="7d54c-153">이 작업을 시작 하기 전에 확인에 설명 된 hello 단계를 완료 한 [작업 4](#task-4---enable-secure-ldap-access-over-the-internet)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="7d54c-154">통해 보안 LDAP 액세스를 설정한 후 hello 인터넷 관리 되는 도메인에 필요한 tooupdate DNS 클라이언트 컴퓨터는 관리 되는이 도메인을 찾을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="7d54c-155">Hello에 표시 되는 외부 IP 주소 작업 4의 hello 끝 **구성** 탭에서 **외부 IP 주소에 대 한 LDAPS 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="7d54c-156">Hello의 hello DNS 이름을 도메인 (예를 들어 ' ldaps.contoso100.com') 포인트 toothis 외부 IP 주소를 관리 하므로 외부 DNS 공급자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="7d54c-157">예에서 toocreate hello DNS 항목을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="7d54c-158">이제 끝났습니다-현재 위치 관리 되는 준비 tooconnect toohello는를 통해 보안 LDAP를 사용 하 여 도메인에 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="7d54c-159">클라이언트 컴퓨터가 hello LDAPS 인증서 toobe 수 tooconnect의 hello 발급자를 성공적으로 신뢰 해야 기억 toohello LDAPS를 사용 하 여 도메인을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="7d54c-160">엔터프라이즈 인증 기관 또는 공개적으로 신뢰할 수 있는 인증 기관을 사용 하는 경우 불필요 toodo 아무 것도 하므로 이러한 인증서 발급자를 신뢰 하는 클라이언트 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="7d54c-161">자체 서명 된 인증서를 사용 하는 경우 hello 클라이언트 컴퓨터에서 신뢰할 수 있는 인증서 저장소 hello로 tooinstall hello hello 자체 서명 된 인증서의 공개 부분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="7d54c-162">잠금 LDAPS hello tooyour 관리 되는 도메인에 액세스할 인터넷</span><span class="sxs-lookup"><span data-stu-id="7d54c-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="7d54c-163">**선택적 작업** -LDAPS를 설정 하지 않은 경우 액세스 toohello 관리 되는 도메인 넘는 인터넷 hello,이 구성 작업을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="7d54c-164">이 작업을 시작 하기 전에 확인에 설명 된 hello 단계를 완료 한 [작업 4](#task-4---enable-secure-ldap-access-over-the-internet)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="7d54c-165">LDAPS 액세스를 위한 관리 되는 도메인 hello를 통해 노출 인터넷 보안 위협이 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="7d54c-166">hello 관리 되는 도메인은 hello에서 연결할 수 있는 보안 LDAP에 사용 되는 hello 포트에서 인터넷 (즉, 636 포트).</span><span class="sxs-lookup"><span data-stu-id="7d54c-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="7d54c-167">따라서 toorestrict 액세스 관리 toohello 도메인 toospecific 알려진 IP 주소를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="7d54c-168">보안 향상된을 위해 NSG ()를 네트워크 보안 그룹을 만들고 Azure AD 도메인 서비스를 설정한 hello 서브넷과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="7d54c-169">hello 다음 표에서 설명 샘플 NSG를 구성할 수 hello 통해 보안 LDAP 액세스 아래로 toolock 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="7d54c-170">hello NSG에는 TCP 포트를 통해 636 지정된 된 집합 에서만에서 IP 주소의 인바운드 LDAPS 액세스를 허용 하는 규칙 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="7d54c-171">hello 기본 'DenyAll' 규칙 적용 tooall 인바운드 트래픽을 다른 hello에서 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="7d54c-172">hello NSG 규칙 tooallow LDAPS 액세스 hello 통해 지정 된 IP 주소에서 인터넷에 hello DenyAll NSG 규칙 보다 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="7d54c-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![샘플 NSG toosecure LDAPS 액세스를 통해 인터넷 hello](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="7d54c-174">**자세한 정보** - [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="7d54c-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="7d54c-175">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="7d54c-175">Related content</span></span>
* [<span data-ttu-id="7d54c-176">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="7d54c-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="7d54c-177">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="7d54c-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="7d54c-178">Azure AD Domain Services 관리되는 도메인에서 그룹 정책 관리</span><span class="sxs-lookup"><span data-stu-id="7d54c-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="7d54c-179">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="7d54c-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="7d54c-180">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="7d54c-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
