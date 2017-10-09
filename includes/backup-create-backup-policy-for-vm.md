## <a name="defining-a-backup-policy"></a>백업 정책 정의
백업 정책을 및의 행렬을 hello 데이터 스냅숏을 만드는 경우, 해당 스냅숏으로 보관 하는 기간을 정의 합니다. VM 백업을 위한 정책을 정의할 때 백업 작업을 *하루에 한 번*트리거할 수 있습니다. 새 정책을 만들 때 적용 된 toohello 자격 증명 모음 됩니다. hello 백업 정책 인터페이스는 다음과 같습니다.

![백업 정책](./media/backup-create-policy-for-vms/backup-policy.png)

toocreate 정책:

1. Hello에 대 한 이름을 입력 **정책 이름**합니다.
2. 데이터의 스냅숏을 매일 또는 매주 간격으로 생성할 수 있습니다. 사용 하 여 hello **백업 빈도** 드롭 다운 메뉴 toochoose 여부 데이터 스냅숏을 매일 또는 매주입니다.
   
   * 일 단위 간격을 선택 하면 hello 스냅숏에 대 한 강조 표시 하는 hello 제어 tooselect hello 시간 hello 사용 합니다. toochange hello 시간 hello 시간을 선택 취소 하 고 hello 새 시간을 선택 합니다.
     
     ![매일 백업 정책](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * 주별 간격을 선택 하면 hello 강조 표시 된 컨트롤 tooselect hello 요일 hello, hello 스냅숏의 시간 일 tootake hello 사용 합니다. Hello 일 메뉴에서 하나 또는 여러 날짜를 선택 합니다. Hello 시간 메뉴에서 한 시간을 선택 합니다. toochange hello 시간 hello 선택 된 시간을 선택 취소 하 고 hello 새 시간을 선택 합니다.
     
     ![매주 백업 정책](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. 기본적으로 모든 **보존 범위** 옵션이 선택되어 있습니다. 보존 범위 제한이 toouse 하지 않으려면 선택을 취소 합니다. 그런 다음 hello interval(s) toouse를 지정 합니다.
   
    매월 및 매년 보존 범위는 주간 또는 일간 증분 기반 toospecify hello 스냅숏을 허용 합니다.
   
   > [!NOTE]
   > VM을 보호하는 경우, 백업 작업이 하루에 한 번 실행됩니다. 때 hello 백업 실행은 hello 동일 각 보존 범위에 대 한 hello 시간입니다.
   > 
   > 
4. Hello 정책에 대 한 모든 옵션을 설정한 후 hello의 위쪽 hello 블레이드 클릭 **저장**합니다.
   
    hello 새 정책이 즉시 적용 된 toohello 자격 증명 모음입니다.

