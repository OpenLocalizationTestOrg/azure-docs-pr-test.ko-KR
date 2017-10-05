---
title: "MongoDB를 사용하여 Node.js 응용 프로그램 배포 | Microsoft Docs"
description: "여러 게스트 실행 파일을 패키지하여 Azure 서비스 패브릭 클러스터에 배포하는 방법에 대한 연습"
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
ms.openlocfilehash: b71723034e5f663986c49481072bfd6779d3d57b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="0658e-103">여러 개의 게스트 실행 파일 배포</span><span class="sxs-lookup"><span data-stu-id="0658e-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="0658e-104">이 문서에서는 여러 게스트 실행 파일을 패키징하고 Azure Service Fabric에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-104">This article shows how to package and deploy multiple guest executables to Azure Service Fabric.</span></span> <span data-ttu-id="0658e-105">단일 Service Fabric 패키지를 빌드 및 배포하는 방법은 [Service Fabric에 게스트 실행 파일 배포](service-fabric-deploy-existing-app.md) 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0658e-105">For building and deploying a single Service Fabric package read how to [deploy a guest executable to Service Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="0658e-106">이 연습에서는 MongoDB를 데이터 저장소로 사용하는 Node.js 프런트 엔드를 통해 응용 프로그램을 배포하는 방법을 보여 줍니다. 이 단계는 다른 응용 프로그램에 종속된 모든 응용 프로그램에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-106">While this walkthrough shows how to deploy an application with a Node.js front end that uses MongoDB as the data store, you can apply the steps to any application that has dependencies on another application.</span></span>   

