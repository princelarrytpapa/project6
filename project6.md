## Web Solution With WordPress
git clone git@github.com:princelarrytpapa/project6.git
## AWS EC2 INSTANCE
Created 2 instances
web server attached with volumes
database server attached with volumes
conneted both servers to the terminal
ssh -i "myproject6-key.pem" ec2-user@ec2-107-22-51-23.compute-1.amazonaws.com
ssh -i "myproject6-key.pem" ec2-user@ec2-3-83-130-126.compute-1.amazonaws.com (database)
## webserver commands
 1  lsblk
    2  sudo gdisk /dev/xvdf
    3  sudo gdisk /dev/xvdg
    4  sudo gdisk /dev/xvdh
    5  lsblk
    6  sudo yum install lvm2
    7  sudo lvmdiskscan
    8  sudo pvcreate /dev/xvdf1
    9  sudo pvcreate /dev/xvdg1
   10  sudo pvcreate /dev/xvdh1
   11  sudo pvs
   12  sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1
   13  sudo vgs
   14  sudo lvcreate -n apps-lv -L 14G webdata-vg
   15  sudo lvcreate -n logs-lv -L 14G webdata-vg
   16  sudo vgdisplay -v #view complete setup - VG, PV, and LV
   17  sudo lsblk
   18  sudo mkfs -t ext4 /dev/webdata-vg/apps-lv
   19  sudo mkfs -t ext4 /dev/webdata-vg/logs-lv
   20  sudo mkdir -p /var/www/html
   21  sudo mkdir -p /home/recovery/logs
   22  sudo mount /dev/webdata-vg/apps-lv /var/www/html/
   23  sudo rsync -av /var/log/. /home/recovery/logs/
   24  sudo mount /dev/webdata-vg/logs-lv /var/log
   25  sudo rsync -av /home/recovery/logs/. /var/log
   26  sudo blkid
   27  sudo vi /etc/fstab
   28  mount -a
   29  sudo systemctl daemon-reload
   30  df -h
   31  sudo yum -y update
   32  sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json
   33  sudo systemctl enable httpd
   34  sudo systemctl start httpd
   35  sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
   36  sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
   37  sudo yum remove yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
   38  cat /etc/redhat-release
   39  sudo yum install -y centos-release-8.4
   40  sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
   41  sudo yum install --nobest yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
   42  sudo yum module list php
   43  sudo yum module reset php
   44  sudo yum module enable php:remi-7.4
   45  sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
   46  sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
   
   50  sudo yum install php php-cli php-fpm php-mysql php-zip php-gd php-mbstring php-curl
   51  sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json
   52  sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
   53  sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
   54  sudo yum module list php
   55  sudo yum module reset php
   56  sudo yum module enable php:remi-7.4
   57  sudo yum install php php-opcache php-gd php-curl php-mysqlnd
   58  sudo systemctl start php-fpm
   59  sudo systemctl enable php-fpm
   60  sudo setsebool -P httpd_execmem 1
   61  sudo systemctl restart httpd
   62    mkdir wordpress
   63    cd   wordpress
   64    sudo wget http://wordpress.org/latest.tar.gz
   65    sudo tar xzvf latest.tar.gz
   66    sudo rm -rf latest.tar.gz
   67    cp wordpress/wp-config-sample.php wordpress/wp-config.php
   68    cp -R wordpress/ /var/www/html/
   69  sudo cp wordpress/wp-config-sample.php wordpress/wp-config.php
   70   sudo cp -R wordpress/ /var/www/html/
   71  sudo ls -l /var/www/html
   72  ls -l
   73  cd wordpress
   74  ls -l
   75  
   77  cd ..
   78  sudo cp -R wordpress/ /var/www/html/
   79  sudo ls -l /var/www/html/
   80*
   81  sudo ls -l /var/www/html/
   82  ls -l wordpress
   83  sudo cp -R wordpress/. /var/www/html/
   84  sudo ls -l /var/www/html
   85  cd /var/www/html
   86  ls
   87  sudo yum install mysql-server
   88  sudo systemctl restart mysqld
   89  sudo systemctl enable mysqld
   90  sudo mysql
   91  sudo systemctl start mysqld
   92  sudo systemctl enable mysqld
   93  sudo systemctl status mysqld
  
   96  sudo vi wp-config.php
   97  sudo systemctl restart httpd
   98  sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf_backup
   99  sudo chown -R apache:apache /var/www/html/wordpress
  100  sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R
  101  sudo setsebool -P httpd_can_network_connect=1
  102  sudo setsebool -P httpd_can_network_connect_db 1
  103
  104  sudo mysql -u wordpress -p -h 172.31.86.235
  105  ls -l
  106  sudo chown -R apache:apache /var/www/html/wordpress
  107  ls -l
  108  sudo chown -R apache:apache /var/www/html/
  109  ls -l
  110    sudo chcon -t httpd_sys_rw_content_t /var/www/html/ -R
  111  sudo setsebool -P httpd_can_network_connect=1
  112  sudo setsebool -P httpd_can_network_connect_db 1
  ## database server commands
   1  lsblk
    2  sudo gdisk /dev/xvdf
    3  sudo gdisk /dev/xvdg
    4  sudo gdisk /dev/xvdh
    5  lsblk
    6  sudo yum install lvm2
    7  sudo lvmdiskscan
    8  sudo pvcreate /dev/xvdf1
    9  sudo pvcreate /dev/xvdg1
   10  sudo pvcreate /dev/xvdh1
   11  sudo pvs
   12  sudo vgcreate database-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1
   13  sudo vgs
   14  sudo lvcreate -n db-lv -L 20G database-vg
   15  sudo lvs
   16  sudo vgdisplay -v #view complete setup - VG, PV, and LV
   17  sudo lsblk
   18  sudo mkfs -t ext4 /dev/database-vg/db-lv
   19  sudo mkdir -p /db
   20  sudo mount /dev/database-vg/db-lv /db/
   21  ls -l /db/
   22  sudo blkid
   
   27  sudo vi /etc/fstab
   28  mount -a
   29  sudo systemctl daemon-reload
   30  df -h
   31  sudo yum -y update
   32  sudo yum install mysql-server
   33  sudo systemctl restart mysqld
   34  sudo systemctl enable mysqld
   35  sudo mysql
   36  sudo mysql_secure_installation
   37  sudo vi /etc/my.cnf
   38  sudo systemctl restart mysqld
   39  ip addr show


