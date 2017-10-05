---
title: "Azure AD Domain Services에서 보안 LDAP(LDAPS) 구성 | Microsoft Docs"
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
ms.openlocfilehash: 3aafe209aad7383cd0610d147b5fdba673023c93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2dd7d-103">Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성</span><span class="sxs-lookup"><span data-stu-id="2dd7d-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2dd7d-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="2dd7d-104">Before you begin</span></span>
<span data-ttu-id="2dd7d-105">[작업 2 - 보안 LDAP 인증서를 .PFX 파일로 내보내기](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)를 완료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="2dd7d-106">이 작업을 완료하는 데 미리 보기 Azure Portal 환경을 사용할 것인지 Azure 클래식 포털을 사용할 것인지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2dd7d-107">**Azure Portal(미리 보기)**: [Azure Portal을 사용하여 보안 LDAP를 사용하도록 설정](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="2dd7d-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="2dd7d-108">**Azure 클래식 포털**: [클래식 Azure Portal을 사용하여 보안 LDAP를 사용하도록 설정](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="2dd7d-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal"></a><span data-ttu-id="2dd7d-109">작업 3 - 클래식 Azure Portal을 사용하여 관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2dd7d-109">Task 3 - enable secure LDAP for the managed domain using the classic Azure portal</span></span>
<span data-ttu-id="2dd7d-110">보안 LDAP를 사용하도록 설정하려면 다음 구성 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="2dd7d-111">**[Azure 클래식 포털](https://manage.windowsazure.com)**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-111">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="2dd7d-112">왼쪽 창에서 **Active Directory** 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-112">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="2dd7d-113">Azure AD 도메인 서비스를 사용하도록 설정한 Azure AD 디렉터리('테넌트'라고도 함)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-113">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Azure AD 디렉터리 선택](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="2dd7d-115">**구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-115">Click the **Configure** tab.</span></span>

    ![디렉터리의 탭 구성](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="2dd7d-117">**도메인 서비스**섹션까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-117">Scroll down to the section titled **domain services**.</span></span> <span data-ttu-id="2dd7d-118">다음 스크린샷에 표시된 것처럼 **보안 LDAP(LDAPS)** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span></span>

    ![도메인 서비스 구성 섹션](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="2dd7d-120">**인증서 구성...** 단추를 클릭하면 **보안 LDAP에 대한 인증서 구성** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-120">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![보안 LDAP에 대한 인증서 구성](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="2dd7d-122">**인증서가 있는 PFX 파일** 뒤의 폴더 아이콘을 클릭하여 관리되는 도메인에 대한 보안 LDAP 액세스에 사용할 인증서가 들어 있는 PFX 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-122">Click the folder icon following **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="2dd7d-123">또한 인증서를 PFX 파일로 내보낼 때 지정한 암호도 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-123">Also enter the password you specified when exporting the certificate to the PFX file.</span></span> <span data-ttu-id="2dd7d-124">완료되면 아래쪽에 있는 [완료] 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-124">Then, click the done button on the bottom.</span></span>

    ![보안 LDAP PFX 파일 및 암호 지정](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="2dd7d-126">**구성** 탭의 **도메인 서비스** 섹션이 회색 표시되고 몇 분 동안 **보류 중...** 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-126">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="2dd7d-127">이 기간 중에 LDAPS 인증서의 정확도가 확인되고 관리되는 도메인에 대해 보안 LDAP가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-127">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![보안 LDAP - 보류 중 상태](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="2dd7d-129">관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정하는 데 약 10-15분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-129">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="2dd7d-130">제공된 보안 LDAP 인증서가 필수 조건을 만족하지 않으면 보안 LDAP는 디렉터리에 사용할 수 없으며 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-130">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="2dd7d-131">도메인 이름이 올바르지 않거나 인증서가 만료되었거나 곧 만료된다는 오류 등이 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-131">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="2dd7d-132">관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정하는 데 성공하면 **보류 중...** 메시지가 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-132">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span></span> <span data-ttu-id="2dd7d-133">표시된 인증서의 지문이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-133">You should see the thumbprint of the certificate displayed.</span></span>

    ![보안 LDAP 사용](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-the-internet"></a><span data-ttu-id="2dd7d-135">작업 4 - 인터넷을 통해 보안 LDAP 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="2dd7d-135">Task 4 - enable secure LDAP access over the internet</span></span>
<span data-ttu-id="2dd7d-136">**선택적 태스크** - 인터넷을 통해 LDAPS를 사용하여 관리되는 도메인에 액세스하지 않으려면 이 구성 태스크를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-136">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="2dd7d-137">이 태스크를 시작하기 전에 [태스크 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal)에 나와 있는 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-137">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="2dd7d-138">**구성** 페이지의 **도메인 서비스** 섹션에서 **인터넷을 통해 보안 LDAP 액세스 사용** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-138">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span></span> <span data-ttu-id="2dd7d-139">보안 LDAP를 통해 관리되는 도메인에 대한 인터넷 액세스가 기본적으로 사용되지 않으므로 이 옵션은 기본적으로 **아니요** 로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-139">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span></span>

    ![보안 LDAP 사용](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="2dd7d-141">**인터넷을 통해 보안 LDAP 액세스 사용**을 **예**로 토글합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-141">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span></span> <span data-ttu-id="2dd7d-142">아래쪽 패널에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-142">Click the **SAVE** button on the bottom panel.</span></span>
    <span data-ttu-id="2dd7d-143">![보안 LDAP 사용](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="2dd7d-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="2dd7d-144">**구성** 탭의 **도메인 서비스** 섹션이 회색 표시되고 몇 분 동안 **보류 중...** 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-144">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="2dd7d-145">잠시 동안 보안 LDAP 통한 관리되는 도메인에 대한 인터넷 액세스가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-145">After some time, internet access to your managed domain over secure LDAP is enabled.</span></span>

    ![보안 LDAP - 보류 중 상태](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="2dd7d-147">보안 LDAP를 통해 관리되는 도메인에 대한 인터넷 액세스를 사용하도록 설정하는 데 약 10분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-147">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="2dd7d-148">인터넷을 통한 관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정하는 데 성공하면 **보류 중...** 메시지가 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-148">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span></span> <span data-ttu-id="2dd7d-149">LDAPS를 통해 디렉터리에 액세스하는 데 사용할 수 있는 외부 IP 주소가 **LDAPS 액세스를 위한 외부 IP 주소**필드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-149">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![보안 LDAP 사용](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="2dd7d-151">작업 5 - 인터넷에서 관리되는 도메인에 액세스할 DNS 구성</span><span class="sxs-lookup"><span data-stu-id="2dd7d-151">Task 5 - configure DNS to access the managed domain from the internet</span></span>
<span data-ttu-id="2dd7d-152">**선택적 태스크** - 인터넷을 통해 LDAPS를 사용하여 관리되는 도메인에 액세스하지 않으려면 이 구성 태스크를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-152">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="2dd7d-153">이 태스크를 시작하기 전에 [태스크 4](#task-4---enable-secure-ldap-access-over-the-internet)에 나와 있는 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-153">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="2dd7d-154">관리되는 도메인에 대한 인터넷을 통한 보안 LDAP 액세스를 사용하도록 설정했으면 클라이언트 컴퓨터가 관리되는 도메인을 찾을 수 있도록 DNS를 업데이트 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-154">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="2dd7d-155">태스크 4의 끝에 외부 IP 주소가 **LDAPS 액세스를 위한 외부 IP 주소**의 **구성** 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-155">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="2dd7d-156">관리되는 도메인의 DNS 이름(예: 'ldaps.contoso100.com')이 이 외부 IP 주소를 가리키도록 외부 DNS 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-156">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="2dd7d-157">이 예에서는 다음과 같은 DNS 항목을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-157">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="2dd7d-158">이것으로 끝입니다. 이제 인터넷을 통해 보안 LDAP를 사용하여 관리되는 도메인에 연결할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-158">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="2dd7d-159">클라이언트 컴퓨터가 LDAPS를 사용하여 관리되는 도메인에 성공적으로 연결하려면 LDAPS 인증서의 발급자를 신뢰해야 한다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-159">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="2dd7d-160">엔터프라이즈 인증 기관 또는 공개적으로 신뢰할 수 있는 인증 기관을 사용하는 경우 클라이언트 컴퓨터가 이러한 인증서 발급자를 신뢰하므로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="2dd7d-161">자체 서명된 인증서를 사용하는 경우 자체 서명된 인증서의 공개 부분을 클라이언트 컴퓨터의 신뢰할 수 있는 인증서 저장소에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-161">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="2dd7d-162">인터넷을 통해 관리되는 도메인에 대한 LDAPS 액세스 잠금</span><span class="sxs-lookup"><span data-stu-id="2dd7d-162">Lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="2dd7d-163">**선택적 작업** - 인터넷을 통해 관리되는 도메인에 대한 LDAPS 액세스를 사용하여 않는 경우 이 구성 작업을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-163">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="2dd7d-164">이 태스크를 시작하기 전에 [태스크 4](#task-4---enable-secure-ldap-access-over-the-internet)에 나와 있는 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-164">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="2dd7d-165">인터넷을 통해 LDAPS 액세스가 가능하도록 관리되는 도메인을 노출하면 보안 위협이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-165">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="2dd7d-166">관리되는 도메인은 보안 LDAP에 사용되는 포트(즉, 포트 636)에서 인터넷을 통해 접속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-166">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="2dd7d-167">따라서 관리되는 도메인에 대한 액세스를 알려진 특정 IP 주소로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-167">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="2dd7d-168">보안이 향상되도록 NSG(네트워크 보안 그룹)를 만들고 Azure AD Domain Services를 사용하도록 설정된 서브넷과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-168">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="2dd7d-169">다음 표에서는 구성 가능한 예제 NSG를 통해 인터넷을 통한 보안 LDAP 액세스를 잠그는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-169">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="2dd7d-170">이 NSG에는 지정된 IP 주소 집합에서만 TCP 포트 636을 통해 인바운드 LDAPS 액세스를 허용하는 규칙 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-170">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="2dd7d-171">기본 'DenyAll' 규칙은 인터넷의 다른 모든 인바운드 트래픽에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-171">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="2dd7d-172">지정된 IP 주소에서 인터넷을 통해 LDAPS 액세스를 허용하는 NSG 규칙은 DenyAll NSG 규칙보다 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd7d-172">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![인터넷을 통해 LDAPS 액세스를 보안하는 예제 NSG](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="2dd7d-174">**자세한 정보** - [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="2dd7d-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="2dd7d-175">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="2dd7d-175">Related content</span></span>
* [<span data-ttu-id="2dd7d-176">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="2dd7d-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2dd7d-177">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="2dd7d-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="2dd7d-178">Azure AD Domain Services 관리되는 도메인에서 그룹 정책 관리</span><span class="sxs-lookup"><span data-stu-id="2dd7d-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="2dd7d-179">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="2dd7d-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="2dd7d-180">네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="2dd7d-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
