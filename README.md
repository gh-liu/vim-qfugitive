# vim-qfugitive

Small add-on for [vim-fugitive](https://github.com/tpope/vim-fugitive) that enhances the quickfix list produced by `:G difftool`: when you visit an entry, you can open the corresponding **context diff** in a vertical split, and optionally enable an **auto diff-follow** mode.

## Requirements

- **Required**: `tpope/vim-fugitive`
- Vim version: uses `getqflist({dict})` fields like `winid`/`id`; recommended **Vim 8+ / recent Neovim**.

## Install

Example with vim-plug:

```vim
Plug 'tpope/vim-fugitive'
Plug 'liu/vim-qfugitive'
```

After installing, run `:helptags ALL` (or `:helptags` for this plugin’s `doc/` directory), then `:help qfugitive`.

## Usage

1. In a git repo, run Fugitive’s difftool (this populates a `cfugitive-difftool` quickfix list):

   - `:G difftool`

2. Open the quickfix window: `:copen`. Press `<CR>` on an entry to jump to its buffer.
3. In that buffer:

   - `\d` or `:GDiffWithCtx`: open a vertical diff split for the entry’s “context” version
   - `\D` or `:GDiffWithCtx!`: toggle **Auto diff** (when enabled, switching quickfix entries will auto-open the corresponding diff)

Note: `\d` / `\D` are the literal backslash mappings (`nnoremap \d`), not `<Leader>d`.

## Commands & mappings

These are **buffer-local**: they only exist in buffers that come from Fugitive’s `cfugitive-difftool` quickfix entries.

- `:GDiffWithCtx`: open the corresponding context diff (no-op if already shown)
- `:GDiffWithCtx!`: toggle Auto diff; if a diff buffer is currently shown, it also closes/unloads it
- `\d`: same as `:GDiffWithCtx`
- `\D`: same as `:GDiffWithCtx!`

## FAQ

- **Why does `\d` do nothing?**
  - The mappings/command are only defined for buffers created by Fugitive’s `:G difftool` quickfix entries.
  - Auto diff only triggers while the quickfix window is open *and* the current quickfix list id matches the one captured when the list was created.

## Docs

See `:help qfugitive` (from `doc/qfugitive.txt`).


