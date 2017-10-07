---
title: "Azure 기계 학습에 대 한 고급 분석 시나리오 aaaIdentify | Microsoft Docs"
description: "이렇게 하면 고급 팀 데이터 과학 프로세스 hello로 예측 분석에 대 한 hello 적절 한 시나리오를 선택 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Azure 기계 학습의 고급 분석 시나리오
이 문서에서는 hello 다양 한 예제 데이터 원본 및 hello에서 처리 될 수 있는 대상 시나리오를 설명 [팀 데이터 과학 프로세스 (TDSP)](data-science-process-overview.md)합니다. hello TDSP 팀 toocollaborate 지능형 응용 프로그램을 구축에 대 한 체계적인 방법을 제공 합니다. 여기에 제시 된 hello 시나리오 hello 데이터 특징별, 소스 위치 및 Azure에서 대상 저장소에 종속 된 hello 데이터 처리 워크플로에서 사용할 수 있는 옵션을 보여 줍니다.

hello **의사 결정 트리** hello 마지막 섹션에 표시 된 데이터와 목표에 적합 한 hello 샘플 시나리오를 선택 하면에 대 한 합니다.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

각각 hello 다음 섹션의 예제 시나리오를 제공 합니다. 각 시나리오에 대해 가능한 데이터 과학 또는 고급 분석 흐름 및 지원되는 Azure 리소스가 나열되어 있습니다.

