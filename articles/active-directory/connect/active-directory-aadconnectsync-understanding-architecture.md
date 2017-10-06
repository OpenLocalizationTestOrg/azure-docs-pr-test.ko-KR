---
title: "Azure AD Connect 동기화: hello 아키텍처 이해 | Microsoft Docs"
description: "이 항목의 Azure AD Connect sync hello 아키텍처에 설명 하 고 hello를 설명 합니다. 사용 되는 용어입니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Azure AD Connect 동기화: hello 아키텍처 이해
이 항목에서는 Azure AD Connect 동기화를 위한 hello 기본 아키텍처를 설명 합니다. 많은 측면에서 MIIS 2003, 2007 ILM 및 FIM 2010 비슷한 tooits 선행 작업입니다. Azure AD Connect 동기화가 이러한 기술의 hello 발전 합니다. 이러한 이전 기술 중 하나에 대해 잘 알고 있다면이 항목의 내용은 hello 친숙 한 tooyou도 됩니다. 새 toosynchronization 인 경우이 항목은 드립니다. 그러나 없는 tooAzure AD Connect 동기화 (이 항목의 호출된 동기화 엔진) 사용자 지정 될 때 성공이 항목 toobe의 요구 사항 tooknow hello 정보입니다.

## <a name="architecture"></a>아키텍처
hello 동기화 엔진이 여러 연결 된 데이터 원본에 저장 된 개체에 대 한 통합된 뷰를 만들고 그 데이터 소스에서 id 정보를 관리 합니다. 이 통합된 보기 hello id 정보를 결정 하는 규칙의 집합 및 연결 된 데이터 원본에서 검색 따라 사용자가 어떻게 tooprocess이이 정보입니다.

### <a name="connected-data-sources-and-connectors"></a>연결된 데이터 원본 및 커넥터
동기화 엔진이 hello는 Active Directory 또는 SQL Server 데이터베이스와 같은 다른 데이터 저장소에서 id 정보를 처리합니다. 데이터베이스 형식에서 해당 데이터를 구성 하 고 표준 데이터 액세스 메서드를 제공 하는 모든 데이터 저장소는 hello 동기화 엔진에 대 한 잠재적인 데이터 소스 후보입니다. 동기화 엔진에 의해 동기화 되는 hello 데이터 저장소 라고 **연결 된 데이터 원본을** 또는 **연결 디렉터리** (CD).

hello 동기화 엔진을 호출 하는 모듈 내에서 연결 된 데이터 소스와 상호 작용 캡슐화는 **커넥터**합니다. 각 유형의 연결된 데이터 원본은 특정 커넥터를 포함합니다. 필요한 작업을 변환 하는 hello 커넥터 연결 된 데이터를 hello hello 형식으로 원본에 대 한 이해 합니다.

커넥터는 연결 된 데이터 원본과 API 호출 (읽기 및 쓰기) tooexchange id 정보를 확인 합니다. 사용자 지정 커넥터 가능한 tooadd 이기도 hello 확장 가능한 연결 프레임 워크를 사용 합니다. hello 다음 그림 커넥터는 연결 된 데이터 원본 toohello 동기화 엔진을 연결 하는 방법을 나타냅니다.

