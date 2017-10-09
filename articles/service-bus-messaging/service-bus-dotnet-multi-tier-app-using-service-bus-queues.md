---
title: "Azure 서비스 버스를 사용 하 여 다중 계층 응용 프로그램 aaa.NET | Microsoft Docs"
description: "서비스 버스 큐 toocommunicate 계층 사이 사용 하 여 Azure에서 다중 계층 응용 프로그램을 개발 하는 때 도움이 되는.NET 자습서입니다."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>Azure 서비스 버스 큐를 사용하는 .NET 다중 계층 응용 프로그램
## <a name="introduction"></a>소개
Microsoft Azure가 Visual Studio를 사용 하 여 쉽게, hello.NET 용 Azure SDK를 무료 개발 합니다. 이 자습서에서는 hello 단계 toocreate 로컬 환경에서 실행 되는 여러 Azure 리소스를 사용 하는 응용 프로그램입니다.

Hello 다음에 설명 합니다.

* 어떻게 tooenable 단일 Azure 개발 컴퓨터에서 다운로드 및 설치 합니다.
* 어떻게 Azure에 대 한 Visual Studio toodevelop toouse 합니다.
* 어떻게 toocreate 웹 및 작업자 역할을 사용 하 여 Azure에서 다중 계층 응용 프로그램입니다.
* 사이의 toocommunicate 서비스 버스 큐를 사용 하 여 눈금 방법입니다.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

이 자습서에서는 빌드하고 Azure 클라우드 서비스에서 hello 다중 계층 응용 프로그램을 실행 합니다. hello 프런트 엔드는 ASP.NET MVC 웹 역할 및 hello 백 엔드는 서비스 버스 큐를 사용 하는 작업자 역할입니다. 만들 수 있습니다 같은 다중 계층 응용 프로그램 프런트 엔드 hello와 배포 tooan 클라우드 서비스가 아닌 Azure 웹 사이트를 웹 프로젝트로 hello 합니다. Hello 아웃 보십시오 [.NET에서-프레미스/클라우드 하이브리드 응용 프로그램](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) 자습서입니다.

hello 다음 스크린 샷에 표시 완료 hello 응용 프로그램입니다.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>시나리오 개요: 역할 간 통신
hello 프런트 엔드 UI 구성 요소, hello 웹 역할에서 실행을 처리 하는 것에 대 한 주문 toosubmit hello 작업자 역할에서 실행 하는 hello 중간 계층 논리와 상호 작용 해야 합니다. 이 예제에서는 서비스 버스 메시징 hello 계층 간 hello 통신에 사용 합니다.

서비스 버스를 사용 하 여 hello 웹 및 중간 계층 간의 메시징 분리 하는 두 구성 요소. 반대로 hello toodirect 메시징 (즉, TCP 또는 HTTP) 웹 계층 toohello 중간 계층을 직접; 연결 되지 않습니다 대신 안정적으로 hello 중간 계층은 tooconsume 준비 될 때까지 유지 하 고 처리 하는 서비스 버스에 메시지로 작업의 단위 밀어냅니다.

두 엔터티 toosupport 조정 된 메시징을 제공 하는 서비스 버스: 큐 및 항목입니다. 큐와 각 메시지를 보낼 toohello 큐는 단일 수신기에서 사용 됩니다. 항목 게시 된 각 메시지 hello 항목으로 등록 하는 사용 가능한 tooa 구독 수는 hello 게시/구독 패턴을 지원 합니다. 각 구독은 메시지의 고유한 큐를 논리적으로 유지 관리합니다. 메시지 전달 hello 구독 큐 toothose hello 필터와 일치 하는 hello 집합을 제한 하는 필터 규칙으로 구독을 구성할 수도 있습니다. hello 다음 예제에서는 서비스 버스 큐.

![][1]

이 통신 메커니즘은 직접 메시징에 비해 몇 가지 장점이 있습니다.

