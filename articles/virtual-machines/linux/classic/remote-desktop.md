---
title: "Linux VM에 대한 원격 데스크톱 | Microsoft Docs"
description: "원격 데스크톱을 설치 및 구성하여 클래식 배포 모델을 위한 Microsoft Azure Linux VM에 연결하는 방법을 알아봅니다."
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
ms.openlocfilehash: 68031d548bdbeda9a83d1bceaaea7c5bbcab3188
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-remote-desktop-to-connect-to-a-microsoft-azure-linux-vm"></a><span data-ttu-id="8834e-103">원격 데스크톱을 사용하여 Microsoft Azure Linux VM에 연결</span><span class="sxs-lookup"><span data-stu-id="8834e-103">Using Remote Desktop to connect to a Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="8834e-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8834e-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8834e-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8834e-107">이 문서의 업데이트된 리소스 관리자 버전은 [여기](../use-remote-desktop.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8834e-107">For the updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="8834e-108">개요</span><span class="sxs-lookup"><span data-stu-id="8834e-108">Overview</span></span>
<span data-ttu-id="8834e-109">RDP(원격 데스크톱 프로토콜)는 Windows에 사용되는 독점 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="8834e-110">어떻게 RDP를 사용하여 Linux VM에 원격으로 연결할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="8834e-110">How can we use RDP to connect to a Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="8834e-111">이 설명서에서 답을 줍니다!</span><span class="sxs-lookup"><span data-stu-id="8834e-111">This guidance will give you the answer!</span></span> <span data-ttu-id="8834e-112">Microsoft Azure Linux VM에 xrdp를 설치 및 구성하는 데 도움이 되며, Windows 컴퓨터에서 원격 데스크톱을 사용하여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-112">It will help you to install and config xrdp on your Microsoft Azure Linux VM, which lets you connect to it with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="8834e-113">이 지침에서는 Ubuntu 또는 OpenSUSE를 실행하는 Linux VM을 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-113">We will use Linux VM running Ubuntu or OpenSUSE as the example in this guidance.</span></span>

<span data-ttu-id="8834e-114">xrdp 도구는 Windows 컴퓨터에서 원격 데스크톱으로 Linux 서버에 연결할 수 있도록 해주는 오픈 소스 RDP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-114">The xrdp tool is an open source RDP server that allows you to connect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="8834e-115">RDP는 VNC(Virtual Network Computing)보다 더 강력한 성능을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="8834e-116">RDP는 빠르고 선명한 반면 VNC는 JPEG 수준의 그래픽을 사용하여 렌더링하며 속도가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="8834e-117">Linux를 실행하는 Microsoft Azure VM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="8834e-118">Linux VM을 만들고 설정하려면 [Azure Linux VM 자습서](createportal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8834e-118">To create and set up a Linux VM, see the [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="8834e-119">원격 데스크톱에 대한 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="8834e-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="8834e-120">이 문서에서는 원격 데스크톱에 대해 기본 끝점 3389를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-120">We will use the default endpoint 3389 for Remote Desktop in this doc.</span></span> <span data-ttu-id="8834e-121">아래와 같은 Linux VM에 `Remote Desktop`으로 3389 끝점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-121">Set up 3389 endpoint as `Remote Desktop` to your Linux VM like below:</span></span>

![이미지](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="8834e-123">VM에 대한 끝점을 설정하는 방법을 모르는 경우 [이 지침](setup-endpoints.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8834e-123">If you don't know how to set up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="8834e-124">Gnome 데스크톱 설치</span><span class="sxs-lookup"><span data-stu-id="8834e-124">Install Gnome Desktop</span></span>
<span data-ttu-id="8834e-125">`putty`를 통해 Linux VM에 연결하고 `Gnome Desktop`을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-125">Connect to your Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="8834e-126">Ubuntu의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-126">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="8834e-127">OpenSUSE의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-127">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="8834e-128">xrdp 설치</span><span class="sxs-lookup"><span data-stu-id="8834e-128">Install xrdp</span></span>
<span data-ttu-id="8834e-129">Ubuntu의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-129">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="8834e-130">OpenSUSE의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-130">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="8834e-131">다음 명령에서 현재 사용하는 버전으로 OpenSUSE 버전을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-131">Update the OpenSUSE version with the version you are using in the following command.</span></span> <span data-ttu-id="8834e-132">아래 예는 `OpenSUSE 13.2`의 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-132">The example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="8834e-133">xrdp를 시작하고 부팅에 xdrp 서비스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-133">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="8834e-134">OpenSUSE의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-134">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="8834e-135">Ubuntu의 경우 설치 후 부팅 시 자동으로 xrdp가 시작되어 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-135">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="8834e-136">Ubuntu 12.04LTS보다 높은 Ubuntu 버전을 사용하는 경우 xfce를 사용</span><span class="sxs-lookup"><span data-stu-id="8834e-136">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="8834e-137">현재 xrdp 버전은 Ubuntu 12.04LTS보다 높은 Ubuntu 버전에 대해 Gnome 데스크톱을 지원하지 않으므로 대신 `xfce` 데스크톱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-137">Because the current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="8834e-138">`xfce`를 설치하려면 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-138">To install `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="8834e-139">그런 다음 이 명령을 사용하여 `xfce`를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-139">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="8834e-140">구성 파일 `/etc/xrdp/startwm.sh`를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-140">Edit the config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="8834e-141">`/etc/X11/Xsession` 줄 앞에 `xfce4-session` 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-141">Add the line `xfce4-session` before the line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="8834e-142">xrdp 서비스를 다시 시작하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-142">To restart the xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="8834e-143">Windows 컴퓨터에서 Linux VM 연결</span><span class="sxs-lookup"><span data-stu-id="8834e-143">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="8834e-144">Windows 컴퓨터에서 원격 데스크톱 클라이언트를 시작하고 Linux VM DNS 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-144">In a Windows machine, start the Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="8834e-145">또는 Azure Portal에서 VM의 대시보드로 이동하고 `Connect`를 클릭하여 Linux VM을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-145">Or go to the Dashboard of your VM in the Azure portal and click `Connect` to connect your Linux VM.</span></span> <span data-ttu-id="8834e-146">이 경우 로그인 창이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-146">In that case, you see the login window:</span></span>

![이미지](./media/remote-desktop/no2.png)

<span data-ttu-id="8834e-148">Linux VM의 사용자 이름 및 암호로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8834e-148">Log in with the user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8834e-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8834e-149">Next steps</span></span>
<span data-ttu-id="8834e-150">xrdp 사용에 대한 자세한 내용은 [http://www.xrdp.org/](http://www.xrdp.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8834e-150">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
