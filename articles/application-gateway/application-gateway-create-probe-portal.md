---
title: "aaaCreate 사용자 지정 프로브-Azure 응용 프로그램 게이트웨이-Azure 포털 | Microsoft Docs"
description: "어떻게 toocreate 사용자 지정 프로브 응용 프로그램 게이트웨이에 대 한 hello 포털을 사용 하 여 알아봅니다"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Hello 포털을 사용 하 여 응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브를 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure 클래식 PowerShell](application-gateway-create-probe-classic-ps.md)

이 문서에서는 hello Azure 포털을 통해 사용자 지정 프로브 tooan 기존 응용 프로그램 게이트웨이 추가 합니다. 사용자 지정 프로브는 특정 상태 확인 페이지를 사용 하는 응용 프로그램 또는 hello 기본 웹 응용 프로그램에 대 한 성공적인 응답을 제공 하지 않는 응용 프로그램에 유용 합니다.

## <a name="before-you-begin"></a>시작하기 전에

응용 프로그램 게이트웨이 아직 없는 경우 방문 [응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-portal.md) toocreate 응용 프로그램 게이트웨이 toowork 사용 합니다.

## <a name="createprobe"></a>Hello 프로브 만들기

프로브는 hello 포털을 통해는 두 단계로 구성 됩니다. hello 첫 번째 단계는 toocreate hello 프로브입니다. Hello 두 번째 단계에서는 hello 프로브 toohello 백 엔드 http 설정의 hello 응용 프로그램 게이트웨이 추가합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다. 아직 계정이 없는 경우 [1개월 평가판](https://azure.microsoft.com/free)을 등록할 수 있습니다.

1. Azure 포털 즐겨찾기 창 hello에서 모든 리소스를 클릭 합니다. Hello 응용 프로그램 게이트웨이 hello에서 모든 리소스 블레이드를 클릭 합니다. 이미 선택한 hello 구독에 있는 여러 가지 리소스가, 경우에 이름으로 hello 필터에에서 partners.contoso.net를 입력할 수 있습니다... 상자 tooeasily 액세스 hello 응용 프로그램 게이트웨이 합니다.

1. 클릭 **프로브** hello 클릭 **추가** 단추 tooadd 검색 합니다.

  ![정보가 입력된 프로브 추가 블레이드][1]

1. Hello에 **추가 상태 프로브** 블레이드에서 hello 프로브에 대 한 hello 필요한 정보를 입력 하 고 클릭 하 여 완료 된 경우 **확인**합니다.

  |**설정** | **값** | **세부 정보**|
  |---|---|---|
  |**Name**|customProbe|이 값은 hello 포털에 액세스 하는 이름 toohello 검색 합니다.|
  |**프로토콜**|HTTP 또는 HTTPS | 상태 프로브 hello hello 프로토콜 사용 합니다.|
  |**호스트**|예: contoso.com|이 값은 hello 프로브에 사용 되는 hello 호스트 이름입니다. 다중 사이트를 Application Gateway에 구성하는 경우에만 적용할 수 있습니다. 그렇지 않으면 '127.0.0.1'을 사용합니다. 이 값은 hello VM 호스트 이름이 다릅니다.|
  |**Path**|/ 또는 다른 경로|사용자 지정 프로브 hello에 대 한 전체 url hello의 hello 나머지입니다. 유효한 경로는 '/'로 시작합니다. 사용 하 여 정당한 http://contoso.com의 기본 경로 hello에 대 한 '/' |
  |**간격(초)**|30|얼마나 자주 hello 프로브는 실행 상태에 대 한 toocheck 합니다. 30 초 보다 낮은 tooset hello는 권장 되지 않습니다.|
  |**시간 제한(초)**|30|hello 양의 시간 hello 검색 시간 초과 전까지 대기합니다. hello 시간 제한 간격 요구 toobe tooensure hello 백 엔드 상태 페이지는 http 호출을 할 수는 충분히 높은 ´ ù.|
  |**비정상 임계값**|3|비정상으로 간주 하는 시도 toobe를 실패 하는 횟수입니다. 임계값이 상태 검사에 실패 하는 경우 백 엔드 hello 0 이면 즉시 비정상 결정 됩니다.|

  > [!IMPORTANT]
  > hello 호스트 이름이 서버 이름과 달라 서는 안녕 있습니다. 이 값은 hello 이름 hello hello 응용 프로그램 서버에서 실행 되는 가상 호스트입니다. hello 프로브 toohttp 보내집니다: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>프로브 toohello 게이트웨이 추가

이제 hello 프로브를 만든입니다 시간 tooadd 것 toohello 게이트웨이 합니다. 프로브 hello hello 응용 프로그램 게이트웨이 백 엔드 http 설정에 설정 되어 있습니다.

1. 클릭 **HTTP 설정** hello 응용 프로그램 게이트웨이 hello 현재 백 엔드 http 설정 hello 창에 나열 된 toobring hello 구성 블레이드를 클릭 합니다.

  ![https 설정 창][2]

1. Hello에 **appGatewayBackEndHttpSettings** 설정 블레이드에서, 검사 hello **사용 하 여 사용자 지정 프로브** 확인란 hello에서 만든 hello 프로브 선택 [만들기 hello 프로브](#createprobe) 섹션 hello에 **사용자 지정 프로브** 드롭 다운...
완료 되 면 **저장** hello 설정이 적용 됩니다.

hello 기본 프로브 hello 기본 액세스 toohello 웹 응용 프로그램을 확인합니다. 사용자 지정 프로브를 만든 후, hello 응용 프로그램 게이트웨이 백 엔드 서버 hello에 대 한 hello 정의 된 사용자 지정 경로 toomonitor 상태를 사용 합니다. 정의 된 hello 기준에 따라, 응용 프로그램 게이트웨이 hello hello 프로브에 지정 된 hello 경로 확인 합니다. Hello 호출 toohost:Port / 경로 HTTP 200 399 상태 응답 반환 하지 않는, 경우 hello 비정상 임계값에 도달 하면 hello 서버 순환 순서에서 가져옵니다. 다시 정상 있게 되 면 hello 비정상 인스턴스 toodetermine에서 계속 검색 됩니다. 트래픽이 흐르는 tooit 다시 및 검색 toohello 시작 hello 인스턴스 백 toohealthy 서버 풀에 추가 되 면 인스턴스는 일반적인 방법으로 사용자 지정된 간격으로 계속 합니다.

## <a name="next-steps"></a>다음 단계

Azure 응용 프로그램 게이트웨이 통해 SSL 오프 로딩 tooconfigure 참조 toolearn [SSL 오프 로드 구성](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

