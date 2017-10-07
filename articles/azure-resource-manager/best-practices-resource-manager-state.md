---
title: "Azure 템플릿 간에 복잡 한 값 aaaPass | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 및 연결 된 템플릿을 사용 하 여 복잡 한 개체 tooshare 상태 데이터를 사용 하는 방법을 권장 하는 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>공유 상태 tooand Azure 리소스 관리자 템플릿
이 항목에서는 템플릿 내에서 상태를 관리 및 공유하는 방법에 대한 모범 사례를 보여 줍니다. hello 매개 변수 및 변수를이 항목의 뒤에 예 tooconveniently의 배포 요구 사항을 구성의 hello 유형의 개체를 정의할 수 있습니다. 이러한 예를 통해 사용자 환경에 맞는 속성 값으로 고유한 개체를 구현할 수 있습니다.

이 항목은 더 큰 백서의 일부입니다. 전체 용지 tooread hello 다운로드 [세계 클래스 리소스 관리자 템플릿 고려 사항 및 입증 된 사례](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf)합니다.

## <a name="provide-standard-configuration-settings"></a>표준 구성 설정 제공
총 유연 하 고 무수 한 변형 하는 서식 파일, 제공 하는 것이 아니라 일반적인 패턴은 tooprovide 알려진된 구성 선택 합니다. 실제로 샌드박스, 작음, 중간 및 대량과 같은 표준 티셔츠 크기를 선택할 수 있습니다. 티셔츠 크기의 다른 예에는 커뮤니티 버전이나 엔터프라이즈 버전 같은 제품이 있습니다. 그 외 경우에는 Map Reduce 또는 No SQL 같은 특정 워크로드에 대한 기술 구성이 있습니다.

복잡 한 개체 "속성 모음" 라고도 하는 데이터 컬렉션을 포함 하는 변수 만들고 해당 데이터 toodrive hello 리소스 선언이 서식 파일에 사용 합니다. 이러한 접근 방식은 고객을 위해 미리 구성된 다양한 크기의 좋은, 알려진 구성을 제공합니다. 알려진된 구성을 없이 hello 서식 파일의 사용자 확인 플랫폼 리소스 제약 조건에서 자체적으로 요소에는 클러스터 크기 조정 하 고 해야 수학 tooidentify hello 결과의 저장소 계정 및 기타 리소스 분할을 수행 (toocluster 크기 인해 및 리소스 제약 조건)입니다. 또한 hello 고객에 대 한 향상 된 환경 toomaking 몇 가지 알려진된 구성을 쉽게 toosupport 됩니다 하 고 더 높은 수준의 밀도 제공 하는 데 합니다.

hello 방법을 예제와 다음 복잡 한 데이터의 컬렉션을 나타내는 개체를 포함 하는 toodefine 변수입니다. 가상 컴퓨터 크기, 네트워크 설정, 운영 체제 설정 및 가용성 설정에 사용 되는 값을 정의 하는 hello 컬렉션입니다.

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

해당 hello 확인 **tshirtSize** 변수 연결 매개 변수를 통해 제공 하는 hello 티셔츠 크기 (**작은**, **보통**, **Large**) toohello 텍스트 **tshirtSize**합니다. 티셔츠 크기에 대 한이 변수 tooretrieve hello 관련 된 복잡 한 개체 변수를 사용 합니다.

그런 다음 hello 서식 파일의 뒷부분에 나오는 이러한 변수를 참조할 수 있습니다. hello 기능 tooreference 라는-변수 및 해당 속성 hello 템플릿 구문을 간소화 하 고 쉽게 toounderstand 컨텍스트. 다음 예제는 hello tooset 값 앞에 표시 된 hello 개체를 사용 하 여 리소스 toodeploy를 정의 합니다. 에 대 한 hello 값을 검색 하 여 hello VM 크기는 설정 하는 예를 들어 `variables('tshirtSize').vmSize` 에서 hello 디스크 크기를 검색에 대 한 hello 값 동안 `variables('tshirtSize').diskSize`합니다. 또한 연결 된 서식 파일에 대 한 hello 값으로 설정 되어에 대 한 URI를 hello `variables('tshirtSize').vmTemplate`합니다.

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>상태 tooa 서식 파일을 전달 합니다.
배포 중에 직접 제공한 매개 변수를 통해 템플릿으로 상태를 공유합니다.

다음 템플릿에서 테이블 일반적으로 사용 되는 목록을 매개 변수 번호입니다.

