## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="83ddf-101">Raspberry Pi 준비</span><span class="sxs-lookup"><span data-stu-id="83ddf-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="83ddf-102">Raspbian 설치</span><span class="sxs-lookup"><span data-stu-id="83ddf-102">Install Raspbian</span></span>

<span data-ttu-id="83ddf-103">처음으로 Raspberry Pi를 사용하는 경우 키트에 포함된 SD 카드에서 NOOBS를 사용하여 Raspbian 운영 체제를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="83ddf-104">[Raspberry Pi 소프트웨어 가이드][lnk-install-raspbian]는 Raspberry Pi에 운영 체제를 설치하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="83ddf-105">이 자습서에서는 Raspberry Pi에 Raspbian 운영 체제를 설치했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="83ddf-106">[Raspberry Pi 3용 Microsoft Azure IoT 시작 키트][lnk-starter-kits]에 포함된 SD 카드에는 이미 NOOBS가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="83ddf-107">이 카드에서 Raspberry Pi를 부팅할 수 있으며 Raspbian OS를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

### <a name="set-up-the-hardware"></a><span data-ttu-id="83ddf-108">하드웨어 설정</span><span class="sxs-lookup"><span data-stu-id="83ddf-108">Set up the hardware</span></span>

<span data-ttu-id="83ddf-109">이 자습서에서는 [Raspberry Pi 3용 Microsoft Azure IoT 시작 키트][lnk-starter-kits]에 포함된 BME280 센서를 사용하여 원격 분석 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-109">This tutorial uses the BME280 sensor included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] to generate telemetry data.</span></span> <span data-ttu-id="83ddf-110">Raspberry Pi 솔루션 대시보드에서 메서드 호출을 처리하는 경우를 나타내는 데 LED를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-110">It uses an LED to indicate when the Raspberry Pi processes a method invocation from the solution dashboard.</span></span>

<span data-ttu-id="83ddf-111">브레드보드의 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-111">The components on the bread board are:</span></span>

- <span data-ttu-id="83ddf-112">빨강 LED</span><span class="sxs-lookup"><span data-stu-id="83ddf-112">Red LED</span></span>
- <span data-ttu-id="83ddf-113">220옴 저항기(빨강, 빨강, 밤색)</span><span class="sxs-lookup"><span data-stu-id="83ddf-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="83ddf-114">BME280 센서</span><span class="sxs-lookup"><span data-stu-id="83ddf-114">BME280 sensor</span></span>

<span data-ttu-id="83ddf-115">다음 다이어그램에서는 하드웨어를 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-115">The following diagram shows how to connect your hardware:</span></span>

![Raspberry Pi의 하드웨어 설정][img-connection-diagram]

<span data-ttu-id="83ddf-117">다음 표에서는 Raspberry Pi에서 브레드보드의 구성 요소로의 연결을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-117">The following table summarizes the connections from the Raspberry Pi to the components on the breadboard:</span></span>

| <span data-ttu-id="83ddf-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="83ddf-118">Raspberry Pi</span></span>            | <span data-ttu-id="83ddf-119">브레드보드</span><span class="sxs-lookup"><span data-stu-id="83ddf-119">Breadboard</span></span>             |<span data-ttu-id="83ddf-120">색</span><span class="sxs-lookup"><span data-stu-id="83ddf-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="83ddf-121">GND(14 핀)</span><span class="sxs-lookup"><span data-stu-id="83ddf-121">GND (Pin 14)</span></span>            | <span data-ttu-id="83ddf-122">LED -ve 핀(18A)</span><span class="sxs-lookup"><span data-stu-id="83ddf-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="83ddf-123">자주색</span><span class="sxs-lookup"><span data-stu-id="83ddf-123">Purple</span></span>          |
| <span data-ttu-id="83ddf-124">GPCLK0(7 핀)</span><span class="sxs-lookup"><span data-stu-id="83ddf-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="83ddf-125">저항기(25A)</span><span class="sxs-lookup"><span data-stu-id="83ddf-125">Resistor (25A)</span></span>         | <span data-ttu-id="83ddf-126">주황색</span><span class="sxs-lookup"><span data-stu-id="83ddf-126">Orange</span></span>          |
| <span data-ttu-id="83ddf-127">SPI_CE0(24 핀)</span><span class="sxs-lookup"><span data-stu-id="83ddf-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="83ddf-128">CS(39A)</span><span class="sxs-lookup"><span data-stu-id="83ddf-128">CS (39A)</span></span>               | <span data-ttu-id="83ddf-129">파랑</span><span class="sxs-lookup"><span data-stu-id="83ddf-129">Blue</span></span>          |
| <span data-ttu-id="83ddf-130">SPI_SCLK(23 핀)</span><span class="sxs-lookup"><span data-stu-id="83ddf-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="83ddf-131">SCK(36A)</span><span class="sxs-lookup"><span data-stu-id="83ddf-131">SCK (36A)</span></span>              | <span data-ttu-id="83ddf-132">노랑</span><span class="sxs-lookup"><span data-stu-id="83ddf-132">Yellow</span></span>        |
| <span data-ttu-id="83ddf-133">SPI_MISO(21 핀)</span><span class="sxs-lookup"><span data-stu-id="83ddf-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="83ddf-134">SDO(37A)</span><span class="sxs-lookup"><span data-stu-id="83ddf-134">SDO (37A)</span></span>              | <span data-ttu-id="83ddf-135">흰색</span><span class="sxs-lookup"><span data-stu-id="83ddf-135">White</span></span>         |
| <span data-ttu-id="83ddf-136">SPI_MOSI(19 핀)</span><span class="sxs-lookup"><span data-stu-id="83ddf-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="83ddf-137">SDI(38A)</span><span class="sxs-lookup"><span data-stu-id="83ddf-137">SDI (38A)</span></span>              | <span data-ttu-id="83ddf-138">녹색</span><span class="sxs-lookup"><span data-stu-id="83ddf-138">Green</span></span>         |
| <span data-ttu-id="83ddf-139">GND(6 핀)</span><span class="sxs-lookup"><span data-stu-id="83ddf-139">GND (Pin 6)</span></span>             | <span data-ttu-id="83ddf-140">GND(35A)</span><span class="sxs-lookup"><span data-stu-id="83ddf-140">GND (35A)</span></span>              | <span data-ttu-id="83ddf-141">검정</span><span class="sxs-lookup"><span data-stu-id="83ddf-141">Black</span></span>         |
| <span data-ttu-id="83ddf-142">3.3V(1 핀)</span><span class="sxs-lookup"><span data-stu-id="83ddf-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="83ddf-143">3Vo(34A)</span><span class="sxs-lookup"><span data-stu-id="83ddf-143">3Vo (34A)</span></span>              | <span data-ttu-id="83ddf-144">빨강</span><span class="sxs-lookup"><span data-stu-id="83ddf-144">Red</span></span>           |

