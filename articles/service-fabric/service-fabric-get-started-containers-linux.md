---
title: "Linux에서 Azure 서비스 패브릭 컨테이너 응용 프로그램 aaaCreate | Microsoft Docs"
description: "Azure Service Fabric에서 첫 번째 Linux 컨테이너 응용 프로그램을 만듭니다.  응용 프로그램과 함께 Docker 이미지를 작성, hello 이미지 tooa 컨테이너 레지스트리 푸시, 빌드 및 서비스 패브릭 컨테이너 응용 프로그램을 배포 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="4f9a9-104">Linux에서 첫 번째 Service Fabric 컨테이너 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4f9a9-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f9a9-105">Windows</span><span class="sxs-lookup"><span data-stu-id="4f9a9-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="4f9a9-106">Linux</span><span class="sxs-lookup"><span data-stu-id="4f9a9-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="4f9a9-107">서비스 패브릭 클러스터에 Linux 컨테이너에서 기존 응용 프로그램을 실행 하면 모든 변경 내용을 tooyour 응용 프로그램이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="4f9a9-108">이 문서에서는 Python을 포함 하는 Docker 이미지를 만드는 과정 [플라스](http://flask.pocoo.org/) 웹 응용 프로그램 및 tooa 서비스 패브릭 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="4f9a9-109">또한 [Azure Container Registry](/azure/container-registry/)를 통해 컨테이너화된 응용 프로그램을 공유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="4f9a9-110">이 문서에서는 Docker에 대한 기본적으로 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="4f9a9-111">읽는 hello 하 여 Docker에 알아볼 수 있습니다 [Docker 개요](https://docs.docker.com/engine/understanding-docker/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f9a9-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4f9a9-112">Prerequisites</span></span>
* <span data-ttu-id="4f9a9-113">다음을 실행하는 개발 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="4f9a9-113">A development computer running:</span></span>
  * <span data-ttu-id="4f9a9-114">[Service Fabric SDK 및 도구](service-fabric-get-started-linux.md)</span><span class="sxs-lookup"><span data-stu-id="4f9a9-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="4f9a9-115">[Linux용 Docker CE](https://docs.docker.com/engine/installation/#prior-releases)</span><span class="sxs-lookup"><span data-stu-id="4f9a9-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="4f9a9-116">Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="4f9a9-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="4f9a9-117">Azure Container Registry의 레지스트리 - Azure 구독 내에서 [컨테이너 레지스트리를 만듭니다](../container-registry/container-registry-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4f9a9-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="4f9a9-118">Hello Docker 컨테이너를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-118">Define hello Docker container</span></span>
<span data-ttu-id="4f9a9-119">Hello를 기반으로 이미지 빌드 [Python 이미지](https://hub.docker.com/_/python/) Docker 허브에 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="4f9a9-120">Dockerfile에서 Docker 컨테이너를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="4f9a9-121">Dockerfile hello 컨테이너 내 hello 환경 설정 toorun, 원하는 hello 응용 프로그램을 로드 하 고 포트 매핑 하기 위한 지침이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="4f9a9-122">Dockerfile hello는 hello 입력된 toohello `docker build` 명령을 hello 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="4f9a9-123">빈 디렉터리를 만들고 hello 파일을 만들 *Dockerfile* (확장명이 없는 파일).</span><span class="sxs-lookup"><span data-stu-id="4f9a9-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="4f9a9-124">Hello 너무 다음 추가*Dockerfile* 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-124">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="4f9a9-125">읽기 hello [Dockerfile 참조](https://docs.docker.com/engine/reference/builder/) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="4f9a9-126">간단한 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4f9a9-126">Create a simple web application</span></span>
<span data-ttu-id="4f9a9-127">"Hello World!"를 반환하는 포트 80에서 수신 대기하는 Flask 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="4f9a9-128">동일한 디렉터리 hello 하 hello 파일을 만들 *requirements.txt*합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="4f9a9-129">Hello 다음 추가 하 고 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="4f9a9-130">Hello를 만들 수도 *app.py* 파일을 hello 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="4f9a9-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="4f9a9-131">Hello 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="4f9a9-131">Build hello image</span></span>
<span data-ttu-id="4f9a9-132">Hello 실행 `docker build` 웹 응용 프로그램을 실행 하는 명령 toocreate hello 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="4f9a9-133">PowerShell 창을 열고 너무 이동*c:\temp\helloworldapp*합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="4f9a9-134">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="4f9a9-135">이 명령은 빌드 hello 프로그램 Dockerfile의 hello 지침을 사용 하 여 새 이미지 이름 지정 (-t 태그 지정) hello 이미지 "helloworldapp"입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="4f9a9-136">이미지 hello 기본 이미지를 Docker 허브에서 끌어와 빌드하고 hello 기본 이미지를 기반으로 응용 프로그램을 추가 하는 새 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="4f9a9-137">Hello 빌드 명령이 완료 되 면 실행 hello `docker images` 명령 hello 새 이미지에 toosee 정보:</span><span class="sxs-lookup"><span data-stu-id="4f9a9-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="4f9a9-138">Hello 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="4f9a9-138">Run hello application locally</span></span>
<span data-ttu-id="4f9a9-139">컨테이너 화 된 응용 프로그램 hello 컨테이너 레지스트리 푸시하여 하기 전에 로컬로 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="4f9a9-140">Hello 응용 프로그램을 실행 하면 포트 80 노출 컴퓨터의 포트 4000 toohello 컨테이너 매핑:</span><span class="sxs-lookup"><span data-stu-id="4f9a9-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="4f9a9-141">*이름* (hello 컨테이너 ID)가 아닌 컨테이너를 실행 하는 이름을 toohello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="4f9a9-142">컨테이너를 실행 하는 toohello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-142">Connect toohello running container.</span></span>  <span data-ttu-id="4f9a9-143">예를 들어 "http://localhost:4000" 4000, 포트에서 반환 된 toohello IP 주소를 가리키는 웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="4f9a9-144">"Hello World!" 제목 hello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="4f9a9-145">hello 브라우저에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-145">display in hello browser.</span></span>

![Hello World!][hello-world]

<span data-ttu-id="4f9a9-147">toostop 컨테이너를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="4f9a9-148">개발 컴퓨터에서 hello 컨테이너를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="4f9a9-149">푸시 hello 이미지 toohello 컨테이너 레지스트리</span><span class="sxs-lookup"><span data-stu-id="4f9a9-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="4f9a9-150">Docker에서 hello 응용 프로그램 실행 되는지 확인 한 후 Azure 컨테이너 레지스트리에 hello 이미지 tooyour 레지스트리를 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="4f9a9-151">실행 `docker login` 와 tooyour 컨테이너 레지스트리에 toolog 프로그램 [레지스트리 자격 증명](../container-registry/container-registry-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="4f9a9-152">hello 다음 예제에서는 전달 hello ID와 Azure Active Directory의 암호 [서비스 사용자](../active-directory/active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="4f9a9-153">예를 들어 수 할당 했는지 자동화 시나리오에 대 한 서비스 주체 tooyour 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="4f9a9-154">또는 레지스트리 사용자 이름과 암호를 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="4f9a9-155">hello 다음 명령은 태그 또는 hello 이미지의 별칭으로 정규화 된 경로 tooyour 레지스트리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="4f9a9-156">이 예에서는 위치 hello hello에 이미지 `samples` hello 레지스트리 hello 루트 네임 스페이스 tooavoid 좀 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="4f9a9-157">푸시 hello 이미지 tooyour 컨테이너 레지스트리:</span><span class="sxs-lookup"><span data-stu-id="4f9a9-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="4f9a9-158">Yeoman 사용 하 여 패키지 hello Docker 이미지</span><span class="sxs-lookup"><span data-stu-id="4f9a9-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="4f9a9-159">hello Linux에 대 한 서비스 패브릭 SDK에 포함 되어는 [Yeoman](http://yeoman.io/) 생성기를 쉽게 toocreate를 사용 하면 응용 프로그램 컨테이너 이미지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="4f9a9-160">Yeoman toocreate 라는 단일 Docker 컨테이너와 응용 프로그램을 사용 하 여 보겠습니다 *SimpleContainerApp*합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="4f9a9-161">서비스 패브릭 컨테이너 응용 프로그램 toocreate 터미널 윈도우를 열고 실행 `yo azuresfcontainer`합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="4f9a9-162">응용 프로그램 이름을 지정합니다(예: "mycontainer").</span><span class="sxs-lookup"><span data-stu-id="4f9a9-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="4f9a9-163">컨테이너 레지스트리에 hello 컨테이너 이미지에 대 한 hello URL을 제공 (예를 들어, "").</span><span class="sxs-lookup"><span data-stu-id="4f9a9-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="4f9a9-164">이 이미지에는 작업이 진입점 정의 따라서 필요 tooexplicitly 입력된 명령을 지정 (명령 hello 컨테이너를 시작 하 고 나면 실행은 유지 하는 hello 컨테이너 내에서 실행).</span><span class="sxs-lookup"><span data-stu-id="4f9a9-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="4f9a9-165">"1"이라는 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-165">Specify an instance count of "1".</span></span>

![컨테이너용 Service Fabric Yeoman 생성기][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="4f9a9-167">포트 매핑 및 컨테이너 리포지토리 인증 구성</span><span class="sxs-lookup"><span data-stu-id="4f9a9-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="4f9a9-168">컨테이너화된 서비스에는 통신을 위한 끝점이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="4f9a9-169">이제 hello 프로토콜, 포트 및 형식 추가 tooan `Endpoint` hello ServiceManifest.xml 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="4f9a9-170">이 문서에 대 한 컨테이너 화 된 hello 서비스 4000 포트에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="4f9a9-171">Hello 제공 `UriScheme` 자동으로 검색 기능에 대 한 서비스 패브릭 명명 서비스 hello로 컨테이너 끝점 hello를 레지스터입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="4f9a9-172">전체 ServiceManifest.xml 예제 파일은이 문서의 hello 끝에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="4f9a9-173">Hello 컨테이너 포트와 호스트 간 포트 매핑을 지정 하 여 구성 된 `PortBinding` 에서 정책을 `ContainerHostPolicies` hello ApplicationManifest.xml 파일의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="4f9a9-174">이 문서에 대 한 `ContainerPort` 은 80 (hello 컨테이너에 지정 된 hello Dockerfile로 포트 80을 노출 하는 데 사용) 및 `EndpointRef` "myserviceTypeEndpoint" (hello 서비스 매니페스트에서 정의 된 hello 끝점)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="4f9a9-175">4000 포트에서 toohello 서비스는 들어오는 요청 tooport 80 hello 컨테이너에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="4f9a9-176">컨테이너와 개인 리포지토리에 tooauthenticate를 필요한 경우 다음 추가 `RepositoryCredentials`합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="4f9a9-177">이 문서에 대 한 hello 계정 이름 및 hello myregistry.azurecr.io 컨테이너 레지스트리에 대 한 암호를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="4f9a9-178">빌드 및 패키지 hello 서비스 패브릭 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="4f9a9-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="4f9a9-179">에 대 한 빌드 스크립트를 포함 하는 hello 서비스 패브릭 Yeoman 템플릿 [Gradle](https://gradle.org/), 어떤 터미널 hello에서 toobuild hello 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="4f9a9-180">toobuild 및 패키지 hello 응용 프로그램을 hello 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="4f9a9-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="4f9a9-181">Hello 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="4f9a9-181">Deploy hello application</span></span>
<span data-ttu-id="4f9a9-182">Hello 응용 프로그램으로 빌드하고 나면 toohello 로컬 클러스터 서비스 패브릭 CLI hello를 사용 하 여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="4f9a9-183">Toohello 로컬 서비스 패브릭 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="4f9a9-184">사용 하 여 hello 제공 hello 템플릿 toocopy에 hello 응용 프로그램 패키지 toohello 클러스터 이미지 저장소, hello 응용 프로그램 형식 등록 hello 응용 프로그램의 인스턴스를 만들 스크립트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="4f9a9-185">브라우저를 열고 http://localhost:19080/탐색기 (hello Vagrant를 사용 하 여 Mac OS X의 경우 VM의 개인 ip hello 바꾸기 localhost)에서 패브릭 탐색기 tooService 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="4f9a9-186">Hello 응용 프로그램 노드를 확장 하 고 응용 프로그램 종류에 대 한 항목 및 해당 형식의 첫 번째 인스턴스 hello에 대 한 다른 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="4f9a9-187">컨테이너를 실행 하는 toohello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-187">Connect toohello running container.</span></span>  <span data-ttu-id="4f9a9-188">예를 들어 "http://localhost:4000" 4000, 포트에서 반환 된 toohello IP 주소를 가리키는 웹 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="4f9a9-189">"Hello World!" 제목 hello를 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="4f9a9-190">hello 브라우저에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-190">display in hello browser.</span></span>

![Hello World!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="4f9a9-192">정리</span><span class="sxs-lookup"><span data-stu-id="4f9a9-192">Clean up</span></span>
<span data-ttu-id="4f9a9-193">Hello 제거 스크립트를 사용 하 여 hello 템플릿 toodelete hello 응용 프로그램 인스턴스 hello 로컬 개발 클러스터에서에 제공 된 및 hello 응용 프로그램 종류의 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="4f9a9-194">Hello 이미지 toohello 컨테이너 레지스트리 강제 한 후에 개발 컴퓨터에서 hello 로컬 이미지를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="4f9a9-195">Service Fabric 응용 프로그램 및 서비스 매니페스트의 전체 예제</span><span class="sxs-lookup"><span data-stu-id="4f9a9-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="4f9a9-196">Hello 완전 한 서비스 및 응용 프로그램 매니페스트가이 문서에 사용 되는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="4f9a9-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="4f9a9-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="4f9a9-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="4f9a9-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="4f9a9-199">더 많은 서비스 tooan 기존 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="4f9a9-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="4f9a9-200">다른 컨테이너 서비스 tooan 응용 프로그램 이미 yeoman를 사용 하 여 만든 수행 tooadd hello 다음 단계:</span><span class="sxs-lookup"><span data-stu-id="4f9a9-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="4f9a9-201">Hello 기존 응용 프로그램의 toohello 루트 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="4f9a9-202">예를 들어 `cd ~/YeomanSamples/MyApplication`경우 `MyApplication` 는 Yeoman에서 만든 hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="4f9a9-203">`yo azuresfcontainer:AddService` 실행</span><span class="sxs-lookup"><span data-stu-id="4f9a9-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="4f9a9-204">컨테이너를 강제로 종료하기 전 시간 간격 구성</span><span class="sxs-lookup"><span data-stu-id="4f9a9-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="4f9a9-205">Hello 서비스 삭제 (또는 이동 tooanother 노드)이 시작 된 후 hello 컨테이너를 제거 하기 전에 hello 런타임 toowait에 대 한 시간 간격을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="4f9a9-206">구성 hello 시간 간격 보냅니다 hello `docker stop <time in seconds>` 명령 toohello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="4f9a9-207">자세한 내용은 [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="4f9a9-208">hello 시간 간격 toowait hello 아래에 지정 된 `Hosting` 섹션.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="4f9a9-209">클러스터 매니페스트 조각 다음 hello tooset hello 간격을 대기 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
<span data-ttu-id="4f9a9-210">hello 기본 시간 간격을 설정 too10 초입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="4f9a9-211">이 구성은 동적 이므로 config hello 클러스터 업데이트 hello 제한 시간에만 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="4f9a9-212">Hello 런타임 tooremove 구성 사용 하지 않는 컨테이너 이미지</span><span class="sxs-lookup"><span data-stu-id="4f9a9-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="4f9a9-213">서비스 패브릭 클러스터 tooremove hello를 구성할 수 있습니다 hello 노드에서 사용 하지 않는 컨테이너 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="4f9a9-214">이 구성은 너무 많은 컨테이너 이미지는 hello 노드에 지정할 경우 빼앗길 디스크 공간 toobe를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="4f9a9-215">tooenable이 기능을 업데이트 hello `Hosting` hello 다음 코드 조각에에서 나와 있는 것 처럼 hello 클러스터 매니페스트 섹션:</span><span class="sxs-lookup"><span data-stu-id="4f9a9-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

<span data-ttu-id="4f9a9-216">삭제 하지 않아야 하는 이미지에 대 한 리소스를 지정 하면 hello에서 `ContainerImagesToSkip` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="4f9a9-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f9a9-217">Next steps</span></span>
* <span data-ttu-id="4f9a9-218">[Service Fabric의 컨테이너](service-fabric-containers-overview.md)를 실행하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="4f9a9-219">읽기 hello [컨테이너에서.NET 응용 프로그램 배포](service-fabric-host-app-in-a-container.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="4f9a9-220">서비스 패브릭 hello에 대 한 자세한 내용은 [응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="4f9a9-221">체크 아웃 hello [서비스 패브릭 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers) GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f9a9-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
