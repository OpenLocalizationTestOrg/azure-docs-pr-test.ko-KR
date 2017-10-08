---
title: "데이터 감사를 위한 지원 aaaSQL 데이터 웨어하우스 하위 클라이언트 | Microsoft Docs"
description: "데이터 감사에 대한 SQL 데이터 웨어하우스 하위 수준 클라이언트 지원에 대해 알아보기"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>SQL Data Warehouse - 감사 및 동적 데이터 마스킹에 대한 하위 수준 클라이언트 지원
[감사](sql-data-warehouse-auditing-overview.md) 는 TDS 리디렉션을 지원하는 SQL 클라이언트와 함께 작동합니다.

TDS 7.4를 구현하는 모든 클라이언트는 리디렉션도 지원해야 합니다. 예외 toothis 리디렉션 구현 되지 않은 Node.JS 용 hello 리디렉션 기능을 완벽 하 게 지원 되지 않으며 Tedious에 JDBC 4.0를 포함 합니다.

"하위 클라이언트"에 대 한 즉, TDS 버전 7.3 지원 하 고 아래-hello 연결 문자열에 FQDN 서버 hello 수정 해야 합니다.

Hello 연결 문자열에서 원래 서버 FQDN: <*서버 이름*>. database.windows.net

Hello 연결 문자열에 수정 된 서버 FQDN: <*서버 이름*>.database. **보안**. windows.net

"하위 클라이언트"의 일부 목록에는 다음이 포함됩니다.

* .NET 4.0 이하
* ODBC 10.0 이하
* JDBC (JDBC TDS 7.4, TDS 리디렉션 기능을 완전히 지원 되지 않는 hello는 지원) 하는 중
* Tedious(Node.JS용)

**설명:** hello 서버 FDQN 수정 위에 (임시 완화) 각 데이터베이스에는 구성에 대 한 요구가 단계 없이 SQL 서버 수준 감사 정책 적용에 대 한도 유용할 수 있습니다.     

