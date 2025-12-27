# Logseq-style Date Picker for SilverBullet

Ce plug ajoute une commande `/date` qui ouvre un calendrier flottant (OrbitCal).
Un clic sur un jour insère une date formatée à la position du curseur.

```space-lua
local js = require("js")
local system = require("system")

-- Importe le widget OrbitCal installé par le plug
local orbit = js.import("/.fs/Library/orbitcal.js")

-- Lit la configuration globale et fournit une valeur par défaut
local function getDatePickerConfig()
  local cfg = system.getConfig() or {}
  local c = cfg.logseqDatePicker or {}
  return {
    -- format par défaut type Logseq
    format = c.format or "[[YYYY-MM-DD]]",
  }
end

-- Remplace les tokens YYYY / MM / DD dans une chaîne
local function formatDate(iso, fmt)
  -- iso attendu: "2025-12-27"
  local y, m, d = iso:match("^(%d%d%d%d)%-(%d%d)%-(%d%d)$")
  if not (y and m and d) then
    return iso
  end
  local s = fmt
  s = s:gsub("YYYY", y)
  s = s:gsub("MM", m)
  s = s:gsub("DD", d)
  return s
end

command.define {
  name = "Date: Insert (Logseq-style)",
  description = "Insert a formatted date using the floating OrbitCal widget",
  slashCommand = "date",      -- tu tapes /date dans l’éditeur
  key = "Ctrl-Alt-D",         -- raccourci clavier optionnel
  run = function()
    local cfg = getDatePickerConfig()

    -- callback appelé par OrbitCal quand on clique sur un jour
    -- NOTE: si js.tojs n’existe pas dans ta version, essaie de passer
    -- directement la fonction Lua (SilverBullet peut la convertir tout seul).
    local cb = js.tojs(function(iso)
      local text = formatDate(iso, cfg.format)
      editor.insertAtCursor(text .. " ")
    end)

    orbit.ToggleCalendarWithCallback(cb)
  end
}


local cb = function(iso)
  local text = formatDate(iso, cfg.format)
  editor.insertAtCursor(text .. " ")
end

orbit.ToggleCalendarWithCallback(cb)
```
