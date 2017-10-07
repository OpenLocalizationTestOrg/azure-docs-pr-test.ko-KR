---
title: "지리적 aaaConfigure 트래픽 라우팅 방법 Azure 트래픽 관리자를 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooconfigure hello Azure 트래픽 관리자를 사용 하 여 지리적 트래픽 라우팅 방법 설명"
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
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>트래픽 관리자를 사용 하 여 hello 지리적 트래픽 라우팅 방법 구성

hello 지리적 트래픽 라우팅 방법을 toodirect 트래픽 hello 요청 발생 한 위치 hello 지리적 위치에 따라 toospecific 끝점을 수 있습니다. 이 자습서 toocreate 트래픽 관리자 라우팅이 방법으로 프로 파일링 하는 방법을 보여 주고 hello 끝점 tooreceive 트래픽을 특정 지역에서 구성.

## <a name="create-a-traffic-manager-profile"></a>Traffic Manager 프로필 만들기

1. Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다. 아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다.
2. Hello 허브 메뉴에서를 클릭 **새로** > **네트워킹** > **스크롤하게**, 클릭 하 고 **트래픽 관리자 프로필**tooopen hello **만들 트래픽 관리자 프로필** 블레이드입니다.
3. Hello에 **만들 트래픽 관리자 프로필** 블레이드:
    1. 사용자의 프로필에 사용할 이름을 제공합니다. 이 이름은 toobe hello trafficmanager.net 영역 내에서 고유 해야 하며 hello DNS 이름이 됩니다 <profilename>, 있으며 trafficmanager.net tooaccess 사용 되는 트래픽 관리자 프로필을 수 있습니다.
    2. 선택 hello **지리** 라우팅 방법입니다.
    3. Hello 구독 toocreate 아래에서이 프로필을 선택 합니다.
    4. 기존 리소스 그룹을 사용 하거나 새 리소스 그룹 tooplace 아래에서이 프로필을 만듭니다. Hello를 사용 하 여 toocreate 새 리소스 그룹을 선택 하면 **리소스 그룹 위치** hello 리소스 그룹의 드롭다운 toospecify hello 위치입니다. 이 설정은 toohello 위치 hello 리소스 그룹의 나타내며 hello 전체적으로 배포 되는 트래픽 관리자 프로필에는 영향이 없습니다.
    5. **만들기**를 클릭하면 사용자의 Traffic Manager 프로필이 생성되고 전역적으로 배포됩니다.

![Traffic Manager 프로필 만들기](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>끝점 추가

1. Hello 포털 검색 표시줄에 방금 만든 hello 트래픽 관리자 프로필 이름을 검색 하 고 표시 되 면 hello 결과 클릭 합니다.
2. 너무 이동**설정** -> **끝점** hello 트래픽 관리자 블레이드에서 합니다.
3. 클릭 **추가** tooshow hello **끝점 추가** 블레이드입니다.
3. Hello에 **끝점** 블레이드에서 클릭 **추가** 및 hello **끝점 추가** 블레이드에 표시 되는 다음과 같이 완료:
4. 선택 **형식** 추가 하는 끝점의 hello 유형에 따라 합니다. 프로덕션에 사용되는 지리적 라우팅 프로필의 경우 둘 이상의 끝점이 있는 자식 프로필을 포함하는 중첩 끝점 형식을 사용하는 것이 좋습니다. 자세한 내용은 [지리적 트래픽 라우팅 방법에 대한 FAQ](traffic-manager-FAQs.md)를 참조하세요.
5. 제공 된 **이름** 기준이 될 toorecognize이이 끝점입니다.
6. 이 블레이드의 특정 필드를 추가 하는 끝점의 hello 형식에 따라 달라 집니다.
    1. Azure 끝점을 추가 하는 경우 선택 hello **대상 리소스 종류** 및 hello **대상** hello 리소스에 따라 원하는 toodirect 트래픽을
    2. 추가 하는 경우는 **외부** 끝점 hello 제공 **정규화 된 도메인 이름 (FQDN)** 끝점입니다.
    3. 추가 하는 경우는 **Nested 끝점**선택, hello **대상 리소스** 해당 toohello 자식 프로필 toouse을 hello를 지정 하는 **최소 자식 끝점계산**.
7. Hello 지도 섹션을 사용 하 여 hello 트래픽을 전송 toobe toothis 끝점 저장할에서 tooadd hello 지역 드롭다운입니다. 하나 이상의 영역을 추가해야 하며 여러 지역을 매핑할 수 있습니다.
8. 모든 끝점에 대해이 단계를 반복이 프로필에서 tooadd 원하는

![Traffic Manager 끝점 추가](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Hello 트래픽 관리자 프로필을 사용 하 여
1.  Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름 hello 섹션 앞에서 만든 하 고 결과 표시 하는 hello hello에 hello 트래픽 관리자 프로필을 클릭 합니다.
2. Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**합니다.
3. hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다. 이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다.  Hello 지리적 라우팅의 경우에서 트래픽 관리자 hello 들어오는 요청의 소스 IP hello 찾은 hello 영역을 발생 하는 것을 결정 합니다. 해당 지역의 매핑된 tooan 끝점 이면 트래픽은 라우트된 toothere입니다. 이 영역의 매핑된 tooan 끝점이 없는 경우 트래픽 관리자는 NODATA 쿼리 응답을 반환 합니다.

## <a name="next-steps"></a>다음 단계

- [지리적 트래픽 라우팅 방법](traffic-manager-routing-methods.md#geographic)에 대해 자세히 알아봅니다.
- 너무 방법에 대해 알아봅니다[트래픽 관리자 설정을 테스트](traffic-manager-testing-settings.md)합니다.
