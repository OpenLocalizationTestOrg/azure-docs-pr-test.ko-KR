---
title: "Azure Service Fabric 및 Azure CLI 2.0 시작"
description: "Azure CLI 버전 2.0에서 Azure Service Fabric 명령 모듈을 사용하는 방법에 대해 알아봅니다. 클러스터에 연결하는 방법 및 응용 프로그램 암호를 관리하는 방법을 알아봅니다."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="6f020-104">Azure Service Fabric 및 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6f020-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="6f020-105">Azure CLI(Azure 명령줄 도구) 버전 2.0에는 Azure Service Fabric 클러스터를 관리할 수 있는 명령이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-105">The Azure command-line tool (Azure CLI) version 2.0 includes commands to help you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="6f020-106">Azure CLI 및 Service Fabric을 시작하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-106">Learn how to get started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="6f020-107">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="6f020-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="6f020-108">Azure CLI 2.0 명령을 사용하여 Service Fabric 클러스터와 상호 작용하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-108">You can use Azure CLI 2.0 commands to interact with and manage Service Fabric clusters.</span></span> <span data-ttu-id="6f020-109">Azure CLI의 최신 버전을 가져오려면 [Azure CLI 2.0 표준 설치 프로세스](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6f020-109">To get the latest version of Azure CLI, follow the [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="6f020-110">자세한 내용은 [Azure CLI 2.0 개요](https://docs.microsoft.com/en-us/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f020-110">For more information, see the [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="6f020-111">Azure CLI 구문</span><span class="sxs-lookup"><span data-stu-id="6f020-111">Azure CLI syntax</span></span>

<span data-ttu-id="6f020-112">Azure CLI에서 모든 Service Fabric 명령은 접두사로 `az sf`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="6f020-113">사용할 수 있는 명령에 대한 일반적인 정보는 `az sf -h`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-113">For general information about the commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="6f020-114">단일 명령의 도움말은 `az sf <command> -h`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="6f020-115">Azure CLI의 Service Fabric 명령은 다음과 같은 명명 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="6f020-116">`<object>`는 `<action>`의 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-116">`<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="6f020-117">클러스터 선택</span><span class="sxs-lookup"><span data-stu-id="6f020-117">Select a cluster</span></span>

<span data-ttu-id="6f020-118">모든 작업을 수행하기 전에 연결할 클러스터를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-118">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="6f020-119">예제를 보려면 다음 코드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f020-119">For an example, see the following code.</span></span> <span data-ttu-id="6f020-120">코드는 보안되지 않은 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-120">The code connects to an unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="6f020-121">프로덕션 환경에는 보안되지 않은 Service Fabric 클러스터를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="6f020-122">클러스터 끝점은 접두사로 `http` 또는 `https`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-122">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="6f020-123">HTTP 게이트웨이에 대한 포트를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-123">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="6f020-124">포트 및 주소는 Service Fabric Explorer URL와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-124">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="6f020-125">인증서로 보호된 클러스터는 암호화되지 않은 .pem 파일 또는 .crt와 .key 파일 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="6f020-126">예:</span><span class="sxs-lookup"><span data-stu-id="6f020-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="6f020-127">자세한 내용은 [안전한 Azure Service Fabric 클러스터에 연결](service-fabric-connect-to-secure-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f020-127">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6f020-128">`select` 명령은 반환하기 전에 요청에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-128">The `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="6f020-129">클러스터를 올바르게 지정했는지 확인하려면 `az sf cluster health`와 같은 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-129">To verify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="6f020-130">명령이 오류를 반환하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-130">Verify that the command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="6f020-131">기본 작업</span><span class="sxs-lookup"><span data-stu-id="6f020-131">Basic operations</span></span>

<span data-ttu-id="6f020-132">클러스터 연결 정보는 여러 Azure CLI 세션에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="6f020-133">Service Fabric 클러스터를 선택한 후에 클러스터에서 모든 Service Fabric 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-133">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="6f020-134">예를 들어, Service Fabric 클러스터 상태를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-134">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="6f020-135">명령이 다음과 같은 출력을 발생시킵니다(Azure CLI 구성에서 JSON 출력이 지정된 것으로 간주).</span><span class="sxs-lookup"><span data-stu-id="6f020-135">The command results in the following output (assuming that JSON output is specified in the Azure CLI configuration):</span></span>

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="6f020-136">팁 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6f020-136">Tips and troubleshooting</span></span>

<span data-ttu-id="6f020-137">Azure CLI에서 Service Fabric 명령을 사용하는 동안 문제가 발생하는 경우 다음 정보가 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-137">You might find the following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="6f020-138">인증서를 PFX에서 PEM 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="6f020-138">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="6f020-139">Azure CLI는 PEM(확장명 .pem) 파일의 클라이언트 쪽 인증서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="6f020-140">Windows에서 PFX 파일을 사용하는 경우 해당 인증서를 PEM 형식으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-140">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="6f020-141">PFX 파일을 PEM 파일로 변환하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-141">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="6f020-142">자세한 내용은 [OpenSSL 설명서](https://www.openssl.org/docs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6f020-142">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="6f020-143">연결 문제</span><span class="sxs-lookup"><span data-stu-id="6f020-143">Connection issues</span></span>

<span data-ttu-id="6f020-144">일부 작업은 다음과 같은 메시지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-144">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="6f020-145">지정된 클러스터 끝점을 사용 가능하고 수신 대기하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-145">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="6f020-146">Service Fabric Explorer UI가 해당 호스트 및 포트에서 사용 가능한지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-146">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="6f020-147">끝점을 업데이트하려면 `az sf cluster select`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-147">To update the endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="6f020-148">자세한 로그</span><span class="sxs-lookup"><span data-stu-id="6f020-148">Detailed logs</span></span>

<span data-ttu-id="6f020-149">자세한 로그는 종종 문제를 디버그하거나 보고하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="6f020-150">Azure CLI는 로그 파일의 자세한 정보를 증가시키는 전역 `--debug` 플래그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-150">Azure CLI offers a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="6f020-151">명령 도움말 및 구문</span><span class="sxs-lookup"><span data-stu-id="6f020-151">Command help and syntax</span></span>

<span data-ttu-id="6f020-152">Service Fabric 명령을 Azure CLI와 동일한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-152">Service Fabric commands follow the same conventions as Azure CLI.</span></span> <span data-ttu-id="6f020-153">특정 명령 또는 명령 그룹의 도움말은 `-h` 플래그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="6f020-154">다른 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f020-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
