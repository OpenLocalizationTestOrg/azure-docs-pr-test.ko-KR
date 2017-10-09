---
title: "공유 액세스 서명으로 서비스 버스 인증 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a><span data-ttu-id="5fbee-103">공유 액세스 서명을 사용한 Service Bus 인증</span><span class="sxs-lookup"><span data-stu-id="5fbee-103">Service Bus authentication with Shared Access Signatures</span></span>

<span data-ttu-id="5fbee-104">*공유 액세스 서명을* (SAS)는 서비스 버스 메시징에 대 한 hello 기본 보안 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-104">*Shared Access Signatures* (SAS) are hello primary security mechanism for Service Bus messaging.</span></span> <span data-ttu-id="5fbee-105">이 문서에서는 SAS을 설명 하 고 작동 하는 방법 toouse 플랫폼 제약 없는 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-105">This article discusses SAS, how they work, and how toouse them in a platform-agnostic way.</span></span>

<span data-ttu-id="5fbee-106">SAS 인증을 사용 하면 응용 프로그램 tooauthenticate tooService hello 네임 스페이스 또는 메시징 엔터티 (큐 또는 항목)는 특정 권한이 연결 된 hello 구성 된 선택 키를 사용 하 여 버스입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-106">SAS authentication enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="5fbee-107">그런 다음이 키 toogenerate 클라이언트 tooauthenticate tooService 버스에 사용할 수 있는 SAS 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-107">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="5fbee-108">SAS 인증 지원은 Azure SDK 버전 2.0 이상 hello에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-108">SAS authentication support is included in hello Azure SDK version 2.0 and later.</span></span>

## <a name="overview-of-sas"></a><span data-ttu-id="5fbee-109">SAS 개요</span><span class="sxs-lookup"><span data-stu-id="5fbee-109">Overview of SAS</span></span>

<span data-ttu-id="5fbee-110">공유 액세스 서명은 SHA-256 보안 해시 또는 URI에 따른 인증 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-110">Shared Access Signatures are an authentication mechanism based on SHA-256 secure hashes or URIs.</span></span> <span data-ttu-id="5fbee-111">SAS는 모든 서비스 버스 서비스에서 사용되는 매우 강력한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-111">SAS is an extremely powerful mechanism that is used by all Service Bus services.</span></span> <span data-ttu-id="5fbee-112">실제 사용 시, SAS에는 *공유 액세스 정책*과 *공유 액세스 서명*(*토큰*이라고 부름)의 두 구성 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-112">In actual use, SAS has two components: a *shared access policy* and a *Shared Access Signature* (often called a *token*).</span></span>

<span data-ttu-id="5fbee-113">SAS 인증 서비스 버스에 연결 된 권한으로 서비스 버스 리소스에 대 한 암호화 키 hello 구성을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-113">SAS authentication in Service Bus involves hello configuration of a cryptographic key with associated rights on a Service Bus resource.</span></span> <span data-ttu-id="5fbee-114">클라이언트 클레임 tooService 버스 리소스에 액세스 한 SAS 토큰을 제공 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-114">Clients claim access tooService Bus resources by presenting a SAS token.</span></span> <span data-ttu-id="5fbee-115">이 토큰 hello 액세스할 리소스 URI, 구성 되며 hello로 서명 된 expiry 키를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-115">This token consists of hello resource URI being accessed, and an expiry signed with hello configured key.</span></span>

