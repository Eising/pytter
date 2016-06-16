# Pytter
A really simple library for Python to generating reverse DNS.

It's meant to be used if you are parsing IP/Hostname mappings from an external
source, and want to export reverse zones from that.

# Examples

## Code

```python
import pytter

config = {'primary_server' : 'my.dns.server.', 'email' : 'hostmaster.my.dns.'}

rd = pytter.Pytter(config)

rd.add_reverse("10.0.0.1", "1.my.domain.name.")
rd.add_reverse("10.1.0.3", "3,my.domain.name.")
rd.add_reverse("10.1.0.4", "4.my.domain.name.")
rd.add_reverse("2001:db8::1", "1.my.domain.name.")

rd.dump_zones(".")
```

This dumps reverse zones in "." for each /24 or /48 network depending on
whether it's IPv4 or IPv6

## Config dict

The config dict has the following options and defaults:

```python
config = {
        'default_ttl' : 86400,
        'primary_server' : None,
        'email' : None,
        'refresh' : 14400,
        'retry' : 1800,
        'expire' : 1209600,
        'minimum_ttl' : 3600,
        'soa_ttl' : 1800,
        'nameservers' : []
}
```

## Setting the Serial

The serial of the zones are automatically set to YYYYMMDD00, but can be set to
whatever you want.

```python

rd = pytter.Pytter(config)

rd.serialnumber = time.strftime("%Y%m%d01")

```

