이 문서에서는 Azure에서 Windows 가상 컴퓨터 (VM)를 실행, 지불 주의 tooscalability, 가용성, 관리 효율성 및 보안에 대 한 검증 된 사례 집합을 설명 합니다.

> [!NOTE]
> Azure에는 [Azure Resource Manager][resource-manager-overview] 및 클래식이라는 두 가지 서로 다른 배포 모델이 있습니다. 이 문서에서는 새로운 배포를 위해 Microsoft에서 권장하는 리소스 관리자를 사용합니다.
>
>

단일 실패 지점을 생성하므로 중요한 작업에 단일 VM을 사용하지 않는 것이 좋습니다. 더 높은 가용성을 위해 [가용성 집합][availability-set]에 여러 VM을 배포합니다. 자세한 내용은 [Azure에서 여러 VM 실행][multi-vm]을 참조하세요.

## <a name="architecture-diagram"></a>아키텍처 다이어그램

Azure에서 VM을 프로 비전만 VM 자체 hello 보다 더 작동 되는 부분이 포함 됩니다. 계산, 네트워킹 및 저장소 요소가 있습니다.

> 이 아키텍처 다이어그램에 포함 된 Visio 문서는 hello에서 다운로드할 수 [Microsoft 다운로드 센터][visio-download]합니다. 이 다이어그램은 hello "Compute-단일 VM"의 페이지입니다.
>
>

![[0]][0]

* **리소스 그룹.** [*리소스 그룹*][resource-manager-overview]은 관련된 리소스를 보유하는 컨테이너입니다. 이 VM에 대 한 리소스를 toohold hello 리소스 그룹을 만듭니다.
* **VM**. TooAzure Blob 저장소를 업로드 하는 가상 하드 디스크 (VHD) 파일 또는 게시 된 이미지 목록에서 VM 프로 비전 할 수 있습니다.
* **OS 디스크.** hello OS 디스크는 VHD에 저장 된 [Azure 저장소][azure-storage]합니다. 즉, hello 호스트 컴퓨터의 작동이 중지 하는 경우에 문제가 계속 되는 것을 의미 합니다.
* **임시 디스크.** hello VM은 사용 하 여 만든 임시 디스크 (hello `D:` 드라이브가 Windows에서). 이 디스크는 hello 호스트 컴퓨터에 실제 드라이브에 저장 됩니다. Azure Storage에는 저장되지 *않으며* 다시 부팅되는 동안에 그리고 다른 VM의 수명 주기 이벤트 동안에 삭제될 수 있습니다. 페이지 또는 스왑 파일과 같은 임시 데이터에 대해서만 이 디스크를 사용합니다.
* **데이터 디스크.** [데이터 디스크][data-disk]는 응용 프로그램 데이터에 사용되는 영구 VHD입니다. 데이터 디스크는 hello 운영 체제 디스크와 같은 Azure 저장소에 저장 됩니다.
* **가상 네트워크(VNet) 및 서브넷.** Azure의 모든 VM은 서브넷으로 세분화되는 VNet에 배포됩니다.
* **공용 IP 주소.** 공용 IP 주소는 VM hello로 필요한 toocommunicate&mdash;예를 들어 원격 데스크톱 (RDP)을 통해.
* **NIC(네트워크 인터페이스)**. hello NIC hello 가상 네트워크와 VM toocommunicate를 hello 수 있습니다.
* **NSG(네트워크 보안 그룹)**. hello [NSG] [ nsg] 네트워크 트래픽 toohello 서브넷 사용 되는 tooallow/거부 됩니다. NSG를 개별 NIC 또는 서브넷에 연결할 수 있습니다. 서브넷과 연결 하는 경우 해당 서브넷의 tooall Vm hello NSG 규칙에 적용 됩니다.
* **진단** 진단 로깅이 관리 및 hello VM 문제 해결에 대 한 매우 중요 합니다.

## <a name="recommendations"></a>권장 사항

