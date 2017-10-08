---
title: "Azure HDInsight에서 Hadoop으로 SSH aaaUse | Microsoft Docs"
description: "SSH(보안 셸)를 사용하여 HDInsight에 액세스할 수 있습니다. 이 문서에서는 Windows, Linux, Unix, 또는 macOS 클라이언트에서 사용 하 여 hello ssh tooHDInsight scp 명령과 연결 설명 합니다."
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
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a><span data-ttu-id="9c076-105">TooHDInsight (Hadoop) SSH를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="9c076-105">Connect tooHDInsight (Hadoop) using SSH</span></span>

<span data-ttu-id="9c076-106">자세한 내용은 방법 toouse [SSH (보안 셸)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely tooHadoop Azure HDInsight에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-106">Learn how toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely connect tooHadoop on Azure HDInsight.</span></span> 

<span data-ttu-id="9c076-107">HDInsight은 hello Hadoop 클러스터 내에서 노드에 대 한 hello 운영 체제로 Linux (Ubuntu)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-107">HDInsight can use Linux (Ubuntu) as hello operating system for nodes within hello Hadoop cluster.</span></span> <span data-ttu-id="9c076-108">hello 다음 표에서 tooLinux 기반 HDInsight SSH 클라이언트를 사용 하 여 연결할 때 필요한 hello 주소와 포트 정보.</span><span class="sxs-lookup"><span data-stu-id="9c076-108">hello following table contains hello address and port information needed when connecting tooLinux-based HDInsight using an SSH client:</span></span>

| <span data-ttu-id="9c076-109">주소</span><span class="sxs-lookup"><span data-stu-id="9c076-109">Address</span></span> | <span data-ttu-id="9c076-110">포트</span><span class="sxs-lookup"><span data-stu-id="9c076-110">Port</span></span> | <span data-ttu-id="9c076-111">다음에 연결...</span><span class="sxs-lookup"><span data-stu-id="9c076-111">Connects to...</span></span> |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | <span data-ttu-id="9c076-112">22</span><span class="sxs-lookup"><span data-stu-id="9c076-112">22</span></span> | <span data-ttu-id="9c076-113">에지 노드(HDInsight의 R Server)</span><span class="sxs-lookup"><span data-stu-id="9c076-113">Edge node (R Server on HDInsight)</span></span> |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9c076-114">22</span><span class="sxs-lookup"><span data-stu-id="9c076-114">22</span></span> | <span data-ttu-id="9c076-115">에지 노드(에지 노드가 있는 경우 다른 클러스터 형식)</span><span class="sxs-lookup"><span data-stu-id="9c076-115">Edge node (any other cluster type, if an edge node exists)</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9c076-116">22</span><span class="sxs-lookup"><span data-stu-id="9c076-116">22</span></span> | <span data-ttu-id="9c076-117">기본 헤드 노드</span><span class="sxs-lookup"><span data-stu-id="9c076-117">Primary headnode</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="9c076-118">23</span><span class="sxs-lookup"><span data-stu-id="9c076-118">23</span></span> | <span data-ttu-id="9c076-119">보조 헤드 노드</span><span class="sxs-lookup"><span data-stu-id="9c076-119">Secondary headnode</span></span> |

> [!NOTE]
> <span data-ttu-id="9c076-120">대체 `<edgenodename>` hello hello 가장자리 노드 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-120">Replace `<edgenodename>` with hello name of hello edge node.</span></span>
>
> <span data-ttu-id="9c076-121">대체 `<clustername>` 클러스터의 hello 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-121">Replace `<clustername>` with hello name of your cluster.</span></span>
>
> <span data-ttu-id="9c076-122">좋습니다 가장자리 노드 클러스터에 있으면, 있습니다 __toohello 가장자리 노드는 항상 연결__ SSH를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-122">If your cluster contains an edge node, we recommend that you __always connect toohello edge node__ using SSH.</span></span> <span data-ttu-id="9c076-123">hello 헤드 노드는 Hadoop의 중요 한 toohello 상태 있는 서비스를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-123">hello head nodes host services that are critical toohello health of Hadoop.</span></span> <span data-ttu-id="9c076-124">hello 가장자리 노드에 보관할 내용은 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-124">hello edge node runs only what you put on it.</span></span>
>
> <span data-ttu-id="9c076-125">에지 노드를 사용하는 방법에 대한 자세한 내용은 [HDInsight에서 에지 노드 사용](hdinsight-apps-use-edge-node.md#access-an-edge-node)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c076-125">For more information on using edge nodes, see [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span></span>

## <a name="ssh-clients"></a><span data-ttu-id="9c076-126">SSH 클라이언트</span><span class="sxs-lookup"><span data-stu-id="9c076-126">SSH clients</span></span>

<span data-ttu-id="9c076-127">Linux, Unix 및 macOS 시스템 제공 hello `ssh` 및 `scp` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-127">Linux, Unix, and macOS systems provide hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="9c076-128">hello `ssh` 클라이언트는 자주 사용 되는 toocreate 원격 명령줄 세션 Linux 또는 Unix 기반 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-128">hello `ssh` client is commonly used toocreate a remote command-line session with a Linux or Unix-based system.</span></span> <span data-ttu-id="9c076-129">hello `scp` 클라이언트는 클라이언트와 hello 원격 시스템 간에 사용 되는 toosecurely 복사본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-129">hello `scp` client is used toosecurely copy files between your client and hello remote system.</span></span>

<span data-ttu-id="9c076-130">Microsoft Windows는 기본적으로 SSH 클라이언트를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-130">Microsoft Windows does not provide any SSH clients by default.</span></span> <span data-ttu-id="9c076-131">hello `ssh` 및 `scp` 클라이언트는 패키지를 다음 hello를 통해 Windows에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-131">hello `ssh` and `scp` clients are available for Windows through hello following packages:</span></span>

* <span data-ttu-id="9c076-132">[Azure 클라우드 셸](../cloud-shell/quickstart.md): 브라우저에서 Bash 환경을 제공 하 고 hello를 제공 하는 hello 클라우드 셸 `ssh`, `scp`, 및 기타 공통 Linux 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): hello Cloud Shell provides a Bash environment in your browser, and provides hello `ssh`, `scp`, and other common Linux commands.</span></span>

* <span data-ttu-id="9c076-133">[Windows 10에서 Ubuntu를 이용한 적](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` 및 `scp` Windows 명령줄에서 Bash hello를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-133">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` and `scp` commands are available through hello Bash on Windows command line.</span></span>

* <span data-ttu-id="9c076-134">[Git (https://git-scm.com/)](https://git-scm.com/): hello `ssh` 및 `scp` hello GitBash 명령줄을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-134">[Git (https://git-scm.com/)](https://git-scm.com/): hello `ssh` and `scp` commands are available through hello GitBash command line.</span></span>

* <span data-ttu-id="9c076-135">[GitHub 데스크톱 (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` 및 `scp` hello GitHub 셸의 명령줄을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` and `scp` commands are available through hello GitHub Shell command line.</span></span> <span data-ttu-id="9c076-136">GitHub 데스크톱 Git 셸 hello에 대 한 hello 명령줄으로 구성 된 toouse Bash, hello Windows 명령 프롬프트에서 또는 PowerShell을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-136">GitHub Desktop can be configured toouse Bash, hello Windows Command Prompt, or PowerShell as hello command line for hello Git Shell.</span></span>

* <span data-ttu-id="9c076-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell 팀 OpenSSH tooWindows 이식 되 고 테스트 릴리스에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell team is porting OpenSSH tooWindows, and provides test releases.</span></span>

    > [!WARNING]
    > <span data-ttu-id="9c076-138">hello SSH 서버 구성 요소를 포함 하는 hello OpenSSH 패키지 `sshd`합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-138">hello OpenSSH package includes hello SSH server component, `sshd`.</span></span> <span data-ttu-id="9c076-139">이 구성 요소는 다른 사람들이 시스템에 SSH 서버를 시작 tooconnect tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-139">This component starts an SSH server on your system, allowing others tooconnect tooit.</span></span> <span data-ttu-id="9c076-140">시스템에서 toohost SSH 서버를 원하는 경우 포트 22를 열지 하거나이 구성 요소를 구성 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9c076-140">Do not configure this component or open port 22 unless you want toohost an SSH server on your system.</span></span> <span data-ttu-id="9c076-141">HDInsight와 필요한 toocommunicate 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-141">It is not required toocommunicate with HDInsight.</span></span>

<span data-ttu-id="9c076-142">[PuTTY(http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) 및 [MobaXterm(http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/)과 같은 몇 가지 그래픽 SSH 클라이언트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-142">There are also several graphical SSH clients, such as [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/).</span></span> <span data-ttu-id="9c076-143">이러한 클라이언트에 사용 되는 tooconnect tooHDInsight 수 있지만, 연결 하는 hello 프로세스 hello를 사용 하 여 보다 차이가 `ssh` 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-143">While these clients can be used tooconnect tooHDInsight, hello process of connecting is different than using hello `ssh` utility.</span></span> <span data-ttu-id="9c076-144">자세한 내용은 사용 중인 hello 그래픽 클라이언트 hello 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9c076-144">For more information, see hello documentation of hello graphical client you are using.</span></span>

## <span data-ttu-id="9c076-145"><a id="sshkey"></a>인증: SSH 키</span><span class="sxs-lookup"><span data-stu-id="9c076-145"><a id="sshkey"></a>Authentication: SSH Keys</span></span>

<span data-ttu-id="9c076-146">SSH 키는 사용 하 여 [공개 키 암호화](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-146">SSH keys use [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH sessions.</span></span> <span data-ttu-id="9c076-147">SSH 키 암호 보다 더 안전 하 고 쉽게 toosecure 액세스 tooyour Hadoop 클러스터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-147">SSH keys are more secure than passwords, and provide an easy way toosecure access tooyour Hadoop cluster.</span></span>

<span data-ttu-id="9c076-148">SSH 계정 키를 사용 하 여 보호를 연결 하는 경우 개인 키와 일치 하는 hello hello 클라이언트에 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-148">If your SSH account is secured using a key, hello client must provide hello matching private key when you connect:</span></span>

* <span data-ttu-id="9c076-149">대부분의 클라이언트 구성된 toouse 수는 __기본 키__합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-149">Most clients can be configured toouse a __default key__.</span></span> <span data-ttu-id="9c076-150">예를 들어 hello `ssh` 에 개인 키에 대 한 클라이언트 찾습니다 `~/.ssh/id_rsa` 에서 Linux 및 Unix 환경에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-150">For example, hello `ssh` client looks for a private key at `~/.ssh/id_rsa` on Linux and Unix environments.</span></span>

* <span data-ttu-id="9c076-151">Hello를 지정할 수 있습니다 __경로 tooa 개인 키__합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-151">You can specify hello __path tooa private key__.</span></span> <span data-ttu-id="9c076-152">Hello로 `ssh` client, 안녕하세요 `-i` 매개 변수는 사용 되는 toospecify hello 경로 tooprivate 키입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-152">With hello `ssh` client, hello `-i` parameter is used toospecify hello path tooprivate key.</span></span> <span data-ttu-id="9c076-153">예: `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9c076-153">For example, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span></span>

* <span data-ttu-id="9c076-154">서로 다른 서버에서 사용할 수 있는 __여러 개의 개인 키__가 있는 경우 [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent)와 같은 유틸리티를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-154">If you have __multiple private keys__ for use with different servers, consider using a utility such as [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent).</span></span> <span data-ttu-id="9c076-155">hello `ssh-agent` 유틸리티 대 한 SSH 세션을 설정할 때 사용 되는 tooautomatically 선택 hello 키 toouse 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-155">hello `ssh-agent` utility can be used tooautomatically select hello key toouse when establishing an SSH session.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="9c076-156">암호와 개인 키를 보호 하는 경우에 hello 키를 사용할 때 hello 암호를 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-156">If you secure your private key with a passphrase, you must enter hello passphrase when using hello key.</span></span> <span data-ttu-id="9c076-157">와 같은 유틸리티 `ssh-agent` 편의 위해 hello 암호를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-157">Utilities such as `ssh-agent` can cache hello password for your convenience.</span></span>

### <a name="create-an-ssh-key-pair"></a><span data-ttu-id="9c076-158">SSH 키 쌍 만들기</span><span class="sxs-lookup"><span data-stu-id="9c076-158">Create an SSH key pair</span></span>

<span data-ttu-id="9c076-159">사용 하 여 hello `ssh-keygen` 명령 toocreate 공용 및 개인 키 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-159">Use hello `ssh-keygen` command toocreate public and private key files.</span></span> <span data-ttu-id="9c076-160">hello 다음 명령은 생성 HDInsight와 사용할 수 있는 2048 비트 RSA 키 쌍:</span><span class="sxs-lookup"><span data-stu-id="9c076-160">hello following command generates a 2048-bit RSA key pair that can be used with HDInsight:</span></span>

    ssh-keygen -t rsa -b 2048

<span data-ttu-id="9c076-161">Hello 키 생성 프로세스 중에 정보를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-161">You are prompted for information during hello key creation process.</span></span> <span data-ttu-id="9c076-162">예를 들어 hello 키 저장 되는 위치 또는 여부 toouse 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-162">For example, where hello keys are stored or whether toouse a passphrase.</span></span> <span data-ttu-id="9c076-163">Hello 프로세스를 완료 한 후에 두 개의 파일이 만들어집니다. 공개 키와 개인 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-163">After hello process completes, two files are created; a public key and a private key.</span></span>

* <span data-ttu-id="9c076-164">hello __공개 키__ toocreate 사용 되는 HDInsight 클러스터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-164">hello __public key__ is used toocreate an HDInsight cluster.</span></span> <span data-ttu-id="9c076-165">hello 공개 키의 확장명은 `.pub`합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-165">hello public key has an extension of `.pub`.</span></span>

* <span data-ttu-id="9c076-166">hello __개인 키__ 클라이언트 toohello HDInsight 클러스터에 사용 되는 tooauthenticate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-166">hello __private key__ is used tooauthenticate your client toohello HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c076-167">암호를 사용하여 키를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-167">You can secure your keys using a passphrase.</span></span> <span data-ttu-id="9c076-168">암호는 사실상 개인 키의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-168">A passphrase is effectively a password on your private key.</span></span> <span data-ttu-id="9c076-169">다른 사람이 사용자의 개인 키가를 입수 하는 경우에 hello 암호 toouse hello 키를 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-169">Even if someone obtains your private key, they must have hello passphrase toouse hello key.</span></span>

### <a name="create-hdinsight-using-hello-public-key"></a><span data-ttu-id="9c076-170">HDInsight hello 공개 키를 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="9c076-170">Create HDInsight using hello public key</span></span>

| <span data-ttu-id="9c076-171">생성 방법</span><span class="sxs-lookup"><span data-stu-id="9c076-171">Creation method</span></span> | <span data-ttu-id="9c076-172">어떻게 toouse hello 공개 키</span><span class="sxs-lookup"><span data-stu-id="9c076-172">How toouse hello public key</span></span> |
| ------- | ------- |
| <span data-ttu-id="9c076-173">**Azure 포털**</span><span class="sxs-lookup"><span data-stu-id="9c076-173">**Azure portal**</span></span> | <span data-ttu-id="9c076-174">선택을 취소 __동일한 암호를 사용 하 여 클러스터 로그인으로__를 선택한 후 __공개 키__ hello SSH 인증 유형으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-174">Uncheck __Use same password as cluster login__, and then select __Public Key__ as hello SSH authentication type.</span></span> <span data-ttu-id="9c076-175">마지막으로, hello 공개 키 파일 선택 하거나 hello에 hello 파일의 hello 텍스트 내용을 붙여 __SSH 공개 키__ 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-175">Finally, select hello public key file or paste hello text contents of hello file in hello __SSH public key__ field.</span></span></br><span data-ttu-id="9c076-176">![HDInsight 클러스터 생성의 SSH 공개 키 대화 상자](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span><span class="sxs-lookup"><span data-stu-id="9c076-176">![SSH public key dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span></span> |
| <span data-ttu-id="9c076-177">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9c076-177">**Azure PowerShell**</span></span> | <span data-ttu-id="9c076-178">사용 하 여 hello `-SshPublicKey` hello의 매개 변수 `New-AzureRmHdinsightCluster` hello 공개 키를 문자열로 hello 내용을 cmdlet 및 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-178">Use hello `-SshPublicKey` parameter of hello `New-AzureRmHdinsightCluster` cmdlet and pass hello contents of hello public key as a string.</span></span>|
| <span data-ttu-id="9c076-179">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="9c076-179">**Azure CLI 1.0**</span></span> | <span data-ttu-id="9c076-180">사용 하 여 hello `--sshPublicKey` hello의 매개 변수 `azure hdinsight cluster create` 명령 및 hello 공개 키의 hello 내용을 문자열로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-180">Use hello `--sshPublicKey` parameter of hello `azure hdinsight cluster create` command and pass hello contents of hello public key as a string.</span></span> |
| <span data-ttu-id="9c076-181">**Resource Manager 템플릿**</span><span class="sxs-lookup"><span data-stu-id="9c076-181">**Resource Manager Template**</span></span> | <span data-ttu-id="9c076-182">템플릿에서 SSH 키를 사용하는 예제는 [SSH 키를 사용하여 Linux에서 HDInsight 배포](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c076-182">For an example of using SSH keys with a template, see [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span></span> <span data-ttu-id="9c076-183">hello `publicKeys` hello 요소 [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) 파일은 사용 되는 toopass hello 키 tooAzure hello 클러스터를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="9c076-183">hello `publicKeys` element in hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) file is used toopass hello keys tooAzure when creating hello cluster.</span></span> |

## <span data-ttu-id="9c076-184"><a id="sshpassword"></a>인증: 암호</span><span class="sxs-lookup"><span data-stu-id="9c076-184"><a id="sshpassword"></a>Authentication: Password</span></span>

<span data-ttu-id="9c076-185">SSH 계정은 암호를 사용하여 보호될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-185">SSH accounts can be secured using a password.</span></span> <span data-ttu-id="9c076-186">TooHDInsight SSH를 사용 하 여 연결할 때 메시지 표시 tooenter hello 암호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-186">When you connect tooHDInsight using SSH, you are prompted tooenter hello password.</span></span>

> [!WARNING]
> <span data-ttu-id="9c076-187">SSH에 대한 암호 인증을 사용하는 것은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-187">We do not recommend using password authentication for SSH.</span></span> <span data-ttu-id="9c076-188">암호 추측할 수 있으며 대입 공격 취약 toobrute 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-188">Passwords can be guessed and are vulnerable toobrute force attacks.</span></span> <span data-ttu-id="9c076-189">대신 [인증하기 위한 SSH 키](#sshkey)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-189">Instead, we recommend that you use [SSH keys for authentication](#sshkey).</span></span>

### <a name="create-hdinsight-using-a-password"></a><span data-ttu-id="9c076-190">암호를 사용하여 HDInsight 만들기</span><span class="sxs-lookup"><span data-stu-id="9c076-190">Create HDInsight using a password</span></span>

| <span data-ttu-id="9c076-191">생성 방법</span><span class="sxs-lookup"><span data-stu-id="9c076-191">Creation method</span></span> | <span data-ttu-id="9c076-192">Toospecify 암호 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9c076-192">How toospecify hello password</span></span> |
| --------------- | ---------------- |
| <span data-ttu-id="9c076-193">**Azure 포털**</span><span class="sxs-lookup"><span data-stu-id="9c076-193">**Azure portal**</span></span> | <span data-ttu-id="9c076-194">기본적으로 hello SSH 사용자 계정에 hello hello 클러스터 로그인 계정과 동일한 암호로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-194">By default, hello SSH user account has hello same password as hello cluster login account.</span></span> <span data-ttu-id="9c076-195">toouse 다른 암호를 선택 취소 __동일한 암호를 사용 하 여 클러스터 로그인으로__, 다음 hello에 hello 암호를 입력 하 고 __SSH 암호__ 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-195">toouse a different password, uncheck __Use same password as cluster login__, and then enter hello password in hello __SSH password__ field.</span></span></br><span data-ttu-id="9c076-196">![HDInsight 클러스터 생성의 SSH 암호 대화 상자](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span><span class="sxs-lookup"><span data-stu-id="9c076-196">![SSH password dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span></span>|
| <span data-ttu-id="9c076-197">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9c076-197">**Azure PowerShell**</span></span> | <span data-ttu-id="9c076-198">사용 하 여 hello `--SshCredential` hello의 매개 변수 `New-AzureRmHdinsightCluster` cmdlet 전달는 `PSCredential` hello SSH 사용자 계정 이름 및 암호를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-198">Use hello `--SshCredential` parameter of hello `New-AzureRmHdinsightCluster` cmdlet and pass a `PSCredential` object that contains hello SSH user account name and password.</span></span> |
| <span data-ttu-id="9c076-199">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="9c076-199">**Azure CLI 1.0**</span></span> | <span data-ttu-id="9c076-200">사용 하 여 hello `--sshPassword` hello의 매개 변수 `azure hdinsight cluster create` 명령 고 hello 암호 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-200">Use hello `--sshPassword` parameter of hello `azure hdinsight cluster create` command and provide hello password value.</span></span> |
| <span data-ttu-id="9c076-201">**Resource Manager 템플릿**</span><span class="sxs-lookup"><span data-stu-id="9c076-201">**Resource Manager Template**</span></span> | <span data-ttu-id="9c076-202">템플릿에서 암호를 사용하는 예제는 [SSH 암호를 사용하여 Linux에서 HDInsight 배포](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c076-202">For an example of using a password with a template, see [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> <span data-ttu-id="9c076-203">hello `linuxOperatingSystemProfile` hello 요소 [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) 파일은 사용 되는 toopass는 hello SSH 계정 이름 및 암호 tooAzure hello 클러스터를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="9c076-203">hello `linuxOperatingSystemProfile` element in hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) file is used toopass hello SSH account name and password tooAzure when creating hello cluster.</span></span>|

### <a name="change-hello-ssh-password"></a><span data-ttu-id="9c076-204">Hello SSH 암호 변경</span><span class="sxs-lookup"><span data-stu-id="9c076-204">Change hello SSH password</span></span>

<span data-ttu-id="9c076-205">Hello SSH 사용자 계정 암호를 변경 하는 방법에 대 한 정보를 참조 hello __암호 변경__ hello의 섹션 [관리할 HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) 문서.</span><span class="sxs-lookup"><span data-stu-id="9c076-205">For information on changing hello SSH user account password, see hello __Change passwords__ section of hello [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) document.</span></span>

## <span data-ttu-id="9c076-206"><a id="domainjoined"></a>인증: 도메인에 조인된 HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c076-206"><a id="domainjoined"></a>Authentication: Domain-joined HDInsight</span></span>

<span data-ttu-id="9c076-207">사용 하는 경우는 __도메인에 가입 된 HDInsight 클러스터__, hello를 사용 해야 `kinit` SSH로 연결한 후에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-207">If you are using a __domain-joined HDInsight cluster__, you must use hello `kinit` command after connecting with SSH.</span></span> <span data-ttu-id="9c076-208">이 명령은 도메인 사용자 및 암호를 묻는 메시지를 표시 하 고 hello 클러스터와 연결 된 hello Azure Active Directory 도메인을 사용 하 여 세션이 인증.</span><span class="sxs-lookup"><span data-stu-id="9c076-208">This command prompts you for a domain user and password, and authenticates your session with hello Azure Active Directory domain associated with hello cluster.</span></span>

<span data-ttu-id="9c076-209">자세한 내용은 [도메인에 조인된 HDInsight 구성](hdinsight-domain-joined-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c076-209">For more information, see [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md).</span></span>

## <a name="connect-toonodes"></a><span data-ttu-id="9c076-210">Toonodes 연결</span><span class="sxs-lookup"><span data-stu-id="9c076-210">Connect toonodes</span></span>

<span data-ttu-id="9c076-211">헤드 노드 및 가장자리 노드 (있는 경우) hello hello를 통해 액세스할 수 포트 22 및 23 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-211">hello head nodes and edge node (if there is one) can be accessed over hello internet on ports 22 and 23.</span></span>

* <span data-ttu-id="9c076-212">Toohello 연결할 때 __헤드 노드__, 포트를 사용 하 여 __22__ tooconnect toohello 기본 헤드 노드 및 포트 __23__ tooconnect toohello 보조 헤드 노드.</span><span class="sxs-lookup"><span data-stu-id="9c076-212">When connecting toohello __head nodes__, use port __22__ tooconnect toohello primary head node and port __23__ tooconnect toohello secondary head node.</span></span> <span data-ttu-id="9c076-213">hello 정규화 된 도메인 이름 toouse은 `clustername-ssh.azurehdinsight.net`여기서 `clustername` hello 클러스터 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-213">hello fully qualified domain name toouse is `clustername-ssh.azurehdinsight.net`, where `clustername` is hello name of your cluster.</span></span>

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* <span data-ttu-id="9c076-214">때 connectiung toohello __가장자리 노드__, 포트 22를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-214">When connectiung toohello __edge node__, use port 22.</span></span> <span data-ttu-id="9c076-215">hello 정규화 된 도메인 이름이 `edgenodename.clustername-ssh.azurehdinsight.net`여기서 `edgenodename` hello 가장자리 노드 만들 때 제공 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-215">hello fully qualified domain name is `edgenodename.clustername-ssh.azurehdinsight.net`, where `edgenodename` is a name you provided when creating hello edge node.</span></span> <span data-ttu-id="9c076-216">`clustername`hello hello 클러스터 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-216">`clustername` is hello name of hello cluster.</span></span>

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> <span data-ttu-id="9c076-217">hello 이전 예제에는 암호 인증을 사용 하는 또는 인증서 인증이 자동으로 발생 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-217">hello previous examples assume that you are using password authentication, or that certificate authentication is occuring automatically.</span></span> <span data-ttu-id="9c076-218">Hello를 사용 하 여 인증을 위해 SSH 키 쌍을 사용 하는 경우 hello 인증서 자동으로 사용 되지 않습니다. `-i` 매개 변수 toospecify hello에 대 한 개인 키입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-218">If you use an SSH key-pair for authentication, and hello certificate is not used automatically, use hello `-i` parameter toospecify hello private key.</span></span> <span data-ttu-id="9c076-219">예: `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="9c076-219">For example, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span></span>

<span data-ttu-id="9c076-220">연결 되 면 hello 프롬프트가 tooindicate hello SSH 사용자 이름 및 hello 노드에 연결 되어 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-220">Once connected, hello prompt changes tooindicate hello SSH user name and hello node you are connected to.</span></span> <span data-ttu-id="9c076-221">예를 들어, 연결 된 경우 toohello 기본 헤드 노드를 `sshuser`, hello 프롬프트가 `sshuser@hn0-clustername:~$`합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-221">For example, when connected toohello primary head node as `sshuser`, hello prompt is `sshuser@hn0-clustername:~$`.</span></span>

### <a name="connect-tooworker-and-zookeeper-nodes"></a><span data-ttu-id="9c076-222">Tooworker 및 사육 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-222">Connect tooworker and Zookeeper nodes</span></span>

<span data-ttu-id="9c076-223">hello 작업자 노드 및 노드에서 직접 액세스할 수 없는 사육 hello 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-223">hello worker nodes and Zookeeper nodes are not directly accessible from hello internet.</span></span> <span data-ttu-id="9c076-224">Hello 클러스터 헤드 노드 또는 노드 가장자리에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-224">They can be accessed from hello cluster head nodes or edge nodes.</span></span> <span data-ttu-id="9c076-225">hello 다음은 hello 일반적인 단계 tooconnect tooother 노드.</span><span class="sxs-lookup"><span data-stu-id="9c076-225">hello following are hello general steps tooconnect tooother nodes:</span></span>

1. <span data-ttu-id="9c076-226">SSH tooconnect tooa 또는 가장자리에서 헤드 노드를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="9c076-226">Use SSH tooconnect tooa head or edge node:</span></span>

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. <span data-ttu-id="9c076-227">Hello를 사용 하 여 SSH 연결 toohello 헤드 hello 또는 가장자리 노드 `ssh` hello 클러스터의 명령 tooconnect tooa 작업자 노드:</span><span class="sxs-lookup"><span data-stu-id="9c076-227">From hello SSH connection toohello head or edge node, use hello `ssh` command tooconnect tooa worker node in hello cluster:</span></span>

        ssh sshuser@wn0-myhdi

    <span data-ttu-id="9c076-228">tooretrieve hello hello 클러스터 노드 hello 도메인 이름 목록은 참조 hello [관리할 HDInsight를 사용 하 여 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) 문서.</span><span class="sxs-lookup"><span data-stu-id="9c076-228">tooretrieve a list of hello domain names of hello nodes in hello cluster, see hello [Manage HDInsight by using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span></span>

<span data-ttu-id="9c076-229">SSH 계정 hello를 사용 하 여 보호 되는 경우는 __암호__를 연결할 때 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-229">If hello SSH account is secured using a __password__, enter hello password when connecting.</span></span>

<span data-ttu-id="9c076-230">SSH 계정 hello를 사용 하 여 보호 되는 경우 __SSH 키__, SSH 전달 hello 클라이언트에서 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-230">If hello SSH account is secured using __SSH keys__, make sure that SSH forwarding is enabled on hello client.</span></span>

> [!NOTE]
> <span data-ttu-id="9c076-231">Toodirectly hello 클러스터의 모든 노드에 액세스 하는 또 다른 방법은 tooinstall을 Azure 가상 네트워크로 HDInsight는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-231">Another way toodirectly access all nodes in hello cluster is tooinstall HDInsight into an Azure Virtual Network.</span></span> <span data-ttu-id="9c076-232">그런 다음 원격 컴퓨터 toohello 조인할 수 있습니다 동일한 가상 네트워크 및 hello 클러스터의 모든 노드에 직접 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-232">Then, you can join your remote machine toohello same virtual network and directly access all nodes in hello cluster.</span></span>
>
> <span data-ttu-id="9c076-233">자세한 내용은 [HDInsight와 함께 가상 네트워크 사용](hdinsight-extend-hadoop-virtual-network.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9c076-233">For more information, see [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md).</span></span>

### <a name="configure-ssh-agent-forwarding"></a><span data-ttu-id="9c076-234">SSH 에이전트 전달 구성</span><span class="sxs-lookup"><span data-stu-id="9c076-234">Configure SSH agent forwarding</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c076-235">hello 다음 단계는 Linux 또는 UNIX 기반 시스템 및 가정 Bash Windows 10에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-235">hello following steps assume a Linux or UNIX-based system, and work with Bash on Windows 10.</span></span> <span data-ttu-id="9c076-236">시스템에 대 한 이러한 단계가 작동 하지 않습니다, 경우에 SSH 클라이언트에 대 한 tooconsult hello 설명서를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-236">If these steps do not work for your system, you may need tooconsult hello documentation for your SSH client.</span></span>

1. <span data-ttu-id="9c076-237">텍스트 편집기를 사용하여 `~/.ssh/config`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-237">Using a text editor, open `~/.ssh/config`.</span></span> <span data-ttu-id="9c076-238">이 파일이 존재하지 않으면 명령줄에 `touch ~/.ssh/config`를 입력하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-238">If this file doesn't exist, you can create it by entering `touch ~/.ssh/config` at a command line.</span></span>

2. <span data-ttu-id="9c076-239">다음 텍스트 toohello hello 추가 `config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-239">Add hello following text toohello `config` file.</span></span>

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    <span data-ttu-id="9c076-240">Hello 대체 __호스트__ 정보 toousing SSH hello 노드의 hello 주소와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-240">Replace hello __Host__ information with hello address of hello node you connect toousing SSH.</span></span> <span data-ttu-id="9c076-241">hello 앞의 예제는 hello 가장자리 노드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-241">hello previous example uses hello edge node.</span></span> <span data-ttu-id="9c076-242">이 항목에 지정 된 노드 hello에 대 한 전달 SSH 에이전트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-242">This entry configures SSH agent forwarding for hello specified node.</span></span>

3. <span data-ttu-id="9c076-243">테스트 SSH 에이전트 hello 터미널 hello에서 다음 명령을 사용 하 여 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-243">Test SSH agent forwarding by using hello following command from hello terminal:</span></span>

        echo "$SSH_AUTH_SOCK"

    <span data-ttu-id="9c076-244">이 명령은 정보 비슷한 toohello를 다음 텍스트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-244">This command returns information similar toohello following text:</span></span>

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    <span data-ttu-id="9c076-245">아무 것도 반환되지 않으면 `ssh-agent`가 실행되지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-245">If nothing is returned, then `ssh-agent` is not running.</span></span> <span data-ttu-id="9c076-246">자세한 내용은 hello 에이전트 시작 스크립트에서 정보를 참조 하십시오. [를 사용 하 여 ssh-에이전트와 ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) 또는 SSH 클라이언트 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9c076-246">For more information, see hello agent startup scripts information at [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) or consult your SSH client documentation.</span></span>

4. <span data-ttu-id="9c076-247">확인 한 후 **ssh-에이전트** SSH 개인 키 toohello 에이전트를 실행 하 고 사용 하 여 hello tooadd 다음 됩니다:</span><span class="sxs-lookup"><span data-stu-id="9c076-247">Once you have verified that **ssh-agent** is running, use hello following tooadd your SSH private key toohello agent:</span></span>

        ssh-add ~/.ssh/id_rsa

    <span data-ttu-id="9c076-248">개인 키로 다른 파일에 저장 되 면 대체 `~/.ssh/id_rsa` hello toohello 파일 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-248">If your private key is stored in a different file, replace `~/.ssh/id_rsa` with hello path toohello file.</span></span>

5. <span data-ttu-id="9c076-249">Toohello 클러스터 가장자리 노드 또는 SSH를 사용 하 여 헤드 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-249">Connect toohello cluster edge node or head nodes using SSH.</span></span> <span data-ttu-id="9c076-250">Hello SSH 명령 tooconnect tooa 작업자 또는 사육 노드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-250">Then use hello SSH command tooconnect tooa worker or zookeeper node.</span></span> <span data-ttu-id="9c076-251">전달 하는 hello 키를 사용 하 여 hello 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-251">hello connection is established using hello forwarded key.</span></span>

## <a name="copy-files"></a><span data-ttu-id="9c076-252">파일 복사</span><span class="sxs-lookup"><span data-stu-id="9c076-252">Copy files</span></span>

<span data-ttu-id="9c076-253">hello `scp` 유틸리티 hello 클러스터의 개별 노드 모두에서 사용 되는 toocopy 파일 tooand 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-253">hello `scp` utility can be used toocopy files tooand from individual nodes in hello cluster.</span></span> <span data-ttu-id="9c076-254">예를 들어 다음 명령은 복사본 hello hello `test.txt` hello 로컬 시스템 toohello 기본 헤드 노드에서 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="9c076-254">For example, hello following command copies hello `test.txt` directory from hello local system toohello primary head node:</span></span>

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

<span data-ttu-id="9c076-255">Hello 후 지정 된 경로가 있으므로 `:`, hello 파일은 hello `sshuser` 홈 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-255">Since no path is specified after hello `:`, hello file is placed in hello `sshuser` home directory.</span></span>

<span data-ttu-id="9c076-256">다음 예에서는 복사본 hello hello `test.txt` hello에서 파일 `sshuser` hello 기본 헤드 노드 toohello 로컬 시스템에 홈 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="9c076-256">hello following example copies hello `test.txt` file from hello `sshuser` home directory on hello primary head node toohello local system:</span></span>

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> <span data-ttu-id="9c076-257">`scp`hello 클러스터 내에서 개별 노드의 hello 파일 시스템만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-257">`scp` can only access hello file system of individual nodes within hello cluster.</span></span> <span data-ttu-id="9c076-258">Hello 클러스터에 대 한 hello HDFS 호환 저장소에서 사용 되는 tooaccess 데이터 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-258">It cannot be used tooaccess data in hello HDFS-compatible storage for hello cluster.</span></span>
>
> <span data-ttu-id="9c076-259">사용 하 여 `scp` 대 한 SSH 세션에서 사용 하기 위해 리소스 tooupload 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-259">Use `scp` when you need tooupload a resource for use from an SSH session.</span></span> <span data-ttu-id="9c076-260">예를 들어 Python 스크립트를 업로드 하 고 한 SSH 세션에서 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c076-260">For example, upload a Python script and then run hello script from an SSH session.</span></span>
>
> <span data-ttu-id="9c076-261">Hello HDFS 호환 저장소에 데이터를 직접 로드에 대 한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="9c076-261">For information on directly loading data into hello HDFS-compatible storage, see hello following documents:</span></span>
>
> * <span data-ttu-id="9c076-262">[Azure Storage를 사용하는 HDInsight](hdinsight-hadoop-use-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="9c076-262">[HDInsight using Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span>
>
> * <span data-ttu-id="9c076-263">[Azure Data Lake Store를 사용하는 HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="9c076-263">[HDInsight using Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c076-264">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c076-264">Next steps</span></span>

* [<span data-ttu-id="9c076-265">HDInsight와 함께 SSH 터널링 사용</span><span class="sxs-lookup"><span data-stu-id="9c076-265">Use SSH tunneling with HDInsight</span></span>](hdinsight-linux-ambari-ssh-tunnel.md)
* [<span data-ttu-id="9c076-266">HDInsight와 함께 가상 네트워크 사용</span><span class="sxs-lookup"><span data-stu-id="9c076-266">Use a virtual network with HDInsight</span></span>](hdinsight-extend-hadoop-virtual-network.md)
* [<span data-ttu-id="9c076-267">HDInsight에서 에지 노드 사용</span><span class="sxs-lookup"><span data-stu-id="9c076-267">Use edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md#access-an-edge-node)