<span data-ttu-id="0658e-107">Visual Studio를 사용하여 여러 게스트 실행 파일이 포함된 응용 프로그램 패키지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-107">You can use Visual Studio to produce the application package that contains multiple guest executables.</span></span> <span data-ttu-id="0658e-108">[Visual Studio를 사용하여 기존 응용 프로그램 패키징](service-fabric-deploy-existing-app.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0658e-108">See [Using Visual Studio to package an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="0658e-109">첫 번째 게스트 실행 파일을 추가한 후 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가->새 Service Fabric 서비스**를 선택하여 솔루션에 두 번째 게스트 실행 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-109">After you have added the first guest executable, right click on the application project and select the **Add->New Service Fabric service** to add the second guest executable project to the solution.</span></span> <span data-ttu-id="0658e-110">참고: Visual Studio 솔루션을 구축하는 Visual Studio 프로젝트에서 원본을 연결하려는 경우 응용 프로그램 패키지는 원본의 변경 내용으로 최신 상태로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-110">Note: If you choose to link the source in the Visual Studio project, building the Visual Studio solution, will make sure that your application package is up to date with changes in the source.</span></span> 

## <a name="samples"></a><span data-ttu-id="0658e-111">샘플</span><span class="sxs-lookup"><span data-stu-id="0658e-111">Samples</span></span>
* [<span data-ttu-id="0658e-112">게스트 실행 파일을 패키징 및 배포하는 샘플</span><span class="sxs-lookup"><span data-stu-id="0658e-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="0658e-113">REST를 사용하여 이름 지정 서비스를 통해 통신하는 두 게스트 실행 파일(C# 및 nodejs)의 샘플</span><span class="sxs-lookup"><span data-stu-id="0658e-113">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-the-multiple-guest-executable-application"></a><span data-ttu-id="0658e-114">수동으로 여러 게스트 실행 응용 프로그램 패키징</span><span class="sxs-lookup"><span data-stu-id="0658e-114">Manually package the multiple guest executable application</span></span>
<span data-ttu-id="0658e-115">또는 실행 게스트를 수동으로 패키징할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-115">Alternatively you can manually package the guest executable.</span></span> <span data-ttu-id="0658e-116">수동 패키징의 경우 이 문서에서는 [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool)에서 제공되는 Service Fabric 패키징 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-116">For the manual packaging, this article uses the Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-the-nodejs-application"></a><span data-ttu-id="0658e-117">Node.js 응용 프로그램 패키징</span><span class="sxs-lookup"><span data-stu-id="0658e-117">Packaging the Node.js application</span></span>
<span data-ttu-id="0658e-118">이 문서에서는 서비스 패브릭 클러스터의 노드에 Node.js가 아직 설치되지 않은 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-118">This article assumes that Node.js is not installed on the nodes in the Service Fabric cluster.</span></span> <span data-ttu-id="0658e-119">결과적으로 패키징 전에 노드 응용 프로그램의 루트 디렉터리에 node.exe를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-119">As a consequence, you need to add Node.exe to the root directory of your node application before packaging.</span></span> <span data-ttu-id="0658e-120">Node.js 응용 프로그램의 디렉터리 구조(Express 웹 프레임워크 및 Jade 템플릿 엔진 사용)는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-120">The directory structure of the Node.js application (using Express web framework and Jade template engine) should look similar to the one below:</span></span>

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

<span data-ttu-id="0658e-121">다음 단계는 Node.js 응용 프로그램에 대한 응용 프로그램 패키지를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-121">As a next step, you create an application package for the Node.js application.</span></span> <span data-ttu-id="0658e-122">아래 코드는 Node.js 응용 프로그램을 포함하는 서비스 패브릭 응용 프로그램 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-122">The code below creates a Service Fabric application package that contains the Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="0658e-123">다음은 사용 중인 매개 변수에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-123">Below is a description of the parameters that are being used:</span></span>

* <span data-ttu-id="0658e-124">**/source** : 패키지할 응용 프로그램의 디렉터리를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-124">**/source** points to the directory of the application that should be packaged.</span></span>
* <span data-ttu-id="0658e-125">**/target** : 패키지를 만들 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-125">**/target** defines the directory in which the package should be created.</span></span> <span data-ttu-id="0658e-126">이 디렉터리는 원본 디렉터리와 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-126">This directory has to be different from the source directory.</span></span>
* <span data-ttu-id="0658e-127">**/appname** : 기존 응용 프로그램의 응용 프로그램 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-127">**/appname** defines the application name of the existing application.</span></span> <span data-ttu-id="0658e-128">이 이름은 매니페스트에서 서비스 패브릭 응용 프로그램 이름이 아니라 서비스 이름으로 변환된다는 점을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-128">It's important to understand that this translates to the service name in the manifest, and not to the Service Fabric application name.</span></span>
* <span data-ttu-id="0658e-129">**/exe**: Service Fabric이 시작할 실행 파일을 정의합니다. 이 예에서는 `node.exe`입니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-129">**/exe** defines the executable that Service Fabric is supposed to launch, in this case `node.exe`.</span></span>
* <span data-ttu-id="0658e-130">**/ma** : 실행 파일을 시작하는 데 사용되는 인수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-130">**/ma** defines the argument that is being used to launch the executable.</span></span> <span data-ttu-id="0658e-131">Node.js가 설치되지 않았기 때문에 서비스 패브릭에서 `node.exe bin/www`를 실행하여 Node.js 웹 서버를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-131">As Node.js is not installed, Service Fabric needs to launch the Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="0658e-132">`/ma:'bin/www'`는 패키징 도구에 `bin/ma`를 node.exe의 인수로 사용하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-132">`/ma:'bin/www'` tells the packaging tool to use `bin/ma` as the argument for node.exe.</span></span>
* <span data-ttu-id="0658e-133">**/AppType** : 서비스 패브릭 응용 프로그램 형식 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-133">**/AppType** defines the Service Fabric application type name.</span></span>

<span data-ttu-id="0658e-134">/target 매개 변수에서 지정한 디렉터리로 이동하면 다음과 같이 도구가 완벽하게 작동하는 서비스 패브릭 패키지를 만든 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-134">If you browse to the directory that was specified in the /target parameter, you can see that the tool has created a fully functioning Service Fabric package as shown below:</span></span>

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
<span data-ttu-id="0658e-135">생성된 ServiceManifest.xml에는 이제 아래의 코드 조각과 같이 Node.js 웹 서버를 시작하는 방법을 설명하는 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-135">The generated ServiceManifest.xml now has a section that describes how the Node.js web server should be launched, as shown in the code snippet below:</span></span>

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
<span data-ttu-id="0658e-136">이 샘플에서 Node.js 웹 서버는 포트 3000에서 수신하므로 ServiceManifest.xml 파일의 끝점 정보를 아래와 같이 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-136">In this sample, the Node.js web server listens to port 3000, so you need to update the endpoint information in the ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-the-mongodb-application"></a><span data-ttu-id="0658e-137">MongoDB 응용 프로그램 패키징</span><span class="sxs-lookup"><span data-stu-id="0658e-137">Packaging the MongoDB application</span></span>
<span data-ttu-id="0658e-138">Node.js 응용 프로그램을 패키지했으므로 이제 MongoDB를 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-138">Now that you have packaged the Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="0658e-139">앞서 언급했듯이 이제부터 수행할 단계는 Node.js 및 MongoDB에만 적용되는 것이 아니라</span><span class="sxs-lookup"><span data-stu-id="0658e-139">As mentioned before, the steps that you go through now are not specific to Node.js and MongoDB.</span></span> <span data-ttu-id="0658e-140">하나의 서비스 패브릭 응용 프로그램으로 패키지되어야 하는 모든 응용 프로그램에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-140">In fact, they apply to all applications that are meant to be packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="0658e-141">MongoDB를 패키지하려면 Mongod.exe 및 Mongo.exe를 패키지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-141">To package MongoDB, you want to make sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="0658e-142">이 두 이진 파일은 MongoDB 설치 디렉터리의 `bin` 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-142">Both binaries are located in the `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="0658e-143">디렉터리 구조는 아래와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-143">The directory structure looks similar to the one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="0658e-144">서비스 패브릭에서 아래와 유사한 명령을 사용하여 MongoDB를 시작해야 하므로 MongoDB를 패키지할 때 `/ma` 매개 변수를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-144">Service Fabric needs to start MongoDB with a command similar to the one below, so you need to use the `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path to data]
```
> [!NOTE]
> <span data-ttu-id="0658e-145">MongoDB 데이터 디렉터리를 노드의 로컬 디렉터리에 넣으면 노드 오류 발생 시 데이터가 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-145">The data is not being preserved in the case of a node failure if you put the MongoDB data directory on the local directory of the node.</span></span> <span data-ttu-id="0658e-146">데이터 손실을 방지하려면 지속형 저장소를 사용하거나 MongoDB 복제본 세트를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-146">You should either use durable storage or implement a MongoDB replica set in order to prevent data loss.</span></span>  
>
>

<span data-ttu-id="0658e-147">PowerShell 또는 명령 셸에서 다음 매개 변수와 함께 패키징 도구를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-147">In PowerShell or the command shell, we run the packaging tool with the following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path to data]' /AppType:NodeAppType
```

<span data-ttu-id="0658e-148">서비스 패브릭 응용 프로그램 패키지에 MongoDB를 추가하려면 /target 매개 변수가 응용 프로그램 매니페스트와 Node.js 응용 프로그램이 이미 포함된 디렉터리를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-148">In order to add MongoDB to your Service Fabric application package, you need to make sure that the /target parameter points to the same directory that already contains the application manifest along with the Node.js application.</span></span> <span data-ttu-id="0658e-149">또한 동일한 ApplicationType 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-149">You also need to make sure that you are using the same ApplicationType name.</span></span>

<span data-ttu-id="0658e-150">해당 디렉터리로 이동하여 도구가 만든 항목을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-150">Let's browse to the directory and examine what the tool has created.</span></span>

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
<span data-ttu-id="0658e-151">도구가 MongoDB 이진 파일이 포함된 디렉터리에 새 폴더 MongoDB를 추가했음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-151">As you can see, the tool added a new folder, MongoDB, to the directory that contains the MongoDB binaries.</span></span> <span data-ttu-id="0658e-152">이제 `ApplicationManifest.xml` 파일을 열면 패키지에 Node.js 응용 프로그램과 MongoDB가 모두 포함된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-152">If you open the `ApplicationManifest.xml` file, you can see that the package now contains both the Node.js application and MongoDB.</span></span> <span data-ttu-id="0658e-153">아래 코드는 응용 프로그램 매니페스트의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-153">The code below shows the content of the application manifest.</span></span>

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

### <a name="publishing-the-application"></a><span data-ttu-id="0658e-154">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="0658e-154">Publishing the application</span></span>
<span data-ttu-id="0658e-155">마지막 단계는 아래의 PowerShell 스크립트를 사용하여 로컬 서비스 패브릭 클러스터에 응용 프로그램을 게시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-155">The last step is to publish the application to the local Service Fabric cluster by using the PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="0658e-156">응용 프로그램을 성공적으로 로컬 클러스터에 게시한 후에는 Node.js 응용 프로그램의 서비스 매니페스트에 입력한 포트(예: http://localhost:3000)에서 Node.js 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-156">Once the application is successfully published to the local cluster, you can access the Node.js application on the port that we have entered in the service manifest of the Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="0658e-157">이 자습서에서는 간편하게 두 기존 응용 프로그램을 하나의 서버 패브릭 응용 프로그램으로 패키지하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-157">In this tutorial, you have seen how to easily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="0658e-158">또한 고가용성 및 상태 시스템 통합 같은 서비스 패브릭의 장점을 활용할 수 있도록 응용 프로그램을 서비스 패브릭에 배포하는 방법도 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-158">You have also learned how to deploy it to Service Fabric so that it can benefit from some of the Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-to-an-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="0658e-159">Linux에서 Yeoman를 사용하여 기존 응용 프로그램에 더 많은 게스트 실행 파일 추가</span><span class="sxs-lookup"><span data-stu-id="0658e-159">Adding more guest executables to an existing application using Yeoman on Linux</span></span>

<span data-ttu-id="0658e-160">`yo`을 사용하여 만든 응용 프로그램에 다른 서비스를 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-160">To add another service to an application already created using `yo`, perform the following steps:</span></span> 
1. <span data-ttu-id="0658e-161">기존 응용 프로그램의 루트로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-161">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="0658e-162">예를 들어 `MyApplication`이 Yeoman에서 만든 응용 프로그램인 경우 `cd ~/YeomanSamples/MyApplication`입니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="0658e-163">`yo azuresfguest:AddService`를 실행하고 필요한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-163">Run `yo azuresfguest:AddService` and provide the necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0658e-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0658e-164">Next steps</span></span>
* <span data-ttu-id="0658e-165">[Service Fabric 및 컨테이너 개요](service-fabric-containers-overview.md)에서 컨테이너 배포 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0658e-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="0658e-166">게스트 실행 파일을 패키징 및 배포하는 샘플</span><span class="sxs-lookup"><span data-stu-id="0658e-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="0658e-167">REST를 사용하여 이름 지정 서비스를 통해 통신하는 두 게스트 실행 파일(C# 및 nodejs)의 샘플</span><span class="sxs-lookup"><span data-stu-id="0658e-167">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
