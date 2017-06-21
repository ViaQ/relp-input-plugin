# RELP input plugin

Plugin for input to fluentd using [RELP protocol](http://www.rsyslog.com/doc/relp.html)

this depends on `relp` ruby gem which host server-side ruby implementation

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'fluent-plugin-relp'
```

Or install it yourself as:

    $ gem install fluent-plugin-relp

## Usage

To use the plugin just add tou your fluent.conf file:
```aconf
<source>
  @type relp
  #optionally, specify port on which to start relp server, defaults to 5170
  port XXXX
  #optionally, specify a tag with which to mark messages received over this connection 
  tag remote
  #optionally, determine remote IP to bind to, by default binds to all incoming connections
  bind XX.XX.XX.XX
</source>

```
With the above set up your fluentd is ready to accept messages transported by RELP, for example logs
sent by rsyslog's `omrelp` module, example of setting up (/etc/rsyslog.conf file):

```aconf 
module(load="omrelp")

*.* (action="omrelp", 
	Target="your_fluentd_host_or_ip" 
	Port="5170_or_yours_set" 
	Protocol="tcp")
```

That is all you need to reliably send system logs to remote fluentd instance.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/ViaQ/fluent-plugin-relp.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
