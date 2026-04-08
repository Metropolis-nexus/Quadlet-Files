# Account provisioning

To provision accounts, set `NEXT_PUBLIC_DISABLE_SIGNUP=false` and register all users through OIDC. Set `NEXT_PUBLIC_DISABLE_SIGNUP=true` when done. Documenso currently does not have a way to allow registration via OIDC while blocking registration via email.

To promote an account to admin, run:

```
root@documenso:~# podman exec -it documenso-postgres /bin/ash
documenso=# UPDATE "User" SET roles = '{ADMIN}' WHERE email = 'akadmin@auth.metropolis.nexus';
documenso=# exit
/ $ exit
```