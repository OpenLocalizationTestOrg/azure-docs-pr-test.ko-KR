---
title: "ASP.NET Core를 사용 하 여 Azure 서비스 패브릭 응용 프로그램에 대 한 웹 프런트 엔드 aaaCreate | Microsoft Docs"
description: "ASP.NET Core 프로젝트와 원격 서비스를 통해 서비스 통신을 사용 하 여 서비스 패브릭 응용 프로그램 toohello 웹을 노출 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>ASP.NET Core를 사용하여 응용 프로그램에 대한 웹 서비스 프런트 엔드 구축
기본적으로 Azure 서비스 패브릭 서비스는 공용 인터페이스 toohello 웹을 제공 하지 않습니다. tooexpose toocreate 웹 tooact를 진입점으로 프로젝트를 마우스 다음 없어 tooyour에서 통신 해야 응용 프로그램의 기능 tooHTTP 클라이언트 개별 서비스입니다.

이 자습서에서는 가져갈부터 hello에 [Visual Studio에서 응용 프로그램 처음 만들기](service-fabric-create-your-first-application-in-visual-studio.md) 자습서 hello 카운터 상태 저장 서비스 앞에 ASP.NET Core 웹 서비스를 추가 합니다. 아직 수행하지 않은 경우 다시 돌아가서 먼저 해당 자습서를 단계별로 실행해야 합니다.

## <a name="set-up-your-environment-for-aspnet-core"></a>ASP.NET Core에 대한 환경 설정

