---
title: "Hadoop에서 SSH 사용 - Azure HDInsight | Microsoft Docs"
description: "SSH(보안 셸)를 사용하여 HDInsight에 액세스할 수 있습니다. 이 문서에서는 Windows, Linux, Unix 또는 macOS 클라이언트의 ssh 및 scp 명령을 사용하여 HDInsight에 연결하는 방법에 대해 설명합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "Linux의 Hadoop 명령, Hadoop Linux 명령, Hadoop macOS, SSH Hadoop, SSH Hadoop 클러스터"
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: df0feb51469333bac42c779d860192d46f24ac62
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-hdinsight-hadoop-using-ssh"></a><span data-ttu-id="9eac0-105">SSH를 사용하여 HDInsight(Hadoop)에 연결</span><span class="sxs-lookup"><span data-stu-id="9eac0-105">Connect to HDInsight (Hadoop) using SSH</span></span>

<span data-ttu-id="9eac0-106">[SSH(보안 셸)](https://en.wikipedia.org/wiki/Secure_Shell)을 사용하여 Azure HDInsight의 Hadoop에 안전하게 연결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-106">Learn how to use [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) to securely connect to Hadoop on Azure HDInsight.</span></span> 

<span data-ttu-id="9eac0-107">HDInsight는 Hadoop 클러스터 내에서 노드의 운영 체제로 Linux(Ubuntu)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-107">HDInsight can use Linux (Ubuntu) as the operating system for nodes within the Hadoop cluster.</span></span> <span data-ttu-id="9eac0-108">다음 표에서는 SSH 클라이언트를 사용하여 Linux 기반 HDInsight에 연결할 때 필요한 주소와 포트 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-108">The following table contains the address and port information needed when connecting to Linux-based HDInsight using an SSH client:</span></span>

| <span data-ttu-id="9eac0-109">주소</span><span class="sxs-lookup"><span data-stu-id="9eac0-109">Address</span></span> | <span data-ttu-id="9eac0-110">포트</span><span class="sxs-lookup"><span data-stu-id="9eac0-110">Port</span></span> | <span data-ttu-id="9eac0-111">다음에 연결...</span><span class="sxs-lookup"><span data-stu-id="9eac0-111">Connects to...</span></span> |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | <span data-ttu-id="9eac0-112">22</span><span class="sxs-lookup"><span data-stu-id="9eac0-112">22</span></span> | <span data-ttu-id="9eac0-113">에지 노드(HDInsight의 R Server)</span><span class="sxs-lookup"><span data-stu-id="9eac0-113">Edge node (R Server on HDInsight)</span></span> |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9eac0-114">22</span><span class="sxs-lookup"><span data-stu-id="9eac0-114">22</span></span> | <span data-ttu-id="9eac0-115">에지 노드(에지 노드가 있는 경우 다른 클러스터 형식)</span><span class="sxs-lookup"><span data-stu-id="9eac0-115">Edge node (any other cluster type, if an edge node exists)</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9eac0-116">22</span><span class="sxs-lookup"><span data-stu-id="9eac0-116">22</span></span> | <span data-ttu-id="9eac0-117">기본 헤드 노드</span><span class="sxs-lookup"><span data-stu-id="9eac0-117">Primary headnode</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9eac0-118">23</span><span class="sxs-lookup"><span data-stu-id="9eac0-118">23</span></span> | <span data-ttu-id="9eac0-119">보조 헤드 노드</span><span class="sxs-lookup"><span data-stu-id="9eac0-119">Secondary headnode</span></span> |

> [!NOTE]
> <span data-ttu-id="9eac0-120">`<edgenodename>`을 에지 노드의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-120">Replace `<edgenodename>` with the name of the edge node.</span></span>
>
> <span data-ttu-id="9eac0-121">`<clustername>`을 클러스터의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-121">Replace `<clustername>` with the name of your cluster.</span></span>
>
> <span data-ttu-id="9eac0-122">클러스터에 에지 노드가 있는 경우 __항상 SSH를 사용하여 에지 노드에 연결__하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-122">If your cluster contains an edge node, we recommend that you __always connect to the edge node__ using SSH.</span></span> <span data-ttu-id="9eac0-123">헤드 노드는 Hadoop의 상태에 중요한 서비스를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-123">The head nodes host services that are critical to the health of Hadoop.</span></span> <span data-ttu-id="9eac0-124">에지 노드는 배치한 내용을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-124">The edge node runs only what you put on it.</span></span>
>
> <span data-ttu-id="9eac0-125">에지 노드를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 에지 노드 사용](hdinsight-apps-use-edge-node.md#access-an-edge-node)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-125">For more information on using edge nodes, see [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span></span>

## <a name="ssh-clients"></a><span data-ttu-id="9eac0-126">SSH 클라이언트</span><span class="sxs-lookup"><span data-stu-id="9eac0-126">SSH clients</span></span>

<span data-ttu-id="9eac0-127">Linux, Unix 및 macOS 시스템은 `ssh` 및 `scp` 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-127">Linux, Unix, and macOS systems provide the `ssh` and `scp` commands.</span></span> <span data-ttu-id="9eac0-128">`ssh` 클라이언트는 일반적으로 Linux 또는 Unix 기반 시스템에서 원격 명령줄 세션을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-128">The `ssh` client is commonly used to create a remote command-line session with a Linux or Unix-based system.</span></span> <span data-ttu-id="9eac0-129">`scp` 클라이언트는 클라이언트와 원격 시스템 간에 파일을 안전하게 복사하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-129">The `scp` client is used to securely copy files between your client and the remote system.</span></span>

<span data-ttu-id="9eac0-130">Microsoft Windows는 기본적으로 SSH 클라이언트를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-130">Microsoft Windows does not provide any SSH clients by default.</span></span> <span data-ttu-id="9eac0-131">`ssh` 및 `scp` 클라이언트는 Windows에서 다음 패키지를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-131">The `ssh` and `scp` clients are available for Windows through the following packages:</span></span>

* <span data-ttu-id="9eac0-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): 브라우저에 Bash 환경을 제공하고 `ssh`, `scp` 및 기타 일반적인 Linux 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): The Cloud Shell provides a Bash environment in your browser, and provides the `ssh`, `scp`, and other common Linux commands.</span></span>

* <span data-ttu-id="9eac0-133">[Windows 10의 Ubuntu에 있는 Bash](https://msdn.microsoft.com/commandline/wsl/about)(영문): `ssh` 및 `scp` 명령은 Windows 명령줄에서 Bash를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-133">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about): The `ssh` and `scp` commands are available through the Bash on Windows command line.</span></span>

* <span data-ttu-id="9eac0-134">[Git(https://git-scm.com/)](https://git-scm.com/)(영문): `ssh` 및 `scp` 명령은 GitBash 명령줄을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-134">[Git (https://git-scm.com/)](https://git-scm.com/): The `ssh` and `scp` commands are available through the GitBash command line.</span></span>

* <span data-ttu-id="9eac0-135">[GitHub 데스크톱(https://desktop.github.com/)](https://desktop.github.com/)(영문): `ssh` 및 `scp` 명령은 GitHub 셸 명령줄을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) The `ssh` and `scp` commands are available through the GitHub Shell command line.</span></span> <span data-ttu-id="9eac0-136">GitHub 데스크탑은 Bash, Windows 명령 프롬프트 또는 PowerShell을 Git Shell의 명령줄로 사용하여 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-136">GitHub Desktop can be configured to use Bash, the Windows Command Prompt, or PowerShell as the command line for the Git Shell.</span></span>

* <span data-ttu-id="9eac0-137">[OpenSSH(https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): PowerShell 팀은 OpenSSH를 Windows에 이식하여 테스트 릴리스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): The PowerShell team is porting OpenSSH to Windows, and provides test releases.</span></span>

    > [!WARNING]
    > <span data-ttu-id="9eac0-138">OpenSSH 패키지는 SSH 서버 구성 요소 `sshd`를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-138">The OpenSSH package includes the SSH server component, `sshd`.</span></span> <span data-ttu-id="9eac0-139">이 구성 요소는 다른 사용자가 연결할 수 있도록 시스템에서 SSH 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-139">This component starts an SSH server on your system, allowing others to connect to it.</span></span> <span data-ttu-id="9eac0-140">시스템에서 SSH 서버를 호스트하려는 것이 아니라면 이 구성 요소를 구성하거나 포트 22를 열지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-140">Do not configure this component or open port 22 unless you want to host an SSH server on your system.</span></span> <span data-ttu-id="9eac0-141">HDInsight와 통신할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-141">It is not required to communicate with HDInsight.</span></span>

<span data-ttu-id="9eac0-142">[PuTTY(http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) 및 [MobaXterm(http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/)과 같은 몇 가지 그래픽 SSH 클라이언트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-142">There are also several graphical SSH clients, such as [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/).</span></span> <span data-ttu-id="9eac0-143">이러한 클라이언트를 사용하여 HDInsight에 연결할 수 있지만, 연결하는 프로세스는 `ssh` 유틸리티를 사용하는 것과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-143">While these clients can be used to connect to HDInsight, the process of connecting is different than using the `ssh` utility.</span></span> <span data-ttu-id="9eac0-144">자세한 내용은 사용하는 그래픽 클라이언트의 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-144">For more information, see the documentation of the graphical client you are using.</span></span>

## <span data-ttu-id="9eac0-145"><a id="sshkey"></a>인증: SSH 키</span><span class="sxs-lookup"><span data-stu-id="9eac0-145"><a id="sshkey"></a>Authentication: SSH Keys</span></span>

<span data-ttu-id="9eac0-146">SSH 키는 [공개 키 암호화](https://en.wikipedia.org/wiki/Public-key_cryptography)를 사용하여 SSH 세션을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-146">SSH keys use [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) to authenticate SSH sessions.</span></span> <span data-ttu-id="9eac0-147">SSH 키는 암호보다 더 안전하며, Hadoop 클러스터에 대한 액세스를 안전하게 보호하는 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-147">SSH keys are more secure than passwords, and provide an easy way to secure access to your Hadoop cluster.</span></span>

<span data-ttu-id="9eac0-148">키를 사용하여 SSH 계정을 보호한 경우 클라이언트는 연결할 때 일치하는 개인 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-148">If your SSH account is secured using a key, the client must provide the matching private key when you connect:</span></span>

* <span data-ttu-id="9eac0-149">대부분의 클라이언트는 __기본 키__를 사용하도록 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-149">Most clients can be configured to use a __default key__.</span></span> <span data-ttu-id="9eac0-150">예를 들어 `ssh` 클라이언트는 Linux 및 Unix 환경의 `~/.ssh/id_rsa`에서 개인 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-150">For example, the `ssh` client looks for a private key at `~/.ssh/id_rsa` on Linux and Unix environments.</span></span>

* <span data-ttu-id="9eac0-151">__개인 키에 대한 경로__를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-151">You can specify the __path to a private key__.</span></span> <span data-ttu-id="9eac0-152">`ssh` 클라이언트에서 `-i` 매개 변수를 사용하여 개인 키에 대한 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-152">With the `ssh` client, the `-i` parameter is used to specify the path to private key.</span></span> <span data-ttu-id="9eac0-153">예: `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9eac0-153">For example, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span></span>

* <span data-ttu-id="9eac0-154">서로 다른 서버에서 사용할 수 있는 __여러 개의 개인 키__가 있는 경우 [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent)와 같은 유틸리티를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-154">If you have __multiple private keys__ for use with different servers, consider using a utility such as [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent).</span></span> <span data-ttu-id="9eac0-155">`ssh-agent` 유틸리티를 사용하여 SSH 세션을 설정할 때 사용할 키를 자동으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-155">The `ssh-agent` utility can be used to automatically select the key to use when establishing an SSH session.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="9eac0-156">암호를 사용하여 개인 키를 보호하는 경우 키를 사용할 때 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-156">If you secure your private key with a passphrase, you must enter the passphrase when using the key.</span></span> <span data-ttu-id="9eac0-157">`ssh-agent`와 같은 유틸리티는 편의상 암호를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-157">Utilities such as `ssh-agent` can cache the password for your convenience.</span></span>

### <a name="create-an-ssh-key-pair"></a><span data-ttu-id="9eac0-158">SSH 키 쌍 만들기</span><span class="sxs-lookup"><span data-stu-id="9eac0-158">Create an SSH key pair</span></span>

<span data-ttu-id="9eac0-159">`ssh-keygen` 명령을 사용하여 공용 및 개인 키 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-159">Use the `ssh-keygen` command to create public and private key files.</span></span> <span data-ttu-id="9eac0-160">다음 명령은 HDInsight와 함께 사용할 수 있는 2048비트 RSA 키 쌍을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-160">The following command generates a 2048-bit RSA key pair that can be used with HDInsight:</span></span>

    ssh-keygen -t rsa -b 2048

<span data-ttu-id="9eac0-161">키 생성 프로세스 중에 정보를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-161">You are prompted for information during the key creation process.</span></span> <span data-ttu-id="9eac0-162">예를 들어, 키가 저장되는 위치 또는 암호를 사용할지 여부를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-162">For example, where the keys are stored or whether to use a passphrase.</span></span> <span data-ttu-id="9eac0-163">프로세스가 완료된 후에 공개 키와 개인 키라는 두 개의 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-163">After the process completes, two files are created; a public key and a private key.</span></span>

* <span data-ttu-id="9eac0-164">__공개 키__는 HDInsight 클러스터를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-164">The __public key__ is used to create an HDInsight cluster.</span></span> <span data-ttu-id="9eac0-165">공개 키의 확장명은 `.pub`입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-165">The public key has an extension of `.pub`.</span></span>

* <span data-ttu-id="9eac0-166">__개인 키__는 HDInsight 클러스터에 클라이언트를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-166">The __private key__ is used to authenticate your client to the HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9eac0-167">암호를 사용하여 키를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-167">You can secure your keys using a passphrase.</span></span> <span data-ttu-id="9eac0-168">암호는 사실상 개인 키의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-168">A passphrase is effectively a password on your private key.</span></span> <span data-ttu-id="9eac0-169">누군가 사용자의 개인 키를 얻게 되더라도 키를 사용하기 위해 암호가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-169">Even if someone obtains your private key, they must have the passphrase to use the key.</span></span>

### <a name="create-hdinsight-using-the-public-key"></a><span data-ttu-id="9eac0-170">공용 키를 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="9eac0-170">Create HDInsight using the public key</span></span>

| <span data-ttu-id="9eac0-171">생성 방법</span><span class="sxs-lookup"><span data-stu-id="9eac0-171">Creation method</span></span> | <span data-ttu-id="9eac0-172">공개 키를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9eac0-172">How to use the public key</span></span> |
| ------- | ------- |
| <span data-ttu-id="9eac0-173">**Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="9eac0-173">**Azure portal**</span></span> | <span data-ttu-id="9eac0-174">__클러스터 로그인으로 동일한 암호 사용__의 선택을 취소한 다음 __공개 키__를 SSH 인증 유형으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-174">Uncheck __Use same password as cluster login__, and then select __Public Key__ as the SSH authentication type.</span></span> <span data-ttu-id="9eac0-175">마지막으로 공개 키 파일을 선택하거나 __SSH 공개 키__ 필드에 파일의 텍스트 내용을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-175">Finally, select the public key file or paste the text contents of the file in the __SSH public key__ field.</span></span></br><span data-ttu-id="9eac0-176">![HDInsight 클러스터 생성의 SSH 공개 키 대화 상자](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span><span class="sxs-lookup"><span data-stu-id="9eac0-176">![SSH public key dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span></span> |
| <span data-ttu-id="9eac0-177">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9eac0-177">**Azure PowerShell**</span></span> | <span data-ttu-id="9eac0-178">`New-AzureRmHdinsightCluster` cmdlet의 `-SshPublicKey` 매개 변수를 사용하여 공개 키의 내용을 문자열로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-178">Use the `-SshPublicKey` parameter of the `New-AzureRmHdinsightCluster` cmdlet and pass the contents of the public key as a string.</span></span>|
| <span data-ttu-id="9eac0-179">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="9eac0-179">**Azure CLI 1.0**</span></span> | <span data-ttu-id="9eac0-180">`azure hdinsight cluster create` 명령의 `--sshPublicKey` 매개 변수를 사용하여 공개 키의 내용을 문자열로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-180">Use the `--sshPublicKey` parameter of the `azure hdinsight cluster create` command and pass the contents of the public key as a string.</span></span> |
| <span data-ttu-id="9eac0-181">**Resource Manager 템플릿**</span><span class="sxs-lookup"><span data-stu-id="9eac0-181">**Resource Manager Template**</span></span> | <span data-ttu-id="9eac0-182">템플릿에서 SSH 키를 사용하는 예제는 [SSH 키를 사용하여 Linux에서 HDInsight 배포](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-182">For an example of using SSH keys with a template, see [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span></span> <span data-ttu-id="9eac0-183">[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) 파일의 `publicKeys` 요소는 클러스터를 만들 때 Azure에 키를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-183">The `publicKeys` element in the [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) file is used to pass the keys to Azure when creating the cluster.</span></span> |

## <span data-ttu-id="9eac0-184"><a id="sshpassword"></a>인증: 암호</span><span class="sxs-lookup"><span data-stu-id="9eac0-184"><a id="sshpassword"></a>Authentication: Password</span></span>

<span data-ttu-id="9eac0-185">SSH 계정은 암호를 사용하여 보호될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-185">SSH accounts can be secured using a password.</span></span> <span data-ttu-id="9eac0-186">SSH를 사용하여 HDInsight에 연결할 경우 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-186">When you connect to HDInsight using SSH, you are prompted to enter the password.</span></span>

> [!WARNING]
> <span data-ttu-id="9eac0-187">SSH에 대한 암호 인증을 사용하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-187">We do not recommend using password authentication for SSH.</span></span> <span data-ttu-id="9eac0-188">암호는 추측할 수 있고 무차별 암호 대입 공격에 취약합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-188">Passwords can be guessed and are vulnerable to brute force attacks.</span></span> <span data-ttu-id="9eac0-189">대신 [인증하기 위한 SSH 키](#sshkey)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-189">Instead, we recommend that you use [SSH keys for authentication](#sshkey).</span></span>

### <a name="create-hdinsight-using-a-password"></a><span data-ttu-id="9eac0-190">암호를 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="9eac0-190">Create HDInsight using a password</span></span>

| <span data-ttu-id="9eac0-191">생성 방법</span><span class="sxs-lookup"><span data-stu-id="9eac0-191">Creation method</span></span> | <span data-ttu-id="9eac0-192">암호를 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="9eac0-192">How to specify the password</span></span> |
| --------------- | ---------------- |
| <span data-ttu-id="9eac0-193">**Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="9eac0-193">**Azure portal**</span></span> | <span data-ttu-id="9eac0-194">기본적으로 SSH 사용자 계정에는 클러스터 로그인 계정인 동일한 암호가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-194">By default, the SSH user account has the same password as the cluster login account.</span></span> <span data-ttu-id="9eac0-195">다른 암호를 사용하려면 __클러스터 로그인으로 동일한 암호 사용__의 선택을 취소한 다음 __SSH 암호__ 필드에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-195">To use a different password, uncheck __Use same password as cluster login__, and then enter the password in the __SSH password__ field.</span></span></br><span data-ttu-id="9eac0-196">![HDInsight 클러스터 생성의 SSH 암호 대화 상자](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span><span class="sxs-lookup"><span data-stu-id="9eac0-196">![SSH password dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span></span>|
| <span data-ttu-id="9eac0-197">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9eac0-197">**Azure PowerShell**</span></span> | <span data-ttu-id="9eac0-198">`New-AzureRmHdinsightCluster` cmdlet의 `--SshCredential` 매개 변수를 사용하고 SSH 사용자 계정 이름 및 암호를 포함하는 `PSCredential` 개체를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-198">Use the `--SshCredential` parameter of the `New-AzureRmHdinsightCluster` cmdlet and pass a `PSCredential` object that contains the SSH user account name and password.</span></span> |
| <span data-ttu-id="9eac0-199">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="9eac0-199">**Azure CLI 1.0**</span></span> | <span data-ttu-id="9eac0-200">`azure hdinsight cluster create` 명령의 `--sshPassword` 매개 변수를 사용하여 암호 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-200">Use the `--sshPassword` parameter of the `azure hdinsight cluster create` command and provide the password value.</span></span> |
| <span data-ttu-id="9eac0-201">**Resource Manager 템플릿**</span><span class="sxs-lookup"><span data-stu-id="9eac0-201">**Resource Manager Template**</span></span> | <span data-ttu-id="9eac0-202">템플릿에서 암호를 사용하는 예제는 [SSH 암호를 사용하여 Linux에서 HDInsight 배포](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-202">For an example of using a password with a template, see [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> <span data-ttu-id="9eac0-203">[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) 파일의 `linuxOperatingSystemProfile` 요소는 클러스터를 만들 때 Azure에 SSH 계정 이름 및 암호를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-203">The `linuxOperatingSystemProfile` element in the [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) file is used to pass the SSH account name and password to Azure when creating the cluster.</span></span>|

### <a name="change-the-ssh-password"></a><span data-ttu-id="9eac0-204">SSH 암호 변경</span><span class="sxs-lookup"><span data-stu-id="9eac0-204">Change the SSH password</span></span>

<span data-ttu-id="9eac0-205">SSH 사용자 계정 암호를 변경하는 방법에 대한 내용은 [HDInsight 관리](hdinsight-administer-use-portal-linux.md#change-passwords) 문서의 __암호 변경__ 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-205">For information on changing the SSH user account password, see the __Change passwords__ section of the [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) document.</span></span>

## <span data-ttu-id="9eac0-206"><a id="domainjoined"></a>인증: 도메인에 조인된 HDInsight</span><span class="sxs-lookup"><span data-stu-id="9eac0-206"><a id="domainjoined"></a>Authentication: Domain-joined HDInsight</span></span>

<span data-ttu-id="9eac0-207">__도메인에 조인된 HDInsight 클러스터__를 사용하는 경우 SSH와 연결한 후에 `kinit` 명령을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-207">If you are using a __domain-joined HDInsight cluster__, you must use the `kinit` command after connecting with SSH.</span></span> <span data-ttu-id="9eac0-208">이 명령은 도메인 사용자 및 암호를 묻는 메시지를 표시하고 클러스터와 연결된 Azure Active Directory 도메인을 사용하여 세션을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-208">This command prompts you for a domain user and password, and authenticates your session with the Azure Active Directory domain associated with the cluster.</span></span>

<span data-ttu-id="9eac0-209">자세한 내용은 [도메인에 조인된 HDInsight 구성](hdinsight-domain-joined-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-209">For more information, see [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md).</span></span>

## <a name="connect-to-nodes"></a><span data-ttu-id="9eac0-210">노드에 연결</span><span class="sxs-lookup"><span data-stu-id="9eac0-210">Connect to nodes</span></span>

<span data-ttu-id="9eac0-211">헤드 노드 및 에지 노드(있는 경우)는 인터넷을 통해 포트 22 및 23에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-211">The head nodes and edge node (if there is one) can be accessed over the internet on ports 22 and 23.</span></span>

* <span data-ttu-id="9eac0-212">__헤드 노드__에 연결할 경우 기본 헤드 노드에 연결하려면 __22__ 포트, 보조 헤드 노드에 연결하려면 __23__ 포트를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-212">When connecting to the __head nodes__, use port __22__ to connect to the primary head node and port __23__ to connect to the secondary head node.</span></span> <span data-ttu-id="9eac0-213">사용할 정규화된 도메인 이름은 `clustername-ssh.azurehdinsight.net`이며, 여기서 `clustername`은 사용자의 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-213">The fully qualified domain name to use is `clustername-ssh.azurehdinsight.net`, where `clustername` is the name of your cluster.</span></span>

    ```bash
    # Connect to primary head node
    # port not specified since 22 is the default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect to secondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* <span data-ttu-id="9eac0-214">__에지 노드__에 연결할 때는 포트 22를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-214">When connectiung to the __edge node__, use port 22.</span></span> <span data-ttu-id="9eac0-215">정규화된 도메인 이름은 `edgenodename.clustername-ssh.azurehdinsight.net`이며, 여기서 `edgenodename`은 에지 노드 연결 시 사용자가 제공한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-215">The fully qualified domain name is `edgenodename.clustername-ssh.azurehdinsight.net`, where `edgenodename` is a name you provided when creating the edge node.</span></span> <span data-ttu-id="9eac0-216">`clustername`은 클러스터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-216">`clustername` is the name of the cluster.</span></span>

    ```bash
    # Connect to edge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> <span data-ttu-id="9eac0-217">이전 예에서는 암호 인증을 사용하고 있고 인증서 인증이 자동으로 발생하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-217">The previous examples assume that you are using password authentication, or that certificate authentication is occuring automatically.</span></span> <span data-ttu-id="9eac0-218">인증에 SSH 키 쌍을 사용하고 인증서가 자동으로 사용되지 않을 경우 `-i` 매개 변수를 사용하여 개인 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-218">If you use an SSH key-pair for authentication, and the certificate is not used automatically, use the `-i` parameter to specify the private key.</span></span> <span data-ttu-id="9eac0-219">예: `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9eac0-219">For example, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span></span>

<span data-ttu-id="9eac0-220">연결되면 프롬프트가 변경되어 SSH 사용자 이름과 사용자가 연결된 노드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-220">Once connected, the prompt changes to indicate the SSH user name and the node you are connected to.</span></span> <span data-ttu-id="9eac0-221">예를 들어, `sshuser`로 기본 헤드 노드에 연결된 경우 프롬프트는 `sshuser@hn0-clustername:~$`입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-221">For example, when connected to the primary head node as `sshuser`, the prompt is `sshuser@hn0-clustername:~$`.</span></span>

### <a name="connect-to-worker-and-zookeeper-nodes"></a><span data-ttu-id="9eac0-222">작업자 및 Zookeeper 노드에 연결</span><span class="sxs-lookup"><span data-stu-id="9eac0-222">Connect to worker and Zookeeper nodes</span></span>

<span data-ttu-id="9eac0-223">작업자 노드와 Zookeeper 노드는 인터넷에서 직접 액세스할 수 없으며,</span><span class="sxs-lookup"><span data-stu-id="9eac0-223">The worker nodes and Zookeeper nodes are not directly accessible from the internet.</span></span> <span data-ttu-id="9eac0-224">클러스터 헤드 노드 또는 에지 노드에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-224">They can be accessed from the cluster head nodes or edge nodes.</span></span> <span data-ttu-id="9eac0-225">다음은 다른 노드에 연결하는 일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-225">The following are the general steps to connect to other nodes:</span></span>

1. <span data-ttu-id="9eac0-226">SSH를 사용하여 헤드 또는 가장자리 노드에 연결:</span><span class="sxs-lookup"><span data-stu-id="9eac0-226">Use SSH to connect to a head or edge node:</span></span>

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. <span data-ttu-id="9eac0-227">헤드 또는 가장자리 노드에 대한 SSH 연결에서는 `ssh` 명령을 사용하여 클러스터의 작업자 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-227">From the SSH connection to the head or edge node, use the `ssh` command to connect to a worker node in the cluster:</span></span>

        ssh sshuser@wn0-myhdi

    <span data-ttu-id="9eac0-228">클러스터에 있는 노드의 도메인 이름 목록을 검색하려면 [Ambari REST API를 사용하여 HDInsight 관리](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-228">To retrieve a list of the domain names of the nodes in the cluster, see the [Manage HDInsight by using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span></span>

<span data-ttu-id="9eac0-229">__암호__를 사용하여 SSH 계정을 보호하는 경우 연결할 때 해당 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-229">If the SSH account is secured using a __password__, enter the password when connecting.</span></span>

<span data-ttu-id="9eac0-230">__SSH 키__를 사용하여 SSH 계정을 보호하는 경우 SSH 전달이 클라이언트에서 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-230">If the SSH account is secured using __SSH keys__, make sure that SSH forwarding is enabled on the client.</span></span>

> [!NOTE]
> <span data-ttu-id="9eac0-231">클러스터에서 모든 노드에 직접 액세스하는 다른 방법은 Azure Virtual Network에 HDInsight를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-231">Another way to directly access all nodes in the cluster is to install HDInsight into an Azure Virtual Network.</span></span> <span data-ttu-id="9eac0-232">그런 다음 동일한 가상 네트워크에 원격 컴퓨터를 조인하고 클러스터에 있는 모든 노드에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-232">Then, you can join your remote machine to the same virtual network and directly access all nodes in the cluster.</span></span>
>
> <span data-ttu-id="9eac0-233">자세한 내용은 [HDInsight와 함께 가상 네트워크 사용](hdinsight-extend-hadoop-virtual-network.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9eac0-233">For more information, see [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md).</span></span>

### <a name="configure-ssh-agent-forwarding"></a><span data-ttu-id="9eac0-234">SSH 에이전트 전달 구성</span><span class="sxs-lookup"><span data-stu-id="9eac0-234">Configure SSH agent forwarding</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9eac0-235">다음 단계에서는 Linux 또는 UNIX 기반 시스템이며 Windows 10의 Bash를 통해 작업한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-235">The following steps assume a Linux or UNIX-based system, and work with Bash on Windows 10.</span></span> <span data-ttu-id="9eac0-236">이 단계가 시스템에서 작동하지 않는다면 해당 SSH 클라이언트에 대한 설명서를 참조해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-236">If these steps do not work for your system, you may need to consult the documentation for your SSH client.</span></span>

1. <span data-ttu-id="9eac0-237">텍스트 편집기를 사용하여 `~/.ssh/config`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-237">Using a text editor, open `~/.ssh/config`.</span></span> <span data-ttu-id="9eac0-238">이 파일이 존재하지 않으면 명령줄에 `touch ~/.ssh/config`를 입력하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-238">If this file doesn't exist, you can create it by entering `touch ~/.ssh/config` at a command line.</span></span>

2. <span data-ttu-id="9eac0-239">`config` 파일에 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-239">Add the following text to the `config` file.</span></span>

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    <span data-ttu-id="9eac0-240">__호스트__ 정보를 SSH를 사용하여 연결한 노드의 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-240">Replace the __Host__ information with the address of the node you connect to using SSH.</span></span> <span data-ttu-id="9eac0-241">이전 예제에서는 에지 노드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-241">The previous example uses the edge node.</span></span> <span data-ttu-id="9eac0-242">이 항목은 지정된 노드에 대한 SSH 에이전트 전달을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-242">This entry configures SSH agent forwarding for the specified node.</span></span>

3. <span data-ttu-id="9eac0-243">터미널에서 다음 명령을 사용하여 SSH 에이전트 전달을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-243">Test SSH agent forwarding by using the following command from the terminal:</span></span>

        echo "$SSH_AUTH_SOCK"

    <span data-ttu-id="9eac0-244">이 명령은 다음 텍스트와 유사한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-244">This command returns information similar to the following text:</span></span>

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    <span data-ttu-id="9eac0-245">아무 것도 반환되지 않으면 `ssh-agent`가 실행되지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-245">If nothing is returned, then `ssh-agent` is not running.</span></span> <span data-ttu-id="9eac0-246">자세한 내용은 [ssh에서 ssh-agent 사용(http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh)(영문)의 에이전트 시작 스크립트 또는 SSH 클라이언트 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-246">For more information, see the agent startup scripts information at [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) or consult your SSH client documentation.</span></span>

4. <span data-ttu-id="9eac0-247">**ssh-agent**가 실행 중인지 확인한 후에는 다음을 사용하여 SSH 개인 키를 에이전트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-247">Once you have verified that **ssh-agent** is running, use the following to add your SSH private key to the agent:</span></span>

        ssh-add ~/.ssh/id_rsa

    <span data-ttu-id="9eac0-248">개인 키가 다른 파일에 저장된 경우 `~/.ssh/id_rsa`를 해당 파일의 경로로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-248">If your private key is stored in a different file, replace `~/.ssh/id_rsa` with the path to the file.</span></span>

5. <span data-ttu-id="9eac0-249">SSH를 사용하여 클러스터 에지 노드 또는 헤드 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-249">Connect to the cluster edge node or head nodes using SSH.</span></span> <span data-ttu-id="9eac0-250">SSH 명령을 사용하여 작업자 또는 zookeeper 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-250">Then use the SSH command to connect to a worker or zookeeper node.</span></span> <span data-ttu-id="9eac0-251">전달된 키를 사용하여 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-251">The connection is established using the forwarded key.</span></span>

## <a name="copy-files"></a><span data-ttu-id="9eac0-252">파일 복사</span><span class="sxs-lookup"><span data-stu-id="9eac0-252">Copy files</span></span>

<span data-ttu-id="9eac0-253">`scp` 유틸리티를 사용하면 클러스터의 개별 노드로 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-253">The `scp` utility can be used to copy files to and from individual nodes in the cluster.</span></span> <span data-ttu-id="9eac0-254">예를 들어 다음 명령은 로컬 시스템의 `test.txt` 디렉터리를 기본 헤드 노드로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-254">For example, the following command copies the `test.txt` directory from the local system to the primary head node:</span></span>

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

<span data-ttu-id="9eac0-255">`:` 다음에 지정된 경로가 없으므로 파일은 `sshuser` 홈 디렉터리에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-255">Since no path is specified after the `:`, the file is placed in the `sshuser` home directory.</span></span>

<span data-ttu-id="9eac0-256">다음 예제에서는 `test.txt` 파일을 기본 헤드 노드의 `sshuser` 홈 디렉터리에서 로컬 시스템으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-256">The following example copies the `test.txt` file from the `sshuser` home directory on the primary head node to the local system:</span></span>

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> <span data-ttu-id="9eac0-257">`scp`는 클러스터 내 개별 노드의 파일 시스템에만 액세스할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="9eac0-257">`scp` can only access the file system of individual nodes within the cluster.</span></span> <span data-ttu-id="9eac0-258">해당 클러스터에 대한 HDFS 호환 저장소의 데이터 액세스에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-258">It cannot be used to access data in the HDFS-compatible storage for the cluster.</span></span>
>
> <span data-ttu-id="9eac0-259">SSH 세션에서 사용할 리소스를 업로드해야 할 때 `scp`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-259">Use `scp` when you need to upload a resource for use from an SSH session.</span></span> <span data-ttu-id="9eac0-260">예를 들어 Python 스크립트를 업로드한 다음 SSH 세션에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9eac0-260">For example, upload a Python script and then run the script from an SSH session.</span></span>
>
> <span data-ttu-id="9eac0-261">HDFS 호환 저장소로 데이터 직접 로드에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9eac0-261">For information on directly loading data into the HDFS-compatible storage, see the following documents:</span></span>
>
> * <span data-ttu-id="9eac0-262">[Azure Storage를 사용하는 HDInsight](hdinsight-hadoop-use-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="9eac0-262">[HDInsight using Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span>
>
> * <span data-ttu-id="9eac0-263">[Azure Data Lake Store를 사용하는 HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="9eac0-263">[HDInsight using Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9eac0-264">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9eac0-264">Next steps</span></span>

* [<span data-ttu-id="9eac0-265">HDInsight와 함께 SSH 터널링 사용</span><span class="sxs-lookup"><span data-stu-id="9eac0-265">Use SSH tunneling with HDInsight</span></span>](hdinsight-linux-ambari-ssh-tunnel.md)
* [<span data-ttu-id="9eac0-266">HDInsight와 함께 가상 네트워크 사용</span><span class="sxs-lookup"><span data-stu-id="9eac0-266">Use a virtual network with HDInsight</span></span>](hdinsight-extend-hadoop-virtual-network.md)
* [<span data-ttu-id="9eac0-267">HDInsight에서 에지 노드 사용</span><span class="sxs-lookup"><span data-stu-id="9eac0-267">Use edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md#access-an-edge-node)