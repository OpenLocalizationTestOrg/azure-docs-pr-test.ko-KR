---
title: "Azure 가상 컴퓨터에 SQL Server에 대 한 효과적으로 aaaManage 비용 | Microsoft Docs"
description: "Hello 오른쪽 SQL Server 가상 컴퓨터 가격 책정 모델을 선택 하기 위한 유용한 정보를 제공 합니다."
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>SQL Server Azure VM에 대한 가격 책정 지침

이 항목에서는 Azure의 SQL Server 가상 컴퓨터에 대한 가격 책정 지침을 제공합니다. 비용에 영향을 주는 여러 가지 아니며 비즈니스 요구를 사용 하 여 비용의 균형을 중요 한 toopick hello 오른쪽 이미지 합니다.

## <a name="free-licensed-sql-server-editions"></a>무료 라이선스 SQL Server 버전

Toodevelop 하려는 경우를 테스트 또는 개념 증명 빌드 다음 무료 라이선스 hello를 사용 하 여 **SQL Server Developer edition**합니다. 이 버전은 모든 SQL Server Enterprise edition에서, 따라서 사용할 수 있습니다 toobuild 원하는 모든 응용 프로그램입니다. 프로덕션 환경에서 toorun을 허용 하지 않습니다. SQL Server 개발자 VM 대금을 청구 hello 비용의 hello VM에 SQL Server 라이선스에 대 한 되지 않습니다.

Toorun 프로덕션 환경에서 간단한 작업을 하려는 경우 (< 4 개 코어, < 1GB의 메모리 < 10 g B/데이터베이스)를 무료 라이선스 hello를 사용 하 여 **SQL Server Express edition**합니다. SQL Express VM에 대금을 청구 hello 비용 hello VM의 하지 SQL 라이선스입니다.

이러한 개발/테스트 또는 간단한 프로덕션 작업의 경우 이러한 작업에 맞는 더 작은 VM 크기를 선택하여 비용을 절감할 수도 있습니다. hello DS1v2 이러한 작업에 대 한 적합 한 선택 수도 있습니다.

이러한 이미지 중 하나를 사용 하 여 SQL Server 2016 Azure VM toocreate 참조 링크를 따라 hello:

