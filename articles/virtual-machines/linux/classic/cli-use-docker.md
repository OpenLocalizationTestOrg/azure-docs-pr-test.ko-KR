---
title: "aaaUsing hello Azure에서 Linux에 대 한 Docker VM 확장"
description: "Docker 및 hello Azure 가상 컴퓨터 확장을 설명 하 고 tooprogrammatically Azure의 hello Azure CLI를 사용 하 여 hello 명령줄에서 docker 호스트에서 가상 컴퓨터를 만드는 방법을 보여 줍니다."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="4861b-103">Hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4861b-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4861b-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4861b-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4861b-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4861b-107">Hello 리소스 관리자 model과 함께 hello Docker VM 확장을 사용 하는 방법에 대 한 내용은 [여기](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4861b-108">이 항목에서는 toocreate hello에서 Docker VM 확장 hello 사용 하 여 VM에서 모든 플랫폼에서 Azure CLI asm (관리) 모드를 서비스 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="4861b-109">[Docker](https://www.docker.com/) hello 중 하나를 사용 하는 가장 인기 있는 가상화 방법입니다. [Linux 컨테이너](http://en.wikipedia.org/wiki/LXC) 데이터 격리 하 고 공유 리소스에서 계산 하는 방법으로 가상 컴퓨터 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="4861b-110">Hello Docker VM 확장 및 hello 사용할 수 있습니다 [Azure Linux 에이전트](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate 개수에 관계 없이 Azure에서 응용 프로그램에 대 한 컨테이너를 호스트 하는 Docker VM입니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="4861b-111">높은 수준의 컨테이너와 그 장점을 설명 toosee 참조 hello [Docker 높은 수준 화이트 보드](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="4861b-112">어떻게 toouse hello azure Docker VM 확장</span><span class="sxs-lookup"><span data-stu-id="4861b-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="4861b-113">Azure와 toouse hello Docker VM 확장을 hello의 버전을 설치 해야 [Azure 명령줄 인터페이스](https://github.com/Azure/azure-sdk-tools-xplat) Azure CLI () (이 쓰기 hello의 현재 버전은 0.10.0 임)으로 0.8.6 보다 높은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="4861b-114">Hello Azure CLI Mac, Linux 및 Windows에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="4861b-115">hello 전체 프로세스 toouse Azure에서 Docker는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="4861b-116">Hello Azure CLI 및 해당 종속성 toocontrol Azure 원하는 hello 컴퓨터에 설치 (windows에서이 수는 가상 컴퓨터로 실행 되는 Linux 배포판)</span><span class="sxs-lookup"><span data-stu-id="4861b-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="4861b-117">Azure의 hello Azure CLI Docker 명령을 toocreate VM Docker 호스트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4861b-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="4861b-118">Azure에서 Docker VM에서 로컬 Docker 명령을 toomanage hello Docker 컨테이너를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="4861b-119">Hello Azure 명령줄 인터페이스 (Azure CLI)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="4861b-120">tooinstall hello Azure CLI를 구성 하 고, 참조 [어떻게 tooinstall hello Azure 명령줄 인터페이스](../../../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="4861b-121">tooconfirm hello 설치 유형 `azure` hello 명령 프롬프트 및 짧은 잠시 후 hello Azure CLI ASCII 아트 hello basic 나열 하는 명령을 사용할 수 있는 tooyou 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="4861b-122">Hello 설치 올바르게 작동 한 경우 수 tootype 있어야 `azure help vm` "docker" hello 나열 된 명령 중 하나 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="4861b-123">Windows 용 docker에 도구가 [Docker 컴퓨터](https://docs.docker.com/installation/windows/)이며 tooautomate hello 만들기를 사용할 수 있습니다 toowork vm이 Azure docker 호스트와 docker 클라이언트를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="4861b-124">Hello Azure CLI tootooyour Azure 계정 연결</span><span class="sxs-lookup"><span data-stu-id="4861b-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="4861b-125">Hello Azure CLI를 사용 하려면 먼저 플랫폼에서 Azure CLI hello와 Azure 계정 자격 증명를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="4861b-126">섹션 hello [어떻게 tooconnect tooyour Azure 구독](../../../xplat-cli-connect.md) tooeither 다운로드 하 고 가져오는 방법에 대해 설명 프로그램 **.publishsettings** 파일 또는 Azure CLI 조직 id를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="4861b-127">하나를 사용할 때의 동작 차이가 있습니다 문서일 수도 혹은 hello 다른 형태의 인증을 지금 수행 있는지 tooread hello toounderstand hello에 대 한 다른 기능 위에 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="4861b-128">Docker를 설치 하 고 Azure 용 hello Docker VM 확장 사용</span><span class="sxs-lookup"><span data-stu-id="4861b-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="4861b-129">Hello에 따라 [Docker 설치 지침](https://docs.docker.com/installation/#installation) 컴퓨터에 로컬로 Docker tooinstall 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="4861b-130">Azure 가상 컴퓨터와 Docker toouse hello VM에 사용 되는 hello Linux 이미지 hello 있어야 [Azure Linux VM 에이전트](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="4861b-131">현재 이 에이전트를 설치할 수 있는 이미지의 유형은 다음의 두 가지뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="4861b-132">Hello Azure 이미지 갤러리에서에서 Ubuntu 이미지 또는</span><span class="sxs-lookup"><span data-stu-id="4861b-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="4861b-133">사용자가 만든 Azure Linux VM 에이전트 설치 및 구성 hello로 Linux 이미지 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="4861b-134">참조 [Azure Linux VM 에이전트](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 방법에 대 한 자세한 내용은 toobuild hello Azure VM 에이전트를 사용 하 여 Linux VM 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="4861b-135">Hello Azure 이미지 갤러리를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4861b-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="4861b-136">Bash 또는 터미널 세션에서 다음 toolocate hello VM 갤러리 toouse에서 가장 최근의 Ubuntu 이미지를 입력 하 여 hello Azure CLI 명령을 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4861b-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="4861b-137">과 같은 hello 이미지 이름 중 하나를 선택 하 고 `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`를 사용 하 여 hello 다음 명령은 toocreate 해당 이미지를 사용 하 여 새 VM 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="4861b-138">설명:</span><span class="sxs-lookup"><span data-stu-id="4861b-138">where:</span></span>

* <span data-ttu-id="4861b-139">*&lt;cloudservice vm 이름&gt;*  hello Azure의 hello Docker 컨테이너 호스트 컴퓨터 될 VM의 hello 이름인</span><span class="sxs-lookup"><span data-stu-id="4861b-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="4861b-140">*&lt;사용자 이름&gt;*  hello VM의 hello 기본 루트 사용자의 hello 사용자 이름인</span><span class="sxs-lookup"><span data-stu-id="4861b-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="4861b-141">*&lt;암호&gt;*  hello 암호의 hello *username* Azure에 대 한 복잡 한 hello 표준을 충족 하는 계정</span><span class="sxs-lookup"><span data-stu-id="4861b-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="4861b-142">현재 암호 해야 8 자 이상, 하나의 소문자 및 대문자 한 문자, 숫자 및 hello 문자 중 하 나와 같은 특수 문자 포함: `!@#$%^&+=`합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="4861b-143">아니요, hello 기간 hello 문장 앞의 hello 끝에는 특수 문자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="4861b-144">Hello 명령이 성공적으로, hello 정확 하 게 인수 및 사용 하는 옵션에 따라 hello 다음 같은 내용이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="4861b-145">가상 컴퓨터를 만들려면 몇 분 정도 걸릴 수 있지만 후 것에 프로 비전 (hello 상태 값은 `ReadyRole`) hello Docker daemon (Docker 서비스 hello) 시작 하 고 toohello Docker 컨테이너 호스트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="4861b-146">tootest hello Docker VM 유형 Azure에서 만든</span><span class="sxs-lookup"><span data-stu-id="4861b-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="4861b-147">여기서  *&lt;vm-name--사용한&gt;*  너무 호출에서 사용 하는 hello 가상 컴퓨터의 hello 이름인`azure vm docker create`합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="4861b-148">다음과 유사한을 Docker 호스트 VM을 나타내는 toohello 다음 Azure에서 실행 중인 및 대기 하 여 명령에 대 한 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="4861b-149">이제 docker 클라이언트 tooobtain 정보를 사용 하 여 tooconnect 시도할 수 있습니다 (일부 Docker 클라이언트 설치 과정에서, Mac에서와 같이 toouse 있을 수 있습니다 `sudo`):</span><span class="sxs-lookup"><span data-stu-id="4861b-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="4861b-150">정당한 toobe 모든 작업 지, Docker 확장 hello에 대 한 VM hello를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="4861b-151">Docker Host VM 인증</span><span class="sxs-lookup"><span data-stu-id="4861b-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="4861b-152">또한 Docker VM toocreating hello hello `azure vm docker create` 명령은 자동으로 hello 필요한 인증서 tooallow Docker 클라이언트 컴퓨터 tooconnect toohello Azure 컨테이너 호스트 HTTPS를 사용 하 여 만들고 hello 인증서 둘 다에 저장 됩니다 hello 클라이언트 및 호스트 컴퓨터를 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="4861b-153">후속 시도에 hello 기존 인증서 다시 사용 되며 hello 새 호스트와 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="4861b-154">기본적으로 인증서에 배치 됩니다 `~/.docker`, Docker 포트에서 구성 된 toorun 됩니다 **2376**합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="4861b-155">다른 포트 toouse 또는 디렉터리를 원하는 경우 hello 다음 중 하나를 사용할 수 `azure vm docker create` 명령줄 옵션 tooconfigure Docker 컨테이너 호스트 VM toouse 다른 포트 또는 연결 하는 클라이언트에 대 한 서로 다른 인증서:</span><span class="sxs-lookup"><span data-stu-id="4861b-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="4861b-156">hello hello 호스트에서 Docker 디먼에 대 한 구성 된 toolisten 이며 hello에서 연결 hello에 의해 생성 된 hello 인증서를 사용 하 여 포트를 지정 하는 클라이언트를 인증 `azure vm docker create` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="4861b-157">hello 클라이언트 컴퓨터에 이러한 인증서 toogain 액세스 toohello Docker 호스트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="4861b-158">이러한 인증서 없이 실행 되는 네트워크로 연결 된 호스트 tooconnect toohello 컴퓨터 수 취약 tooanyone 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="4861b-159">Hello 기본 구성을 수정 하기 전에 hello 위험 tooyour 컴퓨터 및 응용 프로그램을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4861b-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4861b-160">Next steps</span></span>
* <span data-ttu-id="4861b-161">준비 toogo toohello는 [Docker 사용자 가이드] Docker VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="4861b-162">hello 새로운 포털에서 Docker 사용 가능 VM toocreate 참조 [포털 hello로 toouse Docker VM 확장 hello 어떻게]합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="4861b-163">hello Azure Docker VM 확장은 또한 모든 환경 전체 선언적 YAML 파일 tootake 개발자 모델링 응용 프로그램을 사용 하 여 Docker Compose를 지원 하 고 일관 된 배포를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="4861b-164">참조 [Docker 시작 및 toodefine를 작성 하 고, Azure 가상 컴퓨터에서 여러 컨테이너 응용 프로그램 실행]합니다.</span><span class="sxs-lookup"><span data-stu-id="4861b-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[포털 hello로 toouse Docker VM 확장 hello 어떻게]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Docker 사용자 가이드]:https://docs.docker.com/userguide/

[Docker 시작 및 toodefine를 작성 하 고, Azure 가상 컴퓨터에서 여러 컨테이너 응용 프로그램 실행]:../docker-compose-quickstart.md
