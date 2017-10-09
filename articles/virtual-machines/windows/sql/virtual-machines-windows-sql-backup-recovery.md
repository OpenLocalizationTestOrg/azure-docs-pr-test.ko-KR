---
title: "aaaBackup 및 SQL Server에 대 한 복원 | Microsoft Docs"
description: "Azure 가상 컴퓨터에서 실행되는 SQL Server 데이터베이스의 백업 및 복원 시 고려 사항에 대해 설명합니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Azure 가상 컴퓨터에서 SQL Server의 백업 및 복원
## <a name="overview"></a>개요
Azure 저장소에 데이터 손실이 나 물리 데이터 손상을 대 한 모든 Azure VM 디스크 tooguarantee 보호 복사본을 3 개 유지 관리합니다. 따라서 온-프레미스에서와 달리이 대 한 tooworry가 필요 하지 않습니다. 그러나 여전히 응용 프로그램 또는 사용자 오류 (예: 잘못 된 데이터를 삽입 하거나 테이블 삭제)에 대 한 SQL Server 데이터베이스 tooprotect 프로그램을 백업 해야 하며 수 toorestore 되 고 tooa 지정 시간.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Azure Vm에서 실행 되는 SQL server에 네이티브 백업을 사용할 수 있으며 복원 기술 hello 백업 파일의 hello 대상에 대 한 연결 된 디스크를 사용 하 여 키를 누릅니다. 그러나는 hello에 따라 tooan Azure 가상 컴퓨터를 연결할 수 있는 디스크 수는 제한 toohello [hello 가상 컴퓨터의 크기가](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 디스크 관리 tooconsider hello 오버 헤드가 이기도합니다.

SQL Server 2014부터, 백업 및 tooMicrosoft Azure Blob 저장소를 복원할 수 있습니다. 또한 SQL Server 2016은 이 옵션에 대한 향상된 기능을 제공합니다. 또한 Microsoft Azure Blob 저장소에 저장된 데이터베이스 파일의 경우, SQL Server 2016은 Azure 스냅숏을 사용하여 거의 즉시 백업하고 신속하게 복원하는 옵션을 제공합니다. 이 문서에서는 이러한 옵션에 대한 개요를 제공하며 자세한 내용은 [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](https://msdn.microsoft.com/library/jj919148.aspx)에서 확인할 수 있습니다.

> [!NOTE]
> 매우 큰 데이터베이스를 백업에 대 한 hello 옵션의 논의 알려면 [멀티 테라바이트 SQL Server 데이터베이스 백업 전략에 대 한 Azure 가상 컴퓨터](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx)합니다.
> 
> 

아래 섹션에서는 hello 정보는 Azure 가상 컴퓨터에서 지원 되는 SQL Server의 특정 toohello 서로 다른 버전을 포함 합니다.

## <a name="sql-server-virtual-machines"></a>SQL Server 가상 컴퓨터
Azure 가상 컴퓨터에 SQL Server 인스턴스가 실행 중이면, 데이터베이스 파일이 Azure의 데이터 디스크에 이미 상주합니다. 이 디스크는 Azure Blob 저장소에 있습니다. 따라서 hello 이유 백업 데이터베이스 및 hello 방법에 대 한 약간 변경을 수행 합니다. Hello 다음 사항을 고려 합니다. 

* Microsoft Azure hello Microsoft Azure 서비스의 일부로이 보호를 제공 하기 때문에 하드웨어 또는 미디어 오류 로부터 데이터베이스 백업을 tooprovide 보호 tooperform 더 이상 필요 합니다.
* 그러나 사용자 오류 로부터 또는 보관 목적으로, 규정 상의 이유 또는 관리 목적으로 tooperform 데이터베이스 백업을 tooprovide 보호를 보내야합니다.
* Azure에서 직접 hello 백업 파일을 저장할 수 있습니다. 자세한 내용은 hello 다음 서로 다른 버전의 SQL Server hello에 대 한 지침을 제공 하는 섹션을 참조 하세요.

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016은 SQL Server 2014의 [Azure Blob를 사용한 백업 및 복원](https://msdn.microsoft.com/library/jj919148.aspx) 기능을 지원합니다. 하지만 향상 된 기능을 수행 하는 hello도 포함 됩니다.

| 2016의 향상된 기능 | 세부 정보 |
| --- | --- |
| **스트라이프** |TooMicrosoft Azure blob 저장소를 백업할 때 SQL Server 2016 원하는 toomultiple blob tooenable tooa 최대 12.8 t B를 큰 데이터베이스를 백업 합니다. |
| **스냅숏 백업** |Hello Azure 스냅숏 사용을 통해 SQL Server 파일-스냅숏 백업을 거의 즉시 백업 및 hello Azure Blob 저장소 서비스를 사용 하 여 저장 된 데이터베이스 파일에 대 한 신속한 복원을 제공 합니다. 이 기능을 사용 하면 toosimplify 하면 백업 및 복원 정책을 합니다. 또한 파일-스냅숏 백업 기능은 특정 시점 복원도 지원합니다. 자세한 내용은 [Azure에서 데이터베이스 파일에 대한 스냅숏 백업](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx)을 참조하세요. |
| **Managed Backup 일정** |이제 SQL Server Managed Backup tooAzure 사용자 지정 일정을 지원합니다. 자세한 내용은 참조 [SQL Server Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx)합니다. |

Azure Blob 저장소를 사용 하는 경우 SQL Server 2016의 hello 기능의 자습서를 참조 하십시오. [자습서: SQL Server 2016 데이터베이스와 함께 hello Microsoft Azure Blob 저장소 서비스를 사용 하 여](https://msdn.microsoft.com/library/dn466438.aspx)합니다.

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014의 향상 된 기능을 수행 하는 hello를 포함 되어 있습니다.

1. **백업 및 복원 tooAzure**:
   
   * *SQL Server 백업 tooURL* SQL Server Management Studio에서 지원 되었습니다. SQL Server Management studio에서 백업 또는 복원 작업 또는 유지 관리 계획 마법사를 사용 하 여 hello 옵션 tooback tooAzure 출시 되었습니다. 자세한 내용은 참조 [SQL Server 백업 tooURL](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx)합니다.
   * *SQL Server Managed Backup tooAzure* 새 기능을 자동화 된 백업 관리를 사용할 수 있습니다. 이 기능은 Azure 컴퓨터에서 실행되는 SQL Server 2014 인스턴스에 대한 백업 관리를 자동화하는 데 특히 유용합니다. 자세한 내용은 참조 [SQL Server Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx)합니다.
   * *백업 자동화* 추가 자동화 tooautomatically 사용 제공 *SQL Server Managed Backup tooAzure* Azure에서 SQL Server VM에 대 한 모든 기존 및 새 데이터베이스에 있습니다. 자세한 내용은 [Azure Virtual Machines에서 SQL Server에 대한 자동화된 Backup](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.
   * SQL Server 2014 백업 tooAzure에 대 한 모든 hello 옵션의 개요를 참조 하십시오. [SQL Server 백업 및 Microsoft Azure Blob 저장소 서비스로 복원](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx)합니다.
2. **암호화**: SQL Server 2014는 백업을 만들 때 데이터를 암호화하는 기능을 지원합니다. 인증서 나 비대칭 키 osf 사용 하는 hello와 몇 가지 암호화 알고리즘이 지원. 자세한 내용은 [백업 암호화](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx)를 참조하세요.

## <a name="sql-server-2012"></a>SQL Server 2012
SQL Server 2012에서 SQL Server 백업 및 복원에 대한 자세한 내용은 [SQL Server 데이터베이스 백업 및 복원(SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx)을 참조하세요.

SQL Server 2012 SP1 누적 업데이트 2 부터는 hello Azure Blob 저장소 서비스에서에서 tooand 복원을 백업할 수 있습니다. 이 기능은 온-프레미스 인스턴스 또는 Azure 가상 컴퓨터에서 실행 중인 SQL Server에서 SQL Server 데이터베이스를 사용 하는 tooback 될 수 있습니다. 자세한 내용은 [Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx)을 참조하세요.

Hello Azure Blob 저장소 서비스를 사용 하 여 hello 이점 hello 기능 toobypass hello 16 디스크 제한을 포함 연결 된 디스크에 대 한 관리 용이성, hello hello 백업 파일 tooanother 인스턴스는 Azure에서 실행 되는 SQL Server 인스턴스의 직접적인 가용성 가상 컴퓨터 또는 마이그레이션 또는 재해 복구 목적의 온-프레미스 인스턴스를 제공 합니다. 이점 toousing SQL Server 백업에 대 한 Azure blob 저장소 서비스의 전체 목록을 참조 hello *혜택* 섹션 [SQL Server 백업 및 Azure Blob 저장소 서비스로 복원](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx)합니다.

권장 모범 사례 및 문제 해결 정보에 대해서는 [백업 및 복원 모범 사례(Azure Blob 저장소 서비스)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx)를 참조하세요.

## <a name="sql-server-2008"></a>SQL Server 2008
SQL Server 2008 R2에서 SQL Server 백업 및 복원에 대해서는 [SQL Server에서 데이터베이스 백업 및 복원(SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx)을 참조하세요.

SQL Server 2008에서 SQL Server 백업 및 복원에 대해서는 [SQL Server에서 데이터베이스 백업 및 복원(SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx)을 참조하세요.

## <a name="next-steps"></a>다음 단계
Azure VM에서 SQL Server의 배포를 계획 하는 경우 hello 자습서에서 프로비저닝 지침을 찾을 수 있습니다: [Azure 리소스 관리자와 Azure에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.

하지만 백업 및 복원는 잠재적으로 보다 쉽게 데이터 마이그레이션 경로 tooSQL Azure VM에서 서버, 데이터 사용된 toomigrate를 될 수 있습니다. 마이그레이션 옵션 및 권장 사항에 대 한 자세한 내용은 참조 하십시오. [데이터베이스 tooSQL Azure VM에서 서버를 마이그레이션](virtual-machines-windows-migrate-sql.md)합니다.

그 밖에 [Azure Virtual Machines에서 SQL Server 실행과 관련된 리소스](virtual-machines-windows-sql-server-iaas-overview.md)를 검토하세요.

