## <a name="install-wordpress"></a>WordPress 설치

스택을 tootry을 원하는 경우 샘플 응용 프로그램을 설치 합니다. 예를 들어, 다음 단계는 hello 설치 hello 오픈 소스 [WordPress](https://wordpress.org/) 플랫폼 toocreate 웹 사이트 및 블로그. 다른 작업 tootry 포함 [Drupal](http://www.drupal.org) 및 [Moodle](https://moodle.org/)합니다. 

이 WordPress 설정은 개념 증명을 위한 것입니다. 자세한 내용 및 프로덕션 설치에 대 한 설정에 대 한 참조 hello [WordPress 설명서](https://codex.wordpress.org/Main_Page)합니다. 



### <a name="install-hello-wordpress-package"></a>Hello WordPress 패키지 설치

Hello 다음 명령을 실행 합니다.

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>WordPress 구성

WordPress toouse MySQL 및 PHP를 구성 합니다. 다음 명령은 tooopen hello 원하는 텍스트 편집기를 실행 하 고 hello 파일을 만들 `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
다음 줄 toohello 파일, 대체에 대 한 데이터베이스 암호 복사 hello *yourPassword* (다른 값을 변경 하지 않고 둠). Hello 파일을 저장 합니다.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

작업 디렉터리에 텍스트 파일을 만들 `wordpress.sql` tooconfigure hello WordPress 데이터베이스: 

```bash
sudo sensible-editor wordpress.sql
```

추가 명령 뒤에 대 한 데이터베이스 암호를 대체 하는 hello *yourPassword* (다른 값을 변경 하지 않고 둠). Hello 파일을 저장 합니다.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


다음 명령 toocreate hello 데이터베이스 hello를 실행 합니다.

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Hello 명령이 완료 되 면 hello 파일 삭제 `wordpress.sql`합니다.

Hello WordPress 설치 toohello 웹 서버 문서 루트를 이동 합니다.

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

이제 hello WordPress 설치를 완료 하 고 hello 플랫폼에 게시할 수 있습니다. 브라우저를 열고 너무 이동`http://yourPublicIPAddress/wordpress`합니다. VM의 hello 공용 IP 주소를 대체 합니다. 이와 유사한 toothis 이미지 표시 됩니다.

![WordPress 설치 페이지](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)