![Arch1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

데이터는 어느 방향으로나 이동할 수 있지만 양방향으로 동시에 이동할 수는 없습니다. 즉, 커넥터를 동기화 엔진 toohello 연결 된 데이터 원본 또는 hello 연결 된 데이터 원본 toosync 엔진에서 구성 된 tooallow 데이터 tooflow 될 수 있습니다 하지만 한 개체 및 특성에 대 한 한 번에 이러한 작업 중 하나에 발생할 수 있습니다. hello 방향은 서로 다른 특성 및 다른 개체에 대해 다 수 있습니다.

커넥터 tooconfigure hello 개체 유형 toosynchronize 되도록 지정 합니다. Hello 개체 형식 지정 hello 동기화 프로세스에 포함 된 개체의 hello 범위를 정의 합니다. hello 다음 단계에는 특성이 포함 목록으로 알려진 tooselect hello 특성 toosynchronize입니다. 이러한 설정은 응답 toochanges tooyour 비즈니스 규칙에서 언제 든 지 변경할 수 있습니다. Hello Azure AD Connect 설치 마법사를 사용 하는 경우 이러한 설정이 구성 됩니다.

tooexport 개체 tooa 연결 된 데이터 원본 hello 특성 목록은 최소한 포함 최소 hello 특성 필요한 toocreate 연결된 된 데이터 원본에는 특정 개체를 입력 합니다. 예를 들어 hello **sAMAccountName** 특성이 포함 되어야 합니다 hello 특성 포함 목록 tooexport에 사용자 개체는 디렉터리 tooActive 않으므로 Active Directory에 있는 모든 사용자 개체는 **sAMAccountName**  특성을 정의 합니다. 다시 hello 설치 마법사는이 구성을 수행 하지 않습니다.

Hello 연결 된 데이터 원본 파티션 또는 컨테이너 tooorganize 개체 등의 구조적 구성 요소를 사용 하는 경우에 지정된 된 솔루션에 사용 되는 연결 된 데이터 원본의 hello hello 영역을 제한할 수 있습니다.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Hello 동기화 엔진 네임 스페이스의 내부 구조
hello 전체 동기화 엔진 네임 스페이스 hello id 정보를 저장 하는 두 개의 네임 스페이스 구성 됩니다. hello 두 네임 스페이스가 됩니다.

* hello 커넥터 공간 (CS)
* hello 메타 버스 (M)

hello **커넥터 공간** hello 특성 포함 목록에 지정 된 연결 된 데이터 원본과 hello 특성에서 개체를 지정 하는 hello의 설명이 들어 있는 준비 영역입니다. hello 동기화 엔진 hello 커넥터 공간 toodetermine hello 연결 된 데이터 원본과 toostage 들어오는 변경 내용에서 변경 된 내용을 사용 합니다. hello 동기화 엔진은 또한 hello 커넥터 공간 toostage 나가는 내보내기 toohello 연결 된 데이터 원본에 대 한 변경 내용을 사용 합니다. hello 동기화 엔진이 각 커넥터에 대 한 준비 영역으로 고유한 커넥터 공간을 유지합니다.

준비 영역을 사용 하 여 hello 동기화 엔진이 hello 연결 된 데이터 소스에 대해 독립적으로 유지 하 고 가용성 및 내게 필요한 옵션의 영향을 받지 않습니다. 결과적으로, hello 준비 영역의 hello 데이터를 사용 하 여 언제 든 지 id 정보를 처리할 수 있습니다. hello 동기화 엔진이 이후 hello 마지막 통신 세션이 종료 또는 연결 된 데이터 원본 hello만 hello 변경 tooidentity 정보 푸시 아직 받지 못한를 줄여주는 hello 연결 된 데이터 원본 내에서 수행 된 hello 변경 된 내용만 요청할 수 있습니다. hello hello 동기화 엔진과 hello 연결 된 데이터 원본 간의 네트워크 트래픽을 합니다.

또한 동기화 엔진이 hello 커넥터 공간에 준비 하는 모든 개체에 대 한 상태 정보를 저장 합니다. 새 데이터를 수신 하면 동기화 엔진이 항상 hello 데이터 이미 동기화 되었는지 여부를 평가 합니다.

hello **메타 버스** 결합 된 모든 개체의 단일 글로벌, 통합 보기를 제공 하는 여러 연결 된 데이터 원본에서 집계 하는 hello id 정보를 포함 하는 저장소 영역입니다. 메타 버스 개체 hello 연결 된 데이터 원본과 toocustomize hello 동기화 프로세스를 허용 하는 규칙 집합에서 검색 된 hello id 정보에 따라 생성 됩니다.

hello 다음은 hello 커넥터 공간 네임 스페이스 및 hello 동기화 엔진에서 hello 메타 버스 네임 스페이스입니다.

![Arch2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>동기화 엔진 ID 개체
hello 동기화 엔진의 hello 개체는 hello 연결 된 데이터 원본에서 두 개체의 표현을 또는 hello 통합된 보기 동기화 엔진에는 해당 개체의 합니다. 모든 동기화 엔진 개체에는 전역 고유 식별자(GUID)가 있어야 합니다. GUID는 데이터 무결성을 제공하고 개체 간의 관계를 표현합니다.

### <a name="connector-space-objects"></a>커넥터 공간 개체
동기화 엔진은 연결 된 데이터 소스와 통신할 경우 hello id 정보 hello 연결 된 데이터 원본에 읽고 hello 커넥터 공간에 해당 정보 toocreate hello id 개체의 표현을 사용 합니다. 이러한 개체는 개별적으로 만들거나 삭제할 수 없습니다. 그러나 커넥터 공간의 모든 개체를 수동으로 삭제할 수는 있습니다.

Hello 커넥터 공간에 개체를 모두 두 개의 특성을 갖습니다.

* 전역적으로 고유한 식별자(GUID)
* 고유 이름(DN이라고 함)

Hello 연결 된 데이터 원본에는 고유한 특성 toohello 개체를 사용 하는 할당 경우 hello 커넥터 공간에 개체 앵커 특성이 하나씩 있을 수도 있습니다. hello 앵커 특성 hello 연결 된 데이터 원본에서 개체를 고유 하 게 식별 합니다. hello 동기화 엔진 hello 연결 된 데이터 원본에 hello 앵커 toolocate hello 해당이 개체의 표현을 사용합니다. 동기화 엔진에서는 개체의 해당 hello 앵커 되지 변경 hello 개체의 hello 수명 주기 동안

대부분의 hello 커넥터 사용 알려진된 고유 식별자 toogenerate 앵커 자동으로 각 개체에 대 한 가져올 때 합니다. Active Directory Connector hello hello를 사용 하는 예를 들어 **objectGUID** 앵커에 대 한 특성입니다. 명확 하 게 정의 된 고유 식별자를 제공 하지 않는 연결 된 데이터 원본에 대 한 hello 커넥터 구성의 일부분으로 앵커 세대를 지정할 수 있습니다.

Hello 앵커 하나에서 빌드한 경우 더 많은 고유 특성 개체의 입력을 모두 변경 하 고 고유 하 게 있다는 점에서 hello 커넥터 공간 (예를 들어 직원 번호 또는 사용자 ID)에 hello 개체를 식별 합니다.

커넥터 공간 개체 hello 다음 중 하나일 수 있습니다.

* 스테이징 개체
* 자리 표시자

### <a name="staging-objects"></a>스테이징 개체
스테이징 개체 hello 연결 된 데이터 원본의 개체 유형을 지정 하는 hello의 인스턴스를 나타냅니다. 또한 toohello GUID와 hello 고유 이름의 경우는 준비 개체의 hello 개체 유형을 나타내는 값입니다.

항상 가져온 준비 개체 hello 앵커 특성에 대 한 값이 있어야 합니다. 새로 프로 비전 되어 동기화 엔진에 의해 hello 연결 된 데이터 원본에서 만들어지는 hello 과정에는 개체를 준비 hello 앵커 특성에 대 한 값을 갖지 않습니다.

준비 개체는 또한 비즈니스 특성 및 작업 정보 동기화 엔진 tooperform hello 동기화 프로세스에 필요한의 현재 값을 전달 합니다. 작업 정보를 나타내는 개체를 준비 하는 hello에 준비 된 업데이트의 hello 유형 플래그를 포함 합니다. Hello 개체로 플래그가 지정 된 경우 스테이징 개체는 아직 처리 되지 않은 hello 연결 된 데이터 원본의 새 id 정보를 받은 경우 **가져오기 보류 중인**합니다. 스테이징 개체에 새 id 정보를 아직 내보낸된 toohello 연결 된 데이터 원본, 것으로 플래그가 지정 되어 **내보내기 보류 중인**합니다.

스테이징 개체는 가져오기 또는 내보내기 개체가 될 수 있습니다. 동기화 엔진이 hello hello 연결 된 데이터 원본에서 받은 개체 정보를 사용 하 여 가져오기 개체를 만듭니다. 동기화 엔진 hello 커넥터에서에서 선택한 hello 개체 유형 중 하 나와 일치 하는 새 개체의 hello 존재 하는 방법에 대 한 정보를 받으면 가져오기 개체를 만듭니다 hello 커넥터 공간에 hello 연결 된 데이터 원본에서 hello 개체 표현 합니다.

다음 그림 hello hello 연결 된 데이터 원본에서 개체를 나타내는 가져오기 개체를 보여 줍니다.

![Arch3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

hello 동기화 엔진은 hello 메타 버스의 개체 정보를 사용 하 여 내보내기 개체를 만듭니다. 개체 내보내기는 hello 다음 통신 세션 중 내보낸된 toohello 연결 된 데이터 원본 합니다. Hello hello 동기화 엔진의 관점에서 내보내기 개체가 존재 하지 않는 hello 연결 된 데이터 원본에 아직 합니다. 따라서 내보내기 개체에 대 한 hello 앵커 특성은 사용할 수 없습니다. 동기화 엔진에서 hello 개체를 수신한 후 hello 연결 된 데이터 원본은 hello 개체의 hello 앵커 특성에 대 한 고유한 값을 만듭니다.

hello 다음 그림에서는 hello 메타 버스의 id 정보를 사용 하 여 내보내기 개체 어떻게 만들어집니다.

![Arch4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

동기화 엔진이 hello hello 연결 된 데이터 원본의 hello 개체를 다시 여 hello 개체의 내보내기 hello를 확인 합니다. 개체 내보내기 동기화 엔진이 해당 연결 된 데이터 원본의 hello 다음 가져오기 작업 중 받을 때 개체 가져오기 됩니다.

### <a name="placeholders"></a>자리 표시자
hello 동기화 엔진 구조 네임 스페이스 toostore 개체를 사용합니다. 그러나 Active Directory와 같은 일부 연결된 데이터 원본은 계층 구조 네임스페이스를 사용합니다. 단일 구조 네임 스페이스에는 계층적 네임 스페이스에서 정보를 tootransform, 동기화 엔진 자리 표시자 toopreserve hello 계층 구조를 사용합니다.

각 자리 표시자는 개체의 계층 이름 동기화 엔진으로 가져오지 않은 있지만 필요한 tooconstruct hello 계층 이름입니다 (예를 들어 조직 구성 단위) 구성 요소를 나타냅니다. Hello 커넥터 공간에 개체를 준비 된 hello 연결 된 데이터 원본 tooobjects에 참조에 의해 만들어진 간격을 채울 있습니다.

hello 동기화 엔진은 또한 아직 가져오지 않은 자리 표시자 toostore 참조 된 개체를 사용 합니다. 예를 들어, 동기화는 hello에 대 한 구성 된 tooinclude hello 관리자 특성 *Abbie Spencer* 개체 및 hello 받은 값은 개체와 같은 아직 가져온 되지 않은 *CN Lee Sperry, CN = Users, DC = = fabrikam, DC = com*, hello 관리자 정보 hello 커넥터 공간에 대 한 자리 표시자로 저장 됩니다. Hello 관리자 개체입니다. 나중에 가져올 경우 hello 관리자를 나타내는 개체를 준비 하는 hello hello 개체 틀을 덮어씁니다.

### <a name="metaverse-objects"></a>메타버스 개체
Hello 집계 뷰를 포함 하는 메타 버스 개체에 hello 커넥터 공간에 개체를 준비 하는 hello에 대 한 동기화 엔진이 해당 합니다. 동기화 엔진은 개체 가져오기에에서 hello 정보를 사용 하 여 메타 버스 개체를 만듭니다. 여러 커넥터 공간 개체에 연결 된 tooa 단일 메타 버스 개체 수는 있지만 커넥터 공간 개체에는 하나의 메타 버스 개체와 연결 된 toomore 일 수 없습니다.

메타버스 개체는 수동으로 생성 또는 삭제할 수 없습니다. hello 동기화 엔진 hello 커넥터 공간에 링크 tooany 커넥터 공간 개체를 포함 하지 않은 메타 버스 개체를 자동으로 삭제 합니다.

toomap hello 메타 버스에 연결 된 데이터 원본 tooa 해당 개체 형식 내에서 개체 동기화 엔진이 미리 정의 된 개체 유형과 연결 된 속성 집합이 있는 광범위 한 스키마를 제공합니다. 메타버스 개체에 대해 새 개체 유형 및 특성을 만들 수 있습니다. 단일 값 또는 다중값, 특성 일 수 및 문자열, 참조, 숫자 및 부울 값 hello 특성 유형이 될 수 있습니다.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>스테이징 개체 및 메타버스 개체 간의 관계
Hello 동기화 엔진 네임 스페이스 내에서 데이터 흐름 hello 준비 개체 및 메타 버스 개체 간의 링크 관계 hello로 사용 됩니다. 준비 되는 개체를 연결 된 tooa 메타 버스 개체 라고는 **조인된 개체** (또는 **커넥터 개체**). 연결 된 tooa 메타 버스 개체를 준비 개체 라고는 **개체 가입이 해제** (또는 **디스 커넥터 개체**). hello 용어 가입 및 분리는 기본 toonot 혼동 hello 커넥터 데이터 가져오기 및 내보내기 연결된 된 디렉터리에서 담당 합니다.

자리 표시자는 연결 된 tooa 메타 버스 개체

조인 된 개체가 준비 개체와 연결 된 관계 tooa 단일 메타 버스 개체 이루어집니다. 조인 된 개체는 커넥터 공간 개체와 메타 버스 개체 간에 사용 되는 toosynchronize 특성 값입니다.

준비 개체는 조인 된 개체를 동기화 하는 동안 되 면 특성 hello 준비 개체 및 hello 메타 버스 개체 간에 전달 될 수 있습니다. 특성 흐름은 양방향으로 수행되며 가져오기 및 내보내기 특성 규칙을 사용하여 구성합니다.

단일 커넥터 공간 개체에 연결 된 tooonly 하나의 메타 버스 개체 수 있습니다. 그러나 각 메타 버스 개체 hello 다음 그림에에서 나와 있는 것 처럼 hello 동일한 또는 다른 커넥터 공간에 연결 된 toomultiple 커넥터 공간 개체 수 있습니다.

![Arch5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

hello hello 준비 개체 간의 관계를 연결 및 메타 버스 개체 지속적이 고 지정 하는 규칙으로만 제거할 수 있습니다.

연결 되지 않은 개체에 연결 된 tooany 메타 버스 개체를 준비 개체가입니다. 연결 되지 않은 개체의 값이 다르면 hello 특성을 처리 하 hello 메타 버스 내에서 모든 추가 합니다. 안녕 특성 동기화 엔진에 의해 hello hello 연결 된 데이터 원본에 해당 개체의 값이 업데이트 되지 않습니다.

조인되지 않은 개체를 사용하여 ID 정보를 동기화 엔진에 저장하고 나중에 처리할 수 있습니다. Hello 커넥터 공간에 연결 되지 않은 개체 노드로 준비 개체 유지 많은 이점이 있습니다. Hello 시스템에 이미이 개체에 대 한 hello 필요한 정보, 단계별 때문에 필요한 toocreate hello 시 다시이 개체의 표현을 다음 hello 연결 된 데이터 원본에서 가져올지 않습니다. 이러한 방식으로 동기화 엔진 항상에 완전 한 스냅숏이 hello 연결 된 데이터 소스의 현재 연결 toohello 연결 된 데이터 원본에 없는 경우에 있습니다. 연결 되지 않은 개체는 지정 하는 hello 규칙에 따라 조인 된 개체로 또는 그 반대로 변환할 수 있습니다.

가져오기 개체는 조인되지 않은 개체로 만들어집니다. 내보내기 개체에 조인된 개체여야 합니다. 이 규칙 적용은 조인 된 개체가 아닙니다. 모든 내보내기 개체를 삭제 하는 hello 시스템 논리입니다.

## <a name="sync-engine-identity-management-process"></a>동기화 엔진 ID 관리 프로세스
hello identity 관리 프로세스는 서로 다른 연결 된 데이터 원본 간에 id 정보 업데이트 되는 방법을 제어 합니다. ID 관리는 세 가지 프로세스에서 발생합니다.

* 가져오기
* 동기화
* 내보내기

Hello 가져오기 프로세스 동안 동기화 엔진이 hello 연결된 된 데이터 원본에서 들어오는 id 정보를 평가합니다. 변경이 감지 되 면 준비 개체를 새로 만듭니다 하거나 기존 준비 동기화에 대 한 hello 커넥터 공간 개체를 업데이트 합니다.

Hello 동기화 프로세스 동안 동기화 엔진 hello 커넥터 공간에서 발생 한 hello 메타 버스 tooreflect 변경 업데이트 하 고 hello 메타 버스에서 발생 한 hello 커넥터 공간 tooreflect 변경 업데이트 합니다.

Hello 내보내기 프로세스 동안 동기화 엔진이 개체를 준비에 준비 된 하 고 보류 중인 내보내기도 플래그가 지정 하는 변경 내용을 푸시합니다.

hello 다음 그림에서는 각 hello 프로세스 발생 identity 정보 흐름으로 연결 된 데이터 원본 tooanother에서 보여 줍니다.

![Arch6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>가져오기 프로세스
Hello 가져오기 프로세스 동안 동기화 엔진이 업데이트 tooidentity 정보를 평가합니다. 동기화 엔진 개체를 준비 하는 방법에 대 한 hello id 정보를 사용 하는 hello 연결 된 데이터 원본에서 받은 hello id 정보를 비교 하 고 개체를 준비 하는 hello 업데이트가 필요한 지 여부를 결정 합니다. 개체에 새 데이터를 준비 하는 필요한 tooupdate hello 이면 hello 준비 개체 가져오기 보류 중으로 플래그가 지정 됩니다.

동기화 하기 전에 hello 커넥터 공간에 개체를 준비 하 여 동기화 엔진만 hello identity 변경 된 정보를 처리할 수 있습니다. 이 프로세스 hello를 다음 이점을 제공 합니다.

* **효율적인 동기화**. hello 동기화 하는 동안 처리 된 데이터 양을 최소화 됩니다.
* **효율적인 재동기화**. 동기화 엔진에서 다시 연결 중인 hello 동기화 엔진 toohello 데이터 원본 없이 id 정보를 처리 하는 방법을 변경할 수 있습니다.
* **기회 toopreview 동기화**합니다. 동기화 tooverify hello identity 관리 프로세스에 대 한 가정을 정확한 지를 미리 볼 수 있습니다.

Hello 커넥터에에서 지정 된 각 개체에 대해 동기화 엔진이 hello toolocate hello 커넥터의 커넥터 공간 hello에에서 hello 개체의 표현을 먼저 시도 합니다. 동기화 엔진이 hello 커넥터 공간에 대 한 모든 준비 개체를 검사 한 toofind 일치 하는 앵커 특성을 가진 해당 준비 개체를 시도 합니다. 일치 하는 특성을 고정, 동기화 엔진 시도 toofind hello로 준비는 해당 개체를 갖는 기존 준비 개체가 동일한 고유 이름입니다.

동기화 엔진이 앵커는 아니라 고유 이름으로 일치 하는 준비 개체를 찾으면 hello 다음과 같은 특별 한 동작이 수행 됩니다.

* 연결 된 tooas 경우 없는 앵커를 포함 하는 hello 커넥터 공간에 있는 hello 개체 hello 커넥터 공간에서이 개체를 제거 하는 동기화 엔진 및 표시 hello 메타 버스 개체 이기 **실행 된 다음 동기화에서 프로 비전을 다시 시도**합니다. 그런 다음 hello 새 가져오기 개체를 만듭니다.
* Hello 커넥터 공간에 있는 hello 개체 앵커 있으면는이 개체 중 이름이 변경 되거나 삭제 된 hello 연결 된 디렉터리에서 동기화 엔진 가정 합니다. Hello 커넥터 공간 개체에 대 한 임시, 새 고유 이름을 할당 하는 hello 들어오는 개체를 준비할 수 있도록 합니다. hello 이전 개체 되 고 **일시적인**, 상황에 적합 한 hello 커넥터 tooimport hello 이름 바꾸기 또는 삭제 tooresolve hello 대기 합니다.

동기화 엔진이 hello 커넥터에에서 지정 된 toohello 개체를 해당 하는 준비 개체를 찾은 경우에 어떤 종류의 변경 내용 tooapply 결정 합니다. 예를 들어 동기화 엔진이 이름을 바꾸거나 hello hello 연결 된 데이터 원본 개체를 삭제할 수 있습니다 또는 hello 개체의 특성 값을만 업데이트할 수 있습니다.

업데이트된 데이터가 있는 스테이징 개체는 보류 중인 가져오기로 표시됩니다. 다양한 유형의 보류 중인 가져오기가 제공됩니다. Hello hello 가져오기 프로세스의 결과 따라 hello 커넥터 공간에서 준비 개체의 보류 중인 가져오기 유형만 hello 다음과 같습니다.

* **없음**. 사용할 수 있는 개체를 준비 하는 hello hello 특성의 변경 내용을 tooany 없습니다. 동기화 엔진은 이 유형을 보류 중인 가져오기로 플래그 지정하지 않습니다.
* **추가**. hello 준비 개체에 hello 커넥터 공간의 새 가져오기 개체입니다. 동기화 엔진 플래그 가져오기 hello 메타 버스의 추가 처리를 위해 보류 중인이 형식을 지정 합니다.
* **업데이트**. 동기화 엔진이 hello 커넥터 공간에는 해당 준비 개체를 찾아 업데이트 toohello 특성 hello 메타 버스에서 처리할 수 있도록 가져오기 보류 중인 대로이 형식에 플래그를 지정 합니다. 업데이트에는 개체 이름 바꾸기가 포함됩니다.
* **삭제**. 동기화 엔진이 hello 커넥터 공간에는 해당 준비 개체를 찾아 hello 조인된 개체 수를 삭제할 수 있도록 가져오기 보류 중인 대로이 형식에 플래그를 지정 합니다.
* **삭제/추가**. 동기화 엔진이 hello 커넥터 공간에 해당 준비 개체를 찾았지만 hello 개체 형식이 일치 하지 않습니다. 이 경우에 삭제-추가 수정을 준비합니다. A delete-추가 수정이이 개체의 전체 다시 동기화 hello 개체 유형 변경 될 때 다른 규칙 집합을 toothis 개체를 적용 하기 때문에 발생 해야 하는 toohello 동기화 엔진을 나타냅니다.

보류 중인 준비 개체의 가져오기 상태 hello 설정으로 가능한 이므로 tooreduce에 사용할 수 있습니다 hello 시스템 tooprocess 데이터 업데이트 된 개체에만 때문에 동기화 하는 동안 처리 된 데이터 양이 크게 hello 합니다.

### <a name="synchronization-process"></a>동기화 프로세스
동기화는 두 개의 관련된 프로세스로 구성됩니다.

* 인바운드 동기화, hello 커넥터 공간에 hello 데이터를 사용 하 여 hello 메타 버스의 hello 콘텐츠가 업데이트 될 때 지정 합니다.
* 아웃 바운드 동기화, hello 메타 버스의 데이터를 사용 하 여 hello 커넥터 공간의 hello 콘텐츠가 업데이트 될 때 지정 합니다.

Hello 커넥터 공간에 준비 된 hello 정보를 사용 하 여 hello 인바운드 동기화 프로세스에에서 만듭니다 hello 연결 된 데이터 원본에 저장 하는 hello 데이터의 hello 메타 버스 hello 통합 보기입니다. Hello 규칙의 구성에 따라 모든 준비 개체 또는 보류 중인 가져오기 정보로 필드만 집계 됩니다.

아웃 바운드 동기화 프로세스 업데이트 hello 메타 버스 개체가 변경 될 때 개체를 내보냅니다.

인바운드 동기화 hello 연결 된 데이터 원본에서 받은 hello id 정보의 hello 메타 버스의 hello 통합 뷰를 만듭니다. 동기화 엔진이 hello 최신 id 정보는 hello에서 연결한 데이터 소스를 사용 하 여 언제 든 지 id 정보를 처리할 수 있습니다.

**인바운드 동기화**

인바운드 동기화 프로세스를 수행 하는 hello를 포함 되어 있습니다.

* **프로 비전** (호출 또한 **프로젝션** 이 프로세스에서 중요 한 toodistinguish이 아웃 바운드 동기화 프로 비전). hello 동기화 엔진이 스테이징 개체에 따라 새 메타 버스 개체를 만들고 연결 하 합니다. 프로비전은 개체 수준의 작업입니다.
* **조인**. 동기화 엔진이 hello 준비 개체 tooan 기존 메타 버스 개체를 연결합니다. 조인은 개체 수준 작업입니다.
* **가져오기 특성 흐름**. 동기화 엔진 hello 메타 버스의 hello 개체의 특성 흐름 라는 hello 특성 값을 업데이트 합니다. 가져오기 특성 흐름은 스테이징 개체와 메타버스 개체 간의 연결이 필요한 특성 수준 작업입니다.

프로 비전은 hello 메타 버스의 개체를 생성 하는 hello 유일한 프로세스입니다. 프로비전은 조인되지 않은 개체인 가져오기 개체에만 영향을 줍니다. 프로 비전 하는 동안 동기화 엔진은 hello 가져오기 개체의 toohello 개체 형식을 해당 하는 조인된 개체를 만들어서 두 개체 간의 연결을 설정 하는 메타 버스 개체를 만듭니다.

hello 조인 프로세스는 또한 개체 및 가져오기는 메타 버스 개체 간에 연결을 설정 합니다. 조인 및 프로덕션용 제공의 hello 차이점 hello 가입 프로세스 해당 hello 가져오기 개체는 연결 된 tooan 기존 메타 버스 개체를 hello 프로 비전 프로세스에서 새 메타 버스 개체를 만드는 해야 한다는 것입니다.

동기화 엔진 hello 동기화 규칙 구성에 지정 된 조건을 사용 하 여 toojoin 가져오기 개체 tooa 메타 버스 개체를 시도 합니다.

Hello 프로 비전 및 조인 프로세스 동안 동기화 엔진이 가입와 연결 되지 않은 개체 tooa 메타 버스 개체를 연결 합니다. 이러한 개체 수준 작업을 완료 한 후 동기화 엔진이 hello 연결 된 메타 버스 개체의 hello 특성 값을 업데이트할 수 있습니다. 이 프로세스를 가져오기 특성 흐름이라고 합니다.

가져오기 특성 흐름 연결된 tooa 메타 버스 개체 되며 새 데이터를 전송 하는 모든 가져오기 개체에서 발생 합니다.

**아웃바운드 동기화**

아웃바운드 동기화는 메타버스 개체가 변경되지만 삭제되지 않은 경우 내보내기 개체를 업데이트합니다. hello 아웃 바운드 동기화의 목적은 tooevaluate toometaverse 개체 변경 내용을 업데이트 toostaging 개체 hello 커넥터 공간의 여부입니다. 경우에 따라 hello 변경 준비 모든 커넥터 공간의 개체가 하 요구할 수 업데이트할 수 있습니다. 변경된 스테이징 개체는 보류 중인 내보내기로 플래그 지정되어 내보내기 개체가 됩니다. 이러한 내보내기 hello 내보내기 프로세스 중 toohello에 연결 된 데이터 소스 개체는 나중에 푸시됩니다.

아웃바운드 동기화에는 세 가지 프로세스가 있습니다.

* **프로비전**
* **프로비전 해제**
* **내보내기 특성 흐름**

프로비전 및 프로비전 해제는 모두 개체 수준 작업입니다. 프로비전 해제는 프로비전에서만 시작할 수 있으므로 프로비전에 따라 결정됩니다. 프로 비전 해제 메타 버스 개체와 내보내기 개체 간의 제거 hello 링크를 프로 비전 할 때 트리거됩니다.

프로 비전은 변경 내용이 적용 된 tooobjects hello 메타 버스의 경우에 트리거됩니다 항상 합니다. Toometaverse 개체 변경 되 면 hello 프로 비전 프로세스의 일부로 작업을 수행 하는 hello의 동기화 엔진 수행해 보십시오.

* 여기서는 메타 버스 개체는 새로 만든 연결 된 tooa 내보내기 개체, 조인 된 개체를 만듭니다.
* 조인된 개체의 이름을 바꿉니다.
* 메타버스 개체와 스테이징 개체 간의 연결을 조인 해제하여 조인되지 않은 개체가 만들어집니다.

동기화 엔진 toocreate 새 커넥터 개체를 프로 비전 해야 하는 경우 hello 준비 개체 toowhich hello 메타 버스 개체는 연결 된 내보내기 개체 때문에 항상은 hello 개체 hello 연결 된 데이터 원본에 아직 존재 하지 않는 합니다.

동기화 엔진 toodisjoin 연결 되지 않은 개체를 만들어 조인 된 개체를 프로 비전 하려면 해야 하는 경우 프로 비전 해제 트리거됩니다. 프로세스를 프로 비전 해제 하는 hello hello 개체를 삭제 합니다.

를 프로 비전 해제 하는 동안 내보내기 개체를 삭제 하더라도 hello 개체 물리적으로 삭제 되지 않습니다. hello 개체도 플래그가 지정 되어 **삭제**, hello 개체에 해당 hello 삭제 작업을 의미 하는 준비 합니다.

내보내기 특성 흐름에도 hello 아웃 바운드 동기화 프로세스 중 발생 특성 흐름을 가져올 비슷한 toohello 방식으로 인바운드 동기화 중에 발생 합니다. 내보내기 특성 흐름은 조인된 메타버스와 내보내기 개체 간에만 발생합니다.

### <a name="export-process"></a>내보내기 프로세스
Hello 내보내기 프로세스 동안 동기화 엔진이 내보내기 hello 커넥터 공간에 보류 중인으로 플래그가 지정 되는 모든 내보내기 개체를 검사 하 고 보냅니다 업데이트 toohello 연결 된 데이터 원본.

hello 동기화 엔진이 내보내기의 hello 성공 여부를 확인할 수 있지만 hello 식별 관리 프로세스가 완료 되었음을 확인할 충분히 수 없습니다. Hello 연결 된 데이터 원본에 개체는 항상 다른 프로세스에서 변경할 수 있습니다. 동기화 엔진에 영구 연결 toohello 연결 된 데이터 원본을 찾을 수 없기 때문에 정상적으로 내보내면 알림 기반 hello 연결 된 데이터 원본에 있는 개체의 hello 속성에 대 한 충분 한 toomake 가정을 않습니다.

예를 들어 프로세스 hello에 연결 된 데이터 원본 변경 hello 개체의 특성 백업 못했습니다 tootheir 원래 값 (즉, hello 연결 된 데이터 원본 수 값을 덮어쓰려면 hello 및 성공적으로 동기화 엔진에 의해 hello 데이터를 로그 아웃 밀어넣을 직후 적용 hello 연결 된 데이터 원본에).

hello 동기화 엔진 저장소가 내보내고 준비 각 개체에 대 한 상태 정보를 가져옵니다. Hello 특성 포함 목록에 지정 된 hello 특성의 값 hello 마지막으로 내보내기 이후 변경 되 면 hello 가져오기의 저장소를 사용 하면 동기화 엔진이 tooreact 상태를 적절 하 게 내보냅니다. 동기화 엔진 hello 프로세스 tooconfirm 특성 값 가져오기는 내보낸된 toohello 연결 된 데이터 소스를 사용 합니다. Hello 간 비교를 가져오고 내보낸된 정보 hello 다음 그림에에서 나와 있는 것 처럼 사용 하면 동기화 엔진이 toodetermine hello 내보내기 성공 했는지 또는 반복 toobe 필요한 경우.

![Arch7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

예를 들어 동기화 엔진 내보냅니다 특성 값이 5, C tooa 연결 된 데이터 원본, C = 5 내보내기 상태 메모리에 저장 합니다. 이 개체에 각 추가 내보내기 (즉, 아닌 경우 다른 값을 가져온 최근에이 값이 영구적으로 적용 된 toohello 개체는 된 동기화 엔진이 가정 하기 때문에 다시 시도 tooexport C = 5 toohello 연결 된 데이터 원본에 결과 hello에서 연결 된 데이터 원본). C = 5 hello 개체에서 가져오기 작업 중에 받은 hello 내보내기 메모리가 지워집니다.

## <a name="next-steps"></a>다음 단계
Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.

[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.

