
* [Azure에서 가상 컴퓨터 빨리 만들기](#quick-create-a-vm-in-azure)
* [템플릿에서 Azure의 가상 컴퓨터 배포](#deploy-a-vm-in-azure-from-a-template)
* [사용자 지정 이미지에서 가상 컴퓨터 만들기](#create-a-custom-vm-image)
* [가상 네트워크 및 부하 분산 장치를 사용하는 가상 컴퓨터 배포](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [리소스 그룹 제거](#remove-a-resource-group)
* [리소스 그룹 배포에 대 한 hello 로그 표시](#show-the-log-for-a-resource-group-deployment)
* [가상 컴퓨터에 대한 정보 표시](#display-information-about-a-virtual-machine)
* [Tooa Linux 기반 가상 컴퓨터에 연결](#log-on-to-a-linux-based-virtual-machine)
* [가상 컴퓨터 중지](#stop-a-virtual-machine)
* [가상 컴퓨터 시작](#start-a-virtual-machine)
* [데이터 디스크 연결](#attach-a-data-disk)

## <a name="getting-ready"></a>준비
Azure 리소스 그룹과 hello Azure CLI를 사용 하려면 먼저 toohave hello 오른쪽 Azure CLI 버전 및 Azure 계정이 필요 합니다. Hello Azure CLI 없는 경우 [설치](../articles/cli-install-nodejs.md)합니다.

### <a name="update-your-azure-cli-version-too090-or-later"></a>Azure CLI 버전 too0.9.0 업데이트 이상 버전
형식 `azure --version` 설치 된 버전 0.9.0 이미 있는지 toosee 이상.

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

기본 설치 관리자 hello 중 하나를 사용 하 여 사용 중인 버전 0.9.0 아니거나 tooupdate 필요 이상 버전에서는 또는 **npm** 입력 하 여 `npm update -g azure-cli`합니다.

또한 Azure CLI Docker 컨테이너 hello 다음을 사용 하 여 실행할 수 있습니다 [Docker 이미지](https://registry.hub.docker.com/u/microsoft/azure-cli/)합니다. Docker 호스트에서 hello 다음 명령을 실행 합니다.

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a>Azure 계정 및 구독 설정
Azure 구독은 아직 없지만 MSDN 구독은 있는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화할 수 있습니다. 또는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.

이제 [tooyour Azure 계정에에서 대화형 로그온](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) 입력 하 여 `azure login` 고 대화형 로그인 경험 tooyour Azure 계정에 대 한 hello 프롬프트를 따릅니다. 

> [!NOTE]
> 회사 또는 학교 ID 2 단계 인증을 사용할 수 없는, 있습니다 수를 아는 경우 **도** 사용 `azure login -u` 에 ID toolog ळ ा hello와 함께 작동 *없이* 대화형 세션입니다. 회사 또는 학교 ID 하지 않는 경우 다음을 할 수 있습니다 [개인 Microsoft 계정에서 회사 또는 학교 id를 만들려면](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog hello에서 같은 방식으로 합니다.
>
>

계정에는 둘 이상의 구독이 있을 수 있습니다. `azure account list`를 입력하여 구독을 나열할 수 있으며, 다음과 같이 표시될 수 있습니다.

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

Hello 다음을 입력 하 여 hello 현재 Azure 구독을 설정할 수 있습니다. Hello 이름 또는 hello 하는 구독 ID에서 원하는 toomanage hello 리소스를 사용 합니다.

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a>Toohello Azure CLI 리소스 그룹 모드 전환
기본적으로 Azure CLI hello hello 서비스 관리 모드에서 시작 (**asm** 모드). Hello tooswitch tooresource 그룹 모드를 다음을 입력 합니다.

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a>Azure 리소스 템플릿 및 리소스 그룹 이해
대부분의 응용 프로그램은 다양한 리소스 유형(예: 하나 이상의 VM 및 저장소 계정, SQL 데이터베이스, 가상 네트워크 또는 콘텐츠 배달 네트워크)의 조합으로 구축되었습니다. 기본 Azure 서비스 관리 API hello와 hello Azure 클래식 포털 표현 이러한 항목-서비스 접근 방식을 사용 하 여 합니다. 이 방법을 사용 해야 toodeploy 및 hello 개별 서비스를 개별적으로 관리 (또는 작업을 수행 하는 다른 도구를 찾을), 배포의 단일 논리 단위 아니라 합니다.

*그러나 Azure 리소스 관리자 템플릿*, toodeploy 있습니다 수 및 선언적 방식으로 하나의 논리적 배포 단위로 이러한 다른 리소스를 관리 합니다. 명령적 지시 Azure 어떤 toodeploy 하나의 명령 다음에 다른, 대신-hello 리소스 및 관련된 구성 및 배포 매개 변수 모두-JSON 파일의 전체 배포에 설명 하 고이 Azure toodeploy 하나로 이러한 리소스 설명 그룹입니다.

Hello를 관리할 수 있습니다에 Azure CLI 리소스 관리 명령을 사용 하 여 hello 그룹 리소스의 전체 수명 주기:

* 중지, 시작 또는 hello 그룹 내의 hello 리소스를 모두 한 번에 삭제 됩니다.
* 보안 권한 아래로 규칙 toolock 역할 기반 액세스 제어 (RBAC)에 적용 됩니다.
* 작업을 감사합니다.
* 추가 메타데이터로 리소스에 태그를 지정하여 추적을 개선합니다.

Azure 리소스 그룹 및 수 있는 작업 수에 대 한 hello에 대 한 기타 등등 학습할 수 있는 [Azure 리소스 관리자 개요](../articles/azure-resource-manager/resource-group-overview.md)합니다. 템플릿 작성에 관심이 있다면 [Azure 리소스 관리자 템플릿 작성](../articles/resource-group-authoring-templates.md)을 참조하세요.

## <a id="quick-create-a-vm-in-azure"></a>작업: Azure에서 VM 빠르게 만들기
어떤 이미지를 알고 있는 경우에 따라 하 고 해당 이미지에서 VM을 지금 당장 필요한 및 중요 하지 않으면 hello 인프라에 대해 자세히-미정 tootest 결과가 있는 클린 VM에서 합니다. 이 경우에 원하는 toouse hello `azure vm quick-create` 명령을 실행 하 고 VM 및 인프라 hello 인수 필요한 toocreate를 전달 합니다.

먼저 리소스 그룹을 만듭니다.

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

두 번째로 이미지가 필요합니다. hello Azure CLI로 이미지 toofind 참조 [Navigating PowerShell 및 Azure CLI hello를 사용 하 여 Azure 가상 컴퓨터 이미지를 선택 하 고](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 그러나 이 문서에서는 다음과 같이 많이 사용되는 간단한 이미지 목록을 제공합니다. 이 quick-create에서는 CoreOS의 Stable 이미지를 사용합니다.

> [!NOTE]
> ComputeImageVersion에 대 한 제공할 수 있습니다 놓는 '최신' hello 매개 변수 hello Azure CLI 및 두 hello 템플릿 언어에 따라. 따라서 스크립트 또는 템플릿 toomodify 필요 없이 hello 이미지의 최신 및 패치 버전을 hello를 사용 하면 tooalways 수 있습니다. 다음과 같습니다.
>
>

| PublisherName | 제안 | SKU | 버전 |
|:--- |:--- |:--- |:--- |
| OpenLogic |CentOS |7 |7.0.201503 |
| OpenLogic |CentOS |7.1 |7.1.201504 |
| CoreOS |CoreOS |베타 |647.0.0 |
| CoreOS |CoreOS |Stable |633.1.0 |
| MicrosoftDynamicsNAV |DynamicsNAV |2015 |8.0.40459 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2013 |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Standard |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Enterprise |1.0.0 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-DW |12.0.2430 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-OLTP |12.0.2430 |
| Canonical |UbuntuServer |12.04.5-LTS |12.04.201504230 |
| Canonical |UbuntuServer |14.04.2-LTS |14.04.201503090 |
| MicrosoftWindowsServer |WindowsServer |2012-Datacenter |3.0.201503 |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |4.0.201503 |
| MicrosoftWindowsServer |WindowsServer |Windows-Server-Technical-Preview |5.0.201504 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |1.0.141204 |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |4.3.4665 |

Hello를 입력 하 여 VM을 만들기만 `azure vm quick-create` 명령에 대 한 준비 되 고 hello 묻는 메시지를 표시 합니다. 다음과 같이 표시됩니다.

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

이제 새 VM으로 전환하면 됩니다.

## <a id="deploy-a-vm-in-azure-from-a-template"></a>작업: 템플릿에서 Azure의 VM 배포
이 섹션에서는 toodeploy 새 Azure VM에에서 Azure CLI hello 함께 서식 파일을 사용 하 여 hello 지침을 사용 합니다. 이 서식 파일은 새 가상 네트워크와는 달리 지역 및 단일 서브넷에 단일 가상 컴퓨터를 만듭니다 `azure vm quick-create`, 원하는 대로 정확 하 게 toodescribe 있습니다 수 있도록 하 고 오류 없이 반복 합니다. 다음은 이 템플릿에서 만드는 항목입니다.

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a>1 단계: hello JSON 파일 hello 템플릿 매개 변수를 검사 합니다.
다음은 hello 템플릿에 대 한 hello JSON 파일의 hello 내용입니다. (또한 hello 서식 파일에 있는 [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)

Hello 디자이너 toogive 많은 매개 변수를 선택 또는 선택 toooffer 더 수정 하는 템플릿을 만들어 일부만 되었을 하므로 템플릿은 유연 하 고,입니다. 순서 toocollect hello 정보에서 매개 변수로 toopass hello 템플릿이 필요 hello 템플릿 파일 (이 항목 아래 템플릿 인라인 있음)을 열고 확인 hello **매개 변수** 값입니다.

이 경우 hello 템플릿이 묻는 메시지가 표시 됩니다.

* 고유한 저장소 계정 이름
* Hello VM에 대 한 관리자 사용자 이름입니다.
* 암호
* Hello world toouse 외부에 대 한 도메인 이름입니다.
* Ubuntu Server 버전 번호 -- 목록 중 하나만 허용

자세한 내용은 [사용자 이름 및 암호 요구 사항](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm)을 참조하세요.

이러한 값을 사용 하도록 결정 되 면 준비 toocreate에 대 한 그룹 하 고 Azure 구독에이 서식 파일을 배포 합니다.

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a>2 단계: hello 템플릿을 사용 하 여 hello 가상 컴퓨터 만들기
매개 변수 값을 준비 했으면 템플릿 배포에 대 한 리소스 그룹 만들기 하며 다음 hello 서식 파일을 배포 합니다.

toocreate hello 리소스 그룹으로 형식 `azure group create <group name> <location>` hello 그룹 및 toodeploy 넣을 hello 데이터 센터 위치 hello 이름의 합니다. 이 작업은 신속하게 수행됩니다.

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

지금은 toocreate hello 배포, 호출 `azure group deployment create` 전달 합니다.

* hello 템플릿 파일 (JSON 템플릿 tooa 로컬 파일 위에 hello 저장) 하는 경우입니다.
* (원할 경우 hello 파일 GitHub 또는 일부 다른 웹 주소에 toopoint) URI 템플릿.
* toodeploy 넣을 hello 리소스 그룹입니다.
* 배포 이름(선택 사항)

입력 정보 요청된 toosupply hello 매개 변수 값의 hello JSON 파일의 hello "parameters" 섹션에 됩니다. 모든 hello 매개 변수 값을 지정한 경우 배포 시작 됩니다.

다음은 예제입니다.

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

Hello 다음 유형의 정보를 받게 됩니다.

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <a id="create-a-custom-vm-image"></a>작업: 사용자 지정 VM 이미지 만들기
위의 서식 파일의 기본 사용법 hello를 살펴 보았으며, 따라서 म 수를 사용 하 여 비슷한 지침 toocreate 사용자 지정 VM Azure에서 특정.vhd 파일 로부터 통해 템플릿을 사용 하 여 hello Azure CLI 합니다. hello 차이점은이 템플릿은 지정 된 가상 하드 디스크 (VHD)에서 단일 가상 컴퓨터를 만듭니다.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Hello 서식 파일에 대 한 hello JSON 파일을 검사 하는 1 단계:
예를 들어이 섹션을 사용 하는 hello 서식 파일에 대 한 hello JSON 파일의 hello 콘텐츠는 다음과 같습니다. (또한 hello 서식 파일에 있는 [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)

다시, 기본값이 없는 hello 매개 변수에 대 한 tooenter 원하는 toofind hello 값이 필요 합니다. Hello를 실행 하는 경우 `azure group deployment create` 명령, Azure CLI hello 라는 tooenter 하면 해당 값 표시 됩니다.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a>2 단계: hello VHD 받기
이 경우 .vhd가 반드시 필요합니다. 이미 Azure에 있는 VHD를 사용하거나 업로드할 수 있습니다.

Windows 기반 가상 컴퓨터에 대 한 참조 [만들기 및 업로드 Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

Linux 기반 가상 컴퓨터에 대 한 참조 [만들기 및 업로드 hello Linux 운영 체제를 포함 하는 가상 하드 디스크](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a>3 단계: hello 템플릿을 사용 하 여 hello 가상 컴퓨터 만들기
이제 준비 toocreate hello.vhd에 따라 새 가상 컴퓨터. 사용 하 여, 그룹 toodeploy 만들기 `azure group create <location>`:

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

그런 다음 hello를 사용 하 여 hello 배포를 만들 `--template-uri` hello 템플릿에서 직접 옵션 toocall (하거나 hello를 사용할 수 있습니다 `--template-file` 옵션 toouse 로컬로 저장 된 파일). Hello 템플릿에 지정한 기본값을 사용 하므로 메시지가 표시 됩니다만 몇 가지 사항에 대 한 참고 합니다. 서로 다른 위치에서 hello 서식 파일을 배포 하는 경우 일부 명명 충돌과 hello 기본값 (특히 hello DNS 이름 만들면) 헤드로 알 수 있습니다.

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

출력은 hello 다음과 같습니다.

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>작업: 가상 네트워크 및 외부 부하 분산 장치를 사용하는 여러 VM 응용 프로그램 배포
이 서식 파일에는 포트 80에는 부하 분산 규칙을 구성 및 부하 분산 장치 아래의 toocreate 두 개의 가상 컴퓨터가 있습니다. 또한 이 템플릿에서는 저장소 계정, 가상 네트워크, 공용 IP 주소, 가용성 집합 및 네트워크 인터페이스를 배포합니다.

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

이러한 단계 toodeploy Azure PowerShell 명령을 통해 hello GitHub 서식 파일 저장소에서 리소스 관리자 템플릿을 사용 하 여 가상 네트워크 및 부하 분산 장치를 사용 하는 다중 VM 응용 프로그램을 따릅니다.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Hello 서식 파일에 대 한 hello JSON 파일을 검사 하는 1 단계:
다음은 hello 템플릿에 대 한 hello JSON 파일의 hello 내용입니다. Hello 가장 최신 버전을 원하는 경우 것 찾았으며 [서식 파일에 대 한 hello GitHub 리포지토리에서](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json)합니다. 이 항목에서는 hello `--template-uri` hello 서식 파일에서 스위치 toocall hello 사용할 수도 `--template-file` toopass 로컬 버전을 전환 합니다.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a>2 단계: hello 템플릿을 사용 하 여 hello 배포 만들기
사용 하 여 hello 서식 파일에 대 한 리소스 그룹 만들기 `azure group create <location>`합니다. 그런 다음 사용 하 여 해당 리소스 그룹에 배포를 만드는 `azure group deployment create` 하 고 전달 hello 리소스 그룹, 배포 이름을 전달 하 고 매개 변수에 기본값을 갖지 않은 hello 서식 파일에 대 한 hello 메시지에 응답 합니다.

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

이제 hello를 사용 하 여 `azure group deployment create` 명령과 hello `--template-uri` toodeploy hello 서식 파일 옵션입니다. 아래와 같이 메시지가 표시되면 매개 변수 값을 입력할 수 있습니다.

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

이 템플릿은 Windows Server 이미지를 배포하지만 Linux 이미지로 간단하게 대체할 수 있습니다. 여러 웜 관리자와 toocreate Docker 클러스터를 선택 하십시오. [가능합니다](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).

## <a id="remove-a-resource-group"></a>작업: 리소스 그룹 제거
Tooa 리소스 그룹을 다시 배포할 수 없지만 하나 완료 된 후 사용 하 여 삭제할 수 있습니다 `azure group delete <group name>`합니다.

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <a id="show-the-log-for-a-resource-group-deployment"></a>리소스 그룹 배포에 대 한 hello 로그를 표시 하는 작업:
템플릿을 만들거나 사용할 때 일반적인 작업입니다. 그룹에 대 한 hello 호출 toodisplay hello 배포 로그 `azure group log show <groupname>`, 많은 양의 발생 한 시간-또는 하지 않은 이유를 이해 하는 데 유용한 정보를 표시 하는 합니다. (배포 문제 해결에 대한 자세한 내용 및 문제에 대한 기타 정보는 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md)을 참조하세요.)

특정 오류 tootarget, 예를 들어 사용할 수 있습니다와 같은 도구 **jq** 좀 더 정확 하 게, toocorrect 필요한는 개별 오류와 같은 tooquery 것입니다. hello 다음 예제에서는 **jq** 배포에 대 한 로그 tooparse **lbgroup**찾고 오류에 대 한 합니다.

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
잘못되어 수정하거나 다시 시도할 항목을 매우 신속하게 검색할 수 있습니다. 사례를 따르는 hello에서 hello 서식 파일에 된 Vm을 만들 두 hello에 동시 잠금을 hello.vhd에 생성 합니다. (Hello 서식 파일을 수정한 후 hello 배포 성공 신속 하 게 합니다.)

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <a id="display-information-about-a-virtual-machine"></a>작업: 가상 컴퓨터에 대한 정보 표시
Hello를 사용 하 여 리소스 그룹에 특정 Vm에 대 한 정보를 볼 수 `azure vm show <groupname> <vmname>` 명령입니다. 그룹에 있는 둘 이상의 VM가 있으면 먼저 해야 toolist hello Vm 그룹에서 사용 하 여 `azure vm list <groupname>`합니다.

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

그런 다음 myVM1을 조회합니다.

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> Tooprogrammatically 저장소 콘솔 명령의 hello 출력을 조작 하는 경우에 toouse 같은 도구는 JSON을 구문 분석을 설정할 수 있습니다 있습니다  **[jq](https://github.com/stedolan/jq)**  또는  **[jsawk](https://github.com/micha/jsawk)** , 또는 hello 작업에 대 한 좋은 되는 언어 라이브러리입니다.
>
>

## <a id="log-on-to-a-linux-based-virtual-machine"></a>작업: tooa Linux 기반 가상 컴퓨터에 로그온
일반적으로 Linux 컴퓨터에 연결 된 toothrough SSH 됩니다. 자세한 내용은 참조 [어떻게 toouse와 Azure에서 Linux에 SSH](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a id="stop-a-virtual-machine"></a>작업: VM 중지
다음 명령을 실행합니다.

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> 경우이 매개 변수 tookeep hello의 가상 IP (VIP) hello vnet 사용 하 여 해당 vnet의 마지막 VM hello 합니다. <br><br> Hello를 사용 하는 경우 `StayProvisioned` 매개 변수를 계속 청구 됩니다 hello VM에 대 한 합니다.
>
>

## <a id="start-a-virtual-machine"></a>작업: VM 시작
다음 명령을 실행합니다.

```azurecli
azure vm start <group name> <virtual machine name>
```

## <a id="attach-a-data-disk"></a>작업: 데이터 디스크 연결
또한 해야 toodecide tooattach 새 디스크 또는 하나를 포함 하는지 여부를 데이터입니다. 새 디스크에 대 한 hello 명령 hello.vhd 파일 만들고 연결 hello에 동일한 명령입니다.

새 디스크 tooattach이 명령을 실행 합니다.

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

기존의 데이터 디스크를 tooattach이 명령을 실행 합니다.

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

그런 다음 Linux에서와 마찬가지로 toomount hello 디스크에 필요 합니다.

## <a name="next-steps"></a>다음 단계
훨씬 더 많은 사용 예제를 보려면 Azure CLI hello로 **arm** 모드 참조 [Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 Azure CLI를 사용 하 여 hello](../articles/xplat-cli-azure-resource-manager.md)합니다. Azure 리소스와 해당 개념에 대해 자세히 toolearn 참조 [Azure 리소스 관리자 개요](../articles/azure-resource-manager/resource-group-overview.md)합니다.

사용할 수 있는 더 많은 템플릿은 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 및 [템플릿을 사용하는 응용 프로그램 프레임워크](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
