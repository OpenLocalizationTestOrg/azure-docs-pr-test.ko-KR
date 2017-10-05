---
title: "Azure Relay 인증 및 권한 부여 | Microsoft Docs"
description: "Azure Relay의 SAS(공유 액세스 서명) 인증 개요"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 95589ca169926362fa77f0e307afd449014c8402
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-authentication-and-authorization"></a><span data-ttu-id="1c654-103">Azure Relay 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="1c654-103">Azure Relay authentication and authorization</span></span>
<span data-ttu-id="1c654-104">응용 프로그램은 SAS(공유 액세스 서명) 인증을 사용하여 Azure Relay에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-104">Applications can authenticate to Azure Relay using Shared Access Signature (SAS) authentication.</span></span> <span data-ttu-id="1c654-105">[Service Bus 메시징](../service-bus-messaging/service-bus-authentication-and-authorization.md)과 유사하게 SAS 인증을 사용하면 응용 프로그램이 Relay 네임스페이스에 구성된 액세스 키를 통해 Azure Relay 서비스에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-105">Similar to [Service Bus messaging](../service-bus-messaging/service-bus-authentication-and-authorization.md), SAS authentication enables applications to authenticate to the Azure Relay service using an access key configured on the Relay namespace.</span></span> <span data-ttu-id="1c654-106">그런 다음 이 키를 사용하여 클라이언트가 Relay 서비스를 인증하는 데 사용할 수 있는 공유 액세스 서명 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-106">You can then use this key to generate a Shared Access Signature token that clients can use to authenticate to the relay service.</span></span>

## <a name="shared-access-signature-authentication"></a><span data-ttu-id="1c654-107">공유 액세스 서명 인증</span><span class="sxs-lookup"><span data-stu-id="1c654-107">Shared Access Signature authentication</span></span>
<span data-ttu-id="1c654-108">[SAS 인증](../service-bus-messaging/service-bus-sas.md)을 사용하면 특정 권한으로 Azure Relay 리소스에 액세스하는 권한을 사용자에게 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-108">[SAS authentication](../service-bus-messaging/service-bus-sas.md) enables you to grant a user access to Azure Relay resources with specific rights.</span></span> <span data-ttu-id="1c654-109">SAS 인증은 리소스에 연결된 권한이 있는 암호화 키의 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-109">SAS authentication involves the configuration of a cryptographic key with associated rights on a resource.</span></span> <span data-ttu-id="1c654-110">클라이언트는 액세스된 리소스 URI 및 구성된 키로 서명된 만료로 구성된 SAS 토큰을 제공하여 해당 리소스에 대한 액세스를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-110">Clients can then gain access to that resource by presenting a SAS token, which consists of the resource URI being accessed and an expiry signed with the configured key.</span></span>

<span data-ttu-id="1c654-111">Relay 네임스페이스에서 SAS에 대한 키를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-111">You can configure keys for SAS on a Relay namespace.</span></span> <span data-ttu-id="1c654-112">Service Bus 메시징과 달리 [Relay 하이브리드 연결](relay-hybrid-connections-protocol.md)은 무단 또는 익명 발신자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-112">Unlike Service Bus messaging, [Relay Hybrid Connections](relay-hybrid-connections-protocol.md) supports unauthorized or anonymous senders.</span></span> <span data-ttu-id="1c654-113">포털에서 다음 화면에 표시된 것처럼 만들 때 엔터티에 대한 익명 액세스를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-113">You can enable anonymous access for the entity when you create it, as shown in the following screen shot from the portal:</span></span>

![][0]

<span data-ttu-id="1c654-114">SAS를 사용하려면 다음을 구성하는 Relay 네임스페이스에서 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 개체를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-114">To use SAS, you can configure a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a Relay namespace that consists of the following:</span></span>

