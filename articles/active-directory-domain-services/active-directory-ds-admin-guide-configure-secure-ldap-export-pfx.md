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
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="d5be3-103">Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성</span><span class="sxs-lookup"><span data-stu-id="d5be3-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d5be3-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d5be3-104">Before you begin</span></span>
<span data-ttu-id="d5be3-105">[작업 1: 보안 LDAP를 위한 인증서 가져오기](active-directory-ds-admin-guide-configure-secure-ldap.md)를 완료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="d5be3-106">작업 2 - 보안 LDAP 인증서를 .PFX 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="d5be3-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="d5be3-107">이 작업을 시작하기 전에 사용자는 공용 인증 기관에서 보안 LDAP 인증서를 가져오거나 자체 서명된 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="d5be3-108">LDAPS 인증서를 .PFX 파일로 내보내려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="d5be3-109">**시작** 단추를 누르고 **R**을 입력합니다. **실행** 대화 상자에서 **mmc**를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![MMC 콘솔 시작](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="d5be3-111">**사용자 계정 컨트롤** 프롬프트에서 **예**를 클릭하고 관리자 권한으로 MMC(Microsoft Management Console)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="d5be3-112">**파일** 메뉴에서 **스냅인 추가/제거...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![MMC 콘솔에 스냅인 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="d5be3-114">**스냅인 추가/제거** 대화 상자에서 **인증서** 스냅인을 선택하고 **추가 >** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![MMC 콘솔에 인증서 스냅인 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="d5be3-116">**인증서 스냅인** 마법사에서 **컴퓨터 계정**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![컴퓨터 계정에 대한 인증서 스냅인 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="d5be3-118">**컴퓨터 선택** 페이지에서 **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)**를 선택하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![인증서 스냅인 추가 - 컴퓨터 선택](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="d5be3-120">**스냅인 추가/제거** 대화 상자에서 **확인**을 클릭하고 인증서 스냅인을 MMC에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![MMC에 인증서 스냅인 추가 - 완료](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="d5be3-122">MMC 창에서 **콘솔 루트**를 클릭하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="d5be3-123">인증서 스냅인이 로드되는 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="d5be3-124">확장할 **인증서(로컬 컴퓨터)** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="d5be3-125">**개인** 노드, **인증서** 노드를 차례로 클릭하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![개인 인증서 저장소 열기](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="d5be3-127">앞서 만든 자체 서명된 인증서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="d5be3-128">인증서의 속성을 검사하여 지문이 인증서를 만들 때 PowerShell 창에 보고된 것과 일치하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="d5be3-129">자체 서명된 인증서를 선택하고 **마우스 오른쪽 단추로 클릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="d5be3-130">오른쪽 클릭 메뉴에서 **모든 태스크**를 선택하고 **내보내기...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![인증서 내보내기](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="d5be3-132">**인증서 내보내기 마법사**에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![인증서 내보내기 마법사](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="d5be3-134">**개인 키 내보내기** 페이지에서 **예, 개인 키를 내보냅니다.**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![인증서 개인 키 내보내기](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="d5be3-136">인증서와 함께 개인 키를 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="d5be3-137">인증서에 대한 개인 키가 없는 PFX를 제공하면 관리되는 도메인에 대한 보안 LDAP 설정에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="d5be3-138">**파일 형식 내보내기** 페이지에서 내보낸 인증서에 대한 파일 형식으로 **개인 정보 교환 – PKCS #12(.PFX)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![인증서 내보내기 파일 형식](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="d5be3-140">.PFX 파일 형식만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="d5be3-141">인증서를 .CER 파일 형식으로 내보내지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d5be3-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="d5be3-142">**보안** 페이지에서 **암호** 옵션을 선택하고 암호를 입력하여 .PFX 파일을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="d5be3-143">다음 작업에 필요하므로 이 암호를 기억해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="d5be3-144">**다음** 을 클릭하여 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="d5be3-145">인증서 내보내기에 대한 암호</span><span class="sxs-lookup"><span data-stu-id="d5be3-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="d5be3-146">이 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-146">Make a note of this password.</span></span> <span data-ttu-id="d5be3-147">[작업 3 - 관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)에서 이 관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="d5be3-148">**내보낼 파일** 페이지에서 파일 이름 및 인증서를 내보낼 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![인증서 내보내기에 대한 경로](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="d5be3-150">다음 페이지에서 **마침** 을 클릭하여 인증서를 PFX 파일로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="d5be3-151">인증서를 내보내면 확인 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5be3-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![인증서 내보내기 완료](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="d5be3-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d5be3-153">Next step</span></span>
[<span data-ttu-id="d5be3-154">작업 3 - 관리되는 도메인에 대해 보안 LDAP를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d5be3-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
