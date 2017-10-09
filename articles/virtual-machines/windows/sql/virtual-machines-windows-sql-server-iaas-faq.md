---
title: "서버에 Azure 가상 컴퓨터 FAQ aaaSQL | Microsoft Docs"
description: "이 문서에서는 답변 toofrequently Azure Vm에서 SQL Server를 실행 하는 방법에 대 한 질문과 대답입니다."
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Azure Virtual Machines의 SQL Server에 대한 FAQ(질문과 대답)
이 항목에서는 실행에 대 한 일반적인 질문과 대답 toosome의 hello 제공 [Azure 가상 컴퓨터에 SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/)합니다.

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>질문과 대답

1. **SQL Server를 사용하여 Azure 가상 컴퓨터를 만들려면 어떻게 해야 합니까?**

    hello 가장 쉬운 방법은 toocreate SQL Server를 포함 하는 가상 컴퓨터입니다. Azure에 등록 하 고 hello 포털에서 SQL VM 만들기에 대 한 자습서를 참조 하십시오. [hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다. 분 당 사용량 기준 과금 SQL Server 라이선스를 사용 하는 가상 컴퓨터 이미지를 선택할 수 있습니다 또는 사용자 고유의 SQL Server 라이선스 toobring 수 있는 이미지를 사용할 수 있습니다. Hello 옵션을 수동으로 VM에서 SQL Server를 설치 하 고 온-프레미스 라이선스를 다시 사용 해야 합니다. 사용자 라이선스가 필요하면 [Azure에서 Software Assurance를 통한 라이선스 이동](https://azure.microsoft.com/pricing/license-mobility/)이 가능해야 합니다. 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.

1. **SQL Vm과 hello SQL 데이터베이스 서비스 간의 hello 차이점은 무엇입니까?**

    개념적으로 Azure 가상 컴퓨터에서 SQL Server를 실행하는 것은 원격 데이터 센터에 SQL Server를 실행하는 것과 크게 다르지 않습니다. 반면, [SQL 데이터베이스](../../../sql-database/sql-database-technical-overview.md) 는 DaaS(Database-as-a-Service)를 제공합니다. SQL 데이터베이스에 없는 데이터베이스를 호스팅하는 액세스 toohello 컴퓨터. 전체 비교를 보려면 [클라우드 SQL Server 옵션 선택: Azure SQL(PaaS) 데이터베이스 또는 Azure VM의 SQL Server(IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md)를 참조하세요.

1. **내 온-프레미스 SQL Server 데이터베이스 toohello 클라우드는 어떻게 마이그레이션할 수 있습니까?**

    가장 먼저 SQL Server 인스턴스를 사용하여 Azure 가상 컴퓨터를 만듭니다. 다음 온-프레미스 데이터베이스 toothat 인스턴스를 마이그레이션하십시오. 데이터 마이그레이션 전략에 대 한 참조 [SQL Server 데이터베이스 tooSQL Azure VM에서 서버를 마이그레이션하려면](virtual-machines-windows-migrate-sql.md)합니다.

1. **Hello에 SQL Server의 두 번째 인스턴스를 설치할 수 있는 동일한 VM? Hello 기본 인스턴스에 설치 된 기능을 변경할 수 있나요?**

    예. SQL Server 설치 미디어 hello hello에 폴더에 있는 **C** 드라이브입니다. 실행 **Setup.exe** 에서 해당 위치 tooadd 새 SQL Server 인스턴스 또는 hello 컴퓨터에서 SQL Server의 toochange 다른 설치 된 기능입니다. 자동화 된 백업, 자동화 된 패치 적용 및 Azure 키 자격 증명 모음 통합 같은 일부 기능은 hello 기본 인스턴스에 대해 작동 하는 참고 합니다.

1. **SQL Server의 hello 기본 인스턴스를 제거할 수 있나요?**

    예. 그러나 몇 가지 고려 사항이 있습니다. Hello 이전 응답, hello를 사용 하는 기능에에서 명시 된 대로 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md) hello 기본 인스턴스에서 에서만 작동 합니다. Hello 기본 인스턴스를 제거 하는 경우 hello에 대 한 toolook 계속 확장과 이벤트 로그 오류를 생성할 수 있습니다. 이러한 오류는 hello 두 개의 원본에서: **Microsoft SQL Server 자격 증명 관리** 및 **Microsoft SQL Server IaaS 에이전트**합니다. Hello 오류 중 하나가 비슷한 toohello 다음 수 있습니다.
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    Toouninstall hello 기본 인스턴스를 결정 했으면 hello 제거 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md) 도 합니다.

1. **Tooa 새 버전/버전의 hello Azure VM에서 SQL Server를 업그레이드 하려면 어떻게 해야 합니까?**

    현재는 Azure VM에서 실행 중인 SQL Server를 전체 업그레이드할 수 없습니다. Edition/hello 필요한 SQL Server 버전에서는 새 Azure 가상 컴퓨터를 만들고 다음 표준을 사용 하 여 데이터베이스 toohello 새 서버를 마이그레이션할 [데이터 마이그레이션 방법](virtual-machines-windows-migrate-sql.md)합니다.

1. **Azure VM에 라이선스가 있는 내 SQL Server 사본을 설치하려면 어떻게 해야 합니까?**

    있는 경우 두 가지 방법으로 toodo이 Hello 중 하나를 프로 비전 할 수 [라이선스를 지 원하는 가상 컴퓨터 이미지](virtual-machines-windows-sql-server-iaas-overview.md#BYOL)합니다. 또 다른 옵션 toocopy hello SQL Server 설치 미디어 tooa Windows Server VM을 이며 hello VM에 SQL Server를 설치 합니다. 라이선싱의 이유로 [Azure에서 Software Assurance를 통한 라이선스 이동](https://azure.microsoft.com/pricing/license-mobility/)이 가능해야 합니다. 자세한 내용은 [SQL Server Azure VM에 대한 가격 책정 지침](virtual-machines-windows-sql-server-pricing-guidance.md)을 참조하세요.

1. **변경할 수는 VM toouse 나만의 SQL Server 라이선스 hello 종 량 제 갤러리 이미지 중 하나에서 만들어진 경우?**

    아니요. 사용자 고유 라이선스에서 분당 지불 라이선스 toousing 전환 되지 있습니다. Hello 중 하나를 사용 하 여 새 Azure 가상 컴퓨터를 만들 [BYOL 이미지](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), 다음 표준을 사용 하 여 데이터베이스 toohello 새 서버를 마이그레이션할 [데이터 마이그레이션 방법](virtual-machines-windows-migrate-sql.md)합니다.

1. **SQL Server FCI(장애 조치 클러스터 인스턴스)는 Azure VM에서 지원되나요?**

   예. 있습니다 수 [Windows Server 2016에서 Windows 장애 조치 클러스터를 만듭니다](virtual-machines-windows-portal-sql-create-failover-cluster.md) hello 클러스터 저장소에 대 한 저장소 공간 다이렉트 (S2D)를 사용 합니다. 또는 [Azure Virtual Machines에서 SQL Server에 대한 고가용성 및 재해 복구](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions)에 설명된 대로 타사 클러스터링 또는 저장소 솔루션을 사용할 수 있습니다.

1. **대기 모드/장애 조치만 사용 중인 경우 Azure VM에서 SQL Server toopay toolicense 있습니까?**

    Toopay toolicense 하나의 SQL Server로 참여 HA 배포에서 수동 보조 복제본 Software assurance에 설명 된 대로 라이선스 이동성을 사용 하는 경우 없는 [가상 컴퓨터 라이선스 FAQ](http://azure.microsoft.com/pricing/licensing-faq/)합니다.

1. **업데이트와 서비스 팩은 SQL Server VM에 어떻게 적용됩니까?**

    가상 컴퓨터 제어할 수 있습니다 시기 및 업데이트를 적용 하는 방법을 포함 하 여 hello 호스트 컴퓨터. Hello 운영 체제에 수동으로 windows 업데이트를 적용 하려면 또는 라는 예약 서비스를 사용 하도록 설정할 수 [자동화 된 패치 적용](virtual-machines-windows-sql-automated-patching.md)합니다. 자동 패칭은 해당 범주의 SQL Server 업데이트를 포함하여 중요함으로 표시된 업데이트를 설치합니다. 서버를 수동으로 설치 해야 다른 선택적 업데이트 tooSQL 합니다.

1. **구성 (예: Windows 2008 R2 예제 + SQL Server 2012) hello 가상 컴퓨터 갤러리에 표시 되지 않은 구성 가능한 tooset 입니까?**

    아니요. SQL Server를 포함 하는 가상 컴퓨터 갤러리 이미지에 대 한 hello 제공 하는 이미지 중 하나를 선택 해야 합니다.

1. **Azure VM에 SQL Data Tools를 설치하려면 어떻게 해야 합니까?**

     Hello SQL 데이터 도구에서 다운로드 및 설치 [Microsoft SQL Server Data Tools-Visual Studio 2013 용 Business Intelligence](https://www.microsoft.com/en-us/download/details.aspx?id=42313)합니다.

## <a name="resources"></a>리소스

Azure 가상 컴퓨터에서 SQL Server의 개요를 hello 비디오를 시청 [Azure VM은 SQL Server 2016 용 hello 기능이 뛰어난](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)합니다. Hello 항목에 대 한 얻을 수 있습니다 [SQL Server에 대 한 Azure 가상 컴퓨터 개요](virtual-machines-windows-sql-server-iaas-overview.md)합니다.

기타 리소스는 다음과 같습니다.

* [Hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)
* [데이터베이스 tooSQL Azure VM에서 서버 마이그레이션](virtual-machines-windows-migrate-sql.md)
* [Azure Virtual Machines의 SQL Server에 대한 고가용성 및 재해 복구](virtual-machines-windows-sql-high-availability-dr.md)
* [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)
* [Azure Virtual Machines의 SQL Server에 대한 응용 프로그램 패턴 및 개발 전략](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 