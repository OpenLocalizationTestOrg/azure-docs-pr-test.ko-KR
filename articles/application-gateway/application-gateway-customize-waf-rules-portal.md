---
title: "Azure 응용 프로그램 게이트웨이-Azure 포털의 aaaCustomize 웹 응용 프로그램 방화벽 규칙 | Microsoft Docs"
description: "이 문서에서는 toocustomize 웹 응용 프로그램 방화벽 규칙의 방식에 응용 프로그램 게이트웨이에서 Azure 포털 hello로 정보를 제공 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Hello Azure 포털을 통해 웹 응용 프로그램 방화벽 규칙을 사용자 지정

> [!div class="op_single_selector"]
> * [Azure 포털](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

hello Azure 응용 프로그램 게이트웨이 웹 응용 프로그램 방화벽 (WAF) 웹 응용 프로그램에 대 한 보호를 제공합니다. 이러한 보호는 hello Open 웹 응용 프로그램 보안 프로젝트 (OWASP) 핵심 규칙 집합 (CR)에서 제공 됩니다. 일부 규칙은 거짓 긍정의 원인이 되어 실제 트래픽을 차단할 수도 있습니다. 이러한 이유로 응용 프로그램 게이트웨이 hello 기능 toocustomize 규칙 그룹 및 규칙을 제공합니다. Hello 특정 규칙 그룹 및 규칙에 대 한 자세한 내용은 참조 하십시오. [웹 응용 프로그램 방화벽 CRS 규칙 그룹 및 규칙의 목록](application-gateway-crs-rulegroups-rules.md)합니다.

>[!NOTE]
> 응용 프로그램 게이트웨이 WAF 계층 hello를 사용 하지 않는 경우 hello 옵션 tooupgrade hello 응용 프로그램 게이트웨이 toohello WAF 계층 hello 오른쪽 창에 나타납니다. 

![WAF 사용][fig1]

## <a name="view-rule-groups-and-rules"></a>규칙 그룹 및 규칙 보기

**tooview 규칙 그룹 및 규칙**
   1. Toohello 응용 프로그램 게이트웨이 이동한 다음 선택 **웹 응용 프로그램 방화벽**합니다.  
   2. **고급 규칙 구성**을 선택합니다.  
   이 보기는 규칙 집합을 선택 하는 hello와 함께 제공 되는 모든 hello 규칙 그룹의 hello 페이지에는 표를 표시 합니다. Hello 규칙의 확인란이 모두 선택 되어 있습니다.

![사용하지 않도록 설정된 규칙 구성][1]

## <a name="search-for-rules-toodisable"></a>규칙 toodisable 검색

hello **웹 응용 프로그램 방화벽 설정** 블레이드는 텍스트 검색을 통해 toofilter hello 규칙 hello 기능을 제공 합니다. hello 결과 hello 규칙 그룹 및 hello 검색 한 텍스트를 포함 하는 규칙을 표시 합니다.

![규칙 검색][2]

## <a name="disable-rule-groups-and-rules"></a>규칙 그룹 및 규칙을 사용하지 않도록 설정

규칙을 사용하지 않도록 설정할 때 규칙 그룹 전체를 사용하지 않도록 설정하거나 하나 이상의 규칙 그룹에서 특정 규칙만 사용하지 않도록 설정할 수 있습니다. 

**toodisable 규칙 그룹 또는 특정 규칙**

   1. Hello 규칙 또는 toodisable 규칙 그룹을 검색 합니다.
   2. Hello toodisable 원하는 규칙에 대 한 hello 확인란의 선택을 취소 합니다. 
   2. **저장**을 선택합니다. 

![변경 내용 저장][3]

## <a name="next-steps"></a>다음 단계

비활성화 된 규칙을 구성한 후 학습할 수 있는 방법을 tooview WAF 로그 합니다. 자세한 내용은 [Application Gateway 진단](application-gateway-diagnostics.md#diagnostic-logging)을 참조하세요.

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