<span data-ttu-id="5fbee-116">Service Bus [릴레이](service-bus-fundamentals-hybrid-solutions.md#relays), [큐](service-bus-fundamentals-hybrid-solutions.md#queues) 및 [토픽](service-bus-fundamentals-hybrid-solutions.md#topics)에 대해 공유 액세스 서명 권한 부여 규칙을 구성할 수 있습니다 </span><span class="sxs-lookup"><span data-stu-id="5fbee-116">You can configure Shared Access Signature authorization rules on Service Bus [relays](service-bus-fundamentals-hybrid-solutions.md#relays), [queues](service-bus-fundamentals-hybrid-solutions.md#queues), and [topics](service-bus-fundamentals-hybrid-solutions.md#topics).</span></span>

<span data-ttu-id="5fbee-117">SAS 인증 요소 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-117">SAS authentication uses hello following elements:</span></span>

* <span data-ttu-id="5fbee-118">[공유 액세스 권한 부여 규칙](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): Base64 표현에서 256비트 기본 암호화 키, 선택적 보조키 및 키 이름과 관련된 권한입니다(*수신*, *보내기* 또는 *관리* 권한의 컬렉션).</span><span class="sxs-lookup"><span data-stu-id="5fbee-118">[Shared Access authorization rule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): A 256-bit primary cryptographic key in Base64 representation, an optional secondary key, and a key name and associated rights (a collection of *Listen*, *Send*, or *Manage* rights).</span></span>
* <span data-ttu-id="5fbee-119">[공유 액세스 서명](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) 토큰: hello에 액세스 하는 hello 리소스의 URI로 구성 된 리소스 문자열의 hmac-sha256 hello와 expiry로 hello 암호화 키로 사용 하 여 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-119">[Shared Access Signature](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) token: Generated using hello HMAC-SHA256 of a resource string, consisting of hello URI of hello resource that is accessed and an expiry, with hello cryptographic key.</span></span> <span data-ttu-id="5fbee-120">hello 서명 및 hello 다음 섹션에에서 설명 된 기타 요소가 문자열 tooform hello SAS 토큰에 형식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-120">hello signature and other elements described in hello following sections are formatted into a string tooform hello SAS token.</span></span>

## <a name="shared-access-policy"></a><span data-ttu-id="5fbee-121">공유 액세스 정책</span><span class="sxs-lookup"><span data-stu-id="5fbee-121">Shared access policy</span></span>

<span data-ttu-id="5fbee-122">SAS에 대 한 중요 한 사항은 toounderstand는 정책과 시작 됨입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-122">An important thing toounderstand about SAS is that it starts with a policy.</span></span> <span data-ttu-id="5fbee-123">각각의 정책에 대해 **이름**, **범위** 및 **권한** 등, 3가지 정보를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-123">For each policy, you decide on three pieces of information: **name**, **scope**, and **permissions**.</span></span> <span data-ttu-id="5fbee-124">hello **이름** 해당;은 해당 범위 내에서 고유한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-124">hello **name** is just that; a unique name within that scope.</span></span> <span data-ttu-id="5fbee-125">hello 범위는 아주 쉽게: 문제의 hello 리소스의 URI hello의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-125">hello scope is easy enough: it's hello URI of hello resource in question.</span></span> <span data-ttu-id="5fbee-126">서비스 버스 네임 스페이스에 대 한 hello 범위가 hello 정규화 된 도메인 이름 (FQDN)와 같은 `https://<yournamespace>.servicebus.windows.net/`합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-126">For a Service Bus namespace, hello scope is hello fully qualified domain name (FQDN), such as `https://<yournamespace>.servicebus.windows.net/`.</span></span>

<span data-ttu-id="5fbee-127">hello 사용할 수 있는 정책에 대 한 권한은 주로 자체 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-127">hello available permissions for a policy are largely self-explanatory:</span></span>

* <span data-ttu-id="5fbee-128">보내기</span><span class="sxs-lookup"><span data-stu-id="5fbee-128">Send</span></span>
* <span data-ttu-id="5fbee-129">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-129">Listen</span></span>
* <span data-ttu-id="5fbee-130">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-130">Manage</span></span>

<span data-ttu-id="5fbee-131">Hello 정책을 만든 후 할당 한 *기본 키* 및 *보조 키*합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-131">After you create hello policy, it is assigned a *Primary Key* and a *Secondary Key*.</span></span> <span data-ttu-id="5fbee-132">이들은 강력한 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-132">These are cryptographically strong keys.</span></span> <span data-ttu-id="5fbee-133">항상 hello에 사용할 수-변경 내용이 손실 하지 않거나 해당 누출 [Azure 포털][Azure portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-133">Don't lose them or leak them - they'll always be available in hello [Azure portal][Azure portal].</span></span> <span data-ttu-id="5fbee-134">생성 된 hello 키 중 하나를 사용 하 고 언제 든 지 생성 하려면.</span><span class="sxs-lookup"><span data-stu-id="5fbee-134">You can use either of hello generated keys, and you can regenerate them at any time.</span></span> <span data-ttu-id="5fbee-135">그러나를 다시 생성 하거나 hello hello 정책에 기본 키를 변경 하는 경우 여기에서 만든 모든 공유 액세스 서명에 유효 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-135">However, if you regenerate or change hello primary key in hello policy, any Shared Access Signatures created from it will be invalidated.</span></span>

<span data-ttu-id="5fbee-136">서비스 버스 네임 스페이스를 만들 때 정책을 자동으로 만들어집니다 라는 hello 전체 네임 스페이스 **RootManageSharedAccessKey**,이 정책은 모든 사용 권한을 갖게 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-136">When you create a Service Bus namespace, a policy is automatically created for hello entire namespace called **RootManageSharedAccessKey**, and this policy has all permissions.</span></span> <span data-ttu-id="5fbee-137">**root**로 로그온하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-137">You don't log on as **root**, so don't use this policy unless there's a really good reason.</span></span> <span data-ttu-id="5fbee-138">Hello에서 정책을 추가로 만들 수 있습니다 **구성** hello 포털에서 hello 네임 스페이스에 대 한 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-138">You can create additional policies in hello **Configure** tab for hello namespace in hello portal.</span></span> <span data-ttu-id="5fbee-139">서비스 버스 (네임 스페이스, 큐 등)의 단일 트리 수준 too12 연결 된 정책은 tooit를 하나만 사용할 수 있는 중요 한 toonote 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-139">It's important toonote that a single tree level in Service Bus (namespace, queue, etc.) can only have up too12 policies attached tooit.</span></span>

## <a name="configuration-for-shared-access-signature-authentication"></a><span data-ttu-id="5fbee-140">공유 액세스 서명 인증을 위한 구성</span><span class="sxs-lookup"><span data-stu-id="5fbee-140">Configuration for Shared Access Signature authentication</span></span>
<span data-ttu-id="5fbee-141">Hello를 구성할 수 있습니다 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 서비스 버스 네임 스페이스, 큐 또는 항목에는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-141">You can configure hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) rule on Service Bus namespaces, queues, or topics.</span></span> <span data-ttu-id="5fbee-142">구성 된 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 서비스 버스 구독은 현재 지원 되지 않지만 toosecure 액세스 toosubscriptions 네임 스페이스 또는 항목에 구성 된 규칙을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-142">Configuring a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) on a Service Bus subscription is currently not supported, but you can use rules configured on a namespace or topic toosecure access toosubscriptions.</span></span> <span data-ttu-id="5fbee-143">이 절차를 설명 하는 작업 예제에 대 한 참조 hello [공유 액세스 서명 (SAS)를 사용 하 여 인증 서비스 버스 구독을](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) 샘플.</span><span class="sxs-lookup"><span data-stu-id="5fbee-143">For a working sample that illustrates this procedure, see hello [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) sample.</span></span>

<span data-ttu-id="5fbee-144">이러한 규칙을 서비스 버스 네임 스페이스, 큐 또는 항목에서 최대 12개까지 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-144">A maximum of 12 such rules can be configured on a Service Bus namespace, queue, or topic.</span></span> <span data-ttu-id="5fbee-145">서비스 버스 네임 스페이스에 구성 된 규칙에는 해당 네임 스페이스의 tooall 엔터티에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-145">Rules that are configured on a Service Bus namespace apply tooall entities in that namespace.</span></span>

![SAS](./media/service-bus-sas/service-bus-namespace.png)

<span data-ttu-id="5fbee-147">이 그림에서는 hello *manageRuleNS*, *sendRuleNS*, 및 *listenRuleNS* 권한 부여 규칙 tooboth 큐 Q1 및 항목 t 1 적용 하는 동안 *listenRuleQ*  및 *sendRuleQ* tooqueue q 1을 적용 하 고 *sendRuleT* tootopic T1만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-147">In this figure, hello *manageRuleNS*, *sendRuleNS*, and *listenRuleNS* authorization rules apply tooboth queue Q1 and topic T1, while *listenRuleQ* and *sendRuleQ* apply only tooqueue Q1 and *sendRuleT* applies only tootopic T1.</span></span>

<span data-ttu-id="5fbee-148">키 매개 변수를 hello는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-148">hello key parameters of a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) are as follows:</span></span>

| <span data-ttu-id="5fbee-149">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5fbee-149">Parameter</span></span> | <span data-ttu-id="5fbee-150">설명</span><span class="sxs-lookup"><span data-stu-id="5fbee-150">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5fbee-151">*KeyName*</span><span class="sxs-lookup"><span data-stu-id="5fbee-151">*KeyName*</span></span> |<span data-ttu-id="5fbee-152">Hello 권한 부여 규칙을 설명 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-152">A string that describes hello authorization rule.</span></span> |
| <span data-ttu-id="5fbee-153">*PrimaryKey*</span><span class="sxs-lookup"><span data-stu-id="5fbee-153">*PrimaryKey*</span></span> |<span data-ttu-id="5fbee-154">Base64 인코딩 256 비트 기본 키 서명 및 hello SAS 토큰 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-154">A base64-encoded 256-bit primary key for signing and validating hello SAS token.</span></span> |
| <span data-ttu-id="5fbee-155">*SecondaryKey*</span><span class="sxs-lookup"><span data-stu-id="5fbee-155">*SecondaryKey*</span></span> |<span data-ttu-id="5fbee-156">base64 인코딩 256 비트 보조 키를 서명 하 고 hello SAS 토큰 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-156">A base64-encoded 256-bit secondary key for signing and validating hello SAS token.</span></span> |
| <span data-ttu-id="5fbee-157">*AccessRights*</span><span class="sxs-lookup"><span data-stu-id="5fbee-157">*AccessRights*</span></span> |<span data-ttu-id="5fbee-158">Hello 권한 부여 규칙에서 허용 된 액세스 권한의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-158">A list of access rights granted by hello authorization rule.</span></span> <span data-ttu-id="5fbee-159">이러한 권한은 수신, 보내기 및 관리 권한의 컬렉션일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-159">These rights can be any collection of Listen, Send, and Manage rights.</span></span> |

<span data-ttu-id="5fbee-160">서비스 버스 네임 스페이스를 프로 비전 하는 경우는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)와 [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) 도**RootManageSharedAccessKey**, 기본적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-160">When a Service Bus namespace is provisioned, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), with [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) set too**RootManageSharedAccessKey**, is created by default.</span></span>

