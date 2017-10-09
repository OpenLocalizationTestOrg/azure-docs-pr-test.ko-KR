## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="a8c75-101">Raspberry Pi 준비</span><span class="sxs-lookup"><span data-stu-id="a8c75-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="a8c75-102">Raspbian 설치</span><span class="sxs-lookup"><span data-stu-id="a8c75-102">Install Raspbian</span></span>

<span data-ttu-id="a8c75-103">인 경우 hello 라스베리 Pi를 사용 하는 처음으로 tooinstall hello Raspbian 운영 체제 NOOBS hello 키트에 포함 된 hello SD 카드에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="a8c75-104">hello [라스베리 Pi 소프트웨어 가이드] [ lnk-install-raspbian] 설명 방법을 tooinstall 라스베리 Pi에 운영 체제.</span><span class="sxs-lookup"><span data-stu-id="a8c75-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="a8c75-105">이 자습서 라스베리 원주율 hello Raspbian 운영 체제를 설치 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="a8c75-106">hello에 포함 된 hello SD 카드 [라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트] [ lnk-starter-kits] NOOBS 설치에 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="a8c75-107">이 카드의 hello 라스베리 Pi 부팅 수 있으며 tooinstall hello Raspbian 운영 체제를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="a8c75-108">Hello 하드웨어 설정</span><span class="sxs-lookup"><span data-stu-id="a8c75-108">Set up hello hardware</span></span>

<span data-ttu-id="a8c75-109">이 자습서에서는 hello에 포함 된 hello BME280 센서 [라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트] [ lnk-starter-kits] toogenerate 원격 분석 데이터.</span><span class="sxs-lookup"><span data-stu-id="a8c75-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="a8c75-110">LED tooindicate를 사용 하 여 hello 라스베리 Pi hello 솔루션 대시보드에서 메서드 호출을 처리 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a8c75-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="a8c75-111">hello 빵 보드에 hello 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="a8c75-112">빨강 LED</span><span class="sxs-lookup"><span data-stu-id="a8c75-112">Red LED</span></span>
- <span data-ttu-id="a8c75-113">220옴 저항기(빨강, 빨강, 밤색)</span><span class="sxs-lookup"><span data-stu-id="a8c75-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="a8c75-114">BME280 센서</span><span class="sxs-lookup"><span data-stu-id="a8c75-114">BME280 sensor</span></span>

<span data-ttu-id="a8c75-115">hello 다음 다이어그램에서는 어떻게 tooconnect 하드웨어:</span><span class="sxs-lookup"><span data-stu-id="a8c75-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Raspberry Pi의 하드웨어 설정][img-connection-diagram]

<span data-ttu-id="a8c75-117">hello 다음 표에 요약 되어 hello breadboard에 hello 라스베리 Pi toohello 구성 요소에서 hello 연결:</span><span class="sxs-lookup"><span data-stu-id="a8c75-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="a8c75-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="a8c75-118">Raspberry Pi</span></span>            | <span data-ttu-id="a8c75-119">브레드보드</span><span class="sxs-lookup"><span data-stu-id="a8c75-119">Breadboard</span></span>             |<span data-ttu-id="a8c75-120">색</span><span class="sxs-lookup"><span data-stu-id="a8c75-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="a8c75-121">GND(14 핀)</span><span class="sxs-lookup"><span data-stu-id="a8c75-121">GND (Pin 14)</span></span>            | <span data-ttu-id="a8c75-122">LED -ve 핀(18A)</span><span class="sxs-lookup"><span data-stu-id="a8c75-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="a8c75-123">자주색</span><span class="sxs-lookup"><span data-stu-id="a8c75-123">Purple</span></span>          |
| <span data-ttu-id="a8c75-124">GPCLK0(7 핀)</span><span class="sxs-lookup"><span data-stu-id="a8c75-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="a8c75-125">저항기(25A)</span><span class="sxs-lookup"><span data-stu-id="a8c75-125">Resistor (25A)</span></span>         | <span data-ttu-id="a8c75-126">주황색</span><span class="sxs-lookup"><span data-stu-id="a8c75-126">Orange</span></span>          |
| <span data-ttu-id="a8c75-127">SPI_CE0(24 핀)</span><span class="sxs-lookup"><span data-stu-id="a8c75-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="a8c75-128">CS(39A)</span><span class="sxs-lookup"><span data-stu-id="a8c75-128">CS (39A)</span></span>               | <span data-ttu-id="a8c75-129">파랑</span><span class="sxs-lookup"><span data-stu-id="a8c75-129">Blue</span></span>          |
| <span data-ttu-id="a8c75-130">SPI_SCLK(23 핀)</span><span class="sxs-lookup"><span data-stu-id="a8c75-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="a8c75-131">SCK(36A)</span><span class="sxs-lookup"><span data-stu-id="a8c75-131">SCK (36A)</span></span>              | <span data-ttu-id="a8c75-132">노랑</span><span class="sxs-lookup"><span data-stu-id="a8c75-132">Yellow</span></span>        |
| <span data-ttu-id="a8c75-133">SPI_MISO(21 핀)</span><span class="sxs-lookup"><span data-stu-id="a8c75-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="a8c75-134">SDO(37A)</span><span class="sxs-lookup"><span data-stu-id="a8c75-134">SDO (37A)</span></span>              | <span data-ttu-id="a8c75-135">흰색</span><span class="sxs-lookup"><span data-stu-id="a8c75-135">White</span></span>         |
| <span data-ttu-id="a8c75-136">SPI_MOSI(19 핀)</span><span class="sxs-lookup"><span data-stu-id="a8c75-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="a8c75-137">SDI(38A)</span><span class="sxs-lookup"><span data-stu-id="a8c75-137">SDI (38A)</span></span>              | <span data-ttu-id="a8c75-138">녹색</span><span class="sxs-lookup"><span data-stu-id="a8c75-138">Green</span></span>         |
| <span data-ttu-id="a8c75-139">GND(6 핀)</span><span class="sxs-lookup"><span data-stu-id="a8c75-139">GND (Pin 6)</span></span>             | <span data-ttu-id="a8c75-140">GND(35A)</span><span class="sxs-lookup"><span data-stu-id="a8c75-140">GND (35A)</span></span>              | <span data-ttu-id="a8c75-141">검정</span><span class="sxs-lookup"><span data-stu-id="a8c75-141">Black</span></span>         |
| <span data-ttu-id="a8c75-142">3.3V(1 핀)</span><span class="sxs-lookup"><span data-stu-id="a8c75-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="a8c75-143">3Vo(34A)</span><span class="sxs-lookup"><span data-stu-id="a8c75-143">3Vo (34A)</span></span>              | <span data-ttu-id="a8c75-144">빨강</span><span class="sxs-lookup"><span data-stu-id="a8c75-144">Red</span></span>           |