- [SQL Server 2016 Developer Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [SQL Server 2016 Express Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>유료 SQL Server 버전

비 lightweight 프로덕션 작업과 설정한 경우 hello SQL Server 버전을 다음 중 하나를 사용 합니다.

| SQL Server 버전 | 워크로드 |
|-----|-----|
| 웹 | 작은 웹 사이트 |
| Standard | 작은 toomedium 작업 |
| Enterprise | 대규모 또는 중요 업무용 작업|

이러한 버전에 대 한 SQL Server 라이선스에 대 한 두 가지 옵션 toopay 있는: *사용량에 따른 비용 결제* 또는 *사용자 라이선스*합니다.

### <a name="pay-per-usage"></a>사용당 지급

**유료 hello SQL Server 라이선스 사용량 당** hello Azure VM 실행 hello 분당 비용은 hello hello SQL Server 라이선스 비용에 있음을 의미 합니다. 에서 볼 수 있듯이 hello 서로 다른 SQL Server 버전 (웹, Standard, Enterprise)에 대 한 가격 책정 hello hello [Azure VM 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)합니다. hello 비용은 hello 동일한 모든 버전의 SQL Server (2008 R2 too2016). SQL Server와 함께 hello 일반적으로 라이선스 처럼 분당 라이선스 비용은 hello VM 코어 수에 따라 다릅니다.

SQL Server hello 지불 사용량 당 라이선스는 것이 좋습니다.

- 임시 또는 정기적인 작업. 예를 들어 응용 프로그램에 필요한 이벤트 toosupport 두 달에 대 한 모든 연도 또는 비즈니스 분석 월요일.
- 수명 또는 규모를 알 수 없는 작업. 예: 몇 개월 내에 필요하지 않을 수 있거나 수요에 따라 더 많은 또는 더 적은 계산 기능이 필요할 수 있는 앱.

toocreate 이러한 사용량 당 사용량 기준 과금 이미지 중 하나를 사용 하 여 SQL Server 2016 Azure VM hello 다음 링크 참조:

- [SQL Server 2016 Web Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [SQL Server 2016 Standard Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Hello hello에 표시 되는 월별 비용을 예상 hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 만들 때 **크기 선택** 블레이드 SQL Server 라이선스 비용을 다루지 않습니다. 이 hello 단독 VM의 hello 비용입니다.
>
> ![VM 크기 선택 블레이드](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Hello-사용 허가 Express 및 개발자 버전의 SQL Server에서 hello 총 예상된 비용입니다. 하지만 웹, Standard 및 Enterprise에 대 한 hello 추가 SQL 라이선스 비용 hello에 [Windows 가상 컴퓨터 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)합니다. Hello 가격 책정 페이지, SQL Server의 대상 버전을 선택 합니다.

### <a name="bring-your-own-license-byol"></a>BYOL(사용자 라이선스 필요)

**라이선스 이동성을 통해 사용자 고유의 SQL Server 라이선스를 가져오는**, tooas 라고도 **BYOL**기존 SQL Server 볼륨 라이선스를 사용 하 여 Azure VM에서 Software Assurance와 함께 의미 합니다. BYOL를 사용 하 여 SQL Server VM에 대금을 청구 hello 실행 비용을 VM에 SQL Server 라이선스에 대해 hello에 대 한 라이선스 및 Software Assurance 볼륨 라이선스 프로그램을 통해 이미 가져온 있다고 가정 합니다.

License Mobility를 통한 SQL 사용자 라이선스 필요가 권장되는 경우는 다음과 같습니다.

- 연속 작업. 예를 들어 응용 프로그램을 연중 무휴로 toosupport 비즈니스 운영에 필요 합니다.
- 수명 또는 규모가 알려진 작업. 예를 들어 응용 프로그램을 hello 전체 년과 요구는 예상 된 해야 합니다.

SQL Server VM으로 BYOL toouse SQL Server Standard 또는 Enterprise에 대 한 라이선스가 있어야 합니다 및 [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), 몇 가지를 필수 옵션인 [Volume Licensing](https://www.microsoft.com/en-us/download/details.aspx?id=10585) 프로그램 및 선택적 다른 사용자와 구입 합니다.  볼륨 라이선싱 프로그램을 통해 제공 사용료 hello 계약과 hello 수량 또는 약정 tooSQL 서버 hello 형식에 따라 달라 집니다. 하지만 경험상,으로 연속 프로덕션 작업에 대 한 사용자 고유 라이선스를 가져오는 다음 이점을 hello:

| BYOL 이점 | 설명 |
|-----|-----|
| **비용 절감** | 작업에서 SQL Server Standard 또는 Enterprise를 *10개월 넘게* 연속적으로 실행할 경우 SQL Server 사용자 라이선스 필요가 사용당 지급보다 더 비용 효과적입니다. |
| **장기적 절감** | 평균적으로 *30% 연간 더 적게 듭니다* toobuy 또는 첫 번째 3 년 hello에 대 한 SQL Server 라이선스를 갱신 합니다. 또한 3 년이 지나면 toorenew hello 라이선스가 더 이상 Software Assurance에 대 한 정당한 급여 필요 하지 않습니다. 이 시점에는 *200% 더 저렴*합니다. |
| **무료 수동 보조 복제본** | 사용자 고유 라이선스를 가져오는 또 다른 이점은 hello [수동 하나의 보조 복제본에 대 한 라이선스를 확보](https://azure.microsoft.com/pricing/licensing-faq/) 고가용성을 위해 SQL Server 별. 이 라이선스 비용 (예:를 사용 하 여 Always On 가용성 그룹) 항상 사용 가능한 SQL Server 배포의 절반 hello에서 자릅니다. hello 권한 toorun hello 수동 보조 hello 장애 조치 서버 Software Assurance 혜택을 통해 제공 됩니다. |

"{BYOL}"을 접두사로 hello Vm을 확인 하는 toocreate 이러한 bring your-소유-라이선스 이미지 중 하나를 사용 하 여 SQL Server 2016 Azure VM:

- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [SQL Server 2016 Standard Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Azure에서 사용할 SQL Server 라이선스 수를 10일 이내에 알려주세요. hello 링크 toohello 이전 이미지가 지침이 방법은 toodo이 있습니다.

## <a name="avoid-unecessary-costs"></a>불필요한 비용 방지

지속적으로 실행 하지 않는 모든 작업을 사용 하는 경우에 hello 비활성 기간 동안 hello 가상 컴퓨터를 종료 하는 것이 좋습니다. 사용한 양만큼만 요금을 지급합니다.

예를 들어 Azure VM에서 SQL Server 아웃 단순히 하려는 경우 하지 않을 tooincur 요금 실수로 주에 대 한 실행 상태로 유지 합니다. 한 가지 해결 방법은 toouse hello [자동 종료 기능](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)합니다.

![SQL VM 자동 종료](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

자동 종료는 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab)에서 제공되는 광범위한 유사 기능 집합에 포함됩니다.

다른 워크플로의 경우 [Azure Automation](https://azure.microsoft.com/services/automation/) 등의 스크립팅 솔루션을 사용하여 Azure VM을 자동으로 종료하고 다시 시작하는 방법을 고려하세요.

> [!IMPORTANT]
> 종료 되 고 VM을 할당 해제는 hello 유일한 방법은 tooavoid 요금입니다. 단순히를 중지 하거나 전원 옵션 tooshut hello VM 다운을 사용 하 여 여전히 사용 요금을 발생 합니다.

## <a name="next-steps"></a>다음 단계

Azure 가격 책정 지침에 대해서는 [Azure 청구 및 비용 관리를 사용하여 예상치 못한 비용 방지](../../../billing/billing-getting-started.md)를 참조하세요.

가격 책정, 가상 컴퓨터를 최신 SQL Server를 비롯 한 hello hello에 대 한 참조 [Azure VM 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)합니다.

[Azure Virtual Machines의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)에서 다른 SQL Server 가상 컴퓨터 항목을 검토하세요.
