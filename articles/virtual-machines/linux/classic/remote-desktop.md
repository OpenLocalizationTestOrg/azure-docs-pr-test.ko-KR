---
title: "Linux VM aaaRemote 데스크톱 tooa | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall hello 클래식 배포 모델에 대 한 원격 데스크톱 tooconnect tooa Microsoft Azure Linux VM을 구성 하 고"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="33417-103">원격 데스크톱 tooconnect tooa Microsoft Azure Linux VM을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="33417-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="33417-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33417-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="33417-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="33417-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33417-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="33417-107">이 문서의 버전 리소스 관리자를 업데이트 하는 hello에 대 한 참조 [여기](../use-remote-desktop.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="33417-108">개요</span><span class="sxs-lookup"><span data-stu-id="33417-108">Overview</span></span>
<span data-ttu-id="33417-109">RDP(원격 데스크톱 프로토콜)는 Windows에 사용되는 독점 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="33417-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="33417-110">RDP tooconnect tooa Linux VM (가상 컴퓨터)를 원격으로 사용할 수 어떻게 우리?</span><span class="sxs-lookup"><span data-stu-id="33417-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="33417-111">이 지침은 제공 됩니다 응답 hello!</span><span class="sxs-lookup"><span data-stu-id="33417-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="33417-112">Windows 컴퓨터에서 원격 데스크톱 tooit를 연결할 수 하 여 Microsoft Azure Linux VM에서 tooinstall 및 config xrdp을 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33417-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="33417-113">이 설명서에 hello 예로 Ubuntu 또는 OpenSUSE를 실행 하는 Linux VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="33417-114">hello xrdp 도구는 오픈 소스 RDP 서버 tooconnect 수 있는 Windows 컴퓨터에서 원격 데스크톱을 사용 하 여 Linux 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="33417-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="33417-115">RDP는 VNC(Virtual Network Computing)보다 더 강력한 성능을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="33417-116">RDP는 빠르고 선명한 반면 VNC는 JPEG 수준의 그래픽을 사용하여 렌더링하며 속도가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33417-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="33417-117">Linux를 실행하는 Microsoft Azure VM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="33417-118">toocreate 및 Linux VM 설정을 참조 hello [Azure Linux VM 자습서](createportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="33417-119">원격 데스크톱에 대한 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="33417-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="33417-120">이 문서에서 원격 데스크톱에 대 한 hello 기본 끝점 3389 사용 합니다. 3389 끝점으로 설정 `Remote Desktop` 다음과 유사한 tooyour Linux VM:</span><span class="sxs-lookup"><span data-stu-id="33417-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![이미지](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="33417-122">알 수 없는 경우 tooset VM에 대 한 끝점을 확인 하려면 어떻게 해야 [이 지침은](setup-endpoints.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="33417-123">Gnome 데스크톱 설치</span><span class="sxs-lookup"><span data-stu-id="33417-123">Install Gnome Desktop</span></span>
<span data-ttu-id="33417-124">Tooyour Linux VM에 연결을 통해 `putty`, 설치 및 `Gnome Desktop`합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="33417-125">Ubuntu의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="33417-126">OpenSUSE의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="33417-127">xrdp 설치</span><span class="sxs-lookup"><span data-stu-id="33417-127">Install xrdp</span></span>
<span data-ttu-id="33417-128">Ubuntu의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="33417-129">OpenSUSE의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="33417-130">Hello 다음 명령을 사용 하는 hello 버전으로 hello OpenSUSE 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="33417-131">아래 예제에서는 hello에 대 한는 `OpenSUSE 13.2`합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="33417-132">xrdp를 시작하고 부팅에 xdrp 서비스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="33417-133">OpenSUSE의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="33417-134">Ubuntu의 경우 설치 후 부팅 시 자동으로 xrdp가 시작되어 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="33417-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="33417-135">Ubuntu 12.04LTS보다 높은 Ubuntu 버전을 사용하는 경우 xfce를 사용</span><span class="sxs-lookup"><span data-stu-id="33417-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="33417-136">사용 합니다 hello xrdp의 현재 버전에서 지원 하지 않으므로 Gnome 데스크톱 Ubuntu 버전에 대 한 Ubuntu 12.04LTS 이후, `xfce` 데스크톱 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="33417-137">tooinstall `xfce`,이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="33417-138">그런 다음 이 명령을 사용하여 `xfce`를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="33417-139">Hello 구성 파일 편집 `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="33417-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="33417-140">Hello 줄 추가 `xfce4-session` hello 줄 앞 `/etc/X11/Xsession`합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="33417-141">toorestart xrdp 서비스 hello,이 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="33417-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="33417-142">Windows 컴퓨터에서 Linux VM 연결</span><span class="sxs-lookup"><span data-stu-id="33417-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="33417-143">Windows 컴퓨터에서 원격 데스크톱 클라이언트 hello 시작한 Linux VM의 DNS 이름을 입력 하십시오.</span><span class="sxs-lookup"><span data-stu-id="33417-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="33417-144">또는 toohello hello Azure 포털에서에서 VM의 대시보드를 이동 하 고 클릭 `Connect` tooconnect Linux VM입니다.</span><span class="sxs-lookup"><span data-stu-id="33417-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="33417-145">이 경우 hello 로그인 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33417-145">In that case, you see hello login window:</span></span>

![이미지](./media/remote-desktop/no2.png)

<span data-ttu-id="33417-147">Hello 사용자 이름 및 Linux VM의 암호를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="33417-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33417-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33417-148">Next steps</span></span>
<span data-ttu-id="33417-149">xrdp 사용에 대한 자세한 내용은 [http://www.xrdp.org/](http://www.xrdp.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33417-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
