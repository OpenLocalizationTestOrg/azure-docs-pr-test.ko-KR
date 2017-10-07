---
title: "일반적인 시나리오는 데이터 카탈로그 aaaAzure | Microsoft Docs"
description: "Azure Data Catalog를 hello 등록 및 중요 한 데이터 원본 검색을 포함 하 여 셀프 서비스 비즈니스 인텔리전스를 사용 하도록 설정 하 고 데이터 원본 및 프로세스에 대 한 기존 지식에 대 한 일반적인 시나리오의 개요."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 60930d78-d2d4-4d5d-9651-bdda50b0da0e
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: a9bd222bcf85abc31621ce7c09264a399fbb7a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-common-scenarios"></a>Azure 데이터 카탈로그 일반적인 시나리오
이 문서에서는 조직에서 Azure Data Catalog를 통해 기존 데이터 원본에서 더 많은 가치를 얻을 수 있는 일반적인 시나리오를 보여줍니다.

## <a name="scenario-1-registration-of-central-data-sources"></a>시나리오 1: 중앙 데이터 원본 등록
조직에는 종종 높은 가치의 데이터 원본이 많습니다. 이러한 데이터 원본으로는 기간 업무, OLTP(온라인 트랜잭션 처리) 시스템, 데이터 웨어하우스 및 비즈니스 인텔리전스/분석 데이터베이스가 있습니다. 여러 시스템 hello 서로 겹치는 hello, 일반적으로 시간이 갈수록 커집니다 업무상 필요 하 고 자체 hello 비즈니스 인수 / 합병과 예를 들어 통해 발전 합니다.

어려울 수 있습니다 멤버 tooknow 조직에 대 한 여기서 toolocate hello 이러한 데이터 원본 내에서 데이터입니다. Hello 다음과 같은 질문은 시키기:

* Hello의 세 가지 HR 시스템 내에서 사용 해야 합니까 hello 회사 사용 toocreate 이러한 종류의 보고서?
* 해야 곳 tooget hello 방금 끝낸 hello 회계 연도의 판매 수치가 인증
* 사용자를 문의 해야 합니까, 또는 tooget 액세스 toohello 데이터 웨어하우스를 사용 해야 하는 hello 프로세스는 무엇입니까?
* 이 숫자가 맞는지 모르겠습니다. 가 있습니까 통찰력에 요청 어떻게이 데이터와 팀이이 대시보드를 공유 하기 전에 사용 toobe?

toothese 및 기타 질문 답변 Azure Data Catalog에 제공할 수 있습니다. hello 중앙, 중요, 조직에서 사용 되는 IT 관리 데이터 소스는 hello hello 카탈로그를 채우기 위한 논리적 시작 지점 경우가 많습니다. 모든 사용자는 데이터 소스를 등록할 수, 있지만 도입을 촉진 및 hello 사용 지원 가능성이 가장 높은 tooprovide 값 toohello 가장 많은 사용자는 hello 데이터 원본과 kick-started hello 카탈로그 필요 합니다. 

Azure Data Catalog에 시작 하는, 식별 하 고 데이터 소비자의 여러 다른 팀에서 사용 되는 키 데이터 원본을 등록 하 여 첫 번째 단계 toosuccess 수 있습니다.

이 시나리오는 영업 기회 tooannotate hello 중요 한 데이터 원본 toomake 제공을 보다 쉽게 toounderstand 및 액세스 합니다. 이 위해의 중요 한 한 측면에는 사용자 toohello 데이터 원본 액세스를 요청할 수 있습니다 어떻게에 tooinclude 정보입니다. Azure Data catalog hello 사용자 또는 데이터 소스 액세스, 링크 tooexisting 도구 또는 설명서를 제어 하는 일을 담당 하는 팀 또는 hello 액세스 요청 프로세스를 설명 하는 일반 텍스트의 hello 전자 메일 주소를 제공할 수 있습니다. 등록 된 데이터 원본 검색 게 하지만 사용 권한을 tooaccess 아직 없는 멤버를 통해 정의 되 고 hello 데이터 원본 소유자가 제어 하는 hello 프로세스를 사용 하 여 데이터 tooeasily 액세스 요청 hello이 정보입니다.

## <a name="scenario-2-self-service-business-intelligence"></a>시나리오 2: 셀프서비스 비즈니스 인텔리전스
기존의 회사 비즈니스 인텔리전스 솔루션 toobe 계속 하지만 대부분의 조직 데이터의 중요 한 부분 지형의 비즈니스의 속도 변경 하는 hello 했습니다 셀프 서비스 BI 점점 더 중요 합니다. 셀프 서비스 BI를 사용하면 정보 근로자와 분석가는 중앙 IT 팀에 의존하거나 중앙 IT팀의 일정 및 가용성에 제약을 받지 않고 보고서, 통합 문서 및 대시보드를 만들 수 있습니다.

