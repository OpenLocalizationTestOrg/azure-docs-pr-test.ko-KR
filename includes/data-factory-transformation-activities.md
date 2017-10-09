Azure Data Factory 변환 활동이 추가 된 toopipelines 하거나 개별적으로 되거나 되 연결 된 다른 활동을 포함 하는 hello를 지원 합니다.

| 데이터 변환 작업 | 컴퓨팅 환경 |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop 스트리밍](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Machine Learning 작업: 배치 실행 및 업데이트 리소스](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [저장 프로시저](../articles/data-factory/data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL 데이터 웨어하우스 또는 SQL Server |
| [데이터 레이크 분석 U-SQL](../articles/data-factory/data-factory-usql-activity.md) |Azure 데이터 레이크 분석 |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |HDInsight [Hadoop] 또는 Azure Batch |

> [!NOTE]
> MapReduce 작업 toorun Spark 프로그램 HDInsight Spark 클러스터에서 사용할 수 있습니다. 자세한 내용은 [Azure Data Factory에서 Spark 프로그램 호출](../articles/data-factory/data-factory-spark.md) 을 참조하세요.
> 만들 수 있습니다는 사용자 지정 활동 toorun R 스크립트에서 HDInsight 클러스터에 설치 된 R을 사용. [Azure Data Factory를 사용하여 R 스크립트 실행](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)을 참조하세요.
> 
> 

