---
title: "온라인 데이터 원본에서 기계 학습 스튜디오로 aaaImport 데이터 | Microsoft Docs"
description: "어떻게 tooimport Azure 기계 학습 스튜디오 다양 한 온라인 원본에서 학습 데이터입니다."
keywords: "데이터 가져오기, 데이터 형식, 데이터 유형, 데이터 원본, 학습 데이터"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>Azure 기계 학습 스튜디오 hello 데이터 가져오기 모듈과 함께 다양 한 온라인 데이터 원본에서 데이터 가져오기
이 문서에서는 다양 한 소스에서 온라인 데이터 가져오기에 대 한 hello 지원을 설명 및 hello 정보는 Azure 기계 학습 실험에 이러한 원본의 toomove 데이터가 필요 합니다.

> [!NOTE]
> 이 문서에서는 hello에 대 한 일반 정보 제공 [데이터 가져오기] [ import-data] 모듈입니다. 형식, 매개 변수 및 대답 toocommon 질문 hello에 대 한 hello 모듈 참조 항목을 참조 hello 유형의 액세스할 수 있는 데이터에 대 한 정보를 자세한 [데이터 가져오기] [ import-data] 모듈입니다.
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>소개
Hello를 사용 하 여 [데이터 가져오기] [ import-data] 모듈 데이터에 액세스할 수 여러 온라인 데이터 원본 중 하나에서 실험에서 실행 중인 동안 [Azure 기계 학습 스튜디오](https://studio.azureml.net/Home):

* HTTP을 사용하는 웹 URL
* HiveQL을 사용하는 Hadoop
* Azure Blob 저장소
* Azure 테이블
* Azure SQL 데이터베이스 또는 Azure VM의 SQL Server
* 온-프레미스 SQL Server 데이터베이스
* 데이터 피드 공급자, OData 현재
* Azure CosmosDB(이전 명칭 DocumentDB)

하려면 Studio 실험에서 tooaccess 온라인 데이터 원본 추가 hello [데이터 가져오기] [ import-data] 모듈 tooyour, 선택 hello **데이터 소스**를 선택한 다음 필요한 hello 매개 변수를 제공 tooaccess hello 데이터입니다. 지원 되는 hello 온라인 데이터 원본 아래 hello 표에 항목별로 됩니다. 매개 변수를 사용 하는 tooaccess hello 데이터 및이 테이블에도 지원 되는 hello 파일 형식을 보여 줍니다.

실험이 실행 중인 동안 이 학습 데이터에 액세스하므로 데이터는 해당 실험에서만 사용할 수 있습니다. 이와 달리 dataset 모듈에 저장 된 데이터가 작업 영역에서 사용할 수 있는 tooany 실험이 됩니다.

> [!IMPORTANT]
> 현재 hello [데이터 가져오기] [ import-data] 및 [데이터 내보내기] [ export-data] 모듈 읽고 hello를 사용 하 여 만든 Azure 저장소에서 데이터를 쓸 수 클래식 배포 모델입니다. 즉, 핫 저장소 액세스 계층에서 제공 하는 새 Azure Blob 저장소 계정 유형을 hello 또는 저장소 쿨 액세스 계층 아직 지원 되지 않습니다. 
> 
> 일반적으로 이 서비스 옵션이 제공되기 전에 만들었을 수 있는 모든 Azure 저장소 계정은 영향을 받지 않습니다. 
> 새 계정을 toocreate 필요한 경우에 선택 **클래식** hello 배포에 대 한 모델, 리소스 관리자를 사용 하 고 선택 **범용** 대신 **Blob 저장소** 에 대 한 **Kind 계정**합니다. 
> 
> 자세한 내용은 [Azure Blob 저장소: 핫 및 쿨 저장소 계층](../storage/blobs/storage-blob-storage-tiers.md)을 참조하세요.
> 
> 

## <a name="supported-online-data-sources"></a>지원되는 온라인 데이터 원본
Azure 기계 학습 **데이터 가져오기** 모듈은 데이터 원본 hello를 지원 합니다.

| 데이터 원본 | 설명 | 매개 변수 |
| --- | --- | --- |
| HTTP를 통한 웹 URL |HTTP를 사용하는 어떤 웹 URL에서도 데이터를 쉼표로 구분된 값(CSV), 탭으로 구분된 값(TSV), 특성-관계 파일 형식(ARFF) 및 지원 벡터 컴퓨터(SVM-light) 형식으로 읽습니다. |<b>URL</b>: hello hello 사이트 URL과 hello 파일 이름 확장명으로 포함 하는 hello 파일의 전체 이름을 지정 합니다. <br/><br/><b>데이터 형식</b>: hello 지원 데이터 중 하나가 형식 지정: CSV, TSV, ARFF 또는 svmlight입니다. Hello 데이터에 머리글 행을 경우 사용 되는 tooassign 열 이름입니다. |
| Hadoop/HDFS |Hadoop의 분산 저장소에서 데이터를 읽습니다. SQL 유사 쿼리 언어인 HiveQL을 사용 하 여 원하는 hello 데이터를 지정 합니다. HiveQL은 tooaggregate 사용 되는 데이터가 있을 수 있고 데이터 hello 데이터 tooMachine 학습 스튜디오를 추가 하기 전에 필터링을 수행 합니다. |<b>하이브 데이터베이스 쿼리</b>: toogenerate hello 데이터를 사용 하는 hello 하이브 쿼리를 지정 합니다.<br/><br/><b>HCatalog 서버 URI </b> : hello 형식을 사용 하 여 클러스터의 이름이 지정된 하는 hello  *&lt;클러스터 이름&gt;. azurehdinsight.net 합니다.*<br/><br/><b>Hadoop 사용자 계정 이름을</b>: hello Hadoop 사용자 계정 이름이 tooprovision hello 클러스터 사용을 지정 합니다.<br/><br/><b>Hadoop 사용자 계정 암호</b> : 지정 hello hello 클러스터를 프로 비전 할 때 사용 된 자격 증명입니다. 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](../hdinsight/hdinsight-provision-clusters.md)를 참조하세요.<br/><br/><b>출력 데이터의 위치</b>: hello 데이터 distributed Hadoop 파일 시스템 (HDFS) 또는 Azure에 저장 되는지 여부를 지정 합니다. <br/><ul>HDFS에서 출력 데이터를 저장 하는 경우 hello HDFS 서버 URI를 지정 합니다. (Hello HTTPS:// 접두사가 없는 있는지 toouse hello HDInsight 클러스터 이름을 수). <br/><br/>Azure의 출력 데이터를 저장 하는 경우 저장소 컨테이너 이름 및 hello Azure 저장소 계정 이름, 저장소 액세스 키를 지정 해야 합니다.</ul> |
| SQL 데이터베이스 |Azure 가상 컴퓨터에서 실행되는 SQL Server 데이터베이스 또는 Azure SQL 데이터베이스에 저장된 데이터를 읽습니다. |<b>데이터베이스 서버 이름</b>: hello 서버의 데이터베이스를 실행 중인 어떤 hello hello 이름을 지정 합니다.<br/><ul>Azure SQL 데이터베이스의 경우 생성 되는 hello 서버 이름을 입력 합니다. 일반적으로 hello 폼을에  *&lt;generated_identifier&gt;. database.windows.net 합니다.* <br/><br/>Azure Virtual Machines에서 호스트되는 SQL Server인 경우 *tcp:&lt;가상 컴퓨터 DNS 이름&gt;, 1433*을 입력합니다.</ul><br/><b>데이터베이스 이름 </b>: hello 서버에서 hello hello 데이터베이스 이름을 지정 합니다. <br/><br/><b>서버 사용자 계정 이름</b>: hello 데이터베이스에 대 한 액세스 권한이 있는 계정의 사용자 이름을 지정 합니다. <br/><br/><b>서버 사용자 계정 암호</b>: hello hello 사용자 계정의 암호를 지정 합니다.<br/><br/><b>모든 서버 인증서 수락</b>: tooskip 데이터를 읽기 전에 먼저 hello 사이트 인증서를 검토 하려는 경우이 옵션 (보안 수준 낮음)을 사용 합니다.<br/><br/><b>데이터베이스 쿼리</b>: tooread 원하는 hello 데이터를 설명 하는 SQL 문을 입력 합니다. |
| 온-프레미스 SQL 데이터베이스 |온-프레미스 SQL 데이터베이스에 저장된 데이터를 읽습니다. |<b>데이터 게이트웨이</b>: SQL Server 데이터베이스를 액세스할 수 있는 컴퓨터에 설치 된 데이터 관리 게이트웨이 hello의 hello 이름을 지정 합니다. Hello 게이트웨이 설정에 대 한 정보를 참조 하십시오. [온-프레미스 SQL server에서 데이터를 사용 하 여 Azure 기계 학습을 사용 하 여 분석을 진행 수행](machine-learning-use-data-from-an-on-premises-sql-server.md)합니다.<br/><br/><b>데이터베이스 서버 이름</b>: hello 서버의 데이터베이스를 실행 중인 어떤 hello hello 이름을 지정 합니다.<br/><br/><b>데이터베이스 이름 </b>: hello 서버에서 hello hello 데이터베이스 이름을 지정 합니다. <br/><br/><b>서버 사용자 계정 이름</b>: hello 데이터베이스에 대 한 액세스 권한이 있는 계정의 사용자 이름을 지정 합니다. <br/><br/><b>사용자 이름 및 암호</b>: 클릭 <b>값을 입력</b> tooenter 데이터베이스 자격 증명입니다. 온-프레미스 SQL Server가 구성된 방식에 따라 Windows 통합 인증 또는 SQL Server 인증을 사용할 수 있습니다.<br/><br/><b>데이터베이스 쿼리</b>: tooread 원하는 hello 데이터를 설명 하는 SQL 문을 입력 합니다. |
| Azure 테이블 |Hello Azure 저장소의 테이블 서비스에서에서 데이터를 읽습니다.<br/><br/>많은 양의 데이터를 가끔씩만 읽는 경우 Azure 테이블 서비스 hello를 사용 합니다. 이는 유연하고, 비관계형(NoSQL)이고, 확장성이 매우 뛰어나고, 저렴하고, 가용성이 높은 저장소 솔루션을 제공합니다. |hello에 대 한 옵션 hello **데이터 가져오기** 공용 정보 또는 로그인 자격 증명이 필요한 개인 저장소 계정에 액세스 하는지 여부에 따라 변경 합니다. Hello에서 결정 <b>인증 유형을</b> 하며 각각의 고유한 매개 변수 집합이 "PublicOrSAS" 또는 "Account"의 값을 사용할 수 있는 합니다. <br/><br/><b>공용 또는 공유 액세스 서명 (SAS) URI</b>: hello 매개 변수는:<br/><br/><ul><b>테이블 URI</b>: hello 테이블에 대 한 hello 공용 또는 SAS URL을 지정 합니다.<br/><br/><b>속성 이름에 대 한 hello 행 tooscan 지정</b>: hello 값은 <i>TopN</i> tooscan hello 행의 수를 지정 또는 <i>ScanAll</i> hello 테이블에 행이 모든 tooget 합니다. <br/><br/>Hello 데이터 유형이 같은 및 예측 가능한 경우 것이 좋습니다 선택 하면 *TopN* 명사에 대 한 숫자를 입력 합니다. 대형 테이블에 대 한 읽기 시간이 단축 될 수 있습니다 이러한.<br/><br/>Hello 데이터 hello 수준 및 hello 테이블의 위치에 따라 달라 지는 속성 집합으로 구성 하 고, 선택 hello *ScanAll* tooscan 모든 행 옵션입니다. 이 결과 속성 및 메타 데이터 변환의 hello 무결성을 보장 합니다.<br/><br/></ul><b>개인 저장소 계정</b>: hello 매개 변수는: <br/><br/><ul><b>계정 이름</b>: hello 테이블 tooread를 포함 하는 hello 계정의 hello 이름을 지정 합니다.<br/><br/><b>계정 키</b>: hello 계정과 연결 된 hello 저장소 키를 지정 합니다.<br/><br/><b>테이블 이름</b> : hello 데이터 tooread를 포함 하는 hello 테이블의 hello 이름을 지정 합니다.<br/><br/><b>속성 이름에 대 한 행 tooscan</b>: hello 값은 <i>TopN</i> tooscan hello 행의 수를 지정 하거나 <i>ScanAll</i> hello 테이블에 행이 모든 tooget 합니다.<br/><br/>Hello 데이터 유형이 같은 및 예측 가능한 경우 선택 하는 것이 좋습니다 *TopN* 명사에 대 한 숫자를 입력 합니다. 대형 테이블에 대 한 읽기 시간이 단축 될 수 있습니다 이러한.<br/><br/>Hello 데이터 hello 수준 및 hello 테이블의 위치에 따라 달라 지는 속성 집합으로 구성 하 고, 선택 hello *ScanAll* tooscan 모든 행 옵션입니다. 이 결과 속성 및 메타 데이터 변환의 hello 무결성을 보장 합니다.<br/><br/> |
| 데이터 이동 |Azure 저장소에서 이미지, 구조화 되지 않은 텍스트 또는 이진 데이터를 포함 하 여 hello Blob 서비스에 저장 된 데이터를 읽습니다.<br/><br/>Hello Blob 서비스 toopublicly 노출 데이터 또는 tooprivately 스토어 응용 프로그램 데이터를 사용할 수 있습니다. HTTP 또는 HTTPS 연결을 사용하여 어디서나 데이터에 액세스할 수 있습니다. |hello에 대 한 옵션 hello **데이터 가져오기** 공용 정보 또는 로그인 자격 증명이 필요한 개인 저장소 계정에 액세스 하는지 여부에 따라 모듈 변경 합니다. Hello에서 결정 <b>인증 유형을</b> "PublicOrSAS" 또는 "계정"의 값을 사용할 수 있는 합니다.<br/><br/><b>공용 또는 공유 액세스 서명 (SAS) URI</b>: hello 매개 변수는:<br/><br/><ul><b>URI</b>: hello 저장소 blob에 대 한 hello 공용 또는 SAS URL을 지정 합니다.<br/><br/><b>파일 형식을</b>: hello Blob 서비스에에서 hello 데이터의 hello 형식을 지정 합니다. 지원 되는 hello 형식이 CSV, TSV 및 ARFF 않습니다.<br/><br/></ul><b>개인 저장소 계정</b>: hello 매개 변수는: <br/><br/><ul><b>계정 이름</b>: tooread 원하는 hello blob이 포함 된 hello 계정의 hello 이름을 지정 합니다.<br/><br/><b>계정 키</b>: hello 계정과 연결 된 hello 저장소 키를 지정 합니다.<br/><br/><b>경로 toocontainer, 디렉터리 또는 blob </b> : hello 데이터 tooread를 포함 하는 hello blob의 hello 이름을 지정 합니다.<br/><br/><b>Blob 파일 형식</b>: hello blob 서비스에 hello 데이터의 hello 형식을 지정 합니다. hello 지원 되는 데이터 형식은 CSV, TSV, ARFF, CSV에서 지정 된 인코딩 및 Excel 합니다. <br/><br/><ul>Hello 형식이 CSV 또는 TSV 인 경우 hello 파일에는 머리글 행이 포함 되어 있는지 있는지 tooindicate 수 있습니다.<br/><br/>Hello Excel 옵션 tooread Excel 통합 문서에서 데이터를 사용할 수 있습니다. Hello에 <i>Excel 데이터 형식</i> 옵션을 나타내는 hello 데이터를 Excel 워크시트 범위 또는 Excel 테이블입니다. Hello에 <i>Excel 시트 또는 포함 된 테이블 </i>옵션을 hello 시트 또는 tooread에서 원하는 테이블의 hello 이름을 지정 합니다.</ul><br/> |
| 데이터 피드 공급자 |지원되는 피드 공급자에서 데이터를 읽습니다. 현재 유일한 hello Open Data Protocol (OData) 형식을 사용할 수 있습니다. |<b>데이터 콘텐츠 형식</b>: hello OData 형식을 지정 합니다.<br/><br/><b>소스 URL</b>: hello 데이터 피드에 대해 hello 전체 URL을 지정 합니다. <br/>예를 들어 URL 읽기 hello Northwind 샘플 데이터베이스에서 다음을 hello: http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>다음 단계

[데이터 가져오기 및 데이터 내보내기 모듈을 사용하는 Azure ML 웹 서비스 배포](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/
