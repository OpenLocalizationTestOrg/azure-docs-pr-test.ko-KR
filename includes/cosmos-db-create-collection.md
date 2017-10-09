이제 Azure 포털 toocreate 데이터베이스 hello에 hello 데이터 탐색기 도구 및 컬렉션을 사용할 수 있습니다. 

1. Hello hello 왼쪽된 탐색 메뉴에서 Azure 포털에서에서 클릭 **데이터 탐색기 (미리 보기)**합니다. 

2. Hello에 **데이터 탐색기 (미리 보기)** 블레이드에서 클릭 **새 컬렉션**, hello 다음 정보를 제공 합니다.

    ![Azure 포털 데이터 탐색기 블레이드 hello](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    설정|제안 값|설명
    ---|---|---
    데이터베이스 ID|작업|새 데이터베이스에 대 한 hello 이름입니다. 데이터베이스 이름은 1-255자여야 하며, /, \\, #,? 또는 후행 공백은 포함할 수 없습니다.
    컬렉션 ID|항목|새 컬렉션에 대 한 hello 이름입니다. 컬렉션 이름 hello에는 데이터베이스 Id 요구 사항이 동일한 문자입니다.
    저장소 용량| 고정(10GB)|Hello 기본값을 사용 합니다. 이 값은 hello 데이터베이스의 저장 용량 hello입니다.
    처리량|400RU|Hello 기본값을 사용 합니다. Tooreduce 대기 시간을 하려는 경우를 확장할 수 있습니다 hello 처리량 나중입니다.
    파티션 키|/category|데이터를 균등 하 게 배포 하는 파티션 키 tooeach 파티션 합니다. Hello 올바른 파티션 키를 선택 하는 고성능 컬렉션을 만드는 중요 합니다. toolearn 더 참조 [분할에 대 한 디자인](../articles/cosmos-db/partition-data.md#designing-for-partitioning)합니다.    
3. Hello 폼을 완료 한 후 클릭 **확인**합니다.

데이터 탐색기에서는 새 데이터베이스 및 컬렉션 hello 합니다. 
