---
title: "Azure VM에 대한 SSH 연결 문제 해결 | Microsoft Docs"
description: "Linux를 실행하는 Azure VM에 대해 'SSH 연결 실패' 또는 'SSH 연결 거부'와 같은 문제를 해결하는 방법입니다."
keywords: "ssh 연결 거부, ssh 오류, azure ssh, SSH 연결 실패"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: 3a282c8b2c2ba2749de6a2d3688bd57d75703b22
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="bc7e9-104">실패하거나 오류가 발생하거나 거부되는 Azure Linux VM에 대한 SSH 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="bc7e9-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="bc7e9-105">Linux VM(가상 컴퓨터)에 연결하려고 할 때 다양한 이유로 인해 SSH(Secure Shell) 오류, SSH 연결 실패 또는 SSH 연결 거부 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="bc7e9-106">이 문서는 문제를 찾아 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="bc7e9-107">Azure Portal, Azure CLI 또는 Linux용 VM 액세스 확장을 사용하여 연결 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="bc7e9-108">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](http://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="bc7e9-109">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="bc7e9-110">[Azure 지원 사이트](http://azure.microsoft.com/support/options/) 로 가서 **지원 받기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="bc7e9-111">Azure 지원을 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 지원 FAQ](http://azure.microsoft.com/support/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="bc7e9-112">빠른 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="bc7e9-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="bc7e9-113">각 문제 해결 단계 후 VM에 다시 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="bc7e9-114">SSH 구성을 재설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="bc7e9-115">사용자의 자격 증명을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="bc7e9-116">[네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md) 규칙이 SSH 트래픽을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="bc7e9-117">네트워크 보안 그룹 규칙이 SSH 트래픽을 허용하기 위해 존재하는지 확인합니다(기본적으로 TCP 포트 22).</span><span class="sxs-lookup"><span data-stu-id="bc7e9-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="bc7e9-118">Azure Load Balancer를 사용하지 않고 포트 리디렉션/매핑을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="bc7e9-119">[VM 리소스 상태](../../resource-health/resource-health-overview.md)를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="bc7e9-120">VM이 정상으로 보고하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="bc7e9-121">부팅 진단을 사용하도록 설정하는 경우 VM이 로그에서 부팅 오류를 보고하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="bc7e9-122">VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-122">Restart the VM.</span></span>
6. <span data-ttu-id="bc7e9-123">VM을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-123">Redeploy the VM.</span></span>

