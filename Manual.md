### CLI command - tables
```
NAME:
   clickhouse-backup-race tables - List list of tables, exclude skip_tables

USAGE:
   clickhouse-backup tables [-t, --tables=<db>.<table>]] [--all]

OPTIONS:
   --config value, -c value                 Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --all, -a                                print table even when match with skip_tables pattern
   --table value, --tables value, -t value  list tables only match with table name patterns, separated by comma, allow ? and * as wildcard
   
```
### CLI command - create
```
NAME:
   clickhouse-backup-race create - Create new backup

USAGE:
   clickhouse-backup create [-t, --tables=<db>.<table>] [--partitions=<partition_names>] [-s, --schema] [--rbac] [--configs] <backup_name>

DESCRIPTION:
   Create new backup

OPTIONS:
   --config value, -c value                          Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --table value, --tables value, -t value           create backup only matched with table name patterns, separated by comma, allow ? and * as wildcard
   --partitions value                                create backup only for selected partition names, separated by comma
   --schema, -s                                      Backup schemas only
   --rbac, --backup-rbac, --do-backup-rbac           Backup RBAC related objects only
   --configs, --backup-configs, --do-backup-configs  Backup 'clickhouse-server' configuration files only
   
```
### CLI command - create_remote
```
NAME:
   clickhouse-backup-race create_remote - Create and upload

USAGE:
   clickhouse-backup create_remote [-t, --tables=<db>.<table>] [--partitions=<partition_names>] [--diff-from=<local_backup_name>] [--diff-from-remote=<local_backup_name>] [--schema] [--rbac] [--configs] [--resumable] <backup_name>

DESCRIPTION:
   Create and upload

OPTIONS:
   --config value, -c value                          Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --table value, --tables value, -t value           create and upload backup only matched with table name patterns, separated by comma, allow ? and * as wildcard
   --partitions value                                create and upload backup only for selected partition names, separated by comma
   --diff-from value                                 local backup name which used to upload current backup as incremental
   --diff-from-remote value                          remote backup name which used to upload current backup as incremental
   --schema, -s                                      Backup and upload metadata schema only
   --rbac, --backup-rbac, --do-backup-rbac           Backup and upload RBAC related objects only
   --configs, --backup-configs, --do-backup-configs  Backup 'clickhouse-server' configuration files only
   --resume, --resumable                             Save intermediate upload state and resume upload if backup exists on remote storage, ignore when 'remote_storage: custom' or 'use_embedded_backup_restore: true'
   
```
### CLI command - upload
```
NAME:
   clickhouse-backup-race upload - Upload backup to remote storage

USAGE:
   clickhouse-backup upload [-t, --tables=<db>.<table>] [--partitions=<partition_names>] [-s, --schema] [--diff-from=<local_backup_name>] [--diff-from-remote=<remote_backup_name>] [--resumable] <backup_name>

OPTIONS:
   --config value, -c value                 Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --diff-from value                        local backup name which used to upload current backup as incremental
   --diff-from-remote value                 remote backup name which used to upload current backup as incremental
   --table value, --tables value, -t value  Upload data only for matched table name patterns, separated by comma, allow ? and * as wildcard
   --partitions value                       Upload data only for selected partition names, separated by comma
   --schema, -s                             Upload schemas only
   --resume, --resumable                    Save intermediate upload state and resume upload if backup exists on remote storage, ignored with 'remote_storage: custom' or 'use_embedded_backup_restore: true'
   
```
### CLI command - list
```
NAME:
   clickhouse-backup-race list - List list of backups

USAGE:
   clickhouse-backup list [all|local|remote] [latest|previous]

OPTIONS:
   --config value, -c value  Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   
```
### CLI command - download
```
NAME:
   clickhouse-backup-race download - Download backup from remote storage

USAGE:
   clickhouse-backup download [-t, --tables=<db>.<table>] [--partitions=<partition_names>] [-s, --schema] [--resumable] <backup_name>

OPTIONS:
   --config value, -c value                 Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --table value, --tables value, -t value  Download objects which matched with table name patterns, separated by comma, allow ? and * as wildcard
   --partitions value                       Download data only for selected partition names, separated by comma
   --schema, -s                             Download schema only
   --resume, --resumable                    Save intermediate download state and resume download if backup exists on local storage, ignored with 'remote_storage: custom' or 'use_embedded_backup_restore: true'
   
```
### CLI command - restore
```
NAME:
   clickhouse-backup-race restore - Create schema and restore data from backup

USAGE:
   clickhouse-backup restore  [-t, --tables=<db>.<table>] [-m, --restore-database-mapping=<originDB>:<targetDB>[,<...>]] [--partitions=<partitions_names>] [-s, --schema] [-d, --data] [--rm, --drop] [-i, --ignore-dependencies] [--rbac] [--configs] <backup_name>

OPTIONS:
   --config value, -c value                            Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --table value, --tables value, -t value             Restore only database and objects which matched with table name patterns, separated by comma, allow ? and * as wildcard
   --restore-database-mapping value, -m value          Define the rule to restore data. For the database not defined in this struct, the program will not deal with it.
   --partitions value                                  Restore data only for selected partition names, separated by comma
   --schema, -s                                        Restore schema only
   --data, -d                                          Restore data only
   --rm, --drop                                        Drop exists schema objects before restore
   -i, --ignore-dependencies                           Ignore dependencies when drop exists schema objects
   --rbac, --restore-rbac, --do-restore-rbac           Restore RBAC related objects only
   --configs, --restore-configs, --do-restore-configs  Restore 'clickhouse-server' CONFIG related files only
   
```
### CLI command - restore_remote
```
NAME:
   clickhouse-backup-race restore_remote - Download and restore

USAGE:
   clickhouse-backup restore_remote [--schema] [--data] [-t, --tables=<db>.<table>] [-m, --restore-database-mapping=<originDB>:<targetDB>[,<...>]] [--partitions=<partitions_names>] [--rm, --drop] [-i, --ignore-dependencies] [--rbac] [--configs] [--skip-rbac] [--skip-configs] [--resumable] <backup_name>

OPTIONS:
   --config value, -c value                            Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --table value, --tables value, -t value             Download and restore objects which matched with table name patterns, separated by comma, allow ? and * as wildcard
   --restore-database-mapping value, -m value          Define the rule to restore data. For the database not defined in this struct, the program will not deal with it.
   --partitions value                                  Download and restore data only for selected partition names, separated by comma
   --schema, -s                                        Download and Restore schema only
   --data, -d                                          Download and Restore data only
   --rm, --drop                                        Drop schema objects before restore
   -i, --ignore-dependencies                           Ignore dependencies when drop exists schema objects
   --rbac, --restore-rbac, --do-restore-rbac           Download and Restore RBAC related objects only
   --configs, --restore-configs, --do-restore-configs  Download and Restore 'clickhouse-server' CONFIG related files only
   --resume, --resumable                               Save intermediate upload state and resume upload if backup exists on remote storage, ignored with 'remote_storage: custom' or 'use_embedded_backup_restore: true'
   
```
### CLI command - delete
```
NAME:
   clickhouse-backup-race delete - Delete specific backup

USAGE:
   clickhouse-backup delete <local|remote> <backup_name>

OPTIONS:
   --config value, -c value  Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   
```
### CLI command - default-config
```
NAME:
   clickhouse-backup-race default-config - Print default config

USAGE:
   clickhouse-backup-race default-config [command options] [arguments...]

OPTIONS:
   --config value, -c value  Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   
```
### CLI command - print-config
```
NAME:
   clickhouse-backup-race print-config - Print current config merged with environment variables

USAGE:
   clickhouse-backup-race print-config [command options] [arguments...]

OPTIONS:
   --config value, -c value  Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   
```
### CLI command - clean
```
NAME:
   clickhouse-backup-race clean - Remove data in 'shadow' folder from all 'path' folders available from 'system.disks'

USAGE:
   clickhouse-backup-race clean [command options] [arguments...]

OPTIONS:
   --config value, -c value  Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   
```
### CLI command - clean_remote_broken
```
NAME:
   clickhouse-backup-race clean_remote_broken - Remove all broken remote backups

USAGE:
   clickhouse-backup-race clean_remote_broken [command options] [arguments...]

OPTIONS:
   --config value, -c value  Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   
```
### CLI command - watch
```
NAME:
   clickhouse-backup-race watch - Run infinite loop which create full + incremental backup sequence to allow efficient backup sequences

USAGE:
   clickhouse-backup watch [--watch-interval=1h] [--full-interval=24h] [--watch-backup-name-template=shard{shard}-{type}-{time:20060102150405}] [-t, --tables=<db>.<table>] [--partitions=<partitions_names>] [--schema] [--rbac] [--configs]

DESCRIPTION:
   Create and upload

OPTIONS:
   --config value, -c value                          Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --watch-interval value                            Interval for run 'create_remote' + 'delete local' for incremental backup, look format https://pkg.go.dev/time#ParseDuration
   --full-interval value                             Interval for run 'create_remote'+'delete local' when stop create incremental backup sequence and create full backup, look format https://pkg.go.dev/time#ParseDuration
   --watch-backup-name-template value                Template for new backup name, could contain names from system.macros, {type} - full or incremental and {time:LAYOUT}, look to https://go.dev/src/time/format.go for layout examples
   --table value, --tables value, -t value           Create and upload only objects which matched with table name patterns, separated by comma, allow ? and * as wildcard
   --partitions value                                partition names, separated by comma
   --schema, -s                                      Schemas only
   --rbac, --backup-rbac, --do-backup-rbac           Backup RBAC related objects only
   --configs, --backup-configs, --do-backup-configs  Backup `clickhouse-server' configuration files only
   
```
### CLI command - server
```
NAME:
   clickhouse-backup-race server - Run API server

USAGE:
   clickhouse-backup-race server [command options] [arguments...]

OPTIONS:
   --config value, -c value            Config 'FILE' name. (default: "/etc/clickhouse-backup/config.yml") [$CLICKHOUSE_BACKUP_CONFIG]
   --watch                             run watch go-routine for 'create_remote' + 'delete local', after API server startup
   --watch-interval value              Interval for run 'create_remote' + 'delete local' for incremental backup, look format https://pkg.go.dev/time#ParseDuration
   --full-interval value               Interval for run 'create_remote'+'delete local' when stop create incremental backup sequence and create full backup, look format https://pkg.go.dev/time#ParseDuration
   --watch-backup-name-template value  Template for new backup name, could contain names from system.macros, {type} - full or incremental and {time:LAYOUT}, look to https://go.dev/src/time/format.go for layout examples
   
```