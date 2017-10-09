---
title: "기계 학습 스튜디오에서 aaaUse hello 샘플 데이터 집합 | Microsoft Docs"
description: "기계 학습 스튜디오에 포함 된 샘플 모델에 사용 하는 hello 데이터 집합의 설명입니다. 실험에 대해 이 샘플 데이터 집합을 사용할 수 있습니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Azure 기계 학습 스튜디오에서 hello 샘플 데이터 집합을 사용 합니다.
[top]: #machine-learning-sample-datasets

Azure Machine Learning에서 새 작업 영역을 만들 때 다양한 샘플 데이터 집합 및 실험이 기본적으로 포함됩니다. Hello에 hello 샘플 모델에서 사용 되는 다양 한 다음 샘플 데이터 집합의 [Azure Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com/)합니다. 나머지는 Machine Learning에서 일반적으로 사용되는 다양한 유형의 데이터 예로 포함됩니다.

일부 데이터 집합은 Azure Blob Storage에서 사용할 수 있습니다. Hello 다음 표에 이러한 데이터 집합에 대 한 링크를 제공 합니다. Hello를 사용 하 여 실험에서 이러한 데이터 집합을 사용할 수 있습니다 [데이터 가져오기] [ import-data] 모듈입니다.

이러한 샘플 데이터 집합의 hello 나머지 부분에서 작업 영역에서 사용할 수 있는 **저장 된 데이터 집합** hello 모듈 색상표 toohello 열거나 기계 학습 스튜디오에서 새 실험을 만들 때 hello 실험 캔버스의 왼쪽에 있습니다.
사용할 수 있습니다 이러한 데이터 집합의 고유한 실험에서 tooyour 실험 캔버스 끌어.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>데이터 집합 이름</th>
  <th align=left>데이터 집합 설명</th>
</tr>

<tr>
  <td valign=top>성인 인구 조사 소득 이진 분류 데이터 집합</td>
  <td valign=top>
조정 된 소득 인덱스 > 100 16 hello 세 작업 성인을 사용 하 여 hello 1994 년 인구 조사 데이터베이스의 하위 집합입니다.<p> </p><b>사용법:</b> 개인 넘는 50k 연간 소득이 여부 toopredict 인구 통계를 사용 하는 사용자를 분류 합니다.<p> </p><b>관련 조사:</b> Kohavi, R., Becker, B., (1996). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>공항 코드 데이터 집합</td>
  <td valign=top>
미국 공항 코드.<p> </p>이 데이터 집합에 각 미국 공항 hello 공항 ID 번호와 hello 위치 city 및 state와 함께 이름을 제공 하는 한 개의 행을 포함 합니다.
  </td>
</tr>

<tr>
  <td valign=top>자동차 가격 데이터(원시)</td>
  <td valign=top>
여 자동차에 대 한 정보 만들고 hello 가격을 비롯 하 여 hello 보험 위험 점수 뿐만 아니라 실린더 MPG, 수 등의 기능 모델링 합니다.<p> </p>hello 위험 점수 자동 가격 처음 연결 되어 있고 tooactuaries symboling로 알려진 프로세스에서 실제 위험에 맞게 조정 합니다. + 3 값 나타내며 hello 자동 하지 않는 것이 값이-3 한다는 해도 안전 합니다.<p> </p><b>사용법:</b> 기능을 회귀 또는 연쇄 분류를 사용 하 여 hello 위험 점수를 예측 합니다. <p> </p><b>관련 조사:</b> Schlimmer, J.C. (1987). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>자전거 임대 UCI 데이터 집합</td>
  <td valign=top>
Washington DC에서 자전거 임대망을 유지 관리하는 Capital Bikeshare 회사의 실제 데이터를 기반으로 하는 UCI 자전거 임대 데이터 집합.<p> </p>hello dataset 2011 및 2012 년의 총 17,379 행에 대 한 각 날짜의 각 시간에 대해 하나의 행을 있습니다. 1 too977에서 자전거 대 여 시간 단위로 hello 범위가입니다.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Bil Gates RGB 이미지</td>
  <td valign=top>
공개적으로 사용할 수 있는 이미지 파일 tooCSV 데이터를 변환 합니다.<p> </p>hello hello 이미지 변환에 대 한 코드에서에서 제공 됩니다 hello <strong>색 양자화 K-means 클러스터링을 사용 하 여</strong> 모델 세부 정보 페이지입니다.
  </td>
</tr>

