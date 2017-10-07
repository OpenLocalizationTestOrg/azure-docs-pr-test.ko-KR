---
title: "aaaCreate 프로그램 첫 번째 행위자 기반 Azure 마이크로 서비스 C# | Microsoft Docs"
description: "이 자습서의 만들기, 디버깅 및 서비스 패브릭 Reliable Actors를 사용 하 여 간단한 행위자 기반 서비스를 배포 hello 단계를 안내 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
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

이 문서는 Azure 서비스 패브릭 Reliable Actors의 hello 기본 사항에 설명 하 고 만들기, 디버깅, 및 Visual Studio에서 간단한 Reliable Actor 응용 프로그램을 배포 하는 과정을 보여 줍니다.

## <a name="installation-and-setup"></a>설치 및 설정
시작 하기 전에 hello 서비스 패브릭 개발 환경에서 컴퓨터를 설정 했는지 확인 합니다.
Tooset 해야 할 경우 자세한 지침에 참조 설정, [어떻게 hello 개발 환경을 tooset](service-fabric-get-started.md)합니다.

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

## <a name="create-a-new-project-in-visual-studio"></a>Visual Studio에서 새 프로젝트 만들기
관리자 권한으로 Visual Studio 2015 또는 Visual Studio 2017을 시작하고 새로운 Service Fabric 응용 프로그램 프로젝트를 만듭니다.

![Visual Studio용 서비스 패브릭 도구 - 새 프로젝트][1]

Hello 다음 대화 상자에서 원하는 toocreate hello 형식의 프로젝트 선택할 수 있습니다.

![서비스 패브릭 프로젝트 템플릿][5]

Hello HelloWorld 프로젝트에 대 한 hello 서비스 패브릭 Reliable Actors 서비스를 사용 하겠습니다.

Hello 솔루션을 만든 후 다음 구조 hello를 표시 되어야 합니다.

![서비스 패브릭 프로젝트 구조][2]

## <a name="reliable-actors-basic-building-blocks"></a>신뢰할 수 있는 행위자 기본 구성 요소
일반적으로 Reliable Actors 솔루션은 다음 3개 프로젝트로 구성됩니다.

* **hello 응용 프로그램 프로젝트 (MyActorApplication)**합니다. 이 hello 프로젝트의 모든 배포에 대 한 함께 hello 서비스 패키지입니다. Hello 포함 되어 *ApplicationManifest.xml* 및 hello 응용 프로그램을 관리 하기 위한 PowerShell 스크립트입니다.
* **hello 인터페이스 프로젝트 (MyActor.Interfaces)**합니다. 이것이 hello 작업자에 대해 hello 인터페이스 정의 포함 하는 hello 프로젝트입니다. Hello MyActor.Interfaces 프로젝트 hello 솔루션의 hello 행위자로 사용할 hello 인터페이스를 정의할 수 있습니다. 하지만 행위자 인터페이스 hello 인터페이스 hello 행위자 구현과 hello 행위자를 호출 하 의미 toodefine 일반적으로 hello 클라이언트에서 공유 하는 hello 행위자 계약을 정의 모든 이름의 모든 프로젝트에 정의할 수 있는 어셈블리에 hello 행위자 구현에서 구분 하 고 여러 다른 프로젝트에서 공유할 수 있습니다.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **hello 행위자 서비스 프로젝트 (MyActor)**합니다. Hello 사용 toodefine hello 서비스 패브릭 있는 프로젝트 서비스가 진행 중인 toohost hello 작업자입니다. Hello 행위자의 hello 구현을 포함합니다. 행위자 구현을 hello 기본 형식에서 파생 되는 클래스는 `Actor` 구현 hello hello MyActor.Interfaces 프로젝트에 정의 된 인터페이스 및 합니다. 행위자 클래스를 허용 하는 생성자를 구현 해야는 `ActorService` 인스턴스 및 `ActorId` 전달 toohello 기본 `Actor` 클래스입니다. 그러면 플랫폼 종속성의 생성자 종속성 주입이 허용됩니다.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

hello 행위자 서비스는 hello 서비스 패브릭 런타임에서 서비스 유형으로 등록 되어야 합니다. 주문 hello 행위자 서비스 toorun 행위자 인스턴스, 행위자 형식 hello 행위자 서비스에도 등록 해야 합니다. hello `ActorRuntime` 등록 메서드는 행위자를 위한이 작업을 수행 합니다.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Visual Studio에서 새 프로젝트에서 시작 하는 경우 행위자 정의 하나만 있으면 hello 등록 Visual Studio에서 생성 하는 hello 코드에서 기본적으로 포함 됩니다. Hello 서비스에서 다른 행위자를 정의 하는 경우 사용 하 여 tooadd hello 행위자 등록 필요:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> hello 서비스 패브릭 행위자 런타임에서 내보내는 일부 [이벤트 및 성능 카운터에 대 한 관련 tooactor 메서드에서](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters)합니다. 진단 및 성능 모니터링에 유용합니다.
> 
> 

## <a name="debugging"></a>디버그
Visual Studio에 대 한 hello 서비스 패브릭 도구는 로컬 컴퓨터에서 디버깅을 지원 합니다. F5 키 hello를 적중 하 여 디버깅 세션을 시작할 수 있습니다. Visual Studio는 (필요한 경우) 패키지를 작성합니다. 또한 hello 로컬 서비스 패브릭 클러스터에 hello 응용 프로그램을 배포 하 고 hello 디버거 연결 합니다.

Hello 배포 과정에서 hello hello 진행 상황을 확인할 수 있습니다 **출력** 창.

![서비스 패브릭 디버깅 출력 창][3]

## <a name="next-steps"></a>다음 단계
에 대 한 자세한 내용은 [Reliable Actors hello 서비스 패브릭 플랫폼을 사용 하는 방법을](service-fabric-reliable-actors-platform.md)합니다.

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
