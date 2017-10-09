---
title: "Azure 자동화를 사용 하 여 Azure SQL 데이터베이스 aaaManage | Microsoft Docs"
description: "Azure 자동화 서비스 hello 규모에 사용 되는 toomanage Azure SQL 데이터베이스를 수 있는 방법에 대해 알아봅니다."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Azure 자동화를 사용하여 Azure SQL 데이터베이스 관리
이 가이드에서는 toohello Azure 자동화 서비스 및 Azure SQL 데이터베이스의 관리를 사용 하는 toosimplify 수 있는 방법을 소개 합니다.

## <a name="what-is-azure-automation"></a>Azure 자동화 정의
[Azure 자동화](https://azure.microsoft.com/services/automation/) 는 프로세스 자동화를 통해 클라우드 관리를 간소화하기 위한 Azure 서비스입니다. Azure 자동화를 사용 하 여 장기 실행, 수동, 오류가 발생 하기 쉽고 자주 반복 되는 작업에 자동화 된 tooincrease 안정성, 효율성 및 조직에 대 한 시간 toovalue 수 있습니다.

Azure 자동화는 조직의 규모가 커짐에 toomeet 요구에 맞게 확장 되는 매우 안정적이 고 항상 사용 가능한 워크플로 실행 엔진을 제공 합니다. Azure 자동화에서는 작업이 정확히 필요한 시간에 수행되도록 수동, 타사 시스템 또는 예약된 간격에 의해 프로세스를 시작할 수 있습니다.

작동 오버 헤드를 줄이고 확보 IT / DevOps 직원 toofocus 프로그램 클라우드 관리 작업 toobe 이동 하 여 비즈니스 가치를 추가 하는 작업에는 Azure 자동화에 의해 자동으로 실행 합니다.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Azure 자동화를 통해 Azure SQL 데이터베이스 관리 향상
Hello를 사용 하 여 Azure 자동화에서 azure SQL 데이터베이스를 관리할 수 있습니다 [Azure SQL 데이터베이스 PowerShell cmdlet](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) hello에서 사용 가능한 [Azure PowerShell 도구](/powershell/azure/overview)합니다. Azure 자동화에는 사용할 수 있는 Azure SQL 데이터베이스 PowerShell cmdlet이 hello 상자 밖의 hello 서비스 내에서 SQL DB 관리 작업을 모두 수행할 수 있도록 합니다. 또한 Azure 서비스 및 제 3 자 시스템에서 다른 Azure 서비스, tooautomate 복잡 한 작업에 대 한 hello cmdlet 통해 Azure 자동화에서 이러한 cmdlet을 페어링할 수 있는 합니다.

Azure 자동화에는 SQL 서버와 hello 기능 toocommunicate를 직접 PowerShell을 사용 하 여 SQL 명령을 실행 하 여 있습니다.

hello [Azure 자동화 runbook 갤러리](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) 에 다양 한 제품 팀과 커뮤니티 runbook tooget Azure SQL 데이터베이스, 다른 Azure 서비스 및 제 3 자 시스템 관리를 자동화를 시작 합니다. Runbook 갤러리에는 다음이 포함됩니다.

* [SQL Server 데이터베이스에 대해 SQL 쿼리를 실행 합니다.](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [일정에 따라 Azure SQL 데이터베이스를 세로로(위쪽 또는 아래쪽) 조정합니다.](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [해당 데이터베이스의 최대 크기에 도달한 경우 SQL 테이블을 줄이세요.](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Azure SQL 데이터베이스가 심하게 조각화 된 경우 테이블에 색인을 달아주세요.](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>다음 단계
Azure 자동화 및 Azure SQL 데이터베이스를 사용 하는 toomanage 수 있는 방법의 hello 기본 사항 학습 한를 했으므로 이러한 링크 toolearn Azure 자동화에 대 한 자세한를 수행 합니다.

* [Azure 자동화 개요](../automation/automation-intro.md)
* [내 첫 번째 runbook](../automation/automation-first-runbook-graphical.md)
* [Azure 자동화 학습 맵](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Azure 자동화: hello 클라우드에서에서 SQL 에이전트](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

