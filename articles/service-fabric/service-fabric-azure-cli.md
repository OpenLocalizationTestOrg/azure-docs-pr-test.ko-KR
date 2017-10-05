---
title: "Azure Service Fabric XPlat CLI 시작"
description: "Azure Service Fabric XPlat CLI 시작"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="37c18-103">XPlat CLI를 사용하여 Service Fabric 클러스터와 상호 작용</span><span class="sxs-lookup"><span data-stu-id="37c18-103">Using the XPlat CLI to interact with a Service Fabric cluster</span></span>

<span data-ttu-id="37c18-104">Linux에서 XPlat CLI를 사용하여 Linux 컴퓨터의 Service Fabric 클러스터와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-104">You can interact with Service Fabric cluster from Linux machines using the XPlat CLI on Linux.</span></span>

<span data-ttu-id="37c18-105">첫 번째 단계는 git 리포지토리에서 최신 버전의 CLI를 가져오고 다음 명령을 사용하여 경로에서 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="37c18-106">지원하는 각 명령에 대해 도움말을 보려면 명령의 이름을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span>
<span data-ttu-id="37c18-107">명령에 대해서는 자동 완성이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="37c18-108">예를 들어 다음 명령은 모든 응용 프로그램 명령에 대한 도움말을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="37c18-109">다음 예와 같이 특정 명령으로 추가 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="37c18-110">CLI에서 자동 완성을 사용하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="37c18-111">다음 명령은 클러스터에 연결하고 클러스터에 있는 노드를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="37c18-112">명명된 매개 변수를 사용하고 매개 변수가 어떤 기능이 있는지 알아보려면 명령 뒤에 --help를 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="37c18-113">예:</span><span class="sxs-lookup"><span data-stu-id="37c18-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="37c18-114">**클러스터에 포함되지 않은**컴퓨터에서 여러 컴퓨터 클러스터에 연결하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="37c18-115">PublicIPorFQDN 태그를 실제 IP 또는 FQDN으로 적절하게 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="37c18-116">**클러스터에 포함된**컴퓨터에서 여러 컴퓨터 클러스터에 연결하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="37c18-117">PowerShell 또는 CLI를 사용하여 Azure 포털을 통해 만든 Linux Service Fabric 클러스터와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="37c18-118">이러한 클러스터는 안전하지 않으므로 클러스터 매니페스트에서 공용 IP 주소를 추가하여 one-box를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="37c18-119">XPlat CLI를 사용하여 Service Fabric 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="37c18-119">Using the XPlat CLI to connect to a Service Fabric cluster</span></span>

<span data-ttu-id="37c18-120">다음 Azure CLI 명령은 보안 클러스터에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="37c18-121">인증서 세부 정보는 클러스터 노드의 인증서와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="37c18-122">인증서에 인증 기관(CA)이 있는 경우 다음 예와 같이 --ca-cert-path 매개 변수를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="37c18-123">여러 CA가 있는 경우 구분 기호로 쉼표를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="37c18-124">인증서에 있는 일반 이름이 연결 끝점과 일치하지 않는 경우 다음 명령에 표시된 것처럼 `--strict-ssl-false` 매개 변수를 사용하여 확인을 바이패스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="37c18-125">CA 확인을 건너뛰려면 다음 명령에 표시된 것처럼 --reject-unauthorized-false 매개 변수를 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="37c18-126">연결 후에는 클러스터와 상호 작용하기 위해 다른 CLI 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="37c18-127">서비스 패브릭 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="37c18-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="37c18-128">다음 명령을 실행하여 서비스 패브릭 응용 프로그램을 복사, 등록 및 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="37c18-129">응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="37c18-129">Upgrading your application</span></span>

