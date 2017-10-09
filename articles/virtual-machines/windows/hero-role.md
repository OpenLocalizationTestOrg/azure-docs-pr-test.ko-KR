---
title: "첫 번째 Windows VM에는 IIS aaaInstall | Microsoft Docs"
description: "첫 번째 시험해 IIS를 설치 하 고 포트 80을 사용 하 여 Windows 가상 컴퓨터는 Azure 포털 hello 합니다."
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
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="0369c-103">Windows VM에서 역할을 설치하여 실험</span><span class="sxs-lookup"><span data-stu-id="0369c-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="0369c-104">첫 번째 가상 컴퓨터 (VM)를 구성 및 실행 되 고 있으면 tooinstalling 소프트웨어 및 서비스에서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="0369c-105">이 자습서에서는 하겠습니다 toouse 서버 관리자에서 Windows Server VM tooinstall hello IIS 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="0369c-106">그런 다음 네트워크 보안 그룹 (NSG) hello Azure 포털 tooopen 포트 80 tooIIS 트래픽을 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="0369c-107">첫 번째 VM을 아직 만들지 않은 경우 해야 다시가 서 너무[hello Azure 포털에서에서 첫 번째 Windows 가상 컴퓨터를 만들](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 이 자습서를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="0369c-108">VM이 실행 되 고 있는지 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="0369c-109">열기 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0369c-110">Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="0369c-111">Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="0369c-112">Hello 상태가 **중지 (할당 취소)**, hello 클릭 **시작** hello 단추 **Essentials** hello VM의 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="0369c-113">Hello 상태가 **실행**, toohello 다음 단계로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="0369c-114">Toohello 가상 컴퓨터에 연결 하 고 로그인</span><span class="sxs-lookup"><span data-stu-id="0369c-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="0369c-115">Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="0369c-116">Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="0369c-117">Hello 가상 컴퓨터에 대 한 hello 블레이드에서 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="0369c-118">그러면 만들어지고 바로 가기 tooconnect tooyour 컴퓨터과 같은 원격 데스크톱 프로토콜 파일 (.rdp 파일)을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="0369c-119">Toosave hello 파일 tooyour 데스크톱 편리 하 게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="0369c-120">**열기** 파일 tooconnect tooyour VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Hello Azure 포털 보여 주는 스크린샷 어떻게 tooconnect tooyour VM](./media/hero-role/connect.png)
3. <span data-ttu-id="0369c-122">경고가 나타나면 해당 hello.rdp 알 수 없는 게시자에서 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="0369c-123">이것은 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-123">This is normal.</span></span> <span data-ttu-id="0369c-124">Hello 원격 데스크톱 창에서 클릭 **연결** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![알 수 없는 게시자에 대한 경고 스크린샷](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="0369c-126">Hello Windows 보안 창 형식 hello 사용자 이름 및 암호를 만들 때 만든 hello 로컬 계정에 대 한 VM을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="0369c-127">hello 사용자 이름을으로 입력 됩니다 *vmname*&#92; *사용자 이름*, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Hello VM 이름, 사용자 이름 및 암호를 입력 하는 스크린 샷](./media/hero-role/credentials.png)
5. <span data-ttu-id="0369c-129">경고가 나타나면 해당 hello 인증서를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="0369c-130">이것은 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-130">This is normal.</span></span> <span data-ttu-id="0369c-131">클릭 **예** tooverify hello 가상 컴퓨터의 id를 hello 및 로그온을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![메시지를 보여 주는 스크린샷 hello VM의 hello id를 확인 한 섹션인](./media/hero-role/cert-warning.png)

