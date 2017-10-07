---
title: "경로 기반 aaaCreate 규칙-Azure 응용 프로그램 게이트웨이-Azure 포털 | Microsoft Docs"
description: "자세한 내용은 응용 프로그램 게이트웨이 사용 하 여에 대 한 경로 기반 규칙 toocreate 포털 hello 하는 방법"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Hello 포털을 사용 하 여 응용 프로그램 게이트웨이 대 한 기준으로 경로 규칙을 만듭니다

> [!div class="op_single_selector"]
> * [Azure 포털](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL 라우팅 경로 기반 있습니다 tooassociate 경로 Http 요청의 hello URL 경로에 따라 수 있습니다. 경로 tooa 백 엔드 풀 응용 프로그램 게이트웨이 hello에 나열 된 hello URL에 대해 구성 된 경우를 확인 하 고 hello 네트워크 트래픽 toohello 백 엔드 풀 정의 보냅니다. URL 기반 라우팅에 대 한 일반적인 용도는 서로 다른 내용 유형 toodifferent 백 엔드 서버 풀에 대 한 tooload 잔액 요청입니다.

URL 기반 라우팅 새 규칙 유형 tooapplication 게이트웨이 소개합니다. 응용 프로그램 게이트웨이에는 두 가지 규칙 형식(기본 및 경로 기반 규칙)이 있습니다. 기본 규칙 종류 hello hello 백 엔드에 대 한 라운드 로빈 서비스 경로 기반 규칙 하면서 또한 tooround 로빈 배포 풀, 고려 hello 요청 URL의 경로 패턴 hello 적절 한 백 엔드 풀을 선택 하는 동안를 제공 합니다.

## <a name="scenario"></a>시나리오

hello 다음과 같은 시나리오를 진행 기존 응용 프로그램 게이트웨이에서 경로 기반 규칙 만들기.
hello 시나리오에서는 가정 이미 수행 hello 단계 너무[응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-portal.md)합니다.

![url 경로][scenario]

## <a name="createrule"></a>Hello 경로 기반 규칙 만들기

경로 기반 규칙 수 있는 사용 가능한 수신기 toouse 있는지 tooverify hello 규칙을 만들기 전에 해당 수신기가 필요 합니다.

### <a name="step-1"></a>1단계

Toohello 이동 [Azure 포털](http://portal.azure.com) 하 고 기존 응용 프로그램 게이트웨이 선택 합니다. **규칙**

![Application Gateway 개요][1]

### <a name="step-2"></a>2단계

클릭 **경로 기반** 단추 tooadd 새 경로 기반 규칙입니다.

### <a name="step-3"></a>3단계

hello **경로 기반 규칙 추가** 블레이드는 다음 두 섹션이 있습니다. hello 첫 번째 섹션은 hello 수신기, hello 이름 hello 규칙 및 hello 기본 경로 설정을 정의 합니다. 사용자 지정 경로 기반 경로 hello에서 포함 되지 않는 경로 대 한 hello 기본 경로 설정이 됩니다. hello의 두 번째 섹션 hello **경로 기반 규칙 추가** 블레이드 스스로 hello 경로 기반 규칙을 정의한는 합니다.

**기본 설정**

* **이름** -이 값은 hello 포털에 액세스할 수 있는 친숙 한 이름 toohello 규칙입니다.
* **수신기** -이 값은 hello 규칙에 사용 되는 hello 수신기입니다.
* **백 엔드 풀 기본** -이 설정은 hello 백 엔드 toobe hello 기본 규칙에 사용 되는 정의 하는 hello 설정
* **기본 HTTP 설정** -이 설정은이 hello HTTP 설정 toobe hello 기본 규칙에 사용 되는 정의 하는 hello 설정입니다.

**경로 기반 규칙**

* **이름** -이 값은 친숙 한 이름 toopath 기반 규칙입니다.
* **경로** -트래픽을 전달 하는 경우이 설정은 정의 hello에 대 한 경로 hello 규칙 검색
* **백 엔드 풀** -이 설정은 hello 백 엔드 toobe hello 규칙에 사용 되는 정의 하는 hello 설정
* **HTTP 설정** -이 설정은이 hello HTTP 설정 toobe hello 규칙에 사용 되는 정의 하는 hello 설정입니다.

> [!IMPORTANT]
> 경로 패턴 toomatch의 경로: hello 목록입니다. 로 시작 해야 각 / hello만 장소는 "\*" ï ´ ù hello 끝에 합니다. 사용 가능한 예는 /xyz, /xyz* 또는 /xyz/*입니다.  

![정보가 입력된 경로 기반 규칙 추가 블레이드][2]

기존 응용 프로그램 게이트웨이 hello 포털을 통해 쉽게 프로세스 경로 기반 규칙 tooan를 추가 합니다. 경로 기반 규칙을 만든 후 편집된 tooadd 추가 규칙 수 있습니다. 

![추가 경로 기반 규칙 추가][3]

이 단계는 경로 기반 경로를 구성합니다. 중요 한 toounderstand 요청은 다시 작성 하지 이면 hello 요청 및 basic hello url 패턴 보냅니다 hello 요청 toohello 적절 한 백 엔드에 요청 제공 응용 프로그램 게이트웨이으로 검사 합니다.

## <a name="next-steps"></a>다음 단계

Azure 응용 프로그램 게이트웨이 통해 SSL 오프 로딩 tooconfigure 참조 toolearn [SSL 오프 로드 구성](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
