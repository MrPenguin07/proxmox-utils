##### Copyright (c) 2021-2024 tteck  
##### Author: tteck (tteckster)

```
    _______ __                     __                    ______     _
   / ____(_) /__  _______  _______/ /____  ____ ___     /_  __/____(_)___ ___
  / /_  / / / _ \/ ___/ / / / ___/ __/ _ \/ __ `__ \     / / / ___/ / __ `__ \
 / __/ / / /  __(__  ) /_/ (__  ) /_/  __/ / / / / /    / / / /  / / / / / / /
/_/   /_/_/\___/____/\__, /____/\__/\___/_/ /_/ /_/    /_/ /_/  /_/_/ /_/ /_/
                    /____/
```
#### Can be run manually via Proxmox Shell;
`# bash -c "$(wget -qLO - https://github.com/MrPenguin07/proxmox-utils/raw/master/fstrim-script/fstrim.sh)"`

#### Or made into a cron job;
```
30 0 * * 0 sh -c 'pct list | awk "/^[0-9]/ {print $1}" | \
while read ct; do template=$(pct config $ct | \
grep -q "template:" && echo "true" || echo "false"); \
if [ "$template" = "false" ]; then echo "$(date +'%Y-%m-%d') \
$(pct fstrim $ct)"; fi; done >> /var/log/fstrim-cron.log 2>/dev/null'
```
