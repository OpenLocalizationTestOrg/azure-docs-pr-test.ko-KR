---
title: "aaaMicrosoft 포함 된 Power BI 미리 보기 문제 해결"
description: "Microsoft Power BI Embedded 미리 보기 문제 해결"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Microsoft Power BI Embedded 미리 보기 문제 해결
이 문서는 방법에 대 한 대답을 제공 tootroubleshoot **Power BI 포함**합니다.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>SQL Server 연결 문자열 설정
SQL Server 연결 문자열 tooset toofollow 특정 형식 필요합니다. SQL Server에 대한 연결 문자열의 예는 아래와 같습니다.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

SQL Server 연결 문자열에 대해 자세히 toolearn hello 다음 문서 참조:

* [SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>자격 증명 설정
개발 또는 사용자 이름 및 암호와 같은 스테이징 환경에 대 한 자격 증명이 있는 hello 경우에는 프로덕션 솔루션 일치 하는 tooupdate 자격 증명을 할 수 있습니다.

## <a name="see-also"></a>참고 항목
* [샘플 시작](power-bi-embedded-get-started-sample.md)
* [Power BI Embedded란](power-bi-embedded-what-is-power-bi-embedded.md)

