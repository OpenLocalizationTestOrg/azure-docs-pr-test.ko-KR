---
title: "Azure에서 Linux VM에 대한 원격 데스크톱 사용 | Microsoft Docs"
description: "Azure에서 그래픽 도구를 사용하여 Linux VM에 연결하도록 원격 데스크톱(xrdp)을 설치 및 구성하는 방법 알아보기"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: d8d6130a270285c84c1dd057a3512cdeb39287f6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a><span data-ttu-id="5a506-103">Azure에서 원격 데스크톱을 설치 및 구성하여 Linux VM에 연결</span><span class="sxs-lookup"><span data-stu-id="5a506-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span></span>
<span data-ttu-id="5a506-104">Azure의 Linux VM(가상 컴퓨터)은 SSH(보안 셸) 연결을 사용하여 명령줄에서 일반적으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="5a506-105">Linux를 처음 사용하거나 빠른 문제 해결 시나리오의 경우 원격 데스크톱을 사용하는 편이 더 쉬울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span></span> <span data-ttu-id="5a506-106">이 문서에서는 Resource Manager 배포 모델을 사용하여 Linux VM에 대해 데스크톱 환경([xfce](https://www.xfce.org)) 및 원격 데스크톱([xrdp](http://www.xrdp.org))을 설치하고 구성하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using the Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5a506-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5a506-107">Prerequisites</span></span>
<span data-ttu-id="5a506-108">이 문서에는 Azure의 기존 Linux VM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="5a506-109">VM을 만들어야 하는 경우 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-109">If you need to create a VM, use one of the following methods:</span></span>

- <span data-ttu-id="5a506-110">[Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="5a506-110">The [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="5a506-111">[Azure Portal](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5a506-111">The [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="5a506-112">Linux VM에서 데스크톱 환경 설치</span><span class="sxs-lookup"><span data-stu-id="5a506-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="5a506-113">Azure의 Linux VM은 대부분 데스크톱 환경을 기본적으로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="5a506-114">Linux VM은 일반적으로 데스크톱 환경이 아닌 SSH 연결을 사용하여 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="5a506-115">Linux에서 다양한 데스크톱 환경을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="5a506-116">데스크톱 환경 선택에 따라 1~2GB의 디스크 공간을 사용하고 모든 필수 패키지를 설치 및 구성하는 데 5~10분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-116">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span></span>

<span data-ttu-id="5a506-117">다음 예제에서는 Ubuntu VM에 경량 [xfce4](https://www.xfce.org/) 데스크톱 환경을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="5a506-118">다른 배포에 대한 명령은 약간씩 다릅니다. 예를 들어 `yum`을 사용하여 Red Hat Enterprise Linux에 설치하고 적절한 `selinux` 규칙을 구성하거나 `zypper`를 사용하여 SUSE에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-118">Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).</span></span>

<span data-ttu-id="5a506-119">먼저 VM에 SSH를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-119">First, SSH to your VM.</span></span> <span data-ttu-id="5a506-120">다음 예제에서는 사용자 이름 *azureuser*를 사용하여 *myvm.westus.cloudapp.azure.com*이라는 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-120">The following example connects to the VM named *myvm.westus.cloudapp.azure.com* with the username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="5a506-121">Windows를 사용하고 SSH를 사용하는 방법에 대해 자세히 알아보려면 [Windows에서 SSH 키 사용 방법](ssh-from-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a506-121">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="5a506-122">다음으로 다음과 같이 `apt`를 사용하여 xfce를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="5a506-123">원격 데스크톱 서버 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="5a506-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="5a506-124">데스크톱 환경을 설치했으므로 들어오는 연결을 수신하도록 원격 데스크톱 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-124">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span></span> <span data-ttu-id="5a506-125">[xrdp](http://xrdp.org)는 대부분의 Linux 배포판에서 사용할 수 있는 오픈 소스 RDP(원격 데스크톱 프로토콜) 서버로 xfce와 함께 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="5a506-126">다음과 같이 Ubuntu VM에 xrdp를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="5a506-127">사용자 세션을 시작할 때 사용할 데스크톱 환경을 xrdp에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-127">Tell xrdp what desktop environment to use when you start your session.</span></span> <span data-ttu-id="5a506-128">xfce를 구성하여 다음과 같이 xfce를 데스크톱 환경으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-128">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="5a506-129">다음과 같이 적용되려면 변경을 위해 xrdp 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-129">Restart the xrdp service for the changes to take effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="5a506-130">로컬 사용자 계정 암호 설정</span><span class="sxs-lookup"><span data-stu-id="5a506-130">Set a local user account password</span></span>
<span data-ttu-id="5a506-131">VM을 만들 때 사용자 계정의 암호를 만든 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="5a506-132">SSH 키 인증을 사용하고 로컬 계정 암호를 설정하지 않은 경우 xrdp를 사용하여 VM에 로그인하기 전에 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span></span> <span data-ttu-id="5a506-133">xrdp는 인증을 위해 SSH 키를 수락할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="5a506-134">다음 예제에서는 사용자 계정 *azureuser*의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-134">The following example specifies a password for the user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="5a506-135">암호를 지정하더라도 현재 암호 로그인을 허용하지 않으면 암호 로그인을 허용하도록 SSHD 구성이 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-135">Specifying a password does not update your SSHD configuration to permit password logins if it currently does not.</span></span> <span data-ttu-id="5a506-136">보안의 관점에서 키 기반 인증을 사용하여 SSH 터널을 통해 VM에 연결한 다음 xrdp에 연결하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-136">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span></span> <span data-ttu-id="5a506-137">그렇다면, 원격 데스크톱 트래픽을 허용하도록 네트워크 보안 그룹 규칙을 만드는 방법에 대한 다음 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-137">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="5a506-138">원격 데스크톱 트래픽의 네트워크 보안 그룹 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="5a506-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="5a506-139">Linux VM에 도달하는 원격 데스크톱 트래픽을 허용하려면 포트 3389에 대한 TCP가 VM에 도달하도록 네트워크 보안 그룹 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-139">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span></span> <span data-ttu-id="5a506-140">네트워크 보안 그룹 규칙에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a506-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="5a506-141">[Azure Portal을 사용하여 네트워크 보안 그룹 규칙을 만들](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-141">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5a506-142">다음 예제에서는 [az network nsg rule create](/cli/azure/network/nsg/rule#create)를 사용하여 *tcp* 포트 *3389*에 대한 트래픽을 *허용*하는 *myNetworkSecurityGroupRule*이라는 네트워크 보안 그룹 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-142">The following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* to *allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="5a506-143">원격 데스크톱 클라이언트와 Linux VM 연결</span><span class="sxs-lookup"><span data-stu-id="5a506-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="5a506-144">로컬 원격 데스크톱 클라이언트를 열고 IP 주소 또는 Linux VM의 DNS 이름에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-144">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="5a506-145">사용자 계정의 사용자 이름 및 암호를 VM에 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-145">Enter the username and password for the user account on your VM as follows:</span></span>

![원격 데스크톱 클라이언트를 사용하여 xrdp에 연결](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="5a506-147">인증한 후에 xfce 데스크톱 환경이 로드되면 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-147">After authenticating, the xfce desktop environment will load and look similar to the following example:</span></span>

![xrdp를 통한 xfce 데스크톱 환경](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="5a506-149">문제 해결</span><span class="sxs-lookup"><span data-stu-id="5a506-149">Troubleshoot</span></span>
<span data-ttu-id="5a506-150">원격 데스크톱 클라이언트를 사용하여 Linux VM에 연결할 수 없으면 Linux VM에서 `netstat`을 사용하여 다음과 같이 VM이 RDP 연결을 수신 대기하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-150">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="5a506-151">다음 예제에서는 TCP 포트 3389를 예상대로 수신 대기하는 VM을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-151">The following example shows the VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="5a506-152">xrdp 서비스가 Ubuntu VM을 수신 대기하지 않는 경우 다음과 같이 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-152">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="5a506-153">서비스가 응답하지 않는 이유는 Ubuntu VM에서 */var/log*Thug의 로그를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as to why the service may not be responding.</span></span> <span data-ttu-id="5a506-154">또한 원격 데스크톱 연결을 시도하는 동안 syslog를 모니터링하여 모든 오류를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-154">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="5a506-155">Red Hat Enterprise Linux 및 SUSE와 같은 기타 Linux 배포에는 검토할 서비스 및 다른 로그 파일 위치를 다시 시작하는 다른 방법이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span></span>

<span data-ttu-id="5a506-156">원격 데스크톱 클라이언트에서 응답을 수신하지 않고 시스템 로그에 이벤트가 표시되지 않는 경우 이 동작은 원격 데스크톱 트래픽이 VM에 도달할 수 없다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-156">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span></span> <span data-ttu-id="5a506-157">네트워크 보안 그룹 규칙을 검토하여 포트 3389에서 TCP를 허용하는 규칙이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a506-157">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span></span> <span data-ttu-id="5a506-158">자세한 내용은 [응용 프로그램 연결 문제 해결](../windows/troubleshoot-app-connection.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a506-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5a506-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a506-159">Next steps</span></span>
<span data-ttu-id="5a506-160">Linux VM에서 SSH 키를 만들고 사용하는 방법에 대한 자세한 내용은 [Azure에서 Linux VM의 SSH 키 만들기](mac-create-ssh-keys.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a506-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="5a506-161">Windows에서 SSH를 사용하는 방법에 대한 자세한 내용은 [Windows에서 SSH 키를 사용하는 방법](ssh-from-windows.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a506-161">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