| 이름 | 값 | 설명 |
| --- | --- | --- |
| location |제한된 Azure 영역 목록의 문자열 |hello 위치 hello 리소스가 배포 되는 위치입니다. |
| storageAccountNamePrefix |문자열 |Hello hello VM 디스크를 배치 하는 저장소 계정에 대 한 고유 DNS 이름 |
| domainName |문자열 |Hello 형식에서 hello 공개적으로 액세스 가능한 jumpbox VM의 도메인 이름: **{domainName}. { location}.cloudapp.com** 예: **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |문자열 |Hello Vm에 대 한 사용자 이름 |
| adminPassword |문자열 |Hello Vm에 대 한 암호 |
| tshirtSize |제공된 티셔츠 크기의 제한된 목록에서 가져온 문자열 |배율 단위 크기 tooprovision 명명 된 번호입니다. 예: "Small", "Medium", "Large" |
| virtualNetworkName |문자열 |소비자 hello hello 가상 네트워크의 이름 toouse를 하려고 합니다. |
| enableJumpbox |제한된 목록에서 가져온 문자열(enabled/disabled) |매개 변수를 식별 하는 여부 tooenable hello 환경에 대 한 jumpbox 합니다. 값: "enabled", "disabled" |

hello **tshirtSize** hello 이전 섹션에서 사용 되는 매개 변수를 이루어집니다.

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>상태 toolinked 템플릿 전달
Toolinked 서식 파일에 연결할 때 종종 정적을 함께 사용 했으며 변수를 생성 합니다.

### <a name="static-variables"></a>정적 변수
정적 변수 예: Url 템플릿 전체에서 사용 되는 사용 되는 tooprovide 기준 값 경우가 많습니다.

다음 템플릿 발췌 hello에 `templateBaseUrl` GitHub에서 hello 서식 파일에 대 한 hello 루트 위치를 지정 합니다. 새 변수를 작성 하는 hello 다음 줄 `sharedTemplateUrl` hello 기준 URL hello 공유 리소스에 대 한 템플릿의 hello 알려진된 이름으로 연결 합니다. 해당 줄 아래 복잡 한 개체 변수는 사용 되는 toostore 티셔츠 크기, 여기서 hello 기준 URL은 연결 된 toohello 구성 템플릿 위치를 알고 있으며 hello에 저장 된 `vmTemplate` 속성입니다.

이 방법의 hello 이점은 hello 템플릿 위치 변경 되 면 하기만 하면 연결 된 hello 템플릿 전체에서 전달 하는 한 곳에서 toochange hello 정적 변수입니다.

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>생성된 변수
또한 toostatic 변수에서 여러 변수는 동적으로 생성 됩니다. 이 섹션의 hello 일반적인 형식이 생성 된 변수를 식별합니다.

#### <a name="tshirtsize"></a>tshirtSize
위의 hello 예제에서이 생성 된 변수 잘 알고 있다면 합니다.

#### <a name="networksettings"></a>networkSettings
용량, 기능, 또는 범위가 지정 된 종단 간 솔루션 템플릿을 hello 연결 된 템플릿 일반적으로 네트워크에 있는 리소스를 만듭니다. 간단 하 게 하는 한 가지 방법은 toouse 복합 개체 toostore 네트워크 설정 이며 toolinked 서식 파일을 전달 합니다.

아래에서 네트워크 설정을 전달하는 예제를 볼 수 있습니다.

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
연결된 템플릿에서 만든 리소스는 종종 가용성 집합에 배치됩니다. 다음 예제는 hello, hello 가용성 집합 이름을 지정 하 고도 장애 도메인을 hello와 업데이트 도메인 개수 toouse 합니다.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

여러 가용성 집합 (예를 들어 마스터 노드가 마다 하나씩) 및 다른 데이터 노드를 해야 하는 경우 이름을 접두사로 사용 가용성 집합이 여러 개 지정 하거나 특정 티셔츠 크기에 대 한 변수를 만들기 위한 앞에 표시 된 hello 모델을 따를 수 있습니다.

#### <a name="storagesettings"></a>storageSettings
저장소 세부 정보는 연결된 템플릿과 종종 공유됩니다. 다음 hello 예제에는 *storageSettings* 개체 hello에 대 한 세부 정보를 저장소 계정 및 컨테이너 이름을 제공 합니다.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
연결 된 템플릿으로 알려진된 여러 가지 구성 유형을 통해 toopass 운영 체제 설정을 toovarious 노드 종류를 할 수 있습니다. 복잡 한 개체는 쉽게 toostore 및 공유 운영 체제 정보 및을 사용 하면 보다 쉽게 toosupport 배포에 대 한 여러 운영 체제 선택 합니다.

