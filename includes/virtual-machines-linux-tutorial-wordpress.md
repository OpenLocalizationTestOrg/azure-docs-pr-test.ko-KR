## <a name="install-wordpress"></a><span data-ttu-id="642b7-101">WordPress 설치</span><span class="sxs-lookup"><span data-stu-id="642b7-101">Install WordPress</span></span>

<span data-ttu-id="642b7-102">스택을 사용하려는 경우 샘플 앱을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="642b7-103">예를 들어, 다음 단계는 오픈 소스 [WordPress](https://wordpress.org/) 플랫폼을 설치하여 웹 사이트 및 블로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="642b7-104">[Drupal](http://www.drupal.org) 및 [Moodle](https://moodle.org/)을 포함하려는 다른 워크로드입니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="642b7-105">이 WordPress 설정은 개념 증명을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="642b7-106">프로덕션 설치에 대한 자세한 내용 및 설정은 [WordPress 설명서](https://codex.wordpress.org/Main_Page)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="642b7-106">For more information and settings for production installation, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="642b7-107">WordPress 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="642b7-107">Install the WordPress package</span></span>

<span data-ttu-id="642b7-108">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="642b7-109">WordPress 구성</span><span class="sxs-lookup"><span data-stu-id="642b7-109">Configure WordPress</span></span>

<span data-ttu-id="642b7-110">MySQL 및 PHP를 사용하도록 WordPress를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-110">Configure WordPress to use MySQL and PHP.</span></span> <span data-ttu-id="642b7-111">다음 명령을 실행하여 원하는 텍스트 편집기를 열고 `/etc/wordpress/config-localhost.php` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-111">Run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="642b7-112">파일에 다음 줄을 복사하여 *yourPassword*에 대한 데이터베이스 암호를 대체합니다(다른 값을 변경하지 않고 둠).</span><span class="sxs-lookup"><span data-stu-id="642b7-112">Copy the following lines to the file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="642b7-113">그런 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-113">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="642b7-114">작업 디렉터리에서 `wordpress.sql` 텍스트 파일을 만들어 WordPress 데이터베이스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-114">In a working directory, create a text file `wordpress.sql` to configure the WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="642b7-115">다음 명령을 추가하여 *yourPassword*에 대한 데이터베이스 암호를 대체합니다(다른 값을 변경하지 않고 둠).</span><span class="sxs-lookup"><span data-stu-id="642b7-115">Add the following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="642b7-116">그런 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-116">Then save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="642b7-117">다음 명령을 실행하여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-117">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="642b7-118">명령이 완료된 후 `wordpress.sql` 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-118">After the command completes, delete the file `wordpress.sql`.</span></span>

<span data-ttu-id="642b7-119">웹 서버 문서 루트로 WordPress 설치를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-119">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="642b7-120">이제 WordPress 설정을 완료하고 플랫폼에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-120">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="642b7-121">웹 브라우저를 열고 `http://yourPublicIPAddress/wordpress`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-121">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="642b7-122">VM의 공용 IP 주소를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-122">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="642b7-123">이 이미지와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="642b7-123">It should look similar to this image.</span></span>

![WordPress 설치 페이지](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)