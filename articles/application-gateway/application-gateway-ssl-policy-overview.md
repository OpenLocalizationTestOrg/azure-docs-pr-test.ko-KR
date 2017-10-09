---
title: "Azure 응용 프로그램 게이트웨이 aaaSSL 정책 개요 | Microsoft Docs"
description: "에 대 한 자세한 내용은 Azure 응용 프로그램 게이트웨이 tooconfigure SSL 정책 수 있습니다."
services: application gateway
documentationcenter: na
author: amsriva
manager: 
editor: 
tags: azure resource manager
ms.service: application gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure services
ms.date: 08/03/2017
ms.author: amsriva
ms.openlocfilehash: 80dbc437da3dba8a558c518ecdbb5927a11a2ed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-ssl-policy-overview"></a>Application Gateway SSL 정책 개요

응용 프로그램 게이트웨이 toocentralize SSL 인증서 관리를 허용 하 고 백 엔드 서버 팜에서 암호화 및 암호 해독 오버 헤드를 줄입니다. 또한 처리이 중앙 집중식된 SSL toospecify 중앙 SSL을 사용 하면 정책 tooyour 조직의 보안 요구 사항을 적합 합니다. 그러면 보안 지침과 권장되는 정보 및 규정 준수 요구 사항을 모두 충족할 수 있습니다.

SSL 정책에는 SSL 프로토콜 버전으로는 암호 그룹 및 암호는 SSL 핸드셰이크 중에 사용 되는 hello 순서 제어 포함 됩니다. 이 응용 프로그램 게이트웨이 방향으로 두 가지 메커니즘 tooallow 고객 toocontrol SSL 정책, 미리 정의 된 또는 사용자 지정 정책을 제공합니다.

## <a name="predefined-ssl-policy"></a>미리 정의된 SSL 정책

Application Gateway에는 세 가지 미리 정의된 보안 정책이 있습니다. 이러한 정책 tooget hello 적절 한 수준의 보안을 사용 하 여 게이트웨이 구성할 수 있습니다. hello 정책 이름은 hello 연도 및 월 구성 된 주석 처리 됩니다. 각 정책은 다른 SSL 프로토콜 버전 및 암호 그룹을 제공합니다. Toouse hello 최신 SSL 정책 tooensure hello SSL 보안을 극대화 것이 좋습니다. 응용 프로그램 게이트웨이 오늘 허용 사용자 toochoose hello 다음 중 하나에서 미리 정의 된 합니다.

### <a name="appgwsslpolicy20150501"></a>AppGwSslPolicy20150501

|속성  |값  |
|---|---|
|이름     | AppGwSslPolicy20150501        |
|MinProtocolVersion     | TLSv1_0        |
|기본값| True(미리 정의된 정책이 지정되지 않은 경우) |
|CipherSuites     |TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_DHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_DHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_3DES_EDE_CBC_SHA<br>TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA |
  
  ### <a name="appgwsslpolicy20170401"></a>AppGwSslPolicy20170401
  
|속성  |값  |
|   ---      |  ---       |
|이름     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_0        |
|기본값| False |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA |
  
### <a name="appgwsslpolicy20170401s"></a>AppGwSslPolicy20170401S

|속성  |값  |
|---|---|
|이름     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_2        |
|기본값| False |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 <br>    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 <br>    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br> |

## <a name="custom-ssl-policy"></a>SSL 정책 사용자 지정

미리 정의 된 SSL 정책 toobe 요구 사항에 대해 구성 된 경우, 해야 사용자 고유의 사용자 지정 SSL 정책을 정의 해야 합니다. 이 경우 있습니다 완전히 제어할 hello 최소 SSL 프로토콜 버전 toosupport로 지원 되는 암호 그룹 및 해당 우선 순위 순서.
 
SSL 프로토콜 버전:

* SSL 2.0 및 3.0은 모든 Application Gateway에 대해 기본적으로 비활성화됩니다. 이러한 프로토콜 버전을 구성할 수 없습니다.
* 사용자 지정 SSL 정책 정의 제공 hello 프로토콜 게이트웨이 TLSv1_0, TLSv1_1, TLSv1_2 hello 최소 SSL 프로토콜 버전으로 다음 중 하나를 tooselect 옵션입니다.
* SSL 정책을 하나도 정의하지 않으면 3개(TLSv1_0, TLSv1_1, TLSv1_2) 모두 활성화됩니다.

암호 그룹:

응용 프로그램 게이트웨이 hello 다음 사용자 지정 정책을 선택할 수 있는 암호 그룹을 지원 합니다. hello hello 암호 그룹의 순서 SSL 협상 중 hello 우선 순위 순서를 결정 합니다.

사용할 수 있는 암호 그룹:

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

## <a name="next-steps"></a>다음 단계

[Application Gateway에 SSL 정책 구성](application-gateway-configure-ssl-policy-powershell.md)
