#!/bin/bash -xe
# run as root to clone master database

cd /tmp
echo Stopping PostgreSQL
service postgresql-9.4 stop

echo Cleaning up old cluster directory
su - postgres -c "rm -rf /var/lib/pgsql/9.4/data/*"

echo Starting base backup as replicator
su - postgres -c "pg_basebackup -w -h {{ pg_ip }} -D /var/lib/pgsql/9.4/data -X stream -U replicator -v -P"

echo Writing recovery.conf file
su - postgres -c "cat > /var/lib/pgsql/9.4/data/recovery.conf <<- EOF
standby_mode = 'on'
primary_conninfo = 'host={{ pg_ip }} port={{ pg_port }} user=replicator password={{ pg_password }}'
trigger_file = '/tmp/postgresql.trigger'
EOF
"
chmod 600 /var/lib/pgsql/9.4/data/recovery.conf

echo Starting PostgreSQL
service postgresql-9.4 start
