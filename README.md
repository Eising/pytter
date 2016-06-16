# Pytter
A really simple library for Python to generating reverse DNS.

It's meant to be used if you are parsing IP/Hostname mappings from an external
source, and want to export reverse zones from that.

# Examples

## Code

```python
import pytter

config = {'primary_server' : 'my.dns.server.', 'email' : 'hostmaster.my.dns.'}

rd = pytter.Pytter(primary_server='my.dns.server.', email='hostmaster.my.dns.')

rd.add_reverse("10.0.0.1", "1.my.domain.name.")
rd.add_reverse("10.1.0.3", "3,my.domain.name.")
rd.add_reverse("10.1.0.4", "4.my.domain.name.")
rd.add_reverse("2001:db8::1", "1.my.domain.name.")

rd.dump_zones(".")
```

This dumps reverse zones in "." for each /24 or /48 network depending on
whether it's IPv4 or IPv6

## Arguments

The Pytter object is constructed as such:

```python
    def __init__(self, primary_server, email, nameservers=[],
                 default_ttl=86400, refresh=14400, retry=1800, expire=1209600,
                 minimum_ttl=3600, soa_ttl=1800, aggregate_v4=24,
                 aggregate_v6=48):
```

These arguments are defined like this:

```python
'default_ttl' : 86400, # TTL to set as $TTL
'primary_server' : None, # The hostname for the primary DNS server
'email' : None, # The email address in DNS style
'refresh' : 14400, # Time to Refresh
'retry' : 1800, # Time to Retry
'expire' : 1209600, # Time to Expire
'minimum_ttl' : 3600, # Minimum Time to Live
'soa_ttl' : 1800, # The TTL of the SOA record
'nameservers' : [], # Additional NS records
'aggregate_v4' : 24, # The zone size to aggregate to for IPv4
'aggregate_v6' : 48 # The zone size to aggregate to for IPv6
```

## Setting the Serial

The serial of the zones are automatically set to YYYYMMDD00, but can be set to
whatever you want.

```python

rd = pytter.Pytter(config)

rd.serialnumber = time.strftime("%Y%m%d01")

```

## Zone aggregation

Normally zones are considered to follow a /24 boundary for IPv4 and /48 for
IPv6. You may want to change this for IPv6, if you are generating reverse for,
say a /32 or larger. Set the `aggregate_v6` option for this (or `aggregate_v4`
for IPv4).

## Contact and disclaimer

This library is not meant for serious work. If it's working for you, fine, but
I make no guarantees.

If you want to reach out to me, you can do so at eising (at) nordu.net