<span data-ttu-id="bc7e9-124">자세한 문제 해결 단계와 설명이 필요한 경우 계속 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="bc7e9-125">SSH 연결 문제 해결에 사용할 수 있는 방법</span><span class="sxs-lookup"><span data-stu-id="bc7e9-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="bc7e9-126">다음 방법 중 하나를 사용하여 자격 증명 또는 SSH 구성을 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="bc7e9-127">[Azure Portal](#use-the-azure-portal) - SSH 구성 또는 SSH 키를 신속하게 다시 설정해야 하는데 Azure 도구가 설치되지 않은 경우에 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="bc7e9-128">[Azure CLI 2.0](#use-the-azure-cli-20) - 명령줄에 이미 도달한 경우 SSH 구성 또는 자격 증명을 신속하게 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="bc7e9-129">[Azure CLI 1.0](#use-the-azure-cli-10)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="bc7e9-130">[Azure VMAccessForLinux 확장](#use-the-vmaccess-extension) - json 정의 파일을 만들고 다시 사용하여 SSH 구성 또는 사용자 자격 증명을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="bc7e9-131">각 문제 해결 단계 후 VM에 다시 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="bc7e9-132">그래도 연결할 수 없으면 다음 단계를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="bc7e9-133">Azure Portal 사용</span><span class="sxs-lookup"><span data-stu-id="bc7e9-133">Use the Azure portal</span></span>
<span data-ttu-id="bc7e9-134">Azure Portal은 로컬 컴퓨터에 도구를 설치하지 않고 SSH 구성 또는 사용자 자격 증명을 다시 설정하는 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="bc7e9-135">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="bc7e9-136">**지원 + 문제 해결** 섹션까지 아래로 스크롤하고 다음 예제와 같이 **암호 재설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![Azure Portal에서 SSH 구성 또는 자격 증명 다시 설정](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="bc7e9-138">SSH 구성 다시 설정</span><span class="sxs-lookup"><span data-stu-id="bc7e9-138">Reset the SSH configuration</span></span>
<span data-ttu-id="bc7e9-139">첫 번째 단계로 이전 화면처럼 **모드** 드롭 다운 메뉴에서 `Reset configuration only`을 선택하고 **다시 설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="bc7e9-140">이 작업이 완료되면 VM에 다시 액세스하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="bc7e9-141">사용자에 대한 SSH 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="bc7e9-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="bc7e9-142">기존 사용자의 자격 증명을 다시 설정하려면 이전 스크린샷과 같이 **모드** 드롭다운 메뉴에서 `Reset SSH public key` 또는 `Reset password`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="bc7e9-143">사용자 이름 및 SSH 키 또는 새 암호를 지정하고 **다시 설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="bc7e9-144">이 메뉴에서 VM에 대해 sudo 권한이 있는 사용자를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="bc7e9-145">새 사용자 이름 및 연결된 암호 또는 SSH 키를 입력한 다음 **다시 설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="bc7e9-146">Azure CLI 2.0 사용</span><span class="sxs-lookup"><span data-stu-id="bc7e9-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="bc7e9-147">아직 설치하지 않은 경우 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="bc7e9-148">사용자 지정 Linux 디스크 이미지를 만들고 업로드한 경우 [Microsoft Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 버전 2.0.5 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="bc7e9-149">갤러리 이미지를 사용하여 만든 VM의 경우 이 액세스 확장이 이미 설치되어 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="bc7e9-150">SSH 구성 다시 설정</span><span class="sxs-lookup"><span data-stu-id="bc7e9-150">Reset SSH configuration</span></span>
<span data-ttu-id="bc7e9-151">처음에 SSH 구성을 기본값으로 다시 설정하고 VM에서 SSH 서버를 다시 부팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-151">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="bc7e9-152">사용자 계정 이름, 암호 또는 SSH 키는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-152">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="bc7e9-153">다음 예제에서는 [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh)를 사용하여 `myResourceGroup`의 `myVM`이라는 VM에서 SSH 구성을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-153">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-154">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="bc7e9-155">사용자에 대한 SSH 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="bc7e9-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="bc7e9-156">다음 예제에서는 [az vm user update](/cli/azure/vm/user#update)를 사용하여 `myResourceGroup`의 `myVM`이라는 VM에서 `myUsername`의 자격 증명을 `myPassword`에 지정된 값으로 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-156">The following example uses [az vm user update](/cli/azure/vm/user#update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-157">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="bc7e9-158">SSH 키 인증을 사용하는 경우 지정된 사용자의 SSH 키를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-158">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="bc7e9-159">다음 예제에서는 **az vm access set-linux-user**를 사용하여 `myResourceGroup`의 `myVM`이라는 VM에서 `~/.ssh/id_rsa.pub`이라는 사용자의 `myUsername`에 저장된 SSH 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-159">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-160">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="bc7e9-161">VMAccess 확장 사용</span><span class="sxs-lookup"><span data-stu-id="bc7e9-161">Use the VMAccess extension</span></span>
<span data-ttu-id="bc7e9-162">Linux용 VM 액세스 확장은 수행하는 작업을 정의하는 json 파일에서 읽습니다. 이러한 작업에는 SSHD 다시 설정, SSH 키를 다시 설정 또는 사용자 추가가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-162">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="bc7e9-163">Azure CLI를 사용하여 VMAccess 확장을 호출할 수 있지만 원하는 경우 여러 VM에 걸쳐 json 파일을 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-163">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="bc7e9-164">이 방법을 통해 주어진 시나리오에 대해 호출될 수 있는 json 파일의 레포지토리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-164">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="bc7e9-165">SSHD 재설정</span><span class="sxs-lookup"><span data-stu-id="bc7e9-165">Reset SSHD</span></span>
<span data-ttu-id="bc7e9-166">다음과 같은 내용으로 `settings.json`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-166">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="bc7e9-167">Azure CLI를 사용하여 json 파일을 지정하여 SSHD 연결을 다시 설정하도록 `VMAccessForLinux` 확장을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-167">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="bc7e9-168">다음 예제에서는 [az vm extension set](/cli/azure/vm/extension#set)을 사용하여 `myResourceGroup`의 `myVM`이라는 VM에서 SSHD를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-168">The following example uses [az vm extension set](/cli/azure/vm/extension#set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-169">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="bc7e9-170">사용자에 대한 SSH 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="bc7e9-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="bc7e9-171">SSHD가 정상적으로 작동하는 것으로 나타나면 지정된 사용자의 자격 증명을 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-171">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="bc7e9-172">사용자에 대한 암호를 재설정하려면 `settings.json`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-172">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="bc7e9-173">다음 예제에서는 VM에서 `myUsername`의 자격 증명을 `myPassword`에 지정된 값으로 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-173">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="bc7e9-174">고유한 값을 사용하여 다음 줄을 `settings.json` 파일에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-174">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="bc7e9-175">또는 사용자에 대한 SSH 키를 다시 설정하려면 먼저 `settings.json` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-175">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="bc7e9-176">다음 예제에서는 `myResourceGroup`의 `myVM`이라는 VM에서 `myUsername`의 자격 증명을 `myPassword`에 지정된 값으로 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-176">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-177">고유한 값을 사용하여 다음 줄을 `settings.json` 파일에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-177">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="bc7e9-178">json 파일을 만든 후에 json 파일을 지정하여 SSH 사용자 자격 증명을 다시 설정하는 `VMAccessForLinux` 확장을 호출하도록 Azure CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-178">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="bc7e9-179">다음 예제에서는 `myResourceGroup`의 VM `myVM`에서 자격 증명을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-179">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-180">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="bc7e9-181">Azure CLI 1.0 사용</span><span class="sxs-lookup"><span data-stu-id="bc7e9-181">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="bc7e9-182">아직 수행하지 않은 경우 [Azure CLI 1.0을 설치하고 Azure 구독에 연결](../../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-182">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="bc7e9-183">다음과 같이 Resource Manager 모드를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="bc7e9-184">사용자 지정 Linux 디스크 이미지를 만들고 업로드한 경우 [Microsoft Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 버전 2.0.5 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-184">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="bc7e9-185">갤러리 이미지를 사용하여 만든 VM의 경우 이 액세스 확장이 이미 설치되어 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="bc7e9-186">SSH 구성 다시 설정</span><span class="sxs-lookup"><span data-stu-id="bc7e9-186">Reset SSH configuration</span></span>
<span data-ttu-id="bc7e9-187">SSHD 구성 자체가 잘못 구성되었거나 서비스에서 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-187">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="bc7e9-188">SSH 구성 자체가 올바르도록 SSHD를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-188">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="bc7e9-189">SSHD 다시 설정은 수행한 첫 번째 문제 해결 단계여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-189">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="bc7e9-190">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`에서 SSHD를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-190">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-191">다음과 같이 고유한 VM 및 리소스 그룹 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="bc7e9-192">사용자에 대한 SSH 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="bc7e9-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="bc7e9-193">SSHD가 정상적으로 작동하는 것으로 나타나면 지정된 사용자의 암호를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-193">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="bc7e9-194">다음 예제에서는 `myResourceGroup`의 `myVM`이라는 VM에서 `myUsername`의 자격 증명을 `myPassword`에 지정된 값으로 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-194">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-195">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="bc7e9-196">SSH 키 인증을 사용하는 경우 지정된 사용자의 SSH 키를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-196">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="bc7e9-197">다음 예제에서는 `myResourceGroup`의 `myVM`이라는 VM에서 `myUsername` 사용자를 위해 `~/.ssh/id_rsa.pub`에 저장된 SSH 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-197">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-198">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="bc7e9-199">VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="bc7e9-199">Restart a VM</span></span>
<span data-ttu-id="bc7e9-200">SSH 구성 및 사용자 자격 증명을 다시 설정했거나 그 과정에서 오류가 발생한 경우 VM을 다시 시작하여 기본 계산 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-200">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="bc7e9-201">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bc7e9-201">Azure portal</span></span>
<span data-ttu-id="bc7e9-202">Azure Portal을 사용하여 VM을 다시 시작하려면 다음 예제와 같이 VM을 선택하고 **다시 시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-202">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Azure Portal에서 VM 다시 시작](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="bc7e9-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bc7e9-204">Azure CLI 1.0</span></span>
<span data-ttu-id="bc7e9-205">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-205">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-206">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="bc7e9-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bc7e9-207">Azure CLI 2.0</span></span>
<span data-ttu-id="bc7e9-208">다음 예제에서는 [az vm restart](/cli/azure/vm#restart)를 사용하여 `myResourceGroup`이라는 리소스 그룹의 `myVM`이라는 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-208">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-209">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="bc7e9-210">VM 재배포</span><span class="sxs-lookup"><span data-stu-id="bc7e9-210">Redeploy a VM</span></span>
<span data-ttu-id="bc7e9-211">Azure 내의 다른 노드로 VM을 재배포하여 기본 네트워킹 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-211">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="bc7e9-212">VM을 다시 배포하는 방법에 대한 자세한 내용은 [새 Azure 노드로 가상 컴퓨터 다시 배포](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-212">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="bc7e9-213">이 작업이 완료되면 임시 디스크 데이터가 손실되고 가상 컴퓨터와 연결된 동적 IP 주소가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="bc7e9-214">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bc7e9-214">Azure portal</span></span>
<span data-ttu-id="bc7e9-215">Azure Portal을 사용하여 VM을 다시 배포하려면 VM을 선택하고 **지원 + 문제 해결** 섹션까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-215">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="bc7e9-216">다음 예제와 같이 **다시 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-216">Click the **Redeploy** button as in the following example:</span></span>

![Azure Portal에서 VM 다시 배포](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="bc7e9-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bc7e9-218">Azure CLI 1.0</span></span>
<span data-ttu-id="bc7e9-219">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-219">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-220">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="bc7e9-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bc7e9-221">Azure CLI 2.0</span></span>
<span data-ttu-id="bc7e9-222">다음 예제에서는 [az vm redeploy](/cli/azure/vm#redeploy)를 사용하여 `myResourceGroup`이라는 리소스 그룹의 `myVM`이라는 VM을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-222">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="bc7e9-223">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="bc7e9-224">클래식 배포 모델을 사용하여 만든 VM</span><span class="sxs-lookup"><span data-stu-id="bc7e9-224">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="bc7e9-225">클래식 배포 모델을 사용하여 만든 VM의 보다 일반적인 SSH 연결 오류를 해결하려면 다음 단계를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-225">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="bc7e9-226">각 단계 후 VM에 다시 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-226">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="bc7e9-227">[Azure Portal](https://portal.azure.com)에서 원격 액세스를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-227">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bc7e9-228">Azure Portal에서 VM을 선택하고 **원격 다시 설정...** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-228">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="bc7e9-229">VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-229">Restart the VM.</span></span> <span data-ttu-id="bc7e9-230">[Azure portal](https://portal.azure.com)에서 VM을 선택하고 **다시 시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-230">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="bc7e9-231">새 Azure 노드에 VM을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-231">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="bc7e9-232">VM을 다시 배포하는 방법에 대한 자세한 내용은 [새 Azure 노드로 가상 컴퓨터 다시 배포](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-232">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="bc7e9-233">이 작업이 완료되면 임시 디스크 데이터가 손실되고 가상 컴퓨터와 연결된 동적 IP 주소가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="bc7e9-234">[Linux 기반 가상 컴퓨터의 암호 또는 SSH를 다시 설정하는 방법](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-234">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="bc7e9-235">암호 또는 SSH 키를 재설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-235">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="bc7e9-236">새 *sudo* 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="bc7e9-237">SSH 구성을 재설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-237">Reset the SSH configuration.</span></span>
* <span data-ttu-id="bc7e9-238">VM 리소스 상태에 플랫폼 문제가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-238">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="bc7e9-239">VM을 선택하고 **설정** > **상태 확인**까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bc7e9-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bc7e9-240">Additional resources</span></span>
* <span data-ttu-id="bc7e9-241">후속 단계를 수행한 후에도 VM에 대해 SSH를 사용할 수 없는 경우 [자세한 문제 해결 단계](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하여 단계를 검토하고 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-241">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="bc7e9-242">응용 프로그램 액세스 문제를 해결하는 방법에 대한 자세한 내용은 [Azure 가상 컴퓨터에서 실행 중인 응용 프로그램에 대한 액세스 문제 해결](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-242">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="bc7e9-243">클래식 배포 모델을 사용하여 만든 가상 컴퓨터의 문제 해결 방법에 대한 자세한 내용은 [Linux 기반 가상 컴퓨터의 암호 또는 SSH를 다시 설정하는 방법](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc7e9-243">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

