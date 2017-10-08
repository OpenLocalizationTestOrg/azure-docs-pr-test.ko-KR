---
title: "PostgreSQL 관계형 데이터베이스 서비스에 대 한 Azure 데이터베이스의 aaaOverview | Microsoft Docs"
description: "PostgreSQL 관계형 데이터베이스 서비스에 대한 Azure Docs 개요를 제공합니다."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>PostgreSQL용 Azure Database란?

Azure PostgreSQL 데이터베이스는 Microsoft 클라우드 오픈 소스의 hello 커뮤니티 버전에 따라 개발자 용으로 작성 된 hello에 관계형 데이터베이스 서비스 [PostgreSQL](https://www.postgresql.org/) 데이터베이스 엔진입니다. 이 서비스는 공개 미리 보기 상태입니다. PostgreSQL용 Azure Database는 다음과 같은 기능을 제공합니다.
- 여러 서비스 수준에서 예측 가능한 성능
- 응용 프로그램 가동 중지 시간 없는 동적 확장성
- 기본 제공되는 고가용성
- 데이터 보호

이러한 모든 기능에는 인증이 필요하지 않고 추가 비용 없이 제공됩니다. 이러한 기능을 사용 하면 신속한 응용 프로그램 개발 및 사용자 시간 toomarket를 가속화 하는 데 보다는에 시간을 단축 하 고 리소스 toomanaging 가상 컴퓨터 및 인프라 할당 toofocus 있습니다. 또한 toodevelop hello로 응용 프로그램 소스 도구 및 플랫폼의 선택한 열고 배달 hello 속도와 효율성 toolearn 새로운 기술이 필요 없이 비즈니스 요구를 계속할 수 있습니다. 

이 문서는 PostgreSQL 핵심 개념 및 기능 관련된 tooperformance, 확장성 및 관리 효율성에 대 한 소개 tooAzure 데이터베이스입니다. 이 빠른 시작 했는지 tooget 참조:

- [Azure Portal을 사용하여 PostgreSQL용 Azure Database 만들기](quickstart-create-server-database-portal.md)
- [PostgreSQL hello Azure CLI를 사용 하 여에 대 한 Azure 데이터베이스 만들기](quickstart-create-server-database-azure-cli.md)

일련의 Azure CLI 및 PowerShell 샘플은 다음을 참조하세요.

- [PostgreSQL용 Azure Database에 대한 Azure CLI 샘플](./sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>가동 중지 시간 없이 성능 및 규모 조정

현재 PostgreSQL용 Azure Database 서비스는 기본 및 표준 서비스 계층을 제공합니다. 각 서비스 계층은 [다양 한 수준의 성능, IOPS 보장 및 성능이 나와](concepts-service-tiers.md) toosupport tooheavyweight 경량 데이터베이스 작업입니다. 몇 가지 미리 한 달에 대 한 작은 서버에 첫 번째 응용 프로그램을 빌드할 수 있습니다 다음 [hello 성능 수준을 변경](scripts/sample-scale-server-up-or-down.md) 서비스 내에서 계층 수동으로 또는 프로그래밍 방식으로 솔루션의 요구 하는 시간 toomeet hello에 있습니다. 가동 중지 시간 tooyour 응용 프로그램이 나 tooyour 고객 않고이 수행할 수 있습니다. 동적 확장성 데이터베이스 tootransparently 리소스 요구 사항 및 사용 하도록 설정 하면 tooonly hello 리소스에 대 한 지불이 필요할 때 해야 변경 toorapidly 응답할 수 있습니다.

## <a name="monitoring-and-alerting"></a>모니터링 및 경고
어떻게 결정 합니까 시기와 위아래 toodial? Hello 기본 제공 성능 모니터링 및 경고 기능을 단위 계산에 따라 hello 성능 등급을 함께 사용. 확장 단위 계산의 hello 영향을 빠르게 평가할 수 또는 아래로 현재 또는 예상 성능 요구 사항에 따라 이러한 도구를 사용 하 여 있습니다. 자세한 내용은 [PostgreSQL용 Azure Database 옵션 및 성능: 각 서비스 계층에서 사용할 수 있는 항목 이해](./concepts-service-tiers.md)를 참조하세요.

## <a name="keep-your-app-and-business-running"></a>앱 및 비즈니스 운영 유지
Azure의 업계 선도적인 99.99% 가용성(미리 보기 상태에서 사용할 수 없음) SLA(서비스 수준 약정)를 Microsoft에서 관리되는 전 세계 데이터 센터 네트워크의 지원을 받아 앱을 연중 무휴(24/7)로 실행할 수 있습니다. PostgreSQL 서버에 대 한 모든 Azure 데이터베이스 있습니다 활용할 기본 제공 보안, 결함 허용 및 웹 사이트가 없으면 toobuy 또는 디자인, 빌드 및 관리 하는 데이터 보호. PostgreSQL, Azure 데이터베이스와 각 서비스 계층 이런 방식으로 비즈니스 연속성 기능 및 tooget를 사용할 수 있는 옵션 및 실행 중 상태로 유지 되는 포괄적인 집합을 제공 합니다. 사용할 수 있습니다 [지정 시간 복원](howto-restore-server-portal.md) tooreturn 데이터베이스 tooan 35 일 이전에 출시 이전 상태입니다. 또한 데이터베이스를 호스트 하는 hello 데이터 센터가 중단 되 면, 최근 백업의 지리적 중복 복사본에서 데이터베이스를 복원할 수 있습니다.

## <a name="secure-your-data"></a>데이터 보호
Azure Database 서비스는 PostgreSQL용 Azure Database가 액세스를 제한하고, 미사용 및 사용 중인 데이터를 보호하고, 작업을 모니터링하는 데 도움이 되는 기능을 사용하여 보관하도록 데이터 보안을 유지해왔습니다. Hello 방문 [Azure 보안 센터](https://www.microsoft.com/TrustCenter/Security/default.aspx) Azure의 플랫폼 보안에 대 한 정보에 대 한 합니다.

PostgreSQL 서비스에 대 한 Azure 데이터베이스 hello rest에서 데이터에 대 한 저장소 암호화를 사용합니다. 데이터 백업을 포함 하는 쿼리를 실행 하는 동안 hello 엔진에 의해 만들어진 임시 파일의 hello 예외) (가진 디스크에 암호화 됩니다. hello 서비스는 Azure 저장소 암호화에 포함 된 AES 256 비트 암호화를 사용 하 고 hello 키가 시스템에서 관리 합니다. 저장소 암호화는 항상 켜져 있고 해제할 수 없습니다.

기본적으로 Azure 데이터베이스 PostgreSQL 서비스는 구성 된 toorequire hello [SSL 연결 보안](./concepts-ssl-connection-security.md) 데이터에서-동작이 hello 네트워크 전체에 대 한 합니다. 데이터베이스 서버와 클라이언트 응용 프로그램 간의 SSL 연결을 강제 적용 하면 공격 으로부터 보호 "man hello 중간에" hello 서버와 응용 프로그램 간의 hello 데이터 스트림을 암호화 하 여 합니다.  필요에 따라 클라이언트 응용 프로그램에서 SSL 연결을 지원 하지 않으면 tooyour 데이터베이스 서비스를 연결 하기 위한 SSL이 필요한 비활성화할 수 있습니다.

## <a name="next-steps"></a>다음 단계
- Hello 참조 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/postgresql/) 비용 비교 및 계산기에 대 한 합니다.
- [첫 번째 PostgreSQL용 Azure Database를 만들](./quickstart-create-server-database-portal.md)어서 시작합니다.
- Python, PHP, Ruby, C\#, Java, Node.js에서 첫 번째 앱 빌드: [연결 라이브러리](./concepts-connection-libraries.md)
