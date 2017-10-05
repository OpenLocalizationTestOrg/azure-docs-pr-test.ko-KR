---
title: "공유 액세스 서명을 사용한 Azure Service Bus 인증 | Microsoft Docs"
description: "공유 액세스 서명을 사용한 Azure Service Bus 인증 개요, Azure Service Bus를 사용한 SAS 인증 상세 정보"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a2760072acb7c62204759f3ec0d3cb9899460f2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a><span data-ttu-id="ddfb6-103">공유 액세스 서명을 사용한 Service Bus 인증</span><span class="sxs-lookup"><span data-stu-id="ddfb6-103">Service Bus authentication with Shared Access Signatures</span></span>

<span data-ttu-id="ddfb6-104">*공유 액세스 서명*(SAS)은 Service Bus 메시징의 기본 보안 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-104">*Shared Access Signatures* (SAS) are the primary security mechanism for Service Bus messaging.</span></span> <span data-ttu-id="ddfb6-105">이 문서에서는 SAS, 그 작동 방법 및 플랫폼과 상관 없는 방식으로 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-105">This article discusses SAS, how they work, and how to use them in a platform-agnostic way.</span></span>

<span data-ttu-id="ddfb6-106">SAS 인증을 사용하면 응용 프로그램을 네임스페이스 또는 특정 권한이 연관된 메시징 엔터티(큐 또는 토픽)에서 구성된 선택키를 사용하여 Service Bus에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-106">SAS authentication enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="ddfb6-107">그런 다음 이 키를 사용하여 클라이언트가 서비스 버스를 인증하는 데 차례로 사용할 수 있는 SAS 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-107">You can then use this key to generate a SAS token that clients can in turn use to authenticate to Service Bus.</span></span>

<span data-ttu-id="ddfb6-108">SAS 인증 지원은 Azure SDK 버전 2.0 이후에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-108">SAS authentication support is included in the Azure SDK version 2.0 and later.</span></span>

## <a name="overview-of-sas"></a><span data-ttu-id="ddfb6-109">SAS 개요</span><span class="sxs-lookup"><span data-stu-id="ddfb6-109">Overview of SAS</span></span>

<span data-ttu-id="ddfb6-110">공유 액세스 서명은 SHA-256 보안 해시 또는 URI에 따른 인증 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-110">Shared Access Signatures are an authentication mechanism based on SHA-256 secure hashes or URIs.</span></span> <span data-ttu-id="ddfb6-111">SAS는 모든 서비스 버스 서비스에서 사용되는 매우 강력한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-111">SAS is an extremely powerful mechanism that is used by all Service Bus services.</span></span> <span data-ttu-id="ddfb6-112">실제 사용 시, SAS에는 *공유 액세스 정책*과 *공유 액세스 서명*(*토큰*이라고 부름)의 두 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-112">In actual use, SAS has two components: a *shared access policy* and a *Shared Access Signature* (often called a *token*).</span></span>

<span data-ttu-id="ddfb6-113">서비스 버스에서 SAS 인증은 서비스 버스 리소스에 연결된 권한이 있는 암호화 키의 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-113">SAS authentication in Service Bus involves the configuration of a cryptographic key with associated rights on a Service Bus resource.</span></span> <span data-ttu-id="ddfb6-114">클라이언트는 SAS 토큰을 발급하여 서비스 버스 리소스에 액세스를 주장합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-114">Clients claim access to Service Bus resources by presenting a SAS token.</span></span> <span data-ttu-id="ddfb6-115">이 토큰은 액세스된 리소스 URI 및 구성된 키로 서명된 만료 매개 변수로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-115">This token consists of the resource URI being accessed, and an expiry signed with the configured key.</span></span>