<span data-ttu-id="0369c-133">Tooconnect 려 할 때 tootrouble에서 실행 하면 참조 [Windows 기반 Azure 가상 컴퓨터 문제를 해결 하는 원격 데스크톱 연결 tooa](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="0369c-134">VM에 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="0369c-134">Install IIS on your VM</span></span>
<span data-ttu-id="0369c-135">Toohello VM에에서 로그인 해야 했으므로 더 작업할 수 있도록 서버 역할을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="0369c-136">아직 열려 있지 않은 경우 **서버 관리자** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="0369c-137">Hello 클릭 **시작** 메뉴를 차례로 클릭 **서버 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="0369c-138">**서버 관리자**선택, **로컬 서버** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="0369c-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="0369c-139">Hello 메뉴에서 선택 **관리** > **역할 및 기능 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="0369c-140">Hello 추가 역할 및 기능 마법사 hello **설치 유형을** 페이지에서 선택 **역할 기반 또는 기능 기반 설치**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![스크린 샷 보여 주는 hello 추가 역할 및 기능 마법사에 대 한 탭 설치 유형](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="0369c-142">Hello 서버 풀의 hello VM을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="0369c-143">Hello에 **서버 역할** 페이지에서 **웹 서버 (IIS)**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![스크린 샷 보여 주는 hello 추가 역할 및 기능 마법사에 대 한 탭 서버 역할](./media/hero-role/add-iis.png)
7. <span data-ttu-id="0369c-145">IIS에 필요한 기능을 추가 하는 방법에 대 한 팝업 hello, 되는지 확인 **관리 도구 포함** 을 선택 하 고 클릭 **기능 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="0369c-146">클릭 하 여 hello 팝업을 닫으면 **다음** hello 마법사에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Hello IIS 역할을 추가 하는 팝업 tooconfirm 보여 주는 스크린샷](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="0369c-148">Hello 기능 페이지에서 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="0369c-149">Hello에 **웹 서버 역할 (IIS)** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="0369c-150">Hello에 **역할 서비스** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="0369c-151">Hello에 **확인** 페이지 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="0369c-152">Hello 설치가 완료 되 면 클릭 **닫기** hello 마법사에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="0369c-153">포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="0369c-153">Open port 80</span></span>
<span data-ttu-id="0369c-154">VM tooaccept 위해에서 포트 80 통한 트래픽 인바운드 tooadd는 인바운드 규칙 toohello 네트워크 보안 그룹을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="0369c-155">열기 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0369c-156">**가상 컴퓨터** 선택 hello 만든 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="0369c-157">Hello 가상 컴퓨터 설정에서 선택 **네트워크 인터페이스** 다음 선택 hello 기존 네트워크 인터페이스 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Hello에 대 한 가상 컴퓨터 설정을 hello 네트워크 인터페이스를 보여 주는 스크린샷](./media/hero-role/network-interface.png)
4. <span data-ttu-id="0369c-159">**Essentials** hello 네트워크 인터페이스에 대 한 클릭 hello **네트워크 보안 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Hello 네트워크 인터페이스에 대 한 hello Essentials 섹션을 보여 주는 스크린샷](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="0369c-161">Hello에 **Essentials** NSG hello에 대 한 블레이드에서 있어야 인바운드 규칙에 대 한 하나의 기존 기본 **기본 허용 rdp** 수 있는 toolog toohello VM에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="0369c-162">다른 인바운드 규칙 tooallow IIS 트래픽을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="0369c-163">**인바운드 보안 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-163">Click **Inbound security rule**.</span></span>
   
    ![NSG hello에 대 한 hello Essentials 섹션을 보여 주는 스크린샷](./media/hero-role/inbound.png)
6. <span data-ttu-id="0369c-165">**인바운드 보안 규칙**에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Hello 단추 tooadd 보안 규칙을 보여 주는 스크린샷](./media/hero-role/add-rule.png)
7. <span data-ttu-id="0369c-167">**인바운드 보안 규칙**에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="0369c-168">형식 **80** 에서 포트 범위 hello 하 고 있는지 확인 **허용** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="0369c-169">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-169">When you are done, click **OK**.</span></span>
   
    ![Hello 단추 tooadd 보안 규칙을 보여 주는 스크린샷](./media/hero-role/port-80.png)

<span data-ttu-id="0369c-171">Nsg 인바운드 및 아웃 바운드 규칙에 대 한 자세한 내용은 참조 하십시오. [Azure 포털 hello 허용 외부 tooyour VM 사용 하 여 액세스](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0369c-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="0369c-172">Toohello 기본 IIS 웹 사이트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="0369c-173">Hello Azure 포털에서에서 클릭 **가상 컴퓨터** 한 다음 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="0369c-174">Hello에 **Essentials** 블레이드에서 복사 하면 **공용 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![여기서 toofind hello VM의 공용 IP 주소를 보여 주는 스크린샷](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="0369c-176">브라우저를 열고 hello 주소 표시줄에서 다음과 같은 공용 IP 주소 입력: http://<publicIPaddress> 클릭 **Enter** toogo toothat 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="0369c-177">브라우저가는 hello 기본 IIS 웹 페이지를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="0369c-178">모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-178">It looks something like this:</span></span>
   
    ![브라우저에서 다음과 같은 hello 기본 IIS 페이지에 관계를 보여 주는 스크린샷](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="0369c-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0369c-180">Next steps</span></span>
* <span data-ttu-id="0369c-181">또한 실험할 수 [데이터 디스크 연결](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="0369c-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="0369c-182">데이터 디스크는 가상 컴퓨터에 대한 더 많은 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0369c-182">Data disks provide more storage for your virtual machine.</span></span>

