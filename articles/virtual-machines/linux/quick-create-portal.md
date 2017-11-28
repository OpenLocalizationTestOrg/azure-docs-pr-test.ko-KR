---
title: "빠른 시작-aaaAzure VM 만듭니다 포털 | Microsoft Docs"
description: "Azure 빠른 시작 - VM 만들기 포털"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="61289-103">Azure 포털 hello로 Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="61289-103">Create a Linux virtual machine with hello Azure portal</span></span>

<span data-ttu-id="61289-104">Hello Azure 포털을 통해 azure 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61289-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="61289-105">이 메서드는 가상 컴퓨터 및 관련된 모든 리소스를 만들고 구성하기 위한 브라우저 기반 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="61289-106">이 퀵 스타트 단계별로 실행 가상 컴퓨터를 만들고 hello VM에서 웹 서버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="61289-107">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61289-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="61289-108">SSH 키 쌍 만들기</span><span class="sxs-lookup"><span data-stu-id="61289-108">Create SSH key pair</span></span>

<span data-ttu-id="61289-109">SSH 키 쌍 toocomplete이 빠른 시작을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-109">You need an SSH key pair toocomplete this quick start.</span></span> <span data-ttu-id="61289-110">기존 SSH 키 쌍을 사용하는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61289-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="61289-111">Bash 셸의에서이 명령을 실행 하 고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-111">From a Bash shell, run this command and follow hello on-screen directions.</span></span> <span data-ttu-id="61289-112">hello 명령 출력에는 hello 공개 키 파일의 hello 파일 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-112">hello command output includes hello file name of hello public key file.</span></span> <span data-ttu-id="61289-113">Hello 공개 키 파일 toohello 클립보드의 hello 내용을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-113">Copy hello contents of hello public key file toohello clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a><span data-ttu-id="61289-114">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="61289-114">Log in tooAzure</span></span> 

<span data-ttu-id="61289-115">Azure 포털에서 http://portal.azure.com toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-115">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="61289-116">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="61289-116">Create virtual machine</span></span>

