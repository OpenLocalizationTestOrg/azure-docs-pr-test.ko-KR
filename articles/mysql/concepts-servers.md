---
title: "MySQL에 대 한 Azure 데이터베이스에 대 한 aaaServer 개념 | Microsoft Docs"
description: "이 항목에서는 MySQL용 Azure 데이터베이스 서버를 사용할 때의 고려 사항 및 지침을 제공합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>MySQL용 Azure 데이터베이스의 서버 개념
이 항목에서는 MySQL용 Azure 데이터베이스 서버를 사용할 때의 고려 사항 및 지침을 제공합니다.

## <a name="what-is-an-azure-database-for-mysql-server"></a>MySQL용 Azure 데이터베이스 서버란?

MySQL용 Azure 데이터베이스 서버는 여러 데이터베이스에 대한 중앙 관리 지점입니다. 되기 hello 동일한 MySQL 서버 구문 hello 온-프레미스 환경에서에 대해 잘 알고 수 있습니다. 특히, MySQL 서비스에 대 한 hello Azure 데이터베이스 관리 되는 성능을 보장, 액세스 및 서버 수준에서 기능을 노출 합니다.

MySQL용 Azure 데이터베이스 서버:

- Azure 구독 내에서 만들어집니다.
- 데이터베이스에 대 한 hello 부모 리소스가입니다.
- 데이터베이스에 대한 네임스페이스를 제공합니다.
- 컨테이너 강력한 수명 의미 체계가-있는 서버를 삭제 하 고 hello 포함 된 데이터베이스를 삭제 합니다.
- 하위 지역에 리소스를 배치합니다.
- 서버 및 데이터베이스 액세스에 대한 연결 끝점을 제공합니다.
- Tooits 데이터베이스 적용 되는 관리 정책에 대 한 hello 범위를 제공 합니다: 로그인, 방화벽, 사용자, 역할, 구성, 등입니다.
- 여러 버전으로 제공됩니다. 자세한 내용은 [지원되는 MySQL용 Azure 데이터베이스 버전](./concepts-supported-versions.md)을 참조하세요.

Azure Database for MySQL 서버 내에서 하나 이상의 데이터베이스를 만들 수 있습니다. 모든 hello 리소스 toocreate 서버 tooutilize 당 단일 데이터베이스를 선택 하거나 여러 데이터베이스 tooshare hello 리소스를 만들 수 있습니다. 구조적된 서버 hello 가격 책정은, 가격 책정 계층의 hello 구성에 따라, 단위, 저장소 (GB)를 계산 합니다. 자세한 내용은 [가격 책정 계층](./concepts-service-tiers.md)을 참조하세요.

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>어떻게 연결 하 고 MySQL server에 대 한 Azure 데이터베이스 tooan 인증?

hello 다음과 같은 요소가 보장할 안전 하 게 액세스할 tooyour 데이터베이스.

|||
| :-- | :-- |
| **인증 및 권한 부여** | MySQL용 Azure 데이터베이스 서버는 네이티브 MySQL 인증을 지원합니다. 연결 하 고 hello 서버의 관리자 로그인과 tooserver 인증 수 있습니다. |
| **프로토콜** | hello 서비스는 MySQL에서 사용 되는 메시지 기반 프로토콜을 지원 합니다. |
| **TCP/IP** | hello 프로토콜 over TCP/IP 사용 및 Unix 도메인 소켓을 통해 지원 됩니다. |
| **방화벽** | toohelp 데이터를 보호, 방화벽 규칙 방지 모든 액세스 tooyour 데이터베이스 서버 또는 컴퓨터를 지정할 때까지 tooits 데이터베이스 권한이 있어야 합니다. [MySQL용 Azure 데이터베이스 서버 방화벽 규칙](./concepts-firewall-rules.md)을 참조하세요. |
| **SSL** | hello 서비스 지원 응용 프로그램와 데이터베이스 서버 간에 SSL 연결을 적용 합니다.  참조 [응용 프로그램 toosecurely에서 SSL 구성 연결 MySQL 용 tooAzure 데이터베이스 연결](./howto-configure-ssl.md)합니다. |
|||

## <a name="how-do-i-manage-a-server"></a>서버는 어떻게 관리해야 하나요?
Azure CLI hello 또는 hello Azure 포털을 사용 하 여 MySQL server에 대 한 Azure 데이터베이스를 관리할 수 있습니다.

## <a name="next-steps"></a>다음 단계
- Hello 서비스의 개요를 참조 하십시오. [Azure 데이터베이스에 대 한 MySQL 개요](./overview.md)
- **서비스 계층**에 따른 특정 리소스 할당량 및 제한 사항에 대한 자세한 내용은 [서비스 계층](./concepts-service-tiers.md)을 참조하세요.
- 연결 toohello 서비스에 대 한 정보를 참조 하십시오. [MySQL에 대 한 Azure 데이터베이스에 대 한 연결 라이브러리](./concepts-connection-libraries.md)합니다.
