# backup-scripts

A collection of backup scripts using TAR, LVM, mount, RSYNC and MySQL

Sample crontab:
```
23 03 *   *   *   $MYBIN/mysql-backup 1>> $MYLOG/mysql-backup.log 2>&1
23 02 *   *   *   $MYBIN/rm-old-files --dir=/backup/ --regex="^(\S+)-mysqldump-\S+\.sql.gz" --keep=30 1>> $MYLOG/mysql-backup.log 2>&1

23 04 *   *   7   $MYBIN/backup-tar -f 1>> $MYLOG/backup-tar.log 2>&1
23 04 *   *   1-6 $MYBIN/backup-tar -d 1>> $MYLOG/backup-tar.log 2>&1
´´´

## License

backup-scripts

Copyright (C) 2012 naymspace <http://naymspace.de>

Copyright (C) 2013-2015 Tobias M.-Nissen <tn@movb.de>

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

