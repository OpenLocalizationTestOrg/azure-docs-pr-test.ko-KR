---
title: "aaaTroubleshoot SSH 연결 문제 tooan Azure VM | Microsoft Docs"
description: "어떻게 tootroubleshoot 발급 'SSH 연결을 실패 했습니다.' 또는 'SSH 연결을 거부 했습니다.'와 같은 Azure VM에 대 한 Linux를 실행 합니다."
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
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="49ecc-104">SSH 연결 tooan Azure Linux VM에 실패 하면 out, 오류 또는 거부 되었습니다. 문제 해결</span><span class="sxs-lookup"><span data-stu-id="49ecc-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="49ecc-105">SSH 연결 실패, SSH (보안 셸) 오류가 발생 하면 또는 SSH 거부 되었습니다. tooconnect tooa Linux 가상 컴퓨터 (VM)를 할 때 다양 한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="49ecc-106">이 문서에서는 찾기 및 올바른 hello 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="49ecc-107">Linux tootroubleshoot에 hello Azure 포털, Azure CLI 또는 VM 액세스 확장을 사용할 수 있으며 연결 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="49ecc-108">이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure 및 스택 오버플로 포럼 hello](http://azure.microsoft.com/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="49ecc-109">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="49ecc-110">Toohello 이동 [Azure 지원 사이트](http://azure.microsoft.com/support/options/) 선택 **지원을 받는**합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="49ecc-111">Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](http://azure.microsoft.com/support/faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="49ecc-112">빠른 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="49ecc-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="49ecc-113">각 문제 해결 단계를 수행한 후 toohello VM을 다시 연결을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="49ecc-114">Hello SSH 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="49ecc-115">Hello hello 사용자 자격 증명 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="49ecc-116">Hello 확인 [네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md) 규칙 SSH 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="49ecc-117">네트워크 보안 그룹 규칙 (기본적으로 TCP 포트 22) toopermit SSH 트래픽 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="49ecc-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="49ecc-118">Azure Load Balancer를 사용하지 않고 포트 리디렉션/매핑을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="49ecc-119">Hello 확인 [VM 리소스 상태](../../resource-health/resource-health-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="49ecc-120">해당 hello VM 확인 정상인로 보고서 사용.</span><span class="sxs-lookup"><span data-stu-id="49ecc-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="49ecc-121">부트 진단이 사용 하도록 설정 하는 경우 VM hello hello 로그에 있는 부팅 오류를 보고 하지 않는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="49ecc-122">Hello VM을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-122">Restart hello VM.</span></span>
6. <span data-ttu-id="49ecc-123">Hello VM을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-123">Redeploy hello VM.</span></span>

