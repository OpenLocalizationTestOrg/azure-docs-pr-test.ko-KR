이 단계에서는 hello에서 실행 되는 클라이언트 응용 프로그램을 사용 하 여 hello 가용성 그룹 수신기를 테스트 같은 네트워크입니다.

클라이언트 연결 요구 사항을 준수 하는 hello에 있습니다.

* 클라이언트 연결 toohello 수신기 호스트 hello Always On 가용성 복제본을 하나 hello 보다 다른 클라우드 서비스에 있는 컴퓨터에서 가져와야 합니다.
* 클라이언트를 지정 해야 하는 경우 hello Always On 복제본이 다른 서브넷에, *MultisubnetFailover = True* hello 연결 문자열에 있습니다. 이러한 조건으로 인해 병렬 연결 tooreplicas hello에 다양 한 서브넷을 시도 합니다. 이 시나리오에는 지역 간 AlwaysOn 가용성 그룹 배포가 포함됩니다.

한 가지 예는 tooconnect toohello 수신기 hello에 hello Vm 중 하나에서 동일한 Azure 가상 네트워크 (제외 하 고 복제본을 호스트). 쉽게 toocomplete이이 테스트 tootry tooconnect SQL Server Management Studio toohello 가용성 그룹 수신기가 있습니다. 또 다른 간단한 방법은 toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx), 다음과 같습니다.

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Hello EndpointPort 값 이면 *1433*, 필요한 toospecify 없는 hello 호출에서. hello 이전 호출 또한 가정 hello 클라이언트 컴퓨터에는 조인 된 toohello 동일한 도메인 및 hello 호출자에 게 해당 권한이 부여 되었는지 hello 데이터베이스에서 Windows 인증을 사용 하 여 합니다.
> 
> 

Hello 수신기를 테스트 하는 경우 클라이언트에서는 장애 조치 toohello 수신기를 연결할 수 있습니다. 있는지 hello 가용성 그룹 toomake 통해 있는지 toofail 수 있습니다.

