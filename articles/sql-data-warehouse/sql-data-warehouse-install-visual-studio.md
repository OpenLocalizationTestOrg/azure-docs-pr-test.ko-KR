---
title: "aaaInstall Visual Studio 및 SQL 데이터 웨어하우스 용 SSDT | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스용 Visual Studio 및 SSDT(SQL Server 개발 도구) 설치"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>SQL Data Warehouse용 Visual Studio 및 SSDT 설치
SQL 데이터 웨어하우스에 대 한 응용 프로그램 toodevelop hello 가장 최신 버전의 Visual Studio를 사용 하 여 hello 가장 최근 버전 SQL Server Data Tools (SSDT)의 두는 것이 좋습니다.  이전 버전과의 호환성을 위해 SSDT와 함께 Visual Studio 2013 업데이트 5도 지원됩니다.  

SSDT Visual Studio를 사용 하면 toouse hello SQL Server 개체 탐색기 toovisually 테이블, 뷰, 저장된 프로시저 및 SQL 데이터 웨어하우스에 더 많은 개체를 탐색할 수 있을 뿐만 아니라 쿼리를 실행 합니다.

> [!NOTE]
> SQL 데이터 웨어하우스는 아직 Visual Studio 데이터베이스 프로젝트를 지원하지 않습니다.  이 기능은 이후 버전에 추가됩니다.
> 
> 

## <a name="step-1-install-visual-studio"></a>1단계: Visual Studio 설치
이러한 링크 toodownload 따르고 Visual Studio를 설치 합니다. 이미 Visual Studio 2013 또는 이상이 설치 되어 tooStep 2를 건너뛸 수, 하는 경우 SSDT를 설치 합니다.

1. [Visual Studio를 다운로드][]합니다.
2. Hello에 따라 [Visual Studio 설치] [ Installing Visual Studio] MSDN에서 안내 하 고 hello 기본 구성을 선택 합니다.

## <a name="step-2-install-ssdt"></a>2단계: SSDT 설치
Visual Studio 용 SSDT tooinstall 다음이 단계를 수행 하 여 Visual Studio 내에서 SSDT 업데이트에 대 한 단순히 확인 합니다.

1. Visual Studio에서 **도구** / **확장 및 업데이트...**를 클릭합니다. / **업데이트**
2. **제품 업데이트**를 선택한 후 **데이터베이스 도구용 Microsoft SQL Server 업데이트**를 찾습니다.

업데이트가 발견 되지 않으면 경우에 hello 최신 버전이 설치 되어 있어야 합니다.  tooconfirm SSDT가 설치 되어 클릭 **도움말** / **에 대 한 Microsoft Visual Studio** hello 목록에서 SQL Server Data Tools을 찾습니다.  최신 버전의 SSDT hello 14.0.60525.0입니다.  Hello 옵션 tooinstall Visual Studio에서 사용할 수 없는 경우 또는 방문할 수 있습니다 hello [SSDT 다운로드] [ SSDT Download] toodownload 페이지 SSDT를 수동으로 설치 하십시오.

## <a name="next-steps"></a>다음 단계
Hello 최신 버전의 SSDT가지고 준비가 너무[연결] [ connect] tooyour SQL 데이터 웨어하우스 합니다.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Visual Studio를 다운로드]: https://www.visualstudio.com/downloads/합니다.
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
