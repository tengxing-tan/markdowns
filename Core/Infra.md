## Why DB and Application/Web Servers Are Separated

They are separated because they have different responsibilities in a multi-tier architecture.

- Client browsers send requests to the application or web tier.
- A load balancer may sit in front of multiple web servers and distribute traffic.
- Web or application servers run the application code and talk to the database.
- The database stores and serves persistent data.

Typical request flow:

- Browser -> Load Balancer -> Web/Application Server -> Database

This separation helps with:

- scalability, because each tier can be scaled independently
- reliability, because multiple web servers can run at the same time
- safer deployments, because application and database changes can be rolled out in stages
- security, because the database is usually not exposed directly to client browsers

## What a Web Server Is

A web server is software or a machine that receives HTTP requests and serves web content or forwards requests to application code.

Examples:

- IIS on Windows
- Apache HTTP Server
- Nginx

Important distinction:

- IIS is a web server
- a firewall is not a web server; it is a network security component
- application code may be implemented in files such as `.aspx`, `.cs`, or `.vb`, depending on the technology stack

## How DB Changes Relate to Application Files

Database changes are not limited to one or two files. Their impact depends on how the system is built.

DB changes may affect:

- SQL migration scripts
- ORM mappings or data-access code
- configuration files such as connection settings
- backend business logic that reads or writes the changed schema
- reports, APIs, or UI screens that depend on the changed data

So this statement is too narrow:

> DB changes only see these files: `db.xml` and `Sources/sql/invitationClientLog_AddColumn_sysmodified.sql`

A more accurate version is:

> DB changes are usually introduced through migration or SQL files, but their effects can also reach configuration, backend code, and any feature that depends on the changed schema.
