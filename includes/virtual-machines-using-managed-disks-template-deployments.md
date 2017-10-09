# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿에서 Managed Disks 사용

이 문서는 스레드와 관리 되지 않는 디스크에서 Azure 리소스 관리자 템플릿 tooprovision 가상 컴퓨터를 사용 하는 경우 차이점 hello 안내 합니다. 이렇게 tooupdate 기존 템플릿을 사용 하는 관리 되지 않는 디스크 toomanaged 디스크 하 게 됩니다. 참조를 위해 사용 하 여 hello [101 vm-단순 windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) 템플릿을 참조 합니다. 모두 사용 하 여 hello 템플릿을 볼 수 [관리 디스크](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) 사용 하 여 이전 버전 및 [디스크를 관리 되지 않는](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) 원하는 경우 toodirectly 비교 합니다.

## <a name="unmanaged-disks-template-formatting"></a>관리되지 않는 디스크 템플릿 서식 지정

확인 수행 toobegin, 어떻게 관리 되지 않는 디스크에 배포 됩니다. 관리 되지 않는 디스크를 만들 때 저장소 계정 toohold hello VHD 파일이 필요 합니다. 새 저장소 계정을 만들거나 이미 있는 계정을 사용할 수 있습니다. 이 문서에서는 보여 어떻게 toocreate 새 저장소 계정입니다. tooaccomplish이를 아래와 같이 hello 리소스 블록에서 저장소 계정 리소스에 필요 합니다.

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

Hello 가상 컴퓨터 개체 내에서 만든 가상 컴퓨터 hello 하기 전에 hello 저장소 계정 tooensure에 대 한 종속성이 필요 합니다. Hello 내 `storageProfile` 섹션에서 다음 지정 hello hello hello 저장소 계정을 참조 하 고 hello OS 디스크 및 데이터 디스크에 대 한 필요 여부를 지정 하는 VHD 위치를의 전체 URI입니다. 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a>관리 디스크 템플릿 서식 지정

Azure 관리 되는 디스크와 디스크 hello 최상위 리소스 되며 hello 사용자가 만든 저장소 계정 toobe 더 이상 필요 합니다. 관리 되는 디스크에 먼저 hello에 드러난 `2016-04-30-preview` API 버전은 모든 후속 API 버전에서 사용할 수 있는 되었으며 이제 hello 기본 디스크 유형입니다. hello 다음 섹션에서는 hello 기본 설정 하는 과정을 안내 하 고 toofurther 사용자 디스크를 지정 하는 방법에 대해 자세히 설명 합니다.

> [!NOTE]
> Toouse API 버전은 것 보다 이후 `2016-04-30-preview` 간의 주요 변경 내용을 `2016-04-30-preview` 및 `2017-03-30`합니다.
>
>

### <a name="default-managed-disk-settings"></a>기본 관리 디스크 설정

toocreate 하면 더 이상 관리 하는 디스크를 사용 하 여 VM toocreate hello 저장소 계정 리소스 하며 다음과 같이 가상 컴퓨터 리소스를 업데이트할 수 없습니다. 특히 해당 hello 참고 `apiVersion` 반영 `2017-03-30` 및 hello `osDisk` 및 `dataDisks` tooa 더 이상 참조 hello VHD에 대 한 특정 URI입니다. Hello 디스크 ´ ֲ 추가 속성을 지정 하지 않고 배포 시 [표준 LRS 저장소](../articles/storage/common/storage-redundancy.md)합니다. 걸리는의 hello 형식 지정은 이름이 없는 경우 `<VMName>_OsDisk_1_<randomstring>` hello OS 디스크 및 `<VMName>_disk<#>_<randomstring>` 각 데이터 디스크에 대 한 합니다. 기본적으로 Azure 디스크 암호화는 사용할 수 없습니다. 캐싱은 hello OS 디스크 및 데이터 디스크에 대 한 없음에 대 한 읽기/쓰기입니다. 종속성이 있는 여전히 저장소 계정,이 진단 저장소에만 고 디스크 저장소에 필요 하지 않습니다 아래 hello 예제에서 알 수 있습니다.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a>최상위 관리 디스크 리소스 사용

Hello 가상 컴퓨터 개체에는 대체 toospecifying hello 디스크 구성에서로 최상위 디스크 리소스를 만들 수 있으며 연결 hello 가상 컴퓨터를 만드는의 일환으로 키를 누릅니다. 예를 들어 데이터 디스크로 toouse 다음과 같이 디스크 리소스를 만들 수 있습니다.

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

Hello VM 개체 내에서 연결 된 디스크 개체 toobe이을 참조할 수 있습니다. 관리 되는 hello에서 만든 디스크의 hello hello 리소스 ID 지정 `managedDisk` 속성을 사용 하면 VM이 생성 하는 hello로 hello 디스크의 hello 연결 합니다. 해당 hello 참고 `apiVersion` hello VM 리소스 너무 설정 되어`2017-03-30`입니다. 또한 VM 만들기 전에 성공적으로 만들어지면 hello 디스크 리소스 tooensure에 종속성을 작성 했습니다 note 합니다. 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>관리 디스크를 사용하여 VM에서 관리 가용성 집합 만들기

toocreate 가용성 관리 되는 관리 되는 디스크를 사용 하는 vm 집합 추가 hello `sku` 개체 toohello 가용성 리소스를 설정 하 고 hello 설정 `name` 속성 너무`Aligned`합니다. 이렇게 하면 각 VM에 대 한 hello 디스크 충분히 서로 tooavoid 단일 실패 지점을 으로부터 격리 됩니다. 또한 해당 hello 참고 `apiVersion` hello 가용성 집합 리소스에 대해 너무 설정`2017-03-30`합니다.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a>추가 시나리오 및 사용자 지정

toofind hello REST API 사양에 대 한 전체 정보를 검토 하십시오. hello [관리 되는 디스크 REST API 문서를 만들](/rest/api/manageddisks/disks/disks-create-or-update)합니다. 기본 및 템플릿 배포를 통해 제출 된 toohello API 일 수 있는 허용 되는 값으로 추가 시나리오를 찾을 수 있습니다. 

## <a name="next-steps"></a>다음 단계

* 관리 되는 디스크를 사용 하는 전체 서식 파일에 대 한 Azure 빠른 시작 리포지토리 링크를 따라 hello를 방문 합니다.
    * [관리 디스크가 있는 Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [관리 디스크가 있는 Linux VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [관리 디스크 템플릿의 전체 목록](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Hello 방문 [Azure 관리 되는 디스크 개요](../articles/virtual-machines/windows/managed-disks-overview.md) 관리 디스크 문서 toolearn에 더 알아봅니다.
* Hello를 방문 하 여 가상 컴퓨터 리소스에 대 한 hello 템플릿 참조 설명서를 검토 [Microsoft.Compute/virtualMachines 템플릿 참조](/templates/microsoft.compute/virtualmachines) 문서.
* Hello를 방문 하 여 디스크 리소스에 대 한 hello 템플릿 참조 설명서를 검토 [Microsoft.Compute/disks 템플릿 참조](/templates/microsoft.compute/disks) 문서.
 
