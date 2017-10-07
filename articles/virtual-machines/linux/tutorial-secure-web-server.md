---
title: "Azure에서 웹 서버 ssl 인증서 aaaSecure | Microsoft Docs"
description: "Azure에서 Linux VM의 toosecure hello NGINX 웹 서버 ssl 인증서 하는 방법을 알아봅니다"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="4700e-103">Azure에서 Linux 가상 컴퓨터의 SSL 인증서로 웹 서버 보호</span><span class="sxs-lookup"><span data-stu-id="4700e-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="4700e-104">toosecure 웹 서버, 나중에 SSL (Secure Sockets) 인증서 수 tooencrypt 웹 트래픽을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="4700e-105">이 SSL 인증서 Azure 키 자격 증명 모음에 저장할 수 있으며 Azure에서 인증서 tooLinux 가상 컴퓨터 (Vm)의 보안 배포를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="4700e-106">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4700e-107">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="4700e-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="4700e-108">생성 또는 인증서 toohello 주요 자격 증명 모음 업로드</span><span class="sxs-lookup"><span data-stu-id="4700e-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="4700e-109">VM을 만들고 hello NGINX 웹 서버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="4700e-110">Hello VM hello 인증서 삽입 하 고을 SSL 바인딩과 함께 NGINX 구성</span><span class="sxs-lookup"><span data-stu-id="4700e-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4700e-111">Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상.</span><span class="sxs-lookup"><span data-stu-id="4700e-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4700e-112">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4700e-113">Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="4700e-114">개요</span><span class="sxs-lookup"><span data-stu-id="4700e-114">Overview</span></span>
<span data-ttu-id="4700e-115">Azure Key Vault는 암호화 키 및 비밀 정보(인증서 또는 암호)를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="4700e-116">주요 자격 증명 모음은 hello 인증서 관리 프로세스를 간소화 하는 데 도움이 됩니다 하 고 해당 인증서에 액세스 하는 키의 toomaintain 제어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="4700e-117">Key Vault 내에 자체 서명된 인증서를 만들거나 이미 소유하고 있는 기존의 신뢰할 수 있는 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="4700e-118">내재된 인증서를 포함하는 사용자 지정 VM 이미지를 사용하는 대신 실행 중인 VM에 인증서를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="4700e-119">이 프로세스 hello 최신 인증서 배포 하는 동안 웹 서버에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="4700e-120">인증서를 바꾸거나 갱신도 없으면 toocreate 새 사용자 지정 VM 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="4700e-121">hello 최신 인증서는 추가 Vm을 만들 때 자동으로 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="4700e-122">Hello 전체 과정 hello 인증서 되지 hello Azure 플랫폼에서 나 가지 스크립트, 명령줄 기록 또는 서식 파일에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="4700e-123">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="4700e-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="4700e-124">Key Vault 및 인증서를 만들려면 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4700e-125">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupSecureWeb* hello에 *eastus* 위치:</span><span class="sxs-lookup"><span data-stu-id="4700e-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="4700e-126">다음으로 [az keyvault create](/cli/azure/keyvault#create)를 사용하여 Key Vault를 만들고 VM 배포 시에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="4700e-127">각 Key Vault에는 고유한 이름이 필요하며 모두 소문자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="4700e-128">대체 * <mykeyvault> * 다음 예에서는 고유 키 자격 증명 모음 이름으로 hello에:</span><span class="sxs-lookup"><span data-stu-id="4700e-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="4700e-129">인증서 생성 및 Key Vault에 저장</span><span class="sxs-lookup"><span data-stu-id="4700e-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="4700e-130">프로덕션 사용을 위해 [az keyvault certificate import](/cli/azure/certificate#import)를 사용하여 신뢰할 수 있는 공급자가 서명한 유효한 인증서를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="4700e-131">이 자습서에 대 한 hello 다음 예제와 자체 서명 된 인증서를 생성 하는 방법을 [az keyvault 인증서 만들기](/cli/azure/certificate#create) hello 기본 인증서 정책을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="4700e-132">VM에 사용할 인증서 준비</span><span class="sxs-lookup"><span data-stu-id="4700e-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="4700e-133">hello VM 중 toouse hello 인증서 프로세스 만들기, 사용 하 여 인증서의 hello ID를 가져오려면 [az keyvault 비밀 목록-버전](/cli/azure/keyvault/secret#list-versions)합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="4700e-134">Hello 인증서와 변환 [az vm 형식 비밀](/cli/azure/vm#format-secret)합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="4700e-135">다음 예제는 hello hello 출력 hello 사용 하 여 쉽게 이러한 명령 toovariables의 다음 단계에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="4700e-136">클라우드 init config toosecure NGINX 만들기</span><span class="sxs-lookup"><span data-stu-id="4700e-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="4700e-137">[클라우드 init](https://cloudinit.readthedocs.io) 는 널리 사용 되는 접근 방식을 toocustomize Linux VM 처음으로 hello에 대 한 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="4700e-138">클라우드 init tooinstall 패키지를 사용할 수 있으며 파일, 또는 tooconfigure 사용자 및 보안에 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="4700e-139">추가 단계 없이 없는 클라우드 init hello 초기 부팅 프로세스 중 실행 될 때 또는 에이전트 tooapply 구성에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="4700e-140">인증서는 VM을 만들 시점과 키가 보호 하는 hello에 저장 */var/lib/waagent/* 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="4700e-141">tooautomate 추가 hello 인증서 toohello VM 및 클라우드 초기화에 사용 하 여 hello 웹 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="4700e-142">이 예제에서는 설치 하 고 hello NGINX 웹 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="4700e-143">Hello를 사용할 수 있습니다 tooinstall를 처리 하 고 Apache 구성 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="4700e-144">라는 파일을 만들어 *init 웹 server.txt 클라우드* 붙여넣기 hello 구성에 따라:</span><span class="sxs-lookup"><span data-stu-id="4700e-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="4700e-145">보안 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="4700e-145">Create a secure VM</span></span>
<span data-ttu-id="4700e-146">이제 [az vm create](/cli/azure/vm#create)로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="4700e-147">hello 인증서 데이터를 키 자격 증명 모음에서 hello로 주입 `--secrets` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="4700e-148">Hello로 hello init 클라우드 구성에 전달 하면 `--custom-data` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="4700e-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="4700e-149">Hello VM toobe 생성에 대 일 분 정도 걸리며 hello 패키지 tooinstall 및 hello 앱 toostart 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="4700e-150">Hello VM을 만들면 기록해 hello `publicIpAddress` hello Azure CLI로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="4700e-151">이 주소는 사용 되는 tooaccess 웹 브라우저에서 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="4700e-152">tooallow 보안 웹 트래픽을 tooreach VM, 열린 포트 443에서 인터넷 hello와 [az vm-포트를 열](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="4700e-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="4700e-153">Hello 보안 웹 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="4700e-153">Test hello secure web app</span></span>
<span data-ttu-id="4700e-154">웹 브라우저를 열고 입력 수 이제 *https://<publicIpAddress> * hello 주소 표시줄에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="4700e-155">제공 하려면 사용자 고유의 공용 hello VM의에서 IP 주소를 만드는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="4700e-156">자체 서명 된 인증서를 사용 하는 경우 hello 보안 경고를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![웹 브라우저 보안 경고 허용](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="4700e-158">보안 된 NGINX 사이트 hello 다음 예제와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![실행 중인 보안 NGINX 사이트 보기](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="4700e-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4700e-160">Next steps</span></span>

<span data-ttu-id="4700e-161">이 자습서에서는 Azure Key Vault에 저장된 SSL 인증서를 사용하여 NGINX 웹 서버를 보호했습니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="4700e-162">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4700e-163">Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="4700e-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="4700e-164">생성 또는 인증서 toohello 주요 자격 증명 모음 업로드</span><span class="sxs-lookup"><span data-stu-id="4700e-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="4700e-165">VM을 만들고 hello NGINX 웹 서버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="4700e-166">Hello VM hello 인증서 삽입 하 고을 SSL 바인딩과 함께 NGINX 구성</span><span class="sxs-lookup"><span data-stu-id="4700e-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="4700e-167">가상 컴퓨터 스크립트 샘플을 미리 만들어진이 링크 toosee를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4700e-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4700e-168">Windows 가상 컴퓨터 스크립트 샘플 </span><span class="sxs-lookup"><span data-stu-id="4700e-168">Windows virtual machine script samples</span></span>](./cli-samples.md)