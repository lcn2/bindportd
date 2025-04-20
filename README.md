# bindportd

bind to tcp or udp ports


## why bindportd?

NOTE: Executing the following command:

    /usr/local/sbin/bindport -i -s /etc/sysconfig/bindport

right after the network is started is useful as it grabs and holds
on to ports that are often the subject of system crackers and other
network attacks.

Of course, the usefulness depends on the contents of `/etc/sysconfig/bindport`.

Even if you are behind router, packet filter or ipchain control where the
inbound and/or outbound packets to certain ports are blocked, system and
user applications may still try to bind to these ports.  If your application
is unlucky enough to pick one if these blocked ports, it will appear that
the network is dead or non-responsive.

Applications may try to bind to blocks ports perfect valid reasons.
It is perfectly reasonable for a program to use almost any random unused
privileged port.  In fact there are facilities where an application
will ask for any random, unprivileged and unused port on which to listen
or make connections.	Such applications have no way of knowing that the
router/packet filter/ipchain will block them.


# To install

```sh
sudo make install
```


# Examle

```
$ /usr/local/sbin/bindport -c portset.example
```

NOTE: The `portset.example` is just an example **portset** file.
Consider which ports to wish to block by perhaps, looking at `/etc/services`
on your local host.

***WARNING***: The ``portset.example` port list may not be complete.
It may also contain services that you want to use (such as socks).
Just the command to suit your needs and current network attacks.

Also consider:

```sh
$ /usr/local/sbin/bindport -c -i -s portset
```


# To use

```
/usr/local/bin/bindportd [-b] [-c] [-h] [-i] [-m maxport] [-s] [-v] [-V] [-w] portset

	-b	(option ignored, always forks in background)
	-c	close open files after startup (except STDOUT/STDERR if -v)
	-h	print this usage message
	-i	silently ignore privileged ports (0 <= port <= 1023)
	-m	max ports per child (default: 1000)
	-s	block all blockable signals
	-v	verbose
	-V	print version and exit
	-w	(ignored, forked children always wait forever after binding)

    portset is a file containing lines of the form:

	# comment ignored
	# empty line ignored

	udp/portnum		# comment ignored
	tcp/portnum		# comment ignored
	reserve-udp/portnum	# comment ignored
	reserve-tcp/portnum	# comment ignored
	where portnum is an integer [0,65535]
	only udp/portnum and tcp/portnum lines result in port binding

bindportd version: 1.0.0 2025-03-22
```


# Reporting Security Issues

To report a security issue, please visit "[Reporting Security Issues](https://github.com/lcn2/bindportd/security/policy)".
