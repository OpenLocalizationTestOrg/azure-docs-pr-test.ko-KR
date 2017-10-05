---
title: "Azure Event Hubs 인증 및 보안 모델의 개요 | Microsoft Docs"
description: "이벤트 허브 인증 및 보안 모델 개요"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="d35dd-103">이벤트 허브 인증 및 보안 모델 개요</span><span class="sxs-lookup"><span data-stu-id="d35dd-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="d35dd-104">Azure 이벤트 허브 보안 모델은 다음 요구 사항을 만족합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="d35dd-105">유효한 자격 증명을 제공하는 클라이언트만 이벤트 허브로 데이터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="d35dd-106">클라이언트는 다른 클라이언트를 가장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="d35dd-107">악성 클라이언트는 이벤트 허브로 데이터를 보내지 못하도록 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="d35dd-108">클라이언트 인증</span><span class="sxs-lookup"><span data-stu-id="d35dd-108">Client authentication</span></span>
<span data-ttu-id="d35dd-109">Event Hubs 보안 모델은 [공유 액세스 서명(SAS)](../service-bus-messaging/service-bus-sas.md) 토큰 및 *이벤트 게시자*의 조합을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="d35dd-110">이벤트 게시자는 이벤트 허브에 대한 가상 끝점을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="d35dd-111">게시자는 이벤트 허브에 메시지를 보내는 데만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="d35dd-112">게시자에서 메시지를 받을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="d35dd-113">일반적으로 이벤트 허브에서는 클라이언트당 하나의 게시자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="d35dd-114">이벤트 허브의 게시자에게 전달되는 모든 메시지는 해당 이벤트 허브 내의 큐에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="d35dd-115">게시자는 세분화된 액세스 제어 및 제한을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="d35dd-116">각 Event Hubs 클라이언트는 클라이언트에 업로드되는 고유 토큰을 할당받습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="d35dd-117">각 고유 토큰이 고유한 다른 게시자에 대한 액세스가 허용되도록 토큰이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="d35dd-118">토큰을 소유하는 클라이언트는 하나의 게시자에게만 보낼 수 있으며 다른 게시자에게는 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="d35dd-119">여러 클라이언트가 동일한 토큰을 공유하는 경우 각 클라이언트가 게시자를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="d35dd-120">권장하지는 않지만 이벤트 허브에 대한 직접 액세스 권한을 부여하는 토큰을 가진 장치를 장착할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="d35dd-121">이 토큰을 보유하는 모든 장치는 해당 이벤트 허브에 직접 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="d35dd-122">이러한 장치는 제한의 대상이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="d35dd-123">또한 장치에서 해당 이벤트 허브로 보내는 것을 차단할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="d35dd-124">모든 토큰은 SAS 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="d35dd-125">일반적으로 모든 토큰은 동일한 키로 서명됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="d35dd-126">클라이언트는 키를 인식하지 않기 때문에 다른 클라이언트가 토큰을 제조하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="d35dd-127">SAS 키 만들기</span><span class="sxs-lookup"><span data-stu-id="d35dd-127">Create the SAS key</span></span>

<span data-ttu-id="d35dd-128">Event Hubs 네임스페이스를 만들면, 서비스는 **RootManageSharedAccessKey**라는 256비트 SAS 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="d35dd-129">이 키는 네임스페이스에 대한 송신, 수신 및 관리 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="d35dd-130">추가 키를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-130">You can also create additional keys.</span></span> <span data-ttu-id="d35dd-131">특정 이벤트 허브에 대한 전송 권한을 부여하는 키를 생성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="d35dd-132">이 항목의 나머지 부분에서는 이 키의 이름을 **EventHubSendKey**로 지정했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="d35dd-133">다음 예제에서는 이벤트 허브를 만들 때 전송 전용 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="d35dd-134">토큰 생성</span><span class="sxs-lookup"><span data-stu-id="d35dd-134">Generate tokens</span></span>

