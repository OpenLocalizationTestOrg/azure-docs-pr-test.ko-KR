---
title: "Linux 용 Docker VM 확장 aaaUsing | Microsoft Docs"
description: "Docker 및 hello Azure 가상 컴퓨터 확장 및 클래식 배포 모델에서 toocreate Azure 가상 컴퓨터의 docker 호스트를 사용 하 여 Azure CLI hello 하는 방법을 설명 합니다."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="654b0-103">Azure 클래식 포털 hello로 hello Docker VM 확장을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="654b0-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="654b0-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="654b0-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="654b0-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="654b0-107">[Docker](https://www.docker.com/) hello 중 하나를 사용 하는 가장 인기 있는 가상화 방법입니다. [Linux 컨테이너](http://en.wikipedia.org/wiki/LXC) 데이터 격리 하 고 공유 리소스에서 계산 하는 방법으로 가상 컴퓨터 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="654b0-108">관리 하는 hello Docker VM 확장을 사용할 수 있습니다 [Azure Linux 에이전트] toocreate 개수에 관계 없이 Azure에서 응용 프로그램에 대 한 컨테이너를 호스트 하는 Docker VM입니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="654b0-109">이 항목에서 Docker VM a toocreate Azure 클래식 포털 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="654b0-110">hello 명령줄에서 Docker VM toocreate 참조 toosee [toouse hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장을 hello 하는 방법을]합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="654b0-111">높은 수준의 컨테이너와 그 장점을 설명 toosee 참조 hello [Docker 높은 수준 화이트 보드](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="654b0-112">Hello 이미지 갤러리에서에서 새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="654b0-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="654b0-113">hello 첫 번째 단계는 Azure VM hello 예제 서버 이미지 및 Ubuntu 14.04 데스크톱으로 hello 이미지 갤러리에서에서 Ubuntu 14.04 LTS 이미지를 사용 하 여 클라이언트로 Docker VM 확장을 지 원하는 Linux 이미지에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="654b0-114">Hello 포털에서 클릭 **+ 새로 만들기** 의 hello 하단 왼쪽 모서리 toocreate 새 VM 인스턴스 고 hello 또는 hello 선택할 수 있는 항목이에서 Ubuntu 14.04 LTS 이미지를 선택 아래와 같이 이미지 갤러리를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="654b0-115">현재 2014 년 7 월 보다 더 최신 Ubuntu 14.04 LTS 이미지만 hello Docker VM 확장을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![새 Ubuntu 이미지 만들기](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="654b0-117">Docker 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="654b0-117">Create Docker Certificates</span></span>
<span data-ttu-id="654b0-118">VM을 만든 hello, 후 클라이언트 컴퓨터에 Docker가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="654b0-119">자세한 내용은 [Docker 설치 지침](https://docs.docker.com/installation/#installation)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654b0-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="654b0-120">Hello 너무에 따라 Docker 통신에 대 한 인증서 및 키 파일을 만들[https로 Docker 실행] hello 안에 위치 시켜야합니다  **`~/.docker`**  클라이언트 컴퓨터에 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="654b0-121">hello 포털에 hello Docker VM 확장에는 현재 base64 인코딩 되는 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="654b0-122">Hello 명령줄에서 사용 하 여  **`base64`**  또는 다른 즐겨찾기 tool toocreate base64 인코딩된 항목 인코딩.</span><span class="sxs-lookup"><span data-stu-id="654b0-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="654b0-123">인증서 및 키 파일의 간단한 집합으로이 작업을 수행 하면 비슷한 toothis 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="654b0-124">Hello Docker VM 확장 추가</span><span class="sxs-lookup"><span data-stu-id="654b0-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="654b0-125">tooadd hello Docker VM 확장을 만들었으므로 hello VM 인스턴스를 찾아서 너무 아래로 스크롤하여**확장** 아래와 같이 toobring VM 확장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="654b0-126">이 기능은 hello 미리 보기 포털에서 지원 됩니다: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="654b0-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="654b0-127">확장 추가</span><span class="sxs-lookup"><span data-stu-id="654b0-127">Add an Extension</span></span>
<span data-ttu-id="654b0-128">Hello 클릭 **+ 추가** toodisplay hello 가능한 VM 확장 toothis VM을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="654b0-129">Hello Docker VM 확장을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="654b0-130">Hello hello Docker 설명 및 중요 링크 되면서 Docker VM 확장을 선택 하 고 클릭 한 다음 **만들기** hello 아래쪽 toobegin hello 설치 절차에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="654b0-131">인증서 및 키 파일 추가</span><span class="sxs-lookup"><span data-stu-id="654b0-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="654b0-132">Hello 양식 필드의 hello 다음 그래픽에에서 표시 된 대로 hello base64 인코딩된 버전의 CA 인증서, 해당 서버 인증서 및 서버 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="654b0-133">참고는 (예: hello 이미지 이전) hello 2376은 기본적으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="654b0-134">여기에서 모든 끝점을 입력할 수 있습니다 하지만 hello 다음 단계를 끝점에 일치 하는 hello tooopen 됩니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="654b0-135">Hello 기본값을 변경 하는 경우 있는지 tooopen hello 끝점 hello 다음 단계에서 일치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="654b0-136">Hello Docker 통신 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="654b0-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="654b0-137">만든 hello 리소스 그룹을 볼 때 hello VM과와 연결 된 네트워크 보안 그룹을 선택 하 고 클릭 **인바운드 보안 규칙** tooview hello 규칙 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="654b0-138">클릭 **+ 추가** tooadd 규칙 다른 hello 기본적인 경우에서 hello 끝점에 대 한 이름을 입력 합니다 (이 예제에서는 **Docker**), 및 2376 대상 ' 포트 범위 '.</span><span class="sxs-lookup"><span data-stu-id="654b0-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="654b0-139">Hello 프로토콜 보여 주는 값을 설정 **TCP**를 클릭 하 고 **확인** toocreate hello 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="654b0-140">Docker 클라이언트 및 Azure Docker 호스트 테스트</span><span class="sxs-lookup"><span data-stu-id="654b0-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="654b0-141">찾아 hello 형식 클라이언트 컴퓨터의 명령줄에서 VM의 도메인의 hello 이름을 복사 `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (여기서 *dockerextension* hello로 대체 됩니다 하위 도메인 VM에 대 한)입니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="654b0-142">hello 결과 유사한 toothis 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-142">hello result should appear similar toothis:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="654b0-143">Hello 단계를 완료 한 후 해야 구성 하는 Azure VM에서 실행 되는 모든 기능을 갖춘 Docker 호스트 toobe 다른 클라이언트에서 tooremotely 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="654b0-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="654b0-144">Next steps</span></span>
<span data-ttu-id="654b0-145">준비 toogo toohello는 [Docker 사용자 가이드] Docker VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b0-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="654b0-146">명령줄 인터페이스를 통해 Azure Vm에서 Docker 호스트를 만드는 tooautomate 참조 [toouse hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장을 hello 하는 방법을]</span><span class="sxs-lookup"><span data-stu-id="654b0-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[toouse hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장을 hello 하는 방법을]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Azure Linux 에이전트]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[https로 Docker 실행]:http://docs.docker.com/articles/https/
[Docker 사용자 가이드]:https://docs.docker.com/userguide/
