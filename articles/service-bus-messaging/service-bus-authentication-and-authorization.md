---
title: "Azure Service Bus 인증 및 권한 부여 | Microsoft Docs"
description: "SAS(공유 액세스 서명) 인증을 사용하여 Service Bus에 대해 앱을 인증합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 28fb41499c919e5006f1be7daa97610c2a0583af
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-authentication-and-authorization"></a><span data-ttu-id="e2003-103">Service Bus 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="e2003-103">Service Bus authentication and authorization</span></span>

<span data-ttu-id="e2003-104">응용 프로그램은 SAS(공유 액세스 서명) 인증을 사용하여 Azure Service Bus에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-104">Applications can authenticate to Azure Service Bus using Shared Access Signature (SAS) authentication.</span></span> <span data-ttu-id="e2003-105">공유 액세스 서명 인증을 사용하면 응용 프로그램을 네임 스페이스 또는 특정 권한이 연관된 엔터티에서 구성된 선택키를 사용하여 Service Bus에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-105">Shared Access Signature authentication enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the entity with which specific rights are associated.</span></span> <span data-ttu-id="e2003-106">그런 다음 이 키를 사용하여 클라이언트가 Service Bus를 인증하는 데 사용할 수 있는 공유 액세스 서명 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-106">You can then use this key to generate a Shared Access Signature token that clients can use to authenticate to Service Bus.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2003-107">ACS는 이제 사용되지 않으므로 Azure Active Directory Access Control(Access Control Service 또는 ACS라고도 함) 대신 SAS를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-107">You should use SAS instead of Azure Active Directory Access Control (also known as Access Control Service or ACS), as ACS is being deprecated.</span></span> <span data-ttu-id="e2003-108">SAS는 Service Bus에 대한 단순하고 유연하며 사용이 쉬운 인증 체계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-108">SAS provides a simple, flexible, and easy-to-use authentication scheme for Service Bus.</span></span> <span data-ttu-id="e2003-109">응용 프로그램은 권한 있는 "사용자"의 개념을 관리할 필요가 없는 시나리오에서 SAS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-109">Applications can use SAS in scenarios in which they do not need to manage the notion of an authorized "user."</span></span> <span data-ttu-id="e2003-110">자세한 내용은 [이 블로그 게시물](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)에 게시해 주세요.</span><span class="sxs-lookup"><span data-stu-id="e2003-110">For more information, see [this blog post](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).</span></span>

## <a name="shared-access-signature-authentication"></a><span data-ttu-id="e2003-111">공유 액세스 서명 인증</span><span class="sxs-lookup"><span data-stu-id="e2003-111">Shared Access Signature authentication</span></span>

<span data-ttu-id="e2003-112">[SAS 인증](service-bus-sas.md)을 사용하면 특정 권한으로 Service Bus 리소스에 사용자 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-112">[SAS authentication](service-bus-sas.md) enables you to grant a user access to Service Bus resources with specific rights.</span></span> <span data-ttu-id="e2003-113">Service Bus에서 SAS 인증은 Service Bus 리소스에 연결된 권한이 있는 암호화 키의 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-113">SAS authentication in Service Bus involves the configuration of a cryptographic key with associated rights on a Service Bus resource.</span></span> <span data-ttu-id="e2003-114">클라이언트는 액세스된 리소스 URI 및 구성된 키로 서명된 만료로 구성된 SAS 토큰을 제공하여 해당 리소스에 대한 액세스를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-114">Clients can then gain access to that resource by presenting a SAS token, which consists of the resource URI being accessed and an expiry signed with the configured key.</span></span>

<span data-ttu-id="e2003-115">Service Bus 네임 스페이스에서 SAS에 대한 키를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-115">You can configure keys for SAS on a Service Bus namespace.</span></span> <span data-ttu-id="e2003-116">키는 해당 네임 스페이스의 모든 메시징 엔터티에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-116">The key applies to all messaging entities in that namespace.</span></span> <span data-ttu-id="e2003-117">또한 Service Bus 큐 및 항목에 키를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-117">You can also configure keys on Service Bus queues and topics.</span></span> <span data-ttu-id="e2003-118">SAS는 [Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md)에서도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-118">SAS is also supported on [Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md).</span></span>

