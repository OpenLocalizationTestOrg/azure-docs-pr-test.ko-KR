---
title: "SQL Server Vm에 대 한 aaaStorage 구성 | Microsoft Docs"
description: "이 항목에서는 Azure가 프로비전하는 동안 SQL Server VM에 대한 저장소를 구성하는 방법을 설명합니다(Resource Manager 배포 모델). 또한 기존 SQL Server VM에 대한 저장소를 구성하는 방법을 설명합니다."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>SQL Server VM에 대한 저장소 구성
Azure에서 SQL Server 가상 컴퓨터 이미지를 구성 hello 포털 저장소 구성이 tooautomate 해줍니다. 여기에 연결 하는 저장소 toohello VM을 해당 저장소 액세스할 수 있는 tooSQL 서버를 만들고이 toooptimize 특정 성능 요구 사항에 맞게 구성 됩니다.

이 항목에서는 Azure에서 프로비전 중 저장소 SQL Server VM 및 기존 VM에 대한 저장소를 구성하는 방법을 설명합니다. 이 구성은 hello 기초로 [성능 모범 사례](virtual-machines-windows-sql-performance.md) Azure vm의 SQL Server를 실행 합니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>필수 조건
toouse hello 자동 저장소 구성 설정, 가상 컴퓨터 특성에 따라 hello 필요:

* [SQL Server 갤러리 이미지](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing)로 프로비전합니다.
* 사용 하 여 hello [리소스 관리자 배포 모델](../../../azure-resource-manager/resource-manager-deployment-model.md)합니다.
* [프리미엄 저장소](../../../storage/common/storage-premium-storage.md)를 사용합니다.

## <a name="new-vms"></a>새 VM
hello 다음 섹션에서는 설명 방법을 새 SQL Server 가상 컴퓨터에 대 한 tooconfigure 저장소입니다.

### <a name="azure-portal"></a>Azure 포털
SQL Server 갤러리 이미지를 사용 하 여 Azure VM을 프로 비전 하는 경우 선택할 수 있습니다 tooautomatically 새 VM에 대 한 hello 저장소를 구성 합니다. Hello 저장소 크기, 성능 제한 및 작업 유형을 지정 합니다. hello 다음 스크린샷은 SQL VM 중에 사용 하는 hello 저장소 구성 블레이드 프로 비전 합니다.

