---
title: "Stream Analytics: 입력 및 출력에 대한 로그인 자격 증명 회전 | Microsoft Docs"
description: "Tooupdate hello 스트림 분석 입 / 출력에 대 한 자격 증명 하는 방법에 대해 알아봅니다."
keywords: "로그인 자격 증명"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>스트림 분석 작업에서 입력 및 출력을 위한 로그인 자격 증명 회전
## <a name="abstract"></a>요약
오늘날 azure 스트림 분석 hello 작업이 실행 되는 동안 입력/출력에서 hello 자격 증명을 교체 허용 하지 않습니다.

Azure 스트림 분석에서 마지막으로 출력에서 작업을 다시 시작을 지원 하는 동안 싶었기 tooshare hello 전체 프로세스 중지 hello 및 hello 작업의 시작 및 로그인 자격 증명 hello 회전 사이의 hello 지연을 최소화 합니다.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>1 부-hello 새로운 자격 증명 집합을 준비 합니다.
이 부분은 입/출력 다음 적용 가능한 toohello:

* Blob 저장소
* 이벤트 허브(영문)
* SQL 데이터베이스
* 테이블 저장소

다른 입력/출력의 경우 2부를 진행합니다.

### <a name="blob-storagetable-storage"></a>Blob 저장소/테이블 저장소
1. Hello Azure 관리 포털에서 toohello 저장소 확장명을 이동 합니다.  
   ![graphic1][graphic1]
2. 작업에서 사용 하는 hello 저장소 찾아서 것으로 이동 합니다.  
   ![graphic2][graphic2]
3. Hello 액세스 키 관리 명령을 클릭 합니다.  
   ![graphic3][graphic3]
4. Hello 기본 액세스 키 및 보조 액세스 키를 hello 사이의 **선택 하지 작업에서 사용 하는 hello**합니다.
5. 히트 다시 생성:   
   ![graphic4][graphic4]
6. Hello 새로 생성 된 키를 복사 합니다.  
   ![graphic5][graphic5]
7. TooPart 2를 계속 합니다.

### <a name="event-hubs"></a>이벤트 허브(영문)
1. 서비스 버스 확장 toohello hello Azure 관리 포털에서 이동 합니다.  
   ![graphic6][graphic6]
2. 작업에서 사용 하는 서비스 버스 Namespace hello 찾아서 것으로 이동 합니다.  
   ![graphic7][graphic7]
3. 작업에서 서비스 버스 Namespace hello에 대해 공유 액세스 정책, 점프 toostep 6  
4. Toohello 이벤트 허브 탭으로 이동 합니다.  
   ![graphic8][graphic8]
5. 작업에서 사용 하는 이벤트 허브 hello 찾아서 것으로 이동 합니다.  
   ![graphic9][graphic9]
6. Toohello 구성 탭 이동 합니다.  
   ![graphic10][graphic10]
7. Hello 정책 이름 드롭다운 목록, 작업에서 사용 하는 hello 공유 액세스 정책을 찾습니다.  
   ![graphic11][graphic11]
8. Hello 기본 키와 보조 키 hello 사이의 **선택 하지 작업에서 사용 하는 hello**합니다.  
9. 히트 다시 생성:   
   ![graphic12][graphic12]
10. Hello 새로 생성 된 키를 복사 합니다.  
   ![graphic13][graphic13]
11. TooPart 2를 계속 합니다.  

### <a name="sql-database"></a>SQL 데이터베이스
> [!NOTE]
> 참고: tooconnect toohello SQL 데이터베이스 서비스를 필요 합니다. 하겠습니다 tooshow toodo 사용 하 여이에 관리 경험을 hello 방법 hello Azure 관리 포털 하지만 일부 클라이언트 쪽 도구 등 SQL Server Management Studio와 함께 toouse를 선택할 수 있습니다.
>
> 

1. SQL 데이터베이스 확장 toohello hello Azure 관리 포털에서 이동 합니다.  
   ![graphic14][graphic14]
2. 찾기 작업에서 사용 하는 SQL 데이터베이스 hello 및 **hello 서버를 클릭** hello에 동일한 연결 줄:  
   ![graphic15][graphic15]
3. Hello 관리 명령을 클릭 합니다.  
   ![graphic16][graphic16]
4. 데이터베이스 마스터 유형:   
   ![graphic17][graphic17]
5. 사용자 이름, 암호를 입력하고 로그를 클릭합니다.  
   ![graphic18][graphic18]
6. 새 쿼리를 클릭합니다.  
   ![graphic19][graphic19]
7. Hello 바꾸고 사용자 이름으로 쿼리 교체 < login_name > 뒤에 형식 <enterStrongPasswordHere> 새 암호를 사용 합니다.  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. 실행을 클릭합니다.  
   ![graphic20][graphic20]
9. Toostep 2 돌아가서이 이번 hello 데이터베이스를 클릭 합니다.  
   ![graphic21][graphic21]
10. Hello 관리 명령을 클릭 합니다.  
   ![graphic22][graphic22]
11. 사용자 이름, 암호를 입력하고 로그를 클릭합니다.  
   ![graphic23][graphic23]