대부분의 시나리오에 대 한 권장 사항을 따르면 hello 적용 됩니다. 이러한 권장 사항을 재정의하라는 특정 요구 사항이 있는 경우가 아니면 따릅니다.

### <a name="vm-recommendations"></a>VM 권장 사항

Azure는 여러 다른 가상 컴퓨터 크기를 제공 하지만 이러한 컴퓨터 크기 지원 hello DS-및 GS 시리즈 권장 [프리미엄 저장소][premium-storage]합니다. 고성능 컴퓨팅과 같은 특수한 워크로드가 발생하지 않는다면 이러한 컴퓨터 크기 중 하나를 선택합니다. 자세한 내용은 [가상 컴퓨터 크기][virtual-machine-sizes]를 참조하세요.

기존 작업 tooAzure 이동 하는 경우 시작 되는 가장 가까운 일치 tooyour hello hello VM 크기와 온-프레미스 서버입니다. 그런 다음 카디널리티 평가기로 실제 작업의 hello 성능을 측정 tooCPU, 메모리 및 디스크 입/출력 작업 / 초 (IOPS)을 준수 하 고 필요한 경우 hello 크기를 조정 합니다. VM에 대 한 여러 Nic를 필요로 하는 경우 유의 hello Nic의 최대 수의 hello 함수 인지 [VM 크기][vm-size-tables]합니다.   

Hello VM 및 기타 리소스를 프로 비전 할 때 영역을 지정 해야 합니다. 일반적으로 영역을 가장 가까운 tooyour 내부 사용자 선택 또는 고객 합니다. 그러나 일부 지역에서는 일부 VM 크기를 사용할 수 없을 수 있습니다. 자세한 내용은 [지역별 서비스][services-by-region]를 참조하세요. toosee hello 다음 Azure 명령줄 인터페이스 (CLI) 명령을 실행 하는 특정된 지역에서 사용할 수 있는 hello VM 크기의 목록:

```
azure vm sizes --location <location>
```

게시된 VM 이미지를 선택하는 방법에 대한 자세한 내용은 [Powershell 또는 CLI를 사용하여 Azure에서 Windows 가상 컴퓨터 이미지 탐색 및 선택][select-vm-image]을 참조하세요.

### <a name="disk-and-storage-recommendations"></a>디스크 및 저장소 권장 사항

최상의 디스크 I/O 성능을 위해서는 SSD(반도체 드라이브)에 데이터를 저장하는 [프리미엄 저장소][premium-storage]가 권장됩니다. 비용은은 hello 프로 비전 된 디스크의 hello 크기를 기반으로 합니다. IOPS 및 처리량도 디스크 크기에 따라 달라지므로 디스크를 프로비전할 때 세 가지 요소(용량, IOPS, 처리량)를 모두 고려합니다.

저장소 계정에 대 한 hello IOPS 제한에 도달 하는 순서 tooavoid에서 각 VM toohold hello 가상 하드 디스크 (Vhd)에 대 한 별도 Azure 저장소 계정을 만듭니다.

하나 이상의 데이터 디스크를 추가합니다. 새 VHD를 만들 때 형식은 지정되지 않습니다. Hello VM tooformat hello 디스크에 로그인 합니다. 많은 수의 데이터 디스크를 사용 하도록 설정한 경우 hello 저장소 계정의 hello 총 I/O 제한을 고려해 야 합니다. 자세한 내용은 [가상 컴퓨터 디스크 제한][vm-disk-limits]을 참조하세요.

가능한 경우 데이터 디스크에 운영 체제 디스크가 아닌 hello 응용 프로그램을 설치 합니다. 그러나 일부 레거시 응용 프로그램 tooinstall hello c: 드라이브에 있는 구성 요소를 할 수 있습니다. 수 경우 [hello OS 디스크 크기 조정] [ resize-os-disk] PowerShell을 사용 하 여 합니다.

최상의 성능을 위해 toohold 진단 로그를 별도 저장소 계정을 만듭니다. 표준 LRS(로컬 중복 저장소) 계정은 진단 로그에 충분합니다.