<span data-ttu-id="37c18-130">이 과정은 [Windows의 과정](service-fabric-application-upgrade-tutorial-powershell.md)과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="37c18-131">프로젝트 루트 디렉터리에서 응용 프로그램을 빌드, 복사, 등록 및 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="37c18-132">응용 프로그램 인스턴스가 `fabric:/MySFApp`으로 명명된 경우 형식은 MySFApp이고 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-132">If your application instance is named `fabric:/MySFApp`, and the type is MySFApp, the commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="37c18-133">응용 프로그램을 변경하고 수정된 서비스를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="37c18-134">수정된 서비스의 매니페스트 파일(ServiceManifest.xml)을 업데이트된 버전의 서비스(및 필요에 따라 코드, 구성 또는 데이터)로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="37c18-135">또한 응용 프로그램의 매니페스트(ApplicationManifest.xml)를 응용 프로그램에 대한 업데이트된 버전 번호와 수정된 서비스로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="37c18-136">이제 다음 명령을 사용하여 업데이트된 응용 프로그램을 복사 및 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-136">Now, copy and register your updated application using the following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="37c18-137">이제, 다음 명령을 사용하여 응용 프로그램 업그레이드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-137">Now, you can start the application upgrade with the following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="37c18-138">SFX를 사용하여 응용 프로그램 업그레이드를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="37c18-139">몇 분 후 응용 프로그램이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-139">In a few minutes, the application would have been updated.</span></span> <span data-ttu-id="37c18-140">업데이트된 앱에서 오류를 시도해보고 서비스 패브릭의 자동 롤백 기능을 확인해볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="37c18-141">PEM에서 PFX로 또는 그 반대로 변환</span><span class="sxs-lookup"><span data-stu-id="37c18-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="37c18-142">다른 환경에 있을 수 있는 보안 클러스터에 액세스하여 로컬 컴퓨터(Windows 또는 Linux)에 인증서를 설치해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="37c18-143">예를 들어 Windows 컴퓨터에서 보안된 Linux 클러스터를 액세스하거나 그 반대로 액세스하는 동안, 인증서를 PFX에서 PEM으로 또는 그 반대로 변환해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="37c18-144">PEM 파일에서 PFX 파일로 변환하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="37c18-145">PFX 파일에서 PEM 파일로 변환하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="37c18-146">자세한 내용은 [OpenSSL 설명서](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37c18-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="37c18-147">문제 해결</span><span class="sxs-lookup"><span data-stu-id="37c18-147">Troubleshooting</span></span>


### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="37c18-148">응용 프로그램 패키지 복사 실패</span><span class="sxs-lookup"><span data-stu-id="37c18-148">Copying of the application package does not succeed</span></span>

<span data-ttu-id="37c18-149">`openssh` 가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="37c18-150">기본적으로 Ubuntu Desktop에는 설치되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="37c18-151">다음 명령을 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-151">Install it using the following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="37c18-152">문제가 지속되면 다음 명령으로 `sshd_config` 파일을 변경하여 ssh에 대해 PAM을 사용하지 않도록 해보세요.</span><span class="sxs-lookup"><span data-stu-id="37c18-152">If the problem persists, try disabling PAM for ssh by changing the `sshd_config` file using the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="37c18-153">그래도 문제가 지속되면 다음 명령을 실행하여 ssh 세션 수를 늘려 보세요.</span><span class="sxs-lookup"><span data-stu-id="37c18-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="37c18-154">ssh 인증을 위한 키 사용(암호 아님)이 아직 지원되지 않으므로(플랫폼에서는 패키지를 복사하는 데 ssh를 사용하므로) 대신 암호 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37c18-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="37c18-155">Next steps</span></span>

[<span data-ttu-id="37c18-156">개발 환경을 설정하고 Service Fabric 응용 프로그램을 Linux 클러스터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="37c18-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="37c18-157">관련 문서</span><span class="sxs-lookup"><span data-stu-id="37c18-157">Related articles</span></span>

* [<span data-ttu-id="37c18-158">Service Fabric 및 Azure CLI 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="37c18-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