12. 새 쿼리를 클릭합니다.  
   ![graphic24][graphic24]
13. 이 로그인이이 데이터베이스의 hello 컨텍스트에서 hello tooidentify 기준이 될 이름으로 쿼리 교체 사용자 < _ > 뒤에 입력 (제공할 수 있습니다 < login_name >에 대 한 예를 들어 지정한 동일한 값을 hello)와 < login_name >로 대체 새 사용자 이름:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. 실행을 클릭합니다.  
   ![graphic25][graphic25]
15. Hello로 이제 새 사용자를 제공 해야 역할과 같은 역할 및 사용 하면 원래 사용자에 게 권한.
16. TooPart 2를 계속 합니다.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>2 부: Stopping hello 스트림 분석 작업
1. Hello Azure 관리 포털에서 toohello 스트림 분석 확장 프로그램을 이동 합니다.  
   ![graphic26][graphic26]
2. 작업을 찾아 이동합니다.  
   ![graphic27][graphic27]
3. Toohello 입력 탭 이나 hello 자격 증명에 대 한 입력 또는 출력에서 회전 하는지 여부에 따라 hello 출력 탭 이동 합니다.  
   ![graphic28][graphic28]
4. Hello 중지 명령을 클릭 하 고 hello 작업이 중지 되었습니다 확인 합니다.  
   ![graphic29][graphic29] hello 작업 toostop 때까지 대기 합니다.
5. 찾을 hello 입/출력 원하는 toorotate 자격 증명 on 및 이동 넣습니다.  
   ![graphic30][graphic30]
6. TooPart 3을 진행 합니다.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>3 부: hello 스트림 분석 작업 시 hello 자격 편집
### <a name="blob-storagetable-storage"></a>Blob 저장소/테이블 저장소
1. Hello 저장소 계정 키 필드를 찾아 새로 생성 된 키를 붙여 넣습니다.  
   ![graphic31][graphic31]
2. Hello 저장 명령을 클릭 하 고 변경 내용을 저장을 확인 합니다.  
   ![graphic32][graphic32]
3. 변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.
4. TooPart 4를 진행 합니다.

### <a name="event-hubs"></a>이벤트 허브(영문)
1. Hello 이벤트 허브 정책 키 필드를 찾아 새로 생성 된 키를 붙여 넣습니다.  
   ![graphic33][graphic33]
2. Hello 저장 명령을 클릭 하 고 변경 내용을 저장을 확인 합니다.  
   ![graphic34][graphic34]
3. 변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.
4. TooPart 4를 진행 합니다.

### <a name="power-bi"></a>Power BI
1. Hello 갱신 권한 부여를 클릭 합니다.  

   ![graphic35][graphic35]
2. 확인을 수행 하는 hello를 발생 합니다.  

   ![graphic36][graphic36]
3. Hello 저장 명령을 클릭 하 고 변경 내용을 저장을 확인 합니다.  
   ![graphic37][graphic37]
4. 변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.
5. TooPart 4를 진행 합니다.

### <a name="sql-database"></a>SQL 데이터베이스
1. Hello 사용자 이름 및 암호 필드를 찾아 새로 만든된 자격 증명 집합을 수용 여부에.  
   ![graphic38][graphic38]
2. Hello 저장 명령을 클릭 하 고 변경 내용을 저장을 확인 합니다.  
   ![graphic39][graphic39]
3. 변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.  
4. TooPart 4를 진행 합니다.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>4부: 마지막 중지된 시간에서 해당 작업 시작
1. 입/출력 hello를 나 가려고 합니다.  
   ![graphic40][graphic40]
2. Hello 시작 명령을 클릭 합니다.  
   ![graphic41][graphic41]
3. Hello 마지막으로 중지 된 시간을 선택 하 고 확인을 클릭 합니다.  
   ![graphic42][graphic42]
4. TooPart 5를 진행 합니다.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>5 단계: 제거 hello 이전 자격 증명 집합
이 부분은 입/출력 다음 적용 가능한 toohello:

* Blob 저장소
* 이벤트 허브(영문)
* SQL 데이터베이스
* 테이블 저장소

### <a name="blob-storagetable-storage"></a>Blob 저장소/테이블 저장소
1 부 hello 작업에서 이전에 사용한 선택 키에 대 한 반복 toorenew hello 이제 사용 되지 않은 액세스 키입니다.

### <a name="event-hubs"></a>이벤트 허브(영문)
1 부 hello 작업에서 이전에 사용한 키에 대 한 반복 toorenew hello 이제 사용 되지 않는 키입니다.

### <a name="sql-database"></a>SQL 데이터베이스
1. Toohello 쿼리 창에 다음 쿼리, 작업에서 이전에 사용한 사용자 이름 hello로 < previous_login_name > 대체 hello 유형과 파트 1에서 7 단계에서 다시 이동 합니다.  
   `DROP LOGIN <previous_login_name>`  
2. 실행을 클릭합니다.  
   ![graphic43][graphic43]  

Hello를 다음 확인을 받습니다. 

    Command(s) completed successfully.

## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

