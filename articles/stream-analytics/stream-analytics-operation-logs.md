---
title: "스트림 분석에서 작업 및 서비스 로그를 사용 하 여 aaaDebug | Microsoft Docs"
description: "방법 toouse 스트림 분석 작업 로그"
keywords: "서비스 로그"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>서비스 및 작업 로그를 사용하여 Stream Analytics 작업 디버그
모든 Azure 서비스 공급 operational 로깅 메시지 toousers toorecord 정보 관련 toomanagement 작업 합니다. Azure 스트림 분석에서이 정보 디버깅 시작 tooprocessing toooutput에서 시간에 따라 작업 상태, 작업 진행률 및 작업의 오류 메시지 tootrack hello 진행률을 보는 등의 목적으로 사용할 수 있습니다.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Hello Azure 관리 포털에서 작업 로그 찾기
작업 로그는 다음 두 가지 방법으로 액세스할 수 있습니다.  

* Hello 스트림 분석 작업의 대시보드  
* Hello Azure 클래식 포털에서 관리 서비스  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Hello 스트림 분석 작업의 대시보드
스트림 분석 작업의 로그에 해당 하는 링크 toohello hello 작업의 대시보드 탭에 표시 됩니다. 이 링크를 누르면 해당 특정 작업에 대 한 최신 로그를 표시 하는 방식에서 hello 필터를 설정 합니다.

  ![관리 서비스 로그 선택](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>관리 서비스
toomanually는 스트림 분석 및 hello Azure 클래식 포털의 다른 서비스에 대 한 toohello 작업 로그를 이동 합니다.

1. 클릭 **관리 서비스** hello에 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 선택 **스트림 분석** 에 대 한 **형식** hello에 대 한 hello 작업 이름 및 **서비스 이름**합니다.  
   
   ![Stream Analytics 선택](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Hello Azure 포털에서에서 감사 로그 찾기
hello Azure 포털에서에서 스트림 분석 작업에 대 한 작업 로그 toofind 클릭 **찾아보기** 선택한 후 **감사 로그**합니다.

  ![Azure Portal 선택 Stream Analytics](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

이 구독에서 모든 리소스에 대 한 최근 7 일 동안 이벤트 hello에서 보여 주는 블레이드가 열립니다.  Hello를 클릭 하 여 형식 지정 또는 시간 프레임 toosee 이벤트를 필터링 할 수 있습니다 **필터** 명령입니다.

  ![Azure Portal 선택 Stream Analytics](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>로그 세부 정보 가져오기
작업에 대 한 시간 범위 및 상태 tooview hello 로그도 필터링 할 수 있습니다.

Hello hello Azure 관리 포털에서 클릭 **세부 정보** hello 창 tooview hello 맨 아래에 선택한 이벤트에 대 한 자세한 내용은 단추입니다. 

  ![세부 정보 선택](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

Hello Azure 포털에서 로그 항목 toosee 클릭 그 안에 자세한 이벤트를 hello 합니다.

  ![Azure Portal 선택 세부 정보](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

여기에서 hello를 열 수 있습니다 **세부** 블레이드 hello 이벤트를 클릭 하 여 합니다.

  ![Azure Portal 선택 세부 정보](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>실패한 작업 디버그
Hello Azure 관리 포털을 hello 검색 아이콘을 클릭 하 고 '실패' 입력 합니다. 오류가 있는 모든 로그의 결과가 제공됩니다. 

  ![실패한 작업 디버그](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

Azure 포털 hello 메시지 tooview 수준별로 필터링 할 수 있습니다 **위험** 이벤트입니다.

  ![Azure Portal 디버그](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

Hello 오류 중 하나를 선택 하 고 hello 클릭 **세부 정보** hello 오류에 대 한 자세한 내용은 합니다.  일부 오류 메시지는 또한 toomitigate 문제 hello 하는 방법에 대 한 정보를 제공 합니다. 

  ![작업 세부 정보](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

Toocontact이 필요할 경우 [지원](https://azure.microsoft.com/support/options/) hello 통해 toohello 팀 정보를 제공 하거나 [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), 특히 hello hello 작업 세부 정보를 참고 **상관 관계 ID**. 

## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

