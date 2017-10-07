---
title: "aaaAzure 서비스 버스 인증 및 권한 부여 | Microsoft Docs"
description: "앱 tooService 버스 공유 액세스 서명 (SAS) 인증으로 인증 합니다."
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
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Service Bus 인증 및 권한 부여

응용 프로그램 tooAzure 공유 액세스 서명 (SAS)를 사용 하 여 서비스 버스를 인증할 수 있는 인증 합니다. 공유 액세스 서명 인증 사용 응용 프로그램 tooauthenticate tooService hello 네임 스페이스나 특정 권한이 연결 된 hello 엔터티에서 구성 된 선택 키를 사용 하 여 버스입니다. 그런 다음이 키 toogenerate 클라이언트 tooauthenticate tooService 버스를 사용할 수 있는 공유 액세스 서명 토큰을 사용할 수 있습니다.

> [!IMPORTANT]
> ACS는 이제 사용되지 않으므로 Azure Active Directory Access Control(Access Control Service 또는 ACS라고도 함) 대신 SAS를 사용해야 합니다. SAS는 Service Bus에 대한 단순하고 유연하며 사용이 쉬운 인증 체계를 제공합니다. 응용 프로그램 SAS 시나리오에서에서 사용할 수 없는 필요 하지 않은 권한이 있는 "사용자의 합니다." toomanage hello 개념 자세한 내용은 [이 블로그 게시물](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)에 게시해 주세요.

## <a name="shared-access-signature-authentication"></a>공유 액세스 서명 인증

[SAS 인증](service-bus-sas.md) 있습니다 toogrant 특정 권한이 포함 된 사용자 액세스 tooService 버스 리소스를 사용 합니다. SAS 인증 서비스 버스에 연결 된 권한으로 서비스 버스 리소스에 대 한 암호화 키 hello 구성을 수행 해야 합니다. Hello로 서명 된 expiry 키 구성 및 클라이언트 hello 액세스 중인 리소스 URI의 구성 된 SAS 토큰을 제공 하 여 액세스 toothat 리소스를 다음 넓힐 수 있습니다.

Service Bus 네임 스페이스에서 SAS에 대한 키를 구성할 수 있습니다. hello 키는 해당 네임 스페이스에서 메시징 엔터티를 tooall 적용 됩니다. 또한 Service Bus 큐 및 항목에 키를 구성할 수 있습니다. SAS는 [Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md)에서도 지원됩니다.

구성할 수 있습니다 toouse SAS는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 네임 스페이스, 큐 또는 항목에는 개체입니다. 이 규칙 구성 요소를 다음 hello 됩니다.

* *KeyName* hello 규칙을 식별 하는 합니다.
* *PrimaryKey* SAS 토큰 toosign/유효성 검사를 사용 하는 암호화 키가 있습니다.
* *SecondaryKey* SAS 토큰 toosign/유효성 검사를 사용 하는 암호화 키가 있습니다.
* *권한* 수신 대기의 hello 컬렉션을 나타내는, 보내기 또는 관리 권한을 부여 합니다.

Hello 네임 스페이스 수준에서 구성 된 권한 부여 규칙 액세스 권한을 부여할 수 tooall 엔터티 네임 스페이스에 클라이언트에 대 한 hello 해당 키를 사용 하 여 서명 된 토큰으로 합니다. Too12를 서비스 버스 네임 스페이스, 큐 또는 항목에 이러한 권한 부여 규칙을 구성할 수 있습니다. 기본적으로 모든 권한이 있는 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) 은 처음으로 프로비전될 때 모든 네임스페이스에 대해 구성됩니다.

엔터티 tooaccess, hello 클라이언트 특정을 사용 하 여 생성 된 SAS 토큰이 필요 [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)합니다. hello SAS 토큰 hello 리소스 URI toowhich 액세스로 구성 된 리소스 문자열의 hmac-sha256를 요청 하는 hello와 expiry hello 권한 부여 규칙과 연결 된 암호화 키로 사용 하 여 생성 됩니다.

서비스 버스에 대 한 SAS 인증 지원은 hello Azure.NET SDK 버전 2.0에에서 포함 이상 됩니다. SAS는 [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)에 대한 지원을 포함합니다. 연결 문자열을 매개 변수로 허용하는 모든 API는 SAS 연결 문자열에 대한 지원을 포함합니다.

## <a name="next-steps"></a>다음 단계

- SAS에 대한 자세한 내용은 [공유 액세스 서명을 사용한 Service Bus 인증](service-bus-sas.md)을 계속 읽으세요.
- [TooACS Enabled 네임 스페이스를 변경합니다.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Azure Relay 인증 및 권한 부여에 관한 해당 정보는 [Azure Relay 인증 및 권한 부여](../service-bus-relay/relay-authentication-and-authorization.md)를 참조하세요. 

