vi /etc/init.d/proxy

	#!/bin/sh
	# /etc/init.d/proxy
	# Ducnc
	# nguyencongduc3112@gmail.com
	# Scritp de quan ly proxy giua ceilometer va zabbix monitoring

	DIR=/root/ZabbixCeilometer-Proxy/
	PID=`ps -ef | grep "/usr/bin/python" | grep proxy.py| awk '{print $2}'`

	case "$1" in
	  start)
		cd $DIR
		echo "Starting proxy zabbix ceilometer"
		/usr/bin/python proxy.py &
		;;
	  stop)
		echo "Stopping proxy zabbix ceilometer"
		kill -9 $PID
		;;
	  restart)
        echo "Restart proxy zabbix ceilometer"
        /etc/init.d/proxy stop
        /etc/init.d/proxy start
        ;;
	  *)
		echo "Usage: /etc/init.d/proxy{start|stop}"
		exit 1
		;;
	esac

	exit 0

chmod 770 /etc/init.d/proxy

/etc/init.d/proxy start

/etc/init.d/proxy stop

update-rc.d proxy defaults
