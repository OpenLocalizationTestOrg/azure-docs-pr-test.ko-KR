---
title: "HDInsight의 Hive와 aaaAnalyze 및 프로세스 JSON 문서 | Microsoft Docs"
description: "Toouse JSON에 설명 하 고 이러한 분석 하는 방법을 알아보려면 HDInsight의 Hive를 사용 하 여 합니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>HDInsight의 Hive를 사용한 JSON 문서 처리 및 분석

자세한 내용은 방법 tooprocess 및 HDInsight의 Hive를 사용 하 여 JSON 파일을 분석 합니다. 다음 JSON 문서 hello hello 자습서에 사용 됩니다.

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

hello 파일에서 찾을 수 있습니다 wasb://processjson@hditutorialdata.blob.core.windows.net/합니다. HDInsight에서의 Azure Blob 저장소 사용에 대한 자세한 내용은 [HDInsight에서 Hadoop으로 HDFS 호환 가능한 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요. 클러스터의 hello 파일 toohello 기본 컨테이너를 복사할 수 있습니다.

이 자습서에서는 hello 하이브 콘솔을 사용 합니다.  Hello 하이브 콘솔을 열고의 지침은 [사용 하 여 원격 데스크톱을 사용 하는 HDInsight의 Hadoop으로 하이브](hdinsight-hadoop-use-hive-remote-desktop.md)합니다.

## <a name="flatten-json-documents"></a>JSON 문서 평면화
hello 다음 섹션에 나열 된 hello 방법 hello JSON 문서는 단일 행에 필요 합니다. 따라서 hello JSON 문서 tooa 문자열을 결합 해야 합니다. JSON 문서를 병합 이미 있는 경우이 단계를 건너뛸 하 고 JSON 분석 데이터에 직선 toohello 다음 섹션을 이동할 수 있습니다.

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

hello 원시 JSON 파일은  **wasb://processjson@hditutorialdata.blob.core.windows.net/** 합니다. hello *StudentsRaw* 하이브 테이블 toohello 원시 결합 되지 않은 JSON 문서를 가리킵니다.

