---
title: "Linux에서 Azure 서비스 패브릭 행위자 신뢰할 수 있는 Java 응용 프로그램 aaaCreate | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate 및 5 분 후에는 Java 서비스 패브릭 행위자 신뢰할 수 있는 응용 프로그램을 배포 합니다."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Linux에서 첫 번째 Java Service Fabric Reliable Actors 응용 프로그램 만들기
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

이 빠른 시작을 통해 몇 분만에 Linux 개발 환경에서 첫 번째 Azure Service Fabric Java 응용 프로그램을 만들 수 있습니다.  완료 되 면 hello 로컬 개발 클러스터에서 실행 되는 단순한 Java 단일 서비스 응용 프로그램을 해야 합니다.  

## <a name="prerequisites"></a>필수 조건
시작 하기 전에 hello 서비스 패브릭 SDK를 설치, 서비스 패브릭 CLI hello 및 개발 클러스터에 설치 프로그램 [Linux 개발 환경](service-fabric-get-started-linux.md)합니다. Mac OS X을 사용하는 경우 [Vagrant를 사용하여 가상 컴퓨터에서 Linux 개발 환경을 설정](service-fabric-get-started-mac.md)할 수 있습니다.

Tooinstall hello 내용도 [서비스 패브릭 CLI](service-fabric-cli.md)합니다.

