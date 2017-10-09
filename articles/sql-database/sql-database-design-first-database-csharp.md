---
title: "aaaDesign 첫 번째 Azure SQL 데이터베이스-C# | Microsoft Docs"
description: "Toodesign 첫 번째 Azure SQL 데이터베이스 알아보고 tooit ADO.NET을 사용 하 여 C# 프로그램을 사용 하 여 연결 합니다."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a>Azure SQL Database 설계 및 C#과 ADO.NET에 연결

Azure SQL 데이터베이스는 관계형 데이터베이스-으로-a (DBaaS)의 서비스 hello Microsoft 클라우드 ("Azure"). 이 자습서에서는 Azure 포털 및 Visual studio에 ADO.NET toouse hello 하는 방법을 배웁니다. 

> [!div class="checklist"]
> * Hello Azure 포털에서에서 데이터베이스 만들기
> * Hello Azure 포털에서에서 서버 수준 방화벽 규칙 설정
> * ADO.NET 및 Visual Studio를 사용 하 여 toohello 데이터베이스 연결
> * ADO.NET을 사용하여 테이블 만들기
> * ADO.NET을 사용하여 데이터 삽입, 업데이트 및 삭제 
> * ADO.NET 데이터 쿼리

Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>필수 조건

설치된 [Visual Studio Community 2017, Visual Studio Professional 2017 또는 Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/)

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a>다음 단계

이 자습서에서는 기본적인 데이터베이스 작업 같은 데이터베이스와 테이블을 만들 배운, 로드 및 데이터를 쿼리하고 hello 데이터베이스 tooa 이전 지정 시간으로 복원 합니다. 다음 방법에 대해 알아보았습니다.
> [!div class="checklist"]
> * 데이터베이스 만들기
> * 방화벽 규칙 설정
> * 사용 하 여 toohello 데이터베이스 연결 [Visual Studio 및 C#](sql-database-connect-query-dotnet-visual-studio.md)
> * 테이블 만들기
> * 데이터 삽입, 업데이트 및 삭제
> * 쿼리 데이터

데이터 마이그레이션에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
>[SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션](sql-database-migrate-your-sql-server-database.md)

