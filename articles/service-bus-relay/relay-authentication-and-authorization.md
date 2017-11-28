---
title: "aaaAzure 릴레이 인증 및 권한 부여 | Microsoft Docs"
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
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a><span data-ttu-id="50705-103">Azure Relay 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="50705-103">Azure Relay authentication and authorization</span></span>
<span data-ttu-id="50705-104">응용 프로그램 tooAzure 인증할 수 있는 공유 액세스 서명 (SAS) 인증을 사용 하 여 릴레이 합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-104">Applications can authenticate tooAzure Relay using Shared Access Signature (SAS) authentication.</span></span> <span data-ttu-id="50705-105">비슷한 너무[서비스 버스 메시징](../service-bus-messaging/service-bus-authentication-and-authorization.md), SAS 인증을 사용 하면 응용 프로그램 tooauthenticate toohello hello 릴레이 네임 스페이스에 구성 된 선택 키를 사용 하 여 Azure 릴레이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="50705-105">Similar too[Service Bus messaging](../service-bus-messaging/service-bus-authentication-and-authorization.md), SAS authentication enables applications tooauthenticate toohello Azure Relay service using an access key configured on hello Relay namespace.</span></span> <span data-ttu-id="50705-106">그런 다음이 키 toogenerate 클라이언트 tooauthenticate toohello 릴레이 서비스를 사용할 수 있는 공유 액세스 서명 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50705-106">You can then use this key toogenerate a Shared Access Signature token that clients can use tooauthenticate toohello relay service.</span></span>

## <a name="shared-access-signature-authentication"></a><span data-ttu-id="50705-107">공유 액세스 서명 인증</span><span class="sxs-lookup"><span data-stu-id="50705-107">Shared Access Signature authentication</span></span>
<span data-ttu-id="50705-108">[SAS 인증](../service-bus-messaging/service-bus-sas.md) 있습니다 toogrant 특정 권한이 포함 된 사용자 액세스 tooAzure 릴레이 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-108">[SAS authentication](../service-bus-messaging/service-bus-sas.md) enables you toogrant a user access tooAzure Relay resources with specific rights.</span></span> <span data-ttu-id="50705-109">SAS 인증에 연결 된 권한으로 리소스에는 암호화 키의 hello 구성을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-109">SAS authentication involves hello configuration of a cryptographic key with associated rights on a resource.</span></span> <span data-ttu-id="50705-110">Hello로 서명 된 expiry 키 구성 및 클라이언트 hello 액세스 중인 리소스 URI의 구성 된 SAS 토큰을 제공 하 여 액세스 toothat 리소스를 다음 넓힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50705-110">Clients can then gain access toothat resource by presenting a SAS token, which consists of hello resource URI being accessed and an expiry signed with hello configured key.</span></span>

<span data-ttu-id="50705-111">Relay 네임스페이스에서 SAS에 대한 키를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50705-111">You can configure keys for SAS on a Relay namespace.</span></span> <span data-ttu-id="50705-112">Service Bus 메시징과 달리 [Relay 하이브리드 연결](relay-hybrid-connections-protocol.md)은 무단 또는 익명 발신자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-112">Unlike Service Bus messaging, [Relay Hybrid Connections](relay-hybrid-connections-protocol.md) supports unauthorized or anonymous senders.</span></span> <span data-ttu-id="50705-113">설정할 수 있습니다 hello 엔터티에 대 한 익명 액세스를 만들 때 hello 화면 hello 포털에서 다음에 표시 된 대로.</span><span class="sxs-lookup"><span data-stu-id="50705-113">You can enable anonymous access for hello entity when you create it, as shown in hello following screen shot from hello portal:</span></span>

![][0]

<span data-ttu-id="50705-114">구성할 수 있습니다 toouse SAS는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) hello 다음으로 구성 된 릴레이 네임 스페이스에서 개체:</span><span class="sxs-lookup"><span data-stu-id="50705-114">toouse SAS, you can configure a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object on a Relay namespace that consists of hello following:</span></span>

