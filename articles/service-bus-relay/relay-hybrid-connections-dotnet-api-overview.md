---
title: "Azure Relay .NET Standard API 개요 | Microsoft Docs"
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
ms.openlocfilehash: f3f4a2e721b1a75a5b92a5c17a9939c7013340d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="3b04b-103">Azure Relay 하이브리드 연결 .NET Standard API 개요</span><span class="sxs-lookup"><span data-stu-id="3b04b-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="3b04b-104">이 문서는 일부 핵심적인 Azure Relay 하이브리드 연결 .NET Standard [클라이언트 API](/dotnet/api/microsoft.azure.relay)를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="3b04b-105">Relay 연결 문자열 작성기</span><span class="sxs-lookup"><span data-stu-id="3b04b-105">Relay Connection String Builder</span></span>

<span data-ttu-id="3b04b-106">[RelayConnectionStringBuilder][RelayConnectionStringBuilder] 클래스는 Relay 하이브리드 연결에 관련된 연결 문자열의 서식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="3b04b-107">연결 문자열의 서식을 확인하거나 연결 문자열을 처음부터 작성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="3b04b-108">예제를 보려면 다음 코드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b04b-108">See the following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of the Hybrid Connection}";
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

<span data-ttu-id="3b04b-109">연결 문자열을 `RelayConnectionStringBuilder` 메서드에 직접 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="3b04b-110">이 작업을 사용하면 연결 문자열이 유효한 형식인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-110">This operation enables you to verify that the connection string is in a valid format.</span></span> <span data-ttu-id="3b04b-111">매개 변수가 잘못된 경우 생성자가 `ArgumentException`을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare the connectionStringBuilder so that it can be used outside of the loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create the connectionStringBuilder using the supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="3b04b-112">하이브리드 연결 스트림</span><span class="sxs-lookup"><span data-stu-id="3b04b-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="3b04b-113">[HybridConnectionStream][HCStream] 클래스는 [HybridConnectionClient][HCClient] 또는 [HybridConnectionListener][HCListener]로 작업하는지에 상관 없이 Azure Relay 끝점에서 데이터를 송수신하는 데 사용되는 기본 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="3b04b-114">하이브리드 연결 스트림 가져오기</span><span class="sxs-lookup"><span data-stu-id="3b04b-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="3b04b-115">수신기</span><span class="sxs-lookup"><span data-stu-id="3b04b-115">Listener</span></span>
<span data-ttu-id="3b04b-116">[HybridConnectionListener][HCListener]를 사용하면 다음과 같이 `HybridConnectionStream` 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="3b04b-117">클라이언트</span><span class="sxs-lookup"><span data-stu-id="3b04b-117">Client</span></span>
<span data-ttu-id="3b04b-118">[HybridConnectionClient][HCClient]를 사용하면 다음과 같이 `HybridConnectionStream` 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="3b04b-119">데이터 수신</span><span class="sxs-lookup"><span data-stu-id="3b04b-119">Receiving data</span></span>
<span data-ttu-id="3b04b-120">[HybridConnectionStream][HCStream] 클래스를 사용하면 양방향 통신이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="3b04b-121">대부분의 경우 스트림에서 지속적으로 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-121">In most cases, you continuously receive from the stream.</span></span> <span data-ttu-id="3b04b-122">스트림에서 텍스트를 읽는 경우 데이터 구문 분석이 더 쉬운 [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) 개체를 사용하는 것이 좋을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-122">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span></span> <span data-ttu-id="3b04b-123">예를 들어 아닌 데이터를 `byte[]`가 아닌 텍스트로 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="3b04b-124">다음 코드는 취소가 요청될 때까지 스트림에서 개별 텍스트 줄을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel the while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from the 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of the processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="3b04b-125">데이터 전송</span><span class="sxs-lookup"><span data-stu-id="3b04b-125">Sending data</span></span>
<span data-ttu-id="3b04b-126">연결을 설정하면 Relay 끝점으로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-126">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="3b04b-127">연결 개체는 [스트림](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx)을 상속하기 때문에 데이터를 `byte[]`로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="3b04b-128">다음 예제에 이 작업을 수행하는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-128">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="3b04b-129">단, 매번 문자열을 인코딩할 필요 없이 텍스트를 직접 전송하려는 경우 `hybridConnectionStream` 개체를 [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) 개체로 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b04b-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="3b04b-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b04b-130">Next steps</span></span>
<span data-ttu-id="3b04b-131">Azure Relay에 대한 자세한 내용은 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="3b04b-131">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="3b04b-132">Microsoft.Azure.Relay 참조</span><span class="sxs-lookup"><span data-stu-id="3b04b-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="3b04b-133">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="3b04b-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="3b04b-134">사용 가능한 Relay API</span><span class="sxs-lookup"><span data-stu-id="3b04b-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener