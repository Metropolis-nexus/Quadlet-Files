# Account provisioning

To provision accounts, set `NEXT_PUBLIC_DISABLE_SIGNUP=false` and register all users through OIDC. Set `NEXT_PUBLIC_DISABLE_SIGNUP=true` when done. Documenso currently does not have a way to allow registration via OIDC while blocking registration via email.

To promote an account to admin, run:

```
root@documenso:~# podman exec -it documenso-postgres /bin/ash
documenso=# UPDATE "User" SET roles = '{ADMIN}' WHERE email = 'akadmin@auth.metropolis.nexus';
documenso=# exit
/ $ exit
```

# Postgres Optimizations

Adjust `/srv/documenso/postgres/postgresql.conf` to include these optimizations:

```
# https://docs.documenso.com/docs/self-hosting/configuration/database#monitoring

shared_buffers = 1GB
effective_cache_size = 3GB
work_mem = 64MB
maintenance_work_mem = 512MB
max_connections = 100
```

If running directly on ZFS, also include these optimizations:

```
# https://vadosware.io/post/everything-ive-seen-on-optimizing-postgres-on-zfs-on-linux/

full_page_writes = off
wal_init_zero = off
wal_recycle = off
```