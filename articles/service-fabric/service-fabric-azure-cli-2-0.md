---
title: "Azure 서비스 패브릭 및 Azure CLI 2.0 aaaGet 시작"
description: "Azure 서비스 패브릭 toouse hello Azure CLI 버전 2.0에서에서 모듈 명령이 하는 방식에 대해 알아봅니다. 자세한 방법을 tooconnect tooa 클러스터와 방법을 toomanage 응용 프로그램입니다."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="e9fda-104">Azure Service Fabric 및 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e9fda-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="e9fda-105">hello Azure 명령줄 도구 (Azure CLI) 버전 2.0에는 Azure 서비스 패브릭 클러스터를 관리 하는 명령을 toohelp 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="e9fda-106">Azure CLI 및 서비스 패브릭와 tooget 시작 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="e9fda-107">Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="e9fda-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="e9fda-108">와 Azure CLI 2.0 명령을 toointeract를 사용할 수 있으며 서비스 패브릭 클러스터를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="e9fda-109">tooget hello 최신 버전의 Azure CLI에 따라 hello [Azure CLI 2.0 표준 설치 프로세스](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="e9fda-110">자세한 내용은 참조 hello [Azure CLI 2.0 개요](https://docs.microsoft.com/en-us/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="e9fda-111">Azure CLI 구문</span><span class="sxs-lookup"><span data-stu-id="e9fda-111">Azure CLI syntax</span></span>

<span data-ttu-id="e9fda-112">Azure CLI에서 모든 Service Fabric 명령은 접두사로 `az sf`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="e9fda-113">사용 가능한 hello 명령에 대 한 일반적인 정보를 사용 하 여 `az sf -h`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="e9fda-114">단일 명령의 도움말은 `az sf <command> -h`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="e9fda-115">Azure CLI의 Service Fabric 명령은 다음과 같은 명명 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="e9fda-116">`<object>`에 대 한 hello 대상인 `<action>`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="e9fda-117">클러스터 선택</span><span class="sxs-lookup"><span data-stu-id="e9fda-117">Select a cluster</span></span>

<span data-ttu-id="e9fda-118">작업을 수행 하기 전에를 클러스터 tooconnect를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="e9fda-119">예를 들어 hello 코드 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e9fda-119">For an example, see hello following code.</span></span> <span data-ttu-id="e9fda-120">hello 코드 tooan 보안 되지 않은 클러스터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="e9fda-121">프로덕션 환경에는 보안되지 않은 Service Fabric 클러스터를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="e9fda-122">hello 클러스터 끝점 붙어야 `http` 또는 `https`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="e9fda-123">Hello 포트 hello는 HTTP 게이트웨이를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="e9fda-124">hello 포트와 주소는 서비스 패브릭 탐색기 URL hello와 같을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="e9fda-125">인증서로 보호된 클러스터는 암호화되지 않은 .pem 파일 또는 .crt와 .key 파일 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="e9fda-126">예:</span><span class="sxs-lookup"><span data-stu-id="e9fda-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="e9fda-127">자세한 내용은 참조 [Azure 서비스 패브릭 클러스터 보안 연결 tooa](service-fabric-connect-to-secure-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e9fda-128">hello `select` 명령 반환 하기 전에 모든 요청에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="e9fda-129">클러스터를 올바르게 지정 tooverify 같은 명령을 사용 하 여 `az sf cluster health`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="e9fda-130">Hello 명령 오류를 반환 하지 않습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="e9fda-131">기본 작업</span><span class="sxs-lookup"><span data-stu-id="e9fda-131">Basic operations</span></span>

<span data-ttu-id="e9fda-132">클러스터 연결 정보는 여러 Azure CLI 세션에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="e9fda-133">서비스 패브릭 클러스터를 선택한 후에 hello 클러스터에서 모든 서비스 패브릭 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="e9fda-134">예를 들어 tooget hello 서비스 패브릭 클러스터 상태 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="e9fda-135">hello 명령 결과 hello 다음 (있다고 가정할 경우 JSON 출력 hello Azure CLI 구성에 지정 된) 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="e9fda-136">팁 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e9fda-136">Tips and troubleshooting</span></span>

<span data-ttu-id="e9fda-137">Hello Azure CLI에서 서비스 패브릭 명령을 사용 하는 동안 문제가 발생 하는 경우 다음 유용한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="e9fda-138">인증서를 PFX tooPEM 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="e9fda-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="e9fda-139">Azure CLI는 PEM(확장명 .pem) 파일의 클라이언트 쪽 인증서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="e9fda-140">Windows에서 PFX 파일을 사용 하는 경우 해당 인증서 tooPEM 형식을 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="e9fda-141">PFX 파일 tooa PEM 파일을 tooconvert hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="e9fda-142">자세한 내용은 참조 hello [OpenSSL 설명서](https://www.openssl.org/docs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="e9fda-143">연결 문제</span><span class="sxs-lookup"><span data-stu-id="e9fda-143">Connection issues</span></span>

<span data-ttu-id="e9fda-144">일부 작업 메시지의 뒤에 hello를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="e9fda-145">해당 hello 지정 클러스터 끝점을 수신 하 고 사용할 수 있는 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e9fda-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="e9fda-146">또한, 호스트 및 포트는 해당 hello 서비스 패브릭 탐색기 UI를 사용할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="e9fda-147">tooupdate hello 끝점을 사용 하 여 `az sf cluster select`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="e9fda-148">자세한 로그</span><span class="sxs-lookup"><span data-stu-id="e9fda-148">Detailed logs</span></span>

<span data-ttu-id="e9fda-149">자세한 로그는 종종 문제를 디버그하거나 보고하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="e9fda-150">Azure CLI 제공 전역 `--debug` hello 자세한 정도 로그 파일의 증가 하는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="e9fda-151">명령 도움말 및 구문</span><span class="sxs-lookup"><span data-stu-id="e9fda-151">Command help and syntax</span></span>

<span data-ttu-id="e9fda-152">서비스 패브릭 명령을 수행 hello Azure CLI와 동일한 규칙을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="e9fda-153">에 대 한 특정 명령 또는 명령 그룹을 도움말 hello를 사용 하 여 `-h` 플래그:</span><span class="sxs-lookup"><span data-stu-id="e9fda-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="e9fda-154">다른 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e9fda-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
