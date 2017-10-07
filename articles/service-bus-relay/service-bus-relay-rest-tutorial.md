---
title: "Azure 릴레이 사용 하 여 aaaService 버스 REST 자습서 | Microsoft Docs"
description: "REST 기반 인터페이스를 표시하는 간단한 Azure Service Bus 릴레이 호스트 응용 프로그램을 구축합니다."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Azure WCF 릴레이 REST 자습서

이 자습서에서는 간단한 Azure 릴레이 toobuild REST 기반 인터페이스를 노출 하는 응용 프로그램을 호스트 하는 방법을 설명 합니다. REST 웹 클라이언트를 경우 HTTP 통해 서비스 버스 Api 요청 tooaccess hello 웹 브라우저와 같은 수 있습니다.

hello 자습서에서는 서비스 버스에 hello Windows Communication Foundation (WCF) REST 프로그래밍 모델 tooconstruct REST 서비스를 사용 합니다. 자세한 내용은 참조 [WCF REST 프로그래밍 모델](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) 및 [서비스 디자인 및 구현](/dotnet/framework/wcf/designing-and-implementing-services) hello WCF 설명서에에서 있습니다.

## <a name="step-1-create-a-namespace"></a>단계 1: 네임스페이스 만들기

Azure에서 릴레이 기능 hello toobegin를 사용 하 여, 서비스 네임 스페이스를 먼저 만들어야 합니다. 네임스페이스는 응용 프로그램 내에서 Azure 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다. Hello에 따라 [여기에 지침이](relay-create-namespace-portal.md) toocreate 릴레이 네임 스페이스입니다.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>2 단계: Azure 릴레이와 REST 기반 WCF 서비스 계약 toouse 정의

WCF REST 스타일 서비스를 만들 때는 hello 계약을 정의 해야 합니다. hello 계약 작업 hello 지 원하는 호스트를 지정 합니다. 서비스 작업은 웹 서비스 메서드로 생각할 수 있습니다. 계약은 C++, C#, 또는 Visual Basic 인터페이스를 정의하여 만듭니다. Hello 인터페이스의 각 메서드에 tooa 특정 서비스 작업에 해당 합니다. hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 특성 적용된 tooeach 인터페이스 여야 하며 hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 특성에 적용 된 tooeach 작업 이어야 합니다. Hello 변수가 있는 인터페이스의 메서드가 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) hello 없는 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), 메서드가 표시 되지 않습니다. 이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 표시 됩니다.