hello 다음 보여 주는 예제에 대 한 개체 *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
생성된 변수인 *machineSettings*는 VM을 만들기 위한 혼합된 핵심 변수를 포함하는 복잡한 개체입니다. hello 변수는 관리자 사용자 이름 및 암호, hello VM 이름에 대 한 접두사 및 운영 체제 이미지 참조를 포함 합니다.

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

*osImageReference* 검색 hello hello 값 *osSettings* hello 기본 서식 파일에 정의 된 변수입니다. 즉, VM에 대 한 hello 운영 체제를 쉽게 변경할 수 있습니다-완전히 또는 템플릿 소비자의 hello 기본 설정에 기반 합니다.

#### <a name="vmscripts"></a>vmScripts
hello *vmScripts* 개체 스크립트 toodownload hello에 대 한 세부 정보를 포함 하 고 외부 및 내부 참조를 포함 하 여 VM 인스턴스에서 실행 합니다. 외부 참조 hello 인프라를 포함합니다.
내부 참조 hello 설치 된 소프트웨어를 설치 및 구성에 포함 됩니다.

Hello를 사용 하 여 *scriptsToDownload* 속성 toolist hello toodownload toohello VM을 스크립팅 합니다. 이 개체는 또한 여러 유형의 동작에 대 한 참조가 toocommand 줄 인수를 포함합니다. 이 해당 각 개별 노드, 설치 된 모든 노드에 배포 된 후에 실행 되 고 서식 파일을 지정 하는 특정 tooa 수 있는 추가 스크립트에 대 한 hello 기본 설치를 실행 합니다.

이 예제에서 사용 되는 템플릿 toodeploy MongoDB 중재자 toodeliver 높은 가용성을 필요로 하는. hello *arbiterNodeInstallCommand* 너무 추가한*vmScripts* tooinstall hello 중재자 라고 합니다.

hello 변수 섹션 hello 적절 한 값을 사용 하 여 hello tooexecute hello 스크립트를 특정 텍스트를 정의 하는 hello 변수를 찾을 위치입니다.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>템플릿에서 상태 반환
뿐만 아니라 수 데이터를 템플릿으로,, 공유 데이터 백 toohello 호출 서식 파일을 수도 있습니다. Hello에 **출력** 섹션, 연결 된 템플릿의 hello 원본 템플릿을 사용할 수 있는 키/값 쌍을 제공할 수 있습니다.

hello 다음 예제에서는 어떻게 toopass hello 연결 된 서식 파일에서 생성 된 개인 IP 주소

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

Hello 주 템플릿 내에서 구문 다음 hello로 해당 데이터를 사용할 수 있습니다.

    "[reference('master-node').outputs.masterip.value]"

이 식은 hello 출력 섹션 또는 hello 기본 서식 파일의 hello 리소스 섹션에서 사용할 수 있습니다. Hello 런타임 상태를 사용 하기 때문에 hello 식 hello 변수 섹션에서 사용할 수 없습니다. tooreturn hello 기본 서식 파일에서 사용 하 여가이 값:

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

가상 컴퓨터에 대 한 연결 된 템플릿 tooreturn 데이터 디스크의 섹션을 출력 하는 hello를 사용 하는 예제를 참조 [가상 컴퓨터에 대 한 여러 데이터 디스크를 만드는](resource-group-create-multiple.md)합니다.

## <a name="define-authentication-settings-for-virtual-machine"></a>가상 컴퓨터에 대한 인증 설정 정의
Hello를 사용할 수는 가상 컴퓨터에 대 한 구성 설정 toospecify hello 인증 설정에 대해 이전에 표시 된 같은 패턴입니다. 인증 유형 hello에에서 전달 하기 위한 매개 변수를 만듭니다.

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

Hello 서로 다른 인증 유형과 hello hello 매개 변수 값에 따라이 배포에 대 한 어떤 유형이 사용 되는 변수 toostore에 대 한 변수를 추가 합니다.

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

Hello 설정 hello 가상 컴퓨터를 정의할 때 **osProfile** 만든 toohello 변수입니다.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>다음 단계
* toolearn hello 템플릿의 hello 섹션에 대 한 참조 [Azure 리소스 관리자 템플릿 작성](resource-group-authoring-templates.md)
* toosee hello 함수는 서식 파일에서 사용할 수 있는 참조 [Azure 리소스 관리자 템플릿 함수](resource-group-template-functions.md)
