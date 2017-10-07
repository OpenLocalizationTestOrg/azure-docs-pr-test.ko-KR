---
제목: aaa "3 Azure Analysis Services 자습서 단원: 날짜 테이블로 표시 | Microsoft Docs "설명: 방법을 toomark 날짜 테이블에 hello Azure Analysis Services tutorial 프로젝트에 설명 합니다. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-3-mark-as-date-table"></a>단원 3: 날짜 테이블로 표시

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

2단원: 데이터 가져오기에서는 이름이 DimDate인 차원 테이블을 가져왔습니다. 모델에서 이 테이블의 이름은 DimDate이지만 날짜 및 시간 데이터가 포함되어 있으므로 *날짜 테이블*이라고도 합니다.  
  
DAX 시간 인텔리전스 함수를 사용할 때마다, 나중에 측정값을 만들 때와 같이 *날짜 테이블* 및 해당 테이블에 고유 식별자 *날짜 열*을 포함하는 속성을 지정해야 합니다.
  
Hello DimDate 테이블 hello로 표시 하면이 단원에서는 *날짜 테이블* hello 날짜 열 hello 날짜 테이블에 hello로 *날짜 열* (고유 식별자)입니다.  

Hello 날짜 테이블 및 날짜 열을 표시 하기 전에 모델 보다 쉽게 toounderstand toomake를 약간 à 좋은 시간 toodo 됩니다. Hello DimDate 테이블에서 명명 된 열을 알 **FullDateAlternateKey**합니다. 이 열 hello 테이블에 포함 된 각 달력 연도의 모든 날에 대 한 하나의 행을 포함 합니다. 측정 수식 및 보고서에서 이 열을 많이 사용합니다. 하지만 실제로 FullDateAlternateKey는 이 열에 대한 적절한 식별자가 아닙니다. 너무 바꾸면**날짜**만들고 쉽게 tooidentify 하 수식에 포함 합니다. 가능 하면 항상 좋습니다 toorename는 개체 테이블 및 열 toomake 같은으로 SSDT 및 Power BI 및 Excel 같은 응용 프로그램을 보고 클라이언트에 보다 쉽게 tooidentify 합니다. 
  
이 단원에서는 시간 toocomplete 예상: **3 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [2 단원: 데이터 가져오기](../tutorials/aas-lesson-2-get-data.md)합니다. 

### <a name="toorename-hello-fulldatealternatekey-column"></a>toorename hello FullDateAlternateKey 열

1.  Hello 모델 디자이너에서 클릭 hello **DimDate** 테이블입니다.

2.  Hello에 대 한 hello 헤더를 두 번 클릭 **FullDateAlternateKey** 열을 선택한 다음 너무 이름을**날짜**합니다.

  
### <a name="tooset-mark-as-date-table"></a>tooset 날짜 테이블로 표시  
  
1.  선택 hello **날짜** 열을 선택한 다음 hello **속성** 창 아래에서 **데이터 형식**, 있는지 확인 **날짜** 을 선택 합니다.  
  
2.  Hello 클릭 **테이블** 메뉴를 클릭 한 다음 **날짜**, 클릭 하 고 **날짜 테이블로 표시**합니다.  
  
3.  Hello에 **날짜 테이블로 표시** 대화 상자의 hello **날짜** 목록 상자에서 선택 hello **날짜** hello 고유 식별자 열입니다. 보통은 기본적으로 선택되어 있습니다. **확인**을 클릭합니다. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>다음 작업
[단원 4: 관계 만들기](../tutorials/aas-lesson-4-create-relationships.md)
  
