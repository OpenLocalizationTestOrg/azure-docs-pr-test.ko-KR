---
title: "Azure 가상 컴퓨터에서 SQL Server의 aaaOverview | Microsoft Docs"
description: "어떻게 toorun 전체 Azure 가상 컴퓨터에 SQL Server 버전에 알아봅니다. 직접 링크 tooall SQL Server VM 이미지 및 관련된 콘텐츠를 가져옵니다."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Azure Virtual Machines에서 SQL Server 개요
이 항목에서는 Azure 가상 컴퓨터 (Vm)에서 SQL Server를 실행 하기 위한 옵션을 함께 설명 [tooportal 이미지 링크](#option-1-create-a-sql-vm-with-per-minute-licensing) 개요 및 [일반적인 작업](#manage-your-sql-vm)합니다.

> [!NOTE]
> 이미 익숙한 SQL Server 하 고 원하는 toosee toodeploy SQL Server VM을 확인 하려면 어떻게 해야 하는 경우 [hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.
> 
> 

## <a name="overview"></a>개요
데이터베이스 관리자 또는 개발자 인 경우 Azure Vm에 온-프레미스 SQL Server 작업 및 응용 프로그램 toohello 클라우드 방식으로 toomove 제공 합니다. hello 다음 비디오에서는 SQL Server Azure Vm의 기술 개요 합니다.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

비디오 hello hello 다음 영역을 다룹니다.

| Time | 영역 |
| --- | --- |
| 00:21 |Azure VM이란? |
| 01:45 |보안 |
| 02:50 |연결 |
| 03:30 |Storage 안정성 및 성능 |
| 05:20 |VM 크기 |
| 05:54 |고가용성 및 SLA |
| 07:30 |구성 지원 |
| 08:00 |모니터링 |
| 08:32 |데모: SQL Server 2016 VM 만들기 |

> [!NOTE]
> SQL Server 2016을 중점적으로 비디오 hello 하지만 Azure의 SQL Server 2012, 2014 및 2016를 포함 하 여 여러 버전에 대 한 VM 이미지를 제공 합니다. 
> 
> 

## <a name="scenarios"></a>시나리오
Azure에서 데이터 toohost를 선택할 수 있는 방법은 여러 가지가 있습니다. 응용 프로그램은 tooAzure를 이동 하는 경우 성능 tooalso 이동 hello 데이터 향상 됩니다. 하지만 다른 이점도 있습니다. 전역의 존재 여부와 재해 복구에 대 한 액세스 toomultiple 데이터 센터 자동으로 부여 합니다. hello 데이터 매우 보안이 유지 되 고 영 속 이기도합니다.

Azure VM에서 실행하는 SQL Server는 관계형 데이터를 Azure에 저장하기 위한 한 가지 옵션입니다. 여기서는 몇 가지 시나리오를 사용하는 것이 좋습니다. 예를 들어 tooconfigure hello Azure VM을 가능한 tooan 온-프레미스 SQL Server 컴퓨터와 마찬가지로 원하는 수 있습니다. Toorun 추가 응용 프로그램 및 서비스 hello 할 수 있습니다 또는 같은 데이터베이스 서버입니다. 더 많은 시나리오와 고려 사항을 검토 하는 데 도움이 되는 다음과 같은 두 가지 주요 리소스가 있습니다.

* [Azure 가상 컴퓨터에 SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/) Azure Vm에서 SQL Server를 사용 하기 위한 hello 최상의 시나리오의 개요를 제공 합니다. 
* [클라우드 SQL Server 옵션 선택: Azure SQL(PaaS) Database 또는 Azure VM의 SQL Server(IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md)에서는 SQL VM과 SQL Database 간의 자세한 비교를 제공합니다.

## <a name="create-a-new-sql-vm"></a>새 SQL VM 만들기
hello 다음 섹션에서는 Azure 포털의 직접 링크 toohello hello SQL Server 가상 컴퓨터 갤러리 이미지에 대 한 합니다. Hello 이미지 선택에 따라 분 단위로에 SQL Server 라이선스 비용에 대 한 급여 중 하나를 수행할 수 있습니다 또는 (BYOL) 사용자 고유 라이선스를 가져올 수 있습니다.

Hello 자습서에서 새로운 SQL VM을 만들기 위한 단계별 지침을 찾아 [hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다. 또한 hello를 검토 [SQL Server Vm에 대 한 성능 모범 사례](virtual-machines-windows-sql-performance.md), 프로 비전 중 tooselect hello 적절 한 컴퓨터 크기 및 기타 기능이 사용할 수 있는 방법에 대해 설명입니다.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>옵션 1: 분당 라이선스를 사용한 SQL VM 만들기
hello 다음 표에서 hello hello 가상 컴퓨터 갤러리에서 최신 SQL Server 이미지의 행렬. 모든 링크 toobegin 지정 된 버전, 버전 및 운영 체제를 사용 하 여 새 SQL VM 만들기를 클릭 합니다. 

> [!TIP]
> toounderstand hello VM 및 이러한 이미지에 대 한 가격 책정 SQL 참조 [SQL Server Azure Vm에 대 한 지침을 가격](virtual-machines-windows-sql-server-pricing-guidance.md)합니다.

| 버전 | 운영 체제 | 버전 |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

Toothis 목록에서 SQL Server 버전 및 운영 체제의 다른 조합도 사용할 수 있습니다. Hello Azure 포털에서에서 마켓플레이스 검색을 통해 다른 이미지를 찾습니다. 

## <a id="BYOL"></a> 옵션 2: 기존 라이선스를 사용한 SQL VM 만들기
사용자 라이선스가 필요할 수도 있습니다(BYOL). 이 경우에만 SQL Server 라이선스에 대 한 모든 추가 비용이 발생 하지 않고 VM hello에 대 한 지불합니다. toouse 사용자 고유 라이선스를 SQL Server 버전, 버전 및 운영 체제 아래의 hello 매트릭스를 사용 합니다. 이러한 이미지 이름이 접두사로 hello 포털에서 **{BYOL}**합니다.

> [!TIP]
> 사용자 고유의 라이선스를 가져오면 시간에 따른 지속되는 프로덕션 워크로드의 비용을 절약할 수 있습니다. 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.

| 버전 | 운영 체제 | 버전 |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard  BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Toothis 목록에서 SQL Server 버전 및 운영 체제의 다른 조합도 사용할 수 있습니다. Azure 포털 ("SQL Server {BYOL}" 검색) hello에서 마켓플레이스 검색을 통해 다른 이미지를 찾습니다.

> [!IMPORTANT]
> toouse BYOL VM 이미지를와 기업 계약 있어야 [Azure에서 Software Assurance를 통한 라이선스 이동](https://azure.microsoft.com/pricing/license-mobility/)합니다. 또한 유효한 라이선스가 필요 원하는 toouse hello 버전/버전의 SQL Server에 대 한 합니다. 수행 해야 [hello 필요한 BYOL 정보 tooMicrosoft 제공](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) 내 **10** VM을 프로 비전 하는 요일입니다. 

> [!NOTE]
> 가능한 toochange hello 분당 지불 SQL Server VM toouse의 모델 사용자 고유 라이선스를 라이선스는 없습니다. 이 경우 새 BYOL VM 만들고 해야 데이터베이스 toohello 마이그레이션 새 VM입니다. 

## <a name="manage-your-sql-vm"></a>SQL VM 관리
SQL Server VM을 프로비전한 후 여러 가지 선택적 관리 작업이 있습니다. 여러 측면에서 정확하게 온-프레미스 SQL Server 인스턴스를 관리한 대로 SQL Server를 구성 및 관리합니다. 그러나 일부 작업은 특정 tooAzure 됩니다. hello 다음 섹션에서는 강조 표시 링크 toomore 정보로 이러한 영역 중 일부입니다.

### <a name="connect-toohello-vm"></a>Toohello VM 연결
Hello 가장 기본적인 관리 단계 중 하나에 SQL Server Management Studio (SSMS)와 같은 도구를 통해 SQL Server VM tooconnect tooyour입니다. 새 SQL Server VM을 확인 하는 tooconnect tooyour 방법에 대 한 지침은 [tooa Azure에서 SQL Server 가상 컴퓨터를 연결](virtual-machines-windows-sql-connect.md)합니다.

### <a name="migrate-your-data"></a>데이터 마이그레이션
Toomove 좋을 기존 데이터베이스를 설정한 경우 해당 toohello 새로 SQL VM을 프로 비전 합니다. 마이그레이션 옵션 및 지침 목록을 참조 하십시오. [데이터베이스 tooSQL Azure VM에서 서버를 마이그레이션](virtual-machines-windows-migrate-sql.md)합니다.

### <a name="configure-high-availability"></a>고가용성 구성
고가용성이 필요한 경우 SQL Server 가용성 그룹을 구성하는 것이 좋습니다. 여기에는 가상 네트워크의 여러 Azure VM이 포함됩니다. hello Azure 포털에는이 구성을 설정 하는 서식 파일을 있습니다. 자세한 내용은 [Azure Resource Manager 가상 컴퓨터에서 AlwaysOn 가용성 그룹 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요. Toomanually 가용성 그룹과 연결 된 수신기를 구성 하려면 참조 [Azure VM의 AlwaysOn 가용성 그룹 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)합니다.

다른 고가용성 고려 사항은 [Azure Virtual Machines의 SQL Server에 대한 고가용성 및 재해 복구](virtual-machines-windows-sql-high-availability-dr.md)를 참조하세요.

### <a name="back-up-your-data"></a>데이터 백업
Azure Vm을 이용할 수 [자동화 된 백업](virtual-machines-windows-sql-automated-backup.md)는 정기적으로 데이터베이스 tooblob 저장소의 백업을 만듭니다. 수동으로 이 기술을 사용할 수 있습니다. 자세한 내용은 [SQL Server Backup 및 복원에 Azure Storage 사용](virtual-machines-windows-use-storage-sql-server-backup-restore.md)을 참조하세요. 모든 백업 및 복원 옵션에 대한 개요는 [Azure Virtual Machines에서 SQL Server Backup 및 복원](virtual-machines-windows-sql-backup-recovery.md)을 참조하세요.

### <a name="automate-updates"></a>업데이트 자동화
Azure Vm צ ְ ײ [자동화 된 패치 적용](virtual-machines-windows-sql-automated-patching.md) tooschedule 중요 한 windows 및 SQL Server 설치에 대 한 유지 관리 기간을 자동으로 업데이트 합니다.

### <a name="customer-experience-improvement-program-ceip"></a>CEIP(사용자 환경 개선 프로그램)
hello 고객 환경 개선 프로그램 (CEIP)은 기본적으로 사용 됩니다. 이 주기적으로 전송 보고서 tooMicrosoft toohelp SQL Server를 개선 합니다. 관리 작업이 toodisable 사용 하려는 경우가 아니면 CEIP에 필요 없는 것 후 프로 비전 합니다. 사용자 지정 하거나 원격 데스크톱으로 toohello VM을 연결 하 여 hello CEIP를 사용 하지 않도록 설정할 수 있습니다. 그러고 나 서 hello **SQL Server 오류 및 사용 보고** 유틸리티입니다. Hello toodisable 보고 지침을 따릅니다. 

자세한 내용은 참조 hello hello의 CEIP 섹션 [사용 조건 동의](https://msdn.microsoft.com/library/ms143343.aspx) 항목입니다. 

## <a name="next-steps"></a>다음 단계

가격에 대 한 질문에 대 한 참조 [SQL Server Azure Vm에 대 한 지침을 가격](virtual-machines-windows-sql-server-pricing-guidance.md) 및 hello [Azure 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)합니다. Hello에서 SQL Server의 대상 버전을 선택 **OS/소프트웨어** 목록입니다. 그런 다음 다양 한 크기의 가상 컴퓨터에 대 한 hello 가격을 봅니다.

추가 질문이 있나요? 먼저 hello 참조 [Azure 가상 컴퓨터 FAQ에서 SQL Server](virtual-machines-windows-sql-server-iaas-faq.md)합니다. 하지만 Microsoft 및 hello 커뮤니티와 모든 SQL VM 항목 toointeract에 질문이 나 의견 toohello 아래쪽을 추가 합니다.
