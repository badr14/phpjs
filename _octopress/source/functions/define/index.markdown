---
layout: page
title: "JavaScript define function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/define:384
- /functions/view/define
- /functions/view/384
- /functions/define:384
- /functions/384
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's define

{% codeblock misc/define.js lang:js https://raw.github.com/kvz/phpjs/master/functions/misc/define.js raw on github %}
function define (name, value) {
  // Define a new constant
  //
  // version: 903.3016
  // discuss at: http://phpjs.org/functions/define
  // +      original by: Paulo Freitas
  // +       revised by: Andrea Giammarchi (http://webreflection.blogspot.com)
  // + reimplemented by: Brett Zamir (http://brett-zamir.me)
  // *        example 1: define('IMAGINARY_CONSTANT1', 'imaginary_value1');
  // *        results 1: IMAGINARY_CONSTANT1 === 'imaginary_value1'
  var defn, replace, script, that = this,
    d = this.window.document;
  var toString = function (name, value) {
    return 'const ' + name + '=' + (/^(null|true|false|(\+|\-)?\d+(\.\d+)?)$/.test(value = String(value)) ? value : '"' + replace(value) + '"');
  };
  try {
    eval('const e=1');
    replace = function (value) {
      var replace = {
        "\x08": "b",
        "\x0A": "\\n",
        "\x0B": "v",
        "\x0C": "f",
        "\x0D": "\\r",
        '"': '"',
        "\\": "\\"
      };
      return value.replace(/\x08|[\x0A-\x0D]|"|\\/g, function (value) {
        return "\\" + replace[value];
      });
    };
    defn = function (name, value) {
      if (d.createElementNS) {
        script = d.createElementNS('http://www.w3.org/1999/xhtml', 'script');
      } else {
        script = d.createElement('script');
      }
      script.type = 'text/javascript';
      script.appendChild(d.createTextNode(toString(name, value)));
      d.documentElement.appendChild(script);
      d.documentElement.removeChild(script);
    };
  } catch (e) {
    replace = function (value) {
      var replace = {
        "\x0A": "\\n",
        "\x0D": "\\r"
      };
      return value.replace(/"/g, '""').replace(/\n|\r/g, function (value) {
        return replace[value];
      });
    };
    defn = (this.execScript ?
    function (name, value) {
      that.execScript(toString(name, value), 'VBScript');
    } : function (name, value) {
      eval(toString(name, value).substring(6));
    });
  }
  defn(name, value);
}
{% endcodeblock %}

 - [view on github](https://github.com/kvz/phpjs/blob/master/functions/misc/define.js)
 - [edit on github](https://github.com/kvz/phpjs/edit/master/functions/misc/define.js)


### Other PHP functions in the misc extension
{% render_partial _includes/custom/misc.html %}
