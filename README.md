collectd-haproxy
================
This is a collectd plugin to pull HAProxy (<http://haproxy.1wt.eu>) stats from the HAProxy management socket.
It is written in Python and as such, runs under the collectd Python plugin.

Requirements
------------

*HAProxy*  
To use this plugin, HAProxy must be configured to create a management socket with the `stats socket`
configuration option. collectd must have read/write access to the socket.

*collectd*  
collectd must have the Python plugin installed. See (<http://collectd.org/documentation/manpages/collectd-python.5.shtml>)

Options
-------
* `ProxyMonitor`  
Regular expression for proxy/backend to monitor. If unset, defaults to '^(backend|frontend)'.
* `Socket`  
File location of the HAProxy management socket
* `Verbose`  
Enable verbose logging

Example
-------
    <LoadPlugin python>
        Globals true
    </LoadPlugin>

    <Plugin python>
        # haproxy.py is at /usr/lib64/collectd/haproxy.py
        ModulePath "/usr/lib64/collectd/"

        Import "haproxy"

        <Module haproxy>
          Socket "/var/run/haproxy.sock"
          ProxyMonitor "^(backend|frontend|app-*)"
        </Module>
    </Plugin>
