---
title: "aaaCreate C#에서 첫 번째 서비스 패브릭 응용 프로그램 | Microsoft Docs"
description: "Microsoft Azure 서비스 패브릭 응용 프로그램에 상태 비저장 및 상태 저장 서비스 toocreating를 소개 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
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

Azure 서비스 패브릭 응용 프로그램에는 코드를 실행하는 하나 이상의 서비스가 포함되어 있습니다. 이 가이드에서는 toocreate 사용 상태 비저장 및 상태 저장 서비스 패브릭 응용 프로그램 [신뢰할 수 있는 서비스](service-fabric-reliable-services-introduction.md)합니다.  이 Microsoft Virtual Academy 비디오 또한를 보면 어떻게 toocreate 상태 비저장 신뢰할 수 있는 서비스:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>기본 개념
만 신뢰할 수 있는 서비스 시작 tooget toounderstand 몇 가지 기본 개념을 필요 합니다.

* **서비스 유형**: 서비스 구현입니다. 확장 작성 hello 클래스에 의해 정의 된 `StatelessService` 및 다른 코드 또는 종속성 이름 및 버전 번호와 함께 본 사용 합니다.
* **명명 된 서비스 인스턴스**: toorun 사용자가 서비스를 만들면 서비스 유형의 명명 된 인스턴스 훨씬 클래스 형식의 개체 인스턴스를 만들고 있습니다. 서비스 인스턴스는 hello 형식의 hello를 사용 하 여 URI에서 이름이 "패브릭: /"와 같은 구성표 "패브릭: / MyApp/MyService"입니다.
* **서비스 호스트**: hello 명명 된 서비스 인스턴스를 만들면 필요 toorun 호스트 프로세스 내부에 있습니다. hello 서비스 호스트는 서비스의 인스턴스를 실행할 수 있는 프로세스 뿐입니다.
* **서비스 등록**: 등록은 모든 항목을 함께 모읍니다. hello 서비스 형식을 등록 해야 서비스 패브릭 hello로 서비스의 런타임 tooallow 서비스 패브릭 toocreate의 인스턴스를 호스트 하기 toorun 합니다.  

## <a name="create-a-stateless-service"></a>상태 비저장 서비스 만들기
상태 비저장 서비스는 hello norm 클라우드 응용 프로그램에서 현재 사용 중인 서비스의 유형입니다. Hello 서비스 자체는 toobe 안정적으로 저장 또는 항상 사용 가능 해야 하는 데이터를 포함 하므로 상태 비저장 간주 됩니다. 상태 비저장 서비스의 인스턴스가 종료되면 모든 내부 상태가 손실됩니다. 이런이 종류의 서비스 상태 Azure 테이블 또는 SQL 데이터베이스 같은 외부 저장소에 지속형된 tooan 해야 항상 사용 가능 하 고 신뢰할 수 있는 toobe 수행한 것입니다.

관리자 권한으로 Visual Studio 2015 또는 Visual Studio 2017을 시작하고 *HelloWorld*라는 새로운 서비스 패브릭 응용 프로그램 프로젝트를 만듭니다.