<span data-ttu-id="83ddf-145">하드웨어 설정을 완료하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-145">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="83ddf-146">Raspberry Pi를 키트에 포함된 전원 공급 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-146">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="83ddf-147">키트에 포함된 이더넷 케이블을 사용하여 Raspberry Pi를 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-147">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="83ddf-148">또는 Raspberry Pi에 대해 [무선 연결][lnk-pi-wireless]을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="83ddf-149">이제 Raspberry Pi의 하드웨어 설정을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-149">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="83ddf-150">터미널 로그인 및 액세스</span><span class="sxs-lookup"><span data-stu-id="83ddf-150">Sign in and access the terminal</span></span>

<span data-ttu-id="83ddf-151">Raspberry Pi의 터미널 환경에 액세스하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-151">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="83ddf-152">키보드 및 모니터가 Raspberry Pi에 연결된 경우 Raspbian GUI를 사용하여 터미널 창에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-152">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="83ddf-153">데스크톱 컴퓨터에서 SSH를 사용하여 Raspberry Pi의 명령줄에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-153">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="83ddf-154">GUI에서 터미널 창 사용</span><span class="sxs-lookup"><span data-stu-id="83ddf-154">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="83ddf-155">Raspbian에 대한 기본 자격 증명은 사용자 이름 **pi** 및 암호 **raspberry**입니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-155">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="83ddf-156">GUI의 작업 표시줄에서 모니터 모양의 아이콘을 사용하여 **터미널** 유틸리티를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-156">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="83ddf-157">SSH를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="83ddf-157">Sign in with SSH</span></span>

<span data-ttu-id="83ddf-158">Raspberry Pi에 명령줄 액세스를 위해 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-158">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="83ddf-159">[SSH(Secure Shell)][lnk-pi-ssh] 문서에서는 Raspberry Pi에서 SSH를 구성하는 방법 및 [Windows][lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]에서 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-159">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="83ddf-160">사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="83ddf-161">선택 사항: Raspberry Pi의 폴더 공유</span><span class="sxs-lookup"><span data-stu-id="83ddf-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="83ddf-162">필요에 따라 다음 데스크톱 환경을 사용하여 Raspberry Pi의 폴더를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-162">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="83ddf-163">폴더를 공유하면 `nano` 또는 `vi`을 사용하는 대신 원하는 데스크톱 텍스트 편집기(예: [Visual Studio Code](https://code.visualstudio.com/) 또는 [Sublime Text](http://www.sublimetext.com/))를 사용하여 Raspberry Pi의 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-163">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="83ddf-164">Windows 폴더를 공유하려면 Raspberry Pi Samba 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-164">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="83ddf-165">데스크톱에서 SFTP 클라이언트를 포함한 기본 제공 [SFTP](https://www.raspberrypi.org/documentation/remote-access/) 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-165">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="83ddf-166">SPI 사용</span><span class="sxs-lookup"><span data-stu-id="83ddf-166">Enable SPI</span></span>

<span data-ttu-id="83ddf-167">샘플 응용 프로그램을 실행하기 전에 Raspberry Pi에서 SPI(Serial Peripheral Interface) 버스를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-167">Before you can run the sample application, you must enable the Serial Peripheral Interface (SPI) bus on the Raspberry Pi.</span></span> <span data-ttu-id="83ddf-168">Raspberry Pi는 SPI 버스를 통해 BME280 센서 장치와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-168">The Raspberry Pi communicates with the BME280 sensor device over the SPI bus.</span></span> <span data-ttu-id="83ddf-169">다음 명령을 사용하여 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-169">Use the following command to edit the configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="83ddf-170">다음과 같은 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-170">Find the line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="83ddf-171">줄의 주석 처리를 제거하려면 시작 부분에서 `#`을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-171">To uncomment the line, delete the `#` at the start.</span></span>
- <span data-ttu-id="83ddf-172">변경 내용을 저장하고(**Ctrl-O**, **Enter**) 편집기를 종료합니다(**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="83ddf-172">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="83ddf-173">SPI를 사용하려면 Raspberry Pi를 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-173">To enable SPI, reboot the Raspberry Pi.</span></span> <span data-ttu-id="83ddf-174">다시 부팅하면 터미널의 연결이 끊어지므로 Raspberry Pi를 다시 시작할 경우 다시 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83ddf-174">Rebooting disconnects the terminal, you need to sign in again when the Raspberry Pi restarts:</span></span>

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/