### <a name="network-recommendations"></a>네트워크 권장 사항

hello 공용 IP 주소는 동적 또는 정적 수 있습니다. hello 기본값은 동적입니다.

* 예약 된 [고정 IP 주소] [ static-ip] 고정된 IP 주소를 변경 되지 않는 경우 해야 &mdash; 예를 들어 해야 toocreate A DNS에서 기록 하거나 IP 주소 toobe 추가 tooa 수신 허용 목록 hello 필요 합니다.
* Hello IP 주소에 대 한 정규화 된 도메인 이름 (FQDN)를 만들 수 있습니다. 등록할 수 있습니다는 [CNAME 레코드] [ cname-record] toohello FQDN을 가리키는 DNS의 합니다. 자세한 내용은 참조 [hello Azure 포털에서에서 정규화 된 도메인 이름을 만들][fqdn]합니다.

모든 NSG에는 모든 인바운드 인터넷 트래픽을 차단하는 규칙을 포함하여 [기본 규칙][nsg-default-rules] 집합이 있습니다. hello 기본 규칙은 삭제할 수 있지만 다른 규칙을 재정의할 수 있습니다. 인터넷 트래픽을 tooenable toospecific 포트 인바운드 트래픽을 허용 하는 규칙을 만들 &mdash; HTTP에 대 한 예를 들어 포트 80입니다.  

RDP를 tooenable tooTCP 포트 3389 인바운드 트래픽을 허용 하는 NSG 규칙을 추가 합니다.

## <a name="scalability-considerations"></a>확장성 고려 사항

위나 아래로 이동 하 여 VM을 확장할 수 [hello VM 크기를 변경](../articles/virtual-machines/windows/sizes.md)합니다. 가로로 아웃 tooscale 가용성 집합 부하 분산 장치 뒤에 두 개 이상의 가상 컴퓨터를 넣습니다. 자세한 내용은 [Azure에서 확장성 및 가용성을 위해 여러 VM 실행][multi-vm]을 참조하세요.

## <a name="availability-considerations"></a>가용성 고려 사항

더 높은 가용성을 위해 가용성 집합에 여러 VM을 배포합니다. 또한 더 높은 [서비스 수준 약정][vm-sla](SLA)을 제공합니다.

사용자의 VM은 [계획된 유지 관리][planned-maintenance] 또는 [계획되지 않은 유지 관리][manage-vm-availability]의 영향을 받을 수 있습니다. 사용할 수 있습니다 [VM 재부팅 로그] [ reboot-logs] toodetermine 계획 된 유지 관리에 의해 발생 한 VM 다시 부팅 인지 합니다.

VHD는 [Azure Storage][azure-storage]에 저장되며 Azure Storage는 내구성 및 가용성을 위해 복제됩니다.

(예를 들어 사용자 오류)으로 인해 정상 작업 중 데이터 손실을 tooprotect를 구현 해야 사용 하 여 지정 시간 백업을 [blob 스냅숏을] [ blob-snapshot] 또는 다른 도구입니다.

## <a name="manageability-considerations"></a>관리 효율성 고려 사항

**리소스 그룹** 긴밀 하 게 결합 된 리소스에 동일한 수명 주기 해당 공유 hello hello 동일 [리소스 그룹][resource-manager-overview]합니다. 리소스 그룹 모니터 및 toodeploy 리소스 그룹으로 사용 하면 및 리소스 그룹으로 비용 청구를 롤업 합니다. 리소스를 하나의 집합으로 삭제할 수도 있습니다. 이러한 기능은 테스트 배포에서 매우 유용합니다. 리소스에 의미 있는 이름을 지정합니다. 쉽게 toolocate 특정 리소스 있고, 해당 역할을 이해 합니다. [Azure 리소스에 대한 권장되는 명명 규칙][naming conventions]을 참조하세요.

