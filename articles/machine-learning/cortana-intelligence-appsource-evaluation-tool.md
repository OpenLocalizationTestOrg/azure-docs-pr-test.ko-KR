---
title: "aaaCortana Intelligence 솔루션 평가 도구 | Microsoft Docs"
description: "Microsoft 파트너는 Cortana Intelligence 솔루션 tooAppSource toofollow toopublish 필요한 모든 hello 단계는 다음과 같습니다."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Cortana Intelligence 솔루션 평가 도구
## <a name="overview"></a>개요
Microsoft 권장 모범 사례 준수에 대 한 hello Cortana Intelligence 솔루션 평가 도구 tooassess 고급 분석 솔루션을 사용할 수 있습니다. Microsoft는 파트너와 기쁘게 생각된 toowork (Isv / SIs) 고객, 대리점 및 구현에 대 한 tooprovide 고품질 솔루션입니다. 이 가이드 솔루션과 hello 솔루션 평가 도구를 사용 하 여 hello 과정을 안내 하 고 hello에 대 한 검사에서 특정 모범 사례에 설명 합니다.

## <a name="getting-started"></a>시작
하십시오 [다운로드](https://aka.ms/aa-evaluation-tool-download) hello Cortana Intelligence 솔루션 평가 도구를 설치 합니다.

필수 조건:
- Windows 10: [Windows 10 공식 사이트](https://www.microsoft.com/en-us/windows)
- Azure Powershell: [Azure PowerShell을 설치 및 구성](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0)합니다.

## <a name="identifying-your-app"></a>앱 식별
설치가 완료 된 후 hello 도구를 열고 첫 번째 평가 시작 합니다.

![평가 도구 열기](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

솔루션에 대한 식별 정보를 제공합니다.

![Azure 구독 연결](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

Tooyour Azure 구독을 연결 하 고 hello 응용 프로그램을 포함 하는 리소스 그룹을 제공 합니다.

![리소스 선택](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

Hello 리소스 그룹이 로드 되 면 솔루션에 포함 된 및로 모든 데이터 리소스의 hello 액세스 가능성을 식별 하는 hello 리소스를 선택 하십시오.
- 수집
- Consumption
- 내부

이 정보는 사용 toobetter 이해 솔루션에서 다양 한 구성 요소를 활용 하는 방법과 tooensure 사용자 용 구성 요소가 모범 사례와 일치 합니다.

### <a name="ingestion"></a>수집
이 경우 수집 외부 hello 솔루션에서 데이터에 사용 되는 toopull 또는 hello 솔루션 외부 서비스를 toopush 데이터를 사용 하는 모든 데이터 원본의 의미 합니다.

### <a name="consumption"></a>Consumption
이 경우 소비는 직접 또는 간접적으로 사용 되는 toopush 데이터 tooend 사용자는 모든 데이터 집합을 의미 합니다. 예:
- PowerBI에서 직접 쿼리에 사용되는 데이터 집합
- WebApp에서 쿼리되는 데이터 집합

>[!NOTE]
특정 리소스가 수집과 소비 둘 다에 사용되는 경우 **소비**를 선택하세요.

### <a name="internal"></a>내부
내부 응용 프로그램 처리에만 사용되는 데이터 리소스의 경우 내부를 사용합니다.

다음으로 hello 이전 단계에서 지정한 모든 데이터베이스에 대 한 유효한 자격 증명된 tooprovide 수 있습니다.

![테스트 필수 조건 설정](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>솔루션 테스트 사례
hello 솔루션 도구는 솔루션에 자동화 된 테스트의 컬렉션을 수행 합니다.

![테스트 실행 설정](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

Hello 테스트 완료 후 됩니다 설명 또는 이유 솔루션 준수 하지 않는 hello 요구 사항에 대 한 근거 tooprovide 라는 메시지가 표시 됩니다.

![비즈니스 근거 제공](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

예를 들어 SQL DW tooAzure를 게시 하는 솔루션을 테스트 해야 하면 tooalso hello 평가 tooAzure Analysis Services를 게시 합니다. 

솔루션이 Azure Analysis Services 대신 SQL Server Analysis Services를 실행하는 IaaS 가상 컴퓨터를 사용할 수도 있습니다. 이 허용 가능한 실패 이유를 hello 테스트의 것입니다.
## <a name="packaging-your-evaluation-results"></a>평가 결과 패키징
Hello 테스트 사례를 완료 한 후 평가 패키지를 내보낸된 tooa zip 파일 되며 묻는 tooprovide 피드백 hello 평가 도구에. 

이 테스트 결과 Microsoft와 추가 승인 toobe을 가져오기 전에 평가 솔루션 toobe 프로그램에 대 한 zip 파일 tooshare 필요한 tooAppSource

![평가 도구에 등급 지정](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

이 섹션 위의 문서 hello 도구의 다양 한 기능에 설명, 형식이이 도구를 평가 하는 모범 사례를 검토해 보겠습니다.

## <a name="security-evaluation-considerations"></a>보안 평가 고려 사항
### <a name="databases-should-use-azure-active-directory-authentication"></a>데이터베이스에서 Azure Active Directory 인증을 사용해야 함
SQL Azure 또는 Azure SQL DW 리소스 hello sloution에 Azure Active Directory (AAD) 인증으로 활성화 되어야 합니다. AAD id 및 역할의 모든 단일 위치 toomanage 제공합니다.

| 항목 | 참조 문서 |
| --- | --- |
| SQL Database 및 SQL Data Warehouse에서의 AAD | [SQL Database 및 SQL Data Warehouse에서 인증을 위해 Azure Active Directory 인증 사용](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| AAD 구성 및 관리 | [SQL Database 또는 SQL Data Warehouse에서의 Azure Active Directory 인증 구성 및 관리](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Azure WebApps 인증 | [Azure 앱 서비스의 인증 및 권한 부여](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| AAD를 사용하여 WebApps 구성 | [어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>데이터 집합 액세스 가능한 tooend 사용자 역할 기반 액세스 제어를 지원 해야
Hello 평가 도구를 실행 하는 동안 됩니다 보고 또는 리소스 게시 toospecify 라는 메시지가 표시 됩니다. 이러한 리소스는 개발자가 아닌 최종 사용자가 액세스하기 위한 것으로 간주됩니다. 이러한 리소스 수 제공 해야 역할 기반 액세스 제어 (RBAC) 순서 tooensure에 최종 사용자가 수 tooaccess만 데이터를 권한이 부여 합니다.

특히 hello Azure 리소스를 다음 중 하나 RBAC로 구성할 수 있습니다 및 허용 가능한 것으로 간주 됩니다.
- 참조 하십시오 HDInsight [도메인에 가입 하는 HDInsight 클러스터를 사용 하는 소개 tooHadoop 보안](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- Azure SQL, [Azure SQL에서의 AAD 인증]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) 참조
- Azure Analysis Services, [Azure Analysis Services에 대한 데이터베이스 역할 및 사용자 관리](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users) 참조
- Azure SQL Data Warehouse(SQL DW는 RBAC를 지원하기 때문에 직접적인 최종 사용자 액세스에는 권장되지 않음)

다른 리소스 종류를 지 원하는 RBAC를 사용 하는 경우에 지정 하십시오 하는 hello 테스트 사례를 근거.

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Azure Data Lake Store에서 미사용 암호화를 사용해야 함
ADLS(Azure Data Lake Store)는 기본적으로 ADLS 관리 암호화 키를 사용하여 미사용 암호화를 지원합니다. Azure Key Vault를 사용하여 암호화를 구성할 수도 있습니다.

ADLS 암호화 설정을 지정하는 방법에 대한 자세한 내용은 [Azure Data Lake Store 계정 만들기](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account)를 참조하세요.

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>Azure SQL 및 Azure SQL Data Warehouse에서 암호화를 사용해야 함
Azure SQL 및 Azure SQL DW는 둘 다 TDE(투명한 데이터 암호화)를 지원합니다. TDE는 데이터와 로그 파일 둘 다의 실시간 암호화 및 암호 해독을 제공합니다.

| 항목 | 참조 문서 |
| --- | --- |
| TDE(투명한 데이터 암호화) | [투명한 데이터 암호화](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| Azure SQL Data Warehouse 및 TDE | [SQL Data Warehouse 암호화 TDE TSQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| TDE를 사용하여 Azure SQL 구성 | [Azure SQL 데이터베이스를 사용한 투명한 데이터 암호화](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| Always Encrypted를 사용하여 Azure SQL 구성 | [SQL Database Always Encrypted Azure Key Vault](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

또한 tooTDE, Azure SQL도 지원 상시 암호화는 데이터가 암호화 되도록 하는 새 데이터 암호화 기술을 뿐만 아니라 나머지에 하 고, 클라이언트와 서버 간에 뿐만 데이터가 하는 동안 이동 하는 동안 hello 서버에서 명령을 실행 하는 동안 사용 중입니다.

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>Azure 마켓플레이스 hello에서 모든 가상 컴퓨터를 배포 해야
순서 tooprovide AppSource 간에 보안의 일관성 수준에에서 Cortana 인텔리전스 솔루션의 일부로 배포 된 가상 컴퓨터 수 인증 하 고 hello Azure Marketplace에 게시 해야 했습니다.

Azure 마켓플레이스 이미지 toosearch hello 현재 목록을 참조 [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute)합니다.

어떻게 toopublish 가상 컴퓨터의 이미지 Azure 마켓플레이스에 대 한 자세한 내용은 참조 [가이드 toocreate hello Azure Marketplace에 대 한 가상 컴퓨터 이미지](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation)합니다.

## <a name="scalability-evaluation-considerations"></a>확장성 평가 고려 사항
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Cortana Intelligence 솔루션에 확장 가능한 빅 데이터 플랫폼이 포함되어야 함
Cortana 인텔리전스 솔루션 toovery 큰 데이터 크기를 조정 해야 합니다. Azure의 hello 두 페타바이트 규모 데이터 플랫폼 중 하나 포함 되어야을 의미 합니다.
- Azure Data Lake Store
- Azure SQL 데이터 웨어하우스

솔루션은 이러한 데이터 크기에 대 한 지원이 필요로 하지 않는 또는 대체 데이터 플랫폼을 사용 하는 경우 하십시오 설명이 hello 테스트 사례를 근거 합니다.
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Cortana Intelligence 솔루션에 전용 수집 데이터 환경이 포함되어야 함
일반적으로 Cortana Intelligence 솔루션은 관계형 데이터 원본에 직접 데이터를 삽입하지 않아야 합니다. 대신, 구조화되지 않은 환경에 원시 데이터를 저장하고 Azure Data Factory를 사용하여 관계형 저장소에 idempotent 삽입/업데이트해야 합니다.

Azure Data Factory를 사용하여 데이터를 복사하는 방법에 대한 자세한 내용은 [자습서: Visual Studio를 사용하여 복사 작업이 있는 파이프라인 만들기](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio)를 참조하세요.

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>Azure SQL Data Warehouse는 데이터 수집에 PolyBase를 사용해야 함
Azure SQL DW는 확장성이 높은 병렬 데이터 수집을 위해 PolyBase를 지원합니다. PolyBase는 Azure Blob 저장소 또는 Azure 데이터 레이크 저장소에 저장 하는 외부 데이터 집합에 대 한 Azure SQL DW tooissue 쿼리를 toouse 있습니다. 대량 업데이트 tooalternative 메서드 뛰어난 성능을 제공이 합니다.

PolyBase 및 Azure SQL DW 시작 방법에 대한 자세한 내용은 [SQL Data Warehouse에서 PolyBase를 사용하여 데이터 로드](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase)를 참조하세요.

PolyBase 및 Azure SQL DW를 사용한 모범 사례에 대한 자세한 내용은 [SQL Data Warehouse에서 PolyBase를 사용하기 위한 가이드](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide)를 참조하세요.

## <a name="availability-evaluation-considerations"></a>가용성 평가 고려 사항

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>데이터 집합 액세스 가능한 tooend 사용자 대량의 동시 사용자를 지원 해야
Hello 평가 도구를 실행 하는 동안 됩니다 보고 또는 리소스 게시 toospecify 라는 메시지가 표시 됩니다. 이러한 리소스는 개발자가 아닌 최종 사용자가 액세스하기 위한 것으로 간주됩니다. 이러한 리소스는 중간-다수의 동시 사용자를 지원해야 합니다.

특히, Azure SQL 데이터 웨어하우스 hello 유일한 데이터 원본 사용 가능한 tooend 사용자 되지 않아야 합니다. 고급 사용자에 대 한 Azure SQL DW 리소스로 제공 하는 경우 사용자가 사용할 수 있는 tootypical Azure Analysis Services 이루어져야 합니다.

Azure SQL DW 동시성 제한에 대한 자세한 내용은 [SQL Data Warehouse의 동시성 및 워크로드 관리](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency)를 참조하세요.

Azure Analysis Services에 대한 자세한 내용은 [Analysis Services 개요](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)를 참조하세요.

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Azure SQL 리소스에 장애 조치(failover)를 위한 읽기 전용 복제본이 있어야 함
Azure SQL 데이터베이스 지리적 복제 tooa 보조 인스턴스를 지원합니다. 이 인스턴스는 장애 조치 인스턴스 tooprovide 고가용성 응용 프로그램으로 사용할 수 있습니다.

Azure SQL Database의 지역에서 복제에 대한 자세한 내용은 [SQL Database 지역 복제 개요](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview)를 참조하세요.

방법에 대 한 Azure sql tooconfigure 지리적 복제 참조 [TRANSACT-SQL와 Azure SQL 데이터베이스에 대 한 활성 지리적 복제 구성](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql)합니다.

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>Azure SQL Data Warehouse에 지역 중복 백업이 사용하도록 설정되어 있어야 함
Azure SQL DW 매일 백업을 toogeo 중복 저장소를 지원합니다. 이 지역에서 복제를 사용 하면 저장 하면 기본 지역의 스냅숏을 액세스할 수 없습니다 없는 경우에도 데이터 웨어하우스 hello를 복원할 수 있습니다. 이 기능은 기본적으로 켜져 있으며 Cortana Intelligence 솔루션에 대해 사용하지 않도록 설정하면 안 됩니다.

Azure SQL DW 백업 및 복원에 대한 자세한 내용은 [SQL Data Warehouse 백업](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups)을 참조하세요.

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>가상 컴퓨터를 가용성 집합으로 구성해야 함
계획 되거나 계획 되지 않은 유지 관리 이벤트의 순서 toominimize hello 영향의 가용성 집합에서 azure 가상 컴퓨터를 구성 해야 합니다.

Azure 가상 컴퓨터 가용성에 대 한 자세한 내용은 참조 [Azure의 Windows 가상 컴퓨터의 가용성을 hello 관리](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability)합니다.

## <a name="other-evaluation-considerations"></a>기타 평가 고려 사항
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Cortana Intelligence 앱은 데이터 오케스트레이션에 중앙 집중식 도구를 사용해야 함
데이터 이동 및 변환을 관리하고 예약하는 데 단일 도구를 사용하면 중요 업무용 데이터에 대한 일관성을 유지할 수 있습니다. 재시도 논리, 종속성 관리, 경고/로깅 등에 대한 명확한 논리를 제공합니다. Hello 사용 좋습니다 [Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) Azure에서 데이터 오케스트레이션에 대 한 합니다.

Azure Data Factory 이외의 도구를 데이터 오케스트레이션에 사용하는 경우 사용 중인 도구를 설명해 주세요.
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>Azure Data Factory를 사용하여 Azure Machine Learning 모델을 다시 학습해야 함
Azure 기계 학습 (AzureML) hello 작성 및 예측 모델링 및 기계 학습 파이프라인의 배포를 위한 쉽게 toouse 도구를 제공 합니다. 이러한 AzureML 모델의 프로덕션 배포는 단일 고정된 데이터 집합을 기반으로 하지 않는 하지만 대신 toohello 실제 현상의 이동에 맞게 변경에 유용 합니다.

AzureML에서 다시 학습 웹 서비스를 만드는 방법에 대한 자세한 내용은 [프로그래밍 방식으로 Machine Learning 모델 다시 학습](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically)을 참조하세요.

Azure 데이터 팩터리를 사용 하 여 hello 모델 학습 프로세스를 자동화 하는 방법에 대 한 자세한 내용은 참조 [업데이트 리소스 작업을 사용 하 여 업데이트 Azure 기계 학습 모델](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity)합니다.

## <a name="existing-documentation"></a>기존 설명서
[Microsoft Azure 인증 toogrow 클라우드 비즈니스](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Cortana Intelligence용 Microsoft Azure Certified](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

