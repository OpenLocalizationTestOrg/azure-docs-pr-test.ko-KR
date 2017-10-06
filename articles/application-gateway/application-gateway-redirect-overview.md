---
title: "Azure 응용 프로그램 게이트웨이 위한 aaaRedirect 개요 | Microsoft Docs"
description: "Azure 응용 프로그램 게이트웨이에 hello 리디렉션 기능에 대 한 자세한 내용은"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Application Gateway 리디렉션 개요

많은 웹 응용 프로그램에 대 한 일반적인 시나리오는 toosupport 자동 HTTP tooHTTPS 리디렉션 tooensure 응용 프로그램과 사용자 간의 모든 통신이 암호화 된 경로 통해 발생 합니다. 지난 hello, 고객 tooredirect 요청 받은 HTTP tooHTTPS에는 해당 목적으로 제공 하는 전용된 백 엔드 풀 만들기와 같은 기술을 사용 했습니다.  응용 프로그램 게이트웨이 이제 응용 프로그램 게이트웨이 hello에 tooredirect 트래픽 기능을 지원합니다. 이 간단한 응용 프로그램 구성, hello 리소스 사용을 최적화 하며 전역 및 경로 기반 리디렉션을 비롯 한 새로운 리디렉션 시나리오를 지원 합니다. 응용 프로그램 게이트웨이 리디렉션 지원은 제한 되어 tooHTTP HTTPS 리디렉션만-> 합니다. 응용 프로그램 게이트웨이에 대 한 수신기 tooanother 수신기에서 수신 하는 트래픽의 리디렉션을 허용 하는 제네릭 리디렉션 메커니즘입니다. 또한 리디렉션 tooan 외부 사이트도 지원합니다. 응용 프로그램 게이트웨이 리디렉션 지원 hello 다음 기능을 제공 합니다.

1. 게이트웨이 hello에 하나의 수신기 tooanother 수신기에서 전역 리디렉션. 따라서 사이트에 HTTP tooHTTPS 리디렉션을 수 있습니다.
2. 경로 기반 리디렉션. 이 형식의 리디렉션 사용 하 여 특정 사이트 영역에만 HTTP tooHTTPS 리디렉션/카트/으로 쇼핑 카트 영역을 표시 하는 예를 들어 * 합니다.
3. 리디렉션 tooexternal 사이트입니다.

![리디렉션](./media/application-gateway-redirect-overview/redirect.png)

이러한 변경으로 인해 고객 toocreate hello 대상 수신기를 지정 하는 새 리디렉션 구성 개체를 해야 합니다. 또는 외부 사이트 toowhich 리디렉션이 필요 합니다. hello 구성 요소는 hello URI 경로 조회가 문자열 toohello 리디렉션 URL을 추가 하는 옵션 tooenable도 지원 합니다. 고객은 리디렉션이 임시 리디렉션(HTTP 상태 코드 302)인지 영구 리디렉션(HTTP 상태 코드 301)인지도 선택할 수 있습니다. 이 리디렉션 구성을 만든 후 새 규칙을 통해 연결 된 toohello 소스 수신기가 있습니다. 기본 규칙을 사용 하는 경우 hello 리디렉션 구성 소스 수신기와 연결 된 이며 글로벌 리디렉션. 경로 기반 규칙을 사용할 경우 hello 리디렉션 구성 hello URL 경로 지도에 정의 되 고 따라서 사이트의 toohello 특정 경로 영역에만 적용 됩니다.

### <a name="next-steps"></a>다음 단계

[응용 프로그램 게이트웨이에서 URL 리디렉션 구성](application-gateway-configure-redirect-powershell.md)
