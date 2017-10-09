---
title: "aaaCreate 프로그램 첫 번째 신뢰할 수 있는 Azure 마이크로 서비스 java에서 | Microsoft Docs"
description: "Microsoft Azure 서비스 패브릭 응용 프로그램에 상태 비저장 및 상태 저장 서비스 toocreating를 소개 합니다."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Reliable Services로 시작하기
> [!div class="op_single_selector"]
> * [Windows에서 C#](service-fabric-reliable-services-quick-start.md)
> * [Linux에서 Java](service-fabric-reliable-services-quick-start-java.md)
>
>

이 문서는 Azure 서비스 패브릭 신뢰할 수 있는 서비스의 hello 기본 사항에 설명 하 고 만들기 및 Java로 작성 된 간단한 신뢰할 수 있는 서비스 응용 프로그램을 배포 하는 과정을 보여 줍니다. 이 Microsoft Virtual Academy 비디오 또한를 보면 어떻게 toocreate 상태 비저장 신뢰할 수 있는 서비스:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>설치 및 설정
시작 하기 전에 hello 서비스 패브릭 개발 환경 컴퓨터에 설정 되어 있는지 확인 합니다.
Tooset 해야 할 경우, 상태로 업데이트 너무 않을[Mac에서 시작](service-fabric-get-started-mac.md) 또는 [linux 시작](service-fabric-get-started-linux.md)합니다.

## <a name="basic-concepts"></a>기본 개념
만 신뢰할 수 있는 서비스 시작 tooget toounderstand 몇 가지 기본 개념을 필요 합니다.

* **서비스 유형**: 서비스 구현입니다. 확장 작성 hello 클래스에 의해 정의 된 `StatelessService` 및 다른 코드 또는 종속성 이름 및 버전 번호와 함께 본 사용 합니다.
* **명명 된 서비스 인스턴스**: toorun 사용자가 서비스를 만들면 서비스 유형의 명명 된 인스턴스 훨씬 클래스 형식의 개체 인스턴스를 만들고 있습니다. 서비스 인스턴스는 실제로 사용자가 작성한 서비스 클래스의 개체 인스턴스화입니다.
* **서비스 호스트**: 명명 된 서비스 인스턴스를 만들면 호스트 내 필요 toorun hello 합니다. hello 서비스 호스트는 서비스의 인스턴스를 실행할 수 있는 프로세스 뿐입니다.
* **서비스 등록**: 등록은 모든 항목을 함께 모읍니다. hello 서비스 형식을 등록 해야 서비스 패브릭 hello로 서비스의 런타임 tooallow 서비스 패브릭 toocreate의 인스턴스를 호스트 하기 toorun 합니다.  

## <a name="create-a-stateless-service"></a>상태 비저장 서비스 만들기
Service Fabric 응용 프로그램을 만드는 것으로 시작합니다. Linux 용 서비스 패브릭 SDK hello 포함 한 Yeoman 생성기 tooprovide hello 스 캐 폴딩 상태 비저장 서비스와 서비스 패브릭 응용 프로그램에 대 한 합니다. Hello를 실행 하 여 시작 Yeoman 다음 명령:

```bash
$ yo azuresfjava
```

Hello 지침 toocreate에 따라 한 **신뢰할 수 있는 상태 비저장 서비스**합니다. 이 자습서에서는 이름 "HelloWorldApplication" hello 응용 프로그램 및 hello "HelloWorld"를 서비스합니다. hello에 대 한 디렉터리를 포함 하는 hello 결과 `HelloWorldApplication` 및 `HelloWorld`합니다.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Hello 서비스 구현
**HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**를 엽니다. 이 클래스는 hello 서비스 종류를 정의 하며 모든 코드를 실행할 수 있습니다. hello 서비스 API는 코드에 대 한 두 진입점을 제공 합니다.

* 장기 실행 계산 워크로드 등 모든 워크로드의 실행을 시작할 수 있는 `runAsync()`라는 개방형 진입점 메서드.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* 원하는 통신 스택을 연결할 수 있는 통신 진입점. 사용자 및 다른 서비스에서 요청을 수신하도록 시작할 수 있습니다.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

이 자습서에서는 집중 hello `runAsync()` 진입점 메서드. 바로 코드를 실행하기 시작할 수 있습니다.

### <a name="runasync"></a>RunAsync
hello 플랫폼 서비스의 인스턴스가 tooexecute 배치 하 고 준비 하는 경우이 메서드를 호출 합니다. 상태 비저장 서비스의 경우 단순히 hello 서비스 인스턴스를 열 때 것입니다. 서비스 인스턴스가 닫혀 toobe 해야 할 때 취소 토큰에서 toocoordinate를 제공 됩니다. 서비스 패브릭 서비스 인스턴스의이 열기/닫기 주기 전체적으로 hello 서비스 hello 기간 동안 여러 번 발생할 수 있습니다. 다음을 포함하여 여러 가지 이유로 발생할 수 있습니다.

* hello 시스템 리소스 균형 조정에 대 한 서비스 인스턴스를 이동 합니다.
* 오류는 코드에서 발생합니다.
* hello 응용 프로그램 또는 시스템 업그레이드 됩니다.
* 가동 중단을 경험 하는 hello 기본 하드웨어입니다.

이 오케스트레이션 tookeep 서비스 패브릭에서 관리 하는 항상 사용 가능 하 고 적절히 균형 있는 서비스입니다.

`runAsync()`는 동기적으로 차단하지 않아야 합니다. RunAsync 구현 CompletableFuture tooallow hello 런타임 toocontinue를 반환 해야 합니다. 작업 내 작업을 수행 해야 하는 장기 실행 작업 tooimplement 있어야 하는 경우 CompletableFuture hello 합니다.

#### <a name="cancellation"></a>취소
작업의 취소는 취소 토큰을 제공 하는 hello 조정 되는 협조적 노력 합니다. hello까지 기다렸다가 작업 tooend (에서 성공적으로 완료, 취소 또는 오류) 이동 합니다. 중요 한 toohonor hello 취소 토큰, 완료, 작업 및 종료는 `runAsync()` hello 시스템 취소를 요청 하는 경우 가능한 한 신속 하 게 합니다. hello 다음 예제에서는 어떻게 toohandle 취소 이벤트:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>서비스 등록
서비스 유형 hello 서비스 패브릭 런타임을에 등록 해야 합니다. hello 서비스 형식이 hello에 정의 된 `ServiceManifest.xml` 및 구현 하는 서비스 클래스 `StatelessService`합니다. 서비스 등록 hello 프로세스 주 진입점에서 수행 됩니다. 이 예에서 사용 되는 프로세스를 hello `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

hello Yeoman 스 캐 폴딩 gradle 스크립트 toobuild hello 응용 프로그램 및 bash 스크립트 toodeploy 및 응용 프로그램 제거를 포함 합니다. toorun hello 응용 프로그램, gradle 하는 첫 번째 빌드 hello 적용:

```bash
$ gradle
```

그러면 Service Fabric CLI를 사용하여 배포할 수 있는 Service Fabric 응용 프로그램 패키지를 생성합니다.

### <a name="deploy-with-service-fabric-cli"></a>Service Fabric CLI를 사용하여 배포

hello install.sh 스크립트 hello 필요한 서비스 패브릭 CLI 명령을 toodeploy hello 응용 프로그램 패키지를 포함합니다. Install.sh 스크립트 toodeploy hello 응용 프로그램을 실행 합니다.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>다음 단계

* [Service Fabric CLI 시작](service-fabric-cli.md)
