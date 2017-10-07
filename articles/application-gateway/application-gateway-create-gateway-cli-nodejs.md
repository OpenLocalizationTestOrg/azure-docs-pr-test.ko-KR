---
title: "Azure 응용 프로그램 게이트웨이-aaaCreate Azure CLI 1.0 | Microsoft Docs"
description: "Toocreate 응용 프로그램 게이트웨이 사용 하 여 리소스 관리자의 Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Hello Azure CLI를 사용 하 여 응용 프로그램 게이트웨이 만들기

> [!div class="op_single_selector"]
> * [Azure 포털](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure 클래식 PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager 템플릿](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)
> 
> 

Azure Application Gateway는 계층 7 부하 분산 장치입니다. 장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다. 응용 프로그램 게이트웨이 같은 응용 프로그램 배달 기능 hello: HTTP 균형 조정, 쿠키 기반 세션 선호도 및 오프 로드 (SECURE Sockets Layer), 사용자 지정 상태 프로브를 로드 및 여러 사이트에 대 한 지원.

## <a name="prerequisite-install-hello-azure-cli"></a>필수 구성 요소: hello Azure CLI를 설치 합니다.

이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](../xplat-cli-install.md) 너무 필요[tooAzure 로그온](../xplat-cli-connect.md)합니다. 

> [!NOTE]
> Azure 계정이 없는 경우 계정이 필요합니다. [여기서 무료 평가판](../active-directory/sign-up-organization.md)에 등록합니다.

## <a name="scenario"></a>시나리오

이 시나리오에서는 사용 하 여 응용 프로그램 게이트웨이 toocreate Azure 포털을 hello 하는 방법을 배웁니다.

이 시나리오에서는 다음을 수행합니다.

* 두 인스턴스를 사용하여 중간 응용 프로그램 게이트웨이를 만듭니다.
* 예약된 CIDR 블록으로 10.0.0.0/16을 사용하여 이름이 ContosoVNET인 가상 네트워크를 만듭니다.
* CIDR 블록으로 10.0.0.0/28을 사용하는 subnet01이라는 서브넷을 만듭니다.

> [!NOTE]
> 사용자 지정 상태를 포함 하 여 hello 응용 프로그램 게이트웨이 추가 구성 프로브를 통해 백 엔드 풀 주소 및 추가 규칙 hello 응용 프로그램 게이트웨이 구성한 후와 초기 배포 중이 아니라 구성 됩니다.

## <a name="before-you-begin"></a>시작하기 전에

Azure Application Gateway에는 자체 서브넷이 필요합니다. 가상 네트워크를 만들 때 상태로 두고 충분 한 주소 공간 toohave 여러 서브넷을 확인 합니다. 추가 응용 프로그램 게이트웨이 수 toobe 추가 응용 프로그램 게이트웨이 tooa 서브넷을 배포한 후 toohello 서브넷입니다.

## <a name="log-in-tooazure"></a>TooAzure 로그인

열기 hello **Microsoft Azure 명령 프롬프트**, 로그인 하십시오. 

```azurecli-interactive
azure login
```

앞 예제는 hello를 입력 한 후에 코드가 제공 됩니다. Toohttps://aka.ms/devicelogin 브라우저 toocontinue hello 로그인 프로세스에서를 이동 합니다.

![장치 로그인을 보여 주는 cmd][1]

Hello 브라우저에서 hello 받은 코드를 입력 합니다. 로그인 페이지로 리디렉션된 tooa 됩니다.

![브라우저 tooenter 코드][2]

Hello 코드 입력 되 면 로그인, 닫기 hello 브라우저 toocontinue hello 시나리오입니다.

![성공적으로 로그인][3]

## <a name="switch-tooresource-manager-mode"></a>TooResource 관리자 모드를 전환 합니다.

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Hello 리소스 그룹 만들기

Hello 응용 프로그램 게이트웨이 만들기 전에 리소스 그룹 toocontain hello 응용 프로그램 게이트웨이 만들어집니다. hello 다음 hello 명령을 보여 줍니다.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>가상 네트워크 만들기

Hello 리소스 그룹을 만든 후 hello 응용 프로그램 게이트웨이 가상 네트워크가 생성 됩니다.  다음 예제는 hello, hello 주소 공간으로 hello 시나리오 노트 앞에 정의 된 대로 10.0.0.0/16 였습니다.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>서브넷 만들기

Hello 가상 네트워크를 만든 후 hello 응용 프로그램 게이트웨이 서브넷 추가 됩니다.  포함 된 경우 하려는 웹 앱과 toouse 응용 프로그램 게이트웨이 호스트 hello에 동일한 가상 네트워크에 hello 응용 프로그램 게이트웨이, 다른 서브넷에 대 한 충분 한 공간이 있는지 tooleave 수입니다.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Hello 응용 프로그램 게이트웨이 만들기

Hello 가상 네트워크 및 서브넷을 만든 후 hello hello 응용 프로그램 게이트웨이에 대 한 필수 조건을 완료 되었습니다. 또한 이전에 내보낸된.pfx 인증서와 hello 인증서의 암호를 hello는 hello 단계 다음에 필요한: hello 백 엔드에 사용 되는 hello IP 주소는 백 엔드 서버에 대 한 hello IP 주소입니다. 이러한 값 hello 가상 네트워크, 공용 ip 또는 백 엔드 서버에 대 한 정규화 된 도메인 이름을 개인 Ip 중 하나가 될 수 있습니다.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Hello 다음 명령을 실행 하는 생성 중에 제공 될 수 있는 매개 변수 목록은: **azure 네트워크 응용 프로그램 게이트웨이 만들기-도움말**합니다.

이 예제는 hello 수신기, 백 엔드 풀, 백 엔드 http 설정 및 규칙에 대 한 기본 설정으로 기본 응용 프로그램 게이트웨이 만듭니다. Hello를 프로 비전 하는 것은 성공 후 배포 설정을 toosuit 이러한을 수정할 수 있습니다.
이전 단계를 만든 후 hello hello 백 엔드 풀과 정의 된 웹 응용 프로그램에 이미 있는 경우 부하 분산 시작 합니다.

## <a name="next-steps"></a>다음 단계

사용자 지정 상태 toocreate 방문 하 여 조사 하는 방법에 대해 알아봅니다 [만들 사용자 지정 상태 프로브](application-gateway-create-probe-portal.md)

어떻게 tooconfigure SSL 오프 로딩 및 take hello 비용이 많이 드는 SSL 암호 해독 해제 하면 웹 서버 방문 하 여 자세한 [SSL 오프 로드 구성](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
