---
title: "Analysis Services와 Excel aaaConnect tooAzure | Microsoft Docs"
description: "어떻게 tooconnect tooan Azure Analysis Services에 대해 알아봅니다 Excel을 사용 하 여 서버입니다."
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a>Excel로 연결

Azure에서 서버를 만들고 테이블 형식 모델 tooit 배포 했 되 면 준비 tooconnect와는 데이터 탐색을 시작 합니다.


## <a name="connect-in-excel"></a>Excel에서 연결

Excel에서 tooa 서버에 연결 하는 Excel 2016에서 데이터 가져오기를 사용에서 지원 됩니다. 파워 피벗의 hello 테이블 가져오기 마법사를 사용 하 여 연결 하는 것은 지원 되지 않습니다. 

**Excel 2016에서 tooconnect**

1. Hello에 Excel 2016에서 **데이터** 리본에서 클릭 **외부 데이터 가져오기** > **기타 원본** > **Analysis Services** .

2. 데이터 연결 마법사에서 hello **서버 이름**, 프로토콜 및 URI를 포함 하 여 hello 서버 이름을 입력 합니다. 그런 다음 **로그온 자격 증명을**선택, **다음 사용자 이름 및 암호 사용 하 여 hello**, 한 다음 예를 들어 hello 조직 사용자 이름을 입력 nancy@adventureworks.com, 및 암호.

    ![Excel 로그온에서 연결](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. **데이터베이스 및 테이블 선택**, hello 데이터베이스, 모델 또는 큐브 뷰를 선택한 다음 클릭 **마침**합니다.
   
    ![Excel 선택 모델에서 연결](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>참고 항목
[클라이언트 라이브러리](analysis-services-data-providers.md)   
[서버 관리](analysis-services-manage.md)     


