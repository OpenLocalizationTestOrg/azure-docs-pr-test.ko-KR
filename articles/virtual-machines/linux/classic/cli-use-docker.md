---
title: "Azure에서 Linux용 Docker VM 확장 사용"
description: "Docker 및 Azure 가상 컴퓨터 확장에 대해 설명하고, Azure CLI를 사용하여 명령줄에서 Docker 호스트인 가상 컴퓨터를 Azure에 프로그래밍 방식으로 만드는 방법을 안내합니다."
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
ms.openlocfilehash: a542332c921862241f1f000e6a8f0a0ae0e8a934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-from-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="cc38d-103">Azure 명령줄 인터페이스(Azure CLI)에서 Docker VM 확장 사용</span><span class="sxs-lookup"><span data-stu-id="cc38d-103">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="cc38d-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cc38d-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="cc38d-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="cc38d-107">Resource Manager 모델에서 Docker VM 확장을 사용하는 방법에 대한 정보는 [여기](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc38d-107">For information about using the Docker VM extension with the Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cc38d-108">이 항목에서는 모든 플랫폼의 Azure CLI에서 서비스 관리(asm) 모드로 Docker VM 확장을 사용하여 VM을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-108">This topic describes how to create a VM with the Docker VM Extension from the service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="cc38d-109">[Docker](https://www.docker.com/)는 공유 리소스의 데이터와 계산을 격리시키는 한 가지 방법으로 가상 컴퓨터 대신 [Linux 컨테이너](http://en.wikipedia.org/wiki/LXC)를 사용하는 가장 많이 사용되는 가상화 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-109">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="cc38d-110">[Azure Linux 에이전트](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 대한 Docker VM 확장을 사용하여 Azure에 응용 프로그램의 컨테이너를 개수에 제한없이 호스트하는 Docker VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-110">You can use the Docker VM extension and the [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="cc38d-111">컨테이너와 해당 이점에 대한 간략한 설명을 확인하려면 [Docker 요약 화이트보드](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc38d-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-to-use-the-docker-vm-extension-with-azure"></a><span data-ttu-id="cc38d-112">Azure와 함께 Docker VM 확장을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="cc38d-112">How to use the Docker VM Extension with Azure</span></span>
<span data-ttu-id="cc38d-113">Azure와 함께 Docker VM 확장을 사용하려면 [Azure 명령줄 인터페이스](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) 0.8.6 이상 버전을 설치해야 합니다(이 문서를 작성할 당시 현재 버전은 0.10.0임).</span><span class="sxs-lookup"><span data-stu-id="cc38d-113">To use the Docker VM extension with Azure, you must install a version of the [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing the current version is 0.10.0).</span></span> <span data-ttu-id="cc38d-114">Mac, Linux 및 Windows에 Azure CLI를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-114">You can install the Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="cc38d-115">Azure에서 Docker를 사용하는 전체 프로세스는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-115">The complete process to use Docker on Azure is simple:</span></span>

* <span data-ttu-id="cc38d-116">Azure를 제어하려는 컴퓨터(Windows의 경우 가상 컴퓨터로 실행 중인 Linux 배포임)에 Azure CLI와 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-116">Install the Azure CLI and its dependencies on the computer from which you want to control Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="cc38d-117">Azure CLI Docker 명령을 사용하여 Azure에 VM Docker 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-117">Use the Azure CLI Docker commands to create a VM Docker host in Azure</span></span>
* <span data-ttu-id="cc38d-118">로컬 Docker 명령을 사용하여 Azure의 Docker VM에서 Docker 컨테이너를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-118">Use the local Docker commands to manage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="cc38d-119">Azure 명령줄 인터페이스(Azure CLI) 설치</span><span class="sxs-lookup"><span data-stu-id="cc38d-119">Install the Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="cc38d-120">Azure CLI를 설치하고 구성하려면, [Azure 명령줄 인터페이스를 설치하는 방법](../../../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc38d-120">To install and configure the Azure CLI, see [How to install the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="cc38d-121">설치를 확인하려면 명령줄에 `azure`를 입력합니다. 잠시 후에 사용 가능한 기본 명령을 나열하는 Azure CLI ASCII 아트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-121">To confirm the installation, type `azure` at the command prompt and after a short moment you should see the Azure CLI ASCII art, which lists the basic commands available to you.</span></span> <span data-ttu-id="cc38d-122">설치가 제대로 작동한 경우 `azure help vm`을 입력하면 나열된 명령 중 하나가 "docker"임을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-122">If the installation worked correctly, you should be able to type `azure help vm` and see that one of the listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="cc38d-123">Docker에 Windows용 도구, [Docker Machine](https://docs.docker.com/installation/windows/)이 있으며, docker 호스트로 Azure VM과 작업에 사용할 수 있는 docker 클라이언트 작성을 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use to automate the creation of a docker client that you can use to work with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-the-azure-cli-to-to-your-azure-account"></a><span data-ttu-id="cc38d-124">Azure CLI를 Azure 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="cc38d-124">Connect the Azure CLI to to your Azure Account</span></span>
<span data-ttu-id="cc38d-125">Azure CLI를 사용하려면 먼저 Azure 계정 자격 증명을 사용자 플랫폼의 Azure CLI에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-125">Before you can use the Azure CLI you must associate your Azure account credentials with the Azure CLI on your platform.</span></span> <span data-ttu-id="cc38d-126">[Azure 구독에 연결하는 방법](../../../xplat-cli-connect.md) 섹션에서 **.publishsettings** 파일을 다운로드하고 가져오거나 Azure CLI를 조직 ID에 연결하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-126">The section [How to connect to your Azure subscription](../../../xplat-cli-connect.md) explains how to either download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="cc38d-127">사용하는 인증 방법에 따라 동작에 몇 가지 차이점이 있으므로 위 문서를 읽고 서로 다른 기능을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-127">There are some differences in behavior when using one or the other methods of authentication, so do be sure to read the document above to understand the different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-the-docker-vm-extension-for-azure"></a><span data-ttu-id="cc38d-128">Docker 설치 및 Azure용 Docker VM 확장 사용</span><span class="sxs-lookup"><span data-stu-id="cc38d-128">Install Docker and use the Docker VM Extension for Azure</span></span>
<span data-ttu-id="cc38d-129">사용자 컴퓨터에 Docker를 로컬로 설치하려면 [Docker 설치 지침](https://docs.docker.com/installation/#installation) 을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="cc38d-129">Follow the [Docker installation instructions](https://docs.docker.com/installation/#installation) to install Docker locally on your computer.</span></span>

<span data-ttu-id="cc38d-130">Azure 가상 컴퓨터에서 Docker를 사용하려면 VM에 사용하는 Linux 이미지에 [Azure Linux VM 에이전트](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-130">To use Docker with an Azure Virtual Machine, the Linux image used for the VM must have the [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="cc38d-131">현재 이 에이전트를 설치할 수 있는 이미지의 유형은 다음의 두 가지뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="cc38d-132">Azure 이미지 갤러리의 Ubuntu 이미지 또는</span><span class="sxs-lookup"><span data-stu-id="cc38d-132">An Ubuntu image from the Azure Image Gallery or</span></span>
* <span data-ttu-id="cc38d-133">Azure Linux VM 에이전트를 설치 및 구성하여 만든 사용자 지정 Linux 이미지.</span><span class="sxs-lookup"><span data-stu-id="cc38d-133">A custom Linux image that you have created with the Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="cc38d-134">Azure VM 에이전트로 사용자 지정 Linux VM을 빌드하는 방법에 대한 자세한 내용은 [Azure Linux VM 에이전트](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc38d-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how to build a custom Linux VM with the Azure VM Agent.</span></span>

### <a name="using-the-azure-image-gallery"></a><span data-ttu-id="cc38d-135">Azure 이미지 갤러리 사용</span><span class="sxs-lookup"><span data-stu-id="cc38d-135">Using the Azure Image Gallery</span></span>
<span data-ttu-id="cc38d-136">Bash 또는 터미널 세션에서 다음 Azure CLI 명령을 사용하여 VM 갤러리에서 사용하려는 최신 Ubuntu 이미지를 찾아 다음을 입력하여 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-136">From a Bash or Terminal session, use the following Azure CLI command to locate the most recent Ubuntu image in the VM gallery to use by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="cc38d-137">`b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`와 같은 이미지 이름 중 하나를 선택한 후에 다음 명령을 사용하여 해당 이미지를 사용하는 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-137">and select one of the image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use the following command to create a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="cc38d-138">설명:</span><span class="sxs-lookup"><span data-stu-id="cc38d-138">where:</span></span>

* <span data-ttu-id="cc38d-139">*&lt;vm-cloudservice name&gt;*은 Azure에서 Docker 컨테이너 호스트 컴퓨터로 사용할 VM의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-139">*&lt;vm-cloudservice name&gt;* is the name of the VM that will become the Docker container host computer in Azure</span></span>
* <span data-ttu-id="cc38d-140">*&lt;username&gt;* 은 VM의 기본 루트 사용자의 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-140">*&lt;username&gt;* is the username of the default root user of the VM</span></span>
* <span data-ttu-id="cc38d-141">*&lt;password&gt;*는 Azure의 복잡성 표준을 충족하는 *username* 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-141">*&lt;password&gt;* is the password of the *username* account that meets the standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="cc38d-142">현재 암호는 8자 이상이어야 하며 소문자, 대문자, 숫자 및 다음 문자 중 하나와 같은 특수 문자를 각각 한 개씩 포함해야 합니다. `!@#$%^&+=`</span><span class="sxs-lookup"><span data-stu-id="cc38d-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of the following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="cc38d-143">앞의 문장에서 끝에 있는 마침표는 특수 문자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-143">No, the period at the end of the preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="cc38d-144">명령이 성공한 경우 사용한 정확한 인수와 옵션에 따라 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-144">If the command was successful, you should see something like the following, depending on the precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="cc38d-145">가상 컴퓨터를 만들려면 몇 분 정도 걸릴 수 있습니다. 가상 컴퓨터가 프로비전된 후에는(상태 값 `ReadyRole`) Docker 데몬(Docker 서비스)이 시작되며 Docker 컨테이너 호스트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (the state value is `ReadyRole`) the Docker daemon (the Docker service) starts and you can connect to the Docker container host.</span></span>
> 
> 

<span data-ttu-id="cc38d-146">Azure에 만든 Docker VM을 테스트하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-146">To test the Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="cc38d-147">여기서 *&lt;vm-name-you-used&gt;*는 `azure vm docker create`를 호출하는 데 사용한 가상 컴퓨터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-147">where *&lt;vm-name-you-used&gt;* is the name of the virtual machine that you used in your call to `azure vm docker create`.</span></span> <span data-ttu-id="cc38d-148">다음과 같은 결과가 표시됩니다. 이 결과는 Azure에서 Docker 호스트 VM이 작동하여 실행 중이며 명령을 기다리고 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-148">You should see something similar to the following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="cc38d-149">이제 정보를 얻기 위해 Docker 클라이언트를 사용하여 연결을 시도할 수 있습니다(Mac과 같은 일부 Docker 클라이언트 설정에서는 `sudo`를 사용해야 할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="cc38d-149">Now you can try to connect using your docker client to obtain information (in some Docker client setups, such as that on Mac, you may have to use `sudo`):</span></span>

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

<span data-ttu-id="cc38d-150">모두 작동하고 있는지 확인하기 위해 VM의 Docker 확장을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-150">Just to be certain that it's all working, you can examine the VM for the Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="cc38d-151">Docker Host VM 인증</span><span class="sxs-lookup"><span data-stu-id="cc38d-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="cc38d-152">Docker VM을 만드는 것뿐만 아니라 `azure vm docker create` 명령은 Docker 클라이언트 컴퓨터가 HTTPS를 사용하여 Azure 컨테이너 호스트에 연결할 수 있도록 필요한 인증서도 자동으로 만듭니다. 인증서는 해당하는 경우 클라이언트와 호스트 컴퓨터 둘 다에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-152">In addition to creating the Docker VM, the `azure vm docker create` command also automatically creates the necessary certificates to allow your Docker client computer to connect to the Azure container host using HTTPS, and the certificates are stored on both the client and host machines, as appropriate.</span></span> <span data-ttu-id="cc38d-153">이후에 시도할 때는 기존 인증서가 다시 사용되며 새 호스트와 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-153">On subsequent attempts, the existing certificates are reused and shared with the new host.</span></span>

<span data-ttu-id="cc38d-154">기본적으로 인증서는 `~/.docker`에 배치되고 Docker는 포트 **2376**에서 실행되도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-154">By default, certificates are placed in `~/.docker`, and Docker will be configured to run on port **2376**.</span></span> <span data-ttu-id="cc38d-155">다른 포트나 디렉터리를 사용하려는 경우 다음 `azure vm docker create` 명령줄 옵션 중 하나를 사용하여 클라이언트 연결에 다른 포트나 다른 인증서를 사용하도록 Docker 컨테이너 호스트 VM을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-155">If you would like to use a different port or directory, then you may use one of the following `azure vm docker create` command line options to configure your Docker container host VM to use a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port to use for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="cc38d-156">호스트의 Docker 데몬은 `azure vm docker create` 명령에서 생성된 인증서를 사용하여 지정된 포트에서 클라이언트 연결을 수신 대기하고 인증하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-156">The Docker daemon on the host is configured to listen for and authenticate client connections on the specified port using the certificates generated by the `azure vm docker create` command.</span></span> <span data-ttu-id="cc38d-157">클라이언트 컴퓨터가 Docker 호스트에 액세스하려면 해당 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-157">The client machine must have these certificates to gain access to the Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="cc38d-158">해당 인증서 없이 실행되는 네트워크 호스트는 컴퓨터에 연결할 수 있는 모든 사용자에게 취약합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-158">A networked host running without these certificates will be vulnerable to anyone that can to connect to the machine.</span></span> <span data-ttu-id="cc38d-159">기본 구성을 수정하기 전에 컴퓨터와 응용 프로그램에 대한 위험을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-159">Before you modify the default configuration, ensure that you understand the risks to your computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cc38d-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc38d-160">Next steps</span></span>
* <span data-ttu-id="cc38d-161">이제 [Docker 사용자 가이드] 로 이동하여 Docker VM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-161">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="cc38d-162">새 포털에서 Docker 사용 가능 VM을 만들려면 [포털에서 Docker VM 확장을 사용하는 방법]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc38d-162">To create a Docker-enabled VM in the new portal, see [How to use the Docker VM Extension with the Portal].</span></span>
* <span data-ttu-id="cc38d-163">Azure Docker VM 확장은 또한 개발자 모델링된 응용 프로그램을 모든 환경에 가져가고 일관된 배포를 생성하기 위해 선언적 YAML 파일을 사용하는 Docker Compose를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cc38d-163">The Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file to take a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="cc38d-164">[Azure 가상 컴퓨터에서 다중 컨테이너 응용 프로그램 정의 및 실행을 위해 Docker 및 Compose 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc38d-164">See [Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How to use the Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 to another azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 to another azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md
<span data-ttu-id="cc38d-165">[포털에서 Docker VM 확장을 사용하는 방법]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span><span class="sxs-lookup"><span data-stu-id="cc38d-165">[How to use the Docker VM Extension with the Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span></span>

<span data-ttu-id="cc38d-166">[Docker 사용자 가이드]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="cc38d-166">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>

<span data-ttu-id="cc38d-167">[Azure 가상 컴퓨터에서 다중 컨테이너 응용 프로그램 정의 및 실행을 위해 Docker 및 Compose 시작]:../docker-compose-quickstart.md</span><span class="sxs-lookup"><span data-stu-id="cc38d-167">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine]:../docker-compose-quickstart.md</span></span>
