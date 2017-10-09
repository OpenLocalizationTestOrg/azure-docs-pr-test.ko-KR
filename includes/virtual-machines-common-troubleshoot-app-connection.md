시작 또는 Azure 가상 컴퓨터 (VM)에서 실행 되는 tooan 응용 프로그램을 연결 하는 경우에 여러 가지가 이유가 있습니다. 이유는 hello 응용 프로그램 실행 되 고 있지를 포함 하거나, 차단 또는 올바르게 하지 트래픽 toohello 응용 프로그램을 전달 하는 규칙을 네트워킹 수신 대기 포트 hello 예상 hello 포트에서 수신 합니다. 이 문서에서는 체계적인 방법 toofind 및 올바른 hello 문제를 설명 합니다.

Tooyour VM 연결 문제가 발생 하는 경우 RDP 또는 SSH를 사용 하 여 먼저 문서 hello 다음 중 하나를 참조 하십시오.

* [원격 데스크톱 연결 tooa Windows 기반 Azure 가상 컴퓨터 문제 해결](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [SSH (보안 셸) 연결 tooa Linux 기반 Azure 가상 컴퓨터 문제를 해결](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)합니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../articles/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다. 이 문서에서는 두 모델을 사용 하 여 있지만 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 선택 **Get Support**합니다.

## <a name="quick-start-troubleshooting-steps"></a>빠른 시작 문제 해결 단계
Tooan 응용 프로그램을 연결 하는 데 문제가 있으면 hello 일반 문제 해결 단계를 수행 하십시오. 각 단계를 수행 하면 연결 tooyour 응용 프로그램을 다시 시도 하십시오.

* Hello 가상 컴퓨터를 다시 시작
* Hello 끝점 다시 / 방화벽 규칙/네트워크 보안 그룹 (NSG) 규칙
  * [Resource Manager 모델 - 네트워크 보안 그룹 관리](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [클래식 모델 - 클라우드 서비스 끝점 관리](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* 다른 Azure 가상 네트워크 등 다른 위치에서 연결
* Hello 가상 컴퓨터를 다시 배포
  * [Windows VM 다시 배포](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Linux VM 다시 배포](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Hello 가상 컴퓨터를 다시 만듭니다.

자세한 내용은 [끝점 연결 문제 해결(RDP/SSH/HTTP 등의 오류)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows)를 참조하세요.

## <a name="detailed-troubleshooting-overview"></a>자세한 문제 해결 개요
Azure 가상 컴퓨터에서 실행 되는 응용 프로그램의 tootroubleshoot hello 액세스는 네 가지 주요 영역입니다.

![응용 프로그램을 시작할 수 없는 문제 해결](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. hello hello Azure 가상 컴퓨터에서 실행 중인 응용 프로그램입니다.
   * 자체 hello 응용 프로그램이 올바르게 실행?
2. hello Azure 가상 컴퓨터입니다.
   * Hello VM 자체 정상적으로 실행 및 toorequests 응답?
3. Azure 네트워크 끝점.
   * Hello 클래식 배포 모델의 가상 컴퓨터에 대 한 클라우드 서비스 끝점입니다.
   * Resource Manager 배포 모델의 가상 컴퓨터용 네트워크 보안 그룹 및 인바운드 NAT 규칙.
   * 사용자가 toohello 예상 hello 포트에서 VM 응용 프로그램에서에서 흐름 트래픽 수 있습니까?
4. 인터넷 에지 장치
   * 트래픽 흐름을 방지하도록 방화벽 규칙이 제대로 적용되고 있나요?

사이트 간 VPN 또는 express 경로 연결을 통해 hello 응용 프로그램에 액세스 하는 클라이언트 컴퓨터에 대 한 문제를 일으킬 수 있는 hello 주요 영역 hello 응용 프로그램 되며 hello Azure 가상 컴퓨터.

toodetermine hello 소스 hello 문제 및 수정 사항이, 다음이 단계를 수행 합니다.

## <a name="step-1-access-application-from-target-vm"></a>1단계: 대상 VM에서 응용 프로그램에 액세스
Tooaccess hello에서에서 응용 프로그램 hello 적절 한 클라이언트 프로그램으로 실행 되는 hello VM 시도 합니다. Hello 로컬 호스트 이름, hello 로컬 IP 주소 또는 hello 루프백 주소 (127.0.0.1)를 사용 합니다.

![hello VM에서 직접 응용 프로그램을 시작 합니다.](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

예를 들어 hello 응용 프로그램은 웹 서버를 hello VM에서 브라우저를 열고 및 tooaccess hello VM에서 호스팅되는 웹 페이지를 시도 하십시오.

Hello 응용 프로그램에 액세스할 수 있으면 너무 이동[2 단계](#step2)합니다.

Hello 응용 프로그램에 액세스할 수 없는 경우 다음 설정을 hello를 확인 합니다.

* hello 응용 프로그램 hello 대상 가상 컴퓨터에서 실행 됩니다.
* hello 응용 프로그램이 예상 hello TCP 및 UDP 포트에서 수신 합니다.

Windows 및 Linux 기반 가상 컴퓨터를 사용 하 여 hello **netstat-a** tooshow hello 활성 수신 대기 포트 명령입니다. 응용 프로그램를 수신 해야 하는 예상 hello 포트에 대 한 hello 출력을 검사 합니다. Hello 응용 프로그램을 다시 시작 필요에 따라 toouse 예상 hello 포트 구성 하 고 tooaccess hello 응용 프로그램을 로컬 다시 시도 하십시오.

## <a id="step2"></a>2 단계: hello에 다른 VM에서 응용 프로그램을 액세스 동일한 가상 네트워크
다른 VM에서 tooaccess hello 응용 프로그램을 시도 하지만 동일한 hello hello VM의 호스트 이름 또는 Azure에서 할당 된 public, private 또는 공급자 IP 주소를 사용 하 여 가상 네트워크입니다. Hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터에 대 한 hello hello 클라우드 서비스의 공용 IP 주소를 사용 하지 마십시오.

![다른 VM에서 응용 프로그램 시작](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

예를 들어 hello 응용 프로그램은 웹 서버, try tooaccess 웹 페이지에 있는 다른 VM에 있는 브라우저에서 동일한 가상 네트워크를 hello 합니다.

Hello 응용 프로그램에 액세스할 수 있으면 너무 이동[3 단계](#step3)합니다.

Hello 응용 프로그램에 액세스할 수 없는 경우 다음 설정을 hello를 확인 합니다.

* hello 인바운드 요청과 아웃 바운드 응답 트래픽에 hello 대상 VM에서 hello 호스트 방화벽에서 허용 됩니다.
* 침입 탐지 또는 hello 대상 VM에서 실행 되는 소프트웨어를 모니터링 하는 네트워크 hello 트래픽을 허용 합니다.
* 클라우드 서비스 끝점 또는 네트워크 보안 그룹 hello 트래픽을 허용:
  * [클래식 모델 - 클라우드 서비스 끝점 관리](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Resource Manager 모델 - 네트워크 보안 그룹 관리](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* VM 및 부하 분산 장치 또는 방화벽 같은 VM hello 테스트 간의 hello 경로 있는 VM에서 실행 되는 별도 구성 요소 hello 트래픽을 허용 합니다.

Windows 기반 가상 컴퓨터에서 hello 방화벽 규칙을 응용 프로그램의 인바운드 및 아웃 바운드 트래픽을 제외 여부에 toodetermine 고급 보안이 있는 Windows 방화벽을 사용 합니다.

## <a id="step3"></a>3 단계: hello 가상 네트워크 외부에서 응용 프로그램에 액세스
Tooaccess hello 응용 프로그램 hello 가상 네트워크 외부 컴퓨터에서 hello 응용 프로그램이 실행 되는 hello VM으로 시도 하세요. 다른 네트워크를 원래의 클라이언트 컴퓨터로 사용합니다.

![hello 가상 네트워크 외부 컴퓨터에서 응용 프로그램을 시작 합니다.](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

예를 들어 hello 응용 프로그램 웹 서버인 경우 hello 가상 네트워크에 있지 않은 컴퓨터에서 실행 되는 브라우저에서 tooaccess hello 웹 페이지를 보십시오.

Hello 응용 프로그램에 액세스할 수 없는 경우 다음 설정을 hello를 확인 합니다.

* Vm에 대 한 hello 클래식 배포 모델을 사용 하 여 만듭니다.
  
  * Hello hello 들어오는 트래픽을, 특히 hello 프로토콜 (TCP 또는 UDP) 및 hello 공용 및 개인 포트 번호를 허용 하는 VM에 대 한 해당 hello 끝점 구성을 확인 하십시오.
  * Hello 끝점에 대 한 액세스 제어 목록 (Acl)을 hello 인터넷에서에서 들어오는 트래픽을 방해 있는지 확인 합니다.
  * 자세한 내용은 참조 [어떻게 tooSet 끝점 tooa 가상 컴퓨터](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.
* Hello 리소스 관리자 배포 모델을 사용 하 여 만든 vm:
  
  * hello hello hello 들어오는 트래픽을, 특히 hello 프로토콜 (TCP 또는 UDP) 및 hello 공용 및 개인 포트 번호를 허용 하는 VM에 대 한 인바운드 NAT 규칙 구성을 확인 합니다.
  * Hello 인바운드 요청과 아웃 바운드 응답 트래픽은 네트워크 보안 그룹은 하도록 허용 하는지 확인 합니다.
  * 자세한 내용은 [NSG(네트워크 보안 그룹)란?](../articles/virtual-network/virtual-networks-nsg.md)

Hello 가상 컴퓨터 또는 끝점에 부하 분산 된 집합의 구성원 인 경우

* Hello 프로브 프로토콜 (TCP 또는 UDP) 및 포트 번호가 올바른지 확인 하세요.
* Hello 프로브 경우 프로토콜 및 포트는 hello 부하 분산 집합 프로토콜 및 포트와 다른:
  * Hello 응용 프로그램이 hello 프로브 프로토콜 (TCP 또는 UDP) 및 포트 번호에서 수신 확인 (사용 하 여 **netstat – a** 대상 VM hello에서).
  * VM에서 인바운드 프로브 요청 hello 캡슐화 된 트래픽과 아웃 바운드 프로브 응답을 허용 하는 hello 대상에서 해당 hello 호스트 방화벽을 확인 합니다.

Hello 응용 프로그램에 액세스할 수 있으면 인터넷 가장자리 장치를 허용 하는지 확인 합니다.

* 클라이언트 컴퓨터 toohello Azure 가상 컴퓨터에서에서 아웃 바운드 응용 프로그램 요청 트래픽의 hello 합니다.
* 안녕 hello Azure 가상 컴퓨터의에서 응답 트래픽은 인바운드 응용 프로그램.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>4를 단계 IP 확인 toocheck hello 설정을 사용 하 여 hello 응용 프로그램에 액세스할 수 없습니다. 

자세한 내용은 [Azure 네트워크 모니터링 개요](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)를 참조하세요. 

## <a name="additional-resources"></a>추가 리소스
[원격 데스크톱 연결 tooa Windows 기반 Azure 가상 컴퓨터 문제 해결](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[SSH (보안 셸) 연결 tooa Linux 기반 Azure 가상 컴퓨터 문제 해결](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

