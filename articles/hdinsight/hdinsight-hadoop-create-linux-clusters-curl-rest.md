---
title: "Azure-Azure REST API를 사용 하 여 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 toohello Azure REST API를 제출 하 여 toocreate HDInsight 클러스터 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a>Hello Azure REST API를 사용 하 여 Hadoop 클러스터 만들기

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

HDInsight toocreate Azure 리소스 관리자 템플릿을 사용 하 여 클러스터 하 고 Azure REST API hello 하는 방법에 대해 알아봅니다.

Azure REST API hello hello hello HDInsight 클러스터와 같은 새 리소스 만들기를 포함 하 여 Azure 플랫폼에서에서 호스팅되는 서비스 대 tooperform 관리 작업을 허용 합니다.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

> [!NOTE]
> 이 문서 사용 하 여 hello에서 단계를 hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) hello Azure REST API로 유틸리티 toocommunicate 합니다.

## <a name="create-a-template"></a>템플릿 만들기

Azure Resource Manager 템플릿은 **리소스 그룹**과 그 안의 모든 리소스를 설명하는 JSON 문서입니다(예: HDInsight). 이 템플릿 기반 접근 방식을 통해 toodefine hello 리소스를 템플릿과에 HDInsight에 대 한 필요한 있습니다.

hello 다음 JSON 문서는 hello는 병합에서 템플릿 및 매개 변수 파일 [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), Linux 기반 만듦 SSH 사용자 계정에는 암호 toosecure hello를 사용 하 여 클러스터 합니다.

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used tooremotely access hello cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
                               "name": "headnode",
                               "targetInstanceCount": "2",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           },
                           {
                               "name": "workernode",
                               "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

이 예제는 hello이이 문서의 단계에 사용 됩니다. Hello 예제 대체 *값* hello에 **매개 변수** 클러스터에 대 한 hello 값이 포함 된 섹션입니다.

> [!IMPORTANT]
> hello 템플릿에서 HDInsight 클러스터에 대 한 hello 기본 수의 작업자 노드 (4)을 사용합니다. 32개 이상의 작업자 노드를 계획하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.
>
> 노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.

## <a name="log-in-tooyour-azure-subscription"></a>Azure 구독 tooyour에 로그인

설명 하는 hello 단계에 따라 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) hello를 사용 하 여 tooyour 구독을 연결 하 고 `az login` 명령입니다.

## <a name="create-a-service-principal"></a>서비스 주체 만들기

> [!NOTE]
> 이러한 단계는 hello의 요약된 버전에 *암호로 서비스 보안 주체를 만들* hello 섹션 [서비스 주체를 사용 하 여 Azure CLI toocreate tooaccess 리소스](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) 문서. 다음이 단계를 사용 하는 tooauthenticate toohello Azure REST API 서비스 사용자를 만듭니다.

1. 명령줄을 사용 하 여 hello 명령 toolist 다음 Azure 구독.

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    Hello 목록 선택 hello 구독 toouse 원하고 hello 참고 **Subscription_ID** 및 __Tenant_ID__ 열입니다. 이 값을 저장합니다.

2. Hello 다음 명령 toocreate Azure Active Directory에서 응용 프로그램을 사용 합니다.

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    Hello에 대 한 hello 값 바꾸기 `--display-name`, `--homepage`, 및 `--identifier-uris` 고유한 값으로. 새 Active Directory 항목 hello에 대 한 암호를 제공 합니다.

   > [!NOTE]
   > hello `--home-page` 및 `--identifier-uris` 값 tooreference hello에서 호스트 되는 실제 웹 페이지에 필요 하지 않습니다 인터넷 합니다. 이 값은 고유한 URI여야 합니다.

   hello 값이이 명령에서 반환은 hello __앱 ID__ hello 새 응용 프로그램에 대 한 합니다. 이 값을 저장합니다.

3. 사용 하 여 hello 다음 명령은 toocreate hello를 사용 하 여 서비스 사용자 **앱 ID**합니다.

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     hello 값이이 명령에서 반환은 hello __개체 ID__합니다. 이 값을 저장합니다.

