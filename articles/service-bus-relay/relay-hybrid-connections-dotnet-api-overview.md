---
title: "hello Azure 릴레이.NET 표준 Api의 aaaOverview | Microsoft Docs"
description: "Relay .NET Standard API 개요"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Azure Relay 하이브리드 연결 .NET Standard API 개요

이 문서는 Azure 릴레이 하이브리드 연결.NET 표준 hello 키 중 일부를 요약 [클라이언트 Api](/dotnet/api/microsoft.azure.relay)합니다.
  
## <a name="relay-connection-string-builder"></a>Relay 연결 문자열 작성기

hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] 클래스 형식을 tooRelay 특정 하이브리드 연결 된 연결 문자열을 지정 합니다. 연결 문자열 또는 toobuild 처음부터 연결 문자열의 tooverify hello 형식을 사용할 수 있습니다. Hello 코드 예제를 보려면 다음을 참조 하십시오.

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

한 연결을 전달할 수도 있습니다 문자열 간접적으로 toohello `RelayConnectionStringBuilder` 메서드. 이 작업에서는 hello 연결 문자열은 올바른 형식의 tooverify가 있습니다. Hello 생성자를 생성 하는 경우 유효 하지 않으면 hello 매개 변수 중 하나는 `ArgumentException`합니다.

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a>하이브리드 연결 스트림
hello [HybridConnectionStream] [ HCStream] 클래스는 사용 되는 기본 개체 toosend hello와 데이터를 Azure 릴레이 끝점을 사용 하는 여부는 [HybridConnectionClient] [ HCClient], 또는 [HybridConnectionListener][HCListener]합니다.

### <a name="getting-a-hybrid-connection-stream"></a>하이브리드 연결 스트림 가져오기

#### <a name="listener"></a>수신기
[HybridConnectionListener][HCListener]를 사용하면 다음과 같이 `HybridConnectionStream` 개체를 가져올 수 있습니다.

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>클라이언트
[HybridConnectionClient][HCClient]를 사용하면 다음과 같이 `HybridConnectionStream` 개체를 가져올 수 있습니다.

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>데이터 수신
hello [HybridConnectionStream] [ HCStream] 클래스 양방향 통신을 사용 합니다. 대부분의 경우에서 계속 해 서 표시 hello 스트림에서 합니다. Toouse 수도 hello 스트림의 텍스트를 읽는 경우는 [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) hello 데이터 보다 쉽게 구문 분석할 수 있도록 하는 개체입니다. 예를 들어 아닌 데이터를 `byte[]`가 아닌 텍스트로 읽을 수 있습니다.

hello 다음 코드 줄을 읽은 개별 텍스트의 hello 스트림에서 취소가 요청 될 때까지:

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a>데이터 전송
설정 된 연결을 설정한 후에 메시지 toohello 릴레이 끝점을 보낼 수 있습니다. Hello 연결 개체에서 상속 되므로 [스트림](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), 데이터를 보내기는 `byte[]`합니다. hello 방법을 예제와 다음 toodo이:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

그러나 하려는 경우 toosend 텍스트를 직접 tooencode hello 문자열 매번 필요 없이 hello 래핑할 수 `hybridConnectionStream` 개체는 [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) 개체입니다.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>다음 단계
다음이 링크를 방문 하는 Azure 릴레이 대 한 자세한 toolearn:

* [Microsoft.Azure.Relay 참조](/dotnet/api/microsoft.azure.relay)
* [Azure 릴레이란?](relay-what-is-it.md)
* [사용 가능한 Relay API](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener