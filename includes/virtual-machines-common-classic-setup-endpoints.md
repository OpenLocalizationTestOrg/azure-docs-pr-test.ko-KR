
각 끝점에는 *공용 포트*와 *개인 포트*가 있습니다.

* hello 공용 포트는 hello 인터넷에서에서 들어오는 트래픽 toohello 가상 컴퓨터에 대 한 hello Azure 부하 분산 장치 toolisten에서 사용 됩니다.
* hello 개인 포트는 들어오는 트래픽을, 일반적으로 보내는 tooan 응용 프로그램 또는 hello 가상 컴퓨터에서 실행 중인 서비스에 대 한 가상 컴퓨터 toolisten hello에서 사용 됩니다.

에 대 한 기본값 hello IP 프로토콜 및 잘 알려진 네트워크 프로토콜에 대 한 TCP 또는 UDP 포트는 Azure 포털 hello로 끝점을 만들 때 제공 됩니다. 사용자 지정 끝점에 대 한 toospecify hello 올바른 IP 프로토콜 (TCP 또는 UDP)와 hello 공용 및 개인 포트가 필요 합니다. 여러 가상 컴퓨터에서 임의로 toodistribute 들어오는 트래픽을 해야 toocreate 여러 끝점 구성 된 부하 분산 된 집합을 합니다.

끝점을 만든 후에 허용 또는 거부 hello 들어오는 트래픽을 원본 IP 주소에 기반 하는 hello 끝점의 공용 포트 toohello 하는 액세스 제어 목록 (ACL) toodefine 규칙을 사용할 수 있습니다. 그러나 hello 가상 컴퓨터가 Azure 가상 네트워크에 있는 경우에 네트워크 보안 그룹 대신 사용 해야 합니다. 자세한 내용은 [네트워크 보안 그룹 정보](../articles/virtual-network/virtual-networks-nsg.md)를 참조하세요.

> [!NOTE]
> Azure가 자동으로 설정하는 원격 연결 끝점과 연결된 포트에 대해서는 Azure 가상 컴퓨터의 방화벽 구성이 자동으로 수행됩니다. 다른 모든 끝점에 대해 지정 된 포트에 대 한 구성 없이 자동으로 수행 됩니다 hello 가상 컴퓨터의 방화벽 toohello 합니다. Hello 가상 컴퓨터에 대 한 끝점을 만들 때 hello 가상 컴퓨터의 방화벽 hello tooensure hello 프로토콜 및 개인 포트 해당 toohello 끝점 구성에 대 한 hello 트래픽을 수도 있습니다. tooconfigure는 방화벽 hello, hello 설명서 또는 hello 가상 컴퓨터에서 실행 하는 hello 운영 체제에 대 한 온라인 도움말을 참조 하세요.
>
>

## <a name="create-an-endpoint"></a>끝점 만들기
1. 그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **가상 컴퓨터**, 한 다음 원하는 tooconfigure hello 가상 컴퓨터의 hello 이름을 클릭 하 고 있습니다.
3. 클릭 **끝점** hello에 **설정을** 그룹입니다. hello **끝점** 페이지 hello 가상 컴퓨터에 대 한 모든 hello 현재 끝점을 나열 합니다. (이 예제는 Windows VM입니다. Linux VM에는 기본적으로 SSH용 끝점이 표시됩니다.)

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![끝점](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. Hello 끝점 항목 위에 hello 명령 모음에서 **추가**합니다.
5. Hello에 **끝점 추가** 페이지에 hello 끝점에 대 한 이름을 입력 합니다 **이름**합니다.
6. **프로토콜**에서 **TCP** 또는 **UDP**를 선택합니다.
7. **공용 포트**, hello 인터넷에서에서 들어오는 트래픽 hello에 대 한 hello 포트 번호를 입력 합니다. **개인 포트**, 가상 컴퓨터는 hello에 수신 hello 포트 번호를 입력 합니다. 이러한 포트 번호는 다를 수 있습니다. 해당 hello 확인 (6 단계)에서 구성 된 tooallow hello 트래픽 해당 toohello 프로토콜 및 개인 포트 hello 가상 컴퓨터 방화벽에 되었습니다.
10. **Ok**를 클릭합니다.

새 끝점의 hello hello에 나열 됩니다 **끝점** 페이지.

![끝점 만들기 성공](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>끝점에서 ACL hello 관리
트래픽을 보낼 수 있는 컴퓨터 toodefine hello 집합, 끝점에서 ACL hello 원본 IP 주소를 기준으로 트래픽을 제한할 수 있습니다. 이러한 단계 tooadd를 수행 하 고, 수정 또는 끝점에 대 한 ACL을 제거 합니다.

> [!NOTE]
> Hello 끝점에 부하 분산 집합의 일부 이면 하면 변경 끝점에서 ACL은 toohello 적용된 tooall 끝점 hello 집합에 있습니다.
>
>

Hello 가상 컴퓨터가 Azure 가상 네트워크에, Acl 대신 네트워크 보안 그룹을 권장 합니다. 자세한 내용은 [네트워크 보안 그룹 정보](../articles/virtual-network/virtual-networks-nsg.md)를 참조하세요.

1. 그렇게 이미 하지 않은 경우 toohello Azure 포털에에서 로그인 합니다.
2. 클릭 **가상 컴퓨터**, 한 다음 원하는 tooconfigure hello 가상 컴퓨터의 hello 이름을 클릭 하 고 있습니다.
3. **Endpoints**를 클릭합니다. Hello 목록에서 hello 적절 한 끝점을 선택 합니다. hello ACL 목록은 hello hello 페이지 맨 아래에 있습니다.

   ![ACL 세부 정보 지정](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. ACL에 대 한 hello 목록 tooadd, 삭제 또는 편집 규칙의 행을 사용 하 고 해당 순서를 변경 합니다. hello **원격 서브넷** 값은 hello Azure 부하 분산 장치 사용 하 여 toopermit hello 또는 원본 IP 주소를 기반으로 하는 hello 트래픽을 거부 하는 인터넷에서에서 들어오는 트래픽에 대 한 IP 주소 범위입니다. CIDR 형식으로 주소 접두사 형식이 라고도 있는지 toospecify hello IP 주소 범위 여야 합니다. 예는 `10.1.0.0/8`입니다.

 ![새 ACL 항목](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


규칙 tooallow 트래픽만 hello 인터넷 또는 toodeny 트래픽을 특정 한 알려진 주소 범위에서 tooyour 컴퓨터에 해당 하는 특정 컴퓨터에서 사용할 수 있습니다.

hello 규칙은 첫 번째 규칙의 hello로 시작 하 고 hello 마지막 규칙으로 끝나는 순서로 평가 됩니다. 즉, 규칙 가장 제한이 적은 toomost 제한적인에서 정렬 되어야 합니다. 예제 및 자세한 내용은 [네트워크 액세스 제어 목록이란](../articles/virtual-network/virtual-networks-acl.md)을 참조하세요.
