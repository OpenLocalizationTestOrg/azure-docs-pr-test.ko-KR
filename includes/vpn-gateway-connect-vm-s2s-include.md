<span data-ttu-id="8a942-101">원격 데스크톱 연결 tooyour VM을 만들어 배포 tooyour VNet은 VM tooa를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-101">You can connect tooa VM that is deployed tooyour VNet by creating a Remote Desktop Connection tooyour VM.</span></span> <span data-ttu-id="8a942-102">hello 가장 좋은 방법은 tooinitially 확인 tooyour VM tooconnect 하 여이 연결할 수 있는지 컴퓨터 이름 대신 해당 개인 IP를 사용 하 여 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-102">hello best way tooinitially verify that you can connect tooyour VM is tooconnect by using its private IP address, rather than computer name.</span></span> <span data-ttu-id="8a942-103">이런 방식으로 연결할 수 있는 경우, 여부 이름 확인이 제대로 구성 되지 toosee를 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-103">That way, you are testing toosee if you can connect, not whether name resolution is configured properly.</span></span>

1. <span data-ttu-id="8a942-104">Hello 개인 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-104">Locate hello private IP address.</span></span> <span data-ttu-id="8a942-105">여러 가지 방법으로 VM의 hello 개인 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-105">You can find hello private IP address of a VM in multiple ways.</span></span> <span data-ttu-id="8a942-106">아래의 PowerShell 및 Azure 포털 hello에 대 한 hello 단계 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-106">Below, we show hello steps for hello Azure portal and for PowerShell.</span></span>

  - <span data-ttu-id="8a942-107">Azure 포털-hello Azure 포털에서에서 가상 컴퓨터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-107">Azure portal - Locate your virtual machine in hello Azure portal.</span></span> <span data-ttu-id="8a942-108">Hello VM에 대 한 hello 속성을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-108">View hello properties for hello VM.</span></span> <span data-ttu-id="8a942-109">hello 개인 IP 주소가 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-109">hello private IP address is listed.</span></span>

  - <span data-ttu-id="8a942-110">PowerShell-사용 하 여 hello 예제 tooview Vm 및 리소스 그룹에서 개인 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-110">PowerShell - Use hello example tooview a list of VMs and private IP addresses from your resource groups.</span></span> <span data-ttu-id="8a942-111">사용 하기 전에이 예제 toomodify를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-111">You don't need toomodify this example before using it.</span></span>

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

2. <span data-ttu-id="8a942-112">연결 된 VNet tooyour 있는지 확인 hello VPN 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-112">Verify that you are connected tooyour VNet using hello VPN connection.</span></span>
3. <span data-ttu-id="8a942-113">열기 **원격 데스크톱 연결** hello 작업 표시줄에서 hello 검색 상자에 "RDP" 또는 "원격 데스크톱 연결"을 입력 하 여 원격 데스크톱 연결을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-113">Open **Remote Desktop Connection** by typing "RDP" or "Remote Desktop Connection" in hello search box on hello taskbar, then select Remote Desktop Connection.</span></span> <span data-ttu-id="8a942-114">Hello 'mstsc' 명령을 사용 하 여 PowerShell에서 원격 데스크톱 연결을 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-114">You can also open Remote Desktop Connection using hello 'mstsc' command in PowerShell.</span></span> 
4. <span data-ttu-id="8a942-115">원격 데스크톱 연결에서의 VM hello hello 개인 IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-115">In Remote Desktop Connection, enter hello private IP address of hello VM.</span></span> <span data-ttu-id="8a942-116">"옵션 표시" tooadjust 추가 설정을 클릭 한 다음 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-116">You can click "Show Options" tooadjust additional settings, then connect.</span></span>

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a><span data-ttu-id="8a942-117">RDP 연결 tooa VM tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="8a942-117">tootroubleshoot an RDP connection tooa VM</span></span>

<span data-ttu-id="8a942-118">VPN 연결을 통해 tooa 가상 컴퓨터를 연결 하는 데 문제가 hello 다음 사항을 확인.</span><span class="sxs-lookup"><span data-stu-id="8a942-118">If you are having trouble connecting tooa virtual machine over your VPN connection, check hello following:</span></span>

- <span data-ttu-id="8a942-119">VPN 연결이 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-119">Verify that your VPN connection is successful.</span></span>
- <span data-ttu-id="8a942-120">Toohello hello VM에 대 한 개인 IP 주소를 연결 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-120">Verify that you are connecting toohello private IP address for hello VM.</span></span>
- <span data-ttu-id="8a942-121">Toohello VM에 연결할 수 있는 경우 hello 개인 IP를 사용 하 여 주소, 하지만 컴퓨터 이름을 하지 hello을 DNS를 제대로 구성 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-121">If you can connect toohello VM using hello private IP address, but not hello computer name, verify that you have configured DNS properly.</span></span> <span data-ttu-id="8a942-122">이름 확인이 VM에서 작동하는 방법에 대한 자세한 내용은 [VM에서 이름 확인](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a942-122">For more information about how name resolution works for VMs, see [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
- <span data-ttu-id="8a942-123">RDP 연결에 대 한 자세한 내용은 참조 [문제를 해결 하는 원격 데스크톱 연결 tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8a942-123">For more information about RDP connections, see [Troubleshoot Remote Desktop connections tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).</span></span>
