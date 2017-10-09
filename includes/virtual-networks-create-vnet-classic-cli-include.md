## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>어떻게 toocreate Azure CLI를 사용 하 여 클래식 VNet
Hello Azure CLI toomanage hello 명령 프롬프트에서 Windows, Linux 또는 OSX를 실행 하는 컴퓨터에서 Azure 리소스를 사용할 수 있습니다. toocreate hello Azure CLI를 사용 하 여 VNet 아래 hello 단계를 따릅니다.

1. Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../articles/cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.
2. Hello 실행 **azure 네트워크 vnet 만들기** 명령 toocreate VNet 서브넷에 다음과 같이 합니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    예상 출력:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. 만든 hello VNet toobe의 이름입니다. 이 시나리오에서는 *TestVNet*
   * **-e(또는 --address-space)**. VNet 주소 공간입니다. 이 시나리오에서는 *192.168.0.0*
   * **-i(또는 -cidr)**. CIDR 형식의 네트워크 마스크입니다. 이 시나리오에서는 *16*입니다.
   * **-n(또는 --subnet-name**). Hello 첫 번째 서브넷의 이름입니다. 이 시나리오에서는 *FrontEnd*입니다.
   * **-p(또는 --subnet-start-ip)**. 서브넷 또는 서브넷 주소 공간의 시작 IP 주소입니다. 이 시나리오에서는 *192.168.1.0*입니다.
   * **-r(또는 --subnet-cidr)**. 서브넷에 대한 CIDR 형식의 네트워크 마스크입니다. 이 시나리오에서는 *24*입니다.
   * **-l(또는 --location)**. Azure 지역 VNet hello 만들어집니다. 이 시나리오에서는 *Central US*입니다.
3. Hello 실행 **만드는 azure 네트워크 vnet 서브넷** 명령 toocreate 아래와 같이 서브넷입니다. hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    다음은 위의 hello 명령에 대 한 예상 hello 출력이입니다.
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t(또는 --vnet-name)**. Hello hello 서브넷을 만들 수는 VNet의 이름입니다. 이 시나리오에서는 *TestVNet*입니다.
   * **-n (or --name)**. Hello 새 서브넷의 이름입니다. 이 시나리오에서는 *BackEnd*입니다.
   * **-a(또는 --address-prefix)**. 서브넷 CIDR 블록입니다. 이 시나리오에서는 *192.168.2.0/24*입니다.
4. Hello 실행 **azure 네트워크 vnet 표시** 아래와 같이 hello 새 vnet의 tooview hello 속성 명령입니다.
   
            azure network vnet show
   
    다음은 위의 hello 명령에 대 한 예상 hello 출력이입니다.
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

