## <a name="scenario"></a>시나리오
단일 NIC 사용 하 여 VM는 tooa 만들어지고 연결 된 가상 네트워크입니다. 세 가지 hello VM 필요 *개인* IP 주소 및 두 개의 *공용* IP 주소입니다. hello IP 주소를 IP는 구성을 따르고 toohello 할당:

* **IPConfig-1:** *정적* 개인 IP 주소와 *정적* 공용 IP 주소를 할당합니다.
* **IPConfig-2:** *정적* 개인 IP 주소와 *정적* 공용 IP 주소를 할당합니다.
* **IPConfig-3:** *정적* 개인 IP 주소를 할당하고 공용 IP 주소를 할당하지 않습니다.
  
    ![여러 IP 주소](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

hello IP 구성은 hello VM 만들어질 때 NIC를 만들 hello 및 hello NIC가 연결 된 toohello VM 때 관련된 toohello NIC를 됩니다. hello hello 시나리오에 사용 되는 IP 주소 유형은 예시용입니다. 필요한 모든 IP 주소 및 할당 유형을 지정할 수 있습니다.

> [!NOTE]
> 이 문서의 모든 IP 구성을 tooa 할당의 단계를 hello 있지만 단일 NIC 있습니다 여러 IP 구성은 tooany 다중 NIC VM에서 NIC도 할당할 수 있습니다. 여러 Nic 사용 하 여 VM toocreate 읽으려면 어떻게 toolearn hello [여러 nic가 있는 VM을 만들](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) 문서.