## <a name="generate-a-shared-access-signature-token"></a><span data-ttu-id="5fbee-161">공유 액세스 서명(토큰) 생성</span><span class="sxs-lookup"><span data-stu-id="5fbee-161">Generate a Shared Access Signature (token)</span></span>

<span data-ttu-id="5fbee-162">hello 정책 자체 서비스 버스에 대 한 액세스 토큰 hello 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-162">hello policy itself is not hello access token for Service Bus.</span></span> <span data-ttu-id="5fbee-163">Hello는 hello에서 액세스 토큰 생성 된 개체-hello 기본 또는 보조 키 중 하나를 사용 하는</span><span class="sxs-lookup"><span data-stu-id="5fbee-163">It is hello object from which hello access token is generated - using either hello primary or secondary key.</span></span> <span data-ttu-id="5fbee-164">서명 hello 공유 액세스 권한 부여 규칙에 지정 된 키 액세스 toohello 있는 클라이언트는 hello SAS 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-164">Any client that has access toohello signing keys specified in hello shared access authorization rule can generate hello SAS token.</span></span> <span data-ttu-id="5fbee-165">hello 토큰 형식에 따라 hello에 문자열을 만들어 신중 하 게 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-165">hello token is generated by carefully crafting a string in hello following format:</span></span>

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

<span data-ttu-id="5fbee-166">여기서 `signature-string` 는 hello 토큰의 hello 범위의 hello sha-256 해시 (**범위** hello 이전 섹션에 설명 된 대로) 추가 CRLF 및 만료 시간 (hello epoch 이후의 초: `00:00:00 UTC` 1970 년 1 월 1에).</span><span class="sxs-lookup"><span data-stu-id="5fbee-166">Where `signature-string` is hello SHA-256 hash of hello scope of hello token (**scope** as described in hello previous section) with a CRLF appended and an expiry time (in seconds since hello epoch: `00:00:00 UTC` on 1 January 1970).</span></span> 

> [!NOTE]
> <span data-ttu-id="5fbee-167">tooavoid 짧은 토큰 만료 시간 것이 좋습니다 이상는 32 비트 부호 없는 정수 (64 비트) long 정수 또는 가급적 hello 만료 시간 값을 인코딩하는.</span><span class="sxs-lookup"><span data-stu-id="5fbee-167">tooavoid a short token expiry time, it is recommended that you encode hello expiry time value as at least a 32-bit unsigned integer, or preferably a long (64-bit) integer.</span></span>  
> 
> 

<span data-ttu-id="5fbee-168">hello 해시 의사 코드 다음 비슷한 toohello 찾아서 32 바이트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-168">hello hash looks similar toohello following pseudo code and returns 32 bytes.</span></span>

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

<span data-ttu-id="5fbee-169">hello에 hello 해시 되지 않은 값은 **SharedAccessSignature** hello 받는 사람을 계산할 수 hello 해시에서 동일한 매개 변수를 반환 하는지 있는지 toobe hello로 동일한 결과 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-169">hello non-hashed values are in hello **SharedAccessSignature** string so that hello recipient can compute hello hash with hello same parameters, toobe sure that it returns hello same result.</span></span> <span data-ttu-id="5fbee-170">hello URI hello 범위를 지정 하 고 hello 키 이름 hello 정책 사용 toobe toocompute hello 해시를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-170">hello URI specifies hello scope, and hello key name identifies hello policy toobe used toocompute hello hash.</span></span> <span data-ttu-id="5fbee-171">이것은 보안의 관점에서 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-171">This is important from a security standpoint.</span></span> <span data-ttu-id="5fbee-172">Hello 서명이 있는 hello 받는 사람 (서비스 버스)을 계산 하는 일치 하지 않습니다, 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-172">If hello signature doesn't match that which hello recipient (Service Bus) calculates, then access is denied.</span></span> <span data-ttu-id="5fbee-173">이 시점에서 있는지 hello 발신자 액세스 toohello 키를 가지 며 hello 정책에 지정 된 hello 권한을 부여 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-173">At this point you can be sure that hello sender had access toohello key and should be granted hello rights specified in hello policy.</span></span>

<span data-ttu-id="5fbee-174">Hello를 사용 해야 하는이 작업에 대 한 리소스 URI 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-174">Note that you should use hello encoded resource URI for this operation.</span></span> <span data-ttu-id="5fbee-175">hello 리소스 URI는 서비스 버스 리소스 toowhich 액세스 hello의 전체 URI를 요청 하는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-175">hello resource URI is hello full URI of hello Service Bus resource toowhich access is claimed.</span></span> <span data-ttu-id="5fbee-176">예를 들면 `http://<namespace>.servicebus.windows.net/<entityPath>` 또는 `sb://<namespace>.servicebus.windows.net/<entityPath>`입니다. 즉, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-176">For example, `http://<namespace>.servicebus.windows.net/<entityPath>` or `sb://<namespace>.servicebus.windows.net/<entityPath>`; that is, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.</span></span>

<span data-ttu-id="5fbee-177">이 URI 또는 계층 구조 부모 중 하나를 지정 하는 hello 엔터티에서 hello 서명에 사용 되는 공유 액세스 권한 부여 규칙 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-177">hello shared access authorization rule used for signing must be configured on hello entity specified by this URI, or by one of its hierarchical parents.</span></span> <span data-ttu-id="5fbee-178">예를 들어 `http://contoso.servicebus.windows.net/contosoTopics/T1` 또는 `http://contoso.servicebus.windows.net` hello 이전 예제에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-178">For example, `http://contoso.servicebus.windows.net/contosoTopics/T1` or `http://contoso.servicebus.windows.net` in hello previous example.</span></span>

<span data-ttu-id="5fbee-179">SAS 토큰은 hello에서 모든 리소스에 대 한 유효 `<resourceURI>` hello에 사용 된 `signature-string`합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-179">A SAS token is valid for all resources under hello `<resourceURI>` used in hello `signature-string`.</span></span>

<span data-ttu-id="5fbee-180">hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) hello SAS 토큰 의미 toohello **keyName** 공유 액세스 권한 부여 규칙의 hello toogenerate hello 토큰을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-180">hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) in hello SAS token refers toohello **keyName** of hello shared access authorization rule used toogenerate hello token.</span></span>

