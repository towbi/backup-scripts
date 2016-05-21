# backup-scripts

A collection of backup scripts using TAR, LVM, mount, RSYNC and MySQL

## Example usage

### Configuration

*Crontab:*
```
23 03 *   *   *   $MYBIN/mysql-backup 1>> $MYLOG/mysql-backup.log 2>&1
23 02 *   *   *   $MYBIN/rm-old-files --dir=/backup/ --regex="^(\S+)-mysqldump-\S+\.sql.gz" --keep=30 1>> $MYLOG/mysql-backup.log 2>&1

23 04 *   *   7   $MYBIN/backup-tar -f 1>> $MYLOG/backup-tar.log 2>&1
23 04 *   *   1-6 $MYBIN/backup-tar -d 1>> $MYLOG/backup-tar.log 2>&1
```

*backup-tar.conf:*
```
TARGET=/backup
DIRECTORIES=/var/www/myproject
KEEP_FULL=10
KEEP_DIFFERENTIAL=12
RM_OLD_FILES=/root/bin/rm-old-files
```

*mysql-backup.conf:*
```
TARGET=/backup
```

### Backup directory contents

Here's a directory listing of `backup-tar` and `mysql-backup` in use on an
actual production site.

```
tobi@myproject:/backup$ la
total 2241812
-rw-r--r-- 1 root root    309174 Apr 21 03:23 myproject-mysqldump-2016-04-21.sql.gz
-rw-r--r-- 1 root root    313309 Apr 22 03:23 myproject-mysqldump-2016-04-22.sql.gz
-rw-r--r-- 1 root root    315719 Apr 23 03:23 myproject-mysqldump-2016-04-23.sql.gz
-rw-r--r-- 1 root root    318191 Apr 24 03:23 myproject-mysqldump-2016-04-24.sql.gz
-rw-r--r-- 1 root root    320106 Apr 25 03:23 myproject-mysqldump-2016-04-25.sql.gz
-rw-r--r-- 1 root root    323362 Apr 26 03:23 myproject-mysqldump-2016-04-26.sql.gz
-rw-r--r-- 1 root root    326314 Apr 27 03:23 myproject-mysqldump-2016-04-27.sql.gz
-rw-r--r-- 1 root root    329285 Apr 28 03:23 myproject-mysqldump-2016-04-28.sql.gz
-rw-r--r-- 1 root root    331862 Apr 29 03:23 myproject-mysqldump-2016-04-29.sql.gz
-rw-r--r-- 1 root root    334990 Apr 30 03:23 myproject-mysqldump-2016-04-30.sql.gz
-rw-r--r-- 1 root root    338134 May  1 03:23 myproject-mysqldump-2016-05-01.sql.gz
-rw-r--r-- 1 root root    340742 May  2 03:23 myproject-mysqldump-2016-05-02.sql.gz
-rw-r--r-- 1 root root    344464 May  3 03:23 myproject-mysqldump-2016-05-03.sql.gz
-rw-r--r-- 1 root root    347945 May  4 03:23 myproject-mysqldump-2016-05-04.sql.gz
-rw-r--r-- 1 root root    352233 May  5 03:23 myproject-mysqldump-2016-05-05.sql.gz
-rw-r--r-- 1 root root    354566 May  6 03:23 myproject-mysqldump-2016-05-06.sql.gz
-rw-r--r-- 1 root root    357383 May  7 03:23 myproject-mysqldump-2016-05-07.sql.gz
-rw-r--r-- 1 root root    359976 May  8 03:23 myproject-mysqldump-2016-05-08.sql.gz
-rw-r--r-- 1 root root    364229 May  9 03:23 myproject-mysqldump-2016-05-09.sql.gz
-rw-r--r-- 1 root root    367688 May 10 03:23 myproject-mysqldump-2016-05-10.sql.gz
-rw-r--r-- 1 root root    370584 May 11 03:23 myproject-mysqldump-2016-05-11.sql.gz
-rw-r--r-- 1 root root    373792 May 12 03:23 myproject-mysqldump-2016-05-12.sql.gz
-rw-r--r-- 1 root root    376762 May 13 03:23 myproject-mysqldump-2016-05-13.sql.gz
-rw-r--r-- 1 root root    379440 May 14 03:23 myproject-mysqldump-2016-05-14.sql.gz
-rw-r--r-- 1 root root    381363 May 15 03:23 myproject-mysqldump-2016-05-15.sql.gz
-rw-r--r-- 1 root root    384881 May 16 03:23 myproject-mysqldump-2016-05-16.sql.gz
-rw-r--r-- 1 root root    386450 May 17 03:23 myproject-mysqldump-2016-05-17.sql.gz
-rw-r--r-- 1 root root    390361 May 18 03:23 myproject-mysqldump-2016-05-18.sql.gz
-rw-r--r-- 1 root root    393601 May 19 03:23 myproject-mysqldump-2016-05-19.sql.gz
-rw-r--r-- 1 root root    395987 May 20 03:23 myproject-mysqldump-2016-05-20.sql.gz
-rw-r--r-- 1 root root    399970 May 21 03:23 myproject-mysqldump-2016-05-21.sql.gz
-rw-r--r-- 1 root root    166818 Apr 21 03:23 myproject-dev-mysqldump-2016-04-21.sql.gz
-rw-r--r-- 1 root root    166818 Apr 22 03:23 myproject-dev-mysqldump-2016-04-22.sql.gz
-rw-r--r-- 1 root root    166817 Apr 23 03:23 myproject-dev-mysqldump-2016-04-23.sql.gz
-rw-r--r-- 1 root root    166818 Apr 24 03:23 myproject-dev-mysqldump-2016-04-24.sql.gz
-rw-r--r-- 1 root root    166817 Apr 25 03:23 myproject-dev-mysqldump-2016-04-25.sql.gz
-rw-r--r-- 1 root root    166818 Apr 26 03:23 myproject-dev-mysqldump-2016-04-26.sql.gz
-rw-r--r-- 1 root root    166818 Apr 27 03:23 myproject-dev-mysqldump-2016-04-27.sql.gz
-rw-r--r-- 1 root root    166818 Apr 28 03:23 myproject-dev-mysqldump-2016-04-28.sql.gz
-rw-r--r-- 1 root root    166818 Apr 29 03:23 myproject-dev-mysqldump-2016-04-29.sql.gz
-rw-r--r-- 1 root root    166817 Apr 30 03:23 myproject-dev-mysqldump-2016-04-30.sql.gz
-rw-r--r-- 1 root root    166818 May  1 03:23 myproject-dev-mysqldump-2016-05-01.sql.gz
-rw-r--r-- 1 root root    166818 May  2 03:23 myproject-dev-mysqldump-2016-05-02.sql.gz
-rw-r--r-- 1 root root    166818 May  3 03:23 myproject-dev-mysqldump-2016-05-03.sql.gz
-rw-r--r-- 1 root root    166817 May  4 03:23 myproject-dev-mysqldump-2016-05-04.sql.gz
-rw-r--r-- 1 root root    166816 May  5 03:23 myproject-dev-mysqldump-2016-05-05.sql.gz
-rw-r--r-- 1 root root    166818 May  6 03:23 myproject-dev-mysqldump-2016-05-06.sql.gz
-rw-r--r-- 1 root root    166818 May  7 03:23 myproject-dev-mysqldump-2016-05-07.sql.gz
-rw-r--r-- 1 root root    166818 May  8 03:23 myproject-dev-mysqldump-2016-05-08.sql.gz
-rw-r--r-- 1 root root    166818 May  9 03:23 myproject-dev-mysqldump-2016-05-09.sql.gz
-rw-r--r-- 1 root root    166818 May 10 03:23 myproject-dev-mysqldump-2016-05-10.sql.gz
-rw-r--r-- 1 root root    166818 May 11 03:23 myproject-dev-mysqldump-2016-05-11.sql.gz
-rw-r--r-- 1 root root    166818 May 12 03:23 myproject-dev-mysqldump-2016-05-12.sql.gz
-rw-r--r-- 1 root root    166817 May 13 03:23 myproject-dev-mysqldump-2016-05-13.sql.gz
-rw-r--r-- 1 root root    166817 May 14 03:23 myproject-dev-mysqldump-2016-05-14.sql.gz
-rw-r--r-- 1 root root    166818 May 15 03:23 myproject-dev-mysqldump-2016-05-15.sql.gz
-rw-r--r-- 1 root root    166818 May 16 03:23 myproject-dev-mysqldump-2016-05-16.sql.gz
-rw-r--r-- 1 root root    166818 May 17 03:23 myproject-dev-mysqldump-2016-05-17.sql.gz
-rw-r--r-- 1 root root    166818 May 18 03:23 myproject-dev-mysqldump-2016-05-18.sql.gz
-rw-r--r-- 1 root root    166818 May 19 03:23 myproject-dev-mysqldump-2016-05-19.sql.gz
-rw-r--r-- 1 root root    166818 May 20 03:23 myproject-dev-mysqldump-2016-05-20.sql.gz
-rw-r--r-- 1 root root    172419 May 21 03:23 myproject-dev-mysqldump-2016-05-21.sql.gz
-rw-r--r-- 1 root root    128989 Apr 21 03:23 myproject-prodlike-mysqldump-2016-04-21.sql.gz
-rw-r--r-- 1 root root    128989 Apr 22 03:23 myproject-prodlike-mysqldump-2016-04-22.sql.gz
-rw-r--r-- 1 root root    128989 Apr 23 03:23 myproject-prodlike-mysqldump-2016-04-23.sql.gz
-rw-r--r-- 1 root root    128989 Apr 24 03:23 myproject-prodlike-mysqldump-2016-04-24.sql.gz
-rw-r--r-- 1 root root    128989 Apr 25 03:23 myproject-prodlike-mysqldump-2016-04-25.sql.gz
-rw-r--r-- 1 root root    128989 Apr 26 03:23 myproject-prodlike-mysqldump-2016-04-26.sql.gz
-rw-r--r-- 1 root root    128989 Apr 27 03:23 myproject-prodlike-mysqldump-2016-04-27.sql.gz
-rw-r--r-- 1 root root    128989 Apr 28 03:23 myproject-prodlike-mysqldump-2016-04-28.sql.gz
-rw-r--r-- 1 root root    128989 Apr 29 03:23 myproject-prodlike-mysqldump-2016-04-29.sql.gz
-rw-r--r-- 1 root root    128989 Apr 30 03:23 myproject-prodlike-mysqldump-2016-04-30.sql.gz
-rw-r--r-- 1 root root    128989 May  1 03:23 myproject-prodlike-mysqldump-2016-05-01.sql.gz
-rw-r--r-- 1 root root    128989 May  2 03:23 myproject-prodlike-mysqldump-2016-05-02.sql.gz
-rw-r--r-- 1 root root    128989 May  3 03:23 myproject-prodlike-mysqldump-2016-05-03.sql.gz
-rw-r--r-- 1 root root    128989 May  4 03:23 myproject-prodlike-mysqldump-2016-05-04.sql.gz
-rw-r--r-- 1 root root    128989 May  5 03:23 myproject-prodlike-mysqldump-2016-05-05.sql.gz
-rw-r--r-- 1 root root    128989 May  6 03:23 myproject-prodlike-mysqldump-2016-05-06.sql.gz
-rw-r--r-- 1 root root    128989 May  7 03:23 myproject-prodlike-mysqldump-2016-05-07.sql.gz
-rw-r--r-- 1 root root    128989 May  8 03:23 myproject-prodlike-mysqldump-2016-05-08.sql.gz
-rw-r--r-- 1 root root    128989 May  9 03:23 myproject-prodlike-mysqldump-2016-05-09.sql.gz
-rw-r--r-- 1 root root    128989 May 10 03:23 myproject-prodlike-mysqldump-2016-05-10.sql.gz
-rw-r--r-- 1 root root    128989 May 11 03:23 myproject-prodlike-mysqldump-2016-05-11.sql.gz
-rw-r--r-- 1 root root    128989 May 12 03:23 myproject-prodlike-mysqldump-2016-05-12.sql.gz
-rw-r--r-- 1 root root    128989 May 13 03:23 myproject-prodlike-mysqldump-2016-05-13.sql.gz
-rw-r--r-- 1 root root    128989 May 14 03:23 myproject-prodlike-mysqldump-2016-05-14.sql.gz
-rw-r--r-- 1 root root    128989 May 15 03:23 myproject-prodlike-mysqldump-2016-05-15.sql.gz
-rw-r--r-- 1 root root    128989 May 16 03:23 myproject-prodlike-mysqldump-2016-05-16.sql.gz
-rw-r--r-- 1 root root    128989 May 17 03:23 myproject-prodlike-mysqldump-2016-05-17.sql.gz
-rw-r--r-- 1 root root    128989 May 18 03:23 myproject-prodlike-mysqldump-2016-05-18.sql.gz
-rw-r--r-- 1 root root    128989 May 19 03:23 myproject-prodlike-mysqldump-2016-05-19.sql.gz
-rw-r--r-- 1 root root    128989 May 20 03:23 myproject-prodlike-mysqldump-2016-05-20.sql.gz
-rw-r--r-- 1 root root    128989 May 21 03:23 myproject-prodlike-mysqldump-2016-05-21.sql.gz
-rw-r--r-- 1 root root    621144 May  9 04:23 var-www-myproject-from-2016-05-08-diff-2016-05-09.tar.gz
-rw-r--r-- 1 root root    660479 May 10 04:23 var-www-myproject-from-2016-05-08-diff-2016-05-10.tar.gz
-rw-r--r-- 1 root root    660859 May 11 04:23 var-www-myproject-from-2016-05-08-diff-2016-05-11.tar.gz
-rw-r--r-- 1 root root    660999 May 12 04:23 var-www-myproject-from-2016-05-08-diff-2016-05-12.tar.gz
-rw-r--r-- 1 root root    660940 May 13 04:23 var-www-myproject-from-2016-05-08-diff-2016-05-13.tar.gz
-rw-r--r-- 1 root root    660902 May 14 04:23 var-www-myproject-from-2016-05-08-diff-2016-05-14.tar.gz
-rw-r--r-- 1 root root    621137 May 16 04:23 var-www-myproject-from-2016-05-15-diff-2016-05-16.tar.gz
-rw-r--r-- 1 root root    660336 May 17 04:23 var-www-myproject-from-2016-05-15-diff-2016-05-17.tar.gz
-rw-r--r-- 1 root root    660399 May 18 04:23 var-www-myproject-from-2016-05-15-diff-2016-05-18.tar.gz
-rw-r--r-- 1 root root    660443 May 19 04:23 var-www-myproject-from-2016-05-15-diff-2016-05-19.tar.gz
-rw-r--r-- 1 root root    660775 May 20 04:23 var-www-myproject-from-2016-05-15-diff-2016-05-20.tar.gz
-rw-r--r-- 1 root root   1207364 May 21 04:23 var-www-myproject-from-2016-05-15-diff-2016-05-21.tar.gz
-rw-r--r-- 1 root root   3053681 Mar 13 04:24 var-www-myproject-full-2016-03-13.snar
-rw-r--r-- 1 root root 219822159 Mar 13 04:24 var-www-myproject-full-2016-03-13.tar.gz
-rw-r--r-- 1 root root   3055377 Mar 20 04:24 var-www-myproject-full-2016-03-20.snar
-rw-r--r-- 1 root root 220408853 Mar 20 04:24 var-www-myproject-full-2016-03-20.tar.gz
-rw-r--r-- 1 root root   3055576 Mar 27 04:24 var-www-myproject-full-2016-03-27.snar
-rw-r--r-- 1 root root 220205613 Mar 27 04:24 var-www-myproject-full-2016-03-27.tar.gz
-rw-r--r-- 1 root root   3025519 Apr  3 04:24 var-www-myproject-full-2016-04-03.snar
-rw-r--r-- 1 root root 218402860 Apr  3 04:24 var-www-myproject-full-2016-04-03.tar.gz
-rw-r--r-- 1 root root   3025390 Apr 10 04:24 var-www-myproject-full-2016-04-10.snar
-rw-r--r-- 1 root root 218111909 Apr 10 04:24 var-www-myproject-full-2016-04-10.tar.gz
-rw-r--r-- 1 root root   3073767 Apr 17 04:24 var-www-myproject-full-2016-04-17.snar
-rw-r--r-- 1 root root 223457190 Apr 17 04:24 var-www-myproject-full-2016-04-17.tar.gz
-rw-r--r-- 1 root root   3074077 Apr 24 04:24 var-www-myproject-full-2016-04-24.snar
-rw-r--r-- 1 root root 223485859 Apr 24 04:24 var-www-myproject-full-2016-04-24.tar.gz
-rw-r--r-- 1 root root   3074007 May  1 04:24 var-www-myproject-full-2016-05-01.snar
-rw-r--r-- 1 root root 223325351 May  1 04:24 var-www-myproject-full-2016-05-01.tar.gz
-rw-r--r-- 1 root root   3073380 May  8 04:24 var-www-myproject-full-2016-05-08.snar
-rw-r--r-- 1 root root 223197092 May  8 04:24 var-www-myproject-full-2016-05-08.tar.gz
-rw-r--r-- 1 root root   3073368 May 15 04:24 var-www-myproject-full-2016-05-15.snar
-rw-r--r-- 1 root root 223193558 May 15 04:24 var-www-myproject-full-2016-05-15.tar.gz
```

## License

backup-scripts

Copyright (C) 2012 naymspace <http://naymspace.de>

Copyright (C) 2013-2015 Tobias M.-Nissen <tn@movb.de>

Copyright (C) 2016 Tobias König <tn@movb.de>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

