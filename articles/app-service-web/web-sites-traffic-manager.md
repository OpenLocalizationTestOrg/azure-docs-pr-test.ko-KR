---
title: "Azure 트래픽 관리자와 함께 Azure 웹 앱 트래픽 aaaControlling"
description: "이 문서에서는 tooAzure 웹 응용 프로그램 관련 Azure 트래픽 관리자에 대 한 요약 정보를 제공 합니다."
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Azure 트래픽 관리자를 사용하여 Azure 웹 앱 트래픽 제어
> [!NOTE]
> 이 문서에서는 tooAzure 앱 서비스 웹 앱 관련해 서 Microsoft Azure 트래픽 관리자에 대 한 요약 정보를 제공 합니다. 이 문서의 끝 hello에 hello 링크를 방문 하 여 자세한 정보에 대 한 Azure 트래픽 관리자 자체를 찾을 수 있습니다.
> 
> 

## <a name="introduction"></a>소개
Azure 트래픽 관리자 toocontrol를 사용할 수 있습니다 어떻게 웹 클라이언트의 요청은 Azure 앱 서비스의 분산된 tooweb 앱. 웹 앱 끝점 tooa Azure 트래픽 관리자 프로필에 추가 되 면 Azure 트래픽 관리자는 추적 hello 상태 (실행 중, 중지 또는 삭제) 웹 응용 프로그램의 해당 끝점 중이 트래픽을 받아야 결정할 수 있습니다.

## <a name="load-balancing-methods"></a>부하 분산 방법
Azure 트래픽 관리자는 세 가지의 다른 부하 분산 방법을 사용합니다. Hello tooAzure 웹 응용 프로그램 관련 된 목록 다음에 설명 되어 있습니다.

* **장애 조치**: 웹 응용 프로그램 복제본 서로 다른 지역에 있으면이 메서드 tooconfigure 하나의 웹 앱 tooservice 모든 웹 클라이언트 트래픽을 사용 하 고 사례 hello 첫 번째 웹 응용 프로그램에서 트래픽을 하는 다른 지역의 tooservice에서 다른 웹 응용 프로그램 구성 수 사용할 수 없습니다.
* **라운드 로빈**: 웹 응용 프로그램 복제본 서로 다른 지역에 있으면 있습니다를 사용할 수 있습니다이 메서드 toodistribute 트래픽을 균등 하 게 서로 다른 지역에 있는 hello 웹 앱입니다.
* **성능**: hello 성능 방법 hello 가장 짧은 왕복 시간 tooclients에 기반 하는 트래픽을 분산 합니다. 성능 방법 hello hello 내에서 웹 앱에 사용할 수 있습니다 동일한 지역 또는 서로 다른 지역에 있습니다.

## <a name="web-apps-and-traffic-manager-profiles"></a>웹 앱 및 트래픽 관리자 프로필
웹 앱에 대 한 트래픽의 tooconfigure hello 컨트롤을 Azure 트래픽 관리자의 hello 3 부하 분산 앞에서 설명한 방법 중 하나를 사용 하는 프로필을 만들 추가 하는 다음 toocontrol 트래픽 toohello 원하는 hello 끝점에 (이 경우 웹 앱) 프로필입니다. 웹 응용 프로그램 상태 (실행 중, 중지 또는 삭제)은 정기적으로 전달된 toohello 프로 파일링 Azure 트래픽 관리자는 그에 따라 트래픽을 보낼 수 있도록 합니다.

Azure와 함께 Azure 트래픽 관리자를 사용할 때는 주의 hello 지점 다음에 유의 하십시오.

* Hello 내에서 웹 앱 전용 배포에 대 한 웹 앱에 이미 같은 지역의 tooweb 응용 프로그램 모드와 관계 없이 장애 조치 및 라운드 로빈 기능을 제공합니다.
* 에 대 한 배포에 다른 Azure 클라우드 서비스와 함께에서 웹 응용 프로그램을 사용 하는 동일한 지역 hello, 두 가지 유형의 끝점 tooenable 하이브리드 시나리오를 결합할 수 있습니다.
* 프로필에서 지역당 하나의 웹 앱 끝점만 지정할 수 있습니다. 한 영역에 대 한 끝점으로 웹 응용 프로그램을 선택 하면 hello 나머지 웹 응용 프로그램에서 해당 지역의 해당 프로필에 대 한 선택을 사용할 수 없습니다.
* Azure 트래픽 관리자 프로필에 지정 하는 hello 웹 앱 끝점 hello 아래에 표시 될 **도메인 이름** hello 프로필의 hello 웹 앱에 대 한 hello 구성 페이지에서 섹션 하지만 됩니다 구성할 수 있습니다.
* 웹 응용 프로그램 tooa 프로필에 추가한 후 hello **사이트 URL** hello 웹의 대시보드에서 hello에 응용 프로그램의 포털 페이지 하나를 설정한 경우 hello 웹 앱의 hello 사용자 지정 도메인 URL이 표시 됩니다. 그렇지 않으면 hello 트래픽 관리자 프로필 URL 표시 됩니다 (예를 들어 `contoso.trafficmgr.com`). Hello 웹 앱의 직접 도메인 이름을 둘 다 hello 및 트래픽 관리자 URL hello hello에서 hello 웹 앱의 구성 페이지에 표시 됩니다 **도메인 이름** 섹션.
* 사용자 지정 도메인 이름을 작동할지, 기대 하지만 또한 tooadding 해당 tooyour 웹 앱, DNS 맵 toopoint toohello 트래픽 관리자 URL을 구성 해야 합니다. 방법에 대 한 Azure 웹 앱에 대 한 사용자 지정 도메인을 tooset 참조 [Azure 웹 사이트에 대 한 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)합니다.
* 표준 또는 프리미엄 모드 tooa Azure 트래픽 관리자 프로필에에서 있는 웹 응용 프로그램에만 추가할 수 있습니다.

## <a name="next-steps"></a>다음 단계
Azure 트래픽 관리자의 개념 및 기술 개요에 대해서는 [트래픽 관리자 개요](../traffic-manager/traffic-manager-overview.md)를 참조하십시오.

웹 앱과 트래픽 관리자를 사용 하는 방법에 대 한 자세한 내용은 hello 블로그 게시물을 참조 하십시오. [Azure 트래픽 관리자를 Azure 웹 사이트를 사용 하 여](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) 및 [Azure 트래픽 관리자의 경우 이제 Azure 웹 사이트를 통합할 수](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/)합니다.

