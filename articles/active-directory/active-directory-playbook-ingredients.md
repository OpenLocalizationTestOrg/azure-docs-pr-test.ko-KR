---
title: "Active Directory PoC 플레이 북 재료 aaaAzure | Microsoft Docs"
description: "ID 및 액세스 관리 시나리오를 탐색하고 신속하게 구현"
services: active-directory
keywords: "Azure Active Directory, 플레이 북, 개념 증명, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Azure Active Directory 개념 증명 플레이 북 구성 

## <a name="theme"></a>테마
Azure AD는 hello 기업에서 여러 영역 id 및 액세스 솔루션을 제공 합니다. Hello 다음 영역에서에서 hello 시나리오 분류 했습니다:. 

* [다수의 앱, 하나의 ID](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [보안 향상](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [셀프 서비스에 맞게 크기 조정](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

테마 tooframe hello PoC toofocus hello 활동을 사용 하면 비즈니스 목표와 받아들일를 정의는 종종 된 hello 트리거가 hello 먼저에서 개념 증명에 hello 관심 있습니다. 

## <a name="environment"></a>Environment

Hello PoC를 제공 하는 위치는 hello 환경의 중요 toodetermine hello 세부 정보는 이상적으로 hello PoC 완료 된 후에 작성할 수 있습니다. hello 대상 환경은 중요와 같이 실제 가능한 것과 제약 조건 또는 추가 고려 사항을 hello 오버 헤드를 만드는 사이의 hello 적절 한 균형을 찾아야 합니다. hello PoCs에 대 한 일반적인 환경은 다음과 같습니다.
* **프로덕션:** hello 시나리오 라이브 환경에서 구현 될 및 이미 Microsoft 클라우드 서비스 (프로덕션 AD Office 365, Azure AD 테 넌 트/SSO 솔루션)을 배포 합니다. 
* **UAT(사용자 수용 테스트)/개발 환경:** 프로덕션과 유사한 테스트 데이터를 포함하는 테스트 인프라(병렬 AD 및 잠재적으로 Azure AD 테넌트/SSO 솔루션)가 있습니다. 일반적으로 hello 테스트 환경 hello 엔터프라이즈에서 여러 프로젝트 간에 공유 됩니다.

이 가이드의 시나리오 대부분은 기본적으로 추가가 가능합니다. 결과적으로 배포 될 수 hello 프로덕션 테 넌 트에 hello PoC 외부 사용자가 영향을 주지 않고 합니다. 이 문서 전체에서는 테넌트 차원에서 영향을 미치는 시나리오를 살펴볼 것입니다. 이러한 경우에는 비-프로덕션 환경 tooconsider를 할 수 있습니다. 


## <a name="target-users"></a>대상 사용자

hello 환경은 프로덕션 또는 테스트 하는 경우에 특히 hello 시나리오를 실행 하는 사용자의 중요 한 toodetermine hello 대상 집합입니다. PoC에 대 한 대상 사용자의 hello 범주는 있습니다.
* **파일럿 사용자:** hello 솔루션에서 사용 하는 해당 일 tooday hello 계정으로 사용 하 여 hello 환경에서 실제 사용자에 게 작업 함수
* **테스트 사용자:** hello 환경에서 만든 계정을 테스트 

이 가이드의 시나리오 대부분은 파일럿 사용자가 실행할 수 있습니다. 이 문서 전체에서는 필요할 때 대상 사용자 고려 사항을 언급합니다.


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]