## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="4eb41-101">어떻게 toocreate 네트워크 구성을 사용 하 여 가상 네트워크에서에서 파일을 PowerShell</span><span class="sxs-lookup"><span data-stu-id="4eb41-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="4eb41-102">Azure는 xml 파일 toodefine 모든 가상 네트워크 사용 가능한 tooa 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="4eb41-103">이 파일을 다운로드, toomodify 편집 또는 기존 가상 네트워크 삭제 있고 새 가상 네트워크를 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="4eb41-104">이 파일을 참조 하는 toodownload 방법을 배우게이 자습서에서는 tooas 구성 (또는 netcfg) 파일, 네트워크 및 toocreate 새 가상 네트워크를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="4eb41-105">hello 네트워크 구성 파일에 대해 자세히 toolearn 참조 hello [Azure 가상 네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="4eb41-106">toocreate PowerShell에서 다음 단계 완료 hello를 사용 하 여 netcfg 파일을 사용 하 여 가상 네트워크:</span><span class="sxs-lookup"><span data-stu-id="4eb41-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="4eb41-107">Azure PowerShell을 처음 사용 하는 경우 전체 hello hello의 단계를 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azureps-cmdlets-docs) 문서, tooAzure에 로그인 하 고 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="4eb41-108">Hello Azure PowerShell 콘솔에서 hello를 사용 하 여 **Get AzureVnetConfig** cmdlet toodownload hello 네트워크 구성 파일 tooa 디렉터리 hello 다음 명령을 실행 하 여 컴퓨터에:</span><span class="sxs-lookup"><span data-stu-id="4eb41-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="4eb41-109">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4eb41-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="4eb41-110">모든 XML 또는 텍스트 편집기 응용 프로그램을 사용 하 여 2 단계에서 저장 하는 hello 파일을 열고 hello 찾아보십시오  **<VirtualNetworkSites>**  요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="4eb41-111">이미 만들어진 네트워크가 있으면 각 네트워크는 자체의 **<VirtualNetworkSite>** 요소로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="4eb41-112">이 시나리오에 설명 된 toocreate hello 가상 네트워크 추가 hello 바로 아래의 다음과 같은 XML hello  **<VirtualNetworkSites>**  요소:</span><span class="sxs-lookup"><span data-stu-id="4eb41-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. <span data-ttu-id="4eb41-113">Hello 네트워크 구성 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="4eb41-114">Hello Azure PowerShell 콘솔에서 hello를 사용 하 여 **집합 AzureVnetConfig** hello 다음 명령을 실행 하 여 cmdlet tooupload hello 네트워크 구성 파일:</span><span class="sxs-lookup"><span data-stu-id="4eb41-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="4eb41-115">반환되는 출력:</span><span class="sxs-lookup"><span data-stu-id="4eb41-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="4eb41-116">경우 **OperationStatus** 않습니다 *Succeeded* 출력을 반환 하는 hello, 오류 및 완료 단계 6에 대 한 xml 파일 hello를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="4eb41-117">Hello Azure PowerShell 콘솔에서 hello를 사용 하 여 **Get AzureVnetSite** hello 다음 명령을 실행 하 여 새 네트워크 hello cmdlet tooverify 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="4eb41-118">hello 반환 (약식된) 출력 hello 텍스트 뒤에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eb41-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
