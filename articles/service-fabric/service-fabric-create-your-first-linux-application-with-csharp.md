---
title: "aaaCreate C#을 사용 하 여 Linux에서 첫 번째 Azure microservices 앱 | Microsoft Docs"
description: "C#을 사용하여 Service Fabric 응용 프로그램 만들기 및 배포"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="f75fc-103">첫 번째 Azure Service Fabric 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f75fc-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f75fc-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="f75fc-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="f75fc-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="f75fc-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="f75fc-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="f75fc-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="f75fc-107">Service Fabric은 .NET Core 및 Java 모두에서 Linux에 대한 서비스를 구축하는 SDK를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="f75fc-108">이 자습서에서는 방법을 살펴볼 toocreate Linux와 빌드 C# (.NET Core)를 사용 하 여 서비스에 대 한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f75fc-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f75fc-109">Prerequisites</span></span>
<span data-ttu-id="f75fc-110">시작하기 전에 [Linux 개발 환경을 설정](service-fabric-get-started-linux.md)하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="f75fc-111">Mac OS X을 사용하는 경우 [Vagrant를 사용하여 가상 컴퓨터에서 Linux one-box 환경을 설정](service-fabric-get-started-mac.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="f75fc-112">Tooinstall hello 내용도 [서비스 패브릭 CLI](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f75fc-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="f75fc-113">설치 및 hello 생성기 CSharp에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="f75fc-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="f75fc-114">Service Fabric은 Yeoman 템플릿 생성기를 사용하여 터미널에서 Service Fabric CSharp 응용 프로그램을 만들 수 있는 스캐폴딩 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="f75fc-115">CSharp 컴퓨터에서 작업에 대 한 hello 서비스 패브릭 yeoman 템플릿 생성기가 tooensure 아래 hello 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="f75fc-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="f75fc-116">컴퓨터에서 Node.js 및 NPM 설치</span><span class="sxs-lookup"><span data-stu-id="f75fc-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="f75fc-117">NPM의 컴퓨터에 [Yeoman](http://yeoman.io/) 템플릿 생성기 설치</span><span class="sxs-lookup"><span data-stu-id="f75fc-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="f75fc-118">서비스 패브릭 Yeo Java 응용 프로그램 생성기 hello NPM에서 설치</span><span class="sxs-lookup"><span data-stu-id="f75fc-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="f75fc-119">Hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f75fc-119">Create hello application</span></span>
<span data-ttu-id="f75fc-120">서비스 패브릭 응용 프로그램에는 각각 hello 응용 프로그램의 기능을 제공 하 여 특정 역할에 있는 하나 이상의 서비스 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="f75fc-121">서비스 패브릭 hello [Yeoman](http://yeoman.io/) CSharp 마지막 단계에서 설치에 대 한 생성기 쉽게 toocreate를 사용 하면 첫 번째 서비스 및 tooadd 나중에 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="f75fc-122">단일 서비스 Yeoman toocreate 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="f75fc-123">종료, hello hello 스 캐 폴딩 빌드 명령 toostart 다음을 입력 합니다.`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="f75fc-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="f75fc-124">응용 프로그램의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-124">Name your application.</span></span>
3. <span data-ttu-id="f75fc-125">Hello 유형의 첫 번째 서비스를 선택 하 고 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="f75fc-126">이 자습서의 hello 위해 신뢰할 수 있는 행위자 서비스를 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![C#용 Service Fabric Yeoman 생성기][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="f75fc-128">Hello 옵션에 대 한 자세한 내용은 참조 [프로그래밍 모델 개요 서비스 패브릭](service-fabric-choose-framework.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="f75fc-129">Hello 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="f75fc-129">Build hello application</span></span>
<span data-ttu-id="f75fc-130">hello 서비스 패브릭 Yeoman 템플릿에 (toohello 응용 프로그램 폴더를 탐색 하는) 한 후 터미널 hello toobuild hello 응용 프로그램을 사용할 수 있는 빌드 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="f75fc-131">Hello 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="f75fc-131">Deploy hello application</span></span>

<span data-ttu-id="f75fc-132">Hello 응용 프로그램으로 빌드하고 나면 toohello 쿼럼 응답을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="f75fc-133">Toohello 로컬 서비스 패브릭 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="f75fc-134">Hello 템플릿 toocopy에 제공 된 실행된 hello 설치 스크립트 응용 프로그램 패키지 toohello 클러스터 이미지 저장소 hello, hello 응용 프로그램 형식 등록 및 hello 응용 프로그램의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="f75fc-135">배포 hello 작성 된 응용 프로그램이 다른 서비스 패브릭 응용 프로그램으로 동일한 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="f75fc-136">Hello 설명서를 참조 하십시오 [서비스 패브릭 CLI hello로 서비스 패브릭 응용 프로그램 관리](service-fabric-application-lifecycle-sfctl.md) 자세한 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="f75fc-137">매개 변수 toothese 명령은 생성 하는 hello 매니페스트 hello 응용 프로그램 패키지 내에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="f75fc-138">Hello 응용 프로그램을 배포한 후 브라우저를 열고 탐색 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 에서 [http://localhost:19080/탐색기](http://localhost:19080/Explorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="f75fc-139">그런 다음 확대 하는 hello **응용 프로그램** 노드 및 응용 프로그램 종류에 대 한 항목 및 해당 형식의 첫 번째 인스턴스 hello에 대 한 다른 이제는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="f75fc-140">Hello 테스트 클라이언트를 시작 하 고 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="f75fc-141">행위자 프로젝트 자체에서는 아무 것도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="f75fc-142">다른 서비스 또는 클라이언트 toosend 필요로 할 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="f75fc-143">hello 행위자 템플릿은 toointeract hello 행위자 서비스와 함께 사용할 수 있는 간단한 테스트 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="f75fc-144">Hello 조사식 유틸리티 toosee hello 출력 hello 행위자 서비스를 사용 하 여 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="f75fc-145">서비스 패브릭 탐색기에서 hello hello 행위자 서비스에 대 한 주 복제본을 호스팅하는 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="f75fc-146">아래 hello 스크린샷에서에서 노드 3입니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-146">In hello screenshot below, it is node 3.</span></span>

    ![서비스 패브릭 탐색기에서 주 복제본 hello 찾기][sfx-primary]
3. <span data-ttu-id="f75fc-148">Hello 이전 단계에서 찾은 다음 선택 hello 노드를 클릭 **비활성화 (다시 시작)** hello 작업 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="f75fc-149">이 작업에 다른 노드에서 실행 중인 장애 조치 tooa 보조 복제본을 강제 적용 하 여 로컬 클러스터의 한 노드에서 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="f75fc-150">이 작업을 수행 하면 hello 테스트 클라이언트가 고 해당 hello 카운터 tooincrement hello 장애 조치 되더라도 계속 참고에서 주의 기울여야 toohello 출력을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="f75fc-151">더 많은 서비스 tooan 기존 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="f75fc-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="f75fc-152">tooadd 서비스 tooan 이미 다른 응용 프로그램 사용 하 여 만든 `yo`, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="f75fc-153">Hello 기존 응용 프로그램의 toohello 루트 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="f75fc-154">예를 들어 `cd ~/YeomanSamples/MyApplication`경우 `MyApplication` 는 Yeoman에서 만든 hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="f75fc-155">`yo azuresfcsharp:AddService` 실행</span><span class="sxs-lookup"><span data-stu-id="f75fc-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="f75fc-156">Project.json too.csproj에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="f75fc-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="f75fc-157">프로젝트 루트 디렉터리에서 ' 마이그레이션할 dotnet' 실행 되는 모든 hello project.json toocsproj 형식을 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="f75fc-158">업데이트 hello 프로젝트 참조 프로젝트 파일의 파일 toocsproj 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="f75fc-159">Build.sh의 hello 프로젝트 파일 이름을 toocsproj 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75fc-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f75fc-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f75fc-160">Next steps</span></span>

* [<span data-ttu-id="f75fc-161">Reliable Actors에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="f75fc-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="f75fc-162">서비스 패브릭 CLI hello를 사용 하 여 서비스 패브릭 클러스터와의 상호 작용</span><span class="sxs-lookup"><span data-stu-id="f75fc-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="f75fc-163">[Service Fabric 지원 옵션](service-fabric-support.md) 알아보기</span><span class="sxs-lookup"><span data-stu-id="f75fc-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="f75fc-164">Service Fabric CLI 시작</span><span class="sxs-lookup"><span data-stu-id="f75fc-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
