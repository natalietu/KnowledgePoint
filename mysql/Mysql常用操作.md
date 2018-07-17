### sql导出数据

	mysql -hxxx -uroot -p123456  --default-character-set=utf8 -e 'select  a,b,c from tablename ;' databasename > /home/www/natalie/document/xxx.xls