<span data-ttu-id="d35dd-135">SAS 키를 사용하여 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="d35dd-136">클라이언트당 하나의 토큰만 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-136">You must produce only one token per client.</span></span> <span data-ttu-id="d35dd-137">다음 메서드를 사용하여 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="d35dd-138">모든 토큰은 **EventHubSendKey** 키를 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="d35dd-139">각 토큰에는 고유한 URI가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="d35dd-140">이 메서드를 호출할 때 URI는 `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="d35dd-141">모든 토큰에 대해 `PUBLISHER_NAME`는 제외하고 URI는 동일하며, 각 토큰에 대해서는 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="d35dd-142">`PUBLISHER_NAME`은 해당 토큰을 수신하는 클라이언트의 ID를 나타내는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="d35dd-143">이 메서드는 다음 구조를 사용하여 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="d35dd-144">토큰 만료 시간(초)은 1970년 1월 1일에서부터 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="d35dd-145">다음은 토큰 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="d35dd-146">일반적으로 토큰의 수명은 클라이언트와 유사하거나 더 깁니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="d35dd-147">클라이언트에 새 토큰을 가져오는 기능이 있는 경우 짧은 수명의 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="d35dd-148">데이터 전송</span><span class="sxs-lookup"><span data-stu-id="d35dd-148">Sending data</span></span>
<span data-ttu-id="d35dd-149">토큰이 생성된 후에 각 클라이언트는 자체의 고유한 토큰과 함께 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="d35dd-150">클라이언트가 이벤트 허브로 데이터를 전송할 경우 토큰을 사용해서 보내기 요청에 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="d35dd-151">공격자가 도청 및 토큰 가로채기를 하지 못하도록 방지하려면 클라이언트와 이벤트 허브 간의 통신은 암호화된 채널을 통해 이루어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="d35dd-152">클라이언트 차단 목록</span><span class="sxs-lookup"><span data-stu-id="d35dd-152">Blacklisting clients</span></span>
<span data-ttu-id="d35dd-153">토큰이 공격자에 의해 도난당한 경우 공격자가 토큰을 도난당한 클라이언트로 가장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="d35dd-154">클라이언트를 차단할 경우 해당 클라이언트는 다른 게시자를 사용하는 새 토큰을 수신할 때까지 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="d35dd-155">백 엔드 응용 프로그램의 인증</span><span class="sxs-lookup"><span data-stu-id="d35dd-155">Authentication of back-end applications</span></span>

<span data-ttu-id="d35dd-156">Event Hubs는 이 이벤트 허브 클라이언트에서 생성된 데이터를 사용하는 백 엔드 응용 프로그램을 인증하기 위해 Service Bus 항목에 사용된 모델과 유사한 보안 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="d35dd-157">이벤트 허브 소비자 그룹은 서비스 버스 토픽에 대한 구독과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="d35dd-158">소비자 그룹 생성 요청에 이벤트 허브 또는 이벤트 허브가 속한 네임스페이스에 대한 관리 권한을 부여하는 토큰이 함께 지정된 경우 클라이언트는 소비자 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="d35dd-159">수신 요청이 소비자 그룹, 이벤트 허브 또는 이벤트 허브가 속한 네임스페이스에서의 수신 권한을 부여하는 토큰과 함께 지정된 경우 클라이언트는 해당 소비자 그룹의 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="d35dd-160">서비스 버스의 현재 버전은 개별 구독에 대한 SAS 규칙을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="d35dd-161">이벤트 허브 소비자 그룹에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="d35dd-162">SAS 지원은 나중에 두 기능에 대해 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="d35dd-163">개별 소비자 그룹에 대한 SAS 인증이 없는 경우, 공용 키가 있는 모든 소비자 그룹을 보호하기 위해 SAS 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="d35dd-164">이 방식에서는 응용 프로그램이 이벤트 허브의 임의의 소비자 그룹에서 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d35dd-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d35dd-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d35dd-165">Next steps</span></span>
<span data-ttu-id="d35dd-166">이벤트 허브에 대한 자세한 내용은 다음 항목을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="d35dd-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="d35dd-167">[이벤트 허브 개요]</span><span class="sxs-lookup"><span data-stu-id="d35dd-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="d35dd-168">[공유 액세스 서명 개요]</span><span class="sxs-lookup"><span data-stu-id="d35dd-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="d35dd-169">[Event Hubs를 사용하는 샘플 응용 프로그램]</span><span class="sxs-lookup"><span data-stu-id="d35dd-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="d35dd-170">[이벤트 허브 개요]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="d35dd-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="d35dd-171">[Event Hubs를 사용하는 샘플 응용 프로그램]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="d35dd-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="d35dd-172">[공유 액세스 서명 개요]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="d35dd-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

