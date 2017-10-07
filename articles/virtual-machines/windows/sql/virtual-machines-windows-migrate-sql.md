---
title: "SQL Server 데이터베이스 tooSQL VM에 서버 aaaMigrate | Microsoft Docs"
description: "온-프레미스 사용자 toomigrate tooSQL 서버는 Azure 가상 컴퓨터에서 데이터베이스 하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>SQL Server 데이터베이스 tooSQL Azure VM에서 서버 마이그레이션

온-프레미스 SQL Server 사용자 데이터베이스 tooSQL Azure VM에서 서버는 다양 한 메서드 toomigrate 합니다. 이 문서는 간략하게 다양 한 방법에 설명 하 고 hello 다양 한 시나리오에 대 한 최상의 방법을 권장 합니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Hello 기본 마이그레이션 방법
hello 기본 마이그레이션 방법은 다음과 같습니다.

* 압축을 직접 복사 hello에 대 한 백업 파일을 사용 하 여 hello Azure 가상 컴퓨터에 온-프레미스 백업 수행
* 백업 tooURL 수행 하 고 hello hello URL에서 Azure 가상 컴퓨터에 복원
* 분리 hello 데이터 및 로그 파일 tooAzure blob 저장소를 복사 하 고 URL에서 tooSQL Azure VM의 서버 연결
* 온-프레미스 물리적 변환 tooHyper-V VHD 컴퓨터 tooAzure Blob 저장소에 업로드 한 다음 VHD를 업로드 사용 하 여 새 VM 배포
* Windows 가져오기/내보내기 서비스를 사용하여 하드 드라이브 제공
* 있는 경우 AlwaysOn 배포는 온-프레미스, hello를 사용 하 여 [Azure 복제본 추가 마법사](../classic/sql-onprem-availability.md) toocreate Azure와 사용자가 toohello Azure 데이터베이스 인스턴스를 가리키는 장애 조치의 복제본
* SQL Server를 사용 하 여 [트랜잭션 복제](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server 구독자 인스턴스 선택한 다음 사용자가 toohello Azure 데이터베이스 인스턴스를 가리키는 복제를 사용 하지 않도록 설정

> [!TIP]
> Azure의 SQL Server Vm 간에 이러한 동일한 기술을 toomove 데이터베이스를 사용할 수 있습니다. 예를 들어, 없습니다 지원 되는 방법 tooupgrade 하나의 버전/버전 tooanother에서 SQL Server 갤러리 이미지 VM입니다. 이 경우 새 SQL Server VM edition/hello 새 버전에서는 만들고 사용 하 여 hello 마이그레이션 방법 중 하나에서이 문서 toomove 데이터베이스. 

## <a name="choosing-your-migration-method"></a>마이그레이션 메서드 선택
최적의 데이터 전송 성능에 대 한 hello 압축 된 백업 파일을 사용 하 여 Azure VM에 hello 데이터베이스 파일을 마이그레이션하십시오.

toominimize hello 데이터베이스 마이그레이션 프로세스 중에 가동 중지 시간 hello AlwaysOn 옵션이 나 hello 트랜잭션 복제 옵션을 사용 합니다.

가능한 toouse hello 메서드 위에 없는 경우 수동으로 데이터베이스를 마이그레이션하십시오. 이 방법을 사용 하면 일반적으로 시작 hello 데이터베이스 백업의 복사본 다음 Azure를 데이터베이스 백업으로 되며 다음 데이터베이스 복원을 수행 합니다. Azure에 hello 데이터베이스 파일 자체를 복사한 다음 첨부할 수도 있습니다. 데이터베이스를 Azure VM에 수동으로 마이그레이션하는 프로세스를 수행하는 몇 가지 방법이 있습니다.

> [!NOTE]
> 이전 버전의 SQL Server에서 tooSQL Server 2014 또는 SQL Server 2016으로 업그레이드 하면 변경 내용이 필요한 지를 고려해 야 합니다. 마이그레이션 프로젝트의 일부로 hello 새 버전의 SQL Server에서 지원 되지 않는 기능에 대 한 모든 종속성을 해결 하는 것이 좋습니다. Hello 지원 되는 버전 및 시나리오에 대 한 자세한 내용은 참조 하십시오. [tooSQL 서버 업그레이드](https://msdn.microsoft.com/library/bb677622.aspx)합니다.

다음 표에 hello 각 hello 기본 마이그레이션 메서드의 나열 하 고 hello를 사용 하 여 각 방법의 가장 적합 한 경우에 대해 설명 합니다.

| 메서드 | 원본 데이터베이스 버전 | 대상 데이터베이스 버전 | 원본 데이터베이스 백업 크기 제약 조건 | 참고 사항 |
| --- | --- | --- | --- | --- |
| [압축을 직접 복사 hello에 대 한 백업 파일을 사용 하 여 hello Azure 가상 컴퓨터에 온-프레미스 백업 수행](#backup-and-restore) |SQL Server 2005 이상 |SQL Server 2005 이상 |[Azure VM 저장소 제한](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | 컴퓨터 간에 데이터베이스를 이동하는 매우 간단하고 검증된 방법입니다. |
| [백업 tooURL 수행 하 고 hello hello URL에서 Azure 가상 컴퓨터에 복원](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 이상 |SQL Server 2012 SP1 CU2 이상 |SQL Server 2016의 경우 12.8TB 미만, 그렇지 않은 경우 1TB 미만 | 이 메서드는 또 다른 방법은 toomove hello 백업 파일 toohello VM Azure 저장소를 사용 하 여 합니다. |
| [분리 hello 데이터 및 로그 파일 tooAzure blob 저장소를 복사 하 고 URL에서 Azure 가상 컴퓨터에서 tooSQL 서버 연결](#detach-and-attach-from-url) |SQL Server 2005 이상 |SQL Server 2014 이상 |[Azure VM 저장소 제한](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |너무 계획 하는 경우이 메서드를 사용 하 여[hello Azure Blob 저장소 서비스를 사용 하 여 이러한 파일을 저장](https://msdn.microsoft.com/library/dn385720.aspx) tooSQL 서버를 연결 하 고, 특히 매우 큰 데이터베이스는 Azure VM에서 실행 중인 |
| [Convert 온-프레미스 컴퓨터 tooHyper-V Vhd tooAzure Blob 저장소에 업로드 한 다음 업로드 된 VHD를 사용 하 여 새 가상 컴퓨터를 배포](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 이상 |SQL Server 2005 이상 |[Azure VM 저장소 제한](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |사용 하는 경우 [사용자 고유의 SQL Server 라이선스를 가져오는](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), SQL Server의 이전 버전에서 실행 되는 데이터베이스를 마이그레이션할 때 때나 마이그레이션 시스템 및 사용자 데이터베이스의 일부로 함께 hello 다른에 종속 되는 데이터베이스의 마이그레이션 사용자 데이터베이스 및/또는 시스템 데이터베이스입니다. |
| [Windows 가져오기/내보내기 서비스를 사용하여 하드 드라이브 제공](#ship-hard-drive) |SQL Server 2005 이상 |SQL Server 2005 이상 |[Azure VM 저장소 제한](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |사용 하 여 hello [Windows 가져오기/내보내기 서비스](../../../storage/common/storage-import-export-service.md) 수동 복사 방법을 너무 느리면와 같은 데이터베이스의 크기가 매우 큰 경우 |
| [사용 하 여 hello Azure 복제본 추가 마법사](../classic/sql-onprem-availability.md) |SQL Server 2012 이상 |SQL Server 2012 이상 |[Azure VM 저장소 제한](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |가동 중지 시간을 최소화하고 AlwaysOn 온-프레미스 배포가 있을 경우 사용 |
| [SQL Server 트랜잭션 복제 사용](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 이상 |SQL Server 2005 이상 |[Azure VM 저장소 제한](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |사용 하 여 toominimize 가동 중지 시간 및 AlwaysOn 온-프레미스 배포 하지 않은 경우 |

## <a name="backup-and-restore"></a>백업 및 복원
압축으로 데이터베이스를 백업 hello 백업 toohello VM을 복사한 다음 hello 데이터베이스를 복원 합니다. 백업 파일이 1TB 보다 큰 경우 hello VM 디스크의 최대 크기는 1TB 때문에 스트라이프 해야 합니다. 일반적인 단계 toomigrate이 수동 방법을 사용 하 여 사용자 데이터베이스를 따라 hello를 사용 합니다.

1. 전체 데이터베이스 백업 tooan 온-프레미스 위치를 수행 합니다.
2. 만들거나 hello 버전 필요한 SQL Server의 가상 컴퓨터를 업로드 합니다.
3. 요구 사항에 따라 연결을 설정합니다. 참조 [tooa (리소스 관리자) Azure에서 SQL Server 가상 컴퓨터를 연결](virtual-machines-windows-sql-connect.md)합니다.
4. 백업 파일 tooyour VM에 복사 합니다. 명령 프롬프트에서 원격 데스크톱, Windows 탐색기 또는 hello 복사 명령을 사용 하 여 합니다.

## <a name="backup-toourl-and-restore"></a>TooURL 백업 및 복원
Tooa 로컬 파일에 백업 하는 대신 hello를 사용할 수 있습니다 [백업 tooURL](https://msdn.microsoft.com/library/dn435916.aspx) 한 다음 URL toohello VM에서에서 복원 합니다. SQL Server 2016 스트라이프 백업 세트는 지원, 성능을 위해 권장 되 및 필요한 blob 당 tooexceed hello 크기 제한 합니다. 매우 큰 데이터베이스에 대 한 hello 사용 하 여 hello [Windows 가져오기/내보내기 서비스](../../../storage/common/storage-import-export-service.md) 것이 좋습니다.

## <a name="detach-and-attach-from-url"></a>URL에서 분리 및 연결
데이터베이스 및 로그 파일을 분리 하 고 너무 전송[Azure Blob 저장소](https://msdn.microsoft.com/library/dn385720.aspx)합니다. Azure VM에서 hello URL에서 hello 데이터베이스에 연결 합니다. Blob 저장소에 실제 데이터베이스 파일 tooreside hello를 원하는 경우이 사용 합니다. 매우 큰 데이터베이스에 유용할 수 있습니다. 일반적인 단계 toomigrate이 수동 방법을 사용 하 여 사용자 데이터베이스를 따라 hello를 사용 합니다.

1. Hello 인스턴스에서 데이터베이스 파일을 hello 온-프레미스 데이터베이스를 분리 합니다.
2. Hello를 사용 하 여 Azure blob 저장소로 분리 하는 hello 데이터베이스 파일을 복사 합니다. [AZCopy 명령줄 유틸리티](../../../storage/common/storage-use-azcopy.md)합니다.
3. Hello 데이터베이스 파일 hello Azure VM의에서 hello Azure URL toohello SQL Server 인스턴스에 연결 합니다.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>TooVM 변환 및 tooURL 업로드 하 고, 새 VM으로 배포
온-프레미스 SQL Server 인스턴스 tooAzure 가상 컴퓨터에이 메서드 toomigrate 모든 시스템 및 사용자 데이터베이스를 사용 합니다. 이 수동 방법을 사용 하 여 전체 SQL Server 인스턴스 toomigrate 일반적인 단계를 수행 하는 hello를 사용 합니다.

1. 실제 또는 가상 convert를 사용 하 여 tooHyper-V Vhd 컴퓨터 [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx)합니다.
2. Hello를 사용 하 여 VHD 파일 tooAzure 저장소 업로드 [Add-azurevhd cmdlet](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx)합니다.
3. 새 배포 hello를 사용 하 여 가상 컴퓨터 VHD를 업로드 합니다.

> [!NOTE]
> toomigrate 전체 응용 프로그램을 사용 하 여 고려 [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>하드 드라이브를 제공합니다.
사용 하 여 hello [Windows 가져오기/내보내기 서비스 메서드](../../../storage/common/storage-import-export-service.md) tootransfer 많은 양의 파일 데이터 tooAzure 여기서 hello 네트워크를 통해 업로드는 지나치게 많은 비용이 들 또는 가능 하지 않은 경우에는 Blob 저장소입니다. 이 서비스와 하나 보내는 또는 데이터 수는 해당 데이터 tooan Azure 데이터 센터를 포함 하는 더 많은 하드 드라이브 업로드 tooyour 저장소 계정입니다.

## <a name="next-steps"></a>다음 단계
Azure 가상 컴퓨터의 SQL Server 실행에 대한 자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

캡처된 이미지에서 Azure SQL Server 가상 컴퓨터를 만드는 방법에 지침은 [팁 및 트릭에 캡처된 이미지에서 Azure SQL 가상 컴퓨터를 '복제'](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) hello CSS SQL Server 엔지니어 블로그.

