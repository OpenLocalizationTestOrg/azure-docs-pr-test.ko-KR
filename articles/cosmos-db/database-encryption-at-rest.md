---
title: "미사용 데이터베이스 암호화 - Azure Cosmos DB | Microsoft Docs"
description: "Azure Cosmos DB가 모든 데이터의 기본 암호화를 제공하는 방법을 알아봅니다."
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>미사용 Azure Cosmos DB 데이터베이스 암호화

미사용 데이터 암호화 (Ssd)의 반도체 드라이브와 같은 비휘발성 저장소 장치에 있는 데이터의 암호화 toohello 일반적으로 참조 하는 구문 및 하드 디스크 드라이브 (Hdd) 됩니다. Cosmos DB는 해당 주 데이터베이스를 SSD에 저장합니다. 해당 미디어 첨부 파일 및 백업은 일반적으로 HDD로 백업되는 Azure Blob Storage에 저장됩니다. Cosmos DB에 대 한 미사용 데이터 암호화의 hello 릴리스로 모든 데이터베이스, 미디어 첨부 파일 및 백업 암호화 됩니다. 데이터 (네트워크를 통해 hello) 전송에 암호화 되며 이제 미사용 (비휘발성 저장소) 제공 종단 간 암호화 합니다.

As DB Cosmos PaaS 서비스는 매우 쉽게 toouse입니다. Cosmos DB에 저장 된 모든 사용자 데이터 전송에서 휴지 암호화 되며, 필요는 없습니다 tootake 조치 합니다. 암호화에는 이것이 또 다른 방법은 tooput rest는 기본적으로 "on"입니다. 없는 컨트롤 tooturn는 설정 또는 해제 하는 것입니다. Toomeet를 계속 실행 하는 동안이 기능을 제공 했습니다 우리의 [가용성 및 성능 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db)합니다.

## <a name="implement-encryption-at-rest"></a>미사용 암호화 구현

미사용 암호화는 보안 키 저장소 시스템, 암호화된 네트워크 및 암호화 API를 비롯한 수많은 보안 기술을 사용하여 구현되었습니다. 암호를 해독 하 고 데이터를 처리 하는 시스템에는 키를 관리 하는 시스템과 toocommunicate가 됩니다. hello 다이어그램 저장소 키의 암호화 된 데이터 및 hello 관리 어떻게 분리 되는지 보여 줍니다. 

![디자인 다이어그램](./media/database-encryption-at-rest/design-diagram.png)

사용자 요청 hello 기본 흐름은 다음과 같습니다.
- hello 사용자 데이터베이스 계정이 준비 되 면 만들어지고 저장소 키 요청 toohello 관리 서비스 리소스 공급자를 통해 검색 됩니다.
- 사용자는 HTTPS/secure 전송을 통해 연결 tooCosmos DB를 만듭니다. (hello Sdk 추상 hello 정보)입니다.
- hello 사용자가 이전에 만든 보안 연결 hello를 통해 저장 된 JSON 문서 toobe를 보냅니다.
- hello JSON 문서는 hello 사용자가을 인덱싱을 해제 하지 않는 한 인덱싱됩니다.
- JSON 문서 hello 및 인덱스 데이터를 모두 toosecure 저장소에 기록 됩니다.
- 정기적으로 데이터 hello 보안 저장소에서 읽기 및 toohello Azure 암호화 된 Blob 저장소를 백업 합니다.

## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>Q: 저장소 서비스 암호화를 사용하는 경우 Azure Storage 비용은 얼마나 늘어나나요?
A: 추가 비용은 없습니다.

### <a name="q-who-manages-hello-encryption-keys"></a>Q: 누구 hello 암호화 키를 관리?
A: hello 키 Microsoft에서 관리 됩니다.

### <a name="q-how-often-are-encryption-keys-rotated"></a>Q: 얼마나 자주 암호화 키가 순환되나요?
A: Microsoft에는 Cosmos DB가 따르는 암호화 키 회전에 대한 일련의 내부 지침이 있습니다. hello 지침이 게시 되지 않습니다. Microsoft는 hello 게시 [수명 주기 SDL (Security Development)](https://www.microsoft.com/sdl/default.aspx), 내부 지침의 하위 집합으로 간주 되 고 개발자를 위한 유용한 모범 사례에는 합니다.

### <a name="q-can-i-use-my-own-encryption-keys"></a>Q: 나만의 암호화 키를 사용할 수 있나요?
A: cosmos DB PaaS 서비스 이며 하드 tookeep hello 서비스 쉽게 toouse 했습니다. 이 질문이 PCI-DSS와 같은 규정 준수 요구 사항을 충족시키기 위한 프록시 질문으로 자주 제기되는 것을 확인했습니다. 이 기능을 작성 과정의 일부로 Cosmos DB를 사용 하는 고객 hello 필요 toomanage 키 자체 없이 해당 요구 사항을 충족 하는지 준수 감사자 tooensure 들과 협력 합니다.
결과적으로, 현재 제공 하지 않습니다 사용자 hello 옵션 tooburden 자체 키 관리 합니다.

### <a name="q-what-regions-have-encryption-turned-on"></a>Q: 암호화가 설정된 지역은 어디인가요?
A: 모든 Azure Cosmos DB 지역에서 모든 사용자 데이터에 대해 암호화가 켜져 있습니다.

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>Q: 암호화 영향은 hello 성능 대기 시간 및 처리량 Sla?
A: 경우 영향이 나 변경을 toohello 성능 Sla 미사용 데이터 암호화는 모든 기존 및 새 계정에 대해 사용 하도록 설정 했으므로 자세한 내용은 hello에 [Cosmos DB에 대 한 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db) 페이지 toosee hello 최신 보장 합니다.

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>Q: hello 로컬 에뮬레이터 미사용 데이터 암호화를 지원 합니까?
A: hello 에뮬레이터는 독립 실행형 개발/테스트 도구와 관리 되는 Cosmos DB 서비스 사용 하 여 hello hello 키 관리 서비스를 사용 하지 않습니다. 중요 한 에뮬레이터 테스트 데이터를 저장 하는 드라이브에 BitLocker tooenable 것을 권장 합니다. hello [에뮬레이터의 hello 기본 데이터 디렉터리를 변경 지원](local-emulator.md) 잘 알려진 위치를 사용 하 여 뿐만 아니라 합니다.

## <a name="next-steps"></a>다음 단계

Cosmos DB 보안과 hello 최신 향상 기능 개요를 참조 하십시오. [Azure Cosmos DB 데이터베이스 보안](database-security.md)합니다.
Microsoft 인증에 대 한 자세한 내용은 참조 hello [Azure 보안 센터](https://azure.microsoft.com/en-us/support/trust-center/)합니다.
