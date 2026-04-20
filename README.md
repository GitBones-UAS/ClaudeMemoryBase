.claude/commands contains an /ingest /lint and /wiki command
/ingest directs claude to review all new raw sources and turn them into wiki files to be used in the database and update any connections between nodes
/lint directs claude to scan for any duplicate, orphan, or source-less nodes and either delete, connect or condense them to preserve the health of the database
/wiki directs claude to query the wiki (Vault) based on keywords in the chat before scanning the web for answers to a question.
/wiki is the real value add from this database since it allows claude to access a personal record of files, projects, and summarized chats to give me personalized answers across chats and projects
CLAUDE.md contains the general structure of the database for claude and users to read a undertand
