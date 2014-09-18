---
layout: post
title: Add fnv1a_udf to mysql
---

To add fnv1a hash function to your existing mysql community edition or mariadb installation do this:
{% highlight Bash %}
wget http://www.percona.com/redir/downloads/Percona-Server-5.6/LATEST/source/tarball/percona-server-5.6.20-68.0.tar.gz
tar xzf percona-server-5.6.20-68.0.tar.gz
cd percona-server-5.6.20-68.0/plugin/percona-udf/
gcc `mysql_config --cflags` -02 -Wall `mysql_config --include` -shared -o fnv1a_udf.so fnv1a_udf.cc
cp fnv1a_udf.so /usr/lib64/mysql/plugin/
mysql -e "CREATE FUNCTION fnv1a_64 RETURNS INTEGER SONAME 'fnv1a_udf.so'"
{% endhighlight %}

try it..
{% highlight Bash %}
MariaDB [(none)]> select fnv1a_64('123');
+---------------------+
| fnv1a_64('123')     |
+---------------------+
| 5003431119771845851 |
+---------------------+
1 row in set (0.11 sec)
{% endhighlight %}

If you get errno: 22 /lib/libfnv1a_udf.so: undefined symbol: 
 * __gxx_personality_v0 you need to use g++ instead of gcc.