<tr>
  <td valign=top>헌혈 데이터</td>
  <td valign=top>
Hello 피 Transfusion 서비스 Hsin 센터 추 도시, 대만의 hello 피 헌 혈 자 데이터베이스에서 데이터의 하위 집합입니다.<p> </p>헌 혈 자 데이터가 마지막에 기부 이후 hello 개월)를 포함 하 고 빈도 또는 기부 피의 양과 기부, 마지막 기부 이후 시간 hello 총 수입니다.<p> </p><b>사용법:</b> hello ´ ֲ 분류를 통해 toopredict hello 헌 혈 자 기부 피 1 hello 대상 기간과 0 중 기부자를 의미 하는 2007 년 3 월에에서 기부자 아닌 여부. <p> </p><b>관련 조사:</b> Yeh, I.C., (2008). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence, "Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Amazon의 도서 리뷰</td>
  <td valign=top>
펜실베니아 대학 연구원에 의해 hello amazon.com 웹 사이트에서 가져온 Amazon의 책에 대 한 검토 (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">정서</a>). Hello 연구 논문 참조 "약력, Bollywood, 붐 상자와 Blenders: 감성 분류에 대 한 도메인 적응" John Blitzer, 표시 Dredze 및 김철수 pereira가 제공 합니다. 연결의 계산 Linguistics (ACL) 2007입니다.<p> </p>hello 원래 데이터 집합에 1, 2, 3, 4 또는 5 등급으로 975 K 검토 합니다. hello 검토 기간 1997-2007 hello는 사용 및 영어에 작성 된 것입니다. 이 데이터 집합에는 축소 샘플링 too10K 검토 했습니다.
  </td>
</tr>

<tr>
  <td valign=top>유방암 데이터</td>
  <td valign=top>
세 개의 유방암 관련 데이터 집합 hello 컴퓨터 학습 연구에서 자주 나타나는 Oncology Institute에서 제공 하는 중 하나입니다. 진단 정보를 300여 개 조직 샘플에 대한 실험실 분석의 기능과 결합합니다.<p> </p><b>사용법:</b> hello 유형의 유방암을 분류 하 고, 9 특성에 따라, 일부는 선형, 일부는 범주입니다. <p> </p><b>관련 조사:</b> Wohlberg, W.H., Street, W.N., & Mangasarian, O.L. (1995). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>유방암 기능 <td valign=top>
각 117 기능을 통해 설명의 x-레이 이미지 K 102 의심 스러운 영역 (후보)에 대 한 정보를 포함 하는 hello 데이터 집합입니다. hello 기능 소유 되며 해당 의미 hello 데이터 집합 작성자 (Siemens Healthcare)가 표시 되지 않습니다. 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>유방암 정보</td>
  <td valign=top>
hello 데이터 집합의 x-레이 이미지 각 의심 스러운 영역에 대 한 추가 정보를 포함합니다. 각 예에서는 정보를 제공 합니다 (예: 레이블 환자 ID, 패치 상대 toohello 전체 이미지의 좌표) hello hello Breast 유방암 기능 데이터 집합의 해당 행 번호에 대 한 합니다. 환자별로 많은 예제가 있습니다. 암이 있는 환자의 경우 일부 예제는 양성이고 일부는 음성입니다. 암이 없는 환자의 경우 모든 예제는 음성입니다. hello 데이터 집합에는 K 102 예제가 포함 되어 있습니다. hello 지점의 0.6% 확신 hello dataset 편향 되어, hello 나머지는 음수입니다. hello 데이터 집합 Siemens Healthcare에 의해 사용할 수 있게 되었습니다.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>CRM 욕구 레이블 공유</td>
  <td valign=top>
Hello KDD Cup 2009 고객 관계 예측 챌린지의 레이블 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>CRM 이탈 레이블 공유</td>
  <td valign=top>
Hello KDD Cup 2009 고객 관계 예측 챌린지의 레이블 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>CRM 데이터 집합 공유</td>
  <td valign=top>
이 데이터는 hello KDD Cup 2009 고객 관계 예측 챌린지에서 제공 (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>hello dataset 50k 고객 hello 프랑스어 통신 회사 주황색을에서 포함합니다. 각 고객은 익명으로 처리되는 230개 기능을 가지며, 이 중 190개는 숫자이고 40개는 범주입니다. hello 기능은 매우 드입니다.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>CRM 상향 판매 레이블 공유</td>
  <td valign=top>
Hello KDD Cup 2009 고객 관계 예측 챌린지의 레이블 (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>에너지 효율 회귀 데이터</td>
  <td valign=top>
12가지 건물 형태에 따라 시뮬레이트된 에너지 프로필의 컬렉션입니다. hello 건물 영역, 영역 배포 및 방향과 glazing hello glazing 같은 8 기능을 구분 됩니다.<p> </p><b>사용법:</b> 회귀 또는 분류 toopredict hello 에너지 효율성 등급 기반으로 두 개의 실제 값된 응답 중 하나를 사용 합니다. 다중 클래스 분류에 대 한 hello 응답 변수 toohello 가장 근접 한 정수로 반올림 됩니다. <p> </p><b>관련 조사:</b> Xifara, A. & Tsanas, A. (2012). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>비행 지연 데이터</td>
  <td valign=top>
승객 비행 지정 된 시간에 hello TranStats 데이터 수집의 hello 미국에서에서 가져온 성능 데이터 운항정시성 데이터(<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">정시</a>)<p> </p>hello 데이터 집합 hello 기간 2013 년 4 월 10 월에 설명 합니다. TooAzure 기계 학습 스튜디오에 업로드 하기 전에 hello 데이터 집합은 다음과 같이 처리 되었습니다.<ul><li>hello 데이터 집합은 hello 대륙 미국에에서 필터링 된 toocover 제공 하는 hello 70만 가장 바쁜 공항</li><li>취소된 비행은 15분 초과 지연으로 레이블이 지정되었습니다.</li><li>우회 비행은 필터링되었습니다.</li><li>hello 다음과 같은 열에 나온: 년, 월, DayofMonth, DayOfWeek, 통신 회사, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, 취소 됨</li></ul>
</td>
</tr>

<tr>
  <td valign=top>비행 운항정시성(원시)</td>
  <td valign=top>
2011년 10월부터 미국 내의 비행 도착 및 출발 레코드입니다.<p> </p><b>사용:</b> 비행 지연을 예측합니다. <p> </p><b>관련 조사:</b> US 교통국(Dept. of Transportation) <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>산불 데이터</td>
  <td valign=top>
산불 레코드와 결합된 포르투갈 북동부 지역의 기온 및 습도 지수, 풍속 같은 날씨 데이터를 포함합니다.<p> </p><b>사용법:</b> 여기서 hello 목표는 toopredict hello 구울 포리스트 발생의 영역 어려운 회귀 작업입니다. <p> </p><b>관련 조사:</b> Cortez, P., & Morais, A. (2008). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>[Cortez and Morais, 2007] P. Cortez and A. Morais. 데이터 마이닝 접근법 tooPredict 시계 비행 기상 데이터를 사용 하 여 포리스트 발생 합니다. In J. Neves, M. F. Santos 및 J. Machado Eds. 새로운 동향 인공 Intelligence의 절차에 2007 인공 지능, 12 월 Guimarães, 포르투갈 페이지 512-523의 2007 년-포르투갈어 회의 13 EPIA hello 합니다. APPIA, ISBN-13 978-989-95618-0-9. 제공 위치: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>독일 신용 카드 UCI 데이터 집합</td>
  <td valign=top>
UCI Statlog (독일 신용 카드) 데이터 집합을 hello (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + 독일어 + 신용 + 데이터</a>), hello german.data 파일을 사용 합니다.<p> </p>hello 데이터 집합 분류 사람, 낮음 또는 높음 신용 위험으로 특성의 집합에서 설명 합니다. 각 예제는 개인을 나타냅니다. 20 기능을 숫자와 범주 및 이진 레이블 (hello 신용 위험 값). 높은 신용 위험 항목의 레이블은 2이고, 낮은 신용 위험 항목의 레이블은 1입니다. hello 높음 낮은 위험 예제 misclassifying 비용은 1, 반면 hello 비용으로 낮은 위험 수준이 높은 예제 misclassifying는 5입니다.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>IMDB 영화 제목</td>
  <td valign=top>
hello 데이터 집합에 대 한 정보가 영화 트 윗 Twitter에서에서 평가 된: IMDB 영화 ID, 영화 이름, genre 및 프로덕션 연도입니다. 17 K 영화 hello 데이터 집합에 있습니다. hello 데이터 집합 "S. hello 용지에 도입 된 Dooms, T. De Pessemier 및 L. Martens. MovieTweetings: a Movie Rating Dataset Collected From Twitter. Workshop on Crowdsourcing and Human Computation for Recommender Systems, CrowdRec at RecSys 2013"에서 소개되었습니다.
  </td>
</tr>

<tr>
  <td valign=top>붓꽃 2종 데이터</td>
  <td valign=top>
이 hello 가장 잘 알려진 데이터베이스 toobe hello 패턴 인식 홍보 자료에서 찾을 수입니다. hello 데이터 집합은 비교적 작지만 iris 등 세 가지가에서 꽃잎 측정 50 예가 포함 된 합니다.<p> </p><b>사용법:</b> hello 측정에서 hello iris 유형을 예측 합니다.  <p> </p><b>관련 조사:</b> Fisher, R.A. (1988). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>영화 트윗</td>
  <td valign=top>
hello 데이터 집합은 hello 영화 Tweetings 데이터 집합의 확장된 버전입니다. hello 데이터 집합에는 Twitter에서 잘 구성 된 트 윗에서 추출 된 동영상에 대 한 170 K 등급에 있습니다. 각 인스턴스는 트윗을 나타내며 사용자 ID, IMDB 영화 ID, 등급, 타임 스탬프, 해당 트윗에 대한 즐겨찾기 수, 해당 트윗의 리트윗 수 등과 같은 튜플입니다. hello 데이터 집합으로 제공 된 A. 있다고, S. Dooms, B. Loni 및 D. Tikk 추천 시스템 챌린지 2014에 대 한 합니다.
  </td>
</tr>

<tr>
  <td valign=top>다양한 자동차에 대한 MPG 데이터</td>
  <td valign=top>
이 데이터 집합은 Carnegie Mellon University의 hello StatLib 라이브러리에서 제공 하는 hello 데이터 집합의 약간 수정 된 버전. hello dataset 1983 hello에 사용 된 American 통계 연결 표시 합니다.<p> </p>hello 데이터 나열 되며 갤런당, 마일 수의 다양 한 자동차의 연료 소비 함께 정보 원통형, 엔진 치환, 성능, 총 가중치 및 가속 이러한 hello 수가 됩니다.<p> </p><b>사용:</b> 다중 값 개별 특성 3개 및 연속 특성 5개를 기반으로 연비를 예측합니다. <p> </p><b>관련 조사:</b> StatLib, Carnegie Mellon University, (1993). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr>
  <td valign=top>피마 인디언 당뇨병 이진 분류 데이터 집합</td>
  <td valign=top>
Hello National Institute의 식이 조절 Digestive 및 키 드니 질병 데이터베이스에서 데이터의 하위 집합입니다. hello dataset Pima 인도 특성의 여성 환자에 필터링 된 toofocus 했습니다. hello 데이터 라이프 스타일 요소 뿐만 아니라 혈당 insulin 수준 등의 의료 보험 데이터를 포함합니다.<p> </p><b>사용법:</b> hello 주체 식이 조절 (이진 분류)에 있는지 여부를 예측 합니다. <p> </p><b>관련 조사:</b> Sigillito, V. (1990). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml"</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr>
  <td valign=top>음식점 고객 데이터</td>
  <td valign=top>
인구 통계 및 선호도를 비롯한 고객에 대한 메타데이터 집합입니다.<p> </p><b>사용법:</b> 이 데이터 집합을 사용 하 고 함께에서 다른 두 개의 식당 데이터 집합, tootrain hello 추천 시스템을 테스트 합니다. <p> </p><b>관련 조사:</b> Bache, K. and Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>음식점 기능 데이터</td>
  <td valign=top>
음식점 및 음식 종료, 식사 스타일, 위치 같은 기능에 대한 메타데이터 집합입니다.<p> </p><b>사용법:</b> 이 데이터 집합을 사용 하 고 함께에서 다른 두 개의 식당 데이터 집합, tootrain hello 추천 시스템을 테스트 합니다. <p> </p><b>관련 조사:</b> Bache, K. and Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>음식점 등급</td>
  <td valign=top>
눈금에 0 too2에서 사용자가 toorestaurants에 지정한 등급에 포함 되어 있습니다.<p> </p><b>사용법:</b> 이 데이터 집합을 사용 하 고 함께에서 다른 두 개의 식당 데이터 집합, tootrain hello 추천 시스템을 테스트 합니다. <p> </p><b>관련 조사:</b> Bache, K. and Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>강철 가열 냉각 다중 클래스 데이터 집합</td>
  <td valign=top>
일련의 steel annealing (너비, 두께, 유형의 (코일, 시트, 등) hello 결과 강철 형식 hello 물리적 특성을 가진 평가판에서에서 레코드를 포함 하는이 데이터 집합.<p> </p><b>사용:</b> 두 가지 숫자 클래스 특성인 경도 또는 강도의 하나를 예측합니다. 특성 간의 상관 관계를 분석할 수도 있습니다.<p> </p>강철 등급은 SAE 및 기타 조직에서 정의된 집합 표준을 따릅니다. 특정 '등급' (hello 클래스 변수)을 toounderstand hello 값이 필요 합니다. <p> </p><b>관련 조사:</b> Sterling, D. & Buntine, W. (NA). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>여기에 유용한 가이드 toosteel 등급 155633: <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>망원경 데이터</td>
  <td valign=top>
배경 소음과 함께 고에너지 감마 미립자 폭발에 대한 레코드로서, 두 항목 모두 Monte Carlo 프로세스를 사용하여 시뮬레이트됩니다.<p> </p>hello 시뮬레이션의 hello 의도 한 명확 하 게 기반 대기 Cherenkov 감마 telescopes, hello 원하는 신호 (Cherenkov 전자파 샤워 시설) 사이의 배경 노이즈 (hadronic toodifferentiate 통계 방법을 사용 하 여의 tooimprove hello 정확도 샤워 시설 cosmic 광선 hello 위 대기에 의해 시작)입니다.<p> </p>hello 된 데이터를 전처리 된 toocreate 있는 긴된 클러스터 hello 긴 축이 hello 카메라 센터를 위한 것입니다. (Hillas 매개 변수)이이 타원의 hello 특성 판별에 사용할 수 있는 hello 이미지 매개 변수 중이 합니다.<p> </p><b>사용:</b> 샤워 이미지가 신호 또는 배경 소음을 나타내는지를 예측합니다.<p> </p><b>참고:</b> 배경 이벤트를 신호로 분류하는 것은 신호 이벤트를 배경으로 분류하는 것보다 비효율적이므로 단순 분류 정확도는 이 데이터에 대해 의미가 없습니다. 다른 분류자의 비교에 대 한 hello ROC 그래프를 사용 해야 합니다. 신호 hello 임계값을 다음 중 하나 보다 이루어야 백그라운드 이벤트를 받아들이는 확률 hello: 0.01, 0.02, 0.05, 0.1, 또는 0.2입니다.<p> </p>또한 실제 측정을 hello h 또는 노이즈 클래스는 이벤트의 hello 대부분 나타냅니다 반면는 백그라운드 이벤트 (h, hadronic 샤워 시설에 대 한) hello 수 과소평가, note 합니다. <p> </p><b>관련 조사:</b> Bock, R.K. (1995). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>날씨 데이터 집합</td>
  <td valign=top>
NOAA에서 시간당 날씨 토지 기반 관찰 (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">201304 too201310에서 데이터를 병합</a>).<p> </p>hello 날씨 데이터 관찰 공항 날씨 스테이션을 다루는 hello 기간 2013 년 4 월 10 월에서 설명 합니다. TooAzure 기계 학습 스튜디오에 업로드 하기 전에 hello 데이터 집합은 다음과 같이 처리 되었습니다.<ul><li>날씨 스테이션 Id가 매핑된 toocorresponding 공항 Id</li><li>Hello 70 가장 바쁜 공항 연관 되지 않은 날씨 스테이션 필터링</li><li>hello 날짜 열은 연도, 월 및 일에 대 한 별도 열으로 분할 되었습니다.</li><li>hello 다음과 같은 열에 나온: AirportID, 연도, 월, 일, 시간, 표준 시간대, SkyCondition, 표시 유형, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius RelativeHumidity, WindSpeed, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, Altimeter</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Wikipedia SP 500 데이터 집합</td>
  <td valign=top>
데이터는 XML 데이터로 저장되는 각 S&P 500 회사의 자료에 따라 Wikipedia(<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>)에서 파생됩니다.<p> </p>TooAzure 기계 학습 스튜디오에 업로드 하기 전에 hello 데이터 집합은 다음과 같이 처리 되었습니다.<ul><li>각 특정 회사에 대한 텍스트 콘텐츠 추출</li><li>위치 형식 지정 제거</li><li>영숫자가 아닌 문자 제거</li><li>모든 텍스트 toolowercase 변환</li><li>알려진 회사 범주가 추가됨</li></ul><p> </p>Hello 레코드 수가 500 보다 작으면 이므로 일부 회사에 대 한 아티클을 찾을 수 없습니다, note 합니다.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
고객 데이터와 해당 응답 tooa 직접 메일링 캠페인에 대 한 표시가 hello 데이터 집합에 포함 되어 있습니다. 각 행은 고객을 나타냅니다. hello 데이터 집합에 과거 동작 및 레이블 열 3 및 사용자 통계에 대 한 9 기능 (방문 하 고, 변환 및 지출).  방문은 hello 마케팅 캠페인을 변환 이미, 고객 구매 했음을 나타내고 지출 후를 방문한 고객 소요 된 hello 크기 임을 나타내는 이진 열입니다.  hello 데이터 집합으로 제공 된 Kevin Hillstrom MineThatData 전자 메일 분석 및 데이터 마이닝 문제에 대 한 여 합니다.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
테스트 예제 hello RCV1 V2 Reuters 뉴스 데이터 집합에서의 기능입니다. hello 데이터 집합에 해당 Id와 함께 781 K 뉴스 기사 (hello 데이터 집합의 첫 번째 열)입니다. 각 기사는 토큰화, 중지 단어 지정, 형태소 분석됩니다. hello 데이터 집합 David에 의해 사용할 수 있게 되었습니다. D. Lewis가 제공했습니다.
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
학습 예제 hello RCV1 V2 Reuters 뉴스 데이터 집합의 기능입니다. hello 데이터 집합에 해당 Id와 함께 23 K 뉴스 기사 (hello 데이터 집합의 첫 번째 열)입니다. 각 기사는 토큰화, 중지 단어 지정, 형태소 분석됩니다. hello 데이터 집합 David에 의해 사용할 수 있게 되었습니다. D. Lewis가 제공했습니다.
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
Hello KDD Cup 1999 기술 자료 검색에서에서 데이터 집합 및 데이터 마이닝 도구 경쟁 (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>hello 데이터 집합 다운로드 되어 Azure Blob 저장소에 저장 되었습니다 (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) 학습 및 테스트 데이터 집합을 포함 합니다. hello 학습 데이터 집합에 약 126 K 행 / hello 레이블을 포함 하는 43 열이 있습니다. 세 개의 열 hello 레이블 정보의 일부 있고 40 개의 열, 숫자 및 문자열/범주 기능으로 구성 된 hello 모델 학습에 사용할 수 있는 합니다. hello 테스트 데이터에 약 22.5 K hello 학습 데이터와 같이 동일한 43 hello 열이 있는 예제를 테스트 합니다.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></td>
  <td valign=top>
Hello RCV1 V2 Reuters 뉴스 데이터 집합에 대 한 뉴스 기사에 대 한 항목 할당 합니다. 뉴스 기사 tooseveral 항목을 할당할 수 있습니다. 각 행의 hello 형식은 "&lt;주제 이름&gt; &lt;문서 id&gt; 1". hello dataset 2.6 M 항목 할당을 포함합니다. hello 데이터 집합 David에 의해 사용할 수 있게 되었습니다. D. Lewis가 제공했습니다.
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
이 데이터는 hello KDD Cup 2010 학생 성능 평가 챌린지에서에서 제공 (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">학생 성능 평가</a>). hello 사용 되는 데이터는 hello Algebra_2008_2009 학습 집합 (스탬퍼, J., Niculescu Mizil A., Ritter, S. Gordon, G.J., & Koedinger, K.R. (2010)입니다. Algebra I 2008-2009. KDD Cup 2010 교육 데이터 마이닝 챌린지의 챌린지 데이터 집합. <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> 또는 <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>에서 찾아보세요.<p> </p>hello 데이터 집합 다운로드 되어 Azure Blob 저장소에 저장 되었습니다 (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) 시스템 개인 지도 학생에서 로그 파일을 포함 합니다. 문제 ID와 학생 ID, 타임 스탬프, 간략 한 설명을 제공 하는 hello 기능은 및 시도 hello에 hello 문제를 해결 하기 전에 hello 학생 수 올바른 방법입니다. hello 원래 데이터 집합에 8.9 M 레코드가; 이 데이터 집합은 처음 100, 000 행을 축소 샘플링 toohello 되었습니다. hello 데이터 집합에 다양 한 형식의 23 탭으로 구분 된 열: 범주, 숫자 및 타임 스탬프입니다.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
