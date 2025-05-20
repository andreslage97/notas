```bash
git rebase -i 1234
```
### Traer archivos de otros commits
```bash
git checkout abc1234 -- src/Service/UserService.php
```
### Añadir cambios de la rama que partiste
```bash
# 1. Trae los cambios del remoto
git fetch origin nombre-de-la-rama

# 2. Haz el merge con --no-ff explícitamente
git merge --no-ff origin/nombre-de-la-rama

```
