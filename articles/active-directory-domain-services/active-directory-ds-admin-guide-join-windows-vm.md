---
title: "Azure Active Directory Domain Services: 관리되는 도메인에 Windows Server VM 가입 | Microsoft Docs"
description: "Windows Server 가상 컴퓨터를 Azure AD 도메인 서비스에 가입"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9f8d21f6964d26a2e17e31d1f2947e7eb07c177d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="3ee9b-103">Windows Server 가상 컴퓨터를 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="3ee9b-103">Join a Windows Server virtual machine to a managed domain</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ee9b-104">Azure 클래식 포털 - Windows</span><span class="sxs-lookup"><span data-stu-id="3ee9b-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="3ee9b-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="3ee9b-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

<span data-ttu-id="3ee9b-106">이 문서에서는 Azure 클래식 포털을 사용하여 Windows Server 2012 R2를 실행하는 가상 컴퓨터를 Azure AD 도메인 서비스는 관리되는 도메인에 가입하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-106">This article shows you how to join a virtual machine running Windows Server 2012 R2 to an Azure AD Domain Services managed domain, using the Azure classic portal.</span></span>

## <a name="step-1-create-the-windows-server-virtual-machine"></a><span data-ttu-id="3ee9b-107">1단계: Windows Server 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="3ee9b-107">Step 1: Create the Windows Server virtual machine</span></span>
<span data-ttu-id="3ee9b-108">[Azure 클래식 포털에서 Windows Server를 실행하는 가상 컴퓨터 만들기](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 자습서에 나와 있는 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-108">Follow the instructions outlined in the [Create a virtual machine running Windows in the Azure classic portal](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) tutorial.</span></span> <span data-ttu-id="3ee9b-109">이 새로 만든 가상 컴퓨터는 반드시 Azure AD 도메인 서비스가 사용하도록 설정된 동일한 가상 네트워크에 가입되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-109">It is important to ensure that this newly created virtual machine is joined to the same virtual network in which you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="3ee9b-110">'빠른 생성' 옵션으로는 가상 컴퓨터를 가상 네트워크에 가입할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-110">The 'Quick Create' option does not enable you to join the virtual machine to a virtual network.</span></span> <span data-ttu-id="3ee9b-111">따라서 가상 컴퓨터를 만들려면 '갤러리에서' 옵션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-111">Therefore, you need to use the 'From Gallery' option to create the virtual machine.</span></span>

<span data-ttu-id="3ee9b-112">Azure AD 도메인 서비스가 사용하도록 설정된 가상 네트워크에 가입할 Windows 가상 컴퓨터를 만들기 위해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-112">Perform the following steps to create a Windows virtual machine joined to the virtual network in which you've enabled Azure AD Domain Services.</span></span>

1. <span data-ttu-id="3ee9b-113">Azure 클래식 포털의 창 맨 아래의 명령 모음에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-113">In the Azure classic portal, on the command bar at the bottom of the window, click **New**.</span></span>
2. <span data-ttu-id="3ee9b-114">**계산**에서 **가상 컴퓨터**를 클릭한 후 **갤러리에서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-114">Under **Compute**, click **Virtual Machine**, then click **From Gallery**.</span></span>
3. <span data-ttu-id="3ee9b-115">첫 번째 화면의 사용 가능한 이미지 목록에서 가상 컴퓨터의 **이미지를 선택** 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-115">The first screen lets you **Choose an Image** for your virtual machine from the list of available images.</span></span> <span data-ttu-id="3ee9b-116">적절한 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-116">Pick the appropriate image.</span></span>

    ![이미지 선택](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. <span data-ttu-id="3ee9b-118">두 번째 화면에서는 컴퓨터 이름, 크기 및 관리자 사용자 이름과 암호를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-118">The second screen lets you pick a computer name, size, and administrative user name and password.</span></span> <span data-ttu-id="3ee9b-119">앱 또는 워크로드를 실행하는 데 필요한 계층과 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-119">Use the tier and size required to run your app or workload.</span></span> <span data-ttu-id="3ee9b-120">여기에서 선택할 사용자 이름은 컴퓨터에서 로컬 관리자 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-120">The user name you pick here is a local administrator user on the machine.</span></span> <span data-ttu-id="3ee9b-121">여기에 도메인 사용자 계정 자격 증명을 입력하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-121">Do not enter a domain user account's credentials here.</span></span>

    ![가상 컴퓨터 구성](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. <span data-ttu-id="3ee9b-123">세 번째 화면에서는 네트워킹, 저장소 및 가용성에 대한 리소스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-123">The third screen lets you configure resources for networking, storage, and availability.</span></span> <span data-ttu-id="3ee9b-124">**지역/선호도 그룹/가상 네트워크** 드롭다운에서 Azure AD 도메인 서비스를 사용하도록 설정한 가상 네트워크를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-124">Ensure you select the virtual network in which you enabled Azure AD Domain Services from the **Region/Affinity Group/Virtual Network** dropdown.</span></span> <span data-ttu-id="3ee9b-125">필요에 따라 가상 컴퓨터에 대한 **클라우드 서비스 DNS 이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-125">Specify a **Cloud Service DNS Name** as appropriate for the virtual machine.</span></span>

    ![가상 컴퓨터에 대한 가상 네트워크 선택](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > <span data-ttu-id="3ee9b-127">Azure AD 도메인 서비스를 사용하도록 설정한 동일한 가상 네트워크에 가상 컴퓨터를 가입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-127">Ensure that you join the virtual machine to the same virtual network in which you've enabled Azure AD Domain Services.</span></span> <span data-ttu-id="3ee9b-128">결과적으로 가상 컴퓨터에서 도메인을 '볼' 수 있으며 도메인 가입 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-128">As a result, the virtual machine can 'see' the domain and perform tasks such as joining the domain.</span></span> <span data-ttu-id="3ee9b-129">다른 가상 네트워크에 가상 컴퓨터를 만들도록 선택한 경우 가상 네트워크를 Azure AD 도메인 서비스가 사용하도록 설정된 가상 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-129">If you choose to create the virtual machine in a different virtual network, connect that virtual network to the virtual network in which you've enabled Azure AD Domain Services.</span></span>
   >
   >
6. <span data-ttu-id="3ee9b-130">네 번째 화면에서는 VM 에이전트를 설치하고 사용 가능한 확장 중 일부를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-130">The fourth screen lets you install the VM Agent and configure some of the available extensions.</span></span>

    ![완료된](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. <span data-ttu-id="3ee9b-132">가상 컴퓨터가 만들어지면 클래식 포털의 **가상 컴퓨터** 노드 아래에 새 가상 컴퓨터가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-132">After the virtual machine is created, the classic portal lists the new virtual machine under the **Virtual Machines** node.</span></span> <span data-ttu-id="3ee9b-133">가상 컴퓨터와 클라우드 서비스가 둘 다 자동으로 시작되고 해당 상태가 **실행 중**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-133">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

    ![가상 컴퓨터가 시작되어 실행 중](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-to-the-windows-server-virtual-machine-using-the-local-administrator-account"></a><span data-ttu-id="3ee9b-135">2단계: 로컬 관리자 계정을 사용하여 Windows Server 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="3ee9b-135">Step 2: Connect to the Windows Server virtual machine using the local administrator account</span></span>
<span data-ttu-id="3ee9b-136">이제 도메인에 가입하기 위해 새로 만든 Windows Server 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-136">Now, we connect to the newly created Windows Server virtual machine, to join it to the domain.</span></span> <span data-ttu-id="3ee9b-137">연결하려면 가상 컴퓨터를 만들 때 지정한 로컬 관리자 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-137">Use the local administrator credentials you specified when creating the virtual machine, to connect to it.</span></span>

<span data-ttu-id="3ee9b-138">다음 단계를 수행하여 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-138">Perform the following steps to connect to the virtual machine.</span></span>

1. <span data-ttu-id="3ee9b-139">클래식 포털에서 **가상 컴퓨터** 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-139">Navigate to **Virtual Machines** node in the classic portal.</span></span> <span data-ttu-id="3ee9b-140">1단계에서 만든 가상 컴퓨터를 선택하고 창 아래쪽에 있는 명령 모음에서 **연결** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-140">Select the virtual machine you created in Step 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![Windows 가상 컴퓨터에 연결](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="3ee9b-142">클래식 포털에 가상 컴퓨터에 연결하는 데 사용되는 ‘.rdp’ 확장명을 가진 파일을 열거나 저장하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-142">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="3ee9b-143">다운로드가 완료되면 클릭하여 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-143">Click to open the file when it has finished downloading.</span></span>
3. <span data-ttu-id="3ee9b-144">로그인 프롬프트에서 가상 컴퓨터를 만드는 동안 지정한 **로컬 관리자 자격 증명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-144">At the login prompt, enter your **local administrator credentials**, which you specified while creating the virtual machine.</span></span> <span data-ttu-id="3ee9b-145">예를 들어 이 예에서 'localhost\mahesh'를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-145">For example, we've used 'localhost\mahesh' in this example.</span></span>

<span data-ttu-id="3ee9b-146">이때 로컬 관리자 자격 증명을 사용하여 새로 만든 Windows 가상 컴퓨터에 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-146">At this point, you should be logged in to the newly created Windows virtual machine using local Administrator credentials.</span></span> <span data-ttu-id="3ee9b-147">다음 단계는 가상 컴퓨터를 도메인에 가입하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-147">The next step is to join the virtual machine to the domain.</span></span>

## <a name="step-3-join-the-windows-server-virtual-machine-to-the-aad-ds-managed-domain"></a><span data-ttu-id="3ee9b-148">3단계: Windows Server 가상 컴퓨터를 AAD-DS 관리되는 도메인에 가입</span><span class="sxs-lookup"><span data-stu-id="3ee9b-148">Step 3: Join the Windows Server virtual machine to the AAD-DS managed domain</span></span>
<span data-ttu-id="3ee9b-149">Windows Server 가상 컴퓨터를 AAD-DS 관리되는 도메인에 가입하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-149">Perform the following steps to join the Windows Server virtual machine to the AAD-DS managed domain.</span></span>

1. <span data-ttu-id="3ee9b-150">2단계에서와 같이 Windows Server에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-150">Connect to the Windows Server as shown in Step 2.</span></span> <span data-ttu-id="3ee9b-151">시작 화면에서 **서버 관리자**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-151">From the Start screen, open **Server Manager**.</span></span>
2. <span data-ttu-id="3ee9b-152">서버 관리자 창의 왼쪽 창에서 **로컬 서버** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-152">Click **Local Server** in the left pane of the Server Manager window.</span></span>

    ![가상 컴퓨터에서 서버 관리자 시작](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. <span data-ttu-id="3ee9b-154">**속성** 섹션 아래에서 **작업 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-154">Click **WORKGROUP** under the **PROPERTIES** section.</span></span> <span data-ttu-id="3ee9b-155">**시스템 속성** 속성 페이지에서 **변경**을 클릭하여 도메인에 가입합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-155">In the **System Properties** property page, click **Change** to join the domain.</span></span>

    ![시스템 속성 페이지](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. <span data-ttu-id="3ee9b-157">**도메인** 텍스트 상자에 Azure AD 도메인 서비스 관리되는 도메인의 도메인 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-157">Specify the domain name of your Azure AD Domain Services managed domain in the **Domain** textbox and click **OK**.</span></span>

    ![가입할 도메인 지정](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. <span data-ttu-id="3ee9b-159">도메인에 가입하려면 자격 증명을 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-159">You are prompted to enter your credentials to join the domain.</span></span> <span data-ttu-id="3ee9b-160">**'AAD DC 관리자' 그룹에 속한 사용자의 자격 증명을 지정** 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-160">Ensure that you **specify the credentials for a user belonging to the AAD DC Administrators** group.</span></span> <span data-ttu-id="3ee9b-161">이 그룹의 멤버만 관리되는 도메인에 컴퓨터를 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-161">Only members of this group have privileges to join machines to the managed domain.</span></span>

    ![도메인 가입에 자격 증명 지정](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. <span data-ttu-id="3ee9b-163">다음 방법 중 하나로 자격 증명을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-163">You can specify credentials in either of the following ways:</span></span>

   * <span data-ttu-id="3ee9b-164">UPN 형식: Azure AD에 구성된 대로 사용자 계정에 대한 UPN 접미사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-164">UPN format: Specify the UPN suffix for the user account, as configured in Azure AD.</span></span> <span data-ttu-id="3ee9b-165">이 예제에서 'bob' 사용자의 UPN 접미사는 'bob@domainservicespreview.onmicrosoft.com'입니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-165">In this example, the UPN suffix of the user 'bob' is 'bob@domainservicespreview.onmicrosoft.com'.</span></span>
   * <span data-ttu-id="3ee9b-166">SAMAccountName 형식: SAMAccountName 형식으로 계정 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-166">SAMAccountName format: You can specify the account name in the SAMAccountName format.</span></span> <span data-ttu-id="3ee9b-167">이 예제에서 'bob' 사용자는 'CONTOSO100\bob'로 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-167">In this example, the user 'bob' would need to enter 'CONTOSO100\bob'.</span></span>

     > [!NOTE]
     > <span data-ttu-id="3ee9b-168">**UPN 형식을 사용하여 자격 증명을 지정하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="3ee9b-168">**We recommend using the UPN format to specify credentials.**</span></span> <span data-ttu-id="3ee9b-169">사용자의 UPN 접두사가 지나치게 긴 경우(예: 'joereallylongnameuser') SAMAccountName이 자동으로 생성될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-169">The SAMAccountName may be auto-generated if a user's UPN prefix is overly long (for example, 'joereallylongnameuser').</span></span> <span data-ttu-id="3ee9b-170">Azure AD 테넌트에서 여러 사용자가 동일한 UPN 접미사(예: 'bob')를 사용하는 경우 SAMAccountName 형식이 시스템에서 자동으로 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-170">If multiple users have the same UPN prefix (for example, 'bob') in your Azure AD tenant, their SAMAccountName format may be auto-generated by the service.</span></span> <span data-ttu-id="3ee9b-171">이러한 경우 UPN 형식을 사용하여 도메인에 안전하게 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-171">In these cases, the UPN format can be used reliably to log in to the domain.</span></span>
     >
     >
7. <span data-ttu-id="3ee9b-172">도메인 가입에 성공한 후 도메인을 시작한다는 다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-172">After domain join is successful, you see the following message welcoming you to the domain.</span></span> <span data-ttu-id="3ee9b-173">도메인 가입 작업을 완료하도록 가상 컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-173">Restart the virtual machine for the domain join operation to complete.</span></span>

    ![도메인 시작](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="3ee9b-175">도메인 가입 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3ee9b-175">Troubleshooting domain join</span></span>
### <a name="connectivity-issues"></a><span data-ttu-id="3ee9b-176">연결 문제</span><span class="sxs-lookup"><span data-stu-id="3ee9b-176">Connectivity issues</span></span>
<span data-ttu-id="3ee9b-177">가상 컴퓨터에서 도메인을 찾을 수 없는 경우 다음 문제 해결 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-177">If the virtual machine is unable to find the domain, refer to the following troubleshooting steps:</span></span>

* <span data-ttu-id="3ee9b-178">가상 컴퓨터가 도메인 서비스를 사용하도록 설정한 동일한 가상 네트워크에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-178">Ensure that the virtual machine is connected to the same virtual network as that you've enabled Domain Services in.</span></span> <span data-ttu-id="3ee9b-179">그렇지 않은 경우 가상 컴퓨터를 도메인에 연결할 수 없으므로 도메인에 가입할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-179">If not, the virtual machine is unable to connect to the domain and therefore is unable to join the domain.</span></span>
* <span data-ttu-id="3ee9b-180">가상 컴퓨터를 다른 가상 네트워크에 연결하는 경우 이 가상 네트워크가 도메인 서비스가 사용하도록 설정된 가상 네트워크에 연결되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-180">If the virtual machine is connected to another virtual network, ensure that this virtual network is connected to the virtual network in which you've enabled Domain Services.</span></span>
* <span data-ttu-id="3ee9b-181">관리되는 도메인의 도메인 이름을 사용하여 도메인에 ping을 시도합니다(예: 'ping contoso100.com').</span><span class="sxs-lookup"><span data-stu-id="3ee9b-181">Try to ping the domain using the domain name of the managed domain (for example, 'ping contoso100.com').</span></span> <span data-ttu-id="3ee9b-182">작업이 불가능한 경우 Azure AD 도메인 서비스를 사용하도록 설정된 페이지에 표시된 도메인의 IP 주소에 ping을 시도합니다(예: 'ping 10.0.0.4').</span><span class="sxs-lookup"><span data-stu-id="3ee9b-182">If you're unable to do so, try to ping the IP addresses for the domain displayed on the page where you enabled Azure AD Domain Services (for example, 'ping 10.0.0.4').</span></span> <span data-ttu-id="3ee9b-183">IP 주소에는 ping을 수행할 수 있지만 도메인에는 수행할 수 없는 경우 DNS가 잘못 구성되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-183">If you're able to ping the IP address but not the domain, DNS may be incorrectly configured.</span></span> <span data-ttu-id="3ee9b-184">가상 네트워크에 대한 DNS 서버로 도메인의 IP 주소를 구성하지 않았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-184">You may not have configured the IP addresses of the domain as DNS servers for the virtual network.</span></span>
* <span data-ttu-id="3ee9b-185">가상 컴퓨터에서 DNS 확인자 캐시를 플러시해 보세요('ipconfig /flushdns').</span><span class="sxs-lookup"><span data-stu-id="3ee9b-185">Try flushing the DNS resolver cache on the virtual machine ('ipconfig /flushdns').</span></span>

<span data-ttu-id="3ee9b-186">도메인 가입을 위한 자격 증명을 묻는 대화 상자가 표시되면 연결 문제는 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-186">If you get to the dialog box that asks for credentials to join the domain, you do not have connectivity issues.</span></span>

### <a name="credentials-related-issues"></a><span data-ttu-id="3ee9b-187">자격 증명 관련 문제</span><span class="sxs-lookup"><span data-stu-id="3ee9b-187">Credentials-related issues</span></span>
<span data-ttu-id="3ee9b-188">자격 증명을 사용하는 데 문제가 있고 도메인에 가입할 수 없는 경우 다음 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-188">Refer to the following steps if you're having trouble with credentials and are unable to join the domain.</span></span>

* <span data-ttu-id="3ee9b-189">UPN 형식을 사용하여 자격 증명을 지정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-189">Try using the UPN format to specify credentials.</span></span> <span data-ttu-id="3ee9b-190">테넌트에서 여러 사용자가 동일한 UPN 접두사를 사용하거나 UPN 접두사가 지나치게 긴 경우 사용자 계정에 대한 SAMAccountName이 자동으로 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-190">The SAMAccountName for your account may be auto-generated if there are multiple users with the same UPN prefix in your tenant or if your UPN prefix is overly long.</span></span> <span data-ttu-id="3ee9b-191">따라서 사용자 계정에 대한 SAMAccountName 형식은 온-프레미스 도메인에서 사용하거나 예상하는 것과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-191">Therefore, the SAMAccountName format for your account may be different from what you expect or use in your on-premises domain.</span></span>
* <span data-ttu-id="3ee9b-192">'AAD DC 관리자' 그룹에 속한 사용자 계정의 자격 증명을 사용하여 컴퓨터를 관리되는 도메인에 가입해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-192">Try to use the credentials of a user account that belongs to the 'AAD DC Administrators' group to join machines to the managed domain.</span></span>
* <span data-ttu-id="3ee9b-193">시작 가이드에 설명된 단계에 따라 [암호 동기화를 사용하도록 설정](active-directory-ds-getting-started-password-sync.md) 했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-193">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with the steps outlined in the Getting Started guide.</span></span>
* <span data-ttu-id="3ee9b-194">로그인하려면 Azure AD에 구성된 대로 사용자의 UPN(예: 'bob@domainservicespreview.onmicrosoft.com')을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-194">Ensure that you use the UPN of the user as configured in Azure AD (for example, 'bob@domainservicespreview.onmicrosoft.com') to sign in.</span></span>
* <span data-ttu-id="3ee9b-195">시작 가이드에 지정된 대로 암호 동기화가 완료될 때까지 충분히 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ee9b-195">Ensure that you have waited long enough for password synchronization to complete as specified in the Getting Started guide.</span></span>

## <a name="related-content"></a><span data-ttu-id="3ee9b-196">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="3ee9b-196">Related Content</span></span>
* [<span data-ttu-id="3ee9b-197">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="3ee9b-197">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="3ee9b-198">Azure AD 도메인 서비스 관리되는 도메인 관리</span><span class="sxs-lookup"><span data-stu-id="3ee9b-198">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
