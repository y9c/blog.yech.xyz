+++
title = "Use Black as Formatter for Jupyter Notebook"
description = ""
featured_image = ""
date = 2019-01-31T20:34:01+08:00
categories = ["coding"]
tags = ["editor", "python"]
comment = true
+++

> How to setup?

1. Install Nbextensions in jupyter notebook.

   see https://github.com/ipython-contrib/jupyter_contrib_nbextensions#1-install-the-python-package

1. Enable `code prettify` Nbextensions in jupyter notebook.

   check the box in setting page

1. Paste the configuration below into `Prameters`.

   ```json
   {
     "python": {
       "library": "import json\ndef black_reformat(cell_text):\n    import black\n    import re\n    cell_text = re.sub('^%', '#%#', cell_text, flags=re.M)\n    try:\n        reformated_text = black.format_str(cell_text, 88)\n    except TypeError:\n        reformated_text = black.format_str(cell_text, mode=black.FileMode(line_length=88))\n    return re.sub('^#%#', '%', reformated_text, flags=re.M)",
       "prefix": "print(json.dumps(black_reformat(u",
       "postfix": ")))"
     },
     "r": {
       "library": "library(formatR)\nlibrary(jsonlite)",
       "prefix": "cat(toJSON(paste(tidy_source(text=",
       "postfix": ", output=FALSE)[['text.tidy']], collapse='\n')))"
     },
     "javascript": {
       "library": "jsbeautify = require('js-beautify')",
       "prefix": "console.log(JSON.stringify(jsbeautify.js_beautify(",
       "postfix": ")));"
     }
   }
   ```

> Reference

1. https://neuralcoder.science/Black-Jupyter/
1. https://github.com/csurfer/blackcellmagic/issues/5
