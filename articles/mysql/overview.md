---
title: "MySQL 관계형 데이터베이스 서비스에 대 한 Azure 데이터베이스의 aaaOverview | Microsoft Docs"
description: "Hello Azure 데이터베이스 MySQL 관계형 데이터베이스 서비스에 대해 간략하게 설명 합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>MySQL용 Azure Database란? 서비스 소개
MySQL에 대 한 azure 데이터베이스는 Microsoft 클라우드 기반 hello의 관계형 데이터베이스 서비스 [MySQL Community Edition](https://www.mysql.com/products/community/) 데이터베이스 엔진입니다.  MySQL용 Azure Database는 다음과 같은 기능을 제공합니다.

- 여러 서비스 수준에서 예측 가능한 성능
- 응용 프로그램 가동 중지 시간 없는 동적 확장성
- 기본 제공되는 고가용성
- 데이터 보호

이러한 기능에는 인증이 필요하지 않고 추가 비용 없이 제공됩니다. Toofocus 빠른 응용 프로그램 개발 및 사용자 시간 toomarket를 가속화 하는 데 보다는에 시간을 단축 하 고 리소스 toomanaging 가상 컴퓨터 및 인프라를 할당할 수 있습니다. 또한 toodevelop hello로 응용 프로그램 소스 도구 및 플랫폼의 선택한 열고 배달 hello 속도와 효율성 toolearn 새로운 기술이 필요 없이 비즈니스 요구를 계속할 수 있습니다.

![MySQL용 Azure Database 개념 다이어그램](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

이 문서는 MySQL 핵심 개념 및 기능 관련된 tooperformance, 확장성 및 관리 효율성, 링크 tooexplore 세부 정보에 대 한 소개 tooAzure 데이터베이스입니다. 이 빠른 시작 했는지 tooget 참조:
- [Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI를 사용한 MySQL용 Azure 데이터베이스 서버 만들기](quickstart-create-mysql-server-database-using-azure-cli.md)

일련의 Azure CLI 샘플은 다음을 참조하세요.
- [MySQL용 Azure Database에 대한 Azure CLI 샘플](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>가동 중지 시간 없이 성능 및 규모 조정
MySQL용 Azure Database는 기본 및 표준 서비스 계층을 제공합니다. 각 계층은 다양 한 성능 및 기능 toosupport tooheavyweight 경량 데이터베이스 작업을 제공합니다. 월, 다음 변경 된 서비스 계층 tooscale 프로그램 중단 시간 없이 솔루션의 필요성을 해결 몇 달러에 대 한 작은 데이터베이스에 첫 번째 앱을 빌드할 수 있습니다. 확장성 동적 리소스 요구 사항을 변경 하 여 데이터베이스 tootransparently 응답 toorapidly를 수 있습니다. 필요할 때 필요한 hello 리소스에 대 한만 지불 합니다.

## <a name="monitoring-and-alerting"></a>모니터링 및 경고
알 수 있을까요 hello 마우스 오른쪽 단추로 클릭 하 여 중지 아래로 전화 때? Hello 기본 제공 성능 모니터링 및 경고와 hello 성능 등급을 계산 하는 단위에 따라 결합 기능을 사용 합니다. 이러한 기능을 사용 하 확장 또는 축소 현재 기준의 hello 영향을 신속 하 게 평가할 수 있습니다 또는 프로젝트 성능 요구 합니다. 자세한 내용은 [개념: 서비스 계층](concepts-service-tiers.md)을 참조하세요.

## <a name="keep-your-app-and-business-running"></a>앱 및 비즈니스 운영 유지
Azure의 업계 선도적인 99.99% 가용성 SLA(서비스 수준 약정)를 Microsoft에서 관리되는 전 세계 데이터 센터 네트워크의 지원을 받아 앱을 연중 무휴(24/7)로 실행할 수 있습니다. MySQL server에 대 한 모든 Azure 데이터베이스 있습니다 활용할 기본 제공 보안, 결함 허용 및 웹 사이트가 없으면 toobuy 또는 디자인, 빌드 및 관리 하는 데이터 보호. MySQL에 대 한 Azure 데이터베이스를 지정 시간 복원 toorecover 서버 tooan를 사용할 수 있습니다 35 일 이전에 출시 이전 상태입니다.

## <a name="secure-your-data"></a>데이터 보호
Azure Database 서비스는 MySQL용 Azure Database가 액세스를 제한하고, 미사용 및 사용 중인 데이터를 보호하고, 작업을 모니터링하는 데 도움이 되는 기능을 사용하여 보관하도록 데이터 보안을 유지해왔습니다. Hello 방문 [Azure 보안 센터](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) Azure의 플랫폼 보안에 대 한 정보에 대 한 합니다.

MySQL 서비스에 대 한 Azure 데이터베이스 hello rest에서 데이터에 대 한 저장소 암호화를 사용합니다. 데이터 백업을 포함 하는 쿼리를 실행 하는 동안 hello 엔진에 의해 만들어진 임시 파일의 hello 예외) (가진 디스크에 암호화 됩니다. hello 서비스는 Azure 저장소 암호화에 포함 된 AES 256 비트 암호화를 사용 하 고 hello 키가 시스템에서 관리 합니다. 저장소 암호화는 항상 켜져 있고 해제할 수 없습니다.

기본적으로 Azure 데이터베이스 MySQL 서비스는 구성 된 toorequire hello [SSL 연결 보안](./concepts-ssl-connection-security.md) 데이터에서-동작이 hello 네트워크 전체에 대 한 합니다. 데이터베이스 서버와 클라이언트 응용 프로그램 간의 SSL 연결을 강제 적용 하면 공격 으로부터 보호 "man hello 중간에" hello 서버와 응용 프로그램 간의 hello 데이터 스트림을 암호화 하 여 합니다.  필요에 따라 클라이언트 응용 프로그램에서 SSL 연결을 지원 하지 않으면 tooyour 데이터베이스 서비스를 연결 하기 위한 SSL이 필요한 비활성화할 수 있습니다.

## <a name="next-steps"></a>다음 단계
MySQL에 대 한 소개 tooAzure 데이터베이스 읽기 되었으며 hello 질문의 답변 했으므로 "MySQL에 대 한 Azure 데이터베이스는 무엇입니까?", 준비가 되었습니다.
- Hello 가격 계산기 및 비용 비교에 대 한 페이지를 참조 하십시오. [가격](https://azure.microsoft.com/pricing/details/mysql/)
- 첫 번째 서버를 만들어서 시작합니다. [Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기](quickstart-create-mysql-server-database-using-azure-portal.md)
- Python, PHP, Ruby, C에서 첫 번째 앱을 빌드하고\#, Java, Node.js: [MySQL 용 tooconnect tooAzure 데이터베이스를 사용 하는 연결 라이브러리](concepts-connection-libraries.md)