* **임시 분리** Hello 비동기 메시징 패턴을 사용한 생산자와 소비자가 아니어도 hello에서 온라인으로 동시 합니다. 서비스 버스 사용 중인 파티가 hello를 받을 준비가 될 때까지 메시지를 안정적으로 저장 합니다. 이 통해 연결이 해제 하거나 자발적으로 tooa 구성 요소 크래시 등 기한 또는 유지 관리에 대 한 예를 들어 시스템 전체에 영향을 주지 않고 hello 분산 응용 프로그램 toobe의 hello 구성 요소. 또한 응용 프로그램을 사용 하는 hello은 hello 하루 중 특정 시간 동안 toocome 온라인 하기만 하면 됩니다.
* **부하 평준화** 각 작업 단위에 필요한 hello 처리 시간은 일반적으로 일정는 많은 응용 프로그램에서 시스템 부하 시간이 지남에 따라 다릅니다. 여 메시지 생산자와 소비자는 큐와 최대 부하 대신 평균 부하 tooaccommodate 프로 비전 하는 응용 프로그램 (hello 작업자)만 요구 toobe를 사용해 해당 hello 의미 합니다. 증가 하 고 hello 수신 부하가 변경 됨에 따라 축소 하는 hello 큐의 hello 깊이입니다. 직접 money hello 양의 인프라 필요한 tooservice hello 응용 프로그램 부하를 기준으로 저장 됩니다.
* **부하 분산** 부하가 증가 하면 작업자 프로세스가 더 추가할 수 있습니다 tooread hello 큐에서. Hello 작업자 프로세스 중 하나에만 각 메시지를 처리 합니다. 또한이 끌어오기 기반 부하 분산 사용 하면 hello 작업자 컴퓨터의 최적 사용 작업자 컴퓨터의 관점에서 처리 능력을 다른 경우에 자신의 최대 속도로 메시지를 가져올 때. 이 패턴을 hello 종종 *경쟁 소비자* 패턴입니다.
  
  ![][2]

다음 섹션 hello이이 아키텍처를 구현 하는 hello 코드에 설명 합니다.

## <a name="set-up-hello-development-environment"></a>Hello 개발 환경 설정
Azure 응용 프로그램 개발을 시작 하려면 먼저 hello 도구 가져오고 개발 환경을 설정 합니다.

