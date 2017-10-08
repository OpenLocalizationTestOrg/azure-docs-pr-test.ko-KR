---
title: "MySQL에 대 한 Azure 데이터베이스에 대 한 연결 aaaSSL | Microsoft Docs"
description: "SSL 연결을 사용 하는 MySQL 및 tooproperly 관련된 응용 프로그램에 대 한 Azure 데이터베이스를 구성 하는 것에 대 한 정보"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>MySQL용 Azure 데이터베이스의 SSL 연결
MySQL에 대 한 azure 데이터베이스 연결 (SECURE Sockets Layer)을 사용 하 여 데이터베이스 서버 tooclient 응용 프로그램을 지원 합니다. 데이터베이스 서버와 클라이언트 응용 프로그램 간의 SSL 연결을 강제 적용 하면 공격 으로부터 보호 "man hello 중간에" hello 서버와 응용 프로그램 간의 hello 데이터 스트림을 암호화 하 여 합니다.

## <a name="default-settings"></a>기본 설정
기본적으로 hello 데이터베이스 서비스 tooMySQL 연결할 때 구성 된 toorequire SSL 연결 해야 합니다.  가능 하면 항상 hello SSL 옵션을 해제 하지 않는 것이 좋습니다. 

Hello Azure 포털을 통해 MySQL 서버에 대 한 새 Azure 데이터베이스 및 CLI 프로비저닝, 기본적으로 SSL 연결의 적용을 사용 하도록 설정 됩니다. 

마찬가지로, hello Azure 포털에서에서 해당 서버에서 연결 문자열을 "를" 설정 hello에에서 미리 정의 된 연결 문자열이 SSL을 사용 하 여 일반적인 언어 tooconnect tooyour 데이터베이스 서버에 대 한 필요한 hello 매개 변수를 포함 합니다. hello 매개 변수 SSL에 따라 달라 집니다 hello 커넥터 예를 들어 "ssl = true" 또는 "sslmode = 필요" 또는 "sslmode = 필요" 및 다른 변형 합니다.

어떻게 응용 프로그램을 개발할 때 tooenable 또는 사용 안 함 SSL 연결을 참조 하십시오 너무 toolearn[어떻게 tooconfigure SSL](howto-configure-ssl.md)합니다.

## <a name="next-steps"></a>다음 단계
[MySQL용 Azure 데이터베이스에 대한 연결 라이브러리](concepts-connection-libraries.md)
