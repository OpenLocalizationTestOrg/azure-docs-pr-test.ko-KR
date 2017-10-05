---
title: "2015년 8월 1일 스키마 업데이트 미리 보기 - Azure Logic Apps | Microsoft Docs"
description: "스키마 버전 2015-08-01-preview로 Azure Logic Apps에 대한 JSON 정의 만들기"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="6d396-103">Azure Logic Apps에 대한 스키마 업데이트 - 2015년 8월 1일 미리 보기</span><span class="sxs-lookup"><span data-stu-id="6d396-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="6d396-104">Azure Logic Apps에 대한 새 스키마 및 API 버전에 논리 앱의 안정성 및 사용 편의성을 개선하는 향상된 주요 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="6d396-105">**APIApp** 작업 유형이 새로운 [**APIConnection**](#api-connections) 작업 유형으로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="6d396-106">**Repeat**가 [**Foreach**](#foreach)로 이름이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="6d396-107">[**HTTP 수신기** API 앱](#http-listener)은 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="6d396-108">하위 워크플로 호출에 [새 스키마](#child-workflows)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="6d396-109">API 연결로 이동</span><span class="sxs-lookup"><span data-stu-id="6d396-109">Move to API connections</span></span>

<span data-ttu-id="6d396-110">가장 큰 변화는 API를 사용하기 위해 API Apps를 Azure 구독에 더 이상 배포하지 않아도 되므로 API를 사용할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="6d396-111">API를 사용하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="6d396-112">관리되는 API</span><span class="sxs-lookup"><span data-stu-id="6d396-112">Managed APIs</span></span>
* <span data-ttu-id="6d396-113">사용자 지정 Web API</span><span class="sxs-lookup"><span data-stu-id="6d396-113">Your custom Web APIs</span></span>

<span data-ttu-id="6d396-114">이러한 각 방식은 관리 및 호스팅 모델이 다르므로 약간 다르게 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="6d396-115">이 모델의 장점은 사용자의 Azure 리소스 그룹에 배포되는 리소스로 더 이상 제약되지 않는다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="6d396-116">관리되는 API</span><span class="sxs-lookup"><span data-stu-id="6d396-116">Managed APIs</span></span>

<span data-ttu-id="6d396-117">Microsoft는 사용자를 대신해서 Office 365, Salesforce, Twitter, FTP 등의 몇 가지 API를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="6d396-118">관리되는 일부 API를 Bing Translate처럼 있는 그대로 사용할 수도 있지만 구성이 필요한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="6d396-119">이 구성을 *연결*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="6d396-120">예를 들어 Office 365를 사용하는 경우 Office 365 로그인 토큰을 포함하는 연결을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="6d396-121">이 토큰은 논리 앱에서 항상 Office 365 API를 호출할 수 있도록 안전하게 저장되어 새로 고침됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="6d396-122">또는 SQL이나 FTP 서버에 연결하려는 경우 연결 문자열이 있는 연결을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="6d396-123">이 정의에서 이러한 작업을 `APIConnection`이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="6d396-124">다음은 전자 메일을 보내도록 Office 365를 호출하는 연결에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

<span data-ttu-id="6d396-125">`host` 개체는 API 연결에 고유한 입력 부분으로, `api` 및 `connection`의 두 부분을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="6d396-126">`api` 에는 관리 API가 호스팅되는 런타임 URL이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="6d396-127">`GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`를 호출하여 사용 가능한 모든 관리 API를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="6d396-128">API를 사용하는 경우 API에 *연결 매개 변수*가 정의되어 있거나 그렇지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="6d396-129">정의되지 않은 경우 *연결*이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="6d396-130">API가 정의된 경우에는 연결을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="6d396-131">만들어진 연결에는 사용자가 선택한 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="6d396-132">다음에 `host` 개체 내의 `connection` 개체에서 이 이름을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="6d396-133">리소스 그룹에서 연결을 만들려면 다음을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="6d396-134">다음 본문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="6d396-135">Azure Resource Manager 템플릿에서 관리 API 배포</span><span class="sxs-lookup"><span data-stu-id="6d396-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="6d396-136">대화형 로그인이 필요하지 않다면 Azure Resource Manager 템플릿에서 전체 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="6d396-137">로그인이 필요한 경우 Azure Resource Manager 템플릿을 사용하여 모든 항목을 설정할 수 있지만 포털에 방문하여 연결에 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

