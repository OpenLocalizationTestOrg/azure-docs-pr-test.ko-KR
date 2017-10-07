---
title: "aaaDeploy Azure API 관리 서비스 toomultiple Azure 지역 | Microsoft Docs"
description: "Toodeploy Azure API 관리 인스턴스 toomultiple Azure를 서비스 하는 방법에 대해 알아봅니다 영역입니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>어떻게 toodeploy Azure API 관리 서비스 인스턴스 toomultiple Azure 지역
API 관리 개수에 관계 없이 원하는 Azure 지역에서 게시자 toodistribute 단일 API 관리 서비스 API를 매핑함으로써 다중 지역 배포를 지원 합니다. 이를 통해 지역적으로 배포된 API 소비자가 느끼는 요청 대기 시간을 줄일 수 있으며 한 지역이 오프라인인 경우 가능한 서비스를 개선할 수도 있습니다. 

API 관리 서비스를 만들면 처음에 하나만 가질 [단위] [ unit] hello 기본 지역으로 지정 하는 단일 Azure 지역에 상주 합니다. 추가 영역 hello Azure 포털을 통해 쉽게 추가할 수 있습니다. API 관리 게이트웨이 서버 배포 tooeach 지역 이며 호출 트래픽을 가장 가까운 게이트웨이 라우팅된 toohello 됩니다. 영역 오프 라인인 경우 hello 트래픽이 자동으로 리디렉션됩니다 toohello 다음 가장 가까운 게이트웨이로 됩니다. 

> [!IMPORTANT]
> 다중 지역 배포는 hello에서 사용할 수만  **[프리미엄] [ Premium]**  계층입니다.
> 
> 

## <a name="add-region"></a>는 API 관리 서비스 인스턴스 tooa 새 지역 배포
> [!NOTE]
> API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [Azure API 관리 시작] [ Get started with Azure API Management] 자습서입니다.
> 
> 

Hello Azure 포털에서에서 탐색 toohello **배율과 가격** API 관리 서비스 인스턴스에 대 한 페이지입니다. 

![크기 조정 탭][api-management-scale-service]

toodeploy tooa 새 영역을 클릭할 **+ 추가 영역** hello 도구 모음에서 합니다.

![지역 추가][api-management-add-region]

Hello 드롭 다운 목록에서 hello 위치를 선택 하 고 hello와 hello 슬라이더에 대 한 단위 수를 설정 합니다.

![단위 지정][api-management-select-location-units]

클릭 **추가** tooplace hello 위치 테이블에서 선택 항목입니다. 

구성 된 모든 위치 구성할 때까지이 과정을 반복 하 고 클릭 **저장** hello 도구 모음 toostart hello 배포 프로세스에서 합니다.

## <a name="remove-region"> </a>위치에 API 관리 서비스 인스턴스 삭제
Hello Azure 포털에서에서 탐색 toohello **배율과 가격** API 관리 서비스 인스턴스에 대 한 페이지입니다. 

![크기 조정 탭][api-management-scale-service]

원하는 hello 위치에 대 한 tooremove hello를 사용 하 여 hello 상황에 맞는 메뉴를 열고 **...**  hello 테이블의 hello 오른쪽 끝 단추를 클릭 합니다. 선택 hello **삭제** 옵션입니다.

![지역 제거][api-management-remove-region]

Hello 삭제를 확인 하 고 클릭 **저장** tooapply hello 변경 합니다.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

