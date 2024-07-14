# Backend

The [backend](https://github.com/NucleoidMC/nucleoid-backend) is run from `/home/minecraft/services/backend/`, using `screen` as the `minecraft` user.

## Updating

Download the latest binary from [Github Actions](https://github.com/NucleoidMC/nucleoid-backend/actions) (I use the `gh` cli for this), and put move it to `/home/minecraft/services/backend/nucleoid-backend`. Then connect to the backend `screen` session, ctrl-c and [re-run the backend](../../../guides/reboot#start-up-standalone-services).
