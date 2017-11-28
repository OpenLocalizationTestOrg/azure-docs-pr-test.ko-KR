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
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="5700b-103">Azure AD Domain Services 관리되는 도메인에 대해 보안 LDAP(LDAPS) 구성</span><span class="sxs-lookup"><span data-stu-id="5700b-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5700b-104">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5700b-104">Before you begin</span></span>
<span data-ttu-id="5700b-105">[작업 1: 보안 LDAP를 위한 인증서 가져오기](active-directory-ds-admin-guide-configure-secure-ldap.md)를 완료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="5700b-106">작업 2-hello 보안 LDAP 인증서 tooa 내보냅니다. PFX 파일</span><span class="sxs-lookup"><span data-stu-id="5700b-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="5700b-107">이 작업을 시작 하기 전에 hello 보안 LDAP 인증서 공용 인증 기관에서 얻은 하거나 만든 자체 서명 된 인증서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="5700b-108">Tooexport hello LDAPS 인증서 tooa, hello 다음 단계를 수행 합니다. PFX 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="5700b-109">키를 눌러 hello **시작** 단추 및 형식 **R**합니다. Hello에 **실행** 대화 상자에서 형식 **mmc** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Hello MMC 콘솔을 시작 합니다.](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="5700b-111">Hello에 **사용자 계정 컨트롤** 확인을 클릭 **예** toolaunch 관리자 권한으로 MMC (Microsoft Management Console)입니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="5700b-112">Hello에서 **파일** 메뉴를 클릭 하 여 **스냅인 추가/제거...** .</span><span class="sxs-lookup"><span data-stu-id="5700b-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![콘솔의 스냅인 tooMMC 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="5700b-114">Hello에 **추가 또는 제거 스냅인** 대화 상자에서 선택 hello **인증서** 스냅인 hello 클릭 **추가 >** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![인증서 스냅인 tooMMC 콘솔 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="5700b-116">Hello에 **인증서 스냅인** 선택 마법사 **컴퓨터 계정** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![컴퓨터 계정에 대한 인증서 스냅인 추가](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="5700b-118">Hello에 **컴퓨터 선택** 페이지 **로컬 컴퓨터: (hello이이 콘솔이 실행 되 고)** 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![인증서 스냅인 추가 - 컴퓨터 선택](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="5700b-120">Hello에 **추가 또는 제거 스냅인** 대화 상자를 클릭 하 여 **확인** tooadd hello 인증서 스냅인 tooMMC 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![인증서 스냅인 tooMMC-완료를 추가 합니다.](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="5700b-122">Hello MMC 창에서 클릭 tooexpand **콘솔 루트**합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="5700b-123">Hello 인증서 스냅인을 로드 하는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="5700b-124">클릭 **인증서 (로컬 컴퓨터)** tooexpand 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="5700b-125">Tooexpand hello 클릭 **개인** 노드, hello **인증서** 노드.</span><span class="sxs-lookup"><span data-stu-id="5700b-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![개인 인증서 저장소 열기](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="5700b-127">만든 자체 서명 된 인증서를 hello 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="5700b-128">Hello 인증서 tooensure hello 지문이 일치 항목의 hello 인증서를 만들 때 PowerShell windows hello에서 보고 하는 hello 속성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="5700b-129">선택 hello 자체 서명 된 인증서 및 **마우스 오른쪽 단추로 클릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="5700b-130">Hello 오른쪽 클릭 메뉴에서 선택 **모든 작업** 선택 **내보내기...** .</span><span class="sxs-lookup"><span data-stu-id="5700b-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![인증서 내보내기](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="5700b-132">Hello에 **인증서 내보내기 마법사**, 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![인증서 내보내기 마법사](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="5700b-134">Hello에 **개인 키 내보내기** 페이지에서 **예, hello 개인 키 내보내기**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![인증서 개인 키 내보내기](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="5700b-136">Hello hello 인증서와 함께 개인 키를 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="5700b-137">Hello hello 인증서 개인 키를 포함 하지 않는 PFX를 제공 하는 경우 관리 되는 도메인에 대 한 보안 LDAP를 사용 하면 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="5700b-138">Hello에 **파일 내보내기 형식** 페이지에서 **개인 정보 교환-PKCS #12 (합니다. PFX)** 내보낸 인증서의 hello에 대 한 hello 파일 형식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![인증서 내보내기 파일 형식](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="5700b-140">Hello만 합니다. PFX 파일 형식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="5700b-141">Hello 인증서 toohello를 내보내지 않습니다. CER 파일 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="5700b-142">Hello에 **보안** 페이지, 선택 hello **암호** 옵션과 암호 tooprotect hello 입력 합니다. PFX 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="5700b-143">Hello 다음 작업에 필요 하므로이 암호를 기억해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="5700b-144">클릭 **다음** tooproceed 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="5700b-145">인증서 내보내기에 대한 암호</span><span class="sxs-lookup"><span data-stu-id="5700b-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="5700b-146">이 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-146">Make a note of this password.</span></span> <span data-ttu-id="5700b-147">이 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정 하는 동안 필요한 [작업 3-hello 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="5700b-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="5700b-148">Hello에 **파일 tooExport** 페이지 hello 파일 이름 및 원하는 사이트로 tooexport hello 인증서 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![인증서 내보내기에 대한 경로](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="5700b-150">Hello에서 다음 페이지에서 클릭 **마침** tooexport hello 인증서 tooa PFX 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="5700b-151">Hello 인증서를 내보낸 경우 확인 대화 상자를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5700b-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![인증서 내보내기 완료](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="5700b-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5700b-153">Next step</span></span>
[<span data-ttu-id="5700b-154">작업 3-hello 관리 되는 도메인에 대 한 보안 LDAP를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="5700b-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
