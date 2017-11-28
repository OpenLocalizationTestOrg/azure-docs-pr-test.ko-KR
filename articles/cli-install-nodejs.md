---
title: aaaInstall hello Azure CLI 1.0 | Microsoft Docs
description: "Azure 서비스를 사용 하 여 Mac, Linux 및 Windows toostart에 대 한 hello Azure CLI 1.0 설치"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="213e2-103">Hello Azure CLI 1.0 설치</span><span class="sxs-lookup"><span data-stu-id="213e2-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="213e2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="213e2-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="213e2-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="213e2-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="213e2-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="213e2-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="213e2-107">이 항목에서는 많은 수의 리소스 관리자 배포 활동 뿐 아니라 tooinstall hello Azure CLI 1.0 nodeJs에서 빌드하고 지 원하는 모든 클래식 배포 API를 호출 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="213e2-108">Hello를 사용 해야 [Azure CLI 2.0](/cli/azure/overview) 새롭거나 특정 CLI 배포 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="213e2-109">Hello Azure 명령줄 인터페이스 (Azure CLI 1.0) toouse 만들고 Microsoft Azure의에서 리소스를 관리 하기 위한 오픈 소스 셸 기반 명령 집합을 신속 하 게 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="213e2-110">몇 가지 옵션 tooinstall 이러한 플랫폼 간 도구에 있는 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="213e2-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="213e2-111">**npm 패키지** 실행-Linux 배포 또는 운영 체제에서 (JavaScript 용 hello 패키지 관리자) npm tooinstall hello 최신 Azure CLI 1.0 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="213e2-112">node.js 및 npm이 컴퓨터에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="213e2-113">**설치 관리자** - 설치 관리자를 다운로드하여 Mac 또는 Windows에서 손쉽게 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="213e2-114">**Docker 컨테이너** -시작 hello를 사용 하 여 최신 CLI 실행 방식 Docker 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="213e2-115">Docker 호스트가 컴퓨터에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="213e2-116">많은 옵션과 배경 hello 프로젝트 저장소에서 참조 [GitHub](https://github.com/azure/azure-xplat-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="213e2-117">Hello Azure CLI 1.0 설치 되 면 [Azure 구독과 연결](xplat-cli-connect.md) 및 실행된 hello **azure** 프로그램 명령줄 인터페이스 (예: Bash, 터미널, 명령 프롬프트 및 등)에서 명령으로 toowork Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="213e2-118">옵션 1: npm 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="213e2-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="213e2-119">tooinstall hello CLI npm 패키지를 다운로드 하 고 hello 설치 되어 있는지 확인 [최신 Node.js 및 npm](https://nodejs.org/en/download/package-manager/)합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="213e2-120">그런 다음 실행 **npm 설치** tooinstall hello azure cli 패키지:</span><span class="sxs-lookup"><span data-stu-id="213e2-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="213e2-121">Linux 배포판의 toouse 할 수 있습니다 **sudo** 실행 toosuccessfully hello **npm** 명령, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="213e2-122">를 tooinstall 필요 하거나 Node.js 및 npm Linux 배포 또는 운영 체제를 업데이트 하는 경우에 hello 가장 최근의 Node.js LTS 버전 (4.x) 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="213e2-123">이전 버전을 사용하는 경우 설치 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="213e2-124">원하는 경우 다운로드 최신 Linux hello [tar 파일] [ linux-installer] 로컬로 hello npm 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="213e2-125">그런 다음 다음과 같이 hello 다운로드 한 npm 패키지를 설치 (Linux 배포판의 해야 toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="213e2-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="213e2-126">옵션 2: 설치 관리자 사용</span><span class="sxs-lookup"><span data-stu-id="213e2-126">Option 2: Use an installer</span></span>
<span data-ttu-id="213e2-127">Mac 또는 Windows 컴퓨터를 사용 하는 경우 hello CLI 설치 관리자가 다음 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="213e2-128">[Mac OS X 설치 관리자][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="213e2-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="213e2-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="213e2-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="213e2-130">Windows에서 다운로드할 수도 있습니다 hello [웹 플랫폼 설치 관리자](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="213e2-131">이 설치 관리자에서는 옵션 tooinstall hello 추가 Azure SDK 및 명령줄 도구를 설치한 후 hello CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="213e2-132">옵션 3: Docker 컨테이너 사용</span><span class="sxs-lookup"><span data-stu-id="213e2-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="213e2-133">로 컴퓨터를 설정한 경우는 [Docker](https://docs.docker.com/engine/understanding-docker/) 호스트를 실행할 수 있습니다 최신 Azure CLI 1.0 Docker 컨테이너에서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="213e2-134">실행 hello 다음 명령을 (Linux 배포판의 해야 toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="213e2-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="213e2-135">Azure CLI 1.0 명령 실행</span><span class="sxs-lookup"><span data-stu-id="213e2-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="213e2-136">Hello Azure CLI 1.0 설치 된 후 실행 hello **azure** 명령줄 사용자 인터페이스 (예: Bash, 터미널, 명령 프롬프트 및 등)에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="213e2-137">예를 들어, toorun hello 도움말 명령 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="213e2-138">일부 Linux 배포판에 나타날 수 있습니다 유사한 오류가 너무`/usr/bin/env: ‘node’: No such file or directory`합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="213e2-139">이 오류는 최근에 Node.js를 /usr/bin/nodejs에 설치할 때 비롯되었습니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="213e2-140">toofix,이 명령을 실행 하 여 기호화 된 링크 너무/usr/bin/노드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="213e2-141">hello Azure CLI 1.0를 설치한 다음 형식 hello toosee hello 버전:</span><span class="sxs-lookup"><span data-stu-id="213e2-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="213e2-142">이제 준비가 되었습니다!</span><span class="sxs-lookup"><span data-stu-id="213e2-142">Now you are ready!</span></span> <span data-ttu-id="213e2-143">모든 tooaccess hello로 리소스, CLI 명령을 toowork [hello Azure CLI에서에서 tooyour Azure 구독 연결](xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="213e2-144">먼저 Azure CLI를 사용 하는 경우 Microsoft toocollect 사용 정보 tooallow 설정할지 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="213e2-145">참여는 자발적입니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-145">Participation is voluntary.</span></span> <span data-ttu-id="213e2-146">실행 하 여 언제 든 지 중지할 수 tooparticipate을 선택 하면 `azure telemetry --disable`합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="213e2-147">언제 든 지 참여 tooenable 실행 `azure telemetry --enable`합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="213e2-148">Hello CLI를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-148">Update hello CLI</span></span>
<span data-ttu-id="213e2-149">Microsoft은 업데이트 된 버전의 hello Azure CLI를 자주 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="213e2-150">다시 설치 중인 운영 체제에 대 한 hello 설치 관리자를 사용 하 여 CLI hello 또는 hello 최신 Docker 컨테이너를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="213e2-151">Hello 다음을 입력 하 여 최신 Node.js 및 npm 설치를 hello 있는, 하는 경우 업데이트 또는 (Linux 배포판의 해야 toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="213e2-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="213e2-152">탭 완성 기능 사용</span><span class="sxs-lookup"><span data-stu-id="213e2-152">Enable tab completion</span></span>
<span data-ttu-id="213e2-153">CLI 명령의 탭 완성 기능이 Mac 및 Linux에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="213e2-154">tooenable zsh에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="213e2-155">tooenable bash에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="213e2-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="213e2-156">Next steps</span></span>
* <span data-ttu-id="213e2-157">[Hello CLI tooyour Azure 구독에서에서 연결](xplat-cli-connect.md) toocreate 및 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="213e2-158">hello Azure CLI에 대해 자세히 toolearn 소스 코드를 다운로드, 문제를 보고 또는 toohello 프로젝트 참가, hello 방문 [Azure CLI hello에 대 한 GitHub 리포지토리](https://github.com/azure/azure-xplat-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="213e2-159">Hello Azure CLI 또는 Azure를 사용 하는 방법에 대 한 질문이 있으면 방문 hello [의 Azure 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)합니다.</span><span class="sxs-lookup"><span data-stu-id="213e2-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
