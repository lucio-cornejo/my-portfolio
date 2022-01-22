---
title: "Escaping the Tsukuyomi ..."
weight: 3
subtitle: "Setting up the inf_mr() function in Visual Studio Code"
excerpt: "Xaringan is a R package which allows us to create HTML slide presentations using R Markdown and Remark.js ."
date: 2021-12-28
draft: false
---

Here is another workaround I've had to implement when working with Xaringan, now in the case of live creation of Xaringan presentations.

## Xaringan's inf_mr() function

When working on a Xaringan presentation in RStudio, the _xaringan::inf_mr()_ function activates a live preview of the Xaringan final presentation, which now displays changes when they are typed in the Rmd file, **no longer needing to be constantly knitting** in order to see the final Xaringan presentation.

It's an amazing function, yes, but, once again, it hasn't worked well enough for me, due to the following:

- RStudio takes too long (3 seconds perhaps) to update the preview of the final Xaringan presentation, _although it may be due to my slow pc_. Supposedly, such lag can be altered, as explained [here](https://yihui.org/en/2019/02/ultimate-inf-mr/), 
but it has not worked for me.

- RStudio's Markdown snippets work separately but not always when activating one after the other with one snippet's output inside the other one's output. There is a slight workaround to this issue via only using `${0}` (no `${n}` for positive integers n) in RStudio's Markdown snippets, but that's quite limiting for the types of snippets I usually work with.

- It may just be bad luck, but many times I've experienced that such function does not start updating the Xaringan preview as intended, and it takes a couple calls to the function for it to actually start working.

Either way, assuming you already have **R** installed, this is how I've setup my VS Code session in order to have a **replacement** (better for me at least) of Xaringan's lovely inf_mr() function.

- **Step zero** \
  Install [VS Code](https://code.visualstudio.com/download).

- **Step one**  
  Install the following VS Code extensions:
    - [R](https://marketplace.visualstudio.com/items?itemName=Ikuyadeu.r)
    - [R Markdown](https://marketplace.visualstudio.com/items?itemName=TianyiShi.rmarkdown) 
    - [multi-command](https://marketplace.visualstudio.com/items?itemName=ryuta46.multi-command)

- **Step two** \
  Follow [this](https://www.youtube.com/watch?v=EDJqHZx0JnQ&t=188s&ab_channel=NickEubank) video's instructions in order to be able to execute **R** code in **VS Code**.

- **Step three** \
  Appropriately add the following to your `settings.json` file in VS Code (press ctrl+, to open it and then press the button in the upper right corner which opens its JSON file):
```json
"multiCommand.commands": [
  {
    "command": "multiCommand.globalKnit",
        "sequence": [
            // Only works if Rmd file requires rmarkdown::render(...) to get knitted,
            // so so not for Shiny apps or Blogdown sites, but creating its VS Code 
            // shortcuts requires only one line change of this multiCommand.
            "copyFilePath",
            "workbench.action.files.save",
            "editor.action.insertLineAfter",

            // Only insert this next line if your PC uses \ for file directories, like Windows does
            { "command": "type", "args": { "text": "tempo = gsub('\"','', gsub('\\\\\\\\','\/',readClipboard()))\n" } },
            // If that's not the case for you, uncomment the following line:
            // { "command": "type", "args": { "text": "tempo = readClipboard()\n" } },

            { "command": "type", "args": { "text": "file_name = tail(strsplit(tempo,'/')[[1]],n=1)\n"} },
            { "command": "type", "args": { "text": "file_path = substr(tempo,1,nchar(tempo)-nchar(file_name))\n" } },
            { "command": "type", "args": { "text": "setwd(file_path)\n" } },
            { "command": "type", "args": { "text": "rmarkdown::render(file_name)" } }, 
            
            "cursorUp","cursorUp","cursorUp","cursorUp",
            "expandLineSelection","expandLineSelection",
            "expandLineSelection","expandLineSelection",
            "expandLineSelection",

            "r.runSelection",               // Execute via R the lines just selected
            "editor.action.deleteLines",    // Delete the lines just added in order to knit the document
            "workbench.action.files.save"   // save the Rmd file that was just knitted
        ]
    },
    {
        "command": "multiCommand.knit",
        "sequence": [
            "workbench.action.files.save",
            "editor.action.insertLineAfter",
            { "command": "type", "args": { "text": "rmarkdown::render(file_name)" } },
            "expandLineSelection", 
            "r.runSelection",
            "editor.action.deleteLines",
            "workbench.action.files.save"
        ]
    }
]
```
  Basically, the **globalKnit** command uses the path of the Rmd document to be knitted in order to execute in **R** the command to actually knit it, so it takes about a second longer than the **knit** command, which is used only after having used once the **globalKnit** command, in order to get the correct directory where the Rmd document to be knitted is located and the name of such file. \
  You can read [this](https://stackoverflow.com/questions/17605563/efficiently-convert-backslash-to-forward-slash-in-r) if you wish to understand the use of the **gsub()** function. 

  - **Step four** \
    Appropriately add to your `keybindings.json` file in VS Code (to open it, press ctrl+k followed by ctrl+s, then open its JSON file via a button in the top right corner) the following:
    ```json
    {
        "key": "ctrl+shift+k", 
        "command": "extension.multiCommand.execute",
        "args": { "command": "multiCommand.globalKnit" },
        "when": "editorTextFocus"
    },
    {
        "key": "ctrl+alt+k", // Faster R Markdown knit
        "command": "extension.multiCommand.execute",
        "args": { "command": "multiCommand.knit" },
        "when": "editorTextFocus"
    }
    ```
    There, you can change the keyboard inputs to activate the commands 
    **globalKnit** and **knit** that we recently defined.
  
- **Step five** \
  The only thing missing in order to be able to knit Rmd documents
  in VS Code is installing [Pandoc](https://pandoc.org/installing.html). \
  However, that installation is required whenever R Markdown uses Pandoc, obviously, which Xaringan does not. So perhaps it's unnecessary to install Pandoc if you only wish to knit Xaringan documents,
  in which case simply run `xaringan::inf_mr()` in your VS Code terminal with **R** in order to activate the live updates of your Xaringan slides and knitting upon saving the Rmd file. \
  The RStudio snippets I mentioned can be overcome with VS Code snippets,
  I believe that due to the fact that a window with your snippets pops up when you are writing one, so you can select the desired snippet with the keyboard whenever the _bug_ which made them fail in RStudio occurs. Such window does not show up in RStudio when working with R Markdown files, although it does for other type of files, so I guess the small _bug_ could be fixed via adding to RStudio's R Markdown files such pop up window with snippets suggestions.

- **Step six**<br>
  An alternative to `xaringan::inf_mr()` is using the VS Code extesion 
  **Live Server** for the xaringan's html output file, and with the help 
  of some VS Code snippets, write directly into the HTML file and appropriately 'copy,paste,knit' such modifications into the Rmd file
  of the Xaringan presentation being edited live.<br>
  It seems like a tedious process, but I find it just fine and worth
  the result (faster and more reliable live updating of the 
  xaringan presentation).