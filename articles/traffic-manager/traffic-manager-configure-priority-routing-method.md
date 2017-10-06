---
title: "aaaConfigure 우선 순위 트래픽 라우팅 방법 Azure 트래픽 관리자를 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 tooconfigure hello 우선 순위 트래픽 라우팅 방법 트래픽 관리자에서 어떻게 설명"
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
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Traffic Manager에서 우선 순위 트래픽 라우팅 방법 구성

Hello 웹 사이트 모드에 관계 없이 Azure 웹 사이트는 데이터 센터 (지역이 라고도 함) 내 웹 사이트에 대 한 장애 조치 기능을 이미 제공합니다. Traffic Manager는 다른 데이터 센터의 웹 사이트에 대해 장애 조치(Failover)를 제공합니다.

일반적인 서비스 장애 조치 패턴 toosend 트래픽 tooa 기본 서비스 이며의 장애 조치에 대해 동일한 백업 서비스 집합을 제공 합니다. hello 다음 단계에서는 설명 어떻게 tooconfigure이 우선 순위가 지정 된 Azure 클라우드 서비스 및 웹 사이트 장애 조치:

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>tooconfigure hello 우선 순위 트래픽 라우팅 방법

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다. 아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다. 
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** tooconfigure hello에 대 한 라우팅 메서드를 원하는 hello 프로필 이름을 클릭 하 고 있습니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드를 둘 다 hello 클라우드 서비스를 구성에서 tooinclude 되도록 웹 사이트를 사용할 수 있는지 확인 합니다.
4. Hello에 **설정** 섹션에서 클릭 **구성**, 및 hello **구성** 블레이드를 다음과 같이 완료:
    1. 에 대 한 **트래픽 라우팅 방법 설정**, hello 트래픽 라우팅 방법 인지 확인 **우선 순위**합니다. 없는 경우 클릭 **우선 순위** hello 드롭다운 목록에서 합니다.
    2. 집합 hello **끝점 모니터 설정** 다음과 같이이 프로필 내의 모든 모든 끝점에 대해 동일 합니다.
        1. 적절 한 선택 hello **프로토콜**, hello 지정 **포트** 번호입니다. 
        2. **경로**에서 슬래시  */* 를 입력합니다. toomonitor 끝점 경로 파일 이름을 지정 해야 합니다. A 슬래시 "/" hello 상대 경로 대 한 유효한 항목 및 hello이 파일은 hello 루트 디렉터리 (기본값)를 의미 합니다.
        3. Hello hello 페이지의 위쪽에 클릭 **저장**합니다.
5. Hello에 **설정** 섹션에서 클릭 **끝점**합니다.
6. Hello에 **끝점** 블레이드를 끝점에 대 한 hello 우선 순위 순서를 검토 합니다. Hello를 선택 하는 경우 **우선 순위** 트래픽 라우팅 방법을 선택 하는 hello 끝점의 hello 순서가 중요 합니다. 끝점의 hello 우선 순위 순서를 확인 합니다.  hello 기본 끝점 위에 표시 됩니다. 표시 되는 hello 순서에 다시 확인 하십시오. 모든 요청 라우트된 toohello 첫 번째 끝점을 트래픽 관리자에서 감지할 경우 수 정상, hello 트래픽 toohello 다음 끝점을 통해 자동으로 실패 합니다. 
7. toochange hello 끝점 우선 순위 순서를 hello 끝점을 클릭 하 고 hello에 **끝점** 블레이드에 표시 되는 클릭 **편집** hello를 변경 하 고 **우선 순위** 필요에 따라 값 . 
8. 클릭 **저장** toosave hello 끝점 설정을 변경 합니다.
9. 구성 변경을 완료 한 후 클릭 **저장** hello hello 페이지 맨 아래에 있습니다.
10. 다음과 같이 구성에서 hello 변경 내용 테스트:
    1.  Hello 포털 검색 표시줄에 hello 트래픽 관리자 프로필 이름을 검색 하 고 표시 하는 hello hello 결과에 hello 트래픽 관리자 프로필을 클릭 합니다.
    2.  Hello에 **트래픽 관리자** 블레이드 프로필을 클릭 하 여 **개요**합니다.
    3.  hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다. 이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다. 이 경우 모든 요청 라우트된 toohello 첫 번째 끝점은 트래픽 관리자에서 감지할 경우가 되는 하지 정상 hello 트래픽 toohello 다음 끝점으로 자동으로 장애 조치 합니다.
11. 트래픽 관리자 프로필 작동 되 면 hello DNS 레코드에 권한 있는 DNS 서버 toopoint에 회사 도메인 이름 toohello 트래픽 관리자 도메인 이름을 편집 합니다.

![Traffic Manager를 사용한 우선 순위 트래픽 라우팅 방법 구성][1]

## <a name="next-steps"></a>다음 단계


- [가중치 적용 트래픽 라우팅 방법](traffic-manager-configure-weighted-routing-method.md)에 대해 알아보세요.
- [성능 라우팅 방법](traffic-manager-configure-performance-routing-method.md)에 대해 알아보세요.
- [지리적 라우팅 방법](traffic-manager-configure-geographic-routing-method.md)에 대해 알아보세요.
- 너무 방법에 대해 알아봅니다[트래픽 관리자 설정을 테스트](traffic-manager-testing-settings.md)합니다.

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png