4. Hello 할당 **소유자** hello를 사용 하 여 역할 toohello 서비스 사용자 **개체 ID** 값입니다. 사용 하 여 hello **구독 ID** 이전에 얻은 합니다.

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a>인증 토큰 가져오기

다음 명령 tooretrieve 인증 토큰 hello를 사용 합니다.

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

설정 `$TENANTID`, `$APPID`, 및 `$PASSWORD` toohello 값을 가져오거나 이전에 사용 합니다.

이 요청에 성공한 경우 200 계열 응답을 수신 하 고 JSON 문서를 포함 하는 hello 응답 본문입니다.

hello이 요청에서 반환 된 JSON 문서 라는 요소가 포함 **access_token**합니다. 값을 hello **access_token** 가 사용 되는 tooauthentication 요청 toohello REST API입니다.

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

리소스 그룹 toocreate 다음 hello를 사용 합니다.

* 설정 `$SUBSCRIPTIONID` hello 서비스 사용자를 만드는 동안 받은 toohello 구독 ID입니다.
* 설정 `$ACCESSTOKEN` hello 이전 단계에서 받은 toohello 액세스 토큰입니다.
* 대체 `DATACENTERLOCATION` hello 데이터 센터와 toocreate hello 리소스 그룹 및 리소스에 원하는 합니다. 예를 들어 "미국 중남부"입니다.
* 설정 `$RESOURCEGROUPNAME` 이 그룹에 대 한 toouse toohello 이름:

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

이 요청에 성공한 경우 200 계열 응답을 수신 하 고 hello 응답 본문 hello 그룹에 대 한 정보를 포함 하는 JSON 문서를 포함 합니다. hello `"provisioningState"` 요소 값이 포함 `"Succeeded"`합니다.

## <a name="create-a-deployment"></a>배포 만들기

명령 toodeploy hello 템플릿 toohello 리소스 그룹을 다음 hello를 사용 합니다.

* 설정 `$DEPLOYMENTNAME` 이 배포에 대 한 toouse toohello 이름입니다.

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> Hello 템플릿 tooa 파일을 저장 하는 경우 다음 명령을 대신 hello를 사용할 수 있습니다 `-d "{ template and parameters}"`:
>
> `--data-binary "@/path/to/file.json"`

이 요청에 성공한 경우 200 계열 응답을 수신 하 고 hello 응답 본문 hello 배포 작업에 대 한 정보를 포함 하는 JSON 문서를 포함 합니다.

> [!IMPORTANT]
> hello 배포 제출 되 있지만 완료 되지 않았습니다. 몇 분 정도 일반적으로 약 15, 배포 toocomplete hello에 대 한 걸릴 수 있습니다.

## <a name="check-hello-status-of-a-deployment"></a>배포의 hello 상태 확인

다음 명령을 사용 하 여 hello hello 배포의 toocheck hello 상태:

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

이 명령은 hello 배포 작업에 대 한 정보를 포함 하는 JSON 문서를 반환 합니다. hello `"provisioningState"` 요소 hello 배포의 hello 상태를 포함 합니다. 이 요소 값이 포함 되어 있으면 `"Succeeded"`, hello 배포가 성공적으로 완료 합니다.

## <a name="troubleshoot"></a>문제 해결

HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.

## <a name="next-steps"></a>다음 단계

HDInsight 클러스터를 성공적으로 만든 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork 합니다.

### <a name="hadoop-clusters"></a>Hadoop 클러스터

* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight와 함께 MapReduce 사용](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase 클러스터

* [HDInsight에서 HBase 시작](hdinsight-hbase-tutorial-get-started-linux.md)
* [HDInsight에서 HBase용 Java 응용 프로그램 개발](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm 클러스터

* [HDInsight에서 Storm용 Java 토폴로지 개발](hdinsight-storm-develop-java-topology.md)
* [HDInsight의 Storm에서 Python 구성 요소 사용](hdinsight-storm-develop-python-topology.md)
* [HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링](hdinsight-storm-deploy-monitor-topology-linux.md)
