---
title: "Azure Active Directory Domain Services: 관리되는 도메인에 RHEL VM 가입 | Microsoft Docs"
description: "Red Hat Enterprise Linux 가상 컴퓨터를 Azure AD 도메인 서비스에 가입"
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
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="e1f2d-103">Red Hat Enterprise Linux 7 가상 컴퓨터를 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="e1f2d-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="e1f2d-104">이 문서에서는 Red Hat Enterprise Linux(RHEL) 7 가상 컴퓨터를 Azure AD 도메인 서비스 관리되는 도메인에 가입하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="e1f2d-105">Red Hat Enterprise Linux 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="e1f2d-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="e1f2d-106">Azure 포털을 사용하여 RHEL 7 가상 컴퓨터를 프로비전하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="e1f2d-107">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Azure 포털 대시보드](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="e1f2d-109">왼쪽 창에서 **새로 만들기**를 클릭하고 아래 스크린샷에 표시된 대로 검색 표시줄에 **Red Hat**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="e1f2d-110">검색 결과에 Red Hat Enterprise Linux에 대한 항목이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="e1f2d-111">**Red Hat Enterprise Linux 7.2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![결과에서 RHEL 선택](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="e1f2d-113">**모든 항목** 창의 검색 결과에 Red Hat Enterprise Linux 7.2 이미지가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="e1f2d-114">가상 컴퓨터 이미지에 대한 자세한 내용을 보려면 **Red Hat Enterprise Linux 7.2** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![결과에서 RHEL 선택](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="e1f2d-116">**Red Hat Enterprise Linux 7.2** 창에 가상 컴퓨터 이미지에 대한 자세한 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="e1f2d-117">**배포 모델 선택** 드롭다운에서 **클래식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="e1f2d-118">그런 다음 **만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-118">Then click the **Create** button.</span></span>

    ![이미지 세부 정보 보기](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="e1f2d-120">**가상 컴퓨터 만들기** 마법사의 **기본** 페이지에서 새 가상 컴퓨터의 **호스트 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="e1f2d-121">또한 **사용자 이름** 필드에 로컬 관리자 사용자 이름을 지정하고 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="e1f2d-122">로컬 관리자 사용자를 인증하는 데 SSH 키를 사용하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="e1f2d-123">가상 컴퓨터에 대한 **가격 책정 계층** 도 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![VM 만들기 - 기본 페이지](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="e1f2d-125">**가상 컴퓨터 만들기** 마법사의 **크기** 페이지에서 가상 컴퓨터의 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![VM 만들기 - 크기 선택](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="e1f2d-127">**가상 컴퓨터 만들기** 마법사의 **설정** 페이지에서 가상 컴퓨터의 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="e1f2d-128">**가상 네트워크**를 클릭하여 Linux VM을 배포할 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="e1f2d-129">**가상 네트워크** 블레이드에서 Azure AD 도메인 서비스를 사용할 수 있는 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="e1f2d-130">이 예제에서는 'MyPreviewVNet' 가상 네트워크를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![VM 만들기 - 가상 네트워크 선택](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="e1f2d-132">**가상 컴퓨터 만들기** 마법사의 **요약**에서 검토하고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![VM 만들기 - 가상 네트워크 선택됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="e1f2d-134">RHEL 7.2 이미지에 따라 새 가상 컴퓨터의 배포가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![VM 만들기 - 배포 시작됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="e1f2d-136">몇 분 후 가상 컴퓨터가 성공적으로 배포되고 사용할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![VM 만들기 - 배포됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="e1f2d-138">새로 프로비전된 Linux 가상 컴퓨터에 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="e1f2d-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="e1f2d-139">RHEL 7.2 가상 컴퓨터가 Azure에서 프로비전되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="e1f2d-140">다음 작업은 가상 컴퓨터에 원격으로 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="e1f2d-141">**RHEL 7.2 가상 컴퓨터에 연결** [Linux를 실행하는 가상 컴퓨터에 로그온하는 방법](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e1f2d-142">나머지 단계에서는 PuTTY SSH 클라이언트를 사용하여 RHEL 가상 컴퓨터에 연결하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="e1f2d-143">자세한 내용은 [PuTTY 다운로드 페이지](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="e1f2d-144">PuTTY 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="e1f2d-145">새로 만든 RHEL 가상 컴퓨터에 대한 **호스트 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="e1f2d-146">이 예제에서 가상 컴퓨터의 호스트 이름은 'contoso-rhel.cloudapp.net'입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="e1f2d-147">VM의 호스트 이름을 정확히 알지 못하는 경우 Azure 포털에서 VM 대시보드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![PuTTY 연결](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="e1f2d-149">가상 컴퓨터를 만들 때 지정한 로컬 관리자 자격 증명을 사용하여 가상 컴퓨터에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="e1f2d-150">이 예제에서는 로컬 관리자 계정 "mahesh"를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![PuTTY 로그인](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="e1f2d-152">Linux 가상 컴퓨터에 필요한 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="e1f2d-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="e1f2d-153">가상 컴퓨터에 연결된 후 다음 작업은 도메인 가입에 필요한 패키지를 가상 컴퓨터에 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="e1f2d-154">다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-154">Perform the following steps:</span></span>

1. <span data-ttu-id="e1f2d-155">**realmd 설치:** 도메인 가입에 realmd 패키지가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="e1f2d-156">PuTTY 터미널에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="e1f2d-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="e1f2d-157">sudo yum install realmd</span></span>

    ![realmd 설치](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="e1f2d-159">몇 분 후 realmd 패키지가 가상 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![realmd 설치됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="e1f2d-161">**sssd 설치:** 도메인 가입 작업을 수행하는 데 realmd 패키지는 sssd에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="e1f2d-162">PuTTY 터미널에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="e1f2d-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="e1f2d-163">sudo yum install sssd</span></span>

    ![sssd 설치](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="e1f2d-165">몇 분 후 sssd 패키지가 가상 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![realmd 설치됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="e1f2d-167">**kerberos 설치:** PuTTY 터미널에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="e1f2d-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="e1f2d-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![kerberos 설치](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="e1f2d-170">몇 분 후 realmd 패키지가 가상 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos 설치됨](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="e1f2d-172">Linux 가상 컴퓨터를 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="e1f2d-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="e1f2d-173">이제 필요한 패키지를 Linux 가상 컴퓨터에 설치했고 다음 작업은 가상 컴퓨터를 관리되는 도메인에 가입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="e1f2d-174">AAD 도메인 서비스 관리되는 도메인을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="e1f2d-175">PuTTY 터미널에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="e1f2d-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="e1f2d-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="e1f2d-178">**realm discover** 로 관리되는 도메인을 찾을 수 없는 경우 가상 컴퓨터에서 도메인에 연결할 수 있는지 확인합니다(ping 시도).</span><span class="sxs-lookup"><span data-stu-id="e1f2d-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="e1f2d-179">또한 관리되는 도메인을 사용할 수 있는 동일한 가상 네트워크에 가상 컴퓨터를 확실히 배포했는지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="e1f2d-180">kerberos를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-180">Initialize kerberos.</span></span> <span data-ttu-id="e1f2d-181">PuTTY 터미널에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="e1f2d-182">'AAD DC 관리자' 그룹에 속한 사용자를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="e1f2d-183">이러한 사용자만 관리되는 도메인에 컴퓨터를 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="e1f2d-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="e1f2d-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="e1f2d-186">도메인 이름을 대문자로 지정해야 하며 그렇지 않으면 kinit가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="e1f2d-187">컴퓨터를 도메인에 가입합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-187">Join the machine to the domain.</span></span> <span data-ttu-id="e1f2d-188">PuTTY 터미널에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="e1f2d-189">이전 단계에서 지정한 동일한 사용자('kinit')를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="e1f2d-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="e1f2d-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Realm join](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="e1f2d-192">컴퓨터가 관리되는 도메인에 성공적으로 가입되면 메시지("Successfully enrolled machine in realm")가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="e1f2d-193">도메인 가입 확인</span><span class="sxs-lookup"><span data-stu-id="e1f2d-193">Verify domain join</span></span>
<span data-ttu-id="e1f2d-194">컴퓨터가 관리되는 도메인에 성공적으로 가입되었는지 여부를 신속하게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="e1f2d-195">SSH 및 도메인 사용자 계정을 사용하여 새로 도메인에 가입된 RHEL VM에 연결한 후 사용자 계정이 올바르게 확인되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="e1f2d-196">PuTTY 터미널에서 다음 명령을 입력하고 SSH를 사용하여 새로 도메인에 가입된 RHEL 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="e1f2d-197">관리되는 도메인에 속하는 도메인 계정을 사용합니다(예: 여기서는 ‘bob@CONTOSO100.COM’).</span><span class="sxs-lookup"><span data-stu-id="e1f2d-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="e1f2d-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e1f2d-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="e1f2d-199">PuTTY 터미널에서 다음 명령을 입력하여 홈 디렉터리가 올바르게 초기화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="e1f2d-200">pwd</span><span class="sxs-lookup"><span data-stu-id="e1f2d-200">pwd</span></span>
3. <span data-ttu-id="e1f2d-201">PuTTY 터미널에서 다음 명령을 입력하여 그룹 멤버 자격이 올바르게 확인되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="e1f2d-202">id</span><span class="sxs-lookup"><span data-stu-id="e1f2d-202">id</span></span>

<span data-ttu-id="e1f2d-203">이러한 명령의 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-203">A sample output of these commands follows:</span></span>

![도메인 가입 확인](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="e1f2d-205">도메인 가입 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e1f2d-205">Troubleshooting domain join</span></span>
<span data-ttu-id="e1f2d-206">[도메인 가입 문제 해결](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1f2d-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="e1f2d-207">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="e1f2d-207">Related Content</span></span>
* [<span data-ttu-id="e1f2d-208">Azure AD 도메인 서비스 - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="e1f2d-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="e1f2d-209">Windows Server 가상 컴퓨터를 Azure AD 도메인 서비스 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="e1f2d-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="e1f2d-210">[Linux를 실행하는 가상 컴퓨터에 로그온하는 방법](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e1f2d-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="e1f2d-211">Kerberos 설치</span><span class="sxs-lookup"><span data-stu-id="e1f2d-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="e1f2d-212">Red Hat Enterprise Linux 7 - Windows 통합 가이드</span><span class="sxs-lookup"><span data-stu-id="e1f2d-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
