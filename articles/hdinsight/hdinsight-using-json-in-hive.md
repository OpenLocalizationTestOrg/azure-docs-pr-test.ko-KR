---
title: "HDInsight의 하이브를 사용하여 JSON 문서 분석 및 처리 | Microsoft Docs"
description: "JSON 문서를 사용하고 HDInsight의 하이브를 사용하여 이 문서를 분석하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: bd136afebeceb0cd9c24cfc5f15601caa80a755e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="aac49-103">HDInsight의 Hive를 사용한 JSON 문서 처리 및 분석</span><span class="sxs-lookup"><span data-stu-id="aac49-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="aac49-104">HDInsight에서 Hive를 사용하여 JSON 파일을 분석하고 처리하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-104">Learn how to process and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="aac49-105">이 자습서에서는 다음 JSON 문서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-105">The following JSON document is used in the tutorial:</span></span>

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

<span data-ttu-id="aac49-106">이 파일은 wasb://processjson@hditutorialdata.blob.core.windows.net/에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-106">The file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="aac49-107">HDInsight에서의 Azure Blob 저장소 사용에 대한 자세한 내용은 [HDInsight에서 Hadoop으로 HDFS 호환 가능한 Azure Blob 저장소 사용](hdinsight-hadoop-use-blob-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aac49-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="aac49-108">클러스터의 기본 컨테이너에 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-108">You can copy the file to the default container of your cluster.</span></span>

<span data-ttu-id="aac49-109">이 자습서에서는 Hive 콘솔을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-109">In this tutorial, you use the Hive console.</span></span>  <span data-ttu-id="aac49-110">Hive 콘솔을 여는 방법은 [원격 데스크톱을 사용하여 HDInsight에서 Hadoop과 Hive 사용](hdinsight-hadoop-use-hive-remote-desktop.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aac49-110">For instructions of opening the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="aac49-111">JSON 문서 평면화</span><span class="sxs-lookup"><span data-stu-id="aac49-111">Flatten JSON documents</span></span>
<span data-ttu-id="aac49-112">다음 섹션에 나열된 메서드에서는 단일 행의 JSON 문서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-112">The methods listed in the next section require the JSON document in a single row.</span></span> <span data-ttu-id="aac49-113">따라서 JSON 문서를 문자열로 평면화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-113">So you must flatten the JSON document to a string.</span></span> <span data-ttu-id="aac49-114">JSON 문서가 이미 평면화되어 있으면 이 단계를 건너뛰고 다음 섹션인 JSON 데이터 분석으로 바로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="aac49-115">원시 JSON 파일은 **wasb://processjson@hditutorialdata.blob.core.windows.net/**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-115">The raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="aac49-116">*StudentsRaw* Hive 테이블은 평면화되지 않은 JSON 문서를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-116">The *StudentsRaw* Hive table points to the raw unflattened JSON document.</span></span>