<span data-ttu-id="ddfb6-116">Service Bus [릴레이](service-bus-fundamentals-hybrid-solutions.md#relays), [큐](service-bus-fundamentals-hybrid-solutions.md#queues) 및 [토픽](service-bus-fundamentals-hybrid-solutions.md#topics)에 대해 공유 액세스 서명 권한 부여 규칙을 구성할 수 있습니다 </span><span class="sxs-lookup"><span data-stu-id="ddfb6-116">You can configure Shared Access Signature authorization rules on Service Bus [relays](service-bus-fundamentals-hybrid-solutions.md#relays), [queues](service-bus-fundamentals-hybrid-solutions.md#queues), and [topics](service-bus-fundamentals-hybrid-solutions.md#topics).</span></span>

<span data-ttu-id="ddfb6-117">SAS 인증은 다음과 같은 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-117">SAS authentication uses the following elements:</span></span>

* <span data-ttu-id="ddfb6-118">[공유 액세스 권한 부여 규칙](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): Base64 표현에서 256비트 기본 암호화 키, 선택적 보조키 및 키 이름과 관련된 권한입니다(*수신*, *보내기* 또는 *관리* 권한의 컬렉션).</span><span class="sxs-lookup"><span data-stu-id="ddfb6-118">[Shared Access authorization rule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): A 256-bit primary cryptographic key in Base64 representation, an optional secondary key, and a key name and associated rights (a collection of *Listen*, *Send*, or *Manage* rights).</span></span>
* <span data-ttu-id="ddfb6-119">[공유 액세스 서명](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) 토큰: 리소스 문자열의 HMAC-SHA256을 사용하여 생성되고 액세스된 리소스의 URI 및 암호화 키를 가진 만료 매개 변수로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-119">[Shared Access Signature](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) token: Generated using the HMAC-SHA256 of a resource string, consisting of the URI of the resource that is accessed and an expiry, with the cryptographic key.</span></span> <span data-ttu-id="ddfb6-120">다음 섹션에 설명된 서명 및 다른 요소는 문자열로 서식이 지정되어 SAS 토큰을 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-120">The signature and other elements described in the following sections are formatted into a string to form the SAS token.</span></span>

## <a name="shared-access-policy"></a><span data-ttu-id="ddfb6-121">공유 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="ddfb6-121">Shared access policy</span></span>

<span data-ttu-id="ddfb6-122">SAS에 대해 잘 이해하기 위해서는 정책부터 시작하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-122">An important thing to understand about SAS is that it starts with a policy.</span></span> <span data-ttu-id="ddfb6-123">각각의 정책에 대해 **이름**, **범위** 및 **권한** 등, 3가지 정보를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-123">For each policy, you decide on three pieces of information: **name**, **scope**, and **permissions**.</span></span> <span data-ttu-id="ddfb6-124">**이름** 은 해당 범위 내에서 고유한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-124">The **name** is just that; a unique name within that scope.</span></span> <span data-ttu-id="ddfb6-125">범위는 아주 쉬운데, 해당 리소스의 URI를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-125">The scope is easy enough: it's the URI of the resource in question.</span></span> <span data-ttu-id="ddfb6-126">Service Bus 네임스페이스의 경우, 범위는 `https://<yournamespace>.servicebus.windows.net/` 등과 같이 정규화된 도메인 이름(FQDN)입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-126">For a Service Bus namespace, the scope is the fully qualified domain name (FQDN), such as `https://<yournamespace>.servicebus.windows.net/`.</span></span>

<span data-ttu-id="ddfb6-127">정책에서 사용 가능한 권한은 대부분 설명이 따로 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-127">The available permissions for a policy are largely self-explanatory:</span></span>

* <span data-ttu-id="ddfb6-128">보내기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-128">Send</span></span>
* <span data-ttu-id="ddfb6-129">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-129">Listen</span></span>
* <span data-ttu-id="ddfb6-130">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-130">Manage</span></span>

<span data-ttu-id="ddfb6-131">정책을 만든 후 *기본 키*와 *보조 키*가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-131">After you create the policy, it is assigned a *Primary Key* and a *Secondary Key*.</span></span> <span data-ttu-id="ddfb6-132">이들은 강력한 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-132">These are cryptographically strong keys.</span></span> <span data-ttu-id="ddfb6-133">잃어 버리거나 누출되지 않도록 하세요. 항상 [Azure Portal][Azure portal]에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-133">Don't lose them or leak them - they'll always be available in the [Azure portal][Azure portal].</span></span> <span data-ttu-id="ddfb6-134">생성된 키 중 하나를 사용할 수 있으며 언제든지 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-134">You can use either of the generated keys, and you can regenerate them at any time.</span></span> <span data-ttu-id="ddfb6-135">그러나 정책에서 기본 키를 다시 생성하거나 변경할 경우, 만든 공유 액세스 서명은 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-135">However, if you regenerate or change the primary key in the policy, any Shared Access Signatures created from it will be invalidated.</span></span>

<span data-ttu-id="ddfb6-136">서비스 버스 네임스페이스를 만들 때 **RootManageSharedAccessKey**라는 전체 네임스페이스에 대해 정책이 자동으로 만들어지며 이 정책은 모든 사용 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-136">When you create a Service Bus namespace, a policy is automatically created for the entire namespace called **RootManageSharedAccessKey**, and this policy has all permissions.</span></span> <span data-ttu-id="ddfb6-137">**root**로 로그온하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-137">You don't log on as **root**, so don't use this policy unless there's a really good reason.</span></span> <span data-ttu-id="ddfb6-138">포털의 해당 네임스페이스에 대한 **구성** 탭에서 추가 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-138">You can create additional policies in the **Configure** tab for the namespace in the portal.</span></span> <span data-ttu-id="ddfb6-139">Service Bus의 단일 트리 수준(네임스페이스, 큐 등)에는 최대 12개의 정책까지만 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-139">It's important to note that a single tree level in Service Bus (namespace, queue, etc.) can only have up to 12 policies attached to it.</span></span>

## <a name="configuration-for-shared-access-signature-authentication"></a><span data-ttu-id="ddfb6-140">공유 액세스 서명 인증을 위한 구성</span><span class="sxs-lookup"><span data-stu-id="ddfb6-140">Configuration for Shared Access Signature authentication</span></span>
<span data-ttu-id="ddfb6-141">서비스 버스 네임스페이스, 큐 또는 항목에 대한 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-141">You can configure the [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) rule on Service Bus namespaces, queues, or topics.</span></span> <span data-ttu-id="ddfb6-142">서비스 버스 구독에서 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 의 구성은 현재 지원되지 않지만 네임스페이스 또는 항목에 구성된 규칙을 사용하여 구독에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-142">Configuring a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) on a Service Bus subscription is currently not supported, but you can use rules configured on a namespace or topic to secure access to subscriptions.</span></span> <span data-ttu-id="ddfb6-143">이 절차를 설명하는 작업 샘플은 [서비스 버스 구독으로 공유 액세스 서명(SAS) 인증 사용](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-143">For a working sample that illustrates this procedure, see the [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) sample.</span></span>

<span data-ttu-id="ddfb6-144">이러한 규칙을 서비스 버스 네임 스페이스, 큐 또는 항목에서 최대 12개까지 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-144">A maximum of 12 such rules can be configured on a Service Bus namespace, queue, or topic.</span></span> <span data-ttu-id="ddfb6-145">서비스 버스 네임 스페이스에 구성된 규칙이 해당 네임스페이스에 있는 모든 엔터티에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-145">Rules that are configured on a Service Bus namespace apply to all entities in that namespace.</span></span>

![SAS](./media/service-bus-sas/service-bus-namespace.png)

<span data-ttu-id="ddfb6-147">이 그림에서는 *manageRuleNS*, *sendRuleNS* 및 *listenRuleNS* 권한 부여 규칙이 큐 Q1 및 토픽 topic T1에 적용되는 반면, *listenRuleQ* 및 *sendRuleQ*는 큐 Q1에만 적용되고 *sendRuleT*는 토픽 T1에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-147">In this figure, the *manageRuleNS*, *sendRuleNS*, and *listenRuleNS* authorization rules apply to both queue Q1 and topic T1, while *listenRuleQ* and *sendRuleQ* apply only to queue Q1 and *sendRuleT* applies only to topic T1.</span></span>

<span data-ttu-id="ddfb6-148">[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 의 키 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-148">The key parameters of a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) are as follows:</span></span>

| <span data-ttu-id="ddfb6-149">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ddfb6-149">Parameter</span></span> | <span data-ttu-id="ddfb6-150">설명</span><span class="sxs-lookup"><span data-stu-id="ddfb6-150">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ddfb6-151">*KeyName*</span><span class="sxs-lookup"><span data-stu-id="ddfb6-151">*KeyName*</span></span> |<span data-ttu-id="ddfb6-152">권한 부여 규칙을 설명하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-152">A string that describes the authorization rule.</span></span> |
| <span data-ttu-id="ddfb6-153">*PrimaryKey*</span><span class="sxs-lookup"><span data-stu-id="ddfb6-153">*PrimaryKey*</span></span> |<span data-ttu-id="ddfb6-154">서명하고 SAS 토큰의 유효성을 검사하기 위한 base64로 인코딩된 256비트 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-154">A base64-encoded 256-bit primary key for signing and validating the SAS token.</span></span> |
| <span data-ttu-id="ddfb6-155">*SecondaryKey*</span><span class="sxs-lookup"><span data-stu-id="ddfb6-155">*SecondaryKey*</span></span> |<span data-ttu-id="ddfb6-156">서명하고 SAS 토큰의 유효성을 검사하기 위한 base64로 인코딩된 256비트 보조 키입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-156">A base64-encoded 256-bit secondary key for signing and validating the SAS token.</span></span> |
| <span data-ttu-id="ddfb6-157">*AccessRights*</span><span class="sxs-lookup"><span data-stu-id="ddfb6-157">*AccessRights*</span></span> |<span data-ttu-id="ddfb6-158">권한 부여 규칙에서 부여된 액세스 권한의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-158">A list of access rights granted by the authorization rule.</span></span> <span data-ttu-id="ddfb6-159">이러한 권한은 수신, 보내기 및 관리 권한의 컬렉션일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-159">These rights can be any collection of Listen, Send, and Manage rights.</span></span> |

<span data-ttu-id="ddfb6-160">Service Bus 네임스페이스를 프로비전하면 기본적으로 [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName)이 **RootManageSharedAccessKey**로 설정된 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-160">When a Service Bus namespace is provisioned, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), with [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) set to **RootManageSharedAccessKey**, is created by default.</span></span>

## <a name="generate-a-shared-access-signature-token"></a><span data-ttu-id="ddfb6-161">공유 액세스 서명(토큰) 생성</span><span class="sxs-lookup"><span data-stu-id="ddfb6-161">Generate a Shared Access Signature (token)</span></span>

<span data-ttu-id="ddfb6-162">정책 자체는 서비스 버스에 대한 액세스 토큰이 아니며</span><span class="sxs-lookup"><span data-stu-id="ddfb6-162">The policy itself is not the access token for Service Bus.</span></span> <span data-ttu-id="ddfb6-163">기본 또는 보조 키 중 하나를 사용하여 액세스 토큰이 생성되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-163">It is the object from which the access token is generated - using either the primary or secondary key.</span></span> <span data-ttu-id="ddfb6-164">공유 액세스 권한 부여 규칙에 지정된 서명 키에 액세스하는 클라이언트는 SAS 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-164">Any client that has access to the signing keys specified in the shared access authorization rule can generate the SAS token.</span></span> <span data-ttu-id="ddfb6-165">토큰은 다음 형식으로 문자열을 신중하게 선별하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-165">The token is generated by carefully crafting a string in the following format:</span></span>

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

<span data-ttu-id="ddfb6-166">여기서 `signature-string`은 토큰 범위(이전 섹션에서 설명한 대로 **범위**)의 SHA-256 해시로, CRLF가 첨부되어 있고 만료 시간(Epoch 이후 초 단위: 1970년 1월 1일에 `00:00:00 UTC`)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-166">Where `signature-string` is the SHA-256 hash of the scope of the token (**scope** as described in the previous section) with a CRLF appended and an expiry time (in seconds since the epoch: `00:00:00 UTC` on 1 January 1970).</span></span> 

> [!NOTE]
> <span data-ttu-id="ddfb6-167">토큰 만료 시간이 짧아지지 않게, 만료 시간 값을 최소한 32비트의 부호 없는 정수나 Long(64비트) 정수로 인코딩하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-167">To avoid a short token expiry time, it is recommended that you encode the expiry time value as at least a 32-bit unsigned integer, or preferably a long (64-bit) integer.</span></span>  
> 
> 

<span data-ttu-id="ddfb6-168">해시는 다음 의사 코드와 유사하며 32바이트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-168">The hash looks similar to the following pseudo code and returns 32 bytes.</span></span>

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

<span data-ttu-id="ddfb6-169">비해시 값이 **SharedAccessSignature** 문자열에 있으므로 수신자는 동일한 결과를 반환하도록 동일한 매개 변수로 해시를 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-169">The non-hashed values are in the **SharedAccessSignature** string so that the recipient can compute the hash with the same parameters, to be sure that it returns the same result.</span></span> <span data-ttu-id="ddfb6-170">URI는 범위를 지정하며 키 이름은 해시를 계산하는 데 사용할 정책을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-170">The URI specifies the scope, and the key name identifies the policy to be used to compute the hash.</span></span> <span data-ttu-id="ddfb6-171">이것은 보안의 관점에서 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-171">This is important from a security standpoint.</span></span> <span data-ttu-id="ddfb6-172">서명이 수신자(서비스 버스)에서 계산하는 것과 일치하지 않으면 액세스가 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-172">If the signature doesn't match that which the recipient (Service Bus) calculates, then access is denied.</span></span> <span data-ttu-id="ddfb6-173">이제 발신자에게 키에 대한 액세스 권한이 있음을 알 수 있으므로 정책에 지정된 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-173">At this point you can be sure that the sender had access to the key and should be granted the rights specified in the policy.</span></span>

<span data-ttu-id="ddfb6-174">이 작업에 인코딩된 리소스 URI를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-174">Note that you should use the encoded resource URI for this operation.</span></span> <span data-ttu-id="ddfb6-175">리소스 URI은 액세스를 하려는 서비스 버스 리소스의 전체 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-175">The resource URI is the full URI of the Service Bus resource to which access is claimed.</span></span> <span data-ttu-id="ddfb6-176">예를 들면 `http://<namespace>.servicebus.windows.net/<entityPath>` 또는 `sb://<namespace>.servicebus.windows.net/<entityPath>`입니다. 즉, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-176">For example, `http://<namespace>.servicebus.windows.net/<entityPath>` or `sb://<namespace>.servicebus.windows.net/<entityPath>`; that is, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.</span></span>

<span data-ttu-id="ddfb6-177">이 URI로 또는 부모 계층 중 하나에 의해 지정된 엔터티에 서명에 사용된 공유 액세스 권한 부여 규칙을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-177">The shared access authorization rule used for signing must be configured on the entity specified by this URI, or by one of its hierarchical parents.</span></span> <span data-ttu-id="ddfb6-178">예를 들어 이전 예에서 `http://contoso.servicebus.windows.net/contosoTopics/T1` 또는 `http://contoso.servicebus.windows.net`입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-178">For example, `http://contoso.servicebus.windows.net/contosoTopics/T1` or `http://contoso.servicebus.windows.net` in the previous example.</span></span>

<span data-ttu-id="ddfb6-179">SAS 토큰은 `signature-string`에서 사용된 `<resourceURI>`의 모든 리소스에 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-179">A SAS token is valid for all resources under the `<resourceURI>` used in the `signature-string`.</span></span>

<span data-ttu-id="ddfb6-180">SAS 토큰의 [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) 은 토큰을 생성하는 데 사용된 공유 액세스 권한 부여 규칙의 **keyName** 을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-180">The [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) in the SAS token refers to the **keyName** of the shared access authorization rule used to generate the token.</span></span>

<span data-ttu-id="ddfb6-181">*URL로 인코딩된 resourceURI* 은 서명을 계산하는 동안 서명할 문자열에서 사용된 URI와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-181">The *URL-encoded-resourceURI* must be the same as the URI used in the string-to-sign during the computation of the signature.</span></span> <span data-ttu-id="ddfb6-182">[%로 인코딩](https://msdn.microsoft.com/library/4fkewx0t.aspx)되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-182">It should be [percent-encoded](https://msdn.microsoft.com/library/4fkewx0t.aspx).</span></span>

<span data-ttu-id="ddfb6-183">[SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 개체에서 정기적으로 사용되는 키를 다시 생성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-183">It is recommended that you periodically regenerate the keys used in the [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object.</span></span> <span data-ttu-id="ddfb6-184">응용 프로그램은 일반적으로 [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) 를 사용하여 SAS 토큰을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-184">Applications should generally use the [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) to generate a SAS token.</span></span> <span data-ttu-id="ddfb6-185">키를 다시 생성하는 경우 [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) 를 이전 기본 키로 교체하고 새 키를 새 기본 키로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-185">When regenerating the keys, you should replace the [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) with the old primary key, and generate a new key as the new primary key.</span></span> <span data-ttu-id="ddfb6-186">이 옵션을 사용하면 이전 기본 키로 발급되고 아직 만료되지 않은 권한 부여에 대한 토큰을 사용하여 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-186">This enables you to continue using tokens for authorization that were issued with the old primary key, and that have not yet expired.</span></span>

<span data-ttu-id="ddfb6-187">키가 손상되고 키를 해제하면 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)의 [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) 및 [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) 모두를 새 키로 바꿔 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-187">If a key is compromised and you have to revoke the keys, you can regenerate both the [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) and the [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) of a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), replacing them with new keys.</span></span> <span data-ttu-id="ddfb6-188">이 절차는 이전 키로 서명된 모든 토큰을 무효화합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-188">This procedure invalidates all tokens signed with the old keys.</span></span>

## <a name="how-to-use-shared-access-signature-authentication-with-service-bus"></a><span data-ttu-id="ddfb6-189">서비스 버스를 사용한 공유 액세스 서명을 인증하는 방법</span><span class="sxs-lookup"><span data-stu-id="ddfb6-189">How to use Shared Access Signature authentication with Service Bus</span></span>

<span data-ttu-id="ddfb6-190">다음과 같은 시나리오는 권한 부여 규칙의 구성, SAS 토큰의 생성 및 클라이언트 권한 부여를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-190">The following scenarios include configuration of authorization rules, generation of SAS tokens, and client authorization.</span></span>

<span data-ttu-id="ddfb6-191">구성을 설명하고 SAS 권한 부여를 사용하는 서비스 버스 응용 프로그램의 작업 샘플 전체는 [서비스 버스를 사용하여 공유 액세스 서명 인증](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-191">For a full working sample of a Service Bus application that illustrates the configuration and uses SAS authorization, see [Shared Access Signature authentication with Service Bus](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8).</span></span> <span data-ttu-id="ddfb6-192">서비스 버스 구독을 보호하기 위해 네임스페이스 또는 항목에 구성된 SAS 권한 부여 규칙의 사용 방법을 설명하는 관련된 샘플은 [서비스 버스 구독으로 공유 액세스 서명(SAS) 사용](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c)에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-192">A related sample that illustrates the use of SAS authorization rules configured on namespaces or topics to secure Service Bus subscriptions is available here: [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).</span></span>

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a><span data-ttu-id="ddfb6-193">네임스페이스에 대한 공유 액세스 권한 부여 규칙 액세스</span><span class="sxs-lookup"><span data-stu-id="ddfb6-193">Access Shared Access Authorization rules on a namespace</span></span>

<span data-ttu-id="ddfb6-194">서비스 버스 네임스페이스 루트에 대한 작업은 인증서 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-194">Operations on the Service Bus namespace root require certificate authentication.</span></span> <span data-ttu-id="ddfb6-195">Azure 구독에 대한 관리 인증서를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-195">You must upload a management certificate for your Azure subscription.</span></span> <span data-ttu-id="ddfb6-196">관리 인증서를 업로드하려면 [Azure Portal][Azure portal]을 사용하여 [여기](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate)의 단계에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-196">To upload a management certificate, follow the steps [here](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), using the [Azure portal][Azure portal].</span></span> <span data-ttu-id="ddfb6-197">Azure 관리 인증서에 대한 자세한 내용은 [Azure 인증서 개요](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-197">For more information about Azure management certificates, see the [Azure certificates overview](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="ddfb6-198">서비스 버스 네임스페이스에 대한 공유 액세스 권한 부여 규칙에 액세스하기 위한 끝점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-198">The endpoint for accessing shared access authorization rules on a Service Bus namespace is as follows:</span></span>

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

<span data-ttu-id="ddfb6-199">서비스 버스 네임 스페이스에서 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 개체를 만들려면 이 끝점에서 JSON 또는 XML로 직렬화된 규칙 정보를 사용하여 게시 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-199">To create a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a Service Bus namespace, execute a POST operation on this endpoint with the rule information serialized as JSON or XML.</span></span> <span data-ttu-id="ddfb6-200">예:</span><span class="sxs-lookup"><span data-stu-id="ddfb6-200">For example:</span></span>

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on the Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access the management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on the baseAddress above to create an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

<span data-ttu-id="ddfb6-201">마찬가지로 끝점에서 가져오기 작업을 사용하여 네임스페이스에 구성된 권한 부여 규칙을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-201">Similarly, use a GET operation on the endpoint to read the authorization rules configured on the namespace.</span></span>

<span data-ttu-id="ddfb6-202">특정 권한 부여 규칙을 업데이트하거나 삭제하려면 다음 끝점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-202">To update or delete a specific authorization rule, use the following endpoint:</span></span>

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a><span data-ttu-id="ddfb6-203">엔터티에 대한 공유 액세스 권한 부여 규칙 액세스</span><span class="sxs-lookup"><span data-stu-id="ddfb6-203">Access Shared Access Authorization rules on an entity</span></span>

<span data-ttu-id="ddfb6-204">해당하는 [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) 또는 [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription)에서 [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) 컬렉션을 통해 Service Bus 큐나 토픽에 구성된 [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 개체에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-204">You can access a [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object configured on a Service Bus queue or topic through the [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) collection in the corresponding [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) or [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).</span></span>

<span data-ttu-id="ddfb6-205">다음 코드는 큐에 대한 권한 부여 규칙을 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-205">The following code shows how to add authorization rules for a queue.</span></span>

```csharp
// Create an instance of NamespaceManager for the operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it to the queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it to the queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it to the queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create the queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a><span data-ttu-id="ddfb6-206">공유 액세스 서명 권한 부여 사용</span><span class="sxs-lookup"><span data-stu-id="ddfb6-206">Use Shared Access Signature authorization</span></span>

<span data-ttu-id="ddfb6-207">서비스 버스.NET 라이브러리로 Azure.NET SDK를 사용하는 응용 프로그램은 [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) 클래스를 통해 SAS 권한 부여를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-207">Applications using the Azure .NET SDK with the Service Bus .NET libraries can use SAS authorization through the [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) class.</span></span> <span data-ttu-id="ddfb6-208">다음 코드에서는 토큰 공급자를 사용하여 서비스 버스 큐에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-208">The following code illustrates the use of the token provider to send messages to a Service Bus queue.</span></span>

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message to queue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

<span data-ttu-id="ddfb6-209">또한 응용 프로그램은 연결 문자열을 수락하는 메서드에 SAS 연결 문자열을 사용하여 인증에 SAS을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-209">Applications can also use SAS for authentication by using a SAS connection string in methods that accept connection strings.</span></span>

<span data-ttu-id="ddfb6-210">서비스 버스 릴레이로 SAS 권한 부여를 사용하면 서비스 버스 네임 스페이스에 구성된 SAS 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-210">Note that to use SAS authorization with Service Bus relays, you can use SAS keys configured on the Service Bus namespace.</span></span> <span data-ttu-id="ddfb6-211">네임스페이스([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager)와 [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) 개체에 명시적으로 릴레이를 만들면 해당 릴레이 대한 SAS 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-211">If you explicitly create a relay on the namespace ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) with a [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) object, you can set the SAS rules just for that relay.</span></span> <span data-ttu-id="ddfb6-212">서비스 버스 구독으로 SAS 권한 부여를 사용하려면 서비스 버스 네임 스페이스 또는 항목에 구성된 SAS 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-212">To use SAS authorization with Service Bus subscriptions, you can use SAS keys configured on a Service Bus namespace or on a topic.</span></span>

## <a name="use-the-shared-access-signature-at-http-level"></a><span data-ttu-id="ddfb6-213">공유 액세스 서명 사용(HTTP 수준에서)</span><span class="sxs-lookup"><span data-stu-id="ddfb6-213">Use the Shared Access Signature (at HTTP level)</span></span>

<span data-ttu-id="ddfb6-214">서비스 버스의 모든 엔터티에 대해 공유 액세스 서명을 만드는 방법을 알았으므로 HTTP POST를 수행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-214">Now that you know how to create Shared Access Signatures for any entities in Service Bus, you are ready to perform an HTTP POST:</span></span>

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

<span data-ttu-id="ddfb6-215">이 방식은 모든 항목에 대해 작동한다는 것을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-215">Remember, this works for everything.</span></span> <span data-ttu-id="ddfb6-216">큐, 토픽, 구독에 대해 SAS를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-216">You can create SAS for a queue, topic, or subscription.</span></span> 

<span data-ttu-id="ddfb6-217">발신자 또는 클라이언트에게 SAS 토큰을 제공하면 직접 키를 가질 수 없으며 키를 얻기 위해 해시를 되돌릴 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-217">If you give a sender or client a SAS token, they don't have the key directly, and they cannot reverse the hash to obtain it.</span></span> <span data-ttu-id="ddfb6-218">예를 들어 사용자가 액세스할 수 있는 항목 및 액세스 기간을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-218">As such, you have control over what they can access, and for how long.</span></span> <span data-ttu-id="ddfb6-219">정책에서 기본 키를 다시 생성하거나 변경할 경우, 만든 공유 액세스 서명이 무효화되므로 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-219">An important thing to remember is that if you change the primary key in the policy, any Shared Access Signatures created from it will be invalidated.</span></span>

## <a name="use-the-shared-access-signature-at-amqp-level"></a><span data-ttu-id="ddfb6-220">공유 액세스 서명(AMQP 수준) 사용 </span><span class="sxs-lookup"><span data-stu-id="ddfb6-220">Use the Shared Access Signature (at AMQP level)</span></span>

<span data-ttu-id="ddfb6-221">이전 섹션에서는 HTTP POST 요청과 함께 SAS 토큰을 사용하여 데이터를 서비스 버스에 보내는 방법을 살펴봤습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-221">In the previous section, you saw how to use the SAS token with an HTTP POST request for sending data to the Service Bus.</span></span> <span data-ttu-id="ddfb6-222">아시다시피, 서비스 버스는 많은 시나리오에서 성능상의 이유로 사용하는 기본 설정 프로토콜인 AMQP(고급 메시지 큐 프로토콜)를 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-222">As you know, you can access Service Bus using the Advanced Message Queuing Protocol (AMQP) that is the preferred protocol to use for performance reasons, in many scenarios.</span></span> <span data-ttu-id="ddfb6-223">AMQP와 함께 SAS 토큰을 사용하는 방법은 2013년 이후 초안 상태이지만 현재 Azure에서 충분한 지원을 받고 있는 문서 [AMQP 클레임 기반 보안 버전 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) 에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-223">The SAS token usage with AMQP is described in the document [AMQP Claim-Based Security Version 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) that is in working draft since 2013 but well-supported by Azure today.</span></span>

<span data-ttu-id="ddfb6-224">Service Bus에 데이터의 전송을 시작하기 전에 게시자는 AMQP 메시지 안에 있는 SAS 토큰을 **$cbs**(모든 SAS 토큰을 얻고 유효성을 검사하기 위해 서비스에서 사용하는 "특별" 큐)라는 이름의 정의된 AMQP 노드에 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-224">Before starting to send data to Service Bus, the publisher must send the SAS token inside an AMQP message to a well-defined AMQP node named **$cbs** (you can see it as a "special" queue used by the service to acquire and validate all the SAS tokens).</span></span> <span data-ttu-id="ddfb6-225">게시자는 AMQP 메시지 내부에 있는 **ReplyTo** 필드를 지정해야 합니다. 이는 서비스가 토큰 유효성 검사 결과와 함께 게시자에게 응답하는 노드입니다(게시자와 서비스 간의 간단한 요청/응답 패턴).</span><span class="sxs-lookup"><span data-stu-id="ddfb6-225">The publisher must specify the **ReplyTo** field inside the AMQP message; this is the node in which the service replies to the publisher with the result of the token validation (a simple request/reply pattern between publisher and service).</span></span> <span data-ttu-id="ddfb6-226">이 회신 노드는 "즉시" 생성되며 AMQP 1.0 사양에 설명된 것처럼 “원격 노드 동적 생성”에 대해 얘기합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-226">This reply node is created "on the fly," speaking about "dynamic creation of remote node" as described by the AMQP 1.0 specification.</span></span> <span data-ttu-id="ddfb6-227">SAS 토큰이 유효한지 확인한 후 게시자는 이제 데이터를 서비스에 보내기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-227">After checking that the SAS token is valid, the publisher can go forward and start to send data to the service.</span></span>

<span data-ttu-id="ddfb6-228">다음 단계에서는 [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) 라이브러리를 사용하여 AMQP 프로토콜을 통해 SAS 토큰을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-228">The following steps show how to send the SAS token with AMQP protocol using the [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) library.</span></span> <span data-ttu-id="ddfb6-229">이 방법은 C\#으로 개발하는 공식적인 Service Bus SDK를 사용할 수 없는 경우(예를 들어 WinRT, .Net Compact Framework, .Net Micro Framework 및 Mono)에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-229">This is useful if you can't use the official Service Bus SDK (for example on WinRT, .Net Compact Framework, .Net Micro Framework and Mono) developing in C\#.</span></span> <span data-ttu-id="ddfb6-230">물론 이 라이브러리는 클레임 기반 보안이 HTTP 수준에서 작동하는 방식을 볼 때처럼 AMQP 수준에서 작동하는 방식을 이해하는 데 유용합니다("권한 부여" 헤더 내에서 전송되는 HTTP POST 요청 및 SAS 토큰과 함께).</span><span class="sxs-lookup"><span data-stu-id="ddfb6-230">Of course, this library is useful to help understand how claims-based security works at the AMQP level, as you saw how it works at the HTTP level (with an HTTP POST request and the SAS token sent inside the "Authorization" header).</span></span> <span data-ttu-id="ddfb6-231">AMQP에 대한 깊은 지식이 없어도 .Net Framework 응용 프로그램과 함께 공식 서비스 버스 SDK를 사용할 수 있습니다(위 참조).</span><span class="sxs-lookup"><span data-stu-id="ddfb6-231">If you don't need such deep knowledge about AMQP, you can use the official Service Bus SDK with .Net Framework applications, which will do it for you.</span></span>

### <a name="c35"></a><span data-ttu-id="ddfb6-232">C&#35;</span><span class="sxs-lookup"><span data-stu-id="ddfb6-232">C&#35;</span></span>

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) to send</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct the put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive the response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // the sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

<span data-ttu-id="ddfb6-233">위의 `PutCbsToken()` 메서드는 서비스에 대한 TCP 연결 및 전송할 SAS 토큰인 *sasToken* 매개 변수를 나타내는 *연결*([AMQP .NET Lite 라이브러리](https://github.com/Azure/amqpnetlite)에서 제공하는 대로 AMQP 연결 클래스 인스턴스)을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-233">The `PutCbsToken()` method receives the *connection* (AMQP connection class instance as provided by the [AMQP .NET Lite library](https://github.com/Azure/amqpnetlite)) that represents the TCP connection to the service and the *sasToken* parameter that is the SAS token to send.</span></span> 

> [!NOTE]
> <span data-ttu-id="ddfb6-234">연결이 **EXTERNAL로 설정된 SASL 인증 메커니즘** (SAS 토큰을 보낼 필요가 없을 때 사용하는 사용자 이름 및 암호를 가진 기본 PLAIN이 아님)으로 생성된다는 사실이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-234">It's important that the connection is created with **SASL authentication mechanism set to EXTERNAL** (and not the default PLAIN with username and password used when you don't need to send the SAS token).</span></span>
> 
> 

<span data-ttu-id="ddfb6-235">그런 다음 게시자는 SAS 토큰을 보내고 서비스로부터 회신(토큰 유효성 검사 결과)을 받기 위한 2개의 AMQP 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-235">Next, the publisher creates two AMQP links for sending the SAS token and receiving the reply (the token validation result) from the service.</span></span>

<span data-ttu-id="ddfb6-236">AMQP 메시지는 간단한 메시지보다 정보가 많고 속성이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-236">The AMQP message contains a set of properties, and more information than a simple message.</span></span> <span data-ttu-id="ddfb6-237">SAS 토큰은 해당 생성자를 사용하여 메시지의 본문으로 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-237">The SAS token is the body of the message (using its constructor).</span></span> <span data-ttu-id="ddfb6-238">**"ReplyTo"** 속성은 수신기 링크에 대한 유효성 검사 결과를 받기 위한 노드 이름으로 설정됩니다(원하는 대로 이름을 변경할 수 있으며 서비스에서 동적으로 생성함).</span><span class="sxs-lookup"><span data-stu-id="ddfb6-238">The **"ReplyTo"** property is set to the node name for receiving the validation result on the receiver link (you can change its name if you want, and it will be created dynamically by the service).</span></span> <span data-ttu-id="ddfb6-239">마지막 세 응용 프로그램/사용자 지정 속성은 서비스에서 실행하는 작업의 종류를 나타내는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-239">The last three application/custom properties are used by the service to indicate what kind of operation it has to execute.</span></span> <span data-ttu-id="ddfb6-240">CBS 초안 사양에서 설명한 것처럼 이들은 **토큰의 형식**(이 경우 "servicebus.windows.net:sastoken")인 **작업 이름**("put-token")이 되고 토큰이 적용되는 **청중의 "이름"**이어야 합니다(전체 엔터티).</span><span class="sxs-lookup"><span data-stu-id="ddfb6-240">As described by the CBS draft specification, they must be the **operation name** ("put-token"), the **type of token** (in this case, a "servicebus.windows.net:sastoken"), and the **"name" of the audience** to which the token applies (the entire entity).</span></span>

<span data-ttu-id="ddfb6-241">보낸 사람 링크에서 SAS 토큰을 보낸 후 게시자는 수신자 링크에서 회신을 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-241">After sending the SAS token on the sender link, the publisher must read the reply on the receiver link.</span></span> <span data-ttu-id="ddfb6-242">회신은 HTTP 상태 코드와 동일한 값을 포함할 수 있는 **"status-code"** 라는 이름의 응용 프로그램 속성을 가진 간단한 AMQP 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-242">The reply is a simple AMQP message with an application property named **"status-code"** that can contain the same values as an HTTP status code.</span></span>

## <a name="rights-required-for-service-bus-operations"></a><span data-ttu-id="ddfb6-243">서비스 버스 작업에 필요한 권한</span><span class="sxs-lookup"><span data-stu-id="ddfb6-243">Rights required for Service Bus operations</span></span>

<span data-ttu-id="ddfb6-244">다음 테이블에서는 서비스 버스 리소스의 다양한 작업에 필요한 액세스 권한을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-244">The following table shows the access rights required for various operations on Service Bus resources.</span></span>

| <span data-ttu-id="ddfb6-245">작업</span><span class="sxs-lookup"><span data-stu-id="ddfb6-245">Operation</span></span> | <span data-ttu-id="ddfb6-246">필요한 클레임</span><span class="sxs-lookup"><span data-stu-id="ddfb6-246">Claim Required</span></span> | <span data-ttu-id="ddfb6-247">클레임 범위</span><span class="sxs-lookup"><span data-stu-id="ddfb6-247">Claim Scope</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ddfb6-248">**네임스페이스**</span><span class="sxs-lookup"><span data-stu-id="ddfb6-248">**Namespace**</span></span> | | |
| <span data-ttu-id="ddfb6-249">네임스페이스에서 권한 부여 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="ddfb6-249">Configure authorization rule on a namespace</span></span> |<span data-ttu-id="ddfb6-250">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-250">Manage</span></span> |<span data-ttu-id="ddfb6-251">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-251">Any namespace address</span></span> |
| <span data-ttu-id="ddfb6-252">**서비스 레지스트리**</span><span class="sxs-lookup"><span data-stu-id="ddfb6-252">**Service Registry**</span></span> | | |
| <span data-ttu-id="ddfb6-253">개인 정책 열거</span><span class="sxs-lookup"><span data-stu-id="ddfb6-253">Enumerate Private Policies</span></span> |<span data-ttu-id="ddfb6-254">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-254">Manage</span></span> |<span data-ttu-id="ddfb6-255">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-255">Any namespace address</span></span> |
| <span data-ttu-id="ddfb6-256">네임스페이스에서 수신 시작</span><span class="sxs-lookup"><span data-stu-id="ddfb6-256">Begin listening on a namespace</span></span> |<span data-ttu-id="ddfb6-257">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-257">Listen</span></span> |<span data-ttu-id="ddfb6-258">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-258">Any namespace address</span></span> |
| <span data-ttu-id="ddfb6-259">네임스페이스에서 수신기로 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-259">Send messages to a listener at a namespace</span></span> |<span data-ttu-id="ddfb6-260">보내기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-260">Send</span></span> |<span data-ttu-id="ddfb6-261">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-261">Any namespace address</span></span> |
| <span data-ttu-id="ddfb6-262">**큐**</span><span class="sxs-lookup"><span data-stu-id="ddfb6-262">**Queue**</span></span> | | |
| <span data-ttu-id="ddfb6-263">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-263">Create a queue</span></span> |<span data-ttu-id="ddfb6-264">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-264">Manage</span></span> |<span data-ttu-id="ddfb6-265">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-265">Any namespace address</span></span> |
| <span data-ttu-id="ddfb6-266">큐 삭제</span><span class="sxs-lookup"><span data-stu-id="ddfb6-266">Delete a queue</span></span> |<span data-ttu-id="ddfb6-267">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-267">Manage</span></span> |<span data-ttu-id="ddfb6-268">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-268">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-269">큐 열거</span><span class="sxs-lookup"><span data-stu-id="ddfb6-269">Enumerate queues</span></span> |<span data-ttu-id="ddfb6-270">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-270">Manage</span></span> |<span data-ttu-id="ddfb6-271">/$Resources/Queues</span><span class="sxs-lookup"><span data-stu-id="ddfb6-271">/$Resources/Queues</span></span> |
| <span data-ttu-id="ddfb6-272">큐 설명 가져오기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-272">Get the queue description</span></span> |<span data-ttu-id="ddfb6-273">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-273">Manage</span></span> |<span data-ttu-id="ddfb6-274">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-274">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-275">큐에서 권한 부여 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="ddfb6-275">Configure authorization rule for a queue</span></span> |<span data-ttu-id="ddfb6-276">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-276">Manage</span></span> |<span data-ttu-id="ddfb6-277">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-277">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-278">큐로 보내기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-278">Send into to the queue</span></span> |<span data-ttu-id="ddfb6-279">보내기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-279">Send</span></span> |<span data-ttu-id="ddfb6-280">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-280">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-281">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-281">Receive messages from a queue</span></span> |<span data-ttu-id="ddfb6-282">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-282">Listen</span></span> |<span data-ttu-id="ddfb6-283">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-283">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-284">메시지 보기-잠금 모드에서 메시지를 받은 후에 중단 또는 완료</span><span class="sxs-lookup"><span data-stu-id="ddfb6-284">Abandon or complete messages after receiving the message in peek-lock mode</span></span> |<span data-ttu-id="ddfb6-285">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-285">Listen</span></span> |<span data-ttu-id="ddfb6-286">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-286">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-287">나중에 검색에 대한 메시지 연기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-287">Defer a message for later retrieval</span></span> |<span data-ttu-id="ddfb6-288">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-288">Listen</span></span> |<span data-ttu-id="ddfb6-289">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-289">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-290">메시지 효력 상실</span><span class="sxs-lookup"><span data-stu-id="ddfb6-290">Deadletter a message</span></span> |<span data-ttu-id="ddfb6-291">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-291">Listen</span></span> |<span data-ttu-id="ddfb6-292">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-292">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-293">메시지 큐 세션을 사용하여 연결된 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-293">Get the state associated with a message queue session</span></span> |<span data-ttu-id="ddfb6-294">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-294">Listen</span></span> |<span data-ttu-id="ddfb6-295">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-295">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-296">메시지 큐 세션을 사용하여 연결된 상태 설정</span><span class="sxs-lookup"><span data-stu-id="ddfb6-296">Set the state associated with a message queue session</span></span> |<span data-ttu-id="ddfb6-297">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-297">Listen</span></span> |<span data-ttu-id="ddfb6-298">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-298">Any valid queue address</span></span> |
| <span data-ttu-id="ddfb6-299">**항목**</span><span class="sxs-lookup"><span data-stu-id="ddfb6-299">**Topic**</span></span> | | |
| <span data-ttu-id="ddfb6-300">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-300">Create a topic</span></span> |<span data-ttu-id="ddfb6-301">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-301">Manage</span></span> |<span data-ttu-id="ddfb6-302">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-302">Any namespace address</span></span> |
| <span data-ttu-id="ddfb6-303">항목 삭제</span><span class="sxs-lookup"><span data-stu-id="ddfb6-303">Delete a topic</span></span> |<span data-ttu-id="ddfb6-304">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-304">Manage</span></span> |<span data-ttu-id="ddfb6-305">유효한 항목 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-305">Any valid topic address</span></span> |
| <span data-ttu-id="ddfb6-306">항목 열거</span><span class="sxs-lookup"><span data-stu-id="ddfb6-306">Enumerate topics</span></span> |<span data-ttu-id="ddfb6-307">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-307">Manage</span></span> |<span data-ttu-id="ddfb6-308">/$Resources/Topics</span><span class="sxs-lookup"><span data-stu-id="ddfb6-308">/$Resources/Topics</span></span> |
| <span data-ttu-id="ddfb6-309">항목 설명 가져오기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-309">Get the topic description</span></span> |<span data-ttu-id="ddfb6-310">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-310">Manage</span></span> |<span data-ttu-id="ddfb6-311">유효한 항목 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-311">Any valid topic address</span></span> |
| <span data-ttu-id="ddfb6-312">항목에서 권한 부여 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="ddfb6-312">Configure authorization rule for a topic</span></span> |<span data-ttu-id="ddfb6-313">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-313">Manage</span></span> |<span data-ttu-id="ddfb6-314">유효한 항목 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-314">Any valid topic address</span></span> |
| <span data-ttu-id="ddfb6-315">항목으로 보내기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-315">Send to the topic</span></span> |<span data-ttu-id="ddfb6-316">보내기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-316">Send</span></span> |<span data-ttu-id="ddfb6-317">유효한 항목 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-317">Any valid topic address</span></span> |
| <span data-ttu-id="ddfb6-318">**구독**</span><span class="sxs-lookup"><span data-stu-id="ddfb6-318">**Subscription**</span></span> | | |
| <span data-ttu-id="ddfb6-319">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-319">Create a subscription</span></span> |<span data-ttu-id="ddfb6-320">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-320">Manage</span></span> |<span data-ttu-id="ddfb6-321">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="ddfb6-321">Any namespace address</span></span> |
| <span data-ttu-id="ddfb6-322">구독 삭제</span><span class="sxs-lookup"><span data-stu-id="ddfb6-322">Delete subscription</span></span> |<span data-ttu-id="ddfb6-323">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-323">Manage</span></span> |<span data-ttu-id="ddfb6-324">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-324">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-325">구독 열거</span><span class="sxs-lookup"><span data-stu-id="ddfb6-325">Enumerate subscriptions</span></span> |<span data-ttu-id="ddfb6-326">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-326">Manage</span></span> |<span data-ttu-id="ddfb6-327">../myTopic/Subscriptions</span><span class="sxs-lookup"><span data-stu-id="ddfb6-327">../myTopic/Subscriptions</span></span> |
| <span data-ttu-id="ddfb6-328">구독 설명 가져오기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-328">Get subscription description</span></span> |<span data-ttu-id="ddfb6-329">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-329">Manage</span></span> |<span data-ttu-id="ddfb6-330">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-330">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-331">메시지 보기-잠금 모드에서 메시지를 받은 후에 중단 또는 완료</span><span class="sxs-lookup"><span data-stu-id="ddfb6-331">Abandon or complete messages after receiving the message in peek-lock mode</span></span> |<span data-ttu-id="ddfb6-332">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-332">Listen</span></span> |<span data-ttu-id="ddfb6-333">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-333">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-334">나중에 검색에 대한 메시지 연기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-334">Defer a message for later retrieval</span></span> |<span data-ttu-id="ddfb6-335">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-335">Listen</span></span> |<span data-ttu-id="ddfb6-336">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-336">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-337">메시지 효력 상실</span><span class="sxs-lookup"><span data-stu-id="ddfb6-337">Deadletter a message</span></span> |<span data-ttu-id="ddfb6-338">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-338">Listen</span></span> |<span data-ttu-id="ddfb6-339">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-339">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-340">항목 세션을 사용하여 연결된 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-340">Get the state associated with a topic session</span></span> |<span data-ttu-id="ddfb6-341">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-341">Listen</span></span> |<span data-ttu-id="ddfb6-342">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-342">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-343">항목 세션을 사용하여 연결된 상태 설정</span><span class="sxs-lookup"><span data-stu-id="ddfb6-343">Set the state associated with a topic session</span></span> |<span data-ttu-id="ddfb6-344">수신 대기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-344">Listen</span></span> |<span data-ttu-id="ddfb6-345">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-345">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-346">**규칙**</span><span class="sxs-lookup"><span data-stu-id="ddfb6-346">**Rules**</span></span> | | |
| <span data-ttu-id="ddfb6-347">규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="ddfb6-347">Create a rule</span></span> |<span data-ttu-id="ddfb6-348">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-348">Manage</span></span> |<span data-ttu-id="ddfb6-349">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-349">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-350">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="ddfb6-350">Delete a rule</span></span> |<span data-ttu-id="ddfb6-351">관리</span><span class="sxs-lookup"><span data-stu-id="ddfb6-351">Manage</span></span> |<span data-ttu-id="ddfb6-352">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="ddfb6-352">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="ddfb6-353">규칙 열거</span><span class="sxs-lookup"><span data-stu-id="ddfb6-353">Enumerate rules</span></span> |<span data-ttu-id="ddfb6-354">관리 또는 수신</span><span class="sxs-lookup"><span data-stu-id="ddfb6-354">Manage or Listen</span></span> |<span data-ttu-id="ddfb6-355">../myTopic/Subscriptions/mySubscription/Rules</span><span class="sxs-lookup"><span data-stu-id="ddfb6-355">../myTopic/Subscriptions/mySubscription/Rules</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ddfb6-356">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddfb6-356">Next steps</span></span>

<span data-ttu-id="ddfb6-357">Service Bus 메시징에 대해 자세히 알아보려면 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ddfb6-357">To learn more about Service Bus messaging, see the following topics.</span></span>

* [<span data-ttu-id="ddfb6-358">서비스 버스 기본 사항</span><span class="sxs-lookup"><span data-stu-id="ddfb6-358">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="ddfb6-359">Service Bus 큐, 토픽 및 구독</span><span class="sxs-lookup"><span data-stu-id="ddfb6-359">Service Bus queues, topics, and subscriptions</span></span>](service-bus-queues-topics-subscriptions.md)
* [<span data-ttu-id="ddfb6-360">서비스 버스 큐를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="ddfb6-360">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="ddfb6-361">Service Bus 토픽 및 구독을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="ddfb6-361">How to use Service Bus topics and subscriptions</span></span>](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com