---
layout: post
title: Add fnv1a_udf to mysql
---

To add fnv1a hash function to your existing mysql community edition or mariadb installation do this:
{% highlight Bash %}
wget http://www.percona.com/redir/downloads/Percona-Server-5.6/LATEST/source/tarball/percona-server-5.6.20-68.0.tar.gz
cd percona-server-5.6.20-68.0/plugin/percona-udf/
gcc -fPIC -Wall -I/usr/include/mysql -shared -o fnv1a_udf.so fnv1a_udf.cc
cp fnv1a_udf.so /usr/lib64/mysql/plugin/
mysql mysql -e "CREATE FUNCTION fnv1a_64 RETURNS INTEGER SONAME 'fnv1a_udf.so'"
{% endhighlight %}

