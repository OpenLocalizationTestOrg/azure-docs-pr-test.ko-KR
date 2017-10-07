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
# <a name="create-your-first-azure-service-fabric-application"></a>첫 번째 Azure Service Fabric 응용 프로그램 만들기
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric은 .NET Core 및 Java 모두에서 Linux에 대한 서비스를 구축하는 SDK를 제공합니다. 이 자습서에서는 방법을 살펴볼 toocreate Linux와 빌드 C# (.NET Core)를 사용 하 여 서비스에 대 한 응용 프로그램입니다.

## <a name="prerequisites"></a>필수 조건
시작하기 전에 [Linux 개발 환경을 설정](service-fabric-get-started-linux.md)하도록 합니다. Mac OS X을 사용하는 경우 [Vagrant를 사용하여 가상 컴퓨터에서 Linux one-box 환경을 설정](service-fabric-get-started-mac.md)할 수 있습니다.

Tooinstall hello 내용도 [서비스 패브릭 CLI](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>설치 및 hello 생성기 CSharp에 대 한 설정
Service Fabric은 Yeoman 템플릿 생성기를 사용하여 터미널에서 Service Fabric CSharp 응용 프로그램을 만들 수 있는 스캐폴딩 도구를 제공합니다. CSharp 컴퓨터에서 작업에 대 한 hello 서비스 패브릭 yeoman 템플릿 생성기가 tooensure 아래 hello 단계를 따르십시오.
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
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Hello 응용 프로그램 만들기
서비스 패브릭 응용 프로그램에는 각각 hello 응용 프로그램의 기능을 제공 하 여 특정 역할에 있는 하나 이상의 서비스 포함 될 수 있습니다. 서비스 패브릭 hello [Yeoman](http://yeoman.io/) CSharp 마지막 단계에서 설치에 대 한 생성기 쉽게 toocreate를 사용 하면 첫 번째 서비스 및 tooadd 나중에 더 합니다. 단일 서비스 Yeoman toocreate 응용 프로그램을 사용 합니다.

1. 종료, hello hello 스 캐 폴딩 빌드 명령 toostart 다음을 입력 합니다.`yo azuresfcsharp`
2. 응용 프로그램의 이름을 지정합니다.
3. Hello 유형의 첫 번째 서비스를 선택 하 고 이름을 지정 합니다. 이 자습서의 hello 위해 신뢰할 수 있는 행위자 서비스를 선택 했습니다.

   ![C#용 Service Fabric Yeoman 생성기][sf-yeoman]

> [!NOTE]
> Hello 옵션에 대 한 자세한 내용은 참조 [프로그래밍 모델 개요 서비스 패브릭](service-fabric-choose-framework.md)합니다.
>
>

## <a name="build-hello-application"></a>Hello 응용 프로그램 빌드
hello 서비스 패브릭 Yeoman 템플릿에 (toohello 응용 프로그램 폴더를 탐색 하는) 한 후 터미널 hello toobuild hello 응용 프로그램을 사용할 수 있는 빌드 스크립트를 포함 합니다.

  ```sh
 cd myapp
 ./build.sh
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

Hello 응용 프로그램을 배포한 후 브라우저를 열고 탐색 [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 에서 [http://localhost:19080/탐색기](http://localhost:19080/Explorer)합니다. 그런 다음 확대 하는 hello **응용 프로그램** 노드 및 응용 프로그램 종류에 대 한 항목 및 해당 형식의 첫 번째 인스턴스 hello에 대 한 다른 이제는 합니다.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Hello 테스트 클라이언트를 시작 하 고 장애 조치를 수행 합니다.
행위자 프로젝트 자체에서는 아무 것도 수행하지 않습니다. 다른 서비스 또는 클라이언트 toosend 필요로 할 메시지입니다. hello 행위자 템플릿은 toointeract hello 행위자 서비스와 함께 사용할 수 있는 간단한 테스트 스크립트를 포함 합니다.

1. Hello 조사식 유틸리티 toosee hello 출력 hello 행위자 서비스를 사용 하 여 hello 스크립트를 실행 합니다.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. 서비스 패브릭 탐색기에서 hello hello 행위자 서비스에 대 한 주 복제본을 호스팅하는 노드를 찾습니다. 아래 hello 스크린샷에서에서 노드 3입니다.

    ![서비스 패브릭 탐색기에서 주 복제본 hello 찾기][sfx-primary]
3. Hello 이전 단계에서 찾은 다음 선택 hello 노드를 클릭 **비활성화 (다시 시작)** hello 작업 메뉴에서 합니다. 이 작업에 다른 노드에서 실행 중인 장애 조치 tooa 보조 복제본을 강제 적용 하 여 로컬 클러스터의 한 노드에서 다시 시작 합니다. 이 작업을 수행 하면 hello 테스트 클라이언트가 고 해당 hello 카운터 tooincrement hello 장애 조치 되더라도 계속 참고에서 주의 기울여야 toohello 출력을 해야 합니다.

## <a name="adding-more-services-tooan-existing-application"></a>더 많은 서비스 tooan 기존 응용 프로그램 추가

tooadd 서비스 tooan 이미 다른 응용 프로그램 사용 하 여 만든 `yo`, hello 다음 단계를 수행 합니다.
1. Hello 기존 응용 프로그램의 toohello 루트 디렉터리를 변경 합니다.  예를 들어 `cd ~/YeomanSamples/MyApplication`경우 `MyApplication` 는 Yeoman에서 만든 hello 응용 프로그램입니다.
2. `yo azuresfcsharp:AddService` 실행

## <a name="migrating-from-projectjson-toocsproj"></a>Project.json too.csproj에서 마이그레이션
1. 프로젝트 루트 디렉터리에서 ' 마이그레이션할 dotnet' 실행 되는 모든 hello project.json toocsproj 형식을 마이그레이션합니다.
2. 업데이트 hello 프로젝트 참조 프로젝트 파일의 파일 toocsproj 적절 하 게 합니다.
3. Build.sh의 hello 프로젝트 파일 이름을 toocsproj 파일을 업데이트 합니다.

## <a name="next-steps"></a>다음 단계

* [Reliable Actors에 대해 자세히 알아보기](service-fabric-reliable-actors-introduction.md)
* [서비스 패브릭 CLI hello를 사용 하 여 서비스 패브릭 클러스터와의 상호 작용](service-fabric-cli.md)
* [Service Fabric 지원 옵션](service-fabric-support.md) 알아보기
* [Service Fabric CLI 시작](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
