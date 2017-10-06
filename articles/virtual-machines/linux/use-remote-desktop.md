---
title: "Azure에서 Linux VM aaaUse 원격 데스크톱 tooa | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall 그래픽 도구를 사용 하 여 Azure에서 원격 데스크톱 (xrdp) tooconnect tooa Linux VM을 구성 하 고"
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
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="698d9-103">설치 하 고 Azure에서 원격 데스크톱 tooconnect tooa Linux VM 구성</span><span class="sxs-lookup"><span data-stu-id="698d9-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="698d9-104">Azure에서 Linux 가상 컴퓨터 (Vm)는 안전한 셸 SSH 연결을 사용 하 여 hello 명령줄에서 일반적으로 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="698d9-105">때 새 tooLinux 또는 빠른 문제 해결 시나리오에 대 한 원격 데스크톱의 hello 사용이 더 쉬울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="698d9-106">이 세부 정보를 어떻게 문서 tooinstall 데스크톱 환경을 구성 하 고 ([xfce](https://www.xfce.org)) 및 원격 데스크톱 ([xrdp](http://www.xrdp.org)) hello 리소스 관리자 배포 모델을 사용 하 여 Linux VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="698d9-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="698d9-107">Prerequisites</span></span>
<span data-ttu-id="698d9-108">이 문서에는 Azure의 기존 Linux VM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="698d9-109">VM toocreate 해야 할 경우 hello 메서드를 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="698d9-110">hello [Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="698d9-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="698d9-111">hello [Azure 포털](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="698d9-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="698d9-112">Linux VM에서 데스크톱 환경 설치</span><span class="sxs-lookup"><span data-stu-id="698d9-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="698d9-113">Azure의 Linux VM은 대부분 데스크톱 환경을 기본적으로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="698d9-114">Linux VM은 일반적으로 데스크톱 환경이 아닌 SSH 연결을 사용하여 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="698d9-115">Linux에서 다양한 데스크톱 환경을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="698d9-116">데스크톱 환경의 선택에 따라 것 수 too2 1GB의 디스크 공간을 소비 5 too10 분 tooinstall과 모든 hello 필요한 패키지를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="698d9-117">hello 다음 예제에서는 설치 hello lightweight [xfce4](https://www.xfce.org/) Ubuntu VM에서 데스크톱 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="698d9-118">조금씩 다른 배포에 대 한 명령 (사용 하 여 `yum` tooinstall Red Hat Enterprise Linux에 적절 한 구성 및 `selinux` 규칙 또는 사용 `zypper` 예를 들어, SUSE에 tooinstall).</span><span class="sxs-lookup"><span data-stu-id="698d9-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="698d9-119">첫째, SSH tooyour VM입니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="698d9-120">hello 다음 예제에서는 연결 toohello 라는 VM *myvm.westus.cloudapp.azure.com* 의 hello username *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="698d9-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="698d9-121">Windows를 사용 하는 SSH를 사용 하 여에 자세한 정보가 필요한 경우 참조 [windows toouse SSH 키는 어떻게](ssh-from-windows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="698d9-122">다음으로 다음과 같이 `apt`를 사용하여 xfce를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="698d9-123">원격 데스크톱 서버 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="698d9-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="698d9-124">설치 된 데스크톱 환경이가지고 들어오는 연결에 대 한 원격 데스크톱 서비스 toolisten를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="698d9-125">[xrdp](http://xrdp.org)는 대부분의 Linux 배포판에서 사용할 수 있는 오픈 소스 RDP(원격 데스크톱 프로토콜) 서버로 xfce와 함께 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="698d9-126">다음과 같이 Ubuntu VM에 xrdp를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="698d9-127">사용자 세션을 시작할 때 xrdp 어떤 데스크톱 환경 toouse를 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="698d9-128">다음과 같이 xrdp toouse xfce 데스크톱 환경으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="698d9-129">다음과 같이 hello 변경 tootake 효과 대 한 hello xrdp 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="698d9-130">로컬 사용자 계정 암호 설정</span><span class="sxs-lookup"><span data-stu-id="698d9-130">Set a local user account password</span></span>
<span data-ttu-id="698d9-131">VM을 만들 때 사용자 계정의 암호를 만든 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="698d9-132">만 SSH 키 인증을 사용 하 고 로컬 계정 암호 설정, xrdp toolog tooyour VM에서에서 사용 하기 전에 암호를 지정 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="698d9-133">xrdp는 인증을 위해 SSH 키를 수락할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="698d9-134">hello 다음 예제에서는 지정 hello 사용자 계정에 대 한 암호 *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="698d9-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="698d9-135">암호를 지정 하는 현재 없는 경우 프로그램 SSHD 구성 toopermit 암호 로그인 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="698d9-136">보안 측면에서 키 기반 인증을 사용 하 여 SSH 터널이와 tooconnect tooyour VM을 원하는 수 고 tooxrdp 다음 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="698d9-137">이 경우 네트워크 보안 그룹 규칙 tooallow 원격 데스크톱 트래픽이 만드는 방법에 단계를 수행 하는 hello를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="698d9-138">원격 데스크톱 트래픽의 네트워크 보안 그룹 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="698d9-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="698d9-139">원격 데스크톱 트래픽 tooreach tooallow Linux VM 네트워크 보안 그룹 규칙 필요 toobe 만든 VM 포트 3389 tooreach에 TCP를 허용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="698d9-140">네트워크 보안 그룹 규칙에 대한 자세한 내용은 [네트워크 보안 그룹이란?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="698d9-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="698d9-141">수도 있습니다 [사용 하 여 Azure 포털 toocreate를 네트워크 보안 그룹 규칙 hello](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="698d9-142">hello 다음 예제에서는 네트워크 보안 그룹 규칙으로 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 라는 *myNetworkSecurityGroupRule* 너무*허용* 에서트래픽을*tcp* 포트 *3389*합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="698d9-143">원격 데스크톱 클라이언트와 Linux VM 연결</span><span class="sxs-lookup"><span data-stu-id="698d9-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="698d9-144">로컬 원격 데스크톱 클라이언트를 열고 toohello IP 주소 또는 Linux VM의 DNS 이름을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="698d9-145">Hello 사용자 이름 및 암호 hello 사용자 계정에 대 한 VM에 다음과 같이 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![원격 데스크톱 클라이언트를 사용 하 여 tooxrdp 연결](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="698d9-147">를 인증 한 후 hello xfce 데스크톱 환경을 로드 하 고 다음 예제와 비슷한 toohello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![xrdp를 통한 xfce 데스크톱 환경](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="698d9-149">문제 해결</span><span class="sxs-lookup"><span data-stu-id="698d9-149">Troubleshoot</span></span>
<span data-ttu-id="698d9-150">원격 데스크톱 클라이언트를 사용 하 여 Linux VM tooyour를 연결할 수 없는 경우 사용 하 여 `netstat` VM RDP 연결을 위해 다음과 같이 수신 하 여 Linux VM tooverify에:</span><span class="sxs-lookup"><span data-stu-id="698d9-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="698d9-151">다음 예제와 hello hello 3389 예상 대로 TCP 포트에서 수신 대기 하는 VM:</span><span class="sxs-lookup"><span data-stu-id="698d9-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="698d9-152">Hello xrdp 서비스가 수신 대기 하지 않는 경우 Ubuntu VM에서 서비스를 다시 시작 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="698d9-153">검토 로그인 */var/로그*몸이 야 toowhy hello 서비스로 표시에 대 한 Ubuntu VM에 응답 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="698d9-154">모든 오류는 원격 데스크톱 연결 시도가 tooview 중 hello syslog를도 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="698d9-155">다양 한 방법 toorestart 서비스 및 대체 로그 파일 위치 tooreview Red Hat Enterprise Linux 및 SUSE와 같은 다른 Linux 배포판 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="698d9-156">원격 데스크톱 클라이언트에서 받은 모든 응답을 수신 하지 않음 hello 시스템 로그에서 모든 이벤트 표시 되지 않으면 하는 경우이 문제는 원격 데스크톱 트래픽을 hello VM에 연결할 수 없습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="698d9-157">포트 3389에 규칙 toopermit TCP를 포함 하 여 네트워크 보안 그룹 규칙 tooensure를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="698d9-158">자세한 내용은 [응용 프로그램 연결 문제 해결](../windows/troubleshoot-app-connection.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="698d9-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="698d9-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="698d9-159">Next steps</span></span>
<span data-ttu-id="698d9-160">Linux VM에서 SSH 키를 만들고 사용하는 방법에 대한 자세한 내용은 [Azure에서 Linux VM의 SSH 키 만들기](mac-create-ssh-keys.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="698d9-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="698d9-161">Windows에서 SSH를 사용 하는 방법은 참조 하십시오. [windows toouse SSH 키는 어떻게](ssh-from-windows.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="698d9-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

