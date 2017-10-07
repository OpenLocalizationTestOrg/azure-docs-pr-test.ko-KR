---
title: "Azure AD Connect 동기화: 기술 개념 | Microsoft Docs"
description: "Hello의 Azure AD Connect sync 기술 개념에 설명합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Azure AD Connect Sync: 기술 개념
이 문서는 hello 항목의 요약 [이해 아키텍처](active-directory-aadconnectsync-technical-concepts.md)합니다.

Azure AD Connect 동기화는 견고한 메타 디렉터리 동기화 플랫폼상에 빌드됩니다.
다음 섹션 hello 메타 디렉터리 동기화에 대 한 hello 개념을 소개 합니다.
MIIS, ILM 및 FIM을 높이고 hello Azure Active Directory Sync Services hello 다음 플랫폼을 제공 연결 toodata 원본에 대 한 프로 비전 및 프로 비전 해제를 id의 hello 뿐만 아니라 데이터 소스 간의 데이터 동기화 합니다.

![기술 개념](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

hello FIM 동기화 서비스의 측면을 따라 hello에 대 한 자세한 정보를 제공 하는 다음 섹션 hello:

* 커넥터
* 특성 이름
* 커넥터 공간
* 메타 버스
* 프로비전

## <a name="connector"></a>커넥터
연결된 된 디렉터리를 사용 하는 toocommunicate hello 코드 모듈이 커넥터 (이전의 Ma (관리 에이전트)) 이라고 합니다.

이러한 작업은 Azure AD Connect 동기화를 실행 하는 hello 컴퓨터에 설치 됩니다. hello 커넥터는 전문된 에이전트 배포 hello에 의존 하지 않고 원격 시스템 프로토콜을 사용 하 여 에이전트 없는 능력 tooconverse hello를 제공 합니다. 따라서 특히 중요한 응용 프로그램 및 시스템을 다룰 때 위험성과 배포 시간이 감소합니다.

위 hello 그림 hello 커넥터 hello 커넥터 공간과 동의어 이지만 hello 외부 시스템과 모든 통신을 포함 합니다.

hello 커넥터는 처리에 대 한 모든 가져오기 및 내보내기 기능 toohello 시스템 toounderstand 어떻게 않아도 개발자 해제 tooconnect tooeach 시스템 선언적 프로비저닝 toocustomize 데이터 변환을 사용 하는 경우에 고유 하 게 합니다.

가져오기 및 내보내기 경우에 발생할 실행 되도록 예약 된 변경은 toohello 연결 된 데이터 소스를 자동으로 전파 되지 않습니다 이후 hello 시스템 내에서 발생 한 변경 내용 으로부터 단절 추가 허용 합니다. 또한 개발자는 toovirtually 모든 데이터 원본 연결 하기 위한 자체의 커넥터를 만들 수도 수 있습니다.

## <a name="attribute-flow"></a>특성 이름
hello 메타 버스는 인접 커넥터 공간에서 모든 조인 된 id의 hello 통합 뷰입니다. 위 hello 그림 특성 흐름은 인바운드 및 아웃 바운드 흐름에 대 한 화살촉이 있는 선으로 표시 됩니다. 특성 흐름은 복사 나 tooanother 하나의 시스템에서에서 데이터 변환을의 hello 프로세스 및 모든 특성 흐름 (인바운드 또는 아웃 바운드).

특성 흐름 발생 hello 커넥터 공간과 메타 버스 hello 간의 양방향으로 동기화 (전체 또는 델타) 작업은 예약 된 toorun 때 합니다.

특성 흐름은 이러한 동기화가 실행되는 경우에만 발생합니다. 특성 흐름은 동기화 규칙에 정의되어 있습니다. 인바운드 (위 hello 그림의 ISR) 또는 아웃 바운드 (위 hello 그림에서 OSR) 수 있습니다.

## <a name="connected-system"></a>연결된 시스템
연결 된 시스템 (즉, 연결 된 디렉터리)가 참조 toohello 원격 시스템 Azure AD Connect 동기화 tooand 읽기 및 쓰기에서 identity 데이터 tooand 연결 되었습니다.

## <a name="connector-space"></a>커넥터 공간
각 연결 된 데이터 원본 커넥터 공간의 hello의 hello 개체 및 특성의 필터링된 된 하위 집합으로 표시 됩니다.
이 hello 필요 toocontact hello 원격 시스템 하지 않고 로컬 hello 동기화 서비스 toooperate hello 개체를 동기화 할 때와 상호 작용 tooimports 제한를 통해만 내보냅니다.

Hello 데이터 소스와 hello 커넥터가 hello 기능 tooprovide (델타 가져오기) 변경 내용 목록은 때 다음 hello 운영 효율성 증가 크게 hello 마지막 폴링 이후 변경 된 내용만 주기로 교환 됩니다. hello 커넥터 공간 해당 hello 커넥터 일정 가져옵니다 요구 및 내보내기에 의해 자동으로 전파 된 변경 내용에서 연결 된 데이터 원본 hello을 분리 합니다. 이러한 추가 된 보호 테스트, 미기 보기 또는 hello 다음 업데이트를 확인 하는 동안을 부여 합니다.

## <a name="metaverse"></a>메타 버스
hello 메타 버스는 인접 커넥터 공간에서 모든 조인 된 id의 hello 통합 뷰입니다.

을 identities 함께 연결 되 고 가져오기 흐름 매핑을 통해 다양 한 특성에 대 한 권한이 할당 되므로 hello 중앙 메타 버스 개체는 여러 시스템에서 tooaggregate 정보를 시작 합니다. 이 개체 특성 흐름에서 매핑은 정보 toooutbound 시스템을 수행합니다.

개체는 신뢰할 수 있는 시스템 hello 메타 버스에 투영할 때 만들어집니다. 모든 연결이 제거 되는 즉시 hello 메타 버스 개체가 삭제 됩니다.

Hello 메타 버스의 개체를 직접 편집할 수 없습니다. Hello 개체의 모든 데이터는 특성 흐름을 통해 제공 되어야 합니다. hello 메타 버스에는 각 커넥터 공간과 영구 커넥터 유지 관리합니다. 이러한 커넥터는 각 동기화 실행에 대해 다시 평가할 필요가 없습니다. 즉, Azure AD Connect 동기화 하지 않았는지 toolocate hello 일치 하는 원격 개체 때마다. 따라서 일반적으로 수 hello 개체를 상호 연결 하는 일을 담당 하는 비용이 드는 에이전트가 tooprevent 변경 tooattributes hello 필요가 없습니다.

때 프로세스 toobe 관리, Azure AD Connect 동기화를 사용 해야 하는 기존 개체를 가질 수 있는 새 데이터 원본을 검색할는 조인 규칙 tooevaluate 잠재적 대상을 어떤 tooestablish 링크 라고 합니다.
이 평가가 다시 수행 되지 hello 링크가 설정 되 고 hello 원격 연결 된 데이터 원본과 hello 메타 버스 간에 정상 특성 흐름이 발생할 수 있습니다.

## <a name="provisioning"></a>프로비전
신뢰할 수 있는 소스 프로젝트 때 다운스트림 연결된 데이터 원본을 나타내는 다른 커넥터에서 hello 메타 버스 새 커넥터 공간 개체에 새 개체를 만들 수 있습니다.

그러면 고유하게 링크가 설정되고 특성 흐름이 양방향으로 진행될 수 있습니다.

새 커넥터 공간 개체를 만든 toobe 필요 함을 확인 하는 규칙 경우 때마다 프로 비전 호출 됩니다. 그러나를 하기 때문에이 작업만 hello 커넥터 공간 내에서 그는 적용 되지 않으므로 hello 연결 된 데이터 소스에 내보내기를 수행 될 때까지 합니다.

## <a name="additional-resources"></a>추가 리소스
* [Azure AD Connect Sync: 사용자 지정 동기화 옵션](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