<span data-ttu-id="5fbee-181">hello *URL로 인코딩된 resourceURI* hello hello 서명의 hello 계산 하는 동안 hello 서명할 문자열에에서 사용 되는 URI와 동일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-181">hello *URL-encoded-resourceURI* must be hello same as hello URI used in hello string-to-sign during hello computation of hello signature.</span></span> <span data-ttu-id="5fbee-182">[%로 인코딩](https://msdn.microsoft.com/library/4fkewx0t.aspx)되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-182">It should be [percent-encoded](https://msdn.microsoft.com/library/4fkewx0t.aspx).</span></span>

<span data-ttu-id="5fbee-183">주기적으로 다시 생성 하는 hello 키 hello에 사용 되는 것이 좋습니다. [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-183">It is recommended that you periodically regenerate hello keys used in hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object.</span></span> <span data-ttu-id="5fbee-184">응용 프로그램에서 일반적으로 hello를 사용 해야 [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate SAS 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-184">Applications should generally use hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate a SAS token.</span></span> <span data-ttu-id="5fbee-185">Hello 바꿔야 hello 키를 다시 생성할 때는 [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) hello 이전 기본으로 키를 새 기본 키 hello로 새 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-185">When regenerating hello keys, you should replace hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) with hello old primary key, and generate a new key as hello new primary key.</span></span> <span data-ttu-id="5fbee-186">이렇게 하면 이전 기본 키 hello로 가져가기는 아직 만료 되지 않은 및 권한 부여에 대 한 토큰을 사용 하 여 toocontinue 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-186">This enables you toocontinue using tokens for authorization that were issued with hello old primary key, and that have not yet expired.</span></span>

<span data-ttu-id="5fbee-187">두 hello를 다시 생성할 수는 키가 손상 된 경우 toorevoke hello 키를 있으면 [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) 및 hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) 의 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), 새 키로 대체 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-187">If a key is compromised and you have toorevoke hello keys, you can regenerate both hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) and hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) of a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), replacing them with new keys.</span></span> <span data-ttu-id="5fbee-188">이 절차는 hello 이전 키로 서명한 모든 토큰이 무효화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-188">This procedure invalidates all tokens signed with hello old keys.</span></span>

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a><span data-ttu-id="5fbee-189">어떻게 서비스 버스에 toouse 공유 액세스 서명 인증</span><span class="sxs-lookup"><span data-stu-id="5fbee-189">How toouse Shared Access Signature authentication with Service Bus</span></span>

<span data-ttu-id="5fbee-190">다음 시나리오는 hello SAS 토큰 및 클라이언트 권한 부여를 생성, 권한 부여 규칙의 구성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-190">hello following scenarios include configuration of authorization rules, generation of SAS tokens, and client authorization.</span></span>

