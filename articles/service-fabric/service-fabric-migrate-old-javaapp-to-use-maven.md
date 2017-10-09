---
title: "Java SDK tooMaven-aaaMigrate 업데이트 이전 Azure 서비스 패브릭 Java 응용 프로그램 toouse Maven | Microsoft Docs"
description: "Hello 이전 Java 응용 프로그램 toouse hello 서비스 패브릭 Java SDK 사용 Maven에서 toofetch 서비스 패브릭 Java 종속 요소를 업데이트 합니다. 이 설치를 완료 한 후 이전 Java 응용 프로그램 수 toobuild 것입니다."
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
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="f678e-104">Maven에서 있는 이전 Java 서비스 패브릭 응용 프로그램 toofetch의 Java 라이브러리 업데이트</span><span class="sxs-lookup"><span data-stu-id="f678e-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="f678e-105">서비스 패브릭 Java 바이너리 hello 서비스 패브릭 Java SDK tooMaven 호스팅에서 최근에 전환 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="f678e-106">에서는 이제 **mavencentral** toofetch hello 최신 서비스 패브릭 Java 종속성.</span><span class="sxs-lookup"><span data-stu-id="f678e-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="f678e-107">Toobe 앞서 만든 기존 Java 응용 프로그램을 업데이트 하는이 빠른 시작 사용 하면 템플릿이나 Eclipse toobe 기반 Maven 빌드에서 hello와 호환 Yeoman 중 하나를 사용 하 여 서비스 패브릭 Java SDK와 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f678e-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f678e-108">Prerequisites</span></span>
1. <span data-ttu-id="f678e-109">Toouninstall 먼저 기존 Java SDK hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="f678e-110">서비스 패브릭 CLI 다음 최신 설치 hello hello 언급 한 단계 [여기](service-fabric-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="f678e-111">toobuild 및 hello 서비스 패브릭 Java 응용 프로그램에서 작업 tooensure JDK 1.8 있고 Gradle 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="f678e-112">설치 하지 않은 경우 실행할 수 있습니다 (openjdk 8 jdk) JDK 1.8 및 Gradle-tooinstall 다음 hello</span><span class="sxs-lookup"><span data-stu-id="f678e-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="f678e-113">응용 프로그램 toouse의 업데이트 hello 설치/제거 스크립트 hello 언급 된 hello 단계 새 서비스 패브릭 CLI [여기](service-fabric-application-lifecycle-sfctl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="f678e-114">시작 tooour 참조할 수 있습니다 [예제](https://github.com/Azure-Samples/service-fabric-java-getting-started) 참조에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="f678e-115">서비스 패브릭 Java SDK hello를 제거한 후 Yeoman 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="f678e-116">언급 된 hello 필수 구성 요소에 따라 [여기](service-fabric-create-your-first-linux-application-with-java.md) toohave 서비스 패브릭 Yeoman Java 템플릿 생성기를 작동 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="f678e-117">Maven의 Service Fabric Java 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f678e-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="f678e-118">Service Fabric Java 라이브러리는 Maven에서 호스팅되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="f678e-119">Hello에 hello 종속성을 추가할 수 있습니다 ``pom.xml`` 또는 ``build.gradle`` 에서 프로젝트 toouse 서비스 패브릭 Java 라이브러리가 **mavenCentral**합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="f678e-120">행위자</span><span class="sxs-lookup"><span data-stu-id="f678e-120">Actors</span></span>

<span data-ttu-id="f678e-121">응용 프로그램에 대한 Service Fabric Reliable Actor 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-121">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="f678e-122">Services</span><span class="sxs-lookup"><span data-stu-id="f678e-122">Services</span></span>

<span data-ttu-id="f678e-123">응용 프로그램에 대한 Service Fabric 상태 비저장 서비스 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-123">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="f678e-124">기타</span><span class="sxs-lookup"><span data-stu-id="f678e-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="f678e-125">전송</span><span class="sxs-lookup"><span data-stu-id="f678e-125">Transport</span></span>

<span data-ttu-id="f678e-126">Service Fabric Java 응용 프로그램에 대한 전송 계층 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="f678e-127">않아도 hello 전송 계층에서 프로그래밍 하는 경우가 아니면 tooexplicitly이 종속성 tooyour Reliable Actor 또는 서비스 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="f678e-128">패브릭 지원</span><span class="sxs-lookup"><span data-stu-id="f678e-128">Fabric support</span></span>

<span data-ttu-id="f678e-129">서비스 패브릭 런타임을 toonative 발언 서비스 패브릭에서 시스템 수준 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="f678e-130">않아도 tooexplicitly이 종속성 tooyour Reliable Actor 또는 서비스 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="f678e-131">Maven에서 자동으로 페치 가져옵니다이 포함 하는 경우 hello 위의 다른 종속성.</span><span class="sxs-lookup"><span data-stu-id="f678e-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="f678e-132">Service Fabric 상태 비저장 서비스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="f678e-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="f678e-133">기존 서비스 패브릭 상태 비저장 Java 서비스 Maven에서 인출 되는 서비스 패브릭 종속성을 사용 하 여를 해야 tooupdate hello toobe 수 toobuild ``build.gradle`` hello 서비스 내에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="f678e-134">이전에 것 처럼 toobe 다음과 같이 사용-</span><span class="sxs-lookup"><span data-stu-id="f678e-134">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
<span data-ttu-id="f678e-135">Maven에서에서 toofetch hello 종속성 hello 이제 **업데이트** ``build.gradle`` 것이 hello 해당 부분은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
<span data-ttu-id="f678e-136">일반적으로 tooget hello 스크립트를 구축 하는 방법에 대 한 전반적인 관념 다음과 같은 상태 비저장 Java 서비스 패브릭 서비스, 시작 예제에서 tooany 샘플을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="f678e-137">여기에 hello [의 build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) hello EchoServer 샘플에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="f678e-138">Service Fabric 행위자 서비스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="f678e-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="f678e-139">기존 서비스 패브릭 행위자 Java 응용 프로그램 서비스 패브릭 종속성 Maven에서 반입를 사용 하 여 해야 tooupdate hello toobe 수 toobuild ``build.gradle`` hello 인터페이스 패키지 안쪽과 hello 서비스 패키지에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="f678e-140">TestClient 패키지를 사용 하는 경우 해야 tooupdate 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="f678e-141">따라서 프로그램 작업자에 대해 ``Myactor``, hello 다음 hello 장소 tooupdate-해야 하는 것이</span><span class="sxs-lookup"><span data-stu-id="f678e-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="f678e-142">Hello 인터페이스 프로젝트에 대 한 빌드 스크립트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="f678e-143">이전에 것 처럼 toobe 다음과 같이 사용-</span><span class="sxs-lookup"><span data-stu-id="f678e-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="f678e-144">Maven에서에서 toofetch hello 종속성 hello 이제 **업데이트** ``build.gradle`` 것이 hello 해당 부분은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="f678e-145">Hello 행위자 프로젝트에 대 한 빌드 스크립트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="f678e-146">이전에 것 처럼 toobe 다음과 같이 사용-</span><span class="sxs-lookup"><span data-stu-id="f678e-146">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
<span data-ttu-id="f678e-147">Maven에서에서 toofetch hello 종속성 hello 이제 **업데이트** ``build.gradle`` 것이 hello 해당 부분은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="f678e-148">Hello 테스트 클라이언트 프로젝트에 대 한 빌드 스크립트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="f678e-149">여기에서 변경 hello 행위자 프로젝트 즉, 이전 섹션에서 설명 하는 유사한 toohello 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="f678e-150">이전에 사용 되는 스크립트 toobe 다음과 같습니다. 같은 Gradle hello</span><span class="sxs-lookup"><span data-stu-id="f678e-150">Previously hello Gradle script used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
<span data-ttu-id="f678e-151">Maven에서에서 toofetch hello 종속성 hello 이제 **업데이트** ``build.gradle`` 것이 hello 해당 부분은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f678e-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a><span data-ttu-id="f678e-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f678e-152">Next steps</span></span>

* [<span data-ttu-id="f678e-153">Yeoman을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="f678e-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="f678e-154">Eclipse용 Service Fabric 플러그 인을 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="f678e-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="f678e-155">서비스 패브릭 CLI hello를 사용 하 여 서비스 패브릭 클러스터와 상호 작용</span><span class="sxs-lookup"><span data-stu-id="f678e-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
