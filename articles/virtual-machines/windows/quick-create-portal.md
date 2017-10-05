---
title: "Azure 빠른 시작 - Windows VM 만들기 포털 | Microsoft Docs"
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
ms.openlocfilehash: 31ac18add9c3fd956e0d37b1e0c1a510265c22e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="54aab-103">Azure Portal을 사용하여 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="54aab-103">Create a Windows virtual machine with the Azure portal</span></span>

<span data-ttu-id="54aab-104">Azure Portal을 통해 Azure Virtual Machines를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="54aab-105">이 메서드는 가상 컴퓨터 및 관련된 모든 리소스를 만들고 구성하기 위한 브라우저 기반 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="54aab-106">이 빠른 시작은 가상 컴퓨터를 만들고 VM에 웹 서버를 설치하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="54aab-107">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="54aab-108">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="54aab-108">Log in to Azure</span></span>

<span data-ttu-id="54aab-109">Azure Portal( http://portal.azure.com )에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-109">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="54aab-110">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="54aab-110">Create virtual machine</span></span>

1. <span data-ttu-id="54aab-111">Azure Portal의 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-111">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="54aab-112">**계산**을 선택한 후 **Windows Server 2016 Datacenter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="54aab-113">가상 컴퓨터 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-113">Enter the virtual machine information.</span></span> <span data-ttu-id="54aab-114">여기에서 입력한 이사용자 이름과 암호는 가상 컴퓨터에 로그인하는 데 사용됩니다</span><span class="sxs-lookup"><span data-stu-id="54aab-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="54aab-115">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-115">When complete, click **OK**.</span></span>

    ![포털 블레이드에서 VM에 대한 기본 정보 입력](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="54aab-117">VM의 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-117">Select a size for the VM.</span></span> <span data-ttu-id="54aab-118">더 많은 크기를 보려면 **모두 보기**를 선택하거나 **지원되는 디스크 형식** 필터를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-118">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![VM 크기를 보여 주는 스크린샷](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="54aab-120">설정 블레이드에서 기본값을 그대로 유지하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-120">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="54aab-121">요약 페이지에서 **확인**을 클릭하여 가상 컴퓨터 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-121">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="54aab-122">Azure Portal 대시보드에 VM을 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-122">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="54aab-123">배포가 완료되면 VM 요약 블레이드가 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-123">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="54aab-124">가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="54aab-124">Connect to virtual machine</span></span>

<span data-ttu-id="54aab-125">가상 컴퓨터에 대한 원격 데스크톱 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-125">Create a remote desktop connection to the virtual machine.</span></span>

1. <span data-ttu-id="54aab-126">가상 컴퓨터 속성에서 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-126">Click the **Connect** button on the virtual machine properties.</span></span> <span data-ttu-id="54aab-127">원격 데스크톱 프로토콜 파일(.rdp 파일)이 생성되고 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![포털 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="54aab-129">VM에 연결하려면 다운로드한 RDP 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-129">To connect to your VM, open the downloaded RDP file.</span></span> <span data-ttu-id="54aab-130">메시지가 표시되면 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="54aab-131">Mac의 Mac 앱 스토어에서 이 [원격 데스크톱 클라이언트](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12)와 같은 RDP 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from the Mac App Store.</span></span>

3. <span data-ttu-id="54aab-132">가상 컴퓨터를 만들 때 지정한 사용자 이름 및 암호를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-132">Enter the user name and password you specified when creating the virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="54aab-133">로그인 프로세스 중에 인증서 경고가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-133">You may receive a certificate warning during the sign-in process.</span></span> <span data-ttu-id="54aab-134">**예** 또는 **계속**을 클릭하여 연결을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-134">Click **Yes** or **Continue** to proceed with the connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="54aab-135">PowerShell을 사용하여 IIS 설치</span><span class="sxs-lookup"><span data-stu-id="54aab-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="54aab-136">가상 컴퓨터에서 PowerShell 세션을 시작하고 다음 명령을 실행하여 IIS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-136">On the virtual machine, start a PowerShell session and run the following command to install IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="54aab-137">작업이 완료되면 RDP 세션을 종료하고 Azure Portal에서 VM 속성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-137">When done, exit the RDP session and return the VM properties in the Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="54aab-138">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="54aab-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="54aab-139">NSG(네트워크 보안 그룹)는 인바운드 및 아웃바운드 트래픽의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="54aab-140">Azure Portal에서 VM이 만들어지면 RDP 연결의 포트 3389에서 인바운드 규칙이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-140">When a VM is created from the Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="54aab-141">이 VM이 웹 서버를 호스트하기 때문에 포트 80에 NSG 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-141">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="54aab-142">가상 컴퓨터에서 **리소스 그룹**의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-142">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="54aab-143">**네트워크 보안 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-143">Select the **network security group**.</span></span> <span data-ttu-id="54aab-144">NSG는 **형식** 열을 사용하여 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-144">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="54aab-145">왼쪽 메뉴의 설정에서 **인바운드 보안 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-145">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="54aab-146">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-146">Click on **Add**.</span></span>
5. <span data-ttu-id="54aab-147">**이름**에서 **http**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-147">In **Name**, type **http**.</span></span> <span data-ttu-id="54aab-148">**포트 범위**를 80으로 설정하고 **작업**을 **허용**으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-148">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="54aab-149">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-149">Click **OK**.</span></span>


## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="54aab-150">IIS 시작 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="54aab-150">View the IIS welcome page</span></span>

<span data-ttu-id="54aab-151">IIS를 설치하고 VM에 포트 80을 열어서 인터넷에서 웹 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-151">With IIS installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="54aab-152">웹 브라우저를 열고 VM의 공용 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-152">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="54aab-153">공용 IP 주소는 Azure Portal에서 VM 블레이드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-153">the public IP address can be found on the VM blade in the Azure portal.</span></span>

![IIS 기본 사이트](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="54aab-155">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="54aab-155">Clean up resources</span></span>

<span data-ttu-id="54aab-156">더 이상 필요하지 않을 때 리소스 그룹, 가상 컴퓨터 및 모든 관련 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-156">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="54aab-157">이렇게 하려면 가상 컴퓨터 블레이드에서 해당 리소스 그룹을 선택하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-157">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54aab-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54aab-158">Next steps</span></span>

<span data-ttu-id="54aab-159">이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="54aab-160">Azure 가상 컴퓨터에 대한 자세한 내용을 알아보려면 Windows VM의 자습서를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="54aab-160">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="54aab-161">Azure Windows 가상 컴퓨터 자습서</span><span class="sxs-lookup"><span data-stu-id="54aab-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
