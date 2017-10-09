---
title: "aaaConfigure 성능 트래픽 라우팅 방법 Azure 트래픽 관리자를 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooconfigure 트래픽 관리자 tooroute 트래픽에만 toohello 끝점 대기 시간이 가장 짧은 설명"
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a>Hello 성능 트래픽 라우팅 방법 구성

hello 성능 트래픽 라우팅 방법을 hello 클라이언트의 네트워크에서 hello 가장 낮은 대기 시간으로 toodirect 트래픽 toohello 끝점을 허용 합니다. 일반적으로 hello 가장 낮은 대기 시간으로 hello 데이터 센터는 지리적으로 거리가 가장 가까운 hello 합니다. 이 트래픽 라우팅 방법은 네트워크 구성이나 로드의 실시간 변경 내용을 고려할 수 없습니다.

##  <a name="tooconfigure-performance-routing-method"></a>tooconfigure 성능 라우팅 방법

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다. 아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다. 
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** tooconfigure hello에 대 한 라우팅 메서드를 원하는 hello 프로필 이름을 클릭 하 고 있습니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드를 둘 다 hello 클라우드 서비스를 구성에서 tooinclude 되도록 웹 사이트를 사용할 수 있는지 확인 합니다.
4. Hello에 **설정** 섹션에서 클릭 **구성**, 및 hello **구성** 블레이드를 다음과 같이 완료:
    1. **트래픽 라우팅 방법 설정**의 경우 **라우팅 방법**에서 **성능**을 선택합니다.
    2. 집합 hello **끝점 모니터 설정** 다음과 같이이 프로필 내의 모든 모든 끝점에 대해 동일 합니다.
        1. 적절 한 선택 hello **프로토콜**, hello 지정 **포트** 번호입니다. 
        2. **경로**에서 슬래시  */* 를 입력합니다. toomonitor 끝점 경로 파일 이름을 지정 해야 합니다. A 슬래시 "/" hello 상대 경로 대 한 유효한 항목 및 hello이 파일은 hello 루트 디렉터리 (기본값)를 의미 합니다.
        3. Hello hello 페이지의 위쪽에 클릭 **저장**합니다.
5.  다음과 같이 구성에서 hello 변경 내용 테스트:
    1.  Hello 포털 검색 표시줄에 hello 트래픽 관리자 프로필 이름을 검색 하 고 표시 하는 hello hello 결과에 hello 트래픽 관리자 프로필을 클릭 합니다.
    2.  Hello에 **트래픽 관리자** 블레이드 프로필을 클릭 하 여 **개요**합니다.
    3.  hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다. 이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다. 이 경우 모든 요청은 hello 클라이언트의 네트워크에서 hello 가장 낮은 대기 시간으로 라우팅된 toohello 끝점입니다.
6. 트래픽 관리자 프로필 작동 되 면 hello DNS 레코드에 권한 있는 DNS 서버 toopoint에 회사 도메인 이름 toohello 트래픽 관리자 도메인 이름을 편집 합니다.

![Traffic Manager를 사용한 성능 트래픽 라우팅 방법 구성][1]

## <a name="next-steps"></a>다음 단계

- [가중치 적용 트래픽 라우팅 방법](traffic-manager-configure-weighted-routing-method.md)에 대해 알아보세요.
- [우선 순위 라우팅 방법](traffic-manager-configure-priority-routing-method.md)에 대해 알아보세요.
- [지리적 라우팅 방법](traffic-manager-configure-geographic-routing-method.md)에 대해 알아보세요.
- 너무 방법에 대해 알아봅니다[트래픽 관리자 설정을 테스트](traffic-manager-testing-settings.md)합니다.

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png