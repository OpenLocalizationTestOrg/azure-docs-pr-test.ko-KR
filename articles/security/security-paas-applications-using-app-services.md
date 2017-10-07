---
title: "PaaS aaaSecuring 웹 및 Azure 앱 서비스를 사용 하 여 모바일 응용 프로그램 | Microsoft Docs"
description: " PaaS 웹 및 모바일 응용 프로그램 보안을 위한 Azure App Services 보안 모범 사례에 대해 알아봅니다. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>Azure App Services를 사용하여 PaaS 웹 및 모바일 응용 프로그램 보안

이 문서에서는 PaaS 웹 및 모바일 응용 프로그램 보안을 위한 [Azure App Services](https://azure.microsoft.com/services/app-service/) 보안 모범 사례에 대해 설명합니다. 이들 모범 사례는 Azure에 대 한 경험 및 고객의 hello 경험을와 같은 직접 합니다.

## <a name="azure-app-services"></a>Azure App Services
[Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 은 어디에서 든 지 toodata hello 클라우드 또는 온-프레미스에 연결 하 고 웹 앱 및 모든 플랫폼 이나 장치에 대 한 모바일 앱을 만들 수 있는 PaaS 제품입니다. 응용 프로그램 서비스는 hello 웹 및 Azure 웹 사이트 및 Azure 모바일 서비스와 별도로 이전에 전달 된 모바일 특성을 포함 합니다. 또한 비즈니스 프로세스를 자동화하고 클라우드 API를 호스팅하는 새 기능을 포함합니다. 단일 통합 서비스로 응용 프로그램 서비스 tooweb, 모바일, 및 통합 시나리오 풍부한 기능을 제공합니다.

더 toolearn에 개요를 참조 [모바일 앱](../app-service-mobile/app-service-mobile-value-prop.md) 및 [웹 앱](../app-service-web/app-service-web-overview.md)합니다.

## <a name="best-practices"></a>모범 사례

App Services를 사용하는 경우 다음 모범 사례를 따릅니다.

- [Azure AD(Active Directory)를 통해 인증](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory)합니다. App Services는 ID 공급자를 위한 OAuth 2.0 서비스를 제공합니다. OAuth 2.0은 클라이언트 개발자의 단순성에 기반하여 웹 응용 프로그램, 데스크톱 응용 프로그램 및 휴대폰에 대한 특정 권한 부여 흐름을 제공합니다. Azure AD에서는 OAuth 2.0 tooenable tooauthorize toomobile 및 웹 응용 프로그램에 액세스할 수 있습니다.
- Hello 필요 tooknow 및 최소 권한의 보안 원칙에 따라 액세스를 제한 합니다. 액세스를 제한 하는 것은 데이터 액세스를 위한 보안 정책 tooenforce 하려는 조직에 필수적입니다. 역할 기반 액세스 제어 (RBAC) 사용 하는 tooassign 권한 toousers, 그룹 및 특정 범위의 응용 프로그램 수 있습니다. 사용자가 tooapplications, 액세스 권한을 부여할 때는 신중을 더 toolearn 참조 [액세스 관리 시작](../active-directory/role-based-access-control-what-is.md)합니다.
- 키를 보호합니다. 보안이 아무리 훌륭하더라도 구독 키를 분실하면 안됩니다. Azure 키 자격 증명 모음은 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 됩니다. Key Vault를 사용하여, 키와 비밀(예: 인증 키, 저장소 계정 키, 데이터 암호화 키, PFX 파일 및 암호)을 암호화에 하드웨어 보안 모듈(HSM)로 보호된 키를 사용합니다. 추가된 보증을 위해, HSM에서 키를 생성하거나 가져올 수 있습니다. 참조 [Azure 키 자격 증명 모음](../key-vault/key-vault-whatis.md) toolearn 더 합니다. 사용할 수도 있습니다 키 자격 증명 모음 toomanage TLS 인증서 자동 갱신 합니다.
- 들어오는 원본 IP 주소를 제한합니다. [App Services 환경](../app-service-web/app-service-app-service-environment-intro.md)에는 NSG(네트워크 보안 그룹)를 통해 들어오는 원본 IP 주소를 제한하는 데 도움이 되는 가상 네트워크 통합 기능이 있습니다. Azure 가상 네트워크 (Vnet) 모르는 경우 이것이 tooplace에 대 한 다양 한 사용자가 제어 하는 인터넷이 아닌, 라우팅할 수 있는 네트워크에 Azure 리소스가 액세스를 허용 하는 기능입니다. toolearn 더 참조 [앱을 Azure 가상 네트워크와 통합](../app-service-web/web-sites-integrate-with-vnet.md)합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 응용 프로그램 서비스 PaaS 웹 및 모바일 응용 프로그램 보안에 대 한 보안 모범 사례의 tooa 컬렉션을 도입 되었습니다. PaaS 배포의 경우 보안에 대 한 더 toolearn 참조:

- [PaaS 배포 보안](security-paas-deployments.md)
- [Azure SQL Database 및 SQL Data Warehouse를 사용하여 PaaS 웹 및 모바일 응용 프로그램 보안](security-paas-applications-using-sql.md)
