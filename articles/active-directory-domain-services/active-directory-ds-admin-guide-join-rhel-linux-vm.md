---
title: "Azure Active Directory 도메인 서비스: RHEL VM tooa 관리 되는 도메인에 가입 | Microsoft Docs"
description: "Red Hat Enterprise Linux 가상 컴퓨터를 가입 tooAzure AD 도메인 서비스"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="821a0-103">Red Hat Enterprise Linux 7 가상 컴퓨터 tooa 관리 되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="821a0-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="821a0-104">이 문서에서는 toojoin Red Hat Enterprise Linux (RHEL) 7 가상 컴퓨터 tooan Azure AD 도메인 서비스 도메인을 관리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="821a0-105">Red Hat Enterprise Linux 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="821a0-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="821a0-106">Hello 단계 tooprovision RHEL 7 가상 컴퓨터 hello Azure 포털을 사용 하 여 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="821a0-107">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Azure 포털 대시보드](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="821a0-109">클릭 **새로** hello 왼쪽 창에서 데이터 및 형식에 **Red Hat** hello 스크린 샷 다음 그림과 같이 hello 검색 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="821a0-110">Red Hat Enterprise Linux에 대 한 항목 hello 검색 결과에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="821a0-111">**Red Hat Enterprise Linux 7.2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![결과에서 RHEL 선택](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="821a0-113">hello에 hello 검색 결과 **모든** 창 hello Red Hat Enterprise Linux 7.2 이미지를 나열 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="821a0-114">클릭 **Red Hat Enterprise Linux 7.2** tooview hello 가상 컴퓨터 이미지에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="821a0-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![결과에서 RHEL 선택](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="821a0-116">Hello에 **Red Hat Enterprise Linux 7.2** 창의 hello 가상 컴퓨터 이미지에 대 한 자세한 정보 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="821a0-117">Hello에 **배포 모델 선택** 드롭다운에서 선택 **클래식**합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="821a0-118">Hello 클릭 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-118">Then click hello **Create** button.</span></span>

    ![이미지 세부 정보 보기](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="821a0-120">Hello에 **기본 사항** hello의 페이지 **가상 컴퓨터를 만들** 마법사, 입력 hello **호스트 이름** hello 새 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="821a0-121">Hello에 로컬 관리자 사용자 이름을 지정 **사용자 이름** 필드와 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="821a0-122">또한 된 SSH 키 tooauthenticate hello 로컬 관리자 사용자 toouse를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="821a0-123">± ֳ ֵ는 **가격 책정 계층** hello 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![VM 만들기 - 기본 페이지](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="821a0-125">Hello에 **크기** hello 페이지 **가상 컴퓨터를 만들** hello 가상 컴퓨터에 대 한 마법사, 선택 hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![VM 만들기 - 크기 선택](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="821a0-127">Hello에 **설정** hello 페이지 **가상 컴퓨터를 만들** hello 가상 컴퓨터에 대 한 마법사, 선택 hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="821a0-128">클릭 **가상 네트워크** tooselect hello 가상 네트워크 toowhich hello Linux VM을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="821a0-129">Hello에 **가상 네트워크** 블레이드, 선택 hello 가상 네트워크를 Azure AD 도메인 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="821a0-130">이 예제에서는 hello 'MyPreviewVNet' 가상 네트워크를 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![VM 만들기 - 가상 네트워크 선택](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="821a0-132">Hello에 **요약** hello 페이지 **가상 컴퓨터를 만들** 마법사 검토 하 고 클릭 hello **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![VM 만들기 - 가상 네트워크 선택됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="821a0-134">Hello RHEL 7.2 이미지에 따라 hello 새 가상 컴퓨터의 배포를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![VM 만들기 - 배포 시작됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="821a0-136">몇 분 후 hello 가상 컴퓨터에 성공적으로 배포 되 고 사용 하기 위해 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![VM 만들기 - 배포됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="821a0-138">Toohello 새로 프로 비전 된 Linux 가상 컴퓨터를 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="821a0-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="821a0-139">Azure의 hello RHEL 7.2 가상 컴퓨터가 프로비저닝된 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="821a0-140">hello 다음 태스크는 원격으로 tooconnect toohello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="821a0-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="821a0-141">**RHEL 7.2 toohello 가상 컴퓨터 연결** hello hello 문서의 지침에 따라 [어떻게 toolog Linux를 실행 하는 tooa 가상 컴퓨터에서](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="821a0-142">hello 나머지 hello 단계 hello PuTTY SSH 클라이언트 tooconnect toohello RHEL 가상 컴퓨터를 사용 하 여 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="821a0-143">자세한 내용은 참조 hello [PuTTY 다운로드 페이지](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="821a0-144">열기 hello PuTTY 프로그램.</span><span class="sxs-lookup"><span data-stu-id="821a0-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="821a0-145">Hello 입력 **호스트 이름** RHEL 가상 컴퓨터를 새로 만든 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="821a0-146">이 예제에서는 가상 컴퓨터는 hello 호스트 이름이 'contoso rhel.cloudapp.net'.</span><span class="sxs-lookup"><span data-stu-id="821a0-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="821a0-147">VM의 호스트 이름을 hello 잘 모를 경우 hello Azure 포털에서 toohello VM 대시보드를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="821a0-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![PuTTY 연결](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="821a0-149">Hello 가상 컴퓨터를 만들 때 지정한 hello 로컬 관리자 자격 증명을 사용 하 여 toohello 가상 컴퓨터에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="821a0-150">이 예제에서는 "mahesh" hello 로컬 관리자 계정을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![PuTTY 로그인](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="821a0-152">Hello Linux 가상 컴퓨터에 필요한 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="821a0-153">연결 toohello 가상 컴퓨터를 한 후 hello 다음 작업 hello 가상 컴퓨터에 도메인 가입에 대 한 필요한 tooinstall 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="821a0-154">Hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="821a0-155">**Realmd 설치:** hello realmd 패키지 도메인 가입에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="821a0-156">PuTTY 터미널에 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="821a0-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="821a0-157">sudo yum install realmd</span></span>

    ![realmd 설치](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="821a0-159">몇 분 후 hello realmd 패키지 hello 가상 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![realmd 설치됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="821a0-161">**Sssd 설치:** hello realmd 패키지 sssd tooperform 도메인 가입 작업에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="821a0-162">PuTTY 터미널에 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="821a0-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="821a0-163">sudo yum install sssd</span></span>

    ![sssd 설치](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="821a0-165">몇 분 후 hello sssd 패키지 hello 가상 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![realmd 설치됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="821a0-167">**Kerberos 설치:** PuTTY 터미널에 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="821a0-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="821a0-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![kerberos 설치](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="821a0-170">몇 분 후 hello realmd 패키지 hello 가상 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos 설치됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="821a0-172">Hello Linux 가상 컴퓨터 toohello 관리 되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="821a0-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="821a0-173">이제 필요한 hello 패키지 hello Linux 가상 컴퓨터에 설치 되 면 다음 태스크에서는 hello입니다 toojoin hello 가상 컴퓨터 toohello 관리 되는 도메인.</span><span class="sxs-lookup"><span data-stu-id="821a0-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="821a0-174">Hello AAD 도메인 서비스에 대 한 관리 되는 도메인을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="821a0-175">PuTTY 터미널에 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="821a0-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="821a0-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="821a0-178">경우 **영역 검색** 없습니다 toofind 관리 되는 도메인에는 해당 hello 도메인 hello 가상 컴퓨터 (try ping)에서 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="821a0-179">또한 해당 hello 가상 컴퓨터가 배포 된 toohello 되었습니다 실제로 확인 동일한 가상 네트워크는 hello 관리 되는 도메인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="821a0-180">kerberos를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-180">Initialize kerberos.</span></span> <span data-ttu-id="821a0-181">PuTTY 터미널 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="821a0-182">Toohello AAD ' DC Administrators' 그룹에 속한 사용자가을 지정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="821a0-183">이러한 사용자만 컴퓨터 toohello 관리 되는 도메인에 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="821a0-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="821a0-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="821a0-186">Hello 도메인 이름을 대문자로 지정, 다른 kinit 실패를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="821a0-187">Hello 컴퓨터 toohello 도메인에 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="821a0-188">PuTTY 터미널 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="821a0-189">Hello 지정 hello 단계 ('kinit') 앞에 지정 된 동일한 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="821a0-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="821a0-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Realm join](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="821a0-192">메시지 ("영역에 성공적으로 등록 된 컴퓨터")을 얻어야 hello 컴퓨터의 관리 되는 도메인에 가입된 했습니다 toohello 경우.</span><span class="sxs-lookup"><span data-stu-id="821a0-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="821a0-193">도메인 가입 확인</span><span class="sxs-lookup"><span data-stu-id="821a0-193">Verify domain join</span></span>
<span data-ttu-id="821a0-194">신속 하 게 관리 되는 도메인에 가입된 했습니다 toohello hello 컴퓨터 지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="821a0-195">Toohello 연결 새로 도메인 hello 사용자 계정을 올바르게 해결 되 면 SSH 및 도메인 사용자 계정 및 다음 검사 toosee를 사용 하 여 RHEL VM을 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="821a0-196">프로그램 PuTTY 터미널, 형식 hello 명령 tooconnect toohello 새로 다음 도메인 SSH를 사용 하 여 RHEL 가상 컴퓨터를 가입 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="821a0-197">Toohello 관리 되는 도메인에 속해 있는 도메인 계정을 사용 하 여 (예를 들어 'bob@CONTOSO100.COM' 여기서.)</span><span class="sxs-lookup"><span data-stu-id="821a0-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="821a0-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="821a0-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="821a0-199">PuTTY 터미널 hello 명령 toosee hello 홈 디렉터리 올바르게 초기화 된 경우 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="821a0-200">pwd</span><span class="sxs-lookup"><span data-stu-id="821a0-200">pwd</span></span>
3. <span data-ttu-id="821a0-201">PuTTY 터미널 hello 명령 toosee hello 그룹 멤버 자격을 올바르게 해결 되는 경우 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="821a0-202">id</span><span class="sxs-lookup"><span data-stu-id="821a0-202">id</span></span>

<span data-ttu-id="821a0-203">이러한 명령의 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-203">A sample output of these commands follows:</span></span>

![도메인 가입 확인](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="821a0-205">도메인 가입 문제 해결</span><span class="sxs-lookup"><span data-stu-id="821a0-205">Troubleshooting domain join</span></span>
<span data-ttu-id="821a0-206">Toohello 참조 [문제 해결 도메인 가입](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) 문서.</span><span class="sxs-lookup"><span data-stu-id="821a0-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="821a0-207">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="821a0-207">Related Content</span></span>
* [<span data-ttu-id="821a0-208">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="821a0-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="821a0-209">Windows Server 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="821a0-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="821a0-210">[어떻게 Linux를 실행 하는 tooa 가상 컴퓨터에서 toolog](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="821a0-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="821a0-211">Kerberos 설치</span><span class="sxs-lookup"><span data-stu-id="821a0-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="821a0-212">Red Hat Enterprise Linux 7 - Windows 통합 가이드</span><span class="sxs-lookup"><span data-stu-id="821a0-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
