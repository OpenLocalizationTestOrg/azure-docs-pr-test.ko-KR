---
title: "SQL 데이터베이스 연결 아키텍처 aaaAzure | Microsoft Docs"
description: "이 문서에서는 hello Azure SQLDB 연결 아키텍처에서 Azure 내에서 또는 Azure 외부에서."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Azure SQL Database 연결 아키텍처 

이 문서는 hello Azure SQL 데이터베이스 연결 아키텍처에 설명 하 고 hello 서로 다른 구성 요소에서 Azure SQL 데이터베이스 인스턴스의 트래픽 tooyour toodirect를 어떻게 작동 하는지 설명 합니다. 이러한 Azure SQL 데이터베이스 연결 구성 요소는 Azure 내에서 연결 하는 클라이언트와 Azure 외부에서 연결 하는 클라이언트 toodirect 네트워크 트래픽 toohello Azure 데이터베이스를 작동 합니다. Hello 고려 사항 관련 toochanging hello 기본 연결 설정 및이 문서는 또한 스크립트 샘플 toochange 연결 발생 하는 방법을 제공 합니다. 이 문서를 읽은 후에 질문이 있는 경우에 dmalik@microsoft.com에서 Dhruv에 문의하세요. 

## <a name="connectivity-architecture"></a>연결 아키텍처

다음 다이어그램 hello hello Azure SQL 데이터베이스 연결 아키텍처의 대략적인 개요를 제공 합니다. 

![아키텍처 개요](./media/sql-database-connectivity-architecture/architecture-overview.png)


hello 다음과 같은 단계로 진행 방법을 hello Azure SQL 데이터베이스 소프트웨어 부하 분산 장치 (SLB) 및 hello Azure SQL 데이터베이스 게이트웨이 통해 설정 된 tooan Azure SQL 데이터베이스를 연결할 수 있습니다.

- Azure 내에서 또는 Azure 외부의 클라이언트 연결 toohello SLB는 공용 IP 주소를 포함 하 고 포트 1433에서 수신 합니다.
- SLB hello toohello Azure SQL 데이터베이스 게이트웨이 트래픽을 보냅니다.
- hello 게이트웨이 hello 트래픽 toohello 올바른 프록시 미들웨어를 리디렉션합니다.
- hello 프록시 미들웨어 hello 트래픽 toohello 적절 한 Azure SQL 데이터베이스를 리디렉션합니다.

> [!IMPORTANT]
> 이러한 각 구성이 요소는 서비스 거부 (DDoS) 서비스 보호 hello 네트워크 및 hello 응용 프로그램 계층에서 기본 제공 배포 합니다.
>

## <a name="connectivity-from-within-azure"></a>Azure 내부에서 연결

Azure 내부에서 연결하는 경우 연결에는 기본적으로 **리디렉션** 연결 정책이 있습니다. 에 대 한 정책을 **리디렉션** hello TCP 세션이 설정 된 toohello Azure SQL 데이터베이스 후 연결을 hello 클라이언트 세션 임을 의미 다음에서 변경 toohello 대상 가상 IP 사용 하 여 toohello 프록시 미들웨어 리디렉션 hello Azure SQL 데이터베이스 게이트웨이 toothat hello 프록시 미들웨어의입니다. 그런 후 모든 후속 패킷이 hello Azure SQL 데이터베이스 게이트웨이 무시 hello 프록시 미들웨어를 통해 직접 흐름입니다. 다음 다이어그램 hello이 트래픽 흐름을 보여 줍니다.

