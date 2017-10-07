---
title: Power bi Analysis Services aaaConnect tooAzure | Microsoft Docs
description: "어떻게 tooconnect tooan Azure Analysis Services에 대해 알아봅니다 Power BI를 사용 하 여 서버입니다."
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
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a>Power BI로 연결

Azure에서 서버 생성 되었으며 테이블 형식 모델 tooit 배포, 되 면 조직의 사용자가 준비 tooconnect 되며 데이터 탐색을 시작 합니다. 

> [!TIP]
> 있는지 toouse hello 최신 버전의 [Power BI Desktop](https://powerbi.microsoft.com/desktop/)합니다.
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Power BI Desktop에서 연결

1. Power BI Desktop에서 **데이터 가져오기** > **Azure** > **Azure Analysis Services 데이터베이스**를 클릭합니다.

2. **서버**, hello 서버 이름을 입력 합니다. 
    
    있는지 tooinclude hello 전체 URL 이어야 합니다. 예를 들어 asazure://westcentralus.asazure.windows.net/advworks 같이 입력합니다.

3. **데이터베이스**hello 테이블 형식 모델 데이터베이스 또는 큐브 뷰를 여기에 붙여넣습니다 tooconnect 원하는 hello 이름을 알고 있는 경우. 그러지 않으면 이 필드를 비워 두고 나중에 데이터베이스 또는 큐브 뷰를 선택합니다.

4. Hello 기본 둡니다 **라이브 연결** 누른 다음 옵션을 **연결**합니다. 

5. 메시지가 표시되면 로그인 자격 증명을 입력합니다. 

6. **탐색기**를 hello 서버를 확장 한 다음 선택 hello 모델 또는 큐브 뷰를 클릭 한 다음 tooconnect 원하는 **연결**합니다. 해당 보기에 대 한 모든 hello 개체 모델 또는 큐브 뷰 tooshow를 클릭 합니다.

    Power BI Desktop에서 보고서 보기에서 빈 보고서와 hello 모델이 열립니다. hello 필드 목록에는 모든 숨겨지지 않은 모델 개체가 표시 됩니다. 연결 상태는 hello 오른쪽 아래 모서리에 표시 됩니다.

## <a name="connect-in-power-bi-service"></a>Power BI(서비스)에서 연결

1. 서버에는 라이브 연결 tooyour 모델이 있는 Power BI Desktop 파일을 만듭니다.
2. [Power BI](https://powerbi.microsoft.com)에서 **데이터 가져오기** > **파일**을 클릭합니다. 파일을 찾아 선택합니다.



## <a name="see-also"></a>참고 항목
[TooAzure Analysis Services 연결](analysis-services-connect.md)   
[클라이언트 라이브러리](analysis-services-data-providers.md)

