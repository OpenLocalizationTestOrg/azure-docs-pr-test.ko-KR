---
title: "첫 번째 Windows VM에 IIS 설치 | Microsoft Docs"
description: "Azure 포털을 사용하여 IIS를 설치하고 포트 80을 열어 첫 번째 Windows 가상 컴퓨터로 실험합니다."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: b11ce1eab0c26a802c31bc418cdf725cbc4fba30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="ef153-103">Windows VM에서 역할을 설치하여 실험</span><span class="sxs-lookup"><span data-stu-id="ef153-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="ef153-104">첫 번째 VM(가상 컴퓨터)이 작동 및 실행되는 경우 소프트웨어 및 서비스 설치를 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="ef153-105">이 자습서에서는 Windows Server VM의 서버 관리자를 사용하여 IIS를 설치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="ef153-106">그런 다음 Azure 포털을 사용하여 NSG(네트워크 보안 그룹)를 만들고 IIS 트래픽에 대해 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="ef153-107">첫 번째 VM을 아직 만들지 않은 경우 이 자습서를 계속 진행하기 전에 [Azure Portal에서 첫 번째 Windows 가상 컴퓨터 만들기](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)로 되돌아가야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="ef153-108">VM이 실행되고 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="ef153-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="ef153-109">[Azure 포털](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ef153-110">허브 메뉴에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="ef153-111">목록에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="ef153-112">상태가 **중지됨(할당 취소됨)**이면 VM의 **Essentials** 블레이드에서 **시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="ef153-113">상태가 **실행 중**이면 다음 단계로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="ef153-114">가상 컴퓨터에 연결 및 로그인</span><span class="sxs-lookup"><span data-stu-id="ef153-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="ef153-115">허브 메뉴에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="ef153-116">목록에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="ef153-117">가상 컴퓨터 블레이드에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="ef153-118">컴퓨터에 연결하는 바로 가기와 같은 원격 데스크톱 프로토콜 파일(.rdp 파일)을 만들고 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="ef153-119">쉽게 액세스할 수 있도록 바탕 화면에 파일을 저장 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="ef153-120">**열어서** VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-120">**Open** this file to connect to your VM.</span></span>
   
    ![VM에 연결하는 방법을 보여 주는 Azure Portal의 스크린샷](./media/hero-role/connect.png)
3. <span data-ttu-id="ef153-122">.rdp이 알 수 없는 게시자에게서 비롯되었다는 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="ef153-123">이것은 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-123">This is normal.</span></span> <span data-ttu-id="ef153-124">원격 데스크톱 창에서 **연결** 을 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![알 수 없는 게시자에 대한 경고 스크린샷](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="ef153-126">Windows 보안 창에서 VM을 만들 때 생성한 로컬 계정에 대한 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="ef153-127">사용자 이름을 *vmname*&#92;*사용자 이름*으로 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![VM 이름, 사용자 이름 및 암호를 입력하는 스크린샷](./media/hero-role/credentials.png)
5. <span data-ttu-id="ef153-129">인증서를 확인할 수 없다는 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="ef153-130">이것은 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-130">This is normal.</span></span> <span data-ttu-id="ef153-131">**예** 를 클릭하여 가상 컴퓨터의 ID를 확인하고 로그온을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![VM의 ID를 확인하라는 메시지를 보여 주는 스크린샷](./media/hero-role/cert-warning.png)

<span data-ttu-id="ef153-133">연결하려고 할 때 문제가 발생할 경우 [Windows 기반 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef153-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="ef153-134">VM에 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="ef153-134">Install IIS on your VM</span></span>
<span data-ttu-id="ef153-135">VM에 로그인했으므로 더 실험할 수 있도록 서버 역할을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="ef153-136">아직 열려 있지 않은 경우 **서버 관리자** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="ef153-137">**시작** 메뉴를 클릭한 다음 **서버 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="ef153-138">**서버 관리자**의 왼쪽 창에서 **로컬 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="ef153-139">메뉴에서 **관리** > **역할 및 기능 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="ef153-140">역할 및 기능 추가 마법사의 **설치 유형** 페이지에서 **역할 기반 또는 기능 기반 설치**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![설치 유형에 대한 역할 및 기능 마법사 추가 탭을 보여 주는 스크린샷](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="ef153-142">서버 풀에서 VM을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="ef153-143">**서버 역할** 페이지에서 **Web Server(IIS)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![서버 유형에 대한 역할 및 기능 마법사 추가 탭을 보여 주는 스크린샷](./media/hero-role/add-iis.png)
7. <span data-ttu-id="ef153-145">IIS에 필요한 기능을 추가에 대한 팝업에서 **관리 도구 포함**을 선택했는 지 확인한 다음 **기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="ef153-146">팝업을 닫을 때 마법사에서 **다음** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![IIS 역할을 추가하여 확인할 팝업을 보여 주는 스크린샷](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="ef153-148">기능 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="ef153-149">**웹 서버 역할(IIS)** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="ef153-150">**역할 서비스** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="ef153-151">**확인** 페이지에서 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="ef153-152">설치가 완료되면 마법사에서 **닫기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="ef153-153">포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="ef153-153">Open port 80</span></span>
<span data-ttu-id="ef153-154">VM이 포트 80을 통한 인바운드 트래픽을 허용하기 위해 네트워크 보안 그룹에 인바운드 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="ef153-155">[Azure 포털](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ef153-156">**가상 컴퓨터** 에서 만든 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="ef153-157">가상 컴퓨터 설정에서 **네트워크 인터페이스** 를 선택한 다음 기존 네트워크 인터페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![네트워크 인터페이스에 대한 가상 컴퓨터 설정을 보여 주는 스크린샷](./media/hero-role/network-interface.png)
4. <span data-ttu-id="ef153-159">네트워크 인터페이스에 대한 **Essentials**에서 **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![네트워크 인터페이스에 대한 Essentials 섹션을 보여 주는 스크린샷](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="ef153-161">NSG에 대한 **Essentials** 블레이드에서 VM에 로그인할 수 있는 **default-allow-rdp**에 하나의 기존 기본 인바운드 규칙이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="ef153-162">IIS 트래픽을 허용하도록 인바운드 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="ef153-163">**인바운드 보안 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-163">Click **Inbound security rule**.</span></span>
   
    ![NSG에 대한 Essentials 섹션을 보여 주는 스크린샷](./media/hero-role/inbound.png)
6. <span data-ttu-id="ef153-165">**인바운드 보안 규칙**에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![보안 규칙을 추가하는 단추를 보여 주는 스크린샷](./media/hero-role/add-rule.png)
7. <span data-ttu-id="ef153-167">**인바운드 보안 규칙**에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="ef153-168">포트 범위에 **80**을 입력하고 **허용**을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="ef153-169">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-169">When you are done, click **OK**.</span></span>
   
    ![보안 규칙을 추가하는 단추를 보여 주는 스크린샷](./media/hero-role/port-80.png)

<span data-ttu-id="ef153-171">NSG, 인바운드 및 아웃바운드 규칙에 대한 자세한 내용은 [Azure Portal을 사용하여 VM에 대한 외부 액세스 허용](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef153-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="ef153-172">기본 IIS 웹 사이트에 연결</span><span class="sxs-lookup"><span data-stu-id="ef153-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="ef153-173">Azure 포털에서 **가상 컴퓨터** 를 클릭한 다음 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="ef153-174">**Essentials** 블레이드에서 **공용 IP 주소**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![VM의 공용 IP 주소를 찾을 수 있는 위치를 보여 주는 스크린샷](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="ef153-176">브라우저를 열고 주소 표시줄에 http://<publicIPaddress>와 같은 공용 IP 주소를 입력하고 **입력**을 클릭하여 해당 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="ef153-177">브라우저에서 기본 IIS 웹 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="ef153-178">모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-178">It looks something like this:</span></span>
   
    ![브라우저에서 기본 IIS 페이지 모양을 보여 주는 스크린샷](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="ef153-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef153-180">Next steps</span></span>
* <span data-ttu-id="ef153-181">또한 가상 컴퓨터에 대한 [데이터 디스크 연결](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 실험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="ef153-182">데이터 디스크는 가상 컴퓨터에 대한 더 많은 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef153-182">Data disks provide more storage for your virtual machine.</span></span>

