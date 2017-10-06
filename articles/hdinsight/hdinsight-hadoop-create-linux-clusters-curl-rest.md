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
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="8c9b0-103">Hello Azure REST API를 사용 하 여 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="8c9b0-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="8c9b0-104">HDInsight toocreate Azure 리소스 관리자 템플릿을 사용 하 여 클러스터 하 고 Azure REST API hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="8c9b0-105">Azure REST API hello hello hello HDInsight 클러스터와 같은 새 리소스 만들기를 포함 하 여 Azure 플랫폼에서에서 호스팅되는 서비스 대 tooperform 관리 작업을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c9b0-106">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8c9b0-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="8c9b0-108">이 문서 사용 하 여 hello에서 단계를 hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) hello Azure REST API로 유틸리티 toocommunicate 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="8c9b0-109">템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="8c9b0-109">Create a template</span></span>

<span data-ttu-id="8c9b0-110">Azure Resource Manager 템플릿은 **리소스 그룹**과 그 안의 모든 리소스를 설명하는 JSON 문서입니다(예: HDInsight). 이 템플릿 기반 접근 방식을 통해 toodefine hello 리소스를 템플릿과에 HDInsight에 대 한 필요한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="8c9b0-111">hello 다음 JSON 문서는 hello는 병합에서 템플릿 및 매개 변수 파일 [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), Linux 기반 만듦 SSH 사용자 계정에는 암호 toosecure hello를 사용 하 여 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

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

<span data-ttu-id="8c9b0-112">이 예제는 hello이이 문서의 단계에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="8c9b0-113">Hello 예제 대체 *값* hello에 **매개 변수** 클러스터에 대 한 hello 값이 포함 된 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c9b0-114">hello 템플릿에서 HDInsight 클러스터에 대 한 hello 기본 수의 작업자 노드 (4)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="8c9b0-115">32개 이상의 작업자 노드를 계획하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="8c9b0-116">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="8c9b0-117">Azure 구독 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="8c9b0-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="8c9b0-118">설명 하는 hello 단계에 따라 [Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) hello를 사용 하 여 tooyour 구독을 연결 하 고 `az login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="8c9b0-119">서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="8c9b0-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="8c9b0-120">이러한 단계는 hello의 요약된 버전에 *암호로 서비스 보안 주체를 만들* hello 섹션 [서비스 주체를 사용 하 여 Azure CLI toocreate tooaccess 리소스](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) 문서.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="8c9b0-121">다음이 단계를 사용 하는 tooauthenticate toohello Azure REST API 서비스 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="8c9b0-122">명령줄을 사용 하 여 hello 명령 toolist 다음 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="8c9b0-123">Hello 목록 선택 hello 구독 toouse 원하고 hello 참고 **Subscription_ID** 및 __Tenant_ID__ 열입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="8c9b0-124">이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-124">Save these values.</span></span>

2. <span data-ttu-id="8c9b0-125">Hello 다음 명령 toocreate Azure Active Directory에서 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="8c9b0-126">Hello에 대 한 hello 값 바꾸기 `--display-name`, `--homepage`, 및 `--identifier-uris` 고유한 값으로.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="8c9b0-127">새 Active Directory 항목 hello에 대 한 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c9b0-128">hello `--home-page` 및 `--identifier-uris` 값 tooreference hello에서 호스트 되는 실제 웹 페이지에 필요 하지 않습니다 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="8c9b0-129">이 값은 고유한 URI여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-129">They must be unique URIs.</span></span>

   <span data-ttu-id="8c9b0-130">hello 값이이 명령에서 반환은 hello __앱 ID__ hello 새 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="8c9b0-131">이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-131">Save this value.</span></span>

3. <span data-ttu-id="8c9b0-132">사용 하 여 hello 다음 명령은 toocreate hello를 사용 하 여 서비스 사용자 **앱 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="8c9b0-133">hello 값이이 명령에서 반환은 hello __개체 ID__합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="8c9b0-134">이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-134">Save this value.</span></span>

4. <span data-ttu-id="8c9b0-135">Hello 할당 **소유자** hello를 사용 하 여 역할 toohello 서비스 사용자 **개체 ID** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="8c9b0-136">사용 하 여 hello **구독 ID** 이전에 얻은 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="8c9b0-137">인증 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="8c9b0-137">Get an authentication token</span></span>

<span data-ttu-id="8c9b0-138">다음 명령 tooretrieve 인증 토큰 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="8c9b0-139">설정 `$TENANTID`, `$APPID`, 및 `$PASSWORD` toohello 값을 가져오거나 이전에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="8c9b0-140">이 요청에 성공한 경우 200 계열 응답을 수신 하 고 JSON 문서를 포함 하는 hello 응답 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="8c9b0-141">hello이 요청에서 반환 된 JSON 문서 라는 요소가 포함 **access_token**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="8c9b0-142">값을 hello **access_token** 가 사용 되는 tooauthentication 요청 toohello REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="8c9b0-143">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8c9b0-143">Create a resource group</span></span>

<span data-ttu-id="8c9b0-144">리소스 그룹 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="8c9b0-145">설정 `$SUBSCRIPTIONID` hello 서비스 사용자를 만드는 동안 받은 toohello 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="8c9b0-146">설정 `$ACCESSTOKEN` hello 이전 단계에서 받은 toohello 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="8c9b0-147">대체 `DATACENTERLOCATION` hello 데이터 센터와 toocreate hello 리소스 그룹 및 리소스에 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="8c9b0-148">예를 들어 "미국 중남부"입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="8c9b0-149">설정 `$RESOURCEGROUPNAME` 이 그룹에 대 한 toouse toohello 이름:</span><span class="sxs-lookup"><span data-stu-id="8c9b0-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="8c9b0-150">이 요청에 성공한 경우 200 계열 응답을 수신 하 고 hello 응답 본문 hello 그룹에 대 한 정보를 포함 하는 JSON 문서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="8c9b0-151">hello `"provisioningState"` 요소 값이 포함 `"Succeeded"`합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="8c9b0-152">배포 만들기</span><span class="sxs-lookup"><span data-stu-id="8c9b0-152">Create a deployment</span></span>

<span data-ttu-id="8c9b0-153">명령 toodeploy hello 템플릿 toohello 리소스 그룹을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="8c9b0-154">설정 `$DEPLOYMENTNAME` 이 배포에 대 한 toouse toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="8c9b0-155">Hello 템플릿 tooa 파일을 저장 하는 경우 다음 명령을 대신 hello를 사용할 수 있습니다 `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="8c9b0-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="8c9b0-156">이 요청에 성공한 경우 200 계열 응답을 수신 하 고 hello 응답 본문 hello 배포 작업에 대 한 정보를 포함 하는 JSON 문서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c9b0-157">hello 배포 제출 되 있지만 완료 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="8c9b0-158">몇 분 정도 일반적으로 약 15, 배포 toocomplete hello에 대 한 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="8c9b0-159">배포의 hello 상태 확인</span><span class="sxs-lookup"><span data-stu-id="8c9b0-159">Check hello status of a deployment</span></span>