셀프 서비스 BI 시나리오에서는 사용자가 여러 소스의 데이터를 결합하는 것이 일반적이며, 이러한 소스 중 상당수는 이전에 BI 및 분석에 사용되지 않은 것입니다. 하지만 이러한 데이터 원본 중 일부 이미 알려질 수, 어려운 toodiscover 어떤 toodo toolocate 하 고 수 지정된 된 태스크에 대 한 잠재적인 데이터 소스를 평가 합니다.

일반적으로 이러한 검색 프로세스는 수동 1: 분석가 사용 하 여 해당 피어 네트워크 연결 tooidentify 검색 되는 hello 데이터로 작업 하는 다른 사용자입니다. 데이터 원본을 찾아 사용 후 hello 자동으로 반복 되어 다시 과정에 대 한 각 후속 셀프 서비스 BI 검색 하는 중복 수동 프로세스를 수행 하는 여러 사용자를 포함 합니다.

Azure Data Catalog를 사용하면 조직에서 이 반복되는 활동을 없앨 수 있습니다. 기존의 수단을 통해 데이터 소스를 검색 한 후이 경우 분석가 등록 toomake 것 hello 이후 다른 사용자가 더 쉽게 검색할 수 있습니다. 이 주석은 tootake 곳을 하지 않아도 hello 분석가 hello 등록 된 데이터 자산에 주석 지정으로 더 많은 가치를 추가할 수, 있지만 동일한 등록으로 시간 hello에 있습니다. 사용자가 점진적으로 hello 카달로그에 등록 하는 값 toohello 데이터 소스를 추가 하는 해당 일정 허용으로 시간이 지남에 따라 기여할 수 있습니다.

이 유기적 증가 hello 카탈로그 콘텐츠의 보완 합니다. toohello 선불을 등록 하는 중앙 데이터 원본의 경우 많은 사용자가 필요로 하는 데이터와 미리 채우는 hello 카탈로그 초기 사용 및 검색에 대 한 motivator 될 수 있습니다. 사용자가 tooregister를 사용 하도록 설정 하 고 주석을 추가할 추가 소스 및 기타 조직 구성원 참여 하는 방식으로 tookeep 될 수 있습니다.

적용 되는 셀프 서비스 BI에 대해 구체적으로이 시나리오에서는, hello 동일한 패턴 및 문제 toolarge 단위 기업 BI 프로젝트도 됩니다. Data Catalog를 사용하면 조직에서 데이터 원본 수동 검색 프로세스가 개입되는 모든 활동을 개선할 수 있습니다.

## <a name="scenario-3-capturing-tribal-knowledge"></a>시나리오 3: 조직에 관한 정보 찾기
데이터를 어떻게 알 수 있을까요 toodo 업무에 필요한 위치와 toofind 데이터?

일정 시간 동안 일하면 아마도 그냥 알게 될 것입니다. 시간이 지남에 따라 hello 있는 데이터 원본에 키 tooyour 일상적인 작업에 대 한 학습 상태 및 설정 프로세스를 점진적을 완료 한 있습니다.

새 직원 팀에 참여 하는 경우 해당 사용자를은 어떻게 hello 작업에 대 한 필수 데이터 인지 및 위치 toofind 것?

확률은 새 사람 hello tooyou 이러한 질문을 제공 합니다.

지식은이 진행 중인 전송에는 조직 규모에 hello 데이터 소스 검색 프로세스의 일부입니다. Hello 년간 기술 작성 수석 및 경력 전화 팀 멤버 및 최신 팀원 tooask 배웠습니다 질문이 있는 경우. 종종 정보 몇 가지 주요 사람의 hello 헤드에만 존재 있고 사람은 휴가 들어가거나 hello 팀 때 hello 조직에 가장 중요 한 번호입니다.

데이터 전문가 일반적으로 확인 노력 toodocument 자신의 지식을 팀 SharePoint 사이트에 있는 Word 문서 또는 전자 메일을 통해이 공유 합니다. 새로운 검색 문제가이 방법을 사용 하는 중요 하지만 소개: 사용자 하는 방법 알고 있는 어떤 설명서 및 위치 toofind 것?

Azure Data Catalog를 사용하면 중앙의 단일 위치에서 조직의 정보를 저장 및 공유하고 간편하게 검색할 수 있습니다. 데이터 카탈로그에 데이터 전문가 직접 데이터 자산 주석을 달 수 및 tooexisting 설명서 링크를 제공 합니다. 조직 구성원 hello 카탈로그 toodiscover 데이터 소스를 사용 하는 경우 찾게 됩니다 hello 소스 뿐 아니라 자체 뿐만 아니라 이전에 있던 hello 기술 조직의 전문가의 hello 사람들에만 합니다.
