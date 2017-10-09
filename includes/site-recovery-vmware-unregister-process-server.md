hello 단계 toounregister 프로세스 서버가 구성 서버 hello로 연결 상태에 따라 달라 집니다.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>연결된 상태인 프로세스 서버 등록 취소

1. 원격 관리자 권한으로 프로세스 서버 hello로 연결 합니다.
2. Hello 시작 **제어판** 엽니다 **프로그램 > 프로그램 제거**
3. Hello 이름별 프로그램 제거 **Microsoft Azure 사이트 복구 구성/프로세스 서버**
4. 3단계가 완료되면 **Microsoft Azure Site Recovery 구성/프로세스 서버**를 제거할 수 있습니다.

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>연결 해제된 상태인 프로세스 서버 등록 취소

> [!WARNING]
> 프로세스 서버가 설치 되어 있는 hello 없는 방식으로 toorevive hello 가상 컴퓨터인 경우 아래 단계에 사용 하 여 hello는 사용 해야 합니다.

1. 관리자 권한으로 tooyour 구성 서버에 로그온 합니다.
2. 관리 명령 프롬프트를 열고 toohello 디렉터리 찾아보기 `%ProgramData%\ASR\home\svsystems\bin`합니다.
3. 이제 hello 명령을 실행 합니다.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Hello 프로세스 서버 hello 세부 정보를 제거할이 hello 시스템에서 됩니다.