![프로비전하는 동안 SQL Server VM 저장소 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

선택한 설정에 따라 Azure hello 저장소 구성 작업 hello VM을 만든 후 다음을 수행 합니다.

* 에서는 프리미엄 저장소 데이터 디스크 toohello 가상 컴퓨터를 연결 합니다.
* Hello 데이터 디스크 toobe 액세스할 수 있는 tooSQL 서버를 구성합니다.
* Hello 데이터 디스크를 저장소로 구성 hello에 따라 풀 크기와 성능 (IOPS 및 처리량) 요구 사항을 지정 합니다.
* Hello 가상 컴퓨터를 새 드라이브로 hello 저장소 풀을 연결합니다.
* 지정한 워크로드 유형(데이터 웨어하우징, 트랜잭션 처리 또는 일반)에 따라 새 드라이브를 최적화합니다.

Azure 저장소의 설정을 구성 하는 방법에 자세한 내용은 참조 hello [저장소 구성 섹션](#storage-configuration)합니다. Toocreate hello Azure 포털에서에서 SQL Server VM 확인 하려면 어떻게 해야 하는 전체 연습은 [자습서를 프로 비전 하는 hello](virtual-machines-windows-portal-sql-server-provision.md)합니다.

### <a name="resource-manage-templates"></a>Resource Manager 템플릿
리소스 관리자 템플릿을 다음 hello를 사용 하는 경우 기본적으로 저장소 풀 구성 하지 않고도 두 개의 프리미엄 데이터 디스크가 연결 되어 있습니다. 그러나 이러한 템플릿을 toochange hello 수가 toohello 연결 된 가상 컴퓨터는 프리미엄 데이터 디스크를 사용자 지정할 수 있습니다.

* [자동화된 백업을 사용하여 VM 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [자동화된 패치를 사용하여 VM 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [AKV 통합을 사용하여 VM 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>기존 VM
기존 SQL Server Vm에 대 한 hello Azure 포털에서에서 일부 저장소 설정을 수정할 수 있습니다. VM을 선택, toohello 설정 영역을 이동 하 고 SQL Server 구성을 선택 합니다. SQL Server 구성 블레이드 hello VM의 hello 현재 저장소 사용을 보여 줍니다. VM에 있는 모든 드라이브는 이 차트에 표시됩니다. 각 드라이브에 대 한 hello 저장 공간 4 개의 섹션에 표시 됩니다.

* SQL 데이터
* SQL 로그
* 기타(비 SQL 저장소)
* 사용 가능

![기존 SQL Server VM에 대한 저장소 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure hello 저장소 tooadd 새 드라이브 또는 기존 드라이브를 확장, hello 차트 위 hello 편집 링크를 클릭 합니다.

볼 수 있는 hello 구성 옵션 하기 전에이 기능 사용 여부에 따라 달라 집니다. 처음으로 hello에 대 한 사용 하 여, 새 드라이브에 대 한 저장소 요구 사항을 지정할 수 있습니다. 이 기능은 toocreate 드라이브를 이전에 사용한 경우 해당 드라이브의 저장소 tooextend를 선택할 수 있습니다.

### <a name="use-for-hello-first-time"></a>처음으로 hello에 대 한 사용
지정할 수는 경우에이 기능을 사용 하 여 처음으로, 새 드라이브에 대 한 저장소 크기와 성능 제한 hello 합니다. 이 환경은 비슷한 toowhat 시간 프로 비전에 표시 되는 것입니다. hello 주요 차이점은 toospecify hello 작업 부하 유형이 허용 되지 않습니다. 이 제한 사항은 hello 가상 컴퓨터에 모든 기존 SQL Server 구성을 중단을 방지 합니다.

![SQL Server 저장소 슬라이더 구성](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

Azure는 사양에 따라 새 드라이브를 만듭니다. 이 시나리오에서는 Azure 저장소 구성 작업을 수행 하는 hello를 수행 합니다.

* 에서는 프리미엄 저장소 데이터 디스크 toohello 가상 컴퓨터를 연결 합니다.
* Hello 데이터 디스크 toobe 액세스할 수 있는 tooSQL 서버를 구성합니다.
* Hello 데이터 디스크를 저장소로 구성 hello에 따라 풀 크기와 성능 (IOPS 및 처리량) 요구 사항을 지정 합니다.
* Hello 가상 컴퓨터를 새 드라이브로 hello 저장소 풀을 연결합니다.

Azure 저장소의 설정을 구성 하는 방법에 자세한 내용은 참조 hello [저장소 구성 섹션](#storage-configuration)합니다.

### <a name="add-a-new-drive"></a>새 드라이브 추가
SQL Server VM에 이미 저장소를 구성한 경우 저장소를 확장하면 두 가지 새로운 옵션을 표시합니다. hello 첫 번째 옵션은 tooadd는 새 드라이브를 VM의 hello 성능 수준을 늘릴 수 있습니다.

![새 드라이브 tooa SQL VM 추가](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

그러나 hello 드라이브를 추가한 후 몇 가지 추가 수동 구성 tooachieve hello 성능 향상을 수행 해야 합니다.

### <a name="extend-hello-drive"></a>Hello 드라이브를 확장 합니다.
hello 저장소 확장을 위한 다른 옵션은 tooextend hello 기존 드라이브입니다. 이 옵션을 사용 하면 사용자의 드라이브에 대 한 사용 가능한 저장소 hello 있지만 성능을 증가 하지 않습니다. 저장소 풀과 hello 저장소 풀이 만들어진 후 hello 열 수를 변경할 수 없습니다. 열 수가 hello hello 데이터 디스크 스트라이프 수는 병렬 쓰기 hello 수를 결정 합니다. 따라서 추가 데이터 디스크는 성능을 향상시킬 수 없습니다. 만 쓰여지는 hello 데이터에 대 한 더 많은 저장 공간을 제공할 수 있습니다. 이 제한 사항은 hello 드라이브를 확장 하는 경우 열 수가 hello 추가할 수 있는 데이터 디스크의 hello 최소 수를 결정 한다는 의미 이기도 합니다. 따라서 4 개의 데이터 디스크와 저장소 풀을 만드는 경우 열의 hello 수는 또한 4 개입니다. Hello 저장소를 확장 하 든 지 4 개 이상의 데이터 디스크를 추가 해야 합니다.

![SQL VM에 대한 드라이브 확장](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>Storage 구성
이 섹션에서는 Azure SQL VM 프로 비전 또는 hello Azure 포털에서에서 구성 하는 동안 자동으로 수행 하는 hello 저장소 구성 변경에 대 한 대 한 참조를 제공 합니다.

* VM에 대한 2TB 미만의 저장소를 선택한 경우 Azure는 저장소 풀을 만들지 않습니다.
* VM에 대한 2TB 이상의 저장소를 선택한 경우 Azure는 저장소 풀을 구성합니다. 이 항목의 다음 섹션 hello hello 저장소 풀 구성의 hello 세부 정보를 제공합니다.
* 자동 저장소 구성은 항상 [프리미엄 저장소](../../../storage/common/storage-premium-storage.md) P30 데이터 디스크를 사용합니다. 따라서 선택한 수가 테라바이트 간에 1:1 매핑 않으며 tooyour VM을 첨부 하는 데이터 디스크의 hello 수입니다.

가격 책정 정보 참조 hello [저장소 가격](https://azure.microsoft.com/pricing/details/storage) hello에 대 한 페이지 **디스크 저장소** 탭 합니다.

### <a name="creation-of-hello-storage-pool"></a>Hello 저장소 풀 만들기
Azure는 SQL Server Vm에 설정을 toocreate hello 저장소 풀을 다음과 같은 hello를 사용 합니다.

| 설정 | 값 |
| --- | --- |
| 스트라이프 크기 |256KB(데이터 웨어하우징); 64KB(트랜잭션) |
| 디스크 크기 |각각 1TB |
| 캐시 |읽기 |
| 할당 크기 |64KB NTFS 할당 단위 크기 |
| 즉시 파일 초기화 |사용 |
| 메모리 내 페이지 잠금 |사용 |
| 복구 |단순 복구(복원력 없음) |
| 열 수 |데이터 디스크 수<sup>1</sup> |
| TempDB 위치 |데이터 디스크에 저장됨<sup>2</sup> |

<sup>1</sup> hello 저장소 풀을 만든 후 hello hello 저장소 풀의 열 수를 변경할 수 없습니다.

<sup>2</sup> 이 설정은 hello 저장소 구성 기능을 사용 하 여 만드는 toohello 첫 번째 드라이브에만 적용 됩니다.

## <a name="workload-optimization-settings"></a>워크로드 최적화 설정
hello 다음 표에서 hello 세 가지 작업 유형 사용 가능한 옵션 및 해당 해당 최적화.

| 워크로드 유형 | 설명 | 최적화 |
| --- | --- | --- |
| **일반** |대부분의 워크로드를 지원하는 기본 설정 |없음 |
| **트랜잭션 처리** |일반 데이터베이스 OLTP 워크 로드에 대 한 hello 저장소를 최적화 |추적 플래그 1117<br/>추적 플래그 1118 |
| **데이터 웨어하우징** |분석 및 보고 작업에 대 한 hello 저장소를 최적화 |추적 플래그 610<br/>추적 플래그 1117 |

> [!NOTE]
> Hello 저장소 구성 단계에서 선택 하 여 SQL 가상 컴퓨터를 프로 비전 할 때에 hello 작업 유형을 지정할 수 있습니다.
>
>

## <a name="next-steps"></a>다음 단계
다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)합니다.
