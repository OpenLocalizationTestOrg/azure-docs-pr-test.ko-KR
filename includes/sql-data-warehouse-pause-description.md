
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
toosave 비용을 일시 중지할 수 있습니다 및 다시 시작 요청 시 리소스를 계산 합니다. 예를 들어 사용 하지 않을 hello 데이터베이스 hello 밤 및 주말에, 하는 경우 해당 시간 동안 일시 중지 하 고 hello 일 동안 다시 시작 수 있습니다. Hello 데이터베이스 일시 중지 된 동안 Dwu를 청구 되지는지 않습니다.

데이터베이스를 일시 중지하면

* 계산 및 메모리 리소스 toohello 리소스 풀에 사용할 수 있는 hello 데이터 센터에서 반환
* DWU 비용은 hello hello 일시 중지 기간에 대 한 0입니다.
* 데이터 저장소에는 영향이 없으며 데이터는 그대로 유지됩니다. 
* SQL 데이터 웨어하우스가 실행 중이거나 큐에 있는 모든 작업을 취소합니다.

