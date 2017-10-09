원격 데스크톱 연결 tooyour VM을 만들어 배포 tooyour VNet은 VM tooa를 연결할 수 있습니다. hello 가장 좋은 방법은 tooinitially 확인 tooyour VM tooconnect 하 여이 연결할 수 있는지 컴퓨터 이름 대신 해당 개인 IP를 사용 하 여 해결 합니다. 이런 방식으로 연결할 수 있는 경우, 여부 이름 확인이 제대로 구성 되지 toosee를 테스트 됩니다.

1. Hello 개인 IP 주소를 찾습니다. 여러 가지 방법으로 VM의 hello 개인 IP 주소를 찾을 수 있습니다. 아래의 PowerShell 및 Azure 포털 hello에 대 한 hello 단계 보여줍니다.

  - Azure 포털-hello Azure 포털에서에서 가상 컴퓨터를 찾습니다. Hello VM에 대 한 hello 속성을 봅니다. hello 개인 IP 주소가 나열 됩니다.

  - PowerShell-사용 하 여 hello 예제 tooview Vm 및 리소스 그룹에서 개인 IP 주소 목록입니다. 사용 하기 전에이 예제 toomodify를 필요 하지 않습니다.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. 연결 된 VNet tooyour 있는지 확인 hello VPN 연결을 사용 합니다.
3. 열기 **원격 데스크톱 연결** hello 작업 표시줄에서 hello 검색 상자에 "RDP" 또는 "원격 데스크톱 연결"을 입력 하 여 원격 데스크톱 연결을 선택 합니다. Hello 'mstsc' 명령을 사용 하 여 PowerShell에서 원격 데스크톱 연결을 열 수도 있습니다. 
4. 원격 데스크톱 연결에서의 VM hello hello 개인 IP 주소를 입력 합니다. "옵션 표시" tooadjust 추가 설정을 클릭 한 다음 연결할 수 있습니다.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>RDP 연결 tooa VM tootroubleshoot

VPN 연결을 통해 tooa 가상 컴퓨터를 연결 하는 데 문제가 hello 다음 사항을 확인.

- VPN 연결이 성공했는지 확인합니다.
- Toohello hello VM에 대 한 개인 IP 주소를 연결 하 고 있는지 확인 합니다.
- Toohello VM에 연결할 수 있는 경우 hello 개인 IP를 사용 하 여 주소, 하지만 컴퓨터 이름을 하지 hello을 DNS를 제대로 구성 했는지 확인 합니다. 이름 확인이 VM에서 작동하는 방법에 대한 자세한 내용은 [VM에서 이름 확인](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.
- RDP 연결에 대 한 자세한 내용은 참조 [문제를 해결 하는 원격 데스크톱 연결 tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)합니다.
