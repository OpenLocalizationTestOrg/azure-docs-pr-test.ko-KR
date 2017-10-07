---
title: "azure에서 트래픽 관리자 프로필 aaaCreate | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate 트래픽 관리자 프로필"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Traffic Manager 프로필 만들기

이 문서에 설명 된 프로필 **우선 순위** 라우팅 유형을 tooroute 사용자 tootwo Azure 웹 앱 끝점을 만들 수 있습니다. Hello를 사용 하 여 **우선 순위** 라우팅 유형을, 모든 트래픽이 상태인 라우트된 toohello 첫 번째 끝점 둘째 hello 백업으로 유지 됩니다. 결과적으로, 사용자가 첫 번째 끝점 hello 비정상 상태가 되 라우트된 toohello 두 번째 끝점 수 있습니다.

이 문서에서는 두 개의 이전에 만든된 Azure 웹 앱 끝점은 새로 만든 연결된 toothis 트래픽 관리자 프로필입니다. 방법에 대 한 자세한 toolearn toocreate Azure 웹 앱 끝점 방문 hello [Azure 웹 앱 설명서 페이지](https://docs.microsoft.com/azure/app-service-web/)합니다. DNS 이름이 고를 통해 연결할 수 있는 모든 끝점을 추가할 수 있습니다 hello 공용 인터넷 및 예를 들어 Azure 웹 앱 끝점을 사용 합니다.

### <a name="create-a-traffic-manager-profile"></a>Traffic Manager 프로필 만들기
1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다. 계정이 아직 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)에 등록할 수 있습니다. 
2. Hello에 **허브** 메뉴를 클릭 **새로** > **네트워킹** > **스크롤하게**, 클릭 **트래픽 관리자** 프로필 tooopen hello **만들 트래픽 관리자 프로필** 블레이드에서 클릭 **만들기**합니다.
3. Hello에 **만들 트래픽 관리자 프로필** 블레이드를 다음과 같이 완료 합니다.
    1. **이름**에서 사용자의 프로필에 사용할 이름을 제공합니다. 이 이름은 toobe hello trafficmanager.net 영역 내에서 고유 해야 하며 hello DNS 이름으로 인해 <name>, 사용 되는 tooaccess 인 trafficmanager.net 트래픽 관리자 프로필.
    2. **라우팅 메서드**선택, hello **우선 순위** 라우팅 방법입니다.
    3. **구독**, toocreate 아래에서이 프로필을 원하는 hello 구독 선택
    4. **리소스 그룹**, 새 리소스 그룹 tooplace 아래에서이 프로필을 만듭니다.
    5. **리소스 그룹 위치**, hello 리소스 그룹의 hello 위치를 선택 합니다. 이 설정은 hello 리소스 그룹의 toohello 위치를 나타내며 hello 전체적으로 배포 될 트래픽 관리자 프로필에 어떠한 영향도 미치지.
    6. **만들기**를 클릭합니다.
    7. 트래픽 관리자 프로필의 hello 전역 배포 완료 되 면 hello 리소스 중 하나로 각 리소스 그룹에 표시 됩니다.

    ![Traffic Manager 프로필 만들기](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Traffic Manager 끝점 추가

1. Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 결과 표시 하는 hello hello hello에서 섹션을 클릭 하 고 hello 트래픽 관리자 프로필을 앞에서 만든 이름입니다.
2. Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다.
3. Hello에 **끝점** 블레이드에 표시 되는 클릭 **추가**합니다.
4. Hello에 **끝점 추가** 블레이드를 다음과 같이 완료 합니다.
    1. **형식**의 경우 **Azure 끝점**을 클릭합니다.
    2. 제공 된 **이름** 기준이 될 toorecognize이이 끝점입니다.
    3. **대상 리소스 형식**의 경우 **App Service**를 클릭합니다.
    4. 에 대 한 **대상 리소스**, 클릭 **앱 서비스 선택** tooshow hello 목록이 hello에서 웹 앱 hello 동일한 구독 합니다. Hello에 **리소스** 블레이드를 표시 되 면 선택 hello hello 첫 번째 끝점으로 tooadd 되도록 응용 프로그램 서비스입니다.
    5. **우선 순위**의 경우 **1**로 선택합니다. 따라서 정상 상태 이면 toothis 끝점이 모든 트래픽이 됩니다.
    6. **사용 안 함으로 추가**를 선택 취소 상태로 유지합니다.
    7. **확인**
5.  Hello 다음 Azure 웹 앱 끝점에 대해 3 및 4 단계를 반복 합니다. 있는지 tooadd 확인 사용 하 여 해당 **우선 순위** 값 설정에서 **2**합니다.
6.  Hello에 표시 된 두 끝점 모두의 hello 추가 완료 되 면 **트래픽 관리자 프로필** 블레이드로 모니터링 상태와 함께 **온라인**합니다.

    ![Traffic Manager 끝점 추가](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Hello 트래픽 관리자 프로필을 사용 하 여
1.  Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** hello 섹션 앞에서 만든 이름입니다. 표시 되는 hello 결과 hello 트래픽 관리자 프로필을 클릭 합니다.
2. Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**합니다.
3. hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다. 이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다. 이 경우 모든 요청 라우트된 toohello 첫 번째 끝점은 및 트래픽 관리자에서 감지할 경우 수 정상 경우 hello 트래픽 toohello 다음 끝점을 통해 자동으로 실패 합니다.

## <a name="delete-hello-traffic-manager-profile"></a>Hello 트래픽 관리자 프로필 삭제
더 이상 필요 hello 리소스 그룹 및 사용자가 만든 hello 트래픽 관리자 프로필을 삭제 합니다. 따라서 toodo hello에서 hello 리소스 그룹을 선택 **트래픽 관리자 프로필** 블레이드에 대 한 클릭 **삭제**합니다.

## <a name="next-steps"></a>다음 단계

- [라우팅 형식](traffic-manager-routing-methods.md)에 대해 자세히 알아보세요.
- [끝점 형식](traffic-manager-endpoint-types.md)에 대해 자세히 알아보세요.
- [끝점 모니터링](traffic-manager-monitoring.md)에 대해 자세히 알아보세요.