<span data-ttu-id="6d396-138">이 예제에서 해당 연결은 리소스 그룹에서 작동하는 리소스일 뿐임을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="6d396-139">연결은 구독에서 사용할 수 있는 관리 API를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="6d396-140">사용자 지정 Web API</span><span class="sxs-lookup"><span data-stu-id="6d396-140">Your custom Web APIs</span></span>

<span data-ttu-id="6d396-141">사용자 고유의 API(Microsoft 관리 항목 아님)를 사용하는 경우 기본 제공 **HTTP** 작업을 사용하여 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="6d396-142">이상적인 환경을 위해서는 API에 대한 Swagger 끝점을 노출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="6d396-143">이 끝점에서는 논리 앱 디자이너가 API에 대한 입력 및 출력을 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="6d396-144">Swagger가 없는 경우 디자이너는 입력 및 출력을 불투명 JSON 개체로 표시할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="6d396-145">다음은 새 `metadata.apiDefinitionUrl` 속성을 보여 주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

<span data-ttu-id="6d396-146">Azure App Service에서 Web API를 호스트하는 경우 Web API는 디자이너에서 사용 가능한 작업 목록에 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="6d396-147">그렇지 않으면 URL에 직접 붙여 넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="6d396-148">Swagger에서 지원하는 어떤 방법으로든 API 자체를 보호할 수 있지만 Swagger 끝점을 논리 앱 디자이너에서 사용할 수 있게 하려면 끝점을 인증하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="6d396-149">2015-08-01-preview로 배포된 API 앱 호출</span><span class="sxs-lookup"><span data-stu-id="6d396-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="6d396-150">이전에 API 앱을 배포한 경우 **HTTP** 작업을 통해 앱을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="6d396-151">예를 들어 Dropbox를 사용하여 파일을 나열하는 경우 **2014-12-01-preview** 스키마 버전 정의에 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="6d396-152">이 예제와 같은 동등한 HTTP 작업을 생성할 수 있으나 논리 앱 정의의 매개 변수 섹션은 변경되지 않고 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="6d396-153">이러한 속성을 하나씩 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="6d396-154">작업 속성</span><span class="sxs-lookup"><span data-stu-id="6d396-154">Action property</span></span> | <span data-ttu-id="6d396-155">설명</span><span class="sxs-lookup"><span data-stu-id="6d396-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="6d396-156">`Http`다음 위치 대신`APIapp`</span><span class="sxs-lookup"><span data-stu-id="6d396-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="6d396-157">논리 앱 디자이너에서 이 작업을 사용하려는 경우 다음에서 생성되는 메타데이터 끝점을 포함합니다. `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="6d396-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="6d396-158">생성된 위치: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="6d396-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="6d396-159">항상 `POST`</span><span class="sxs-lookup"><span data-stu-id="6d396-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="6d396-160">API App 매개 변수와 동일</span><span class="sxs-lookup"><span data-stu-id="6d396-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="6d396-161">API App 인증과 동일</span><span class="sxs-lookup"><span data-stu-id="6d396-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="6d396-162">이 방법은 모든 API App 작업에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="6d396-163">하지만 이러한 이전 API Apps는 더 이상 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="6d396-164">따라서 이전의 다른 두 옵션 중 하나로 전환해야 합니다(관리 API 또는 사용자 지정 Web API 호스팅).</span><span class="sxs-lookup"><span data-stu-id="6d396-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="6d396-165">'repeat'가 'foreach'로 이름 변경됨</span><span class="sxs-lookup"><span data-stu-id="6d396-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="6d396-166">이전 스키마 버전에서 **Repeat**가 혼동되고 **Repeat**가 실제로 for each loop인지 제대로 포착되지 않는다는 의견을 많이 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="6d396-167">따라서 `repeat`에서 `foreach`로 이름을 변경하였습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="6d396-168">예를 들어 이전에는 다음과 같이 작성해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-168">For example, previously you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

<span data-ttu-id="6d396-169">이제 다음과 같이 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-169">Now you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

<span data-ttu-id="6d396-170">이전에 함수 `@repeatItem()`은 반복되는 현재 항목을 참조하는 데 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="6d396-171">이 함수가 이제 `@item()`으로 단순화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="6d396-172">'foreach'의 참조 출력</span><span class="sxs-lookup"><span data-stu-id="6d396-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="6d396-173">간소화하기 위해 `foreach` 작업의 출력은 `repeatItems`라는 개체에 래핑되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="6d396-174">한편 이전 `repeat` 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-174">While the outputs from the previous `repeat` example were:</span></span>

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

