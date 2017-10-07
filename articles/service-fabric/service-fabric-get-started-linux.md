---
title: "linux 개발 환경을 aaaSet | Microsoft Docs"
description: "Hello 런타임 및 SDK를 설치 하 고 Linux에서 로컬 개발 클러스터를 만듭니다. 이 설치를 완료 한 후 응용 프로그램 준비 toobuild 됩니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="2d72d-104">Linux에서 개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="2d72d-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d72d-105">Windows</span><span class="sxs-lookup"><span data-stu-id="2d72d-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="2d72d-106">Linux</span><span class="sxs-lookup"><span data-stu-id="2d72d-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="2d72d-107">OSX</span><span class="sxs-lookup"><span data-stu-id="2d72d-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="2d72d-108">toodeploy 실행 [Azure 서비스 패브릭 응용 프로그램](service-fabric-application-model.md) Linux 개발 컴퓨터에 hello 런타임 및 일반 SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="2d72d-109">또한 Java 및 .NET Core용 선택적 SDK를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d72d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2d72d-110">Prerequisites</span></span>

<span data-ttu-id="2d72d-111">운영 체제 버전에 따라 hello 개발을 위해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="2d72d-112">Ubuntu 16.04(`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="2d72d-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="2d72d-113">APT 원본 업데이트</span><span class="sxs-lookup"><span data-stu-id="2d72d-113">Update your APT sources</span></span>
<span data-ttu-id="2d72d-114">tooinstall hello SDK 및 hello 관련 된 런타임 패키지 hello apt get 명령줄 도구를 통해 먼저 고급 패키징 도구 (APT) 소스 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="2d72d-115">터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-115">Open a terminal.</span></span>
2. <span data-ttu-id="2d72d-116">Hello 서비스 패브릭 리포지토리 tooyour 원본 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="2d72d-117">Hello 추가 `dotnet` 리포지토리 tooyour 원본 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="2d72d-118">Hello 추가 새 Gnu 개인 정보 보호 (GnuPG, 또는 GPG) tooyour APT keyring 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="2d72d-119">Hello 공식 Docker GPG 키 tooyour APT keyring을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="2d72d-120">Hello Docker 리포지토리를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="2d72d-121">패키지 새로 고침 목록을 새로 hello에 따라 저장소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="2d72d-122">설치 및 로컬 클러스터 설치에 대 한 SDK hello 설정</span><span class="sxs-lookup"><span data-stu-id="2d72d-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="2d72d-123">소스를 업데이트 한 후에 hello SDK를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="2d72d-124">Hello 서비스 패브릭 SDK 패키지를 설치 하 고 hello 설치 확인 toohello 사용권 계약에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="2d72d-125">hello 다음 명령을 자동화 서비스 패브릭 패키지에 대 한 hello 라이선스를 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="2d72d-126">로컬 클러스터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-126">Set up a local cluster</span></span>
  <span data-ttu-id="2d72d-127">Hello 설치에 성공한 경우에 로컬 클러스터 수 toostart 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="2d72d-128">Hello 클러스터 설치 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="2d72d-129">웹 브라우저를 열고 너무 이동[서비스 패브릭 탐색기](http://localhost:19080/Explorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="2d72d-130">Hello 클러스터가 시작 했습니다 hello 서비스 패브릭 탐색기 대시보드를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Linux의 Service Fabric Explorer][sfx-linux]

  <span data-ttu-id="2d72d-132">이 시점에서 게스트 컨테이너 또는 게스트 실행 파일에 따라 미리 빌드된 Service Fabric 응용 프로그램 패키지 또는 새 응용 프로그램 패키지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="2d72d-133">toobuild hello Java 또는.NET Core Sdk를 사용 하 여 새로운 서비스 전반에 제공 되는 hello 선택적인 설정 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="2d72d-134">독립 실행형 클러스터는 Linux에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="2d72d-135">hello 미리 보기 지원 한 상자만 하 고 Azure Linux 다중 컴퓨터 클러스터.</span><span class="sxs-lookup"><span data-stu-id="2d72d-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="2d72d-136">서비스 패브릭 CLI hello 설정</span><span class="sxs-lookup"><span data-stu-id="2d72d-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="2d72d-137">hello [서비스 패브릭 CLI](service-fabric-cli.md) 에 엔터티 서비스 패브릭 클러스터와 응용 프로그램을 포함 하 여 상호 작용 하기 위한 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="2d72d-138">Python에 기반 하는, 있는지 toohave python 및 pip 다음 명령을 hello를 계속 진행 하기 전에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="2d72d-139">설치 및 hello 생성기 컨테이너 및 게스트 실행 파일에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="2d72d-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="2d72d-140">Service Fabric은 Yeoman 템플릿 생성기를 사용하여 터미널에서 Service Fabric 응용 프로그램을 만들 수 있는 스캐폴딩 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="2d72d-141">컴퓨터에서 작업 하기 위한 hello 서비스 패브릭 yeoman 템플릿 생성기 있는 tooensure 아래 hello 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="2d72d-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="2d72d-142">컴퓨터에서 Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="2d72d-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="2d72d-143">NPM의 컴퓨터에 [Yeoman](http://yeoman.io/) 템플릿 생성기 설치</span><span class="sxs-lookup"><span data-stu-id="2d72d-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="2d72d-144">서비스 패브릭 Yeo 컨테이너 생성기 hello 및 게스트 execuatble 생성기 NPM에서 설치</span><span class="sxs-lookup"><span data-stu-id="2d72d-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="2d72d-145">생성기 위에 hello를 설치한 후 게스트 실행 파일 또는 컨테이너 서비스를 사용 하 여 수 toocreate 앱을 실행 하 여 있어야 `yo azuresfguest` 또는 `yo azuresfcontainer` 각각.</span><span class="sxs-lookup"><span data-stu-id="2d72d-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="2d72d-146">Hello 필요한 Java 아티팩트 (선택 사항, toouse hello Java 프로그래밍 모델)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="2d72d-147">Java를 사용 하 여 toobuild 서비스 패브릭 서비스 Gradle 빌드 작업을 실행 하는 데 사용 되는 함께 설치 된 JDK 1.8 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="2d72d-148">다음 코드 조각 hello Open JDK 1.8 Gradle 함께 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="2d72d-149">서비스 패브릭 Java 라이브러리 hello Maven에서 끌어 오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="2d72d-150">Hello Eclipse Neon 플러그 인 설치 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="2d72d-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="2d72d-151">Hello 내에서 서비스 패브릭 용 hello Eclipse 플러그 인을 설치할 수 있습니다 **Java 개발자를 위한 Eclipse IDE**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="2d72d-152">또한 tooService 패브릭 Java 응용 프로그램에서 Eclipse toocreate 서비스 패브릭 게스트 실행 가능한 응용 프로그램 및 컨테이너 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="2d72d-153">Eclipse에서 최신 Eclipse Neon 있고 최신 Buildship 버전 hello 확인 (1.0.17 이상) 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="2d72d-154">선택 하 여 hello 버전의 설치 된 구성 요소를 확인할 수 있습니다 **도움말** > **설치 세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="2d72d-155">Buildship hello 지침을 사용 하 여 업데이트할 수 있습니다 [Eclipse Buildship: Eclipse 플러그 인에 대 한 Gradle][buildship-update]합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="2d72d-156">tooinstall hello 서비스 패브릭 플러그 인 선택 **도움말** > **새 소프트웨어 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="2d72d-157">Hello에 **작업할** 상자에서 입력 **http://dl.microsoft.com/eclipse**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="2d72d-158">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-158">Click **Add**.</span></span>

    ![hello 사용 가능한 소프트웨어 페이지][sf-eclipse-plugin]

5. <span data-ttu-id="2d72d-160">선택 hello **ServiceFabric** 플러그 인을 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="2d72d-161">Hello 설치 단계를 완료 하 고 hello 최종 사용자 사용권 계약에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="2d72d-162">서비스 패브릭 Eclipse 플러그 인 설치 hello 이미 있는 경우 hello 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="2d72d-163">선택 하 여 확인할 수 있습니다 **도움말** > **설치 세부 정보** 서비스 패브릭의 hello 목록에 다음 검색 플러그 인을 설치 합니다. 최신 버전을 사용할 수 있는 경우 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="2d72d-164">자세한 내용은 [Eclipse Java 응용 프로그램 배포를 위한 Azure Service Fabric 플러그 인](service-fabric-get-started-eclipse.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d72d-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="2d72d-165">Hello.NET Core SDK (선택 사항, 프로그래밍 모델을.NET Core toouse hello)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="2d72d-166">.NET Core SDK hello hello 라이브러리 및.NET Core를 사용 하 여 필요한 toobuild 서비스 패브릭 서비스 되는 템플릿을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="2d72d-167">실행 중인 hello 다음과-hello.NET Core SDK 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="2d72d-168">업데이트 hello SDK 및 런타임</span><span class="sxs-lookup"><span data-stu-id="2d72d-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="2d72d-169">tooupdate toohello 최신 버전의 SDK hello 및 런타임, hello 다음 명령을 실행 (의도 하지 않은 hello Sdk를 선택 취소):</span><span class="sxs-lookup"><span data-stu-id="2d72d-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="2d72d-170">Maven에서 tooupdate hello Java SDK 바이너리, 해야 hello에 해당 이진 hello tooupdate hello 버전 정보 ``build.gradle`` 파일 toopoint toohello 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="2d72d-171">정확히 필요한 tooupdate hello 버전 tooknow tooany 참조할 수 있습니다 ``build.gradle`` 파일 샘플을 시작 하는 서비스 패브릭에서 [여기](https://github.com/Azure-Samples/service-fabric-java-getting-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="2d72d-172">Hello 패키지 업데이트를 실행 하 여 로컬 개발 클러스터 toostop을 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="2d72d-173">이 페이지에 대 한 hello 지침에 따라 로컬 클러스터 업그레이드 한 후 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d72d-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d72d-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d72d-174">Next steps</span></span>

* [<span data-ttu-id="2d72d-175">Yeoman을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="2d72d-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="2d72d-176">Eclipse용 Service Fabric 플러그 인을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="2d72d-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="2d72d-177">Linux에서 첫 번째 CSharp 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="2d72d-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="2d72d-178">OSX에서 개발 환경 준비</span><span class="sxs-lookup"><span data-stu-id="2d72d-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="2d72d-179">서비스 패브릭 CLI toomanage hello 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="2d72d-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="2d72d-180">Service Fabric Windows/Linux 간 차이점</span><span class="sxs-lookup"><span data-stu-id="2d72d-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="2d72d-181">Service Fabric CLI 시작</span><span class="sxs-lookup"><span data-stu-id="2d72d-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
