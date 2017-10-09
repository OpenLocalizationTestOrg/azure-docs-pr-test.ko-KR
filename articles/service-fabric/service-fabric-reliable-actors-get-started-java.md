---
title: "aaaCreate 프로그램 첫 번째 행위자 기반 Azure 마이크로 서비스 java에서 | Microsoft Docs"
description: "이 자습서의 만들기, 디버깅 및 서비스 패브릭 Reliable Actors를 사용 하 여 간단한 행위자 기반 서비스를 배포 hello 단계를 안내 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Reliable Actors 시작
> [!div class="op_single_selector"]
> * [Windows에서 C#](service-fabric-reliable-actors-get-started.md)
> * [Linux에서 Java](service-fabric-reliable-actors-get-started-java.md)
> 
> 

이 문서는 Azure 서비스 패브릭 Reliable Actors의 hello 기본 사항에 설명 하 고 만들기 및 java에서 간단한 Reliable Actor 응용 프로그램을 배포 하는 과정을 보여 줍니다.

## <a name="installation-and-setup"></a>설치 및 설정
시작 하기 전에 hello 서비스 패브릭 개발 환경 컴퓨터에 설정 되어 있는지 확인 합니다.
Tooset 해야 할 경우, 상태로 업데이트 너무 않을[Mac에서 시작](service-fabric-get-started-mac.md) 또는 [linux 시작](service-fabric-get-started-linux.md)합니다.

## <a name="basic-concepts"></a>기본 개념
Reliable Actors만 시작 tooget toounderstand 몇 가지 기본 개념을 필요 합니다.

* **행위자 서비스**. Reliable Actors hello 서비스 패브릭 인프라에 배포할 수 있는 신뢰할 수 있는 서비스에 패키지 됩니다. 행위자 인스턴스는 명명된 서비스 인스턴스에서 활성화됩니다.
* **행위자 등록**. 신뢰할 수 있는 서비스와 함께 하 Reliable Actor 서비스에 등록 된 hello 서비스 패브릭 런타임을 toobe가 필요 합니다. 또한 hello 행위자 형식에 등록 된 hello 행위자 런타임 toobe가 필요 합니다.
* **행위자 인터페이스**. hello 행위자 인터페이스는 사용 되는 toodefine 행위자의 강력한 형식의 공용 인터페이스입니다. Reliable Actor 모델 용어 hello hello 행위자 인터페이스 hello 행위자 hello 메시지 유형을 이해 하 고 처리할 수를 정의 합니다. 클라이언트 응용 프로그램 너무 "send" (비동기) 메시지 toohello 행위자 및 hello 행위자 인터페이스 다른 행위자가 사용 됩니다. Reliable Actors는 여러 인터페이스를 구현할 수 있습니다.
* **ActorProxy 클래스**. hello ActorProxy 클래스 클라이언트 응용 프로그램 tooinvoke에서 사용 하는 hello hello 행위자 인터페이스를 통해 노출 되는 메서드. hello ActorProxy 클래스는 두 가지 중요 한 기능을 제공합니다.
  
  * 이름 확인: hello 클러스터 (찾기 그 데이터베이스가 호스팅될 hello 클러스터의 노드 hello)에서 수 toolocate hello 작업자는 합니다.
  * 오류 처리: hello 행위자 toobe를 필요로 하는 오류 hello 클러스터의 노드 tooanother 재배치 하는 예를 들어,이 메서드 호출을 다시 시도 하 고 다시 후 hello 행위자 위치를 확인할 수 있습니다.

hello tooactor 인터페이스와 관련 된 규칙 설명이 사항이 있습니다.

* 행위자 인터페이스 메서드는 오버로드할 수 없습니다.
* 행위자 인터페이스 메서드에는 out, ref 또는 선택적 매개 변수가 없어야 합니다.
* 제네릭 인터페이스는 지원되지 않습니다.

## <a name="create-an-actor-service"></a>행위자 서비스 만들기
새 Service Fabric 응용 프로그램을 만들어 시작합니다. Linux 용 서비스 패브릭 SDK hello 포함 한 Yeoman 생성기 tooprovide hello 스 캐 폴딩 상태 비저장 서비스와 서비스 패브릭 응용 프로그램에 대 한 합니다. Hello를 실행 하 여 시작 Yeoman 다음 명령:

```bash
$ yo azuresfjava
```

Hello 지침 toocreate에 따라 한 **Reliable Actor 서비스**합니다. 이 자습서에서는 이름을 hello 응용 프로그램 "HelloWorldActorApplication" 및 hello 행위자 "HelloWorldActor." 스 캐 폴딩 다음 hello는 만듭니다.

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>신뢰할 수 있는 행위자 기본 구성 요소
앞에서 설명한 hello 기본 개념 hello Reliable Actor 서비스의 기본 빌딩 블록으로 변환 합니다.

### <a name="actor-interface"></a>행위자 인터페이스
이 hello 작업자에 대해 hello 인터페이스 정의 포함 합니다. Hello 행위자 구현과 hello 행위자를 호출 하 여 일반적으로 의미 toodefine hello 행위자 구현과에서 분리 하 고 다른 여러에서 공유할 수 있는 위치에 있으므로 hello 클라이언트가에서 공유 하는 hello 행위자 계약을 정의 하는이 인터페이스 서비스 또는 클라이언트 응용 프로그램입니다.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>행위자 서비스
여기에는 행위자 구현 및 행위자 등록 코드가 포함됩니다. hello 행위자 클래스 hello 행위자 인터페이스를 구현합니다. 사용자 행위자가 작업을 수행하는 위치입니다.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>행위자 등록
hello 행위자 서비스는 hello 서비스 패브릭 런타임에서 서비스 유형으로 등록 되어야 합니다. 주문 hello 행위자 서비스 toorun 행위자 인스턴스, 행위자 형식 hello 행위자 서비스에도 등록 해야 합니다. hello `ActorRuntime` 등록 메서드는 행위자를 위한이 작업을 수행 합니다.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>테스트 클라이언트
간단한 테스트 클라이언트 응용 프로그램에서 실행할 수 있습니다 별도로 hello 서비스 패브릭 응용 프로그램 tootest 행위자 서비스입니다. 이 예제는 hello ActorProxy 사용된 tooactivate 수 및 행위자 인스턴스와 통신할 수 있는 합니다. 사용자의 서비스와 함께 배포되지 않습니다.

### <a name="hello-application"></a>hello 응용 프로그램
마지막으로, 응용 프로그램 패키지 hello hello 행위자 서비스 및 기타 서비스 배포에 대 한 향후 hello에 추가할 수도 있습니다. Hello 포함 되어 *ApplicationManifest.xml* 및 hello 행위자 서비스 패키지에 대 한 자리 표시자입니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

hello Yeoman 스 캐 폴딩 gradle 스크립트 toobuild hello 응용 프로그램 및 bash 스크립트 toodeploy 및 응용 프로그램 제거를 포함 합니다. toodeploy hello 응용 프로그램, gradle 하는 첫 번째 빌드 hello 적용:

```bash
$ gradle
```

그러면 Service Fabric CLI 도구를 사용하여 배포할 수 있는 Service Fabric 응용 프로그램 패키지를 생성합니다.

### <a name="deploy-service-fabric-cli"></a>Service Fabric CLI 배포

hello install.sh 스크립트 hello 필요한 서비스 패브릭 CLI (sfctl) 명령을 toodeploy hello 응용 프로그램 패키지를 포함합니다.
Hello install.sh 스크립트 toodeploy hello 응용 프로그램을 실행 합니다.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>다음 단계

* [Service Fabric CLI 시작](service-fabric-cli.md)
