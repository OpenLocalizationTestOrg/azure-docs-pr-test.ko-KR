---
title: "Azure REST API를 사용하여 Hadoop 클러스터 만들기 - Azure | Microsoft Docs"
description: "Azure REST API에 Azure Resource Manager 템플릿을 제출하여 HDInsight 클러스터를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: a36a41c231472ceeeb46d02ddb65549b1c79728a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="89c80-103">Azure REST API를 사용하여 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="89c80-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="89c80-104">Azure Resource Manager 템플릿 및 Azure REST API를 사용하여 HDInsight 클러스터를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="89c80-105">Azure REST API를 사용하면 HDInsight 클러스터 등과 같은 새 리소스 생성을 포함하여 Azure 플랫폼에서 호스트되는 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89c80-106">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="89c80-107">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89c80-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="89c80-108">이 문서의 단계는 [curl(https://curl.haxx.se/)](https://curl.haxx.se/) 유틸리티를 사용하여 Azure REST API와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="89c80-109">템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="89c80-109">Create a template</span></span>

<span data-ttu-id="89c80-110">Azure Resource Manager 템플릿은 **리소스 그룹**과 그 안의 모든 리소스를 설명하는 JSON 문서입니다(예: HDInsight). 이 템플릿 기반 접근 방식을 사용하면 하나의 템플릿에서 HDInsight에 필요한 리소스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="89c80-111">다음 JSON 문서는 [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password)의 템플릿과 매개 변수 파일의 병합기로, 암호를 사용하여 SSH 사용자 계정을 보호하는 Linux 기반 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

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
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to remotely access the cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
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

<span data-ttu-id="89c80-112">이 예는 이 문서의 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="89c80-113">**매개 변수** 섹션에 있는 예제 *값*을 클러스터에 대한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89c80-114">이 템플릿에서는 HDInsight 클러스터에 대해 작업자 노드의 기본 개수(4)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="89c80-115">32개 이상의 작업자 노드를 계획하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="89c80-116">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89c80-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="89c80-117">Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="89c80-118">[Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)의 단계에 따라 `az login` 명령을 사용하여 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="89c80-119">서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="89c80-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="89c80-120">이러한 단계는 [Azure CLI를 사용하여 리소스에 액세스하기 위한 서비스 주체 만들기](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) 문서의 *암호를 사용하여 서비스 주체 만들기* 섹션의 요약된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="89c80-121">이러한 단계에서는 Azure REST API에 인증하는 데 사용되는 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="89c80-122">명령줄에서 다음 명령을 사용하여 Azure 구독을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="89c80-123">목록에서 사용하려는 구독을 선택하고 **Subscription_ID** 및 __Tenant_ID__ 열을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="89c80-124">이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-124">Save these values.</span></span>

2. <span data-ttu-id="89c80-125">다음 명령을 사용하여 Azure Active Directory에서 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="89c80-126">`--display-name`, `--homepage` 및 `--identifier-uris`에 대한 값을 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="89c80-127">새 Active Directory 항목에 대한 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="89c80-128">`--home-page` 및 `--identifier-uris` 값은 인터넷에서 호스트되는 실제 웹 페이지를 참조할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="89c80-129">이 값은 고유한 URI여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-129">They must be unique URIs.</span></span>

   <span data-ttu-id="89c80-130">이 명령에서 반환되는 값은 새 응용 프로그램에 대한 __App ID__입니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="89c80-131">이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-131">Save this value.</span></span>

3. <span data-ttu-id="89c80-132">다음 명령을 수행하여 **App ID**를 사용해 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="89c80-133">이 명령에서 반환되는 값은 __개체 ID__입니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="89c80-134">이 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-134">Save this value.</span></span>

4. <span data-ttu-id="89c80-135">**개체 ID** 값을 사용하여 **소유자** 역할을 서비스 주체에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="89c80-136">또한 이전에 받은 **구독 ID**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="89c80-137">인증 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="89c80-137">Get an authentication token</span></span>

<span data-ttu-id="89c80-138">다음 명령을 사용하여 인증 토큰을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="89c80-139">`$TENANTID`, `$APPID` 및 `$PASSWORD`를 얻거나 이전에 사용한 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="89c80-140">이 요청에 성공하면 200 시리즈 응답을 받게 되며 응답 본문에 JSON 문서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="89c80-141">이 요청에서 반환되는 JSON 문서는 **access_token**이라는 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="89c80-142">**access_token**의 값은 REST API에 대한 인증 요청에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="89c80-143">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="89c80-143">Create a resource group</span></span>

<span data-ttu-id="89c80-144">다음을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="89c80-145">`$SUBSCRIPTIONID`를 서비스 주체를 만들 때 받은 구독 ID로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="89c80-146">`$ACCESSTOKEN`을 이전 단계에서 받은 액세스 토큰으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="89c80-147">`DATACENTERLOCATION`을 리소스 그룹과 리소스를 만들려는 데이터 센터로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="89c80-148">예를 들어 "미국 중남부"입니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="89c80-149">`$RESOURCEGROUPNAME`을 이 그룹에 사용하려는 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="89c80-150">이 요청에 성공하면 200 시리즈 응답을 받게 되며 응답 본문에 그룹 정보가 담긴 JSON 문서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="89c80-151">`"provisioningState"` 요소는 `"Succeeded"`라는 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="89c80-152">배포 만들기</span><span class="sxs-lookup"><span data-stu-id="89c80-152">Create a deployment</span></span>

<span data-ttu-id="89c80-153">다음 명령을 사용하여 리소스 그룹에 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="89c80-154">`$DEPLOYMENTNAME`을 이 배포에 사용하려는 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="89c80-155">템플릿을 파일에 저장한 경우 `-d "{ template and parameters}"` 대신 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="89c80-156">이 요청에 성공하면 200 시리즈 응답을 받게 되며 응답 본문에 배포 작업 정보가 담긴 JSON 문서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89c80-157">배포가 제출되었지만 완료된 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="89c80-158">배포가 완료되려면 보통 몇 분(보통 15분 전후)이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="89c80-159">배포 상태 확인</span><span class="sxs-lookup"><span data-stu-id="89c80-159">Check the status of a deployment</span></span>

<span data-ttu-id="89c80-160">배포 상태를 확인하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="89c80-161">이 명령은 배포 작업 관련 정보가 담긴 JSON 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="89c80-162">`"provisioningState"` 요소는 배포의 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="89c80-163">이 요소가 `"Succeeded"` 값을 포함하면 배포가 성공적으로 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="89c80-164">문제 해결</span><span class="sxs-lookup"><span data-stu-id="89c80-164">Troubleshoot</span></span>

<span data-ttu-id="89c80-165">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89c80-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89c80-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89c80-166">Next steps</span></span>

<span data-ttu-id="89c80-167">HDInsight 클러스터를 성공적으로 만들었으므로 다음을 사용하여 클러스터 작업을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89c80-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="89c80-168">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="89c80-168">Hadoop clusters</span></span>

* [<span data-ttu-id="89c80-169">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="89c80-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="89c80-170">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="89c80-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="89c80-171">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="89c80-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="89c80-172">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="89c80-172">HBase clusters</span></span>

* [<span data-ttu-id="89c80-173">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="89c80-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="89c80-174">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="89c80-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="89c80-175">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="89c80-175">Storm clusters</span></span>

* [<span data-ttu-id="89c80-176">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="89c80-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="89c80-177">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="89c80-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="89c80-178">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="89c80-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
