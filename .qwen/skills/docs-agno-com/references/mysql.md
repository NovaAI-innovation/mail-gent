# MySQL

**Source:** https://docs.agno.com/database/providers/mysql/overview.md
**Section:** Docs

**Description:** Use MySQL for agent session storage and persistence.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# MySQL

> Use MySQL for agent session storage and persistence.

Agno supports using [MySQL](https://www.mysql.com/) as a database with the `MySQLDb` class.

## Usage

```python mysql_for_agent.py theme={null}
from agno.agent import Agent
from agno.db.mysql import MySQLDb

# Setup your Database
db = MySQLDb(db_url="mysql+pymysql://ai:ai@localhost:3306/ai")

# Setup your Agent with the Database
agent = Agent(db=db)
```

### Run MySQL

Install [docker desktop](https://docs.docker.com/desktop/install/mac-install/) and run **MySQL** on port **3306** using:

```bash  theme={null}
docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=ai \
  -e MYSQL_DATABASE=ai \
  -e MYSQL_USER=ai \
  -e MYSQL_PASSWORD=ai \
  -p 3306:3306 \
  -d mysql:8
```

## Params

<Snippet file="db-mysql-params.mdx" />