hello WCF 계약 및 REST 스타일 계약 간의 주요 차이점은 속성 toohello hello 추가 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx)합니다. 이 속성을 사용 하면 hello에 인터페이스 tooa 메서드에서 메서드 toomap hello 인터페이스의 다른 쪽입니다. 이 경우 사용 합니다 [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink 메서드 tooHTTP GET입니다. 따라서 서비스 버스 tooaccurately 검색 및 toohello 인터페이스 전송 되는 명령을 해석할 수 있습니다.

### <a name="toocreate-a-contract-with-an-interface"></a>계약 인터페이스와 함께 toocreate

1. 관리자 권한으로 Visual Studio를 열고: hello에서 마우스 오른쪽 단추로 클릭 hello 프로그램 **시작** 메뉴를 차례로 클릭 **관리자 권한으로 실행**합니다.
2. 새 콘솔 응용 프로그램 프로젝트를 만듭니다. Hello 클릭 **파일** 메뉴와 선택 **새로**을 선택한 후 **프로젝트**합니다. Hello에 **새 프로젝트** 대화 상자에서 클릭 **Visual C#**선택, hello **콘솔 응용 프로그램** 서식 파일을 하 고 이름을 **ImageListener**합니다. Hello 기본값을 사용 하 여 **위치**합니다. 클릭 **확인** toocreate hello 프로젝트.
3. C# 프로젝트의 경우 Visual Studio는 `Program.cs` 파일을 만듭니다. 이 클래스는 빈 포함 `Main()` 올바르게 콘솔 응용 프로그램 프로젝트 toobuild에 대 한 요구 하는 방법입니다.
4. 추가 참조 tooService 버스 및 **System.ServiceModel.dll** hello Service Bus NuGet 패키지를 설치 하 여 toohello 프로젝트. 이 패키지는 hello WCF 뿐만 아니라 참조 toohello 서비스 버스 라이브러리에 자동으로 추가 **System.ServiceModel**합니다. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **ImageListener** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다. Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다. 클릭 **설치**, hello 사용 약관을 수락 합니다.
5. 해야 명시적으로 참조를 추가 하면 너무**system.servicemodel.web.dll을 참조** toohello 프로젝트:
   
    a. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **참조** hello 프로젝트 폴더와 클릭 한 다음 아래에 폴더 **참조 추가**합니다.
   
    b. Hello에 **참조 추가** 대화 상자를 클릭 hello **프레임 워크** 탭과 hello hello 왼쪽에 **검색** 상자에 입력 합니다 **System.ServiceModel.Web** . 선택 hello **System.ServiceModel.Web** 확인란을 선택한 다음 클릭 **확인**합니다.
6. Hello 다음 추가 `using` hello 위쪽 hello Program.cs 파일에는 문입니다.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) WCF의 toobasic 기능을 프로그래밍 방식으로 액세스할 수 있도록 하는 hello 네임 스페이스입니다. WCF 릴레이 여러 hello 개체 및 WCF toodefine 서비스 계약의 특성을 사용합니다. 이 네임스페이스는 대부분의 릴레이 응용 프로그램에서 사용됩니다. 마찬가지로, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) 사용 하면 Azure 릴레이 및 hello 클라이언트 웹 브라우저와 통신할 수 있는 hello 개체인 hello 채널을 정의 합니다. 마지막으로, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) toocreate 웹 기반 응용 프로그램을 사용 하는 hello 형식을 포함 합니다.
7. Hello 이름 바꾸기 `ImageListener` 네임 스페이스 너무**Microsoft.ServiceBus.Samples**합니다.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. 직접 여는 중괄호 hello 네임 스페이스 선언의 hello, 후 이라는 새 인터페이스 정의 **IImageContract** hello 적용 **ServiceContractAttribute** 특성 toohello 인터페이스는 값 `http://samples.microsoft.com/ServiceModel/Relay/`합니다. 코드의 hello 범위 전체에서 사용 하는 hello 네임 스페이스에서 네임 스페이스 값 hello 다릅니다. hello 네임 스페이스 값은이 계약에 대 한 고유 식별자로 사용 되며 버전 정보가 있어야 합니다. 자세한 내용은 [서비스 버전 관리](http://go.microsoft.com/fwlink/?LinkID=180498)를 참조하세요. Hello 네임 스페이스를 명시적으로 지정 하면 hello 기본 네임 스페이스 값을 toohello 계약 이름에 추가 되지 않습니다.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. Hello 내 `IImageContract` 인터페이스를 hello 단일 작업 hello에 대 한 메서드를 선언 `IImageContract` hello에 노출 계약 인터페이스 및 hello 적용 `OperationContractAttribute` hello 공용 서비스 버스의 일부로 tooexpose 되도록 toohello 메서드 특성 계약입니다.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. Hello에 **OperationContract** 특성을 추가 hello **WebGet** 값입니다.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    이렇게 하면 HTTP GET 요청이 너무 릴레이 서비스 tooroute hello`GetImage`, 및의 값을 반환 하는 tootranslate hello `GetImage` HTTP GETRESPONSE 회신으로 합니다. Hello 자습서의 뒷부분에서 사용 합니다 웹 브라우저 tooaccess이 메서드와 toodisplay hello 이미지 hello 브라우저에서.
11. Hello 직후 `IImageContract` 정의 모두 hello에서 상속 되는 채널을 선언 `IImageContract` 및 `IClientChannel` 인터페이스입니다.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    채널은는 hello 서비스와 클라이언트가 전달 정보 tooeach 다른 hello WCF 개체입니다. 이상에서는 호스트 응용 프로그램에 hello 채널을 만들어집니다. 이 채널 toopass hello의에서 HTTP GET 요청이 hello 브라우저 tooyour에 다음 사용 하 여 azure 릴레이 **GetImage** 구현 합니다. 또한 사용 하 여 hello 채널 tootake hello hello 릴레이 **GetImage** 값을 반환 하 고 hello 클라이언트 브라우저에 대 한 HTTP GETRESPONSE로 변환 합니다.
12. Hello에서 **빌드** 메뉴를 클릭 하 여 **솔루션 빌드** tooconfirm hello 정확도 지금까지 작업 합니다.

### <a name="example"></a>예제
hello 코드 다음 WCF 릴레이 계약을 정의 하는 기본적인 인터페이스를 보여 줍니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>3 단계: 서비스 버스 REST 기반 WCF 서비스 계약 toouse 구현
REST 스타일 WCF 릴레이 서비스를 만드는 먼저 만들어야 hello 계약 인터페이스를 사용 하 여 정의 해야 합니다. hello 다음 단계는 tooimplement hello 인터페이스입니다. 라는 클래스를 생성이 포함 됩니다 **ImageService** 구현 하는 사용자 정의 hello **IImageContract** 인터페이스입니다. Hello 계약을 구현 후 App.config 파일을 사용 하 여 hello 인터페이스를 구성 합니다. hello 구성 파일 hello hello 서비스 이름, hello 이름 hello 계약 및 hello 유형의 프로토콜을 사용 하는 toocommunicate hello 릴레이 서비스와 같은 hello 응용 프로그램에 필요한 정보를 포함 합니다. 이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.

Hello 그 이전 단계를 REST 스타일 계약과 릴레이 WCF 계약 구현 간의 차이가 매우 작은 있으면 합니다.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>tooimplement REST 스타일 서비스 버스 계약
1. 이라는 새 클래스를 만들 **ImageService** hello의 hello 정의 바로 뒤 **IImageContract** 인터페이스입니다. hello **ImageService** 클래스 구현 hello **IImageContract** 인터페이스입니다.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    비슷한 tooother 인터페이스 구현에 다른 파일에 hello 정의 구현할 수 있습니다. 그러나이 자습서에서는 hello 구현에에서 표시 hello 동일한 hello 인터페이스 정의로 파일 및 `Main()` 메서드.
2. Hello 적용 [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello 특성 **IImageService** 클래스 hello 클래스 tooindicate는 WCF 계약 구현 합니다.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    앞에서 설명한 바와 같이 이 네임스페이스는 기존의 네임스페이스가 아닙니다. 만으로도 hello hello 계약을 식별 하는 WCF 아키텍처의 일부입니다. 자세한 내용은 참조 hello [데이터 계약 이름을](https://msdn.microsoft.com/library/ms731045.aspx) hello WCF 설명서의에서 항목입니다.
3. .Jpg 이미지 tooyour 프로젝트를 추가 합니다.  
   
    이 hello 서비스 hello 수신 브라우저에에서 표시 하는 그림입니다. 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **추가**를 클릭합니다. 그 다음 **기존 항목**을 클릭합니다. 사용 하 여 hello **기존 항목 추가** 대화 상자 toobrowse tooan.jpg, 적절 한 클릭 **추가**합니다.
   
    Hello 파일을 추가할 때는 다음 사항을 확인 **모든 파일** hello 드롭다운 목록에서 다음 toohello에서 선택 된 **파일 이름:** 필드입니다. 이 자습서의 나머지 부분 hello 가정 해당 hello hello 이미지 이름이 "image.jpg"입니다. 다른 파일을 만든 경우 toorename hello 이미지 했거나 코드 toocompensate 변경 됩니다.
4. 서비스를 실행 하는 hello에 hello 이미지 파일을 찾을 수 있는지 toomake **솔루션 탐색기** hello 이미지 파일을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다. Hello에 **속성** 창 설정 **tooOutput 디렉터리 복사** 너무**변경 된 내용만 복사**합니다.
5. 추가 참조 toohello **System.Drawing.dll** 어셈블리 toohello 프로젝트를 마우스 추가적으로 관련 된 hello 다음 `using` 문.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. Hello에 **ImageService** 클래스, 추가 hello 생성자 로드 비트맵 hello 및 toosend 준비 다음 그 toohello 클라이언트 브라우저.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Hello 이전 코드 바로 뒤 hello 다음 추가 **GetImage** hello에 대 한 메서드 **ImageService** hello 이미지가 포함 된 클래스는 HTTP tooreturn 메시지입니다.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    이 구현에서는 **MemoryStream** tooretrieve 이미지 hello 및 toohello 브라우저 스트리밍에 대 한 준비 합니다. Hello 스트림 위치를 0에서 시작, hello 스트림 콘텐츠를 jpeg 선언 및 hello 정보를 스트리밍합니다.
8. Hello에서 **빌드** 메뉴를 클릭 하 여 **솔루션 빌드**합니다.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>서비스 버스에서 hello 웹 서비스를 실행 하기 위한 toodefine hello 구성
1. **솔루션 탐색기**를 두 번 클릭 **App.config** tooopen hello Visual Studio 편집기에서.
   
    hello **App.config** hello 서비스 이름, 끝점 (즉,: hello 위치 서로 toocommunicate 클라이언트와 호스트에 대 한 Azure 릴레이 노출) 및 (프로토콜을 사용 하는 toocommunicate의 hello 형식)를 바인딩 파일에 포함 되어 있습니다. hello 기본적인 차이점은 해당 hello 구성 된 서비스 끝점 참조 tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) 바인딩.
2. hello `<system.serviceModel>` XML 요소는 하나 이상의 서비스를 정의 하는 WCF 요소. 사용 되는 toodefine hello 서비스 이름과 끝점을 더 합니다. Hello hello 맨 아래에 `<system.serviceModel>` 요소 (하지만 안에서 `<system.serviceModel>`), 추가 `<bindings>` hello 콘텐츠 뒤에 있는 요소입니다. Hello 응용 프로그램에 사용 된 hello 바인딩을 정의 합니다. 여러 바인딩을 정의할 수 있지만 이 자습서에서는 하나만 정의합니다.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    hello 이전 코드에 대 한 WCF 릴레이 정의 [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) 바인딩으로 **relayClientAuthenticationType** 도**None**합니다. 이 설정은 이 바인딩을 사용하는 끝점에 클라이언트 자격 증명이 필요 없다는 것을 나타냅니다.
3. Hello 후 `<bindings>` 요소를 추가 `<services>` 요소입니다. 비슷한 toohello 바인딩에 단일 구성 파일에 여러 서비스를 정의할 수 있습니다. 하지만 이 자습서에서는 하나만 정의합니다.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    이 단계에서는 이전에 정의 된 hello 기본값을 사용 하는 서비스 구성 **webHttpRelayBinding**합니다. Hello 기본 사용 **sbTokenProvider**, hello 다음 단계에서 정의 됩니다.
4. Hello 후 `<services>` 요소를 만들는 `<behaviors>` 요소 콘텐츠 뒤, hello로 "SAS_KEY" 대체 hello로 *공유 액세스 서명을* hello에서 이전에 가져온 (SAS) 키 [Azure 포털 ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. Hello에 App.config에 여전히 `<appSettings>` 요소, replace hello 전체 연결 문자열 값 hello 포털에서 이전에 가져온 hello 연결 문자열을 사용 합니다. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. Hello에서 **빌드** 메뉴를 클릭 하 여 **솔루션 빌드** toobuild hello 전체 솔루션입니다.

### <a name="example"></a>예제
hello 다음 코드를 보여 줍니다 hello를 사용 하 여 서비스 버스에서 실행 되는 REST 기반 서비스에 대 한 hello 계약 및 서비스 구현을 **WebHttpRelayBinding** 바인딩.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

hello 다음 예제에서는 hello 서비스와 관련 된 hello App.config 파일

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>4 단계: 호스트 hello REST 기반 WCF 서비스 toouse Azure 릴레이
이 단계에서는 toorun 웹 서비스는 콘솔 응용 프로그램을 사용 하 여 WCF 릴레이 된 하는 방법을 설명 합니다. 이 단계에서 작성 된 hello 코드의 전체 목록은 hello 절차 다음에 hello 예에 제공 됩니다.

### <a name="toocreate-a-base-address-for-hello-service"></a>toocreate hello 서비스에 대 한 기본 주소
1. Hello에 `Main()` 함수 선언, 프로젝트의 가변 toostore hello 네임 스페이스를 만듭니다. 있는지 tooreplace 확인 `yourNamespace` 이전에 만든 hello 릴레이 네임 스페이스의 hello 이름의 합니다.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    서비스 버스 네임 스페이스 toocreate 고유한 URI 프로그램의 hello 이름을 사용합니다.
2. 만들기는 `Uri` hello 네임 스페이스를 기반으로 하는 hello 서비스의 기본 주소 hello에 대 한 인스턴스.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate hello 웹 서비스 호스트를 구성 합니다.
* 이 섹션 앞부분에서 만든 hello URI 주소를 사용 하 여 hello 웹 서비스 호스트를 만듭니다.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    hello 서비스 호스트는 hello 호스트 응용 프로그램을 인스턴스화하는 hello WCF 개체입니다. 이 예에서는 전달 hello 유형 toocreate 원하는 호스트의 (는 **ImageService**), 또한 tooexpose hello 호스트 응용 프로그램 원하는 주소 hello 및 합니다.

### <a name="toorun-hello-web-service-host"></a>toorun hello 웹 서비스 호스트
1. Hello 서비스를 엽니다.
   
    ```csharp
    host.Open();
    ```
    hello 서비스가 실행 됩니다.
2. Hello 서비스가 실행 되 고 toostop 서비스 hello 하는 방법을 나타내는 메시지를 표시 합니다.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. 완료 되 면 hello 서비스 호스트를 닫습니다.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>예제
다음 예제는 hello hello 자습서와 호스트 hello 서비스 콘솔 응용 프로그램에서에서는 hello 서비스 계약과 구현을 이전 단계에서를 포함 합니다. Hello를 라는 ImageListener.exe 실행 파일로 코드를 다음 컴파일하십시오.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>Hello 코드 컴파일
Hello 솔루션을 빌드한 후 다음 toorun hello 응용 프로그램 hello지 않습니다.

1. 키를 눌러 **F5**, 또는 toohello 실행 파일 위치 (ImageListener\bin\Debug\ImageListener.exe) toorun hello 서비스를 검색 합니다. Tooperform hello 다음 단계를 필요한 대로 hello 응용 프로그램 실행을 유지 합니다.
2. 복사한 hello 명령 프롬프트에서 hello 주소 브라우저 toosee hello 이미지에 붙여 넣습니다.
3. 작업을 완료 하는 경우 키를 눌러 **Enter** hello 명령 프롬프트 창 tooclose hello 응용 프로그램에서 합니다.

## <a name="next-steps"></a>다음 단계
Hello 서비스 버스 릴레이 서비스를 사용 하는 응용 프로그램을 만든 했으므로 다음 Azure 릴레이 대 한 자세한 문서 toolearn hello 참조:

* [Azure Service Bus 아키텍처 개요](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Azure Relay 개요](relay-what-is-it.md)
* [Toouse hello WCF.net 서비스를 릴레이 하는 방법](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
