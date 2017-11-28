---
title: "Azure Service Fabric CLI(sfctl) 시작"
description: "Azure Service Fabric CLI를 사용하는 방법에 대해 알아봅니다. 클러스터에 연결하는 방법 및 응용 프로그램 암호를 관리하는 방법을 알아봅니다."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: 5ce9adf6c82e3a5521883c5de1e0689d5bf0d94e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="08af4-104">Azure Service Fabric 명령줄</span><span class="sxs-lookup"><span data-stu-id="08af4-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="08af4-105">Azure Service Fabric CLI(sfctl)는 Azure Service Fabric 엔터티와 상호 작용하고 관리하기 위한 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-105">The Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="08af4-106">Sfctl은 Windows 또는 Linux 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="08af4-107">Sfctl은 Python이 지원되는 모든 플랫폼에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08af4-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="08af4-108">Prerequisites</span></span>

<span data-ttu-id="08af4-109">설치 이전에 사용자 환경이 Python 및 PIP를 모두 설치했는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-109">Prior to installation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="08af4-110">자세한 내용은 [PIP 빠른 시작 설명서](https://pip.pypa.io/en/latest/quickstart/) 및 공식 [Python 설치 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="08af4-110">For more information, take a look at the [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="08af4-111">Python 2.7 및 3.6이 모두 지원되지만 Python 3.6을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-111">While both python 2.7 and 3.6 are supported, it is recommended to use python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="08af4-112">설치</span><span class="sxs-lookup"><span data-stu-id="08af4-112">Install</span></span>

<span data-ttu-id="08af4-113">Azure Service Fabric CLI(sfctl)가 Python 패키지로 패키징됩니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-113">The Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="08af4-114">최신 버전을 설치하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-114">To install the latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="08af4-115">설치 후에 `sfctl -h`를 실행하여 사용 가능한 명령에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-115">After installation, run `sfctl -h` to get information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="08af4-116">CLI 구문</span><span class="sxs-lookup"><span data-stu-id="08af4-116">CLI syntax</span></span>

<span data-ttu-id="08af4-117">명령은 항상 `sfctl`이라는 접두사가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="08af4-118">사용할 수 있는 모든 명령에 대한 일반적인 정보는 `sfctl -h`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="08af4-119">단일 명령의 도움말은 `sfctl <command> -h`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="08af4-120">명령은 동사 또는 동작 앞에 오는 명령의 대상을 포함한 반복 구조를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-120">Commands follow a repeatable structure, with the target of the command preceding the verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="08af4-121">이 예제에서는 `<object>`는 `<action>`의 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-121">In this example, `<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="08af4-122">클러스터 선택</span><span class="sxs-lookup"><span data-stu-id="08af4-122">Select a cluster</span></span>

<span data-ttu-id="08af4-123">모든 작업을 수행하기 전에 연결할 클러스터를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-123">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="08af4-124">예를 들어, 다음을 실행하여 `testcluster.com`이라는 클러스터를 선택하고 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-124">For example, run the following to select and connect to the cluster with the name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="08af4-125">프로덕션 환경에는 보안되지 않은 Service Fabric 클러스터를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="08af4-126">클러스터 끝점은 접두사로 `http` 또는 `https`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-126">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="08af4-127">HTTP 게이트웨이에 대한 포트를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-127">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="08af4-128">포트 및 주소는 Service Fabric Explorer URL와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-128">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="08af4-129">인증서로 보호된 클러스터에 PEM 인코딩 인증서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="08af4-130">단일 파일이나 인증서 및 키 쌍으로 인증서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-130">The certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="08af4-131">자세한 내용은 [안전한 Azure Service Fabric 클러스터에 연결](service-fabric-connect-to-secure-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08af4-131">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="08af4-132">기본 작업</span><span class="sxs-lookup"><span data-stu-id="08af4-132">Basic operations</span></span>

<span data-ttu-id="08af4-133">클러스터 연결 정보는 여러 sfctl 세션에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="08af4-134">Service Fabric 클러스터를 선택한 후에 클러스터에서 모든 Service Fabric 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-134">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="08af4-135">예를 들어, Service Fabric 클러스터 상태를 가져오려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-135">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="08af4-136">이 명령은 다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-136">The command results in the following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="08af4-137">팁 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="08af4-137">Tips and troubleshooting</span></span>

<span data-ttu-id="08af4-138">일반적인 문제를 해결하기 위한 몇 가지 제안 및 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="08af4-139">인증서를 PFX에서 PEM 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="08af4-139">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="08af4-140">Service Fabric CLI는 PEM(확장명 .pem) 파일의 클라이언트 쪽 인증서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-140">The Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="08af4-141">Windows에서 PFX 파일을 사용하는 경우 해당 인증서를 PEM 형식으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-141">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="08af4-142">PFX 파일을 PEM 파일로 변환하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-142">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="08af4-143">자세한 내용은 [OpenSSL 설명서](https://www.openssl.org/docs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08af4-143">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="08af4-144">연결 문제</span><span class="sxs-lookup"><span data-stu-id="08af4-144">Connection issues</span></span>

<span data-ttu-id="08af4-145">일부 작업은 다음과 같은 메시지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-145">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="08af4-146">지정된 클러스터 끝점을 사용 가능하고 수신 대기하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-146">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="08af4-147">Service Fabric Explorer UI가 해당 호스트 및 포트에서 사용 가능한지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-147">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="08af4-148">끝점을 업데이트하려면 `sfctl cluster select`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-148">To update the endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="08af4-149">자세한 로그</span><span class="sxs-lookup"><span data-stu-id="08af4-149">Detailed logs</span></span>

<span data-ttu-id="08af4-150">자세한 로그는 종종 문제를 디버그하거나 보고하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="08af4-151">로그 파일의 자세한 정보를 증가시키는 전역 `--debug` 플래그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-151">There is a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="08af4-152">명령 도움말 및 구문</span><span class="sxs-lookup"><span data-stu-id="08af4-152">Command help and syntax</span></span>

<span data-ttu-id="08af4-153">특정 명령 또는 명령 그룹의 도움말은 `-h` 플래그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08af4-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="08af4-154">다른 예제:</span><span class="sxs-lookup"><span data-stu-id="08af4-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="08af4-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08af4-155">Next steps</span></span>

* [<span data-ttu-id="08af4-156">Azure Service Fabric CLI에서 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="08af4-156">Deploy an application with the Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="08af4-157">Linux에서 Service Fabric 시작</span><span class="sxs-lookup"><span data-stu-id="08af4-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
