---
title: "Mac OS X toowork Azure 서비스 패브릭에서 개발 환경을 aaaSet | Microsoft Docs"
description: "Hello 런타임, SDK 및 도구를 설치 하 고 로컬 개발 클러스터를 만듭니다. 이 설치를 완료 한 후 Mac OS X에서 응용 프로그램 준비 toobuild 됩니다."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="efc7e-104">Mac OS X에서 개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="efc7e-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="efc7e-105">Windows</span><span class="sxs-lookup"><span data-stu-id="efc7e-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="efc7e-106">Linux</span><span class="sxs-lookup"><span data-stu-id="efc7e-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="efc7e-107">OSX</span><span class="sxs-lookup"><span data-stu-id="efc7e-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="efc7e-108">Mac OS X를 사용 하 여 Linux 클러스터에서 서비스 패브릭 응용 프로그램 toorun를 작성할 수 있습니다. 이 문서에서는 어떻게 tooset 개발을 위한 Mac 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efc7e-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="efc7e-109">Prerequisites</span></span>
<span data-ttu-id="efc7e-110">서비스 패브릭에서 실행 되지 않을 기본적으로 OS X toorun 로컬 서비스 패브릭 클러스터, Vagrant 및 VirtualBox 사용 하 여 미리 구성 된 Ubuntu 가상 컴퓨터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="efc7e-111">시작하기 전에 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="efc7e-112">Vagrant(v1.8.4 이상)</span><span class="sxs-lookup"><span data-stu-id="efc7e-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="efc7e-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="efc7e-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="efc7e-114">Toouse 상호 지원 및 버전을 Vagrant VirtualBox 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="efc7e-115">지원되지 않는 VirtualBox 버전에서는 Vagrant가 비정상적으로 동작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="efc7e-116">만들 로컬 VM hello</span><span class="sxs-lookup"><span data-stu-id="efc7e-116">Create hello local VM</span></span>
<span data-ttu-id="efc7e-117">toocreate 5 노드 서비스 패브릭 클러스터를 포함 하는 로컬 VM hello에 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="efc7e-118">복제 hello `Vagrantfile` 리포지토리</span><span class="sxs-lookup"><span data-stu-id="efc7e-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="efc7e-119">이 단계 bring 다운 hello 파일 `Vagrantfile` hello VM 포함 된 hello 위치 hello VM과 함께 구성에서 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="efc7e-120">Hello 리포지토리의 로컬 복제본 toohello 이동</span><span class="sxs-lookup"><span data-stu-id="efc7e-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="efc7e-121">(선택 사항) Hello 기본 VM 설정을 수정합니다</span><span class="sxs-lookup"><span data-stu-id="efc7e-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="efc7e-122">기본적으로 hello 로컬 VM에서 다음과 같이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="efc7e-123">3GB의 메모리 할당</span><span class="sxs-lookup"><span data-stu-id="efc7e-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="efc7e-124">개인 호스트 네트워크에서 IP 192.168.50.50 구성 hello Mac 호스트에서 트래픽의 통과 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="efc7e-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="efc7e-125">이러한 설정 중 하나를 변경 하거나 hello에 다른 구성 toohello VM을 추가할 수 있습니다 `Vagrantfile`합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="efc7e-126">Hello 참조 [Vagrant 설명서](http://www.vagrantup.com/docs) hello 구성 옵션의 전체 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="efc7e-127">Hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="efc7e-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="efc7e-128">이 단계는 hello 미리 구성 된 VM 이미지를 로컬로 제거한 다음 설정을 로컬 서비스 패브릭 클러스터 것에 부팅을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="efc7e-129">하시면 것 tootake 몇 분 정도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="efc7e-130">설치가 성공적으로 완료 된 경우 해당 hello 클러스터를 시작 하는 나타내는 hello 출력에 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![다음 VM 프로비전을 시작하는 클러스터 설치][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="efc7e-132">Hello VM 다운로드에 시간이 오래 걸리면, wget 또는 curl을 사용 하 여 다운로드할 수 있습니다 또는 변수에 지정 된 toohello 링크를 이동 하 여 브라우저를 통해 **config.vm.box_url** hello 파일에 `Vagrantfile`합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="efc7e-133">로컬에서 다운로드 한 후 편집 `Vagrantfile` hello 이미지 다운로드 한 toopoint toohello 로컬 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="efc7e-134">예제 hello 이미지 too/home/users/test/azureservicefabric.tp8.box 다운로드 한 경우 다음 설정에 대 한 **config.vm.box_url** toothat 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="efc7e-135">해당 hello 테스트 클러스터에 올바르게 설정 되었는지 http://192.168.50.50:19080/탐색기 (hello 기본 개인 네트워크 IP 유지 한다고 가정)에서 패브릭 탐색기 tooService 이동 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Hello 호스트 Mac에서에서 본 서비스 패브릭 탐색기][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="efc7e-137">Yeoman을 사용하여 Mac에서 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="efc7e-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="efc7e-138">Service Fabric은 Yeoman 템플릿 생성기를 사용하여 터미널에서 Service Fabric 응용 프로그램을 만들 수 있는 스캐폴딩 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="efc7e-139">컴퓨터에서 작업 하는 hello 서비스 패브릭 yeoman 템플릿 생성기 있는 tooensure 아래 hello 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="efc7e-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="efc7e-140">Toohave Node.js 및 NPM 있습니다 mac에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="efc7e-141">그렇지 않으면 Node.js 및 NPM hello 다음을 사용 하 여 Homebrew를 사용 하 여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="efc7e-142">toocheck hello 버전의 Node.js 및 NPM Mac에 설치에서는 hello를 사용할 수 있습니다 ``-v`` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="efc7e-143">NPM의 컴퓨터에 [Yeoman](http://yeoman.io/) 템플릿 생성기 설치</span><span class="sxs-lookup"><span data-stu-id="efc7e-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="efc7e-144">Hello Yeoman 설치 생성기 원하는 toouse를 시작 하는 hello에 hello 단계에 따라 [설명서](service-fabric-get-started-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="efc7e-145">toocreate 서비스 패브릭 응용 프로그램 Yeoman를 사용 하 여 다음과 같이 hello-</span><span class="sxs-lookup"><span data-stu-id="efc7e-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="efc7e-146">Mac에서 서비스 패브릭 Java 응용 프로그램 toobuild 해야-JDK 1.8 및 Gradle hello 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="efc7e-147">Eclipse Neon에 대 한 hello 서비스 패브릭 플러그 인을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="efc7e-148">서비스 패브릭 hello에 대 한 플러그 인을 제공 **Java IDE에 대 한 Eclipse Neon** 작성, 빌드 및 Java 서비스 배포의 hello 프로세스를 단순화할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="efc7e-149">이 일반에 언급 된 hello 설치 단계를 따르면 [설명서](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) 설치 또는 서비스 패브릭 Eclipse 플러그 인을 업데이트 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="efc7e-150">기본적으로 지원 hello 기본 IP hello에 설명 된 대로 ``Vagrantfile`` hello에 ``Local.json`` hello 생성 된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="efc7e-151">변경 하 고 다른 IP와 Vagrant 배포 hello에 해당 IP를 업데이트 하십시오 ``Local.json`` 도 응용 프로그램의 합니다.</span><span class="sxs-lookup"><span data-stu-id="efc7e-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efc7e-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="efc7e-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="efc7e-153">Yeoman을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="efc7e-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="efc7e-154">Eclipse용 Service Fabric 플러그 인을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="efc7e-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="efc7e-155">Hello Azure 포털에서에서 서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="efc7e-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="efc7e-156">Azure 리소스 관리자 hello를 사용 하 여 서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="efc7e-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="efc7e-157">Hello 서비스 패브릭 응용 프로그램 모델 이해</span><span class="sxs-lookup"><span data-stu-id="efc7e-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