* <span data-ttu-id="50705-115">*KeyName* hello 규칙을 식별 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-115">*KeyName* that identifies hello rule.</span></span>
* <span data-ttu-id="50705-116">*PrimaryKey* SAS 토큰 toosign/유효성 검사를 사용 하는 암호화 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50705-116">*PrimaryKey* is a cryptographic key used toosign/validate SAS tokens.</span></span>
* <span data-ttu-id="50705-117">*SecondaryKey* SAS 토큰 toosign/유효성 검사를 사용 하는 암호화 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50705-117">*SecondaryKey* is a cryptographic key used toosign/validate SAS tokens.</span></span>
* <span data-ttu-id="50705-118">*권한* 수신 대기의 hello 컬렉션을 나타내는, 보내기 또는 관리 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-118">*Rights* representing hello collection of Listen, Send, or Manage rights granted.</span></span>

<span data-ttu-id="50705-119">Hello 네임 스페이스 수준에서 구성 된 권한 부여 규칙 액세스 권한을 부여할 수 클라이언트에 대 한 네임 스페이스에 릴레이 연결 tooall hello 해당 키를 사용 하 여 서명 된 토큰으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-119">Authorization rules configured at hello namespace level can grant access tooall relay connections in a namespace for clients with tokens signed using hello corresponding key.</span></span> <span data-ttu-id="50705-120">Too12를 릴레이 네임 스페이스에 이러한 권한 부여 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50705-120">Up too12 such authorization rules can be configured on a Relay namespace.</span></span> <span data-ttu-id="50705-121">기본적으로 모든 권한이 있는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 은 처음으로 프로비전될 때 모든 네임스페이스에 대해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="50705-121">By default, a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) with all rights is configured for every namespace when it is first provisioned.</span></span>

<span data-ttu-id="50705-122">엔터티 tooaccess, hello 클라이언트 특정을 사용 하 여 생성 된 SAS 토큰이 필요 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-122">tooaccess an entity, hello client requires a SAS token generated using a specific [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="50705-123">hello SAS 토큰 hello 리소스 URI toowhich 액세스로 구성 된 리소스 문자열의 hmac-sha256를 요청 하는 hello와 expiry hello 권한 부여 규칙과 연결 된 암호화 키로 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50705-123">hello SAS token is generated using hello HMAC-SHA256 of a resource string that consists of hello resource URI toowhich access is claimed, and an expiry with a cryptographic key associated with hello authorization rule.</span></span>

<span data-ttu-id="50705-124">SAS 인증 지원은 Azure 릴레이 대 한 hello Azure.NET SDK 버전 2.0에에서 포함 이상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="50705-124">SAS authentication support for Azure Relay is included in hello Azure .NET SDK versions 2.0 and later.</span></span> <span data-ttu-id="50705-125">SAS는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-125">SAS includes support for a [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule).</span></span> <span data-ttu-id="50705-126">연결 문자열을 매개 변수로 허용하는 모든 API는 SAS 연결 문자열에 대한 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-126">All APIs that accept a connection string as a parameter include support for SAS connection strings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50705-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50705-127">Next steps</span></span>
- <span data-ttu-id="50705-128">SAS에 대한 자세한 내용은 [공유 액세스 서명을 사용한 Service Bus 인증](../service-bus-messaging/service-bus-sas.md)을 계속 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="50705-128">Continue reading [Service Bus authentication with Shared Access Signatures](../service-bus-messaging/service-bus-sas.md) for more details about SAS.</span></span>
- <span data-ttu-id="50705-129">Hello 참조 [Azure 릴레이 하이브리드 연결 프로토콜 가이드](relay-hybrid-connections-protocol.md) hello 하이브리드 연결 기능에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="50705-129">See hello [Azure Relay Hybrid Connections protocol guide](relay-hybrid-connections-protocol.md) for detailed information about hello Hybrid Connections capability.</span></span>
- <span data-ttu-id="50705-130">Service Bus 메시징 인증 및 권한 부여에 관한 해당 정보는 [Service Bus 인증 및 권한 부여](../service-bus-messaging/service-bus-authentication-and-authorization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="50705-130">For corresponding information about Service Bus Messaging authentication and authorization, see [Service Bus authentication and authorization](../service-bus-messaging/service-bus-authentication-and-authorization.md).</span></span> 

[0]: ./media/relay-authentication-and-authorization/hcanon.png