![Hello 새 프로젝트 대화 상자 toocreate 새 서비스 패브릭 응용 프로그램을 사용 하 여](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

그런 다음 *HelloWorldStateless*라는 상태 비저장 서비스 프로젝트를 만듭니다.

![Hello 두 번째 대화 상자에는 상태 비저장 서비스 프로젝트 만들기](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

이제 솔루션에는 2개의 프로젝트가 있습니다.

* *HelloWorld*. 이 hello *응용 프로그램* 프로젝트를 포함 하 여 *서비스*합니다. 또한 응용 프로그램으로 hello 응용 프로그램 toodeploy 데 도움이 되는 PowerShell 스크립트의 수를 설명 하는 hello 응용 프로그램 매니페스트를 포함 합니다.
* *HelloWorldStateless*. 이것이 hello 서비스 프로젝트입니다. Hello 상태 비저장 서비스 구현을 포함합니다.

## <a name="implement-hello-service"></a>Hello 서비스 구현
열기 hello **HelloWorldStateless.cs** hello 서비스 프로젝트의 파일입니다. 서비스 패브릭에서 서비스는 모든 비즈니스 논리를 실행할 수 있습니다. hello 서비스 API는 코드에 대 한 두 진입점을 제공 합니다.

* 장기 실행 계산 워크로드 등 모든 워크로드의 실행을 시작할 수 있는 *RunAsync*라는 개방형 진입점 메서드.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* ASP.NET Core와 같이 원하는 통신 스택을 연결할 수 있는 통신 진입점. 사용자 및 다른 서비스에서 요청을 수신하도록 시작할 수 있습니다.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

이 자습서에 대해 살펴볼 것 hello `RunAsync()` 진입점 메서드. 바로 코드를 실행하기 시작할 수 있습니다.
hello 프로젝트 템플릿은 포함의 예제 구현은 `RunAsync()` 롤링 수를 증가 하는 합니다.

> [!NOTE]
> 통신와 toowork 스택 하는 방법에 대 한 세부 정보를 참조 하십시오. [OWIN 자체 호스트 된 서비스 패브릭 웹 API 서비스](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

hello 플랫폼 서비스의 인스턴스가 tooexecute 배치 하 고 준비 하는 경우이 메서드를 호출 합니다. 상태 비저장 서비스의 경우 단순히 hello 서비스 인스턴스를 열 때 것입니다. 서비스 인스턴스가 닫혀 toobe 해야 할 때 취소 토큰에서 toocoordinate를 제공 됩니다. 서비스 패브릭 서비스 인스턴스의이 열기/닫기 주기 전체적으로 hello 서비스 hello 기간 동안 여러 번 발생할 수 있습니다. 다음을 포함하여 여러 가지 이유로 발생할 수 있습니다.

* hello 시스템 리소스 균형 조정에 대 한 서비스 인스턴스를 이동 합니다.
* 오류는 코드에서 발생합니다.
* hello 응용 프로그램 또는 시스템 업그레이드 됩니다.
* 가동 중단을 경험 하는 hello 기본 하드웨어입니다.

이 오케스트레이션 hello 시스템 tookeep에서 관리 하는 항상 사용 가능 하 고 적절히 균형 있는 서비스입니다.

`RunAsync()`는 동기적으로 차단하지 않아야 합니다. RunAsync 구현 작업을 반환 하거나 모든 장기 실행 또는 차단 작업이 tooallow hello 런타임 toocontinue에 await 해야 합니다. Hello에 대 한 참고 `while(true)` hello 이전 예제에서는 작업 반환 루프 `await Task.Delay()` 사용 됩니다. 워크로드가 동기적으로 차단해야 하는 경우 `RunAsync` 구현에서 `Task.Run()`을 사용하여 새 작업을 예약해야 합니다.

작업의 취소는 취소 토큰을 제공 하는 hello 조정 되는 협조적 노력 합니다. hello 시스템에서 성공적으로 완료, 취소 또는 오류) (에서 작업 tooend 기다릴 이동 합니다. 중요 한 toohonor hello 취소 토큰, 완료, 작업 및 종료는 `RunAsync()` hello 시스템 취소를 요청 하는 경우 가능한 한 신속 하 게 합니다.

이 상태 비저장 서비스 예에서 hello count 지역 변수에 저장 됩니다. 하지만 저장 된 hello 값을 해당 서비스 인스턴스의 hello 현재 주기 위해서만 존재 상태 비저장 서비스 이기 때문에 있습니다. Hello 서비스 이동 하거나 다시 시작, hello 값이 손실 됩니다.

## <a name="create-a-stateful-service"></a>상태 저장 서비스 만들기
서비스 패브릭은 상태 저장하는 서비스의 새로운 종류를 도입합니다. 상태 저장 서비스를 사용 하는 hello 코드와 같은 위치에 자체 hello 서비스 내에서 안정적으로 상태를 유지할 수 있습니다. 상태는 항상 사용 가능 서비스 패브릭에서 hello 필요 toopersist 상태 tooan 외부 저장소 없이 합니다.

카운터 값에서 사용 가능 하 고 영구 상태 비저장 toohighly tooconvert hello 서비스 이동 하거나 다시 시작 되 면 경우에 상태 저장 서비스가 필요 합니다.

동일한 hello *HelloWorld* 응용 프로그램을 선택 하 고 hello 응용 프로그램 프로젝트의 hello 서비스 참조를 마우스 오른쪽 단추로 클릭 하 여 새 서비스를 추가할 수 있습니다 **추가-새 서비스 패브릭 서비스 >**합니다.

![서비스 tooyour 서비스 패브릭 응용 프로그램 추가](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

**상태 저장 서비스** 를 선택하고 *HelloWorldStateful*이라는 이름을 지정합니다. **확인**을 클릭합니다.

![Hello 새 프로젝트 대화 상자 toocreate 새 서비스 패브릭 상태 저장 서비스를 사용 하 여](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

응용 프로그램을 두 가지 서비스를 만들었습니다: 상태 비저장 서비스 hello *HelloWorldStateless* 및 상태 저장 서비스의 hello *HelloWorldStateful*합니다.

상태 저장 서비스는 hello 동일한 시작 지점으로 상태 비저장 서비스입니다. hello 중요 한 차이점은의 가용성을 hello는 *상태 공급자* 안정적으로 상태를 저장할 수 있는 합니다. 서비스 패브릭 호출 상태 공급자 구현에는 [신뢰할 수 있는 컬렉션](service-fabric-reliable-services-reliable-collections.md), 신뢰할 수 있는 상태 관리자 hello 통해 복제 된 데이터 구조를 만들 수 있습니다. 상태 저장 Reliable Service는 기본적으로 이 상태 제공자를 사용합니다.

열기 **HelloWorldStateful.cs** 에 *HelloWorldStateful*, hello RunAsync 메서드 뒤에 포함 된:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()` 은 상태 저장 및 상태 비저장 서비스에서 비슷하게 작동합니다. 그러나 상태 저장 서비스의 hello 플랫폼 추가 작업을 수행 사용자 대신 실행 되기 전에 `RunAsync()`합니다. 이 작업에서 해당 hello 신뢰할 수 있는 상태 관리자 보장를 포함할 수 있으며 신뢰할 수 있는 컬렉션은 준비 toouse 합니다.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>신뢰할 수 있는 컬렉션 및 hello 신뢰할 수 있는 상태 관리자
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) tooreliably hello 서비스에서 상태 저장을 사용할 수 있는 사전 구현입니다. 서비스 패브릭 및 신뢰할 수 있는 컬렉션을 사용 하 여 외부 영구 저장소에 대 한 hello 필요 없이 서비스에 직접 데이터를 저장할 수 있습니다. 신뢰할 수 있는 컬렉션은 데이터를 항상 사용할 수 있게 만듭니다. 서비스 패브릭은 서비스의 여러 *복제본* 을 만들고 관리하여 이를 달성합니다. 또한 해당 복제본 및 해당 상태 전환 관리의 트래버스하여 hello 복잡성을 추상화 하는 API를 제공 합니다.

신뢰할 수 있는 컬렉션은 사용자 지정 형식을 포함하여 모든 .NET 유형을 저장할 수 있습니다. 단, 몇 가지 주의 사항이 있습니다.

* 서비스 패브릭에서 항상 사용 가능한 상태는 *복제* 상태 노드 및 신뢰할 수 있는 컬렉션에서 각 복제본에서 데이터 toolocal 디스크를 저장 합니다. 즉, 신뢰할 수 있는 컬렉션에 저장된 모든 항목이 *직렬화 가능*상태가 됩니다. 신뢰할 수 있는 수집은 기본적으로 사용 하 여 [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) 직렬화를 따라서 것이 중요 한 toomake 프로그램 형식이 되는지 [hello 데이터 계약 Serializer에서 지 원하는](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) hello 기본값을 사용 하는 경우 직렬 변환기입니다.
* 신뢰할 수 있는 컬렉션의 트랜잭션을 커밋하면 고가용성을 위해 개체가 복제됩니다. 신뢰할 수 있는 컬렉션에 저장된 개체는 서비스의 로컬 메모리에 유지됩니다. 즉, 로컬 참조 방식 toohello 개체를 사용 해야 합니다.
  
   트랜잭션에서 hello 신뢰할 수 있는 컬렉션에서 업데이트 작업을 수행 하지 않고 해당 개체의 로컬 인스턴스를 변경 하지 마십시오 유용 합니다. 개체의 변경 내용을 toolocal 인스턴스가 자동으로 복제 되지 않기 때문입니다. 다시 hello 사전에 다시 hello 개체를 삽입 하거나 hello 중 하나를 사용 해야 *업데이트* hello 사전에 대 한 메서드.

hello 신뢰할 수 있는 상태 관리자에서를 신뢰할 수 있는 컬렉션을 관리 합니다. 요청할 수 있습니다 단순히 hello 신뢰할 수 있는 상태 관리자는 신뢰할 수 있는 컬렉션에 대 한 이름으로 언제 든 지 고 모든 위치에서 서비스에. hello 신뢰할 수 있는 상태 관리자를 사용 하면 참조를 다시 가져오십시오. 저장 하는 참조 tooreliable 컬렉션 인스턴스 클래스 멤버 변수 또는 속성 하지 않는 것이 좋습니다. 특별 한 주의 해야 tooensure hello 참조 설정 된 hello 서비스 수명 주기에서 항상 tooan 인스턴스. hello 신뢰할 수 있는 상태 관리자를이 작업을 처리 하 고 반복 방문을 위해 최적화 됩니다.

### <a name="transactional-and-asynchronous-operations"></a>트랜잭션 및 비동기 작업
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

신뢰할 수 있는 컬렉션에 있는지 다양 한 hello 이와 동일한 작업을 하는 해당 `System.Collections.Generic` 및 `System.Collections.Concurrent` 함수와 제외 하 고 LINQ를 합니다. 신뢰할 수 있는 컬렉션의 작업은 비동기적입니다. 신뢰할 수 있는 컬렉션을 사용한 쓰기 작업 I/O 작업 tooreplicate 수행 및 데이터 toodisk 유지 때문입니다.

신뢰할 수 있는 컬렉션 작업은 *트랜잭션*이므로 여러 신뢰할 수 있는 컬렉션 및 작업에서 상태를 일관성 있게 유지할 수 있습니다. 예를 들어 신뢰할 수 있는 큐에서 작업 항목 큐에서 제거 하 고,에서 작업을 수행 하 고, 단일 트랜잭션 내에서 모든 신뢰할 수 있는 사전에 hello 결과 저장할 수 있습니다. 이 원자성 작업으로 처리 및 hello 전체 작업이 성공 합니다 중 하나 또는 전체 작업 hello 롤백합니다 보장 합니다. Hello 항목 큐에서 제거 후 오류가 발생 하지만 hello 결과 저장 하기 전에 hello 전체 트랜잭션이 롤백될 및 hello 항목 처리에 대 한 hello 큐에 남아 있습니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행
이제 toohello 반환 *HelloWorld* 응용 프로그램입니다. 이제 서비스를 빌드하고 배포할 수 있습니다. 누를 때 **F5**, 응용 프로그램에 작성 되 고 배포 된 tooyour 로컬 클러스터 됩니다.

Hello 서비스 실행 시작 후에 생성 된 hello 이벤트 추적에 대 한 ETW (Windows) 이벤트를 볼 수 있습니다는 **진단 이벤트** 창. Hello 상태 비저장 서비스와 hello hello 응용 프로그램에서 상태 저장 서비스에서 표시 하는 hello 이벤트는 note 합니다. Hello를 클릭 하 여 hello 스트림을 두면 **일시 중지** 단추입니다. 그런 다음 해당 메시지를 확장 하 여 hello 메시지 정보를 검사할 수 있습니다.

> [!NOTE]
> Hello 응용 프로그램을 실행 하기 전에 실행 하는 로컬 개발 클러스터 했는지 확인 합니다. 체크 아웃 hello [시작 가이드](service-fabric-get-started.md) 로컬 환경 설정에 대 한 내용은 합니다.
> 
> 

![Visual Studio에서 진단 이벤트 보기](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>다음 단계
[Visual Studio에서 서비스 패브릭 응용 프로그램 디버깅](service-fabric-debugging-your-application.md)

[시작: OWIN 자체 호스팅을 사용하는 서비스 패브릭 Web API 서비스](service-fabric-reliable-services-communication-webapi.md)

[신뢰할 수 있는 컬렉션에 대한 자세한 정보](service-fabric-reliable-services-reliable-collections.md)

[응용 프로그램 배포](service-fabric-deploy-remove-applications.md)

[응용 프로그램 업그레이드](service-fabric-application-upgrade.md)

[신뢰할 수 있는 서비스에 대한 개발자 참조](https://msdn.microsoft.com/library/azure/dn706529.aspx)

