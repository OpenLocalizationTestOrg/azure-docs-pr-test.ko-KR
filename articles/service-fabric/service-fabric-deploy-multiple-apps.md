---
title: "MongoDB를 사용 하는 Node.js 응용 aaaDeploy | Microsoft Docs"
description: "방법에 대 한 연습 toopackage toodeploy tooan Azure 서비스 패브릭 클러스터에 대 한 여러의 게스트 실행 파일"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="24691-103">여러 개의 게스트 실행 파일 배포</span><span class="sxs-lookup"><span data-stu-id="24691-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="24691-104">이 문서에서는 어떻게 toopackage 및 여러 게스트 실행 파일 tooAzure 서비스 패브릭을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="24691-105">만들고 단일 서비스 패브릭 패키지를 배포 하는 방법을 너무 읽을[게스트 실행 tooService 패브릭 배포](service-fabric-deploy-existing-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="24691-106">이 연습에서는 toodeploy MongoDB hello 데이터 저장소로 사용 하는 Node.js 프런트 엔드 응용 프로그램을 적용 하는 방법을 다른 응용 프로그램에 의존 하는 hello 단계 tooany 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24691-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="24691-107">여러 개의 게스트 실행 파일이 포함 된 Visual Studio tooproduce hello 응용 프로그램 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="24691-108">참조 [Visual Studio를 사용 하 여 기존 응용 프로그램 toopackage](service-fabric-deploy-existing-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="24691-109">첫 번째 hello 게스트 실행 파일을 추가 하면 마우스 오른쪽 단추로 클릭 hello 응용 프로그램 프로젝트와 선택 hello **추가-새 서비스 패브릭 서비스 >** tooadd hello 두 번째 게스트 실행 파일 프로젝트 toohello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="24691-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="24691-110">참고: hello hello Visual Studio 솔루션을 구축 하는 Visual Studio 프로젝트에서에서 toolink hello 소스 됩니다 되도록 선택 하면 응용 프로그램 패키지는 toodate hello 소스에 변경한 내용으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="24691-111">샘플</span><span class="sxs-lookup"><span data-stu-id="24691-111">Samples</span></span>
* [<span data-ttu-id="24691-112">게스트 실행 파일을 패키징 및 배포하는 샘플</span><span class="sxs-lookup"><span data-stu-id="24691-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="24691-113">REST를 사용 하 여 hello 명명 서비스를 통해 두 개의 게스트 실행 파일 (C# 및 nodejs) 통신의 샘플</span><span class="sxs-lookup"><span data-stu-id="24691-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="24691-114">수동으로 패키지 hello 여러 게스트 실행 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="24691-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="24691-115">또는 hello 게스트 실행 파일을 수동으로 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="24691-116">Hello 수동 패키지에 대 한이 문서에서는 hello 서비스 패브릭 패키징 도구에서 제공 되는 [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool)합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="24691-117">패키징 hello Node.js 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="24691-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="24691-118">이 문서에서는 Node.js hello 서비스 패브릭 클러스터의 hello 노드에 설치 되어 있지 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="24691-119">이 인해 tooadd Node.exe toohello 루트 디렉터리 패키징하기 전에 노드 응용 프로그램의 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="24691-120">(Express 웹 프레임 워크 및 Jade 템플릿 엔진 사용) hello Node.js 응용 프로그램의 디렉터리 구조 hello 아래와 유사한 toohello 하나 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24691-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="24691-121">다음 단계로 hello Node.js 응용 프로그램에 대 한 응용 프로그램 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24691-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="24691-122">아래 hello 코드는 hello Node.js 응용 프로그램을 포함 하는 서비스 패브릭 응용 프로그램 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24691-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="24691-123">다음은 사용 중인 hello 매개 변수 설명이입니다.</span><span class="sxs-lookup"><span data-stu-id="24691-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="24691-124">**/source** 패키지 해야 하는 hello 응용 프로그램의 포인트 toohello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="24691-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="24691-125">**/target** 패키지를 만들는 hello hello 디렉터리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="24691-126">이 디렉터리에 toobe hello 소스 디렉터리와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="24691-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="24691-127">**/appname** hello 기존 응용 프로그램의 hello 응용 프로그램 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="24691-128">것이 중요 한 toounderstand hello 매니페스트에서 toohello 서비스 이름 및 서비스 패브릭 응용 프로그램 이름이 아닌 toohello 변환이 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="24691-129">**/exe** 서비스 패브릭 toolaunch,이 경우 있어야 하 고 실행 하는 hello 정의 `node.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="24691-130">**/ma** 사용된 toolaunch hello 실행 되는 hello 인수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="24691-131">Node.js 설치 되지 않은 서비스 패브릭 요구 toolaunch hello Node.js 웹 서버를 실행 하 여 `node.exe bin/www`합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="24691-132">`/ma:'bin/www'`hello 패키징 도구 toouse 지시 `bin/ma` node.exe hello 인수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="24691-133">**/ AppType** hello 서비스 패브릭 응용 프로그램 유형 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="24691-134">Hello /target 매개 변수에서 지정 된 toohello 디렉터리를 이동 하는 경우 아래와 같이 해당 hello 도구에서 완벽 하 게 작동 서비스 패브릭 패키지를 만들었습니다 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="24691-135">생성 된 ServiceManifest.xml은 이제 아래 hello 코드 조각에 나와 있는 것 처럼 방법을 hello Node.js 웹 서버를 시작 해야를 설명 하는 섹션에는 hello:</span><span class="sxs-lookup"><span data-stu-id="24691-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="24691-136">이 샘플에서는 hello Node.js 웹 서버는 수신 tooport 3000, 아래와 같이 hello ServiceManifest.xml 파일에 tooupdate hello 끝점 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="24691-137">패키징 hello MongoDB 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="24691-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="24691-138">Hello Node.js 응용 프로그램을 압축 한 했으므로 계속 진행 하 고 MongoDB 패키지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="24691-139">앞서 언급 했 듯이 하는 대로 특정 tooNode.js 및 MongoDB 이제 통과 하는 hello 단계 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="24691-140">실제로 하나의 서비스 패브릭 응용 프로그램과 함께 패키지 toobe tooall 응용 프로그램 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24691-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="24691-141">MongoDB toopackage 원하는 toomake 패키지 Mongod.exe 및 Mongo.exe 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="24691-142">두 이진 hello에 살고 있는 `bin` MongoDB 설치 디렉터리의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="24691-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="24691-143">hello 디렉터리 구조 아래 하나 비슷한 toohello와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="24691-144">서비스 패브릭 필요 하나 명령 비슷한 toohello와 MongoDB toostart 아래 있으므로 toouse hello 필요 `/ma` MongoDB 패키징할 때 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="24691-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="24691-145">hello 노드의 hello 로컬 디렉터리에 hello MongoDB 데이터 디렉터리를 설정 하는 경우 노드 실패의 경우 hello hello 데이터 보존 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="24691-146">지 속성 저장소를 사용 하거나 MongoDB 복제본 순서 tooprevent 데이터 손실의 집합을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="24691-147">PowerShell 또는 hello 명령 셸에서 매개 변수 뒤 hello로 hello 패키징 도구를 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="24691-148">해당 hello /target 매개 toohello 가리키는지 toomake 순서 tooadd MongoDB tooyour 서비스 패브릭 응용 프로그램 패키지에 필요한 hello Node.js 응용 프로그램과 함께 hello 응용 프로그램 매니페스트를 이미 포함 된 같은 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="24691-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="24691-149">또한 사용 하 고 있는지 toomake 해야 스토어로 이름이 같은 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="24691-150">보겠습니다 toohello 디렉터리 찾아보기 및 검사 hello 도구 소개를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="24691-151">볼 수 있듯이 hello 도구가 hello MongoDB 바이너리를 포함 하는 새 폴더, MongoDB, toohello 디렉터리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="24691-152">Hello를 열면 `ApplicationManifest.xml` 파일을 해당 hello 패키지 hello Node.js 응용 프로그램과 MongoDB 이제 포함을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="24691-153">hello 코드 아래 hello 응용 프로그램 매니페스트의 콘텐츠 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24691-153">hello code below shows hello content of hello application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a><span data-ttu-id="24691-154">Hello 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="24691-154">Publishing hello application</span></span>
<span data-ttu-id="24691-155">hello 마지막 단계는 아래의 hello PowerShell 스크립트를 사용 하 여 toopublish hello 응용 프로그램 toohello 로컬 서비스 패브릭 클러스터를입니다.</span><span class="sxs-lookup"><span data-stu-id="24691-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="24691-156">Hello 응용 프로그램에서 성공적으로 게시 된 toohello 로컬 클러스터를 hello Node.js 응용 프로그램의 hello Node.js 응용 프로그램-예를 들어 http://localhost:3000 hello 서비스 매니페스트에 입력 된 hello 포트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="24691-157">이 자습서에서는 tooeasily 하나의 서비스 패브릭 응용 프로그램으로 두 개의 기존 응용 프로그램을 패키지 하는 방법을 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="24691-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="24691-158">또한 배웠습니다 어떻게 toodeploy 것 tooService 패브릭 한다는 높은 가용성 및 상태 시스템 통합 같은 서비스 패브릭 기능에서 일부 hello 얻을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="24691-159">게스트 실행 파일 tooan 기존 응용 프로그램별 Yeoman를 사용 하 여 Linux에서 추가</span><span class="sxs-lookup"><span data-stu-id="24691-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="24691-160">tooadd 서비스 tooan 이미 다른 응용 프로그램 사용 하 여 만든 `yo`, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="24691-161">Hello 기존 응용 프로그램의 toohello 루트 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="24691-162">예를 들어 `cd ~/YeomanSamples/MyApplication`경우 `MyApplication` 는 Yeoman에서 만든 hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="24691-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="24691-163">실행 `yo azuresfguest:AddService` hello 필요한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="24691-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24691-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24691-164">Next steps</span></span>
* <span data-ttu-id="24691-165">[Service Fabric 및 컨테이너 개요](service-fabric-containers-overview.md)에서 컨테이너 배포 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="24691-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="24691-166">게스트 실행 파일을 패키징 및 배포하는 샘플</span><span class="sxs-lookup"><span data-stu-id="24691-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="24691-167">REST를 사용 하 여 hello 명명 서비스를 통해 두 개의 게스트 실행 파일 (C# 및 nodejs) 통신의 샘플</span><span class="sxs-lookup"><span data-stu-id="24691-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
