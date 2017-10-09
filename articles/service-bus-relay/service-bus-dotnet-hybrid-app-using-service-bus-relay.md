---
title: "aaaAzure WCF 릴레이 하이브리드에-프레미스/클라우드 응용 프로그램 (.NET) | Microsoft Docs"
description: "자세한 내용은 방법 Azure WCF 릴레이 사용 하는.NET에서-프레미스/클라우드 toocreate 혼성 응용 프로그램입니다."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Azure WCF 릴레이를 사용하는 .NET 온-프레미스/클라우드 하이브리드 응용 프로그램
## <a name="introduction"></a>소개

이 문서에서는 toobuild 하이브리드 응용 프로그램을 Microsoft Azure 및 Visual Studio 클라우드 하는 방법을 보여 줍니다. hello 자습서에서는 Azure를 사용 하 여 이전 본 경험이 없는 보유 합니다. 30 분 이내에 여러 Azure 리소스를 사용 하는 응용 프로그램 및 hello 클라우드에서 실행 해야 합니다.

다음 내용을 배웁니다.

* 어떻게 toocreate 또는 웹 솔루션에 의해 소비에 대 한 기존 웹 서비스를 조정 합니다.
* 어떻게 toouse hello Azure WCF 릴레이 서비스 tooshare 데이터는 Azure 응용 프로그램 및 웹 서비스 간에 다른 곳에서 호스팅됩니다.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>하이브리드 솔루션에 유용한 Azure 릴레이

비즈니스 솔루션은 일반적으로 새 tootackle로 작성 된 사용자 지정 코드 및 고유한 비즈니스 요구 사항 및 솔루션 및 시스템에에서 이미 준비 되어을 제공 하는 기존 기능 조합으로 구성 합니다.

솔루션 설계자는 toouse hello 클라우드 운영 비용 절감 및 확장 요구 사항을 보다 쉽게 처리를 시작 했습니다. 이 과정에서 hello 클라우드 솔루션에 기존 서비스 자산 만족할 만한 tooleverage가 솔루션에 대 한 구성 요소는 hello 사내 방화벽 내부와 외부로 쉽게 도달할 액세스용 있음을 찾습니다. 많은 내부 서비스를 작성 또는 노출 될 수 있으므로 쉽게 hello 회사 네트워크 가장자리에 방식으로 호스트 되지 않습니다.

