# kickstart.nvim

### Introduction

A starting point for Neovim that is:

* Small
* Single-file (with examples of moving to multi-file)
* Documented
* Modular

This repo is meant to be used as by **YOU** to begin your Neovim journey; remove the things you don't use and add what you miss.

Distribution Alternatives:
- [LazyVim](https://www.lazyvim.org/): A delightful distribution maintained by @folke (the author of lazy.nvim, the package manager used here)

### Installation

Kickstart.nvim targets *only* the latest ['stable'](https://github.com/neovim/neovim/releases/tag/stable) and latest ['nightly'](https://github.com/neovim/neovim/releases/tag/nightly) of Neovim. If you are experiencing issues, please make sure you have the latest versions.

* Backup your previous configuration
* (Recommended) Fork this repo (so that you have your own copy that you can modify).
* Clone the kickstart repo into `$HOME/.config/nvim/` (Linux/Mac) or `~/AppData/Local/nvim/` (Windows)
  * If you don't want to include it as a git repo, you can just clone it and then move the files to this location
* Start Neovim (`nvim`) and allow `lazy.nvim` to complete installation.
* Restart Neovim
* **You're ready to go!**

Additional system requirements:
- Make sure to review the readmes of the plugins if you are experiencing errors. In particular:
  - [ripgrep](https://github.com/BurntSushi/ripgrep#installation) is required for multiple [telescope](https://github.com/nvim-telescope/telescope.nvim#suggested-dependencies) pickers.
- See as well [Windows Installation](#Windows-Installation)

### Configuration And Extension

* Inside of your fork, feel free to modify any file you like! It's your fork!
* Then there are two primary configuration options available:
  * Include the `lua/kickstart/plugins/*` files in your configuration.
  * Add new configuration in `lua/custom/plugins/*` files, which will be auto sourced using `lazy.nvim`
    * NOTE: To enable this, you need to uncomment `{ import = 'custom.plugins' }` in your `init.lua`

You can also merge updates/changes from the repo back into your fork, to keep up-to-date with any changes for the default configuration

#### Example: Adding an autopairs plugin

In the file: `lua/custom/plugins/autopairs.lua`, add:

```lua
-- File: lua/custom/plugins/autopairs.lua

return {
  "windwp/nvim-autopairs",
  config = function()
    require("nvim-autopairs").setup {}
  end,
}
```


This will automatically install `nvim-autopairs` and enable it on startup. For more information, see documentation for [lazy.nvim](https://github.com/folke/lazy.nvim).

#### Example: Adding a file tree plugin

In the file: `lua/custom/plugins/filetree.lua`, add:

```lua
return {
  "nvim-neo-tree/neo-tree.nvim",
  version = "*",
  dependencies = {
    "nvim-lua/plenary.nvim",
    "nvim-tree/nvim-web-devicons", -- not strictly required, but recommended
    "MunifTanjim/nui.nvim",
  },
  config = function ()
    -- Unless you are still migrating, remove the deprecated commands from v1.x
    vim.cmd([[ let g:neo_tree_remove_legacy_commands = 1 ]])

    require('neo-tree').setup {}
  end,
}
```

This will install the tree plugin and add the command `:NeoTree` for you. You can explore the documentation at [neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim) for more information.

#### Example: Adding a file to change default options

To change default options, you can add a file in the `/after/plugin/` folder (see `:help load-plugins`) to include your own options, keymaps, autogroups, and more. The following is an example `defaults.lua` file (located at `$HOME/.config/nvim/after/plugin/defaults.lua`).

```lua
vim.opt.relativenumber = true

vim.keymap.set('n', '<leader>sr', require('telescope.builtin').resume, { desc = '[S]earch [R]esume' })
```
