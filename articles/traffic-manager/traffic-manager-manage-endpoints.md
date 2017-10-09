---
title: "Azure 트래픽 관리자의 aaaManage 끝점 | Microsoft Docs"
description: "이 문서는 Azure 트래픽 관리자에서 끝점을 추가, 제거 및 사용하거나 사용하지 않도록 설정하는 데 도움이 됩니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>끝점 추가, 사용 안 함, 사용 또는 삭제

장애 조치 및 라운드 로빈 트래픽 hello 웹 사이트 모드에 관계 없이 데이터 센터 내 웹 사이트에 대 한 라우팅 기능을 이미 제공 하는 hello Azure 앱 서비스 웹 앱 기능입니다. Azure 트래픽 관리자 toospecify 장애 조치 및 다른 데이터 센터의 웹 사이트 및 클라우드 서비스에 대 한 라운드 로빈 트래픽을 라우팅할 수 있습니다. hello 첫 번째 단계 필요한 tooprovide 기능 tooadd hello 클라우드 서비스나 웹 사이트 끝점 tooTraffic 관리자 인지 합니다.

트래픽 관리자 프로필의 일부인 개별 끝점을 사용하지 않도록 설정할 수도 있습니다. 끝점을 해제 하면 열은 그대로 hello 프로필의 일부로 남겨두면 hello 프로필 처럼 hello 끝점에 포함 되지 않습니다. 이 작업은 유지 관리 모드에 있거나 다시 배포할 끝점을 일시적으로 제거하는 데 유용합니다. Hello 끝점은 다시 실행을 사용할 수 있습니다.

> [!NOTE]
> 끝점을 해제 하면 영향을 주지 toodo Azure에서 배포 상태입니다. 정상 끝점 수를 유지 됩니다. tooreceive 트래픽을 트래픽 관리자에서 사용 하지 않도록 설정 하는 경우에 합니다. 또한 한 프로필에서 끝점을 사용하지 않도록 설정해도 다른 프로필의 해당 끝점 상태에는 영향을 주지 않습니다.

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>tooadd 클라우드 서비스 또는 응용 프로그램 서비스 끝점 tooa 트래픽 관리자 프로필

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름을 toomodify를 원하고 hello에 hello 트래픽 관리자 프로필을 클릭 한 다음 결과 표시 하는 hello 합니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다.
4. Hello에 **끝점** 블레이드에 표시 되는 클릭 **추가**합니다.
5. Hello에 **끝점 추가** 블레이드를 다음과 같이 완료 합니다.
    1. **형식**의 경우 **Azure 끝점**을 클릭합니다.
    2. 제공 된 **이름** 기준이 될 toorecognize이이 끝점입니다.
    3. 에 대 한 **대상 리소스 종류**에서 드롭 다운 hello, hello 적절 한 리소스 종류를 선택 합니다.
    4. 에 대 한 **대상 리소스**드롭 다운 hello에서 hello 적절 한 대상 리소스를 선택, tooshow hello 목록 아래에 있는 리소스 hello hello에 동일한 구독 **리소스 블레이드**합니다. Hello에 **리소스** 블레이드를 표시 되 면 hello 첫 번째 끝점으로 tooadd 않겠다고 선택 hello 서비스입니다.
    5. **우선 순위**의 경우 **1**로 선택합니다. 따라서 정상 상태 이면 toothis 끝점이 모든 트래픽이 됩니다.
    6. **사용 안 함으로 추가**를 선택 취소 상태로 유지합니다.
    7. **확인**
6.  4 단계와 5 tooadd hello 다음 Azure 끝점을 반복 합니다. 있는지 tooadd 확인 사용 하 여 해당 **우선 순위** 값 설정에서 **2**합니다.
7.  Hello에 표시 된 두 끝점 모두의 hello 추가 완료 되 면 **트래픽 관리자 프로필** 블레이드로 모니터링 상태와 함께 **온라인**합니다.

> [!NOTE]
> Hello를 사용 하 여 프로필에서 끝점을 제거 하거나 추가 하면 *장애 조치* 트래픽 라우팅 방법, hello 장애 조치 우선 순위 목록 수 정렬 되지 않습니다 수 있습니다 원하는대로 합니다. Hello 구성 페이지에서 장애 조치 우선 순위 목록 hello hello 순서를 조정할 수 있습니다. 자세한 내용은 [장애 조치(Failover) 트래픽 라우팅 구성](traffic-manager-configure-failover-routing-method.md)을 참조하세요.

## <a name="toodisable-an-endpoint"></a>toodisable 끝점

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름 toomodify를 원하고 표시 되는 hello 결과의 hello 트래픽 관리자 프로필을 클릭 합니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다. 
4. Toodisable, hello 끝점을 클릭 한 다음 hello **끝점** 블레이드에 표시 되는 클릭 **편집**합니다.
5. Hello에 **끝점** 블레이드에서 hello 끝점 상태 변경**비활성화**, 클릭 하 고 **저장**합니다.
6. 클라이언트는 hello 지속 될 시간 to Live (TTL) toosend 트래픽 toohello 끝점을 계속합니다. Hello TTL hello 트래픽 관리자 프로필의 hello 구성 페이지에서 변경할 수 있습니다.

## <a name="tooenable-an-endpoint"></a>tooenable 끝점

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름 toomodify를 원하고 표시 되는 hello 결과의 hello 트래픽 관리자 프로필을 클릭 합니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다. 
4. Toodisable, hello 끝점을 클릭 한 다음 hello **끝점** 블레이드에 표시 되는 클릭 **편집**합니다.
5. Hello에 **끝점** 블레이드에서 hello 끝점 상태 변경**Enabled**, 클릭 하 고 **저장**합니다.
6. 클라이언트는 hello 지속 될 시간 to Live (TTL) toosend 트래픽 toohello 끝점을 계속합니다. Hello TTL hello 트래픽 관리자 프로필의 hello 구성 페이지에서 변경할 수 있습니다.

## <a name="toodelete-an-endpoint"></a>toodelete 끝점

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름 toomodify를 원하고 표시 되는 hello 결과의 hello 트래픽 관리자 프로필을 클릭 합니다.
3. Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다. 
4. Toodisable, hello 끝점을 클릭 한 다음 hello **끝점** 블레이드에 표시 되는 클릭 **편집**합니다.
5. Hello에 **끝점** 블레이드에서 hello 끝점 상태 변경**Enabled**, 클릭 하 고 **저장**합니다.


## <a name="next-steps"></a>다음 단계

* [Traffic Manager 프로필 관리](traffic-manager-manage-profiles.md)
* [라우팅 방법 구성](traffic-manager-configure-routing-method.md)
* [트래픽 관리자 성능 저하 상태 문제 해결](traffic-manager-troubleshooting-degraded.md)
* [트래픽 관리자 성능 고려 사항](traffic-manager-performance-considerations.md)
* [트래픽 관리자 작업(REST API 참조)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