> [!NOTE]
> **모든 hello 다음 시나리오에 대 한 해야 합니다.**
> <br/>
> 
> * [저장소 계정 만들기](../storage/common/storage-create-storage-account.md)
>   <br/>
> * [Azure 기계 학습 작업 영역 만들기](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>시나리오 \#1: 로컬 파일에 작은 toomedium 표 형식 데이터 집합
![작은 toomedium 로컬 파일][1]

#### <a name="additional-azure-resources-none"></a>추가 Azure 리소스: 없음
1. Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.
2. 데이터 집합을 업로드합니다.
3. 데이터 집합을 업로드한 Azure 컴퓨터 학습 실험 흐름을 작성합니다.

## <a name="smalllocalprocess"></a>시나리오 \#2: 처리를 필요로 하는 로컬 파일의 작은 toomedium 데이터 집합
![처리를 사용 하 여 작은 toomedium 로컬 파일][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>추가 Azure 리소스: Azure 가상 컴퓨터 (IPython Notebook 서버)
1. IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.
2. 데이터 tooan Azure storage 컨테이너를 업로드 합니다.
3. IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure 저장소 컨테이너에서 데이터에 액세스합니다.
4. 테이블 형식, 데이터 toocleaned를 변환 합니다.
5. Azure Blob에 변환된 데이터를 저장합니다.
6. Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.
7. Hello를 사용 하 여 Azure blob에서 hello 데이터 읽기 [데이터 가져오기] [ import-data] 모듈입니다.
8. 수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.

## <a name="largelocal"></a>시나리오 \#3: 로컬 파일에서 큰 데이터 집합, Azure Blob을 대상으로 함
![큰 로컬 파일][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>추가 Azure 리소스: Azure 가상 컴퓨터 (IPython Notebook 서버)
1. IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.
2. 데이터 tooan Azure storage 컨테이너를 업로드 합니다.
3. IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure Blob에서 데이터에 액세스합니다.
4. 필요한 경우 데이터 toocleaned, 테이블 형식 변환 합니다.
5. 데이터를 탐색하고 필요에 따라 기능을 만듭니다.
6. 중소 데이터 샘플을 추출합니다.
7. Azure blob에 hello 샘플링 된 데이터를 저장 합니다.
8. Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.
9. Hello를 사용 하 여 Azure blob에서 hello 데이터 읽기 [데이터 가져오기] [ import-data] 모듈입니다.
10. 수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.

## <a name="smalllocaltodb"></a>시나리오 \#4: Azure 가상 컴퓨터에서 SQL Server를 대상으로 하는 로컬 파일의 작은 toomedium 데이터 집합
![Azure에서 작은 toomedium 로컬 파일 tooSQL DB][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)
1. SQL Server + IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.
2. 데이터 tooan Azure storage 컨테이너를 업로드 합니다.
3. IPython Notebook을 사용하여 Azure 저장소 컨테이너에서 데이터를 사전 처리하고 정리합니다.
4. 필요한 경우 데이터 toocleaned, 테이블 형식 변환 합니다.
5. 데이터 tooVM 로컬 파일 저장 (IPython 노트북 VM에서 실행 되 고, 로컬 드라이브 tooVM 드라이브 참조).
6. Azure VM에서 실행 되는 데이터 tooSQL 서버 데이터베이스를 로드 합니다.
   
   옵션 \#1: SQL Server Management Studio 사용.
   
   * 로그인 tooSQL 서버 VM
   * SQL Server Management Studio를 실행합니다.
   * 데이터베이스 및 대상 테이블을 만듭니다.
   * VM-로컬 파일에서 메서드 tooload hello 데이터를 가져오기 하는 hello 대량 중 하나를 사용 합니다.
   
   옵션 \#2: IPython Notebook 사용 – 중간 및 대규모 데이터 집합을 권장하지 않음
   
   <!-- -->    
   * ODBC 연결 문자열 tooaccess SQL Server VM에서 사용 합니다.
   * 데이터베이스 및 대상 테이블을 만듭니다.
   * VM-로컬 파일에서 메서드 tooload hello 데이터를 가져오기 하는 hello 대량 중 하나를 사용 합니다.
7. 데이터를 탐색하고 필요에 따라 기능을 만듭니다. 참고 hello 기능 toobe hello 데이터베이스 테이블에서 구체화 필요 하지 않습니다. Hello 필요한 쿼리 toocreate을 확인만 해당 합니다.
8. 필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.
9. Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.
10. 읽기 hello 데이터 직접에서 hello hello를 사용 하 여 SQL Server [데이터 가져오기] [ import-data] 모듈입니다. 필드를 추출 하는 붙여넣기 hello 필요한 쿼리 기능을 만들고 직접 hello에에서 필요한 경우 데이터를 샘플링 [데이터 가져오기] [ import-data] 쿼리 합니다.
11. 수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.

## <a name="largelocaltodb"></a>시나리오 \#5: 로컬 파일의 큰 데이터 집합, Azure VM의 SQL Server를 대상으로 함
![Azure의 큰 로컬 파일 tooSQL DB][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)
1. SQL Server 및 IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.
2. 데이터 tooan Azure storage 컨테이너를 업로드 합니다.
3. (선택 사항) 데이터를 사전 처리하고 정리합니다.
   
   a.  IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure에서 데이터에 액세스합니다.
   
       blobs.
   
   b.  필요한 경우 데이터 toocleaned, 테이블 형식 변환 합니다.
   
   c.  데이터 tooVM 로컬 파일 저장 (IPython 노트북 VM에서 실행 되 고, 로컬 드라이브 tooVM 드라이브 참조).
4. Azure VM에서 실행 되는 데이터 tooSQL 서버 데이터베이스를 로드 합니다.
   
   a.  로그인 tooSQL 서버 VM입니다.
   
   b.  데이터를 저장하지 경우, Azure에서 데이터 파일을 다운로드합니다.
   
       storage container toolocal-VM folder.
   
   c.  SQL Server Management Studio를 실행합니다.
   
   d.  데이터베이스 및 대상 테이블을 만듭니다.
   
   e.  Hello 대량 중 하나를 사용 방법을 tooload hello 데이터를 가져옵니다.
   
   f.  테이블 조인에 필요한 경우 인덱스 tooexpedite 조인을 만듭니다.
   
   > [!NOTE]
   > 큰 데이터 크기의 더 빠른 로드에 대 한 분할 된 테이블 만들고 hello 데이터 병렬로 대량 좋습니다. 자세한 내용은 참조 [병렬 데이터 가져오기 tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)합니다.
   > 
   > 
5. 데이터를 탐색하고 필요에 따라 기능을 만듭니다. 참고 hello 기능 toobe hello 데이터베이스 테이블에서 구체화 필요 하지 않습니다. Hello 필요한 쿼리 toocreate을 확인만 해당 합니다.
6. 필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.
7. Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.
8. 읽기 hello 데이터 직접에서 hello hello를 사용 하 여 SQL Server [데이터 가져오기] [ import-data] 모듈입니다. 필드를 추출 하는 붙여넣기 hello 필요한 쿼리 기능을 만들고 직접 hello에에서 필요한 경우 데이터를 샘플링 [데이터 가져오기] [ import-data] 쿼리 합니다.
9. 업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작

## <a name="largedbtodb"></a>시나리오 \#6: 온-프레미스의 SQL 서버 데이터베이스의 큰 데이터 집합, Azure 가상 컴퓨터의 SQL Server를 대상으로 함
![대형 SQL DB 온-프레미스 tooSQL DB Azure에서][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)
1. SQL Server 및 IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.
2. Hello 데이터 중 하나 사용 하 여 SQL Server toodump 파일에서 메서드 tooexport hello 데이터를 내보냅니다.
   
   > [!NOTE]
   > 대체 (빠른) 메서드 toomove hello 전체 데이터베이스 toothe SQL Server 인스턴스로 Azure의 hello 온-프레미스 데이터베이스에서 모든 데이터 toomove를 결정 합니다. Hello 단계 tooexport 데이터, 데이터베이스 및 부하/가져오기 데이터 toohello 대상 데이터베이스 만들기를 건너뛰고 hello 대체 방법에 따라 합니다.
   > 
   > 
3. 덤프 파일 tooAzure 저장소 컨테이너를 업로드 합니다.
4. Azure 가상 컴퓨터에서 실행 하는 hello 데이터 tooa SQL Server 데이터베이스를 로드 합니다.
   
   a.  SQL Server VM toohello를 로그인 합니다.
   
   b.  Azure 저장소 컨테이너 toohello VM 로컬 폴더에서 데이터 파일을 다운로드 합니다.
   
   c.  SQL Server Management Studio를 실행합니다.
   
   d.  데이터베이스 및 대상 테이블을 만듭니다.
   
   e.  Hello 대량 중 하나를 사용 방법을 tooload hello 데이터를 가져옵니다.
   
   f.  테이블 조인에 필요한 경우 인덱스 tooexpedite 조인을 만듭니다.
   
   > [!NOTE]
   > 큰 데이터 크기의 더 빠른 로드에 대 한 동시에 분할 된 테이블 및 toobulk 가져오기 hello 데이터를 만듭니다. 자세한 내용은 참조 [병렬 데이터 가져오기 tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)합니다.
   > 
   > 
5. 데이터를 탐색하고 필요에 따라 기능을 만듭니다. 참고 hello 기능 toobe hello 데이터베이스 테이블에서 구체화 필요 하지 않습니다. Hello 필요한 쿼리 toocreate을 확인만 해당 합니다.
6. 필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.
7. Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.
8. 읽기 hello 데이터 직접에서 hello hello를 사용 하 여 SQL Server [데이터 가져오기] [ import-data] 모듈입니다. 필드를 추출 하는 붙여넣기 hello 필요한 쿼리 기능을 만들고 직접 hello에에서 필요한 경우 데이터를 샘플링 [데이터 가져오기] [ import-data] 쿼리 합니다.
9. 업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>대체 방법 toocopy 온-프레미스 SQL Server tooAzure SQL 데이터베이스에서에서 전체 데이터베이스
![Local DB를 분리 하 고 Azure에서 DB tooSQL 연결][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)
tooreplicate hello 전체 SQL Server 데이터베이스의 SQL Server VM을 복사 해야 데이터베이스에서 한 위치/서버 tooanother 해당 hello 데이터베이스를 일시적으로 오프 라인 수 것으로 가정 합니다. SQL Server Management Studio 개체 탐색기 hello 또는 hello 동등한 TRANSACT-SQL 명령을 사용 하 여이 작업을 수행 합니다.

1. Hello 원본 위치에서 hello 데이터베이스를 분리 합니다. 자세한 내용은 [데이터베이스 분리](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx)를 참조하세요.
2. Windows 탐색기나 Windows 명령 프롬프트 창에서 복사 hello 데이터베이스 파일 및 로그 파일을 Azure에서 SQL Server VM hello 파일 toohello 대상 위치를 분리 합니다.
3. 복사 하는 hello 파일 toohello 대상 SQL Server 인스턴스에 연결 합니다. 자세한 내용은 [데이터베이스 연결](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx)을 참조하세요.

[분리 및 연결을 사용하여 데이터베이스 이동(Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>시나리오 \#7: 로컬 파일의 빅 데이터, Azure HDInsight Hadoop 클러스터의 Hive 데이터베이스를 대상으로 함
![로컬 대상 Hive의 빅 데이터][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>추가 Azure 리소스: Azure HDInsight Hadoop 클러스터 및 Azure Virtual Machine(IPython Notebook 서버)
1. IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.
2. Azure HDInsight Hadoop 클러스터를 만듭니다.
3. (선택 사항) 데이터를 사전 처리하고 정리합니다.
   
   a.  IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure에서 데이터에 액세스합니다.
   
       blobs.
   
   b.  필요한 경우 데이터 toocleaned, 테이블 형식 변환 합니다.
   
   c.  데이터 tooVM 로컬 파일 저장 (IPython 노트북 VM에서 실행 되 고, 로컬 드라이브 tooVM 드라이브 참조).
4. Hello 2 단계에서 선택한 hello Hadoop 클러스터의 데이터 toohello 기본 컨테이너를 업로드 합니다.
5. Azure HDInsight Hadoop 클러스터에서 데이터 tooHive 데이터베이스를 로드 합니다.
   
   a.  Hello Hadoop 클러스터의 헤드 노드 toohello 로그인
   
   b.  Hadoop 명령줄 hello를 엽니다.
   
   c.  명령에 의해 hello Hive 루트 디렉터리를 입력 `cd %hive_home%\bin` 에서 Hadoop 명령줄입니다.
   
   d.  Hello 하이브 쿼리 toocreate 데이터베이스 및 테이블을 실행 하 고 blob 저장소 tooHive 테이블에서 데이터를 로드 합니다.
   
   > [!NOTE]
   > Hello 데이터 크기가 크면 사용자 파티션이 있는 hello Hive 테이블을 만들 수 있습니다. 그런 다음, 사용자가 사용할 수는 `for` hello 하이브 테이블 파티션에 의해 분할에 헤드 노드 tooload 데이터 hello에 hello Hadoop 명령줄에서에서 루프입니다.
   > 
   > 
6. Hadoop 명령줄에서 데이터를 탐색하고 필요에 따라 기능을 만듭니다. 참고 hello 기능 toobe hello 데이터베이스 테이블에서 구체화 필요 하지 않습니다. Hello 필요한 쿼리 toocreate을 확인만 해당 합니다.
   
   a.  Hello Hadoop 클러스터의 헤드 노드 toohello 로그인
   
   b.  Hadoop 명령줄 hello를 엽니다.
   
   c.  명령에 의해 hello Hive 루트 디렉터리를 입력 `cd %hive_home%\bin` 에서 Hadoop 명령줄입니다.
   
   d.  Hello Hadoop 클러스터 tooexplore hello 데이터의 hello 헤드 노드에서 hello 하이브 쿼리 Hadoop 명령 줄에서 실행 하 고 필요에 따라 기능을 만듭니다.
7. 필요한 경우 원하는, Azure 기계 학습 스튜디오에서 데이터 toofit hello 샘플.
8. Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.
9. Hello에서 직접 hello 데이터를 읽는 `Hive Queries` hello를 사용 하 여 [데이터 가져오기] [ import-data] 모듈입니다. 필드를 추출 하는 붙여넣기 hello 필요한 쿼리 기능을 만들고 직접 hello에에서 필요한 경우 데이터를 샘플링 [데이터 가져오기] [ import-data] 쿼리 합니다.
10. 업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작

## <a name="decisiontree"></a>시나리오 선택 의사 결정 트리
- - -
hello 다음 다이어그램 위에서 설명한 hello 시나리오 및 요약 hello 고급 분석 프로세스 및 기술 선택한 내용을 tooeach 항목별로 hello 시나리오를 사용 하는 합니다. 데이터 처리, 탐색, 기능 엔지니어링 및 샘플링 걸릴 수 있습니다는 하나 또는 중간 hello 소스에서 / 환경-메서드 및/또는 더 – 대상 환경에 배치한 필요에 따라 반복적으로 진행할 수 있습니다. 만 hello 다이어그램 일부 가능한 흐름을 사용 하 게 되 고 철저 한 열거형을 제공 하지 않습니다.

![샘플 DS 프로세스 연습 시나리오][8]

### <a name="advanced-analytics-in-action-examples"></a>고급 분석 작동 예제
사용 하는 종단 간 Azure 기계 학습 연습에 대 한 hello 고급 분석 프로세스 및 기술 공용 데이터 집합을 사용 하 여 다음을 참조 하십시오.

* [실행 중인 팀 데이터 과학 프로세스: SQL Server 사용](machine-learning-data-science-process-sql-walkthrough.md)
* [실행 중인 팀 데이터 과학 프로세스: HDInsight Hadoop 클러스터 사용](machine-learning-data-science-process-hive-walkthrough.md)

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