**VM 진단.** 기본 상태 메트릭, 진단 인프라 로그 및 [부팅 진단][boot-diagnostics]을 모니터링 및 진단을 사용하도록 설정할 수 있습니다. 부팅 진단은 VM이 부팅할 수 없는 상태로 전환되는 경우 부팅 오류를 진단하는 데 도움이 될 수 있습니다. 자세한 내용은 [모니터링 및 진단 사용][enable-monitoring]을 참조하세요. 사용 하 여 hello [Azure 로그 컬렉션] [ log-collector] 확장 toocollect Azure 플랫폼 로그 및 tooAzure 저장소에 업로드 합니다.   

진단을 사용 하는 다음 CLI 명령을 hello:

```
azure vm enable-diag <resource-group> <vm-name>
```

**VM 중지.** Azure에서는 "중지됨"과 "할당 취소됨" 상태를 구분합니다. Hello VM 상태가 중지 되 면 하지만 하지 않을 때 VM hello는 할당이 해제 된 요금이 청구 됩니다.

다음 CLI 명령을 toodeallocate VM hello를 사용 합니다.

```
azure vm deallocate <resource-group> <vm-name>
```

Hello Azure 포털에서에서 hello **중지** 단추 hello VM의 할당을 취소 합니다. 그러나 hello 로그인 한 상태에서 운영 체제를 통해 종료 된 경우 hello VM은 중지 하지만 *하지* 의 할당이 취소 되므로 계속 청구 됩니다.

**VM 삭제.** VM을 삭제 하면 hello Vhd는 삭제 되지 않습니다. 즉, 데이터 손실 없이 hello VM을 안전 하 게 삭제할 수 있습니다. 그러나 저장소에 대한 비용은 계속 청구됩니다. toodelete hello VHD에서 hello 파일을 삭제 [Blob 저장소][blob-storage]합니다.

사용 하 여 tooprevent 실수로 삭제 한 [리소스 잠금] [ resource-lock] toolock hello 전체 리소스 그룹 또는 잠금 등의 개별 리소스, hello VM입니다.

## <a name="security-considerations"></a>보안 고려 사항

사용 하 여 [Azure 보안 센터] [ security-center] tooget Azure 리소스의 보안 상태 hello의 중앙 보기. 보안 센터 잠재적인 보안 문제를 모니터링 하 고 배포의 hello 보안 상태에 대 한 종합적인 그림을 제공 합니다. 보안 센터는 각 Azure 구독을 기준으로 구성됩니다. [보안 센터 사용]에 설명된 것처럼 보안 데이터 수집을 사용하도록 설정합니다. 데이터 수집이 사용되도록 설정되면 보안 센터는 해당 구독에서 만든 모든 VM을 자동으로 검색합니다.

**패치 관리.** 이 기능이 설정된 경우 보안 센터는 보안 및 중요 업데이트 누락 여부를 확인합니다. 사용 하 여 [그룹 정책 설정을] [ group-policy] hello VM tooenable 자동 시스템 업데이트 합니다.

**맬웨어 방지.** 이 기능이 설정되면 보안 센터는 맬웨어 방지 소프트웨어 설치 여부를 확인합니다. 내 보안 센터 tooinstall 맬웨어 방지 소프트웨어를 사용할 수도 있습니다 hello Azure 포털입니다.

**작업.** 사용 하 여 [역할 기반 액세스 제어] [ rbac] (RBAC) toocontrol 액세스 toohello Azure 배포 하는 리소스입니다. RBAC는 DevOps 팀의 권한 부여 역할 toomembers를 할당할 수 있습니다. 예를 들어 hello 읽기 역할 Azure 리소스를 볼 있지만 생성, 관리 또는 안 삭제 합니다. 일부 역할은 특정 tooparticular Azure 리소스 종류입니다. 예를 들어 hello 가상 컴퓨터 참가자 역할 수를 다시 시작 하거나 VM 할당을 취소, hello 관리자 암호 재설정, 새 VM을 만듭니다 등. 이 참조 아키텍처에 유용할 수 있는 기타 [기본 제공 RBAC 역할][rbac-roles]에는 [DevTest Labs 사용자][rbac-devtest] 및 [네트워크 참가자][rbac-network]가 포함됩니다. 사용자 toomultiple 역할을 할당할 수 있으며 더욱 세분화 된 사용 권한에 대 한 사용자 지정 역할을 만들 수 있습니다.

