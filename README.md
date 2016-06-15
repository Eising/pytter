# Pytter
A really stupid library for Python to manage reverse DNS

# Examples

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