<span data-ttu-id="a8c75-145">toocomplete hello 하드웨어 설치 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="a8c75-146">Hello 키트에 포함 된 라스베리 Pi toohello 전원 공급 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="a8c75-147">키트에 포함 된 hello 이더넷 케이블을 사용 하 여 라스베리 Pi tooyour 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="a8c75-148">또는 Raspberry Pi에 대해 [무선 연결][lnk-pi-wireless]을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="a8c75-149">이제 hello 하드웨어를 라스베리 Pi의 설치를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="a8c75-150">로그인 및 액세스 hello 터미널</span><span class="sxs-lookup"><span data-stu-id="a8c75-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="a8c75-151">환경을 사용 하는 두 가지 옵션 tooaccess 터미널 라스베리 원주율:</span><span class="sxs-lookup"><span data-stu-id="a8c75-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="a8c75-152">키보드 연결된 tooyour 라스베리 Pi를 모니터링 하는 경우에 hello Raspbian GUI tooaccess 터미널 윈도우를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="a8c75-153">액세스 hello 명령줄 데스크톱 컴퓨터의 SSH를 사용 하 여 라스베리 원주율입니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="a8c75-154">Hello GUI에서에서 터미널 윈도우를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a8c75-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="a8c75-155">Raspbian에 대 한 hello 기본 자격 증명이 username **pi** 및 암호 **라스베리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="a8c75-156">Hello GUI에에서 hello 작업 표시줄에서 hello를 시작할 수 있습니다 **터미널** hello 모양의 아이콘을 모니터를 사용 하 여 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="a8c75-157">SSH를 사용하여 로그인</span><span class="sxs-lookup"><span data-stu-id="a8c75-157">Sign in with SSH</span></span>

<span data-ttu-id="a8c75-158">명령줄 액세스 tooyour 라스베리 Pi에 대 한 SSH를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="a8c75-159">hello 문서 [SSH (보안 셸)] [ lnk-pi-ssh] 설명 방법을 tooconfigure 라스베리 Pi와의 SSH 방법과에서 tooconnect [Windows] [ lnk-ssh-windows] 또는 [Linux 및 Mac OS][lnk-ssh-linux]합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="a8c75-160">사용자 이름 **pi** 및 암호 **raspberry**로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="a8c75-161">선택 사항: Raspberry Pi의 폴더 공유</span><span class="sxs-lookup"><span data-stu-id="a8c75-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="a8c75-162">필요에 따라 데스크톱 환경 라스베리 원주율 tooshare 폴더를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="a8c75-163">공유 폴더를 사용 하면 있습니다 toouse 데스크톱 원하는 텍스트 편집기 (예: [Visual Studio Code](https://code.visualstudio.com/) 또는 [Sublime 텍스트](http://www.sublimetext.com/)) tooedit 파일을 사용 하는 대신 프로그램 라스베리 Pi `nano` 또는 `vi`.</span><span class="sxs-lookup"><span data-stu-id="a8c75-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="a8c75-164">Windows와 함께 폴더 tooshare hello 라스베리 Pi에서 Samba 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="a8c75-165">또는 기본 제공 hello를 사용 하 여 [SFTP](https://www.raspberrypi.org/documentation/remote-access/) 바탕 화면에 SFTP 클라이언트와 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="a8c75-166">SPI 사용</span><span class="sxs-lookup"><span data-stu-id="a8c75-166">Enable SPI</span></span>

<span data-ttu-id="a8c75-167">Hello 샘플 응용 프로그램을 실행 하기 전에 hello 직렬 주변 SPI (인터페이스) 버스 라스베리 Pi hello에 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="a8c75-168">hello 라스베리 Pi hello SPI 버스 통해 hello BME280 센서 장치와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="a8c75-169">다음 명령은 tooedit hello 구성 파일 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="a8c75-170">Hello 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="a8c75-171">delete hello toouncomment hello 선 `#` hello 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="a8c75-172">변경 내용을 저장 (**Ctrl-O**, **Enter**) 및 exit hello 편집기 (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="a8c75-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="a8c75-173">tooenable SPI, 라스베리 Pi hello를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="a8c75-174">Hello 터미널의 연결을 끊습니다 재부팅 toosign 다시 라스베리 Pi hello를 다시 시작할 때에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8c75-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

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