[Azure 릴레이](https://azure.microsoft.com/services/service-bus/) 용인지 기존 Windows Communication Foundation (WCF) 웹 서비스의 사용 사례 hello 및 안전 하 게 액세스할 수 있는 toosolutions 필요 없이 hello 회사 경계 외부에 있는 서비스 만들어 개입 수준이 변경 toohello 회사 네트워크 인프라를 사용 합니다. 이러한 릴레이 서비스를 여전히 기존 환경 내 호스트 하지만 들어오는 세션 및 요청 toohello 클라우드에 호스트 된 릴레이 서비스에 대 한 수신을 위임 합니다. 또한 Azure Relay는 [SAS(공유 액세스 서명](../service-bus-messaging/service-bus-sas.md)) 인증을 사용하여 이러한 서비스에 무단으로 액세스하지 못하도록 보호합니다.

## <a name="solution-scenario"></a>솔루션 시나리오
이 자습서에서는 toosee hello 제품 인벤토리 페이지에서 제품 목록을 수 있는 ASP.NET 웹 사이트를 만듭니다.

![][0]

hello 자습서에서는 기존 온-프레미스 시스템을 제품 정보를 유지 하 고 Azure 릴레이 tooreach를 사용 하 여 해당 시스템으로 가정 합니다. 간단한 콘솔 응용 프로그램에서 실행되며 메모리 내 제품 집합에서 지원되는 웹 서비스에서 이를 시뮬레이션합니다. 수 toorun이 콘솔 응용 프로그램 컴퓨터의 수 및 hello 웹 역할을 Azure에 배포 합니다. 이렇게 하면 표시 됩니다는 컴퓨터에 실제로 호출 하는 hello Azure 데이터 센터에서에서 실행 중인 hello 웹 역할 방법을 컴퓨터 하나 이상 방화벽 및 네트워크 주소 변환 (NAT) 계층 뒤에 있는 대부분은 경우에 합니다.

## <a name="set-up-hello-development-environment"></a>Hello 개발 환경 설정

Azure 응용 프로그램 개발을 시작 하려면 먼저 hello 도구를 다운로드 하 고 개발 환경을 설정 합니다.

1. Hello SDK에서에서 hello Azure SDK for.NET 설치 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. Hello에 **.NET** 열 hello 버전 [Visual Studio](http://www.visualstudio.com) 사용 하는 합니다. 이 자습서 사용 하 여 Visual Studio 2015에서에서 hello 실행 하지만 Visual Studio 2017를 사용 합니다.
3. Toorun 라는 메시지가 표시 하거나 저장 hello 설치 관리자를 클릭 **실행**합니다.
4. Hello에 **웹 플랫폼 설치 관리자**, 클릭 **설치** hello 설치를 진행 합니다.
5. Hello 설치가 완료 되 면 할 모든 필요한 toostart toodevelop hello 앱. hello SDK는 Visual Studio에서 Azure 응용 프로그램을 쉽게 개발할 수 있는 도구를 포함 합니다.

## <a name="create-a-namespace"></a>네임스페이스 만들기

Azure에서 릴레이 기능 hello toobegin를 사용 하 여, 서비스 네임 스페이스를 먼저 만들어야 합니다. 네임스페이스는 응용 프로그램 내에서 Azure 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다. Hello에 따라 [여기에 지침이](relay-create-namespace-portal.md) toocreate 릴레이 네임 스페이스입니다.

## <a name="create-an-on-premises-server"></a>온-프레미스 서버 만들기

먼저, (모의) 온-프레미스 제품 카탈로그 시스템을 빌드합니다. 것은 매우 간단 합니다. 이 त ु म toointegrate 완전 한 서비스 화면과 상호 제품 카탈로그는 실제 온-프레미스 시스템을 나타내는 것으로 볼 수 있습니다.

이 프로젝트는 Visual Studio 콘솔 응용 프로그램 및 hello를 사용 하 여 [Azure Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello 구성 설정 및 서비스 버스 라이브러리.

### <a name="create-hello-project"></a>Hello 프로젝트 만들기

1. 관리자 권한을 사용하여 Microsoft Visual Studio를 시작합니다. toodo 따라서 hello Visual Studio 프로그램 아이콘을 마우스 오른쪽 단추로 클릭 **관리자 권한으로 실행**합니다.
2. Hello에 Visual Studio에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.
3. **설치된 템플릿**의 **Visual C#**에 있는 **콘솔 앱(.NET Framework)**을 클릭합니다. Hello에 **이름** 상자 hello 이름을 입력 합니다 **ProductsServer**:

   ![][11]
4. 클릭 **확인** toocreate hello **ProductsServer** 프로젝트.
5. Visual Studio 용 NuGet 패키지 관리자 hello를 이미 설치한 경우 toohello 다음 단계를 건너뜁니다. 그렇지 않으면 [NuGet][NuGet]을 방문하여 [NuGet 설치](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)를 클릭합니다. Hello 프롬프트 tooinstall hello NuGet 패키지 관리자에 따라 다음 Visual Studio를 다시 시작 합니다.
6. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsServer** 프로젝트를 선택한 다음 클릭 **NuGet 패키지 관리**합니다.
7. Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다. 선택 hello **WindowsAzure.ServiceBus** 패키지 합니다.
8. 클릭 **설치**, hello 사용 약관을 수락 합니다.

   ![][13]

   이제 클라이언트 어셈블리를 참조 하는 데 해당 hello 필요한 note 합니다.
8. 제품 계약의 새 클래스를 추가합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsServer** 프로젝트 **추가**, 클릭 하 고 **클래스**합니다.
9. Hello에 **이름** 상자 hello 이름을 입력 합니다 **ProductsContract.cs**합니다. 그런 다음 **추가**를 클릭합니다.
10. **ProductsContract.cs**, hello 서비스에 대 한 hello 계약을 정의 하는 코드를 다음 hello hello 네임 스페이스 정의 바꿉니다.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. Program.cs에 hello 네임 스페이스 정을 hello 프로필 서비스와 그에 대 한 hello 호스트를 추가 하는 코드를 다음 hello로 바꿉니다.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. 솔루션 탐색기에서 hello를 두 번 클릭 **App.config** tooopen 파일 hello Visual Studio 편집기에서. Hello hello 맨 아래에 `<system.ServiceModel>` 요소 (하지만 안에서 `<system.ServiceModel>`), hello 다음 XML 코드를 추가 합니다. 수 있는지 tooreplace *yourServiceNamespace* 여 네임 스페이스의 hello 이름의 및 *yourKey* hello 포털에서 이전 검색 hello SAS 키를 가진:

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. Hello에 App.config에 여전히 `<appSettings>` 요소, replace hello 연결 문자열 값 hello 포털에서 이전에 가져온 hello 연결 문자열을 사용 합니다.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. 키를 눌러 **Ctrl + Shift + B** 또는 hello **빌드** 메뉴를 클릭 **솔루션 빌드** toobuild hello 응용 프로그램 및 지금까지 진행 중인 작업의 hello 정확도 확인 합니다.

## <a name="create-an-aspnet-application"></a>ASP.NET 응용 프로그램 만들기

이 섹션에서는 제품 서비스에서 검색한 데이터를 표시하는 간단한 ASP.NET 응용 프로그램을 빌드합니다.

### <a name="create-hello-project"></a>Hello 프로젝트 만들기

1. 관리자 권한으로 Visual Studio 2013을 실행 중인지 확인합니다.
2. Hello에 Visual Studio에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.
3. **설치된 템플릿**에서 **Visual C#** 아래에 있는 **ASP.NET 웹 응용 프로그램(.NET Framework)**을 클릭합니다. 이름 hello 프로젝트 **ProductsPortal**합니다. 그런 후 **OK**를 클릭합니다.

   ![][15]

4. Hello에서 **ASP.NET 템플릿** hello 목록 **새 ASP.NET 웹 응용 프로그램** 대화 상자에서 클릭 **MVC**합니다.

   ![][16]

6. Hello 클릭 **인증 변경** 단추입니다. Hello에 **인증 변경** 대화 상자에서 **인증 안 함** 을 선택한 다음 클릭 **확인**합니다. 이 자습서의 경우 사용자 로그인이 필요하지 않은 앱을 배포하고 있습니다.

    ![][18]

7. Hello에 다시 **새 ASP.NET 웹 응용 프로그램** 대화 상자를 클릭 하 여 **확인** toocreate hello MVC 응용 프로그램입니다.
8. 이제 새 웹앱에 대한 Azure 리소스를 구성해야 합니다. Hello에 hello 단계를 따라 [이 문서의 섹션 tooAzure 게시](../app-service-web/app-service-web-get-started-dotnet.md)합니다. 그런 다음 toothis 자습서 돌아간 toohello 다음 단계를 진행 합니다.
10. 솔루션 탐색기에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **클래스**를 클릭합니다. Hello에 **이름** 상자 hello 이름을 입력 합니다 **Product.cs**합니다. 그런 다음 **추가**를 클릭합니다.

    ![][17]

### <a name="modify-hello-web-application"></a>Hello 웹 응용 프로그램 수정

1. Visual Studio에서 hello Product.cs 파일에서 코드 다음 hello로 hello 기존 네임 스페이스 정의 대체 합니다.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. 솔루션 탐색기에서 확장 hello **컨트롤러** 폴더 hello를 두 번 클릭 한 다음 **HomeController.cs** tooopen 파일 Visual Studio에서.
3. **HomeController.cs**, 코드 다음 hello hello 기존 네임 스페이스 정의 바꿉니다.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. 솔루션 탐색기에서 hello Views\Shared 폴더를 확장 한 다음를 두 번 클릭 **_Layout.cshtml** tooopen hello Visual Studio 편집기에서.
5. 모든 항목을 변경 **내 ASP.NET 응용 프로그램** 너무**LITWARE의 제품**합니다.
6. Hello 제거 **홈**, **에 대 한**, 및 **연락처** 링크 합니다. 다음 예제는 hello, hello 강조 표시 된 코드를 삭제 합니다.

    ![][41]

7. 솔루션 탐색기에서 hello Views\Home 폴더를 확장 한 다음를 두 번 클릭 **Index.cshtml** tooopen hello Visual Studio 편집기에서. Hello 파일의 전체 내용을 hello 코드 다음 hello로 대체 합니다.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. 작업의 tooverify hello 정확도 지금까지 누르면 **Ctrl + Shift + B** toobuild hello 프로젝트.

### <a name="run-hello-app-locally"></a>Hello 응용 프로그램을 로컬로 실행

작동 하는 hello 응용 프로그램 tooverify를 실행 합니다.

1. 되도록 **ProductsPortal** 는 hello 활성 프로젝트입니다. 솔루션 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 프로젝트로 설정**합니다.
2. Visual Studio에서 **F5** 키를 누릅니다.
3. 응용 프로그램이 브라우저에 실행되는 것으로 나타나야 합니다.

   ![][21]

## <a name="put-hello-pieces-together"></a>Hello 조각 준비

hello 다음 단계는 toohook hello ASP.NET 응용 프로그램으로 hello 온-프레미스 제품 서버를 설치 합니다.

1. 열려 있지 않으면 Visual Studio에서 다시 열고 hello **ProductsPortal** hello에서 만든 프로젝트 [ASP.NET 응용 프로그램 만들기](#create-an-aspnet-application) 섹션.
2. Hello "온-프레미스 서버 만들기" 섹션에서 유사한 toohello 단계가 hello NuGet 패키지 toohello 프로젝트 참조를 추가 합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 프로젝트를 선택한 다음 클릭 **NuGet 패키지 관리**합니다.
3. "서비스 버스" 및 선택 hello에 대 한 검색 **WindowsAzure.ServiceBus** 항목입니다. 그런 다음 hello 설치를 완료 하 고이 대화 상자를 닫습니다.
4. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 프로젝트를 선택한 다음 클릭 **추가**, 다음 **기존 항목**합니다.
5. Toohello 이동 **ProductsContract.cs** hello에서 파일 **ProductsServer** 콘솔 프로젝트. Toohighlight ProductsContract.cs를 클릭 합니다. 아래쪽 화살표는 hello 다음 너무 클릭**추가**, 클릭 **링크로 추가**합니다.

   ![][24]

6. 이제 hello 열 **HomeController.cs** hello Visual Studio 편집기에서 파일 및 코드 다음 hello hello 네임 스페이스 정의 바꿉니다. 수 있는지 tooreplace *yourServiceNamespace* 서비스 네임 스페이스의 hello 이름의 및 *yourKey* SAS 키를 가진 합니다. 이렇게 하면 hello 클라이언트 toocall hello 온-프레미스 서비스 에서도 hello hello 호출 결과 반환 합니다.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 솔루션 (확인 되었는지 tooright 클릭 hello 솔루션을 hello 프로젝트가 아닌). **추가**를 클릭한 후 **기존 프로젝트**를 클릭합니다.
8. Toohello 이동 **ProductsServer** hello를 두 번 클릭 한 다음 프로젝트를 **ProductsServer.csproj** 솔루션 파일 tooadd 것입니다.
9. **ProductsServer** 주문 toodisplay hello 데이터에서 실행 되어야 합니다 **ProductsPortal**합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 솔루션과 클릭 **속성**합니다. hello **속성 페이지** 대화 상자가 표시 됩니다.
10. 왼쪽 hello, 클릭 **시작 프로젝트**합니다. Hello 오른쪽 클릭 **여러 개의 시작 프로젝트**합니다. 되도록 **ProductsServer** 및 **ProductsPortal** 를 해당 순서로 함께 표시 **시작** 모두에 대 한 hello 동작으로 설정 합니다.

      ![][25]

11. Hello에 여전히 **속성** 대화 상자에서 클릭 **프로젝트 종속성** hello 왼쪽에 있습니다.
12. Hello에 **프로젝트** 목록에서 클릭 **ProductsServer**합니다. **ProductsPortal**이 선택되지 않았는지 확인합니다.
13. Hello에 **프로젝트** 목록에서 클릭 **ProductsPortal**합니다. **ProductsServer**가 선택되어 있는지 확인합니다.

    ![][26]

14. 클릭 **확인** hello에 **속성 페이지** 대화 상자.

## <a name="run-hello-project-locally"></a>Hello 프로젝트를 로컬로 실행

눌러 Visual Studio에서 tootest hello 응용 프로그램을 로컬로 **F5**합니다. hello 온-프레미스 서버 (**ProductsServer**), 첫 번째로 시작 해야 하 고 hello **ProductsPortal** 응용 프로그램이 브라우저 창에서 시작 됩니다. 이 이번에 표시 됩니다는 hello 제품 재고 hello 제품 서비스 온-프레미스 시스템에서 검색 된 데이터를 나열 합니다.

![][10]

키를 눌러 **새로 고침** hello에 **ProductsPortal** 페이지. 때마다 hello 페이지를 새로 고침, 메시지를 표시 하는 hello 서버 응용 프로그램에 표시 됩니다 때 `GetProducts()` 에서 **ProductsServer** 호출 됩니다.

Toohello 다음 단계를 진행 하기 전에 두 응용 프로그램을 닫습니다.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Hello ProductsPortal 프로젝트 tooan Azure 웹 응용 프로그램 배포

hello 다음 단계는 toorepublish hello Azure 웹 앱 **ProductsPortal** 프런트 엔드 합니다. 다음 hello지 않습니다.

1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 프로젝트를 마우스 클릭 **게시**합니다. 클릭 **게시** hello에 **게시** 페이지.

  > [!NOTE]
  > 때 hello hello 브라우저 창에서 오류 메시지가 표시 될 수 있습니다 **ProductsPortal** 웹 프로젝트 hello 배포 후 자동으로 시작 합니다. 이 예상 된 하 고 있기 때문에 발생 hello **ProductsServer** 응용 프로그램이 아직 실행 되지 않습니다.
>
>

2. Hello의 hello URL 복사 hello URL hello 다음 단계에서 필요 하므로 웹 앱을 배포 합니다. 또한 Visual Studio의 hello Azure 앱 서비스 활동 창에서이 URL을 가져올 수 있습니다.

  ![][9]

3. 응용 프로그램을 실행 하는 hello 브라우저 창 toostop hello를 닫습니다.

### <a name="set-productsportal-as-web-app"></a>웹앱으로 ProductsPortal 설정

Hello 클라우드에서 실행 중인 hello 응용 프로그램을 하기 전에 확인 해야 **ProductsPortal** 웹 앱과 Visual Studio 내에서 시작 됩니다.

1. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **ProductsPortal** 프로젝트를 마우스 클릭 **속성**합니다.
2. Hello 왼쪽 열에서 클릭 **웹**합니다.
3. Hello에 **시작 작업** 섹션에서 hello **시작 URL** 단추 hello 텍스트 상자에 URL을 입력 hello; 이전에 배포 된 웹 앱에 대 한 예를 들어 `http://productsportal1234567890.azurewebsites.net/`합니다.

    ![][27]

4. Hello에서 **파일** Visual Studio에서 메뉴를 클릭 **모두 저장**합니다.
5. Visual Studio에서 hello 빌드 메뉴에서 클릭 **솔루션 다시 빌드**합니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행

1. F5 toobuild 누르고 hello 응용 프로그램을 실행 합니다. hello 온-프레미스 서버 (hello **ProductsServer** 콘솔 응용 프로그램), 첫 번째로 시작 해야 하 고 hello **ProductsPortal** hello 화면 뒤에 나와 있는 것 처럼 응용 프로그램이 브라우저 창에서 시작 됩니다 샷 합니다. 해당 hello 제품 재고 hello 제품 서비스 온-프레미스 시스템에서 검색 된 데이터를 나열 하 고 hello 웹 응용 프로그램에서 해당 데이터를 표시 합니다. 다시 확인 합니다. Hello URL toomake 있는지를 확인 하는 **ProductsPortal** hello 클라우드의 Azure 웹 앱으로 실행 합니다.

   ![][1]

   > [!IMPORTANT]
   > hello **ProductsServer** 콘솔 응용 프로그램 실행 해야 하며 수 tooserve hello 데이터 toohello **ProductsPortal** 응용 프로그램입니다. Hello 브라우저에 오류가 표시 되는 경우 더 많은 몇 초 정도 대기 **ProductsServer** tooload 및 다음 디스플레이 hello 메시지입니다. 다음 키를 누릅니다 **새로 고침** hello 브라우저에서 합니다.
   >
   >

   ![][37]
2. Hello 브라우저에서 다시 눌러 **새로 고침** hello에 **ProductsPortal** 페이지. 때마다 hello 페이지를 새로 고침, 메시지를 표시 하는 hello 서버 응용 프로그램에 표시 됩니다 때 `GetProducts()` 에서 **ProductsServer** 호출 됩니다.

    ![][38]

## <a name="next-steps"></a>다음 단계

toolearn Azure 릴레이 대 한 자세한 참조 리소스 다음 hello:  

* [Azure 릴레이란?](relay-what-is-it.md)  
* [Toouse 릴레이 하는 방법](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
