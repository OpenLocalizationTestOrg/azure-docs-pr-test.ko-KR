---
title: "Azure Cosmos DB 커넥터에 대 한 aaaPower BI 자습서 | Microsoft Docs"
description: "이 Power BI 자습서 tooimport JSON을 사용 하 고, 통찰력 있는 보고서를 만들 하 고 및 hello Azure Cosmos DB와 Power BI 커넥터를 사용 하 여 데이터를 시각화 합니다."
keywords: "power bi 자습서, 데이터 시각화, power bi 커넥터"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Azure Cosmos DB에 대 한 power BI 자습서: Power BI 커넥터 hello를 사용 하 여 데이터 시각화
[PowerBI.com](https://powerbi.microsoft.com/) 은 온라인 서비스 만들기 및 중요 한 tooyou 및 조직 된 데이터로 대시보드 및 보고서를 공유할 수 있습니다.  Power BI Desktop에는 전용 제작 도구를 사용 하면입니다 tooretrieve에서에서 보고서 데이터를 다양 한 데이터 원본, 병합 및 hello 데이터 변환, 강력한 보고서 및 시각화를 만들고 게시 hello 보고서 tooPower BI은 합니다.  Hello Power BI Desktop의 최신 버전으로 Power BI에 대 한 hello Cosmos DB 커넥터를 통해 tooyour Cosmos DB 계정 이제 연결할 수 있습니다.   

이 Power BI 자습서 hello 단계 tooconnect tooa Cosmos DB 계정 Power BI Desktop의 과정을 안내 했습니다,이 tooa 컬렉션 변환 JSON 데이터를 Power BI Desktop 쿼리를 사용 하 여 테이블 형식으로 탐색 창의 hello를 사용 하 여 tooextract hello 데이터를 원하는 위치로 이동 편집기 및 작성 하 고 보고서 tooPowerBI.com 게시 합니다.

이 Power BI 자습서를 완료 하면 다음 질문 수 tooanswer hello 수 있습니다.  

* Power BI Desktop을 사용하여 Cosmos DB의 데이터로 보고서를 빌드하는 방법
* Power BI Desktop에서 tooa Cosmos DB 계정은 어떻게 연결할 수 있습니까?
* Power BI 데스크톱의 컬렉션에서 데이터를 검색하는 방법
* Power BI 데스크톱에서 중첩된 JSON 데이터를 변환하는 방법
* PowerBI.com에서 내 보고서를 게시 및 공유하는 방법

> [!NOTE]
> Cosmos DB Azure 용 hello Power BI 커넥터 추출 및 데이터 변환에 대 한 BI Desktop tooPower 연결합니다. Power BI Desktop에서 만든 보고서 게시 tooPowerBI.com 될 수 있습니다. Azure Cosmos DB 데이터의 직접 추출 및 변환은 PowerBI.com에서 수행할 수 없습니다. 

## <a name="prerequisites"></a>필수 조건
이 Power BI 자습서 hello 지침을 수행 하기 전에 다음 리소스 액세스 toohello 있는지를 확인 합니다.

* [Power BI Desktop의 최신 버전 hello](https://powerbi.microsoft.com/desktop)합니다.
* 액세스 tooour 데모 계정 또는 Cosmos DB 계정의 데이터입니다.
  * hello 데모 계정이이 자습서의 예제는 hello 화산 데이터로 채워집니다. 이 데모 계정은 SLA와 연결되지 않으며 데모용으로만 의미가 있습니다.  Hello 오른쪽 toomake 수정 toothis 데모 계정을 포함 하는 예약 되어있습니다 하지만 변경, 액세스를 제한 하는 hello 키를 변경 하는 계정이 hello 및 이유 또는 사전 통지 없이 언제 든 지 hello 데이터를 delete 종료에 제한 되지 않습니다.
    * URL: https://analytics.documents.azure.com
    * 읽기 전용 키: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==
  * 또는 toocreate 사용자 고유의 계정 참조 [hello Azure 포털을 사용 하 여 Azure Cosmos DB 데이터베이스 계정 만들기](https://azure.microsoft.com/documentation/articles/create-account/)합니다. 그런 다음 tooget 샘플 화산 데이터 비슷한 toowhat는이 자습서에 사용 (hello GeoJSON 블록을 포함 하지 않는) 참조 하십시오 hello [NOAA 사이트](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) 다음 hello를 사용 하 여 hello 데이터를 가져올 [Azure Cosmos DB 데이터 마이그레이션 도구](import-data.md)합니다.

tooshare 보고서를 PowerBI.com에서 PowerBI.com에서 계정이 있어야 합니다.  Power BI 무료 및 Power BI Pro에 대 한 자세한 정보는 toolearn 방문 [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing)합니다.

## <a name="lets-get-started"></a>이제 시작하겠습니다.
이 자습서에서는 화산 hello 전 세계의 내용을 파악 geologist 한다고 가정해 보겠습니다.  hello 화산 데이터 Cosmos DB 계정에 저장 됩니다 및 샘플 문서 다음 hello 같이 hello JSON 문서를 표시 합니다.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

원하는 tooretrieve hello 화산 데이터 hello Cosmos DB에서에서 계정 및 보고서를 수행 하는 hello와 같은 대화형 Power BI 보고서에서 데이터를 시각화 합니다.

![Hello Power BI 커넥터와 함께이 Power BI 자습서를 완료 하 여 Power BI Desktop 화산 보고서 hello 사용 하 여 수 toovisualize 데이터 됩니다.](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

준비 toogive 시도? 이제 시작하겠습니다.

1. 워크스테이션에서 Power BI 데스크톱을 실행합니다.
2. Power BI 데스크톱이 시작되면 *시작* 화면이 표시됩니다.
   
    ![Power BI 데스크톱 시작 화면 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. 할 수 있습니다 **데이터 가져오기**, 참조 **최근 소스**, 또는 **다른 보고서 열기** hello에서 직접 *시작* 화면입니다.  Hello 오른쪽 위 모서리 tooclose hello 화면에 hello X를 클릭 합니다. hello **보고서** Power BI Desktop의 뷰가 표시 됩니다.
   
    ![Power BI 데스크톱 보고서 보기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. 선택 hello **홈** 리본을 클릭 한 다음 **데이터 가져오기**합니다.  hello **데이터 가져오기** 창이 표시 되어야 합니다.
5. **Azure**를 클릭하고 **Microsoft Azure DocumentDB(베타)**를 클릭한 다음 **연결**을 클릭합니다. 

    ![Power BI 데스크톱 데이터 가져오기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. Hello에 **미리 보기 커넥터** 페이지 **계속**합니다. hello **Microsoft Azure DocumentDB Connect** 창이 나타납니다.
7. Tooretrieve hello 데이터를 아래와 같이 선택한 다음 클릭 hello Cosmos DB 계정 끝점 URL 지정 **확인**합니다. toouse 사용자 고유의 계정 hello hello URI에서에서 URL 상자 hello에 검색할 수 있습니다  **[키](manage-account.md#keys)**  블레이드 hello Azure 포털의. toouse hello 계정 데모, 입력 `https://analytics.documents.azure.com` hello URL에 대 한 합니다. 
   
    비워 hello 데이터베이스 이름, 컬렉션 이름 및 SQL 문 처럼 이러한 필드는 선택 사항.  대신, hello 탐색기 tooselect hello 데이터베이스 및 컬렉션 tooidentify hello 데이터에서 제공 하는 위치를 사용 합니다.
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 데스크톱 연결 창](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. 을 연결 하는 hello에 대 한 toothis 끝점 처음으로 hello 계정 키에 대 한 메시지가 표시 됩니다. 사용자 고유의 계정에 대 한 hello에서 hello 키 검색 **기본 키** 상자 hello에  **[읽기 전용 키](manage-account.md#keys)**  블레이드 hello Azure 포털의. Hello 데모 계정에 대 한 hello 키는 `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`합니다. Hello 적절 한 키를 입력 한 다음 클릭 **연결**합니다.
   
    보고서를 작성할 때 hello 읽기 전용 키를 사용 하는 것이 좋습니다.  이렇게 하면 hello 마스터 키 toopotential 보안 위험의 불필요 하 게 노출이 되지 것입니다. hello 읽기 전용 키가 hello에서 사용할 수 있는 [키](manage-account.md#keys) hello Azure 포털의 블레이드 위에 제공 된 hello 데모 계정 정보를 사용할 수 있습니다.
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 계정 키](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > 오류가 발생할 경우 "hello 지정 된 데이터베이스를 찾을 수 없습니다." hello 해결 방법은이 단계를 참조 [Power BI 문제](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200)합니다.
    
9. Hello 계정을 성공적으로 연결 되 면 hello **탐색기** 표시 됩니다.  hello **탐색기** hello 계정에서 데이터베이스 목록이 표시 됩니다.
10. 클릭 하 고 여기서 hello 데이터 hello 데모 계정을 사용 하 여 hello 보고서에서 옵니다에 대 한 선택 hello 데이터베이스에서 확장 **volcanodb**합니다.   
11. 이제 있습니다 hello 데이터를 검색 하는 컬렉션을 선택 합니다. 데모 계정 hello를 사용 하는 경우 선택 **volcano1**합니다.
    
    hello 미리 보기 창에는 목록이 표시 **레코드** 항목입니다.  문서는 Power BI에서 **레코드** 형식으로 나타납니다. 마찬가지로, 문서 내의 중첩된 JSON 블록도 **레코드**입니다.
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 탐색기 창](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. 클릭 **편집** toolaunch hello 쿼리 편집기에서 새 창 tootransform hello 데이터입니다.

## <a name="flattening-and-transforming-json-documents"></a>JSON 문서 평면화 및 변환
1. 여기서 hello toohello Power BI 쿼리 편집기 창 전환 **문서** hello 가운데 창에서 열.
   ![Power BI 데스크톱 쿼리 편집기](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Hello 확장기 hello의 hello 오른쪽 클릭 **문서** 열 머리글입니다.  필드 목록 사용 하 여 hello 상황에 맞는 메뉴가 표시 됩니다.  예를 들어, 보고서에 필요한 hello 필드, 화산 이름, 국가, 지역, 위치, 권한 상승, 유형, 상태 및 마지막 알고 폭발 및 클릭 한 다음 선택 **확인**합니다.
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 문서 확장](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. hello 가운데 창의 hello 필드가 선택 된 hello 결과의 미리 보기가 표시 됩니다.
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 결과 평면화](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. 예에서 hello Location 속성은 문서에서 GeoJSON 블록.  보이는 것처럼 위치는 Power BI 데스크톱에서 **레코드** 형식으로 나타납니다.  
5. Hello hello 위치 열 머리글의 오른쪽에 hello 확장기를 클릭 합니다.  유형 및 좌표 필드와 hello 상황에 맞는 메뉴가 표시 됩니다.  보겠습니다 hello 좌표 필드를 선택 하 고 클릭 **확인**합니다.
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 위치 레코드](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. hello 가운데 창 이제 표시의 좌표 열 **목록** 유형입니다.  Hello 자습서의 hello 시작 부분에 표시 된 것과 같이 hello이이 자습서에서는 GeoJSON 데이터 지점 형식의 hello 좌표 배열에 기록 된 위도 및 경도 값이 포함 된 것입니다.
   
    hello 좌표 [0] 요소는 [1] 좌표는 위도 나타내는 동안 경도를 나타냅니다.
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 좌표 목록](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. tooflatten hello 좌표 배열, 만듭니다는 **사용자 지정 열** LatLong를 호출 합니다.  선택 hello **열 추가** 리본을 클릭할 **사용자 지정 열 추가**합니다.  hello **사용자 지정 열 추가** 창이 표시 되어야 합니다.
8. 예를 들어 LatLong hello 새 열에 대 한 이름을 제공 합니다.
9. 그런 다음 hello hello 새 열에 대 한 사용자 지정 수식을 지정 합니다.  이 예에서는 다음 수식을 hello를 사용 하 여 아래와 같이 쉼표로 구분 된 hello 위도 및 경도 값 연결 합니다: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`합니다. **확인**을 클릭합니다.
   
    DAX 함수를 포함한 데이터 분석 식(DAX)에 대한 자세한 내용은 [Power BI 데스크톱의 DAX 기초](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop)를 참조하세요.
   
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 사용자 지정 열 추가](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. 이제 hello 가운데 창 위도 hello로 채워진 hello 새 LatLong 열 및 경도 값을 쉼표로 구분 하 여 표시 됩니다.
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 사용자 지정 LatLong 열](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Hello 새 열에는 오류가 나타나면 쿼리 설정 단계 적용 hello hello 다음 그림 일치 하는지 확인 합니다.
    
    ![적용된 단계는 원본, 탐색, 확장된 문서, 확장된 Document.Location, 추가된 사용자 지정이어야 합니다.](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    삭제 단계를 다른 경우 추가 단계를 hello 및 hello 사용자 지정 열을 다시 추가 해 보십시오. 
11. 표 형식으로 flattening hello 데이터를 완료 했으므로 했습니다.  모든 쿼리 편집기 tooshape hello에서 사용할 수 있는 hello 기능을 활용할 수 있으며 Cosmos DB에는 데이터를 변환할 수 있습니다.  Hello 샘플을 사용 하는 hello 데이터 형식을 변경 권한 상승을 위해 너무**정수** hello를 변경 하 여 **데이터 형식** hello에 **홈** 리본.
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 열 형식 변경](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. 클릭 **닫고 적용** toosave hello 데이터 모델입니다.
    
    ![Azure Cosmos DB Power BI Connector에 대한 Power BI 자습서 - 닫기 및 적용](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>빌드 hello 보고서
Power BI Desktop 보고서 보기는 toovisualize 데이터 보고서를 만들기 시작할 수 있습니다.  Hello에 필드를 끌어다 보고서를 만들 수 **보고서** 캔버스입니다.

![Power BI 데스크톱 보고서 보기 - Power BI 커넥터](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

보고서 보기 hello에 있습니다.

1. hello **필드** 창은 필드가 보고서에 사용할 수 있는 데이터 모델 목록이 나타납니다.
2. hello **시각화** 창. 보고서는 단일 또는 여러 시각화 요소를 포함할 수 있습니다.  Hello에서 사용자의 요구에 맞추는 방식 hello 시각적 개체 형식 선택 **시각화** 창.
3. hello **보고서** 캔버스,이 보고서에 대 한 hello 시각적 개체가 작성 합니다.
4. hello **보고서** 페이지. Power BI 데스크톱에서 여러 보고서 페이지를 추가할 수 있습니다.

hello 다음 hello 간단한 대화형 지도 보기 보고서를 만드는 기본 단계를 보여 줍니다.

1. 이 예에서는 각 화산의 hello 위치를 표시 하는 지도 보기를 만듭니다.  Hello에 **시각화** 창 위의 hello 스크린샷에 강조 표시 된 대로 hello 지도 시각적 종류를 클릭 합니다.  Hello에 그릴 hello 지도 시각적 형식이 나타납니다 **보고서** 캔버스입니다.  hello **시각화** 창 해야 속성 관련된 toohello 지도 시각적 유형 집합을 표시할 수도 있습니다.
2. 이제 hello LatLong 필드를에서 끌어서 hello **필드** 창 toohello **위치** 속성 **시각화** 창.
3. 다음으로, 끌어서 놓기 hello 화산 이름 필드 toohello **범례** 속성입니다.  
4. 그런 다음 끌어서 놓기 hello 상승 필드 toohello **크기** 속성입니다.  
5. 이제 거품 hello hello 화산 toohello 상승 상관 관계를 지정 하는 hello 거품 크기와 각 화산의 hello 위치를 나타내는 집합을 보여 주는 시각적 맵 hello를 나타납니다.
6. 이제 기본 보고서를 만들었습니다.  더 많은 시각화를 추가 하 여 hello 보고서를 추가로 사용자 지정할 수 있습니다.  경우에 slicer toomake hello 화산 형식 보고서 대화형 추가 했습니다.  
   
    ![Power BI 자습서 hello Azure Cosmos DB에 대 한 완료 되 면 hello 최종 Power BI Desktop 보고서의 스크린샷](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>보고서 게시 및 공유
tooshare 보고서를 PowerBI.com에서 계정이 있어야 합니다.

1. Power BI Desktop hello hello 클릭 **홈** 리본.
2. **게시**를 클릭합니다.  PowerBI.com 계정에 대 한 증명된 tooenter hello 사용자 이름 및 암호 됩니다.
3. Hello 자격 증명 인증 되 면 hello 보고서는 선택한 게시 된 tooyour 위치입니다.
4. 클릭 **Power BI에서 열기 'PowerBITutorial.pbix'** toosee PowerBI.com에서 보고서를 공유 합니다.
   
    ![게시 tooPower BI 성공! Power BI에서 자습서 열기](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>PowerBI.com에서 대시보드 만들기
이제 보고서가 있으니 PowerBI.com에서 공유하겠습니다.

TooPowerBI.com Power BI Desktop에서에서 보고서를 게시 하는 경우에 생성 한 **보고서** 및 **데이터 집합** PowerBI.com 테 넌 트에 있습니다. 예를 들어 이라는 보고서 게시 후 **PowerBITutorial** tooPowerBI.com, PowerBITutorial에에서 나타나는 두 hello **보고서** 및 **데이터 집합** 섹션에서 PowerBI.com 합니다.

   ![새 보고서 및 PowerBI.com에서 데이터 집합의 스크린 샷 hello](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate 공유할 수 있는 대시보드 클릭 hello **라이브 고정 페이지** PowerBI.com 보고서에서 단추입니다.

   ![새 보고서 및 PowerBI.com에서 데이터 집합의 스크린 샷 hello](./media/powerbi-visualize/power-bi-pin-live-tile.png)

hello 지침에 따라 [보고서에서 타일 고정](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate 새 대시보드 합니다. 

또한 대시보드를 만들기 전에 tooreport 임시 수정 작업을 수행할 수 있습니다. 그러나 tooperform hello 수정 내용을 Power BI Desktop을 사용 하 고 hello 보고서 tooPowerBI.com 다시 게시 하는 것이 좋습니다.

## <a name="refresh-data-in-powerbicom"></a>PowerBI.com에서 데이터 새로 고침
두 가지 toorefresh 데이터, 임시 및 예약 합니다.

임시 새로 고침을 클릭 하세요 (...) hello eclipses hello 하 여 **Dataset**, 예: PowerBITutorial 합니다. **지금 새로 고침**을 포함한 작업의 목록이 표시됩니다. 클릭 **지금 새로 고침** toorefresh hello 데이터입니다.

![PowerBI.com에서 지금 새로 고침의 스크린샷](./media/powerbi-visualize/power-bi-refresh-now.png)

예약 된 새로 수행 hello를 수행 합니다.

1. 클릭 **새로 고침 예약** hello 작업 목록에 있습니다. 

    ![PowerBI.com에서 새로 고침 예약 hello의 스크린샷](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. Hello에 **설정** 페이지 **데이터 원본 자격 증명**합니다. 
3. **자격 증명 편집**을 클릭합니다. 
   
    hello 구성 팝업이 나타납니다. 
4. 해당 데이터 집합에 대 한 hello 키 tooconnect toohello Cosmos DB 계정을 입력 한 다음 클릭 **로그인**합니다. 
5. 확장 **새로 고침 예약** toorefresh hello 데이터 집합을 원하는 hello 일정을 설정 하 고 있습니다. 
6. 클릭 **적용** 있고 완료 된 hello 예약 된 새로 고침을 설정 합니다.

## <a name="next-steps"></a>다음 단계
* Power BI에 대해 자세히 toolearn 참조 [Power BI 시작](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)합니다.
* Cosmos DB에 대해 자세히 toolearn 참조 hello [Azure Cosmos DB 설명서 방문 페이지](https://azure.microsoft.com/documentation/services/documentdb/)합니다.