<span data-ttu-id="5fbee-191">전체에 대 한 hello 구성 및 사용 하 여 SAS 권한 부여를 설명 하는 서비스 버스 응용 프로그램의 작업 예제 참조 [서비스 버스를 통해 공유 액세스 서명 인증](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-191">For a full working sample of a Service Bus application that illustrates hello configuration and uses SAS authorization, see [Shared Access Signature authentication with Service Bus](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8).</span></span> <span data-ttu-id="5fbee-192">네임 스페이스 또는 항목 toosecure 서비스 버스 구독에 구성 된 SAS 권한 부여 규칙의 hello 사용을 보여 주는 관련된 샘플은 여기: [서비스 버스 구독을 사용 하는 공유 액세스 서명 (SAS)를 사용 하 여 인증 ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).</span><span class="sxs-lookup"><span data-stu-id="5fbee-192">A related sample that illustrates hello use of SAS authorization rules configured on namespaces or topics toosecure Service Bus subscriptions is available here: [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).</span></span>

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a><span data-ttu-id="5fbee-193">네임스페이스에 대한 공유 액세스 권한 부여 규칙 액세스</span><span class="sxs-lookup"><span data-stu-id="5fbee-193">Access Shared Access Authorization rules on a namespace</span></span>

<span data-ttu-id="5fbee-194">서비스 버스 네임 스페이스 루트 hello에 대 한 작업에는 인증서 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-194">Operations on hello Service Bus namespace root require certificate authentication.</span></span> <span data-ttu-id="5fbee-195">Azure 구독에 대한 관리 인증서를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-195">You must upload a management certificate for your Azure subscription.</span></span> <span data-ttu-id="5fbee-196">관리 인증서 tooupload hello 단계에 따라 [여기](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), hello를 사용 하 여 [Azure 포털][Azure portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-196">tooupload a management certificate, follow hello steps [here](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), using hello [Azure portal][Azure portal].</span></span> <span data-ttu-id="5fbee-197">Azure 관리 인증서에 대 한 자세한 내용은 참조 hello [Azure 인증서 개요](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-197">For more information about Azure management certificates, see hello [Azure certificates overview](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="5fbee-198">서비스 버스 네임 스페이스에 대 한 공유 액세스 권한 부여 규칙 액세스를 위한 hello 끝점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-198">hello endpoint for accessing shared access authorization rules on a Service Bus namespace is as follows:</span></span>

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

<span data-ttu-id="5fbee-199">toocreate는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 서비스 버스 네임 스페이스에서 개체를 JSON 또는 XML로 serialize 하는 hello 규칙 정보로이 끝점에서 POST 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-199">toocreate a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a Service Bus namespace, execute a POST operation on this endpoint with hello rule information serialized as JSON or XML.</span></span> <span data-ttu-id="5fbee-200">예:</span><span class="sxs-lookup"><span data-stu-id="5fbee-200">For example:</span></span>

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

<span data-ttu-id="5fbee-201">마찬가지로, hello 네임 스페이스에 구성 된 hello 끝점 tooread hello 권한 부여 규칙에 대 한 GET 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-201">Similarly, use a GET operation on hello endpoint tooread hello authorization rules configured on hello namespace.</span></span>

<span data-ttu-id="5fbee-202">tooupdate 또는 특정 권한 부여 규칙을 삭제 hello 다음 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-202">tooupdate or delete a specific authorization rule, use hello following endpoint:</span></span>

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a><span data-ttu-id="5fbee-203">엔터티에 대한 공유 액세스 권한 부여 규칙 액세스</span><span class="sxs-lookup"><span data-stu-id="5fbee-203">Access Shared Access Authorization rules on an entity</span></span>

<span data-ttu-id="5fbee-204">에 액세스할 수 있습니다는 [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 에 서비스 버스 큐 또는 항목 hello 통해 구성 된 개체 [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) hello에 대 한 컬렉션 해당 [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) 또는 [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-204">You can access a [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object configured on a Service Bus queue or topic through hello [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) collection in hello corresponding [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) or [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).</span></span>

<span data-ttu-id="5fbee-205">코드 다음 hello tooadd 권한 부여 규칙 큐에 대 한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-205">hello following code shows how tooadd authorization rules for a queue.</span></span>

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a><span data-ttu-id="5fbee-206">공유 액세스 서명 권한 부여 사용</span><span class="sxs-lookup"><span data-stu-id="5fbee-206">Use Shared Access Signature authorization</span></span>

<span data-ttu-id="5fbee-207">서비스 버스.NET 라이브러리 hello와 hello Azure.NET SDK를 사용 하 여 응용 프로그램 hello 통해 SAS 권한 부여 צ ְ ײ [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-207">Applications using hello Azure .NET SDK with hello Service Bus .NET libraries can use SAS authorization through hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) class.</span></span> <span data-ttu-id="5fbee-208">hello 다음 코드에서는 hello 토큰 공급자 toosend 메시지 tooa 서비스 버스 큐의 hello 사용.</span><span class="sxs-lookup"><span data-stu-id="5fbee-208">hello following code illustrates hello use of hello token provider toosend messages tooa Service Bus queue.</span></span>

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

<span data-ttu-id="5fbee-209">또한 응용 프로그램은 연결 문자열을 수락하는 메서드에 SAS 연결 문자열을 사용하여 인증에 SAS을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-209">Applications can also use SAS for authentication by using a SAS connection string in methods that accept connection strings.</span></span>

<span data-ttu-id="5fbee-210">서비스 버스 릴레이 통해 해당 toouse SAS 권한 부여를 hello 서비스 버스 네임 스페이스에 구성 된 SAS 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-210">Note that toouse SAS authorization with Service Bus relays, you can use SAS keys configured on hello Service Bus namespace.</span></span> <span data-ttu-id="5fbee-211">Hello 네임 스페이스에 릴레이 명시적으로 만들면 ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) 와 [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) 개체를 해당 릴레이 대 한 hello SAS 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-211">If you explicitly create a relay on hello namespace ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) with a [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) object, you can set hello SAS rules just for that relay.</span></span> <span data-ttu-id="5fbee-212">서비스 버스 구독으로 toouse SAS 권한 부여, 항목 또는 서비스 버스 네임 스페이스에 구성 된 SAS 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-212">toouse SAS authorization with Service Bus subscriptions, you can use SAS keys configured on a Service Bus namespace or on a topic.</span></span>

## <a name="use-hello-shared-access-signature-at-http-level"></a><span data-ttu-id="5fbee-213">공유 액세스 서명을 hello를 사용 하 여 (HTTP 수준)</span><span class="sxs-lookup"><span data-stu-id="5fbee-213">Use hello Shared Access Signature (at HTTP level)</span></span>

<span data-ttu-id="5fbee-214">배웠으므로 어떻게 toocreate 공유 액세스 서명 서비스 버스의 모든 엔터티에 대 한,는 HTTP POST tooperform 준비:</span><span class="sxs-lookup"><span data-stu-id="5fbee-214">Now that you know how toocreate Shared Access Signatures for any entities in Service Bus, you are ready tooperform an HTTP POST:</span></span>

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

<span data-ttu-id="5fbee-215">이 방식은 모든 항목에 대해 작동한다는 것을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="5fbee-215">Remember, this works for everything.</span></span> <span data-ttu-id="5fbee-216">큐, 토픽, 구독에 대해 SAS를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-216">You can create SAS for a queue, topic, or subscription.</span></span> 

<span data-ttu-id="5fbee-217">부여 보낸 사람 또는 클라이언트는 SAS 토큰 hello 키를 직접 부여 되지 하 고 hello 해시 tooobtain를 되돌릴 수 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-217">If you give a sender or client a SAS token, they don't have hello key directly, and they cannot reverse hello hash tooobtain it.</span></span> <span data-ttu-id="5fbee-218">예를 들어 사용자가 액세스할 수 있는 항목 및 액세스 기간을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-218">As such, you have control over what they can access, and for how long.</span></span> <span data-ttu-id="5fbee-219">중요 한 사항은 tooremember는 hello hello 정책에 기본 키를 변경 하면 여기에서 만든 모든 공유 액세스 서명을 무효화 될입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-219">An important thing tooremember is that if you change hello primary key in hello policy, any Shared Access Signatures created from it will be invalidated.</span></span>

## <a name="use-hello-shared-access-signature-at-amqp-level"></a><span data-ttu-id="5fbee-220">공유 액세스 서명을 hello를 사용 하 여 (AMQP 수준)</span><span class="sxs-lookup"><span data-stu-id="5fbee-220">Use hello Shared Access Signature (at AMQP level)</span></span>

<span data-ttu-id="5fbee-221">Hello 이전 단원의 toouse 데이터 toohello 서비스 버스 전송에 대 한 HTTP POST 요청으로 SAS 토큰을 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-221">In hello previous section, you saw how toouse hello SAS token with an HTTP POST request for sending data toohello Service Bus.</span></span> <span data-ttu-id="5fbee-222">서비스 버스에 액세스할 수 아시다시피, 고급 메시지 큐 프로토콜 AMQP ()를 다양 한 시나리오에서 성능상의 이유로 hello 기본 설정 프로토콜 toouse hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-222">As you know, you can access Service Bus using hello Advanced Message Queuing Protocol (AMQP) that is hello preferred protocol toouse for performance reasons, in many scenarios.</span></span> <span data-ttu-id="5fbee-223">SAS 토큰 사용 하 여 사용 AMQP hello hello 문서에 설명 되어 [AMQP Claim-Based 보안 버전 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) 즉에 시행 중인 초안 오늘 완벽 하 게 Azure에서 지원 되지만 2013 버전부터 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-223">hello SAS token usage with AMQP is described in hello document [AMQP Claim-Based Security Version 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) that is in working draft since 2013 but well-supported by Azure today.</span></span>

<span data-ttu-id="5fbee-224">Toosend 데이터 tooService 버스를 시작 하기 전에 hello 게시자는 AMQP 메시지 tooa 잘 정의 된 AMQP 노드 라는 내부 hello SAS 토큰을 전송 해야 **$cbs** (것 hello 서비스 tooacquire에서 사용 하는 "특별 한" 큐로 파악 하 고 모든 유효성 검사 hello SAS 토큰)입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-224">Before starting toosend data tooService Bus, hello publisher must send hello SAS token inside an AMQP message tooa well-defined AMQP node named **$cbs** (you can see it as a "special" queue used by hello service tooacquire and validate all hello SAS tokens).</span></span> <span data-ttu-id="5fbee-225">hello 게시자 hello를 지정 해야 **ReplyTo** hello AMQP 메시지 내부의 필드 나타냅니다;이 서비스는 hello에 hello 토큰 유효성 검사 (간단한 요청/회신 패턴 간에 hello 결과 함께 toohello 게시자에 응답 하는 hello 노드 게시자 및 서비스)입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-225">hello publisher must specify hello **ReplyTo** field inside hello AMQP message; this is hello node in which hello service replies toohello publisher with hello result of hello token validation (a simple request/reply pattern between publisher and service).</span></span> <span data-ttu-id="5fbee-226">이 회신 노드가 만들어집니다 "hello 즉석에서" hello AMQP 1.0 사양에 설명 된 대로 "원격 노드의 동적 만들기"에 대 한 말입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-226">This reply node is created "on hello fly," speaking about "dynamic creation of remote node" as described by hello AMQP 1.0 specification.</span></span> <span data-ttu-id="5fbee-227">해당 hello SAS 토큰은 유효을 확인 한 후 hello 게시자 수 앞으로 이동한 다음 toosend 데이터 toohello 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-227">After checking that hello SAS token is valid, hello publisher can go forward and start toosend data toohello service.</span></span>

<span data-ttu-id="5fbee-228">hello 다음 단계 보여 toosend hello를 사용 하 여 AMQP 프로토콜와 SAS 토큰을 hello 하는 방법을 [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-228">hello following steps show how toosend hello SAS token with AMQP protocol using hello [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) library.</span></span> <span data-ttu-id="5fbee-229">Hello 공식을 사용할 수 없는 경우에 유용 서비스 버스 SDK (예를 들어 WinRT,.Net Compact Framework,.Net 마이크로 프레임 워크 및 모노) c에서 개발\#합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-229">This is useful if you can't use hello official Service Bus SDK (for example on WinRT, .Net Compact Framework, .Net Micro Framework and Mono) developing in C\#.</span></span> <span data-ttu-id="5fbee-230">물론,이 라이브러리는 유용 toohelp 클레임 기반 보안을 이해 "는 HTTP POST 요청 및 hello SAS 토큰 내 보낸된 hello 인증" 헤더) (사용 하는 hello HTTP 수준에서 작동 방식을 본 것 처럼 hello AMQP 수준에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-230">Of course, this library is useful toohelp understand how claims-based security works at hello AMQP level, as you saw how it works at hello HTTP level (with an HTTP POST request and hello SAS token sent inside hello "Authorization" header).</span></span> <span data-ttu-id="5fbee-231">AMQP에 대 한 이러한 깊은 지식이 없어도, hello 공식을 사용할 수 있습니다 서비스 버스 SDK.net Framework 응용 프로그램을 수행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-231">If you don't need such deep knowledge about AMQP, you can use hello official Service Bus SDK with .Net Framework applications, which will do it for you.</span></span>

### <a name="c35"></a><span data-ttu-id="5fbee-232">C&#35;</span><span class="sxs-lookup"><span data-stu-id="5fbee-232">C&#35;</span></span>

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
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

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

<span data-ttu-id="5fbee-233">hello `PutCbsToken()` 메서드 수신 hello *연결* (AMQP 연결 클래스 인스턴스 hello 제공한 [AMQP.NET Lite 라이브러리](https://github.com/Azure/amqpnetlite))을 나타내는 hello TCP 연결 toohello 서비스와 hello *sasToken* hello SAS 토큰 toosend 된 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-233">hello `PutCbsToken()` method receives hello *connection* (AMQP connection class instance as provided by hello [AMQP .NET Lite library](https://github.com/Azure/amqpnetlite)) that represents hello TCP connection toohello service and hello *sasToken* parameter that is hello SAS token toosend.</span></span> 

> [!NOTE]
> <span data-ttu-id="5fbee-234">Hello 연결이 이루어진 반드시 **SASL 인증 메커니즘 설정 tooEXTERNAL** (및 사용자 이름 및 암호로 toosend hello SAS 토큰이 필요 하지 않을 때 사용 되는 기본 일반 하지 hello).</span><span class="sxs-lookup"><span data-stu-id="5fbee-234">It's important that hello connection is created with **SASL authentication mechanism set tooEXTERNAL** (and not hello default PLAIN with username and password used when you don't need toosend hello SAS token).</span></span>
> 
> 

<span data-ttu-id="5fbee-235">다음으로 hello 게시자 hello SAS 토큰 송수신 hello 서비스에서 hello 회신 (hello 토큰 유효성 검사 결과)에 대 한 두 개의 AMQP 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-235">Next, hello publisher creates two AMQP links for sending hello SAS token and receiving hello reply (hello token validation result) from hello service.</span></span>

<span data-ttu-id="5fbee-236">hello AMQP 메시지 속성 집합과 간단한 메시지 보다 더 많은 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-236">hello AMQP message contains a set of properties, and more information than a simple message.</span></span> <span data-ttu-id="5fbee-237">hello SAS 토큰은 hello 메시지 (생성자를 사용 하 여)의 hello 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-237">hello SAS token is hello body of hello message (using its constructor).</span></span> <span data-ttu-id="5fbee-238">hello **"ReplyTo"** 속성이 hello 수신기 링크 (이름을 변경할 수 있습니다는 원하는 경우 hello 서비스에 의해 동적으로 생성 됩니다) hello 유효성 검사 결과 받기 위한 toohello 노드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-238">hello **"ReplyTo"** property is set toohello node name for receiving hello validation result on hello receiver link (you can change its name if you want, and it will be created dynamically by hello service).</span></span> <span data-ttu-id="5fbee-239">hello 마지막 세 응용 프로그램/사용자 지정 속성을 사용 하 여 hello 서비스 tooindicate 종류 있기 tooexecute 연산의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-239">hello last three application/custom properties are used by hello service tooindicate what kind of operation it has tooexecute.</span></span> <span data-ttu-id="5fbee-240">Hello 되는 hello CBS 초안 사양에서 설명한 것 처럼 **작업 이름** ("put-토큰"), hello **형식의 토큰** (이 경우는 "servicebus.windows.net:sastoken")에 hello 및 **" "hello 대상 그룹의 이름** toowhich hello 토큰 (전체 엔터티 hello)를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-240">As described by hello CBS draft specification, they must be hello **operation name** ("put-token"), hello **type of token** (in this case, a "servicebus.windows.net:sastoken"), and hello **"name" of hello audience** toowhich hello token applies (hello entire entity).</span></span>

<span data-ttu-id="5fbee-241">Hello 보낸 사람 링크 hello SAS 토큰을 보낸 후 hello 게시자 hello 수신기 링크 hello 회신을 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-241">After sending hello SAS token on hello sender link, hello publisher must read hello reply on hello receiver link.</span></span> <span data-ttu-id="5fbee-242">hello 회신은 라는 응용 프로그램 속성이 있는 간단한 AMQP 메시지 **"상태 코드"** hello 동일한 값으로 HTTP 상태 코드를 포함할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-242">hello reply is a simple AMQP message with an application property named **"status-code"** that can contain hello same values as an HTTP status code.</span></span>

## <a name="rights-required-for-service-bus-operations"></a><span data-ttu-id="5fbee-243">서비스 버스 작업에 필요한 권한</span><span class="sxs-lookup"><span data-stu-id="5fbee-243">Rights required for Service Bus operations</span></span>

<span data-ttu-id="5fbee-244">hello 다음 표에 서비스 버스 리소스에 대 한 다양 한 작업에 필요한 hello 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fbee-244">hello following table shows hello access rights required for various operations on Service Bus resources.</span></span>

| <span data-ttu-id="5fbee-245">작업</span><span class="sxs-lookup"><span data-stu-id="5fbee-245">Operation</span></span> | <span data-ttu-id="5fbee-246">필요한 클레임</span><span class="sxs-lookup"><span data-stu-id="5fbee-246">Claim Required</span></span> | <span data-ttu-id="5fbee-247">클레임 범위</span><span class="sxs-lookup"><span data-stu-id="5fbee-247">Claim Scope</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5fbee-248">**네임스페이스**</span><span class="sxs-lookup"><span data-stu-id="5fbee-248">**Namespace**</span></span> | | |
| <span data-ttu-id="5fbee-249">네임스페이스에서 권한 부여 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="5fbee-249">Configure authorization rule on a namespace</span></span> |<span data-ttu-id="5fbee-250">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-250">Manage</span></span> |<span data-ttu-id="5fbee-251">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-251">Any namespace address</span></span> |
| <span data-ttu-id="5fbee-252">**서비스 레지스트리**</span><span class="sxs-lookup"><span data-stu-id="5fbee-252">**Service Registry**</span></span> | | |
| <span data-ttu-id="5fbee-253">개인 정책 열거</span><span class="sxs-lookup"><span data-stu-id="5fbee-253">Enumerate Private Policies</span></span> |<span data-ttu-id="5fbee-254">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-254">Manage</span></span> |<span data-ttu-id="5fbee-255">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-255">Any namespace address</span></span> |
| <span data-ttu-id="5fbee-256">네임스페이스에서 수신 시작</span><span class="sxs-lookup"><span data-stu-id="5fbee-256">Begin listening on a namespace</span></span> |<span data-ttu-id="5fbee-257">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-257">Listen</span></span> |<span data-ttu-id="5fbee-258">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-258">Any namespace address</span></span> |
| <span data-ttu-id="5fbee-259">네임 스페이스에서 tooa 수신기 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="5fbee-259">Send messages tooa listener at a namespace</span></span> |<span data-ttu-id="5fbee-260">보내기</span><span class="sxs-lookup"><span data-stu-id="5fbee-260">Send</span></span> |<span data-ttu-id="5fbee-261">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-261">Any namespace address</span></span> |
| <span data-ttu-id="5fbee-262">**큐**</span><span class="sxs-lookup"><span data-stu-id="5fbee-262">**Queue**</span></span> | | |
| <span data-ttu-id="5fbee-263">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="5fbee-263">Create a queue</span></span> |<span data-ttu-id="5fbee-264">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-264">Manage</span></span> |<span data-ttu-id="5fbee-265">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-265">Any namespace address</span></span> |
| <span data-ttu-id="5fbee-266">큐 삭제</span><span class="sxs-lookup"><span data-stu-id="5fbee-266">Delete a queue</span></span> |<span data-ttu-id="5fbee-267">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-267">Manage</span></span> |<span data-ttu-id="5fbee-268">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-268">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-269">큐 열거</span><span class="sxs-lookup"><span data-stu-id="5fbee-269">Enumerate queues</span></span> |<span data-ttu-id="5fbee-270">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-270">Manage</span></span> |<span data-ttu-id="5fbee-271">/$Resources/Queues</span><span class="sxs-lookup"><span data-stu-id="5fbee-271">/$Resources/Queues</span></span> |
| <span data-ttu-id="5fbee-272">Hello 큐 설명 가져오기</span><span class="sxs-lookup"><span data-stu-id="5fbee-272">Get hello queue description</span></span> |<span data-ttu-id="5fbee-273">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-273">Manage</span></span> |<span data-ttu-id="5fbee-274">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-274">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-275">큐에서 권한 부여 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="5fbee-275">Configure authorization rule for a queue</span></span> |<span data-ttu-id="5fbee-276">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-276">Manage</span></span> |<span data-ttu-id="5fbee-277">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-277">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-278">Toohello 큐로 보내기</span><span class="sxs-lookup"><span data-stu-id="5fbee-278">Send into toohello queue</span></span> |<span data-ttu-id="5fbee-279">보내기</span><span class="sxs-lookup"><span data-stu-id="5fbee-279">Send</span></span> |<span data-ttu-id="5fbee-280">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-280">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-281">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="5fbee-281">Receive messages from a queue</span></span> |<span data-ttu-id="5fbee-282">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-282">Listen</span></span> |<span data-ttu-id="5fbee-283">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-283">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-284">중단 또는 미리 보기-잠금 모드에서 hello 메시지를 받은 후 메시지 완료</span><span class="sxs-lookup"><span data-stu-id="5fbee-284">Abandon or complete messages after receiving hello message in peek-lock mode</span></span> |<span data-ttu-id="5fbee-285">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-285">Listen</span></span> |<span data-ttu-id="5fbee-286">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-286">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-287">나중에 검색에 대한 메시지 연기</span><span class="sxs-lookup"><span data-stu-id="5fbee-287">Defer a message for later retrieval</span></span> |<span data-ttu-id="5fbee-288">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-288">Listen</span></span> |<span data-ttu-id="5fbee-289">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-289">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-290">메시지 효력 상실</span><span class="sxs-lookup"><span data-stu-id="5fbee-290">Deadletter a message</span></span> |<span data-ttu-id="5fbee-291">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-291">Listen</span></span> |<span data-ttu-id="5fbee-292">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-292">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-293">메시지 큐 세션과 연결 된 hello 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="5fbee-293">Get hello state associated with a message queue session</span></span> |<span data-ttu-id="5fbee-294">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-294">Listen</span></span> |<span data-ttu-id="5fbee-295">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-295">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-296">메시지 큐 세션과 연결 된 hello 상태 설정</span><span class="sxs-lookup"><span data-stu-id="5fbee-296">Set hello state associated with a message queue session</span></span> |<span data-ttu-id="5fbee-297">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-297">Listen</span></span> |<span data-ttu-id="5fbee-298">유효한 큐 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-298">Any valid queue address</span></span> |
| <span data-ttu-id="5fbee-299">**항목**</span><span class="sxs-lookup"><span data-stu-id="5fbee-299">**Topic**</span></span> | | |
| <span data-ttu-id="5fbee-300">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="5fbee-300">Create a topic</span></span> |<span data-ttu-id="5fbee-301">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-301">Manage</span></span> |<span data-ttu-id="5fbee-302">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-302">Any namespace address</span></span> |
| <span data-ttu-id="5fbee-303">항목 삭제</span><span class="sxs-lookup"><span data-stu-id="5fbee-303">Delete a topic</span></span> |<span data-ttu-id="5fbee-304">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-304">Manage</span></span> |<span data-ttu-id="5fbee-305">유효한 항목 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-305">Any valid topic address</span></span> |
| <span data-ttu-id="5fbee-306">항목 열거</span><span class="sxs-lookup"><span data-stu-id="5fbee-306">Enumerate topics</span></span> |<span data-ttu-id="5fbee-307">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-307">Manage</span></span> |<span data-ttu-id="5fbee-308">/$Resources/Topics</span><span class="sxs-lookup"><span data-stu-id="5fbee-308">/$Resources/Topics</span></span> |
| <span data-ttu-id="5fbee-309">Hello 항목 설명 가져오기</span><span class="sxs-lookup"><span data-stu-id="5fbee-309">Get hello topic description</span></span> |<span data-ttu-id="5fbee-310">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-310">Manage</span></span> |<span data-ttu-id="5fbee-311">유효한 항목 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-311">Any valid topic address</span></span> |
| <span data-ttu-id="5fbee-312">항목에서 권한 부여 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="5fbee-312">Configure authorization rule for a topic</span></span> |<span data-ttu-id="5fbee-313">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-313">Manage</span></span> |<span data-ttu-id="5fbee-314">유효한 항목 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-314">Any valid topic address</span></span> |
| <span data-ttu-id="5fbee-315">Toohello 항목 보내기</span><span class="sxs-lookup"><span data-stu-id="5fbee-315">Send toohello topic</span></span> |<span data-ttu-id="5fbee-316">보내기</span><span class="sxs-lookup"><span data-stu-id="5fbee-316">Send</span></span> |<span data-ttu-id="5fbee-317">유효한 항목 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-317">Any valid topic address</span></span> |
| <span data-ttu-id="5fbee-318">**구독**</span><span class="sxs-lookup"><span data-stu-id="5fbee-318">**Subscription**</span></span> | | |
| <span data-ttu-id="5fbee-319">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="5fbee-319">Create a subscription</span></span> |<span data-ttu-id="5fbee-320">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-320">Manage</span></span> |<span data-ttu-id="5fbee-321">네임스페이스 주소</span><span class="sxs-lookup"><span data-stu-id="5fbee-321">Any namespace address</span></span> |
| <span data-ttu-id="5fbee-322">구독 삭제</span><span class="sxs-lookup"><span data-stu-id="5fbee-322">Delete subscription</span></span> |<span data-ttu-id="5fbee-323">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-323">Manage</span></span> |<span data-ttu-id="5fbee-324">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-324">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-325">구독 열거</span><span class="sxs-lookup"><span data-stu-id="5fbee-325">Enumerate subscriptions</span></span> |<span data-ttu-id="5fbee-326">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-326">Manage</span></span> |<span data-ttu-id="5fbee-327">../myTopic/Subscriptions</span><span class="sxs-lookup"><span data-stu-id="5fbee-327">../myTopic/Subscriptions</span></span> |
| <span data-ttu-id="5fbee-328">구독 설명 가져오기</span><span class="sxs-lookup"><span data-stu-id="5fbee-328">Get subscription description</span></span> |<span data-ttu-id="5fbee-329">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-329">Manage</span></span> |<span data-ttu-id="5fbee-330">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-330">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-331">중단 또는 미리 보기-잠금 모드에서 hello 메시지를 받은 후 메시지 완료</span><span class="sxs-lookup"><span data-stu-id="5fbee-331">Abandon or complete messages after receiving hello message in peek-lock mode</span></span> |<span data-ttu-id="5fbee-332">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-332">Listen</span></span> |<span data-ttu-id="5fbee-333">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-333">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-334">나중에 검색에 대한 메시지 연기</span><span class="sxs-lookup"><span data-stu-id="5fbee-334">Defer a message for later retrieval</span></span> |<span data-ttu-id="5fbee-335">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-335">Listen</span></span> |<span data-ttu-id="5fbee-336">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-336">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-337">메시지 효력 상실</span><span class="sxs-lookup"><span data-stu-id="5fbee-337">Deadletter a message</span></span> |<span data-ttu-id="5fbee-338">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-338">Listen</span></span> |<span data-ttu-id="5fbee-339">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-339">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-340">항목 세션과 연결 된 hello 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="5fbee-340">Get hello state associated with a topic session</span></span> |<span data-ttu-id="5fbee-341">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-341">Listen</span></span> |<span data-ttu-id="5fbee-342">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-342">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-343">항목 세션과 연결 된 hello 상태 설정</span><span class="sxs-lookup"><span data-stu-id="5fbee-343">Set hello state associated with a topic session</span></span> |<span data-ttu-id="5fbee-344">수신 대기</span><span class="sxs-lookup"><span data-stu-id="5fbee-344">Listen</span></span> |<span data-ttu-id="5fbee-345">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-345">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-346">**규칙**</span><span class="sxs-lookup"><span data-stu-id="5fbee-346">**Rules**</span></span> | | |
| <span data-ttu-id="5fbee-347">규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="5fbee-347">Create a rule</span></span> |<span data-ttu-id="5fbee-348">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-348">Manage</span></span> |<span data-ttu-id="5fbee-349">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-349">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-350">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="5fbee-350">Delete a rule</span></span> |<span data-ttu-id="5fbee-351">관리</span><span class="sxs-lookup"><span data-stu-id="5fbee-351">Manage</span></span> |<span data-ttu-id="5fbee-352">../myTopic/Subscriptions/mySubscription</span><span class="sxs-lookup"><span data-stu-id="5fbee-352">../myTopic/Subscriptions/mySubscription</span></span> |
| <span data-ttu-id="5fbee-353">규칙 열거</span><span class="sxs-lookup"><span data-stu-id="5fbee-353">Enumerate rules</span></span> |<span data-ttu-id="5fbee-354">관리 또는 수신</span><span class="sxs-lookup"><span data-stu-id="5fbee-354">Manage or Listen</span></span> |<span data-ttu-id="5fbee-355">../myTopic/Subscriptions/mySubscription/Rules</span><span class="sxs-lookup"><span data-stu-id="5fbee-355">../myTopic/Subscriptions/mySubscription/Rules</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5fbee-356">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fbee-356">Next steps</span></span>

<span data-ttu-id="5fbee-357">서비스 버스 메시징에 대 한 더 toolearn hello 다음 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5fbee-357">toolearn more about Service Bus messaging, see hello following topics.</span></span>

* [<span data-ttu-id="5fbee-358">서비스 버스 기본 사항</span><span class="sxs-lookup"><span data-stu-id="5fbee-358">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="5fbee-359">Service Bus 큐, 토픽 및 구독</span><span class="sxs-lookup"><span data-stu-id="5fbee-359">Service Bus queues, topics, and subscriptions</span></span>](service-bus-queues-topics-subscriptions.md)
* [<span data-ttu-id="5fbee-360">어떻게 toouse 서비스 버스 큐</span><span class="sxs-lookup"><span data-stu-id="5fbee-360">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="5fbee-361">어떻게 toouse 서비스 버스 항목 및 구독</span><span class="sxs-lookup"><span data-stu-id="5fbee-361">How toouse Service Bus topics and subscriptions</span></span>](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com