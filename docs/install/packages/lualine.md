# Lualine - modeline theme

[nvim-lualine/lualine.nvim](https://github.com/nvim-lualine/lualine.nvim) is a fast and configurable statusline for neovim

Example status line: evil_lualine

![NeoVim LuaLine - evil-lualine theme](https://user-images.githubusercontent.com/13149513/113875129-4453ba00-97d8-11eb-8f21-94a9ef565db3.png)

<!-- TODO: screenshot of lualine with clojure lsp and conjure runing -->

## Lualine configuration in Fennel

`nvim/fnl/config/plugin/lualine.fnl`

```fennel
(module config.plugin.lualine
  {autoload {core aniseed.core
             lualine lualine
             lsp config.plugin.lspconfig}})

(defn lsp_connection []
  (if (vim.tbl_isempty (vim.lsp.buf_get_clients 0)) "" ""))

(def github-lua-theme
  (core.assoc
    (require :lualine.themes.auto)
    :inactive {:a {:bg "#19181e" :fg "#a4a3a6"}
               :b {:bg "#19181e" :fg "#a4a3a6"}
               :c {:bg "#19181e" :fg "#a4a3a6"}}
    :normal {:a {:bg "#131217" :fg "#24292e"}
             :b {:bg "#131217" :fg "#3b8eea"}
             :c {:bg "#19181e" :fg "#d1d5da"}}
    :command {:a {:bg "#131217" :fg "#24292e"}
              :b {:bg "#131217" :fg "#ccbed8"}
              :c {:bg "#19181e" :fg "#d1d5da"}}
    :visual {:a {:bg "#131217" :fg "#24292e"}
             :b {:bg "#131217" :fg "#ced4b1"}
             :c {:bg "#19181e" :fg "#d1d5da"}}
    :replace {:a {:bg "#131217" :fg "#24292e"}
              :b {:bg "#131217" :fg "#d1b6bd"}
              :c {:bg "#19181e" :fg "#d1d5da"}}
    :insert {:a {:bg "#131217" :fg "#24292e"}
             :b {:bg "#131217" :fg "#a8d1c9"}
             :c {:bg "#19181e" :fg "#d1d5da"}}))

(lualine.setup
  {:options {:theme github-lua-theme
             :icons_enabled true
             :section_separators ["" ""]
             :component_separators ["" ""]}
   :sections {:lualine_a []
              :lualine_b [[:mode {:upper true}]]
              :lualine_c [["FugitiveHead"]
                          [:filename {:filestatus true
                                      :path 1}]]
              :lualine_x [[:diagnostics {:sections [:error
                                                    :warn
                                                    :info
                                                    :hint]
                                         :sources [:nvim_lsp]}]
                          [lsp_connection]
                          :location
                          :filetype]
              :lualine_y [:encoding]
              :lualine_z []}
   :inactive_sections {:lualine_a []
                       :lualine_b []
                       :lualine_c [[:filename {:filestatus true
                                               :path 1}]]
                       :lualine_x []
                       :lualine_y []
                       :lualine_z []}})
```