* <span data-ttu-id="1c654-115">*KeyName* 입니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-115">*KeyName* that identifies the rule.</span></span>
* <span data-ttu-id="1c654-116">*PrimaryKey* 는 SAS 토큰을 서명/확인하는 데 사용되는 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-116">*PrimaryKey* is a cryptographic key used to sign/validate SAS tokens.</span></span>
* <span data-ttu-id="1c654-117">*SecondaryKey* 는 SAS 토큰을 서명/확인하는 데 사용되는 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-117">*SecondaryKey* is a cryptographic key used to sign/validate SAS tokens.</span></span>
* <span data-ttu-id="1c654-118">*권한* 입니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-118">*Rights* representing the collection of Listen, Send, or Manage rights granted.</span></span>

<span data-ttu-id="1c654-119">네임스페이스 수준에서 구성된 권한 부여 규칙은 해당 키를 사용하여 서명된 토큰으로 클라이언트에 대한 네임스페이스의 모든 relay 연결에 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-119">Authorization rules configured at the namespace level can grant access to all relay connections in a namespace for clients with tokens signed using the corresponding key.</span></span> <span data-ttu-id="1c654-120">권한 부여 규칙은 Relay 네임스페이스에서 최대 12개까지 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-120">Up to 12 such authorization rules can be configured on a Relay namespace.</span></span> <span data-ttu-id="1c654-121">기본적으로 모든 권한이 있는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 은 처음으로 프로비전될 때 모든 네임스페이스에 대해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-121">By default, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) with all rights is configured for every namespace when it is first provisioned.</span></span>

<span data-ttu-id="1c654-122">엔터티에 액세스하려면 클라이언트는 특정 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)을 사용하여 생성된 SAS 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-122">To access an entity, the client requires a SAS token generated using a specific [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="1c654-123">액세스를 요청하는 리소스 URI로 구성된 리소스 문자열의 HMAC-SHA256 및 권한 부여 규칙에 연결된 암호화 키가 있는 만료를 사용하여 SAS 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-123">The SAS token is generated using the HMAC-SHA256 of a resource string that consists of the resource URI to which access is claimed, and an expiry with a cryptographic key associated with the authorization rule.</span></span>

<span data-ttu-id="1c654-124">Azure Relay에 대한 SAS 인증 지원은 Azure.NET SDK 버전 2.0 이상에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-124">SAS authentication support for Azure Relay is included in the Azure .NET SDK versions 2.0 and later.</span></span> <span data-ttu-id="1c654-125">SAS는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-125">SAS includes support for a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="1c654-126">연결 문자열을 매개 변수로 허용하는 모든 API는 SAS 연결 문자열에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1c654-126">All APIs that accept a connection string as a parameter include support for SAS connection strings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c654-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c654-127">Next steps</span></span>
- <span data-ttu-id="1c654-128">SAS에 대한 자세한 내용은 [공유 액세스 서명을 사용한 Service Bus 인증](../service-bus-messaging/service-bus-sas.md)을 계속 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="1c654-128">Continue reading [Service Bus authentication with Shared Access Signatures](../service-bus-messaging/service-bus-sas.md) for more details about SAS.</span></span>
- <span data-ttu-id="1c654-129">하이브리드 연결 기능에 대한 자세한 내용은 [Azure Relay 하이브리드 연결 프로토콜 가이드](relay-hybrid-connections-protocol.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c654-129">See the [Azure Relay Hybrid Connections protocol guide](relay-hybrid-connections-protocol.md) for detailed information about the Hybrid Connections capability.</span></span>
- <span data-ttu-id="1c654-130">Service Bus 메시징 인증 및 권한 부여에 관한 해당 정보는 [Service Bus 인증 및 권한 부여](../service-bus-messaging/service-bus-authentication-and-authorization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c654-130">For corresponding information about Service Bus Messaging authentication and authorization, see [Service Bus authentication and authorization](../service-bus-messaging/service-bus-authentication-and-authorization.md).</span></span> 

[0]: ./media/relay-authentication-and-authorization/hcanon.png