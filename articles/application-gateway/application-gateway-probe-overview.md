---
title: "Azure 응용 프로그램 게이트웨이에 대 한 모니터링 개요 aaaHealth | Microsoft Docs"
description: "Azure 응용 프로그램 게이트웨이의 기능을 모니터링 하는 hello에 대 한 자세한 내용은"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>응용 프로그램 게이트웨이 상태 모니터링 개요

기본적으로 azure 응용 프로그램 게이트웨이 응용 프로그램은 백 엔드 풀의 모든 리소스의 hello 상태를 모니터링 하 고 자동으로 hello 풀에서 비정상으로 간주 하는 모든 리소스를 제거 합니다. 응용 프로그램 게이트웨이 toomonitor hello 비정상 인스턴스를 계속 하 고 해당 추가 사용 가능 하 게 하 고 응답 toohealth 프로브 toohello 정상 백 엔드 풀을 백업 합니다. 응용 프로그램 게이트웨이 백 엔드 HTTP 설정 hello에에서 정의 된 동일한 포트 hello로 hello 상태 프로브를 보냅니다. 이 구성을 통해 해당 hello 프로브 hello 동일한 포트 고객 tooconnect toohello 백 엔드 사용 될 수 있는지 테스트 하는 것입니다.

![Application Gateway 프로브 예제][1]

또한 toousing 기본 상태 프로브 모니터링도 사용자 지정할 수 있습니다 hello 상태 프로브 toosuit 응용 프로그램의 요구 사항입니다. 이 문서에서는 기본 및 사용자 지정 상태 프로브를 모두 설명합니다.

> [!NOTE]
> 응용 프로그램 게이트웨이 서브넷에 NSG 있으면 포트 범위 65503 65534 인바운드 트래픽 hello 응용 프로그램 게이트웨이 서브넷에서 열어야 합니다. 이러한 포트는 hello 백 엔드 상태 API toowork 필요 합니다.

## <a name="default-health-probe"></a>기본 상태 프로브

응용 프로그램 게이트웨이는 사용자 지정 프로브 구성을 설정하지 않는 경우 기본 상태 프로브를 자동으로 구성합니다. 동작을 모니터링 하는 hello hello 백 엔드 풀에 대해 구성 된 HTTP 요청 toohello IP 주소 하 여 작동 합니다. 기본 프로브에 대해 https hello 백 엔드 http 설정 구성 된 경우 hello 프로브도 HTTPS를 사용 hello 백 엔드의 잘 tootest 상태입니다.

예: 포트 80에서 응용 프로그램 게이트웨이 toouse 백 엔드 서버 A, B 및 C tooreceive HTTP 네트워크 트래픽을 구성 합니다. 세 명의 서버 hello 정상 HTTP 응답에 대 한 30 초 마다 테스트 hello 기본 상태 모니터링 합니다. 정상 HTTP 응답은 [상태 코드](https://msdn.microsoft.com/library/aa287675.aspx) 200에서 399 사이입니다.

서버 A에 대 한 hello 기본 프로브 확인이 실패 하면 hello 응용 프로그램 게이트웨이 백 엔드 풀에서 제거 하 고 네트워크 트래픽 흐름이 toothis 서버를 중지 합니다. hello 기본 프로브는 여전히 toocheck 서버에 대 한 30 초는 마다 계속합니다. 서버 A 응답 하는 경우 성공적으로 tooone 요청에서 기본 상태 검색, 정상 toohello 백 엔드 풀 및 toohello 서버를 다시 흐르기 트래픽 시작으로 다시 추가 됩니다.

### <a name="default-health-probe-settings"></a>기본 상태 프로브 설정

| 프로브 속성 | 값 | 설명 |
| --- | --- | --- |
| 프로브 URL |http://127.0.0.1:\<port\>/ |URL 경로 |
| 간격 |30 |프로브 간격(초) |
| 시간 제한 |30 |프로브 시간 제한(초) |
| 비정상 임계값 |3 |프로브 재시도 횟수. hello 연속 프로브 오류 발생 횟수 hello 비정상 임계값에 도달 하면 hello 백 엔드 서버가 표시 됩니다. |

> [!NOTE]
> hello 포트는 hello 동일 hello 백 엔드 HTTP 설정으로 포트입니다.

hello 기본 검색만 보므로 http://127.0.0.1:\<포트\> toodetermine 상태입니다. Tooconfigure hello 상태 프로브 toogo tooa 사용자 지정 URL이 필요 하거나 다른 설정을 수정할 경우에 단계를 수행 하는 hello에 설명 된 대로 사용자 지정 프로브를 사용 해야 합니다.

## <a name="custom-health-probe"></a>사용자 지정 상태 프로브

사용자 지정 프로브 toohave hello 상태 모니터링을 보다 세부적으로 제어를 허용 합니다. 사용자 지정 프로브를 사용할 때는 hello 백 엔드 풀 인스턴스 비정상으로 표시 하기 전에 hello 프로브 간격, URL 및 경로 tootest hello 및 실패 한 응답 tooaccept 수를 구성할 수 있습니다.

### <a name="custom-health-probe-settings"></a>사용자 지정 상태 프로브 설정

hello 다음 표에서 사용자 지정 상태 검색의 hello 속성에 대 한 정의 합니다.

| 프로브 속성 | 설명 |
| --- | --- |
| 이름 |Hello 검색의 이름입니다. 이 이름은 백 엔드 HTTP 설정에 사용 되는 toorefer toohello 프로브입니다. |
| 프로토콜 |프로토콜은 toosend hello 프로브를 사용합니다. hello 백 엔드 HTTP 설정에 정의 된 hello 프로토콜을 사용 하는 hello 프로브 |
| 호스트 |호스트 이름 toosend hello 프로브 다중 사이트를 Application Gateway에 구성하는 경우에만 적용할 수 있습니다. 그렇지 않으면 '127.0.0.1'을 사용합니다. 이 값은 VM 호스트 이름과 다릅니다. |
| Path |Hello 프로브의 상대 경로입니다. hello 유효한 경로가에서 시작 하 고 '/'입니다. |
| 간격 |프로브 간격(초). 이 값은 두 개의 연속 프로브 사이의 hello 시간 간격입니다. |
| 시간 제한 |프로브 시간 제한(초) 이 시간 제한 기간 내에서 유효한 응답 받지 hello 프로브 실패로 표시 됩니다.  |
| 비정상 임계값 |프로브 재시도 횟수. hello 연속 프로브 오류 발생 횟수 hello 비정상 임계값에 도달 하면 hello 백 엔드 서버가 표시 됩니다. |

> [!IMPORTANT]
> 응용 프로그램 게이트웨이 단일 사이트에 대해 구성 된 경우 기본 hello 호스트에서 이름은로 지정 해야 '127.0.0.1', 그렇지 않으면 사용자 지정 프로브를 구성 하지 않는 한 합니다.
> 참조에 대 한 사용자 지정 프로브 보내집니다 너무\<프로토콜\>://\<호스트\>:\<포트\>\<경로\>합니다. hello 사용 되는 포트 됩니다 hello 백 엔드 HTTP 설정에 정의 된 대로 동일한 포트를 hello 합니다.

## <a name="next-steps"></a>다음 단계
응용 프로그램 게이트웨이 상태를 모니터링 하는 방법에 대 한 학습을 구성할 수 있습니다는 [사용자 지정 상태 프로브](application-gateway-create-probe-portal.md) hello Azure 포털에서에서 또는 [사용자 지정 상태 프로브](application-gateway-create-probe-ps.md) PowerShell 및 hello Azure 리소스 관리자를 사용 하 여 배포 모델입니다.

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