<span data-ttu-id="6d396-175">그렇지만 이제 이 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-175">Now these outputs are:</span></span>

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

<span data-ttu-id="6d396-176">이전에는 이러한 출력을 참조할 때 작업 본문을 얻으려면 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="6d396-177">이제 대신 다음을 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-177">Now you can do instead:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="6d396-178">이와 같이 변경되면서 함수 `@repeatItem()`, `@repeatBody()` 및 `@repeatOutputs()`가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="6d396-179">네이티브 HTTP 수신기</span><span class="sxs-lookup"><span data-stu-id="6d396-179">Native HTTP listener</span></span>

<span data-ttu-id="6d396-180">이제 HTTP 수신기 기능이 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="6d396-181">따라서 HTTP 수신기 API App을 더 이상 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="6d396-182">[논리 앱 끝점을 호출 가능한 상태로 만드는 방법에 대한 자세한 내용은 여기](../logic-apps/logic-apps-http-endpoint.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d396-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="6d396-183">이러한 변경으로 함수 `@accessKeys()`가 제거되고 필요한 경우 끝점을 가져오기 위해 `@listCallbackURL()` 함수로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="6d396-184">또한 이제 논리 앱에서 트리거를 하나 이상 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="6d396-185">워크플로를 `/run`하려는 경우 `manual`, `apiConnectionWebhook` 또는 `httpWebhook` 트리거 중 하나를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="6d396-186">하위 워크플로 호출</span><span class="sxs-lookup"><span data-stu-id="6d396-186">Call child workflows</span></span>

<span data-ttu-id="6d396-187">이전에는 하위 워크플로를 호출하려면 해당 워크플로로 이동하여 액세스 토큰을 가져온 후 해당 하위 워크플로를 호출하려는 논리 앱 정의에 토큰을 붙여넣어야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="6d396-188">새 스키마를 사용할 경우 Logic Apps 엔진은 런타임에 하위 워크플로에 대한 SAS를 자동으로 생성합니다. 따라서 정의에 어떠한 비밀도 붙여넣을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="6d396-189">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-189">Here is an example:</span></span>

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

<span data-ttu-id="6d396-190">두 번째 향상된 내용은 들어오는 요청에 대한 전체 액세스 권한을 하위 워크플로에 부여하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="6d396-191">따라서 *queries* 섹션 및 *headers* 개체에서 매개 변수를 전달할 수 있으며 전체 본문을 완전히 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="6d396-192">마지막으로, 하위 워크플로에 필요한 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="6d396-193">이전에는 하위 워크플로를 직접 호출할 수 있었지만 이제는 상위에서 호출할 워크플로에 트리거 끝점을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="6d396-194">일반적으로 `manual` 유형의 트리거를 추가한 후 상위 정의에 해당 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="6d396-195">특히 호출 중인 트리거를 항상 지정해야 하므로 `host` 속성은 `triggerName`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="6d396-196">기타 변경 내용</span><span class="sxs-lookup"><span data-stu-id="6d396-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="6d396-197">새 'queries' 속성</span><span class="sxs-lookup"><span data-stu-id="6d396-197">New 'queries' property</span></span>

<span data-ttu-id="6d396-198">이제 모든 작업 유형에서 `queries`라는 새 입력을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="6d396-199">이 입력은 문자열을 직접 조합할 필요가 없는 구조화된 개체일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="6d396-200">'parse()' 함수 이름이 'json()'으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="6d396-201">곧 더 많은 콘텐츠가 추가될 예정이므로 `parse()` 함수 이름을 `json()`으로 바꾸었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="6d396-202">서비스 예정: 엔터프라이즈 통합 API</span><span class="sxs-lookup"><span data-stu-id="6d396-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="6d396-203">관리된 버전의 엔터프라이즈 통합 API가 없습니다(예: AS2).</span><span class="sxs-lookup"><span data-stu-id="6d396-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="6d396-204">그 동안은 HTTP 작업을 통해 기존에 배포된 BizTalk API를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d396-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="6d396-205">자세한 내용은 [통합 로드맵](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/)의 "이미 배포된 API 앱 사용"을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d396-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