<span data-ttu-id="8c9b0-160">다음 명령을 사용 하 여 hello hello 배포의 toocheck hello 상태:</span><span class="sxs-lookup"><span data-stu-id="8c9b0-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="8c9b0-161">이 명령은 hello 배포 작업에 대 한 정보를 포함 하는 JSON 문서를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="8c9b0-162">hello `"provisioningState"` 요소 hello 배포의 hello 상태를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="8c9b0-163">이 요소 값이 포함 되어 있으면 `"Succeeded"`, hello 배포가 성공적으로 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="8c9b0-164">문제 해결</span><span class="sxs-lookup"><span data-stu-id="8c9b0-164">Troubleshoot</span></span>

<span data-ttu-id="8c9b0-165">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c9b0-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c9b0-166">Next steps</span></span>

<span data-ttu-id="8c9b0-167">HDInsight 클러스터를 성공적으로 만든 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c9b0-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="8c9b0-168">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="8c9b0-168">Hadoop clusters</span></span>

* [<span data-ttu-id="8c9b0-169">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="8c9b0-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="8c9b0-170">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="8c9b0-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="8c9b0-171">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="8c9b0-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="8c9b0-172">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="8c9b0-172">HBase clusters</span></span>

* [<span data-ttu-id="8c9b0-173">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="8c9b0-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="8c9b0-174">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="8c9b0-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="8c9b0-175">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="8c9b0-175">Storm clusters</span></span>

* [<span data-ttu-id="8c9b0-176">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="8c9b0-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="8c9b0-177">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="8c9b0-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="8c9b0-178">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="8c9b0-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