<span data-ttu-id="49ecc-124">자세한 문제 해결 단계와 설명이 필요한 경우 계속 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="49ecc-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="49ecc-125">사용할 수 있는 방법 tootroubleshoot SSH 연결 문제</span><span class="sxs-lookup"><span data-stu-id="49ecc-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="49ecc-126">자격 증명 또는 hello 메서드를 다음 중 하나를 사용 하 여 SSH 구성을 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="49ecc-127">[Azure 포털](#use-the-azure-portal) -tooquickly 해야 할 경우 좋은 hello SSH 구성을 또는 SSH 키를 다시 설정 하 고 설치 된 Azure 도구를 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="49ecc-128">[Azure CLI 2.0](#use-the-azure-cli-20) -이미 실행 중인 hello 명령줄에 신속 하 게 hello SSH 구성을 다시 설정 또는 자격 증명 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="49ecc-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="49ecc-129">Hello를 사용할 수도 있습니다 [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="49ecc-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="49ecc-130">[Azure 작업에서는 VMAccessForLinux 확장](#use-the-vmaccess-extension) -만들고 json 정의 파일 tooreset hello SSH 구성 또는 사용자 자격 증명을 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="49ecc-131">각 문제 해결 단계 후 tooyour VM을 다시 연결 하십시오.</span><span class="sxs-lookup"><span data-stu-id="49ecc-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="49ecc-132">여전히 연결할 수 없는 경우 hello 다음 단계를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="49ecc-133">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="49ecc-133">Use hello Azure portal</span></span>
<span data-ttu-id="49ecc-134">hello Azure 포털 로컬 컴퓨터에 다양 한 도구를 설치 하지 않고 신속 하 게 tooreset hello는 SSH 구성 이나 사용자 자격 증명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="49ecc-135">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="49ecc-136">Toohello 아래로 스크롤하여 **지원 + 문제 해결** 선택한 섹션 **암호 재설정** hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="49ecc-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![Hello Azure 포털에서에서 자격 증명 또는 SSH 구성을 다시 설정](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="49ecc-138">Hello SSH 구성을 다시 설정</span><span class="sxs-lookup"><span data-stu-id="49ecc-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="49ecc-139">첫 번째 단계로, 선택 `Reset configuration only` hello에서 **모드** 드롭 다운 메뉴 hello 스크린 샷, 이전에 클릭 hello **재설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="49ecc-140">이 작업 완료 되 면 tooaccess VM 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="49ecc-141">사용자에 대한 SSH 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="49ecc-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="49ecc-142">기존 사용자의 tooreset hello 자격 증명 중 하나를 선택 합니다. `Reset SSH public key` 또는 `Reset password` hello에서 **모드** hello 스크린 샷 앞에서 같이 드롭 다운 메뉴.</span><span class="sxs-lookup"><span data-stu-id="49ecc-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="49ecc-143">Hello 사용자 이름 및 SSH 키 또는 새 암호를 지정 하 고 hello 클릭 **재설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="49ecc-144">또한이 메뉴에서 VM hello에서 sudo 권한이 있는 사용자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="49ecc-145">새 사용자 이름 및 연결 된 암호 또는 SSH 키를 입력 하 고 클릭 hello **재설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="49ecc-146">Hello Azure CLI 2.0을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="49ecc-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="49ecc-147">아직 하지 않는 경우 hello를 최신 버전 설치 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="49ecc-148">만든 사용자 지정 Linux 디스크 이미지를 업로드 하는 경우 확인 되었는지 hello [Microsoft Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 2.0.5 버전 이상이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="49ecc-149">갤러리 이미지를 사용하여 만든 VM의 경우 이 액세스 확장이 이미 설치되어 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="49ecc-150">SSH 구성 다시 설정</span><span class="sxs-lookup"><span data-stu-id="49ecc-150">Reset SSH configuration</span></span>
<span data-ttu-id="49ecc-151">처음 시도 재설정 하는 중 hello SSH 구성 toodefault 값과 재부팅 중 이어서 hello SSH 서버 hello VM에서 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="49ecc-152">이 변경 한다는 것 hello 사용자 계정 이름, 암호 또는 SSH 키 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="49ecc-153">hello 다음 예제에서는 [az vm 사용자 재설정-ssh](/cli/azure/vm/user#reset-ssh) hello 라는 VM에서 tooreset hello SSH 구성을 `myVM` 에서 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-154">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="49ecc-155">사용자에 대한 SSH 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="49ecc-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="49ecc-156">hello 다음 예제에서는 [az vm 사용자 업데이트](/cli/azure/vm/user#update) tooreset hello에 대 한 자격 증명 `myUsername` toohello 값에 지정 된 `myPassword`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-157">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="49ecc-158">SSH 키 인증을 사용 하는 경우 지정된 된 사용자에 대 한 hello SSH 키를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="49ecc-159">hello 다음 예제에서는 **az vm 집합-linux 사용자 액세스** tooupdate hello SSH 키에 저장 된 `~/.ssh/id_rsa.pub` 라는 hello 사용자에 대 한 `myUsername`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-160">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="49ecc-161">Hello VMAccess 확장을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="49ecc-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="49ecc-162">Linux 용 VM 액세스 확장 hello 아웃 toocarry 동작을 정의 하는 json 파일에서 읽습니다. 이러한 작업에는 SSHD 다시 설정, SSH 키를 다시 설정 또는 사용자 추가가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="49ecc-163">Hello Azure CLI toocall hello VMAccess 확장을 계속 사용할 하지만 원하는 경우 여러 Vm 간에 hello json 파일을 재사용할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="49ecc-164">이 방법을 사용 하면 toocreate 주어진 시나리오에 대 한 다음 호출 수 있는 json 파일의 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="49ecc-165">SSHD 재설정</span><span class="sxs-lookup"><span data-stu-id="49ecc-165">Reset SSHD</span></span>
<span data-ttu-id="49ecc-166">라는 파일을 만들어 `settings.json` 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="49ecc-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="49ecc-167">Hello Azure CLI를 사용 하 여 다음 호출 hello `VMAccessForLinux` 확장 tooreset json 파일을 지정 하 여 SSHD 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="49ecc-168">hello 다음 예제에서는 [az vm 확장 집합](/cli/azure/vm/extension#set) hello 라는 VM에서 tooreset SSHD `myVM` 에서 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-169">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="49ecc-170">사용자에 대한 SSH 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="49ecc-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="49ecc-171">SSHD toofunction 올바르게 나타나면 giver 사용자에 대 한 hello 자격 증명을 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="49ecc-172">사용자가 tooreset hello 암호 라는 파일을 만들어 `settings.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="49ecc-173">hello 다음 예제에서는 다시 설정에 대 한 자격 증명 hello `myUsername` toohello 값에 지정 된 `myPassword`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="49ecc-174">Hello 줄에 다음을 입력 하면 `settings.json` 고유한 값을 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="49ecc-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="49ecc-175">또는 사용자에 대 한 SSH 키 hello, 먼저 라는 파일을 만들어 tooreset `settings.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="49ecc-176">hello 다음 예제에서는 다시 설정에 대 한 자격 증명 hello `myUsername` toohello 값에 지정 된 `myPassword`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-177">Hello 줄에 다음을 입력 하면 `settings.json` 고유한 값을 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="49ecc-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="49ecc-178">Json 파일을 만든 후 hello Azure CLI toocall hello를 사용 하 여 `VMAccessForLinux` 확장 tooreset json 파일을 지정 하 여 SSH 사용자 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="49ecc-179">hello 다음 예제에서는 재설정 hello 라는 VM에서 자격 증명 `myVM` 에서 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-180">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="49ecc-181">Hello Azure CLI 1.0을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="49ecc-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="49ecc-182">아직 없는 경우, [hello Azure CLI 1.0을 설치 하 고 tooyour Azure 구독 연결](../../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="49ecc-183">다음과 같이 Resource Manager 모드를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="49ecc-184">만든 사용자 지정 Linux 디스크 이미지를 업로드 하는 경우 확인 되었는지 hello [Microsoft Azure Linux 에이전트](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 2.0.5 버전 이상이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="49ecc-185">갤러리 이미지를 사용하여 만든 VM의 경우 이 액세스 확장이 이미 설치되어 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="49ecc-186">SSH 구성 다시 설정</span><span class="sxs-lookup"><span data-stu-id="49ecc-186">Reset SSH configuration</span></span>
<span data-ttu-id="49ecc-187">hello SSHD 구성 자체 잘못 구성 되었을 수 있습니다 또는 hello 서비스 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="49ecc-188">SSHD toomake 자체 hello SSH 구성이 유효한 지 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="49ecc-189">SSHD 재설정 hello 첫 번째 문제 해결 단계를 수행한 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="49ecc-190">hello 다음 예제에서는 재설정 라는 VM에서 SSHD `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-191">다음과 같이 고유한 VM 및 리소스 그룹 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="49ecc-192">사용자에 대한 SSH 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="49ecc-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="49ecc-193">SSHD toofunction 올바르게 나타나면 hello giver 사용자의 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="49ecc-194">hello 다음 예제에서는 다시 설정에 대 한 자격 증명 hello `myUsername` toohello 값에 지정 된 `myPassword`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-195">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="49ecc-196">SSH 키 인증을 사용 하는 경우 지정된 된 사용자에 대 한 hello SSH 키를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="49ecc-197">다음 예에서는 업데이트 hello SSH 키에 저장 된 hello `~/.ssh/id_rsa.pub` 라는 hello 사용자에 대 한 `myUsername`, hello 라는 VM에서 `myVM` 에서 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-198">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="49ecc-199">VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="49ecc-199">Restart a VM</span></span>
<span data-ttu-id="49ecc-200">Hello SSH 구성 및 사용자 자격 증명 다시 설정, 또는 작업에 오류가 발생 하는 경우에 hello VM tooaddress 되었던 계산 문제를 다시 시작을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="49ecc-201">Azure portal</span><span class="sxs-lookup"><span data-stu-id="49ecc-201">Azure portal</span></span>
<span data-ttu-id="49ecc-202">사용 하 여 VM toorestart hello Azure 포털에서 선택 하 고 VM hello **다시 시작** hello 다음 예제와 같이 단추:</span><span class="sxs-lookup"><span data-stu-id="49ecc-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Hello Azure 포털에서에서 VM을 다시 시작](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="49ecc-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="49ecc-204">Azure CLI 1.0</span></span>
<span data-ttu-id="49ecc-205">다음 예제에서는 다시 시작 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-206">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="49ecc-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="49ecc-207">Azure CLI 2.0</span></span>
<span data-ttu-id="49ecc-208">hello 다음 예제에서는 [az vm 다시 시작](/cli/azure/vm#restart) toorestart hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-209">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="49ecc-210">VM 재배포</span><span class="sxs-lookup"><span data-stu-id="49ecc-210">Redeploy a VM</span></span>
<span data-ttu-id="49ecc-211">모든 기본 네트워킹 문제를 해결할 수도 있습니다는 Azure 내에서 VM tooanother 노드를 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="49ecc-212">VM을 다시 배포 하는 방법에 대 한 정보를 참조 하십시오. [가상 컴퓨터 toonew Azure 노드를 다시 배포](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="49ecc-213">이 작업이 완료 되 면 임시 디스크 데이터 손실 되 고 hello 가상 컴퓨터와 연결 된 동적 IP 주소 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="49ecc-214">Azure portal</span><span class="sxs-lookup"><span data-stu-id="49ecc-214">Azure portal</span></span>
<span data-ttu-id="49ecc-215">VM 및 toohello 아래로 스크롤하여 사용 하 여 VM tooredeploy hello Azure 포털에서 선택 **지원 + 문제 해결** 섹션.</span><span class="sxs-lookup"><span data-stu-id="49ecc-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="49ecc-216">Hello 클릭 **재배포** hello 다음 예제와 같이 단추:</span><span class="sxs-lookup"><span data-stu-id="49ecc-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Hello Azure 포털에서에서 VM을 다시 배포](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="49ecc-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="49ecc-218">Azure CLI 1.0</span></span>
<span data-ttu-id="49ecc-219">다음 예에서는 재배포 시 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-220">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="49ecc-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="49ecc-221">Azure CLI 2.0</span></span>
<span data-ttu-id="49ecc-222">다음 예에서는 사용 하 여 hello [az vm 재배포](/cli/azure/vm#redeploy) tooredeploy hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="49ecc-223">다음과 같이 사용자 고유의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="49ecc-224">Hello 클래식 배포 모델을 사용 하 여 만든 Vm</span><span class="sxs-lookup"><span data-stu-id="49ecc-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="49ecc-225">Hello 클래식 배포 모델을 사용 하 여 만든 Vm에 대해 이러한 단계 tooresolve hello 가장 일반적인 SSH 연결 실패를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="49ecc-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="49ecc-226">각 단계를 수행한 후 toohello VM을 다시 연결을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="49ecc-227">Hello에서 원격 액세스를 다시 설정 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="49ecc-228">에 Azure 포털 hello VM을 선택 하 고 hello 클릭 **원격 다시 설정...**  단추입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="49ecc-229">Hello VM을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-229">Restart hello VM.</span></span> <span data-ttu-id="49ecc-230">Hello에 [Azure 포털](https://portal.azure.com), VM을 선택 하 고 hello 클릭 **다시 시작** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="49ecc-231">Hello VM tooa 새 Azure 노드를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="49ecc-232">방법에 대 한 정보에 대 한 VM을 tooredeploy 참조 [가상 컴퓨터 toonew Azure 노드를 다시 배포](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="49ecc-233">이 작업이 완료 되 면 임시 디스크 데이터 손실 되 고 hello 가상 컴퓨터와 연결 된 동적 IP 주소 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="49ecc-234">Hello 지침에 따라 [어떻게 tooreset 암호 또는 Linux 기반 가상 컴퓨터에 대 한 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 에:</span><span class="sxs-lookup"><span data-stu-id="49ecc-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="49ecc-235">Hello 암호 또는 SSH 키를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="49ecc-236">새 *sudo* 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="49ecc-237">Hello SSH 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="49ecc-238">플랫폼 문제가 있는지에 대 한 hello VM의 리소스 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="49ecc-239">VM을 선택하고 **설정** > **상태 확인**까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49ecc-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="49ecc-240">Additional resources</span></span>
* <span data-ttu-id="49ecc-241">인 경우 아직 못했습니다 tooSSH tooyour VM 후 다음 단계 이후 hello 참조 [자세한 문제 해결 단계](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview 추가 단계 tooresolve 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="49ecc-242">응용 프로그램 액세스 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [문제 해결 액세스 tooan 응용 프로그램이 Azure 가상 컴퓨터에서 실행 중인](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="49ecc-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="49ecc-243">Hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooreset 암호 또는 Linux 기반 가상 컴퓨터에 대 한 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="49ecc-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

