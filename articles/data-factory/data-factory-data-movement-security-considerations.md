---
title: "Azure Data Factory에서 데이터 이동 위한 aaaSecurity 고려 사항 | Microsoft Docs"
description: "Azure Data Factory에서 데이터 이동 보안에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 4bfce8884df14ad5b94e28ad3dfcf7025e2130a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---security-considerations-for-data-movement"></a>Azure Data Factory - 데이터 이동을 위한 보안 고려 사항
## <a name="introduction"></a>소개
이 문서에서는 Azure Data Factory에서 데이터 이동 서비스를 있는지 toosecure 데이터를 사용 하는 기본 보안 인프라를 설명 합니다. Azure Data Factory 관리 리소스는 Azure 보안 인프라를 기반으로 하며 Azure가 제공하는 모든 가능한 보안 수단을 사용합니다.

Data Factory 솔루션에서 하나 이상의 데이터 [파이프라인](data-factory-create-pipelines.md)를 만듭니다. 파이프라인은 함께 작업을 수행하는 활동의 논리적 그룹화입니다. 이러한 파이프라인 hello 영역 hello 데이터 팩터리에서 생성 된 위치에 있어야 합니다. 

데이터 팩터리는에서 사용할 수 있는 경우에 **West US**, **미국 동부**, 및 **유럽 북부** 지역 hello 데이터 이동 서비스를 사용할 수 [에 전체적으로 여러 지역](data-factory-data-movement-activities.md#global)합니다. 아직 데이터 팩터리 서비스에서는 데이터에는 지역 남지 않습니다 / 지역 명시적으로 지시 하지 않는 한 hello 서비스 toouse 대체 지역 hello 데이터 이동 서비스가 없으면 toothat 영역을 배포 합니다. 

Azure Data Factory 자체는 인증서를 사용하여 암호화된 클라우드 데이터 저장소에 대한 링크된 서비스 자격 증명을 제외한 모든 데이터를 저장하지 않습니다. Tooorchestrate 간의 데이터 이동을 데이터 기반 워크플로 만들 수 있습니다 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 및 사용 하 여 데이터의 처리 [계산 서비스](data-factory-compute-linked-services.md) 온-프레미스 또는 다른 지역 들에 환경입니다. 또한 있습니다 너무[워크플로 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 프로그래밍 방식으로 모두 사용 하 여 및 UI 메커니즘입니다.

Azure Data Factory를 사용한 데이터 이동은 다음에 대해 **인증을 받았습니다**.
-   [HIPAA/HITECH](https://www.microsoft.com/en-us/trustcenter/Compliance/HIPAA)  
-   [ISO/IEC 27001](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27001)  
-   [ISO/IEC 27018](https://www.microsoft.com/en-us/trustcenter/Compliance/ISO-IEC-27018) 
-   [CSA STAR](https://www.microsoft.com/en-us/trustcenter/Compliance/CSA-STAR-Certification)
     
Azure 규정 준수 및 Azure 자체 인프라를 보호 하는 방법을에 관심이 방문 하 여 hello [Microsoft 보안 센터](https://www.microsoft.com/TrustCenter/default.aspx)합니다. 

이 문서에서 검토 하 고 hello 다음 두 개의 데이터 이동 시나리오의에서 보안 고려 사항: 

- **클라우드 시나리오** - 이 시나리오에서는 출처와 목적지 모두 인터넷을 통해 공개적으로 액세스할 수 있습니다. 여기에는 Azure Storage, Azure SQL Data Warehouse, Azure SQL Database, Azure Data Lake Store, Amazon S3, Amazon Redshift, Salesforce와 같은 SaaS 서비스, FTP 및 OData와 같은 웹 프로토콜과 같은 관리 클라우드 저장소 서비스가 포함됩니다. 지원되는 데이터 원본 목록은 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats)에 있습니다.
- **하이브리드 시나리오**-이 시나리오에서 원본 또는 대상이 방화벽 뒤에 또는 온-프레미스 회사 네트워크 또는 hello 데이터 내 저장소는 개인 네트워크에서 / 가상 네트워크 (가장 자주 hello 원본) 및 공개적으로 액세스할 수 없는 . 가상 컴퓨터에서 호스팅되는 데이터베이스 서버도 이 시나리오에 해당합니다.

## <a name="cloud-scenarios"></a>클라우드 시나리오
###<a name="securing-data-store-credentials"></a>데이터 저장소 자격 증명 보안
Azure Data Factory는 **Microsoft에서 관리하는 인증서**를 사용하여 **암호화**하여 데이터 저장소 자격 증명을 보호합니다. 이 인증서는 **2년마다** 갱신됩니다(인증서 갱신 및 자격 증명 마이그레이션 포함). 이러한 암호화된 자격 증명은 **Azure Data Factory 관리 서비스에서 관리하는 Azure Storage**에 안전하게 저장됩니다. Azure Storage 보안에 대한 자세한 내용은 [Azure Storage 보안 개요](../security/security-storage-overview.md)를 참조하세요.

### <a name="data-encryption-in-transit"></a>전송 중 암호화
Hello 클라우드 데이터 저장소에서 HTTPS 또는 TLS를 지 원하는 경우 모든 데이터가 Data Factory에서 데이터 이동 서비스 간에 전송 되 고 HTTPS 또는 TLS 보안 채널을 통해 클라우드 데이터 저장소는.

> [!NOTE]
> 모든 연결이 너무**Azure SQL 데이터베이스** 및 **Azure SQL 데이터 웨어하우스** 데이터 hello 데이터베이스에서 tooand 전송 되는 동안 항상 암호화 (SSL/TLS)가 필요 합니다. JSON 편집기를 사용 하 여 파이프라인을 제작 하는 동안 추가 hello **암호화** 속성 너무 설정**true** hello에 **연결 문자열**합니다. Hello를 사용 하는 경우 [복사 마법사](data-factory-azure-copy-wizard.md), hello 마법사는 기본적으로이 속성을 설정 합니다. 에 대 한 **Azure 저장소**를 사용할 수 있습니다 **HTTPS** hello 연결 문자열에 있습니다.

### <a name="data-encryption-at-rest"></a>휴지 상태의 암호화
일부 데이터 저장소가 미사용 데이터 암호화를 지원합니다. 이러한 데이터 저장소에 데이터 암호화 메커니즘을 사용하는 것이 좋습니다. 

#### <a name="azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스
Azure SQL 데이터 웨어하우스 투명 한 데이터 암호화 (TDE) 실시간 암호화 및 미사용 데이터의 암호 해독을 수행 하 여 악의적인 활동의 위협을 hello에 대 한 보호에 도움이 됩니다. 이 동작은 투명 toohello 클라이언트에 설명 합니다. 자세한 내용은 [SQL Data Warehouse에서 데이터베이스 보호](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md)를 참조하세요.

#### <a name="azure-sql-database"></a>Azure SQL Database
Azure SQL 데이터베이스는 toohello 응용 프로그램 변경 하지 않고도 실시간 암호화 및 hello 데이터 암호 해독을 수행 하 여 악의적인 활동의 hello 취약점 으로부터 보호 하는 데 도움이 투명 한 데이터 암호화 (TDE)도 지원 합니다. 이 동작은 투명 toohello 클라이언트에 설명 합니다. 자세한 내용은 [Azure SQL Database를 사용한 투명한 데이터 암호화](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)를 참조하세요. 

#### <a name="azure-data-lake-store"></a>Azure Data Lake Store
또한 azure 데이터 레이크 저장소 hello 계정에 저장 된 데이터에 대 한 암호화를 제공 합니다. 사용 하도록 설정 데이터 레이크 저장소 자동으로 유지 하기 전에 데이터를 암호화 하 고 검색을 투명 하 게 toohello 클라이언트 hello 데이터에 액세스 하기 전에 암호를 해독 합니다. 자세한 내용은 [Azure Data Lake Store의 데이터 보안](../data-lake-store/data-lake-store-security-overview.md)을 참조하세요. 

#### <a name="azure-blob-storage-and-azure-table-storage"></a>Azure Blob Storage 및 Azure Table Storage
Azure Blob 저장소 및 Azure 테이블 저장소는 저장소 서비스 암호화 SSE (), 유지 toostorage 하기 전에 데이터와 해독 검색 하기 전에 자동으로 암호화를 지원 합니다. 자세한 내용은 [미사용 데이터에 대한 Azure 저장소 서비스 암호화](../storage/common/storage-service-encryption.md)를 참조하세요.

#### <a name="amazon-s3"></a>Amazon S3
Amazon S3는 미사용 데이터의 클라이언트 및 서버 암호화를 모두 지원합니다. 자세한 내용은 [암호화를 사용하여 데이터 보호](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html)를 참조하세요. 현재, 데이터 팩터리는 VPC(가상 사설 클라우드) 내에서 Amazon S3를 지원하지 않습니다.

#### <a name="amazon-redshift"></a>Amazon Redshift
Amazon Redshift는 미사용 데이터에 대한 클러스터 암호화를 지원합니다. 자세한 내용은 [Amazon Redshift 데이터베이스 암호화](http://docs.aws.amazon.com/redshift/latest/mgmt/working-with-db-encryption.html)를 참조하세요. 현재, 데이터 팩터리는 VPC 내에서 Amazon Redshift를 지원하지 않습니다. 

#### <a name="salesforce"></a>Salesforce
Salesforce는 모든 파일, 첨부 파일, 사용자 정의 필드의 암호화를 허용하는 Shield Platform Encryption을 지원합니다. 자세한 내용은 참조 [웹 서버 OAuth 인증 흐름 이해 hello](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm)합니다.  

## <a name="hybrid-scenarios-using-data-management-gateway"></a>하이브리드 시나리오(데이터 관리 게이트웨이 사용)
하이브리드 시나리오에는 데이터 관리 게이트웨이 toobe (Azure) 가상 네트워크 또는 가상 사설 클라우드 (Amazon) 내 온-프레미스 네트워크에 설치 해야 합니다. hello 게이트웨이 수 tooaccess hello 로컬 데이터 저장소 여야 합니다. Hello 게이트웨이에 대 한 자세한 내용은 참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)합니다. 

![데이터 관리 게이트웨이 채널](media/data-factory-data-movement-security-considerations/data-management-gateway-channels.png)

hello **명령 채널** Data Factory에서 데이터 이동 서비스 및 데이터 관리 게이트웨이 간의 통신을 허용 합니다. 정보를 포함 하는 hello 통신 관련 toohello 활동입니다. hello 데이터 채널은 온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 데이터를 전송 하는 데 사용 됩니다.    

### <a name="on-premises-data-store-credentials"></a>온-프레미스 데이터 저장소 자격 증명
온-프레미스 데이터 저장소에 대 한 hello 자격 증명을 로컬로 저장 됩니다 (hello 클라우드)에 없습니다. 세 가지 방법으로 설정할 수 있습니다. 

- Azure Portal/복사 마법사에서 HTTPS를 통해 **일반 텍스트**(보안 수준 낮음)를 사용합니다. 일반 텍스트 toohello 온-프레미스 게이트웨이 hello 자격 증명이 전달 됩니다.
- **복사 마법사에서 JavaScript 암호화 라이브러리** 사용 중.
- **한 번 클릭 기반 자격 증명 관리자 앱** 사용. hello 클릭-응용 프로그램 액세스 toohello 게이트웨이 않으며 hello 데이터 저장소에 대 한 자격 증명을 설정 하는 hello 온-프레미스 컴퓨터에서 실행 되 면입니다. 이 옵션 및 다음는 hello hello 가장 강력한 보안 옵션입니다. hello 자격 증명 관리자 앱 기본적으로 사용 하 여 hello 포트 8050 hello 보안 통신을 위해 게이트웨이 컴퓨터에 합니다.  
- 사용 하 여 [새로 AzureRmDataFactoryEncryptValue](/powershell/module/azurerm.datafactories/New-AzureRmDataFactoryEncryptValue) PowerShell cmdlet tooencrypt 자격 증명입니다. hello cmdlet hello 인증서 해당 게이트웨이 구성 된 toouse tooencrypt hello 자격 증명을 사용 합니다. 이 cmdlet에서 반환 하는 hello 암호화 된 자격 증명을 사용 하 고 너무 추가할 수**EncryptedCredential** hello 요소의 **connectionString** hello로 사용 하는 hello JSON 파일의 [ 새 AzureRmDataFactoryLinkedService](/powershell/module/azurerm.datafactories/new-azurermdatafactorylinkedservice) cmdlet 또는 hello 포털에서 데이터 팩터리 편집기 hello의 hello JSON 조각입니다. 이 옵션과 hello 클릭-응용 프로그램 hello 가장 강력한 보안 옵션에 한 번입니다. 

#### <a name="javascript-cryptography-library-based-encryption"></a>JavaScript 암호화 라이브러리 기반 암호화
사용 하 여 데이터 저장소 자격 증명을 암호화할 수 [JavaScript 암호화 라이브러리](https://www.microsoft.com/download/details.aspx?id=52439) hello에서 [복사 마법사](data-factory-copy-wizard.md)합니다. 이 옵션을 선택 hello 복사 마법사는 게이트웨이의 hello 공개 키를 검색 하 고 tooencrypt hello 데이터 저장소 자격 증명을 사용 합니다. hello 자격 증명 되 hello 게이트웨이 컴퓨터에서 암호를 해독 하 고 Windows에 의해 보호 [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx)합니다.

**지원되는 브라우저:** IE8, IE9, IE10, IE11, Microsoft Edge 및 최신 Firefox, Chrome, Opera, Safari 브라우저를 지원합니다. 

#### <a name="click-once-credentials-manager-app"></a>클릭 한 번 자격 증명 관리자 앱
Hello 클릭을 시작할 수 있습니다-면 파이프라인을 만들 때 Azure 포털 또는 복사 마법사에서에서 자격 증명 관리자 응용 프로그램을 기반으로 합니다. 이 응용 프로그램을 사용 하면 hello 유선을 통해 자격 증명을 일반 텍스트로 전송 되지 않습니다. 기본적으로 사용 하 여 hello 포트 **8050** hello 보안 통신을 위해 게이트웨이 컴퓨터에 있습니다. 필요한 경우 이 포트를 변경할 수 있습니다.  
  
![Hello 게이트웨이에 대 한 HTTPS 포트](media/data-factory-data-movement-security-considerations/https-port-for-gateway.png)

현재 Data Management Gateway는 단일 **인증서**를 사용합니다. 이 인증서는 hello 게이트웨이 설치 시 생성 됩니다 (tooData 관리 게이트웨이 2016 년 11 월 이후에 생성 및 버전 2.4.xxxx.x 적용 이상 버전). 이 인증서를 자신의 SSL/TLS 인증서로 바꿀 수 있습니다. Hello 클릭 하 여이 인증서를 사용 하는-자격 증명 관리자 응용 프로그램 toosecurely 데이터 저장소 자격 증명을 설정 하기 위한 toohello 게이트웨이 컴퓨터를 연결 합니다. 데이터 저장 저장소 자격 증명이 안전 하 게 온-프레미스 Windows hello를 사용 하 여 [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx) 게이트웨이 사용 하 여 hello 컴퓨터에 있습니다. 

> [!NOTE]
> 2016 년 11 월 이전 또는 버전 2.3.xxxx.x의 설치 된 이전 게이트웨이 toouse 자격 증명 암호화 및 클라우드에 저장을 계속 합니다. Hello 자격 증명이 마이그레이션된 tooan 온-프레미스 컴퓨터 hello 게이트웨이 toohello 최신 버전을 업그레이드 하는 경우에    
  
| 게이트웨이 버전(생성 중) | 저장된 자격 증명 | 자격 증명 암호화/보안 | 
| --------------------------------- | ------------------ | --------- |  
| < = 2.3.xxxx.x | 클라우드에서 | 인증서 (자격 증명 관리자 앱에서 사용 하는 hello와에서 다름)를 사용 하 여 암호화 | 
| > = 2.4.xxxx.x | 온-프레미스 | DPAPI를 통해 보안 | 
  

### <a name="encryption-in-transit"></a>전송 중 암호화
보안 채널을 통해 모든 데이터 전송을 **HTTPS** 및 **TLS over TCP** Azure 서비스와 통신 하는 동안 tooprevent 중간자 개입 공격입니다.
 
사용할 수도 있습니다 [IPSec VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md) 또는 [Express 경로](../expressroute/expressroute-introduction.md) 온-프레미스 네트워크와 Azure 간의 toofurther hello 보안 통신 채널입니다.

가상 네트워크는 hello 클라우드에서 네트워크의 논리적 표현입니다. Azure 가상 네트워크 (VNet)는 온-프레미스 네트워크 tooyour (사이트-사이트) IPSec VPN 또는 Express 경로 (개인 피어 링)을 설정 하 여 연결할 수 있습니다.       

hello 다음 표에 요약 되어 hello 네트워크 및 게이트웨이 구성 권장 사항을 기반으로 다양 한 조합을 하이브리드 데이터 이동 위한 원본 및 대상 위치입니다.

| 원본 | 대상 | 네트워크 구성 | 게이트웨이 설치 |
| ------ | ----------- | --------------------- | ------------- | 
| 온-프레미스 | 가상 네트워크에 배포된 가상 컴퓨터 및 클라우드 서비스 | IPSec VPN(지점 및 사이트 간 또는 사이트 간) | 게이트웨이는 Vnet의 온-프레미스 또는 Azure 가상 컴퓨터(VM)에 설치할 수 있습니다. | 
| 온-프레미스 | 가상 네트워크에 배포된 가상 컴퓨터 및 클라우드 서비스 | ExpressRoute(개인 피어링) | 게이트웨이는 VNet의 Azure VM 또는 온-프레미스 환경에 설치할 수 있습니다. | 
| 온-프레미스 | 공개 끝점이 있는 Azure 기반 서비스 | ExpressRoute(공용 피어링) | 게이트웨이를 온-프레미스에 설치해야 합니다. | 

hello 다음 이미지 hello의 사용을 표시 데이터 관리 게이트웨이 온-프레미스 데이터베이스 및 Express 경로 IPSec VPN (가상 네트워크와 함께)을 사용 하 여 Azure 서비스 간의 데이터 이동에:

**ExpressRoute:**
 
![게이트웨이와 함께 ExpressRoute 사용](media/data-factory-data-movement-security-considerations/express-route-for-gateway.png) 

**IPSec VPN:**

![게이트웨이가 있는 IPSec VPN](media/data-factory-data-movement-security-considerations/ipsec-vpn-for-gateway.png)

### <a name="firewall-configurations-and-whitelisting-ip-address-of-gateway"></a>게이트웨이의 방화벽 구성 및 화이트리스트 IP 주소

#### <a name="firewall-requirements-for-on-premisesprivate-network"></a>온-프레미스/개인 네트워크에 대한 방화벽 요구 사항  
기업에서는 **회사 방화벽** hello 중앙 라우터 hello 조직에서 실행 됩니다. **Windows 방화벽** 디먼는 hello 게이트웨이가 설치 된 hello 로컬 컴퓨터에서 실행 합니다. 

hello 다음 표에 나와 **아웃 바운드 포트** 및 hello에 대 한 도메인 요구 사항 **회사 방화벽**합니다.

| 도메인 이름 | 아웃바운드 포트 | 설명 |
| ------------ | -------------- | ----------- | 
| `*.servicebus.windows.net` | 443, 80 | Data Factory에 hello 게이트웨이 tooconnect toodata 이동 서비스에 필요한 |
| `*.core.windows.net` | 443 | Hello를 사용 하는 경우 hello 게이트웨이 tooconnect tooAzure 저장소 계정에서 사용 하는 [복사본을 스테이징](data-factory-copy-activity-performance.md#staged-copy) 기능입니다. | 
| `*.frontend.clouddatahub.net` | 443 | Hello 게이트웨이 tooconnect toohello Azure 데이터 팩터리 서비스에 필요합니다. | 
| `*.database.windows.net` | 1433   | (선택 사항) 목적지가 Azure SQL Database/Azure SQL Data Warehouse 인 경우 필요합니다. 사용 하 여 hello hello 포트 1433을 열지 않고 복사 기능 toocopy 데이터 tooAzure SQL 데이터베이스/Azure SQL 데이터 웨어하우스 준비입니다. | 
| `*.azuredatalakestore.net` | 443 | (선택 사항) 목적지가 Azure Data Lake 매장인 경우 필요 | 

> [!NOTE] 
> Toomanage 포트를 할 수 있습니다/허용 목록을 도메인에서 각 데이터 원본에서 필요에 따라 회사 방화벽 수준 hello 합니다. 이 표는 Azure SQL Database, Azure SQL Data Warehouse, Azure Data Lake Store만을 예제로 사용합니다.   

hello 다음 표에 나와 **인바운드 포트** hello에 대 한 요구 사항을 **windows 방화벽**합니다.

| 인바운드 포트 | 설명 | 
| ------------- | ----------- | 
| 8050(TCP) | Hello 자격 증명 관리자 응용 프로그램 toosecurely 집합 자격 증명 hello 게이트웨이에서 온-프레미스 데이터 저장소에 필요합니다. | 

![게이트웨이 포트 요구 사항](media\data-factory-data-movement-security-considerations/gateway-port-requirements.png) 

#### <a name="ip-configurations-whitelisting-in-data-store"></a>데이터 저장소의 IP 구성/화이트리스트
Hello 클라우드에서 일부 데이터 저장소에 액세스 하는 hello 컴퓨터의 IP 주소 허용 목록이 필요 합니다. Hello 게이트웨이 컴퓨터의 IP 주소 hello 허용 목록 방화벽에서 적절 하 게 구성 되어 있는지 확인 합니다.

hello 다음 클라우드 데이터 저장소 있어야 hello 게이트웨이 컴퓨터의 IP 주소의 허용 목록을 합니다. 기본적으로 이러한 데이터 저장소 중 일부는 hello IP 주소의 허용 목록이 필요 하지 않을 수 있습니다. 

- [Azure SQL Database](../sql-database/sql-database-firewall-configure.md) 
- [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal)
- [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-secure-data.md#set-ip-address-range-for-data-access)
- [Azure Cosmos DB](../documentdb/documentdb-firewall-support.md)
- [Amazon Redshift](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 

## <a name="frequently-asked-questions"></a>질문과 대답

**질문:** 에서 서로 다른 데이터 팩터리 hello 게이트웨이 공유할 수 있습니까?
**대답:** 이 기능은 아직 지원하지 않습니다. 적극적으로 노력하고 있습니다.

**질문:** hello 게이트웨이 toowork hello 포트 요구 사항은 무엇입니까?
**답변:** 게이트웨이 tooopen HTTP 기반 연결을 사용 하면 인터넷 합니다. hello **아웃 바운드 포트 443 및 80** 이 연결에 대 한 게이트웨이 toomake 열려 있어야 합니다. 열기 **인바운드 포트 8050** 자격 증명 관리자 응용 프로그램에 대 한 (수준이 아닌 회사 방화벽) hello 컴퓨터 수준에만 합니다. Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스를 사용 하는 경우 마찬가지로 원본 / 대상으로 합니다 할 tooopen **1433** 포트도 합니다. 자세한 내용은 [방화벽 구성 및 허용 IP 주소](#firewall-configurations-and-whitelisting-ip-address-of gateway) 섹션을 참조하세요. 

**질문:** 게이트웨이의 인증서 요구 사항은 무엇입니까?
**답변:** 현재 게이트웨이의 데이터 저장소 자격 증명을 안전 하 게 설정 하기 위한 hello 자격 증명 관리자 응용 프로그램에서 사용 하는 인증서가 필요 합니다. 이 인증서는 자체 서명된 인증서를 만들고 hello 게이트웨이 설치 프로그램에서 구성 합니다. 대신 자신의 TLS/SSL 인증서를 사용할 수 있습니다. 자세한 정보는 [클릭 한번 자격 증명 관리자 응용 프로그램](#click-once-credentials-manager-app) 섹션을 참조하세요. 

## <a name="next-steps"></a>다음 단계
복사 활동의 성능에 대한 자세한 내용은 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.

 