1. Hello SDK에서에서 hello Azure SDK for.NET 설치 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. Hello에 **.NET** 열 hello 버전 [Visual Studio](http://www.visualstudio.com) 사용 하는 합니다. 이 자습서 사용 하 여 Visual Studio 2015에서에서 hello 실행 하지만 Visual Studio 2017를 사용 합니다.
3. Toorun 라는 메시지가 표시 하거나 저장 hello 설치 관리자를 클릭 **실행**합니다.
4. Hello에 **웹 플랫폼 설치 관리자**, 클릭 **설치** hello 설치를 진행 합니다.
5. Hello 설치가 완료 되 면 할 모든 필요한 toostart toodevelop hello 앱. hello SDK는 Visual Studio에서 Azure 응용 프로그램을 쉽게 개발할 수 있는 도구를 포함 합니다.

## <a name="create-a-namespace"></a>네임스페이스 만들기
다음 단계 hello toocreate 서비스 네임 스페이스 이며 공유 액세스 서명 (SAS) 키를 가져옵니다. 네임스페이스는 서비스 버스를 통해 노출되는 각 응용 프로그램에 대한 응용 프로그램 경계를 제공합니다. 네임 스페이스를 만들 때 SAS 키 hello 시스템에 의해 생성 됩니다. 네임 스페이스와 SAS 키 조합 hello 서비스 버스 tooauthenticate 액세스 tooan 응용 프로그램에 대 한 hello 자격 증명을 제공합니다.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>웹 역할 만들기
이 섹션에서는 응용 프로그램의 프런트 엔드 hello 빌드할 수 있습니다. 먼저, 응용 프로그램을 표시 하는 hello 페이지를 만듭니다.
그 후 항목 tooa 서비스 버스 큐를 전송 하 고 hello 큐에 대 한 상태 정보를 표시 하는 코드를 추가 합니다.

### <a name="create-hello-project"></a>Hello 프로젝트 만들기
1. Visual Studio를 시작 관리자 권한을 사용 하 여,: 마우스 오른쪽 단추 클릭 hello **Visual Studio** 프로그램 아이콘을 클릭 하 고 **관리자 권한으로 실행**합니다. 이 문서의 뒷부분에 설명 된 hello Azure 계산 에뮬레이터는 Visual Studio를 관리자 권한으로 시작할 수 없다는 필요 합니다.
   
   Hello에 Visual Studio에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.
2. **설치된 템플릿**의 **Visual C#**에서 **클라우드**를 클릭한 다음 **Azure Cloud Service**를 클릭합니다. 이름 hello 프로젝트 **MultiTierApp**합니다. 그런 후 **OK**를 클릭합니다.
   
   ![][9]
3. **.NET Framework 4.5** 역할에서 **ASP.NET 웹 역할**을 두 번 클릭합니다.
   
   ![][10]
4. 위로 마우스를 가져가고 **WebRole1** 아래 **Azure 클라우드 서비스 솔루션**hello 연필 아이콘을 클릭 하 고 너무 hello 웹 역할의 이름을 바꿀**FrontendWebRole**합니다. 그런 후 **OK**를 클릭합니다. "FrontEnd"가 아니라 소문자 "e"를 사용하여 "Frontend"를 입력해야 합니다.
   
   ![][11]
5. Hello에서 **새 ASP.NET 프로젝트** 대화 상자의 hello **´ ï ´** 목록에서 클릭 **MVC**합니다.
   
   ![][12]
6. Hello에 여전히 **새 ASP.NET 프로젝트** 대화 상자를 클릭 hello **인증 변경** 단추입니다. Hello에 **인증 변경** 대화 상자를 클릭 **인증 안 함**, 클릭 하 고 **확인**합니다. 이 자습서의 경우 사용자 로그인이 필요하지 않은 앱을 배포하고 있습니다.
   
    ![][16]
7. Hello에 다시 **새 ASP.NET 프로젝트** 대화 상자를 클릭 **확인** toocreate hello 프로젝트.
8. **솔루션 탐색기**, hello에 **FrontendWebRole** 프로젝트를 마우스 오른쪽 단추로 클릭 **참조**, 클릭 **NuGet 패키지 관리**합니다.
9. Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다. 선택 hello **WindowsAzure.ServiceBus** 클릭, 패키지 **설치**, hello 사용 약관을 수락 합니다.
   
   ![][13]
   
   이제 클라이언트 어셈블리를 참조 하 고 몇 가지 새 코드 파일이 추가 되었습니다. 해당 hello 필요한 note 합니다.
10. **솔루션 탐색기**에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **클래스**를 클릭합니다. Hello에 **이름** 상자 hello 이름을 입력 합니다 **OnlineOrder.cs**합니다. 그런 다음 **추가**를 클릭합니다.

### <a name="write-hello-code-for-your-web-role"></a>웹 역할에 대 한 hello 코드 작성
이 섹션에서는 hello 응용 프로그램이 표시 하는 다양 한 페이지를 만듭니다.

1. Visual Studio에서 hello OnlineOrder.cs 파일에서 기존 네임 스페이스 정을 코드 다음 hello로 바꿉니다.
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. **솔루션 탐색기**에서 **Controllers\HomeController.cs**를 두 번 클릭합니다. Hello 다음 추가 **를 사용 하 여** hello hello 맨 문 파일 서비스 버스와 방금 만든 모델에 대 한 tooinclude hello 네임 스페이스입니다.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. 또한 Visual Studio에서 hello HomeController.cs 파일에서 기존 네임 스페이스 정의 코드 다음 hello로 대체 합니다. 이 코드는 hello 제출 항목 toohello 큐를 처리 하기 위한 메서드를 포함 합니다.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. Hello에서 **빌드** 메뉴를 클릭 하 여 **솔루션 빌드** tootest hello 정확도 지금까지 작업 합니다.
5. 이제 hello에 대 한 hello 보기를 만들 `Submit()` 앞에서 만든 메서드. Hello 내에서 마우스 오른쪽 단추로 클릭 `Submit()` 메서드 (hello 오버 로드 `Submit()` 매개 변수를 사용 하는)을 선택한 후 **뷰 추가**합니다.
   
   ![][14]
6. Hello 보기를 만드는 방법에 대 한 대화 상자가 나타납니다. Hello에 **템플릿** 목록에서 선택 **만들기**합니다. Hello에 **모델 클래스** 목록에서 클릭 hello **OnlineOrder** 클래스입니다.
   
   ![][15]
7. **추가**를 클릭합니다.
8. 이제 변경 hello 응용 프로그램의 이름을 표시 합니다. **솔루션 탐색기**를 두 번 클릭은 **Views\Shared\\_Layout.cshtml** tooopen 파일 hello Visual Studio 편집기에서.
9. **내 ASP.NET 응용 프로그램**과 일치하는 모든 항목을 **LITWARE 제품**으로 바꿉니다.
10. Hello 제거 **홈**, **에 대 한**, 및 **연락처** 링크 합니다. Hello 강조 표시 된 코드를 삭제 합니다.
    
    ![][28]
11. Hello 제출 페이지 tooinclude hello 큐에 대 한 일부 정보를 마지막으로 수정 합니다. **솔루션 탐색기**를 두 번 클릭은 **Views\Home\Submit.cshtml** tooopen 파일 hello Visual Studio 편집기에서. 다음 줄을 다음 hello 추가 `<h2>Submit</h2>`합니다. 지금은 hello `ViewBag.MessageCount` 비어 있습니다. 나중에 채웁니다.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. 이제 UI를 구현했습니다. 누르면 **F5** toorun 응용 프로그램이 예상 대로 표시 되는지 확인 합니다.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>항목 tooa 서비스 버스 큐를 전송 하기 위한 hello 코드 작성
이제 항목 tooa 큐 전송에 대 한 코드를 추가 합니다. 먼저 서비스 버스 큐 연결 정보를 포함하는 클래스를 만듭니다. 그런 다음 Global.aspx.cs에서 연결을 초기화합니다. HomeController.cs tooactually 전송 항목 tooa 서비스 버스 큐의 앞부분에서 만든 hello 제출 코드를 마지막으로 업데이트 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **FrontendWebRole** (하지 hello 역할, hello 프로젝트를 마우스 오른쪽 단추 클릭). **추가**를 클릭한 후 **클래스**를 클릭합니다.
2. Hello 클래스 이름을 **QueueConnector.cs**합니다. 클릭 **추가** toocreate hello 클래스입니다.
3. 이제 hello 연결 정보를 캡슐화 하 고 hello 연결 tooa 서비스 버스 큐를 초기화 하는 코드를 추가 합니다. 코드를 다음 hello hello QueueConnector.cs의 전체 내용을 바꾸고 값을 입력 `your Service Bus namespace` (네임 스페이스 이름) 및 `yourKey`, 하는 hello **기본 키** hello Azure에서에서 이전에 가져온 포털입니다.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. 이제 **Initialize** 메서드가 호출되는지 확인합니다. **솔루션 탐색기**에서 **Global.asax\Global.asax.cs**를 두 번 클릭합니다.
5. Hello 다음 hello의 hello 끝에 코드 줄을 추가 **Application_Start** 메서드.
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. 마지막으로, 항목 toohello 큐를 제출 하려면 앞에서 만든 hello 웹 코드를 업데이트 합니다. **솔루션 탐색기**에서 **Controllers\HomeController.cs**를 두 번 클릭합니다.
7. 업데이트 hello `Submit()` 메서드 (hello 오버 로드에 매개 변수가 없으면) 다음과 같이 tooget hello 메시지 수 hello 큐에 대 한 합니다.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. 업데이트 hello `Submit(OnlineOrder order)` 메서드 (hello 오버 로드 매개 변수를 사용 하는) 다음과 같이 toosubmit 주문 정보 toohello 큐입니다.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. 이제 hello 응용 프로그램을 다시 실행할 수 있습니다. 주문 제출 때마다 hello 메시지 수가 증가 합니다.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Hello 작업자 역할 만들기
이제 hello 주문 제출을 처리 하는 hello 작업자 역할을 만듭니다. 이 예에서는 hello **서비스 버스 큐가 있는 작업자 역할** Visual Studio 프로젝트 템플릿이 합니다. 이미 hello 포털에서 필요한 hello 자격 증명을 획득 합니다.

1. Visual Studio tooyour Azure 계정을 연결 해야 합니다.
2. Visual Studio에서의 **솔루션 탐색기** 마우스 오른쪽 단추로 클릭는 **역할** hello 아래에 폴더 **MultiTierApp** 프로젝트.
3. **추가**를 클릭한 후 **새 작업자 역할 프로젝트**를 클릭합니다. hello **새 역할 프로젝트 추가** 대화 상자가 나타납니다.
   
   ![][26]
4. Hello에 **새 역할 프로젝트 추가** 대화 상자를 클릭 **서비스 버스 큐가 있는 작업자 역할**합니다.
   
   ![][23]
5. Hello에 **이름** 상자, 이름 hello 프로젝트 **OrderProcessingRole**합니다. 그런 다음 **추가**를 클릭합니다.
6. Hello "서비스 버스 네임 스페이스 만들기" 섹션 toohello 클립보드의 9 단계에서 가져온 hello 연결 문자열을 복사 합니다.
7. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **OrderProcessingRole** 5 단계에서 만든 (오른쪽 단추로 클릭 하 고 있는지 확인 **OrderProcessingRole** 아래**역할**, 하지 클래스 hello 및). 그런 다음 **속성**을 클릭합니다.
8. Hello에 **설정** hello 탭 **속성** 대화 상자, hello 내부를 클릭 **값** 에 대 한 **Microsoft.ServiceBus.ConnectionString**, 6 단계에서 복사한 hello 끝점 값을 붙여 넣습니다.
   
   ![][25]
9. 만들기는 **OnlineOrder** hello 큐에서 처리 하는 동안 toorepresent hello orders 클래스입니다. 이미 만든 클래스를 다시 사용할 수 있습니다. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **OrderProcessingRole** 클래스 (하지 hello 역할, hello 클래스 아이콘을 마우스 오른쪽 단추 클릭). **추가**를 클릭한 후 **기존 항목**을 클릭합니다.
10. Toohello 하위 폴더에 대 한 찾아보기 **FrontendWebRole\Models**를 두 번 클릭 하 고 **OnlineOrder.cs** tooadd 것 toothis 프로젝트.
11. **WorkerRole.cs**, hello의 hello 값 변경 **QueueName** 변수 `"ProcessingQueue"` 너무`"OrdersQueue"` hello 코드 다음에 표시 된 대로 합니다.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Hello 다음 추가 문을 사용 하 여 hello hello WorkerRole.cs 파일 위쪽에 있습니다.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. Hello에 `Run()` 함수 hello 내부 `OnMessage()` 호출, hello hello 내용 바꾸기 `try` 코드 다음 hello로 절.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. Hello 응용 프로그램을 완료 했습니다. 솔루션 탐색기에서 hello MultiTierApp 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 hello 전체 응용 프로그램을 테스트할 수 있습니다 선택 **시작 프로젝트로 설정**, 한 다음 F5 키를 눌러 합니다. 메시지 수는 증가 하지 않습니다 hello 작업자 역할 hello 큐에서 항목을 처리 하 고 완료 된 것으로 표시 하기 때문에 유의 합니다. Hello Azure 계산 에뮬레이터 UI를 확인 하 여 작업자 역할의 hello 추적 출력을 볼 수 있습니다. 작업 표시줄의 알림 영역 hello에에서 hello 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여이 작업을 수행할 수 **계산 에뮬레이터 UI 표시**합니다.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>다음 단계
서비스 버스에 대 한 자세한 toolearn hello 다음 리소스 참조:  

* [Azure Service Bus 설명서][sbdocs]  
* [Service Bus 서비스 페이지][sbacom]  
* [어떻게 tooUse 서비스 버스 큐][sbacomqhowto]  

다중 계층 시나리오에 대해 자세히 toolearn 참조:  

* [저장소 테이블, 큐 및 Blob을 사용하는 .NET 다중 계층 응용 프로그램][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