<span data-ttu-id="e2003-119">SAS를 사용하려면 네임스페이스, 큐 또는 토픽에서 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 개체를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-119">To use SAS, you can configure a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a namespace, queue, or topic.</span></span> <span data-ttu-id="e2003-120">이 규칙은 다음 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-120">This rule consists of the following elements:</span></span>

* <span data-ttu-id="e2003-121">*KeyName* 입니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-121">*KeyName* that identifies the rule.</span></span>
* <span data-ttu-id="e2003-122">*PrimaryKey* 는 SAS 토큰을 서명/확인하는 데 사용되는 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-122">*PrimaryKey* is a cryptographic key used to sign/validate SAS tokens.</span></span>
* <span data-ttu-id="e2003-123">*SecondaryKey* 는 SAS 토큰을 서명/확인하는 데 사용되는 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-123">*SecondaryKey* is a cryptographic key used to sign/validate SAS tokens.</span></span>
* <span data-ttu-id="e2003-124">*권한* 입니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-124">*Rights* representing the collection of Listen, Send, or Manage rights granted.</span></span>

<span data-ttu-id="e2003-125">네임 스페이스 수준에서 구성된 권한 부여 규칙은 해당 키를 사용하여 서명된 토큰으로 클라이언트에 대한 네임 스페이스의 모든 엔터티에 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-125">Authorization rules configured at the namespace level can grant access to all entities in a namespace for clients with tokens signed using the corresponding key.</span></span> <span data-ttu-id="e2003-126">이러한 권한 부여 규칙을 Service Bus 네임 스페이스, 큐 또는 항목에서 최대 12개까지 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-126">Up to 12 such authorization rules can be configured on a Service Bus namespace, queue, or topic.</span></span> <span data-ttu-id="e2003-127">기본적으로 모든 권한이 있는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 은 처음으로 프로비전될 때 모든 네임스페이스에 대해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-127">By default, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) with all rights is configured for every namespace when it is first provisioned.</span></span>

<span data-ttu-id="e2003-128">엔터티에 액세스하려면 클라이언트는 특정 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)을 사용하여 생성된 SAS 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-128">To access an entity, the client requires a SAS token generated using a specific [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="e2003-129">액세스를 요청하는 리소스 URI로 구성된 리소스 문자열의 HMAC-SHA256 및 권한 부여 규칙에 연결된 암호화 키가 있는 만료를 사용하여 SAS 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-129">The SAS token is generated using the HMAC-SHA256 of a resource string that consists of the resource URI to which access is claimed, and an expiry with a cryptographic key associated with the authorization rule.</span></span>

<span data-ttu-id="e2003-130">Service Bus에 대한 SAS 인증 지원은 Azure.NET SDK 버전 2.0 이후에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-130">SAS authentication support for Service Bus is included in the Azure .NET SDK versions 2.0 and later.</span></span> <span data-ttu-id="e2003-131">SAS는 [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-131">SAS includes support for a [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="e2003-132">연결 문자열을 매개 변수로 허용하는 모든 API는 SAS 연결 문자열에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e2003-132">All APIs that accept a connection string as a parameter include support for SAS connection strings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2003-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2003-133">Next steps</span></span>

- <span data-ttu-id="e2003-134">SAS에 대한 자세한 내용은 [공유 액세스 서명을 사용한 Service Bus 인증](service-bus-sas.md)을 계속 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="e2003-134">Continue reading [Service Bus authentication with Shared Access Signatures](service-bus-sas.md) for more details about SAS.</span></span>
- [<span data-ttu-id="e2003-135">ACS 지원 네임스페이스로 변경</span><span class="sxs-lookup"><span data-stu-id="e2003-135">Changes To ACS Enabled namespaces.</span></span>](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- <span data-ttu-id="e2003-136">Azure Relay 인증 및 권한 부여에 관한 해당 정보는 [Azure Relay 인증 및 권한 부여](../service-bus-relay/relay-authentication-and-authorization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2003-136">For corresponding information about Azure Relay authentication and authorization, see [Azure Relay authentication and authorization](../service-bus-relay/relay-authentication-and-authorization.md).</span></span> 

