## Summary

This is a first pass at trying to figure out what auditing might look like. 


### Structure of an audit event

```
type AuditEvent struct {
  Id string,
  UserID string,
  Action string,
  At string,
  Metadata map[string]interface{},
}
```

### What to do with audit events 

- Do we want to store audit events in our database?
- Do we want to emit audit events that an operator can consume?
- Do we want to log audit events in some meaningful way?

#### Store them

```
CREATE TABLE audit_events as (
  id SERIAL PRIMARY KEY,
  user_id TEXT NOT NULL,
  action TEXT NOT NULL,
  at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  metadata JSON,
)
```

Depending on what we choose to store in the database, this table could grow quite quickly. Should audit events be cleaned up in some way? Do we keep them forever? Is this configurable?

This probably won't grow as fast as `build_events` so maybe its not an issue?


#### Emit them
#### Log them