### <a name="install-and-set-up-hello-generators-for-java"></a>설치 및 Java 용 hello 생성기 설정
Service Fabric은 Yeoman 템플릿 생성기를 사용하여 터미널에서 Service Fabric Java 응용 프로그램을 만들 수 있는 스캐폴딩 도구를 제공합니다. Java 용 hello 서비스 패브릭 yeoman 템플릿 생성기가 컴퓨터에 관한 작업 방법을 tooensure 아래 hello 단계를 따르십시오.
1. 컴퓨터에서 Node.js 및 NPM 설치

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. NPM의 컴퓨터에 [Yeoman](http://yeoman.io/) 템플릿 생성기 설치

  ```bash
  sudo npm install -g yo
  ```
3. 서비스 패브릭 Yeo Java 응용 프로그램 생성기 hello NPM에서 설치

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Hello 응용 프로그램 만들기
서비스 패브릭 응용 프로그램에는 각각 hello 응용 프로그램의 기능을 제공 하 여 특정 역할에 있는 하나 이상의 서비스 포함 되어 있습니다. hello 마지막 섹션에는 설치 된 hello 생성기 쉽게 toocreate를 사용 하면 첫 번째 서비스 및 tooadd 나중에 더 합니다.  Eclipse용 플러그 인을 사용하여 Service Fabric Java 응용 프로그램을 만들고 빌드하고 배포할 수 있습니다. [Eclipse를 사용하여 첫 번째 Java 응용 프로그램 만들기 및 배포](service-fabric-get-started-eclipse.md)를 참조하세요. 이 빠른 시작에 대 한 Yeoman toocreate 응용 프로그램을 사용 하 여 단일 서비스를 저장 하 고 카운터 값을 가져옵니다.

1. 터미널에서 ``yo azuresfjava``을 입력합니다.
2. 응용 프로그램의 이름을 지정합니다.
3. Hello 유형의 첫 번째 서비스를 선택 하 고 이름을 지정 합니다. 이 자습서에서 Reliable Actor 서비스를 선택합니다. Hello에 대 한 자세한 내용은 다른 종류의 서비스 참조 [프로그래밍 모델 개요 서비스 패브릭](service-fabric-choose-framework.md)합니다.
   ![Java용 Service Fabric Yeoman 생성기][sf-yeoman]

## <a name="build-hello-application"></a>Hello 응용 프로그램 빌드
에 대 한 빌드 스크립트를 포함 하는 hello 서비스 패브릭 Yeoman 템플릿 [Gradle](https://gradle.org/), 어떤 터미널 hello에서 toobuild hello 응용 프로그램을 사용할 수 있습니다.
Maven에서 Service Fabric Java 종속성을 가져옵니다. toobuild 및 hello 서비스 패브릭 Java 응용 프로그램에서 작업 tooensure JDK가 있고 Gradle 설치 해야 합니다. 아직 설치 되지 않은, hello를 실행할 수 있습니다 tooinstall JDK(openjdk-8-jdk) 및 Gradle-

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild 및 패키지 hello 응용 프로그램을 hello 다음 실행:

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Hello 응용 프로그램 배포
Hello 응용 프로그램으로 빌드하고 나면 toohello 쿼럼 응답을 배포할 수 있습니다.

1. Toohello 로컬 서비스 패브릭 클러스터를 연결 합니다.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Hello 템플릿 toocopy에 제공 된 실행된 hello 설치 스크립트 응용 프로그램 패키지 toohello 클러스터 이미지 저장소 hello, hello 응용 프로그램 형식 등록 및 hello 응용 프로그램의 인스턴스를 만듭니다.

    ```bash
    ./install.sh
    ```

배포 hello 작성 된 응용 프로그램이 다른 서비스 패브릭 응용 프로그램으로 동일한 hello입니다. Hello 설명서를 참조 하십시오 [서비스 패브릭 CLI hello로 서비스 패브릭 응용 프로그램 관리](service-fabric-application-lifecycle-sfctl.md) 자세한 지침에 대 한 합니다.

매개 변수 toothese 명령은 생성 하는 hello 매니페스트 hello 응용 프로그램 패키지 내에서 찾을 수 있습니다.

Hello 응용 프로그램을 배포한 후 브라우저를 열고 탐색 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 에서 [http://localhost:19080/탐색기](http://localhost:19080/Explorer)합니다.
그런 다음 확대 하는 hello **응용 프로그램** 노드 및 응용 프로그램 종류에 대 한 항목 및 해당 형식의 첫 번째 인스턴스 hello에 대 한 다른 이제는 합니다.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Hello 테스트 클라이언트를 시작 하 고 장애 조치를 수행 합니다.
행위자 자체적으로 아무 작업도 수행 하지 않습니다, 다른 서비스 또는 클라이언트 toosend 필요로 할 메시지입니다. hello 행위자 템플릿은 toointeract hello 행위자 서비스와 함께 사용할 수 있는 간단한 테스트 스크립트를 포함 합니다.

1. Hello 조사식 유틸리티 toosee hello 출력 hello 행위자 서비스를 사용 하 여 hello 스크립트를 실행 합니다.  hello를 호출 하는 hello 테스트 스크립트 `setCountAsync()` hello 행위자 tooincrement 하는 카운터를 메서드 호출 hello `getCountAsync()` 메서드 hello 행위자 tooget hello 새 카운터 값 및 해당 값을 toohello 콘솔 표시를 합니다.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. 서비스 패브릭 탐색기에서 hello 노드 호스팅 hello 주 복제본을 hello 행위자 서비스에 대 한를 찾습니다. 아래 hello 스크린샷에서에서 노드 3입니다. hello 기본 서비스 복제본 핸들 읽기 및 쓰기 작업입니다.  서비스 상태에 변경 내용은 toohello 보조 복제본, 노드 0 및 hello 화면 아래에 1에서 실행 중인 다음 복제 됩니다.

    ![서비스 패브릭 탐색기에서 주 복제본 hello 찾기][sfx-primary]

3. **노드**, hello 이전 단계에서 찾은 다음 선택 hello 노드를 클릭 **비활성화 (다시 시작)** hello 작업 메뉴에서 합니다. 이 작업 hello 기본 서비스 복제본을 실행 하는 hello 노드를 다시 시작 되 고 다른 노드에서 실행 하는 hello 보조 복제본의 장애 조치 tooone를 수행 합니다.  해당 보조 복제본이 승격된 tooprimary, 다른 보조 복제본은 서로 다른 노드에 만들고 hello 주 복제본 tootake 읽기/쓰기 작업을 시작 합니다. Hello 노드 다시 시작 되 면 hello 테스트 클라이언트가 고 해당 hello 카운터 계속 tooincrement 불구 하 고 hello 장애 조치 메모의 hello 출력을 살펴보십시오.

## <a name="remove-hello-application"></a>Hello 응용 프로그램 제거
Hello 템플릿 toodelete hello 응용 프로그램 인스턴스에 제공 된 hello 제거 스크립트를 사용 하 여, hello 응용 프로그램 패키지 등록 취소 하 고 hello 클러스터 이미지 저장소에서 hello 응용 프로그램 패키지를 제거 합니다.

```bash
./uninstall.sh
```

서비스 패브릭 탐색기 표시는 hello 응용 프로그램 및 응용 프로그램 형식에에서 더 이상 표시 hello **응용 프로그램** 노드.

## <a name="service-fabric-java-libraries-on-maven"></a>Maven의 Service Fabric Java 라이브러리
Service Fabric Java 라이브러리는 Maven에서 호스팅되었습니다. Hello에 hello 종속성을 추가할 수 있습니다 ``pom.xml`` 또는 ``build.gradle`` 에서 프로젝트 toouse 서비스 패브릭 Java 라이브러리가 **mavenCentral**합니다.

### <a name="actors"></a>행위자

응용 프로그램에 대한 Service Fabric Reliable Actor 지원입니다.

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

### <a name="services"></a>Services

응용 프로그램에 대한 Service Fabric 상태 비저장 서비스 지원입니다.

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

### <a name="others"></a>기타
#### <a name="transport"></a>전송

Service Fabric Java 응용 프로그램에 대한 전송 계층 지원입니다. 않아도 hello 전송 계층에서 프로그래밍 하는 경우가 아니면 tooexplicitly이 종속성 tooyour Reliable Actor 또는 서비스 응용 프로그램을 추가 합니다.

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

#### <a name="fabric-support"></a>패브릭 지원

서비스 패브릭 런타임을 toonative 발언 서비스 패브릭에서 시스템 수준 지원 합니다. 않아도 tooexplicitly이 종속성 tooyour Reliable Actor 또는 서비스 응용 프로그램을 추가 합니다. Maven에서 자동으로 페치 가져옵니다이 포함 하는 경우 hello 위의 다른 종속성.

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

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Maven 함께 사용 하는 기존 서비스 패브릭 Java 응용 프로그램 toobe 마이그레이션
서비스 패브릭 Java SDK tooMaven 리포지토리에서 최근 서비스 패브릭 Java 라이브러리 전환 했습니다. 기존 서비스 패브릭 상태 비저장 또는 hello 서비스를 사용 하는 행위자 Java 응용 프로그램 hello 새 응용 프로그램 Yeoman 또는 Eclipse를 사용 하 여 생성 됩니다 (Maven으로 수 toowork 됩니다)는 최신 버전에 업데이트 된 프로젝트를 생성 하는 동안 업데이트할 수 있습니다. 패브릭 Java SDK 앞에서 Maven에서 toouse hello 서비스 패브릭 Java 종속성. 언급 된 hello 단계를 따르십시오 [여기](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure Maven으로 오래 된 응용 프로그램이 작동 합니다.

## <a name="next-steps"></a>다음 단계

* [Eclipse를 사용하여 Linux에서 첫 번째 Service Fabric Java 응용 프로그램 만들기](service-fabric-get-started-eclipse.md)
* [Reliable Actors에 대해 자세히 알아보기](service-fabric-reliable-actors-introduction.md)
* [서비스 패브릭 CLI hello를 사용 하 여 서비스 패브릭 클러스터와 상호 작용](service-fabric-cli.md)
* [Service Fabric 지원 옵션](service-fabric-support.md) 알아보기
* [Service Fabric CLI 시작](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
