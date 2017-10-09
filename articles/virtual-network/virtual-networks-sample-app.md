---
title: "Dmz와 함께 사용할 aaaAzure 샘플 응용 프로그램 | Microsoft Docs"
description: "DMZ tootest 트래픽 흐름 시나리오를 만든 후이 간단한 웹 응용 프로그램 배포"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="6351f-103">DMZ에 사용할 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="6351f-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="6351f-104">[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]</span><span class="sxs-lookup"><span data-stu-id="6351f-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="6351f-105">이 PowerShell 스크립트를 hello IIS01 및 AppVM01 서버 tooinstall에서 로컬로 실행 하 고 백 엔드 AppVM01 서버 hello의에서 내용으로 hello 프런트 엔드 IIS01 서버에서 html 페이지를 표시 하는 간단한 웹 응용 프로그램을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-105">These PowerShell scripts can be run locally on hello IIS01 and AppVM01 servers tooinstall and set up a simple web application that displays an html page from hello front-end IIS01 server with content from hello back-end AppVM01 server.</span></span>

<span data-ttu-id="6351f-106">이 응용 프로그램 많은 hello DMZ 예제 및 UDR, 끝점, Nsg에 변경 내용을 hello 하는 방법에 대 한 단순한 테스트 환경 하며 방화벽 규칙 트래픽 흐름에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-106">This application provides a simple testing environment for many of hello DMZ Examples and how changes on hello Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-tooallow-icmp"></a><span data-ttu-id="6351f-107">방화벽 규칙 tooallow ICMP</span><span class="sxs-lookup"><span data-stu-id="6351f-107">Firewall rule tooallow ICMP</span></span>
<span data-ttu-id="6351f-108">모든 Windows VM tooallow ICMP (Ping) 트래픽을이 간단한 PowerShell 문을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-108">This simple PowerShell statement can be run on any Windows VM tooallow ICMP (Ping) traffic.</span></span> <span data-ttu-id="6351f-109">보다 쉽게 테스트 하 고 (기본적으로 켜져 ICMP 대부분 Linux 배포판)에 대 한 hello windows 방화벽을 통해 hello ping 프로토콜 toopass 허용 하 여 문제 해결이 방화벽 업데이트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-109">This firewall update allows for easier testing and troubleshooting by allowing hello ping protocol toopass through hello windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="6351f-110">다음 스크립트는 hello를 사용 하는 경우이 방화벽 규칙 추가 hello 첫 번째 문입니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-110">If you use hello following scripts, this firewall rule addition is hello first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="6351f-111">IIS01 - 웹 응용 프로그램 설치 스크립트</span><span class="sxs-lookup"><span data-stu-id="6351f-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="6351f-112">이 스크립트는 다음과 같은 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-112">This script will:</span></span>

1. <span data-ttu-id="6351f-113">IMCPv4 열고 쉽게 테스트용 hello 로컬 서버의 windows 방화벽 (Ping)</span><span class="sxs-lookup"><span data-stu-id="6351f-113">Open IMCPv4 (Ping) on hello local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="6351f-114">IIS를 설치 하 고 hello.Net Framework v4.5</span><span class="sxs-lookup"><span data-stu-id="6351f-114">Install IIS and hello .Net Framework v4.5</span></span>
3. <span data-ttu-id="6351f-115">ASP.NET 웹 페이지와 Web.config 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="6351f-116">Hello 기본 응용 프로그램 풀 toomake 파일 액세스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-116">Change hello Default application pool toomake file access easier</span></span>
5. <span data-ttu-id="6351f-117">Hello 익명 사용자 tooyour 관리자 계정 및 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-117">Set hello Anonymous user tooyour admin account and password</span></span>

<span data-ttu-id="6351f-118">이 PowerShell 스크립트는 IIS01에 RDP 처리된 동안 로컬로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="6351f-119">AppVM01 - 파일 서버 설치 스크립트</span><span class="sxs-lookup"><span data-stu-id="6351f-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="6351f-120">이 스크립트는이 간단한 응용 프로그램에 대 한 hello 백 엔드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-120">This script sets up hello back-end for this simple application.</span></span> <span data-ttu-id="6351f-121">이 스크립트는 다음과 같은 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-121">This script will:</span></span>

