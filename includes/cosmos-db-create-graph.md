이제 Azure 포털 toocreate 그래프 데이터베이스 hello에 hello 데이터 탐색기 도구를 사용할 수 있습니다. 

1. Hello hello 왼쪽된 탐색 메뉴에서 Azure 포털에서에서 클릭 **데이터 탐색기 (미리 보기)**합니다. 
2. Hello에 **데이터 탐색기 (미리 보기)** 블레이드에서 클릭 **새 그래프**, 다음 정보는 hello를 사용 하 여 hello 페이지를 채웁니다.

    ![Hello Azure 포털에서에서 데이터 탐색기](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    설정|제안 값|설명
    ---|---|---
    데이터베이스 ID|sample-database|새 데이터베이스에 대 한 hello ID입니다. 데이터베이스 이름은 1~255자 사이여야 하며 `/ \ # ?` 또는 후행 공백을 포함할 수 없습니다.
    그래프 ID|sample-graph|새 그래프에 대 한 hello ID입니다. 그래프 이름에는 hello 요구 사항 데이터베이스 id로 문자 동일 합니다.
    저장소 용량| 10 GB|Hello 기본값을 그대로 둡니다. 이 hello 데이터베이스의 저장 용량 hello입니다.
    처리량|400RU|Hello 기본값을 그대로 둡니다. 확장할 수 있습니다 hello 처리량 나중 tooreduce 대기 시간 하려는 경우.
    파티션 키|/userid|데이터를 균등 하 게 배포 하는 파티션 키 tooeach 파티션 합니다. 그래프 hello 올바른 파티션 키가 만드는 성능이 중요 한 선택에 대 한 자세한 [분할에 대 한 디자인](../articles/cosmos-db/partition-data.md#designing-for-partitioning)합니다.

3. Hello 양식에 입력, 클릭 **확인**합니다.
