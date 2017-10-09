---
title: "Azure 서비스 패브릭 CLI (sfctl) aaaGet 시작"
description: "Toouse Azure 서비스 패브릭 CLI hello 하는 방법에 대해 알아봅니다. 자세한 방법을 tooconnect tooa 클러스터와 방법을 toomanage 응용 프로그램입니다."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="2c190-104">Azure Service Fabric 명령줄</span><span class="sxs-lookup"><span data-stu-id="2c190-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="2c190-105">hello Azure 서비스 패브릭 CLI (sfctl)는 상호 작용 하 고 Azure 서비스 패브릭 엔터티를 관리 하기 위한 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="2c190-106">Sfctl은 Windows 또는 Linux 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="2c190-107">Sfctl은 Python이 지원되는 모든 플랫폼에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c190-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2c190-108">Prerequisites</span></span>

<span data-ttu-id="2c190-109">이전 tooinstallation python 및 설치 하는 pip를 모두 사용자 환경에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="2c190-110">자세한 내용은 살펴보세요 hello [pip 빠른 시작 설명서](https://pip.pypa.io/en/latest/quickstart/), 공식 및 [설명서를 설치 하는 python](https://wiki.python.org/moin/BeginnersGuide/Download)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="2c190-111">두 python 2.7 및 3.6는 지원 되지만, toouse python 3.6 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="2c190-112">설치</span><span class="sxs-lookup"><span data-stu-id="2c190-112">Install</span></span>

<span data-ttu-id="2c190-113">Azure 서비스 패브릭 CLI (sfctl) hello python 패키지로 패키지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="2c190-114">실행 hello 최신 버전을 tooinstall:</span><span class="sxs-lookup"><span data-stu-id="2c190-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="2c190-115">설치 후 실행 `sfctl -h` 사용 가능한 명령에 대 한 tooget 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="2c190-116">CLI 구문</span><span class="sxs-lookup"><span data-stu-id="2c190-116">CLI syntax</span></span>

<span data-ttu-id="2c190-117">명령은 항상 `sfctl`이라는 접두사가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="2c190-118">사용할 수 있는 모든 명령에 대한 일반적인 정보는 `sfctl -h`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="2c190-119">단일 명령의 도움말은 `sfctl <command> -h`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="2c190-120">명령에 따라 hello hello 대상으로 하는 반복 구조 명령 이전 hello 동사 나 작업 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="2c190-121">이 예제에서는 `<object>` 한 hello 대상이 `<action>`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="2c190-122">클러스터 선택</span><span class="sxs-lookup"><span data-stu-id="2c190-122">Select a cluster</span></span>

<span data-ttu-id="2c190-123">작업을 수행 하기 전에를 클러스터 tooconnect를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="2c190-124">예를 들어 hello tooselect 다음을 실행 하 고 hello 이름의 toohello 클러스터에 연결 `testcluster.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="2c190-125">프로덕션 환경에는 보안되지 않은 Service Fabric 클러스터를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="2c190-126">hello 클러스터 끝점 붙어야 `http` 또는 `https`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="2c190-127">Hello 포트 hello는 HTTP 게이트웨이를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="2c190-128">hello 포트와 주소는 서비스 패브릭 탐색기 URL hello와 같을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="2c190-129">인증서로 보호된 클러스터에 PEM 인코딩 인증서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="2c190-130">단일 파일 또는 인증서 및 키 쌍으로 hello 인증서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="2c190-131">자세한 내용은 참조 [Azure 서비스 패브릭 클러스터 보안 연결 tooa](service-fabric-connect-to-secure-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="2c190-132">기본 작업</span><span class="sxs-lookup"><span data-stu-id="2c190-132">Basic operations</span></span>

<span data-ttu-id="2c190-133">클러스터 연결 정보는 여러 sfctl 세션에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="2c190-134">서비스 패브릭 클러스터를 선택한 후에 hello 클러스터에서 모든 서비스 패브릭 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="2c190-135">예를 들어 tooget hello 서비스 패브릭 클러스터 상태 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="2c190-136">hello 명령 hello 출력 뒤에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-136">hello command results in hello following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="2c190-137">팁 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2c190-137">Tips and troubleshooting</span></span>

<span data-ttu-id="2c190-138">일반적인 문제를 해결하기 위한 몇 가지 제안 및 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="2c190-139">인증서를 PFX tooPEM 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="2c190-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="2c190-140">서비스 패브릭 CLI hello PEM (.pem 확장명) 파일로 클라이언트 쪽 인증서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="2c190-141">Windows에서 PFX 파일을 사용 하는 경우 해당 인증서 tooPEM 형식을 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="2c190-142">tooconvert PFX 파일 tooa PEM 파일을 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="2c190-143">자세한 내용은 참조 hello [OpenSSL 설명서](https://www.openssl.org/docs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="2c190-144">연결 문제</span><span class="sxs-lookup"><span data-stu-id="2c190-144">Connection issues</span></span>

<span data-ttu-id="2c190-145">일부 작업 메시지의 뒤에 hello를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="2c190-146">해당 hello 지정 클러스터 끝점을 수신 하 고 사용할 수 있는 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2c190-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="2c190-147">또한, 호스트 및 포트는 해당 hello 서비스 패브릭 탐색기 UI를 사용할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="2c190-148">tooupdate hello 끝점을 사용 하 여 `sfctl cluster select`합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="2c190-149">자세한 로그</span><span class="sxs-lookup"><span data-stu-id="2c190-149">Detailed logs</span></span>

<span data-ttu-id="2c190-150">자세한 로그는 종종 문제를 디버그하거나 보고하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="2c190-151">전역는 `--debug` hello 자세한 정도 로그 파일의 증가 하는 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="2c190-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="2c190-152">명령 도움말 및 구문</span><span class="sxs-lookup"><span data-stu-id="2c190-152">Command help and syntax</span></span>

<span data-ttu-id="2c190-153">에 대 한 특정 명령 또는 명령 그룹을 도움말 hello를 사용 하 여 `-h` 플래그:</span><span class="sxs-lookup"><span data-stu-id="2c190-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="2c190-154">다른 예제:</span><span class="sxs-lookup"><span data-stu-id="2c190-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="2c190-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c190-155">Next steps</span></span>

* [<span data-ttu-id="2c190-156">Azure 서비스 패브릭 CLI hello로 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="2c190-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="2c190-157">Linux에서 Service Fabric 시작</span><span class="sxs-lookup"><span data-stu-id="2c190-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
