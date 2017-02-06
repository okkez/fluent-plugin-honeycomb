
## Getting started

1. Install this plugin with `gem install fluent-plugin-honeycomb`

2. A minimal configuration looks like this:

```

<match your_match>
  @type honeycomb
  writekey "YOUR_WRITEKEY"
  dataset "fluentd_test_dataset"
</match>
```

## Configuration

### Basic options

Parameter | Type | Required? | Description
| --- | --- | --- | --- |
| `writekey` | string | yes | Your Honeycomb write key. |
| `dataset | string | yes | The name of the destination dataset in
your Honeycomb account. |
| `sample_rate` | integer | no | Sample your event stream by sending 1 out of every N events. |
| `include_tag_key` | bool | no | Whether to include the Fluentd tag in the submitted event. |
| `tag_key` | string | no | If `include_tag_key` is `true`, the tag key name in the event (default: `fluentd_tag`).

### Buffering options

`fluent-plugin-honeycomb` supports the [standard configuration options](http://docs.fluentd.org/v0.12/articles/buffer-plugin-overview) for buffered output plugins.

### Unusual options

You shouldn't usually need to adjust these.

Parameter | Type | Required? | Description
| --- | --- | --- | --- |
| `api_host` | string | no | Base URL to send events to (default: `https://api.honeycomb.io` |

## Limitations

`fluent-plugin-honeycomb` does not currently batch events. This functionality should be implemented in `libhoney-rb`.

## Development
I recommend using [rbenv](https://github.com/rbenv/rbenv) for development.

To set up Fluentd, run:

```
gem install fluentd
fluentd --setup ./fluent
```

Edit the configuration file at `./fluent/fluent.conf`, then run

```
fluentd -c ./fluent/fluent.conf -v
```

A note about naming: The gem must be named `fluent-plugin-xxx` in order to automatically be included in Fluentd's plugin list. See http://www.fluentd.org/faqs.