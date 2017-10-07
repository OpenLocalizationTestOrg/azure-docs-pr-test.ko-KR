---
title: "분석 데이터 레이크 저장소 출력 aaaStream | Microsoft Docs"
description: "스트림 분석 작업에서 Azure Data Lake 저장소의 인증 및 권한 부여 구성"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a>스트림 분석 Data Lake 저장소 출력
스트림 분석 작업은 여러 출력 메서드를 지원하며 그 중 하나는 [Azure Data Lake 저장소](https://azure.microsoft.com/services/data-lake-store/)입니다. Azure 데이터 레이크 저장소는 빅 데이터 분석 작업을 위한 엔터프라이즈 수준 하이퍼 스케일 리포지토리입니다. 데이터 레이크 저장소를 통해 운영 및 예비 분석에 대 한 원하는 크기, 유형 및 수집 속도의 toostore 데이터입니다.

## <a name="authorize-a-data-lake-store-account"></a>Data Lake 저장소 계정 권한 부여
1. 데이터 레이크 저장소를 hello Azure 포털에서에서 출력으로 선택 하는 경우 메시지가 표시 됩니다 기존 데이터 레이크 저장소 또는 toorequest tooauthorize 사용 hello 클래식 포털을 통해 toohello 데이터 레이크 저장소에 액세스 합니다.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. 이미 있는 경우 tooData 레이크 스토어에 액세스 "권한을 부여" 지금 "을 페이지 짧은 시간에 대 한 팝업 됩니다"리디렉션 tooauthorization "를 나타내는입니다. hello 페이지 자동으로 닫히고 tooconfigure hello Data Lake 저장소 출력은 허용 하는 hello 페이지가 나타납니다.

데이터 레이크 저장소에 대 한 등록 하지 한 hello "등록 지금" 링크 tooinitiate hello 요청을 수행 하거나 수 hello에 따라 [시작된 지침 확인](../data-lake-store/data-lake-store-get-started-portal.md)합니다.

## <a name="configure-hello-data-lake-store-output-properties"></a>Hello 데이터 레이크 저장소 출력 속성 구성
Hello 데이터 레이크 저장소 계정 인증을 사용 하는 후에 데이터 레이크 저장소 출력에 대 한 hello 속성을 구성할 수 있습니다. hello 다음 표에서 hello 목록 속성 이름 및 해당 설명 tooconfigure 데이터 레이크 저장소 출력입니다.

<table>
<tbody>
<tr>
<td><B>속성 이름</B></td>
<td><B>설명</B></td>
</tr>
<tr>
<td>출력 별칭</td>
<td>쿼리 toodirect hello 쿼리 출력 toothis Data Lake 저장소에에서 사용 되는 친숙 한 이름입니다.</td>
</tr>
<tr>
<td>Data Lake 저장소 계정</td>
<td>출력을 보내는 hello 저장소 계정의 hello 이름입니다. 데이터 레이크 저장소 계정에 권한이 hello 로그인 한 사용자 목록이 나타납니다.</td>
</tr>
<tr>
<td>경로 접두사 패턴[<I>선택 사항</I>]</td>
<td>파일에 사용 된 경로 toowrite hello hello 내에서 파일 데이터 레이크 저장소 계정을 지정 합니다. <BR>{date}, {time}<BR>예제 1: folder1/logs/{date}/{time}<BR>예제 2: folder1/logs/{date}</td>
</tr>
<tr>
<td>날짜 형식[<I>선택 사항</I>]</td>
<td>Hello 날짜 토큰이 hello 접두사 경로에 사용 되며, hello 날짜 형식을 사용자 파일 구성할 지를 선택할 수 있습니다. 예: YYYY/MM/DD</td>
</tr>
<tr>
<td>시간 형식[<I>선택 사항</I>]</td>
<td>Hello 시간 토큰이 hello 접두사 경로에 사용 되며, 경우에 파일 구성 됩니다 hello 시간 형식을 지정 합니다. 현재 hello만 지원 점은 HH입니다.</td>
</tr>
<tr>
<td>이벤트 직렬화 형식</td>
<td>출력 데이터에 대한 직렬화 형식입니다. JSON, CSV 및 Avro를 지원합니다.</td>
</tr>
<tr>
<td>인코딩</td>
<td>CSV 또는 JSON 형식인 경우 인코딩을 지정해야 합니다. U t F-8 hello만 현재 지원 인코딩 형식입니다.</td>
</tr>
<tr>
<td>구분 기호</td>
<td>CSV 직렬화에만 적용됩니다. 스트림 분석은 CSV 데이터를 직렬화하기 위해 다양하고 일반적인 구분 기호를 지원합니다. 지원되는 값은 쉼표, 세미콜론, 공백, 탭 및 세로 막대입니다.</td>
</tr>
<tr>
<td>형식</td>
<td>JSON 직렬화에만 적용됩니다. 줄 바꿈을 하 여 지정 hello 출력 각 JSON 개체를 새 줄으로 구분 하 여 형식이 지정 됩니다. 배열 지정 hello 출력 JSON 개체의 배열으로 형식이 지정 됩니다.</td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a>Data Lake 저장소 권한 부여 갱신
현재는 제한 사항에서 인증 토큰 hello 필요한 toobe 수동으로 데이터 레이크 저장소 출력을 제공 하는 모든 작업에 대 한 일 마다 새로 고쳐집니다. Toore 만들어야-업무를 만든 이후 또는 마지막으로 인증 된 암호를 변경한 경우 사용자 데이터 레이크 저장소 계정을 인증 합니다. 이 문제의 증상은 작업 출력 없음 다시 권한 부여에 대 한 필요성을 나타내는 hello 작업 로그에 오류가 있습니다.

tooresolve이이 문제를 실행 중인 작업을 중지 하 고 출력 tooyour 데이터 레이크 저장소로 이동 합니다. Hello "갱신 인증" 링크를 클릭 하 고 페이지 짧은 시간에 대 한 팝업 됩니다 "리디렉션 tooauthorization..."를 나타내는입니다. hello 페이지 자동으로 닫히고 성공 하면 "권한 부여를 갱신 했습니다" 표시 됩니다. 그런 다음 "저장" tooclick hello hello 페이지 맨 아래에 필요 하 고 마지막으로 중지 된 시간 tooavoid 데이터 손실 hello에서 작업을 다시 시작 하 여 계속할 수 있습니다.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

