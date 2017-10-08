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
# <a name="azure-relay-authentication-and-authorization"></a>Azure Relay 인증 및 권한 부여
응용 프로그램 tooAzure 인증할 수 있는 공유 액세스 서명 (SAS) 인증을 사용 하 여 릴레이 합니다. 비슷한 너무[서비스 버스 메시징](../service-bus-messaging/service-bus-authentication-and-authorization.md), SAS 인증을 사용 하면 응용 프로그램 tooauthenticate toohello hello 릴레이 네임 스페이스에 구성 된 선택 키를 사용 하 여 Azure 릴레이 서비스입니다. 그런 다음이 키 toogenerate 클라이언트 tooauthenticate toohello 릴레이 서비스를 사용할 수 있는 공유 액세스 서명 토큰을 사용할 수 있습니다.

## <a name="shared-access-signature-authentication"></a>공유 액세스 서명 인증
[SAS 인증](../service-bus-messaging/service-bus-sas.md) 있습니다 toogrant 특정 권한이 포함 된 사용자 액세스 tooAzure 릴레이 리소스를 사용 합니다. SAS 인증에 연결 된 권한으로 리소스에는 암호화 키의 hello 구성을 수행 해야 합니다. Hello로 서명 된 expiry 키 구성 및 클라이언트 hello 액세스 중인 리소스 URI의 구성 된 SAS 토큰을 제공 하 여 액세스 toothat 리소스를 다음 넓힐 수 있습니다.

Relay 네임스페이스에서 SAS에 대한 키를 구성할 수 있습니다. Service Bus 메시징과 달리 [Relay 하이브리드 연결](relay-hybrid-connections-protocol.md)은 무단 또는 익명 발신자를 지원합니다. 설정할 수 있습니다 hello 엔터티에 대 한 익명 액세스를 만들 때 hello 화면 hello 포털에서 다음에 표시 된 대로.

![][0]

구성할 수 있습니다 toouse SAS는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) hello 다음으로 구성 된 릴레이 네임 스페이스에서 개체:

* *KeyName* hello 규칙을 식별 하는 합니다.
* *PrimaryKey* SAS 토큰 toosign/유효성 검사를 사용 하는 암호화 키가 있습니다.
* *SecondaryKey* SAS 토큰 toosign/유효성 검사를 사용 하는 암호화 키가 있습니다.
* *권한* 수신 대기의 hello 컬렉션을 나타내는, 보내기 또는 관리 권한을 부여 합니다.

Hello 네임 스페이스 수준에서 구성 된 권한 부여 규칙 액세스 권한을 부여할 수 클라이언트에 대 한 네임 스페이스에 릴레이 연결 tooall hello 해당 키를 사용 하 여 서명 된 토큰으로 합니다. Too12를 릴레이 네임 스페이스에 이러한 권한 부여 규칙을 구성할 수 있습니다. 기본적으로 모든 권한이 있는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 은 처음으로 프로비전될 때 모든 네임스페이스에 대해 구성됩니다.

엔터티 tooaccess, hello 클라이언트 특정을 사용 하 여 생성 된 SAS 토큰이 필요 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)합니다. hello SAS 토큰 hello 리소스 URI toowhich 액세스로 구성 된 리소스 문자열의 hmac-sha256를 요청 하는 hello와 expiry hello 권한 부여 규칙과 연결 된 암호화 키로 사용 하 여 생성 됩니다.

SAS 인증 지원은 Azure 릴레이 대 한 hello Azure.NET SDK 버전 2.0에에서 포함 이상 됩니다. SAS는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)에 대한 지원을 포함합니다. 연결 문자열을 매개 변수로 허용하는 모든 API는 SAS 연결 문자열에 대한 지원을 포함합니다.

## <a name="next-steps"></a>다음 단계
- SAS에 대한 자세한 내용은 [공유 액세스 서명을 사용한 Service Bus 인증](../service-bus-messaging/service-bus-sas.md)을 계속 읽으세요.
- Hello 참조 [Azure 릴레이 하이브리드 연결 프로토콜 가이드](relay-hybrid-connections-protocol.md) hello 하이브리드 연결 기능에 대 한 자세한 내용은 합니다.
- Service Bus 메시징 인증 및 권한 부여에 관한 해당 정보는 [Service Bus 인증 및 권한 부여](../service-bus-messaging/service-bus-authentication-and-authorization.md)를 참조하세요. 

[0]: ./media/relay-authentication-and-authorization/hcanon.png