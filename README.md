# ranger.nvim

[Ranger](https://github.com/ranger/ranger) integration plugin for neovim.

## Dependencies

- [Ranger](https://github.com/ranger/ranger)

## Install

Install using your package manager. This plugin *does not set* Neovim keymaps by
default, you will need to set your own keymaps. See below [Lazy](https://github.com/folke/lazy.nvim)
configuration for example.

```lua
{
  "kelly-lin/ranger.nvim",
  config = function()
    require("ranger-nvim").setup({ replace_netrw = false })
    vim.api.nvim_set_keymap("n", "<leader>ef", "", { noremap = true, callback = require("ranger-nvim").open })
  end,
},
```

## Configuration

You can configure `ranger.nvim` by invoking `ranger_nvim.setup()` with an
options `table` described below. Note: `ranger_nvim.setup()` is *optional*, if you
do not invoke `ranger_nvim.setup()` `ranger.nvim` will use the default values.

| Key           | Type      | Default | Description                        |
| ------------- | --------- | ------- | ---------------------------------- |
| replace_netrw | `boolean` | `false` | Replace `netrw` with `ranger` when neovim is launched with a directory argument. |
| keybinds      | `Keybind` | See [ranger keybindings](#ranger-keybindings). | Key bindings set in `ranger` to control how files are opened in neovim. See [ranger keybindings](#ranger-keybindings). |

See below code snippet for example configuring `ranger.nvim` with the default
values.

```lua
local ranger_nvim = require("ranger-nvim")
ranger_nvim.setup({
  replace_netrw = false,
    keybinds = {
      ["<C-v>"] = ranger_nvim.OPEN_MODE.vsplit,
      ["<C-o>"] = ranger_nvim.OPEN_MODE.split,
    },
})
```

## API

### `open(select_current_file: boolean)`

Opens `ranger` in a fullscreen floating window.

When `select_current_file` is set to `true`, `ranger` will focus on the file in
the current buffer on load.

You can control how to open these files in Neovim by using the [ranger keybindings](#ranger-keybindings)
that `ranger.nvim` sets.

## Ranger Keybindings

`ranger.nvim` sets `ranger` keybindings in order to control how selected files
are opened in neovim. You can override the keybindings using `ranger_nvim.setup()`.

See below table for default keybindings.

**Note: the keybinding string is in ranger keybinding syntax and not vim syntax
(they are bindings for ranger)**

| Keybinding  | Action |
| ----------- | ------ |
| `<CR>`, `l` (when selected on file) | Open files in current window |
| `<C-v>`                             | Open files in vertical split |
| `<C-o>`                             | Open files in horizontal split |

### Overriding Keybindings

The `ranger-nvim` module provides an `OPEN_MODE` enum which is used to control
the open modes. To override keybinds, create an entry in the `keybinds` table
with a `string` key in **ranger** keybinding syntax (the same syntax you would
use in your `rc.conf`) and the value of an `OPEN_MODE` variant.

```lua
local ranger_nvim = require("ranger-nvim")
ranger_nvim.setup({
    keybinds = {
      ["<C-v>"] = ranger_nvim.OPEN_MODE.vsplit,
      ["<C-o>"] = ranger_nvim.OPEN_MODE.split,
    },
})
```

## Contributing

All feature/pull requests are welcome!