![아키텍처 개요](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Azure 외부에서 연결

Azure 외부에서 연결하는 경우 연결에는 기본적으로 **프록시** 연결 정책이 있습니다. 에 대 한 정책을 **프록시** hello TCP 세션이 hello Azure SQL 데이터베이스 게이트웨이 통해 설정 되 고 모든 후속 패킷이 흐름을 통해 의미 hello 게이트웨이 합니다. 다음 다이어그램 hello이 트래픽 흐름을 보여 줍니다.

![아키텍처 개요](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Azure SQL Database 게이트웨이 IP 주소

온-프레미스 리소스에서 tooconnect tooan Azure SQL 데이터베이스, Azure 지역에 대 한 tooallow 아웃 바운드 네트워크 트래픽은 toohello Azure SQL 데이터베이스 게이트웨이 할 수 있습니다. 온-프레미스 리소스에서 연결할 때 hello 기본 설정인 프록시 모드에서는 연결할 때 연결에만 hello 게이트웨이 통해 이동 합니다.

다음 표에 hello hello 모든 데이터 영역에 대 한 hello Azure SQL 데이터베이스 게이트웨이의 Ip 기본 및 보조 합니다. 일부 지역에는 두 개의 IP 주소가 있습니다. 이 영역에 hello 기본 IP 주소는 hello 게이트웨이의 hello 현재 IP 주소가 고 hello 두 번째 IP 주소는 장애 조치 IP 주소입니다. hello 장애 조치 주소는 hello 주소 toowhich tookeep hello 서비스 서버 가용성 높은 이동 될 수 있습니다. 이러한 영역에 대 한 허용 아웃 바운드 tooboth hello IP 주소 하는 것이 좋습니다. hello 두 번째 IP 주소에서 수신 하지 않습니다 모든 서비스를 Azure SQL 데이터베이스 tooaccept 연결에 의해 활성화 될 때까지 Microsoft가 소유 하 고 하 고

| 지역 이름 | 기본 IP 주소 | 보조 IP 주소 |
| --- | --- |--- |
| 오스트레일리아 동부 | 191.238.66.109 | 13.75.149.87 |
| 오스트레일리아 동남부 | 191.239.192.109 | 13.73.109.251 |
| 브라질 남부 | 104.41.11.5 | |    
| 캐나다 중부 | 40.85.224.249 | |    
| 캐나다 동부 | 40.86.226.166 | |
| 미국 중부 | 23.99.160.139 | 13.67.215.62 |
| 동아시아 | 191.234.2.139 | 52.175.33.150 |
| 미국 동부 1 | 191.238.6.43 | 40.121.158.30 |
| 미국 동부 2 | 191.239.224.107 | 40.79.84.180 |
| 인도 중부 | 104.211.96.159  | |   
| 인도 남부 | 104.211.224.146  | |
| 인도 서부 | 104.211.160.80 | |
| 일본 동부 | 191.237.240.43 | 13.78.61.196 |
| 일본 서부 | 191.238.68.11 | 104.214.148.156 |
| 한국 중부 | 52.231.32.42 | |
| 한국 남부 | 52.231.200.86 |  |
| 미국 중북부 | 23.98.55.75 | 23.96.178.199 |
| 북유럽 | 191.235.193.75 | 40.113.93.91 |
| 미국 중남부 | 23.98.162.75 | 13.66.62.124 |
| 동남아시아 | 23.100.117.95 | 104.43.15.0 |
| 영국 북부 | 13.87.97.210 | |
| 영국 남부 1 | 51.140.184.11 | |    
| 영국 남부 2 | 13.87.34.7 | |
| 영국 서부 | 51.141.8.11  | |
| 미국 중서부 | 13.78.145.25 | |
| 서유럽 | 191.237.232.75 | 40.68.37.158 |
| 미국 서부 1 | 23.99.34.75 | 104.42.238.205 |
| 미국 서부 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>SQL Database 연결 정책 변경

Azure SQL 데이터베이스 서버를 사용 하 여 hello에 대 한 Azure SQL 데이터베이스 연결 정책 toochange hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx)합니다. 

- 연결 정책을 너무 설정 되어 있으면**프록시**, 패킷 흐름 hello Azure SQL 데이터베이스 게이트웨이 통해 모든 네트워크입니다. 이 설정은 tooallow 아웃 바운드 tooonly hello Azure SQL 데이터베이스 게이트웨이 IP 필요합니다. **프록시** 설정을 사용하면 **리디렉션** 설정보다 대기 시간이 길어집니다. 
- 연결 정책을 설정 하는 경우 **리디렉션**, 모든 네트워크 패킷 흐름 직접 toohello 미들웨어 프록시입니다. 이 설정은 tooallow 아웃 바운드 toomultiple Ip 필요합니다. 

## <a name="script-toochange-connection-settings"></a>스크립트 toochange 연결 설정

> [!IMPORTANT]
> 이 스크립트는 hello 필요 [Azure PowerShell 모듈](/powershell/azure/install-azurerm-ps)합니다.
>

PowerShell 스크립트 뒤 hello toochange 연결 정책을 hello 하는 방법을 보여 줍니다.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>다음 단계

- 참조 toochange Azure SQL 데이터베이스 서버에 대 한 Azure SQL 데이터베이스 연결 정책을 hello 하는 방법에 대 한 내용은 [REST API를 hello 만들기 또는 업데이트 서버 연결 정책을 사용 하 여](https://msdn.microsoft.com/library/azure/mt604439.aspx)합니다.
- ADO.NET 4.5 이상 버전을 사용하는 클라이언트의 Azure SQL Database 연결 동작에 대한 자세한 정보는 [ADO.NET 4.5에 대한 1433 이외 포트](sql-database-develop-direct-route-ports-adonet-v12.md)를 참조하세요.
- 일반 응용 프로그램 개발 개요 정보는 [SQL Database 응용 프로그램 개발 개요](sql-database-develop-overview.md)를 참조하세요.
