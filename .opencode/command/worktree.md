---
description: Crea un worktree git en .worktrees/<nombre-derivado> inferido del argumento. No hace nada más.
---

El argumento escrito por el usuario NO se usa directamente. Deriva de él un nombre de worktree seguro ("slug"):

1. Toma todo el argumento ($ARGUMENTS).
2. Conviértelo en un nombre de carpeta válido:
   - minúsculas
   - quita tildes/diacríticos y caracteres especiales
   - espacios → guiones "-"
   - colapsa guiones repetidos; recorta guiones iniciales/finales
   - conserva solo a-z, 0-9, guiones y guiones bajos
   - si queda vacío, usa "worktree"
3. Ejecuta exactamente:

git worktree add .worktrees/<nombre-derivado>

Ejemplo: /worktree Nuevo login de usuario → git worktree add .worktrees/nuevo-login-de-usuario

NO cambies de directorio, NO hagas checkout, NO crees ramas ni hagas ningún otro cambio. Ejecuta solo ese comando y termina.