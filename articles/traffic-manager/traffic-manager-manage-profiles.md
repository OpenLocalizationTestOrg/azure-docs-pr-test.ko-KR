---
title: "Azure 트래픽 관리자 프로필 aaaManage | Microsoft Docs"
description: "이 문서는 Azure Traffic Manager 프로필을 만들고, 사용하거나 사용하지 않도록 설정하며, 삭제하는 데 도움이 됩니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Azure 트래픽 관리자 프로필 관리

트래픽 관리자 프로필 트래픽 tooyour 클라우드 서비스 또는 웹 사이트 끝점의 메서드 toocontrol hello 배포 트래픽 라우팅을 사용 합니다. 이 문서에서는 설명 방법을 toocreate 하 고 이러한 프로필을 관리 합니다.

## <a name="create-a-traffic-manager-profile"></a>Traffic Manager 프로필 만들기

Hello Azure 포털을 사용 하 여 트래픽 관리자 프로필을 만들 수 있습니다. 프로필을 만든 후 끝점, 모니터링 및 기타 설정을 hello Azure 포털에서에서 구성할 수 있습니다. 트래픽 관리자 프로필 별로 too200 끝점을 지원합니다. 하지만 대부분의 사용 시나리오에는 적은 수의 끝점만 필요합니다.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate 트래픽 관리자 프로필

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다. 아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다. 
2. Hello에 **허브** 메뉴를 클릭 **새로** > **네트워킹** > **스크롤하게**, 클릭 **트래픽 관리자** 프로필 tooopen hello **만들 트래픽 관리자 프로필** 블레이드에서 클릭 **만들기**합니다.
3. Hello에 **만들 트래픽 관리자 프로필** 블레이드를 다음과 같이 완료 합니다.
    1. **이름**에서 사용자의 프로필에 사용할 이름을 제공합니다. 이 이름은 toobe hello trafficmanager.net 영역 내에서 고유 해야 하며 hello DNS 이름으로 인해 <name>를 사용 하는 tooaccess trafficmanager.net 트래픽 관리자 프로필.
    2. **라우팅 메서드**선택, hello **우선 순위** 라우팅 방법입니다.
    3. **구독**, toocreate 아래에서이 프로필을 원하는 hello 구독 선택
    4. **리소스 그룹**, 새 리소스 그룹 tooplace 아래에서이 프로필을 만듭니다.
    5. **리소스 그룹 위치**, hello 리소스 그룹의 hello 위치를 선택 합니다. 이 설정은 hello 리소스 그룹의 toohello 위치를 나타내며 hello 전체적으로 배포 될 트래픽 관리자 프로필에 어떠한 영향도 미치지.
    6. **만들기**를 클릭합니다.
    7. 트래픽 관리자 프로필의 hello 전역 배포 완료 되 면 hello 리소스 중 하나로 각 리소스 그룹에 표시 됩니다.

## <a name="disable-enable-or-delete-a-profile"></a>프로필 사용 안 함, 사용 또는 삭제

트래픽 관리자는 사용자 요청 toohello 구성 된 끝점을 참조 하지 않는 하므로 기존 프로필을 비활성화할 수 있습니다. 트래픽 관리자 프로필을 사용 하지 않으면 hello 프로필 및 hello 프로필에 포함 된 hello 정보 그대로 유지 하 고 hello 트래픽 관리자 인터페이스에서 편집할 수 있습니다.  Hello 프로필을 다시 설정 하는 조회 다시 시작 합니다. Hello Azure 포털에서에서 트래픽 관리자 프로필을 만들 때 자동으로 설정 됩니다. 프로필이 더 이상 필요하지 않으면 해당 프로필을 삭제할 수 있습니다.

### <a name="toodisable-a-profile"></a>toodisable 프로필

1. 사용자 지정 도메인을 사용 하는 경우 인터넷 DNS 서버의 hello CNAME 레코드를 더 이상 tooyour 트래픽 관리자 프로필을 가리키도록 변경 합니다.
2. 트래픽 중지 되 고 hello 트래픽 관리자 프로필 설정을 통해 toohello 끝점을 이동 합니다.
3. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름을 toomodify를 원하고 hello에 hello 트래픽 관리자 프로필을 클릭 한 다음 결과 표시 하는 hello 합니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**, hello 개요 블레이드에 클릭 **사용 하지 않도록 설정**, toodisable hello 트래픽 관리자 프로필을 확인 합니다.

### <a name="tooenable-a-profile"></a>tooenable 프로필

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름을 toomodify를 원하고 hello에 hello 트래픽 관리자 프로필을 클릭 한 다음 결과 표시 하는 hello 합니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**, hello 개요 블레이드에서 다음을 클릭 하 고 **사용**합니다.
5. 사용자 지정 도메인을 사용 하는 경우 트래픽 관리자 프로필의 인터넷 DNS 서버 toopoint toohello 도메인 이름의 CNAME 리소스 레코드를 만듭니다.
6. 트래픽은은 toohello 방향이 지정 된 끝점을 다시입니다.

### <a name="toodelete-a-profile"></a>toodelete 프로필

1. 인터넷 DNS 서버의 DNS 리소스 레코드 hello에 더 이상 트래픽 관리자 프로필의 toohello 도메인 이름을 가리키는 CNAME 리소스 레코드를 사용 해야 합니다.
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름을 toomodify를 원하고 hello에 hello 트래픽 관리자 프로필을 클릭 한 다음 결과 표시 하는 hello 합니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**, hello 개요 블레이드에 클릭 **삭제**, toodelete hello 트래픽 관리자 프로필을 확인 합니다.

## <a name="next-steps"></a>다음 단계

* [끝점 추가](traffic-manager-endpoints.md)
* [우선 순위 라우팅 메서드 구성](traffic-manager-configure-priority-routing-method.md)
* [지리적 라우팅 메서드 구성](traffic-manager-configure-geographic-routing-method.md) 
* [가중 라우팅 메서드 구성](traffic-manager-configure-weighted-routing-method.md)
* [성능 라우팅 메서드 구성](traffic-manager-configure-performance-routing-method.md)
