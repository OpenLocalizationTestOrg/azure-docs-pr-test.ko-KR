<span data-ttu-id="3c25f-101">VM에 원격 데스크톱 연결을 만들어 VNet에 배포된 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-101">You can connect to a VM that is deployed to your VNet by creating a Remote Desktop Connection to your VM.</span></span> <span data-ttu-id="3c25f-102">처음에 VM에 연결할 수 있는지 확인하는 가장 좋은 방법은 컴퓨터 이름이 아닌 개인 IP 주소를 사용하여 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-102">The best way to initially verify that you can connect to your VM is to connect by using its private IP address, rather than computer name.</span></span> <span data-ttu-id="3c25f-103">이 방법을 사용하면 연결할 수 있는지, 이름 확인이 제대로 구성되었는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-103">That way, you are testing to see if you can connect, not whether name resolution is configured properly.</span></span>

1. <span data-ttu-id="3c25f-104">개인 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-104">Locate the private IP address.</span></span> <span data-ttu-id="3c25f-105">여러 가지 방법으로 VM의 개인 IP 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-105">You can find the private IP address of a VM in multiple ways.</span></span> <span data-ttu-id="3c25f-106">아래에서 Azure Portal 및 PowerShell에서의 단계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-106">Below, we show the steps for the Azure portal and for PowerShell.</span></span>

  - <span data-ttu-id="3c25f-107">Azure Portal - Azure Portal에서 가상 컴퓨터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-107">Azure portal - Locate your virtual machine in the Azure portal.</span></span> <span data-ttu-id="3c25f-108">VM 속성을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-108">View the properties for the VM.</span></span> <span data-ttu-id="3c25f-109">개인 IP 주소가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-109">The private IP address is listed.</span></span>

  - <span data-ttu-id="3c25f-110">PowerShell - 예제를 사용하여 리소스 그룹의 VM 및 개인 IP 주소 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-110">PowerShell - Use the example to view a list of VMs and private IP addresses from your resource groups.</span></span> <span data-ttu-id="3c25f-111">이 예제는 수정하지 않고 그냥 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-111">You don't need to modify this example before using it.</span></span>

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

2. <span data-ttu-id="3c25f-112">VPN 연결을 사용하여 VNet에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-112">Verify that you are connected to your VNet using the VPN connection.</span></span>
3. <span data-ttu-id="3c25f-113">작업 표시줄에서 검색 상자에 "RDP" 또는 "원격 데스크톱 연결"을 입력하여 **원격 데스크톱 연결**을 열고 원격 데스크톱 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-113">Open **Remote Desktop Connection** by typing "RDP" or "Remote Desktop Connection" in the search box on the taskbar, then select Remote Desktop Connection.</span></span> <span data-ttu-id="3c25f-114">PowerShell에서 'mstsc' 명령을 사용하여 원격 데스크톱 연결을 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-114">You can also open Remote Desktop Connection using the 'mstsc' command in PowerShell.</span></span> 
4. <span data-ttu-id="3c25f-115">원격 데스크톱 연결에서 VM의 개인 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-115">In Remote Desktop Connection, enter the private IP address of the VM.</span></span> <span data-ttu-id="3c25f-116">"옵션 표시"를 클릭하여 추가 설정을 조정한 다음 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-116">You can click "Show Options" to adjust additional settings, then connect.</span></span>

### <a name="to-troubleshoot-an-rdp-connection-to-a-vm"></a><span data-ttu-id="3c25f-117">VM에 대한 RDP 연결 문제를 해결하려면</span><span class="sxs-lookup"><span data-stu-id="3c25f-117">To troubleshoot an RDP connection to a VM</span></span>

<span data-ttu-id="3c25f-118">VPN 연결을 통해 가상 컴퓨터에 연결하는 데 문제가 있는 경우 다음 항목을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-118">If you are having trouble connecting to a virtual machine over your VPN connection, check the following:</span></span>

- <span data-ttu-id="3c25f-119">VPN 연결이 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-119">Verify that your VPN connection is successful.</span></span>
- <span data-ttu-id="3c25f-120">VM의 개인 IP 주소에 연결하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-120">Verify that you are connecting to the private IP address for the VM.</span></span>
- <span data-ttu-id="3c25f-121">컴퓨터 이름이 아닌 개인 IP 주소를 사용하여 VM에 연결할 수 있는 경우 DNS를 올바르게 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c25f-121">If you can connect to the VM using the private IP address, but not the computer name, verify that you have configured DNS properly.</span></span> <span data-ttu-id="3c25f-122">이름 확인이 VM에서 작동하는 방법에 대한 자세한 내용은 [VM에서 이름 확인](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c25f-122">For more information about how name resolution works for VMs, see [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
- <span data-ttu-id="3c25f-123">RDP 연결에 대한 자세한 내용은 [VM에 대한 원격 데스크톱 연결 문제 해결](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c25f-123">For more information about RDP connections, see [Troubleshoot Remote Desktop connections to a VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).</span></span>