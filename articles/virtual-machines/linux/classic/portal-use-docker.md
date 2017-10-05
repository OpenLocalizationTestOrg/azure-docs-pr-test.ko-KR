---
title: "Linux용 Docker VM 확장 사용 | Microsoft Docs"
description: "Docker 및 Azure 가상 컴퓨터 확장에 대해 설명하고, 클래식 배포 모델에서 Azure CLI를 사용하는 Docker 호스트인 Azure 가상 컴퓨터를 만드는 방법을 안내합니다."
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
ms.openlocfilehash: 932744208d9d53c87e31dcdf9e34539750be4bdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-with-the-azure-classic-portal"></a><span data-ttu-id="123f9-103">Azure 클래식 포털에서 Docker VM 확장 사용</span><span class="sxs-lookup"><span data-stu-id="123f9-103">Using the Docker VM Extension with the Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="123f9-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="123f9-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="123f9-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="123f9-107">[Docker](https://www.docker.com/)는 공유 리소스의 데이터와 계산을 격리시키는 한 가지 방법으로 가상 컴퓨터 대신 [Linux 컨테이너](http://en.wikipedia.org/wiki/LXC)를 사용하는 가장 많이 사용되는 가상화 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-107">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="123f9-108">[Azure Linux 에이전트] 에서 관리되는 Docker VM 확장을 사용하여 Azure에 응용 프로그램의 컨테이너를 개수에 제한 없이 호스트하는 Docker VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-108">You can use the Docker VM extension managed by [Azure Linux Agent] to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="123f9-109">이 항목에서는 Azure 클래식 포털에서 Docker VM을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-109">This topic describes how to create a Docker VM from the Azure classic portal.</span></span> <span data-ttu-id="123f9-110">명령줄에서 Docker VM을 만드는 방법을 확인하려면 [Azure 명령줄 인터페이스(Azure CLI)에서 Docker VM 확장을 사용하는 방법]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="123f9-110">To see how to create a Docker VM at the command line, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="123f9-111">컨테이너와 해당 이점에 대한 간략한 설명을 확인하려면 [Docker 요약 화이트보드](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="123f9-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-the-image-gallery"></a><span data-ttu-id="123f9-112">이미지 갤러리에서 새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="123f9-112">Create a new VM from the Image Gallery</span></span>
<span data-ttu-id="123f9-113">첫 단계를 수행하려면 Docker VM 확장을 지원하는 Linux 이미지의 Azure VM이 필요합니다. 여기서는 이미지 갤러리의 Ubuntu 14.04 LTS 이미지를 예제 서버 이미지로, Ubuntu 14.04 Desktop을 클라이언트로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-113">The first step requires an Azure VM from a Linux image that supports the Docker VM Extension, using an Ubuntu 14.04 LTS image from the Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="123f9-114">포털의 왼쪽 아래에서 **+ 새로 만들기**를 클릭하여 새 VM 인스턴스를 만들고 아래에 나와 있는 것처럼 선택 가능한 항목 또는 전체 이미지 갤러리에서 Ubuntu 14.04 LTS 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-114">In the portal, click **+ New** in the bottom left corner to create a new VM instance and select an Ubuntu 14.04 LTS image from the selections available or from the complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="123f9-115">현재는 2014년 7월 이후의 Ubuntu 14.04 LTS 이미지만이 Docker VM 확장을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support the Docker VM Extension.</span></span>
> 
> 

![새 Ubuntu 이미지 만들기](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="123f9-117">Docker 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="123f9-117">Create Docker Certificates</span></span>
<span data-ttu-id="123f9-118">VM을 만든 후에는 클라이언트 컴퓨터에 Docker가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-118">After the VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="123f9-119">자세한 내용은 [Docker 설치 지침](https://docs.docker.com/installation/#installation)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="123f9-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="123f9-120">[https를 사용하여 Docker 실행]의 지침에 따라 Docker 통신용 인증서 및 키 파일을 만든 다음 클라이언트 컴퓨터의 **`~/.docker`** 디렉터리에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-120">Create the certificate and key files for Docker communication according to [Running Docker with https] and place them in the **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="123f9-121">현재는 포털의 Docker VM 확장을 사용하려면 base64로 인코딩된 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-121">The Docker VM Extension in the portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="123f9-122">명령줄에서 **`base64`** 또는 기타 인코딩 도구를 사용하여 base64 인코딩 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-122">At the command line, use **`base64`** or another favorite encoding tool to create base64-encoded topics.</span></span> <span data-ttu-id="123f9-123">아래에는 간단한 인증서 및 키 파일 집합을 사용하는 이 작업의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-123">Doing this with a simple set of certificate and key files might look similar to this:</span></span>

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

## <a name="add-the-docker-vm-extension"></a><span data-ttu-id="123f9-124">Docker VM 확장 추가</span><span class="sxs-lookup"><span data-stu-id="123f9-124">Add the Docker VM Extension</span></span>
<span data-ttu-id="123f9-125">Docker VM 확장을 추가하려면 앞에서 만든 VM 인스턴스를 찾은 다음 아래쪽의 **확장**으로 스크롤하여 확장을 클릭합니다. 그러면 아래와 같이 VM 확장이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-125">To add the Docker VM Extension, locate the VM instance you created and scroll down to **Extensions** and click it to bring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="123f9-126">이 기능은 미리 보기 포털에서만 지원됩니다. https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="123f9-126">This functionality is supported in the preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="123f9-127">확장 추가</span><span class="sxs-lookup"><span data-stu-id="123f9-127">Add an Extension</span></span>
<span data-ttu-id="123f9-128">**+ 추가** 를 클릭하여 이 VM에 추가할 수 있는 VM 확장을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-128">Click the **+ Add** to display the possible VM Extensions you can add to this VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-the-docker-vm-extension"></a><span data-ttu-id="123f9-129">Docker VM 확장 선택</span><span class="sxs-lookup"><span data-stu-id="123f9-129">Select the Docker VM Extension</span></span>
<span data-ttu-id="123f9-130">Docker VM 확장을 선택하면 Docker 설명 및 중요 링크가 표시됩니다. 그러면 아래쪽의 **만들기**를 클릭하여 설치 절차를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-130">Choose the Docker VM Extension, which brings up the Docker description and important links, and then click **Create** at the bottom to begin the installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="123f9-131">인증서 및 키 파일 추가</span><span class="sxs-lookup"><span data-stu-id="123f9-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="123f9-132">다음 그림에 나와 있는 것처럼 양식 필드에서 CA 인증서, 서버 인증서 및 서버 키의 base64 인코딩 버전을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-132">In the form fields, enter the base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in the following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="123f9-133">위의 이미지에 나와 있는 것처럼 포트에는 기본적으로 2376이 입력되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-133">Note that (as in the preceding image) the 2376 is filled in by default.</span></span> <span data-ttu-id="123f9-134">여기에는 원하는 어떤 끝점이든 입력할 수 있지만 다음 단계에서 일치하는 끝점을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-134">You can enter any endpoint here, but the next step will be to open up the matching endpoint.</span></span> <span data-ttu-id="123f9-135">기본값을 변경하는 경우에는 다음 단계에서 일치하는 끝점을 여세요.</span><span class="sxs-lookup"><span data-stu-id="123f9-135">If you change the default, make sure to open up the matching endpoint in the next step.</span></span>
> 
> 

## <a name="add-the-docker-communication-endpoint"></a><span data-ttu-id="123f9-136">Docker 통신 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="123f9-136">Add the Docker Communication Endpoint</span></span>
<span data-ttu-id="123f9-137">만든 리소스 그룹을 볼 경우, 여기에 표시된 대로 VM에 연결된 네트워크 보안 그룹을 선택하고 **인바운드 보안 규칙** 을 클릭하여 규칙을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-137">When viewing the resource group you've created, select the Network Security Group associated with your VM, and click **Inbound Security Rules** to view the rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="123f9-138">**+ 추가**를 클릭하여 다른 규칙을 추가합니다. 기본 규칙의 경우 끝점 이름을 입력하고(이 예제에서는 **Docker**) 및 2376 '대상 포트 범위'를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-138">Click **+ Add** to add another rule, and in the default case, enter a name for the endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="123f9-139">프로토콜 값은 **TCP**를 표시하도록 설정하고 **확인**을 클릭하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-139">Set the protocol value showing **TCP**, and Click **OK** to create the rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="123f9-140">Docker 클라이언트 및 Azure Docker 호스트 테스트</span><span class="sxs-lookup"><span data-stu-id="123f9-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="123f9-141">VM 도메인의 이름을 찾아서 복사한 다음 클라이언트 컴퓨터의 명령줄에 `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info`을 입력합니다. 여기서 *dockerextension*은 VM의 하위 도메인으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-141">Locate and copy the name of your VM's domain, and at the command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by the subdomain for your VM).</span></span>

<span data-ttu-id="123f9-142">결과는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-142">The result should appear similar to this:</span></span>

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

<span data-ttu-id="123f9-143">위 단계를 완료했으면 이제 다른 클라이언트에서 원격으로 연결하도록 구성된 완전한 기능의 Docker 호스트가 Azure VM에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-143">Once you complete the above steps, you now have a fully functional Docker host running on an Azure VM, configured to be connected to remotely from other clients.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="123f9-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="123f9-144">Next steps</span></span>
<span data-ttu-id="123f9-145">이제 [Docker 사용자 가이드] 로 이동하여 Docker VM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="123f9-145">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="123f9-146">명령줄 인터페이스를 통해 Azure VM에서 Docker 호스트를 자동으로 만들려면 [Azure 명령줄 인터페이스(Azure CLI)에서 Docker VM 확장을 사용하는 방법]</span><span class="sxs-lookup"><span data-stu-id="123f9-146">If you want to automate creating Docker hosts on Azure VMs through command line interface, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from the Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add the Docker VM Extension]:#adddockerextension
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
<span data-ttu-id="123f9-147">[Azure 명령줄 인터페이스(Azure CLI)에서 Docker VM 확장을 사용하는 방법]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span><span class="sxs-lookup"><span data-stu-id="123f9-147">[How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span></span>
<span data-ttu-id="123f9-148">[Azure Linux 에이전트]:../agent-user-guide.md</span><span class="sxs-lookup"><span data-stu-id="123f9-148">[Azure Linux Agent]:../agent-user-guide.md</span></span>
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md

<span data-ttu-id="123f9-149">[https를 사용하여 Docker 실행]:http://docs.docker.com/articles/https/</span><span class="sxs-lookup"><span data-stu-id="123f9-149">[Running Docker with https]:http://docs.docker.com/articles/https/</span></span>
<span data-ttu-id="123f9-150">[Docker 사용자 가이드]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="123f9-150">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>