이 자습서와 함께 Visual Studio 2017 toofollow가 필요합니다. 모든 버전에서 수행합니다. 

 - [Visual Studio 2017 설치](https://www.visualstudio.com/)

toodevelop ASP.NET Core 서비스 패브릭 응용 프로그램 설치 작업을 수행 하는 hello가 있어야 합니다.
 - **Azure 개발**(*웹 및 클라우드* 아래)
 - **ASP.NET 및 웹 개발**(*웹 및 클라우드* 아래)
 - **.NET Core 플랫폼 간 개발**(*다른 도구 집합* 아래)

>[!Note] 
>hello Visual Studio 2015 용.NET Core 도구는 더 이상 업데이트 toohave 필요한 Visual Studio 2015를 아직 사용 중인 경우 [.NET Core VS 2015 Tooling 미리 보기 2](https://www.microsoft.com/net/download/core) 설치 합니다.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>ASP.NET Core 서비스 tooyour 응용 프로그램 추가
ASP.NET Core는 플랫폼 간 경량 웹 개발 프레임 워크 toocreate 최신 웹 UI를 사용할 수 있으며 웹 Api입니다. 

ASP.NET Web API 프로젝트 tooour 기존 응용 프로그램을 추가 해 보겠습니다.

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **서비스** 내 응용 프로그램 프로젝트 hello 및 선택 **추가 > 새 서비스 패브릭 서비스**합니다.
   
    ![새 서비스 tooan 기존 응용 프로그램 추가][vs-add-new-service]
2. Hello에 **서비스를 만들** 페이지에서 선택 **ASP.NET Core** 에 이름을 지정 합니다.
   
    ![Hello 새 서비스 대화 상자에서 ASP.NET 웹 서비스를 선택합니다.][vs-new-service-dialog]

3. hello 다음 페이지는 ASP.NET Core 집합이 프로젝트 템플릿을 제공합니다. 동일한 hello는 이러한 참고를 만들면 서비스 패브릭 응용 프로그램, 외부 프로그램 ASP.NET Core 프로젝트 적은 양의 추가 코드 tooregister 볼 수는 선택 사항 hello 서비스 hello 서비스 패브릭 런타임 사용 합니다. 이 자습서에서는 **Web API**를 선택합니다. 적용할 수 있습니다는 전체 웹 응용 프로그램에 동일한 개념 toobuilding hello 합니다.
   
    ![ASP.NET 프로젝트 유형 선택][vs-new-aspnet-project-dialog]
   
    Web API 프로젝트를 만들었으면 응용 프로그램에 두 개의 서비스가 있을 것입니다. 정확 하 게 hello에서 더 많은 서비스를 추가할 수 toobuild 응용 프로그램을 계속 하면서 동일한 방식으로 합니다. 각 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행
tooget 하겠습니다, 보겠습니다의 의미를 살펴보면 ASP.NET Core 웹 API 템플릿을 hello hello 기본 동작을 제공 하는 내용이 및 hello 새 응용 프로그램 배포.

1. Visual Studio toodebug hello 응용 프로그램에서 F5 키를 누릅니다.
2. 배포가 완료 되 면 Visual Studio는 브라우저 toohello 루트 hello ASP.NET Web API 서비스의 시작 됩니다. hello ASP.NET Core 웹 API 템플릿을 404 오류 hello 브라우저에 표시 되어야 하므로 hello 루트에 대 한 기본 동작을 제공 하지 않습니다.
3. 추가 `/api/values` hello 브라우저에서 toohello 위치입니다. 그러면 호출 hello `Get` hello Web API 템플릿에 ValuesController hello에 메서드. Hello 템플릿--두 문자열을 포함 하는 JSON 배열에서 제공 하는 hello 기본 응답을 반환 합니다.
   
    ![ASP.NET Core Web API 템플릿에서 반환되는 기본값][browser-aspnet-template-values]
   
    Hello 자습서의 hello 결과적으로 기본 문자열이이 페이지 hello hello 대신 상태 저장 서비스에서 가장 최근의 카운터 값 표시 됩니다.

## <a name="connect-hello-services"></a>Hello 서비스 연결
서비스 패브릭은 신뢰할 수 있는 서비스와 유연하게 통신할 수 있는 방법을 제공합니다. 단일 응용 프로그램 내에 TCP를 통해 액세스할 수 있는 서비스, HTTP REST API를 통해 액세스할 수 있는 다른 서비스 및 웹 소켓을 통해 액세스할 수 있는 다른 서비스가 있을 수 있습니다. 참조에 대 한 배경 사용할 수 있는 hello 옵션 및 hello 보완, [서비스와 통신](service-fabric-connect-and-communicate-with-services.md)합니다. 이 자습서에서는 사용 하 여 [서비스 패브릭 원격 서비스](service-fabric-reliable-services-communication-remoting.md)hello SDK에서에서 제공 합니다.

원격 서비스 접근 방식 (원격 프로시저 호출 또는 Rpc에서 모델링) hello 인터페이스 tooact hello hello 서비스에 대 한 공용 계약으로 정의 합니다. 그런 다음 hello 서비스와 상호 작용 하기 위한 해당 인터페이스 toogenerate 프록시 클래스를 사용 합니다.

### <a name="create-hello-remoting-interface"></a>Hello 원격 인터페이스 만들기
상태 저장 서비스의 hello와이 case hello ASP.NET Core 웹 프로젝트의에서 다른 서비스 간의 hello 계약으로 hello 인터페이스 tooact를 만들어 보겠습니다. 이 인터페이스는 자체 클래스 라이브러리 프로젝트에 만들겠습니다 하므로 toomake RPC 호출을 사용 하는 모든 서비스에서 공유 되어야 합니다.

1. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **브라우저에서 해당 위치에** > **새 프로젝트**해야 합니다.

2. Hello 선택 **Visual C#** 왼쪽 탐색 창 및 선택 hello hello에 항목 **클래스 라이브러리** 템플릿. 해당 hello.NET Framework 버전 너무 설정 되어 있는지 확인**4.5.2**합니다.
   
    ![상태 저장 서비스에 대한 인터페이스 프로젝트 만들기][vs-add-class-library-project]

3. Hello 설치 **Microsoft.ServiceFabric.Services.Remoting** NuGet 패키지 합니다. 검색할 **Microsoft.ServiceFabric.Services.Remoting** hello NuGet에서에서 관리자를 패키지 하 고 원격 서비스를 사용 하는 hello 솔루션의 모든 프로젝트에 대 한 설치 포함 하 여:
   - hello 서비스 인터페이스를 포함 하는 hello 클래스 라이브러리 프로젝트
   - hello 상태 저장 서비스 프로젝트
   - hello ASP.NET Core 웹 서비스 프로젝트
   
    ![Hello 서비스 NuGet 패키지를 추가합니다.][vs-services-nuget-package]

4. Hello 클래스 라이브러리의 단일 메서드와 인터페이스를 만듭니다 `GetCountAsync`에서 hello 인터페이스를 확장 하 고 `Microsoft.ServiceFabric.Services.Remoting.IService`합니다. hello 원격 인터페이스는 원격 서비스 인터페이스는이 인터페이스 tooindicate에서 파생 되어야 합니다.
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>상태 저장 서비스의 hello 인터페이스를 구현 합니다.
이제 hello 인터페이스를 정의한 필요한 tooimplement hello 상태 저장 서비스에 있습니다.

1. 상태 저장 서비스에 hello 인터페이스를 포함 하는 참조 toohello 클래스 라이브러리 프로젝트를 추가 합니다.
   
    ![상태 저장 서비스의 hello에 참조 toohello 클래스 라이브러리 프로젝트를 추가합니다.][vs-add-class-library-reference]
2. Hello 클래스에서 상속 되는 위치를 찾을 `StatefulService`와 같은 `MyStatefulService`, 고 tooimplement hello 확장 `ICounter` 인터페이스입니다.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. 이제 hello에 정의 된 hello 단일 메서드를 구현 `ICounter` 인터페이스 `GetCountAsync`합니다.
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>서비스 remoting 수신기를 사용 하 여 hello 상태 저장 서비스를 노출 합니다.
Hello로 `ICounter` 인터페이스 구현 hello 마지막 단계는 tooopen hello 원격 서비스 통신 채널입니다. 상태 저장 서비스의 경우 서비스 패브릭은 `CreateServiceReplicaListeners`라는 재정의 가능한 메서드를 제공합니다. 이 방법으로 통신 서비스에 대 한 tooenable 되도록의 hello 형식을 기반으로 하나 이상의 통신 수신기를 지정할 수 있습니다.

> [!NOTE]
> 통신 채널 toostateless 서비스를 열기 위한 동등한 방법이 hello 라고 `CreateServiceInstanceListeners`합니다.

이 경우 기존 hello 대체 하겠습니다 `CreateServiceReplicaListeners` 메서드의 인스턴스를 제공 하 고 `ServiceRemotingListener`를 통해 클라이언트에서 호출 되는 RPC 끝점 만듦 `ServiceProxy`합니다.  

hello `CreateServiceRemotingListener` hello에 대 한 확장 메서드 `IService` 인터페이스 있습니다 tooeasily 만들기는 `ServiceRemotingListener` 모든 기본 설정을 사용 합니다. toouse이 확장 메서드를 hello 해야 `Microsoft.ServiceFabric.Services.Remoting.Runtime` 가져온 네임 스페이스입니다. 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Hello ServiceProxy 클래스 toointeract hello 서비스와 함께 사용
상태 저장 서비스는 RPC를 통해 이제 다른 서비스에서 준비 tooreceive 트래픽입니다. 따라서 모든 작업을 계속은 hello ASP.NET 웹 서비스에서에서 된 hello 코드 toocommunicate를 추가 합니다.

1. ASP.NET 프로젝트에서 hello를 포함 하는 참조 toohello 클래스 라이브러리 추가 `ICounter` 인터페이스입니다.

2. Hello 추가한 이전 **Microsoft.ServiceFabric.Services.Remoting** NuGet 패키지 toohello ASP.NET 프로젝트. 이 패키지는 hello 제공 `ServiceProxy` 사용할 수 있는 클래스 toomake RPC toohello 상태 저장 서비스를 호출 합니다. Hello ASP.NET Core 웹 서비스 프로젝트에서에서이 NuGet 패키지가 설치 되어 있는지 확인 합니다.

4. Hello에 **컨트롤러** 폴더, 열기 hello `ValuesController` 클래스입니다. 해당 hello 참고 `Get` 메서드는 현재 방금 "value1" 및 "value2"-hello 브라우저 앞에서 살펴본에 일치 하는 하드 코드 된 문자열 배열을 반환 합니다. 이 구현을 코드 다음 hello로 바꿉니다.
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    hello 첫 번째 코드 줄은 hello 키 하나입니다. 두 가지 정보를 tooprovide 해야 toocreate hello ICounter 프록시 toohello 상태 저장 서비스를: hello 서비스의 파티션 ID와 hello 이름입니다.
   
    고객 ID 또는 우편 번호와 같은 정의 하는 키에 따라 상태로 다른 버킷으로 분할 하 여 분할 tooscale 상태 저장 서비스를 사용할 수 있습니다. Trivial 응용 프로그램에서는 상태 저장 서비스의 hello은 하나만 포함 한 파티션에만 하므로 hello 키 문제가 되지 않습니다. 사용자가 제공한 아무 키나 toohello 일으킵니다 같은 파티션에 합니다. 서비스를 분할에 대 한 더 toolearn 참조 [어떻게 toopartition 서비스 패브릭 신뢰할 수 있는 서비스](service-fabric-concepts-partitioning.md)합니다.
   
    hello 서비스 이름은 hello 양식 패브릭의 URI입니다. /&lt;i o n _&gt;/&lt;service_name&gt;합니다.
   
    이러한 두 가지 정보를 서비스 패브릭 hello 컴퓨터에 요청을 보내야 하는 고유 하 게 확인할 수 있습니다. hello `ServiceProxy` 클래스도 원활 하 게 처리 프로그램이 hello 상태 저장 서비스의 파티션을 호스팅하는 hello 컴퓨터에서 오류가 발생 하 고 다른 컴퓨터에는 승격 된 tootake 있어야 합니다. hello 경우 그 자리입니다. 이 추상화 쓰기를 사용 하면 더 간단 다른 서비스와 클라이언트 코드 toodeal hello 합니다.
   
    Hello hello 프록시, 있으면 호출 하면 됩니다 `GetCountAsync` 메서드 해당 결과 반환 합니다.

5. F5 키를 눌러 다시 toorun hello 응용 프로그램을 수정 합니다. 로 이전에 Visual Studio를 자동으로 시작 hello 웹 프로젝트의 hello 브라우저 toohello 루트입니다. Hello "api/값" 경로 추가 하 고 반환 된 hello 현재 카운터 값이 표시 됩니다.
   
    ![hello 브라우저에 표시 되는 hello 상태 저장 카운터 값][browser-aspnet-counter-value]
   
    Hello 브라우저를 새로 고치려면 주기적으로 toosee hello 카운터 값 업데이트입니다.

## <a name="kestrel-and-weblistener"></a>Kestrel 및 WebListener

hello Kestrel, 이라는 기본 ASP.NET Core 웹 서버는 [현재 지원 되지 않는 직접 인터넷 트래픽을 처리 하기 위한](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)합니다. 결과적으로, hello 서비스 패브릭 용 ASP.NET Core 상태 비저장 서비스 템플릿을 사용 하 여 [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) 기본적으로 합니다. 

서비스 패브릭 서비스에 대 한 자세한 정보 Kestrel 및 WebListener toolearn 너무 참조 하십시오[서비스 패브릭 신뢰할 수 있는 서비스에서 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)합니다.

## <a name="connecting-tooa-reliable-actor-service"></a>Tooa Reliable Actor 서비스 연결
이 자습서는 상태 저장 서비스와 통신하는 웹 프런트 엔드를 추가하는 방법에 초점을 맞추고 있습니다. 그러나 매우 유사한 모델 tootalk tooactors를 따를 수 있습니다. 사용자가 Reliable Actor 프로젝트를 만들면 Visual Studio에서 자동으로 인터페이스 프로젝트를 생성합니다. Hello 행위자가 포함 된 웹 프로젝트 toocommunicate hello에서에서 해당 인터페이스 toogenerate 행위자 프록시를 사용할 수 있습니다. hello 통신 채널을 자동으로 제공 됩니다. 해당 tooestablishing toodo은 어느 것에 필요 하지 않은 한 `ServiceRemotingListener` 이 자습서에서는 상태 저장 서비스의 hello 했던 것 처럼 합니다.

## <a name="how-web-services-work-on-your-local-cluster"></a>웹 서비스가 로컬 클러스터에서 작동하는 방식
일반적으로 동일한 서비스 패브릭 응용 프로그램 tooa 다중 컴퓨터 로컬 클러스터에 배포 하는 클러스터 및 예상 대로 작동 하는지 항상 확신 hello 정확 하 게 배포할 수 있습니다. 즉, 로컬 클러스터 된 다섯 개 노드 구성을 단순히 tooa 단일 컴퓨터 축소 됩니다.

그러나 Tooweb 서비스를 때는,는 하나의 키 미묘한 차이입니다. 클러스터와 Azure에서 부하 분산 장치 뒤에 배치를 확인 해야 hello 부하 분산 장치 이후 웹 서비스에 모든 컴퓨터에 배포 되 hello 컴퓨터 간에 트래픽을 단순히 라운드 robins 합니다. Hello 설정 하 여 이렇게 하려면 `InstanceCount` hello 서비스 toohello 특수 값 "-1"에 대 한 합니다.

반면, 웹 서비스를 로컬로 실행할 때 필요한 tooensure hello 서비스의 인스턴스를 하나만 실행 합니다. 충돌에서 수신 하는 hello 동일 하는 여러 프로세스에서 실행, 경로 및 포트. Hello 웹 서비스 인스턴스 수가 너무 하 여 설정 해야 결과적으로, 로컬 배포에 대 한 "1".

서로 다른 환경에 대 한 서로 다른 값 tooconfigure 참조 toolearn [여러 환경에 대 한 응용 프로그램 매개 변수 관리](service-fabric-manage-multiple-environment-app-configuration.md)합니다.

## <a name="next-steps"></a>다음 단계
이제 ASP.NET Core를 통해 웹 프런트가 응용 프로그램에 사용할 수 있게 설정되었으므로 ASP.NET Core가 Service Fabric과 작동하는 방식을 깊이 있게 이해하도록 [Service Fabric Reliable Services의 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)에 대해 자세히 알아보세요.

그런 다음, [서비스와 통신 하는 방법에 대 한 자세한 정보](service-fabric-connect-and-communicate-with-services.md) 일반적 완전 한 tooget 그림 어떻게 서비스의 통신 서비스 패브릭에서 작동 합니다.

서비스 통신의 작동 방식을 잘 알고 있으면 [Azure에서 클러스터를 만들고 응용 프로그램 toohello 클라우드 배포](service-fabric-cluster-creation-via-portal.md)합니다.

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
