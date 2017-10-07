---
title: "가 중 aaaConfigure 라운드 로빈 트래픽 라우팅 방법 Azure 트래픽 관리자를 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 tooload 트래픽 관리자의 라운드 로빈 메서드를 사용 하 여 트래픽을 분산 하는 방법을 설명 합니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a>트래픽 관리자의가 중 hello 트래픽 라우팅 방법 구성

일반적인 트래픽 라우팅 메서드 패턴은 tooprovide 클라우드 서비스 및 웹 사이트를 포함 하는 라운드 로빈 방식으로 트래픽을 tooeach 보낼 동일한 끝점의 집합입니다. 단계를 수행 하는 hello 어떻게 tooconfigure이 유형의 설명 트래픽 라우팅 방법입니다.

> [!NOTE]
> Azure Websites는 데이터 센터(지역이라고도 함) 내의 웹 사이트에 대해 이미 라운드 로빈 부하 분산 기능을 제공합니다. 트래픽 관리자 다른 데이터 센터의 웹 사이트에 대 한 라운드 로빈 트래픽 라우팅 방법을 toospecify를 사용 합니다.

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a>tooconfigure 가중치 hello 트래픽 라우팅 방법

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다. 아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다. 
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** tooconfigure hello에 대 한 라우팅 메서드를 원하는 hello 프로필 이름을 클릭 하 고 있습니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드를 둘 다 hello 클라우드 서비스를 구성에서 tooinclude 되도록 웹 사이트를 사용할 수 있는지 확인 합니다.
4. Hello에 **설정** 섹션에서 클릭 **구성**, 및 hello **구성** 블레이드를 다음과 같이 완료:
    1. 에 대 한 **트래픽 라우팅 방법 설정**, hello 트래픽 라우팅 방법 인지 확인 **가 중**합니다. 없는 경우 클릭 **가 중** hello 드롭다운 목록에서 합니다.
    2. 집합 hello **끝점 모니터 설정** 다음과 같이이 프로필 내의 모든 모든 끝점에 대해 동일 합니다.
        1. 적절 한 선택 hello **프로토콜**, hello 지정 **포트** 번호입니다. 
        2. **경로**에서 슬래시  */* 를 입력합니다. toomonitor 끝점 경로 파일 이름을 지정 해야 합니다. A 슬래시 "/" hello 상대 경로 대 한 유효한 항목 및 hello이 파일은 hello 루트 디렉터리 (기본값)를 의미 합니다.
        3. Hello hello 페이지의 위쪽에 클릭 **저장**합니다.
5. 다음과 같이 구성에서 hello 변경 내용 테스트:
    1.  Hello 포털 검색 표시줄에 hello 트래픽 관리자 프로필 이름을 검색 하 고 표시 하는 hello hello 결과에 hello 트래픽 관리자 프로필을 클릭 합니다.
    2.  Hello에 **트래픽 관리자** 블레이드 프로필을 클릭 하 여 **개요**합니다.
    3.  hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다. 이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다. 이 경우 모든 요청이 라운드 로빈 방식으로 각 끝점에 라우팅됩니다.
6. 트래픽 관리자 프로필 작동 되 면 hello DNS 레코드에 권한 있는 DNS 서버 toopoint에 회사 도메인 이름 toohello 트래픽 관리자 도메인 이름을 편집 합니다.

![Traffic Manager를 사용한 가중치 적용 트래픽 라우팅 방법 구성][1]

## <a name="next-steps"></a>다음 단계

- [우선 순위 트래픽 라우팅 방법](traffic-manager-configure-priority-routing-method.md)에 대해 알아보세요.
- [성능 트래픽 라우팅 방법](traffic-manager-configure-performance-routing-method.md)에 대해 알아보세요.
- [지리적 라우팅 방법](traffic-manager-configure-geographic-routing-method.md)에 대해 알아보세요.
- 너무 방법에 대해 알아봅니다[트래픽 관리자 설정을 테스트](traffic-manager-testing-settings.md)합니다.

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
