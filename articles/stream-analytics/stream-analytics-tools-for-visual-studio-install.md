---
title: "Visual Studio용 Azure Stream Analytics 도구의 설치 지침 | Microsoft Docs"
description: "Visual Studio용 Azure Stream Analytics 도구의 설치 지침"
keywords: Visual Studio
documentationcenter: 
services: stream-analytics
author: su-jie
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 9/19/2017
ms.author: sujie
ms.openlocfilehash: 307270a25545a0388e67c37656057f81535d8d3b
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="installation-instructions-for-stream-analytics-tools-for-visual-studio"></a>Visual Studio용 Stream Analytics 도구의 설치 지침
Azure Stream Analytics 도구는 이제 Visual Studio 2017, 2015 및 2013을 지원합니다. 이 문서에서는 이러한 도구를 설치 및 제거하는 방법을 소개합니다.

[Visual Studio용 Stream Analytics 도구](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-tools-for-visual-studio)를 사용하는 방법을 알아보세요.

## <a name="install"></a>설치
### <a name="visual-studio-2017"></a>Visual Studio 2017
* [Visual Studio 2017(15.3 이상)](https://www.visualstudio.com/)을 다운로드합니다. Enterprise(Ultimate/Premium), Professional 및 Community Edition이 지원됩니다. Express Edition은 지원되지 않습니다. 
* Stream Analytics 도구는 Visual Studio 2017에서 **Azure 개발**과 **데이터 저장 및 처리** 워크로드의 일부입니다. Visual Studio 설치의 일부로 이러한 두 워크로드 중 하나를 사용하도록 설정합니다.

다음과 같이 **데이터 저장 및 처리** 워크로드를 사용하도록 설정합니다.

![데이터 저장 및 처리 워크로드](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-2017-install-01.png)

다음과 같이 **Azure 개발** 워크로드를 사용하도록 설정합니다.

![Azure 개발 워크로드](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-2017-install-02.png)


### <a name="visual-studio-2013-2015"></a>Visual Studio 2013, 2015
* Visual Studio 2015 또는 Visual Studio 2013 업데이트 4를 설치합니다. Enterprise(Ultimate/Premium), Professional 및 Community Edition이 지원됩니다. Express Edition은 지원되지 않습니다. 
* [웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)를 사용하여 .NET용 Microsoft Azure SDK 버전 2.7.1 이상을 설치합니다.
* [Azure Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs)를 설치합니다.



## <a name="update"></a>업데이트

### <a name="visual-studio-2017"></a>Visual Studio 2017
Visual Studio 알림 영역에 새 버전 미리 알림이 표시됩니다. 

### <a name="visual-studio-2013-2015"></a>Visual Studio 2013, 2015
설치된 Visual Studio용 Stream Analytics 도구는 새 버전을 자동으로 확인합니다. 팝업 창의 지침에 따라 최신 버전을 설치합니다. 


## <a name="uninstall"></a>제거

### <a name="visual-studio-2017"></a>Visual Studio 2017
Visual Studio 설치 관리자를 두 번 클릭하고 **수정**을 선택합니다. **데이터 저장 및 처리** 워크로드 또는 **Azure 개발** 워크로드에서 **Azure Data Lake 및 Stream Analytics 도구** 확인란을 선택 취소합니다.

### <a name="visual-studio-2013-2015"></a>Visual Studio 2013, 2015
[제어판]으로 이동하고 **Microsoft Azure Data Lake 및 Visual Studio용 Stream Analytics 도구**를 제거합니다.