<span data-ttu-id="aac49-117">*StudentsOneLine* Hive 테이블은 HDInsight 기본 파일 시스템에서 데이터를 */json/students/* 경로에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-117">The *StudentsOneLine* Hive table stores the data in the HDInsight default file system under the */json/students/* path.</span></span>

<span data-ttu-id="aac49-118">INSERT 문은 StudentOneLine 테이블을 평면화된 JSON 데이터로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-118">The INSERT statement populates the StudentOneLine table with the flattened JSON data.</span></span>

<span data-ttu-id="aac49-119">SELECT 문은 1행만 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-119">The SELECT statement shall only return one row.</span></span>

<span data-ttu-id="aac49-120">SELECT 문의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-120">Here is the output of the SELECT statement:</span></span>

![JSON 문서 평면화][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="aac49-122">Hive에서 JSON 문서 분석</span><span class="sxs-lookup"><span data-stu-id="aac49-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="aac49-123">하이브는 JSON 문서에서 쿼리를 실행할 수 있는 다음 세 가지 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-123">Hive provides three different mechanisms to run queries on JSON documents:</span></span>

* <span data-ttu-id="aac49-124">GET\_JSON\_OBJECT UDF(사용자 정의 함수) 사용</span><span class="sxs-lookup"><span data-stu-id="aac49-124">use the GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="aac49-125">JSON_TUPLE UDF 사용</span><span class="sxs-lookup"><span data-stu-id="aac49-125">use the JSON_TUPLE UDF</span></span>
* <span data-ttu-id="aac49-126">사용자 지정 SerDe 사용</span><span class="sxs-lookup"><span data-stu-id="aac49-126">use custom SerDe</span></span>
* <span data-ttu-id="aac49-127">Python 또는 기타 언어를 사용하여 자체 UDF를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="aac49-128">Hive에서 Python 실행에 대한 자세한 내용은 [이 문서][hdinsight-python]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aac49-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-the-getjsonobject-udf"></a><span data-ttu-id="aac49-129">GET\_JSON_OBJECT UDF 사용</span><span class="sxs-lookup"><span data-stu-id="aac49-129">Use the GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="aac49-130">Hive는 런타임에 JSON 쿼리를 수행할 수 있는 [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object)라는 기본 제공 UDF를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="aac49-131">이 메서드에는 두 개의 인수, 즉 평면화된 JSON 문서와 구문 분석해야 하는 JSON 필드가 있는 테이블 이름 및 메서드 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-131">This method takes two arguments – the table name and method name, which has the flattened JSON document and the JSON field that needs to be parsed.</span></span> <span data-ttu-id="aac49-132">이 UDF의 작동 방식에 대한 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-132">Let’s look at an example to see how this UDF works.</span></span>

<span data-ttu-id="aac49-133">학생의 이름 및 성 가져오기</span><span class="sxs-lookup"><span data-stu-id="aac49-133">Get the first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="aac49-134">이 쿼리를 콘솔 창에서 실행할 경우의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-134">Here is the output when running this query in console window.</span></span>

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="aac49-136">get-json_object UDF에는 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-136">There are a few limitations of the get-json_object UDF.</span></span>

* <span data-ttu-id="aac49-137">쿼리의 각 필드에서는 쿼리를 다시 구문 분석해야 하므로 성능에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-137">Because each field in the query requires reparsing the query, it affects the performance.</span></span>
* <span data-ttu-id="aac49-138">GET\_JSON_OBJECT()는 배열의 문자열 표현을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-138">GET\_JSON_OBJECT() returns the string representation of an array.</span></span> <span data-ttu-id="aac49-139">이 배열을 Hive 배열로 변환하려면 정규식을 사용하여 대괄호 ‘[‘ 및 ‘]’을 바꾼 다음 분할 호출하여 배열을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-139">To convert this array to a Hive array, you have to use regular expressions to replace the square brackets ‘[‘ and ‘]’ and then also call split to get the array.</span></span>

<span data-ttu-id="aac49-140">그렇기 때문에 Hive Wiki에서는 json_tuple을 사용하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-140">This is why the Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-the-jsontuple-udf"></a><span data-ttu-id="aac49-141">JSON_TUPLE UDF 사용</span><span class="sxs-lookup"><span data-stu-id="aac49-141">Use the JSON_TUPLE UDF</span></span>
<span data-ttu-id="aac49-142">Hive에서 제공하는 다른 UDF는 [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object)보다 성능이 뛰어난 [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple)입니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="aac49-143">이 메서드는 키 집합 및 JSON 문자열을 사용하며, 하나의 함수를 통해 값의 튜플을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="aac49-144">다음 쿼리는 JSON 문서에서 학생 ID와 등급을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-144">The following query returns the student id and the grade from the JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="aac49-145">Hive 콘솔에 표시되는 이 스크립트의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-145">The output of this script in the Hive console:</span></span>

![json_tuple UDF][image-hdi-hivejson-jsontuple]

<span data-ttu-id="aac49-147">JSON\_TUPLE은 Hive에서 [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) 구문을 사용합니다. 이 구문을 사용하면 json\_tuple이 원래 테이블의 각 행에 UDT 함수를 적용하여 가상 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-147">JSON\_TUPLE uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span></span>  <span data-ttu-id="aac49-148">LATERAL VIEW를 반복 사용하면 복잡한 JSON이 다루기 어렵게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-148">Complex JSONs become too unwieldy because of the repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="aac49-149">또한 JSON_TUPLE은 중첩된 JSON을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="aac49-150">사용자 지정 SerDe 사용</span><span class="sxs-lookup"><span data-stu-id="aac49-150">Use custom SerDe</span></span>
<span data-ttu-id="aac49-151">SerDe는 중첩된 JSON 문서에 가장 적합한 구문 분석으로, JSON 스키마를 정의하고 이 스키마를 사용하여 문서를 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-151">SerDe is the best choice for parsing nested JSON documents, it allows you to define the JSON schema, and use the schema to parse the documents.</span></span> <span data-ttu-id="aac49-152">이 자습서에서는 [Roberto Congiu](https://github.com/rcongiu)가 개발한 가장 일반적인 SerDe 중 하나를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-152">In this tutorial, you use one of the more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="aac49-153">**사용자 지정 SerDe를 사용하려면**</span><span class="sxs-lookup"><span data-stu-id="aac49-153">**To use the custom SerDe:**</span></span>

1. <span data-ttu-id="aac49-154">[Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="aac49-155">HDInsight의 Windows 배포를 사용하려면 Windows X64 버전 JDK를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-155">Choose the Windows X64 version of the JDK if you are going to be using the Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="aac49-156">JDK 1.8은 이 SerDe에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="aac49-157">설치 완료 후 새 사용자 환경 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-157">After the installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="aac49-158">Windows 화면에서 **고급 시스템 설정 보기** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-158">Open **View advanced system settings** from the Windows screen.</span></span>
   2. <span data-ttu-id="aac49-159">**환경 변수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="aac49-160">새 **JAVA_HOME** 환경 변수를 추가합니다. 이 변수는 **C:\Program Files\Java\jdk1.7.0_55** 또는 JDK 설치 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-160">Add a new **JAVA_HOME** environment variable is pointing to **C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![JDK에 대한 올바른 구성 값 설정][image-hdi-hivejson-jdk]
2. <span data-ttu-id="aac49-162">[Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="aac49-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="aac49-163">제어판-->사용자 계정의 환경 변수에 대한 시스템 변수 편집으로 이동하여 bin 폴더를 경로에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-163">Add the bin folder to your path by going to Control Panel-->Edit the System Variables for your account Environment variables.</span></span> <span data-ttu-id="aac49-164">다음 스크린샷은 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-164">The following screenshot shows you how to do this.</span></span>
   
    ![Maven 설치][image-hdi-hivejson-maven]
3. <span data-ttu-id="aac49-166">[Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github 사이트에서 프로젝트를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-166">Clone the project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="aac49-167">다음 스크린샷에 표시된 것처럼 "Zip 다운로드" 단추를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-167">You can do this by clicking on the “Download Zip” button as shown in the following screenshot.</span></span>
   
    ![프로젝트 복제][image-hdi-hivejson-serde]

<span data-ttu-id="aac49-169">4: 이 패키지를 다운로드한 폴더로 이동하여 "mvn package"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-169">4: Go to the folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="aac49-170">클러스터에 복사할 수 있는 필수 jar 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-170">This should create the necessary jar files that you can then copy over to the cluster.</span></span>

<span data-ttu-id="aac49-171">5: 패키지를 다운로드한 루트 폴더 아래의 대상 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-171">5: Go to the target folder under the root folder where you downloaded the package.</span></span> <span data-ttu-id="aac49-172">클러스터의 헤드 노드에 json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-172">Upload the json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file to head-node of your cluster.</span></span> <span data-ttu-id="aac49-173">일반적으로 C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin과 유사한 하이브 이진 파일 폴더에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-173">I usually put it under the hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="aac49-174">6: Hive 프롬프트에서 “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-174">6: In the hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="aac49-175">이 예제에서는 jar이 C:\apps\dist\hive-0.13.x\bin 폴더에 있으므로 표시된 이름으로 jar을 직접 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-175">Since in my case, the jar is in the C:\apps\dist\hive-0.13.x\bin folder, I can directly add the jar with the name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![프로젝트에 JAR 추가][image-hdi-hivejson-addjar]

<span data-ttu-id="aac49-177">이제 SerDe를 사용하여 JSON 문서를 쿼리할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-177">Now, you are ready to use the SerDe to run queries against the JSON document.</span></span>

<span data-ttu-id="aac49-178">다음 문은 정의된 스키마가 있는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-178">The following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="aac49-179">학생의 이름 및 성을 나열하려면</span><span class="sxs-lookup"><span data-stu-id="aac49-179">To list the first name and last name of the student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="aac49-180">하이브 콘솔의 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-180">Here is the result from the Hive console.</span></span>

![SerDe 쿼리 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="aac49-182">JSON 문서의 성적 합계를 계산하려면</span><span class="sxs-lookup"><span data-stu-id="aac49-182">To calculate the sum of scores of the JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="aac49-183">이전 쿼리에서는 성적의 합계를 구할 수 있도록 [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF를 사용하여 성적 배열을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-183">The preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF to expand the array of scores so that they can be summed.</span></span>

<span data-ttu-id="aac49-184">하이브 콘솔의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-184">Here is the output from the Hive console.</span></span>

![SerDe 쿼리 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="aac49-186">지정된 학생이 80점 넘게 받은 과목을 찾으려면</span><span class="sxs-lookup"><span data-stu-id="aac49-186">To find which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="aac49-187">이전 쿼리는 문자열을 반환하는 get\_json\_object와 달리 하이브 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-187">The preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![SerDe 쿼리 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="aac49-189">잘못된 형식의 JSON을 중지하려면 이 SerDe의 [Wiki 페이지](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) 에 설명된 대로 다음 코드를 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-189">If you want to skil malformed JSON, then as explained in the [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing the following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="aac49-190">요약</span><span class="sxs-lookup"><span data-stu-id="aac49-190">Summary</span></span>
<span data-ttu-id="aac49-191">결론적으로 선택하는 하이브의 JSON 연산자 유형은 시나리오에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-191">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="aac49-192">JSON 문서가 간단하고 조회할 필드가 하나뿐인 경우에는 하이브 UDF get\_json\_object를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-192">If you have a simple JSON document and you only have one field to look up on – you can choose to use the Hive UDF get\_json\_object.</span></span> <span data-ttu-id="aac49-193">조회가 키가 두 개 이상인 경우에는 json_tuple을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-193">If you have more than one key to look up on, then you can use json_tuple.</span></span> <span data-ttu-id="aac49-194">중첩된 문서가 있는 경우에는 JSON SerDe를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac49-194">If you have a nested document, then you should use the JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aac49-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aac49-195">Next steps</span></span>

<span data-ttu-id="aac49-196">다른 관련된 문서는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aac49-196">For other related articles, see</span></span>

* [<span data-ttu-id="aac49-197">샘플 Apache log4j 파일 분석을 위해 HDInsight에서 Hadoop과 함께 Hive 및 HiveQL 사용</span><span class="sxs-lookup"><span data-stu-id="aac49-197">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="aac49-198">HDInsight의 Hive를 사용하여 비행 지연 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="aac49-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="aac49-199">HDInsight에서 Hive를 사용하여 Twitter 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="aac49-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="aac49-200">Azure Cosmos DB 및 HDInsight를 사용하여 Hadoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="aac49-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
