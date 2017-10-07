---
title: "SQL Server 백업 및 복원에 대 한 Azure 저장소 aaaHow toouse | Microsoft Docs"
description: "자세한 방법을 tooback SQL Server tooAzure 저장소를 구성 합니다. SQL 데이터베이스 tooAzure 저장소를 백업 hello 이점에 설명 합니다."
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>SQL Server 백업 및 복원에 Azure 저장소 사용
## <a name="overview"></a>개요
SQL Server 2012 SP1 CU2 이상에서는 작성할 수 있습니다 이제 SQL Server 백업을 직접 toohello Azure Blob 저장소 서비스. 온-프레미스 SQL Server 데이터베이스 또는 Azure 가상 컴퓨터에서 SQL Server 데이터베이스와이 기능 tooback tooand 복원을 hello Azure Blob 서비스에서 사용할 수 있습니다. 백업 toocloud hello 클라우드에서 가용성, 무제한 지리적 복제 오프 사이트 저장소 및 데이터 tooand 마이그레이션의의 용이성의 이점을 제공합니다. Transact-SQL 또는 SMO를 사용하여 BACKUP 또는 RESTORE 문을 실행할 수 있습니다.

SQL Server 2016에서는 새로운 기능입니다. 사용할 수 있습니다 [파일-스냅숏 백업](http://msdn.microsoft.com/library/mt169363.aspx) tooperform 거의 즉시 백업 하 고 매우 빠른 복원 합니다.

이 항목에서는 toouse SQL 백업에 대 한 Azure 저장소를 선택할 수 있습니다 하 고 다음 관련 된 hello 구성 요소를 설명 하는 이유를 설명 합니다. Hello 문서 tooaccess 연습 및 SQL Server 백업을 사용 하 여이 서비스를 사용 하 여 추가 정보 toostart hello 끝에서 제공 하는 hello 리소스를 사용할 수 있습니다.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>사용 하 여 hello SQL Server 백업을 위해 Azure Blob 서비스의 이점
SQL Server를 백업할 때 발생하는 몇 가지 해결 과제는 다음과 같습니다. 이러한 과제 저장소 관리, 저장소 오류의 위험, toooff 사이트 저장소 및 하드웨어 구성에 액세스 합니다. 대부분의 이러한 문제는 SQL Server 백업에 대 한 hello Azure Blob 저장소 서비스를 사용 하 여 주소가 지정 됩니다. 다음 이점을 hello를 고려 합니다.

* **사용 편의성**: Azure blob에 백업을 저장할 편리한 유연 하며 쉽게 tooaccess 오프 사이트 옵션 일 수 있습니다. SQL Server 백업은 기존 수정 하는 것 만큼 쉽게 수에 대 한 오프 사이트 저장소를 만드는 스크립트/작업 toouse hello **백업 tooURL** 구문입니다. 오프 사이트 저장소는 대개 있어야 hello 프로덕션 데이터베이스 위치 tooprevent 로부터 충분히 멀리 줄 hello 오프 사이트 및 프로덕션 데이터베이스 위치 모두에 영향을 줄 수 있는 재해 합니다. 너무 선택 하 여[지역 간 복제 Azure blob](../../../storage/common/storage-redundancy.md), hello 전체 지역에 영향을 줄 수 있는 재해의 hello 이벤트에는 추가 보호 계층을 해야 합니다.
* **백업 보관**: hello Azure Blob 저장소 서비스는 옵션 tooarchive 백업을 더 자주 사용 되는 대체 toohello 테이프를 제공 합니다. 테이프 저장소 물리적 이동과 tooan 오프 사이트 시설 및 측정값 tooprotect hello 미디어 필요할 수 있습니다. Azure Blob 저장소에 백업 저장은 즉각적이고 내구성 있는 고가용성 보관 옵션을 제공합니다.
* **관리되는 하드웨어**: Azure 서비스를 사용하면 하드웨어 관리의 오버헤드가 없습니다. Azure 서비스는 hello 하드웨어를 관리 하며 하드웨어 오류에 대비한 중복과 보호에 대 한 지리적 복제를 제공 합니다.
* **무제한 저장소**: 액세스 toovirtually 있는 직접 백업 tooAzure blob를 활성화 하 여 무제한 저장 합니다. 또는 tooan Azure 가상 컴퓨터 디스크를 백업에서 컴퓨터 크기에 따라 제한도 있습니다. 제한 toohello 수가 디스크의 tooan 백업에 대 한 Azure 가상 컴퓨터를 연결할 수 있습니다. 매우 큰 인스턴스의 경우 16개의 디스크로 제한되고 작은 인스턴스의 경우에는 디스크의 수가 더 적습니다.
* **가용성 백업**: Azure blob에 저장 된 백업 언제 든 지 고 어디에서 나 사용할 수 있고 쉽게 수 hello 필요 없이 온-프레미스 SQL Server 또는 Azure 가상 컴퓨터는 실행 중인 다른 SQL Server 복원 tooeither에 대 한 액세스 데이터베이스 연결/분리 또는 다운로드 하 고 연결에 대 한 VHD를 hello 합니다.
* **비용**: hello 사용 되는 서비스에 대해서만 비용을 지불 합니다. 오프사이트 및 백업 보관 옵션으로 비용 효율성을 추구할 수 있습니다. Hello 참조 [Azure 가격 계산기](http://go.microsoft.com/fwlink/?LinkId=277060 "가격 계산기"), 및 hello [Azure 가격 문서](http://go.microsoft.com/fwlink/?LinkId=277059 "가격 책정 문서") 더 정보입니다.
* **Storage 스냅숏을**: 데이터베이스 파일은 Azure blob에 저장 하 고 SQL Server 2016을 사용 하는 경우 사용할 수 있습니다 [파일-스냅숏 백업](http://msdn.microsoft.com/library/mt169363.aspx) tooperform 거의 즉시 백업 하 고 매우 빠른 복원 합니다.

자세한 내용은 [Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](http://go.microsoft.com/fwlink/?LinkId=271617)을 참조하십시오.

다음 두 섹션 hello hello 필요한 SQL Server 구성 요소를 포함 하 여 hello Azure Blob 저장소 서비스를 소개 합니다. 중요 한 toounderstand hello 구성 요소 및 상호 작용 toosuccessfully 백업 및 복원 hello Azure Blob 저장소 서비스에서 않습니다.

## <a name="azure-blob-storage-service-components"></a>Azure Blob 저장소 서비스 구성 요소
hello 다음 Azure 구성 요소는 사용 toohello Azure Blob 저장소 서비스로 백업할 때.

| 구성 요소 | 설명 |
| --- | --- |
| **저장소 계정** |hello 저장소 계정은 모든 저장소 서비스의 시작 지점 hello입니다. tooaccess는 Azure Blob 저장소 서비스에는 먼저 Azure 저장소 계정을 만듭니다. Azure Blob 저장소 서비스에 대 한 자세한 내용은 참조 [어떻게 toouse hello Azure Blob 저장소 서비스](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **컨테이너** |컨테이너는 Blob 집합의 그룹화를 제공하며 Blob을 개수에 제한 없이 저장할 수 있습니다. Azure Blob 서비스는 SQL Server 백업 tooan toowrite 있어야 이상 hello 루트 컨테이너가 만들어져 있습니다. |
| **Blob** |임의 형식 및 크기의 파일입니다. Blob이 URL 형식에 따라 hello를 사용 하 여 주소 지정 가능한: **https://[storage account].blob.core.windows.net/[container]/[blob]**합니다. 페이지 Blob에 대한 자세한 내용은 [블록 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요. |

## <a name="sql-server-components"></a>SQL Server 구성 요소
hello 다음 SQL Server 구성 요소는 사용 toohello Azure Blob 저장소 서비스로 백업할 때.

| 구성 요소 | 설명 |
| --- | --- |
| **URL** |URL은 식별자 URI (Uniform Resource) tooa 고유한 백업 파일을 지정 합니다. hello URL hello SQL Server 백업 파일의 사용 되는 tooprovide hello 위치와 이름을입니다. hello URL은 컨테이너가 아닌 tooan 실제 blob을 가리키도록 해야 합니다. Hello blob가 없는 경우 자동으로 만들어집니다. 기존 blob 지정 되 면 백업이 실패 하지 않는 한 hello > WITH FORMAT 옵션을 지정 합니다. hello 다음은 hello BACKUP 명령에서에서 지정 하는 hello URL의 예: **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**합니다. HTTPS는 필수가 아니지만 사용하는 것이 좋습니다. |
| **자격 증명** |자격 증명으로 필요한 tooconnect tooAzure Blob 저장소 서비스를 인증 하는 hello 정보가 저장 됩니다.  SQL Server toowrite 백업 tooan Azure Blob 또는 복원 하기 위해 SQL Server 자격 증명을 만들어야 합니다. 자세한 내용은 [SQL Server 자격 증명](https://msdn.microsoft.com/library/ms189522.aspx)을 참조하세요. |

> [!NOTE]
> Toocopy를 선택 하 고 백업 파일 toohello Azure Blob 저장소 서비스로 업로드 경우 계획인 경우 toouse 복원 작업을 위해이 파일은 페이지 blob 유형 저장소 옵션으로 사용 해야 합니다. 블록 Blob 유형에서 RESTORE를 사용하면 오류를 일으키며 실패합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
1. 아직 Azure 계정이 없는 경우 새로 하나 만듭니다. Azure를 평가 하는 경우 고려 hello [무료 평가판](https://azure.microsoft.com/free/)합니다.
2. 복원을 수행 하 고 저장소 계정을 만들 수 있도록 안내 하는 자습서를 따라 hello 중 하나를 통해 이동 합니다.
   
   * **SQL Server 2014**: [자습서: SQL Server 2014 백업 및 Azure Blob 저장소 서비스로 복원 tooMicrosoft](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx)합니다.
   * **SQL Server 2016**: [자습서: SQL Server 2016 데이터베이스와 함께 hello Microsoft Azure Blob 저장소 서비스 사용](https://msdn.microsoft.com/library/dn466438.aspx)
3. [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](https://msdn.microsoft.com/library/jj919148.aspx)부터 시작해서 추가 설명서를 검토하세요.

문제가 있는 경우 hello 항목을 검토 [SQL Server 백업 tooURL Best Practices and Troubleshooting](https://msdn.microsoft.com/library/jj919149.aspx)합니다.

기타 SQL Server 백업 및 복원 옵션에 대해서는 [Azure Virtual Machines에서 SQL Server 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)을 참조하세요.

