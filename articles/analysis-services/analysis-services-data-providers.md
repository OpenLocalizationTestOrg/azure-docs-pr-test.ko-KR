---
title: "tooAzure Analysis Services에 연결 하는 데 필요한 aaaClient 라이브러리 | Microsoft Docs"
description: "클라이언트 응용 프로그램 및 도구 tooconnect Azure Analysis Services에 필요한 클라이언트 라이브러리를 설명 합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>TooAzure Analysis Services에 연결 하기 위한 클라이언트 라이브러리

클라이언트 라이브러리는 클라이언트 응용 프로그램 및 도구 tooconnect tooAnalysis 서비스 서버에 대 한 필요 합니다. 

Analysis Services는 세 가지 클라이언트 라이브러리를 활용합니다. ADOMD.NET 및 AMO(Analysis Services Management Objects)는 관리되는 클라이언트 라이브러리입니다. hello Analysis Services OLE DB 공급자 (MSOLAP DLL)는 네이티브 클라이언트 라이브러리입니다. hello에 3을 모두 설치 하는 일반적으로 같은 시간입니다. Azure Analysis Services hello 최신 버전이 필요합니다. 

Power BI Desktop 및 Excel과 같은 Microsoft 클라이언트 응용 프로그램은 세 가지 클라이언트 라이브러리를 모두 설치합니다. 그러나 hello 버전 또는 업데이트 빈도 따라 클라이언트 라이브러리 아닐 Azure Analysis Services에서 필요한 hello 최신 버전입니다. hello 마찬가지 toocustom 응용 프로그램이 나 AsCmd, TOM, ADOMD.NET 같은 다른 인터페이스입니다. 이러한 응용 프로그램 hello 라이브러리를 수동으로 설치 해야 합니다. 수동 설치를 위한 hello 클라이언트 라이브러리는 배포 가능한 패키지와 SQL Server 기능 팩에 포함 됩니다. 그러나 이러한 클라이언트 라이브러리 동률된 toohello SQL Server 버전 이며 hello를 최신 수 있습니다.  

클라이언트 연결에 대 한 클라이언트 라이브러리는 Azure Analysis Services 서버 tooa 데이터 원본에서 데이터 공급자 필요한 tooconnect 다릅니다. 데이터 원본 연결에 대해 자세히 toolearn 참조 [데이터 원본 연결](analysis-services-datasource.md)합니다.

## <a name="download-hello-latest-client-libraries"></a>Hello 최신 클라이언트 라이브러리 다운로드  
프로덕션 환경에 있으며 완전히 해제 한 후 지원 되는 버전을 필요로 하는 경우 클라이언트 라이브러리를 따라 hello를 사용 합니다.

[MSOLAP(amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP(x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>다음 단계
[Excel로 연결](analysis-services-connect-excel.md)    
[Power BI와 연결](analysis-services-connect-pbi.md)
