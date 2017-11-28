---
title: "빠른 시작-aaaAzure Windows VM 만듭니다 포털 | Microsoft Docs"
description: "Azure 빠른 시작 - Windows VM 만들기 포털"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="b496e-103">Azure 포털 hello로 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="b496e-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="b496e-104">Hello Azure 포털을 통해 azure 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="b496e-105">이 메서드는 가상 컴퓨터 및 관련된 모든 리소스를 만들고 구성하기 위한 브라우저 기반 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="b496e-106">이 퀵 스타트 단계별로 실행 가상 컴퓨터를 만들고 hello VM에서 웹 서버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="b496e-107">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="b496e-108">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="b496e-108">Log in tooAzure</span></span>

<span data-ttu-id="b496e-109">Azure 포털에서 http://portal.azure.com toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="b496e-110">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="b496e-110">Create virtual machine</span></span>

1. <span data-ttu-id="b496e-111">Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="b496e-112">**계산**을 선택한 후 **Windows Server 2016 Datacenter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="b496e-113">Hello 가상 컴퓨터 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="b496e-114">hello 사용자 이름 및 암호를 여기에 입력 된 toohello 가상 컴퓨터에서 사용 되는 toolog입니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="b496e-115">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-115">When complete, click **OK**.</span></span>

    ![Hello 포털 블레이드에서 VM에 대 한 기본 정보를 입력 합니다.](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="b496e-117">Hello VM에 대 한 크기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-117">Select a size for hello VM.</span></span> <span data-ttu-id="b496e-118">toosee 자세한 크기 선택 **모든 보기** hello 변경 또는 **지원 되는 디스크 형식을** 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![VM 크기를 보여 주는 스크린샷](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="b496e-120">Hello 설정 블레이드에서 hello 기본값을 유지 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="b496e-121">Hello 요약 페이지에서 클릭 **확인** toostart hello 가상 컴퓨터에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="b496e-122">hello VM에 Azure 포털 대시보드에서 고정 된 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="b496e-123">Hello 배포 완료 되 면 hello VM 요약 블레이드 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="b496e-124">Toovirtual 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="b496e-124">Connect toovirtual machine</span></span>

<span data-ttu-id="b496e-125">원격 데스크톱 연결 toohello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="b496e-126">Hello 클릭 **연결** hello 가상 컴퓨터 속성에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="b496e-127">원격 데스크톱 프로토콜 파일(.rdp 파일)이 생성되고 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![포털 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="b496e-129">VM을 열고 hello tooconnect tooyour RDP 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="b496e-130">메시지가 표시되면 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="b496e-131">Mac에서 이와 같은 RDP 클라이언트가 필요한 [원격 데스크톱 클라이언트](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) hello Mac 앱 스토어에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="b496e-132">Hello 사용자 이름 및 hello 가상 컴퓨터를 만들 때 지정한 암호를 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="b496e-133">Hello 로그인 프로세스 중 인증서 경고가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="b496e-134">클릭 **예** 또는 **계속** tooproceed hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="b496e-135">PowerShell을 사용하여 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="b496e-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="b496e-136">Hello 가상 컴퓨터에서 PowerShell 세션을 시작 하 고 hello 다음 명령 tooinstall IIS를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="b496e-137">을 완료 한 후 hello RDP 세션을 종료 하 고 hello Azure 포털에서에서 hello VM 속성을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="b496e-138">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="b496e-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="b496e-139">NSG(네트워크 보안 그룹)는 인바운드 및 아웃바운드 트래픽의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="b496e-140">VM hello Azure 포털에서에서 만들어지면는 인바운드 규칙 RDP 연결에 대 한 포트 3389에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="b496e-141">이 VM에서 웹 서버를 호스트 하기 때문에 포트 80에 대해 만든 toobe NSG 규칙에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="b496e-142">Hello 가상 컴퓨터의 hello hello 이름을 클릭 **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="b496e-143">선택 hello **네트워크 보안 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-143">Select hello **network security group**.</span></span> <span data-ttu-id="b496e-144">hello NSG를 식별할 수 있습니다 hello를 사용 하 여 **형식** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="b496e-145">설정에서 hello 왼쪽 메뉴에서 클릭 **인바운드 보안 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="b496e-146">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-146">Click on **Add**.</span></span>
5. <span data-ttu-id="b496e-147">**이름**에서 **http**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-147">In **Name**, type **http**.</span></span> <span data-ttu-id="b496e-148">있는지 확인 **포트 범위가** too80 설정 및 **동작** 너무 설정**허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="b496e-149">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="b496e-150">보기 hello IIS 시작 페이지</span><span class="sxs-lookup"><span data-stu-id="b496e-150">View hello IIS welcome page</span></span>

<span data-ttu-id="b496e-151">IIS를 설치 하 고 포트 80 엽니다 tooyour VM hello 웹 서버 hello에서 액세스할 수 있습니다, 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="b496e-152">웹 브라우저를 열고 hello hello VM의 공용 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="b496e-153">hello Azure 포털에서에서 VM 블레이드의 hello hello 공용 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![IIS 기본 사이트](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="b496e-155">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="b496e-155">Clean up resources</span></span>

<span data-ttu-id="b496e-156">더 이상 필요 hello 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="b496e-157">toodo 따라서 hello 가상 컴퓨터 블레이드에서 hello 리소스 그룹을 선택 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b496e-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b496e-158">Next steps</span></span>

<span data-ttu-id="b496e-159">이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="b496e-160">Azure 가상 컴퓨터에 대해 자세히 toolearn Windows vm의 toohello 자습서를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b496e-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b496e-161">Azure Windows 가상 컴퓨터 자습서</span><span class="sxs-lookup"><span data-stu-id="b496e-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