1. <span data-ttu-id="61289-117">Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61289-117">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="61289-118">**계산**을 선택한 후 **Ubuntu Server 16.04 LTS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="61289-119">Hello 가상 컴퓨터 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-119">Enter hello virtual machine information.</span></span> <span data-ttu-id="61289-120">**인증 유형**으로 **SSH 공용 키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="61289-121">SSH 공개 키를 붙여 넣는 경우 주의 tooremove 모든 선행 또는 후행 공백은 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-121">When pasting in your SSH public key, take care tooremove any leading or trailing white space.</span></span> <span data-ttu-id="61289-122">완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-122">When complete, click **OK**.</span></span>

    ![Hello 포털 블레이드에서 VM에 대 한 기본 정보를 입력 합니다.](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="61289-124">Hello VM에 대 한 크기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-124">Select a size for hello VM.</span></span> <span data-ttu-id="61289-125">toosee 자세한 크기 선택 **모든 보기** hello 변경 또는 **지원 되는 디스크 형식을** 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="61289-125">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![VM 크기를 보여 주는 스크린샷](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="61289-127">Hello 설정 블레이드에서 hello 기본값을 유지 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-127">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="61289-128">Hello 요약 페이지에서 클릭 **확인** toostart hello 가상 컴퓨터에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-128">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="61289-129">hello VM에 Azure 포털 대시보드에서 고정 된 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61289-129">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="61289-130">Hello 배포 완료 되 면 hello VM 요약 블레이드 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="61289-130">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="61289-131">Toovirtual 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="61289-131">Connect toovirtual machine</span></span>

<span data-ttu-id="61289-132">Hello 가상 컴퓨터와 SSH 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="61289-132">Create an SSH connection with hello virtual machine.</span></span>

1. <span data-ttu-id="61289-133">Hello 클릭 **연결** hello 가상 컴퓨터 블레이드 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="61289-133">Click hello **Connect** button on hello virtual machine blade.</span></span> <span data-ttu-id="61289-134">hello 단추 표시 사용된 tooconnect toohello 가상 컴퓨터 일 수 있는 한 SSH 연결 문자열을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-134">hello connect button displays an SSH connection string that can be used tooconnect toohello virtual machine.</span></span>

    ![포털 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="61289-136">실행된 hello 다음 명령은 toocreate SSH 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="61289-136">Run hello following command toocreate an SSH session.</span></span> <span data-ttu-id="61289-137">Hello Azure 포털에서에서 복사 하는 hello로 hello 연결 문자열을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-137">Replace hello connection string with hello one you copied from hello Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="61289-138">NGINX 설치</span><span class="sxs-lookup"><span data-stu-id="61289-138">Install NGINX</span></span>

<span data-ttu-id="61289-139">사용 하 여 hello 다음 스크립트 tooupdate 패키지 소스를 이용한 적 하 고 hello 최신 NGINX 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="61289-140">을 완료 한 후 hello SSH 세션을 종료 하 고 hello Azure 포털에서에서 hello VM 속성을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-140">When done, exit hello SSH session and return hello VM properties in hello Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="61289-141">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="61289-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="61289-142">NSG(네트워크 보안 그룹)는 인바운드 및 아웃바운드 트래픽의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="61289-143">VM hello Azure 포털에서에서 만들어지면는 인바운드 규칙 SSH 연결에 대 한 포트 22에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="61289-143">When a VM is created from hello Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="61289-144">이 VM에서 웹 서버를 호스트 하기 때문에 포트 80에 대해 만든 toobe NSG 규칙에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-144">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="61289-145">Hello 가상 컴퓨터의 hello hello 이름을 클릭 **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-145">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="61289-146">선택 hello **네트워크 보안 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-146">Select hello **network security group**.</span></span> <span data-ttu-id="61289-147">hello NSG를 식별할 수 있습니다 hello를 사용 하 여 **형식** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="61289-147">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="61289-148">설정에서 hello 왼쪽 메뉴에서 클릭 **인바운드 보안 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-148">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="61289-149">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-149">Click on **Add**.</span></span>
5. <span data-ttu-id="61289-150">**이름**에서 **http**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-150">In **Name**, type **http**.</span></span> <span data-ttu-id="61289-151">있는지 확인 **포트 범위가** too80 설정 및 **동작** 너무 설정**허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-151">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="61289-152">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-152">Click **OK**.</span></span>


## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="61289-153">Hello NGINX 시작 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="61289-153">View hello NGINX welcome page</span></span>

<span data-ttu-id="61289-154">Hello 웹 서버 hello에서 액세스할 수 있습니다, NGINX 설치 되어 있으며 포트 80 엽니다 tooyour VM 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-154">With NGINX installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="61289-155">웹 브라우저를 열고 hello hello VM의 공용 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-155">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="61289-156">hello Azure 포털에서에서 VM 블레이드의 hello hello 공용 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61289-156">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![NGINX 기본 사이트](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="61289-158">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="61289-158">Clean up resources</span></span>

<span data-ttu-id="61289-159">더 이상 필요 hello 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-159">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="61289-160">toodo 따라서 hello 가상 컴퓨터 블레이드에서 hello 리소스 그룹을 선택 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-160">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61289-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="61289-161">Next steps</span></span>

<span data-ttu-id="61289-162">이 빠른 시작에서 간단한 가상 컴퓨터, 네트워크 보안 그룹 규칙을 배포했으며 웹 서버를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="61289-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="61289-163">Azure 가상 컴퓨터에 대해 자세히 toolearn Linux Vm에 대 한 toohello 자습서를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="61289-163">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61289-164">Azure Linux 가상 컴퓨터 자습서</span><span class="sxs-lookup"><span data-stu-id="61289-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
