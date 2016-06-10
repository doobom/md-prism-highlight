# md-prism-highlight
Pelican plugin that highlight codeblocks in markdown using [Prism](http://prismjs.com/index.html).

This is done by providing a custom markdown fenced code block extension that replaces the original one.

Note: remember to remove the default codehilite extension which is enabled by pelican.

## Installation

#### Enable plugin
Add `md-prism-highlight` to pelican config file. See [official documentation](http://docs.getpelican.com/en/3.6.3/plugins.html#how-to-use-plugins) for more info.

```
PLUGINS = ['md-prism-highlight',]
```

#### Include Prism
The default theme doesn't include Prism. But it's easy to download and add it to your theme (possibly in `base.html`). Please follow the instruction on the [download page](http://prismjs.com/download.html).

Please note to include corresponding Prism plugins if you need its functionality.

## Usage
Just write code using fenced code block syntax as usual. Additional options for Prism can be specified either inline or using a preset defined inside pelican config file.

    ```python preset=mypreset lineno=True line=1-4,7
    # some code
    ```

#### Inline options
Inline options are specified directly right after the opening fence, in the same line. It has the format `language( key=value)*`.

Note that the first `language` option is mandatory, as Prism doesn't auto detect language. See Prism official site for a list of [supported languages](http://prismjs.com/index.html#languages-list).

Inline options take precedence over options set in preset. So you can load a preset and override some specific options.

However no space is allowed in both keys and values as it's used for seprate key-value pairs. And no escape is possible to avoid complex parsing code. In this case you can still specify value containing spaces and other special characters using preset.

#### Preset
Preset allows you to group related options and apply them easily to multiple code blocks. They are specified in the pelican config file as a dictionary, under `PRISM_PRESET`.

```python
PRISM_PRESET = {
    'mypreset': {
        'lineno': True,
        'line': '1-4,7',
        'user': 'supercoolusername',
        'start': '2'
    },
    'another': {
        'lineno': False,
        'start': '-5'
    }
}
```

#### Available options
| Option | Default value | Meaning |
|:---:|:---:|:---:|
| `preset` | None | Load a preset. Only available for inline option |
| `lineno` | `True` | Whether enable line number |
| `classes` | None | Additional classes applied to the `pre` tag, splited by `,` |
| other | None | Directly passed as a data attribute of the `pre` tag. For example, `line=1-4,7` will be `<pre data-line="1-4,7">`. This way, you can pass arbitrary options to Prism |
