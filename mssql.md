# Basic

Queries aren't fired until you give the `GO`.

# Import

```
RESTORE FILELISTONLY
from disk='/backup/fine-backup.bak'
go
```

Get values from columns `LogicalName` and `PhysicalName`, then use Logical name to assign
a new filename, by moving the volume to it.

```
restore database [db-name] from disk='/backup/fine-backup.bak'
with move 'db-name0data' to '/casket/db-name.mdf'
, move 'db-name0log' to '/casket/db-name_l.ldf'
go
```

# Language

## Syntaxe

To escape a symbol, squared brack are used:

```tsql
use [hyphen-separated];
go
```

## Database manipulation

Show available databases:

```tsql
SELECT name, database_id FROM sys.databases;
```

## Table manipulation