1. <span data-ttu-id="6351f-122">IMCPv4 열고 hello 방화벽 쉽게 테스트 하는 것에 대 한 (Ping)</span><span class="sxs-lookup"><span data-stu-id="6351f-122">Open IMCPv4 (Ping) on hello firewall for easier testing</span></span>
2. <span data-ttu-id="6351f-123">Hello 웹 사이트에 대 한 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="6351f-123">Create a directory for hello web site</span></span>
3. <span data-ttu-id="6351f-124">텍스트 파일 toobe를 원격으로 생성할 hello 웹 페이지에 액세스</span><span class="sxs-lookup"><span data-stu-id="6351f-124">Create a text file toobe remotely access by hello web page</span></span>
4. <span data-ttu-id="6351f-125">Hello 디렉터리 및 파일 tooAnonymous tooallow 액세스 사용 권한을 설정합니다</span><span class="sxs-lookup"><span data-stu-id="6351f-125">Set permissions on hello directory and file tooAnonymous tooallow access</span></span>
5. <span data-ttu-id="6351f-126">IE 보안 강화 tooallow 쉽게이 서버에서 검색 해제</span><span class="sxs-lookup"><span data-stu-id="6351f-126">Turn off IE Enhanced Security tooallow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6351f-127">**모범 사례**:는 일반적으로 프로덕션 서버에서 바람직하지 toosurf hello 웹 및 하지 프로덕션 서버에서 IE 보안 강화를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea toosurf hello web from a production server.</span></span> <span data-ttu-id="6351f-128">또한 익명 액세스를 위해 파일 공유를 여는 것도 바람직하지 않지만 여기서는 간단한 설명을 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="6351f-129">이 PowerShell 스크립트는 AppVM01에 RDP 처리된 동안 로컬로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="6351f-130">PowerShell은 필요한 toobe 관리자 tooensure 성공적으로 실행으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-130">PowerShell is required toobe run as Administrator tooensure successful execution.</span></span>

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="6351f-131">DNS01 - DNS 서버 설치 스크립트</span><span class="sxs-lookup"><span data-stu-id="6351f-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="6351f-132">이 샘플 응용 프로그램 tooset hello DNS 서버를에 포함 된 스크립트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-132">There is no script included in this sample application tooset up hello DNS server.</span></span> <span data-ttu-id="6351f-133">Hello DNS01 서버 toobe 있어야 hello 방화벽 규칙, NSG, 또는 UDR 테스트 tooinclude DNS 트래픽이 필요한 경우 수동으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-133">If testing of hello firewall rules, NSG, or UDR needs tooinclude DNS traffic, hello DNS01 server needs toobe set up manually.</span></span> <span data-ttu-id="6351f-134">hello 네트워크 구성 xml 파일을 두 예제 모두에 대 한 리소스 관리자 템플릿을 DNS01 hello DNS 서버를 백업 하는 hello와 수준 3에 의해 호스팅되는 공용 DNS 서버 및 주 DNS 서버 hello로 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-134">hello Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as hello primary DNS server and hello public DNS server hosted by Level 3 as hello backup DNS server.</span></span> <span data-ttu-id="6351f-135">hello 수준 3 DNS 서버 hello 로컬이 아닌 트래픽에 사용 되는 실제 DNS 서버 라인과 DNS01으로 설정 하지, DNS 발생 하는 로컬 네트워크에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-135">hello Level 3 DNS server would be hello actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6351f-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6351f-136">Next steps</span></span>
* <span data-ttu-id="6351f-137">IIS 서버의 hello IIS01 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6351f-137">Run hello IIS01 script on an IIS server</span></span>
* <span data-ttu-id="6351f-138">AppVM01에서 파일 서버 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="6351f-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="6351f-139">빌드 IIS01 toovalidate에 공용 IP toohello 찾아보기</span><span class="sxs-lookup"><span data-stu-id="6351f-139">Browse toohello Public IP on IIS01 toovalidate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
