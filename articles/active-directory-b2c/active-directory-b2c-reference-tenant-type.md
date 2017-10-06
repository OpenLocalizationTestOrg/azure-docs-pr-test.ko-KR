---
title: "Azure Active Directory B2C: 지역 가용성 및 데이터 상주 | Microsoft Docs"
description: "Azure Active Directory B2C 테 넌 트의 hello 형식에 대 한 항목"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a>Azure Active Directory B2C: 지역 가용성 및 데이터 상주
지역 가용성과 데이터 상주는 Azure의 hello 나머지에서 AD B2C tooAzure 다르게 적용 되는 두 개의 매우 다른 개념입니다. 이 문서 hello 차이점 개념을 설명 하 고와 Azure AD B2C tooAzure를 적용 하는 방법을 비교 합니다.

## <a name="summary"></a>요약
Azure AD B2C은 **일반적으로 사용할 수 있는 전 세계** hello 옵션에 대 한 **미국이 나 유럽 데이터 상주**합니다.

## <a name="concepts"></a>개념
* **지역 가용성** toowhere 참조는 서비스를 사용 하기 위해 사용할 수 있습니다.
* **데이터 상주** 참조 toowhere 사용자 데이터가 저장 됩니다.

## <a name="region-availability"></a>지역 가용성
Azure AD B2C 제공 되며, 전 세계 hello Azure 공용 클라우드를 통해 

이 점에서 차이가 hello 모델 데이터 상주 가용성 연결 하는 대부분의 다른 Azure 서비스 수행 합니다. 두 Azure에서이 예제를 확인할 수 [제품 사용 가능한 하 여 지역](https://azure.microsoft.com/regions/services/) 페이지와 hello [Active Directory B2C 가격 계산기](https://azure.microsoft.com/pricing/details/active-directory-b2c/)합니다.

## <a name="data-residency"></a>데이터 상주
Azure AD B2C는 사용자 데이터를 미국 또는 유럽에 저장합니다.

데이터 상주는 [Azure AD B2C 테넌트](active-directory-b2c-get-started.md)를 만들 때 선택된 국가/지역에 따라 결정됩니다.

![미리 보기 테넌트의 스크린 샷](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

데이터가 다음 국가/지역의 hello에 대 한 hello 미국에 있습니다.

> 미국, 캐나다, 코스타리카, 도미니카 공화국, 엘살바도르, 과테말라, 멕시코, 파나마, 푸에르토리코, 트리니다드토바고

국가/지역의 다음 hello에 대 한 데이터가 유럽에 있습니다.

> 알제리, 오스트리아, 아제르바이잔, 바레인, 벨로루시, 벨기에, 불가리아, 크로아티아, 키프로스, 체코, 덴마크, 이집트, 에스토니아, 핀란드, 프랑스, 독일, 그리스, 헝가리, 아이슬란드, 아일랜드, 이스라엘, 이탈리아, 요르단, 카자흐스탄, 케냐, 쿠웨이트, 라트비아, 레바논, 리히텐슈타인, 리투아니아, 룩셈부르크, 마케도니아(FYROM), 몰타, 몬테네그로, 모로코, 네덜란드, 나이지리아, 노르웨이, 오만, 파키스탄, 폴란드, 포르투갈, 카타르, 루마니아, 러시아, 사우디아라비아, 세르비아, 슬로바키아, 슬로베니아, 남아프리카 공화국, 스페인, 스웨덴, 스위스, 튀니지, 터키, 우크라이나 아랍에미리트 및 영국.

hello 나머지 국가/지역에서 hello 프로세스 toohello 목록에 추가 되는 합니다.  지금은 Azure AD B2C hello 국가/지역 위의 중 하나를 선택 하 여 사용할 수 있습니다.

> 아프가니스탄, 아르헨티나, 오스트레일리아, 브라질, 칠레, 콜롬비아, 에콰도르, 홍콩 특별 행정구, 인도, 인도네시아, 이라크, 일본, 한국, 말레이시아, 뉴질랜드, 파라과이, 페루, 필리핀, 싱가포르, 스리랑카, 대만, 태국, 우루과이 및 베네수엘라.

## <a name="preview-tenant"></a>미리 보기 테넌트
Azure AD B2C 미리 보기 기간 동안 B2C 테넌트를 만든 경우 **테넌트 유형**은 **미리 보기 테넌트**라고 할 가능성이 있습니다. Hello 대/소문자 인 경우 개발 및 테스트 목적에 대해서만 하 고 프로덕션 응용 프로그램에 대해 테 넌 트를 사용 해야 합니다.

> [!IMPORTANT]
> B2C 테 넌 트 tooa 프로덕션 규모 B2C 테 넌 트 미리 보기에서 마이그레이션 경로가 없습니다. 미리 보기 B2C 테 넌 트를 삭제 하는 경우 알려진 문제 및 재생성이 다음 프로덕션 규모 B2C 테 넌 트에서 hello 동일한 도메인 이름입니다. Toocreate 다른 도메인 이름의 프로덕션 규모 B2C 테 넌 트를 해야합니다.


![미리 보기 테넌트의 스크린 샷](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
