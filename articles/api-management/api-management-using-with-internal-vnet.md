---
title: "내부 가상 네트워크와 aaaHow toouse Azure API 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toosetup 및 내부 가상 네트워크의 Azure API 관리를 구성 합니다."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>내부 가상 네트워크에서 Azure API Management를 사용하는 방법
Azure 가상 네트워크 (Vnet) API 관리 Api hello 인터넷에 액세스할 수 없습니다 관리할 수 있습니다. 다양 한 VPN 기술 사용할 수 있는 toomake hello 연결 이며 hello VNET 내에 있는 두 가지 주요 모드에서 API 관리를 배포할 수 있습니다.
* 외부
* 내부

## <a name="overview"> </a>개요
API 관리는 내부 가상 네트워크 모드에서 배포 될 때 모든 hello 서비스 끝점 (게이트웨이, 개발자 포털, 게시자 포털, 직접 관리 및 Git)만 액세스를 제어 하는 가상 네트워크 내 표시 됩니다. None hello 서비스 끝점의 공용 DNS 서버 hello에 등록 됩니다.

API 관리를 사용 하 여 내부 모드로, 다음 시나리오는 hello 얻을 수 있습니다.
* 사이트 간 연결 또는 ExpressRoute VPN 연결을 사용하여 외부의 타사에서 개인 데이터 센터에 호스팅한 API에 안전하게 액세스할 수 있게 합니다.
* 공통 게이트웨이를 통해 클라우드 기반 API와 온-프레미스 API를 공개함으로써 하이브리드 클라우드 시나리오를 사용하도록 설정합니다.
* 단일 게이트웨이 끝점을 사용하여 여러 지리적 위치에서 호스팅되는 API를 관리합니다. 

## <a name="enable-vpn"> </a>내부 가상 네트워크에 API Management 만들기
hello 내부 가상 네트워크에서 API 관리 서비스는 내부 부하 Balancer(ILB) 뒤에 호스트 됩니다. hello에 hello hello ILB의 IP 주소는 [r f c 1918](http://www.faqs.org/rfcs/rfc1918.html) 범위입니다.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Azure Portal을 사용하여 VNET 연결 사용
먼저 hello 단계에 따라 hello API 관리 서비스를 만든 [만들기 API 관리 서비스][Create API Management service]합니다. 그런 다음 설치 API 관리 toobe 내부 가상 네트워크에 배포 합니다.

![내부 가상 네트워크에서 APIM 설정을 위한 메뉴][api-management-using-internal-vnet-menu]

Hello 배포에 성공한 경우 서비스의 내부 가상 IP 주소 hello hello 대시보드에 표시 됩니다.

![내부 VNET이 구성된 API Management 대시보드][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>PowerShell cmdlet을 사용하여 VNET 연결 사용
Hello PowerShell cmdlet을 사용 하 여 VNET 연결을 설정할 수도 있습니다.

* **VNET 내 API 관리 서비스 만들기**: hello cmdlet을 사용 하 여 [새로 AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate Azure API 관리 VNET 내의 서비스 및 toouse hello 내부 VNET 유형을 구성 합니다.

* **VNET 내 기존 API 관리 서비스를 배포**: hello cmdlet을 사용 하 여 [업데이트 AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove 기존 Azure API 관리 하는 가상 네트워크 내 서비스 및 toouse 구성 내부 VNET 형식입니다.

## <a name="apim-dns-configuration"></a>DNS 구성
외부 가상 네트워크 모드에서 API Management를 사용하는 경우 Azure에서 DNS를 관리합니다. 내부 가상 네트워크 모드에서는 사용자 고유의 DNS toomanage 구조가 있습니다.

> [!NOTE]
> API 관리 서비스에 IP 주소에서 오는 toorequests 수신 대기 하지 않습니다. Toorequests toohello (게이트웨이, 개발자 포털, 게시자 포털, 직접 관리 끝점 및 git를 포함)는 서비스 끝점에 구성 된 호스트에만 응답 합니다.

### <a name="access-on-default-host-names"></a>기본 호스트 이름에 대한 액세스
API 관리 서비스는 Azure 공용 클라우드에서 예를 들어 "contoso" 라는 만들면 hello 다음 서비스 끝점 기본적으로 구성 됩니다.

>   게이트웨이/프록시 - contoso.azure-api.net

> 게시자 포털 및 개발자 포털 - contoso.portal.azure-api.net

> 직접 관리 끝점 - contoso.management.azure-api.net

>   GIT - contoso.scm.azure-api.net

tooaccess 이러한 API 관리 서비스 끝점을 사용 하 여 API 관리를 배포 하는 연결 된 서브넷 toohello 가상 네트워크에서 가상 컴퓨터를 만들 수 있습니다. 서비스에 대 한 내부 가상 IP 주소 hello 10.0.0.5로 가정 하 고 할 수 있는 호스트 파일 매핑 (%SystemDrive%\drivers\etc\hosts)를 다음과 같이 hello:

> 10.0.0.5    contoso.azure-api.net

> 10.0.0.5    contoso.portal.azure-api.net

> 10.0.0.5    contoso.management.azure-api.net

> 10.0.0.5    contoso.scm.azure-api.net

Hello 만든 가상 컴퓨터에서에서 모든 hello 서비스 끝점에 액세스할 수 있습니다. 가상 네트워크에서 사용자 지정 DNS 서버를 사용하는 경우 A DNS 레코드를 만들고 가상 네트워크의 어느 곳에서나 이러한 끝점에 액세스할 수 있습니다. 

### <a name="access-on-custom-domain-names"></a>사용자 지정 도메인 이름에 대한 액세스
Tooaccess hello hello 기본 호스트 이름 가진 API 관리 서비스를 사용 하지 않으려는 경우 모든 서비스 끝점 같은 아래에 대 한 사용자 지정 도메인 이름을 설정할 수 있습니다.

![API Management를 위한 사용자 지정 도메인 설정][api-management-custom-domain-name]

그런 다음 가상 네트워크 내에서 액세스할 수 있는 이러한 끝점의 DNS 서버 tooaccess: A 레코드를 만들 수 있습니다.

## <a name="related-content"> </a>관련 콘텐츠
* [VNET에 APIM을 설정하는 동안의 일반 네트워크 구성 문제][Common Network Configuration Issues]
* [가상 네트워크 FAQ](../virtual-network/virtual-networks-faq.md)
* [DNS에 A 레코드 만들기](https://msdn.microsoft.com/en-us/library/bb727018.aspx)(영문)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