> [!NOTE]
> RBAC의 VM에 로그온 한 사용자가 수행할 수 있는 hello 동작을 제한 하지 않습니다. 이러한 사용 권한은 hello 계정 유형을 hello 게스트 운영 체제에 따라 결정 됩니다.   
>
>

hello 실행 tooreset hello 로컬 관리자 암호를 `vm reset-access` Azure CLI 명령입니다.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

사용 하 여 [감사 로그] [ audit-logs] toosee 동작 및 이벤트를 다른 VM 프로 비전 합니다.

**데이터 암호화.** 고려 [Azure 디스크 암호화] [ disk-encryption] tooencrypt hello OS 및 데이터 디스크가 필요 합니다.

## <a name="solution-deployment"></a>솔루션 배포

이 참조 아키텍처에 대한 배포는 [GitHub][github-folder]에서 사용할 수 있습니다. VNet, NSG 및 단일 VM을 포함합니다. toodeploy hello 아키텍처, 다음이 단계를 수행 합니다.

1. Hello 단추 아래를 마우스 오른쪽 단추로 클릭 하 고 링크를 선택 하거나 "열기 새 탭에서" 또는 "새 창에서 열기 링크입니다."  
   [![TooAzure 배포](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Hello Azure 포털에서에서 hello 링크를 연 후 hello 설정 중 일부에 대 한 값을 입력 해야 합니다.

   * hello **리소스 그룹** 이름이 선택 hello 매개 변수 파일에 이미 정의 되어 **새로 만들기** 입력 `ra-single-vm-rg` hello 텍스트 상자에 있습니다.
   * Hello에서 선택 hello 지역 **위치** 드롭다운 상자입니다.
   * Hello를 편집 하지 않는 **템플릿 루트 Uri** 또는 hello **루트 Uri 매개 변수** 텍스트 상자입니다.
   * 선택 **windows** hello에 **Os 유형이** 드롭다운 상자입니다.
   * Hello 사용 약관을 검토 한 다음 hello 클릭 **toohello 약관 위에서 설명한 동의** 확인란을 선택 합니다.
   * Hello 클릭 **구매** 단추입니다.
3. Hello 배포 toocomplete 될 때까지 기다립니다.
4. hello 매개 변수 파일에 하드 코드 된 관리자 사용자 이름 및 암호를 포함 하 고 즉시 변경 하는 둘 다이 가장 좋습니다. Hello 라는 VM에서 클릭 `ra-single-vm0 `hello Azure 포털의에서. 다음에 클릭 **암호 재설정** hello에 **지원 + 문제 해결** 블레이드입니다. 선택 **암호 재설정** hello에 **모드** 드롭다운 상자는 새 선택 **사용자 이름** 및 **암호**합니다. Hello 클릭 **업데이트** toopersist hello 새 사용자 이름 및 암호를 단추입니다.

다른 방법은 toodeploy에 대 한 내용은이 아키텍처 hello에 hello 추가 정보 파일을 참조 하십시오 [지침 단일 vm][github-folder]] GitHub 폴더입니다.

## <a name="customize-hello-deployment"></a>Hello 배포를 사용자 지정
요구 사항 toochange hello 배포 toomatch 해야 할 경우 hello 지침 hello에 따라 [readme][github-folder]합니다.

## <a name="next-steps"></a>다음 단계
더 높은 가용성을 위해 부하 분산 장치 뒤에 둘 이상의 VM을 배포합니다. 자세한 내용은 [Azure에서 여러 VM 실행][multi-vm]을 참조하세요.

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[보안 센터 사용]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Azure의 단일 Windows VM 아키텍처"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
