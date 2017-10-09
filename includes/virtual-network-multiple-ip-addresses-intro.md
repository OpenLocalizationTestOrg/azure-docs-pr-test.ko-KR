> [!div class="op_single_selector"]
> * [포털](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [CLI 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [템플릿](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Azure 가상 컴퓨터 (VM) 두 개 이상 있어 더 많은 네트워크 인터페이스 (NIC) tooit 연결 합니다. 정적 또는 동적 공용 및 개인 IP 주소 할당된 tooit 하거나 NIC 하나 할 수도 있습니다. 주소 tooa VM을 여러 IP를 할당 hello를 다음 기능을 통해 수 있습니다.

* 단일 서버에서 IP 주소와 SSL 인증서를 사용하여 여러 웹 사이트 또는 서비스를 호스트할 수 있습니다.
* 방화벽 또는 부하 분산 장치와 같은 네트워크 가상 어플라이언스로 사용됩니다.
* 안녕 기능 tooadd hello Nic tooan Azure 부하 분산 장치 백 엔드 풀에 대 한 모든 hello 개인 IP 주소. 만 hello 지나서 hello 기본 NIC 수 hello에 대 한 기본 IP 주소 tooa 백 엔드 풀을 추가 합니다. hello을 읽을 수 tooload 여러 IP 구성은 균형을 조정 하는 방법에 대해 더 알아봅니다 toolearn [부하 분산 여러 IP 구성은](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.

모든 연결 된 NIC tooa VM 두 개 이상 있어 tooit 더 많은 IP 구성에 연결 합니다. 각 구성에는 하나의 정적 또는 동적 개인 IP 주소가 할당됩니다. 각 구성은 한 공용 IP 주소 연결 리소스 tooit이 있을 수 있습니다. 공용 IP 주소 리소스 중 하나는 동적 또는 정적 공용 IP 주소 할당 tooit에 있습니다. Azure에서 toolearn IP에 대 한 주소, hello 읽기 [Azure의 IP 주소](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) 문서. 

제한 toohow 많은 개인 IP는 tooa NIC. 주소를 할당할 수 있습니다 이기도 한도 toohow Azure 구독에서 사용할 수 있는 많은 공용 IP 주소입니다. Hello 참조 [Azure 제한](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) 을 참조 합니다.
