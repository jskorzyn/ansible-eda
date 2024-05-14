# Event-Driven Ansible Demos

## Scenarios

1. Webhook with Curl
2. URL watch
3. EDA with GitOps

### 1. Webhook with Curl

#### Prerequsite

1. Eda controller or `ansible-rulebook` running
2. EDA Git project - with calalog structure (rulebook folder)

#### Rulebook Example

```yaml
---
- name: Webhook with curl
  hosts: all
  sources:
    - ansible.eda.webhook:
        host: 0.0.0.0
        port: 5000
  rules:
    - name: Test action
      condition: event.payload.message == "test"
      action:
        debug:
```

#### How to trigger

```bash
curl -H 'Content-Type: application/json' -d "{\"message\": \"test\"}" 10.28.20.18:5000/endpoint
```

* 10.28.20.18 - EDA controller IP
* port 5000 - webhook plugin listening port

## 3. EDA GitOps

### GitLab Webhook definition

```html
http://10.28.20.18:5000/endpoint

Trigger: Push
```
