### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Hello 가상 컴퓨터에 대 한 TCP 끝점 만들기
Hello에서 순서 tooaccess SQL Server에서에서 인터넷을 hello 가상 컴퓨터는 끝점 toolisten 들어오는 TCP 통신에 있어야 합니다. 이 Azure 구성 단계에서는 들어오는 TCP 포트 트래픽을 tooa TCP 포트를 액세스할 수 있는 toohello 가상 컴퓨터가 안내 합니다.

> [!NOTE]
> Hello 내에서 연결 하는 경우 동일한 클라우드 서비스 또는 가상 네트워크, 않아도 toocreate 공개적으로 액세스할 수 있는 끝점입니다. 이 경우 toohello 다음 단계를 계속할 수 있습니다. 자세한 내용은 [연결 시나리오](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios)를 참조하세요.
> 
> 

1. Hello Azure 포털에서 선택 **가상 컴퓨터 (클래식)**합니다.
2. 그런 후 SQL Server 가상 컴퓨터를 선택합니다.
3. 선택 **끝점**, hello를 클릭 한 다음 **추가** hello hello 끝점 블레이드 위쪽에 단추입니다.
   
    ![포털의 끝점 만들기 단계](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. Hello에 **끝점 추가** 블레이드에서 제공는 **이름** SQLEndpoint 등입니다.
5. 선택 **TCP** hello에 대 한 **프로토콜**합니다.
6. **공용 포트**에 대해 포트 번호(예: **57500**)를 지정합니다.
7. 에 대 한 **개인 포트**, 너무 기본값으로 사용 하는 SQL Server의 수신 대기 포트 지정**1433**합니다.
8. 클릭 **확인** toocreate hello 끝점입니다.