hello *StudentsOneLine* hello hello에서 HDInsight 기본 파일 시스템에에서 hello 데이터를 저장 하는 Hive 테이블 */json/학생/* 경로입니다.

hello INSERT 문을 JSON 데이터 결합 hello hello StudentOneLine 테이블을 채웁니다.

hello SELECT 문은 행을 하나만 반환 해야 합니다.

다음은 hello hello SELECT 문의 출력이입니다.

![Hello JSON 문서를 평면화 합니다.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>Hive에서 JSON 문서 분석
Hive는 JSON 문서에 세 가지 다른 메커니즘 toorun 쿼리를 제공 합니다.

* GET hello를 사용 하 여\_JSON\_개체 UDF (사용자 정의 함수)
* hello JSON_TUPLE UDF를 사용 하 여
* 사용자 지정 SerDe 사용
* Python 또는 기타 언어를 사용하여 자체 UDF를 작성합니다. Hive에서 Python 실행에 대한 자세한 내용은 [이 문서][hdinsight-python]를 참조하세요.

### <a name="use-hello-getjsonobject-udf"></a>사용 하 여 hello GET\_JSON_OBJECT UDF
Hive는 런타임에 JSON 쿼리를 수행할 수 있는 [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object)라는 기본 제공 UDF를 제공합니다. 이 메서드는 두 개의 인수-hello 테이블 이름 및 메서드 이름을 hello 결합 된 JSON 문서와 hello JSON 필드를 toobe 구문 분석할 필요 합니다. 이 UDF 작동 방식 예제 toosee는에서 살펴보겠습니다.

Hello 이름 및 각 학생의 성

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

다음은 콘솔 창에서이 쿼리를 실행할 때 hello 출력 합니다.

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

Hello get json_object의 몇 가지 제한 사항이 UDF 합니다.

* Hello 쿼리의 각 필드에에서 필요 하므로 hello 쿼리를 다시 구문 분석, hello 성능을 영향을 줍니다.
* 가져오기\_JSON_OBJECT() 배열 hello 문자열 표현을 반환 합니다. tooconvert 대괄호 hello toouse 정규식 tooreplace 해야이 배열 tooa 하이브 배열 ' [' 및 ']'이 고 다음도 분할 tooget hello 배열 호출 합니다.

이 때문에 hello 하이브 wiki json_tuple 사용할 것을 권장 합니다.  

### <a name="use-hello-jsontuple-udf"></a>Hello JSON_TUPLE UDF를 사용 하 여
Hive에서 제공하는 다른 UDF는 [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object)보다 성능이 뛰어난 [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple)입니다. 이 메서드는 키 집합 및 JSON 문자열을 사용하며, 하나의 함수를 통해 값의 튜플을 반환합니다. hello 다음 쿼리 hello 학생 id와 반환 hello 등급 hello JSON 문서에서:

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

hello 하이브 콘솔에서이 스크립트의 hello 출력:

![json_tuple UDF][image-hdi-hivejson-jsontuple]

JSON\_튜플 hello를 사용 하 여 [보기 하 여 측면](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) json 허용 하이브에 구문\_튜플 toocreate hello UDT 함수 tooeach hello 원본 테이블의 행을 적용 하 여 가상 테이블입니다.  반복 hello 너무 어려워 지 되어 복잡 한 Json 측면 보기를 활용 합니다. 또한 JSON_TUPLE은 중첩된 JSON을 처리할 수 없습니다.

### <a name="use-custom-serde"></a>사용자 지정 SerDe 사용
SerDe hello 중첩 된 JSON 문서를 구문 분석을 위한 최선의 선택은, toodefine hello JSON 스키마 및 사용 하 여 hello 스키마 tooparse hello 문서 수입니다. 이 자습서를 사용 하 여 hello 중 하나에서 개발 된 더 인기가 SerDe [Roberto Congiu](https://github.com/rcongiu)합니다.

**toouse는 사용자 지정 SerDe hello:**

1. [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR)를 설치합니다. Toobe hdinsight hello Windows 배포를 사용 하는 경우 hello Windows X64 버전의 hello JDK 선택 합니다.
   
   > [!WARNING]
   > JDK 1.8은 이 SerDe에서 작동하지 않습니다.
   > 
   > 
   
    Hello 설치가 완료 된 후에 새로운 사용자 환경 변수를 추가 합니다.
   
   1. 열기 **고급 시스템 설정 보기** hello Windows 화면에서 합니다.
   2. **환경 변수**를 클릭합니다.  
   3. 새로 추가 **JAVA_HOME** 환경 변수가 너무 가리키고**C:\Program Files\Java\jdk1.7.0_55** 아무 곳에 나 JDK 설치 되어 있습니다.
      
      ![JDK에 대한 올바른 구성 값 설정][image-hdi-hivejson-jdk]
2. [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Hello bin 폴더 tooyour 경로 추가 이동 하 여 tooControl 패널--> 계정 환경 변수에 대 한 hello 시스템 변수 편집 합니다. hello 다음 스크린샷에 표시 하는 toodo이 있습니다.
   
    ![Maven 설치][image-hdi-hivejson-maven]
3. 복제 hello 프로젝트 [하이브-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github 사이트입니다. Hello 스크린 샷 다음 그림과 같이 hello "zip 파일 다운로드" 단추를 클릭 하 여이 수행할 수 있습니다.
   
    ![복제 hello 프로젝트][image-hdi-hivejson-serde]

4:이 패키지를 선택한 다음 패키지 유형"mvn"를 다운로드 한 위치 이동 toohello 폴더입니다. 이 만들어야 hello 필요한 jar 파일을 통해 toohello 클러스터 복사할 수 있습니다.

5: hello 패키지를 다운로드 하는 hello 루트 폴더 아래의 toohello 대상 폴더를 이동 합니다. Hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar 파일 toohead-클러스터의 노드를 업로드 합니다. 일반적으로 hello 하이브 이진 폴더에서 관리 하려면: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin 또는 이와 비슷한 이름입니다.

6: hello 하이브 프롬프트에서 "jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar 추가"를 입력 합니다. 이므로 여기서에서 hello jar hello C:\apps\dist\hive-0.13.x\bin 폴더에 표시 된 것 처럼 hello 이름의 hello jar 직접 추가할 수 있습니다.

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![JAR tooyour 프로젝트 추가][image-hdi-hivejson-addjar]

이제 있습니다 hello JSON 문서에 대 한 준비 toouse hello SerDe toorun 쿼리 됩니다.

hello 문 다음 정의 된 스키마와 테이블을 만듭니다.

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

toolist hello 이름 및 hello 학생의 성

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Hello 하이브 콘솔에서 hello 결과 다음과 같습니다.

![SerDe 쿼리 1][image-hdi-hivejson-serde_query1]

hello JSON 문서의 점수의 toocalculate hello 합계

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

앞에 쿼리에서 사용 하 여 hello [측면 보기 분해](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello 점수의 배열 합산할 수 있도록 합니다.

다음은 hello hello 하이브 콘솔 출력이입니다.

![SerDe 쿼리 2][image-hdi-hivejson-serde_query2]

특정된 학생이 주체는 toofind 80 포인트 이상 점수가 매겨진 했습니다.

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

hello 앞의 쿼리 하이브 배열을 반환 get 달리\_json\_개체는 문자열을 반환 합니다.

![SerDe 쿼리 3][image-hdi-hivejson-serde_query3]

Tooskil 하려는 경우 다음 hello에 설명 된 것된으로 잘못 된 형식의 JSON [wiki 페이지](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) 이 SerDe이의 구현 하 hello 코드 다음을 입력 하 여:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>요약
결론적으로 hello 유형의 사용자가 선택한 하이브에 JSON 연산자 각 시나리오에 따라 달라 집니다. 간단한 JSON 문서를 해야 하 고만 하나의 필드 toolook에 있는 toouse hello 하이브 UDF get를 선택할 수 있습니다 경우\_json\_개체입니다. 에 대해 둘 이상의 키 toolook 설정한 경우 json_tuple를 사용할 수 있습니다. 중첩 된 문서를 설정한 경우 JSON SerDe hello를 사용 해야 합니다.

## <a name="next-steps"></a>다음 단계

다른 관련된 문서는 다음을 참조하세요.

* [HDInsight tooanalyze 샘플 Apache log4j 파일에서에서 Hadoop으로 Hive 및 HiveQL를 사용 하 여](hdinsight-use-hive.md)
* [HDInsight의 Hive를 사용하여 비행 지연 데이터 분석](hdinsight-analyze-flight-delay-data.md)
* [HDInsight에서 Hive를 사용하여 Twitter 데이터 분석](hdinsight-analyze-twitter-data.md)
* [Azure Cosmos DB 및 HDInsight를 사용하여 Hadoop 작업 실행](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
