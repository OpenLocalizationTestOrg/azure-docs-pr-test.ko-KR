---
title: "aaaHost Azure 응용 프로그램 게이트웨이 통해 여러 사이트 | Microsoft Docs"
description: "이 페이지에서는 지침 tooconfigure 기존 Azure 응용 프로그램 게이트웨이 hello에서 여러 웹 응용 프로그램에 대 한 Azure 포털 hello로 동일한 게이트웨이에 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>여러 웹 응용 프로그램을 호스트하는 기존 응용 프로그램 게이트웨이 구성

> [!div class="op_single_selector"]
> * [쉬운 테이블](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

여러 사이트 호스팅 사용 하면 하나의 웹 응용 프로그램 둘 이상의 toodeploy hello에 동일한 응용 프로그램 게이트웨이 합니다. Hello 들어오는 HTTP 요청에는 수신기가 트래픽을 받게 toodetermine 호스트 헤더의 존재 여부에 의존 합니다. hello 수신기는 다음 트래픽 tooappropriate 백 엔드 풀의 hello 게이트웨이 hello 규칙 정의에 구성 된 대로 지시 합니다. SSL 사용한 웹 응용 프로그램에서 응용 프로그램 게이트웨이 hello SNI 서버 이름 표시 () 확장 toochoose hello 올바른 수신기 hello 웹 트래픽에 대 한 사용합니다. 여러 사이트 호스팅에 대 한 일반적인 용도는 다른 웹 도메인 toodifferent 백 엔드 서버 풀에 대 한 tooload 잔액 요청입니다. 마찬가지로 여러 하위 도메인의 hello에 동일한 루트 도메인을 호스팅할 수 또한 동일한 응용 프로그램 게이트웨이 hello 합니다.

## <a name="scenario"></a>시나리오

다음 예제는 hello에서 응용 프로그램 게이트웨이으로 두 개의 백 엔드 서버 풀 contoso.com과 fabrikam.com을에 대 한 트래픽을 제공: contoso 서버 풀 및 fabrikam 서버 풀입니다. 유사한 설정을 app.contoso.com 및 blog.contoso.com와 같은 하위 도메인을 사용 하는 toohost 될 수 있습니다.

![다중 사이트 시나리오][multisite]

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오는 멀티 사이트 지원 tooan 기존 응용 프로그램 게이트웨이 추가합니다. toocomplete이이 시나리오에서는 기존 응용 프로그램 게이트웨이 toobe 사용 가능한 tooconfigure 필요 합니다. 방문 [hello 포털을 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-portal.md) toolearn 어떻게 toocreate hello 포털에서 기본 응용 프로그램 게이트웨이 합니다.

hello 다음은 tooupdate hello 응용 프로그램 게이트웨이 위해 필요한 hello 단계입니다.

1. 각 사이트에 대 한 백 엔드 풀 toouse를 만듭니다.
2. 각 사이트 Application Gateway에서 지원할 수신기를 만듭니다.
3. Hello 적절 한 백 엔드 사용 규칙 toomap 각 수신기를 만듭니다.

## <a name="requirements"></a>요구 사항

* **백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다. 나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다. FQDN을 사용할 수도 있습니다.
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.
* **프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다. 트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.
* **수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우. 다중 사이트 지원 응용 프로그램 게이트웨이의 경우 호스트 이름 및 SNI 표시도 추가됩니다.
* **규칙:** hello 규칙 hello 수신기를 hello 백 엔드 서버 풀에 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다. 트래픽 구체적인 정도 관계 없이 일치 하는 hello 첫 번째 규칙을 통해 이동 됩니다 및 규칙 나열 된 hello 순서로 처리 됩니다. 예를 들어 기본 수신기를 사용 하 여 규칙과 동일한 포트를 사용 하는 hello 규칙 hello에서 모두 다중 사이트 수신기를 사용 하 여 규칙을 설정한 경우 hello 다중 사이트 수신기 해야 보다 먼저 나열 되어야 hello 규칙으로 다중 사이트 규칙 toofunction hello에 대 한 순서 대로 기본 수신기 hello와 가 필요합니다. 
* **인증서:** 각 수신기에는 고유한 인증서가 필요하며, 이 예에서는 다중 사이트의 수신기가 2개 만들어집니다. 두 개의.pfx 인증서와 해당에 대 한 hello 암호 만든 toobe가 필요 합니다.

## <a name="create-back-end-pools-for-each-site"></a>각 사이트에 사용할 백 엔드 풀 만들기

Application Gateway에서 지원할 각 사이트에는 백 엔드 풀이 필요합니다. 이 예에서는 2개 백 엔드 풀, 즉 하나는 contoso11.com, 다른 하나는 fabrikam11.com의 백 엔드 풀이 만들어집니다.

### <a name="step-1"></a>1단계

Azure 포털 (https://portal.azure.com) hello에 tooan 기존 응용 프로그램 게이트웨이 이동 합니다. **백엔드 풀**을 선택하고 **추가**를 클릭합니다.

![백 엔드 풀 추가][7]

### <a name="step-2"></a>2단계

Hello 백 엔드 풀에 대 한 hello 정보를 입력 **pool1**hello 백 엔드 서버에 대 한 hello ip 주소 또는 Fqdn을 추가 하 고 클릭, **확인**

![pool1 백엔드 풀 설정][8]

### <a name="step-3"></a>3단계

Hello 백 엔드 풀 블레이드에서 클릭 **추가** tooadd 프로그램 추가 백 엔드 풀 **pool2**hello 백 엔드 서버에 대 한 hello ip 주소 또는 FQDN을 추가 하 고 클릭, **확인**

![pool2 백엔드 풀 설정][9]

## <a name="create-listeners-for-each-back-end"></a>각 백 엔드 풀의 수신기 만들기

응용 프로그램 게이트웨이 HTTP 1.1 사용 한 웹 사이트에 둘 이상의 호스트 헤더 toohost hello 동일한 공용 IP 주소 및 포트. hello 기본 수신기 hello 포털에서 만들어진이 속성이 포함 되어 있지 않습니다.

### <a name="step-1"></a>1단계

클릭 **수신기** 기존 응용 프로그램 게이트웨이 hello 되 고 클릭 **다중 사이트** tooadd hello에 대 한 첫 번째 수신기입니다.

![수신기 개요 블레이드][1]

### <a name="step-2"></a>2단계

Hello 수신기에 대 한 hello 정보를 입력 합니다. 이 예에서는 SSL 종료를 구성하고 새 프런트 엔드 포트를 만듭니다. SSL 종료에 사용 되는 hello.pfx 인증서 toobe를 업로드 합니다. 이 블레이드 비교 toohello 표준 기본 수신기 블레이드에서 hello 유일한 차이는 hello 호스트 이름입니다.

![수신기 속성 블레이드][2]

### <a name="step-3"></a>3단계

클릭 **다중 사이트** hello 두 번째 사이트에 대 한 hello 이전 단계에 설명 된 대로 다른 수신기를 만듭니다. 있는지 toouse hello 두 번째 수신기에 대 한 다른 인증서를 확인 합니다. 이 블레이드 비교 toohello 표준 기본 수신기 블레이드에서 hello 유일한 차이는 hello 호스트 이름입니다. Hello 수신기에 대 한 hello 정보를 입력 하 고 클릭 **확인**합니다.

![수신기 속성 블레이드][3]

> [!NOTE]
> Hello 응용 프로그램 게이트웨이 용 Azure 포털의에서 수신기 생성은 장기 실행 작업, 소요 시간 toocreate hello 일부 두 수신기가이 시나리오에서는 합니다. 경우 전체 hello 수신기 hello 다음 이미지와 같이 hello 포털에서 보여 줍니다.

![수신기 개요][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>규칙 toomap 수신기 toobackend 풀 만들기

### <a name="step-1"></a>1단계

Azure 포털 (https://portal.azure.com) hello에 tooan 기존 응용 프로그램 게이트웨이 이동 합니다. 선택 **규칙** hello 기존 기본 규칙을 선택 하 고 **rule1** 클릭 **편집**합니다.

### <a name="step-2"></a>2단계

다음 이미지는 hello와 같이 hello 규칙 블레이드를 입력 합니다. 첫 번째 수신기 hello 및 첫 번째 풀을 선택 하 고 클릭 하면 **저장** 완료 된 경우.

![기존 규칙 편집][6]

### <a name="step-3"></a>3단계

클릭 **기본 규칙** toocreate hello에 대 한 두 번째 규칙입니다. Hello 두 번째 수신기 및 두 번째 백 엔드 풀과 hello 양식을 작성 하 고 클릭 **확인** toosave 합니다.

![기본 규칙 추가 블레이드][10]

이 시나리오를 완료 hello Azure 포털을 통한 멀티 사이트 지원을 사용 하 여 기존 응용 프로그램 게이트웨이 구성 합니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 tooprotect와 웹 사이트 [응용 프로그램 게이트웨이-웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
